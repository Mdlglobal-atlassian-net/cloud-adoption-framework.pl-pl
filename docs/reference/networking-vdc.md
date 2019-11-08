---
title: 'Wirtualne centra danych: perspektywa sieci'
description: Dowiedz się, jak utworzyć wirtualne centrum danych na platformie Azure.
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 526c7846de947b9098f7d9d0b7458a314177a9c8
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753732"
---
# <a name="virtual-datacenters-a-network-perspective"></a>Wirtualne centra danych: perspektywa sieci

## <a name="overview"></a>Przegląd

Migrowanie lokalnych aplikacji na platformę Azure zapewnia organizacjom zalety zabezpieczonej i opłacalnej infrastruktury, nawet jeśli aplikacje są migrowane z minimalnymi zmianami. Aby jednak zapewnić największą elastyczność w zakresie przetwarzania w chmurze, przedsiębiorstwa muszą rozwijać swoje architektury, aby korzystać z możliwości platformy Azure.

Microsoft Azure zapewnia usługi i infrastrukturę z możliwością skalowania przy użyciu funkcji i niezawodności klasy korporacyjnej. Te usługi i infrastruktura oferują wiele opcji łączności hybrydowej, dzięki czemu klienci mogą uzyskiwać dostęp do nich za pośrednictwem publicznej sieci Internet lub za pośrednictwem prywatnego połączenia usługi Azure ExpressRoute. Partnerzy firmy Microsoft oferują również ulepszone funkcje, oferując usługi zabezpieczeń i urządzenia wirtualne zoptymalizowane pod kątem działania na platformie Azure.

Klienci mogą wybrać dostęp do tych usług w chmurze za pośrednictwem Internetu lub usługi Azure ExpressRoute, która zapewnia łączność sieci prywatnej. Dzięki platformie Microsoft Azure klienci mogą bezproblemowo rozbudować infrastrukturę do chmury i skompilować architektury wielowarstwowe. Partnerzy firmy Microsoft oferują również ulepszone funkcje, oferując usługi zabezpieczeń i urządzenia wirtualne zoptymalizowane pod kątem działania na platformie Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-virtual-datacenter"></a>Co to jest wirtualne centrum danych?

W tej chwili chmura była zasadniczo platformą do hostowania aplikacji publicznych. Przedsiębiorstwa rozpoczęły zrozumienie wartości chmury i rozpoczęły przenoszenie wewnętrznych aplikacji biznesowych do chmury. Te typy aplikacji spowodowały dodatkowe kwestie dotyczące zabezpieczeń, niezawodności, wydajności i kosztów, które wymagały dodatkowej elastyczności w sposobie dostarczania usług w chmurze. Ukryte to sposób tworzenia nowych infrastruktury i usług sieciowych zaprojektowanych w celu zapewnienia tej elastyczności, ale także nowych funkcji skalowania, odzyskiwania po awarii i innych zagadnień.

Rozwiązania w chmurze zostały wcześniej zaprojektowane do obsługi jednego, relatywnie izolowanych aplikacji w spektrum publicznym. To podejście działało prawidłowo przez kilka lat. Następnie korzyści płynące z rozwiązań w chmurze i wiele obciążeń o dużej skali są hostowane w chmurze. Rozwiązywanie problemów dotyczących zabezpieczeń, niezawodności, wydajności i kosztów wdrożeń w jednym lub kilku regionach stało się istotne w całym cyklu życia usługi w chmurze.

Na poniższym diagramie wdrożenia w chmurze przedstawiono przykład luki w zabezpieczeniach wyróżnioną w kolorze czerwonym. Żółte pole zawiera pomieszczenie do optymalizowania sieciowych urządzeń wirtualnych w ramach obciążeń.

![0][0]

Wirtualne centrum danych to koncepcja, która ponosi konieczność skalowania do obsługi obciążeń przedsiębiorstwa, a jednocześnie równoważy konieczność zajmowania się problemami wprowadzonymi podczas obsługi aplikacji o dużej skali w chmurze publicznej.

Implementacja wirtualnego centrum danych nie reprezentuje jedynie obciążeń aplikacji w chmurze, ale także sieci, zabezpieczeń, zarządzania i infrastruktury (na przykład usługi DNS i usług katalogowych). W miarę jak coraz więcej obciążeń przedsiębiorstwa przechodzą na platformę Azure, ważne jest, aby myśleć o infrastrukturze pomocniczej i obiektach, w których umieszczane są te obciążenia. Należy dokładnie zadbać o to, jak zasoby są strukturalne, aby uniknąć rozprzestrzeniania setek "wysp obciążeń", które muszą być zarządzane oddzielnie z niezależnym przepływem danych, modelami zabezpieczeń i wyzwaniami dotyczącymi zgodności.

Koncepcje wirtualnego centrum danych to zestaw zaleceń i najlepszych rozwiązań związanych z wdrażaniem kolekcji oddzielnych, ale powiązanych jednostek ze wspólnymi funkcjami pomocniczymi, funkcjami i infrastrukturą. Wyświetlając swoje obciążenia za pomocą obiektywu wirtualnego centrum danych, można osiągnąć obniżony koszt z powodu oszczędności skalowania, zoptymalizowanych zabezpieczeń za pomocą scentralizowanego składnika i kontroli, a także ułatwić operacje, zarządzanie i inspekcje zgodności.

> [!NOTE]
> Ważne jest, aby zrozumieć, że wirtualne centrum danych **nie** jest dyskretnym produktem platformy Azure, ale kombinacją różnych funkcji i możliwości, które spełniają Twoje dokładne wymagania. Wirtualne centrum danych to sposób, w którym można myśleć o obciążeniach i użyciu platformy Azure, aby zmaksymalizować zasoby i możliwości w chmurze. Jest to modularna metoda tworzenia usług IT na platformie Azure z uwzględnieniem ról organizacyjnych i obowiązków przedsiębiorstwa.

Implementacja wirtualnego centrum danych może pomóc przedsiębiorstwom w uzyskaniu obciążeń i aplikacji na platformie Azure w następujących scenariuszach:

- Hostowanie wielu powiązanych obciążeń.
- Migruj obciążenia ze środowiska lokalnego na platformę Azure.
- Implementowanie wspólnych lub scentralizowanych wymagań dotyczących zabezpieczeń i dostępu w ramach obciążeń.
- DevOps platformę Azure i scentralizowanie ją odpowiednio dla dużych przedsiębiorstw.

Kluczem do odblokowania zalet wirtualnego centrum danych jest scentralizowana topologia sieci piasty i szprycha z różnymi usługami i funkcjami platformy Azure:

- [Virtual Network platformy Azure][VNet],
- [Sieciowe grupy zabezpieczeń][network-security-groups],
- [Komunikacja równorzędna sieci wirtualnej][VNetPeering],
- [Trasy zdefiniowane przez użytkownika][user-defined-routes]i
- Tożsamość platformy Azure z [kontrolą dostępu opartą na rolach (RBAC)][RBAC] i opcjonalnie [zaporą platformy Azure][AzFW], [Azure DNS][DNS], [frontony platformy Azure][AFD]i [Azure Virtual WAN][vWAN].

## <a name="who-should-implement-a-virtual-datacenter"></a>Kto powinien zaimplementować wirtualne centrum danych?

Każdy klient platformy Azure, który zdecydował się przyjąć chmurę, może skorzystać z efektywności konfigurowania zestawu zasobów do wspólnego użycia przez wszystkie aplikacje. W zależności od wielkości nawet pojedyncze aplikacje mogą korzystać z wzorców i składników używanych do kompilowania implementacji wirtualnego centrum danych.

Jeśli organizacja ma centralne zespoły lub działy dla działu IT, sieci, zabezpieczeń lub zgodności, implementacja wirtualnego centrum danych może pomóc wymusić punkty zasad, rozdzielenia cła i zapewnić jednorodność podstawowych składników, jednocześnie dostarczając zespoły aplikacji mogą mieć wiele wolności i kontrolować odpowiednie wymagania.

Organizacje, które chcą DevOps, mogą również używać podstawowych koncepcji centrów danych w celu zapewnienia autoryzowanych kieszeni zasobów platformy Azure i upewnienia się, że mają całkowitą kontrolę w tej grupie (subskrypcję lub grupę zasobów w ramach wspólnej subskrypcji), ale granice sieci i zabezpieczeń pozostają zgodne zgodnie z definicją scentralizowanych zasad w centralnej sieci wirtualnej i grupie zasobów.

<!-- markdownlint-enable MD026 -->

## <a name="considerations-for-implementing-a-virtual-datacenter"></a>Zagadnienia dotyczące implementacji wirtualnego centrum danych

Podczas projektowania implementacji wirtualnego centrum danych należy wziąć pod uwagę kilka problemów z wystawieniem:

### <a name="identity-and-directory-service"></a>Tożsamość i usługa katalogowa

