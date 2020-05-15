---
title: Hostowanie aplikacji przez Migrowanie jej do maszyn wirtualnych platformy Azure i zawsze dostępnych grup dostępności SQL Server
description: Dowiedz się, jak firma Contoso przeprowadza ponowne hostowanie lokalnej aplikacji przez migrowanie jej na maszyny wirtualne platformy Azure i do zawsze włączonych grup dostępności programu SQL Server.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: c356554dbdca417708d7eb9698d9729270d8e981
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401021"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc AOAG SQLAOG SQLAOGAVSET contosoadmin contosocloudwitness MSSQLSERVER BEPOOL contosovmsacc SHAOG NSGs inetpub iisreset -->

# <a name="rehost-an-on-premises-app-with-azure-virtual-machines-and-sql-server-always-on-availability-groups"></a>Ponowne hostowanie aplikacji lokalnej przy użyciu usługi Azure Virtual Machines i SQL Server zawsze włączone grupy dostępności

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso rehostuje dwuwarstwową aplikację systemu Windows .NET działającą na maszynach wirtualnych VMware w ramach migracji na platformę Azure. Firma Contoso migruje maszynę wirtualną frontonu aplikacji do maszyny wirtualnej platformy Azure oraz bazę danych aplikacji do maszyny wirtualnej usługi Azure SQL Server działającej w klastrze trybu failover systemu Windows Server z zawsze włączonymi grupami dostępności programu SQL Server.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co lokalne systemy i infrastruktura stają się przeciążone.

- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.

- **Zwiększenie elastyczności.** Dział IT firmy Contoso chce lepiej odpowiadać na zapotrzebowania biznesowe. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.

- **Zasięgu.** W miarę pomyślnego rozwoju firmy dział IT firmy Contoso musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.

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
- Maszyny wirtualne znajdują się na VMware ESXi hosta **contosohost1.contoso.com** (wersja 6,5).
- Środowisko VMware jest zarządzane przez vCenter Server 6,5 (**vCenter.contoso.com**), uruchomione na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-Datacenter) z lokalnym kontrolerem domeny (**ContosoDC1**).

### <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu:

- Firma Contoso przeprowadzi migrację maszyny wirtualnej WEBVM frontonu aplikacji do maszyny wirtualnej usługi IaaS na platformie Azure.
  - Maszyna wirtualna frontonu na platformie Azure zostanie wdrożona w grupie zasobów ContosoRG (używanej w przypadku zasobów produkcyjnych).
  - Zostanie ona umieszczona w sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
- Baza danych aplikacji będzie migrowana do maszyny wirtualnej programu SQL Server na platformie Azure.
  - Będzie ona dostępna w sieci bazy danych platformy Azure firmy Contoso (PROD-DB-EUS2) w regionie podstawowym Wschodnie stany USA 2.
  - Zostanie ona umieszczona w klastrze trybu failover systemu Windows Server z dwoma węzłami, który używa zawsze dostępnych grup dostępności programu SQL Server.
  - Na platformie Azure zostaną wdrożone dwa SQL Server węzły maszyny wirtualnej w klastrze w grupie zasobów ContosoRG.
  - Węzły maszyny wirtualnej zostaną umieszczone w sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
  - Na maszynach wirtualnych zostanie uruchomiony system Windows Server 2016 z programem SQL Server 2017 Enterprise Edition. Firma Contoso nie ma licencji dla tego systemu operacyjnego, dlatego użyje obrazu w portalu Azure Marketplace, który będzie dostarczać licencję jako opłatę za zobowiązanie dotyczące umowy związanej z platformą Azure.
  - Poza unikatowymi nazwami obie maszyny wirtualne używają tych samych ustawień.
