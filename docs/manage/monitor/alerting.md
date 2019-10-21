---
title: Przewodnik monitorowania w chmurze — alerty
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Określ, kiedy używać Azure Monitor lub System Center Operations Manager w Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 0157cf5c50cd676478b28889b565c7f3f6952e32
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548603"
---
# <a name="cloud-monitoring-guide-alerting"></a>Przewodnik po monitorowaniu w chmurze: alerty

W latach organizacje IT miały problemy z zwalczaniem zmęczenia alertów utworzonego przez narzędzia monitorowania wdrożone w przedsiębiorstwie. Wiele systemów generuje dużą liczbę alertów często uważanych za bezużyteczne, a inne są istotne, ale są lub ignorowane. W związku z tym, działania IT i dla deweloperów zostały niezmienione w celu zaspokojenia jakości poziomu usług wykorzystanej dla klientów wewnętrznych lub zewnętrznych. Konieczna jest znajomość stanu infrastruktury i aplikacji w celu zapewnienia niezawodności. Należy szybko identyfikować przyczyny, aby zminimalizować spadek wydajności i przerwy w działaniu usługi lub zmniejszyć liczbę incydentów.

## <a name="successful-alerting-strategy"></a>Strategia pomyślnego alertu

*Nie możesz rozwiązać tego, co nie jest już znane.*

Ostrzegaj o znaczeniu krytycznym. Jest on przypięty przez gromadzenie i mierzenie właściwych metryk i dzienników. Potrzebne jest również narzędzie do monitorowania, które umożliwia przechowywanie, agregowanie, wizualizowanie, analizowanie i Inicjowanie automatycznej reakcji po spełnieniu warunków. Poprawa przestrzegania usług i aplikacji może być realizowana tylko w przypadku całkowitego zrozumienia jego kompozycji. Należy zmapować tę kompozycję do szczegółowej konfiguracji monitorowania, która ma zostać zastosowana przez platformę monitorowania. Dotyczy to również przewidywalnych Stanów niepowodzeń (objawy nie przyczyny awarii), które mają sens dla alertu.

Aby określić, czy objaw jest odpowiednim kandydatem do zgłaszania alertów, należy wziąć pod uwagę następujące zasady:

- **Czy ma to znaczenie?** Czy problem polega na objawem problemu lub problemie związanym z ogólną kondycją aplikacji? Czy na przykład chcesz mieć ostrożność, jeśli użycie procesora CPU jest wysokie dla zasobu? Lub że określone zapytanie SQL uruchomione w wystąpieniu bazy danych SQL w tym zasobie zużywa wysokie wykorzystanie procesora CPU w okresie dłuższym? Ponieważ warunek użycia procesora CPU jest rzeczywistym problemem, należy go ostrzec. Ale nie musisz powiadamiać zespołu, ponieważ nie ma on informacji o tym, co jest przyczyną warunku w pierwszym miejscu. Alerty i powiadamianie o problemach z użyciem procesu zapytania SQL są odpowiednie i funkcjonalne.
- **Czy jest to pilne?** Czy problem jest prawdziwy i czy wymaga pilnej uwagi? Jeśli tak, to odpowiedzialny zespół powinien natychmiast zostać powiadomiony.
- **Czy klienci mają te zmiany?** Czy przyczyną problemu mogą być użytkownicy usługi lub aplikacji?
- **Czy są to inne zależne systemy?** Czy istnieją alerty z zależności, które są powiązane, i które mogą być skorelowane, aby uniknąć informowania innych zespołów pracujących nad tym samym problemem?

Zadawaj te pytania, gdy początkowo tworzysz konfigurację monitorowania. Testowanie i weryfikowanie założeń w środowisku nieprodukcyjnym, a następnie wdrażanie do produkcji. Konfiguracje monitorowania są uzyskiwane z znanych trybów niepowodzeń, wyników testów symulowanych błędów i doświadczeń od różnych członków zespołu.

Po wydaniu konfiguracji monitorowania możesz uzyskać informacje na temat pracy i tego, co się nie dzieje. Należy wziąć pod uwagę wysoki poziom alertów, problemy niezauważalne przez monitorowanie, ale zauważalne przez użytkowników końcowych i jakie były najlepsze działania w ramach tej oceny. Zidentyfikuj zmiany do wdrożenia w celu usprawnienia dostarczania usługi w ramach trwającego, ciągłego procesu ulepszania monitorowania. Nie tylko oceniasz zakłócenia alertów lub pominięte alerty, ale również efektywność monitorowania obciążenia. Jest to informacje o wydajności zasad alertów, procesu i ogólnej kulturze, aby określić, czy są one ulepszane.

