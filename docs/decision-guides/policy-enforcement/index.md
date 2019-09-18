---
title: Przewodnik podejmowania decyzji dotyczących wymuszania zasad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej o subskrypcjach wymuszania zasad jako podstawowym priorytecie projektu podczas migracji na platformę Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 383f2d6a2443c70c8e082183f601b8186fc98870
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023727"
---
# <a name="policy-enforcement-decision-guide"></a>Przewodnik podejmowania decyzji dotyczących wymuszania zasad

Definiowanie zasad organizacyjnych jest nieefektywne, jeśli nie istnieje sposób wymuszania ich w organizacji. Kluczowym aspektem planowania jakiejkolwiek migracji do chmury jest określenie najlepszego sposobu połączenia narzędzi dostarczanych przez platformę chmury z istniejącymi procesami informatycznymi w celu zapewnienia maksymalnej zgodności z zasadami dla całej infrastruktury w chmurze.

![Wykres opcji wymuszania zasad od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-policy-enforcement.png)

Idź do: [Zalecane praktyki dotyczące punktu odniesienia](#baseline-recommended-practices) | [Monitorowanie zgodności zasad](#policy-compliance-monitoring) | [Wymuszanie zasad](#policy-enforcement) | [Zasady dla wielu organizacji](#cross-organization-policy) | [Wymuszanie automatyczne](#automated-enforcement)

Wraz z rozwojem infrastruktury w chmurze pojawi się potrzeba odpowiedniej obsługi i wymuszania zasad w większym zbiorze zasobów i subskrypcji. Gdy infrastruktura staje się coraz większa i rosną wymagania dotyczące zasad organizacji, zakres procesów wymuszania zasad musi zostać rozszerzony, aby zapewnić spójne przestrzeganie zasad i szybkie wykrywanie naruszeń.

Dostarczane przez platformę mechanizmy wymuszania zasad na poziomie zasobów lub subskrypcji zazwyczaj są wystarczające w przypadku mniejszych infrastruktur w chmurze. Większe wdrożenia uzasadniają większy zakres wymuszania i mogą wymagać korzystania z bardziej zaawansowanych mechanizmów wymuszania obejmujących standardy wdrażania, grupowanie i organizację zasobów oraz integrację wymuszania zasad z systemami rejestrowania i raportowania.

Podstawowe czynniki przy ustalaniu zakresu procesów wymuszania zasad to [wymagania dotyczące utrzymania ładu w chmurze](../../govern/index.md) w organizacji, rozmiar i rodzaj infrastruktury w chmurze oraz sposób odzwierciedlenia organizacji w [projekcie subskrypcji](../subscriptions/index.md). Zwiększenie rozmiaru infrastruktury lub większa potrzeba centralnego zarządzania wymuszaniem zasad może usprawiedliwić zwiększenie zakresu wymuszania.

## <a name="baseline-recommended-practices"></a>Zalecane praktyki dotyczące punktu odniesienia

W przypadku pojedynczej subskrypcji i prostych wdrożeń w chmurze wiele zasad firmowych można wymusić przy użyciu funkcji, które są natywne dla zasobów i subskrypcji na platformie Azure. Spójne używanie wzorców omówionych w [przewodnikach podejmowania decyzji](../index.md) dotyczących usługi Cloud Adoption Framework ułatwiają ustalenie poziomu odniesienia zgodności z zasadami bez konieczności inwestowania w wymuszanie zasad. Między innymi są to następujące funkcje:

- [Szablony wdrażania](../resource-consistency/index.md) umożliwiają aprowizowanie zasobów za pomocą standardowej struktury i konfiguracji.
- [Standardy tagowania i nazewnictwa](../resource-tagging/index.md) mogą ułatwić organizowanie operacji oraz spełnienie wymagań w zakresie księgowości i biznesu.
- Ograniczenia dotyczące zarządzania ruchem i sieci można implementować za pośrednictwem [sieci definiowanej przez oprogramowanie](../software-defined-network/index.md).
- [Kontrola dostępu oparta na rolach](../identity/index.md) umożliwia zabezpieczanie oraz izolowanie zasobów w chmurze.

Planowanie wymuszania zasad w chmurze można rozpocząć, sprawdzając, jak aplikacja wzorców standardowych omówionych w tych przewodnikach może pomóc w spełnieniu wymagań organizacyjnych.

## <a name="policy-compliance-monitoring"></a>Monitorowanie zgodności zasad

Pierwszym krokiem poza proste korzystanie z mechanizmów wymuszania zasad dostarczanych przez platformę Azure jest zapewnienie możliwości sprawdzania, czy oparte na chmurze aplikacje i usługi są zgodne z zasadami organizacyjnymi. Obejmuje to funkcje powiadomień służących do alarmowania odpowiednich podmiotów, gdy zasób przestaje być zgodny. Skuteczne [rejestrowanie i raportowanie](../logging-and-reporting/index.md) stanu zgodności obciążeń w chmurze jest kluczowym elementem strategii wymuszania zasad firmowych.

Gdy infrastruktura w chmurze rośnie, dodatkowe narzędzia, takie jak usługa [Azure Security Center](https://docs.microsoft.com/azure/security-center), mogą zapewnić zintegrowane zabezpieczenia i wykrywanie zagrożeń oraz ułatwić stosowanie scentralizowanego zarządzania zasadami i alarmowania w przypadku zasobów lokalnych i zasobów w chmurze.

## <a name="policy-enforcement"></a>Wymuszanie zasad

Na platformie Azure można stosować ustawienia konfiguracji i reguły tworzenia zasobów na poziomie grupy zarządzania, subskrypcji lub grupy zasobów w celu zapewnienia dostosowania zasad.

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) to usługa platformy Azure służąca do tworzenia zasad, przypisywania ich i zarządzania nimi. Te zasady wymuszają różne reguły i efekty dotyczące zasobów, dzięki czemu zasoby te pozostają zgodne ze standardami firmy i umowami dotyczącymi poziomu usług. Usługa Azure Policy ocenia zasoby pod kątem niezgodności z przypisanymi zasadami. Na przykład można ograniczyć rozmiar jednostki SKU maszyn wirtualnych w danym środowisku. Po zaimplementowaniu odpowiednich zasad nowe i istniejące zasoby będą oceniane pod kątem zgodności. Użycie odpowiednich zasad umożliwia zapewnienie zgodności istniejących zasobów.

## <a name="cross-organization-policy"></a>Zasady dla wielu organizacji

Gdy infrastruktura w chmurze powiększy się na wiele subskrypcji wymagających wymuszania, może być konieczne skoncentrowanie się na strategii wymuszania w całej infrastrukturze chmury, aby można było zapewnić spójność zasad.

[Projekt subskrypcji](../subscriptions/index.md) będzie musiał uwzględnić zasady, ponieważ są one związane ze strukturą organizacyjną. Oprócz zapewniania obsługi złożonej organizacji w projekcie subskrypcji, [grupy zarządzania platformy Azure](../../ready/considerations/scaling-subscriptions.md#managing-multiple-subscriptions) umożliwiają także przypisywanie reguł usługi Azure Policy w wielu subskrypcjach.

## <a name="automated-enforcement"></a>Wymuszanie automatyczne

Podczas gdy standardowe szablony wdrażania są skuteczne na mniejszą skalę, usługa [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) umożliwia standardową aprowizację i aranżację wdrożenia rozwiązań platformy Azure w dużej skali. Obciążenia w wielu subskrypcjach można wdrażać przy użyciu spójnych ustawień zasad dla wszystkich utworzonych zasobów.

W przypadku środowisk IT, w których zintegrowano zasoby w chmurze z zasobami lokalnymi, konieczne może być użycie systemów rejestrowania i raportowania w celu zapewnienia funkcji monitorowania hybrydowego. Niestandardowe systemy monitorowania operacyjnego lub systemy innych firm mogą oferować dodatkowe funkcje wymuszania zasad. W przypadku większych lub bardziej dojrzałych infrastruktur w chmurze warto zastanowić się, jak najlepiej zintegrować te systemy z zasobami w chmurze.

## <a name="next-steps"></a>Następne kroki

Wymuszanie zasad to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
