---
title: 'Wprowadzenie: zwiększanie niezawodności przy użyciu odpowiednich kontrolek'
description: Zapoznaj się z podstawą poprawy niezawodności poprzez kontrolki ładu i linię bazową zarządzania.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: c75b7a17c8c2676688f5221ec0e4d0f2ed0641a5
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400216"
---
# <a name="get-started-improve-reliability-with-the-right-controls"></a>Wprowadzenie: zwiększanie niezawodności przy użyciu odpowiednich kontrolek

Jak stosujemy odpowiednie kontrolki w celu zwiększenia niezawodności? Ten przewodnik pomaga zminimalizować zakłócenia związane z niespójnościami w konfiguracji, organizacji zasobów, liniach bazowych zabezpieczeń lub ochronie zasobów. Kroki przedstawione w tym przewodniku pomogą Ci w rozliczeniu niezawodności i kosztów w portfelu IT oraz pomóc zespołowi nadzoru w upewnieniu się, że saldo jest stosowane konsekwentnie. Niezawodność również zależy od innych ról i funkcji. W tym artykule opisano różne funkcje pomocnicze, które ułatwiają tworzenie wyrównania poszczególnych zespołów.

Zarządzanie operacjami i nadzorowanie jest równym partnerom w niezawodności przedsiębiorstwa. Decyzje podjęte w odniesieniu do praktyk operacyjnych ustawiają podstawę dla niezawodności. Metody służące do zarządzania ogólnym środowiskiem zapewniają spójność wszystkich zasobów. Pierwsze dwa kroki w tym przewodniku ułatwiają rozpoczęcie pracy obu zespołów. Gdy są one wymienione sekwencyjnie, następujące kroki mogą postępować równolegle. Kolejne kroki ułatwiają rozpoczęcie pracy w całym przedsiębiorstwie w celu uzyskania bardziej niezawodnych rozwiązań w całym przedsiębiorstwie.

