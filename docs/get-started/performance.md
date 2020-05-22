---
title: 'Wprowadzenie: zapewnianie spójnej wydajności w portfolio'
description: Poznaj podstawowe informacje dotyczące zarządzania wydajnością w portfolio, w tym obsługę wydajności, Ustawianie oczekiwań i tworzenie wyrównania organizacyjnego.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 147bce258b57c7f0b7af343cc387bf9da008da4a
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752416"
---
# <a name="get-started-ensure-consistent-performance-across-a-portfolio"></a>Wprowadzenie: zapewnianie spójnej wydajności w portfolio

Jak zapewnić odpowiednią wydajność w portfelu obciążeń? Kroki opisane w tym przewodniku mogą pomóc w ustaleniu procesów w celu utrzymania tego poziomu wydajności.

Wydajność zależy również od innych ról i funkcji. Ten artykuł mapuje te funkcje pomocnicze, które ułatwiają tworzenie wyrównania poszczególnych zespołów.

Scentralizowane zarządzanie operacjami to najczęstsze podejście do spójnej wydajności w portfolio. Decyzje dotyczące praktyk operacyjnych określają linię bazową operacji i wszelkie całościowe ulepszenia.

Pierwszy krok w tym przewodniku pomoże Ci rozpocząć pracę. Kolejne kroki ułatwiają rozpoczęcie pracy w całym przedsiębiorstwie w celu przeprowadzenia przejazdu na wydajność przedsiębiorstwa w całym portfelu obciążeń.

![Wprowadzenie do zarządzania wydajnością w przedsiębiorstwie](../_images/get-started/performance-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Krok 1. Ustalenie wymagań dotyczących zarządzania operacjami

Linia bazowa zarządzania operacjami, pokreślona w strukturze Microsoft Cloud wdrażania dla platformy Azure, udostępnia zestaw kontrolek i natywnych narzędzi do obsługi chmurowej w celu zapewnienia spójnych operacji. Rozszerzanie tego planu bazowego za pomocą narzędzi automatyzacji zapewnia monitorowanie wydajności i automatyzację w celu spełnienia spójnych wymagań dotyczących wydajności w portfolio.

**Dostarczane**

- Zwiększenie planu bazowego zarządzania w celu uwzględnienia automatycznych zadań korygowania związanych z odchyleniami od oczekiwań wydajności.
- Gdy wzorce danych specyficzne dla obciążenia lub zmiany architektury są niezbędne do spełnienia wymagań dotyczących wydajności, należy użyć operacji specyficznych dla obciążenia, aby zapewnić większą kontrolę wydajności.
- Udokumentowanie decyzji operacyjnych w portfolio IT w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx). Należy skoncentrować się na tym, jak decyzje dotyczące automatyzacji wydajności są wymienione w sekcji **zgodność operacyjna** na karcie **linia bazowa** .

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- W artykule [ulepszony wiersz bazowy zarządzania](../manage/azure-management-guide/enhanced-baseline.md) przedstawiono przykłady użycia narzędzi, takich jak Azure Automation, aby dodać usprawnienia związane z wydajnością. Takie podejście może pomóc w utrzymaniu spójnej wydajności poprzez podstawowe modyfikacje rozmiaru i skali dodatkowych zasobów.
- [Operacje specyficzne dla obciążenia](../manage/azure-management-guide/platform-specialization.md) używają dobrze zaprojektowanego przeglądu Microsoft Azure, aby zapewnić wskazówki dotyczące automatyzacji dla określonego obciążenia. To podejście do zarządzania wydajnością jest szczególnie przydatne, gdy dane specyficzne dla obciążenia powinny mieć na celu wykonywanie akcji operacyjnych.
- W powyższych wskazówkach przyjęto założenie, że istniejąca implementacja [linii bazowej zarządzania](../manage/considerations/discipline.md) obsługuje pełen portfel obciążeń.

> [!NOTE]
> Różne decyzje podejmowane przez cały cykl życia w chmurze mogą mieć bezpośredni wpływ na wydajność. Poniższe kroki ułatwiają zarys partnerstwa i wspieranie działań wymaganych do zapewnienia wydajności w portfolio IT.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-consistent-application-of-the-management-baseline"></a>Krok 2. spójna aplikacja planu bazowego zarządzania

W miarę poprawy planu bazowego zarządzania należy się upewnić, że te ulepszenia przeniosą do dyscypliny ładu o spójności zasobów. W ten sposób zapewnimy stosowanie ulepszonej linii bazowej we wszystkich zarządzanych środowiskach.

**Dostarczane**

