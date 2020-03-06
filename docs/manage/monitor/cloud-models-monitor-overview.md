---
title: Strategia monitorowania dla modeli wdrożenia w chmurze
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, którą strategię monitorowania zarządzania chmurą zastosować.
author: MGoedtel
ms.author: magoedte
ms.date: 10/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3b6434937816255269bda41c422099a07a25f5bc
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341831"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Przewodnik po monitorowaniu w chmurze: strategia monitorowania dla modeli wdrożenia w chmurze

Ten artykuł zawiera naszą zalecaną strategię monitorowania dla każdego z modeli wdrożenia w chmurze, w oparciu o następujące kryteria:

- Musisz zachować zobowiązania do Operations Manager lub innej platformy monitorowania przedsiębiorstwa, ponieważ jest ona zintegrowana z procesami, wiedzą i wiedzą o działaniach IT, a niektóre funkcje nie są jeszcze dostępne w Azure Monitor.
- Należy monitorować obciążenia zarówno lokalnie, jak i w chmurze publicznej lub tylko w chmurze.
- Twoja strategia migracji do chmury obejmuje modernizację operacji IT i przejście do naszych rozwiązań i usług monitorowania w chmurze.
- Mogą istnieć krytyczne systemy, które są gapped lub fizycznie izolowane lub są hostowane w chmurze prywatnej lub na sprzęcie fizycznym. te systemy muszą być monitorowane.

Nasza strategia obejmuje obsługę infrastruktury monitorowania (obciążeń obliczeniowych, magazynowania i serwera), aplikacji (użytkowników końcowych, wyjątków i klienta) oraz zasobów sieciowych. Zapewnia kompletną, zorientowaną na usługę perspektywę monitorowania.

## <a name="azure-cloud-monitoring"></a>Monitorowanie w chmurze platformy Azure

Azure Monitor to usługa platformy Azure Native platform, która zapewnia jedno źródło monitorowania zasobów platformy Azure. Została zaprojektowana dla rozwiązań w chmurze, które:

- Są zbudowane na platformie Azure.
- Obsługa możliwości biznesowej, która jest oparta na obciążeniach maszyn wirtualnych lub złożonych architektur, które korzystają z mikrousług i innych zasobów platformy.

Monitoruje wszystkie warstwy stosu, rozpoczynając od usług dzierżawców, takich jak Azure Active Directory Domain Services, oraz zdarzeń na poziomie subskrypcji i usługi Azure Service Health.

Monitoruje również zasoby infrastruktury, takie jak maszyny wirtualne, magazyn i zasoby sieciowe. Na najwyższej warstwie monitoruje aplikację.

Monitorując każdą z tych zależności i zbierając odpowiednie sygnały, które mogą emitować każdy z nich, uzyskasz przydatność aplikacji i potrzebną infrastrukturę kluczy.

Nasze zalecane podejście do monitorowania każdej warstwy stosu są podsumowane w poniższej tabeli:

<!-- markdownlint-disable MD033 -->

