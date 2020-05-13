---
title: Zrównoważone priorytety konkurencji
description: Odkryj strategie dotyczące równoważenia konkurencyjnych priorytetów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: c5eebc5bbc73aa73858daa4b11a3578af8ccc6d9
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219091"
---
# <a name="balance-competing-priorities"></a>Zrównoważone priorytety konkurencji

Zaokrętowanie na drodze cyfrowej transformacji cyfrowych działa jak funkcja wymuszania dla uczestników projektu w zespołach branżowych i technologicznych. Ścieżka do sukcesu jest zdecydowana w organizacji w celu zrównoważenia konkurencyjnych priorytetów.

Podobnie jak w przypadku innych transformacji cyfrowych, wdrażanie w chmurze będzie ujawniać konkurencyjne priorytety w całym cyklu życia. Podobnie jak w przypadku innych form transformacji, zdolność do znajdowania salda tych priorytetów będzie miała znaczny wpływ na realizację wartości biznesowej. Zrównoważenie tych konkurencyjnych priorytetów będzie wymagało otwartych i czasami trudnych konwersacji między uczestnikami projektu (i czasami z poszczególnymi współautorami).

W tym artykule opisano niektóre konkurujące priorytety, które są powszechnie omówione podczas wykonywania każdej metodologii. Mamy nadzieję, że ta zaawansowana świadomość pomoże Ci lepiej przygotować się do tych dyskusji podczas opracowywania strategii wdrażania chmury.

<!-- cSpell:ignore caf -->

![Omówienie cyklu życia wdrożenia w chmurze](../_images/caf-overview.png)

Poniższe sekcje są wyrównane do przepływu w porównaniu z cyklem życia zajmowanego przez chmurę. Jednak ważne jest, aby rozpoznać, że wdrożenie chmury jest iteracyjne (nie proces sekwencyjny), a te priorytety konkurujące (i czasami powtarzają się) w różnych punktach w podróży do wdrożenia chmury.

## <a name="general-theme-of-the-cloud-adoption-framework-approach"></a>Ogólny motyw podejścia do struktury wdrażania chmury

Wbudowane rozwiązania i zaawansowane planowanie są oparte na serii założeń, które mogą (lub mogą nie) być dokładne w czasie. Wdrożenie chmury jest często nowym doświadczeniem dla firmy i zespołów technicznych. Podobnie jak w przypadku większości nowych środowisk lub możliwości uczenia, istnieje wysokie prawdopodobieństwo, że te założenia będą sprawdzone jako fałszywe.

Następujące sprawdzone zasady Agile opóźnionych decyzji technicznych są preferowanym podejściem do większości wskazówek w tej strukturze. Takie podejście odbywa się zgodnie ze spójnym wzorcem: ustanowienie ogólnego stanu końcowego, szybkie przejście do początkowej implementacji, testowanie i weryfikowanie założeń oraz refaktoryzację wczesną, aby zająć się założeniami. Ten typ wzrostu sposób myślenia maksymalizuje uczenie i minimalizuje ryzyko związane z wartością biznesową, ale wymaga pewnego komfortu i niejednoznaczności.

Czasami niejednoznaczność może być scarier (lub bardziej niebezpieczna) od fałszywych założeń. Chociaż ta struktura jest podzielna na uczenie i rozliczanie niejednoznaczności podczas wykonywania, istnieje wiele sytuacji, które wymagają, aby zespół pozostały w drodze do podejścia opartego na analizie lub na podstawie założeń. Poniższe sekcje zawierają próbę zilustrowania co najmniej jednego "rozszerzonego przykładowego zakresu" w każdej sekcji, aby zilustrować czas, w którym druga iteracja może być cenna.

## <a name="balance-during-the-strategy-phase"></a>Saldo w fazie strategii

Podstawowym celem metodologii strategii jest opracowanie rozwinięcia między uczestnikami projektu. Po zdefiniowaniu, które wyrównane do pozycji strategicznej, będzie obsługiwać zachowania w ramach każdej z tych metod, aby zapewnić, że decyzje techniczne umożliwiają dostosowanie żądanych wyników firmy. Rozwijanie rozdzielania między uczestnikami projektu tworzy typowe priorytety konkurujące: **głębokość uzasadnienia** **w porównaniu z czasem do wpływu na działalność biznesową**.