Zarówno System Center Operations Manager, jak i Azure Monitor obsługują alerty w oparciu o statyczne lub nawet dynamiczne wartości progowe i akcje skonfigurowane na ich podstawie. Przykładami mogą być alerty dla wiadomości e-mail, wiadomości SMS i połączeń głosowych w przypadku prostych powiadomień. Obie te usługi obsługują także integrację narzędzia ITSM, które automatyzują tworzenie rekordów zdarzeń i eskalację do właściwego zespołu pomocy technicznej lub dowolnego innego systemu zarządzania alertami przy użyciu elementu webhook.

Jeśli to możliwe, można użyć dowolnej z kilku usług w celu zautomatyzowania akcji odzyskiwania. Obejmują one program System Center Orchestrator, Azure Automation, Azure Logic Apps lub Skalowanie automatyczne w przypadku obciążeń elastycznych. Podczas powiadamiania zespołów odpowiedzialnych za Najczęstsze działania związane z alertami mogą być również wymagane automatyzację działań naprawczych. Może to usprawnić cały proces zarządzania zdarzeniami. Automatyzacja tych zadań odzyskiwania może również zmniejszyć ryzyko wystąpienia błędu ludzkiego.

## <a name="azure-monitor-alerting"></a>Alerty Azure Monitor

Jeśli używasz wyłącznie Azure Monitor, poniższe wskazówki dotyczą programu. Postępuj zgodnie z poniższymi wskazówkami przy rozważaniu szybkości, kosztów i ilości miejsca do magazynowania w Azure Monitor.

Istnieje sześć repozytoriów, które przechowują dane monitorowania, w zależności od używanej funkcji i konfiguracji.

- **Baza danych metryk Azure Monitor.** Baza danych szeregów czasowych używana głównie do metryk Azure Monitor platformy, ale również ma Application Insights dane metryk są dublowane. Informacje wprowadzane do tej bazy danych mają najszybszy czas alertów.

- **Magazyn dzienników Application Insights.** Baza danych przechowująca większość Application Insights telemetrii w formularzu dziennika.

- **Magazyn dzienników Azure Monitor.** Magazyn podstawowy dla danych dziennika platformy Azure. Inne narzędzia umożliwiają kierowanie danych do nich i można je analizować w dziennikach Azure Monitor. Zapytania alertów dziennika mają większe opóźnienia z powodu pozyskiwania i indeksowania. To opóźnienie jest zwykle 5-10 minut, ale może być większe w pewnych okolicznościach.

- **Magazyn dziennika aktywności.** Używany dla wszystkich zdarzeń dziennika aktywności i kondycji usługi. Możliwe jest wygenerowanie alertów. Przechowuje zdarzenia poziomu subskrypcji występujące na obiektach w subskrypcji, jak widać poza tymi obiektami. Na przykład po ustawieniu zasad lub uzyskaniu dostępu do zasobu.

- **Usługa Azure Storage.** Magazyn ogólnego przeznaczenia obsługiwany przez Diagnostyka Azure i inne narzędzia do monitorowania. Jest to niska cena opcji długoterminowego przechowywania danych telemetrycznych monitorowania. Alerty nie są obsługiwane na podstawie danych przechowywanych w tej usłudze.

- **Event Hubs.** Zwykle używany do przesyłania strumieniowego danych do narzędzi monitorowania/narzędzia ITSM w środowisku lokalnym lub innym partnerom.

Istnieją cztery typy alertów w Azure Monitor, które są nieco powiązane z repozytorium, w którym są przechowywane dane.

- [Alert dotyczący metryki](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric). Alerty dotyczące danych w bazie danych metryk Azure Monitor. Alerty występują, gdy monitorowana wartość przekroczy próg zdefiniowany przez użytkownika, a następnie ponownie, gdy powróci do stanu "normalny".

- [Alert dotyczący zapytania dziennika](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query). Dostępne dla alertów dotyczących zawartości w magazynach Application Insights lub dzienników platformy Azure. Może również generować alerty oparte na zapytaniach między obszarami roboczymi.

- [Alert dziennika aktywności](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log). Alerty dotyczące elementów w magazynie dzienników aktywności, z wyjątkiem danych Service Health.

- [Service Health alertu](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json). Specjalny typ alertu, tylko w przypadku Service Health problemów pochodzących z magazynu dziennika aktywności.

### <a name="alerting-through-partner-tools"></a>Alerty za poorednictwem narzędzi partnerskich

