---
title: 'Zobowiązania biznesowe: zarządzanie i operacje w chmurze'
description: 'Zobowiązania biznesowe: zarządzanie i operacje w chmurze'
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4827ca2aac045b105beed9c15de366311092a7f2
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807856"
---
# <a name="business-commitment-in-cloud-management"></a>Zobowiązania biznesowe w zarządzaniu chmurą

Zdefiniowanie _zobowiązania biznesowego_ to ćwiczenie priorytetów. Celem jest dostosowanie odpowiedniego poziomu zarządzania operacyjnego przy akceptowalnym koszcie eksploatacyjnym. Znalezienie tego salda wymaga kilku punktów danych i obliczeń, które zostały opisane w tym artykule.

![Balans kosztów i odporności](../../_images/manage/business-commitment-scale.png)

Zobowiązania do stabilności biznesowej, za pomocą odporności technicznej lub innej umowy dotyczącej poziomu usług (SLA), są podejmowane decyzje biznesowe. W przypadku większości obciążeń w środowisku wystarcza poziom odniesienia zarządzania chmurą. W przypadku innych, wzrost kosztu od 2 do 4x jest łatwo uzasadniony ze względu na potencjalny wpływ wszelkich przerw w działaniu firmy.

Poprzednie artykuły w tej serii mogą pomóc w zrozumieniu klasyfikacji i wpływu zakłóceń na różne obciążenia. Ten artykuł ułatwia obliczenie zwracanych wartości. Jak pokazano na powyższym obrazie, każdy poziom zarządzania chmurą ma punkty przegięcia, w których koszt może wzrosnąć szybciej niż zwiększa odporność. Te punkty przegięcia będą monitował szczegółowe decyzje biznesowe i zobowiązania biznesowe.

## <a name="determine-a-proper-commitment-with-the-business"></a>Ustalenie właściwego zobowiązania z firmą

Dla każdego obciążenia w portfelu zespół operacyjny chmury i zespół strategii chmury powinien dostosować poziom zarządzania, który jest dostarczany bezpośrednio przez zespół operacyjny chmury.

Po ustanowieniu zobowiązania z firmą istnieje kilka kluczowych aspektów do dopasowania:

- Wymagania wstępne dotyczące operacji IT
- Odpowiedzialność za zarządzanie
- Dzierżawa w chmurze
- Nietrwałe czynniki kosztowe
- Zwrot z inwestycji
- Sprawdzanie poprawności poziomu zarządzania

Aby pomóc w podejmowaniu decyzji, w dalszej części tego artykułu opisano wszystkie te aspekty bardziej szczegółowo.

## <a name="it-operations-prerequisites"></a>Wymagania wstępne dotyczące operacji IT

[Przewodnik zarządzania Azure](../azure-management-guide/index.md) zawiera opis narzędzi do zarządzania, które są dostępne na platformie Azure. Przed osiągnięciem zobowiązania z firmą należy określić akceptowalną podstawową linię bazową zarządzania, która ma być stosowana do wszystkich zarządzanych obciążeń. Następnie obliczy standardowy koszt zarządzania dla każdego z zarządzanych obciążeń w portfolio IT, na podstawie liczby rdzeni procesora CPU, miejsca na dysku i innych zmiennych związanych z zasobami. Ponadto Szacowana zostanie złożona umowa SLA dla każdego obciążenia w oparciu o architekturę.

> [!TIP]
> Zespoły ds. operacji IT często używają domyślnego minimum 99,9 procent czasu dla początkowej złożonej umowy SLA. Mogą również zdecydować się na normalizację kosztów zarządzania na podstawie średniego obciążenia, szczególnie w przypadku rozwiązań o minimalnych wymaganiach dotyczących rejestrowania i magazynowania. Uśrednianie kosztów kilku obciążeń o krytycznym znaczeniu może zapewnić punkt początkowy dla początkowych konwersacji.

<!-- -->

