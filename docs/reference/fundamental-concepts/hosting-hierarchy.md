---
title: Zrozumienie i wyrównanie hierarchii portfolio
description: Zrozumienie i wyrównanie hierarchii portfolio
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 816224c77f5825e7bae1e63e5a77db648b5dcfd8
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756111"
---
<!-- cSpell:ignore matrixed ISVs -->

<!-- markdownlint-disable MD026 -->

# <a name="understand-and-align-the-portfolio-hierarchy"></a>Zrozumienie i wyrównanie hierarchii portfolio

Potrzeby biznesowe są często obsługiwane, udoskonalane lub przyspieszane przez technologię informatyczną. Kolekcja technologii, która zapewnia zdefiniowaną wartość biznesową, nazywa się _obciążeniem_. Ta kolekcja może obejmować aplikacje, serwery lub maszyny wirtualne, dane, urządzenia i inne podobne zasoby.

Zwykle uczestnik projektu biznesowego i lider techniczny mają odpowiedzialność za ciągłą obsługę poszczególnych obciążeń. W niektórych fazach cyklu życia obciążenia te role są wyraźnie określone. W przypadku bardziej funkcjonalnej fazy cyklu życia obciążenia te role mogą zostać przeniesione do zespołu zarządzania operacji udostępnionej lub zespołu operacji w chmurze. Wraz ze wzrostem liczby obciążeń role (określone lub implikowane) stają się bardziej skomplikowane i bardziej macierzowe.

Większość firm korzysta z wielu obciążeń w celu dostarczania ważnych funkcji biznesowych. Zbieranie obciążeń, zasobów i współczynniki pomocnicze (projekty, osoby, procesy i inwestycje) nosi nazwę _portfolio_. Macierz biznesowa, rozwój i pracownicy operacyjni wymagają hierarchii portfolio, aby pokazać, jak wszystkie obciążenia i pomocnicze usługi łączą się ze sobą.

Ten artykuł zawiera jasne definicje poziomów hierarchii portfolio. Artykuł wyrównuje różne zespoły z odpowiednią odpowiedzialnością w każdej warstwie oraz ze źródłem najlepszych wskazówek dla tego zespołu w celu dostarczenia na oczekiwania dla tego poziomu. W tym artykule każdy poziom hierarchii jest również nazywany _zakresem_.

## <a name="portfolio-hierarchy"></a>Hierarchia portfolio

Obciążenia i ich zasoby pomocnicze są na początku każdego portfolio. Dodatkowe zakresy lub warstwy poniżej definiują sposób wyświetlania obciążeń i w jakim stopniu mają wpływ macierz potencjalnych zespołów pomocniczych.

Podczas wdrażania pierwszego obciążenia, obciążenie i jego zasoby mogą być jedynym zdefiniowanym zakresem. Inne warstwy mogą być jawnie zdefiniowane w miarę wdrażania większej liczby obciążeń.

![Hierarchia portfolio, platformy, strefy wyładunkowej, obciążeń i zasobów. Wymienione od najwyższego do najniższej kolejności w zagnieżdżonej relacji nadrzędny/podrzędny.](../../_images/ready/hierarchy.png)

Chociaż warunki mogą się różnić, wszystkie rozwiązania IT obejmują zasoby i obciążenia:

- **Zasób:** Najmniejsza jednostka funkcji technicznej, która obsługuje obciążenie lub rozwiązanie.
- **Obciążenie:** Najmniejsza jednostka wsparcia IT dla firmy. Obciążenie to zbiór zasobów (infrastruktury, aplikacji i danych), które obsługują wspólny cel biznesowy lub wykonywanie wspólnego procesu biznesowego.

Gdy firmy obsługują obciążenia za pomocą podejść lub scentralizowanych metod, istnieje szerszej hierarchii, która może obsługiwać te obciążenia:

