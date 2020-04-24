---
title: 'Wirtualne centrum danych: perspektywa sieci'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak bezproblemowo rozbudować infrastrukturę do chmury i utworzyć architekturę wielowarstwową przy użyciu systemu Azure.
author: tracsman
ms.author: jonor
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: ba2933a90c67d1c7c0cd33057ab0b2476dfd584c
ms.sourcegitcommit: 825f9ae5b6cdd2fa6cb18c14a9733ba9106194f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81646973"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs iptables WAFs DDOS ITSM LLAP anycast vwan -->

# <a name="the-virtual-datacenter-a-network-perspective"></a>Wirtualne centrum danych: perspektywa sieci

Aplikacje migrowane z platformy lokalnej będą korzystać z bezpiecznej infrastruktury na platformie Azure, nawet przy minimalnych zmianach aplikacji. Nawet przedsiębiorstwa powinny dostosować swoje architektury, aby zwiększyć elastyczność i korzystać z możliwości platformy Azure.

Microsoft Azure zapewnia usługi i infrastrukturę z możliwością skalowania przy użyciu funkcji i niezawodności klasy korporacyjnej. Te usługi i infrastruktura oferują wiele opcji łączności hybrydowej, dzięki czemu klienci mogą wybierać dostęp do nich za pośrednictwem Internetu lub prywatnego połączenia sieciowego. Partnerzy firmy Microsoft mogą również zapewniać Ulepszone możliwości, oferując usługi zabezpieczeń i wirtualne urządzenia zoptymalizowane pod kątem działania na platformie Azure.

Klienci mogą korzystać z platformy Azure, aby bezproblemowo poszerzać infrastrukturę do chmury i budować architektury wielowarstwowe.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-virtual-datacenter"></a>Co to jest wirtualne centrum danych?

Chmura rozpoczęła się jako platforma do hostowania aplikacji publicznych. Przedsiębiorstwa uznały wartość chmury i rozpoczęły Migrowanie wewnętrznych aplikacji biznesowych. Te aplikacje przestosowały dodatkowe zagadnienia dotyczące zabezpieczeń, niezawodności, wydajności i kosztów, które wymagały dodatkowej elastyczności podczas dostarczania usług Cloud Services. Nowe usługi infrastruktury i sieci zostały zaprojektowane w celu zapewnienia tej elastyczności i nowych funkcji zapewnianych przez elastyczne skalowanie, odzyskiwanie po awarii i inne zagadnienia.

Rozwiązania w chmurze zostały początkowo zaprojektowane do obsługi jednego, relatywnie izolowanych aplikacji w spektrum publicznym. To podejście działało prawidłowo przez kilka lat. Ze względu na to, że korzyści z rozwiązań w chmurze zostały wyczyszczone, w chmurze obsługiwane są wiele obciążeń o dużej skali. Rozwiązywanie problemów dotyczących zabezpieczeń, niezawodności, wydajności i kosztów wdrożeń w jednym lub kilku regionach stało się istotne w całym cyklu życia usługi w chmurze.

Na przykładzie poniższego diagramu wdrożenia w chmurze czerwony prostokąt wyróżnia lukę w zabezpieczeniach. Żółte pole pokazuje możliwość optymalizowania sieciowych urządzeń wirtualnych w różnych obciążeniach.

![0][0]

Wirtualne centra danych pomagają osiągnąć skalę wymaganą dla obciążeń przedsiębiorstwa. Ta Skala musi zająć się wyzwaniami wprowadzonymi podczas uruchamiania aplikacji o dużej skali w chmurze publicznej.

Implementacja wirtualnego centrum danych (VDC) obejmuje więcej niż obciążenia aplikacji w chmurze. Zapewnia także sieć, zabezpieczenia, zarządzanie i inne infrastruktury, takie jak usługi DNS i Active Directory. W miarę migrowania dodatkowych obciążeń do platformy Azure należy wziąć pod uwagę infrastrukturę i obiekty, które obsługują te obciążenia. Starannie strukturę zasobów ułatwiają uniknięcie rozprzestrzeniania setek w setkach zarządzanych "wysp obciążeń" z niezależnymi przepływami danych, modelami zabezpieczeń i wyzwaniami dotyczącymi zgodności.

Koncepcja wirtualnego centrum danych zawiera zalecenia i projekty wysokiego poziomu służące do implementowania kolekcji oddzielnych, ale powiązanych jednostek. Te jednostki często mają wspólne funkcje pomocnicze, funkcje i infrastrukturę. Wyświetlanie obciążeń jako wirtualnego centrum danych pozwala osiągnąć obniżony koszt z oszczędności skalowania, zoptymalizowanych zabezpieczeń za pośrednictwem scentralizowanych składników i przepływów, a także ułatwić operacje, zarządzanie i inspekcje zgodności.

> [!NOTE]
> Wirtualne centrum danych **nie** jest określoną usługą platformy Azure. Zamiast tego różne funkcje i możliwości platformy Azure są łączone w celu spełnienia wymagań. Wirtualne centrum danych to sposób, w którym można myśleć o obciążeniach i użyciu platformy Azure w celu zoptymalizowania zasobów i możliwości w chmurze. Zapewnia modularne podejście do udostępniania usług IT na platformie Azure, zachowując jednocześnie role organizacyjne i obowiązki przedsiębiorstwa.

Wirtualne centrum danych ułatwia przedsiębiorstwom wdrażanie obciążeń i aplikacji na platformie Azure w następujących scenariuszach:

- Hostowanie wielu powiązanych obciążeń.
- Migruj obciążenia ze środowiska lokalnego na platformę Azure.
- Implementowanie wspólnych lub scentralizowanych wymagań dotyczących zabezpieczeń i dostępu w ramach obciążeń.
- DevOps i scentralizowanie odpowiednio dla dużego przedsiębiorstwa.

## <a name="who-should-implement-a-virtual-datacenter"></a>Kto powinien zaimplementować wirtualne centrum danych?

Każdy klient, który zdecydował się przyjąć platformę Azure, może skorzystać z efektywności konfigurowania zestawu zasobów do wspólnego użycia przez wszystkie aplikacje. W zależności od rozmiaru nawet pojedyncze aplikacje mogą korzystać z wzorców i składników używanych do kompilowania implementacji VDC.

Niektóre organizacje mają centralne zespoły lub działy dla IT, sieci, zabezpieczeń lub zgodności. Wdrożenie VDC może pomóc wymusić punkty zasad, oddzielać obowiązki i zapewnić spójność podstawowych składników. Zespoły aplikacji mogą zachować swobodę i kontrolę, która jest odpowiednia dla wymagań.

Organizacje z podejściem DevOps mogą również używać koncepcji VDC w celu zapewnienia autoryzowanych kieszeni zasobów platformy Azure. Ta metoda może zapewnić, że grupy DevOps mają całkowitą kontrolę w ramach tego grupowania, na poziomie subskrypcji lub w grupach zasobów w ramach wspólnej subskrypcji. W tym samym czasie granice sieci i zabezpieczeń pozostają zgodne zgodnie z definicją scentralizowanych zasad w sieci centrowej i centralnej zarządzanej grupy zasobów.

## <a name="considerations-for-implementing-a-virtual-datacenter"></a>Zagadnienia dotyczące implementacji wirtualnego centrum danych

Podczas projektowania wirtualnego centrum danych należy wziąć pod uwagę następujące problemy:

### <a name="identity-and-directory-service"></a>Tożsamość i usługa katalogowa

Tożsamości i usługi katalogowe to kluczowe możliwości zarówno lokalnych, jak i w chmurze centrów danych. Tożsamość obejmuje wszystkie aspekty dostępu i autoryzacji do usług w ramach implementacji VDC. Aby mieć pewność, że tylko autoryzowani użytkownicy i procesy uzyskują dostęp do zasobów platformy Azure, platforma Azure korzysta z kilku typów poświadczeń do uwierzytelniania, w tym haseł kont, kluczy kryptograficznych, podpisów cyfrowych i certyfikatów. [Usługa azure Multi-Factor Authentication][multi-factor-authentication] zapewnia dodatkową warstwę zabezpieczeń na potrzeby uzyskiwania dostępu do usług platformy Azure przy użyciu silnego uwierzytelniania z szerokim zakresem opcji łatwej weryfikacji (połączenie telefoniczne, wiadomość SMS lub powiadomienie aplikacji mobilnej), które umożliwiają klientom wybór preferowanej metody.

Każde duże przedsiębiorstwo musi zdefiniować proces zarządzania tożsamościami, który opisuje zarządzanie indywidualnymi tożsamościami, uwierzytelnianiem, autoryzacją, rolami i uprawnieniami w ramach lub w VDC. Celem tego procesu jest zwiększenie bezpieczeństwa i produktywności przy jednoczesnym zmniejszeniu kosztów, przestoju i powtarzalnych zadań ręcznych.

Organizacje korporacyjne mogą wymagać wymagającej kombinacji usług dla różnych branż, a pracownicy często mają różne role w przypadku różnych projektów. VDC wymaga dobrej współpracy między różnymi zespołami, z których każda korzysta z określonych ról, aby uzyskać systemy z dobrymi zasadami zarządzania. Macierz obowiązków, dostępu i praw mogą być złożone. Zarządzanie tożsamościami w VDC jest implementowane za pośrednictwem [Azure Active Directory (Azure AD)][azure-ad] i kontroli dostępu opartej na ROLACH (RBAC).

Usługa katalogowa to udostępniona infrastruktura informacyjna, która umożliwia lokalizowanie i organizowanie codziennych elementów oraz zasobów sieciowych oraz zarządzanie nimi. Te zasoby mogą obejmować woluminy, foldery, pliki, drukarki, użytkowników, grupy, urządzenia i inne obiekty. Każdy zasób w sieci jest traktowany jako obiekt przez serwer katalogowy. Informacje o zasobie są przechowywane jako Kolekcja atrybutów skojarzonych z tym zasobem lub obiektem.

Wszystkie usługi Microsoft Online Business Services są zależne od Azure Active Directory (Azure AD) w celu logowania się i innych potrzeb związanych z tożsamościami. Azure Active Directory to kompleksowe rozwiązanie do zarządzania tożsamościami i dostępem w chmurze o wysokiej dostępności, które łączy podstawowe usługi katalogowe, zaawansowane zarządzanie tożsamościami i zarządzania dostępem do aplikacji. Usługa Azure AD może być zintegrowana z lokalnym Active Directory, aby umożliwić Logowanie jednokrotne dla wszystkich aplikacji lokalnych opartych na chmurze i lokalnie hostowanych. Atrybuty użytkownika lokalnego Active Directory mogą być automatycznie synchronizowane z usługą Azure AD.

