---
title: 'Innowacje na platformie Azure: Angażowanie przez aplikacje'
description: Dowiedz się więcej o usługach platformy Azure, które ułatwiają modernizację istniejących aplikacji internetowych i interfejsów API oraz tworzenie aplikacji natywnych dla chmury.
author: billyclaymyersmsft
ms.author: wimyers
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 53bf6e8a6c3e01255e57613b3b1a3cd2fa9cdc07
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222253"
---
<!-- cSpell:ignore billyclaymyersmsft wimyers functionapp -->

::: zone target="docs"

# <a name="azure-innovation-guide-engage-customers-through-apps"></a>Przewodnik po innowacjach na platformie Azure: Budowa relacji z klientami przy użyciu aplikacji

::: zone-end

::: zone target="chromeless"

# <a name="engage-customers-through-apps"></a>Budowa relacji z klientami przy użyciu aplikacji

::: zone-end

Innowacje dotyczące aplikacji obejmują zarówno modernizowanie istniejących aplikacji hostowanych lokalnie, jak i tworzenie aplikacji natywnych dla chmury przy użyciu kontenerów lub technologii bezserwerowych. Platforma Azure udostępnia usługi PaaS, takie jak Azure App Service, umożliwiające łatwe modernizowanie istniejących aplikacji internetowych oraz aplikacji interfejsu API opracowanych w środowisku .NET, .NET Core, Java, Node.js, Ruby, Python lub PHP i przeznaczonych do wdrożenia na platformie Azure.

Model kontenerów o otwartym standardzie umożliwia łatwe tworzenie mikrousług lub konteneryzowanie istniejących aplikacji i wdrażanie ich na platformie Azure za pomocą usług zarządzanych, takich jak Azure Kubernetes Service, Azure Container Instances i Web App for Containers. Technologie bezserwerowe, takie jak Azure Functions i Azure Logic Apps, korzystają z modelu użycia (opartego na płatności za zużyte zasoby), a nie na wdrażaniu infrastruktury i zarządzaniu nią, dzięki czemu ułatwiają skoncentrowanie się na tworzeniu aplikacji.

<!-- markdownlint-disable MD025 -->

# <a name="deliver-value-faster"></a>[Szybsze dostarczanie wartości](#tab/DeliverValueFaster)

Jedną z zalet rozwiązań opartych na chmurze jest możliwość szybszego zbierania opinii i dostarczania wartości użytkownikom. Szybsze uzyskiwanie opinii na temat aplikacji — zarówno od klientów zewnętrznych, jak i użytkowników w firmie — jest korzystne.

## <a name="azure-app-service"></a>Azure App Service

Usługa Azure App Service zapewnia środowisko hostingu dla aplikacji, które eliminuje niedogodności związane z zarządzaniem infrastrukturą i stosowaniem poprawek systemu operacyjnego. Usługa ta pozwala spełnić potrzeby użytkowników dzięki automatyzacji skalowania przy zachowaniu zdefiniowanych limitów, umożliwiających kontrolę nad kosztami.

Usługa App Service zapewnia najwyższej jakości obsługę języków ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP i Python. Jeśli musisz hostować inny stos środowiska uruchomieniowego, możesz skorzystać z funkcji Web App for Containers, która umożliwia szybkie i łatwe rozpoczęcie hostowania kontenera Docker w usłudze App Service. Pozwala to hostować niestandardowy stos kodu w środowisku, w którym nie są używane serwery.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować wdrożenia usługi Azure App Service:

1. Wybierz pozycję **App Services**.
2. Konfigurowanie nowej usługi: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami: wybierz odpowiednią aplikację z listy hostowanych aplikacji.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2FSites]" submitText="Go to App Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Usługi Azure Cognitive Services umożliwiają dodanie zaawansowanej analizy bezpośrednio do aplikacji za pomocą zestawu interfejsów API, które pozwalają korzystać z obsługiwanych przez firmę Microsoft algorytmów sztucznej inteligencji i uczenia maszynowego.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować wdrożenia usług Azure Cognitive Services:

