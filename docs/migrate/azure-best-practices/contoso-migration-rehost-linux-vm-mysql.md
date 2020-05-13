---
title: Ponowne hostowanie aplikacji dla systemu Linux, używanej do obsługi pomocy technicznej, na platformie Azure i w usłudze Azure Database for MySQL
description: Dowiedz się, jak firma Contoso przeprowadza ponowne hostowanie lokalnej aplikacji dla systemu Linux przez migrację na maszyny wirtualne platformy Azure i do usługi Azure Database for MySQL.
author: givenscj
ms.author: abuck
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 61398802202a33f9c514cf5a5b6a2528e7b662e4
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215997"
---
<!-- cSpell:ignore givenscj OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc contosoosticket osticket InnoDB binlog systemctl NSGs -->

# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Ponowne hostowanie aplikacji lokalnej dla systemu Linux na maszynach wirtualnych platformy Azure i w usłudze Azure Database for MySQL

W tym artykule opisano, w jaki sposób fikcyjna firma Contoso ponownie hostuje dwuwarstwową aplikację opartą na stosie LAMP (Linux, Apache, MySQL, PHP), migrując ją ze środowiska lokalnego na platformę Azure przy użyciu maszyn wirtualnych platformy Azure i usługi Azure Database for MySQL.

Używana w tym przykładzie aplikacja do obsługi pomocy technicznej, osTicket, jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co lokalne systemy i infrastruktura stają się przeciążone.
- **Ograniczanie ryzyka.** Aplikacja do obsługi pomocy technicznej ma kluczowe znaczenie dla działalności firmy. Firma Contoso chce przenieść ją na platformę Azure, eliminując ryzyko.
- **Sunąć.** Firma Contoso nie chce teraz zmieniać używanej aplikacji. Po prostu chce mieć pewność, że aplikacja jest stabilna.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury w firmie Contoso określił cele migracji, aby wybrać najlepszą metodę migracji:

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie, gdy działa w lokalnym środowisku programu VMware. Aplikacja działająca w chmurze będzie miała tak samo krytyczne znaczenie jak w środowisku lokalnym.
- Firma Contoso nie chce inwestować w tę aplikację. Jest ona ważna dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Firma Contoso przeprowadziła już kilka procesów migracji aplikacji dla systemu Windows, a teraz chce poznać sposób korzystania z infrastruktury platformy Azure z systemem Linux.
- Firma Contoso chce zminimalizować zadania administratora bazy danych po przeniesieniu aplikacji do chmury.

## <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu:

- Obecnie aplikacja jest warstwą obejmującą dwie maszyny wirtualne ( `OSTICKETWEB` i `OSTICKETMYSQL` ).
- Maszyny wirtualne znajdują się na hoście VMware ESXi `contosohost1.contoso.com` (wersja 6.5).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (`vcenter.contoso.com`) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (`contoso-datacenter`) i lokalny kontroler domeny (`contosodc1`).
- Aplikacja warstwy internetowej na maszynie `OSTICKETWEB` zostanie przeniesiona na maszynę wirtualną platformy Azure w modelu IaaS.
- Baza danych aplikacji zostanie przeniesiona do usługi typu PaaS, Azure Database for MySQL.
- Ponieważ migracja dotyczy obciążenia produkcyjnego, zasoby będą znajdować się w grupie zasobów produkcyjnych `ContosoRG`.
- `OSTICKETWEB`Zasób zostanie zreplikowany do regionu podstawowego (Wschodnie stany USA 2) i umieszczony w sieci produkcyjnej ( `VNET-PROD-EUS2` ):
  - Internetowa maszyna wirtualna zostanie umieszczona w podsieci frontonu (`PROD-FE-EUS2`).
