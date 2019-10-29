---
title: 'Przewodnik po innowacjach na platformie Azure: Przygotowanie do zbierania opinii klientów'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przygotowanie do zbierania opinii klientów
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: ec17c66fa92abc292a19a8e74c215111d8638a05
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769366"
---
::: zone target="docs"

# <a name="azure-innovation-guide-prepare-for-customer-feedback"></a>Przewodnik po innowacjach na platformie Azure: Przygotowanie do zbierania opinii klientów

::: zone-end

::: zone target="chromeless"

# <a name="prepare-for-customer-feedback"></a>Przygotowanie do zbierania opinii klientów

::: zone-end

Wdrażanie i utrzymywanie zaangażowanych użytkowników jest kluczem do powodzenia innowacji. Dlaczego?

Tworzenie nowego, innowacyjnego rozwiązania nie polega na spełnianiu zachcianek użytkowników. Chodzi o sformułowanie hipotezy, którą można przetestować i ulepszyć. Wyróżniamy dwa typy takich testów: Ilościowe (informacje zwrotne z testów), odpowiadające oczekiwanym akcjom. Jakościowe (opinie klientów), informujące o tym, co oznaczają te metryki dla klientów. Połączenie tych testów pozwala sformułować następną hipotezę i określić kolejne usprawnienie rozwiązania. Te informacje zwrotne są podstawą [procesu tworzenie-pomiar-nauka](../considerations/adoption.md), który stanowi rdzeń tej metodologii.

Przed zintegrowaniem pętli informacji zwrotnych należy mieć udostępnione repozytorium rozwiązania. Scentralizowane repozytorium umożliwia rejestrowanie wszystkich informacji zwrotnych dotyczących projektu i reagowanie na nie.  Serwis [GitHub](https://github.com/) to podstawowe miejsce przechowywania oprogramowania typu open source. Jest to również jedna z najczęściej używanych platform do hostowania repozytoriów kodu źródłowego aplikacji komercyjnych. Artykuł dotyczący [tworzenia repozytoriów GitHub](https://docs.microsoft.com/azure/devops/pipelines/repos/github?view=azure-devops&tabs=yaml) ułatwi Ci rozpoczęcie korzystania z repozytorium.

Każde z poniższych narzędzi platformy Azure umożliwia integrację z projektami hostowanymi w witrynie GitHub (lub jest z nimi zgodne):

## <a name="quantitative-feedback-for-web-appstabquantitative-apps"></a>[Ilościowe informacje zwrotne dotyczące aplikacji internetowych](#tab/Quantitative-Apps)

Application Insights to narzędzie monitorujące, które pozwala korzystać — niemal w czasie rzeczywistym — z ilościowych informacji zwrotnych na temat użycia aplikacji. Informacje te pomagają przetestować i zweryfikować bieżącą hipotezę, co ułatwia kształtowanie następnej funkcji lub scenariusza użytkownika na liście prac.

### <a name="action"></a>Akcja

Aby wyświetlić dane ilościowe z aplikacji:

1. Wybierz pozycję **App Insights**.
2. Jeśli aplikacji nie ma na liście, kliknij link **Dodaj +** i postępuj zgodnie z instrukcjami umożliwiającymi skonfigurowanie usługi App Insights.
3. Jeśli aplikacja znajduje się na liście, wybierz tę aplikację.
4. Okienko **Przegląd** zawiera statystyki dotyczące aplikacji. Link **Pulpit nawigacyjny aplikacji** umożliwia utworzenie niestandardowego pulpitu nawigacyjnego w celu wyświetlenia danych, które są bardziej istotne dla hipotezy.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Go to App Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Aby wyświetlić dane dotyczące aplikacji, przejdź do witryny [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents).

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

- [Konfigurowanie usługi Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/learn/quick-monitor-portal)
- [Wprowadzenie do usługi Azure Monitor App Insights](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-users)
- [Tworzenie pulpitu nawigacyjnego danych telemetrycznych](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-app-dashboards)

## <a name="quantitative-feedback-for-apistabquantitative-apis"></a>[Ilościowe informacje zwrotne dotyczące interfejsów API](#tab/Quantitative-APIs)

Połączona gospodarka zmienia sposób wprowadzania innowacji w firmach.  Rośnie dynamika zakłóceń działalności w poszczególnych rynkach i sektorach. Zakłócenia te mają różną postać, a firmy muszą zmagać się z **„dylematem innowatora”** : jak skoordynować tempo zmian bez kolidowania z bieżącą działalnością biznesową.

Zewnętrzne użycie interfejsów API w przedsiębiorstwach dotyczy zmiany sposobu współpracy z klientami i partnerami. Z kolei wewnętrzne użycie interfejsów API jest związane z płynnym łączeniem odrębnych części firmy. Gospodarka oparta na interfejsach API wykorzystuje cztery bloki konstrukcyjne: sieci społecznościowe, urządzenia mobilne, analitykę i chmurę. Aplikacje i usługi można łączyć szybko i ekonomicznie, tworząc ofertę o zwiększonej wartości.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby rejestrować dane ilościowe z interfejsów API:

1. Wybierz usługę **API Management**.
2. Wybierz z listy odpowiedni interfejs API.
3. Wybierz pozycję **Ustawienia diagnostyczne** w sekcji **Monitorowanie**.

Aby wyświetlić dane ilościowe z interfejsów API:

1. Wybierz usługę **API Management**.
2. Wybierz z listy odpowiedni interfejs API.
3. Wybierz pozycję **Aplikacja** w sekcji **Monitorowanie**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice]" submitText="Go to API Management Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Aby otworzyć usługę API Management, przejdź do witryny [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.ApiManagement%2Fservice).

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