- Firma Contoso przeprowadzi wdrożenie wewnętrznego modułu równoważenia obciążenia, który nasłuchuje ruchu w klastrze i kieruje go do odpowiedniego węzła klastra.
  - Wewnętrzny moduł równoważenia obciążenia zostanie wdrożony w grupie zasobów ContosoNetworkingRG (używanej do obsługi zasobów sieciowych).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

    ![Architektura scenariusza](./media/contoso-migration-rehost-vm-sql-ag/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i programu SQL Server. Następujące zagadnienia pomogły podjąć decyzję o przejściu do maszyny wirtualnej usługi IaaS platformy Azure z programem SQL Server:

- Korzystanie z maszyny wirtualnej platformy Azure z programem SQL Server wydaje się być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub bazę danych lub rozważa umieszczenie i uruchamianie na tej samej maszynie wirtualnej aplikacje innych firm.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Maszyna wirtualna WEBVM zostanie przeniesiona na platformę Azure bez zmian, co oznacza prostą migrację. <br><br> Warstwa programu SQL Server będzie uruchamiana w programie SQL Server 2017 i systemie Windows Server 2016. Spowoduje to wycofanie aktualnego bieżącego systemu operacyjnego Windows Server 2008 R2, a program SQL Server 2017 będzie obsługiwać cele i wymagania techniczne firmy Contoso. Dział IT zapewnia całkowitą zgodność podczas odchodzenia od programu SQL Server 2008 R2. <br><br> Firma Contoso może skorzystać z inwestycji w program Software Assurance i zastosować korzyść użycia hybrydowego platformy Azure. <br><br> Wdrożenie programu SQL Server o wysokiej dostępności na platformie Azure zapewnia odporność na uszkodzenia, dzięki czemu warstwa danych aplikacji nie jest już jednym punktem przejścia w tryb failover.
**Wady** | Na maszynie wirtualnej WEBVM jest uruchomiony system Windows Server 2008 R2. System operacyjny jest obsługiwany przez platformę Azure dla określonych ról (lipiec 2018). [Dowiedz się więcej](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines). <br><br> Warstwa internetowa aplikacji wciąż będzie stanowić pojedynczy punkt przejścia w tryb failover. <br><br> Firma Contoso nadal będzie musiała obsługiwać warstwę internetową jako maszynę wirtualną platformy Azure, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service. <br><br> Przy wybranym rozwiązaniu firma Contoso będzie musiała kontynuować zarządzanie dwoma maszynami wirtualnymi programu SQL Server zamiast przechodzić do platformy zarządzanej, takiej jak wystąpienie zarządzane usługi Azure SQL Database. Ponadto dzięki programowi Software Assurance firma Contoso może wymienić swoje istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi Azure SQL Database.

<!-- markdownlint-enable MD033 -->

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) | Firma Contoso używa usługi Azure Migrate do oceny swoich maszyn wirtualnych VMware. Usługa Azure Migrate ocenia przydatność maszyn do migracji. Dzięki tej usłudze można oszacować wymagany rozmiar i koszt działania na platformie Azure. | Od maja 2018 r. Azure Migrate jest usługą bezpłatną.

## <a name="migration-process"></a>Proces migracji

Administratorzy firmy Contoso będą migrować maszyny wirtualne aplikacji na platformę Azure.

- Przeprowadzimy migrację maszyny wirtualnej frontonu do maszyny wirtualnej platformy Azure przy użyciu Azure Migrate:
  - Pierwszym krokiem będzie przygotowanie i skonfigurowanie składników platformy Azure oraz przygotowanie lokalnej infrastruktury środowiska VMware.
  - Po przygotowaniu wszystkich elementów administratorzy mogą rozpocząć replikację maszyny wirtualne.
  - Po włączeniu i uruchomieniu replikacji firma przeprowadzą oni migrację maszyny wirtualnej przez przełączenie jej do trybu failover na platformę Azure.
- Po zweryfikowaniu bazy danych przeprowadzimy migrację bazy danych do klastra SQL Server na platformie Azure przy użyciu usługi Data Migration Service (DMS).
  - W ramach pierwszego kroku będą oni musieli aprowizować maszyny wirtualne z programem SQL Server na platformie Azure, skonfigurować klaster i wewnętrzny moduł równoważenia obciążenia oraz skonfigurować zawsze dostępne grup dostępności.
  - Dzięki temu można migrować bazę danych.
- Po migracji administratorzy włączą zawsze włączoną ochronę bazy danych.

    ![Proces migracji](./media/contoso-migration-rehost-vm-sql-ag/migration-process.png)

## <a name="prerequisites"></a>Wymagania wstępne

Oto czynności, które firma Contoso musi wykonać w ramach tego scenariusza.

<!-- markdownlint-disable MD033 -->

| **Wymagania** | **Szczegóły** |
| --- | --- |
| **Subskrypcja platformy Azure** | Firma Contoso utworzyła już subskrypcję na początku tej serii artykułów. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial). <br><br> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje. <br><br> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora. |
| **Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Infrastruktura platformy Azure wymagana do migracji](./contoso-migration-infrastructure.md). <br><br> Dowiedz się więcej na temat wymagań [wstępnych](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) dotyczących Azure Migrate: Migracja serwera. |
| **Serwery lokalne** | Lokalny serwer vCenter powinien mieć uruchomioną wersję 5,5, 6,0, 6,5 lub 6,7. <br><br> Host ESXi z systemem w wersji 5,5, 6,0, 6,5 lub 6,7. <br><br> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi. |
| **Lokalne maszyny wirtualne** | [Przejrzyj maszyny z systemem Linux](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), które zostały zatwierdzone do działania na platformie Azure. |

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1: przygotowanie klastra AOAG.** Tworzenie klastra na potrzeby wdrażania dwóch węzłów maszyny wirtualnej z programem SQL Server na platformie Azure.
> - **Krok 2: Wdróż i skonfiguruj klaster.** Przygotowywanie klastra programu SQL Server platformy Azure. Bazy danych są migrowane do istniejącego klastra.
> - **Krok 3. wdrożenie Azure Load Balancer.** Wdróż moduł równoważenia obciążenia, aby równoważyć ruch do węzłów programu SQL Server.
> - **Krok 4: przygotowanie platformy Azure dla Azure Migrate.** Utwórz konto usługi Azure Storage, aby przechowywać zreplikowane dane.
> - **Krok 5: Przygotowanie lokalnego programu VMware do Azure Migrate.** Przygotowywanie kont do odnajdywania maszyn wirtualnych i instalacji agenta. Przygotowywanie lokalnych maszyn wirtualnych, aby użytkownicy mogli łączyć się z maszynami wirtualnymi platformy Azure po migracji.
> - **Krok 6. replikowanie maszyn wirtualnych.** Włączanie replikacji maszyny wirtualnej do platformie Azure.
> - **Krok 7. Migrowanie bazy danych za pomocą usługi Data Migration Service (DMS).** Przeprowadź migrację bazy danych na platformę Azure przy użyciu usługi Data Migration Service.
> - **Krok 8. Ochrona bazy danych programu.** Tworzenie zawsze dostępnej grupy dostępności dla klastra.
> - **Krok 9. Migrowanie maszyn wirtualnych za pomocą Azure Migrate** Uruchom test pracy w trybie failover, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami. Następnie uruchom pełne przejście do trybu failover na platformie Azure.