- Baza danych aplikacji zostanie zmigrowana do Azure Database for MySQL przy użyciu [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

    ![Architektura scenariusza](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi proces migracji w następujący sposób:

Migracja maszyny wirtualnej warstwy internetowej:

- W pierwszym kroku firma Contoso konfiguruje infrastrukturę platformy Azure i lokalną, która jest wymagana do wdrożenia Azure Migrate.
- Mają już [infrastrukturę platformy Azure](./contoso-migration-infrastructure.md) , więc firma Contoso musi dodać i skonfigurować replikację maszyn wirtualnych za pomocą narzędzia do migracji Azure Migrate serwera.
- Po przygotowaniu wszystko firma Contoso może rozpocząć replikację maszyny wirtualnej.
- Po włączeniu replikacji i zakończeniu pracy firma Contoso ukończy przenoszenie przy użyciu Azure Migrate.

Migracja bazy danych:

1. Firma Contoso przeprowadzi aprowizację wystąpienia usługi MySQL na platformie Azure.
2. Firma Contoso konfiguruje Azure Database Migration Service (DMS), zapewniając dostęp do lokalnego serwera baz danych.
3. Firma Contoso migruje bazę danych do Azure Database for MySQL.

    ![Proces migracji](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Firma Contoso używa usługi Azure Migrate do oceny swoich maszyn wirtualnych VMware. Usługa Azure Migrate ocenia przydatność maszyn do migracji. Dzięki tej usłudze można oszacować wymagany rozmiar i koszt działania na platformie Azure. | [Azure Migrate](https://azure.microsoft.com/pricing/details/azure-migrate) jest dostępna bez dodatkowych opłat, jednak opłaty mogą być naliczane w zależności od narzędzi (pierwszej lub niezależnego dostawcy oprogramowania), które będą używane do oceny i migracji.
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Baza danych opiera się na aparacie serwera MySQL typu open-source. Zapewnia ona w pełni zarządzaną, gotową do użytku korporacyjną bazę danych MySQL do tworzenia i wdrażania aplikacji. | Dowiedz się więcej o Azure Database for MySQL [cenach](https://azure.microsoft.com/pricing/details/mysql) i skalowalności.

## <a name="prerequisites"></a>Wymagania wstępne

W tym scenariuszu firma Contoso potrzebuje następujących elementów.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial). <br><br> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje. <br><br> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora. <br><br> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Infrastruktura platformy Azure wymagana do migracji](./contoso-migration-infrastructure.md).
**Serwery lokalne** | Lokalny serwer vCenter powinien mieć uruchomioną wersję 5,5, 6,0, 6,5 lub 6,7. <br><br> Host ESXi z systemem w wersji 5,5, 6,0, 6,5 lub 6,7. <br><br> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.
**Lokalne maszyny wirtualne** | [Przejrzyj maszyny z systemem Linux](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), które zostały zatwierdzone do działania na platformie Azure.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Administratorzy firmy Contoso przeprowadzają migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Przygotowywanie platformy Azure dla Azure Migrate: Migracja serwera.** Dodają narzędzie migracji serwera do projektu usługi Azure Migrate.
> - **Krok 2: Przygotowanie lokalnego programu VMware dla Azure Migrate: Migracja serwera.** Przygotowuje konta do odnajdywania maszyn wirtualnych i przygotowuje się do nawiązania połączenia z maszyną wirtualną platformy Azure po migracji.
> - **Krok 3. replikowanie maszyn wirtualnych.** Konfigurują replikację i rozpoczynają replikowanie maszyn wirtualnych w magazynie platformy Azure.
> - **Krok 4. Migrowanie maszyny wirtualnej aplikacji przy użyciu Azure Migrate: Migracja serwera.** Przeprowadza migrację testową, aby upewnić się, że wszystko działa, a następnie przeprowadzić pełną migrację, aby przenieść maszynę wirtualną do platformy Azure.
> - **Krok 5. Migrowanie bazy danych.** Umożliwiają one Konfigurowanie migracji przy użyciu Azure Database Migration Service (DMS).

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 1. Przygotowywanie platformy Azure dla Azure Migrate: Narzędzia migracji serwera

Oto składniki platformy Azure, których firma Contoso potrzebuje do zmigrowania maszyn wirtualnych na platformę Azure:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne platformy Azure, gdy są one tworzone podczas migracji.
- Azure Migrate: Narzędzie do migracji serwera (komórki jajowe), obsługiwane i skonfigurowane.

Składniki te są konfigurowane w następujący sposób:

1. Konfigurowanie sieci — firma Contoso ma już skonfigurowaną sieć, która może być dla Azure Migrate: Migracja serwera podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md)

2. Inicjowanie obsługi administracyjnej Azure Migrate: Narzędzia migracji serwera.

    - Z Azure Migrate Pobierz obraz komórki jajowe i zaimportuj go do programu VMWare.

        ![Pobierz plik komórki jajowe](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    - Uruchom zaimportowany obraz i skonfiguruj narzędzie, w tym następujące kroki:

      - Skonfiguruj wymagania wstępne.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

      - Wskaż narzędzie subskrypcję platformy Azure.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-register-azure.png)

      - Ustaw poświadczenia programu VMWare vCenter.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

      - Dodaj wszystkie poświadczenia oparte na systemie Linux do odnajdowania.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-credentials.png)

3. Po skonfigurowaniu narzędzia mogą wyliczyć wszystkie maszyny wirtualne. Po zakończeniu zobaczysz je w narzędziu Azure Migrate na platformie Azure.

**Potrzebujesz dodatkowej pomocy?**

[Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate) konfigurowaniu Azure Migrate: Narzędzia migracji serwera.

## <a name="step-2-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Krok 2: Przygotowanie lokalnego programu VMware dla Azure Migrate: Migracja serwera

Po przeprowadzeniu migracji na platformę Azure firma Contoso chce mieć możliwość nawiązania połączenia z replikowanymi maszynami wirtualnymi na platformie Azure. W tym celu administratorzy firmy Contoso muszą wykonać kilka czynności:

- Aby można było uzyskać dostęp do maszyny wirtualnej platformy Azure, Włącz protokół SSH na lokalnej maszynie wirtualnej z systemem Linux przed migracją. W przypadku Ubuntu można to zrobić za pomocą następującego polecenia: `sudo apt-get ssh install -y` .

- Po przeprowadzeniu migracji można sprawdzić **diagnostykę rozruchu** , aby wyświetlić zrzut ekranu maszyny wirtualnej.

- Jeśli to nie zadziała, muszą upewnić się, że maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

- Zainstaluj [agenta platformy Azure dla systemu Linux](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux).

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) przygotowywaniu maszyn wirtualnych do migracji.

