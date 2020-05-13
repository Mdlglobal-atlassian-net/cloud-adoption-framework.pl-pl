---
title: 'Innowacje na platformie Azure: Przewidywanie i wpływ'
description: Dowiedz się więcej o rozwiązaniach platformy Azure do przewidywania potrzeb klientów i ponownego integrowania prognoz z rozwiązaniem w celu wpływania na zachowanie klientów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 97008960de4eecb7ff0dc4f756ad4ca11865c634
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83224055"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Przewodnik po innowacjach na platformie Azure: Przewidywanie i wpływ

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Przewidywanie i wpływ

::: zone-end

Twoja innowacyjna firma ma wgląd w dane, zachowania i potrzeby klientów. Analiza tych szczegółowych informacji może pomóc we wcześniejszym przewidywaniu potrzeb klientów — nawet zanim klienci zdadzą sobie sprawę z tych potrzeb. W tym artykule przedstawiono kilka metod dostarczania rozwiązań predykcyjnych. W końcowej części artykułu przedstawiono metody integrowania tych prognoz z rozwiązaniem w celu kształtowania zachowań klientów.

Poniższa tabela ułatwia znalezienie najlepszego rozwiązania w zależności od wymagań implementacji.

| Usługa | Wstępnie utworzone modele | Tworzenie i eksperymentowanie | Trenowanie i tworzenie przy użyciu języka Python | Wymagane umiejętności |
|---|---|---|---|---|
| Azure Cognitive Services | Yes | Nie | Nie | Umiejętności deweloperskie i znajomość interfejsu API |
| Azure Machine Learning Studio | Yes | Yes | Nie | Ogólna znajomość algorytmów predykcyjnych |
| Usługa Azure Machine Learning | Yes | Yes | Yes | Analityk danych |

## <a name="azure-cognitive-services"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Najszybszą i najłatwiejszą metodą przewidywania potrzeb klientów jest użycie usług Azure Cognitive Services. Usługi Cognitive Services umożliwiają prognozowanie na podstawie istniejących modeli, bez dodatkowego trenowania. Użycie tych usług jest optymalnym rozwiązaniem sprawdzającym się nawet wtedy, gdy wśród personelu nie masz analityka danych, który może wytrenować model predykcyjny. W przypadku niektórych usług trenowanie nie jest wymagane. Inne usługi wymagają tylko minimalnego trenowania.

Listę dostępnych usług oraz informacje o wymaganym trenowaniu można znaleźć w temacie [Usługi Cognitive Services i uczenie maszynowe](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Akcja

Aby użyć interfejsu API usługi Cognitive Service:

1. W witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.CognitiveServices%2FAccounts) przejdź do usług **Cognitive Services**.
2. Wybierz pozycję **Dodaj**, aby znaleźć interfejs API usług Cognitive Services w portalu Azure Marketplace.
3. Wykonaj jedną z następujących czynności:
   - Jeśli znasz nazwę usługi, której chcesz użyć, wpisz ją w polu **Wyszukaj w witrynie Marketplace**.
   - Aby wyświetlić listę interfejsów API usług Cognitive Services, wybierz link **Zobacz więcej** obok nagłówka usług Cognitive Services.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts]" submitText="Go to Cognitive Services" :::

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usług Cognitive Services w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2FAccounts).

::: zone-end

## <a name="azure-machine-learning-studio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Jeśli istniejące modele w usługach Cognitive Services nie umożliwiają uzyskania odpowiedniej prognozy, z pomocą przychodzi usługa Azure Machine Learning Studio. Pozwala ona utworzyć wymagane prognozy, a przy tym nie wymaga zaawansowanych umiejętności analityka danych.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Za pomocą usługi Azure Machine Learning Studio można utworzyć model i eksperymentować z nim w następujący sposób:

1. W witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces) przejdź do usługi **Azure Machine Learning Studio**.
2. Wybierz pozycję **Utwórz obszar roboczy Machine Learning Studio** i postępuj zgodnie z instrukcjami, aby utworzyć obszar roboczy.

   Nowy obszar roboczy zawiera interfejs typu „przeciągnij i upuść”, który pozwala utworzyć model i eksperymentować z nim (jest to alternatywa dla trenowania głębokiego).

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usługi Azure Machine Learning Studio w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2FWorkspaces).

::: zone-end

## <a name="azure-machine-learning-service"></a>[Usługa Azure Machine Learning](#tab/MachineLearningService)

Usługa Azure Machine Learning umożliwia korzystanie z bardziej zaawansowanych, opartych na kodzie metod, które są wymagane do trenowania głębokiego z użyciem zestawów danych klientów. Przy użyciu języków takich jak Python analitycy danych mogą trenować, a następnie tworzyć algorytmy umożliwiające przewidywanie potrzeb klientów.

### <a name="action"></a>Akcja

Przy użyciu usługi Azure Machine Learning analityk danych może wytrenować i utworzyć model, korzystając z zaawansowanych języków, takich jak Python:

1. Wybierz pozycję **Azure Machine Learning Service**.
2. Wybierz pozycję **Utwórz obszary robocze usługi Machine Learning Service** i postępuj zgodnie z instrukcjami, aby utworzyć obszar roboczy.
3. Nowy obszar roboczy pozwala korzystać z metod opartych na kodzie, które umożliwiają analitykom danych trenowanie i tworzenie modeli wymagających bardziej zaawansowanej analizy do dokładnego przewidywania potrzeb klientów.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces]" submitText="Go to Azure Machine Learning service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usługi Azure Machine Learning Studio w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2FWorkspaces).

::: zone-end

## <a name="influence"></a>Wywieranie wpływu

Produktem końcowym wszystkich wcześniej omówionych metod jest interfejs API, który udostępnia model predykcyjny aplikacjom. W swoim rozwiązaniu użyj dowolnej z tych metod, aby przekazać dane zebrane od klienta do predykcyjnego interfejsu API. Możesz następnie zintegrować wyniki ze środowiskiem klienta jako sugerowany krok do wykonania.

Te sugerowane kroki do wykonania mogą pomóc w ukształtowaniu wzorców zachowań klienta i wpłynąć na sposób reakcji klientów. Ponieważ sugerowane kroki do wykonania są oparte na algorytmach predykcyjnych, korzystają z wcześniejszych potrzeb klientów i dostępnych danych, umożliwiając przewidywanie i spełnianie przyszłych potrzeb klientów. Często ma to miejsce, zanim klient zorientuje się, że taka potrzeba zaistniała.