**Priorytety konkurujące:**

- **Głębokość uzasadnienia:** Zainteresowane strony często chcą uzyskać ścisłą analizę finansową i pełne uzasadnienie biznesowe, aby mieć wygodne dopasowanie do kierunku strategicznego. Niestety, ten poziom analizy może wymagać rozszerzonego okresu, aby umożliwić zbieranie i analizowanie danych.
- **Czas do wpływu na działalność biznesową:** Z drugiej strony, zainteresowane osoby często są odpowiedzialne za dostarczanie wyników handlowych w określonych przedziale czasowym. Czasochłonne analizy i oceny mogą spowodować, że te wyniki są narażone na ryzyko przed rozpoczęciem pracy technicznej.

**Minimalny zakres:** Znalezienie tego salda wymaga wcześniejszego omówienia dyskusji udziałowców w procesie. Metodologia strategii sugeruje ograniczenie zakresu wyrównania podczas tego wczesnego nakładu pracy. W sugerowanym podejściu uczestnicy projektu koncentrują się na dostosowywaniu zestawu najważniejszych motywacji, wymiernych rezultatach i ogólnym wyrównaniu biznesowym. Zainteresowane strony powinny następnie szybko zatwierdzić niewielką liczbę początkowych projektów lub pilotażów w celu uzyskania wymaganych możliwości nauki.

**Rozszerzony przykład zakresu:** Jeśli początkowa analiza biznesowa wskazuje na wysokie ryzyko negatywnego wpływu na działalność firmy, może być konieczne spowolnienie i bardziej ostrożne ocenianie dokładniejszej analizy podczas uzasadnienia biznesowego.

## <a name="balance-during-the-plan-phase"></a>Saldo w fazie planu

Podobnie jak w przypadku priorytetów fazy strategii, w fazie planu istnieje potrzeba zrównoważenia głębokości planowania początkowego i opóźnionych decyzji technicznych.

**Priorytety konkurujące:**

- **Głębokość wstępnego planowania** dotycząca implementacji technicznej w chmurze często zawiera dużą liczbę założeń. Szczególnie w przypadku, gdy zespół ma luki w zakresie umiejętności, środowisko to ponosi luki w zakresie odnajdywania lub obciążenia nie mają jasno zdefiniowanych Stanów architektury. Wszystkie te założenia są wspólne dla szczegółowych planów wdrażania w chmurze. Do usunięcia tych założeń są wymagane eksperymenty, pilotaży i analizy jakościowe.
- **Opóźnione decyzje techniczne** założono, że później można podjąć decyzję techniczną, im dokładniejsze jest podjęcie decyzji. Następujące zasady związane z planowaniem produktów Agile pomogą opóźnić decyzje techniczne, umożliwiając im ich wypróbowanie w odpowiednim czasie z odpowiednimi informacjami. Jednak takie podejście powoduje znacznie wyższy stopień niejednoznaczności w planie początkowym.

**Minimalny zakres:** Podejścia do tworzenia produktów Agile są sugerowane w ramach akcji monitowania w ramach zarządzania planami. Metodologia planu zaleca wykonanie poniższych kroków w celu osiągnięcia tego salda. Sporządź spis pełnej cyfrowej przy użyciu zautomatyzowanych narzędzi do odnajdywania, ale Użyj funkcji przyrostowej racjonalizacji do zaplanowania w ciągu następnych 1-3 miesięcy pracy. Upewnij się, że odpowiednie wyrównanie organizacyjne ma być szybko przenoszone. Utwórz plan gotowości do kwalifikacji dla przypisanego zespołu. Użyj szablonu planu wdrażania w chmurze, aby szybko wdrożyć początkową zaległość.

**Rozszerzony przykład zakresu:** Czasami dostarczenie planu wdrażania w chmurze może odpowiadać na zdarzenia biznesowe zależne od czasu lub o dużym wpływie. Gdy sukces wymaga przenoszenia dużej liczby zasobów w ustalonym czasie, powyższe kroki są często wykonywane z dokładniejszym nakładem na planowanie. Kluczem do sukcesu w tych scenariuszach jest zaplanowanie wystarczającej ilości miejsca, aby rozpocząć, a następnie zaplanować pełne zaangażowanie. Takie podejście zmniejsza prawdopodobieństwo zaplanowania blokowania wyników firmy.

