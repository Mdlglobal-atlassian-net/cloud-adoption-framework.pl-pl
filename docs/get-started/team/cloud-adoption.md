---
title: 'Wprowadzenie: Tworzenie zespołu wdrażania w chmurze'
description: Ustanów zakres, elementy dostarczane przez zespół i funkcje, aby przygotować się do pomyślnego wdrożenia chmury.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: cb831deaf758d26d15df0d8797f6fda7d0e8dfbf
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229251"
---
# <a name="get-started-build-a-cloud-adoption-team"></a>Wprowadzenie: Tworzenie zespołu wdrażania w chmurze

Zespoły wdrożeniowe chmury to nowoczesne zespoły zespołów implementacji technicznej lub zespołów projektowych. Jednak charakter chmury może wymagać większej struktury zespołu płynów. Niektóre zespoły rozwiązań w chmurze skupiają się wyłącznie na migracji w chmurze, a inne koncentrują się na innowacjech korzystających z technologii chmurowych. Niektóre z nich obejmują szeroką wiedzę techniczną, która jest wymagana do ukończenia dużych wysiłków związanych z wdrażaniem, takich jak Pełna migracja centrów danych, a inne mają ściślejszy fokus techniczny i mogą poruszać się między projektami w celu osiągnięcia określonych celów, na przykład zespołu specjalistów ds. technologii, którzy ułatwiają konwertowanie maszyn wirtualnych SQL na wystąpienia usługi SQL PaaS.

![Wprowadzenie do tworzenia zespołu wdrażania w chmurze](../../_images/get-started/adoption-team-map.png)

## <a name="step-1-determine-the-type-of-adoption-team-you-need"></a>Krok 1. określenie typu zespołu adopcji, którego potrzebujesz

Zespoły wdrożeniowe w chmurze mogą wykonać jeden lub więcej z następujących rodzajów zastosowania:

    - Migracja istniejących obciążeń.
    - Modernizacja lub istniejące obciążenia i zasoby.
    - Zmiana architektury istniejących obciążeń i zasobów
    - Opracowywanie nowych obciążeń.

Przyjęcie dowolnego portfolio IT prawdopodobnie wymaga zastosowania mieszanki tych umiejętności. Niestety, te różne wysiłki wymagają różnych umiejętności i mindsets. W ramach tych wysiłków bardziej wyspecjalizowany zespół adopcji jest bardziej wydajny i efektywny, że zespół będzie w trakcie dostarczania tego typu pracy. Z drugiej strony wszystkie opcje implementacji w ramach wdrażania w chmurze mogą być przeciążone.

Podczas pierwszego kompilowania zespołu wdrożenia w chmurze dostosowanie do jednej z metod wdrażania pomoże przyspieszyć rozwój umiejętności zespołu.

**Dostarczane**

- Ustal, która metodologia jest Najlepsza dla zespołu: metodologia migracji lub metodologia innowacji.
- Każda metodologia ma cztery etapowe środowisko dołączania, które ułatwia zrozumienie narzędzi i procesów wymaganych do uzyskania naprawdę dobrego działania. Czas inwestycji jako zespół przechodzący przez kilka pierwszych kroków, aby zrozumieć, jakie narzędzia i scenariusze najprawdopodobniej będą potrzebne we wczesnych iteracjach.
- Zaktualizuj firmowe [Szablony Raci](../../organize/raci-alignment.md) , aby pomóc innym użytkownikom w zrozumieniu, kto znajduje się w zespole, i którą metodologią zespół będzie skupić się na dostarczaniu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Przegląd metodologii migracji](../../migrate/index.md) zawiera opis procesu, narzędzi i podejścia do migracji i modernizacji portfolio obciążeń.
- [Przegląd metodologii innowacje](../../innovate/index.md) zawiera opis procesu, narzędzi i podejścia do dodawania obciążeń natywnych w chmurze do portfolio.
- [Zrozumienie koncepcji](../../strategy/motivations.md) związanych z tym zagadnieniem, aby sprawdzić, czy są one lepiej dopasowane do migracji lub wysiłków innowacji.

## <a name="step-2-align-your-team-to-other-supporting-teams"></a>Krok 2. wyrównanie zespołu do innych zespołów pomocniczych