![Wprowadzenie do niezawodności przedsiębiorstwa](../_images/get-started/reliability-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Krok 1. Ustalenie wymagań dotyczących zarządzania operacjami

Wszystkie obciążenia nie są tworzone jako równe. W każdym środowisku istnieją obciążenia, które mają bezpośredni i stały wpływ na działalność firmy. Obsługiwane są również procesy biznesowe i obciążenia, które mają mniejszy wpływ na ogólną firmę. W tym kroku zespół operacyjny w chmurze identyfikuje i implementuje początkowe wymagania w celu obsługi ogólnego portfela IT.

**Dostarczane**

- Zaimplementuj linię bazową zarządzania w celu zdefiniowania standardowych operacji wymaganych dla wszystkich obciążeń produkcyjnych.
- Negocjuj zobowiązania biznesowe z zespołem strategii chmury w celu opracowania planu dla zaawansowanych operacji i wymagań dotyczących odporności.
- Rozwiń swoją linię bazową zarządzania, jeśli do większości obciążeń są wymagane dodatkowe operacje.
- Stosuj zaawansowane wymagania dotyczące operacji, aby przeciążać strefy i zasoby, które obsługują wyższe obciążenia krytyczne.
- Udokumentowanie decyzji dotyczących operacji w portfolio IT w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- **[Linia bazowa zarządzania](../manage/considerations/discipline.md):**

  - [Spis i widoczność](../manage/considerations/inventory.md): [Narzędzia natywne w chmurze](../manage/azure-management-guide/inventory.md) mogą [pomóc zbierać dane](../manage/monitor/data-collection.md), [konfigurować alerty](../manage/monitor/index.md)i implementować [platformę monitorowania](../manage/monitor/index.md) , która najlepiej pasuje do modelu operacyjnego.
  - [Zgodność operacyjna](../manage/considerations/operational-compliance.md): największe wartości procentowe przestoju mogą pochodzić od zmian w konfiguracji zasobów lub słabych praktyk konserwacyjnych. Postępuj zgodnie z [przewodnikiem zarządzania serwerem Azure](../manage/azure-server-management/index.md) , aby zaimplementować narzędzia natywne w chmurze w celu zarządzania poprawkami i zmianami w konfiguracji zasobów.
  - [Ochrona i odzyskiwanie](../manage/considerations/protect.md): awarie są nieuniknione na każdej platformie. Gdy wystąpi zakłócenie, przygotuj się z [rozwiązaniami do tworzenia kopii zapasowych i odzyskiwania](../manage/azure-management-guide/protect-recover.md) , aby zminimalizować czas trwania ewentualnych przerw w działaniu.

- **[Zaawansowane operacje](../manage/design-principles.md):** Użyj planu bazowego zarządzania jako podstawy dla konwersacji związanych z [wyrównaniami biznesowymi](../manage/considerations/business-alignment.md) w celu stworzenia przejrzystości dotyczącej [krytycznego](../manage/considerations/criticality.md), [wpływu na działalność biznesową](../manage/considerations/impact.md)i [zobowiązań związanych z operacjami](../manage/considerations/commitment.md). Wyrównanie biznesowe pozwala określić liczbę i zweryfikować żądania dla [rozszerzonej linii bazowej](../manage/azure-management-guide/enhanced-baseline.md), zarządzania [różnymi platformami technologii](../manage/azure-management-guide/workload-specialization.md)lub [operacji specyficznych dla obciążenia](../manage/azure-management-guide/platform-specialization.md).

- **Zapoznaj się z przeglądem architektury:** Zmiany architektury na poziomie obciążenia mogą być wymagane w celu spełnienia wymagań dotyczących operacji. [Struktura architektury platformy Azure](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) i [Przegląd architektury platformy Azure](https://docs.microsoft.com/assessments?id=azure-architecture-review) mogą pomóc w obciążeniu tych konwersacji z właścicielem technicznym określonego obciążenia.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-consistently-apply-the-management-baseline"></a>Krok 2. spójnie Zastosuj linię bazową zarządzania

Niezawodność przedsiębiorstwa wymaga spójnego zastosowania linii bazowej zarządzania. Taka spójność pochodzi z odpowiednich zasad firmowych, procesów IT i zautomatyzowanych narzędzi do zarządzania implementacją planu bazowego dla wszystkich zasobów, których to dotyczy.

**Dostarczane**

- Upewnij się, że dla wszystkich systemów, których to dotyczy, jest odpowiednia linia bazowa zarządzania.
- Udokumentowanie zasad spójności zasobów, procesów i wskazówek dotyczących projektowania w [szablonie dyscypliny spójności zasobów](../govern/resource-consistency/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa](../ready/azure-best-practices/naming-and-tagging.md) i oznaczania i [wymuszania Konwencji znakowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags), z określonym naciskiem na znaczniki dla "krytyczne".
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustal [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.
- Jeśli jesteś nowym członkiem dyscypliny Cost Management, weź pod uwagę następujące zagadnienia dotyczące ulepszeń w zakresie [zarządzania kosztami](../govern/guides/complex/cost-management-improvement.md). [implementation](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)

> [!NOTE]
> **Kroki prowadzące do rozpoczęcia partnerstwa w niezawodności z innymi zespołami:** Różne decyzje podejmowane przez cały cykl życia w chmurze mogą mieć bezpośredni wpływ na niezawodność. Poniższe kroki ułatwiają zaprojektowanie partnerstwa i wspieranie działań koniecznych do zapewnienia spójnej niezawodności w portfelu IT.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-define-your-strategy"></a>Krok 3. Definiowanie strategii

**Dostarczane**

- Rejestruj motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Upewnij się, że linia bazowa zarządzania zapewnia pomoc techniczną, która jest wyrównana do strategicznego kierunku wdrożenia chmury.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Poznaj motywacje](../strategy/motivations.md): krytyczne zdarzenia biznesowe i niektóre motywacje do migracji mogą być zależne od kosztów, co zwiększa znaczenie kontroli kosztów dla wszystkich kolejnych wysiłków. Inne przeszukiwane motywacje dotyczące innowacji lub wzrostu dzięki migracji mogą być bardziej ukierunkowane na dochody w oparciu o linię górną. Zrozumienie motywacji ułatwia zrozumienie, jak wysoki jest priorytet zarządzania kosztami.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): niektóre wyniki fiskalne mają być wyjątkowo czułe. Gdy żądane wyniki są mapowane na metryki fiskalne, należy zainwestować w Cost Management dyscypliny zarządzania wczesnie.
- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md): uzasadnienie biznesowe służy jako ogólny widok ogólnego planu finansowego na potrzeby wdrażania w chmurze. Może to być dobre źródło dla początkowych nakładów budżetowych.

