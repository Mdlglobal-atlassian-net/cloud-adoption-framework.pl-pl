---
title: Ponowne kompilowanie aplikacji lokalnej na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso ponownie kompiluje aplikację na platformie Azure przy użyciu usług Azure App Service, Azure Kubernetes Service, Cosmos DB, Azure Functions i Azure Cognitive Services.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 160d39a26e579816b2e961df30715e6aae1d16bb
ms.sourcegitcommit: f53e8620adfca7bb5660ef23cac1dab069998e0e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2020
ms.locfileid: "76726339"
---
# <a name="rebuild-an-on-premises-app-on-azure"></a>Ponowne kompilowanie aplikacji lokalnej na platformie Azure

W tym artykule pokazano, jak fikcyjna firma Contoso ponownie kompiluje dwuwarstwową aplikację .NET systemu Windows uruchomioną na maszynach wirtualnych VMware w ramach migracji do platformy Azure. Firma Contoso migruje maszynę wirtualną frontonu aplikacji do aplikacji internetowej usługi Azure App Service. Zaplecze aplikacji jest tworzone przy użyciu mikrousług wdrożonych w kontenerach zarządzanych przez usługę Azure Kubernetes Service (AKS). Witryna współdziała z usługą Azure Functions w celu udostępnienia funkcji obsługi zdjęć zwierząt domowych.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Czynniki biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso się rozwija i chce zapewnić klientom zróżnicowane środowiska w witrynach internetowych firmy Contoso.
- **Zwinność.** Firma Contoso chce być w stanie szybciej reagować na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej.
- **Skalowalność.** W miarę rozwoju firmy Contoso jej dział IT musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.
- **Redukcja kosztów.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso określił wymagania związane z aplikacją w tym procesie migracji. Na podstawie tych wymagań określono najlepszą metodę migracji:

- Na platformie Azure aplikacja będzie miała tak samo krytyczne znaczenie jak teraz. Powinna być wydajna i łatwa w skalowaniu.
- Aplikacja nie powinna korzystać ze składników IaaS. Wszystko powinno być skonstruowane tak, aby możliwe było korzystanie z usług PaaS lub usług bezserwerowych.
- Kompilacje aplikacji powinny działać w usługach w chmurze, a kontenery powinny znajdować się w prywatnym rejestrze kontenerów dla całego przedsiębiorstwa w chmurze.
- Usługa interfejsu API używana do obsługi zdjęć zwierząt powinna być dokładna i niezawodna w rzeczywistych warunkach, ponieważ decyzje podjęte przez aplikację muszą być uznawane w należących do firmy hotelach. W hotelach będzie mogło przebywać każde zwierzę, które otrzyma zezwolenie na dostęp w aplikacji.
- Aby spełnić wymagania stawiane przez potok DevOps, firma Contoso użyje usługi Azure DevOps i repozytoriów Git do zarządzania kodem źródłowym. Do kompilowania kodu i wdrażania go w usługach Azure App Service, Azure Functions i AKS będą używane zautomatyzowane kompilacje i wydania.
- Mikrousługi na zapleczu oraz witryna internetowa na frontonie wymagają użycia różnych potoków ciągłej integracji/ciągłego wdrażania.
- Usługi zaplecza i aplikacja internetowa frontonu mają inny cykl wydawania. Aby spełnić to wymaganie, wdrażane są dwa różne potoki.
- Firma Contoso potrzebuje funkcji zatwierdzania wszystkich wdrożeń witryny internetowej frontonu przez kierownictwo, a potok ciągłej integracji/ciągłego wdrażania musi ją zapewnić.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które będą używane do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja lokalna SmartHotel360 jest podzielona na warstwy, które znajdują się na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5)
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

### <a name="proposed-architecture"></a>Proponowana architektura

