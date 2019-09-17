---
title: Najlepsze rozwiązania dotyczące konfigurowania sieci pod kątem obciążeń migrowanych do platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Po przeprowadzeniu migracji na platformę Azure należy zapoznać się z najlepszymi rozwiązaniami dotyczącymi konfigurowania sieci na potrzeby migrowanych obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8fbdd20c435d4aed8a284174d813abc8d391171b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022850"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Najlepsze rozwiązania w celu skonfigurowania sieci w przypadku obciążeń migracji na platformę Azure

Projektowanie pod kątem migracji, oprócz migracji, oraz plan jest jedną z najważniejszych etapów projektowania i implementowania sieci platformy Azure. W tym artykule opisano najlepsze rozwiązania dotyczące sieci podczas migrowania do implementacji rozwiązań IaaS i PaaS na platformie Azure.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisanych w tym artykule opierają się na platformie Azure oraz z funkcji dostępnych w momencie pisania. Funkcje i możliwości zmiany w czasie. Nie wszystkie zalecenia może być odpowiednie dla danego wdrożenia, dlatego wybierz te, które będą dla Ciebie.

## <a name="design-virtual-networks"></a>Projektowanie sieci wirtualnych

Platforma Azure udostępnia sieci wirtualne (Vnet):

- Zasoby platformy Azure komunikować się prywatnie, bezpośrednio i bezpiecznie ze sobą za pośrednictwem sieci wirtualnych.
- Możesz skonfigurować punkt końcowy połączenia w przypadku sieci wirtualnych, dla maszyn wirtualnych i usług, które wymagają komunikację z Internetem.
- Sieć wirtualna jest to logiczna izolacja chmury platformy Azure przeznaczoną do Twojej subskrypcji.
- Można zaimplementować wiele sieci wirtualnych w ramach każdej subskrypcji platformy Azure i regionu platformy Azure.
- Każda sieć wirtualna jest odizolowana od innych sieci wirtualnych.
- Sieci wirtualne mogą zawierać prywatne i publiczne adresy IP zdefiniowane w dokumencie [RFC 1918](https://tools.ietf.org/html/rfc1918), wyrażone w notacji CIDR. Publiczne adresy IP określone w przestrzeni adresowej sieci wirtualnej nie są bezpośrednio dostępne z Internetu.
- Sieci wirtualne mogą łączyć się ze sobą za pomocą komunikacji równorzędnej sieci wirtualnej. Połączone sieci wirtualne mogą znajdować się w tej samej lub różnych regionach. Ten sposób zasobów w jednej sieci wirtualnej można nawiązać zasobów w innych sieciach wirtualnych.
- Domyślnie platforma Azure kieruje ruchem między podsieciami w sieci wirtualnej, połączonymi sieciami wirtualnymi, sieciami lokalnymi oraz Internetem.

Podczas planowania topologii sieci wirtualnej należy wziąć pod uwagę sposób rozmieszczenia przestrzeni adresowej IP, sposób implementacji sieci gwiazdy, sposób segmentowania sieci wirtualnych w podsieci, konfigurowanie systemu DNS i implementowanie stref dostępności platformy Azure.

## <a name="best-practice-plan-ip-addressing"></a>Najlepsze rozwiązanie: planowanie adresowania IP

Gdy tworzysz sieci wirtualne w ramach migracji, ważne jest zaplanowanie przestrzeni adresowej IP sieci wirtualnej.

- Przypisz przestrzeń adresową, który nie jest większy niż zakres CIDR /16 w każdej sieci wirtualnej. Sieci wirtualne umożliwiają wykorzystanie 65536 adresów IP i przypisanie prefiks mniejszy niż/16 mogłoby spowodować utratę adresów IP. Ważne jest nie tracić adresów IP, nawet jeśli pochodzi z zakresów prywatnych definicją w dokumencie RFC 1918.
- Przestrzeń adresowa sieci wirtualnej nie mogą nakładać się z zakresami adresów sieci lokalnej.
- Nie można używać translacji adresów sieciowych (NAT).
- Nakładające się przestrzenie adresów może spowodować, że nie można połączyć sieci i routingu, który nie działa prawidłowo. Jeśli sieci zachodziły na siebie, konieczne będzie zmodyfikowanie sieci lub użyciu translatora adresów sieciowych (NAT).

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) z sieciami wirtualnymi platformy Azure.
- [Odczyt](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) sieć — często zadawane pytania.
- [Dowiedz](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) się więcej na temat ograniczeń sieci.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Najlepsze rozwiązanie: implementowanie topologii sieci piasty i szprych

Topologia sieci piasty i szprych izoluje obciążenia przy jednoczesnym udostępnianiu usług, takich jak tożsamość i zabezpieczenia.

- Piasta to sieć wirtualna platformy Azure, pełni rolę centralnego punktu łączności.
- Szprychy są sieciami wirtualnymi podłączać do koncentratora sieci wirtualnej za pomocą komunikacji równorzędnej sieci wirtualnych.
- Usługi udostępnione są wdrażane w piaście, a poszczególne obciążenia są wdrażane jako szprychy.

Rozważ następujące źródła:

- Implementowanie topologii gwiazdy na platformie Azure umożliwia scentralizowanie typowych usług, takich jak połączenia z sieciami lokalnymi i zapory, izolacji między sieciami wirtualnymi. Piastą zapewnia centralny punkt łączności z sieciami lokalnymi i miejsce do użycia usług hosta przez obciążenia hostowane w sieci wirtualne będące szprychami.
- Konfiguracja gwiazdy jest zwykle używany przez większych przedsiębiorstw. Mniejsze sieci, warto rozważyć prostsze projekt, aby zaoszczędzić na kosztach i złożoności.
- Sieci wirtualne będące szprychami mogą być używane do izolowania obciążeń z każdej szprysze zarządzana oddzielnie od innych szprych. Każde obciążenie może zawierać wiele warstw i wiele podsieci, które są połączone z modułami równoważenia obciążenia platformy Azure.
- Sieci wirtualne gwiazdy można implementować w różnych grupach zasobów, a nawet w różnych subskrypcjach. W przypadku komunikacji równorzędnej sieci wirtualnych w różnych subskrypcjach subskrypcje mogą być kojarzone z tymi samymi lub różnymi dzierżawami usługi Azure Active Directory (Azure AD). Umożliwia to zdecentralizowane zrządzanie każdym obciążeniem, a jednocześnie udostępnianie usług obsługiwanych w sieci będącej piastą.

![Zarządzanie zmianami](./media/migrate-best-practices-networking/hub-spoke.png)
*topologii gwiazdy*

