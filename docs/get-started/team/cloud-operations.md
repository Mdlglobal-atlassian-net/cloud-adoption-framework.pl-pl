---
title: 'Wprowadzenie: Tworzenie zespołu operacji w chmurze'
description: Ten przewodnik pomaga zespołowi operacyjnemu w chmurze zrozumieć zakres, elementy dostarczane i funkcje, z którymi są odpowiedzialni.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: f7670efdfb22a6542efe93f309e8bbaf83a2027e
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83815127"
---
# <a name="get-started-build-a-cloud-operations-team"></a>Wprowadzenie: Tworzenie zespołu operacji w chmurze

Zespół operacyjny koncentruje się na monitorowaniu, naprawianiu i korygowaniem problemów związanych z tradycyjnymi operacjami IT i zasobami. W chmurze wiele kosztów kapitałowych i działań związanych z operacjami jest przesyłanych do dostawcy chmury, dzięki czemu można wykonać operację w celu poprawy i zapewnienia znaczącej dodatkowej wartości.

![Wprowadzenie do tworzenia zespołu operacji w chmurze](../../_images/get-started/operations-team-map.png)

## <a name="step-1-determine-whether-a-cloud-operations-team-is-needed"></a>Krok 1. ustalenie, czy zespół operacji w chmurze jest wymagany

Przed zwolnieniem obciążeń do produkcji należy uzyskać umowę na odpowiedzialność za dostarczenie [funkcji operacji w chmurze](../../organize/cloud-operations.md). W przypadku niektórych portfeli odpowiedzialności operacyjne mogą zawiesić się z zespołami wdrażania DevOps i chmurą. W innych przypadkach, dostawca usług zarządzanych z obsługą operacji w chmurze może przyjmować bieżące obowiązki operacyjne.

W przypadku braku umów dotyczących operacji na DevOps lub dostawcy usług jest bezpieczne założenie, że ktoś w tej organizacji będzie musiał zatwierdzić bieżące obowiązki operacyjne dotyczące zarządzania obciążeniami produkcyjnymi.

**Dostarczane**

- Ustal, czy potrzebujesz zespołu operacji w chmurze.
- Udokumentowanie decyzji i osób odpowiedzialnych w [Raci (odpowiedzialnych, umożliwiających, z którymi odbywa się konsultacje i informowanie)](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) w `Org Alignment` arkuszu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Funkcje operacji w chmurze](../../organize/cloud-operations.md) mogą być rozłożone na wiele osób lub zespołów. Zdecyduj, czy zespół operacji w chmurze jest wymagany. Pewien poziom operacji jest zawsze wymagany w przypadku obciążeń produkcyjnych.
- Jeśli długoterminowa strategia wdrażania chmury w firmie może być dostarczana z jednej strefy wyładunkowej w jednym środowisku chmury, działania związane z zarządzaniem i operacjami mogą być wystarczająco małe, aby można je było dostarczyć przez jedną osobę lub jeden zespół. Ten zespół jest mało prawdopodobne, aby można było wywołać operacje w chmurze, ponieważ będzie on obsługiwał wiele funkcji. W przypadku tej osoby lub zespołu następujące wskazówki mogą pomóc w zapewnieniu, że mogą one dostarczać tę ważną funkcję operacji.

<!-- markdownlint-disable MD033 -->

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury |

## <a name="step-2-align-with-other-teams"></a>Krok 2. Wyrównywanie z innymi zespołami

Zespół operacyjny w chmurze dziedziczy obowiązki operacyjne dla wszystkich obciążeń w portfolio produkcyjnym. Te obowiązki mogą się różnić w zależności od obciążeń, na podstawie oczekiwań i zobowiązań, które zespół wprowadził do zainteresowanych podmiotów. Decyzje dotyczące architektury podejmowane przez zespoły wdrażające w chmurze ukierunkowane na migrację i innowacje mają również wpływ na zobowiązania operacyjne zespołu.

