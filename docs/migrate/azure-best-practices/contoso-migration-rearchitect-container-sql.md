---
title: Zmienianie architektury aplikacji na korzystającą z kontenera platformy Azure i usługi Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso zmienia infrastrukturę aplikacji na korzystającą z kontenerów systemu Windows na platformie Azure i usługi Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 0efdd1a42ae7ff161c29f37365d0a14d4d869496
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547365"
---
# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Zmienianie architektury lokalnej aplikacji na korzystającą z kontenera platformy Azure i usługi Azure SQL Database

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso zmienia architekturę dwuwarstwowej aplikacji platformy .NET w systemie Windows działającą na maszynach wirtualnych VMware w ramach migracji na platformę Azure. Firma Contoso migruje maszynę wirtualną frontonu aplikacji do kontenera systemu Windows na platformie Azure, a bazę danych aplikacji do bazy danych Azure SQL Database.

Aplikacja SmartHotel360 używana w tym przykładzie jest oferowana jako aplikacja typu open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Czynniki biznesowe

Zespół liderów IT firmy Contoso w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co jej lokalne systemy i infrastruktura stają się przeciążone.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.** Firma Contoso chce lepiej odpowiadać na zapotrzebowania w branży. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę pomyślnego rozwoju firmy dział IT firmy Contoso musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.
- **Redukcja kosztów.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji.

<!-- markdownlint-disable MD033 -->

**Cele** | **Szczegóły**
--- | ---
**Wymagania dotyczące aplikacji** | Aplikacja na platformie Azure będzie miała nadal krytyczne znaczenie dla działania firmy, tak jak dzisiaj.<br/><br/> Powinna ona mieć takie same możliwości związane z wydajnością, jak w przypadku programu VMware.<br/><br/> Firma Contoso chce przestać obsługiwać system Windows Server 2008 R2, w którym aktualnie działa aplikacja, i chce inwestować w aplikację.<br/><br/> Firma Contoso chce również przejść z programu SQL Server 2008 R2 do nowoczesnej platformy bazy danych PaaS, która zminimalizuje potrzebę zarządzania.<br/><br/> Firma Contoso chce skorzystać z inwestycji w licencjonowanie programu SQL Server Licencjonowanie i pakiet Software Assurance, o ile jest to możliwe.<br/><br/> Firma Contoso chce mieć możliwość skalowania w górę warstwy internetową aplikacji.
**Ograniczenia** | Aplikacja składa się z aplikacji ASP.NET i usługi WCF uruchomionej na tej samej maszynie wirtualnej. Firma Contoso chce ją podzielić na dwie aplikacje internetowe przy użyciu usługi Azure App Service.
**Wymagania dotyczące platformy Azure** | Firma Contoso chce przenieść aplikację na platformę Azure i uruchomić ją w kontenerze, aby zwiększyć żywotność aplikacji. Istotne jest, aby nie rozpoczynać wdrożenia aplikacji na platformie Azure zupełnie od podstaw.
**DevOps** | Firma Contoso chce przenieść się do modelu DevOps przy użyciu usług Azure DevOps Services do kompilacji kodu i potoku wydania.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które zostaną użyte do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja lokalna SmartHotel360 jest podzielona na warstwy, które znajdują się na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5)
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

### <a name="proposed-architecture"></a>Proponowana architektura

