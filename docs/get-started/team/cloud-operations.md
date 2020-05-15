---
title: 'Wprowadzenie: Tworzenie zespołu operacji w chmurze'
description: Ten przewodnik pomaga zespołowi operacyjnemu w chmurze zrozumieć zakres, elementy dostarczane i funkcje, z którymi są odpowiedzialni.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: af65cff02d7c3768bf5fca554334923cf2172937
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400163"
---
# <a name="get-started-build-a-cloud-operations-team"></a>Wprowadzenie: Tworzenie zespołu operacji w chmurze

Zespół operacyjny koncentruje się na monitorowaniu, naprawianiu i korygowaniu problemów związanych z tradycyjnymi operacjami IT i zasobami. W chmurze wiele kosztów kapitałowych i działań związanych z operacjami jest przesyłanych do dostawcy chmury, dzięki czemu można wykonać operację w celu poprawy i zapewnienia znaczącej dodatkowej wartości.

![Wprowadzenie do tworzenia zespołu operacji w chmurze](../../_images/get-started/operations-team-map.png)

## <a name="step-1-determine-if-a-cloud-operations-team-is-needed"></a>Krok 1. ustalenie, czy zespół operacji w chmurze jest wymagany

Przed zwolnieniem obciążeń do produkcji należy uzyskać umowę na odpowiedzialność za dostarczenie [funkcji operacji w chmurze](../../organize/cloud-governance.md). W przypadku niektórych portfeli odpowiedzialności operacyjne mogą pozostawać w zespole DevOps i w chmurze. W innych przypadkach, dostawca usług zarządzanych z obsługą operacji w chmurze może przyjmować bieżące obowiązki operacyjne.

Jeśli nie ma żadnych umów dotyczących operacji na DevOps lub dostawcy usług, można bezpiecznie założyć, że ktoś w niej będzie musiał zatwierdzić bieżące obowiązki operacyjne dotyczące zarządzania wszelkimi obciążeniami produkcyjnymi.

**Dostarczane**

- Ustal, czy potrzebujesz zespołu operacji w chmurze.
- Udokumentowanie decyzji i osób odpowiedzialnych w [szablonie Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) na karcie wyrównanie organizacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Funkcje operacji w chmurze](../../organize/cloud-operations.md) mogą być rozłożone na wiele osób lub zespołów. Konieczne będzie określenie, czy zespół operacji w chmurze jest wymagany. Jednak pewien poziom operacji jest zawsze wymagany w przypadku obciążeń produkcyjnych.
- Jeśli strategia wdrażania długoterminowego w firmie może zostać dostarczona z jednej strefy wyładunkowej w jednym środowisku chmury, to ilość działań związanych z zarządzaniem i operacjami może być wystarczająco mała, aby mogła zostać dostarczona przez jedną osobę lub jednego zespołu. Ten zespół jest mało prawdopodobne, aby można było wywołać operacje w chmurze, ponieważ będą one obsługiwać wiele funkcji. Nawet dla tego zespołu lub osoby, następujące wskazówki pomogą zagwarantować, że zespół zostanie przygotowany do dostarczenia do tej ważnej funkcji operacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury |

## <a name="step-2-align-with-other-teams"></a>Krok 2. Wyrównywanie z innymi zespołami

Zespół operacyjny dziedziczy obowiązki operacyjne dla wszystkich obciążeń w portfolio produkcyjnym. Te obowiązki mogą się różnić między obciążeniami, w zależności od oczekiwań i zobowiązań związanych z firmą. Decyzje dotyczące architektury podejmowane przez migrację i innowacje ukierunkowane zespoły wdrażania chmury wpływają również na zobowiązania operacyjne, które mogą zostać wykonane. Przed zaimplementowaniem wszelkich trwających działań operacyjnych ważne jest, aby dostosować je do innych zespołów. Zespół operacyjny w chmurze powinien spełnić inne zespoły identyfikowane w szablonie RACI, aby zapewnić wyrównanie najważniejszych tematów, takich jak zabezpieczenia, koszt, wydajność, zarządzanie, wdrażanie i wdrożenie. Kroki 4 i 5 mogą ułatwić wyrównania.

**Dostarczane**

