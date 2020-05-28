---
title: Hostowanie aplikacji na maszynach wirtualnych platformy Azure za pomocą Azure Migrate
description: Dowiedz się, w jaki sposób firma Contoso rehostuje aplikację lokalną za pomocą dźwigu i przeniesie migrację maszyn lokalnych na platformę Azure przy użyciu usługi Azure Migrate.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 146760046dc82b80e347ca2b71ca2ac5f8c090e0
ms.sourcegitcommit: 6fef15cc3a8af725dc743e19f127513bc58dd257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/27/2020
ms.locfileid: "84023427"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc NSGs agentless -->

# <a name="rehost-an-on-premises-app-on-azure-vms"></a>Ponowne hostowanie aplikacji lokalnej na maszynach wirtualnych platformy Azure

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso ponownie hostuje dwuwarstwową aplikację frontonu .NET systemu Windows działającą na maszynach wirtualnych VMware, migrując maszyny wirtualne aplikacji na platformę Azure.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co jej lokalne systemy i infrastruktura stają się przeciążone.
- **Ograniczanie ryzyka.** Aplikacja SmartHotel360 ma kluczowe znaczenie dla działalności firmy Contoso. Firma chce przenieść aplikację na platformę Azure, eliminując ryzyko.
- **Sunąć.** Firma Contoso nie chce modyfikować aplikacji, ale chce mieć pewność, że jest stabilna.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji:

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie w środowisku VMware. Aplikacja działająca w chmurze będzie miała tak samo krytyczne znaczenie jak w środowisku lokalnym.
- Firma Contoso nie chce inwestować w tę aplikację. Jest ona ważna dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Firma Contoso nie chce zmieniać modelu operacyjnego dla tej aplikacji. Firma chce korzystać z niej w chmurze w taki sam sposób, jak korzysta z niej teraz.
- Firma Contoso nie chce zmieniać żadnych funkcji aplikacji. Zmieni się tylko jej lokalizacja.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które zostaną użyte do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja działa warstwowo na dwóch maszynach wirtualnych (**WEBVM** i **SQLVM**).
- Maszyny wirtualne znajdują się na VMware ESXi hosta **contosohost1.contoso.com** (wersja 6,5).
- Środowisko VMware jest zarządzane przez vCenter Server 6,5 (**vCenter.contoso.com**), uruchomione na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-Datacenter) z lokalnym kontrolerem domeny (**ContosoDC1**).

### <a name="proposed-architecture"></a>Proponowana architektura

- Ponieważ aplikacja jest obciążeniem produkcyjnym, maszyny wirtualne aplikacji na platformie Azure będą znajdowały się w grupie zasobów produkcyjnych ContosoRG.
- Maszyny wirtualne aplikacji zostaną przeniesione do regionu podstawowego platformy Azure (Wschodnie stany USA 2) i umieszczone w sieci produkcyjnej (VNET-PROD-EUS2).
- Maszyna wirtualna frontonu internetowego będzie znajdować się w podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
- Maszyna wirtualna bazy danych będzie znajdować się w podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-rehost-vm/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i programu SQL Server. Następujące zagadnienia pomogły podjąć decyzję o przejściu do programu SQL Server uruchomionego na maszynie wirtualnej IaaS platformy Azure:

- Korzystanie z maszyny wirtualnej platformy Azure z systemem SQL Server wydaje się być najlepszym rozwiązaniem, jeśli firma Contoso wymaga dostosowania systemu operacyjnego i bazy danych, lub jeśli warto umieścić i uruchomić aplikacje innych firm na tej samej maszynie wirtualnej.
- Dzięki programowi Software Assurance firma Contoso może w przyszłości wymienić istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi SQL Database, stosując korzyść użycia hybrydowego platformy Azure dla programu SQL Server. Dzięki temu firma może zaoszczędzić do 30% na wystąpieniu zarządzanym.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

