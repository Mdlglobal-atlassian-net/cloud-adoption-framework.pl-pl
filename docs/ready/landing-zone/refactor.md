---
title: Strefy wyładunkowe refaktoryzacji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proces refaktoryzacji stref wyładunkowej
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bc5263b1f9dfcbdb0d5c14e79e5de976fdd59818
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83221811"
---
# <a name="refactor-landing-zones"></a>Strefy wyładunkowe refaktoryzacji

Strefa docelowa to środowisko służące do hostowania obciążeń, a przy tym wstępne **udostępnianie kodu**. Ponieważ infrastruktura strefy wyładunkowej jest zdefiniowana w kodzie, można ją ponownie obsłużyć, podobnie jak w przypadku innych baz kodu. Refaktoryzacja to proces modyfikacji lub restrukturyzacji kodu źródłowego w celu zoptymalizowania danych wyjściowych tego kodu bez zmiany jego celu ani funkcji podstawowych.

Gotowa metodologia używa koncepcji refaktoryzacji w celu przyspieszenia migracji i usunięcia wspólnych blokad. Kroki opisane w temacie gotowe Omówienie omawiają proces, który rozpoczyna się od wstępnie zdefiniowanego szablonu strefy docelowej, który jest wyrównany do funkcji hostingu. Następnie Refaktoryzacja lub Dodaj do kodu źródłowego, aby rozszerzyć strefy wyładunkowe, aby zapewnić tę funkcję poprzez ulepszone zabezpieczenia, działania lub nadzór. Na poniższej ilustracji przedstawiono koncepcję refaktoryzacji.

![Ilustracja refaktoryzacji strefy ładunkowej — opisana w dalszej części tego artykułu](../../_images/ready/refactor.png)

## <a name="common-blockers"></a>Typowe bloki

Gdy klienci przyjmą chmurę, zagadnienia dotyczące strefy wyładunkowej są pojedynczym najbardziej typowym zamiarem do wdrożenia i wyników firmy związanych z chmurą. Klienci mogą przerastać do jednego z następujących dwóch zablokowanych. Często różne zespoły będą przepływać do jednego z tych dwóch zabloków, co sprawia, że zakleszczenie w kulturze utrudniają wdrażanie.

Oba główne bloki są umieszczone w jednym przekonaniu, środowisko chmury i istniejące centra danych powinny mieć wartość z przedziału lub blisko funkcji w zakresie operacji, zarządzania i zabezpieczeń. Jest to bardzo długoterminowy cel. Jednak ból pochodzi z równowagi delikatnej między chronometrażem do osiągnięcia tego celu i szybkością wymaganą do dostarczenia wyników firmy.

### <a name="blocker-acting-too-soon"></a>Blokowanie: działa zbyt wcześnie

Zajęło to lata i istotny nakład na osiągnięcie bieżącego stanu zabezpieczeń, ładu i operacji w bieżącym centrum danych. Wymagane są również obserwacje, uczenie i dostosowania w celu spełnienia unikatowych ograniczeń tego środowiska. Replikowanie tych samych procedur i konfiguracji zajmie trochę czasu. Dotarcie do 100% parzystości funkcji może również spowodować, że środowisko przeprowadzi w chmurze. Takie podejście do parzystości często prowadzi do znacznego niezaplanowanych wydatków w środowisku chmury. Nie należy próbować zastosować bieżących wymagań stanu do środowiska w przyszłości jako bramy wczesnego etapu. Takie podejście rzadko daje zyskowność.

![Typowy blok: działa zbyt wcześnie](../../_images/ready/blocker-act-too-soon.png)

Na powyższym obrazie klient ma cel 100 obciążeń żyjących w chmurze. W tym miejscu klient prawdopodobnie wdroży swoje pierwsze obciążenie. Następnie ich pierwsze 10 lub tak, zanim będą gotowe do wydania jednego z tych obciążeń do środowiska produkcyjnego. Ostatecznie dotrzemy do celu planu wdrożenia i mają niezawodne portfolio w chmurze. Jednak czerwona litera X w obrazie pokazuje, gdzie klienci często są zawieszeń. Oczekiwanie na 100% wyrównanie może opóźnić pierwsze obciążenie przez tygodnie, miesiące lub nawet lata.

### <a name="blocker-acting-too-late"></a>Blokowanie: działa zbyt późno

Z drugiej strony, działając zbyt późno, może mieć znaczne długoterminowe konsekwencje dotyczące sukcesu w chmurze. Jeśli zespół oczekuje na dostęp do funkcji, dopóki nie zostaną ukończone wysiłki, napotykają niepotrzebne przeszkody i wymagają kilku eskalacji, aby zachować wysiłki na śledzenie.

![Typowy blok: działa zbyt późno](../../_images/ready/blocker-act-too-late.png)