Pojedynczy Administrator globalny nie musi przypisywać wszystkich uprawnień w implementacji VDC. Zamiast tego każdy konkretny dział, Grupa użytkowników lub usługi w usłudze katalogowej może mieć uprawnienia wymagane do zarządzania własnymi zasobami w ramach implementacji VDC. Uprawnienia do tworzenia struktury wymagają równoważenia. Zbyt wiele uprawnień może utrudnić wydajność, a zbyt mało lub luźne uprawnienia mogą zwiększyć zagrożenie bezpieczeństwa. Kontrola dostępu oparta na rolach (RBAC) na platformie Azure pomaga rozwiązać ten problem, oferując szczegółowe zarządzanie dostępem do zasobów w implementacji VDC.

### <a name="security-infrastructure"></a>Infrastruktura zabezpieczeń

Infrastruktura zabezpieczeń odnosi się do podziału ruchu w konkretnym segmencie sieci wirtualnej implementacji VDC. Ta infrastruktura określa sposób, w jaki dane przychodzące i wychodzące są kontrolowane w implementacji VDC. Platforma Azure jest oparta na architekturze wielodostępnej, która zapobiega nieautoryzowanemu i niezamierzonyemu ruchowi między wdrożeniami przy użyciu izolacji sieci wirtualnej, list kontroli dostępu, modułów równoważenia obciążenia, filtrów IP i zasad przepływu ruchu. Translator adresów sieciowych (NAT) oddziela ruch sieciowy między ruchem zewnętrznym.

Sieć szkieletowa Azure przydziela zasoby infrastruktury do obciążeń dzierżawców i zarządza komunikacją z maszynami wirtualnymi i z nich. Funkcja hypervisor platformy Azure wymusza separację pamięci i procesów między maszynami wirtualnymi i bezpiecznie kieruje ruch sieciowy do dzierżawców systemu operacyjnego gościa.

### <a name="connectivity-to-the-cloud"></a>Łączność z chmurą

Wirtualne centrum danych wymaga połączenia z sieciami zewnętrznymi w celu oferowania usług klientom, partnerom lub użytkownikom wewnętrznym. Wymaganie łączności dotyczy nie tylko Internetu, ale również do sieci lokalnych i centrów danych.

Klienci kontrolują, które usługi mogą uzyskać dostęp do publicznego Internetu. Ten dostęp jest kontrolowany przy użyciu [zapory platformy Azure][AzFW] lub innych typów urządzeń sieci wirtualnej (urządzeń WUS), niestandardowych zasad routingu za pomocą [tras zdefiniowanych przez użytkownika][UDR]i filtrowania sieci przy użyciu [sieciowych grup zabezpieczeń][NSG]. Firma Microsoft zaleca, aby wszystkie zasoby dostępne z Internetu były chronione także przez [Standard Azure DDoS Protection][DDoS].

Przedsiębiorstwa mogą wymagać połączenia ich wirtualnego centrum danych z lokalnymi centrami danych lub innymi zasobami. Połączenie między platformą Azure i sieciami lokalnymi jest kluczowym aspektem podczas projektowania efektywnej architektury. Przedsiębiorstwa mają dwa różne sposoby tworzenia połączeń: przekazywanie przez Internet lub bezpośrednie połączenia prywatne.

Połączenie sieci [VPN typu lokacja-lokacja na platformie][VPN] Azure łączy sieci lokalne z wirtualnym centrum danych na platformie Azure. Łącze jest nawiązywane za pomocą bezpiecznych szyfrowanych połączeń (tunele IPsec). Połączenia sieci VPN typu lokacja-lokacja są elastyczne, szybko tworzone i zwykle nie wymagają dodatkowego zaopatrzenia w sprzęt. Na podstawie standardowych protokołów branżowych większość bieżących urządzeń sieciowych może tworzyć połączenia sieci VPN z platformą Azure przez Internet lub istniejące ścieżki łączności.

[**ExpressRoute**][ExR] umożliwia prywatne połączenia między wirtualnym centrum danych a sieciami lokalnymi. Połączenia ExpressRoute nie przechodzą przez publiczny Internet i oferują wyższy poziom bezpieczeństwa, niezawodność i wyższą szybkość (do 100 GB/s) oraz spójne opóźnienia. ExpressRoute zawiera zalety reguł zgodności skojarzonych z połączeniami prywatnymi. Za pomocą programu [ExpressRoute Direct][ExRD]można łączyć się bezpośrednio z routerami firmy Microsoft przy 10 GB/s lub 100 GB/s.

Wdrożenie połączeń ExpressRoute zazwyczaj obejmuje zaangażowanie się z dostawcą usług ExpressRoute (ExpressRoute Direct to wyjątek). W przypadku klientów, którzy muszą szybko rozpocząć pracę, często należy używać sieci VPN typu lokacja-lokacja w celu nawiązania połączenia między wirtualnym centrum danych a zasobami lokalnymi. Po zakończeniu fizycznego połączenia z dostawcą usług, Przeprowadź migrację łączności przez połączenie ExpressRoute.

W przypadku dużej liczby połączeń sieci VPN lub ExpressRoute [**Azure Virtual WAN**][virtual-wan] to usługa sieciowa, która zapewnia zoptymalizowaną i zautomatyzowaną łączność między gałęziami za pośrednictwem platformy Azure. Wirtualna sieć WAN pozwala nawiązywać połączenia z platformą Azure i konfigurować je w celu komunikowania się z nią. Łączenie i Konfigurowanie można wykonać ręcznie lub za pomocą preferowanych urządzeń dostawcy za pośrednictwem wirtualnego partnera sieci WAN. Korzystanie z preferowanych urządzeń dostawcy umożliwia łatwe używanie, uproszczenie łączności i zarządzanie konfiguracją. Wbudowany pulpit nawigacyjny platformy Azure zapewnia błyskawiczne Rozwiązywanie problemów, które mogą pomóc zaoszczędzić czas i umożliwia łatwą obsługę łączności między lokacjami w dużej skali. Wirtualna sieć WAN udostępnia również usługi zabezpieczeń z opcjonalną zaporą platformy Azure i menedżerem zapory w wirtualnym koncentratorze sieci WAN.

### <a name="connectivity-within-the-cloud"></a>Łączność w chmurze

[Sieci wirtualne platformy Azure][virtual-network] i [Komunikacja równorzędna sieci wirtualnych][virtual-network-peering] to podstawowe składniki sieciowe w wirtualnym centrum danych. Sieć wirtualna gwarantuje granicę izolacji wirtualnych zasobów centrum danych. Komunikacja równorzędna umożliwia komunikację między różnymi sieciami wirtualnymi w tym samym regionie świadczenia usługi Azure, między regionami, a nawet między sieciami w różnych subskrypcjach. Zarówno wewnątrz, jak i między sieciami wirtualnymi, przepływy ruchu mogą być kontrolowane przez zestawy reguł zabezpieczeń określonych w [grupach zabezpieczeń sieci][NSG], zasady zapory ([Zapora platformy Azure][AzFW] lub [wirtualne urządzenia sieciowe][NVA]) oraz niestandardowe [trasy zdefiniowane przez użytkownika][UDR].

Sieci wirtualne to również punkty zakotwiczenia umożliwiające integrację produktów platformy Azure jako usługi (PaaS), takich jak [Azure Storage][Storage], [Azure SQL][SQL]i inne zintegrowane usługi publiczne z publicznymi punktami końcowymi. Za pomocą [punktów końcowych usługi][ServiceEndpoints] i [linku prywatnego platformy Azure][PrivateLink]możesz zintegrować usługi publiczne z siecią prywatną. Możesz nawet korzystać z prywatnych usług publicznych, ale nadal korzystać z zalet usług PaaS zarządzanych przez platformę Azure.

## <a name="virtual-datacenter-overview"></a>Omówienie wirtualnego centrum danych

### <a name="topologies"></a>Topologie

Wirtualne centrum danych można skompilować przy użyciu jednej z tych topologii wysokiego poziomu na podstawie potrzeb i wymagań dotyczących skalowalności:

W przypadku *płaskiej* topologii wszystkie zasoby są wdrażane w jednej sieci wirtualnej. Podsieci umożliwiają sterowanie przepływem i segregowanie.

![11][11]

W *topologii sieci wirtualne* Komunikacja równorzędna jest bezpośrednio łączona ze wszystkimi sieciami wirtualnymi.

![12][12]

Topologia *komunikacji równorzędnej i szprych* jest odpowiednia dla aplikacji rozproszonych i zespołów z delegowanymi zadaniami.

![13][13]

Topologia *wirtualnej sieci WAN platformy Azure* może obsługiwać scenariusze dużych biur oddziałów i globalne usługi sieci WAN.

![14][14]

Topologia komunikacji równorzędnej i szprychy oraz topologia wirtualnej sieci WAN platformy Azure używają układu gwiazdy, który jest optymalny w przypadku komunikacji, zasobów udostępnionych i scentralizowanych zasad zabezpieczeń. Koncentratory są tworzone przy użyciu koncentratora komunikacji równorzędnej sieci wirtualnej (oznaczonego jako `Hub Virtual Network` na diagramie) lub wirtualnego koncentratora sieci WAN (oznaczonego jako `Azure Virtual WAN` na diagramie). Wirtualna sieć WAN platformy Azure została zaprojektowana w celu zapewnienia dużej ilości gałęzi do rozgałęzienia i rozgałęziania do platformy Azure, a także do unikania kompleksów kompilowania wszystkich składników osobno w koncentratorze komunikacji równorzędnej sieci wirtualnych. W niektórych przypadkach wymagania mogą wymagać projektu koncentratora komunikacji równorzędnej sieci wirtualnej, na przykład potrzeb sieciowych urządzeń wirtualnych w centrum.

W obu topologiach Hub i szprych koncentrator jest centralną strefą sieci, która kontroluje i sprawdza cały ruch między różnymi strefami: Internet, lokalnie i szprych. Topologia gwiazdy pomaga centralnie wymuszać zasady zabezpieczeń. Minimalizuje również ryzyko błędnej konfiguracji i ekspozycji.

Koncentrator często zawiera wspólne składniki usługi używane przez szprychy. Poniżej przedstawiono typowe usługi centralne:

- Infrastruktura Active Directory systemu Windows, wymagana do uwierzytelniania użytkowników innych firm, którzy uzyskują dostęp z niezaufanych sieci przed uzyskaniem dostępu do obciążeń w szprychie. Obejmuje ona powiązane usługi Active Directory Federation Services (AD FS).
- Usługa rozproszonego systemu nazw (DNS) służąca do rozpoznawania nazw obciążeń w szprychach, do uzyskiwania dostępu do zasobów lokalnych i w Internecie, jeśli [Azure DNS][DNS] nie jest używana.
- Infrastruktura kluczy publicznych (PKI) do implementowania obciążeń logowania jednokrotnego.
- Kontrola przepływu ruchu TCP i UDP między strefami sieciowymi szprych i Internetem.
- Sterowanie przepływem między szprychami i środowiskiem lokalnym.
- W razie konieczności sterowanie przepływem między jedną szprychą a inną.

Wirtualne centrum danych zmniejsza całkowity koszt przy użyciu infrastruktury centrum udostępnionej między wieloma szprychami.

Rolą każdej szprychy może być hostowanie różnych typów obciążeń. Szprychy zapewniają również modularne podejście do powtarzających się wdrożeń tych samych obciążeń. Przykłady to programowanie i testowanie, testy akceptacji użytkowników, środowisko przedprodukcyjne i środowisko produkcyjne. Szprychy mogą również dzielić różne grupy w obrębie organizacji i umożliwiać ich tworzenie. Przykładem są grupy DevOps. Wewnątrz szprychy można wdrażać podstawowe obciążenia lub złożone obciążenia wielowarstwowe z kontrolą ruchu między warstwami.

### <a name="subscription-limits-and-multiple-hubs"></a>Ograniczenia subskrypcji i wiele piast

> [!IMPORTANT]
> W zależności od wielkości wdrożeń platformy Azure może być konieczna strategia wielu centrów. Podczas projektowania strategii gwiazdy i gwiazdy "czy ta Skala projektu może korzystać z innej sieci wirtualnej centrum w tym regionie?", także "czy ta Skala projektu może obsługiwać wiele regionów?". Znacznie lepiej jest zaplanować projekt, który skaluje się i nie potrzebuje, niż nie można zaplanować go i potrzebować.
>
> Kiedy skalowanie do pomocniczego (lub więcej) centrum będzie zależeć od czynników wyposażono, zwykle opartych na ograniczeniach w skali. Zapoznaj się z [limitami][limits] subskrypcji, sieci wirtualnych i maszyn wirtualnych podczas projektowania na potrzeby skalowania.

Na platformie Azure każdy składnik, niezależnie od typu, jest wdrażany w ramach subskrypcji platformy Azure. Izolacja składników platformy Azure w różnych subskrypcjach platformy Azure może spełniać różne wymagania biznesowe, takie jak konfigurowanie różnych poziomów dostępu i autoryzacji.

Jedna implementacja VDC może skalować w górę do dużej liczby szprych, chociaż podobnie jak w przypadku każdego systemu IT, istnieją limity platformy. Wdrożenie centrum jest powiązane z określoną subskrypcją platformy Azure, która ma ograniczenia i limity (na przykład maksymalną liczbę wirtualnych sieci równorzędnych. Zobacz [Limity, przydziały i ograniczenia usługi i subskrypcji platformy Azure][limits], aby uzyskać szczegółowe informacje). W przypadkach, gdy mogą to być problemy, architektura można skalować w górę, rozszerzając model z jednego piasty do klastra koncentratora i szprych. Za pomocą komunikacji równorzędnej sieci wirtualnej, ExpressRoute, wirtualnej sieci WAN lub sieci VPN typu lokacja-lokacja można podłączyć wiele centrów w jednym lub większej liczbie regionów świadczenia usługi Azure.

![2][2]

Wprowadzenie wielu centrów zwiększa koszty i nakłady pracy związane z zarządzaniem systemem. Jest to uzasadnione tylko z powodu skalowalności, limitów systemu, nadmiarowości, replikacji regionalnej dla wydajności użytkowników końcowych lub odzyskiwania po awarii. W scenariuszach wymagających wielu centrów wszystkie centra powinny dążyć do zaoferowania tego samego zestawu usług w celu ułatwienia działania.

### <a name="interconnection-between-spokes"></a>Wzajemne połączenia między szprychami

W pojedynczym szprychie lub płaskim projekcie sieci można zaimplementować złożone obciążenia wielowarstwowe. Konfiguracje wielowarstwowe można zaimplementować przy użyciu podsieci, jednej dla każdej warstwy lub aplikacji w tej samej sieci wirtualnej. Sterowanie ruchem i filtrowanie odbywa się przy użyciu sieciowych grup zabezpieczeń i tras zdefiniowanych przez użytkownika.

Architekt może chcieć wdrożyć obciążenie wielowarstwowe w wielu sieciach wirtualnych. Za pomocą komunikacji równorzędnej sieci wirtualnych szprychy mogą łączyć się z innymi szprychami w tym samym koncentratorze lub różnych centrach. Typowym przykładem tego scenariusza jest przypadek, w którym serwery przetwarzania aplikacji znajdują się w jednej szprychie lub w sieci wirtualnej. Baza danych jest wdrażana w innej szprychie lub w sieci wirtualnej. W takim przypadku można łatwo połączyć szprychy z sieciami równorzędnymi, a tym samym, aby uniknąć przesyłania danych przez centrum. Należy zachować ostrożną architekturę i Przegląd zabezpieczeń, aby upewnić się, że pominięcie centrum nie pomija ważnych punktów zabezpieczeń lub inspekcji, które mogą istnieć tylko w centrum.

![3][3]

Szprychy mogą być również połączone ze szprychą, która pełni rolę piasty. Takie podejście tworzy hierarchię dwupoziomową: szprycha na wyższym poziomie (poziom 0) staje się piastą dla małych szprych (poziom 1) w hierarchii. Szprychy implementacji VDC są wymagane do przekazywania ruchu do centralnego koncentratora, dzięki czemu ruch może być przesyłany do miejsca docelowego w sieci lokalnej lub w publicznym Internecie. Architektura z dwoma poziomami koncentratorów zawiera złożone Routing, który usuwa zalety prostej relacji gwiazdy.

Mimo że platforma Azure umożliwia złożone topologie, jedną z podstawowych zasad koncepcji VDC jest powtarzalność i prostota. Aby zminimalizować nakład pracy związany z zarządzaniem, prosta konstrukcja gwiazdy jest architekturą referencyjną VDC, którą zalecamy.

### <a name="components"></a>Składniki

Wirtualne centrum danych składa się z czterech podstawowych typów składników: **infrastruktury**, **sieci obwodowej**, **obciążeń**i **monitorowania**.

Każdy typ składnika składa się z różnych funkcji i zasobów platformy Azure. Implementacja VDC składa się z wystąpień wielu typów składników i wielu odmian tego samego typu składnika. Na przykład może istnieć wiele różnych logicznie oddzielonych wystąpień obciążeń, które reprezentują różne aplikacje. Te różne typy składników i wystąpienia są używane do ostatecznego kompilowania VDC.

![4][4]

Powyższa architektura koncepcyjna wysokiego poziomu VDC pokazuje różne typy składników używane w różnych strefach topologii gwiazdy. Diagram przedstawia składniki infrastruktury w różnych częściach architektury.

Ogólnie rzecz biorąc, prawa dostępu i uprawnienia powinny być oparte na grupach. Zajmowanie się grupami, a nie indywidualnymi użytkownikami, ułatwia konserwację zasad dostępu przez zapewnienie spójnego sposobu zarządzania nim w zespołach i pomaga w minimalizacji błędów konfiguracji. Przypisanie i usunięcie użytkowników do i z odpowiednich grup pomaga w zachowaniu Aktualności uprawnień określonego użytkownika.

Każda grupa ról powinna mieć unikatowy prefiks dla swoich nazw. Ten prefiks ułatwia ustalenie, która grupa jest skojarzona z tym obciążeniem. Na przykład obciążenie obsługujące usługę uwierzytelniania może mieć grupy o nazwach **AuthServiceNetOps**, **AuthServiceSecOps**, **AuthServiceDevOps**i **AuthServiceInfraOps**. Scentralizowane role lub role niepowiązane z konkretną usługą mogą być poprzedzone **firmowymi**. Przykładem jest **CorpNetOps**.

Wiele organizacji używa odmian następujących grup w celu zapewnienia głównych podziałów ról:

- Centralna Grupa IT, **Corp** ma prawa własności do sterowania składnikami infrastruktury. Przykładami są sieci i zabezpieczenia. Grupa musi mieć rolę współautora w ramach subskrypcji, kontroli centrum i uprawnień współautora sieci w szprychach. Duże organizacje często dzielą te obowiązki związane z zarządzaniem między wieloma zespołami. Przykładami jest Grupa **CorpNetOps** operacji sieciowych z wyłącznym koncentracją w sieci i grupami operacji zabezpieczeń **CorpSecOps** , odpowiedzialnych za zaporę i zasady zabezpieczeń. W tym konkretnym przypadku należy utworzyć dwie różne grupy do przypisywania ról niestandardowych.
- Grupa Dev-Test, **AppDevOps,** ma odpowiedzialność za wdrażanie obciążeń aplikacji lub usług. Ta grupa przyjmuje rolę współautora maszyny wirtualnej dla wdrożeń IaaS lub co najmniej jedną rolę współautora PaaS. Zobacz [wbudowane role dla zasobów platformy Azure][Roles]. Opcjonalnie zespół deweloperów i testów może potrzebować widoczności zasad zabezpieczeń (sieciowych grup zabezpieczeń) i zasad routingu (zdefiniowanych przez użytkownika tras) w centrum lub w konkretnym szprychie. Oprócz roli współautora dla obciążeń, ta grupa powinna również mieć rolę czytnika sieci.
- Operacja i Grupa konserwacji, **CorpInfraOps** lub **AppInfraOps,** odpowiada za zarządzanie obciążeniami w środowisku produkcyjnym. Ta grupa musi być współautorem subskrypcji na obciążeniach w dowolnych subskrypcjach produkcyjnych. Niektóre organizacje mogą również oszacować, czy potrzebują dodatkowej grupy zespołu pomocy technicznej z rolą współautor subskrypcji w środowisku produkcyjnym i centralną subskrypcją centrum. Dodatkowa grupa rozwiązuje potencjalne problemy z konfiguracją w środowisku produkcyjnym.

