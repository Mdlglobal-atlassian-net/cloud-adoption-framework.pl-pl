---
title: Ocenianie obciążeń lokalnych na potrzeby migracji na platformę Azure
description: Poznaj przykładowy przykład sposobu oceny aplikacji lokalnej do migracji na platformę Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 6fc2992f98c16171173a3313fe19411c05883fa2
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312105"
---
<!-- cSpell:ignore WEBVM SQLVM OSTICKETWEB OSTICKETMYSQL CONTOSODC contosohost vcenter prereqs ctypes ctypeslib smarthotelapp -->

# <a name="assess-on-premises-workloads-for-migration-to-azure"></a>Ocena obciążeń lokalnych pod kątem migracji do platformy Azure

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso ocenia proces migracji aplikacji lokalnej na platformę Azure. W przykładowym scenariuszu lokalna aplikacja SmartHotel360 firmy Contoso działa obecnie w oprogramowaniu VMware. Firma Contoso ocenia maszyny wirtualne aplikacji przy użyciu usługi Azure Migrate, a bazę danych programu SQL Server aplikacji przy użyciu narzędzia Data Migration Assistant.

## <a name="overview"></a>Omówienie

Ponieważ Contoso rozważa migrację na platformę Azure, firma musi przeprowadzić ocenę techniczną i finansową, aby określić, czy lokalne obciążenia są dobrym kandydatami do migracji do chmury. W szczególności zespół firmy Contoso chce ocenić zgodność maszyny i bazy danych na potrzeby migracji. Oszacowane powinny zostać wydajność i koszty działania zasobów firmy Contoso na platformie Azure.

Aby rozpocząć pracę i lepiej zrozumieć odpowiednie technologie, firma Contoso ocenia dwie ze swoich aplikacji lokalnych, które podsumowano w poniższej tabeli. Firma ocenia scenariusze migracji, w których następuje ponowne hostowanie i refaktoryzacja aplikacji na potrzeby migracji. Więcej informacji na temat ponownego hostowania i refaktoryzacji zawiera [przegląd przykładów migracji](../migrate/azure-best-practices/contoso-migration-overview.md).

<!-- markdownlint-disable MD033 -->