**Dowiedz się więcej:**

- [Przeczytaj o](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) topologii gwiazdy.
- Uzyskaj zalecenia dotyczące sieci dla uruchomionych na platformie Azure [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) i [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm) maszyn wirtualnych.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) o komunikacji równorzędnej sieci wirtualnych.

## <a name="best-practice-design-subnets"></a>Najlepsze rozwiązanie: projektowanie podsieci

Aby zapewnić izolację w sieci wirtualnej, należy posegmentować ją na jedną lub więcej podsieci i przypisać części przestrzeni adresowej sieci wirtualnej do każdej podsieci.

- Możesz utworzyć wiele podsieci w ramach każdej sieci wirtualnej.
- Domyślnie platforma Azure kieruje ruchem sieciowym między wszystkie podsieci w sieci wirtualnej.
- Decyzje związane z podsieci są oparte na Twoje wymagania techniczne i organizacyjne.
- Możesz utworzyć przy użyciu notacji CIDR podsieci.
- Podczas ustawiania zakresu sieci dla podsieci, to należy pamiętać, że Azure zachowuje pięciu adresów IP w każdej podsieci, której nie można użyć. Na przykład jeśli tworzysz najmniejszą dostępnej podsieci/29 (z ośmioma adresów IP), Azure zostaną zachowane pięciu adresów, dzięki czemu masz tylko trzy można używać adresów, które mogą być przypisane do hostów w podsieci.
- W większości przypadków zaleca się użycie podsieci /28 jako najmniejszej.

**Przykład:**

W tabeli przedstawiono przykład sieci wirtualnej z przestrzenią adresową 10.245.16.0/20 podzieloną na podsieci na potrzeby planowanej migracji.

**Podsieć** | **CIDR** | **Adresy** | **Korzystanie**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | Maszyny wirtualne z bazy danych

**Dowiedz się więcej:**

- [Dowiedz](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) się więcej na temat projektowania podsieci.
- [Dowiedz się](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure), w jaki sposób fikcyjna firma (Contoso) przygotowała infrastrukturę sieciową do migracji.

## <a name="best-practice-set-up-a-dns-server"></a>Najlepsze rozwiązanie: konfigurowanie serwera DNS

Platforma Azure domyślnie dodaje serwer DNS podczas wdrażania sieci wirtualnej. Pozwala na szybkie tworzenie sieci wirtualnych i wdrażania zasobów. Jednak ten serwer DNS tylko zapewnia usługi do zasobów w tej sieci wirtualnej. Jeśli chcesz połączyć ze sobą wiele sieci wirtualnych lub połącz się z lokalnym serwerem z sieciami wirtualnymi, potrzebujesz możliwości rozpoznawania nazw dodatkowe. Na przykład może być konieczne usługi Active Directory do rozpoznawania nazw DNS między sieciami wirtualnymi. Aby to zrobić, należy wdrożyć własnego niestandardowego serwera DNS na platformie Azure.

- Serwery DNS w sieci wirtualnej może przekazywać zapytań DNS do rozpoznawania cyklicznego na platformie Azure. Dzięki temu można rozpoznawać nazwy hostów w ramach tej sieci wirtualnej. Na przykład kontroler domeny działający na platformie Azure można odpowiadać na zapytania DNS dotyczące własnej domeny i przesyłania dalej wszystkich innych zapytań na platformie Azure.
- Przesyłania dalej DNS umożliwia maszynom wirtualnym wyświetlić swoje zasoby lokalne (za pośrednictwem kontrolera domeny) i nazwy hosta platformy Azure (przy użyciu usługi przesyłania dalej). Dostęp do rozpoznawania cyklicznego na platformie Azure znajduje się za pomocą wirtualnego adresu IP 168.63.129.16.
- Przekazywanie DNS również umożliwia rozpoznawanie nazw DNS między sieciami wirtualnymi i umożliwia maszyn lokalnych do rozpoznawania nazw hostów udostępnianych przez platformę Azure.
  - Aby rozpoznać nazwę hosta maszyny Wirtualnej, serwer DNS maszyny Wirtualnej musi znajdować się w tej samej sieci wirtualnej i można skonfigurować na kwerendy nazwy hosta do przodu na platformie Azure.
  - Ponieważ sufiks DNS różni się w każdej sieci wirtualnej, można użyć reguły warunkowego przesyłania dalej do wysyłania zapytań DNS do poprawną sieć wirtualną dla rozwiązania.
- Jeśli używasz własnych serwerów DNS, można określić wiele serwerów DNS w każdej sieci wirtualnej. Można również określić wiele serwerów DNS dla każdego interfejsu sieciowego (dla usługi Azure Resource Manager) lub dla usługi w chmurze (w przypadku klasycznego modelu wdrażania).
- Serwery DNS określona dla interfejsu lub w chmurze Usługa sieciowa mają pierwszeństwo przed serwerów DNS określona dla sieci wirtualnej.
- W modelu wdrażania usługi Azure Resource Manager można określić serwery DNS dla sieci wirtualnej i interfejsu sieciowego, ale najlepszym rozwiązaniem jest użycie ustawienia tylko w przypadku sieci wirtualnych.

    ![Serwery DNS](./media/migrate-best-practices-networking/dns2.png) *serwery DNS dla sieci wirtualnej*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) rozpoznawania nazw, gdy używasz własnego serwera DNS.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-subscriptions) o regułach i ograniczeniach nazewnictwa DNS.

## <a name="best-practice-set-up-availability-zones"></a>Najlepsze rozwiązanie: konfigurowanie stref dostępności

Strefy dostępności zwiększają wysoką dostępność, aby chronić aplikacje i dane przed awariami centrów danych.

- Strefy dostępności to unikatowe fizycznie lokalizacje w regionie platformy Azure.
- Każda strefa składa się z co najmniej jeden centrów danych, wyposażone w niezależne zasilanie, chłodzenie i usługi sieciowe.
- Aby zapewnić odporność, istnieje co najmniej trzy osobne strefy we wszystkich regionach włączone.
- Fizyczne rozdzielenie stref dostępności w obrębie regionu chroni aplikacje i dane przed awariami centrum danych.
- Strefowo nadmiarowe usługi Replikowanie aplikacji i danych w strefach dostępności, aby chronić przed pojedynczych punktów awarii. — Dzięki strefom dostępności platforma Azure oferuje umową SLA gwarantującą dostępność przez 99,99% dostępności maszyn wirtualnych.

    ![Strefa dostępności](./media/migrate-best-practices-networking/availability-zone.png) *strefy dostępności*

