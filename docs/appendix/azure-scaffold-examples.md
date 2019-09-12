---
title: Scenariusze i przykłady dotyczące zarządzania subskrypcjami
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zawiera przykłady implementacji zarządzania subskrypcjami platformy Azure dla typowych scenariuszy.
author: rdendtler
ms.author: rodend
ms.date: 01/03/2017
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: 92320fe24974d7e79d63751dd9afb96787e8c76d
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906117"
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Przykłady implementacji szkieletu platformy Azure Enterprise

> [!NOTE]
> Tworzenie szkieletu przedsiębiorstwa platformy Azure zostało zintegrowane z platformą wdrażania Microsoft Cloud. Zawartość tego artykułu jest teraz reprezentowana w sekcji gotowych [](../ready/index.md) nowej struktury. Ten artykuł zostanie uznany za przestarzały na początku 2020. Aby rozpocząć korzystanie z nowego procesu, zapoznaj się z tematem gotowym do [omówienia](../ready/index.md), [tworzeniu pierwszej strefy docelowej](../ready/azure-readiness-guide/migration-landing-zone.md)i/lub zagadnieniami dotyczącymi [strefy docelowej](../ready/considerations/index.md).

W tym artykule przedstawiono przykłady zastosowania przez przedsiębiorstwo zaleceń dla [szkieletu platformy Azure Enterprise](azure-scaffold.md). Używa fikcyjnej firmy o nazwie contoso do zilustrowania najlepszych rozwiązań dla typowych scenariuszy.

## <a name="background"></a>Tło

Contoso to firma ogólnoświatowa, która udostępnia rozwiązania łańcucha dostaw dla klientów. Udostępniają one wszystkie elementy oprogramowania jako modelu usługi do spakowanego modelu wdrożonego lokalnie. Opracowują one oprogramowanie na całym świecie przy użyciu znaczących centrów rozwoju w Indiach, Stany Zjednoczone i Kanadzie.

Część producenta niezależnego dostawcy oprogramowania jest dzielona na kilka niezależnych jednostek, które zarządzają produktami w znaczących firmach. Każda jednostka biznesowa ma swoich własnych deweloperów, menedżerów produktów i architektów.

Jednostka biznesowa usług Enterprise Technology Services (ETS) udostępnia scentralizowaną funkcję IT i zarządza kilkoma centrami danych, w których jednostki biznesowe obsługują swoje aplikacje. Wraz z zarządzaniem centrami danych organizacja ETS zapewnia i zarządza scentralizowaną współpracą (np. pocztą e-mail i witrynami sieci Web) oraz usługami sieciowymi/telefonicznymi. Umożliwiają one również zarządzanie obciążeniami przeznaczonymi dla klientów w przypadku mniejszych jednostek pracy, które nie mają pracowników operacyjnych.

W tym artykule są używane następujące osób:

- Dave jest administratorem platformy Azure.
- Alicja to dyrektor ds. rozwoju firmy Contoso w jednostce biznesowej łańcucha dostaw.

Firma Contoso musi utworzyć aplikację biznesową i aplikację skierowaną do klientów. Postanowiono uruchamiać aplikacje na platformie Azure. Dave odczytuje artykuł dotyczący tego [ładu](azure-scaffold.md) i jest gotowy do wdrożenia zaleceń.

## <a name="scenario-1-line-of-business-application"></a>Scenariusz 1: aplikacja biznesowa

Firma Contoso tworzy system zarządzania kodem źródłowym (BitBucket), który będzie używany przez deweloperów na całym świecie. Aplikacja używa infrastruktury jako usługi (IaaS) do hostingu i składa się z serwerów sieci Web i serwera bazy danych. Deweloperzy uzyskują dostęp do serwerów w swoich środowiskach deweloperskich, ale nie potrzebują dostępu do serwerów na platformie Azure. Firma Contoso ETS chce zezwolić właścicielowi aplikacji i zespołowi na zarządzanie aplikacją. Aplikacja jest dostępna tylko w sieci firmowej firmy Contoso. Dave musi skonfigurować subskrypcję tej aplikacji. Subskrypcja będzie również hostować inne oprogramowanie związane z deweloperem w przyszłości.

### <a name="naming-standards-and-resource-groups"></a>Nazewnictwo standardów i grup zasobów

Dave tworzy subskrypcję do obsługi narzędzi deweloperskich, które są wspólne dla wszystkich jednostek firmy. Dave musi utworzyć znaczące nazwy dla subskrypcji i grup zasobów (dla aplikacji i sieci). Tworzy następujące grupy zasobów i subskrypcji:

| Element | Name | Opis |
| --- | --- | --- |
| Subscription |Produkcja contoso ETS DeveloperTools |Obsługuje popularne narzędzia deweloperskie |
| Resource group |BitBucket — prod-RG |Zawiera serwer sieci Web aplikacji i serwer bazy danych |
| Resource group |corenetworks-prod-rg |Zawiera sieci wirtualne i połączenie bramy lokacja-lokacja |

### <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach

Po utworzeniu subskrypcji Dave chce mieć pewność, że odpowiednie zespoły i właściciele aplikacji mogą uzyskać dostęp do swoich zasobów. Dave uznaje, że każdy zespół ma inne wymagania. Używa grup, które zostały zsynchronizowane z Active Directory lokalnego firmy Contoso do Azure Active Directory i zapewnia odpowiedni poziom dostępu do zespołów.

Dave przypisuje następujące role dla subskrypcji:

| Role | Przypisane do | Opis |
| --- | --- | --- |
| [Właściciel](/azure/role-based-access-control/built-in-roles#owner) |Identyfikator zarządzany z lokalnego Active Directory firmy Contoso |Ten identyfikator jest kontrolowany z dostępem just-in-Time (JIT) za pomocą narzędzia do zarządzania tożsamościami firmy Contoso i zapewnia pełną inspekcję dostępu właściciela subskrypcji |
| [Czytelnik zabezpieczeń](/azure/role-based-access-control/built-in-roles#security-reader) |Dział zarządzania zabezpieczeniami i ryzykiem |Ta rola umożliwia użytkownikom przeglądanie Azure Security Center i stanu zasobów |
| [Współautor sieci](/azure/role-based-access-control/built-in-roles#network-contributor) |Zespół sieci |Ta rola umożliwia zespołowi sieci firmy Contoso zarządzanie lokacją sieci VPN między lokacjami i sieciami wirtualnymi |
| *Rola niestandardowa* |Właściciel aplikacji |Dave tworzy rolę, która przyznaje możliwość modyfikowania zasobów w grupie zasobów. Aby uzyskać więcej informacji, zobacz [role niestandardowe w usłudze Azure RBAC](/azure/role-based-access-control/custom-roles) |

### <a name="policies"></a>Zasady

Dave mają następujące wymagania dotyczące zarządzania zasobami w ramach subskrypcji:

- Ponieważ narzędzia programistyczne obsługują deweloperów na całym świecie, nie chce blokować tworzenia zasobów przez użytkowników w dowolnym regionie. Jednak musi on wiedzieć, gdzie są tworzone zasoby.
- Jest on zaangażowany w koszty. W związku z tym chce uniemożliwić właścicielom aplikacji Tworzenie niekoniecznie kosztownych maszyn wirtualnych.
- Ponieważ ta aplikacja obsługuje deweloperów w wielu jednostkach roboczych, chce, aby każdy zasób był oznakowany jednostką biznesową i właścicielem aplikacji. Korzystając z tych tagów, można rozliczać odpowiednie zespoły przy użyciu opcji ETS.

Tworzy następujące zasady za pośrednictwem [Azure Policy](/azure/azure-policy/azure-policy-introduction):

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |Wizyjn |Inspekcja tworzenia zasobów w dowolnym regionie |
| type |odrzuć |Odmowa tworzenia maszyn wirtualnych z serii G |
| tags |odrzuć |Wymagaj tagu właściciela aplikacji |
| tags |odrzuć |Wymagaj tagu centrum kosztów |
| tags |łączono |Dołącz nazwę tagu **BusinessUnit** i wartość tagu **ETS** do wszystkich zasobów |

### <a name="resource-tags"></a>Tagi zasobów

Dave rozumie, że musi mieć określone informacje na rachunku, aby zidentyfikować centrum kosztów dla implementacji BitBucket. Ponadto Dave chce znać wszystkie zasoby, które są własnością.

Dodaje następujące [znaczniki](/azure/azure-resource-manager/resource-group-using-tags) do grup zasobów i zasobów.

| Nazwa tagu | Wartość tagu |
| --- | --- |
| ApplicationOwner |Nazwa osoby, która zarządza tą aplikacją |
| CostCenter |Centrum kosztów grupy, która płaci za użycie platformy Azure |
| BusinessUnit |**ETS** (jednostka biznesowa skojarzona z subskrypcją) |

### <a name="core-network"></a>Sieć podstawowa

Firma Contoso — informacje o zabezpieczeniach i zespół ds. zarządzania ryzykiem przegląd Dave plan, aby przenieść aplikację na platformę Azure. Chcą mieć pewność, że aplikacja nie jest ujawniona w Internecie. Dave także aplikacje dla deweloperów, które w przyszłości zostaną przeniesione na platformę Azure. Aplikacje te wymagają interfejsów publicznych. Aby spełnić te wymagania, udostępnia wewnętrzne i zewnętrzne sieci wirtualne oraz sieciową grupę zabezpieczeń w celu ograniczenia dostępu.

Tworzy następujące zasoby:

| Typ zasobu | Name | Opis |
| --- | --- | --- |
| Sieć wirtualna |internal-vnet |Używany z aplikacją BitBucket i jest połączony za pośrednictwem ExpressRoute z siecią firmową firmy Contoso. Podsieć (`bitbucket`) udostępnia aplikację z określoną przestrzenią adresów IP |
| Sieć wirtualna |zewnętrzna Sieć wirtualna |Dostępne dla przyszłych aplikacji, które wymagają publicznych punktów końcowych |
| Sieciowa grupa zabezpieczeń |BitBucket — sieciowej grupy zabezpieczeń |Zapewnia, że obszar ataków tego obciążenia jest zminimalizowany przez umożliwienie połączeń tylko na porcie 443 dla podsieci, w której przebywa aplikacja (`bitbucket`) |

### <a name="resource-locks"></a>Blokady zasobów

Dave uznaje, że łączność z firmowej sieci firmy Contoso z wewnętrzną siecią wirtualną musi być chroniona przed dowolnym skryptem Wayward lub przypadkowym usunięciem.

Tworzy następującą [blokadę zasobu](/azure/azure-resource-manager/resource-group-lock-resources):

| Typ blokady | Resource | Opis |
| --- | --- | --- |
| **CanNotDelete** |internal-vnet |Uniemożliwia użytkownikom usuwanie sieci wirtualnej lub podsieci, ale nie uniemożliwia dodawania nowych podsieci |

### <a name="azure-automation"></a>Azure Automation

Dave nie ma nic do automatyzowania dla tej aplikacji. Mimo że utworzono konto Azure Automation, nie będzie ono początkowo używane.

### <a name="azure-security-center"></a>Azure Security Center

Firma Contoso zarządzanie usługami IT musi szybko identyfikować i obsługiwać zagrożenia. Chcą również zrozumieć, jakie problemy mogą istnieć.

Aby spełnić te wymagania, Dave włącza [Azure Security Center](/azure/security-center/security-center-intro) i zapewnia dostęp do roli czytelnik zabezpieczeń.

## <a name="scenario-2-customer-facing-app"></a>Scenariusz 2: aplikacja dołączona do klienta

Liderzy biznesowi w jednostce biznesowej łańcucha dostaw zidentyfikowano różne możliwości zwiększania zaangażowania z klientami firmy Contoso przy użyciu karty lojalnościowej. Zespół Alicja musi utworzyć tę aplikację i zdecydować, że platforma Azure zwiększa swoją zdolność do zaspokajania potrzeb firmy. Alicja współpracuje z usługą Dave z usługi ETS, aby skonfigurować dwie subskrypcje na potrzeby tworzenia i obsługi tej aplikacji.

### <a name="azure-subscriptions"></a>Subskrypcje platformy Azure

Dave loguje się do Enterprise Portal platformy Azure i zauważa, że dział łańcucha dostaw już istnieje. Jednak ponieważ ten projekt jest pierwszym projektem programistycznym dla zespołu łańcucha dostaw na platformie Azure, Dave rozpoznaje potrzebę nowego konta dla zespołu deweloperów. Tworzy konto "R & D" dla swojego zespołu i przypisuje do niego dostęp. Alicja loguje się za pośrednictwem Azure Portal i tworzy dwie subskrypcje: jeden do przechowywania serwerów deweloperskich i jeden do przechowywania serwerów produkcyjnych. Podczas tworzenia następujących subskrypcji następuje zgodność z określonymi wcześniej standardami nazewnictwa:

| Użycie subskrypcji | Name |
| --- | --- |
| Programowanie |Contoso SupplyChain ResearchDevelopment LoyaltyCard Development |
| Produkcja |Produkcja contoso SupplyChain Operations LoyaltyCard |

### <a name="policies"></a>Zasady

Dave i Alicja omawiają aplikację i identyfikują, że ta aplikacja obsługuje tylko klientów w regionie Ameryki Północnej. Alicja i jej zespół planuje używać środowiska usługi aplikacji platformy Azure i usługi Azure SQL do tworzenia aplikacji. Może być konieczne utworzenie maszyn wirtualnych podczas opracowywania. Alicja chce upewnić się, że deweloperzy mają zasoby potrzebne im do eksplorowania i badania problemów bez konieczności ściągania.

W przypadku **subskrypcji deweloperskich**tworzone są następujące zasady:

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |Wizyjn |Inspekcja tworzenia zasobów w dowolnym regionie |

Nie ograniczają one typu jednostki SKU, którą użytkownik może utworzyć podczas opracowywania i nie wymagają tagów dla żadnych grup zasobów ani zasobów.

W przypadku **subskrypcji produkcyjnej**tworzone są następujące zasady:

| Pole | Efekt | Opis |
| --- | --- | --- |
| location |odrzuć |Odmów tworzenia wszelkich zasobów poza centrami danych USA |
| tags |odrzuć |Wymagaj tagu właściciela aplikacji |
| tags |odrzuć |Wymagaj tagu działu |
| tags |łączono |Dołącz tag do każdej grupy zasobów, która wskazuje środowisko produkcyjne |

Nie ograniczają one typu jednostki SKU, którą użytkownik może utworzyć w środowisku produkcyjnym.

### <a name="resource-tags"></a>Tagi zasobów

Dave rozumie, że musi mieć określone informacje w celu zidentyfikowania odpowiednich grup gospodarczych do rozliczeń i własności. Definiuje Tagi zasobów dla grup zasobów i zasobów.

| Nazwa tagu | Wartość tagu |
| --- | --- |
| ApplicationOwner |Nazwa osoby, która zarządza tą aplikacją |
| Dział |Centrum kosztów grupy, która płaci za użycie platformy Azure |
| EnvironmentType |**Produkcja** (Mimo że subskrypcja obejmuje **produkcyjną** nazwę, łącznie z tym tagiem umożliwia łatwą identyfikację podczas przeglądania zasobów w portalu lub na rachunku) |

### <a name="core-networks"></a>Sieci podstawowe

Firma Contoso — informacje o zabezpieczeniach i zespół ds. zarządzania ryzykiem przegląd Dave plan, aby przenieść aplikację na platformę Azure. Chcą mieć pewność, że aplikacja karty lojalnościowej jest odpowiednio izolowana i chroniona w sieci DMZ. Aby spełnić to wymaganie, Dave i Alicja tworzy zewnętrzną sieć wirtualną i sieciową grupę zabezpieczeń w celu wyizolowania aplikacji karty lojalnościowej z firmowej sieci firmy Contoso.

W przypadku **subskrypcji deweloperskiej**tworzone są:

| Typ zasobu | Name | Opis |
| --- | --- | --- |
| Sieć wirtualna |internal-vnet |Obsługuje środowisko deweloperskie kart lojalnościowych Contoso i jest połączone przez ExpressRoute z siecią firmową firmy Contoso |

W przypadku **subskrypcji produkcyjnej**tworzone są:

| Typ zasobu | Name | Opis |
| --- | --- | --- |
| Sieć wirtualna |zewnętrzna Sieć wirtualna |Obsługuje aplikację karty lojalnościowej i nie jest połączona bezpośrednio z ExpressRoute firmy Contoso. Kod jest wypychany przez system kodu źródłowego bezpośrednio do usług PaaS. |
| Sieciowa grupa zabezpieczeń |loyaltycard — sieciowej grupy zabezpieczeń |Zapewnia, że obszar ataków tego obciążenia jest zminimalizowany przez umożliwienie komunikacji wyłącznie w ramach protokołu TCP 443. Firma Contoso bada także za pomocą zapory aplikacji sieci Web w celu uzyskania dodatkowej ochrony. |

### <a name="resource-locks"></a>Blokady zasobów

Dave i Alicja przydaje i decyduje się dodać blokady zasobów dla niektórych kluczowych zasobów w środowisku, aby zapobiec przypadkowemu usunięciu podczas wypychania kodu errant.

Tworzą następujące blokady:

| Typ blokady | Resource | Opis |
| --- | --- | --- |
| **CanNotDelete** |zewnętrzna Sieć wirtualna |Aby uniemożliwić osobom usuwanie sieci wirtualnej lub podsieci. Blokada nie zapobiega dodawaniu nowych podsieci |

### <a name="azure-automation"></a>Azure Automation

Alicja i jej zespół programistyczny mają wiele elementów Runbook do zarządzania środowiskiem dla tej aplikacji. Elementy Runbook umożliwiają dodawanie/usuwanie węzłów aplikacji i innych zadań DevOps.

Aby można było używać tych elementów Runbook, włączają [automatyzację](/azure/automation/automation-intro).

### <a name="azure-security-center"></a>Azure Security Center

Firma Contoso zarządzanie usługami IT musi szybko identyfikować i obsługiwać zagrożenia. Chcą również zrozumieć, jakie problemy mogą istnieć.

Aby spełnić te wymagania, Dave włącza Azure Security Center. Zapewnia, że Azure Security Center monitorowanie zasobów i zapewnia dostęp do zespołów DevOps i zabezpieczeń.

## <a name="next-steps"></a>Następne kroki

- Aby dowiedzieć się więcej na temat tworzenia szablonów Menedżer zasobów, zobacz [najlepsze rozwiązania dotyczące tworzenia Azure Resource Manager szablonów](/azure/azure-resource-manager/resource-manager-template-best-practices).
