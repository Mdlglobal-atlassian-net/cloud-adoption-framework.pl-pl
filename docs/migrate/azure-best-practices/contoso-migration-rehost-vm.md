---
title: Hostowanie aplikacji na maszynach wirtualnych platformy Azure za pomocą Azure Site Recovery
description: Dowiedz się, w jaki sposób firma Contoso rehostuje aplikację lokalną za pomocą dźwigu i przeniesie migrację maszyn lokalnych na platformę Azure przy użyciu usługi Azure Site Recovery.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 8b704c88b2e6a161c49082301df6e6a3d7d77154
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222899"
---
# <a name="rehost-an-on-premises-app-on-azure-vms"></a>Ponowne hostowanie aplikacji lokalnej na maszynach wirtualnych platformy Azure

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso ponownie hostuje dwuwarstwową aplikację frontonu .NET systemu Windows działającą na maszynach wirtualnych VMware, migrując maszyny wirtualne aplikacji na platformę Azure.

Aplikacja SmartHotel360 używana w tym przykładzie jest oferowana jako aplikacja typu open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co jej lokalne systemy i infrastruktura stają się przeciążone.
- **Ograniczanie ryzyka.** Aplikacja SmartHotel360 ma kluczowe znaczenie dla działalności firmy Contoso. Firma chce przenieść aplikację na platformę Azure, eliminując ryzyko.
- **Rozszerzenie.** Firma Contoso nie chce modyfikować aplikacji, ale chce mieć pewność, że jest stabilna.

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
- Maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).

### <a name="proposed-architecture"></a>Proponowana architektura

- Ponieważ aplikacja jest obciążeniem produkcyjnym, maszyny wirtualne aplikacji na platformie Azure będą znajdowały się w grupie zasobów produkcyjnych ContosoRG.
- Maszyny wirtualne aplikacji zostaną przeniesione do regionu podstawowego platformy Azure (Wschodnie stany USA 2) i umieszczone w sieci produkcyjnej (VNET-PROD-EUS2).
- Maszyna wirtualna frontonu internetowego będzie znajdować się w podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
- Maszyna wirtualna bazy danych będzie znajdować się w podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-rehost-vm/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i programu SQL Server. Następujące zagadnienia pomogły podjąć decyzję o przejściu do programu SQL Server uruchomionego na maszynie wirtualnej IaaS platformy Azure:

