---
title: Najlepsze rozwiązania dotyczące konfigurowania sieci pod kątem obciążeń migrowanych do platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Po przeprowadzeniu migracji do platformy Azure, należy uzyskać najlepsze rozwiązania dotyczące konfigurowania sieci dla migrowanych obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a7f119dcfd2b7cdfc71b8a4c6f913448cd98e763
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753615"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące konfigurowania sieci pod kątem obciążeń migrowanych do platformy Azure

Projektowanie pod kątem migracji, oprócz migracji, oraz plan jest jedną z najważniejszych etapów projektowania i implementowania sieci platformy Azure. W tym artykule opisano najlepsze rozwiązania dotyczące sieci w przypadku migrowania do implementacji usług IaaS i PaaS na platformie Azure.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule dotyczą funkcji usług i platformy Azure dostępnych w momencie pisania artykułu. Funkcje i możliwości zmieniają się w miarę upływu czasu. Nie wszystkie rekomendacje mogą obowiązywać dla danego wdrożenia, więc wybierz te, które są odpowiednie w Twoim przypadku.

## <a name="design-virtual-networks"></a>Projektowanie sieci wirtualnych

Platforma Azure oferuje sieci wirtualne:

- Zasoby platformy Azure komunikować się prywatnie, bezpośrednio i bezpiecznie ze sobą za pośrednictwem sieci wirtualnych.
- Można skonfigurować połączenia punktów końcowych w sieciach wirtualnych dla maszyn wirtualnych i usług, które wymagają komunikacji internetowej.
- Sieć wirtualna jest to logiczna izolacja chmury platformy Azure przeznaczoną do Twojej subskrypcji.
- W każdej subskrypcji platformy Azure oraz w każdym regionie świadczenia usługi Azure możesz zaimplementować wiele sieci wirtualnych.
- Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych.
- Sieci wirtualne mogą zawierać prywatne i publiczne adresy IP określone w [RFC 1918](https://tools.ietf.org/html/rfc1918), wyrażona w notacji CIDR. Publiczne adresy IP określone w przestrzeni adresowej sieci wirtualnej nie są bezpośrednio dostępne z Internetu.
- Sieci wirtualne mogą łączyć się ze sobą za pomocą komunikacji równorzędnej sieci wirtualnej. Połączone sieci wirtualne mogą znajdować się w tej samej lub różnych regionach. Dzięki temu zasoby w jednej sieci wirtualnej mogą łączyć się z zasobami w innych sieciach wirtualnych.
- Domyślnie platforma Azure kieruje ruch pomiędzy podsieciami w sieci wirtualnej, połączone z sieciami wirtualnymi, sieciami lokalnymi i Internetem.

Podczas planowania topologii sieci wirtualnej należy wziąć pod uwagę sposób rozmieszczenia przestrzeni adresowej IP, sposób implementacji sieci gwiazdy, sposób segmentowania sieci wirtualnych w podsieci, konfigurowanie systemu DNS i implementowanie stref dostępności platformy Azure.

## <a name="best-practice-plan-ip-addressing"></a>Najlepsze rozwiązanie: Planowanie adresowania IP

Podczas tworzenia sieci wirtualnych w ramach migracji, należy zaplanować przestrzenią adresów IP sieci wirtualnej.

- Należy przypisać przestrzeń adresową, która nie jest większa od zakresu CIDR /16 dla każdej sieci wirtualnej. Sieci wirtualne zezwalają na korzystanie z 65 536 adresów IP, a przypisanie prefiksu mniejszego niż /16 powoduje utratę adresów IP. Ważne jest nie tracić adresów IP, nawet jeśli pochodzi z zakresów prywatnych definicją w dokumencie RFC 1918.
- Przestrzeń adresowa sieci wirtualnej nie powinna nakładać się z zakresami sieci lokalnych.
- Nie należy używać translatora adresów sieciowych (NAT).
- Nakładające się przestrzenie adresów może spowodować, że nie można połączyć sieci i routingu, który nie działa prawidłowo. Jeśli sieci się nakładają, należy ponownie zaprojektować sieć lub użyć translatora adresów sieciowych (NAT).

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) z sieciami wirtualnymi platformy Azure.
- [Odczyt](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) sieć — często zadawane pytania.
- [Dowiedz](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) się więcej na temat ograniczeń sieci.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Najlepsze rozwiązanie: implementowanie topologii sieci gwiazdy i gwiazdy

Topologia sieci piasty i szprych izoluje obciążenia przy jednoczesnym udostępnianiu usług, takich jak tożsamość i zabezpieczenia.

- Piasta to działający jako punkt centralny łączności z siecią wirtualną platformy Azure.
- Szprychy to sieci wirtualne, które łączą się z siecią wirtualną piasty przy użyciu komunikacji równorzędnej sieci wirtualnych.
- Usługi udostępnione są wdrażane w piaście, a poszczególne obciążenia są wdrażane jako szprychy.

Rozważ następujące źródła:

- Implementacja topologii gwiazdy na platformie Azure umożliwia centralizowanie typowych usług, takich jak połączenia z sieciami lokalnymi, zapory i izolacja między sieciami wirtualnymi. Sieć wirtualna piasty zapewnia centralny punkt łączności z sieciami lokalnymi oraz miejsce do hostowania użycia usług przez obciążenia hostowane w sieciach wirtualnych szprych.
- Konfiguracja gwiazdy jest zwykle używana przez większe przedsiębiorstwa. W mniejszych sieciach można zastosować prostsze projekty, aby zaoszczędzić na kosztach i zredukować złożoność.
- Sieci wirtualne szprych mogą być używane do izolowania obciążeń w poszczególnych szprychach zarządzanych oddzielnie od innych szprych. Każde obciążenie może zawierać wiele warstw i wiele podsieci połączonych za pośrednictwem modułów równoważenia obciążenia platformy Azure.
- Gwiazda sieciami wirtualnymi można zaimplementować w różnych grupach zasobów, a nawet w różnych subskrypcjach. W przypadku komunikacji równorzędnej sieci wirtualnych w różnych subskrypcjach subskrypcje mogą być kojarzone z tymi samymi lub różnymi dzierżawami usługi Azure Active Directory (Azure AD). Umożliwia to zdecentralizowane zrządzanie każdym obciążeniem, a jednocześnie udostępnianie usług obsługiwanych w centralnej sieci.

![Zarządzanie zmianami](./media/migrate-best-practices-networking/hub-spoke.png)
*Topologia gwiazdy*

**Dowiedz się więcej:**

- [Poczytaj](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) o topologii gwiazdy.
- Uzyskaj zalecenia dotyczące sieci dla uruchomionych na platformie Azure [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) i [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm) maszyn wirtualnych.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) komunikacja równorzędna sieci wirtualnych.