## <a name="balance-during-the-ready-phase"></a>Saldo w fazie gotowości

Kiedy zespoły przyjęcia są przygotowywane do ich pierwszych kroków w chmurze, często są konkurujące priorytety między czasem na wdrażanie i długoterminowe operacje. Zespół może się wiązać z dobrym rozwiązaniem, aby zapewnić odpowiednie zadanie zadania w sposób niedobrze zarządzany. Ten problem jest konieczny w tradycyjnych środowiskach IT, w których czynność tworzenia platformy wymaga zasobów fizycznych i cykli pozyskiwania. Jeśli jednak cała platforma IT jest zdefiniowana w kodzie, tradycyjne programowanie taktykę (np. refaktoryzacji) zmniejszy konieczność dobrego zarządzania od początku.

**Priorytety konkurujące:**

- **Długoterminowe operacje:** Klienci często uzyskują dostęp do środowiska chmury, które spełnia wymagania funkcji z aktualnymi systemami zarządzania operacjami, zarządzaniem i bezpieczeństwem. W przypadku bieżącego badania klientów ponad 90% klientów wymagało wsparcia w porównaniu z tym sposób myślenia. Ten program blokujący wprowadza miesiące, spowalniając lub uniemożliwiając wpływ na działalność biznesową.
- **Czas do przyjęcia:** Narzędzia oparte na chmurze, takie jak Azure Policy, plany platformy Azure i grupy zarządzania, umożliwiają łatwe refaktoryzację na platformie IT. Ponadto wstępnie zdefiniowane strefy wyładunkowe zapewniają ceniona stanowiska w celu przyspieszenia wdrożenia do środowiska, które już spełnia wiele wymagań dotyczących parzystości funkcji. Istnieje możliwość przyspieszenia czasu wprowadzenia na rynek przy minimalnym wpływie na długotrwałe operacje.

**Minimalny zakres:** Przygotowana metodologia przedstawia ścieżkę bezpośrednią od szybkiego wdrażania do długotrwałych operacji. Takie podejście rozpoczyna się od podstawowego wprowadzenia do narzędzi, które umożliwiają refaktoryzację środowiska. W oparciu o te narzędzia i wymagania dotyczące środowiska klient jest kierowany do wybranych wstępnie zdefiniowanych stref wyładunkowych (z których każda została dostarczona przy użyciu infrastruktury jako modeli kodu). Kod ten można następnie refaktoryzacji w trakcie wdrażania chmury w celu usprawnienia operacji, bezpieczeństwa i zarządzania postures.

<!-- docsTest:ignore "Govern and Manage methodologies" -->

**Rozszerzony przykład zakresu:** W przypadku zespołów, których plan przyjęcia jest wywoływany przez średniookresowy cel (w ciągu 24 miesięcy) do hostowania **ponad 1 000 zasobów (aplikacji, infrastruktury lub zasobów danych) w chmurze**, sugerowany jest bardziej niezawodny widok stref wypełniania. W takich sytuacjach metodologia rządząca i zarządzanie należy wziąć pod uwagę podczas początkowej konwersacji strefy docelowej. Jednak te szczegółowe zagadnienie często dodaje tygodnie lub miesiące do planu wdrożenia chmury. Aby zminimalizować wpływ na wyniki biznesowe, zespół ds. przyjęcia powinien równolegle obsługiwać rzeczywiste obciążenia w chmurze w celu utworzenia bardziej dojrzałej strefy wyładunkowej i centralnej architektury.

## <a name="balance-during-the-migrate-phase"></a>Saldo w fazie migracji

Podczas prac migracji często chodzi o to, aby zespoły wdrażające założono, że obciążenia zostaną przehostowane w chmurze w ich bieżącej konfiguracji jako Konfiguracja. To bezpośrednie konkurowanie z widokiem wyszukiwania do przodu w celu przetworzenia architektury każdego obciążenia, aby lepiej wykorzystać możliwości chmury. Jednak te dwa nie wykluczają się wzajemnie i mogą być rozłącznych, gdy są zarządzane przez wspólny proces.

