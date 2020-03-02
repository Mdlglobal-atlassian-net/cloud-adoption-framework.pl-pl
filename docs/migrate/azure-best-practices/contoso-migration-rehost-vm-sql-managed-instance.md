---
title: Ponowne hostowanie aplikacji lokalnej przez migrację do maszyn wirtualnych platformy Azure i wystąpienia zarządzanego usługi Azure SQL Database
description: Dowiedz się, w jaki sposób firma Contoso przeprowadza ponowne hostowanie aplikacji lokalnej na maszynach wirtualnych platformy Azure za pomocą wystąpienia zarządzanego usługi Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 7ec95c75d81b93852a59ef137a02cc35d83a1cd3
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223073"
---
# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>Ponowne hostowanie aplikacji lokalnej na maszynie wirtualnej platformy Azure i wystąpieniu zarządzanym usługi SQL Database

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso migruje dwuwarstwową aplikację frontonu .NET systemu Windows działającą na maszynach wirtualnych VMware na maszynę wirtualną platformy Azure przy użyciu usługi Azure Site Recovery. Pokazano również, jak firma Contoso migruje bazę danych aplikacji do wystąpienia zarządzanego usługi Azure SQL Database.

Aplikacja SmartHotel360 używana w tym przykładzie jest oferowana jako aplikacja typu open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT firmy Contoso w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się. W związku z tym zwiększyło się obciążenie lokalnych systemów i infrastruktury firmy.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury i usprawnić procesy dla swoich deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, a firma mogła dzięki temu szybciej obsługiwać swoich klientów.
- **Zwiększenie elastyczności.** Firma Contoso chce lepiej odpowiadać na zapotrzebowania w branży. Chce być w stanie szybciej reagować na zamiany zachodzące na rynku, aby odnosić sukcesy w gospodarce światowej. Firma Contoso nie chce utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę rozwoju firmy Contoso jej dział IT musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.

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
- Główne centrum danych jest w pełni zwirtualizowane przy użyciu oprogramowania VMware. Firma Contoso ma dwa hosty wirtualizacji ESXi 6.5, które są zarządzane za pomocą programu vCenter Server 6.5.
- Do zarządzania tożsamościami firma Contoso używa usługi Active Directory. Serwery DNS firmy Contoso działają w sieci wewnętrznej.
- Firma Contoso używa lokalnego kontrolera domeny (**ContosoDC1**).
- Kontrolery domeny działają na maszynach wirtualnych VMware. Kontrolery domeny w lokalnych oddziałach działają na serwerach fizycznych.
- Aplikacja SmartHotel360 jest podzielona na warstwy między dwie maszyny wirtualne (**WEBVM** i **SQLVM**), które znajdują się na hoście VMware ESXi w wersji 6.5 (**contosohost1.contoso.com**).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.

