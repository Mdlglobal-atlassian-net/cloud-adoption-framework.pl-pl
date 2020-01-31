---
title: Jaką rolę odgrywa replikacja i synchronizacja w procesie migracji?
description: Proces migracji do chmury, który koncentruje się na zadaniach migrowania obciążeń do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6b37cea7b912cb4d65f9b1b119787e96b2f698d6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802025"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-role-does-replication-play-in-the-migration-process"></a>Jaką rolę odgrywa replikacja w procesie migracji?

Lokalne centra danych są wypełnione zasobami fizycznymi, takimi jak serwery, urządzenia i urządzenia sieciowe. Jednak każdy serwer jest tylko powłoką fizyczną. Rzeczywista wartość pochodzi z kodu binarnego działającego na serwerze. Centra danych mają za zadanie obsługiwać aplikacje i dane. Stanowią one podstawowy kod binarny do zmigrowania. Istnieją również inne zasoby cyfrowe oraz źródła binarne służące do obsługi tych aplikacji i magazynów danych, takie jak systemy operacyjne, trasy sieciowe, pliki i protokoły zabezpieczeń.

Replikacja jest głównym mechanizmem migracji. Jest to proces kopiowania wersji z określonego momentu różnych plików binarnych. Migawki binarne są następnie kopiowane na nową platformę i wdrażane na nowym sprzęcie w ramach procesu nazywanego *rozmieszczaniem*. Po poprawnym wykonaniu replikacji rozmieszczona kopia pliku binarnego powinna zachowywać się identycznie jak oryginalny plik binarny na starym sprzęcie. Jednak taka migawka pliku binarnego staje się od razu nieaktualna i niezgodna z oryginalnym źródłem. Aby zachować zgodność między nowym i starym plikiem binarnym, proces *synchronizacji* stale aktualizuje kopię przechowywaną na nowej platformie. Synchronizacja jest wykonywana do momentu, gdy poziom zasobu zostanie podwyższony w celu wyrównania go z wybranym modelem promocji. W tym momencie synchronizacja jest przerywana.

## <a name="required-prerequisites-to-replication"></a>Wymagania wstępne dotyczące replikacji

Przed replikacją należy przygotować *nową platformę* i sprzęt do odbierania kopii binarnych. W artykule dotyczącym [wymagań wstępnych](../prerequisites/index.md) przedstawiono minimalne wymagania środowiska, które ułatwiają tworzenie bezpiecznej, niezawodnej i wydajnej platformy do odbierania replik binarnych.

*Źródłowe pliki binarne* muszą być również przygotowane do replikacji i synchronizacji. W artykułach dotyczących oceny, architektury i korygowania opisano działania niezbędne do zapewnienia gotowości źródłowych danych binarnych do replikacji i synchronizacji.

Aby móc wykonywać procesy replikacji i synchronizacji oraz zarządzać nimi, konieczne jest zaimplementowanie *łańcucha narzędzi* do zapewnienia zgodności z nową platformą i źródłowymi plikami binarnymi. W artykule dotyczącym [opcji replikacji](./replicate-options.md) opisano różne narzędzia, które mogą pomóc podczas migracji na platformę Azure.

## <a name="replication-risks---physics-of-replication"></a>Zagrożenia replikacji — fizyka replikacji

Podczas planowania i wykonywania replikacji dowolnego źródła danych binarnych do nowego miejsca docelowego należy pamiętać o istnieniu kilku podstawowych praw, których trzeba przestrzegać.