- Możesz zaplanować i opracować wysokiej dostępności do architektury migracji kolokowanie obliczeń, magazynu, sieci i zasobów danych w strefie, a replikowanie ich w innych strefach. Usługi platformy Azure, które obsługują strefy dostępności, dzielą się na dwie kategorie:
  - Usługi strefowe: zasób jest kojarzony z określoną strefą. Na przykład maszyny wirtualne, dyski zarządzane, adresy IP.
  - Usługi strefowo nadmiarowe: zasób jest replikowany automatycznie między strefami. Na przykład magazyn strefowo nadmiarowy, usługa Azure SQL Database.
- Możesz wdrożyć standardowe obciążenia platformy Azure równoważenia obciążenia dostępnego z Internetu lub warstwy aplikacji w celu zapewnienia odporności strefowej.

    ![Moduł równoważenia obciążenia](./media/migrate-best-practices-networking/load-balancer.png) *modułu równoważenia obciążenia*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/availability-zones/az-overview) stref dostępności.

## <a name="design-hybrid-cloud-networking"></a>Sieć w chmurze hybrydowej projektu

W przypadku pomyślnej migracji bardzo ważne jest łączenie z firmową siecią lokalną z platformą Azure. Spowoduje to utworzenie połączenia zawsze włączone, znane jako sieć chmury hybrydowej, w których usługi są dostępne na platformie Azure w chmurze i użytkowników firmowych. Istnieją dwie opcje tworzenia sieci tego typu:

- **Sieć VPN typu lokacja-lokacja:** połączenie typu lokacja-lokacja jest ustanawiane między lokalnym urządzeniem VPN i bramą Azure VPN Gateway, która jest wdrażana w sieci wirtualnej. Każdy autoryzowany zasób lokalny może uzyskać dostęp do sieci wirtualnych. Komunikacja między lokacjami jest wysyłana przez szyfrowany tunel za pośrednictwem Internetu.
- **Azure ExpressRoute:** połączenie usługi Azure ExpressRoute jest ustanawiane między siecią lokalną i platformą Azure za pośrednictwem partnera usługi ExpressRoute. To połączenie jest prywatne i ruch nie przechodzi przez Internet.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) o sieci w chmurze hybrydowej.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Najlepsze rozwiązanie: implementowanie sieci VPN typu lokacja-lokacja o wysokiej dostępności

Aby zaimplementować sieć VPN typu lokacja-lokacja, należy skonfigurować bramę sieci VPN na platformie Azure.

- Tworzenie bramy sieci VPN jest określonego typu bramy sieci wirtualnej, która jest używana do wysyłania zaszyfrowanego ruchu sieciowego między siecią wirtualną platformy Azure a lokalizacją lokalną za pośrednictwem publicznej sieci Internet.
- Tworzenie bramy sieci VPN umożliwia również wysyłać zaszyfrowany ruch sieciowy między sieciami wirtualnymi platformy Azure za pośrednictwem sieci firmy Microsoft.
- Każda sieć wirtualna może mieć tylko jedną bramę sieci VPN.
- Możesz utworzyć wiele połączeń z tą samą bramą sieci VPN. Podczas tworzenia wielu połączeń, wszystkie tunele VPN współdzielą dostępną przepustowość bramy.
- Każda brama Azure VPN Gateway składa się z dwóch wystąpień działających w konfiguracji aktywne-w gotowości.
  - W przypadku planowanej konserwacji lub nieplanowanych zakłóceń działania aktywnego wystąpienia następuje przejście w tryb failover, a wystąpienie w trybie gotowości automatycznie przejmuje zadanie i wznawia połączenie typu lokacja-lokacja lub połączenie między sieciami wirtualnymi.
  - Przełączenie powoduje krótką przerwę w działaniu.
  - W przypadku planowanej konserwacji łączność powinna zostać przywrócona w ciągu od 10 do 15 sekund.
  - W przypadku nieplanowanych awarii odzyskiwanie połączenia trwa dłużej, od 1 do 1,5 minuty w najgorszym przypadku.
  - Połączenia klienta sieci VPN typu punkt-lokacja (P2S) z bramą zostaną rozłączone, a użytkownicy będą musieli ponownie nawiązać połączenia z poziomu maszyn klienckich.

Podczas konfigurowania sieci VPN typu lokacja-lokacja należy wykonać następujące czynności:

- Potrzebna jest sieć wirtualna, której zakres adresów nie nakłada się na sieć lokalną, z której zostanie połączona sieć VPN.
- W sieci należy utworzyć podsieć bramy.
- Tworzenie bramy sieci VPN, określ typ bramy (VPN) i czy brama jest oparta na zasadach lub oparte na trasach. Sieć VPN typu RouteBased jest zalecane jako bardziej możliwością i Zadbaj o przyszłość.
- Tworzenie bramy sieci lokalnej w środowisku lokalnym, a następnie skonfigurować urządzenie sieci VPN w środowisku lokalnym.
- Możesz utworzyć połączenie sieci VPN lokacja lokacja trybu failover między bramą sieci wirtualnej i lokalnym urządzeniem. Za pomocą opartej na trasach VPN umożliwia aktywny / pasywny lub aktywny aktywny połączenia z platformą Azure. Oparta na trasach obsługuje również lokacja lokacja (za pomocą dowolnego komputera) i połączenia punkt lokacja (z jednego komputera) jednocześnie.
- Należy określić jednostkę SKU, którego chcesz używać bramy. To zależy od wymagań dotyczących obciążenia, przepustowości, funkcji i umów SLA.
- Protokół border gateway protocol (BGP) to opcjonalna funkcja za pomocą usługi Azure ExpressRoute i bramami sieci VPN opartej na trasach umożliwia propagację trasy protokołu BGP w środowisku lokalnym w Twoich sieciach wirtualnych.

![Sieć VPN](./media/migrate-best-practices-networking/vpn.png)
*sieci VPN typu lokacja lokacja*

**Dowiedz się więcej:**

- [Przegląd](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) zgodne lokalnymi urządzeniami sieci VPN.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) bram sieci VPN.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) połączeń sieci VPN o wysokiej dostępności.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) planowanie i projektowanie bramy sieci VPN.
- [Przegląd](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) ustawień usługi VPN gateway.
- [Przegląd](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) jednostki SKU bramy.
- [Poczytaj o](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) konfigurowaniu protokołu BGP za pomocą bram sieci VPN platformy Azure.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Najlepsze rozwiązanie: konfigurowanie bramy na potrzeby bram VPN Gateway

