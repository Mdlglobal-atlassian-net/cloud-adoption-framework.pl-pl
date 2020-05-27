---
title: Wdrażanie infrastruktury migracji
description: Dowiedz się, jak firma Contoso konfiguruje infrastrukturę platformy Azure na potrzeby migracji na platformę Azure.
author: deltadan
ms.author: abuck
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: cf026f32e52f5742525e655cd904e152e849bcd6
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861977"
---
<!-- cSpell:ignore deltadan CSPs untrust CIDR RRAS CONTOSODC sysvol ITIL NSGs ASGs -->

# <a name="deploy-a-migration-infrastructure"></a>Wdrażanie infrastruktury migracji

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso przygotowuje infrastrukturę lokalną do migracji, konfiguruje infrastrukturę platformy Azure w ramach przygotowania do migracji i uruchamia działalność biznesową w środowisku hybrydowym. W przypadku użycia tego przykładu w celu zaplanowania własnych wysiłków związanych z migracją infrastruktury należy pamiętać o następujących kwestiach:

- Udostępniona przykładowa architektura jest specyficzna dla firmy Contoso. Podczas podejmowania ważnych decyzji dotyczących infrastruktury, w tym projektu subskrypcji lub architektury sieci, uwzględnij potrzeby biznesowe, strukturę i wymagania techniczne swojej organizacji.
- To, czy potrzebujesz wszystkich elementów opisanych w tym artykule, zależy od Twojej strategii migracji. Na przykład jeśli tworzysz tylko aplikacje natywne w chmurze na platformie Azure, możesz potrzebować mniej złożonej struktury sieci.

## <a name="overview"></a>Omówienie

Aby firma Contoso mogła przeprowadzić migrację na platformę Azure, kluczowe jest przygotowanie infrastruktury platformy Azure. Ogólnie rzecz biorąc, należy wziąć pod uwagę sześć szerokich obszarów firmy Contoso:

> [!div class="checklist"]
>
> - **Krok 1: subskrypcje platformy Azure.** Jak firma Contoso dokona zakupu platformy Azure i w jaki sposób będzie korzystać z platformy Azure oraz jej usług?
> - **Krok 2: tożsamość hybrydowa.** Jak będzie zarządzać dostępem do zasobów lokalnych i zasobów platformy Azure oraz kontrolować do nich dostęp po migracji? Jak firma Contoso rozszerzy lub przeniesie zarządzanie tożsamościami do chmury?
> - **Krok 3. odzyskiwanie awaryjne i odporność.** W jaki sposób firma Contoso zapewnia odporność aplikacji i infrastruktury na przestoje i awarie?
> - **Krok 4. sieć.** Jak firma Contoso powinna zaprojektować infrastrukturę sieciową i ustanowić połączenie między lokalnym centrum danych a platformą Azure?
> - **Krok 5. zabezpieczenia.** Jak firma Contoso będzie zabezpieczać wdrożenie hybrydowe/wdrożenie platformy Azure?
> - **Krok 6. zarządzanie.** W jaki sposób firma Contoso będzie zapewniać zgodność wdrożenia z wymaganiami dotyczącymi zabezpieczeń i ładu?

## <a name="before-you-start"></a>Przed rozpoczęciem

Przed rozpoczęciem przeglądania infrastruktury Rozważ odczytanie niektórych informacji w tle dotyczących odpowiednich możliwości platformy Azure:

- Dostępnych jest kilka opcji zakupu dostępu do platformy Azure, w tym: płatność zgodnie z rzeczywistym użyciem, umowy Enterprise Agreement (EA), program licencjonowania Open od odsprzedawców produktów firmy Microsoft lub partnerów firmy Microsoft, tzw. dostawców rozwiązań w chmurze (CSP). Dowiedz się więcej na temat [opcji zakupu](https://azure.microsoft.com/pricing/purchase-options) i przeczytaj, jak [są zorganizowane subskrypcje platformy Azure](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Zapoznaj się z omówieniem [zarządzania tożsamościami i dostępem](https://www.microsoft.com/security/business/identity) na platformie Azure. W szczególności uzyskaj informacje na temat [usługi Azure AD i rozszerzania lokalnej usługi Active Directory na chmurę](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Istnieje przydatna dostępna do pobrania książka elektroniczna dotycząca [zarządzania dostępem i tożsamościami w środowisku hybrydowym](https://azure.microsoft.com/resources/hybrid-cloud-identity).
- Platforma Azure oferuje niezawodną infrastrukturę sieciową z opcjami łączności hybrydowej. Zapoznaj się z omówieniem [sieci i kontroli dostępu do sieci](https://docs.microsoft.com/azure/security/security-network-overview).
- Zapoznaj się z [wprowadzeniem do zabezpieczeń platformy Azure](https://docs.microsoft.com/azure/security/fundamentals/overview)i Dowiedz się, jak utworzyć plan dla [ładu platformy Azure](https://docs.microsoft.com/azure/governance).

## <a name="on-premises-architecture"></a>Architektura lokalna

Oto diagram przedstawiający bieżącą infrastrukturę lokalną firmy Contoso.

 ![Architektura firmy Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Firma Contoso ma jedno główne centrum danych znajdujące się w mieście w Nowym Jorku w Stany Zjednoczone wschodnim.
- Firma ma trzy dodatkowe oddziały lokalne na terenie Stanów Zjednoczonych.
- Główne centrum danych jest połączone z Internetem przy użyciu połączenia Fiber Metro Ethernet (500 MB/s).
- Każdy oddział jest połączony lokalnie z Internetem przy użyciu połączeń klasy biznesowej z tunelami IPSec VPN prowadzącymi z powrotem do głównego centrum danych. Takie podejście umożliwia stałe połączenie całej sieci i optymalizację łączności z Internetem.
- Główne centrum danych jest w pełni zwirtualizowane przy użyciu programu VMware. Firma Contoso ma dwa hosty wirtualizacji ESXi 6.5, zarządzane za pomocą programu vCenter Server 6.5.
- Firma Contoso korzysta z usługi Active Directory na potrzeby zarządzania tożsamościami oraz serwerów DNS w sieci wewnętrznej.
- Kontrolery domeny w centrum danych działają na maszynach wirtualnych VMware. Kontrolery domeny w lokalnych oddziałach działają na serwerach fizycznych.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Krok 1. Kupowanie i subskrybowanie na platformie Azure

Firma Contoso musi ustalić, jak kupić platformę Azure, utworzyć architekturę subskrypcji oraz jak licencjonować usługi i zasoby.

### <a name="buy-azure"></a>Kupowanie platformy Azure

Firma Contoso rejestruje się w [Umowa Enterprise (EA)](https://azure.microsoft.com/pricing/enterprise-agreement). Niniejsza Umowa obejmuje zobowiązanie pieniężne z góry na platformę Azure, entitling contoso, aby uzyskać korzyści, w tym elastyczne opcje rozliczeń i zoptymalizowane ceny.

- Firma Contoso oszacowała swoje przewidywane roczne wydatki na platformę Azure. Po podpisaniu umowy firma Contoso zapłaciła za pierwszy rok w całości.
- Firma Contoso musi wykorzystać całość zobowiązania przed upływem roku lub utraci ich niewykorzystaną wartość.
- Jeśli z jakiegoś powodu firma Contoso przekroczy swoje zobowiązanie i wyda więcej, firma Microsoft wystawi fakturę za nadwyżkę.
- W przypadku wszelkich kosztów przekraczających zobowiązanie będą obowiązywały te same stawki, które określono w umowie z firmą Contoso. Nie ma kar za przekroczenie zobowiązania.

### <a name="manage-subscriptions"></a>Zarządzanie subskrypcjami

Po zapłaceniu za platformę Azure firma Contoso musi ustalić, jak zarządzać subskrypcjami platformy Azure. Firma Contoso ma umowę EA i w rezultacie nie ma limitu liczby subskrypcji platformy Azure, które może skonfigurować.

- Rejestracja w usłudze Azure Enterprise określa sposób, w jaki firma kształtuje usługi platformy Azure i korzysta z nich, a także definiuje podstawową strukturę ładu.
- W pierwszym kroku firma Contoso zdefiniowała strukturę nazywaną „szkieletem przedsiębiorstwa” na potrzeby rejestracji Enterprise. Firma Contoso użyła [wskazówek dotyczących szkieletu przedsiębiorstwa platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) , aby ułatwić zrozumienie i projektowanie szkieletu.
- Na razie firma Contoso postanowiła wykorzystać podejście funkcjonalne do zarządzania subskrypcjami.
  - W ramach przedsiębiorstwa będzie używać jednego działu IT, który kontroluje budżet platformy Azure. Będzie to jedyna grupa z subskrypcjami.
  - Firma Contoso rozszerzy ten model w przyszłości, tak aby inne grupy firmowe mogły dołączyć jako działy w ramach rejestracji Enterprise.
  - W dziale IT firma Contoso ma dwie subskrypcje, produkcję i rozwój.
  - Jeśli firma Contoso wymaga dodatkowych subskrypcji w przyszłości, musi zarządzać dostępem, zasadami i zgodnością dla tych subskrypcji. Będzie to możliwe dzięki wprowadzeniu [grup zarządzania platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview) jako dodatkowej warstwy ponad subskrypcjami.

  ![Struktura przedsiębiorstwa](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Sprawdzanie licencjonowania

Po skonfigurowaniu subskrypcji firma Contoso może przyjrzeć się licencjonowaniu firmy Microsoft. Strategia licencjonowania będzie zależeć od zasobów, które firma Contoso chce zmigrować na platformę Azure oraz jak są wybierane i wdrażane maszyny wirtualne i usługi na platformie Azure.

#### <a name="azure-hybrid-benefit"></a>Korzyść użycia hybrydowego platformy Azure

W przypadku wdrażania maszyn wirtualnych na platformie Azure obrazy standardowe obejmują licencję, która spowoduje obciążanie firmy Contoso opłatami za każdą minutę korzystania z oprogramowania. Firma Contoso jest jednak długoterminowym klientem firmy Microsoft i utrzymywała umowy EA oraz licencje Open z pakietem Software Assurance (SA).

Korzyść użycia hybrydowego platformy Azure zapewnia ekonomiczną metodę migracji, dzięki czemu firma Contoso może zaoszczędzić na maszynach wirtualnych platformy Azure i SQL Server obciążeniach, konwertując lub używając licencji systemu Windows Server Datacenter i Standard Edition objętych pakietem Software Assurance. Dzięki temu firma Contoso może uregulować niższą podstawową stawkę obliczeniową dla maszyn wirtualnych i SQL Server. Aby uzyskać więcej informacji, zobacz [korzyść użycia hybrydowego platformy Azure](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>Przenośność licencji

Przenośność licencji w ramach programu Software Assurance zapewnia klientom licencjonowania zbiorowego firmy Microsoft, jak firma Contoso pozwala na wdrażanie kwalifikujących się aplikacji serwera przy użyciu aktywnego skojarzenia zabezpieczeń na platformie Azure. Eliminuje to konieczność kupowania nowych licencji. Brak powiązanych opłat za przenośność umożliwia łatwe wdrożenie istniejących licencji na platformie Azure. Aby uzyskać więcej informacji, zobacz [Przenośność licencji w ramach programu Software Assurance na platformie Azure](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Rezerwacja wystąpień dla przewidywalnych obciążeń

Przewidywalne obciążenia to te, które zawsze muszą być dostępne z działającymi maszynami wirtualnymi. Na przykład aplikacje biznesowe, takie jak system SAP ERP. Z kolei nieprzewidywalne obciążenia są zmiennymi, takimi jak maszyny wirtualne, które są włączone podczas wysokiego zapotrzebowania i wyłączone, gdy zapotrzebowanie jest niskie.

![Wystąpienie zarezerwowane](./media/contoso-migration-infrastructure/reserved-instance.png)

W programie Exchange for using zarezerwowane wystąpienia dla konkretnych wystąpień maszyn wirtualnych muszą być utrzymywane przez długi czas, a firma Contoso może uzyskać rabat i priorytetową pojemność. Użycie [wystąpień zarezerwowanych na platformie Azure](https://azure.microsoft.com/pricing/reserved-vm-instances) wraz z korzyść użycia hybrydowego platformy Azure może zaoszczędzić firmie Contoso do 82% od zwykłego cennika płatność zgodnie z rzeczywistym użyciem (od 2018 kwietnia).

## <a name="step-2-manage-hybrid-identity"></a>Krok 2. Zarządzanie tożsamością hybrydową

Udzielanie i kontrolowanie dostępu użytkowników do zasobów platformy Azure za pomocą zarządzania dostępem i tożsamościami (IAM) to ważny krok podczas składania infrastruktury platformy Azure.

- Firma Contoso decyduje się rozszerzyć lokalną usługę Active Directory na chmurę zamiast tworzyć nowy oddzielny system na platformie Azure.
- W tym celu tworzy usługę Active Directory opartą na platformie Azure.
- Firma Contoso nie ma usługi Office 365, dlatego musi zainicjować obsługę administracyjną nowej usługi Azure AD.
- Usługa Office 365 używa usługi Azure AD do zarządzania użytkownikami. Jeśli firma Contoso korzystała z usługi Office 365, ma już dzierżawę usługi Azure AD i może użyć tej usługi jako katalogu głównego.
- Dowiedz się więcej o [usłudze Azure AD dla pakietu Office 365](https://docs.microsoft.com/office365/enterprise/about-office-365-identity).
- Dowiedz się, jak [dodać subskrypcję do istniejącej dzierżawy usługi Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory).

### <a name="create-an-azure-ad-directory"></a>Tworzenie katalogu usługi Azure AD

Firma Contoso używa bezpłatnej wersji usługi Azure AD, która jest oferowana w ramach subskrypcji platformy Azure. Administratorzy contoso tworzą katalog usługi Azure AD:

1. W witrynie [Azure Portal](https://portal.azure.com) przechodzą do pozycji **Utwórz zasób** > **Tożsamość** > **Azure Active Directory**.
2. W obszarze **Utwórz katalog**Podaj nazwę katalogu, początkową nazwę domeny i region, w którym ma zostać utworzony katalog.

    ![Tworzenie katalogu usługi Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > Utworzony katalog ma początkową nazwę domeny w formularzu `domain-name.onmicrosoft.com` . Nazwy nie można zmienić ani usunąć. Zamiast tego należy dodać zarejestrowaną nazwę domeny do usługi Azure AD.

### <a name="add-the-domain-name"></a>Dodawanie nazwy domeny

Aby móc używać swojej standardowej nazwy domeny, administratorzy firmy Contoso muszą dodać ją jako niestandardową nazwę domeny do usługi Azure AD. Ta opcja umożliwia przypisanie przyjaznych nazw użytkowników. Na przykład użytkownik może zalogować się przy użyciu adresu e-mail `billg@contoso.com` zamiast `billg@contosomigration.microsoft.com` .

Aby skonfigurować niestandardową nazwę domeny, Dodaj ją do katalogu, Dodaj wpis DNS, a następnie Sprawdź nazwę w usłudze Azure AD.

1. W obszarze **niestandardowe nazwy domen**  >  **Dodaj domenę niestandardową**dodają domenę.
2. Aby można było użyć wpisu DNS na platformie Azure, należy zarejestrować go za pomocą swojego rejestratora domen.

    - Na liście **Niestandardowe nazwy domen** widzą informacje DNS dotyczące nazwy i notują je. Używany jest wpis MX.
    - Aby to zrobić, potrzebują dostępu do serwera nazw. Zalogowanie się w `contoso.com` domenie i utworzenie nowego rekordu MX dla wpisu DNS dostarczonego przez usługę Azure AD, z uwzględnieniem wymienionych informacji.

3. Po propagacji rekordów DNS w nazwie szczegółów domeny wybierają przycisk **Weryfikuj**, aby sprawdzić niestandardową nazwę domeny.

     ![Wpis DNS usługi Azure AD](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Konfigurowanie lokalnych i grup i użytkowników platformy Azure

Po ustanowieniu katalogu usługi Azure AD Administratorzy firmy Contoso muszą dodać pracowników do lokalnych grup Active Directory, które będą synchronizowane z usługą Azure AD. Powinni używać nazw grup lokalnych odpowiadających nazwom grup zasobów na platformie Azure. Ułatwi to identyfikowanie dopasowań na potrzeby synchronizacji.

#### <a name="create-resource-groups-in-azure"></a>Tworzenie grup zasobów na platformie Azure

W grupach zasobów platformy umieszczane są zasoby platformy Azure. Użycie identyfikatora grupy zasobów umożliwia platformie Azure wykonywanie operacji na zasobach należących do grupy.

- Subskrypcja platformy Azure może mieć wiele grup zasobów. Grupa zasobów istnieje w jednej subskrypcji.
- Ponadto jedna grupa zasobów może mieć wiele zasobów. Zasób należy do pojedynczej grupy zasobów.

Administratorzy firmy Contoso konfigurują grupy zasobów platformy Azure, jak pokazano w poniższej tabeli.

<!-- markdownlint-disable MD033 -->

| Grupa zasobów | Szczegóły |
| --- | --- |
| `ContosoCobRG` | Ta grupa zawiera wszystkie zasoby związane z ciągłością działania. Obejmuje ona magazyny, których firma Contoso będzie używać na potrzeby usługi Azure Site Recovery i usługi Azure Backup. <br><br> Obejmuje również zasoby używane do migracji, w tym usługę Azure Migrate i usługę Azure Database Migration Service. |
| `ContosoDevRG` | Ta grupa zawiera zasoby deweloperskie i testowe. |
| `ContosoFailoverRG` | Ta grupa służy jako strefa docelowa dla zasobów w trybie failover. |
| `ContosoNetworkingRG` | Ta grupa zawiera wszystkie zasoby sieciowe. |
| `ContosoRG` | Ta grupa zawiera zasoby związane z aplikacjami produkcyjnymi i bazami danych. |

<!-- markdownlint-disable MD026 -->

Administratorzy tworzą grupy zasobów w następujący sposób:

1. W witrynie Azure Portal > **Grupy zasobów** dodają grupę.
2. Dla każdej grupy określają nazwę, subskrypcję, do której należy Grupa, oraz region.
3. Grupy zasobów są wyświetlane na liście **Grupy zasobów**.

  ![Grupy zasobów](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scale-resource-groups"></a>Skalowanie grup zasobów

W przyszłości firma Contoso doda inne grupy zasobów w zależności od potrzeb. Może na przykład zdefiniować grupy zasobów dla poszczególnych aplikacji lub usług, aby każda mogła być zarządzana i zabezpieczana niezależnie.

#### <a name="create-matching-security-groups-on-premises"></a>Tworzenie zgodnych grup zabezpieczeń w środowisku lokalnym

1. W lokalnej usłudze Active Directory administratorzy firmy Contoso konfigurują grupy zabezpieczeń o nazwach zgodnych z nazwami grup zasobów platformy Azure.

    ![Grupy zabezpieczeń lokalnej usługi Active Directory](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. Na potrzeby zarządzania tworzą dodatkową grupę, która zostanie dodana do wszystkich innych grup. Ta grupa będzie miała uprawnienia do wszystkich grup zasobów na platformie Azure. Do tej grupy zostanie dodana ograniczona liczba administratorów globalnych.

### <a name="synchronize-active-directory"></a>Synchronizowanie usługi Active Directory

Firma Contoso chce zapewnić wspólną tożsamość na potrzeby uzyskiwania dostępu do zasobów lokalnych i w chmurze. W tym celu zintegruje lokalną usługę Active Directory z usługą Azure AD. W tym modelu:

- Użytkownicy i organizacje mogą korzystać z jednej tożsamości, aby uzyskiwać dostęp do aplikacji lokalnych i usług w chmurze, takich jak usługa Office 365, lub tysięcy innych witryn w Internecie.
- Administratorzy mogą używać grup w usłudze Active Directory do zaimplementowania [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) na platformie Azure.

Aby ułatwić integrację, firma Contoso używa [narzędzia Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Po zainstalowaniu i skonfigurowaniu narzędzia na kontrolerze domeny program zsynchronizuje lokalne tożsamości Active Directory z usługą Azure AD.

### <a name="download-the-tool"></a>Pobieranie narzędzia

1. W Azure Portal Administratorzy contoso przejdą do **Azure Active Directory**  >  **Azure AD Connect**i pobierają najnowszą wersję narzędzia do serwera, którego używają do synchronizacji.

    ![Pobieranie programu Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. Rozpoczynają `AzureADConnect.msi` instalację przy użyciu **ustawień ekspresowych**. Jest to najbardziej Typowa instalacja, która może być używana dla topologii z jednym lasem z synchronizacją skrótu hasła do uwierzytelniania.

    ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. Na ekranie **Łączenie z usługą Azure AD** określają poświadczenia do nawiązywania połączenia z usługą Azure AD (w postaci `admin@contoso.com` lub `admin@contoso.onmicrosoft.com`).

    ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. W obszarze **Połącz z AD DS**określają one poświadczenia dla Active Directory lokalnych (w postaci `CONTOSO\admin` lub `contoso.com\admin` ).

     ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. Na ekranie **Wszystko gotowe do skonfigurowania** wybierają pozycję **Uruchom proces synchronizacji po ukończeniu konfiguracji**, aby natychmiast uruchomić synchronizację. Następnie uruchamiają instalację.

    . Weź pod uwagę następujące kwestie:
  
    - Firma Contoso ma połączenie bezpośrednie z platformą Azure. Jeśli lokalny Active Directory znajduje się za serwerem proxy, przejrzyj temat [Rozwiązywanie problemów z łącznością z usługą Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity).

    - Po pierwszej synchronizacji obiekty z lokalnej usługi Active Directory są widoczne w katalogu usługi Azure AD.

      ![Lokalna usługa Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

    - Zespół IT firmy Contoso jest reprezentowany w każdej grupie, na podstawie roli.

      ![Członkowie lokalnej usługi Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Konfigurowanie kontroli dostępu opartej na rolach (RBAC)

[Kontrola dostępu oparta na rolach (RBAC) na](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) platformie Azure umożliwia precyzyjne zarządzanie dostępem na platformie Azure. Korzystając z modelu RBAC, można udzielić użytkownikom tylko takiego dostępu, jakiego potrzebują do wykonania swoich zadań. Odpowiednią rolę RBAC do użytkowników, grup i aplikacji należy przypisać na poziomie zakresu. Zakresem przypisania roli może być subskrypcja, grupa zasobów lub pojedynczy zasób.

Administratorzy firmy Contoso przypisują role do grup Active Directory, które są zsynchronizowane z lokalnego.

1. W `ControlCobRG` grupie zasobów wybierają pozycję **Kontrola dostępu (IAM)**  >  **Dodaj przypisanie roli**.
2. W obszarze **Dodaj rolę przypisania roli**  >  **Role**, > **współautor**, wybierają `ContosoCobRG` grupę z listy. Grupa zostanie wyświetlona na liście **Wybrani członkowie**.
3. Powtarzają one te same uprawnienia dla innych grup zasobów (z wyjątkiem programu `ContosoAzureAdmins` ), dodając `Contributor` uprawnienia do konta, które jest zgodne z grupą zasobów.
4. Dla `ContosoAzureAdmins` grupy przypisuje `Owner` rolę.

    ![Członkowie lokalnej usługi Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Krok 3. Projektowanie pod kątem odporności

### <a name="set-up-regions"></a>Konfigurowanie regionów

Zasoby platformy Azure są wdrażane w regionach.

- Regiony są zorganizowane w lokalizacje geograficzne, a wymagania dotyczące oddziałów danych, suwerenności, zgodności i odporności są honorowane w granicach geograficznych.
- Region składa się z zestawu centrów danych. Te centra danych są wdrożone wewnątrz obwodu o zdefiniowanym opóźnieniu i połączone za pośrednictwem dedykowanej regionalnej sieci o małych opóźnieniach.
- Każdy region świadczenia usługi Azure jest sparowany z innym regionem w celu zapewnienia odporności.
- Przeczytaj więcej na temat [regionów świadczenia usługi Azure](https://azure.microsoft.com/global-infrastructure/regions) i dowiedz się, [jak regiony są sparowane](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Firma Contoso zdecydowała się użyć `East US 2` (znajdującej się w Wirginia) jako regionu podstawowego i `Central US` (znajdującego się w Iowa) jako regionu pomocniczego z kilku powodów:

- Centrum danych firmy Contoso znajduje się w Nowym Jorku, a firma Contoso brała pod uwagę opóźnienie do najbliższego centrum danych.
- `East US 2`ma wszystkie usługi i produkty, których potrzebuje firma Contoso. Nie wszystkie regiony platformy Azure mają dostępne te same produkty i usługi. Aby uzyskać więcej informacji, zobacz [produkty platformy Azure według regionów](https://azure.microsoft.com/global-infrastructure/services).
- `Central US`to region sparowany na platformie Azure dla `East US 2` .

Myśląc o środowisku hybrydowym, firma Contoso musi rozważyć, jak wbudować odporność i strategię odzyskiwania po awarii w projekt regionów. Szeroka strategia obejmuje zakres od wdrożenia z jednym regionem, który opiera się na funkcjach platformy Azure, takich jak domeny błędów i wielowymiarowe parowanie w celu odporności, przez cały model aktywny-aktywny, w którym usługi Cloud Services i baza danych są wdrażane i obsługują użytkowników z dwóch regionów.

Firma Contoso zdecydowała się na środkową drogę. Wdraża aplikacje i zasoby w regionie podstawowym, a także zachowuje pełną kopię infrastruktury w regionie pomocniczym, dzięki czemu będzie ona gotowa do działania jako pełna kopia zapasowa w przypadku wystąpienia kompletnego błędu aplikacji lub awarii regionalnej.

### <a name="set-up-availability"></a>Konfigurowanie dostępności

**Zestawy dostępności:**

Zestawy dostępności pomagają chronić aplikacje i dane przed awariami sprzętu lokalnego i sieci w centrum danych.

- Zestawy dostępności rozpraszają maszyny wirtualne platformy Azure na różny sprzęt fizyczny w centrum danych.
- Domeny błędów reprezentują odpowiednie elementy sprzętu korzystające ze wspólnego źródła zasilania i przełącznika sieciowego w centrum danych. Maszyny wirtualne w zestawie dostępności są rozproszone między różne domeny błędów, aby zminimalizować wyłączenia spowodowane pojedynczą awarią sprzętu lub sieci.
- Domeny aktualizacji reprezentują odpowiednie elementy sprzętu, które mogą być poddawane konserwacji lub ponownie uruchamiane w tym samym czasie. Zestawy dostępności również rozpraszają maszyny wirtualne między wiele domen aktualizacji, aby upewnić się, że co najmniej jedno wystąpienie będzie działać przez cały czas.

Firma Contoso będzie implementować zestawy dostępności zawsze, gdy obciążenia maszyn wirtualnych wymagają wysokiej dostępności. Aby uzyskać więcej informacji, zobacz [Zarządzanie dostępnością maszyn wirtualnych z systemem Windows na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Strefy dostępności:**

Strefy dostępności pomagają chronić aplikacje i dane przed awariami wpływającymi na całe centrum danych w regionie.

- Każda strefa dostępności reprezentuje unikatową lokalizację fizyczną w regionie świadczenia usługi Azure.
- Każda strefa składa się z co najmniej jednego centrum danych wyposażonego w niezależne zasilanie, chłodzenie i sieć.
- Istnieją co najmniej trzy osobne strefy we wszystkich włączonych regionach.
- Fizyczna separacja stref w ramach regionu chroni aplikacje i dane przed awariami centrum danych.

Firma Contoso będzie wdrażać strefy dostępności, ponieważ aplikacje wymagają skalowalności, wysokiej dostępności i odporności. Aby uzyskać więcej informacji, zobacz [regiony i strefy dostępności na platformie Azure](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="configure-backup"></a>Konfigurowanie kopii zapasowych

**Azure Backup:**

Usługa Azure Backup umożliwia tworzenie kopii zapasowych i przywracanie dysków maszyn wirtualnych platformy Azure.

- Usługa Azure Backup umożliwia automatyczne tworzenie kopii zapasowych obrazów dysków maszyn wirtualnych przechowywanych w usłudze Azure Storage.
- Kopie zapasowe są spójne na poziomie aplikacji, co gwarantuje, że kopia zapasowa danych jest spójna transakcyjnie i że aplikacje będą uruchamiały się po przywróceniu.
- Azure Backup obsługuje Magazyn lokalnie nadmiarowy (LRS), aby replikować wiele kopii danych kopii zapasowej w ramach programu w przypadku wystąpienia awarii sprzętu lokalnego.
- Jeśli wystąpi awaria regionalna, Azure Backup obsługuje także magazyn Geograficznie nadmiarowy (GRS), co umożliwia replikowanie danych kopii zapasowej do pomocniczego regionu.
- Azure Backup szyfruje dane podczas przesyłania przy użyciu algorytmu AES-256. Kopie zapasowe danych są szyfrowane przy użyciu [szyfrowanie usługi Storage (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).

Firma Contoso będzie używać Azure Backup z GRS na wszystkich maszynach produkcyjnych w środowisku produkcyjnym, aby zapewnić, że kopie zapasowe danych obciążenia są tworzone i można je szybko przywrócić, jeśli wystąpi zakłócenie. Aby uzyskać więcej informacji, zobacz [omówienie Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

### <a name="set-up-disaster-recovery"></a>Konfigurowanie odzyskiwania po awarii

**Azure Site Recovery:**

Usługa Azure Site Recovery pomaga zapewnić ciągłość działania dzięki utrzymywaniu działania aplikacji biznesowych i obciążeń podczas regionalnych awarii.

- Azure Site Recovery ciągle replikuje maszyny wirtualne platformy Azure z poziomu podstawowego do regionu pomocniczego, zapewniając jednocześnie kopie funkcjonalne w obu lokalizacjach.
- W przypadku awarii w regionie podstawowym aplikacja lub usługa przechodzi w tryb failover w celu użycia wystąpień maszyn wirtualnych replikowanych w regionie pomocniczym, co minimalizuje potencjalne zakłócenia.
- Kiedy operacje wrócą do normalnego działania, aplikacje i usługi mogą powrócić po awarii na maszyny wirtualne w regionie podstawowym.

Firma Contoso zaimplementuje [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) dla wszystkich produkcyjnych maszyn wirtualnych używanych w obciążeniach o znaczeniu krytycznym, co zapewnia minimalne zakłócenia podczas przestoju w regionie podstawowym.

## <a name="step-4-design-a-network-infrastructure"></a>Krok 4. Projektowanie infrastruktury sieciowej

Po wdrożeniu projektu regionalnego firma Contoso jest gotowa do rozważenia strategii sieci. Należy wziąć pod uwagę sposób, w jaki lokalne centrum danych i platforma Azure łączą się i komunikują ze sobą, oraz sposób projektowania infrastruktury sieci na platformie Azure. Firma Contoso musi:

- **Planowanie hybrydowej łączności sieciowej.** Firma musi ustalić, w jaki sposób zamierza połączyć sieci w środowisku lokalnym i na platformie Azure.
- **Zaprojektować infrastrukturę sieci platformy Azure.** Oznacza to podjęcie decyzji odnośnie sposobu wdrożenia sieci w regionach. Jak sieci będą komunikowały się w obrębie tego samego regionu i w różnych regionach?
- **Projektuj i Konfiguruj sieci platformy Azure.** Musi skonfigurować sieci i podsieci platformy Azure, a następnie zdecydować, co będzie się w nich znajdować.

### <a name="plan-hybrid-network-connectivity"></a>Planowanie hybrydowej łączności sieciowej

Firma Contoso rozważała [wiele architektur](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) dla sieci hybrydowej między platformą Azure a lokalnym centrum danych. Aby uzyskać więcej informacji, zobacz [Wybieranie rozwiązania do łączenia sieci lokalnej z platformą Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations).

Z uwagi na to, że infrastruktura sieci lokalnej contoso składa się obecnie z centrum danych w Nowym Jorku i lokalnych gałęzi w wschodniej połowie USA. Wszystkie lokalizacje mają połączenie klasy biznesowej z Internetem. Każdy oddział jest następnie połączony z centrum danych za pośrednictwem tunelu IPSec VPN przez Internet.

![Sieć firmy Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

Oto, jak firma Contoso zdecydowała się wdrożyć łączność hybrydową:

1. Skonfiguruje nowe połączenie sieci VPN typu lokacja-lokacja między centrum danych firmy Contoso w Nowym Jorku i dwoma regionami świadczenia usługi Azure w regionach Wschodnie stany USA 2 i Środkowe stany USA.
2. Ruch oddziału powiązany z sieciami wirtualnymi na platformie Azure będzie kierowany przez główne centrum danych firmy Contoso.
3. Kiedy firma Contoso przeprowadzi skalowanie w górę wdrożenia platformy Azure, ustanowi połączenie ExpressRoute między centrum danych i regionami świadczenia usługi Azure. Gdy to się stanie, Contoso pozostawi połączenie sieci VPN typu lokacja-lokacja tylko do celów związanych z trybem failover.
    - Dowiedz się więcej [na temat wybierania między rozwiązaniem hybrydowym sieci VPN i ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations).
    - Sprawdź [lokalizacje i obsługę usługi ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**Tylko sieć VPN:**

![Sieć VPN firmy Contoso](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**Sieć VPN i usługa ExpressRoute:**

![Sieć VPN firmy Contoso/usługa ExpressRoute](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Projektowanie infrastruktury sieci platformy Azure

Konfiguracja sieci firmy Contoso musi zapewnić bezpieczeństwo i skalowalność wdrożenia hybrydowego. Firma Contoso podejmuje długoterminowe podejście do tego, projektowanie sieci wirtualnych jako odporne na awarie i gotowe do używania w przedsiębiorstwie. Aby uzyskać więcej informacji, zobacz [Planowanie sieci wirtualnych](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm).

Aby połączyć dwa regiony, firma Contoso Zaimplementuj model sieci typu centrum-Hub:

- W każdym regionie będzie używany model gwiazdy.
- Do połączenia sieci i piast Contoso będzie używać komunikacji równorzędnej sieci platformy Azure.

#### <a name="network-peering"></a>Komunikacja równorzędna sieci

[Komunikacja równorzędna sieci wirtualnych](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) w systemie Azure łączy sieci wirtualne i centra. Globalna komunikacja równorzędna umożliwia połączenia między siecią wirtualną lub koncentratorami w różnych regionach. Lokalna Komunikacja równorzędna łączy sieci wirtualne w tym samym regionie. Komunikacja równorzędna sieci wirtualnej zapewnia kilka zalet:

- Ruch sieciowy między sieciami wirtualnymi w komunikacji równorzędnej jest prywatny.
- Ruch między sieciami wirtualnymi jest utrzymywany w sieci szkieletowej firmy Microsoft. Do komunikacji między sieciami wirtualnymi nie jest wymagany publiczny Internet, bramy ani szyfrowanie.
- Komunikacja równorzędna zapewnia domyślne połączenie o małych opóźnieniach i dużej przepustowości między zasobami w różnych sieciach wirtualnych.

#### <a name="hub-to-hub-across-regions"></a>Połączenie między piastami w różnych regionach

Firma Contoso wdroży piastę w każdym regionie. Koncentrator jest siecią wirtualną na platformie Azure, która działa jako centralny punkt łączności z siecią lokalną. Sieci wirtualne piasty będą łączyć się ze sobą przy użyciu globalnej komunikacji równorzędnej sieci wirtualnych. Globalna komunikacja równorzędna sieci wirtualnych łączy sieci wirtualne w różnych regionach świadczenia usługi Azure.

- Piasta w każdym regionie jest połączona za pomocą komunikacji równorzędnej z partnerską piastą w innym regionie.
- Piasta jest połączona za pomocą komunikacji równorzędnej z każdą siecią w swoim regionie i może połączyć się ze wszystkimi zasobami sieciowymi.

    ![Globalna komunikacja równorzędna](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Model gwiazdy w obrębie regionu

W każdym regionie firma Contoso wdroży sieci wirtualne przeznaczone do różnych celów, jako sieci będące szprychami piasty regionu. Sieci wirtualne w regionie używają komunikacji równorzędnej do łączenia się ze swoją piastą i między sobą.

#### <a name="design-the-hub-network"></a>Projektowanie sieci piasty

W modelu gwiazdy wybranym przez firmę Contoso należy przemyśleć sposób, w jaki będzie kierowany ruch z lokalnego centrum danych i z Internetu. Oto, jak firma Contoso zdecydowała się obsługiwać Routing zarówno dla `East US 2` centrów, jak i `Central US` :

- Firma Contoso opracowuje sieć, która pozwala na ruch z Internetu, a także z sieci firmowej przy użyciu sieci VPN z platformą Azure.
- Architektura sieci ma dwie granice: niezaufaną strefę obwodową frontonu i strefę zaufaną zaplecza.
- Zapora będzie miała kartę sieciową w każdej strefie, kontrolując dostęp do stref zaufanych.
- Z Internetu:
  - Ruch z Internetu osiągnie publiczny adres IP ze zrównoważonym obciążeniem w sieci obwodowej.
  - Ten ruch jest kierowany przez zaporę i podlega regułom zapory.
  - Po zaimplementowaniu mechanizmów kontroli dostępu do sieci ruch zostanie przekazany do odpowiedniej lokalizacji w zaufanej strefie.
  - Ruch wychodzący z sieci wirtualnej będzie kierowany do Internetu przy użyciu tras zdefiniowanych przez użytkownika. Ruch jest wymuszany przez zaporę i sprawdzany zgodnie z zasadami firmy Contoso.
- Z centrum danych firmy Contoso:
  - Ruch przychodzący przez sieć VPN typu lokacja-lokacja lub ExpressRoute trafi na publiczny adres IP bramy sieci VPN platformy Azure.
  - Ruch jest kierowany przez zaporę i podlega regułom zapory.
  - Po zastosowaniu reguł zapory ruch jest przekazywany dalej do wewnętrznego modułu równoważenia obciążenia (jednostka SKU w warstwie Standardowa) w zaufanej podsieci strefy wewnętrznej.
  - Ruch wychodzący z zaufanej podsieci do lokalnego centrum danych za pośrednictwem sieci VPN jest kierowany przez zaporę (i zastosowane reguły) przed przesłaniem za pośrednictwem połączenia sieci VPN typu lokacja-lokacja.

### <a name="design-and-set-up-azure-networks"></a>Projektowanie i konfigurowanie sieci platformy Azure

Po wdrożeniu topologii sieci i routingu firma Contoso jest gotowa do skonfigurowania sieci i podsieci platformy Azure.

- Firma Contoso zaimplementuje klasę sieci prywatnej na platformie Azure ( `10.0.0.0/8` ). To działa, ponieważ lokalnie ma przestrzeń adresową klasy B ( `172.160.0.0/16` ), więc firma Contoso może mieć pewność, że nie będzie nakładać się między zakresami adresów.
- Firma Contoso wdroży sieci wirtualnych w regionie podstawowym i pomocniczym.
- Firma Contoso będzie używać konwencji nazewnictwa, która zawiera prefiks `VNET` i skrót regionu `EUS2` lub `CUS` . Korzystając z tego standardu, sieci centrów zostaną nazwane `VNET-HUB-EUS2` (w `East US 2` regionie) i `VNET-HUB-CUS` (w `Central US` regionie).

#### <a name="virtual-networks-in-east-us-2"></a>Sieci wirtualne w`East US 2`

`East US 2`jest regionem podstawowym, który będzie używany przez firmę Contoso do wdrażania zasobów i usług. Oto, jak firma Contoso będzie projektować sieci w tym regionie:

- **Centrum:** Sieć wirtualna centrum w `East US 2` systemie jest traktowana jako podstawowa łączność z lokalnym centrum danych.
- **Sieci wirtualne:** Sieci wirtualnych szprych w programie `East US 2` może służyć do izolowania obciążeń w razie potrzeby. Oprócz sieci wirtualnej centrum firma Contoso będzie miała dwa szprychy sieci wirtualnych w `East US 2` :
  - `VNET-DEV-EUS2`. Ta sieć wirtualna zapewni zespołowi programistycznemu i testującemu w pełni funkcjonalną sieć dla projektów deweloperskich. Będzie działać jako produkcyjny obszar pilotażowy i będzie polegać na infrastrukturze produkcyjnej.
    - `VNET-PROD-EUS2`. W tej sieci będą znajdować się składniki produkcyjne IaaS platformy Azure.
  - Każda sieć wirtualna będzie miała własną unikatową przestrzeń adresową, bez nakładania się. Firma Contoso zamierza skonfigurować routing niewymagający używania translatora adresów sieciowych.
- **Podsieci**
  - W każdej sieci dla każdej warstwy aplikacji będzie podsieć.
  - Każda podsieć w sieci produkcyjnej będzie miała pasującą podsieć w sieci wirtualnej opracowywania.
  - Dodatkowo sieć produkcyjna ma podsieć dla kontrolerów domeny.

Sieci wirtualnych w programie `East US 2` zostały podsumowane w poniższej tabeli.

| **Environment** | **Zakresu** | **Element równorzędny** |
| --- | --- | --- |
| `VNET-HUB-EUS2` | `10.240.0.0/20` | `VNET-HUB-CUS2`, `VNET-DEV-EUS2`, `VNET-PROD-EUS2` |
| `VNET-DEV-EUS2` | `10.245.16.0/20` | `VNET-HUB-EUS2` |
| `VNET-PROD-EUS2` | `10.245.32.0/20` | `VNET-HUB-EUS2`, `VNET-PROD-CUS` |

![Model gwiazdy w regionie podstawowym](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Podsieci w `East US 2 Hub` sieci ( `VNET-HUB-EUS2` )

| Podsieć/strefa | CIDR | Możliwe do użycia adresy IP |
| --- | --- | --- |
| `IB-UntrustZone` | `10.240.0.0/24`  | 251 |
| `IB-TrustZone`   | `10.240.1.0/24`  | 251 |
| `OB-UntrustZone` | `10.240.2.0/24`  | 251 |
| `OB-TrustZone`   | `10.240.3.0/24`  | 251 |
| `GatewaySubnets` | `10.240.10.0/24` | 251 |

#### <a name="subnets-in-the-east-us-2-development-network-vnet-dev-eus2"></a>Podsieci w `East US 2` sieci programistycznej ( `VNET-DEV-EUS2` )

Sieć wirtualna opracowywania jest używana przez zespół programistyczny jako produkcyjny obszar pilotażowy. Ma trzy podsieci.

| Podsieć | CIDR | Addresses (Adresy) | W podsieci |
| --- | --- | --- | --- |
| `DEV-FE-EUS2` | `10.245.16.0/22` | 1019 | Maszyny wirtualne frontonu/warstwy internetowej |
| `DEV-APP-EUS2` | `10.245.20.0/22` | 1019 | Maszyny wirtualne warstwy aplikacji |
| `DEV-DB-EUS2` | `10.245.24.0/23` | 507 | Maszyny wirtualne bazy danych |

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Podsieci w `East US 2` sieci produkcyjnej ( `VNET-PROD-EUS2` )

Składniki IaaS platformy Azure znajdują się w sieci produkcyjnej. Każda warstwa aplikacji ma własną podsieć. Podsieci są zgodne z tymi w sieci deweloperskiej, a dodatkowo istnieje podsieć dla kontrolerów domeny.

| Podsieć | CIDR | Addresses (Adresy) | W podsieci |
| --- | --- | --- | --- |
| `PROD-FE-EUS2` | `10.245.32.0/22` | 1019 | Maszyny wirtualne frontonu/warstwy internetowej |
| `PROD-APP-EUS2` | `10.245.36.0/22` | 1019 | Maszyny wirtualne warstwy aplikacji |
| `PROD-DB-EUS2` | `10.245.40.0/23` | 507 | Maszyny wirtualne bazy danych |
| `PROD-DC-EUS2` | `10.245.42.0/24` | 251 | Maszyny wirtualne kontrolerów domeny |

![Architektura sieci piasty](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Sieci wirtualne w `Central US` (region pomocniczy)

`Central US`Czy jest to region pomocniczy firmy Contoso. Oto, jak firma Contoso zaprojektuje architekturę sieci w tym regionie:

- **Centrum:** Sieć wirtualna centrum w `Central US` systemie jest traktowana jako pomocniczy punkt łączności z lokalnym centrum danych, a szprycha sieci wirtualnych w programie `Central US` może służyć do izolowania obciążeń w razie potrzeby, zarządzane oddzielnie od innych szprych.
- **Sieci wirtualnych:** Firma Contoso będzie miała dwie sieci wirtualnych w `Central US` :
  - `VNET-PROD-CUS`: Ta sieć wirtualna jest siecią produkcyjną i można ją traktować jako pomocniczy centrum.
  - `VNET-ASR-CUS`: Ta sieć wirtualna działa jako lokalizacja, w której maszyny wirtualne są tworzone po przejściu w tryb failover z lokalizacji lokalnej, lub jako lokalizacja maszyn wirtualnych platformy Azure, które są przenoszone w trybie przełączenia z lokacji podstawowej do regionu pomocniczego. Ta sieć jest podobna do sieci produkcyjnych, ale nie ma w niej żadnych kontrolerów domeny.
  - Każda sieć wirtualna w regionie będzie mieć własną przestrzeń adresową, bez nakładania się. Firma Contoso skonfiguruje routing bez translatora adresów sieciowych.
- **Podsieci:** Podsieci zostaną zaprojektowane w podobny sposób do tych w programie `East US 2` .

Sieci wirtualnych w programie `Central US` są podsumowane w poniższej tabeli.

| VNet | Zakres | Element równorzędny |
| --- | --- | --- |
| **VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS |
| **VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS |
| **VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2 |

![Model gwiazdy w regionie sparowanym](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Podsieci w sieci piasty w regionie Środkowe stany USA (VNET-HUB-CUS)

**Podsieci** | **CIDR** | **Możliwe do użycia adresy IP**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Podsieci w sieci produkcyjnej w regionie Środkowe stany USA (VNET-PROD-CUS)

Równolegle z siecią produkcyjną w podstawowym regionie Wschodnie stany USA 2 istnieje sieć produkcyjna w regionie pomocnicze stany USA.

| **Podsieci** | **CIDR** | **Addresses (Adresy)** | **W podsieci** |
| --- | --- | --- | --- |
| **PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej |
| **PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji |
| **PROD-DB-CUS** | 10.255.40.0/23 | 507 | Maszyny wirtualne bazy danych |
| **PROD-DC-CUS** | 10.255.42.0/24 | 251 | Maszyny wirtualne kontrolerów domeny |

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Podsieci w sieci trybu failover/odzyskiwania w regionie Środkowe stany USA (VNET-ASR-CUS)

Sieć VNET-ASR-CUS jest używana do celów przełączania w tryb failover między regionami. Usługa Site Recovery będzie używana do replikowania maszyn wirtualnych platformy Azure i przełączania ich w tryb failover między regionami. Działa ona również jako centrum danych firmy Contoso dla sieci platformy Azure w przypadku obciążeń chronionych, które pozostają w środowisku lokalnym, ale w trybie failover są przełączane na platformę Azure na potrzeby odzyskiwania po awarii.

Sieć VNET-ASR-CUS jest tą samą podstawową podsiecią co produkcyjna sieć wirtualna w regionie Wschodnie stany USA 2, ale nie potrzebuje podsieci kontrolera domeny.

| **Podsieci** | **CIDR** | **Addresses (Adresy)** | **W podsieci** |
| --- | --- | --- | --- |
| **ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej |
| **ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji |
| **ASR-DB-CUS** | 10.255.24.0/23 | 507 | Maszyny wirtualne bazy danych |

![Architektura sieci piasty](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Konfigurowanie połączeń komunikacji równorzędnej

Piasta w każdym regionie będzie połączona za pomocą komunikacji równorzędnej z piastą w drugim regionie i ze wszystkimi sieciami wirtualnymi w obrębie regionu piasty. Dzięki temu piasty mogą komunikować się i wyświetlać wszystkie sieci wirtualne w regionie. Należy pamiętać, że:

- Komunikacja równorzędna tworzy połączenie dwustronne. Jedno z inicjującego elementu równorzędnego w pierwszej sieci wirtualnej i drugie w drugiej sieci wirtualnej.
- We wdrożeniu hybrydowym ruch między elementami równorzędnymi musi być widoczny z połączenia sieci VPN między lokalnym centrum danych i platformą Azure. Aby to umożliwić, istnieją pewne określone ustawienia, które należy ustawić dla połączeń komunikacji równorzędnej.

W przypadku wszystkich połączeń z sieci wirtualnych szprych za pośrednictwem piasty do lokalnego centrum danych firma Contoso musi zezwolić na przekazywanie ruchu i przechodzenie między bramami sieci VPN.

##### <a name="domain-controller"></a>Kontroler domeny

W przypadku kontrolerów domeny w sieci VNET-PROD-EUS2 firma Contoso chce, aby ruch przepływał zarówno między piastą/siecią produkcyjną regionu EUS2, jak i za pośrednictwem połączenia sieci VPN do środowiska lokalnego. W tym celu Administratorzy contoso muszą zezwolić na następujące czynności:

1. **Zezwalaj na ruch przesłany dalej** i **Zezwalaj na tranzyt bramy** w połączeniu komunikacji równorzędnej. W naszym przykładzie jest to sieć wirtualna-HUB-EUS2 do połączenia VNET-EUS2.

    ![Komunikacja równorzędna](./media/contoso-migration-infrastructure/peering1.png)

2. **Zezwalaj na ruch przesłany dalej** i **Użyj bram zdalnych** po drugiej stronie komunikacji równorzędnej, w połączeniu sieci VNET-PROD-EUS2 z siecią VNET-HUB-EUS2.

    ![Komunikacja równorzędna](./media/contoso-migration-infrastructure/peering2.png)

3. Lokalnie firma skonfiguruje trasę statyczną, która kieruje ruch lokalny do trasy przez tunel VPN do sieci wirtualnej. Konfiguracja zostanie ukończona na bramie udostępniającej tunel VPN z firmy Contoso do platformy Azure. Do tego celu używana jest usługa RRAS.

    ![Komunikacja równorzędna](./media/contoso-migration-infrastructure/peering3.png)

##### <a name="production-networks"></a>Sieci produkcyjne

Sieć równorzędna będąca szprychą nie może widzieć sieci równorzędnej będącej szprychą w innym regionie za pośrednictwem piasty.

Aby jej sieci produkcyjne w obu regionach widziały siebie nawzajem, firma Contoso musi utworzyć połączenia komunikacji równorzędnej sieci VNET-PROD-EUS2 i VENT-PROD-CUS.

![Komunikacja równorzędna](./media/contoso-migration-infrastructure/peering4.png)

### <a name="set-up-dns"></a>Konfigurowanie systemu DNS

Podczas wdrażania zasobów w sieciach wirtualnych istnieje kilka możliwości rozpoznawania nazw domen. Można użyć usługi rozpoznawania nazw oferowanej przez platformę Azure lub udostępnić serwery DNS na potrzeby rozpoznawania nazw. Używany typ rozpoznawania nazw zależy od tego, w jaki sposób zasoby muszą komunikować się ze sobą. Uzyskaj [więcej informacji](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) na temat usługi Azure DNS.

Administratorzy firmy Contoso zdecydowali, że usługa Azure DNS nie jest dobrym wyborem w środowisku hybrydowym. Zamiast tego firma będzie korzystać z lokalnych serwerów DNS.

<!-- docsTest:ignore "on premises" -->

- Ponieważ jest to sieć hybrydowa, wszystkie maszyny wirtualne lokalnie i na platformie Azure muszą być w stanie rozpoznawać nazwy, aby działać prawidłowo. Oznacza to, że do wszystkich sieci wirtualnych należy zastosować niestandardowe ustawienia DNS.
- Firma Contoso wdrożyła kontrolery domen w centrum danych Contoso i w oddziałach. Podstawowe serwery DNS to CONTOSODC1 (172.16.0.10) i CONTOSODC2 (172.16.0.1).
- Po wdrożeniu sieci wirtualnych lokalne kontrolery domeny są konfigurowane jako serwery DNS w sieci.
- Jeśli dla sieci wirtualnej określono opcjonalny niestandardowy serwer DNS, wirtualny adres IP `168.63.129.16` dla tłumaczeń cyklicznych na platformie Azure musi być dodany do listy. W tym celu firma Contoso konfiguruje ustawienia serwera DNS w każdej sieci wirtualnej. Na przykład niestandardowe ustawienia DNS dla sieci VNET-HUB-EUS2 są następujące:

    ![Niestandardowe DNS](./media/contoso-migration-infrastructure/custom-dns.png)

Poza lokalnymi kontrolerami domeny firma Contoso wdraża cztery więcej kontrolerów domeny do obsługi sieci platformy Azure, dwa dla każdego regionu. Oto, co firma Contoso wdroży na platformie Azure.

| **Okolicy** | **Kontroler domeny** | **Environment** | **Podsieci** | **Adres IP** |
| --- | --- | --- | --- | --- |
| EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4 |
| EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5 |
| CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4 |
| CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4 |

Po wdrożeniu lokalnych kontrolerów domeny firma Contoso musi zaktualizować ustawienia DNS w sieciach w obu regionach w celu uwzględnienia nowych kontrolerów domeny na liście serwerów DNS.

#### <a name="set-up-domain-controllers-in-azure"></a>Konfigurowanie kontrolerów domeny na platformie Azure

Po zaktualizowaniu ustawień sieci administratorzy firmy Contoso są gotowi do utworzenia kontrolerów domeny na platformie Azure.

1. W witrynie Azure Portal wdrażają nową maszynę wirtualną z systemem Windows Server w odpowiedniej sieci wirtualnej.
2. [Tworzą one zestawy dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets) w każdej lokalizacji maszyny wirtualnej. Zestawy dostępności pełnią następujące funkcje:

    - Zapewniają, że sieć szkieletowa Azure rozdziela maszyny wirtualne w różnych infrastrukturach w regionie świadczenia usługi Azure.
    - Umożliwia firmie Contoso kwalifikowanie się do umowy SLA gwarantującej dostępność na poziomie 99,95% dla maszyn wirtualnych na platformie Azure.

    ![Grupa dostępności](./media/contoso-migration-infrastructure/availability-group.png)

3. Po wdrożeniu maszyny wirtualnej otwierają interfejs sieciowy maszyny wirtualnej. Ustawiają prywatny adres IP jako statyczny i określają prawidłowy adres.

    ![Karta sieciowa maszyny wirtualnej](./media/contoso-migration-infrastructure/vm-nic.png)

4. Teraz dołączają nowy dysk danych do maszyny wirtualnej. Ten dysk zawiera bazę danych usługi Active Directory i udział sysvol.
    - Od rozmiaru dysku będzie zależeć liczba operacji we/wy, które obsługuje.
    - W miarę upływu czasu i powiększania środowiska może być konieczne zwiększenie rozmiaru dysku.
    - Dysk nie powinien być ustawiony na Odczyt/zapis dla buforowania hosta. Bazy danych usługi Active Directory nie obsługują tego ustawienia.

     ![Dysk usługi Active Directory](./media/contoso-migration-infrastructure/ad-disk.png)

5. Po dodaniu dysku nawiązują połączenie z maszyną wirtualną za pośrednictwem Pulpitu zdalnego i otwierają Menedżera serwera.

6. Następnie w obszarze **Usługi plików i magazynowania** uruchamiają Kreator nowego woluminu, upewniając się, że dysk ma przypisaną literę F: lub wyższą na lokalnej maszynie wirtualnej.

     ![Kreator nowego woluminu](./media/contoso-migration-infrastructure/volume-wizard.png)

7. W Menedżerze serwera dodają rolę **Active Directory Domain Services**. Następnie konfigurują maszynę wirtualną jako kontrolera domeny.

      ![Rola serwera](./media/contoso-migration-infrastructure/server-role.png)

8. Po skonfigurowaniu maszyny wirtualnej jako kontrolera domeny i jej ponownym uruchomieniu otwierają Menedżera DNS i konfigurują program rozpoznawania nazw usługi Azure DNS jako usługę przesyłania dalej. Dzięki temu kontroler domeny może przekazywać dalej zapytania DNS, których nie może rozpoznać w usłudze Azure DNS.

    ![Usługa przesyłania dalej DNS](./media/contoso-migration-infrastructure/dns-forwarder.png)

9. Teraz aktualizują niestandardowe ustawienia DNS dla każdej sieci wirtualnej przy użyciu odpowiedniego kontrolera domeny dla regionu sieci wirtualnej. Uwzględniają lokalne kontrolery domeny na liście.

### <a name="set-up-active-directory"></a>Konfigurowanie usługi Active Directory

Usługa Active Directory jest usługą o znaczeniu krytycznym w sieci i musi być poprawnie skonfigurowana. Administratorzy firmy Contoso utworzą lokacje usługi Active Directory dla centrum danych firmy Contoso oraz dla regionów EUS2 i CUS.

1. Tworzą one dwie nowe lokacje ( `AZURE-EUS2` i `AZURE-CUS` ) wraz z witryną centrum danych ( `ContosoDatacenter` ).
2. Po utworzeniu lokacji tworzą podsieci w lokacjach w celu dopasowania do sieci wirtualnych i centrum danych.

    ![Podsieci kontrolerów domeny](./media/contoso-migration-infrastructure/dc-subnets.png)

3. Następnie tworzą dwa łącza lokacji, aby wszystko połączyć. Kontrolery domeny należy wtedy przenieść do ich lokalizacji.

    ![Łącza kontrolerów domeny](./media/contoso-migration-infrastructure/dc-links.png)

4. Po skonfigurowaniu wszystkich elementów topologia replikacji usługi Active Directory jest wdrożona.

    ![Replikacja kontrolerów domeny](./media/contoso-migration-infrastructure/ad-resolution.png)

5. Po zakończeniu wszystkiego lista kontrolerów domeny i lokacji jest wyświetlana w Centrum administracyjne usługi Active Directory lokalnej.

    ![Centrum administracyjne usługi Active Directory](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Krok 5. Planowanie zarządzania

Platforma Azure udostępnia szereg mechanizmów kontroli ładu w usługach i na platformie Azure. Aby uzyskać więcej informacji, zobacz [Opcje ładu platformy Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

Podczas konfigurowania tożsamości i kontroli dostępu firma Contoso zaczęła już implementować pewne aspekty ładu i bezpieczeństwa. Ogólnie istnieją trzy obszary, które należy wziąć pod uwagę:

- **Zasady:** Azure Policy stosuje i wymusza reguły oraz efekty dotyczące zasobów, dzięki czemu zasoby pozostają zgodne z wymaganiami firmy i umowy SLA.
- **Blokady:** System Azure umożliwia blokowanie subskrypcji, grup zasobów i innych zasobów, dzięki czemu mogą być modyfikowane tylko przez te osoby, które mają odpowiednie uprawnienia.
- **Tagi:** Zasoby można kontrolować, przeprowadzać inspekcję i zarządzać nimi za pomocą tagów. Tagi dołączają do zasobów metadane, dostarczając informacje o zasobach lub właścicielach.

### <a name="set-up-policies"></a>Konfigurowanie zasad

Usługa Azure Policy ocenia zasoby, skanując je pod kątem elementów niezgodnych z wdrożonymi definicjami zasad. Na przykład możesz mieć zasadę, która zezwala tylko na niektóre typy maszyn wirtualnych lub wymaga, aby zasoby miały określony tag.

Zasady określają definicję zasad, a przypisanie zasad określa zakres, w którym należy zastosować zasady. Zakresem może być zarówno grupa zarządzania, jak i grupa zasobów. [Dowiedz się więcej](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) na temat tworzenia zasad i zarządzania nimi.

Firma Contoso chce rozpocząć kilka zasad:

- Chce mieć pewność, że zasoby można wdrożyć tylko w regionach EUS2 i CUS.
- Chce ograniczyć jednostki SKU maszyn wirtualnych tylko do zatwierdzonych jednostek SKU. Celem jest upewnienie się, że kosztowne jednostki SKU maszyn wirtualnych nie są używane.

#### <a name="limit-resources-to-regions"></a>Ograniczanie zasobów do regionów

Firma Contoso używa wbudowanej definicji zasad **Dozwolone lokalizacje**, aby ograniczyć regiony zasobów.

1. W witrynie Azure Portal wybierz pozycję **Wszystkie usługi** i wyszukaj **Zasady**.
2. Wybierz pozycję **przypisania**  >  **Przypisz zasady**.
3. Na liście zasad wybierz pozycję **Dozwolone lokalizacje**.
4. W obszarze **Zakres** ustaw nazwę subskrypcji platformy Azure, a następnie wybierz dwa regiony z listy dozwolonych.

    ![Regiony dozwolone przez zasady](./media/contoso-migration-infrastructure/policy-region.png)

5. Domyślnym ustawieniem zasad jest **Odmów**, co oznacza, że jeśli ktoś rozpocznie wdrożenie w subskrypcji, która nie znajduje się w regionie EUS2 lub CUS, wdrożenie zakończy się niepowodzeniem. Oto co się stanie, jeśli ktoś z subskrypcji Contoso podejmie próbę skonfigurowania wdrożenia w regionie Zachodnie stany USA.

    ![Zasady nie powiodły się](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Zezwalanie na określone jednostki SKU maszyn wirtualnych

Firma Contoso użyje wbudowanej definicji zasad, `Allow virtual machine SKUs` Aby ograniczyć typy maszyn wirtualnych, które można utworzyć w ramach subskrypcji.

![Jednostka SKU zasad](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Sprawdzanie zgodności z zasadami

Zasady zaczynają obowiązywać natychmiast, a firma Contoso może sprawdzić zasoby pod kątem zgodności.

1. W witrynie Azure Portal wybierz link **Zgodność**.
2. Zostanie wyświetlony pulpit nawigacyjny zgodności. Możesz przejść do szczegółów, aby uzyskać więcej informacji.

    ![Zgodność z zasadami](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Konfigurowanie blokad

Firma Contoso długo używała struktury ITIL do zarządzania swoimi systemami. Jednym z najważniejszych aspektów struktury jest kontrola zmian, a firma Contoso chce się upewnić, że kontrola zmian zostanie zaimplementowana we wdrożeniu platformy Azure.

Firma Contoso będzie [blokować zasoby](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) w następujący sposób:

- Każdy składnik produkcyjny lub trybu failover musi znajdować się w grupie zasobów, która ma blokadę ReadOnly. Oznacza to, że aby zmodyfikować lub usunąć elementy produkcyjne, należy usunąć blokadę.
- Grupy zasobów nieprodukcyjnych będą mieć blokady CanNotDelete. Oznacza to, że autoryzowani użytkownicy mogą odczytywać lub modyfikować zasób, ale nie mogą go usunąć.

### <a name="set-up-tagging"></a>Konfigurowanie tagowania

Aby śledzić zasoby w miarę ich dodawania, coraz ważniejsze dla firmy Contoso będzie skojarzenie zasobów z odpowiednim działem, klientem i środowiskiem.

Oprócz dostarczania informacji o zasobach i właścicielach tagi umożliwią firmie Contoso agregowanie i grupowanie zasobów oraz używanie tych danych do celów obciążeń zwrotnych.

Firma Contoso musi wizualizować swoje zasoby platformy Azure w taki sposób, który ma sens dla firmy, na przykład według roli lub działu. Zwróć uwagę, że zasoby mogą współużytkować ten sam tag (być oznaczone tym samym tagiem), nawet jeśli nie znajdują się w tej samej grupie zasobów. Firma Contoso utworzy taksonomię tagów, dzięki czemu wszyscy będą korzystać z tych samych tagów.

| **Nazwa tagu** | **Wartość** |
| --- | --- |
| `CostCenter` | 12345: musi być prawidłowym centrum kosztów z platformy SAP. |
| `BusinessUnit` | Nazwa jednostki biznesowej (z oprogramowania SAP). Dopasowuje `CostCenter` . |
| `ApplicationTeam` | Alias adresu e-mail zespołu, który jest właścicielem pomocy technicznej dla aplikacji. |
| `CatalogName` | Nazwa aplikacji lub `ShareServices` dla katalogu usług obsługiwanego przez zasób. |
| `ServiceManager` | Alias adresu e-mail menedżera usługi ITIL dla zasobu. |
| `COBPriority` | Priorytet ustawiony przez firmę dla ciągłości działania i odzyskiwania po awarii. Wartości 1–5. |
| `ENV` | `DEV`, `STG` , i `PROD` są dozwolone wartości, reprezentujące projektowanie, przemieszczanie i produkcję. |

Na przykład:

 ![Tagi platformy Azure](./media/contoso-migration-infrastructure/azure-tag.png)

Po utworzeniu tagu firma Contoso wróci i utworzy nowe definicje i przypisania zasad, aby wymusić używanie wymaganych tagów w całej organizacji.

## <a name="step-6-consider-security"></a>Krok 6. Rozważ bezpieczeństwo

W chmurze bezpieczeństwo ma kluczowe znaczenie, a platforma Azure oferuje szeroką gamę narzędzi i możliwości zabezpieczeń. Ułatwiają one tworzenie bezpiecznych rozwiązań na bezpiecznej platformie Azure. Przeczytaj artykuł [Chmura, której można zaufać](https://azure.microsoft.com/overview/trusted-cloud), aby dowiedzieć się więcej o zabezpieczeniach platformy Azure.

Istnieje kilka aspektów, którymi firma Contoso musi się zająć:

- **Azure Security Center:** [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) zapewnia ujednolicone Zarządzanie zabezpieczeniami i zaawansowaną ochronę przed zagrożeniami w ramach obciążeń chmury hybrydowej. Służy do stosowania zasad zabezpieczeń w ramach obciążeń, ograniczania zagrożeń związanych z zagrożeniami oraz wykrywania i reagowania na ataki.
- **Sieciowe grupy zabezpieczeń:** [Sieciowe grupy zabezpieczeń (sieciowej grupy zabezpieczeń)](https://docs.microsoft.com/azure/virtual-network/security-overview) filtrują ruch sieciowy na podstawie listy reguł zabezpieczeń umożliwiających lub odrzucających ruch sieciowy do zasobów podłączonych do usługi Azure sieci wirtualnych.
- **Szyfrowanie danych:** [Azure Disk Encryption](https://docs.microsoft.com/azure/security/fundamentals/encryption-atrest) to funkcja, która ułatwia szyfrowanie dysków maszyn wirtualnych z systemami Windows i Linux IaaS.

### <a name="work-with-the-azure-security-center"></a>Praca z usługą Azure Security Center

Firma Contoso chce mieć szybki wgląd w stan zabezpieczeń swojej nowej chmury hybrydowej, a zwłaszcza obciążeń platformy Azure. W rezultacie firma Contoso zdecydowała się zaimplementować usługę Azure Security Center, rozpoczynając od następujących funkcji:

- Scentralizowane zarządzanie zasadami.
- Ciągła ocena.
- Rekomendacje z możliwością wykonania akcji.

#### <a name="centralize-policy-management"></a>Scentralizowane zarządzanie zasadami

Dzięki scentralizowanemu zarządzaniu zasadami firma Contoso będzie zapewniać zgodność z wymaganiami dotyczącymi zabezpieczeń, centralnie zarządzając zasadami zabezpieczeń w całym środowisku. Może po prostu i szybko zaimplementować zasady, które mają zastosowanie do wszystkich zasobów platformy Azure.

![Zasady zabezpieczeń](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Ocena i działanie

Firma Contoso będzie korzystać z ciągłej oceny zabezpieczeń, która monitoruje Bezpieczeństwo maszyn, sieci, magazynu, danych i aplikacji; w celu odnalezienia potencjalnych problemów z zabezpieczeniami.

- Security Center analizuje stan zabezpieczeń zasobów obliczeniowych firmy Contoso, infrastruktury i danych oraz aplikacji i usług platformy Azure.
- Ciągła ocena ułatwia zespołowi operacyjnemu firmy Contoso wykrywanie potencjalnych problemów z zabezpieczeniami, takich jak systemy bez aktualizacji zabezpieczeń lub uwidocznione porty sieciowe.
- W szczególności firma Contoso chce upewnić się, że wszystkie maszyny wirtualne są chronione. Usługa Security Center ułatwia to zadanie, sprawdzając kondycję maszyn wirtualnych i udostępniając praktyczne rekomendacje uszeregowane według priorytetu, które umożliwiają podjęcie działań w celu skorygowania luk w zabezpieczeniach, zanim zostaną wykorzystane.

![Monitorowanie](./media/contoso-migration-infrastructure/monitoring.png)

### <a name="work-with-nsgs"></a>Praca z sieciowymi grupami zabezpieczeń

Firma Contoso może ograniczyć ruch sieciowy do zasobów w sieci wirtualnej przy użyciu sieciowych grup zabezpieczeń.

- Grupa zabezpieczeń sieci zawiera listę reguł zabezpieczeń, które zezwalają na lub blokują przychodzący lub wychodzący ruch sieciowy na podstawie źródłowego lub docelowego adresu IP, portu i protokołu.
- Po zastosowaniu do podsieci reguły są stosowane do wszystkich zasobów w podsieci. Obok interfejsów sieciowych obejmuje to wystąpienia usług platformy Azure wdrożone w tej podsieci.
- Grupy zabezpieczeń aplikacji umożliwiają skonfigurowanie zabezpieczeń sieci jako naturalnego rozszerzenia struktury aplikacji, co pozwala na grupowanie maszyn wirtualnych i definiowanie zasad zabezpieczeń sieci na podstawie tych grup.
  - Grupy zabezpieczeń aplikacji oznaczają dla firmy Contoso możliwość ponownego używania zasad zabezpieczeń na dużą skalę bez ręcznej obsługi jawnych adresów IP. Platforma obsługuje złożoność jawnych adresów IP i wiele zestawów reguł, co pozwala skupić się na logice biznesowej.
  - Firma Contoso może określić grupę zabezpieczeń aplikacji jako źródło i obiekt docelowy reguły zabezpieczeń. Po zdefiniowaniu zasad zabezpieczeń firma Contoso może utworzyć maszyny wirtualne i przypisać karty sieciowe maszyn wirtualnych do grupy.

Firma Contoso zaimplementuje kombinację sieciowych grup zabezpieczeń i grup zabezpieczeń aplikacji. Niepokoi się o zarządzanie sieciowymi grupami zabezpieczeń. Obawia się nadużywania sieciowych grup zabezpieczeń i dodatkowej złożoności dla pracowników zespołu ds. operacji. Oto, co zrobi firma Contoso:

- Cały ruch do i z wszystkich podsieci (w pionie) będzie podlegać regule sieciowej grupy zabezpieczeń, z wyjątkiem podsieci GatewaySubnets w sieciach piasty.
- Wszystkie zapory i kontrolery domeny będą chronione za pomocą sieciowych grup zabezpieczeń podsieci i sieciowych grup zabezpieczeń kart sieciowych.
- Do wszystkich aplikacji produkcyjnych będą stosowane grupy zabezpieczeń aplikacji.

Firma Contoso utworzyła model pokazujący, jak to będzie wyglądać w przypadku jej aplikacji.

![Zabezpieczenia](./media/contoso-migration-infrastructure/asg.png)

Sieciowe grupy zabezpieczeń skojarzone z grupami zabezpieczeń aplikacji zostaną skonfigurowane z najniższymi uprawnieniami w celu zapewnienia, że tylko dozwolone pakiety mogą przepływać z jednej części sieci do jej lokalizacji docelowej.

| Akcja | Nazwa | Element źródłowy | Środowisko docelowe | Port |
| --- | --- | --- | --- | --- |
| `Allow` | `AllowInternetToFE` | `VNET-HUB-EUS1`/`IB-TrustZone` | `APP1-FE` | 80, 443 |
| `Allow` | `AllowWebToApp` | `APP1-FE` | `APP1-APP` | 80, 443 |
| `Allow` | `AllowAppToDB` | `APP1-APP` | `APP1-DB` | 1433 |
| `Deny`  | `DenyAllInbound` | Dowolne | Dowolne | Dowolne |

### <a name="encrypt-data"></a>Szyfrowanie danych

Usługa Azure Disk Encryption integruje się z usługą Azure Key Vault, aby pomóc w sterowaniu i zarządzaniu wpisami tajnymi i kluczami szyfrowania dysków w ramach subskrypcji usługi Key Vault. Gwarantuje to, że wszystkie dane na dyskach maszyn wirtualnych są szyfrowane podczas przechowywania w magazynie platformy Azure.

- Firma Contoso ustaliła, że określone maszyny wirtualne wymagają szyfrowania.
- Firma Contoso zastosuje szyfrowanie do maszyn wirtualnych z danymi klienta, poufnymi lub podlegającymi ochronie danych osobowych.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso konfiguruje infrastrukturę i zasady platformy Azure dla subskrypcji platformy Azure oraz funkcji identyfikacji hybrydowej, odzyskiwania po awarii, sieci, ładu i zabezpieczeń.

Nie każda czynność wykonywana w tym miejscu jest wymagana w przypadku migracji do chmury. W takim przypadku firma Contoso zaplanował infrastrukturę sieci, która może obsłużyć wszystkie typy migracji, gdy są bezpieczne, odporne i skalowalne.

Dzięki tej infrastrukturze firma Contoso jest gotowa do przejścia i wypróbowania migracji.

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu infrastruktury platformy Azure firma Contoso jest gotowa do rozpoczęcia migracji obciążeń do chmury. Zobacz sekcję [wzorców i przykładów dotyczących migracji](./contoso-migration-overview.md#windows-server-workloads) w celu wybrania scenariuszy korzystających z tej przykładowej infrastruktury jako celu migracji.
