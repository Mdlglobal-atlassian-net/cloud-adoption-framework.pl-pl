---
title: 'Wprowadzenie: Odblokowywanie projektu i konfiguracji środowiska'
description: Rozpocznij projektowanie i Konfigurowanie środowiska chmury.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 39e5feba4e0d214a86767bf6a2152ae1887dc383
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229797"
---
<!-- docsTest:ignore Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template -->

# <a name="get-started-design-and-configuration"></a>Wprowadzenie: projektowanie i konfiguracja

Projektowanie i konfiguracja środowiska są najczęściej spotykanymi blokadami do migracji lub innowacji ukierunkowanych na wdrażanie. Szybkie wdrożenie projektu, który obsługuje plan wdrożenia długoterminowego, może być trudne. W tym artykule przedstawiono podejście i serie kroków, które mogą pomóc w przezwyciężeniu typowych programów i przyspieszyć wdrażanie.

![Wprowadzenie do projektowania i konfiguracji](../_images/get-started/environment-map.png)

Nakłady pracy wymagane do utworzenia efektywnego projektu i konfiguracji środowiska mogą być złożone, ale zakres może być zarządzany, aby zwiększyć szanse sukcesu zespołu platformy w chmurze. Największe wyzwanie jest wyrównaniem między wieloma uczestnikami, a niektórzy z nich mają uprawnienia do zatrzymywania lub spowalniania podjętych działań. Te kroki przedstawiają sposoby szybkiego zaspokajania krótkoterminowych celów i ustalania długoterminowych sukcesów.

## <a name="step-1-document-the-business-strategy"></a>Krok 1. udokumentowanie strategii biznesowej

Aby uniknąć wspólnych blokad migracji, należy się upewnić, że udokumentowano i zwięzłą strategię biznesową. Wyrównania uczestnika projektu dotyczącej motywacji, oczekiwanego rezultatu biznesowego, a uzasadnienie biznesowe jest ważne w przypadku wdrażania i konfiguracji środowiska.

Jasno i zwięzła Strategia biznesowa pomaga zespołowi Cloud Platform zrozumieć, co jest ważne, i co należy mieć priorytet w przypadku podejmowania decyzji dotyczących konfiguracji środowiska. W szczególności pomaga zespołom podejmować decyzje o wyborze szybkości innowacji lub przenoszonej do kontrolek.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować motywacje, odpowiednie wyniki biznesowe i wysokie uzasadnienie biznesowe.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Motywacje](../strategy/motivations.md): pierwszy krok do strategicznego dostosowywania ma na celu uzyskanie konsensusu na potrzeby motywacji prowadzących do przeprowadzenia migracji. Zacznij od ustalenia i kategoryzacji motywacji oraz wspólnych motywów z różnych uczestników firmy i.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): w przypadku wyrównania motywacji możliwe jest przechwycenie żądanych wyników firmy. Zapewnia to czyszczenie metryk, których można użyć do mierzenia ogólnego przekształcenia.
- [Tworzenie aplikacji do migracji w chmurze](../strategy/cloud-migration-business-case.md): jest to dobry punkt wyjścia do opracowywania przypadku pracy w przypadku migracji, z przejrzystością na temat formuł i narzędzi, które mogą pomóc w uzasadnieniu biznesowym.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe | <li> Zespół platformy w chmurze |

## <a name="step-2-assess-the-digital-estate"></a>Krok 2. Ocena elektronicznej

Funkcja odnajdywania i oceny zapewnia lepszy poziom wyrównania technicznego i pomaga utworzyć plan do działania w celu dostarczenia na strategię. W tym kroku sprawdzaj, czy sprawa biznesowa korzysta z danych o bieżącym stanie środowiska, analizie ilościowej tych danych i szczegółowej ocenie jakościowej obciążeń o najwyższym priorytecie.

Dane wyjściowe tej oceny dotyczą zespołu platformy w chmurze, które mają jasny wgląd w środowisko stanu końcowego i wymagania wymagane do obsługi planu wdrożenia.

**Dostarczane**

- Dane pierwotne w istniejącym spisie.
- Analiza ilościowa istniejącego spisu w celu uściślenia uzasadnienia biznesowego.
- Analiza jakościowa pierwszych 10 obciążeń.
- Zaktualizowano uzasadnienie biznesowe w ramach [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Istniejące systemy spisu](../digital-estate/inventory.md): zrozumienie bieżącego stanu z programistycznego, opartego na danych podejścia to pierwszy krok. Znajdź i Zbierz dane, aby włączyć wszystkie działania oceny.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): Usprawnij wysiłki oceniania, aby skupić się na analizie jakościowej wszystkich zasobów (prawdopodobnie nawet w przypadku obsługi przypadku biznesowego). Następnie należy dodać głęboką analizę jakościową dla pierwszych 10 obciążeń, które mają zostać zmigrowane.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury | <li> Zespół platformy w chmurze |

