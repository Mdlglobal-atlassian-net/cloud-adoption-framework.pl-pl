---
title: Najlepsze rozwiązania dotyczące konfigurowania sieci pod kątem obciążeń migrowanych do platformy Azure
description: Po przeprowadzeniu migracji na platformę Azure należy zapoznać się z najlepszymi rozwiązaniami dotyczącymi konfigurowania sieci na potrzeby migrowanych obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a8a4bc504c085f461cb70f561670fe55a20a544b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803878"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące konfigurowania sieci pod kątem obciążeń migrowanych do platformy Azure

Po zaplanowaniu i zaprojektowaniu migracji jednym z najważniejszych kroków — oprócz samej migracji jest zaprojektowanie i zaimplementowanie sieci platformy Azure. W tym artykule opisano najlepsze rozwiązania dotyczące sieci w przypadku migrowania do implementacji usług IaaS i PaaS na platformie Azure.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule dotyczą funkcji usług i platformy Azure dostępnych w momencie pisania artykułu. Funkcje i możliwości zmieniają się w miarę upływu czasu. Nie wszystkie rekomendacje mogą obowiązywać dla danego wdrożenia, więc wybierz te, które są odpowiednie w Twoim przypadku.

## <a name="design-virtual-networks"></a>Projektowanie sieci wirtualnych

Platforma Azure oferuje sieci wirtualne:

- Zasoby platformy Azure komunikują się prywatnie, bezpośrednio i bezpiecznie ze sobą za pośrednictwem sieci wirtualnych.
- Można skonfigurować połączenia punktów końcowych w sieciach wirtualnych dla maszyn wirtualnych i usług, które wymagają komunikacji internetowej.
- Sieć wirtualna jest logiczną izolacją chmury platformy Azure przeznaczoną dla subskrypcji.
- W każdej subskrypcji platformy Azure oraz w każdym regionie świadczenia usługi Azure możesz zaimplementować wiele sieci wirtualnych.
- Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych.
- Sieci wirtualne mogą zawierać prywatne i publiczne adresy IP zdefiniowane w dokumencie [RFC 1918](https://tools.ietf.org/html/rfc1918), wyrażone w notacji CIDR. Publiczne adresy IP określone w przestrzeni adresowej sieci wirtualnej nie są bezpośrednio dostępne z Internetu.
- Sieci wirtualne mogą łączyć się ze sobą za pomocą komunikacji równorzędnej sieci wirtualnej. Połączone sieci wirtualne mogą znajdować się w tym samym lub różnych regionach. Dzięki temu zasoby w jednej sieci wirtualnej mogą łączyć się z zasobami w innych sieciach wirtualnych.
- Domyślnie platforma Azure kieruje ruchem między podsieciami w sieci wirtualnej, połączonymi sieciami wirtualnymi, sieciami lokalnymi oraz Internetem.

Podczas planowania topologii sieci wirtualnej należy wziąć pod uwagę sposób rozmieszczenia przestrzeni adresowej IP, sposób implementacji sieci gwiazdy, sposób segmentowania sieci wirtualnych w podsieci, konfigurowanie systemu DNS i implementowanie stref dostępności platformy Azure.

## <a name="best-practice-plan-ip-addressing"></a>Najlepsze rozwiązanie: Planowanie adresowania IP

Gdy tworzysz sieci wirtualne w ramach migracji, ważne jest zaplanowanie przestrzeni adresowej IP sieci wirtualnej.

- Należy przypisać przestrzeń adresową, która nie jest większa od zakresu CIDR /16 dla każdej sieci wirtualnej. Sieci wirtualne zezwalają na korzystanie z 65 536 adresów IP, a przypisanie prefiksu mniejszego niż /16 powoduje utratę adresów IP. Ważne jest, aby nie tracić adresów IP, nawet jeśli znajdują się w zakresach prywatnych zdefiniowanych w dokumencie RFC 1918.
- Przestrzeń adresowa sieci wirtualnej nie powinna nakładać się z zakresami sieci lokalnych.
- Nie należy używać translatora adresów sieciowych (NAT).
- Nakładające się adresy mogą spowodować, że nie będzie można połączyć sieci, a routing nie będzie działać prawidłowo. Jeśli sieci się nakładają, należy ponownie zaprojektować sieć lub użyć translatora adresów sieciowych (NAT).

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) sieci wirtualnych platformy Azure.
- [Przeczytaj](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) często zadawane pytania dotyczące sieci.
- [Dowiedz](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) się więcej na temat ograniczeń sieci.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Najlepsze rozwiązanie: implementowanie topologii sieci gwiazdy i gwiazdy

Topologia sieci piasty i szprych izoluje obciążenia przy jednoczesnym udostępnianiu usług, takich jak tożsamość i zabezpieczenia.

- Piasta to sieć wirtualna platformy Azure, pełni rolę centralnego punktu łączności.
- Szprychy to sieci wirtualne, które łączą się z siecią wirtualną piasty przy użyciu komunikacji równorzędnej sieci wirtualnych.
- Usługi udostępnione są wdrażane w piaście, a poszczególne obciążenia są wdrażane jako szprychy.

Rozważ następujące źródła:

- Implementacja topologii gwiazdy na platformie Azure umożliwia centralizowanie typowych usług, takich jak połączenia z sieciami lokalnymi, zapory i izolacja między sieciami wirtualnymi. Sieć wirtualna piasty zapewnia centralny punkt łączności z sieciami lokalnymi oraz miejsce do hostowania użycia usług przez obciążenia hostowane w sieciach wirtualnych szprych.
- Konfiguracja gwiazdy jest zwykle używana przez większe przedsiębiorstwa. W mniejszych sieciach można zastosować prostsze projekty, aby zaoszczędzić na kosztach i zredukować złożoność.
- Sieci wirtualne szprych mogą być używane do izolowania obciążeń w poszczególnych szprychach zarządzanych oddzielnie od innych szprych. Każde obciążenie może zawierać wiele warstw i wiele podsieci połączonych za pośrednictwem modułów równoważenia obciążenia platformy Azure.
- Sieci wirtualne gwiazdy można implementować w różnych grupach zasobów, a nawet w różnych subskrypcjach. W przypadku komunikacji równorzędnej sieci wirtualnych w różnych subskrypcjach subskrypcje mogą być kojarzone z tymi samymi lub różnymi dzierżawami usługi Azure Active Directory (Azure AD). Umożliwia to zdecentralizowane zrządzanie każdym obciążeniem, a jednocześnie udostępnianie usług obsługiwanych w sieci będącej piastą.

