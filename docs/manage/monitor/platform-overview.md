---
title: Przewodnik monitorowania chmury — Omówienie platform monitorowania
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Określ, kiedy używać Azure Monitor lub System Center Operations Manager w Microsoft Azure
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 33d9647a0804859a611d45e130c753cab89a6ef6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031072"
---
# <a name="cloud-monitoring-guide-overview-of-our-monitoring-platforms"></a>Przewodnik monitorowania chmury: Omówienie naszych platform monitorowania

Firma Microsoft oferuje szereg możliwości monitorowania z dwóch produktów: System Center Operations Manager, która została zaprojektowana dla lokalnego, a następnie rozszerzona do chmury i Azure Monitor, która została zaprojektowana dla chmury, ale również może monitorować systemy lokalne. Te dwie oferty zapewniają podstawowe usługi monitorowania, takie jak alerty, śledzenie czasu przestoju usługi, monitorowanie kondycji aplikacji i infrastruktury, Diagnostyka i analiza.

Wiele organizacji korzysta z najnowszych wskazówek dotyczących elastyczności DevOps i innowacji w chmurze do zarządzania środowiskami heterogenicznych. Jednak są one również zaangażowane w odpowiednie i odpowiedzialne decyzje dotyczące monitorowania tych obciążeń.

Ten artykuł zawiera ogólne omówienie naszych platform monitorowania, które ułatwiają zrozumienie sposobu dostarczania podstawowych funkcji monitorowania.

## <a name="story-of-system-center-operations-manager"></a>Historie System Center Operations Manager

W 2000 wprowadzono pole zarządzania operacjami z firmą Microsoft Operations Manager (MOM) 2000. W 2007 wprowadzono ponownie przeprojektowaną wersję produktu o nazwie System Center Operations Manager. Przeniesiono poza proste monitorowanie systemu Windows Server i skoncentrowano się na niezawodnej, kompleksowym monitorowaniu usług i aplikacji, w tym na platformach heterogenicznych, urządzeniach sieciowych i innych zależnościach aplikacji lub usług. Jest to ustanowiona platforma monitorowania klasy korporacyjnej dla środowisk lokalnych, w tej samej klasie jak IBM Tivoli lub HP Operations Manager w branży. Miało to na celu obsługę monitorowania zasobów obliczeniowych i platform działających na platformie Azure, Amazon Web Services (AWS) i innych dostawców chmury.

## <a name="story-of-azure-monitor"></a>Historie Azure Monitor

Gdy platforma Azure została wydana w 2010, monitorowanie usług Cloud Services zostało dostarczone z agentem Diagnostyka Azure, który zapewnia sposób zbierania danych diagnostycznych z zasobów platformy Azure. Ta funkcja została uznana za ogólne narzędzie monitorowania, a nie na platformę monitorowania klasy korporacyjnej.  

Application Insights wprowadzono zmiany w branży, gdzie rośnie rozprzestrzenianie się rozwiązań chmurowych, mobilnych i IoT oraz wprowadzenie praktyk DevOps. Zwiększył się z programu Application Performance Monitoring w Operations Manager do usługi platformy Azure, która zapewnia rozbudowane monitorowanie aplikacji sieci Web, które są zapisywane w różnych językach. W 2015, wersja zapoznawcza Application Insights programu Visual Studio została ogłoszona i nowsza, stała się znana jako Application Insights. Gromadzi szczegółowe informacje o wydajności aplikacji, żądaniach i wyjątkach oraz śladach.

W 2015 usługa Azure Operational Insights była ogólnie dostępna. Dostarczono usługę analizy Log Analytics, która zbiera i przeszukuje dane z maszyn na platformie Azure, w Premium lub innych środowiskach chmurowych i podłączonych do System Center Operations Manager. Oferowane są pakiety analiz, które udostępniają różne wstępnie spakowane konfiguracje zarządzania i monitorowania, które zawierały kolekcję zapytań i logiki analitycznych, wizualizacje i reguły zbierania danych na potrzeby takich scenariuszy jak Inspekcja zabezpieczeń, kondycja oceny i zarządzanie alertami.  Późniejsza usługa Azure Operational Insights stała się znana jako Log Analytics.  

