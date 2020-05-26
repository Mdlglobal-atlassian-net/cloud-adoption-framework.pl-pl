---
title: 'Wprowadzenie: budowanie centrum w chmurze doskonałości'
description: Ten przewodnik ułatwia zespołowi usługi Cloud Center doskonałości (CCoE) zrozumienie zakresu, elementów dostarczanych i możliwości wymaganych do pomyślnego przeprowadzenia podróży w chmurze.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: ebccc9b47cc12b0b54b9a7aec1c88d2a7e733816
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814312"
---
<!-- cSpell:ignore deprioritize -->

# <a name="get-started-build-a-cloud-center-of-excellence"></a>Wprowadzenie: budowanie centrum w chmurze doskonałości

Centrum w chmurze doskonałości (CCoE) tworzy balans między szybkością i stabilnością.

CCoE może przyspieszyć innowacje i migracje, zmniejszając jednocześnie całkowity koszt zmian i zwiększając elastyczność biznesową. Może to dawać zauważalne redukcje w czasie na rynek. Zgodnie z oczekiwaniami, wskaźniki jakości są ulepszane, z uwzględnieniem niezawodności, wydajności wydajności, bezpieczeństwa, utrzymania i zadowolenia klientów. Korzyści związane z wydajnością, elastycznością i jakością są szczególnie istotne, jeśli firma planuje implementację wysiłków migracji w chmurze na dużą skalę lub chce wykorzystać chmurę do zwiększenia innowacji związanych z rozróżnieniem rynku.

Model CCoE również tworzy znaczną zmianę w kulturze. Podstawową podstawą podejścia CCoE jest to, że służy on jako Broker, partner lub przedstawiciel firmy. Jest to model przesunięty od tradycyjnego widoku jako jednostka operacji lub warstwa abstrakcji między zasobami biznesowymi i INFORMATYCZNymi.

Bez podejścia CCoE, zamierza skupić się na zapewnianiu kontroli i odpowiedzialności centralnej, działającej jak stoplights w przecięciu. Gdy CCoE się powiedzie, fokus jest odpowiedzialny za wolne i delegowane odpowiedzialności, które są bardziej podobne do Roundabout w przecięciu. Żadne podejście nie jest prawidłowe lub nie jest właściwe, są jedynie alternatywnymi widokami odpowiedzialności i zarządzania. Jeśli chcesz ustanowić model samoobsługowy, który umożliwia jednostkom biznesowym podejmowanie własnych decyzji, przy równoczesnym przestrzeganiu zestawu wytycznych i ustalonych, powtarzalnych kontrolek, model CCoE może pasować do strategii technologicznej.

## <a name="prerequisites"></a>Wymagania wstępne

- Zweryfikuj tolerancję firmy na potrzeby wzrostu sposób myślenia i wygodnie wydawanie centralnych obowiązków. Jak wspomniano powyżej, celem CCoE jest wymiana kontroli nad elastyczność i szybkość.
- Upewnij się, że masz pomoc techniczną od lidera i najważniejszych udziałowców.

## <a name="minimum-scope"></a>Zakres minimalny

Głównym cłem zespołu CCoE jest przyspieszenie wdrażania chmury za pomocą rozwiązań natywnych lub hybrydowych.

Celem CCoE jest:

- Pomóż w tworzeniu nowoczesnej organizacji INFORMATYCZNej za pomocą podejścia Agile do przechwytywania i implementowania wymagań firmy.
- Użyj pakietów wdrożeniowych wielokrotnego użytku, które są zgodne z zasadami zarządzania zabezpieczeniami, zgodności i usług.
- Obsługa funkcjonalnej platformy platformy Azure w celu wyrównania przy użyciu procedur operacyjnych.
- Przejrzyj i zatwierdź korzystanie z narzędzi natywnych w chmurze.
- W miarę upływu czasu można znormalizować i zautomatyzować często używane składniki i rozwiązania platformy.

## <a name="deliverables"></a>Rezultaty

CCoE wysiłki mogą być przyspieszone z pomocą techniczną zainteresowanych stron firmy. CCoE wysiłki są wyśrodkowane w celu wprowadzenia długoterminowych ulepszeń biznesowych i szybkości. Zdefiniowanie wpływu bieżących modeli operacyjnych i wartości ulepszeń jest przydatne jako narzędzie przewodnika i negocjowania dla CCoE.

Udokumentowanie następujących:

- Ustanów zestaw wyników i celów działalności, które są oczekiwane w wyniku elastyczności i szybkości działania firmy.
- Jasno definiować wyłączane punkty utworzone przez bieżące procesy IT (takie jak szybkość, elastyczność, stabilność i wyzwania dotyczące kosztów).
- Jasno określaj historyczny wpływ tych problemów, takich jak utracony udział w rynku, korzyści dla konkurentów w funkcjach i funkcje, słabe środowiska klienta i wzrost budżetu.
- Zdefiniuj możliwości poprawy biznesowe, które są blokowane przez bieżące punkty i modele operacyjne.
- Ustanów osie czasu i metryki związane z tymi szansami.