Jeśli nakład pracy związany z wdrażaniem w chmurze firmy jest wystarczająco wcześnie, aby dysponować zespołami pomocniczymi, można znaleźć listę zespołów i ekspertów z dziedziny w Twojej firmie w wersji [Raci szablonu](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx), w tym zarządzania chmurą, operacji w chmurze, centrum rozwiązań w chmurze lub innych podobnych zespołów.

**Dostarczane**

- Zapoznaj się ze wskazówkami dotyczącymi projektu, planami bazowymi, zasadami i procesami z różnych zespołów pomocniczych, aby zrozumieć guardrails, które zostały nawiązane w celu zapoznania się z wdrożeniem chmury.
- Zapoznaj się ze wskazówkami dotyczącymi innych zespołów wdrażania chmury, aby zrozumieć wszelkie ograniczenia, które mogą wystąpić w wyniku tych guardrails.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Oceń zasady firmowe](../../govern/corporate-policy.md) określają procedurę definiowania zasad firmowych, co może ograniczać decyzje, które mogą być bezpiecznie wykonywane w środowisku chmury firmy.
- [Dyscypliny ładu](../../govern/corporate-policy.md) przedstawiają typy kontrolek lub procesów zorganizowanych, które zespół nadzoru prawdopodobnie wdrożono w celu zapewnienia bezpiecznego, zgodnego wdrożenia chmury.
- W obszarze [Zarządzanie metodologią](../../manage/index.md) opisano zagadnienia, które prowadzą do linii bazowej operacji w chmurze, aby zapewnić podstawowe zarządzanie operacjami.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury jest odpowiedzialny za utrzymanie jasnej struktury RACI w całym cyklu życia chmury. | Przejrzyj wskazówki i wymagania z: <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe <li> Inne zespoły wdrażania w chmurze lub poszczególne osoby wymienione w RACI |

## <a name="step-3-begin-your-adoption-journey"></a>Krok 3. rozpoczęcie podróży wdrażania

W zależności od typu zespołu adopcji, którego jesteś członkiem, zaczniesz korzystać z jednej z dwóch podróży:

- Wprowadzenie: Migrowanie obciążeń do chmury.
- Wprowadzenie: tworzenie nowych produktów lub usług.

W każdym z tych przewodników wprowadzenie zobaczysz wskazówki dotyczące różnych zespołów na liście wraz z różnymi stopniami odpowiedzialności i odpowiedzialności. Użyj tych elementów jako informacji referencyjnych, aby zrozumieć, jak zespół mieści się w pozostałej części podróży. Należy również użyć tych odwołań, aby zrozumieć poziomy pomocy technicznej, które będą mogły zostać uzyskane z całego przedsiębiorstwa.

Na koniec zespół ds. wdrażania w chmurze będzie odpowiedzialny za dostarczanie przez przydzielone działania związane z migracją lub opracowywanie nowych produktów. Podczas gdy zespoły pomocnicze są odpowiedzialne za przeprowadzanie kroków w celu pomyślnego wykonania czynności, jest odpowiedzialny za każdy zespół rozwiązań w chmurze, aby upewnić się, że zapewnia pomoc techniczną. Zespół ds. przyjęcia jest zachęcany do współpracy z innymi zespołami w celu wykonania tych czynności, jeśli zespół odpowiedzialny za nie istnieje lub potrzebuje więcej pomocy technicznej w celu dostarczenia na ich potrzeby.

**Dostarczane**

