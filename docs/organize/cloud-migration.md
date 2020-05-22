---
title: Omówienie funkcji migracji do chmury
description: Zrozumienie funkcji migracji do chmury.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: a5b3caa04e3f87c30236425aff770e82e0a37b4c
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755582"
---
# <a name="cloud-migration-functions"></a>Funkcje migracji w chmurze

Zespoły migracji w chmurze to nowoczesne zespoły zespołów implementacji technicznej lub zespołów projektowych. Jednak charakter chmury może wymagać większej struktury zespołu płynów. Niektóre zespoły migracji koncentrują się wyłącznie na migracji w chmurze, a inne koncentrują się na innowacjech korzystających z technologii chmurowych. Niektóre z nich obejmują szeroką wiedzę techniczną, która jest wymagana do ukończenia dużych wysiłków związanych z wdrażaniem, takich jak Pełna migracja centrów danych, a inne mają ściślejszy fokus techniczny i mogą poruszać się między projektami w celu osiągnięcia określonych celów, na przykład zespołu specjalistów ds. technologii, którzy ułatwiają konwertowanie maszyn wirtualnych SQL na wystąpienia usługi SQL PaaS.

Bez względu na typ lub liczbę zespołów migracji w chmurze, te zespoły zwykle udostępniają wiedzę z dziedziny dla INFORMATYKów, analizy biznesowej lub partnerów implementacji.

## <a name="prerequisites"></a>Wymagania wstępne