## <a name="best-practice-design-subnets"></a>Najlepsze rozwiązanie: Zaprojektuj podsieci

Aby zapewnić izolację w sieci wirtualnej, należy posegmentować ją na jedną lub więcej podsieci i przypisać części przestrzeni adresowej sieci wirtualnej do każdej podsieci.

- W każdej sieci wirtualnej można utworzyć wiele podsieci.
- Domyślnie platforma Azure kieruje ruchem sieciowym między wszystkie podsieci w sieci wirtualnej.
- Decyzje dotyczące podsieci opierają się na wymaganiach technicznych i organizacyjnych.
- Możesz utworzyć przy użyciu notacji CIDR podsieci.
- Podczas ustawiania zakresu sieci dla podsieci, to należy pamiętać, że Azure zachowuje pięciu adresów IP w każdej podsieci, której nie można użyć. Jeśli na przykład utworzysz najmniejszą dostępną podsieć /29 (z ośmioma adresami IP), platforma Azure zachowa pięć adresów, więc będziesz mieć tylko trzy możliwe do użycia adresy, które można przypisać do hostów w podsieci.
- W większości przypadków należy użyć/28 jako najmniejszej podsieci.

**Przykład:**

W tabeli przedstawiono przykład sieci wirtualnej przy użyciu przestrzeni adresowej 10.245.16.0/20 podzielono ją na podsieci, w przypadku planowanej migracji.

**Podsieć** | **CIDR** | **Adresy** | **Korzystanie**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Maszyny wirtualne z bazy danych

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) projektowania podsieci.
- [Dowiedz się](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), w jaki sposób fikcyjna firma (Contoso) przygotowała infrastrukturę sieciową do migracji.

## <a name="best-practice-set-up-a-dns-server"></a>Najlepsze rozwiązanie: Konfigurowanie serwera DNS

Platforma Azure dodaje serwer DNS domyślnie podczas wdrażania sieci wirtualnej. Dzięki temu można szybko tworzyć sieci wirtualne i wdrażać zasoby. Jednak ten serwer DNS zapewnia tylko usługi dla zasobów w tej sieci wirtualnej. Jeśli chcesz połączyć ze sobą wiele sieci wirtualnych lub połącz się z lokalnym serwerem z sieciami wirtualnymi, potrzebujesz możliwości rozpoznawania nazw dodatkowe. Na przykład może być konieczne usługi Active Directory do rozpoznawania nazw DNS między sieciami wirtualnymi. W tym celu należy wdrożyć własny niestandardowy serwer DNS na platformie Azure.

- Serwery DNS w sieci wirtualnej może przekazywać zapytań DNS do rozpoznawania cyklicznego na platformie Azure. Dzięki temu można rozpoznawać nazwy hostów w ramach tej sieci wirtualnej. Na przykład kontroler domeny działający na platformie Azure może odpowiadać na zapytania DNS dotyczące własnych domen i przekazywać wszystkie inne zapytania do platformy Azure.
- Przekazywanie dalej w systemie DNS umożliwia maszynom wirtualnym wyświetlanie zasobów lokalnych (za pośrednictwem kontrolera domeny) i nazw hostów udostępnianych przez platformę Azure (przy użyciu programu do przekazywania dalej). Dostęp do cyklicznych programów rozpoznawania nazw na platformie Azure jest udostępniany przy użyciu wirtualnego adresu IP 168.63.129.16.
- Przekazywanie dalej w systemie DNS umożliwia również rozpoznawanie nazw DNS między sieciami wirtualnymi i umożliwia maszynom lokalnym rozpoznawanie nazw hostów udostępnianych przez platformę Azure.
  - Aby rozpoznać nazwę hosta maszyny Wirtualnej, serwer DNS maszyny Wirtualnej musi znajdować się w tej samej sieci wirtualnej i można skonfigurować na kwerendy nazwy hosta do przodu na platformie Azure.
  - Ponieważ sufiks DNS różni się w każdej sieci wirtualnej, można użyć reguły warunkowego przesyłania dalej do wysyłania zapytań DNS do poprawną sieć wirtualną dla rozwiązania.
- W przypadku korzystania z własnych serwerów DNS można określić wiele serwerów DNS dla każdej sieci wirtualnej. Można również określić wiele serwerów DNS dla każdego interfejsu sieciowego (dla usługi Azure Resource Manager) lub dla usługi w chmurze (w przypadku klasycznego modelu wdrażania).
- Serwery DNS określona dla interfejsu lub w chmurze Usługa sieciowa mają pierwszeństwo przed serwerów DNS określona dla sieci wirtualnej.
- W modelu wdrażania usługi Azure Resource Manager można określić serwery DNS dla sieci wirtualnej i interfejsu sieciowego, ale najlepszym rozwiązaniem jest użycie ustawienia tylko w przypadku sieci wirtualnych.

    ![Serwery DNS](./media/migrate-best-practices-networking/dns2.png) *Serwery DNS dla sieci wirtualnej*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) rozpoznawania nazw, gdy używasz własnego serwera DNS.
- [Dowiedz się więcej](../../ready/azure-best-practices/naming-and-tagging.md) o regułach i ograniczeniach nazewnictwa DNS.

## <a name="best-practice-set-up-availability-zones"></a>Najlepsze rozwiązanie: ustawienie strefy dostępności

Strefy dostępności zwiększenie wysokiej dostępności chronią aplikacje i dane przed awariami centrum danych.

- Strefy dostępności to unikatowe fizycznie lokalizacje w regionie platformy Azure.
- Każda strefa składa się z co najmniej jeden centrów danych, wyposażone w niezależne zasilanie, chłodzenie i usługi sieciowe.
- Aby zapewnić odporność, istnieje co najmniej trzy osobne strefy we wszystkich regionach włączone.
- Fizyczna separacja stref dostępności w ramach regionu chroni aplikacje i dane przed awariami centrum danych.
- Strefowo nadmiarowe usługi Replikowanie aplikacji i danych w strefach dostępności, aby chronić przed pojedynczych punktów awarii. — Dzięki strefom dostępności platforma Azure oferuje umową SLA gwarantującą dostępność przez 99,99% dostępności maszyn wirtualnych.

    ![Strefa dostępności](./media/migrate-best-practices-networking/availability-zone.png) *strefy dostępności*

- Wysoką dostępność można zaplanować i utworzyć w architekturze migracji przez umieszczanie zasobów obliczeniowych, magazynu, sieci i danych w ramach tej samej strefy, a następnie replikowanie ich w innych strefach. Usługi platformy Azure, które obsługują strefy dostępności można podzielić na dwie kategorie:
  - Strefowy usług: zasób jest skojarzona z określonej strefy. Aby uzyskać przykład maszyn wirtualnych dysków zarządzanych, adresy IP).
  - Strefowo nadmiarowe usług: zasób jest automatycznie replikowana w strefach. Na przykład magazyn strefowo nadmiarowy, Azure SQL Database.