Ten artykuł ułatwi Ci użycie [usługi Azure Monitor w celu uzyskania informacji zwrotnych z interfejsów API](https://docs.microsoft.com/azure/api-management/api-management-howto-use-azure-monitor)

## <a name="qualitative-feedbacktabqualitative"></a>[Jakościowe informacje zwrotne](#tab/Qualitative)

Lista prac (tablica) umożliwia rejestrowanie informacji zwrotnych jako scenariuszy użytkownika. Pozwala ona również śledzić powiązaną pracę jako zadania umożliwiające podejmowanie odpowiednich działań. Usługę Azure Boards można zintegrować bezpośrednio z witryną GitHub, co pozwala bezproblemowo zarządzać zadaniami dotyczącymi informacji zwrotnych oraz kodem źródłowym.

::: zone target="docs"

### <a name="action"></a>Akcja

Usługi Azure Boards i Azure Pipelines wymagają oddzielnego portalu w witrynie GitHub i na platformie Azure.
Aby rozpocząć pracę z tymi narzędziami, wybierz usługę [Azure DevOps](https://dev.azure.com/)

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akcja

Aby utworzyć projekt DevOps:

1. Wybierz pozycję **Projekt usługi Azure DevOps**.
2. Kliknij pozycję **Utwórz projekt DevOps**.
3. Wybierz pozycję **Środowisko wykonawcze, struktura i usługa**.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/microsoft.visualstudio%2Faccount%2Fproject]" submitText="Go to Azure DevOps Project" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

Poniższe linki ułatwią scentralizowane zarządzanie informacjami zwrotnymi przy użyciu usługi Azure Boards i witryny GitHub:

- [Wprowadzenie do usługi Azure Boards](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)
- [Usługa Azure Boards i witryna GitHub](https://docs.microsoft.com/azure/devops/boards/boards/kanban-quickstart?view=azure-devops)

## <a name="close-the-loop-with-pipelinestabpipelines"></a>[Zamykanie pętli z potokami](#tab/pipelines)

Reagowanie na informacje zwrotne nie zawsze skutkuje wprowadzeniem funkcji, o którą prosi klient. Jednak każdy punkt danych powinien powodować jakąś zmianę. Zmiana ta może dotyczyć sposobu myślenia. Może to być również zmiana techniczna, zupełnie inna niż oczekiwana przez klienta. Potoki wdrażania i narzędzia, np. usługa Azure Pipelines, umożliwiają szybkie publikowanie takich zmian, co pozwala często je udostępniać klientom.

Aby wyświetlić aktywne wdrożenia powiązane z aplikacjami hostowanymi na platformie Azure:

### <a name="action"></a>Akcja

Aby wyświetlić bieżące wdrożenia w potoku:

1. Wybierz usługę **App Service**.
2. Wybierz z listy odpowiednią aplikację.
3. Wybierz pozycję **Centrum wdrażania** w sekcji **Wdrożenie** w okienku usług aplikacji.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites]" submitText="Go to App Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Aby wyświetlić aplikacje w usłudze App Service, przejdź do witryny [Azure Portal](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2Fsites).

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

Poniższe linki umożliwiają rozpoczęcie tworzenia potoków wdrożenia:

- [Tworzenie pierwszego potoku](https://docs.microsoft.com/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2)
- [Zwalnianie zadań w witrynie GitHub](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/github-release?view=azure-devops)
