---
title: 'Wprowadzenie: tworzenie nowych produktów i usług w chmurze'
description: Dowiedz się więcej na temat metodologii innowacji jako podejścia do programowania nowych produktów i usług w chmurze.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 97da5f902fb195a4390b33ef5b8eed2f12ac4a94
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621193"
---
# <a name="get-started-accelerate-new-product-and-service-innovation-in-the-cloud"></a>Wprowadzenie: przyspiesz innowacje nowych produktów i usług w chmurze

Tworzenie nowych produktów i usług w chmurze wymaga innego podejścia niż migracja. Metodologia wdrażania w chmurze stanowi podejście, które prowadzi do rozwoju nowych produktów i usług.

Ten przewodnik wykorzystuje sekcje struktury wdrażania chmury, które zostały wyróżnione na poniższej ilustracji. Chociaż innowacje są mniej przewidywalne niż standardowa migracja, nadal mieszczą się w kontekście szerszego planu wdrażania w chmurze. Ten przewodnik może pomóc przedsiębiorstwu zapewnić pomoc techniczną potrzebną do innowacji i zapewnić strukturę potrzebną do tworzenia zrównoważonego portfolio w ramach wdrożenia chmury.

![Wprowadzenie do przyspieszenia innowacji w chmurze](../_images/get-started/innovation-map.png)

## <a name="step-1-document-the-business-strategy"></a>Krok 1. udokumentowanie strategii biznesowej

Aby uniknąć powszechnych bloków, należy utworzyć jasno i zwięzłą strategię biznesową dla innowacji. Wyrównania uczestnika projektu dotyczącego motywacji i oczekiwanych wyników działalności biznesowej będą kształtować decyzje podejmowane przez zespół rozwiązań w chmurze.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować motywacje i żądane wyniki biznesowe.

<!-- docsTest:ignore "Get started: Accelerate migration" -->

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Motywacje](../strategy/motivations.md): pierwszy krok do strategicznego dostosowywania ma na celu uzyskanie konsensusu na potrzeby motywacji prowadzących do wysiłku innowacji. Zacznij od ustalenia i kategoryzacji motywacji oraz wspólnych motywów z różnych uczestników firmy i.
- [Wyniki biznesowe](../strategy/business-outcomes/index.md): w przypadku wyrównania motywacji możliwe jest przechwycenie żądanych wyników firmy. Zapewnia to wyraźne metryki, za pomocą których można mierzyć ogólną transformację.
- [Balansowanie portfolio](../strategy/balance-the-portfolio.md): innowacje nie są właściwą ścieżką dla każdego obciążenia. Takie podejście do wdrożenia jest bardziej istotne w przypadku nowych niestandardowych aplikacji lub obciążeń, które **wymagają** ponownej architektury lub pełnego odbudowy. Gdy motywacje przeważnie preferują innowacje dla wszystkich obciążeń, ważne jest, aby oszacować portfolio w celu zapewnienia, że te inwestycje mogą generować pożądaną zwrot z inwestycji. Modernizacja określonych zasobów i niewielkiej skali, które mogą być innowacyjne, ale mogą być lepiej obsłużone przez następujące kroki [: przyspieszanie migracji](./migrate.md).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-2-evaluate-the-business-justification"></a>Krok 2. oszacowanie uzasadnienia biznesowego

W pierwszym miejscu podczas tworzenia przypadku biznesowego należy oszacować początkowy zwrot wysokiego poziomu z potencjalnego wysiłku związanego z wdrażaniem chmury. Celem tego kroku jest upewnienie się, że wszystkie zainteresowane strony będą wyrównane do jednego z prostych pytań: "w oparciu o dostępne dane, czy ogólnie przyjęto, że w chmurze podejmowana jest decyzja biznesowa?". Na tym pytaniu zespół może lepiej dostosować sposób, w jaki ten projekt innowacji pomaga sprostać potrzebom prognozowanym przez użytkowników końcowych w celu wdrożenia chmury.

**Dostarczane**

- Użyj [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) , aby zarejestrować uzasadnienie biznesowe.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Uzasadnienie biznesowe](../strategy/cloud-migration-business-case.md): przed przeprowadzeniem oceny każdej możliwości wprowadzania innowacji w chmurze, należy wykonać ogólne uzasadnienie biznesowe w celu ustalenia wyrównania uczestnika projektu dotyczącego ogólnego planu wdrażania.
- [Wartość biznesowa konsensusu](../innovate/business-value.md): określenie wartości innowacji może być trudne na początku procesu. Wykonanie w tym artykule może pomóc w ocenie wyrównania wartości biznesowej określonego wysiłku innowacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury | <li> Zespół ds. wdrażania chmury |

