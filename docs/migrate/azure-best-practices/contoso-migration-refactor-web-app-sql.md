---
title: Refaktoryzowanie aplikacji przez migrowanie jej do usług Azure App Service i Azure SQL Database
description: Dowiedz się, w jaki sposób firma Contoso ponownie hostuje aplikację lokalną przez migrowanie jej do aplikacji internetowej Azure App Service i bazy danych usługi Azure SQL Server.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 35a64b9f42df3737e186d25a43ecad457010607d
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807448"
---
# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Refaktoryzowanie aplikacji lokalnej do aplikacji internetowej Azure App Service i bazy danych Azure SQL Database

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso refaktoryzuje dwuwarstwową aplikację platformy .NET w systemie Windows działającą na maszynach wirtualnych VMware w ramach migracji na platformę Azure. Firma przeprowadza migrację maszyny wirtualnej frontonu aplikacji do aplikacji internetowej Azure App Service i migrację bazy danych aplikacji do bazy danych Azure SQL Database.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Czynniki biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się i następuje przeciążenie lokalnych systemów i infrastruktury.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.**  Dział IT firmy Contoso chce lepiej odpowiadać na zapotrzebowania biznesowe. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę pomyślnego rozwoju firmy dział IT firmy Contoso musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.
- **Redukcja kosztów.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Aplikacja** | Aplikacja na platformie Azure będzie miała nadal krytyczne znaczenie dla działania firmy, tak jak dzisiaj.<br/><br/> Powinna ona mieć takie same możliwości związane z wydajnością, jak w przypadku programu VMware.<br/><br/> Zespół nie chce inwestować w aplikację. Na razie administratorzy będą po prostu bezpiecznie przenosić aplikację do chmury.<br/><br/> Zespół chce przestać obsługiwać system Windows Server 2008 R2, w którym aktualnie działa aplikacja.<br/><br/> Zespół chce również przejść z programu SQL Server 2008 R2 do nowoczesnej platformy bazy danych PaaS, która zminimalizuje potrzebę zarządzania.<br/><br/> Firma Contoso chce skorzystać z inwestycji w licencjonowanie programu SQL Server Licencjonowanie i pakiet Software Assurance, o ile jest to możliwe.<br/><br/> Ponadto firma Contoso chce wyeliminować pojedynczy punkt awarii w warstwie internetowej.
**Ograniczenia** | Aplikacja składa się z aplikacji ASP.NET i usługi WCF działającej na tej samej maszynie wirtualnej. Ma ona zostać podzielona na dwie aplikacje internetowe przy użyciu usługi Azure App Service.
**Azure** | Firma Contoso chce przenieść aplikację na platformę Azure, ale nie chce jej uruchamiać na maszynach wirtualnych. Firma Contoso chce korzystać z usług Azure w warstwie internetowej i warstwie danych.
**DevOps** | Firma Contoso chce przenieść się do modelu metodyki DevOps przy użyciu usługi Azure DevOps na potrzeby obsługi kompilacji i potoków wydań.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które będą używane do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja lokalna SmartHotel360 jest podzielona na warstwy, które znajdują się na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5)
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

### <a name="proposed-solution"></a>Proponowane rozwiązanie