## <a name="step-3-create-a-cloud-adoption-plan"></a>Krok 3. Tworzenie planu wdrażania chmury

Szablon planu wdrażania w chmurze zapewnia przyspieszone podejście do tworzenia zaległości projektu. Zaległości można następnie zmodyfikować, aby odzwierciedlały wyniki oceny, racjonalizację, umiejętność umiejętności i partnera.

Przegląd krótkoterminowego planu wdrażania i zaległości w chmurze ułatwia zespołowi Cloud Platform zrozumienie potrzeb środowiska w ciągu następnych kilku miesięcy. Pozwala to na przeostrzenie "definicji gotowe" dla pierwszych kilku stref przeładunku.

**Dostarczane**

- Wdróż szablon zaległości.
- Zaktualizuj szablon w celu odzwierciedlenia pierwszych 10 obciążeń do migracji.
- Aktualizuj osoby i szybkość, aby oszacować czas wydania.
- Ryzyka dla osi czasu:
  - Brak wiedzy z usługą Azure DevOps może spowolnić proces wdrażania.
  - Złożoność i dane dostępne dla każdego obciążenia mogą również wpływać na osie czasu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Szablon planu wdrażania w chmurze](../plan/template.md): Wdróż podstawowy szablon.
- [Wyrównanie obciążenia](../plan/workloads.md): Zdefiniuj obciążenia w zaległości.
- [Wyrównanie nakładu pracy](../plan/assets.md): Wyrównaj zasoby i obciążenia w zaległości, aby jasno zdefiniować wysiłki dla obciążeń z priorytetyzacją.
- [Wyrównanie osób i czasu](../plan/iteration-paths.md): Ustanów iteracje, szybkość pracy i wydania dla zmigrowanych obciążeń.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół platformy w chmurze | <li> Zespół platformy w chmurze |

## <a name="step-4-deploy-the-first-landing-zone"></a>Krok 4. wdrażanie pierwszej strefy docelowej

Początkowo zespół wdrażania chmury potrzebuje strefy docelowej, która może obsługiwać wymagania początkowej Wave obciążeń. W miarę upływu czasu strefa docelowa będzie skalowana w celu rozwiązania bardziej złożonych obciążeń. Na razie Zacznij od początkowej strefy wyładunkowej, aby umożliwić wczesną naukę zespołu platform w chmurze i zespołu adopcji rozwiązań w chmurze.

**Dostarczane**

- Wdróż pierwszą strefę docelową dla wstępnych migracji o niskim ryzyku.
- Opracowywanie planu do refaktoryzacji z zespołem usługi Cloud Center doskonałości (CCoE) lub centralnym.
- Ryzyka dla osi czasu:
  - Wymagania dotyczące ładu, operacji i zabezpieczeń dla pierwszych 10 obciążeń mogą znacząco spowolnić ten proces. Rzeczywiste Refaktoryzacja pierwszej strefy docelowej i kolejnych stref wypełniania będzie trwać znacznie dłużej, ale powinny być wykonywane równolegle do wysiłków związanych z migracją.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Wybierz strefę wyładunkowej](../ready/landing-zone/first-landing-zone.md): Użyj tego artykułu, aby znaleźć odpowiednie podejście do wdrożenia strefy docelowej na podstawie planu adopcji krótkoterminowej. Następnie Wdróż tę standardową bazę kodu.
- [Rozwiń swoją strefę](../ready/considerations/index.md)docelową: nie próbuj jeszcze spełnić długoterminowych ograniczeń dotyczących nadzoru, zabezpieczeń ani operacji, chyba że są one wymagane do obsługi planu adopcji krótkoterminowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-deploy-an-initial-governance-foundation"></a>Krok 5. wdrażanie początkowej podstawy ładu

Zarządzanie to kluczowy czynnik do długoterminowego sukcesu dowolnego wysiłku związanego z migracją. Ważna jest szybkość migracji i wpływu na działalność biznesową. Jednak szybkość bez nadzoru może być niebezpieczna. Organizacja musi podejmować decyzje dotyczące ładu, które są zgodne ze wzorcem wdrażania, oraz potrzebom dotyczącym zarządzania i zgodności.

W miarę dokonywania tych decyzji powrócimy do równoległych wysiłków zespołu platformy w chmurze.