## <a name="step-3-gather-data-and-analyze-assets-and-workloads"></a>Krok 3. zbieranie danych i analizowanie zasobów i obciążeń

W większości przedsiębiorstw innowacje można przyspieszyć, korzystając z istniejących zasobów, takich jak aplikacje, maszyny wirtualne i dane. Planując innowacje, ważne jest, aby zrozumieć, jak i kiedy te zasoby zostaną zmigrowane do chmury.

**Dostarczane**

- Dane pierwotne w istniejącym spisie (aplikacje, maszyny wirtualne i dane)
- Jeśli proponowane innowacje mają zależności dotyczące istniejącego spisu, należy wykonać następujące elementy dostarczane:
  - Analiza ilościowa wszelkich magazynów pomocniczych wymaganych do obsługi planowanych innowacji.
  - Analiza jakościowa wszelkich obciążeń pomocniczych wymaganych do dostarczenia innowacji.
- Oblicz koszt nowego spisu wymaganego do wspierania nakładu innowacji.
- Aktualizacja uzasadnienia biznesowego w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) z użyciem rafinowanych obliczeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

Odnajdywanie i Ocena zapewniają lepszy poziom wyrównania technicznego w celu utworzenia planu umożliwiającego podjęcie odpowiednich działań w celu przeprowadzenia migracji wszelkich zależnych obciążeń wymaganych przez planowane innowacje. Jest to bardzo powszechne, gdy firmy mają istniejące źródła danych, scentralizowane aplikacje lub wymagane warstwy usług, które są potrzebne do dostarczania innowacji w kontekście pozostałej części przedsiębiorstwa. W przypadku systemów zależnych następujące artykuły mogą przeprowadzić proces odnajdywania i oceny.

