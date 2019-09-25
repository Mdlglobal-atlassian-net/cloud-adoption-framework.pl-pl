---
title: Przewodnik monitorowania w chmurze — strategia monitorowania dla modeli wdrożenia w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Określ, kiedy używać Azure Monitor lub System Center Operations Manager w Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: badf03f3616de8e6612221282aa24996f0b6e8f8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221134"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Przewodnik monitorowania chmury: Strategia monitorowania dla modeli wdrożenia w chmurze

Ten artykuł zawiera naszą zalecaną strategię monitorowania dla każdego z modeli wdrożenia w chmurze, w oparciu o następujące kryteria:

- Wymagane jest kontynuowanie zobowiązania do Operations Manager lub innej platformy monitorowania przedsiębiorstwa. Jest to spowodowane integracją z procesami operacji IT, wiedzą i wiedzą lub bez względu na to, że niektóre funkcje nie są jeszcze dostępne w Azure Monitor.
- Musisz monitorować obciążenia zarówno lokalnie, jak i w chmurze publicznej lub tylko w chmurze.
- Twoja strategia migracji do chmury obejmuje modernizację operacji IT i przejście do naszych rozwiązań i usług monitorowania w chmurze.
- Być może masz krytyczne systemy, które są gapped powietrze lub fizycznie izolowane, hostowane w chmurze prywatnej lub na sprzęcie fizycznym i muszą być monitorowane.

Nasza strategia obejmuje obsługę infrastruktury monitorowania (obciążeń obliczeniowych, magazynowania i serwera), aplikacji (użytkowników końcowych, wyjątków i klienta) oraz zasobów sieciowych w celu zapewnienia kompletnej, zorientowanej na usługę perspektywy monitorowania.

## <a name="azure-cloud-monitoring"></a>Monitorowanie w chmurze platformy Azure

Usługa Azure Monitor to usługa platformy, która zapewnia jedno źródło monitorowania zasobów systemu Azure. Jest ona przeznaczona dla rozwiązań w chmurze, które są oparte na platformie Azure, i obsługują możliwość biznesową opartą na obciążeniach maszyn wirtualnych lub złożonych architekturach, które korzystają z mikrousług i innych zasobów platformy. Monitoruje wszystkie warstwy stosu, rozpoczynając od usług dzierżawców, takich jak Azure Active Directory Domain Services, oraz zdarzeń na poziomie subskrypcji i usługi Azure Service Health. Służy również do monitorowania zasobów infrastruktury, takich jak maszyny wirtualne, magazyn i zasoby sieciowe, i w górnej warstwie aplikacji. Monitorowanie każdej z tych zależności i zbieranie właściwych sygnałów, które mogą emitować każdy z nich, zapewnia wgląd w aplikacje i potrzebną infrastrukturę kluczy.

Poniższa tabela zawiera podsumowanie zalecanego podejścia do monitorowania każdej warstwy stosu.

<!-- markdownlint-disable MD033 -->

