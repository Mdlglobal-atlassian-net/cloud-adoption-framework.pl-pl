---
title: Refaktoryzacja aplikacji przez Migrowanie jej do Azure App Service i Azure SQL Database wystąpienia zarządzanego
description: Dowiedz się, w jaki sposób firma Contoso rehostuje aplikację lokalną przez Migrowanie jej do Azure App Service aplikacji sieci Web i Azure SQL Database wystąpienia zarządzanego.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: fd8c7e81d457ee3a63186217fda72223272ad3b7
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83815263"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc smarthotel SQLMI SHWCF SHWEB -->

# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-managed-instance"></a>Refaktoryzacja aplikacji lokalnej do Azure App Service aplikacji sieci Web i wystąpienia zarządzanego Azure SQL

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso refaktoryzuje dwuwarstwową aplikację platformy .NET w systemie Windows działającą na maszynach wirtualnych VMware w ramach migracji na platformę Azure. Migrujemy maszynę wirtualną aplikacji frontonu do aplikacji sieci Web Azure App Service. Pokazano również, jak firma Contoso migruje bazę danych aplikacji do wystąpienia zarządzanego usługi Azure SQL Database.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się i następuje przeciążenie lokalnych systemów i infrastruktury.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.**  Dział IT firmy Contoso chce lepiej odpowiadać na zapotrzebowania biznesowe. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Zasięgu.** W miarę pomyślnego rozwoju firmy dział IT firmy Contoso musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.
- **Obniżyć koszty.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Aplikacja** | Aplikacja na platformie Azure będzie miała nadal krytyczne znaczenie dla działania firmy, tak jak dzisiaj. <br><br> Powinna ona mieć takie same możliwości związane z wydajnością, jak w przypadku programu VMware. <br><br> Zespół nie chce inwestować w aplikację. Na razie administratorzy będą po prostu bezpiecznie przenosić aplikację do chmury. <br><br> Zespół chce przestać obsługiwać system Windows Server 2008 R2, w którym aktualnie działa aplikacja. <br><br> Zespół chce również przejść z programu SQL Server 2008 R2 do nowoczesnej platformy bazy danych PaaS, która zminimalizuje potrzebę zarządzania. <br><br> Firma Contoso chce skorzystać z inwestycji w licencjonowanie programu SQL Server Licencjonowanie i pakiet Software Assurance, o ile jest to możliwe. <br><br> Ponadto firma Contoso chce wyeliminować pojedynczy punkt awarii w warstwie internetowej.
**Ograniczenia** | Aplikacja składa się z aplikacji ASP.NET i usługi WCF uruchomionej na tej samej maszynie wirtualnej. Ma ona zostać podzielona na dwie aplikacje internetowe przy użyciu usługi Azure App Service.
**Azure** | Firma Contoso chce przenieść aplikację na platformę Azure, ale nie chce jej uruchamiać na maszynach wirtualnych. Firma Contoso chce korzystać z usług Azure w warstwie internetowej i warstwie danych.
**DevOps** | Firma Contoso chce przenieść się do modelu metodyki DevOps przy użyciu usługi Azure DevOps na potrzeby obsługi kompilacji i potoków wydań.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które będą używane do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja lokalna SmartHotel360 jest podzielona na warstwy, które znajdują się na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Maszyny wirtualne znajdują się na VMware ESXi hosta **contosohost1.contoso.com** (wersja 6,5).
- Środowisko VMware jest zarządzane przez vCenter Server 6,5 (**vCenter.contoso.com**), uruchomione na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-Datacenter) z lokalnym kontrolerem domeny (**ContosoDC1**).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

### <a name="proposed-solution"></a>Proponowane rozwiązanie

- W przypadku warstwy internetowej aplikacji firma Contoso zdecydowała się użyć usługi Azure App Service. Ta usługa PaaS umożliwia wdrożenie aplikacji przy użyciu tylko kilku zmian konfiguracji. Firma Contoso będzie używać programu Visual Studio do wprowadzania zmian i wdrażania dwóch aplikacji internetowych. Jedna z nich będzie związana z witryny internetową, a druga z usługą WCF.
- Aby spełnić wymagania dotyczące potoku DevOps, firma Contoso zabrała usługę Azure DevOps do zarządzania kodem źródłowym przy użyciu repozytoriów Git. Do kompilowania kodu i wdrażania go w usłudze Azure App Service będą używane zautomatyzowane kompilacje i wydania.

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i wystąpienia zarządzanego programu SQL Server. Następujące zagadnienia pomogły w podjęciu decyzji o wybraniu wystąpienia zarządzanego.

