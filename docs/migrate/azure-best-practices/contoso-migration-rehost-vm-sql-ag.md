---
title: Ponowne hostowanie aplikacji przez migrowanie jej na maszyny wirtualne platformy Azure i do zawsze włączonej grupy dostępności programu SQL Server
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso przeprowadza ponowne hostowanie lokalnej aplikacji przez migrowanie jej na maszyny wirtualne platformy Azure i do zawsze włączonych grup dostępności programu SQL Server.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 1292eeec6559fc6caa6cd6ff265a37147cf0b887
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058651"
---
# <a name="rehost-an-on-premises-app-on-azure-vms-and-sql-server-always-on-availability-group"></a>Ponowne hostowanie aplikacji lokalizacji na maszynach wirtualnych platformy Azure i w zawsze włączonej grupie dostępności programu SQL Server

W tym artykule pokazano, jak fikcyjna firma Contoso ponownie hostuje dwuwarstwową aplikację .NET systemu Windows uruchomioną na maszynach wirtualnych VMware w ramach migracji do platformy Azure. Firma Contoso migruje maszynę wirtualną frontonu aplikacji do maszyny wirtualnej platformy Azure oraz bazę danych aplikacji do maszyny wirtualnej usługi Azure SQL Server działającej w klastrze trybu failover systemu Windows Server z zawsze włączonymi grupami dostępności programu SQL Server.

Aplikacja SmartHotel360 używana w tym przykładzie jest oferowana jako aplikacja typu open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Czynniki biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co lokalne systemy i infrastruktura stają się przeciążone.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.** Firma Contoso chce lepiej odpowiadać na zapotrzebowania w branży. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę pomyślnego rozwoju firmy dział IT firmy Contoso musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji:

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie w środowisku VMware. Aplikacja działająca w chmurze będzie miała tak samo krytyczne znaczenie jak w środowisku lokalnym.
- Firma Contoso nie chce inwestować w tę aplikację. Jest ona ważna dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Lokalna baza danych dla aplikacji miała problemy z dostępnością. Firma Contoso chce wdrożyć ją na platformie Azure jako klaster o wysokiej dostępności, korzystając z możliwości pracy w trybie failover.
- Firma Contoso chce uaktualnić bieżącą platformę SQL Server 2008 R2 do programu SQL Server 2017.
- Firma Contoso nie chce używać bazy danych Azure SQL Database dla tej aplikacji i szuka alternatywnych rozwiązań.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu swoich celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które zostaną użyte do tego celu.

### <a name="current-architecture"></a>Bieżąca architektura

- Aplikacja działa warstwowo na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5)
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).

### <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu:

- Firma Contoso przeprowadzi migrację maszyny wirtualnej WEBVM frontonu aplikacji do maszyny wirtualnej usługi IaaS na platformie Azure.
  - Maszyna wirtualna frontonu na platformie Azure zostanie wdrożona w grupie zasobów ContosoRG (używanej w przypadku zasobów produkcyjnych).
  - Zostanie ona umieszczona w sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
- Baza danych aplikacji będzie migrowana do maszyny wirtualnej programu SQL Server na platformie Azure.
  - Będzie ona dostępna w sieci bazy danych platformy Azure firmy Contoso (PROD-DB-EUS2) w regionie podstawowym Wschodnie stany USA 2.
  - Zostanie ona umieszczona w klastrze trybu failover systemu Windows Server z dwoma węzłami, który używa zawsze dostępnych grup dostępności programu SQL Server.
  - Na platformie Azure dwa węzły maszyny wirtualnej programu SQL Server w klastrze zostaną wdrożone w grupie zasobów ContosoRG.
  - Węzły maszyny wirtualnej zostaną umieszczone w sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
  - Na maszynach wirtualnych zostanie uruchomiony system Windows Server 2016 z programem SQL Server 2017 Enterprise Edition. Firma Contoso nie ma licencji dla tego systemu operacyjnego, dlatego użyje obrazu w portalu Azure Marketplace, który będzie dostarczać licencję jako opłatę za zobowiązanie dotyczące umowy związanej z platformą Azure.
  - Poza unikatowymi nazwami obie maszyny wirtualne używają tych samych ustawień.
- Firma Contoso przeprowadzi wdrożenie wewnętrznego modułu równoważenia obciążenia, który nasłuchuje ruchu w klastrze i kieruje go do odpowiedniego węzła klastra.
  - Wewnętrzny moduł równoważenia obciążenia zostanie wdrożony w grupie zasobów ContosoNetworkingRG (używanej do obsługi zasobów sieciowych).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i programu SQL Server. Następujące zagadnienia pomogły podjąć decyzję o przejściu do maszyny wirtualnej usługi IaaS platformy Azure z programem SQL Server:

- Korzystanie z maszyny wirtualnej platformy Azure z programem SQL Server wydaje się być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub bazę danych lub rozważa umieszczenie i uruchamianie na tej samej maszynie wirtualnej aplikacje innych firm.
- Korzystając z narzędzia Data Migration Assistant, firma Contoso może łatwo ocenić bazę danych Azure SQL Database i przeprowadzić jej migrację.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Maszyna wirtualna WEBVM zostanie przeniesiona na platformę Azure bez zmian, co oznacza prostą migrację.<br/><br/> Warstwa programu SQL Server będzie uruchamiana w programie SQL Server 2017 i systemie Windows Server 2016. Spowoduje to wycofanie aktualnego bieżącego systemu operacyjnego Windows Server 2008 R2, a program SQL Server 2017 będzie obsługiwać cele i wymagania techniczne firmy Contoso. Dział IT zapewnia całkowitą zgodność podczas odchodzenia od programu SQL Server 2008 R2.<br/><br/> Firma Contoso może skorzystać z inwestycji w program Software Assurance i zastosować korzyść użycia hybrydowego platformy Azure.<br/><br/> Wdrożenie programu SQL Server o wysokiej dostępności na platformie Azure zapewnia odporność na uszkodzenia, dzięki czemu warstwa danych aplikacji nie jest już jednym punktem przejścia w tryb failover.
**Wady** | Na maszynie wirtualnej WEBVM jest uruchomiony system Windows Server 2008 R2. System operacyjny jest obsługiwany przez platformę Azure dla określonych ról (lipiec 2018). [Dowiedz się więcej](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).<br/><br/> Warstwa internetowa aplikacji wciąż będzie stanowić pojedynczy punkt przejścia w tryb failover.<br/><br/> Firma Contoso nadal będzie musiała obsługiwać warstwę internetową jako maszynę wirtualną platformy Azure, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service.<br/><br/> Przy wybranym rozwiązaniu firma Contoso będzie musiała kontynuować zarządzanie dwoma maszynami wirtualnymi programu SQL Server zamiast przechodzić do platformy zarządzanej, takiej jak wystąpienie zarządzane usługi Azure SQL Database. Ponadto dzięki programowi Software Assurance firma Contoso może wymienić swoje istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi Azure SQL Database.

