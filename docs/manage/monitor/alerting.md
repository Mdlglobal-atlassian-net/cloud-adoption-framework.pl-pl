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
ms.openlocfilehash: efbb3b677f2349f0d2e8c240c42c75d75cf849f1
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564992"
---
# <a name="cloud-monitoring-guide-alerting"></a>Przewodnik po monitorowaniu w chmurze: alerty

W latach organizacje IT miały problemy z zwalczaniem zmęczenia alertów utworzonego przez narzędzia do monitorowania wdrożone w przedsiębiorstwie. Wiele systemów generuje dużą liczbę alertów często uważanych za bezużyteczne, podczas gdy inne alerty są istotne, ale są lub ignorowane. W związku z tym, działania IT i dla deweloperów zostały niezmienione w celu zaspokojenia jakości poziomu usług wykorzystanej dla klientów wewnętrznych lub zewnętrznych. Aby zapewnić niezawodność, konieczna jest znajomość stanu infrastruktury i aplikacji. Aby zminimalizować spadek wydajności i przerwy w działaniu usługi lub zmniejszyć liczbę incydentów, należy szybko zidentyfikować przyczyny.

## <a name="successful-alerting-strategy"></a>Strategia pomyślnego alertu

*Nie możesz rozwiązać tego, co nie jest już znane.*

Ostrzegaj o znaczeniu krytycznym. Jest on przypięty przez gromadzenie i mierzenie właściwych metryk i dzienników. Potrzebne jest również narzędzie do monitorowania, które umożliwia przechowywanie, agregowanie, wizualizowanie, analizowanie i Inicjowanie automatycznej reakcji po spełnieniu warunków. Możesz poprawić przestrzeganie usług i aplikacji tylko wtedy, gdy w pełni zrozumiesz jej kompozycję. Należy zmapować tę kompozycję do szczegółowej konfiguracji monitorowania, która ma zostać zastosowana przez platformę monitorowania. Ta konfiguracja obejmuje przewidywalne Stany niepowodzeń (objawy, a nie przyczyny awarii), które mają sens dla alertu.

Aby określić, czy objaw jest odpowiednim kandydatem do zgłaszania alertów, należy wziąć pod uwagę następujące zasady:

- **Czy ma to znaczenie?** Czy problem polega na objawem problemu lub problemie związanym z ogólną kondycją aplikacji? Czy na przykład chcesz zadbać o to, czy wykorzystanie procesora CPU jest wysokie dla zasobu? Lub że określone zapytanie SQL uruchomione w wystąpieniu bazy danych SQL w tym zasobie zużywa wysokie wykorzystanie procesora CPU w okresie dłuższym? Ponieważ warunek użycia procesora CPU jest rzeczywistym problemem, należy go ostrzec. Ale nie musisz powiadamiać zespołu, ponieważ nie ma on informacji o tym, co jest przyczyną warunku w pierwszym miejscu. Alerty i powiadamianie o problemach z użyciem procesu zapytania SQL są odpowiednie i funkcjonalne.
- **Czy jest to pilne?** Czy problem jest prawdziwy i czy wymaga pilnej uwagi? Jeśli tak, należy natychmiast powiadomić członków zespołu.
- **Czy klienci mają te zmiany?** Czy przyczyną problemu mogą być użytkownicy usługi lub aplikacji?
- **Czy są to inne zależne systemy?** Czy istnieją alerty z zależności, które są powiązane, i które mogą być skorelowane, aby uniknąć informowania innych zespołów pracujących nad tym samym problemem?

Zadawaj te pytania, gdy początkowo tworzysz konfigurację monitorowania. Testowanie i weryfikowanie założeń w środowisku nieprodukcyjnym, a następnie wdrażanie do produkcji. Konfiguracje monitorowania są uzyskiwane z znanych trybów niepowodzeń, wyników testów symulowanych błędów i doświadczeń od różnych członków zespołu.

Po wydaniu konfiguracji monitorowania możesz uzyskać informacje na temat pracy i tego, co się nie dzieje. Należy wziąć pod uwagę wysoki poziom alertów, problemy niezauważalne przez monitorowanie, ale zauważalne przez użytkowników końcowych i jakie były najlepsze działania w ramach tej oceny. Zidentyfikuj zmiany do wdrożenia w celu usprawnienia dostarczania usługi w ramach trwającego, ciągłego procesu ulepszania monitorowania. Nie tylko oceniasz zakłócenia alertów lub pominięte alerty, ale również efektywność monitorowania obciążenia. Jest to informacje o wydajności zasad alertów, procesu i ogólnej kulturze, aby określić, czy są one ulepszane.