Tożsamości i usługi katalogowe są kluczowym aspektem wszystkich centrów danych, zarówno lokalnie, jak i w chmurze. Tożsamość jest związana ze wszystkimi aspektami dostępu i autoryzacji do usług w ramach wirtualnej implementacji centrum danych. Aby mieć pewność, że tylko autoryzowani użytkownicy i procesy uzyskują dostęp do Twojego konta i zasobów platformy Azure, platforma Azure korzysta z kilku typów poświadczeń do uwierzytelniania. Obejmują one hasła (Aby uzyskać dostęp do konta platformy Azure), kluczy kryptograficznych, podpisów cyfrowych i certyfikatów. [Usługa azure Multi-Factor Authentication][multi-factor-authentication] to dodatkowa warstwa zabezpieczeń do uzyskiwania dostępu do usług platformy Azure. Multi-Factor Authentication zapewnia silne uwierzytelnianie dzięki szerokiemu zakresowi opcji łatwej weryfikacji (połączenie telefoniczne, wiadomość SMS lub powiadomienie aplikacji mobilnej) i umożliwia klientom wybranie preferowanej metody.

Każde duże przedsiębiorstwo musi zdefiniować proces zarządzania tożsamościami, który opisuje zarządzanie indywidualnymi tożsamościami, uwierzytelnianiem, autoryzacją, rolami i uprawnieniami w ramach lub w ramach ich wirtualnej implementacji centrum danych. Celem tego procesu jest zwiększenie bezpieczeństwa i produktywności przy jednoczesnym zmniejszeniu kosztów, przestoju i powtarzalnych zadań ręcznych.

Organizacje korporacyjne mogą wymagać wymagającej kombinacji usług dla różnych branż, a pracownicy często mają różne role w przypadku różnych projektów. Wirtualne centrum danych wymaga odpowiedniej współpracy między różnymi zespołami, z których każda korzysta z określonych ról, w celu uzyskania systemów z dobrymi zasadami zarządzania. Macierz obowiązków, dostępu i praw mogą być złożone. Zarządzanie tożsamościami w wirtualnym centrum danych jest realizowane za pośrednictwem [Azure Active Directory (Azure AD)][azure-ad] i kontroli dostępu opartej na ROLACH (RBAC).

Usługa katalogowa to udostępniona infrastruktura informacyjna, która umożliwia lokalizowanie i organizowanie codziennych elementów oraz zasobów sieciowych oraz zarządzanie nimi. Te zasoby mogą obejmować woluminy, foldery, pliki, drukarki, użytkowników, grupy, urządzenia i inne obiekty. Każdy zasób w sieci jest traktowany jako obiekt przez serwer katalogowy. Informacje o zasobie są przechowywane jako Kolekcja atrybutów skojarzonych z tym zasobem lub obiektem.

Wszystkie usługi Microsoft Online Business Services są zależne od Azure Active Directory (Azure AD) w celu logowania się i innych potrzeb związanych z tożsamościami. Usługa Azure Active Directory to kompleksowe rozwiązanie o wysokiej dostępności do zarządzania tożsamościami i dostępem w chmurze, które oferuje podstawowe usługi katalogowe, zaawansowane funkcje zarządzania tożsamościami i zarządzania dostępem do aplikacji. Usługa Azure AD może być zintegrowana z lokalnym Active Directory, aby umożliwić Logowanie jednokrotne dla wszystkich aplikacji lokalnych opartych na chmurze i lokalnie hostowanych. Atrybuty użytkownika lokalnego Active Directory mogą być automatycznie synchronizowane z usługą Azure AD.

Do przypisywania wszystkich uprawnień w wirtualnej implementacji centrum danych nie jest wymagany pojedynczy Administrator globalny. Zamiast tego każdy konkretny dział, Grupa użytkowników lub usługi w usłudze katalogowej może mieć uprawnienia wymagane do zarządzania własnymi zasobami w ramach implementacji wirtualnego centrum danych. Uprawnienia do tworzenia struktury wymagają równoważenia. Zbyt wiele uprawnień może utrudnić wydajność, a zbyt mało lub luźne uprawnienia mogą zwiększyć zagrożenie bezpieczeństwa. Kontrola dostępu oparta na rolach (RBAC) na platformie Azure pomaga rozwiązać ten problem, oferując precyzyjne zarządzanie dostępem do zasobów w ramach implementacji wirtualnego centrum danych.

#### <a name="security-infrastructure"></a>Infrastruktura zabezpieczeń

Infrastruktura zabezpieczeń odnosi się do podziału ruchu w konkretnym segmencie sieci wirtualnej w ramach implementacji wirtualnego centrum danych. Ta infrastruktura określa sposób, w jaki dane przychodzące i wychodzące są kontrolowane w wirtualnej implementacji centrum danych. Platforma Azure jest oparta na architekturze wielodostępnej, która zapobiega nieautoryzowanemu i niezamierzonyemu ruchowi między wdrożeniami przy użyciu izolacji sieci wirtualnej, list kontroli dostępu (ACL), modułów równoważenia obciążenia, filtrów IP i zasad przepływu ruchu. Translator adresów sieciowych (NAT) oddziela ruch sieciowy między ruchem zewnętrznym.

Sieć szkieletowa Azure przydziela zasoby infrastruktury do obciążeń dzierżawców i zarządza komunikacją z maszynami wirtualnymi i z nich. Funkcja hypervisor platformy Azure wymusza separację pamięci i procesów między maszynami wirtualnymi i bezpiecznie kieruje ruch sieciowy do dzierżawców systemu operacyjnego gościa.

#### <a name="connectivity-to-the-cloud"></a>Łączność z chmurą

Implementacja wirtualnego centrum danych wymaga połączenia z sieciami zewnętrznymi w celu oferowania usług klientom, partnerom i użytkownikom wewnętrznym. Wymaganie łączności dotyczy nie tylko Internetu, ale również do sieci lokalnych i centrów danych.

Klienci kontrolują dostęp do usług i są dostępne z publicznej sieci Internet przy użyciu [zapory platformy Azure][AzFW] lub innych typów urządzeń sieci wirtualnej (urządzeń WUS), niestandardowych zasad routingu za pomocą [tras zdefiniowanych przez użytkownika][user-defined-routes]i sieci Filtrowanie przy użyciu [sieciowych grup zabezpieczeń][network-security-groups]. Firma Microsoft zaleca, aby wszystkie zasoby dostępne z Internetu były chronione także przez [Standard Azure DDoS Protection][DDoS].

Przedsiębiorstwa mogą wymagać łączenia ich implementacji wirtualnego centrum danych z lokalnymi centrami danych lub innymi zasobami. Połączenie między platformą Azure i sieciami lokalnymi jest kluczowym aspektem podczas projektowania efektywnej architektury. Przedsiębiorstwa mają dwa różne sposoby tworzenia połączeń: przekazywanie przez Internet lub bezpośrednie połączenia prywatne.

Połączenie [**sieci VPN typu lokacja-lokacja**][VPN] jest usługą połączenia za pośrednictwem Internetu między sieciami lokalnymi a implementacją wirtualnego centrum danych ustanowioną za pośrednictwem bezpiecznych połączeń szyfrowanych (tunele protokołu IPSec/IKE). Połączenie lokacja-lokacja jest elastyczne, szybkie oraz proste w tworzeniu i nie wymaga żadnych dalszych zakupów, ponieważ wszystkie połączenia nawiązują połączenie za pośrednictwem Internetu.

W przypadku dużej liczby połączeń sieci VPN [**Azure Virtual WAN**][vWAN] jest usługą sieciową, która zapewnia zoptymalizowaną i zautomatyzowaną łączność między gałęziami za pośrednictwem platformy Azure. Wirtualna sieć WAN umożliwia łączenie się z konfigurowaniem urządzeń gałęziowych w celu komunikowania się z platformą Azure. Łączenie i Konfigurowanie można wykonać ręcznie lub za pomocą preferowanych urządzeń dostawcy za pośrednictwem wirtualnego partnera sieci WAN. Korzystanie z preferowanych urządzeń dostawcy umożliwia łatwe używanie, uproszczenie łączności i zarządzanie konfiguracją. Wbudowany pulpit nawigacyjny sieci WAN na platformie Azure udostępnia na bieżąco wskazówki dotyczące rozwiązywania problemów, dzięki którym oszczędzisz czas, i umożliwia łatwe monitorowanie łączności między lokacjami w dużej skali.

[**ExpressRoute**][ExR] to usługa łączności platformy Azure, która umożliwia prywatne połączenia między implementacją wirtualnego centrum danych a sieciami lokalnymi. Połączenia ExpressRoute nie przechodzą przez publiczny Internet i oferują wyższy poziom bezpieczeństwa, niezawodność i wyższą szybkość (do 10 GB/s) oraz spójne opóźnienia. ExpressRoute jest przydatne w przypadku implementacji wirtualnych centrów danych, ponieważ klienci ExpressRoute mogą uzyskać korzyści wynikające z reguł zgodności skojarzonych z połączeniami prywatnymi. Za pomocą usługi [ExpressRoute Direct][ExRD]można łączyć się bezpośrednio z routerami firmy Microsoft na 100 GB/s dla klientów o większych wymaganiach dotyczących przepustowości.

