---
title: 'Wprowadzenie: Odblokowywanie projektu i konfiguracji środowiska'
description: Rozpocznij projektowanie i Konfigurowanie środowiska chmury.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 761c6c7a8bed468a7d2c9005365a815fbe48e8ae
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752880"
---
# <a name="get-started-design-and-configuration"></a>Wprowadzenie: projektowanie i konfiguracja

Projektowanie i konfiguracja środowiska są najczęściej spotykanymi blokadami, które mają na celu wdrażanie działań skoncentrowanych na migracji lub innowacyjności. Szybkie wdrożenie projektu, który obsługuje plan wdrożenia długoterminowego, może być trudne. W tym artykule przedstawiono podejście i serie kroków, które mogą pomóc w przezwyciężeniu typowych programów i przyspieszyć wdrażanie.

![Wprowadzenie do projektowania i konfiguracji](../_images/get-started/environment-map.png)

Nakłady pracy wymagane do utworzenia efektywnego projektu i konfiguracji środowiska mogą być złożone. Możesz zarządzać zakresem, aby zwiększyć szanse sukcesu zespołu platformy w chmurze. Największe wyzwanie jest wyrównaniem między wieloma uczestnikami. Niektórzy z tych udziałowców mają uprawnienia do zatrzymywania lub spowalniania działań związanych z wdrażaniem. Te kroki przedstawiają sposoby szybkiego zaspokajania krótkoterminowych celów i ustalania długoterminowych sukcesów.

## <a name="step-1-document-the-business-strategy"></a>Krok 1. udokumentowanie strategii biznesowej

Aby uniknąć wspólnych blokad migracji, należy się upewnić, że masz jasno i zwięzłą strategię biznesową. Wyrównania uczestnika projektu dotyczącej motywacji, oczekiwanego rezultatu biznesowego, a uzasadnienie biznesowe jest ważne w przypadku wdrażania i konfiguracji środowiska.

Jasno i zwięzła Strategia biznesowa pomaga zespołowi Cloud Platform zrozumieć, co jest ważne, i co należy mieć priorytet w przypadku podejmowania decyzji dotyczących konfiguracji środowiska. W szczególności pomaga zespołom podejmować decyzje, gdy są zmuszeni do wyboru szybkości innowacji lub przełączenia do kontrolek.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować motywacje, odpowiednie wyniki biznesowe i wysokie uzasadnienie biznesowe.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Motywacje](../strategy/motivations.md): pierwszy krok do dostosowania strategicznego ma na celu wyrażenie zgody na motywacje, które zwiększają nakłady pracy związane z migracją. Zacznij od ustalenia i kategoryzacji motywacji oraz wspólnych motywów z różnych uczestników firmy i.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): po wyrównaniu motywacji możliwe jest przechwycenie żądanych wyników firmy. Te informacje zapewniają jasne metryki, których można użyć do mierzenia ogólnego przekształcenia.
- [Tworzenie sprawy biznesowej migracji do chmury](../strategy/cloud-migration-business-case.md): teraz można rozpocząć opracowywanie przypadku biznesowego migracji z wyraźnymi wskazówkami dotyczącymi formuł i narzędzi, które mogą pomóc w uzasadnieniu biznesowym.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe | <li> Zespół platformy w chmurze |

## <a name="step-2-assess-the-digital-estate"></a>Krok 2. Ocena elektronicznej

Funkcja odnajdywania i oceny zapewnia lepszy poziom wyrównania technicznego, który pomaga utworzyć plan akcji, którego można użyć do dostarczenia strategii. W tym kroku sprawdzasz poprawność przypadku biznesowego za pomocą danych o bieżącym stanie środowiska. Następnie należy przeprowadzić analizę ilościową tych danych i szczegółową ocenę jakościową obciążeń o najwyższym priorytecie.

Dane wyjściowe oceny typu cyfrowego zapewniają zespołowi usługi Cloud platformom jasny wgląd w środowisko stanu końcowego i wymagania, które są niezbędne do obsługi planu wdrożenia.

**Dostarczane**