- Wystąpienie zarządzane ma na celu zapewnienie niemal 100% zgodności z najnowszą wersją lokalnego programu SQL Server. Firma Microsoft zaleca wystąpienie zarządzane dla klientów z programem SQL Server działającym lokalnie lub na maszynie wirtualnej IaaS, którzy chcą zmigrować swoje aplikacje do w pełni zarządzanej usługi przy minimalnych zmianach projektowych.
- Firma Contoso planuje migrację dużej liczby aplikacji z lokalizacji lokalnej do modelu IaaS. Wiele z nich jest udostępnianych przez niezależnych dostawców oprogramowania. Firma Contoso wie, że korzystanie z wystąpienia zarządzanego pomoże zapewnić zgodność bazy danych dla tych aplikacji, ale nie zapewni tego usługa SQL Database, która może nie być obsługiwana.
- Firma Contoso może po prostu przetworzyć dźwig i przenieść migrację do wystąpienia zarządzanego przy użyciu w pełni zautomatyzowanego Azure Database Migration Service. Firma Contoso może w przyszłości ponownie wykorzystać tę usługę do migracji baz danych.
- Wystąpienie zarządzane SQL obsługuje program SQL Server Agent, co jest ważną kwestią w przypadku aplikacji SmartHotel360. Firma Contoso potrzebuje tej zgodności, ponieważ w przeciwnym razie będzie musiała ponownie zaprojektować plany konserwacji wymagane przez aplikację.
- Dzięki programowi Software Assurance firma Contoso może wymienić swoje istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Dzięki temu firma Contoso może zaoszczędzić do 30% na wystąpieniu zarządzanym.
- Wystąpienie zarządzane SQL jest w pełni zawarte w sieci wirtualnej, dzięki czemu zapewnia większą izolację i bezpieczeństwo danych firmy Contoso. Firma Contoso może korzystać z zalet chmury publicznej, jednocześnie zapewniając izolację środowiska od publicznego Internetu.
- Wystąpienie zarządzane obsługuje wiele funkcji zabezpieczeń, w tym Always Encrypted, dynamiczne maskowanie danych, zabezpieczenia na poziomie wiersza i wykrywanie zagrożeń.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Nie trzeba zmieniać kodu aplikacji SmartHotel360 w celu przeprowadzenia migracji na platformę Azure. <br><br> Firma Contoso może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server. <br><br> Po migracji obsługa systemu Windows Server 2008 R2 nie będzie konieczna. Aby uzyskać więcej informacji, zobacz [Zasady cyklu życia firmy Microsoft](https://aka.ms/lifecycle). <br><br> Firma Contoso może skonfigurować warstwę internetową aplikacji z wieloma wystąpieniami, dzięki czemu nie będzie ona już pojedynczym punktem awarii. <br><br> Baza danych nie będzie już zależeć od wieku programu SQL Server 2008 R2. <br><br> Wystąpienie zarządzane SQL spełnia wymagania techniczne i cele firmy Contoso. <br><br> Wystąpienie zarządzane zapewni 100-procentową zgodność z bieżącym wdrożeniem przy jednoczesnym zaprzestaniu korzystania z programu SQL Server 2008 R2. <br><br> Firma może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server. <br><br> Może ponownie użyć usługi Azure Database Migration Service na potrzeby dodatkowych przyszłych migracji. <br><br> Wystąpienie zarządzane SQL ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi konfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Usługa Azure App Service obsługuje tylko jedno wdrożenie aplikacji dla każdej aplikacji internetowej. Oznacza to, że należy aprowizować dwie aplikacje internetowe (jedna dla witryny internetowej i druga dla usługi WCF). <br><br> W przypadku warstwy danych wystąpienie zarządzane może nie być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub serwer bazy danych lub jeśli chce uruchamiać aplikacje innych firm wraz z programem SQL Server. Uruchomienie programu SQL Server na maszynie wirtualnej IaaS może zapewnić taką elastyczność.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Proponowana architektura

![Architektura scenariusza](./media/contoso-migration-refactor-web-app-sql-managed-instance/architecture.png)

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso inicjuje Azure SQL Database wystąpienie zarządzane i migruje bazę danych SmartHotel360 do niej przy użyciu Azure Database Migration Service (DMS).
2. Firma Contoso aprowizuje i konfiguruje aplikacje internetowe oraz wdraża do nich aplikację SmartHotel360.

    ![Proces migracji](./media/contoso-migration-refactor-web-app-sql-managed-instance/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Wystąpienie zarządzane usługi Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Wystąpienie zarządzane to usługa zarządzanej bazy danych, która reprezentuje w pełni zarządzane wystąpienie programu SQL Server w chmurze platformy Azure. Używa tego samego kodu co najnowsza wersja aparatu bazy danych programu SQL Server oraz ma najnowsze funkcje, ulepszenia wydajności i poprawki zabezpieczeń. | Korzystanie z wystąpienia zarządzanego usługi SQL Database uruchomionego na platformie Azure powoduje naliczanie opłat zależnych od pojemności. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Tworzenie zaawansowanych aplikacji w chmurze za pomocą w pełni zarządzanej platformy | Koszt oparty na rozmiarze, lokalizacji i czasie użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/what-is-azure-pipelines) | Zapewnia potok ciągłej integracji i ciągłego wdrażania (CI/CD) na potrzeby tworzenia aplikacji. Potok rozpoczyna się od repozytorium Git na potrzeby zarządzania kodem aplikacji, systemu kompilacji na potrzeby produkcji pakietów i innych artefaktów kompilacji oraz systemu zarządzania wydaniami na potrzeby wdrażania zmian w środowiskach deweloperskich, testowych i produkcyjnych.

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do uruchomienia tego scenariusza:

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial). <br><br> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje. <br><br> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Konfigurowanie SQL Database wystąpienia zarządzanego.** Firma Contoso potrzebuje istniejącego wystąpienia zarządzanego, do którego zostanie zmigrowana lokalna baza danych programu SQL Server.
> - **Krok 2: Migrowanie z Azure Database Migration Service (DMS).** Firma Contoso migruje bazę danych aplikacji za pomocą usługi Azure Data Migration Service.
> - **Krok 3. udostępnianie aplikacji sieci Web.** Firma Contoso aprowizuje dwie aplikacje internetowe.
> - **Krok 4. Konfigurowanie usługi Azure DevOps.** Firma Contoso tworzy nowy projekt usługi Azure DevOps i importuje repozytorium usługi Git.
> - **Krok 5. Konfigurowanie parametrów połączenia.** Firma Contoso konfiguruje parametry połączenia tak, aby aplikacja internetowa warstwy internetowej, aplikacja internetowa usługi WCF i wystąpienie programu SQL mogły się komunikować.
> - **Krok 6. Konfigurowanie potoków kompilacji i wydania.** W ostatnim kroku firma Contoso konfiguruje potoki kompilowania i wydawania, aby utworzyć aplikację, i wdraża je w dwóch oddzielnych aplikacjach sieci Web.

