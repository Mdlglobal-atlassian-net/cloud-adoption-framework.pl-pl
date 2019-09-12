---
title: Topologia sieci piasty i szprych
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Topologia sieci piasty i szprych
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 48f73d7c7f2e7f3bba8183464c786a3e0744807c
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905489"
---
# <a name="hub-and-spoke-network-topology"></a>Topologia sieci piasty i szprych

*Piasta i szprychy* to model sieci umożliwiający bardziej efektywne zarządzanie typowymi wymaganiami dotyczącymi komunikacji i zabezpieczeń. Pomaga również uniknąć ograniczeń subskrypcji platformy Azure. Ten model dotyczy następujących kwestii:

- **Oszczędność kosztów i efektywność zarządzania**. Scentralizowanie w jednej lokalizacji usług, które mogą być współużytkowane przez wiele obciążeń, takich jak wirtualne urządzenia sieciowe (NVA) i serwery DNS, umożliwia działowi IT zminimalizowanie nadmiarowych zasobów i zadań związanych z zarządzaniem.
- **Pokonywanie ograniczeń subskrypcji**. Duże obciążenia oparte na chmurze mogą wymagać użycia większej ilości zasobów, niż jest to dozwolone w pojedynczej subskrypcji platformy Azure. (Zobacz [ograniczenia subskrypcji][Limits]). Komunikacja równorzędna sieci wirtualnych obciążenia z różnych subskrypcji do centrum może pokonać te ograniczenia.
- **Separacja problemów**. Poszczególne obciążenia można wdrożyć między centralnymi zespołami IT i zespołami obciążeń.

Dodatkowa struktura i możliwości oferowane przez ten model mogą nie przynieść korzyści mniejszym majątkom w chmurze. Jednak w przypadku większych nakładów pracy związanych z wdrożeniem chmury warto rozważyć implementację architektury sieciowej typu piasta i szprychy, jeśli występują problemy wymienione wcześniej.