Wdrażanie połączeń usługi ExpressRoute obejmuje zazwyczaj zaangażowanie dostawcy usług ExpressRoute. W przypadku klientów, którzy muszą szybko rozpocząć pracę, często należy najpierw użyć sieci VPN typu lokacja-lokacja do ustanowienia łączności między wirtualną implementacją centrum danych a zasobami lokalnymi, a następnie przeprowadzić migrację do połączenia ExpressRoute, gdy fizyczne połączenie z dostawcą usług zostało zakończone.

#### <a name="connectivity-within-the-cloud"></a>*Łączność w chmurze*

[Sieci wirtualnych][VNet] i [wirtualna Komunikacja równorzędna][VNetPeering] to podstawowe usługi łączności sieciowej w ramach implementacji wirtualnego centrum danych. Sieć wirtualna gwarantuje naturalną granicę izolacji wirtualnych zasobów centrum danych, a Komunikacja równorzędna między różnymi sieci wirtualnychami w tym samym regionie platformy Azure lub nawet w różnych regionach. Kontrola ruchu wewnątrz sieci wirtualnej i między sieci wirtualnych musi być zgodna z zestawem reguł zabezpieczeń określonych przy użyciu list kontroli dostępu ([sieciowych grup zabezpieczeń][network-security-groups]), [wirtualnych urządzeń sieciowych][NVA]i niestandardowych tabel routingu ([tras zdefiniowanych przez użytkownika][user-defined-routes]).

## <a name="virtual-datacenter-overview"></a>Omówienie wirtualnego centrum danych

### <a name="topology"></a>Topologia

*Koncentrator i szprycha* to model służący do projektowania topologii sieci dla implementacji wirtualnego centrum danych.

![1][1]

Jak pokazano, na platformie Azure można używać dwóch typów konstrukcji i gwiazdy. W przypadku komunikacji, zasobów udostępnionych i scentralizowanych zasad zabezpieczeń (koncentrator sieci VNet na diagramie) lub wirtualnego typu sieci WAN (wirtualna sieć WAN na diagramie) dla dużej ilości gałęzi do rozgałęzienia i rozgałęziania do platformy Azure.

Centrum jest centralną strefą sieci, która kontroluje i sprawdza ruch przychodzący lub wyjściowy między różnymi strefami: Internet, lokalnie i szprych. Topologia gwiazdy umożliwia działowi IT efektywną metodę wymuszania zasad zabezpieczeń w centralnej lokalizacji. Minimalizuje również ryzyko błędnej konfiguracji i ekspozycji.

Koncentrator często zawiera wspólne składniki usługi używane przez szprychy. Poniżej przedstawiono typowe usługi centralne:

- Infrastruktura Active Directory systemu Windows, wymagana do uwierzytelniania użytkowników innych firm, którzy uzyskują dostęp z niezaufanych sieci przed uzyskaniem dostępu do obciążeń w szprychie. Obejmuje ona powiązane usługi Active Directory Federation Services (AD FS).
- Usługa DNS do rozpoznawania nazw obciążeń w szprychach, do uzyskiwania dostępu do zasobów lokalnych i w Internecie, jeśli usługa [Azure DNS][DNS] nie jest używana.
- Infrastruktura kluczy publicznych (PKI) do implementowania obciążeń logowania jednokrotnego.
- Kontrola przepływu ruchu TCP i UDP między strefami sieciowymi szprych i Internetem.
- Sterowanie przepływem między szprychami i środowiskiem lokalnym.
- W razie konieczności sterowanie przepływem między jedną szprychą a inną.

Wirtualne centrum danych zmniejsza całkowity koszt przy użyciu infrastruktury centrum udostępnionej między wieloma szprychami.

Rolą każdej szprychy może być hostowanie różnych typów obciążeń. Szprychy zapewniają również modularne podejście do powtarzających się wdrożeń tych samych obciążeń. Przykłady to programowanie i testowanie, testy akceptacji użytkowników, środowisko przedprodukcyjne i środowisko produkcyjne. Szprychy mogą również dzielić różne grupy w obrębie organizacji i umożliwiać ich tworzenie. Przykładem są grupy usługi Azure DevOps. Wewnątrz szprychy można wdrażać podstawowe obciążenia lub złożone obciążenia wielowarstwowe z kontrolą ruchu między warstwami.

#### <a name="subscription-limits-and-multiple-hubs"></a>Ograniczenia subskrypcji i wiele piast

Na platformie Azure każdy składnik, niezależnie od typu, jest wdrażany w ramach subskrypcji platformy Azure. Izolacja składników platformy Azure w różnych subskrypcjach platformy Azure może spełniać wymagania różnych LOB, takich jak konfigurowanie zróżnicowanego poziomu dostępu i autoryzacji.

Pojedyncza implementacja wirtualnego centrum danych może skalować w górę do dużej liczby szprych, chociaż podobnie jak w przypadku każdego systemu INFORMATYCZNego, istnieją limity platformy. Wdrożenie usługi Hub jest powiązane z określoną subskrypcją platformy Azure, która ma ograniczenia i limity (na przykład maksymalną liczbę wirtualnych sieci równorzędnych; Aby uzyskać szczegółowe informacje, zobacz [limity subskrypcji i usług platformy Azure, przydziały i ograniczenia][limits] ). W przypadkach, gdy mogą to być problemy, architektura można skalować w górę, rozszerzając model z jednego piasty do klastra koncentratora i szprych. Wiele centrów w jednym lub większej liczbie regionów świadczenia usługi Azure można połączyć za pomocą komunikacji równorzędnej sieci wirtualnych, ExpressRoute, wirtualnej sieci WAN lub VPN typu lokacja-lokacja.

![2][2]

Wprowadzenie wielu centrów zwiększa koszty i nakłady pracy związane z zarządzaniem systemem. Jest to usprawiedliwione tylko skalowalnością, limitami systemu lub nadmiarowością oraz replikacją regionalną dla wydajności użytkownika końcowego lub odzyskiwania po awarii. W scenariuszach wymagających wielu centrów wszystkie centra powinny dążyć do zaoferowania tego samego zestawu usług w celu ułatwienia działania.

#### <a name="interconnection-between-spokes"></a>Wzajemne połączenia między szprychami

Wewnątrz jednego szprychy można zaimplementować złożone obciążenia wielowarstwowe. Konfiguracje wielowarstwowe można zaimplementować przy użyciu podsieci (jednej dla każdej warstwy) w tej samej sieci wirtualnej i filtrowanie przepływów przy użyciu sieciowych grup zabezpieczeń.

Architekt może chcieć wdrożyć obciążenie wielowarstwowe w wielu sieciach wirtualnych. Za pomocą komunikacji równorzędnej sieci wirtualnych szprychy mogą łączyć się z innymi szprychami w tym samym koncentratorze lub różnych centrach. Typowym przykładem tego scenariusza jest przypadek, w którym serwery przetwarzania aplikacji znajdują się w jednej szprychie lub w sieci wirtualnej. Baza danych jest wdrażana w innej szprychie lub w sieci wirtualnej. W takim przypadku można łatwo połączyć szprychy z usługą komunikacji równorzędnej sieci wirtualnej i w związku z tym uniknąć przesyłania danych przez centrum. Należy zachować ostrożną architekturę i Przegląd zabezpieczeń, aby upewnić się, że pominięcie centrum nie pomija ważnych punktów zabezpieczeń lub inspekcji, które mogą istnieć tylko w centrum.

![3][3]

Szprychy mogą być również połączone ze szprychą, która pełni rolę piasty. Takie podejście tworzy hierarchię dwupoziomową: szprycha na wyższym poziomie (poziom 0) staje się piastą dla małych szprych (poziom 1) w hierarchii. Szprychy wirtualnej implementacji centrum danych są wymagane do przekazywania ruchu do centralnego koncentratora, dzięki czemu ruch może być przesyłany do miejsca docelowego w sieci lokalnej lub w publicznym Internecie. Architektura z dwoma poziomami koncentratorów zawiera złożone Routing, który usuwa zalety prostej relacji gwiazdy.

Mimo że platforma Azure pozwala na złożone topologie, jedną z podstawowych zasad pojęcia wirtualnego centrum danych jest powtarzalność i prostota. W celu zminimalizowania nakładu pracy związanego z zarządzaniem prostym projektem gwiazdy jest architektura referencyjna wirtualnego centrum danych.

### <a name="components"></a>Składniki

Wirtualne centrum danych składa się z czterech podstawowych typów składników: **infrastruktury**, **sieci obwodowej**, **obciążeń**i **monitorowania**.

Każdy typ składnika składa się z różnych funkcji i zasobów platformy Azure. Implementacja wirtualnego centrum danych składa się z wystąpień wielu typów składników i wielu odmian tego samego typu składnika. Na przykład może istnieć wiele różnych logicznie oddzielonych wystąpień obciążeń, które reprezentują różne aplikacje. Te różne typy składników i wystąpienia są używane do ostatecznego tworzenia wirtualnego centrum danych.

![4][4]

Powyższa architektura koncepcyjna wysokiego poziomu wirtualnego centrum danych pokazuje różne typy składników używane w różnych strefach topologii gwiazdy. Diagram przedstawia składniki infrastruktury w różnych częściach architektury.