![Zarządzanie zmianami](./media/migrate-best-practices-networking/hub-spoke.png)
*Topologia gwiazdy*

**Dowiedz się więcej:**

- [Poczytaj](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) o topologii gwiazdy.
- Uzyskaj rekomendacje dotyczące sieci w przypadku uruchamiania maszyn wirtualnych platformy Azure w systemach [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) i [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm).
- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) o komunikacji równorzędnej sieci wirtualnych.

## <a name="best-practice-design-subnets"></a>Najlepsze rozwiązanie: Zaprojektuj podsieci

Aby zapewnić izolację w sieci wirtualnej, należy posegmentować ją na jedną lub więcej podsieci i przypisać części przestrzeni adresowej sieci wirtualnej do każdej podsieci.

- W każdej sieci wirtualnej można utworzyć wiele podsieci.
- Domyślnie platforma Azure kieruje ruchem między wszystkimi podsieciami w sieci wirtualnej.
- Decyzje dotyczące podsieci opierają się na wymaganiach technicznych i organizacyjnych.
- Podsieci są tworzone przy użyciu notacji CIDR.
- Podczas decydowania o zakresie sieci dla podsieci należy pamiętać, że platforma Azure zachowuje pięć adresów IP z każdej podsieci, których nie można używać. Jeśli na przykład utworzysz najmniejszą dostępną podsieć /29 (z ośmioma adresami IP), platforma Azure zachowa pięć adresów, więc będziesz mieć tylko trzy możliwe do użycia adresy, które można przypisać do hostów w podsieci.
- W większości przypadków należy użyć/28 jako najmniejszej podsieci.

**Przykład:**

W tabeli przedstawiono przykład sieci wirtualnej z przestrzenią adresową 10.245.16.0/20 podzieloną na podsieci na potrzeby planowanej migracji.

**Podsieć** | **CIDR** | **Adresy** | **Korzystanie**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Maszyny wirtualne bazy danych

**Dowiedz się więcej:**

- [Dowiedz](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) się więcej na temat projektowania podsieci.
- [Dowiedz się](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), w jaki sposób fikcyjna firma (Contoso) przygotowała infrastrukturę sieciową do migracji.

## <a name="best-practice-set-up-a-dns-server"></a>Najlepsze rozwiązanie: Konfigurowanie serwera DNS

Platforma Azure domyślnie dodaje serwer DNS podczas wdrażania sieci wirtualnej. Dzięki temu można szybko tworzyć sieci wirtualne i wdrażać zasoby. Jednak ten serwer DNS zapewnia tylko usługi dla zasobów w tej sieci wirtualnej. Jeśli chcesz połączyć wiele sieci wirtualnych razem lub połączyć się z serwerem lokalnym z sieci wirtualnych, potrzebujesz dodatkowych możliwości rozpoznawania nazw. Na przykład możesz potrzebować usługi Active Directory do rozpoznawania nazw DNS między sieciami wirtualnymi. W tym celu należy wdrożyć własny niestandardowy serwer DNS na platformie Azure.

- Serwery DNS w sieci wirtualnej mogą przekazywać zapytania DNS do cyklicznego programu rozpoznawania nazw na platformie Azure. Pozwala to na rozpoznawanie nazw hostów w danej sieci wirtualnej. Na przykład kontroler domeny działający na platformie Azure może odpowiadać na zapytania DNS dotyczące własnych domen i przekazywać wszystkie inne zapytania do platformy Azure.
- Przekazywanie dalej w systemie DNS umożliwia maszynom wirtualnym wyświetlanie zasobów lokalnych (za pośrednictwem kontrolera domeny) i nazw hostów udostępnianych przez platformę Azure (przy użyciu programu do przekazywania dalej). Dostęp do cyklicznych programów rozpoznawania nazw na platformie Azure jest udostępniany przy użyciu wirtualnego adresu IP 168.63.129.16.
- Przekazywanie dalej w systemie DNS umożliwia również rozpoznawanie nazw DNS między sieciami wirtualnymi i umożliwia maszynom lokalnym rozpoznawanie nazw hostów udostępnianych przez platformę Azure.
  - Aby można było rozpoznać nazwę hosta maszyny wirtualnej, maszyna wirtualna serwera DNS musi znajdować się w tej samej sieci wirtualnej i musi być skonfigurowana do przekazywania zapytań o nazwy hosta na platformę Azure.
  - Ponieważ sufiks DNS jest inny w każdej sieci wirtualnej, można użyć reguł przekazywania warunkowego w celu wysyłania zapytań DNS do odpowiedniej sieci wirtualnej w celu rozpoznania.
- W przypadku korzystania z własnych serwerów DNS można określić wiele serwerów DNS dla każdej sieci wirtualnej. Można również określić wiele serwerów DNS dla każdego interfejsu sieciowego (w przypadku usługi Azure Resource Manager) lub dla usługi w chmurze (w przypadku klasycznego modelu wdrażania).
- Serwery DNS określone dla interfejsu sieciowego lub usługi w chmurze mają pierwszeństwo przed serwerami DNS określonymi dla sieci wirtualnej.
- W modelu wdrażania usługi Azure Resource Manager można określić serwery DNS dla sieci wirtualnej i interfejsu sieciowego, ale najlepszym rozwiązaniem jest użycie ustawienia tylko w sieciach wirtualnych.

    ![Serwery DNS](./media/migrate-best-practices-networking/dns2.png) *serwery DNS dla sieci wirtualnej*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) o rozpoznawaniu nazw podczas korzystania z własnego serwera DNS.
- [Dowiedz się więcej](../../ready/azure-best-practices/naming-and-tagging.md) o regułach i ograniczeniach nazewnictwa DNS.

## <a name="best-practice-set-up-availability-zones"></a>Najlepsze rozwiązanie: ustawienie strefy dostępności

Strefy dostępności zwiększają wysoką dostępność, aby chronić aplikacje i dane przed awariami centrów danych.

- Strefy dostępności to unikatowe fizyczne lokalizacje w regionie świadczenia usługi Azure.
- Każda strefa składa się z co najmniej jednego centrum danych wyposażonego w niezależne zasilanie, chłodzenie i sieć.
- W celu zapewnienia odporności istnieją co najmniej trzy osobne strefy we wszystkich włączonych regionach.
- Fizyczna separacja stref dostępności w ramach regionu chroni aplikacje i dane przed awariami centrum danych.
- Usługi strefowo nadmiarowe replikują aplikacje i dane w strefach dostępności, aby chronić je przed pojedynczymi punktami awarii. - - Dzięki strefom dostępności platforma Azure oferuje umowę SLA gwarantującą czas działania maszyny wirtualnej na poziomie 99,99%.

    ![Strefa dostępności](./media/migrate-best-practices-networking/availability-zone.png) *strefy dostępności*

