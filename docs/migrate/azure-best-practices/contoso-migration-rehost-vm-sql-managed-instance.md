---
title: Ponowne hostowanie aplikacji lokalnej przez migrację do maszyn wirtualnych platformy Azure i wystąpienia zarządzanego usługi Azure SQL Database
description: Dowiedz się, w jaki sposób firma Contoso przeprowadza ponowne hostowanie aplikacji lokalnej na maszynach wirtualnych platformy Azure za pomocą wystąpienia zarządzanego usługi Azure SQL Database.
author: givenscj
ms.author: abuck
ms.date: 04/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 089a772bdc41bc96f327f9d9ce34d2107fd48934
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80996793"
---
<!-- cSpell:ignore givenscj WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL contosohost vcenter contosodc NSGs agentless SQLMI iisreset -->

# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>Ponowne hostowanie aplikacji lokalnej na maszynie wirtualnej platformy Azure i wystąpieniu zarządzanym usługi SQL Database

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso migruje dwuwarstwową aplikację frontonu systemu Windows .NET działającą na maszynach wirtualnych VMware na maszynę wirtualną platformy Azure przy użyciu usługi Azure Migrate. Pokazano również, jak firma Contoso migruje bazę danych aplikacji do wystąpienia zarządzanego usługi Azure SQL Database.

Używana w tym przykładzie aplikacja SmartHotel360 jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT firmy Contoso w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się. W związku z tym zwiększyło się obciążenie lokalnych systemów i infrastruktury firmy.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury i usprawnić procesy dla swoich deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, a firma mogła dzięki temu szybciej obsługiwać swoich klientów.
- **Zwiększenie elastyczności.** Dział IT firmy Contoso chce lepiej odpowiadać na zapotrzebowania biznesowe. Chce być w stanie szybciej reagować na zamiany zachodzące na rynku, aby odnosić sukcesy w gospodarce światowej. Firma Contoso nie chce utrudniać pracy ani stać się przeszkodą biznesową.
- **Zasięgu.** W miarę rozwoju firmy Contoso jej dział IT musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso zidentyfikował cele tej migracji. Firma określa najlepszą metodę migracji przy użyciu celów migracji.

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie w lokalnym środowisku VMware firmy Contoso. Przeniesienie do chmury nie oznacza, że wydajność aplikacji jest mniej istotna.
- Firma Contoso nie chce inwestować w aplikację. Aplikacja ma istotne znaczenie dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Po zmigorwaniu aplikacji zadania dotyczące administrowania bazą danych powinny być zminimalizowane.
- Firma Contoso nie chce używać usługi Azure SQL Database dla tej aplikacji. Szuka alternatywy.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu swoich celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które zostaną użyte do tego celu.

### <a name="current-architecture"></a>Bieżąca architektura

- Firma Contoso ma jedno główne centrum danych (**contoso-datacenter**). Centrum danych znajduje się w Nowym Jorku we wschodnich Stanach Zjednoczonych.
- Firma Contoso ma trzy dodatkowe oddziały lokalne na terenie Stanów Zjednoczonych.
- Główne centrum danych jest połączone z Internetem łączem światłowodowym Metro Ethernet (500 MB/s).
- Każdy oddział jest połączony lokalnie z Internetem przy użyciu połączeń klasy biznesowej z tunelami IPsec sieci VPN z głównym centrum danych. Taka konfiguracja zapewnia trwałe połączenie całej sieci firmy Contoso i optymalizację łączności z Internetem.
- Główne centrum danych jest w pełni zwirtualizowane przy użyciu programu VMware. Firma Contoso ma dwa hosty wirtualizacji ESXi 6.5, które są zarządzane za pomocą programu vCenter Server 6.5.
- Do zarządzania tożsamościami firma Contoso używa usługi Active Directory. Serwery DNS firmy Contoso działają w sieci wewnętrznej.
- Firma Contoso używa lokalnego kontrolera domeny (**ContosoDC1**).
- Kontrolery domeny działają na maszynach wirtualnych VMware. Kontrolery domeny w lokalnych oddziałach działają na serwerach fizycznych.
- Aplikacja SmartHotel360 jest podzielona na warstwy między dwie maszyny wirtualne (**WEBVM** i **SQLVM**), które znajdują się na hoście VMware ESXi w wersji 6.5 (**contosohost1.contoso.com**).
- Środowisko VMware jest zarządzane przez vCenter Server 6,5 (**vCenter.contoso.com**) uruchomionego na maszynie wirtualnej.