- [Istniejące systemy spisu](../digital-estate/inventory.md): zrozumienie bieżącego stanu z programistycznego, opartego na danych podejścia to pierwszy krok. Odkryj i Zbierz dane, aby włączyć wszystkie działania oceny.
- [Racjonalizacja przyrostowa](../digital-estate/rationalize.md#incremental-rationalization): Usprawnij wysiłki oceniania, aby skupić się na analizie jakościowej wszystkich zasobów (prawdopodobnie nawet w przypadku obsługi przypadku biznesowego). Następnie Dodaj głęboką analizę jakościową dla pierwszych 10 obciążeń.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury |

## <a name="step-4-plan-for-migration-of-dependent-assets"></a>Krok 4. Planowanie migracji zasobów zależnych

Gdy nowe innowacje są zależne od istniejących obciążeń lub zasobów, szablon planu wdrażania w chmurze zapewnia przyspieszone podejście do tworzenia zaległości projektu. Zaległości można następnie zmodyfikować, aby odzwierciedlały wyniki odnajdywania, racjonalizację, umiejętność i swoją umowę.

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
- [Wyrównanie nakładu pracy](../plan/assets.md): Wyrównaj zasoby i obciążenia w zaległości, aby jasno zdefiniować nakład pracy dla obciążeń z priorytetyzacją.
- [Wyrównanie osób i czasu](../plan/iteration-paths.md): Ustanów iteracje, szybkość pracy i wydania dla obciążeń.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury |

## <a name="step-5-align-governance-requirements-to-your-adoption-plan"></a>Krok 5. dostosowanie wymagań ładu do planu wdrożenia

Omawianie planowanych innowacji z zespołem nadzoru pomaga uniknąć wielu zablokowanych, zanim wystąpią. Czasami nowatorskie nowe rozwiązania mogą wymagać praktyk, które nie są zalecane w praktyce dotyczącej ładu. Niektóre z tych wymaganych funkcji mogą być nawet blokowane przez zautomatyzowane narzędzia wymuszania ładu.

**Dostarczane**

- Tworzenie przejrzystości i zrozumienie między potrzebami innowacji i ograniczeniami ładu.
- W razie potrzeby zaktualizuj zasady i procesy w celu odzwierciedlenia wszelkich zmian lub wyjątków istniejących ograniczeń ładu.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

Poniższe linki ułatwią zespołowi wdrożenia zrozumienie podejścia podjętego przez zespół nadzorujący w chmurze.

- [Podejście do ładu](../govern/index.md): Ta metodologia przedstawia proces planowania zasad i procesów korporacyjnych, a następnie budowanie dyscyplin, które są wymagane do dostarczenia w ramach organizacji w chmurze.
- [Definiowanie zasad firmowych](../govern/corporate-policy.md): Identyfikowanie i łagodzenie ryzyka biznesowego.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-define-operational-needs-and-business-commitments"></a>Krok 6. Definiowanie potrzeb operacyjnych i zobowiązań firmy

Zdefiniuj plan długoterminowych obowiązków operacyjnych dotyczących planowanych innowacji. Czy ustanowiona linia bazowa zarządzania będzie wystarczająca do zaspokajania potrzeb operacyjnych? W przeciwnym razie Oceń opcje operacji finansowania, które są specyficzne dla technologii, która obsługuje te innowacje.

**Dostarczane**

- Ukończ [Przegląd architektury platformy Azure](https://docs.microsoft.com/assessments/?id=azure-architecture-review) , aby ocenić różne decyzje dotyczące architektury i operacji.
- Dostosuj [skoroszyt zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , aby odzwierciedlał wszystkie wymagane Operacje zaawansowane.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Rozwiń linię bazową zarządzania](../manage/best-practices.md): Ta sekcja struktury wdrażania w chmurze prowadzi użytkownika przez różne przejścia do zarządzania operacyjnego w chmurze.
- [Korzystaj z zaawansowanych operacji](../manage/design-principles.md): odkryj sposoby wykraczania poza linię bazową zarządzania.
- Jeśli wymagane są operacje zaawansowane do obsługi Twoich potrzeb związanych z operacjami, należy oszacować [zobowiązania biznesowe](../manage/considerations/business-alignment.md) , aby określić obowiązki operacyjne dla obu zespołów.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. operacji w chmurze <li> Zespół ds. wdrażania chmury | <li> Zespół strategii chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-7-deploy-an-aligned-landing-zone"></a>Krok 7. wdrażanie wyrównanej strefy docelowej

Wszystkie zasoby hostowane w chmurze w ramach strefy ładunkowej. Strefa docelowa może mieć jawne wymagania dotyczące ładu, bezpieczeństwa i działania. Może to być zupełnie nowa subskrypcja bez pomocy technicznej z innych zespołów. W każdym z tych scenariuszy ważne jest, aby zacząć od strefy docelowej, która jest wyrównana do wymagań dotyczących ładu i działania od początku. Począwszy od zatwierdzonej strefy wyładunkowej, zespół będzie mógł odkrycie naruszeń zasad przed rozpoczęciem opracowywania, a nie w momencie wydania rozwiązania do produkcji. To wczesne odnajdowanie pomaga w usunięciu blokowanych i udostępnia zespół ds. przyjęcia i zespół nadzoru z czasem wymaganym do wdrożenia zmiany.

**Dostarczane**

- Wdróż pierwszą strefę docelową dla początkowego i niskiego ryzyka podczas wczesnej innowacji.
- Opracowywanie planu do refaktoryzacji z CCoE lub centralnym celem zapewnienia ładu, bezpieczeństwa i wyrównania operacyjnego.
- Ryzyka dla osi czasu:
  - Wymagania dotyczące ładu, operacji i zabezpieczeń dla pierwszych 10 obciążeń mogą znacząco spowolnić ten proces. Rzeczywiste Refaktoryzacja pierwszej strefy docelowej i kolejnych stref wypełniania będzie trwać znacznie dłużej, ale powinny być wykonywane równolegle do wysiłków związanych z migracją.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Wybierz strefę wyładunkowej](../ready/landing-zone/first-landing-zone.md): Użyj tego artykułu, aby znaleźć odpowiednie podejście do wdrożenia strefy docelowej na podstawie wzorca wdrożenia. Następnie Wdróż tę standardową bazę kodu.
- [Rozszerzanie strefy docelowej](../ready/considerations/index.md): niezależnie od punktu początkowego Zidentyfikuj luki w wdrożonej strefie docelowej, aby dodać wymagane składniki organizacji, zabezpieczeń, nadzoru, zgodności, operacji i tak dalej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół platformy w chmurze <li> Zespół ds. wdrażania chmury | <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-8-innovate-in-the-cloud"></a>Krok 8. innowacje w chmurze

Metodologia innowacje zawiera wskazówki dotyczące narzędzi i metod zarządzania produktami najczęściej używanych do innowacji w chmurze. Poniższe kroki pomogą Ci rozpocząć pracę z tym podejściem.

**Dostarczane**

- Rozwiązania oparte na technologii, które wzbogacają klientów i mają wartość dla firmy.
- Procesy i narzędzia pozwalające na szybsze wykonywanie iteracji dla tych rozwiązań i Dodawanie większej wartości przy użyciu chmury:
  - Podejście iteracyjne projektowania.
  - Aplikacje utworzone przez użytkownika.
  - Środowiska oparte na technologii.
  - Integracja produktów i technologii fizycznych przy użyciu IoT.
  - Analiza otoczenia: integracja nieinwazyjnej technologii ze środowiskiem.
  - Cognitive Services: dane Big Data, AI, uczenie maszynowe i rozwiązania predykcyjne.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Wartość biznesowa konsensus](../innovate/business-value.md): Jeśli od czasu ostatniego konsensusu wartość biznesowa przekazano więcej niż trzy miesiące, lub jeśli jedna z nich nie została ukończona, Zacznij tutaj.