Zarówno System Center Operations Manager, jak i Azure Monitor obsługują alerty w oparciu o statyczne lub nawet dynamiczne wartości progowe i akcje skonfigurowane na ich podstawie. Przykładami mogą być alerty dla wiadomości e-mail, wiadomości SMS i połączeń głosowych w przypadku prostych powiadomień. Obie te usługi obsługują również integrację zarządzanie usługami IT (narzędzia ITSM), w celu zautomatyzowania tworzenia rekordów zdarzeń i eskalacji do właściwego zespołu pomocy technicznej lub dowolnego innego systemu zarządzania alertami, który używa elementu webhook.

Jeśli to możliwe, można użyć dowolnej z kilku usług w celu zautomatyzowania akcji odzyskiwania. Obejmują one program System Center Orchestrator, Azure Automation, Azure Logic Apps lub Skalowanie automatyczne w przypadku obciążeń elastycznych. Podczas powiadamiania zespołów odpowiedzialnych jest najbardziej powszechną akcją dotyczącą alertów, jednak Automatyzacja działań naprawczych może być również odpowiednia. Ta Automatyzacja może pomóc usprawnić cały proces zarządzania zdarzeniami. Automatyzacja tych zadań odzyskiwania może również zmniejszyć ryzyko wystąpienia błędu ludzkiego.

## <a name="azure-monitor-alerting"></a>Alerty Azure Monitor

Jeśli używasz wyłącznie Azure Monitor, postępuj zgodnie z poniższymi wskazówkami, aby wziąć pod uwagę szybkość, koszt i ilość miejsca do magazynowania.

W zależności od używanej funkcji i konfiguracji można przechowywać dane monitorowania w jednym z sześciu repozytoriów:

- **Baza danych metryk Azure Monitor:** Baza danych szeregów czasowych używana głównie do metryk Azure Monitor platformy, ale również ma Application Insights dane metryk są dublowane. Informacje wprowadzane do tej bazy danych mają najszybszy czas alertów.

- **Magazyn dzienników Application Insights:** Baza danych przechowująca większość Application Insights telemetrii w formularzu dziennika.

- **Magazyn dzienników Azure Monitor:** Magazyn podstawowy dla danych dziennika platformy Azure. Inne narzędzia umożliwiają kierowanie danych do nich i można je analizować w dziennikach Azure Monitor. Z powodu pozyskiwania i indeksowania zapytania alertów dziennika mają większe opóźnienia. To opóźnienie jest zwykle 5-10 minut, ale może być większe w pewnych okolicznościach.

- **Magazyn dziennika aktywności:** Używany dla wszystkich zdarzeń dziennika aktywności i kondycji usługi. Możliwe jest wygenerowanie alertów. Przechowuje zdarzenia poziomu subskrypcji występujące na obiektach w subskrypcji, jak widać poza tymi obiektami. Przykładem może być konfiguracja zasad lub dostęp do zasobu lub jego usunięcie.

- **Usługa Azure Storage:** Magazyn ogólnego przeznaczenia, który jest obsługiwany przez Diagnostyka Azure i inne narzędzia do monitorowania. Jest to niska cena opcji długoterminowego przechowywania danych telemetrycznych monitorowania. Alerty nie są obsługiwane na podstawie danych przechowywanych w tej usłudze.

- **Event Hubs:** Zwykle używany do przesyłania strumieniowego danych do narzędzi monitorowania lub narzędzia ITSM w innych partnerach.

Azure Monitor ma cztery typy alertów, a każdy z nich jest związany z repozytorium, w którym są przechowywane dane:

- [Alert dotyczący metryki](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric): alerty dotyczące danych w bazie danych metryk Azure monitor. Alerty występują, gdy monitorowana wartość przekroczy próg zdefiniowany przez użytkownika, a następnie ponownie, gdy powróci do stanu "normalny".

- [Alert dotyczący zapytania dziennika](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query): dostępne dla alertów dotyczących zawartości w magazynach Application Insights lub dzienników platformy Azure. Może również generować alerty oparte na zapytaniach między obszarami roboczymi.

- [Alert dziennika aktywności](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log): alerty dotyczące elementów w magazynie dziennika aktywności, z wyjątkiem danych Service Health.

- [Alert Service Health](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json): specjalny typ alertu — tylko w przypadku problemów Service Health pochodzących z magazynu dzienników aktywności.

### <a name="enable-alerting-through-partner-tools"></a>Włączanie alertów za poorednictwem narzędzi partnerskich