W 2016, wersja zapoznawcza Azure Monitor była ogłoszona jako "zapłon". Zapewnia ona wspólną strukturę zbierania metryk platformy, dzienników diagnostyki zasobów i zdarzeń dziennika aktywności na poziomie subskrypcji z dowolnej usługi platformy Azure, która została uruchomiona przy użyciu platformy. Wcześniej każda usługa platformy Azure miała własną metodę monitorowania.

Na konferencji dotyczącej zapłonu firmy Microsoft w 2018 ogłoszono, że Azure Monitora została rozwinięta w taki sposób, aby obejmowała kilka różnych usług opracowanych z niezależnymi funkcjami

- Oryginalne **Azure monitor** funkcje zbierania metryk platformy, dzienników diagnostyki zasobów i dzienników aktywności tylko dla zasobów platformy Azure.
- **Application Insights** monitorowania aplikacji.
- **Log Analytics** jako podstawową lokalizację zbierania i analizowania danych dziennika.
- Nowa **Usługa ujednoliconych alertów** , która łączy mechanizmy alertów z każdej z wymienionych wcześniej usług.  
- **Usługa azure Network Watcher** umożliwia monitorowanie, diagnozowanie i wyświetlanie metryk dla zasobów w sieci wirtualnej platformy Azure.

## <a name="the-story-of-operations-management-suite-oms"></a>Historia pakietu Operations Management Suite (OMS)

Od 2015 do 2018 kwietnia, pakiet Operations Management Suite (OMS) to zbiór następujących usług zarządzania platformy Azure do celów licencjonowania:

- Application Insights
- Azure Automation
- Azure Backup
- Operational Insights (później Log Analytics z oznaczeniem)
- Site Recovery

Funkcje usług, które były częścią pakietu OMS, nie uległy zmianie, gdy pakiet OMS został wycofany, został przewyrównany w obszarze Azure Monitor.

## <a name="infrastructure-requirements"></a>Wymagania dotyczące infrastruktury

### <a name="operations-manager"></a>Operations Manager

Operations Manager wymaga znaczącej infrastruktury i konserwacji do obsługi grupy zarządzania, która jest podstawową jednostką funkcjonalności. Co najmniej jeden z grup zarządzania składa się z jednego lub większej liczby serwerów zarządzania, SQL Server, hostowania bazy danych operacyjnych i magazyn danych raportowania oraz agentów. Złożoność projektu grupy zarządzania zależy od wielu czynników, takich jak zakres obciążeń do monitorowania i liczba urządzeń lub komputerów, które obsługują obciążenia. Jeśli potrzebujesz wysokiej dostępności i odporności lokacji, tak jak w przypadku platform monitorowania przedsiębiorstwa, wymagania dotyczące infrastruktury i powiązanej konserwacji mogą się znacznie zwiększyć.

