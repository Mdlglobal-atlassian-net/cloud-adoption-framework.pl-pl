---
title: Możliwości ładu chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Opisuje sposób tworzenia możliwości zarządzania chmurą
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 38fa6133c9a4f823d4347b3c1b4db5dd81f24ceb
ms.sourcegitcommit: 7df593a67a2e77b5f61c815814af9f0c36ea5ebd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2020
ms.locfileid: "75781458"
---
# <a name="cloud-governance-capabilities"></a>Możliwości ładu chmury

Każdy rodzaj zmiany generuje nowe ryzyko. Możliwości ładu chmury zapewniają, że ryzyko i odporność na ryzyko są prawidłowo oceniane i zarządzane. Ta funkcja zapewnia właściwą identyfikację zagrożeń, które nie mogą być tolerowane przez firmę. Osoby, które udostępniają tę możliwość, mogą następnie konwertować ryzyka na zasady firmowe. Zasady te są następnie wykonywane przez zdefiniowane dyscypliny wykonywane przez członków personelu, którzy zapewniają możliwości ładu chmurowego.

## <a name="possible-sources-for-this-capability"></a>Możliwe źródła dla tej możliwości

W zależności od żądanych wyników działalności biznesowej umiejętności potrzebne do zapewnienia pełnej możliwości zarządzania chmurą mogą być udostępniane przez:

- Zarządzanie IT
- Architektura przedsiębiorstwa
- Zabezpieczenia
- Operacje IT
- Infrastruktura IT
- Networking
- Tożsamość
- Wirtualizacja
- Ciągłość biznesowa i odzyskiwanie po awarii
- Właściciele aplikacji w ramach tej
- Właściciele finansów

Możliwości ładu chmury identyfikują ryzyko związane z bieżącymi i przyszłymi wersjami. Ta funkcja jest widoczna w obszarze wysiłki, aby oszacować ryzyko, zrozumieć potencjalne oddziaływania i podejmować decyzje dotyczące odporności na ryzyko. W takim przypadku plany można szybko zaktualizować, aby odzwierciedlały zmiany w [możliwościach wdrożenia chmury](./cloud-adoption.md).

## <a name="key-responsibilities"></a>Kluczowe obowiązki

Podstawową opłatą za wszelką możliwość zarządzania chmurą jest równowaga konkurencyjnych sił transformacji i ryzyka. Ponadto zarządzanie chmurą gwarantuje, że wdrożenie [chmury](./cloud-adoption.md) ma świadomość danych i klasyfikacji zasobów oraz wskazówki dotyczące architektury, które regulują wszystkie podejścia do wdrażania. Zespół będzie również współpracował z [centrum usługi Cloud doskonałości](./cloud-center-of-excellence.md) , aby zastosować zautomatyzowane podejścia do zarządzania środowiskami chmury.

Te zadania są zwykle wykonywane przez funkcję ładu w chmurze co miesiąc.

**Zadania wczesnego planowania:**

- Zrozumienie [ryzyka biznesowego](../govern/policy-compliance/risk-tolerance.md) wprowadzonego przez plan
- Reprezentuje [tolerancję biznesową dla ryzyka](../govern/policy-compliance/risk-tolerance.md)
- Pomoc przy tworzeniu [specjalisty ładu](../govern/guides/index.md)

**Trwające miesięczne zadania:**

- Zrozumienie [ryzyka biznesowego](../govern/policy-compliance/risk-tolerance.md) wprowadzonego podczas każdej wersji
- Reprezentuje [tolerancję biznesową dla ryzyka](../govern/policy-compliance/risk-tolerance.md)
- Pomoc w przyrostowym ulepszaniu [zasad i wymagań dotyczących zgodności](../govern/policy-compliance/index.md)

## <a name="meeting-cadence"></a>Erze spotkania

Możliwość zarządzania chmurą jest zwykle dostarczana przez zespół pracujący. Zobowiązanie czasu od każdego członka zespołu będzie reprezentować znaczną część dziennych harmonogramów. Udziały nie będą ograniczone do spotkań i cykli przesyłania opinii.

## <a name="additional-participants"></a>Dodatkowi uczestnicy

Poniżej przedstawiono uczestników, którzy często biorą udział w działaniach ładu w chmurze:

- Liderzy od środkowego zarządzania i bezpośrednich współautorów w kluczowych rolach, które zostały wyznaczone do reprezentowania firmy, będą pomóc w ocenie tolerancji ryzyka.
- Możliwości ładu chmury są dostarczane przez rozszerzenie [możliwości strategii chmury](./cloud-strategy.md). Tak jak CIO i liderzy biznesowi powinni wziąć udział w możliwościach strategii chmury, ich bezpośrednie raporty mogą uczestniczyć w działaniach związanych z zarządzaniem chmurą.
- Pracownicy biznesowi, którzy są członkami jednostki biznesowej, którzy ściśle współpracują z liderem biznesowym firmy, powinni być uprawnieni do podejmowania decyzji dotyczących zagrożenia firmowego i technicznego.
- Technologie informatyczne (IT) i bezpieczeństwo informacji (IS) pracownicy, którzy rozumieją techniczne aspekty transformacji w chmurze, mogą obsłużyć wydajność, a nie jest spójnym dostawcą możliwości zarządzania chmurą.

## <a name="maturation-of-cloud-governance-capability"></a>Dojrzewanie możliwości ładu w chmurze

Niektóre duże organizacje mają istniejące, dedykowane zespoły, które koncentrują się na ładu IT. Zespoły te są wyspecjalizowane w zarządzaniu ryzykiem w portfelu IT. Gdy te zespoły istnieją, można szybko przyspieszyć następujące modele zapadalności. Jednak zespół nadzoru IT zachęca do przeglądania modelu ładu chmurowego, aby zrozumieć, w jaki sposób ładu przesunie się nieco w chmurze. Najważniejsze artykuły obejmują [rozszerzanie zasad firmowych do chmury](../govern/corporate-policy.md) i [pięć dyscyplin zarządzania chmurą](../govern/governance-disciplines.md).

**Brak ładu:** Organizacja jest często przenoszona do chmury bez jasnego planu na potrzeby zarządzania. Przed długim zagadnieniami dotyczącymi zabezpieczeń, kosztów, skali i operacji zaczynają wyzwalać konwersacje na temat potrzeb modelu ładu i osób, które mogą personelować procesy skojarzone z tym modelem. Rozpoczęcie tych konwersacji jest zawsze dobrym pierwszym krokiem w celu pokonania antywzorców "No ładu". Sekcja dotycząca [definiowania zasad firmowych](../govern/corporate-policy.md) może ułatwić wykonywanie tych konwersacji.

**Zablokowano zarządzanie:** Jeśli problemy związane z bezpieczeństwem, kosztem, skalą i operacjami nie są przekazywane, projekty i cele biznesowe mają być zablokowane. Brak odpowiedniego nadzoru powoduje wygenerowanie obaw, niepewności i wątpliwości między uczestnikami projektu i inżynierów. Zatrzymaj tę funkcję w jej śladach, podejmując wczesną akcję. Dwie prowadnice ładu zdefiniowane w strukturze wdrażania w chmurze mogą pomóc w rozpoczęciu małego zestawu, a wstępnie ograniczyć zasady w celu zminimalizowania niepewności i wczesnego nadzoru w czasie. Wybierz jedną z [złożonych przewodników dla przedsiębiorstw](../govern/guides/complex/index.md) lub [standardowego przewodnika Enterprise](../govern/guides/standard/index.md).

**Dobrowolne zarządzanie:** Brave Souls w każdym przedsiębiorstwie. Gallant to kilka osób, które chcą przeskoczyć i pomóc zespołowi poznać ich błędy. Często jest to sposób uruchamiania ładu, szczególnie w mniejszych firmach. Te Brave soulsją czas na naprawianie niektórych problemów i wypychanie zespołów wdrażania chmurowego do spójnego, dobrze zarządzanego zestawu najlepszych rozwiązań.

Wysiłki tych osób są znacznie lepsze niż scenariusze "bez nadzoru" lub "Blokowanie zablokowane". Podczas gdy ich wysiłki powinny być commendedne, nie należy mylić tego podejścia z zarządzaniem. Właściwe zarządzanie wymaga więcej niż sporadycznej pomocy technicznej w celu zapewnienia spójności dysku, co jest celem jakiegokolwiek dobrego podejścia do ładu. Wskazówki w [pięciu dyscyplinach zarządzania chmurą](../govern/governance-disciplines.md) mogą pomóc w opracowaniu tej dyscypliny.

**Powiernik chmury:** Ten moniker stał się wskaźnikiem honoru dla wielu architektów w chmurze, którzy specjalizują się na wczesnym etapie zarządzania. Po pierwszym uruchomieniu praktyk nadzoru wyniki są podobne do tych w przypadku ładu ochotników. Istnieje jednak jedna podstawowa różnica. Powiernik w chmurze ma na uwadze plan. Na tym etapie okresu zapadalności zespół poświęca czas na oczyszczenie Messes przez architektów chmury, którzy wcześniej do nich. Jednak powiernik w chmurze dopasowuje ten nakład do dobrze skonstruowanych [zasad firmowych](../govern/corporate-policy.md). Korzystają również z narzędzi automatyzacji ładu, takich jak te opisane w temacie [ładu MVP](../govern/guides/complex/index.md).