- Upewnij się, że dla wszystkich systemów, których dotyczy ta ulepszona linia bazowa zarządzania, są odpowiednie.
- Udokumentowanie zasad, procesów i wskazówki dotyczące projektowania spójności zasobów w [szablonie dyscypliny spójności zasobów](../govern/resource-consistency/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa i znakowania](../ready/azure-best-practices/naming-and-tagging.md). [Wymuś konwencje tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags), z konkretnym naciskiem na znaczniki dla "krytyczne".
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustanawiaj [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.
- Jeśli jesteś nowym członkiem dyscypliny ładu Cost Management, weź pod uwagę [artykuł dotyczący ulepszeń w zakresie zarządzania kosztami](../govern/guides/complex/cost-management-improvement.md), z fokusem w sekcji [implementacja](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices) .

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-define-strategy"></a>Krok 3. Definiowanie strategii

Strategiczne decyzje mają bezpośredni wpływ na wydajność, zgrywanie przez cykl życia i długoterminowe operacje. Strategiczna przejrzystość poprawia wydajność w portfolio. To przejrzystość pomaga również zespołowi operacyjnemu zrozumieć, które obciążenia muszą mieć stopień specjalizacji obciążeń i zaawansowane operacje.

**Dostarczane**

- Rejestruj motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Upewnij się, że linia bazowa zarządzania zapewnia pomoc techniczną, która jest wyrównana do strategicznego kierunku wdrożenia chmury.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Poznaj motywacje](../strategy/motivations.md): krytyczne zdarzenia biznesowe i niektóre motywacje do migracji mogą być wrażliwe na koszty, co zwiększa znaczenie kontroli kosztów dla wszystkich późniejszych wysiłków. Inne trendy do przodu dotyczące innowacji lub wzrostu przez proces migracji mogą być bardziej ukierunkowane na dochody w oparciu o linię górną. Zrozumienie motywacji może pomóc w zrozumieniu, jak wysoki jest priorytet zarządzania kosztami.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): niektóre wyniki fiskalne mają być wyjątkowo czułe. Gdy żądane wyniki są mapowane na metryki fiskalne, należy zainwestować w dyscyplinę Cost Management ładu wczesnie.
- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md): uzasadnienie biznesowe służy jako ogólny widok planu finansowego na potrzeby wdrażania w chmurze. Może to być dobre źródło dla początkowych nakładów budżetowych.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-4-assess-and-plan-for-workload-adoption"></a>Krok 4. Ocena i Planowanie wdrażania obciążeń

Znak cyfrowy (lub analiza istniejącego portfolio IT) może pomóc w weryfikacji uzasadnienia biznesowego i udostępnieniu rafinowanego widoku portfolio IT. Plan wdrożenia zapewnia przejrzystość na osi czasu działań podczas jej wdrażania. Dostosowanie tego planu i analizy elementów cyfrowych umożliwiają planowanie przyszłych zależności w usłudze Operations Management.

Zrozumienie planu powoduje także zapraszanie zespołu operacji w chmurze do cyklu programowania. Zespół może następnie oszacować i zaplanować wszelkie zmiany w linii bazowej zarządzania, które są wymagane do zapewnienia operacji obciążeń.

**Dostarczane**

- Aktualizowanie [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) w celu odzwierciedlenia zmian wyzwalanych przez analizę cyfr.
- Pracuj z zespołem ds. operacji w chmurze, aby jasno definiować krytyczne znaczenie i wpływ na działalność biznesową poszczególnych obciążeń w ramach planu wdrożenia w czasie zbliżania i długoterminowego.
- Współpraca z zespołem operacji w chmurze w celu ustanowienia osi czasu na potrzeby gotowości operacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Zbieranie spisu](../digital-estate/inventory.md): Ustanów źródło danych do analizy podpisywania cyfrowego przed przyjęciem.
- [Najlepsze rozwiązanie — Azure Migrate](../plan/contoso-migration-assessment.md): Użyj Azure Migrate do zebrania spisu.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): podczas przyrostowej racjonalizacji należy użyć analizy ilościowej w celu zidentyfikowania kandydatów w chmurze na potrzeby budżetowania.
- [Wyrównaj modele kosztów i modele prognoz](../digital-estate/calculate.md): Użyj Azure Cost Management do rozrównania kosztów i modeli prognoz przez [Tworzenie budżetów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Kompiluj plan wdrożenia chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan): Utwórz plan z możliwością działania, zasobem i szczegółami osi czasu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-expand-the-landing-zones"></a>Krok 5. rozszerzanie stref wyładunkowej

Przygotowana metodologia struktury wdrażania chmury koncentruje się w dużym stopniu na tworzeniu stref wyładunkowych w celu hostowania obciążeń w chmurze. W trakcie implementacji strefy wyładunkowej różne decyzje mogą mieć wpływ na operacje.

Zapoznaj się z zespołem ds. operacji w chmurze, aby uzyskać informacje na temat zmian w strefie docelowej Zapoznaj się również z zespołem nadzoru chmurowego, aby poznać zasady "spójności zasobów" i wskazówki dotyczące projektowania, które mogą mieć wpływ na projekt strefy docelowej.

**Dostarczane**

- Wdróż co najmniej jedną strefę docelową, która umożliwia hostowanie obciążeń w ramach planu adopcji krótkoterminowej.
- Upewnij się, że wszystkie strefy ładunkowe spełniają decyzje dotyczące operacji i wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-operations.md): najlepsze rozwiązania w zakresie ulepszania operacji w ramach strefy docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-adoption"></a>Krok 6. wdrażanie

Działania długoterminowe mogą mieć wpływ decyzje podejmowane podczas migracji i wysiłków innowacji. Wczesne wyrównanie spójne w procesach wdrażania ułatwia usuwanie barier w wersji produkcyjnej. Zmniejsza to również nakład pracy wymagany do dołączania nowych rozwiązań do praktyk związanych z zarządzaniem.

**Dostarczane**

- Przetestuj gotowość operacyjną wdrożeń produkcyjnych przy użyciu zasad spójności zasobów.
- Weryfikuj przestrzeganie wskazówek dotyczących projektowania pod kątem spójności zasobów i wymagań dotyczących operacji.
- Udokumentowanie wszelkich zaawansowanych wymagań dotyczących operacji w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Lista kontrolna gotowości środowiska](../migrate/migration-considerations/prerequisites/planning-checklist.md)
- [Lista kontrolna przed podwyższeniem poziomu](../migrate/migration-considerations/optimize/ready.md)
- [Lista kontrolna wydania produkcyjnego](../migrate/migration-considerations/optimize/promote.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Powyższe kroki ułatwią zaimplementowanie kontroli i procesów w celu zapewnienia wydajności w całym przedsiębiorstwie i wszystkich hostowanych zasobach.