## <a name="step-1-prepare-a-sql-server-always-on-availability-group-cluster"></a>Krok 1. Przygotowywanie klastra SQL Server z zawsze włączonym grupą dostępności

Administratorzy firmy Contoso konfigurują klaster w następujący sposób:

1. Tworzą dwie maszyny wirtualne z programem SQL Server, wybierając obraz systemu Windows Server 2016 programu SQL Server 2017 Enterprise w portalu Azure Marketplace.

    ![Jednostka SKU maszyny wirtualnej SQL](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-sku.png)

2. W oknie **Kreator tworzenia maszyny wirtualnej**  >  **—** konfiguracja:

    - Nazwy maszyn wirtualnych: **SQLAOG1** i **SQLAOG2**.
    - Ponieważ maszyny mają krytyczne znaczenie dla działania firmy, administratorzy włączają dysk SSD dla typu dysku maszyny wirtualnej.
    - Określają poświadczenia maszyny.
    - Wdrażają maszyny wirtualne w regionie podstawowym WSCHODNIE STANY USA 2 w grupie zasobów ContosoRG.

3. W obszarze **Rozmiar** zaczynają się od jednostki SKU D2s_V3 dla obu maszyn wirtualnych. Skalowanie odbędzie się później w miarę potrzeb.
4. W obszarze **Ustawienia** wykonają następujące czynności:

    - Ponieważ te maszyny wirtualne są krytycznymi bazami danych aplikacji, korzystają z dysków zarządzanych.
    - Umieszczają maszyny w sieci produkcyjnej regionu podstawowego WSCHODNIE STANY USA 2 (**VNET-PROD-EUS2**) w podsieci bazy danych (**PROD-DB-EUS2**).
    - Tworzenie nowego zestawu dostępności: **SQLAOGAVSET**, z dwiema domenami błędów i pięcioma domenami aktualizacji.

      ![Maszyna wirtualna SQL](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-settings.png)

5. W obszarze **ustawień programu SQL Server** ograniczają łączność SQL z siecią wirtualną (prywatną) na domyślnym porcie 1433. W przypadku uwierzytelniania używane są te same poświadczenia, które są używane w witrynie Onsite (**contosoadmin**).

    ![Maszyna wirtualna SQL](./media/contoso-migration-rehost-vm-sql-ag/sql-vm-db.png)

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
3. Umieszczają one konto w trzecim regionie: Południowo-środkowe stany USA. Znajdują się one poza regionem podstawowym i pomocniczym, dzięki czemu będzie on dostępny podczas awarii regionalnej.
4. Umieszczają je w grupie zasobów **ContosoInfraRG**, która zawiera zasoby infrastruktury.

    ![Monitor w chmurze](./media/contoso-migration-rehost-vm-sql-ag/witness-storage.png)

5. Po utworzeniu konta magazynu są generowane powiązane z nim podstawowe i pomocnicze klucze dostępu. Do utworzenia monitora chmury jest potrzebny podstawowy klucz dostępu. Klucz zostanie wyświetlony w obszarze nazwy konta magazynu > **Klucze dostępu**.

    ![Klucz dostępu](./media/contoso-migration-rehost-vm-sql-ag/access-key.png)

### <a name="add-sql-server-vms-to-contoso-domain"></a>Dodawanie maszyn wirtualnych z programem SQL Server do domeny firmy Contoso

1. Firma Contoso dodaje maszyny SQLAOG1 i SQLAOG2 do domeny contoso.com.
2. Następnie na każdej maszynie wirtualnej administratorzy instalują funkcję i narzędzia klastra trybu failover systemu Windows.

### <a name="set-up-the-cluster"></a>Konfigurowanie klastra

Przed skonfigurowaniem klastra administratorzy firmy Contoso tworzą migawkę dysku systemu operacyjnego na każdej maszynie.

![Tworzenie migawki](./media/contoso-migration-rehost-vm-sql-ag/snapshot.png)

1. Następnie uruchamiają przygotowany skrypt, aby utworzyć klaster trybu failover systemu Windows.

    ![Tworzenie klastra](./media/contoso-migration-rehost-vm-sql-ag/create-cluster1.png)

2. Po utworzeniu klastra sprawdzają, czy maszyny wirtualne są widoczne jako węzły klastra.

     ![Tworzenie klastra](./media/contoso-migration-rehost-vm-sql-ag/create-cluster2.png)

### <a name="configure-the-cloud-witness"></a>Konfigurowanie monitora w chmurze