Przed zaimplementowaniem przez zespół operacyjny w chmurze wszelkich trwających działań, ważne jest, aby było ono wyrównane z innymi zespołami. Zespół powinien spełnić inne zespoły, które zostały zidentyfikowane w szablonie RACI, aby zapewnić wyrównanie najważniejszych tematów, takich jak zabezpieczenia, koszt, wydajność, zarządzanie, wdrażanie i wdrożenie. Kroki 4 i 5 mogą pomóc w uproszczeniu tego wyrównania.

**Dostarczane**

- Omawiaj implementację bieżącego stanu i bieżące plany przyjęcia dla każdego zespołu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Aby zrozumieć motywacje, metryki i strategię zespołu, przejrzyj [strategię i plan planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) swojej firmy z członkami zespołu strategii chmurowych.
- Aby zrozumieć osie czasu i priorytetyzację, zapoznaj się z [szablonem planu wdrożenia chmury](../../plan/template.md) w firmie z członkami zespołu ds. wdrażania w chmurze.
- Aby zrozumieć wymagania operacyjne i zobowiązania, które zespół ustanowił z firmą, zacznij opracowywać [skoroszyt zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li>  Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Krok 3. nawiązanie erze z innymi zespołami

Wdrażanie w chmurze zwykle znajduje się w fale lub wersjach. Regularna erze, która jest wyrównana z tymi wersjami, umożliwia zespołowi operacyjnemu w chmurze przygotowanie się do etapach na końcu kolejnej fazy. Zaangażowanie się z strategiami, wdrażaniem i zarządzaniem w trakcie planowania i przegląd pomaga zespołowi operacyjnemu zachować się z wyprzedzeniem.

**Dostarczane**

- Ustanów erze z zespołami pomocniczymi. Jeśli to możliwe, Wyrównaj ten erze z cyklami wydań i planowania.
- Ustanów osobne erze bezpośrednio z zespołem ds. strategii chmurowej lub jego różnych członków zespołu, aby zapoznać się z wymaganiami operacyjnymi związanymi z następną analizą.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Dodatkowe wskazówki dotyczące cadences na potrzeby spotkań można znaleźć w sekcji "elementy dostarczane" [funkcji operacji w chmurze](../../organize/cloud-operations.md#deliverables).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury |

## <a name="step-4-review-the-methodology"></a>Krok 4: przegląd metodologii

Aby pomóc w ustaleniu przyszłej wizji w zakresie zarządzania operacjami i współpracy w celu osiągnięcia tej wizji, zapoznaj się z metodologią zarządzania w strukturze wdrożenia chmury.

**Dostarczane**

- Uzyskaj zrozumienie metodologii, podejścia i implementacji, które wspierają metodologię zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [metodologią zarządzania w strukturze wdrożenia chmury](../../manage/index.md).

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za wizję i podejście do zarządzania operacjami.

## <a name="step-5-implement-the-operations-baseline"></a>Krok 5. Implementowanie linii bazowej operacji

Jeśli praktyki operacji nie są już wdrożone w środowiskach chmury, Rozpocznij od punktu odniesienia operacji. Ta linia bazowa będzie implementować natywne rozwiązania w chmurze, no-Ops/niskie zastosowania, aby zapewnić podstawowy poziom ochrony operacyjnej.

**Dostarczane**

- Wdróż podstawowe konfiguracje zarządzania serwerem platformy Azure, które są wymagane do obsługi środowiska w ciągu najbliższych kilku wysiłków.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zaimplementuj konfigurację [linii bazowej operacji](../../manage/azure-server-management/index.md) .

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za wdrożenie linii bazowej operacji.

## <a name="step-6-align-business-commitments"></a>Krok 6. wyrównanie zobowiązań gospodarczych

Zapoznaj się ze zobowiązaniami linii bazowej operacji zespołu z zainteresowanymi stronami biznesowymi. Ta linia bazowa ułatwia ocenę ogólnych wymagań dotyczących większości obciążeń. Proces ten ułatwia również identyfikację osób biorących udział w różnych obciążeniach i pozwala na udokumentowanie bieżących oczekiwań operacyjnych.

**Dostarczane**

- Udokumentowanie oczekiwań uczestników firmy.
- Określ, czy zaawansowane operacje są wymagane dla określonych obciążeń lub platform.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Utwórz [wyrównanie biznesowe](../../manage/considerations/business-alignment.md) w chmurze.
- Udokumentowanie oczekiwań portfela i operacji w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Zespół odpowiedzialny za:**

- Zespół ds. operacji w chmurze powinien zrozumieć oczekiwania biznesowe i jest odpowiedzialny za ciągłe wyrównywanie z tymi oczekiwaniami.

## <a name="step-7-operations-maturity"></a>Krok 7: data_spłaty operacji

Poprzez nieustanne wprowadzanie ulepszeń operacyjnych zespół może:

- Popraw linię bazową operacji.
- Ulepszanie operacji platformy.
- Implementowanie operacji specyficznych dla obciążenia.

W miarę jak dodatkowe obciążenia są przenoszone do operacji w chmurze, konieczna jest przejrzysta operacja ulepszeń operacji.

**Dostarczane**

- Popraw termin zapadalności operacji, aby wspierać zobowiązania dla uczestników biznesowych.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Oceń najlepsze opcje [zaawansowanego zarządzania operacjami](../../manage/design-principles.md).

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za ulepszenia operacyjne i dojrzałości w czasie.

## <a name="step-8-scale-operations-consistency-through-governance"></a>Krok 8: skalowanie spójności operacji poprzez zarządzanie

W miarę jak Planowanie operacji w dalszym ciągu zespół powinien koordynować zespół nadzoru chmurowego, aby stosować wymagania dotyczące operacji w całym portfolio.

**Dostarczane**

- Pomóż zespołowi ładu w chmurze zaimplementować nowe wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [przewodnikiem ładu w celu zwiększenia spójności zasobów](../../govern/guides/complex/resource-consistency-improvement.md).

<!-- markdownlint-disable MD033 -->

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół ds. operacji w chmurze |

## <a name="step-9-adoption-handoffs"></a>Krok 9. wdrażanie etapach

Po zakończeniu nowych działań związanych z wdrażaniem w chmurze zespół rozwiązań operacyjnych nie będzie odpowiedzialny za działania w chmurze i zespoły nadzorujące zarządzanie chmurą. Aby zapewnić odpowiednią dokumentację i wyrównanie zasad oraz przyjąć odpowiedzialność za obciążenia, zespół powinien pozostać wyrównany z wersjami adopcji.

**Dostarczane**

- Regularnie Przeglądaj i Akceptuj etapach z zespołów wdrażania w chmurze.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Ustanów proces dołączania [nowych obciążeń i zasobów](https://docs.microsoft.com/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding).

<!-- markdownlint-disable MD033 -->

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespoły wdrażania chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze |

## <a name="whats-next"></a>Co dalej

W miarę przyjmowania i skalowania operacji ważne jest definiowanie i automatyzowanie najlepszych rozwiązań dotyczących zarządzania, które zwiększają istniejące wymagania IT. Tworzenie zespołu usługi Cloud Center doskonałości (CCoE) to ważny krok w kierunku skalowania rozwiązań chmurowych, operacji w chmurze i zarządzania chmurą.

Dowiedz się więcej o usługach:

- [Funkcje centrum doskonałości chmury](../../organize/cloud-center-of-excellence.md)
- [Antywzorce organizacyjne: silosy i fiefdoms](../../organize/fiefdoms-silos.md)

Dowiedz się, jak wyrównać zakres obowiązków dla zespołów, opracowując macierz międzyzespołową, która identyfikuje strony RACI. Pobierz i zmodyfikuj [szablon arkusza kalkulacyjnego Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).