Jeśli używasz rozwiązania do tworzenia alertów zewnętrznych, Roześlij je tak, jak to możliwe za pośrednictwem usługi Azure Event Hubs, ponieważ najszybszą ścieżką jest Azure Monitor. Musisz zanieść opłaty za pozyskiwanie w centrum zdarzeń. Jeśli koszt jest problemem i szybkość nie, możesz użyć usługi Azure Storage jako tańszej alternatywy. Wystarczy upewnić się, że narzędzia do monitorowania i narzędzia ITSM mogą odczytywać dane z usługi Azure Storage w celu wyodrębnienia danych.

Azure Monitor obejmuje obsługę integracji z innymi platformami monitorowania i oprogramowaniem narzędzia ITSM, takim jak usługi ServiceNow. Możesz korzystać z alertów platformy Azure i nadal wyzwalać akcje poza platformą Azure zgodnie z wymaganiami procesu zarządzania zdarzeniami lub DevOps. Jeśli chcesz otrzymywać alerty w Azure Monitor i zautomatyzować odpowiedź, możesz inicjować automatyczne akcje przy użyciu Azure Functions, Azure Logic Apps lub Azure Automation na podstawie Twojego scenariusza i wymagań.

### <a name="specialized-azure-monitoring-offerings"></a>Wyspecjalizowane oferty monitorowania platformy Azure

[Rozwiązania do zarządzania](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) zwykle przechowują swoje dane w magazynie dzienników platformy Azure. Dwa wyjątki są Azure Monitor dla maszyn wirtualnych i Azure Monitor dla kontenerów. W poniższej tabeli opisano środowisko alertów w oparciu o określony typ danych i miejsce, w którym są przechowywane.

Rozwiązanie| Typ danych | Zachowanie alertu
:---|:---|:---
Usługa Azure Monitor dla kontenerów | Obliczone średnie dane wydajności z węzłów i zasobników są zapisywane w magazynie metryk. | Tworzenie alertów dotyczących metryk, jeśli chcesz otrzymywać alerty w oparciu o wahania wydajności zmierzonego wykorzystania, zagregowane w czasie.
|| Obliczone dane wydajności używające percentylów z węzłów, kontrolerów, kontenerów i zasobników są zapisywane w magazynie dzienników. Dzienniki kontenerów i informacje o spisie są również zapisywane w magazynie dzienników. | Utwórz alerty kwerendy dziennika, jeśli chcesz otrzymywać alerty na podstawie zmienności mierzonego użycia z klastrów i kontenerów. Alerty zapytań dzienników można również skonfigurować na podstawie liczby faz i liczby węzłów stanu.
Usługa Azure Monitor dla maszyn wirtualnych | Kryteria kondycji są metrykami zapisanymi w magazynie metryk. | Alerty są generowane, gdy stan kondycji ulegnie zmianie z kondycji na stan w złej kondycji. Obsługuje tylko grupy akcji skonfigurowane do wysyłania wiadomości SMS lub powiadomień e-mail.
|| Dane dziennika wydajności mapy i systemu operacyjnego gościa są zapisywane w magazynie dzienników. | Utwórz alerty zapytania dziennika.

### <a name="fastest-speed-driven-by-cost"></a>Najszybsza szybkość według kosztu

Opóźnienie to jedna z najważniejszych decyzji, które obejmują alerty i szybkie rozwiązywanie problemów wpływających na usługę. Jeśli potrzebujesz alertów niemal w czasie rzeczywistym w ciągu pięciu minut, Oceń pierwsze, jeśli masz lub można otrzymywać alerty dotyczące danych telemetrycznych, w których są one domyślnie przechowywane. Ogólnie rzecz biorąc, ta strategia jest również najtańszą opcją, ponieważ używane narzędzie już wysyła swoje dane do tej lokalizacji.

Tym samym, istnieje kilka ważnych przypisów dla tej reguły.

**Telemetrię systemu operacyjnego gościa** ma wiele ścieżek do pobrania w systemie.

