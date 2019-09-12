---
title: Sieci obwodowe
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Sieci obwodowe
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: cf5b641bb894c9784f01e4e9eaae545b6b38a30d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828541"
---
# <a name="perimeter-networks"></a>Sieci obwodowe

[Sieci obwodowe][perimeter-network] umożliwiają bezpieczną łączność między sieciami w chmurze i sieciami w środowisku lokalnym lub w fizycznym centrum danych, wraz z wychodzącymi i przychodzącymi połączeniami internetowymi. Są one również nazywane strefami zdemilitaryzowanymi (DMZ).

Aby sieci obwodowe działały prawidłowo, pakiety przychodzące, zanim nawiążą połączenie z serwerami wewnętrznej bazy danych, muszą przechodzić przez urządzenia zabezpieczające hostowane w bezpiecznych podsieciach. Można do nich zaliczyć m.in. zaporę, system wykrywania nieautoryzowanego dostępu (IDS) oraz systemy ochrony przed intruzami (IPS). Przed opuszczeniem sieci pakiety z obciążeń powiązane z Internetem powinny również przejść przez urządzenia zabezpieczające w sieci obwodowej. Przepływ ten ma na celu wymuszanie zasad, kontrolę i inspekcję.

Sieci obwodowe korzystają z następujących funkcji i usług platformy Azure:

- [Sieci wirtualne][virtual-networks], [trasy definiowane przez użytkownika][user-defined-routes] oraz [sieciowe grupy zabezpieczeń][network-security-groups]
- [Sieciowe urządzenia wirtualne][NVA] (NVA)
- [Azure Load Balancer][ALB]
- [Usługa Azure Application Gateway][AppGW] i [zapora aplikacji internetowej][AppGWWAF] (WAF)
- [Publiczne adresy IP][PIP]
- [Usługa Azure Front Door][AFD] z [zaporą aplikacji internetowej][AFDWAF]
- [Azure Firewall][AzFW]

> [!NOTE]
> Architektury referencyjne platformy Azure udostępniają przykładowe szablony, których można używać do wdrażania własnych sieci obwodowych:
>
> - [Wdróż strefę DMZ między platformą Azure i lokalnym centrum danych](/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)
> - [Wdróż strefę DMZ między platformą Azure i Internetem](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)

Zazwyczaj centralne zespoły IT oraz zespoły ds. bezpieczeństwa są odpowiedzialne za określenie wymagań dotyczących obsługi sieci obwodowych.

![Przykładowa sieć piasty i szprych (typu gwiazda)][7]

Na diagramie powyżej przedstawiono przykładową [sieć piasty i szprych](./hub-spoke-network-topology.md), która wdraża wymuszanie dwóch obwodów z dostępem do Internetu i sieci lokalnej. Oba obwody znajdują się w koncentratorze DMZ. W koncentratorze DMZ sieć obwodowa połączona z Internetem może skalować w górę w celu zapewnienia obsługi wielu aplikacji biznesowych (LOB), korzystając z wielu farm zapór aplikacji internetowych oraz wystąpień usługi Azure Firewall, które pomagają chronić sieci wirtualne szprych. Koncentrator umożliwia również w zależności od potrzeb łączność za pośrednictwem sieci VPN lub usługi Azure ExpressRoute.

## <a name="virtual-networks"></a>Sieci wirtualne

Sieci obwodowe są zwykle tworzone przy użyciu [sieci wirtualnej][virtual-networks] z wieloma podsieciami w celu hostowania różnych typów usług, które filtrują i sprawdzają ruch do lub z Internetu przy użyciu urządzeń WUS, zapór aplikacji internetowych oraz wystąpień usługi Azure App Gateway.

## <a name="user-defined-routes"></a>Trasy definiowane przez użytkownika

Korzystając z [tras definiowanych przez użytkownika][user-defined-routes], klienci mogą wdrażać zapory, systemy wykrywania nieautoryzowanego dostępu/adresy IP oraz inne urządzenia wirtualne. Klienci mogą następnie kierować ruch sieciowy przez te urządzenia zabezpieczające w celu wymuszania zasad granicy zabezpieczeń, inspekcji i kontroli. Trasy definiowane przez użytkownika mogą być tworzone w celu zagwarantowania, że ruch będzie przechodzić przez określone niestandardowe maszyny wirtualne, urządzenia WUS i moduły równoważenia obciążenia.

