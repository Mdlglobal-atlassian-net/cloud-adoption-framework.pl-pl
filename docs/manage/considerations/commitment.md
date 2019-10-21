---
title: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e9ac7b930018e8eb8a8d750692de808be943db0c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558131"
---
# <a name="business-commitment-in-cloud-management"></a>Zobowiązania biznesowe w zarządzaniu chmurą

Zdefiniowanie zobowiązania biznesowego to ćwiczenie priorytetów. Celem jest dostosowanie odpowiedniego poziomu zarządzania operacyjnego przy akceptowalnym koszcie eksploatacyjnym. Znalezienie salda wymaga kilku punktów danych i obliczeń przedstawionych w poniższych sekcjach.

![Balans kosztów i odporności](../../_images/manage/business-commitment-scale.png)

Zobowiązania do stabilności firmy (za pośrednictwem odporności technicznej lub innych wpływów umów SLA) stanowią decyzję o uzasadnieniu biznesowym. W przypadku większości obciążeń w środowisku wystarcza poziom odniesienia zarządzania chmurą. W przypadku innych użytkowników wzrost kosztów w wysokości 2 &ndash;4x jest łatwo uzasadniony ze względu na potencjalny wpływ wszelkich przerw w działaniu firmy. W poprzednich artykułach w tej serii pomoc w zrozumieniu klasyfikacji i wpływu zakłóceń na różne obciążenia. Ten artykuł pomoże w obliczaniu zwracanych wartości. Jak wskazano na poniższej ilustracji, na każdym poziomie zarządzania chmurą istnieją punkty przegięcia, w których koszt może wzrosnąć szybciej niż zwiększa odporność. Te punkty przegięcia będą monitował szczegółowe decyzje biznesowe i zobowiązania biznesowe.

## <a name="determining-a-proper-commitment-with-the-business"></a>Określenie właściwego zaangażowania z firmą

Dla każdego obciążenia w teczce zespół operacyjny chmury i zespół strategii chmury powinien dostosować poziom zarządzania udostępniony bezpośrednio przez zespół operacyjny chmury.

Poniżej znajdują się kluczowe aspekty, które należy dostosować podczas ustanawiania zobowiązania z firmą:

- Wymagania wstępne dotyczące operacji IT
- Odpowiedzialność za zarządzanie
- Dzierżawa w chmurze
- Nietrwałe czynniki kosztowe
- Zwrot z inwestycji
- Sprawdzanie poprawności poziomu zarządzania

Pozostała część tego artykułu zawiera konspekt każdego z tych kryteriów, aby pomóc w podejmowaniu decyzji.

## <a name="it-operations-prerequisites"></a>Wymagania wstępne dotyczące operacji IT

[Przewodnik zarządzania platformy Azure](../azure-management-guide/index.md) zawiera opis narzędzi do zarządzania dostępnych na platformie Azure. Przed osiągnięciem zobowiązania z działalnością należy określić akceptowalną podstawową linię bazową zarządzania, która ma być stosowana do wszystkich zarządzanych obciążeń. Następnie obliczy standardowy koszt zarządzania dla każdego z zarządzanych obciążeń w portfolio IT, na podstawie liczby rdzeni procesora CPU, miejsca na dysku i innych zmiennych związanych z zasobami. Ponadto Szacowana zostanie złożona umowa SLA dla każdego obciążenia w oparciu o architekturę.

> [!TIP]
> Zespoły operacji IT często używają domyślnego minimum 99,9% czasu dla początkowej złożonej umowy SLA. Mogą również zdecydować się na normalizację kosztów zarządzania na podstawie średniego obciążenia, szczególnie w przypadku rozwiązań o minimalnych wymaganiach dotyczących rejestrowania i magazynowania. Uśrednianie kosztów kilku obciążeń o krytycznym znaczeniu może zapewnić punkt początkowy dla początkowych konwersacji.

> [!TIP]
> Dla czytelników, którzy korzystają z [skoroszytu usługi Ops Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) do planowania zarządzania chmurą, należy zaktualizować pola zarządzania Ops, aby odzwierciedlały te wymagania wstępne. Te pola obejmują poziom zobowiązania, umowę SLA i koszt miesięczny. Koszt miesięczny powinien przedstawiać miesięczne koszty dodatkowych narzędzi do zarządzania operacyjnego.