- Wysoką dostępność można zaplanować i utworzyć w architekturze migracji przez umieszczanie zasobów obliczeniowych, magazynu, sieci i danych w ramach tej samej strefy, a następnie replikowanie ich w innych strefach. Usługi platformy Azure, które obsługują strefy dostępności, dzielą się na dwie kategorie:
  - Strefowy usług: zasób jest skojarzona z określonej strefy. Na przykład maszyny wirtualne, dyski zarządzane, adresy IP.
  - Strefowo nadmiarowe usług: zasób jest automatycznie replikowana w strefach. Na przykład magazyn strefowo nadmiarowy, usługa Azure SQL Database.
- Aby zapewnić strefową odporność na uszkodzenia, można wdrożyć standardowy moduł równoważenia obciążenia platformy Azure z obciążeniami internetowymi lub warstwami aplikacji.

    ![Moduł równoważenia obciążenia](./media/migrate-best-practices-networking/load-balancer.png) *modułu równoważenia obciążenia*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/availability-zones/az-overview) stref dostępności.

## <a name="design-hybrid-cloud-networking"></a>Projektowanie sieci w chmurze hybrydowej

W przypadku pomyślnej migracji najważniejsze jest połączenie lokalnych sieci firmowych z platformą Azure. Dzięki temu można utworzyć zawsze włączone połączenie znane jako sieć hybrydowa w chmurze, w którym usługi są dostarczane z chmury platformy Azure do użytkowników w firmie. Istnieją dwie opcje tworzenia sieci tego typu:

- **Sieć VPN lokacja lokacja:** nawiązaniem połączenia lokacja lokacja między urządzeniem sieci VPN zgodne w środowisku lokalnym i bramą Azure VPN gateway, które zostało wdrożone w sieci wirtualnej. Każdy autoryzowany zasób lokalny może uzyskać dostęp do sieci wirtualnych. Komunikacja między lokacjami jest wysyłana przez szyfrowany tunel za pośrednictwem Internetu.
- **Usługa ExpressRoute systemu Azure:** nawiązania połączenia usługi Azure ExpressRoute między siecią lokalną i platformę Azure za pośrednictwem partnera usługi ExpressRoute. To połączenie jest prywatne i ruch nie przechodzi przez Internet.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) o sieci w chmurze hybrydowej.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Najlepsze rozwiązanie: Implementowanie wysokiej dostępności sieci VPN typu lokacja lokacja

Aby zaimplementować sieć VPN typu lokacja-lokacja, należy skonfigurować bramę sieci VPN na platformie Azure.

- Brama sieci VPN jest określonym typem bramy wirtualnej, który wysyła zaszyfrowany ruch sieciowy między siecią wirtualną platformy Azure a lokalizacją lokalną za pośrednictwem publicznego Internetu.
- Brama sieci VPN może również wysyłać szyfrowany ruch sieciowy między usługą Azure sieci wirtualnych za pośrednictwem sieci firmy Microsoft.
- Każda sieć wirtualna może mieć tylko jedną bramę sieci VPN.
- Możesz utworzyć wiele połączeń do tej samej bramy sieci VPN. W przypadku utworzenia wielu połączeń wszystkie tunele VPN współdzielą dostępną przepustowość bramy.
- Każda brama Azure VPN Gateway składa się z dwóch wystąpień działających w konfiguracji aktywne-w gotowości.
  - W przypadku planowanej konserwacji lub nieplanowanych zakłóceń działania aktywnego wystąpienia następuje przejście w tryb failover, a wystąpienie w trybie gotowości automatycznie przejmuje zadanie i wznawia połączenie typu lokacja-lokacja lub połączenie między sieciami wirtualnymi.
  - Przełączenie powoduje krótką przerwę w działaniu.
  - W przypadku planowanej konserwacji łączność powinna zostać przywrócona w ciągu od 10 do 15 sekund.
  - W przypadku nieplanowanych awarii odzyskiwanie połączenia trwa dłużej, od 1 do 1,5 minuty w najgorszym przypadku.
  - Połączenia klienta sieci VPN typu punkt-lokacja (P2S) z bramą zostaną rozłączone, a użytkownicy będą musieli ponownie nawiązać połączenia z poziomu maszyn klienckich.

Podczas konfigurowania sieci VPN typu lokacja-lokacja należy wykonać następujące czynności:

- Potrzebna jest sieć wirtualna, której zakres adresów nie nakłada się na sieć lokalną, z której zostanie połączona sieć VPN.
- W sieci należy utworzyć podsieć bramy.
- Należy utworzyć bramę sieci VPN, określić typ bramy (sieć VPN) i ustalić, czy brama jest oparta na zasadach, czy oparta na trasach. Sieci VPN opartej na trasach są uważane za dodatkowe możliwości i przyszłe potwierdzenie.
- Lokalną bramę sieciową można utworzyć lokalnie i skonfigurować lokalne urządzenie sieci VPN.
- Należy utworzyć połączenie sieci VPN typu lokacja-lokacja między bramą sieci wirtualnej i urządzeniem lokalnym. Korzystanie z sieci VPN opartej na trasach zezwala na połączenia aktywne-pasywne lub aktywne-aktywne z platformą Azure. Wersja oparta na trasach obsługuje również jednocześnie połączenia typu lokacja-lokacja (z dowolnego komputera) i punkt-lokacja (z jednego komputera).
- Należy wybrać jednostkę SKU bramy, która ma być używana. Będzie to zależeć od wymagań dotyczących obciążenia, przepływności, funkcji i umów SLA.
- Protokół BGP (Border Gateway Protocol) to opcjonalna funkcja, której można używać z usługą Azure ExpressRoute i bramami sieci VPN opartymi na trasach do propagowania lokalnych tras protokołu BGP do sieci wirtualnych.

![Sieć VPN](./media/migrate-best-practices-networking/vpn.png)
*Sieć VPN typu lokacja-lokacja*

**Dowiedz się więcej:**

- [Przejrzyj](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) zgodne lokalne urządzenia sieci VPN.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) bram sieci VPN.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) o wysoko dostępnych połączeniach sieci VPN.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) o planowaniu i projektowaniu bramy sieci VPN.
- [Przejrzyj](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) ustawienia bramy sieci VPN.
- [Przejrzyj](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) jednostki SKU bramy.
- [Poczytaj o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) konfigurowaniu protokołu BGP za pomocą bram sieci VPN platformy Azure.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Najlepsze rozwiązanie: Konfigurowanie bramy dla bramy sieci VPN