- Możesz wdrożyć standardowe obciążenia platformy Azure równoważenia obciążenia dostępnego z Internetu lub warstwy aplikacji w celu zapewnienia odporności strefowej.

    ![Moduł równoważenia obciążenia](./media/migrate-best-practices-networking/load-balancer.png) *Moduł równoważenia obciążenia*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/availability-zones/az-overview) stref dostępności.

## <a name="design-hybrid-cloud-networking"></a>Projektowanie sieci w chmurze hybrydowej

W przypadku pomyślnej migracji najważniejsze jest połączenie lokalnych sieci firmowych z platformą Azure. Spowoduje to utworzenie połączenia zawsze włączone, znane jako sieć chmury hybrydowej, w których usługi są dostępne na platformie Azure w chmurze i użytkowników firmowych. Istnieją dwa sposoby tworzenia tego typu sieci:

- **Sieć VPN lokacja lokacja:** nawiązaniem połączenia lokacja lokacja między urządzeniem sieci VPN zgodne w środowisku lokalnym i bramą Azure VPN gateway, które zostało wdrożone w sieci wirtualnej. Każdy uprawniony lokalnych zasobów mogą uzyskiwać dostęp do sieci wirtualnych. Łączności lokacja lokacja są wysyłane przez szyfrowany tunel za pośrednictwem Internetu.
- **Usługa ExpressRoute systemu Azure:** nawiązania połączenia usługi Azure ExpressRoute między siecią lokalną i platformę Azure za pośrednictwem partnera usługi ExpressRoute. To połączenie jest prywatne i ruch nie przechodzi przez Internet.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) o sieci w chmurze hybrydowej.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Najlepsze rozwiązanie: Implementowanie wysokiej dostępności sieci VPN typu lokacja lokacja

Aby zaimplementować VPN lokacja lokacja, należy skonfigurować bramę sieci VPN na platformie Azure.

- Brama sieci VPN jest określonym typem bramy wirtualnej, który wysyła zaszyfrowany ruch sieciowy między siecią wirtualną platformy Azure a lokalizacją lokalną za pośrednictwem publicznego Internetu.
- Brama sieci VPN może również wysyłać szyfrowany ruch sieciowy między usługą Azure sieci wirtualnych za pośrednictwem sieci firmy Microsoft.
- Każda sieć wirtualna może mieć tylko jedną bramę sieci VPN.
- Możesz utworzyć wiele połączeń do tej samej bramy sieci VPN. Podczas tworzenia wielu połączeń, wszystkie tunele VPN współdzielą dostępną przepustowość bramy.
- Każda brama Azure VPN Gateway składa się z dwóch wystąpień działających w konfiguracji aktywne-w gotowości.
  - W przypadku planowanej konserwacji lub nieplanowanych zakłóceń działania aktywnego wystąpienia następuje przejście w tryb failover, a wystąpienie w trybie gotowości automatycznie przejmuje zadanie i wznawia połączenie typu lokacja-lokacja lub połączenie między sieciami wirtualnymi.
  - Przełączenie powoduje krótką przerwę w działaniu.
  - W przypadku planowanej konserwacji łączność powinna zostać przywrócona w ciągu od 10 do 15 sekund.
  - W przypadku nieplanowanych awarii odzyskiwanie połączenia trwa dłużej, od 1 do 1,5 minuty w najgorszym przypadku.
  - Połączenia klienta sieci VPN typu punkt-lokacja (P2S) z bramą zostaną rozłączone, a użytkownicy będą musieli ponownie nawiązać połączenia z poziomu maszyn klienckich.

Podczas konfigurowania sieci VPN lokacja lokacja, możesz wykonać następujące czynności:

- Potrzebna jest sieć wirtualna, której zakres adresów nie nakłada się na sieć lokalną, z której zostanie połączona sieć VPN.
- W sieci należy utworzyć podsieć bramy.
- Tworzenie bramy sieci VPN, określ typ bramy (VPN) i czy brama jest oparta na zasadach lub oparte na trasach. Sieci VPN opartej na trasach są uważane za dodatkowe możliwości i przyszłe potwierdzenie.
- Lokalną bramę sieciową można utworzyć lokalnie i skonfigurować lokalne urządzenie sieci VPN.
- Należy utworzyć połączenie sieci VPN typu lokacja-lokacja między bramą sieci wirtualnej i urządzeniem lokalnym. Korzystanie z sieci VPN opartej na trasach zezwala na połączenia aktywne-pasywne lub aktywne-aktywne z platformą Azure. Oparta na trasach obsługuje również lokacja lokacja (za pomocą dowolnego komputera) i połączenia punkt lokacja (z jednego komputera) jednocześnie.
- Należy określić jednostkę SKU, którego chcesz używać bramy. To zależy od wymagań dotyczących obciążenia, przepustowości, funkcji i umów SLA.
- Protokół BGP (Border Gateway Protocol) to opcjonalna funkcja, której można używać z usługą Azure ExpressRoute i bramami sieci VPN opartymi na trasach do propagowania lokalnych tras protokołu BGP do sieci wirtualnych.

![Sieć VPN](./media/migrate-best-practices-networking/vpn.png)
*sieci VPN typu lokacja lokacja*

**Dowiedz się więcej:**

- [Przejrzyj](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) zgodne lokalne urządzenia sieci VPN.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) bram sieci VPN.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) połączeń sieci VPN o wysokiej dostępności.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) planowanie i projektowanie bramy sieci VPN.
- [Przegląd](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) ustawień usługi VPN gateway.
- [Przegląd](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) jednostki SKU bramy.
- [Przeczytaj o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) konfigurowania protokołu BGP z bramami sieci VPN platformy Azure.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Najlepsze rozwiązanie: Konfigurowanie bramy dla bramy sieci VPN

Po utworzeniu bramy sieci VPN na platformie Azure, należy użyć specjalnego podsieć o nazwie GatewaySubnet. Podczas tworzenia tej podsieci należy zwrócić uwagę na następujące najlepsze rozwiązania:

- Długość prefiksu podsieci bramy może mieć maksymalną długość 29 (na przykład 10.119.255.248/29). Bieżący zalecane jest, że używasz długość prefiksu 27 (na przykład 10.119.255.224/27).
- Podczas definiowania przestrzeni adresowej podsieci bramy należy użyć ostatniej części przestrzeni adresowej sieci wirtualnej.
- Korzystając z platformy Azure podsieci GatewaySubnet, nigdy nie należy wdrażać żadnych maszyn wirtualnych lub innych urządzeń, takich jak Application Gateway w ramach podsieci bramy.
- Nie przypisuj grupy zabezpieczeń sieci (NSG) do tej podsieci. Spowoduje to zatrzymanie działania bramy.

