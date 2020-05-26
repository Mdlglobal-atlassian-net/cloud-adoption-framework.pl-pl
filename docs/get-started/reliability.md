---
title: 'Wprowadzenie: zwiększanie niezawodności przy użyciu odpowiednich kontrolek'
description: Zapoznaj się z podstawą poprawy niezawodności poprzez kontrolki ładu i linię bazową zarządzania.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 0f7ae79bbcc9fb4c02a0c9e731d2e826f4682138
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814821"
---
# <a name="get-started-improve-reliability-with-the-right-controls"></a>Wprowadzenie: zwiększanie niezawodności przy użyciu odpowiednich kontrolek

Jak zastosować odpowiednie kontrolki w celu zwiększenia niezawodności? Ten artykuł pomaga zminimalizować zakłócenia związane z:

- Niespójności w konfiguracji.
- Organizacja zasobów.
- Linie bazowe zabezpieczeń.
- Ochrona zasobów.

Kroki opisane w tym artykule ułatwiają zespołowi operacyjnemu zrównoważenie niezawodności i kosztów w portfelu IT. Ten artykuł pomaga również zespołowi nadzoru w zapewnianiu spójnego stosowania bilansu. Niezawodność również zależy od innych ról i funkcji. W tym artykule opisano funkcje pomocnicze, które ułatwiają tworzenie wyrównania wśród poszczególnych zespołów.

Zarządzanie operacjami i nadzorowanie jest równym partnerom w niezawodności przedsiębiorstwa. Decyzje podejmowane w sprawie praktyk operacyjnych ustawiają podstawę dla niezawodności. Metody służące do zarządzania ogólnym środowiskiem zapewniają spójność wszystkich zasobów.

Pierwsze dwa kroki w tym artykule ułatwiają rozpoczęcie pracy obu zespołów. Są one wyświetlane sekwencyjnie, ale można je wykonywać równolegle. Kolejne kroki ułatwiają rozpoczęcie pracy w całym przedsiębiorstwie w celu uzyskania bardziej niezawodnych rozwiązań w całym przedsiębiorstwie.

![Wprowadzenie do niezawodności przedsiębiorstwa](../_images/get-started/reliability-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Krok 1. Ustalenie wymagań dotyczących zarządzania operacjami

Nie wszystkie obciążenia są tworzone jako równe. W każdym środowisku istnieją obciążenia, które mają bezpośredni i stały wpływ na działalność firmy. Obsługiwane są również procesy biznesowe i obciążenia, które mają mniejszy wpływ na ogólną firmę. W tym kroku zespół operacyjny w chmurze identyfikuje i implementuje początkowe wymagania w celu obsługi ogólnego portfela IT.

**Dostarczane**

- Zaimplementuj linię bazową zarządzania, aby zdefiniować standardowe operacje, które są wymagane dla wszystkich obciążeń produkcyjnych.
- Negocjuj zobowiązania biznesowe z zespołem strategii chmury w celu opracowania planu dla zaawansowanych operacji i wymagań dotyczących odporności.
- Rozwiń swoją linię bazową zarządzania, jeśli do większości obciążeń są wymagane dodatkowe operacje.
- Stosuj zaawansowane wymagania dotyczące operacji, aby przeciążać strefy i zasoby, które obsługują te, które są najbardziej krytyczne.
- Udokumentowanie decyzji dotyczących operacji w portfolio IT w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Linia bazowa zarządzania](../manage/considerations/discipline.md):

  - [Spis i widoczność](../manage/considerations/inventory.md): [Narzędzia natywne w chmurze](../manage/azure-management-guide/inventory.md) mogą pomóc [zbierać dane](../manage/monitor/data-collection.md) i [konfigurować alerty](../manage/monitor/index.md). Narzędzia te mogą również ułatwić implementację [platformy monitorowania](../manage/monitor/index.md) , która najlepiej pasuje do Twojego modelu operacyjnego.
  - [Zgodność operacyjna](../manage/considerations/operational-compliance.md): największe wartości procentowe przestoju mogą pochodzić od zmian w konfiguracji zasobów lub słabych praktyk konserwacyjnych. Postępuj zgodnie z [przewodnikiem zarządzania serwerem Azure](../manage/azure-server-management/index.md) , aby zaimplementować narzędzia natywne w chmurze do zarządzania poprawkami i zmianami w konfiguracji zasobów.
  - [Ochrona i odzyskiwanie](../manage/considerations/protect.md): awarie są nieuniknione na każdej platformie. Gdy wystąpi zakłócenie, przygotuj się z [rozwiązaniami do tworzenia kopii zapasowych i odzyskiwania](../manage/azure-management-guide/protect-recover.md) , aby zminimalizować czas trwania.
