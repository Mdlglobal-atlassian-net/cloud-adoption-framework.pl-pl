---
title: Strategia utrzymania ładu lub zgodności
description: Strategia utrzymania ładu lub zgodności
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 17952dc4c3ff28f2fcfe1a378a9efb969d65925b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803130"
---
# <a name="governance-or-compliance-strategy"></a>Strategia utrzymania ładu lub zgodności

Jeśli w ramach nakładu pracy na migrację wymagany jest ład lub zgodność, konieczne jest rozszerzenie zakresu. Poniższe wskazówki pomogą rozszerzyć zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md), aby zastosować różne podejścia do realizacji wymagań dotyczących ładu lub zgodności.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Gdy wymagany jest ład lub zgodność, największe znaczenie mają działania dotyczące wymagań wstępnych. Podczas oceny, migracji i optymalizacji mogą być wymagane dodatkowe korekty.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Konfiguracja podstawowego środowiska platformy Azure może zmienić się znacząco podczas integrowania wymagań dotyczących ładu lub zgodności. Aby zrozumieć, jak zmieniają się wymagania wstępne, ważne jest zrozumienie charakteru wymagań. Przed rozpoczęciem migracji wymagającej utrzymania ładu lub zachowania zgodności należy wybrać odpowiednie podejście i zaimplementować je w środowisku chmury. Poniżej przedstawiono kilka podejść wysokiego poziomu, które są często spotykane podczas migracji:

**Wspólne podejście ładu:** W przypadku większości organizacji [model ładu platformy wdrażania w chmurze](../../govern/guides/index.md) jest wystarczającym podejściem, które składa się z minimalnej, opłacalnej implementacji produktu (MVP), a następnie dokierowanych iteracji w zakresie zarządzania w celu poprawienia materialnych zagrożeń zidentyfikowanych w planie przyjęcia. Takie podejście zapewnia minimalny zestaw narzędzi niezbędnych do ustanowienia spójnego ładu, co pozwala zespołowi zaznajomić się z narzędziami. Następnie zespół rozszerza te narzędzia, aby rozwiązywać typowe problemy dotyczące ładu.

**Plany zgodności ISO 27001:** W przypadku klientów, którzy są zobowiązani do przestrzegania standardów zgodności ISO, [przykłady planów usług udostępnionych iso 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared/index) mogą działać jako bardziej wydajny MVP, aby generować bardziej zaawansowane ograniczenia ładu w procesie iteracyjnym. [Przykład App Service Environment/SQL Database ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) rozszerza strategię, aby mapować sterowanie i wdrażać typową architekturę w środowisku aplikacji. W miarę wydawania dodatkowych strategii zgodności będą one przywoływane również tutaj.

**Wirtualne centrum danych:** Może być wymagany bardziej niezawodny punkt wyjścia ładu. W takich przypadkach należy wziąć pod uwagę [Wirtualne centrum danych Azure (VDC)](../../reference/vdc.md). To podejście zazwyczaj jest zalecane podczas wysiłku wdrażania w skali przedsiębiorstwa, a szczególnie w przypadku nakładów pracy, które przekraczają 10 000 zasobów. Jest to de facto wybór dla złożonych scenariuszy nadzoru, gdy konieczne jest spełnienie dowolnej z następujących kwestii: rozbudowane wymagania dotyczące zgodności z innymi firmami, głęboka znajomość danej dziedziny lub zgodność z dojrzałymi zasadami nadzoru IT i wymaganiami dotyczącymi zgodności.

### <a name="partnership-option-to-complete-prerequisites"></a>Opcja partnerstwa w celu spełnienia wymagań wstępnych

**Usługi firmy Microsoft:** Usługi firmy Microsoft udostępniają oferty rozwiązań, które można dostosować do modelu ładu platformy wdrażania w chmurze, planów zgodności lub opcji wirtualnego centrum danych w celu zapewnienia najbardziej odpowiedniego modelu zarządzania lub zgodności. Oferta rozwiązania [Secure Cloud Insights (SCI)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) pozwala określić oparty na danych obraz wdrożenia klienckiego na platformie Azure i sprawdzić dojrzałość implementacji Azure klienta podczas identyfikowania optymalizacji istniejących architektur wdrażania, usuwania zagrożeń związanych z ładem, zabezpieczeniami i dostępnością. Szczegółowe informacje o kliencie pozwolą przeprowadzić następujące podejścia:

- **Cloud Foundation:** Ustanów podstawowe projekty, wzorce i zarządzanie architekturą platformy Azure, korzystając z oferty [hybrydowej rozwiązania Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) . Zamapuj wymagania klienta do najbardziej odpowiedniej architektury referencyjnej. Zaimplementuj produkt o minimalnej koniecznej funkcjonalności, składający się z usług udostępnionych i obciążeń IaaS.
- **Modernizacja chmury:** Oferta rozwiązania do [modernizacji w chmurze](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) służy jako kompleksowe podejście do przenoszenia aplikacji, danych i infrastruktury do chmury gotowej do użycia w przedsiębiorstwie, a także do optymalizowania i modernizacji po wdrożeniu w chmurze.
- Wprowadzanie **innowacji w chmurze:** Zaangażuj klienta dzięki innowacyjnemu i unikatowemu podejściu rozwiązania [Cloud Center doskonałości (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) , które kompiluje nowoczesne organizacje IT, aby zapewnić elastyczność na dużą skalę z DevOps, zachowując kontrolę. Implementacja podejścia Agile pozwala przechwycić wymagania biznesowe, ponownie użyć pakietów wdrożeniowych, które są dostosowane do zasad zabezpieczeń, zgodności i zarządzania usługami, i utrzymać platformę Azure dostosowaną do procedur operacyjnych.

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

W trakcie oceny wymagane są dodatkowe decyzje, które należy dostosować do wymaganego podejścia do ładu. Zespół ds. ładu chmury powinien udostępnić wszystkim członkom zespołu wdrożeniowego ds. chmury wszelkie oświadczenia dotyczące zasad, wskazówki dotyczące architektury i wymagania dotyczące ładu/zgodności przed oceną obciążenia.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

Wymagania dotyczące oceny ładu i zgodności są zbyt specyficzne dla klienta, aby można było podać ogólne wskazówki dotyczące faktycznych czynności podejmowanych podczas oceny. Jednak proces powinien obejmować zadania i alokacje czasu dla "dostosowanie do wymagań dotyczących zgodności/zarządzania". Aby uzyskać dodatkowe informacje na temat tych wymagań, zobacz następujące linki:

Aby lepiej zrozumieć ład, zapoznaj się z [omówieniem pięciu dyscyplin ładu chmury](../../govern/governance-disciplines.md). Ta część przewodnika Cloud Adoption Framework zawiera również szablony służące do dokumentowania zasad, wskazówek i wymagań dotyczących każdej z pięciu dyscyplin:

- [Zarządzanie kosztami](../../govern/cost-management/template.md)
- [Punkt odniesienia zabezpieczeń](../../govern/security-baseline/template.md)
- [Spójność zasobów].. /.. /govern/resource-consistency/template.md)
- [Linia bazowa tożsamości].. /.. /govern/identity-baseline/template.md)
- [Przyspieszanie wdrażania](../../govern/deployment-acceleration/template.md)

Aby uzyskać wskazówki dotyczące opracowywania wytycznych dotyczących ładu opartych na modelu ładu Cloud Adoption Framework, zobacz artykuł [Implementing a cloud governance strategy](../../govern/corporate-policy.md) (Implementacja strategii ładu chmury).

## <a name="optimize-and-promote-process-changes"></a>Optymalizacja i podwyższenie poziomu zmian procesu

W trakcie procesów optymalizacji i podwyższania zespół nadzoru chmury shluld czas inwestycji na testowanie i weryfikację zgodności z przepisami dotyczącymi nadzoru i przestrzegania standardów. Ponadto ten krok to dobry moment, aby wprowadzić procesy do zespołu ds. ładu chmury w celu zadbanie o szablony, które mogą zapewnić dodatkowe [przyspieszenie wdrażania](../../govern/deployment-acceleration/index.md) przyszłych projektów.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Sugerowana akcja w trakcie procesu optymalizacji i podwyższania poziomu

W trakcie tego procesu plan projektu powinien obejmować alokacje czasu dla zespołu nadzoru w chmurze w celu przeprowadzania przeglądu zgodności dla każdego obciążenia planowanego do promocji w środowisku produkcyjnym.

## <a name="next-steps"></a>Następne kroki

Jako ostatni element [listy rozwijanej rozszerzony zakres](./index.md), Wróć do listy kontrolnej i ponownie Oceń wszelkie dodatkowe wymagania dotyczące zakresu dla wysiłku migracji.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
