---
title: Przewodniki dotyczące ładu w chmurze
description: Zapoznaj się z przewodnikami dotyczącymi ładu w chmurze, które ilustrują najlepsze rozwiązania w zakresie podejścia przyrostowego do każdego scenariusza ładu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 69c46eb18c3181ed1f4301847786ebb538ee46fe
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83754862"
---
# <a name="cloud-governance-guides"></a>Przewodniki dotyczące ładu w chmurze

Praktyczne przewodniki dotyczące zapewniania ładu w tej sekcji przedstawiają przyrostowe podejście modelu ładu z przewodnika Cloud Adoption Framework na podstawie wcześniej opisanej [metodologii Ład](../methodology.md). Możesz ustanowić zwinne podejście do ładu w chmurze, które będzie się rozwijać w celu zaspokajania potrzeb wynikających z dowolnego scenariusza ładu w chmurze.

## <a name="review-and-adopt-cloud-governance-best-practices"></a>Przejrzyj i wdróż najlepsze rozwiązania dotyczące nadzoru chmury

Aby rozpocząć podróż po wdrażaniu chmury, wybierz jeden z następujących przewodników dotyczących ładu. W każdym przewodniku przedstawiono zestaw najlepszych rozwiązań opartych na zestawie fikcyjnych środowisk użytkowników. Czytelnicy, dla których przyrostowe podejście modelu ładu z przewodnika Cloud Adoption Framework jest nowe, przed wdrożeniem zestawu najlepszych rozwiązań powinni przejrzeć poniższe wprowadzenie do ogólnej teorii ładu.

<!-- markdownlint-disable MD033 -->

- [Standardowy przewodnik dotyczący ładu](./standard/index.md): Przewodnik dla większości organizacji oparty na zalecanym modelu z dwoma subskrypcjami, przeznaczony dla wdrożeń w wielu regionach, które nie obejmują chmur publicznych i suwerennych/rządowych.

> [!div class="nextstepaction"]
> [Standardowy przewodnik dotyczący ładu](./standard/index.md)

- [Przewodnik dotyczący ładu dla przedsiębiorstw złożonych](./complex/index.md): Przewodnik dla przedsiębiorstw, które są zarządzane przez wiele niezależnych jednostek biznesowych IT lub obejmują chmurę publiczną i suwerenną/rządową.

> [!div class="nextstepaction"]
> [Przewodnik dotyczący ładu dla przedsiębiorstw złożonych](./complex/index.md)

<!-- markdownlint-enable MD033 -->

## <a name="an-incremental-approach-to-cloud-governance"></a>Przyrostowy model utrzymania ładu w chmurze

## <a name="choose-a-governance-guide"></a>Wybieranie przewodnika po utrzymywaniu ładu

W przewodnikach przedstawiono, w jaki sposób zaimplementować minimalną konieczną funkcjonalność ładu. Od tego miejsca w każdym przewodniku przedstawiane jest, w jaki sposób zespół ds. utrzymania ładu w chmurze może jako partner podejmować działania wyprzedzające zespoły wdrażania chmury w celu przyspieszania wysiłków związanych z wdrażaniem. Model ładu z przewodnika Cloud Adoption Framework umożliwia kierowanie stosowaniem ładu od jego utworzenia przez kolejne ulepszenia i ewolucje.

Aby rozpocząć podróż nadzoru, wybierz jedną z dwóch poniższych opcji. Opcje są oparte na zsyntetyzowanych doświadczeniach użytkowników. Tytuły są utworzone na podstawie skomplikowania organizacji w celu ułatwienia nawigacji. Twoja decyzja może być bardziej złożona. Poniższe tabele przedstawiają różnice między tymi dwiema opcjami.

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