1. Administratorzy firmy Contoso konfigurują monitor w chmurze za pomocą **kreatora konfiguracji kworum** w Menedżerze klastra trybu failover.
2. W Kreatorze wybierają opcję utworzenia monitora chmury z kontem magazynu.
3. Skonfigurowany monitor w chmurze jest wyświetlany w przystawce Menedżer klastra trybu failover.

    ![Monitor w chmurze](./media/contoso-migration-rehost-vm-sql-ag/cloud-witness.png)

### <a name="enable-sql-server-always-on-availability-groups"></a>Włączanie zawsze włączonych grup dostępności programu SQL Server

Administratorzy firmy Contoso mogą teraz włączyć rozwiązanie Zawsze włączone:

1. W programie SQL Server Configuration Manager włączają **zawsze włączone grupy dostępności** dla usługi **SQL Server (MSSQLSERVER)**.

    ![Włączanie rozwiązania Zawsze włączone](./media/contoso-migration-rehost-vm-sql-ag/enable-always-on.png)

2. Ponownie uruchamiają usługę, aby zmiany zaczęły obowiązywać.

Po włączeniu rozwiązania Zawsze włączone firma Contoso może skonfigurować zawsze włączoną grupę dostępności, która będzie chronić bazę danych SmartHotel360.

**Potrzebujesz dodatkowej pomocy?**

- [Przeczytaj informacje](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness) na temat monitora w chmurze i konfigurowania odpowiadającego mu konta magazynu.
- [Uzyskaj instrukcje](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial) dotyczące konfigurowania klastra i tworzenia grupy dostępności.

## <a name="step-3-deploy-the-azure-load-balancer"></a>Krok 3. wdrażanie Azure Load Balancer

Administratorzy firmy Contoso chcą teraz wdrożyć wewnętrzny moduł równoważenia obciążenia, który znajduje się przed węzłami klastra. Moduł równoważenia obciążenia nasłuchuje ruchu i kieruje go do odpowiedniego węzła.

![Równoważenie obciążenia](./media/contoso-migration-rehost-vm-sql-ag/architecture-lb.png)

Tworzą moduł równoważenia obciążenia w następujący sposób:

1. W Load Balancer Azure Portal > **Networking**  >  **Load Balancer**skonfiguruje nowy wewnętrzny moduł równoważenia obciążenia: **ILB-prod-DB-EUS2-SQLAOG**.
2. Umieszczają moduł równoważenia obciążenia w sieci produkcyjnej **VNET-PROD-EUS2** w podsieci **PROD-DB-EUS2**.
3. Przypisują mu statyczny adres IP: 10.245.40.100.
4. Jako element sieci wdrażają moduł równoważenia obciążenia w grupie zasobów sieciowych **ContosoNetworkingRG**.

    ![Równoważenie obciążenia](./media/contoso-migration-rehost-vm-sql-ag/lb-create.png)

Po wdrożeniu wewnętrznego modułu równoważenia obciążenia muszą go skonfigurować. Tworzą one pulę adresów zaplecza, konfiguruje sondę kondycji i konfiguruje regułę równoważenia obciążenia.

### <a name="add-a-back-end-pool"></a>Dodawanie puli zaplecza

Aby dystrybuować ruch do maszyn wirtualnych w klastrze, administratorzy firmy Contoso konfigurują pulę adresów zaplecza zawierającą adresy IP kart sieciowych dla maszyn wirtualnych, które będą odbierać ruch sieciowy z modułu równoważenia obciążenia.

1. W ustawieniach usługi równoważenia obciążenia w portalu firma Contoso dodaje pulę zaplecza: **ILB-prod-DB-EUS-SQLAOG-BEPOOL**.
2. Kojarzą pulę z zestawem dostępności SQLAOGAVSET. Maszyny wirtualne w zestawie (**SQLAOG1** i **SQLAOG2**) są dodawane do puli.

    ![Pula zaplecza](./media/contoso-migration-rehost-vm-sql-ag/backend-pool.png)

### <a name="create-a-health-probe"></a>Tworzenie sondy kondycji

Administratorzy firmy Contoso tworzą sondę kondycji, aby moduł równoważenia obciążenia mógł monitorować kondycję aplikacji. Sonda dynamicznie dodaje lub usuwa maszyny wirtualne z rotacji modułu równoważenia obciążenia na podstawie ich odpowiedzi na kontrole kondycji.

Tworzą sondę w następujący sposób:

1. W ustawieniach usługi równoważenia obciążenia w portalu firma Contoso tworzy sondę kondycji: **SQLAlwaysOnEndPointProbe**.
2. Ustawiają sondę tak, aby monitorowała maszyny wirtualne na porcie TCP 59999.
3. Ustawiają interwał wynoszący 5 sekund między sondami oraz próg wynoszący 2. Jeśli dwie sondy zakończą się niepowodzeniem, kondycja maszyny wirtualnej zostanie uznana za złą.

    ![Sonda](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

### <a name="configure-the-load-balancer-to-receive-traffic"></a>Konfigurowanie modułu równoważenia obciążenia do odbierania ruchu

Teraz administratorzy firmy Contoso konfigurują regułę modułu równoważenia obciążenia, aby zdefiniować sposób dystrybucji ruchu do maszyn wirtualnych.

- Adres IP frontonu obsługuje ruch przychodzący.
- Pula adresów IP zaplecza odbiera ruch.

Tworzą regułę w następujący sposób:

1. W ustawieniach usługi równoważenia obciążenia w portalu dodaje nową regułę: **SQLAlwaysOnEndPointListener**.
2. Ustawiają odbiornik frontonu tak, aby odbierał przychodzący ruch klienta SQL na porcie 1433 protokołu TCP.
3. Określają pulę zaplecza, do której będzie kierowany ruch, oraz port, na którym maszyny wirtualne nasłuchują ruchu.
4. Włączają zmienny adres IP (bezpośredni zwrot serwera). Jest to zawsze wymagane w przypadku rozwiązania Zawsze włączone programu SQL.

    ![Sonda](./media/contoso-migration-rehost-vm-sql-ag/nlb-probe.png)

**Potrzebujesz dodatkowej pomocy?**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) usługi Azure Load Balancer.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/load-balancer/tutorial-load-balancer-basic-internal-portal) na temat tworzenia modułu równoważenia obciążenia.

## <a name="step-4-prepare-azure-for-azure-migrate"></a>Krok 4. Przygotowywanie platformy Azure dla Azure Migrate

Oto składniki platformy Azure, które firma Contoso potrzebuje do wdrożenia Azure Migrate:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne, gdy zostaną utworzone podczas przełączenia w tryb failover.
- Konto magazynu platformy Azure do przechowywania replikowanych danych.

Administratorzy firmy Contoso konfigurują te składniki w następujący sposób:

1. Firma Contoso utworzyła już sieć/podsieć, z której mogą korzystać Azure Migrate podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-rehost-vm-sql-ag.md).

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyna wirtualna WEBVM zostanie zmigrowana do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie podstawowym Wschodnie stany USA 2.
    - Maszyna wirtualna WEBVM zostanie umieszczona w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych, oraz w podsieci produkcyjnej (PROD-FE-EUS2).

2. Administratorzy firmy Contoso tworzą konto usługi Azure Storage (contosovmsacc20180528) w regionie podstawowym.

    - Administratorzy używają konta ogólnego przeznaczenia w warstwie Standard z replikacją LRS.

## <a name="step-5-prepare-on-premises-vmware-for-azure-migrate"></a>Krok 5. Przygotowanie lokalnego programu VMware do Azure Migrate

Oto co administratorzy firmy Contoso przygotowują w środowisku lokalnym:

- Konto na serwerze vCenter lub hoście vSphere ESXi w celu zautomatyzowania odnajdowania maszyn wirtualnych.
- Ustawienia lokalnej maszyny wirtualnej, aby firma Contoso mogła połączyć się z replikowaną maszyną wirtualną platformy Azure po przejściu w tryb failover.

### <a name="prepare-an-account-for-automatic-discovery"></a>Przygotowywanie konta do automatycznego odnajdowania

Azure Migrate potrzebuje dostępu do serwerów VMware, aby:

- Automatyczne odnajdywanie maszyn wirtualnych.
- Organizowanie replikacji, trybu failover i powrotu po awarii.
- Wymagane jest co najmniej konto tylko do odczytu. Potrzebne jest konto, na którym można uruchamiać operacje takie jak tworzenie i usuwanie dysków, a także włączanie maszyn wirtualnych.

Administratorzy firmy Contoso konfigurują to konto w następujący sposób:

1. Tworzą rolę na poziomie serwera vCenter.
2. Następnie przypisują do tej roli wymagane uprawnienia.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po migracji firma Contoso chce nawiązać połączenie z maszynami wirtualnymi platformy Azure i umożliwić platformie Azure zarządzanie maszynami wirtualnymi. W tym celu administratorzy firmy Contoso wykonują następujące czynności przed migracją:

1. W celu uzyskania dostępu przez Internet:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Upewniają się, że zostały dodane reguły TCP i UDP dla profilu **publicznego**.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.

2. W celu uzyskania dostępu przez sieć VPN lokacja-lokacja:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.
    - Dla systemu Windows Ustaw zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na **OnlineAll**.

3. Zainstaluj agenta platformy Azure:

    - [Agent systemu Linux platformy Azure](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux)
    - [Agent systemu Windows Azure](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-windows)

4. Różne

   - W przypadku systemu Windows na maszynie wirtualnej nie ma żadnych oczekujących aktualizacji podczas wyzwalania migracji. W przeciwnym razie nie będzie można zalogować się na maszynie wirtualnej do momentu ukończenia aktualizacji.
   - Po migracji można sprawdzić **diagnostykę rozruchu** , aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli to nie zadziała, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

5. Potrzebujesz dodatkowej pomocy?

   - [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) przygotowywaniu maszyn wirtualnych do migracji.

## <a name="step-6-replicate-the-on-premises-vms-to-azure"></a>Krok 6. replikowanie lokalnych maszyn wirtualnych na platformę Azure

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

Po ukończeniu odnajdywania można rozpocząć replikację maszyn wirtualnych VMware na platformę Azure.