Jeśli używasz rozwiązania do tworzenia alertów zewnętrznych, Roześlij ją tak samo jak w przypadku usługi Azure Event Hubs, która jest najszybszą ścieżką do Azure Monitor. Musisz zanieść opłaty za pozyskiwanie w centrum zdarzeń. Jeśli koszt jest problemem i szybkość nie jest możliwa, można użyć usługi Azure Storage jako tańszej alternatywy. Wystarczy upewnić się, że narzędzia do monitorowania i narzędzia ITSM mogą odczytywać dane z usługi Azure Storage w celu wyodrębnienia danych.

Azure Monitor obejmuje obsługę integracji z innymi platformami monitorowania i oprogramowaniem narzędzia ITSM, takim jak usługi ServiceNow. Możesz korzystać z alertów platformy Azure i nadal wyzwalać akcje poza platformą Azure zgodnie z wymaganiami procesu zarządzania zdarzeniami lub DevOps. Jeśli chcesz otrzymywać alerty w Azure Monitor i zautomatyzować odpowiedź, możesz inicjować automatyczne akcje przy użyciu Azure Functions, Azure Logic Apps lub Azure Automation na podstawie Twojego scenariusza i wymagań.

### <a name="specialized-azure-monitoring-offerings"></a>Wyspecjalizowane oferty monitorowania platformy Azure

[Rozwiązania do zarządzania](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) zwykle przechowują swoje dane w magazynie dzienników platformy Azure. Dwa wyjątki są Azure Monitor dla maszyn wirtualnych i Azure Monitor dla kontenerów. W poniższej tabeli opisano środowisko alertów w oparciu o określony typ danych i miejsce, w którym są przechowywane.

Rozwiązanie| Typ danych | Zachowanie alertu
:---|:---|:---
Usługa Azure Monitor dla kontenerów | Obliczone średnie dane wydajności z węzłów i zasobników są zapisywane w magazynie metryk. | Tworzenie alertów dotyczących metryk, jeśli chcesz otrzymywać alerty w oparciu o wahania wydajności zmierzonego wykorzystania, zagregowane w czasie.
|| Obliczone dane wydajności używające percentylów z węzłów, kontrolerów, kontenerów i zasobników są zapisywane w magazynie dzienników. Dzienniki kontenerów i informacje o spisie są również zapisywane w magazynie dzienników. | Utwórz alerty kwerendy dziennika, jeśli chcesz otrzymywać alerty na podstawie zmienności mierzonego użycia z klastrów i kontenerów. Alerty zapytań dzienników można również skonfigurować na podstawie liczby faz i liczby węzłów stanu.
Usługa Azure Monitor dla maszyn wirtualnych | Kryteria kondycji są metrykami zapisanymi w magazynie metryk. | Alerty są generowane, gdy kondycja ulegnie zmianie z kondycji na złej kondycji. Ten alert obsługuje tylko grupy akcji, które są skonfigurowane do wysyłania wiadomości SMS lub powiadomień e-mail.
|| Dane dziennika wydajności mapy i systemu operacyjnego gościa są zapisywane w magazynie dzienników. | Utwórz alerty zapytania dziennika.

### <a name="fastest-speed-driven-by-cost"></a>Najszybsza szybkość według kosztu

Opóźnienie to jedna z najważniejszych decyzji, które obejmują alerty i szybkie rozwiązywanie problemów wpływających na usługę. Jeśli potrzebujesz alertów niemal w czasie rzeczywistym w ciągu pięciu minut, Oceń pierwsze, jeśli masz lub można otrzymywać alerty dotyczące danych telemetrycznych, w których są one domyślnie przechowywane. Ogólnie rzecz biorąc, ta strategia jest również najtańszą opcją, ponieważ używane narzędzie już wysyła swoje dane do tej lokalizacji.

Tym samym, istnieje kilka ważnych przypisów dla tej reguły.

**Telemetrię systemu operacyjnego gościa** ma wiele ścieżek do pobrania w systemie.

