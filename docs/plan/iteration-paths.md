---
title: Ustanawianie planów wydań i iteracji
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak definiować iteracje i plany wydań, aby ułatwić zarządzanie implementacją.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8aaee4546568301eabbe774cea08c3d5d975bb3e
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092671"
---
# <a name="establish-iterations-and-release-plans"></a>Ustanawianie planów wydań i iteracji

Metody Agile i inne iteracyjne metodologii są oparte na koncepcji iteracji i wydań. W tym artykule opisano przypisanie iteracji i wydań podczas planowania. Te przypisania są widoczne na osi czasu, aby łatwiej tworzyć konwersacje wśród członków zespołu strategii chmurowej. Przypisania są również wyrównane do zadań technicznych w sposób, w jaki zespół wdrażania chmury może zarządzać podczas wdrażania.

## <a name="establish-iterations"></a>Ustanów iteracje

W iteracyjnym podejściu do implementacji technicznej należy zaplanować wysiłki techniczne wokół cyklicznych bloków czasowych. Iteracje mają jeden tydzień na sześć tygodni czasu. Z konsensusu sugeruje, że dwa tygodnie to średni czas trwania iteracji dla większości zespołów wdrożenia chmury. Jednak wybór czasu trwania iteracji zależy od typu nakładu pracy, kosztów administracyjnych i preferencji zespołu.

Aby rozpocząć wyrównywanie wysiłków na osi czasu, zalecamy zdefiniowanie zestawu iteracji, który ostatnie 6 – 12 miesięcy.

## <a name="understand-velocity"></a>Informacje o szybkości

Wyrównywanie wysiłków do iteracji i wydań wymaga poznania prędkości. Szybkość jest ilością pracy, którą można wykonać w każdej iteracji. Podczas wczesnego planowania szybkość jest szacowana. Po kilku iteracjach prędkość stanie się wysoce cennym wskaźnikiem zobowiązań, które zespół może zapewnić z pewnością.

Szybkość można mierzyć w warunkach abstrakcyjnych, takich jak punkty wątku. Możesz również zmierzyć ją w bardziej wymiernych warunkach, takich jak godziny. W przypadku większości platform iteracyjnych zalecamy używanie pomiarów abstrakcyjnych, aby uniknąć wyzwań w precyzji i postrzeganiu. Przykłady w tym artykule przedstawiają prędkość w godzinach dla przebiegu. Ta reprezentacja sprawia, że temat jest bardziej zrozumiały.

**Przykład:** Zespół wdrażania w chmurze z pięcioma osobami zatwierdził dwutygodniowe przebiegi. Zgodnie z obecnymi zobowiązaniami, takimi jak spotkania i pomoc techniczna dla innych procesów, każdy członek zespołu może w sposób ciągły współtworzyć 20 godzin na tydzień, aby uzyskać nakład Dla tego zespołu okresowe oszacowanie prędkości wynosi 100 godzin na przebieg.

## <a name="iteration-planning"></a>Planowanie iteracji

Początkowo planujesz iteracje, oceniając zadania techniczne na podstawie zaległych zaległości. Zespoły wdrażania chmury oceniają nakład pracy potrzebny do wykonania różnych zadań. Te zadania są następnie przypisywane do pierwszej dostępnej iteracji.

Podczas planowania iteracji zespoły wdrażania chmury weryfikują i udoskonalają oszacowania. Są tak, dopóki nie wyrównania wszystkie dostępne szybkości do określonych zadań. Ten proces jest kontynuowany dla każdego priorytetowego obciążenia, dopóki wszystkie zadania nie zostaną wyrównane do prognozowanej iteracji.

W tym procesie zespół sprawdza poprawność zadań przypisanych do następnego przebiegu. Zespół aktualizuje swoje oszacowania na podstawie rozmowy zespołu o każdym zadaniu. Następnie zespół dodaje każde szacowane zadanie do następnego przebiegu, dopóki nie zostanie osiągnięta dostępna szybkość. Na koniec zespół ocenia dodatkowe zadania i dodaje je do następnej iteracji. Zespół wykonuje te czynności do momentu wyczerpania prędkości tej iteracji.