Podczas tworzenia bramy sieci VPN na platformie Azure należy użyć specjalnej podsieci o nazwie GatewaySubnet. Podczas tworzenia tej podsieci należy zwrócić uwagę na następujące najlepsze rozwiązania:

- Długość prefiksu podsieci bramy może wynosić maksymalnie 29 (na przykład 10.119.255.248/29). Obecnie zalecane jest używanie długości prefiksu 27 (na przykład 10.119.255.224/27).
- Podczas definiowania przestrzeni adresowej podsieci bramy należy użyć ostatniej części przestrzeni adresowej sieci wirtualnej.
- W przypadku korzystania z usługi Azure GatewaySubnet nigdy nie należy wdrażać żadnych maszyn wirtualnych ani innych urządzeń, takich jak Application Gateway, do podsieci bramy.
- Do tej podsieci nie należy przypisywać sieciowej grupy zabezpieczeń. Spowoduje to zatrzymanie działania bramy.

**Dowiedz się więcej:**

- [Użyj tego narzędzia](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed), aby określić przestrzeń adresową IP.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Najlepsze rozwiązanie: Implementowanie Azure wirtualne sieci WAN dla oddziałów

W przypadku wielu połączeń sieci VPN Azure Virtual WAN to usługa sieciowa zapewniająca zoptymalizowaną i zautomatyzowaną łączność między oddziałami za pośrednictwem platformy Azure.

- Usługa Virtual WAN umożliwia łączenie urządzeń w oddziałach z platformą Azure i konfigurowanie ich komunikacji. Można to zrobić ręcznie lub za pomocą urządzeń preferowanych dostawców — partnerów usługi Virtual WAN.
- Użycie urządzeń preferowanych dostawców zapewnia prostą obsługę, łączność oraz zarządzanie konfiguracją.
- Wbudowany pulpit nawigacyjny sieci WAN na platformie Azure udostępnia na bieżąco szczegółowe informacje dotyczące rozwiązywania problemów, dzięki którym oszczędzisz czas, i umożliwia łatwe monitorowanie łączności między lokacjami w dużej skali.

**Dowiedz się więcej:** 
[Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) o usłudze Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Najlepsze rozwiązanie: implementowanie ExpressRoute dla połączeń o kluczowym znaczeniu

Usługa Azure ExpressRoute rozszerza infrastrukturę lokalną do chmury firmy Microsoft przez tworzenie prywatnych połączeń między wirtualnym centrum danych platformy Azure i sieciami lokalnymi.

- Połączenia usługi ExpressRoute mogą znajdować się w sieci typu dowolny-dowolny (sieć VPN IP), sieci Ethernet typu punkt-punkt lub za pośrednictwem dostawcy połączenia. Nie przechodzą one przez publiczny Internet.
- Połączenia usługi ExpressRoute zapewniają wyższe zabezpieczenia, niezawodność i wyższą szybkość (do 10 GB/s), a także spójne opóźnienia.
- Usługa ExpressRoute jest przydatna w przypadku wirtualnych centrów danych, ponieważ klienci mogą uzyskać korzyści wynikające z reguł zgodności skojarzonych z połączeniami prywatnymi.
- Za pomocą usługi ExpressRoute Direct możesz łączyć się bezpośrednio z routerami firmy Microsoft z szybkością 100 GB/s w celu zaspokojenia potrzeb dotyczących większych przepustowości.
- Usługa ExpressRoute używa protokołu BGP do wymiany tras między sieciami lokalnymi, wystąpieniami platformy Azure i publicznymi adresami firmy Microsoft.

Wdrażanie połączeń usługi ExpressRoute obejmuje zazwyczaj zaangażowanie dostawcy usług ExpressRoute. Typowym sposobem szybkiego rozpoczynania pracy jest użycie najpierw sieci VPN typu lokacja-lokacja do ustanowienia połączenia między wirtualnym centrum danych i zasobami lokalnymi, a następnie przeprowadzenie migracji do połączenia usługi ExpressRoute po ustanowieniu fizycznego wzajemnego połączenia z dostawcą usługi.

**Dowiedz się więcej:**

- [Przeczytaj](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) omówienie usługi ExpressRoute.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) o usłudze ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Najlepsze rozwiązanie: Optymalizacja routingu usługi ExpressRoute za pomocą protokołu BGP społeczności

Jeśli masz wiele obwodów usługi ExpressRoute, masz więcej niż jedną ścieżkę łączenia z firmą Microsoft. W związku z tym może wystąpić routing nieoptymalny, tzn. ruch może użyć dłuższej ścieżki w celu dotarcia do firmy Microsoft lub z firmy Microsoft do sieci użytkownika. Im dłuższa ścieżka sieciowa, tym większe opóźnienie. Opóźnienie ma bezpośredni wpływ na wydajność aplikacji i środowisko użytkownika.

**Przykład:**

Zapoznajmy się z przykładem:

- masz dwa biura w USA: jedno w Los Angeles i jedno w Nowym Jorku.
- Biura są połączone za pośrednictwem sieci WAN, która może być Twoją siecią podstawową lub siecią IP VPN dostawcy usług.
- Dostępne są dwa obwody usługi ExpressRoute: jeden w zachodnich stanach USA i jeden we wschodnich stanach USA, które są również połączone w ramach sieci WAN. Oczywiście masz dwie ścieżki połączenia z siecią firmy Microsoft.

**Problem:**

Teraz wyobraź sobie, że dysponujesz wdrożeniem platformy Azure (np. usługą Azure App Service) zarówno w zachodnich, jak i wschodnich stanach USA.

- Aby zapewnić optymalne środowisko, użytkownicy w poszczególnych biurach uzyskują dostęp do najbliższych usług platformy Azure.
- Z tego względu chcesz połączyć użytkowników w Los Angeles z regionem Zachodnie stany USA platformy Azure, a użytkowników w Nowym Jorku z regionem Wschodnie stany USA na platformie Azure.
- Działa to w przypadku użytkowników z Wybrzeża Wschodniego, ale nie dla tych z Wybrzeża Zachodniego. Występuje następujący problem:
  - W poszczególnych obwodach usługi ExpressRoute anonsujemy zarówno prefiks dla wschodnich stanów USA na platformie Azure (23.100.0.0/16), jak i prefiks w zachodnich stanach USA na platformie Azure (13.100.0.0/16).
  - Bez znajomości regionu, z którego pochodzi danych prefiks, prefiksy nie są traktowane w inny sposób.
  - Sieć WAN może założyć, że oba prefiksy są bliżej wschodnich stanów USA niż zachodnich stanów USA, i dlatego będzie kierować użytkowników z obu biur do obwodu usługi ExpressRoute w regionie Wschodnie stany USA, zapewniając nieoptymalne środowisko dla użytkowników w biurze w Los Angeles.