## <a name="step-3-replicate-vm"></a>Krok 3. replikowanie maszyny wirtualnej

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

Po ukończeniu odnajdywania można rozpocząć replikację maszyny wirtualnej aplikacji na platformę Azure.

1. Na **serwerach**Azure Migrate project > **Azure Migrate: Migracja serwera**, kliknij przycisk **replikacja**.

    ![Replikowanie maszyn wirtualnych](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. W obszarze **Replikacja** > **Ustawienia źródła** > **Czy maszyny są zwirtualizowane** wybierz pozycję **Tak, z funkcją VMware vSphere Hypervisor**.

3. W obszarze **Urządzenie lokalne** wybierz nazwę skonfigurowanego urządzenia usługi Azure Migrate > przycisk **OK**.

    ![Ustawienia źródła](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. W obszarze **Maszyny wirtualne** wybierz maszyny wirtualne, które mają być replikowane.
    - Jeśli przeprowadzasz ocenę dla maszyn wirtualnych, możesz zastosować rekomendacje dotyczące rozmiarów maszyn wirtualnych i typów dysków (Premium/standardowy) w wynikach oceny. W tym celu w obszarze **Zaimportować ustawienia migracji z oceny usługi Azure Migrate?** wybierz opcję **Tak**.
    - Jeśli nie uruchomiono oceny lub nie chcesz używać ustawień oceny, wybierz opcję **Nie**.
    - W przypadku wybrania opcji korzystania z oceny wybierz grupę maszyn wirtualnych i nazwę oceny.

    ![Wybieranie oceny](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. W obszarze **Maszyny wirtualne** wyszukaj potrzebne maszyny wirtualne i sprawdź każdą maszynę wirtualną, którą chcesz migrować. Następnie kliknij przycisk **Dalej: ustawienia docelowe**.

6. W obszarze **Ustawienia elementu docelowego** wybierz subskrypcję i docelowy region migracji, a następnie określ grupę zasobów, w której będą znajdować się maszyny wirtualne platformy Azure po migracji. W obszarze **Sieć wirtualna** wybierz sieć wirtualną/podsieć platformy Azure, do której zostaną dołączone maszyny wirtualne platformy Azure po migracji.

7. W **korzyść użycia hybrydowego platformy Azure**wybierz następujące opcje:

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie kliknij przycisk **Dalej**.

8. W obszarze **Obliczenia** sprawdź nazwę, rozmiar, typ dysku systemu operacyjnego i zestaw dostępności maszyny wirtualnej. Maszyny wirtualne muszą być zgodne z [wymaganiami platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Rozmiar maszyny wirtualnej:** Jeśli używasz zaleceń dotyczących oceny, lista rozwijana rozmiaru maszyny wirtualnej będzie zawierać zalecany rozmiar. W przeciwnym razie usługa Azure Migrate wybierze rozmiar na podstawie najbliższego dopasowania w subskrypcji platformy Azure. Alternatywnie możesz wybrać rozmiar ręczny w obszarze **rozmiaru maszyny wirtualnej platformy Azure**.
    - **Dysk systemu operacyjnego:** Określ dysk systemu operacyjnego (Boot) dla maszyny wirtualnej. Dysk systemu operacyjnego to dysk, na którym jest zainstalowany program ładujący i instalator systemu operacyjnego.
    - **Zestaw dostępności:** Jeśli maszyna wirtualna powinna znajdować się w zestawie dostępności platformy Azure po migracji, określ zestaw. Zestaw musi znajdować się w docelowej grupie zasobów określonej dla migracji.

9. W obszarze **Dyski** określ, czy dyski maszyn wirtualnych mają być replikowane na platformę Azure, a następnie wybierz typ dysku (standardowe dyski SSD/dyski twarde lub dyski zarządzane w warstwie Premium) na platformie Azure. Następnie kliknij przycisk **Dalej**.
    - Dyski można wykluczyć z replikacji.
    - Jeśli wykluczysz dyski, nie będą one znajdować się na maszynie wirtualnej platformy Azure po migracji.

10. W obszarze **Przegląd i rozpoczynanie replikacji** sprawdź ustawienia, a następnie kliknij pozycję **Replikuj**, aby uruchomić replikację początkową dla serwerów.

> [!NOTE]
> Ustawienia replikacji można aktualizować w dowolnym momencie przed rozpoczęciem replikacji w obszarze **Zarządzanie**  >  **maszynami replikowanymi**. Ustawień nie można zmienić po rozpoczęciu replikacji.

## <a name="step-4-migrate-the-vm-with-azure-migrate-server-migration"></a>Krok 4. Migrowanie maszyny wirtualnej za pomocą Azure Migrate: Migracja serwera

Administratorzy firmy Contoso uruchamiają szybką migrację testową, a następnie pełną migrację do przeniesienia maszyny wirtualnej sieci Web.

### <a name="run-a-test-migration"></a>Uruchamianie migracji testowej

1. W obszarze serwery **celów migracji**  >  **Servers**  >  **Azure Migrate: Migracja serwera**, kliknij przycisk **Testuj zmigrowane serwery**.

     ![Serwery z przeprowadzoną migracją testową](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Kliknij prawym przyciskiem myszy maszynę wirtualną do przetestowania, a następnie kliknij pozycję **Testuj migrację**.

    ![Testowanie migracji](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. W obszarze **Testowanie migracji** wybierz sieć wirtualną platformy Azure, w której zostanie umieszczona maszyna wirtualna platformy Azure po migracji. Zalecamy użycie sieci wirtualnej nieprodukcyjnej.
4. Zostanie uruchomione zadanie **Testowanie migracji**. Monitoruj zadanie w powiadomieniach portalu.
5. Po zakończeniu migracji sprawdź zmigrowane maszyny wirtualne platformy Azure w obszarze **Maszyny wirtualne** w witrynie Azure Portal. Nazwa maszyny ma sufiks **-Test**.
6. Po zakończeniu testu kliknij prawym przyciskiem myszy maszynę wirtualną platformy Azure w obszarze **Replikowanie maszyn**, a następnie kliknij pozycję **Wyczyść migrację testową**.

    ![Czyszczenie migracji](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vm"></a>Migracja maszyny wirtualnej

Teraz Administratorzy firmy Contoso uruchamiają pełną migrację, aby zakończyć przenoszenie.

1. W Azure Migrate serwery > Project **Servers**  >  **Azure Migrate: Migracja serwera**, kliknij przycisk **replikowanie serwerów**.

    ![Replikowanie serwerów](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. W obszarze **Replikowanie maszyn** kliknij prawym przyciskiem myszy maszynę wirtualną > **Migruj**.
3. W obszarze **Migrowanie**  >  **Zamknij maszyny wirtualne i przeprowadź planowaną migrację bez utraty danych**wybierz pozycję **tak**  >  **OK**.
    - Domyślnie usługa Azure Migrate zamyka lokalną maszynę wirtualną i uruchamia replikację na żądanie, aby zsynchronizować wszystkie zmiany maszyny wirtualnej, które wystąpiły od momentu ostatniej replikacji. Gwarantuje to brak utraty danych.
    - Jeśli nie chcesz zamykać maszyny wirtualnej, wybierz pozycję **nie**.
4. Zostanie uruchomione zadanie migracji maszyny wirtualnej. Śledź zadanie w powiadomieniach platformy Azure.
5. Po zakończeniu zadania możesz wyświetlić maszynę wirtualną i zarządzać nią na stronie **Maszyny wirtualne**.

## <a name="step-5-provision-azure-database-for-mysql"></a>Krok 5. Udostępnianie Azure Database for MySQL

Administratorzy firmy Contoso aprowizują wystąpienie bazy danych MySQL w regionie podstawowym Wschodnie stany USA 2.

1. W witrynie Azure Portal tworzą zasób usługi Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. Dodają nazwę **contosoosticket** dla usługi bazy danych platformy Azure. Dodają bazę danych do grupy zasobów produkcyjnych **ContosoRG** i określają jej poświadczenia.
3. Wersja lokalnej bazy danych MySQL to 5.7, dlatego wybierają tę wersję w celu zachowania zgodności. Używają rozmiarów domyślnych, które spełniają wymagania dotyczące bazy danych.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. W obszarze **Opcje nadmiarowości kopii zapasowej** wybierają pozycję **Geograficznie nadmiarowe**. Ta opcja umożliwia przywrócenie bazy danych w regionie dodatkowym Środkowe stany USA w przypadku wystąpienia awarii. Tę opcję można skonfigurować tylko podczas aprowizowania bazy danych.

     ![Nadmiarowość](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. W obszarze sieci **VNET-PROD-EUS2** > **Punkty końcowe usługi** dodają punkt końcowy usługi (podsieć bazy danych) dla usługi SQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. Po dodaniu podsieci tworzą regułę sieci wirtualnej, która zezwala na dostęp z poziomu podsieci bazy danych w sieci produkcyjnej.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-6-migrate-the-database"></a>Krok 6. Migrowanie bazy danych

Istnieje kilka sposobów przenoszenia bazy danych MySQL. Każdy z nich wymaga utworzenia wystąpienia usługi Azure DB for MySQL dla elementu docelowego. Po utworzeniu można przeprowadzić migrację przy użyciu dwóch ścieżek:

- 6a: Azure Database Migration Service
- 6B: Tworzenie kopii zapasowej i przywracanie bazy danych MySQL Workbench

### <a name="step-6a-migrate-the-database-azure-database-migration-service"></a>Krok 6a: Migrowanie bazy danych (Azure Database Migration Service)

Administratorzy firmy Contoso Migrowanie bazy danych przy użyciu usług Azure Database Migration Services przy użyciu [samouczka migracji krok po kroku](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online). Mogą wykonywać migracje w trybie online, offline i hybrydowym (wersja zapoznawcza) za pomocą programu MySQL 5,6 lub 5,7.

> [!NOTE]
> Program MySQL 8,0 jest obsługiwany w Azure Database for MySQL, ale narzędzie DMS nie obsługuje jeszcze tej wersji.

Podsumowując, należy wykonać następujące czynności:

- Upewnij się, że spełniono wszystkie wymagania wstępne dotyczące migracji:

  - Źródło serwera MySQL musi być zgodne z wersją obsługiwaną przez Azure Database for MySQL. Azure Database for MySQL obsługuje — program MySQL Community Edition, aparat InnoDB i migracja między źródłem i celem z tymi samymi wersjami.
  - Włącz logowanie binarne w pliku my. ini (Windows) lub My. cnf (UNIX). Niewykonanie tej czynności spowoduje wystąpienie `Error in binary logging. Variable binlog_row_image has value 'minimal'. Please change it to 'full. For more information, see https://go.microsoft.com/fwlink/?linkid=873009` błędu w Kreatorze migracji.
  - Użytkownik musi mieć `ReplicationAdmin` rolę.
  - Migruj schematy bazy danych bez kluczy obcych i wyzwalaczy.

- Utwórz sieć wirtualną, która łączy się za pośrednictwem ExpressRoute lub sieci VPN z siecią lokalną.

- Utwórz Azure Database Migration Service z jednostką `Premium` SKU, która jest połączona z siecią wirtualną.

- Upewnij się, że Azure Database Migration Service może uzyskać dostęp do bazy danych MySQL za pośrednictwem sieci wirtualnej. Dzięki temu można upewnić się, że wszystkie porty przychodzące są dozwolone z platformy Azure do bazy danych MySQL na poziomie sieci wirtualnej, sieci VPN i komputera, który hostuje MySQL.

- Uruchom narzędzie Azure Database Migration Service:

  - Utwórz projekt migracji.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-new-project-02.png)

  - Dodaj źródło (lokalna baza danych).

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-source.png)

  - Wybierz element docelowy.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-target.png)

  - Wybierz bazy danych do migracji.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-databases.png)

  - Skonfiguruj ustawienia zaawansowane.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-settings.png)

  - Uruchom replikację i rozwiąż wszelkie błędy.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-monitor.png)

  - Wykonaj ostateczną uruchomienie produkcyjne.
  
    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete.png)

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-complete-02.png)
  
  - Przywróć wszystkie klucze obce i wyzwalacze.

  - Zmodyfikuj aplikacje, aby używały nowej bazy danych.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/migration-dms-cutover-apps.png)