Podczas tworzenia bramy sieci VPN na platformie Azure należy użyć specjalnej podsieci o nazwie GatewaySubnet. Podczas tworzenia tej uwagi podsieci te najlepsze rozwiązania:

- Długość prefiksu podsieci bramy może mieć maksymalną długość 29 (na przykład 10.119.255.248/29). Bieżący zalecane jest, że używasz długość prefiksu 27 (na przykład 10.119.255.224/27).
- Podczas definiowania przestrzeni adresowej podsieci bramy należy użyć ostatniej części przestrzeni adresowej sieci wirtualnej.
- Korzystając z platformy Azure podsieci GatewaySubnet, nigdy nie należy wdrażać żadnych maszyn wirtualnych lub innych urządzeń, takich jak Application Gateway w ramach podsieci bramy.
- Nie przypisuj grupy zabezpieczeń sieci (NSG) do tej podsieci. Go spowoduje, że brama przestanie działać.

**Dowiedz się więcej:**

- [Użyj tego narzędzia](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed), aby określić przestrzeń adresową IP.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Najlepsze rozwiązanie: implementowanie usługi Azure Virtual WAN dla biur oddziałów

W przypadku wielu połączeń sieci VPN Azure Virtual WAN to usługa sieciowa zapewniająca zoptymalizowaną i zautomatyzowaną łączność między oddziałami za pośrednictwem platformy Azure.

- Usługa Virtual WAN umożliwia łączenie urządzeń w oddziałach z platformą Azure i konfigurowanie ich komunikacji. Można to zrobić ręcznie lub za pomocą urządzeń preferowanych dostawców — partnerów usługi Virtual WAN.
- Za pomocą preferowanego dostawcy urządzeń umożliwia proste zarządzanie użycia, łącznością i konfiguracji.
- Azure w sieci WAN wbudowany pulpit nawigacyjny zapewnia błyskawiczny wgląd rozwiązywania problemów, które zaoszczędzić czas i w prosty sposób śledzenia na dużą skalę połączenia lokacja lokacja.

**Dowiedz się więcej:** 
[Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) o usłudze Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Najlepsze rozwiązanie: implementowanie usługi ExpressRoute dla połączeń krytycznych dla działalności firmy

Usługa Azure ExpressRoute rozszerza infrastrukturę lokalną do chmury firmy Microsoft przez tworzenie prywatnych połączeń między wirtualnym centrum danych platformy Azure i sieciami lokalnymi.

- Połączenia usługi ExpressRoute mogą znajdować się w sieci typu dowolny-dowolny (sieć VPN IP), sieci Ethernet typu punkt-punkt lub za pośrednictwem dostawcy połączenia. One omijają publiczny internet.
- Połączenia ExpressRoute zapewniają wyższy poziom zabezpieczeń, niezawodność i szybkość (10 GB/s), wraz z spójne opóźnienia.
- Usługa ExpressRoute jest przydatne w przypadku wirtualnych centrów danych, jak klienci mogą uzyskać korzyści wynikające z reguły zgodności, skojarzone z prywatnych połączeń.
- Usługa ExpressRoute bezpośrednio można połączyć się bezpośrednio do firmy Microsoft routery przy 100Gbps na potrzeby większej przepustowości.
- Usługi ExpressRoute używa protokołu BGP w celu wymiany tras między sieciami lokalnymi, wystąpienia platformy Azure i publicznymi adresami Microsoft.

Wdrażanie połączeń usługi ExpressRoute obejmuje zazwyczaj zaangażowanie dostawcy usług ExpressRoute. Typowym sposobem szybkiego rozpoczynania pracy jest użycie najpierw sieci VPN typu lokacja-lokacja do ustanowienia połączenia między wirtualnym centrum danych i zasobami lokalnymi, a następnie przeprowadzenie migracji do połączenia usługi ExpressRoute po ustanowieniu fizycznego wzajemnego połączenia z dostawcą usługi.

**Dowiedz się więcej:**

- [Przeczytaj](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) omówienie usługi ExpressRoute.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) o usłudze ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Najlepsze rozwiązanie: optymalizowanie routingu usługi ExpressRoute przy użyciu społeczności BGP

Jeśli masz wiele obwodów usługi ExpressRoute, masz więcej niż jedną ścieżkę łączenia z firmą Microsoft. W związku z tym może wystąpić routing nieoptymalny, tzn. ruch może użyć dłuższej ścieżki w celu dotarcia do firmy Microsoft lub z firmy Microsoft do sieci użytkownika. Im dłuższa ścieżka sieciowa, tym większe opóźnienie. Opóźnienie ma bezpośredni wpływ na wydajność aplikacji i środowisko użytkownika.

**Przykład:**

Zapoznajmy się z przykładem:

- masz dwa biura w USA: jedno w Los Angeles i jedno w Nowym Jorku.
- Biura są połączone w sieci WAN, który może być Twoją siecią podstawową lub dostawcą usług IP VPN.
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

Aby zoptymalizować routing dla użytkowników obu biur, trzeba wiedzieć, który prefiks odpowiada zachodnim, a który wschodnim stanom USA. Możesz zakodować te informacje przy użyciu wartości społeczności BGP.

- Przypisujesz unikatową wartość społeczności BGP do każdego regionu świadczenia usługi Azure. Na przykład 12076:51004 dla wschodnich i 12076:51006 dla zachodnich stanów USA.
- Teraz, gdy jest jasne, który prefiks należy do którego regionu platformy Azure, możesz skonfigurować preferowany obwód usługi ExpressRoute.
- Ponieważ do wymiany informacji o routingu używasz protokołu BGP, w celu wpłynięcia na routing możesz użyć preferencji lokalnej protokołu BGP.
- W naszym przykładzie przypisujesz wyższą wartość preferencji lokalnej na 13.100.0.0/16 w zachodnich niż we wschodnich stanach USA i podobnie wyższą wartość preferencji lokalnej na 23.100.0.0/16 we wschodnich niż w zachodnich stanach USA.
- Ta konfiguracja zapewnia, że zarówno ścieżki do firmy Microsoft są dostępne, będą łączyli się zachodnich stanach USA przy użyciu obwodu zachodnie użytkownicy w Los Angeles, gdy użytkownicy Nowy Jork nawiązać wschodnie stany USA przy użyciu obwodu Wschodnia. Routing jest zoptymalizowany po obu stronach.

![Sieć VPN](./media/migrate-best-practices-networking/bgp2.png)
*społeczności BGP zoptymalizowane pod kątem połączenia*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) na temat optymalizowania routingu.