**Priorytety konkurujące:**

- **Rehostowanie:** Klienci często są w stanie przeprowadzić migrację do _dźwigu i przenieść_ wszystkie zasoby do chmury w bieżącej konfiguracji stanu. Powoduje to niewielki dryf w portfolio IT. To podejście jest również najszybszym sposobem wycofywania zasobów w istniejącym centrum danych.
- **Rearchitektura:** Modernizacja architektury poszczególnych obciążeń maksymalizuje wartość chmury w kosztach, wydajności i operacjach. Jednak takie podejście jest znacznie wolniejsze i często wymaga dostępu do każdego kodu źródłowego aplikacji.

**Minimalny zakres:** W trakcie planowania wczesnego należy użyć opcji Rehost w celu zaplanowania i jasno zrozumieć, że ta opcja jest początkowym założeniami biznesowymi, a nie z decyzją techniczną. W metodologii migrowania zespół rozwiązań w chmurze będzie następnie zakwestionować to założenie dla każdego zmigrowanego obciążenia. Ta metodologia jest zgodna z podejściem do oceny/migracji/podwyższenia poziomu dla każdego obciążenia lub grupy lub obciążeń tworzących fabrykę migracji. W fazie oceny zespół ds. przyjęcia ocenia dopasowanie techniczne i architekturę każdego obciążenia. Ten nakład oceny rzadko skutkuje czystym podejściem i przesunięciami, ponieważ wiele składników w architekturze można wybrać do refaktoryzacji i modernizacji.

**Rozszerzony przykład zakresu:** W przypadku obciążeń o krytycznym znaczeniu lub dużej czułości, takich jak aplikacja typu mainframe lub wielowarstwowa mikrousług, w fazie oceny mogą być wymagane dokładniejsze oceny obciążenia. W tych sytuacjach związanych z rozarchitekturą klienci powinni skorzystać z przeglądu architektury platformy Azure i platformy Azure Architecturej, aby ograniczyć wymagania dotyczące obciążeń podczas oceny.

## <a name="balance-during-the-innovate-phase"></a>Równowaga w fazie innowacji

Prawdziwe innowacje związane z klientem tworzą typowe priorytety powodujące konflikty między potrzebami dostarczenia do planowanego zestawu funkcji i procesu tworzenia empatię przez klienta.

**Priorytety konkurujące:**

- **Fokus funkcji:** Plany wstępne dla innowacji kompilują się z istniejącej funkcji cyfrowej i w chmurze w celu dostarczenia zestawu funkcji spełniających potrzeby klienta. Jest to łatwe w obsłudze planu do zapewnienia wdrożenia technicznego, co prowadzi do nakładzie pracy związanej z programowaniem. Takie podejście często prowadzi do zaspokojenia tymczasowych uczestników projektu, ale zmniejsza prawdopodobieństwo, że innowacje mają wpływ na zachowania klientów.
- **Empatię klienta:** Plany wstępne są ważną częścią biznesową rozwoju i powinny być uwzględniane w regularnych raportach. Jednak uczenie, mierzenie i kompilowanie za pomocą empatię klienta to Dokładniejszy pomiar sukcesu w wysiłku innowacyjności. Skoncentrowanie się na klientach nad funkcjami ma większe znaczenie w krótkoterminowej i długoterminowej zadowoleniu klientów oraz o znaczeniu biznesowym.

**Minimalny zakres:** Metodologia innowacje ilustruje, jak zintegrować strategię i plany poprzez wartość biznesową konsensusu. W tym przewodniku przedstawiono narzędzia natywne w chmurze, które mogą przyspieszyć poszczególne dyscypliny innowacji, a także najlepsze rozwiązania dotyczące implementacji. Na koniec sekcji ulepszenia procesów przedstawiono podejścia do tworzenia empatię klienta przy jednoczesnym przestrzeganiu planów i strategii w trakcie podróży w chmurze. Takie podejście koncentruje się na dostarczaniu innowacji przy użyciu możliwie najmniejszej technologii.

