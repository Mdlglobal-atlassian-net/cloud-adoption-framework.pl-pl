---
title: Najlepsze rozwiązania dla przedsiębiorstw przechodzących na platformę Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Opisuje szkielet używany przez przedsiębiorstwa do zapewnienia bezpiecznego i możliwego do zarządzania środowiskiem.
author: rdendtler
ms.author: rodend
ms.date: 09/22/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: 2e605766e06b106fab61576e64bd5059569c8b38
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548768"
---
# <a name="azure-enterprise-scaffold-prescriptive-subscription-governance"></a>Szkielet platformy Azure dla przedsiębiorstw: zalecenia dotyczące zarządzania subskrypcjami

> [!NOTE]
> Tworzenie szkieletu przedsiębiorstwa platformy Azure zostało zintegrowane z platformą wdrażania Microsoft Cloud. Zawartość tego artykułu jest teraz reprezentowana w sekcji [gotowych](../ready/index.md) nowej struktury. Ten artykuł zostanie uznany za przestarzały na początku 2020. Aby rozpocząć korzystanie z nowego procesu, zapoznaj się z tematem [gotowym do omówienia](../ready/index.md), [tworzeniu pierwszej strefy docelowej](../ready/azure-setup-guide/migration-landing-zone.md)i/lub [zagadnieniami dotyczącymi strefy docelowej](../ready/considerations/index.md).

Przedsiębiorstwa coraz częściej wdrażają chmurę publiczną pod kątem elastyczności i elastyczność. Są one zależne od siły chmury w celu generowania przychodów i optymalizowania użycia zasobów dla firmy. Microsoft Azure zapewnia wiele usług i możliwości, które przedsiębiorstwa tworzą, takie jak bloki konstrukcyjne, aby zająć szeroką gamę obciążeń i aplikacji.

Wybór Microsoft Azure jest tylko pierwszym krokiem do osiągnięcia korzyści z chmury. Drugim krokiem jest zrozumienie, w jaki sposób przedsiębiorstwo może efektywnie korzystać z platformy Azure i identyfikować możliwości linii bazowej, które muszą być stosowane w celu uzyskania odpowiedzi na pytania, takie jak:

- "Interesuje mnie o suwerenności danych; Jak upewnić się, że moje dane i systemy spełniają nasze wymagania prawne? ".
- "Jak mogę wiedzieć, co jest obsługiwane przez każdy zasób, aby można było z nim z niego odnosić i rozliczać?"
- "Chcę, aby upewnić się, że wszystko, co jest wdrażane lub w chmurze publicznej, zaczyna się od sposób myślenia zabezpieczeń, jak mogę pomóc w uproszczeniu?"

Prospektem pustej subskrypcji bez guardrails jest zniechęcające. Puste miejsce może utrudniać przejście na platformę Azure.

Ten artykuł zawiera punkt wyjścia dla specjalistów technicznych w celu rozwiązania potrzeby nadzoru i zrównoważenia go z potrzebą elastyczności. Wprowadza koncepcję szkieletu przedsiębiorstwa, która prowadzi do zapewnienia bezpieczeństwa w zakresie wdrażania i zarządzania środowiskami platformy Azure w bezpieczny sposób. Zapewnia ona strukturę służącą do tworzenia skutecznych i wydajnych kontroli.

## <a name="need-for-governance"></a>Potrzeba dla ładu

Podczas przejścia na platformę Azure należy zająć się zagadnieniem Nadzoru wczesnego, aby zapewnić pomyślne korzystanie z chmury w przedsiębiorstwie. Niestety, czas i Bureaucracy tworzenia kompleksowego systemu zarządzania oznacza, że niektóre grupy biznesowe bezpośrednio przechodzą do dostawców, bez konieczności od przedsiębiorstwa. Takie podejście może spowodować, że otwarty w przedsiębiorstwie nie zostanie naruszony, jeśli zasoby nie są prawidłowo zarządzane. Charakterystyka &mdash;agility chmury publicznej, elastyczności i cen opartych na użyciu &mdash;are ważnych dla grup gospodarczych, które muszą szybko spełnić wymagania klientów (zarówno wewnętrznych, jak i zewnętrznych). Jednak przedsiębiorstwo musi zapewnić skuteczną ochronę danych i systemów.

Podczas tworzenia budynku tworzenie szkieletu jest używane do tworzenia podstawy struktury. Szkielet jest przewodnikiem ogólnym i zawiera punkty zakotwiczenia umożliwiające zamontowanie systemów trwałych. Szkielet przedsiębiorstwa jest taki sam: Zestaw elastycznych kontrolek i możliwości platformy Azure, które zapewniają strukturę środowiska oraz kotwice dla usług skompilowanych w chmurze publicznej. Zapewnia ona konstruktorom (grupom IT i biznesowym) podstawę do tworzenia i dołączania nowych usług w celu zapewnienia szybszego dostarczania.

Szkielet jest oparty na praktykach, które zostały zebrane z wielu zakontraktowań z klientami o różnej wielkości. Ci klienci mają od małych organizacji tworzenie rozwiązań w chmurze w dużych przedsiębiorstwach wielonarodowych i niezależnych dostawców oprogramowania, którzy przeprowadzają migrację obciążeń i opracowują rozwiązania natywne w chmurze. Tworzenie szkieletu przedsiębiorstwa jest elastyczne w celu zapewnienia obsługi tradycyjnych obciążeń IT i obciążeń Agile, takich jak deweloperzy tworzący aplikacje oprogramowania jako usługi (SaaS) na podstawie możliwości platformy Azure.

Szkielet przedsiębiorstwa jest przeznaczony do podstaw każdej nowej subskrypcji na platformie Azure. Dzięki temu administratorzy mogą zapewnić, że obciążenia spełniają minimalne wymagania dotyczące ładu organizacji, bez uniemożliwiania użytkownikom i deweloperom szybkiego zaspokajania ich celów. Nasze doświadczenie pokazuje, że te duże szybkości, a nie utrudniają rozwój chmury publicznej.

> [!NOTE]
> Firma Microsoft udostępniła w wersji zapoznawczej nową funkcję o nazwie [plany platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/overview) , która umożliwi spakowanie i wdrażanie popularnych obrazów, szablonów, zasad i skryptów w ramach subskrypcji i grup zarządzania oraz zarządzanie nimi. Ta funkcja jest mostkiem między celem szkieletu a modelem referencyjnym i wdrażaniem tego modelu w organizacji.
>
Na poniższej ilustracji przedstawiono składniki szkieletu. Podstawą jest plan jednolity dla hierarchii zarządzania i subskrypcji. Filary składają się z zasad Menedżer zasobów i silnych standardów nazewnictwa. Pozostała część szkieletu to podstawowe funkcje i funkcje platformy Azure, które umożliwiają i łączą bezpieczne i możliwe do zarządzania środowisko.

![Szkielet przedsiębiorstwa](../_images/reference/scaffoldv2.png)

## <a name="define-your-hierarchy"></a>Definiowanie hierarchii