- **Strefa** docelowa: Strefy wyładunkowe zapewniają obciążenia z dostępem do wszystkich podstawowych _narzędzi_ (lub udostępnionej instalacji wodociągowej), które są dostarczane z _platformy platform Foundation_ , która jest wymagana do obsługi jednego lub większej liczby obciążeń.
- **Narzędzia podstawowe:** Te udostępnione usługi IT są wymagane do obsługi obciążeń w ramach technologii i portfela biznesowego.
- **Platforma platformy:** Ta konstrukcja organizacyjna służy do scentralizowania rozwiązań podstawowych i pomaga zapewnić, że te kontrolki są wymuszane dla wszystkich stref.
- **Platformy w chmurze:** W zależności od ogólnej strategii obsługi pełnego _portfolio_klienci mogą potrzebować wielu platform w chmurze z różnymi wdrożeniami platformy platform Foundation, aby zarządzać wieloma regionami, rozwiązaniami hybrydowymi lub nawet rozwiązaniami wielochmurowymi.
- **Portfolio:** Dzięki soczewkom technologicznym portfolio jest kolekcja obciążeń, zasobów i zasobów pomocniczych obejmujących wszystkie platformy w chmurze. Dzięki soczewkom biznesowym portfolio jest kolekcja projektów, osób, procesów i inwestycji, które obsługują i zarządzają portfolio technologii w celu uzyskania wyników firmy. Razem te dwie soczewki przechwytują _portfolio_.

## <a name="hierarchy-accountability-and-guidance"></a>Odpowiedzialność i wskazówki dotyczące hierarchii

Zespół księgowy zarządza każdą warstwą hierarchii portfolio. Na poniższym diagramie przedstawiono mapowanie między zespołem odpowiedzialnym za konto i wskazówki dotyczące wspierania jego decyzji handlowych, decyzji technicznych i implementacji technicznej.

> [!NOTE]
> Zespoły wymienione na poniższej liście mogą być zespołami wirtualnymi (v-Teams) lub indywidualnymi. W przypadku niektórych wariantów tej hierarchii niektóre zespoły mogą być zwinięte zgodnie z opisem w dalszej części wariantów odpowiedzialności.

![Wyrównanie odpowiedzialności do hierarchii](../../_images/ready/hierarchy-with-roles.png)

<!-- docsTest:ignore "Strategy and Plan methodologies" "Migrate and Plan methodologies" "Migrate and Innovate methodologies" -->

- **Portfolio:** Zespół strategii chmury i centrum w chmurze doskonałości (CCoE) wykorzystują strategię i planować metody, które mają na celu podjęcie decyzji dotyczących ogólnego portfela. Zespół strategii chmury jest odpowiedzialny za poziom przedsiębiorstwa w hierarchii portfolio w chmurze. Zespół strategii chmury powinien również poinformować o decyzjach o środowisku, strefach wyładunkowych i obciążeniach o wysokim priorytecie.
- **Platformy w chmurze:** Zespół zarządzający chmurą jest odpowiedzialny za dyscypliny, które zapewniają spójność w poszczególnych środowiskach z metodologią ładu. Zespół ds. zarządzania chmurą jest odpowiedzialny za zarządzanie wszystkimi zasobami we wszystkich środowiskach. Zespół zarządzający chmurą powinien konsultować zmiany, które mogą wymagać wyjątku lub zmiany w odniesieniu do zasad. Zespół nadzorujący chmury powinien również uzyskać informacje o postępie i przyjęciu zasobów.
- **Strefy wyładunkowe i platforma Cloud Foundation:** Zespół platformy w chmurze jest odpowiedzialny za opracowywanie stref wyładunkowych i narzędzi platformy, które obsługują wdrażanie. Zespół usługi Cloud Automation jest odpowiedzialny za Automatyzowanie rozwoju i ciągłej pomocy technicznej dla tych stref i narzędzi platformy. Oba zespoły korzystają z gotowej metodologii do wdrożenia. Obydwie zespoły powinny otrzymywać informacje o postępie wdrażania obciążeń oraz wszelkich zmianach w przedsiębiorstwie lub środowisku.
- **Obciążenia:** Wdrażanie odbywa się na poziomie obciążenia. Zespoły wdrażające chmur używają metodologii migracji i innowacji do ustanowienia skalowalnych procesów w celu przyspieszenia wdrażania. Po zakończeniu przyjmowania własność obciążeń jest prawdopodobnie przekazywana do zespołu operacji w chmurze, który używa metody zarządzania do obsługi zarządzania operacjami. Oba zespoły powinny być wygodne przy użyciu dobrze zaprojektowanej platformy Microsoft Azure, aby podejmować szczegółowe decyzje dotyczące architektury, które wpływają na obsługiwane przez nie obciążenia. Obydwie zespoły powinny otrzymywać informacje o zmianach w strefach i środowiskach. Oba zespoły mogą sporadycznie wchodzić w skład funkcji strefy wyładunkowej.
- **Zasoby:** Zasoby są zwykle odpowiedzialnością dla zespołu operacji w chmurze. Ten zespół korzysta z linii bazowej zarządzania w metodologii zarządzania, aby przeprowadzić decyzje dotyczące zarządzania operacjami. Należy również użyć Azure Advisor i Microsoft Azure dobrze zaprojektowanej struktury, aby wprowadzić szczegółowe zmiany zasobów i architektury, które są wymagane do dostarczenia na wymagania dotyczące operacji.