VDC jest zaprojektowana tak, że grupy utworzone dla centralnej grupy IT, zarządzanie centrum, mają odpowiednie grupy na poziomie obciążenia. Poza zarządzaniem tylko zasobami centrum Centralna Grupa IT może kontrolować dostęp zewnętrzny i uprawnienia najwyższego poziomu subskrypcji. Grupy obciążeń mogą również kontrolować zasoby i uprawnienia do ich sieci wirtualnych niezależnie od centralnych.

Wirtualne centrum danych jest podzielone na partycje, aby bezpiecznie hostować wiele projektów w różnych branżach (LOB). Wszystkie projekty wymagają różnych środowisk izolowanych (dev, przeprowadzających i Production). Osobne subskrypcje platformy Azure dla każdego z tych środowisk mogą zapewnić naturalną izolację.

![5][5]

Na powyższym diagramie przedstawiono relację między projektami, użytkownikami i grupami organizacji oraz środowiskami, w których są wdrażane składniki platformy Azure.

Zwykle w tym środowisku (lub warstwie) jest system, w którym wiele aplikacji jest wdrażanych i wykonywanych. Duże przedsiębiorstwa wykorzystują środowisko programistyczne (gdzie zmiany są wprowadzane i testowane) oraz środowisko produkcyjne (które są używane przez użytkowników końcowych). Te środowiska są oddzielane, często z kilkoma środowiskami przejściowymi między nimi, aby umożliwić wdrażanie stopniowe (wdrażanie), testowanie i wycofywanie w przypadku wystąpienia problemów. Architektury wdrażania różnią się znacznie, ale zazwyczaj jest to podstawowy proces rozpoczynający się od projektowania (DEV) i kończący się w środowisku produkcyjnym.

Wspólna architektura dla tych typów środowisk wielowarstwowych składa się z DevOps na potrzeby projektowania i testowania, przeprowadzających dla środowisk przejściowych i produkcyjnych. Organizacje mogą używać jednego lub wielu dzierżawców usługi Azure AD do definiowania dostępu i praw do tych środowisk. Poprzedni diagram przedstawia przypadek, w którym są używane dwa różne dzierżawy usługi Azure AD: jeden dla DevOps i przeprowadzających, a drugi wyłącznie dla środowiska produkcyjnego.

Obecność różnych dzierżawców usługi Azure AD wymusza rozdzielenie między środowiskami. Ta sama Grupa użytkowników, taka jak Centralna, musi być uwierzytelniana przy użyciu innego identyfikatora URI w celu uzyskania dostępu do innej dzierżawy usługi Azure AD w celu zmodyfikowania ról lub uprawnień do środowisk DevOps lub produkcyjnych projektu. Obecność różnych uwierzytelnień użytkowników w celu uzyskania dostępu do różnych środowisk zmniejsza potencjalne przerwy i inne problemy spowodowane błędami ludzkimi.

#### <a name="component-type-infrastructure"></a>Typ składnika: infrastruktura

Ten typ składnika to miejsce, w którym znajduje się większość infrastruktury pomocniczej. Jest to również miejsce, w którym scentralizowane zespoły IT, bezpieczeństwa i zgodności spędzają najwięcej czasu.

![6][6]

Składniki infrastruktury zapewniają połączenie z różnymi składnikami implementacji VDC oraz znajdują się zarówno w centrum, jak i szprych. Odpowiedzialność za zarządzanie i utrzymywanie składników infrastruktury jest zwykle przypisana do centralnych zespołów IT i/lub zabezpieczeń.

Jednym z podstawowych zadań zespołu infrastruktury IT jest zagwarantowanie spójności schematów adresów IP w całym przedsiębiorstwie. Prywatna przestrzeń adresów IP przypisana do implementacji VDC musi być spójna i nie pokrywa się z prywatnymi adresami IP przypisanymi do sieci lokalnych.

Podczas gdy translator adresów sieciowych na lokalnych routerach granicznych lub w środowiskach platformy Azure może uniknąć konfliktów adresów IP, dodaje komplikacje do składników infrastruktury. Prostota zarządzania to jeden z najważniejszych celów VDC, więc użycie translatora adresów sieciowych do obsługi zagadnień związanych z adresami IP, podczas gdy prawidłowe rozwiązanie nie jest zalecanym rozwiązaniem.

Składniki infrastruktury mają następujące funkcje:

- [**Tożsamości i usługi katalogowe**][azure-ad]. Dostęp do każdego typu zasobu na platformie Azure jest kontrolowany przez tożsamość przechowywaną w usłudze katalogowej. Usługa katalogowa przechowuje nie tylko listę użytkowników, ale również prawa dostępu do zasobów w określonej subskrypcji platformy Azure. Te usługi mogą istnieć tylko w chmurze lub mogą być synchronizowane z tożsamością lokalną przechowywaną w Active Directory.
- [**Virtual Network**][virtual-network]. Sieci wirtualne są jednym z głównych składników VDC i umożliwiają utworzenie granicy izolacji ruchu na platformie Azure. Sieć wirtualna składa się z jednego lub wielu segmentów sieci wirtualnej, z których każdy ma określony prefiks sieci IP (podsieć, IPv4 lub dwubajtowy protokół IPv4/IPv6). Sieć wirtualna definiuje wewnętrzny obszar obwodu, w którym IaaS maszyny wirtualne i usługi PaaS mogą nawiązywać prywatną komunikację. Maszyny wirtualne (i usługi PaaS Services) w jednej sieci wirtualnej nie mogą komunikować się bezpośrednio z maszynami wirtualnymi (i usługami PaaS) w innej sieci wirtualnej, nawet jeśli obie sieci wirtualne są tworzone przez tego samego klienta w ramach tej samej subskrypcji. Izolacja jest właściwością krytyczną, która zapewnia, że maszyny wirtualne klienta i komunikacja pozostają prywatne w ramach sieci wirtualnej. W przypadku pożądanej łączności między sieciami poniższe funkcje opisują, jak można to osiągnąć.
- [**Komunikacja równorzędna sieci wirtualnej**][virtual-network-peering]. Podstawową funkcją służącą do tworzenia infrastruktury VDC jest Komunikacja równorzędna sieci wirtualnych, która łączy dwie sieci wirtualne w tym samym regionie, za pośrednictwem sieci centrum danych platformy Azure lub w całym regionie platformy Azure na całym świecie.
- [**Virtual Network punkty końcowe usługi**][ServiceEndpoints]. Punkty końcowe usługi zwiększają prywatną przestrzeń adresową sieci wirtualnej, aby uwzględnić miejsce PaaS. Punkty końcowe również zwiększają tożsamość sieci wirtualnej do usług platformy Azure za pośrednictwem bezpośredniego połączenia. Punkty końcowe umożliwiają zabezpieczanie krytycznych zasobów usługi platformy Azure tylko do sieci wirtualnych.
- [**Link prywatny**][PrivateLink]. Link prywatny platformy Azure umożliwia dostęp do usług Azure PaaS Services (na przykład [Azure Storage][Storage], [Azure Cosmos DB][Cosmos]i [Azure SQL Database][SQL]) oraz hostowanych usług klienta i partnerskich platformy Azure za pośrednictwem prywatnego punktu końcowego w sieci wirtualnej. Ruch między siecią wirtualną a usługą odbywa się za pośrednictwem sieci szkieletowej firmy Microsoft, eliminując ekspozycję z publicznego Internetu. Możesz również utworzyć własną [prywatną usługę linku][PrivateLinkSvc] w sieci wirtualnej i dostarczyć ją prywatnie do klientów. Środowisko instalacji i użycia korzystające z prywatnego linku platformy Azure jest spójne w przypadku usługi Azure PaaS, należącej do klienta i udostępnionych usług partnerskich.
- [**Trasy zdefiniowane przez użytkownika**][UDR]. Ruch w sieci wirtualnej jest domyślnie kierowany na podstawie tabeli routingu systemowego. Zdefiniowana przez użytkownika trasa jest niestandardową tabelą routingu, którą Administratorzy sieci mogą skojarzyć z co najmniej jedną podsiecią, aby zastąpić zachowanie tabeli routingu systemu i zdefiniować ścieżkę komunikacji w ramach sieci wirtualnej. Obecność tras zdefiniowanych przez użytkownika gwarantuje, że ruch wychodzący z tranzytu szprych przez określone niestandardowe maszyny wirtualne lub wirtualne urządzenia sieciowe i moduły równoważenia obciążenia obecne zarówno w centrum, jak i szprych.
- [**Sieciowe grupy zabezpieczeń**][NSG]. Grupa zabezpieczeń sieci to lista reguł zabezpieczeń, które działają jako Filtrowanie ruchu dla źródeł IP, miejsc docelowych adresów IP, protokołów, portów źródłowych IP i portów docelowych IP (nazywanego również krotką warstwy 4 5). Sieciową grupę zabezpieczeń można zastosować do podsieci, wirtualnej karty sieciowej skojarzonej z maszyną wirtualną platformy Azure lub obu tych usług. Sieciowe grupy zabezpieczeń są niezbędne do wdrożenia prawidłowej kontroli przepływu w centrum i szprych. Poziom zabezpieczeń zapewniany przez grupę zabezpieczeń sieci to funkcja, z której otwierane są porty i w jakim celu. Klienci powinni stosować dodatkowe filtry na maszynę wirtualną z użyciem zapór opartych na hoście, takich jak dołączenie iptables lub Zapora systemu Windows.
- [**System DNS**][DNS]. System DNS zapewnia rozpoznawanie nazw zasobów w wirtualnym centrum danych. Platforma Azure udostępnia usługi DNS do rozpoznawania nazw [publicznych][DNS] i [prywatnych][PrivateDNS] . Strefy prywatne zapewniają rozpoznawanie nazw zarówno w sieci wirtualnej, jak i w sieciach wirtualnych. Strefy prywatne mogą nie tylko obejmować sieci wirtualne w tym samym regionie, ale również między regionami i subskrypcjami. Do publicznej rozdzielczości Azure DNS zapewnia usługi hostingu dla domen DNS, zapewniając rozpoznawanie nazw przy użyciu infrastruktury Microsoft Azure. Dzięki hostowaniu swoich domen na platformie Azure możesz zarządzać rekordami DNS z zastosowaniem tych samych poświadczeń, interfejsów API, narzędzi i rozliczeń co w przypadku innych usług platformy Azure.
- Zarządzanie [**grupami**][MgmtGrp], [**subskrypcjami**][subscription-management]i [**grupami zasobów**][RGMgmt] . Subskrypcja definiuje naturalną granicę, aby utworzyć wiele grup zasobów na platformie Azure. Ta separacja może dotyczyć funkcji, podziału ról lub rozliczeń. Zasoby w ramach subskrypcji są łączone razem z kontenerami logicznymi znanymi jako grupy zasobów. Grupa zasobów reprezentuje grupę logiczną, aby zorganizować zasoby w wirtualnym centrum danych. Jeśli Twoja organizacja ma wiele subskrypcji, możesz potrzebować sposobu na wydajne zarządzanie dostępem, zasadami i zgodnością dla tych subskrypcji. Grupy zarządzania platformy Azure zapewniają poziom zakresu powyżej subskrypcji. Subskrypcje są organizowane w kontenerach znanych jako grupy zarządzania i stosują swoje warunki ładu do grup zarządzania. Wszystkie subskrypcje w grupie zarządzania automatycznie dziedziczą warunki zastosowane do tej grupy zarządzania. Aby wyświetlić te trzy funkcje w widoku hierarchii, zobacz [organizowanie zasobów][Organize] w strukturze wdrażania w chmurze.
- [**Kontrola dostępu oparta na rolach (RBAC)**][RBAC]. RBAC może mapować role organizacyjne i prawa dostępu do określonych zasobów platformy Azure, co pozwala ograniczyć użytkowników tylko do określonego podzestawu akcji. W przypadku synchronizowania Azure Active Directory z lokalnym Active Directory można używać tych samych grup Active Directory na platformie Azure, które są używane lokalnie. Za pomocą RBAC można udzielić dostępu, przypisując odpowiednią rolę użytkownikom, grupom i aplikacjom w odpowiednim zakresie. Zakres przypisania roli może być subskrypcją platformy Azure, grupą zasobów lub pojedynczym zasobem. RBAC umożliwia dziedziczenie uprawnień. Rola przypisana w zakresie nadrzędnym również przyznaje dostęp do elementów podrzędnych zawartych w nim. Za pomocą RBAC można oddzielić cła i przyznać dostęp tylko do użytkowników, których potrzebują do wykonywania swoich zadań. Na przykład jeden pracownik może zarządzać maszynami wirtualnymi w ramach subskrypcji, podczas gdy inna może zarządzać bazami danych SQL Server w tej samej subskrypcji.

