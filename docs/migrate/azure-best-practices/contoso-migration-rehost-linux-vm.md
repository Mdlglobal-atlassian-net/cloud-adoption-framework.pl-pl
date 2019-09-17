---
title: Ponowne hostowanie aplikacji lokalnej dla systemu Linux na maszynach wirtualnych platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso przeprowadza ponowne hostowanie lokalnej aplikacji dla systemu Linux przez migrację na maszyny wirtualne platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: a2186172248dcaf3006fc7fe0d55fa8174910c6a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025015"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms"></a>Ponowne hostowanie aplikacji lokalnej dla systemu Linux na maszynach wirtualnych platformy Azure

W tym artykule pokazano, jak fikcyjna firma Contoso przeprowadza ponowne hostowanie dwuwarstwowej aplikacji opartej na stosie LAMP (Linux, Apache, MySQL, PHP), korzystając z maszyn wirtualnych platformy Azure w modelu „infrastruktura jako usługa” (IaaS).

Używana w tym przykładzie aplikacja do obsługi pomocy technicznej, osTicket, jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co lokalne systemy i infrastruktura stają się przeciążone.
- **Ograniczanie ryzyka.** Aplikacja do obsługi pomocy technicznej ma kluczowe znaczenie dla działalności firmy Contoso. Firma Contoso chce przenieść ją na platformę Azure, eliminując ryzyko.
- **Rozszerzenie.** Firma Contoso nie chce teraz zmieniać używanej aplikacji. Po prostu chce mieć pewność, że aplikacja jest stabilna.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury w firmie Contoso określił cele migracji, zgodnie z którymi należy wybrać najlepszą metodę migracji:

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie, gdy działa w lokalnym środowisku programu VMware. Aplikacja działająca w chmurze będzie miała tak samo krytyczne znaczenie jak w środowisku lokalnym.
- Firma Contoso nie chce inwestować w tę aplikację. Jest ona ważna dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Firma Contoso nie chce zmieniać modelu operacyjnego dla tej aplikacji. Chce korzystać z aplikacji w chmurze w taki sam sposób, jak korzysta z niej teraz.
- Firma Contoso nie chce zmieniać funkcjonalności aplikacji. Zmieni się tylko jej lokalizacja.
- Firma Contoso przeprowadziła już kilka procesów migracji aplikacji dla systemu Windows, a teraz chce poznać sposób korzystania z infrastruktury platformy Azure z systemem Linux.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które zostaną użyte do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja OSTicket działa na dwóch maszynach wirtualnych (**OSTICKETWEB** i **OSTICKETMYSQL**).
- Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (**contoso-datacenter**) i lokalny kontroler domeny (**contosodc1**).

### <a name="proposed-architecture"></a>Proponowana architektura

- Ponieważ aplikacja jest obciążeniem produkcyjnym, maszyny wirtualne na platformie Azure będą znajdowały się w grupie zasobów produkcyjnych **ContosoRG**.
- Maszyny wirtualne zostaną przeniesione do regionu podstawowego (Wschodnie stany USA 2) i umieszczone w sieci produkcyjnej (VNET-PROD-EUS2):
  - Internetowa maszyna wirtualna zostanie umieszczona w podsieci frontonu (PROD-FE-EUS2).
  - Maszyna wirtualna bazy danych zostanie umieszczona w podsieci bazy danych (PROD-DB-EUS2).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Obie maszyny wirtualne aplikacji zostaną przeniesione na platformę Azure bez zmian, co oznacza prostą migrację.<br/><br/> Ponieważ firma Contoso zastosuje metodę „lift and shift” w przypadku obu maszyn wirtualnych aplikacji, nie będą potrzebne żadne specjalne narzędzia do migracji i konfiguracji bazy danych aplikacji.<br/><br/> Firma Contoso zachowa pełną kontrolę nad maszynami wirtualnymi aplikacji na platformie Azure. <br/><br/> Maszyny wirtualne aplikacji mają system Ubuntu 16.04-TLS, który jest zalecaną dystrybucją systemu Linux. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros).