Linia bazowa zarządzania operacjami będzie służyć jako początkowy punkt początkowy do zweryfikowania w każdej z poniższych sekcji.

## <a name="management-responsibility"></a>Odpowiedzialność za zarządzanie

W tradycyjnych środowiskach lokalnych koszt zarządzania środowiskiem jest zwykle uznawany za Sunk kosztem firmy. W chmurze zarządzanie jest decyzją nigdy wykonywane celowo z bezpośrednim wpływem na budżet. Koszty każdej funkcji zarządzania mogą być bezpośrednio przypisane do poszczególnych obciążeń wdrożonych w chmurze. Takie podejście pozwala na większą kontrolę, ale tworzy wymaganie zespołów operacyjnych w chmurze i zespołów strategii chmurowej, aby najpierw zatwierdzić umowę dotyczącą odpowiedzialności.

**Delegowana odpowiedzialność:** Ze względu na to, że nie ma potrzeby scentralizowania i przyjmowania kosztów zarządzania operacyjnego, operacje działu IT w wielu organizacjach rozważają nowe podejścia. Jedną z typowych metod nazywa się delegowanie odpowiedzialności. W centrum usług w chmurze, operacje na platformie i Automatyzacja platformy zapewniają samoobsługowe narzędzia do zarządzania, które mogą być używane przez zespoły operacyjne prowadzone przez firmę, niezależnie od centralnych zespołów operacyjnych IT. Takie podejście zapewnia uczestnikom współpracy pełną kontrolę nad budżetami związanymi z zarządzaniem. Umożliwia także CCoE, aby upewnić się, że minimalny zestaw guardrails jest prawidłowo zaimplementowany. W tym modelu działa jako Broker i przewodnik ułatwiający podejmowanie decyzji w firmie. Operacje biznesowe nadzorują codzienne operacje zależnych obciążeń.

**Centralna odpowiedzialność:** Wymagania dotyczące zgodności, złożoność techniczna i niektóre modele usług udostępnionych mogą wymagać centralnego modelu IT. W tym modelu kontynuuje konserwację obowiązków zarządzania operacjami. W związku z tym, projektowanie środowiska, kontrole zarządzania i narzędzia ładu mogą być centralnie zarządzane i kontrolowane, co ogranicza rolę zainteresowanych uczestników firmy podczas wykonywania zobowiązań w zakresie zarządzania. Jednak widoczność kosztów i architektury rozwiązań w chmurze znacznie ułatwia scentralizowanemu działowi IT przekazanie kosztów i poziomu zarządzania dla każdego obciążenia.

**Model mieszany:** Klasyfikacja jest niezwykle ważnym modelem mieszanym do obowiązków związanych z zarządzaniem. Firmy, które znajdują się w pośrodku transformacji z lokalizacji lokalnej do chmury, mogą wymagać od siebie pierwszego modelu operacyjnego. Inne firmy, które mają ścisłe wymagania w zakresie zgodności lub zależą od długoterminowych umów z dostawcą usług IT, mogą wymagać scentralizowanego modelu operacyjnego. Pomimo tego typu ograniczeń firmy mają potrzebę innowacji. Gdy błyskawiczne innowacje muszą przyozdobć, w pośrodku scentralizowanego modelu odpowiedzialności centralnej IT, klasyfikacja i model mieszany mogą zapewnić balans. W tym podejściu centralnie udostępnia scentralizowany model operacyjny dla wszystkich obciążeń, które są krytyczne lub zawierają informacje poufne. Wszystkie inne klasyfikacje obciążeń mogą jednak zostać umieszczone w środowisku chmury przeznaczonym do delegowanych obowiązków. Podejście do scentralizowanej odpowiedzialności służy jako ogólny model operacyjny. Dzięki tej firmie można elastycznie korzystać z wyspecjalizowanego modelu operacyjnego na podstawie wymaganego poziomu pomocy technicznej i czułości.

Pierwszym krokiem jest zatwierdzenie do podejścia do odpowiedzialności, które będzie kształtować następujące zobowiązania.

**Która organizacja będzie odpowiedzialna za codzienne zarządzanie operacjami w tym obciążeniu?**

## <a name="cloud-tenancy"></a>Dzierżawa w chmurze

Chociaż nie jest to zalecane, firma nie może obsługiwać zasobów w wielu dzierżawach. Artykuł w witrynie Lighthouse dla wielu dzierżawców zawiera kilka przykładów dla wielodostępnych środowisk platformy Azure. W oparciu o przykłady w tym artykule następnym zobowiązaniem jest dzierżawa.

