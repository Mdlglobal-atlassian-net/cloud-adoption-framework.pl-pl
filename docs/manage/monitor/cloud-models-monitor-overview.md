---
title: Przewodnik monitorowania w chmurze — strategia monitorowania dla modeli wdrożenia w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Określ, kiedy używać Azure Monitor lub System Center Operations Manager w Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 10/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 5988cbb16e47a603af85eac97078b7dc0a00e295
ms.sourcegitcommit: d37c4443e9acaa381ea74ee3fc50e3b99f13f22a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2019
ms.locfileid: "72001888"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Przewodnik monitorowania chmury: Strategia monitorowania dla modeli wdrożenia w chmurze

Ten artykuł zawiera naszą zalecaną strategię monitorowania dla każdego z modeli wdrożenia w chmurze, w oparciu o następujące kryteria:

- Musisz zachować zaangażowanie do Operations Manager lub innej platformy monitorowania przedsiębiorstwa z powodu integracji z procesami operacji IT, wiedzą i wiedzą lub pewnych funkcji, które nie są jeszcze dostępne w Azure Monitor.
- Musisz monitorować obciążenia zarówno lokalnie, jak i w chmurze publicznej lub tylko w chmurze.
- Twoja strategia migracji do chmury obejmuje modernizację operacji IT i przejście do naszych rozwiązań i usług monitorowania w chmurze.
- Być może masz krytyczne systemy, które są gapped powietrze lub fizycznie izolowane, hostowane w chmurze prywatnej lub na sprzęcie fizycznym i muszą być monitorowane.

Nasza strategia obejmuje obsługę infrastruktury monitorowania (obciążeń obliczeniowych, magazynowania i serwera), aplikacji (użytkowników końcowych, wyjątków i klienta) oraz zasobów sieciowych w celu zapewnienia kompletnej, zorientowanej na usługę perspektywy monitorowania.

## <a name="azure-cloud-monitoring"></a>Monitorowanie w chmurze platformy Azure

Azure Monitor to usługa platformy Azure Native platform, która zapewnia jedno źródło monitorowania zasobów platformy Azure. Jest ona przeznaczona dla rozwiązań w chmurze, które są oparte na platformie Azure, i obsługują możliwość biznesową opartą na obciążeniach maszyn wirtualnych lub złożonych architekturach, które korzystają z mikrousług i innych zasobów platformy. Monitoruje wszystkie warstwy stosu, rozpoczynając od usług dzierżawców, takich jak Azure Active Directory Domain Services, oraz zdarzeń na poziomie subskrypcji i usługi Azure Service Health. Służy również do monitorowania zasobów infrastruktury, takich jak maszyny wirtualne, magazyn i zasoby sieciowe, i w górnej warstwie aplikacji. Monitorowanie każdej z tych zależności i zbieranie właściwych sygnałów, które mogą emitować każdy z nich, zapewnia wgląd w aplikacje i potrzebną infrastrukturę kluczy.

Poniższa tabela zawiera podsumowanie zalecanego podejścia do monitorowania każdej warstwy stosu.

<!-- markdownlint-disable MD033 -->