- W przypadku warstwy bazy danych w aplikacji firma Contoso porównała bazę danych Azure SQL Database z programem SQL Server w [tym artykule](https://docs.microsoft.com/azure/sql-database/sql-database-features). Firma Contoso zdecydowała się na zastosowanie bazy danych Azure SQL Database z kilku powodów:
  - Azure SQL Database to usługa zarządzana z relacyjnymi bazami danych. Zapewnia ona przewidywalną wydajność na wielu poziomach usługi z niemal zerową liczbą czynności administracyjnych. Zalety obejmują dynamiczną skalowalność bez przestojów, wbudowaną inteligentną optymalizację oraz globalną skalowalność i dostępność.
  - Firma Contoso może używać lekkiej wersji narzędzia Data Migration Assistant (DMA) do uzyskiwania dostępu do lokalnej bazy danych i migrowania jej do usług SQL Azure.
  - Dzięki pakietowi Software Assurance firma Contoso może wymienić istniejące licencje na obniżone stawki bazy danych SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Może to zapewnić oszczędności do 30%.
  - Baza danych SQL Database udostępnia funkcje zabezpieczeń, takie jak funkcja Always Encrypted, dynamiczne maskowanie danych i zabezpieczenia na poziomie wiersza/wykrywanie zagrożeń.
- W przypadku warstwy internetowej aplikacji firma Contoso zdecydowała się użyć usługi Azure App Service. Ta usługa PaaS umożliwia wdrożenie aplikacji przy użyciu tylko kilku zmian konfiguracji. Firma Contoso będzie używać programu Visual Studio do wprowadzania zmian i wdrażania dwóch aplikacji internetowych. Jedna z nich będzie związana z witryny internetową, a druga z usługą WCF.
- Aby spełnić wymagania stawiane przez potok DevOps, firma Contoso wybrała opcję użycia usługi Azure DevOps i repozytoriów Git do zarządzania kodem źródłowym. Do kompilowania kodu i wdrażania go w usłudze Azure App Service będą używane zautomatyzowane kompilacje i wydania.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Nie trzeba zmieniać kodu aplikacji SmartHotel360 w celu przeprowadzenia migracji na platformę Azure.<br/><br/> Firma Contoso może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server.<br/><br/> Po migracji obsługa systemu Windows Server 2008 R2 nie będzie konieczna. [Dowiedz się więcej](https://support.microsoft.com/lifecycle).<br/><br/> Firma Contoso może skonfigurować warstwę internetową aplikacji z wieloma wystąpieniami, dzięki czemu nie będzie ona już pojedynczym punktem awarii.<br/><br/> Baza danych nie będzie już zależeć od wieku programu SQL Server 2008 R2.<br/><br/> Baza danych SQL Database obsługuje wymagania techniczne. Firma Contoso oceniła lokalną bazę danych przy użyciu narzędzia Data Migration Assistant i stwierdziła, że jest ona zgodna.<br/><br/> Baza danych Azure SQL Database ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi konfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Usługa Azure App Service obsługuje tylko jedno wdrożenie aplikacji dla każdej aplikacji internetowej. Oznacza to, że należy aprowizować dwie aplikacje internetowe (jedna dla witryny internetowej i druga dla usługi WCF).<br/><br/> Jeśli firma Contoso używa Data Migration Assistant zamiast Azure Database Migration Service do migrowania swojej bazy danych, infrastruktura nie będzie gotowa do migrowania baz danych na dużą skalę. Firma Contoso będzie musiała utworzyć inny region, aby zapewnić możliwość przejścia w tryb failover, jeśli region podstawowy będzie niedostępny.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Proponowana architektura

![Architektura scenariusza](media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso aprowizuje wystąpienie usług SQL Azure i migruje do niego bazę danych aplikacji SmartHotel360.
2. Firma Contoso aprowizuje i konfiguruje aplikacje internetowe oraz wdraża do nich aplikację SmartHotel360.

    ![Proces migracji](media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Firma Contoso używa narzędzia DMA do oceny i wykrywania problemów ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych na platformie Azure. Narzędzie DMA ocenia równoważność funkcji między obiektami źródłowymi i docelowymi SQL oraz rekomenduje ulepszenia dotyczące wydajności i niezawodności. | Narzędzie to można pobrać bezpłatnie.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Usługa inteligentnej, w pełni zarządzanej relacyjnej bazy danych w chmurze. | Koszt oparty na funkcjach, przepływności i rozmiarze. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Tworzenie zaawansowanych aplikacji w chmurze za pomocą w pełni zarządzanej platformy | Koszt oparty na rozmiarze, lokalizacji i czasie użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Zapewnia potok ciągłej integracji i ciągłego wdrażania (CI/CD) na potrzeby tworzenia aplikacji. Potok rozpoczyna się od repozytorium Git na potrzeby zarządzania kodem aplikacji, systemu kompilacji na potrzeby produkcji pakietów i innych artefaktów kompilacji oraz systemu zarządzania wydaniami na potrzeby wdrażania zmian w środowiskach deweloperskich, testowych i produkcyjnych.

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do uruchomienia tego scenariusza:

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Inicjowanie obsługi administracyjnej wystąpienia SQL Database na platformie Azure.** Firma Contoso aprowizuje wystąpienie SQL na platformie Azure. Po przeprowadzeniu migracji witryny internetowej na platformę Azure aplikacja internetowa usługi WCF będzie wskazywać to wystąpienie.
> - **Krok 2. Migrowanie bazy danych za pomocą DMA.** Firma Contoso migruje bazę danych aplikacji przy użyciu narzędzia Data Migration Assistant.
> - **Krok 3. udostępnianie aplikacji sieci Web.** Firma Contoso aprowizuje dwie aplikacje internetowe.
> - **Krok 4. Konfigurowanie usługi Azure DevOps.** Firma Contoso tworzy nowy projekt usługi Azure DevOps i importuje repozytorium usługi Git.
> - **Krok 5. Konfigurowanie parametrów połączenia.** Firma Contoso konfiguruje parametry połączenia tak, aby aplikacja internetowa warstwy internetowej, aplikacja internetowa usługi WCF i wystąpienie programu SQL mogły się komunikować.
> - **Krok 6. Konfigurowanie potoków kompilacji i wydania.** W ostatnim kroku firma Contoso konfiguruje potoki kompilowania i wydawania, aby utworzyć aplikację, a następnie wdraża je w dwóch oddzielnych aplikacjach internetowych.

## <a name="step-1-provision-an-azure-sql-database"></a>Krok 1. Inicjowanie obsługi Azure SQL Database

1. Administratorzy firmy Contoso wybierają bazę danych SQL Database na platformie Azure.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Określają nazwę bazy danych odpowiadającą bazie danych działającej na lokalnej maszynie wirtualnej (**SmartHotel.Registration**). Umieszczają bazę danych w grupie zasobów ContosoRG. Jest to grupa zasobów, której używają na potrzeby zasobów produkcyjnych na platformie Azure.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. Konfigurują nowe wystąpienie programu SQL Server (**sql-smarthotel-eus2**) w regionie podstawowym.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Ustawiają warstwę cenową, aby odpowiadała potrzebom dotyczącym serwera i bazy danych. Następnie wybierają opcję oszczędzania pieniędzy dzięki korzyści użycia hybrydowego platformy Azure, ponieważ mają już licencję programu SQL Server.
5. W przypadku określania rozmiarów korzystają z funkcji kupowania opartego na liczbie rdzeni wirtualnych i ustalają limity na podstawie oczekiwanych wymagań.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Następnie tworzą wystąpienie bazy danych.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Po utworzeniu wystąpienia otwierają bazę danych i notują szczegóły, które są potrzebne podczas korzystania z narzędzia Data Migration Assistant w przypadku migracji.

    ![Aprowizowanie kodu SQL](media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Potrzebujesz dalszej pomocy?**

- [Uzyskaj pomoc](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) przy aprowizacji bazy danych SQL Database.
- [Dowiedz](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) się więcej na temat limitów zasobów rdzeni wirtualnych.

## <a name="step-2-migrate-the-database-with-dma"></a>Krok 2. Migrowanie bazy danych przy użyciu DMA

Administratorzy firmy Contoso będą migrować bazę danych SmartHotel360 przy użyciu narzędzia DMA.

### <a name="install-dma"></a>Instalowanie narzędzia DMA

1. Pobierają oni narzędzie z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=53595) na lokalną maszynę wirtualną programu SQL Server (**SQLVM**).
2. Uruchamiają instalatora (DownloadMigrationAssistant.msi) na maszynie wirtualnej.
3. Na stronie **Finish (Zakończenie)** wybierają pozycję **Launch Microsoft Data Migration Assistant (Uruchom narzędzie Microsoft Data Migration Assistant)** przed zakończeniem pracy kreatora.

### <a name="migrate-the-database-with-dma"></a>Migrowanie bazy danych przy użyciu narzędzia DMA

1. W narzędziu DMA tworzą nowy projekt **(SmartHotelDB**) i wybierają pozycję **Migration** (Migracja).
2. Wybierają typ serwera źródłowego jako **SQL Server** i obiekt docelowy jako **Azure SQL Database**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-1.png)

3. W obszarze szczegółów migracji dodają **SQLVM** jako serwer źródłowy i bazę danych **SmartHotel.Registration**.

     ![DMA](media/contoso-migration-refactor-web-app-sql/dma-2.png)

4. Występuje błąd prawdopodobnie skojarzony z uwierzytelnianiem. Jednak po zbadaniu okazuje się, że problemem jest kropka (.) w nazwie bazy danych. Jako obejście podejmują decyzję o aprowizowaniu nowej bazy danych SQL przy użyciu nazwy **SmartHotel-Registration**, aby rozwiązać ten problem. Po ponownym uruchomieniu narzędzia DMA można wybrać opcję **SmartHotel-Registration** i kontynuować pracę z kreatorem.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-3.png)

5. W obszarze **Wybieranie obiektów** wybierają tabele bazy danych i generują skrypt SQL.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-4.png)

6. Po utworzeniu skryptu w narzędziu DMA wybierają pozycję **Wdróż schemat**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-5.png)

