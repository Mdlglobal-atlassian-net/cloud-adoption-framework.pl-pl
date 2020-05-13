---
title: 'Wprowadzenie: przyspieszanie migracji'
description: Zalecane kroki dotyczące wyrównania uczestnika projektu, planowania migracji, wdrażania strefy docelowej i migrowania pierwszych 10 obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: d45898c16e7894a62d65e991737419964a570e34
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229576"
---
# <a name="get-started-accelerate-migration"></a>Wprowadzenie: przyspieszanie migracji

Właściwe wyrównania biznesowe i zainteresowanych działów IT mogą pomóc organizacji w pokonaniu przeszkody migracji i przyspieszeniu wysiłków migracji. W tym artykule przedstawiono zalecane kroki, które należy wykonać w celu wyrównania przez uczestnika projektu, planowania migracji, wdrożenia strefy docelowej i migracji pierwszych 10 obciążeń. Może ona również pomóc Ci w długotrwałym pomyślnym przewidzianym przez właściwy nadzór i zarządzanie.

Skorzystaj z tego przewodnika, aby zmniejszyć ilość materiałów i procesy wymagane do dopasowania ogólnego wysiłku migracji. Ten proces wykorzystuje sekcje struktury wdrażania chmury, które zostały wyróżnione na poniższej ilustracji.

![Wprowadzenie do migracji na platformie Azure](../_images/get-started/migration-map.png)

Jeśli Twój Scenariusz migracji jest nietypowy, możesz uzyskać spersonalizowaną ocenę gotowości do migracji w organizacji za pomocą [oceny strategicznej migracji i narzędzia gotowości](https://docs.microsoft.com/assessments/?id=strategic-migration-assessment) , aby zidentyfikować wskazówki, które najlepiej odpowiadają bieżącym potrzebom.

## <a name="get-started"></a>Rozpoczęcie pracy

Nakłady techniczne i proces wymagany do migracji obciążeń są stosunkowo proste. Efektywne zakończenie procesu migracji jest ważne. Strategiczna gotowość do migracji będzie jednak mieć jeszcze większy wpływ na osie czasu i pomyślne ukończenie ogólnej migracji.

Przyspieszenie wdrożenia oznacza rozjęcie czynności wymaganych do obsługi zespołu wdrażania chmury podczas migracji. W tym przewodniku opisano te iteracyjne zadania w formacie liniowej listy kontrolnej, aby ułatwić klientom rozpoczęcie właściwej ścieżki do migracji w chmurze. Aby zilustrować znaczenie kroków pomocniczych, migracja jest wymieniona w kroku 10 w tym artykule. W rzeczywistości zespół ds. wdrażania chmury prawdopodobnie rozpocznie swoją pierwszą migrację pilotażową równolegle z krokami 4 lub 5.

## <a name="step-1-align-stakeholders"></a>Krok 1. Wyrównywanie uczestników projektu

Aby uniknąć wspólnych blokad migracji, należy utworzyć jasno i zwięzłą strategię biznesową dla migracji. Wyrównania uczestnika projektu dotyczącego motywacji i oczekiwanych wyników działalności biznesowej będą kształtować decyzje podejmowane przez zespół rozwiązań w chmurze.

- [Motywacje](../strategy/motivations.md): pierwszy krok do strategicznego dostosowywania ma na celu uzyskanie konsensusu na potrzeby motywacji prowadzących do przeprowadzenia migracji. Zacznij od ustalenia i kategoryzacji motywacji oraz wspólnych motywów z różnych uczestników firmy i.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): w przypadku wyrównania motywacji możliwe jest przechwycenie żądanych wyników firmy. Zapewnia to wyraźne metryki, za pomocą których można mierzyć ogólną transformację.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować motywacje i żądane wyniki biznesowe.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-align-partner-support"></a>Krok 2. wyrównanie wsparcia partnera

Partnerzy, usługi firmy Microsoft lub różne programy firmy Microsoft są dostępne do obsługi przez cały proces migracji.

- [Poznaj opcje partnerstwa](../migrate/migration-considerations/assess/partnership-options.md) , aby znaleźć odpowiedni poziom partnerstwa i pomocy technicznej.

**Dostarczane**