- Korzystanie z maszyny wirtualnej platformy Azure z programem SQL Server wydaje się być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub bazę danych lub rozważa umieszczenie i uruchamianie na tej samej maszynie wirtualnej aplikacje innych firm.
- Dzięki programowi Software Assurance firma Contoso może w przyszłości wymienić istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi SQL Database, stosując korzyść użycia hybrydowego platformy Azure dla programu SQL Server. Dzięki temu firma może zaoszczędzić do 30% na wystąpieniu zarządzanym.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Obie maszyny wirtualne aplikacji zostaną przeniesione na platformę Azure bez zmian, co oznacza prostą migrację.<br/><br/> Ponieważ firma Contoso używa metody podnoszenia i przesunięcia dla maszyn wirtualnych aplikacji, nie jest wymagana specjalna konfiguracja ani narzędzia migracji dla bazy danych aplikacji.<br/><br/> Firma Contoso może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure.<br/><br/> Firma Contoso zachowa pełną kontrolę nad maszynami wirtualnymi aplikacji na platformie Azure.
**Wady** | Na maszynach wirtualnych WEBVM i SQLVM działa system Windows Server 2008 R2. System operacyjny jest obsługiwany przez platformę Azure dla określonych ról (lipiec 2018). [Dowiedz się więcej](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).<br/><br/> Warstwa internetowa i warstwa danych aplikacji wciąż będą stanowiły pojedynczy punkt awarii.<br/><br/> Maszyna wirtualna SQLVM działa na serwerze SQL Server 2008 R2, który nie jest objęty wsparciem podstawowym. Jest jednak obsługiwany w przypadku maszyn wirtualnych platformy Azure (lipiec 2018). [Dowiedz się więcej](https://support.microsoft.com/help/956893).<br/><br/> Firma Contoso nadal będzie musiała obsługiwać aplikację na maszynach wirtualnych na platformie Azure, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service czy Azure SQL Database.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

Firma Contoso będzie migrować maszyny wirtualne bazy danych i frontonu aplikacji do maszyn wirtualnych platformy Azure za pomocą metody niekorzystającej z agenta narzędzia migracji serwera usługi Azure Migrate.

- W pierwszej kolejności firma Contoso przygotowuje i konfiguruje składniki platformy Azure na potrzeby migracji serwera usługi Azure Migrate oraz przygotowuje lokalną infrastrukturę VMware.
- Firma Contoso ma już [infrastrukturę platformy Azure](./contoso-migration-infrastructure.md), więc musi dodać konfigurację replikacji maszyn wirtualnych za pomocą narzędzia migracji serwera w usłudze Azure Migrate.
- Po przygotowaniu wszystkich elementów firma Contoso może rozpocząć replikację maszyn wirtualnych.
- Po włączeniu i uruchomieniu replikacji firma Contoso przeprowadzi migrację maszyny wirtualnej przez przełączenie jej do trybu failover na platformę Azure.

![Proces migracji](./media/contoso-migration-rehost-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Migracja serwera usługi Azure Migrate](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm) | Usługa organizuje migrację lokalnych aplikacji i obciążeń oraz wystąpień maszyn wirtualnych AWS/GCP, a także zarządza tym procesem. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure zostaną utworzone w momencie przejścia w tryb failover i wówczas będą naliczane opłaty. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/azure-migrate) o opłatach i cenach.

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do realizacji tego scenariusza.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje we wcześniejszym artykule z tej serii. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.<br/><br/> Dowiedz się więcej na temat określonych [wymagań wstępnych](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prerequisites) dotyczących migracji serwera usługi Azure Migrate.
**Serwery lokalne** | Lokalne serwery vCenter w wersji 5.5, 6.0 lub 6.5<br/><br/> Hosty ESXi powinny działać w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna VMware powinna być uruchomiona na hoście ESXi.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Administratorzy firmy Contoso uruchamiają migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Przygotowywanie platformy Azure do Azure Migrate migracji serwera.** Dodają narzędzie migracji serwera do projektu usługi Azure Migrate.
> - **Krok 2: Przygotowanie lokalnej migracji programu VMware do Azure Migrate serwera.** Przygotowują konta do użycia na potrzeby odnajdowania maszyn wirtualnych oraz przygotowują się do połączenia z maszynami wirtualnymi platformy Azure po przejściu w tryb failover.
> - **Krok 3. replikowanie maszyn wirtualnych.** Konfigurują replikację i rozpoczynają replikowanie maszyn wirtualnych w magazynie platformy Azure.
> - **Krok 4. Migrowanie maszyn wirtualnych przy użyciu migracji Azure Migrate Server.** Przeprowadzają próbne przejście do trybu failover, aby sprawdzić, czy wszystko działa prawidłowo, a następnie przeprowadzają pełne przejście do trybu failover, aby zmigorwać maszyny wirtualne na platformę Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 1. Przygotowanie platformy Azure do narzędzia migracji Azure Migrate Server

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

    ![Narzędzie migracji serwera usługi Azure Migrate](./media/contoso-migration-rehost-vm/server-migration-tool.png)

**Potrzebujesz dodatkowej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/migrate) o konfigurowaniu narzędzia migracji serwera usługi Azure Migrate.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po przełączeniu w tryb failover firma Contoso chce nawiązać połączenie z maszynami wirtualnymi na platformie Azure. W tym celu administratorzy firmy Contoso wykonują następujące czynności przed migracją:

