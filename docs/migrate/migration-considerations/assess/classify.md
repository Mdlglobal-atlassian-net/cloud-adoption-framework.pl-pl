---
title: Klasyfikacja obciążenia przed migracją
description: Klasyfikowanie obciążeń podczas oceny wstępnej migracji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2378c3ba3e17a9c1408a07c65129dc853a83d8b2
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432834"
---
# <a name="workload-classification-before-migration"></a>Klasyfikacja obciążenia przed migracją

Podczas każdej iteracji procesu migracji co najmniej jedno obciążenie zostanie zmigrowane i podwyższone do środowiska produkcyjnego. Przed każdą z tych działań migracji ważne jest klasyfikowanie poszczególnych obciążeń. Klasyfikacja ułatwia wyjaśnienie wymagań związanych z zarządzaniem, zabezpieczeniami, działaniami i danymi.

Poniższe wskazówki dotyczą sugerowanych wymagań dotyczących tagowania przedstawionych w [artykule nazewnictwo i określanie wzorców oznakowania](../../../ready/azure-best-practices/naming-and-tagging.md#metadata-tags) przez dodanie ważnych [operacji](../../../manage/considerations/criticality.md#criticality-scale) i elementów [ładu](../../../govern/guides/complex/prescriptive-guidance.md#resource-tagging) .

W tym artykule zasugerujemy zwiększenie znaczenia i czułości danych do istniejących standardów oznakowania. Każdy z tych punktów danych pomoże innym zespołom zrozumieć, które obciążenia mogą wymagać dodatkowej uwagi lub pomocy technicznej.

## <a name="data-sensitivity"></a>Czułość danych

Jak opisano w artykule dotyczącym [klasyfikacji danych](../../../govern/policy-compliance/data-classification.md), klasyfikacja danych mierzy wpływ przecieku danych na firmę lub klientów. Zespoły nadzoru i zabezpieczeń wykorzystują czułość lub klasyfikację danych jako wskaźnik zagrożeń bezpieczeństwa. Podczas oceny zespół ds. wdrażania chmury powinien ocenić klasyfikację danych dla każdego obciążenia przeznaczonego do migracji i udostępnić tę klasyfikację zespołom pomocniczym. Obciążenia przeznaczone wyłącznie na "dane publiczne" mogą nie mieć wpływu na zespoły pomocnicze. Jednak w miarę jak dane przenoszone są do końca "wysoce poufne", zarówno zespoły nadzoru, jak i zabezpieczenia będą prawdopodobnie miały udział w ocenie obciążenia.

Pracuj z zespołami ds. zabezpieczeń i zarządzania tak szybko, jak to możliwe, aby zdefiniować następujące elementy:

- Czysty proces udostępniania wszelkich obciążeń w zaległości z danymi poufnymi.
- Zrozumienie wymagań dotyczących ładu i linii bazowej zabezpieczeń wymaganych do różnych różnych poziomów czułości danych.
- Wszelka czułość danych może mieć wpływ na projekt subskrypcji, hierarchie grup zarządzania lub wymagania dotyczące strefy docelowej.
- Wszelkie wymagania dotyczące testowania klasyfikacji danych, które mogą obejmować określone narzędzia lub zdefiniowany zakres klasyfikacji.

## <a name="mission-criticality"></a>Krytyczne znaczenie dla działalności

Zgodnie z opisem w artykule dotyczącym [krytycznego obciążenia](../../../manage/considerations/criticality.md), krytyczne znaczenie dla obciążenia jest miarą znaczącego wpływu na działalność podczas przestoju. Ten punkt danych ułatwia zespołom ds. zarządzania i bezpieczeństwa ocenę ryzyka dotyczącego awarii i naruszeń. Podczas oceny zespół ds. wdrażania chmury powinien ocenić istotność dla każdego obciążenia przeznaczonego do migracji i udostępnić tę klasyfikację zespołom pomocniczym. Obciążenia "niskie" lub "nieobsługiwane" mogą mieć niewielki wpływ na zespoły pomocnicze. Jednak w przypadku obciążeń "klasyfikacje" krytyczne "lub" krytyczne dla jednostek ", ich zależności operacyjne stają się bardziej widoczne.

Pracuj z zespołami ds. zabezpieczeń i działań tak szybko, jak to możliwe, aby zdefiniować następujące elementy:

- Czysty proces udostępniania wszelkich obciążeń w zaległości z wymaganiami dotyczącymi obsługi.
- Zrozumienie wymagań związanych z zarządzaniem operacjami i spójnością zasobów dla różnych różnych poziomów zagrożenia.
- Wszelkie krytyczne znaczenie mogą mieć miejsce w projekcie subskrypcji, hierarchiach grup zarządzania lub wymaganiach dotyczących strefy docelowej.
- Wszelkie wymagania dotyczące nieważności dokumentu, które mogą obejmować konkretne raporty dotyczące ruchu lub użycia, analizy finansowe lub inne narzędzia.

## <a name="next-steps"></a>Następne kroki

Po poprawnym sklasyfikowaniu obciążeń są znacznie łatwiejsze do [dopasowania priorytetów firmy](./business-priorities.md).

> [!div class="nextstepaction"]
> [Uzgadnianie priorytetów biznesowych](./business-priorities.md)