**Dowiedz się więcej:**

- [Użyj tego narzędzia](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed), aby określić przestrzeń adresową IP.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Najlepsze rozwiązanie: Implementowanie Azure wirtualne sieci WAN dla oddziałów

Wiele połączeń sieci VPN Azure wirtualnego WAN jest sieci usługa, która zapewnia zoptymalizowane i automatyczne łączność gałęzi do gałęzi za pośrednictwem platformy Azure.

- Usługa Virtual WAN umożliwia łączenie urządzeń w oddziałach z platformą Azure i konfigurowanie ich komunikacji. Można to zrobić ręcznie lub za pomocą urządzeń preferowanych dostawców — partnerów usługi Virtual WAN.
- Użycie urządzeń preferowanych dostawców zapewnia prostą obsługę, łączność oraz zarządzanie konfiguracją.
- Wbudowany pulpit nawigacyjny sieci WAN na platformie Azure udostępnia na bieżąco szczegółowe informacje dotyczące rozwiązywania problemów, dzięki którym oszczędzisz czas, i umożliwia łatwe monitorowanie łączności między lokacjami w dużej skali.

**Dowiedz się więcej:** 
[Dowiedz się więcej o](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) WAN wirtualnych platformy Azure.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Najlepsze rozwiązanie: implementowanie ExpressRoute dla połączeń o kluczowym znaczeniu

Usługa Azure ExpressRoute rozszerza infrastrukturę lokalną do chmury firmy Microsoft przez tworzenie prywatnych połączeń między wirtualnym centrum danych platformy Azure i sieciami lokalnymi.

- Połączenia usługi ExpressRoute mogą znajdować się w sieci typu dowolny-dowolny (sieć VPN IP), sieci Ethernet typu punkt-punkt lub za pośrednictwem dostawcy połączenia. Nie przechodzą one przez publiczny Internet.
- Połączenia ExpressRoute zapewniają wyższy poziom zabezpieczeń, niezawodność i szybkość (10 GB/s), wraz z spójne opóźnienia.
- Usługa ExpressRoute jest przydatna w przypadku wirtualnych centrów danych, ponieważ klienci mogą uzyskać korzyści wynikające z reguł zgodności skojarzonych z połączeniami prywatnymi.
- Usługa ExpressRoute bezpośrednio można połączyć się bezpośrednio do firmy Microsoft routery przy 100Gbps na potrzeby większej przepustowości.
- Usługi ExpressRoute używa protokołu BGP w celu wymiany tras między sieciami lokalnymi, wystąpienia platformy Azure i publicznymi adresami Microsoft.

Wdrażanie połączeń usługi ExpressRoute, zazwyczaj obejmuje angażowanie dostawcy usługi ExpressRoute. Typowym sposobem szybkiego rozpoczynania pracy jest użycie najpierw sieci VPN typu lokacja-lokacja do ustanowienia połączenia między wirtualnym centrum danych i zasobami lokalnymi, a następnie przeprowadzenie migracji do połączenia usługi ExpressRoute po ustanowieniu fizycznego wzajemnego połączenia z dostawcą usługi.

**Dowiedz się więcej:**

- [Przeczytaj](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) omówienie usługi ExpressRoute.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) o usłudze ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Najlepsze rozwiązanie: Optymalizacja routingu usługi ExpressRoute za pomocą protokołu BGP społeczności

Jeśli masz wiele obwodów usługi ExpressRoute, masz więcej niż jedną ścieżkę łączenia z firmą Microsoft. W związku z tym może wystąpić routing nieoptymalny, tzn. ruch może użyć dłuższej ścieżki w celu dotarcia do firmy Microsoft lub z firmy Microsoft do sieci użytkownika. Im dłuższa ścieżka sieciowa, tym większe opóźnienie. Opóźnienie ma bezpośredni wpływ na wydajność aplikacji i środowisko użytkownika.

**Przykład:**

Zapoznajmy się z przykładem:

- masz dwa biura w USA: jedno w Los Angeles i jedno w Nowym Jorku.
- Biura są połączone w sieci WAN, który może być Twoją siecią podstawową lub dostawcą usług IP VPN.
- Dostępne są dwa obwody usługi ExpressRoute: jeden w zachodnich stanach USA i jeden we wschodnich stanach USA, które są również połączone w ramach sieci WAN. Oczywiście masz dwie ścieżki połączenia z siecią firmy Microsoft.

**Problem:**

Teraz wyobraź sobie, że dysponujesz wdrożeniem platformy Azure (np. usługą Azure App Service) zarówno w zachodnich, jak i wschodnich stanach USA.

- Aby zapewnić optymalne środowisko, użytkownicy w poszczególnych biurach uzyskują dostęp do najbliższych usług platformy Azure.
- Co chcesz się połączyć użytkowników z Los Angeles zachodnich stanach USA i użytkownikom w Nowym Jorku, wschodnie stany USA.
- Działa to w przypadku użytkowników z Wybrzeża Wschodniego, ale nie dla tych z Wybrzeża Zachodniego. Występuje następujący problem:
  - W poszczególnych obwodach usługi ExpressRoute anonsujemy zarówno prefiks dla wschodnich stanów USA na platformie Azure (23.100.0.0/16), jak i prefiks w zachodnich stanach USA na platformie Azure (13.100.0.0/16).
  - Bez znajomości regionu, z którego pochodzi danych prefiks, prefiksy nie są traktowane w inny sposób.
  - Sieć WAN może założyć, że oba prefiksy są bliżej wschodnich stanów USA niż zachodnich stanów USA, i dlatego będzie kierować użytkowników z obu biur do obwodu usługi ExpressRoute w regionie Wschodnie stany USA, zapewniając nieoptymalne środowisko dla użytkowników w biurze w Los Angeles.

![Sieć VPN](./media/migrate-best-practices-networking/bgp1.png)
*społeczności BGP niezoptymalizowane połączenia*

**Rozwiązanie:**

Aby zoptymalizować routing dla użytkowników obu biur, trzeba wiedzieć, który prefiks odpowiada zachodnim, a który wschodnim stanom USA. Możesz zakodować te informacje przy użyciu wartości społeczności BGP.