Podstawą szkieletu jest hierarchia i relacja rejestracji w przedsiębiorstwie platformy Azure w ramach subskrypcji i grup zasobów. Rejestracja w przedsiębiorstwie definiuje kształt i użycie usług platformy Azure w ramach Twojej firmy z punktu widzenia umowy. W ramach Umowa Enterprise można dodatkowo podzielić środowisko na działy, konta, subskrypcje i grupy zasobów, aby pasowały do struktury organizacji.

![hierarchia](../_images/reference/agreement.png)

Subskrypcja platformy Azure to podstawowa jednostka, w której znajdują się wszystkie zasoby. Definiuje również kilka limitów w ramach platformy Azure, takich jak liczba rdzeni, sieci wirtualne i inne zasoby. Grupy zasobów służą do dokładniejszego uściślenia modelu subskrypcji i zapewnienia bardziej naturalnej grupy zasobów.

Każde przedsiębiorstwo jest inne, a hierarchia w powyższym obrazie umożliwia znaczną elastyczność w zakresie organizowania platformy Azure w firmie. Modelowanie hierarchii w taki sposób, aby odzwierciedlały rozliczenia firmy, zarządzanie zasobami i zapotrzebowanie na dostęp do zasobów, jest pierwszą i największą decyzją podejmowaną podczas uruchamiania w chmurze publicznej.

### <a name="departments-and-accounts"></a>Działy i konta

Trzy typowe wzorce rejestracji platformy Azure to:

- Wzorzec **funkcjonalny** :

  ![Wzorzec funkcjonalny](../_images/reference/functional.png)

- Wzorzec **jednostki biznesowej** :

  ![Wzorzec jednostki biznesowej](../_images/reference/business.png)

- Wzorzec **geograficzny** :

  ![Wzorzec geograficzny](../_images/reference/geographic.png)