Ogólnie rzecz biorąc, prawa dostępu i uprawnienia powinny być oparte na grupach. Zajmowanie się grupami, a nie indywidualnymi użytkownikami, ułatwia konserwację zasad dostępu przez zapewnienie spójnego sposobu zarządzania nim w zespołach i pomaga w minimalizacji błędów konfiguracji. Przypisanie i usunięcie użytkowników do i z odpowiednich grup ułatwia zapewnienie aktualności uprawnień określonego użytkownika.

Każda grupa ról powinna mieć unikatowy prefiks dla swoich nazw. Ten prefiks ułatwia ustalenie, która grupa jest skojarzona z tym obciążeniem. Na przykład obciążenie obsługujące usługę uwierzytelniania może mieć grupy o nazwach **AuthServiceNetOps**, **AuthServiceSecOps**, **AuthServiceDevOps**i **AuthServiceInfraOps**. Scentralizowane role lub role niepowiązane z konkretną usługą mogą być poprzedzone **firmowymi**. Przykładem jest **CorpNetOps**.

Wiele organizacji używa odmian następujących grup w celu zapewnienia głównych podziałów ról:

- Centralna Grupa IT, **Corp** ma prawa własności do sterowania składnikami infrastruktury. Przykładami są sieci i zabezpieczenia. Grupa musi mieć rolę współautora w ramach subskrypcji, kontroli centrum i uprawnień współautora sieci w szprychach. Duże organizacje często dzielą te obowiązki związane z zarządzaniem między wieloma zespołami. Przykładami jest Grupa **CorpNetOps** operacji sieciowych z wyłącznym koncentracją w sieci i grupami operacji zabezpieczeń **CorpSecOps** , odpowiedzialnych za zaporę i zasady zabezpieczeń. W tym konkretnym przypadku należy utworzyć dwie różne grupy do przypisywania ról niestandardowych.
- Grupa Dev-Test, **AppDevOps,** ma odpowiedzialność za wdrażanie obciążeń aplikacji lub usług. Ta grupa przyjmuje rolę współautora maszyny wirtualnej dla wdrożeń IaaS lub co najmniej jedną rolę współautora PaaS. Zobacz [wbudowane role dla zasobów platformy Azure][Roles]. Opcjonalnie zespół deweloperów i testów może potrzebować widoczności zasad zabezpieczeń (sieciowych grup zabezpieczeń) i zasad routingu (zdefiniowanych przez użytkownika tras) w centrum lub w konkretnym szprychie. Oprócz roli współautora dla obciążeń, ta grupa powinna również mieć rolę czytnika sieci.
- Operacja i Grupa konserwacji, **CorpInfraOps** lub **AppInfraOps,** odpowiada za zarządzanie obciążeniami w środowisku produkcyjnym. Ta grupa musi być współautorem subskrypcji na obciążeniach w dowolnych subskrypcjach produkcyjnych. Niektóre organizacje mogą również oszacować, czy potrzebują dodatkowej grupy zespołu pomocy technicznej z rolą współautor subskrypcji w środowisku produkcyjnym i centralną subskrypcją centrum. Dodatkowa grupa rozwiązuje potencjalne problemy z konfiguracją w środowisku produkcyjnym.

Wirtualne centrum danych zostało zaprojektowane w taki sposób, że grupy utworzone dla centralnej grupy IT, zarządzanie centrum, mają odpowiednie grupy na poziomie obciążenia. Poza zarządzaniem tylko zasobami centrum centralną grupę IT można sterować dostępem zewnętrznym i uprawnieniami najwyższego poziomu w ramach subskrypcji. Grupy obciążeń mogą również kontrolować zasoby i uprawnienia sieci wirtualnej niezależnie od centralnej.

Wirtualne centrum danych jest podzielone na partycje, aby bezpiecznie hostować wiele projektów w różnych branżach. Wszystkie projekty wymagają różnych środowisk izolowanych (dev, przeprowadzających, Production). Osobne subskrypcje platformy Azure dla każdego z tych środowisk zapewniają naturalną izolację.

![5][5]

Na powyższym diagramie przedstawiono relację między projektami, użytkownikami i grupami organizacji oraz środowiskami, w których są wdrażane składniki platformy Azure.

Zwykle w tym środowisku (lub warstwie) jest system, w którym wiele aplikacji jest wdrażanych i wykonywanych. Duże przedsiębiorstwa wykorzystują środowisko programistyczne (gdzie zmiany są wprowadzane i testowane) oraz środowisko produkcyjne (które są używane przez użytkowników końcowych). Te środowiska są oddzielane, często z kilkoma środowiskami przejściowymi między nimi, aby umożliwić wdrażanie stopniowe (wdrażanie), testowanie i wycofywanie w przypadku wystąpienia problemów. Architektury wdrażania różnią się znacznie, ale zazwyczaj jest to podstawowy proces rozpoczynający się od projektowania (DEV) i kończący się w środowisku produkcyjnym.

Wspólna architektura dla tych typów środowisk wielowarstwowych składa się z usługi Azure DevOps na potrzeby programowania i testowania, przeprowadzających dla środowisk przejściowych i produkcyjnych. Organizacje mogą używać jednego lub wielu dzierżawców usługi Azure AD do definiowania dostępu i praw do tych środowisk. Poprzedni diagram przedstawia przypadek, w którym są używane dwa różne dzierżawy usługi Azure AD: jeden dla usług Azure DevOps i przeprowadzających, a drugi wyłącznie dla środowiska produkcyjnego.

Obecność różnych dzierżawców usługi Azure AD wymusza rozdzielenie między środowiskami. Ta sama Grupa użytkowników, taka jak Centralna, musi uwierzytelniać się przy użyciu innego identyfikatora URI w celu uzyskania dostępu do innej dzierżawy usługi Azure AD w celu zmodyfikowania ról lub uprawnień w środowisku produkcyjnym platformy Azure DevOps lub w projekcie. Obecność różnych uwierzytelnień użytkowników w celu uzyskania dostępu do różnych środowisk zmniejsza potencjalne przerwy i inne problemy spowodowane błędami ludzkimi.

#### <a name="component-type-infrastructure"></a>Typ składnika: infrastruktura

Ten typ składnika to miejsce, w którym znajduje się większość infrastruktury pomocniczej. Jest to również miejsce, w którym scentralizowane zespoły IT, bezpieczeństwa i zgodności spędzają najwięcej czasu.

![6][6]

Składniki infrastruktury zapewniają połączenie z różnymi składnikami implementacji wirtualnego centrum danych i znajdują się zarówno w centrum, jak i szprych. Odpowiedzialność za zarządzanie i utrzymywanie składników infrastruktury jest zwykle przypisana do centralnego zespołu IT lub zabezpieczeń.

Jednym z podstawowych zadań zespołu infrastruktury IT jest zagwarantowanie spójności schematów adresów IP w całym przedsiębiorstwie. Prywatna przestrzeń adresów IP przypisana do implementacji wirtualnego centrum danych musi być spójna i nie pokrywa się z prywatnymi adresami IP przypisanymi do sieci lokalnych.

Podczas gdy translator adresów sieciowych na lokalnych routerach granicznych lub w środowiskach platformy Azure może uniknąć konfliktów adresów IP, dodaje komplikacje do składników infrastruktury. Prostota zarządzania to jeden z najważniejszych celów wirtualnego centrum danych, dzięki czemu korzystanie z translatora adresów sieciowych do obsługi adresów IP nie jest zalecanym rozwiązaniem.

Składniki infrastruktury mają następujące funkcje:

- [**Tożsamości i usługi katalogowe**][azure-ad]. Dostęp do każdego typu zasobu na platformie Azure jest kontrolowany przez tożsamość przechowywaną w usłudze katalogowej. Usługa katalogowa przechowuje nie tylko listę użytkowników, ale również prawa dostępu do zasobów w określonej subskrypcji platformy Azure. Te usługi mogą istnieć tylko w chmurze lub mogą być synchronizowane z tożsamością lokalną przechowywaną w Active Directory.
- [**Virtual Network**][VPN]. Sieci wirtualne są jednym z głównych składników wirtualnego centrum danych i umożliwiają utworzenie granicy izolacji ruchu na platformie Azure. Virtual Network składa się z jednego lub wielu segmentów sieci wirtualnej, z których każdy ma określony prefiks sieci IP (podsieć). Virtual Network definiuje wewnętrzny obszar obwodu, w którym IaaS maszyny wirtualne i usługi PaaS mogą nawiązywać prywatną komunikację. Maszyny wirtualne (i usługi PaaS Services) w jednej sieci wirtualnej nie mogą komunikować się bezpośrednio z maszynami wirtualnymi (i usługami PaaS) w innej sieci wirtualnej, nawet jeśli obie sieci wirtualne są tworzone przez tego samego klienta w ramach tej samej subskrypcji. Izolacja jest właściwością krytyczną, która zapewnia, że maszyny wirtualne klienta i komunikacja pozostają prywatne w ramach sieci wirtualnej.
- [**Trasy zdefiniowane przez użytkownika**][user-defined-routes]. Ruch w sieci wirtualnej jest domyślnie kierowany na podstawie tabeli routingu systemowego. Zdefiniowana przez użytkownika trasa jest niestandardową tabelą routingu, którą Administratorzy sieci mogą skojarzyć z co najmniej jedną podsiecią, aby zastąpić zachowanie tabeli routingu systemu i zdefiniować ścieżkę komunikacji w ramach sieci wirtualnej. Obecność tras zdefiniowanych przez użytkownika gwarantuje, że ruch wychodzący z tranzytu szprych przez określone niestandardowe maszyny wirtualne lub wirtualne urządzenia sieciowe i moduły równoważenia obciążenia obecne zarówno w centrum, jak i szprych.
- [**Sieciowe grupy zabezpieczeń**][network-security-groups]. Grupa zabezpieczeń sieci to lista reguł zabezpieczeń, które działają jako Filtrowanie ruchu dla źródeł IP, miejsc docelowych adresów IP, protokołów, portów źródłowych IP i portów docelowych IP. Sieciową grupę zabezpieczeń można zastosować do podsieci, wirtualnej karty sieciowej skojarzonej z maszyną wirtualną platformy Azure lub obu tych usług. Sieciowe grupy zabezpieczeń są niezbędne do wdrożenia prawidłowej kontroli przepływu w centrum i szprych. Poziom zabezpieczeń zapewniany przez grupę zabezpieczeń sieci to funkcja, z której otwierane są porty i w jakim celu. Klienci powinni stosować dodatkowe filtry na maszynę wirtualną z użyciem zapór opartych na hoście, takich jak dołączenie iptables lub Zapora systemu Windows.
- [**System DNS**][DNS]. Rozpoznawanie nazw zasobów w sieci wirtualnych implementacji wirtualnego centrum danych jest zapewniane za pomocą systemu DNS. Platforma Azure udostępnia usługi DNS do rozpoznawania nazw [publicznych][DNS] i [prywatnych][PrivateDNS] . Strefy prywatne zapewniają rozpoznawanie nazw zarówno w sieci wirtualnej, jak i w sieciach wirtualnych. Strefy prywatne mogą nie tylko obejmować sieci wirtualne w tym samym regionie, ale również między regionami i subskrypcjami. Do publicznej rozdzielczości Azure DNS zapewnia usługi hostingu dla domen DNS, zapewniając rozpoznawanie nazw przy użyciu infrastruktury Microsoft Azure. Dzięki hostowaniu swoich domen na platformie Azure możesz zarządzać rekordami DNS z zastosowaniem tych samych poświadczeń, interfejsów API, narzędzi i rozliczeń co w przypadku innych usług platformy Azure.
- Zarządzanie [**subskrypcjami**][SubMgmt] i [**grupami zasobów**][RGMgmt]. Subskrypcja definiuje naturalną granicę, aby utworzyć wiele grup zasobów na platformie Azure. Zasoby w ramach subskrypcji są łączone razem z kontenerami logicznymi znanymi jako grupy zasobów. Grupa zasobów reprezentuje grupę logiczną w celu zorganizowania zasobów implementacji wirtualnego centrum danych.
- [**RBAC**][RBAC]. Za pomocą RBAC można zmapować rolę organizacyjną wraz z prawami dostępu do określonych zasobów platformy Azure, co pozwala ograniczyć użytkowników tylko do określonego podzestawu akcji. Za pomocą RBAC można udzielić dostępu, przypisując odpowiednią rolę użytkownikom, grupom i aplikacjom w odpowiednim zakresie. Zakres przypisania roli może być subskrypcją platformy Azure, grupą zasobów lub pojedynczym zasobem. RBAC umożliwia dziedziczenie uprawnień. Rola przypisana w zakresie nadrzędnym również przyznaje dostęp do elementów podrzędnych zawartych w nim. Za pomocą RBAC można oddzielić cła i przyznać dostęp tylko do użytkowników, których potrzebują do wykonywania swoich zadań. Na przykład za pomocą RBAC Zezwól jednemu pracownikowi na zarządzanie maszynami wirtualnymi w ramach subskrypcji, podczas gdy inna może zarządzać baz danych SQL w ramach tej samej subskrypcji.
- [**Komunikacja równorzędna sieci**][VNetPeering]wirtualnych. Podstawowa funkcja służąca do tworzenia infrastruktury wirtualnego centrum danych jest równorzędna Sieć wirtualna, mechanizm łączący dwie sieci wirtualne (sieci wirtualnych) w tym samym regionie za pośrednictwem sieci centrum danych platformy Azure lub za pomocą szkieletu World Wide Azure w różnych regionach .

#### <a name="component-type-perimeter-networks"></a>Typ składnika: sieci obwodowe

Składniki [sieci obwodowej][DMZ] umożliwiają połączenie sieciowe między lokalnymi lub fizycznymi sieciami centrów danych oraz łącznością z Internetem. Jest to również miejsce, gdzie zespoły sieci i zabezpieczeń prawdopodobnie spędzają najwięcej czasu.

Pakiety przychodzące powinny przechodzić przez urządzenia zabezpieczeń w centrum przed osiągnięciem serwerów zaplecza w szprychach. Przykłady to zapora, identyfikatory i adresy IP. Zanim opuszczą sieć, pakiety powiązane z Internetem z obciążeń powinny również przepływać przez urządzenia zabezpieczeń w sieci obwodowej. Przepływ ten ma na celu wymuszanie zasad, kontrolę i inspekcję.

Składniki sieci obwodowej zapewniają następujące funkcje:

- [Sieci wirtualne][VNet], [trasy definiowane przez użytkownika][user-defined-routes] oraz [sieciowe grupy zabezpieczeń][network-security-groups]
- [Wirtualne urządzenia sieciowe][NVA]
- [Azure Load Balancer][ALB]
- [Application Gateway platformy Azure][AppGW] z [zaporą aplikacji sieci Web (WAF)][AppGWWAF]
- [Publiczne adresy IP][PIP]
- [Drzwi frontonu platformy Azure][AFD] z [zaporą aplikacji sieci Web (WAF)][AFDWAF]
- [Azure Firewall][AzFW]

Zazwyczaj centralne zespoły IT i zabezpieczeń odpowiadają za definicje wymagań i eksploatację sieci obwodowej.

![7][7]

Na powyższym diagramie przedstawiono wymuszanie dwóch obwodów z dostępem do Internetu i sieci lokalnej, które znajdują się w centrum DMZ. W centrum DMZ sieć obwodowa z Internetem może być skalowana w górę, aby obsługiwała dużą liczbę LOB przy użyciu wielu Farm zapór aplikacji sieci Web (sieciowi) lub zapór platformy Azure. W centrum umożliwia również łączność za pośrednictwem sieci VPN lub ExpressRoute zgodnie z wymaganiami.

[**Sieci wirtualne**][VNet]. Koncentrator jest zazwyczaj zbudowany w sieci wirtualnej z wieloma podsieciami, aby hostować różne typy usług, które filtrują i sprawdzają ruch do lub z Internetu za pośrednictwem wystąpień urządzeń WUS, WAF i Azure Application Gateway.

[**Trasy zdefiniowane przez użytkownika**][user-defined-routes] Korzystając z tras zdefiniowanych przez użytkownika, klienci mogą wdrażać zapory, identyfikatory/adresy IP i inne urządzenia wirtualne oraz kierować ruchem sieciowym za pośrednictwem tych urządzeń zabezpieczeń w celu wymuszania, inspekcji i inspekcji zasad granicy zabezpieczeń. Trasy zdefiniowane przez użytkownika mogą być tworzone zarówno przez centrum, jak i szprychy w celu zagwarantowania, że ruch przesyłany przez określone niestandardowe maszyny wirtualne, wirtualne urządzenia sieciowe i moduły równoważenia obciążenia używane przez implementację wirtualnego centrum danych. W celu zagwarantowania, że ruch wygenerowany z maszyn wirtualnych znajdujących się w tranzycie szprych do właściwych urządzeń wirtualnych, należy ustawić trasę zdefiniowaną przez użytkownika w podsieciach szprychy, ustawiając adres IP frontonu wewnętrznego modułu równoważenia obciążenia jako Następny przeskok. Wewnętrzny moduł równoważenia obciążenia rozkłada ruch wewnętrzny na urządzenia wirtualne (pula wewnętrznej bazy danych modułu równoważenia obciążenia).

[**Zapora systemu Azure**][AzFW] to zarządzana, oparta na chmurze usługa zabezpieczeń sieci, która chroni zasoby Virtual Network platformy Azure. Jest to w pełni stanowa Zapora jako usługa z wbudowaną wysoką dostępnością i nieograniczoną skalowalnością chmury. Możesz centralnie tworzyć, wymuszać i rejestrować zasady łączności aplikacji i sieci w subskrypcjach i sieciach wirtualnych. Usługa Azure Firewall używa statycznego publicznego adresu IP do zasobów sieci wirtualnej. Umożliwia to zewnętrznym zaporom identyfikowanie ruchu pochodzącego z danej sieci wirtualnej. Usługa jest w pełni zintegrowana z usługą Azure Monitor na potrzeby rejestrowania i analiz.