W przykładzie sieci piasty i szprych zagwarantowanie, że ruch generowany przez maszyny wirtualne znajdujące się w szprysze przechodzi przez poprawne urządzenia wirtualne w koncentratorze, wymaga trasy definiowanej przez użytkownika definiowanej w podsieciach szprychy. Ta trasa ustawia adres IP frontonu wewnętrznego modułu równoważenia obciążenia w następnym przeskoku. Wewnętrzny moduł równoważenia obciążenia rozkłada ruch wewnętrzny na urządzenia wirtualne (pula wewnętrznej bazy danych modułu równoważenia obciążenia).

## <a name="azure-firewall"></a>Azure Firewall

[Azure Firewall][AzFW] to zarządzana usługa oparta na chmurze, która chroni zasoby sieci wirtualnej platformy Azure. Jest to w pełni stanowa zapora zarządzana z wbudowaną wysoką dostępnością i możliwością nieograniczonego skalowania w chmurze. Możesz centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych.

Usługa Azure Firewall używa statycznego publicznego adresu IP do zasobów sieci wirtualnej. Umożliwia to zewnętrznym zaporom identyfikowanie ruchu pochodzącego z danej sieci wirtualnej. Usługa współpracuje z usługą Azure Monitor na potrzeby rejestrowania i analiz.

## <a name="network-virtual-appliances"></a>Wirtualne urządzenia sieciowe

Sieci obwodowe z dostępem do Internetu są zazwyczaj zarządzane za pomocą wystąpienia usługi Azure Firewall lub farmy zapór albo [zapór aplikacji internetowych][AFDWAF].

Różne aplikacje biznesowe często używają wielu aplikacji internetowych. Aplikacje internetowe często mają różne luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki. Zapora aplikacji internetowej wykrywa ataki na aplikacje internetowe (HTTP/HTTPS) bardziej szczegółowo niż zapora ogólna. W porównaniu z tradycyjną technologią stosowaną w przypadku zapór zapory aplikacji internetowych mają zestaw konkretnych funkcji chroniących wewnętrzne serwery internetowe przed zagrożeniami.

Wystąpienie usługi Azure Firewall oraz zapora [wirtualnego urządzenia sieciowego][NVA] korzystają ze wspólnej płaszczyzny administracyjnej oraz zestawu reguł zabezpieczeń, który chroni obciążenia hostowane w szprychach oraz pomaga kontrolować dostęp do sieci lokalnych. Usługa Azure Firewall ma wbudowaną skalowalność, a zapory urządzeń WUS można skalować ręcznie za modułem równoważenia obciążenia.

Farma zapór ma zwykle mniej wyspecjalizowane oprogramowanie niż zapora aplikacji internetowej, ale obsługuje szerszy zakres aplikacji, aby filtrować i sprawdzać wszelkiego rodzaju ruch wychodzący i przychodzący. Jeśli używasz rozwiązania z urządzeniem WUS, możesz znaleźć i wdrożyć oprogramowanie z platformy Azure Marketplace.

Użyj jednego zestawu wystąpień usługi Azure Firewall (lub urządzeń WUS) dla ruchu pochodzącego z Internetu oraz innego zestawu dla ruchu pochodzącego z sieci lokalnej. Używanie tylko jednego zestawu zapór dla obu rodzajów ruchu stwarza zagrożenie dla bezpieczeństwa, ponieważ nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego. Używanie oddzielnych warstw zapory zmniejsza złożoność sprawdzania zasad zabezpieczeń i wyraźnie pokazuje, które reguły dotyczą którego przychodzącego żądania sieciowego.

## <a name="azure-load-balancer"></a>Azure Load Balancer