### <a name="accountability-variants"></a>Warianty odpowiedzialności:

- **Pojedyncze środowisko:** Jeśli w przedsiębiorstwie wymagane jest tylko jedno środowisko, CCoE nie jest zwykle wymagane.
- **Jedna strefa** docelowa: Jeśli środowisko ma tylko jedną strefę docelową, możliwości zarządzania i platformy mogą być połączone w jeden zespół.
- **Pojedyncze obciążenie:** Niektóre firmy potrzebują tylko jednego obciążenia lub kilku obciążeń w jednej strefie docelowej i jednym środowisku. W takich przypadkach istnieje niewielkie zapotrzebowanie na rozdzielenie obowiązków między zespołami ładu, platform i Operations.

## <a name="common-workload-and-accountability-examples"></a>Typowe przykłady obciążeń i odpowiedzialności

W poniższych przykładach przedstawiono hierarchię portfolio.

### <a name="cots-workloads"></a>Obciążenia NOSIDEŁEK

Tradycyjnie korporacyjne rozwiązania programistyczne (NOSIDEŁEK) mogą korzystać z rozwiązań do zarządzania procesami biznesowymi. Te rozwiązania są instalowane, konfigurowane, a następnie obsługiwane. Istnieje niewiele zmian w architekturze rozwiązań po zakończeniu konfiguracji.

W tych scenariuszach wszystkie wdrożenia w chmurze rozwiązań NOSIDEŁEK kończą się przejściem do zespołu operacji w chmurze. Zespół operacyjny w chmurze stał się właścicielem technicznym tego oprogramowania i przyjmuje odpowiedzialność za zarządzanie konfiguracją, kosztami, cyklami poprawek i innymi potrzebami operacyjnymi.

Te obciążenia obejmują pakiety ewidencjonowania aktywności, oprogramowanie logistyczne lub rozwiązania charakterystyczne dla branż. W terminologii firmy Microsoft dostawcy tych pakietów nazywa się niezależnymi dostawcami oprogramowania (ISV). Wielu niezależnych dostawców oprogramowania oferuje usługę do wdrażania i obsługiwania wystąpienia pakietu oprogramowania w Twoich subskrypcjach. Mogą również oferować wersję pakietu oprogramowania, który działa w środowisku hostowanym w chmurze, zapewniając platformę jako usługę (PaaS) alternatywę dla obciążenia.

Z wyjątkiem ofert PaaS, zespoły operacyjne w chmurze są odpowiedzialne za zapewnienie podstawowych wymagań w zakresie zgodności dla tych obciążeń. Zespół operacyjny w chmurze powinien współpracować z zespołem nadzoru w chmurze w celu wyrównania kosztów, wydajności i innych filarów architektury.

### <a name="in-development-with-active-revisions"></a>W opracowywaniu z aktywnymi poprawkami

Jeśli rozwiązanie NOSIDEŁEK lub oferta PaaS nie jest wyrównana do potrzeb firmy lub nie istnieje rozwiązanie, przedsiębiorstwa tworzą niestandardowe obciążenia. Zazwyczaj niewielka część portfolio IT używa tego podejścia do obciążeń. Jednak te obciążenia mają na celu osiągnięcie nieproporcjonalnie dużej wartości udziału w rezultatach działalności biznesowej, szczególnie w odniesieniu do nowych strumieni przychodów. Te obciążenia są często mapowane na nowe pomysły innowacji.

Ze względu na różne przesunięcia, które są przeznaczone dla metod agile i praktyk DevOps, te obciążenia preferują wyrównanie biznesowe/DevOps na tradycyjne zarządzanie IT. W przypadku tych obciążeń może nie być możliwe przekazanie do zespołu operacji w chmurze przez kilka lat. W takich przypadkach zespół programistyczny służy jako właściciel techniczny obciążenia.

Ze względu na rozbudowane i powiązane ograniczenia kapitałowe, niestandardowe opcje tworzenia są często ograniczone do możliwości wysokiej wartości. Typowe przykłady to innowacje aplikacji, analiza danych szczegółowych lub funkcje biznesowe o kluczowym znaczeniu.