1. Na **serwerach**Azure Migrate project > **Azure Migrate: Migracja serwera**, kliknij przycisk **replikacja**.

    ![Replikowanie maszyn wirtualnych](./media/contoso-migration-rehost-vm/select-replicate.png)

2. W obszarze **Replikacja** > **Ustawienia źródła** > **Czy maszyny są zwirtualizowane** wybierz pozycję **Tak, z funkcją VMware vSphere Hypervisor**.

3. W obszarze **Urządzenie lokalne** wybierz nazwę skonfigurowanego urządzenia usługi Azure Migrate > przycisk **OK**.

    ![Ustawienia źródła](./media/contoso-migration-rehost-vm/source-settings.png)

4. W obszarze **Maszyny wirtualne** wybierz maszyny wirtualne, które mają być replikowane.
    - Jeśli przeprowadzasz ocenę dla maszyn wirtualnych, możesz zastosować rekomendacje dotyczące rozmiarów maszyn wirtualnych i typów dysków (Premium/standardowy) w wynikach oceny. W tym celu w obszarze **Zaimportować ustawienia migracji z oceny usługi Azure Migrate?** wybierz opcję **Tak**.
    - Jeśli nie uruchomiono oceny lub nie chcesz używać ustawień oceny, wybierz opcję **Nie**.
    - W przypadku wybrania opcji korzystania z oceny wybierz grupę maszyn wirtualnych i nazwę oceny.

    ![Wybieranie oceny](./media/contoso-migration-rehost-vm/select-assessment.png)

5. W obszarze **Maszyny wirtualne** wyszukaj potrzebne maszyny wirtualne i sprawdź każdą maszynę wirtualną, którą chcesz migrować. Następnie kliknij przycisk **Dalej: ustawienia docelowe**.

6. W obszarze **Ustawienia elementu docelowego** wybierz subskrypcję i docelowy region migracji, a następnie określ grupę zasobów, w której będą znajdować się maszyny wirtualne platformy Azure po migracji. W obszarze **Sieć wirtualna** wybierz sieć wirtualną/podsieć platformy Azure, do której zostaną dołączone maszyny wirtualne platformy Azure po migracji.

7. W **korzyść użycia hybrydowego platformy Azure**wybierz następujące opcje:

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie kliknij przycisk **Dalej**.
    - Wybierz opcję **Tak**, jeśli masz maszyny z systemem Windows Server, które są objęte aktywnym programem Software Assurance lub subskrypcjami systemu Windows Server, i chcesz zastosować korzyść do migrowanych maszyn. Następnie kliknij przycisk **Dalej**.

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

## <a name="step-7-migrate-the-database-with-azure-database-migration-service-dms"></a>Krok 7. Migrowanie bazy danych za pomocą Azure Database Migration Service (DMS)

Administratorzy firmy Contoso dokonują migracji przy użyciu usług Azure Database Migration Services (DMS) przy użyciu [samouczka migracji krok po kroku](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online). Mogą wykonywać migracje w trybie online, offline i hybrydowym (wersja zapoznawcza).

Podsumowując, należy wykonać następujące czynności:

- Utwórz Azure Database Migration Service (DMS) z jednostką `Premium` SKU, która jest połączona z siecią wirtualną.
- Upewnij się, że Azure Database Migration Service (DMS) może uzyskać dostęp do SQL Server zdalnego za pośrednictwem sieci wirtualnej. Dzięki temu można upewnić się, że wszystkie porty przychodzące są dozwolone z platformy Azure do SQL Server na poziomie sieci wirtualnej, sieci VPN sieciowej i na komputerze, który hostuje SQL Server.
- Skonfiguruj Azure Database Migration Service:
  - Utwórz projekt migracji.
  - Dodaj źródło (lokalna baza danych).
  - Wybierz element docelowy.
  - Wybierz bazy danych do migracji.
  - Skonfiguruj ustawienia zaawansowane.
  - Rozpocznij replikację.
  - Usuń wszelkie błędy.
  - Wykonaj ostateczną uruchomienie produkcyjne.

## <a name="step-8-protect-the-database-with-always-on"></a>Krok 8. Ochrona bazy danych zawsze włączona

W przypadku bazy danych aplikacji działającej na maszynie wirtualnej **SQLAOG1** administratorzy firmy Contoso mogą teraz chronić ją przy użyciu zawsze włączonych grup dostępności. Konfigurują rozwiązanie Zawsze włączone przy użyciu programu SQL Management Studio, a następnie przypisują odbiornik przy użyciu klastrowania systemu Windows.

### <a name="create-an-always-on-availability-group"></a>Tworzenie zawsze włączonej grupy dostępności

1. W programie SQL Management Studio klikają prawym przyciskiem myszy pozycję **Always on High Availability** (Zawsze włączona wysoka dostępność), aby uruchomić kreatora **New Availability Group Wizard** (Kreator nowej grupy dostępności).
2. W obszarze **Specify Options** (Określanie opcji) nadają grupie dostępności nazwę **SHAOG**. W obszarze **Select Database** (Wybieranie bazy danych) wybierają bazę danych SmartHotel360.

    ![Zawsze włączona grupa dostępności](./media/contoso-migration-rehost-vm-sql-ag/aog-1.png)