Warstwa | Resource | Scope | Metoda
---|---|---|----
Aplikacja | Aplikacja oparta na sieci Web działająca na platformie .NET, .NET Core, Java, JavaScript i Node. js na maszynie wirtualnej platformy Azure, na platformie Azure App Services, na platformie Azure Service Fabric, w Azure Functions i na platformie Azure Cloud Services | Monitoruj działającą aplikację sieci Web, aby automatycznie wykrywać anomalie wydajności, identyfikować wyjątki i problemy z kodem oraz zbierać analizy zachowania użytkowników. |  Azure Monitor (Application Insights)
Zasoby platformy Azure — PaaS | 1. Usługi Azure Database Services (na przykład SQL lub mySQL) | 1. Metryki wydajności usługi Azure Database for SQL. | 1. Włącz rejestrowanie diagnostyczne w celu przesyłania strumieniowego danych SQL do dzienników Azure Monitor.
Zasoby platformy Azure — IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Grupy zabezpieczeń sieci<br/> 4. Azure Traffic Manager<br/> 5. Maszyna wirtualna<br/> 6. Usługa Azure Kubernetes/Azure Container Instances | 1. Pojemność, dostępność i wydajność.<br/> 2. Dzienniki wydajności i diagnostyki (aktywność, dostęp, wydajność i Zapora).<br/> 3. Monitoruj zdarzenia, gdy reguły są stosowane, oraz licznik reguł dla tego, ile razy reguła została zastosowana do odmowy lub zezwolenia.<br/> 4. Monitoruj dostępność stanu punktu końcowego.<br/> 5. Monitoruj wydajność, dostępność i wydajność w systemie operacyjnym gościa maszyny wirtualnej. Mapowanie zależności aplikacji hostowanych na poszczególnych maszynach wirtualnych, w tym widoczność aktywnych połączeń sieciowych między serwerami, opóźnieniem połączenia przychodzącego i wychodzącego oraz portów w dowolnej architekturze połączonej z protokołem TCP.<br/> 6. Monitoruj wydajność, dostępność i wydajność obciążeń działających w kontenerach i wystąpieniach kontenerów. | 1. Metryki magazynu dla usługi BLOB Storage.<br/> 2. Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 3. Włącz rejestrowanie diagnostyczne grup zabezpieczeń sieci i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 4. Włącz rejestrowanie diagnostyczne dla punktów końcowych Traffic Manager i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 5. Włącz usługę Azure Monitor dla maszyn wirtualnych<br/> 6. Włącz Azure Monitor dla kontenerów
Sieć| Komunikacja między maszyną wirtualną i jednym lub wieloma punktami końcowymi (inna maszyna wirtualna, w pełni kwalifikowana nazwa domeny, jednolity identyfikator zasobu lub adres IPv4). | Monitoruj zmiany, opóźnienia i topologię sieci między maszyną wirtualną a punktem końcowym. | Azure Network Watcher
Subskrypcja platformy Azure | Kondycja usługi platformy Azure i podstawowa Kondycja zasobów | <li> Akcje administracyjne wykonywane w ramach usługi lub zasobu.<br/><li> Kondycja usługi w ramach usługi platformy Azure jest w stanie obniżonej lub niedostępności.<br/><li> Wykryto problemy z kondycją w ramach zasobu platformy Azure z perspektywy usługi platformy Azure.<br/><li> Operacje wykonywane przy użyciu automatycznego skalowania platformy Azure wskazujące awarię lub wyjątek. <br/><li> Operacje wykonywane z Azure Policy wskazujące, że wystąpiła dozwolona lub odmowa akcja.<br/><li> Rekord alertów generowanych przez Azure Security Center. |Dostarczana w dzienniku aktywności do monitorowania i wysyłania alertów za pomocą Azure Resource Manager.
Dzierżawa platformy Azure|Usługa Azure Active Directory || Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorowanie chmury hybrydowej

W przypadku wielu organizacji chmura musi być stopniowo zbliżana, gdzie model chmury hybrydowej jest najbardziej typowym krokiem w podróży. Starannie wybierasz odpowiedni podzbiór aplikacji i infrastrukturę, aby rozpocząć migrację, unikając przerw w działaniu firmy. Jednak firma Microsoft oferuje dwie platformy monitorujące, które obsługują ten model chmury, a decyzje IT są mylone z tym, które z nich najlepiej nadają się do wspierania ich działalności biznesowej i celów operacyjnych IT. Będziemy przeglądać kilka czynników, aby sprostać niepewności i zapewnić zrozumienie platformy, którą należy wziąć pod uwagę.

Oto niektóre z kluczowych aspektów technicznych, które należy wziąć pod uwagę:

* Należy zebrać dane z zasobów platformy Azure, które obsługują obciążenie, i przesłać je do istniejących narzędzi lokalnych lub zarządzanych dostawcy usług.

* Musisz zachować aktualną inwestycję w System Center Operations Manager i skonfigurować ją do monitorowania zasobów IaaS i PaaS działających na platformie Azure. Opcjonalnie ze względu na to, że monitorowane są dwa środowiska o różnej charakterystyce, w zależności od wymagań należy określić integrację z Azure Monitorą.

* W ramach strategii modernizacji do standaryzacji jednego narzędzia, aby zmniejszyć koszty i złożoność, należy zatwierdzić Azure Monitor monitorowania zasobów na platformie Azure i w sieci firmowej.

Poniższa tabela zawiera podsumowanie wymagań Azure Monitor i System Center Operations Manager obsługi monitorowania modelu chmury hybrydowej na podstawie wspólnego zestawu kryteriów.

