---
title: 'Przewodnik po innowacjach na platformie Azure: Demokratyzowanie danych'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak zdemokratyzować dane przy użyciu platformy Azure.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 65c1ecd1d722286fb495af3069862131629c35d1
ms.sourcegitcommit: 0d14d89b9004a65a322724342cb5086ad2c77467
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/22/2019
ms.locfileid: "72777085"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Przewodnik po innowacjach na platformie Azure: Demokratyzowanie danych

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratyzowanie danych

::: zone-end

Jednym z pierwszych kroków demokratyzowania danych jest zwiększenie możliwości odnajdywania danych. Katalogowanie udostępniania danych i zarządzanie nim może pomóc przedsiębiorstwom w maksymalnym wykorzystaniu istniejących zasobów informacyjnych. Katalog danych ułatwia odnajdywanie źródeł danych i ich zrozumienie przez użytkowników, którzy zarządzają danymi. Usługa Azure Data Catalog umożliwia zarządzanie danymi w przedsiębiorstwie, natomiast usługa Azure Data Share umożliwia zarządzanie danymi i ich udostępnianie poza przedsiębiorstwem.

Usługi platformy Azure, które umożliwiają przetwarzanie danych, takie jak Azure Time Series Insights i Stream Analytics, to kolejne rozwiązania wykorzystywane przez klientów i partnerów w celu zaspokojenia innowacyjnych potrzeb.

# <a name="catalogtabcatalog"></a>[Wykaz](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Usługa Azure Data Catalog eliminuje wyzwania związane z odnajdywaniem danych przez konsumentów, a także umożliwia producentom danych utrzymywanie zasobów informacyjnych. Zapewnij lepszą komunikację między działem informatycznym i resztą firmy, umożliwiając wszystkim dzielenie się informacjami. Przechowuj dane w wybranym przez siebie miejscu i łącz się przy użyciu wybranych narzędzi. Zachowaj kontrolę nad tym, kto może odnajdować zarejestrowane zasoby danych. Zapewnij integrację z istniejącymi narzędziami i procesami za pomocą otwartych interfejsów API REST.

> [!div class="checklist"]
>
> - Zarejestruj subskrypcję
> - Wyszukuj i dodawaj adnotacje
> - Łącz i zarządzaj

::: zone target="docs"

**Przejdź do usługi [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog).**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

W jednej organizacji jest obsługiwana tylko jedna usługa Azure Data Catalog. Jeśli katalog został już utworzony dla Twojej organizacji, nie można dodawać kolejnych katalogów.

Aby utworzyć usługę Azure Data Catalog dla organizacji:

1. Przejdź do usługi **Azure Data Catalog**.
2. Kliknij przycisk **Utwórz**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2Fcatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="sharetabshare"></a>[Share](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Kluczowym czynnikiem wprowadzania innowacji jest osiągnięcie równowagi między otwartym udostępnianiem danych i kontrolą nad tym, jakie dane są udostępniane i komu są one udostępniane. Podczas demokratyzowania danych organizacje mogą łatwo ulec przeciążeniu z powodu ogromnych ilości danych, tempa ich przetwarzania i złożoności ich cyklu życia. Dzięki usłudze Azure Data Share dostawca może kontrolować sposób przetwarzania swoich danych przez określenie warunków użytkowania udostępnionych danych. Uzyskanie danych jest uzależnione od tego, czy konsument danych zaakceptował te warunki. Dostawcy danych mogą określać częstotliwość, z jaką konsumenci danych będą otrzymywać aktualizacje. Dostawca danych może w dowolnym momencie odwołać dostęp do nowych aktualizacji.

> [!div class="checklist"]
>
> - Utwórz usługę Data Share.
> - Dodaj zestawy danych do usługi Data Share.
> - Włącz harmonogram synchronizacji dla usługi Data Share.
> - Dodaj odbiorców do usługi Data Share.

::: zone target="docs"
**Przejdź do usługi [Azure Data Share](https://docs.microsoft.com/azure/data-share).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby utworzyć usługę Azure Data Share, wykonaj następujące czynności:

1. Przejdź do usługi **Azure Data Share**.
2. Kliknij pozycję **Utwórz usługę Data Share**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2Faccounts]" submitText="Go to Azure Data Share" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

Użyj platformy [Azure Open Datasets](https://docs.microsoft.com/azure/open-datasets/overview-what-are-open-datasets), aby zwiększyć swoje możliwości analityczne przez włączenie do modeli danych dotyczących [świąt](https://azure.microsoft.com/services/open-datasets/catalog/public-holidays) i [pogody](https://azure.microsoft.com/services/open-datasets/catalog/noaa-global-forecast-system) oraz [zdjęć przestrzennych](https://azure.microsoft.com/services/open-datasets/catalog/hls).

Znajdujące się tutaj informacje o [demokratyzacji procesów biznesowych](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/democratize-business-processes) i [zwiększaniu możliwości amatorskich deweloperów](https://docs.microsoft.com/business-applications-release-notes/october18/microsoft-flow/empower-citizen-developers) będą pomocne przy wykonywaniu następnych kroków.

# <a name="insightstabinsights"></a>[Insights](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Dzięki możliwości eksplorowania niemal w czasie rzeczywistym strumieni danych i wielowarstwowych magazynów dla danych szeregów czasowych i modeli w skali IoT na potrzeby określania kontekstu nieprzetworzonych danych telemetrycznych oraz uzyskiwania szczegółowych danych opartych na zasobach, możliwości wprowadzania innowacji danych są nieograniczone. Na platformie Time Series Insights można zapewnić bezproblemową i ciągłą integrację z innymi rozwiązaniami do obsługi danych, udostępnić możliwość analizy głównych przyczyn i wykrywania anomalii, w tym niestandardowe opcje aplikacji.

> [!div class="checklist"]
>
> - Planuj swoje środowisko usługi Time Series Insights.
> - Wizualizuj dane w eksploratorze.
> - Poznawaj zagadnienia związane z przechowywaniem danych.
> - Opracowuj i udostępniaj widoki niestandardowe.

::: zone target="docs"

**Przejdź do platformy [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview).**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

### <a name="action"></a>Akcja

Aby utworzyć środowisko usługi Azure Time Series Insights, wykonaj następujące czynności:

1. Przejdź do platformy **Azure Time Series Insights**.
2. Kliknij pozycję **Utwórz środowisko usługi Time Series Insights**.
3. Wskaż dla tego środowiska źródło zdarzeń — usługę IoT Hub lub centrum zdarzeń.

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2Fenvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