- **Szybkość światła.** Podczas przenoszenia dużych ilości danych światłowód jest nadal najszybszą opcją. Niestety, za pomocą tych kabli można przenosić dane z szybkością tylko dwóch trzecich szybkości światła. Oznacza to, że nie ma metody zapewniającej natychmiastową lub nieograniczoną replikację danych.
- **Szybkość potoku WAN.** Większa niż szybkość przenoszenia danych to przepustowość pasma, która definiuje ilość danych na sekundę, które mogą być przenoszone przez istniejącą sieć WAN do docelowego centrum danych.
- **Szybkość rozbudowy sieci WAN.** Jeśli pozwala na to budżet, do rozwiązania WAN firmy można dodać dodatkową przepustowość. Może jednak upłynąć kilka tygodni lub nawet miesięcy, zanim dodatkowe połączenia światłowodowe zostaną zainstalowane, zainicjowane i zintegrowane.
- **Szybkość dysków.** Jeśli dane mogłyby być szybciej przenoszone i nie byłoby limitu przepustowości między źródłowymi plikami binarnymi i ich miejscem docelowym, ograniczeniem byłyby prawa fizyki. Dane mogą być replikowane tylko tak szybko, jak to możliwe, ponieważ mogą być odczytywane z dysków źródłowych. Odczytanie poszczególnych jedynek i zer z każdego obracającego się dysku w centrum danych zabiera nieco czasu.
- **Szybkość obliczeń ludzkich.** Dyski i światło zapewniają większą szybkość niż szybkość podejmowania decyzji przez ludzi. Czas ten wydłuża się jeszcze, gdy osoby muszą współpracować ze sobą w grupie i podejmować wspólne decyzje. Replikacja nigdy nie przezwycięży opóźnień związanych z ludzkimi procesami analitycznymi.

Wszystkie te prawa fizyki wprowadzają następujące zagrożenia, które zwykle mają wpływ na plany migracji:

- **Czas replikacji.** Zaawansowane narzędzia do replikacji nie mogą przezwyciężyć podstawowych praw fizyki &mdash; replikacja wymaga czasu i przepustowości. Plany powinny uwzględniać realistyczne osie czasu odzwierciedlające ilość czasu potrzebną do replikowania plików binarnych. *Całkowita dostępna przepustowość migracji* to wielkość przepustowości z ograniczeniami, mierzona w megabitach na sekundę (Mb/s) lub gigabitach na sekundę (Gb/s), która nie jest używana na inne potrzeby biznesowe o wyższym priorytecie. *Łączny magazyn migracji* to całkowite miejsce na dysku (w gigabajtach lub terabajtach) wymagane do przechowywania migawki wszystkich zasobów do zmigrowania. Początkowy szacunek czasu można obliczyć, dzieląc *łączny magazyn migracji* przez *całkowitą dostępną przepustowość migracji*. Zwróć uwagę na konwersję jednostek z bitów na bajty. W sekcji „Skumulowany efekt dryfowania dysku” opisano dokładniejszą metodę obliczania czasu.
- **Skumulowany efekt dryfowania dysku.** Źródłowe i docelowe pliki binarne muszą pozostawać zsynchronizowane od momentu replikacji do czasu podwyższenia poziomu zasobu do środowiska produkcyjnego. *Dryf* plików binarnych zużywa dodatkową przepustowość, ponieważ wszystkie zmiany w danych binarnych muszą być cyklicznie replikowane. Podczas synchronizacji cały dryf danych binarnych musi zostać uwzględniony w obliczeniach łącznego magazynu migracji. Wydłużanie czasu podwyższania poziomu zasobu do środowiska produkcyjnego powoduje wystąpienia bardziej skumulowanego efektu dryfu. Zwiększanie liczby synchronizowanych zasobów powoduje zwiększenie zapotrzebowania na przepustowość. Każdy zasób przechowywany w stanie synchronizacji powoduje utratę części całkowitej dostępnej przepustowości migracji.
- **Czas na zmianę biznesową.** Jak wspomniano w poprzedniej sekcji „Skumulowany efekt dryfowania dysku”, czas synchronizacji ma skumulowany negatywny wpływ na szybkość migracji. Ustawienie priorytetów na liście prac migracji i zaawansowane przygotowania do [planu zmian w firmie](../optimize/business-change-plan.md) mają kluczowe znaczenie dla szybkości migracji. Najważniejszym testem zgodności działań biznesowych i technicznych podczas migracji jest tempo podwyższania poziomu. Szybsze podwyższenie poziomu zasobu do środowiska produkcyjnego zmniejszy wpływ dryfowania dysku na przepustowość, a tym samym większy przepustowość, którą będzie można przydzielić do replikacji kolejnego obciążenia.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu replikacji można rozpocząć [działania dotyczące przemieszczania](./stage.md).

> [!div class="nextstepaction"]
> [Działania dotyczące przemieszczania podczas migracji](./stage.md)
