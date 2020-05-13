---
title: Migrowanie aplikacji do Azure App Service i SQL Database
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak replikować aplikację, migrując ją do Azure App Service i Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 37a8a55762dc1ddb49e41673da1497cef4a1606f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223647"
---
<!-- cSpell:ignore WEBVM SQLVM contosohost vcenter contosodc smarthotel SHWEB SHWCF -->

# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Refaktoryzowanie aplikacji lokalnej do aplikacji internetowej Azure App Service i bazy danych Azure SQL Database

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso refaktoryzuje dwuwarstwową aplikację platformy .NET w systemie Windows działającą na maszynach wirtualnych VMware w ramach migracji na platformę Azure. Firma przeprowadza migrację maszyny wirtualnej frontonu aplikacji do aplikacji internetowej Azure App Service i migrację bazy danych aplikacji do bazy danych Azure SQL Database.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się i następuje przeciążenie lokalnych systemów i infrastruktury.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.**  Dział IT firmy Contoso chce lepiej odpowiadać na zapotrzebowania biznesowe. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Zasięgu.** W miarę rozwoju działalności biznesowej firma Contoso musi zapewnić systemy, które mogą rosnąć w tym samym tempie.
- **Obniżyć koszty.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Aplikacja** | Aplikacja na platformie Azure będzie miała nadal krytyczne znaczenie dla działania firmy, tak jak dzisiaj. <br><br> Powinna ona mieć takie same możliwości związane z wydajnością, jak w przypadku programu VMware. <br><br> Zespół nie chce inwestować w aplikację. Na razie administratorzy będą bezpiecznie przenosić aplikację do chmury. <br><br> Zespół chce przestać obsługiwać system Windows Server 2008 R2, w którym aktualnie działa aplikacja. <br><br> Zespół chce również przejść z programu SQL Server 2008 R2 do nowoczesnej platformy bazy danych PaaS, która zminimalizuje potrzebę zarządzania. <br><br> Firma Contoso chce skorzystać z inwestycji w licencjonowanie programu SQL Server Licencjonowanie i pakiet Software Assurance, o ile jest to możliwe. <br><br> Ponadto firma Contoso chce wyeliminować pojedynczy punkt awarii w warstwie internetowej.
**Ograniczenia** | Aplikacja składa się z aplikacji ASP.NET i usługi WCF uruchomionej na tej samej maszynie wirtualnej. Chcą rozłożyć te składniki na dwie aplikacje sieci Web przy użyciu Azure App Service.
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