<!-- markdownlint-enable MD033 -->

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Data Migration Assistant](/sql/dma/dma-overview?view=ssdt-18vs2017) | Narzędzie DMA działa lokalnie z lokalnej maszyny programu SQL Server i migruje bazę danych z sieci VPN typu lokacja-lokacja do platformy Azure. | DMA to bezpłatne narzędzie z możliwością pobrania.
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Usługa Site Recovery orkiestruje odzyskiwanie po awarii i zarządza nim w przypadku maszyn wirtualnych platformy Azure, lokalnych maszyn wirtualnych i serwerów fizycznych. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure zostaną utworzone w momencie przejścia w tryb failover i wówczas będą naliczane opłaty. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery) o opłatach i cenach.

## <a name="migration-process"></a>Proces migracji

Administratorzy firmy Contoso będą migrować maszyny wirtualne aplikacji na platformę Azure.

- Przeprowadzą oni migrację maszyny wirtualnej frontonu do maszyny wirtualnej platformy Azure przy użyciu usługi Site Recovery:
  - Pierwszym krokiem będzie przygotowanie i skonfigurowanie składników platformy Azure oraz przygotowanie lokalnej infrastruktury środowiska VMware.
  - Po przygotowaniu wszystkich elementów administratorzy mogą rozpocząć replikację maszyny wirtualne.
  - Po włączeniu i uruchomieniu replikacji firma przeprowadzą oni migrację maszyny wirtualnej przez przełączenie jej do trybu failover na platformę Azure.
- Przeprowadzą również migrację bazy danych do klastra programu SQL Server na platformie Azure przy użyciu narzędzia Data Migration Assistant (DMA).
  - W ramach pierwszego kroku będą oni musieli aprowizować maszyny wirtualne z programem SQL Server na platformie Azure, skonfigurować klaster i wewnętrzny moduł równoważenia obciążenia oraz skonfigurować zawsze dostępne grup dostępności.
  - Po wykonaniu tych czynności będzie można migrować bazę danych
- Po migracji administratorzy włączą zawsze włączoną ochronę bazy danych.