[**Wirtualne urządzenia sieciowe**][NVA]. W centrum sieć obwodowa mająca dostęp do Internetu jest zazwyczaj zarządzana za pomocą wystąpienia zapory platformy Azure lub farmy zapory lub zapory aplikacji sieci Web (WAF).

Różne aplikacje biznesowe często używają wielu aplikacji internetowych. Aplikacje internetowe często mają różne luki w zabezpieczeniach i są obiektami ataków wykorzystujących te luki. Zapory aplikacji sieci Web to specjalny typ produktu służący do wykrywania ataków na aplikacje sieci Web, protokół HTTP/HTTPS, bardziej szczegółowo niż w przypadku zapory ogólnej. W porównaniu z tradycją technologii zapory sieciowi mają zestaw określonych funkcji do ochrony wewnętrznych serwerów sieci Web przed zagrożeniami.

Zapora platformy Azure lub Zapora urządzenie WUS korzystają ze wspólnej płaszczyzny administracyjnej z zestawem reguł zabezpieczeń, aby chronić obciążenia hostowane w szprychach i kontrolować dostęp do sieci lokalnych. Zapora platformy Azure ma wbudowaną skalowalność, podczas gdy zapory urządzenie WUS można ręcznie skalować za modułem równoważenia obciążenia. Ogólnie rzecz biorąc, Farma zapory ma mniej wyspecjalizowane oprogramowanie w porównaniu z WAF, ale ma szerszy zakres aplikacji do filtrowania i kontrolowania dowolnego typu ruchu wyjściowego i przychodzącego. Jeśli jest używane podejście urządzenie WUS, można je znaleźć i wdrożyć z portalu Azure Marketplace.

Użyj jednego zestawu zapór systemu Azure (lub urządzeń WUS) dla ruchu pochodzącego z Internetu, a drugi dla ruchu pochodzącego z lokalnego. Używanie tylko jednego zestawu zapór dla obu rodzajów ruchu stanowi zagrożenie dla bezpieczeństwa, ponieważ nie zapewnia obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego. Użycie osobnych warstw zapory zmniejsza złożoność sprawdzania reguł zabezpieczeń i czyści, które reguły odnoszą się do tych, które są przychodzące żądania sieciowe.

Zalecamy użycie jednego zestawu wystąpień zapory platformy Azure lub urządzeń WUS dla ruchu pochodzącego z Internetu. Użyj innego dla ruchu pochodzącego z lokalnego. Używanie tylko jednego zestawu zapór w obu przypadkach stanowi zagrożenie bezpieczeństwa, ponieważ nie zapewnia on obwodu zabezpieczeń między dwoma zestawami ruchu sieciowego. Użycie osobnych warstw zapory zmniejsza złożoność sprawdzania reguł zabezpieczeń i pozwala wyczyścić, które reguły odnoszą się do tych, które są przychodzące żądania sieciowe.

[**Azure Load Balancer**][ALB] oferuje usługę warstwy 4 (TCP, UDP) o wysokiej dostępności, która może dystrybuować ruch przychodzący między wystąpieniami usługi zdefiniowanymi w zestawie o zrównoważonym obciążeniu. Ruch wysyłany do modułu równoważenia obciążenia z punktów końcowych frontonu IP lub prywatnych punktów końcowych IP może być rozpowszechniany z lub bez translacji adresów do zestawu puli adresów IP zaplecza (przykłady to wirtualne urządzenia sieciowe lub maszyny wirtualne).

Azure Load Balancer może również sondować kondycję różnych wystąpień serwera, a gdy wystąpienie nie odpowiada na sondę, moduł równoważenia obciążenia zatrzymuje wysyłanie ruchu do wystąpienia złej kondycji. W wirtualnym centrum danych zewnętrzny moduł równoważenia obciążenia jest wdrażany w centrum i szprych. W centrum moduł równoważenia obciążenia służy do wydajnego kierowania ruchem do usług w szprychach, a moduły równoważenia obciążenia są używane do zarządzania ruchem aplikacji.

[Azure Front drzwiczks (AFD)][AFD] to wysoce dostępna i skalowalna platforma Microsoft Web Application Acceleration platform, globalne Load Balancer http, ochrona aplikacji i Content Delivery Network. W przypadku ponad 100 lokalizacji na granicy sieci globalnej firmy Microsoft AFD umożliwia tworzenie, obsługiwanie i skalowanie dynamicznej aplikacji sieci Web oraz zawartości statycznej. Usługa AFD udostępnia swoją aplikację dzięki światowej klasy wydajności użytkowników końcowych, ujednoliconej automatyzacji konserwacji/sygnatury konserwacyjnej, automatyzacji BCDR, ujednoliconej informacji o kliencie/użytkowniku, buforowaniu i usłudze Service Insights. Platforma oferuje wydajność, niezawodność i pomoc techniczną umowy SLA, certyfikaty zgodności i podlegające inspekcji praktyki bezpieczeństwa opracowane, eksploatowane i obsługiwane natywnie przez platformę Azure.

[**Application Gateway**][AppGW] Microsoft Azure Application Gateway to dedykowane urządzenie wirtualne udostępniające kontroler dostarczania aplikacji (ADC) jako usługa, oferując różne możliwości równoważenia obciążenia warstwy 7 dla aplikacji. Pozwala to zoptymalizować produktywność farmy sieci Web dzięki przeciążeniu przerwania protokołu SSL intensywnie korzystających z procesora CPU do bramy aplikacji. Zapewnia także inne możliwości routingu warstwy 7, takie jak okrężna dystrybucja ruchu przychodzącego, koligacja sesji na podstawie plików cookie, routing oparty na ścieżkach URL i możliwość hostowania wielu witryn sieci Web za pojedynczą bramą Application Gateway. Zapora aplikacji internetowych jest również udostępniana w ramach jednostki SKU zapory aplikacji internetowych w usłudze Application Gateway. Zapewnia ona ochronę aplikacji internetowych przed typowymi internetowymi lukami w zabezpieczeniach. Usługę Application Gateway można skonfigurować jako bramę umożliwiającą dostęp do Internetu, bramę tylko wewnętrzną lub jako kombinację obu tych opcji.

[**Publiczne adresy IP**][PIP]. W przypadku niektórych funkcji platformy Azure można skojarzyć punkty końcowe usługi z publicznym adresem IP, aby można było uzyskać dostęp do zasobu z Internetu. Ten punkt końcowy używa translatora adresów sieciowych (NAT) do kierowania ruchu do wewnętrznego adresu i portu w sieci wirtualnej platformy Azure. Ta ścieżka stanowi podstawową metodę przekazywania ruchu zewnętrznego do sieci wirtualnej. Można skonfigurować publiczne adresy IP, aby określić, który ruch jest przesyłany i jak i w jaki sposób i gdzie jest tłumaczony do sieci wirtualnej.

Usługa [**Azure DDoS Protection Standard**][DDoS] zapewnia dodatkowe możliwości ograniczania funkcjonalności w ramach [podstawowej warstwy usług][DDoS] , która jest dostrajana specjalnie do zasobów usługi Azure Virtual Network. Usługa DDoS Protection w warstwie Standardowa jest prosta do włączenia i nie wymaga żadnych zmian w aplikacji. Zasady ochrony są dostosowane przez dedykowane algorytmy monitorowania ruchu i uczenia maszynowego. Zasady są stosowane do publicznych adresów IP skojarzonych z zasobami wdrożonymi w sieciach wirtualnych. Do tych zasobów należą m.in. wystąpienia usług Azure Load Balancer, Azure Application Gateway i Azure Service Fabric. Dane telemetryczne w czasie rzeczywistym są dostępne za pośrednictwem widoków Azure Monitor podczas ataku i historii. Ochronę warstwy aplikacji można dodać za pomocą zapory aplikacji sieci Web platformy Azure Application Gateway. Zapewniono ochronę publicznych adresów IP platformy Azure z protokołem IPv4.

#### <a name="component-type-monitoring"></a>Typ składnika: monitorowanie

Składniki monitorowania zapewniają widoczność i alerty dotyczące wszystkich typów składników. Wszystkie zespoły powinny mieć dostęp do monitorowania dla składników i usług, do których mają dostęp. Jeśli masz scentralizowaną pomoc techniczną lub zespoły operacyjne, wymagają zintegrowanego dostępu do danych dostarczanych przez te składniki.

Platforma Azure oferuje różne typy usług rejestrowania i monitorowania, które umożliwiają śledzenie zachowania zasobów hostowanych na platformie Azure. Zarządzanie i kontrola obciążeń na platformie Azure opiera się nie tylko na zbieraniu danych dzienników, ale również o możliwości wyzwalania akcji na podstawie określonych zgłoszonych zdarzeń.

[**Azure monitor**][Monitor]. Platforma Azure obejmuje wiele usług, które indywidualnie wykonują określoną rolę lub zadanie w obszarze monitorowania. Razem usługi te zapewniają kompleksowe rozwiązanie umożliwiające zbieranie, analizowanie oraz działanie na podstawie danych telemetrycznych z aplikacji użytkownika oraz zasobów platformy Azure, które je obsługują. Mogą one również służyć do monitorowania krytycznych zasobów lokalnych, aby zapewnić hybrydowe środowisko monitorowania. Zapoznanie się z dostępnymi narzędziami i danymi stanowi pierwszy etap tworzenia pełnej strategii monitorowania aplikacji.