Strategiczne decyzje mają bezpośredni wpływ na niezawodność, zgrywanie przez cykl życia i długoterminowe operacje. Przejrzystość strategiczna usprawnia wysiłki.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-4-develop-a-cloud-adoption-plan"></a>Krok 4. opracowywanie planu wdrażania chmury

Znak cyfrowy (lub analiza istniejącego portfolio IT) może pomóc w zweryfikowaniu uzasadnienia biznesowego i udostępnieniu rafinowanego widoku ogólnego portfolio IT. Plan wdrożenia zapewnia przejrzystość na osi czasu działań podczas jej wdrażania. Dostosowanie tego planu i analizy elementów cyfrowych zapewniają sposób planowania przyszłych zależności zarządzania operacjami. Zrozumienie planu powoduje także zapraszanie zespołu operacji w chmurze do cykli rozwojowe w celu oszacowania i zaplanowania wszelkich zmian w linii bazowej zarządzania, wymaganych do zapewnienia operacji związanych z obciążeniem.

**Dostarczane**

- Aktualizacja [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) w celu odzwierciedlenia zmian, które są potrzebne do realizacji odpowiedniej strategii. Zarejestrowane zmiany mogą obejmować następujące elementy:
  - Ocena istniejącego podpisu cyfrowego.
  - Plan wdrażania w chmurze odzwierciedlający wymagane zmiany i prace.
  - Zmiana organizacyjna wymagana do dostarczenia planu.
  - Plan odnoszący się do umiejętności, które są potrzebne, aby umożliwić istniejącemu zespołowi pomyślne ukończenie wymaganej pracy.
- Współpraca z zespołem nadzoru w celu wyrównania modeli kosztów i modeli prognoz, w tym wysiłków umożliwiających optymalizację wydatków za pomocą analizy ilościowej.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Zbierz spis](../digital-estate/inventory.md). Ustanów źródło danych do analizy podpisywania cyfrowego przed przyjęciem.
- [Najlepsze rozwiązanie — Azure Migrate](../plan/contoso-migration-assessment.md). Użyj Azure Migrate, aby zebrać spis.
- [Przyrostowa racjonalizacja](../digital-estate/rationalize.md#incremental-rationalization). Podczas przyrostowej racjonalizacji analiza ilościowa może identyfikować kandydatów w chmurze na potrzeby budżetowania.
- [Wyrównaj modele kosztów i modele prognoz](../digital-estate/calculate.md). Użyj Azure Cost Management do wyrównania kosztów i modeli prognoz przez [Tworzenie budżetów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Utwórz plan wdrożenia chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan). Utwórz plan z możliwością działania, zasobami i szczegółami osi czasu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-implement-landing-zone-best-practices"></a>Krok 5. Implementowanie najlepszych rozwiązań dotyczących strefy wyładunkowej

Przygotowana metodologia struktury wdrażania chmury koncentruje się w dużym stopniu na tworzeniu stref wyładunkowych w celu hostowania obciążeń w chmurze. W trakcie implementacji strefy wyładunkowej wiele decyzji może mieć wpływ na operacje. Zapoznaj się z zespołem ds. operacji w chmurze, aby uzyskać informacje na temat zmian w strefie docelowej Zapoznaj się również z zespołem nadzoru chmurowego, aby poznać zasady "spójność zasobów" i wskazówki dotyczące projektowania, które mogą mieć wpływ na projekt strefy docelowej.

**Dostarczane**

- Wdróż co najmniej jedną strefę obciążeniową, która umożliwia hostowanie obciążeń w ramach planu adopcji krótkoterminowej.
- Upewnij się, że wszystkie strefy ładunkowe spełniają decyzje dotyczące operacji i wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-operations.md): najlepsze rozwiązania w zakresie ulepszania operacji w danej strefie docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-complete-waves-of-adoption-effort-and-change"></a>Krok 6. zakończenie wysiłków wdrażania i zmiana

Do długotrwałych operacji mogą wpływać decyzje podejmowane podczas migracji i wysiłków innowacji. Zachowanie spójnego wyrównania w procesach wdrażania pomaga usunąć bariery w wersjach produkcyjnych i ograniczyć nakład pracy potrzebny do dołączenia nowych rozwiązań do praktyk związanych z zarządzaniem.

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

Powyższe kroki ułatwią wdrożenie odpowiednich kontroli i procesów wymaganych do zapewnienia niezawodności w całym przedsiębiorstwie i wszystkich hostowanych zasobach.
