---
title: 'Wprowadzenie: zarządzanie kosztami chmury'
description: Poznaj podstawy zarządzania kosztami związanymi z wdrażaniem w chmurze.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 456d5ecbe31d23731515821943da02861144bffe
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814547"
---
# <a name="get-started-manage-cloud-costs"></a>Wprowadzenie: zarządzanie kosztami chmury

Cost Management dyscypliny zarządzania chmurą koncentrują się na tworzeniu budżetów, monitorowaniu wzorców alokacji kosztów i wdrażaniu formantów w celu usprawnienia zachowań wydatków w chmurze w portfelu IT. Optymalizacja kosztów przedsiębiorstwa obejmuje wiele innych ról i funkcji pozwalających zminimalizować koszt i zrównoważyć wymagania dotyczące skalowania, wydajności, zabezpieczeń i niezawodności. W tym artykule zawarto mapowanie różnych funkcji pomocniczych do przewodnika wprowadzającego, które ułatwiają tworzenie wyrównania wśród poszczególnych zespołów.

Jednak Optymalizacja kosztów przedsiębiorstwa obejmuje wiele innych ról i funkcji pozwalających zminimalizować koszt i zrównoważyć wymagania dotyczące skalowania, wydajności, zabezpieczeń i niezawodności. Ten artykuł mapuje te funkcje pomocnicze, aby pomóc w tworzeniu wyrównania między nimi.

Zarządzanie jest podstawą optymalizacji kosztów w ramach każdego dużego przedsiębiorstwa. W poniższej sekcji przedstawiono wskazówki dotyczące optymalizacji kosztów w kontekście zarządzania. Kolejne kroki ułatwiają każdemu zespołowi podejmowanie działań, które są ukierunkowane na swoją rolę w optymalizacji kosztu. Razem te kroki pomogą Ci rozpocząć pracę w trakcie podróży w kierunku optymalizacji kosztów.

![Wprowadzenie do zarządzania kosztami przedsiębiorstwa](../_images/get-started/cost-map.png)

## <a name="step-1-optimize-enterprise-costs"></a>Krok 1. Optymalizowanie kosztów przedsiębiorstwa

Zespół ds. zarządzania chmurą jest dobrze przygotowany do oceny i działania w ramach przechodzenia lub nieplanowanych wydatków przez połączenie monitorowania wydajności, zmniejszenie rozmiarów zasobów i bezpieczne zakończenie korzystania z nieużywanych zasobów. Optymalizacja kosztu przedsiębiorstwa rozpoczyna się od udostępnienia zespołowi wiedzy o narzędziach, procesach i zależnościach, które są wymagane do działania w celu wyeliminowania problemów dotyczących kosztów na poziomie środowiska.

**Dostarczane**

- Implementuj zmiany kosztów zarządzania w całym przedsiębiorstwie.
- Udokumentowanie zasad zarządzania kosztami, procesów i wskazówek dotyczących projektowania w [Cost Management szablonu dyscypliny](../govern/cost-management/template.md).

Te elementy dostarczane są wynikiem kilku zadań cyklicznych:

- Zapewnij strategię strategiczną dla zespołu strategii chmury (w tym w przypadku uczestników projektu w portfelu).
- Zoptymalizuj koszty w środowisku:
  - Ręcznie lub automatycznie zamykaj nieużywane maszyny wirtualne.
  - Usuwanie lub cofanie zatrzymanych maszyn wirtualnych.
  - Upewnij się, że rozmiar zasobu jest prawidłowy.
  - Wyrównaj wydatki do oczekiwań budżetowych.