- Fronton aplikacji jest wdrażany jako aplikacja sieci Web Azure App Service w podstawowym regionie platformy Azure.
- Funkcja platformy Azure umożliwia przekazywanie zdjęć zwierząt, a witryna współdziała z tą funkcją.
- Funkcja obsługi zdjęć zwierząt korzysta z interfejsu API przetwarzania obrazów usługi Azure Cognitive Services oraz z usługi Cosmos DB.
- Zaplecze witryny jest utworzone przy użyciu mikrousług. Zostaną one wdrożone w kontenerach zarządzanych przez usługę Azure Kubernetes Service (AKS).
- Kontenery zostaną utworzone przy użyciu usługi Azure DevOps, a następnie wypchnięte do usługi Azure Container Registry (ACR).
- Na chwilę obecną firma Contoso będzie ręcznie wdrażała aplikację internetową i kod funkcji przy użyciu programu Visual Studio.
- Mikrousługi zostaną wdrożone przy użyciu skryptu programu PowerShell, który wywołuje narzędzia wiersza polecenia rozwiązania Kubernetes.

    ![Architektura scenariusza](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Użycie usług PaaS i rozwiązań bezserwerowych w przypadku kompleksowego wdrożenia znacząco skraca czas, który firma Contoso musi przeznaczyć na zarządzanie.<br/><br/> Przejście do architektury mikrousług umożliwia firmie Contoso łatwe rozszerzenie rozwiązania w przyszłości.<br/><br/> Nową funkcję można uruchomić w trybie online bez zakłócania jakichkolwiek istniejących baz kodu rozwiązania.<br/><br/> Aplikacja internetowa zostanie skonfigurowana przy użyciu wielu wystąpień, eliminując pojedynczy punkt awarii.<br/><br/> Włączone zostanie skalowanie automatyczne umożliwiające aplikacji obsługę zmieniającego się ruchu.<br/><br/> Przeniesienie do usług PaaS oznacza, że firma Contoso może wycofać przestarzałe rozwiązania działające w systemie operacyjnym Windows Serwer 2008 R2.<br/><br/> Usługa Cosmos DB ma wbudowaną funkcję odporności na uszkodzenia, która nie wymaga konfiguracji przez firmę Contoso. Oznacza to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Kontenery są bardziej złożone niż inne opcje migracji. Konieczność szkolenia może być problemem dla firmy Contoso. Kontenery wprowadzają nowy poziom złożoności, który mimo konieczności szkolenia ma wiele zalet.<br/><br/> Zespół operacyjny firmy Contoso musi poszerzyć swoje kompetencje, aby nauczyć się obsługi platformy Azure, kontenerów i mikrousług używanych przez aplikację.<br/><br/> Firma Contoso nie wdrożyła jeszcze w pełni metodyki DevOps dla całego rozwiązania. Firma Contoso musi wziąć to pod uwagę podczas wdrażania w usługach AKS, Azure Functions i Azure App Service.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso aprowizuje usługi ACR, AKS i Cosmos DB.
2. Aprowizuje infrastrukturę na potrzeby wdrożenia, w tym aplikację internetową usługi Azure App Service, konto magazynu, funkcję i interfejs API.
3. Po utworzeniu infrastruktury firma skompiluje swoje obrazy kontenerów mikrousług przy użyciu usługi Azure DevOps, która wypchnie je do usługi ACR.
4. Firma Contoso wdroży te mikrousługi w usłudze AKS przy użyciu skryptu programu PowerShell.
5. Na koniec wdroży funkcję i aplikację internetową.

    ![Proces migracji](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Upraszcza wdrażanie i obsługę platformy Kubernetes oraz zarządzanie nią. Zapewnia w pełni zarządzaną usługę organizowania kontenerów Kubernetes. | AKS to bezpłatna usługa. Płaci się wyłącznie za maszyny wirtualne, skojarzony magazyn i wykorzystane zasoby sieciowe. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/kubernetes-service).
[Azure Functions](https://azure.microsoft.com/services/functions) | Przyspiesza opracowywanie zawartości dzięki opartemu na zdarzeniach bezserwerowemu środowisku obliczeniowemu. Umożliwia skalowanie na żądanie. | Płaci się tylko za wykorzystane zasoby. Plan jest rozliczany na podstawie liczby wykonań i użycia zasobów na sekundę. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/functions).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Przechowuje obrazy dla dowolnego typu wdrożeń kontenerów. | Koszt zależy od funkcji, magazynu i czasu użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/container-registry).
[Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Szybko kompiluj, wdrażaj i skaluj aplikacje internetowe, aplikacje mobilne i aplikacje interfejsów API klasy korporacyjnej działające na dowolnej platformie. | Opłaty za plany usługi App Service są naliczane co sekundę. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).

## <a name="prerequisites"></a>Wymagania wstępne

W tym scenariuszu firma Contoso potrzebuje następujących elementów:

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.
**Infrastruktura platformy Azure** | [Dowiedz się](./contoso-migration-infrastructure.md), jak firma Contoso skonfigurowała infrastrukturę platformy Azure.
**Wymagania wstępne dla deweloperów** | Firma Contoso potrzebuje następujących narzędzi na stacji roboczej dewelopera:<br/><br/> - [Visual Studio 2017 Community Edition: wersja 15,5](https://www.visualstudio.com)<br/><br/> Włączony pakiet roboczy platformy .NET.<br/><br/> [Git](https://git-scm.com)<br/><br/> [Azure PowerShell](https://azure.microsoft.com/downloads)<br/><br/> [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> Program [Docker CE (dla systemu Windows 10) lub Docker EE (dla systemu Windows Server)](https://docs.docker.com/docker-for-windows/install) skonfigurowany pod kątem korzystania z kontenerów systemu Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1: Inicjowanie obsługi AKS i ACR.** Firma Contoso aprowizuje zarządzany klaster usługi AKS i usługę ACR przy użyciu programu PowerShell.
> - **Krok 2. Kompilowanie kontenerów platformy Docker.** Firma skonfiguruje ciągłą integrację kontenerów platformy Docker przy użyciu usługi Azure DevOps i wypchnie je do usługi ACR.
> - **Krok 3. wdrażanie mikrousług zaplecza.** Firma wdroży resztę infrastruktury, która będzie używana przez mikrousługi zaplecza.
> - **Krok 4. wdrażanie infrastruktury frontonu.** Firma wdroży infrastrukturę frontonu, w tym usługę Blob Storage do przechowywania zdjęć zwierząt, usługę Cosmos DB i interfejs API przetwarzania obrazów.
> - **Krok 5. Migrowanie zaplecza.** Firma wdroży mikrousługi i uruchomi je w usłudze AKS w celu migracji zaplecza.
> - **Krok 6. publikowanie frontonu.** Firma opublikuje aplikację SmartHotel360 w usłudze App Service oraz aplikację funkcji, która będzie wywoływana przez usługę do przetwarzania zdjęć zwierząt.

## <a name="step-1-provision-back-end-resources"></a>Krok 1. Udostępnianie zasobów zaplecza

Administratorzy firmy Contoso uruchamiają skrypt wdrożenia w celu utworzenia zarządzanego klastra platformy Kubernetes przy użyciu usług AKS i Azure Container Registry (ACR).

- Instrukcje w tej sekcji korzystają z repozytorium **SmartHotel360-Azure-backend**.
- Repozytorium GitHub **SmartHotel360-Azure-backend** zawiera całe oprogramowanie potrzebne do tej części wdrożenia.  

### <a name="ensure-prerequisites"></a>Zapewnianie wymagań wstępnych

1. Przed rozpoczęciem Administratorzy firmy Contoso muszą upewnić się, że wszystkie wstępnie wymagane oprogramowanie zainstalowane na komputerze deweloperskim, którego używa do wdrożenia.
2. Klonują repozytorium lokalnie na maszynę deweloperską przy użyciu usługi Git: `git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git`

### <a name="provision-aks-and-acr"></a>Aprowizowanie usług AKS i ACR

Administratorzy firmy Contoso przeprowadzają aprowizację w następujący sposób:

1. Otwierają folder przy użyciu Visual Studio Code i przechodzi do katalogu **/Deploy/k8s** , który zawiera skrypt **Gen-AKS-ENV. ps1**.

2. Uruchamiają skrypt, aby utworzyć zarządzany klaster platformy Kubernetes za pomocą usług AKS i ACR.

   ![AKS](./media/contoso-migration-rebuild/aks1.png)

3. Po otwarciu pliku aktualizują parametr $location, używając wartości **eastus2**, i zapisują plik.

   ![AKS](./media/contoso-migration-rebuild/aks2.png)

4. Wybierają kolejno pozycje **View** (Widok)  > **Integrated Terminal** (Zintegrowany terminal), aby otworzyć zintegrowany terminal w programie Visual Studio Code.

   ![AKS](./media/contoso-migration-rebuild/aks3.png)

5. W zintegrowanym terminalu programu PowerShell logują się na platformie Azure przy użyciu polecenia Connect-AzureRmAccount. [Dowiedz się więcej](https://docs.microsoft.com/powershell/azure/get-started-azureps) o rozpoczynaniu pracy z programem PowerShell.

   ![AKS](./media/contoso-migration-rebuild/aks4.png)

6. Uwierzytelniają interfejs wiersza polecenia platformy Azure, uruchamiając polecenie **az login** i postępując według instrukcji uwierzytelniania w przeglądarce internetowej. [Dowiedz się więcej](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) na temat logowania za pomocą interfejsu wiersza polecenia platformy Azure.

   ![AKS](./media/contoso-migration-rebuild/aks5.png)

7. Uruchamiają następujące polecenie, przekazując nazwę grupy zasobów ContosoRG, nazwę klastra usługi AKS smarthotel-aks-eus2 i nazwę nowego rejestru.

   ```PowerShell
   .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
   ```

   ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Platforma Azure tworzy kolejną grupę zasobów, zawierającą zasoby dla klastra usługi AKS.

   ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. Po zakończeniu wdrażania instalują narzędzie wiersza polecenia **kubectl**. Narzędzie jest już zainstalowane w usłudze Azure CloudShell.

   ```console
   az aks install-cli
   ```

10. Sprawdzają połączenie z klastrem, uruchamiając polecenie **kubectl get nodes**. Węzeł ma taką sama nazwę jak maszyna wirtualna w automatycznie utworzonej grupie zasobów.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. Wykonują następujące polecenie, aby uruchomić pulpit nawigacyjny rozwiązania Kubernetes:

    ```console
    az aks browse --resource-group ContosoRG --name smarthotelakseus2
    ```

12. Pulpit nawigacyjny zostaje otwarty na nowej karcie przeglądarki. Jest to połączenie tunelowane, wykorzystujące interfejs wiersza polecenia platformy Azure.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Krok 2. Konfigurowanie potoku zaplecza

### <a name="create-an-azure-devops-project-and-build"></a>Tworzenie projektu i kompilacji usługi Azure DevOps

Firma Contoso tworzy projekt usługi Azure DevOps i konfiguruje kompilację ciągłej integracji w celu utworzenia kontenera, a następnie wypycha go do usługi ACR. Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).

1. Na stronie visualstudio.com tworzą nową organizację (**contosodevops360.visualstudio.com**) i konfigurują ją pod kątem korzystania z usługi Git.

2. Tworzą nowy projekt (**SmartHotelBackend**), korzystając z usługi Git do kontroli wersji i metody Agile do przepływu pracy.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png)

3. Importują [repozytorium GitHub](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)

4. W obszarze **Pipelines** (Potoki) wybierają pozycję **Build** (Kompilacja) i tworzą nowy potok przy użyciu repozytorium Git usługi Azure Repos jako źródła.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

5. Decydują się rozpocząć od pustego zadania.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)

6. Wybierają pozycję **Hosted Linux Preview** (Hostowana wersja zapoznawcza systemu Linux) dla potoku kompilacji.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)

