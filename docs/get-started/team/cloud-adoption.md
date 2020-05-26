---
title: 'Wprowadzenie: Tworzenie zespołu wdrażania w chmurze'
description: Ustanów zakres, elementy dostarczane przez zespół i funkcje, aby przygotować się do pomyślnego wdrożenia chmury.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 33744f6911ec724c517a7fa93979a8adbdd370c1
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814466"
---
# <a name="get-started-build-a-cloud-adoption-team"></a>Wprowadzenie: Tworzenie zespołu wdrażania w chmurze

Zespoły wdrożeniowe chmury to nowoczesne zespoły zespołów implementacji technicznej lub zespołów projektowych. Charakter chmury może wymagać większej liczby struktur zespołu płynów.

Niektóre zespoły rozwiązań w chmurze skupiają się wyłącznie na migracji do chmury, a inne koncentrują się na innowacjach korzystających z technologii chmurowych. Niektóre zespoły obejmują szeroką wiedzę techniczną, która jest wymagana do ukończenia dużych wysiłków związanych z wdrażaniem, takich jak Pełna migracja centrów danych, a inne mają ściślejszy fokus techniczny.

Mniejszy zespół może przenosić się między projektami w celu osiągnięcia określonych celów. Na przykład zespół specjalistów ds. platformy danych może skupić się na ułatwianiu konwersji SQL Database maszyn wirtualnych na wystąpienia usługi SQL PaaS.

![Wprowadzenie do tworzenia zespołu wdrażania w chmurze](../../_images/get-started/adoption-team-map.png)

## <a name="step-1-determine-the-type-of-adoption-team-you-need"></a>Krok 1. określenie typu zespołu adopcji, którego potrzebujesz

Zespoły wdrożeniowe w chmurze mogą wykonać jeden lub więcej z następujących rodzajów zastosowania:

- Migracja istniejących obciążeń
- Modernizacja istniejących obciążeń i zasobów
- Zmiana architektury istniejących obciążeń i zasobów
- Opracowywanie nowych obciążeń

Przyjęcie dowolnego portfolio IT prawdopodobnie wymaga zastosowania mieszanki tego rodzaju wysiłków. Niestety każdy typ wymaga różnych umiejętności i mindsets. Im bardziej wyspecjalizowany zespół ds. przyjęcia, tym bardziej wydajny i efektywny zespół będzie mógł uzyskać ten typ pracy. Z drugiej strony wszystkie opcje implementacji w chmurze mogą być przeciążone dla bardziej wyspecjalizowanych zespołów.

Podczas pierwszego kompilowania zespołu wdrażania w chmurze, dostosowanie z jedną z metod wdrażania ułatwi rozwój umiejętności zespołu.

**Dostarczane**

- Ustal, która metodologia jest Najlepsza dla zespołu: metodologia migracji lub metodologia innowacji.
- Każda metodologia ma cztery etapy dołączania, które ułatwiają zespołowi zrozumienie narzędzi i procesów, które są wymagane, aby naprawdę to miało dobry dostęp. Czas inwestycji jako zespół przechodzący przez kilka pierwszych kroków, aby zrozumieć, jakie narzędzia i scenariusze najprawdopodobniej są potrzebne we wczesnych iteracjach.
- Zaktualizuj [Raci firmy (odpowiedzialny](../../organize/raci-alignment.md) , umożliwiający zapoznanie się z informacjami i wiedzą), aby pomóc innym użytkownikom w zrozumieniu zespołu i metodologii, którą zespół będzie skupić na dostarczaniu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Przegląd metodologii migracji](../../migrate/index.md) zawiera opis procesu, narzędzi i podejścia do migracji i modernizacji portfolio obciążeń.
- [Przegląd metodologii innowacje](../../innovate/index.md) zawiera opis procesu, narzędzi i podejścia do dodawania obciążeń natywnych w chmurze do portfolio.
- Zapoznaj się z [uzasadnieniami](../../strategy/motivations.md) związanymi z tym wysiłkiem, aby sprawdzić, czy są one lepiej dopasowane do migracji lub wysiłków innowacji.

