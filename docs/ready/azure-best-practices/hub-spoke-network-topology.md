---
title: Topologia sieci piasty i szprych
description: Poznaj topologie sieci gwiazdy i gwiazdy.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 3f0a49675e82727b07c3d285397768de6429e8e8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76800036"
---
# <a name="hub-and-spoke-network-topology"></a>Topologia sieci piasty i szprych

*Piasta i szprychy* to model sieci umożliwiający bardziej efektywne zarządzanie typowymi wymaganiami dotyczącymi komunikacji i zabezpieczeń. Pomaga również uniknąć ograniczeń subskrypcji platformy Azure. Ten model dotyczy następujących kwestii:

- **Oszczędność kosztów i efektywność zarządzania**. Scentralizowanie w jednej lokalizacji usług, które mogą być współużytkowane przez wiele obciążeń, takich jak wirtualne urządzenia sieciowe (NVA) i serwery DNS, umożliwia działowi IT zminimalizowanie nadmiarowych zasobów i zadań związanych z zarządzaniem.
- **Pokonywanie ograniczeń subskrypcji**. Duże obciążenia oparte na chmurze mogą wymagać użycia większej ilości zasobów, niż jest to dozwolone w pojedynczej subskrypcji platformy Azure. Komunikacja równorzędna sieci wirtualnych obciążenia z różnych subskrypcji do centrum może pokonać te ograniczenia. Aby uzyskać więcej informacji, zobacz [limity subskrypcji](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Separacja problemów**. Poszczególne obciążenia można wdrożyć między centralnymi zespołami IT i zespołami obciążeń.

Dodatkowa struktura i możliwości oferowane przez ten model mogą nie przynieść korzyści mniejszym majątkom w chmurze. Jednak większe działania związane z wdrażaniem w chmurze powinny uwzględniać implementację architektury sieci typu Hub i szprychy, jeśli mają one jakiekolwiek problemy wymienione wcześniej.

> [!NOTE]
> Lokacja architektury referencyjnej platformy Azure zawiera przykładowe szablony, których można użyć jako podstawy do implementowania własnych sieci Hub i szprych:
>
> - [Implementowanie topologii sieci gwiazdy i gwiazdy na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementowanie topologii sieci gwiazdy i gwiazdy przy użyciu usług udostępnionych na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Przegląd

![Przykłady topologii sieci gwiazdy i gwiazdy][1]

Jak pokazano na diagramie, platforma Azure obsługuje dwa typy centrów i satelitów. Obsługuje ona komunikację, zasoby udostępnione i scentralizowane zasady zabezpieczeń („centrum sieci wirtualnej” na diagramie) lub typ wirtualnej sieci WAN („wirtualna sieć WAN” na diagramie) na potrzeby wielkoskalowej komunikacji między oddziałami lub między oddziałem i platformą Azure.

Piasta to centralna strefa sieciowa, która kontroluje i sprawdza ruch przychodzący i wychodzący między strefami: Internet, środowisko lokalne i szprychy. Topologia gwiazdy umożliwia działowi IT efektywną metodę wymuszania zasad zabezpieczeń w centralnej lokalizacji. Minimalizuje również ryzyko błędnej konfiguracji i ekspozycji.

Piasta zawiera często wspólne składniki usługi używane przez szprychy. Poniżej przedstawiono typowe usługi centralne:

- Infrastruktura usługi Active Directory systemu Windows Server, wymagana do uwierzytelniania użytkowników innych firm, którzy uzyskują dostęp z niezaufanych sieci przed uzyskaniem dostępu do obciążeń w szprysze. Obejmuje ona powiązane usługi Active Directory Federation Services (AD FS).
- Usługa DNS do rozpoznawania nazw obciążeń w szprychach, do uzyskiwania dostępu do zasobów lokalnych i w Internecie, jeśli usługa [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) nie jest używana.
- Infrastruktura kluczy publicznych (PKI) do implementowania obciążeń logowania jednokrotnego.
- Kontrola przepływu ruchu TCP i UDP między strefami sieciowymi szprych i Internetem.
- Sterowanie przepływem między szprychami i środowiskiem lokalnym.
- W razie konieczności sterowanie przepływem między jedną szprychą a inną.

Używając infrastruktury piasty udostępnionej w celu obsługi wielu szprych, można zminimalizować nadmiarowość, uprościć zarządzanie i obniżyć koszt całkowity.

Rolą każdej szprychy może być hostowanie różnych typów obciążeń. Szprychy zapewniają również modularne podejście do powtarzających się wdrożeń tych samych obciążeń. Przykłady to programowanie i testowanie, testowanie akceptacji przez użytkowników, przygotowanie i produkcja.

Szprychy mogą również dzielić różne grupy w obrębie organizacji i umożliwiać ich tworzenie. Przykładem są grupy usługi Azure DevOps. Wewnątrz szprychy można wdrażać podstawowe obciążenia lub złożone obciążenia wielowarstwowe z kontrolą ruchu między warstwami.

## <a name="subscription-limits-and-multiple-hubs"></a>Ograniczenia subskrypcji i wiele piast

Na platformie Azure każdy składnik, niezależnie od typu, jest wdrażany w ramach subskrypcji platformy Azure. Izolacja składników platformy Azure w różnych subskrypcjach platformy Azure może spełniać różne wymagania biznesowe, takie jak konfigurowanie różnych poziomów dostępu i autoryzacji.

Pojedyncze implementacje Hub i szprychy mogą być skalowane do dużej liczby szprych. Jednak podobnie jak w przypadku każdego systemu informatycznego, istnieją ograniczenia platformy. Wdrożenie piasty jest powiązane z określoną subskrypcją platformy Azure, która ma ograniczenia i limity. Przykładem jest maksymalna liczba komunikacji równorzędnych sieci wirtualnych. Aby uzyskać więcej informacji, zobacz [Limity, przydziały i ograniczenia usług i subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

W przypadkach, gdy ograniczenia mogą stanowić problem, można skalować w górę architekturę, rozszerzając model z jednej piasty i szprych do klastra piast i szprych. Możesz połączyć wiele piast w jednym lub większej liczbie regionów świadczenia usługi Azure za pomocą komunikacji równorzędnej sieci wirtualnych, usługi Azure ExpressRoute, wirtualnej sieci WAN lub sieci VPN typu lokacja-lokacja.

![Klaster piast i szprych][2]

Wprowadzenie wielu piast zwiększa koszt i nakłady pracy związane z zarządzaniem w systemie. Jest to usprawiedliwione tylko skalowalnością, ograniczeniami systemu lub nadmiarowością i replikacją regionalną na potrzeby wydajności użytkownika lub odzyskiwania po awarii. W scenariuszach wymagających wielu piast wszystkie piasty powinny dążyć do oferowania tego samego zestawu usług w celu ułatwienia zadań operacyjnych.

## <a name="interconnection-between-spokes"></a>Wzajemne połączenia między szprychami

Istnieje możliwość zaimplementowania złożonych, wielowarstwowych obciążeń w obrębie jednej szprychy. Konfiguracje wielowarstwowe można implementować przy użyciu podsieci (jedna dla każdej warstwy) w tej samej sieci wirtualnej i przy użyciu sieciowych grup zabezpieczeń do filtrowania przepływów.

Architekt może chcieć wdrożyć obciążenie wielowarstwowe w wielu sieciach wirtualnych. Za pomocą komunikacji równorzędnej sieci wirtualnych szprychy mogą łączyć się z innymi szprychami w tej samej piaście lub w różnych piastach.

Typowym przykładem tego scenariusza jest przypadek, w którym serwery przetwarzania aplikacji znajdują się w jednej szprysze lub sieci wirtualnej. Baza danych jest wdrażana w innej szprysze lub sieci wirtualnej. W takim przypadku można łatwo połączyć szprychy za pomocą komunikacji równorzędnej sieci wirtualnych, aby uniknąć przesyłania danych przez piastę. Rozwiązaniem jest przeprowadzenie starannej architektury i przeglądu zabezpieczeń, aby upewnić się, że pominięcie centrum nie pomija ważnych punktów zabezpieczeń lub inspekcji, które mogą istnieć tylko w centrum.

![Szprychy połączone ze sobą i z piastą][3]

Szprychy mogą być również połączone ze szprychą, która pełni rolę piasty. Takie podejście tworzy hierarchię dwupoziomową: szprycha na wyższym poziomie (poziom 0) staje się piastą dla małych szprych (poziom 1) w hierarchii. Szprychy wdrożenia gwiazdy i gwiazdy są wymagane do przekazywania ruchu do centralnego koncentratora, dzięki czemu ruch może być przesyłany do miejsca docelowego w sieci lokalnej lub w publicznym Internecie. Architektura z dwoma poziomami koncentratorów wprowadza skomplikowany Routing, który usuwa zalety prostej relacji gwiazdy i satelity.

<!-- images -->

[0]: ../../_images/azure-best-practices/network-redundant-equipment.png "Przykłady nakładania się składników"
[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Ogólny przykład piasty i szprych"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ../../_images/azure-best-practices/network-hub-spoke-block-level-diagram.png "Diagram na poziomie bloku piasty i szprych"
[5]: ../../_images/azure-best-practices/network-users-groups-subscriptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ../../_images/azure-best-practices/network-infrastructure-high-level.png "Diagram infrastruktury wysokiego poziomu"
[7]: ../../_images/azure-best-practices/network-high-level-perimeter-networks.png "Diagram infrastruktury wysokiego poziomu"
[8]: ../../_images/azure-best-practices/network-vnet-peering-perimeter-networks.png "Komunikacja równorzędna sieci wirtualnych i sieci obwodowe"
[9]: ../../_images/azure-best-practices/network-high-level-diagram-monitoring.png "Ogólny diagram dla monitorowania"
[10]: ../../_images/azure-best-practices/network-high-level-workloads.png "Ogólny diagram dla obciążenia"

<!-- links -->

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
[SubMgmt]: ../../reference/azure-scaffold.md
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AFD]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
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