### <a name="breakfix-or-sunset-development"></a>Rozbicie/naprawa lub opracowywanie oprogramowania zachód

Po osiągnięciu przez niestandardowe obciążenie szczytowe, zespół programistyczny może zostać ponownie przypisany do innych projektów. W takich przypadkach własność techniczna zwykle przechodzi do zespołu operacji w chmurze. Jeśli istnieje potrzeba małych poprawek, zespół operacyjny zarejestrowanie deweloperów w celu rozwiązania tego błędu.

W niektórych przypadkach zespół programistyczny przenosi do projektu, który ostatecznie zastąpi bieżące obciążenie. Alternatywnie zespół może się przenieść, ponieważ szansa biznesowa obsługiwana przez obciążenie jest stopniowo wycofywana. Są to przykłady scenariuszy z zachód słońca, w których zespół operacyjny działa jako właściciel techniczny do momentu, gdy obciążenie nie jest już potrzebne.

W obu scenariuszach zespół operacyjny w chmurze zwykle służy jako długoterminowy właściciel techniczny i producent decyzji. Ten zespół prawdopodobnie będzie musiał zarejestrować deweloperów aplikacji, gdy zmiany operacyjne wymagają znaczących zmian w architekturze.

### <a name="mission-critical-workloads"></a>Obciążenia o krytycznym znaczeniu dla działalności

W każdej firmie kilka obciążeń jest zbyt ważne dla firmy, w przypadku których ich awaria nie powiedzie się. W przypadku tych obciążeń o kluczowym znaczeniu zazwyczaj istnieją zwykle operacje i właściciele deweloperów z różnymi poziomami odpowiedzialności. Zespoły te powinny wyrównać zmiany operacyjne i zmiany architektury, aby zminimalizować zakłócenia w rozwiązaniu produkcyjnym.

Te scenariusze wymagają ścisłego skoncentrowania się na rozdzieleniu obowiązków. Aby osiągnąć Rozdzielenie obowiązków, zespół operacyjny zazwyczaj będzie utrzymywać odpowiedzialność za codzienne zmiany operacyjne w środowisku produkcyjnym. Gdy te zmiany operacyjne wymagają zmiany architektury, zostaną one ukończone przez zespół deweloperów lub adopcji w środowisku nieprodukcyjnym, zanim zespół operacyjny zastosuje zmiany do środowiska produkcyjnego.

Przykłady obciążeń o kluczowym znaczeniu wymagające rozdzielenia obowiązków obejmują obciążenia takie jak SAP, Oracle lub inne rozwiązania do planowania zasobów przedsiębiorstwa (ERP), które obejmują wiele jednostek gospodarczych w firmie.

## <a name="strategy-portfolio-alignment"></a>Wyrównanie portfolio strategii

Ważne jest zrozumienie strategicznych celów związanych z wdrażaniem chmury i dostosowanie portfolio do obsługi tej transformacji. Kilka typowych typów strategicznego dopasowania portfolio ułatwia kształtowanie struktury hierarchii portfolio. Poniższe sekcje zawierają przykłady wyrównania i wpływu portfolio w hierarchii portfolio.

### <a name="innovation-or-development-led-portfolio"></a>Portfolio i programowanie na rozwój

Niektóre firmy, szczególnie szybko rozwijające się z ustalonymi uruchomieniami, mają średnią wartość procentową niestandardowych projektów programistycznych. W przypadku portfolio o dużych możliwościach programistycznych środowisko, strefa docelowa i obciążenia są często kompresowane &mdash; . mogą istnieć określone środowiska (środowiska produkcyjne lub nieprodukcyjne) dla określonych obciążeń. Wynikiem tego jest współczynnik 1:1 między środowiskiem, strefą docelową i obciążeniem.

Ze względu na to, że środowisko obsługuje niestandardowe rozwiązania, potok DevOps i raportowanie na poziomie aplikacji mogą zastąpić potrzeby operacji i funkcji ładu. W przypadku tych klientów istnieje duże skoncentrowanie się na działaniach, ładu i innych rolach pomocniczych. Jest to również silniejszy nacisk na obowiązki wdrażania chmury i zespołów automatyzacji chmury.

**Wyrównanie portfolio:** Portfolio IT prawdopodobnie koncentruje się na obciążeniach i właścicielach obciążeń w celu uzyskania krytycznych decyzji dotyczących architektury. Zespoły te mogą znaleźć więcej wartości w Microsoft Azure dobrze wdrożonych wskazówkach platformy w ramach działań związanych z wdrażaniem i działaniami.