1. Wybierz pozycję **Cognitive Services**.
2. Konfigurowanie nowej usługi: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami: wybierz odpowiednią usługę z listy hostowanych usług.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-bot-service"></a>Usługa Azure Bot

Usługi Azure Bot Services umożliwiają rozbudowanie standardowej aplikacji o interfejs naturalnego bota, który pozwala tworzyć nowe możliwości interakcji z użyciem sztucznej inteligencji i uczenia maszynowego.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować wdrożenia usług Azure Bot Services:

1. Wybierz pozycję **Usługi botów**.
2. Konfigurowanie nowej usługi: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami: wybierz odpowiedniego bota z listy hostowanych usług.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.BotService%2FBotServices]" submitText="Go to Bot Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-devops"></a>Azure DevOps

W świecie innowacji na pewno napotkasz metodykę DevOps. Przez długi czas firma Microsoft sprzedawała produkt lokalny o nazwie Team Foundation Server (TFS). W ramach tworzenia innowacyjnych produktów firma Microsoft opracowała opartą na chmurze usługę Azure DevOps, która udostępnia narzędzia do kompilowania i wydawania obsługujące wiele języków i miejsc docelowych wydań. Aby uzyskać więcej informacji, zobacz [usługę Azure DevOps](https://docs.microsoft.com/azure/devops).

## <a name="visual-studio-app-center"></a>Visual Studio App Center

Wraz ze wzrostem popularności aplikacji mobilnych rośnie zapotrzebowanie na platformę, która umożliwia automatyczne testowanie różnych konfiguracji na rzeczywistych urządzeniach. Rozwiązanie Visual Studio App Center nie jest tylko miejscem, w którym można testować aplikacje w systemach iOS, Android, Windows i macOS. Jest to również platforma monitorowania, która może wykorzystywać usługę Azure Application Insights do szybkiego i prostego analizowania danych telemetrycznych. Aby uzyskać więcej informacji, zobacz [Omówienie rozwiązania Visual Studio App Center](https://docs.microsoft.com/appcenter).

Rozwiązanie Visual Studio App Center udostępnia również usługę, która pozwala wysyłać powiadomienia do aplikacji na różnych platformach za pomocą pojedynczego wywołania bez konieczności komunikowania się z każdą usługą powiadomień. Aby uzyskać więcej informacji, zobacz [Usługa Visual Studio App Center Push (ACP)](https://docs.microsoft.com/appcenter/push).

### <a name="learn-more"></a>Dowiedz się więcej

- [Omówienie usługi App Service](https://docs.microsoft.com/azure/app-service/overview)
- [Web App for Containers: uruchamianie niestandardowego kontenera](https://docs.microsoft.com/azure/app-service/containers/quickstart-docker)
- [Wprowadzenie do usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)
- [Platforma Azure dla deweloperów .NET i .NET Core](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet)
- [Dokumentacja zestawu Azure SDK dla języka Python](https://docs.microsoft.com/azure/python)
- [Platforma Azure dla deweloperów języka Java w chmurze](https://docs.microsoft.com/azure/java/?view=azure-java-stable)
- [Tworzenie aplikacji internetowej w języku PHP na platformie Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-php)
- [Dokumentacja zestawu Azure SDK dla języka JavaScript](https://docs.microsoft.com/azure/javascript)
- [Dokumentacja zestawu Azure SDK dla języka Go](https://docs.microsoft.com/azure/go)
- [Rozwiązania DevOps](https://azure.microsoft.com/solutions/devops)

# <a name="create-cloud-native-apps"></a>[Tworzenie aplikacji natywnych dla chmury](#tab/CloudNative)

<!-- markdownlint-disable MD026 -->

## <a name="what-are-cloud-native-applications"></a>Co to są aplikacje natywne dla chmury?

Aplikacje natywne dla chmury są tworzone od podstaw z myślą o optymalizacji pod kątem skali i wydajności chmury. Są one luźno powiązane, obserwowalne i oparte na architekturze mikrousług, używają usług zarządzanych i korzystają z ciągłego dostarczania w celu zapewnienia niezawodności i krótszego czasu wprowadzenia na rynek. Zwykle są przenośne i mogą działać w środowiskach dynamicznych, takich jak chmury publiczne, prywatne i hybrydowe. Aplikacje natywne dla chmury zwykle tworzy się przy użyciu następujących metod:

- Mikrousługi
- Praca bezserwerowa
- Containers

## <a name="microservices"></a>Mikrousługi

Mikrousługi to styl architektury oprogramowania, w którym aplikacje składają się z niewielkich, niezależnych modułów komunikujących się ze sobą przy użyciu odpowiednio zdefiniowanych kontraktów interfejsów API. Te moduły usług to odłączone bloki konstrukcyjne, które są na tyle małe, że mogą implementować jedną funkcję. Oto zalety mikrousług:

- Niezależne tworzenie usług.
- Autonomiczne skalowanie usług.
- Stosowanie odpowiednich metod wdrażania i języków programowania.
- Izolacja punktów awarii.
- Szybsze dostarczanie wartości.

### <a name="azure-kubernetes-service-aks"></a>Azure Kubernetes Service (AKS)

Korzystaj z w pełni zarządzanej usługi Kubernetes do obsługi aprowizowania, uaktualniania i skalowania zasobów klastrów na żądanie. Usługa AKS ułatwia wdrażanie aplikacji konteneryzowanych i zarządzanie nimi. Oferuje ona bezserwerową platformę Kubernetes, zintegrowane środowisko ciągłej integracji i ciągłego dostarczania oraz zabezpieczenia i nadzór klasy korporacyjnej. Połącz zespoły deweloperskie i operacyjne na jednej platformie, aby szybko i pewnie tworzyły, dostarczały i skalowały aplikacje.

#### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować usługę AKS:

1. Przejdź do obszaru **Azure Kubernetes Services**.
2. Konfigurowanie nowej usługi: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami: Wybierz z listy odpowiednią usługę Kubernetes.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FManagedClusters]" submitText="Go to Azure Kubernetes Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="event-based-solutions"></a>Rozwiązania oparte na zdarzeniach

### <a name="azure-functions"></a>Azure Functions

Usługa Azure Functions udostępnia platformę do uruchamiania małych fragmentów kodu lub funkcji w chmurze. Funkcje pozwalają rozpocząć refaktoryzację kodu na architekturę mikrousług.

Środowisko uruchomieniowe Azure Functions obsługuje wiele języków, np. C#, Java, JavaScript i Python. Aby zapoznać się z pełną listą, zobacz [Obsługiwane języki w usłudze Azure Functions](https://docs.microsoft.com/azure/azure-functions/supported-languages).

Kolejną zaletą funkcji jest możliwość ich wyzwalania przez różne akcje i zdarzenia, np. elementy HTTPTrigger, TimerTrigger oraz wyzwalacze z innych usług platformy Azure, takich jak Blob Storage, Event Grid i Service Bus. Aby uzyskać więcej informacji na temat wyzwalaczy i powiązań, zobacz [Pojęcia dotyczące powiązań i wyzwalaczy usługi Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings).

#### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować wdrożenia usługi Azure Functions:

1. Wybierz pozycję **Aplikacja funkcji**.
2. Konfigurowanie nowej aplikacji: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi aplikacjami: Wybierz odpowiednią aplikację z listy aplikacji funkcji.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2FSites/kind/functionapp]" submitText="Go to Azure Functions" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="serverless-solutions"></a>Rozwiązania bezserwerowe

Twórz aplikacje natywne dla chmury bez aprowizowania infrastruktury i zarządzania nią, przy użyciu w pełni zarządzanej platformy, która automatycznie zajmuje się skalowaniem oraz zapewnianiem dostępności i wydajności. Oto zalety rozwiązań bezserwerowych platformy Azure:

- Skrócenie czasu tworzenia oprogramowania.
- Zwiększenie wydajności zespołu.
- Zwiększenie korzyści dla organizacji.

### <a name="azure-logic-apps"></a>Azure Logic Apps

Zintegruj dane i aplikacje zamiast pisać złożony kod umożliwiający współdziałanie odrębnych systemów. Wizualnie twórz bezserwerowe przepływy pracy dzięki usłudze Azure Logic Apps i korzystaj z własnych interfejsów API, funkcji bezserwerowych lub gotowych łączników w modelu SaaS („oprogramowanie jako usługa”), takich jak Salesforce, Microsoft Office 365 i Dropbox.

#### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować aplikacje logiki na platformie Azure:

1. Wybierz pozycję **Aplikacje logiki**.
2. Konfigurowanie nowej aplikacji: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi aplikacjami: Wybierz z listy odpowiednią aplikację logiki.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Logic%2FWorkflows]" submitText="Go to Azure Logic Apps" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="serverless-api-management"></a>Zarządzanie bezserwerowymi interfejsami API

Publikuj, zabezpieczaj, przekształcaj, obsługuj i monitoruj interfejsy API za pomocą Azure API Management — w pełni zarządzanej usługi oferującej model użycia zaprojektowany i wdrożony pod kątem pełnego dopasowania do aplikacji bezserwerowych.

#### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować usługi API Management:

1. Wybierz pozycję **Usługi API Management**.
2. Konfigurowanie nowej usługi: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami: Wybierz z listy odpowiednią usługę.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2FService]" submitText="Go to API Management services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="containers"></a>Containers

Modernizując portfolio aplikacji, można skorzystać z różnych usług kontenerów platformy Azure, które pozwalają migrować istniejące aplikacje do kontenerów oraz tworzyć natywne dla chmury aplikacje mikrousług, umożliwiające szybsze dostarczanie wartości użytkownikom. Opracowuj i aktualizuj swoje aplikacje konteneryzowane oraz zarządzaj nimi dzięki kompleksowym narzędziom dla deweloperów i narzędziom do ciągłej integracji/ciągłego wdrażania. Zarządzaj kontenerami w dużej skali za pomocą w pełni zarządzanej usługi organizowania kontenerów Kubernetes, którą można zintegrować z usługą Azure Active Directory. Na każdym etapie modernizacji możesz przyspieszyć opracowywanie aplikacji konteneryzowanych, jednocześnie spełniając wymagania dotyczące zabezpieczeń.

### <a name="azure-container-instances"></a>Azure Container Instances

Uruchamiaj kontenery platformy Docker na żądanie w zarządzanym, bezserwerowym środowisku platformy Azure. Azure Container Instances to rozwiązanie uniwersalne, które może działać w odizolowanych kontenerach bez orkiestracji. Uruchamiając swoje obciążenia w ramach usługi Container Instances, możesz skoncentrować się na projektowaniu i tworzeniu aplikacji, zamiast zarządzać infrastrukturą, w ramach której one działają.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować usługę Container Instances:

1. Wybierz pozycję **Container Instances**.
2. Konfiguracja nowego wystąpienia kontenera: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi wystąpieniami kontenerów: wybierz z listy odpowiednie wystąpienie kontenera.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ContainerInstance%2FContainerGroups]" submitText="Go to Container instances" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="azure-red-hat-openshift"></a>Azure Red Hat OpenShift

Platforma Azure Red Hat OpenShift umożliwia elastyczne, samoobsługowe wdrażanie w pełni zarządzanych klastrów OpenShift. Zapewnij zgodność z przepisami i skoncentruj się na opracowywaniu aplikacji, pozwalając, aby firmy Microsoft i Red Hat zajęły się aktualizowaniem i monitorowaniem węzła głównego, infrastruktury i aplikacji oraz stosowaniem do nich poprawek. Wybierz własne rozwiązania rejestru, sieci, magazynu lub ciągłej integracji/ciągłego wdrażania. Możesz też szybko rozpocząć pracę dzięki wbudowanym rozwiązaniom umożliwiającym zautomatyzowane zarządzanie kodem źródłowym, kompilowanie kontenerów i aplikacji, wdrażanie, skalowanie, zarządzanie kondycją i nie tylko.

**Zobacz [Azure Red Hat OpenShift](https://docs.microsoft.com/azure/openshift/intro-openshift)**

# <a name="isolate-points-of-failure"></a>[Izolacja punktów awarii](#tab/IsolatePointsOfFailure)

Pod koniec etapu wstępnego testowania należy ocenić sposoby izolowania i usuwania punktów awarii. Dzięki rozproszeniu chmury platformy Azure można zaprojektować aplikację pod kątem minimalizacji awarii i zwiększenia wydajności.

## <a name="azure-front-door-service"></a>Azure Front Door Service

Usługa Azure Front Door Service udostępnia skalowalny, bezpieczny punkt wejścia, którego można użyć do dostarczania aplikacji globalnych. Usługa ta umożliwia optymalizację ruchu w celu uzyskania najlepszej wydajności i zapewnia natychmiastowe przechodzenie do trybu failover w skali globalnej. Jeśli chcesz zakończyć korzystanie z protokołu zabezpieczeń TLS (odciążanie protokołu SSL) lub przetwarzanie poszczególnych żądań HTTP/HTTPS na poziomie warstwy aplikacji, usługa Azure Front Door Service jest lepszym wyborem niż usługa Azure Traffic Manager.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować usługi Front Door:

1. Wybierz pozycję **Usługi Front Door**.
2. Konfiguracja nowej usługi Front Door: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi usługami Front Door: Wybierz z listy odpowiednią usługę Front Door.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FFrontDoors]" submitText="Go to Front Doors" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="traffic-manager"></a>Traffic Manager

Usługa Traffic Manager umożliwia oparte na systemie DNS równoważenie obciążenia, którym można kierować na podstawie różnych reguł. Pomaga to zapewnić odporność w razie awarii wdrożonych usług. Usługę Traffic Manager można również umieścić na stosie, aby korzystać zarówno z routingu opartego na awariach, jak i routingu opartego na wydajności, co pozwala zapewnić najlepszą jakość usług w różnych obszarach geograficznych.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować profile usługi Traffic Manager:

1. Wybierz pozycję **Profile usługi Traffic Manager**.
2. Konfiguracja nowego profilu: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi profilami: wybierz z listy odpowiedni profil.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FTrafficManagerProfiles]" submitText="Go to Traffic Manager profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-content-delivery-network"></a>Azure Content Delivery Network

Platforma Azure udostępnia rozproszoną usługę Content Delivery Network (CDN), która umożliwia dostarczanie zasobów w odpowiednim czasie dzięki ich buforowaniu w lokalizacji znajdującej się blisko użytkowników. Buforowanie pomaga w zwiększeniu komfortu pracy klientów. Ponadto podczas pobierania zawartości zapobiega problemom powodowanym przez usterki sieciowe występujące pomiędzy punktem końcowym usługi CDN i centrum danych, które hostuje aplikację. Z usługi Content Delivery Network mogą również korzystać aplikacje, które nie są hostowane na platformie Azure.

### <a name="action"></a>Akcja

Aby skonfigurować lub monitorować profile usługi Content Delivery Network:

1. Wybierz pozycję **Profile CDN**.
2. Konfiguracja nowego profilu: Wybierz pozycję **Dodaj** i postępuj zgodnie z instrukcjami.
3. Zarządzanie istniejącymi profilami: wybierz z listy odpowiedni profil.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Cdn%2FProfiles]" submitText="Go to CDN profiles" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
- [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager)
- [Content Delivery Network](https://docs.microsoft.com/azure/cdn)