**Wady** | Warstwa internetowa i warstwa danych aplikacji wciąż będą stanowiły pojedynczy punkt awarii. <br/><br/> Firma Contoso nadal będzie musiała obsługiwać aplikację na maszynach wirtualnych na platformie Azure, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service czy Azure Database for MySQL.<br/><br/> Firma Contoso ma świadomość, że ze względu na zastosowanie prostej metody „lift and shift” do migracji maszyn wirtualnych nie będzie mogła skorzystać ze wszystkich funkcji oferowanych przez usługę [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) (takich jak wbudowana wysoka dostępność, przewidywalna wydajność, proste skalowanie, automatyczna kopia zapasowa i wbudowane zabezpieczenia).

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi migrację w następujący sposób:

- W pierwszej kolejności firma Contoso przygotowuje i konfiguruje składniki platformy Azure na potrzeby migracji serwera usługi Azure Migrate oraz przygotowuje lokalną infrastrukturę VMware.
- Firma Contoso ma już [infrastrukturę platformy Azure](./contoso-migration-infrastructure.md), więc musi dodać konfigurację replikacji maszyn wirtualnych za pomocą narzędzia migracji serwera w usłudze Azure Migrate. 
- Po przygotowaniu wszystkich elementów firma Contoso może rozpocząć replikację maszyn wirtualnych.
- Po włączeniu i uruchomieniu replikacji firma Contoso przeprowadzi migrację maszyny wirtualnej przez przełączenie jej do trybu failover na platformę Azure.

![Proces migracji](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Usługi Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Migracja serwera usługi Azure Migrate](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | Usługa organizuje migrację lokalnych aplikacji i obciążeń oraz wystąpień maszyn wirtualnych AWS/GCP, a także zarządza tym procesem. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure zostaną utworzone w momencie przejścia w tryb failover i wówczas będą naliczane opłaty. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/azure-migrate/) o opłatach i cenach.


## <a name="prerequisites"></a>Wymagania wstępne

W tym scenariuszu firma Contoso potrzebuje następujących elementów.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje na początku tej serii artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** |  [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.<br/><br/> Dowiedz się więcej na temat określonych [wymagań wstępnych](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) dotyczących migracji serwera usługi Azure Migrate.
**Serwery lokalne** | Lokalny serwer vCenter w wersji 5.5, 6.0 lub 6.5<br/><br/> Host ESXi w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.
**Lokalne maszyny wirtualne** | [Przejrzyj maszyny z systemem Linux](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), które zostały zatwierdzone do działania na platformie Azure.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Przygotowywanie platformy Azure do migracji serwera usługi Azure Migrate.** Dodają narzędzie migracji serwera do projektu usługi Azure Migrate. 
> - **Krok 2. Przygotowywanie lokalnego programu VMware do migracji serwera usługi Azure Migrate.** Przygotowują konta do użycia na potrzeby odnajdowania maszyn wirtualnych oraz przygotowują się do połączenia z maszynami wirtualnymi platformy Azure po przejściu w tryb failover.
> - **Krok 3. Replikowanie maszyn wirtualnych.** Konfigurują replikację i rozpoczynają replikowanie maszyn wirtualnych w magazynie platformy Azure.
> - **Krok 4. Migrowanie maszyn wirtualnych przy użyciu procesu migracji serwera usługi Azure Migrate.** Przeprowadzają próbne przejście do trybu failover, aby sprawdzić, czy wszystko działa prawidłowo, a następnie przeprowadzają pełne przejście do trybu failover, aby zmigorwać maszyny wirtualne na platformę Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 1: Przygotowywanie platformy Azure do użycia narzędzia migracji serwera usługi Azure Migrate

Oto składniki platformy Azure, których firma Contoso potrzebuje do zmigrowania maszyn wirtualnych na platformę Azure:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne platformy Azure, gdy zostaną utworzone podczas przełączenia w tryb failover.
- Aprowizowane narzędzie do migracji serwera usługi Azure Migrate Server. 

Składniki te są konfigurowane w następujący sposób:

1. Konfigurowanie sieci — firma Contoso ma już sieć, której można używać w przypadku migracji serwera usługi Azure Migrate podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md)

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyny wirtualne zostaną zmigrowane do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie głównym Wschodnie stany USA 2.
    - Obie maszyny wirtualne zostaną umieszczone w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych.
    - Maszyna wirtualna frontonu aplikacji (WEBVM) zostanie zmigrowana do podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
    - Maszyna wirtualna bazy danych aplikacji (SQLVM) zostanie zmigrowana do podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.


