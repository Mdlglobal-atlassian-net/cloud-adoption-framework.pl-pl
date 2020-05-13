---
title: Zrozumienie funkcji zarządzania chmurą
description: Poznaj funkcję zespołu nadzoru w chmurze, w tym źródło, zakres i element dostarczany.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/20/2020
ms.openlocfilehash: 1ccda999eb0327f7694374b0589321ca0965f1c2
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215759"
---
<!-- docsTest:ignore IS -->

# <a name="cloud-governance-functions"></a>Funkcje ładu chmury

Zespół zarządzający chmurą gwarantuje, że ryzyko i odporność na ryzyko są prawidłowo oceniane i zarządzane. Ten zespół zapewnia właściwą identyfikację zagrożeń, które nie mogą być tolerowane przez firmę. Osoby na tym zespole konwertują ryzyko na zarządzanie zasadami firmowymi.

W zależności od żądanych wyników działalności biznesowej wymagane są następujące umiejętności, aby zapewnić pełną funkcję ładu w chmurze:

- Zarządzanie IT
- Architektura przedsiębiorstwa
- Zabezpieczenia
- Operacje IT
- Infrastruktura IT
- Networking
- Tożsamość
- Wirtualizacja
- Ciągłość działania i odzyskiwanie po awarii
- Właściciele aplikacji w ramach tej
- Właściciele finansów

Te funkcje linii bazowej pomagają identyfikować zagrożenia związane z bieżącymi i przyszłymi wersjami. Te wysiłki pomagają w ocenie ryzyka, zrozumieniu potencjalnych wpływów i podejmowaniu decyzji dotyczących tolerancji ryzyka. W takim przypadku można szybko zaktualizować plany w celu odzwierciedlenia zmian potrzeb [zespołu migracji w chmurze](./cloud-migration.md).

## <a name="preparation"></a>Przygotowanie