7. W obszarze **Phase 1** (Faza 1) dodają zadanie **Docker Compose**. To zadanie kompiluje narzędzie Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)

8. Powtarzają czynność i dodają kolejne zadanie **Docker Compose**. To zadanie wypycha kontenery do usługi ACR.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. Wybierają pierwsze zadanie (kompilowania) i konfigurują kompilację przy użyciu subskrypcji platformy Azure, autoryzacji i usługi ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. Określają ścieżkę pliku **docker-compose.yaml** w folderze **src** repozytorium. Wybierają kompilowanie obrazów usługi i dołączają najnowszy tag. Gdy akcja zmieni się na **Build service images** (Kompilowanie obrazów usługi), nazwa zadania usługi Azure DevOps zmieni się na **Build services automatically** (Automatyczne kompilowanie usług).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Teraz konfigurowane zostanie drugie zadanie Docker (wypychanie). Wybierają subskrypcję oraz wystąpienie **smarthotelacreus2** usługi ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. Ponownie wprowadzają plik do pliku docker-compose.yaml, a następnie wybierają pozycję **Push service images** (Wypychanie obrazów usługi) i dołączają najnowszy tag. Gdy akcja zmieni się na **Push service images**, nazwa zadania usługi Azure DevOps zmieni się na **Push services automatically** (Automatyczne wypychanie usług).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. Gdy zadania usługi Azure DevOps zostaną skonfigurowane, firma Contoso zapisuje potok kompilacji i rozpoczyna proces kompilacji.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. Wybierają zadanie kompilacji, aby sprawdzić postęp.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. Po zakończeniu kompilacji usługa ACR pokazuje nowe repozytoria, które są wypełniane kontenerami używanymi przez mikrousługi.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Wdrażanie infrastruktury zaplecza

