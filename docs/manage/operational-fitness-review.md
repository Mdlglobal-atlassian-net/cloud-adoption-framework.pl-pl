---
title: Ustanowienie przeglądu sprawności operacyjnej
description: Ustanów proces przeglądu sprawności operacyjnej w celu pełnego zrozumienia problemów wynikających z uruchamiania obciążeń w środowisku produkcyjnym.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9bc4e2bb9b39a83ab8829ea4a12cd1bb019bf0c3
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341814"
---
# <a name="establish-an-operational-fitness-review"></a>Ustanowienie przeglądu sprawności operacyjnej

Gdy przedsiębiorstwo zaczyna obsługiwać obciążenia na platformie Azure, następnym krokiem jest ustanowienie procesu *przeglądu sprawności operacyjnej*. Ten proces wylicza, implementuje i iteracyjnie przegląda *niefunkcjonalne wymagania* dotyczące tych obciążeń. Niefunkcjonalne wymagania są związane z oczekiwanym zachowaniem operacyjnym usługi.

Istnieje pięć podstawowych kategorii niefunkcjonalnych wymagań, które są nazywane [filarami jakości oprogramowania](https://docs.microsoft.com/azure/architecture/guide/pillars):

- Skalowalność
- Dostępność
- Odporność, w tym ciągłość biznesowa i odzyskiwanie po awarii
- Zarządzanie
- Bezpieczeństwo

Proces kontroli sprawności operacyjnej zapewnia, że obciążenia o kluczowym znaczeniu są zgodne z oczekiwaniami firmy w odniesieniu do filarów jakości.

Utwórz proces dla przeglądu sprawności operacyjnej, aby w pełni zrozumieć problemy wynikające z uruchamiania obciążeń w środowisku produkcyjnym oraz jak skorygować i rozwiązać te problemy. W tym artykule opisano proces wysokiego poziomu dla przeglądu sprawności operacyjnej, którego przedsiębiorstwo może wykorzystać do osiągnięcia tego celu.

## <a name="operational-fitness-at-microsoft"></a>Użyteczność operacyjna w firmie Microsoft

Od samego początku wiele zespołów w firmie Microsoft zabrało rozwój platformy Azure. Trudno jest zapewnić jakość i spójność projektu takiego rozmiaru i złożoności. Konieczny jest niezawodny proces wyliczania i implementowania podstawowych niefunkcjonalnych wymagań w regularnych odstępach czasu.

Procesy, które firma Microsoft stosuje jako podstawy dla procesów przedstawionych w tym artykule.

## <a name="understand-the-problem"></a>Opis problemu

Po [rozpoczęciu pracy](../getting-started/migrate.md), pierwszym krokiem w ramach transformacji cyfrowej przedsiębiorstwa jest zidentyfikowanie problemów firmy, które należy rozwiązać, przyjmując platformę Azure. Następnym krokiem jest określenie rozwiązania wysokiego poziomu problemu, takiego jak Migrowanie obciążenia do chmury lub dostosowanie istniejącej usługi lokalnej do uwzględnienia funkcjonalności chmury. Na koniec warto zaprojektować i zaimplementować rozwiązanie.

W trakcie tego procesu fokus jest często dotyczący funkcji usługi: zestawu wymagań _funkcjonalnych_ , które mają być wykonywane przez usługę. Na przykład usługa dostarczania produktów wymaga funkcji do określenia lokalizacji źródłowej i docelowej produktu, śledzenia produktu podczas dostarczania i wysyłania powiadomień do klienta.

_Niefunkcjonalne_ wymagania, w przeciwieństwie, odnoszą się do właściwości, takich jak [dostępność](https://docs.microsoft.com/azure/architecture/checklist/availability), [odporność](https://docs.microsoft.com/azure/architecture/resiliency)i [skalowalność](https://docs.microsoft.com/azure/architecture/checklist/scalability)usługi. Te właściwości różnią się w zależności od wymagań funkcjonalnych, ponieważ nie wpływają one bezpośrednio na końcową funkcję żadnej konkretnej funkcji w usłudze. Jednak niefunkcjonalne wymagania odnoszą się do wydajności i ciągłości usługi.

Niektóre niefunkcjonalne wymagania można określić w ramach umowy dotyczącej poziomu usług (SLA). Można na przykład przedstawić ciągłość działania usługi jako procent dostępności: "dostępne przez 99,99% czasu". Inne niefunkcjonalne wymagania mogą być trudniejsze do zdefiniowania i mogą ulec zmianie w miarę zmieniania potrzeb produkcyjnych. Na przykład usługi zorientowane konsumentowo mogą ulec nieprzewidzianej przepływności po przejściu do większej popularności.

> [!NOTE]
> Aby uzyskać więcej informacji o wymaganiach dotyczących odporności, zobacz [projektowanie niezawodnych aplikacji platformy Azure](https://docs.microsoft.com/azure/architecture/reliability#define-requirements). Ten artykuł zawiera wyjaśnienia dotyczące pojęć, takich jak cel punktu odzyskiwania (RPO), cel czasu odzyskiwania (RTO) i Umowa SLA.

## <a name="process-for-operational-fitness-review"></a>Proces przeglądu sprawności operacyjnej

Kluczem do utrzymania wydajności i ciągłości usług przedsiębiorstwa jest wdrożenie procesu na potrzeby przeglądu sprawności operacyjnej.

![Przegląd procesu przeglądu sprawności operacyjnej](../_images/manage/ofr-flow.png)

Na wysokim poziomie proces ma dwie fazy. W *fazie wymagania wstępne*wymagania są ustanawiane i mapowane na usługi pomocnicze. Ta faza zdarza się nierzadko: być może rocznie lub w przypadku wprowadzenia nowych operacji. Dane wyjściowe fazy wymagań wstępnych są używane w *fazie przepływu*. Faza przepływu występuje częściej, np. miesięcznie.

### <a name="prerequisites-phase"></a>Faza wymagań wstępnych

Kroki opisane w tej fazie przechwytują wymagania dotyczące przeprowadzania regularnego przeglądu ważnych usług.

1. **Identyfikuj krytyczne operacje biznesowe**. Zidentyfikuj działania biznesowe o kluczowym znaczeniu dla przedsiębiorstwa. Operacje biznesowe są niezależne od funkcjonalności usługi pomocniczej. Innymi słowy, operacje biznesowe reprezentują rzeczywiste działania, które firma musi wykonać, i które są obsługiwane przez zestaw usług IT.

    Termin *"krytyczny"* (lub " *krytyczny dla działalności firmy*") odzwierciedla poważny wpływ na działalność firmy, jeśli operacja jest utrudniona. Na przykład sprzedaż detaliczna w trybie online może być operacją biznesową, taką jak "Włącz klienta, aby dodać element do koszyka" lub "Przetwarzaj płatność kartą kredytową". Jeśli jedna z tych operacji zakończy się niepowodzeniem, klient nie będzie mógł ukończyć transakcji, a firma nie będzie mogła zrealizować sprzedaży.

1. **Mapuj operacje na usługi**. Mapuj krytyczne operacje biznesowe na usługi, które je obsługują. W przypadku koszyka zakupów może być uwzględnionych kilka usług, w tym usługa zarządzania zapasami magazynu i usługa koszyka zakupów. Aby przetwarzać płatność kartą kredytową, lokalna usługa płatnicza może korzystać z usługi przetwarzania płatności innej firmy.

1. **Analizuj zależności usługi**. Większość operacji firmowych wymaga aranżacji między wieloma usługami pomocniczymi. Ważne jest, aby zrozumieć zależności między usługami i przepływ transakcji o kluczowym znaczeniu w ramach tych usług.

    Należy również wziąć pod uwagę zależności między usługami lokalnymi i usługami platformy Azure. W przykładzie koszyka usługa spisu zasobów może być hostowana lokalnie i pobierana przez pracowników z magazynu fizycznego. Może jednak przechowywać dane przechowywane w usłudze Azure, na przykład w usłudze [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction)lub w bazie danych, takie jak [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

Dane wyjściowe z tych działań to zestaw *metryk karty wyników* dla operacji usługi. Karta wyników mierzy kryteria, takie jak dostępność, skalowalność i odzyskiwanie po awarii. Metryki karty wyników wyrażają kryteria operacyjne, których oczekuje usługa. Te metryki mogą być wyrażone na poziomie szczegółowości, który jest odpowiedni dla operacji usługi.

Karta wyników powinna być wyrażona w prostych terminach w celu ułatwienia zrozumiałej dyskusji między właścicielami i inżynierami biznesowymi. Na przykład Metryka karty wyników dla skalowalności może być w prosty sposób kodowane kolorami. Kolor zielony oznacza spełnienie zdefiniowanych kryteriów, żółty oznacza, że nie spełnia on zdefiniowanych kryteriów, ale aktywnie wdraża planowane korygowanie, a czerwony oznacza, że nie spełni zdefiniowanego kryterium bez planu ani akcji.

Ważne jest, aby podkreślić, że te metryki powinny bezpośrednio odzwierciedlać potrzeby biznesowe.

### <a name="service-review-phase"></a>Faza przeglądu usługi

Etap przeglądu usługi jest podstawą przeglądu sprawności operacyjnej. Obejmuje to następujące czynności:

1. **Metryki usługi miary**. Użyj metryk karty wyników do monitorowania usług, aby upewnić się, że usługi spełniają oczekiwania biznesowe. Monitorowanie usług jest niezbędne. Jeśli nie można monitorować zestawu usług w odniesieniu do niefunkcjonalnych wymagań, należy rozważyć odpowiednie metryki karty wyników na czerwono. W takim przypadku pierwszym krokiem do skorygowania jest wdrożenie odpowiedniego monitorowania usługi. Na przykład jeśli firma oczekuje usługi, która będzie działać z 99,99% dostępności, ale nie ma żadnych danych telemetrycznych produkcyjnych w celu mierzenia dostępności, założono, że nie spełniasz wymagań.

2. **Planowanie korygowania**. Dla każdej operacji usługi, dla której metryki spadły poniżej akceptowalnego progu, ustal koszt korygowaniem usługi w celu przeprowadzenia operacji na akceptowalnym poziomie. Jeśli koszt usługi korygowaniem jest większy niż przewidywane generowanie przychodów usługi, przejdź do, aby uwzględnić niematerialne koszty, takie jak obsługa klienta. Na przykład jeśli klienci mają problemy z pomyślnym przekazaniem zamówienia przy użyciu usługi, zamiast tego można wybrać konkurenta.

3. **Zaimplementuj korygowanie**. Gdy właściciele firmy i zespół inżynieryjny zgadzają się na plan, zaimplementuj go. Zgłoś stan implementacji przy każdej analizie metryk karty wyników.

Ten proces jest iteracyjny i jest idealnym rozwiązaniem dla przedsiębiorstwa. Ten zespół powinien regularnie zaspokajać istniejące projekty korygujące, rozpoczynać podstawowe przeglądy nowych obciążeń i śledzić ogólną kartę wyników przedsiębiorstwa. Zespół powinien również mieć uprawnienia do przechowywania zespołów naprawczych, jeśli są one opóźnione lub nie spełnią metryk.

## <a name="structure-of-the-review-team"></a>Struktura zespołu przeglądu

Zespół odpowiedzialny za przegląd sprawności operacyjnej składa się z następujących ról:

- **Właściciel biznesowy:** Zawiera informacje o firmie umożliwiające identyfikację i określanie priorytetów każdej operacji biznesowej o kluczowym znaczeniu. Ta rola również porównuje koszt środków zaradczych z wpływem na działalność biznesową oraz kieruje ostateczną decyzję dotyczącą korygowania.

- Ambasadorzy **biznesowi:** Dzieli operacje biznesowe na części niejawne i mapuje te części na usługi i infrastrukturę, zarówno lokalnie, jak i w chmurze. Rola wymaga głębokiej znajomości technologii skojarzonej z każdą operacją biznesową.

- **Właściciel inżyniera:** Implementuje usługi skojarzone z operacją biznesową. Osoby te mogą uczestniczyć w projektowaniu, wdrażaniu i wdrażaniu wszelkich rozwiązań niefunkcjonalnych problemów, które nie zostały omówione przez zespół recenzji.

- **Właściciel usługi:** Obsługuje aplikacje i usługi firmy. Te osoby te zbierają dane dotyczące rejestrowania i użycia dla tych aplikacji i usług. Te dane są używane zarówno do identyfikowania problemów, jak i weryfikowania poprawek po ich wdrożeniu.

## <a name="review-meeting"></a>Przejrzyj spotkanie

Zalecamy regularne spotkanie zespołu ds. recenzji. Na przykład zespół może spełnić co miesiąc, a następnie raportować stan i metryki do wyższego kierownictwa w oparciu o kwartał.

Dostosuj szczegóły procesu i spotkania zgodnie z konkretnymi potrzebami. Zalecane jest wykonanie następujących zadań jako punktu początkowego:

1. Właściciel firmy i Ambasadorzy biznesowi wyliczają i określają niefunkcjonalne wymagania dla każdej operacji biznesowej oraz dane wejściowe od właścicieli inżynierów i usług. W przypadku operacji firmowych, które zostały wcześniej zidentyfikowane, przejrzyj i sprawdź priorytet. W przypadku nowych operacji roboczych Przypisz priorytet na istniejącej liście.

2. Właściciele inżynierów i usług mapują bieżący stan operacji biznesowej do odpowiednich usług lokalnych i w chmurze. Mapowanie jest listą składników w każdej usłudze, zorientowanych jako drzewo zależności. Właściciele inżynierów i usług określają ścieżki krytyczne w drzewie.

3. Właściciele inżynierów i usług przeglądają bieżący stan rejestrowania i monitorowania operacyjnego usług wymienionych w poprzednim kroku. Niezawodne rejestrowanie i monitorowanie są krytyczne: identyfikują składniki usługi, które przyczyniają się do niespełnienia wymagań niefunkcjonalnych. Jeśli nie ma wystarczającego rejestrowania i monitorowania, zespół musi je umieścić w miejscu przez utworzenie i wdrożenie planu.

4. Zespół tworzy metryki kart wyników dla nowych operacji biznesowych. Karta wyników składa się z listy składników składników dla każdej usługi identyfikowanej w kroku 2. Jest ono wyrównane z niefunkcjonalnymi wymaganiami i zawiera miarę, jak dobrze każdy składnik spełnia wymagania.

5. W przypadku składników składników, które nie spełniają wymagań niefunkcjonalnych, zespół projektuje rozwiązanie wysokiego poziomu i przypisze właściciela inżynierów. W tym momencie właściciel biznesowy i ambasador firmy nawiązują budżet na działania naprawcze w oparciu o oczekiwany przychód operacji biznesowej.

6. Na koniec zespół przeprowadza przegląd trwającej operacji korygowania. Każda Metryka karty wyników dla pracy w toku jest sprawdzana pod kątem oczekiwanych kryteriów. W przypadku składników składników, które spełniają kryteria metryk, właściciel usługi prezentuje dane rejestrowania i monitorowania w celu potwierdzenia spełnienia kryteriów. Dla tych składników składowych, które nie spełniają kryteriów metryk, każdy właściciel inżynierów objaśnia problemy, które uniemożliwiają spełnienie kryteriów i przedstawia wszelkie nowe projekty do skorygowania.

## <a name="recommended-resources"></a>Zalecane zasoby

- [Filary jakości oprogramowania](https://docs.microsoft.com/azure/architecture/guide/pillars).
    W tej części przewodnika po architekturze aplikacji platformy Azure opisano pięć filarów jakości oprogramowania: skalowalność, dostępność, odporność, zarządzanie i zabezpieczenia.
- [Dziesięć zasad projektowania dla aplikacji platformy Azure](https://docs.microsoft.com/azure/architecture/guide/design-principles).
    W tej sekcji przewodnika po architekturze aplikacji platformy Azure omówiono zestaw zasad projektowania, dzięki którym aplikacja jest bardziej skalowalna, odporna na błędy i łatwość zarządzania.
- [Projektowanie odpornych aplikacji na platformę Azure](https://docs.microsoft.com/azure/architecture/resiliency).
    Ten przewodnik rozpoczyna się od definicji _odporności_ i powiązanych koncepcji. Następnie opisuje proces osiągania odporności przy użyciu podejścia strukturalnego w czasie trwania aplikacji, od projektowania i implementacji do wdrożenia i operacji.
- [Wzorce projektowe w chmurze](https://docs.microsoft.com/azure/architecture/patterns).
    Te wzorce projektowe są przydatne dla zespołów inżynieryjnych podczas kompilowania aplikacji na filarach jakości oprogramowania.
- [Azure Advisor](https://docs.microsoft.com/azure/advisor).
    Program Advisor oferuje rekomendacje, które są personalizowane w oparciu o Twoje użycie i konfiguracje, aby ułatwić optymalizację zasobów pod kątem wysokiej dostępności, bezpieczeństwa, wydajności i kosztów.