#### <a name="component-type-perimeter-networks"></a>Typ składnika: sieci obwodowe

Składniki sieci obwodowej (nazywane czasem siecią DMZ) łączą lokalne lub fizyczne sieci centrów danych oraz łączność z Internetem. Obwód zazwyczaj wymaga znaczących inwestycji w sieć i zespoły ds. zabezpieczeń.

Pakiety przychodzące powinny przechodzić przez urządzenia zabezpieczające w centrum przed osiągnięciem serwerów zaplecza i usług w szprychach. Przykłady to zapora, identyfikatory i adresy IP. Zanim opuszczą sieć, pakiety powiązane z Internetem z obciążeń powinny również przepływać przez urządzenia zabezpieczeń w sieci obwodowej. Ten przepływ umożliwia wymuszanie zasad, inspekcję i inspekcję.

Składniki sieci obwodowej obejmują:

- [Sieci wirtualne][virtual-network], [trasy definiowane przez użytkownika][UDR] oraz [sieciowe grupy zabezpieczeń][NSG]
- [Wirtualne urządzenia sieciowe][NVA]
- [Azure Load Balancer][ALB]
- [Application Gateway platformy Azure][AppGW] z [zaporą aplikacji sieci Web (WAF)][AppGWWAF]
- [Publiczne adresy IP][PIP]
- [Drzwi frontonu platformy Azure][azure-front-door] z [zaporą aplikacji sieci Web (WAF)][AFDWAF]
- [Zapora platformy Azure][AzFW] i [Menedżer zapory platformy Azure][AzFWMgr]
- [Standardowa DDoS Protection][DDoS]

Zazwyczaj centralne zespoły IT i zabezpieczeń odpowiadają za definicje wymagań i eksploatację sieci obwodowej.

![7][7]

Na powyższym diagramie przedstawiono wymuszanie dwóch obwodów z dostępem do Internetu i sieci lokalnej, które znajdują się w centrum DMZ. W centrum DMZ sieć obwodowa z Internetem może być skalowalna w górę w celu zapewnienia obsługi wielu linii gospodarczych przy użyciu wielu Farm zapór aplikacji sieci Web (sieciowi) lub zapór platformy Azure. Koncentrator umożliwia również lokalne połączenie za pośrednictwem sieci VPN lub ExpressRoute.

> [!NOTE]
> Na powyższym diagramie, w "centrum DMZ", wiele następujących funkcji można powiązać ze sobą w wirtualnym Centrum sieci WAN platformy Azure (na przykład w przypadku sieci wirtualnych, tras zdefiniowanych przez użytkownika, sieciowych grup zabezpieczeń, bram sieci VPN, bram ExpressRoute, modułów równoważenia obciążenia platformy Azure, zapory platformy Azure, Menedżera zapory i DDOS). Przy użyciu wirtualnych centrów sieci Azure można utworzyć centralną sieć wirtualną, a tym samym VDC, znacznie łatwiej, ponieważ większość złożoności inżynieryjnej jest obsługiwana przez platformę Azure podczas wdrażania wirtualnego centrum sieci WAN platformy Azure.

[**Sieci wirtualne**][virtual-network]. Koncentrator jest zazwyczaj zbudowany w sieci wirtualnej z wieloma podsieciami, aby hostować różne typy usług, które filtrują i sprawdzają ruch do lub z Internetu za pośrednictwem zapory platformy Azure, urządzeń WUS, WAF i Azure Application Gateway wystąpienia.

[**Trasy zdefiniowane przez użytkownika**][UDR] Korzystając z tras zdefiniowanych przez użytkownika, klienci mogą wdrażać zapory, identyfikatory/adresy IP i inne urządzenia wirtualne oraz kierować ruchem sieciowym za pośrednictwem tych urządzeń zabezpieczeń w celu wymuszania, inspekcji i inspekcji zasad granicy zabezpieczeń. Trasy zdefiniowane przez użytkownika mogą być tworzone zarówno w centrum, jak i szprychy w celu zagwarantowania, że ruch przesyłany przez określone niestandardowe maszyny wirtualne, wirtualne urządzenia sieciowe i moduły równoważenia obciążenia używane przez implementację VDC. W celu zagwarantowania, że ruch wygenerowany z maszyn wirtualnych znajdujących się w tranzycie szprych do właściwych urządzeń wirtualnych, w podsieciach satelity należy ustawić trasę zdefiniowaną przez użytkownika, ustawiając adres IP frontonu wewnętrznego modułu równoważenia obciążenia jako następny przeskok. Wewnętrzny moduł równoważenia obciążenia rozkłada ruch wewnętrzny na urządzenia wirtualne (pula wewnętrznej bazy danych modułu równoważenia obciążenia).

[**Zapora systemu Azure**][AzFW] to zarządzana usługa zabezpieczeń sieci chroniąca zasoby Virtual Network platformy Azure. Jest to zarządzana przez stanowa Zapora, która zapewnia wysoką dostępność i skalowalność chmury. Możesz centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych. Usługa Azure Firewall używa statycznego publicznego adresu IP do zasobów sieci wirtualnej. Umożliwia to zewnętrznym zaporom identyfikowanie ruchu pochodzącego z danej sieci wirtualnej. Usługa jest w pełni zintegrowana z usługą Azure Monitor na potrzeby rejestrowania i analiz.

Jeśli używasz topologii wirtualnej sieci WAN platformy Azure, [**Menedżer zapory platformy Azure**][AzFWMgr] to usługa zarządzania zabezpieczeniami, która zapewnia centralne zasady zabezpieczeń i Zarządzanie trasami dla obwodów zabezpieczeń opartych na chmurze. Współpracuje z Centrum sieci wirtualnej platformy Azure, zasobem zarządzanym przez firmę Microsoft, który umożliwia łatwe tworzenie architektur Hub i szprych. Gdy zasady zabezpieczeń i routingu są skojarzone z tym centrum, jest ono nazywane bezpiecznym koncentratorem wirtualnym.

[**Wirtualne urządzenia sieciowe**][NVA]. W centrum sieć obwodowa mająca dostęp do Internetu jest zazwyczaj zarządzana za pomocą wystąpienia zapory platformy Azure lub farmy zapory lub zapory aplikacji sieci Web (WAF).

Różne branże biznesowe często korzystają z wielu aplikacji sieci Web, które mają wpływ na różne luki w zabezpieczeniach i potencjalną lukę w zabezpieczeniach. Zapory aplikacji sieci Web to specjalny typ produktu służący do wykrywania ataków na aplikacje sieci Web, protokół HTTP/HTTPS, bardziej szczegółowo niż w przypadku zapory ogólnej. W porównaniu z tradycją technologii zapory sieciowi mają zestaw określonych funkcji do ochrony wewnętrznych serwerów sieci Web przed zagrożeniami.

Zapora platformy Azure lub Zapora urządzenie WUS korzystają ze wspólnej płaszczyzny administracyjnej z zestawem reguł zabezpieczeń, aby chronić obciążenia hostowane w szprychach i kontrolować dostęp do sieci lokalnych. Zapora platformy Azure ma wbudowaną skalowalność, podczas gdy zapory urządzenie WUS można ręcznie skalować za modułem równoważenia obciążenia. Ogólnie rzecz biorąc, Farma zapory ma mniej wyspecjalizowane oprogramowanie w porównaniu z WAF, ale ma szerszy zakres aplikacji do filtrowania i kontrolowania dowolnego typu ruchu wyjściowego i przychodzącego. Jeśli jest używane podejście urządzenie WUS, można je znaleźć i wdrożyć z portalu Azure Marketplace.

Zalecamy użycie jednego zestawu wystąpień zapory platformy Azure lub urządzeń WUS dla ruchu pochodzącego z Internetu. Użyj innego dla ruchu pochodzącego z lokalnego. Używanie tylko jednego zestawu zapór w obu przypadkach stanowi zagrożenie bezpieczeństwa, ponieważ nie zapewnia on obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego. Użycie osobnych warstw zapory zmniejsza złożoność sprawdzania reguł zabezpieczeń i pozwala wyczyścić, które reguły odnoszą się do tych, które są przychodzące żądania sieciowe.