Istnieją dwa główne typy dzienników na platformie Azure:

- [Dziennik aktywności platformy Azure][ActLog], zwany wcześniej **dziennikami operacyjnymi**, zawiera szczegółowe informacje o operacjach wykonywanych na zasobach w ramach subskrypcji platformy Azure. Te dzienniki raportują zdarzenia płaszczyzny kontroli dla subskrypcji. Każdy zasób platformy Azure tworzy dzienniki inspekcji.

- [Dzienniki diagnostyczne Azure monitor][DiagLog] są dziennikami generowanymi przez zasób, który zapewnia rozbudowane i częste dane dotyczące operacji tego zasobu. Zawartość tych dzienników różni się w zależności od typu zasobu.

![9][9]

Ważne jest, aby śledzić dzienniki dla sieciowych grup zabezpieczeń, szczególnie te informacje:

- [Dzienniki zdarzeń][nsg-log] zawierają informacje dotyczące zasad sieciowych grup zabezpieczeń stosowanych do maszyn wirtualnych i ról wystąpień opartych na adresie Mac.
- [Dzienniki liczników][nsg-log] śledzą, ile razy reguła sieciowych grup zabezpieczeń została uruchomiona w celu odmowy lub zezwolenia na ruch.

Wszystkie dzienniki mogą być przechowywane na kontach usługi Azure Storage na potrzeby inspekcji, statycznej analizy lub tworzenia kopii zapasowych. W przypadku przechowywania dzienników na koncie usługi Azure Storage klienci mogą używać różnych typów platform do pobierania, przygotowywania, analizowania i wizualizacji tych danych w celu zgłaszania stanu i kondycji zasobów w chmurze.

Duże przedsiębiorstwa powinny już uzyskać standardową strukturę monitorowania systemów lokalnych. Mogą one stanowić rozszerzoną strukturę do integrowania dzienników generowanych przez wdrożenia w chmurze. Korzystając z [usługi Azure log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-queries), organizacje mogą zachować wszystkie rejestracje w chmurze. Log Analytics jest zaimplementowana jako usługa oparta na chmurze. Dzięki temu możesz szybko korzystać z minimalnej inwestycji w usługi infrastruktury. Log Analytics integruje się także ze składnikami programu System Center, takimi jak System Center Operations Manager, aby zwiększyć istniejące inwestycje zarządzania do chmury.

Log Analytics to usługa platformy Azure, która ułatwia zbieranie, skorelowanie, wyszukiwanie i wykonywanie działań związanych z danymi dzienników i wydajności generowanymi przez systemy operacyjne, aplikacje i składniki w chmurze infrastruktury. Zapewnia ona klientom informacje operacyjne w czasie rzeczywistym przy użyciu zintegrowanego wyszukiwania i niestandardowych pulpitów nawigacyjnych w celu przeanalizowania wszystkich rekordów we wszystkich obciążeniach w ramach implementacji wirtualnego centrum danych.

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

Rozwiązanie [Network Performance Monitor][NPM] wewnątrz pakietu Operations Management Suite może zapewnić kompleksowe informacje o sieci. Te informacje obejmują pojedynczy widok sieci platformy Azure i sieci lokalnych. Rozwiązanie ma określone monitory dla usług ExpressRoute i publicznych.

#### <a name="component-type-workloads"></a>Typ składnika: obciążenia

Składniki obciążenia to miejsce, w którym znajdują się rzeczywiste aplikacje i usługi. Jest to również sytuacja, w której zespoły deweloperów aplikacji spędzają najwięcej czasu.

Możliwości obciążeń są nieograniczone. Poniżej przedstawiono zaledwie kilka możliwych typów obciążeń:

**Wewnętrzne aplikacje LOB:** Aplikacje biznesowe to aplikacje komputerowe krytyczne dla trwającej operacji przedsiębiorstwa. Aplikacje LOB mają pewne typowe cechy:

- **Interaktywny według natury:** Wprowadzono dane i są zwracane wyniki lub raporty.
- **Oparte na danych:** Obciążenia intensywnie korzystające z danych z częstego dostępu do baz danych lub innych magazynów.
- **Zintegrowane:** Obciążenia zapewniające integrację z innymi systemami w organizacji lub poza nią.

**Witryny sieci Web, które są dostępne dla klientów (Internet lub wewnętrzny):** Większość aplikacji, które współdziałają z Internetem, to witryny sieci Web. Platforma Azure oferuje możliwość uruchamiania witryny sieci Web na maszynie wirtualnej IaaS lub witrynie [Azure Web Apps][WebApps] site (PaaS). Usługa Azure Web Apps obsługuje integrację z usługą sieci wirtualnych, która pozwala na wdrożenie Web Apps w strefie sieci szprych. Wewnętrzne witryny sieci Web nie muszą ujawniać publicznego punktu końcowego, ponieważ zasoby są dostępne za pośrednictwem prywatnych adresów IP bez obsługi routingu z prywatnej sieci wirtualnej.

**Dane Big Data i analiza:** Gdy dane wymagają skalowania w górę do dużego woluminu, bazy danych mogą nie skalować się prawidłowo. Technologia Hadoop oferuje system do równoległego uruchamiania zapytań rozproszonych na dużej liczbie węzłów. Klienci mają możliwość uruchamiania obciążeń danych w maszynach wirtualnych IaaS lub PaaS ([HDInsight][HDI]). Usługa HDInsight obsługuje wdrażanie w sieci wirtualnej opartej na lokalizacji, ale można ją wdrożyć w klastrze w szprychie wirtualnego centrum danych.

**Zdarzenia i komunikaty:** usługa [Azure Event Hubs][EventHubs] jest usługą pozyskiwania danych telemetrycznych w skali, która gromadzi, przekształca i przechowuje miliony zdarzeń. Usługa Distributed Streaming platform oferuje niewielkie opóźnienia i możliwość konfigurowania czasu przechowywania, dzięki czemu można pozyskiwanie ogromnych ilości danych telemetrycznych na platformie Azure i odczytywać te dane z wielu aplikacji. Przy Event Hubs pojedynczy strumień może obsługiwać zarówno potoki w czasie rzeczywistym, jak i oparte na partiach.

Możesz zaimplementować wysoce niezawodną usługę do obsługi komunikatów w chmurze między aplikacjami i usługami za pomocą [Azure Service Bus][ServiceBus]. Oferuje asynchroniczne komunikaty obsługiwane przez brokera między klientem i serwerem, strukturalną funkcją pierwszej pierwszej wyewidencjonowywania (FIFO) oraz możliwościami publikowania i subskrybowania.

![10][10]

### <a name="make-a-virtual-datacenter-highly-available-multiple-virtual-datacenters"></a>Zapewnienie wysokiej dostępności wirtualnego centrum danych: wiele wirtualnych centrów danych

Do tej pory ten artykuł koncentruje się na projektowaniu jednego wirtualnego centrum danych, opisującym podstawowe składniki i architekturę, która przyczynia się do odporności. Funkcje platformy Azure, takie jak Azure load module, urządzeń WUS, zestawy dostępności, zestawy skalowania, oraz inne mechanizmy przyczyniają się do systemu, który umożliwia tworzenie stałych poziomów umów SLA w usługach produkcyjnych.

Jednak ze względu na to, że pojedyncze wirtualne centrum danych jest zwykle implementowane w ramach jednego regionu, może być narażony na wszystkie poważne awarie, które mają wpływ na cały region. Klienci wymagający wysokiego umowy SLA muszą chronić usługi przez wdrożenia tego samego projektu w dwóch (lub więcej) wirtualnych implementacjach centrów danych umieszczonych w różnych regionach.

Oprócz zagadnień związanych z umową SLA istnieje kilka typowych scenariuszy, w których wdrożenie wielu wirtualnych implementacji centrum danych ma sens:

- Obecność regionalna lub globalna.
- Odzyskiwanie sprawności systemu po awarii.
- Mechanizm do przekierowywania ruchu między centrami danych.

#### <a name="regionalglobal-presence"></a>Obecność regionalna/globalna

Centra danych platformy Azure znajdują się w wielu regionach na całym świecie. W przypadku wybrania wielu centrów danych platformy Azure klienci muszą rozważyć dwa powiązane czynniki: odległości geograficzne i opóźnienie. Aby zaoferować najlepsze środowisko użytkownika, należy oszacować odległość geograficzną między każdą implementacją wirtualnego centrum danych a także odległość między każdą wirtualną implementacją centrum danych i użytkownikami końcowymi.

Region, w którym są hostowane wirtualne implementacje centrów danych, musi być zgodny z wymaganiami prawnymi obowiązującymi przez daną organizację.

#### <a name="disaster-recovery"></a>Odzyskiwanie po awarii