- [Przewodnik dotyczący innowacji platformy Azure](../innovate/innovation-guide/index.md): Skorzystaj z przewodnika innowacji platformy Azure, aby przyspieszyć wdrażanie innowacyjnych rozwiązań, opisując narzędzia i procesy, które mogą pomóc w tworzeniu minimalnego produktu, który jest w dobrej kondycji.
- [Najlepsze rozwiązania innowacyjne](../innovate/best-practices/index.md): Dowiedz się, jak połączyć usługi platformy Azure, aby utworzyć łańcucha narzędzi do rozdzielania cyfrowo.
- [Pętle opinii](../innovate/considerations/adoption.md): Opracuj ulepszone pętle opinii, aby szybko zapewnić klientom wpływ na innowacje.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Centrum doskonałości chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="value-statement"></a>Value — instrukcja

Kroki opisane w tym przewodniku mogą pomóc zespołowi w tworzeniu innowacyjnych rozwiązań w chmurze, które tworzą wartość biznesową, są odpowiednio regulowane i są dobrze zaprojektowane.

## <a name="next-steps"></a>Następne kroki

Platforma wdrażania w chmurze to rozwiązanie cyklu życia. Może to pomóc w rozpoczęciu podróży innowacji, ale może też pomóc w zawieszeniu dojrzałości zespołów, które obsługują wysiłki innowacyjne. Poniższe zespoły mogą użyć tych następnych kroków, aby kontynuować okres zapadalności swoich wysiłków. Te procesy równoległe nie są liniowe i nie powinny być wyświetlane jako Zablokowani. Zamiast tego każda z nich jest strumieniem wartości równoległych, aby pomóc w pożądanym ogólnym gotowości chmury firmy.

| Zespół | Następna iteracja |
|---|---|
| &nbsp;Zespół ds. wdrażania chmury &nbsp; | [Ulepszenia procesów](../innovate/considerations/index.md) zapewniają wgląd w informacje o podejściach do udostępniania rozwiązań w zakresie innowacji, które wpływają na klientów i wdrażanie cykliczne. |
| &nbsp;Zespół strategii &nbsp; chmury | [Metodologia strategii](../strategy/index.md) i [metodologia planu](../plan/index.md) to iteracyjne procesy, które rozwijają się z planem wdrożenia. Wróć do tych stron przeglądu i Kontynuuj, aby kontynuować iteracje strategii biznesowej i technicznej. |
| &nbsp;Zespół platformy w chmurze &nbsp; | Przejdź ponownie do [przygotowanej metodologii](../ready/index.md) , aby kontynuować korzystanie z ogólnej platformy w chmurze, która obsługuje migrację lub inne wysiłki. |
| Zespół nadzorujący chmury &nbsp; &nbsp; | Użyj [metody rządzącej](../govern/index.md) , aby kontynuować ulepszanie procesów ładu, zasad i dyscyplin. |
| &nbsp;Zespół ds. operacji w chmurze &nbsp; | Kompiluj [metody zarządzania](../manage/index.md) , aby zapewnić bardziej zaawansowane operacje na platformie Azure. |