2. Aprowizowanie narzędzia migracji serwera usługi Azure Migrate — po utworzeniu sieci i konta magazynu administratorzy tworzą magazyn usług Recovery Services (ContosoMigrationVault), który umieszczają w grupie zasobów ContosoFailoverRG w regionie podstawowym Wschodnie stany USA 2.

    ![Narzędzie migracji serwera usługi Azure Migrate](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**Potrzebujesz dalszej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/) o konfigurowaniu narzędzia migracji serwera usługi Azure Migrate. 


### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po przełączeniu do trybu failover na platformie Azure firma Contoso chce mieć możliwość nawiązania połączenia z replikowanymi maszynami wirtualnymi na platformie Azure. W tym celu administratorzy firmy Contoso muszą wykonać kilka czynności:

- Aby mieć dostęp do maszyn wirtualnych platformy Azure za pośrednictwem Internetu, muszą włączyć protokół SSH na lokalnych maszynach wirtualnych systemu Linux przed migracją. W przypadku systemu Ubuntu można to zrobić za pomocą następującego polecenia: **Sudo apt-get ssh install -y**.
- Po rozpoczęciu migracji (przełączeniu do trybu failover) mogą sprawdzić **diagnostykę rozruchu**, aby wyświetlić zrzut ekranu maszyny wirtualnej.
- Jeśli to nie zadziała, muszą upewnić się, że maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potrzebujesz dalszej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) na temat przygotowywania maszyn wirtualnych do migracji

## <a name="step-3-replicate-the-on-premises-vms"></a>Krok 3: replikowanie lokalnych maszyn wirtualnych


Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

Po ukończeniu odnajdywania można rozpocząć replikację maszyn wirtualnych VMware na platformę Azure.