Nazwa aplikacji | Platforma | Warstwy aplikacji | Szczegóły
--- | --- | --- | ---
SmartHotel360<br/><br/> (zarządza wymaganiami firmy Contoso dotyczącymi podróży) | Działa w systemie Windows z bazą danych SQL Server | Aplikacja dwuwarstwowa. Frontonowa witryna internetowa ASP.NET działa na jednej maszynie wirtualnej (**WEBVM**), a program SQL Server działa na innej maszynie wirtualnej (**SQLVM**). | Maszyny wirtualne VMware działają na hoście ESXi zarządzanym przez program vCenter Server.<br/><br/> Przykładową aplikację można pobrać z witryny [GitHub](https://github.com/Microsoft/SmartHotel360).
osTicket<br/><br/> (aplikacja dla pomocy technicznej firmy Contoso) | Działa w systemie Linux/Apache z zainstalowanym środowiskiem MySQL PHP (LAMP) | Aplikacja dwuwarstwowa. Frontonowa witryna internetowa napisana w języku PHP działa na jednej maszynie wirtualnej (**OSTICKETWEB**), a baza danych MySQL działa na innej maszynie wirtualnej (**OSTICKETMYSQL**). | Aplikacja jest używana przez aplikacje obsługi klientów do śledzenia problemów dotyczących pracowników wewnętrznych i klientów zewnętrznych.<br/><br/> Przykład można pobrać z witryny [GitHub](https://github.com/osTicket/osTicket).

<!-- markdownlint-enable MD033 -->

## <a name="current-architecture"></a>Bieżąca architektura

Na tym diagramie przedstawiono bieżącą infrastrukturę lokalną firmy Contoso:

![Bieżąca architektura firmy Contoso](../migrate/azure-best-practices/media/contoso-migration-assessment/contoso-architecture.png)

- Firma Contoso ma jedno główne centrum danych. Centrum danych znajduje się w Nowym Jorku we wschodnich Stanach Zjednoczonych.
- Firma Contoso ma trzy dodatkowe oddziały lokalne na terenie Stanów Zjednoczonych.
- Główne centrum danych jest połączone z Internetem łączem światłowodowym Metro Ethernet (500 MB/s).
- Każdy oddział jest połączony lokalnie z Internetem przy użyciu połączeń klasy biznesowej z tunelami IPsec sieci VPN z głównym centrum danych. Taka konfiguracja zapewnia trwałe połączenie całej sieci firmy Contoso i optymalizację łączności z Internetem.
- Główne centrum danych jest w pełni zwirtualizowane przy użyciu oprogramowania VMware. Firma Contoso ma dwa hosty wirtualizacji ESXi 6.5, które są zarządzane za pomocą programu vCenter Server 6.5.
- Do zarządzania tożsamościami firma Contoso używa usługi Active Directory. Serwery DNS firmy Contoso działają w sieci wewnętrznej.
- Kontrolery domeny w centrum danych działają na maszynach wirtualnych VMware. Kontrolery domeny w lokalnych oddziałach działają na serwerach fizycznych.

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT firmy Contoso w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się. W związku z tym zwiększyło się obciążenie lokalnych systemów i infrastruktury firmy.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy dla swoich deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, a firma mogła dzięki temu szybciej obsługiwać swoich klientów.
- **Zwiększenie elastyczności.** Firma Contoso chce lepiej odpowiadać na zapotrzebowania w branży. Chce być w stanie szybciej reagować na zamiany zachodzące na rynku, aby odnosić sukcesy w gospodarce światowej. Firma Contoso nie chce utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę rozwoju firmy Contoso jej dział IT musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.

## <a name="assessment-goals"></a>Cele oceny

Zespół ds. chmury firmy Contoso zidentyfikował cele oceny migracji:

- Po migracji aplikacje na platformie Azure powinny mieć taką samą wydajność jak obecnie w lokalnym środowisku VMware firmy Contoso. Przeniesienie do chmury nie oznacza, że wydajność aplikacji jest mniej istotna.
- Firma Contoso musi sprawdzić zgodność swoich aplikacji i baz danych z wymaganiami dotyczącymi platformy Azure. Dla firmy Contoso ważne jest też zrozumienie opcji hostingu na platformie Azure.
- Po przeniesieniu aplikacji do chmury administrowanie bazami danych firmy Contoso powinno zostać zminimalizowane.
- Specjaliści z firmy Contoso chcą poznać nie tylko opcje migracji, ale również koszty związane z infrastrukturą, które będzie trzeba ponosić po przejściu do chmury.

## <a name="assessment-tools"></a>Narzędzia oceny

Do oceny migracji firma Contoso używa narzędzi firmy Microsoft. Narzędzia te są dopasowane do celów firmy i powinny dostarczyć firmie Contoso wszystkie niezbędne informacje.

Technologia | Opis | Koszty
--- | --- | ---
[Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | Firma Contoso używa narzędzia Data Migration Assistant do oceny i wykrywania problemów ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych na platformie Azure. Narzędzie Data Migration Assistant ocenia równoważność funkcji między źródłowymi i docelowymi elementami SQL. Wynikiem działania tego narzędzia są zalecenia dotyczące poprawy wydajności i niezawodności. | Narzędzie Data Migration Assistant można bezpłatnie pobrać.
[Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) | Firma Contoso używa usługi Azure Migrate do oceny swoich maszyn wirtualnych VMware. Usługa Azure Migrate ocenia przydatność maszyn do migracji. Dzięki tej usłudze można oszacować wymagany rozmiar i koszt działania na platformie Azure. | Od maja 2018 r. Azure Migrate jest usługą bezpłatną.
[Mapa usługi](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-service-map) | Usługa Azure Migrate za pomocą rozwiązania Service Map przedstawia zależności między maszynami, które firma chce zmigrować. | Rozwiązanie Service Map jest częścią dzienników usługi Azure Monitor. Obecnie firma Contoso może używać rozwiązania Service Map przez 180 dni bez naliczania opłat.

W tym scenariuszu przedstawiciel firmy Contoso pobiera i uruchamia narzędzie Data Migration Assistant w celu oceny lokalnej bazy danych SQL Server pod kątem przydatności dla swojej aplikacji do obsługi podróży. Za pomocą usługi Azure Migrate z mapowaniem zależności firma Contoso ocenia maszyny wirtualne aplikacji przed ich zmigrowaniem na platformę Azure.

## <a name="assessment-architecture"></a>Architektura do oceny

![architekturę do oceny migracji](../migrate/azure-best-practices/media/contoso-migration-assessment/migration-assessment-architecture.png)

- Contoso to fikcyjna nazwa reprezentująca typowe przedsiębiorstwo.
- Firma Contoso ma lokalne centrum danych (**contoso-datacenter**) i lokalne kontrolery domeny (**CONTOSODC1** oraz **CONTOSODC2**).
- Maszyny wirtualne VMware znajdują się na hostach VMware ESXi w wersji 6.5 (**contosohost1**, **contosohost2**).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com** uruchomiony na maszynie wirtualnej).
- Aplikacja do obsługi podróży SmartHotel360 ma następujące cechy:
  - Aplikacja korzysta z dwóch maszyn wirtualnych VMware (**WEBVM** i **SQLVM**).
  - Obie maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com**.
  - Na maszynach wirtualnych jest uruchomiony system Windows Server 2008 R2 Datacenter z dodatkiem SP1.
- Środowisko VMware jest zarządzane przez program vCenter Server (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Aplikacja osTicket dla pomocy technicznej:
  - Ta aplikacja działa na dwóch maszynach wirtualnych (**OSTICKETWEB** i **OSTICKETMYSQL**).
  - Na maszynach wirtualnych jest uruchomiony system Ubuntu Linux Server 16.04-LTS.
  - Na maszynie wirtualnej **OSTICKETWEB** działa oprogramowanie Apache 2 i PHP 7.0.
  - Na maszynie wirtualnej **OSTICKETMYSQL** działa program MySQL 5.7.22.

## <a name="prerequisites"></a>Wymagania wstępne

Firma Contoso i inni użytkownicy muszą spełniać następujące wymagania wstępne dotyczące oceny:

- Uprawnienia właściciela lub współautora dla subskrypcji platformy Azure lub grupy zasobów w subskrypcji platformy Azure.
- Lokalne wystąpienie programu vCenter Server w wersji 6.5, 6.0 lub 5.5.
- Konto tylko do odczytu w programie vCenter Server lub uprawnienia do utworzenia takiego konta.
- Uprawnienia do utworzenia maszyny wirtualnej w wystąpieniu programu vCenter Server przy użyciu szablonu OVA.
- Co najmniej jeden host ESXi w wersji 5.5 lub nowszej.
- Co najmniej dwie lokalne maszyny wirtualne VMware, w tym jedna z uruchomioną bazą danych programu SQL Server.
- Uprawnienia do zainstalowania agentów usługi Azure Migrate na każdej maszynie wirtualnej.
- Maszyny wirtualne powinny mieć bezpośrednie połączenie z Internetem.
  - Możesz ograniczyć dostęp do Internetu do [wymaganych adresów URL](https://docs.microsoft.com/azure/migrate/concepts-collector).
  - Jeśli maszyny wirtualne nie mają łączności z Internetem, należy zainstalować na nich [bramę usługi Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/gateway) i przekierować przez nią ruch agentów.
- W pełni kwalifikowana nazwa domeny (FQDN) maszyny wirtualnej, na której działa wystąpienie SQL Server, na potrzeby oceny bazy danych.
- Zapora systemu Windows uruchomiona na maszynie wirtualnej programu SQL Server powinna zezwalać na połączenia zewnętrzne na porcie TCP 1433 (domyślnym). Taka konfiguracja umożliwia narzędziu Data Migration Assistant nawiązanie połączenia.

## <a name="assessment-overview"></a>Przegląd oceny

Firma Contoso przeprowadza ocenę w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Pobieranie i Instalowanie Data Migration Assistant.** Przedstawiciel firmy Contoso przygotowuje narzędzie Data Migration Assistant do oceny lokalnej bazy danych SQL Server.
> - **Krok 2. Ocena bazy danych przy użyciu Data Migration Assistant.** Przedstawiciel firmy Contoso uruchamia ocenę bazy danych i analizuje ją.
> - **Krok 3: przygotowanie do oceny maszyny wirtualnej przy użyciu Azure Migrate.** Przedstawiciel firmy Contoso konfiguruje konta lokalne i dostosowuje ustawienia programu VMware.
> - **Krok 4. odnajdywanie lokalnych maszyn wirtualnych przy użyciu Azure Migrate.** Przedstawiciel firmy Contoso tworzy maszynę wirtualną modułu zbierającego usługi Azure Migrate. Następnie przedstawiciel firmy Contoso uruchamia moduł zbierający w celu odnalezienia maszyn wirtualnych do oceny.
> - **Krok 5. Przygotowanie do analizy zależności przy użyciu Azure Migrate.** Przedstawiciel firmy Contoso instaluje agentów usługi Azure Migrate na maszynach wirtualnych, dzięki czemu można zobaczyć mapowanie zależności między maszynami wirtualnymi.
> - **Krok 6. Ocena maszyn wirtualnych przy użyciu Azure Migrate.** Przedstawiciel firmy Contoso sprawdza zależności, grupuje maszyny wirtualne i uruchamia ocenę. Gdy ocena jest gotowa, przedstawiciel firmy Contoso analizuje ją pod kątem przygotowania do migracji.

    > [!NOTE]
    > Assessments shouldn't just be limited to using tooling to discover information about your environment, you should schedule in time to speak to business owners, end users, other members within the IT department, etc in order to get a full picture of what is happening within the environment and understand things tooling cannot tell you. 

## <a name="step-1-download-and-install-data-migration-assistant"></a>Krok 1. Pobieranie i Instalowanie Data Migration Assistant

1. Przedstawiciel firmy Contoso pobiera narzędzie Data Migration Assistant z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=53595).
    - Narzędzie Data Migration Assistant można zainstalować na dowolnym komputerze, który może połączyć się z wystąpieniem programu SQL Server. Nie trzeba go uruchamiać na maszynie programu SQL Server.
    - Narzędzia Data Migration Assistant nie należy uruchamiać na komputerze hostującym program SQL Server.
2. Przedstawiciel firmy Contoso uruchamia pobrany plik instalatora (DownloadMigrationAssistant.msi), aby rozpocząć instalację.
3. Na stronie **Finish** (Zakończenie) przedstawiciel firmy Contoso wybiera pozycję **Launch Microsoft Data Migration Assistant** (Uruchom narzędzie Microsoft Data Migration Assistant) przed zakończeniem pracy kreatora.

## <a name="step-2-run-and-analyze-the-database-assessment-for-smarthotel360"></a>Krok 2. Uruchamianie i analizowanie oceny bazy danych dla SmartHotel360

Teraz firma Contoso może przeprowadzić ocenę lokalnej bazy danych SQL Server pod kątem aplikacji SmartHotel360.

1. Z poziomu narzędzia Data Migration Assistant przedstawiciel firmy Contoso wybiera pozycję **New** (Nowy) > **Assessment** (Ocena), a następnie nadaje ocenie nazwę taką samą jak nazwa projektu.
2. W obszarze **Source server type**, (Typ serwera źródłowego) przedstawiciel firmy Contoso wybiera pozycję **SQL Server**, a w obszarze **Target Server type** (Typ serwera docelowego) pozycję **SQL Server on Azure Virtual Machines** (Program SQL Server w usłudze Azure Virtual Machines)

    ![Data Migration Assistant — wybór źródła](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-1.png)

    > [!NOTE]
    > Obecnie narzędzie Data Migration Assistant nie obsługuje przeprowadzania oceny migracji do wystąpienia zarządzanego usługi Azure SQL Database. Aby obejść ten problem, firma Contoso używa programu SQL Server na maszynie wirtualnej platformy Azure jako tymczasowego obiektu docelowego dla oceny.

3. W obszarze **Select Target Version**, (Wybierz wersję docelową) przedstawiciel firmy Contoso wybiera program SQL Server 2017 jako wersję docelową. Firma Contoso musi wybrać tę wersję, ponieważ jest to wersja używana przez wystąpienie zarządzane usługi SQL Database.
4. Przedstawiciel firmy Contoso wybiera raporty, które ułatwiają odnajdywanie informacji dotyczących zgodności i nowych funkcji:
    - Raport **Compatibility issues** (Problemy ze zgodnością) informuje o zmianach, które mogą uniemożliwić migrację lub które wymagają drobnych korekt przed migracją. Ten raport zawiera przydatne dla firmy Contoso informacje o wszelkich obecnie używanych funkcjach, które są przestarzałe. Problemy są uporządkowane według poziomu zgodności.
    - Raport **New feature recommendation** (Zalecenia dotyczące nowych funkcji) informuje o nowych funkcjach docelowej platformy programu SQL Server, które można wykorzystać w bazie danych po zakończeniu migracji. Zalecenia dotyczące nowych funkcji są zorganizowane pod nagłówkami **Performance** (Wydajność), **Security** (Zabezpieczenia) i **Storage** (Magazyn).

    ![Data Migration Assistant — problemy ze zgodnością i nowe funkcje](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-2.png)

5. W oknie **Connect to a server** (Nawiązywanie połączenia z serwerem) przedstawiciel firmy Contoso wprowadza nazwę maszyny wirtualnej, na której uruchomiono bazę danych, i poświadczenia umożliwiające uzyskanie do niej dostępu. Przedstawiciel firmy Contoso wybiera pozycję **Trust server certificate** (Certyfikat serwera zaufania), aby upewnić się, że maszyna wirtualna może uzyskać dostęp do programu SQL Server. Następnie przedstawiciel firmy Contoso wybiera pozycję **Connect** (Połącz).

    ![Data Migration Assistant — nawiązywanie połączenia z serwerem](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-3.png)

6. W obszarze **Add source** (Dodaj źródło) przedstawiciel firmy Contoso dodaje bazę danych, która ma zostać oceniona, a następnie wybiera pozycję **Next** (Dalej), aby rozpocząć ocenę.
7. Tworzona jest ocena.

    ![Data Migration Assistant — tworzenie oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-4.png)

8. W obszarze **Review results** (Przegląd wyników) przedstawiciel firmy Contoso przegląda wyniki oceny.

### <a name="analyze-the-database-assessment"></a>Analizowanie oceny bazy danych

Wyniki są wyświetlane zaraz po ich udostępnieniu. Po rozwiązaniu problemów przedstawiciel firmy Contoso musi wybrać pozycję **Restart assessment** (Uruchom ocenę ponownie), aby ponownie uruchomić ocenę.

1. W raporcie **Compatibility issues** (Problemy ze zgodnością) przedstawiciel firmy Contoso sprawdza wszelkie problemy na każdym poziomie zgodności. Poziomy zgodności są mapowane na wersje programu SQL Server w następujący sposób:

    - 100: SQL Server 2008/Azure SQL Database
    - 110: SQL Server 2012/Azure SQL Database
    - 120: SQL Server 2014/Azure SQL Database
    - 130: SQL Server 2016/Azure SQL Database
    - 140: SQL Server 2017/Azure SQL Database

    ![Data Migration Assistant — raport dotyczący problemów ze zgodnością](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-5.png)

2. W raporcie **Feature recommendations** (Zalecenia dotyczące funkcji) przedstawiciel firmy Contoso sprawdza, jakie funkcje wydajności, zabezpieczeń i magazynu są zalecane po przeprowadzeniu migracji. Zalecenia obejmują różne funkcje, w tym przetwarzanie OLTP danych w pamięci i indeksy magazynu kolumn, dynamiczne maskowanie danych, Stretch Database, Always Encrypted i Transparent Data Encryption.

    ![Data Migration Assistant — raport z zaleceniami dotyczącymi funkcji](../migrate/azure-best-practices/media/contoso-migration-assessment/dma-assessment-6.png)

    > [!NOTE]
    > Przedstawiciel firmy Contoso powinien [włączyć funkcję Transparent Data Encryption](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption?view=sql-server-2017) dla wszystkich baz danych SQL Server. Jest to szczególnie istotne, gdy baza danych znajduje się w chmurze, zamiast być hostowana w środowisku lokalnym. Funkcję Transparent Data Encryption należy włączyć dopiero po migracji. Jeśli ta funkcja jest już włączona, przedstawiciel firmy Contoso musi przenieść certyfikat lub klucz asymetryczny do głównej bazy danych na serwerze docelowym. Dowiedz się, jak [przenieść bazę danych chronioną przez funkcję Transparent Data Encryption do innego wystąpienia programu SQL Server](https://docs.microsoft.com/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017).

3. Przedstawiciel firmy Contoso może wyeksportować ocenę w formacie JSON lub CSV.

> [!NOTE]
> W przypadku ocen na dużą skalę:
>
> - Uruchom wiele ocen jednocześnie i wyświetl ich stany na stronie **All assessments** (Wszystkie oceny).
> - Skonsoliduj oceny w [bazie danych programu SQL Server](https://docs.microsoft.com/sql/dma/dma-consolidatereports?view=ssdt-18vs2017).
> - Skonsoliduj oceny w [raporcie usługi Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport?view=ssdt-18vs2017).

## <a name="step-3-prepare-for-vm-assessment-by-using-azure-migrate"></a>Krok 3. Przygotowanie do oceny maszyn wirtualnych za pomocą Azure Migrate

Przedstawiciel firmy Contoso musi utworzyć konto VMware, którego usługa Azure Migrate będzie mogła użyć do automatycznego odnajdywania maszyn wirtualnych na potrzeby oceny. Należy sprawdzić uprawnienia do tworzenia maszyny wirtualnej, ustawić poziom statystyk i zwrócić uwagę na porty, które muszą być otwarte.

### <a name="set-up-a-vmware-account"></a>Konfigurowanie konta VMware

Funkcja odnajdywania maszyn wirtualnych wymaga konta tylko do odczytu w programie vCenter Server z następującymi właściwościami:

- **Typ użytkownika:** Co najmniej użytkownik tylko do odczytu.
- **Uprawnienia:** W przypadku obiektu centrum danych zaznacz pole wyboru **Propaguj do obiektów podrzędnych** . W obszarze **Role** (Rola) wybierz pozycję **Read-only** (Tylko do odczytu).
- **Szczegóły:** Użytkownik jest przypisany na poziomie centrum danych z dostępem do wszystkich obiektów w centrum danych.
- Aby ograniczyć dostęp, przypisz rolę **Brak dostępu** z obiektem **Propaguj do obiektu podrzędnego** do obiektów podrzędnych (hostów vSphere, magazynów danych, maszyn wirtualnych i sieci).

### <a name="verify-permissions-to-create-a-vm"></a>Weryfikowanie uprawnień do utworzenia maszyny wirtualnej

Przedstawiciel firmy Contoso weryfikuje, czy ma uprawnienia do tworzenia maszyny wirtualnej, przez zaimportowanie pliku w formacie OVA. Dowiedz się, jak [utworzyć i przypisać rolę z uprawnieniami](https://kb.vmware.com/s/article/1023189?other.KM_Utility.getArticleLanguage=1&r=2&other.KM_Utility.getArticleData=1&other.KM_Utility.getArticle=1&ui-comm-runtime-components-aura-components-siteforce-qb.Quarterback.validateRoute=1&other.KM_Utility.getGUser=1).

### <a name="verify-ports"></a>Weryfikowanie portów

Ocena firmy Contoso korzysta z mapowania zależności. Mapowanie zależności wymaga zainstalowania agenta na maszynach wirtualnych, które będą oceniane. Agent musi mieć możliwość połączenia się z platformą Azure przez port TCP 443 na każdej maszynie wirtualnej. Dowiedz się więcej o [wymaganiach dotyczących połączenia](https://docs.microsoft.com/azure/log-analytics/log-analytics-concept-hybrid).

## <a name="step-4-discover-vms"></a>Krok 4. odnajdywanie maszyn wirtualnych

Na potrzeby odnajdywania maszyn wirtualnych przedstawiciel firmy Contoso tworzy projekt usługi Azure Migrate. Przedstawiciel firmy Contoso pobiera i konfiguruje maszynę wirtualną modułu zbierającego. Następnie przedstawiciel firmy Contoso uruchamia moduł zbierający w celu odnalezienia lokalnych maszyn wirtualnych.

### <a name="create-a-project"></a>Tworzenie projektu

Skonfiguruj nowy projekt usługi Azure Migrate w następujący sposób.

1. W witrynie Azure Portal > **Wszystkie usługi** znajdź pozycję **Azure Migrate**.

1. W obszarze **Usługi** wybierz pozycję **Azure Migrate**.

1. W obszarze **Przegląd**w obszarze **odnajdywanie, ocenianie i Migrowanie serwerów**wybierz pozycję **Oceń i Przeprowadź migrację serwerów**.

    ![Azure Migrate — tworzenie projektu migracji](../migrate/azure-best-practices/media/contoso-migration-assessment/assess-migrate.png)

1. W obszarze **wprowadzenie**wybierz pozycję **Dodaj narzędzia**.

1. W obszarze **Projekt migracji**wybierz subskrypcję platformy Azure i utwórz grupę zasobów, jeśli jej nie masz.

1. W obszarze **Szczegóły projektu* określ nazwę projektu i lokalizację geograficzną, w której chcesz utworzyć projekt. Obsługiwane są Stany Zjednoczone, Azja, Europa, Australia, Zjednoczone Królestwo, Kanada, Indie i Japonia.

    - Lokalizacja geograficzna projektu jest używana wyłącznie do przechowywania metadanych zebranych z lokalnych maszyn wirtualnych.
    - Podczas przeprowadzania migracji można wybrać dowolny region docelowy.

1. Wybierz opcję **Dalej**.

1. W **narzędziu Wybierz ocenę**wybierz pozycję **Azure Migrate: Ocena serwera** > **dalej**.

    ![Azure Migrate — narzędzie do oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-tool.png)

1. W obszarze **Wybierz narzędzie migracji** wybierz pozycję **Pomiń na razie dodawanie narzędzia migracji** > **Dalej**.

1. W oknie **Recenzja + Dodawanie narzędzi**przejrzyj ustawienia, a następnie wybierz pozycję **Dodaj narzędzia**.

1. Zaczekaj kilka minut, aż projekt usługi Azure Migrate zostanie wdrożony. Nastąpi przekierowanie do strony projektu. Jeśli nie widzisz projektu, możesz uzyskać do niego dostęp z obszaru **Serwery** na pulpicie nawigacyjnym usługi Azure Migrate.

### <a name="download-the-collector-appliance"></a>Pobieranie urządzenia modułu zbierającego

1. W obszarze **cele migracji** > **serwery** > **Azure Migrate: Ocena serwera**, wybierz pozycję **odkryj**.

1. W obszarze **odnajdywanie maszyn** > **są zwirtualizowane maszyny?** wybierz opcję **tak, za pomocą funkcji hypervisor VMware vSphere**.

1. Wybierz pozycję **Pobierz** , aby pobrać. Plik szablonu komórki jajowe.

     ![Azure Migrate — pobieranie modułu zbierającego](../migrate/azure-best-practices/media/contoso-migration-assessment/download-ova-v2.png)

### <a name="verify-the-collector-appliance"></a>Weryfikowanie urządzenia modułu zbierającego

Przed wdrożeniem maszyny wirtualnej przedstawiciel firmy Contoso sprawdza zabezpieczenia pliku OVA:

1. Na komputerze, na którym plik został pobrany, przedstawiciel firmy Contoso otwiera okno wiersza polecenia administratora.

1. Następnie uruchamia następujące polecenie, aby wygenerować wartość skrótu dla pliku OVA:

    `C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]`

    **Przykład:**

    `C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256`

1. Wygenerowany skrót powinien być zgodny z wartościami skrótu opisanymi w sekcji [Weryfikowanie zabezpieczeń](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#verify-security) w artykule [Ocena maszyn wirtualnych VMware na potrzeby migracji](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware) .

### <a name="create-the-collector-appliance"></a>Tworzenie urządzenia modułu zbierającego

Teraz przedstawiciel firmy Contoso może zaimportować pobrany plik do wystąpienia programu vCenter Server i zaprowizować maszynę wirtualną urządzenia modułu zbierającego:

1. W konsoli klienta vSphere przedstawiciel firmy Contoso wybiera pozycję **File** (Plik) > **Deploy OVF Template** (Wdróż szablon OVF).

    ![Klient internetowy programu vSphere — wdrażanie szablonu OVF](../migrate/azure-best-practices/media/contoso-migration-assessment/vcenter-wizard.png)

1. W kreatorze wdrażania szablonu OVF przedstawiciel firmy Contoso wybiera pozycję **Source** (Źródło), a następnie określa lokalizację pliku OVA.

1. W polu **Name and Location** (Nazwa i lokalizacja) przedstawiciel firmy Contoso określa nazwę wyświetlaną dla maszyny wirtualnej modułu zbierającego. Następnie wybiera lokalizację magazynu, w którym będzie hostowana maszyna wirtualna. Przedstawiciel firmy Contoso określa również host lub klaster, na którym będzie uruchamiane urządzenie modułu zbierającego.

1. W obszarze **Storage** (Magazyn) przedstawiciel firmy Contoso określa lokalizację magazynu. W polu **Disk Format** (Format dysku) przedstawiciel firmy Contoso wybiera sposób aprowizowania magazynu.

1. W obszarze **Network Mapping** (Mapowanie sieci) przedstawiciel firmy Contoso określa sieć, w której ma zostać nawiązane połączenie z maszyną wirtualną modułu zbierającego. Sieć musi mieć połączenie z Internetem w celu wysyłania metadanych do platformy Azure.

1. Przedstawiciel firmy Contoso przegląda ustawienia, a następnie wybiera pozycję **Power on after deployment** (Włącz po zakończeniu wdrażania) > **Finish** (Zakończ). Po utworzeniu urządzenia zostaje wyświetlony komunikat potwierdzający pomyślne zakończenie operacji.

### <a name="run-the-collector-to-discover-vms"></a>Uruchamianie modułu zbierającego w celu odnalezienia maszyn wirtualnych

Teraz przedstawiciel firmy Contoso uruchamia moduł zbierający w celu odnalezienia maszyn wirtualnych. Aktualnie moduł zbierający obsługuje wyłącznie **Angielski (Stany Zjednoczone)** jako język systemu operacyjnego i język interfejsu modułu zbierającego.

1. W konsoli klienta vSphere przedstawiciel firmy Contoso wybiera pozycję **Open Console** (Otwórz konsolę). Przedstawiciel firmy Contoso określa i akceptuje postanowienia licencyjne oraz preferencje dotyczące haseł dla maszyny wirtualnej modułu zbierającego.

1. Na pulpicie firma Contoso wybiera skrót do **Menedżera konfiguracji urządzenia platformy Microsoft Azure**.

    ![Konsola klienta vSphere — skrót do modułu zbierającego](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-shortcut-v2.png)

1. W usłudze Azure Migrate Collector przedstawiciel firmy Contoso wybiera pozycję **Skonfiguruj wymagania wstępne**. Przedstawiciel firmy Contoso akceptuje postanowienia licencyjne i zapoznaje się z informacjami innych firm.

1. Moduł zbierający sprawdza, czy maszyna wirtualna ma dostęp do Internetu, czy jest zsynchronizowany czas oraz czy jest uruchomiona usługa modułu zbierającego. (Usługa modułu zbierającego jest instalowana domyślnie na maszynie wirtualnej). Firma Contoso instaluje również zestaw SDK tworzenia dysków wirtualnych VMware vSphere.

    > [!NOTE]
    > Przyjęto tu założenie, że maszyna wirtualna ma bezpośredni dostęp do Internetu, bez serwera proxy.

    ![Azure Migrate Collector — sprawdzanie wymagań wstępnych](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-verify-prereqs-v2.png)

1. Zaloguj się do **konta** platformy Azure i wybierz wcześniej utworzoną subskrypcję oraz projekt usługi Migrate. Wprowadź również nazwę **urządzenia** , aby można było je zidentyfikować w Azure Portal.
1. W oknie **Określanie szczegółów programu vCenter Server** przedstawiciel firmy Contoso wprowadza nazwę (FQDN) lub adres IP wystąpienia programu vCenter Server i poświadczenia tylko do odczytu używane do odnajdywania.
1. Przedstawiciel firmy Contoso wybiera zakres odnajdowania maszyn wirtualnych. Moduł zbierający może odnajdywać tylko maszyny wirtualne znajdujące się w określonym zakresie. Zakresem może być określony folder, centrum danych albo klaster.

    ![Określanie szczegółów programu vCenter Server](../migrate/azure-best-practices/media/contoso-migration-assessment/collector-connect-vcenter.png)

1. Moduł zbierający zacznie teraz odnajdywać i zbierać informacje o środowisku firmy Contoso.

    ![Wyświetlanie postępu zbierania](../migrate/azure-best-practices/media/contoso-migration-assessment/migrate-discovery.png)

### <a name="verify-vms-in-the-portal"></a>Weryfikowanie maszyn wirtualnych w portalu

Po zakończeniu zbierania przedstawiciel firmy Contoso sprawdza, czy maszyny wirtualne są widoczne w portalu:

1. W projekcie usługi Azure Migrate przedstawiciel firmy Contoso wybiera pozycję **Serwery** > **Odnalezione serwery**. Przedstawiciel firmy Contoso sprawdza, czy są widoczne maszyny wirtualne, które powinny zostać odnalezione.

    ![Azure Migrate — odnalezione maszyny](../migrate/azure-best-practices/media/contoso-migration-assessment/discovery-complete.png)

1. Obecnie maszyny nie mają zainstalowanych agentów usługi Azure Migrate. Przedstawiciel firmy Contoso musi zainstalować agentów, aby wyświetlić zależności.

    ![Azure Migrate — wymagana jest Instalacja agenta](../migrate/azure-best-practices/media/contoso-migration-assessment/machines-no-agent.png)

## <a name="step-5-prepare-for-dependency-analysis"></a>Krok 5. Przygotowanie do analizy zależności

Aby wyświetlić zależności między maszynami wirtualnymi, które mają zostać ocenione, przedstawiciel firmy Contoso pobiera i instaluje agentów na maszynach wirtualnych aplikacji. Przedstawiciel firmy Contoso instaluje agentów na wszystkich maszynach wirtualnych swoich aplikacji, zarówno dla systemu Windows, jak i Linux.

### <a name="take-a-snapshot"></a>Tworzenie migawki

Aby zachować kopię maszyn wirtualnych przed ich zmodyfikowaniem, przedstawiciel firmy Contoso tworzy migawkę przed zainstalowaniem agentów.

![Migawka maszyny](../migrate/azure-best-practices/media/contoso-migration-assessment/snapshot-vm.png)

### <a name="download-and-install-the-vm-agents"></a>Pobieranie i instalowanie agentów maszyny wirtualnej

1. W obszarze **Maszyny** przedstawiciel firmy Contoso wybiera maszynę. W kolumnie **Zależności** przedstawiciel firmy Contoso wybiera pozycję **Wymaga instalacji**.

1. W okienku **Odnajdź maszyny** przedstawiciel firmy Contoso wykonuje następujące czynności:
    - Pobiera Microsoft Monitoring Agent (MMA) i agenta zależności Microsoft dla każdej maszyny wirtualnej z systemem Windows.
    - Pobiera MMA i agenta zależności dla każdej maszyny wirtualnej z systemem Linux.

1. Przedstawiciel firmy Contoso kopiuje identyfikator i klucz obszaru roboczego. Identyfikator i klucz obszaru roboczego będzie potrzebny podczas instalowania agenta MMA.

    ![Pobieranie agenta](../migrate/azure-best-practices/media/contoso-migration-assessment/download-agents.png)

### <a name="install-the-agents-on-windows-vms"></a>Instalowanie agentów na maszynach wirtualnych z systemem Windows

Przedstawiciel firmy Contoso uruchamia instalację na każdej maszynie wirtualnej.

#### <a name="install-the-mma-on-windows-vms"></a>Instalowanie agentów MMA na maszynach wirtualnych z systemem Windows

1. Przedstawiciel firmy Contoso klika dwukrotnie pobranego agenta.

1. Na stronie **Folder docelowy** przedstawiciel firmy Contoso pozostawia domyślny folder instalacji, a następnie wybiera pozycję **Dalej**.

1. W obszarze **Opcje instalacji agenta** przedstawiciel firmy Contoso wybiera pozycję **Połącz agenta z usługą Azure Log Analytics** > **Dalej**.

    ![Konfiguracja agenta Microsoft Monitoring Agent — opcje instalacji agenta](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install.png)

1. W obszarze **Azure Log Analytics** przedstawiciel firmy Contoso wkleja identyfikator i klucz obszaru roboczego skopiowane z portalu.

    ![Konfiguracja agenta Microsoft Monitoring Agent — Azure Log Analytics](../migrate/azure-best-practices/media/contoso-migration-assessment/mma-install2.png)

1. W okienku **Gotowe do instalacji** przedstawiciel firmy Contoso instaluje agenta MMA.

#### <a name="install-the-dependency-agent-on-windows-vms"></a>Instalowanie Agenta zależności na maszynach wirtualnych z systemem Windows

1. Contoso klika dwukrotnie pobranego agenta zależności.

1. Następnie akceptuje postanowienia licencyjne i czeka na zakończenie instalacji.

    ![Konfiguracja Agent zależności — Instalowanie](../migrate/azure-best-practices/media/contoso-migration-assessment/dependency-agent.png)

### <a name="install-the-agents-on-linux-vms"></a>Instalowanie agentów na maszynach wirtualnych z systemem Linux

Przedstawiciel firmy Contoso uruchamia instalację na każdej maszynie wirtualnej.

#### <a name="install-the-mma-on-linux-vms"></a>Instalowanie agentów MMA na maszynach wirtualnych z systemem Linux

1. Przedstawiciel firmy Contoso instaluje bibliotekę ctypes języka Python na każdej maszynie wirtualnej za pomocą następującego polecenia:

    `sudo apt-get install python-ctypeslib`

1. Przedstawiciel firmy Contoso musi uruchomić to polecenie, aby zainstalować agenta MMA jako użytkownik główny. Aby stać się użytkownikiem głównym, przedstawiciel firmy Contoso uruchamia następujące polecenie, a następnie wprowadza hasło główne:

    `sudo -i`

1. Przedstawiciel firmy Contoso instaluje agenta MMA w następujący sposób:

    - Przedstawiciel firmy Contoso wprowadza identyfikator i klucz obszaru roboczego w poleceniu.
    - Polecenia są przeznaczone dla środowiska 64-bitowego.
    - Identyfikator obszaru roboczego i klucz podstawowy znajdują się w obszarze roboczym usługi Log Analytics w witrynie Azure Portal. Wybierz pozycję **Ustawienia**, a następnie kartę **Połączone źródła**.
    - Uruchom następujące polecenia, aby pobrać agenta usługi Log Analytics, zweryfikować sumę kontrolną i zainstalować oraz dołączyć agenta:

    `wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w 6b7fcaff-7efb-4356-ae06-516cacf5e25d -s k7gAMAw5Bk8pFVUTZKmk2lG4eUciswzWfYLDTxGcD8pcyc4oT8c6ZRgsMy3MmsQSHuSOcmBUsCjoRiG2x9A8Mg==`

#### <a name="install-the-dependency-agent-on-linux-vms"></a>Instalowanie Agenta zależności na maszynach wirtualnych z systemem Linux

Po zainstalowaniu MMA firmy Contoso instaluje agenta zależności na maszynach wirtualnych z systemem Linux:

1. Agent zależności jest instalowany na komputerach z systemem Linux przy użyciu InstallDependencyAgent-Linux64. bin, skryptu powłoki, który ma samowyodrębniający się plik binarny. Przedstawiciel firmy Contoso uruchamia ten plik przy użyciu polecenia sh lub dodaje uprawnienia do wykonywania do samego pliku.

1. Firma Contoso instaluje agenta zależności systemu Linux jako element główny:

    `wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin && sudo sh InstallDependencyAgent-Linux64.bin -s`

## <a name="step-6-run-and-analyze-the-vm-assessment"></a>Krok 6. Uruchamianie i analizowanie oceny maszyny wirtualnej

Przedstawiciel firmy Contoso może teraz sprawdzić zależności maszyny i utworzyć grupę. Następnie uruchamia ocenę dla grupy.

### <a name="verify-dependencies-and-create-a-group"></a>Sprawdzanie zależności i tworzenie grupy

1. Aby określić, które maszyny mają być analizowane, przedstawiciel firmy Contoso wybiera pozycję **Wyświetl zależności**.

    ![Azure Migrate — wyświetlanie zależności maszyn](../migrate/azure-best-practices/media/contoso-migration-assessment/view-machine-dependencies.png)

1. W przypadku maszyny SQLVM mapa zależności zawiera następujące informacje:

    - Grupy procesów lub procesy z aktywnymi połączeniami sieciowymi uruchomione na maszynie SQLVM w określonym przedziale czasu (domyślnie przez godzinę).
    - Połączenia przychodzące TCP (klienta) do wszystkich zależnych maszyn i połączenia wychodzące TCP (serwera) z wszystkich zależnych maszyn.
    - Maszyny zależne z zainstalowanymi agentami usługi Azure Migrate są wyświetlane jako osobne pola.
    - W przypadku maszyn bez zainstalowanych agentów są wyświetlane informacje o porcie i adresie IP.

1. W przypadku maszyn z zainstalowanym agentem (WEBVM) przedstawiciel firmy Contoso wybiera pole komputera, aby wyświetlić więcej informacji. Informacje obejmują nazwę FQDN, system operacyjny i adres MAC.

    ![Azure Migrate — wyświetlanie zależności grupy](../migrate/azure-best-practices/media/contoso-migration-assessment/sqlvm-dependencies.png)

1. Przedstawiciel firmy Contoso wybiera maszyny wirtualne, które mają zostać dodane do grupy (SQLVM i WEBVM). Firma Contoso utrzymuje klucz `Ctrl` podczas klikania, aby wybrać wiele maszyn wirtualnych.

1. Przedstawiciel firmy Contoso wybiera pozycję **Utwórz grupę**, a następnie wprowadza nazwę (**smarthotelapp**).

    > [!NOTE]
    > Aby wyświetlić bardziej szczegółowe zależności, możesz rozszerzyć zakres czasu. Możesz wybrać przedział lub datę początkową i datę końcową.

### <a name="run-an-assessment"></a>Uruchamianie oceny

1. W okienku **Grupy** przedstawiciel firmy Contoso otwiera grupę (**smarthotelapp**), a następnie wybiera pozycję **Utwórz ocenę**.

    ![Azure Migrate — tworzenie oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/run-vm-assessment.png)

1. Aby wyświetlić ocenę, przedstawiciel firmy Contoso wybiera pozycję **Zarządzaj** > **Oceny**.

Przedstawiciel firmy Contoso korzysta z domyślnych ustawień oceny, ale możesz [je dostosować](https://docs.microsoft.com/azure/migrate/how-to-modify-assessment).

### <a name="analyze-the-vm-assessment"></a>Analizowanie oceny maszyny wirtualnej

Ocena usługi Azure Migrate zawiera informacje dotyczące zgodności środowiska lokalnego z platformą Azure, sugerowanych rozmiarów maszyn wirtualnych platformy Azure oraz szacowanych miesięcznych kosztów platformy Azure.

![Azure Migrate — raport z oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-overview.png)

#### <a name="review-confidence-rating"></a>Przegląd oceny zaufania

![Azure Migrate — wyświetlanie oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/assessment-display.png)

Ocena zaufania jest reprezentowana przez gwiazdki (od 1 do 5). 1 gwiazdka to ocena najniższa, a 5 gwiazdek to ocena najwyższa.

- Ocena zaufania jest przypisana do oceny na podstawie dostępności punktów danych potrzebnych do obliczenia oceny.
- Pomaga to oszacować niezawodność zaleceń dotyczących rozmiarów udostępnianych przez usługę Azure Migrate.
- Ocena zaufania jest przydatna podczas ustalania *rozmiaru na podstawie wydajności*. Usługa Azure Migrate może nie dysponować wystarczającą liczbą punktów danych, aby móc ustalić rozmiar na podstawie użycia. W przypadku ustalania rozmiaru *jako lokalnego* ocena zaufania to zawsze 5 gwiazdek, ponieważ usługa Azure Migrate ma wszystkie punkty danych, których potrzebuje do ustalenia rozmiaru maszyny wirtualnej.
- W zależności od wartości procentowej dostępnych punktów danych ocenę zaufania dla oceny określa:

   Dostępność punktów danych | Ocena zaufania
   --- | ---
   0%–20% | 1 gwiazdka
   21%–40% | 2 gwiazdki
   41%–60% | 3 gwiazdki
   61%–80% | 4 gwiazdki
   81%–100% | 5 gwiazdek

#### <a name="verify-azure-readiness"></a>Sprawdzanie gotowości na platformę Azure

![Azure Migrate — gotowość do oceny](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-readiness.png)

Raport z oceny zawiera podsumowane informacje w tabeli. Do wyświetlenia treści dotyczącej ustalania rozmiaru na podstawie wydajności usługa Azure Migrate potrzebuje następujących informacji. Jeśli nie można zebrać tych informacji, ocena rozmiarów może być niedokładna.

- Dane użycia procesora CPU i pamięci.
- Liczba operacji we/wy na sekundę i przepływność dla każdego dysku podłączonego do maszyny wirtualnej.
- Informacje o ruchu wchodzącym/wychodzącym dla każdej karty sieciowej podłączonej do maszyny wirtualnej.

<!-- markdownlint-disable MD033 -->

Ustawienie | Wskazanie | Szczegóły
--- | --- | ---
**Gotowość maszyny wirtualnej platformy Azure** | Wskazuje, czy maszyna wirtualna jest gotowa do migracji. | Możliwe stany:<br/><br/>– Gotowa na platformę Azure<br/><br/>– Gotowa warunkowo <br/><br/>– Niegotowa na platformę Azure<br/><br/>– Nieznana gotowość<br/><br/> Jeśli maszyna wirtualna nie jest gotowa, w usłudze Azure Migrate są wyświetlane instrukcje rozwiązania tego problemu.
**Rozmiar maszyny wirtualnej platformy Azure** | W przypadku gotowych maszyn wirtualnych w usłudze Azure Migrate są udostępniane zalecenia dotyczące rozmiaru maszyny wirtualnej platformy Azure. | Zalecenia te zależą od właściwości oceny:<br/><br/>– Jeśli wybrano opcję ustalania rozmiaru na podstawie wydajności, uwzględniana jest historia wydajności maszyn wirtualnych.<br/><br/>– Jeśli wybrano opcję *jak lokalne*, rozmiar jest ustalany na podstawie rozmiaru lokalnej maszyny wirtualnej, a dane dotyczące użycia nie są uwzględniane.
**Sugerowane narzędzie** | Ponieważ na maszynach platformy Azure działają agenci, usługa Azure Migrate sprawdza procesy uruchomione na konkretnej maszynie. Dzięki temu wiadomo, czy dana maszyna jest maszyną bazy danych.
**Informacje o maszynie wirtualnej** | Raport zawiera ustawienia lokalnej maszyny wirtualnej, w tym system operacyjny, typ rozruchu oraz informacje o dysku i magazynie.

<!-- markdownlint-enable MD033 -->

#### <a name="review-monthly-cost-estimates"></a>Przegląd szacowanego kosztu miesięcznego

Ten widok przedstawia łączne koszty zasobów obliczeniowych i magazynowych w przypadku korzystania z maszyn wirtualnych na platformie Azure. Przedstawiono w nim także szczegółowe informacje dotyczące poszczególnych maszyn.

![Azure Migrate — koszty platformy Azure](../migrate/azure-best-practices/media/contoso-migration-assessment/azure-costs.png)

- Koszty są szacowane na podstawie zalecanego rozmiaru maszyny.
- Szacowany miesięczny koszt zasobów obliczeniowych i magazynowych jest agregowany dla wszystkich maszyn wirtualnych w grupie.

## <a name="clean-up-after-assessment"></a>Czyszczenie po przeprowadzeniu oceny

- Po zakończeniu oceny przedstawiciel firmy Contoso zachowuje urządzenie usługi Azure Migrate do użycia w przyszłych ocenach.
- Przedstawiciel firmy Contoso wyłącza maszynę wirtualną VMware. Zostanie ona ponownie użyta przez firmę Contoso podczas oceniania dodatkowych maszyn wirtualnych.
- Projekt **Contoso Migration** zostanie również zachowany na platformie Azure. Ten projekt jest obecnie wdrożony w grupie zasobów **ContosoFailoverRG** w regionie Wschodnie stany USA na platformie Azure.
- Maszyna wirtualna modułu zbierającego ma 180-dniową licencję ewaluacyjną. Po wygaśnięciu jej ważności przedstawiciel firmy Contoso będzie musiał pobrać moduł zbierający i ponownie go skonfigurować.

## <a name="conclusion"></a>Podsumowanie

W tym scenariuszu firma Contoso ocenia swoją bazę danych aplikacji SmartHotel360 przy użyciu narzędzia do oceny migracji danych. Za pomocą usługi Azure Migrate dokonywana jest również ocena lokalnych maszyn wirtualnych. Przedstawiciel firmy Contoso przegląda oceny w celu upewnienia się, że lokalne zasoby są gotowe do migracji na platformę Azure.

## <a name="next-steps"></a>Następne kroki

Gdy firma Contoso oceni to obciążenie jako potencjalnie nadające się do migracji, może rozpocząć przygotowywanie swojej infrastruktury lokalnej i infrastruktury platformy Azure na potrzeby migracji. Zapoznaj się z artykułem dotyczącym [wdrażania infrastruktury platformy Azure](../migrate/azure-best-practices/contoso-migration-infrastructure.md) w sekcji najlepszych rozwiązań w zakresie migrowania struktury wdrażania chmury, aby zobaczyć przykład, jak firma Contoso wykonuje te procesy.