7. Narzędzie DMA potwierdza, że wdrożenie zakończyło się pomyślnie.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-6.png)

8. Teraz rozpoczynają migrację.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-7.png)

9. Po zakończeniu migracji administratorzy firmy Contoso mogą sprawdzić, czy baza danych działa w wystąpieniu usługi SQL Azure.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-8.png)

10. Usuwają dodatkową bazę danych SQL Database **SmartHotel.Registration** w witrynie Azure Portal.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-9.png)

## <a name="step-3-provision-web-apps"></a>Krok 3. udostępnianie aplikacji sieci Web

Po przeprowadzeniu migracji bazy danych administratorzy firmy Contoso mogą teraz aprowizować dwie aplikacje internetowe.

1. Wybierają pozycję **Aplikacja internetowa** w portalu.

    ![Aplikacja internetowa](media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Podają nazwę aplikacji (**SHWEB-EUS2**), wybierają system Windows do jej uruchomienia i umieszczają ją w produkcyjnej grupie zasobów **ContosoRG**. Tworzą nową aplikację internetową i plan usługi Azure App Service.

    ![Aplikacja internetowa](media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Po przeprowadzeniu aprowizacji aplikacji internetowej powtarzają proces tworzenia aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**)

    ![Aplikacja internetowa](media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Po zakończeniu przechodzą do adresu aplikacji, aby sprawdzić, czy zostały pomyślnie utworzone.

## <a name="step-4-set-up-azure-devops"></a>Krok 4. Konfigurowanie usługi Azure DevOps

Firma Contoso musi utworzyć infrastrukturę metodyki DevOps i potoki dla aplikacji. W tym celu administratorzy firmy Contoso tworzą nowy projekt DevOps, importują kod, a następnie konfigurują potoki kompilacji i wydania.

1. Na koncie usług Azure DevOps firmy Contoso tworzą nowy projekt (**ContosoSmartHotelRefactor**), a następnie wybierają pozycję **Git** na potrzeby kontroli wersji.

    ![Nowy projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Importują repozytorium usługi Git, które aktualnie przechowuje kod aplikacji. Znajduje się on w [repozytorium publicznym](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) i można go pobrać.

    ![Pobieranie kodu aplikacji](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Po zaimportowaniu kodu łączą program Visual Studio z repozytorium i klonują kod przy użyciu programu Team Explorer.

    ![Łączenie z projektem](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Po sklonowaniu repozytorium na maszynę deweloperską otwierają plik rozwiązania dla aplikacji. Aplikacja internetowa i usługa WCF mają oddzielne projekty w pliku.

    ![Plik rozwiązania](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Krok 5. Konfigurowanie parametrów połączenia

Administratorzy firmy Contoso muszą upewnić się, że wszystkie aplikacje internetowe i baza danych mogą się komunikować. W tym celu konfigurują parametry połączenia w kodzie i w aplikacjach internetowych.

1. W aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**) > **Ustawienia** > **Ustawienia aplikacji** dodają nowe parametry połączenia o nazwie **DefaultConnection**.
2. Parametry połączenia są pobierane z bazy danych **SmartHotel-Registration** i powinny być aktualizowane przy użyciu prawidłowych poświadczeń.

    ![Parametry połączenia](media/contoso-migration-refactor-web-app-sql/string1.png)

3. Za pomocą programu Visual Studio otwierają projekt **SmartHotel.Registration.wcf** z pliku rozwiązania. Sekcja **connectionStrings** pliku web.config usługi WCF SmartHotel.Registration.Wcf powinna zostać zaktualizowana przy użyciu parametrów połączenia.

     ![Parametry połączenia](media/contoso-migration-refactor-web-app-sql/string2.png)

4. Sekcja **client** pliku web.config dla obiektu SmartHotel.Registration.Web powinna zostać zmieniona tak, aby wskazywała lokalizację usługi WCF. Jest to adres URL aplikacji internetowej WCF, która hostuje punkt końcowy usługi.

    ![Parametry połączenia](media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Po wprowadzeniu zmian w kodzie administratorzy muszą zatwierdzić te zmiany. Przy użyciu rozwiązania Team Explorer w programie Visual Studio przeprowadzają zatwierdzanie i synchronizację.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Krok 6. Konfigurowanie potoków kompilacji i wydania na platformie Azure DevOps

Administratorzy firmy Contoso konfigurują teraz usługę Azure DevOps w celu wykonania procesu kompilowania i wydawania.

1. W usłudze Azure DevOps wybierają pozycję **Kompilacja i wydanie** > **Nowy potok**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Wybierają pozycję **Azure Repos (Git)** i odpowiednie repozytorium.

    ![Usługa Git i repozytorium](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. W obszarze **Wybierz szablon** wybierają szablon platformy ASP.NET dla kompilacji.

     ![Szablon platformy ASP.NET](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Nazwa **ContosoSmartHotelRefactor-ASP.NET-CI** jest używana na potrzeby kompilacji. Wybierają pozycję **Zapisz i dodaj do kolejki**.

     ![Zapisywanie i dodawanie do kolejki](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Spowoduje to rozpoczęcie pierwszej kompilacji. Wybierają numer kompilacji, aby obserwować proces. Po zakończeniu mogą zobaczyć opinię o procesie, a następnie wybrać pozycję **Artefakty**, aby przejrzeć wyniki kompilacji.

    ![Przegląd](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. Folder **Drop** zawiera wyniki kompilacji.

    - Dwa pliki ZIP to pakiety zawierające aplikacje.
    - Te pliki są używane w potoku wydania na potrzeby wdrażania w usłudze Azure App Service.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Wybierają kolejno pozycje **Wydania** >  **+Nowy potok**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Wybierają szablon wdrożenia dla usługi Azure App Service.

    ![Szablon wdrożenia usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Nadają potokowi wydania nazwę **ContosoSmartHotel360Refactor** i określają nazwę aplikacji internetowej usługi WCF (SHWCF-EUS2) dla nazwy **etapu**.

    ![Środowisko](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. W obszarze etapów wybierają opcję **1 zadanie, 1 zadanie podrzędne** w celu skonfigurowania wdrożenia usługi WCF.

    ![Wdrażanie usługi WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Sprawdzają, czy subskrypcja została wybrana i autoryzowana, a następnie wybierają **nazwę usługi App Service**.

     ![Wybieranie nazwy usługi App Service](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. W potoku > **Artefakty** wybierają pozycję **+Dodaj artefakt**, a następnie wybierają opcję kompilowania przy użyciu potoku **ContosoSmarthotel360Refactor**.

     ![Kompilacja](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Wybierają ikonę błyskawicy na artefakcie, aby włączyć wyzwalacz ciągłego wdrażania.

     ![Ikona błyskawicy](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Wyzwalacz ciągłego wdrażania powinien być ustawiony na wartość **Włączono**.

    ![Ciągłe wdrażanie włączone](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Teraz przechodzą z powrotem do etapu obejmującego 1 zadanie i 1 zadanie podrzędne, a następnie wybierają pozycję **Wdróż usługę Azure App Service**.

    ![Wdrażanie usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. W obszarze **Wybierz plik lub folder** znajdują plik **SmartHotel.Registration.Wcf.zip**, który został utworzony podczas kompilacji, a następnie wybierają pozycję **Zapisz**.

    ![Zapisywanie usługi WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Wybierają one **potok** > **etapy** **+ Dodaj**, aby dodać środowisko dla **SHWEB-EUS2**. Wybierają inne wdrożenie usługi Azure App Service.

    ![Dodawanie środowiska](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Powtarzają proces, aby opublikować plik aplikacji internetowej (**SmartHotel.Registration.Web.zip**) do odpowiedniej aplikacji internetowej.

    ![Publikowanie aplikacji internetowej](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. Zapisany potok wydania będzie wyglądać w następujący sposób.

     ![Podsumowanie potoku wydania](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. Przechodzą z powrotem do **kompilacji**, a następnie wybierają pozycję **Wyzwalacze** > **Włącz ciągłą integrację**. Powoduje to włączenie potoku, gdy zmiany w kodzie zostaną zatwierdzone oraz gdy nastąpi pełna kompilacja i wydanie.

    ![Włączanie ciągłej integracji](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

21. Wybierają pozycję **Zapisz i dodaj do kolejki**, aby uruchomić pełny potok. Zostanie wyzwolona nowa kompilacja, która z kolei spowoduje utworzenie pierwszego wydania aplikacji do usługi Azure App Service.

    ![Zapisywanie potoku](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

22. Administratorzy firmy Contoso mogą wykonywać kroki procesu potoku kompilowania i wydawania z poziomu usługi Azure DevOps. Po zakończeniu kompilacji rozpocznie się wydanie.

    ![Kompilowanie i wydawanie aplikacji](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

23. Po zakończeniu potoku obie lokacje zostały wdrożone i aplikacja działa w trybie online.

    ![Kończenie wydawania](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

W tym momencie aplikacja została pomyślnie migrowana na platformę Azure.

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po migracji firma Contoso musi wykonać następujące kroki czyszczenia:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie dokumentacji wewnętrznej tak, aby wyświetlić nowe lokalizacje aplikacji SmartHotel360. Przedstawienie bazy danych jako działającej w usłudze Azure SQL Database, a frontonu jako uruchomionego w dwóch aplikacjach internetowych.
- Przegląd wszystkich zasobów korzystających ze zlikwidowanych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

- Firma Contoso musi upewnić się, że nowa baza danych **SmartHotel-Registration** jest bezpieczna. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- W szczególności firma Contoso powinna zaktualizować aplikacje internetowe tak, aby używały protokołu SSL z certyfikatami.

### <a name="backups"></a>Tworzenie kopii zapasowych

- Firma Contoso musi zapoznać się z wymaganiami tworzenia kopii zapasowych dla usługi Azure SQL Database. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Firma Contoso musi również zapoznać się z informacjami na temat zarządzania kopiami zapasowymi i operacjami przywracania bazy danych SQL Database. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups) o automatycznych kopiach zapasowych.
- Firma Contoso powinna rozważyć wdrożenie grup trybu failover w celu zapewnienia regionalnego przechodzenia bazy danych w tryb failover. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Firma Contoso musi rozważyć wdrożenie aplikacji internetowej w głównym regionie Wschodnie stany USA 2 i Środkowe stany USA w celu uzyskania odporności. Firma Contoso może skonfigurować usługę Traffic Manager w celu zapewnienia możliwości przełączenia w tryb failover w przypadku awarii regionalnych.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma Contoso włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła refaktoryzację aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji do dwóch aplikacji internetowych usługi Azure App Service. Baza danych aplikacji została migrowana do bazy danych Azure SQL Database.