1. W projekcie usługi Azure Migrate wybierz pozycję > **Serwery**, **Azure Migrate: Migracja serwera** i kliknij pozycję **Replikuj**.

    ![Replikowanie maszyn wirtualnych](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. W obszarze **Replikacja** > **Ustawienia źródła** > **Czy maszyny są zwirtualizowane** wybierz pozycję **Tak, z funkcją VMware vSphere Hypervisor**.
3. W obszarze **Urządzenie lokalne** wybierz nazwę skonfigurowanego urządzenia usługi Azure Migrate > przycisk **OK**. 

    ![Ustawienia źródła](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. W obszarze **Maszyny wirtualne** wybierz maszyny wirtualne, które mają być replikowane.
    - Jeśli przeprowadzasz ocenę dla maszyn wirtualnych, możesz zastosować rekomendacje dotyczące rozmiarów maszyn wirtualnych i typów dysków (Premium/standardowy) w wynikach oceny. W tym celu w obszarze **Zaimportować ustawienia migracji z oceny usługi Azure Migrate?** wybierz opcję **Tak**.
    - Jeśli nie uruchomiono oceny lub nie chcesz używać ustawień oceny, wybierz opcję **Nie**.
    - W przypadku wybrania opcji korzystania z oceny wybierz grupę maszyn wirtualnych i nazwę oceny.

    ![Wybieranie oceny](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. W obszarze **Maszyny wirtualne** wyszukaj potrzebne maszyny wirtualne i sprawdź każdą maszynę wirtualną, którą chcesz migrować. Następnie kliknij pozycję **Dalej: Ustawienia elementu docelowego**.


6. W obszarze **Ustawienia elementu docelowego** wybierz subskrypcję i docelowy region migracji, a następnie określ grupę zasobów, w której będą znajdować się maszyny wirtualne platformy Azure po migracji. W obszarze **Sieć wirtualna** wybierz sieć wirtualną/podsieć platformy Azure, do której zostaną dołączone maszyny wirtualne platformy Azure po migracji.
7. W obszarze **Korzyść użycia hybrydowego platformy Azure**:

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie kliknij przycisk **Next** (Dalej).
    - Wybierz opcję **Tak**, jeśli masz maszyny z systemem Windows Server, które są objęte aktywnym programem Software Assurance lub subskrypcjami systemu Windows Server, i chcesz zastosować korzyść do migrowanych maszyn. Następnie kliknij przycisk **Next** (Dalej).


8. W obszarze **Obliczenia** sprawdź nazwę, rozmiar, typ dysku systemu operacyjnego i zestaw dostępności maszyny wirtualnej. Maszyny wirtualne muszą być zgodne z [wymaganiami platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#agentless-migration-vmware-vm-requirements).

    - **Rozmiar maszyny wirtualnej**: jeśli używasz rekomendacji dotyczących oceny, lista rozwijana rozmiarów maszyny wirtualnej będzie zawierać zalecany rozmiar. W przeciwnym razie usługa Azure Migrate wybierze rozmiar na podstawie najbliższego dopasowania w subskrypcji platformy Azure. Alternatywnie możesz wybrać rozmiar ręczny w obszarze **rozmiaru maszyny wirtualnej platformy Azure**. 
    - **Dysk systemu operacyjnego**: określ dysk systemu operacyjnego (rozruchowy) dla maszyny wirtualnej. Dysk systemu operacyjnego to dysk, na którym jest zainstalowany program ładujący i instalator systemu operacyjnego. 
    - **Zestaw dostępności**: jeśli maszyna wirtualna powinna znajdować się w zestawie dostępności platformy Azure po migracji, określ ten zestaw. Zestaw musi znajdować się w docelowej grupie zasobów określonej dla migracji.

9. W obszarze **Dyski** określ, czy dyski maszyn wirtualnych mają być replikowane na platformę Azure, a następnie wybierz typ dysku (standardowe dyski SSD/dyski twarde lub dyski zarządzane w warstwie Premium) na platformie Azure. Następnie kliknij przycisk **Next** (Dalej).
    - Dyski można wykluczyć z replikacji.
    - Jeśli wykluczysz dyski, nie będą one znajdować się na maszynie wirtualnej platformy Azure po migracji. 


10. W obszarze **Przegląd i rozpoczynanie replikacji** sprawdź ustawienia, a następnie kliknij pozycję **Replikuj**, aby uruchomić replikację początkową dla serwerów.

> [!NOTE]
> Ustawienia replikacji możesz zaktualizować w dowolnym momencie przed rozpoczęciem replikacji w obszarze **Zarządzanie** > **Replikowanie maszyn**. Ustawień nie można zmienić po rozpoczęciu replikacji.



## <a name="step-4-migrate-the-vms"></a>Krok 4: migrowanie maszyn wirtualnych

Administratorzy firmy Contoso uruchamiają szybki test przejścia do trybu failover, a następnie pełne przełączenie w tryb failover, aby zmigrować maszyny wirtualne.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

1. W obszarze **Cele migracji** > **Serwery** > **Azure Migrate: migracja serwera** kliknij pozycję **Przeprowadzono migrację testową serwerów**.

     ![Serwery z przeprowadzoną migracją testową](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Kliknij prawym przyciskiem myszy maszynę wirtualną do przetestowania, a następnie kliknij pozycję **Testuj migrację**.

    ![Testowanie migracji](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. W obszarze **Testowanie migracji** wybierz sieć wirtualną platformy Azure, w której zostanie umieszczona maszyna wirtualna platformy Azure po migracji. Zalecamy użycie sieci wirtualnej nieprodukcyjnej.
4. Zostanie uruchomione zadanie **Testowanie migracji**. Monitoruj zadanie w powiadomieniach portalu.
5. Po zakończeniu migracji sprawdź zmigrowane maszyny wirtualne platformy Azure w obszarze **Maszyny wirtualne** w witrynie Azure Portal. Nazwa maszyny ma sufiks **-Test**.
6. Po zakończeniu testu kliknij prawym przyciskiem myszy maszynę wirtualną platformy Azure w obszarze **Replikowanie maszyn**, a następnie kliknij pozycję **Wyczyść migrację testową**.

    ![Czyszczenie migracji](./media/contoso-migration-rehost-linux-vm/clean-up.png)


### <a name="migrate-the-vms"></a>Migrowanie maszyn wirtualnych

Teraz administratorzy firmy Contoso uruchamiają pełne przejście do trybu failover w celu ukończenia migracji.

1. W projekcie usługi Azure Migrate wybierz pozycję > **Serwery** > **Azure Migrate: migracja serwera** i kliknij pozycję **Replikowanie serwerów**.

    ![Replikowanie serwerów](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. W obszarze **Replikowanie maszyn** kliknij prawym przyciskiem myszy maszynę wirtualną > **Migruj**.
3. W obszarze **Migrowanie** > **Zamknij maszyny wirtualne i przeprowadź planowaną migrację bez utraty danych** wybierz pozycję **Tak** > **OK**.
    - Domyślnie usługa Azure Migrate zamyka lokalną maszynę wirtualną i uruchamia replikację na żądanie, aby zsynchronizować wszystkie zmiany maszyny wirtualnej, które wystąpiły od momentu ostatniej replikacji. Gwarantuje to brak utraty danych.
    - Jeśli nie chcesz zamykać maszyny wirtualnej, wybierz pozycję **Nie**
4. Zostanie uruchomione zadanie migracji maszyny wirtualnej. Śledź zadanie w powiadomieniach platformy Azure.
5. Po zakończeniu zadania możesz wyświetlić maszynę wirtualną i zarządzać nią na stronie **Maszyny wirtualne**.



### <a name="connect-the-vm-to-the-database"></a>Łączenie maszyny wirtualnej z bazą danych

W ostatnim kroku procesu migracji administratorzy firmy Contoso zaktualizują parametry połączenia aplikacji tak, aby wskazywały bazę danych aplikacji działającą na maszynie wirtualnej **OSTICKETMYSQL**.

1. Konfigurują połączenie SSH z maszyną wirtualną **OSTICKETMYSQL** za pomocą programu Putty lub innego klienta SSH. Maszyna wirtualna jest prywatna, a więc nawiązują połączenie przy użyciu prywatnego adresu IP.

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Muszą upewnić się, że maszyna wirtualna **OSTICKETWEB** może komunikować się z maszyną **OSTICKETMYSQL**. Obecnie w konfiguracji jest na stałe zapisany lokalny adres IP 172.16.0.43.

    **Przed aktualizacją:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Po aktualizacji:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Ponownie uruchamiają usługę za pomocą polecenia **systemctl restart apache2**.

    ![Ponowne uruchamianie](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Na koniec aktualizują rekordy DNS dla maszyn wirtualnych **OSTICKETWEB** i **OSTICKETMYSQL** na jednym z kontrolerów domeny firmy Contoso.

    ![Aktualizowanie rekordów DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Aktualizowanie rekordów DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) o próbnym uruchamianiu trybu failover.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) o migracji maszyn wirtualnych do platformy Azure. 

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji warstwy aplikacji osTicket działają na maszynach wirtualnych platformy Azure.

Teraz firma Contoso musi wykonać następujące czynności w celu wyczyszczenia zasobów:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie lokalnych maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Aktualizacja dokumentacji wewnętrznej w celu wskazania nowej lokalizacji i adresów IP maszyn wirtualnych OSTICKETWEB i OSTICKETMYSQL.
- Przegląd wszystkich zasobów korzystających z tych maszyn wirtualnych i aktualizacja wszelkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Firma Contoso skorzystała z usługi Azure Migrate z mapowaniem zależności do przeprowadzenia oceny maszyn wirtualnych pod kątem migracji. Administratorzy powinni usunąć z maszyny wirtualnej zainstalowanego w tym celu agenta Microsoft Monitoring Agent oraz agenta zależności.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po uruchomieniu aplikacji firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Bezpieczeństwo

Zespół ds. zabezpieczeń w firmie Contoso przeprowadza przegląd maszyn wirtualnych OSTICKETWEB i OSTICKETMYSQL w celu wykrycia ewentualnych problemów z zabezpieczeniami.

- Zespół przegląda sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyn wirtualnych. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Zespół rozważa również zabezpieczenie danych na dyskach maszyn wirtualnych przy użyciu usług Disk Encryption i Azure Key Vault.

[Dowiedz się więcej](https://docs.microsoft.com/azure/security/azure-security-best-practices-vms) na temat rozwiązań zabezpieczeń dla maszyn wirtualnych.

### <a name="bcdr"></a>Zapewnienie ciągłości działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii firma Contoso podejmuje następujące działania:

- **Zapewnienie bezpieczeństwa danych.** Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- **Zapewnienie ciągłości działania aplikacji.** Firma Contoso replikuje maszyny wirtualne aplikacji w regionie pomocniczym platformy Azure za pomocą usługi Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu zasobów firma Contoso przypisuje tagi platformy Azure zdefiniowane na etapie [wrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- Firma Contoso nie ma żadnych problemów z licencjonowaniem serwerów z systemem Ubuntu.
- Firma włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.