Mając utworzony klaster usługi AKS i skompilowane obrazy platformy Docker, administratorzy firmy Contoso wdrażają resztę infrastruktury, która będzie używana przez mikrousługi zaplecza.

- Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- W folderze **/deploy/k8s/arm** jest jeden skrypt do tworzenia wszystkich elementów.

Wdrożenie przebiega w następujący sposób:

1. Administratorzy otwierają wiersz polecenia dla deweloperów i używają polecenia az login, aby zalogować się przy użyciu subskrypcji platformy Azure.
2. Używają pliku deploy.cmd, aby wdrożyć zasoby platformy Azure w grupie zasobów ContosoRG i regionie EUS2, wpisując następujące polecenie:

    ```console
    .\deploy.cmd azuredeploy ContosoRG -c eastus2
    ```

    ![Wdrażanie zaplecza](./media/contoso-migration-rebuild/backend1.png)

3. W witrynie Azure Portal zapisują parametry połączenia dla każdej bazy danych do użycia w przyszłości.

    ![Wdrażanie zaplecza](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Tworzenie potoku wydania zaplecza

Teraz administratorzy firmy Contoso wykonują następujące czynności:

- Wdrażają kontroler ruchu przychodzącego serwera NGINX, aby umożliwić ruch przychodzący do usług.
- Wdrażają mikrousługi w klastrze usług AKS.
- Na początku aktualizują parametry połączenia mikrousług przy użyciu usługi Azure DevOps. Konfigurują nowy potok wydania Azure DevOps w celu wdrożenia mikrousług.
- Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- Niektóre ustawienia konfiguracji (na przykład Active Directory B2C) nie zostały omówione w tym artykule. Aby uzyskać więcej informacji na temat tych ustawień, przejrzyj repozytorium powyżej.

Tworzą potok:

1. W programie Visual Studio aktualizują plik **/deploy/k8s/config_local.yml**, używając zapisanych wcześniej informacji na temat parametrów połączenia baz danych.

    ![Połączenia baz danych](./media/contoso-migration-rebuild/back-pipe1.png)

2. Otwierają usługę Azure DevOps i w projekcie SmartHotel360 wybierają kolejno pozycje **Releases** (Wydania) i **+New Pipeline** (+ Nowy potok).

    ![Nowy potok](./media/contoso-migration-rebuild/back-pipe2.png)

3. Wybierają pozycję **Empty Job** (Puste zadanie), aby uruchomić potok bez szablonu.
4. Udostępniają nazwy etapów i potoków.

      ![Nazwa etapu](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Nazwa potoku](./media/contoso-migration-rebuild/back-pipe5.png)

5. Dodają artefakt.

     ![Dodawanie artefaktu](./media/contoso-migration-rebuild/back-pipe6.png)

6. Wybierają typ źródła **Git** i określają projekt, źródło oraz gałąź master dla aplikacji SmartHotel360.

    ![Ustawienia artefaktu](./media/contoso-migration-rebuild/back-pipe7.png)

7. Wybierają link zadania.

    ![Link zadania](./media/contoso-migration-rebuild/back-pipe8.png)

8. Dodają nowe zadanie usługi Azure PowerShell w celu uruchomienia skryptu programu PowerShell w środowisku platformy Azure.

    ![Program PowerShell na platformie Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. Wybierają subskrypcję platformy Azure dla zadania i wybierają skrypt **deploy.ps1** z repozytorium Git.

    ![Uruchamianie skryptu](./media/contoso-migration-rebuild/back-pipe10.png)

10. Dodają argumenty do skryptu. Skrypt usunie całą zawartość klastra (poza **ruchem przychodzącym** i **kontrolerem ruchu przychodzącego**) i wdroży mikrousługi.

    ![Argumenty skryptu](./media/contoso-migration-rebuild/back-pipe11.png)

11. Ustawiają preferowaną najnowszą wersję usługi Azure PowerShell i zapisują potok.

12. Wracają do strony **Release** (Wydanie) i ręcznie tworzą nowe wydanie.

    ![Nowe wydanie](./media/contoso-migration-rebuild/back-pipe12.png)

13. Wybierają utworzone wydanie, a następnie w obszarze **Actions** (Akcje) wybierają pozycję **Deploy** (Wdróż).

      ![Wdrażanie wydania](./media/contoso-migration-rebuild/back-pipe13.png)

14. Po zakończeniu wdrażania uruchamiają następujące polecenie w usłudze Azure Cloud Shell, aby sprawdzić stan usług: **kubectl get services**.

## <a name="step-3-provision-front-end-services"></a>Krok 3. Udostępnianie usług frontonu

Administratorzy firmy Contoso muszą wdrożyć infrastrukturę, która będzie używana przez aplikacje frontonu. Tworzą kontener obiektów blob do przechowywania obrazów zwierząt, bazę danych Cosmos do przechowywania dokumentów z informacjami o zwierzętach; oraz interfejs API przetwarzania obrazów dla witryny internetowej.

Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web).

### <a name="create-blob-storage-containers"></a>Tworzenie kontenerów w usłudze Blob Storage

1. W witrynie Azure Portal otwierają wcześniej utworzone konto magazynu i wybierają pozycję **Obiekty blob**.
2. Tworzą nowy kontener — **Pets** (Zwierzęta domowe) — ustawiając poziom dostępu publicznego na „kontener”. Użytkownicy będą mogli przekazywać zdjęcia swoich zwierząt do tego kontenera.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob1.png)