[**Azure Load Balancer**][ALB] oferuje usługę warstwy 4 (TCP/UDP) o wysokiej dostępności, która może dystrybuować ruch przychodzący między wystąpieniami usługi zdefiniowanymi w zestawie o zrównoważonym obciążeniu. Ruch wysyłany do modułu równoważenia obciążenia z punktów końcowych frontonu IP lub prywatnych punktów końcowych IP może być rozpowszechniany z lub bez translacji adresów do zestawu puli adresów IP zaplecza (takich jak wirtualne urządzenia sieciowe lub maszyny wirtualne).

Azure Load Balancer może również sondować kondycję różnych wystąpień serwera, a gdy wystąpienie nie odpowiada na sondę, moduł równoważenia obciążenia zatrzymuje wysyłanie ruchu do wystąpienia złej kondycji. W wirtualnym centrum danych zewnętrzny moduł równoważenia obciążenia jest wdrażany w centrum i szprych. Moduł równoważenia obciążenia jest używany do wydajnego kierowania ruchu między wystąpieniami zapory, a w szprychach usługi równoważenia obciążenia są używane do zarządzania ruchem aplikacji.

[**Azure Front drzwiczks**][azure-front-door] (AFD) to wysoce dostępna i skalowalna platforma Microsoft Web Application Acceleration platform, globalne Load Balancer http, ochrona aplikacji i Content Delivery Network. W przypadku ponad 100 lokalizacji na granicy sieci globalnej firmy Microsoft AFD umożliwia tworzenie, obsługiwanie i skalowanie dynamicznej aplikacji sieci Web oraz zawartości statycznej. Usługa AFD udostępnia swoją aplikację dzięki światowej klasy wydajności użytkowników końcowych, ujednoliconej automatyzacji konserwacji/sygnatury konserwacyjnej, automatyzacji BCDR, ujednoliconej informacji o kliencie/użytkowniku, buforowaniu i usłudze Service Insights. Platforma oferuje następujące funkcje:
    - Umowy dotyczące poziomu usług (umowy SLA) dotyczące wydajności, niezawodności i obsługi
    - Certyfikaty zgodności
    - Poddawane inspekcji praktyki zabezpieczeń, które są opracowywane, eksploatowane i natywnie obsługiwane przez platformę Azure.
Drzwi frontonu platformy Azure udostępniają również zaporę aplikacji sieci Web (WAF), która chroni aplikacje sieci Web przed typowymi lukami w zabezpieczeniach i atakami.

[**Usługa Azure Application Gateway**][AppGW] to dedykowane urządzenie wirtualne udostępniające zarządzany kontroler dostarczania aplikacji (ADC). Oferuje różne możliwości równoważenia obciążenia warstwy 7 dla aplikacji. Pozwala zoptymalizować wydajność kolektywu serwerów sieci Web przez odciążenie przerwania protokołu SSL intensywnie korzystających z procesora CPU do bramy aplikacji. Zapewnia także inne możliwości routingu warstwy 7, takie jak dystrybucja okrężna ruchu przychodzącego, koligacja sesji na podstawie plików cookie, routing oparty na ścieżkach URL i możliwość hostowania wielu witryn sieci Web za pojedynczą bramą aplikacji. Zapora aplikacji internetowych jest również udostępniana w ramach jednostki SKU zapory aplikacji internetowych w usłudze Application Gateway. Zapewnia ona ochronę aplikacji internetowych przed typowymi internetowymi lukami w zabezpieczeniach. Usługę Application Gateway można skonfigurować jako bramę umożliwiającą dostęp do Internetu, bramę tylko wewnętrzną lub jako kombinację obu tych opcji.

[**Publiczne adresy IP**][PIP]. Niektóre funkcje platformy Azure umożliwiają kojarzenie punktów końcowych usługi z publicznym adresem IP, dzięki czemu zasób jest dostępny z Internetu. Ten punkt końcowy używa translatora adresów sieciowych do kierowania ruchu do wewnętrznego adresu i portu w sieci wirtualnej platformy Azure. Ta ścieżka stanowi podstawową metodę przekazywania ruchu zewnętrznego do sieci wirtualnej. Można skonfigurować publiczne adresy IP, aby określić, który ruch jest przesyłany i jak i w jaki sposób i gdzie jest tłumaczony do sieci wirtualnej.

Usługa [**Azure DDoS Protection Standard**][DDoS] zapewnia dodatkowe możliwości ograniczania funkcjonalności w ramach [podstawowej warstwy usług][DDoS] , która jest dostrajana specjalnie do zasobów usługi Azure Virtual Network. Usługa DDoS Protection w warstwie Standardowa jest prosta do włączenia i nie wymaga żadnych zmian w aplikacji. Zasady ochrony są dostosowywane za pośrednictwem dedykowanych algorytmów monitorowania ruchu i uczenia maszynowego. Zasady są stosowane do publicznych adresów IP skojarzonych z zasobami wdrożonymi w sieciach wirtualnych. Do tych zasobów należą m.in. wystąpienia usług Azure Load Balancer, Azure Application Gateway i Azure Service Fabric. Dzienniki generowane przez system w czasie niemal rzeczywistym są dostępne za pośrednictwem Azure Monitor widoków podczas ataku i historii. Ochronę warstwy aplikacji można dodać za pomocą zapory aplikacji sieci Web platformy Azure Application Gateway. Zapewniona jest ochrona dla publicznych adresów IP platformy Azure IPv4 i IPv6.

Topologia gwiazdy używa komunikacji równorzędnej sieci wirtualnej i tras zdefiniowanych przez użytkownika do prawidłowego kierowania ruchu.

![0,8][8]

Na diagramie zdefiniowana przez użytkownika trasa zapewnia, że ruch z satelity do zapory przed przekazaniem go do lokalizacji lokalnej za pośrednictwem bramy ExpressRoute (Jeśli zasady zapory umożliwiają ten przepływ).

#### <a name="component-type-monitoringmonitoroverview"></a>Typ składnika: [monitorowanie][MonitorOverview]

Składniki monitorowania zapewniają widoczność i alerty ze wszystkich typów składników. Wszystkie zespoły powinny mieć dostęp do monitorowania dla składników i usług, do których mają dostęp. Jeśli masz scentralizowaną pomoc techniczną lub zespoły operacyjne, wymagają zintegrowanego dostępu do danych dostarczanych przez te składniki.

Platforma Azure oferuje różne typy usług rejestrowania i monitorowania, które umożliwiają śledzenie zachowania zasobów hostowanych na platformie Azure. Zarządzanie i kontrola obciążeń na platformie Azure opiera się nie tylko na zbieraniu danych dzienników, ale również o możliwości wyzwalania akcji na podstawie określonych zgłoszonych zdarzeń.

[**Azure monitor**][AzureMonitor]. Platforma Azure obejmuje wiele usług, które indywidualnie wykonują określoną rolę lub zadanie w obszarze monitorowania. Razem te usługi zapewniają kompleksowe rozwiązanie do zbierania, analizowania i działania dzienników generowanych przez system z aplikacji i zasobów platformy Azure, które je obsługują. Mogą one również służyć do monitorowania krytycznych zasobów lokalnych, aby zapewnić hybrydowe środowisko monitorowania. Zrozumienie dostępnych narzędzi i danych to pierwszy krok w opracowaniu kompletnej strategii monitorowania dla aplikacji.

Istnieją dwa podstawowe typy dzienników w Azure Monitor:

- [Metryki][Metrics] to wartości liczbowe, które opisują część systemu w konkretnym momencie. Są one lekkie i mogą obsługiwać niemal scenariusze w czasie rzeczywistym. W przypadku wielu zasobów platformy Azure zobaczysz dane zebrane przez Azure Monitor bezpośrednio na stronie Przegląd w Azure Portal. Na przykład poszukaj dowolnej maszyny wirtualnej i zobaczysz kilka wykresów, które wyświetlają metryki wydajności. Wybierz dowolne wykresy, aby otworzyć dane w Eksploratorze metryk w Azure Portal, co pozwala na wykres wartości wielu metryk w czasie. Możesz wyświetlić wykresy interaktywnie lub przypiąć je do pulpitu nawigacyjnego, aby wyświetlić inne wizualizacje.

- [Dzienniki][Logs] zawierają różne rodzaje danych zorganizowanych w rekordy z różnymi zestawami właściwości dla każdego typu. Zdarzenia i ślady są przechowywane jako dzienniki wraz z danymi dotyczącymi wydajności, które można łączyć w celu analizy. Dane dziennika zbierane przez Azure Monitor mogą być analizowane za pomocą zapytań, aby szybko pobierać, konsolidować i analizować zebrane dane. Dzienniki są przechowywane i wysyłane z [log Analytics][LogAnalytics]. Możesz tworzyć i testować zapytania przy użyciu Log Analytics w Azure Portal, a następnie bezpośrednio analizować dane przy użyciu tych narzędzi lub zapisywać zapytania do użycia z wizualizacjami lub regułami alertów.

![9][9]

Usługa Azure Monitor może zbierać dane z różnych źródeł. Dane monitorowania aplikacji można traktować w warstwach od aplikacji, dowolnego systemu operacyjnego i usług, na których bazują na platformie Azure. Usługa Azure Monitor zbiera dane z każdej z następujących warstw:

- **Dane monitorowania aplikacji:** Dane dotyczące wydajności i funkcjonalności kodu, który zapisano, niezależnie od jego platformy.
- Dane monitorowania systemu operacyjnego gościa: dane dotyczące systemu operacyjnego, w którym działa aplikacja. Ten system operacyjny może działać na platformie Azure, w innej chmurze lub lokalnie.
- **Dane monitorowania zasobów platformy Azure:** Dane dotyczące operacji zasobu platformy Azure.
- **Dane monitorowania subskrypcji platformy Azure:** Dane dotyczące operacji i zarządzania subskrypcją platformy Azure, a także dane dotyczące kondycji i działania samej platformy Azure.
- **Dane monitorowania dzierżawy platformy Azure:** Dane dotyczące działania usług platformy Azure na poziomie dzierżawy, takie jak Azure Active Directory.
- **Źródła niestandardowe:** Można również dołączać dzienniki wysyłane z źródeł lokalnych. Przykładami mogą być lokalne zdarzenia serwera lub dane wyjściowe dziennika systemowego urządzenia sieciowego.