- Ustalanie warunków i postanowień lub innych umów umownych przed zaangażowaniem partnera pomocniczego.
- Zidentyfikuj zatwierdzonych partnerów w ramach [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Krok 3. zbieranie danych i analizowanie zasobów i obciążeń

Odnajdywanie i Ocena zapewniają lepszy poziom wyrównania technicznego w celu utworzenia planu umożliwiającego podjęcie odpowiednich działań. W tym kroku sprawa biznesowa jest weryfikowana przy użyciu danych o bieżącym środowisku stanu, analizie ilościowej tych danych i głębokiej ocenie jakościowej obciążeń o najwyższym priorytecie.

- [Istniejące systemy spisu](../digital-estate/inventory.md): zrozumienie bieżącego stanu z programistycznego, opartego na danych podejścia to pierwszy krok. Odkryj i Zbierz dane, aby włączyć wszystkie działania oceny.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): Usprawnij wysiłki oceniania, aby skupić się na analizie jakościowej wszystkich zasobów (prawdopodobnie nawet w przypadku obsługi przypadku biznesowego). Następnie należy dodać głęboką analizę jakościową dla pierwszych 10 obciążeń, które mają zostać zmigrowane.

**Dostarczane**

- Dane pierwotne w istniejącym spisie.
- Analiza ilościowa istniejącego spisu w celu uściślenia uzasadnienia biznesowego.
- Analiza jakościowa pierwszych 10 obciążeń.
- Aktualizacja uzasadnienia biznesowego w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury |

## <a name="step-4-make-a-business-case"></a>Krok 4. Tworzenie przypadku biznesowego

Jeśli przypadek biznesowy do migracji będzie prawdopodobnie iteracyjną konwersacją między uczestnikami projektu. W pierwszym miejscu podczas tworzenia przypadku biznesowego należy oszacować początkowy zwrot wysokiego poziomu z potencjalnej migracji do chmury. Celem tego kroku jest upewnienie się, że wszystkie zainteresowane strony będą wyrównane do jednego z prostych pytań: "w oparciu o dostępną datę, jest ogólnym przyjęciem w chmurze decyzji biznesowej?".

- [Tworzenie aplikacji do migracji w chmurze](../strategy/cloud-migration-business-case.md) to dobry punkt wyjścia do tworzenia przypadku pracy w przypadku migracji, z przejrzystością na temat formuł i narzędzi, które mogą pomóc w uzasadnieniu biznesowym.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować uzasadnienie biznesowe.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury |

## <a name="step-5-create-a-migration-plan"></a>Krok 5. Tworzenie planu migracji

Szablon planu wdrażania w chmurze zapewnia przyspieszone podejście do tworzenia zaległości projektu. Zaległości można następnie zmodyfikować, aby odzwierciedlały wyniki odnajdywania, racjonalizację, umiejętność i swoją umowę.

- [Szablon planu wdrażania w chmurze](../plan/template.md): Wdróż podstawowy szablon.
- [Wyrównanie obciążenia](../plan/workloads.md): Zdefiniuj obciążenia w zaległości.
- [Wyrównanie nakładu pracy](../plan/assets.md): Wyrównaj zasoby i obciążenia w zaległości, aby jasno zdefiniować nakład pracy dla obciążeń z priorytetyzacją.
- [Wyrównanie osób i czasu](../plan/iteration-paths.md): Ustanów iteracje, szybkość pracy i wydania dla zmigrowanych obciążeń.

**Dostarczane**

- Wdróż szablon zaległości.
- Zaktualizuj szablon w celu odzwierciedlenia pierwszych 10 obciążeń do migracji.
- Aktualizuj osoby i szybkość, aby oszacować czas wydania.
- Ryzyka dla osi czasu:
  - Brak wiedzy z usługą Azure DevOps może spowolnić proces wdrażania.
  - Złożoność i dane dostępne dla każdego obciążenia mogą również wpływać na osie czasu.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury |

## <a name="step-6-build-a-skills-readiness-plan"></a>Krok 6. Tworzenie planu gotowości do kwalifikacji

Istniejący pracownicy mogą odgrywać rolę praktyczną w ramach wysiłków związanych z migracją. Mogą jednak być wymagane dodatkowe umiejętności. W tym kroku zespół będzie samooceny, aby identyfikować okazje do rozwoju umiejętności lub użyć partnerów w celu rozszerzenia tych umiejętności.

- [Utwórz plan gotowości do kwalifikacji](../plan/adapt-roles-skills-processes.md). Szybko Oceń wymagane i istniejące umiejętności, aby lepiej zrozumieć, jakie wymagania dotyczące kwalifikacji powinny być rozkierowane.

**Dostarczane**