**Czy to obciążenie będzie się znajdować w jednej dzierżawie platformy Azure wraz ze wszystkimi innymi obciążeniami?**

## <a name="soft-cost-factors"></a>Nietrwałe czynniki kosztowe

W następnej sekcji tego artykułu przedstawiono podejście do zwrotów porównawczych związanych z poziomami procesów zarządzania i narzędziami. Na końcu tej sekcji każde analizowane obciążenie będzie mierzyć koszt zarządzania względem przewidywanego wpływu zakłóceń działania firmy. Takie podejście zapewni stosunkowo łatwy sposób zrozumienia, czy inwestycja w bardziej zaawansowane podejścia do zarządzania jest uzasadniona.

Przed uruchomieniem liczb należy zwrócić uwagę na nietrwałe czynniki. Nieprzerwane czynniki kosztowe generują zwrot, ale to nie jest trudne do mierzenia dzięki bezpośredniemu oszczędności kosztów, które byłyby widoczne w rachunku zysków i strat. Nietrwałe czynniki kosztowe są ważne, ponieważ mogą wskazywać potrzebę zainwestowania na wyższy poziom zarządzania niż w rozsądny sposób.

Poniżej przedstawiono kilka przykładów tych czynników:

- Codziennie używaj obciążenia przez tablicę lub dyrektora naczelnego.
- Użycie obciążenia przez pierwszych _x%_ klientów, którzy prowadzą do wyższego wpływu na dochody w innym miejscu.
- Wpływ na zadowolenie pracowników.

Następny punkt danych wymagany do podjęcia zobowiązania to lista nieelastycznych czynników kosztów. Te nie muszą być udokumentowane na tym etapie, ale uczestnik projektu biznesowego powinien mieć świadomość znaczenia tych czynników i ich wykluczenia z następujących obliczeń.

## <a name="calculate-loss-avoidance-roi"></a>Oblicz zwrot z inwestycji

Podczas obliczania względnych zwrotów kosztów zarządzania operacjami zespół IT odpowiedzialny za operacje w chmurze powinien spełnić powyższe wymagania wstępne i założyć minimalny poziom zarządzania dla wszystkich obciążeń.

Następne zobowiązanie, które należy wykonać, jest akceptacją przez firmę kosztów związanych z ofertą zarządzaną przez linię bazową.

**Czy firma wyraża zgodę na inwestycję w linię bazową w celu spełnienia minimalnych standardów operacji w chmurze?**

Jeśli firma nie wyraża zgody na ten poziom zarządzania, należy opracować rozwiązanie, które umożliwi firmie dalsze działanie, bez istotnego wpływu na operacje w chmurze innych obciążeń.

Jeśli firma chce mieć więcej niż poziom standardowy, w pozostałej części tej sekcji można sprawdzić poprawność inwestycji i skojarzonych zwrotów (w postaci unikania utraty informacji).

### <a name="increased-levels-of-management-design-principles-and-service-catalog"></a>Zwiększone poziomy zarządzania: zasady projektowania i katalog usług

W przypadku rozwiązań zarządzanych istnieje kilka zasad projektowania i rozwiązań szablonów, które można zastosować oprócz linii bazowej zarządzania. Każda z zasad projektowania pod kątem niezawodności i odporności dodaje koszt operacyjny do obciążenia. W odniesieniu do tych dodatkowych zobowiązań i działalności biznesowej ważne jest zapoznanie się z potencjalnymi stratami, które można uniknąć przez zwiększenie inwestycji.

Poniższe obliczenia przeprowadzą przez formuły, aby lepiej zrozumieć porównanie strat i zwiększone inwestycje w zarządzanie. Aby uzyskać wskazówki dotyczące obliczania kosztów zwiększonego zarządzania, zapoznaj się z artykułami dotyczącymi [automatyzacji obciążeń](./workload.md) i [automatyzacji platform](./platform.md).

> [!TIP]
> Dla czytelników, którzy korzystają z [skoroszytu usługi Ops Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) do planowania zarządzania chmurą, należy zaktualizować pola zarządzania Ops, aby odzwierciedlić każdą konwersację. Te pola obejmują poziom zobowiązania, umowę SLA i koszt miesięczny. Koszt miesięczny powinien przedstawiać miesięczne koszty dodatkowych narzędzi do zarządzania operacyjnego. Po zaktualizowaniu te pola będą aktualizować formuły zwrotu z inwestycji i każde z poniższych pól.