- [Zaawansowane operacje](../manage/design-principles.md): Użyj planu bazowego zarządzania jako podstawy dla konwersacji [wyrównania Twojej firmy](../manage/considerations/business-alignment.md) . Pomaga to jasno omówić [krytyczne](../manage/considerations/criticality.md), [wpływ na działalność biznesową](../manage/considerations/impact.md)i [zobowiązania operacyjne](../manage/considerations/commitment.md). Wyrównanie biznesowe pozwala określić liczbę i zweryfikować żądania dla [rozszerzonej linii bazowej](../manage/azure-management-guide/enhanced-baseline.md), zarządzania [różnymi platformami technologii](../manage/azure-management-guide/workload-specialization.md)lub [operacji specyficznych dla obciążenia](../manage/azure-management-guide/platform-specialization.md).
- **Zapoznaj się z przeglądem architektury:** Zmiany architektury na poziomie obciążenia mogą być wymagane w celu spełnienia wymagań dotyczących operacji. [Microsoft Azure dobrze zaprojektowanej struktury](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) i [Microsoft Azure udokumentowane przeglądy](https://docs.microsoft.com/assessments?id=azure-architecture-review) mogą pomóc w wykonywaniu tych rozmów przez właściciela technicznego określonego obciążenia.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-consistently-apply-the-management-baseline"></a>Krok 2. spójnie Zastosuj linię bazową zarządzania

Niezawodność przedsiębiorstwa wymaga spójnego zastosowania linii bazowej zarządzania. Taka spójność pochodzi z odpowiednich zasad firmowych, procesów IT i narzędzi automatycznych. Te zasoby określają implementację linii bazowej zarządzania dla wszystkich zasobów, których to dotyczy.

**Dostarczane**

- Upewnij się, że dla wszystkich systemów, których to dotyczy, jest odpowiednia linia bazowa zarządzania.
- Udokumentowanie zasad spójności zasobów, procesów i wskazówek dotyczących projektowania w [szablonie dyscypliny spójności zasobów](../govern/resource-consistency/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa i znakowania](../ready/azure-best-practices/naming-and-tagging.md). [Wymuś konwencje tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags), z określonym akcentem w przypadku tagów o krytycznym znaczeniu.
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustanawiaj [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.
- Jeśli dopiero zaczynasz Cost Management dyscypliny, postępuj zgodnie ze wskazówkami zawartymi w artykule ulepszenia w zakresie [zarządzania kosztami](../govern/guides/complex/cost-management-improvement.md) . Skup się na sekcji [implementacji](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices) .

> [!NOTE]
> **Kroki prowadzące do rozpoczęcia partnerstwa w niezawodności z innymi zespołami:** Różne decyzje podejmowane przez cały cykl życia w chmurze mogą mieć bezpośredni wpływ na niezawodność. Poniższe kroki przedstawiają partnerstwo i wspierają wysiłki wymagane do zapewnienia spójnej niezawodności w portfolio IT.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-define-your-strategy"></a>Krok 3. Definiowanie strategii

Decyzje strategiczne mają bezpośredni wpływ na niezawodność. Umożliwiają one przechodzenie przez cykl życia i wykonywanie długoterminowych operacji. Przejrzystość strategiczna usprawnia wysiłki.

**Dostarczane**

- Rejestruj motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Upewnij się, że linia bazowa zarządzania zapewnia pomoc techniczną, która jest wyrównana do strategicznego kierunku wdrożenia chmury.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Poznaj motywacje](../strategy/motivations.md): krytyczne zdarzenia biznesowe i niektóre motywacje do migracji są zależne od kosztów. Obszary te mogą zwiększyć znaczenie kontroli kosztu dla wszystkich późniejszych wysiłków. Inne trendy do przodu dotyczące innowacji lub wzrostu przez proces migracji mogą być bardziej ukierunkowane na dochody w oparciu o linię górną. Zrozumienie motywacji pomaga określić priorytety zarządzania kosztami.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): niektóre wyniki fiskalne mają być wyjątkowo czułe. Gdy żądane wyniki są mapowane na metryki fiskalne, należy zainwestować na wczesne dyscypliny ładu Cost Management.
- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md): uzasadnienie biznesowe służy jako ogólny widok ogólnego planu finansowego na potrzeby wdrażania w chmurze. Może to być dobre źródło dla początkowych nakładów budżetowych.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-4-develop-a-cloud-adoption-plan"></a>Krok 4. opracowywanie planu wdrażania chmury