Chociaż każdy z tych wzorców ma swoje miejsce, wzorzec **jednostki biznesowej** jest coraz większy, aby można było modelować model kosztów organizacji, a także odzwierciedlać zakres kontroli. Firma Microsoft Core i Grupa operacji stworzyły efektywny podzestaw wzorca **jednostki biznesowej** modeluje się w **federalnym**, **stanowym**i **lokalnym**. Aby uzyskać więcej informacji, zobacz [organizowanie subskrypcji i grup zasobów w przedsiębiorstwie](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

### <a name="azure-management-groups"></a>Grupy zarządzania platformy Azure

Firma Microsoft oferuje teraz inny sposób modelowania hierarchii: [grupy zarządzania platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview). Grupy zarządzania są znacznie bardziej elastyczne niż działy i konta i mogą być zagnieżdżane do sześciu poziomów. Grupy zarządzania pozwalają utworzyć hierarchię, która jest oddzielona od hierarchii rozliczeń, wyłącznie w celu wydajnego zarządzania zasobami. Grupy zarządzania mogą dublować hierarchie rozliczeń i często zaczynają się one w ten sposób. Jednak możliwości grup zarządzania są używane do modelowania organizacji, grupowania powiązanych subskrypcji (niezależnie od ich lokalizacji w hierarchii rozliczeń) i przypisywania wspólnych ról, zasad i inicjatyw. Oto niektóre przykłady:

- **Produkcja a nieprodukcja.** Niektóre przedsiębiorstwa tworzą grupy zarządzania, aby identyfikować ich subskrypcje produkcyjne i nieprodukcyjne. Grupy zarządzania jeszcze bardziej ułatwiają tym klientom zarządzanie rolami i zasadami. Na przykład subskrypcja nieprodukcyjnego może pozwolić deweloperom na dostęp współautorów, ale w środowisku produkcyjnym ma tylko dostęp do czytnika.
- **Usługi wewnętrzne a usługi zewnętrzne.** Przedsiębiorstwa często mają różne wymagania, zasady i role dla usług wewnętrznych i usług przeznaczonych dla klientów.

Dobrze zaprojektowane grupy zarządzania to między innymi Azure Policy i inicjatywy — szkielet wydajnego zarządzania platformą Azure.

### <a name="subscriptions"></a>Subskrypcje

Podczas decydowania o działach i kontach (lub grupach zarządzania) przede wszystkim przeglądasz, jak podział środowiska platformy Azure jest zgodny z organizacją. Subskrypcje są jednak wykonywane w rzeczywistości, a decyzje mają wpływ na bezpieczeństwo, skalowalność i rozliczenia. Wiele organizacji Przyjrzyj następujące wzorce jako przewodniki:

- **Aplikacja/usługa:** Subskrypcje reprezentują aplikację lub usługę (portfolio aplikacji)
- **Cykl życia:** Subskrypcje reprezentują cykl życia usługi, na przykład produkcyjne lub deweloperskie.
- **Dział:** Subskrypcje reprezentują działy w organizacji.

Dwa pierwsze wzorce są najczęściej używane i obie są zdecydowanie zalecane. Podejście do cyklu życia jest odpowiednie dla większości organizacji. W takim przypadku generalnym zaleceniem jest użycie dwóch podstawowych subskrypcji, `Production` i `Nonproduction`, a następnie użycie grup zasobów w celu dodatkowego rozdzielenia środowiska.

### <a name="resource-groups"></a>Grupy zasobów

Azure Resource Manager umożliwia umieszczenie zasobów w zrozumiałych grupach do zarządzania, rozliczeń lub naturalnej koligacji. Grupy zasobów to kontenery zasobów ze wspólnym cyklem życia lub mające taki atrybut, jak "wszystkie serwery SQL" lub "aplikacja A".

Grup zasobów nie można zagnieżdżać, a zasoby mogą należeć tylko do jednej grupy zasobów. Niektóre akcje mogą działać na wszystkie zasoby w grupie zasobów. Na przykład usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów. Podobnie jak w przypadku subskrypcji, istnieją typowe wzorce podczas tworzenia grup zasobów i różnią się od "tradycyjnych IT" obciążeń do "Agile IT":

- "Tradycyjne IT" są najczęściej pogrupowane według elementów w ramach tego samego cyklu życia, takich jak aplikacja. Grupowanie według aplikacji umożliwia zarządzanie poszczególnymi aplikacjami.
- "Agile IT" pozwala skupić się na zewnętrznych aplikacjach w chmurze dostępnych dla klientów. Grupy zasobów często odzwierciedlają warstwy wdrożenia (takie jak warstwa sieci Web lub warstwa aplikacji) i zarządzanie nimi.

> [!NOTE]
> Zrozumienie obciążenia ułatwia tworzenie strategii grupy zasobów. Wzorce te mogą być mieszane i dopasowywane. Na przykład grupa zasobów usługi udostępnionej w tej samej subskrypcji co grupy zasobów "Agile".

## <a name="naming-standards"></a>Standardy nazewnictwa

Pierwszy filar szkieletu jest spójnym standardem nazewnictwa. Dobrze zaprojektowane standardy nazewnictwa umożliwiają identyfikowanie zasobów w portalu, na rachunku i w skryptach. Istnieje już istniejące standardy nazewnictwa infrastruktury lokalnej. Podczas dodawania platformy Azure do środowiska należy rozszerzyć te standardy nazewnictwa na zasoby platformy Azure.

> [!TIP]
> W przypadku konwencji nazewnictwa:
>
> - Zapoznaj się ze [wskazówkami dotyczącymi wzorców i rozwiązań](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions), a następnie stosuj je w miarę możliwości. Te wskazówki ułatwiają decydowanie o zrozumiałym standardzie nazewnictwa i zawiera obszerne przykłady.
> - Korzystanie z zasad Menedżer zasobów w celu wymuszania standardów nazewnictwa.
>
> Należy pamiętać, że trudno zmienić nazwy w późniejszym czasie, więc kilka minut będzie teraz zaoszczędzić problemy później.

Należy skoncentrować się na tych zasobach, które są najczęściej używane i wyszukiwane. Na przykład wszystkie grupy zasobów powinny być zgodne ze silnym standardem dla przejrzystości.

### <a name="resource-tags"></a>Tagi zasobów

Tagi zasobów są ściśle wyrównane ze standardami nazewnictwa. Gdy zasoby są dodawane do subskrypcji, coraz bardziej ważne jest ich logiczne klasyfikowanie na potrzeby rozliczeń, zarządzania i celów operacyjnych. Aby uzyskać więcej informacji, zobacz [Używanie tagów do organizowania zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

> [!IMPORTANT]
> Tagi mogą zawierać dane osobowe i mogą być objęte przepisami Rodo. Uważnie Zaplanuj zarządzanie tagami. Jeśli szukasz ogólnych informacji o Rodo, zobacz sekcję Rodo w [portalu zaufania usługi](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Tagi są używane na wiele sposobów poza rozliczeniami i zarządzaniem. Są one często używane jako część automatyzacji (zobacz sekcję w dalszej części). Może to spowodować konflikty, jeśli nie są one rozpatrywane na początku. Najlepszym rozwiązaniem jest zidentyfikowanie wszystkich typowych tagów na poziomie przedsiębiorstwa (na przykład ApplicationOwner i CostCenter) i ich spójność podczas wdrażania zasobów przy użyciu automatyzacji.

## <a name="azure-policy-and-initiatives"></a>Azure Policy i inicjatywy

Drugi filar szkieletu polega na używaniu [Azure Policy i inicjatyw](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction) do zarządzania ryzykiem przez Wymuszanie reguł (z efektami) w ramach zasobów i usług w Twoich subskrypcjach. Inicjatywy platformy Azure to kolekcje zasad, które są przeznaczone do osiągnięcia jednego celu. Zasady i inicjatywy są następnie przypisywane do zakresu zasobów, aby rozpocząć wymuszanie tych zasad.

Zasady i inicjatywy są jeszcze bardziej zaawansowane, gdy są używane z wymienionymi wcześniej grupami zarządzania. Grupy zarządzania umożliwiają przypisanie inicjatywy lub zasad do całego zestawu subskrypcji.

### <a name="common-uses-of-resource-manager-policies"></a>Typowe zastosowania zasad Menedżer zasobów

Zasady i inicjatywy to zaawansowane narzędzie dostępne w zestawie narzędzi platformy Azure. Zasady umożliwiają firmom zapewnienie kontroli nad obciążeniami "tradycyjnym", które pozwalają na stabilność, która jest wymagana w przypadku aplikacji biznesowych, a także umożliwianie "Agile" obciążeń &mdash;for przykład, opracowywanie aplikacji klienta bez ujawnienie przedsiębiorstwa do dodatkowego ryzyka. Najczęstsze wzorce dla zasad są następujące:

- **Zgodność geograficzna i niezależność danych.** Platforma Azure oferuje coraz większą listę regionów na całym świecie. Przedsiębiorstwa często muszą zapewnić, że zasoby w określonym zakresie pozostają w regionie geograficznym, aby spełnić wymagania prawne.
- **Unikaj ujawniania serwerów publicznie.** Azure Policy może zabronić wdrożenia niektórych typów zasobów. Często należy utworzyć zasady, aby odmówić tworzenia publicznego adresu IP w określonym zakresie, co pozwala uniknąć niezamierzonego narażenia serwera z Internetem.
- **Zarządzanie kosztami i metadane.** Tagi zasobów są często używane do dodawania ważnych danych rozliczeń do zasobów i grup zasobów, takich jak CostCenter, Owner i innych. Te Tagi są niecenne do dokładnego rozliczania i zarządzania zasobami. Zasady mogą wymuszać stosowanie tagów zasobów do wszystkich wdrożonych zasobów, ułatwiając zarządzanie nimi.

### <a name="common-uses-of-initiatives"></a>Typowe zastosowania inicjatyw

Inicjatywy zapewniają przedsiębiorstwom możliwość grupowania zasad logicznych i śledzenia ich jako pojedynczej jednostki. Inicjatywy te pomagają przedsiębiorstwom zaspokajać potrzeby zarówno Agile, jak i tradycyjnych obciążeń. Typowe zastosowania inicjatyw obejmują:

- **Włącz monitorowanie w Azure Security Center.** Jest to domyślna inicjatywa w Azure Policy i świetny przykład działań. Umożliwia ona korzystanie z zasad identyfikujących nieszyfrowane bazy danych SQL, luki w zabezpieczeniach maszyn wirtualnych i bardziej typowe potrzeby związane z zabezpieczeniami.
- **Inicjatywa specyficzna dla przepisów prawnych.** Przedsiębiorstwa często grupują zasady wspólne do wymagań prawnych (takich jak HIPAA), dzięki czemu kontrolki i zgodności do tych kontrolek są efektywnie śledzone.
- **Typy zasobów i jednostki SKU.** Utworzenie inicjatywy ograniczającej typy zasobów, które można wdrożyć, a także jednostek SKU, które można wdrożyć, może pomóc w kontroli kosztów i upewnić się, że organizacja wdraża tylko zasoby, dla których zespół dysponuje zestawem umiejętności i procedurami do obsługi.

> [!TIP]
> Zalecamy, aby zawsze używać definicji inicjatyw zamiast definicji zasad. Po przypisaniu inicjatywy do zakresu, takiego jak subskrypcja lub Grupa zarządzania, można łatwo dodać kolejne zasady do inicjatywy bez konieczności zmiany żadnych przypisań. Dzięki temu rozumiesz, co jest stosowane i co znacznie ułatwia śledzenie zgodności.

### <a name="policy-and-initiative-assignments"></a>Przypisania zasad i inicjatyw

Po utworzeniu zasad i zgrupowaniu ich w inicjatywy logiczne należy przypisać zasady do zakresu, niezależnie od tego, czy jest to grupa zarządzania, subskrypcja, czy grupa zasobów. Przypisania umożliwiają również wykluczanie podzakresu z przypisania zasad. Na przykład jeśli odmówisz tworzenia publicznych adresów IP w ramach subskrypcji, możesz utworzyć przypisanie z wykluczeniem dla grupy zasobów połączonej z chronioną strefą DMZ.

Znajdziesz kilka przykładów dotyczących zasad, które pokazują, w jaki sposób zasady i inicjatywy mogą być stosowane do różnych zasobów platformy Azure w ramach tego repozytorium [GitHub](https://github.com/Azure/azure-policy) .

## <a name="identity-and-access-management"></a>Zarządzanie tożsamościami i dostępem

Jednym z pierwszych i najbardziej najważniejszych pytań, które należy zadać, gdy rozpoczynasz pracę z chmurą publiczną, jest "kto powinien mieć dostęp do zasobów?". i "jak kontrolować ten dostęp?" Kontrolowanie dostępu do Azure Portal i zasobów w portalu ma kluczowe znaczenie dla długoterminowego bezpieczeństwa zasobów w chmurze.

Aby zabezpieczyć dostęp do zasobów, należy najpierw skonfigurować dostawcę tożsamości, a następnie skonfigurować role i dostęp. Usługa Azure Active Directory (Azure AD), połączona z lokalnym Active Directory, jest podstawą tożsamości platformy Azure. Wspomniane informacje *nie* są takie same, jak w przypadku Active Directory lokalnych, a ważne jest, aby zrozumieć, co to jest dzierżawa usługi Azure AD i jak odnosi się do rejestracji na platformie Azure. Zapoznaj się z dostępnymi [informacjami](../govern/resource-consistency/resource-access-management.md) , aby uzyskać pełną podstawę w usłudze Azure AD i Active Directory lokalnych. Aby nawiązać połączenie i zsynchronizować Active Directory z usługą Azure AD, zainstaluj i skonfiguruj [narzędzie Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) lokalnie.

![Diagram architektury usługi AD](../_images/reference/ad-architecture.png)

Po wstępnym udostępnieniu platformy Azure kontrola dostępu do subskrypcji była podstawowa: administrator lub administrator współpracujący. Dostęp do subskrypcji w modelu klasycznym implikuje dostęp do wszystkich zasobów w portalu. Ten braku szczegółowych kontroli prowadzi do rozprzestrzeniania się subskrypcji w celu zapewnienia poziomu uzasadnionej kontroli dostępu do rejestracji na platformie Azure. Ta proliferacja subskrypcji nie jest już wymagana. Za pomocą kontroli dostępu opartej na rolach (RBAC) można przypisywać użytkowników do ról standardowych, które zapewniają wspólny dostęp, taki jak "Owner", "Współautor" lub "Reader", a nawet tworzyć własne role.

W przypadku implementowania dostępu opartego na rolach należy wykonać następujące czynności:

- Kontroluj administratorów/współadministratorów subskrypcji, ponieważ te role mają rozległe uprawnienia. Aby zarządzać klasycznymi wdrożeniami platformy Azure, wystarczy dodać właściciela subskrypcji jako współadministratora.
- Grupy zarządzania umożliwiają przypisywanie [ról](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview#management-group-access) w wielu subskrypcjach i zmniejszanie obciążeń związanych z zarządzaniem nimi na poziomie subskrypcji.
- Dodaj użytkowników platformy Azure do grupy (na przykład właściciele aplikacji X) w Active Directory. Użyj zsynchronizowanej grupy, aby zapewnić członkom grupy odpowiednie prawa do zarządzania grupą zasobów zawierającą aplikację.
- Postępuj zgodnie z zasadami udzielenia **najmniejszego poziomu uprawnień** wymaganego do wykonania oczekiwanej pracy.

> [!IMPORTANT]
>Rozważ skorzystanie z usług [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure), Azure [Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted) i [dostępu warunkowego](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) , aby zapewnić lepsze zabezpieczenia i wgląd w działania administracyjne na platformie Azure opłaty. Te funkcje pochodzą z prawidłowej licencji Azure AD — wersja Premium (w zależności od funkcji) w celu dalszego zabezpieczania tożsamości i zarządzania nią. Usługa Azure AD PIM umożliwia dostęp administracyjny "just-in-Time" z przepływem pracy zatwierdzania, a także pełną inspekcję aktywacji i działań administratorów. Usługa Azure Multi-Factor Authentication jest kolejną funkcją krytyczną i umożliwia weryfikację dwuetapową logowania do Azure Portal. W połączeniu z kontrolami dostępu warunkowego można efektywnie zarządzać ryzykiem naruszenia.

Planowanie i przygotowywanie do kontroli tożsamości i dostępu oraz stosowanie najlepszych rozwiązań w zakresie zarządzania tożsamościami ([link](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices)) jest jednym z najlepszych strategii zaradczych, które można zastosować i powinny być uznawane za obowiązkowe dla każdego wdrożenia.

## <a name="security"></a>Zabezpieczenia

Jeden z największych blokad do wdrożenia w chmurze tradycyjnie ma wpływ na bezpieczeństwo. Menedżerowie ryzyka IT i działy zabezpieczeń muszą zapewnić, że zasoby na platformie Azure są chronione i zabezpieczone domyślnie. Platforma Azure udostępnia funkcje, których można używać do ochrony zasobów podczas wykrywania i eliminowania zagrożeń związanych z tymi zasobami.

### <a name="azure-security-center"></a>Azure Security Center

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) zapewnia ujednolicony widok stanu zabezpieczeń zasobów w środowisku, oprócz zaawansowanej ochrony przed zagrożeniami. Azure Security Center to otwarta platforma, która umożliwia partnerom firmy Microsoft tworzenie oprogramowania, które jest w nim podłączane i zwiększa jego możliwości. Podstawowe możliwości Azure Security Center (warstwa Bezpłatna) zapewniają ocenę i zalecenia, które pomogą ulepszyć stan bezpieczeństwa. Jej warstwy płatne umożliwiają korzystanie z dodatkowych i cennych funkcji, takich jak dostęp administratora just in Time i adaptacyjne kontrolki aplikacji (listy dozwolonych).

> [!TIP]
>Azure Security Center to zaawansowane narzędzie, które jest regularnie ulepszane dzięki nowym funkcjom, których można użyć do wykrywania zagrożeń i ochrony przedsiębiorstwa. Zdecydowanie zaleca się, aby zawsze włączać Azure Security Center.

### <a name="azure-resource-locks"></a>Blokady zasobów platformy Azure

Ponieważ organizacja dodaje podstawowe usługi do subskrypcji, coraz bardziej ważne jest uniknięcie zakłócenia działania firmy. Jednym z typów zakłóceń, które często widzisz, jest niezamierzone konsekwencje skryptów i narzędzi pracujących nad subskrypcją platformy Azure. [Blokady zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) umożliwiają ograniczanie operacji na zasobach o wysokiej wartości, gdy ich modyfikowanie lub usuwanie miałoby znaczący wpływ. Blokady są stosowane do subskrypcji, grupy zasobów, a nawet poszczególnych zasobów. Typowym przypadkiem użycia jest stosowanie blokad do zasobów podstawowych, takich jak sieci wirtualne, bramy, sieciowe grupy zabezpieczeń i konta magazynu kluczy.

### <a name="secure-devops-toolkit"></a>Secure DevOps Toolkit

Pakiet Secure DevOps Kit dla platformy Azure (AzSK) to zbiór skryptów, narzędzi, rozszerzeń i możliwości automatyzacji utworzonych pierwotnie przez zespół IT firmy Microsoft, które zostały [udostępnione jako "open source" za pośrednictwem usługi GitHub](https://github.com/azsk/DevOpsKit-docs). AzSK ma na celu kompleksową subskrypcję platformy Azure i wymagania dotyczące zabezpieczeń zasobów dla zespołów korzystających z rozbudowanej automatyzacji i bezproblemowego integrowania zabezpieczeń z natywnymi przepływami pracy DevOps w celu zapewnienia bezpiecznego DevOps z tymi sześcioma obszarami koncentracji:

- Zabezpiecz subskrypcję
- Włącz bezpieczne programowanie
- Integrowanie zabezpieczeń z usługą CI/CD
- Ciągła gwarancja
- Alerty i monitorowanie
- Zarządzanie ryzykiem w chmurze

![Zestaw narzędzi platformy Azure DevOps](../_images/reference/secure-devops-kit.png)

AzSK to bogaty zestaw narzędzi, skryptów i informacji, które są ważną częścią pełnego planu ładu platformy Azure, a wraz z tym, że jest to niezbędne do tworzenia szkieletu, mają kluczowe znaczenie dla organizacji celów zarządzania ryzykiem.

### <a name="azure-update-management"></a>Update Management platformy Azure

Jednym z najważniejszych zadań, które można wykonać w celu zapewnienia bezpieczeństwa środowiska, jest upewnienie się, że serwery są poprawione przy użyciu najnowszych aktualizacji. Mimo że jest dostępnych wiele narzędzi, platforma Azure udostępnia rozwiązanie [Update Management platformy Azure](https://docs.microsoft.com/azure/automation/automation-update-management) , które umożliwia identyfikowanie i wprowadzanie krytycznych poprawek systemu operacyjnego. Używa Azure Automation, omówione w sekcji [Automatyzowanie](#automate) w dalszej części tego przewodnika.

## <a name="monitor-and-alerts"></a>Monitorowanie i alerty

Zbieranie i analizowanie danych telemetrycznych, które zawierają szczegółowe informacje o działaniach, metrykach wydajności, kondycji i dostępności usług używanych w ramach subskrypcji platformy Azure, ma kluczowe znaczenie dla aktywnego zarządzania aplikacjami i Infrastruktura i to podstawowe potrzeby każdej subskrypcji platformy Azure. Każda usługa platformy Azure emituje dane telemetryczne w postaci dzienników aktywności, metryk i dzienników diagnostycznych.

- **Dzienniki aktywności** opisują wszystkie operacje wykonywane na zasobach w Twoich subskrypcjach.
- **Metryki** to dane numeryczne emitowane przez zasób opisujące wydajność i kondycję zasobu.
- **Dzienniki diagnostyczne** są emitowane przez usługę platformy Azure i umożliwiają rozbudowane, częste dane dotyczące operacji tej usługi.

Te informacje mogą być wyświetlane i przetwarzane na wielu poziomach i stale ulepszane. Platforma Azure oferuje funkcje **udostępnione**, **podstawowe**i **głębokiego** monitorowania zasobów platformy Azure za pomocą usług przedstawionych na poniższym diagramie.

![kontrolą](../_images/reference/monitoring.png)

### <a name="shared-capabilities"></a>Współdzielone możliwości

- **Alerty:** Można zbierać wszystkie dzienniki, zdarzenia i metryki z zasobów platformy Azure, ale bez możliwości powiadomienia o warunkach krytycznych i działaniach, dane te są przydatne tylko w celach historycznych i dowodowych. Alerty platformy Azure aktywnie powiadamiają użytkownika o warunkach definiowanych we wszystkich aplikacjach i infrastrukturze. Można tworzyć reguły alertów w dziennikach, zdarzeniach i metrykach, które używają grup akcji do powiadamiania zestawów odbiorców. Grupy akcji umożliwiają również automatyzację korygowania przy użyciu akcji zewnętrznych, takich jak elementy webhook, aby uruchamiać Azure Automation Runbook i Azure Functions.

- **Pulpity nawigacyjne:** Pulpity nawigacyjne umożliwiają agregowanie widoków monitorowania i łączenie danych między zasobami i subskrypcjami w celu udostępnienia całej korporacyjnemu widoku telemetrii zasobów platformy Azure. Możesz tworzyć i konfigurować własne widoki oraz udostępniać je innym osobom. Na przykład możesz utworzyć pulpit nawigacyjny składający się z różnych kafelków dla administratorów baz danych, aby podać informacje w ramach wszystkich usług Azure Database, w tym Azure SQL DB, Azure DB for PostgreSQL i Azure DB for MySQL.

- **Eksplorator metryk:** Metryki to wartości liczbowe generowane przez zasoby platformy Azure (takie jak% procesora CPU lub we/wy dysku), które zapewniają wgląd w działanie i wydajność zasobów. Za pomocą Eksplorator metryk można definiować i wysyłać metryki, które są przydatne do Log Analytics do agregacji i analizy.

### <a name="core-monitoring"></a>Monitorowanie podstawowe

- **Azure Monitor:** Azure Monitor to podstawowa usługa platformy, która zapewnia pojedyncze źródło do monitorowania zasobów platformy Azure. Interfejs Azure Portal Azure Monitor zapewnia scentralizowany punkt przerwania dla wszystkich funkcji monitorowania w ramach platformy Azure, w tym głębokiego monitorowania możliwości Application Insights, Log Analytics, monitorowania sieci, rozwiązań do zarządzania i Mapy usług. Za pomocą Azure Monitor można wizualizować, wykonywać zapytania, kierować trasy, archiwizować i podejmować działania dotyczące metryk i dzienników pochodzących z zasobów platformy Azure w całej chmurze. Oprócz portalu można pobrać dane za pomocą poleceń cmdlet monitorowania programu PowerShell, międzyplatformowego interfejsu wiersza polecenia lub Azure Monitor interfejsów API REST.

- **Azure Advisor:** Azure Advisor stale monitoruje dane telemetryczne w ramach subskrypcji i środowisk i zawiera zalecenia dotyczące najlepszych rozwiązań dotyczących optymalizacji zasobów platformy Azure w celu oszczędności i poprawy wydajności, bezpieczeństwa i dostępności zasobów. tworzące swoje aplikacje.

- **Service Health:** Azure Service Health identyfikuje wszelkie problemy z usługami platformy Azure, które mogą mieć wpływ na Twoje aplikacje, a także pomaga w planowaniu okien obsługi zaplanowanych.

- **Dziennik aktywności:** Dziennik aktywności zawiera opis wszystkich operacji na zasobach w Twoich subskrypcjach. Zawiera on dziennik inspekcji, aby określić, co "co", "kto" i "When" każdej operacji tworzenia, aktualizowania i usuwania zasobów. Zdarzenia dziennika aktywności są przechowywane na platformie i są dostępne do wykonywania zapytań przez 90 dni. Dzienniki aktywności można pozyskać do Log Analytics w celu uzyskania dłuższych okresów przechowywania oraz dokładniejszego wykonywania zapytań i analiz w wielu zasobach.

### <a name="deep-application-monitoring"></a>Szczegółowe monitorowanie aplikacji

- **Application Insights:** Application Insights umożliwia zbieranie danych telemetrycznych specyficznych dla aplikacji i monitorowanie wydajności, dostępności i użycia aplikacji w chmurze lub lokalnie. Instrumentacja aplikacji dzięki obsługiwanym zestawom SDK dla wielu języków, w tym .NET, JavaScript, JAVA, Node. js, Ruby i Python. Zdarzenia Application Insights są pozyskiwane w tym samym Log Analytics magazynie danych, który obsługuje monitorowanie infrastruktury i zabezpieczeń, aby umożliwić skorelowanie i agregowanie zdarzeń w czasie za pomocą zaawansowanego języka zapytań.

### <a name="deep-infrastructure-monitoring"></a>Szczegółowe monitorowanie infrastruktury

- **Log Analytics:** Log Analytics odgrywa centralną rolę w monitorowaniu platformy Azure, zbierając dane telemetryczne i inne z różnych źródeł oraz dostarczając język zapytań i aparat analityczny, który zapewnia wgląd w działanie aplikacji i zasobów. Możliwe jest bezpośrednie współdziałanie z danymi Log Analytics za pomocą szybkiego wyszukiwania i widoków dzienników. Możesz też użyć narzędzi analitycznych w innych usługach platformy Azure, które przechowują swoje dane w Log Analytics, takich jak Application Insights lub Azure Security Center.

- **Monitorowanie sieci:** Usługi monitorowania sieci platformy Azure umożliwiają uzyskanie wglądu w przepływ ruchu sieciowego, wydajność, bezpieczeństwo, łączność i wąskie gardła. Dobrze zaplanowana konstrukcja sieciowa powinna obejmować skonfigurowanie usług monitorowania sieci platformy Azure, takich jak Network Watcher i monitor ExpressRoute.

- **Rozwiązania do zarządzania:** Rozwiązania do zarządzania to spakowane zestawy logiki, szczegółowe dane i wstępnie zdefiniowane zapytania Log Analytics dla aplikacji lub usługi. Są one zależne od Log Analytics jako podstaw do przechowywania i analizowania danych zdarzeń. Przykładowe rozwiązania do zarządzania obejmują kontenery monitorowania i analizę Azure SQL Database.

- **Service map:** Service Map udostępnia widok graficzny składników infrastruktury, ich procesów i współzależności z innymi komputerami i procesami zewnętrznymi. Integruje zdarzenia, dane dotyczące wydajności i rozwiązania do zarządzania w usłudze Log Analytics.

> [!TIP]
> Przed utworzeniem poszczególnych alertów należy utworzyć i zachować zestaw udostępnionych grup akcji, które mogą być używane w ramach alertów platformy Azure. Dzięki temu można centralnie zarządzać cyklem życia list odbiorców, metodami dostarczania powiadomień (adresami e-mail, numerami telefonów SMS) i elementami webhook do akcji zewnętrznych (Azure Automation elementy Runbook, Azure Functions/Logic Apps, narzędzia ITSM).

## <a name="cost-management"></a>Zarządzanie kosztami

Jednym z najważniejszych zmian, które należy wykonać podczas przechodzenia z chmury lokalnej do chmury publicznej, jest przełączenie z wydatków inwestycyjnych (Kupowanie sprzętu) do wydatków operacyjnych (płacisz za usługę w miarę ich używania). Ten przełącznik wymaga również bardziej dokładnego zarządzania kosztami. Zaletą chmury jest to, że można się w sposób zasadniczy i pozytywnie wpływać na koszt usługi używanej przez zaledwie wyłączenie lub zmianę ich rozmiarów, gdy nie jest to konieczne. Świadome zarządzanie kosztami w chmurze jest najlepszym rozwiązaniem i jednym, który jest codziennie codziennym klientom.

Firma Microsoft udostępnia kilka narzędzi, które umożliwiają wizualizowanie, śledzenie i zarządzanie kosztami. Udostępniamy również pełny zestaw interfejsów API umożliwiających Dostosowywanie i integrację zarządzania kosztami w własnych narzędziach i pulpitach nawigacyjnych. Te narzędzia są luźno pogrupowane w Azure Portal możliwości i funkcje zewnętrzne.

### <a name="azure-portal-capabilities"></a>Możliwości Azure Portal

Są to narzędzia zapewniające natychmiastowe informacje o kosztach, a także możliwość podejmowania działań.

- **Koszt zasobu subskrypcji:** W portalu widok [Analiza kosztów platformy Azure](https://docs.microsoft.com/azure/cost-management/overview) umożliwia szybkie przeszukiwanie kosztów i informacji na temat dziennych wydatków według zasobów lub grup zasobów.
- **Azure Cost Management:** Ten produkt jest wynikiem zakupu Cloudyn przez firmę Microsoft i umożliwia zarządzanie i analizowanie wydatków na platformę Azure, a także to, co poświęcasz innym dostawcom chmury publicznej. Istnieją zarówno warstwy bezpłatne, jak i płatne, które są dostępne w ramach [przeglądu](https://docs.microsoft.com/azure/cost-management/overview).
- **Budżety platformy Azure i grupy akcji:** Zapoznaj się z tym, co się stało z kosztami i wykonywanych przez niego operacji do momentu, aż ostatnio przeprowadzono bardziej ręczne wykonanie Po wprowadzeniu budżetów platformy Azure i jej interfejsów API można teraz tworzyć akcje (jak w [tym przykładzie](https://channel9.msdn.com/Shows/Azure-Friday/Managing-costs-with-the-Azure-Budgets-API-and-Action-Groups)), gdy koszty osiągnęły wartość progową. Na przykład podczas zamykania grupy zasobów "test", gdy trafi 100% swojego budżetu lub [inny przykład].
- **Azure Advisor** Zapoznaj się z tym, czego kosztami jest tylko połowa sprawdzonej; druga połowa zawiera informacje o tym, co należy zrobić z tymi informacjami. [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) udostępnia zalecenia dotyczące działań, które należy podjąć w celu oszczędności, zwiększenia niezawodności lub nawet zwiększenia zabezpieczeń.

### <a name="external-cost-management-tools"></a>Narzędzia do zarządzania kosztami zewnętrznymi

- **Azure Consumption Insights Power BI:** Czy chcesz utworzyć własne wizualizacje dla swojej organizacji? Jeśli tak, wówczas pakiet zawartości Azure Consumption Insights dla Power BI jest wybranym narzędziem. Korzystając z tego pakietu zawartości i Power BI można tworzyć niestandardowe wizualizacje do reprezentowania organizacji, przeprowadzać dokładniejszą analizę kosztów i dodawać do innych źródeł danych w celu dodatkowego wzbogacania.

- **Interfejs API użycia:** [Interfejsy API użycia](/rest/api/consumption) zapewniają programistyczny dostęp do danych kosztów i użycia oprócz informacji o budżetach, wystąpieniach zarezerwowanych i opłatach za witrynę Marketplace. Te interfejsy API są dostępne tylko dla rejestracji w przedsiębiorstwie i niektórych subskrypcji sieci Web bezpośrednich, ale zapewniają możliwość integracji danych kosztów z własnymi narzędziami i magazynami danych. [Dostęp do tych interfejsów API można także uzyskać za pomocą interfejsu wiersza polecenia platformy Azure](/cli/azure/consumption?view=azure-cli-latest).

Klienci, którzy są użytkownikami długoterminowymi i dojrzałymi w chmurze, przestrzegają pewnych najlepszych rozwiązań:

- **Aktywne monitorowanie kosztów.** Organizacje, które są dojrzałymi użytkownikami platformy Azure, stale monitorują koszty i podejmują działania w razie konieczności. Niektóre organizacje mogą nawet przeznaczyć na przeanalizowanie i zasugerować zmiany w użyciu, a te osoby nie są opłacane za pierwszym razem, gdy znajdą nieużywany klaster usługi HDInsight uruchomiony przez miesiące.
- **Użyj wystąpień zarezerwowanych maszyn wirtualnych.** Inna usługa Key cechą do zarządzania kosztami w chmurze polega na użyciu odpowiedniego narzędzia dla tego zadania. Jeśli masz maszynę wirtualną IaaS, która musi pozostać w 24x7, użycie wystąpienia zarezerwowanej maszyny wirtualnej spowoduje znaczne oszczędności. Znalezienie odpowiedniej równowagi między automatyzacją zamykania maszyn wirtualnych i korzystaniem z wystąpień zarezerwowanych maszyn wirtualnych wymaga środowiska i analizy.
- **Efektywnie używaj automatyzacji.** Wiele obciążeń nie musi być wykonywanych codziennie. Wyłączenie maszyny wirtualnej na okres czterech godzin dziennie może zaoszczędzić 15% kosztów. Automatyzacja będzie szybko obciążana za siebie.
- **Użyj tagów zasobów do widoczności.** Jak wspomniano w innym miejscu w tym dokumencie, użycie tagów zasobów umożliwi lepsze analizowanie kosztów.

Zarządzanie kosztami to dyscyplina, która jest podstawą dla efektywnego i wydajnego działania chmury publicznej. Przedsiębiorstwa, które osiągają sukces, mogą kontrolować swoje koszty i dopasować je do ich rzeczywistej podaży, zamiast kupowania i zostaje popytu.

## <a name="automate"></a>Automatyzacja

Jedną z wielu możliwości, które różnią się okresem zapadalności organizacji korzystających z usług Cloud Providers, jest poziom automatyzacji, który ma wbudowaną funkcję. Automatyzacja jest procesem niekończącym, a organizacja przechodzi do chmury. jest to każdy obszar, w którym należy zainwestować zasoby i czas na kompilację. Automatyzacja służy do wielu celów, w tym spójnego wdrażania zasobów (w przypadku, gdy wiąże się to z innymi koncepcjami podstawowych koncepcji, szablonów i DevOps) na Korygowanie problemów. Automatyzacja to "dołączona tkanka" szkieletu platformy Azure i łączy każdy obszar.

Kilka narzędzi może pomóc Ci w rozpoczęciu tej możliwości od narzędzi pierwszej firmy, takich jak Azure Automation, Event Grid i interfejsu wiersza polecenia platformy Azure, do obszernej liczby narzędzi innych firm, takich jak Terraform, Jenkins, Chef i Puppet. Podstawowe narzędzia automatyzacji obejmują Azure Automation, Event Grid i Azure Cloud Shell.

- **Azure Automation** Usługa to oparta na chmurze funkcja umożliwiająca tworzenie elementów Runbook (w programach PowerShell lub Python) i pozwala zautomatyzować procesy, konfigurować zasoby, a nawet stosować poprawki. [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) zawiera rozbudowany zestaw funkcji międzyplatformowych, które są integralną częścią wdrożenia, ale są zbyt obszerne, aby można je było szczegółowo znaleźć w tym miejscu.
- **Event Grid** to w pełni zarządzany system routingu zdarzeń, który umożliwia reagowanie na zdarzenia w środowisku platformy Azure. Podobnie jak Azure Automation to dołączona tkana organizacja w chmurze, [Event Grid](https://docs.microsoft.com/azure/event-grid) to tkana tkanka dobrej automatyzacji. Za pomocą Event Grid można utworzyć prostą akcję bezserwerową, aby wysłać wiadomość e-mail do administratora po każdym utworzeniu nowego zasobu i zalogować go do bazy danych. Ten sam Event Grid może powiadamiać o usunięciu zasobu i usunięciu elementu z bazy danych.
- **Azure Cloud Shell** to interaktywna [powłoka](https://docs.microsoft.com/azure/cloud-shell/overview) oparta na przeglądarce służąca do zarządzania zasobami na platformie Azure. Zapewnia całe środowisko dla programu PowerShell lub bash, które są uruchamiane zgodnie z potrzebami (i obsługiwane przez Ciebie), dzięki czemu masz spójne środowisko, z którego można uruchamiać skrypty. Azure Cloud Shell zapewnia dostęp do dodatkowych narzędzi kluczowych — już zainstalowane — w celu zautomatyzowania środowiska, w tym [interfejsu wiersza polecenia platformy Azure](/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), [Terraform](https://docs.microsoft.com/azure/virtual-machines/linux/terraform-install-configure) i coraz większej listy dodatkowych [narzędzi](https://azure.microsoft.com/updates/cloud-shell-new-cli-tools-and-font-size-selection) do zarządzania kontenerami, bazami danych (sqlcmd) i szczegółowe.

Automatyzacja to zadanie w pełnym czasie i szybko staje się jednym z najważniejszych zadań operacyjnych w ramach zespołu w chmurze. Organizacje, które przyjmują podejście "Automatyzacja First", przewyższają sukces korzystania z platformy Azure:

- **Zarządzanie kosztami:** Aktywnie przeszukiwanie możliwości i tworzenie automatyzacji w celu zmiany rozmiaru zasobów, skalowanie w górę lub w dół oraz wyłączanie nieużywanych zasobów.
- **Elastyczność operacyjna:** Dzięki automatyzacji (wraz z szablonami i DevOps) można uzyskać poziom powtarzalności, który zwiększa dostępność, zwiększa bezpieczeństwo i umożliwia zespołowi skoncentrowanie się na rozwiązywaniu problemów z firmą.

## <a name="templates-and-devops"></a>Szablony i DevOps

Jak wyróżniono w sekcji Automatyzowanie, celem jako organizacja powinna być Inicjowanie obsługi zasobów przy użyciu szablonów i skryptów sterowanych przez źródło oraz zminimalizowanie interaktywnej konfiguracji środowisk. Takie podejście do "infrastruktury jako kodu" oraz DevOps proces tworzenia ciągłego wdrażania może zapewnić spójność i zmniejszenie dryfu w swoich środowiskach. Niemal każdy zasób platformy Azure jest wdrażany za pośrednictwem [Azure Resource Manager szablonów JSON](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) w połączeniu z programem PowerShell lub interfejsem wiersza polecenia platformy Azure międzyplatformowym i narzędziami, takimi jak Terraform z Hashicorp (które są w pierwszej klasie obsługiwane i zintegrowane z platformą Azure Cloud Shell).

Artykuł, taki jak [najlepsze rozwiązania dotyczące korzystania z szablonów Azure Resource Manager](https://blogs.msdn.microsoft.com/mvpawardprogram/2018/05/01/azure-resource-manager) , oferuje doskonałą dyskusję na temat najlepszych rozwiązań i lekcji na potrzeby zastosowania podejścia DevOps do Azure Resource Manager szablonów za pomocą [usługi Azure DevOps](https://docs.microsoft.com/azure/devops/user-guide/?view=vsts) łańcucha narzędzi . Zapoznaj się z czasem i wysiłkią w celu opracowania podstawowego zestawu szablonów specyficznych dla wymagań organizacji i opracowania ciągłego potoków dostarczania przy użyciu DevOps łańcuchy narzędzi (takich jak Azure DevOps, Jenkins, Bamboo, TeamCity i Concourse), szczególnie w przypadku Twojego środowiska produkcyjne i pytania i odpowiedzi. Istnieje duża Biblioteka [szablonów szybkiego startu platformy Azure](https://github.com/Azure/azure-quickstart-templates) w serwisie GitHub, których można użyć jako punktu wyjścia dla szablonów. możesz szybko tworzyć potoki dostarczania oparte na chmurze za pomocą usługi Azure DevOps.

Najlepszym rozwiązaniem w przypadku subskrypcji produkcyjnych lub grup zasobów jest użycie funkcji kontroli dostępu RBAC, aby domyślnie nie zezwalać użytkownikom interaktywnym na korzystanie z automatycznych potoków ciągłego dostarczania w oparciu o jednostki usługi w celu aprowizacji wszystkich zasobów i Dostarcz cały kod aplikacji. Żaden administrator ani Deweloper nie powinien dotykać Azure Portal, aby interaktywnie konfigurować zasoby. Ten poziom DevOps ma uzgodniony nakład pracy i korzysta ze wszystkich koncepcji szkieletu platformy Azure, zapewniając spójne i bezpieczniejsze środowisko, które będzie spełniało potrzeby Twojej organizacji.

> [!TIP]
> Podczas projektowania i opracowywania złożonych szablonów Azure Resource Manager należy używać [połączonych szablonów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-linked-templates) do organizowania i refaktoryzacji złożonych relacji zasobów z monolitycznych plików JSON. Umożliwi to osobne zarządzanie zasobami i bardziej czytelne, weryfikowalne i wielokrotne użycie szablonów.

Azure to dostawca usług w chmurze w skali. W miarę przenoszenia organizacji z serwerów lokalnych do chmury opierają się na tych samych pojęciach, które są używane przez dostawców chmury i aplikacje SaaS, dzięki czemu organizacja reaguje na potrzeby biznesowe znacznie bardziej wydajnie.

## <a name="core-network"></a>Sieć podstawowa

Ostatnim składnikiem modelu referencyjnego szkieletu platformy Azure jest rdzeń do sposobu, w jaki organizacja uzyskuje dostęp do platformy Azure w bezpieczny sposób. Dostęp do zasobów może być wewnętrzny (w sieci firmy) lub zewnętrzny (przez Internet). Użytkownicy w organizacji mogą łatwo bezproblemowo umieszczać zasoby w niewłaściwym miejscu i mogą otwierać je w złośliwym dostępie. Podobnie jak w przypadku urządzeń lokalnych, przedsiębiorstwa muszą dodać odpowiednie środki kontroli, aby upewnić się, że użytkownicy platformy Azure podejmują właściwe decyzje. W przypadku zarządzania subskrypcjami identyfikujemy podstawowe zasoby, które zapewniają podstawową kontrolę dostępu. Podstawowe zasoby składają się z:

- **Sieci wirtualne** są obiektami kontenerów dla podsieci. Chociaż nie jest to absolutnie konieczne, często są używane podczas łączenia aplikacji z wewnętrznymi zasobami firmy.
- **Trasy zdefiniowane przez użytkownika** umożliwiają manipulowanie tabelą tras w podsieci, co umożliwia przesyłanie ruchu przez sieciowe urządzenie wirtualne lub do bramy zdalnej w równorzędnej sieci wirtualnej.
- **Komunikacja równorzędna sieci wirtualnych** umożliwia bezproblemowe łączenie co najmniej dwóch sieci wirtualnych platformy Azure, tworząc bardziej złożone projekty typu Hub i szprych lub sieci usług udostępnionych.
- **Punkty końcowe usługi.** W przeszłości usługi PaaS opierają się na różnych metodach zabezpieczania dostępu do tych zasobów z sieci wirtualnych. Punkty końcowe usługi umożliwiają zabezpieczenie dostępu do włączonych usług PaaS **wyłącznie** z połączonych punktów końcowych, zwiększając ogólne zabezpieczenia.
- **Grupy zabezpieczeń** to obszerny zestaw reguł, które zapewniają możliwość zezwalania na ruch przychodzący i wychodzący do/z zasobów platformy Azure. [Grupy zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/security-overview) składają się z reguł zabezpieczeń, które można rozszerzyć za pomocą **tagów usługi** (które definiują typowe usługi platformy Azure, takie jak Azure Key Vault lub Azure SQL Database) i **grup zabezpieczeń aplikacji** (które definiują i obsługują aplikacje). Struktura, taka jak serwery sieci Web lub serwery aplikacji).

> [!TIP]
> Użyj tagów usługi i grup zabezpieczeń aplikacji w sieciowych grupach zabezpieczeń nie tylko, aby zwiększyć czytelność reguł &mdash;which ma kluczowe znaczenie dla zrozumienie wpływu &mdash;but, aby umożliwić efektywne mikrosegmentację w większej podsieci, zmniejszenie rozwojem i zwiększanie elastyczności.

### <a name="azure-virtual-datacenter"></a>Wirtualne centrum danych Azure

Platforma Azure udostępnia zarówno wewnętrzne możliwości, jak i funkcje innych firm, które umożliwiają efektywne zasobów zakresie zabezpieczeń. Co ważniejsze, firma Microsoft oferuje najlepsze rozwiązania i wskazówki w formie [wirtualnego centrum danych platformy Azure (VDC)](./networking-vdc.md). Podczas przechodzenia z pojedynczego obciążenia do wielu obciążeń, które wykorzystują możliwości hybrydowe, wskazówki VDC zapewniają "przepisy", aby umożliwić elastyczne, sieci, które będą rosnąć w miarę wzrostu obciążeń na platformie Azure.

## <a name="next-steps"></a>Następne kroki

Zarządzanie ma kluczowe znaczenie dla sukcesu platformy Azure. Ten artykuł dotyczy implementacji technicznej szkieletu przedsiębiorstwa, ale tylko dotyka szerszego procesu i relacji między składnikami. Zarządzanie zasadami przepływów od góry i zależy od tego, co firma chce osiągnąć. W naturalny sposób Tworzenie modelu zarządzania dla platformy Azure obejmuje przedstawicieli z działu IT, ale co ważniejsze, powinno mieć silną reprezentację od liderów grupy biznesowej oraz zarządzania zabezpieczeniami i ryzykiem. Na koniec szkielet przedsiębiorstwa ma na celu wyeliminowanie ryzyka biznesowego, aby ułatwić jego misja i cele.

Teraz, gdy znasz już zasady zarządzania subskrypcjami, zapoznaj się z tymi zaleceniami. Zobacz [Przykłady implementacji ładu subskrypcji platformy Azure](./azure-scaffold-examples.md).
