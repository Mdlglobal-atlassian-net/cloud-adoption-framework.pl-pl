---
title: 'Przewodnik po innowacjach na platformie Azure: Przewidywanie i wpływ'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Naucz się przewidywać i wywierać wpływ przy użyciu platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b2ed1b072d5226649e5248e350edfa3578978c4c
ms.sourcegitcommit: 910efd3e686bd6b9bf93951d84253b43d4cc82b5
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72769259"
---
::: zone target="docs"

# <a name="azure-innovation-guide-predict-and-influence"></a>Przewodnik po innowacjach na platformie Azure: Przewidywanie i wpływ

::: zone-end

::: zone target="chromeless"

# <a name="predict-and-influence"></a>Przewidywanie i wpływ

::: zone-end

Twoja innowacyjna firma ma wgląd w dane, zachowania i potrzeby klientów. Analiza tych szczegółowych informacji może pomóc we wcześniejszym przewidywaniu potrzeb klientów. W tym artykule przedstawiono kilka metod dostarczania rozwiązań predykcyjnych. W dalszej części artykułu przedstawiono metody integrowania tych prognoz z rozwiązaniem w celu kształtowania zachowań klientów.

Poniższa tabela ułatwia znalezienie najlepszego rozwiązania w zależności od wymagań implementacji.

|Usługa  |Wstępnie utworzone modele  |Tworzenie i eksperymentowanie  |Trenowanie i tworzenie przy użyciu języka Python|Wymagane umiejętności|
|---------|---------|---------|---------|---------|
|Cognitive Services|Yes|Nie|Nie|Umiejętności deweloperskie i znajomość interfejsu API|
|Azure Machine Learning Studio|Yes|Yes|Nie|Ogólna znajomość algorytmów predykcyjnych|
|Usługa Azure Machine Learning|Yes|Yes|Yes|Analityk danych|

## <a name="azure-cognitive-servicestabcognitiveservices"></a>[Azure Cognitive Services](#tab/CognitiveServices)

Najszybszą i najłatwiejszą metodą uzyskiwania prognoz jest użycie usług Azure Cognitive Services. Usługi Cognitive Services umożliwiają prognozowanie na podstawie istniejących modeli, bez dodatkowego trenowania. Użycie tych usług jest optymalnym rozwiązaniem, jeśli nie ma analityka danych, który może wytrenować model predykcyjny. W przypadku niektórych usług trenowanie nie jest wymagane. Inne usługi wymagają tylko minimalnego trenowania.

Listę dostępnych usług oraz informacje o wymaganym trenowaniu można znaleźć w temacie [Usługi Cognitive Services i uczenie maszynowe](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-and-machine-learning#service-requirements-for-the-data-model).

### <a name="action"></a>Akcja

Aby użyć interfejsu API usługi Cognitive Service:

1. Wybierz pozycję **Cognitive Services**.
2. Kliknij pozycję **Dodaj+** , aby znaleźć usługę Cognitive Service w portalu Marketplace.
3. Jeśli znasz nazwę odpowiedniej usługi, możesz ją wpisać w polu tekstowym **Wyszukaj w witrynie Marketplace**.
4. Możesz też wyświetlić listę usług Cognitive Services. W tym celu kliknij link **Zobacz więcej** obok nagłówka usług Cognitive Services.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts]" submitText="Go to Cognitive Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usług Cognitive Services w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.CognitiveServices%2Faccounts).

::: zone-end

## <a name="azure-machine-learning-studiotabmachinelearningstudio"></a>[Azure Machine Learning Studio](#tab/MachineLearningStudio)

Jeśli istniejące modele w usługach Cognitive Services nie umożliwiają uzyskania odpowiedniej prognozy, z pomocą przychodzi usługa Azure Machine Learning Studio. Pozwala ona utworzyć wymagane prognozy, a przy tym nie wymaga zaawansowanych umiejętności analityka danych.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Za pomocą usługi Azure Machine Learning Studio można utworzyć model i eksperymentować z nim:

1. Wybierz pozycję **Azure Machine Learning Studio**.
2. Kliknij pozycję **Utwórz obszar roboczy Machine Learning Studio** i postępuj zgodnie z instrukcjami, aby utworzyć obszar roboczy.
3. Nowy obszar roboczy zawiera interfejs typu „przeciągnij i upuść”, który pozwala utworzyć model i eksperymentować z nim (jest to alternatywa dla trenowania głębokiego).

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces]" submitText="Go to Azure Machine Learning Studio" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usługi Azure Machine Learning Studio w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearning%2Fworkspaces).

::: zone-end

## <a name="azure-machine-learning-servicetabmachinelearningservice"></a>[Usługa Azure Machine Learning](#tab/MachineLearningService)

Usługa Azure Machine Learning umożliwia korzystanie z bardziej zaawansowanych, opartych na kodzie metod, które są wymagane do trenowania głębokiego zestawów danych klientów. Przy użyciu języków, takich jak Python, analitycy danych mogą trenować, a następnie tworzyć algorytmy umożliwiające przewidywanie potrzeb klientów.

### <a name="action"></a>Akcja

Przy użyciu usługi Azure Machine Learning analityk danych może wytrenować i utworzyć model, korzystając z zaawansowanych języków, takich jak Python:

1. Wybierz pozycję **Usługa Azure Machine Learning**.
2. Kliknij pozycję **Utwórz obszary robocze Machine Learning Service** i postępuj zgodnie z instrukcjami, aby utworzyć obszar roboczy.
3. Nowy obszar roboczy pozwala korzystać z metod opartych na kodzie, które umożliwiają analitykom danych trenowanie i tworzenie modeli wymagających bardziej zaawansowanej analizy do dokładnego przewidywania potrzeb klientów.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces]" submitText="Go to Azure Machine Learning Service" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Możesz przejść bezpośrednio do usługi Azure Machine Learning Studio w witrynie [Azure Portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.MachineLearningServices%2Fworkspaces).

::: zone-end

## <a name="influence"></a>Wywieranie wpływu

Produktem końcowym wszystkich omówionych metod jest interfejs API, który udostępnia model predykcyjny aplikacjom. W swoim rozwiązaniu użyj dowolnej z tych metod, aby przekazać dane zebrane od klienta do predykcyjnego interfejsu API. Możesz następnie zintegrować wyniki ze środowiskiem klienta jako sugerowany krok do wykonania.

Takie następne kroki umożliwiają kształtowanie wzorców zachowań klientów i wpływanie na ich działania. Sugerowane kroki do wykonania są oparte na algorytmach predykcyjnych, dlatego korzystają z dostępnych danych dotyczących wcześniejszych klientów, umożliwiając przewidywanie i spełnianie potrzeb. Często ma to miejsce, zanim klient zorientuje się, że taka potrzeba zaistniała.