![Bieżąca architektura firmy Contoso](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu firma Contoso chce zmigrować swoją dwuwarstwową lokalną aplikację turystyczną w następujący sposób:

- Zmigrować bazę danych aplikacji (**SmartHotelDB**) do wystąpienia zarządzanego usługi Azure SQL Database.
- Zmigrować maszynę wirtualną frontonu **WebVM** do maszyny wirtualnej platformy Azure.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Zagadnienia dotyczące bazy danych

W ramach procesu projektowania rozwiązania firma Contoso wykonała porównanie funkcji usługi Azure SQL Database i wystąpienia zarządzanego programu SQL Server. Następujące zagadnienia pomogły w podjęciu decyzji o wybraniu wystąpienia zarządzanego.

- Wystąpienie zarządzane ma na celu zapewnienie niemal 100% zgodności z najnowszą wersją lokalnego programu SQL Server. Firma Microsoft zaleca wystąpienie zarządzane dla klientów z programem SQL Server działającym lokalnie lub na maszynie wirtualnej IaaS, którzy chcą zmigrować swoje aplikacje do w pełni zarządzanej usługi przy minimalnych zmianach projektowych.
- Firma Contoso planuje migrację dużej liczby aplikacji z lokalizacji lokalnej do modelu IaaS. Wiele z nich jest udostępnianych przez niezależnych dostawców oprogramowania. Firma Contoso wie, że korzystanie z wystąpienia zarządzanego pomoże zapewnić zgodność bazy danych dla tych aplikacji, ale nie zapewni tego usługa SQL Database, która może nie być obsługiwana.
- Firma Contoso może po prostu przetworzyć dźwig i przenieść migrację do wystąpienia zarządzanego przy użyciu w pełni zautomatyzowanego Azure Database Migration Service. Firma Contoso może w przyszłości ponownie wykorzystać tę usługę do migracji baz danych.
- Wystąpienie zarządzane SQL obsługuje program SQL Server Agent, co jest ważną kwestią w przypadku aplikacji SmartHotel360. Firma Contoso potrzebuje tej zgodności, ponieważ w przeciwnym razie będzie musiała ponownie zaprojektować plany konserwacji wymagane przez aplikację.
- Dzięki programowi Software Assurance firma Contoso może wymienić swoje istniejące licencje na obniżone stawki na wystąpienie zarządzane usługi SQL Database, używając korzyści użycia hybrydowego platformy Azure dla programu SQL Server. Dzięki temu firma Contoso może zaoszczędzić do 30% na wystąpieniu zarządzanym.
- Wystąpienie zarządzane SQL jest w pełni zawarte w sieci wirtualnej, dzięki czemu zapewnia większą izolację i bezpieczeństwo danych firmy Contoso. Firma Contoso może korzystać z zalet chmury publicznej, jednocześnie zapewniając izolację środowiska od publicznego Internetu.
- Wystąpienie zarządzane obsługuje wiele funkcji zabezpieczeń, w tym Always Encrypted, dynamiczne maskowanie danych, zabezpieczenia na poziomie wiersza i wykrywanie zagrożeń.

### <a name="solution-review"></a>Przegląd rozwiązania

Firma Contoso ocenia proponowany projekt, sporządzając listę zalet i wad.

<!-- markdownlint-disable MD033 -->

**Zagadnienie** | **Szczegóły**
--- | ---
**Zalety** | Maszyna wirtualna WEBVM zostanie przeniesiona na platformę Azure bez zmian, co oznacza prostą migrację.<br/><br/> Wystąpienie zarządzane SQL spełnia wymagania techniczne i cele firmy Contoso.<br/><br/> Wystąpienie zarządzane zapewni 100-procentową zgodność z bieżącym wdrożeniem przy jednoczesnym zaprzestaniu korzystania z programu SQL Server 2008 R2.<br/><br/> Firma może skorzystać z inwestycji w program Software Assurance i użyć korzyści użycia hybrydowego platformy Azure dla programu SQL Server i systemu Windows Server.<br/><br/> Może ponownie użyć usługi Azure Database Migration Service na potrzeby dodatkowych przyszłych migracji.<br/><br/> Wystąpienie zarządzane SQL ma wbudowaną odporność na uszkodzenia, której firma Contoso nie musi konfigurować. Gwarantuje to, że warstwa danych nie jest już pojedynczym punktem awarii.
**Wady** | Na maszynie wirtualnej WEBVM jest uruchomiony system Windows Server 2008 R2. Mimo iż ten system operacyjny jest obsługiwany przez platformę Azure, nie jest już obsługiwaną platformą. [Dowiedz się więcej](https://support.microsoft.com/help/956893).<br/><br/> Warstwa internetowa pozostaje pojedynczym punktem awarii, a usługi świadczy tylko maszyna wirtualna WEBVM.<br/><br/> Firma Contoso nadal będzie musiała obsługiwać warstwę internetową aplikacji jako maszynę wirtualną, zamiast przenieść ją do usługi zarządzanej, takiej jak Azure App Service.<br/><br/> W przypadku warstwy danych wystąpienie zarządzane może nie być najlepszym rozwiązaniem, jeśli firma Contoso chce dostosować system operacyjny lub serwer bazy danych lub jeśli chce uruchamiać aplikacje innych firm wraz z programem SQL Server. Uruchomienie programu SQL Server na maszynie wirtualnej IaaS może zapewnić taką elastyczność.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi migrację warstw internetowych i danych aplikacji SmartHotel360 na platformę Azure, wykonując następujące czynności:

1. Firma Contoso ma już swoją infrastrukturę platformy Azure, więc w tym scenariuszu wystarczy dodać kilka określonych składników platformy Azure.
2. Warstwa danych zostanie zmigrowana przy użyciu usługi Azure Database Migration Service. Ta usługa nawiązuje połączenie z lokalną maszyną wirtualną z programem SQL Server przy użyciu połączenia sieci VPN typu lokacja-lokacja między centrum danych firmy Contoso i platformą Azure. Następnie usługa migruje bazę danych.
3. Warstwa sieci Web zostanie zmigrowana przy użyciu podnośnika i migracji przesuniętej przy użyciu Site Recovery. Proces ten obejmuje przygotowanie lokalnego środowiska VMware, skonfigurowanie i włączenie replikacji oraz zmigrowanie maszyn wirtualnych przez przełączenie ich w tryb failover na platformie Azure.

     ![Architektura migracji](media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Usługi platformy Azure

NDES | Opis | Koszty
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Usługa Azure Database Migration Service umożliwia bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. | Dowiedz się więcej o [obsługiwanych regionach](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) i [cenniku usługi Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Wystąpienie zarządzane usługi Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Wystąpienie zarządzane to usługa zarządzanej bazy danych, która reprezentuje w pełni zarządzane wystąpienie programu SQL Server w chmurze platformy Azure. Używa tego samego kodu co najnowsza wersja aparatu bazy danych programu SQL Server oraz ma najnowsze funkcje, ulepszenia wydajności i poprawki zabezpieczeń. | Korzystanie z wystąpienia zarządzanego usługi SQL Database uruchomionego na platformie Azure powoduje naliczanie opłat zależnych od pojemności. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Usługa Site Recovery organizuje migrację i odzyskiwanie po awarii maszyn wirtualnych platformy Azure, lokalnych maszyn wirtualnych i serwerów fizycznych oraz zarządza tymi procesami. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure zostaną utworzone w momencie przejścia do trybu failover i wówczas będą naliczane opłaty. Dowiedz się więcej o [opłatach za usługę Site Recovery i cenach](https://azure.microsoft.com/pricing/details/site-recovery).

## <a name="prerequisites"></a>Wymagania wstępne

Firma Contoso i inni użytkownicy muszą spełniać następujące wymagania wstępne dotyczące tego scenariusza:

<!-- markdownlint-disable MD033 -->

Wymagania | Szczegóły
--- | ---
**Subskrypcja platformy Azure** | Subskrypcję należy utworzyć jeszcze przed przeprowadzeniem oceny w pierwszym artykule w tej serii. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zobacz [Zarządzanie dostępem do usługi Site Recovery przy użyciu kontroli dostępu opartej na rolach](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Infrastruktura platformy Azure wymagana do migracji](./contoso-migration-infrastructure.md).
**Usługa Site Recovery (lokalna)** | Lokalne wystąpienie programu vCenter Server w wersji 5.5, 6.0 lub 6.5<br/><br/> Host ESXi w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.<br/><br/> Maszyny wirtualne muszą spełniać [wymagania platformy Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Obsługiwana konfiguracja [sieci](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) i [magazynu](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage).
**Usługa Database Migration Service** | W przypadku usługi Azure Database Migration Service potrzebne jest [zgodne lokalne urządzenie sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Musisz mieć możliwość skonfigurowania lokalnego urządzenia sieci VPN. Musi ono mieć widoczny zewnętrznie publiczny adres IPv4. Adres nie może znajdować się za urządzeniem NAT.<br/><br/> Upewnij się, że masz dostęp do lokalnej bazy danych programu SQL Server.<br/><br/> Zapora systemu Windows powinna mieć dostęp do aparatu źródłowej bazy danych. Dowiedz się, jak [skonfigurować zaporę systemu Windows pod kątem dostępu do aparatu bazy danych](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).<br/><br/> Jeśli przed maszyną bazy danych znajduje się zapora, dodaj reguły zezwalające na dostęp do bazy danych za pośrednictwem portu SMB 445.<br/><br/> Poświadczenia, które służą do nawiązywania połączenia ze źródłowym wystąpieniem programu SQL Server i których elementem docelowym jest wystąpienie zarządzane, muszą być elementami członkowskimi roli serwera sysadmin.<br/><br/> Musisz mieć udział sieciowy w lokalnej bazie danych umożliwiający wykonanie kopii zapasowej źródłowej bazy danych za pomocą usługi Azure Database Migration Service.<br/><br/> Upewnij się, że konto usługi, na którym uruchomiono źródłowe wystąpienie programu SQL Server, ma uprawnienia do zapisu w udziale sieciowym.<br/><br/> Zanotuj nazwę i hasło użytkownika systemu Windows, który ma uprawnienia do pełnej kontroli nad udziałem sieciowym. Usługa Azure Database Migration Service personifikuje te poświadczenia użytkownika w celu przekazania plików kopii zapasowej do kontenera usługi Azure Storage.<br/><br/> Proces instalacji programu SQL Server Express domyślnie zmienia ustawienie protokołu TCP/IP na wartość **Wyłączony**. Upewnij się, że ustawienie to jest włączone.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Oto jak firma Contoso planuje skonfigurować wdrożenie:

> [!div class="checklist"]
>
> - **Krok 1. Konfigurowanie SQL Database wystąpienia zarządzanego.** Firma Contoso potrzebuje istniejącego wystąpienia zarządzanego, do którego zostanie zmigrowana lokalna baza danych programu SQL Server.
> - **Krok 2: przygotowanie Azure Database Migration Service.** Firma Contoso musi zarejestrować dostawcę migracji bazy danych, utworzyć wystąpienie, a następnie utworzyć projekt usługi Azure Database Migration Service. Firma Contoso musi również skonfigurować identyfikator URI sygnatury dostępu współdzielonego (SAS) dla usługi Azure Database Migration Service. Identyfikator URI sygnatury dostępu współdzielonego zapewnia delegowany dostęp do zasobów na koncie magazynu firmy Contoso, dzięki czemu firma Contoso może przyznać ograniczone uprawnienia do obiektów magazynu. Firma Contoso konfiguruje identyfikator URI sygnatury dostępu współdzielonego, aby usługa Azure Database Migration Service mogła uzyskać dostęp do kontenera konta magazynu, do którego przekaże pliki kopii zapasowej programu SQL Server.
> - **Krok 3: przygotowanie platformy Azure dla Site Recovery.** Firma Contoso musi utworzyć konto magazynu do przechowywania replikowanych danych dla usługi Site Recovery. Musi również utworzyć magazyn usług Azure Recovery Services.
> - **Krok 4: Przygotowanie lokalnego programu VMware do Site Recovery.** Firma Contoso przygotuje konta do użycia na potrzeby odnajdowania maszyn wirtualnych i instalacji agenta w celu nawiązania połączenia z maszynami wirtualnymi platformy Azure po przejściu do trybu failover.
> - **Krok 5. replikowanie maszyn wirtualnych.** Aby skonfigurować replikację, firma Contoso skonfiguruje źródłowe i docelowe środowiska usługi Site Recovery, skonfiguruje zasady replikacji i uruchomi replikację maszyn wirtualnych do usługi Azure Storage.
> - **Krok 6. Migrowanie bazy danych przy użyciu Azure Database Migration Service.** Firma Contoso zmigruje bazę danych.
> - **Krok 7. Migrowanie maszyn wirtualnych przy użyciu Site Recovery.** Firma Contoso wykona testowe przełączenie w tryb failover, aby upewnić się, że wszystko działa. Następnie firma Contoso wykona pełne przełączenie w tryb failover, aby zmigrować maszyny wirtualne na platformę Azure.

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
    - **SQLMI-DS-EUS2** (10.235.0.0.25)
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Ta podsieć służy do dołączania katalogu do wystąpienia zarządzanego.

      ![Wystąpienie zarządzane — tworzenie sieci wirtualnej](media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Po wdrożeniu sieci wirtualnej i podsieci sieci są one łączone równorzędnie w następujący sposób:

    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-HUB-EUS2** (sieć wirtualna koncentratora dla regionu Wschodnie stany USA 2),
    - sieć **VNET-SQLMI-EUS2** z siecią **VNET-PROD-EUS2** (sieć produkcyjna).

      ![Komunikacja równorzędna sieci](media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Określają niestandardowe ustawienia DNS. Serwer DNS wskazuje najpierw kontrolery domeny platformy Azure firmy Contoso. Serwer DNS platformy Azure jest pomocniczy. Kontrolery domeny platformy Azure firmy Contoso znajdują się w następujących lokalizacjach:

    - w podsieci **PROD-DC-EUS2**, w sieci produkcyjnej regionu Wschodnie stany USA 2 (**VNET-PROD-EUS2**)
    - Adres **CONTOSODC3** : 10.245.42.4
    - Adres **CONTOSODC4** : 10.245.42.5
    - Azure DNS resolver: 168.63.129.16

      ![Serwery DNS sieci](media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**Potrzebujesz dodatkowej pomocy?**

- Zapoznaj się z omówieniem [wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Dowiedz się, jak [utworzyć sieć wirtualną dla wystąpienia zarządzanego usługi SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Dowiedz się, jak [skonfigurować komunikację równorzędną](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Dowiedz się, jak [zaktualizować ustawienia DNS usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started-dns).

### <a name="set-up-routing"></a>Konfigurowanie routingu

Wystąpienie zarządzane jest umieszczane w prywatnej sieci wirtualnej. Firma Contoso potrzebuje tabeli tras, aby jej sieć wirtualna mogła komunikować się z usługą zarządzania platformy Azure. Jeśli sieć wirtualna nie może komunikować się z usługą, która nią zarządza, ta sieć wirtualna staje się niedostępna.

Firma Contoso bierze pod uwagę następujące czynniki:

- Tabela tras zawiera zestaw reguł (tras), które określają sposób, w jaki pakiety wysyłane z wystąpienia zarządzanego powinny być kierowane w sieci wirtualnej.
- Tabela tras jest skojarzona z podsieciami, w których są wdrażane wystąpienia zarządzane. Każdy pakiet, który opuszcza podsieć, jest obsługiwany na podstawie skojarzonej tabeli tras.
- Podsieć może być skojarzona tylko z jedną tabelą tras.
- Nie ma dodatkowych opłat za tworzenie tabel tras na platformie Microsoft Azure.

 Aby skonfigurować routing, administratorzy firmy Contoso wykonują następujące czynności:

1. Tworzą zdefiniowaną przez użytkownika tabelę tras w grupie zasobów **ContosoNetworkingRG**.

    ![Tabela tras](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Aby zachować zgodność z wymaganiami wystąpienia zarządzanego, po wdrożeniu tabeli tras(**MIRouteTable**) dodają trasę z prefiksem adresu 0.0.0.0/0. Opcja **Typ następnego przeskoku** jest ustawiana na wartość **Internet**.

    ![Prefiks tabeli tras](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Kojarzą tabelę tras z podsiecią **SQLMI-DB-EUS2** (w sieci **VNET-SQLMI-EUS2**).

    ![Podsieć tabeli tras](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [skonfigurować trasy dla wystąpienia zarządzanego](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

### <a name="create-a-managed-instance"></a>Tworzenie wystąpienia zarządzanego

Teraz administratorzy firmy Contoso mogą zaaprowizować wystąpienie zarządzane usługi SQL Database:

1. Ponieważ wystąpienie zarządzane obsługuje aplikację biznesową, administratorzy wdrażają je w regionie podstawowym firmy Wschodnie stany USA 2. Dodają wystąpienie zarządzane do grupy zasobów **ContosoRG**.
2. Wybierają warstwę cenową, rozmiar obliczeniowy i magazyn dla wystąpienia. Dowiedz się więcej o [cenach wystąpienia zarządzanego](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Wystąpienie zarządzane](media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Po wdrożeniu wystąpienia zarządzanego w grupie zasobów **ContosoRG** pojawiają się dwa nowe zasoby:

    - klaster wirtualny na wypadek, gdyby firma Contoso miała wiele wystąpień zarządzanych,
    - wystąpienie zarządzane bazy danych programu SQL Server.

      ![Wystąpienie zarządzane](media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [zaaprowizować wystąpienie zarządzane](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Krok 2. Przygotowywanie Azure Database Migration Service

Aby przygotować usługę Azure Database Migration Service, administratorzy firmy Contoso muszą wykonać kilka czynności:

- Zarejestrować dostawcę usługi Azure Database Migration Service na platformie Azure.
- Umożliwić usłudze Azure Database Migration Service dostęp do usługi Azure Storage na potrzeby przekazywania plików kopii zapasowej używanych do migrowania bazy danych. Aby zapewnić dostęp do usługi Azure Storage, tworzą kontener usługi Azure Blob Storage. Generują identyfikator URI sygnatury dostępu współdzielonego dla kontenera usługi Blob Storage.
- Utworzyć projekt usługi Azure Database Migration Service.

Następnie wykonują następujące czynności:

1. Rejestrują dostawcę migracji bazy danych w ramach jego subskrypcji.
    ![Database Migration Service — rejestracja](media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. Tworzą kontener usługi Blob Storage. Firma Contoso generuje identyfikator URI sygnatury dostępu współdzielonego, aby usługa Azure Database Migration Service mogła uzyskać do niego dostęp.

    ![Database Migration Service — generowanie identyfikatora URI sygnatury dostępu współdzielonego](media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. Tworzą wystąpienia usługi Azure Database Migration Service.

    ![Database Migration Service — tworzenie wystąpienia](media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. Umieszczają wystąpienie usługi Azure Database Migration Service w podsieci **PROD-DC-EUS2** sieci wirtualnej **VNET-PROD-DC-EUS2**.
    - Usługa Azure Database Migration Service jest umieszczana w tym miejscu, ponieważ usługa musi znajdować się w sieci wirtualnej, która może uzyskać dostęp do lokalnej maszyny wirtualnej z programem SQL Server za pośrednictwem bramy sieci VPN.
    - Sieć wirtualna **VNET-PROD-EUS2** ma komunikuje się równorzędnie z siecią wirtualną **VNET-HUB-EUS2** i może korzystać z bram zdalnych. Opcja **Użyj zdalnych bram** zapewnia, że usługa Azure Database Migration Service może komunikować się zgodnie z potrzebami.

        ![Database Migration Service — konfigurowanie sieci](media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**Potrzebujesz dodatkowej pomocy?**

- Dowiedz się, jak [skonfigurować usługę Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal).
- Dowiedz się, jak [utworzyć sygnaturę dostępu współdzielonego i jej używać](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-site-recovery-service"></a>Krok 3. Przygotowywanie platformy Azure dla usługi Site Recovery

Potrzebnych jest kilka elementów platformy Azure, aby firma Contoso mogła skonfigurować usługę Site Recovery pod kątem migracji maszyny wirtualnej warstwy internetowej (**WEBVM**):

- Sieć wirtualna, w której będą znajdować się zasoby w trybie failover.
- Konto magazynu do przechowywania replikowanych danych.
- Magazyn usługi Recovery Services na platformie Azure.

Administratorzy firmy Contoso konfigurują usługę Site Recovery w następujący sposób:

1. Ponieważ maszyna wirtualna jest frontonem internetowym dla aplikacji SmartHotel360, firma Contoso przełącza maszynę wirtualną w tryb failover do istniejącej sieci produkcyjnej (**VNET-PROD-EUS2**) i podsieci (**PROD-FE-EUS2**). Sieć i podsieć znajdują się w regionie podstawowym Wschodnie stany USA 2. Firma Contoso skonfigurowała sieć podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md).
2. Tworzą konto magazynu (**contosovmsacc20180528**). Firma Contoso używa konta ogólnego przeznaczenia. Firma Contoso wybiera magazyny w warstwie Standardowa i lokalnie nadmiarową replikację magazynu.

    ![Site Recovery — tworzenie konta magazynu](media/contoso-migration-rehost-vm-sql-managed-instance/asr-storage.png)

3. Gdy sieć i konto magazynu są gotowe, tworzą magazyn (**ContosoMigrationVault**). Firma Contoso umieszcza magazyn w grupie zasobów **ContosoFailoverRG** w regionie podstawowym Wschodnie stany USA 2.

    ![Recovery Services — tworzenie magazynu](media/contoso-migration-rehost-vm-sql-managed-instance/asr-vault.png)

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [skonfigurować platformę Azure do wdrożenia usługi Site Recovery](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure).

## <a name="step-4-prepare-on-premises-vmware-for-site-recovery"></a>Krok 4. Przygotowanie lokalnego programu VMware do Site Recovery

Aby przygotować oprogramowanie VMware do korzystania z usługi Site Recovery, administratorzy firmy Contoso muszą wykonać następujące zadania:

- Przygotować konto w wystąpieniu programu vCenter lub na hoście vSphere ESXi. Konto automatyzuje odnajdywanie maszyn wirtualnych.
- Przygotować konto umożliwiające automatyczną instalację usługi Mobility Service na maszynach wirtualnych VMware, które firma Contoso chce replikować.
- Przygotować lokalne maszyny wirtualne do nawiązania połączenia z maszynami wirtualnymi platformy Azure utworzonymi po przełączeniu w tryb failover.

### <a name="prepare-an-account-for-automatic-discovery"></a>Przygotowywanie konta do automatycznego odnajdowania

Usługa Site Recovery musi mieć dostęp do serwerów VMware w następujących celach:

- Automatyczne odnajdywanie maszyn wirtualnych. Wymagane jest co najmniej konto tylko do odczytu.
- Organizowanie replikacji, trybu failover i powrotu po awarii. Firma Contoso potrzebuje konta, na którym można uruchamiać operacje takie jak tworzenie i usuwanie dysków, a także włączanie maszyn wirtualnych.

Administratorzy firmy Contoso konfigurują konto, wykonując następujące zadania:

1. Utworzenie roli na poziomie programu vCenter.
2. Przypisanie wymaganych uprawnień do tej roli.

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [utworzyć i przypisać rolę na potrzeby automatycznego odnajdywania](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery).

### <a name="prepare-an-account-for-mobility-service-installation"></a>Przygotowanie konta do instalacji usługi Mobility Service

Usługa Mobility Service musi być zainstalowana na maszynie wirtualnej, którą firma Contoso chce zreplikować. Firma Contoso bierze pod uwagę następujące czynniki dotyczące usługi Mobility Service:

- Usługa Site Recovery może przeprowadzić automatyczną instalację wypychaną tego składnika, gdy firma Contoso włączy replikację dla maszyny wirtualnej.
- W przypadku automatycznej instalacji wypychanej firma Contoso musi przygotować konto, za pomocą którego usługa Site Recovery uzyska dostęp do maszyny wirtualnej.
- To konto określa się podczas konfigurowania replikacji w konsoli platformy Azure.
- Firma Contoso musi przygotować domenę lub konto lokalne z uprawnieniami do instalowania na maszynie wirtualnej.

**Potrzebujesz dodatkowej pomocy?**

Dowiedz się, jak [utworzyć konto na potrzeby instalacji wypychanej usługi Mobility Service](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation).

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po przejściu do trybu failover na platformie Azure firma Contoso chce nawiązać połączenie z replikowanymi maszynami wirtualnymi na platformie Azure. W tym celu Administratorzy firmy Contoso muszą wykonać kilka zadań na lokalnej maszynie wirtualnej przed migracją:

1. Aby uzyskać dostęp przez Internet, włączają protokół RDP na lokalnej maszynie wirtualnej przed przełączeniem do trybu failover. Upewniają się, że reguły TCP i UDP zostały dodane do profilu **publicznego** oraz że w pozycji **Zapora systemu Windows** > **Dozwolone aplikacje** zezwolono na użycie protokołu RDP we wszystkich profilach.
2. Aby uzyskać dostęp za pośrednictwem połączenia VPN typu lokacja-lokacja firmy Contoso, włączają protokół RDP na maszynie lokalnej. W pozycji **Zapora systemu Windows** > **Dozwolone aplikacje i funkcje** zezwalają na używanie protokołu RDP dla sieci typu **Domena i prywatne**.
3. Ustawiają zasady sieci SAN systemu operacyjnego na lokalnej maszynie wirtualnej na wartość **OnlineAll**.

Administratorzy firmy Contoso muszą także sprawdzić następujące elementy po uruchomieniu trybu failover:

- Podczas wyzwalania trybu failover na maszynie wirtualnej nie powinno być żadnych oczekujących aktualizacji systemu Windows. Jeśli system Windows będzie miał oczekujące aktualizacje, firma Contoso nie będzie mogła zalogować się na maszynie wirtualnej do momentu ukończenia aktualizacji.
- Po przejściu do trybu failover administratorzy powinni sprawdzić **diagnostykę rozruchu**, aby wyświetlić zrzut ekranu maszyny wirtualnej. Jeśli nie będą mogli wyświetlić diagnostyki rozruchu, powinni sprawdzić, czy maszyna wirtualna jest uruchomiona, a następnie zapoznać się ze [wskazówkami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="step-5-replicate-the-on-premises-vms-to-azure"></a>Krok 5. replikowanie lokalnych maszyn wirtualnych na platformę Azure

Przed uruchomieniem migracji na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację lokalnej maszyny wirtualnej.

### <a name="set-a-replication-goal"></a>Wybieranie celu replikacji

1. Po wybraniu nazwy magazynu (**ContosoVMVault**) ustawiają cel replikacji (**Wprowadzenie** > **Site Recovery** > **Przygotowanie infrastruktury**).
2. Administratorzy określają, że ich maszyny wirtualne znajdują się w środowisku lokalnym i że są to maszyny wirtualne VMware replikowane na platformie Azure.

    ![Przygotowanie infrastruktury — cel ochrony](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potwierdzanie planowania wdrożenia

Aby kontynuować, administratorzy firmy Contoso potwierdzają, że zakończyli planowanie wdrożenia. Wybierają pozycję **Tak, już to zostało zrobione**. W tym wdrożeniu firma Contoso migruje tylko pojedynczą maszynę wirtualną i dlatego planowanie wdrożenia nie jest konieczne.

### <a name="set-up-the-source-environment"></a>Konfigurowanie środowiska źródłowego

Teraz administratorzy firmy Contoso konfigurują środowisko źródłowe. Aby skonfigurować środowisko źródłowe, pobierają szablon OVF i za jego pomocą wdrażają serwer konfiguracji oraz skojarzone z nim składniki jako lokalną maszynę wirtualną VMware o wysokiej dostępności. Składniki na serwerze obejmują:

- Serwer konfiguracji służący do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure. Serwer konfiguracji zarządza replikacją danych.
- Serwer przetwarzania, który działa jako brama replikacji. Serwer przetwarzania:
  - odbiera dane replikacji,
  - optymalizuje dane replikacji przy użyciu pamięci podręcznej, kompresji i szyfrowania,
  - wysyła dane replikacji do usługi Azure Storage.
- Serwer przetwarzania instaluje także usługę Mobility Service na maszynach wirtualnych, które zostaną zreplikowane. Serwer przetwarzania wykonuje automatyczne odnajdowanie lokalnych maszyn wirtualnych VMware.
- Po utworzeniu i uruchomieniu maszyny wirtualnej serwera konfiguracji firma Contoso rejestruje serwer w magazynie.

Aby skonfigurować środowisko źródłowe, administratorzy firmy Contoso wykonują następujące czynności:

1. Pobierają szablon OVF z witryny Azure Portal (**Przygotowanie infrastruktury** > **Źródło** > **Serwer konfiguracji**).

    ![Dodawanie serwera konfiguracji](./media/contoso-migration-rehost-vm-sql-managed-instance/add-cs.png)

2. Importują szablon do programu VMware w celu utworzenia i wdrożenia maszyny wirtualnej.

    ![Wdrażanie szablonu OVF](./media/contoso-migration-rehost-vm-sql-managed-instance/vcenter-wizard.png)

3. Po pierwszym uruchomieniu maszyna wirtualna uruchamia środowisko instalacji systemu Windows Server 2016. Administratorzy akceptują umowę licencyjną i wprowadzają hasło administratora.
4. Po zakończeniu instalacji logują się na maszynie wirtualnej jako administrator. Po pierwszym zalogowaniu zostanie automatycznie uruchomione narzędzie do konfiguracji usługi Azure Site Recovery.
5. W narzędziu do konfiguracji usługi Site Recovery wprowadzają nazwę, która zostanie użyta do zarejestrowania serwera konfiguracji w magazynie.
6. Narzędzie sprawdza połączenie maszyny wirtualnej z platformą Azure. Po nawiązaniu połączenia wybierają pozycję **Zaloguj się**, aby zalogować się do subskrypcji platformy Azure. Użyte poświadczenia muszą zapewniać dostęp do magazynu, w którym jest zarejestrowany serwer konfiguracji.

    ![Rejestrowanie serwera konfiguracji](./media/contoso-migration-rehost-vm-sql-managed-instance/config-server-register2.png)

7. Narzędzie wykonuje pewne zadania konfiguracyjne, a następnie wywołuje ponowne uruchomienie. Ponownie logują się do maszyny. Zostanie automatycznie uruchomiony kreator zarządzania serwerem konfiguracji.
8. W kreatorze wybierają kartę sieciową, która będzie odbierała ruch związany z replikacją. Po skonfigurowaniu tego ustawienia nie można go zmienić.
9. Wybierają subskrypcję, grupę zasobów i magazyn usług Recovery Services do zarejestrowania serwera konfiguracji.

    ![Wybieranie magazynu usług Recovery Services](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz1.png)

10. Pobierają i instalują serwer MySQL oraz oprogramowanie VMware PowerCLI. Następnie weryfikują ustawienia serwera.
11. Po weryfikacji ustawień wprowadzają nazwę FQDN lub adres IP wystąpienia programu vCenter Server lub hosta vSphere. Pozostawiają port domyślny i wprowadzają nazwę wyświetlaną dla wystąpienia programu vCenter Server na platformie Azure.
12. Określają utworzone wcześniej konto, aby usługa Site Recovery mogła automatycznie wykryć maszyny wirtualne VMware dostępne do replikacji.
13. Wprowadzają poświadczenia, dzięki czemu usługa Mobility Service jest instalowana automatycznie po włączeniu replikacji. W przypadku maszyn z systemem Windows konto musi mieć uprawnienia administratora lokalnego na maszynach wirtualnych.

    ![Konfigurowanie programu vCenter Server](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz2.png)

14. Po zakończeniu rejestracji ponownie sprawdzają w witrynie Azure Portal, czy serwer konfiguracji i serwer VMware są widoczne na stronie **Źródło** w magazynie. Odnajdowanie może potrwać 15 minut lub dłużej.
15. Usługa Site Recovery nawiąże połączenie z serwerami VMware przy użyciu podanych ustawień i odnajdzie maszyny wirtualne.

### <a name="set-up-the-target"></a>Konfigurowanie środowiska docelowego

Teraz administratorzy firmy Contoso konfigurują środowisko docelowe replikacji:

1. W obszarze **Przygotowanie infrastruktury** > **Docelowa** określają ustawienia środowiska docelowego.
2. Usługa Site Recovery sprawdza, czy we wskazanym środowisku docelowym istnieje konto magazynu i sieć.

### <a name="create-a-replication-policy"></a>Tworzenie zasad replikacji

Po skonfigurowaniu środowiska źródłowego i docelowego administratorzy firmy Contoso tworzą zasady replikacji i kojarzą je z serwerem konfiguracji:

1. W obszarze **Przygotowywanie infrastruktury** > **Ustawienia replikacji** > **Zasady replikacji** >  **Utwórz i skojarz** tworzą zasady **ContosoMigrationPolicy**.
2. Korzystają z ustawień domyślnych:
    - **Próg punktu odzyskiwania:** Domyślnie 60 minut. Ta wartość określa częstość tworzenia punktów odzyskiwania. Przekroczenie tego limitu przez replikację ciągłą spowoduje wygenerowanie alertu.
    - **Przechowywanie punktów odzyskiwania:** Domyślnie 24 godziny. Ta wartość określa długość okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać do dowolnego punktu w tym oknie.
    - **Częstotliwość migawek spójnych na poziomie aplikacji:** Wartość domyślna to 1 godzina. Ta wartość określa częstotliwość tworzenia migawek spójnych na poziomie aplikacji.

    ![Zasady replikacji — tworzenie](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy.png)

3. Zasady zostaną automatycznie skojarzone z serwerem konfiguracji.

    ![Zasady replikacji — kojarzenie](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy2.png)

**Potrzebujesz dodatkowej pomocy?**

- Pełne instrukcje dotyczące tych kroków można znaleźć w artykule [Konfigurowanie odzyskiwania po awarii dla lokalnych maszyn wirtualnych VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Szczegółowe instrukcje pomogą Ci w [skonfigurowaniu środowiska źródłowego](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [wdrożeniu serwera konfiguracji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) i [skonfigurowaniu ustawień replikacji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).

### <a name="enable-replication"></a>Włączanie replikacji

Teraz administratorzy firmy Contoso mogą rozpocząć replikację maszyny wirtualnej WebVM.

1. W obszarze **Replikowanie aplikacji** > **Źródło** > **Replikuj** wybierają ustawienia środowiska źródłowego.
2. Określają, że chcą włączyć maszyny wirtualne, wybierają wystąpienie programu SQL Server i ustawiają serwer konfiguracji.

    ![Włączanie replikacji — środowisko źródłowe](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication1.png)

3. Określają ustawienia środowiska docelowego, w tym grupę zasobów i sieć, w której znajdzie się maszyna wirtualna po przełączeniu do trybu failover. Określają konto magazynu, w którym będą przechowywane zreplikowane dane.

    ![Włączanie replikacji — środowisko docelowe](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication2.png)

4. Wybierają maszynę wirtualną **WebVM** na potrzeby replikacji. Po włączeniu replikacji usługa Site Recovery instaluje usługę Mobility Service na każdej maszynie wirtualnej.

    ![Włączanie replikacji — wybieranie maszyny wirtualnej](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication3.png)

5. Sprawdzają, czy wybrano prawidłowe zasady replikacji, i włączają replikację dla maszyny wirtualnej **WEBVM**. Śledzą postęp replikacji w obszarze **Zadania**. Po uruchomieniu zadania **Sfinalizuj ochronę** maszyna jest gotowa do przejścia w tryb failover.

6. W obszarze **Podstawy** w witrynie Azure Portal mogą zobaczyć stan maszyn wirtualnych replikowanych na platformie Azure:

    ![Widok infrastruktury](./media/contoso-migration-rehost-vm-sql-managed-instance/essentials.png)

**Potrzebujesz dodatkowej pomocy?**

Pełne instrukcje do wszystkich kroków można znaleźć w artykule [Włączanie replikacji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-6-migrate-the-database"></a>Krok 6. Migrowanie bazy danych

Administratorzy firmy Contoso muszą utworzyć projekt usługi Azure Database Migration Service, a następnie przeprowadzić migrację bazy danych.

### <a name="create-an-azure-database-migration-service-project"></a>Tworzenie projektu usługi Azure Database Migration Service

1. Tworzą projekt usługi Azure Database Migration Service. Wybierają typ serwera źródłowego **SQL Server** i **wystąpienie zarządzane usługi Azure SQL Database** jako element docelowy.

     ![Database Migration Service — nowy projekt migracji](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Zostanie otwarty Kreator migracji.

### <a name="migrate-the-database"></a>migrowanie bazy danych

1. W Kreatorze migracji określają źródłową maszynę wirtualną, na której znajduje się lokalna baza danych. Wprowadzają poświadczenia w celu uzyskania dostępu do bazy danych.

    ![Database Migration Service — szczegóły środowiska źródłowego](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. Wybierają bazę danych do migracji (**SmartHotel.Registration**):

    ![Database Migration Service — wybieranie źródłowych baz danych](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-sourcedb.png)

3. Wprowadzają dla elementu docelowego nazwę wystąpienia zarządzanego na platformie Azure oraz poświadczenia dostępu.

    ![Database Migration Service — szczegóły środowiska docelowego](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. W obszarze **Nowe działanie** > **Uruchom migrację** określają ustawienia dotyczące uruchamiania migracji:
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

## <a name="step-7-migrate-the-vm"></a>Krok 7. Migrowanie maszyny wirtualnej

Administratorzy firmy Contoso uruchamiają szybki test przejścia do trybu failover, a następnie przeprowadzają migrację maszyny wirtualnej.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Testowe przełączenie w tryb failover przed przeprowadzeniem migracji maszyny wirtualnej WEBVM pomaga upewnić się, że wszystko działa zgodnie z oczekiwaniami. Następnie administratorzy wykonują następujące czynności:

1. Uruchamiają próbę przejścia w tryb failover przy użyciu najnowszego dostępnego punktu w czasie (**Najnowszy przetworzony**).
2. Wybierają pozycję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**. Gdy ta opcja zostanie wybrana, usługa Site Recovery spróbuje zamknąć źródłową maszynę wirtualną przed wyzwoleniem trybu failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się.
3. Próbne przełączenia do trybu failover: a. Uruchamiane jest sprawdzanie wymagań wstępnych, aby upewnić się, że zostały spełnione wszystkie warunki migracji.
    b. Tryb failover przetwarza dane, aby umożliwić utworzenie maszyny wirtualnej platformy Azure. Jeśli zostanie wybrany najnowszy punkt odzyskiwania, punkt odzyskiwania zostanie utworzony na podstawie danych.
    c. Przy użyciu danych przetworzonych w poprzednim kroku utworzona zostaje maszyna wirtualna platformy Azure.
4. Po zakończeniu trybu failover w witrynie Azure Portal będzie widoczna replika maszyny wirtualnej platformy Azure. Sprawdzają, czy wszystko działa prawidłowo: maszyna wirtualna ma odpowiedni rozmiar, jest połączona z odpowiednią siecią i jest uruchomiona.
5. Po zweryfikowaniu testowego przełączenia w tryb failover przeprowadzają czyszczenie po przejściu do trybu failover oraz rejestrują wszelkie obserwacje.

### <a name="migrate-the-vm"></a>migrowanie maszyny wirtualnej

1. Jeśli próbne przejście do trybu failover przebiegło zgodnie z oczekiwaniami, administratorzy firmy Contoso mogą utworzyć plan odzyskiwania na potrzeby migracji i dodać maszynę wirtualną WEBVM do planu:

     ![Tworzenie planu odzyskiwania — wybieranie elementów](./media/contoso-migration-rehost-vm-sql-managed-instance/recovery-plan.png)

2. Uruchamiają tryb failover w ramach planu i wybierają najnowszy punkt odzyskiwania. Określają, że usługa Site Recovery powinna spróbować zamknąć lokalną maszynę wirtualną przed wyzwoleniem trybu failover.

    ![Praca awaryjna](./media/contoso-migration-rehost-vm-sql-managed-instance/failover1.png)

3. Po przejściu w tryb failover administratorzy sprawdzają, czy maszyna wirtualna platformy Azure jest widoczna zgodnie z oczekiwaniami w witrynie Azure Portal.

   ![Szczegóły planu odzyskiwania](./media/contoso-migration-rehost-vm-sql-managed-instance/failover2.png)

4. Po sprawdzeniu ukończą migrację, aby zakończyć proces migracji, zatrzymać replikację maszyny wirtualnej i zatrzymać naliczanie opłat za usługę Site Recovery dla maszyny wirtualnej.

    ![Tryb failover — ukończenie migracji](./media/contoso-migration-rehost-vm-sql-managed-instance/failover3.png)

### <a name="update-the-connection-string"></a>Aktualizowanie parametrów połączenia

W ostatnim kroku procesu migracji administratorzy firmy Contoso aktualizują parametry połączenia aplikacji tak, aby wskazywały zmigrowaną bazę danych działającą na wystąpieniu zarządzanym firmy Contoso.

1. Odnajdują parametry połączenia w witrynie Azure Portal, wybierając pozycję **Ustawienia** > **Parametry połączenia**.

    ![Parametry połączeń](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. Aktualizują parametry przy użyciu nazwy użytkownika i hasła wystąpienia zarządzanego usługi SQL Database.
3. Po skonfigurowaniu parametrów zastępują bieżące parametry połączenia w pliku web.config aplikacji.
4. Po zaktualizowaniu pliku i zapisaniu go ponownie uruchamiają usługi IIS na maszynie wirtualnej WEBVM za pomocą polecenia `IISRESET /RESTART` w oknie wiersza polecenia.
5. Po ponownym uruchomieniu usług IIS aplikacja korzysta z bazy danych uruchomionej w wystąpieniu zarządzanym usługi SQL Database.
6. W tym momencie można zamknąć lokalną maszynę SQLVM. Migracja została ukończona.

**Potrzebujesz dodatkowej pomocy?**

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

### <a name="bcdr"></a>BCDR

W celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR, Business Continuity and Disaster Recovery) firma Contoso podejmuje następujące działania:

- Zachowaj bezpieczeństwo danych: Firma Contoso tworzy kopie zapasowe danych na maszynach wirtualnych za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Przechowuj aplikacje i uruchamiaj je: contoso replikuje maszyny wirtualne aplikacji na platformie Azure do regionu pomocniczego za pomocą Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).
- Firma Contoso zdobywa więcej informacji o zarządzaniu wystąpieniem zarządzanym SQL, w tym o [tworzeniu kopii zapasowych bazy danych](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Firma Contoso ma już licencję na maszynę WEBVM. Aby skorzystać z cen wynikających z korzyści użycia hybrydowego platformy Azure, firma Contoso konwertuje istniejącą maszynę wirtualną platformy Azure.
- Firma Contoso włącza usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Cost Management to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia firmie Contoso korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. Dowiedz się więcej na temat usługi [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview).

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso przeprowadza ponowne hostowanie aplikacji SmartHotel360 na platformie Azure, migrując maszynę wirtualną frontonu aplikacji na platformę Azure za pomocą usługi Site Recovery. Firma Contoso przeprowadza migrację lokalnej bazy danych do wystąpienia zarządzanego usługi Azure SQL Database za pomocą usługi Azure Database Migration Service.