3. Tworzą drugi nowy kontener o nazwie **settings** (ustawienia). W tym kontenerze zostanie umieszczony plik ze wszystkimi ustawieniami aplikacji frontonu.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob2.png)

4. Zapisują szczegóły dostępu do konta magazynu w pliku tekstowym do użycia w przyszłości.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a>Aprowizowanie bazy danych Cosmos

Administratorzy firmy Contoso aprowizują bazę danych Cosmos, która będzie używana do przechowywania informacji o zwierzętach.

1. Tworzą wystąpienie usługi **Azure Cosmos DB** w portalu Azure Marketplace.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. Określają nazwę (**contosomarthotel**), wybierają interfejs API SQL i umieszczają usługę w produkcyjnej grupie zasobów ContosoRG, w głównym regionie Wschodnie stany USA 2.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. Dodają nową kolekcję do bazy danych z domyślną pojemnością i przepływnością.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. Zapisują informacje dotyczące połączenia z bazą danych do użycia w przyszłości.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Aprowizowanie interfejsu API przetwarzania obrazów

Administratorzy firmy Contoso aprowizują interfejs API przetwarzania obrazów. Interfejs API będzie wywoływany przez funkcję w celu oceny zdjęć przekazywanych przez użytkowników.

1. Tworzą wystąpienie interfejsu API **przetwarzania obrazów** w portalu Azure Marketplace.

     ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision1.png)

2. Aprowizują interfejs API (**smarthotelpets**) w produkcyjnej grupie zasobów ContosoRG w głównym regionie Wschodnie stany USA 2.

    ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision2.png)

3. Zapisują parametry połączenia interfejsu API w pliku tekstowym do użycia w przyszłości.

     ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Aprowizowanie aplikacji internetowej platformy Azure

Administratorzy firmy Contoso aprowizują aplikację internetową w witrynie Azure Portal.

1. Wybierają pozycję **Aplikacja internetowa** w portalu.

    ![Aplikacja internetowa](media/contoso-migration-rebuild/web-app1.png)

2. Podają nazwę aplikacji (**smarthotelcontoso**), wybierają system Windows do jej uruchomienia i umieszczają ją w produkcyjnej grupie zasobów **ContosoRG**. Tworzą nowe wystąpienie usługi Application Insights w celu monitorowania aplikacji.

    ![Nazwa aplikacji internetowej](media/contoso-migration-rebuild/web-app2.png)

3. Po zakończeniu przechodzą do adresu aplikacji, aby sprawdzić, czy została pomyślnie utworzona.

