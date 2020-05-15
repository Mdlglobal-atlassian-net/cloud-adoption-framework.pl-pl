---
title: 'Wprowadzenie: zapewnianie spójnej wydajności w portfolio'
description: Poznaj podstawowe informacje dotyczące zarządzania wydajnością w portfolio, w tym ustanawianie procesów do obsługi wydajności, Ustawianie oczekiwań wydajności i tworzenie wyrównania w całej organizacji.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 845574b9b7e045869561f43745a23ec104893d1f
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400199"
---
# <a name="get-started-ensure-consistent-performance-across-a-portfolio"></a>Wprowadzenie: zapewnianie spójnej wydajności w portfolio

Jak zapewnić odpowiednią wydajność w portfelu obciążeń? Ten przewodnik może pomóc w ustaleniu procesów związanych z utrzymywaniem wydajności w całym przedsiębiorstwie. Kroki opisane w tym miejscu mogą pomóc zespołowi operacyjnemu zapewnić spójne oczekiwania wydajności dla wszystkich obciążeń. Wydajność zależy również od innych ról i funkcji. Ten artykuł mapuje te funkcje pomocnicze, które ułatwiają tworzenie wyrównania poszczególnych zespołów.

Scentralizowane zarządzanie operacjami to najczęstsze podejście do spójnej wydajności w portfolio. Decyzje podjęte w odniesieniu do praktyk operacyjnych definiują linię bazową operacji i wszelkie całościowe ulepszenia. Pierwszy krok w tym przewodniku pomoże Ci rozpocząć pracę. Kolejne kroki ułatwiają rozpoczęcie pracy w całym przedsiębiorstwie na potrzeby wspólnej podróży do wydajności przedsiębiorstwa w całym portfolio obciążeń.

![Wprowadzenie do zarządzania wydajnością w przedsiębiorstwie](../_images/get-started/performance-map.png)

## <a name="step-1-establish-operations-management-requirements"></a>Krok 1. Ustalenie wymagań dotyczących zarządzania operacjami

Linia bazowa zarządzania operacjami, pokreślona w strukturze wdrażania chmury, udostępnia zestaw kontrolek i natywnych narzędzi do obsługi chmurowej w celu zapewnienia spójnych operacji. Rozszerzanie tej linii bazowej przy użyciu narzędzi automatyzacji zapewnia monitorowanie wydajności i automatyzację wymaganą do spełnienia spójnych wymagań w zakresie wydajności w ramach portfolio.

**Dostarczane**

- Zwiększenie planu bazowego zarządzania w celu uwzględnienia automatycznych zadań korygowania związanych z odchyleniami od oczekiwań wydajności.
- Gdy wymagane są wzorce danych dotyczące obciążeń lub zmiany architektury w celu spełnienia wymagań dotyczących wydajności, operacje specyficzne dla obciążenia mogą zapewnić większą kontrolę wydajności.
- Udokumentowanie decyzji operacyjnych w całym portfolio IT w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) z uwzględnieniem decyzji dotyczących automatyzacji wydajności w sekcji "zgodność operacyjna" karty "linia bazowa".

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- W artykule [ulepszony plan bazowy zarządzania](../manage/azure-management-guide/enhanced-baseline.md) przedstawiono przykłady użycia narzędzi, takich jak Azure Automation, aby dodać usprawnienia związane z wydajnością. Takie podejście może pomóc w utrzymaniu spójnej wydajności poprzez podstawowe modyfikacje rozmiaru i skali dodatkowych zasobów.
- [Operacje związane z obciążeniem](../manage/azure-management-guide/platform-specialization.md) wykorzystują Przegląd architektury platformy Azure, aby zapewnić wskazówki dotyczące automatyzacji dla określonego obciążenia. To podejście do zarządzania wydajnością jest szczególnie przydatne, gdy działania operacyjne powinny być prowadzone przez dane specyficzne dla obciążenia.
- W powyższych wskazówkach przyjęto założenie, że istnieje implementacja [planu bazowego zarządzania](../manage/considerations/discipline.md) w celu obsługi pełnego portfolio obciążeń.

> [!NOTE]
> **Kroki umożliwiające rozwyrównywanie oczekiwań wydajności w organizacji:** Różne decyzje podejmowane przez cały cykl życia w chmurze mogą mieć bezpośredni wpływ na wydajność. Poniższe kroki ułatwiają zarys partnerstwa i wspieranie działań wymaganych do zapewnienia wydajności w portfolio IT.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-consistent-application-of-the-management-baseline"></a>Krok 2. spójna aplikacja planu bazowego zarządzania

W miarę poprawy planu bazowego zarządzania ważne jest, aby zapewnić, że te udoskonalenia przeniosą do dyscypliny spójności zasobów w zakresie zarządzania chmurą. W ten sposób zapewnimy stosowanie ulepszonej linii bazowej we wszystkich zarządzanych środowiskach.

**Dostarczane**