Warstwa | Zasób | Zakres | Metoda
---|---|---|----
Aplikacja | Aplikacja oparta na sieci Web działająca na platformie .NET, .NET Core, Java, JavaScript i Node. js na maszynie wirtualnej platformy Azure, na platformie Azure App Services, na platformie Azure Service Fabric, Azure Functions i Cloud Services na platformie Azure. | Monitoruj działającą aplikację sieci Web, aby automatycznie wykrywać anomalie wydajności, identyfikować wyjątki i problemy z kodem oraz zbierać analizy zachowania użytkowników. |  Azure Monitor (Application Insights).
Zasoby platformy Azure — platforma jako usługa (PaaS) | Usługi Azure Database Services (na przykład SQL lub MySQL). | Metryki wydajności usługi Azure Database for SQL. | Włączanie rejestrowania diagnostycznego w celu przesyłania strumieniowego danych SQL do dzienników Azure Monitor.
Zasoby platformy Azure — infrastruktura jako usługa (IaaS) | 1. usługa Azure Storage<br/> 2. Application Gateway platformy Azure<br/> 3. sieciowe grupy zabezpieczeń<br/> 4. Traffic Manager platformy Azure<br/> 5. Virtual Machines platformy Azure<br/> 6. usługa Azure Kubernetes/Azure Container Instances | 1. pojemność, dostępność i wydajność.<br/> 2. Dzienniki wydajności i diagnostyki (aktywność, dostęp, wydajność i Zapora).<br/> 3. Monitoruj zdarzenia, gdy reguły są stosowane, oraz licznik reguł dla tego, ile razy reguła jest stosowana do odmowy lub zezwolenia.<br/> 4. Monitoruj dostępność stanu punktu końcowego.<br/> 5. monitorowanie pojemności, dostępności i wydajności w systemie operacyjnym gościa maszyny wirtualnej (OS). Mapowanie zależności aplikacji hostowanych na poszczególnych maszynach wirtualnych, w tym widoczność aktywnych połączeń sieciowych między serwerami, opóźnieniem połączenia przychodzącego i wychodzącego oraz portów w dowolnej architekturze połączonej z protokołem TCP.<br/> 6. monitorowanie pojemności, dostępności i wydajności obciążeń działających w kontenerach i wystąpieniach kontenerów. | 1. metryki magazynu dla usługi BLOB Storage.<br/> 2. Włącz rejestrowanie diagnostyki i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 3. Włącz rejestrowanie diagnostyki sieciowych grup zabezpieczeń i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 4. Włącz rejestrowanie diagnostyki dla punktów końcowych Traffic Manager i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 5. Włącz Azure Monitor dla maszyn wirtualnych.<br/> 6. Włącz Azure Monitor dla kontenerów.
Network | Komunikacja między maszyną wirtualną i jednym lub wieloma punktami końcowymi (inna maszyna wirtualna, w pełni kwalifikowana nazwa domeny, jednolity identyfikator zasobu lub adres IPv4). | Monitoruj zmiany, opóźnienia i topologię sieci między maszyną wirtualną a punktem końcowym. | Network Watcher platformy Azure.
Subskrypcja platformy Azure | Kondycja usługi platformy Azure i podstawowa Kondycja zasobów. | <li> Akcje administracyjne wykonywane w ramach usługi lub zasobu.<br/><li> Kondycja usługi w ramach usługi platformy Azure jest w stanie obniżonej lub niedostępności.<br/><li> Wykryto problemy z kondycją w ramach zasobu platformy Azure z perspektywy usługi platformy Azure.<br/><li> Operacje wykonywane przy użyciu automatycznego skalowania platformy Azure wskazujące awarię lub wyjątek. <br/><li> Operacje wykonywane z Azure Policy wskazujące, że wystąpiła dozwolona lub odmowa akcja.<br/><li> Rekord alertów generowanych przez Azure Security Center. | Dostarczana w dzienniku aktywności do monitorowania i wysyłania alertów za pomocą Azure Resource Manager.
Dzierżawa platformy Azure | Azure Active Directory || Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorowanie chmury hybrydowej

W przypadku wielu organizacji przejście do chmury musi być stopniowo zbliżane, gdzie model chmury hybrydowej jest najbardziej typowym krokiem w podróży. Należy uważnie wybrać odpowiedni podzbiór aplikacji i infrastruktury, aby rozpocząć migrację, a jednocześnie uniknąć przerw w działaniu firmy. Jednak firma Microsoft oferuje dwie platformy monitorujące, które obsługują ten model chmury, a decyzje IT mogą być niepewne, co jest najlepszym rozwiązaniem dla wspierania ich działalności biznesowej i celów operacyjnych IT.

W tej sekcji postanowimy o niepewności, sprawdzając kilka czynników i oferując zrozumienie platformy, które należy wziąć pod uwagę.

Weź pod uwagę następujące kluczowe aspekty techniczne:

- Należy zebrać dane z zasobów platformy Azure, które obsługują obciążenie, i przekazywać je do istniejących narzędzi lokalnych lub zarządzanych dostawcy usług.

- Musisz zachować aktualną inwestycję w System Center Operations Manager i skonfigurować ją do monitorowania zasobów IaaS i PaaS, które działają na platformie Azure. Opcjonalnie ze względu na to, że monitorowane są dwa środowiska o różnej charakterystyce, w zależności od wymagań należy określić, jak integracja z Azure Monitor obsługuje strategię.

- W ramach strategii modernizacji do standaryzacji jednego narzędzia, aby zmniejszyć koszty i złożoność, należy zatwierdzić Azure Monitor monitorowania zasobów na platformie Azure i w sieci firmowej.

Poniższa tabela zawiera podsumowanie wymagań Azure Monitor i System Center Operations Manager obsługi monitorowania modelu chmury hybrydowej na podstawie wspólnego zestawu kryteriów.