- Dodaj plan gotowości do umiejętności [i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury |

## <a name="step-7-deploy-and-align-a-landing-zone"></a>Krok 7. wdrażanie i wyrównywanie strefy docelowej

Wszystkie zmigrowane zasoby są wdrażane w ramach strefy docelowej. Początkowo strefa docelowa będzie uproszczony do obsługi mniejszych obciążeń. W miarę upływu czasu skalowanie zostanie rozbudowane pod kątem bardziej złożonych obciążeń.

- [Wybierz strefę wyładunkowej](../ready/landing-zone/first-landing-zone.md): Użyj tego artykułu, aby znaleźć odpowiednie podejście do wdrożenia strefy docelowej na podstawie wzorca wdrożenia. Następnie Wdróż tę standardową bazę kodu.
- [Rozszerzanie strefy docelowej](../ready/considerations/index.md): niezależnie od punktu początkowego Zidentyfikuj luki w wdrożonej strefie docelowej, aby dodać wymagane składniki organizacji, zabezpieczeń, nadzoru, zgodności, operacji i tak dalej.

**Dostarczane**

- Wdróż pierwszą strefę docelową na potrzeby wstępnej migracji o niskim ryzyku.
- Utwórz plan do refaktoryzacji przy użyciu CCoE lub centralnych.
- Ryzyka dla osi czasu:
  - Wymagania dotyczące ładu, operacji i zabezpieczeń dla pierwszych 10 obciążeń mogą znacząco spowolnić ten proces.
  - Rzeczywiste Refaktoryzacja pierwszej strefy docelowej i kolejnych stref wypełniania będzie trwać znacznie dłużej, ale powinny być wykonywane równolegle do wysiłków związanych z migracją.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-8-migrate-your-first-10-workloads"></a>Krok 8. Migrowanie pierwszych 10 obciążeń

Nakłady techniczne wymagane do przeprowadzenia migracji pierwszych 10 obciążeń są stosunkowo proste. Jest to również proces iteracyjny, który będzie powtarzany podczas migracji większej liczby zasobów. Proces obejmuje ocenę obciążeń (zobacz **krok 4**), wdrożenie obciążeń, a następnie zwolnienie ich do środowiska produkcyjnego.

![Fazy iteracji migracji: Ocena, wdrażanie, wydanie](../_images/migrate/methodology-effort-only.png)

Narzędzia migracji do chmury umożliwiają Migrowanie wszystkich maszyn wirtualnych w centrum danych w jednym przebiegu lub iteracji. Jednak jest to bardziej powszechne w przypadku migrowania mniejszej liczby obciążeń podczas każdej iteracji. Rozdzielenie migracji na mniejsze fale lub wydania wymaga większego planowania, ale zmniejsza ryzyko techniczne i wpływ zarządzania zmianami organizacji.

W przypadku każdej iteracji zespół rozwiązań w chmurze będzie lepszy do migracji obciążeń. Następujące kroki spowodują rozpoczęcie pracy zespołu technicznego na tej krzywej zapadalności:

1. Migruj swoje **pierwsze obciążenia** w czystej IaaS podejście przy użyciu narzędzi opisanych w [przewodniku migracji platformy Azure](../migrate/azure-migration-guide/index.md).
2. Rozwiń opcje narzędzi, aby użyć **migracji i modernizacji** przy użyciu [scenariuszy migracji](../migrate/azure-best-practices/contoso-migration-overview.md).
3. Opracowuj **strategię techniczną** , korzystając z szerszych metod opisanych w [temacie najlepsze rozwiązania dotyczące migracji](../migrate/azure-best-practices/index.md).
4. Zwiększ spójność, niezawodność i wydajność dzięki efektywnemu podejściu **fabryki migracji** , jak opisano w [ulepszeniach procesu migracji](../migrate/migration-considerations/index.md).

**Dostarczane**

Ciągłe ulepszanie zdolności zespołu adopcji do migracji obciążeń.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-9-hand-off-production-workloads-to-cloud-governance"></a>Krok 9. przekazywanie obciążeń produkcyjnych do ładu w chmurze

Zarządzanie to kluczowy czynnik do długoterminowego sukcesu dowolnego wysiłku związanego z migracją. Ważna jest szybkość migracji i wpływu na działalność biznesową. Jednak szybkość bez nadzoru może być niebezpieczna. Organizacja będzie musiała podejmować decyzje dotyczące ładu, które są zgodne ze wzorcami wdrażania, oraz potrzebami dotyczącymi zarządzania i zgodności.

- [Podejście do ładu](../govern/index.md): Ta metodologia przedstawia proces planowania zasad i procesów firmowych. Następnie kompilując dyscypliny wymagane do dostarczenia na zarządzanie w ramach działań w chmurze dla przedsiębiorstw.
- [Początkowa ładu](../govern/guides/complex/prescriptive-guidance.md): zrozumienie dyscypliny linii bazowej, dyscypliny linii bazowej zabezpieczeń i przyspieszenia wdrożenia, które są wymagane do utworzenia specjalisty dla ładu, który ma stanowić podstawę dla całego wdrożenia.

**Dostarczane**

- Wdróż początkową podstawę ładu.
- Ukończ test porównawczy, aby zaplanować przyszłe ulepszenia.
- Ryzyka dotyczące osi czasu:-ulepszanie zasad i implementacji ładu może dodać 1-4 tygodni na dyscyplinę.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-10-hand-off-production-workloads-to-cloud-operations"></a>Krok 10. przekazywanie obciążeń produkcyjnych do operacji w chmurze

Zarządzanie operacjami jest kolejną wymaganiem do osiągnięcia sukcesu migracji. Migrowanie pojedynczych obciążeń do chmury bez znajomości trwających operacji korporacyjnych jest ryzykowną decyzją. Równolegle z migracją należy zacząć planowanie operacji na dłuższy okres.

- [Plan bazowy zarządzania](../manage/index.md)
- [Zdefiniowanie zobowiązań biznesowych](../manage/considerations/business-alignment.md)
- [Rozwinięcie planu bazowego zarządzania](../manage/best-practices.md)
- [Uzyskaj specyficzne dla operacji zaawansowanych](../manage/design-principles.md)

**Dostarczane**

- Wdróż linię bazową zarządzania.
- Ukończ skoroszyt zarządzania operacjami.
- Zidentyfikuj wszystkie obciążenia wymagające oceny przeglądu architektury platformy Azure.
- Ryzyka dla osi czasu:
  - Przejrzyj skoroszyt: jedna godzina dla właściciela aplikacji.
  - Ukończ ocenę przeglądu architektury platformy Azure: godzinę dla aplikacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Kroki opisane w tym przewodniku mogą pomóc zespołom przyspieszyć swoje wysiłki w zakresie zarządzania zmianami i wyrównania uczestnika projektu. Wykonanie tych kroków może spowolnić proces, ale te kroki spowodują usunięcie wspólnych blokad i przyspieszenie realizacji wartości biznesowej.

## <a name="next-steps"></a>Następne kroki

Platforma wdrażania w chmurze to rozwiązanie cyklu życia. Może to pomóc w rozpoczęciu podróży migracji, ale może też pomóc w zawieszeniu dojrzałości zespołów, które obsługują wysiłki związane z migracją. Poniższe zespoły mogą użyć tych następnych kroków, aby kontynuować okres zapadalności swoich wysiłków. Te procesy równoległe nie są liniowe i nie powinny być wyświetlane jako Zablokowani. Zamiast tego każda z nich jest strumieniem wartości równoległych, aby pomóc w pożądanym ogólnym gotowości chmury firmy.

| Zespół  | Następna iteracja |
|---|---|
| &nbsp;Zespół ds. wdrażania chmury &nbsp; | [Ulepszenia procesów](../migrate/migration-considerations/index.md) zapewniają wgląd w przejście do fabryki migracji z wydajnymi możliwościami migracji. |
| &nbsp;Zespół strategii &nbsp; chmury | [Metodologia strategii](../strategy/index.md) i [metodologia planu](../plan/index.md) to iteracyjne procesy, które rozwijają się z planem wdrożenia. Wróć do tych stron przeglądu i Kontynuuj, aby kontynuować iteracje strategii biznesowej i technicznej. |
| &nbsp;Zespół platformy w chmurze &nbsp; | Przejdź ponownie do [przygotowanej metodologii](../ready/index.md) , aby kontynuować korzystanie z ogólnej platformy w chmurze, która obsługuje migrację lub inne wysiłki. |
| Zespół nadzorujący chmury &nbsp; &nbsp; | Użyj [metody rządzącej](../govern/index.md) , aby kontynuować ulepszanie procesów ładu, zasad i dyscyplin. |
| &nbsp;Zespół ds. operacji w chmurze &nbsp; | Kompiluj [metody zarządzania](../manage/index.md) , aby zapewnić bardziej zaawansowane operacje na platformie Azure. |

Jeśli Twój Scenariusz migracji jest nietypowy, możesz uzyskać spersonalizowaną ocenę gotowości do migracji w organizacji za pomocą [oceny strategicznej migracji i narzędzia gotowości](https://docs.microsoft.com/assessments/?id=strategic-migration-assessment). W oparciu o odpowiedzi podane podczas przeprowadzania oceny można pomóc w ustaleniu wskazówek, które najlepiej odpowiadają bieżącym potrzebom.