### <a name="step-6b-migrate-the-database-mysql-workbench"></a>Krok 6B: Migrowanie bazy danych (MySQL Workbench)

Administratorzy firmy Contoso migrują bazę danych przy użyciu funkcji tworzenia kopii zapasowych i przywracania za pomocą narzędzi MySQL. Instalują aplikację MySQL Workbench, tworzą kopię zapasową bazy danych z maszyny wirtualnej OSTICKETMYSQL, a następnie przywracają ją na serwer usługi Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalacja aplikacji MySQL Workbench

1. Sprawdzają [wymagania wstępne i pliki do pobrania aplikacji MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).

2. Instalują program MySQL Workbench dla systemu Windows zgodnie [z instrukcjami instalacji](https://dev.mysql.com/doc/workbench/en/wb-installing.html).

3. W programie MySQL Workbench tworzą połączenie usługi MySQL z maszyną OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. Eksportują bazę danych **osticket** do samodzielnego pliku lokalnego.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. Po utworzeniu lokalnej kopii zapasowej bazy danych tworzą połączenie z wystąpieniem usługi Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Teraz mogą zaimportować (przywrócić) bazę danych w wystąpieniu usługi Azure Database for MySQL z utworzonego samodzielnego pliku. Dla wystąpienia zostanie utworzony nowy schemat (osticket).

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

### <a name="connect-the-vm-to-the-database"></a>Łączenie maszyny wirtualnej z bazą danych

W ostatnim kroku procesu migracji Administratorzy firmy Contoso aktualizują parametry połączenia aplikacji w taki sposób, aby wskazywały bazę danych aplikacji działającą na maszynie wirtualnej **OSTICKETMYSQL** .

1. Konfigurują połączenie SSH z maszyną wirtualną **OSTICKETMYSQL** za pomocą programu Putty lub innego klienta SSH. Maszyna wirtualna jest prywatna, a więc nawiązują połączenie przy użyciu prywatnego adresu IP.

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Muszą upewnić się, że maszyna wirtualna **OSTICKETWEB** może komunikować się z maszyną **OSTICKETMYSQL**. Obecnie w konfiguracji jest na stałe zapisany lokalny adres IP 172.16.0.43.

    **Przed aktualizacją:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Po aktualizacji:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Usługa zostanie ponownie uruchomiona za pomocą programu `systemctl restart apache2` .

    ![Ponowne uruchamianie](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Na koniec aktualizują rekordy DNS dla maszyn wirtualnych **OSTICKETWEB** i **OSTICKETMYSQL** na jednym z kontrolerów domeny firmy Contoso.

    ![Aktualizowanie rekordów DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Aktualizowanie rekordów DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) uruchamianiu migracji testowej.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) o migracji maszyn wirtualnych do platformy Azure.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po uruchomieniu aplikacji firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji warstwy aplikacji osTicket działają na maszynach wirtualnych platformy Azure.

Teraz firma Contoso musi wykonać następujące czynności:

- Usunięcie maszyn wirtualnych VMware ze spisu programu vCenter.
- Usunięcie lokalnych maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie wewnętrznej dokumentacji tak, aby wskazywała nowe lokalizacje i adresy IP.
- Przegląd wszystkich zasobów korzystających z lokalnych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Firma Contoso skorzystała z usługi Azure Migrate z mapowaniem zależności do przeprowadzenia oceny maszyny wirtualnej **OSTICKETWEB** pod kątem migracji.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso sprawdza maszynę wirtualną i bazę danych, aby określić problemy z zabezpieczeniami.

- Administratorzy przeglądają sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyny wirtualnej. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Należy rozważyć zabezpieczenie danych na dyskach maszyn wirtualnych przy użyciu szyfrowania dysków i Azure Key Vault.
- Nie skonfigurowano komunikacji między maszyną wirtualną a wystąpieniem bazy danych z użyciem protokołu SSL. Trzeba to zrobić, aby upewnić się, że hakerzy nie mogą zaatakować bazy danych.

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania w zakresie zabezpieczeń dotyczące obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Zapewnienie ciągłości działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii firma Contoso podejmuje następujące działania:

- **Zachowaj bezpieczeństwo danych.** Firma Contoso tworzy kopie zapasowe danych na maszynie wirtualnej aplikacji za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-overview). Nie trzeba konfigurować kopii zapasowej bazy danych. Usługa Azure Database for MySQL automatycznie tworzy kopie zapasowe i magazyny serwerów. Wybrano opcję użycia nadmiarowości geograficznej bazy danych, aby była odporna na awarie i gotowa do produkcji.

- **Zapewnienie ciągłości działania aplikacji.** Firma Contoso replikuje maszyny wirtualne aplikacji w regionie pomocniczym platformy Azure za pomocą usługi Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu zasobów firma Contoso przypisuje tagi platformy Azure zgodnie z decyzjami podjętymi na etapie wdrażania [infrastruktury platformy Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- Nie ma problemów z licencjonowaniem dla wdrożenia serwerów Contoso Ubuntu.
- Firma Contoso będzie używać [Azure Cost Management](https://azure.microsoft.com/services/cost-management) , aby zapewnić, że pozostają w ramach budżetów ustanowionych przez ich lidera.
