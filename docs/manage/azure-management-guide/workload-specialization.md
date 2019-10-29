---
title: Specjalizacja obciążeń dotycząca zarządzania chmurą na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Usprawnienie operacji zarządzania chmurą specyficznych dla obciążeń
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 51bdf23ccb2262202dfa095c5e9b57f727d11d3b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556993"
---
# <a name="workload-specialization-for-cloud-management"></a>Specjalizacja obciążeń dotycząca zarządzania chmurą

Specjalizacja obciążeń bazuje na pojęciach przedstawionych w temacie [Specjalizacja platformy](./platform-specialization.md).

![Rozszerzenie planu bazowego zarządzania chmurą](../../_images/manage/beyond-the-baseline.png)

- **Operacje obciążeń:** Inwestycje w operacje największe na obciążenie. Najwyższy poziom odporności. Zalecane dla +/-20% obciążeń, które zwiększają wartość biznesową. Zazwyczaj zarezerwowane dla obciążeń o dużym lub krytycznym znaczeniu.
- **Operacje platformy:** Inwestycje w operacje są rozłożone na wiele obciążeń. Ulepszenia w zakresie odporności mają wpływ na wszystkie obciążenia, które korzystają ze zdefiniowanej platformy. Zalecane dla +/-20% platform o krytycznym znaczeniu. Zazwyczaj zarezerwowane dla obciążeń o średniej i dużej ważności.
- **Rozszerzony plan bazowy zarządzania:** Relatywnie najniższe inwestycje w operacje. Nieco udoskonalone zobowiązania biznesowe dzięki dodatkowym, natywnym dla chmury narzędziom i procesom obsługi operacji.

## <a name="high-level-process"></a>Przetwarzanie wysokiego poziomu

Specjalizacja obciążeń obejmuje zdyscyplinowane wykonywanie czterech poniższych procesów w ramach podejścia iteracyjnego. Wszystkie procesy zostały szczegółowo opisane w artykule [Specjalizacja platformy](./platform-specialization.md).

- **Ulepszanie projektu systemu:** Usprawnij projekt określonego obciążenia, aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach większy sens może mieć automatyzacja korygowania i ograniczenie wpływu przerw.
- **Skalowanie rozwiązania:** W miarę ulepszania projektu systemów i zautomatyzowanego korygowania zmiany te można skalować na całe środowisko za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Różne narzędzia do monitorowania umożliwiają wykrywanie ulepszeń przyrostowych, które można wprowadzić w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

## <a name="cultural-change"></a>Zmiana kulturowa

Specjalizacja obciążeń często wyzwala zmianę kulturową. W tradycyjnych obciążeniach informatycznych występują procesy ukierunkowane na tworzeniu planu bazowego zarządzania, rozszerzonych planach bazowych i operacjach na platformie. Te typy ofert można skalować w całym środowisku. Specjalizacja obciążeń jest bardzo podobna do specjalizacji platformy. Jednak w przeciwieństwie do typowych platform specjalizacja wymagana przez poszczególne obciążenia często nie jest skalowana.

Gdy pojawia się konieczność wprowadzenia specjalizacji obciążeń, zarządzanie operacyjne często wykracza poza perspektywę centralnego działu IT. Podejście sugerowane w strukturze wdrażania chmury polega na rozproszeniu funkcji zarządzania chmurą.

W tym modelu zadania operacyjne, takie jak monitorowanie, wdrażanie, DevOps oraz inne innowacyjne funkcje, są przesuwane do obszaru tworzenia aplikacji lub organizacji jednostki biznesowej. Zespół ds. platformy w chmurze i podstawowy zespół ds. monitorowania chmury wciąż uczestniczą w tworzeniu planu bazowego zarządzania w całym środowisku. Te scentralizowane zespoły kierują również pracą wyspecjalizowanych zespołów ds. obciążeń, udzielając porad w zakresie operacji związanych z obciążeniami. Jednak codzienne czynności związane z zarządzaniem operacyjnym są wykonywane przez zespół ds. zarządzania chmurą, który nie należy do działu IT. Taka rozproszona kontrola jest jednym z głównych wskaźników dojrzałości zespołu centrum doskonałości chmury.

## <a name="beyond-platform-specialization---application-insights"></a>Nie tylko specjalizacja platformy — usługa Application Insights

Zapewnienie przejrzystych operacji obciążeń wymaga większej liczby szczegółowych informacji dotyczących konkretnego obciążenia. W fazie ciągłego ulepszania usługa Application Insights staje się niezbędnym dodatkiem do łańcucha narzędzi zarządzania chmurą.

|Monitorowanie aplikacji|Application Insights|Monitorowanie i diagnostyka aplikacji| |Wydajność, dostępność i użycie|Application Insights|Zaawansowane monitorowanie aplikacji za pomocą pulpitu nawigacyjnego aplikacji, złożonych map oraz funkcji użycia i śledzenia|

### <a name="deploy-application-insights"></a>Wdrażanie usługi Application Insights

1. W witrynie Azure Portal wyszukaj tekst **Application Insights**.
2. Kliknij pozycję **+ Dodaj**, aby utworzyć zasób usługi Application Insights umożliwiający monitorowanie aktywnej aplikacji internetowej.
3. Postępuj zgodnie z instrukcjami wyświetlanymi na ekranie

Aby uzyskać wskazówki dotyczące konfigurowania monitorowania aplikacji, zobacz [Centrum usługi Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub).

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Monitorowanie wydajności, dostępności i użycia

1. W witrynie Azure Portal wyszukaj tekst **Application Insights**.
2. Wybierz z listy jeden z zasobów usługi Application Insights

Obszar nawigacji usługi Application Insights zawiera różne opcje monitorowania wydajności, dostępności, użycia i zależności. Poszczególne widoki danych aplikacji zapewniają wgląd w pętlę informacji zwrotnych ciągłego ulepszania.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/microsoft.insights%2Fcomponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