- Upewnij się, że dla wszystkich systemów, których dotyczy ta ulepszona linia bazowa zarządzania, są odpowiednie.
- Udokumentowanie zasad spójności zasobów, procesów i wskazówek dotyczących projektowania w [szablonie dyscypliny spójności zasobów](../govern/resource-consistency/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa](../ready/azure-best-practices/naming-and-tagging.md) i oznaczania i [wymuszania Konwencji tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) z określonym naciskiem na znaczniki dla "krytyczne".
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustal [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.
- Jeśli jesteś nowym członkiem dyscypliny Cost Management, weź pod uwagę następujące zagadnienia dotyczące ulepszeń w zakresie [zarządzania kosztami](../govern/guides/complex/cost-management-improvement.md). [implementation](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-define-strategy"></a>Krok 3. Definiowanie strategii

Strategiczne decyzje mają bezpośredni wpływ na wydajność, zgrywanie przez cykl życia i długoterminowe operacje. Strategiczna przejrzystość poprawia wydajność w portfolio. To przejrzystość pomaga również zespołowi operacyjnemu zrozumieć, które obciążenia wymagają stopnia specjalizacji obciążeń i zaawansowanych operacji.

**Dostarczane**

- Rejestruj motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Upewnij się, że linia bazowa zarządzania zapewnia pomoc techniczną, która jest wyrównana do strategicznego kierunku wdrożenia chmury.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Poznaj motywacje](../strategy/motivations.md): krytyczne zdarzenia biznesowe i niektóre motywacje do migracji mogą być zależne od kosztów, co zwiększa znaczenie kontroli kosztów dla wszystkich kolejnych wysiłków. Inne przeszukiwane motywacje dotyczące innowacji lub wzrostu dzięki migracji mogą być bardziej ukierunkowane na dochody w oparciu o linię górną. Zrozumienie motywacji może pomóc w zrozumieniu, jak wysoki jest priorytet zarządzania kosztami.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): niektóre wyniki fiskalne mają być wyjątkowo czułe. Gdy żądane wyniki są mapowane na metryki fiskalne, należy zainwestować w Cost Management dyscypliny zarządzania wczesnie.
- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md): uzasadnienie biznesowe służy jako ogólny widok ogólnego planu finansowego na potrzeby wdrażania w chmurze. Może to być dobre źródło dla początkowych nakładów budżetowych.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-4-assess-and-plan-for-workload-adoption"></a>Krok 4. Ocena i Planowanie wdrażania obciążeń

Znak cyfrowy (lub analiza istniejącego portfolio IT) może pomóc w zweryfikowaniu uzasadnienia biznesowego i udostępnieniu rafinowanego widoku ogólnego portfolio IT. Plan wdrożenia zapewnia przejrzystość na osi czasu działań podczas jej wdrażania. Dostosowanie tego planu i analizy elementów cyfrowych zapewniają sposób planowania przyszłych zależności zarządzania operacjami. Zrozumienie planu powoduje także zapraszanie zespołu operacji w chmurze do cykli rozwojowe w celu oszacowania i zaplanowania wszelkich zmian w linii bazowej zarządzania, wymaganych do zapewnienia operacji związanych z obciążeniem.

**Dostarczane**

- Aktualizowanie [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) w celu odzwierciedlenia zmian wyzwalanych przez analizę cyfr.
- Pracuj z zespołem ds. operacji w chmurze, aby jasno definiować krytyczne znaczenie i wpływ na działalność biznesową poszczególnych obciążeń w ramach planu wdrożenia w czasie zbliżania i długoterminowego.
- Współpraca z zespołem operacji w chmurze w celu ustanowienia osi czasu na potrzeby gotowości operacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Zbieranie spisu](../digital-estate/inventory.md): Ustanów źródło danych do analizy podpisywania cyfrowego przed przyjęciem.
- [Najlepsze rozwiązanie — Azure Migrate](../plan/contoso-migration-assessment.md): Użyj Azure Migrate do zebrania spisu.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): podczas przyrostowej racjonalizacji analiza ilościowa może identyfikować kandydatów w chmurze na potrzeby budżetowania.
- [Wyrównaj modele kosztów i modele prognoz](../digital-estate/calculate.md): Użyj Azure Cost Management do rozrównania kosztów i modeli prognoz przez [Tworzenie budżetów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Kompiluj plan wdrażania chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan): Utwórz plan z możliwością działania, zasobami i szczegółami osi czasu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-expand-the-landing-zones"></a>Krok 5. rozszerzanie stref wyładunkowej

Przygotowana metodologia struktury wdrażania chmury koncentruje się w dużym stopniu na tworzeniu stref wyładunkowych w celu hostowania obciążeń w chmurze. W trakcie implementacji strefy wyładunkowej różne decyzje, które mogą mieć wpływ na operacje. Zapoznaj się z zespołem ds. operacji w chmurze, aby uzyskać informacje na temat zmian w strefie docelowej Zapoznaj się również z zespołem nadzoru chmurowego, aby poznać zasady "spójności zasobów" i wskazówki dotyczące projektowania, które mogą mieć wpływ na projekt strefy docelowej.

**Dostarczane**

- Wdróż co najmniej jedną strefę docelową, która może obsługiwać obciążenia w ramach planu adopcji krótkoterminowej.
- Upewnij się, że wszystkie strefy ładunkowe spełniają decyzje dotyczące operacji i wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-operations.md): najlepsze rozwiązania w zakresie ulepszania operacji w danej strefie docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-adoption"></a>Krok 6. wdrażanie

Decyzje podjęte podczas migracji i wysiłków programistycznych mogą mieć wpływ na długotrwałe operacje. Wczesne wyrównanie spójne w procesach wdrażania ułatwia usuwanie barier w wersji produkcyjnej i zmniejsza nakład pracy potrzebny do dołączania nowych rozwiązań do praktyk związanych z zarządzaniem.

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
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół ds. operacji w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Powyższe kroki ułatwią wdrożenie odpowiednich kontroli i procesów wymaganych do zapewnienia wydajności w całym przedsiębiorstwie i wszystkich hostowanych zasobach.
