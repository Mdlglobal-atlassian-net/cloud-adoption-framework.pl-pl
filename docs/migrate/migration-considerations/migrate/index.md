---
title: Wykonywanie migracji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wykonywanie migracji
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 21520edecc7ba874713561672cd0bd38aa96c0a2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818237"
---
# <a name="execute-a-migration"></a>Wykonywanie migracji

Po dokonaniu oceny obciążenia można przeprowadzić jego migrację do chmury. W tej serii artykułów opisano różne działania, które mogą być wykonywane podczas migracji.

## <a name="objective"></a>Cel

Celem migracji jest zmigrowanie pojedynczego obciążenia do chmury.

## <a name="definition-of-done"></a>Definicja *gotowości*

Faza migracji jest uznawana za ukończoną, gdy obciążenie zostanie przemieszczone i przygotowane do testowania w chmurze. Dotyczy to również wszystkich zależnych zasobów, bez których obciążenie nie mogłoby działać. W procesie optymalizacji obciążenie jest przygotowywane do użycia w środowisku produkcyjnym.

Ta definicja *gotowości* może się różnić w zależności od stosowanych procesów testowania i wydawania. W następnym artykule z tej serii opisano [podejmowanie decyzji co do modelu podwyższania poziomu](./promotion-models.md). Może on pomóc w zrozumieniu, kiedy będzie najlepszy moment do podwyższenia poziomu zmigrowanego obciążenia do środowiska produkcyjnego.

## <a name="accountability-during-migration"></a>Odpowiedzialność podczas migracji

Za cały proces migracji jest odpowiedzialny zespół ds. wdrażania w chmurze. Jednak członkowie zespołu ds. strategii w chmurze mają również kilka obowiązków, które opisano w poniższej sekcji.

## <a name="responsibilities-during-migration"></a>Obowiązki podczas migracji

Oprócz odpowiedzialności wysokiego poziomu istnieją również akcje, za które powinny być bezpośrednio odpowiedzialne poszczególne osoby lub grupy. Poniżej przedstawiono kilka działań, za które odpowiedzialność powinny ponosić odpowiednie osoby:

- **Korygowanie.** Rozwiąż wszelkie problemy ze zgodnością, które uniemożliwiają zmigrowanie obciążenia do chmury.
  - Jak przedstawiono w artykule wstępnym dotyczącym [technicznej złożoności i zarządzania zmianami](../prerequisites/technical-complexity.md), decyzja powinna zostać podjęta z wyprzedzeniem, aby móc określić sposób wykonania tego działania. W szczególności należy odpowiedzieć sobie na pytanie, czy korygowanie zostanie ukończone przez zespół ds. wdrażania w chmurze podczas tego samego przebiegu co rzeczywista migracja. Alternatywnie fala lub model fabryki może zostać użyty do zakończenia korygowania w oddzielnej iteracji. Jeśli członkowie zespołu nie potrafią odpowiedzieć na to podstawowe pytanie dotyczące procesu, zasadne może być powrócenie do sekcji [wymagań wstępnych](../prerequisites/index.md).
- **Replikacja.** Utwórz kopie poszczególnych zasobów w chmurze, aby zsynchronizować maszyny wirtualne, dane i aplikacje z zasobami w chmurze.
  - W celu zakończenia tego działania mogą być wymagane różne narzędzia w zależności od modelu podwyższania poziomu.
- **Przemieszczanie.** Po zreplikowaniu i zweryfikowaniu wszystkich zasobów obciążenie można przemieścić na potrzeby testowania biznesowego i wykonywania planu zmian biznesowych.

## <a name="next-steps"></a>Następne kroki

Po zrozumieniu ogólnych procesów migracji możesz [zdecydować się na wybór modelu podwyższania poziomu](./promotion-models.md).

> [!div class="nextstepaction"]
> [Wybierz model podwyższania poziomu](./promotion-models.md)