- W przypadku warstwy bazy danych w aplikacji firma Contoso porównała bazę danych Azure SQL Database z programem SQL Server w [tym artykule](https://docs.microsoft.com/azure/sql-database/sql-database-features). Firma Contoso zdecydowała się na zastosowanie bazy danych Azure SQL Database z kilku powodów:
  - Azure SQL Database to usługa zarządzana z relacyjnymi bazami danych. Zapewnia ona przewidywalną wydajność na wielu poziomach usługi z niemal zerową liczbą czynności administracyjnych. Zalety obejmują dynamiczną skalowalność bez przestojów, wbudowaną inteligentną optymalizację oraz globalną skalowalność i dostępność.
  - Firma Contoso może użyć uproszczonej Data Migration Assistant (DMA) do oceny lokalnej bazy danych w usłudze Azure SQL.
  - Firma Contoso może używać Azure Database Migration Service (DMS) do migrowania lokalnej bazy danych do usługi Azure SQL.
  - Dzięki pakietowi Software Assurance firma Contoso może wymienić istniejące licencje na obniżone stawki bazy danych SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Może to zapewnić oszczędności do 30%.
  - Baza danych SQL Database udostępnia funkcje zabezpieczeń, takie jak funkcja Always Encrypted, dynamiczne maskowanie danych i zabezpieczenia na poziomie wiersza/wykrywanie zagrożeń.
- W przypadku warstwy internetowej aplikacji firma Contoso zdecydowała się użyć usługi Azure App Service. Ta usługa PaaS umożliwia wdrożenie aplikacji przy użyciu tylko kilku zmian konfiguracji. Firma Contoso będzie używać programu Visual Studio do wprowadzania zmian i wdrażania dwóch aplikacji internetowych. Jedna z nich będzie związana z witryny internetową, a druga z usługą WCF.
- Aby spełnić wymagania stawiane przez potok DevOps, firma Contoso wybrała opcję użycia usługi Azure DevOps i repozytoriów Git do zarządzania kodem źródłowym. Do kompilowania kodu i wdrażania go w usłudze Azure App Service będą używane zautomatyzowane kompilacje i wydania.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Kod aplikacji SmartHotel360 nie wymaga zmian dotyczących migracji na platformę Azure. <br><br> Firma Contoso może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server. <br><br> Po migracji system Windows Server 2008 R2 nie będzie musiał być obsługiwany. Aby uzyskać więcej informacji, zobacz [Zasady cyklu życia firmy Microsoft](https://aka.ms/lifecycle). <br><br> Firma Contoso może skonfigurować warstwę internetową aplikacji z wieloma wystąpieniami, dzięki czemu nie będzie ona już pojedynczym punktem awarii. <br><br> Baza danych nie będzie już zależeć od wieku programu SQL Server 2008 R2. <br><br> Baza danych SQL Database obsługuje wymagania techniczne. Firma Contoso oceniła lokalną bazę danych przy użyciu narzędzia Data Migration Assistant i stwierdziła, że jest ona zgodna. <br><br> Azure SQL Database ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi skonfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii. <br><br> Jeśli firma Contoso używa Azure Database Migration Service do migrowania swojej bazy danych, będzie miała gotową infrastrukturę do migrowania baz danych na dużą skalę.
**Wady** | Usługa Azure App Service obsługuje tylko jedno wdrożenie aplikacji dla każdej aplikacji internetowej. Oznacza to, że należy aprowizować dwie aplikacje internetowe (jedna dla witryny internetowej i druga dla usługi WCF).

<br>

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Proponowana architektura

![Architektura scenariusza](./media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso inicjuje obsługę wystąpienia usługi Azure SQL i migruje bazę danych SmartHotel360 do niej przy użyciu Azure Database Migration Service (DMS).
2. Firma Contoso aprowizuje i konfiguruje aplikacje internetowe oraz wdraża do nich aplikację SmartHotel360.

    ![Proces migracji](./media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Firma Contoso używa narzędzia DMA do oceny i wykrywania problemów ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych na platformie Azure. Narzędzie DMA ocenia równoważność funkcji między obiektami źródłowymi i docelowymi SQL oraz rekomenduje ulepszenia dotyczące wydajności i niezawodności. | Narzędzie to można pobrać bezpłatnie.
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Usługa inteligentnej, w pełni zarządzanej relacyjnej bazy danych w chmurze. | Koszt oparty na funkcjach, przepływności i rozmiarze. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](https://docs.microsoft.com/azure/app-service/overview) | Tworzenie zaawansowanych aplikacji w chmurze za pomocą w pełni zarządzanej platformy | Koszt oparty na rozmiarze, lokalizacji i czasie użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Zapewnia potok ciągłej integracji i ciągłego wdrażania (CI/CD) na potrzeby tworzenia aplikacji. Potok rozpoczyna się od repozytorium Git na potrzeby zarządzania kodem aplikacji, systemu kompilacji na potrzeby produkcji pakietów i innych artefaktów kompilacji oraz systemu zarządzania wydaniami na potrzeby wdrażania zmian w środowiskach deweloperskich, testowych i produkcyjnych.

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
> - **Krok 1. Inicjowanie obsługi administracyjnej wystąpienia SQL Database na platformie Azure.** Firma Contoso aprowizuje wystąpienie SQL na platformie Azure. Po przeprowadzeniu migracji witryny internetowej na platformę Azure aplikacja internetowa usługi WCF będzie wskazywać to wystąpienie.
> - **Krok 2. Ocena bazy danych za pomocą usługi Azure Database Asystent migracji (DMA) i migrowanie Database Migration Service (DMS).** Firma Contoso ocenia bazę danych pod kątem migracji, a następnie migruje bazę danych aplikacji za pomocą usługi Azure Data Migration Service.
> - **Krok 3. udostępnianie aplikacji sieci Web.** Firma Contoso aprowizuje dwie aplikacje internetowe.
> - **Krok 4. Konfigurowanie usługi Azure DevOps.** Firma Contoso tworzy nowy projekt usługi Azure DevOps i importuje repozytorium usługi Git.
> - **Krok 5. Konfigurowanie parametrów połączenia.** Firma Contoso konfiguruje parametry połączenia tak, aby aplikacja internetowa warstwy internetowej, aplikacja internetowa usługi WCF i wystąpienie programu SQL mogły się komunikować.
> - **Krok 6. Konfigurowanie potoków kompilacji i wydania.** W ostatnim kroku firma Contoso konfiguruje potoki kompilowania i wydawania, aby utworzyć aplikację, i wdraża je w dwóch oddzielnych aplikacjach sieci Web.

## <a name="step-1-provision-an-azure-sql-database"></a>Krok 1. Inicjowanie obsługi Azure SQL Database

1. Administratorzy firmy Contoso wybierają bazę danych SQL Database na platformie Azure.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Określają nazwę bazy danych odpowiadającą bazie danych działającej na lokalnej maszynie wirtualnej (**SmartHotel.Registration**). Umieszczają bazę danych w grupie zasobów ContosoRG. Jest to grupa zasobów, której używają na potrzeby zasobów produkcyjnych na platformie Azure.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. Konfigurują nowe wystąpienie programu SQL Server (**sql-smarthotel-eus2**) w regionie podstawowym.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Ustawiają warstwę cenową, aby odpowiadała potrzebom dotyczącym serwera i bazy danych. Następnie wybierają opcję oszczędzania pieniędzy dzięki korzyści użycia hybrydowego platformy Azure, ponieważ mają już licencję programu SQL Server.
5. W przypadku ustalania wielkości korzystają z zakupu opartego na rdzeń wirtualnyach i ustalają limity dla ich oczekiwanych wymagań.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. Następnie tworzą wystąpienie bazy danych.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Po utworzeniu wystąpienia otwierają bazę danych i notują szczegóły, które są potrzebne podczas korzystania z narzędzia Data Migration Assistant w przypadku migracji.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**Potrzebujesz dodatkowej pomocy?**

- [Uzyskaj pomoc](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) przy aprowizacji bazy danych SQL Database.
- [Dowiedz się więcej na temat](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) limitów zasobów rdzeń wirtualny.

## <a name="step-2-assess-the-database-with-database-migration-assistant-dma-and-migrate-with-azure-database-migration-service-dms"></a>Krok 2. Ocena bazy danych przy użyciu Asystent migracji bazy danych (DMA) i Migrowanie z Azure Database Migration Service (DMS)

Administratorzy firmy Contoso oceniają bazę danych przy użyciu Asystent migracji bazy danych (DMA), a następnie migruje ją przy użyciu usług Azure Database Migration Services (DMS) przy użyciu [samouczka migracji krok po kroku](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online). Mogą wykonywać migracje w trybie online, offline i hybrydowym (wersja zapoznawcza).

Podsumowując, należy wykonać następujące czynności:

- Korzystając z Asystent migracji bazy danych (DMA), można wykrywać i rozwiązywać problemy związane z migracją bazy danych.
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

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Podają nazwę aplikacji (**SHWEB-EUS2**), wybierają system Windows do jej uruchomienia i umieszczają ją w produkcyjnej grupie zasobów **ContosoRG**. Tworzą nową aplikację internetową i plan usługi Azure App Service.

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Po przeprowadzeniu aprowizacji aplikacji internetowej powtarzają proces tworzenia aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**)

    ![Aplikacja internetowa](./media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Po zakończeniu przechodzą do adresu aplikacji, aby sprawdzić, czy zostały pomyślnie utworzone.

## <a name="step-4-set-up-azure-devops"></a>Krok 4. Konfigurowanie usługi Azure DevOps

Firma Contoso musi utworzyć infrastrukturę metodyki DevOps i potoki dla aplikacji. W tym celu administratorzy firmy Contoso tworzą nowy projekt DevOps, importują kod, a następnie konfigurują potoki kompilacji i wydania.

1. W organizacji contoso DevOps Organization tworzy nowy projekt (**ContosoSmartHotelRefactor**), a następnie wybierz pozycję **git** dla kontroli wersji.

    ![Nowy projekt](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Importują repozytorium usługi Git, które aktualnie przechowuje kod aplikacji. Jest ona w [publicznym repozytorium GitHub](https://github.com/Microsoft/SmartHotel360-Registration) i można ją pobrać.

    ![Pobieranie kodu aplikacji](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Po zaimportowaniu kodu łączą program Visual Studio z repozytorium i klonują kod przy użyciu programu Team Explorer.

    ![Łączenie z projektem](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Po sklonowaniu repozytorium na maszynę deweloperską otwierają plik rozwiązania dla aplikacji. Aplikacja internetowa i usługa WCF mają oddzielne projekty w pliku.

    ![Plik rozwiązania](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Krok 5. Konfigurowanie parametrów połączenia

Administratorzy firmy Contoso muszą upewnić się, że wszystkie aplikacje internetowe i baza danych mogą się komunikować. W tym celu konfigurują parametry połączenia w kodzie i w aplikacjach internetowych.

1. W aplikacji internetowej dla usługi WCF (**SHWCF-EUS2**) > **Ustawienia** > **Ustawienia aplikacji** dodają nowe parametry połączenia o nazwie **DefaultConnection**.
2. Parametry połączenia są pobierane z bazy danych **SmartHotel-Registration** i powinny być aktualizowane przy użyciu prawidłowych poświadczeń.

    ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql/string1.png)

3. Za pomocą programu Visual Studio otwierają projekt **SmartHotel.Registration.wcf** z pliku rozwiązania. Sekcja **connectionStrings** pliku web.config usługi WCF SmartHotel.Registration.Wcf powinna zostać zaktualizowana przy użyciu parametrów połączenia.

     ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql/string2.png)

4. Sekcja **client** pliku web.config dla obiektu SmartHotel.Registration.Web powinna zostać zmieniona tak, aby wskazywała lokalizację usługi WCF. Jest to adres URL aplikacji internetowej WCF, która hostuje punkt końcowy usługi.

    ![Parametry połączenia](./media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Po wprowadzeniu zmian w kodzie administratorzy muszą zatwierdzić te zmiany. Przy użyciu rozwiązania Team Explorer w programie Visual Studio przeprowadzają zatwierdzanie i synchronizację.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Krok 6. Konfigurowanie potoków kompilacji i wydania na platformie Azure DevOps

Administratorzy firmy Contoso konfigurują teraz usługę Azure DevOps w celu wykonania procesu kompilowania i wydawania.

1. W usłudze Azure DevOps wybierają pozycję **kompilacja i wydanie**  >  **nowego potoku**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Wybierają pozycję **Azure Repos (Git)** i odpowiednie repozytorium.

    ![Usługa Git i repozytorium](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. W obszarze **Wybierz szablon** wybierają szablon platformy ASP.NET dla kompilacji.

     ![Szablon platformy ASP.NET](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Nazwa **ContosoSmartHotelRefactor-ASP.NET-CI** jest używana na potrzeby kompilacji. Wybierają pozycję **Zapisz i dodaj do kolejki**.

     ![Zapisywanie i dodawanie do kolejki](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Spowoduje to rozpoczęcie pierwszej kompilacji. Wybierają numer kompilacji, aby obserwować proces. Po zakończeniu zobaczysz opinię o procesie, a następnie wybierzesz **artefakty** , aby przejrzeć wyniki kompilacji.

    ![Przegląd](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. Folder **Drop** zawiera wyniki kompilacji.

    - Dwa pliki ZIP to pakiety zawierające aplikacje.
    - Te pliki są używane w potoku wydania na potrzeby wdrażania w usłudze Azure App Service.

     ![Artefakt](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Wybierają **wersje**  >  **+ Nowy potok**.

    ![Nowy potok](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Wybierają szablon wdrożenia dla usługi Azure App Service.

    ![Szablon wdrożenia usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Nadają potokowi wydania nazwę **ContosoSmartHotel360Refactor** i określają nazwę aplikacji internetowej usługi WCF (SHWCF-EUS2) dla nazwy **etapu**.

    ![Środowisko](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. W obszarze etapów wybierają opcję **1 zadanie, 1 zadanie podrzędne** w celu skonfigurowania wdrożenia usługi WCF.

    ![Wdrażanie usługi WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Sprawdzają, czy subskrypcja została wybrana i autoryzowana, a następnie wybierają **nazwę usługi App Service**.

     ![Wybieranie nazwy usługi App Service](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. Na > **artefakty**potoku wybierają **i dodają artefakt**, a następnie wybierają kompilację przy użyciu potoku **ContosoSmarthotel360Refactor** .

     ![Kompilacja](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Sprawdzają one, że został sprawdzony piorun w artefaktie, aby włączyć wyzwalacz ciągłego wdrażania.

     ![Ikona błyskawicy](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. Wyzwalacz ciągłego wdrażania powinien być ustawiony na wartość **Włączono**.

    ![Ciągłe wdrażanie włączone](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Teraz przechodzą z powrotem do zadania etap 1, I zadań, a następnie wybierz pozycję **wdróż Azure App Service**.

    ![Wdrażanie usługi Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. W obszarze **Wybierz plik lub folder**zlokalizuj plik **SmartHotel. Registration. WCF. zip** , który został utworzony podczas kompilacji, a następnie wybierz pozycję **Zapisz**.

    ![Zapisywanie usługi WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Wybierają **etapy potoku**  >  **Stages**, a następnie **dodają** , aby dodać środowisko dla **SHWEB-EUS2**. Wybierają inne wdrożenie usługi Azure App Service.

    ![Dodawanie środowiska](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Powtarzają proces, aby opublikować plik aplikacji internetowej (**SmartHotel.Registration.Web.zip**) do odpowiedniej aplikacji internetowej.

    ![Publikowanie aplikacji internetowej](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. Zapisany potok wydania będzie wyglądać w następujący sposób.

     ![Podsumowanie potoku wydania](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. Są one przenoszone do **kompilacji**, a następnie wybierz kolejno pozycje **wyzwalacze**  >  **Włącz ciągłą integrację**. Powoduje to włączenie potoku, gdy zmiany w kodzie zostaną zatwierdzone oraz gdy nastąpi pełna kompilacja i wydanie.

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
- Firma Contoso musi rozważyć wdrożenie aplikacji internetowej w głównym regionie Wschodnie stany USA 2 i Środkowe stany USA w celu uzyskania odporności. Firma Contoso może skonfigurować Traffic Manager, aby zapewnić pracę w trybie failover w trakcie okresu regionalnego.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma Contoso będzie używać [Azure Cost Management](https://azure.microsoft.com/services/cost-management) , aby zapewnić, że pozostają w ramach budżetów ustanowionych przez ich lidera.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła refaktoryzację aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji do dwóch aplikacji internetowych usługi Azure App Service. Baza danych aplikacji została migrowana do bazy danych Azure SQL Database.