- Sprawdź poprawność wszelkich zmian architektury, korzystając z dobrze zaprojektowanego przeglądu Microsoft Azure, aby ułatwić rozmowę z właścicielami technicznymi obciążeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa i znakowania](../ready/azure-best-practices/naming-and-tagging.md). [Wymuś konwencje tagowania, korzystając z Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) z konkretnym wyróżnieniem tagów dla "centrum kosztów" i "właściciel techniczny".
- Regularnie należy zapoznać się z [najlepszymi rozwiązaniami w zakresie zarządzania kosztami](../govern/cost-management/best-practices.md) i zastosować je do analizy i ulepszeń w całym przedsiębiorstwie. Oto kilka z najbardziej wpływających praktyk ładu:

  - Postępuj zgodnie z [ogólnymi najlepszymi rozwiązaniami](../govern/cost-management/best-practices.md) , aby zmniejszyć rozmiar i koszty oraz zatrzymać nieużywane maszyny.
  - Stosuj [korzyści z używania hybrydowego](../govern/cost-management/best-practices.md#best-practice-take-advantage-of-azure-hybrid-benefit) , aby zmniejszyć koszty licencjonowania.
  - Wyrównaj [wystąpienia zarezerwowane](../govern/cost-management/best-practices.md#best-practice-use-reserved-vm-instances) , aby zmniejszyć koszty zasobów.
  - [Monitoruj wykorzystanie zasobów](../govern/cost-management/best-practices.md#best-practice-monitor-resource-utilization) , aby zminimalizować wpływ na wydajność zasobów.
  - [Zmniejsz koszty nieproduktywności](../govern/cost-management/best-practices.md#best-practice-reduce-nonproduction-costs) , korzystając z zasad, aby zarządzać środowiskami nieprodukcyjnymi.
  - Zaleceń dotyczących [optymalizacji kosztów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).

- Do zaimplementowania efektywnych zmian optymalizacji kosztów może być konieczny kompromis na poziomie obciążenia. [Microsoft Azure dobrze zaprojektowanej struktury](https://docs.microsoft.com/azure/architecture/framework/cost/tradeoffs) i [Microsoft Azure udokumentowane przeglądy](https://docs.microsoft.com/assessments/?id=azure-architecture-review) mogą pomóc w wykonywaniu tych rozmów przez właściciela technicznego określonego obciążenia.
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustal [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.
- Jeśli jesteś nowym członkiem dyscypliny Cost Management, weź pod uwagę następujące zagadnienia dotyczące ulepszeń w zakresie [zarządzania kosztami](../govern/guides/complex/cost-management-improvement.md). [implementation](../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

Zespół nadzoru może wykrywać i zwiększać znaczną optymalizację kosztów w większości przedsiębiorstw. Podstawowe, oparte na danych rozmiary zasobów mogą mieć bezpośredni i wymierny wpływ na koszty.

Zgodnie z opisem w temacie [Tworzenie ekonomicznej organizacji](../organize/cost-conscious-organization.md), skoncentrowanie się na zarządzaniu kosztami i optymalizacji kosztów może zapewnić znacznie więcej wartości. Poniższe kroki przedstawiają sposób, w jaki różne zespoły mogą pomóc w tworzeniu organizacji z niedrogią.

## <a name="step-2-define-a-strategy"></a>Krok 2. Definiowanie strategii

Strategiczne decyzje mają bezpośredni wpływ na kontrolę kosztów, zgrywanie przez cykl życia i wykonywanie długoterminowych operacji. Przejrzystość strategiczna poprawi koszty optymalizacji kosztów, prowadzone przez zespół nadzoru.

**Dostarczane**

- Rejestruj motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).
- Utwórz swój pierwszy budżet przy użyciu Azure Cost Management.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Poznaj motywacje](../strategy/motivations.md). Krytyczne zdarzenia biznesowe i niektóre motywacje migracji mogą być wrażliwe na koszty, zwiększając znaczenie kontroli kosztów dla wszystkich późniejszych wysiłków. Inne trendy do przodu dotyczące innowacji lub wzrostu przez proces migracji mogą skupić się więcej na przychodach z góry. Zrozumienie motywacji pomoże Ci zrozumieć, jak wysoki priorytet powinien być związany z zarządzaniem kosztami.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md). Niektóre wyniki finansowe mają być wyjątkowo wrażliwe na koszty. Gdy żądane wyniki są mapowane na metryki fiskalne, należy zainwestować w dyscypliny Cost Management ładu bardzo wcześnie.
- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md). Uzasadnienie biznesowe służy jako ogólny widok planu finansowego na potrzeby wdrażania w chmurze. Jest to dobre źródło dla początkowych nakładów budżetowych.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-develop-a-cloud-adoption-plan"></a>Krok 3. opracowywanie planu wdrażania chmury

Plan wdrożenia zapewnia przejrzystość na osi czasu działań podczas jej wdrażania. Wyrównanie planu i analiza cyfr cyfrowych umożliwiają prognozowanie miesięcznego wzrostu wydatków. Pomaga również zespołowi nadzoru w chmurze wyrównywać procesy i identyfikować wzorce wydatków.

**Dostarczane**

- Wykonaj kroki od 1 do 6 tworzenia [planu wdrożenia chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan).
- Pracuj z zespołem nadzoru w chmurze, aby udoskonalać budżety i tworzyć realistyczne prognozy wydatków.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Zbierz spis](../digital-estate/inventory.md). Ustanów źródło danych do analizy podpisywania cyfrowego przed przyjęciem.
- [Najlepsze rozwiązanie: Azure Migrate](../plan/contoso-migration-assessment.md). Użyj Azure Migrate, aby zebrać spis.
- [Przyrostowa racjonalizacja](../digital-estate/rationalize.md#incremental-rationalization). Podczas przyrostowej racjonalizacji i analizy ilościowej Zidentyfikuj kandydatów w chmurze na potrzeby budżetowania.
- [Wyrównaj modele kosztów i modele prognoz](../digital-estate/calculate.md). Użyj Azure Cost Management do wyrównania kosztów i modeli prognoz przez [Tworzenie budżetów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json).
- [Utwórz plan wdrożenia chmury](../plan/plan-intro.md#build-your-cloud-adoption-plan). Utwórz plan z możliwością działania, zasobami i szczegółami osi czasu. Ten plan jest podstawą do wydatków związanych z upływem czasu (lub prognozowania kosztów). _Wydatki w czasie_ są początkową linią bazową dla wszystkich analiz optymalizacji z możliwością działania w ramach dyscypliny ładu Cost Management.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-4-implement-best-practices-for-landing-zones"></a>Krok 4. Implementowanie najlepszych rozwiązań dla stref wyładunkowej

Przygotowana metodologia Microsoft Cloud Framework wdrażania dla systemu Azure koncentruje się na tworzeniu stref wyładunkowych w celu hostowania obciążeń w chmurze. Podczas wdrażania stref wyładunkowych organizacja powinna rozważyć różne decyzje dotyczące optymalizacji kosztów.

**Dostarczane**

- Wdróż co najmniej jedną strefę docelową, która umożliwia hostowanie obciążeń w ramach planu adopcji krótkoterminowej.
- Upewnij się, że wszystkie strefy docelowe spełniają decyzje dotyczące optymalizacji kosztów i wymagania dotyczące zarządzania kosztami.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Śledzenie kosztów](../ready/azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access). Należy ustanowić dobrze zarządzaną hierarchię środowiskową, zapewnić odpowiedni poziom dostępu do kosztów i używać dodatkowych zasobów zarządzania kosztami w każdej strefie docelowej.
- [Zoptymalizuj inwestycję w chmurę](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi optymalizacji inwestycji.
- [Tworzenie budżetów i zarządzanie nimi](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi tworzenia budżetów i zarządzania nimi.
- [Zoptymalizuj koszty z zaleceń](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi używania zaleceń, które optymalizują koszty.
- [Monitoruj użycie i wydatki](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi monitorowania użycia i wydatków w ramach strefy docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-complete-waves-of-migration-effort"></a>Krok 5. zakończenie pracy dotyczącej migracji

Migracja jest procesem powtarzalnym wykonywanym przez zespół ds. wdrażania w chmurze. W trakcie tego procesu istnieje wiele możliwości optymalizacji kosztów w portfelu. Wiele z tych decyzji w procesie jest stosowanych do małej grupy obciążeń podczas każdej fazy lub iteracji migracji.

**Dostarczane**

- Testy porównawcze, testowe, zmiany rozmiaru i wdrożenia kolekcji w pełni zoptymalizowanych obciążeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Mechanizmy kontroli kosztów skoncentrowane na migracji](../migrate/azure-migration-guide/manage-costs.md) zapewniają wgląd w informacje o kontrolkach optymalizacji kosztów natywnych w chmurze, które pomagają podczas migracji.
- [Najlepsze rozwiązania w zakresie optymalizacji kosztów migrowanych obciążeń](../migrate/azure-best-practices/migrate-best-practices-costs.md) zawierają listę kontrolną 14 najlepszych rozwiązań, które należy wykonać przed i po migracji w celu zmaksymalizowania optymalizacji kosztów każdej wersji obciążenia.

Długoterminowe koszty operacyjne są typowymi motywami w każdym obszarze ulepszeń procesów migracji. Ta lista ulepszeń procesów jest zorganizowana według fazy procesu migracji:

- [Wymagania wstępne](../migrate/migration-considerations/prerequisites/index.md) zawierają informacje dotyczące zarządzania zmianami i zaległościami, które mają wpływ na budżet i rzeczywiste koszty chmury.
- [Ocena](../migrate/migration-considerations/assess/index.md) zawiera sześć określonych procesów, od weryfikacji założeń do poznania opcji partnerów. Każdy proces ma wpływ na możliwości optymalizacji chmury.
- [Migracja](../migrate/migration-considerations/migrate/index.md) zawiera jedną sugestię procesu dotyczącą zasobów korygowaniem. Ta sugestia pozwala zoptymalizować stan as skonfigurowany w celu zoptymalizowania rozwiązania.
- [Promuj](../migrate/migration-considerations/optimize/index.md) się w dużym stopniu na testowaniu, zmianie rozmiarów, sprawdzaniu i zwalnianiu zmigrowanych zasobów oraz likwidowanie wycofanych zasobów. Jest to pierwszy czysty punkt, w którym prognozy i budżety mogą być testowane względem rzeczywistej wydajności i konfiguracji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-drive-customer-focused-innovation"></a>Krok 6. nałożenie innowacji ukierunkowanych na klientów

Innowacje i rozwój nowych produktów wymagają znacznie bardziej szczegółowego stopnia przeglądu architektury. Struktura wdrażania w chmurze zawiera szczegółowe informacje na temat procesu innowacji i zarządzania produktami. Decyzje dotyczące optymalizacji kosztów rozwiązań dotyczących innowacji są w dużej mierze poza zakresem.

**Dostarczane**

- Podejmuj kluczowe decyzje dotyczące architektury dotyczące innowacji, aby zrównoważyć koszty i inne istotne zagadnienia dotyczące projektowania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Skorzystaj z [dobrze zaprojektowanej Microsoft Azure przegląd](https://docs.microsoft.com/assessments/?id=azure-architecture-review) , aby poznać saldo decyzji dotyczących architektury.
- Zapoznaj się z [wydajną platformą Microsoft Azure](https://docs.microsoft.com/azure/architecture/framework) , aby uzyskać bardziej szczegółowe wskazówki dotyczące optymalizacji kosztów podczas innowacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-7-implement-sound-operations"></a>Krok 7. Implementowanie operacji dźwiękowych

Ustanowienie stałego planu bazowego zarządzania pomoże Ci zbierać dane i tworzyć alerty operacyjne. Ten nakład pracy może pomóc w wykrywaniu możliwości w celu optymalizacji kosztów. Zostanie utworzona równowaga między odpornością i optymalizacją kosztów.

**Dostarczane**

- Monitoruj środowisko przedsiębiorstwa pod kątem bieżących zaleceń, aby zoptymalizować koszty, wyrównane do stopnia ważności i klasyfikacji odporności poszczególnych obciążeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Utwórz wyrównanie biznesowe](../manage/considerations/business-alignment.md) , aby uzyskać przejrzystość w zakresie krytyczności i akceptowalnego poziomu na potrzeby inwestycji związanych z odpornością.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Wykonanie tych kroków może pomóc [w tworzeniu organizacji z](../organize/cost-conscious-organization.md)niedrogimi kosztami. Optymalizacja kosztów jest łatwiejsza do wdrożenia, gdy organizacja używa udostępnionej własności i koncentruje się na współpracy z właściwymi zespołami w odpowiednim czasie.