Podobnie jak w przypadku tego obrazu, klient czeka zbyt długo, aby dotrzeć do gotowości przedsiębiorstwa między strefami wyładunkowymi. Przez oczekiwanie na zbyt długi czas klient zostanie ograniczony do wielkości refaktoryzacji i rozwinięcia, które mogą być w środowisku. Te ograniczenia spowodują ograniczenie możliwości pomyślnego sukcesu.

### <a name="finding-balance"></a>Znajdowanie salda

Aby uniknąć tych powszechnych bloków, sugerujemy iteracyjne podejście na podstawie dobrze uporządkowanego planu wdrażania chmury, który maksymalizuje możliwości uczenia i minimalizuje czas wdrożenia firmy. Refaktoryzacja i równoległe działania mają kluczowe znaczenie dla tego podejścia.

> [!WARNING]
> Zespół ds. wdrażania, którzy mają cel średni (w ciągu 24 miesięcy), aby **hostować ponad 1 000 zasobów (aplikacje, infrastruktura lub zasoby danych) w chmurze,** bardzo mało prawdopodobne, aby można było pomyślnie korzystać z metody refaktoryzacji. Krzywa uczenia jest zbyt wysoka i oś czasu jest zbyt ścisła, aby umożliwić podejście organiczne do osiągnięcia umiejętności. Dokładniejszy punkt wyjścia wymagający mniejszego dostosowania będzie lepszym rozwiązaniem do osiągnięcia celów. Partnerzy Twojej implementacji prawdopodobnie będą mogli poprowadzić Cię przez lepszy sposób.

Pozostała część tego artykułu koncentruje się na pewnych kluczowych ograniczeniach, które mogą być stosowane do refaktoryzacji, jednocześnie minimalizując ryzyko.

## <a name="theory"></a>Teorii

Koncepcja refaktoryzacji strefy docelowej jest prosta, ale wymaga odpowiedniej guardrails. Koncepcje przedstawione powyżej przedstawiają podstawowe przepływy w następujący sposób. Gdy wszystko jest gotowe do skompilowania pierwszej strefy docelowej, Zacznij od początkowej strefy wyładunkowej zdefiniowanej za pomocą szablonu. Po wdrożeniu tej strefy docelowej należy skorzystać z drzew decyzyjnych w kolejnych artykułach w sekcji "rozszerzanie strefy docelowej" w tej serii artykułów (zobacz Spis treści) do refaktoryzacji i dodać do początkowej strefy docelowej. Powtarzaj decyzje drzewa i refaktoryzacje do momentu, aż masz gotowe do użycia środowisko przedsiębiorstwa, które spełnia rozszerzone wymagania dotyczące zabezpieczeń, operacji i zespołów nadzoru.

## <a name="development-approach"></a>Podejście programistyczne

Zaletą podejścia opartego na refaktoryzacji jest możliwość tworzenia równoległych ścieżek iteracji na potrzeby programowania. Poniższy obraz zawiera przykład dwóch równoległych ścieżek iteracji: wdrażania chmury i platformy w chmurze. Oba postępy w swoim własnym tempie, z minimalnym ryzykiem, gdy zachodzi konieczność zablokowania codziennych wysiłków zespołu. Wyrównanie do planu wdrożenia i Refaktoryzacja guardrails tworzenia zestawu umów dla punktów kontrolnych, które zapewniają jasne przyszłe zależności stanu.

![Równoległa iteracja strefy docelowej](../../_images/ready/iterations.png)

W przykładowych ścieżkach iteracji zespół wdrażania chmury migruje swoje portfolio 100 obciążeń do chmury. Równolegle zespół platformy Cloud Platform koncentruje się na dalszej części planu wdrażania chmury, aby upewnić się, że środowisko jest przygotowane dla tych obciążeń.

W tym przykładzie planowane iteracje działają w następujący sposób:

- Zespół platformy w chmurze rozpocznie prace programistyczne przez wdrożenie początkowej strefy docelowej. Ta strefa docelowa umożliwia zespołowi wdrażania chmury wdrożenie i rozpoczęcie testowania pierwszego obciążenia.
- Aby przygotować się do następnego wdrożenia 10 obciążeń zespołu ds. rozwiązań w chmurze, zespół platform w chmurze pracuje z wyprzedzeniem i doda środowisko połączone, traktując chmurę jako strefę militarized (DMZ).
- Zanim zespół ds. przyjęcia będzie mógł zwolnić swoje pierwsze obciążenie produkcyjne, musi on mieć przegląd zabezpieczeń. Gdy zespół ds. wdrażania wdraża swoje pierwsze 10 obciążeń, zespół platformy przejdzie w przód, aby zdefiniować i zaimplementować wymagania dotyczące zabezpieczeń.
- W momencie wydania pierwszego obciążenia w środowisku produkcyjnym obie zespoły powinny mieć wystarczającą liczbę informacji, aby przygotować się do dłuższego modelu usług udostępnionych. Scentralizowanie podstawowych architektur usług pomoże Ci w rozrównaniu zarządzania i zespołu operacji. Scentralizowanie usług podstawowych pomoże przygotować zespół ds. wdrożenia do skalowania i wypróbowania kolejnej szeregu obciążeń produkcyjnych.
- Ponieważ zespół zbliża się do celu migrowania obciążeń 100, zespół rozpocznie pracę w kierunku większej części modelu współpracy doskonałości i struktury zespołu.