![Sieć VPN](./media/migrate-best-practices-networking/bgp1.png)
*Niezoptymalizowane połączenie społeczności protokołu BGP*

**Rozwiązanie:**

Aby zoptymalizować routing dla użytkowników obu biur, trzeba wiedzieć, który prefiks odpowiada zachodnim, a który wschodnim stanom USA. Te informacje można kodować przy użyciu wartości społeczności BGP.

- Przypisujesz unikatową wartość społeczności BGP do każdego regionu świadczenia usługi Azure. Na przykład 12076:51004 dla wschodnich i 12076:51006 dla zachodnich stanów USA.
- Teraz, gdy jest jasne, który prefiks należy do którego regionu platformy Azure, możesz skonfigurować preferowany obwód usługi ExpressRoute.
- Ponieważ do wymiany informacji o routingu używasz protokołu BGP, w celu wpłynięcia na routing możesz użyć preferencji lokalnej protokołu BGP.
- W naszym przykładzie przypisujesz wyższą wartość preferencji lokalnej na 13.100.0.0/16 w zachodnich niż we wschodnich stanach USA i podobnie wyższą wartość preferencji lokalnej na 23.100.0.0/16 we wschodnich niż w zachodnich stanach USA.
- Ta konfiguracja gwarantuje, że gdy obie ścieżki do firmy Microsoft są dostępne, użytkownicy w Los Angeles łączą się z regionem Zachodnie stany USA platformy Azure przy użyciu obwodu zachodniego, a użytkownicy w Nowym Jorku łączą się z regionem Wschodnie stany USA — obwodu wschodniego. Routing jest zoptymalizowany po obu stronach.

![Sieć VPN](./media/migrate-best-practices-networking/bgp2.png)
*Zoptymalizowane połączenie społeczności protokołu BGP*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) na temat optymalizowania routingu.

## <a name="secure-vnets"></a>Zabezpiecz sieci wirtualnych

Odpowiedzialność za zabezpieczanie sieci wirtualnych jest podzielona między firmę Microsoft i użytkownika. Firma Microsoft oferuje wiele funkcji sieciowych, a także usług, które ułatwiają zabezpieczanie zasobów. W przypadku projektowania zabezpieczeń sieci wirtualnych najlepsze rozwiązania, które warto zastosować, obejmują implementację sieci obwodowej, użycie filtrowania i grup zabezpieczeń, zabezpieczanie dostępu do zasobów i adresów IP oraz implementowanie ochrony przed atakami.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) najlepszych rozwiązań z zakresu zabezpieczeń sieci.
- [Dowiedz się](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security), jak projektować bezpieczne sieci.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Najlepsze rozwiązanie: Implementowanie sieci obwodowej platformy Azure

Mimo że firma Microsoft inwestuje bardzo dużo w ochronę infrastruktury chmury, musisz również chronić usługi w chmurze i grupy zasobów. Podejście wielowarstwowe do zabezpieczeń zapewnia najlepszą ochronę. Zastosowanie sieci obwodowej jest ważną częścią tej strategii obrony.

- Sieć obwodowa chroni zasoby sieci wewnętrznej z sieci niezaufanej.
- Jest to najbardziej zewnętrzna warstwa widoczna w Internecie. Mówiąc ogólnie, znajduje się ona między Internetem a infrastrukturą przedsiębiorstwa i przeważnie ma pewne formy ochrony po obu stronach.
- W typowej topologii sieci przedsiębiorstwa podstawowa infrastruktura jest silnie wzmocniona na obrzeżach z wieloma warstwami urządzeń zabezpieczeń. Granica każdej warstwy składa się z urządzeń i punktów wymuszania zasad.
- Każda warstwa może zawierać kombinację rozwiązań zabezpieczeń sieci, które obejmują zapory, zapobieganie atakom typu „odmowa usługi” (DoS), system wykrywania nieautoryzowanego dostępu/ochrony przed nieautoryzowanym dostępem (IDS/IPS) i urządzenia sieci VPN.
- Wymuszanie zasad w sieci obwodowej może korzystać z zasad zapory, list kontroli dostępu (ACL) lub wybranego routingu.
- Ruch przychodzący z Internetu jest przechwytywany i obsługiwany przez kombinację rozwiązań obronnych w celu blokowania ataków i szkodliwego ruchu przy jednoczesnym dopuszczaniu wiarygodnych żądań do sieci.
- Ruch przychodzący może być kierowany bezpośrednio do zasobów w sieci obwodowej. Następnie zasób sieci obwodowej może komunikować się z innymi zasobami w sieci, przenosząc ruch dalej do sieci po walidacji.

Na poniższej ilustracji przedstawiono przykład pojedynczej podsieci sieci obwodowej w sieci firmowej z dwoma granicami zabezpieczeń.

![Sieć VPN](./media/migrate-best-practices-networking/perimeter.png)
*Wdrażanie sieci obwodowej*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o wdrażaniu sieci obwodowej między platformą Azure i lokalnym centrum danych.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Najlepsze rozwiązanie: ruch w sieci wirtualnej filtr z sieciowymi grupami zabezpieczeń

Sieciowe grupy zabezpieczeń zawierają wiele reguł zabezpieczeń dla ruchu przychodzącego i wychodzącego, które filtrują ruch przechodzący do i z zasobów. Filtrowanie może odbywać się według źródłowego i docelowego adresu IP, portu i protokołu.