|Wymaganie | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Wymagania dotyczące infrastruktury | **Nie** | **Tak**<br> Wymaga co najmniej serwera zarządzania programu oraz serwera SQL do obsługi operacyjnej bazy danych i bazy danych magazyn danych raportowania. Jest bardziej skomplikowany, gdy wymagane jest HA/DR, maszyny w wielu lokacjach, niezaufane systemy i inne zagadnienia dotyczące projektowania.|
|Łączność ograniczona — brak Internetu<br> lub sieć izolowana | **Nie** | **Tak** | 
|Ograniczony dostęp do Internetu kontrolowany przez łączność | **Tak** | **Tak** |
|Ograniczone połączenia — często rozłączone | **Tak** | **Tak** |
|Konfigurowalne monitorowanie kondycji | **Nie** | **Tak** |
| Test dostępności aplikacji sieci Web (izolowana sieć) | **Tak, ograniczone**<br> Azure Monitor ma ograniczoną obsługę w tym obszarze i wymaga niestandardowych wyjątków zapory. | **Tak** | 
| Test dostępności aplikacji sieci Web (dystrybuowany globalnie) | **Nie** | **Tak** |
|Monitorowanie obciążeń maszyn wirtualnych | **Tak, ograniczone**<br> Może zbierać usługi IIS oraz SQL Server dzienników błędów, zdarzeń systemu Windows i liczników wydajności. Wymaga utworzenia niestandardowych zapytań, alertów i wizualizacji. | **Tak**<br> Obsługuje monitorowanie większości obciążeń serwera z dostępnymi pakietami administracyjnymi. Na maszynie wirtualnej jest wymagany agent Log Analytics lub Agent Operations Manager, który umożliwia raportowanie z powrotem do grupy zarządzania w sieci firmowej.|
|Monitorowanie usługi Azure IaaS | **Tak** | **Tak**<br> Obsługuje monitorowanie większości infrastruktury z sieci firmowej. Śledzi stan dostępności, metryki i alerty dla maszyn wirtualnych platformy Azure, bazy danych SQL i magazynu za pośrednictwem pakietu administracyjnego platformy Azure.|
|Monitorowanie usługi Azure PaaS | **Tak** | **Tak, ograniczone**<br> Na podstawie tego, co jest obsługiwane w pakiecie administracyjnym platformy Azure. | 
|Monitorowanie usług platformy Azure | **Tak**<br> | **Tak**<br> Chociaż nie ma natywnego monitorowania kondycji usługi platformy Azure w ramach pakietu administracyjnego, można utworzyć niestandardowe przepływy pracy, aby wysyłać zapytania dotyczące usługi Azure Service Health. Użyj interfejsu API REST platformy Azure, aby otrzymywać alerty za pomocą istniejących powiadomień.|
|Nowoczesne monitorowanie aplikacji sieci Web | **Tak** | **Nie** |
|Starsze monitorowanie aplikacji sieci Web | **Tak, ograniczone jest zależne od zestawu SDK**<br> Obsługuje monitorowanie starszych wersji aplikacji sieci Web platformy .NET i języka Java. | **Tak, ograniczone** |
|Monitorowanie kontenerów usługi Azure Kubernetes Service | **Tak** | **Nie** |
|Monitorowanie kontenerów platformy Docker/Windows | **Tak** | **Nie** | 
|Monitorowanie wydajności sieci | **Tak** | **Tak, ograniczone**<br> Program obsługuje sprawdzanie dostępności i zbiera podstawowe dane statystyczne z urządzeń sieciowych przy użyciu protokołu SNMP z sieci firmowej.|
|Interaktywna analiza danych | **Tak** | **Nie**<br> Opiera się na SQL Server Reporting Services wstępnie dostępnych lub niestandardowych raportach, rozwiązaniach wizualizacji innych firm lub niestandardowej implementacji Power BI. Istnieją ograniczenia dotyczące skalowania i wydajności w magazynie danych Operations Manager. Integracja z usługą Azure Monitor Logs jako alternatywa dla wymagań agregacji danych. Integrację uzyskuje się przez skonfigurowanie łącznika Log Analytics.| 
|Kompleksowa diagnostyka, analiza głównych przyczyn i rozwiązywanie problemów | **Tak** | **Tak, ograniczone**<br> Obsługuje kompleksową diagnostykę i rozwiązywanie problemów tylko w przypadku lokalnej infrastruktury i aplikacji. Program używa innych składników programu System Center lub rozwiązań partnerskich.|
|Interaktywne wizualizacje (pulpity nawigacyjne) | **Tak** | **Tak, ograniczone**<br> Zapewnia podstawowe pulpity nawigacyjne z konsolą sieci Web HTLM5 lub zaawansowane środowisko z rozwiązań partnerskich, takich jak kwadratowe i Savision. |
|Integracja z narzędziami IT/DevOps | **Tak** | **Tak, ograniczone** |

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Zbieranie i przesyłanie strumieniowe danych monitorowania do narzędzi innych firm lub lokalnych