**Definicje granic:** Granice logiczne, nawet na poziomie przedsiębiorstwa, prawdopodobnie będą skoncentrowane na segmentacji środowisk produkcyjnych i nieprodukcyjnych. Może być również przejrzyste segmentacja między produktami w portfolio oprogramowania firmy. Czasami może być również segmentacja między programowaniem i hostowanymi wystąpieniami klientów.

### <a name="operations-led-portfolio"></a>Portfolio LED operacji

Wielonarodowe organizacje przedsiębiorstwa z bardziej ustanowionymi zespołami operacyjnymi IT zwykle mają silniejszy fokus na rzecz nadzoru i operacji niż w przypadku rozwoju. W tych organizacjach wyższa część obciążeń zazwyczaj jest wyrównana do kategorii NOSIDEŁEK lub Break/Fix, które są obsługiwane przez właścicieli technicznych w zespole operacji w chmurze.

**Wyrównanie portfolio:** Portfel IT będzie wyrównany do obciążeń, ale te obciążenia są następnie wyrównane do jednostek operacyjnych lub jednostek roboczych. Może być również organizacja dla modeli finansowania, branżowych lub innych wymagań dotyczących segmentacji biznesowej.

**Definicje granic:** Strefy wyładunkowe prawdopodobnie będą grupować aplikacje w Archetypes aplikacji, aby zachować podobne operacje w podobnym segmentacji. Środowiska będą prawdopodobnie odwoływać się do konstrukcji fizycznych, takich jak centrum danych, kraj, region dostawcy chmury lub inne operacyjne standardy organizacji.

### <a name="migration-led-portfolio"></a>Migracja — portfolio LED

Podobnie jak w przypadku portfolio LED operacji, portfolio, który jest w dużym stopniu oparty na migracji, będzie oparty na określonych sterownikach firmy, które doprowadziły do migracji istniejących zasobów. Zazwyczaj centrum danych jest największym czynnikiem w tych sterownikach.

**Wyrównanie portfolio:** Portfolio IT może obciążać obciążenie, ale jest to bardziej dobry wyrównany do zasobów. Jeśli przejścia do operacji IT miały miejsce w historii firmy, wiele zasobów aktywnego użycia może nie być łatwo mapowanych na obciążenie finansowane. W takich przypadkach wiele elementów zawartości może nie mieć zdefiniowanego obciążenia lub nie musi wyznaczać właściciela obciążenia do momentu opóźnienia w procesie migracji.

**Definicje granic:** Strefy wyładunkowe będą prawdopodobnie grupować aplikacje w granice, które odzwierciedlają segmentację lokalną. Chociaż nie jest to najlepsze rozwiązanie, środowiska często pasują do lokalnych nazw centrów danych i stref wyładunkowych, które reprezentują praktyki segmentacji sieci. Lepszym rozwiązaniem jest spójność segmentacji, która jest bardziej blisko zgodna z portfolio z uruchomioną operacją.

### <a name="governance-led-portfolio"></a>Portfolio dla ładu

Wyrównanie do zespołów ładu powinno być wykonywane tak szybko, jak to możliwe. Dzięki praktykom ładu i narzędziom do zarządzania chmurą, portfele i granice środowiska mogą najlepiej zrównoważyć potrzeby innowacji, operacji i migracji.

**Wyrównanie portfolio:** Portfolio o nadzorze ładu umożliwiają uwzględnienie punktów danych, które przechwytują dane innowacyjne i operacje, takie jak obciążenie, właściciel operacji, klasyfikacja danych i krytyczne znaczenie operacyjne. Te punkty danych tworzą dobrze zaokrąglony widok portfolio.

**Definicje granic:** Granice w portfelu ładu, które mają na celu preferują operacje na innowacyjności, natomiast przy użyciu hierarchii opartej na grupach zarządzania, która jest mapowana na kryteria dla jednostek biznesowych i środowisk deweloperskich. Na każdym poziomie hierarchii granica ładu w chmurze może mieć różne stopnie wymuszania zasad, co pozwala na rozwój i elastyczność. W tym samym czasie wymagania dotyczące klasy produkcyjnej mogą być stosowane do subskrypcji produkcyjnych w celu zapewnienia rozdzielenia obowiązków i spójnych operacji.