- Sieciowe grupy zabezpieczeń zawierają reguły zabezpieczeń, które zezwalają na lub blokują przychodzący ruch sieciowy (lub wychodzący ruch sieciowy z) dla kilku typów zasobów platformy Azure. Dla każdej reguły można określić źródło i obiekt docelowy, port i protokół.
- Reguły sieciowej grupy zabezpieczeń są oceniane według priorytetu na podstawie krotki składającej się z 5 informacji (urządzenie źródłowe, port źródłowy, urządzenie docelowe, port docelowy i protokół) w celu zezwolenia na ruch lub zablokowania go.
- Rekord przepływu tworzony jest dla istniejących połączeń. Komunikacja jest dozwolona lub zablokowana na podstawie stanu połączenia z rekordu przepływu.
- Rekord przepływu pozwala na to, aby sieciowa grupa zabezpieczeń była grupą stanową. Jeśli na przykład zostanie określona reguła zabezpieczeń dla ruchu wychodzącego do dowolnego adresu za pośrednictwem portu 80, nie trzeba określać reguły zabezpieczeń ruchu przychodzącego, aby odpowiadać na ruch wychodzący. Należy tylko określić regułę zabezpieczeń dla ruchu przychodzącego w przypadku, jeśli komunikacja jest inicjowana zewnętrznie.
- Jest to również prawdziwe w odwrotnym przypadku. Jeśli ruch przychodzący jest dozwolony przez port, nie musisz określać reguły zabezpieczeń dla ruchu wychodzącego, aby odpowiadać na ruch przychodzący przez port.
- Istniejące połączenia nie są przerywane po usunięciu reguły zabezpieczeń, która zezwoliła na przepływ. Przepływy ruchu są przerywane po zakończeniu połączenia, gdy przez co najmniej kilka minut nie ma ruchu z żadnej strony.
- Podczas tworzenia sieciowych grup zabezpieczeń utwórz ich jak najmniej, ale tyle, ile potrzebujesz.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Najlepsze rozwiązanie: bezpieczny ruch wschód/zachód i północ/południe

W przypadku zabezpieczania sieci wirtualnych ważne jest rozważenie wektorów ataków.

- Użycie tylko sieciowych grup zabezpieczeń podsieci upraszcza środowisko, ale zabezpiecza wyłącznie ruch do podsieci. Jest to ruch typu północ/południe.
- Ruch między maszynami wirtualnymi w tej samej podsieci jest znany jako ruch typu wschód/zachód.
- Ważne jest używanie obu rodzajów ochrony, ponieważ jeśli haker uzyska dostęp z zewnątrz, zostanie zatrzymany podczas próby dołączenia maszyn znajdujących się w tej samej podsieci.

### <a name="use-service-tags-on-nsgs"></a>Używanie tagów usług w sieciowych grupach zabezpieczeń

Tag usługi reprezentuje grupę prefiksów adresów IP. Użycie tagu usługi pomaga zminimalizować złożoność podczas tworzenia reguł sieciowej grupy zabezpieczeń.

- Podczas tworzenia reguł tagów usługi można używać zamiast konkretnych adresów IP.
- Firma Microsoft zarządza prefiksami adresów skojarzonymi z tagiem usługi i automatycznie aktualizuje tag usługi, gdy adresy ulegną zmianie.
- Nie można utworzyć własnego tagu usługi ani określić adresów IP uwzględnionych w tagu.

Tagi usługi eliminują czynności wykonywane ręcznie z procesu przypisywania reguły do grup usług platformy Azure. Jeśli na przykład chcesz zezwolić podsieci sieci wirtualnej zawierającej serwery internetowe na dostęp do bazy danych Azure SQL Database, możesz utworzyć regułę ruchu wychodzącego do portu 1433 i użyć tagu usługi **Sql**.

- Ten tag **Sql** określa prefiksy adresów usług Azure SQL Database i Azure SQL Data Warehouse.
- W przypadku określenia wartości **Sql** dozwolony lub blokowany jest ruch do usługi Sql.
- Jeśli chcesz zezwolić na dostęp do usługi **Sql** w konkretnym regionie, możesz określić region. Jeśli na przykład chcesz zezwolić na dostęp do usługi Azure SQL Database tylko w regionie Wschodnie stany USA, możesz określić **Sql.EastUS** jako tag usługi.
- Tag reprezentuje usługę, ale nie konkretne wystąpienia usługi. Na przykład tag reprezentuje usługę Azure SQL Database, ale nie reprezentuje konkretnej bazy danych ani serwera SQL.
- Wszystkie prefiksy adresów reprezentowane przez ten tag są również reprezentowane przez tag **Internet**.

**Dowiedz się więcej:**

- [Poczytaj na temat](https://docs.microsoft.com/azure/virtual-network/security-overview) sieciowych grup zabezpieczeń.
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) tagi usług dostępne dla sieciowych grup zabezpieczeń.

## <a name="best-practice-use-application-security-groups"></a>Najlepsze rozwiązanie: przy użyciu grup zabezpieczeń aplikacji

Grupy zabezpieczeń aplikacji umożliwiają konfigurowanie zabezpieczeń sieci jako naturalnego rozszerzenia struktury aplikacji.

- Można grupować maszyny wirtualne i definiować zasady zabezpieczeń sieci na podstawie grup zabezpieczeń aplikacji.
- Grupy zabezpieczeń aplikacji umożliwiają ponowne używanie zasady zabezpieczeń na dużą skalę bez ręcznej obsługi jawnych adresów IP.
- Grupy zabezpieczeń aplikacji obsługują złożoność jawnych adresów IP i wiele zestawów reguł, co pozwala skupić się na logice biznesowej.

**Przykład:**

![Grupa zabezpieczeń aplikacji](./media/migrate-best-practices-networking/asg.png)
*Przykład grupy zabezpieczeń aplikacji*

**Interfejs sieciowy** | **Grupa zabezpieczeń aplikacji**
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
Allow-HTTP-Inbound-Internet | Zezwalanie na ruch z Internetu do serwerów internetowych. Ruch przychodzący z Internetu jest blokowany przez domyślną regułę zabezpieczeń DenyAllInbound, dlatego dodatkowa reguła nie jest potrzebna w przypadku grup zabezpieczeń aplikacji AsgLogic i AsgDb. | Priorytet: 100<br/><br/> Źródło: Internet<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgWeb<br/><br/> Port docelowy: 80<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwalaj na.
Deny-Database-All | Domyślna reguła zabezpieczeń AllowVNetInBound zezwala na całą komunikację między zasobami w tej samej sieci wirtualnej, ta zasada jest potrzebna w celu blokowania ruchu ze wszystkich zasobów. | Priorytet: 120<br/><br/> Źródło: *<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: wszystkie<br/><br/> Dostęp: odmowa.
Allow-Database-BusinessLogic | Zezwolenie na ruch z grupy zabezpieczeń aplikacji AsgLogic do grupy zabezpieczeń aplikacji AsgDb. Priorytet tej reguły jest wyższy niż priorytet reguły Deny-Database-All i jest ona przetwarzana przed tą regułą, dlatego ruch z grupy zabezpieczeń aplikacji AsgLogic jest dozwolony, a cały pozostały ruch jest blokowany. | Priorytet: 110<br/><br/> Źródło: AsgLogic<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwalaj na.