Aby zbierać metryki i dzienniki z zasobów platformy i infrastruktury platformy Azure, należy włączyć dzienniki diagnostyczne platformy Azure dla tych zasobów. Ponadto dzięki maszynom wirtualnym platformy Azure można zbierać metryki i dzienniki z systemu operacyjnego gościa, włączając rozszerzenie Diagnostyka Azure. Aby przekazać dane diagnostyczne emitowane z zasobów platformy Azure do narzędzi lokalnych lub dostawcy usług zarządzanych, skonfiguruj [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) do przesyłania strumieniowego danych. 

### <a name="monitor-with-system-center-operations-manager"></a>Monitoruj przy użyciu System Center Operations Manager

Mimo że System Center Operations Manager pierwotnie zaprojektowano jako rozwiązanie lokalne do monitorowania między aplikacjami, obciążeniami i infrastrukturą w środowisku IT, rozbudowano w taki sposób, aby obejmowała możliwości monitorowania chmury i integruje się z usługą Azure, Office 365 i Amazon Web Services (AWS). Jest w stanie monitorować te różnorodne środowiska z pakietami administracyjnymi zaprojektowanymi i zaktualizowanymi w celu ich obsługi.  

W przypadku klientów, którzy zastosowali znaczące inwestycje w Operations Manager, aby osiągnąć kompleksowe monitorowanie, które ściśle integruje się z ich procesami i narzędziami zarządzanie usługami IT, lub klienci nowym na platformie Azure, rozumie się pytanie:

* Może Operations Manager dalej dostarczać wartość i czy ma ona sens biznesową?

* Jeśli funkcje w Operations Manager są odpowiednie dla naszej organizacji IT?

* Czy integracja Operations Manager z Azure Monitor oferuje ekonomiczne i kompleksowe rozwiązanie do monitorowania? 

Jeśli zainwestowano już w Operations Manager, nie ma potrzeby skoncentrowania się na planowaniu migracji w celu ich natychmiastowego zastępowania. Dzięki platformie Azure lub innym dostawcom chmury istniejącym jako rozszerzenie Twojej sieci lokalnej, Operations Manager może monitorować maszyny wirtualne gościa i zasoby platformy Azure, tak jakby znajdowały się w sieci firmowej. Wymaga to niezawodnego połączenia sieciowego między siecią i siecią wirtualną platformy Azure, która ma wystarczającą przepustowość. 

Aby monitorować obciążenia działające na platformie Azure, potrzebne są:

