---
title: 'Wprowadzenie: Tworzenie zespołu ładu w chmurze'
description: Ustanów zakres, elementy dostarczane przez zespół nadzoru i możliwości przygotowania do pomyślnego zarządzania chmurą.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 04/04/2020
ms.openlocfilehash: 5b1d1cb9213b40242e95af60bead9ef3a919054a
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229147"
---
<!-- docsTest:ignore Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template -->

# <a name="get-started-build-a-cloud-governance-team"></a>Wprowadzenie: Tworzenie zespołu ładu w chmurze

Zespół zarządzający chmurą gwarantuje, że ryzyko i odporność na ryzyko są prawidłowo oceniane i zarządzane. Ten zespół zapewnia właściwą identyfikację zagrożeń, które nie mogą być tolerowane przez firmę. Osoby na tym zespole konwertują ryzyko na zarządzanie zasadami firmowymi.

![Wprowadzenie do tworzenia zespołu zarządzania chmurą](../../_images/get-started/governance-team-map.png)

## <a name="step-1-determine-if-a-cloud-governance-team-is-needed"></a>Krok 1. ustalenie, czy zespół ładu chmury jest wymagany

Oficjalne wskazówki w zakresie wdrażania chmury to zawsze Tworzenie zespołu nadzoru w chmurze. Na początku ten zespół może być wyjątkowo mały. Jednak niezależnie od jego rozmiaru ta rola będzie ważna. Jeśli zespół nie jest wymagany, Grupa lub osoba będąca członkiem zespołu powinna wyrazić zgodę na spełnienie obowiązków związanych z [funkcjami ładu w chmurze](../../organize/cloud-governance.md).

**Dostarczane**

- Ustal, czy potrzebujesz zespołu nadzoru w chmurze.
- Udokumentowanie decyzji i osób odpowiedzialnych w [szablonie Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) na karcie wyrównanie organizacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Funkcje ładu chmury](../../organize/cloud-governance.md) mogą być rozłożone na wiele osób lub zespołów. Posiadanie zespołu, który przechodzi przez tytuł "zespół ds. zarządzania chmurą", ma niewielki znaczenie. Jednak wymagane możliwości powinny nastąpić z podmiotem lub zespołem.
- W przypadku długoterminowej strategii wdrażania chmurowego firmy można dostarczyć z jednej strefy wyładunkowej w jednym środowisku chmury, a następnie wpływ na działalność nadzoru i operacji może być wystarczająco mały do dostarczenia przez jedną osobę lub jednego zespołu. Jest mało prawdopodobne, że zespół nadzoruje chmurę, ponieważ obsługuje wiele funkcji poza zarządzaniem chmurą. Nawet w przypadku tego zespołu Poniższy przewodnik z wprowadzeniem pomoże Ci upewnić się, że zespół jest przygotowany do dostarczenia do tej ważnej funkcji zarządzania.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury |

## <a name="step-2-align-with-other-teams"></a>Krok 2. Wyrównywanie z innymi zespołami

Zespół nadzoru gwarantuje spójność i zgodność z zestawem wspólnych zasad. Te zasady pochodzą z ciągłego wyrównania z innymi zespołami. Przed ustanowieniem zasad lub zautomatyzowanym nadzorem w chmurze zespół nadzorujący chmury powinien spełnić inne zespoły identyfikowane w szablonie RACI, aby zapewnić wyrównanie najważniejszych tematów, takich jak zabezpieczenia, koszt, wydajność, operacje i wdrażanie. Kroki 4 i 5 mogą ułatwić wyrównania.

**Dostarczane**

- Omawiaj bieżące implementacje stanu i ciągłych planów wdrażania dla każdego zespołu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [strategią i planem planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) swojej firmy, korzystając z członków zespołu strategii chmury, aby zrozumieć motywacje, metryki i strategię.
- Zapoznaj się z [szablonem planu wdrożenia chmury](../../plan/template.md) w firmie z członkami zespołu wdrażania chmury, aby zrozumieć osie czasu i priorytetyzację.
- Przejrzyj [skoroszyt zarządzania](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/manage/opsmanagementworkbook.xlsx) operacjami zespołu operacji, aby zrozumieć wymagania operacyjne i zobowiązania, które zostały nawiązane z firmą.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Krok 3. nawiązanie erze z innymi zespołami

Wdrażanie w chmurze ogólne jest dostępne w przypadku wersji. Regularne erze wyrównane do tych wersji umożliwi zespołowi nadzoru w chmurze zapoznanie się z wyprzedzeniem i zrozumienie zagrożeń, które zostaną wprowadzone w następnej fazie. Zaangażowanie się z strategiami, wdrażaniem i zespołami operacyjnymi podczas planowania i przeglądów pomoże zespołowi nadzoru nadal korzystać z zagrożeń.

**Dostarczane**

