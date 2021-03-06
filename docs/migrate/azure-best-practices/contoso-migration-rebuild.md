---
title: Ponowne kompilowanie aplikacji lokalnej na platformie Azure
description: Dowiedz się, jak firma Contoso ponownie kompiluje aplikację na platformie Azure przy użyciu Azure App Service, usługi Azure Kubernetes Service, Azure Cosmos DB, Azure Functions i Cognitive Services platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: db53dbb9e024cdde817b80a79dae3e3e789d9c16
ms.sourcegitcommit: 6fef15cc3a8af725dc743e19f127513bc58dd257
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/27/2020
ms.locfileid: "84023546"
---
<!-- docsTest:ignore SmartHotel360 SmartHotel360-Backend Pet.Checker vcenter.contoso.com contoso-datacenter git aks ContosoRG PetCheckerFunction -->

<!-- cSpell:ignore givenscj WEBVM SQLVM contosohost vcenter contosodc smarthotel contososmarthotel smarthotelcontoso smarthotelpetchecker petchecker smarthotelakseus smarthotelacreus smarthotelpets kubectl contosodevops visualstudio azuredeploy cloudapp smarthotelsettingsurl appsettings -->

# <a name="rebuild-an-on-premises-app-on-azure"></a>Ponowne kompilowanie aplikacji lokalnej na platformie Azure

W tym artykule pokazano, jak fikcyjna firma Contoso ponownie kompiluje dwuwarstwową aplikację .NET systemu Windows uruchomioną na maszynach wirtualnych VMware w ramach migracji do platformy Azure. Firma Contoso migruje maszynę wirtualną frontonu aplikacji do aplikacji internetowej usługi Azure App Service. Zaplecze aplikacji jest tworzone przy użyciu mikrousług wdrożonych w kontenerach zarządzanych przez usługę Azure Kubernetes Service (AKS). Witryna współdziała z usługą Azure Functions w celu udostępnienia funkcji obsługi zdjęć zwierząt domowych.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso się rozwija i chce zapewnić klientom zróżnicowane środowiska w witrynach internetowych firmy Contoso.
- **Zwinność.** Firma Contoso chce być w stanie szybciej reagować na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej.
- **Zasięgu.** Po pomyślnym rozwojem firmy firma Contoso IT musi zapewnić systemy, które mogą rosnąć w tym samym tempie.
- **Obniżyć koszty.** Firma Contoso chce zminimalizować koszty licencjonowania.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso określił wymagania związane z aplikacją w tym procesie migracji. Na podstawie tych wymagań określono najlepszą metodę migracji:

- Na platformie Azure aplikacja będzie miała tak samo krytyczne znaczenie jak teraz. Powinna być wydajna i łatwa w skalowaniu.
- Aplikacja nie powinna korzystać ze składników IaaS. Wszystko powinno być skonstruowane tak, aby możliwe było korzystanie z usług PaaS lub usług bezserwerowych.
- Kompilacje aplikacji powinny działać w usługach w chmurze, a kontenery powinny znajdować się w prywatnym rejestrze kontenerów dla całego przedsiębiorstwa w chmurze.
- Usługa interfejsu API używana do obsługi zdjęć zwierząt powinna być dokładna i niezawodna w rzeczywistych warunkach, ponieważ decyzje podjęte przez aplikację muszą być uznawane w należących do firmy hotelach. W hotelach będzie mogło przebywać każde zwierzę, które otrzyma zezwolenie na dostęp w aplikacji.
- Aby spełnić wymagania dotyczące potoku DevOps, firma Contoso będzie używać repozytorium Git w Azure Repos do zarządzania kodem źródłowym. Do kompilowania kodu i wdrażania go w usługach Azure App Service, Azure Functions i AKS będą używane zautomatyzowane kompilacje i wydania.
- Mikrousługi na zapleczu oraz witryna internetowa na frontonie wymagają użycia różnych potoków ciągłej integracji/ciągłego wdrażania.
- Usługi zaplecza i aplikacja internetowa frontonu mają inny cykl wydawania. Aby spełnić to wymaganie, wdrażane są dwa różne potoki.
- Firma Contoso potrzebuje funkcji zatwierdzania wszystkich wdrożeń witryny internetowej frontonu przez kierownictwo, a potok ciągłej integracji/ciągłego wdrażania musi ją zapewnić.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które będą używane do tego celu.

### <a name="current-app"></a>Bieżąca aplikacja

- Aplikacja lokalna SmartHotel360 jest podzielona na warstwy, które znajdują się na dwóch maszynach wirtualnych (WEBVM i SQLVM).
- Maszyny wirtualne znajdują się na VMware ESXi hosta **contosohost1.contoso.com** (wersja 6,5).
- Środowisko VMware jest zarządzane przez vCenter Server 6,5 (**vCenter.contoso.com**), uruchomione na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (**contoso-Datacenter**) z lokalnym kontrolerem domeny (**ContosoDC1**).
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

