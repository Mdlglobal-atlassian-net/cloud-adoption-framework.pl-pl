---
title: Walidacja założeń oceny przed migracją
description: Użyj struktury wdrażania chmury dla platformy Azure, aby dowiedzieć się, jak zweryfikować założenia oceny przed rozpoczęciem migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: cc095a1751e945ca18763757582a6cd27b65d72a
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "81119767"
---
# <a name="assess-workloads-and-validate-assumptions-before-migration"></a>Ocena obciążeń i weryfikacja założeń przed migracją

Wiele z istniejących obciążeń idealnie nadaje się do migracji do chmury, ale nie każdy zasób jest zgodny z platformami chmury i nie dla wszystkich obciążeń jest korzystny hosting w chmurze. [Planowanie infrastruktury cyfrowej](../../../digital-estate/index.md) umożliwia utworzenie ogólnej [listy prac związanych z migracją](../prerequisites/technical-complexity.md#migration-backlog-aligning-business-priorities-and-timing) dla potencjalnych obciążeń do migracji. Jednak jest to planowanie wysokiego poziomu. Opiera się ono na założeniach przyjmowanych przez zespół ds. strategii w chmurze bez dogłębnej analizy zagadnień technicznych.

W efekcie przed migracją obciążenia do chmury krytyczne znaczenie ma ocena poszczególnych zasobów powiązanych z tym obciążeniem pod kątem możliwości migracji. Podczas tej oceny zespół ds. wdrażania chmury powinien ocenić zgodność pod względem technicznym, wymaganej architektury, oczekiwań dotyczących wydajności/rozmiaru oraz zależności, aby upewnić się, że zmigrowane obciążenie można efektywnie wdrożyć w chmurze.

Proces *oceny* to pierwsze z czterech działań przyrostowych mających miejsce w ramach iteracji. Jak przedstawiono w artykule wstępnym dotyczącym [złożoności technicznej i zarządzania zmianami](../prerequisites/technical-complexity.md), decyzja powinna zostać podjęta z wyprzedzeniem, aby móc określić sposób wykonania tej fazy. W szczególności należy odpowiedzieć sobie na pytanie, czy ocena zostanie wykonana przez zespół ds. wdrażania w chmurze podczas tego samego przebiegu co rzeczywista migracja. Alternatywnie, czy fala lub model fabryki może zostać użyty do wykonania ocen w oddzielnej iteracji. Jeśli członkowie zespołu nie potrafią odpowiedzieć na to podstawowe pytanie dotyczące procesu, warto ponownie zapoznać się z sekcją [wymagań wstępnych](../prerequisites/index.md).

## <a name="objective"></a>Cel

Ocena kandydatów do migracji obejmująca ocenę obciążenia, powiązanych zasobów i zależności przed migracją.

## <a name="definition-of-done"></a>Definicja *gotowości*

Ten proces można uznać za ukończony, gdy uzyskano następujące informacje o kandydacie do migracji:

- Zdefiniowano ścieżkę przejścia ze środowiska lokalnego do chmury, w tym podjęto decyzję dotyczącą podejścia do podwyższania poziomu produkcji.
- Uzyskano wszystkie wymagane zatwierdzenia i szacowane koszty oraz dokonano wymaganych zmian lub przeprowadzono procesy weryfikacji, aby umożliwić zespołowi ds. wdrażania chmury wykonanie migracji.

## <a name="accountability-during-assessment"></a>Odpowiedzialność podczas oceny

Za cały proces oceny jest odpowiedzialny zespół ds. wdrażania w chmurze. Jednak członkowie zespołu ds. strategii w chmurze mają również kilka obowiązków, które wymieniono w poniższej sekcji.

## <a name="responsibilities-during-assessment"></a>Obowiązki podczas oceny

Oprócz odpowiedzialności wysokiego poziomu istnieją również akcje, za które powinny być bezpośrednio odpowiedzialne poszczególne osoby lub grupy. Poniżej przedstawiono kilka działań, za które odpowiedzialność powinny ponosić odpowiednie osoby:

- **Priorytet biznesowy** Zespół rozumie cel migracji tego obciążenia, w tym zamierzony wpływ na działalność.
  - Członek zespołu ds. wdrażania w chmurze powinien ponosić ostateczną odpowiedzialność za to działanie pod kierunkiem zespołu ds. wdrażania w chmurze.
- **Uzgodnienie stanowiska osób biorących udział w projekcie** Zespół uzgadnia oczekiwania i priorytety z wewnętrznymi uczestnikami projektu, identyfikując kryteria sukcesu migracji. Jakie są kryteria sukcesu po migracji?
- **Uściślona racjonalizacja.** Oceń początkowe założenia dotyczące racjonalizacji. Czy w celu przeprowadzenia migracji danego obciążenia ma zostać zastosowane inne [podejście do racjonalizacji](../../../digital-estate/rationalize.md)?
- **Decyzje dotyczące modernizacji.** Bez względu na decyzję o racjonalizacji, czy różne zasoby w obciążeniu mają być modernizowane, aby korzystać z rozwiązań PaaS?
- **Koszt** Koszt docelowej architektury został oszacowany i skorygowano całkowity budżet.
- **Obsługa techniczna migracji** Zespół zdecydował, w jaki sposób zostaną wykonane prace techniczne związane z migracją, w tym podjął decyzje dotyczące pomocy technicznej partnera lub firmy Microsoft.
- **Ocena** Obciążenie jest oceniane pod kątem zgodności i zależności.
  - To działanie powinno zostać przypisane specjaliście w tej dziedzinie, który zna architekturę i operacje dotyczące kandydującego obciążenia.
- **Tworzenie architektury** Zespół uzgodnił ostateczny stan architektury migrowanego obciążenia.
- **Narzędzia migracji.** W zależności od podejścia do modernizacji i architektury w celu automatyzowania migracji można użyć różnych narzędzi do migracji. Czy, na podstawie proponowanej architektury, ta migracja będzie korzystać z najlepszych [narzędzi do migracji](../../../decision-guides/migrate-decision-guide/index.md)?
- **Uzgodnienie listy prac** Zespół ds. wdrażania w chmurze sprawdza wymagania i zatwierdza migrację kandydującego obciążenia. Po zatwierdzenia lista prac wydania i lista prac iteracji są odpowiednio aktualizowane.
- **Struktura podziału pracy lub harmonogram prac** Zespół ustala harmonogram kamieni milowych, identyfikując cele podczas planowania, wdrażania i przeglądu procesów.
- **Ostateczne zatwierdzenie** Wszystkie wymagane osoby zatwierdzające sprawdziły plan i zatwierdziły podejście dotyczące migracji zasobu.
  - Aby uniknąć niespodzianek w dalszej części procesu, co najmniej jeden przedstawiciel firmy powinien być zaangażowany w proces zatwierdzania.

> [!CAUTION]
> Ta pełna lista obowiązków i akcji umożliwia obsługę dużych i złożonych migracji obejmujących wiele ról z różnymi poziomami odpowiedzialności, które wymagają szczegółowego procesu zatwierdzania. Mniejsze i prostsze migracje nie muszą wymagać wszystkich ról i akcji opisanych w tym miejscu. Aby określić, które z tych działań zwiększają wartość, a które są niepotrzebne, zespół ds. wdrażania chmury i zespół ds. strategii w chmurze powinny zastosować ten pełny proces w ramach pierwszej migracji obciążenia. Po weryfikacji i przetestowaniu obciążenia zespół może ocenić ten proces i wybrać akcje, które mają być stosowane w przyszłości.

## <a name="next-steps"></a>Następne kroki

Po uzyskaniu ogólnej wiedzy dotyczącej procesu oceny można rozpocząć proces [klasyfikowania obciążeń](./classify.md).

> [!div class="nextstepaction"]
> [Klasyfikowanie obciążeń](./classify.md)
