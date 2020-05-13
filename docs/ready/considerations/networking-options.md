---
title: Przejrzyj opcje sieci
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak identyfikować możliwości sieciowe, które muszą obsługiwać obciążenia platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c310bb6bf7bf2054f315d80c5bddf75871edef09
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223069"
---
<!-- cSpell:ignore paas NVAs VPNs -->

# <a name="review-your-network-options"></a>Przejrzyj opcje sieci

Projektowanie i implementowanie możliwości sieciowych platformy Azure to krytyczna część działań związanych z wdrażaniem w chmurze. Należy podjąć decyzje projektowe dotyczące sieci w celu prawidłowej obsługi obciążeń i usług, które będą hostowane w chmurze. Produkty i usługi sieciowe platformy Azure obsługują szeroką gamę funkcji sieciowych. Wybór struktury tych usług, narzędzi i architektur sieciowych zależy od wymagań dotyczących obciążeń, ładu i łączności w danej organizacji.

## <a name="identify-workload-networking-requirements"></a>Identyfikowanie wymagań sieciowych obciążeń

W ramach oceny i przygotowania strefy docelowej należy zidentyfikować funkcje sieciowe, które muszą być przez nią obsługiwane. Ten proces polega na ocenie poszczególnych aplikacji i usług, które składają się na obciążenie, aby określić wymagania dotyczące kontroli sieci łączności. Po zidentyfikowaniu i udokumentowaniu wymagań można utworzyć zasady dla strefy docelowej w celu kontrolowania dozwolonych zasobów sieciowych i konfiguracji w zależności od potrzeb związanych z obciążeniem.

W przypadku każdej aplikacji lub usługi, która zostanie wdrożona w środowisku strefy docelowej, należy skorzystać z następującego drzewa decyzyjnego jako punktu wyjścia, aby ułatwić określenie narzędzi sieciowych lub usług do użycia:

![Drzewo decyzyjne usług sieciowych platformy Azure](../../_images/ready/network-decision-tree.png)

### <a name="key-questions"></a>Kluczowe pytania

Odpowiedz na następujące pytania dotyczące obciążeń, aby ułatwić podejmowanie decyzji na podstawie drzewa decyzyjnego usług sieciowych platformy Azure:

- **Czy obciążenia będą wymagać sieci wirtualnej?** Zarządzane typy zasobów platformy jako usługi (PaaS) korzystają z podstawowych funkcji sieciowych platformy, które nie zawsze wymagają sieci wirtualnej. Jeśli obciążenia nie wymagają zaawansowanych funkcji sieciowych i nie trzeba wdrażać zasobów infrastruktury jako usługi (IaaS), domyślne [natywne funkcje sieciowe zapewniane przez zasoby PaaS](../../decision-guides/software-defined-network/paas-only.md) mogą spełniać wymagania dotyczące łączności i zarządzania ruchem.
- **Czy obciążenia będą wymagać łączności między sieciami wirtualnymi i lokalnym centrum danych?** Platforma Azure udostępnia dwa rozwiązania do ustanawiania funkcji sieci hybrydowej: Azure VPN Gateway i Azure ExpressRoute. Usługa [Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) umożliwia łączenie sieci lokalnych z platformą Azure za pomocą połączeń sieci VPN między lokacjami w podobny sposób, w jaki zakłada się zdalny oddział i ustanawia połączenie z nim. VPN Gateway ma maksymalną przepustowość 10 GB/s. Usługa [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) oferuje większą niezawodność i mniejsze opóźnienie, dzięki użyciu prywatnego połączenia między platformą Azure i infrastrukturą lokalną. Opcje przepustowości dla ExpressRoute z zakresu od 50 MB/s do 100 GB/s.
- **Czy będzie konieczna kontrola i inspekcja ruchu wychodzącego za pomocą lokalnych urządzeń sieciowych?** W przypadku obciążeń natywnych dla chmury można użyć usługi [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) lub hostowanych w chmurze [wirtualnych urządzeń sieciowych](https://azure.microsoft.com/solutions/network-appliances) innych firm w celu kontroli i inspekcji ruchu przychodzącego lub wychodzącego z publicznej sieci Internet. Jednak wiele zasad zabezpieczeń IT przedsiębiorstwa wymaga, aby ruch wychodzący związany z Internetem był przekazywany przez centralnie zarządzane urządzenia w środowisku lokalnym organizacji. [Wymuszone tunelowanie](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) obsługuje te scenariusze. Nie wszystkie usługi zarządzane obsługują wymuszone tunelowanie. Usługi i funkcje, takie jak [środowisko App Service Environment w usłudze Azure App Service](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-key-concepts), [Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes), [wystąpienia zarządzane w usłudze Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index), [Azure Databricks](https://docs.microsoft.com/azure/azure-databricks/what-is-azure-databricks) i [Azure HDInsight](https://docs.microsoft.com/azure/hdinsight), obsługują tę konfigurację, gdy usługa lub funkcja jest wdrożona w sieci wirtualnej.
- **Czy konieczne będzie łączenie wielu sieci wirtualnych?** [Komunikacja równorzędna w sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) umożliwia łączenie wielu wystąpień usługi [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Komunikacja równorzędna umożliwia obsługę połączeń między subskrypcjami i regionami. W przypadku scenariuszy, w których zapewniane są usługi współużytkowane przez wiele subskrypcji lub konieczne jest zarządzanie dużą liczbą sieci równorzędnych, należy rozważyć przyjęcie [architektury sieciowej o topologii gwiazdy](../../decision-guides/software-defined-network/hub-spoke.md) lub użyć usługi [Azure Virtual WAN](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about). Komunikacja równorzędna w sieci wirtualnej zapewnia łączność tylko między dwiema sieciami równorzędnymi. Domyślnie nie zapewnia ona łączności przechodniej między wieloma sieciami równorzędnymi.
- **Czy obciążenia będą dostępne za pośrednictwem Internetu?** Platforma Azure zapewnia usługi mające na celu pomoc w zarządzaniu dostępem zewnętrznym do aplikacji i usługi oraz jego zabezpieczeniu:
  - [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview)
  - [Urządzenia sieciowe](https://azure.microsoft.com/solutions/network-appliances)
  - [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor/front-door-overview)
  - [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway)
  - [Traffic Manager platformy Azure](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)
- **Czy jest wymagana obsługa zarządzania niestandardową usługą DNS?** Usługa [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) jest usługą hostingu dla domen DNS. Usługa Azure DNS zapewnia rozpoznawanie nazw przy użyciu infrastruktury platformy Azure. Jeśli obciążenia wymagają rozpoznawania nazw, które wykracza poza funkcje udostępniane przez usługę Azure DNS, może być konieczne wdrożenie dodatkowych rozwiązań. Jeśli obciążenia wymagają również usług Active Directory, rozważ użycie usług [Azure Active Directory Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/overview) w celu rozszerzenia możliwości usługi Azure DNS. Aby uzyskać więcej możliwości, można również [wdrożyć niestandardowe maszyny wirtualne IaaS](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances) w celu spełnienia wymagań.

## <a name="common-networking-scenarios"></a>Typowe scenariusze pracy w sieci

Sieć platformy Azure składa się z wielu produktów i usług, które zapewniają różne możliwości sieciowe. W ramach procesu projektowania sieci można porównać wymagania dotyczące obciążeń ze scenariuszami sieciowymi w poniższej tabeli, aby zidentyfikować narzędzia i usługi platformy Azure, których można użyć w celu zapewnienia potrzebnych możliwości sieciowych:

<!-- markdownlint-disable MD033 -->

| **Scenariusz** | **Produkt lub usługa sieciowa** |
| --- | --- |
| Potrzebuję infrastruktury sieciowej do łączenia dowolnych zasobów, od maszyn wirtualnych po przychodzące połączenia sieci VPN. | [Virtual Network platformy Azure](https://docs.microsoft.com/azure/virtual-network) |
| Chcę zrównoważyć przychodzące i wychodzące połączenia oraz żądania do aplikacji lub usług. | [Azure Load Balancer](https://docs.microsoft.com/azure/load-balancer) |
| Chcę zoptymalizować dostarczanie z farm serwerów aplikacji, jednocześnie zwiększając bezpieczeństwo aplikacji za pomocą zapory aplikacji internetowych. | [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway) <br/>[Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Chcę bezpiecznie korzystać z Internetu w celu uzyskania dostępu do sieci Azure Virtual Network za pomocą bram sieci VPN o wysokiej wydajności. | [VPN Gateway platformy Azure](https://docs.microsoft.com/azure/vpn-gateway) |
| Chcę zapewnić niezwykle szybkie odpowiedzi DNS i niezwykle wysoką dostępność, aby zaspokoić wszystkie potrzeby związane z domeną. | [System DNS platformy Azure](https://docs.microsoft.com/azure/dns) |
| Chcę przyspieszyć dostarczanie zawartości o wysokiej przepustowości do klientów na całym świecie — od aplikacji i przechowywanej zawartości, po przesyłanie strumieniowe filmów wideo. | [Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn) |
| Chcę chronić moje aplikacje platformy Azure przed atakami DDoS. | [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) |
| Chcę w sposób optymalny dystrybuować ruch do usług w obrębie globalnych regionów platformy Azure, zapewniając wysoką dostępność i krótki czas reakcji. | [Traffic Manager platformy Azure](https://docs.microsoft.com/azure/traffic-manager) <br><br> [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |
| Chcę dodać łączność z sieciami prywatnymi, aby móc uzyskać dostęp do usług w chmurze firmy Microsoft z sieci firmowych, tak jakby znajdowały się lokalnie w centrum danych. | [Azure ExpressRoute](https://docs.microsoft.com/azure/expressroute) |
| Chcę monitorować i diagnozować warunki na poziomie sieci. | [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher) |
| Potrzebuję natywnych możliwości zapory z wbudowaną wysoką dostępnością, skalowalnością w chmurze i konserwacją bez ograniczeń. | [Azure Firewall](https://docs.microsoft.com/azure/firewall/overview) |
| Chcę bezpiecznie połączyć biura firmy, punkty sprzedaży detalicznej i witryny. | [Wirtualna sieć WAN platformy Azure](https://docs.microsoft.com/azure/virtual-wan) |
| Potrzebuję skalowalnego punktu dostarczania z rozszerzonymi zabezpieczeniami na potrzeby globalnych aplikacji internetowych opartych na mikrousługach. | [Azure Front Door Service](https://docs.microsoft.com/azure/frontdoor) |

<!-- markdownlint-enable MD033 -->

## <a name="choose-a-networking-architecture"></a>Wybór architektury sieci

Po zidentyfikowaniu usług sieciowych platformy Azure potrzebnych do obsługi obciążeń należy również zaprojektować architekturę, która będzie łączyć te usługi, aby zapewnić infrastrukturę sieciową w chmurze dla strefy docelowej. [Przewodnik po decyzjach dotyczących sieci zdefiniowanej programowo](../../decision-guides/software-defined-network/index.md) w ramach struktury wdrażania chmury zawiera szczegółowe informacje na temat niektórych wzorców architektury sieci najczęściej używanych na platformie Azure.

W poniższej tabeli przedstawiono podstawowe scenariusze obsługiwane przez te wzorce:

| **Scenariusz**                                                                                                                                                                                                                                                                                                                                                          | **Sugerowana architektura sieci**                                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Wszystkie obciążenia hostowane na platformie Azure wdrożone w strefie docelowej będą całkowicie PaaS, nie wymagają sieci wirtualnej ani nie są częścią szerszego wysiłku związanego z wdrażaniem w chmurze, który obejmuje zasoby IaaS.                                                                                                                                                          | [Tylko usługa PaaS](../../decision-guides/software-defined-network/paas-only.md)            |
| Obciążenia hostowane na platformie Azure wymagają wdrożenia zasobów opartych na usłudze IaaS, takich jak maszyny wirtualne, lub sieci wirtualnej, ale nie wymagają łączności ze środowiskiem lokalnym.                                                                                                                                                                            | [Natywne dla chmury](../../decision-guides/software-defined-network/cloud-native.md)      |
| Obciążenia hostowane na platformie Azure wymagają ograniczonego dostępu do zasobów lokalnych, ale wymagane jest traktowanie połączeń w chmurze jako niezaufanych.                                                                                                                                                                                                                             | [Strefa DMZ w chmurze](../../decision-guides/software-defined-network/cloud-dmz.md)            |
| Obciążenia hostowane na platformie Azure wymagają ograniczonego dostępu do zasobów lokalnych i planujesz wdrożyć sprawdzone zasady zabezpieczeń oraz bezpieczną łączność między chmurą i środowiskiem lokalnym.                                                                                                                                                           | [Hybrydowe](../../decision-guides/software-defined-network/hybrid.md)                  |
| Musisz wdrożyć dużą liczbę maszyn wirtualnych i obciążeń, które mogą przekraczać [limity subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits), i zarządzać nimi, musisz udostępnić usługi w różnych subskrypcjach lub potrzebujesz bardziej rozbudowanej struktury dla roli, aplikacji lub podziału uprawnień. | [Gwiazda](../../decision-guides/software-defined-network/hub-spoke.md)        |
| Istnieje wiele oddziałów, które muszą łączyć się ze sobą i z platformą Azure.                                                                                                                                                                                                                                                                                         | [Wirtualna sieć WAN platformy Azure](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) |

<!-- TODO: Refactor VDC content below. -->
<!-- docsTest:ignore "Azure Virtual Datacenter" -->

### <a name="azure-virtual-datacenter"></a>Wirtualne centrum danych Azure

Oprócz korzystania z tych wzorców architektury, jeśli grupa IT przedsiębiorstwa zarządza dużymi środowiskami w chmurze, rozważ zapoznanie się [ze wskazówkami dotyczącymi wirtualnego centrum danych platformy Azure](../../reference/vdc.md) podczas projektowania infrastruktury chmurowej opartej na platformie Azure. Wirtualne centrum danych na platformie Azure oferuje połączone podejście do sieci, zabezpieczeń, zarządzania i infrastruktury, jeśli organizacja spełnia następujące kryteria:

- Twoje przedsiębiorstwo podlega przepisom, zgodnie z którymi wymagane jest używanie scentralizowanych funkcji monitorowania i inspekcji.
- Twoja infrastruktura chmury będzie się składać z ponad 10 000 maszyn wirtualnych IaaS lub równoważnej liczby usług PaaS.
- Należy włączyć możliwości elastycznego wdrażania dla obciążeń jako wsparcie dla zespołów deweloperów i zespołów operacyjnych, jednocześnie zachowując zgodność z typowymi zasadami i nadzorem oraz centralną kontrolę IT nad podstawowymi usługami.
- Twoja branża zależy od złożonej platformy, która wymaga głębokiej znajomości danej dziedziny (na przykład finansów, przemysłu naftowego lub produkcji).
- Twoje istniejące zasady nadzoru IT wymagają większej zgodności z istniejącymi funkcjami nawet na wczesnym etapie wdrażania.

## <a name="follow-azure-networking-best-practices"></a>Stosuj najlepsze rozwiązania sieciowe na platformie Azure

W ramach procesu projektowania sieci zapoznaj się z następującymi artykułami:

- [Planowanie sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się, jak zaplanować sieci wirtualne na podstawie wymagań dotyczących izolacji, łączności i lokalizacji.
- [Najlepsze rozwiązania z zakresu zabezpieczeń sieci na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) Dowiedz się więcej o najlepszych rozwiązaniach dotyczących platformy Azure, które mogą pomóc w ulepszaniu zabezpieczeń sieci.
- [Najlepsze rozwiązania dotyczące sieci podczas migrowania obciążeń do platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-best-practices-networking?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json) Uzyskaj dodatkowe wskazówki dotyczące implementowania sieci platformy Azure do obsługi obciążeń opartych na rozwiązaniach IaaS i PaaS.
