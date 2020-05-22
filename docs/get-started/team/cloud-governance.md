---
title: 'Wprowadzenie: Tworzenie zespołu ładu w chmurze'
description: Ustanów zakres, elementy dostarczane i możliwości zespołu nadzoru, aby przygotować się do pomyślnego zarządzania chmurą.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 3b50d45457eb65b0a97a435dcd2d8e70fadc246d
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752051"
---
# <a name="get-started-build-a-cloud-governance-team"></a>Wprowadzenie: Tworzenie zespołu ładu w chmurze

Zespół zarządzający chmurą gwarantuje, że ryzyko związane z wdrażaniem w chmurze i odporność na ryzyko są prawidłowo oceniane i zarządzane. Zespół identyfikuje zagrożenia, które nie mogą być tolerowane przez firmę, i konwertuje ryzyko na zasady firmowe.

![Wprowadzenie do tworzenia zespołu zarządzania chmurą](../../_images/get-started/governance-team-map.png)

## <a name="step-1-determine-whether-a-cloud-governance-team-is-needed"></a>Krok 1. ustalenie, czy zespół nadzoru w chmurze jest wymagany

Oficjalne wskazówki dotyczące struktury wdrażania w chmurze dla platformy Azure to zawsze Tworzenie zespołu nadzoru chmurowego. Na początku zespół może być wyjątkowo mały. Bez względu na jego rozmiar rola będzie ważna. Jeśli zespół nie jest wymagany, Grupa lub osoba, która znajduje się w istniejącym zespole przyjęcia, powinna wyrazić zgodę na spełnienie obowiązków związanych z [funkcjami ładu w chmurze](../../organize/cloud-governance.md).

**Dostarczane**

- Ustal, czy potrzebujesz zespołu nadzoru w chmurze.
- Udokumentowanie decyzji i osób odpowiedzialnych w [Raci (odpowiedzialnych, do których można się skontaktować i poinformowanie o nich)](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) , wybierając kartę **wyrównanie organizacji** .

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Funkcje ładu chmury](../../organize/cloud-governance.md) mogą już być rozłożone na wielu użytkowników lub zespoły. Posiadanie zespołu, który przechodzi przez tytuł "zespół ds. zarządzania chmurą" nie jest ważne, ale wymagane możliwości powinny znajdować się na stronie lub w zespole.
- Jeśli długoterminowa strategia wdrażania chmury w firmie może zostać dostarczona z jednej strefy wyładunkowej w jednym środowisku chmury, ilość działań związanych z zarządzaniem i operacjami może być wystarczająco mała do dostarczenia przez jedną osobę lub jednego zespołu. Jest mało prawdopodobne, że zespół nadzoruje chmurę, ponieważ obsługuje wiele funkcji poza nadzorem w chmurze. Nawet dla tego zespołu Przewodnik ten może pomóc w zapewnieniu, że może on dostarczyć na ważną funkcję ładu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury |

## <a name="step-2-align-with-other-teams"></a>Krok 2. Wyrównywanie z innymi zespołami

Zespół nadzoru gwarantuje spójność i zgodność z zestawem wspólnych zasad. Te zasady pochodzą z ciągłego wyrównania z innymi zespołami.

Przed ustaleniem zasad lub zautomatyzowanym nadzorem w chmurze zespół nadzorujący chmury powinien spełnić inne zespoły, które są określone w szablonie RACI. Pomoże to zapewnić wyrównanie najważniejszych tematów, takich jak zabezpieczenia, koszt, wydajność, operacje i wdrażanie. Kroki 4 i 5 mogą ułatwić wyrównania.

**Dostarczane**