<!--markdownlint-enable MD033 -->

- Reguły określające grupę zabezpieczeń aplikacji jako źródło lub obiekt docelowy są stosowane tylko do interfejsów sieciowych, które są elementami członkowskimi grupy zabezpieczeń aplikacji. Jeśli interfejs sieciowy nie jest elementem członkowskim grupy zabezpieczeń aplikacji, reguła nie jest stosowana do tego interfejsu sieciowego, mimo że grupa zabezpieczeń sieci jest skojarzona z podsiecią.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) o grupach zabezpieczeń aplikacji.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Najlepsze rozwiązanie: bezpieczny dostęp do usługi PaaS za pomocą punktów końcowych usługi sieci wirtualnej

Punkty końcowe usługi sieci wirtualnej rozszerzają prywatną przestrzeń adresową i tożsamość sieci wirtualnej do usług platformy Azure za pośrednictwem połączenia bezpośredniego.

- Punkty końcowe umożliwiają zabezpieczanie krytycznych zasobów usługi platformy Azure tylko do sieci wirtualnych. Ruch z sieci wirtualnej do usługi platformy Azure zawsze pozostaje w sieci szkieletowej platformy Microsoft Azure.
- Przestrzenie adresowe prywatnych sieci wirtualnych mogą się nakładać, przez co nie można za ich pomocą jednoznacznie identyfikować ruchu pochodzącego z sieci wirtualnej.
- Po włączeniu punktów końcowych usługi w sieci wirtualnej można zabezpieczyć zasoby usługi platformy Azure przez dodanie reguły sieci wirtualnej do zasobów usługi. Zwiększa to bezpieczeństwo przez całkowite uniemożliwienie publicznego dostępu z Internetu do tych zasobów i zezwolenie na ruch tylko z Twojej sieci wirtualnej.

![Punkty końcowe usługi](./media/migrate-best-practices-networking/endpoint.png)
*Punkty końcowe usługi*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o punktach końcowych usługi sieci wirtualnej.

## <a name="best-practice-control-public-ip-addresses"></a>Najlepsze rozwiązanie: kontrolowanie publiczne adresy IP

Publiczne adresy IP na platformie Azure mogą być kojarzone z maszynami wirtualnymi, modułami równoważenia obciążenia, bramami aplikacji i bramami sieci VPN.

- Publiczne adresy IP umożliwiają zasobom internetowym komunikowanie się w ramach ruchu przychodzącego z zasobami platformy Azure, a zasobom platformy Azure komunikowanie się w ramach ruchu wychodzącego z Internetem.
- Publiczne adresy IP są tworzone przy użyciu podstawowej lub standardowej jednostki SKU, między którymi występuje kilka różnic. Standardowe jednostki SKU można przypisać do dowolnej usługi, ale zazwyczaj są one konfigurowane na maszynach wirtualnych, w modułach równoważenia obciążenia i w bramach aplikacji.
- Należy pamiętać, że podstawowy publiczny adres IP nie ma automatycznie skonfigurowanej sieciowej grupy zabezpieczeń. Musisz skonfigurować własną i przypisać reguły, aby kontrolować dostęp. Adresy IP standardowej jednostki SKU mają domyślnie przypisane reguły i sieciową grupę zabezpieczeń.
- Najlepszym rozwiązaniem jest rezygnacja z konfigurowania maszyn wirtualnych przy użyciu publicznego adresu IP.
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
*Azure Firewall*

- Usługa Azure Firewall może centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych.
- Usługa Azure Firewall korzysta ze statycznego publicznego adresu IP dla zasobów sieci wirtualnej, co umożliwia zewnętrznym zaporom identyfikowanie ruchu pochodzącego z sieci wirtualnej.
- Usługa Azure Firewall jest w pełni zintegrowana z usługą Azure Monitor na potrzeby rejestrowania i analiz.
- Najlepszym rozwiązaniem podczas tworzenia reguł usługi Azure Firewall jest użycie tagów FQDN do tworzenia reguł.
  - Tag FQDN reprezentuje grupę nazw FQDN skojarzonych z dobrze znanymi usługami firmy Microsoft.
  - Możesz użyć tagu FQDN, aby zezwolić na wymagany ruch sieciowy wychodzący przez zaporę.
- Aby na przykład ręcznie zezwolić na ruch sieciowy witryny Windows Update przez zaporę, należy utworzyć wiele reguł aplikacji. Przy użyciu tagów FQDN tworzysz regułę aplikacji i dołączasz tag Windows Update. Dzięki tej regule ruch sieciowy do punktów końcowych witryny Microsoft Windows Update może przepływać przez zaporę.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/firewall/overview) usługi Azure Firewall.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/firewall/fqdn-tags) o tagach FQDN.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Najlepsze rozwiązanie: wdrażanie zapory aplikacji sieci Web (WAF)

Aplikacje internetowe coraz częściej stają się obiektami złośliwych ataków wykorzystujących znane luki w zabezpieczeniach. Ataki wykorzystujące luki obejmują wstrzyknięcia kodu SQL i działania skryptów między witrynami. Zapobieganie takim atakom z poziomu kodu aplikacji może być trudne. Może też wymagać rygorystycznego przestrzegania harmonogramu konserwacji, poprawek i monitorowania na poziomie wielu warstw topologii aplikacji. Scentralizowana zapora aplikacji internetowej ułatwia zarządzanie zabezpieczeniami oraz ułatwia administratorom aplikacji ochronę przed zagrożeniami lub intruzami. Zapora aplikacji internetowej może szybciej reagować na zagrożenia bezpieczeństwa, stosując poprawki znanych luk w zabezpieczeniach w lokalizacji centralnej, zamiast zabezpieczać poszczególne aplikacje internetowe. Istniejące bramy Application Gateway można łatwo przekonwertować na bramę Application Gateway obsługującą zaporę aplikacji internetowej.

Zapora aplikacji internetowej to funkcja usługi Azure Application Gateway.

- Zapora aplikacji internetowej zapewnia centralną ochronę aplikacji internetowych przez typowymi atakami wykorzystującymi luki i lukami w zabezpieczeniach.
- Zapora aplikacji internetowej chroni bez modyfikacji kodu zaplecza.
- Może ona jednocześnie chronić wiele aplikacji internetowych za bramą aplikacji.
- Zapora aplikacji internetowej jest integrowana z usługą Azure Security Center.
- Reguły zapory aplikacji internetowej i grupy reguł można dostosować tak, aby spełniały wymagania aplikacji.
- Najlepszym rozwiązaniem jest użycie zapory aplikacji internetowej przed wszelkimi aplikacjami internetowymi, w tym aplikacjami na maszynach wirtualnych platformy Azure, lub jako usługi Azure App Service.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/application-gateway/waf-overview) na temat zapory aplikacji internetowej.
- [Przejrzyj](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) ograniczenia i wykluczenia dotyczące zapory aplikacji internetowej.