3. W obszarze **Specify Replicas** (Określanie replik) dodają dwa węzły SQL jako repliki dostępności, a następnie konfigurują je w celu zapewnienia automatycznego przejścia w tryb failover z zatwierdzaniem synchronicznym.

     ![Zawsze włączona grupa dostępności](./media/contoso-migration-rehost-vm-sql-ag/aog-2.png)

4. Konfigurują odbiornik dla grupy (**SHAOG**) i port. Adres IP wewnętrznego modułu równoważenia obciążenia jest dodawany jako statyczny adres IP (10.245.40.100).

    ![Zawsze włączona grupa dostępności](./media/contoso-migration-rehost-vm-sql-ag/aog-3.png)

5. W obszarze **Select Data Synchronization** (Wybieranie synchronizacji danych) włączają automatyczne rozmieszczanie. W przypadku tej opcji program SQL Server automatycznie tworzy repliki pomocnicze dla każdej bazy danych w grupie, więc firma Contoso nie musi ręcznie tworzyć kopii zapasowych ani ich przywracać. Po zakończeniu walidacji zostanie utworzona grupa dostępności.

    ![Zawsze włączona grupa dostępności](./media/contoso-migration-rehost-vm-sql-ag/aog-4.png)

6. Firma Contoso napotkała problem podczas tworzenia grupy. Administratorzy nie używają zintegrowanych zabezpieczeń systemu Windows i dlatego muszą udzielić uprawnień do logowania SQL w celu utworzenia ról klastra trybu failover systemu Windows.

    ![Zawsze włączona grupa dostępności](./media/contoso-migration-rehost-vm-sql-ag/aog-5.png)

7. Po utworzeniu grupy firma Contoso może ją zobaczyć w programie SQL Management Studio.

### <a name="configure-a-listener-on-the-cluster"></a>Konfigurowanie odbiornika w klastrze

W ramach ostatniego kroku konfigurowania wdrożenia SQL administratorzy firmy Contoso konfigurują wewnętrzny moduł równoważenia obciążenia jako odbiornik w klastrze i przenoszą odbiornik do trybu online. W tym celu używają skryptu.

![Odbiornik klastra](./media/contoso-migration-rehost-vm-sql-ag/cluster-listener.png)

### <a name="verify-the-configuration"></a>Sprawdzanie konfiguracji

Po skonfigurowaniu wszystkich elementów firma Contoso ma teraz działającą grupę dostępności na platformie Azure, która korzysta z migrowanej bazy danych. Administratorzy sprawdzają to, łącząc się z wewnętrznym modułem równoważenia obciążenia w programie SQL Management Studio.

![Połączenie z wewnętrznym modułem równoważenia obciążenia](./media/contoso-migration-rehost-vm-sql-ag/ilb-connect.png)

**Potrzebujesz dodatkowej pomocy?**

- Dowiedz się więcej na temat [grupy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#create-the-availability-group) i [odbiornika](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-tutorial#configure-listener).
- Ręcznie [skonfiguruj klaster tak, aby używał adresu IP modułu równoważenia obciążenia](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#configure-the-cluster-to-use-the-load-balancer-ip-address).
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2) na temat tworzenia i używania sygnatur dostępu współdzielonego.

## <a name="step-9-migrate-the-vm-with-azure-migrate"></a>Krok 9. Migrowanie maszyny wirtualnej za pomocą Azure Migrate

Administratorzy firmy Contoso uruchamiają szybki test przejścia do trybu failover, a następnie przeprowadzają migrację maszyny wirtualnej.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Próba przejścia do trybu failover pozwala sprawdzić, czy wszystko działa zgodnie z oczekiwaniami, przed przeprowadzeniem faktycznej migracji.

1. Administratorzy uruchamiają próbę przejścia do trybu failover przy użyciu najnowszego dostępnego punktu w czasie (**Najnowszy przetworzony**).
2. Wybierają opcję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**, dzięki czemu Azure Migrate próbuje zamknąć ŹRÓDŁową maszynę wirtualną przed wyzwoleniem trybu failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się.
3. Próbne przełączenia do trybu failover:

    - Uruchamiane jest sprawdzanie wymagań wstępnych, aby upewnić się, że zostały spełnione wszystkie warunki migracji.
    - Tryb failover przetwarza dane, aby umożliwić utworzenie maszyny wirtualnej platformy Azure. W przypadku wybrania najnowszego punktu odzyskiwania zostanie utworzony punkt odzyskiwania z danych.
    - Tworzona jest maszyna wirtualna platformy Azure przy użyciu danych przetworzonych w poprzednim kroku.

4. Po zakończeniu przechodzenia w tryb failover w witrynie Azure Portal będzie widoczna replika maszyny wirtualnej na platformie Azure. Administratorzy sprawdzają, czy maszyna wirtualna ma prawidłowy rozmiar, jest połączona z odpowiednią siecią i jest uruchomiona.
5. Gdy wszystko zostanie sprawdzone, przeprowadzają czyszczenie po przejściu do trybu failover oraz rejestrują i zapisują wszelkie obserwacje.

### <a name="run-a-failover"></a>Uruchamianie trybu failover

1. Jeśli próbne przejście do trybu failover przebiegło zgodnie z oczekiwaniami, administratorzy firmy Contoso mogą utworzyć plan odzyskiwania na potrzeby migracji i dodać maszynę wirtualną WEBVM do planu.

     ![Plan odzyskiwania](./media/contoso-migration-rehost-vm-sql-ag/recovery-plan.png)

2. Uruchamiają tryb failover z użyciem utworzonego planu. Wybierają one najnowszy punkt odzyskiwania i określają, że Azure Migrate powinna próbować zamknąć lokalną maszynę wirtualną przed wyzwoleniem trybu failover.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover1.png)