Te punkty danych nie są na nim atakowane. Zamiast tego pomagają CCoE uczyć się od przeszłości i tworzyć realistyczne zaległości oraz planować ulepszenia.

### <a name="solutions-and-controls"></a>Rozwiązania i kontrolki

Każdy element członkowski CCoE jest związany z zrozumieniem niezbędnych ograniczeń, ryzyka i ochrony, które doprowadziły do bieżącego zestawu formantów IT. Zbiorowe wysiłki CCoE powinny mieć na celu uwzględnienie rozwiązań w chmurze (lub hybrydowych), które umożliwiają odpowiednie wyniki biznesowe samoobsługi. W miarę tworzenia rozwiązań są one udostępniane różnym zespołom w formie formantów lub zautomatyzowanych procesów, które służą jako guardrails do różnych wysiłków. Te guardrails pomoc w kierowaniu działań związanych z przepływem pracy różnych zespołów i delegowanie obowiązków do uczestników w różnych procesach migracji lub innowacji.

Przykłady tego przejścia:

| Scenariusz | Rozwiązanie CCoE | Rozwiązanie po CCoE |
|---------|---------|---------|
| Inicjowanie obsługi administracyjnej SQL Server produkcyjnych | Zespoły sieci, IT i danych udostępniają różne składniki w ciągu kilku dni lub nawet tygodni. | Zespół wymagający serwera wdraża wystąpienie PaaS Azure SQL Database. Można również użyć prezatwierdzonego szablonu do wdrożenia wszystkich zasobów IaaS w chmurze w godzinach. |
| Inicjowanie obsługi administracyjnej środowiska programistycznego | Zespoły Network, IT, Development i DevOps wyrażają zgodę na specyfikacje i wdrożenie środowiska. | Zespół programistyczny definiuje własne specyfikacje i wdraża środowisko na podstawie przydzielonych budżetów. |
| Aktualizuj wymagania dotyczące zabezpieczeń, aby zwiększyć ochronę danych | Zespoły sieci, IT i zabezpieczeń umożliwiają aktualizowanie różnych urządzeń sieciowych i maszyn wirtualnych w wielu środowiskach w celu dodania ochrony. | Narzędzia do zarządzania chmurą służą do aktualizowania zasad, które mogą być stosowane natychmiast do wszystkich zasobów we wszystkich środowiskach w chmurze. |

### <a name="negotiations"></a>Negocjacji

W katalogu głównym dowolnego wysiłku CCoE jest proces trwającej negocjacji. Zespół CCoE negocjuje z istniejącymi funkcjami IT, aby zmniejszyć centralną kontrolę. Wady dla działalności firmy w tej negocjacji to swoboda, elastyczność i szybkość. Wartość handlu dla istniejących zespołów IT jest dostarczana jako nowe rozwiązania. Nowe rozwiązania zapewniają istniejący zespół IT z co najmniej jedną z następujących korzyści:

- Możliwość automatyzowania typowych problemów.
- Ulepszenia spójności (skrócenie w codziennym frustrations).
- Możliwość uczenia i wdrożenia nowych rozwiązań technicznych.
- Zmniejszenie zdarzeń o wysokiej ważności (mniej krótkich poprawek lub późnych odpowiedzi na pager).
- Możliwość rozszerzenia zakresu technicznego, który zajmuje się szerszymi tematami.
- Uczestnictwo w rozwiązaniach biznesowych wyższego poziomu, które dotyczą wpływu technologii.
- Zmniejszenie menial zadań konserwacyjnych.
- Zwiększenie strategii technologicznej i automatyzacji.

W programie Exchange dla tych korzyści istniejąca funkcja IT może być transakcją następujących wartości, niezależnie od tego, czy są prawdziwe czy postrzegane:

- Wykrywanie kontroli z ręcznych procesów zatwierdzania.
- Wykrywanie stabilności z kontroli zmian.
- Sense bezpieczeństwa zadań przed ukończeniem niezbędnych, niepowtarzalnych zadań.
- Wykrywanie spójności, które wynikają z przestrzegania istniejących dostawców rozwiązań IT.

W dobrej kondycji firmy, ten proces negocjacji jest dynamiczną konwersacją między elementami równorzędnymi i partnerskimi zespołami IT. Szczegóły techniczne mogą być złożone, ale można nimi zarządzać, gdy rozumieją one cel i wspierają wysiłki CCoE.

### <a name="meeting-cadence"></a>Erze spotkania

CCoE jest funkcją podaną przez zespoły o dużej zapotrzebowaniu. Ważne jest, aby umożliwić współpracę organiczną i śledzenie wzrostu za pomocą wspólnego repozytorium/wykazu rozwiązań. Maksymalizuj interakcje naturalne, ale Zminimalizuj spotkania. Gdy ta funkcja jest dojrzała, zespoły powinny próbować ograniczyć liczbę przeznaczonych spotkań. Uczestnictwo w spotkaniach cyklicznych, takich jak spotkania wydania obsługiwane przez zespół ds. wdrażania chmury, udostępnia dane wejściowe. Równolegle, spotkanie po każdym planie wydania może zapewnić minimalny punkt dotykowy dla tego zespołu.