![Bieżąca architektura firmy Contoso](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu firma Contoso chce zmigrować swoją dwuwarstwową lokalną aplikację turystyczną w następujący sposób:

- Zmigrować bazę danych aplikacji (**SmartHotelDB**) do wystąpienia zarządzanego usługi Azure SQL Database.
- Zmigrować maszynę wirtualną frontonu **WebVM** do maszyny wirtualnej platformy Azure.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i wystąpienia zarządzanego programu SQL Server. Następujące zagadnienia pomogły w podjęciu decyzji o wybraniu wystąpienia zarządzanego.

- Wystąpienie zarządzane ma na celu zapewnienie niemal 100% zgodności z najnowszą wersją lokalnego programu SQL Server. Firma Microsoft zaleca wystąpienia zarządzane dla klientów, którzy działają SQL Server lokalnie lub na maszynach wirtualnych IaaS i chcą migrować swoje aplikacje do w pełni zarządzanej usługi przy minimalnych zmianach projektu.
- Firma Contoso planuje migrację dużej liczby aplikacji z lokalizacji lokalnej do modelu IaaS. Wiele z nich jest udostępnianych przez niezależnych dostawców oprogramowania. Firma Contoso zdaje sobie sprawę z używania wystąpienia zarządzanego, która zapewni zgodność bazy danych dla tych aplikacji, a nie za pomocą SQL Database, które mogą nie być obsługiwane.
- Firma Contoso może wykonać operację podnoszenia i przeshift do wystąpienia zarządzanego przy użyciu w pełni zautomatyzowanego Azure Database Migration Service. Firma Contoso może w przyszłości ponownie wykorzystać tę usługę do migracji baz danych.
- Wystąpienie zarządzane SQL obsługuje agenta SQL Server, ważnym składnikiem aplikacji SmartHotel360. Firma Contoso potrzebuje tej zgodności, ponieważ w przeciwnym razie będzie musiała ponownie zaprojektować plany konserwacji wymagane przez aplikację.
- Dzięki programowi Software Assurance firma Contoso może wymienić swoje istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Dzięki temu firma Contoso może zaoszczędzić do 30% na wystąpieniu zarządzanym.
- Wystąpienie zarządzane SQL jest w pełni zawarte w sieci wirtualnej, dzięki czemu zapewnia większą izolację i bezpieczeństwo danych firmy Contoso. Firma Contoso może korzystać z zalet chmury publicznej, jednocześnie zapewniając izolację środowiska od publicznego Internetu.
- Wystąpienie zarządzane obsługuje wiele funkcji zabezpieczeń, w tym zawsze zaszyfrowane, dynamiczne maskowanie danych, zabezpieczenia na poziomie wiersza i wykrywanie zagrożeń.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Uzyskać**
--- | ---
**Zalety** | Maszyna wirtualna WEBVM zostanie przeniesiona na platformę Azure bez zmian, co oznacza prostą migrację.<br/><br/> Wystąpienie zarządzane SQL spełnia wymagania techniczne i cele firmy Contoso.<br/><br/> Wystąpienie zarządzane zapewni 100-procentową zgodność z bieżącym wdrożeniem przy jednoczesnym zaprzestaniu korzystania z programu SQL Server 2008 R2.<br/><br/> Firma może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server.<br/><br/> Może ponownie użyć usługi Azure Database Migration Service na potrzeby dodatkowych przyszłych migracji.<br/><br/> Wystąpienie zarządzane SQL ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi konfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Na maszynie wirtualnej WEBVM jest uruchomiony system Windows Server 2008 R2. Mimo iż ten system operacyjny jest obsługiwany przez platformę Azure, nie jest już obsługiwaną platformą. [Dowiedz się więcej](https://support.microsoft.com/help/956893).<br/><br/> Warstwa internetowa pozostaje pojedynczym punktem awarii, a usługi świadczy tylko maszyna wirtualna WEBVM.<br/><br/> Firma Contoso nadal będzie musiała obsługiwać warstwę internetową aplikacji jako maszynę wirtualną, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service.<br/><br/> W przypadku warstwy danych wystąpienie zarządzane może nie być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub serwer bazy danych lub jeśli chce uruchamiać aplikacje innych firm wraz z programem SQL Server. Uruchomienie programu SQL Server na maszynie wirtualnej IaaS może zapewnić taką elastyczność.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi migrację warstw internetowych i danych aplikacji SmartHotel360 na platformę Azure, wykonując następujące czynności:

1. Firma Contoso ma już swoją infrastrukturę platformy Azure, więc w tym scenariuszu wystarczy dodać kilka określonych składników platformy Azure.
2. Warstwa danych zostanie zmigrowana przy użyciu usługi Azure Database Migration Service. Ta usługa nawiązuje połączenie z lokalną maszyną wirtualną z programem SQL Server przy użyciu połączenia sieci VPN typu lokacja-lokacja między centrum danych firmy Contoso i platformą Azure. Następnie usługa migruje bazę danych.
3. Warstwa sieci Web zostanie zmigrowana przy użyciu podnośnika i migracji przesuniętej przy użyciu Azure Migrate. Proces ten obejmuje przygotowanie lokalnego środowiska VMware, skonfigurowanie i włączenie replikacji oraz zmigrowanie maszyn wirtualnych przez przełączenie ich w tryb failover na platformie Azure.

     ![Architektura migracji](./media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Usługi Azure

Usługa | Opis | Koszty
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Wystąpienie zarządzane usługi Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Wystąpienie zarządzane to usługa zarządzanej bazy danych, która reprezentuje w pełni zarządzane wystąpienie programu SQL Server w chmurze platformy Azure. Używa tego samego kodu co najnowsza wersja aparatu bazy danych programu SQL Server oraz ma najnowsze funkcje, ulepszenia wydajności i poprawki zabezpieczeń. | Korzystanie z wystąpienia zarządzanego usługi SQL Database uruchomionego na platformie Azure powoduje naliczanie opłat zależnych od pojemności. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) | Firma Contoso używa usługi Azure Migrate do oceny swoich maszyn wirtualnych VMware. Usługa Azure Migrate ocenia przydatność maszyn do migracji. Dzięki tej usłudze można oszacować wymagany rozmiar i koszt działania na platformie Azure. | Od maja 2018 r. Azure Migrate jest usługą bezpłatną.

## <a name="prerequisites"></a>Wymagania wstępne

Firma Contoso i inni użytkownicy muszą spełniać następujące wymagania wstępne dotyczące tego scenariusza:

<!-- markdownlint-disable MD033 -->

Wymagania | Szczegóły
--- | ---
**Subskrypcja platformy Azure** | Subskrypcję należy utworzyć jeszcze przed przeprowadzeniem oceny w pierwszym artykule w tej serii. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś administratorem subskrypcji, musisz skontaktować się z administratorem, aby przypisać uprawnienia właściciela lub współautora do niezbędnych grup zasobów i zasobów.
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Azure infrastructure for Migration (Infrastruktura platformy Azure wymagana do migracji)](./contoso-migration-infrastructure.md).
**Serwery lokalne** | Lokalny serwer vCenter w wersji 5.5, 6.0 lub 6.5<br/><br/> Host ESXi w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.
**Lokalne maszyny wirtualne** | [Przejrzyj maszyny z systemem Linux](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros), które zostały zatwierdzone do działania na platformie Azure.
**Database Migration Service** | W przypadku usługi Azure Database Migration Service potrzebne jest [zgodne lokalne urządzenie sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Musisz mieć możliwość skonfigurowania lokalnego urządzenia sieci VPN. Musi ono mieć widoczny zewnętrznie publiczny adres IPv4. Adres nie może znajdować się za urządzeniem NAT.<br/><br/> Upewnij się, że możesz uzyskać dostęp do lokalnej bazy danych SQL Server.<br/><br/> Zapora systemu Windows powinna mieć dostęp do aparatu źródłowej bazy danych. Dowiedz się, jak [skonfigurować zaporę systemu Windows pod kątem dostępu do aparatu bazy danych](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).<br/><br/> Jeśli przed maszyną bazy danych znajduje się zapora, dodaj reguły zezwalające na dostęp do bazy danych za pośrednictwem portu SMB 445.<br/><br/> Poświadczenia, które służą do nawiązywania połączenia ze źródłowym wystąpieniem programu SQL Server i których elementem docelowym jest wystąpienie zarządzane, muszą być elementami członkowskimi roli serwera sysadmin.<br/><br/> Musisz mieć udział sieciowy w lokalnej bazie danych umożliwiający wykonanie kopii zapasowej źródłowej bazy danych za pomocą usługi Azure Database Migration Service.<br/><br/> Upewnij się, że konto usługi, na którym uruchomiono źródłowe wystąpienie programu SQL Server, ma uprawnienia do zapisu w udziale sieciowym.<br/><br/> Zanotuj nazwę i hasło użytkownika systemu Windows, który ma uprawnienia do pełnej kontroli nad udziałem sieciowym. Usługa Azure Database Migration Service personifikuje te poświadczenia użytkownika w celu przekazania plików kopii zapasowej do kontenera usługi Azure Storage.<br/><br/> Proces instalacji programu SQL Server Express domyślnie zmienia ustawienie protokołu TCP/IP na wartość **Wyłączony**. Upewnij się, że ustawienie to jest włączone.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Oto jak firma Contoso planuje skonfigurować wdrożenie:

> [!div class="checklist"]
>
> - **Krok 1: przygotowanie SQL Database wystąpienia zarządzanego.** Firma Contoso potrzebuje istniejącego wystąpienia zarządzanego, do którego zostanie zmigrowana lokalna baza danych programu SQL Server.
> - **Krok 2: przygotowanie Azure Database Migration Service.** Firma Contoso musi zarejestrować dostawcę migracji bazy danych, utworzyć wystąpienie, a następnie utworzyć projekt usługi Azure Database Migration Service. Firma Contoso musi również skonfigurować identyfikator URI sygnatury dostępu współdzielonego (SAS) dla usługi Azure Database Migration Service. Identyfikator URI sygnatury dostępu współdzielonego zapewnia delegowany dostęp do zasobów na koncie magazynu firmy Contoso, dzięki czemu firma Contoso może przyznać ograniczone uprawnienia do obiektów magazynu. Firma Contoso konfiguruje identyfikator URI sygnatury dostępu współdzielonego, aby usługa Azure Database Migration Service mogła uzyskać dostęp do kontenera konta magazynu, do którego przekaże pliki kopii zapasowej programu SQL Server.
> - **Krok 3. Przygotowywanie platformy Azure do Azure Migrate migracji serwera.** Dodają narzędzie migracji serwera do projektu usługi Azure Migrate.
> - **Krok 4: Przygotowanie lokalnej migracji programu VMware do Azure Migrate serwera.** Przygotowuje konta do odnajdywania maszyn wirtualnych i przygotowuje się do łączenia się z maszynami wirtualnymi platformy Azure po migracji.
> - **Krok 5. replikowanie maszyn wirtualnych.** Konfigurują replikację i rozpoczynają replikowanie maszyn wirtualnych w magazynie platformy Azure.
> - **Krok 6. Migrowanie bazy danych przy użyciu Azure Database Migration Service.** Firma Contoso zmigruje bazę danych.
> - **Krok 7. Migrowanie maszyny wirtualnej przy użyciu migracji Azure Migrate Server.** Przeprowadza migrację testową, aby upewnić się, że wszystko działa, a następnie uruchomić pełną migrację, aby przenieść maszyny wirtualne na platformę Azure.

## <a name="step-1-prepare-a-sql-database-managed-instance"></a>Krok 1. Przygotowanie SQL Database wystąpienia zarządzanego

Aby skonfigurować wystąpienie zarządzane usługi Azure SQL Database, firma Contoso musi mieć podsieć, która spełnia następujące wymagania:

- Podsieć musi być dedykowana. Musi być pusta i nie może zawierać żadnej innej usługi w chmurze. Podsieć nie może być podsiecią bramy.
- Po utworzeniu wystąpienia zarządzanego firma Contoso nie powinna dodawać zasobów do tej podsieci.
- Z podsiecią nie może być skojarzona żadna sieciowa grupa zabezpieczeń.
- Podsieć musi mieć zdefiniowaną przez użytkownika tabelę tras. Jedyną przypisaną trasą powinna być 0.0.0.0/0 z następnym przeskokiem do Internetu.
- Opcjonalny niestandardowy serwer DNS: Jeśli w sieci wirtualnej platformy Azure jest określony niestandardowy serwer DNS, należy dodać do listy adres IP rekursywnych tłumaczeń platformy Azure (na przykład 168.63.129.16). Dowiedz się, jak [skonfigurować niestandardowy serwer DNS dla wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- Z podsiecią nie może być skojarzony żaden punkt końcowy usługi (magazyn lub SQL). Punkty końcowe usługi powinny być wyłączone w sieci wirtualnej.
- Podsieć musi mieć co najmniej 16 adresów IP. Dowiedz się, jak [zmienić rozmiar podsieci wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- W środowisku hybrydowym firmy Contoso wymagane są niestandardowe ustawienia DNS. Firma Contoso skonfiguruje ustawienia DNS, aby używać co najmniej jednego serwera DNS platformy Azure firmy. Dowiedz się więcej o [dostosowywaniu serwerów DNS](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Konfigurowanie sieci wirtualnej dla wystąpienia zarządzanego

Administratorzy firmy Contoso konfigurują sieć wirtualną w następujący sposób:

1. Tworzą nową sieć wirtualną (**VNET-SQLMI-EU2**) w regionie podstawowym Wschodnie stany USA 2. Spowoduje to dodanie sieci wirtualnej do grupy zasobów **ContosoNetworkingRG**.
2. Przypisują przestrzeń adresową 10.235.0.0/24. Dzięki temu zakres nie będzie pokrywał się z innymi sieciami w tym przedsiębiorstwie.
3. Dodają dwie podsieci do sieci:
    - **SQLMI-ds-EUS2** (10.235.0.0.25).
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Ta podsieć służy do dołączania katalogu do wystąpienia zarządzanego.

      ![Wystąpienie zarządzane — tworzenie sieci wirtualnej](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Po wdrożeniu sieci wirtualnej i podsieci sieci są one łączone równorzędnie w następujący sposób:

    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-HUB-EUS2** (sieć wirtualna koncentratora dla regionu Wschodnie stany USA 2),
    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-PROD-EUS2** (sieć produkcyjna).

      ![Komunikacja równorzędna sieci](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Określają niestandardowe ustawienia DNS. Serwer DNS wskazuje najpierw kontrolery domeny platformy Azure firmy Contoso. Serwer DNS platformy Azure jest pomocniczy. Kontrolery domeny platformy Azure firmy Contoso znajdują się w następujących lokalizacjach:

    - Znajduje się w podsieci **prod-DC-EUS2** w sieci produkcyjnej Wschodnie stany USA 2 (**VNET-prod-EUS2**).
    - Adres **CONTOSODC3** : 10.245.42.4.
    - Adres **CONTOSODC4** : 10.245.42.5.
    - Azure DNS resolver: 168.63.129.16.

      ![Serwery DNS sieci](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Potrzebujesz dalszej pomocy?**

- Zapoznaj się z omówieniem [wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Dowiedz się, jak [utworzyć sieć wirtualną dla wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Dowiedz się, jak [skonfigurować komunikację równorzędną](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Dowiedz się, jak [zaktualizować ustawienia DNS usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services/tutorial-create-instance).

### <a name="set-up-routing"></a>Konfigurowanie routingu

Wystąpienie zarządzane jest umieszczane w prywatnej sieci wirtualnej. Firma Contoso potrzebuje tabeli tras, aby jej sieć wirtualna mogła komunikować się z usługą zarządzania platformy Azure. Jeśli sieć wirtualna nie może komunikować się z usługą, która nią zarządza, ta sieć wirtualna staje się niedostępna.

Firma Contoso bierze pod uwagę następujące czynniki:

- Tabela tras zawiera zestaw reguł (tras), które określają sposób, w jaki pakiety wysyłane z wystąpienia zarządzanego powinny być kierowane w sieci wirtualnej.
- Tabela tras jest skojarzona z podsieciami, w których są wdrażane wystąpienia zarządzane. Każdy pakiet, który opuszcza podsieć, jest obsługiwany na podstawie skojarzonej tabeli tras.
- Podsieć może być skojarzona tylko z jedną tabelą tras.
- Nie ma dodatkowych opłat za tworzenie tabel tras na platformie Microsoft Azure.

 Aby skonfigurować Routing, Administratorzy firmy Contoso wykonują następujące czynności:

1. Tworzą zdefiniowaną przez użytkownika tabelę tras w grupie zasobów **ContosoNetworkingRG**.

    ![Tabela tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Aby zachować zgodność z wymaganiami wystąpienia zarządzanego, po wdrożeniu tabeli tras(**MIRouteTable**) dodają trasę z prefiksem adresu 0.0.0.0/0. Opcja **Typ następnego przeskoku** jest ustawiana na wartość **Internet**.

    ![Prefiks tabeli tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Kojarzą tabelę tras z podsiecią **SQLMI-DB-EUS2** (w sieci **VNET-SQLMI-EUS2**).

    ![Podsieć tabeli tras](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Potrzebujesz dalszej pomocy?**

Dowiedz się, jak [skonfigurować trasy dla wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

### <a name="create-a-managed-instance"></a>Tworzenie wystąpienia zarządzanego

Teraz administratorzy firmy Contoso mogą zaaprowizować wystąpienie zarządzane usługi SQL Database:

1. Ponieważ wystąpienie zarządzane obsługuje aplikację biznesową, administratorzy wdrażają je w regionie podstawowym firmy Wschodnie stany USA 2. Dodają wystąpienie zarządzane do grupy zasobów **ContosoRG**.
2. Wybierają warstwę cenową, rozmiar obliczeniowy i magazyn dla wystąpienia. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Wystąpienie zarządzane](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Po wdrożeniu wystąpienia zarządzanego w grupie zasobów **ContosoRG** pojawiają się dwa nowe zasoby:

    - klaster wirtualny na wypadek, gdyby firma Contoso miała wiele wystąpień zarządzanych,
    - wystąpienie zarządzane bazy danych programu SQL Server.

      ![Wystąpienie zarządzane](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Potrzebujesz dalszej pomocy?**

Dowiedz się, jak [zaaprowizować wystąpienie zarządzane](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started).

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Krok 2. Przygotowywanie Azure Database Migration Service

Aby przygotować usługę Azure Database Migration Service, administratorzy firmy Contoso muszą wykonać kilka czynności:

- Zarejestrować dostawcę usługi Azure Database Migration Service na platformie Azure.
- Umożliwić usłudze Azure Database Migration Service dostęp do usługi Azure Storage na potrzeby przekazywania plików kopii zapasowej używanych do migrowania bazy danych. Aby zapewnić dostęp do usługi Azure Storage, tworzą kontener usługi Azure Blob Storage. Generują identyfikator URI sygnatury dostępu współdzielonego dla kontenera usługi Blob Storage.
- Utworzyć projekt usługi Azure Database Migration Service.

Następnie wykonują następujące czynności:

1. Rejestrują dostawcę migracji bazy danych w ramach jego subskrypcji.
    ![Database Migration Service — rejestracja](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. Tworzą kontener usługi Blob Storage. Firma Contoso generuje identyfikator URI sygnatury dostępu współdzielonego, aby usługa Azure Database Migration Service mogła uzyskać do niego dostęp.

    ![Database Migration Service — generowanie identyfikatora URI sygnatury dostępu współdzielonego](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. Tworzą wystąpienia usługi Azure Database Migration Service.

    ![Database Migration Service — tworzenie wystąpienia](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. Umieszczają wystąpienie usługi Azure Database Migration Service w podsieci **PROD-DC-EUS2** sieci wirtualnej **VNET-PROD-DC-EUS2**.
    - Usługa Azure Database Migration Service jest umieszczana w tym miejscu, ponieważ usługa musi znajdować się w sieci wirtualnej, która może uzyskać dostęp do lokalnej maszyny wirtualnej z programem SQL Server za pośrednictwem bramy sieci VPN.
    - Sieć wirtualna **VNET-PROD-EUS2** ma komunikuje się równorzędnie z siecią wirtualną **VNET-HUB-EUS2** i może korzystać z bram zdalnych. Opcja **Użyj zdalnych bram** zapewnia, że usługa Azure Database Migration Service może komunikować się zgodnie z potrzebami.

        ![Database Migration Service — konfigurowanie sieci](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Potrzebujesz dalszej pomocy?**

- Dowiedz się, jak [skonfigurować usługę Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal).
- Dowiedz się, jak [utworzyć sygnaturę dostępu współdzielonego i jej używać](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Krok 3. Przygotowanie platformy Azure do narzędzia migracji Azure Migrate Server

Oto składniki platformy Azure, których firma Contoso potrzebuje do zmigrowania maszyn wirtualnych na platformę Azure:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne platformy Azure, gdy są one tworzone podczas migracji.
- Aprowizowane narzędzie do migracji serwera usługi Azure Migrate Server.

Składniki te są konfigurowane w następujący sposób:

1. **Skonfiguruj sieć:** Firma Contoso już skonfigurował sieć, która może być dla migracji Azure Migrate serwera podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md)

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyny wirtualne zostaną zmigrowane do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie głównym Wschodnie stany USA 2.
    - Obie maszyny wirtualne zostaną umieszczone w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych.
    - Maszyna wirtualna frontonu aplikacji (WEBVM) zostanie zmigrowana do podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
    - Maszyna wirtualna bazy danych aplikacji (SQLVM) zostanie zmigrowana do podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.

## <a name="step-4-prepare-on-premises-vmware-for-azure-migrate-server-migration"></a>Krok 4. Przygotowanie lokalnej migracji programu VMware do Azure Migrate serwera

Oto składniki platformy Azure, których firma Contoso potrzebuje do zmigrowania maszyn wirtualnych na platformę Azure:

- Sieć wirtualna, w której będą znajdować się maszyny wirtualne platformy Azure, gdy są one tworzone podczas migracji.
- Zainicjowano i skonfigurowano narzędzie do migracji Azure Migrate Server (komórki jajowe).

Składniki te są konfigurowane w następujący sposób:

1. Konfigurowanie sieci — firma Contoso ma już sieć, której można używać w przypadku migracji serwera usługi Azure Migrate podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md)

    - Aplikacja SmartHotel360 jest aplikacją produkcyjną, a maszyny wirtualne zostaną zmigrowane do sieci produkcyjnej platformy Azure (VNET-PROD-EUS2) w regionie głównym Wschodnie stany USA 2.
    - Obie maszyny wirtualne zostaną umieszczone w grupie zasobów ContosoRG, która jest używana na potrzeby zasobów produkcyjnych.
    - Maszyna wirtualna frontonu aplikacji (WEBVM) zostanie zmigrowana do podsieci frontonu (PROD-FE-EUS2) w sieci produkcyjnej.
    - Maszyna wirtualna bazy danych aplikacji (SQLVM) zostanie zmigrowana do podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej.

2. Inicjowanie obsługi administracyjnej narzędzia do migracji Azure Migrate Server.

    - Z Azure Migrate Pobierz obraz komórki jajowe i zaimportuj go do programu VMWare.

        ![Pobierz plik komórki jajowe](./media/contoso-migration-rehost-vm/migration-download-ova.png)

    - Uruchom zaimportowany obraz i skonfiguruj narzędzie, w tym następujące kroki:

      - Skonfiguruj wymagania wstępne.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-setup-prerequisites.png)

      - Wskaż narzędzie subskrypcję platformy Azure.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-register-azure.png)

      - Ustaw poświadczenia programu VMWare vCenter.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-vcenter-server.png)

      - Dodaj do odnajdywania dowolne poświadczenia oparte na systemie Linux lub Windows.

        ![Konfigurowanie narzędzia](./media/contoso-migration-rehost-vm/migration-credentials.png)

3. Po skonfigurowaniu narzędzia mogą wyliczyć wszystkie maszyny wirtualne. Po zakończeniu zobaczysz je w narzędziu Azure Migrate na platformie Azure.

**Potrzebujesz dalszej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/migrate) o konfigurowaniu narzędzia migracji serwera usługi Azure Migrate.

### <a name="prepare-on-premises-vms"></a>Przygotowywanie lokalnych maszyn wirtualnych

Po migracji firma Contoso chce nawiązać połączenie z maszynami wirtualnymi platformy Azure i umożliwić platformie Azure zarządzanie maszynami wirtualnymi. W tym celu administratorzy firmy Contoso wykonują następujące czynności przed migracją:

1. W celu uzyskania dostępu przez Internet:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Upewniają się, że zostały dodane reguły TCP i UDP dla profilu **publicznego**.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.

2. W celu uzyskania dostępu przez sieć VPN lokacja-lokacja:

    - Przed migracją Włącz protokół RDP lub SSH na lokalnej maszynie wirtualnej.
    - Sprawdź, czy w zaporze systemu operacyjnego jest dozwolony protokół RDP lub SSH.
    - Dla systemu Windows Ustaw zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na **OnlineAll**.

3. Zainstaluj agenta platformy Azure:

    - [Agent systemu Linux platformy Azure](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux)
    - [Agent systemu Windows Azure](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-windows)

4. Różne

   - W przypadku systemu Windows na maszynie wirtualnej nie ma żadnych oczekujących aktualizacji podczas wyzwalania migracji. W przeciwnym razie nie będzie można zalogować się na maszynie wirtualnej do momentu ukończenia aktualizacji.
   - Po migracji można sprawdzić **diagnostykę rozruchu** , aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli to nie zadziała, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

5. Potrzebujesz dodatkowej pomocy?

   - [Dowiedz się więcej o](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-vm#prepare-vms-for-migration) przygotowywaniu maszyn wirtualnych do migracji.

## <a name="step-5-replicate-the-on-premises-vms"></a>Krok 5. replikowanie lokalnych maszyn wirtualnych

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

Po ukończeniu odnajdywania można rozpocząć replikację maszyn wirtualnych VMware na platformę Azure.

1. Na **serwerach**Azure Migrate project > **Azure Migrate: Migracja serwera**, kliknij przycisk **replikacja**.

    ![Replikowanie maszyn wirtualnych](./media/contoso-migration-rehost-vm/select-replicate.png)

2. W obszarze **Replikacja** > **Ustawienia źródła** > **Czy maszyny są zwirtualizowane** wybierz pozycję **Tak, z funkcją VMware vSphere Hypervisor**.

3. W obszarze **Urządzenie lokalne** wybierz nazwę skonfigurowanego urządzenia usługi Azure Migrate > przycisk **OK**.

    ![Ustawienia źródła](./media/contoso-migration-rehost-vm/source-settings.png)

4. W obszarze **Maszyny wirtualne** wybierz maszyny wirtualne, które mają być replikowane.
    - Jeśli przeprowadzasz ocenę dla maszyn wirtualnych, możesz zastosować rekomendacje dotyczące rozmiarów maszyn wirtualnych i typów dysków (Premium/standardowy) w wynikach oceny. W tym celu w obszarze **Zaimportować ustawienia migracji z oceny usługi Azure Migrate?** wybierz opcję **Tak**.
    - Jeśli nie uruchomiono oceny lub nie chcesz używać ustawień oceny, wybierz opcję **Nie**.
    - W przypadku wybrania opcji korzystania z oceny wybierz grupę maszyn wirtualnych i nazwę oceny.

    ![Wybieranie oceny](./media/contoso-migration-rehost-vm/select-assessment.png)

5. W obszarze **Maszyny wirtualne** wyszukaj potrzebne maszyny wirtualne i sprawdź każdą maszynę wirtualną, którą chcesz migrować. Następnie kliknij przycisk **Dalej: ustawienia docelowe**.

6. W obszarze **Ustawienia elementu docelowego** wybierz subskrypcję i docelowy region migracji, a następnie określ grupę zasobów, w której będą znajdować się maszyny wirtualne platformy Azure po migracji. W obszarze **Sieć wirtualna** wybierz sieć wirtualną/podsieć platformy Azure, do której zostaną dołączone maszyny wirtualne platformy Azure po migracji.

7. W **korzyść użycia hybrydowego platformy Azure**wybierz następujące opcje:

    - Wybierz pozycję **Nie**, jeśli nie chcesz stosować korzyści użycia hybrydowego platformy Azure. Następnie kliknij przycisk **Dalej**.
    - Wybierz opcję **Tak**, jeśli masz maszyny z systemem Windows Server, które są objęte aktywnym programem Software Assurance lub subskrypcjami systemu Windows Server, i chcesz zastosować korzyść do migrowanych maszyn. Następnie kliknij przycisk **Dalej**.

8. W obszarze **Obliczenia** sprawdź nazwę, rozmiar, typ dysku systemu operacyjnego i zestaw dostępności maszyny wirtualnej. Maszyny wirtualne muszą być zgodne z [wymaganiami platformy Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#vmware-requirements).

    - **Rozmiar maszyny wirtualnej:** Jeśli używasz zaleceń dotyczących oceny, lista rozwijana rozmiaru maszyny wirtualnej będzie zawierać zalecany rozmiar. W przeciwnym razie usługa Azure Migrate wybierze rozmiar na podstawie najbliższego dopasowania w subskrypcji platformy Azure. Alternatywnie możesz wybrać rozmiar ręczny w obszarze **rozmiaru maszyny wirtualnej platformy Azure**.
    - **Dysk systemu operacyjnego:** Określ dysk systemu operacyjnego (Boot) dla maszyny wirtualnej. Dysk systemu operacyjnego to dysk, na którym jest zainstalowany program ładujący i instalator systemu operacyjnego.
    - **Zestaw dostępności:** Jeśli maszyna wirtualna powinna znajdować się w zestawie dostępności platformy Azure po migracji, określ zestaw. Zestaw musi znajdować się w docelowej grupie zasobów określonej dla migracji.

9. W obszarze **Dyski** określ, czy dyski maszyn wirtualnych mają być replikowane na platformę Azure, a następnie wybierz typ dysku (standardowe dyski SSD/dyski twarde lub dyski zarządzane w warstwie Premium) na platformie Azure. Następnie kliknij przycisk **Dalej**.
    - Dyski można wykluczyć z replikacji.
    - Jeśli wykluczysz dyski, nie będą one znajdować się na maszynie wirtualnej platformy Azure po migracji.

10. W obszarze **Przegląd i rozpoczynanie replikacji** sprawdź ustawienia, a następnie kliknij pozycję **Replikuj**, aby uruchomić replikację początkową dla serwerów.

> [!NOTE]
> Ustawienia replikacji można aktualizować w dowolnym momencie przed rozpoczęciem replikacji w obszarze **Zarządzanie** > **maszynami replikowanymi**. Ustawień nie można zmienić po rozpoczęciu replikacji.

## <a name="step-6-migrate-the-database-using-the-azure-database-migration-service"></a>Krok 6. Migrowanie bazy danych przy użyciu Azure Database Migration Service

Administratorzy firmy Contoso muszą utworzyć projekt usługi Azure Database Migration Service, a następnie przeprowadzić migrację bazy danych.

### <a name="create-an-azure-database-migration-service-project"></a>Tworzenie projektu usługi Azure Database Migration Service

1. Tworzą projekt usługi Azure Database Migration Service. Wybierają typ serwera źródłowego **SQL Server** i **wystąpienie zarządzane usługi Azure SQL Database** jako element docelowy.

     ![Database Migration Service — nowy projekt migracji](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Zostanie otwarty Kreator migracji.

### <a name="migrate-the-database"></a>Migracja bazy danych

1. W Kreatorze migracji określają źródłową maszynę wirtualną, na której znajduje się lokalna baza danych. Wprowadzają poświadczenia w celu uzyskania dostępu do bazy danych.

    ![Database Migration Service — szczegóły środowiska źródłowego](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. Wybierają bazę danych do migracji (**SmartHotel.Registration**):

    ![Database Migration Service — wybieranie źródłowych baz danych](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source-db.png)

3. Wprowadzają dla elementu docelowego nazwę wystąpienia zarządzanego na platformie Azure oraz poświadczenia dostępu.

    ![Database Migration Service — szczegóły środowiska docelowego](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. W obszarze **nowe** > **uruchomienie migracji**należy określić ustawienia do uruchomienia migracji:
    - Poświadczenia środowiska źródłowego i docelowego.
    - Baza danych do zmigrowania.
    - Udział sieciowy utworzony na lokalnej maszynie wirtualnej. Usługa Azure Database Migration Service dodaje kopie zapasowe źródła do tego udziału.
        - Konto usługi uruchamiające źródłowe wystąpienie programu SQL Server musi mieć uprawnienia do zapisu w tym udziale.
        - Należy użyć ścieżki FQDN do udziału.
    - Identyfikator URI sygnatury dostępu współdzielonego umożliwiający usłudze Azure Database Migration Service uzyskiwanie dostępu do kontenera konta magazynu, do którego usługa przekazuje pliki kopii zapasowej na potrzeby migracji.

        ![Database Migration Service — konfigurowanie ustawień migracji](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

5. Zapisują ustawienia migracji, a następnie uruchamiają migrację.
6. W obszarze **Przegląd** monitorują stan migracji.

    ![Database Migration Service — monitorowanie](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

7. Po zakończeniu migracji sprawdzają, czy docelowe bazy danych istnieją w wystąpieniu zarządzanym.

    ![Database Migration Service — weryfikowanie migracji bazy danych](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vms-with-azure-migrate-server-migration"></a>Krok 7. Migrowanie maszyn wirtualnych przy użyciu migracji Azure Migrate serwera

Administratorzy firmy Contoso uruchamiają szybką migrację testową i sprawdzają, czy maszyna wirtualna działa prawidłowo, a następnie migruje maszynę wirtualną.

### <a name="run-a-test-migration"></a>Uruchamianie migracji testowej

1. W obszarze**serwery** >  **celów** > migracji**Azure Migrate: Migracja serwera**, kliknij przycisk **Testuj zmigrowane serwery**.

     ![Serwery z przeprowadzoną migracją testową](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Kliknij prawym przyciskiem myszy maszynę wirtualną do przetestowania, a następnie kliknij pozycję **Testuj migrację**.

    ![Testowanie migracji](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. W obszarze **Testowanie migracji** wybierz sieć wirtualną platformy Azure, w której zostanie umieszczona maszyna wirtualna platformy Azure po migracji. Zalecamy użycie sieci wirtualnej nieprodukcyjnej.
4. Zostanie uruchomione zadanie **Testowanie migracji**. Monitoruj zadanie w powiadomieniach portalu.
5. Po zakończeniu migracji sprawdź zmigrowane maszyny wirtualne platformy Azure w obszarze **Maszyny wirtualne** w witrynie Azure Portal. Nazwa maszyny ma sufiks **-Test**.
6. Po zakończeniu testu kliknij prawym przyciskiem myszy maszynę wirtualną platformy Azure w obszarze **Replikowanie maszyn**, a następnie kliknij pozycję **Wyczyść migrację testową**.

    ![Czyszczenie migracji](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrowanie maszyn wirtualnych

Teraz Administratorzy firmy Contoso uruchamiają pełną migrację, aby zakończyć przenoszenie.

1. W Azure Migrate **serwery** > > Project**Azure Migrate: Migracja serwera**, kliknij przycisk **replikowanie serwerów**.

    ![Replikowanie serwerów](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. W obszarze **Replikowanie maszyn** kliknij prawym przyciskiem myszy maszynę wirtualną > **Migruj**.
3. W obszarze **Migrowanie** > **Zamknij maszyny wirtualne i przeprowadź planowaną migrację bez utraty danych**wybierz pozycję **tak** > **OK**.
    - Domyślnie usługa Azure Migrate zamyka lokalną maszynę wirtualną i uruchamia replikację na żądanie, aby zsynchronizować wszystkie zmiany maszyny wirtualnej, które wystąpiły od momentu ostatniej replikacji. Gwarantuje to brak utraty danych.
    - Jeśli nie chcesz zamykać maszyny wirtualnej, wybierz pozycję **nie**.
4. Zostanie uruchomione zadanie migracji maszyny wirtualnej. Śledź zadanie w powiadomieniach platformy Azure.
5. Po zakończeniu zadania możesz wyświetlić maszynę wirtualną i zarządzać nią na stronie **Maszyny wirtualne**.
6. Na koniec aktualizuje rekordy DNS **WEBVM** na jednym z kontrolerów domeny contoso.

### <a name="update-the-connection-string"></a>Aktualizowanie parametrów połączenia

W ostatnim kroku procesu migracji administratorzy firmy Contoso aktualizują parametry połączenia aplikacji tak, aby wskazywały zmigrowaną bazę danych działającą na wystąpieniu zarządzanym firmy Contoso.

1. W Azure Portal znajdują się parametry połączenia, wybierając pozycję **Ustawienia** > **Parametry połączenia**.

    ![Parametry połączeń](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. Aktualizują parametry przy użyciu nazwy użytkownika i hasła wystąpienia zarządzanego usługi SQL Database.
3. Po skonfigurowaniu parametrów zastępują bieżące parametry połączenia w pliku web.config aplikacji.
4. Po zaktualizowaniu pliku i zapisaniu go ponownie uruchamiają usługi IIS na maszynie wirtualnej WEBVM za pomocą polecenia `iisreset /restart` w oknie wiersza polecenia.
5. Po ponownym uruchomieniu usług IIS aplikacja korzysta z bazy danych uruchomionej w wystąpieniu zarządzanym usługi SQL Database.
6. W tym momencie można zamknąć lokalną maszynę SQLVM. Migracja została ukończona.

**Potrzebujesz dalszej pomocy?**

- Dowiedz się, jak [uruchomić test trybu failover](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure).
- Dowiedz się, jak [utworzyć plan odzyskiwania](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).
- Dowiedz się, jak [przełączyć się do trybu failover na platformie Azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover).

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji aplikacja SmartHotel360 będzie działać na maszynie wirtualnej platformy Azure, a baza danych aplikacji SmartHotel360 będzie dostępna w wystąpieniu zarządzanym usługi Azure SQL Database.

Teraz firma Contoso musi wykonać następujące zadania oczyszczania:

- Usunąć maszynę WEBVM ze spisu programu vCenter Server.
- Usunąć maszynę SQLVM ze spisu programu vCenter Server.
- Usunąć maszyny WEBVM i SQLVM z lokalnych zadań tworzenia kopii zapasowej.
- Zaktualizować dokumentację wewnętrzną, aby była wyświetlana nowa lokalizacja i adres IP maszyny WEBVM.
- Usunąć maszynę SQLVM z dokumentacji wewnętrznej. Alternatywnie firma Contoso może skorygować dokumentację, aby maszyna SQLVM była wyświetlana jako usunięta i nieznajdująca się w spisie maszyn wirtualnych.
- Przejrzeć wszystkie zasoby, które wchodzą w interakcje ze zlikwidowanymi maszynami wirtualnymi. Zaktualizować odpowiednie ustawienia lub dokumentację, aby odzwierciedlić nową konfigurację.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po migracji zasobów na platformę Azure firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso przegląda maszyny wirtualne platformy Azure i wystąpienie zarządzane usługi SQL Database, aby sprawdzić, czy występują problemy z zabezpieczeniami dotyczące implementacji:

- Zespół przegląda sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyn wirtualnych. Sieciowe grupy zabezpieczeń pomagają zapewnić, że może być przekazywany tylko ruch dozwolony dla aplikacji.
- Zespół ds. zabezpieczeń firmy Contoso rozważa również objęcie ochroną danych na dysku przy użyciu usług Azure Disk Encryption i Azure Key Vault.
- Zespół włącza wykrywanie zagrożeń w wystąpieniu zarządzanym. Funkcja wykrywania zagrożeń wysyła alert do zespołu ds. zabezpieczeń firmy Contoso / systemu pomocy technicznej, aby otworzyć bilet w przypadku wykrycia zagrożenia. Dowiedz się więcej na temat [wykrywania zagrożeń dla wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-threat-detection).

     ![Zabezpieczenia wystąpienia zarządzanego — wykrywanie zagrożeń](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Aby dowiedzieć się więcej na temat rozwiązań z zakresu bezpieczeństwa dotyczących maszyn wirtualnych, zobacz [Najlepsze rozwiązania dotyczące zabezpieczeń dla obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Zapewnienie ciągłości działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Zachowaj bezpieczeństwo danych: Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=/azure/virtual-machines/linux/toc.json).
- Przechowuj aplikacje i uruchamiaj je: contoso replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).
- Firma Contoso zdobywa więcej informacji o zarządzaniu wystąpieniem zarządzanym SQL, w tym o [tworzeniu kopii zapasowych bazy danych](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Firma Contoso ma już licencję na maszynę WEBVM. Aby skorzystać z cen wynikających z korzyści użycia hybrydowego platformy Azure, firma Contoso konwertuje istniejącą maszynę wirtualną platformy Azure.
- Firma Contoso będzie używać [Azure Cost Management](https://azure.microsoft.com/services/cost-management) , aby zapewnić, że pozostają w ramach budżetów ustanowionych przez ich lidera.

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso rehostuje aplikację SmartHotel360 na platformie Azure przez Migrowanie maszyny wirtualnej frontonu aplikacji na platformę Azure przy użyciu usługi Azure Migrate. Firma Contoso przeprowadza migrację lokalnej bazy danych do wystąpienia zarządzanego usługi Azure SQL Database za pomocą usługi Azure Database Migration Service.
