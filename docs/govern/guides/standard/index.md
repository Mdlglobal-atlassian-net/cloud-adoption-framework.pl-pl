---
title: Przewodnik dotyczący ładu dla przedsiębiorstw standardowych
description: Zobacz, jak fikcyjne standardowe przedsiębiorstwo przechodzi przez różne etapy dojrzałości ładu podczas definiowania produktu o podstawowej funkcjonalności w oparciu o najlepsze rozwiązania.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 67412e36a4048d1441679458bbff5a90bbceaa84
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214785"
---
# <a name="standard-enterprise-governance-guide"></a>Przewodnik dotyczący ładu dla przedsiębiorstw standardowych

## <a name="overview-of-best-practices"></a>Omówienie najlepszych rozwiązań

Ten przewodnik po ładzie śledzi doświadczenia fikcyjnej firmy na różnych etapach dojrzałości ładu. Jest ona oparta na doświadczeniach prawdziwych klientów. Najlepsze rozwiązania są oparte na ograniczeniach i potrzebach fikcyjnej firmy.

Jako szybki punkt startowy, to omówienie definiuje minimalną konieczną funkcjonalność (MVP) dla ładu na podstawie najlepszych rozwiązań. Zawiera także linki do pewnych etapów rozwoju ładu, które wprowadzają kolejne najlepsze rozwiązania w miarę pojawiania się nowego ryzyka biznesowego lub technicznego.

> [!WARNING]
> Ten program MVP jest punktem startowym planu bazowego opartego na zestawie założeń. Nawet ten minimalny zestaw najlepszych rozwiązań jest oparty na zasadach firmowych opracowanych na podstawie unikatowego ryzyka biznesowego i tolerancji ryzyka. Aby sprawdzić, czy te założenia mają zastosowanie do Twojego przypadku, przeczytaj [dłuższy opis](./narrative.md) dla tego artykułu.

### <a name="governance-best-practices"></a>Najlepsze rozwiązania dotyczące ładu

Te najlepsze rozwiązania stanowią podstawę, przy użyciu której organizacja może szybko i spójnie dodać zabezpieczenia ładu w Twoich subskrypcjach platformy Azure.

### <a name="resource-organization"></a>Organizacja zasobów

Poniższy diagram przedstawia hierarchię MVP ładu na potrzeby organizowania zasobów.

![Diagram organizacji zasobów](../../../_images/govern/resource-organization.png)

Każda aplikacja powinna zostać wdrożona w odpowiednim obszarze grupy zarządzania, subskrypcji i hierarchii grupy zasobów. Podczas planowania wdrożenia zespół ds. zapewnienia ładu w chmurze utworzy w hierarchii niezbędne węzły, aby pomóc zespołom wdrażania chmury.

1. Jedna grupa zarządzania dla każdego typu środowiska (np. produkcyjne, deweloperskie i testowe).
2. Dwie subskrypcje, pierwsza dla obciążeń produkcyjnych, a druga dla obciążeń nieprodukcyjnych.
3. Na każdym poziomie tej hierarchii grupowania należy stosować [spójną nomenklaturę](../../../ready/azure-best-practices/naming-and-tagging.md).
4. Grupy zasobów należy wdrażać w sposób, który uwzględnia cykl życia ich zawartości: wszystko co jest wspólnie opracowywane, zarządzane i wycofywane, podlega tym samym operacjom. Więcej informacji o najlepszych rozwiązaniach dotyczących grup zasobów możesz znaleźć [tutaj](../../../decision-guides/resource-consistency/index.md).
5. [Wybór regionu](../../../migrate/azure-best-practices/multiple-regions.md) jest niezwykle istotny i należy o nim pamiętać, aby praca w sieci, monitorowanie i inspekcja odbywały się w odpowiedni sposób względem operacji przełączenia w tryb failover i powrotu po awarii, oraz wysyłane było potwierdzenie, że [wymagane jednostki SKU są dostępne w preferowanych regionach](https://azure.microsoft.com/global-infrastructure/services).

Oto przykład zastosowania tego wzorca:

![Przykład organizacji zasobów dla średniej firmy](../../../_images/govern/mid-market-resource-organization.png)

Te wzorce pozostawiają przestrzeń na rozwój bez niepotrzebnego komplikowania hierarchii.

[!INCLUDE [governance-of-resources](../../../../includes/governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Iteracyjne ulepszenia ładu

Po wdrożeniu tego programu MVP można szybko włączyć do środowiska dodatkowe warstwy ładu. Oto kilka sposobów ulepszenia programu MVP w celu zaspokojenia określonych potrzeb firmy:

- [Punkt odniesienia zabezpieczeń dla chronionych danych](./security-baseline-improvement.md)
- [Konfiguracje zasobów dla aplikacji o kluczowym znaczeniu](./resource-consistency-improvement.md)
- [Mechanizmy kontroli do zarządzania kosztami](./cost-management-improvement.md)
- [Mechanizmy kontroli na potrzeby rozwoju środowiska wielochmurowego](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Co zapewniają te wskazówki?

W programie MVP określono praktyki i narzędzia z dyscypliny [Przyspieszanie wdrażania](../../deployment-acceleration/index.md) umożliwiające szybkie zastosowanie zasad firmowych. W szczególności w programie MVP są używane usługi Azure Blueprints i Azure Policy oraz grupy zarządzania platformy Azure w celu zastosowania kilku podstawowych zasad firmowych, jak zdefiniowano w opisie dla tej fikcyjnej firmy. Te zasady firmowe są stosowane przy użyciu szablonów usługi Azure Resource Manager i zasad platformy Azure w celu ustanowienia małego planu bazowego dla tożsamości i zabezpieczeń.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Przyrostowe ulepszanie praktyk w zakresie zapewniania ładu

Wraz z upływem czasu ten program MVP ładu będzie używany do ulepszania praktyk w zakresie zapewniania ładu. Wraz z postępem wdrażania rośnie ryzyko biznesowe. W ramach modelu zapewniania ładu przewodnika Cloud Adoption Framework będą zmieniane różnorodne dyscypliny do zarządzania tym ryzykiem. W kolejnych artykułach z tej serii omówiono przyrostowe ulepszanie zasad firmowych wpływających na fikcyjną firmę. Te ulepszenia mają miejsce w ramach trzech dyscyplin:

- Usługa Cost Management — w miarę zwiększania skali wdrożenia.
- Punkt odniesienia zabezpieczeń — w miarę wdrażania chronionych danych.
- Spójność zasobów — gdy zespół ds. operacji IT zaczyna obsługiwać obciążenia o znaczeniu krytycznym.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-improvement.png)

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już program MVP ładu i wiesz, jakie są etapy ulepszania ładu, które można śledzić, przeczytaj opis pomocniczy, aby uzyskać dodatkowy kontekst.

> [!div class="nextstepaction"]
> [Przeczytaj opis pomocniczy](./narrative.md)