> [!TIP]
> Jeśli planujesz zarządzanie chmurą za pomocą [skoroszytu usługi Ops](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , należy zaktualizować pola zarządzania Ops, aby odzwierciedlały te wymagania wstępne. Te pola obejmują _poziom zobowiązania_, umowę _SLA_i _koszt miesięczny_. Koszt miesięczny powinien przedstawiać miesięczne koszty dodatkowych narzędzi do zarządzania operacyjnego.

Linia bazowa zarządzania operacjami służy jako początkowy punkt początkowy do sprawdzenia poprawności w każdej z poniższych sekcji.

## <a name="management-responsibility"></a>Odpowiedzialność za zarządzanie

W tradycyjnych środowiskach lokalnych koszt zarządzania środowiskiem jest zwykle traktowany jako Sunk koszt, który jest własnością operacji IT. W chmurze zarządzanie jest decyzją nigdy wykonywane celowo z bezpośrednim wpływem na budżet. Koszty każdej funkcji zarządzania mogą być bardziej bezpośrednio przypisane do każdego obciążenia, które jest wdrażane w chmurze. Takie podejście pozwala na większą kontrolę, ale tworzy wymaganie zespołów operacyjnych w chmurze i zespołów strategii chmurowej, aby najpierw zatwierdzić umowę dotyczącą odpowiedzialności.

Organizacje mogą również zdecydować się na [przetworzyć niektóre z ich bieżących funkcji zarządzania dla dostawcy usług](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Dostawcy usług mogą korzystać z [usługi Azure Lighthouse](https://azure.com/lighthouse) , aby zapewnić organizacjom dokładniejszą kontrolę nad udzieleniem dostępu do zasobów, a także większy wgląd w działania wykonywane przez dostawców usług.

- **Delegowana odpowiedzialność:** Ze względu na to, że nie ma potrzeby scentralizowania i przyjmowania kosztów zarządzania operacyjnego, operacje działu IT w wielu organizacjach rozważają nowe podejścia. Jedną z typowych metod nazywa się _delegowanie odpowiedzialności_. W centrum usług w chmurze z modelem doskonałości operacje platformy i Automatyzacja platformy zapewniają samoobsługowe narzędzia do zarządzania, które mogą być używane przez zespoły operacyjne prowadzone przez firmę, niezależnie od centralnych zespołów operacyjnych IT. Takie podejście daje zainteresowanym podmiotom gospodarczym pełną kontrolę nad budżetami związanymi z zarządzaniem. Umożliwia także zespołowi usługi Cloud Center doskonałości (CCoE), aby upewnić się, że minimalny zestaw guardrails został poprawnie zaimplementowany. W tym modelu działa jako Broker i przewodnik ułatwiający podejmowanie decyzji w firmie. Operacje biznesowe nadzorują codzienne operacje zależnych obciążeń.

- **Centralna odpowiedzialność:** Wymagania dotyczące zgodności, złożoność techniczna i niektóre modele usług udostępnionych mogą wymagać _centralnego modelu IT_ . W tym modelu kontynuuje wykonywanie obowiązków związanych z zarządzaniem operacjami. Narzędzia projektowe, kontrolne zarządzania i zarządzanie środowiskami mogą być centralnie zarządzane i kontrolowane, co ogranicza rolę zainteresowanych uczestników firmy w celu podejmowania zobowiązań w zakresie zarządzania. Jednak widoczność kosztów i architektury podejścia do chmury znacznie ułatwia scentralizowanemu działowi IT przekazywanie kosztów i poziomu zarządzania dla każdego obciążenia.

- **Model mieszany:** Klasyfikacja jest najprawdopodobniej z _mieszanym modelem_ obowiązków związanych z zarządzaniem. Firmy, które znajdują się w pośrodku transformacji z lokalizacji lokalnej do chmury, mogą wymagać od siebie pierwszego modelu operacyjnego. Firmy mające ścisłe wymagania w zakresie zgodności lub które zależą od długoterminowych kontraktów z dostawcami z dostawcą usług IT, mogą wymagać scentralizowanego modelu operacyjnego.

  Niezależnie od ich ograniczeń, dzisiejsze firmy muszą wprowadzać innowacje. W przypadku szybkiej innowacji, w pośrodku modelu z centralnym i scentralizowanym zakresem odpowiedzialności, podejście mieszane może zapewnić równowagę. W tym podejściu centralnie udostępnia scentralizowany model operacyjny dla wszystkich obciążeń, które są krytyczne dla działalności firmy lub zawierają informacje poufne. W tym samym czasie wszystkie inne klasyfikacje obciążeń mogą zostać umieszczone w środowisku chmury, które jest przeznaczone do delegowanych obowiązków. Podejście do scentralizowanej odpowiedzialności służy jako ogólny model operacyjny. Dzięki tej firmie można elastycznie zastosować wyspecjalizowany model operacyjny na podstawie wymaganego poziomu pomocy technicznej i czułości.

Pierwszym krokiem jest zatwierdzenie do podejścia do odpowiedzialności, które następnie kształtuje następujące zobowiązania.

**Która organizacja będzie odpowiedzialna za codzienne zarządzanie operacjami dla tego obciążenia?**

## <a name="cloud-tenancy"></a>Dzierżawa w chmurze

W przypadku większości firm zarządzanie jest łatwiejsze, gdy wszystkie zasoby znajdują się w jednej dzierżawie. Niektóre organizacje mogą jednak wymagać obsługi wielu dzierżawców. Aby dowiedzieć się, dlaczego firma może wymagać wielodostępnego środowiska platformy Azure, zobacz [scentralizowanie operacji zarządzania przy użyciu usługi Azure Lighthouse](../centralize-operations.md).

**Czy to obciążenie będzie się znajdować w jednej dzierżawie platformy Azure wraz ze wszystkimi innymi obciążeniami?**

## <a name="soft-cost-factors"></a>Nietrwałe czynniki kosztowe

W następnej sekcji przedstawiono podejście do zwrotów porównawczych, które są skojarzone z poziomami procesów zarządzania i narzędziami. Na końcu tej sekcji każde analizowane obciążenie mierzy koszt zarządzania względem przewidywanego wpływu zakłóceń działania firmy. To podejście zapewnia stosunkowo łatwy sposób zrozumienia, czy inwestycja w bogatsze podejścia do zarządzania jest uzasadniona.

Zanim zaczniesz korzystać z liczb, ważne jest, aby przyjrzeć się niezmiennym kosztom. Nieprzerwane czynniki kosztowe generują zwrot, ale takie zwrócenie jest trudne do mierzenia dzięki bezpośredniemu oszczędności kosztów, które byłyby widoczne w zestawieniu zysków i strat. Nietrwałe czynniki kosztowe są ważne, ponieważ mogą wskazywać potrzebę zainwestowania na wyższy poziom zarządzania niż w rozsądny sposób.

Poniżej przedstawiono kilka przykładów nieprawidłowych czynników kosztów:

- Dzienne użycie obciążeń przez tablicę lub dyrektor naczelny.
- Użycie obciążenia przez pierwszych _x procent_ klientów, którzy powodują większy wpływ na dochody w innym miejscu.
- Wpływ na zadowolenie pracowników.

Następny punkt danych, który jest wymagany do wykonania zobowiązania, to lista nieelastycznych czynników kosztów. Te czynniki nie muszą być udokumentowane na tym etapie, ale zainteresowane strony biznesowe powinny mieć świadomość znaczenia tych czynników i ich wykluczenia z następujących obliczeń.

## <a name="calculate-loss-avoidance-roi"></a>Oblicz zwrot z inwestycji

Gdy obliczamy względne zwroty kosztów zarządzania operacjami, zespół IT odpowiedzialny za operacje w chmurze powinien spełnić wspomniane wyżej wymagania wstępne i założyć minimalny poziom zarządzania dla wszystkich obciążeń.

Następne zobowiązanie, które należy wykonać, jest akceptacją przez firmę kosztów związanych z ofertą zarządzaną przez linię bazową.

**Czy firma wyraża zgodę na inwestycję w linię bazową w celu spełnienia minimalnych standardów operacji w chmurze?**

Jeśli firma nie wyraża zgody na ten poziom zarządzania, należy opracować rozwiązanie, które umożliwi firmie dalsze działanie, bez istotnego wpływu na operacje w chmurze innych obciążeń.

Jeśli firma chce mieć więcej niż standardowy poziom zarządzania, pozostała część tej sekcji pomaga sprawdzić, czy inwestycje i skojarzone zwroty (w formie unikania utraty).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Zwiększone poziomy zarządzania: zasady projektowania i katalog usług

W przypadku rozwiązań zarządzanych można stosować kilka zasad projektowania i rozwiązań szablonów oprócz linii bazowej zarządzania. Każda z zasad projektowania pod kątem niezawodności i odporności dodaje koszt operacyjny do obciążenia. W odniesieniu do tych dodatkowych zobowiązań i działalności biznesowej ważne jest zapoznanie się z potencjalnymi stratami, które można uniknąć przez zwiększenie inwestycji.

Poniższe obliczenia przeprowadzą przez formuły, aby lepiej zrozumieć różnice między stratami i wzrostem inwestycji związanych z zarządzaniem. Aby uzyskać wskazówki dotyczące obliczania kosztów zwiększonego zarządzania, zobacz [Automatyzacja obciążeń](./workload.md) i [Automatyzacja platform](./platform.md).

> [!TIP]
> Jeśli planujesz zarządzanie chmurą za pomocą [skoroszytu usługi Ops](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) , zaktualizuj pola zarządzania Ops, aby odzwierciedlały odzwierciedlenie poszczególnych konwersacji. Te pola obejmują _poziom zobowiązania_, umowę _SLA_i _koszt miesięczny_. Koszt miesięczny powinien reprezentować miesięczny koszt dodanych narzędzi do zarządzania operacyjnego. Po ich zaktualizowaniu pola będą aktualizować formuły zwrotu z inwestycji i każde z poniższych pól.

### <a name="estimate-outage-hours-per-year"></a>Oszacowanie przestoju (godz. rocznie)

Złożona umowa SLA jest umową dotyczącą poziomu usług opartą na wdrażaniu poszczególnych zasobów w obciążeniu. To pole określa _szacowane przestoje_ (oznaczone etykietą _Est. przestój_ w skoroszycie). Aby obliczyć szacowane przestoje w godzinach na rok bez użycia skoroszytu, zastosuj następującą formułę:

> _Szacowany czas przestoju = (1-złożona wartość &#215; procentowa SLA) liczba godzin w roku_

Skoroszyt używa domyślnej wartości _8 760 godzin rocznie_.

### <a name="standard-loss-impact"></a>Standardowy wpływ na utratę

_Standardowy wpływ na utratę_ (oznaczony jako _Standardowy wpływ_ w skoroszycie) prognozuje wpływ na sytuację finansową, przy założeniu, że szacowane prognozowanie _przestojów_ jest dokładne. Aby obliczyć tę prognozę bez użycia skoroszytu, zastosuj następującą formułę:

> _Wpływ standardowy = Szacowana awaria @ trzy 9 czasu &#215; przestoju — wpływ na wartość_

Stanowi to podstawę dla kosztu, gdyby zainteresowane strony biznesowe wypełniły inwestycję w wyższy poziom zarządzania.

### <a name="composite-sla-impact"></a>Złożony wpływ umowy SLA

_Złożony wpływ umowy SLA_ ( _wpływ na poziom zobowiązania_ w skoroszycie) zapewnia zaktualizowany wpływ na kwestie finansowe na podstawie zmian w umowie SLA dotyczącej czasu pracy. To obliczenie pozwala porównać przewidywany wpływ na finanse obu opcji. Aby obliczyć ten wpływ na prognozę bez arkusza kalkulacyjnego, zastosuj następującą formułę:

> _Złożony wpływ umowy SLA = szacowany &#215; czas przestoju — wpływ na wartość_

Wartość reprezentuje potencjalne straty, które mają być nieuniknione przez zmieniony poziom zobowiązania i nową umowną umowę SLA.

### <a name="comparison-basis"></a>Porównanie — podstawa

_Porównanie_ oblicza wpływ na standardowy i złożony wpływ umowy SLA, aby określić, która jest najbardziej odpowiednia w kolumnie zwracanej.

### <a name="return-on-loss-avoidance"></a>Zwróć przy unikaniu utraty strat

Jeśli koszt zarządzania obciążeniem przekracza potencjalne straty, proponowane inwestycje w zarządzanie chmurą mogą nie być rozwijającemu. Aby porównać _zwrot dotyczący unikania utraty strat_, zobacz kolumnę z etykietą roczne zwrotne _*_ * * *. Aby samodzielnie obliczyć tę kolumnę, użyj następującej formuły:

> _Zwróć na uniknięcie utraty = (podstawa porównania — koszt &#215; miesięczny 12) &#247; ) (koszt &#215; miesięczny 12))_

O ile nie istnieją inne nietrwałe czynniki, które należy wziąć pod uwagę, to porównanie może szybko zasugerować, że powinna być zagłębić się w operacji w chmurze, odporności, niezawodności lub w innych obszarach.

## <a name="validate-the-commitment"></a>Weryfikowanie zobowiązania

W tym momencie w procesie zobowiązania zostały wykonane: scentralizowane lub delegowane odpowiedzialności, dzierżawa platformy Azure i poziom zobowiązania. Każde zobowiązanie powinno być zweryfikowane i udokumentowane w celu zapewnienia, że zespół operacyjny w chmurze, zespół strategii chmurowej i zainteresowane strony biznesowe są wyrównane do tego zobowiązania, aby zarządzać obciążeniem.

## <a name="next-steps"></a>Następne kroki

Po dokonaniu zobowiązania odpowiedzialne zespoły operacji mogą rozpocząć konfigurowanie danego obciążenia. Aby rozpocząć, Oceń różne podejścia do [spisu i widoczności](./inventory.md).

> [!div class="nextstepaction"]
> [Opcje spisu i widoczności](./inventory.md)