<!-- markdownlint-disable MD033 -->

|Wymaganie | Azure Monitor | Operations Manager |
|:--|:---|:---|
|Wymagania dotyczące infrastruktury | Nie | Yes<br> Wymaga co najmniej serwera zarządzania i programu SQL Server do hostowania operacyjnej bazy danych i bazy danych magazyn danych raportowania. Złożoność zwiększa się, gdy wymagane jest zapewnienie wysokiej dostępności i odzyskiwania po awarii oraz maszyn w wielu lokacjach, niezaufanych systemach i innych kwestiach związanych z projektowaniem.|
|Łączność ograniczona — brak Internetu<br> lub sieć izolowana | Nie | Yes |
|Ograniczony dostęp do Internetu kontrolowany przez łączność | Yes | Yes |
|Ograniczone połączenia — często rozłączone | Yes | Yes |
|Konfigurowalne monitorowanie kondycji | Nie | Yes |
| Test dostępności aplikacji sieci Web (izolowana sieć) | Tak, ograniczone<br> Azure Monitor ma ograniczoną obsługę w tym obszarze i wymaga niestandardowych wyjątków zapory. | Yes |
| Test dostępności aplikacji sieci Web (dystrybuowany globalnie) | Nie | Yes |
|Monitorowanie obciążeń maszyn wirtualnych | Tak, ograniczone<br> Może zbierać usługi IIS oraz SQL Server dzienników błędów, zdarzeń systemu Windows i liczników wydajności. Wymaga utworzenia niestandardowych zapytań, alertów i wizualizacji. | Yes<br> Obsługuje monitorowanie większości obciążeń serwera z dostępnymi pakietami administracyjnymi. Na maszynie wirtualnej jest wymagany agent Log Analytics lub Agent Operations Manager, który umożliwia raportowanie z powrotem do grupy zarządzania w sieci firmowej.|
|Monitorowanie usługi Azure IaaS | Yes | Yes<br> Obsługuje monitorowanie większości infrastruktury z sieci firmowej. Śledzi stan dostępności, metryki i alerty dla maszyn wirtualnych platformy Azure, bazy danych SQL i magazynu za pośrednictwem pakietu administracyjnego platformy Azure.|
|Monitorowanie usługi Azure PaaS | Yes | Tak, ograniczone<br> Na podstawie tego, co jest obsługiwane w pakiecie administracyjnym platformy Azure. |
|Monitorowanie usług platformy Azure | Yes<br> | Yes<br> Chociaż nie ma natywnego monitorowania kondycji usługi platformy Azure w ramach pakietu administracyjnego, można utworzyć niestandardowe przepływy pracy, aby wysyłać zapytania dotyczące usługi Azure Service Health. Użyj interfejsu API REST platformy Azure, aby otrzymywać alerty za pomocą istniejących powiadomień.|
|Nowoczesne monitorowanie aplikacji sieci Web | Yes | Nie |
|Starsze monitorowanie aplikacji sieci Web | Tak, ograniczone, różni się w zależności od zestawu SDK<br> Obsługuje monitorowanie starszych wersji aplikacji sieci Web platformy .NET i języka Java. | Tak, ograniczone |
|Monitorowanie kontenerów usługi Azure Kubernetes Service | Yes | Nie |
|Monitorowanie kontenerów platformy Docker lub Windows | Yes | Nie |
|Monitorowanie wydajności sieci | Yes | Tak, ograniczone<br> Program obsługuje sprawdzanie dostępności i zbiera podstawowe dane statystyczne z urządzeń sieciowych przy użyciu Simple Network Management Protocol (SNMP) z sieci firmowej.|
|Interaktywna analiza danych | Yes | Nie<br> Opiera się na SQL Server Reporting Services raportach z konserwowanych lub niestandardowych, rozwiązaniach do wizualizacji innych firm lub niestandardowej implementacji Power BI. Istnieją ograniczenia dotyczące skalowania i wydajności w magazynie danych Operations Manager. Integracja z usługą Azure Monitor Logs jako alternatywa dla wymagań agregacji danych. Aby uzyskać integrację, należy skonfigurować łącznik Log Analytics.|
|Kompleksowa diagnostyka, analiza głównych przyczyn i rozwiązywanie problemów | Yes | Tak, ograniczone<br> Obsługuje kompleksową diagnostykę i rozwiązywanie problemów tylko w przypadku lokalnej infrastruktury i aplikacji. Program używa innych składników programu System Center lub rozwiązań partnerskich.|
|Interaktywne wizualizacje (pulpity nawigacyjne) | Yes | Tak, ograniczone<br> Program udostępnia podstawowe pulpity nawigacyjne z konsolą sieci Web HTML5 lub zaawansowane środowisko z rozwiązań partnerskich, takie jak kwadratowe i Savision. |
|Integracja z narzędziami IT lub DevOps | Yes | Tak, ograniczone |