- Omawiaj implementację bieżącego stanu i bieżące plany przyjęcia dla każdego zespołu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [strategią i planem planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) swojej firmy, korzystając z członków zespołu strategii chmury, aby zrozumieć motywacje, metryki i strategię.
- Zapoznaj się z [szablonem planu wdrożenia chmury](../../plan/template.md) w firmie z członkami zespołu wdrażania chmury, aby zrozumieć osie czasu i priorytetyzację.
- Przejrzyj [skoroszyt zarządzania](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) operacjami zespołu operacji, aby zrozumieć wymagania operacyjne i zobowiązania, które zostały nawiązane z firmą.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół ds. operacji w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-establish-a-cadence-with-other-teams"></a>Krok 3. nawiązanie erze z innymi zespołami

Wdrażanie w chmurze zwykle znajduje się w fale lub wersjach. Regularna erze, która jest wyrównana z tymi wersjami, umożliwia zespołowi nadzoru chmurowego wyszukiwanie i zrozumienie zagrożeń, które zostaną wprowadzone w następnej fazie Wave. Zaangażowanie się z strategiami, wdrażaniem i zespołami operacyjnymi podczas planowania i przeglądów pomaga również zespołowi nadzoru nadal korzystać z zagrożeń.

**Dostarczane**