- Najszybszy sposób na wysłanie alertów dotyczących tych danych polega na zaimportowaniu ich jako metryki niestandardowych. W tym celu należy użyć rozszerzenia Diagnostyka Azure, a następnie użyć alertu dotyczącego metryki. Jednak metryki niestandardowe są obecnie dostępne w wersji zapoznawczej i są [droższe niż inne opcje](https://azure.microsoft.com/pricing/details/monitor).

- Najtańsza, ale najwolniejsza Metoda polega na wysłaniu jej do magazynu Kusto dzienników platformy Azure. Uruchomienie agenta Log Analytics na maszynie wirtualnej jest najlepszym sposobem na uzyskanie wszystkich metryk systemu operacyjnego gościa i danych dzienników do tego magazynu.

- Można wysłać do obu magazynów, uruchamiając zarówno rozszerzenie, jak i agenta na tej samej maszynie wirtualnej. Następnie możesz szybko otrzymywać alerty, ale również używać danych systemu operacyjnego gościa w ramach bardziej złożonych wyszukiwań w połączeniu z inną telemetrią.

**Importowanie danych z lokalnego.** Jeśli próbujesz wysyłać zapytania i monitorować między maszynami działającymi na platformie Azure i lokalnymi, możesz użyć agenta Log Analytics, aby zbierać dane systemu operacyjnego gościa. Następnie można użyć funkcji o nazwie [Logs do metryk](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) , aby usprawnić te metryki w magazynie metryk. Ta metoda pomija część procesu pozyskiwania w magazynie dzienników platformy Azure i w ten sposób jest dostępna wcześniej w bazie danych metryk.

### <a name="minimize-alerts"></a>Minimalizuj alerty

Jeśli używasz rozwiązania, takiego jak Azure Monitor dla maszyn wirtualnych i Znajdź domyślne kryteria kondycji, które monitoruje akceptowalny stopień wykorzystania wydajności, nie twórz nakładających się metryk ani zapytań dziennika na podstawie tych samych liczników wydajności.

Jeśli nie używasz Azure Monitor dla maszyn wirtualnych, zapoznaj się z następującymi funkcjami, aby utworzyć zadanie tworzenia alertów i zarządzać powiadomieniami:

> [!NOTE]
> Te funkcje mają zastosowanie tylko do alertów metryk; oznacza to, że alerty na podstawie danych wysyłanych do bazy danych metryk Azure Monitor. Nie dotyczą one innych typów alertów. Jak wspomniano wcześniej, głównym celem alertów dotyczących metryk jest szybkość. Jeśli alert w ciągu mniej niż 5 minut nie jest istotny, możesz zamiast tego użyć alertu zapytania dziennika.

- [Progi dynamiczne](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds). Progi dynamiczne sprawdzają aktywność zasobu w danym okresie i tworzą górne i dolne progi "normalne zachowanie". Gdy monitorowana Metryka wykracza poza te progi, zostanie wyświetlony alert.

- [Alerty wielokrotne](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts). Można utworzyć alert dotyczący metryki, który używa kombinacji dwóch różnych danych wejściowych z dwóch różnych typów zasobów. Na przykład jeśli chcesz uruchomić alert, gdy procesor maszyny wirtualnej przekracza 90 procent, a liczba komunikatów w określonej Azure Service Bus kolejce obsłużyć tę maszynę wirtualną, można to zrobić bez tworzenia zapytania dziennika. Działa to tylko w przypadku dwóch sygnałów. W przypadku bardziej złożonej kwerendy podawanie danych metryki do magazynu dzienników Azure Monitor i użycie zapytania dziennika.

- [Alerty wielozasobów](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts). Azure Monitor zezwala na regułę alertu o pojedynczej metryce, która ma zastosowanie do wszystkich zasobów maszyny wirtualnej. Ta funkcja może zaoszczędzić czas, ponieważ nie trzeba tworzyć poszczególnych alertów dla każdej maszyny wirtualnej. Cennik tego typu alertu jest taki sam. Jeśli utworzono alerty 50 na potrzeby monitorowania użycia procesora CPU dla maszyn wirtualnych 50 lub 1 alert, który monitoruje użycie procesora dla wszystkich maszyn wirtualnych 50, koszt ten jest taki sam. Te typy alertów można również używać w połączeniu z progami dynamicznymi.

Te funkcje umożliwiają zaoszczędzenie czasu przez zminimalizowanie powiadomień o alertach i zarządzanie alertami.

### <a name="alerts-limitations"></a>Ograniczenia alertów

Pamiętaj, aby zanotować [ograniczenia](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) liczby alertów, które można utworzyć. Niektóre ograniczenia (ale nie wszystkie z nich) można zwiększyć, wywołując pomoc techniczną.

### <a name="best-query-experience"></a>Najlepsze środowisko zapytań

Jeśli szukasz trendów we wszystkich danych, warto zaimportować wszystkie dane do dzienników platformy Azure, chyba że są one już w Application Insights. Można tworzyć zapytania w obu obszarach roboczych, dlatego nie ma potrzeby przenoszenia danych między nimi. Możesz również zaimportować dziennik aktywności i Service Health dane do obszaru roboczego Log Analytics. Płacisz za ten pozyskiwanie i przechowywanie, ale uzyskasz wszystkie dane w jednym miejscu na potrzeby analizy i wykonywania zapytań. Daje to również możliwość tworzenia złożonych warunków zapytania i alertów.