1. W celu uzyskania dostępu przez Internet:

    - Przed włączeniem trybu failover włączają protokół RDP na lokalnej maszynie wirtualnej.
    - Upewniają się, że zostały dodane reguły TCP i UDP dla profilu **publicznego**.
    - W obszarze **Zapora systemu Windows** > **Dozwolone aplikacje** sprawdzają, czy protokół RDP jest dozwolony dla wszystkich profilów.

2. W celu uzyskania dostępu przez sieć VPN lokacja-lokacja:

    - Włączają protokół RDP na maszynie lokalnej.
    - W obszarze **Zapora systemu Windows** -> **Dozwolone aplikacje i funkcje** zezwalają na używanie protokołu RDP dla sieci typu **Domena i prywatne**.
    - Ustawiają zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na wartość **OnlineAll**.

Ponadto po uruchomieniu trybu failover muszą sprawdzić następujące kwestie:

- Podczas wyzwalania trybu failover na maszynie wirtualnej nie powinno być żadnych oczekujących aktualizacji systemu Windows. W takim przypadku nie będzie można zalogować się do maszyny wirtualnej do momentu ukończenia aktualizacji.
- Po przejściu do trybu failover administratorzy mogą sprawdzić **diagnostykę rozruchu**, aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli to nie zadziała, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) na temat przygotowywania maszyn wirtualnych do migracji

## <a name="step-3-replicate-the-on-premises-vms"></a>Krok 3. replikowanie lokalnych maszyn wirtualnych

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

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie wybierz przycisk **Dalej**.
    - Wybierz opcję **Tak**, jeśli masz maszyny z systemem Windows Server, które są objęte aktywnym programem Software Assurance lub subskrypcjami systemu Windows Server, i chcesz zastosować korzyść do migrowanych maszyn. Następnie wybierz przycisk **Dalej**.