- Należy przypisać unikatową wartość społeczności BGP do każdego regionu platformy Azure. Na przykład 12076:51004 dla wschodnich i 12076:51006 dla zachodnich stanów USA.
- Skoro już to oczywiste, który prefiks należy do regionu platformy Azure, możesz skonfigurować preferowany obwód usługi ExpressRoute.
- Ponieważ do wymiany informacji o routingu używasz protokołu BGP, w celu wpłynięcia na routing możesz użyć preferencji lokalnej protokołu BGP.
- W naszym przykładzie można przypisać wyższą wartość preferencji lokalnej na 13.100.0.0/16 w zachodnich niż we wschodnich Stanach USA i podobnie wyższą wartość preferencji lokalnej na 23.100.0.0/16 we wschodnich niż w zachodnich stanach USA.
- Ta konfiguracja zapewnia, że zarówno ścieżki do firmy Microsoft są dostępne, będą łączyli się zachodnich stanach USA przy użyciu obwodu zachodnie użytkownicy w Los Angeles, gdy użytkownicy Nowy Jork nawiązać wschodnie stany USA przy użyciu obwodu Wschodnia. Routing jest zoptymalizowany po obu stronach.

![Sieć VPN](./media/migrate-best-practices-networking/bgp2.png)
*społeczności BGP zoptymalizowane pod kątem połączenia*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) na temat optymalizowania routingu.

## <a name="secure-vnets"></a>Zabezpiecz sieci wirtualnych

Odpowiedzialność za zabezpieczanie sieci wirtualnych jest podzielona między firmę Microsoft i użytkownika. Firma Microsoft oferuje wiele funkcji sieciowych, a także usług, które ułatwiają zabezpieczanie zasobów. W przypadku projektowania zabezpieczeń sieci wirtualnych najlepsze rozwiązania, które warto zastosować, obejmują implementację sieci obwodowej, użycie filtrowania i grup zabezpieczeń, zabezpieczanie dostępu do zasobów i adresów IP oraz implementowanie ochrony przed atakami.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) najlepszych rozwiązań zabezpieczeń sieciowych.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security) projektowanie pod kątem bezpiecznej sieci.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Najlepsze rozwiązanie: Implementowanie sieci obwodowej platformy Azure

Mimo że Microsoft intensywnie inwestuje w zakresie ochrony infrastruktury chmury, musisz również chronić usługi w chmurze i grupy zasobów. Wielowarstwowego podejścia do zabezpieczeń zapewnia najlepszą ochronę. Zastosowanie sieci obwodowej jest ważną częścią tej strategii obrony.

- Sieci obwodowej chroni wewnętrznych zasobów sieciowych z niezaufaną siecią.
- Jest to najbardziej zewnętrzna warstwa widoczna w Internecie. Mówiąc ogólnie, znajduje się ona między Internetem a infrastrukturą przedsiębiorstwa i przeważnie ma pewne formy ochrony po obu stronach.
- W topologii sieci typowego przedsiębiorstwa infrastrukturze podstawowej jest silnie wzmocnione na strefy, dzięki wielu wbudowanym warstwom zabezpieczeń urządzeń. Granica każdej warstwy składa się z urządzeń i punktów wymuszania zasad.
- Każda warstwa może zawierać kombinację rozwiązania zabezpieczeń sieciowych, które zawierają zapór, zapobiegania przeprowadzenie ataku typu "odmowa usługi" (DoS), systemy ochrony wykrywania/nieautoryzowanego nieautoryzowanego dostępu (IDS/IPS) i urządzenia sieci VPN.
- Wymuszanie zasad w sieci obwodowej użyć zasad zapory, listy kontroli dostępu (ACL) lub specyficznego routingu.
- Ruch przychodzący z Internetu jest przechwytywany i obsługiwany przez kombinację rozwiązań obronnych w celu blokowania ataków i szkodliwego ruchu przy jednoczesnym dopuszczaniu wiarygodnych żądań do sieci.
- Ruch przychodzący może być kierowany bezpośrednio do zasobów w sieci obwodowej. Zasób sieci obwodowej, następnie może komunikować się z innymi zasobami, które są bardziej w sieci, przeniesienie do przodu ruch do sieci po weryfikacji.

Poniższej ilustracji przedstawiono przykład sieci obwodowej jednej podsieci w sieci firmowej, z dwoma granic zabezpieczeń.

![Sieć VPN](./media/migrate-best-practices-networking/perimeter.png)
*Wdrażanie sieci obwodowej*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) wdrażanie sieć obwodowa między platformą Azure i lokalnym centrum danych.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Najlepsze rozwiązanie: ruch w sieci wirtualnej filtr z sieciowymi grupami zabezpieczeń

Sieciowe grupy zabezpieczeń zawierają wiele reguł zabezpieczeń dla ruchu przychodzącego i wychodzącego, które filtrują ruch przechodzący do i z zasobów. Filtrowanie może być przez źródłowy i docelowy adres IP, portu i protokołu.

- Sieciowe grupy zabezpieczeń zawierają reguły zabezpieczeń, które blokują lub zezwalają na ruch do sieci dla ruchu przychodzącego (lub wychodzącego ruchu sieciowego z) kilka typów zasobów platformy Azure. Dla każdej reguły można określić źródło i obiekt docelowy, port i protokół.
- Reguły sieciowej grupy zabezpieczeń są oceniane według priorytetu, korzystając z informacji 5 krotka (źródłowy, port źródłowy, docelowy, port docelowy i protokół) do blokują lub zezwalają na ruch.
- Rekord przepływu tworzony jest dla istniejących połączeń. Komunikacja jest dozwolona lub zablokowana na podstawie stanu połączenia z rekordu przepływu.
- Przepływ rekord umożliwia sieciowej grupy zabezpieczeń można stanowych. Jeśli na przykład zostanie określona reguła zabezpieczeń dla ruchu wychodzącego do dowolnego adresu za pośrednictwem portu 80, nie trzeba określać reguły zabezpieczeń ruchu przychodzącego, aby odpowiadać na ruch wychodzący. Należy tylko określić regułę zabezpieczeń dla ruchu przychodzącego w przypadku, jeśli komunikacja jest inicjowana zewnętrznie.
- Jest to również prawdziwe w odwrotnym przypadku. Ruch przychodzący jest dozwolony przez port, nie trzeba określić regułę zabezpieczeń dla ruchu wychodzącego, aby odpowiadać na ruch przychodzący przez port.
- Istniejące połączenia nie są przerwane po usunięciu reguły zabezpieczeń, która umożliwiała przepływ. Przepływy ruchu są przerywane po zakończeniu połączenia, gdy przez co najmniej kilka minut nie ma ruchu z żadnej strony.
- Podczas tworzenia sieciowych grup zabezpieczeń, należy utworzyć few jak to możliwe, ale tyle, które są niezbędne.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Najlepsze rozwiązanie: bezpieczny ruch wschód/zachód i północ/południe

W przypadku zabezpieczania sieci wirtualnych ważne jest rozważenie wektorów ataków.