- [Utwórz konto platformy Azure](https://docs.microsoft.com/learn/modules/create-an-azure-account): pierwszy krok korzystania z platformy Azure to utworzenie konta.
- [Azure Portal](https://docs.microsoft.com/learn/modules/tour-azure-portal): Zapoznaj się z Azure Portal funkcjami i usługami oraz Dostosuj Portal.
- [Wprowadzenie do platformy Azure](https://docs.microsoft.com/learn/modules/welcome-to-azure): Rozpoczynanie pracy z platformą Azure. Utwórz i skonfiguruj pierwszą maszynę wirtualną w chmurze.
- [Podstawy platformy Azure](https://docs.microsoft.com/learn/paths/azure-for-the-data-engineer): Poznaj koncepcje chmury, Poznaj zalety, Porównaj i Odróżnij podstawowe strategie oraz Poznaj zakres usług dostępnych na platformie Azure.
- Zapoznaj się z [metodologią migrowania](../migrate/index.md).

## <a name="minimum-scope"></a>Zakres minimalny

Jądrem wszystkich działań związanych z wdrażaniem w chmurze jest zespół migracji w chmurze. Ten zespół udostępnia zmiany techniczne, które umożliwiają wdrażanie. W zależności od celów nakładu pracy ten zespół może obejmować różnorodną gamę członków zespołu, którzy obsługują szeroki zestaw zadań technicznych i służbowych.

Zakres zespołu obejmuje co najmniej:

- [Racjonalizacja podpisu cyfrowego](../digital-estate/index.md)
- Przeglądanie, sprawdzanie poprawności i [przenoszenie zaległości migracji z priorytetami](../migrate/migration-considerations/assess/release-iteration-backlog.md)
- Wykonywanie [pierwszego obciążenia](../digital-estate/rationalize.md#select-the-first-workload) jako możliwości uczenia się.

## <a name="deliverable"></a>Dostarcza

Podstawowy element dostarczany z dowolnego zespołu migracji w chmurze to termin, wysoka jakość rozwiązań technicznych, które zostały opisane w planie wdrożenia, zgodnie z wymaganiami dotyczącymi zarządzania i rezultatami biznesowymi przy użyciu technologii, narzędzi i dostępnych rozwiązań do automatyzacji.

### <a name="ongoing-monthly-tasks"></a>Trwające miesięczne zadania

- Nadzorowanie [procesów zarządzania zmianami](../migrate/migration-considerations/prerequisites/technical-complexity.md).
- Zarządzanie [zaległościami wersji i przebiegu](../migrate/migration-considerations/assess/release-iteration-backlog.md)
- Kompiluj i obsługuj przyjętą strefę docelową w połączeniu z wymaganiami dotyczącymi zarządzania.
- Wykonaj zadania techniczne opisane w [zaległościach przebiegu](../migrate/migration-considerations/assess/release-iteration-backlog.md).

### <a name="team-cadence"></a>Erze zespołu

Firma Microsoft zaleca, aby zespoły zapewniające możliwość wdrażania chmury były przeznaczone do pracy w czasie pełnym.

Najlepiej, jeśli te zespoły spotykają się codziennie w sposób samodzielny. Celem codziennych spotkań jest szybkie aktualizowanie zaległości i komunikowanie się, co zostało zakończone, co należy zrobić dzisiaj i jakie elementy są blokowane, wymagając dodatkowej obsługi zewnętrznej.

Harmonogramy wydań i czasy trwania iteracji są unikatowe dla każdej firmy. Jednak zakres od jednego do czterech tygodni na iterację jest równy średniemu czasowi trwania. Bez względu na iterację lub wydanie erze zaleca się, aby zespół zaspokajał wszystkie zespoły pomocnicze na końcu każdej wersji, aby komunikować się z wynikami wydania i zmieniać priorytet nadchodzących wysiłków. Jest również cenny do zaspokajania jako zespół na końcu każdego przebiegu, z centrum w [chmurze doskonałości](../organize/cloud-center-of-excellence.md) lub [zespołem](./cloud-governance.md) nadzoru w chmurze, aby zachować zgodność z typowymi wysiłkami i potrzebami pomocy technicznej.

Niektóre z zadań technicznych związanych z wdrażaniem w chmurze mogą stać się powtarzane. Członkowie zespołu powinni obrócić co 3 &ndash; miesiące, aby uniknąć problemów z zadowoleniem pracowników i zachować odpowiednie umiejętności. Rotacyjna siedziba w centrum rozwiązań w [chmurze doskonałości](../organize/cloud-center-of-excellence.md) lub [zespołu nadzoru chmurowego](./cloud-governance.md) może zapewnić doskonałą okazję, aby pracownicy mogli korzystać z nowych innowacji.

## <a name="baseline-capability"></a>Możliwość linii bazowej

W zależności od żądanych wyników działalności biznesowej wymagane jest, aby zapewnić możliwość korzystania z pełnych możliwości wdrażania chmury:

- Realizatory infrastruktury
- Inżynierowie DevOps
- Deweloperzy aplikacji
- Analityki danych
- Specjaliści platformy danych lub aplikacji

W celu zapewnienia optymalnej współpracy i wydajności zalecamy, aby zespoły rozwiązań w chmurze miały średni rozmiar zespołu sześciu osób. Zespoły te powinny być samodzielne z perspektywą wykonywania technicznego. Zdecydowanie zalecamy, aby te zespoły obejmowały również wiedzę na temat zarządzania projektami, z głębokiego środowiska Agile, Scrum lub innymi iteracyjnymi modelami. Ten zespół jest najbardziej efektywny, gdy jest zarządzany przy użyciu płaskiej struktury.

## <a name="out-of-scope"></a>Poza zakresem

Może być konieczne dodatkowe wsparcie z istniejących pracowników działu IT. Może to być cenny współautor do wdrożenia w chmurze przez przeprowadzeniem brokera w chmurze i partnera na potrzeby innowacji i elastyczność biznesową.

- [Centralne obowiązki IT](../organize/central-it.md)

## <a name="whats-next"></a>Co dalej

Przyjęcie jest doskonałe, ale nieregulowane wdrożenie może dawać nieoczekiwane wyniki. Wyrównaj do [zespołu ds. ładu w chmurze](./cloud-governance.md) , aby przyspieszyć wdrażanie i najlepsze rozwiązania, jednocześnie zmniejszając ryzyko biznesowe i techniczne.

Te dwa zespoły tworzą saldo w ramach wysiłków związanych z wdrażaniem w chmurze, ale są uznawane za MVP, ponieważ mogą nie być trwałe. Każdy zespół ma wiele systemyów, jak przedstawiono na [wykresach *odpowiedzialnych* ](../organize/raci-alignment.md), do których można się skontaktować.

Dowiedz się więcej na temat [antywzorców organizacyjnych: silosów i fiefdoms](../organize/fiefdoms-silos.md).