Skonfigurowanie środowiska gotowego dla przedsiębiorstwa zajmie trochę czasu. Takie podejście nie spowoduje eliminacji tego wymagania. Zamiast tego takie podejście służy do usuwania wczesnych blokad i tworzenia szans dla zespołów i rozwiązań do wdrażania, aby poznać siebie.

## <a name="landing-zone-refactoring-guardrails"></a>Guardrails refaktoryzacji strefy wyładunkowej

Wszystkie początkowe szablony stref lądowania mają ograniczenia. Guardrails lub zasady podczas refaktoryzacji powinny odzwierciedlać te ograniczenia. Przed rozpoczęciem procesu refaktoryzacji strefy docelowej należy zrozumieć długoterminowe wymagania planu wdrożenia chmury oraz klasyfikację obciążeń kandydatów w porównaniu z początkowymi ograniczeniami szablonu.

Jako przykład tworzenia refaktoryzacji guardrails, umożliwia porównanie podejścia programistycznego w poprzednim przykładzie, a także Migrowanie planu strefy ładunkowej CAF.

- Zgodnie z [założeniami szczegóły dotyczące CAF migracji strefy ładunkowej](./migrate-landing-zone.md#assumptions)ta początkowa strefa docelowa nie jest przeznaczona do obsługi poufnych danych ani obciążeń o kluczowym znaczeniu. Te funkcje będą musiały zostać dodane przez refaktoryzację.
- W tym przykładzie, pozwala założyć, że portfolio 100 obciążeń będzie wymagało zarówno funkcji krytycznych, jak i poufnych danych.

Aby zrównoważyć te dwa konkurencyjne wymagania, zespół ds. wdrażania i zespół platformy będą działać w ramach następujących uzgodnionych warunków:

- Zespół ds. wdrażania chmury będzie określać priorytety obciążeń produkcyjnych, które nie mają dostępu do poufnych danych i nie są uważane za krytyczne.
- Przed wydaniem produkcyjnym zespół ds. zabezpieczeń i operacji sprawdzi poprawność dostosowania do poprzednich zasad.
- Zespół platformy w chmurze współpracuje z zespołami ds. zabezpieczeń i zarządzania, aby zaimplementować linię bazową zabezpieczeń. Po zatwierdzeniu przez zabezpieczenia zespołu wdrożenia zostanie wyczyszczony w celu migrowania obciążeń, które mają dostęp do poufnych danych.
- Zespół platformy w chmurze będzie współdziałać z zespołem operacji w celu zaimplementowania planu bazowego zarządzania. Gdy zespół operacyjny zatwierdza implementację, zespół adopcji zostanie wyczyszczony w celu migrowania obciążeń o wyższym poziomie krytyczności.

Na potrzeby tego przykładu powyższy zestaw uzgodnionych warunków umożliwi zespołowi adopcji rozpoczęcie pracy związanej z migracją. Ułatwia ona również kształtowanie się zespołu platform w zakresie interakcji z innymi zespołami, ponieważ tworzą one na dłuższy okres gotowy do pracy w przedsiębiorstwie.

## <a name="meeting-long-term-requirements-while-refactoring"></a>Spełnianie długoterminowych wymagań podczas refaktoryzacji

Sekcja gotowej metodologii rozszerzania strefy docelowej pomoże w przeniesieniu do dłuższych warunków. Gdy zespół wdrażający chmurę postępuje zgodnie z planem wdrażania, w sekcji rozszerzanie strefy docelowej zostaną podane wskazówki ułatwiające podejmowanie decyzji i refaktoryzacji zgodnie z rozwijającymi się wymaganiami różnych zespołów.

![Równoległa iteracja strefy docelowej](../../_images/ready/refactor-methodologies.png)

Każda podsekcja "rozszerzanie strefy docelowej" jest mapowana na jeden z dodatków przedstawionych na powyższym obrazie. Poza tymi podstawowymi rozszerzeniami, bardziej szczegółowe metody (takie jak zasady lub zarządzanie) tej struktury będą pomocne w przejściu poza podstawowe modyfikacje strefy docelowej w celu zaimplementowania długoterminowych dyscyplin.

## <a name="next-steps"></a>Następne kroki

Aby rozpocząć proces refaktoryzacji, [Wybierz pierwszą strefę](./first-landing-zone.md)docelową.

> [!div class="nextstepaction"]
> [Wybieranie pierwszej strefy docelowej](./first-landing-zone.md)