- Omawiaj bieżące implementacje stanu i ciągłych planów wdrażania dla każdego zespołu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [strategią i planem planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) swojej firmy, korzystając z członków zespołu strategii chmury, aby zrozumieć motywacje, metryki i strategię.
- Zapoznaj się z [szablonem planu wdrożenia chmury](../../plan/template.md) w firmie z członkami zespołu wdrażania chmury, aby zrozumieć osie czasu i priorytetyzację.
- Zacznij projektować [skoroszyt zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , aby zrozumieć wymagania operacyjne i zobowiązania, które zostały nawiązane z firmą.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-establish-cadence-with-other-teams"></a>Krok 3. nawiązanie erze z innymi zespołami

Wdrażanie w chmurze zwykle znajduje się w fale lub w wydaniach. Regularne erze wyrównane do tych wersji umożliwi zespołowi Operations w chmurze przygotowanie się do etapachu na końcu kolejnej fazy. Zaangażowanie się z strategiami, wdrażaniem i zarządzaniem w trakcie planowania i przegląd pomaga zespołowi operacyjnemu zachować się z wyprzedzeniem.

**Dostarczane**

- Ustanów erze z każdym z zespołów pomocniczych. Jeśli to możliwe, Wyrównaj ten erze do wersji i planowania cykle.
- Ustanów osobne erze bezpośrednio z zespołem ds. strategii chmury (lub różnych członków zespołu), aby zapoznać się z wymaganiami operacyjnymi związanymi z następnym etapem wdrażania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [funkcjami operacji w chmurze](../../organize/cloud-operations.md#deliverables) , aby uzyskać dodatkowe wskazówki na temat spotkania cadences.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół nadzorujący chmury |

## <a name="step-4-review-the-methodology"></a>Krok 4: przegląd metodologii

Zapoznaj się z metodologią zarządzania platformą wdrażania w chmurze, aby pomóc w ustaleniu przyszłej wizji dotyczącej zarządzania operacjami, a następnie działającym podejściem do uzyskania tej wizji.

**Dostarczane**

- Uzyskaj zrozumienie metodologii, podejścia i implementacji, które wspierają metodologię zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [metodologią zarządzania](../../manage/index.md).

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za wizję i podejście do zarządzania operacjami.

## <a name="step-5-implement-the-operations-baseline"></a>Krok 5. Implementowanie linii bazowej operacji

Jeśli nie ma żadnych praktyk dotyczących operacji wdrożonych w środowiskach w chmurze, Zacznij od linii bazowej operacji. Ta linia bazowa będzie implementować natywne rozwiązania w chmurze, no-Ops/niskie zastosowania, aby zapewnić podstawowy poziom ochrony operacyjnej.

**Dostarczane**

- Wdróż podstawowe konfiguracje zarządzania serwerem platformy Azure wymagane do obsługi środowiska w ciągu najbliższych kilku wysiłków.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zaimplementuj konfigurację [linii bazowej operacji](../../manage/azure-server-management/index.md) .

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za linię bazową operacji.

## <a name="step-6-align-business-commitments"></a>Krok 6. wyrównanie zobowiązań gospodarczych

Zapoznaj się ze zobowiązaniami linii bazowej operacji z firmą. Ta linia bazowa ułatwia ocenę ogólnych wymagań dotyczących większości obciążeń. Proces ten pomaga również identyfikować zainteresowane strony biznesowe dotyczące różnych obciążeń i umożliwia dokumentowanie bieżących oczekiwań operacyjnych.

**Dostarczane**

- Udokumentowanie oczekiwań firmy.
- Ustal, czy dla konkretnych obciążeń lub platform są wymagane Zaawansowane operacje.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Utwórz [wyrównanie biznesowe](../../manage/considerations/business-alignment.md) w chmurze.
- Udokumentowanie oczekiwań portfela i operacji w [skoroszycie zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx).

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze powinien zrozumieć oczekiwania biznesowe i jest odpowiedzialny za ciągłe wyrównywanie działania z tymi oczekiwaniami.

## <a name="step-7-operations-maturity"></a>Krok 7: data_spłaty operacji

Ulepszenia operacyjne mogą powodować powstanie kilku opcji:

- Popraw linię bazową operacji.
- Ulepszanie operacji platformy.
- Implementowanie operacji specyficznych dla obciążenia.

W miarę jak dodatkowe obciążenia są przenoszone do operacji w chmurze, konieczna jest przejrzysta operacja ulepszeń operacji.

**Dostarczane**

- Poprawa dojrzałości operacji w celu wspierania zobowiązań firmy.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Oceń najlepszą opcję dla [zaawansowanego zarządzania operacjami](../../manage/design-principles.md).

**Zespół odpowiedzialny za:**

- Zespół operacyjny w chmurze jest odpowiedzialny za ulepszenia operacyjne i dojrzałości w czasie.

## <a name="step-8-scale-operations-consistency-through-governance"></a>Krok 8: skalowanie spójności operacji poprzez zarządzanie

Podobnie jak w przypadku operacji, koordynuj z zespołem nadzoru chmurowego, aby zastosować wymagania dotyczące operacji w całym portfolio.

**Dostarczane**

- Pomóż zespołowi ładu w chmurze zaimplementować nowe wymagania dotyczące spójności zasobów.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Przykład [poprawy spójności zasobów przy użyciu wymuszania ładu](../../govern/guides/complex/resource-consistency-improvement.md).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół ds. operacji w chmurze |

## <a name="step-9-adoption-handoffs"></a>Krok 9. wdrażanie etapach

Po zakończeniu nowych działań związanych z wdrażaniem zespół ds. wdrażania chmury będzie przełączać obowiązki operacyjne do zespołu ds. operacji w chmurze i zespołów nadzoru chmurowego. Zachowaj zgodność z wersjami przyjmowania, aby zapewnić odpowiednią dokumentację i wyrównanie zasad w celu zagwarantowania odpowiedzialności za obciążenia.

**Dostarczane**

- Regularnie Przeglądaj i Akceptuj etapach z zespołów wdrażania w chmurze.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Ustanów proces dołączania [nowych obciążeń i zasobów](https://docs.microsoft.com/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespoły wdrażania chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze |

## <a name="whats-next"></a>Co dalej

W miarę przyjmowania i skalowania operacji ważne jest definiowanie i automatyzowanie najlepszych rozwiązań dotyczących zarządzania, które zwiększają istniejące wymagania IT. Tworzenie zespołu usługi Cloud Center doskonałości (CCoE) jest ważnym krokiem do skalowania działań związanych z wdrażaniem w chmurze, operacji w chmurze i zarządzania chmurą.

Dowiedz się więcej o usługach:

- [Centrum usługi w chmurze funkcji doskonałości](../../organize/cloud-center-of-excellence.md)
- [Antywzorce organizacyjne: silosy i fiefdoms](../../organize/fiefdoms-silos.md)

Dowiedz się, jak wyrównać zakres obowiązków dla zespołów, opracowując macierz międzyzespołową, która identyfikuje osoby odpowiedzialne, obsługujące, konsultowane i poinformowane (RACI). Pobierz i zmodyfikuj [szablon arkusza kalkulacyjnego Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).
