---
title: Sieci obwodowe
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak efektywnie skonfigurować platformę Azure dla swojej organizacji.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
ms.custom: virtual-network
ms.openlocfilehash: 889a524c26b06a3252dc84d9fa36426cdc07b88c
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223358"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs WAFs -->

# <a name="perimeter-networks"></a>Sieci obwodowe

[Sieci obwodowe][perimeter-network] umożliwiają bezpieczną łączność między sieciami w chmurze i sieciami w środowisku lokalnym lub w fizycznym centrum danych, wraz z wychodzącymi i przychodzącymi połączeniami internetowymi. Są one również nazywane strefami zdemilitaryzowanymi (DMZ).

Aby sieci obwodowe działały prawidłowo, pakiety przychodzące, zanim nawiążą połączenie z serwerami wewnętrznej bazy danych, muszą przechodzić przez urządzenia zabezpieczające hostowane w bezpiecznych podsieciach. Przykłady to zapora, systemy wykrywania intruzów i systemy zapobiegania włamaniom. Przed opuszczeniem sieci pakiety z obciążeń powiązane z Internetem powinny również przejść przez urządzenia zabezpieczające w sieci obwodowej. Przepływ ten ma na celu wymuszanie zasad, kontrolę i inspekcję.

Sieci obwodowe korzystają z następujących funkcji i usług platformy Azure:

- [Sieci wirtualne][virtual-networks], [trasy definiowane przez użytkownika][user-defined-routes] oraz [sieciowe grupy zabezpieczeń][network-security-groups]
- [Wirtualne urządzenia sieciowe (urządzeń WUS)][network-virtual-appliances]
- [Azure Load Balancer][alb]
- [Azure Application Gateway][appgw] i [Zapora aplikacji sieci Web (WAF)][appgwwaf]
- [Publiczne adresy IP][PIP]
- [Usługa frontonu platformy Azure][afd] z [zaporą aplikacji sieci Web][afdwaf]
- [Azure Firewall][Azure-firewall]

> [!NOTE]
> Architektury referencyjne platformy Azure udostępniają przykładowe szablony, których można używać do wdrażania własnych sieci obwodowych:
>
> - [Wdróż strefę DMZ między platformą Azure i lokalnym centrum danych](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)
> - [Wdróż strefę DMZ między platformą Azure i Internetem](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)

Zazwyczaj centralne zespoły IT i bezpieczeństwa są odpowiedzialne za określenie wymagań dotyczących obsługi sieci obwodowej.

![Przykład topologii sieci gwiazdy i gwiazdy](../../_images/azure-best-practices/network-high-level-perimeter-networks.png)

Na powyższym diagramie przedstawiono przykładową [topologię sieci Hub i szprych](./hub-spoke-network-topology.md) , która implementuje wymuszanie dwóch obwodów z dostępem do Internetu i sieci lokalnej. Oba obwody znajdują się w koncentratorze DMZ. W centrum DMZ sieć obwodowa do Internetu może być skalowalna w górę w celu zapewnienia obsługi wielu przedsiębiorstw za pośrednictwem wielu Farm sieciowi i wystąpień zapory platformy Azure, które pomagają chronić sieci wirtualne szprych. Koncentrator umożliwia również w zależności od potrzeb łączność za pośrednictwem sieci VPN lub usługi Azure ExpressRoute.

## <a name="virtual-networks"></a>Sieci wirtualne

Sieci obwodowe są zwykle tworzone przy użyciu [sieci wirtualnej][virtual-networks] z wieloma podsieciami w celu hostowania różnych typów usług, które filtrują i sprawdzają ruch do lub z Internetu przy użyciu urządzeń WUS, zapór aplikacji internetowych oraz wystąpień usługi Azure App Gateway.

## <a name="user-defined-routes"></a>Trasy definiowane przez użytkownika

Korzystając z [tras zdefiniowanych przez użytkownika][user-defined-routes], klienci mogą wdrażać zapory, systemy wykrywania intruzów, systemy zapobiegania włamaniom i inne urządzenia wirtualne. Klienci mogą następnie kierować ruch sieciowy przez te urządzenia zabezpieczające w celu wymuszania zasad granicy zabezpieczeń, inspekcji i kontroli. Trasy definiowane przez użytkownika mogą być tworzone w celu zagwarantowania, że ruch będzie przechodzić przez określone niestandardowe maszyny wirtualne, urządzenia WUS i moduły równoważenia obciążenia.