> [!NOTE]
> Strona Architektury referencyjne platformy Azure zawiera przykładowe szablony, których można użyć jako podstawy do zaimplementowania własnych sieci piasty i szprych:
>
> - [Implementowanie topologii sieci piasty i szprych na platformie Azure](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementowanie topologii sieci piasty i szprych za pomocą usług udostępnionych na platformie Azure](/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Omówienie

![Przykłady topologii sieci piasty i szprych][1]

Jak pokazano na diagramie, platforma Azure obsługuje dwa typy projektów piasty i szprych. Obsługuje ona komunikację, zasoby udostępnione i scentralizowane zasady zabezpieczeń („centrum sieci wirtualnej” na diagramie) lub typ wirtualnej sieci WAN („wirtualna sieć WAN” na diagramie) na potrzeby wielkoskalowej komunikacji między oddziałami lub między oddziałem i platformą Azure.

Piasta to centralna strefa sieciowa, która kontroluje i sprawdza ruch przychodzący i wychodzący między strefami: Internet, środowisko lokalne i szprychy. Topologia piasty i szprych zapewnia działowi IT efektywną metodę wymuszania zasad zabezpieczeń w lokalizacji centralnej. Minimalizuje również ryzyko błędnej konfiguracji i ekspozycji.

Piasta zawiera często wspólne składniki usługi używane przez szprychy. Poniżej przedstawiono typowe usługi centralne:

- Infrastruktura usługi Active Directory systemu Windows Server, wymagana do uwierzytelniania użytkowników innych firm, którzy uzyskują dostęp z niezaufanych sieci przed uzyskaniem dostępu do obciążeń w szprysze. Obejmuje ona powiązane usługi Active Directory Federation Services (AD FS).
- Usługa DNS do rozpoznawania nazw obciążeń w szprychach, do uzyskiwania dostępu do zasobów lokalnych i w Internecie, jeśli usługa [Azure DNS][DNS] nie jest używana.
- Infrastruktura kluczy publicznych (PKI) do implementowania obciążeń logowania jednokrotnego.
- Kontrola przepływu ruchu TCP i UDP między strefami sieciowymi szprych i Internetem.
- Sterowanie przepływem między szprychami i środowiskiem lokalnym.
- W razie konieczności sterowanie przepływem między jedną szprychą a inną.

Używając infrastruktury piasty udostępnionej w celu obsługi wielu szprych, można zminimalizować nadmiarowość, uprościć zarządzanie i obniżyć koszt całkowity.

Rolą każdej szprychy może być hostowanie różnych typów obciążeń. Szprychy zapewniają również modularne podejście do powtarzających się wdrożeń tych samych obciążeń. Przykłady to programowanie i testowanie, testowanie akceptacji przez użytkowników, przygotowanie i produkcja.

Szprychy mogą również dzielić różne grupy w obrębie organizacji i umożliwiać ich tworzenie. Przykładem są grupy usługi Azure DevOps. Wewnątrz szprychy można wdrażać podstawowe obciążenia lub złożone obciążenia wielowarstwowe z kontrolą ruchu między warstwami.

## <a name="subscription-limits-and-multiple-hubs"></a>Ograniczenia subskrypcji i wiele piast

Na platformie Azure każdy składnik, niezależnie od typu, jest wdrażany w ramach subskrypcji platformy Azure. Izolacja składników platformy Azure w różnych subskrypcjach platformy Azure może spełniać różne wymagania biznesowe, takie jak konfigurowanie różnych poziomów dostępu i autoryzacji.

Pojedyncza implementacja piasty i szprych może być skalowana w górę do dużej liczby szprych. Jednak podobnie jak w przypadku każdego systemu informatycznego, istnieją ograniczenia platformy. Wdrożenie piasty jest powiązane z określoną subskrypcją platformy Azure, która ma ograniczenia i limity. (Przykładem może być maksymalna liczba komunikacji równorzędnych sieci wirtualnych. Zobacz [Limity, przydziały i ograniczenia usługi i subskrypcji platformy Azure][Limits], aby uzyskać szczegółowe informacje).

W przypadkach, gdy ograniczenia mogą stanowić problem, można skalować w górę architekturę, rozszerzając model z jednej piasty i szprych do klastra piast i szprych. Możesz połączyć wiele piast w jednym lub większej liczbie regionów świadczenia usługi Azure za pomocą komunikacji równorzędnej sieci wirtualnych, usługi Azure ExpressRoute, wirtualnej sieci WAN lub sieci VPN typu lokacja-lokacja.

![Klaster piast i szprych][2]

Wprowadzenie wielu piast zwiększa koszt i nakłady pracy związane z zarządzaniem w systemie. Jest to usprawiedliwione tylko skalowalnością, ograniczeniami systemu lub nadmiarowością i replikacją regionalną na potrzeby wydajności użytkownika lub odzyskiwania po awarii. W scenariuszach wymagających wielu piast wszystkie piasty powinny dążyć do oferowania tego samego zestawu usług w celu ułatwienia zadań operacyjnych.

## <a name="interconnection-between-spokes"></a>Wzajemne połączenia między szprychami

Istnieje możliwość zaimplementowania złożonych, wielowarstwowych obciążeń w obrębie jednej szprychy. Konfiguracje wielowarstwowe można implementować przy użyciu podsieci (jedna dla każdej warstwy) w tej samej sieci wirtualnej i przy użyciu sieciowych grup zabezpieczeń do filtrowania przepływów.

Architekt może chcieć wdrożyć obciążenie wielowarstwowe w wielu sieciach wirtualnych. Za pomocą komunikacji równorzędnej sieci wirtualnych szprychy mogą łączyć się z innymi szprychami w tej samej piaście lub w różnych piastach.

Typowym przykładem tego scenariusza jest przypadek, w którym serwery przetwarzania aplikacji znajdują się w jednej szprysze lub sieci wirtualnej. Baza danych jest wdrażana w innej szprysze lub sieci wirtualnej. W takim przypadku można łatwo połączyć szprychy za pomocą komunikacji równorzędnej sieci wirtualnych, aby uniknąć przesyłania danych przez piastę. Rozwiązaniem jest przeprowadzenie starannego przeglądu architektury i zabezpieczeń, aby upewnić się, że pominięcie piasty nie pomija ważnych punktów zabezpieczeń lub inspekcji, które mogą istnieć tylko w piaście.

![Szprychy połączone ze sobą i z piastą][3]

Szprychy mogą być również połączone ze szprychą, która pełni rolę piasty. Takie podejście tworzy hierarchię dwupoziomową: szprycha na wyższym poziomie (poziom 0) staje się piastą dla małych szprych (poziom 1) w hierarchii. Szprychy w implementacji piasty i szprych są wymagane do przekazywania ruchu do piasty centralnej, aby ruch mógł zostać przesłany do miejsca docelowego w sieci lokalnej lub w publicznym Internecie. Architektura z dwoma poziomami piast obejmuje złożony routing, który eliminuje zalety prostej relacji piasty i szprych.

<!-- images -->

[0]: ./images/network-redundant-equipment.png "Przykłady nakładania się składników"
[1]: ./images/network-hub-spoke-high-level.png "Ogólny przykład piasty i szprych"
[2]: ./images/network-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ./images/network-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ./images/network-hub-spoke-block-level-diagram.png "Diagram na poziomie bloku piasty i szprych"
[5]: ./images/network-users-groups-subsciptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ./images/network-infrastructure-high-level.png "Ogólny diagram infrastruktury"
[7]: ./images/network-highlevel-perimeter-networks.png "Ogólny diagram infrastruktury"
[8]: ./images/network-vnet-peering-perimeter-neworks.png "Komunikacja równorzędna sieci wirtualnych i sieci obwodowe"
[9]: ./images/network-high-level-diagram-monitoring.png "Ogólny diagram dla monitorowania"
[10]: ./images/network-high-level-workloads.png "Ogólny diagram dla obciążenia"

<!-- links -->

[Limits]: /azure/azure-subscription-service-limits
[Roles]: /azure/role-based-access-control/built-in-roles
[VNet]: /azure/virtual-network/virtual-networks-overview
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
[DMZ]: /azure/best-practices-network-security
[ALB]: /azure/load-balancer/load-balancer-overview
[PIP]: /azure/virtual-network/resource-groups-networking#public-ip-address
[AFD]: /azure/frontdoor/front-door-overview
[AppGW]: /azure/application-gateway/application-gateway-introduction
[WAF]: /azure/application-gateway/application-gateway-web-application-firewall-overview
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