Poprzedni proces jest kontynuowany do momentu przypisania wszystkich zadań do iteracji.

**Przykład:** Zacznijmy od poprzedniego przykładu. Załóżmy, że każda migracja obciążenia wymaga 40 zadań. Załóżmy również, że oszacowano każde zadanie, aby wykonać średnio jedną godzinę. Łączne szacowanie wynosi około 40 godzin na migrację obciążenia. Jeśli te oszacowania pozostają spójne dla wszystkich 10 obciążeń z priorytetyzacją, te obciążenia będą trwać 400 godzin.

Prędkość zdefiniowana w poprzednim przykładzie sugeruje, że migracja pierwszych 10 obciążeń zajmie cztery iteracje, czyli dwa miesiące czasu kalendarzowego. Pierwsza iteracja będzie zawierać 100 zadań, które powodują migrację dwóch obciążeń. W następnej iteracji podobna kolekcja 100 zadań spowoduje migrację trzech obciążeń.

> [!WARNING]
> Powyższa liczba zadań i oszacowań jest używana wyłącznie jako przykład. Zadania techniczne są rzadko zgodne. Nie powinieneś zobaczyć tego przykładu jako odbicia czasu wymaganego do migracji obciążenia.

## <a name="release-planning"></a>Planowanie wydania

W ramach wdrażania w chmurze wersja jest definiowana jako kolekcja elementów dostarczających, które tworzą wystarczającą wartość biznesową, aby uzasadnić ryzyko zakłócenia procesów firmy.

Zwalnianie wszelkich zmian związanych z obciążeniem w środowisku produkcyjnym tworzy pewne zmiany w procesach biznesowych. W idealnym przypadku te zmiany są bezproblemowe, a firma widzi wartość zmian bez znaczących przerw w działaniu usługi. Jednak ryzyko zakłócenia działania firmy jest obecne w przypadku zmiany i nie powinno być podejmowane w sposób jasny.

Aby upewnić się, że zmiana jest uzasadniona przez potencjalny zwrot, zespół strategii chmury powinien brać udział w planowaniu wersji. Gdy zadania są wyrównane do przebiegów, zespół może określić przybliżoną oś czasu, gdy każde obciążenie będzie gotowe do wydania produkcyjnego. Zespół ds. strategii chmury przeanalizuje chronometraż każdej wersji. Następnie zespół zidentyfikuje punkt przegięcia między ryzykiem a wartością biznesową.

**Przykład:** W poprzednim przykładzie zespół strategii chmury sprawdził plan iteracji. Przegląd zidentyfikowano dwa punkty wydań. Podczas drugiej iteracji do migracji będzie gotowych łącznie pięć obciążeń. Te pięć obciążeń zapewniają znaczącą wartość biznesową i wyzwalają pierwsze wydanie. Następne wydanie będzie miało dwie iteracje później, gdy następne pięć obciążeń jest gotowych do wydania.

## <a name="assign-iteration-paths-and-tags"></a>Przypisywanie ścieżek iteracji i tagów

W przypadku klientów, którzy zarządzają planami wdrażania chmury w usłudze Azure DevOps, poprzednie procesy są odzwierciedlane przez przypisanie ścieżki iteracji do każdego zadania i scenariusza użytkownika. Zalecamy również znakowanie każdego obciążenia z określoną wersją. Takie oznakowanie i podawanie strumieniowym automatycznego wypełniania raportów osi czasu.

## <a name="next-steps"></a>Następne kroki

[Szacuj osie czasu](./timelines.md) , aby prawidłowo komunikować oczekiwania.

> [!div class="nextstepaction"]
> [Szacowanie osi czasu](./timelines.md)