[Azure Load Balancer][ALB] oferuje usługę (TCP/UDP) warstwy 4 o wysokiej dostępności, która może rozkładać ruch przychodzący między wystąpieniami usługi zdefiniowanymi w zestawie o zrównoważonym obciążeniu. Ruch wysyłany do modułu równoważenia obciążenia z punktów końcowych frontonu (punktów końcowych publicznego adresu IP lub punktów końcowych prywatnego adresu IP) można rozłożyć ponownie z użyciem translacji adresów lub bez w puli adresów IP wewnętrznej bazy danych (np. urządzeń WUS lub maszyn wirtualnych).

Usługa Azure Load Balancer może również sondować kondycję różnych wystąpień serwera. Jeśli wystąpienie nie zareaguje na sondę, moduł równoważenia obciążenia przestaje wysyłać ruch do wystąpienia o złej kondycji.

Przykładem użycia sieci piasty i szprych (topologii gwiazdy) może być wdrożenie zewnętrznego modułu równoważenia obciążenia zarówno na piaście, jak i na szprychach. Na piaście moduł równoważenia obciążenia skutecznie kieruje ruch do usług na szprychach. W szprychach moduły równoważenia obciążenia zarządzają ruchem aplikacji.

## <a name="azure-front-door-service"></a>Azure Front Door Service

[Azure Front Door Service][AFD] to wysoce dostępna i skalowalna platforma do przyspieszania aplikacji internetowych oraz globalny moduł równoważenia obciążenia HTTPS firmy Microsoft. Za pomocą usługi Azure Front Door Service można kompilować, obsługiwać i skalować dynamiczną aplikację internetową oraz zawartość statyczną. Działa w ponad 100 miejscach na granicy sieci globalnej firmy Microsoft.

Usługa Azure Front Door Service udostępnia aplikacji ujednoliconą regionalną/oznaczoną arazutomatyzację konserwacji, automatyzację BCDR, ujednolicone buforowanie informacji o kliencie/użytkowniku oraz szczegółowe informacje na temat usługi. Platforma oferuje wydajność, niezawodność i obsługę umów SLA. Oferuje ona również certyfikaty zgodności oraz podlegające inspekcji praktyki zabezpieczeń, które są opracowywane, obsługiwane i wspierane natywnie przez platformę Azure.

## <a name="application-gateway"></a>Application Gateway

Usługa [Azure Application Gateway][AppGW] to dedykowane urządzenie wirtualne udostępniające zarządzany kontroler dostarczania aplikacji (ADC, Application Delivery Controller). Oferuje różnorodne możliwości równoważenia obciążenia warstwy 7 dla Twojej aplikacji.

Usługa Application Gateway umożliwia optymalizowanie wydajności farmy sieci Web dzięki przeniesieniu obciążenia intensywnego przerywania połączenia SSL z procesora CPU do usługi Application Gateway. Zapewnia także inne możliwości routingu warstwy 7, takie jak okrężna dystrybucja ruchu przychodzącego, koligacja sesji na podstawie plików cookie, routing oparty na ścieżkach URL i możliwość hostowania wielu witryn sieci Web za pojedynczą bramą aplikacji.

Jednostka SKU zapory aplikacji internetowej bramy aplikacji obejmuje zaporę aplikacji internetowej. Zapewnia ona ochronę aplikacji internetowych przed typowymi internetowymi lukami w zabezpieczeniach. Usługę Application Gateway można skonfigurować jako bramę umożliwiającą dostęp do Internetu, bramę tylko wewnętrzną lub jako kombinację obu tych opcji.

## <a name="public-ips"></a>Publiczne adresy IP

W przypadku niektórych funkcji platformy Azure można skojarzyć punkty końcowe usługi z [publicznym adresem IP][PIP], aby można było uzyskać dostęp do zasobu z Internetu. Ten punkt końcowy używa translatora adresów sieciowych (NAT) do kierowania ruchu do wewnętrznego adresu i portu w sieci wirtualnej platformy Azure. Ta ścieżka stanowi podstawową metodę przekazywania ruchu zewnętrznego do sieci wirtualnej. Można skonfigurować publiczne adresy IP, aby określić, jaki ruch będzie przepuszczany, oraz w jaki sposób i gdzie będzie przekładany na sieć wirtualną.