- Ustanów erze z każdym z zespołów pomocniczych. Jeśli to możliwe, Wyrównaj ten erze do wersji i planowania cykle.
- Ustanów osobne erze bezpośrednio z zespołem ds. strategii chmury (lub różnych członków zespołu), aby zapoznać się z ryzykiem związanym z następną analizą przyjęcia oraz ocenić swój poziom tolerancji dla tych zagrożeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z funkcjami nadzoru w [chmurze](../../organize/cloud-governance.md#deliverable) , aby uzyskać dodatkowe wskazówki na temat spotkania cadences.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół ds. operacji w chmurze |

## <a name="step-4-review-the-methodology"></a>Krok 4: przegląd metodologii

Zapoznaj się z metodologią działania platformy wdrażania w chmurze, aby uzyskać pomoc w ustaleniu przyszłej wizji dotyczącej zarządzania i działającego podejścia do tej wizji.

**Dostarczane**

- Uzyskaj zrozumienie metodologii, podejścia i implementacji, które wspierają metodologię zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [metodologią zarządzania](../../govern/methodology.md).

**Zespół odpowiedzialny za:**

- Zespół ds. zarządzania chmurą jest odpowiedzialny za ustanawianie wizji i podejście do ładu.

## <a name="step-5-complete-the-governance-benchmark"></a>Krok 5. Kończenie testu porównawczego ładu

Zarządzanie to szeroki temat. Ta krótka ocena może pomóc zrozumieć, gdzie rozpocząć pracę.

**Dostarczane**

- Ukończ ocenę testu porównawczego w oparciu o konwersacje z różnymi uczestnikami projektu (lub poproszenie innych zespołów o samodzielne przeprowadzenie oceny).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Oceń potrzeby i priorytety związane z zarządzaniem za pomocą [testu porównawczego](../../govern/benchmark.md)

**Zespół odpowiedzialny za:**

- Zespół ds. zarządzania chmurą powinien zrozumieć luki zidentyfikowane w teście porównawczym ładu i zapewnić kierownictwo, który pomaga rozwiązywać luki.

## <a name="step-6-implement-the-initial-governance-best-practice-and-configuration"></a>Krok 6. Implementowanie początkowego najlepszego rozwiązania i konfiguracji zarządzania

Metodologia rządząca obejmuje dwa podejścia do początkowego ładu. Przejrzyj wszystkie i Implementuj te, które najlepiej pasują do Twoich potrzeb.

**Dostarczane**

- Wdróż podstawowe narzędzia do zarządzania i konfiguracje organizacji wymagane do zarządzania środowiskiem w ciągu najbliższych kilku wysiłków.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [początkową](../../govern/initial-foundation.md) konfiguracją najlepszych rozwiązań i wskazówki dotyczące implementacji.

**Zespół odpowiedzialny za:**

- Zespół nadzorujący w chmurze jest odpowiedzialny za przegląd i wdrażanie najlepszych rozwiązań z zakresu nadzoru i początkowej usługi ładu.

## <a name="step-7-continuously-improve-the-governance-maturity"></a>Krok 7. nieustanne ulepszanie okresu zarządzania

Wymagania dotyczące ładu zwiększają się wraz z ukończeniem dodatkowego wdrożenia chmury. Zachowaj zgodność z ciągłym planem wdrożenia, aby zapewnić, że podejście ładu może utrzymywać odpowiednie poziomy nadzoru i kontroli.

**Dostarczane**

- Zaimplementuj usprawnienia ładu chroniące przed zmianami ryzyka i potrzebami zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zaimplementuj [rozwinięte scenariusze ładu](../../govern/foundation-improvements.md) , aby poprawić początkową podstawę zarządzania.

**Zespół odpowiedzialny za:**

- Zespół ds. ładu w chmurze umożliwia dostosowanie z ciągłymi planami wdrażania.

## <a name="step-8-evaluate-landing-zone-changes"></a>Krok 8. oszacowanie zmian strefy wyładunkowej

Gdy strefy wyładunkowe są wdrażane i rozszerzane, mogą pojawić się nowe zagrożenia lub naruszenia zasad zarządzania. Okresowe przeglądanie konfiguracji strefy wyładunkowej w celu zidentyfikowania odchyleń od zasad, które nie są przechwytywane do natywnych narzędzi do zarządzania w chmurze. Upewnij się, że każde wdrożenie strefy docelowej jest zgodne z wytycznymi dotyczącymi nadzoru strefy docelowej.

**Dostarczane**

- Pomóż zespołowi Cloud Platform w opracowaniu ulepszeń strefy docelowej, które są zgodne z zasadami ładu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Usprawnij [Zarządzanie strefami wyładunkowymi](../../ready/considerations/landing-zone-governance.md).

**Zespół odpowiedzialny za:**

- Zespół nadzorujący chmury powinien upewnić się, że każde wdrożenie strefy wyładunkowej jest zgodne z wytycznymi ładu.

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

Każda firma jest unikatowa i w związku z tym ma swoje potrzeby w zakresie zarządzania. Wybierz poziom dojrzałości, który pasuje do Twojej organizacji, i użyj struktury wdrażania w chmurze, aby zapoznać się z praktykami, procesami i narzędziami, które pomogą Ci w tym miejscu.

W miarę rozwoju chmurowego, zespoły są upoważnione do wdrażania chmury w szybszym tępy. Dalsze wysiłki związane z wdrażaniem w chmurze powodują wyzwolenie dojrzałości w operacjach IT. Opracowywanie [zespołu operacji w chmurze](./cloud-operations.md)lub synchronizacja z zespołem operacji w chmurze w celu zapewnienia, że zarządzanie jest częścią rozwoju operacji.