W przykładzie sieci typu Hub i szprych gwarantujemy, że ruch generowany przez maszyny wirtualne znajdujące się w szprychie przechodzi przez poprawne urządzenia wirtualne w centrum, wymaga zdefiniowanej przez użytkownika trasy zdefiniowanej w podsieciach szprychy. Ta trasa ustawia adres IP frontonu wewnętrznego modułu równoważenia obciążenia w następnym przeskoku. Wewnętrzny moduł równoważenia obciążenia rozkłada ruch wewnętrzny na urządzenia wirtualne (pula wewnętrznej bazy danych modułu równoważenia obciążenia).

## <a name="azure-firewall"></a>Azure Firewall

[Zapora systemu Azure][Azure-firewall] to zarządzana usługa oparta na chmurze, która pomaga chronić zasoby Virtual Network platformy Azure. Jest to w pełni stanowa zapora zarządzana z wbudowaną wysoką dostępnością i możliwością nieograniczonego skalowania w chmurze. Możesz centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych.

Usługa Azure Firewall używa statycznego publicznego adresu IP do zasobów sieci wirtualnej. Umożliwia to zewnętrznym zaporom identyfikowanie ruchu pochodzącego z danej sieci wirtualnej. Usługa współpracuje z usługą Azure Monitor na potrzeby rejestrowania i analiz.

## <a name="network-virtual-appliances"></a>Wirtualne urządzenia sieciowe

Sieci obwodowe z dostępem do Internetu są zazwyczaj zarządzane za pomocą wystąpienia usługi Azure Firewall lub farmy zapór albo [zapór aplikacji internetowych][afdwaf].

Różne linie biznesowe często korzystają z wielu aplikacji sieci Web. Aplikacje internetowe często mają różne luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki. Zapora aplikacji sieci Web wykrywa ataki na aplikacje sieci Web (HTTP/S) bardziej szczegółowo niż w przypadku zapory ogólnej. W porównaniu z tradycyjną technologią stosowaną w przypadku zapór zapory aplikacji internetowych mają zestaw konkretnych funkcji chroniących wewnętrzne serwery internetowe przed zagrożeniami.

Wystąpienie zapory platformy Azure i [sieciowe urządzenie wirtualne] [urządzenie WUS] korzystają ze wspólnej płaszczyzny administracyjnej z zestawem reguł zabezpieczeń, aby pomóc w ochronie obciążeń hostowanych w szprychach i kontrolować dostęp do sieci lokalnych. Usługa Azure Firewall ma wbudowaną skalowalność, a zapory urządzeń WUS można skalować ręcznie za modułem równoważenia obciążenia.

Farma zapór ma zwykle mniej wyspecjalizowane oprogramowanie niż zapora aplikacji internetowej, ale obsługuje szerszy zakres aplikacji, aby filtrować i sprawdzać wszelkiego rodzaju ruch wychodzący i przychodzący. Jeśli używasz rozwiązania z urządzeniem WUS, możesz znaleźć i wdrożyć oprogramowanie z platformy Azure Marketplace.

Użyj jednego zestawu wystąpień usługi Azure Firewall (lub urządzeń WUS) dla ruchu pochodzącego z Internetu oraz innego zestawu dla ruchu pochodzącego z sieci lokalnej. Używanie tylko jednego zestawu zapór dla obu rodzajów ruchu stwarza zagrożenie dla bezpieczeństwa, ponieważ nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego. Używanie oddzielnych warstw zapory zmniejsza złożoność sprawdzania zasad zabezpieczeń i wyraźnie pokazuje, które reguły dotyczą którego przychodzącego żądania sieciowego.

## <a name="azure-load-balancer"></a>Azure Load Balancer

[Azure Load Balancer][alb] oferuje usługę (TCP/UDP) warstwy 4 o wysokiej dostępności, która może rozkładać ruch przychodzący między wystąpieniami usługi zdefiniowanymi w zestawie o zrównoważonym obciążeniu. Ruch wysyłany do modułu równoważenia obciążenia z punktów końcowych frontonu (punktów końcowych publicznego adresu IP lub punktów końcowych prywatnego adresu IP) można rozłożyć ponownie z użyciem translacji adresów lub bez w puli adresów IP wewnętrznej bazy danych (np. urządzeń WUS lub maszyn wirtualnych).

Usługa Azure Load Balancer może również sondować kondycję różnych wystąpień serwera. Jeśli wystąpienie nie zareaguje na sondę, moduł równoważenia obciążenia przestaje wysyłać ruch do wystąpienia o złej kondycji.

Przykładem użycia topologii sieci gwiazdy i satelity jest wdrożenie zewnętrznego modułu równoważenia obciążenia zarówno w centrum, jak i szprych. Na piaście moduł równoważenia obciążenia skutecznie kieruje ruch do usług na szprychach. W szprychach moduły równoważenia obciążenia zarządzają ruchem aplikacji.

