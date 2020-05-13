---
title: Działania dotyczące przemieszczania podczas migracji
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć działania etapowe i skojarzone elementy dostarczane podczas migracji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 40a0899a10e242e98ed16aa2bcbfdbd55f65afc2
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216082"
---
# <a name="understand-staging-activities-during-a-migration"></a>Informacje dotyczące przemieszczania podczas migracji

Zgodnie z opisem w artykule dotyczącym modeli promocji _przemieszczanie_ to proces, podczas którego zasoby zostały zmigrowane do chmury. Nie są one jednak jeszcze gotowe do promowania do środowiska produkcyjnego. Jest to często ostatni krok w procesie migracji. Po przemieszczeniu obciążenie jest zarządzane przez zespoły ds. operacji informatycznych lub operacji w chmurze w celu przygotowania ich do użycia w środowisku produkcyjnym.

## <a name="deliverables"></a>Rezultaty

Przemieszczanie zasoby mogą nie być gotowe do użycia w środowisku produkcyjnym. Istnieje kilka testów gotowości do użycia w środowisku produkcyjnym, które powinny zostać sfinalizowane przed ukończeniem tego etapu. Poniżej znajduje się rezultatów prac często kojarzonych z ukończeniem przemieszczania zasobów.

- **Testy automatyczne.** Przed zakończeniem procesu przemieszczania należy uruchomić wszystkie dostępne testy automatyczne umożliwiające weryfikację wydajności obciążeń. Po zakończeniu przemieszczania zasobu jego synchronizacja z oryginalnym systemem źródłowym zostanie przerwana. W związku z tym trudniejsze jest ponowne wdrożenie replikowanych zasobów po przemieszczeniu zasobów w celu optymalizacji.
- **Dokumentacja dotycząca migracji.** Większość narzędzi do migracji może wygenerować zautomatyzowany raport dotyczący migrowanych zasobów. Przed zakończeniem działania przemieszczania wszystkie zmigrowane zasoby powinny zostać udokumentowane w celu zachowania przejrzystości.
- **Dokumentacja dotycząca konfiguracji.** Wszelkie zmiany wprowadzone w zasobie (podczas korygowania, replikacji lub przygotowania) powinny być udokumentowane pod kątem gotowości operacyjnej.
- **Dokumentacja dotycząca listy prac.** Lista prac dotycząca migracji powinna zostać zaktualizowana w celu odzwierciedlenia przemieszczonych obciążeń i zasobów.

## <a name="next-steps"></a>Następne kroki

Po przetestowaniu i udokumentowaniu przemieszczonych zasobów możesz przejść [do działań związanych z optymalizacją](../optimize/index.md).

> [!div class="nextstepaction"]
> [Optymalizacja migrowanych obciążeń](../optimize/index.md)