- Najszybszy sposób na wysłanie alertów dotyczących tych danych polega na zaimportowaniu ich jako metryki niestandardowych. W tym celu należy użyć rozszerzenia Diagnostyka Azure, a następnie przy użyciu alertu dotyczącego metryki. Jednak metryki niestandardowe są obecnie dostępne w wersji zapoznawczej i są [droższe niż inne opcje](https://azure.microsoft.com/pricing/details/monitor).

- Najtańsza, ale najwolniejsza Metoda polega na wysłaniu jej do magazynu Kusto dzienników platformy Azure. Uruchomienie agenta Log Analytics na maszynie wirtualnej jest najlepszym sposobem na uzyskanie wszystkich metryk systemu operacyjnego gościa i danych dzienników do tego magazynu.

- Można wysłać je do obu magazynów, uruchamiając zarówno rozszerzenie, jak i agenta na tej samej maszynie wirtualnej. Następnie można szybko wysyłać alerty, ale również używać danych systemu operacyjnego gościa w ramach bardziej złożonych wyszukiwań podczas łączenia ich z inną telemetrią.

**Importowanie danych z lokalizacji lokalnej:** Jeśli próbujesz wysyłać zapytania i monitorować między maszynami działającymi na platformie Azure i lokalnymi, możesz użyć agenta Log Analytics, aby zbierać dane systemu operacyjnego gościa. Następnie można użyć funkcji o nazwie [Logs do metryk](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) , aby usprawnić metryki w magazynie metryk. Ta metoda pomija część procesu pozyskiwania w magazynie dzienników platformy Azure, a dane są dostępne wcześniej w bazie danych metryk.

### <a name="minimize-alerts"></a>Minimalizuj alerty

W przypadku korzystania z rozwiązania takiego jak Azure Monitor dla maszyn wirtualnych i znajdowania domyślnych kryteriów kondycji, które monitorują akceptowalne użycie wydajności, nie twórz nakładających się metryk ani alertów zapytań dzienników opartych na tych samych licznikach wydajności.

Jeśli nie używasz Azure Monitor dla maszyn wirtualnych, Utwórz zadanie tworzenia alertów i zarządzania powiadomieniami, korzystając z następujących funkcji:

> [!NOTE]
> Te funkcje mają zastosowanie tylko do alertów metryk i alertów opartych na danych wysyłanych do bazy danych metryk Azure Monitor. Funkcje nie mają zastosowania do innych typów alertów. Jak wspomniano wcześniej, głównym celem alertów dotyczących metryk jest szybkość. W przypadku otrzymania alertu w ciągu mniej niż pięciu minut nie ma podstawowego znaczenia, zamiast tego można użyć alertu zapytania dziennika.

- [Progi dynamiczne](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds): progi dynamiczne sprawdzają aktywność zasobu w danym okresie i tworzą górne i dolne progi "normalne zachowanie". Gdy monitorowana Metryka wykracza poza te progi, zostanie wyświetlony alert.

- [Alerty](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts)wielocyfrowe: można utworzyć alert dotyczący metryki, który używa kombinacji dwóch różnych danych wejściowych z dwóch różnych typów zasobów. Jeśli na przykład chcesz uruchomić alert, gdy użycie procesora CPU przez maszynę wirtualną przekracza 90 procent, a liczba komunikatów w określonej Azure Service Bus kolejce obsłużyć przez tę maszynę wirtualną, można to zrobić bez tworzenia zapytania dziennika. Ta funkcja działa tylko dla dwóch sygnałów. W przypadku bardziej złożonej kwerendy podawanie danych metryki do magazynu dzienników Azure Monitor i użycie zapytania dziennika.

- [Alerty wielozasobów](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts): Azure monitor zezwala na regułę alertu o pojedynczej metryce, która ma zastosowanie do wszystkich zasobów maszyny wirtualnej. Ta funkcja może zaoszczędzić czas, ponieważ nie trzeba tworzyć poszczególnych alertów dla każdej maszyny wirtualnej. Cennik tego typu alertu jest taki sam. Bez względu na to, czy tworzysz 50 alertów na potrzeby monitorowania użycia procesora CPU w przypadku maszyn wirtualnych 50 lub jeden alert monitorujący wykorzystanie procesora dla wszystkich maszyn wirtualnych 50, koszt ten jest taki sam. Te typy alertów można również używać w połączeniu z progami dynamicznymi.

Te funkcje umożliwiają zaoszczędzenie czasu przez zminimalizowanie powiadomień o alertach i zarządzanie alertami.

### <a name="alerts-limitations"></a>Ograniczenia alertów

Pamiętaj, aby zanotować [ograniczenia](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) dotyczące liczby alertów, które można utworzyć. Niektóre ograniczenia (ale nie wszystkie z nich) można zwiększyć, wywołując pomoc techniczną.

### <a name="best-query-experience"></a>Najlepsze środowisko zapytań

Jeśli szukasz trendów we wszystkich danych, warto zaimportować wszystkie dane do dzienników platformy Azure, chyba że są one już w Application Insights. Można tworzyć zapytania w obu obszarach roboczych, dlatego nie ma potrzeby przenoszenia danych między nimi. Możesz również zaimportować dziennik aktywności i Service Health dane do obszaru roboczego Log Analytics. Płacisz za ten pozyskiwanie i przechowywanie, ale uzyskasz wszystkie dane w jednym miejscu na potrzeby analizy i wykonywania zapytań. Takie podejście daje również możliwość tworzenia złożonych warunków zapytania i alertów.
