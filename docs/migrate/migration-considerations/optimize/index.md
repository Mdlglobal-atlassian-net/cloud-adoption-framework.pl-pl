---
title: Optymalizacja migrowanych obciążeń
description: Użyj struktury wdrażania chmury dla platformy Azure, aby przygotować zmigrowane obciążenie i elementy zawartości do podwyższenia do poziomu produkcyjnego.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0d83ccc83397153619bc7ca99881c6a2775ab1a3
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120689"
---
# <a name="release-workloads"></a>Wydanie obciążeń

Po wdrożeniu w chmurze kolekcji obciążeń i ich zasobów pomocniczych należy ją przygotować przed wydaniem. W tej fazie procesu migracji kolekcja obciążeń jest testowana pod kątem obciążenia i testowana w firmie. Następnie obciążenia są optymalizowane i dokumentowane. Po przejrzeniu i zatwierdzeniu wdrożeń obciążeń przez firmę i zespoły IT te obciążenia mogą zostać wydane lub przekazane do zespołów ds. ładu, zabezpieczeń i operacyjnych na potrzeby bieżących operacji.

Celem „wydania obciążeń” jest przygotowanie migrowanych obciążeń do podniesienia poziomu w celu użycia w środowisku produkcyjnym.

## <a name="definition-of-done"></a>Definicja *gotowości*

Proces optymalizacji uznaje się za zakończony po poprawnym skonfigurowaniu obciążenia, dopasowaniu jego rozmiaru i wdrożeniu w środowisku produkcyjnym.

## <a name="accountability-during-optimization"></a>Odpowiedzialność podczas optymalizacji

Za cały proces optymalizacji jest odpowiedzialny zespół ds. wdrażania w chmurze. Jednak członkowie zespołu ds. strategii w chmurze, zespołu ds. operacji w chmurze i zespołu ds. utrzymania ładu w chmurze powinni również być odpowiedzialni za działania podejmowane w ramach tego procesu.

## <a name="responsibilities-during-optimization"></a>Obowiązki podczas optymalizacji

Oprócz odpowiedzialności wysokiego poziomu istnieją również akcje, za które powinny być bezpośrednio odpowiedzialne poszczególne osoby lub grupy. Poniżej przedstawiono kilka działań, za które odpowiedzialność powinny ponosić odpowiednie osoby:

- **Testowanie biznesowe.** Rozwiąż wszelkie problemy ze zgodnością, które uniemożliwiają ukończenie migracji obciążenia do chmury.
  - Zaawansowani użytkownicy z firmy powinni aktywnie uczestniczyć w testowaniu zmigrowanych obciążeń. W zależności od stopnia optymalizacji może być wymagane wykonanie wielu cykli testowania.
- **Plan zmian biznesowych.** Opracowanie planu wdrożenia użytkowników, zmian w procesach biznesowych i modyfikacji biznesowych wskaźników KPI lub metryk szkolenia jako wyniku nakładu pracy migracji.
- **Test porównawczy i optymalizacja.** Badanie testowania biznesowego i testowania automatycznego w celu wykonania testów porównawczych wydajności. W zależności od sposobu użycia zespół ds. wdrażania w chmurze dopasowuje rozmiar wdrożonych zasobów, aby zrównoważyć koszt i wydajność względem oczekiwanych wymagań środowiska produkcyjnego.
- **Gotowość do użytku produkcyjnego.** Przygotuj obciążenie i środowisko do obsługi przyszłych zastosowań produkcyjnych.
- **Podwyższanie poziomu.** Przekieruj ruch produkcyjny do zmigrowanego i zoptymalizowanego obciążenia. To działanie reprezentuje ukończenie cyklu wydawania.

Oprócz podstawowych działań istnieje kilka działań równoległych, które wymagają określonych przydziałów i planów wykonania:

- **Likwidowanie.** Ogólnie rzecz biorąc, oszczędności można uzyskać z migracji, gdy poprzednie zasoby produkcyjne zostaną zlikwidowane i prawidłowo usunięte.
- **Retrospektywa.** Każde wydanie tworzy szansę dla uczenia głębokiego i rozwijania możliwości. Po ukończeniu każdego cyklu wydawania zespół ds. wdrażania w chmurze powinien ocenić procesy wykonywane podczas migrowania w celu zidentyfikowania ulepszeń.

## <a name="next-steps"></a>Następne kroki

Po ogólnym zrozumieniu procesu optymalizacji możesz rozpocząć ten proces przez [opracowanie planu zmian biznesowych dla wybranego obciążenia](./business-change-plan.md).

> [!div class="nextstepaction"]
> [Plan zmian biznesowych](./business-change-plan.md)
