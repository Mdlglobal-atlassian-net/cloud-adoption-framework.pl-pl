---
title: Wdrażanie infrastruktury migracji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso konfiguruje infrastrukturę platformy Azure na potrzeby migracji na platformę Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/1/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: c367bb500cf9271603cab07ac07649607bfc04a4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024343"
---
# <a name="deploy-a-migration-infrastructure"></a>Wdrażanie infrastruktury migracji

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso przygotowuje infrastrukturę lokalną do migracji, konfiguruje infrastrukturę platformy Azure w ramach przygotowania do migracji i uruchamia działalność biznesową w środowisku hybrydowym. Jeśli korzystasz z tego przykładu w celu zaplanowania własnych działań związanych z migracją infrastruktury, musisz pamiętać o następujących kwestiach:

- Udostępniona przykładowa architektura jest specyficzna dla firmy Contoso. Podczas podejmowania ważnych decyzji dotyczących infrastruktury, w tym projektu subskrypcji lub architektury sieci, uwzględnij potrzeby biznesowe, strukturę i wymagania techniczne swojej organizacji.
- To, czy potrzebujesz wszystkich elementów opisanych w tym artykule, zależy od Twojej strategii migracji. Na przykład jeśli tworzysz tylko aplikacje natywne w chmurze na platformie Azure, możesz potrzebować mniej złożonej struktury sieci.

## <a name="overview"></a>Omówienie

Aby firma Contoso mogła przeprowadzić migrację na platformę Azure, kluczowe jest przygotowanie infrastruktury platformy Azure. Ogólnie rzecz biorąc, należy wziąć pod uwagę sześć szerokich obszarów firmy Contoso:

> [!div class="checklist"]
>
> - **Krok 1. Subskrypcje platformy Azure.** Jak firma Contoso dokona zakupu platformy Azure i w jaki sposób będzie korzystać z platformy Azure oraz jej usług?
> - **Krok 2. Tożsamość hybrydowa.** Jak będzie zarządzać dostępem do zasobów lokalnych i zasobów platformy Azure oraz kontrolować do nich dostęp po migracji? Jak firma Contoso rozszerzy lub przeniesie zarządzanie tożsamościami do chmury?
> - **Krok 3. Odzyskiwanie po awarii i odporność.** W jaki sposób firma Contoso zapewnia odporność aplikacji i infrastruktury na przestoje i awarie?
> - **Krok 4. Sieć.** Jak firma Contoso powinna zaprojektować infrastrukturę sieciową i ustanowić połączenie między lokalnym centrum danych a platformą Azure?
> - **Krok 5. Bezpieczeństwo.** Jak firma Contoso będzie zabezpieczać wdrożenie hybrydowe/wdrożenie platformy Azure?
> - **Krok 6: Ład.** W jaki sposób firma Contoso będzie zapewniać zgodność wdrożenia z wymaganiami dotyczącymi zabezpieczeń i ładu?

## <a name="before-you-start"></a>Przed rozpoczęciem

Przed rozpoczęciem przeglądania infrastruktury warto zapoznać się z pewnymi dodatkowymi informacjami dotyczącymi możliwości platformy Azure, które zostały omówione w tym artykule:

- Dostępnych jest kilka opcji zakupu dostępu do platformy Azure, w tym: płatność zgodnie z rzeczywistym użyciem, umowy Enterprise Agreement (EA), program licencjonowania Open od odsprzedawców produktów firmy Microsoft lub partnerów firmy Microsoft, tzw. dostawców rozwiązań w chmurze (CSP). Dowiedz się więcej na temat [opcji zakupu](https://azure.microsoft.com/pricing/purchase-options) i przeczytaj, jak [są zorganizowane subskrypcje platformy Azure](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Zapoznaj się z omówieniem [zarządzania tożsamościami i dostępem](https://www.microsoft.com/trustcenter/security/identity) na platformie Azure. W szczególności uzyskaj informacje na temat [usługi Azure AD i rozszerzania lokalnej usługi Active Directory na chmurę](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Istnieje przydatna dostępna do pobrania książka elektroniczna dotycząca [zarządzania dostępem i tożsamościami w środowisku hybrydowym](https://azure.microsoft.com/resources/hybrid-cloud-identity).
- Platforma Azure oferuje niezawodną infrastrukturę sieciową z opcjami łączności hybrydowej. Zapoznaj się z omówieniem [sieci i kontroli dostępu do sieci](https://docs.microsoft.com/azure/security/security-network-overview).
- Zapoznaj się z wprowadzeniem do [zabezpieczeń platformy Azure](https://docs.microsoft.com/azure/security/azure-security) i przeczytaj o tworzeniu planu [ładu](https://docs.microsoft.com/azure/security/governance-in-azure).

## <a name="on-premises-architecture"></a>Architektura lokalna

Oto diagram przedstawiający bieżącą infrastrukturę lokalną firmy Contoso.

 ![Architektura firmy Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Firma Contoso ma jedno główne centrum danych znajdujące się w Nowym Jorku na wschodzie Stanów Zjednoczonych.
- Firma ma trzy dodatkowe oddziały lokalne na terenie Stanów Zjednoczonych.
- Główne centrum danych jest połączone z Internetem łączem światłowodowym Metro Ethernet (500 MB/s).
- Każdy oddział jest połączony lokalnie z Internetem przy użyciu połączeń klasy biznesowej z tunelami IPSec VPN prowadzącymi z powrotem do głównego centrum danych. Pozwala to na trwałe połączenie całej sieci i optymalizację łączności z Internetem.
- Główne centrum danych jest w pełni zwirtualizowane przy użyciu oprogramowania VMware. Firma Contoso ma dwa hosty wirtualizacji ESXi 6.5, zarządzane za pomocą programu vCenter Server 6.5.
- Firma Contoso korzysta z usługi Active Directory na potrzeby zarządzania tożsamościami oraz serwerów DNS w sieci wewnętrznej.
- Kontrolery domeny w centrum danych działają na maszynach wirtualnych VMware. Kontrolery domeny w oddziałach lokalnych działają na serwerach fizycznych.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Krok 1: Kupowanie i subskrybowanie platformy Azure

Firma Contoso musi ustalić, jak kupić platformę Azure, utworzyć architekturę subskrypcji oraz jak licencjonować usługi i zasoby.

### <a name="buy-azure"></a>Kupowanie platformy Azure

Firma Contoso zdecydowała się na [umowę Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement). Wiąże się to z podjęciem zobowiązania pieniężnego związanego z korzystaniem z platformy Azure, ale daje firmie Contoso ogromne korzyści, w tym elastyczne opcje rozliczania i nasze najlepsze ceny.

- Firma Contoso oszacowała swoje przewidywane roczne wydatki na platformę Azure. Po podpisaniu umowy firma Contoso zapłaciła za pierwszy rok w całości.
- Firma Contoso musi wykorzystać całość zobowiązania przed upływem roku lub utraci ich niewykorzystaną wartość.
- Jeśli z jakiegoś powodu firma Contoso przekroczy swoje zobowiązanie i wyda więcej, firma Microsoft wystawi fakturę za nadwyżkę.
- W przypadku wszelkich kosztów przekraczających zobowiązanie będą obowiązywały te same stawki, które określono w umowie z firmą Contoso. Nie ma kar za przekroczenie zobowiązania.

### <a name="manage-subscriptions"></a>Zarządzaj subskrypcjami

Po zapłaceniu za platformę Azure firma Contoso musi ustalić, jak zarządzać subskrypcjami platformy Azure. Firma Contoso ma umowę EA i w rezultacie nie ma limitu liczby subskrypcji platformy Azure, które może skonfigurować.

- Rejestracja w usłudze Azure Enterprise określa sposób, w jaki firma kształtuje usługi platformy Azure i korzysta z nich, a także definiuje podstawową strukturę ładu.
- W pierwszym kroku firma Contoso zdefiniowała strukturę nazywaną „szkieletem przedsiębiorstwa” na potrzeby rejestracji Enterprise. Firma Contoso skorzystała z [tego artykułu](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) w celu lepszego zrozumienia i zaprojektowania szkieletu.
- Na razie firma Contoso postanowiła wykorzystać podejście funkcjonalne do zarządzania subskrypcjami.
  - Wewnątrz przedsiębiorstwa będzie używany jeden dział IT, kontrolujący budżet platformy Azure. Będzie to jedyna grupa z subskrypcjami.
  - Firma Contoso rozszerzy ten model w przyszłości, tak aby inne grupy firmowe mogły dołączyć jako działy w ramach rejestracji Enterprise.
  - Wewnątrz działu IT firma Contoso ustrukturyzowała dwie subskrypcje: produkcyjną i deweloperską.
  - Jeśli w przyszłości będą wymagane dodatkowe subskrypcje, firma będzie musiała zarządzać dostępem, zasadami i zgodnością dla tych subskrypcji. Będzie to możliwe dzięki wprowadzeniu [grup zarządzania platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview) jako dodatkowej warstwy ponad subskrypcjami.

  ![Struktura przedsiębiorstwa](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Sprawdzanie licencjonowania

Po skonfigurowaniu subskrypcji firma Contoso może przyjrzeć się licencjonowaniu firmy Microsoft. Strategia licencjonowania będzie zależeć od zasobów, które firma Contoso chce migrować na platformę Azure, oraz sposobu wybierania i wdrażania maszyn wirtualnych oraz usług platformy Azure.

#### <a name="azure-hybrid-benefit"></a>Korzyści użycia hybrydowego platformy Azure

W przypadku wdrażania maszyn wirtualnych na platformie Azure obrazy standardowe obejmują licencję, która spowoduje obciążanie firmy Contoso opłatami za każdą minutę korzystania z oprogramowania. Firma Contoso jest jednak długoterminowym klientem firmy Microsoft i utrzymywała umowy EA oraz licencje Open z pakietem Software Assurance (SA).

Korzyść użycia hybrydowego platformy Azure oferuje ekonomiczną metodę migracji dla firmy Contoso, umożliwiając jej zaoszczędzenie na obciążeniach maszyn wirtualnych platformy Azure i programu SQL Server przez przekonwertowanie lub ponowne użycie licencji systemu Windows Server w wersji Standard i Datacenter objętych pakietem Software Assurance. Dzięki temu firma Contoso będzie płacić niższą stawkę za zasoby obliczeniowe w przypadku maszyn wirtualnych i programu SQL Server. [Dowiedz się więcej](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>Przenośność licencji

Przenośność licencji w ramach pakietu Software Assurance zapewnia klientom licencjonowania zbiorowego firmy Microsoft, takim jak firma Contoso, elastyczność wdrażania kwalifikujących się aplikacji serwerowych przy użyciu aktywnego pakietu Software Assurance na platformie Azure. Eliminuje to konieczność kupowania nowych licencji. Brak powiązanych opłat za przenośność umożliwia łatwe wdrożenie istniejących licencji na platformie Azure. [Dowiedz się więcej](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Rezerwacja wystąpień dla przewidywalnych obciążeń

Przewidywalne obciążenia to te, które zawsze muszą być dostępne z działającymi maszynami wirtualnymi. Przykładem są aplikacje biznesowe, takie jak system SAP ERP. Z kolei nieprzewidywalne obciążenia są zmiennymi, takimi jak maszyny wirtualne, które są włączone podczas wysokiego zapotrzebowania i wyłączone, gdy zapotrzebowanie jest niskie.

![Wystąpienie zarezerwowane](./media/contoso-migration-infrastructure/reserved-instance.png)

W zamian za używanie wystąpień zarezerwowanych dla konkretnych wystąpień maszyn wirtualnych przez długi czas, firma Contoso może uzyskać zarówno rabat, jak i priorytetyzowane możliwości obliczeniowe. Korzystając z [wystąpień zarezerwowanych platformy Azure](https://azure.microsoft.com/pricing/reserved-vm-instances) w połączeniu z korzyścią użycia hybrydowego platformy Azure firma Contoso może zaoszczędzić nawet 82% w stosunku do normalnych cen w modelu płatności zgodnie z rzeczywistym użyciem (kwiecień 2018 r.).

## <a name="step-2-manage-hybrid-identity"></a>Krok 2: Zarządzanie tożsamością hybrydową

Udzielanie i kontrolowanie dostępu użytkowników do zasobów platformy Azure za pomocą zarządzania dostępem i tożsamościami (IAM) to ważny krok podczas składania infrastruktury platformy Azure.

- Firma Contoso decyduje się rozszerzyć lokalną usługę Active Directory na chmurę zamiast tworzyć nowy oddzielny system na platformie Azure.
- W tym celu tworzy usługę Active Directory opartą na platformie Azure.
- Firma Contoso nie ma usługi Office 365, dlatego musi zainicjować obsługę administracyjną nowej usługi Azure AD.
- Usługa Office 365 używa usługi Azure AD do zarządzania użytkownikami. Jeśli firma Contoso korzystała z usługi Office 365, ma już dzierżawę usługi Azure AD i może użyć tej usługi jako katalogu głównego.
- [Dowiedz się więcej](https://support.office.com/article/understanding-office-365-identity-and-azure-active-directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9) o usłudze Azure AD dla usługi Office 365 i dowiedz się, [jak dodać subskrypcję](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) do istniejącej dzierżawy usługi Azure AD.

### <a name="create-an-azure-ad"></a>Tworzenie usługi Azure AD

Firma Contoso używa bezpłatnej wersji usługi Azure AD, która jest oferowana w ramach subskrypcji platformy Azure. Administratorzy firmy Contoso konfigurują katalog w następujący sposób:

1. W witrynie [Azure Portal](https://portal.azure.com) przechodzą do pozycji **Utwórz zasób** > **Tożsamość** > **Azure Active Directory**.
2. W oknie **Tworzenie katalogu** podają nazwę katalogu, początkową nazwę domeny i region, w którym ma zostać utworzony katalog usługi Azure AD.

    ![Tworzenie usługi Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > Utworzony katalog ma początkową nazwę domeny w postaci **nazwadomeny.onmicrosoft.com.** Nazwy nie można zmienić ani usunąć. Zamiast tego należy dodać zarejestrowaną nazwę domeny do usługi Azure AD.

### <a name="add-the-domain-name"></a>Dodawanie nazwy domeny

Aby móc używać swojej standardowej nazwy domeny, administratorzy firmy Contoso muszą dodać ją jako niestandardową nazwę domeny do usługi Azure AD. Ta opcja umożliwia przypisanie przyjaznych nazw użytkowników. Na przykład użytkownik może logować się przy użyciu adresu e-mail billg@contoso.com i nie potrzebuje adresu billg@contosomigration.microsoft.com.

Aby skonfigurować niestandardową nazwę domeny, administratorzy muszą dodać ją do katalogu, dodać wpis DNS, a następnie zweryfikować nazwę w usłudze Azure AD.

1. W obszarze **Niestandardowe nazwy domen** > **Dodaj domenę niestandardową** dodają domenę.
2. Aby użyć wpisu DNS na platformie Azure, muszą zarejestrować ją u swojego rejestratora domen.

    - Na liście **Niestandardowe nazwy domen** widzą informacje DNS dotyczące nazwy i notują je. Używany jest wpis MX.
    - Aby to zrobić, potrzebują dostępu do serwera nazw. Logują się do domeny Contoso.com i tworzą nowy rekord MX dla wpisu DNS dostarczonego przez usługę Azure AD, korzystając z zanotowanych szczegółów.

3. Po propagacji rekordów DNS w nazwie szczegółów domeny wybierają przycisk **Weryfikuj**, aby sprawdzić niestandardową nazwę domeny.

     ![Wpis DNS usługi Azure AD](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Konfigurowanie lokalnych i grup i użytkowników platformy Azure

Teraz, gdy usługa Azure AD jest uruchomiona, administratorzy firmy Contoso muszą dodać pracowników do grup lokalnej usługi Active Directory, które będą synchronizowane z usługą Azure Active Directory. Powinni używać nazw grup lokalnych odpowiadających nazwom grup zasobów na platformie Azure. Ułatwi to identyfikowanie dopasowań na potrzeby synchronizacji.

#### <a name="create-resource-groups-in-azure"></a>Tworzenie grup zasobów na platformie Azure

W grupach zasobów platformy umieszczane są zasoby platformy Azure. Użycie identyfikatora grupy zasobów umożliwia platformie Azure wykonywanie operacji na zasobach należących do grupy.

- Subskrypcja platformy Azure może obejmować wiele grup zasobów, ale grupa zasobów może istnieć tylko w jednej subskrypcji.
- Ponadto jedna grupa zasobów może zawierać wiele zasobów, ale zasób może należeć tylko do jednej grupy zasobów.

Administratorzy firmy Contoso konfigurują grupy zasobów platformy Azure zgodnie z opisem w poniższej tabeli.

<!-- markdownlint-disable MD033 -->

**Grupa zasobów** | **Szczegóły**
--- | ---
**ContosoCobRG** | Ta grupa zawiera wszystkie zasoby związane z ciągłością działania. Obejmuje ona magazyny, których firma Contoso będzie używać na potrzeby usługi Azure Site Recovery i usługi Azure Backup.<br/><br/> Obejmuje również zasoby używane do migracji, w tym usługę Azure Migrate i usługę Azure Database Migration Service.
**ContosoDevRG** | Ta grupa zawiera zasoby deweloperskie i testowe.
**ContosoFailoverRG** | Ta grupa służy jako strefa docelowa dla zasobów w trybie failover.
**ContosoNetworkingRG** | Ta grupa zawiera wszystkie zasoby sieciowe.
**ContosoRG** | Ta grupa zawiera zasoby związane z aplikacjami produkcyjnymi i bazami danych.

<!-- markdownlint-disable MD026 -->

Administratorzy tworzą grupy zasobów w następujący sposób:

1. W witrynie Azure Portal > **Grupy zasobów** dodają grupę.
2. Dla każdej grupy określają nazwę, subskrypcję, do której grupa należy, oraz region.
3. Grupy zasobów są wyświetlane na liście **Grupy zasobów**.

    ![Grupy zasobów](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scaling-resource-groups"></a>Skalowanie grup zasobów

W przyszłości firma Contoso doda inne grupy zasobów w zależności od potrzeb. Może na przykład zdefiniować grupy zasobów dla poszczególnych aplikacji lub usług, aby każda mogła być zarządzana i zabezpieczana niezależnie.

#### <a name="create-matching-security-groups-on-premises"></a>Tworzenie zgodnych grup zabezpieczeń w środowisku lokalnym

1. W lokalnej usłudze Active Directory administratorzy firmy Contoso konfigurują grupy zabezpieczeń o nazwach zgodnych z nazwami grup zasobów platformy Azure.

    ![Grupy zabezpieczeń lokalnej usługi Active Directory](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. Na potrzeby zarządzania tworzą dodatkową grupę, która zostanie dodana do wszystkich innych grup. Ta grupa będzie miała uprawnienia do wszystkich grup zasobów na platformie Azure. Do tej grupy zostanie dodana ograniczona liczba administratorów globalnych.

### <a name="synchronize-active-directory"></a>Synchronizowanie usługi Active Directory

Firma Contoso chce zapewnić wspólną tożsamość na potrzeby uzyskiwania dostępu do zasobów lokalnych i w chmurze. W tym celu zintegruje lokalną usługę Active Directory z usługą Azure AD. W tym modelu:

- Użytkownicy i organizacje mogą korzystać z jednej tożsamości, aby uzyskiwać dostęp do aplikacji lokalnych i usług w chmurze, takich jak usługa Office 365, lub tysięcy innych witryn w Internecie.
- Administratorzy mogą używać grup w usłudze Active Directory do zaimplementowania [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) na platformie Azure.

Aby ułatwić integrację, firma Contoso używa [narzędzia Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Po zainstalowaniu i skonfigurowaniu narzędzia na kontrolerze domeny zsynchronizuje ono lokalne tożsamości lokalnej usługi Active Directory z usługą Azure AD.

### <a name="download-the-tool"></a>Pobieranie narzędzia

1. W witrynie Azure Portal administratorzy firmy Contoso przechodzą do pozycji **Azure Active Directory** > **Azure AD Connect** i pobierają najnowszą wersję narzędzia na serwer, którego używają do synchronizacji.

    ![Pobierz program Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. Uruchamiają instalację pliku **AzureADConnect.msi**, klikając przycisk **Użyj ustawień ekspresowych**. Jest to najbardziej typowa instalacja, która może być używana dla topologii z jednym lasem, z synchronizacją skrótów haseł na potrzeby uwierzytelniania.

    ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. Na ekranie **Łączenie z usługą Azure AD** określają poświadczenia do nawiązywania połączenia z usługą Azure AD (w postaci admin@contoso.com lub admin@contoso.onmicrosoft.com).

    ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. Na ekranie **Łączenie z usługami AD DS** określają poświadczenia dla lokalnej usługi Active Directory (w postaci CONTOSO\admin lub contoso.com\admin).

     ![Kreator programu Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. Na ekranie **Wszystko gotowe do skonfigurowania** wybierają pozycję **Uruchom proces synchronizacji po ukończeniu konfiguracji**, aby natychmiast uruchomić synchronizację. Następnie uruchamiają instalację.

Należy pamiętać o następujących kwestiach:

- Firma Contoso ma połączenie bezpośrednie z platformą Azure. Jeśli lokalna usługa Active Directory znajduje się za serwerem proxy, przeczytaj ten [artykuł](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity).

- Po pierwszej synchronizacji obiekty z lokalnej usługi Active Directory są widoczne w katalogu usługi Azure AD.

    ![Lokalna usługa Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

- Zespół IT firmy Contoso jest reprezentowany w każdej grupie, na podstawie roli.

    ![Członkowie lokalnej usługi Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Konfigurowanie kontroli dostępu opartej na rolach (RBAC)

[Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Korzystając z modelu RBAC, można udzielić użytkownikom tylko takiego dostępu, jakiego potrzebują do wykonania swoich zadań. Odpowiednią rolę RBAC do użytkowników, grup i aplikacji należy przypisać na poziomie zakresu. Zakresem przypisania roli może być subskrypcja, grupa zasobów lub pojedynczy zasób.

Administratorzy firmy Contoso przypisują teraz role do grup usługi Active Directory, które zsynchronizowali ze środowiska lokalnego.

1. W grupie zasobów **ControlCobRG** wybierają pozycję **Kontrola dostępu (zarządzanie dostępem i tożsamościami)**  > **Dodaj przypisanie roli**.
2. W obszarze **Dodaj przypisania roli** > **Rola** > **Współautor** wybierają grupę **ContosoCobRG** z listy. Grupa zostanie wyświetlona na liście **Wybrani członkowie**.
3. Powtarzają to z tymi samymi uprawnieniami dla innych grup zasobów (z wyjątkiem grupy **ContosoAzureAdmins**) przez dodanie uprawnień współautora do konta odpowiadającego grupie zasobów.
4. W przypadku grupy **ContosoAzureAdmins** przypisują rolę **Właściciel**.

    ![Członkowie lokalnej usługi Active Directory na platformie Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Krok 3: Projektowanie pod kątem odporności

### <a name="set-up-regions"></a>Konfigurowanie regionów

Zasoby platformy Azure są wdrażane w regionach.

- Regiony są zorganizowane w obszary geograficzne, a wymagania dotyczące rezydencji, niezależności, zgodności i odporności danych są uznawane w granicach geograficznych.
- Region składa się z zestawu centrów danych. Te centra danych są wdrożone wewnątrz obwodu o zdefiniowanym opóźnieniu i połączone za pośrednictwem dedykowanej regionalnej sieci o małych opóźnieniach.
- Każdy region świadczenia usługi Azure jest sparowany z innym regionem w celu zapewnienia odporności.
- Przeczytaj więcej na temat [regionów świadczenia usługi Azure](https://azure.microsoft.com/global-infrastructure/regions) i dowiedz się, [jak regiony są sparowane](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Firma Contoso zdecydowała się wybrać region Wschodnie stany USA 2 (z lokalizacją w stanie Wirginia) jako region podstawowy oraz region Środkowe stany USA (z lokalizacją w stanie Iowa) jako region pomocniczy. Istnieje kilka przyczyn tej decyzji:

- Centrum danych firmy Contoso znajduje się w Nowym Jorku, a firma Contoso brała pod uwagę opóźnienie do najbliższego centrum danych.
- Region Wschodnie stany USA 2 ma wszystkie usługi i produkty, których firma Contoso potrzebuje. Nie wszystkie regiony platformy Azure są takie same, jeśli chodzi o dostępne produkty i usługi. Możesz przejrzeć [produkty platformy Azure według regionów](https://azure.microsoft.com/global-infrastructure/services).
- Środkowe stany USA to region sparowany na platformie Azure z regionem Wschodnie stany USA 2.

Myśląc o środowisku hybrydowym, firma Contoso musi rozważyć, jak wbudować odporność i strategię odzyskiwania po awarii w projekt regionów. W szerokim ujęciu strategie obejmują zakres od wdrożenia w jednym regionie, które bazuje na funkcjach platformy Azure, takich jak domeny błędów i regionalne parowanie w celu zapewnienia odporności, po pełny model aktywne-aktywne, w którym usługi Cloud Services i baza danych są wdrażane i obsługują użytkowników z dwóch regionów.

Firma Contoso zdecydowała się na środkową drogę. Wdroży aplikacje i zasoby w regionie podstawowym i zachowa pełną kopię infrastruktury w regionie pomocniczym, aby była gotowa do działania jako pełna kopia zapasowa na wypadek całkowitej awarii aplikacji lub awarii regionalnej.

### <a name="set-up-availability"></a>Konfigurowanie dostępności

**Zestawy dostępności:**

Zestawy dostępności pomagają chronić aplikacje i dane przed awariami sprzętu lokalnego i sieci w centrum danych.

- Zestawy dostępności rozpraszają maszyny wirtualne platformy Azure na różny sprzęt fizyczny w centrum danych.
- Domeny błędów reprezentują odpowiednie elementy sprzętu korzystające ze wspólnego źródła zasilania i przełącznika sieciowego w centrum danych. Maszyny wirtualne w zestawie dostępności są rozproszone między różne domeny błędów, aby zminimalizować wyłączenia spowodowane pojedynczą awarią sprzętu lub sieci.
- Domeny aktualizacji reprezentują odpowiednie elementy sprzętu, które mogą być poddawane konserwacji lub ponownie uruchamiane w tym samym czasie. Zestawy dostępności również rozpraszają maszyny wirtualne między wiele domen aktualizacji, aby upewnić się, że co najmniej jedno wystąpienie będzie działać przez cały czas.

Firma Contoso będzie implementować zestawy dostępności zawsze, gdy obciążenia maszyn wirtualnych wymagają wysokiej dostępności. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Strefy dostępności:**

Strefy dostępności pomagają chronić aplikacje i dane przed awariami wpływającymi na całe centrum danych w regionie.

- Każda strefa dostępności reprezentuje unikatową lokalizację fizyczną w regionie świadczenia usługi Azure.
- Każda strefa składa się z co najmniej jednego centrum danych wyposażonego w niezależne zasilanie, chłodzenie i sieć.
- Istnieją co najmniej trzy osobne strefy we wszystkich włączonych regionach.
- Fizyczna separacja stref w ramach regionu chroni aplikacje i dane przed awariami centrum danych.

Firma Contoso będzie wdrażać strefy dostępności w celu spełnienia wymagań aplikacji dotyczących skalowalności, wysokiej dostępności i odporności. [Dowiedz się więcej](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="set-up-backup"></a>Konfigurowanie kopii zapasowej

**Azure Backup:**

Usługa Azure Backup umożliwia tworzenie kopii zapasowych i przywracanie dysków maszyn wirtualnych platformy Azure.

- Usługa Azure Backup umożliwia automatyczne tworzenie kopii zapasowych obrazów dysków maszyn wirtualnych przechowywanych w usłudze Azure Storage.
- Kopie zapasowe są spójne na poziomie aplikacji, co gwarantuje, że kopia zapasowa danych jest spójna transakcyjnie i że aplikacje będą uruchamiały się po przywróceniu.
- Usługa Azure Backup obsługuje magazyn lokalnie nadmiarowy (LRS) w celu replikowania wielu kopii danych kopii zapasowych w centrum danych w razie awarii sprzętu lokalnego.
- W przypadku awarii regionalnej usługa Azure Backup obsługuje również magazyn geograficznie nadmiarowy (GRS), który replikuje dane kopii zapasowej do sparowanego regionu pomocniczego.
- Usługa Azure Backup szyfruje przesyłane dane przy użyciu algorytmu AES 256. Dane kopii zapasowych podczas magazynowania są szyfrowane przy użyciu [szyfrowania usługi Storage (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

Firma Contoso będzie używać usługi Azure Backup z magazynem geograficznie nadmiarowym (GRS) na wszystkich produkcyjnych maszynach wirtualnych, aby zapewnić wykonywanie kopii zapasowych danych obciążeń i możliwość ich szybkiego przywrócenia w razie awarii lub innych zakłóceń. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup).

### <a name="set-up-disaster-recovery"></a>Konfigurowanie odzyskiwania po awarii

**Azure Site Recovery:**

Usługa Azure Site Recovery pomaga zapewnić ciągłość działania dzięki utrzymywaniu działania aplikacji biznesowych i obciążeń podczas regionalnych awarii.

- Usługa Azure Site Recovery stale replikuje maszyny wirtualne platformy Azure z regionu podstawowego do pomocniczego, zapewniając funkcjonalne kopie w obu lokalizacjach.
- W razie awarii w regionie podstawowym aplikacja lub usługa przechodzi w tryb failover w celu używania wystąpień maszyn wirtualnych zreplikowanych w regionie pomocniczym, minimalizując potencjalne przerwy w działaniu.
- Kiedy operacje wrócą do normalnego działania, aplikacje i usługi mogą powrócić po awarii na maszyny wirtualne w regionie podstawowym.

Firma Contoso zaimplementuje usługę Azure Site Recovery dla wszystkich produkcyjnych maszyn wirtualnych używanych w obciążeniach o krytycznym znaczeniu, aby zminimalizować przerwy w działaniu podczas awarii w regionie podstawowym. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

## <a name="step-4-design-a-network-infrastructure"></a>Krok 4: Projektowanie infrastruktury sieci

Po wdrożeniu projektu regionalnego firma Contoso jest gotowa do rozważenia strategii sieci. Należy wziąć pod uwagę sposób, w jaki lokalne centrum danych i platforma Azure łączą się i komunikują ze sobą, oraz sposób projektowania infrastruktury sieci na platformie Azure. Firma Contoso musi:

- **Zaplanować hybrydową łączność sieciową.** Firma musi ustalić, w jaki sposób zamierza połączyć sieci w środowisku lokalnym i na platformie Azure.
- **Zaprojektować infrastrukturę sieci platformy Azure.** Oznacza to podjęcie decyzji odnośnie sposobu wdrożenia sieci w regionach. Jak sieci będą komunikowały się w obrębie tego samego regionu i w różnych regionach?
- **Zaprojektować i skonfigurować sieci platformy Azure.** Musi skonfigurować sieci i podsieci platformy Azure, a następnie zdecydować, co będzie się w nich znajdować.

### <a name="plan-hybrid-network-connectivity"></a>Planowanie hybrydowej łączności sieciowej

Firma Contoso rozważała [wiele architektur](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) dla sieci hybrydowej między platformą Azure a lokalnym centrum danych. [Przeczytaj więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) na temat porównywania opcji.

Przypomnijmy, że lokalna infrastruktura sieciowa firmy Contoso obecnie składa się z centrum danych w Nowym Jorku i lokalnych oddziałów we wschodniej części USA. Wszystkie lokalizacje mają połączenie klasy biznesowej z Internetem. Każdy oddział jest następnie połączony z centrum danych za pośrednictwem tunelu IPSec VPN przez Internet.

![Sieć firmy Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

Oto, jak firma Contoso zdecydowała się wdrożyć łączność hybrydową:

1. Skonfiguruje nowe połączenie sieci VPN typu lokacja-lokacja między centrum danych firmy Contoso w Nowym Jorku i dwoma regionami świadczenia usługi Azure w regionach Wschodnie stany USA 2 i Środkowe stany USA.
2. Ruch z oddziałów powiązany z sieciami wirtualnymi platformy Azure będzie kierowany przez główne centrum danych firmy Contoso.
3. Kiedy firma Contoso przeprowadzi skalowanie w górę wdrożenia platformy Azure, ustanowi połączenie ExpressRoute między centrum danych i regionami świadczenia usługi Azure. Gdy to się stanie, Contoso pozostawi połączenie sieci VPN typu lokacja-lokacja tylko do celów związanych z trybem failover.
    - [Dowiedz się więcej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) na temat wybierania między siecią VPN a rozwiązaniem hybrydowym z usługą ExpressRoute.
    - Sprawdź [lokalizacje i obsługę usługi ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**Tylko sieć VPN:**

![Sieć VPN firmy Contoso](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**Sieć VPN i usługa ExpressRoute:**

![Sieć VPN firmy Contoso/usługa ExpressRoute](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Projektowanie infrastruktury sieci platformy Azure

Dla firmy Contoso krytyczne znaczenie ma zaimplementowanie sieci w sposób zapewniający bezpieczeństwo i skalowalność wdrożenia hybrydowego. Aby to osiągnąć, firma Contoso przyjmuje podejście długoterminowe i projektuje sieci wirtualne pod kątem odporności i gotowości do użycia w przedsiębiorstwie. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) o planowaniu sieci wirtualnych.

W celu połączenia dwóch regionów firma Contoso zdecydowała się zaimplementować model „piasta-piasta”:

- W każdym regionie będzie używany model gwiazdy.
- Do połączenia sieci i piast Contoso będzie używać komunikacji równorzędnej sieci platformy Azure.

#### <a name="network-peering"></a>Komunikacja równorzędna sieci

Platforma Azure oferuje komunikację równorzędną sieci na potrzeby łączenia sieci wirtualnych i piast. Globalna komunikacja równorzędna umożliwia połączenia między sieciami wirtualnymi/piastami w różnych regionach. Lokalna komunikacja równorzędna łączy sieci wirtualne w tym samym regionie. Komunikacja równorzędna sieci wirtualnych zapewnia kilka korzyści:

- Ruch sieciowy między sieciami wirtualnymi w komunikacji równorzędnej jest prywatny.
- Ruch między sieciami wirtualnymi jest utrzymywany w sieci szkieletowej firmy Microsoft. Do komunikacji między sieciami wirtualnymi nie jest wymagany publiczny Internet, bramy ani szyfrowanie.
- Komunikacja równorzędna zapewnia domyślne połączenie o małych opóźnieniach i dużej przepustowości między zasobami w różnych sieciach wirtualnych.

Dowiedz się więcej o [komunikacji równorzędnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

#### <a name="hub-to-hub-across-regions"></a>Połączenie między piastami w różnych regionach

Firma Contoso wdroży piastę w każdym regionie. Piasta to sieć wirtualna (VNet) na platformie Azure, która działa jako centralny punkt łączności z Twoją siecią lokalną. Sieci wirtualne piasty będą łączyć się ze sobą przy użyciu globalnej komunikacji równorzędnej sieci wirtualnych. Globalna komunikacja równorzędna sieci wirtualnych łączy sieci wirtualne w różnych regionach świadczenia usługi Azure.

- Piasta w każdym regionie jest połączona za pomocą komunikacji równorzędnej z partnerską piastą w innym regionie.
- Piasta jest połączona za pomocą komunikacji równorzędnej z każdą siecią w swoim regionie i może połączyć się ze wszystkimi zasobami sieciowymi.

    ![Globalna komunikacja równorzędna](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Model gwiazdy w obrębie regionu

W każdym regionie firma Contoso wdroży sieci wirtualne przeznaczone do różnych celów, jako sieci będące szprychami piasty regionu. Sieci wirtualne w regionie używają komunikacji równorzędnej do łączenia się ze swoją piastą i między sobą.

#### <a name="design-the-hub-network"></a>Projektowanie sieci piasty

W modelu gwiazdy wybranym przez firmę Contoso należy przemyśleć sposób, w jaki będzie kierowany ruch z lokalnego centrum danych i z Internetu. Oto, jak firma Contoso zdecydowała się obsługiwać routing dla piast regionów Wschodnie stany USA 2 i Środkowe stany USA:

- Firma Contoso projektuje sieć określaną jako „odwrócone c”, ponieważ to jest ścieżka, którą pakiety przepływają z sieci ruchu przychodzącego do sieci ruchu wychodzącego.
- Architektura sieci ma dwie granice: niezaufaną strefę obwodową frontonu i strefę zaufaną zaplecza.
- Zapora będzie miała kartę sieciową w każdej strefie, kontrolując dostęp do stref zaufanych.
- Z Internetu:
  - Ruch z Internetu osiągnie publiczny adres IP ze zrównoważonym obciążeniem w sieci obwodowej.
  - Ten ruch jest kierowany przez zaporę i podlega regułom zapory.
  - Po zaimplementowaniu mechanizmów kontroli dostępu do sieci ruch zostanie przekazany do odpowiedniej lokalizacji w zaufanej strefie.
  - Ruch wychodzący z sieci wirtualnej będzie kierowany do Internetu przy użyciu tras zdefiniowanych przez użytkownika. Ruch jest wymuszany przez zaporę i sprawdzany zgodnie z zasadami firmy Contoso.
- Z centrum danych firmy Contoso:
  - Ruch przychodzący za pośrednictwem sieci VPN typu lokacja-lokacja (lub usługi ExpressRoute) osiąga publiczny adres IP bramy Azure VPN Gateway.
  - Ruch jest kierowany przez zaporę i podlega regułom zapory.
  - Po zastosowaniu reguł zapory ruch jest przekazywany dalej do wewnętrznego modułu równoważenia obciążenia (jednostka SKU w warstwie Standardowa) w zaufanej podsieci strefy wewnętrznej.
  - Ruch wychodzący z zaufanej podsieci do lokalnego centrum danych za pośrednictwem sieci VPN jest kierowany przez zaporę (i zastosowane reguły) przed przesłaniem za pośrednictwem połączenia sieci VPN typu lokacja-lokacja.

### <a name="design-and-set-up-azure-networks"></a>Projektowanie i konfigurowanie sieci platformy Azure

Po wdrożeniu topologii sieci i routingu firma Contoso jest gotowa do skonfigurowania sieci i podsieci platformy Azure.

- Firma Contoso zaimplementuje sieć prywatną klasy A na platformie Azure (0.0.0.0 do 127.255.255.255). To działa, ponieważ lokalnie ma ona prywatną przestrzeń adresową klasy B 172.160.0/16, więc firma Contoso może mieć pewność, że zakresy adresów nie będą się nakładać.
- Zamierza wdrożyć sieci wirtualne w regionach głównym i pomocniczym.
- Firma Contoso będzie używać konwencji nazewnictwa, która uwzględnia w nazwach prefiks **VNET** i skrót regionu **EUS2** lub **CUS**. Przy użyciu tego standardu sieciom piast zostaną nadane nazwy **VNET-HUB-EUS2** (Wschodnie stany USA 2) i **VNET-HUB-CUS** (Środkowe stany USA).
- Firma Contoso nie ma [rozwiązania IPAM](https://docs.microsoft.com/windows-server/networking/technologies/ipam/ipam-top), dlatego musi zaplanować routing sieciowy bez translatora adresów sieciowych.

#### <a name="virtual-networks-in-east-us-2"></a>Sieci wirtualne w regionie Wschodnie stany USA 2

Wschodnie stany USA 2 to region podstawowy, którego firma Contoso będzie używać do wdrażania zasobów i usług. Oto, jak firma Contoso zaprojektuje architekturę sieci w tym regionie:

- **Piasta:** Sieć wirtualna piasty w regionie Wschodnie stany USA 2 jest centralnym punktem podstawowej łączności z lokalnym centrum danych.
- **Sieci wirtualne:** Sieci wirtualne będące szprychami w regionie Wschodnie stany USA 2 mogą w razie potrzeby służyć do izolowania obciążeń. Oprócz sieci wirtualnej piasty w regionie Wschodnie stany USA 2 firma Contoso będzie miała dwie sieci wirtualne szprych:
  - **VNET-DEV-EUS2**. Ta sieć wirtualna zapewni zespołowi programistycznemu i testującemu w pełni funkcjonalną sieć dla projektów deweloperskich. Będzie działać jako produkcyjny obszar pilotażowy i będzie polegać na infrastrukturze produkcyjnej.
    - **VNET-PROD-EUS2**. W tej sieci będą znajdować się składniki produkcyjne IaaS platformy Azure.
  - Każda sieć wirtualna będzie miała własną unikatową przestrzeń adresową, bez nakładania się. Firma Contoso zamierza skonfigurować routing niewymagający używania translatora adresów sieciowych.
- **Podsieci:**
  - W każdej sieci każda warstwa aplikacji będzie miała własną podsieć
  - Każda podsieć w sieci produkcyjnej będzie miała pasującą podsieć w sieci wirtualnej opracowywania.
  - Dodatkowo sieć produkcyjna ma podsieć dla kontrolerów domeny.

Sieci wirtualne w regionie Wschodnie stany USA 2 zostały przedstawione w poniższej tabeli.

**Sieć wirtualna** | **Zakres** | **Element równorzędny**
--- | --- | ---
**VNET-HUB-EUS2** | 10.240.0.0/20 | VNET-HUB-CUS2, VNET-DEV-EUS2, VNET-PROD-EUS2
**VNET-DEV-EUS2** | 10.245.16.0/20 | VNET-HUB-EUS2
**VNET-PROD-EUS2** | 10.245.32.0/20 | VNET-HUB-EUS2, VNET-PROD-CUS

![Model gwiazdy w regionie podstawowym](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Podsieci w sieci piasty w regionie Wschodnie stany USA 2 (VNET-HUB-EUS2)

**Podsieć/strefa** | **CIDR** | **Możliwe do użycia adresy IP
--- | --- | ---
**IB-UntrustZone** | 10.240.0.0/24 | 251
**IB-TrustZone** | 10.240.1.0/24 | 251
**OB-UntrustZone** | 10.240.2.0/24 | 251
**OB-TrustZone** | 10.240.3.0/24 | 251
**GatewaySubnets** | 10.240.10.0/24 | 251

#### <a name="subnets-in-the-east-us-2-dev-network-vnet-dev-eus2"></a>Podsieci w sieci opracowywania w regionie Wschodnie stany USA 2 (VNET-DEV-EUS2)

Sieć wirtualna opracowywania jest używana przez zespół programistyczny jako produkcyjny obszar pilotażowy. Ma trzy podsieci.

**Podsieć** | **CIDR** | **Adresy** | **W podsieci**
--- | --- | --- | ---
**DEV-FE-EUS2** | 10.245.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
**DEV-APP-EUS2** | 10.245.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
**DEV-DB-EUS2** | 10.245.24.0/23 | 507 | Maszyny wirtualne bazy danych

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Podsieci w sieci produkcyjnej Wschodnie stany USA 2 (VNET-PROD-EUS2)

Składniki IaaS platformy Azure znajdują się w sieci produkcyjnej. Każda warstwa aplikacji ma własną podsieć. Podsieci są zgodne z tymi w sieci deweloperskiej, a dodatkowo istnieje podsieć dla kontrolerów domeny.

**Podsieć** | **CIDR** | **Adresy** | **W podsieci**
--- | --- | --- | ---
**PROD-FE-EUS2** | 10.245.32.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
**PROD-APP-EUS2** | 10.245.36.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
**PROD-DB-EUS2** | 10.245.40.0/23 | 507 | Maszyny wirtualne bazy danych
**PROD-DC-EUS2** | 10.245.42.0/24 | 251 | Maszyny wirtualne kontrolerów domeny

![Architektura sieci piasty](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Sieci wirtualne w regionie Środkowe stany USA (regionie pomocniczym)

Środkowe stany USA to region pomocniczy firmy Contoso. Oto, jak firma Contoso zaprojektuje architekturę sieci w tym regionie:

- **Piasta:** Sieć wirtualna piasty w regionie Wschodnie stany USA 2 jest centralnym punktem łączności z lokalnym centrum danych, a sieci wirtualne szprych w regionie Wschodnie stany USA 2 mogą być w razie potrzeby używane do izolowania obciążeń i zarządzane oddzielnie od innych szprych.
- **Sieci wirtualne:** Firma Contoso będzie miała dwie sieci wirtualne w regionie Środkowe stany USA:
  - VNET-PROD-CUS. Ta sieć wirtualna jest siecią produkcyjną, podobną do sieci VNET-PROD_EUS2.
  - VNET-ASR-CUS. Ta sieć wirtualna będzie działać jako lokalizacja, w której maszyny wirtualne są tworzone po przełączeniu w tryb failover ze środowiska lokalnego, lub jako lokalizacja maszyn wirtualnych platformy Azure, które są przełączane w tryb failover z regionu podstawowego do pomocniczego. Ta sieć jest podobna do sieci produkcyjnych, ale nie ma w niej żadnych kontrolerów domeny.
  - Każda sieć wirtualna w regionie będzie mieć własną przestrzeń adresową, bez nakładania się. Firma Contoso skonfiguruje routing bez translatora adresów sieciowych.
- **Podsieci:** Podsieci zostaną zaprojektowane w podobny sposób jak te w regionie Wschodnie stany USA 2. Wyjątkiem jest to, że firma Contoso nie potrzebuje podsieci dla kontrolerów domeny.

Poniższa tabela zawiera podsumowanie sieci wirtualnych w regionie Środkowe stany USA.

**Sieć wirtualna** | **Zakres** | **Element równorzędny**
--- | --- | ---
**VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS
**VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS
**VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2

![Model gwiazdy w regionie sparowanym](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Podsieci w sieci piasty w regionie Środkowe stany USA (VNET-HUB-CUS)

**Podsieć** | **CIDR** | **Możliwe do użycia adresy IP**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Podsieci w sieci produkcyjnej w regionie Środkowe stany USA (VNET-PROD-CUS)

Równolegle z siecią produkcyjną w regionie podstawowym Wschodnie stany USA 2 istnieje sieć produkcyjna w regionie pomocniczym Środkowe stany USA.

**Podsieć** | **CIDR** | **Adresy** | **W podsieci**
--- | --- | --- | ---
**PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
**PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
**PROD-DB-CUS** | 10.255.40.0/23 | 507 | Maszyny wirtualne bazy danych
**PROD-DC-CUS** | 10.255.42.0/24 | 251 | Maszyny wirtualne kontrolerów domeny

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Podsieci w sieci trybu failover/odzyskiwania w regionie Środkowe stany USA (VNET-ASR-CUS)

Sieć VNET-ASR-CUS jest używana do celów przełączania w tryb failover między regionami. Usługa Site Recovery będzie używana do replikowania maszyn wirtualnych platformy Azure i przełączania ich w tryb failover między regionami. Działa ona również jako centrum danych firmy Contoso dla sieci platformy Azure w przypadku obciążeń chronionych, które pozostają w środowisku lokalnym, ale w trybie failover są przełączane na platformę Azure na potrzeby odzyskiwania po awarii.

Sieć VNET-ASR-CUS jest tą samą podstawową podsiecią co produkcyjna sieć wirtualna w regionie Wschodnie stany USA 2, ale nie potrzebuje podsieci kontrolera domeny.

**Podsieć** | **CIDR** | **Adresy** | **W podsieci**
--- | --- | --- | ---
**ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Maszyny wirtualne frontonu/warstwy internetowej
**ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Maszyny wirtualne warstwy aplikacji
**ASR-DB-CUS** | 10.255.24.0/23 | 507 | Maszyny wirtualne bazy danych

![Architektura sieci piasty](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Konfigurowanie połączeń komunikacji równorzędnej

Piasta w każdym regionie będzie połączona za pomocą komunikacji równorzędnej z piastą w drugim regionie i ze wszystkimi sieciami wirtualnymi w obrębie regionu piasty. Dzięki temu piasty mogą komunikować się i wyświetlać wszystkie sieci wirtualne w regionie. Należy pamiętać o następujących kwestiach:

- Komunikacja równorzędna tworzy połączenie dwustronne. Jedno z inicjującego elementu równorzędnego w pierwszej sieci wirtualnej i drugie w drugiej sieci wirtualnej.
- We wdrożeniu hybrydowym ruch między elementami równorzędnymi musi być widoczny z połączenia sieci VPN między lokalnym centrum danych i platformą Azure. Aby to umożliwić, istnieją pewne określone ustawienia, które należy ustawić dla połączeń komunikacji równorzędnej.

W przypadku wszystkich połączeń z sieci wirtualnych szprych za pośrednictwem piasty do lokalnego centrum danych firma Contoso musi zezwolić na przekazywanie ruchu i przechodzenie między bramami sieci VPN.

##### <a name="domain-controller"></a>Kontroler domeny

W przypadku kontrolerów domeny w sieci VNET-PROD-EUS2 firma Contoso chce, aby ruch przepływał zarówno między piastą/siecią produkcyjną regionu EUS2, jak i za pośrednictwem połączenia sieci VPN do środowiska lokalnego. Aby to umożliwić, administratorzy firmy Contoso muszą ustawić następujące opcje:

1. **Zezwalaj na ruch przesłany dalej** i **Zezwalaj na tranzyt bramy** w połączeniu komunikacji równorzędnej. W naszym przykładzie jest to połączenie sieci VNET-HUB-EUS2 z siecią VNET-PROD-EUS2.

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

- Ponieważ jest to sieć hybrydowa, wszystkie maszyny wirtualne w środowisku lokalnym i na platformie Azure muszą być w stanie rozpoznawać nazwy, aby działać prawidłowo. Oznacza to, że do wszystkich sieci wirtualnych należy zastosować niestandardowe ustawienia DNS.
- Firma Contoso wdrożyła kontrolery domen w centrum danych Contoso i w oddziałach. Podstawowe serwery DNS to CONTOSODC1 (172.16.0.10) i CONTOSODC2 (172.16.0.1)
- Po wdrożeniu sieci wirtualnych lokalne kontrolery domen będą ustawione do używania jako serwery DNS w sieciach.
- Aby skonfigurować tę opcję, w przypadku używania niestandardowego systemu DNS w sieci wirtualnej, należy dodać adres IP cyklicznych programów rozpoznawania nazw na platformie Azure (na przykład 168.63.129.16) do listy serwerów DNS. W tym celu firma Contoso konfiguruje ustawienia serwera DNS w każdej sieci wirtualnej. Na przykład niestandardowe ustawienia DNS dla sieci VNET-HUB-EUS2 są następujące:

    ![Niestandardowe DNS](./media/contoso-migration-infrastructure/custom-dns.png)

Oprócz lokalnych kontrolerów domeny firma Contoso chce zaimplementować jeszcze cztery dodatkowe na potrzeby obsługi sieci platformy Azure, po dwa dla każdego regionu. Oto, co firma Contoso wdroży na platformie Azure.

**Region** | **DC** | **Sieć wirtualna** | **Podsieć** | **Adres IP**
--- | --- | --- | --- | ---
EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4
EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5
CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4
CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4

Po wdrożeniu lokalnych kontrolerów domeny firma Contoso musi zaktualizować ustawienia DNS w sieciach w obu regionach w celu uwzględnienia nowych kontrolerów domeny na liście serwerów DNS.

#### <a name="set-up-domain-controllers-in-azure"></a>Konfigurowanie kontrolerów domeny na platformie Azure

Po zaktualizowaniu ustawień sieci administratorzy firmy Contoso są gotowi do utworzenia kontrolerów domeny na platformie Azure.

1. W witrynie Azure Portal wdrażają nową maszynę wirtualną z systemem Windows Server w odpowiedniej sieci wirtualnej.
2. Tworzą zestawy dostępności w każdej lokalizacji maszyny wirtualnej. Zestawy dostępności pełnią następujące funkcje:

    - Zapewniają, że sieć szkieletowa Azure rozdziela maszyny wirtualne w różnych infrastrukturach w regionie świadczenia usługi Azure.
    - Umożliwia firmie Contoso kwalifikowanie się do umowy SLA gwarantującej dostępność na poziomie 99,95% dla maszyn wirtualnych na platformie Azure. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets).

    ![Grupa dostępności](./media/contoso-migration-infrastructure/availability-group.png)

3. Po wdrożeniu maszyny wirtualnej otwierają interfejs sieciowy maszyny wirtualnej. Ustawiają prywatny adres IP jako statyczny i określają prawidłowy adres.

    ![VM NIC](./media/contoso-migration-infrastructure/vm-nic.png)

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

1. Tworzą dwie nowe lokacje (AZURE-EUS2 i AZURE-CUS) wraz z lokacją centrum danych (ContosoDatacenter).
2. Po utworzeniu lokacji tworzą podsieci w lokacjach w celu dopasowania do sieci wirtualnych i centrum danych.

    ![Podsieci kontrolerów domeny](./media/contoso-migration-infrastructure/dc-subnets.png)

3. Następnie tworzą dwa łącza lokacji, aby wszystko połączyć. Kontrolery domeny należy wtedy przenieść do ich lokalizacji.

    ![Łącza kontrolerów domeny](./media/contoso-migration-infrastructure/dc-links.png)

4. Po skonfigurowaniu wszystkich elementów topologia replikacji usługi Active Directory jest wdrożona.

    ![Replikacja kontrolerów domeny](./media/contoso-migration-infrastructure/ad-resolution.png)

5. Kiedy wszystko jest ukończone, lista kontrolerów domeny i lokacji jest wyświetlana w lokalnym Centrum administracyjnym usługi Active Directory.

    ![Centrum administracyjne usługi Active Directory](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Krok 5. Planowanie pod kątem ładu

Platforma Azure udostępnia szereg mechanizmów kontroli ładu w usługach i na platformie Azure. [Przeczytaj więcej](https://docs.microsoft.com/azure/security/governance-in-azure), aby uzyskać podstawową wiedzę na temat opcji.

Podczas konfigurowania tożsamości i kontroli dostępu firma Contoso zaczęła już implementować pewne aspekty ładu i bezpieczeństwa. Ogólnie istnieją trzy obszary, które należy wziąć pod uwagę:

- **Zasady:** Usługa Azure Policy stosuje i wymusza reguły i efekty dotyczące zasobów, dzięki czemu zasoby pozostają zgodne z wymaganiami firmy i umowami SLA.
- **Blokady:** Platforma Azure umożliwia blokowanie subskrypcji, grup zasobów i innych zasobów, tak aby mogły być modyfikowane tylko przez osoby z odpowiednimi uprawnieniami.
- **Tagi:** Zasoby można kontrolować, poddawać inspekcji i zarządzać nimi za pomocą tagów. Tagi dołączają do zasobów metadane, dostarczając informacje o zasobach lub właścicielach.

### <a name="set-up-policies"></a>Konfigurowanie zasad

Usługa Azure Policy ocenia zasoby, skanując je pod kątem elementów niezgodnych z wdrożonymi definicjami zasad. Na przykład możesz mieć zasadę, która zezwala tylko na niektóre typy maszyn wirtualnych lub wymaga, aby zasoby miały określony tag.

Zasady określają definicję zasad, a przypisanie zasad określa zakres, w którym należy zastosować zasady. Zakresem może być zarówno grupa zarządzania, jak i grupa zasobów. [Dowiedz się więcej](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) na temat tworzenia zasad i zarządzania nimi.

Firma Contoso chce zacząć korzystać z kilku zasad:

- Chce mieć pewność, że zasoby mogą być wdrażane tylko w regionach EUS2 i CUS.
- Chce ograniczyć jednostki SKU maszyn wirtualnych tylko do zatwierdzonych jednostek SKU. Celem jest upewnienie się, że kosztowne jednostki SKU maszyn wirtualnych nie są używane.

#### <a name="limit-resources-to-regions"></a>Ograniczanie zasobów do regionów

Firma Contoso używa wbudowanej definicji zasad **Dozwolone lokalizacje**, aby ograniczyć regiony zasobów.

1. W witrynie Azure Portal wybierz pozycję **Wszystkie usługi** i wyszukaj **Zasady**.
2. Wybierz pozycję **Przypisania** > **Przypisz zasady**.
3. Na liście zasad wybierz pozycję **Dozwolone lokalizacje**.
4. W obszarze **Zakres** ustaw nazwę subskrypcji platformy Azure, a następnie wybierz dwa regiony z listy dozwolonych.

    ![Regiony dozwolone przez zasady](./media/contoso-migration-infrastructure/policy-region.png)

5. Domyślnym ustawieniem zasad jest **Odmów**, co oznacza, że jeśli ktoś rozpocznie wdrożenie w subskrypcji, która nie znajduje się w regionie EUS2 lub CUS, wdrożenie zakończy się niepowodzeniem. Oto co się stanie, jeśli ktoś z subskrypcji Contoso podejmie próbę skonfigurowania wdrożenia w regionie Zachodnie stany USA.

    ![Zasady nie powiodły się](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Zezwalanie na określone jednostki SKU maszyn wirtualnych

Firma Contoso będzie używać wbudowanej definicji zasad **zezwalania na jednostki SKU maszyn wirtualnych** w celu ograniczenia typu maszyn wirtualnych, które można utworzyć w ramach subskrypcji.

![Jednostka SKU zasad](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Sprawdzanie zgodności z zasadami

Zasady zaczynają obowiązywać natychmiast, a firma Contoso może sprawdzić zasoby pod kątem zgodności.

1. W witrynie Azure Portal wybierz link **Zgodność**.
2. Zostanie wyświetlony pulpit nawigacyjny zgodności. Możesz przejść do szczegółów, aby uzyskać więcej informacji.

    ![Zgodność z zasadami](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Konfigurowanie blokad

Firma Contoso długo używała struktury ITIL do zarządzania swoimi systemami. Jednym z najważniejszych aspektów struktury jest kontrola zmian, a firma Contoso chce się upewnić, że kontrola zmian zostanie zaimplementowana we wdrożeniu platformy Azure.

Firma Contoso zamierza zaimplementować blokady w następujący sposób:

- Każdy składnik produkcyjny lub trybu failover musi znajdować się w grupie zasobów, która ma blokadę ReadOnly. Oznacza to, że aby zmodyfikować lub usunąć elementy produkcyjne, należy usunąć blokadę.
- Grupy zasobów nieprodukcyjnych będą mieć blokady CanNotDelete. Oznacza to, że autoryzowani użytkownicy mogą odczytywać lub modyfikować zasób, ale nie mogą go usunąć.

[Dowiedz się więcej](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) o blokadach.

### <a name="set-up-tagging"></a>Konfigurowanie tagowania

Aby śledzić zasoby w miarę ich dodawania, coraz ważniejsze dla firmy Contoso będzie skojarzenie zasobów z odpowiednim działem, klientem i środowiskiem.

Oprócz dostarczania informacji o zasobach i właścicielach tagi umożliwią firmie Contoso agregowanie i grupowanie zasobów oraz używanie tych danych do celów obciążeń zwrotnych.

Firma Contoso musi zwizualizować swoje zasoby platformy Azure w sposób, który ma sens dla tej firmy. Na przykład według roli lub działu. Zwróć uwagę, że zasoby mogą współużytkować ten sam tag (być oznaczone tym samym tagiem), nawet jeśli nie znajdują się w tej samej grupie zasobów. Firma Contoso utworzy prostą taksonomię tagów, dzięki czemu wszyscy będą korzystać z tych samych tagów.

**Nazwa tagu** | **Wartość**
--- | ---
CostCenter | 12345: Musi być prawidłowym centrum kosztów z systemu SAP.
BusinessUnit | Nazwa jednostki biznesowej (z oprogramowania SAP). Dopasowuje CostCenter.
ApplicationTeam | Alias adresu e-mail zespołu, który jest właścicielem pomocy technicznej dla aplikacji.
CatalogName | Nazwa aplikacji lub ShareServices dla katalogu usług obsługiwanego przez zasób.
ServiceManager | Alias adresu e-mail menedżera usługi ITIL dla zasobu.
COBPriority | Priorytet ustawiony przez firmę dla ciągłości działania i odzyskiwania po awarii. Wartości 1–5.
ENV | Możliwe wartości to DEV, STG, PROD. Reprezentują one, odpowiednio, środowisko deweloperskie, przejściowe i produkcyjne.

Przykład:

 ![Tagi platformy Azure](./media/contoso-migration-infrastructure/azure-tag.png)

Po utworzeniu tagu firma Contoso wróci i utworzy nowe definicje i przypisania zasad, aby wymusić używanie wymaganych tagów w całej organizacji.

## <a name="step-6-consider-security"></a>Krok 6: Uwzględnianie zabezpieczeń

W chmurze bezpieczeństwo ma kluczowe znaczenie, a platforma Azure oferuje szeroką gamę narzędzi i możliwości zabezpieczeń. Ułatwiają one tworzenie bezpiecznych rozwiązań na bezpiecznej platformie Azure. Przeczytaj artykuł [Chmura, której można zaufać](https://azure.microsoft.com/overview/trusted-cloud), aby dowiedzieć się więcej o zabezpieczeniach platformy Azure.

Istnieje kilka aspektów, którymi firma Contoso musi się zająć:

- **Azure Security Center:** Usługa Azure Security Center zapewnia ujednolicone zarządzanie zabezpieczeniami i zaawansowaną ochronę przed zagrożeniami na potrzeby różnych obciążeń chmury hybrydowej. Usługa Security Center umożliwia stosowanie zasad zabezpieczeń do różnych obciążeń, ograniczanie podatności na zagrożenia i wykrywanie ataków oraz reagowanie na nie. [Dowiedz się więcej](https://docs.microsoft.com/azure/security-center/security-center-intro).
- **Sieciowe grupy zabezpieczeń (NSG):** Sieciowa grupa zabezpieczeń (zapora) jest filtrem zawierającym listę reguł zabezpieczeń, które po zastosowaniu blokują lub zezwalają na ruch sieciowy do zasobów połączonych z sieciami wirtualnymi platformy Azure. [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-network/security-overview).
- **Szyfrowanie danych:** Usługa Azure Disk Encryption jest możliwością ułatwiającą szyfrowanie dysków maszyn wirtualnych IaaS z systemami Windows i Linux. [Dowiedz się więcej](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest).

### <a name="work-with-the-azure-security-center"></a>Praca z usługą Azure Security Center

Firma Contoso chce mieć szybki wgląd w stan zabezpieczeń swojej nowej chmury hybrydowej, a zwłaszcza obciążeń platformy Azure. W rezultacie firma Contoso zdecydowała się zaimplementować usługę Azure Security Center, rozpoczynając od następujących funkcji:

- Scentralizowane zarządzanie zasadami
- Ciągła ocena
- Zalecenia z możliwością wykonywania akcji

#### <a name="centralize-policy-management"></a>Scentralizowane zarządzanie zasadami

Dzięki scentralizowanemu zarządzaniu zasadami firma Contoso będzie zapewniać zgodność z wymaganiami dotyczącymi zabezpieczeń, centralnie zarządzając zasadami zabezpieczeń w całym środowisku. W ten sposób może łatwo i szybko zaimplementować zasady, które mają zastosowanie do wszystkich zasobów platformy Azure.

![Zasady zabezpieczeń](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Ocena i działanie

Firma Contoso będzie korzystać z ciągłej oceny zabezpieczeń, która monitoruje zabezpieczenia maszyn, sieci, magazynu, danych i aplikacji pod kątem potencjalnych problemów z zabezpieczeniami.

- Usługa Security Center będzie analizować stan zabezpieczeń zasobów obliczeniowych, infrastruktury i danych firmy Contoso oraz usług i aplikacji platformy Azure.
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

![Bezpieczeństwo](./media/contoso-migration-infrastructure/asg.png)

Sieciowe grupy zabezpieczeń skojarzone z grupami zabezpieczeń aplikacji zostaną skonfigurowane z najniższymi uprawnieniami w celu zapewnienia, że tylko dozwolone pakiety mogą przepływać z jednej części sieci do jej lokalizacji docelowej.

**Akcja** | **Nazwa** | **Element źródłowy** | **Obiekt docelowy** | **Port**
--- | --- | --- | --- | ---
Allow | AllowiInternetToFE | VNET-HUB-EUS1/IB-TrustZone | APP1-FE 80, 443
Allow | AllowWebToApp | APP1-FE | APP1-APP | 80, 443
Allow | AllowAppToDB | APP1-APP | APP1-DB | 1433
Zablokuj | DenyAllInbound | Any | Any | Any

### <a name="encrypt-data"></a>Szyfrowanie danych

Usługa Azure Disk Encryption integruje się z usługą Azure Key Vault, aby pomóc w sterowaniu i zarządzaniu wpisami tajnymi i kluczami szyfrowania dysków w ramach subskrypcji usługi Key Vault. Gwarantuje to, że wszystkie dane na dyskach maszyn wirtualnych są szyfrowane podczas przechowywania w magazynie platformy Azure.

- Firma Contoso ustaliła, że określone maszyny wirtualne wymagają szyfrowania.
- Firma Contoso zastosuje szyfrowanie do maszyn wirtualnych z danymi klienta, poufnymi lub podlegającymi ochronie danych osobowych.

## <a name="conclusion"></a>Wniosek

W tym artykule firma Contoso konfiguruje infrastrukturę i zasady platformy Azure dla subskrypcji platformy Azure oraz funkcji identyfikacji hybrydowej, odzyskiwania po awarii, sieci, ładu i zabezpieczeń.

Nie wszystkie kroki wykonane tutaj przez firmę Contoso są wymagane do przeprowadzenia migracji do chmury. W takim przypadku warto zaplanować infrastrukturę sieci, która może być używana dla wszystkich typów migracji, jest bezpieczna, odporna na błędy i skalowalna.

Po wdrożeniu tej infrastruktury firma Contoso jest gotowa do przejścia do następnego etapu i wypróbowania migracji.

## <a name="next-steps"></a>Następne kroki

Po skonfigurowaniu infrastruktury platformy Azure firma Contoso jest gotowa do rozpoczęcia migracji obciążeń do chmury. Zobacz sekcję [wzorców i przykładów dotyczących migracji](./contoso-migration-overview.md#windows-server-workloads) w celu wybrania scenariuszy korzystających z tej przykładowej infrastruktury jako celu migracji.