![Proces migracji](media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Wymagania wstępne

Oto czynności, które firma Contoso musi wykonać w ramach tego scenariusza.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła już subskrypcję na początku tej serii artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.<br/><br/> Dowiedz się więcej na temat szczegółowych wymagań usługi Site Recovery związanych z [siecią](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) i [magazynem](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage).
**Usługa Site Recovery (lokalna)** | Lokalny serwer vCenter w wersji 5.5, 6.0 lub 6.5<br/><br/> Host ESXi w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.<br/><br/> Maszyny wirtualne muszą spełniać [wymagania platformy Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Obsługiwana konfiguracja [sieci](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) i [magazynu](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage).<br/><br/> Maszyny wirtualne, które mają być replikowane, muszą spełniać [wymagania platformy Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Przygotowywanie klastra.** Tworzenie klastra na potrzeby wdrażania dwóch węzłów maszyny wirtualnej z programem SQL Server na platformie Azure.
> - **Krok 2: Wdróż i skonfiguruj klaster.** Przygotowywanie klastra programu SQL Server platformy Azure. Bazy danych są migrowane do istniejącego klastra.
> - **Krok 3. wdrażanie modułu równoważenia obciążenia.** Wdróż moduł równoważenia obciążenia, aby równoważyć ruch do węzłów programu SQL Server.
> - **Krok 4: przygotowanie platformy Azure dla Site Recovery.** Tworzenie konta usługi Azure Storage w celu przechowywania replikowanych danych oraz magazynu usług Recovery Services.
> - **Krok 5: Przygotowanie lokalnego programu VMware do Site Recovery.** Przygotowywanie kont do odnajdywania maszyn wirtualnych i instalacji agenta. Przygotowywanie lokalnych maszyn wirtualnych, aby użytkownicy mogli łączyć się z maszynami wirtualnymi platformy Azure po migracji.
> - **Krok 6. replikowanie maszyn wirtualnych.** Włączanie replikacji maszyny wirtualnej do platformie Azure.
> - **Krok 7. Instalowanie systemu DMA.** Pobieranie i instalowanie narzędzia Data Migration Assistant.
> - **Krok 7. Migrowanie bazy danych za pomocą DMA.** Migrowanie bazy danych na platformę Azure.
> - **Krok 9. Ochrona bazy danych programu.** Tworzenie zawsze dostępnej grupy dostępności dla klastra.
> - **Krok 10. Migrowanie maszyny wirtualnej aplikacji sieci Web.** Uruchom testowanie trybu failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami. Następnie uruchom pełne przejście do trybu failover na platformie Azure.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Krok 1. Przygotowywanie klastra SQL Server z zawsze włączonym grupą dostępności

Administratorzy firmy Contoso konfigurują klaster w następujący sposób:

1. Tworzą dwie maszyny wirtualne z programem SQL Server, wybierając obraz systemu Windows Server 2016 programu SQL Server 2017 Enterprise w portalu Azure Marketplace.

    ![Jednostka SKU maszyny wirtualnej SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

2. W obszarze **Kreator tworzenia maszyny wirtualnej** > **Podstawy** konfigurują:

    - Nazwy maszyn wirtualnych: **SQLAOG1** i **SQLAOG2**.
    - Ponieważ maszyny mają krytyczne znaczenie dla działania firmy, administratorzy włączają dysk SSD dla typu dysku maszyny wirtualnej.
    - Określają poświadczenia maszyny.
    - Wdrażają maszyny wirtualne w regionie podstawowym WSCHODNIE STANY USA 2 w grupie zasobów ContosoRG.

3. W obszarze **Rozmiar** zaczynają się od jednostki SKU D2s_V3 dla obu maszyn wirtualnych. Skalowanie odbędzie się później w miarę potrzeb.
4. W obszarze **Ustawienia** wykonają następujące czynności:

    - Ponieważ te maszyny wirtualne są krytycznymi bazami danych aplikacji, korzystają z dysków zarządzanych.
    - Umieszczają maszyny w sieci produkcyjnej regionu podstawowego WSCHODNIE STANY USA 2 (**VNET-PROD-EUS2**) w podsieci bazy danych (**PROD-DB-EUS2**).
    - Tworzenie nowego zestawu dostępności: **SQLAOGAVSET**, z dwiema domenami błędów i pięcioma domenami aktualizacji.

      ![Maszyna wirtualna SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

5. W obszarze **ustawień programu SQL Server** ograniczają łączność SQL z siecią wirtualną (prywatną) na domyślnym porcie 1433. W przypadku uwierzytelniania korzystają z tych samych poświadczeń, których używają lokalnie (**contosoadmin**).

    ![Maszyna wirtualna SQL](media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

**Potrzebujesz dodatkowej pomocy?**

- [Uzyskaj pomoc](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#1-configure-basic-settings) przy aprowizacji maszyny wirtualnej programu SQL Server.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-prereq#create-sql-server-vms) o konfigurowaniu maszyn wirtualnych dla różnych jednostek SKU programu SQL Server.

## <a name="step-2-deploy-and-set-up-the-cluster"></a>Krok 2. wdrażanie i Konfigurowanie klastra

Administratorzy firmy Contoso konfigurują klaster w następujący sposób:

1. Konfigurują konto usługi Azure Storage do działania jako monitor w chmurze.
2. Dodają maszyny wirtualne z programem SQL Server do domeny Active Directory w lokalnym centrum danych firmy Contoso.
3. Tworzą klaster na platformie Azure.
4. Konfigurują monitor w chmurze.
5. Na koniec włączają zawsze włączone grupy dostępności SQL.

### <a name="set-up-a-storage-account-as-cloud-witness"></a>Konfigurowanie konta magazynu jako monitora w chmurze

Aby skonfigurować monitor w chmurze, firma Contoso potrzebuje konta usługi Azure Storage, na którym będzie przechowywany plik obiektu blob używany do rozstrzygania klastrów. To samo konto magazynu może służyć do konfigurowania monitora w chmurze dla wielu klastrów.

Administratorzy firmy Contoso tworzą konto usługi magazynu w następujący sposób:

1. Określają rozpoznawalną nazwę dla konta (**contosocloudwitness**).
2. Wdrażają ogólne wszechstronne konto z magazynem lokalnie nadmiarowym.
3. Umieszczają konto w trzecim regionie — Południowo-środkowe stany USA. Umieszczają je poza regionem podstawowym i pomocniczym, dzięki czemu będzie ono dostępne w przypadku awarii regionalnej.
4. Umieszczają je w grupie zasobów **ContosoInfraRG**, która zawiera zasoby infrastruktury.

    ![Monitor w chmurze](media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

5. Po utworzeniu konta magazynu są generowane powiązane z nim podstawowe i pomocnicze klucze dostępu. Do utworzenia monitora chmury jest potrzebny podstawowy klucz dostępu. Klucz zostanie wyświetlony w obszarze nazwy konta magazynu > **Klucze dostępu**.

    ![Klucz dostępu](media/contoso-migration-rehost-vm-sql-ag/access-key.png)

### <a name="add-sql-server-vms-to-contoso-domain"></a>Dodawanie maszyn wirtualnych z programem SQL Server do domeny firmy Contoso

1. Firma Contoso dodaje maszyny SQLAOG1 i SQLAOG2 do domeny contoso.com.
2. Następnie na każdej maszynie wirtualnej administratorzy instalują funkcję i narzędzia klastra trybu failover systemu Windows.

### <a name="set-up-the-cluster"></a>Konfigurowanie klastra

Przed skonfigurowaniem klastra administratorzy firmy Contoso tworzą migawkę dysku systemu operacyjnego na każdej maszynie.

![migawka](media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Następnie uruchamiają przygotowany skrypt, aby utworzyć klaster trybu failover systemu Windows.

    ![Tworzenie klastra](media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

2. Po utworzeniu klastra sprawdzają, czy maszyny wirtualne są widoczne jako węzły klastra.

     ![Tworzenie klastra](media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

## <a name="configure-the-cloud-witness"></a>Konfigurowanie monitora w chmurze

1. Administratorzy firmy Contoso konfigurują monitor w chmurze za pomocą **kreatora konfiguracji kworum** w Menedżerze klastra trybu failover.
2. W kreatorze wybierają opcję utworzenia monitora w chmurze na koncie magazynu.
3. Skonfigurowany monitor w chmurze jest wyświetlany w przystawce Menedżer klastra trybu failover.

    ![Monitor w chmurze](media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Włączanie zawsze włączonych grup dostępności programu SQL Server

Administratorzy firmy Contoso mogą teraz włączyć rozwiązanie Zawsze włączone:

1. W programie SQL Server Configuration Manager włączają **zawsze włączone grupy dostępności** dla usługi **SQL Server (MSSQLSERVER)** .

    ![Włączanie rozwiązania Zawsze włączone](media/contoso-migration-rehost-vm-sql-ag/enable-alwayson.png)

2. Ponownie uruchamiają usługę, aby zmiany zaczęły obowiązywać.

Po włączeniu rozwiązania Zawsze włączone firma Contoso może skonfigurować zawsze włączoną grupę dostępności, która będzie chronić bazę danych SmartHotel360.

**Potrzebujesz dodatkowej pomocy?**

- [Przeczytaj informacje](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness) na temat monitora w chmurze i konfigurowania odpowiadającego mu konta magazynu.
- [Uzyskaj instrukcje](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial) dotyczące konfigurowania klastra i tworzenia grupy dostępności.

## <a name="step-3-deploy-the-azure-load-balancer"></a>Krok 3. wdrażanie Azure Load Balancer

Administratorzy firmy Contoso chcą teraz wdrożyć wewnętrzny moduł równoważenia obciążenia, który znajduje się przed węzłami klastra. Moduł równoważenia obciążenia nasłuchuje ruchu i kieruje go do odpowiedniego węzła.

![Równoważenie obciążenia](media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

Tworzą moduł równoważenia obciążenia w następujący sposób:

1. W Azure Portal > **sieci**  > **Load Balancer**konfiguruje nowy wewnętrzny moduł równoważenia obciążenia: **ILB-prod-DB-EUS2-SQLAOG**.
2. Umieszczają moduł równoważenia obciążenia w sieci produkcyjnej **VNET-PROD-EUS2** w podsieci **PROD-DB-EUS2**.
3. Przypisują mu statyczny adres IP: 10.245.40.100.
4. Jako element sieci wdrażają moduł równoważenia obciążenia w grupie zasobów sieciowych **ContosoNetworkingRG**.

    ![Równoważenie obciążenia](media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

Po wdrożeniu wewnętrznego modułu równoważenia obciążenia muszą go skonfigurować. Tworzą pulę adresów zaplecza, konfigurują sondę kondycji, a następnie konfigurują regułę równoważenia obciążenia.

### <a name="add-a-back-end-pool"></a>Dodawanie puli zaplecza

Aby dystrybuować ruch do maszyn wirtualnych w klastrze, administratorzy firmy Contoso konfigurują pulę adresów zaplecza zawierającą adresy IP kart sieciowych dla maszyn wirtualnych, które będą odbierać ruch sieciowy z modułu równoważenia obciążenia.

1. W ustawieniach usługi równoważenia obciążenia w portalu firma Contoso dodaje pulę zaplecza: **ILB-prod-DB-EUS-SQLAOG-BEPOOL**.
2. Kojarzą pulę z zestawem dostępności SQLAOGAVSET. Maszyny wirtualne w zestawie (**SQLAOG1** i **SQLAOG2**) są dodawane do puli.

    ![Pula zaplecza](media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Tworzenie sondy kondycji

Administratorzy firmy Contoso tworzą sondę kondycji, aby moduł równoważenia obciążenia mógł monitorować kondycję aplikacji. Sonda dynamicznie dodaje lub usuwa maszyny wirtualne z rotacji modułu równoważenia obciążenia na podstawie ich odpowiedzi na kontrole kondycji.

Tworzą sondę w następujący sposób:

1. W ustawieniach usługi równoważenia obciążenia w portalu firma Contoso tworzy sondę kondycji: **SQLAlwaysOnEndPointProbe**.
2. Ustawiają sondę tak, aby monitorowała maszyny wirtualne na porcie TCP 59999.
3. Ustawiają interwał wynoszący 5 sekund między sondami oraz próg wynoszący 2. Jeśli dwie sondy zakończą się niepowodzeniem, kondycja maszyny wirtualnej zostanie uznana za złą.

    ![Sonda](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurowanie modułu równoważenia obciążenia do odbierania ruchu

Teraz administratorzy firmy Contoso konfigurują regułę modułu równoważenia obciążenia, aby zdefiniować sposób dystrybucji ruchu do maszyn wirtualnych.

- Adres IP frontonu obsługuje ruch przychodzący.
- Pula adresów IP zaplecza odbiera ruch.

Tworzą regułę w następujący sposób:

1. W ustawieniach usługi równoważenia obciążenia w portalu dodaje nową regułę równoważenia obciążenia: **SQLAlwaysOnEndPointListener**.
2. Ustawiają odbiornik frontonu tak, aby odbierał przychodzący ruch klienta SQL na porcie 1433 protokołu TCP.
3. Określają pulę zaplecza, do której będzie kierowany ruch, oraz port, na którym maszyny wirtualne nasłuchują ruchu.
4. Włączają zmienny adres IP (bezpośredni zwrot serwera). Jest to zawsze wymagane w przypadku rozwiązania Zawsze włączone programu SQL.

    ![Sonda](media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Potrzebujesz dodatkowej pomocy?**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) usługi Azure Load Balancer.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal) na temat tworzenia modułu równoważenia obciążenia.

## <a name="step-4-prepare-azure-for-the-site-recovery-service"></a>Krok 4. Przygotowanie platformy Azure dla usługi Site Recovery

Oto składniki platformy Azure, których firma Contoso potrzebuje do wdrożenia usługi Site Recovery:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne, gdy zostaną utworzone podczas przełączenia w tryb failover.
- Konto magazynu platformy Azure do przechowywania replikowanych danych.
- Magazyn usług Recovery Services na platformie Azure.

Administratorzy firmy Contoso konfigurują te składniki w następujący sposób:

1. Firma Contoso utworzyła już sieć/podsieć, której można używać dla usługi Site Recovery podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-rehost-vm-sql-ag.md).

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyna wirtualna WEBVM zostanie zmigrowana do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
    - Maszyna wirtualna WEBVM zostanie umieszczona w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych, oraz w podsieci produkcyjnej (PROD-FE-EUS2).

2. Administratorzy firmy Contoso tworzą konto usługi Azure Storage (contosovmsacc20180528) w regionie podstawowym.

    - Administratorzy używają konta ogólnego przeznaczenia w warstwie Standard z replikacją LRS.
    - Konto musi znajdować się w tym samym regionie co magazyn.

      ![Magazyn usługi Site Recovery](media/contoso-migration-rehost-vm-sql-ag/asr-storage.png)

3. Po utworzeniu sieci i konta usługi Storage administratorzy tworzą teraz magazyn usługi Recovery Service (**ContosoMigrationVault**) i umieszczają go w grupie zasobów **ContosoFailoverRG**, w regionie podstawowym Wschodnie stany USA 2.

    ![Magazyn usługi Recovery Services](media/contoso-migration-rehost-vm-sql-ag/asr-vault.png)

**Potrzebujesz dodatkowej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure) na temat konfigurowania platformy Azure pod kątem usługi Site Recovery.

## <a name="step-5-prepare-on-premises-vmware-for-site-recovery"></a>Krok 5. Przygotowanie lokalnego programu VMware do Site Recovery

Oto co administratorzy firmy Contoso przygotowują w środowisku lokalnym:

- Konto na serwerze vCenter lub hoście vSphere ESXi w celu zautomatyzowania odnajdowania maszyn wirtualnych.
- Konto umożliwiające automatyczną instalację usługi mobilności na maszynach wirtualnych VMware, które chcą replikować.
- Ustawienia lokalnej maszyny wirtualnej, aby firma Contoso mogła połączyć się z replikowaną maszyną wirtualną platformy Azure po przejściu w tryb failover.

### <a name="prepare-an-account-for-automatic-discovery"></a>Przygotowywanie konta do automatycznego odnajdowania

Usługa Site Recovery musi mieć dostęp do serwerów VMware w następujących celach:

- Automatyczne odnajdywanie maszyn wirtualnych.
- Organizowanie replikacji, trybu failover i powrotu po awarii.
- Wymagane jest co najmniej konto tylko do odczytu. Potrzebne jest konto, na którym można uruchamiać operacje takie jak tworzenie i usuwanie dysków, a także włączanie maszyn wirtualnych.

Administratorzy firmy Contoso konfigurują to konto w następujący sposób:

1. Tworzą rolę na poziomie serwera vCenter.
2. Następnie przypisują do tej roli wymagane uprawnienia.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Przygotowywanie konta do instalacji usługi Mobility

Usługa Mobility Service musi być zainstalowana na każdej maszynie wirtualnej.

- Usługa Site Recovery może przeprowadzić automatyczną instalację wypychaną tego składnika w momencie włączenia replikacji maszyny wirtualnej.
- Potrzebujesz konta, za pomocą którego usługa Site Recovery może uzyskiwać dostęp do maszyny wirtualnej na potrzeby instalacji wypychanej. To konto określasz podczas konfigurowania replikacji w konsoli platformy Azure.
- Może to być konto domeny lub konto lokalne z uprawnieniami do instalowania na maszynie wirtualnej.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po przejściu w tryb failover na platformie Azure firma Contoso chce mieć możliwość nawiązania połączenia z maszynami wirtualnymi na platformie Azure. W tym celu administratorzy firmy Contoso wykonują następujące czynności przed migracją:

1. W celu uzyskania dostępu przez Internet:

   - Włączają protokół RDP na lokalnej maszynie wirtualnej przed przejściem w tryb failover.
   - Upewniają się, że zostały dodane reguły TCP i UDP dla profilu **publicznego**.
   - W obszarze **Zapora systemu Windows** > **Dozwolone aplikacje** sprawdzają, czy protokół RDP jest dozwolony dla wszystkich profilów.

2. W celu uzyskania dostępu przez sieć VPN lokacja-lokacja:

   - Włączają protokół RDP na maszynie lokalnej.
   - W obszarze **Zapora systemu Windows** -> **Dozwolone aplikacje i funkcje** zezwalają na używanie protokołu RDP dla sieci typu **Domena i prywatne**.
   - Ustawiają zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na wartość **OnlineAll**.

Ponadto po uruchomieniu trybu failover muszą sprawdzić następujące kwestie:

- Podczas wyzwalania trybu failover na maszynie wirtualnej nie powinno być żadnych oczekujących aktualizacji systemu Windows. W przeciwnym razie użytkownicy nie będą mogli zalogować się na maszynie wirtualnej do momentu ukończenia aktualizacji.
- Po przejściu do trybu failover administratorzy mogą sprawdzić **diagnostykę rozruchu**, aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli to nie zadziała, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) na temat tworzenia i przypisywania roli na potrzeby automatycznego odnajdowania.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) na temat tworzenia konta na potrzeby instalacji wypychanej usługi mobilności.

## <a name="step-6-replicate-the-on-premises-vms-to-azure-with-site-recovery"></a>Krok 6. replikowanie lokalnych maszyn wirtualnych na platformę Azure za pomocą Site Recovery

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

### <a name="set-a-replication-goal"></a>Wybieranie celu replikacji

1. W magazynie po wybraniu nazwy magazynu (ContosoVMVault) ustawiają cel replikacji (**Wprowadzenie** > **Site Recovery** > **Przygotowanie infrastruktury**).
2. Administratorzy określają, że ich maszyny wirtualne znajdują się w środowisku lokalnym, działają w programie VMware i są replikowane na platformie Azure.

    ![Cel replikacji](./media/contoso-migration-rehost-vm-sql-ag/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potwierdzanie planowania wdrożenia

Aby kontynuować, muszą potwierdzić, że zakończono planowanie wdrożenia, wybierając pozycję **Tak, już to zostało zrobione**. W tym scenariuszu firma Contoso tylko migruje maszynę wirtualną, co nie wymaga planowania wdrożenia.

### <a name="set-up-the-source-environment"></a>Konfigurowanie środowiska źródłowego

Administratorzy firmy Contoso muszą skonfigurować środowisko źródłowe. W tym celu pobiorą szablon OVF i za jego pomocą wdrożą serwer konfiguracji usługi Site Recovery jako wysoce dostępną lokalną maszynę wirtualną VMware. Po uruchomieniu serwera konfiguracji rejestrują go w magazynie.

Na serwerze konfiguracji jest uruchomionych kilka składników:

- Składnik serwera konfiguracji służy do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure oraz do zarządzania replikacją danych.
- Serwer przetwarzania, który działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła je do usługi Azure Storage.
- Serwer przetwarzania instaluje także usługę mobilności na maszynach wirtualnych, które będą replikowane, i automatycznie odnajduje lokalne maszyny wirtualne VMware.

Administratorzy firmy Contoso wykonują te czynności w następujący sposób:

1. W magazynie pobierają szablon OVF z obszaru **Przygotowanie infrastruktury** > **Źródło** > **Serwer konfiguracji**.

    ![Pobieranie szablonu OVF](./media/contoso-migration-rehost-vm-sql-ag/add-cs.png)

2. Importują szablon do programu VMware w celu utworzenia i wdrożenia maszyny wirtualnej.

    ![Szablon OVF](./media/contoso-migration-rehost-vm-sql-ag/vcenter-wizard.png)

3. Po pierwszym uruchomieniu maszyna wirtualna uruchamia środowisko instalacji systemu Windows Server 2016. Administratorzy akceptują umowę licencyjną i wprowadzają hasło administratora.
4. Po zakończeniu instalacji logują się na maszynie wirtualnej jako administrator. Po pierwszym zalogowaniu zostanie domyślnie uruchomione narzędzie do konfiguracji usługi Azure Site Recovery.
5. W tym narzędziu należy określić nazwę używaną do zarejestrowania serwera konfiguracji w magazynie.
6. Narzędzie sprawdza, czy maszyna wirtualna może połączyć się z platformą Azure. Po nawiązaniu połączenia administratorzy logują się w subskrypcji platformy Azure. Użyte poświadczenia muszą zapewniać dostęp do magazynu, w którym chcesz zarejestrować serwer konfiguracji.

    ![Rejestrowanie serwera konfiguracji](./media/contoso-migration-rehost-vm-sql-ag/config-server-register2.png)

7. Narzędzie wykonuje pewne zadania konfiguracyjne, a następnie wywołuje ponowne uruchomienie.
8. Administratorzy ponownie logują się na maszynie, po czym jest automatycznie uruchamiany kreator zarządzania serwerem konfiguracji.
9. W kreatorze wybierają kartę sieciową, która będzie odbierała ruch związany z replikacją. Po skonfigurowaniu tego ustawienia nie można go zmienić.
10. Wybierają subskrypcję, grupę zasobów i magazyn do zarejestrowania serwera konfiguracji.
        ![magazyn](./media/contoso-migration-rehost-vm-sql-ag/cswiz1.png)

11. Następnie pobierają i instalują serwer MySQL oraz oprogramowanie VMware PowerCLI.
12. Po przeprowadzeniu walidacji określają nazwę FQDN lub adres IP serwera vCenter lub hosta vSphere. Pozostawiają port domyślny i określają przyjazną nazwę serwera vCenter.
13. Określają konto utworzone na potrzeby automatycznego odnajdowania oraz poświadczenia służące do automatycznej instalacji usługi Mobility Service. W przypadku maszyn z systemem Windows konto musi mieć uprawnienia administratora lokalnego na maszynach wirtualnych.

    ![vCenter](./media/contoso-migration-rehost-vm-sql-ag/cswiz2.png)

14. Po zakończeniu rejestracji dokładnie sprawdzają w witrynie Azure Portal, czy serwer konfiguracji i serwer VMware są widoczne na stronie **Źródło** w magazynie. Odnajdowanie może potrwać 15 minut lub dłużej.
15. Usługa Site Recovery nawiąże połączenie z serwerami VMware przy użyciu podanych ustawień i odnajdzie maszyny wirtualne.

### <a name="set-up-the-target"></a>Konfigurowanie środowiska docelowego

Teraz administratorzy firmy Contoso określają ustawienia replikacji w środowisku docelowym.

1. W obszarze **Przygotowanie infrastruktury** > **Docelowa** wybierają ustawienia środowiska docelowego.
2. Usługa Site Recovery sprawdza, czy we wskazanym środowisku docelowym istnieje konto usługi Azure Storage i sieć.

### <a name="create-a-replication-policy"></a>Tworzenie zasad replikacji

Teraz administratorzy firmy Contoso mogą utworzyć zasady replikacji.

1. W obszarze **Przygotowanie infrastruktury** > **Ustawienia replikacji** > **Zasady replikacji** >  **Utwórz i skojarz** administratorzy tworzą zasady o nazwie **ContosoMigrationPolicy**.
2. Korzystają z ustawień domyślnych:
    - **Próg punktu odzyskiwania:** Domyślnie 60 minut. Ta wartość określa częstość tworzenia punktów odzyskiwania. Przekroczenie tego limitu przez replikację ciągłą spowoduje wygenerowanie alertu.
    - **Przechowywanie punktów odzyskiwania:** Domyślnie 24 godziny. Ta wartość określa długość okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać do dowolnego punktu w tym oknie.
    - **Częstotliwość migawek spójnych na poziomie aplikacji:** Wartość domyślna to godzina. Ta wartość określa częstotliwość tworzenia migawek spójnych na poziomie aplikacji.

        ![Tworzenie zasad replikacji](./media/contoso-migration-rehost-vm-sql-ag/replication-policy.png)

3. Zasady zostaną automatycznie skojarzone z serwerem konfiguracji.

    ![Kojarzenie zasad replikacji](./media/contoso-migration-rehost-vm-sql-ag/replication-policy2.png)

### <a name="enable-replication"></a>Włączanie replikacji

Teraz administratorzy firmy Contoso mogą rozpocząć replikację maszyny wirtualnej WebVM.

1. W obszarze **Replikowanie aplikacji** > **Źródło** >  **+Replikuj** wybierają ustawienia źródła.
2. Określają, że chcą włączyć maszyny wirtualne oraz wybierają serwer vCenter i serwer konfiguracji.

    ![Włączanie replikacji](./media/contoso-migration-rehost-vm-sql-ag/enable-replication1.png)

3. Teraz określają ustawienia środowiska docelowego, w tym grupę zasobów i sieć wirtualną, a także konto usługi Storage, na którym będą przechowywane replikowane dane.

     ![Włączanie replikacji](./media/contoso-migration-rehost-vm-sql-ag/enable-replication2.png)

4. Wybierają maszynę wirtualną WebVM do replikacji, sprawdzają zasady replikacji i włączają replikację. Po włączeniu replikacji usługa Site Recovery instaluje usługę Mobility Service na każdej maszynie wirtualnej.

    ![Włączanie replikacji](./media/contoso-migration-rehost-vm-sql-ag/enable-replication3.png)

5. Postęp replikacji można śledzić w obszarze **Zadania**. Po uruchomieniu zadania **Sfinalizuj ochronę** maszyna jest gotowa do przejścia w tryb failover.
6. W obszarze **Podstawy** w witrynie Azure Portal mogą zobaczyć strukturę maszyn wirtualnych replikowanych na platformie Azure.

    ![Widok infrastruktury](./media/contoso-migration-rehost-vm-sql-ag/essentials.png)

**Potrzebujesz dodatkowej pomocy?**

- Pełne instrukcje do wszystkich kroków można znaleźć w artykule [Konfigurowanie odzyskiwania po awarii dla lokalnych maszyn wirtualnych VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Szczegółowe instrukcje pomogą Ci w [skonfigurowaniu środowiska źródłowego](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [wdrożeniu serwera konfiguracji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) i [skonfigurowaniu ustawień replikacji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).
- Możesz dowiedzieć się więcej na temat [włączania replikacji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-7-install-the-data-migration-assistant-dma"></a>Krok 7. Instalowanie Data Migration Assistant (DMA)

Administratorzy firmy Contoso będą migrować bazę danych SmartHotel360 do maszyny wirtualnej platformy Azure o nazwie **SQLAOG1** przy użyciu narzędzia DMA. Konfigurują narzędzie DMA w następujący sposób:

1. Pobierają oni narzędzie z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=53595) na lokalną maszynę wirtualną programu SQL Server (**SQLVM**).
2. Uruchamiają instalatora (DownloadMigrationAssistant.msi) na maszynie wirtualnej.
3. Na stronie **Finish** (Zakończenie) wybierają pozycję **Launch Microsoft Data Migration Assistant** (Uruchom narzędzie Microsoft Data Migration Assistant) przed zakończeniem pracy kreatora.

## <a name="step-8-migrate-the-database-with-dma"></a>Krok 8. Migrowanie bazy danych przy użyciu DMA

1. W narzędziu DMA administratorzy uruchamiają nową migrację, **SmartHotel**.
2. W obszarze **Target server type** (Typ serwera docelowego) wybierają pozycję **SQL Server on Azure Virtual Machines** (Program SQL Server na maszynach wirtualnych platformy Azure).

    ![Narzędzie DMA](media/contoso-migration-rehost-vm-sql-ag/dma-1.png)

3. W obszarze szczegółów migracji dodają maszynę wirtualną **SQLVM** jako serwer źródłowy i maszynę wirtualną **SQLAOG1** jako obiekt docelowy. Określają poświadczenia dla każdej maszyny.

     ![Narzędzie DMA](media/contoso-migration-rehost-vm-sql-ag/dma-2.png)

4. Tworzą udział lokalny dla informacji dotyczących bazy danych i konfiguracji. Musi być on dostępny z dostępem do zapisu przez konto programu SQL Server na maszynach wirtualnych SQLVM i SQLAOG1.

    ![Narzędzie DMA](media/contoso-migration-rehost-vm-sql-ag/dma-3.png)

5. Firma Contoso wybiera nazwy logowania, które powinny być migrowane, a następnie uruchamia migrację. Po zakończeniu narzędzie DMA pokazuje migrację jako zakończoną pomyślnie.

    ![Narzędzie DMA](media/contoso-migration-rehost-vm-sql-ag/dma-4.png)

6. Sprawdzają, czy baza danych działa na maszynie wirtualnej **SQLAOG1**.

    ![Narzędzie DMA](media/contoso-migration-rehost-vm-sql-ag/dma-5.png)

Narzędzie DMA nawiązuje połączenie z lokalną maszyną wirtualną z programem SQL Server przy użyciu połączenia sieci VPN typu lokacja-lokacja między centrum danych firmy Contoso i platformą Azure, a następnie migruje bazę danych.

## <a name="step-7-protect-the-database-with-always-on"></a>Krok 7. Ochrona bazy danych zawsze włączona

W przypadku bazy danych aplikacji działającej na maszynie wirtualnej **SQLAOG1** administratorzy firmy Contoso mogą teraz chronić ją przy użyciu zawsze włączonych grup dostępności. Konfigurują rozwiązanie Zawsze włączone przy użyciu programu SQL Management Studio, a następnie przypisują odbiornik przy użyciu klastrowania systemu Windows.

### <a name="create-an-always-on-availability-group"></a>Tworzenie zawsze włączonej grupy dostępności

1. W programie SQL Management Studio klikają prawym przyciskiem myszy pozycję **Always on High Availability** (Zawsze włączona wysoka dostępność), aby uruchomić kreatora **New Availability Group Wizard** (Kreator nowej grupy dostępności).
2. W obszarze **Specify Options** (Określanie opcji) nadają grupie dostępności nazwę **SHAOG**. W obszarze **Select Database** (Wybieranie bazy danych) wybierają bazę danych SmartHotel360.

    ![Zawsze włączona grupa dostępności](media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

3. W obszarze **Specify Replicas** (Określanie replik) dodają dwa węzły SQL jako repliki dostępności, a następnie konfigurują je w celu zapewnienia automatycznego przejścia w tryb failover z zatwierdzaniem synchronicznym.

     ![Zawsze włączona grupa dostępności](media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

4. Konfigurują odbiornik dla grupy (**SHAOG**) i port. Adres IP wewnętrznego modułu równoważenia obciążenia jest dodawany jako statyczny adres IP (10.245.40.100).

    ![Zawsze włączona grupa dostępności](media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

5. W obszarze **Select Data Synchronization** (Wybieranie synchronizacji danych) włączają automatyczne rozmieszczanie. W przypadku tej opcji program SQL Server automatycznie tworzy repliki pomocnicze dla każdej bazy danych w grupie, więc firma Contoso nie musi ręcznie tworzyć kopii zapasowych ani ich przywracać. Po zakończeniu walidacji zostanie utworzona grupa dostępności.

    ![Zawsze włączona grupa dostępności](media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

6. Firma Contoso napotkała problem podczas tworzenia grupy. Administratorzy nie używają zintegrowanych zabezpieczeń systemu Windows i dlatego muszą udzielić uprawnień do logowania SQL w celu utworzenia ról klastra trybu failover systemu Windows.

    ![Zawsze włączona grupa dostępności](media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

7. Po utworzeniu grupy firma Contoso może ją zobaczyć w programie SQL Management Studio.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurowanie odbiornika w klastrze

W ramach ostatniego kroku konfigurowania wdrożenia SQL administratorzy firmy Contoso konfigurują wewnętrzny moduł równoważenia obciążenia jako odbiornik w klastrze i przenoszą odbiornik do trybu online. W tym celu używają skryptu.

![Odbiornik klastra](media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Sprawdzanie konfiguracji

Po skonfigurowaniu wszystkich elementów firma Contoso ma teraz działającą grupę dostępności na platformie Azure, która korzysta z migrowanej bazy danych. Administratorzy sprawdzają to, łącząc się z wewnętrznym modułem równoważenia obciążenia w programie SQL Management Studio.

![Połączenie z wewnętrznym modułem równoważenia obciążenia](media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Potrzebujesz dodatkowej pomocy?**

- Dowiedz się więcej na temat [grupy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) i [odbiornika](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener).
- Ręcznie [skonfiguruj klaster tak, aby używał adresu IP modułu równoważenia obciążenia](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address).
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2) na temat tworzenia i używania sygnatur dostępu współdzielonego.

## <a name="step-8-migrate-the-vm-with-site-recovery"></a>Krok 8. Migrowanie maszyny wirtualnej za pomocą Site Recovery

Administratorzy firmy Contoso uruchamiają szybki test przejścia do trybu failover, a następnie przeprowadzają migrację maszyny wirtualnej.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Próba przejścia do trybu failover pozwala sprawdzić, czy wszystko działa zgodnie z oczekiwaniami, przed przeprowadzeniem faktycznej migracji.

1. Uruchamiają testowe przełączenie w tryb failover przy użyciu najnowszego dostępnego punktu w czasie (**Najnowszy przetworzony**).
2. Wybierają opcję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**, aby usługa Site Recovery podjęła próbę zamknięcia źródłowej maszyny wirtualnej przed jej przełączeniem w tryb failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się.
3. Próbne przełączenia do trybu failover:

    - Uruchamiane jest sprawdzanie wymagań wstępnych, aby upewnić się, że zostały spełnione wszystkie warunki migracji.
    - Tryb failover przetwarza dane, aby umożliwić utworzenie maszyny wirtualnej platformy Azure. Jeśli zostanie wybrany najnowszy punkt odzyskiwania, punkt odzyskiwania zostanie utworzony na podstawie danych.
    - Tworzona jest maszyna wirtualna platformy Azure przy użyciu danych przetworzonych w poprzednim kroku.

4. Po zakończeniu przechodzenia w tryb failover w witrynie Azure Portal będzie widoczna replika maszyny wirtualnej na platformie Azure. Administratorzy sprawdzają, czy maszyna wirtualna ma prawidłowy rozmiar, jest połączona z odpowiednią siecią i jest uruchomiona.
5. Gdy wszystko zostanie sprawdzone, przeprowadzają czyszczenie po przejściu do trybu failover oraz rejestrują i zapisują wszelkie obserwacje.

### <a name="run-a-failover"></a>Uruchamianie trybu failover

1. Jeśli próbne przejście do trybu failover przebiegło zgodnie z oczekiwaniami, administratorzy firmy Contoso mogą utworzyć plan odzyskiwania na potrzeby migracji i dodać maszynę wirtualną WEBVM do planu.

     ![Plan odzyskiwania](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

2. Uruchamiają tryb failover z użyciem utworzonego planu. Wybierają najnowszy punkt odzyskiwania i określają, że usługa Site Recovery powinna podjąć próbę zamknięcia lokalnej maszyny wirtualnej przed wyzwoleniem trybu failover.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

3. Po przejściu w tryb failover administratorzy sprawdzają, czy maszyna wirtualna platformy Azure jest widoczna zgodnie z oczekiwaniami w witrynie Azure Portal.

    ![Plan odzyskiwania](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

4. Po sprawdzeniu maszyny wirtualnej na platformie Azure kończą migrację, aby zakończyć proces migracji, zatrzymać replikację maszyny wirtualnej i zatrzymać naliczanie opłat za usługę Site Recovery dla maszyny wirtualnej.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Aktualizowanie parametrów połączenia

W ostatnim kroku procesu migracji administratorzy firmy Contoso aktualizują parametry połączenia aplikacji tak, aby wskazywały migrowaną bazę danych działającą na odbiorniku SHAOG. Ta konfiguracja zostanie zmieniona na maszynie wirtualnej WEBVM działającej obecnie na platformie Azure. Ta konfiguracja znajduje się w pliku web.config aplikacji ASP.

1. Znajdź plik w lokalizacji C:\inetpub\SmartHotelWeb\web.config. Zmień nazwę serwera w celu odzwierciedlenia nazwy FQDN AOG: shaog.contoso.com.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

2. Po zaktualizowaniu pliku i zapisaniu go ponownie uruchamiają usługi IIS na maszynie wirtualnej WEBVM. W tym celu używają polecenia IISRESET/RESTART z poziomu wiersza polecenia.
3. Po ponownym uruchomieniu usług IIS aplikacja korzysta teraz z bazy danych działającej w programie SQL MI.

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) o próbnym uruchamianiu trybu failover.
- [Dowiedz się](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans), jak utworzyć plan odzyskiwania.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) na temat przechodzenia do trybu failover na platformie Azure.

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po migracji aplikacja SmartHotel360 działa na maszynie wirtualnej platformy Azure, a baza danych SmartHotel360 znajduje się w klastrze usług SQL Azure.

Teraz firma Contoso musi wykonać następujące kroki dotyczące czyszczenia:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie dokumentacji wewnętrznej tak, aby wyświetlić nowe lokalizacje i adresy IP maszyn wirtualnych.
- Przegląd wszystkich zasobów korzystających z zlikwidowanych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Dodanie dwóch nowych maszyn wirtualnych (SQLAOG1 i SQLAOG2) do systemów monitorowania produkcji.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso sprawdza maszyny wirtualne platformy Azure WEBVM, SQLAOG1 and SQLAOG2, aby określić problemy z zabezpieczeniami.

- Zespół przegląda sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyny wirtualnej. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Zespół rozważa zabezpieczenie danych na dysku przy użyciu usług Azure Disk Encryption i Key Vault.
- Zespół powinien oszacować szyfrowanie Transparent Data Encryption (TDE), a następnie włączyć je w bazie danych SmartHotel360 działającej na nowym odbiorniku AOG SQL. [Dowiedz się więcej](/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017).

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania w zakresie zabezpieczeń dotyczące obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="bcdr"></a>Zapewnienie ciągłości działania i odzyskiwanie po awarii

 W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Zachowaj bezpieczeństwo danych: Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych WEBVM, SQLAOG1 i SQLAOG2 za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Firma Contoso sprawdza również, jak używać usługi Azure Storage do tworzenia kopii zapasowych programu SQL Server bezpośrednio do magazynu obiektów blob. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore).
- Przechowuj aplikacje i uruchamiaj je: contoso replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

1. Firma Contoso ma istniejące licencje dla maszyny wirtualnej WEBVM i zastosuje korzyść użycia hybrydowego platformy Azure. Firma Contoso przekonwertuje istniejące maszyny wirtualne platformy Azure, aby skorzystać z tych cen.
2. Firma Contoso włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) o usłudze Azure Cost Management.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła ponowne hostowanie aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji na platformę Azure za pomocą usługi Site Recovery. Firma Contoso przeprowadziła migrację bazy danych aplikacji do klastra programu SQL Server aprowizowanego na platformie Azure i zabezpieczyła ją w zawsze włączonej grupie programu SQL Server.