## <a name="securing-vnets"></a>Zabezpieczanie sieci wirtualnych

Odpowiedzialność za zabezpieczanie sieci wirtualnych jest podzielona między firmę Microsoft i użytkownika. Firma Microsoft oferuje wiele funkcji sieciowych, a także usług, które ułatwiają zabezpieczanie zasobów. W przypadku projektowania zabezpieczeń sieci wirtualnych najlepsze rozwiązania, które warto zastosować, obejmują implementację sieci obwodowej, użycie filtrowania i grup zabezpieczeń, zabezpieczanie dostępu do zasobów i adresów IP oraz implementowanie ochrony przed atakami.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) najlepszych rozwiązań zabezpieczeń sieciowych.
- [Dowiedz się](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security), jak projektować bezpieczne sieci.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Najlepsze rozwiązanie: implementowanie sieci obwodowej platformy Azure

Mimo że firma Microsoft inwestuje bardzo dużo w ochronę infrastruktury chmury, musisz również chronić usługi w chmurze i grupy zasobów. Wielowarstwowego podejścia do zabezpieczeń zapewnia najlepszą ochronę. Umieszczenie sieci obwodowej w miejscu stanowi ważną część strategii obrony.

- Sieci obwodowej chroni wewnętrznych zasobów sieciowych z niezaufaną siecią.
- To najbardziej zewnętrznej warstwy, która jest połączone z Internetem. Zazwyczaj znajduje się między Internetem a infrastrukturą przedsiębiorstwa, zazwyczaj z pewnego rodzaju ochrony po obu stronach.
- W topologii sieci typowego przedsiębiorstwa infrastrukturze podstawowej jest silnie wzmocnione na strefy, dzięki wielu wbudowanym warstwom zabezpieczeń urządzeń. Granicę każda warstwa składa się z urządzeniami i punkty wymuszania zasad.
- Każda warstwa może zawierać kombinację rozwiązania zabezpieczeń sieciowych, które zawierają zapór, zapobiegania przeprowadzenie ataku typu "odmowa usługi" (DoS), systemy ochrony wykrywania/nieautoryzowanego nieautoryzowanego dostępu (IDS/IPS) i urządzenia sieci VPN.
- Wymuszanie zasad w sieci obwodowej użyć zasad zapory, listy kontroli dostępu (ACL) lub specyficznego routingu.
- Ponieważ ruch przychodzący dociera z Internetu, ma został przechwycony i obsługiwane przy użyciu kombinacji rozwiązanie chroniące blokowanie ataków i szkodliwy ruch, zapewniając uzasadnione żądania do sieci.
- Ruch przychodzący może kierować bezpośrednio do zasobów w sieci obwodowej. Zasób sieci obwodowej, następnie może komunikować się z innymi zasobami, które są bardziej w sieci, przeniesienie do przodu ruch do sieci po weryfikacji.

Poniższej ilustracji przedstawiono przykład sieci obwodowej jednej podsieci w sieci firmowej, z dwoma granic zabezpieczeń.

![Sieć VPN](./media/migrate-best-practices-networking/perimeter.png)
*wdrażania w sieci obwodowej*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o wdrażaniu sieci obwodowej między platformą Azure i lokalnym centrum danych.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Najlepsze rozwiązanie: filtrowanie ruchu sieci wirtualnej za pomocą sieciowych grup zabezpieczeń

Sieciowe grupy zabezpieczeń zawierają wiele reguł zabezpieczeń dla ruchu przychodzącego i wychodzącego, które filtrują ruch przechodzący do i z zasobów. Filtrowanie może być przez źródłowy i docelowy adres IP, portu i protokołu.

- Sieciowe grupy zabezpieczeń zawierają reguły zabezpieczeń, które blokują lub zezwalają na ruch do sieci dla ruchu przychodzącego (lub wychodzącego ruchu sieciowego z) kilka typów zasobów platformy Azure. Dla każdej reguły można określić źródło i obiekt docelowy, port i protokół.
- Reguły sieciowej grupy zabezpieczeń są oceniane według priorytetu, korzystając z informacji 5 krotka (źródłowy, port źródłowy, docelowy, port docelowy i protokół) do blokują lub zezwalają na ruch.
- Rekord przepływu tworzony jest dla istniejących połączeń. Komunikacja jest dozwolona lub zablokowana na podstawie stanu połączenia z rekordu przepływu.
- Przepływ rekord umożliwia sieciowej grupy zabezpieczeń można stanowych. Na przykład jeśli zostanie określona reguła zabezpieczeń dla ruchu wychodzącego do dowolnego adresu za pośrednictwem portu 80, nie musisz odpowiadać na ruch wychodzący regułę zabezpieczeń dla ruchu przychodzącego. Należy tylko określić regułę zabezpieczeń dla ruchu przychodzącego w przypadku, jeśli komunikacja jest inicjowana zewnętrznie.
- Jest to również prawdziwe w odwrotnym przypadku. Ruch przychodzący jest dozwolony przez port, nie trzeba określić regułę zabezpieczeń dla ruchu wychodzącego, aby odpowiadać na ruch przychodzący przez port.
- Istniejące połączenia nie są przerwane po usunięciu reguły zabezpieczeń, która umożliwiała przepływ. Widok przepływów ruchu sieciowego są przerywane, połączenia zostaną zatrzymane, gdy żaden ruch nie jest danych w dowolnym kierunku, przez co najmniej kilka minut.
- Podczas tworzenia sieciowych grup zabezpieczeń utwórz ich jak najmniej, ale tyle, ile potrzebujesz.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Najlepsze rozwiązanie: bezpieczny ruch typu północ/południe i wschód/zachód

W przypadku zabezpieczania sieci wirtualnych ważne jest rozważenie wektorów ataków.

- Przy użyciu tylko podsieć sieciowych grup zabezpieczeń upraszcza środowiska, ale tylko zabezpiecza ruch do podsieci. Jest to nazywane północ/południe ruchu.
- Ruch między maszynami wirtualnymi w tej samej podsieci jest znany jako ruch typu wschód/zachód.
- Ważne jest używanie obu rodzajów ochrony, ponieważ jeśli haker uzyska dostęp z zewnątrz, zostanie zatrzymany podczas próby dołączenia maszyn znajdujących się w tej samej podsieci.

### <a name="use-service-tags-on-nsgs"></a>Używanie tagów usług w sieciowych grupach zabezpieczeń

Tag usługi reprezentuje grupę prefiksów adresów IP. Przy użyciu tagu usługi pomaga zminimalizować złożoność tworzenia reguły sieciowej grupy zabezpieczeń.