**Pomoc techniczna i zaangażowanie w biznesie:** Zespoły CCoE mogą przedstawiać szybkie zwroty w niektórych obszarach. Cele wyższego poziomu, takie jak elastyczność biznesowa i czas wprowadzenia na rynek, mogą zająć dużo czasu. W trakcie dojrzewania istnieje duże ryzyko, że CCoE nie zostanie zaakceptowany lub wycofane, aby skoncentrować się na innych wysiłkach IT.

W okresie pierwszych sześciu do dziewięciu miesięcy CCoE się, że zainteresowane strony biznesowe przydzielą czas na spełnienie miesięcznego lidera IT i CCoE. W przypadku formalnych procedury do tych spotkań istnieje niewielkie zapotrzebowanie. Wystarczy pamiętać, że CCoE członkowie i ich kierownictwo znaczenia tego programu mogą wejść w sposób, aby CCoE sukces.

Ponadto zalecamy, aby zainteresowane strony biznesowe były poinformowane o postępie i zablokowaniu napotykanym przez zespół CCoE. Wiele z ich wysiłków będzie wyglądać jak techniczne minutiae. Ważne jest, aby umożliwić zainteresowanym stronom zrozumienie postępu planu, dzięki czemu mogą one mieć wpływ na to, kiedy zespół rozwiąże pary lub rozprasza inne priorytety.

**Uczestnicy projektu IT wspierają wizję:** Pomyślne CCoE pracy wymaga dużej liczby negocjacji z istniejącymi członkami zespołu IT. Po wykonaniu tych czynności wszystkie te składniki przyczyniają się do rozwiązania i zauważają się za odpowiednie zmiany. Jeśli tak się nie dzieje, niektórzy członkowie istniejącego zespołu IT mogą chcieć zamieścić mechanizmy kontroli z różnych powodów. Wsparcie dla udziałowców IT jest istotne dla sukcesu CCoE, gdy wystąpią takie sytuacje. Zachęcanie i wzmocnienie ogólnych celów CCoE jest ważne, aby rozwiązać blokować odpowiednie negocjacje. W rzadkich przypadkach, zainteresowane strony IT mogą nawet wymagać dalszych kroków i rozdzielić zakleszczenie lub głos związany z CCoEem.

**Uczestnicy działu IT wspierają priorytety:** CCoE może być znaczącym zobowiązaniem dla dowolnego zespołu z ograniczoną ilością zasobów. Usuwanie silnych architektów z projektów krótkoterminowych do skoncentrowania się na długoterminowych korzyściach może stworzyć trudności dla członków zespołu, którzy nie są częścią CCoE. Ważne jest, aby skoncentrować się na tym, i że uczestnicy IT pozostają w stanie skupić się na celu CCoE. Obsługa liderów IT i udziałowców IT jest wymagana do rozróżnienia zakłóceń codziennych operacji na rzecz CCoE obowiązków.

**Zainteresowane strony IT zapewniają bufor i odpowiedzialność:** Zespół CCoE będzie eksperymentować z nowymi metodami. Niektóre z tych metod nie są dobrze wyrównane z istniejącymi operacjami lub ograniczeniami technicznymi. Istnieje realne ryzyko wystąpienia CCoE w przypadku, gdy eksperymenty kończą się niepowodzeniem. Ważne jest, aby zachęcić i buforować zespół z powodu skutków "szybkiej awarii". Równie ważne jest, aby zapewnić, że zespół jest odpowiedzialny za rozwój sposób myślenia, dzięki czemu są one dostępne do uczenia się i znajdowania lepszych rozwiązań.

## <a name="baseline-capability"></a>Możliwość linii bazowej

Model CCoE wymaga współpracy między następującymi możliwościami:

- Wdrażanie w chmurze (w szczególnych architektach rozwiązań).
- Strategia chmury (w przypadku programu i menedżerów projektów).
- Ład w chmurze.
- Platforma w chmurze.
- Automatyzacja w chmurze.

Ten model wymaga również wsparcia ze strony lidera i najważniejszych udziałowców.

Liderem jest pierwszy i najbardziej oczywisty uczestnik projektu. Menedżerowie IT będą odgrywać ważną część. Wsparcie CIO i innych liderów IT na poziomie kierownictwa jest decydujące w trakcie tego procesu.

Mniej oczywisty jest potrzebą dla uczestników biznesowych. Elastyczność biznesowa i czas wprowadzenia na rynek to kluczowe motywacje do tworzenia CCoE. Przykłady uczestników biznesowych obejmują liderów biznesowych, kadry kierowniczej, dyrektorów operacji i właścicieli produktów biznesowych.

## <a name="whats-next"></a>Co dalej

Model CCoE wymaga [możliwości platformy chmury](./cloud-platform.md) i [możliwości automatyzacji w chmurze](./cloud-automation.md). Następnym krokiem jest dostosowanie [możliwości platformy w chmurze](./cloud-platform.md).