### <a name="estimate-outage-hours-per-year"></a>Oszacowanie przestoju (godz. rocznie)

"Złożona umowa SLA" jest umową dotyczącą poziomu usług opartą na wdrażaniu poszczególnych zasobów w obciążeniu. To pole będzie miało na celu "szacowane przestoje" (oznaczone etykietą EST). Przestój * * * w skoroszycie). Aby obliczyć szacowane przestoje w godzinach na rok bez użycia skoroszytu, zastosuj następującą formułę:

**Szacowany czas przestoju = (1-złożona wartość procentowa SLA)/* liczba godzin w roku* *

W skoroszycie jest używana domyślna wartość 8 760 godzin na rok.

### <a name="standard-loss-impact"></a>Standardowy wpływ na utratę

Standardowy wpływ na utratę (zatytułowany "wpływ standardowy" w skoroszycie) prognozuje wpływ ewentualnych przestojów, przy założeniu, że przewidywanie "szacowane przestoje" potwierdza dokładne. Aby obliczyć tę prognozę bez użycia skoroszytu, zastosuj następującą formułę:

**Wpływ standardowy = Szacowana awaria @ trzy 9-* procentowy wpływ na czas* pracy/wartość *

Stanowi to podstawę dla kosztu, gdyby zainteresowane strony biznesowe wypełniły inwestycję w wyższy poziom zarządzania.

### <a name="composite-sla-impact"></a>Złożony wpływ umowy SLA

Złożony wpływ umowy SLA (zatytułowany "wpływ na poziom zobowiązania" w skoroszycie) zapewnia zaktualizowany wpływ na kwestie finansowe na podstawie zmian w umowie SLA dotyczącej czasu pracy. Pozwala to porównać przewidywany wpływ na finanse obu opcji. Aby obliczyć przewidywany wpływ bez użycia arkusza kalkulacyjnego, zastosuj następującą formułę.

**Złożony wpływ umowy SLA = szacowany wpływ przestoju/* czasu na wartość* *

Wartość reprezentuje potencjalne straty, które mają być nieuniknione przez zmieniony poziom zobowiązania i nową umowną umowę SLA.

### <a name="comparison-basis"></a>Porównanie — podstawa

Porównanie oblicza wpływ na standardowy i złożony wpływ umowy SLA, aby określić, która jest najbardziej odpowiednia w kolumnie zwracanej.

### <a name="return-on-loss-avoidance"></a>Zwróć przy unikaniu utraty strat

Jeśli koszt zarządzania obciążeniem przekracza potencjalne straty, proponowane inwestycje w zarządzanie chmurą mogą nie być rozwijającemu. Aby porównać "zwracanie po utracie strat", zobacz kolumnę zatytułowaną "roczna subskrypcja * * * *". Aby samodzielnie obliczyć tę kolumnę, Użyj tej formuły:

**Zwróć po uniknięciu utraty = (podstawa porównania — koszt miesięczny/* 12))//(koszt miesięczny/* 12)) **

Jeśli nie istnieją inne nietrwałe czynniki, które należy wziąć pod uwagę, to porównanie może szybko zasugerować, że powinna być bardziej zaproponowana w przypadku operacji w chmurze, odporności, niezawodności lub innych obszarów.

## <a name="validate-the-commitment"></a>Weryfikowanie zobowiązania

W tym momencie w procesie zobowiązania zostały wykonane: scentralizowane lub delegowane odpowiedzialności, dzierżawa platformy Azure i poziom zobowiązania.
Każde zobowiązanie powinno być zweryfikowane i udokumentowane w celu zapewnienia, że zespół operacyjny w chmurze, zespół strategii chmurowej i zainteresowane strony biznesowe są wyrównane do tego zobowiązania, aby zarządzać obciążeniem.

## <a name="next-steps"></a>Następne kroki

Po dokonaniu zobowiązania odpowiedzialne zespoły operacji mogą rozpocząć konfigurację dla danego obciążenia. Aby rozpocząć, Oceń różne podejścia do [spisu i widoczności](./inventory.md).

> [!div class="nextstepaction"]
> [Opcje spisu i widoczności](./inventory.md)