- Użycie tylko sieciowych grup zabezpieczeń podsieci upraszcza środowisko, ale zabezpiecza wyłącznie ruch do podsieci. Jest to ruch typu północ/południe.
- Ruch między maszynami wirtualnymi w tej samej podsieci jest określany jako ruch Wschód/Zachód.
- Ważne jest używanie obu rodzajów ochrony, ponieważ jeśli haker uzyska dostęp z zewnątrz, zostanie zatrzymany podczas próby dołączenia maszyn znajdujących się w tej samej podsieci.

### <a name="use-service-tags-on-nsgs"></a>Za pomocą tagów usługi na sieciowych grup zabezpieczeń

Tag usługi reprezentuje grupę prefiksów adresów IP. Przy użyciu tagu usługi pomaga zminimalizować złożoność tworzenia reguły sieciowej grupy zabezpieczeń.

- Podczas tworzenia reguł tagów usługi można używać zamiast konkretnych adresów IP.
- Firma Microsoft zarządza prefiksami adresów skojarzony z tag usługi i automatycznie aktualizuje tag usługi, po zmianie adresów.
- Nie można utworzyć własnego tagu usługi ani określić, jakie adresy IP są uwzględniane w tagu.

Tagi usługi eliminują czynności wykonywane ręcznie z procesu przypisywania reguły do grup usług platformy Azure. Na przykład, jeśli chcesz zezwolić w podsieci sieci wirtualnej, zawierającej dostęp serwerów sieci web do usługi Azure SQL Database, możesz można utworzyć regułę dla ruchu wychodzącego do portu 1433 i użyj **Sql** tag usługi.

- Ten tag **Sql** określa prefiksy adresów usług Azure SQL Database i Azure SQL Data Warehouse.
- W przypadku określenia wartości **Sql** dozwolony lub blokowany jest ruch do usługi Sql.
- Jeśli chcesz zezwolić na dostęp do usługi **Sql** w konkretnym regionie, możesz określić region. Jeśli na przykład chcesz zezwolić na dostęp do usługi Azure SQL Database tylko w regionie Wschodnie stany USA, możesz określić **Sql.EastUS** jako tag usługi.
- Tag reprezentuje usługę, ale nie konkretne wystąpienia usługi. Na przykład tag reprezentuje usługę Azure SQL Database, ale nie zawiera określonej bazy danych SQL lub serwera.
- Wszystkie prefiksy adresów reprezentowane przez ten tag są również reprezentowane przez tag **Internet**.

**Dowiedz się więcej:**

- [Przeczytaj o](https://docs.microsoft.com/azure/virtual-network/security-overview) sieciowych grup zabezpieczeń.
- [Przegląd](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) tagi usługi dostępne dla sieciowych grup zabezpieczeń.

## <a name="best-practice-use-application-security-groups"></a>Najlepsze rozwiązanie: przy użyciu grup zabezpieczeń aplikacji

Grupy zabezpieczeń aplikacji umożliwiają skonfigurowanie zabezpieczeń sieci jako naturalnego rozszerzenia struktury aplikacji.

- Można grupować maszyny wirtualne i definiować zasady zabezpieczeń sieci na podstawie grup zabezpieczeń aplikacji.
- Grupy zabezpieczeń aplikacji umożliwiają ponowne używanie zasady zabezpieczeń na dużą skalę bez ręcznej obsługi jawnych adresów IP.
- Grupy zabezpieczeń aplikacji obsługuje złożoność jawnych adresów IP i wiele zestawów reguł, co pozwala skupić się na logice biznesowej.

**Przykład:**

![Grupa zabezpieczeń aplikacji](./media/migrate-best-practices-networking/asg.png)
*Przykład grupy zabezpieczeń aplikacji*

**Interfejs sieciowy** | **Grupy zabezpieczeń aplikacji**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- W naszym przykładzie każdy interfejs sieciowy należy tylko do jednej grupy zabezpieczeń aplikacji, ale w rzeczywistości interfejs może należeć do wielu grup, zgodnie z ograniczeniami platformy Azure.
- Żaden z interfejsów sieciowych nie ma skojarzonej sieciowej grupy zabezpieczeń. Grupa NSG1 została skojarzona z obiema podsieciami i zawiera poniższe reguły.

<!--markdownlint-disable MD033 -->

**Nazwa reguły** | **Przeznaczenie** | **Szczegóły**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Zezwalać na ruch z Internetu do serwerów sieci web. Ruch przychodzący z Internetu odmowa przez DenyAllInbound domyślną regułą zabezpieczeń, dzięki czemu nie dodatkowe reguły jest wymagany w przypadku AsgLogic lub AsgDb grup zabezpieczeń aplikacji. | Priorytet: 100<br/><br/> Źródło: Internet<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgWeb<br/><br/> Port docelowy: 80<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwalaj na.
Deny-Database-All | Domyślna reguła zabezpieczeń AllowVNetInBound zezwala na całą komunikację między zasobami w tej samej sieci wirtualnej, ta zasada jest potrzebna w celu blokowania ruchu ze wszystkich zasobów. | Priorytet: 120<br/><br/> Źródło: *<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: wszystkie<br/><br/> Dostęp: odmowa.
Allow-Database-BusinessLogic | Zezwolenie na ruch z grupy zabezpieczeń aplikacji AsgLogic do grupy zabezpieczeń aplikacji AsgDb. Priorytet tej reguły jest wyższy niż priorytet reguły Deny-Database-All i jest ona przetwarzana przed tą regułą, dlatego ruch z grupy zabezpieczeń aplikacji AsgLogic jest dozwolony, a cały pozostały ruch jest blokowany. | Priorytet: 110<br/><br/> Źródło: AsgLogic<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwalaj na.

<!--markdownlint-enable MD033 -->

- Reguły określające grupę zabezpieczeń aplikacji jako źródło lub obiekt docelowy są stosowane tylko do interfejsów sieciowych, które są elementami członkowskimi grupy zabezpieczeń aplikacji. Jeśli interfejs sieciowy nie jest elementem członkowskim grupy zabezpieczeń aplikacji, reguła nie jest stosowana do tego interfejsu sieciowego, mimo że grupa zabezpieczeń sieci jest skojarzona z podsiecią.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) o grupach zabezpieczeń aplikacji.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Najlepsze rozwiązanie: bezpieczny dostęp do usługi PaaS za pomocą punktów końcowych usługi sieci wirtualnej

Punkty końcowe usługi sieci wirtualnej rozszerzenie Twojej sieci wirtualnej prywatną przestrzeń adresową oraz tożsamość do usług platformy Azure za pośrednictwem bezpośredniego połączenia.