| **Zagadnienie** | **Szczegóły** |
| --- | --- |
| **Zalety** | Obie maszyny wirtualne aplikacji zostaną przeniesione na platformę Azure bez zmian, co oznacza prostą migrację. <br><br> Ponieważ firma Contoso używa metody podnoszenia i przesunięcia dla maszyn wirtualnych aplikacji, nie jest wymagana specjalna konfiguracja ani narzędzia migracji dla bazy danych aplikacji. <br><br> Firma Contoso może skorzystać z inwestycji w program Software Assurance i zastosować korzyść użycia hybrydowego platformy Azure. <br><br> Firma Contoso zachowa pełną kontrolę nad maszynami wirtualnymi aplikacji na platformie Azure. |
| **Wady** | Na maszynach wirtualnych WEBVM i SQLVM działa system Windows Server 2008 R2. System operacyjny jest obsługiwany przez platformę Azure dla określonych ról. [Dowiedz się więcej](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines). <br><br> Warstwy sieci Web i danych aplikacji pozostaną single point of failure. <br><br> SQLVM jest uruchomiona na SQL Server 2008 R2, która nie jest już w ramach podstawowego wsparcia. Jest to jednak obsługiwane w przypadku maszyn wirtualnych platformy Azure. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support). <br><br> Firma Contoso musi kontynuować obsługę aplikacji na maszynach wirtualnych platformy Azure zamiast przechodzenia do usługi zarządzanej, takiej jak Azure App Service i Azure SQL Database. |

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

Firma Contoso będzie migrować maszyny wirtualne frontonu i bazy danych aplikacji do maszyn wirtualnych platformy Azure przy użyciu metody bezagentowej narzędzia migracji serwera Azure Migrate:.

- W pierwszym kroku firma Contoso przygotowuje i konfiguruje składniki platformy Azure dla Azure Migrate: Migracja serwera i przygotowuje lokalną infrastrukturę programu VMware.
- Mają już [infrastrukturę platformy Azure](./contoso-migration-infrastructure.md) , więc firma Contoso musi dodać konfigurację replikacji maszyn wirtualnych za pomocą narzędzia do migracji Azure Migrate: serwera.
- Po przygotowaniu wszystkich elementów firma Contoso może rozpocząć replikację maszyn wirtualnych.
- Po włączeniu i rozpoczęciu replikacji firma Contoso przeprowadzi migrację maszyny wirtualnej przez przetestowanie migracji i w razie jej przełączenia w tryb failover na platformie Azure.

![Proces migracji](./media/contoso-migration-rehost-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Usługi platformy Azure

| **Usługa** | **Opis** | **Koszty** |
| --- | --- | --- |
| [Azure Migrate: Migracja serwera](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm) | Usługa organizuje migrację lokalnych aplikacji i obciążeń oraz wystąpień maszyn wirtualnych AWS/GCP, a także zarządza tym procesem. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure są tworzone i są naliczane opłaty, gdy odbywa się migracja, a maszyny wirtualne działają na platformie Azure. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/azure-migrate) o opłatach i cenach. |

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do realizacji tego scenariusza.

<!-- markdownlint-disable MD033 -->

| **Wymagania** | **Szczegóły** |
| --- | --- |
| **Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje we wcześniejszym artykule z tej serii. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial). <br><br> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje. <br><br> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora. <br><br> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control). |
| **Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure. <br><br> Dowiedz się więcej na temat wymagań [wstępnych](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prerequisites) dotyczących Azure Migrate: Migracja serwera. |
| **Serwery lokalne** | Lokalne serwery vCenter powinny mieć uruchomioną wersję 5,5, 6,0, 6,5 lub 6,7. <br><br> Hosty ESXi powinny działać w wersji 5,5, 6,0, 6,5 lub 6,7. <br><br> Co najmniej jedna maszyna wirtualna VMware powinna być uruchomiona na hoście ESXi. |

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Administratorzy firmy Contoso uruchamiają migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Przygotowywanie platformy Azure dla Azure Migrate: Migracja serwera.** Dodają narzędzie migracji serwera do projektu usługi Azure Migrate.
> - **Krok 2: Przygotowanie lokalnego programu VMware dla Azure Migrate: Migracja serwera.** Przygotowuje konta do odnajdywania maszyn wirtualnych i przygotowuje się do łączenia się z maszynami wirtualnymi platformy Azure po migracji.
> - **Krok 3. replikowanie maszyn wirtualnych.** Konfigurują replikację i rozpoczynają replikowanie maszyn wirtualnych w magazynie platformy Azure.
> - **Krok 4. Migrowanie maszyn wirtualnych przy użyciu Azure Migrate: Migracja serwera.** Przeprowadza migrację testową, aby upewnić się, że wszystko działa, a następnie przeprowadzić pełną migrację, aby przenieść maszyny wirtualne na platformę Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 1. Przygotowywanie platformy Azure dla Azure Migrate: Narzędzia migracji serwera

