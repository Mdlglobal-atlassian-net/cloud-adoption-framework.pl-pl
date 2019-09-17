---
title: Strategia utrzymania ładu lub zgodności
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Strategia utrzymania ładu lub zgodności
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 6c1ac4000f5b79d6b177e8703f5e58b6dd9c9e56
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022731"
---
# <a name="governance-or-compliance-strategy"></a>Strategia utrzymania ładu lub zgodności

Jeśli w ramach nakładu pracy na migrację wymagany jest ład lub zgodność, konieczne jest rozszerzenie zakresu. Poniższe wskazówki pomogą rozszerzyć zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md), aby zastosować różne podejścia do realizacji wymagań dotyczących ładu lub zgodności.

## <a name="general-scope-expansion"></a>Rozszerzenie zakresu ogólnego

Gdy wymagany jest ład lub zgodność, największe znaczenie mają działania dotyczące wymagań wstępnych. Podczas oceny, migracji i optymalizacji mogą być wymagane dodatkowe korekty.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Konfiguracja podstawowego środowiska platformy Azure może zmienić się znacząco podczas integrowania wymagań dotyczących ładu lub zgodności. Aby zrozumieć, jak zmieniają się wymagania wstępne, ważne jest zrozumienie charakteru wymagań. Przed rozpoczęciem migracji wymagającej utrzymania ładu lub zachowania zgodności należy wybrać odpowiednie podejście i zaimplementować je w środowisku chmury. Poniżej przedstawiono kilka podejść wysokiego poziomu, które są często spotykane podczas migracji:

**Typowe podejście do ładu:** W przypadku większości organizacji [model ładu Cloud Adoption Framework](../../govern/guides/index.md) jest wystarczającym podejściem, które składa się z implementacji produktu o minimalnej koniecznej funkcjonalności (MVP), po której następują iteracje dojrzałości ładu nakierowane na wymierne ryzyka określone w planie wdrożenia. Takie podejście zapewnia minimalny zestaw narzędzi niezbędnych do ustanowienia spójnego ładu, co pozwala zespołowi zaznajomić się z narzędziami. Następnie zespół rozszerza te narzędzia, aby rozwiązywać typowe problemy dotyczące ładu.

**Strategie zgodności ISO 27001:** W przypadku klientów, którzy są zobowiązani do przestrzegania standardów zgodności ISO, [przykłady strategii usług udostępnionych ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared/index) mogą posłużyć jako bardziej wydajny produkt MVP, aby generować bardziej zaawansowane ograniczenia ładu na wcześniejszym etapie procesu iteracyjnego. [Przykład App Service Environment/SQL Database ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload) rozszerza strategię, aby mapować sterowanie i wdrażać typową architekturę w środowisku aplikacji. W miarę wydawania dodatkowych strategii zgodności będą one przywoływane również tutaj.

**Wirtualne centrum danych:** Wymagany może być bardziej niezawodny punkt początkowy nadzoru. W takich przypadkach należy wziąć pod uwagę [Wirtualne centrum danych Azure (VDC)](../../reference/vdc.md). To podejście zazwyczaj jest zalecane podczas wysiłku wdrażania w skali przedsiębiorstwa, a szczególnie w przypadku nakładów pracy, które przekraczają 10 000 zasobów. Jest to de facto wybór dla złożonych scenariuszy nadzoru, gdy konieczne jest spełnienie dowolnej z następujących kwestii: rozbudowane wymagania dotyczące zgodności z innymi firmami, głęboka znajomość danej dziedziny lub zgodność z dojrzałymi zasadami nadzoru IT i wymaganiami dotyczącymi zgodności.

### <a name="partnership-option-to-complete-prerequisites"></a>Opcja partnerstwa w celu spełnienia wymagań wstępnych

**Microsoft Services:** Dział Microsoft Services oferuje rozwiązania, które można dostosować do modelu ładu Cloud Adoption Framework, strategii zgodności lub opcji wirtualnego centrum danych w celu zapewnienia najbardziej odpowiedniego modelu ładu lub zgodności. Oferta rozwiązania [Secure Cloud Insights (SCI)](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) pozwala określić oparty na danych obraz wdrożenia klienckiego na platformie Azure i sprawdzić dojrzałość implementacji Azure klienta podczas identyfikowania optymalizacji istniejących architektur wdrażania, usuwania zagrożeń związanych z ładem, zabezpieczeniami i dostępnością. Szczegółowe informacje o kliencie pozwolą przeprowadzić następujące podejścia:

- **Cloud Foundation:** Ustanów podstawowe projekty, wzorce oraz architekturę ładu klienta platformy Azure, korzystając z oferowanego rozwiązania [Hybrid Cloud Foundation (HCF)](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf). Zamapuj wymagania klienta do najbardziej odpowiedniej architektury referencyjnej. Zaimplementuj produkt o minimalnej koniecznej funkcjonalności, składający się z usług udostępnionych i obciążeń IaaS.
- **Cloud Modernization:** Skorzystaj z oferty rozwiązania [Cloud Modernization](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) jako kompleksowego podejścia do przenoszenia aplikacji, danych i infrastruktury do chmury gotowej do użycia w przedsiębiorstwie, a także do optymalizowania i modernizacji w chmurze.
- **Wprowadzanie innowacji w chmurze:** Zaangażuj klienta dzięki innowacyjnemu i unikatowemu podejściu rozwiązania [Cloud Center doskonałości (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) , które kompiluje nowoczesne organizacje IT, aby zapewnić elastyczność na dużą skalę z DevOps, zachowując kontrolę. Implementacja podejścia Agile pozwala przechwycić wymagania biznesowe, ponownie użyć pakietów wdrożeniowych, które są dostosowane do zasad zabezpieczeń, zgodności i zarządzania usługami, i utrzymać platformę Azure dostosowaną do procedur operacyjnych.

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

W trakcie oceny wymagane są dodatkowe decyzje, które należy dostosować do wymaganego podejścia do ładu. Zespół ds. ładu chmury powinien udostępnić wszystkim członkom zespołu wdrożeniowego ds. chmury wszelkie oświadczenia dotyczące zasad, wskazówki dotyczące architektury i wymagania dotyczące ładu/zgodności przed oceną obciążenia.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

Wymagania dotyczące oceny ładu i zgodności są zbyt specyficzne dla klienta, aby można było podać ogólne wskazówki dotyczące faktycznych czynności podejmowanych podczas oceny. Zaleca się jednak, aby proces obejmował zadania i przydziały czasu dotyczące „dostosowania do wymagań zgodności/ładu”. Aby uzyskać dodatkowe informacje na temat tych wymagań, zobacz następujące linki:

Aby lepiej zrozumieć ład, zapoznaj się z [omówieniem pięciu dyscyplin ładu chmury](../../govern/governance-disciplines.md). Ta część przewodnika Cloud Adoption Framework zawiera również szablony służące do dokumentowania zasad, wskazówek i wymagań dotyczących każdej z pięciu dyscyplin:

- [Zarządzanie kosztami](../../govern/cost-management/template.md)
- [Punkt odniesienia zabezpieczeń](../../govern/security-baseline/template.md)
- [Spójność zasobów].. /.. /govern/resource-consistency/template.md)
- [Linia bazowa tożsamości].. /.. /govern/identity-baseline/template.md)
- [Przyspieszanie wdrażania](../../govern/deployment-acceleration/template.md)

Aby uzyskać wskazówki dotyczące opracowywania wytycznych dotyczących ładu opartych na modelu ładu Cloud Adoption Framework, zobacz artykuł [Implementing a cloud governance strategy](../../govern/corporate-policy.md) (Implementacja strategii ładu chmury).

## <a name="optimize-and-promote-process-changes"></a>Zmiany procesu optymalizacji i podwyższania poziomu

W trakcie procesów optymalizacji i podwyższania poziomu zaleca się, aby zespół ds. ładu chmury zainwestował czas na przetestowanie i zweryfikowanie zgodności ze standardami ładu i zgodności. Ponadto ten krok to dobry moment, aby wprowadzić procesy do zespołu ds. ładu chmury w celu zadbanie o szablony, które mogą zapewnić dodatkowe [przyspieszenie wdrażania](../../govern/deployment-acceleration/index.md) przyszłych projektów.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Sugerowana akcja w trakcie procesu optymalizacji i podwyższania poziomu

W trakcie tego procesu zaleca się, aby plan projektu obejmował przydziały czasu do zespołu ds. ładu chmury w celu przeprowadzania przeglądu zgodności każdego obciążenia, dla którego jest planowane podwyższenie poziomu w środowisku produkcyjnym.

## <a name="next-steps"></a>Następne kroki

Na końcu [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md) Czytelnik jest zachęcany do powrotu do listy kontrolnej i ponownej oceny wszelkich dodatkowych wymagań dotyczących zakresu nakładu pracy migracji.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