8. W obszarze **Obliczenia** sprawdź nazwę, rozmiar, typ dysku systemu operacyjnego i zestaw dostępności maszyny wirtualnej. Maszyny wirtualne muszą być zgodne z [wymaganiami platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Rozmiar maszyny wirtualnej:** Jeśli używasz zaleceń dotyczących oceny, lista rozwijana rozmiaru maszyny wirtualnej będzie zawierać zalecany rozmiar. W przeciwnym razie usługa Azure Migrate wybierze rozmiar na podstawie najbliższego dopasowania w subskrypcji platformy Azure. Alternatywnie możesz wybrać rozmiar ręczny w obszarze **rozmiaru maszyny wirtualnej platformy Azure**.
    - **Dysk systemu operacyjnego:** Określ dysk systemu operacyjnego (Boot) dla maszyny wirtualnej. Dysk systemu operacyjnego to dysk, na którym jest zainstalowany program ładujący i instalator systemu operacyjnego.
    - **Zestaw dostępności:** Jeśli maszyna wirtualna powinna znajdować się w zestawie dostępności platformy Azure po migracji, określ zestaw. Zestaw musi znajdować się w docelowej grupie zasobów określonej dla migracji.

9. W obszarze **Dyski** określ, czy dyski maszyn wirtualnych mają być replikowane na platformę Azure, a następnie wybierz typ dysku (standardowe dyski SSD/dyski twarde lub dyski zarządzane w warstwie Premium) na platformie Azure. Następnie wybierz przycisk **Dalej**.
    - Dyski można wykluczyć z replikacji.
    - Jeśli wykluczysz dyski, nie będą one znajdować się na maszynie wirtualnej platformy Azure po migracji.

10. W obszarze **Przegląd i uruchamianie replikacji**Sprawdź ustawienia, a następnie wybierz pozycję **Replikuj** , aby rozpocząć replikację początkową dla serwerów.

> [!NOTE]
> Ustawienia replikacji możesz zaktualizować w dowolnym momencie przed rozpoczęciem replikacji w obszarze **Zarządzanie** > **Replikowanie maszyn**. Ustawień nie można zmienić po rozpoczęciu replikacji.

## <a name="step-4-migrate-the-vms"></a>Krok 4. Migrowanie maszyn wirtualnych

Administratorzy firmy Contoso uruchamiają szybki test przejścia do trybu failover, a następnie pełne przełączenie w tryb failover, aby zmigrować maszyny wirtualne.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

1. W obszarze **cele migracji** > **serwery** > **Azure Migrate: Migracja serwera**, wybierz opcję **Testuj zmigrowane serwery**.

     ![Serwery z przeprowadzoną migracją testową](./media/contoso-migration-rehost-vm/test-migrated-servers.png)

2. Kliknij prawym przyciskiem myszy maszynę wirtualną do przetestowania, a następnie wybierz pozycję **Testuj migrację**.

    ![Testowanie migracji](./media/contoso-migration-rehost-vm/test-migrate.png)

3. W obszarze **Testowanie migracji** wybierz sieć wirtualną platformy Azure, w której zostanie umieszczona maszyna wirtualna platformy Azure po migracji. Zalecamy użycie sieci wirtualnej nieprodukcyjnej.
4. Zostanie uruchomione zadanie **Testowanie migracji**. Monitoruj zadanie w powiadomieniach portalu.
5. Po zakończeniu migracji sprawdź zmigrowane maszyny wirtualne platformy Azure w obszarze **Maszyny wirtualne** w witrynie Azure Portal. Nazwa maszyny ma sufiks **-Test**.
6. Po zakończeniu testu kliknij prawym przyciskiem myszy maszynę wirtualną platformy Azure w obszarze **replikowanie maszyn**, a następnie wybierz polecenie **Oczyść test migracja**.

    ![Czyszczenie migracji](./media/contoso-migration-rehost-vm/clean-up.png)

### <a name="migrate-the-vms"></a>migrowanie maszyn wirtualnych

Teraz administratorzy firmy Contoso uruchamiają pełne przejście do trybu failover w celu ukończenia migracji.

1. Na **serwerach** Azure Migrate > project > **Azure Migrate: Migracja serwera**, a następnie wybierz opcję **replikowanie serwerów**.

    ![Replikowanie serwerów](./media/contoso-migration-rehost-vm/replicating-servers.png)

2. W obszarze **Replikowanie maszyn** kliknij prawym przyciskiem myszy maszynę wirtualną > **Migruj**.
3. W obszarze **Migrowanie** > **Zamknij maszyny wirtualne i przeprowadź planowaną migrację bez utraty danych** wybierz pozycję **Tak** > **OK**.
    - Domyślnie usługa Azure Migrate zamyka lokalną maszynę wirtualną i uruchamia replikację na żądanie, aby zsynchronizować wszystkie zmiany maszyny wirtualnej, które wystąpiły od momentu ostatniej replikacji. Gwarantuje to brak utraty danych.
    - Jeśli nie chcesz zamykać maszyny wirtualnej, wybierz pozycję **Nie**
4. Zostanie uruchomione zadanie migracji maszyny wirtualnej. Śledź zadanie w powiadomieniach platformy Azure.
5. Po zakończeniu zadania możesz wyświetlić maszynę wirtualną i zarządzać nią na stronie **Maszyny wirtualne**.

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) o próbnym uruchamianiu trybu failover.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) o migracji maszyn wirtualnych do platformy Azure.

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

## <a name="bcdr"></a>BCDR

W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Zachowaj bezpieczeństwo danych: Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Przechowuj aplikacje i uruchamiaj je: contoso replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

1. Firma Contoso ma istniejące licencje dla swoich maszyn wirtualnych i zastosuje korzyść użycia hybrydowego platformy Azure. Firma Contoso przekonwertuje istniejące maszyny wirtualne platformy Azure, aby skorzystać z tych cen.
2. Firma włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła ponowne hostowanie aplikacji SmartHotel360 na platformie Azure, migrując maszyny wirtualne aplikacji do maszyn wirtualnych platformy Azure za pomocą narzędzia migracji serwera usługi Azure Migrate.