**Dostarczane**

- Wdróż początkową podstawę ładu.
- Ukończ test porównawczy, aby zaplanować przyszłe ulepszenia.
- Ryzyka dotyczące osi czasu:-ulepszanie zasad i implementacji ładu może dodać 1-4 tygodni na dyscyplinę.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Podejście do ładu](../govern/index.md): Ta metodologia przedstawia proces planowania zasad i procesów firmowych. Następnie kompilując dyscypliny wymagane do dostarczenia na zarządzanie w ramach działań w chmurze dla przedsiębiorstw.
- [Narzędzie porównawcze zarządzania](../govern/benchmark.md): Znajdź luki w bieżącym stanie, aby można było zaplanować przyszłość.
- [Początkowa ładu](../govern/guides/complex/prescriptive-guidance.md): informacje o dyscyplinach linii bazowej, dyscypliny linii bazowej zabezpieczeń i przyspieszeniu wdrażania wymagane do utworzenia specjalisty dla ładu, który będzie stanowić podstawę dla całego wdrożenia.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Konsultowane zespoły |
| --- | --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe | <li> Zespół platformy w chmurze |

## <a name="step-6-implement-an-operations-baseline"></a>Krok 6. Implementowanie linii bazowej operacji

Zarządzanie operacjami jest kolejną wymaganiem do osiągnięcia sukcesu migracji. Migrowanie do chmury bez znajomości trwających operacji jest ryzykowną decyzją. Równolegle z migracją należy zacząć planowanie operacji na dłuższy okres.

Plany te są tworzone w ramach równoległych wysiłków zespołu platformy w chmurze.

**Dostarczane**

- Wdróż linię bazową zarządzania.
- Ukończ skoroszyt zarządzania operacjami.
- Zidentyfikuj wszystkie obciążenia wymagające oceny przeglądu architektury platformy Azure.
- Ryzyka dla osi czasu:
  - Przejrzyj skoroszyt: jedna godzina dla właściciela aplikacji.
  - Ukończ ocenę przeglądu architektury platformy Azure: godzinę dla aplikacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Plan bazowy zarządzania](../manage/index.md)
- [Zdefiniowanie zobowiązań biznesowych](../manage/considerations/business-alignment.md)
- [Rozwinięcie planu bazowego zarządzania](../manage/best-practices.md)
- [Uzyskaj specyficzne dla operacji zaawansowanych](../manage/design-principles.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Konsultowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe | <li> Zespół platformy w chmurze |

## <a name="step-7-expand-the-landing-zone"></a>Krok 7. rozszerzanie strefy docelowej

Zespół ds. wdrażania w chmurze rozpoczyna swoją pierwszą liczbę migracji, zespół platformy w chmurze może rozpocząć tworzenie do konfiguracji środowiska stanu końcowego dzięki obsłudze zarządzania chmurą i zespołom operacji w chmurze. W zależności od tempa planu wdrażania w chmurze może to być konieczne w przypadku wersji iteracyjnych, co pozwala dodać funkcjonalność przed wymaganiami planu wdrażania.

**Dostarczane**

- Należy zastosować podejście programistyczne oparte na testach w celu refaktoryzacji stref wyładunkowej.
- Usprawnij zarządzanie strefami wyładunkowymi.
- Rozwiń operacje strefy wyładunkowej.
- Zaimplementuj zabezpieczenia strefy wyładunkowej.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Refaktoryzacja stref wyładunkowej](../ready/landing-zone/refactor.md)
- [Tworzenie na podstawie testów stref wyładunkowych](../ready/considerations/test-driven-development.md)
- [Rozwiń węzeł Zarządzanie strefami przeładunkowymi](../ready/considerations/landing-zone-governance.md)
- [Rozwiń operacje strefy wyładunkowej](../ready/considerations/landing-zone-operations.md)
- [Rozwiń węzeł zabezpieczenia strefy wyładunkowej](../ready/considerations/landing-zone-security.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Kroki opisane w tym przewodniku mogą ułatwić Ci i zespołom przyspieszanie swojej ścieżki do środowiska chmury gotowego dla przedsiębiorstwa, które jest prawidłowo skonfigurowane.

## <a name="next-steps"></a>Następne kroki

Należy wziąć pod uwagę następujące kolejne kroki w przyszłych iteracjach, aby skompilować swoje początkowe wysiłki:

- [Ścieżki szkoleniowe o gotowości technicznej dotyczącej środowiska](../ready/suggested-skills.md)
- [Lista kontrolna planowania środowiska migracji](../migrate/migration-considerations/prerequisites/planning-checklist.md)