## <a name="azure-ddos-protection-standard"></a>Usługa Azure DDoS Protection w warstwie Standardowa

Usługa [Azure DDoS Protection w warstwie Standardowa][DDoS] zapewnia dodatkowe możliwości ograniczania w warstwie [usług podstawowych][DDoS], które są dostosowane specjalnie do zasobów sieci wirtualnej platformy Azure. Usługa DDoS Protection w warstwie Standardowa jest prosta do włączenia i nie wymaga żadnych zmian w aplikacji.

Zasady ochrony można dostosowywać przy użyciu dedykowanego monitorowania ruchu i algorytmów uczenia maszynowego. Zasady są stosowane do publicznych adresów IP skojarzonych z zasobami wdrożonymi w sieciach wirtualnych. Do tych zasobów należą m.in. wystąpienia usług Azure Load Balancer, Azure Application Gateway i Azure Service Fabric.

Dane telemetryczne w czasie rzeczywistym są dostępne w widokach usługi Azure Monitor zarówno podczas ataku, jak i w celach historycznych. Ochronę warstwy aplikacji można dodać za pomocą zapory aplikacji internetowej w usłudze Azure Application Gateway. Zapewniono ochronę publicznych adresów IP platformy Azure z protokołem IPv4.

<!-- images -->

[0]: ./images/network-redundant-equipment.png "Przykłady nakładania się składników"
[1]: ./images/network-hub-spoke-high-level.png "Ogólny przykład piasty i szprych"
[2]: ./images/network-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ./images/network-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ./images/network-hub-spoke-block-level-diagram.png "Diagram poziomu bloku sieci piasty i szprych"
[5]: ./images/network-users-groups-subsciptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ./images/network-infrastructure-high-level.png "Ogólny diagram infrastruktury"
[7]: ./images/network-highlevel-perimeter-networks.png "Diagram infrastruktury wysokiego poziomu"
[8]: ./images/network-vnet-peering-perimeter-neworks.png "Wirtualne sieci równorzędne i sieci obwodowe"
[9]: ./images/network-high-level-diagram-monitoring.png "Diagram wysokiego poziomu na potrzeby monitorowania"
[10]: ./images/network-high-level-workloads.png "Diagram wysokiego poziomu na potrzeby obciążenia"

<!-- links -->

[Limits]: /azure/azure-subscription-service-limits
[Roles]: /azure/role-based-access-control/built-in-roles
[virtual-networks]: /azure/virtual-network/virtual-networks-overview
[network-security-groups]: /azure/virtual-network/virtual-networks-nsg
[DNS]: /azure/dns/dns-overview
[PrivateDNS]: /azure/dns/private-dns-overview
[VNetPeering]: /azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: /azure/virtual-network/virtual-networks-udr-overview
[RBAC]: /azure/role-based-access-control/overview
[azure-ad]: /azure/active-directory/active-directory-whatis
[VPN]: /azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: /azure/expressroute/expressroute-introduction
[ExRD]: /azure/expressroute/expressroute-erdirect-about
[vWAN]: /azure/virtual-wan/virtual-wan-about
[NVA]: /azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: /azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: /azure/azure-resource-manager/resource-group-overview
[perimeter-network]: /azure/best-practices-network-security
[ALB]: /azure/load-balancer/load-balancer-overview
[DDoS]: /azure/virtual-network/ddos-protection-overview
[PIP]: /azure/virtual-network/virtual-network-public-ip-address
[AFD]: /azure/frontdoor/front-door-overview
[AFDWAF]: /azure/frontdoor/waf-overview
[AppGW]: /azure/application-gateway/application-gateway-introduction
[AppGWWAF]: /azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: /azure/monitoring-and-diagnostics/
[ActLog]: /azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: /azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: /azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: /azure/operations-management-suite/operations-management-suite-overview
[NPM]: /azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: /azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: /azure/app-service/
[HDI]: /azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: /azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: /azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: /azure/traffic-manager/traffic-manager-overview