- W przypadku warstwy bazy danych w aplikacji firma Contoso porównała bazę danych Azure SQL Database z programem SQL Server w [tym artykule](https://docs.microsoft.com/azure/sql-database/sql-database-features). Firma Contoso zdecydowała się na zastosowanie bazy danych Azure SQL Database z kilku powodów:
  - Azure SQL Database to usługa zarządzana z relacyjnymi bazami danych. Zapewnia ona przewidywalną wydajność na wielu poziomach usługi z niemal zerową liczbą czynności administracyjnych. Zalety obejmują dynamiczną skalowalność bez przestojów, wbudowaną inteligentną optymalizację oraz globalną skalowalność i dostępność.
  - Firma Contoso używa lekkiej wersji narzędzia Data Migration Assistant (DMA) do uzyskiwania dostępu do lokalnej bazy danych i migrowania jej do usług SQL Azure.
  - Dzięki pakietowi Software Assurance firma Contoso może wymienić istniejące licencje na obniżone stawki bazy danych SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Może to zapewnić oszczędności do 30%.
  - Baza danych SQL Database udostępnia kilka funkcji zabezpieczeń, takie jak funkcja Always Encrypted, dynamiczne maskowanie danych i zabezpieczenia na poziomie wiersza/wykrywanie zagrożeń.
- W przypadku warstwy internetowej aplikacji firma Contoso zdecydowała się przekonwertować ją do kontenera systemu Windows przy użyciu usług Azure DevOps Services.
  - Firma Contoso wdroży aplikację przy użyciu usługi Azure Service Fabric i pobierze obraz kontenera systemu Windows z rejestru Azure Container Registry (ACR).
  - Prototyp służący do rozszerzania aplikacji w celu dołączenia analizy tonacji zostanie zaimplementowany jako inna usługa w ramach usługi Service Fabric, połączona z bazą danych Cosmos DB. Spowoduje to odczytanie informacji z tweetów i wyświetlenie ich w aplikacji.
- Aby zaimplementować potok DevOps, firma Contoso użyje usługi Azure DevOps i repozytoriów Git do zarządzania kodem źródłowym. Zautomatyzowane kompilacje i wydania będą używane do kompilowania kodu i wdrażania go w usługach Azure Container Registry i Azure Service Fabric.

    ![Architektura scenariusza](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Konieczna będzie zmiana kodu aplikacji SmartHotel360 w celu przeprowadzenia migracji do usługi Azure Service Fabric. Jednak przy użyciu narzędzi Service Fabric SDK do wprowadzania zmian nakład pracy jest minimalny.<br/><br/> Dzięki przejściu do usługi Service Fabric firma Contoso może zacząć opracowywać mikrousługi, aby szybko dodawać je do aplikacji wraz z upływem czasu, bez ryzyka dla oryginalnego kodu bazowego.<br/><br/> Kontenery systemu Windows oferują takie same korzyści jak kontenery ogólnie. Zwiększają one elastyczność, przenośność i kontrolę.<br/><br/> Firma Contoso może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server.<br/><br/> Po przeprowadzeniu migracji nie będzie już potrzebna obsługa systemu Windows Server 2008 R2. [Dowiedz się więcej](https://support.microsoft.com/lifecycle).<br/><br/> Firma Contoso może skonfigurować warstwę internetową aplikacji z wieloma wystąpieniami, dzięki czemu nie będzie ona już pojedynczym punktem awarii.<br/><br/> Nie będzie ona już zależeć od wieku programu SQL Server 2008 R2.<br/><br/> Baza danych SQL Database obsługuje wymagania techniczne firmy Contoso. Administratorzy firmy Contoso ocenili lokalną bazę danych przy użyciu narzędzia Data Migration Assistant i stwierdzili, że jest ona zgodna.<br/><br/> Baza danych SQL Database ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi konfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Kontenery są bardziej złożone niż inne opcje migracji. Konieczność szkolenia dotyczącego kontenerów może być problemem dla firmy Contoso. Kontenery wprowadzają nowy poziom złożoności, który mimo konieczności szkolenia ma wiele zalet.<br/><br/> Zespół operacyjny firmy Contoso będzie musiał poszerzyć swoje kompetencje, aby nauczyć się obsługi platformy Azure, kontenerów i mikrousług używanych przez aplikację.<br/><br/> Jeśli firma Contoso używa Data Migration Assistant zamiast Azure Database Migration Service do migracji bazy danych, infrastruktura nie będzie gotowa do migrowania baz danych na dużą skalę.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso aprowizuje klaster usługi Azure Service Fabric dla systemu Windows.
2. Aprowizuje również wystąpienie usług SQL Azure i migruje do niego bazę danych aplikacji SmartHotel360.
3. Firma Contoso konwertuje maszynę wirtualną warstwy internetowej na kontener platformy Docker przy użyciu narzędzi zestawu Service Fabric SDK.
4. Następnie nawiązuje połączenie z klastrem usługi Service Fabric i usługą ACR oraz wdraża aplikację za pomocą usługi Azure Service Fabric.

    ![Proces migracji](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Data Migration Assistant (DMA)](/sql/dma/dma-overview?view=ssdt-18vs2017) | Ocenia i wykrywa problemy ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych na platformie Azure. Narzędzie DMA ocenia równoważność funkcji między obiektami źródłowymi i docelowymi SQL oraz rekomenduje ulepszenia dotyczące wydajności i niezawodności. | Narzędzie to można pobrać bezpłatnie.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Udostępnia usługę inteligentnej, w pełni zarządzanej relacyjnej bazy danych w chmurze. | Koszt oparty na funkcjach, przepływności i rozmiarze. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Przechowuje obrazy dla dowolnego typu wdrożeń kontenerów. | Koszt zależy od funkcji, magazynu i czasu użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/container-registry).
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Kompilowanie i obsługa skalowalnych aplikacji rozproszonych, które pracują w trybie ciągłym | Koszt na podstawie rozmiaru, lokalizacji i czasu działania węzłów obliczeniowych. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/service-fabric).
[Azure DevOps](https://docs.microsoft.com/azure/azure-portal/tutorial-azureportal-devops) | Zapewnia potok ciągłej integracji i ciągłego wdrażania (CI/CD) na potrzeby tworzenia aplikacji. Potok rozpoczyna się od repozytorium Git na potrzeby zarządzania kodem aplikacji, systemu kompilacji na potrzeby produkcji pakietów i innych artefaktów kompilacji oraz systemu zarządzania wydaniami na potrzeby wdrażania zmian w środowiskach deweloperskich, testowych i produkcyjnych.

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do uruchomienia tego scenariusza:

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje wcześniej w tej serii artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso wcześniej skonfigurowała infrastrukturę platformy Azure.
**Wymagania wstępne dla deweloperów** | Firma Contoso potrzebuje następujących narzędzi na stacji roboczej dewelopera:<br/><br/> - [Visual Studio 2017 Community Edition: wersja 15,5](https://www.visualstudio.com)<br/><br/> - Włączony pakiet roboczy platformy .NET.<br/><br/> - [Usługa Git](https://git-scm.com)<br/><br/> - [Zestaw Service Fabric SDK 3.0 lub nowszy](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)<br/><br/> - [Program Docker CE (dla systemu Windows 10) lub Docker EE (dla systemu Windows Server)](https://docs.docker.com/docker-for-windows/install) skonfigurowany pod kątem korzystania z kontenerów systemu Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadza migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Inicjowanie obsługi administracyjnej wystąpienia SQL Database na platformie Azure.** Firma Contoso aprowizuje wystąpienie SQL na platformie Azure. Po przeprowadzeniu migracji internetowej maszyny wirtualnej frontonu do kontenera platformy Azure wystąpienie kontenera z frontonem aplikacji internetowej wskaże tę bazę danych.
> - **Krok 2. Tworzenie Azure Container Registry (ACR).** Firma Contoso aprowizuje rejestr kontenerów przedsiębiorstwa na potrzeby obrazów kontenerów platformy Docker.
> - **Krok 3. udostępnianie usługi Azure Service Fabric.** Aprowizuje klaster usługi Service Fabric.
> - **Krok 4. Zarządzanie certyfikatami usługi Service Fabric.** Firma Contoso konfiguruje certyfikaty na potrzeby dostępu usług Azure DevOps Services do klastra.
> - **Krok 5. Migrowanie bazy danych za pomocą DMA.** Migruje bazę danych aplikacji przy użyciu narzędzia Data Migration Assistant.
> - **Krok 6. Konfigurowanie Azure DevOps Services.** Firma Contoso konfiguruje nowy projekt w ramach usług Azure DevOps Services i importuje kod do repozytorium Git.
> - **Krok 7. Konwertowanie aplikacji.** Firma Contoso konwertuje aplikację do kontenera przy użyciu usługi Azure DevOps i narzędzi zestawu SDK.
> - **Krok 8. Konfigurowanie kompilacji i wydania.** Firma Contoso konfiguruje potoki kompilacji i wydawania, aby utworzyć i opublikować aplikację w usłudze ACR i klastrze usługi Service Fabric.
> - **Krok 9. rozbudowanie aplikacji.** Gdy aplikacja jest publiczna, firma Contoso rozszerza ją w celu wykorzystania możliwości platformy Azure i ponownie publikuje ją na platformie Azure przy użyciu potoku.

## <a name="step-1-provision-an-azure-sql-database"></a>Krok 1. Inicjowanie obsługi Azure SQL Database

Administratorzy firmy Contoso aprowizują bazę danych Azure SQL Database.

1. Decydują się na utworzenie bazy danych **SQL Database** na platformie Azure.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

2. Określają nazwę bazy danych odpowiadającą bazie danych działającej na lokalnej maszynie wirtualnej (**SmartHotel.Registration**). Umieszczają bazę danych w grupie zasobów ContosoRG. Jest to grupa zasobów, której używają na potrzeby zasobów produkcyjnych na platformie Azure.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

3. Konfigurują nowe wystąpienie programu SQL Server (**sql-smarthotel-eus2**) w regionie podstawowym.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

4. Ustawiają warstwę cenową, aby odpowiadała potrzebom dotyczącym serwera i bazy danych. Następnie wybierają opcję oszczędzania pieniędzy dzięki korzyści użycia hybrydowego platformy Azure, ponieważ mają już licencję programu SQL Server.
5. W przypadku określania rozmiarów korzystają z funkcji kupowania opartego na liczbie rdzeni wirtualnych i ustalają limity na podstawie oczekiwanych wymagań.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

6. Następnie tworzą wystąpienie bazy danych.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

7. Po utworzeniu wystąpienia otwierają bazę danych i notują szczegóły, które są potrzebne podczas korzystania z narzędzia Data Migration Assistant w przypadku migracji.

    ![Aprowizowanie kodu SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**Potrzebujesz dodatkowej pomocy?**

- [Uzyskaj pomoc](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) przy aprowizacji bazy danych SQL Database.
- [Dowiedz](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) się więcej na temat limitów zasobów rdzeni wirtualnych.

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Krok 2. Tworzenie ACR i Inicjowanie obsługi kontenera platformy Azure

Kontener platformy Azure jest tworzony przy użyciu plików wyeksportowanych z internetowej maszyny wirtualnej. Kontener jest przechowywany w rejestrze Azure Container Registry (ACR).

1. Administratorzy firmy Contoso tworzą rejestr Container Registry w witrynie Azure Portal.

     ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

2. Udostępniają nazwę rejestru (**contosoacreus2**) i umieszczają ją w regionie podstawowym w grupie zasobów, której używają na potrzeby zasobów infrastruktury. Włączają dostęp dla użytkowników administracyjnych i ustawia ją jako jednostkę SKU Premium, aby możliwe było korzystanie z replikacji geograficznej.

    ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Krok 3. udostępnianie usługi Azure Service Fabric

Kontener SmartHotel360 zostanie uruchomiony w klastrze usługi Azure Service Fabric. Administratorzy firmy Contoso tworzą klaster usługi Service Fabric w następujący sposób:

1. Utwórz zasób usługi Service Fabric w witrynie Azure Marketplace.

     ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

2. W obszarze **Ustawienia podstawowe** udostępniana jest unikatowa nazwa DS klastra oraz poświadczenia umożliwiające dostęp do lokalnej maszyny wirtualnej. Umieszczają zasób w produkcyjnej grupie zasobów (**ContosoRG**) w podstawowym regionie Wschodnie stany USA 2.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

3. W obszarze **Konfiguracja typu węzła** wprowadzają nazwę typu węzła, ustawienia trwałości, rozmiar maszyny wirtualnej i punkty końcowe aplikacji.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

4. W obszarze**Tworzenie magazynu Key Vault** tworzą nowy magazyn Key Vault w ramach grupy zasobów infrastruktury, w której będzie przechowywany certyfikat.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

5. W obszarze **Zasady dostępu** umożliwiają dostęp do maszyn wirtualnych w celu wdrożenia magazynu kluczy.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

6. Określają nazwę certyfikatu.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

7. Na stronie podsumowania kopiują link używany do pobierania certyfikatu. Jest on potrzebny do nawiązywania połączenia z klastrem usługi Service Fabric.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

8. Po pomyślnym zakończeniu weryfikacji inicjują klaster.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

9. W Kreatorze importu certyfikatów importują pobrany certyfikat na maszyny deweloperskie. Certyfikat jest używany do uwierzytelniania w klastrze.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

10. Po aprowizacji klastra nawiązują połączenie z Eksploratorem klastrów usługi Service Fabric.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

11. Muszą wybrać właściwy certyfikat.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

12. Eksplorator klastrów usługi Service Fabric ładuje się, po czym administrator firmy Contoso może zarządzać klastrem.

    ![Sieć szkieletowa usługi](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Krok 4. Zarządzanie certyfikatami Service Fabric

Firma Contoso potrzebuje skonfigurować certyfikaty w celu umożliwienia dostępu usług Azure DevOps Services do klastra. Administratorzy firmy Contoso wykonują wymagane w tym celu czynności konfiguracyjne.

1. Otwierają witrynę Azure Portal i przechodzą do magazynu Key Vault.
2. Otwierają certyfikaty i kopiują odcisk palca certyfikatu, który został utworzony podczas procesu aprowizacji.

    ![Kopiowanie odcisku palca](./media/contoso-migration-rearchitect-container-sql/cert1.png)

3. Kopiują go do pliku tekstowego do użycia w przyszłości.
4. Teraz dodają certyfikat klienta, który stanie się certyfikatem klienta administratora w klastrze. Umożliwia to usługom Azure DevOps Services nawiązanie połączenia z klastrem w celu wdrożenia aplikacji w ramach potoku wydania. Aby to zrobić, otwierają magazyn Key Vault w portalu i wybierają pozycję **Certyfikaty** > **Generuj/Importuj**.

    ![Generowanie certyfikatu klienta](./media/contoso-migration-rearchitect-container-sql/cert2.png)

5. Wprowadzają nazwę certyfikatu i podają nazwę wyróżniającą certyfikatu X.509 w polu**Temat**.

     ![Nazwa certyfikatu](./media/contoso-migration-rearchitect-container-sql/cert3.png)

6. Po utworzeniu certyfikatu pobierają go lokalnie w formacie PFX.

     ![Pobieranie certyfikatu](./media/contoso-migration-rearchitect-container-sql/cert4.png)

7. Teraz wracają do listy certyfikatów w usłudze Key Vault i kopiują odcisk palca właśnie utworzonego certyfikatu klienta. Zapisują go w pliku tekstowym.

     ![Odcisk palca certyfikatu klienta](./media/contoso-migration-rearchitect-container-sql/cert5.png)

8. W przypadku wdrażania usług Azure DevOps Services należy określić wartość Base64 certyfikatu. Wykonują to na lokalnej deweloperskiej stacji roboczej przy użyciu programu PowerShell. Wklejają dane wyjściowe do pliku tekstowego w celu późniejszego użycia.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Wartość Base64](./media/contoso-migration-rearchitect-container-sql/cert6.png)

9. Na koniec dodają nowy certyfikat do klastra usługi Service Fabric. W tym celu w portalu otwierają klaster, a następnie wybierają pozycję **Zabezpieczenia**.

     ![Dodawanie certyfikatu klienta](./media/contoso-migration-rearchitect-container-sql/cert7.png)

10. Wybierają pozycję **Dodaj** > **Klient administracyjny** i wkleją odcisk palca nowego certyfikatu klienta. Następnie wybierają pozycję**Dodaj**. Może to potrwać maksymalnie 15 minut.

     ![Dodawanie certyfikatu klienta](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Krok 5. Migrowanie bazy danych przy użyciu DMA

Administratorzy firmy Contoso mogą teraz przeprowadzić migrację bazy danych SmartHotel360 przy użyciu narzędzia DMA.

### <a name="install-dma"></a>Instalowanie narzędzia DMA

1. Pobierają oni narzędzie z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=53595) na lokalną maszynę wirtualną programu SQL Server (**SQLVM**).
2. Uruchamiają instalatora (DownloadMigrationAssistant.msi) na maszynie wirtualnej.
3. Na stronie **Finish** (Zakończenie) wybierają pozycję **Launch Microsoft Data Migration Assistant** (Uruchom narzędzie Microsoft Data Migration Assistant) przed zakończeniem pracy kreatora.

### <a name="configure-the-firewall"></a>Konfigurowanie zapory

Aby nawiązać połączenie z bazą danych Azure SQL Database, administratorzy firmy Contoso konfigurują regułę zapory w celu zezwolenia na dostęp.

1. W obszarze właściwości **zapory i sieci wirtualnych** dla bazy danych zezwalają na dostęp do usług platformy Azure i dodają regułę dla adresu IP klienta lokalnej maszyny wirtualnej programu SQL Server.
2. Tworzona jest reguła zapory na poziomie serwera.

    ![Zapora](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**Potrzebujesz dodatkowej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) na temat tworzenia reguł zapory na potrzeby usługi Azure SQL Database i zarządzania nimi.

### <a name="migrate"></a>Migrowanie

Administratorzy firmy Contoso przeprowadzają teraz migrację bazy danych.

1. W narzędziu DMA tworzą nowy projekt (**SmartHotelDB**) i wybierają pozycję **Migration (Migracja)** .
2. Wybierają typ serwera źródłowego jako **SQL Server** i obiekt docelowy jako **Azure SQL Database**.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

3. W obszarze szczegółów migracji dodają **SQLVM** jako serwer źródłowy i bazę danych **SmartHotel.Registration**.

     ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

4. Występuje błąd prawdopodobnie skojarzony z uwierzytelnianiem. Jednak po zbadaniu okazuje się, że problemem jest kropka (.) w nazwie bazy danych. Jako obejście podejmują decyzję o aprowizowaniu nowej bazy danych SQL przy użyciu nazwy **SmartHotel-Registration**, aby rozwiązać ten problem. Po ponownym uruchomieniu narzędzia DMA można wybrać opcję **SmartHotel-Registration** i kontynuować pracę z kreatorem.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

5. W obszarze **Wybieranie obiektów** wybierają tabele bazy danych i generują skrypt SQL.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

6. Po utworzeniu skryptu w narzędziu DMA wybierają pozycję **Wdróż schemat**.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

7. Narzędzie DMA potwierdza, że wdrożenie zakończyło się pomyślnie.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

8. Teraz rozpoczynają migrację.

    ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

9. Po zakończeniu migracji administratorzy firmy Contoso mogą sprawdzić, czy baza danych działa w wystąpieniu usługi SQL Azure.

     ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

10. Usuwają dodatkową bazę danych SQL Database **SmartHotel.Registration** w witrynie Azure Portal.

     ![Narzędzie DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Krok 6. Konfigurowanie Azure DevOps Services

Firma Contoso musi utworzyć infrastrukturę metodyki DevOps i potoki dla aplikacji. Aby to zrobić, Administratorzy contoso tworzą nowy projekt usługi Azure DevOps, zaimportuj swój kod, a następnie Kompiluj i wydawanie potoków.

1. Na koncie usług Azure DevOps firmy Contoso tworzą nowy projekt (**ContosoSmartHotelRearchitect**), a następnie wybierają pozycję **Git** na potrzeby kontroli wersji.
![Nowy projekt](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

2. Importują repozytorium usługi Git, które aktualnie przechowuje kod aplikacji. Znajduje się on w [repozytorium publicznym](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) i można go pobrać.

    ![Pobieranie kodu aplikacji](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

3. Po zaimportowaniu kodu łączą program Visual Studio z repozytorium i klonują kod przy użyciu programu Team Explorer.

4. Po sklonowaniu repozytorium na maszynę deweloperską otwierają plik rozwiązania dla aplikacji. Aplikacja internetowa i usługa WCF mają oddzielne projekty w pliku.

    ![Plik rozwiązania](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Krok 7. Konwertowanie aplikacji do kontenera

Aplikacja lokalna to tradycyjna aplikacja z trzema warstwami:

- Zawiera formularze WebForms i usługę WCF nawiązującą połączenie z programem SQL Server.
- Używa programu Entity Framework do integracji z danymi w bazie danych SQL Database, do których uzyskuje dostęp za pośrednictwem usługi WCF.
- Aplikacja WebForms współdziała z usługą WCF.

Administratorzy firmy Contoso przekonwertują aplikację do kontenera przy użyciu programu Visual Studio i narzędzi SDK Tools w następujący sposób:

1. Korzystając z programu Visual Studio, przeglądają plik otwartego rozwiązania (SmartHotel.Registration.sln) znajdujący się w katalogu **SmartHotel360-internal-booking-apps\src\Registration** lokalnego repozytorium. Wyświetlane są dwie aplikacje. Aplikacja SmartHotel.Registration.Web frontonu internetowego i aplikacja SmartHotel.Registration.WCF usługi WCF.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container2.png)

2. Klikają prawym przyciskiem myszy aplikację internetową, a następnie wybierają pozycję **Dodaj (Dodaj)**  > **Container Orchestrator Support (Obsługa orkiestratora kontenerów)** .
3. W obszarze **Add Container Orchestra Support (Dodawanie obsługi orkiestratora kontenerów)** wybierają pozycję **Service Fabric**.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container3.png)

4. Powtarzają proces dla aplikacji SmartHotel.Registration.WCF.
5. Teraz sprawdzają, jak zmieniło się rozwiązanie.

    - Nowa aplikacja to **SmartHotel.RegistrationApplication/**
    - Zawiera dwie usługi: **SmartHotel. Registration. WCF** i **SmartHotel. Registration. Web**.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container4.png)

6. Program Visual Studio utworzył plik platformy Docker i pobrał wymagane obrazy lokalnie na maszynę deweloperską.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container5.png)

7. Plik manifestu (**ServiceManifest.xml**) jest tworzony i otwierany przez program Visual Studio. Ten plik zawiera informacje określające sposób, w jaki usługa Service Fabric ma skonfigurować kontener po jego wdrożeniu na platformie Azure.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container6.png)

8. Inny plik manifestu (**ApplicationManifest.xml) zawiera aplikacje konfiguracyjne dla kontenerów.

    ![Kontener](./media/contoso-migration-rearchitect-container-sql/container7.png)

9. Otwierają plik **ApplicationParameters/Cloud.xml** i aktualizują parametry połączenia w celu połączenia aplikacji z bazą danych Azure SQL Database. Parametry połączenia mogą znajdować się w bazie danych w witrynie Azure Portal.

    ![Parametry połączenia](./media/contoso-migration-rearchitect-container-sql/container8.png)

10. Zatwierdzają zaktualizowany kod i wypychają go do usług Azure DevOps Services.

    ![Zatwierdzenie](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Krok 8. Tworzenie i wydawanie potoków w Azure DevOps Services

Administratorzy firmy Contoso konfigurują teraz usługi Azure DevOps Services w celu wykonania procesu kompilowania i wydawania w celu zastosowania praktyk DevOps.

1. W usługach Azure DevOps Services wybierają pozycję **Build and release (Kompilacja i wydanie)**  > **New pipeline (Nowy potok)** .

    ![Nowy potok](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

2. Wybierają pozycję **Azure DevOps Services (Git)** i odpowiednie repozytorium.

    ![Usługa Git i repozytorium](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

3. W obszarze **Wybieranie szablonu** wybierają sieć szkieletową z obsługą platformy Docker.

     ![Sieć szkieletowa i platforma Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

4. Zmieniają obrazy tagów akcji, aby **utworzyć obraz**, i konfigurują zadanie w taki sposób, aby korzystało z zaprowizowanego rejestru ACR.

     ![Rejestr](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

5. W zadaniu **wypychania obrazów** konfigurują obraz pod kątem wypychania do rejestru ACR i wybierają uwzględnienie najnowszego tagu.
6. W obszarze **Triggers** (Wyzwalacze) włączają ciągłą integrację i dodają gałąź master.

    ![Wyzwalacze](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

7. Wybierają pozycję **Save and Queue (Zapisz i dodaj do kolejki)** , aby rozpocząć kompilację.
8. Po pomyślnym zakończeniu kompilacji przechodzą do potoku wydania. W usługach Azure DevOps Services wybierają pozycję **Wydania** > **Nowy potok**.

    ![Potok wydania](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

9. Wybierają szablon**Wdrożenie usługi Azure Service Fabric** i nazywają etap (**SmartHotelSF**).

    ![Środowisko](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

10. Podają nazwę potoku (**ContosoSmartHotel360Rearchitect**). Dla etapu wybierają pozycję **1 job, 1 task (1 zadanie, 1 podzadanie)** , aby skonfigurować wdrożenie usługi Service Fabric.

    ![Faza i zadanie](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

11. Teraz wybierają pozycję **New** (Nowe), aby dodać nowe połączenie z klastrem.

    ![Nowe połączenie](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

12. W obszarze**Add Service Fabric service connection (Dodawanie połączenia z usługą Service Fabric)** konfigurują połączenie oraz ustawienia uwierzytelniania, które będą używane przez usługi Azure DevOps Services do wdrożenia aplikacji. Punkt końcowy klastra można znaleźć w witrynie Azure Portal. Administratorzy firmy Contoso dodają również ciąg **tcp://** jako prefiks.

13. Zebrane informacje o certyfikacie to dane wprowadzone w polach **Server Certificate Thumbprint (Odcisk palca certyfikatu)** i **Client Certificate (Certyfikat klienta)** .

    ![Certyfikat](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

14. Wybierają pozycję Pipeline (Potok) > **Add an artifact (Dodaj artefakt)** .

     ![Artefakt](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

15. Wybierają projekt i potok kompilacji. Używana jest najnowsza wersja.

     ![Kompilacja](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

16. Zwróć uwagę na to, że błyskawica na artefakcie jest zaznaczona.

     ![Stan artefaktu](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

17. Ponadto należy pamiętać, że włączony jest wyzwalacz ciągłego wdrażania.
   ![Włączone ciągłe wdrażanie](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

18. Wybierają pozycję **Save (Zapisz)**  > **Create a release (Utwórz wydanie)** .

    ![Wydawanie](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

19. Po zakończeniu wdrożenia aplikacja SmartHotel360 będzie teraz działać w ramach usługi Service Fabric.

    ![Publikuj](./media/contoso-migration-rearchitect-container-sql/publish4.png)

20. Aby nawiązać połączenie z aplikacją, kierują ruch do publicznego adresu IP modułu równoważenia obciążenia platformy Azure przed węzłami usługi Service Fabric.

    ![Publikuj](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Krok 9. zwiększenie i ponowne opublikowanie aplikacji

Gdy aplikacja SmartHotel360 i baza danych jest uruchomiona na platformie Azure, firma Contoso chce ją rozszerzyć.

- Deweloperzy firmy Contoso są prototypami nowej aplikacji platformy .NET Core, która będzie działać w klastrze Service Fabric.
- Aplikacja zostanie użyta do ściągnięcia danych tonacji z bazy danych Cosmos DB.
- Te dane będą w formie tweetów przetwarzanych przy użyciu bezserwerowej funkcji platformy Azure i interfejsu API analizy tekstu usług Azure Cognitive Services.

### <a name="provision-azure-cosmos-db"></a>Aprowizowanie bazy danych Azure Cosmos DB

Jako pierwszy krok administratorzy firmy Contoso aprowizują bazę danych Azure Cosmos Database.

1. Tworzą zasób bazy danych Azure Cosmos DB z poziomu witryny Azure Marketplace.

    ![Rozszerzanie](./media/contoso-migration-rearchitect-container-sql/extend1.png)

2. Udostępniają nazwę bazy danych(**contososmarthotel**), wybierają interfejs API SQL i umieszczają zasób w produkcyjnej grupie zasobów w podstawowym regionie Wschodnie stany USA 2.

    ![Rozszerzanie](./media/contoso-migration-rearchitect-container-sql/extend2.png)

3. W obszarze **Wprowadzenie** wybierają pozycję **Eksplorator danych** i dodają nową kolekcję.
4. W obszarze **Dodawanie kolekcji** podają identyfikatory i ustawiają pojemność magazynu i przepływność.

    ![Rozszerzanie](./media/contoso-migration-rearchitect-container-sql/extend3.png)

5. W portalu otwierają nową bazę danych, wybierają pozycję **Kolekcja** > **Dokumenty**, a następnie wybierają pozycję **Nowy dokument**.
6. Wklejają poniższy kod JSON do okna dokumentu. Są to przykładowe dane w postaci pojedynczego tweetu.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Rozszerzanie](./media/contoso-migration-rearchitect-container-sql/extend4.png)

7. Lokalizują punkt końcowy bazy danych Cosmos DB i klucz uwierzytelniania. Są one używane w aplikacji do nawiązania połączenia z kolekcją. W bazie danych wybierają pozycję **Klucze** i kopiują identyfikator URI i klucz podstawowy do Notatnika.

    ![Rozszerzanie](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Aktualizowanie aplikacji tonacji

Po zainicjowaniu bazy danych Cosmos DB administratorzy firmy Contoso mogą skonfigurować aplikację w celu nawiązywania połączenia z tą bazą danych.

1. W programie Visual Studio otwierają plik ApplicationModern\ApplicationParameters\cloud.xml w Eksplorator rozwiązań.

    ![Aplikacja tonacji](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

2. Wypełniają następujące dwa parametry:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Aplikacja tonacji](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Ponowne publikowanie aplikacji

Po rozszerzeniu aplikacji administratorzy firmy Contoso publikują ją ponownie na platformie Azure przy użyciu potoku.

1. Zatwierdzają i wypychają swój kod do usług Azure DevOps Services. Spowoduje to uruchomienie potoków kompilacji i wydania.

2. Po zakończeniu kompilacji i wdrożenia aplikacja SmartHotel360 będzie teraz działać w ramach usługi Service Fabric. W konsoli zarządzania usługi Service Fabric są teraz wyświetlane trzy usługi.

    ![Ponowne publikowanie](./media/contoso-migration-rearchitect-container-sql/republish3.png)

3. Administratorzy firmy Contoso mogą teraz klikać usługi, aby zobaczyć, że aplikacja SentimentIntegration jest uruchomiona.

    ![Ponowne publikowanie](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po migracji firma Contoso musi wykonać następujące kroki czyszczenia:

- Usunięcie lokalnych maszyn wirtualnych ze spisu serwera vCenter.
- Usunięcie maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie dokumentacji wewnętrznej tak, aby wyświetlić nowe lokalizacje aplikacji SmartHotel360. Przedstawienie bazy danych jako działającej w usłudze Azure SQL Database, a frontonu jako uruchomionego w usłudze Service Fabric.
- Przegląd wszystkich zasobów korzystających z zlikwidowanych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

- Administratorzy firmy Contoso muszą upewnić się, że nowa baza danych **SmartHotel-Registration** jest bezpieczna. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- W szczególności firma Contoso powinna zaktualizować kontener tak, aby używał protokołu SSL z certyfikatami.
- Firma Contoso powinna rozważyć użycie usługi Key Vault w celu chronienia wpisów tajnych aplikacji usługi Service Fabric. [Dowiedz się więcej](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups"></a>Tworzenie kopii zapasowych

- Firma Contoso musi zapoznać się z wymaganiami tworzenia kopii zapasowych dla usługi Azure SQL Database. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Administratorzy firmy Contoso powinni rozważyć wdrożenie grup trybu failover w celu zapewnienia regionalnego przechodzenia bazy danych w tryb failover. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Mogą oni wykorzystać replikację geograficzną dla jednostki SKU w warstwie Premium usługi ACR. [Dowiedz się więcej](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Firma Contoso musi rozważyć wdrożenie aplikacji internetowej w głównym regionie Wschodnie stany USA 2 i Środkowe stany USA, gdy funkcja Web App for Containers stanie się dostępna. Administratorzy firmy Contoso mogą skonfigurować usługę Traffic Manager w celu zapewnienia możliwości przełączenia w tryb failover w przypadku awarii regionalnych.
- Baza danych Cosmos DB automatycznie tworzy kopie zapasowe. [Przeczytaj](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) o tym procesie, aby dowiedzieć się więcej.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) o usłudze Azure Cost Management.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadziła refaktoryzację aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji do usługi Service Fabric. Baza danych aplikacji została migrowana do bazy danych Azure SQL Database.