**Rozszerzony przykład zakresu:** Czasami innowacje mogą być zależne od obciążeń o krytycznym znaczeniu lub dużej czułości. Gdy "klient" jest użytkownikiem wewnętrznym, nakład programistyczny może być zarówno krytyczną, jak i wysoką czułością w najkrótszym czasie iteracji. W tych scenariuszach, zespół ds. wdrażania powinien korzystać z przeglądu architektury platformy Azure i platformy Azure Architecturej, aby oszacować zaawansowane Projektowanie architektury wczesnie w procesie.

## <a name="balance-during-the-govern-phase"></a>Saldo w fazie regulowania

Postępowanie nadzoru w chmurze to stała równowaga między dwoma konkurencyjnymi priorytetami: szybkością i elastycznością a dobrze zarządzanym środowiskiem. Zespół nadzoru chmurowego koncentruje się na ocenie i minimalizacji ryzyka dla działalności firmy za pomocą jednolitych kontroli i minimalizowania zmiany. Zespół ds. przyjęcia koncentruje się na prowadzeniu wyników działalności biznesowej, które wymagają nowych zagrożeń i polega na tworzeniu zmian.

**Priorytety konkurujące:**

- **Dobrze regulowane:** Każda kontrolka zaprojektowana w celu zminimalizowania ryzyka blokuje pewne aspekty zmian lub ogranicza opcje projektowania. Kontrola jest istotna dla dobrze regulowanego środowiska. Jednak po zaprojektowaniu i wdrożeniu formantów w izolacji mogą one być uznawane za szkodliwe jako zagrożenia, które są przeznaczone do zapobiegania.
- **Szybkość i elastyczność:** Szybkość i elastyczność to podstawowe wymagania biznesowe w zakresie gospodarki cyfrowej. Oba muszą mieć możliwość wprowadzenia zmiany z minimalnymi blokowaniem do innowacji lub adopcji. Gdy zmiana jest oparta na izolacji ładu, generuje nowe zagrożenia, które mogą szkodzić firmie w niezamierzony sposób.

**Minimalny zakres:** Metodologia rządząca sugeruje, że w izolacji nie powinno się kiedykolwiek mieć żadnego ładu ani adopcji. Ta metodologia zaczyna się zrozumieć dyscypliny ładu i konwersacje dotyczące ryzyka, zasad i procesów związanych z działalnością biznesową. Jako aktywny członek w trakcie podróży w chmurze zespół nadzoru może zaimplementować minimalny zestaw guardrails, aby sprostać materialnym zagrożeniom w ramach planu wdrażania chmury. Wraz z upływem czasu zespół nadzoru może resłużyć i rozwijać te guardrails w celu spełnienia nowych zagrożeń. Takie podejście maksymalizuje uczenie i innowacje, a jednocześnie minimalizuje ryzyko.

**Rozszerzony przykład zakresu:** Gdy ryzyko biznesowe jest wysokie, szczególnie wczesne w przyjęciu, zespół ds. zarządzania chmurą może być wymagany do przyspieszenia rozwinięcia implementacji zarządzania. Te same wskazówki i ćwiczenia mogą służyć do dodawania tego wyższego poziomu ładu, ale może być konieczne przyspieszenie chronometrażu. W niektórych scenariuszach zaawansowana kondycja ładu może nawet być wymagana podczas wdrażania pierwszej strefy wyładunkowej.

## <a name="balance-during-the-manage-phase"></a>Saldo w fazie zarządzania

Model biznesowy IT dotyczący zarządzania operacjami został ciągle rozwijający się w ciągu ostatnich dekad. W miarę jak konserwacja sprzętu jest w dalszej wersji na podstawie podstawowej wartości, widok w programie Operations Management został również przesunięty. Ponieważ zwiększa to koncentrację na dostarczaniu wartości biznesowej, zespoły zarządzania operacjami są w konflikcie z zrównoważeniem nie-Ops/niską ilością inwestycji.

**Priorytety konkurujące:**

- **Szerokie inwestycje:** W przypadku nieprzerwanego inwestowania w awarie, szybkie odzyskiwanie i monitorowanie w środowisku jest tradycyjne podejście do zarządzania operacjami. Takie podejście może być kosztowne i czasami duplikuje pomocnicze produkty udostępniane przez dostawcę chmury.
- **Nie-Ops i małe operacje:** Korzystaj z natywnych narzędzi do obsługi operacji w chmurze, aby zminimalizować powtarzające się i cykliczne zadania wcześniej dostarczone przez pracowników. Zmniejszenie tych zależności operacyjnych w modelu zarządzania operacjami zwalnia te pracowników, aby zwiększyć ich wartość. Samo takie podejście może prowadzić do subpar obsługi operacji.