- Podczas tworzenia reguł, można użyć tagów usługi zamiast konkretnych adresów IP.
- Firma Microsoft zarządza prefiksami adresów skojarzony z tag usługi i automatycznie aktualizuje tag usługi, po zmianie adresów.
- Nie można utworzyć własnego tagu usługi ani określić, jakie adresy IP są uwzględniane w tagu.

Tagi usługi zająć ręczna Praca poza Przypisywanie reguły do grup usług platformy Azure. Na przykład, jeśli chcesz zezwolić w podsieci sieci wirtualnej, zawierającej dostęp serwerów sieci web do usługi Azure SQL Database, możesz można utworzyć regułę dla ruchu wychodzącego do portu 1433 i użyj **Sql** tag usługi.

- To **Sql** tag określa prefiksy adresów usług Azure SQL Database i Azure SQL Data Warehouse.
- Jeśli określisz **Sql** jako wartość, ruch jest dozwolony lub zablokowany do bazy danych Sql.
- Jeśli chcesz zezwolić na dostęp do **Sql** w określonym regionie, można określić tego regionu. Na przykład, jeśli chcesz zezwolić na dostęp tylko do usługi Azure SQL Database w regionie wschodnie stany USA, można określić **Sql.EastUS** jako tag usługi.
- Tag reprezentuje usługę, ale nie konkretne wystąpienia usługi. Na przykład tag reprezentuje usługę Azure SQL Database, ale nie zawiera określonej bazy danych SQL lub serwera.
- Wszystkie prefiksy adresów reprezentowane przez ten tag są również reprezentowane przez tag **Internet**.

**Dowiedz się więcej:**

- [Przeczytaj o](https://docs.microsoft.com/azure/virtual-network/security-overview) sieciowych grup zabezpieczeń.
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) tagi usług dostępne dla sieciowych grup zabezpieczeń.

## <a name="best-practice-use-application-security-groups"></a>Najlepsze rozwiązanie: używanie grup zabezpieczeń aplikacji

Grupy zabezpieczeń aplikacji umożliwiają konfigurowanie zabezpieczeń sieci jako naturalnego rozszerzenia struktury aplikacji.

- Można pogrupować maszyny wirtualne i definiowanie zasad zabezpieczeń sieci opartych na grupach zabezpieczeń aplikacji.
- Grupy zabezpieczeń aplikacji umożliwiają ponowne używanie zasady zabezpieczeń na dużą skalę bez ręcznej obsługi jawnych adresów IP.
- Grupy zabezpieczeń aplikacji obsługują złożoność jawnych adresów IP i wiele zestawów reguł, co pozwala skupić się na logice biznesowej.

**Przykład:**

![Grupa zabezpieczeń aplikacji](./media/migrate-best-practices-networking/asg.png)
*Przykład grupy zabezpieczeń aplikacji*

**Interfejs sieciowy** | **Grupy zabezpieczeń aplikacji**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- W tym przykładzie każdy interfejs sieciowy należy do tylko jednej grupy zabezpieczeń aplikacji, ale w rzeczywistości interfejs może należeć do wielu grup, zgodnie z limity platformy Azure.
- Żadna z interfejsów sieciowych nie ma skojarzonej sieciowej grupy zabezpieczeń. NSG1 jest skojarzona z obu podsieci i zawiera następujące reguły.

<!--markdownlint-disable MD033 -->

**Nazwa reguły** | **Cel** | **Szczegóły**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Zezwalać na ruch z Internetu do serwerów sieci web. Ruch przychodzący z Internetu jest blokowany przez domyślną regułę zabezpieczeń DenyAllInbound, dlatego dodatkowa reguła nie jest potrzebna w przypadku grup zabezpieczeń aplikacji AsgLogic i AsgDb. | Priorytet: 100<br/><br/> Źródło: Internet<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgWeb<br/><br/> Port docelowy: 80<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwól.
Deny-Database-All | Domyślna reguła zabezpieczeń AllowVNetInBound zezwala na całą komunikację między zasobami w tej samej sieci wirtualnej, ta zasada jest potrzebna w celu blokowania ruchu ze wszystkich zasobów. | Priorytet: 120<br/><br/> Źródło: *<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: Wszyscy<br/><br/> Dostęp: Zablokuj.
Allow-Database-BusinessLogic | Zezwolenie na ruch z grupy zabezpieczeń aplikacji AsgLogic do grupy zabezpieczeń aplikacji AsgDb. Priorytet tej reguły jest wyższy niż priorytet reguły Deny-Database-All i jest ona przetwarzana przed tą regułą, dlatego ruch z grupy zabezpieczeń aplikacji AsgLogic jest dozwolony, a cały pozostały ruch jest blokowany. | Priorytet: 110<br/><br/> Źródło: AsgLogic<br/><br/> Port źródłowy: *<br/><br/> Miejsce docelowe: AsgDb<br/><br/> Port docelowy: 1433<br/><br/> Protokół: TCP<br/><br/> Dostęp: Zezwól.

<!--markdownlint-enable MD033 -->

- Reguły określające grupę zabezpieczeń aplikacji jako źródło lub obiekt docelowy są stosowane tylko do interfejsów sieciowych, które są elementami członkowskimi grupy zabezpieczeń aplikacji. Jeśli interfejs sieciowy nie jest elementem członkowskim grupy zabezpieczeń aplikacji, reguła nie jest stosowana do tego interfejsu sieciowego, mimo że grupa zabezpieczeń sieci jest skojarzona z podsiecią.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) o grupach zabezpieczeń aplikacji.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Najlepsze rozwiązanie: zabezpieczanie dostępu do usługi PaaS za pomocą punktów końcowych usługi sieci wirtualnej

Punkty końcowe usługi sieci wirtualnej rozszerzają prywatną przestrzeń adresową i tożsamość sieci wirtualnej do usług platformy Azure za pośrednictwem połączenia bezpośredniego.

- Punkty końcowe umożliwiają zabezpieczanie zasobów usługi platformy Azure krytyczne tylko sieci wirtualne. Ruch z sieci wirtualnej do usługi platformy Azure zawsze pozostaje w sieci szkieletowej platformy Microsoft Azure.
- Przestrzeń prywatnych adresów sieci wirtualnej mogą nakładające się przestrzenie i dlatego nie może być używany do jednoznacznego identyfikowania ruch pochodzący z sieci wirtualnej.
- Po włączeniu punktów końcowych usługi w sieci wirtualnej można zabezpieczyć zasoby usługi platformy Azure przez dodanie reguły sieci wirtualnej do zasobów usługi. To zapewnia wyższy poziom zabezpieczeń, w pełni usunięcie publicznego dostępu do Internetu do zasobów i zezwolenie na ruch tylko z sieci wirtualnej.

