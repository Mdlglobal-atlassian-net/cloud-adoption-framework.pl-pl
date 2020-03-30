---
title: 'Innowacje na platformie Azure: Demokratyzowanie danych'
description: Dowiedz się więcej o usługach Azure Data Catalog, Azure Data Share i innych narzędziach rozszerzających możliwości odnajdywania i analizy danych.
author: absheik
ms.author: absheik
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0c3a584277d708a0dcef8fcf019ed76589a3fd16
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356650"
---
::: zone target="docs"

# <a name="azure-innovation-guide-democratize-data"></a>Przewodnik po innowacjach na platformie Azure: Demokratyzowanie danych

::: zone-end

::: zone target="chromeless"

# <a name="democratize-data"></a>Demokratyzowanie danych

::: zone-end

Jednym z pierwszych kroków demokratyzowania danych jest zwiększenie możliwości ich odnajdywania. Katalogowanie udostępniania danych i zarządzanie nim może pomóc przedsiębiorstwom w maksymalnym wykorzystaniu istniejących zasobów informacyjnych. Katalog danych ułatwia odnajdywanie źródeł danych i ich zrozumienie przez użytkowników, którzy zarządzają danymi. Usługa Azure Data Catalog umożliwia zarządzanie danymi w przedsiębiorstwie, natomiast usługa Azure Data Share umożliwia zarządzanie danymi i ich udostępnianie poza przedsiębiorstwem.

Usługi platformy Azure, które umożliwiają przetwarzanie danych, takie jak Azure Time Series Insights i Stream Analytics, to kolejne rozwiązania wykorzystywane przez klientów i partnerów w celu zaspokojenia innowacyjnych potrzeb.

# <a name="catalog"></a>[Wykaz](#tab/Catalog)

## <a name="azure-data-catalog"></a>Azure Data Catalog

Usługa Azure Data Catalog eliminuje wyzwania związane z odnajdywaniem danych przez konsumentów oraz umożliwia producentom danych utrzymywanie zasobów informacyjnych. Usługa zapewnia lepszą komunikację między działem informatycznym i resztą firmy, umożliwiając wszystkim dzielenie się informacjami. Dane można przechowywać w dowolnym miejscu i łączyć je z narzędziami, których chcesz używać. Za pomocą usługi Azure Data Catalog można kontrolować, kto może odnajdywać zarejestrowane zasoby danych. Możesz zapewnić integrację z istniejącymi narzędziami i procesami za pomocą otwartych interfejsów API REST.

> [!div class="checklist"]
>
> - Zarejestruj
> - Wyszukuj i dodawaj adnotacje
> - Łącz i zarządzaj

::: zone target="docs"

**Przejdź do [dokumentacji dotyczącej usługi Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

W jednej organizacji można używać tylko jednej usługi Azure Data Catalog. Jeśli katalog danych został już utworzony dla Twojej organizacji, nie można dodawać kolejnych katalogów.

Aby utworzyć usługę Azure Data Catalog dla organizacji:

1. Przejdź do usługi **Azure Data Catalog**.
2. Wybierz pozycję **Utwórz**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataCatalog%2FCatalogs]" submitText="Go to Azure Data Catalog" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="share"></a>[Share](#tab/Share)

## <a name="azure-data-share"></a>Azure Data Share

Kluczowym czynnikiem wprowadzania innowacji jest osiągnięcie równowagi między otwartym udostępnianiem danych i kontrolą nad tym, jakie dane są udostępniane i komu. Podczas próby demokratyzowania danych organizacje mogą łatwo ulec przeciążeniu z powodu ogromnych ilości danych, tempa ich przetwarzania i złożoności ich cyklu życia. Usługa Azure Data Share sprawia, że dostawca może kontrolować sposób przetwarzania swoich danych przez określenie warunków użytkowania udostępnionych danych. Przed otrzymaniem danych odbiorca danych musi zaakceptować te warunki. Dostawcy danych mogą określać częstotliwość, z jaką konsumenci danych będą otrzymywać aktualizacje. Dostawca danych może w dowolnym momencie odwołać dostęp do nowych aktualizacji.

> [!div class="checklist"]
>
> - Utwórz usługę Data Share.
> - Dodaj zestawy danych do usługi Data Share.
> - Włącz harmonogram synchronizacji dla usługi Data Share.
> - Dodaj odbiorców do usługi Data Share.

::: zone target="docs"
**Przejdź do [dokumentacji dotyczącej usługi Azure Data Share](https://docs.microsoft.com/azure/data-share)**

::: zone-end

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby utworzyć udział danych:

1. Przejdź do **udziałów usługi Azure Data Share**.
2. Kliknij pozycję **Utwórz udział danych**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.DataShare%2FAccounts]" submitText="Go to Azure Data Shares" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

# <a name="insights"></a>[Insights](#tab/Insights)

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Możliwości wprowadzania innowacji w zakresie danych przy użyciu usługi Azure Time Series Insights są nieograniczone. Usługa udostępnia eksplorację danych strumieni danych w czasie zbliżonym do rzeczywistego i wielowarstwowy magazyn dla danych szeregów czasowych w skali IoT. Ponadto zapewnia modele na potrzeby określania kontekstu nieprzetworzonych danych telemetrycznych i uzyskiwania szczegółowych danych opartych na zasobach. Na platformie Time Series Insights można zapewnić bezproblemową i ciągłą integrację z innymi rozwiązaniami do obsługi danych, udostępnić możliwość analizy głównych przyczyn i wykrywania anomalii, w tym niestandardowe opcje aplikacji.

> [!div class="checklist"]
>
> - Planuj swoje środowisko usługi Time Series Insights.
> - Wizualizuj dane w eksploratorze.
> - Poznawaj zagadnienia związane z przechowywaniem danych.
> - Opracowuj i udostępniaj widoki niestandardowe.

::: zone target="docs"

**Przejdź do [omówienia usługi Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-update-overview)**

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby utworzyć środowisko usługi Azure Time Series Insights, wykonaj następujące czynności:

1. Przejdź do **środowisk usługi Azure Time Series Insights**.
2. Wybierz pozycję **Utwórz środowisko usługi Time Series Insights**.
3. Wskaż dla tego środowiska źródło zdarzeń — usługę Azure IoT Hub lub Event Hubs.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.TimeSeriesInsights%2FEnvironments]" submitText="Go to Azure Time Series Insights" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