* [Pakiet administracyjny platformy Azure](https://www.microsoft.com/download/details.aspx?id=50013) do zbierania metryk wydajności emitowanych przez usługi platformy Azure, takie jak role sieci Web i procesu roboczego, Application Insights testy dostępności (webtests), Service Bus itd. Pakiet administracyjny używa interfejsu API REST platformy Azure do monitorowania dostępności i wydajności tych zasobów. Niektóre typy usług platformy Azure nie mają żadnych metryk ani żadnych wstępnie zdefiniowanych monitorów w pakiecie administracyjnym, ale nadal mogą być monitorowane przez relacje zdefiniowane w pakiecie administracyjnym platformy Azure dla odnalezionych usług.

* [Pakiet administracyjny Azure SQL Database](https://www.microsoft.com/download/details.aspx?id=38829) do monitorowania dostępności i wydajności baz danych SQL Azure i serwerów usługi Azure SQL Database przy użyciu interfejsu API REST platformy Azure i zapytań T-SQL do SQL Server widoków systemowych.

* Aby monitorować system operacyjny gościa i obciążenia uruchomione na maszynie wirtualnej, takie jak SQL Server, IIS lub Apache Tomcat, należy pobrać i zaimportować pakiet administracyjny obsługujący aplikację, usługę i system operacyjny.

W pakiecie administracyjnym jest zdefiniowana wiedza opisująca sposób monitorowania poszczególnych zależności i składników. Oba pakiety administracyjne platformy Azure wymagają wykonania zestawu kroków konfiguracyjnych na platformie Azure i Operations Manager w celu rozpoczęcia monitorowania tych zasobów. 

W warstwie aplikacji Operations Manager oferuje podstawowe możliwości monitorowania wydajności aplikacji dla niektórych starszych wersji platformy .NET i języka Java. Jeśli niektóre aplikacje w środowisku chmury hybrydowej działają w trybie offline lub izolowanym siecią, w taki sposób, że nie mogą komunikować się z usługą w chmurze publicznej, Operations Manager Program Application Performance Monitoring (APM) może być opcją realną dla Niektóre ograniczone scenariusze. W przypadku aplikacji nieuruchomionych na starszych platformach hostowanych zarówno lokalnie, jak i w chmurze publicznej, która umożliwia komunikację za pośrednictwem zapory (bezpośrednie lub za pośrednictwem serwera proxy) na platformie Azure, użyj Azure Monitor Application Insights. Zapewnia to głębokie monitorowanie na poziomie kodu z użyciem pierwszej klasy do obsługi ASP.NET, ASP.NET Core, Java, JavaScript i Node. js.

W przypadku dowolnej aplikacji sieci Web, która może zostać osiągnięta zewnętrznie, należy włączyć typ transakcji syntetycznych znanych jako [monitorowanie dostępności]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability). Ważne jest, aby dowiedzieć się, czy aplikacja lub krytyczny punkt końcowy HTTP/HTTPS, na którym bazuje aplikacja, jest dostępny i odpowiada. Application Insights monitorowanie dostępności umożliwia uruchamianie testów z wielu centrów danych platformy Azure i zapewnia wgląd w kondycję aplikacji z perspektywy globalnej.

Chociaż Operations Manager jest w stanie monitorować zasoby hostowane na platformie Azure, istnieje kilka korzyści, które uwzględniają Azure Monitor, ponieważ ich mocne ograniczenia w Operations Manager i ustanawiają silną podstawę do obsługi migracji ostatecznej z tego programu. W tym miejscu analizujemy każdą z naszych rekomendacji, aby uwzględnić Azure Monitor w strategii monitorowania hybrydowego.  

#### <a name="disadvantage-of-using-operations-manager-by-itself"></a>Wadą używania Operations Manager przez siebie

1. Analizowanie danych monitorowania w Operations Manager jest zwykle wykonywane przy użyciu wstępnie zdefiniowanych widoków zdefiniowanych w pakietach administracyjnych, które są dostępne z konsoli programu, z raportów SQL Server Reporting Services (SSRS) lub widoków niestandardowych utworzonych przez użytkownika końcowego. Wykonywanie analizy ad hoc danych nie jest możliwe z pola. Raportowanie Operations Manager jest nieelastyczne, magazyn danych, który umożliwia długoterminowe przechowywanie danych monitorowania nie jest skalowane ani nie działa, oraz wiedzą, jak pisać instrukcje języka T-SQL, opracowywanie rozwiązania Power BI lub rozwiązań innych firm wymagany do obsługi wymagań dotyczących różnych osób w organizacji IT. 

2. Generowanie alertów w Operations Manager nie zapewnia obsługi złożonych wyrażeń i obejmuje logikę korelacji w celu ułatwienia zmniejszenia poziomu szumów alertów i grup alertów w celu pokazywania relacji między nimi w celu ułatwienia identyfikacji głównej przyczyny wykonaj. 

#### <a name="advantage-of-operations-manager--azure-monitor"></a>Zalety Operations Manager i Azure Monitor

1. Dzienniki Azure Monitor to rozwiązanie, które umożliwia obejście ograniczeń Operations Manager i ponosi Operations Manager baza danych magazynu danych w celu zbierania ważnych danych dotyczących wydajności i dzienników. Azure Monitor zapewnia lepszą analizę, wydajność podczas wykonywania zapytań dotyczących dużych ilości danych i przechowywania niż Operations Manager magazynu danych. Język zapytań umożliwia tworzenie znacznie bardziej złożonych i zaawansowanych zapytań, dzięki czemu można uruchamiać zapytania dotyczące terabajtów danych w ciągu kilku sekund. Możesz szybko przekształcić dane na wykresy kołowe, wykresy czasowe i wiele innych wizualizacji. Nie są już ograniczone przez pracę z raportami w Operations Manager na podstawie SQL Server Reporting Services, niestandardowych zapytań SQL lub innych obejść, aby przeanalizować te dane.

2. Zapewnij udoskonalone środowisko obsługi alertów, implementując rozwiązanie do zarządzania alertami Azure Monitor. Alerty wygenerowane w grupie zarządzania Operations Manager można przesłać dalej do obszaru roboczego usługi Logs Azure Monitor dzienników. Można skonfigurować subskrypcję odpowiedzialną za przekazywanie alertów z usługi Operations Manager do dzienników Azure Monitor, aby przekazywać tylko niektóre alerty. Na przykład można przesłać dalej tylko alerty, które spełniają kryteria do wykonywania zapytań w zakresie zarządzania problemami, a także badanie głównej przyczyny awarii lub problemów za pomocą jednego z okien szklanych. Ponadto możesz skorelować inne dane dziennika z Application Insights lub innych źródeł, aby uzyskać szczegółowe informacje, które pomagają ulepszyć środowisko użytkownika, zwiększyć czas przestoju i skrócić czas rozwiązywania problemów.

3. Monitoruj natywną infrastrukturę i aplikacje w chmurze, korzystając z prostej lub wielowarstwowej architektury na platformie Azure i korzystaj z Operations Manager do monitorowania infrastruktury lokalnej. Obejmuje to co najmniej jedną maszynę wirtualną, wiele maszyn wirtualnych umieszczonych w zestawie dostępności lub zestaw skalowania maszyn wirtualnych lub aplikację kontenerową wdrożoną w usłudze Azure Kubernetes Service (AKS) działającą w kontenerach systemu Windows Server lub Linux.

4. Użyj rozwiązania System Center Operations Manager Health Check, aby proaktywnie ocenić ryzyko i kondycję grupy zarządzania System Center Operations Manager w regularnych odstępach czasu. Może to zamienić lub nawiązać wszelkie niestandardowe funkcje, które zostały dodane do grupy zarządzania.

5. Funkcja map Azure Monitor dla maszyn wirtualnych umożliwia monitorowanie standardowych metryk łączności z poziomu połączeń sieciowych między maszynami wirtualnymi platformy Azure i lokalnymi maszynami wirtualnymi. Te metryki obejmują czas odpowiedzi, żądania na minutę, przepływność ruchu i linki. Można zidentyfikować nieudane połączenia, rozwiązać problemy, przeprowadzić weryfikację migracji, przeprowadzić analizę zabezpieczeń i sprawdzić ogólną architekturę usługi. Usługa map może automatycznie odnajdywać składniki aplikacji w systemach Windows i Linux oraz mapować komunikację między usługami. Pomaga to identyfikować połączenia i zależności, z którymi było nieświadome, planowanie i weryfikowanie migracji do platformy Azure oraz minimalizowanie rozwiązań w trakcie rozwiązywania problemów.

6. Za pomocą Network Performance Monitor Monitoruj łączność sieciową między:

   - Sieci firmowej i platformy Azure.

   - Najważniejsze aplikacje wielowarstwowe i mikrousługi.

   - Lokalizacje użytkowników i aplikacje oparte na sieci Web (HTTP/HTTPs).

   Ta strategia zapewnia widoczność warstwy sieciowej bez potrzeby korzystania z protokołu SNMP. Może również znajdować się na interaktywnej mapie topologii, topologii przeskoków między punktem końcowym i docelowym. Lepszym rozwiązaniem jest próba wykonania tego samego wyniku przy użyciu monitorowania sieci w programie Operations Manager lub innych narzędzi do monitorowania sieci, które są obecnie używane w danym środowisku.

### <a name="monitor-with-azure-monitor"></a>Monitoruj przy użyciu usługi Azure Monitor

Podczas migracji do chmury są dostępne liczne wyzwania, a także wiele szans sprzedaży. Dzięki temu organizacja może przeprowadzić migrację z jednego lub wielu lokalnych narzędzi do monitorowania przedsiębiorstwa, aby nie tylko zredukować nakłady inwestycyjne i koszty operacyjne, ale również korzystać z zalet platformy monitorowania w chmurze, takiej jak Azure Monitor. w skali chmury. Sprawdź wymagania dotyczące monitorowania i zgłaszania alertów, konfigurację istniejących narzędzi do monitorowania, obciążeń przenoszonych do chmury i skonfiguruj Azure Monitor po sfinalizowaniu planu. 

- Monitoruj hybrydową infrastrukturę i aplikacje, korzystając z prostej lub wielowarstwowej architektury, w której składniki są hostowane między platformą Azure, innym dostawcą chmury i siecią firmową. Obejmuje to co najmniej jedną maszynę wirtualną, wiele maszyn wirtualnych umieszczonych w zestawie dostępności lub zestaw skalowania maszyn wirtualnych lub aplikację kontenerową wdrożoną w usłudze Azure Kubernetes Service (AKS) działającą w kontenerach systemu Windows Server lub Linux. 

- Włącz Azure Monitor dla maszyn wirtualnych, Azure Monitor dla kontenerów i Application Insights wykrywać i diagnozować problemy między infrastrukturą i aplikacjami. Aby uzyskać dokładniejszą analizę i korelację danych zbieranych z wielu składników lub zależności obsługujących aplikację, należy użyć dzienników Azure Monitor.

- Tworzenie inteligentnych alertów, które mogą być stosowane do podstawowego zestawu aplikacji i składników usług, zmniejszenie szumu alertów z progami dynamicznymi dla złożonych sygnałów oraz korzystanie z agregacji alertów w oparciu o algorytmy uczenia maszynowego w celu szybkiego identyfikowania wykonaj.

 - Zdefiniuj bibliotekę zapytań i pulpitów nawigacyjnych, aby obsługiwać wymagania dotyczące różnych osób w organizacji IT.

- Zdefiniuj standardy i metody umożliwiające monitorowanie zasobów hybrydowych i w chmurze, linię bazową monitorowania dla każdego zasobu, progi alertów itp.  

- Skonfiguruj kontrolę dostępu opartą na rolach (RBAC), aby przyznać użytkownikom i grupom tylko dostęp do danych monitorowania z zasobów, które są odpowiedzialne za zarządzanie. 

- Dołącz automatyzację i samoobsługowe, aby umożliwić każdemu zespołowi tworzenie, Włączanie i dostrajanie konfiguracji monitorowania i alertów w razie potrzeby. 

## <a name="private-cloud-monitoring"></a>Monitorowanie chmury prywatnej

Można osiągnąć całościowe monitorowanie Azure Stack z System Center Operations Manager. W celu monitorowania obciążeń uruchomionych w ramach dzierżawy, poziomu zasobów na maszynach wirtualnych oraz Azure Stack hostingu infrastruktury (serwery fizyczne i przełączniki sieciowe). Możesz również uzyskać całościowe monitorowanie z użyciem kombinacji [możliwości monitorowania infrastruktury](/azure/azure-stack/azure-stack-monitor-health) zawartej w Azure Stack. Te funkcje ułatwiają wyświetlanie kondycji i alertów dla regionu Azure Stack i [usługi Azure monitor](/azure/azure-stack/user/azure-stack-metrics-azure-data) w Azure Stack, która zapewnia metryki infrastruktury i dzienniki na poziomie podstawowym dla większości usług.

Jeśli zainwestowano już w Operations Manager, Użyj pakietu administracyjnego Azure Stack do monitorowania stanu dostępności i kondycji Azure Stack wdrożeń. Obejmuje to regiony, dostawcy zasobów, aktualizacje, przebiegi aktualizacji, jednostki skalowania, węzły jednostek, role infrastruktury i ich wystąpienia (jednostki logiczne składają się z zasobów sprzętowych). Używa ona interfejsów API REST i aktualizacji dostawcy zasobów, aby komunikować się z Azure Stack. Aby monitorować serwery fizyczne i urządzenia magazynujące, należy użyć pakietu administracyjnego dostawcy OEM (na przykład dostarczonego przez firmę Lenovo, Hewlett Packard lub Dell). Operations Manager może natywnie monitorować przełączniki sieciowe w celu zbierania podstawowych statystyk przy użyciu protokołu SNMP. Monitorowanie obciążeń dzierżawców jest możliwe z pakietem administracyjnym platformy Azure, wykonując dwa podstawowe kroki. Skonfiguruj subskrypcję, którą chcesz monitorować, a następnie Dodaj monitory dla tej subskrypcji.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Zbieranie właściwych danych](./data-collection.md)