![Punkty końcowe usługi](./media/migrate-best-practices-networking/endpoint.png)
*punkty końcowe usługi*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o punktach końcowych usługi sieci wirtualnej.

## <a name="best-practice-control-public-ip-addresses"></a>Najlepsze rozwiązanie: kontrolowanie publicznych adresów IP

Publiczne adresy IP na platformie Azure mogą być kojarzone z maszynami wirtualnymi, modułami równoważenia obciążenia, bramami aplikacji i bramami sieci VPN.

- Publiczne adresy IP umożliwiają zasobom internetowym komunikowanie się w ramach ruchu przychodzącego z zasobami platformy Azure, a zasobom platformy Azure komunikowanie się w ramach ruchu wychodzącego z Internetem.
- Publiczne adresy IP są tworzone przy użyciu podstawowej lub standardowej jednostki SKU, między którymi występuje kilka różnic. Standardowe jednostki SKU można przypisać do dowolnej usługi, ale zazwyczaj są one konfigurowane na maszynach wirtualnych, w modułach równoważenia obciążenia i w bramach aplikacji.
- Należy zauważyć, że podstawowa publiczny adres IP nie ma sieciową grupę zabezpieczeń konfigurowane automatycznie. Musisz skonfigurować własne i przypisać zasady kontroli dostępu. Standardowe adresy IP jednostki SKU ma sieciową grupę zabezpieczeń i reguł, które domyślnie przypisane.
- Najlepszym rozwiązaniem jest maszyn wirtualnych nie powinien mieć skonfigurowaną publicznego adresu IP.
  - Jeśli potrzebujesz, aby otworzyć port, powinno to być dla usług sieci web, taki jak port 80 i 443.
  - Porty standardowa zdalnego zarządzania, takie jak SSH (22) i protokołu RDP (3389) powinna być równa Odmów wraz z innych portów, przy użyciu sieciowych grup zabezpieczeń.
- Jest to lepsze rozwiązanie do umieszczenia maszyn wirtualnych za bramą Azure load balancer lub aplikacji. Następnie w razie potrzeby uzyskania dostępu do portów zarządzania zdalnego przy użyciu dostępu do maszyny Wirtualnej just-in-time w usłudze Azure Security Center.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses) publiczne adresy IP na platformie Azure.
- [Poczytaj więcej](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) o dostępie typu just-in-time do maszyny wirtualnej w usłudze Azure Security Center.

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Korzystanie z zalet funkcji zabezpieczeń platformy Azure dla sieci

Platforma Azure ma funkcje zabezpieczeń platformy, które są łatwe w użyciu i zapewniają rozbudowane środki zaradcze w przypadku typowych ataków w sieci. Obejmują one zaporę platformy Azure, zaporę aplikacji internetowej i usługę Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Najlepsze rozwiązanie: wdrażanie usługi Azure Firewall

Azure Firewall to zarządzana, sieciowa usługa zabezpieczeń oparta na chmurze, która zabezpiecza zasoby sieci wirtualnej. Jest to w pełni stanowa zapora zarządzana z wbudowaną wysoką dostępnością i możliwością nieograniczonego skalowania w chmurze.

![Punkty końcowe usługi](./media/migrate-best-practices-networking/firewall.png)
*Azure Firewall*

- Usługa Azure Firewall może centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych.
- Usługa Azure Firewall korzysta ze statycznego publicznego adresu IP dla zasobów sieci wirtualnej, co umożliwia zewnętrznym zaporom identyfikowanie ruchu pochodzącego z sieci wirtualnej.
- Zaporę platformy Azure jest w pełni zintegrowana z usługą Azure Monitor rejestrowania i analizy.
- Najlepszym rozwiązaniem podczas tworzenia reguł zapory usługi Azure należy użyć tagów w pełni kwalifikowaną nazwę domeny do tworzenia reguł.
  - FQDN tag reprezentuje grupę nazw FQDN skojarzone z dobrze znanych usług firmy Microsoft.
  - Za pomocą tagu w pełni kwalifikowaną nazwę domeny umożliwia wymagane wychodzącego ruchu sieciowego przez zaporę.
- Na przykład aby ręcznie zezwolić na Windows Update ruchu sieciowego przez zaporę, będziesz potrzebować umożliwiający tworzenie wielu reguł aplikacji. Za pomocą tagów w pełni kwalifikowaną nazwę domeny, Utwórz regułę aplikacji, a include — tag aktualizacji Windows. Z tą regułą w miejscu ruchu sieciowego do punktów końcowych usługi Microsoft Windows Update może przepływać przez zaporę.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/firewall/overview) zapory platformy Azure.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/firewall/fqdn-tags) o tagach FQDN.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Najlepsze rozwiązanie: wdrażanie zapory aplikacji internetowej

Aplikacje internetowe coraz częściej stają się obiektami złośliwych ataków wykorzystujących znane luki w zabezpieczeniach. Luki w zabezpieczeniach to ataki przez wstrzyknięcie kodu SQL i ataki z użyciem skryptów między witrynami. Zapobieganie atakom na takie w kodzie aplikacji może stanowić wyzwanie i mogą wymagać rygorystycznego przestrzegania harmonogramu konserwacji, poprawek i monitorowania na poziomie wielu warstw topologii aplikacji. Zapory aplikacji internetowych scentralizowane ułatwia zarządzanie zabezpieczeniami przyspiesza i ułatwia administratorom aplikacji, ochrona przed zagrożeniami i intruzami. Zapora aplikacji sieci web może reagować na zagrożenia bezpieczeństwa szybciej, poprzez wdrażanie poprawek znanych luk w zabezpieczeniach w centralnej lokalizacji zamiast zabezpieczanie poszczególnych aplikacjach sieci web. Istniejące bramy Application Gateway można łatwo przekonwertować na bramę Application Gateway obsługującą zaporę aplikacji internetowej.

Zapora aplikacji internetowej to funkcja usługi Azure Application Gateway.

