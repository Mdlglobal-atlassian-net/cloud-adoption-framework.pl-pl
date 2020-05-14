---
title: Przewodnik monitorowania chmury
description: Uzyskaj informacje na temat usług Azure Monitor i System Center Operations Manager oraz zalecanej strategii monitorowania poszczególnych modeli wdrożenia chmury.
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: b900826ef28aada53a9a73cdae9679d5f35f3007
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223766"
---
# <a name="cloud-monitoring-guide-introduction"></a>Przewodnik monitorowania chmury: Wprowadzenie

Chmura całkowicie zmienia sposoby, w jakie firmy pozyskują zasoby technologiczne i korzystają z nich. W przeszłości przedsiębiorstwa były właścicielami wszystkich poziomów technologii — od infrastruktury po oprogramowanie — i brały za nie odpowiedzialność. Obecnie chmura oferuje przedsiębiorstwom możliwość aprowizowania i używania zasobów w zależności od potrzeb.

Mimo że chmura zapewnia niemal nieograniczoną elastyczność w zakresie stosowanych rozwiązań, przedsiębiorstwa szukają sprawdzonej i spójnej metodologii wdrażania technologii chmurowych. Każde przedsiębiorstwo ma inne cele i harmonogramy wdrożeń chmury, co powoduje, że opracowanie podejścia do wdrażania, które będzie odpowiednie dla wszystkich, jest prawie niemożliwe.

![Diagram strategii wdrażania chmury](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Ta transformacja cyfrowa jest też szansą na zmodernizowanie infrastruktury, obciążeń i aplikacji. W zależności od strategii biznesowej i celów biznesowych wdrożenie modelu chmury hybrydowej może być częścią procesu migracji ze środowiska lokalnego do pełnej funkcjonalności w chmurze. W trakcie tego procesu zadaniem zespołów IT jest wdrożenie chmury i szybkie urzeczywistnienie jej wartości. Dział IT musi również zapewnić efektywne monitorowanie aplikacji lub usług migrowanych na platformę Azure i w dalszym ciągu dostarczać skuteczne operacje IT/DevOps.

Uczestnicy projektu chcą korzystać z opartych na chmurze narzędzi SaaS (oprogramowanie jako usługa) do monitorowania i zarządzania. Chcą oni wiedzieć, jakie usługi i rozwiązania dostarczać, aby uzyskać pełną widoczność, obniżyć koszty oraz poświęcać mniej czasu na infrastrukturę i konserwację tradycyjnych programowych narzędzi do obsługi operacji IT.

Jednak zespoły IT często wolą nadal korzystać z narzędzi, w które dużo zainwestowały. To podejście obsługuje ich procesy operacji usług do monitorowania obu modeli w chmurze, a ostatecznie przejście na ofertę SaaS. Zespoły IT wolą to rozwiązanie nie tylko ze względu na czasochłonne planowanie, zasoby i koszty przejścia. Wynika to również z niepewności w kwestii, jakie produkty lub usługi platformy Azure są odpowiednie lub mają zastosowanie do osiągnięcia przejścia.

Celem tego przewodnika jest przedstawienie szczegółowej dokumentacji ułatwiającej kierownikom IT w przedsiębiorstwach, osobom podejmującym decyzje biznesowe, architektom aplikacji i deweloperom aplikacji zrozumienie następujących kwestii:

- Platformy monitorowania Azure z omówieniem i porównaniem możliwości.
- Najlepsze rozwiązanie do monitorowania obciążeń hybrydowych i prywatnych oraz obciążeń natywnych platformy Azure.
- Zalecana metoda kompleksowego monitorowania infrastruktury i aplikacji jako całości. Podejście to obejmuje możliwe do wdrożenia rozwiązania na potrzeby migrowania tych typowych obciążeń na platformę Azure.

Ten przewodnik nie zawiera instrukcji dotyczących używania lub konfigurowania poszczególnych usług i rozwiązań platformy Azure, ale zawiera odwołania do tych źródeł, gdy są potrzebne lub dostępne. Z tego przewodnika dowiesz się, jak pomyślnie obsługiwać obciążenie zgodnie z najlepszymi rozwiązaniami i wzorcami.

Jeśli nie znasz usługi Azure Monitor i programu System Center Operations Manager i chcesz dowiedzieć się, co je wyróżnia na tle innych rozwiązań, i porównać je ze sobą, zobacz [Omówienie platform monitorowania](./platform-overview.md).

## <a name="audience"></a>Grupy odbiorców

Ten przewodnik jest przydatny przede wszystkim dla administratorów przedsiębiorstwa, pracowników działu operacji IT oraz działu zabezpieczeń i zgodności IT, architektów aplikacji, a także właścicieli opracowywania obciążeń i właścicieli operacji obciążeń.

## <a name="how-this-guide-is-structured"></a>Struktura tego przewodnika

Ten artykuł jest częścią serii. Następujące artykuły należy przeczytać razem we wskazanej kolejności:

- Wprowadzenie (w tym artykule)
- [Strategia monitorowania modeli wdrażania w chmurze](./cloud-models-monitor-overview.md)
- [Zbieranie właściwych danych](./data-collection.md)
- [Alerty](./alerting.md)

## <a name="products-and-services"></a>Produkty i usługi

Dostępne są usługi i oprogramowanie ułatwiające monitorowanie różnych zasobów hostowanych na platformie Azure, w sieci firmowej lub u innych dostawców usług w chmurze oraz zarządzania nimi. Oto one:

- System Center Operations Manager
- Usługa Azure Monitor (obejmuje usługi Log Analytics i Application Insights)
- Usługi Azure Policy i Azure Blueprints
- Azure Automation
- Azure Logic Apps
- Azure Event Hubs

Ta pierwsza wersja przewodnika obejmuje nasze bieżące platformy monitorowania: Azure Monitor i System Center Operations Manager. Zawiera również opis zalecanej strategii monitorowania poszczególnych modeli wdrażania w chmurze. Ponadto podano pierwszy zbiór zaleceń dotyczących monitorowania, począwszy od alertów i zbierania danych.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Strategia monitorowania modeli wdrażania w chmurze](./cloud-models-monitor-overview.md)
