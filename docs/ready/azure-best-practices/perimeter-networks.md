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
ms.openlocfilehash: 92aa03c07a6652f15a0400a025b8911a4d0d07dd
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240174"
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
> - [Wdróż strefę DMZ między platformą Azure i lokalnym centrum danych](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid)
> - [Wdróż strefę DMZ między platformą Azure i Internetem](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)

Zazwyczaj centralne zespoły IT oraz zespoły ds. bezpieczeństwa są odpowiedzialne za określenie wymagań dotyczących obsługi sieci obwodowych.

![Przykład topologii sieci gwiazdy i gwiazdy][7]

Na powyższym diagramie przedstawiono przykładową [topologię sieci Hub i szprych](./hub-spoke-network-topology.md) , która implementuje wymuszanie dwóch obwodów z dostępem do Internetu i sieci lokalnej. Oba obwody znajdują się w koncentratorze DMZ. W koncentratorze DMZ sieć obwodowa połączona z Internetem może skalować w górę w celu zapewnienia obsługi wielu aplikacji biznesowych (LOB), korzystając z wielu farm zapór aplikacji internetowych oraz wystąpień usługi Azure Firewall, które pomagają chronić sieci wirtualne szprych. Koncentrator umożliwia również w zależności od potrzeb łączność za pośrednictwem sieci VPN lub usługi Azure ExpressRoute.

## <a name="virtual-networks"></a>Sieci wirtualne

Sieci obwodowe są zwykle tworzone przy użyciu [sieci wirtualnej][virtual-networks] z wieloma podsieciami w celu hostowania różnych typów usług, które filtrują i sprawdzają ruch do lub z Internetu przy użyciu urządzeń WUS, zapór aplikacji internetowych oraz wystąpień usługi Azure App Gateway.

## <a name="user-defined-routes"></a>Trasy definiowane przez użytkownika

Korzystając z [tras definiowanych przez użytkownika][user-defined-routes], klienci mogą wdrażać zapory, systemy wykrywania nieautoryzowanego dostępu/adresy IP oraz inne urządzenia wirtualne. Klienci mogą następnie kierować ruch sieciowy przez te urządzenia zabezpieczające w celu wymuszania zasad granicy zabezpieczeń, inspekcji i kontroli. Trasy definiowane przez użytkownika mogą być tworzone w celu zagwarantowania, że ruch będzie przechodzić przez określone niestandardowe maszyny wirtualne, urządzenia WUS i moduły równoważenia obciążenia.

W przykładzie sieci typu Hub i szprych gwarantujemy, że ruch generowany przez maszyny wirtualne znajdujące się w szprychie przechodzi przez poprawne urządzenia wirtualne w centrum, wymaga zdefiniowanej przez użytkownika trasy zdefiniowanej w podsieciach szprychy. Ta trasa ustawia adres IP frontonu wewnętrznego modułu równoważenia obciążenia w następnym przeskoku. Wewnętrzny moduł równoważenia obciążenia rozkłada ruch wewnętrzny na urządzenia wirtualne (pula wewnętrznej bazy danych modułu równoważenia obciążenia).

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

Przykładem użycia topologii sieci gwiazdy i satelity jest wdrożenie zewnętrznego modułu równoważenia obciążenia zarówno w centrum, jak i szprych. Na piaście moduł równoważenia obciążenia skutecznie kieruje ruch do usług na szprychach. W szprychach moduły równoważenia obciążenia zarządzają ruchem aplikacji.

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

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Przykłady nakładania się składników"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Ogólny przykład piasty i szprych"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Diagram poziomu bloku sieci piasty i szprych"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Diagram infrastruktury wysokiego poziomu"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Diagram infrastruktury wysokiego poziomu"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "Wirtualne sieci równorzędne i sieci obwodowe"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Diagram wysokiego poziomu na potrzeby monitorowania"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Diagram wysokiego poziomu na potrzeby obciążenia"

<!-- links -->

[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: https://docs.microsoft.com/azure/architecture/cloud-adoption/reference/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[AppGWWAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[Monitor]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[nsg-log]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[NPM]: https://docs.microsoft.com/azure/log-analytics/log-analytics-network-performance-monitor
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