![Diagram grupy zarządzania Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor to usługa SaaS, w której cała infrastruktura obsługująca ją na platformie Azure jest zarządzana przez firmę Microsoft. Jest on przeznaczony do przeprowadzania monitorowania, analizy i diagnostyki na dużą skalę i jest dostępny we wszystkich chmurach narodowych. Podstawowe części infrastruktury (moduły zbierające, magazyny, metryki i dzienniki) niezbędne do obsługi Azure Monitor są obsługiwane przez firmę Microsoft.  

![Diagram Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Zbieranie danych

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agenci

Operations Manager zbiera tylko dane bezpośrednio z agentów zainstalowanych na [komputerach z systemem Windows](https://docs.microsoft.com//system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Może akceptować dane z zestawu SDK Operations Manager, ale jest to zwykle używane w przypadku partnerów rozszerzających produkt za pomocą aplikacji niestandardowych, a nie do zbierania danych monitorowania. Może zbierać dane z innych źródeł, takich jak [komputery z systemem Linux](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) i urządzenia sieciowe, przy użyciu specjalnych modułów uruchomionych w agencie systemu Windows zdalnie uzyskujących dostęp do tych innych urządzeń.

![Diagram Operations Manager agenta](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

Agent Operations Manager może zbierać dane z wielu źródeł danych na komputerze lokalnym, takich jak dziennik zdarzeń, dzienniki niestandardowe i liczniki wydajności. Może również uruchamiać skrypty, które mogą zbierać dane z komputera lokalnego lub ze źródeł zewnętrznych. Można napisać skrypty niestandardowe do zbierania danych, które nie mogą być zbierane w inny sposób, lub z różnych urządzeń zdalnych, których nie można monitorować w inny sposób.

#### <a name="management-packs"></a>Pakiety administracyjne

Operations Manager wykonuje wszystkie czynności monitorowania za pomocą przepływów pracy (reguł, monitorów i odnajdywania obiektów). Są one spakowane w [pakiecie administracyjnym](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019)i wdrażane dla agentów. Pakiety administracyjne są dostępne dla różnych produktów i usług, które obejmują wstępnie zdefiniowane zasady i monitory. Możesz również utworzyć własny pakiet administracyjny dla własnych aplikacji i scenariuszy niestandardowych.

#### <a name="monitoring-configuration"></a>Konfiguracja monitorowania

Pakiety administracyjne mogą zawierać setki reguł, monitorów i reguł odnajdywania obiektów. Agent uruchamia wszystkie te ustawienia monitorowania ze wszystkich pakietów administracyjnych, które mają zastosowanie, które są określane przez reguły odnajdywania. Każde wystąpienie każdego ustawienia monitorowania działa niezależnie, a natychmiast działa bezpośrednio na zbieranych danych. Poniżej przedstawiono sposób, w jaki Operations Manager można osiągnąć alerty niemal w czasie rzeczywistym oraz bieżący stan kondycji monitorowanych zasobów.

Przykładowo monitor może próbkować licznik wydajności co kilka minut. Jeśli ten licznik przekroczy wartość progową, natychmiast ustawi stan kondycji obiektu docelowego, który natychmiast wyzwala alert w grupie zarządzania. Zaplanowana reguła może oglądać konkretne zdarzenie, które ma zostać utworzone, i natychmiast uruchomić alert po utworzeniu tego zdarzenia w lokalnym dzienniku zdarzeń.

Ponieważ te ustawienia monitorowania są odizolowane od siebie i pracują z poszczególnych źródeł danych, Operations Manager ma wyzwania skorelowania danych między wieloma źródłami. Trudno jest również reagować na dane po ich zebraniu. Można uruchamiać przepływy pracy, które uzyskują dostęp do bazy danych Operations Manager, ale ten scenariusz nie jest typowy i jest zazwyczaj używany w ograniczonej liczbie przepływów pracy specjalnych przeznaczenie.

![Diagram grupy zarządzania Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Źródła danych

Azure Monitor zbiera dane z różnych źródeł, w tym zasobów platformy i infrastruktury platformy Azure, agentów na komputerach z systemem Windows i Linux oraz monitorowania danych zebranych w usłudze Azure Storage. Każdy klient REST może zapisywać dane dziennika do Azure Monitor przy użyciu interfejsu API, a także definiować metryki niestandardowe dla aplikacji sieci Web. Niektóre dane metryk mogą być kierowane do różnych lokalizacji, w zależności od ich użycia. Można na przykład użyć danych dla alertów "szybkiej jako możliwe" lub długoterminowej analizy trendów przeszukiwanych w połączeniu z innymi danymi dziennika.

#### <a name="monitoring-solutions-and-insights"></a>Monitorowanie rozwiązań i szczegółowych informacji

Rozwiązania do monitorowania wykorzystują platformę Logs w Azure Monitor, aby zapewnić monitorowanie dla określonej aplikacji lub usługi. Zazwyczaj określają one zbieranie danych z agentów lub usług platformy Azure, a także udostępniają zapytania i widoki dzienników umożliwiające analizowanie tych danych. Zazwyczaj nie zapewniają one reguł alertów, co oznacza, że musisz zdefiniować własne kryteria alertu na podstawie zebranych danych.

Szczegółowe informacje, takie jak Azure Monitor kontenerów i Azure Monitor dla maszyn wirtualnych, umożliwiają używanie dzienników i platformy metryk Azure Monitor w celu zapewnienia niestandardowego środowiska monitorowania dla aplikacji lub usługi w Azure Portal. Oprócz dostosowanej analizy zebranych danych mogą one zawierać warunki monitorowania kondycji i alertów.

#### <a name="monitoring-configuration"></a>Konfiguracja monitorowania

Azure Monitor oddziela zbieranie danych od akcji wykonanych względem tych danych, które obsługują rozproszone mikrousługi w środowisku chmury. Konsoliduje dane z wielu źródeł na wspólną platformę danych, a także udostępnia funkcje analizy, wizualizacji i alertów na podstawie zebranych danych.

Wszystkie dane zbierane przez Azure Monitor są przechowywane jako dzienniki lub metryki i różne funkcje monitora polegają na obu. Metryki zawierają wartości liczbowe w szeregach czasowych, które są dobrze dopasowane do alertów niemal w czasie rzeczywistym i szybkiego wykrywania problemów. Dzienniki zawierają dane tekstowe lub liczbowe i są obsługiwane przez zaawansowany język zapytań, który sprawia, że są one szczególnie przydatne do wykonywania złożonej analizy.

Ponieważ monitor oddziela zbieranie danych od akcji związanych z tymi danymi, może nie być w stanie zapewnić w wielu przypadkach alertów niemal w czasie rzeczywistym. Aby otrzymywać alerty dotyczące danych dziennika, zapytania są uruchamiane według cyklicznego harmonogramu zdefiniowanego w alercie. Takie zachowanie pozwala Azure Monitor łatwo skorelować dane ze wszystkich monitorowanych źródeł i interaktywnie analizować dane na różne sposoby. Jest to szczególnie przydatne w przypadku analizy głównej przyczyny i zidentyfikowania, gdzie może wystąpić problem.

## <a name="health-monitoring"></a>Monitorowanie kondycji

### <a name="operations-manager"></a>Operations Manager

Pakiety administracyjne w Operations Manager obejmują model usługi, który opisuje składniki monitorowanej aplikacji oraz ich relacje. Monitory identyfikują bieżący stan kondycji każdego składnika na podstawie danych i skryptów w agencie. Stan kondycji umożliwia szybkie wyświetlenie podsumowania kondycji monitorowanych komputerów i aplikacji.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor nie zapewnia użytkownikowi definiowanej metody implementacji modelu usług lub monitorów, które wskazują bieżący stan kondycji wszystkich składników usługi. Ponieważ rozwiązania monitorujące bazują na standardowych funkcjach Azure Monitor, nie zapewniają monitorowania poziomu stanu. Następujące funkcje Azure Monitor mogą być przydatne:

- **Application Insights** kompiluje złożoną mapę aplikacji sieci Web i zapewnia stan kondycji dla każdego składnika aplikacji lub zależności. Dotyczy to również stanu alertów i przechodzenia do szczegółów w celu uzyskania bardziej szczegółowej diagnostyki aplikacji.

- **Azure monitor dla maszyn wirtualnych** zapewnia środowisko monitorowania kondycji maszyn wirtualnych platformy Azure gościa, podobnie jak Operations Manager, podczas monitorowania maszyn wirtualnych z systemami Windows i Linux. Szacuje kondycję kluczowych składników systemu operacyjnego z perspektywy dostępności i wydajności w celu ustalenia bieżącego stanu kondycji. Po ustaleniu, że maszyna wirtualna gościa ma zrównoważone wykorzystanie zasobów, pojemność miejsca na dysku lub problem związany z podstawową funkcjonalnością systemu operacyjnego, generuje alert, aby uzyskać ten stan do uwagi.

- **Azure monitor kontenerów służy do** monitorowania wydajności i kondycji usług Azure Kubernetes Services lub Azure Container Instances. Zbiera metryki pamięci i procesora z kontrolerów, węzły i kontenerów, które są dostępne w usłudze Kubernetes za pomocą interfejsu API metryki. Gromadzi również dzienniki kontenerów oraz dane spisu dotyczące kontenerów i ich obrazów. Wstępnie zdefiniowane kryteria kondycji na podstawie zebranych danych wydajności pomagają ustalić, czy występuje wąskie gardło zasobów lub problemy z pojemnością. Można także zrozumieć ogólną wydajność lub wydajność z określonego typu obiektu Kubernetes (pod, węzła, kontrolera lub kontenera).

## <a name="analyzing-data"></a>Analizowanie danych

### <a name="operations-manager"></a>Operations Manager

Operations Manager oferuje cztery podstawowe sposoby analizowania danych po ich zebraniu.

- Za pomocą **Eksplorator kondycji**można dowiedzieć się, które monitory identyfikują problem ze stanem kondycji, oraz zapoznać się z wiedzą na temat monitora i możliwych przyczyn związanych z nim działań.

- **Widoki** to wstępnie zdefiniowane wizualizacje zebranych danych, takie jak wykres danych wydajności lub lista monitorowanych składników oraz ich bieżący stan kondycji. Widok diagramu wizualnie przedstawia model usługi aplikacji.

- **Raporty** umożliwiają podsumowywanie danych historycznych przechowywanych w magazynie danych Operations Manager. Można dostosować dane, na których bazują widoki i raporty. Nie istnieje jednak możliwość zezwalania na złożoną lub interaktywną analizę zebranych danych.

- **Operations Manager powłokę poleceń**, która rozszerza program Windows PowerShell z dodatkowym zestawem poleceń cmdlet, może wysyłać zapytania i wizualizować zebrane dane. Obejmuje to wykresy i inne wizualizacje, natywnie przy użyciu programu PowerShell lub za pomocą konsoli sieci Web Operations Manager opartej na języku HTML.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor ma wydajny aparat analityczny, który pozwala interaktywnie współpracować z danymi dzienników i połączyć je z innymi danymi monitorowania w celu uzyskania trendu i analizy danych. Widoki i pulpity nawigacyjne pozwalają wizualizować dane zapytań na różne sposoby z Azure Portal i importować do Power BI. Rozwiązania do monitorowania obejmują zapytania i widoki umożliwiające prezentowanie zbieranych danych. Szczegółowe informacje, takie jak Application Insights, Azure Monitor dla maszyn wirtualnych i Azure Monitor dla kontenerów obejmują dostosowane wizualizacje obsługujące interaktywne scenariusze monitorowania.

## <a name="alerting"></a>Generowanie alertów

### <a name="operations-manager"></a>Operations Manager

Operations Manager tworzy alerty w odpowiedzi na zdarzenia wstępnie zdefiniowane, po spełnieniu progu wydajności oraz o zmianie stanu kondycji monitorowanego składnika. Obejmuje ono pełne zarządzanie alertami, co pozwala na ustawienie ich rozdzielczości i przypisanie ich do różnych operatorów lub inżynierów systemów. Można ustawić reguły powiadomień, które określają, które alerty będą wysyłać aktywne powiadomienia.

Pakiety administracyjne zawierają różne wstępnie zdefiniowane reguły alertów dla różnych warunków krytycznych w monitorowanej aplikacji. Można dostosować te reguły lub utworzyć niestandardowe reguły do określonych wymagań środowiska.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor umożliwia tworzenie alertów na podstawie metryki przekraczającej próg lub na podstawie zaplanowanego wyniku zapytania. Alerty oparte na metrykach mogą osiągać wyniki niemal w czasie rzeczywistym, podczas gdy zaplanowane zapytania mają dłuższy czas odpowiedzi, w zależności od szybkości pozyskiwania i indeksowania danych. Zamiast ograniczać się do określonego agenta, alerty zapytań dzienników w Azure Monitor umożliwiają analizowanie danych między wszystkimi danymi przechowywanymi w wielu obszarach roboczych. Te alerty obejmują również dane z konkretnej aplikacji Application Insights przy użyciu zapytania między obszarami roboczymi.

Chociaż rozwiązania monitorujące mogą obejmować reguły alertów, zwykle są one tworzone na podstawie własnych wymagań.

## <a name="workflows"></a>Workflows

### <a name="operations-manager"></a>Operations Manager

Pakiety administracyjne w Operations Manager zawierają setki poszczególnych przepływów pracy i określają, jakie dane mają być zbierane i jakie działania należy wykonać w przypadku tych danych. Na przykład reguła może próbkować licznik wydajności co kilka minut, przechowując jego wyniki na potrzeby analizy. Monitor może próbkować ten sam licznik wydajności i porównać jego wartość z progiem w celu określenia stanu kondycji monitorowanego obiektu. Inna reguła może uruchomić skrypt w celu zebrania i przeanalizowania niektórych danych na komputerze agenta i wyzwolenia alertu, jeśli zwróci konkretną wartość.

Przepływy pracy w Operations Manager są niezależne od siebie, więc Analiza wielu monitorowanych obiektów jest trudna. Te scenariusze monitorowania muszą opierać się na danych po ich zebraniu, które są możliwe, ale mogą być trudne i nie są wspólne.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor oddziela zbieranie danych od akcji i analizy wykonanych z tych danych. Agenci i inne źródła danych zapisują dane dziennika do obszaru roboczego Log Analytics i dane metryki do bazy danych metryk, bez żadnej analizy tych danych lub wiedzą, jak mogą one być używane. Monitor wykonuje alerty i inne akcje z przechowywanych danych, co pozwala na wykonywanie analiz między danymi ze wszystkich źródeł.

## <a name="extending-base-platform"></a>Rozszerzanie platformy podstawowej

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementuje wszystkie logiki monitorowania w pakiecie administracyjnym, który można utworzyć samodzielnie lub uzyskać od nas lub do partnera. Podczas instalowania pakietu administracyjnego program automatycznie odnajduje składniki aplikacji lub usługi w różnych agentach i wdraża odpowiednie zasady i monitory. Pakiet administracyjny zawiera definicje kondycji, reguły alertów, reguły zbierania danych o wydajności i zdarzeń oraz widoki, które zapewniają pełne monitorowanie obsługujące usługę lub aplikację infrastruktury.

Zestaw SDK Operations Manager umożliwia Operations Manager integrację z platformami monitorowania innych firm lub oprogramowaniem narzędzia ITSM. Zestaw SDK jest również używany przez niektóre pakiety administracyjne partnerów do obsługi monitorowania urządzeń sieciowych i zapewniania niestandardowych środowisk prezentacji, takich jak kwadratowy pulpit nawigacyjny HTML5 lub integracja z programem Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor zbiera metryki i dzienniki z zasobów platformy Azure, z niewielką konfiguracją. Rozwiązania monitorujące dodają logikę do monitorowania aplikacji lub usługi, ale nadal pracują w standardowych kwerendach dzienników i widokach w monitorze. Szczegółowe informacje, takie jak Application Insights i Azure Monitor dla maszyn wirtualnych, wykorzystują platformę monitorowania do zbierania i przetwarzania danych, a także udostępniają dodatkowe narzędzia do wizualizacji i analizowania danych. Dane zbierane przez usługi Insights można łączyć z innymi danymi przy użyciu podstawowych funkcji monitorowania, takich jak kwerendy dzienników i alerty.

Monitor obsługuje kilka metod zbierania danych monitorowania lub zarządzania z platformy Azure lub zasobów zewnętrznych. Następnie można wyodrębnić i przesłać dane z zasobów metrycznych lub dzienników do narzędzi Narzędzia ITSM lub monitorowania albo wykonać zadania administracyjne za pomocą interfejsu API REST Azure Monitor.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Monitorowanie modeli wdrażania w chmurze](./cloud-models-monitor-overview.md)
