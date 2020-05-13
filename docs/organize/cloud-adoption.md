---
title: Informacje o funkcjach wdrażania w chmurze
description: Zapoznaj się ze sposobem, w jaki funkcje wdrażania chmury umożliwiają rozwiązanie techniczne, dzięki czemu można odpowiednio personelować zespoły.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: ac8307d3af159f3d6d35ccf2ded55f77786a33d7
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215878"
---
# <a name="cloud-adoption-functions"></a>Funkcje wdrażania chmury

Funkcje wdrażania chmury umożliwiają wdrażanie rozwiązań technicznych w chmurze. Podobnie jak w przypadku każdego projektu IT, osoby dostarczające rzeczywistą służbę będą określać powodzenie. Zespoły udostępniające niezbędne funkcje wdrażania chmury mogą być udostępniane przez wielu ekspertów lub partnerów wdrażających.

Zespoły wdrożeniowe chmury to nowoczesne zespoły zespołów implementacji technicznej lub zespołów projektowych. Jednak charakter chmury może wymagać większej struktury zespołu płynów. Niektóre zespoły koncentrują się wyłącznie na migracji w chmurze, a inne zespoły koncentrują się na innowacjech korzystających z technologii chmurowych. Niektóre zespoły obejmują szeroką wiedzę techniczną wymaganą do ukończenia dużych wysiłków związanych z wdrażaniem, takich jak Pełna migracja centrum danych. Inne zespoły mają ściślejszy zespół techniczny i mogą poruszać się między projektami w celu osiągnięcia określonych celów. Przykładem może być zespół specjalistów ds. platformy danych, który ułatwia konwertowanie maszyn wirtualnych SQL na wystąpienia programu SQL PaaS.

Niezależnie od typu lub liczby zespołów wdrażania w chmurze, funkcje wymagane do wdrożenia chmury są udostępniane przez specjalistów z dziedziny IT, analizy biznesowej lub partnerów implementacji.

W zależności od żądanych wyników firmy, umiejętności potrzebne do zapewnienia pełnej funkcji wdrażania w chmurze mogą obejmować:

- Realizatory infrastruktury
- Inżynierowie DevOps
- Deweloperzy aplikacji
- Analityki danych
- Specjaliści platformy danych lub aplikacji

W celu zapewnienia optymalnej współpracy i wydajności zalecamy, aby zespoły rozwiązań w chmurze miały średni rozmiar zespołu sześciu osób. Zespoły te powinny być samodzielne z perspektywą wykonywania technicznego. Zdecydowanie zalecamy, aby te zespoły obejmowały również wiedzę na temat zarządzania projektami, z głębokiego środowiska Agile, Scrum lub innymi iteracyjnymi modelami. Ten zespół jest najbardziej efektywny, gdy jest zarządzany przy użyciu płaskiej struktury.

## <a name="preparation"></a>Przygotowanie

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

Podstawową potrzebą funkcji wdrażania w chmurze jest czasochłonna, wysoka jakość rozwiązań technicznych, które opisano w planie wdrażania. Rozwiązania te powinny być zgodne z wymaganiami dotyczącymi zarządzania i rezultatami biznesowymi, a także korzystać z technologii, narzędzi i rozwiązań automatyzacji dostępnych dla zespołu.

**Zadania wczesnego planowania:**

- Wykonaj [racjonalizację podpisu cyfrowego](../digital-estate/index.md).
- Przejrzyj, zweryfikuj i przejdź do [zaległości migracji z priorytetami](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Rozpocznij wykonywanie [pierwszego obciążenia](../digital-estate/rationalize.md#select-the-first-workload) jako okazję do uczenia się.

**Trwające miesięczne zadania:**

- Nadzorowanie [procesów zarządzania zmianami](../migrate/migration-considerations/prerequisites/technical-complexity.md).
- Zarządzanie [zaległościami wersji i przebiegu](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Kompiluj i obsługuj przyjętą strefę docelową w połączeniu z wymaganiami dotyczącymi zarządzania.
- Wykonaj zadania techniczne opisane w [zaległościach przebiegu](../migrate/migration-considerations/assess/release-iteration-backlog.md).

**Erze spotkania:**

Firma Microsoft zaleca, aby zespoły zapewniające funkcje wdrażania chmury były przeznaczone do pracy w pełnym czasie.

Najlepiej, jeśli te zespoły spotykają się codziennie w sposób samodzielny. Celem codziennych spotkań jest szybkie aktualizowanie zaległości i komunikowanie się, co zostało zakończone, co należy zrobić dzisiaj i jakie elementy są blokowane, wymagając dodatkowej obsługi zewnętrznej.

Harmonogramy wydań i czasy trwania iteracji są unikatowe dla każdej firmy. Jednak zakres od jednego do czterech tygodni na iterację wygląda na średni czas trwania. Bez względu na iterację lub wydanie erze zaleca się, aby zespół zaspokajał wszystkie zespoły pomocnicze na końcu każdej wersji, aby komunikować się z wynikami wydania i zmieniać priorytet nadchodzących wysiłków. Podobnie jest cenny do zaspokajania jako zespół na końcu każdego przebiegu, z centrum w chmurze doskonałości lub zespołem nadzoru w chmurze, aby zachować zgodność z typowymi działaniami i wszelkimi potrzebami pomocy technicznej.

Niektóre z zadań technicznych związanych z wdrażaniem w chmurze mogą stać się powtarzane. Członkowie zespołu powinni obrócić co 3 &ndash; miesiące, aby uniknąć problemów z zadowoleniem pracowników i zachować odpowiednie umiejętności. Obracanie stanowiska w centrum rozwiązań w chmurze doskonałości lub zespołu nadzoru chmurowego może zapewnić doskonałą okazję, aby pracownicy mogli korzystać z nowych innowacji.

Dowiedz się więcej na temat funkcji [centrum w chmurze doskonałości](./cloud-center-of-excellence.md) lub [zespołu](./cloud-governance.md)nadzoru w chmurze.

## <a name="next-steps"></a>Następne kroki

- [Tworzenie zespołu wdrażania w chmurze](../get-started/team/cloud-adoption.md)
- Wyrównaj działania związane z wdrażaniem w chmurze dzięki [funkcjom ładu w chmurze](./cloud-governance.md) , aby przyspieszyć wdrażanie i zaimplementować najlepsze rozwiązania, jednocześnie zmniejszając ryzyko biznesowe i techniczne.