- Punkty końcowe umożliwiają zabezpieczanie krytycznych zasobów usługi platformy Azure tylko do sieci wirtualnych. Ruch z sieci wirtualnej do usługi platformy Azure zawsze pozostaje w sieci szkieletowej platformy Microsoft Azure.
- Przestrzeń prywatnych adresów sieci wirtualnej mogą nakładające się przestrzenie i dlatego nie może być używany do jednoznacznego identyfikowania ruch pochodzący z sieci wirtualnej.
- Po włączeniu punktów końcowych usługi w sieci wirtualnej można zabezpieczyć zasoby usługi platformy Azure przez dodanie reguły sieci wirtualnej do zasobów usługi. To zapewnia wyższy poziom zabezpieczeń, w pełni usunięcie publicznego dostępu do Internetu do zasobów i zezwolenie na ruch tylko z sieci wirtualnej.

![Punkty końcowe usługi](./media/migrate-best-practices-networking/endpoint.png)
*Punkty końcowe usługi*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o punktach końcowych usługi sieci wirtualnej.

## <a name="best-practice-control-public-ip-addresses"></a>Najlepsze rozwiązanie: kontrolowanie publiczne adresy IP

Publiczne adresy IP na platformie Azure może być skojarzony z maszynami wirtualnymi, modułami równoważenia obciążenia, bramy application Gateway oraz bram sieci VPN.

- Publiczne adresy IP umożliwiają zasobom Internetu komunikację dla ruchu przychodzącego z zasobami platformy Azure i zasobów platformy Azure do komunikowania się ruch wychodzący do Internetu.
- Publiczne adresy IP są tworzone przy użyciu podstawowej lub standardowej jednostki SKU, między którymi występuje kilka różnic. Standardowe jednostki SKU można przypisać do dowolnej usługi, ale zazwyczaj są one konfigurowane na maszynach wirtualnych, w modułach równoważenia obciążenia i w bramach aplikacji.
- Należy zauważyć, że podstawowa publiczny adres IP nie ma sieciową grupę zabezpieczeń konfigurowane automatycznie. Musisz skonfigurować własne i przypisać zasady kontroli dostępu. Adresy IP standardowej jednostki SKU mają domyślnie przypisane reguły i sieciową grupę zabezpieczeń.
- Najlepszym rozwiązaniem jest maszyn wirtualnych nie powinien mieć skonfigurowaną publicznego adresu IP.
  - Jeśli potrzebny jest otwarty port, powinien on być przeznaczony tylko dla usług internetowych, tak jak port 80 lub 443.
  - Standardowe porty zarządzania zdalnego, takie jak SSH (22) i RDP (3389), powinny mieć ustawioną odmowę, tak jak wszystkie inne porty używające sieciowych grup zabezpieczeń.
- Lepszym rozwiązaniem jest umieszczenie maszyn wirtualnych za modułem równoważenia obciążenia platformy Azure lub bramą aplikacji. Jeśli jest potrzebny dostęp do portów zarządzania zdalnego, można użyć dostępu just-in-time do maszyny wirtualnej w usłudze Azure Security Center.

**Dowiedz się więcej:**

- [Publiczne adresy IP na platformie Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses)
- [Zarządzanie dostępem do maszyny wirtualnej przy użyciu funkcji just in Time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Korzystanie z zalet funkcji zabezpieczeń platformy Azure dla sieci

Platforma Azure ma funkcje zabezpieczeń platformy, które są łatwe w użyciu i zapewniają rozbudowane środki zaradcze w przypadku typowych ataków w sieci. Obejmują one zaporę platformy Azure, zaporę aplikacji internetowej i usługę Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Najlepsze rozwiązanie: wdrażanie zapory platformy Azure

Azure Firewall to zarządzana, sieciowa usługa zabezpieczeń oparta na chmurze, która zabezpiecza zasoby sieci wirtualnej. Jest to w pełni stanowa zapora zarządzana z wbudowaną wysoką dostępnością i możliwością nieograniczonego skalowania w chmurze.

![Punkty końcowe usługi](./media/migrate-best-practices-networking/firewall.png)
*zapory usługi Azure*

- Usługa Azure Firewall może centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych.
- Usługa Azure Firewall korzysta ze statycznego publicznego adresu IP dla zasobów sieci wirtualnej, co umożliwia zewnętrznym zaporom identyfikowanie ruchu pochodzącego z sieci wirtualnej.
- Zaporę platformy Azure jest w pełni zintegrowana z usługą Azure Monitor rejestrowania i analizy.
- Najlepszym rozwiązaniem podczas tworzenia reguł zapory usługi Azure należy użyć tagów w pełni kwalifikowaną nazwę domeny do tworzenia reguł.
  - FQDN tag reprezentuje grupę nazw FQDN skojarzone z dobrze znanych usług firmy Microsoft.
  - Za pomocą tagu w pełni kwalifikowaną nazwę domeny umożliwia wymagane wychodzącego ruchu sieciowego przez zaporę.
- Na przykład aby ręcznie zezwolić na Windows Update ruchu sieciowego przez zaporę, będziesz potrzebować umożliwiający tworzenie wielu reguł aplikacji. Przy użyciu tagów FQDN tworzysz regułę aplikacji i dołączasz tag Windows Update. Z tą regułą w miejscu ruchu sieciowego do punktów końcowych usługi Microsoft Windows Update może przepływać przez zaporę.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/firewall/overview) zapory platformy Azure.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/firewall/fqdn-tags) tagów w pełni kwalifikowaną nazwę domeny.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Najlepsze rozwiązanie: wdrażanie zapory aplikacji sieci Web (WAF)

Aplikacje internetowe coraz częściej stają się obiektami złośliwych ataków wykorzystujących znane luki w zabezpieczeniach. Luki w zabezpieczeniach to ataki przez wstrzyknięcie kodu SQL i ataki z użyciem skryptów między witrynami. Zapobieganie atakom na takie w kodzie aplikacji może stanowić wyzwanie i mogą wymagać rygorystycznego przestrzegania harmonogramu konserwacji, poprawek i monitorowania na poziomie wielu warstw topologii aplikacji. Scentralizowana zapora aplikacji internetowej ułatwia zarządzanie zabezpieczeniami oraz ułatwia administratorom aplikacji ochronę przed zagrożeniami lub intruzami. Zapora aplikacji sieci web może reagować na zagrożenia bezpieczeństwa szybciej, poprzez wdrażanie poprawek znanych luk w zabezpieczeniach w centralnej lokalizacji zamiast zabezpieczanie poszczególnych aplikacjach sieci web. Istniejące bramy Application Gateway można łatwo przekonwertować na bramę Application Gateway obsługującą zaporę aplikacji internetowej.

Zapora aplikacji internetowej to funkcja usługi Azure Application Gateway.