Oto składniki platformy Azure, których firma Contoso potrzebuje do zmigrowania maszyn wirtualnych na platformę Azure:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne platformy Azure, gdy są one tworzone podczas migracji.
- Azure Migrate: Narzędzie do migracji serwera (komórki jajowe), obsługiwane i skonfigurowane.

Składniki te są konfigurowane w następujący sposób:

1. Konfigurowanie sieci — firma Contoso ma już skonfigurowaną sieć, która może być dla Azure Migrate: Migracja serwera podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md)

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyny wirtualne zostaną zmigrowane do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie głównym Wschodnie stany USA 2.
    - Obie maszyny wirtualne zostaną umieszczone w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych.
    - Maszyna wirtualna frontonu aplikacji (WEBVM) zostanie zmigrowana do podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
    - Maszyna wirtualna bazy danych aplikacji (SQLVM) zostanie zmigrowana do podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.

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

      - Dodaj wszystkie poświadczenia oparte na systemie Windows do odnajdowania.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-credentials.png)

3. Po skonfigurowaniu narzędzia mogą wyliczyć wszystkie maszyny wirtualne. Po zakończeniu zobaczysz je w narzędziu Azure Migrate na platformie Azure.

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się więcej na temat konfigurowania [Azure Migrate: Narzędzia migracji serwera](https://docs.microsoft.com/azure/migrate/migrate-services-overview#azure-migrate-server-migration-tool).
### <a name="prepare-on-premises-vms"></a>Przygotowywanie lokalnych maszyn wirtualnych

Po migracji firma Contoso chce nawiązać połączenie z maszynami wirtualnymi platformy Azure i umożliwić platformie Azure zarządzanie maszynami wirtualnymi. W tym celu administratorzy firmy Contoso wykonują następujące czynności przed migracją:

1. W celu uzyskania dostępu przez Internet:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Upewniają się, że zostały dodane reguły TCP i UDP dla profilu **publicznego**.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.

2. W celu uzyskania dostępu przez sieć VPN lokacja-lokacja:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.
    - Dla systemu Windows Ustaw zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na **OnlineAll**.

3. Zainstaluj agenta platformy Azure.

    - [Agent systemu Windows Azure](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-windows)

4. Inne zagadnienia:

   - W przypadku systemu Windows na maszynie wirtualnej nie ma żadnych oczekujących aktualizacji podczas wyzwalania migracji. W przeciwnym razie nie będzie można zalogować się na maszynie wirtualnej do momentu ukończenia aktualizacji.
   - Po migracji można sprawdzić **diagnostykę rozruchu** , aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli to nie zadziała, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

5. Potrzebujesz dodatkowej pomocy?

   - Dowiedz się więcej o [przygotowywaniu maszyn wirtualnych do migracji](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration).

## <a name="step-2-replicate-the-on-premises-vms"></a>Krok 2. replikowanie lokalnych maszyn wirtualnych

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

Po ukończeniu odnajdywania można rozpocząć replikację maszyn wirtualnych VMware na platformę Azure.

1. Na **serwerach**Azure Migrate project > **Azure Migrate: Migracja serwera**, wybierz opcję **replikacja**.

    ![Replikowanie maszyn wirtualnych](./media/contoso-migration-rehost-vm/select-replicate.png)

2. W obszarze **Replikacja** > **Ustawienia źródła** > **Czy maszyny są zwirtualizowane** wybierz pozycję **Tak, z funkcją VMware vSphere Hypervisor**.

3. W obszarze **Urządzenie lokalne** wybierz nazwę skonfigurowanego urządzenia usługi Azure Migrate > przycisk **OK**.

    ![Ustawienia źródła](./media/contoso-migration-rehost-vm/source-settings.png)

4. W obszarze **Maszyny wirtualne** wybierz maszyny wirtualne, które mają być replikowane.
    - Jeśli przeprowadzasz ocenę dla maszyn wirtualnych, możesz zastosować rekomendacje dotyczące rozmiarów maszyn wirtualnych i typów dysków (Premium/standardowy) w wynikach oceny. W tym celu w obszarze **Zaimportować ustawienia migracji z oceny usługi Azure Migrate?** wybierz opcję **Tak**.
    - Jeśli nie uruchomiono oceny lub nie chcesz używać ustawień oceny, wybierz opcję **Nie**.
    - W przypadku wybrania opcji korzystania z oceny wybierz grupę maszyn wirtualnych i nazwę oceny.

    ![Wybieranie oceny](./media/contoso-migration-rehost-vm/select-assessment.png)

5. W obszarze **Maszyny wirtualne** wyszukaj potrzebne maszyny wirtualne i sprawdź każdą maszynę wirtualną, którą chcesz migrować. Następnie wybierz kolejno pozycje **Dalej: ustawienia docelowe**.

6. W obszarze **Ustawienia elementu docelowego** wybierz subskrypcję i docelowy region migracji, a następnie określ grupę zasobów, w której będą znajdować się maszyny wirtualne platformy Azure po migracji. W obszarze **Sieć wirtualna** wybierz sieć wirtualną/podsieć platformy Azure, do której zostaną dołączone maszyny wirtualne platformy Azure po migracji.

7. W **korzyść użycia hybrydowego platformy Azure**wybierz następujące opcje:

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie wybierz pozycję **Dalej**.
    - Wybierz opcję **Tak**, jeśli masz maszyny z systemem Windows Server, które są objęte aktywnym programem Software Assurance lub subskrypcjami systemu Windows Server, i chcesz zastosować korzyść do migrowanych maszyn. Następnie wybierz pozycję **Dalej**.

8. W obszarze **Obliczenia** sprawdź nazwę, rozmiar, typ dysku systemu operacyjnego i zestaw dostępności maszyny wirtualnej. Maszyny wirtualne muszą być zgodne z [wymaganiami platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Rozmiar maszyny wirtualnej:** Jeśli używasz zaleceń dotyczących oceny, lista rozwijana rozmiaru maszyny wirtualnej będzie zawierać zalecany rozmiar. W przeciwnym razie usługa Azure Migrate wybierze rozmiar na podstawie najbliższego dopasowania w subskrypcji platformy Azure. Alternatywnie możesz wybrać rozmiar ręczny w obszarze **rozmiaru maszyny wirtualnej platformy Azure**.
    - **Dysk systemu operacyjnego:** Określ dysk systemu operacyjnego (Boot) dla maszyny wirtualnej. Dysk systemu operacyjnego to dysk, na którym jest zainstalowany program ładujący i instalator systemu operacyjnego.
    - **Zestaw dostępności:** Jeśli maszyna wirtualna powinna znajdować się w zestawie dostępności platformy Azure po migracji, określ zestaw. Zestaw musi znajdować się w docelowej grupie zasobów określonej dla migracji.

9. W obszarze **Dyski** określ, czy dyski maszyn wirtualnych mają być replikowane na platformę Azure, a następnie wybierz typ dysku (standardowe dyski SSD/dyski twarde lub dyski zarządzane w warstwie Premium) na platformie Azure. Następnie wybierz pozycję **Dalej**.
    - Dyski można wykluczyć z replikacji.
    - Jeśli wykluczysz dyski, nie będą one znajdować się na maszynie wirtualnej platformy Azure po migracji.

10. W obszarze **Przegląd i uruchamianie replikacji**Sprawdź ustawienia, a następnie wybierz pozycję **Replikuj** , aby rozpocząć replikację początkową dla serwerów.

> [!NOTE]
> Ustawienia replikacji można aktualizować w dowolnym momencie przed rozpoczęciem replikacji w obszarze **Zarządzanie**  >  **maszynami replikowanymi**. Ustawień nie można zmienić po rozpoczęciu replikacji.

## <a name="step-3-migrate-the-vms"></a>Krok 3. Migrowanie maszyn wirtualnych

Administratorzy firmy Contoso uruchamiają szybką migrację testową, a następnie pełną migrację do migracji maszyn wirtualnych.

### <a name="run-a-test-migration"></a>Uruchamianie migracji testowej

1. W obszarze serwery **celów migracji**  >  **Servers**  >  **Azure Migrate: Migracja serwera**wybierz kolejno pozycje **Testuj zmigrowane serwery**.

     ![Serwery z przeprowadzoną migracją testową](./media/contoso-migration-rehost-vm/test-migrated-servers.png)

2. Kliknij prawym przyciskiem myszy maszynę wirtualną do przetestowania, a następnie wybierz pozycję **Testuj migrację**.

    ![Testowanie migracji](./media/contoso-migration-rehost-vm/test-migrate.png)

3. W obszarze **Testowanie migracji** wybierz sieć wirtualną platformy Azure, w której zostanie umieszczona maszyna wirtualna platformy Azure po migracji. Zalecamy użycie sieci wirtualnej nieprodukcyjnej.
4. Zostanie uruchomione zadanie **Testowanie migracji**. Monitoruj zadanie w powiadomieniach portalu.
5. Po zakończeniu migracji sprawdź zmigrowane maszyny wirtualne platformy Azure w obszarze **Maszyny wirtualne** w witrynie Azure Portal. Nazwa maszyny ma sufiks **-Test**.
6. Po zakończeniu testu kliknij prawym przyciskiem myszy maszynę wirtualną platformy Azure w obszarze **replikowanie maszyn**, a następnie wybierz polecenie **Oczyść test migracja**.

    ![Czyszczenie migracji](./media/contoso-migration-rehost-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrowanie maszyn wirtualnych

Teraz Administratorzy firmy Contoso uruchamiają pełną migrację.

1. W Azure Migrate serwery > Project **Servers**  >  **Azure Migrate: Migracja serwera**, a następnie wybierz opcję **replikowanie serwerów**.

    ![Replikowanie serwerów](./media/contoso-migration-rehost-vm/replicating-servers.png)

2. W obszarze **Replikowanie maszyn** kliknij prawym przyciskiem myszy maszynę wirtualną > **Migruj**.
3. W obszarze **Migrowanie**  >  **Zamknij maszyny wirtualne i przeprowadź planowaną migrację bez utraty danych**wybierz pozycję **tak**  >  **OK**.
    - Domyślnie usługa Azure Migrate zamyka lokalną maszynę wirtualną i uruchamia replikację na żądanie, aby zsynchronizować wszystkie zmiany maszyny wirtualnej, które wystąpiły od momentu ostatniej replikacji. Gwarantuje to brak utraty danych.
    - Jeśli nie chcesz zamykać maszyny wirtualnej, wybierz pozycję **nie**.
4. Zostanie uruchomione zadanie migracji maszyny wirtualnej. Śledź zadanie w powiadomieniach platformy Azure.
5. Po zakończeniu zadania możesz wyświetlić maszynę wirtualną i zarządzać nią na stronie **Maszyny wirtualne**.

**Potrzebujesz dodatkowej pomocy?**

- Dowiedz się więcej o [uruchamianiu migracji testowej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration).
- Dowiedz się więcej o [migrowaniu maszyn wirtualnych na platformę Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms).

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji warstwy aplikacji SmartHotel360 działają na maszynach wirtualnych platformy Azure.

Teraz firma Contoso musi wykonać następujące kroki dotyczące czyszczenia:

- Po zakończeniu migracji zatrzymać replikację.
- Usunąć maszynę WEBVM ze spisu programu vCenter.
- Usunąć maszynę SQLVM ze spisu programu vCenter.
- Usunąć maszyny WEBVM i SQLVM z lokalnych zadań tworzenia kopii zapasowej.
- Zaktualizować dokumentację wewnętrzną, aby była wyświetlana nowa lokalizacja i adresy IP maszyn wirtualnych.
- Przejrzeć wszystkie zasoby korzystające z tych maszyn wirtualnych i zaktualizować wszelkie ustawienia lub dokumenty, aby odzwierciedlały nową konfigurację.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po uruchomieniu aplikacji firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć ją na platformie Azure.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso sprawdza maszyny wirtualne platformy Azure, aby określić problemy z zabezpieczeniami.

- Aby kontrolować dostęp, zespół przegląda sieciowe grupy zabezpieczeń maszyn wirtualnych. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Zespół rozważa również zabezpieczenie danych na dysku przy użyciu usług Azure Disk Encryption i Key Vault.

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania w zakresie zabezpieczeń dotyczące obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Ciągłość działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Zachowaj bezpieczeństwo danych: Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych za pomocą [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).
- Przechowuj aplikacje i uruchamiaj je: contoso [replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Firma Contoso ma istniejące licencje dla swoich maszyn wirtualnych i zastosuje korzyść użycia hybrydowego platformy Azure. Firma Contoso przekonwertuje istniejące maszyny wirtualne platformy Azure, aby skorzystać z tych cen.
- Firma Contoso umożliwi [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview) monitorowania zasobów platformy Azure i zarządzania nimi.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przehostuje aplikację SmartHotel360 na platformie Azure przez Migrowanie maszyn wirtualnych aplikacji do maszyn wirtualnych platformy Azure przy użyciu narzędzia do migracji Azure Migrate: serwera.