- Zapora aplikacji internetowej zapewnia centralną ochronę aplikacji internetowych przez typowymi atakami wykorzystującymi luki i lukami w zabezpieczeniach.
- Zapora aplikacji internetowej chroni bez modyfikacji kodu zaplecza.
- Może ona jednocześnie chronić wiele aplikacji internetowych za bramą aplikacji.
- Zapora aplikacji internetowej jest integrowana z usługą Azure Security Center.
- Można dostosować reguły zapory aplikacji sieci Web i grup reguł, aby odpowiadał wymaganiom Twojej aplikacji.
- Najlepszym rozwiązaniem zapory aplikacji sieci Web należy używać z przodu, w żadnej aplikacji przeznaczonych dla sieci web, w tym aplikacje na maszynach wirtualnych platformy Azure lub usługi Azure App Service.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/application-gateway/waf-overview) zapory aplikacji sieci Web.
- [Przejrzyj](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) ograniczenia i wykluczenia dotyczące zapory aplikacji internetowej.

## <a name="best-practice-implement-azure-network-watcher"></a>Najlepsze rozwiązanie: implementowanie usługi Azure Network Watcher

Usługa Azure Network Watcher udostępnia narzędzia do monitorowania zasobów i komunikacji w sieci wirtualnej platformy Azure. Na przykład można monitorować komunikacji między maszyny Wirtualnej i punktu końcowego, takie jak innej maszyny Wirtualnej lub nazwa FQDN, wyświetlanie zasobów i relacji między zasobami w sieci wirtualnej, lub diagnozować problemy z ruchem sieciowym.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Przy użyciu usługi Network Watcher można monitorować i diagnozować problemy z siecią bez logując się do maszyn wirtualnych.
- Możesz wyzwalać Przechwytywanie pakietów przez ustawienie alertów i uzyskać dostęp do informacji o wydajności w czasie rzeczywistym na poziomie pakietów. Można szczegółowo analizować problemy.
- Najlepszym rozwiązaniem jest użycie usługi Network Watcher do przeglądania dzienników przepływów sieciowych grup zabezpieczeń.
  - Dzienniki przepływów sieciowych grup zabezpieczeń w usłudze Network Watcher umożliwiają wyświetlanie informacji dotyczących ruchu IP przychodzącego i wychodzącego przez sieciową grupę zabezpieczeń.
  - Dzienniki przepływów są pisane w formacie JSON.
  - Dzienniki przepływów przedstawiają przepływy wychodzące i przychodzące dla każdej reguły, interfejs sieciowy, do którego odnosi się przepływ, 5-krotkowe informacje o przepływie (źródłowy/docelowy adres IP, port źródłowy/docelowy i protokół) oraz informację zezwoleniu na ruch albo jego zablokowaniu.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/network-watcher) usługi Network Watcher.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) dzienniki przepływu o sieciowej grupy zabezpieczeń.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Korzystaj z narzędzi partnera w witrynie Azure Marketplace

Bardziej złożone topologie sieci można skorzystać z produktów zabezpieczeń od naszych partnerów firmy Microsoft, która znajduje się w określonej sieci wirtualne urządzenia (urządzenia WUS).

- Urządzenie NVA jest maszyną Wirtualną, która realizuje funkcje sieci, takie jak zapora, Optymalizacja sieci WAN lub inne funkcje sieci.
- Wirtualne urządzenia sieciowe wzmacniają zabezpieczenia sieci wirtualnej i funkcje sieciowe. Można je wdrażać w przypadku zapór o wysokiej dostępności, zapobiegania włamaniom, wykrywania intruzów, zapór aplikacji internetowych, optymalizacji sieci WAN, routingu, równoważenia obciążenia, sieci VPN, zarządzania certyfikatami, usługi Active Directory i uwierzytelniania wieloskładnikowego.
- Wirtualne urządzenia sieciowe są oferowane przez wielu dostawców w witrynie  [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Najlepsze rozwiązanie: implementowanie zapór i wirtualnych urządzeń sieciowych w sieciach centrów

W centrum sieć obwodowa (z dostępem do Internetu) jest zazwyczaj zarządzana za pomocą zapory platformy Azure, farmy zapór lub zapory aplikacji internetowej. Przeanalizujmy następujące porównania.

<!--markdownlint-disable MD033 -->

**Typ zapory** | **Szczegóły**
--- | ---
Zapory aplikacji internetowych | Aplikacje internetowe są powszechnie używane oraz często mają luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki.<br/><br/> Zapory aplikacji internetowych są projektowane tak, aby wykrywać ataki na aplikacje internetowe (HTTP/HTTPS) skuteczniej niż zapora ogólna.<br/><br/> W porównaniu z tradycyjną technologią zapory aplikacji internetowych mają zestaw konkretnych funkcji chroniących wewnętrzne serwery internetowe przed zagrożeniami.
Azure Firewall | Podobnie jak w przypadku farm zapór wirtualnych urządzeń sieciowych usługa Azure Firewall używa wspólnego mechanizmu administrowania oraz zestawu reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach szprych i kontrolować dostęp do sieci lokalnych.<br/><br/> Usługa Azure Firewall ma wbudowaną skalowalność.
Zapory wirtualnych urządzeń sieciowych | Podobnie jak urządzenie WUS zapory usługi Azure farm zapory mają wspólnego mechanizmu administracji i zestaw reguł zabezpieczeń, aby chronić obciążenia hostowane w sieciach gwiazdy i kontrolować dostęp do sieci lokalnej.<br/><br/> Urządzenie WUS zapory można ręcznie skalować za modułem równoważenia obciążenia.<br/><br/> Chociaż zapory urządzenie WUS nie ma mniej specjalistyczne oprogramowanie niż zapory aplikacji sieci Web ma szerszy zakres aplikacji do filtrowania i sprawdzić ruch wychodzący i przychodzący dowolnego typu.<br/><br/> Jeśli chcesz użyć urządzenia WUS można je znaleźć w witrynie Azure Marketplace.

<!--markdownlint-enable MD033 -->

Firma Microsoft zaleca używanie jednego zestawu Azure zapory (lub urządzenia WUS) dla ruchu pochodzącego z Internetu, a drugą dla ruchu pochodzącego w środowisku lokalnym.

- Przy użyciu tylko jeden zestaw zapory dla obu stanowi zagrożenie bezpieczeństwa, ponieważ on nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego.
- Korzystanie z warstw oddzielną zaporę zmniejsza złożoność sprawdzania zasad zabezpieczeń, a to oczywiste, które reguły dotyczą którego przychodzącego żądania sieciowego.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) przy użyciu urządzeń WUS w sieci wirtualnej platformy Azure.

## <a name="next-steps"></a>Kolejne kroki

Przejrzyj najlepsze rozwiązania:

- [Najlepsze praktyki](./migrate-best-practices-security-management.md) zabezpieczeń i zarządzania po migracji.
- [Najlepsze praktyki](./migrate-best-practices-costs.md) usługi cost management po migracji.