4. Teraz w witrynie Azure Portal tworzą miejsce przejściowe (staging) dla kodu. Potok będzie używał tego miejsca do wdrażania. To gwarantuje, że kod nie zostanie wprowadzony do produkcji, aż administratorzy nie przeprowadzą wydania.

    ![Miejsce przejściowe aplikacji internetowej](media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Aprowizowanie aplikacji funkcji platformy Azure

W witrynie Azure Portal administratorzy firmy Contoso aprowizują aplikację funkcji.

1. Wybierają pozycję **Aplikacja funkcji**.

   ![Tworzenie aplikacji funkcji](./media/contoso-migration-rebuild/function-app1.png)

2. Podają nazwę aplikacji (**smarthotelpetchecker**). Umieszczają aplikację w produkcyjnej grupie zasobów **ContosoRG**. Ustawiają lokalizację hostowania jako **Plan zużycia** i umieszczają aplikację w regionie Wschodnie stany USA 2. Zostanie utworzone nowe konto magazynu wraz z wystąpieniem usługi Application Insights do monitorowania.

   ![Ustawienia aplikacji funkcji](./media/contoso-migration-rebuild/function-app2.png)

3. Po wdrożeniu aplikacji przechodzą do adresu aplikacji, aby sprawdzić, czy została utworzona pomyślnie.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Krok 4. Konfigurowanie potoku frontonu

Administratorzy firmy Contoso tworzą dwa różne projekty dla witryny frontonu.

1. W usłudze Azure DevOps tworzą projekt **SmartHotelFrontend**.

   ![Projekt frontonu](./media/contoso-migration-rebuild/function-app1.png)

2. Importują repozytorium Git [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-public-web.git) do nowego projektu.

3. Dla aplikacji funkcji tworzą kolejny projekt usługi Azure DevOps (SmartHotelPetChecker) i importują repozytorium Git [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) do tego projektu.

### <a name="configure-the-web-app"></a>Konfigurowanie aplikacji internetowej

Teraz administratorzy firmy Contoso konfigurują aplikację internetową, która będzie korzystała z zasobów firmy Contoso.

1. Łączą się z projektem usługi Azure DevOps i klonują repozytorium lokalnie na inną maszynę deweloperską.
2. W programie Visual Studio otwierają folder, aby wyświetlić wszystkie pliki w repozytorium.

    ![Pliki repozytorium](./media/contoso-migration-rebuild/configure-webapp1.png)

3. Aktualizują konfigurację, wprowadzając potrzebne zmiany.

    - Po uruchomieniu aplikacja internetowa wyszukuje ustawienie aplikacji **SettingsUrl**.
    - Ta zmienna musi zawierać adres URL pliku konfiguracji.
    - Domyślne ustawienie to publiczny punkt końcowy.

4. Aktualizują plik /config-sample.json/sample.json.

    - Jest to plik konfiguracji witryny internetowej używany w przypadku korzystania z publicznego punktu końcowego.
    - Edytują sekcje **urls** i **pets_config**, wpisując wartości dla punktów końcowych interfejsu API usługi AKS, kont magazynu i bazy danych Cosmos.
    - Adresy URL powinny odpowiadać nazwie DNS nowej aplikacji internetowej, która zostanie utworzona przez firmę Contoso.
    - W przypadku firmy Contoso jest to **smarthotelcontoso.eastus2.cloudapp.azure.com**.

    ![Ustawienia w pliku JSON](./media/contoso-migration-rebuild/configure-webapp2.png)

5. Po zaktualizowaniu pliku zmieniają jego nazwę na **smarthotelsettingsurl** i przekazują go do magazynu obiektów blob utworzonego wcześniej.

    ![Zmiana nazwy i przekazanie pliku](./media/contoso-migration-rebuild/configure-webapp3.png)

6. Wybierają plik, aby uzyskać adres URL. Podczas ściągania plików konfiguracji aplikacja korzysta z adresu URL.

    ![Adres URL aplikacji](./media/contoso-migration-rebuild/configure-webapp4.png)

7. W pliku **appsettings.Production.json** aktualizują ustawienie **SettingsURL**, wprowadzając adres URL nowego pliku.

    ![Aktualizowanie adresu URL](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-azure-app-service"></a>Wdrażanie witryny internetowej w usłudze Azure App Service

Administratorzy firmy Contoso mogą teraz opublikować witrynę internetową.

1. Otwierają usługę Azure DevOps i w projekcie **SmartHotelFrontend** w obszarze **Builds and Releases** (Kompilacje i wydania) wybierają pozycję **+New Pipeline** (+ Nowy potok).
2. Wybierają pozycję **Azure DevOps Git** jako źródło.
3. Wybierają szablon **ASP.NET Core**.
4. Weryfikują potok i sprawdzają, czy wybrano opcje **Publish Web Projects** (Publikowanie projektów internetowych) i **Zip Published Projects** (Kompresowanie opublikowanych projektów do plików ZIP).

    ![Ustawienia potoku](./media/contoso-migration-rebuild/vsts-publishfront2.png)

5. W obszarze **Triggers** (Wyzwalacze) włączają ciągłą integrację i dodają gałąź master. Gwarantuje to, że po każdym wprowadzeniu nowego kodu do gałęzi master będzie uruchamiany potok kompilacji.

    ![Integracja ciągła](./media/contoso-migration-rebuild/vsts-publishfront3.png)

6. Wybierają pozycję **Save & Queue** (Zapisz i dodaj do kolejki), aby rozpocząć kompilację.
7. Po zakończeniu kompilacji konfigurują potok wydania, wybierając pozycję **Azure App Service Deployment** (Wdrożenie usługi Azure App Service).
8. Wprowadzają nazwę etapu **Staging** (Przygotowanie).

    ![Nazwa środowiska](./media/contoso-migration-rebuild/vsts-publishfront4.png)

9. Dodają artefakt i wybierają właśnie skonfigurowaną kompilację.

     ![Dodawanie artefaktu](./media/contoso-migration-rebuild/vsts-publishfront5.png)

10. Wybierają ikonę błyskawicy na artefakcie i włączają ciągłe wdrażanie.

    ![Ciągłe wdrażanie](./media/contoso-migration-rebuild/vsts-publishfront6.png)
11. W obszarze **Environment** (Środowisko) wybierają pozycję **1 job, 1 task** (1 zadanie, 1 podzadanie) w obszarze **Staging**.
12. Po wybraniu nazwy subskrypcji i aplikacji otwierają zadanie **Deploy Azure App Service** (Wdrażanie usługi Azure App Service). Wdrożenie jest skonfigurowane pod kątem korzystania z miejsca wdrożenia **staging**. W ten sposób kod jest automatycznie kompilowany w tym miejscu do przeglądu i zatwierdzenia.

     ![Gniazdo](./media/contoso-migration-rebuild/vsts-publishfront7.png)

13. W obszarze **Pipeline** (Potok) dodają nowy etap.

    ![Nowe środowisko](./media/contoso-migration-rebuild/vsts-publishfront8.png)

14. Wybierają pozycję **Azure App Service deployment with slot** (Wdrożenie usługi Azure App Service z miejscem wdrożenia) i nadają środowisku nazwę **Prod**.
15. Wybierają pozycję **1 job, 2 tasks** (1 zadanie, 2 podzadania), a następnie wybierają subskrypcję, nazwę usługi App Service oraz miejsce wdrożenia **staging**.

    ![Nazwa środowiska](./media/contoso-migration-rebuild/vsts-publishfront10.png)

16. Usuwają pozycję **Deploy Azure App Service to Slot** (Wdrażanie usługi Azure App Service do miejsca wdrożenia) z potoku. Została tam umieszczona w poprzednich krokach.

    ![Usuwanie z potoku](./media/contoso-migration-rebuild/vsts-publishfront11.png)

17. Zapisują potok. W potoku wybierają pozycję **Post-deployment conditions** (Warunki po wdrożeniu).

    ![Po wdrożeniu](./media/contoso-migration-rebuild/vsts-publishfront12.png)

18. Włączają pozycję **Post-deployment approvals** (Zatwierdzenia po wdrożeniu) i dodają lidera zespołu deweloperskiego jako osobę zatwierdzającą.

    ![Zatwierdzenie po wdrożeniu](./media/contoso-migration-rebuild/vsts-publishfront13.png)

19. W potoku kompilacji ręcznie uruchamiają kompilację. To powoduje wyzwolenie nowego potoku wydania, który wdraża witrynę w przejściowym miejscu wdrożenia (staging). W przypadku firmy Contoso adres URL tego miejsca to `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Po zakończeniu kompilacji i wdrożeniu wydania w miejscu wdrożenia usługa Azure DevOps Services wysyła wiadomość e-mail do lidera zespołu deweloperskiego w celu zatwierdzenia.

21. Lider zespołu deweloperskiego wybiera pozycję **View approval** (Wyświetl zatwierdzenie) i może zatwierdzić lub odrzucić żądanie w portalu usługi Azure DevOps.

    ![Wiadomość e-mail dotycząca zatwierdzenia](./media/contoso-migration-rebuild/vsts-publishfront14.png)

22. Lider wprowadza komentarze i zatwierdza wdrożenie. To powoduje zamianę miejsc wdrożenia **staging** i **prod** i wprowadzenie kompilacji do środowiska produkcyjnego.

    ![Zatwierdzanie i zamiana](./media/contoso-migration-rebuild/vsts-publishfront15.png)

23. Potok kończy zamianę.

    ![Kończenie zamiany](./media/contoso-migration-rebuild/vsts-publishfront16.png)

24. Zespół sprawdza miejsce **prod**, aby potwierdzić, że aplikacja internetowa jest w środowisku produkcyjnym pod adresem `https://smarthotelcontoso.azurewebsites.net/`.

### <a name="deploy-the-petchecker-function-app"></a>Wdrażanie aplikacji funkcji PetChecker

Administratorzy firmy Contoso wdrażają aplikację w następujący sposób.

1. Klonują repozytorium lokalnie na maszynę deweloperską, nawiązując połączenie z projektem usługi Azure DevOps.
2. W programie Visual Studio otwierają folder, aby wyświetlić wszystkie pliki w repozytorium.
3. Otwierają plik **src/PetCheckerFunction/local.settings.json** i dodają ustawienia aplikacji dotyczące magazynu, bazy danych Cosmos i interfejsu API przetwarzania obrazów.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function5.png)

4. Zatwierdzają kod i synchronizują go z powrotem z usługą Azure DevOps, co powoduje wypchnięcie zmian.
5. Dodają nowy potok kompilacji i wybierają źródło **Azure DevOps Git**.
6. Wybierają szablon **ASP.NET Core (.NET Framework)** .
7. Akceptują wartości domyślne w szablonie.
8. W obszarze **Triggers** (Wyzwalacze) wybierają pozycję **Enable continuous integration** (Włącz ciągłą integrację), a następnie pozycję **Save & Queue** (Zapisz i dodaj do kolejki), aby rozpocząć kompilację.
9. Po zakończeniu kompilacji tworzą potok wydania, dodając pozycję **Azure App Service deployment with slot** (Wdrożenie usługi Azure App Service z miejscem wdrożenia).
10. Nadają środowisku nazwę **Prod** i wybierają subskrypcję. W polu **App type** (Typ aplikacji) ustawiają wartość **Function App** (Aplikacja funkcji) i wprowadzają **smarthotelpetchecker** jako nazwę usługi aplikacji.

    ![Aplikacja funkcji](./media/contoso-migration-rebuild/petchecker2.png)

11. Dodają artefakt **Build** (Kompilacja).

    ![Artefakt](./media/contoso-migration-rebuild/petchecker3.png)

12. Włączają pozycję **Continuous deployment trigger** (Wyzwalacz ciągłego wdrażania) i wybierają pozycję **Save** (Zapisz).
13. Wybierają pozycję **Queue new build** (Dodaj nową kompilację do kolejki), aby uruchomić pełny potok ciągłej integracji/ciągłego wdrażania.
14. Wdrożona funkcja pojawi się w witrynie Azure Portal ze stanem **Uruchomiona**.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function6.png)