Projekt planu odzyskiwania po awarii zależy od typów obciążeń i możliwości synchronizowania stanu tych obciążeń między różnymi implementacjami wirtualnych centrów danych. W idealnym przypadku większość klientów chce szybko przejść do trybu pracy awaryjnej i może wymagać synchronizacji danych aplikacji między wdrożeniami z wieloma wirtualnymi implementacjami centrum danych. Jednak podczas projektowania planów odzyskiwania po awarii należy wziąć pod uwagę, że większość aplikacji jest wrażliwa na opóźnienia, które może być spowodowane tą synchronizacją danych.

Synchronizacja i monitorowanie pulsu aplikacji w różnych wirtualnych implementacjach centrów danych wymaga ich komunikacji za pośrednictwem sieci. Dwie implementacje w różnych regionach mogą być połączone przez:

- Komunikacja równorzędna sieci wirtualnych — wirtualne sieci równorzędne mogą łączyć centra w różnych regionach.
- ExpressRoute prywatną komunikację równorzędną, gdy centra w każdej wirtualnej implementacji centrum danych są połączone z tym samym obwodem ExpressRoute.
- Wiele obwodów usługi ExpressRoute połączonych za pośrednictwem sieci szkieletowej firmy i wielu wirtualnych implementacji centrów danych połączonych z obwodami ExpressRoute.
- Połączenia sieci VPN typu lokacja-lokacja między strefą centrum wirtualnych wdrożeń centrów w każdym regionie świadczenia usługi Azure.

Typowa Komunikacja równorzędna sieci wirtualnych lub połączeń ExpressRoute jest preferowanym typem łączności sieciowej ze względu na wyższą przepustowość i spójne poziomy opóźnienia podczas przesyłania danych za pośrednictwem szkieletu firmy Microsoft.

Zalecamy, aby klienci uruchamiali testy kwalifikacji sieci w celu sprawdzenia opóźnienia i przepustowości tych połączeń, a także zdecydować, czy synchroniczna lub asynchroniczna replikacja danych jest odpowiednia w oparciu o wynik. Ważne jest również, aby zważyć te wyniki w widoku optymalnego celu czasu odzyskiwania (RTO).

#### <a name="disaster-recovery-diverting-traffic-from-one-region-to-another"></a>Odzyskiwanie po awarii: przekierowywanie ruchu z jednego regionu do innego

Usługa [Azure Traffic Manager][traffic-manager] okresowo sprawdza kondycję usługi publicznych punktów końcowych w różnych wirtualnych implementacjach centrów danych, a jeśli te punkty końcowe nie powiodą się, automatycznie kieruje do pomocniczego wirtualnego centrum danych przy użyciu systemu nazw domen ( DNS).

Ponieważ używa usługi DNS, Traffic Manager jest tylko do użytku z publicznymi punktami końcowymi platformy Azure. Usługa jest zwykle używana do kontrolowania lub przekierowywania ruchu do maszyn wirtualnych platformy Azure i Web Apps w dobrej kondycji w przypadku implementacji wirtualnego centrum danych. Traffic Manager jest odporny nawet w przypadku awarii całego regionu platformy Azure i może kontrolować dystrybucję ruchu użytkowników dla punktów końcowych usługi w różnych wirtualnych centrach danych na podstawie kilku kryteriów. Na przykład awaria usługi w określonej wirtualnej implementacji centrum danych lub wybranie implementacji wirtualnego centrum danych z najniższym opóźnieniem sieci.

### <a name="summary"></a>Podsumowanie

Wirtualne centrum danych to podejście do migracji centrów danych w celu utworzenia skalowalnej architektury platformy Azure, która maksymalizuje użycie zasobów w chmurze, zmniejsza koszty i upraszcza zarządzanie systemem. Wirtualne centrum danych jest oparte na topologii sieci gwiazdy, zapewniającej wspólne usługi udostępnione w centrum i zezwalającej na określone aplikacje i obciążenia w szprychach. Wirtualne centrum danych jest również zgodne ze strukturą ról firmy, w której różne działy, takie jak centralne IT, DevOps i Operations and Maintenance, działają razem podczas wykonywania ich określonych ról. Wirtualne centrum danych spełnia wymagania związane z przełączaniem i przenoszeniem zmian, ale również ma wiele zalet do natywnych wdrożeń w chmurze.

## <a name="references"></a>Informacje

W tym dokumencie omówiono następujące funkcje. Postępuj zgodnie z linkami, aby dowiedzieć się więcej.

<!-- markdownlint-disable MD033 -->

|Funkcje sieciowe|Równoważenie obciążenia|Łączność|
|-|-|-|
|[Sieci wirtualne platformy Azure][VNet]</br>[Sieciowe grupy zabezpieczeń][network-security-groups]</br>[Dzienniki sieciowych grup zabezpieczeń][nsg-log]</br>[Trasy zdefiniowane przez użytkownika][user-defined-routes]</br>[Wirtualne urządzenia sieciowe][NVA]</br>[Publiczne adresy IP][PIP]</br>[Azure DDoS][DDoS]</br>[Azure Firewall][AzFW]</br>[System DNS platformy Azure][DNS]|[Azure Front Door][AFD]</br>[Azure Load Balancer (L3)][ALB]</br>[Application Gateway (P7)][AppGW]</br>[Zapora aplikacji sieci Web] WAF</br>[Azure Traffic Manager][traffic-manager]</br></br></br></br></br> |[Komunikacja równorzędna sieci wirtualnych][VNetPeering]</br>[Wirtualna sieć prywatna][VPN]</br>[Wirtualna sieć WAN][vWAN]</br>[ExpressRoute][ExR]</br>[ExpressRoute bezpośrednie][ExRD]</br></br></br></br></br>

|Tożsamość</br>|Monitorowanie</br>|Najlepsze rozwiązania</br>|
|-|-|-|
|[Azure Active Directory][azure-ad]</br>[Multi-Factor Authentication][multi-factor-authentication]</br>[Podstawowe funkcje kontroli dostępu][RBAC]</br>[Domyślne role usługi Azure AD][Roles]</br></br></br> |[Network Watcher][NetWatch]</br>[Azure Monitor][Monitor]</br>[Dzienniki aktywności][ActLog]</br>[Dzienniki diagnostyczne][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br>[Monitor wydajności sieci][NPM]|[Najlepsze rozwiązania dotyczące sieci obwodowej][DMZ]</br>[Zarządzanie subskrypcjami][SubMgmt]</br>[Zarządzanie grupami zasobów][RGMgmt]</br>[Limity subskrypcji platformy Azure][limits] </br></br></br>|

|Inne usługi platformy Azure|
|-|
|[Azure Web Apps][WebApps]</br>[HDInsight (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

- Eksplorowanie [komunikacji równorzędnej sieci][VNetPeering]wirtualnych, nieprzypinanie technologii dla projektów gwiazdy i gwiazdy.
- Zaimplementuj [usługę Azure AD][azure-ad] , aby rozpocząć pracę z eksploracją [RBAC][RBAC] .
- Opracowuj model zarządzania subskrypcjami i zasobami oraz model RBAC, aby zaspokoić strukturę, wymagania i zasady organizacji. Planowanie najważniejszych działań. Tak jak to praktycznie, Zaplanuj reorganizacja, fuzje, nowe linie produktów i inne zagadnienia.

<!-- images -->

[0]: ../_images/vdc/networking-redundant-equipment.png "Przykłady nakładania się składników"
[1]: ../_images/vdc/networking-vdc-high-level.png "Przykład wysokiego poziomu koncentratora i satelity w implementacji wirtualnego centrum danych"
[2]: ../_images/vdc/networking-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ../_images/vdc/networking-spoke-to-spoke.png "Szprycha do szprychy"
[4]: ../_images/vdc/networking-vdc-block-level-diagram.png "Diagram poziomu blokowego dla implementacji wirtualnego centrum danych"
[5]: ../_images/vdc/networking-users-groups-subscriptions.png "Użytkownicy, grupy, subskrypcje i projekty"
[6]: ../_images/vdc/networking-infrastructure-high-level.png "Diagram infrastruktury wysokiego poziomu"
[7]: ../_images/vdc/networking-high-level-perimeter-networks.png "Diagram infrastruktury wysokiego poziomu"
[8]: ../_images/vdc/networking-vnet-peering-perimeter-networks.png "Wirtualne sieci równorzędne i sieci obwodowe"
[9]: ../_images/vdc/networking-high-level-diagram-monitoring.png "Ogólny diagram dla monitorowania"
[10]: ../_images/vdc/networking-high-level-workloads.png "Diagram wysokiego poziomu na potrzeby obciążenia"

<!-- links -->

[limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/role-based-access-control/built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[network-security-groups]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg
[DNS]: https://docs.microsoft.com/azure/dns/dns-overview
[PrivateDNS]: https://docs.microsoft.com/azure/dns/private-dns-overview
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview
[user-defined-routes]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview
[RBAC]: https://docs.microsoft.com/azure/role-based-access-control/overview
[multi-factor-authentication]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[azure-ad]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction
[ExRD]: https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about
[vWAN]: https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[AzFW]: https://docs.microsoft.com/azure/firewall/overview
[SubMgmt]: /azure/architecture/cloud-adoption/appendix/azure-scaffold
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
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