## <a name="step-1-set-up-a-sql-database-managed-instance"></a>Krok 1. Konfigurowanie SQL Database wystąpienia zarządzanego

Aby skonfigurować wystąpienie zarządzane usługi Azure SQL Database, firma Contoso musi mieć podsieć, która spełnia następujące wymagania:

- Podsieć musi być dedykowana. Musi być pusta i nie może zawierać żadnej innej usługi w chmurze. Podsieć nie może być podsiecią bramy.
- Po utworzeniu wystąpienia zarządzanego firma Contoso nie powinna dodawać zasobów do tej podsieci.
- Z podsiecią nie może być skojarzona żadna sieciowa grupa zabezpieczeń.
- Podsieć musi mieć zdefiniowaną przez użytkownika tabelę tras. Jedyną przypisaną trasą powinna być 0.0.0.0/0 z następnym przeskokiem do Internetu.
- Jeśli dla sieci wirtualnej określono opcjonalny niestandardowy serwer DNS, wirtualny adres IP `168.63.129.16` dla tłumaczeń cyklicznych na platformie Azure musi być dodany do listy. Dowiedz się, jak [skonfigurować niestandardowy serwer DNS dla Azure SQL Database wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- Z podsiecią nie może być skojarzony żaden punkt końcowy usługi (magazyn lub SQL). Punkty końcowe usługi powinny być wyłączone w sieci wirtualnej.
- Podsieć musi mieć co najmniej 16 adresów IP. Dowiedz się, jak [zmienić rozmiar podsieci wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
- W środowisku hybrydowym firmy Contoso wymagane są niestandardowe ustawienia DNS. Firma Contoso skonfiguruje ustawienia DNS, aby używać co najmniej jednego serwera DNS platformy Azure firmy. Dowiedz się więcej o [dostosowywaniu serwerów DNS](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Konfigurowanie sieci wirtualnej dla wystąpienia zarządzanego

Administratorzy firmy Contoso konfigurują sieć wirtualną w następujący sposób:

1. Tworzą nową sieć wirtualną (**VNET-SQLMI-EU2**) w regionie podstawowym Wschodnie stany USA 2. Spowoduje to dodanie sieci wirtualnej do grupy zasobów **ContosoNetworkingRG**.
2. Przypisują przestrzeń adresową 10.235.0.0/24. Dzięki temu zakres nie będzie pokrywał się z innymi sieciami w tym przedsiębiorstwie.
3. Dodają dwie podsieci do sieci:
    - **SQLMI-ds-EUS2** (10.235.0.0.25).
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Ta podsieć służy do dołączania katalogu do wystąpienia zarządzanego.

      ![Wystąpienie zarządzane: tworzenie sieci wirtualnej](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Po wdrożeniu sieci wirtualnej i podsieci sieci są one łączone równorzędnie w następujący sposób:

    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-HUB-EUS2** (sieć wirtualna koncentratora dla regionu Wschodnie stany USA 2),
    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-PROD-EUS2** (sieć produkcyjna).

      ![Komunikacja równorzędna sieci](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Określają niestandardowe ustawienia DNS. Serwer DNS wskazuje najpierw kontrolery domeny platformy Azure firmy Contoso. Serwer DNS platformy Azure jest pomocniczy. Kontrolery domeny platformy Azure firmy Contoso znajdują się w następujących lokalizacjach:

    - Znajduje się w podsieci **prod-DC-EUS2** w sieci produkcyjnej Wschodnie stany USA 2 (**VNET-prod-EUS2**).
    - Adres **CONTOSODC3** : 10.245.42.4.
    - Adres **CONTOSODC4** : 10.245.42.5.
    - Azure DNS resolver: 168.63.129.16.

      ![Serwery DNS sieci](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Potrzebujesz dodatkowej pomocy?**

- Zapoznaj się z omówieniem [wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Dowiedz się, jak [utworzyć sieć wirtualną dla wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-configure-vnet-subnet).
- Dowiedz się, jak [skonfigurować komunikację równorzędną](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Dowiedz się, jak [zaktualizować ustawienia DNS usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services/tutorial-create-instance).

### <a name="set-up-routing"></a>Konfigurowanie routingu

Wystąpienie zarządzane jest umieszczane w prywatnej sieci wirtualnej. Firma Contoso potrzebuje tabeli tras, aby jej sieć wirtualna mogła komunikować się z usługą zarządzania platformy Azure. Jeśli sieć wirtualna nie może komunikować się z usługą, która nią zarządza, ta sieć wirtualna staje się niedostępna.

Firma Contoso bierze pod uwagę następujące czynniki:

- Tabela tras zawiera zestaw reguł (tras), które określają sposób, w jaki pakiety wysyłane z wystąpienia zarządzanego powinny być kierowane w sieci wirtualnej.
- Tabela tras jest skojarzona z podsieciami, w których są wdrażane wystąpienia zarządzane. Każdy pakiet, który opuszcza podsieć, jest obsługiwany na podstawie skojarzonej tabeli tras.
- Podsieć może być skojarzona tylko z jedną tabelą tras.
- Nie ma dodatkowych opłat za tworzenie tabel tras na platformie Microsoft Azure.

 Aby skonfigurować routing, administratorzy firmy Contoso wykonują następujące czynności:

1. Tworzą zdefiniowaną przez użytkownika tabelę tras w grupie zasobów **ContosoNetworkingRG**.

    ![Tabela tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Aby zachować zgodność z wymaganiami wystąpienia zarządzanego, po wdrożeniu tabeli tras(**MIRouteTable**) dodają trasę z prefiksem adresu 0.0.0.0/0. Opcja **Typ następnego przeskoku** jest ustawiana na wartość **Internet**.

    ![Prefiks tabeli tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Kojarzą tabelę tras z podsiecią **SQLMI-DB-EUS2** (w sieci **VNET-SQLMI-EUS2**).

    ![Podsieć tabeli tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [skonfigurować trasy dla wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Tworzenie wystąpienia zarządzanego

Teraz administratorzy firmy Contoso mogą zaaprowizować wystąpienie zarządzane usługi SQL Database:

1. Ponieważ wystąpienie zarządzane obsługuje aplikację biznesową, administratorzy wdrażają je w regionie podstawowym firmy Wschodnie stany USA 2. Dodają wystąpienie zarządzane do grupy zasobów **ContosoRG**.
2. Wybierają warstwę cenową, rozmiar obliczeniowy i magazyn dla wystąpienia. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Wystąpienie zarządzane](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Po wdrożeniu wystąpienia zarządzanego w grupie zasobów **ContosoRG** pojawiają się dwa nowe zasoby:

    - klaster wirtualny na wypadek, gdyby firma Contoso miała wiele wystąpień zarządzanych,
    - wystąpienie zarządzane bazy danych programu SQL Server.

      ![Wystąpienie zarządzane](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [zaaprowizować wystąpienie zarządzane](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-2-migrate-with-azure-database-migration-service-dms"></a>Krok 2. Migrowanie z Azure Database Migration Service (DMS)

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

## <a name="step-3-provision-web-apps"></a>Krok 3. udostępnianie aplikacji sieci Web

Po przeprowadzeniu migracji bazy danych administratorzy firmy Contoso mogą teraz aprowizować dwie aplikacje internetowe.

1. Wybierają pozycję **Aplikacja internetowa** w portalu.

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app1.png)

2. Podają nazwę aplikacji (**SHWEB-EUS2**), wybierają system Windows do jej uruchomienia i umieszczają ją w produkcyjnej grupie zasobów **ContosoRG**. Tworzą nową aplikację internetową i plan usługi Azure App Service.

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app2.png)

3. Po przeprowadzeniu aprowizacji aplikacji internetowej powtarzają proces tworzenia aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**)

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql-managed-instance/web-app3.png)

4. Po zakończeniu przechodzą do adresu aplikacji, aby sprawdzić, czy zostały pomyślnie utworzone.

## <a name="step-4-set-up-azure-devops"></a>Krok 4. Konfigurowanie usługi Azure DevOps

Firma Contoso musi utworzyć infrastrukturę metodyki DevOps i potoki dla aplikacji. W tym celu administratorzy firmy Contoso tworzą nowy projekt DevOps, importują kod, a następnie konfigurują potoki kompilacji i wydania.

1. Na koncie usług Azure DevOps firmy Contoso tworzą nowy projekt (**ContosoSmartHotelRefactor**), a następnie wybierają pozycję **Git** na potrzeby kontroli wersji.

    ![Nowy projekt](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts1.png)

2. Importują repozytorium usługi Git, które aktualnie przechowuje kod aplikacji. Jest ona w [publicznym repozytorium GitHub](https://github.com/Microsoft/SmartHotel360-Registration) i można ją pobrać.

    ![Pobieranie kodu aplikacji](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts2.png)

3. Po zaimportowaniu kodu łączą program Visual Studio z repozytorium i klonują kod przy użyciu programu Team Explorer.

    ![Łączenie z projektem](./media/contoso-migration-refactor-web-app-sql-managed-instance/devops1.png)

4. Po sklonowaniu repozytorium na maszynę deweloperską otwierają plik rozwiązania dla aplikacji. Aplikacja internetowa i usługa WCF mają oddzielne projekty w pliku.

    ![Plik rozwiązania](./media/contoso-migration-refactor-web-app-sql-managed-instance/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Krok 5. Konfigurowanie parametrów połączenia

Administratorzy firmy Contoso muszą upewnić się, że wszystkie aplikacje internetowe i baza danych mogą się komunikować. W tym celu konfigurują parametry połączenia w kodzie i w aplikacjach internetowych.

1. W aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**) > **Ustawienia** > **Ustawienia aplikacji** dodają nowe parametry połączenia o nazwie **DefaultConnection**.
2. Parametry połączenia są pobierane z bazy danych **SmartHotel-Registration** i powinny być aktualizowane przy użyciu prawidłowych poświadczeń.

    ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql-managed-instance/string1.png)

3. Za pomocą programu Visual Studio otwierają projekt **SmartHotel.Registration.wcf** z pliku rozwiązania. Sekcja **connectionStrings** pliku Web. config usługi WCF **SmartHotel. Registration. WCF** powinna zostać zaktualizowana przy użyciu parametrów połączenia.

     ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql-managed-instance/string2.png)

4. Sekcja **klienta** pliku Web. config dla **SmartHotel. Registration. Web** powinna zostać zmieniona, aby wskazywała nową lokalizację usługi WCF. Jest to adres URL aplikacji internetowej WCF, która hostuje punkt końcowy usługi.

    ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql-managed-instance/strings3.png)

5. Po wprowadzeniu zmian w kodzie administratorzy muszą zatwierdzić te zmiany. Przy użyciu rozwiązania Team Explorer w programie Visual Studio przeprowadzają zatwierdzanie i synchronizację.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Krok 6. Konfigurowanie potoków kompilacji i wydania na platformie Azure DevOps

Administratorzy firmy Contoso konfigurują teraz usługę Azure DevOps w celu wykonania procesu kompilowania i wydawania.

1. W usłudze Azure DevOps wybierają pozycję **kompilacja i wydanie**  >  **nowego potoku**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline1.png)

2. Wybierają pozycję **Azure Repos (Git)** i odpowiednie repozytorium.

    ![Usługa Git i repozytorium](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline2.png)

3. W obszarze **Wybierz szablon** wybierają szablon platformy ASP.NET dla kompilacji.

     ![Szablon platformy ASP.NET](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline3.png)

4. Nazwa **ContosoSmartHotelRefactor-ASP.NET-CI** jest używana na potrzeby kompilacji. Wybierają pozycję **Zapisz i dodaj do kolejki**.

     ![Zapisywanie i dodawanie do kolejki](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline4.png)

5. Spowoduje to rozpoczęcie pierwszej kompilacji. Wybierają numer kompilacji, aby obserwować proces. Po zakończeniu mogą zobaczyć opinię o procesie, a następnie wybrać pozycję **Artefakty**, aby przejrzeć wyniki kompilacji.

    ![Przegląd](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline5.png)

6. Folder **Drop** zawiera wyniki kompilacji.

    - Dwa pliki ZIP to pakiety zawierające aplikacje.
    - Te pliki są używane w potoku wydania na potrzeby wdrażania w usłudze Azure App Service.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline6.png)

7. Wybierają **wersje**  >  **+ Nowy potok**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline7.png)

8. Wybierają szablon wdrożenia dla usługi Azure App Service.

    ![Szablon wdrożenia usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline8.png)

9. Nadają potokowi wydania nazwę **ContosoSmartHotel360Refactor** i określają nazwę aplikacji internetowej usługi WCF (SHWCF-EUS2) dla nazwy **etapu**.

    ![Środowisko](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline9.png)

10. W obszarze etapów wybierają opcję **1 zadanie, 1 zadanie podrzędne** w celu skonfigurowania wdrożenia usługi WCF.

    ![Wdrażanie usługi WCF](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline10.png)

11. Sprawdzają, czy subskrypcja została wybrana i autoryzowana, a następnie wybierają **nazwę usługi App Service**.

     ![Wybieranie nazwy usługi App Service](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline11.png)

12. W potoku > **Artefakty** wybierają pozycję **+Dodaj artefakt**, a następnie wybierają opcję kompilowania przy użyciu potoku **ContosoSmarthotel360Refactor**.

     ![Kompilacja](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline12.png)

13. Wybierają ikonę błyskawicy na artefakcie, aby włączyć wyzwalacz ciągłego wdrażania.

     ![Ikona błyskawicy](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline13.png)

14. Wyzwalacz ciągłego wdrażania powinien być ustawiony na wartość **Włączono**.

    ![Ciągłe wdrażanie włączone](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline14.png)

15. Teraz przechodzą z powrotem do etapu obejmującego 1 zadanie i 1 zadanie podrzędne, a następnie wybierają pozycję **Wdróż usługę Azure App Service**.

    ![Wdrażanie usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline15.png)

16. W obszarze **Wybierz plik lub folder** znajdują plik **SmartHotel.Registration.Wcf.zip**, który został utworzony podczas kompilacji, a następnie wybierają pozycję **Zapisz**.

    ![Zapisywanie usługi WCF](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline16.png)

17. Wybierają **etapy potoku**  >  **Stages**, a następnie **dodają** , aby dodać środowisko dla **SHWEB-EUS2**. Wybierają inne wdrożenie usługi Azure App Service.

    ![Dodawanie środowiska](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline17.png)

18. Powtarzają proces, aby opublikować plik aplikacji internetowej (**SmartHotel.Registration.Web.zip**) do odpowiedniej aplikacji internetowej.

    ![Publikowanie aplikacji internetowej](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline18.png)

19. Zapisany potok wydania będzie wyglądać w następujący sposób.

     ![Podsumowanie potoku wydania](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline19.png)

20. Przechodzą z powrotem do **kompilacji**, a następnie wybierają pozycję **Wyzwalacze** > **Włącz ciągłą integrację**. Powoduje to włączenie potoku, gdy zmiany w kodzie zostaną zatwierdzone oraz gdy nastąpi pełna kompilacja i wydanie.

    ![Włączanie ciągłej integracji](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline20.png)

21. Wybierają pozycję **Zapisz i dodaj do kolejki**, aby uruchomić pełny potok. Zostanie wyzwolona nowa kompilacja, która z kolei spowoduje utworzenie pierwszego wydania aplikacji do usługi Azure App Service.

    ![Zapisywanie potoku](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline21.png)

22. Administratorzy firmy Contoso mogą wykonywać kroki procesu potoku kompilowania i wydawania z poziomu usługi Azure DevOps. Po zakończeniu kompilacji rozpocznie się wydanie.

    ![Kompilowanie i wydawanie aplikacji](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline22.png)

23. Po zakończeniu potoku obie lokacje zostały wdrożone i aplikacja działa w trybie online.

    ![Kończenie wydawania](./media/contoso-migration-refactor-web-app-sql-managed-instance/pipeline23.png)

W tym momencie aplikacja została pomyślnie migrowana na platformę Azure.

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po migracji firma Contoso musi wykonać następujące kroki czyszczenia:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie dokumentacji wewnętrznej tak, aby wyświetlić nowe lokalizacje aplikacji SmartHotel360. Pokaż bazę danych jako działającą w wystąpieniu zarządzanym usługi Azure SQL i fronton jako uruchomiony w dwóch aplikacjach sieci Web.
- Przegląd wszystkich zasobów korzystających ze zlikwidowanych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

- Firma Contoso musi upewnić się, że nowa baza danych **SmartHotel-Registration** jest bezpieczna. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- W szczególności firma Contoso powinna zaktualizować aplikacje internetowe tak, aby używały protokołu SSL z certyfikatami.

### <a name="backups"></a>Tworzenie kopii zapasowych

- Firma Contoso musi przejrzeć wymagania dotyczące kopii zapasowej bazy danych wystąpienia zarządzanego Azure SQL. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Firma Contoso musi również zapoznać się z informacjami na temat zarządzania kopiami zapasowymi i operacjami przywracania bazy danych SQL Database. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) o automatycznych kopiach zapasowych.
- Firma Contoso powinna rozważyć wdrożenie grup trybu failover w celu zapewnienia regionalnego przechodzenia bazy danych w tryb failover. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Firma Contoso musi rozważyć wdrożenie aplikacji internetowej w głównym regionie Wschodnie stany USA 2 i Środkowe stany USA w celu uzyskania odporności. Firma Contoso może skonfigurować Traffic Manager, aby zapewnić pracę w trybie failover w przypadku wystąpienia awarii regionalnego.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma Contoso będzie używać [Azure Cost Management](https://azure.microsoft.com/services/cost-management) , aby zapewnić, że pozostają w ramach budżetów ustanowionych przez ich lidera.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła refaktoryzację aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji do dwóch aplikacji internetowych usługi Azure App Service. Baza danych aplikacji została zmigrowana do wystąpienia zarządzanego usługi Azure SQL.