Digital (lub analiza istniejącego portfolio IT) może pomóc w sprawdzeniu uzasadnienia biznesowego. Może ona zapewnić elegancję widok całości portfolio IT. Plan wdrożenia zapewnia przejrzystość na osi czasu działań podczas jej wdrażania.

W przypadku wyrównania planu wdrożenia z analizą elementów cyfrowych można zaplanować przyszłe zależności zarządzania operacjami. Zrozumienie planu przyjęcia powoduje również zaproszenie zespołu operacji w chmurze do cykli programistycznych. Mogą oni szacować i planować wszelkie zmiany w linii bazowej zarządzania, które są wymagane do zapewnienia operacji obciążeń.

**Dostarczane**

- Aktualizacja [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) w celu odzwierciedlenia zmian, które są potrzebne do osiągnięcia odpowiedniej strategii. Zarejestrowane zmiany mogą obejmować:

  - Ocena istniejącego podpisu cyfrowego.
  - Plan wdrażania chmury, który odzwierciedla wymagane zmiany i prace.
  - Zmiana organizacyjna wymagana do dostarczenia planu.
  - Plan odnoszący się do umiejętności, które są potrzebne, aby umożliwić istniejącemu zespołowi pomyślne ukończenie wymaganej pracy.
- Pracuj z zespołem nadzoru, aby wyrównać modele kosztów i modele prognoz. Ten proces obejmuje wysiłki w celu optymalizacji wydatków dzięki analizie ilościowej.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Zbieranie spisu](../digital-estate/inventory.md): Ustanów źródło danych do analizy podpisywania cyfrowego przed przyjęciem.
- [Najlepsze rozwiązania — Azure Migrate](../plan/contoso-migration-assessment.md): Użyj Azure Migrate do zebrania spisu.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): podczas przyrostowej racjonalizacji analiza ilościowa może identyfikować kandydatów w chmurze na potrzeby budżetowania.
- [Wyrównaj modele kosztów i modele prognoz](../digital-estate/calculate.md): Użyj Azure Cost Management do rozrównania kosztów i modeli prognoz przez [Tworzenie budżetów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Kompiluj plan wdrażania chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan): Utwórz plan z możliwością działania, zasobami i szczegółami osi czasu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-implement-landing-zone-best-practices"></a>Krok 5. Implementowanie najlepszych rozwiązań dotyczących strefy wyładunkowej

Gotowa metodologia wdrożenia chmury dla platformy Azure jest w dużym stopniu ukierunkowana na rozwój stref wypełniania na potrzeby obsługi obciążeń w chmurze. W trakcie implementacji strefy wyładunkowej wiele decyzji może mieć wpływ na operacje. Zapoznaj się z zespołem ds. operacji w chmurze, aby uzyskać informacje na temat zmian w strefie docelowej Zapoznaj się również z zespołem nadzoru chmurowego, aby poznać zasady spójności zasobów i wskazówki dotyczące projektowania, które mogą mieć wpływ na projekt strefy docelowej.

**Dostarczane**

- Wdróż co najmniej jedną strefę wypełniania, która umożliwia hostowanie obciążeń w ramach planu adopcji krótkoterminowej.
- Upewnij się, że wszystkie strefy ładunkowe spełniają decyzje dotyczące operacji i wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-operations.md): najlepsze rozwiązania w zakresie ulepszania operacji w danej strefie docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-complete-waves-of-adoption-effort-and-change"></a>Krok 6. zakończenie wysiłków wdrażania i zmiana

Do długotrwałych operacji mogą wpływać decyzje podejmowane podczas migracji i wysiłków innowacji. Wczesne wyrównanie spójne w procesach wdrażania pomaga usunąć bariery dla wydań produkcyjnych. Zmniejsza to również nakład pracy, który jest wymagany do wprowadzenia nowych rozwiązań do praktyk związanych z zarządzaniem.

**Dostarczane**

- Przetestuj gotowość operacyjną wdrożeń produkcyjnych przy użyciu zasad spójności zasobów.
- Weryfikuj przestrzeganie wymagań dotyczących projektowania spójności zasobów i działań.
- Udokumentowanie wszelkich zaawansowanych wymagań dotyczących operacji w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Lista kontrolna gotowości środowiska](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [Lista kontrolna przed podwyższeniem poziomu](../migrate/migration-considerations/optimize/ready.md)
- [Lista kontrolna wydania produkcyjnego](../migrate/migration-considerations/optimize/promote.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Te kroki ułatwiają zaimplementowanie kontrolek i procesów, które są potrzebne w celu zapewnienia niezawodności w całym przedsiębiorstwie i wszystkich hostowanych zasobach.
