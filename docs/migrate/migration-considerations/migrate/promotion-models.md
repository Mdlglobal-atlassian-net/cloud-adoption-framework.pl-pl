---
title: Typy modeli promocji
description: Poznaj trzy popularne modele promocji używane podczas migracji do chmury oraz sposób, w jaki wybór modelu wpływa na działania widoczne w ramach migracji i optymalizacji procesów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 105c25258fba28fe61cc127e1f1e602c0c822202
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216133"
---
# <a name="promotion-models-single-step-staged-or-flight"></a>Modele promocji: jeden etap, etapowy lub samolot

Migracja obciążenia jest często postrzegana jako pojedyncze działanie. W rzeczywistości jest to zbiór drobniejszych działań, które ułatwiają przenoszenie zasobów cyfrowych do chmury. Jednym z ostatnich działań w ramach migracji jest podwyższenie poziomu zasobu do użycia produkcyjnego. Podwyższenie poziomu to moment, w którym system produkcyjny zmienia się dla użytkowników końcowych. Często jest to proste zadanie porównywalne ze zmianą routingu sieci polegające na przekierowaniu użytkowników końcowych do nowego zasobu produkcyjnego. Podwyższenie poziomu to również moment, w którym operacje IT lub operacje w chmurze zmieniają fokus procesów zarządzania operacyjnego z poprzedniego systemu produkcyjnego do nowych systemów produkcyjnych.

Istnieje kilka modeli podwyższania poziomu. W tym artykule opisano trzy modele najczęściej stosowane podczas migracji do chmury. Wybór modelu podwyższania poziomu powoduje zmianę działań obserwowanych w ramach procesów migracji i optymalizacji. W związku z tym model podwyższania poziomu powinien zostać ustalony na wczesnym etapie procesu wydawania.

## <a name="impact-of-promotion-model-on-migrate-and-optimize-activities"></a>Wpływ modelu podwyższania poziomu na działania migracji i optymalizacji

W każdym z następujących modeli podwyższania poziomu wybrane narzędzie migracji replikuje i przygotowuje zasoby, które składają się na obciążenie. Po przygotowaniu każdy model traktuje zasób nieco inaczej.

- **Promocja w jednym kroku.** W modelu podwyższania poziomu _w pojedynczym kroku_ proces przygotowywania jest wykonywany dwa razy. Po przygotowaniu wszystkich zasobów ruch użytkowników końcowych jest przekierowywany, a środowisko przejściowe staje się środowiskiem produkcyjnym. W takim przypadku podwyższanie poziomu jest częścią procesu migracji. Jest to najszybszy model migracji. Jednak takie podejście utrudnia integrację niezawodnych działań związanych z testowaniem i optymalizacją. Ponadto ten typ modelu zakłada, że zespół migracji ma dostęp do środowiska przejściowego i produkcyjnego, co narusza Rozdzielenie obowiązków w niektórych środowiskach.
  > [!NOTE]
  >W spisie treści tej witryny działanie podwyższania poziomu jest wymienione jako część procesu optymalizacji. W modelu pojedynczego kroku podwyższenie poziomu następuje podczas migracji. W związku z tym, w przypadku korzystania z tego modelu, należy odpowiednio zaktualizować role i obowiązki.
- **Przejściowy.** W _przejściowym_ modelu podwyższania poziomu obciążenie jest uznawane za zmigrowane po jego przygotowaniu, ale kiedy jego poziom nie został jeszcze podwyższony. Przed podwyższeniem poziomu zmigrowane obciążenie przechodzi serię testów wydajności, testów biznesowych i zmian optymalizacji. Jego poziom jest podwyższany dopiero później zgodnie z planem testu biznesowego. Takie podejście zwiększa równowagę między kosztami i wydajnością, a jednocześnie ułatwia weryfikację obciążenia pod kątem biznesowym.
- **Pakiet testowy.** Model podwyższania poziomu z _pakietem testowym_ łączy cechy modelu pojedynczego kroku i przejściowego. W modelu z pakietem testowym zasoby składające się na obciążenie są traktowane jako zasoby produkcyjne po umieszczeniu ich w środowisku przejściowym. Ruch produkcyjny jest kierowany do tego obciążenia po skróconym okresie intensywnych testów automatycznych. Jest to jednak tylko podzestaw ruchu. Ten ruch można traktować jako pierwszy pakiet testowy środowiska produkcyjnego. Jeśli z perspektywy funkcjonalnej i wydajnościowej obciążenie spełnia wymagania, migrowany jest dodatkowy ruch. Po przeniesieniu całego ruchu produkcyjnego do nowych zasobów podwyższenie poziomu obciążenia jest uznawane za zakończone.

Wybrany model podwyższania poziomu ma wpływ na kolejność działań, które powinny zostać wykonane. Ma on również wpływ na role i obowiązki członków zespołu wdrożeniowego ds. chmury. Wybrany model może mieć nawet wpływ na kompozycję przebiegu lub wielu przebiegów.

## <a name="single-step-promotion"></a>Podwyższanie poziomu w pojedynczym kroku