## <a name="step-2-align-your-team-with-other-supporting-teams"></a>Krok 2. Wyrównywanie zespołu z innymi zespołami pomocniczymi

Jeśli nakład pracy związany z wdrażaniem w chmurze firmy jest wystarczająco wcześnie, aby dysponować zespołami pomocniczymi, można znaleźć listę zespołów i ekspertów z dziedziny w Twojej firmie w wersji [Raci szablonu](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx), w tym zarządzania chmurą, operacji w chmurze, centrum rozwiązań w chmurze lub innych podobnych zespołów.

**Dostarczane**

- Zapoznaj się ze wskazówkami dotyczącymi projektu, planami bazowymi, zasadami i procesami z różnych zespołów pomocniczych, aby zrozumieć guardrails, które zostały nawiązane dla tworzenia chmurowych operacji.
- Zapoznaj się ze wskazówkami dotyczącymi innych zespołów wdrażania chmury, aby zrozumieć wszelkie ograniczenia, które mogą wystąpić w wyniku tych guardrails.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Oceń zasady firmowe](../../govern/corporate-policy.md) określają procedurę definiowania zasad firmowych, co może ograniczyć decyzje, które zespół może bezpiecznie wprowadzić w środowisku chmury firmy.
- [Dyscypliny ładu](../../govern/corporate-policy.md) przedstawiają typy kontrolek lub procesów zorganizowanych, które zespół nadzoru może zaimplementować, aby umożliwić bezpieczne, zgodne Wdrażanie chmury.
- W obszarze [Zarządzanie metodologią](../../manage/index.md) opisano zagadnienia, które przechodzą do linii bazowej operacji w chmurze w celu zapewnienia podstawowego zarządzania operacjami.

<!-- markdownlint-disable MD033 -->

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury jest odpowiedzialny za utrzymanie jasnej struktury RACI w całym cyklu życia chmury. | Przejrzyj wskazówki i wymagania z: <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe <li> Inne zespoły wdrażania w chmurze lub poszczególne osoby wymienione w RACI |

## <a name="step-3-begin-your-adoption-journey"></a>Krok 3. rozpoczęcie podróży wdrażania

W zależności od typu zespołu adopcji, którego jesteś członkiem, rozpocznie się jedno z następujących podróży:

- Wprowadzenie: Migrowanie obciążeń do chmury
- Wprowadzenie: tworzenie nowych produktów lub usług

Te przewodniki wprowadzające zawierają wskazówki dotyczące różnych zespołów wymienionych wraz z ich różnymi stopniami odpowiedzialności i odpowiedzialności. Skorzystaj z przewodników, aby zrozumieć, jak zespół mieści się w pozostałej części podróży. Należy również użyć ich do zrozumienia poziomów wsparcia, które można oczekiwać od firmy.

Na koniec zespół wdrażania w chmurze jest odpowiedzialny za dostarczanie w ramach ich przypisanych działań związanych z migracją lub nowego produktu. Mimo że zespoły pomocnicze są odpowiedzialne za zapewnianie, że każdy krok zostanie ukończony, jest odpowiedzialny za każdy zespół rozwiązań w chmurze, aby upewnić się, że zespół pomocniczy otrzymuje pomoc techniczną. Jeśli zespół obsługujący konto jeszcze nie istnieje lub potrzebuje więcej pomocy technicznej w celu dostarczenia na kolejne kroki, zachęcamy do partnera z innymi zespołami, aby dokończyć swoje dostawy.

**Dostarczane**