- Dane pierwotne w istniejącym spisie.
- Analiza ilościowa istniejącego spisu w celu uściślenia uzasadnienia biznesowego.
- Analiza jakościowa pierwszych 10 obciążeń.
- Zaktualizowano uzasadnienie biznesowe w ramach [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Istniejące systemy spisu](../digital-estate/inventory.md): zrozumienie bieżącego stanu z programistycznego, opartego na danych podejścia to pierwszy krok. Znajdź i Zbierz dane, aby włączyć wszystkie działania oceny.
- Ocena [przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): Usprawnij wysiłki oceny, aby skoncentrować się na analizie jakościowej wszystkich zasobów, prawdopodobnie nawet w przypadku obsługi przypadku biznesowego. Następnie należy dodać głęboką analizę jakościową dla pierwszych 10 obciążeń, które mają zostać zmigrowane.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury | <li> Zespół platformy w chmurze |

## <a name="step-3-create-a-cloud-adoption-plan"></a>Krok 3. Tworzenie planu wdrażania chmury

Szablon planu wdrażania w chmurze zapewnia przyspieszone podejście do tworzenia zaległości projektu. Zaległości można następnie zmodyfikować, aby odzwierciedlały wyniki oceny, racjonalizację, wymagane umiejętności i umowę partnera.

Przegląd krótkoterminowego planu wdrażania i zaległości w chmurze ułatwia zespołowi Cloud Platform zrozumienie potrzeb środowiska w ciągu następnych kilku miesięcy. To tło pozwala im wzmocnić "definicję gotowe" dla pierwszych kilku stref.

**Dostarczane**

- Wdróż szablon zaległości.
- Zaktualizuj szablon w celu odzwierciedlenia pierwszych 10 obciążeń, które mają zostać zmigrowane.
- Aktualizuj osoby i szybkość pracy (czas pracy), aby oszacować czas wydania.
- Ryzyka dla osi czasu:
  - Brak wiedzy z usługą Azure DevOps może spowolnić proces wdrażania.
  - Złożoność i dane dostępne dla każdego obciążenia mogą również wpływać na osie czasu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Szablon planu wdrażania w chmurze](../plan/template.md): Wdróż podstawowy szablon.
- [Wyrównanie obciążenia](../plan/workloads.md): Zdefiniuj obciążenia w zaległości.
- [Wyrównanie nakładu pracy](../plan/assets.md): Wyrównaj zasoby i obciążenia w zaległości, aby jasno zdefiniować wysiłki dla obciążeń z priorytetyzacją.
- [Wyrównanie osób i czasu](../plan/iteration-paths.md): Ustanów iteracje, szybkość i wydania dla zmigrowanych obciążeń.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Poinformowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Zespół platformy w chmurze | <li> Zespół platformy w chmurze |

## <a name="step-4-deploy-the-first-landing-zone"></a>Krok 4. wdrażanie pierwszej strefy docelowej

Początkowo zespół wdrażania w chmurze potrzebuje strefy docelowej, która może obsługiwać wymagania pierwszej Wave obciążeń. W miarę upływu czasu strefa docelowa skaluje się w celu rozwiązania bardziej złożonych obciążeń. Na razie Zacznij od strefy wyładunkowej, która umożliwia wczesną naukę zespołu platform w chmurze i zespołu adopcji rozwiązań w chmurze.

**Dostarczane**

- Wdróż pierwszą strefę docelową dla wstępnych migracji o niskim ryzyku.
- Utwórz plan do refaktoryzacji w centrum usługi Cloud Center dla zespołu doskonałości lub centralnie.
- Ryzyka dla osi czasu:
  - Wymagania dotyczące ładu, operacji i zabezpieczeń dla pierwszych 10 obciążeń mogą spowolnić ten proces. Rzeczywiste Refaktoryzacja pierwszej strefy docelowej i kolejnych stref wypełniania trwa dłużej, ale powinno się to zdarzyć równolegle z wysiłkami migracji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Wybierz strefę wyładunkowej](../ready/landing-zone/first-landing-zone.md): Użyj tego artykułu, aby znaleźć odpowiednie podejście do wdrożenia strefy docelowej na podstawie planu adopcji krótkoterminowej. Następnie Wdróż tę standardową bazę kodu.
- [Rozwiń swoją strefę](../ready/considerations/index.md)docelową: nie podejmuj jeszcze starań, aby spełnić długoterminowe ograniczenia dotyczące zarządzania, zabezpieczeń lub operacji, chyba że są one wymagane do obsługi planu adopcji krótkoterminowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-deploy-an-initial-governance-foundation"></a>Krok 5. wdrażanie początkowej podstawy ładu