Kolejną Podstawową różnicą między powiernikiem chmury a kierownictwem ładu jest pomoc techniczna. Przede wszystkim nadmiaru nauczyją się w ciągu kilku godzin. Powiernik w chmurze otrzymuje wsparcie od lidera, aby zmniejszyć dzienne obowiązki w celu zapewnienia, że regularne przydzielanie czasu można zainwestować w celu usprawnienia nadzoru chmurowego.

**Opiekun chmury:** Jako że praktyki ładu zwiększyć i stają się akceptowane przez zespoły rozwiązań w chmurze, rola architektów w chmurze, którzy specjalizują się w ładu, zmienią się w taki sposób, jak rola zespołu zarządzającego chmurą. Ogólnie rzecz biorąc, bardziej dojrzałe praktyki mają na celu zwrócenie uwagi od innych ekspertów, którzy mogą pomóc w wzmocnieniu ochrony zapewnianej przez implementacje ładu.

Różnica jest delikatna, dlatego jest ważnym rozróżnieniem podczas kompilowania kultury IT ukierunkowanej na zarządzanie. Powiernik w chmurze czyści messesy opracowane przez innowacyjne architektów w chmurze, a dwie role mają naturalne tarcie i sprzeciwianie się. Ochrona w chmurze pomaga zapewnić bezpieczną pracę w chmurze, dzięki czemu inne architektzy w chmurze mogą szybko przełączać się do mniejszej liczby Messes.

Opiekunowie w chmurze zaczynają korzystać z bardziej zaawansowanych metod ładu, aby przyspieszyć wdrażanie platformy i zespoły pomocy samoobsługowe ich potrzeby w zakresie środowiska, dzięki czemu mogą być szybciej przenoszone. Przykłady tych bardziej zaawansowanych funkcji są widoczne w ulepszeń przyrostowych dla programu ładu MVP, takich jak [poprawa linii bazowej zabezpieczeń](../govern/guides/complex/security-baseline-improvement.md).

**Akceleratory chmury:** Opiekunowie w chmurze i usługa w chmurze w sposób naturalny zbiera skrypty i automatyzacji, które przyspieszają wdrażanie środowisk, platform, a nawet składników różnych aplikacji. Opieka i udostępnianie tych skryptów oprócz scentralizowanych obowiązków związanych z zarządzaniem pozwala rozwijać w ten sposób wysoki stopień przestrzegania tych architektów.

Te osoby nadzorujące, którzy otwierają swoje skrypty nadzorowane, ułatwiają szybkie dostarczanie projektów technologicznych i osadzanie ładu w architekturze obciążeń. Ten wpływ na obciążenie i obsługę dobrych wzorców projektowych podnosi akceleratory chmury do wyższej rangi specjalisty ds. zarządzania.

**Ładu globalne:** Gdy organizacje zależą od globalnie rozproszonych potrzeb, mogą występować znaczne odchylenia operacji i ładu w różnych lokalizacje geograficzne. Wymagania związane z jednostką biznesową, a nawet wymogi dotyczące niezależności danych lokalnych mogą spowodować najlepsze rozwiązania dotyczące ładu, które zakłócają wymagane operacje. W tych scenariuszach model nadzoru warstwowego umożliwia minimalny poziom spójności i zlokalizowany nadzór. Artykuł dotyczący [wielu warstw](../govern/guides/complex/multiple-layers-of-governance.md) nadzoru zawiera więcej szczegółowych informacji na temat osiągnięcia tego poziomu dojrzałości.

Każda firma jest unikatowa i w związku z tym ma swoje potrzeby w zakresie zarządzania. Wybierz poziom dojrzałości, który pasuje do Twojej organizacji, i użyj struktury wdrażania w chmurze, aby zapoznać się z praktykami, procesami i narzędziami, które pomogą Ci w tym miejscu.

## <a name="next-steps"></a>Następne kroki

W miarę rozwoju chmurowego, zespoły będą miały prawo do szybszego wdrażania chmury w tępy. Dalsze wysiłki związane z wdrażaniem w chmurze powodują wyzwolenie dojrzałości w operacjach IT. Ta dojrzewanie może również wymagać rozwoju [możliwości operacji w chmurze](./cloud-operations.md).

> [!div class="nextstepaction"]
> [Opracowywanie możliwości operacji w chmurze](./cloud-operations.md)