### <a name="proposed-architecture"></a>Proponowana architektura

- Fronton aplikacji jest wdrażany jako aplikacja sieci Web Azure App Service w podstawowym regionie platformy Azure.
- Funkcja platformy Azure umożliwia przekazywanie zdjęć zwierząt, a witryna współdziała z tą funkcją.
- Funkcja Photo PET używa interfejs API przetwarzania obrazów platformy Azure Cognitive Services wraz z Azure Cosmos DB.
- Zaplecze witryny jest utworzone przy użyciu mikrousług. Zostaną one wdrożone w kontenerach zarządzanych w AKS.
- Kontenery zostaną skompilowane przy użyciu usługi Azure DevOps i wypchnięte do Azure Container Registry.
- Na chwilę obecną firma Contoso będzie ręcznie wdrażała aplikację internetową i kod funkcji przy użyciu programu Visual Studio.
- Mikrousługi zostaną wdrożone przy użyciu skryptu programu PowerShell, który wywołuje narzędzia wiersza polecenia rozwiązania Kubernetes.

    ![Architektura scenariusza](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Użycie usług PaaS i rozwiązań bezserwerowych w przypadku kompleksowego wdrożenia znacząco skraca czas, który firma Contoso musi przeznaczyć na zarządzanie. <br><br> Przejście do architektury opartej na mikrousługach pozwala firmie Contoso łatwo rozciągnąć rozwiązanie w miarę upływu czasu. <br><br> Nową funkcję można uruchomić w trybie online bez zakłócania jakichkolwiek istniejących baz kodu rozwiązania. <br><br> Aplikacja internetowa zostanie skonfigurowana przy użyciu wielu wystąpień, eliminując pojedynczy punkt awarii. <br><br> Włączone zostanie skalowanie automatyczne umożliwiające aplikacji obsługę zmieniającego się ruchu. <br><br> Przeniesienie do usług PaaS oznacza, że firma Contoso może wycofać przestarzałe rozwiązania działające w systemie operacyjnym Windows Serwer 2008 R2. <br><br> Azure Cosmos DB ma wbudowaną odporność na uszkodzenia, która nie wymaga konfiguracji przez firmę contoso. Oznacza to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Kontenery są bardziej złożone niż inne opcje migracji. Konieczność szkolenia może być problemem dla firmy Contoso. Wprowadzają one nowy poziom złożoności, który zapewnia wartość pomimo krzywej. <br><br> Zespół operacyjny firmy Contoso musi poszerzyć swoje kompetencje, aby nauczyć się obsługi platformy Azure, kontenerów i mikrousług używanych przez aplikację. <br><br> Firma Contoso nie wdrożyła jeszcze w pełni metodyki DevOps dla całego rozwiązania. Firma Contoso musi wziąć to pod uwagę podczas wdrażania w usługach AKS, Azure Functions i Azure App Service.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

1. Firma Contoso ma postanowienia Azure Container Registry, AKS i Azure Cosmos DB.
2. Firma Contoso inicjuje obsługę infrastruktury wdrożenia, w tym Azure App Service aplikacji sieci Web, konta magazynu, funkcji i interfejsu API.
3. Po utworzeniu infrastruktury zostaną skompilowane obrazy kontenerów mikrousług za pomocą usługi Azure DevOps, które wypychają je do rejestru kontenerów.
4. Firma Contoso wdroży te mikrousługi w usłudze AKS przy użyciu skryptu programu PowerShell.
5. Na koniec wdroży funkcję i aplikację internetową.

    ![Proces migracji](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[AKS](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Upraszcza wdrażanie i obsługę platformy Kubernetes oraz zarządzanie nią. Zapewnia w pełni zarządzaną usługę organizowania kontenerów Kubernetes. | AKS to bezpłatna usługa. Płaci się wyłącznie za maszyny wirtualne, skojarzony magazyn i wykorzystane zasoby sieciowe. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/kubernetes-service).
[Azure Functions](https://azure.microsoft.com/services/functions) | Przyspiesza opracowywanie zawartości dzięki opartemu na zdarzeniach bezserwerowemu środowisku obliczeniowemu. Umożliwia skalowanie na żądanie. | Płaci się tylko za wykorzystane zasoby. Plan jest rozliczany na podstawie liczby wykonań i użycia zasobów na sekundę. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/functions).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Przechowuje obrazy dla dowolnego typu wdrożeń kontenerów. | Koszt zależy od funkcji, magazynu i czasu użytkowania. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/container-registry).
[Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Zapewnia możliwość szybkiego kompilowania, wdrażania i skalowania aplikacji internetowych, aplikacji mobilnych i aplikacji interfejsów API klasy korporacyjnej działających na dowolnej platformie. | Opłaty za plany usługi App Service są naliczane co sekundę. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).

## <a name="prerequisites"></a>Wymagania wstępne

W tym scenariuszu firma Contoso potrzebuje następujących elementów:

<!-- markdownlint-disable MD033 -->

| **Wymagania** | **Szczegóły** |
| --- | --- |
| Subskrypcja platformy Azure | <li> Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial). <li> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje. <li> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora. |
| Infrastruktura platformy Azure | <li> Dowiedz się, [jak firma Contoso konfiguruje infrastrukturę platformy Azure](./contoso-migration-infrastructure.md). |
| Wymagania wstępne dla deweloperów | Firma Contoso potrzebuje następujących narzędzi na stacji roboczej dewelopera: <li>  [Visual Studio 2017 Community Edition: wersja 15,5](https://visualstudio.microsoft.com) <li> Włączony pakiet roboczy platformy .NET. <li> [Git](https://git-scm.com) <li> [Azure PowerShell](https://azure.microsoft.com/downloads) <li> [Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) <li> Program [Docker CE (dla systemu Windows 10) lub Docker EE (dla systemu Windows Server)](https://docs.docker.com/docker-for-windows/install) skonfigurowany pod kątem korzystania z kontenerów systemu Windows. |

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Udostępnianie AKS i Azure Container Registry.** Firma Contoso inicjuje zarządzany klaster AKS i rejestr kontenerów za pomocą programu PowerShell.
> - **Krok 2. Kompilowanie kontenerów platformy Docker.** Konfigurowanie ciągłej integracji (CI) dla kontenerów platformy Docker za pomocą usługi Azure DevOps i wypychanie ich do rejestru kontenerów.
> - **Krok 3. wdrażanie mikrousług zaplecza.** Firma wdroży resztę infrastruktury, która będzie używana przez mikrousługi zaplecza.
> - **Krok 4. wdrażanie infrastruktury frontonu.** Wdrażają one infrastrukturę frontonu, w tym usługę BLOB Storage dla telefonów PET, Azure Cosmos DB i interfejs API przetwarzania obrazów.
> - **Krok 5. Migrowanie zaplecza.** Firma wdroży mikrousługi i uruchomi je w usłudze AKS w celu migracji zaplecza.
> - **Krok 6. publikowanie frontonu.** Firma opublikuje aplikację SmartHotel360 w usłudze App Service oraz aplikację funkcji, która będzie wywoływana przez usługę do przetwarzania zdjęć zwierząt.

## <a name="step-1-provision-back-end-resources"></a>Krok 1. Udostępnianie zasobów zaplecza

Administratorzy firmy Contoso uruchamiają skrypt wdrażania, aby utworzyć zarządzany klaster Kubernetes przy użyciu AKS i Azure Container Registry.

- Instrukcje w tej sekcji korzystają z repozytorium **SmartHotel360-zaplecza** .
- Repozytorium GitHub **SmartHotel360-zaplecza** zawiera wszystkie oprogramowanie dla tej części wdrożenia.

### <a name="ensure-prerequisites"></a>Zapewnianie wymagań wstępnych

1. Przed rozpoczęciem Administratorzy firmy Contoso muszą upewnić się, że wszystkie wstępnie wymagane oprogramowanie zainstalowane na komputerze deweloperskim, którego używa do wdrożenia.
2. Klonują repozytorium lokalnie na maszynę deweloperską przy użyciu usługi Git: 

    `git clone https://github.com/Microsoft/SmartHotel360-Backend.git`

### <a name="provision-aks-and-azure-container-registry"></a>Udostępnianie AKS i Azure Container Registry

Administratorzy firmy Contoso przeprowadzają aprowizację w następujący sposób:

1. Otwierają folder przy użyciu Visual Studio Code i przejdź do katalogu **/Deploy/k8s** , który zawiera skrypt **Gen-AKS-ENV. ps1**.

2. Uruchamiają one skrypt, aby utworzyć zarządzany klaster Kubernetes przy użyciu AKS i Azure Container Registry.

    ![AKS](./media/contoso-migration-rebuild/aks1.png)

3. Po otwarciu pliku aktualizują parametr $location, używając wartości **eastus2**, i zapisują plik.

    ![AKS](./media/contoso-migration-rebuild/aks2.png)

4. Wybierają opcję **Wyświetl**  >  **zintegrowany terminal** , aby otworzyć zintegrowany terminal w Visual Studio Code.

    ![AKS](./media/contoso-migration-rebuild/aks3.png)

5. W zintegrowanym terminalu programu PowerShell logują się do platformy Azure przy użyciu `Connect-AzureRmAccount` polecenia. Aby uzyskać więcej informacji, zobacz Rozpoczynanie [pracy z programem PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

    ![AKS](./media/contoso-migration-rebuild/aks4.png)

6. Umożliwiają one uwierzytelnianie interfejsu wiersza polecenia platformy Azure, uruchamiając `az login` polecenie i postępując zgodnie z instrukcjami dotyczącymi uwierzytelniania przy użyciu przeglądarki sieci Web. [Dowiedz się więcej](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest) na temat logowania za pomocą interfejsu wiersza polecenia platformy Azure.

    ![AKS](./media/contoso-migration-rebuild/aks5.png)

7. Uruchamiają następujące polecenie, przekazując nazwę grupy zasobów **ContosoRG**, nazwę klastra AKS **Smarthotel-AKS-eus2**i nową nazwę rejestru.

    `.\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2`

    ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Platforma Azure tworzy kolejną grupę zasobów, zawierającą zasoby dla klastra usługi AKS.

    ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. Po zakończeniu wdrożenia zainstaluje `kubectl` Narzędzie wiersza polecenia. Narzędzie jest już zainstalowane na Azure Cloud Shell.

    `az aks install-cli`

10. Weryfikują połączenie z klastrem, uruchamiając `kubectl get nodes` polecenie. Węzeł ma taką sama nazwę jak maszyna wirtualna w automatycznie utworzonej grupie zasobów.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. Wykonują następujące polecenie, aby uruchomić pulpit nawigacyjny rozwiązania Kubernetes:

    `az aks browse --resource-group ContosoRG --name smarthotelakseus2`

12. Pulpit nawigacyjny zostaje otwarty na nowej karcie przeglądarki. Jest to połączenie tunelowane, wykorzystujące interfejs wiersza polecenia platformy Azure.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Krok 2. Konfigurowanie potoku zaplecza

### <a name="create-an-azure-devops-project-and-build"></a>Tworzenie projektu i kompilacji usługi Azure DevOps

Firma Contoso tworzy projekt usługi Azure DevOps i konfiguruje kompilację elementu konfiguracji w celu utworzenia kontenera, a następnie wypchnięcie go do rejestru kontenerów. Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-zaplecza](https://github.com/Microsoft/SmartHotel360-Backend) .

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

8. Powtarzają czynność i dodają kolejne zadanie **Docker Compose**. Ta jedna wypychanie kontenerów do rejestru kontenerów.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. Wybierają pierwsze zadanie (do skompilowania) i konfiguruje kompilację przy użyciu subskrypcji platformy Azure, autoryzacji i rejestru kontenerów.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. Określają ścieżkę pliku **docker-compose.yaml** w folderze **src** repozytorium. Wybierają kompilowanie obrazów usługi i dołączają najnowszy tag. Gdy akcja zmieni się na **Build service images** (Kompilowanie obrazów usługi), nazwa zadania usługi Azure DevOps zmieni się na **Build services automatically** (Automatyczne kompilowanie usług).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Teraz konfigurowane zostanie drugie zadanie Docker (wypychanie). Wybierają one subskrypcję i rejestr kontenerów **smarthotelacreus2** .

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. Ponownie wprowadza plik do pliku Docker-Zredaguj. YAML, a następnie wybierz opcję **obrazy usługi wypychanej** i Dołącz najnowszy tag. Gdy akcja zmieni się na **Push service images**, nazwa zadania usługi Azure DevOps zmieni się na **Push services automatically** (Automatyczne wypychanie usług).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. Gdy zadania usługi Azure DevOps zostaną skonfigurowane, firma Contoso zapisuje potok kompilacji i rozpoczyna proces kompilacji.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. Wybierają zadanie kompilacji, aby sprawdzić postęp.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. Po zakończeniu kompilacji rejestr kontenerów pokazuje nowe repozytoria, które są wypełnione kontenerami używanymi przez mikrousługi.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Wdrażanie infrastruktury zaplecza

Mając utworzony klaster usługi AKS i skompilowane obrazy platformy Docker, administratorzy firmy Contoso wdrażają resztę infrastruktury, która będzie używana przez mikrousługi zaplecza.

- Instrukcje w sekcji korzystają z repozytorium [SmartHotel360-zaplecza](https://github.com/Microsoft/SmartHotel360-Backend) .
- W folderze **/deploy/k8s/arm** jest jeden skrypt do tworzenia wszystkich elementów.

Wdrożenie przebiega w następujący sposób:

1. Otwierają one wiersz polecenia dewelopera i używają polecenia `az login` dla subskrypcji platformy Azure.

2. Używają one pliku Deploy. cmd do wdrażania zasobów platformy Azure w **ContosoRG** grupy zasobów i **EUS2** , wpisując następujące polecenie:

    `.\deploy.cmd azuredeploy ContosoRG -c eastus2`

    ![Wdrażanie zaplecza](./media/contoso-migration-rebuild/backend1.png)

3. W witrynie Azure Portal zapisują parametry połączenia dla każdej bazy danych do użycia w przyszłości.

    ![Wdrażanie zaplecza](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Tworzenie potoku wydania zaplecza

Teraz administratorzy firmy Contoso wykonują następujące czynności:

- Wdrażają kontroler ruchu przychodzącego serwera NGINX, aby umożliwić ruch przychodzący do usług.
- Wdrażają mikrousługi w klastrze usług AKS.
- Na początku aktualizują parametry połączenia mikrousług przy użyciu usługi Azure DevOps. Konfigurują nowy potok wydania Azure DevOps w celu wdrożenia mikrousług.
- Instrukcje w tej sekcji korzystają z repozytorium [SmartHotel360-zaplecza](https://github.com/Microsoft/SmartHotel360-Backend) .
- Niektóre ustawienia konfiguracji (na przykład Active Directory B2C) nie zostały omówione w tym artykule. Aby uzyskać więcej informacji na temat tych ustawień, przejrzyj repozytorium powyżej.

Tworzą potok:

1. W programie Visual Studio aktualizują plik **/deploy/k8s/config_local.yml**, używając zapisanych wcześniej informacji na temat parametrów połączenia baz danych.

    ![Połączenia bazy danych](./media/contoso-migration-rebuild/back-pipe1.png)

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

14. Po zakończeniu wdrażania Uruchom następujące polecenie, aby sprawdzić stan usług przy użyciu Azure Cloud Shell: `kubectl get services` .

## <a name="step-3-provision-front-end-services"></a>Krok 3. Udostępnianie usług frontonu

Administratorzy firmy Contoso muszą wdrożyć infrastrukturę, która będzie używana przez aplikacje frontonu. Tworzą:

- Kontener magazynu obiektów BLOB do przechowywania obrazów PET
- Baza danych Azure Cosmos DB do przechowywania dokumentów zawierających informacje PET
- Interfejs API przetwarzania obrazów witryny sieci Web.

Instrukcje dotyczące tej sekcji korzystają z repozytorium [SmartHotel360-witryna sieci Web](https://github.com/microsoft/smartHotel360-website) .

### <a name="create-blob-storage-containers"></a>Tworzenie kontenerów w usłudze Blob Storage

1. W Azure Portal otwierają utworzone konto magazynu, a następnie wybierają **obiekty blob**.
2. Tworzą one nowy kontener o nazwie **zwierzęta domowe** z poziomem dostępu publicznego ustawionym na kontener. Użytkownicy będą mogli przekazywać zdjęcia swoich zwierząt do tego kontenera.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob1.png)

3. Tworzą drugi nowy kontener o nazwie **settings** (ustawienia). W tym kontenerze zostanie umieszczony plik ze wszystkimi ustawieniami aplikacji frontonu.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob2.png)

4. Zapisują szczegóły dostępu do konta magazynu w pliku tekstowym do użycia w przyszłości.

    ![Magazyn obiektów blob](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-an-azure-cosmos-db-database"></a>Inicjowanie obsługi administracyjnej bazy danych Azure Cosmos DB

Administratorzy firmy Contoso inicjują bazę danych Azure Cosmos DB, która będzie używana na potrzeby informacji dla zwierząt domowych.

1. Tworzą wystąpienie usługi **Azure Cosmos DB** w portalu Azure Marketplace.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. Określają one nazwę (**contososmarthotel**), wybierają interfejs API SQL i umieszcza go w produkcyjnej grupie zasobów **ContosoRG**, w regionie głównej Wschodnie stany USA 2.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. Dodają nową kolekcję do bazy danych z domyślną pojemnością i przepływnością.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. Zapisują informacje dotyczące połączenia z bazą danych do użycia w przyszłości.

    ![Azure Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Aprowizowanie interfejsu API przetwarzania obrazów

Administratorzy firmy Contoso aprowizują interfejs API przetwarzania obrazów. Interfejs API będzie wywoływany przez funkcję w celu oceny zdjęć przekazywanych przez użytkowników.

1. Tworzą wystąpienie interfejsu API **przetwarzania obrazów** w portalu Azure Marketplace.

     ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision1.png)

2. Udostępniają one interfejs API (**smarthotelpets**) w produkcyjnej grupie zasobów **ContosoRG**w regionie Wschodnie stany USA 2.

    ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision2.png)

3. Zapisują parametry połączenia interfejsu API w pliku tekstowym do użycia w przyszłości.

     ![Przetwarzanie obrazów](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Aprowizowanie aplikacji internetowej platformy Azure

Administratorzy firmy Contoso aprowizują aplikację internetową w witrynie Azure Portal.

1. Wybierają pozycję **Aplikacja internetowa** w portalu.

    ![Aplikacja internetowa](./media/contoso-migration-rebuild/web-app1.png)

2. Podają nazwę aplikacji (**smarthotelcontoso**), wybierają system Windows do jej uruchomienia i umieszczają ją w produkcyjnej grupie zasobów **ContosoRG**. Tworzą nowe wystąpienie Application Insights na potrzeby monitorowania aplikacji.

    ![Nazwa aplikacji internetowej](./media/contoso-migration-rebuild/web-app2.png)

3. Po zakończeniu przechodzą do adresu aplikacji, aby sprawdzić, czy została pomyślnie utworzona.

4. Teraz w witrynie Azure Portal tworzą miejsce przejściowe (staging) dla kodu. Potok będzie używał tego miejsca do wdrażania. To gwarantuje, że kod nie zostanie wprowadzony do produkcji, aż administratorzy nie przeprowadzą wydania.

    ![Miejsce przejściowe aplikacji internetowej](./media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Aprowizowanie aplikacji funkcji platformy Azure

W witrynie Azure Portal administratorzy firmy Contoso aprowizują aplikację funkcji.

1. Wybierają pozycję **Aplikacja funkcji**.

    ![Tworzenie aplikacji funkcji](./media/contoso-migration-rebuild/function-app1.png)

2. Podają nazwę aplikacji (**smarthotelpetchecker**). Umieszczają aplikację w produkcyjnej grupie zasobów **ContosoRG**. Ustawili miejsce hostingu na **Plan zużycia**i umieścisz aplikację w regionie Wschodnie stany USA 2. Zostanie utworzone nowe konto magazynu wraz z wystąpieniem usługi Application Insights do monitorowania.

    ![Ustawienia aplikacji funkcji](./media/contoso-migration-rebuild/function-app2.png)

3. Po wdrożeniu aplikacji przechodzą do adresu aplikacji, aby sprawdzić, czy została utworzona pomyślnie.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Krok 4. Konfigurowanie potoku frontonu

Administratorzy firmy Contoso tworzą dwa różne projekty dla witryny frontonu.

1. W usłudze Azure DevOps tworzą projekt **SmartHotelFrontend**.

    ![Projekt frontonu](./media/contoso-migration-rebuild/function-app1.png)

2. Importują repozytorium Git [SmartHotel360 front end](https://github.com/Microsoft/SmartHotel360-Website) do nowego projektu.

3. W przypadku aplikacji funkcji tworzy kolejny projekt platformy Azure DevOps (**SmartHotelPetChecker**) i importuje repozytorium git [PetChecker](https://github.com/sonahander/SmartHotel360-PetCheckerFunction) do tego projektu.

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
    - Edytują **adresy URL** i **pets_config** z wartościami punktów końcowych interfejsu API AKS, kont magazynu i bazy danych Azure Cosmos DB.
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

    ![Ustawienia potoku](./media/contoso-migration-rebuild/vsts-publish-front2.png)

5. W obszarze **Triggers (Wyzwalacze)** włączają ciągłą integrację i dodają gałąź master. Gwarantuje to, że po każdym wprowadzeniu nowego kodu do gałęzi master będzie uruchamiany potok kompilacji.

    ![Ciągła integracja](./media/contoso-migration-rebuild/vsts-publish-front3.png)

6. Wybierają pozycję **Save & Queue** (Zapisz i dodaj do kolejki), aby rozpocząć kompilację.
7. Po zakończeniu kompilacji konfigurują potok wydania, wybierając pozycję **Azure App Service Deployment** (Wdrożenie usługi Azure App Service).
8. Wprowadzają nazwę etapu **Staging** (Przygotowanie).

    ![Nazwa środowiska](./media/contoso-migration-rebuild/vsts-publish-front4.png)

9. Dodają artefakt i wybierają utworzoną przez siebie kompilację.

     ![Dodawanie artefaktu](./media/contoso-migration-rebuild/vsts-publish-front5.png)

10. Wybierają ikonę błyskawicy na artefakcie i włączają ciągłe wdrażanie.

    ![Ciągłe wdrażanie](./media/contoso-migration-rebuild/vsts-publish-front6.png)
11. W obszarze **Environment** (Środowisko) wybierają pozycję **1 job, 1 task** (1 zadanie, 1 podzadanie) w obszarze **Staging**.
12. Po wybraniu nazwy subskrypcji i aplikacji otwierają zadanie **Deploy Azure App Service** (Wdrażanie usługi Azure App Service). Wdrożenie jest skonfigurowane pod kątem korzystania z miejsca wdrożenia **staging**. W ten sposób kod jest automatycznie kompilowany w tym miejscu do przeglądu i zatwierdzenia.

     ![Gniazdo](./media/contoso-migration-rebuild/vsts-publish-front7.png)

13. W obszarze **Pipeline** (Potok) dodają nowy etap.

    ![Nowe środowisko](./media/contoso-migration-rebuild/vsts-publish-front8.png)

14. Wybierają pozycję **Azure App Service deployment with slot** (Wdrożenie usługi Azure App Service z miejscem wdrożenia) i nadają środowisku nazwę **Prod**.
15. Wybierają one **1 zadanie, 2 zadania**, a następnie wybierz subskrypcję, nazwę usługi App Service i miejsce **przejściowe** .

    ![Nazwa środowiska](./media/contoso-migration-rebuild/vsts-publish-front10.png)

16. Usuwają pozycję **Deploy Azure App Service to Slot** (Wdrażanie usługi Azure App Service do miejsca wdrożenia) z potoku. Została tam umieszczona w poprzednich krokach.

    ![Usuwanie z potoku](./media/contoso-migration-rebuild/vsts-publish-front11.png)

17. Zapisują potok. W potoku wybierają pozycję **Post-deployment conditions** (Warunki po wdrożeniu).

    ![Po wdrożeniu](./media/contoso-migration-rebuild/vsts-publish-front12.png)

18. Włączają pozycję **Post-deployment approvals** (Zatwierdzenia po wdrożeniu) i dodają lidera zespołu deweloperskiego jako osobę zatwierdzającą.

    ![Zatwierdzenie po wdrożeniu](./media/contoso-migration-rebuild/vsts-publish-front13.png)

19. W potoku kompilacji ręcznie uruchamiają kompilację. To powoduje wyzwolenie nowego potoku wydania, który wdraża witrynę w przejściowym miejscu wdrożenia (staging). W przypadku firmy Contoso adres URL tego miejsca to `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Po zakończeniu kompilacji i wdrożeniu wydania w miejscu wdrożenia usługa Azure DevOps Services wysyła wiadomość e-mail do lidera zespołu deweloperskiego w celu zatwierdzenia.

21. Lider zespołu deweloperskiego wybiera pozycję **View approval** (Wyświetl zatwierdzenie) i może zatwierdzić lub odrzucić żądanie w portalu usługi Azure DevOps.

    ![Wiadomość e-mail dotycząca zatwierdzenia](./media/contoso-migration-rebuild/vsts-publish-front14.png)

22. Lider wprowadza komentarze i zatwierdza wdrożenie. Spowoduje to rozpoczęcie wymiany miejsc **przejściowych** i **produkcyjnych oraz przeniesienie** kompilacji do środowiska produkcyjnego.

    ![Zatwierdzanie i zamiana](./media/contoso-migration-rebuild/vsts-publish-front15.png)

23. Potok kończy zamianę.

    ![Kończenie zamiany](./media/contoso-migration-rebuild/vsts-publish-front16.png)

24. Zespół sprawdza miejsce **prod**, aby potwierdzić, że aplikacja internetowa jest w środowisku produkcyjnym pod adresem `https://smarthotelcontoso.azurewebsites.net/`.

### <a name="deploy-the-petchecker-function-app"></a>Wdrażanie aplikacji funkcji PetChecker

Administratorzy firmy Contoso wdrażają aplikację w następujący sposób.

1. Klonują repozytorium lokalnie na maszynę deweloperską, nawiązując połączenie z projektem usługi Azure DevOps.
2. W programie Visual Studio otwierają folder, aby wyświetlić wszystkie pliki w repozytorium.
3. Otwierają one plik **src/PetCheckerFunction/Local. Settings. JSON** i dodaje ustawienia aplikacji do magazynu, bazy danych Azure Cosmos DB i interfejs API przetwarzania obrazów.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function5.png)

4. Zatwierdzają kod i synchronizują go z powrotem z usługą Azure DevOps, co powoduje wypchnięcie zmian.
5. Dodajemy nowy potok kompilacji, a następnie wybierz pozycję **Azure DevOps git** dla źródła.
6. Wybierają szablon **ASP.NET Core (.NET Framework)**.
7. Akceptują wartości domyślne w szablonie.
8. W obszarze **wyzwalacze**wybierz pozycję **Włącz integrację ciągłą**, a następnie wybierz pozycję **Zapisz & kolejkę** , aby rozpocząć kompilację.
9. Po zakończeniu kompilacji tworzą potok wydania, dodając pozycję **Azure App Service deployment with slot** (Wdrożenie usługi Azure App Service z miejscem wdrożenia).
10. Nadaj im nazwę **produkcyjny**środowiska, a następnie wybierz subskrypcję. W polu **App type** (Typ aplikacji) ustawiają wartość **Function App** (Aplikacja funkcji) i wprowadzają **smarthotelpetchecker** jako nazwę usługi aplikacji.

    ![Aplikacja funkcji](./media/contoso-migration-rebuild/petchecker2.png)

11. Dodają artefakt **Build** (Kompilacja).

    ![Artefakt](./media/contoso-migration-rebuild/petchecker3.png)

12. Włącza **wyzwalacz ciągłego wdrażania**, a następnie wybierz pozycję **Zapisz**.
13. Wybierają pozycję **Queue new build** (Dodaj nową kompilację do kolejki), aby uruchomić pełny potok ciągłej integracji/ciągłego wdrażania.
14. Wdrożona funkcja pojawi się w witrynie Azure Portal ze stanem **Uruchomiona**.

    ![Wdrażanie funkcji](./media/contoso-migration-rebuild/function6.png)

15. Przechodzą do aplikacji, aby sprawdzić, czy aplikacja Pet Checker działa zgodnie z oczekiwaniami pod adresem `http://smarthotel360public.azurewebsites.net/pets`.

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
- Aby można było używać protokołu SSL z certyfikatami, należy zaktualizować aplikację. Wystąpienie kontenera należy wdrożyć ponownie, aby odpowiadało na porcie 443.
- Firma Contoso powinna rozważyć użycie usługi Key Vault w celu chronienia wpisów tajnych aplikacji usługi Service Fabric. [Dowiedz się więcej](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Kopie zapasowe i odzyskiwanie po awarii

- Firma Contoso musi przejrzeć [wymagania dotyczące kopii zapasowej Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).
- Firma Contoso powinna rozważyć wdrożenie [grup trybu failover SQL, aby zapewnić regionalną pracę w trybie failover dla bazy danych](https://docs.microsoft.com/azure/sql-database/sql-database-auto-failover-group).
- Firma Contoso może używać [replikacji geograficznej dla jednostki SKU Azure Container Registry Premium](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).
- Kopia zapasowa Azure Cosmos DB została utworzona automatycznie. Firma Contoso może [dowiedzieć się więcej](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) na temat tego procesu.

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu wszystkich zasobów firma Contoso powinna przypisać tagi platformy Azure zgodnie z [planem infrastruktury](./contoso-migration-infrastructure.md#set-up-tagging).
- Wszystkie koszty licencjonowania są wliczone w koszt usług PaaS używanych przez firmę Contoso. Ten koszt zostanie odjęty od umowy EA.
- Firma Contoso umożliwi [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview) monitorowania zasobów platformy Azure i zarządzania nimi.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso ponownie skompilowała aplikację SmartHotel360 na platformie Azure. Lokalna maszyna wirtualna frontonu aplikacji została ponownie skompilowana w aplikacjach internetowych usługi Azure App Service. Zaplecze aplikacji zostało skompilowane przy użyciu mikrousług wdrożonych w kontenerach zarządzanych przez usługę Azure Kubernetes Service (AKS). Firma Contoso rozszerzyła funkcjonalność aplikacji o aplikację do obsługi zdjęć zwierząt.

## <a name="suggested-skills"></a>Sugerowane umiejętności

Microsoft Learn to nowe podejście do uczenia się. Gotowość do nowych umiejętności i obowiązków, które są związane z wdrażaniem chmury, nie przychodzi łatwo. Microsoft Learn oferuje bardziej satysfakcjonującą metodę praktycznego uczenia się, która ułatwia szybsze osiąganie celów. Zdobywaj punkty i poziomy i osiągaj więcej.

Poniżej przedstawiono kilka przykładów dostosowanych ścieżek szkoleniowych na Microsoft Learn, które są wyrównane do aplikacji Contoso SmartHotel360 na platformie Azure.

- ** [Wdróż witrynę sieci Web na platformie Azure za pomocą Azure App Service](https://docs.microsoft.com/learn/paths/deploy-a-website-with-azure-app-service):** Aplikacje sieci Web na platformie Azure umożliwiają łatwe publikowanie witryny sieci Web i zarządzanie nią bez konieczności pracy z podstawowymi serwerami, magazynem lub zasobami sieciowymi. Zamiast tego możesz skupić się na funkcjach witryny, polegając na niezawodnej platformie Azure, która zapewnia bezpieczny dostęp do witryny.

- ** [Przetwarzaj i Klasyfikuj obrazy za pomocą usług Azure poznawczej](https://docs.microsoft.com/learn/paths/classify-images-with-vision-services):** Usługa Azure Cognitive Services oferuje wbudowaną funkcję do włączania funkcji przetwarzania obrazów w aplikacjach. Dowiedz się, jak usługa Cognitive Vision Services pozwala wykrywać twarze, tagować i klasyfikować obrazy oraz identyfikować obiekty.