- Zapoznaj się z [metodologią zarządzania](../govern/index.md).
- Weź pod [rząd ocenę oceny wydajności](../govern/benchmark.md).
- [Wprowadzenie do zabezpieczeń na platformie Azure](https://docs.microsoft.com/learn/modules/intro-to-security-in-azure): Poznaj podstawowe pojęcia związane z ochroną infrastruktury i danych w chmurze. Dowiedz się, jakie obowiązki są Twoje i jakie są dla Ciebie obsługiwane przez platformę Azure.
- Informacje o sposobach pracy w grupach w celu [zarządzania kosztami](../organize/cost-conscious-organization.md).

## <a name="minimum-scope"></a>Zakres minimalny

- Zrozumienie [ryzyka biznesowego](../govern/policy-compliance/risk-tolerance.md) wprowadzonego przez plan.
- Reprezentuje [tolerancję firmy dla ryzyka](../govern/policy-compliance/risk-tolerance.md).
- Pomóż utworzyć [specjalistę ładu](../govern/guides/index.md).

Powiąż następujących uczestników z działaniami ładu w chmurze:

- Liderzy od środkowego zarządzania i bezpośrednich współautorów w kluczowych rolach powinni reprezentować firmę i pomóc w ocenie tolerancji ryzyka.
- Funkcje ładu chmury są dostarczane przez rozszerzenie [zespołu strategii chmurowej](./cloud-strategy.md). Tak jak CIO i liderzy biznesowi mogą uczestniczyć w funkcjach strategii chmurowej, ich raporty bezpośrednie mogą uczestniczyć w działaniach związanych z zarządzaniem chmurą.
- Pracownicy biznesowi, którzy są członkami jednostki biznesowej, którzy ściśle współpracują z liderem biznesowym firmy, powinni być uprawnieni do podejmowania decyzji dotyczących zagrożenia firmowego i technicznego.
- Technologie informatyczne (IT) i bezpieczeństwo informacji (IS) pracownicy, którzy rozumieją techniczne aspekty transformacji w chmurze, mogą obsłużyć wydajność, a nie jest spójnym dostawcą funkcji zarządzania chmurą.

## <a name="deliverable"></a>Dostarcza

Misja ładu w chmurze polega na zrównoważeniu konkurencyjnych sił transformacji i ryzyka. Ponadto zarządzanie chmurą gwarantuje, że [zespół migracji w chmurze](./cloud-migration.md) wie o danych i klasyfikacji zasobów, a także wskazówki dotyczące architektury, które regulują wdrażanie. Zespoły nadzoru lub poszczególne osoby współpracują również z [centrum usługi Cloud doskonałości](../organize/cloud-center-of-excellence.md) , aby stosować zautomatyzowane podejścia do zarządzania środowiskami chmury.

**Trwające miesięczne zadania:**

- Zrozumienie [ryzyka biznesowego](../govern/policy-compliance/risk-tolerance.md) wprowadzonego podczas każdej wersji.
- Reprezentuje [tolerancję firmy dla ryzyka](../govern/policy-compliance/risk-tolerance.md).
- Pomoc w przyrostowym ulepszaniu [zasad i wymagań dotyczących zgodności](../govern/policy-compliance/index.md).

**Erze spotkania:**

Zobowiązanie czasu od każdego członka zespołu zespołu nadzoru w chmurze będzie reprezentować znaczną część ich dziennych harmonogramów. Udziały nie będą ograniczone do spotkań i cykli przesyłania opinii.

## <a name="out-of-scope"></a>Poza zakresem

W miarę skalowania, zespół ds. zarządzania chmurą może zadbać o to, aby zachować swoje innowacje. Jest to szczególnie prawdziwe, jeśli środowisko ma duże wymagania dotyczące zgodności, operacji lub zabezpieczeń. W takim przypadku można przenieść niektóre odpowiedzialności do istniejącego zespołu IT, aby ograniczyć zakres dla zespołu nadzoru.

## <a name="next-steps"></a>Następne kroki

Niektóre duże organizacje mają dedykowane zespoły, które koncentrują się na ładu IT. Zespoły te są wyspecjalizowane w zarządzaniu ryzykiem w portfelu IT. Gdy te zespoły istnieją, można szybko przyspieszyć następujące modele zapadalności. Jednak zespół nadzoru IT zachęca do przeglądania modelu ładu chmurowego, aby zrozumieć, w jaki sposób ładu przesunie się nieco w chmurze. Najważniejsze artykuły obejmują rozszerzanie zasad firmowych do chmury i pięć dyscyplin zarządzania chmurą.
Bez nadzoru: jest to typowy dla organizacji, które przechodzą do chmury bez jasnego planu na potrzeby zarządzania. Przed długim zagadnieniami dotyczącymi zabezpieczeń, kosztów, skali i operacji zaczynają wyzwalać konwersacje na temat potrzeb modelu ładu i osób, które mogą personelować procesy skojarzone z tym modelem. Rozpoczęcie tych konwersacji jest zawsze dobrym pierwszym krokiem w celu pokonania antywzorców "No ładu". Sekcja dotycząca definiowania zasad firmowych może ułatwić wykonywanie tych konwersacji.

**Zablokowano zarządzanie:** Jeśli problemy związane z bezpieczeństwem, kosztem, skalą i operacjami nie są przekazywane, projekty i cele biznesowe mają być zablokowane. Brak odpowiedniego nadzoru powoduje wygenerowanie obaw, niepewności i wątpliwości między uczestnikami projektu i inżynierów. Zatrzymaj tę funkcję w jej śladach, podejmując wczesną akcję. Dwie prowadnice ładu zdefiniowane w strukturze wdrażania w chmurze mogą pomóc w rozpoczęciu małego zestawu, a wstępnie ograniczyć zasady w celu zminimalizowania niepewności i wczesnego nadzoru w czasie. Wybierz jedną z złożonych przewodników dla przedsiębiorstw lub standardowego przewodnika Enterprise.

**Dobrowolne zarządzanie:** Brave Souls w każdym przedsiębiorstwie. Gallant to kilka osób, które chcą przeskoczyć i pomóc zespołowi poznać ich błędy. Często jest to sposób uruchamiania ładu, szczególnie w mniejszych firmach. Te Brave soulsją czas na naprawianie niektórych problemów i wypychanie zespołów wdrażania chmurowego do spójnego, dobrze zarządzanego zestawu najlepszych rozwiązań.

Wysiłki tych osób są znacznie lepsze niż scenariusze "bez nadzoru" lub "Blokowanie zablokowane". Podczas gdy ich wysiłki powinny być commendedne, nie należy mylić tego podejścia z zarządzaniem. Właściwe zarządzanie wymaga więcej niż sporadycznej pomocy technicznej w celu zapewnienia spójności dysku, co jest celem jakiegokolwiek dobrego podejścia do ładu. Wskazówki w pięciu dyscyplinach zarządzania chmurą mogą pomóc w opracowaniu tej dyscypliny.

**Powiernik chmury:** Ten moniker stał się wskaźnikiem honoru dla wielu architektów w chmurze, którzy specjalizują się na wczesnym etapie zarządzania. Po pierwszym uruchomieniu praktyk nadzoru wyniki są podobne do tych w przypadku ładu ochotników. Istnieje jednak jedna podstawowa różnica. Powiernik w chmurze ma na uwadze plan. Na tym etapie okresu zapadalności zespół poświęca czas na oczyszczenie Messes przez architektów chmury, którzy wcześniej do nich. Jednak powiernik w chmurze dopasowuje ten nakład do dobrze skonstruowanych zasad firmowych. Korzystają również z narzędzi ładu ładu, takich jak te opisane w temacie ładu MVP.

Kolejną Podstawową różnicą między powiernikiem chmury a kierownictwem ładu jest pomoc techniczna. Przede wszystkim nadmiaru nauczyją się w ciągu kilku godzin. Powiernik w chmurze otrzymuje wsparcie od lidera, aby zmniejszyć dzienne obowiązki w celu zapewnienia, że regularne przydzielanie czasu można zainwestować w celu usprawnienia nadzoru chmurowego.

**Opiekun chmury:** Jako że praktyki ładu zwiększyć i stają się akceptowane przez zespoły rozwiązań w chmurze, rola architektów w chmurze, którzy specjalizują się w ładu, zmienią się w taki sposób, jak rola zespołu zarządzającego chmurą. Ogólnie rzecz biorąc, bardziej dojrzałe praktyki mają na celu zwrócenie uwagi od innych ekspertów, którzy mogą pomóc w wzmocnieniu ochrony zapewnianej przez implementacje ładu.

Różnica jest delikatna, dlatego jest ważnym rozróżnieniem podczas kompilowania kultury IT ukierunkowanej na zarządzanie. Powiernik w chmurze czyści messesy opracowane przez innowacyjne architektów w chmurze, a dwie role mają naturalne tarcie i sprzeciwianie się. Ochrona w chmurze pomaga zapewnić bezpieczną pracę w chmurze, dzięki czemu inne architektzy w chmurze mogą szybko przełączać się do mniejszej liczby Messes.
Opiekunowie w chmurze zaczynają korzystać z bardziej zaawansowanych metod ładu, aby przyspieszyć wdrażanie platformy i zespoły pomocy samoobsługowe ich potrzeby w zakresie środowiska, dzięki czemu mogą być szybciej przenoszone. Przykłady tych bardziej zaawansowanych funkcji są widoczne w ulepszeń przyrostowych dla programu ładu MVP, takich jak poprawa linii bazowej zabezpieczeń.

**Akceleratory chmury:** Opiekunowie w chmurze i usługi w chmurze w sposób naturalny zbierają skrypty i narzędzia do zarządzania, które przyspieszają wdrażanie środowisk, platform, a nawet składników różnych aplikacji. Opieka i udostępnianie tych skryptów oprócz scentralizowanych obowiązków związanych z zarządzaniem pozwala rozwijać w ten sposób wysoki stopień przestrzegania tych architektów.

Te osoby nadzorujące, którzy otwierają swoje skrypty nadzorowane, ułatwiają szybkie dostarczanie projektów technologicznych i osadzanie ładu w architekturze obciążeń. Ten wpływ na obciążenie i obsługę dobrych wzorców projektowych podnosi akceleratory chmury do wyższej rangi specjalisty ds. zarządzania.

**Ładu globalne:** Gdy organizacje zależą od globalnie rozproszonych potrzeb, mogą występować znaczne odchylenia operacji i ładu w różnych lokalizacje geograficzne. Wymagania związane z jednostką biznesową, a nawet wymogi dotyczące niezależności danych lokalnych mogą spowodować najlepsze rozwiązania dotyczące ładu, które zakłócają wymagane operacje. W tych scenariuszach model nadzoru warstwowego umożliwia minimalny poziom spójności i zlokalizowany nadzór. Artykuł dotyczący wielu warstw nadzoru zawiera więcej szczegółowych informacji na temat osiągnięcia tego poziomu dojrzałości.

Każda firma jest unikatowa i w związku z tym ma swoje potrzeby w zakresie zarządzania. Wybierz poziom dojrzałości, który pasuje do Twojej organizacji, i użyj struktury wdrażania w chmurze, aby zapoznać się z praktykami, procesami i narzędziami, które pomogą Ci w tym miejscu.

W miarę rozwoju chmurowego, zespoły są upoważnione do wdrażania chmury w szybszym tępy. Dalsze wysiłki związane z wdrażaniem w chmurze powodują wyzwolenie dojrzałości w operacjach IT. Opracowywanie zespołu operacji w chmurze lub synchronizacja z zespołem operacji w chmurze w celu zapewnienia, że zarządzanie jest częścią rozwoju operacji.

Dowiedz się więcej o uruchamianiu [zespołu zarządzania chmurą](../get-started/team/cloud-governance.md) lub [zespołu operacji w chmurze](../get-started/team/cloud-operations.md).

Po ustaleniu [początkowej podstawy ładu w chmurze](../govern/initial-foundation.md)należy użyć tych najlepszych rozwiązań w ramach [ulepszeń ładu Foundation](../govern/foundation-improvements.md) , aby przejść do planu wdrożenia i zapobiec ryzyku.