Warstwa | Resource | Scope | Metoda
---|---|---|----
Aplikacja | Aplikacja oparta na sieci Web działająca na platformie .NET, .NET Core, Java, JavaScript i Node. js na maszynie wirtualnej platformy Azure, na platformie Azure App Services, na platformie Azure Service Fabric, w Azure Functions i na platformie Azure Cloud Services | Monitoruj działającą aplikację sieci Web, aby automatycznie wykrywać anomalie wydajności, identyfikować wyjątki i problemy z kodem oraz zbierać dane telemetryczne. |  Application Insights
Containers | Usługa Azure Kubernetes/Azure Container Instances | Monitoruj wydajność, dostępność i wydajność obciążeń działających w kontenerach i wystąpieniach kontenerów. | Usługa Azure Monitor dla kontenerów
System operacyjny gościa | System operacyjny Linux i Windows | Monitoruj wydajność, dostępność i wydajność. Zależności mapy hostowane na poszczególnych maszynach wirtualnych, w tym widoczność aktywnych połączeń sieciowych między serwerami, opóźnienie połączeń przychodzących i wychodzących oraz porty w dowolnej architekturze połączonej z protokołem TCP. | Usługa Azure Monitor dla maszyn wirtualnych
Zasoby platformy Azure — PaaS | Usługi Azure Database Services (na przykład SQL lub mySQL) | Metryki wydajności usługi Azure Database for SQL. | Włącz rejestrowanie diagnostyczne w celu przesyłania strumieniowego danych SQL do dzienników Azure Monitor.
Zasoby platformy Azure — IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. W usłudze Azure Key Vault<br/> 4. Grupy zabezpieczeń sieci<br/> 5. Azure Traffic Manager | 1. Pojemność, dostępność i wydajność.<br/> 2. Dzienniki wydajności i diagnostyki (aktywność, dostęp, wydajność i Zapora).<br/> 3. Monitoruj sposób i czas uzyskiwania dostępu do Twoich magazynów kluczy oraz przez kogo.<br/> 4. Monitoruj zdarzenia, gdy reguły są stosowane, oraz licznik reguł dla tego, ile razy reguła została zastosowana do odmowy lub zezwolenia.<br/>5. Monitoruj dostępność stanu punktu końcowego. | 1. Metryki magazynu dla usługi BLOB Storage.<br/> 2. Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 3. Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor, a następnie Włącz [rozwiązanie Azure Key Vault Analytics](https://docs.microsoft.com/azure/azure-monitor/insights/azure-key-vault). <br/> 4. Włącz rejestrowanie diagnostyczne grup zabezpieczeń sieci i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.<br/> 5. Włącz rejestrowanie diagnostyczne dla punktów końcowych Traffic Manager i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.
Sieć| Komunikacja między maszyną wirtualną i jednym lub wieloma punktami końcowymi (inna maszyna wirtualna, w pełni kwalifikowana nazwa domeny, jednolity identyfikator zasobu lub adres IPv4). | Monitoruj zmiany, opóźnienia i topologię sieci między maszyną wirtualną a punktem końcowym. | Azure Network Watcher
Subskrypcja platformy Azure | Kondycja usługi platformy Azure i podstawowa Kondycja zasobów | <li> Akcje administracyjne wykonywane w ramach usługi lub zasobu.<br/><li> Kondycja usługi w ramach usługi platformy Azure jest w stanie obniżonej lub niedostępności.<br/><li> Wykryto problemy z kondycją w ramach zasobu platformy Azure z perspektywy usługi platformy Azure.<br/><li> Operacje wykonywane przy użyciu automatycznego skalowania platformy Azure wskazujące awarię lub wyjątek. <br/><li> Operacje wykonywane z Azure Policy wskazujące, że wystąpiła dozwolona lub odmowa akcja.<br/><li> Rekord alertów generowanych przez Azure Security Center. |Dostarczana w dzienniku aktywności do monitorowania i wysyłania alertów za pomocą Azure Resource Manager.
Dzierżawa platformy Azure|Usługa Azure Active Directory || Włącz rejestrowanie diagnostyczne i skonfiguruj przesyłanie strumieniowe do dzienników Azure Monitor.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Monitorowanie chmury hybrydowej

Ta sekcja jest obecnie opracowywana w celu dostarczenia kompleksowego zestawu zaleceń, które wiążą Cię z Twoim modelem chmury i wkrótce zostaną udostępnione.  

## <a name="private-cloud-monitoring"></a>Monitorowanie chmury prywatnej

Można osiągnąć całościowe monitorowanie Azure Stack z System Center Operations Manager. W celu monitorowania obciążeń uruchomionych w ramach dzierżawy, poziomu zasobów na maszynach wirtualnych oraz Azure Stack hostingu infrastruktury (serwery fizyczne i przełączniki sieciowe). Możesz również uzyskać całościowe monitorowanie z użyciem kombinacji [możliwości monitorowania infrastruktury](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) zawartej w Azure Stack. Te funkcje ułatwiają wyświetlanie kondycji i alertów dla regionu Azure Stack i [usługi Azure monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) w Azure Stack, która zapewnia metryki infrastruktury i dzienniki na poziomie podstawowym dla większości usług.

Jeśli zainwestowano już w Operations Manager, Użyj pakietu administracyjnego Azure Stack do monitorowania stanu dostępności i kondycji Azure Stack wdrożeń. Obejmuje to regiony, dostawcy zasobów, aktualizacje, przebiegi aktualizacji, jednostki skalowania, węzły jednostek, role infrastruktury i ich wystąpienia (jednostki logiczne składają się z zasobów sprzętowych). Używa ona interfejsów API REST i aktualizacji dostawcy zasobów, aby komunikować się z Azure Stack. Aby monitorować serwery fizyczne i urządzenia magazynujące, należy użyć pakietu administracyjnego dostawcy OEM (na przykład dostarczonego przez firmę Lenovo, Hewlett Packard lub Dell). Operations Manager może natywnie monitorować przełączniki sieciowe w celu zbierania podstawowych statystyk przy użyciu protokołu SNMP. Monitorowanie obciążeń dzierżawców jest możliwe z pakietem administracyjnym platformy Azure, wykonując dwa podstawowe kroki. Skonfiguruj subskrypcję, którą chcesz monitorować, a następnie Dodaj monitory dla tej subskrypcji.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Zbieranie właściwych danych](./data-collection.md)