- Ustanów erze z każdym z zespołów pomocniczych. Jeśli to możliwe, Wyrównaj ten erze z cyklami wydań i planowania.
- Ustanów osobne erze bezpośrednio z zespołem ds. strategii chmury (lub różnych członków zespołu), aby zapoznać się z ryzykiem, które są związane z następną analizą przyjęcia i ocenić poziom tolerancji dla tego ryzyka.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Aby uzyskać dodatkowe wskazówki dotyczące cadences na potrzeby spotkań, zapoznaj się z sekcją "informacje o dostarczeniu" [funkcji zarządzania chmurą](../../organize/cloud-governance.md#deliverable).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Zespół ds. operacji w chmurze |

## <a name="step-4-review-the-methodology"></a>Krok 4: przegląd metodologii

Aby pomóc w ustaleniu przyszłej wizji dotyczącej zarządzania i współpracy z tym wzrokiem, zapoznaj się z metodologią rozwiązania w zakresie wdrażania w chmurze.

**Dostarczane**

- Uzyskaj zrozumienie metodologii, podejścia i implementacji, które wspierają metodologię zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z [metodologią zarządzania](../../govern/methodology.md).

**Zespół odpowiedzialny za:**

- Zespół ds. zarządzania chmurą jest odpowiedzialny za ustanawianie wizji i podejście do ładu.

## <a name="step-5-complete-the-governance-benchmark"></a>Krok 5. Kończenie testu porównawczego ładu

Zarządzanie to szeroki temat. Krótka ocena może pomóc zespołowi zrozumieć, gdzie rozpocząć pracę.

**Dostarczane**

- Ukończ ocenę testu porównawczego, który jest oparty na konwersacjach z różnymi uczestnikami projektu. Lub poproszenie innych zespołów o samodzielne przeprowadzenie oceny.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Oceń potrzeby i priorytety związane z zarządzaniem za pomocą [testu porównawczego](../../govern/benchmark.md).

**Zespół odpowiedzialny za:**

- Zespół nadzorujący chmur powinien zrozumieć luki, które są identyfikowane w teście porównawczym, a następnie zapewnić kierownictwo, który pomaga rozwiązywać przerwy.

## <a name="step-6-implement-the-initial-governance-best-practice-and-configuration"></a>Krok 6. Implementowanie początkowego najlepszego rozwiązania i konfiguracji zarządzania

Metodologia rządząca obejmuje dwa podejścia do początkowego ładu. Przejrzyj każde podejście i zaimplementuj te, które najlepiej pasują do Twoich potrzeb.

**Dostarczane**

- Wdróż podstawowe narzędzia do zarządzania i konfiguracje organizacji, które są wymagane do zarządzania środowiskiem w ciągu najbliższych kilku wysiłków.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Aby uzyskać wskazówki dotyczące konfiguracji i implementacji, zapoznaj [się z tematem wstępne zarządzanie chmurą](../../govern/initial-foundation.md).

**Zespół odpowiedzialny za:**

- Zespół ds. nadzoru chmurowego jest odpowiedzialny za przegląd i wdrażanie najlepszych rozwiązań z zakresu nadzoru i początkowej usługi ładu.

## <a name="step-7-continuously-improve-governance-maturity"></a>Krok 7. ciągłe ulepszanie okresu ważności ładu

Wymagania dotyczące ładu zwiększają się wraz z ukończeniem dodatkowych działań związanych z wdrażaniem w chmurze. Zachowaj zgodność z ciągłym planem wdrożenia, aby mieć pewność, że podejście do nadzoru może utrzymywać odpowiednie poziomy zarządzania i kontroli.

**Dostarczane**

- Zaimplementuj usprawnienia ładu chroniące przed zmianami ryzyka i potrzebami zarządzania.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Aby pomóc w ulepszaniu początkowej podstawy ładu, zaimplementuj [rozwinięte scenariusze ładu](../../govern/foundation-improvements.md).

**Zespół odpowiedzialny za:**

- Zespół ds. zarządzania chmurą jest odpowiedzialny za dostosowanie z ciągłymi planami wdrażania.

## <a name="step-8-evaluate-landing-zone-changes"></a>Krok 8. oszacowanie zmian strefy wyładunkowej

Gdy strefy wyładunkowe są wdrażane i rozszerzane, mogą pojawić się nowe zagrożenia lub naruszenia zasad zarządzania. Okresowo Przeglądaj konfiguracje stref wyładunkowych, aby zidentyfikować wszelkie odchylenia od zasad, które nie są przechwytywane przez natywne narzędzia do zarządzania w chmurze. Upewnij się, że każde wdrożenie strefy docelowej jest zgodne z wytycznymi dotyczącymi nadzoru strefy docelowej.

**Dostarczane**

- Pomóż zespołowi Cloud Platform w opracowaniu ulepszeń strefy docelowej, która musi być zgodna z zasadami ładu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Usprawnij [Zarządzanie strefami wyładunkowymi](../../ready/considerations/landing-zone-governance.md).

**Zespół odpowiedzialny za:**

- Zespół nadzorujący chmury powinien upewnić się, że każde wdrożenie strefy wyładunkowej jest zgodne z wytycznymi ładu.

## <a name="step-9-adoption-handoffs"></a>Krok 9. wdrażanie etapach

Po zakończeniu nowych działań związanych z wdrażaniem w chmurze zespół ds. wdrożenia chmury wychodzi z obowiązków operacyjnych do zespołu operacji w chmurze i zespołów nadzoru chmurowego. Zachowaj zgodność z pakietem Release cadences, aby zapewnić odpowiednią dokumentację i wyrównanie zasad, i aby pomóc zespołowi przyjąć odpowiedzialność za obciążenia.

**Dostarczane**

- Regularnie Przeglądaj i Akceptuj etapach z innych zespołów wdrażania w chmurze.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Ustanów proces dołączania [nowych obciążeń i zasobów](https://docs.microsoft.com/azure/azure-resource-manager/custom-providers/concepts-resource-onboarding).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespoły wdrażania chmury | <li> Zespół nadzorujący chmury <li> Zespół ds. operacji w chmurze |

## <a name="whats-next"></a>Co dalej

Wszystkie firmy są unikatowe i w związku z tym mają swoje potrzeby w zakresie zarządzania. Wybierz poziom dojrzałości, który pasuje do Twojej organizacji, i użyj struktury wdrażania w chmurze, aby zapoznać się z praktykami, procesami i narzędziami, które mogą pomóc w tym miejscu.

W miarę rozwoju chmurowego, zespoły mają prawo do szybszego wdrożenia chmury. Ciągłe działania związane z wdrażaniem w chmurze mają na celu wyzwolenie dojrzałości w operacjach IT. Aby zapewnić, że zarządzanie jest częścią rozwoju operacji, należy opracować [zespół operacyjny w chmurze](./cloud-operations.md) lub zsynchronizować z istniejącym zespołem operacji w chmurze.
