---
title: Wyspecjalizowane obciążenia dotyczące zarządzania chmurą
description: Aby dowiedzieć się więcej o operacjach zarządzania chmurą dotyczących wyspecjalizowanych obciążeń, skorzystaj z podręcznika Cloud Adoption Framework dla platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 06389b972ee01079a3927515c95d3f3ae3cab3de
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80426565"
---
# <a name="workload-specialization-for-cloud-management"></a>Specjalizacja obciążeń dotycząca zarządzania chmurą

Specjalizacja obciążeń bazuje na pojęciach przedstawionych w temacie [Specjalizacja platformy](./platform-specialization.md).

![Rozszerzenie planu bazowego zarządzania chmurą](../../_images/manage/beyond-the-baseline.png)

- **Operacje obciążeń:** Inwestycje w operacje największe na obciążenie i najwyższy poziom odporności. Zalecamy operacje obciążeń dla około 20% obciążeń, które zwiększają wartość biznesową. Ta specjalizacja jest zazwyczaj zarezerwowana dla obciążeń o dużym lub krytycznym znaczeniu.
- **Operacje platformy:** Inwestycje w operacje są rozłożone na wiele obciążeń. Ulepszenia w zakresie odporności wpływają na wszystkie obciążenia korzystające ze zdefiniowanej platformy. Sugerujemy operacje platformy dla około 20% platform o krytycznym znaczeniu. Ta specjalizacja jest zazwyczaj zarezerwowana dla obciążeń o średniej i dużej ważności.
- **Rozszerzony plan bazowy zarządzania:** Relatywnie najniższe inwestycje w operacje. Ta specjalizacja nieco udoskonala zobowiązania biznesowe dzięki dodatkowym, natywnym dla chmury narzędziom i procesom obsługi operacji.

## <a name="high-level-process"></a>Przetwarzanie wysokiego poziomu

Specjalizacja obciążeń obejmuje zdyscyplinowane wykonywanie czterech poniższych procesów w ramach podejścia iteracyjnego. Wszystkie procesy zostały szczegółowo opisane w artykule [Specjalizacja platformy](./platform-specialization.md).

- **Ulepszanie projektu systemu:** Usprawnij projekt określonego obciążenia, aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach większy sens może mieć automatyzacja korygowania i ograniczenie wpływu przerw.
- **Skalowanie rozwiązania:** W miarę ulepszania projektu systemów i zautomatyzowanego korygowania zmiany te można skalować na całe środowisko za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Różne narzędzia do monitorowania umożliwiają wykrywanie ulepszeń przyrostowych. Te ulepszenia można wprowadzić w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

## <a name="cultural-change"></a>Zmiana kulturowa

Specjalizacja obciążeń często wyzwala zmianę kulturową w tradycyjnych procesach informatycznych skupionych na tworzeniu planu bazowego zarządzania, rozszerzonych planach bazowych i operacjach platformy. Te typy ofert można skalować w całym środowisku. Specjalizacja obciążeń jest podobna do specjalizacji platformy. Jednak w przeciwieństwie do typowych platform specjalizacja wymagana przez poszczególne obciążenia często nie jest skalowana.

Gdy pojawia się konieczność wprowadzenia specjalizacji obciążeń, zarządzanie operacyjne zwykle wykracza poza perspektywę centralnego działu IT. Podejście sugerowane w strukturze wdrażania chmury polega na rozproszeniu funkcji zarządzania chmurą.

W tym modelu zadania operacyjne, takie jak monitorowanie, wdrażanie, DevOps oraz inne innowacyjne funkcje, są przesuwane do obszaru tworzenia aplikacji lub organizacji jednostki biznesowej. Zespół ds. platformy w chmurze i podstawowy zespół ds. monitorowania chmury wciąż uczestniczą w tworzeniu planu bazowego zarządzania w całym środowisku.

Te scentralizowane zespoły kierują również pracą wyspecjalizowanych zespołów ds. obciążeń, udzielając porad w zakresie operacji związanych z obciążeniami. Jednak codzienne czynności związane z zarządzaniem operacyjnym są wykonywane przez zespół ds. zarządzania chmurą, który nie należy do działu IT. Taka rozproszona kontrola jest jednym z głównych wskaźników dojrzałości zespołu centrum doskonałości chmury.

## <a name="beyond-platform-specialization-application-insights"></a>Poza specjalizacją platformy: Application Insights

Zapewnienie przejrzystych operacji obciążeń wymaga większej liczby szczegółowych informacji dotyczących konkretnego obciążenia. W fazie ciągłego ulepszania usługa Application Insights staje się niezbędnym dodatkiem do łańcucha narzędzi zarządzania chmurą.

|Wymaganie|Narzędzie|Przeznaczenie|
|---|---|---|
|Monitorowanie aplikacji|Application Insights|Monitorowanie i diagnostyka aplikacji|
|Wydajność, dostępność i użycie|Application Insights|Zaawansowane monitorowanie aplikacji za pomocą pulpitu nawigacyjnego aplikacji, złożonych map oraz funkcji użycia i śledzenia|

### <a name="deploy-application-insights"></a>Wdrażanie usługi Application Insights

1. W witrynie Azure Portal przejdź do aplikacji **Application Insights**.
1. Wybierz pozycję **+ Dodaj**, aby utworzyć zasób usługi Application Insights umożliwiający monitorowanie aktywnej aplikacji internetowej.
1. Postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.

Aby uzyskać wskazówki dotyczące konfigurowania monitorowania aplikacji, zobacz [Centrum usługi Azure Monitor Application Insights](https://docs.microsoft.com/azure/azure-monitor/azure-monitor-app-hub).

::: zone target="chromeless"

::: form action="OpenBlade[#create/Microsoft.AppInsights]" submitText="Create Application Insight resources" :::

::: zone-end

### <a name="monitor-performance-availability-and-usage"></a>Monitorowanie wydajności, dostępności i użycia

1. W witrynie Azure Portal wyszukaj tekst **Application Insights**.
1. Wybierz z listy jeden z zasobów usługi Application Insights.

Usługa Application Insights oferuje różne opcje monitorowania wydajności, dostępności, użycia i zależności. Poszczególne widoki danych aplikacji zapewniają wgląd w pętlę informacji zwrotnych ciągłego ulepszania.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Insights%2FComponents]" submitText="Monitor applications" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