W tym modelu replikowanie, przygotowywanie i podwyższanie poziomu zasobów odbywa się przy użyciu narzędzi do automatyzacji migracji. Zasoby są replikowane do zawartego środowiska przejściowego kontrolowanego przez narzędzie do migracji. Po zreplikowaniu wszystkich zasobów narzędzie może w jednym kroku wykonać zautomatyzowany proces podwyższania poziomu zasobów do wybranej subskrypcji. W środowisku przejściowym narzędzie kontynuuje replikację zasobu, co minimalizuje utratę danych między tymi dwoma środowiskami. Po podwyższeniu poziomu zasobu połączenie między systemem źródłowym i zreplikowanym jest przerywane. W tym podejściu, jeśli w systemie źródłowym wystąpią dodatkowe zmiany, zostaną one utracone.

**Formaty.** Korzyści wynikające z tego podejścia są następujące:

- W tym modelu wprowadzana jest mniejsza liczba zmian w systemach docelowych.
- Ciągła replikacja minimalizuje utratę danych.
- Jeśli proces przygotowywania zakończy się niepowodzeniem, można go szybko usunąć i powtórzyć.
- Dzięki replikacji i powtarzanym testom środowiska przejściowego możliwe jest przyrostowe wykonywanie skryptów i procesu testowania.

**Wada.** Negatywne aspekty tego podejścia są następujące:

- Zasoby przygotowywane w izolowanej za pomocą narzędzi piaskownicy nie zezwalają na zastosowanie złożonych modelów testowania.
- Podczas replikacji narzędzie do migracji zużywa przepustowość w lokalnym centrum danych. Przygotowywanie dużej ilości zasobów przez dłuższy czas ma wykładniczy wpływ na dostępną przepustowość, zakłócając proces migracji i potencjalnie wpływając na wydajność obciążeń produkcyjnych w środowisku lokalnym.

## <a name="staged-promotion"></a>Podwyższanie poziomu w środowisku przejściowym

W tym modelu przejściowa piaskownica zarządzana przez narzędzie do migracji jest używana do przeprowadzania ograniczonego testowania. Zreplikowane zasoby są następnie wdrażane w środowisku chmury, które służy jako rozszerzone środowisko przejściowe. Zmigrowane zasoby działają w chmurze, podczas gdy dodatkowe zasoby są replikowane, przygotowywane i migrowane. Po udostępnieniu pełnych obciążeń inicjowane jest dalsze testowanie. Kiedy zostanie przeprowadzona migracja wszystkich zasobów skojarzonych z subskrypcją, poziom subskrypcji i wszystkich hostowanych obciążeń jest podwyższany do poziomu produkcyjnego. W tym scenariuszu podczas podwyższania poziomu nie są dokonywane żadne zmiany obciążeń. Zamiast tego zmiany są wprowadzane w warstwach sieci i tożsamości, w konsekwencji czego użytkownicy są kierowani do nowego środowiska oraz odwoływany jest dostęp dla zespołu wdrożeniowego ds. chmury.

**Formaty.** Korzyści wynikające z tego podejścia są następujące:

- Ten model zapewnia możliwości dokładniejszego testowania biznesowego.
- Obciążenie może być dokładniej badane w celu lepszego zoptymalizowania wydajności i kosztów zasobów.
- W ramach podobnych ograniczeń dotyczących czasu i przepustowości można zreplikować większą liczbę zasobów.

**Wada.** Negatywne aspekty tego podejścia są następujące:

- Wybrane narzędzie do migracji nie może obsługiwać trwającej replikacji po przeprowadzeniu migracji.
- Dodatkowe środki replikacji danych są wymagane do zsynchronizowania platform danych w ramach horyzontu czasowego przemieszczania.

## <a name="flight-promotion"></a>Podwyższanie poziomu z pakietem testowym

Ten model jest podobny do przejściowego modelu podwyższania poziomu. Istnieje jednak jedna podstawowa różnica. Gdy subskrypcja jest gotowa do podwyższenia poziomu, routing użytkowników końcowych odbywa się w etapach lub pakietach testowych. W każdym pakiecie testowym dodatkowi użytkownicy są kierowani z powrotem do systemów produkcyjnych.

**Formaty.** Korzyści wynikające z tego podejścia są następujące:

- Ten model zmniejsza ryzyko związane z przeprowadzaniem dużych migracji lub wykonywaniem działań mających na celu podwyższenie poziomu. Identyfikacja błędów w zmigrowanym rozwiązaniu może mieć mniejszy wpływ na procesy biznesowe.
- W tym modelu długotrwałe monitorowanie wymagań dotyczących wydajności obciążeń w środowisku chmury zwiększa dokładność podejmowania decyzji dotyczących zmiany rozmiaru zasobów.
- W ramach podobnych ograniczeń dotyczących czasu i przepustowości można zreplikować większą liczbę zasobów.

**Wada.** Negatywne aspekty tego podejścia są następujące:

- Wybrane narzędzie do migracji nie może obsługiwać trwającej replikacji po przeprowadzeniu migracji.
- Dodatkowe środki replikacji danych są wymagane do zsynchronizowania platform danych w ramach horyzontu czasowego przemieszczania.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu i zaakceptowaniu modelu podwyższania poziomu przez zespół wdrożeniowy ds. chmury można rozpocząć [korygowanie zasobów](./remediate.md).

> [!div class="nextstepaction"]
> [Korygowanie zasobów przed migracją](./remediate.md)