> [!WARNING]
> Wymagany może być bardziej niezawodny punkt początkowy nadzoru. W takich przypadkach należy wziąć pod uwagę podejście [wirtualnego centrum danych Azure](#azure-virtual-datacenter), które zostało krótko opisane [poniżej](#azure-virtual-datacenter). To podejście zazwyczaj jest zalecane podczas wysiłku wdrażania w skali przedsiębiorstwa, a szczególnie w przypadku nakładów pracy, które przekraczają 10 000 zasobów. Jest to też domyślny wybór dla złożonych scenariuszy nadzoru, gdy konieczne jest spełnienie dowolnej z następujących kwestii: rozbudowane wymagania dotyczące zgodności z innymi firmami, głęboka znajomość danej dziedziny lub zgodność z dojrzałymi zasadami nadzoru IT i wymaganiami dotyczącymi zgodności.

<!-- markdownlint-disable MD028 -->

> [!NOTE]
> Jest mało prawdopodobne, że jeden z przewodników będzie całkowicie pasował do Twojej sytuacji. Wybierz przewodnik najbliższy Twoim potrzebom i użyj go jako punktu początkowego. W przewodniku udostępniane będą dodatkowe informacje w celu ułatwienia dostosowywania decyzji dotyczących spełniania określonych kryteriów.

### <a name="business-characteristics"></a>Charakterystyka firmy

| Charakterystyka | Organizacja standardowa | Przedsiębiorstwo złożone |
|---|---|---|
| Lokalizacja geograficzna (kraj lub region geopolityczny) | Klienci lub personel znajdują się głównie w jednej lokalizacji geograficznej | Klienci lub personel znajdują się w wielu lokalizacjach geograficznych lub wymagają suwerennych chmur. |
| Jednostki biznesowe, których to dotyczy | Jednostki biznesowe korzystające ze wspólnej infrastruktury IT | Wiele jednostek biznesowych nie korzystających ze wspólnej infrastruktury IT |
| Budżet działu IT | Pojedynczy budżet działu IT | Przydzielony budżet w różnych jednostkach biznesowych i walutach |
| Inwestycje związane z infrastrukturą IT | Inwestycje kapitałowe oparte na wydatkach są planowane co rok i zwykle obejmują tylko podstawowe czynności konserwacyjne. | Inwestycje kapitałowe oparte na wydatkach są planowane co rok i często obejmują czynności konserwacyjne oraz cykl odświeżania od trzech do pięciu lat. |

### <a name="current-state-before-adopting-cloud-governance"></a>Bieżący stan przed wdrożeniem nadzoru chmury

| Stan | Przedsiębiorstwo standardowe | Przedsiębiorstwo złożone |
|---|---|---|
| Centrum danych lub inni dostawcy hostingu | Mniej niż pięć centrów danych | Więcej niż pięć centrów danych |
| Networking | Brak sieci WAN lub jeden bądź dwóch dostawców sieci WAN | Złożona sieć lub globalna sieć WAN |
| Tożsamość | Pojedynczy las, pojedyncza domena. | Złożone, wiele lasów, wiele domen. |

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>Żądany przyszły stan po przyrostowym ulepszaniu ładu chmury

| Stan | Organizacja standardowa | Przedsiębiorstwo złożone |
|---|---|---|
| Zarządzanie kosztami &mdash; księgowość w chmurze | Model przewidywania kosztów. Rozliczenia są scentralizowana za pośrednictwem działu IT. | Model obciążeń zwrotnych. Rozliczenia mogą być dystrybuowane za pośrednictwem zaopatrzenia działu IT. |
| Punkt odniesienia zabezpieczeń &mdash; chronione dane | Dane finansowe i własność intelektualna firmy. Ograniczone dane klienta. Brak wymagań dotyczących zgodności z innymi firmami. | Wiele kolekcji danych finansowych i osobowych klientów. Konieczne może być wzięcie pod uwagę zgodności z innymi firmami. |

## <a name="azure-virtual-datacenter"></a>Wirtualne centrum danych Azure

Wirtualne centrum danych Azure to podejście oparte na maksymalnym wykorzystaniu możliwości platformy Azure w chmurze przy jednoczesnym respektowaniu zasad dotyczących zabezpieczeń i nadzoru w przedsiębiorstwie.

W porównaniu do tradycyjnych środowisk lokalnych platforma Azure umożliwia zespołom opracowującym obciążenia i ich sponsorom biznesowym wykorzystywanie zwiększonej elastyczności wdrażania oferowanej na platformach w chmurze. Wraz ze zwiększeniem wysiłków związanych z wdrażaniem chmury związanych z koniecznością uwzględnienia danych i obciążeń o kluczowym znaczeniu ta elastyczność może spowodować konflikt z firmowymi wymaganiami dotyczącymi zabezpieczeń i zgodności z zasadami ustanowionymi przez Twoje zespoły IT. Dzieje się tak szczególnie w przypadku dużych przedsiębiorstw, w których istnieją zaawansowane wymagania dotyczące nadzoru i zgodności z przepisami.

Podejście usługi Azure Virtual Datacenter ma na celu rozwiązanie tych problemów wcześniej podczas cyklu życia wdrażania, zapewniając modele, architektury referencyjne, przykładowe artefakty automatyzacji i wskazówki ułatwiające osiągnięcie równowagi między wymaganiami dewelopera i nadzoru IT podczas działań związanych z wdrażaniem chmury przedsiębiorstwa. Podstawą tego podejścia jest sama koncepcja wirtualnego centrum danych: implementacja granic izolacji wokół infrastruktury w chmurze poprzez zastosowanie kontroli dostępu i zabezpieczeń, zasad sieciowych i monitorowania zgodności.

Wirtualne centrum danych może być uważane za Twoją własną izolowaną chmurę na platformie Azure, które integruje procesy zarządzania, wymagania prawne i procesy zabezpieczeń wymagane przez zasady dotyczące nadzoru. W ramach tych wirtualnych granic wirtualne centrum danych Azure oferuje przykładowe modele wdrażania obciążeń przy jednoczesnym zapewnieniu spójnych zasad zgodności oraz udostępnia podstawowe wskazówki dotyczące implementowania separacji ról i obowiązków w chmurze dla organizacji.

### <a name="azure-virtual-datacenter-assumptions"></a>Założenia dotyczące wirtualnego centrum danych Azure

Mimo że mniejsze zespoły mogą korzystać z modeli i zaleceń udostępnianych przez wirtualne centrum danych Azure, to podejście zostało zaprojektowane jako przewodnik dla grup IT przedsiębiorstwa zarządzających dużymi środowiskami w chmurze. W przypadku organizacji spełniających następujące kryteria zalecane jest postępowanie zgodnie ze wskazówkami dotyczącymi wirtualnego centrum danych Azure podczas projektowania infrastruktury chmury opartej na platformie Azure:

- Twoje przedsiębiorstwo podlega wymaganiom dotyczącym zgodności z przepisami, zgodnie z którymi konieczne jest używanie scentralizowanych funkcji monitorowania i inspekcji.
- Musisz zachować zgodność z typowymi zasadami i nadzorem oraz centralną kontrolę IT nad usługami podstawowymi.
- Twoja branża zależy od złożonej platformy, która wymaga złożonej kontroli oraz głębokiej znajomości danej dziedziny na potrzeby zarządzania nią. Najczęściej dotyczy to dużych przedsiębiorstw z branży finansów, przemysłu naftowego lub produkcji.
- Twoje istniejące zasady nadzoru IT wymagają większej zgodności z istniejącymi funkcjami nawet w trakcie wczesnego etapu wdrażania.

Aby uzyskać więcej informacji, odwiedź sekcję [wirtualnego centrum danych Azure](../../reference/vdc.md) w witrynie Cloud Adoption Framework.

## <a name="next-steps"></a>Następne kroki

Wybierz jeden z tych przewodników:

> [!div class="nextstepaction"]
> [Przewodnik dotyczący ładu dla przedsiębiorstw standardowych](./standard/index.md)
>
> [Przewodnik dotyczący ładu dla przedsiębiorstw złożonych](./complex/index.md)
