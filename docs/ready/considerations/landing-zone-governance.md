---
title: Ulepszanie ładu strefy docelowej
description: Ulepszanie ładu strefy docelowej
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: fd500f00ecd021a1d05904c675d63a64e8b6764b
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756536"
---
# <a name="improve-landing-zone-governance"></a>Ulepszanie ładu strefy docelowej

Zarządzanie strefami wyładunkowymi jest najmniejszą jednostką ogólnego zarządzania. Ustanowienie solidnej podstawy zarządzania w ramach pierwszych kilku stref wypełniania spowoduje zredukowanie ilości operacji refaktoryzacji wymaganej później w cyklu życia. Poprawa nadzoru strefy wyładunkowej integruje kontrolę kosztów, ustanowi podstawowe narzędzia umożliwiające skalowanie i ułatwi zespołowi nadzoru chmurowego dostarczenie pięciu dyscyplin nadzoru chmurowego.

## <a name="landing-zone-governance-best-practices"></a>Najlepsze praktyki dotyczące zarządzania strefami wyładunkowymi

- **Wstępne zarządzanie wyładunkiem:** Artykuł dotyczący ustanawiania [początkowego ładu](../../govern/guides/complex/index.md) programu ułatwia dodawanie początkowych narzędzi nadzoru do pierwszych kilku stref. Te praktyki ułatwiają skalowanie wdrażania i zarządzania, a także wdrażanie kosztów związanych z zarządzaniem kosztem. Ta metoda rozpoczyna się od: organizacja zasobów, definicje zasad, role RBAC i definicje planu.
- ** [Wzorce nazewnictwa i znakowania](../azure-best-practices/naming-and-tagging.md):** Zapewnij spójność nazw i tagowania, które stanowią podstawowe dane do ustanawiania praktyk związanych z zarządzaniem dźwiękiem.
- ** [Śledź koszty w ramach obciążeń](../azure-best-practices/track-costs.md):** Rozpocznij śledzenie kosztów w pierwszej strefie docelowej. Oceń, w jaki sposób będzie stosowana spójność wielu obciążeń i ról.
- ** [Skaluj z wieloma subskrypcjami](../azure-best-practices/scale-subscriptions.md):** Oceń, w jaki sposób Ta strefa docelowa i inne strefy wyładunkowe będą skalowane, ponieważ wymaga to wielu subskrypcji.
- ** [Organizuj subskrypcje](../azure-best-practices/organize-subscriptions.md):** Zapoznaj się z tematem organizowania wielu subskrypcji i zarządzania nimi.

## <a name="four-steps-to-improve-overall-governance"></a>Cztery kroki w celu usprawnienia ogólnego zarządzania

[Metodologia rządząca](../../govern/index.md) zapewnia ogólne wskazówki dotyczące tworzenia zasad, procesów i dyscyplin ładu. Stosujemy podstawową strukturę tej metodologii oraz następujące kroki z tej metodologii w celu usprawnienia nadzoru i zarządzania strefą docelową we wszystkich strefach wyładunkowych.

1. [Zapoznaj się z metodologią](../../govern/methodology.md): Poznaj podstawową metodologię do obsługi projektowania ładu stanu końcowego.
2. [Test porównawczy](../../govern/benchmark.md): Oceń bieżący i przyszły stan w celu ustalenia wizji i podjęcia odpowiednich działań.
3. [Początkowe zarządzanie podstawą](../../govern/initial-foundation.md): mały, łatwo zaimplementowany zestaw narzędzi ładu, aby ustanowić początkową podstawę dla wszystkich stref wyładunkowych.
4. [Ulepszanie ładu](../../govern/foundation-improvements.md): można iteracyjnie dodać kontrolki ładu, aby wzmocnić wszystkie Zarządzanie strefami przeładunkowymi.

## <a name="next-steps"></a>Następne kroki

Wdrażanie w chmurze będzie nadal rozwijane z każdą Wave lub wydaniem nowych obciążeń. Aby zachować te wymagania, zaleca się, aby zespoły platformy chmury okresowo [przeglądali dodatkowe najlepsze rozwiązania w zakresie strefy docelowej](../azure-best-practices/index.md).

> [!div class="nextstepaction"]
> [Zapoznaj się z dodatkowymi najlepszymi rozwiązaniami strefy docelowej](../azure-best-practices/index.md)