Dane monitorowania są przydatne tylko wtedy, gdy mogą zwiększyć widoczność do działania środowiska obliczeniowego. Azure Monitor obejmuje kilka funkcji i narzędzi, które zapewniają cenne informacje dotyczące aplikacji i innych zasobów, od których zależą. Monitorowanie rozwiązań i funkcji, takich jak Application Insights i Azure Monitor dla kontenerów, zapewnia szczegółowe informacje o różnych aspektach aplikacji i określonych usługach platformy Azure.

Rozwiązania do monitorowania w Azure Monitor są spakowanymi zestawami logiki, które zapewniają wgląd w konkretną aplikację lub usługę. Obejmują one logikę zbierania danych monitorowania dla aplikacji lub usługi, zapytania do analizy tych danych i widoki do wizualizacji. Rozwiązania do monitorowania są dostępne od firmy Microsoft i partnerów w celu zapewnienia monitorowania różnych usług platformy Azure i innych aplikacji.

Wszystkie zebrane bogate dane są ważne do podjęcia aktywnej akcji na zdarzeniach w danym środowisku, w których ręczne zapytania same nie wystarczą. Alerty w usłudze Azure Monitor aktywnie powiadamiać użytkownika o warunkach krytycznych i potencjalnie podejmować działania naprawcze. Reguły alertów w oparciu o metryki zapewniają generowanie alertów niemal w czasie rzeczywistym na podstawie wartości liczbowych, natomiast reguły oparte na dziennikach umożliwiają użycie złożonej logiki w danych z wielu źródeł. Reguły alertów w Azure Monitor używają grup akcji, które zawierają unikatowe zestawy odbiorców i akcje, które mogą być współużytkowane przez wiele reguł. W zależności od wymagań grupy akcji mogą wykonywać takie działania jak korzystanie z elementów webhook, które powodują uruchamianie alertów zewnętrznych lub integrację z narzędziami narzędzia ITSM.

Azure Monitor również umożliwia tworzenie niestandardowych pulpitów nawigacyjnych. Pulpity nawigacyjne platformy Azure umożliwiają łączenie różnych rodzajów danych, w tym metryk i dzienników, w jednym okienku w Azure Portal. Opcjonalnie możesz udostępnić pulpit nawigacyjny innym użytkownikom platformy Azure. Elementy w Azure Monitor można dodać do pulpitu nawigacyjnego platformy Azure oprócz danych wyjściowych zapytania dziennika lub wykresu metryk. Można na przykład utworzyć pulpit nawigacyjny, który łączy kafelki przedstawiające wykres metryk, tabelę dzienników aktywności, wykres użycia Application Insights i dane wyjściowe zapytania dziennika.

Na koniec Azure Monitor dane są źródłem natywnym Power BI. Power BI to usługa analizy biznesowej, która zapewnia interaktywne wizualizacje w różnych źródłach danych i jest skutecznym sposobem udostępniania danych innym osobom w organizacji i poza nią. Power BI można skonfigurować do automatycznego importowania danych dziennika z Azure Monitor, aby skorzystać z tych dodatkowych wizualizacji.

[Usługa Azure Network Watcher][NetWatch] udostępnia narzędzia do monitorowania, diagnozowania i wyświetlania metryk oraz włączania i wyłączania dzienników dla zasobów w sieci wirtualnej platformy Azure. Jest to usługa wieloaspektowe, która umożliwia korzystanie z następujących funkcji i nie tylko:

- Monitoruj komunikację między maszyną wirtualną a punktem końcowym.
- Wyświetl zasoby w sieci wirtualnej i ich relacje.
- Diagnozuj problemy z filtrowaniem ruchu sieciowego do lub z maszyny wirtualnej.
- Diagnozuj problemy z routingiem sieciowym z maszyny wirtualnej.
- Diagnozuj połączenia wychodzące z maszyny wirtualnej.
- Przechwyć pakiety do i z maszyny wirtualnej.
- Diagnozuj problemy z bramą sieci wirtualnej platformy Azure i połączeniami.
- Określanie względnych opóźnień między regionami platformy Azure i dostawcami usług internetowych.
- Wyświetlanie reguł zabezpieczeń dla interfejsu sieciowego.
- Wyświetl metryki sieci.
- Analizuj ruch do lub z sieciowej grupy zabezpieczeń.
- Wyświetlanie dzienników diagnostycznych dla zasobów sieciowych.

#### <a name="component-type-workloads"></a>Typ składnika: obciążenia

Składniki obciążenia to miejsce, w którym znajdują się rzeczywiste aplikacje i usługi. Jest to miejsce, w którym zespoły deweloperów aplikacji spędzają najwięcej czasu.

Możliwości obciążeń są nieograniczone. Poniżej przedstawiono zaledwie kilka możliwych typów obciążeń:

**Aplikacje wewnętrzne:** Aplikacje biznesowe mają kluczowe znaczenie dla operacji w przedsiębiorstwie. Te aplikacje mają kilka typowych cech:

- **Interaktywny:** Wprowadzono dane i są zwracane wyniki lub raporty.
- **Oparte na danych:** Intensywna dostęp do baz danych lub innych magazynów.
- **Zintegrowane:** Oferuj integrację z innymi systemami w organizacji lub poza nią.

**Witryny sieci Web dostępne dla klientów (dostępne w Internecie lub wewnętrznie):** Większość aplikacji internetowych to witryny sieci Web. Na platformie Azure można uruchomić witrynę sieci Web za pośrednictwem maszyny wirtualnej IaaS lub witryny [Azure Web Apps][WebApps] site (PaaS). Usługa Azure Web Apps integruje się z sieciami wirtualnymi w celu wdrażania aplikacji sieci Web w strefie sieci szprych. Udostępnione wewnętrznie witryny sieci Web nie muszą ujawniać publicznego internetowego punktu końcowego, ponieważ zasoby są dostępne za pośrednictwem prywatnych adresów IP, które nie są trasowane z prywatnej sieci wirtualnej.

**Analiza danych Big Data:** Gdy dane wymagają skalowania do dużych woluminów, relacyjne bazy danych mogą nie działać prawidłowo w przypadku skrajnego obciążenia lub bez struktury danych. [Azure HDInsight][HDInsight] to zarządzana usługa analizy typu open source w chmurze dla przedsiębiorstw. Można używać platform typu open source, takich jak Hadoop, Apache Spark, Apache Hive, LLAP, Apache Kafka, Apache Storm i R. Usługa HDInsight obsługuje wdrażanie w sieci wirtualnej opartej na lokalizacji, można wdrożyć w klastrze w szprychie wirtualnego centrum danych.

**Zdarzenia i obsługa komunikatów:** platforma [Azure Event Hubs][EventHubs] to usługa pozyskiwania danych Big Data i usług pozyskiwania zdarzeń. Może odbierać i przetwarzać miliony zdarzeń na sekundę. Zapewnia ona małe opóźnienia i możliwość konfigurowania czasu przechowywania, dzięki czemu można pozyskiwanie ogromnych ilości danych na platformie Azure i odczytywać je z wielu aplikacji. Pojedynczy strumień może obsługiwać zarówno potoki w czasie rzeczywistym, jak i oparte na partiach.

Możesz zaimplementować wysoce niezawodną usługę do obsługi komunikatów w chmurze między aplikacjami i usługami za pomocą [Azure Service Bus][ServiceBus]. Oferuje asynchroniczne komunikaty obsługiwane przez brokera między klientem i serwerem, strukturalną funkcją pierwszej pierwszej wyewidencjonowywania (FIFO) i publikowaniem i subskrybowaniem funkcji.

![10][10]

Te przykłady stanowią jedynie ułameką powierzchnię typów obciążeń, które można utworzyć na platformie Azure. wszystko od podstawowej aplikacji sieci Web i programu SQL Server do najnowszej wersji usługi IoT, danych Big Data, Machine Learning, AI i tak wiele więcej.

### <a name="highly-availability-multiple-virtual-datacenters"></a>Wysoka dostępność: wiele wirtualnych centrów danych

Do tej pory ten artykuł koncentruje się na projektowaniu jednego VDC, opisującym podstawowe składniki i architektury, które przyczyniają się do odporności. Funkcje platformy Azure, takie jak Azure load module, urządzeń WUS, strefy dostępności, zestawy dostępności, zestawy skalowania i inne funkcje, które ułatwiają uwzględnienie stałych poziomów umów SLA w usługach produkcyjnych.

Jednak ze względu na to, że wirtualne centrum danych jest zwykle zaimplementowane w jednym regionie, może być narażony na awarie, które mają wpływ na cały region. Klienci wymagający wysokiej dostępności muszą chronić usługi za pomocą wdrożeń tego samego projektu w co najmniej dwóch implementacjach VDC wdrożonych w różnych regionach.

Oprócz zagadnień związanych z umową SLA kilka typowych scenariuszy korzysta z wielu wirtualnych centrów danych:

- Regionalne lub globalne obecność użytkowników końcowych lub partnerów.
- Wymagania dotyczące odzyskiwania po awarii.
- Mechanizm do przekierowywania ruchu między centrami danych w celu załadowania lub wydajności.

#### <a name="regionalglobal-presence"></a>Obecność regionalna/globalna

Centra danych platformy Azure istnieją w wielu regionach na całym świecie. Podczas wybierania wielu centrów danych platformy Azure należy wziąć pod uwagę dwa czynniki pokrewne: odległości geograficzne i opóźnienie. Aby zoptymalizować środowisko użytkownika, należy oszacować odległość między poszczególnymi centrami wirtualnymi, a także odległość od każdego wirtualnego centrum danych do użytkowników końcowych.

Region świadczenia usługi Azure, który hostuje wirtualne centrum danych, musi być zgodny z wymaganiami prawnymi obowiązującymi w danej organizacji.

#### <a name="disaster-recovery"></a>Odzyskiwanie po awarii

Projekt planu odzyskiwania po awarii zależy od typów obciążeń i możliwości synchronizacji stanu tych obciążeń między różnymi implementacjami VDC. W idealnym przypadku większość klientów potrzebuje szybkiego mechanizmu pracy awaryjnej i wymaga synchronizacji danych aplikacji między wdrożeniami działającymi w wielu implementacjach VDC. Jednak podczas projektowania planów odzyskiwania po awarii należy wziąć pod uwagę, że większość aplikacji jest wrażliwa na opóźnienia, które może być spowodowane tą synchronizacją danych.

Synchronizacja i monitorowanie pulsu aplikacji w różnych implementacjach VDC wymaga ich komunikacji za pośrednictwem sieci. Wiele implementacji VDC w różnych regionach można połączyć za poorednictwem:

- Komunikacja między centrami jest wbudowana w wirtualne centra sieci WAN platformy Azure między regionami w tej samej wirtualnej sieci WAN.
- Komunikacja równorzędna sieci wirtualnych w celu połączenia centrów w różnych regionach.
- Prywatna Komunikacja równorzędna ExpressRoute, gdy centra w każdej implementacji VDC są połączone z tym samym obwodem ExpressRoute.
- Wiele obwodów usługi ExpressRoute połączonych za pośrednictwem sieci szkieletowej firmy oraz wiele implementacji VDC podłączonych do obwodów usługi ExpressRoute.
- Połączenia sieci VPN typu lokacja-lokacja między strefą centrum implementacji VDC w każdym regionie świadczenia usługi Azure.

Zwykle wirtualne centra sieci WAN, wirtualne sieci równorzędne lub połączenia ExpressRoute są preferowane dla połączeń sieciowych ze względu na wyższą przepustowość i spójne poziomy opóźnienia podczas przekazywania przez sieć szkieletową firmy Microsoft.

Uruchom testy kwalifikacji sieci, aby sprawdzić opóźnienia i przepustowość tych połączeń i zdecydować, czy synchroniczna lub asynchroniczna replikacja danych jest odpowiednia w oparciu o wynik. Ważne jest również, aby zważyć te wyniki w widoku optymalnego celu czasu odzyskiwania (RTO).

#### <a name="disaster-recovery-diverting-traffic-from-one-region-to-another"></a>Odzyskiwanie po awarii: przekierowywanie ruchu z jednego regionu do innego

Zarówno usługa [azure Traffic Manager][azure-traffic-manager] , jak i [drzwi platformy Azure][azure-front-door] okresowo sprawdzają kondycję usługi punktów końcowych nasłuchiwania w różnych implementacjach VDC i, jeśli te punkty końcowe zakończą się niepowodzeniem, są automatycznie kierowane do następnego najbliższej VDC Traffic Manager używa pomiarów użytkownika w czasie rzeczywistym i systemu DNS, aby kierować użytkowników do najbliższego (lub następnego najbliższego wystąpienia błędu). Drzwi frontonu platformy Azure to zwrotny serwer proxy o ponad 100 lokacjach brzegowych firmy Microsoft, przy użyciu emisji pojedynczej do kierowania użytkowników do najbliższego punktu końcowego nasłuchiwania.

### <a name="summary"></a>Podsumowanie

Wirtualne podejście do migracji do centrum danych tworzy skalowalną architekturę, która optymalizuje użycie zasobów platformy Azure, obniża koszty i upraszcza zarządzanie systemem. Wirtualne centrum danych jest typowe w oparciu o topologie sieci Hub i szprych (za pomocą wirtualnych sieci równorzędnych lub wirtualnych koncentratorów WAN). Wspólne usługi udostępnione udostępniane w centrum, a określone aplikacje i obciążenia są wdrażane w szprychach. Wirtualne centrum danych jest również zgodne ze strukturą ról firmy, w której różne działy, takie jak centralne IT, DevOps i Operations and Maintenance, działają razem podczas wykonywania ich określonych ról. Wirtualne centrum danych obsługuje Migrowanie istniejących obciążeń lokalnych na platformę Azure, ale również zapewnia wiele korzyści dla wdrożeń natywnych w chmurze.

## <a name="references"></a>Dokumentacja

Dowiedz się więcej na temat możliwości platformy Azure omówionych w tym dokumencie.

<!-- markdownlint-disable MD033 -->

|Funkcje sieciowe | Równoważenie obciążenia | Łączność |
| --- | --- | --- |
|[Sieci wirtualne platformy Azure][virtual-network]</br>[Sieciowe grupy zabezpieczeń][NSG]</br>[Punkty końcowe usługi][ServiceEndpoints]</br>[Link prywatny][PrivateLink]</br>[Trasy zdefiniowane przez użytkownika][UDR]</br>[Wirtualne urządzenia sieciowe][NVA]</br>[Publiczne adresy IP][PIP]</br>[System DNS platformy Azure][DNS]|[Azure Front Door][azure-front-door]</br>[Azure Load Balancer (P4)][ALB]</br>[Application Gateway (P7)][AppGW]</br>[Traffic Manager platformy Azure][azure-traffic-manager]</br></br></br></br></br> |[Virtual Network komunikacji równorzędnej][virtual-network-peering]</br>[Wirtualna sieć prywatna][VPN]</br>[Wirtualna sieć WAN][virtual-wan]</br>[ExpressRoute][ExR]</br>[Usługa ExpressRoute Direct][ExRD]</br></br></br></br></br>

|Tożsamość | Monitorowanie | Najlepsze rozwiązania |
| --- | --- | --- |
|[Azure Active Directory][azure-ad]</br>[Multi-Factor Authentication][multi-factor-authentication]</br>[Kontrola dostępu oparta na rolach][RBAC]</br>[Domyślne role usługi Azure AD][Roles]</br></br></br> |[Network Watcher][NetWatch]</br>[Azure Monitor][MonitorOverview]</br>[Log Analytics][LogAnalytics]</br> |[Grupa zarządzania][MgmtGrp]</br>[Zarządzanie subskrypcjami][subscription-management]</br>[Zarządzanie grupami zasobów][RGMgmt]</br>[Limity subskrypcji platformy Azure][limits] </br></br></br>|

Zabezpieczenia |Inne usługi platformy Azure | |
|-|-|-|
|[Azure Firewall][AzFW]</br>[Firewall Manager][AzFWMgr]</br>[Application Gateway WAF][AppGWWAF]</br>[WAF drzwi przednich][AFDWAF]</br>[Azure DDoS][DDoS]</br>|[Usługa Azure Storage][Storage]</br>[Azure SQL][SQL]</br>[Azure Web Apps][WebApps]</br>[Cosmos DB][Cosmos]</br>[HDInsight][HDInsight]|[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]</br>[Azure IoT][IoT]</br>[Azure Machine Learning][machine-learning]|

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [komunikacji równorzędnej sieci wirtualnych][virtual-network-peering], podstawowej technologii topologii gwiazdy i szprych.
- Zaimplementuj [Azure Active Directory][azure-ad] , aby użyć [kontroli dostępu opartej na rolach][RBAC].
- Opracowywanie modelu zarządzania subskrypcjami i zasobami przy użyciu kontroli dostępu opartej na rolach, która pasuje do struktury, wymagań i zasad organizacji. Planowanie najważniejszych działań. Analizuj, w jaki sposób reorganizacja, fuzje, nowe linie produktów i inne zagadnienia wpłyną na początkowe modele, aby zapewnić możliwość skalowania w celu spełnienia przyszłych potrzeb i wzrostu.

<!-- images -->

[0]: ../_images/vdc/networking-vdc-redundant.png "Przykłady nakładania się składników"
<!-- _1_ >: ../_images/vdc/networking-vdc-high-level.png "Example of hub and spoke VDC" -->
[2]: ../_images/vdc/networking-vdc-cluster.png "Klaster centrów i szprych"
[3]: ../_images/vdc/networking-vdc-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ../_images/vdc/networking-vdc-block-level-diagram.png "Diagram poziomu blokowego VDC"
[5]: ../_images/vdc/networking-vdc-users-groups-subscriptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ../_images/vdc/networking-vdc-infrastructure.png "Diagram infrastruktury"
[7]: ../_images/vdc/networking-vdc-perimeter.png "Diagram infrastruktury"
[8]: ../_images/vdc/networking-vdc-perimeter-peering.png "Virtual Network komunikacji równorzędnej i sieci obwodowej"
[9]: ../_images/vdc/networking-vdc-monitoring.png "Diagram Azure Monitor"
[10]: ../_images/vdc/networking-vdc-workloads.png "Diagram obciążeń"
[11]: ../_images/vdc/networking-vdc-brief-flat.png "Przykład sieci płaskiej"
[12]: ../_images/vdc/networking-vdc-brief-mesh.png "Przykład sieci z siatką"
[13]: ../_images/vdc/networking-vdc-brief-hub.png "Przykład VDC gwiazdy"
[14]: ../_images/vdc/networking-vdc-brief-vwan.png "Przykład wirtualnej sieci WAN VDC"

<!-- links -->

[limits]: https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[virtual-network]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/security-overview
[PrivateLink]: https://docs.microsoft.com/azure/private-link/private-link-overview
[PrivateLinkSvc]: https://docs.microsoft.com/azure/private-link/private-link-service-overview
[ServiceEndpoints]: https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[virtual-network-peering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[multi-factor-authentication]: https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks
[azure-ad]: https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[virtual-wan]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[AzFWMgr]: https://docs.microsoft.com/azure/firewall-manager/overview
[Organize]: ../ready/azure-setup-guide/organize-resources.md
[MgmtGrp]: https://docs.microsoft.com/azure/governance/management-groups/overview
[subscription-management]: ../ready/azure-best-practices/scale-subscriptions.md
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal#what-is-a-resource-group
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[DDoS]: https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/virtual-network-public-ip-address
[azure-front-door]: https://docs.microsoft.com/azure/frontdoor/front-door-overview
[AFDWAF]: https://docs.microsoft.com/azure/web-application-firewall/afds/afds-overview
[AppGW]: https://docs.microsoft.com/azure/application-gateway/overview
[AppGWWAF]: https://docs.microsoft.com/azure/web-application-firewall/ag/ag-overview
[MonitorOverview]: https://docs.microsoft.com/azure/networking/networking-overview#monitor
[AzureMonitor]: https://docs.microsoft.com/azure/azure-monitor/overview
[Metrics]: https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-metrics
[Logs]: https://docs.microsoft.com/azure/azure-monitor/platform/data-platform-logs
[LogAnalytics]: https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal
[NetWatch]: https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview
[WebApps]: https://docs.microsoft.com/azure/app-service/
[HDInsight]: https://docs.microsoft.com/azure/hdinsight/hdinsight-overview
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-about
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[azure-traffic-manager]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
[Storage]: https://docs.microsoft.com/azure/storage/common/storage-introduction
[SQL]: https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview
[Cosmos]: https://docs.microsoft.com/azure/cosmos-db/introduction
[IoT]: https://docs.microsoft.com/azure/iot-fundamentals/iot-introduction
[machine-learning]: https://docs.microsoft.com/azure/machine-learning/overview-what-is-azure-ml