## <a name="best-practice-implement-azure-network-watcher"></a>Najlepsze rozwiązanie: Implementowanie usługi Azure Network Watcher

Usługa Azure Network Watcher udostępnia narzędzia do monitorowania zasobów i komunikacji w sieci wirtualnej platformy Azure. Na przykład można monitorować komunikację między maszyną wirtualną i punktem końcowym, takim jak inna maszyna wirtualna lub nazwa FQDN, wyświetlać zasoby i relacje zasobów w sieci wirtualnej lub diagnozować problemy z ruchem sieciowym.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Dzięki usłudze Network Watcher można monitorować i diagnozować problemy z siecią bez konieczności logowania się na maszynach wirtualnych.
- Można wyzwalać przechwytywanie pakietów przez ustawienie alertów oraz uzyskiwać dostęp do informacji o wydajności w czasie rzeczywistym na poziomie pakietów. Można szczegółowo analizować problemy.
- Najlepszym rozwiązaniem jest użycie usługi Network Watcher do przeglądania dzienników przepływów sieciowych grup zabezpieczeń.
  - Dzienniki przepływów sieciowych grup zabezpieczeń w usłudze Network Watcher umożliwiają wyświetlanie informacji dotyczących ruchu IP przychodzącego i wychodzącego przez sieciową grupę zabezpieczeń.
  - Dzienniki przepływów są pisane w formacie JSON.
  - Dzienniki przepływów przedstawiają przepływy wychodzące i przychodzące dla każdej reguły, interfejs sieciowy, do którego odnosi się przepływ, 5-krotkowe informacje o przepływie (źródłowy/docelowy adres IP, port źródłowy/docelowy i protokół) oraz informację zezwoleniu na ruch albo jego zablokowaniu.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/network-watcher) usługi Network Watcher.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) o dziennikach przepływów sieciowych grup zabezpieczeń.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Korzystanie z narzędzi partnerów w portalu Azure Marketplace

W przypadku bardziej złożonych topologii sieci można używać produktów zabezpieczeń od partnerów firmy Microsoft, w szczególności wirtualnych urządzeń sieciowych (NVA, network virtual appliance).

- Wirtualne urządzenie sieciowe to maszyna wirtualna wykonująca funkcję sieciową, np. funkcję zapory, optymalizacji WAN lub inną.
- Wirtualne urządzenia sieciowe wzmacniają zabezpieczenia sieci wirtualnej i funkcje sieciowe. Można je wdrażać w przypadku zapór o wysokiej dostępności, zapobiegania włamaniom, wykrywania intruzów, zapór aplikacji internetowych, optymalizacji sieci WAN, routingu, równoważenia obciążenia, sieci VPN, zarządzania certyfikatami, usługi Active Directory i uwierzytelniania wieloskładnikowego.
- Wirtualne urządzenia sieciowe są oferowane przez wielu dostawców w witrynie  [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Najlepsze rozwiązanie: wdrożenie zapory i urządzenia WUS w sieci Centrum

W centrum sieć obwodowa (z dostępem do Internetu) jest zazwyczaj zarządzana za pomocą zapory platformy Azure, farmy zapór lub zapory aplikacji internetowej. Przeanalizujmy następujące porównania.

<!--markdownlint-disable MD033 -->

**Typ zapory** | **Szczegóły**
--- | ---
Zapory aplikacji internetowych | Aplikacje internetowe są powszechnie używane oraz często mają luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki.<br/><br/> Zapory aplikacji internetowych są projektowane tak, aby wykrywać ataki na aplikacje internetowe (HTTP/HTTPS) skuteczniej niż zapora ogólna.<br/><br/> W porównaniu z tradycyjną technologią zapory aplikacji internetowych mają zestaw konkretnych funkcji chroniących wewnętrzne serwery internetowe przed zagrożeniami.
Azure Firewall | Podobnie jak w przypadku farm zapór wirtualnych urządzeń sieciowych usługa Azure Firewall używa wspólnego mechanizmu administrowania oraz zestawu reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach szprych i kontrolować dostęp do sieci lokalnych.<br/><br/> Usługa Azure Firewall ma wbudowaną skalowalność.
Zapory wirtualnych urządzeń sieciowych | Podobnie jak usługa Azure Firewall farmy zapór wirtualnych urządzeń sieciowych używają wspólnego mechanizmu administrowania oraz zestawu reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach szprych i kontrolować dostęp do sieci lokalnych.<br/><br/> Zapory wirtualnych urządzeń sieciowych można ręcznie skalować za modułem równoważenia obciążenia.<br/><br/> Chociaż zapora wirtualnego urządzenia sieciowego ma mniej wyspecjalizowane oprogramowanie niż zapora aplikacji internetowej, obsługuje szerszy zakres aplikacji, aby filtrować i sprawdzać wszelkiego rodzaju ruch wychodzący i przychodzący.<br/><br/> Jeśli chcesz korzystać z wirtualnego urządzenia sieciowego, możesz je znaleźć w portalu Azure Marketplace.

<!--markdownlint-enable MD033 -->

Zalecamy użycie jednego zestawu zapór Azure Firewall (lub wirtualnych urządzeń sieciowych) dla ruchu pochodzącego z Internetu oraz innego zestawu dla ruchu pochodzącego ze środowiska lokalnego.

- Używanie tylko jednego zestawu zapór dla obu rodzajów ruchu stanowi zagrożenie dla bezpieczeństwa, ponieważ nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego.
- Używanie oddzielnych warstw zapory zmniejsza złożoność sprawdzania zasad zabezpieczeń i wyraźnie pokazuje, które reguły dotyczą którego przychodzącego żądania sieciowego.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o korzystaniu z wirtualnych urządzeń sieciowych w sieci wirtualnej platformy Azure.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z innymi najlepszymi rozwiązaniami:

- [Najlepsze rozwiązania](./migrate-best-practices-security-management.md) w zakresie zabezpieczeń i zarządzania po migracji.
- [Najlepsze rozwiązania](./migrate-best-practices-costs.md) dotyczące zarządzania kosztami po migracji.