**Minimalny zakres:** Metodologia zarządzania sugeruje utworzenie natywnej, niezwiązanej z chmurą linii bazowej. W celu potwierdzenia, że punkt odniesienia No-Ops nie spełni wszystkich potrzeb firmy, współpracuje z firmą w celu zdefiniowania zobowiązań i lepszego wyrównania inwestycji. Rozwiń linię bazową, aby spełnić typowe potrzeby dla wszystkich obciążeń. Następnie Włącz zespoły platformy lub określone zespoły obciążeń, aby zarządzać dobrze zarządzanymi rozwiązaniami w środowisku dobrze zarządzanym.

**Rozszerzony przykład zakresu:** W większości środowisk mała część obciążeń, których wartość biznesowa uzasadnia głębokie inwestycje w operacje. W tych scenariuszach zespół IT może chcieć wykorzystać Przegląd architektury platformy Azure i platformę Azure Architecture w celu zapoznania się z bardziej szczegółowymi operacjami.

## <a name="balance-during-the-organize-phase"></a>Saldo w fazie organizowania

Konkurencyjne priorytety w tym artykule odzwierciedlają dysk IT w celu dostarczenia na wymagania biznesowe dotyczące szybkości i elastyczności. Ta sama zmiana jest wyświetlana w zmianach w schematach organizacyjnych (lub strukturach zespołów v) w celu zapewnienia większego wsparcia dla wyników działania biznesowego. Ponieważ Liderzy IT odzwierciedlają struktury zespołu, często są rozwiązywane dwa konkurencyjne priorytety: scentralizowany formant i delegowany formant.

**Priorytety konkurujące:**

- **Scentralizowana kontrola:** Ten model operacyjny koncentruje się na scentralizowaniu wszystkich kontroli wymaganych do wymuszania sztywnych zasad. W tym modelu służy jako zablokowanie innowacji, szybkości i elastyczności. Może jednak zapewnić wyższy poziom stabilności, zgodności i zabezpieczeń.
- **Delegowany formant:** W ramach tego rozproszonego modelu operacyjnego zakłada się, że każdy zespół DevOps zespołu lub aplikacji biznesowej udostępni swój własny zestaw kontrolek na podstawie rozwiązań wymaganych do realizacji celów firmy. W tym modelu zapewnia guardrails, aby pomóc w utrzymaniu zespołów w podróży, ale jednocześnie minimalizuje liczbę wymuszonych ograniczeń technicznych, jeśli jest to możliwe.

**Minimalny zakres:** Większość organizacji przejdzie przez naturalny zestaw ewolucji z upływem czasu. Metoda Organizuj przedstawia najbardziej typowe serie ewolucji. Proponowane wskazówki są przeznaczone dla zespołów, które mogą dążyć do przechodzenia do struktury usługi Cloud Center doskonałości (CCoE) w celu dostarczenia delegowanych metod kontroli.

**Rozszerzony przykład zakresu:** Istnieje wiele sytuacji, w których należy wyzwolić potrzebę scentralizowanej kontroli. Wymagania dotyczące zgodności innych firm i tymczasowe zagrożenie bezpieczeństwa są dwa przykłady wyzwalaczy dla scentralizowanej kontroli. W takich sytuacjach często istnieje potrzeba ustalenia ograniczenia zasad i sztywnych, stałych kontrolek. Jednak w celu zapewnienia innowacji i adopcji, zaleca się, aby centralni zespoły IT dostarczali te kontrolki w oparciu o krytyczne i czułość poszczególnych obciążeń. Zapewnienie środowisk o mniejszej kontroli, ale ograniczonego zakresu lub profilu ryzyka, umożliwia elastyczność nawet wtedy, gdy wymagana jest kontrola.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [zrównoważyć migrację, innowacje i eksperymenty](./balance-the-portfolio.md) , aby zmaksymalizować wartość działania migracji do chmury.

> [!div class="nextstepaction"]
> [Balansowanie portfolio](./balance-the-portfolio.md)