3. Po przejściu w tryb failover administratorzy sprawdzają, czy maszyna wirtualna platformy Azure jest widoczna zgodnie z oczekiwaniami w witrynie Azure Portal.

    ![Plan odzyskiwania](./media/contoso-migration-rehost-vm-sql-ag/failover2.png)

4. Po sprawdzeniu maszyny wirtualnej na platformie Azure ukończą migrację, aby zakończyć proces migracji, zatrzymać replikację maszyny wirtualnej i zatrzymać Azure Migrate rozliczenia dla maszyny wirtualnej.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover3.png)

### <a name="update-the-connection-string"></a>Aktualizowanie parametrów połączenia

W ostatnim kroku procesu migracji administratorzy firmy Contoso aktualizują parametry połączenia aplikacji tak, aby wskazywały migrowaną bazę danych działającą na odbiorniku SHAOG. Ta konfiguracja zostanie zmieniona na maszynie wirtualnej WEBVM działającej obecnie na platformie Azure. Ta konfiguracja znajduje się w pliku web.config aplikacji ASP.

1. Znajdź plik w lokalizacji `C:\inetpub\SmartHotelWeb\web.config` . Zmień nazwę serwera w celu odzwierciedlenia nazwy FQDN odbiornika AOG: shaog.contoso.com.

    ![Tryb failover](./media/contoso-migration-rehost-vm-sql-ag/failover4.png)

2. Po zaktualizowaniu pliku i zapisaniu go ponownie uruchamiają usługi IIS na maszynie wirtualnej WEBVM. Są one używane `iisreset /restart` z poziomu wiersza polecenia.
3. Po ponownym uruchomieniu usług IIS aplikacja korzysta teraz z bazy danych działającej w programie SQL MI.

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) o próbnym uruchamianiu trybu failover.
- [Dowiedz się](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans), jak utworzyć plan odzyskiwania.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) na temat przechodzenia w tryb failover na platformie Azure.

### <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po migracji aplikacja SmartHotel360 działa na maszynie wirtualnej platformy Azure, a baza danych SmartHotel360 znajduje się w klastrze usług SQL Azure.

Teraz firma Contoso musi wykonać następujące kroki dotyczące czyszczenia:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie dokumentacji wewnętrznej tak, aby wyświetlić nowe lokalizacje i adresy IP maszyn wirtualnych.
- Przegląd wszystkich zasobów korzystających ze zlikwidowanych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Dodanie dwóch nowych maszyn wirtualnych (SQLAOG1 i SQLAOG2) do systemów monitorowania produkcji.

### <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso sprawdza maszyny wirtualne platformy Azure WEBVM, SQLAOG1 and SQLAOG2, aby określić problemy z zabezpieczeniami.

- Zespół przegląda sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyny wirtualnej. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Zespół rozważa zabezpieczenie danych na dysku przy użyciu usług Azure Disk Encryption i Key Vault.
- Zespół powinien oszacować szyfrowanie Transparent Data Encryption (TDE), a następnie włączyć je w bazie danych SmartHotel360 działającej na nowym odbiorniku AOG SQL. [Dowiedz się więcej](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017).

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania w zakresie zabezpieczeń dotyczące obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

## <a name="business-continuity-and-disaster-recovery"></a>Ciągłość działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Aby zapewnić bezpieczeństwo danych, firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych WEBVM, SQLAOG1 i SQLAOG2 za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-overview).
- Firma Contoso sprawdza również, jak używać usługi Azure Storage do tworzenia kopii zapasowych programu SQL Server bezpośrednio do magazynu obiektów blob. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-use-storage-sql-server-backup-restore).
- Aby zachować działanie aplikacji, firma Contoso replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Firma Contoso ma istniejące licencje dla maszyny wirtualnej WEBVM i zastosuje korzyść użycia hybrydowego platformy Azure. Firma Contoso przekonwertuje istniejące maszyny wirtualne platformy Azure, aby skorzystać z tych cen.
- Firma Contoso będzie używać [Azure Cost Management](https://azure.microsoft.com/services/cost-management) , aby zapewnić, że pozostają w ramach budżetów ustanowionych przez ich lidera.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przehostuje aplikację SmartHotel360 na platformie Azure przez migrację maszyny wirtualnej frontonu aplikacji na platformę Azure przy użyciu usługi Azure Migrate. Firma Contoso migruje bazę danych aplikacji do klastra SQL Server obsługiwanego na platformie Azure przy użyciu Azure Database Migration Service i chronił ją w SQL Server zawsze włączone grupy dostępności.