<!-- markdownlint-enable MD033 -->

### <a name="collect-and-stream-monitoring-data-to-third-party-or-on-premises-tools"></a>Zbieranie i przesyłanie strumieniowe danych monitorowania do narzędzi innych firm lub lokalnych

Aby zbierać metryki i dzienniki z zasobów platformy i infrastruktury platformy Azure, należy włączyć dzienniki Diagnostyka Azure dla tych zasobów. Ponadto dzięki maszynom wirtualnym platformy Azure można zbierać metryki i dzienniki z systemu operacyjnego gościa, włączając rozszerzenie Diagnostyka Azure. Aby przesłać dane diagnostyczne, które są emitowane z zasobów platformy Azure do narzędzi lokalnych lub dostawcy usług zarządzanych, skonfiguruj [Event Hubs](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-stream-event-hubs) do przesyłania strumieniowego danych.

### <a name="monitor-with-system-center-operations-manager"></a>Monitoruj przy użyciu System Center Operations Manager

Mimo że System Center Operations Manager pierwotnie zaprojektowano jako rozwiązanie lokalne do monitorowania między aplikacjami, obciążeniami i składnikami infrastruktury, które działają w środowisku IT, został rozbudowany w taki sposób, aby obejmował monitorowanie chmury możliwość. Integruje się z platformą Azure, pakietem Office 365 i Amazon Web Services (AWS). Może ona być monitorowana w różnych środowiskach z pakietami administracyjnymi, które zostały zaprojektowane i zaktualizowane w celu ich obsługi.  

W przypadku klientów, którzy zastosowali znaczące inwestycje w Operations Manager, aby osiągnąć kompleksowe monitorowanie ściśle zintegrowane ze swoimi zarządzanie usługami ITmi procesami i narzędziami, lub dla klientów nowych na platformie Azure, zrozumiałe jest zadawanie następujących informacji masz

- Czy Operations Manager kontynuować dostarczanie wartości i czy ma ona sens biznesowy?
- Czy funkcje w Operations Manager być odpowiednie dla naszej organizacji IT?
- Czy integracja Operations Manager z Azure Monitor oferuje ekonomiczne i kompleksowe rozwiązanie do monitorowania?

Jeśli zainwestowano już w Operations Manager, nie trzeba skupić się na planowaniu migracji w celu jej natychmiastowego zastępowania. Korzystając z platformy Azure lub innych dostawców chmury, którzy istnieją jako rozszerzenia własnej sieci lokalnej, Operations Manager mogą monitorować maszyny wirtualne gościa i zasoby platformy Azure, tak jakby znajdowały się w sieci firmowej. Takie podejście wymaga niezawodnego połączenia sieciowego między siecią i siecią wirtualną platformy Azure, która ma wystarczającą przepustowość.

Aby monitorować obciążenia działające na platformie Azure, potrzebne są:

- [Pakiet administracyjny dla platformy Azure](https://www.microsoft.com/download/details.aspx?id=50013). Zbiera metryki wydajności emitowane przez usługi platformy Azure, takie jak role sieci Web i procesu roboczego, Application Insights testy dostępności (testy sieci Web), Azure Service Bus i tak dalej. Pakiet administracyjny używa interfejsu API REST platformy Azure do monitorowania dostępności i wydajności tych zasobów. Niektóre typy usług platformy Azure nie mają metryk ani wstępnie zdefiniowanych monitorów w pakiecie administracyjnym, ale nadal można je monitorować za pomocą relacji zdefiniowanych w pakiecie administracyjnym platformy Azure dla odnalezionych usług.

- [Pakiet administracyjny dla Azure SQL Database](https://www.microsoft.com/download/details.aspx?id=38829) monitorowania dostępności i wydajności baz danych SQL Azure i serwerów usługi Azure SQL Database przy użyciu interfejsu API REST platformy Azure i zapytań T-SQL do SQL Server widoków systemowych.

- Aby monitorować system operacyjny gościa i obciążenia uruchomione na maszynie wirtualnej, takie jak SQL Server, IIS lub Apache Tomcat, należy pobrać i zaimportować pakiet administracyjny obsługujący aplikację, usługę i system operacyjny.

W pakiecie administracyjnym jest zdefiniowana wiedza opisująca sposób monitorowania poszczególnych zależności i składników. Oba pakiety administracyjne platformy Azure wymagają wykonania zestawu kroków konfiguracyjnych na platformie Azure i Operations Manager przed rozpoczęciem monitorowania tych zasobów.

W warstwie aplikacji Operations Manager oferuje podstawowe możliwości monitorowania wydajności aplikacji dla niektórych starszych wersji platformy .NET i języka Java. Jeśli niektóre aplikacje w środowisku chmury hybrydowej działają w trybie offline lub izolowanym przez sieć, w taki sposób, że nie mogą komunikować się z usługą w chmurze publicznej, Operations Manager Application Performance Monitoring (APM) może być opcją realną dla Niektóre ograniczone scenariusze. W przypadku aplikacji, które nie są uruchomione na starszych platformach, ale są hostowane lokalnie i w dowolnej chmurze publicznej, która umożliwia komunikację za pośrednictwem zapory (bezpośrednie lub za pośrednictwem serwera proxy) na platformie Azure, użyj Azure Monitor Application Insights. Ta usługa oferuje głębokie monitorowanie na poziomie kodu z obsługą pierwszej klasy dla ASP.NET, ASP.NET Core, Java, JavaScript i Node. js.

W przypadku dowolnej aplikacji sieci Web, którą można uzyskać zewnętrznie, należy włączyć typ transakcji syntetycznej znanej jako [monitorowanie dostępności]( https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability). Ważne jest, aby dowiedzieć się, czy aplikacja lub krytyczne punkty końcowe protokołu HTTP/HTTPS, na których bazują aplikacja, są dostępne i odpowiada. Dzięki monitorowaniu dostępności Application Insights można uruchamiać testy z wielu centrów danych platformy Azure i zapewniać wgląd w kondycję aplikacji z perspektywy globalnej.

Mimo że Operations Manager jest w stanie monitorować zasoby hostowane na platformie Azure, istnieje kilka zalet, aby dołączać Azure Monitor, ponieważ jego mocne przezwyciężyją ograniczenia w Operations Manager i mogą nawiązywać silne podstawy Obsługa ostatecznej migracji. W tym miejscu analizujemy każdą z tych mocnych i słabych stron, z zaleceniem uwzględnienia Azure Monitor w strategii monitorowania hybrydowego.  

#### <a name="disadvantages-of-using-operations-manager-by-itself"></a>Wady używania Operations Manager przez siebie

- Analizowanie danych monitorowania w Operations Manager jest zwykle wykonywane przy użyciu wstępnie zdefiniowanych widoków, które są udostępniane przez pakiety administracyjne dostępne z konsoli programu, z raportów SQL Server Reporting Services (SSRS) lub z widoków niestandardowych utworzonych przez użytkowników końcowych. Analiza danych ad hoc nie jest możliwa. Raportowanie Operations Manager jest nieelastyczne. Magazyn danych, który zapewnia długoterminowe przechowywanie danych monitorowania, nie jest skalowany ani nie działa prawidłowo. I wiedzą na temat pisania instrukcji języka T-SQL, opracowywania rozwiązania Power BI lub korzystania z rozwiązań innych firm do obsługi wymagań dla różnych osób w organizacji IT.

- Generowanie alertów w Operations Manager nie obsługuje złożonych wyrażeń ani nie obejmuje logiki korelacji. Aby pomóc w zmniejszeniu szumu, alerty są pogrupowane w celu wyświetlenia relacji między nimi i zidentyfikowania ich przyczyn.

#### <a name="advantages-of-using-operations-manager-with-azure-monitor"></a>Zalety korzystania z Operations Manager z Azure Monitor

- Azure Monitor jest sposobem na obejście ograniczeń Operations Manager. Uzupełnienie bazy danych magazynu danych Operations Manager przez gromadzenie ważnych danych dotyczących wydajności i dzienników. Azure Monitor zapewnia lepszą analizę, wydajność (podczas wykonywania zapytań dotyczących dużych ilości danych) i przechowywanie niż Operations Manager magazynu danych.

  Korzystając z języka zapytań Azure Monitor, można tworzyć dużo bardziej złożone i zaawansowane zapytania. W ciągu kilku sekund można uruchamiać zapytania między terabajtami danych. Możesz szybko przekształcić dane na wykresy kołowe, wykresy czasowe i wiele innych wizualizacji. Aby przeanalizować te dane, nie są już ograniczone przez pracę z Operations Manager raportami opartymi na SQL Server Reporting Services, niestandardowych zapytaniach SQL lub innych obejściach.

- Udoskonalone środowisko obsługi alertów można zapewnić, implementując rozwiązanie do zarządzania alertami Azure Monitor. Alerty generowane w grupie zarządzania Operations Manager można przesłać dalej do obszaru roboczego usługi Logs Azure Monitor dzienników. Można skonfigurować subskrypcję odpowiedzialną za przekazywanie alertów z Operations Manager do Azure Monitor dzienników, aby przekazywać tylko niektóre alerty. Na przykład można przesłać dalej tylko alerty, które spełniają kryteria do wykonywania zapytań w zakresie zarządzania problemami, a także badanie głównej przyczyny awarii lub problemów za pomocą jednego z okien szklanych. Ponadto możesz skorelować inne dane dziennika z Application Insights lub innych źródeł, aby uzyskać szczegółowe informacje, które pomagają ulepszyć środowisko użytkownika, zwiększyć czas przestoju i skrócić czas rozwiązywania problemów.

- Możesz monitorować natywną infrastrukturę i aplikacje w chmurze, korzystając z prostej lub wielowarstwowej architektury na platformie Azure, a Operations Manager można używać do monitorowania infrastruktury lokalnej. To monitorowanie obejmuje co najmniej jedną maszynę wirtualną, wiele maszyn wirtualnych umieszczonych w zestawie dostępności lub zestaw skalowania maszyn wirtualnych, lub aplikację zwirtualizowaną wdrożoną w usłudze Azure Kubernetes Service (AKS) działającą w kontenerach systemu Windows Server lub Linux.

- Możesz użyć rozwiązania System Center Operations Manager Health Check, aby proaktywnie ocenić ryzyko i kondycję grupy zarządzania System Center Operations Manager w regularnych odstępach czasu. To rozwiązanie może zastąpić lub uzupełnić wszelkie niestandardowe funkcje dodane do grupy zarządzania.

- Za pomocą funkcji mapy Azure Monitor dla maszyn wirtualnych można monitorować standardowe metryki łączności z połączeń sieciowych między maszynami wirtualnymi platformy Azure i lokalnymi maszynami wirtualnymi. Te metryki obejmują czas odpowiedzi, żądania na minutę, przepływność ruchu i linki. Można zidentyfikować nieudane połączenia, rozwiązać problemy, przeprowadzić weryfikację migracji, przeprowadzić analizę zabezpieczeń i sprawdzić ogólną architekturę usługi. Usługa map może automatycznie odnajdywać składniki aplikacji w systemach Windows i Linux oraz mapować komunikację między usługami. Ta automatyzacja pomaga identyfikować połączenia i zależności, z którymi było nieświadome, zaplanować i zweryfikować migrację na platformę Azure oraz zminimalizować proces rozwiązywania problemów.

- Za pomocą Network Performance Monitor można monitorować łączność sieciową między:
  - Sieci firmowej i platformy Azure.
  - Najważniejsze aplikacje wielowarstwowe i mikrousługi.
  - Lokalizacje użytkowników i aplikacje oparte na sieci Web (HTTP/HTTPS).

Ta strategia zapewnia widoczność warstwy sieciowej bez potrzeby korzystania z protokołu SNMP. Może również znajdować się w interaktywnej mapie topologii, topologia przeskoków między źródłem a docelowym punktem końcowym. Jest to lepszy wybór niż próba wykonania tego samego wyniku przy użyciu monitorowania sieci w Operations Manager lub innych narzędzi do monitorowania sieci, które są obecnie używane w danym środowisku.

### <a name="monitor-with-azure-monitor"></a>Monitorowanie za pomocą usługi Azure Monitor

Mimo że migracja do chmury przedstawia wiele wyzwań, zawiera również wiele szans. Dzięki temu organizacja może przeprowadzić migrację z jednego lub wielu lokalnych narzędzi do monitorowania przedsiębiorstwa, aby nie tylko zredukować nakłady inwestycyjne i koszty operacyjne, ale również korzystać z zalet platformy monitorowania w chmurze, takiej jak Azure Monitor może być oferowany w skali chmury. Sprawdź wymagania dotyczące monitorowania i wysyłania alertów, konfigurację istniejących narzędzi do monitorowania oraz obciążeń przenoszonych do chmury. Po sfinalizowaniu planu Skonfiguruj Azure Monitor.

- Monitoruj hybrydową infrastrukturę i aplikacje, korzystając z prostej lub wielowarstwowej architektury, w której składniki są hostowane między platformą Azure, innymi dostawcami chmury i siecią firmową. Składniki mogą zawierać co najmniej jedną maszynę wirtualną, wiele maszyn wirtualnych umieszczonych w zestawie dostępności lub zestaw skalowania maszyn wirtualnych, lub aplikację zwirtualizowaną wdrożoną w usłudze Azure Kubernetes Service (AKS) działającą w kontenerach systemu Windows Server lub Linux.

- Włącz Azure Monitor dla maszyn wirtualnych, Azure Monitor dla kontenerów i Application Insights wykrywać i diagnozować problemy między infrastrukturą i aplikacjami. Aby uzyskać dokładniejszą analizę i korelację danych zbieranych z wielu składników lub zależności obsługujących aplikację, należy użyć dzienników Azure Monitor.

- Tworzenie inteligentnych alertów, które mają zastosowanie do podstawowego zestawu aplikacji i składników usług, zmniejszenie szumu alertów z progami dynamicznymi dla złożonych sygnałów i używanie agregacji alertów na podstawie algorytmów uczenia maszynowego w celu szybkiego zidentyfikowania problemu.

- Zdefiniuj bibliotekę zapytań i pulpitów nawigacyjnych, aby obsługiwać wymagania różnych osób w organizacji IT.

- Zdefiniuj standardy i metody umożliwiające monitorowanie zasobów hybrydowych i w chmurze, linię bazową monitorowania dla każdego zasobu, progi alertów itd.  

- Skonfiguruj kontrolę dostępu opartą na rolach (RBAC), aby przyznać użytkownikom i grupom tylko dostęp do tych zasobów, których potrzebują do zarządzania nimi.

- Dołącz automatyzację i samoobsługowe, aby umożliwić każdemu zespołowi tworzenie, Włączanie i dostrajanie konfiguracji monitorowania i alertów w razie potrzeby.

## <a name="private-cloud-monitoring"></a>Monitorowanie chmury prywatnej

Można osiągnąć całościowe monitorowanie Azure Stack z System Center Operations Manager. W tym celu można monitorować obciążenia uruchomione w dzierżawie, na poziomie zasobów na maszynach wirtualnych oraz Azure Stack hostingu infrastruktury (serwery fizyczne i przełączniki sieciowe).

Można również uzyskać całościowe monitorowanie z kombinacją [możliwości monitorowania infrastruktury](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) , które znajdują się w Azure Stack. Te funkcje ułatwiają wyświetlanie kondycji i alertów dla regionu Azure Stack i [usługi Azure monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) w Azure Stack, która zapewnia metryki infrastruktury i dzienniki na poziomie podstawowym dla większości usług.

Jeśli zainwestowano już w Operations Manager, Użyj pakietu administracyjnego Azure Stack do monitorowania stanu dostępności i kondycji Azure Stack wdrożeń, w tym regionów, dostawców zasobów, aktualizacji, przebiegów aktualizacji, jednostek skalowania, węzłów jednostek, infrastruktury role i ich wystąpienia (jednostki logiczne składają się z zasobów sprzętowych). Ten pakiet administracyjny używa interfejsów API REST i aktualizacji dostawcy zasobów do komunikowania się z Azure Stack. Aby monitorować serwery fizyczne i urządzenia magazynujące, należy użyć pakietu administracyjnego dostawcy OEM (na przykład dostarczonego przez firmę Lenovo, Hewlett Packard lub Dell). Operations Manager może natywnie monitorować przełączniki sieciowe w celu zbierania podstawowych statystyk przy użyciu protokołu SNMP. Monitorowanie obciążeń dzierżawców jest możliwe z pakietem administracyjnym platformy Azure, wykonując dwa podstawowe kroki. Skonfiguruj subskrypcję, którą chcesz monitorować, a następnie Dodaj monitory dla tej subskrypcji.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Zbieranie właściwych danych](./data-collection.md)