## <a name="azure-front-door-service"></a>Azure Front Door Service

[Azure Front Door Service][afd] to wysoce dostępna i skalowalna platforma do przyspieszania aplikacji internetowych oraz globalny moduł równoważenia obciążenia HTTPS firmy Microsoft. Za pomocą usługi Azure Front Door Service można kompilować, obsługiwać i skalować dynamiczną aplikację internetową oraz zawartość statyczną. Działa w ponad 100 miejscach na granicy sieci globalnej firmy Microsoft.

Usługa Azure Front Door Service udostępnia aplikacji ujednoliconą regionalną/oznaczoną arazutomatyzację konserwacji, automatyzację BCDR, ujednolicone buforowanie informacji o kliencie/użytkowniku oraz szczegółowe informacje na temat usługi. Platforma oferuje wydajność, niezawodność i obsługę umów SLA. Oferuje ona również certyfikaty zgodności oraz podlegające inspekcji praktyki zabezpieczeń, które są opracowywane, obsługiwane i wspierane natywnie przez platformę Azure.

## <a name="azure-application-gateway"></a>Azure Application Gateway

[Usługa Azure Application Gateway][appgw] to dedykowane urządzenie wirtualne udostępniające zarządzany kontroler dostarczania aplikacji. Oferuje różne możliwości równoważenia obciążenia warstwy 7 dla Twojej aplikacji.

Usługa Azure Application Gateway pozwala zoptymalizować wydajność kolektywu serwerów sieci Web, przenosząc do bramy aplikacji czasochłonne zakończenie protokołu SSL. Zapewnia także inne możliwości routingu warstwy 7, w tym rozkład okrężny ruchu przychodzącego, koligację sesji na podstawie plików cookie, routing oparty na ścieżkach URL i możliwość hostowania wielu witryn sieci Web za pojedynczą bramą aplikacji.

Jednostka SKU usługi Azure Application Gateway WAF obejmuje zaporę aplikacji sieci Web. Zapewnia ona ochronę aplikacji internetowych przed typowymi internetowymi lukami w zabezpieczeniach. Usługę Azure Application Gateway można skonfigurować jako bramę internetową, bramę tylko wewnętrzną lub kombinację obu tych usług.

## <a name="public-ips"></a>Publiczne adresy IP

W przypadku niektórych funkcji platformy Azure można skojarzyć punkty końcowe usługi z [publicznym adresem IP][PIP], aby można było uzyskać dostęp do zasobu z Internetu. Ten punkt końcowy używa translacji adresów sieciowych (NAT) do kierowania ruchu do wewnętrznego adresu i portu w usłudze Azure Virtual Network. Ta ścieżka stanowi podstawową metodę przekazywania ruchu zewnętrznego do sieci wirtualnej. Można skonfigurować publiczne adresy IP, aby określić, jaki ruch będzie przepuszczany, oraz w jaki sposób i gdzie będzie przekładany na sieć wirtualną.

## <a name="azure-ddos-protection-standard"></a>Usługa Azure DDoS Protection w warstwie Standardowa

Usługa [Azure DDoS Protection Standard][DDoS] zapewnia dodatkowe możliwości ograniczania funkcjonalności w ramach [podstawowej warstwy usług][DDoS] , która jest dostrajana specjalnie do zasobów usługi Azure Virtual Network. Standard DDoS Protection jest prosty do włączenia i nie wymaga żadnych zmian w aplikacji.

Zasady ochrony można dostosowywać przy użyciu dedykowanego monitorowania ruchu i algorytmów uczenia maszynowego. Zasady są stosowane do publicznych adresów IP skojarzonych z zasobami wdrożonymi w sieciach wirtualnych. Do tych zasobów należą m.in. wystąpienia usług Azure Load Balancer, Azure Application Gateway i Azure Service Fabric.

Dane telemetryczne w czasie rzeczywistym są dostępne w widokach usługi Azure Monitor zarówno podczas ataku, jak i w celach historycznych. Ochronę warstwy aplikacji można dodać przy użyciu zapory aplikacji sieci Web w usłudze Azure Application Gateway. Zapewniono ochronę publicznych adresów IP platformy Azure z protokołem IPv4.

<!-- links -->

[Virtual-networks]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[Network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[User-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[Network-virtual-appliances]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[Azure-firewall]: https://docs.microsoft.com/azure/firewall/overview
[Perimeter-network]: https://docs.microsoft.com/azure/best-practices-network-security
[Alb]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[Afd]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[Afdwaf]: https://docs.microsoft.com/azure/frontdoor/waf-overview
[Appgw]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[Appgwwaf]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