Zarządzanie to kluczowy czynnik do długoterminowego sukcesu dowolnego wysiłku związanego z migracją. Ważna jest szybkość migracji i wpływu na działalność biznesową. Jednak szybkość bez nadzoru może być niebezpieczna. Organizacja musi podejmować decyzje dotyczące ładu, które są zgodne ze wzorcem wdrożenia i wymaganiami dotyczącymi zarządzania i zgodności.

W miarę dokonywania tych decyzji powracają one do równoległych wysiłków zespołu platformy w chmurze.

**Dostarczane**

- Wdróż początkową podstawę ładu.
- Ukończ test porównawczy, aby zaplanować przyszłe ulepszenia.
- Ryzyka dla osi czasu:
  - Zasady poprawy i wdrożenia ładu mogą dodać jeden do czterech tygodni na dyscyplinę.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Podejście do ładu](../govern/index.md): Ta metodologia przedstawia proces planowania zasad i procesów firmowych. Następnie Kompiluj dyscypliny wymagane do dostarczenia na zarządzanie w ramach działań w chmurze dla przedsiębiorstw.
- [Narzędzie porównawcze zarządzania](../govern/benchmark.md): Znajdź luki w bieżącym stanie, aby można było zaplanować przyszłość.
- [Początkowa ładu](../govern/guides/complex/prescriptive-guidance.md): zrozumienie dyscypliny linii bazowej, dyscypliny linii bazowej zabezpieczeń i przyspieszenia wdrożenia, które są wymagane do utworzenia minimalnego produktu, który ma być używany jako podstawa dla całego wdrożenia.

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
- Zidentyfikuj wszystkie obciążenia, które wymagają Microsoft Azureej oceny z obsługą architektury.
- Ryzyka dla osi czasu:
  - Przejrzyj skoroszyt: Oszacuj godzinę dla właściciela aplikacji.
  - Ukończ Microsoft Azure dobrze zaprojektowanej ocenie przeglądu: Oszacuj godzinę dla każdej aplikacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Ustalenie planu bazowego zarządzania](../manage/index.md)
- [Zdefiniowanie zobowiązań biznesowych](../manage/considerations/business-alignment.md)
- [Rozwinięcie planu bazowego zarządzania](../manage/best-practices.md)
- [Uzyskaj specyficzne dla operacji zaawansowanych](../manage/design-principles.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające | Konsultowane zespoły |
| --- | --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe | <li> Zespół platformy w chmurze |

## <a name="step-7-expand-the-landing-zone"></a>Krok 7. rozszerzanie strefy docelowej

Zespół ds. wdrażania w chmurze rozpoczyna swoją pierwszą liczbę migracji, zespół platformy Cloud Platform może rozpocząć tworzenie w kierunku konfiguracji środowiska stanu końcowego dzięki obsłudze zarządzania chmurą i zespołom operacji w chmurze. W zależności od tempa planu wdrażania w chmurze ten proces może być konieczny w przypadku wersji iteracyjnych. Funkcje mogą być dodawane przed wymaganiami planu wdrażania.

**Dostarczane**

- Należy zastosować podejście programistyczne oparte na testach w celu refaktoryzacji stref wyładunkowej.
- Usprawnij zarządzanie strefami wyładunkowymi.
- Rozwiń operacje strefy wyładunkowej.
- Zaimplementuj zabezpieczenia strefy wyładunkowej.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Refaktoryzacja stref docelowych](../ready/landing-zone/refactor.md)
- [Rozwój stref docelowych oparty na testach](../ready/considerations/test-driven-development.md)
- [Rozwiń węzeł Zarządzanie strefami przeładunkowymi](../ready/considerations/landing-zone-governance.md)
- [Rozwiń operacje strefy wyładunkowej](../ready/considerations/landing-zone-operations.md)
- [Rozwiń węzeł zabezpieczenia strefy wyładunkowej](../ready/considerations/landing-zone-security.md)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Kroki opisane w tym przewodniku mogą ułatwić Ci i zespołom przyspieszanie swojej ścieżki do środowiska chmury gotowego dla przedsiębiorstwa, które zostało prawidłowo skonfigurowane.

## <a name="next-steps"></a>Następne kroki

Należy wziąć pod uwagę następujące kolejne kroki w przyszłych iteracjach, aby skompilować swoje początkowe wysiłki:

- [Ścieżki szkoleniowe o gotowości technicznej dotyczącej środowiska](../ready/suggested-skills.md)
- [Lista kontrolna planowania środowiska migracji](../migrate/migration-considerations/prerequisites/planning-checklist.md)