- Coraz lepszym rozwiązaniem jest dostarczanie metodologii związanej z podejściem do wdrażania.
- Obsługa innych zespołów w celu wykonania czynności, gdy te kroki są blokowane dla wdrożenia.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- W przewodniku wprowadzenie do migracji zespół ds. przyjęcia jest odpowiedzialny za dostarczanie [krok 10: Migrowanie pierwszego obciążenia](../migrate.md#step-8-migrate-your-first-10-workloads).
- W przewodniku wprowadzającym dla nowych produktów zespół ds. przyjęcia jest odpowiedzialny za dostarczanie [krok 8: innowacje w chmurze](../innovate.md#step-8-innovate-in-the-cloud).

Wszystkie inne kroki dotyczące tych list kontrolnych zostały zaprojektowane w celu łatwiejszego zarządzania pracą.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Ostatecznie zespół wdrażania w chmurze jest odpowiedzialny za sukces. | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe <li> Zespół strategii chmury |

## <a name="step-4-expand-your-skills-with-scenarios-and-best-practices"></a>Krok 4. rozwijanie umiejętności przy użyciu scenariuszy i najlepszych rozwiązań

Po jednej lub dwóch iteracjach wdrożenia zespół będzie zrozumieć podstawy ich podstawowej metodologii wdrażania. Z tego miejsca zespół będzie prawdopodobnie gotowy do skorzystania z dodatkowych scenariuszy i rozpocząć wdrażanie niektórych dodatkowych najlepszych rozwiązań. Każdy z poniższych linków udostępnia strony docelowe, które ujawniają część spisu treści zawierającej listy obu typów wskazówek dla zespołu, aby przeglądać i rozwijać swoje umiejętności.

**Dostarczane**

- Zwiększ umiejętności i środowisko, aby rozwiązać bardziej złożone scenariusze wdrażania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Migruj nowe typy obciążeń lub Rozwiązuj bardziej złożone wyzwania związane z migracją, korzystając z [scenariuszy](../../migrate/azure-best-practices/contoso-migration-overview.md) i [najlepszych](../../migrate/azure-best-practices/index.md)rozwiązań.
- Wprowadzanie innowacji przy użyciu nowych rozwiązań natywnych w chmurze lub Rozwiązywanie bardziej złożonych wyzwań innowacji dzięki [scenariuszom](../../innovate/kubernetes/index.md) i [najlepszym praktykom](../../innovate/best-practices/index.md).

**Zespół odpowiedzialny za:**

Zespół ds. wdrażania w chmurze jest odpowiedzialny za rozwijanie umiejętności.

## <a name="step-5-build-a-cloud-adoption-factory"></a>Krok 5. Kompilowanie fabryki wdrażania w chmurze

Ponieważ zespół stał się bardziej zaznajomiony z różnymi scenariuszami wdrażania, będziesz mógł szybciej pracować. Ta część wytycznych zajmie się przyjęciem do kolejnego poziomu. Podejście do fabryki rozwiązań w chmurze analizuje procesy związane z wdrażaniem. Większość obciążeń związanych z migracją i innowacyjnością pochodzi z dużej ilości spotkań ze względu na brak wiedzy i przejrzystości. Wyraźne Definiowanie procesów i interakcji w różnych fazach podróży w chmurze spowoduje usunięcie blokowania kulturowego i politycznego.

**Dostarczane**

- Usprawnij procesy dostarczania, aby utworzyć wysoko zoptymalizowaną fabrykę wdrażania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Wskazówki dotyczące procesu do obsługi działań związanych z [migracją](../../migrate/migration-considerations/index.md) można znaleźć w sekcji ulepszenia procesu w metodologii migracji.
- W metodologii innowacji wskazówki koncentrują się na [procesach innowacji](../../innovate/considerations/index.md) , co skutkuje mniejszą technologią i bardziej wpływającym na rozwój produktu.

**Zespół odpowiedzialny za:**

Zespół wdrażania w chmurze jest odpowiedzialny za tworzenie procesów, które przyjmują do następnego poziomu.

## <a name="whats-next"></a>Co dalej

Przyjęcie jest doskonałe, ale nieregulowane wdrożenie może dawać nieoczekiwane wyniki. Wyrównaj wdrożenie chmury dzięki [funkcjom ładu w chmurze](../../organize/cloud-governance.md) , aby przyspieszyć wdrażanie i najlepsze rozwiązania, jednocześnie zmniejszając ryzyko biznesowe i techniczne.

Te dwa zespoły tworzą saldo w ramach wysiłków związanych z wdrażaniem w chmurze, ale są one uznawane za MVP, ponieważ mogą nie być trwałe. Każdy zespół ma wiele systemyów, jak przedstawiono na [wykresach _odpowiedzialnych_ ](../../organize/raci-alignment.md), do których można się skontaktować.

Dowiedz się więcej na temat [antywzorców organizacyjnych: silosów i fiefdoms](../../organize/fiefdoms-silos.md).