15. Przechodzą do aplikacji, aby sprawdzić, czy aplikacja Pet Checker działa zgodnie z oczekiwaniami pod adresem [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets).

16. Wybierają awatar, aby przekazać zdjęcie.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function7.png)

17. Pierwsze zdjęcie, które chcą sprawdzić, przedstawia małego psa.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function8.png)

18. Aplikacja zwraca komunikat o akceptacji.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function9.png)

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi teraz w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

- Firma Contoso musi upewnić się, że nowe bazy danych są bezpieczne. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).
- Aplikacja musi zostać zaktualizowana w celu korzystania z protokołu SSL z certyfikatami. Wystąpienie kontenera należy wdrożyć ponownie, aby odpowiadało na porcie 443.
- Firma Contoso powinna rozważyć użycie usługi Key Vault w celu chronienia wpisów tajnych aplikacji usługi Service Fabric. [Dowiedz się więcej](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Kopie zapasowe i odzyskiwanie po awarii

- Firma Contoso musi zapoznać się z wymaganiami tworzenia kopii zapasowych dla usługi Azure SQL Database. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Firma Contoso powinna rozważyć wdrożenie grup trybu failover dla bazy danych SQL w celu zapewnienia regionalnego przechodzenia bazy danych w tryb failover. [Dowiedz się więcej](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).
- Firma Contoso może użyć replikacji geograficznej dla jednostek SKU w warstwie Premium usługi ACR. [Dowiedz się więcej](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Baza danych Cosmos DB automatycznie tworzy kopie zapasowe. Firma Contoso może [dowiedzieć się więcej](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) na temat tego procesu.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma Contoso włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso ponownie skompilowała aplikację SmartHotel360 na platformie Azure. Lokalna maszyna wirtualna frontonu aplikacji została ponownie skompilowana w aplikacjach internetowych usługi Azure App Service. Zaplecze aplikacji zostało skompilowane przy użyciu mikrousług wdrożonych w kontenerach zarządzanych przez usługę Azure Kubernetes Service (AKS). Firma Contoso rozszerzyła funkcjonalność aplikacji o aplikację do obsługi zdjęć zwierząt.

## <a name="suggested-skills"></a>Sugerowane umiejętności

Microsoft Learn to nowe podejście do uczenia się. Gotowość do nowych umiejętności i obowiązków, które są związane z wdrażaniem chmury, nie przychodzi łatwo. Microsoft Learn oferuje bardziej satysfakcjonującą metodę praktycznego uczenia się, która ułatwia szybsze osiąganie celów. Zdobywaj punkty i poziomy i osiągaj więcej.

Poniżej przedstawiono kilka przykładów dostosowanych ścieżek szkoleniowych na Microsoft Learn, które są wyrównane do aplikacji Contoso SmartHotel360 na platformie Azure.

[Wdrażanie witryny sieci Web na platformie Azure za pomocą Azure App Service](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service/): aplikacje sieci Web na platformie Azure umożliwiają łatwe publikowanie i zarządzanie witryną sieci Web bez konieczności pracy z podstawowymi serwerami, magazynem lub zasobami sieciowymi. Zamiast tego możesz skoncentrować się na funkcjach witryny internetowej i polegać na niezawodnej platformie Azure w zakresie zabezpieczania dostępu do witryny.

[Przetwarzaj i Klasyfikuj obrazy za pomocą usług Azure poznawczej](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services/): usługa Azure Cognitive Services oferuje wbudowaną funkcję, która umożliwia korzystanie z funkcji przetwarzania obrazów w aplikacjach. Dowiedz się, jak korzystać z usług poznawczych, aby wykrywać twarze, Tagi i klasyfikować obrazy oraz identyfikować obiekty.
