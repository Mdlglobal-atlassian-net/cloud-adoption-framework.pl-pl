---
title: Przewodnik dotyczący ładu dla przedsiębiorstw złożonych
description: Przewodnik dotyczący ładu dla przedsiębiorstw złożonych
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2485aa48a8af05fdf945f39523439743f30977c6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805748"
---
# <a name="governance-guide-for-complex-enterprises"></a>Przewodnik dotyczący ładu dla przedsiębiorstw złożonych

## <a name="overview-of-best-practices"></a>Omówienie najlepszych rozwiązań

Ten przewodnik po ładzie śledzi doświadczenia fikcyjnej firmy na różnych etapach dojrzałości ładu. Jest ona oparta na doświadczeniach prawdziwych klientów. Sugerowane najlepsze rozwiązania są oparte na ograniczeniach i potrzebach fikcyjnej firmy.

Jako szybki punkt startowy, to omówienie definiuje minimalną konieczną funkcjonalność (MVP) dla ładu na podstawie najlepszych rozwiązań. Zawiera także linki do pewnych etapów rozwoju ładu, które wprowadzają kolejne najlepsze rozwiązania w miarę pojawiania się nowego ryzyka biznesowego lub technicznego.

> [!WARNING]
> Ten program MVP jest punktem startowym planu bazowego opartego na zestawie założeń. Nawet ten minimalny zestaw najlepszych rozwiązań jest oparty na zasadach firmowych opracowanych na podstawie unikatowego ryzyka biznesowego i tolerancji ryzyka. Aby sprawdzić, czy te założenia mają zastosowanie do Twojego przypadku, przeczytaj [dłuższy opis](./narrative.md) dla tego artykułu.

### <a name="governance-best-practices"></a>Najlepsze rozwiązania dotyczące ładu

Te najlepsze rozwiązania stanowią podstawę, przy użyciu której organizacja może szybko i spójnie dodać zabezpieczenia ładu w wielu subskrypcjach platformy Azure.

### <a name="resource-organization"></a>Organizacja zasobów

Poniższy diagram przedstawia hierarchię MVP ładu na potrzeby organizowania zasobów.

![Diagram organizacji zasobów](../../../_images/govern/resource-organization.png)

Każda aplikacja powinna zostać wdrożona w odpowiednim obszarze grupy zarządzania, subskrypcji i hierarchii grupy zasobów. Podczas planowania wdrożenia zespół ds. zapewnienia ładu w chmurze utworzy w hierarchii niezbędne węzły, aby pomóc zespołom wdrażania chmury.

1. Najpierw zdefiniuj grupę zarządzania dla każdej jednostki biznesowej ze szczegółową hierarchią, która odzwierciedla lokalizację geograficzną, a następnie typ środowiska (na przykład środowisko produkcyjne lub nieprodukcyjne).
2. Utwórz subskrypcję produkcyjną i subskrypcję nieprodukcyjną dla każdej unikatowej kombinacji odrębnej jednostki biznesowej lub lokalizacji geograficznej. Tworzenie różnych subskrypcji wymaga uważnego podejścia. Aby uzyskać więcej informacji, zobacz [Przewodnik po decyzji dotyczącej subskrypcji](../../../decision-guides/subscriptions/index.md).
3. Na każdym poziomie tej hierarchii grupowania zastosuj [spójną nomenklaturę](../../../ready/azure-best-practices/naming-and-tagging.md).
4. Grupy zasobów powinny być wdrażane z uwzględnieniem ich cyklu życia zawartości. Zasoby, które są wspólnie tworzone, zarządzane i wycofywane, powinny należeć do tej samej grupy zasobów. Aby uzyskać więcej informacji o najlepszych rozwiązaniach dotyczących używania grup zasobów, [zobacz tutaj](../../../decision-guides/resource-consistency/index.md).
5. [Wybór regionu](../../../decision-guides/regions/index.md) jest niezwykle istotny i należy o nim pamiętać, aby praca w sieci, monitorowanie i inspekcja odbywały się w odpowiedni sposób względem operacji przełączenia w tryb failover i powrotu po awarii, oraz wysyłane było potwierdzenie, że [wymagane jednostki SKU są dostępne w preferowanych regionach](https://azure.microsoft.com/global-infrastructure/services).

![Diagram organizacji zasobów w dużym przedsiębiorstwie](../../../_images/govern/large-enterprise-resource-organization.png)

Te wzorce pozostawiają przestrzeń na rozwój bez niepotrzebnego komplikowania hierarchii.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

<!-- See comments for suggestion to possibly add here -->

## <a name="incremental-governance-improvements"></a>Przyrostowe ulepszenia ładu

Po wdrożeniu tego programu MVP można szybko włączyć do środowiska dodatkowe warstwy ładu. Oto kilka sposobów ulepszenia programu MVP w celu zaspokojenia określonych potrzeb firmy:

- [Punkt odniesienia zabezpieczeń dla chronionych danych](./security-baseline-improvement.md)
- [Konfiguracje zasobów dla aplikacji o kluczowym znaczeniu](./resource-consistency-improvement.md)
- [Mechanizmy kontroli do zarządzania kosztami](./cost-management-improvement.md)
- [Mechanizmy kontroli do przyrostowego ulepszania wielochmurowego](./multicloud-improvement.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>Co zapewniają te wskazówki?

W programie MVP ustanawiane są praktyki i narzędzia z dyscypliny [Przyspieszanie wdrażania](../../deployment-acceleration/index.md) w celu szybkiego zastosowania zasad firmowych. W szczególności w programie MVP są używane usługi Azure Blueprints i Azure Policy oraz grupy zarządzania platformy Azure w celu zastosowania kilku podstawowych zasad firmowych, jak zdefiniowano w opisie dla tej fikcyjnej firmy. Te zasady firmowe są stosowane przy użyciu szablonów usługi Azure Resource Manager i zasad platformy Azure w celu ustanowienia małego planu bazowego dla tożsamości i zabezpieczeń.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp.png)

## <a name="incremental-improvements-to-governance-practices"></a>Przyrostowe ulepszanie praktyk w zakresie zapewniania ładu

Wraz z upływem czasu ten program MVP ładu będzie używany do przyrostowego ulepszania praktyk w zakresie zapewniania ładu. Wraz z postępem wdrażania rośnie ryzyko biznesowe. W ramach modelu zapewniania ładu przewodnika Cloud Adoption Framework będą dostosowywane różnorodne dyscypliny do zarządzania tym ryzykiem. W kolejnych artykułach z tej serii omówiono zmiany zasad firmowych wpływających na fikcyjną firmę. Te zmiany mają miejsce w ramach czterech dyscyplin:

- Punkt odniesienia obsługi tożsamości — w miarę zmian zależności migracji.
- Usługa Cost Management — w miarę zwiększania skali wdrożenia.
- Punkt odniesienia zabezpieczeń — w miarę wdrażania chronionych danych.
- Spójność zasobów — gdy zespół ds. operacji IT zaczyna obsługiwać obciążenia o znaczeniu krytycznym.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-improvement-large.png)

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już program MVP ładu i nadchodzące zmiany w zakresie ładu, przeczytaj opis pomocniczy, aby uzyskać dodatkowy kontekst.

> [!div class="nextstepaction"]
> [Przeczytaj opis pomocniczy](./narrative.md)