- Coraz lepszym rozwiązaniem jest dostarczanie metodologii związanej z podejściem do wdrażania.
- Obsługa innych zespołów w celu wykonania czynności związanych z ich kontem, nawet jeśli te kroki są blokadami w celu podjęcia działań.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- W przewodniku Get-Started dla migracji zespół ds. przyjęcia jest odpowiedzialny za dostarczanie [krok 10: Migrowanie pierwszego obciążenia](../migrate.md#step-8-migrate-your-first-10-workloads).
- W podręczniku Get-Started dla nowych produktów zespół ds. przyjęcia jest odpowiedzialny za dostarczanie [krok 8: innowacje w chmurze](../innovate.md#step-8-innovate-in-the-cloud).

Wszystkie inne kroki dotyczące tych list kontrolnych zostały zaprojektowane w celu łatwiejszego zarządzania pracą.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe <li> Zespół strategii chmury |

## <a name="step-4-expand-your-skills-with-scenarios-and-best-practices"></a>Krok 4. rozwijanie umiejętności przy użyciu scenariuszy i najlepszych rozwiązań

Po jednej lub dwóch iteracjach zespół ds. wdrażania chmury zapoznaje się z podstawą ich podstawowej metodologii. Z tego miejsca zespół będzie prawdopodobnie gotowy do skorzystania z dodatkowych scenariuszy i rozpocząć wdrażanie niektórych dodatkowych najlepszych rozwiązań.

**Dostarczane**

- Zwiększ umiejętności i środowisko, aby rozwiązać bardziej złożone scenariusze wdrażania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

Zespół może przeglądać i rozwijać swoje umiejętności, przeglądając następujące wskazówki:

- Migruj nowe typy obciążeń lub Rozwiązuj bardziej złożone wyzwania związane z migracją, korzystając z [scenariuszy](../../migrate/azure-best-practices/contoso-migration-overview.md) i [najlepszych](../../migrate/azure-best-practices/index.md)rozwiązań.
- Wprowadzanie innowacji przy użyciu nowych rozwiązań w chmurze lub Rozwiązywanie bardziej złożonych wyzwań dzięki [scenariuszom](../../innovate/kubernetes/index.md) i [najlepszym praktykom](../../innovate/best-practices/index.md).

**Zespół odpowiedzialny za:**

- Zespół ds. wdrażania w chmurze jest odpowiedzialny za rozwijanie umiejętności.

## <a name="step-5-build-a-cloud-adoption-factory"></a>Krok 5. Kompilowanie fabryki wdrażania w chmurze

Ponieważ zespół stał się bardziej zaznajomiony z różnymi scenariuszami wdrażania, będzie mógł robić więcej i szybciej pracować. W tej sekcji wskazówek zostanie przyjęta możliwość wdrożenia zespołu na wyższym poziomie.

Podejście do fabryki rozwiązań w chmurze analizuje procesy związane z wdrażaniem. Ze względu na brak interpretacji i wyraźnej komunikacji większość obciążeń związanych z migracją i innowacyjnością pochodzi z dużej ilości spotkań. Wyraźne Definiowanie procesów i interakcji w różnych fazach podróży w chmurze spowoduje usunięcie blokowania kulturowego i politycznego.

**Dostarczane**

- Usprawnij procesy dostarczania, aby utworzyć wysoko zoptymalizowaną fabrykę wdrażania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Wskazówki dotyczące procesu, które obsługują działania związane z [migracją](../../migrate/migration-considerations/index.md) , można znaleźć w sekcji ulepszenia procesu w metodologii migracji.
- W metodologii innowacji wskazówki koncentrują się na [procesach innowacji](../../innovate/considerations/index.md) , które powodują zmniejszenie technologii i wydajniejsze opracowywanie produktów.

**Zespół odpowiedzialny za:**

- Zespół wdrażania w chmurze jest odpowiedzialny za tworzenie procesów, które przyjmują do następnego poziomu.

## <a name="whats-next"></a>Co dalej

Wdrażanie w chmurze to doskonałe rozwiązanie, ale nieregulowane wdrożenie może dawać nieoczekiwane wyniki. Aby przyspieszyć wdrażanie i najlepsze rozwiązania, w miarę zmniejszania ryzyka biznesowego i technicznego należy wyrównać wdrożenie chmury przy użyciu [funkcji zarządzania chmurą](../../organize/cloud-governance.md).

Dostosowanie do zespołu ds. zarządzania chmurą tworzy saldo w ramach wysiłków związanych z wdrażaniem w chmurze, ale jest to uznawane za minimalny produkt żywotny (MVP), ponieważ może on nie być trwały. Każdy zespół ma wiele systemy, jak opisano na [wykresach Raci](../../organize/raci-alignment.md).

Dowiedz się więcej o nadchodzących [antywzorców organizacyjnych: silosach i fiefdoms](../../organize/fiefdoms-silos.md).