- Zapora aplikacji sieci Web zapewnia scentralizowaną ochronę aplikacji sieci web, przed typowymi programami wykorzystującymi luki i lukami w zabezpieczeniach.
- Zapora aplikacji internetowej chroni bez modyfikacji kodu zaplecza.
- Może ona jednocześnie chronić wiele aplikacji internetowych za bramą aplikacji.
- Zapora aplikacji sieci Web jest zintegrowana z usługą Azure Security Center.
- Reguły zapory aplikacji internetowej i grupy reguł można dostosować tak, aby spełniały wymagania aplikacji.
- Najlepszym rozwiązaniem zapory aplikacji sieci Web należy używać z przodu, w żadnej aplikacji przeznaczonych dla sieci web, w tym aplikacje na maszynach wirtualnych platformy Azure lub usługi Azure App Service.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/application-gateway/waf-overview) zapory aplikacji sieci Web.
- [Przejrzyj](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) ograniczenia i wykluczenia dotyczące zapory aplikacji internetowej.

## <a name="best-practice-implement-azure-network-watcher"></a>Najlepsze rozwiązanie: Implementowanie usługi Azure Network Watcher

Usługa Azure Network Watcher udostępnia narzędzia umożliwiające monitorowanie, zasoby i materiały w sieci wirtualnej platformy Azure. Na przykład można monitorować komunikację między maszyną wirtualną i punktem końcowym, takim jak inna maszyna wirtualna lub nazwa FQDN, wyświetlać zasoby i relacje zasobów w sieci wirtualnej lub diagnozować problemy z ruchem sieciowym.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Dzięki usłudze Network Watcher można monitorować i diagnozować problemy z siecią bez konieczności logowania się na maszynach wirtualnych.
- Możesz wyzwalać Przechwytywanie pakietów przez ustawienie alertów i uzyskać dostęp do informacji o wydajności w czasie rzeczywistym na poziomie pakietów. Gdy pojawi się problem, można zbadać je szczegółowo.
- Najlepszym rozwiązaniem jest użycie usługi Network Watcher do przeglądania dzienników przepływów sieciowych grup zabezpieczeń.
  - Dzienniki przepływu sieciowych grup zabezpieczeń w usługi Network Watcher umożliwiają wyświetlanie informacji na temat przychodzący i wychodzący ruch IP sieciowej grupy zabezpieczeń.
  - Dzienniki przepływów są pisane w formacie JSON.
  - Dzienniki przepływów przedstawiają przepływy wychodzące i przychodzące dla każdej reguły, interfejs sieciowy, do którego odnosi się przepływ, 5-krotkowe informacje o przepływie (źródłowy/docelowy adres IP, port źródłowy/docelowy i protokół) oraz informację zezwoleniu na ruch albo jego zablokowaniu.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/network-watcher) usługi Network Watcher.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) dzienniki przepływu o sieciowej grupy zabezpieczeń.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Korzystaj z narzędzi partnera w witrynie Azure Marketplace

Bardziej złożone topologie sieci można skorzystać z produktów zabezpieczeń od naszych partnerów firmy Microsoft, która znajduje się w określonej sieci wirtualne urządzenia (urządzenia WUS).

- Wirtualne urządzenie sieciowe to maszyna wirtualna wykonująca funkcję sieciową, np. funkcję zapory, optymalizacji WAN lub inną.
- Wirtualne urządzenia sieciowe wzmacniają zabezpieczenia sieci wirtualnej i funkcje sieciowe. Można je wdrażać w przypadku zapór o wysokiej dostępności, zapobiegania włamaniom, wykrywania intruzów, zapór aplikacji internetowych, optymalizacji sieci WAN, routingu, równoważenia obciążenia, sieci VPN, zarządzania certyfikatami, usługi Active Directory i uwierzytelniania wieloskładnikowego.
- Urządzenie WUS jest dostępny od wielu dostawców z [portalu Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Najlepsze rozwiązanie: wdrożenie zapory i urządzenia WUS w sieci Centrum

W centrum sieć obwodowa (z dostępem do Internetu) jest zazwyczaj zarządzana za pomocą zapory platformy Azure, farmy zapór lub zapory aplikacji internetowej. Przeanalizujmy następujące porównania.

<!--markdownlint-disable MD033 -->

**Typ zapory** | **Szczegóły**
--- | ---
Zapory aplikacji internetowych | Aplikacje internetowe są powszechnie używane oraz często mają luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki.<br/><br/> Sieciowi są przeznaczone do wykrywania ataków na aplikacje sieci web (HTTP/HTTPS), w szczególności niż ogólny zapory.<br/><br/> W porównaniu z tradycyjną technologią zapory aplikacji internetowych mają zestaw konkretnych funkcji chroniących wewnętrzne serwery internetowe przed zagrożeniami.
Azure Firewall | Podobnie jak w przypadku farm zapór wirtualnych urządzeń sieciowych usługa Azure Firewall używa wspólnego mechanizmu administrowania oraz zestawu reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach szprych i kontrolować dostęp do sieci lokalnych.<br/><br/> Usługa Azure Firewall ma wbudowaną skalowalność.
Zapory wirtualnych urządzeń sieciowych | Podobnie jak urządzenie WUS zapory usługi Azure farm zapory mają wspólnego mechanizmu administracji i zestaw reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach gwiazdy i kontrolować dostęp do sieci lokalnej.<br/><br/> Zapory wirtualnych urządzeń sieciowych można ręcznie skalować za modułem równoważenia obciążenia.<br/><br/> Chociaż zapory urządzenie WUS nie ma mniej specjalistyczne oprogramowanie niż zapory aplikacji sieci Web ma szerszy zakres aplikacji do filtrowania i sprawdzić ruch wychodzący i przychodzący dowolnego typu.<br/><br/> Jeśli chcesz korzystać z wirtualnego urządzenia sieciowego, możesz je znaleźć w portalu Azure Marketplace.

<!--markdownlint-enable MD033 -->

Zalecamy użycie jednego zestawu zapór Azure Firewall (lub wirtualnych urządzeń sieciowych) dla ruchu pochodzącego z Internetu oraz innego zestawu dla ruchu pochodzącego ze środowiska lokalnego.

- Przy użyciu tylko jeden zestaw zapory dla obu stanowi zagrożenie bezpieczeństwa, ponieważ on nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego.
- Używanie oddzielnych warstw zapory zmniejsza złożoność sprawdzania zasad zabezpieczeń i wyraźnie pokazuje, które reguły dotyczą którego przychodzącego żądania sieciowego.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) przy użyciu urządzeń WUS w sieci wirtualnej platformy Azure.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z innymi najlepszymi rozwiązaniami:

- [Najlepsze rozwiązania](./migrate-best-practices-security-management.md) w zakresie zabezpieczeń i zarządzania po migracji.
- [Najlepsze praktyki](./migrate-best-practices-costs.md) usługi cost management po migracji.
