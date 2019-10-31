---
title: Ponowne hostowanie aplikacji dla systemu Linux, używanej do obsługi pomocy technicznej, na platformie Azure i w usłudze Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak firma Contoso przeprowadza ponowne hostowanie lokalnej aplikacji dla systemu Linux przez migrację na maszyny wirtualne platformy Azure i do usługi Azure Database for MySQL.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c623d7c537d19f700fed4d28523f60c4fd03d4ea
ms.sourcegitcommit: e0a783dac15bc4c41a2f4ae48e1e89bc2dc272b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/30/2019
ms.locfileid: "73058626"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Ponowne hostowanie aplikacji lokalnej dla systemu Linux na maszynach wirtualnych platformy Azure i w usłudze Azure Database for MySQL

W tym artykule opisano, w jaki sposób fikcyjna firma Contoso ponownie hostuje dwuwarstwową aplikację opartą na stosie LAMP (Linux, Apache, MySQL, PHP), migrując ją ze środowiska lokalnego na platformę Azure przy użyciu maszyn wirtualnych platformy Azure i usługi Azure Database for MySQL.

Używana w tym przykładzie aplikacja do obsługi pomocy technicznej, osTicket, jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Czynniki biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, przez co lokalne systemy i infrastruktura stają się przeciążone.
- **Ograniczanie ryzyka.** Aplikacja do obsługi pomocy technicznej ma kluczowe znaczenie dla działalności firmy. Firma Contoso chce przenieść ją na platformę Azure, eliminując ryzyko.
- **Rozszerzanie.** Firma Contoso nie chce teraz zmieniać używanej aplikacji. Po prostu chce mieć pewność, że aplikacja jest stabilna.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury w firmie Contoso określił cele migracji, aby wybrać najlepszą metodę migracji:

- Po migracji aplikacja na platformie Azure powinna mieć taką samą wydajność jak obecnie, gdy działa w lokalnym środowisku programu VMware. Aplikacja działająca w chmurze będzie miała tak samo krytyczne znaczenie jak w środowisku lokalnym.
- Firma Contoso nie chce inwestować w tę aplikację. Jest ona ważna dla działalności firmy, ale firma Contoso chce po prostu bezpiecznie przenieść ją do chmury w obecnej postaci.
- Firma Contoso przeprowadziła już kilka procesów migracji aplikacji dla systemu Windows, a teraz chce poznać sposób korzystania z infrastruktury platformy Azure z systemem Linux.
- Firma Contoso chce zminimalizować zadania administratora bazy danych po przeniesieniu aplikacji do chmury.

## <a name="proposed-architecture"></a>Proponowana architektura

W tym scenariuszu:

- Aplikacja działa warstwowo na dwóch maszynach wirtualnych (`OSTICKETWEB` i `OSTICKETMYSQL`).
- Maszyny wirtualne znajdują się na hoście VMware ESXi `contosohost1.contoso.com` (wersja 6.5).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (`vcenter.contoso.com`) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (`contoso-datacenter`) i lokalny kontroler domeny (`contosodc1`).
- Aplikacja warstwy internetowej na maszynie `OSTICKETWEB` zostanie przeniesiona na maszynę wirtualną platformy Azure w modelu IaaS.
- Baza danych aplikacji zostanie przeniesiona do usługi typu PaaS, Azure Database for MySQL.
- Ponieważ migracja dotyczy obciążenia produkcyjnego, zasoby będą znajdować się w grupie zasobów produkcyjnych `ContosoRG`.
- Zasoby zostaną zreplikowane do regionu podstawowego (Wschodnie stany USA 2) i umieszczone w sieci produkcyjnej (`VNET-PROD-EUS2`):
  - Internetowa maszyna wirtualna zostanie umieszczona w podsieci frontonu (`PROD-FE-EUS2`).
  - Wystąpienie bazy danych zostanie umieszczone w podsieci bazy danych (`PROD-DB-EUS2`).
- Baza danych aplikacji zostanie przeniesiona do usługi Azure Database for MySQL przy użyciu narzędzi MySQL.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi proces migracji w następujący sposób:

Migracja maszyny wirtualnej warstwy internetowej:

1. W pierwszym kroku firma Contoso skonfiguruje platformę Azure i infrastrukturę lokalną pod kątem wdrożenia usługi Site Recovery.
2. Po przygotowaniu platformy Azure i składników lokalnych firma Contoso skonfiguruje i włączy replikację maszyn wirtualnych.
3. Gdy replikacja zacznie działać, firma Contoso przeprowadzi migrację maszyny wirtualnej na platformę Azure przez przełączenie jej do trybu failover.

Migracja bazy danych:

1. Firma Contoso przeprowadzi aprowizację wystąpienia usługi MySQL na platformie Azure.
2. Firma Contoso skonfiguruje aplikację MySQL Workbench i utworzy lokalnie kopię zapasową bazy danych.
3. Następnie firma Contoso przywróci bazę danych z lokalnej kopii zapasowej na platformę Azure.

![Proces migracji](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Usługi platformy Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | Usługa organizuje migrację i odzyskiwanie po awarii maszyn wirtualnych platformy Azure, lokalnych maszyn wirtualnych i serwerów fizycznych oraz zarządza tymi procesami. | Podczas replikacji na platformę Azure naliczane są opłaty za usługę Azure Storage. Maszyny wirtualne platformy Azure zostaną utworzone w momencie przejścia w tryb failover i wówczas będą naliczane opłaty. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery) o opłatach i cenach.
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Baza danych opiera się na aparacie serwera MySQL typu open-source. Udostępnia on w pełni zarządzaną, gotową do używania w przedsiębiorstwie bazę danych MySQL w wersji Community jako usługę do opracowywania i wdrażania aplikacji.

## <a name="prerequisites"></a>Wymagania wstępne

W tym scenariuszu firma Contoso potrzebuje następujących elementów.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje w jednym z poprzednich artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Infrastruktura platformy Azure wymagana do migracji](./contoso-migration-infrastructure.md).<br/><br/> Dowiedz się więcej na temat szczegółowych wymagań usługi Site Recovery związanych z [siecią](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) i [magazynem](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage).
**Serwery lokalne** | Lokalny serwer vCenter w wersji 5.5, 6.0 lub 6.5<br/><br/> Host ESXi w wersji 5.5, 6.0 lub 6.5<br/><br/> Co najmniej jedna maszyna wirtualna programu VMware uruchomiona na hoście ESXi.
**Lokalne maszyny wirtualne** | [Zapoznaj się z listą wymagań maszyn wirtualnych z systemem Linux](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#replicated-machines), których migracja jest obsługiwana przez usługę Site Recovery.<br/><br/> Sprawdź obsługiwane [systemy plików i magazynu systemu Linux](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#linux-file-systemsguest-storage).<br/><br/> Maszyny wirtualne muszą spełniać [wymagania platformy Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Administratorzy firmy Contoso przeprowadzają migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1: przygotowanie platformy Azure dla Site Recovery.** Tworzą konto usługi Azure Storage do przechowywania replikowanych danych oraz magazyn usługi Recovery Services.
> - **Krok 2: Przygotowanie lokalnego programu VMware do Site Recovery.** Przygotowują konta do użycia na potrzeby odnajdowania maszyn wirtualnych i instalacji agenta oraz przygotowują się do połączenia z maszynami wirtualnymi platformy Azure po przejściu w tryb failover.
> - **Krok 3. Przeprowadź obsługę administracyjną bazy danych.** Na platformie Azure aprowizują oni wystąpienie usługi Azure Database for MySQL.
> - **Krok 4. replikowanie maszyn wirtualnych.** Konfigurują źródłowe i docelowe środowiska usługi Site Recovery, konfigurują zasady replikacji i uruchamiają replikację maszyn wirtualnych do usługi Azure Storage.
> - **Krok 5. Migrowanie bazy danych.** Konfigurują migrację przy użyciu narzędzi usługi MySQL.
> - **Krok 6. Migrowanie maszyn wirtualnych przy użyciu Site Recovery.** Na końcu przeprowadzają próbne przejście w tryb failover, aby sprawdzić, czy wszystko działa prawidłowo, a następnie przeprowadzają pełne przejście w tryb failover, aby ukończyć migrację maszyn wirtualnych na platformę Azure.

## <a name="step-1-prepare-azure-for-the-site-recovery-service"></a>Krok 1. Przygotowywanie platformy Azure dla usługi Site Recovery

Firma Contoso musi utworzyć kilka składników platformy Azure na potrzeby usługi Site Recovery:

- Sieć wirtualną, w której będą znajdować się zasoby w trybie failover. Firma Contoso już utworzyła tę sieć wirtualną na etapie [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md).
- Nowe konto usługi Azure Storage do przechowywania replikowanych danych.
- Magazyn usług Recovery Services na platformie Azure.

Administratorzy firmy Contoso tworzą konto usługi Storage i magazyn w następujący sposób:

1. Tworzą konto usługi Storage (**contosovmsacc20180528**) w regionie Wschodnie stany USA 2.

    - Konto magazynu musi znajdować się w tym samym regionie, co magazyn usługi Recovery Services.
    - Administratorzy używają konta ogólnego przeznaczenia w warstwie Standard Storage z replikacją LRS (magazyn lokalnie nadmiarowy).

    ![Magazyn usługi Site Recovery](./media/contoso-migration-rehost-linux-vm-mysql/asr-storage.png)

2. Po utworzeniu sieci i konta usługi Storage administratorzy tworzą magazyn (ContosoMigrationVault), który umieszczają w grupie zasobów **ContosoFailoverRG**, w regionie podstawowym Wschodnie stany USA 2.

    ![Magazyn usługi Recovery Services](./media/contoso-migration-rehost-linux-vm-mysql/asr-vault.png)

**Potrzebujesz dodatkowej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure) na temat konfigurowania platformy Azure pod kątem usługi Site Recovery.

## <a name="step-2-prepare-on-premises-vmware-for-site-recovery"></a>Krok 2: Przygotowanie lokalnego programu VMware do Site Recovery

Administratorzy firmy Contoso przygotowują lokalną infrastrukturę VMware w następujący sposób:

- Tworzą konto na serwerze vCenter w celu zautomatyzowania odnajdowania maszyn wirtualnych.
- Tworzą konto umożliwiające automatyczną instalację usługi mobilności na maszynach wirtualnych programu VMware, które będą replikowane.
- Przygotowują lokalne maszyny wirtualne do nawiązania połączenia z maszynami wirtualnymi platformy Azure utworzonymi po migracji.

### <a name="prepare-an-account-for-automatic-discovery"></a>Przygotowywanie konta do automatycznego odnajdowania

Usługa Site Recovery musi mieć dostęp do serwerów VMware w następujących celach:

- Automatyczne odnajdywanie maszyn wirtualnych. Wymagane jest co najmniej konto tylko do odczytu.
- Organizowanie replikacji, trybu failover i powrotu po awarii. Potrzebne jest konto, na którym można uruchamiać operacje takie jak tworzenie i usuwanie dysków, a także włączanie maszyn wirtualnych.

Administratorzy firmy Contoso konfigurują to konto w następujący sposób:

1. Tworzą rolę na poziomie serwera vCenter.
2. Następnie przypisują do tej roli wymagane uprawnienia.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Przygotowywanie konta do instalacji usługi Mobility

Usługa mobilności musi być zainstalowana na każdej maszynie wirtualnej, którą firma Contoso chce zmigrować.

- Po włączeniu replikacji dla maszyny wirtualnej usługa Site Recovery może przeprowadzić automatyczną instalację wypychaną tego składnika.
- W przypadku automatycznej instalacji. Usługa Site Recovery potrzebuje konta z uprawnieniami dostępu do maszyny wirtualnej.
- Szczegóły konta wprowadza się podczas konfigurowania replikacji.
- Może to być konto domeny lub konto lokalne, ale musi mieć uprawnienia do instalowania.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Przygotowanie do połączenia z maszynami wirtualnymi Azure po przejściu do trybu failover

Po przełączeniu w tryb failover na platformie Azure firma Contoso chce mieć możliwość nawiązania połączenia z maszynami wirtualnymi na platformie Azure. Aby to umożliwić, administratorzy firmy Contoso muszą wykonać następujące czynności:

- Aby uzyskać dostęp za pośrednictwem Internetu, muszą włączyć protokół SSH na lokalnych maszynach wirtualnych systemu Linux przed migracją. W przypadku Ubuntu można to zrobić za pomocą następującego polecenia: **sudo apt-get SSH Install-y**.
- Po przełączeniu w tryb failover powinni sprawdzić **diagnostykę rozruchu**, aby wyświetlić zrzut ekranu maszyny wirtualnej.
- Jeśli to nie zadziała, muszą sprawdzić, czy maszyna wirtualna jest uruchomiona, i zapoznać się z tymi [poradami dotyczącymi rozwiązywania problemów](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) na temat tworzenia i przypisywania roli na potrzeby automatycznego odnajdowania.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) na temat tworzenia konta na potrzeby instalacji wypychanej usługi mobilności.

## <a name="step-3-provision-azure-database-for-mysql"></a>Krok 3. Udostępnianie Azure Database for MySQL

Administratorzy firmy Contoso aprowizują wystąpienie bazy danych MySQL w regionie podstawowym Wschodnie stany USA 2.

1. W witrynie Azure Portal tworzą zasób usługi Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. Dodają nazwę **contosoosticket** dla usługi bazy danych platformy Azure. Dodają bazę danych do grupy zasobów produkcyjnych **ContosoRG** i określają jej poświadczenia.
3. Wersja lokalnej bazy danych MySQL to 5.7, dlatego wybierają tę wersję w celu zachowania zgodności. Używają rozmiarów domyślnych, które spełniają wymagania dotyczące bazy danych.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. W obszarze **Opcje nadmiarowości kopii zapasowej** wybierają pozycję **Geograficznie nadmiarowe**. Ta opcja umożliwia przywrócenie bazy danych w regionie dodatkowym Środkowe stany USA w przypadku wystąpienia awarii. Tę opcję można skonfigurować tylko podczas aprowizowania bazy danych.

     ![Nadmiarowość](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. W obszarze sieci **VNET-PROD-EUS2** > **Punkty końcowe usługi** dodają punkt końcowy usługi (podsieć bazy danych) dla usługi SQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. Po dodaniu podsieci tworzą regułę sieci wirtualnej, która zezwala na dostęp z poziomu podsieci bazy danych w sieci produkcyjnej.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-4-replicate-the-on-premises-vms"></a>Krok 4. replikowanie lokalnych maszyn wirtualnych

Przed migracją maszyny wirtualnej warstwy internetowej na platformę Azure administratorzy firmy Contoso muszą skonfigurować i włączyć replikację.

### <a name="set-a-protection-goal"></a>Określanie celu ochrony

1. W obszarze magazynu po wybraniu nazwy magazynu (ContosoVMVault) należy ustawić cel replikacji (**Wprowadzenie** > **Site Recovery** > **Przygotowanie infrastruktury**).
2. Administratorzy określają, że ich maszyny wirtualne znajdują się w środowisku lokalnym, że są to maszyny wirtualne VMware, i że chcą przeprowadzić replikację na platformie Azure.

    ![Cel replikacji](./media/contoso-migration-rehost-linux-vm-mysql/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Potwierdzanie planowania wdrożenia

Aby przejść dalej, należy potwierdzić, że zakończono planowanie wdrożenia, wybierając pozycję **Tak, już to zostało zrobione**. W tym scenariuszu firma Contoso migruje tylko jedną maszynę wirtualną, co nie wymaga planowania wdrożenia.

### <a name="set-up-the-source-environment"></a>Konfigurowanie środowiska źródłowego

Teraz administratorzy firmy Contoso konfigurują środowisko źródłowe. W tym celu za pomocą szablonu OVF wdrożą serwer konfiguracji usługi Site Recovery jako wysoce dostępną lokalną maszynę wirtualną programu VMware. Po uruchomieniu serwera konfiguracji rejestrują go w magazynie.

Na serwerze konfiguracji jest uruchomionych kilka składników:

- Składnik serwera konfiguracji służy do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure oraz do zarządzania replikacją danych.
- Serwer przetwarzania, który działa jako brama replikacji. Odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła je do usługi Azure Storage.
- Serwer przetwarzania instaluje także usługę mobilności na maszynach wirtualnych, które będą replikowane, i automatycznie odnajduje lokalne maszyny wirtualne VMware.

Administratorzy firmy Contoso robią to w następujący sposób:

1. Pobierają szablon OVF z obszaru **Przygotowanie infrastruktury** > **Źródło** > **Serwer konfiguracji**.

    ![Pobieranie szablonu OVF](./media/contoso-migration-rehost-linux-vm-mysql/add-cs.png)

2. Importują szablon do programu VMware w celu utworzenia i wdrożenia maszyny wirtualnej.

    ![Szablon OVF](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-wizard.png)

3. Po pierwszym uruchomieniu maszyna wirtualna uruchamia środowisko instalacji systemu Windows Server 2016. Administratorzy akceptują umowę licencyjną i wprowadzają hasło administratora.
4. Po zakończeniu instalacji logują się na maszynie wirtualnej jako administrator. Po pierwszym zalogowaniu zostanie domyślnie uruchomione narzędzie do konfiguracji usługi Azure Site Recovery.
5. W tym narzędziu należy określić nazwę używaną do zarejestrowania serwera konfiguracji w magazynie.
6. Narzędzie sprawdza, czy maszyna wirtualna może połączyć się z platformą Azure.
7. Po nawiązaniu połączenia administratorzy logują się w subskrypcji platformy Azure. Użyte poświadczenia muszą zapewniać dostęp do magazynu, w którym zarejestrują serwer konfiguracji.

    ![Rejestrowanie serwera konfiguracji](./media/contoso-migration-rehost-linux-vm-mysql/config-server-register2.png)

8. Narzędzie wykonuje pewne zadania konfiguracyjne, a następnie wywołuje ponowne uruchomienie.
9. Administratorzy ponownie logują się na maszynie, po czym jest automatycznie uruchamiany kreator zarządzania serwerem konfiguracji.
10. W kreatorze wybierają kartę sieciową, która będzie odbierała ruch związany z replikacją. Po skonfigurowaniu tego ustawienia nie można go zmienić.
11. Wybierają subskrypcję, grupę zasobów i magazyn do zarejestrowania serwera konfiguracji.

    ![magazyn](./media/contoso-migration-rehost-linux-vm-mysql/cswiz1.png)

12. Teraz pobierają i instalują serwer MySQL oraz oprogramowanie VMware PowerCLI.
13. Po przeprowadzeniu walidacji określają nazwę FQDN lub adres IP serwera vCenter lub hosta vSphere. Pozostawiają port domyślny i określają przyjazną nazwę serwera vCenter.
14. Wprowadzają konto utworzone na potrzeby automatycznego odnajdowania oraz poświadczenia, których użyje usługa Site Recovery w celu automatycznej instalacji usługi mobilności.

    ![vCenter](./media/contoso-migration-rehost-linux-vm-mysql/cswiz2.png)

15. Po zakończeniu rejestracji sprawdzają w witrynie Azure Portal, czy serwer konfiguracji i serwer VMware są widoczne na stronie **Źródło** w magazynie. Odnajdowanie może potrwać 15 minut lub dłużej.
16. Gdy wszystko jest gotowe, usługa Site Recovery łączy się z serwerami VMware i odnajduje maszyny wirtualne.

### <a name="set-up-the-target"></a>Konfigurowanie środowiska docelowego

Teraz administratorzy firmy Contoso wprowadzają ustawienia replikacji w środowisku docelowym.

1. W obszarze **Przygotowanie infrastruktury** > **Docelowa** wybierają ustawienia środowiska docelowego.
2. Usługa Site Recovery sprawdza, czy we wskazanym środowisku docelowym istnieje konto usługi Azure Storage i sieć.

### <a name="create-a-replication-policy"></a>Tworzenie zasad replikacji

Po skonfigurowaniu środowiska źródłowego i docelowego administratorzy firmy Contoso mogą utworzyć zasady replikacji.

1. W obszarze **Przygotowanie infrastruktury** > **Ustawienia replikacji** > **Zasady replikacji** >  **Utwórz i skojarz** administratorzy tworzą zasady o nazwie **ContosoMigrationPolicy**.

2. Korzystają z ustawień domyślnych:
    - **Próg punktu odzyskiwania:** Domyślnie 60 minut. Ta wartość określa częstość tworzenia punktów odzyskiwania. Przekroczenie tego limitu przez replikację ciągłą spowoduje wygenerowanie alertu.
    - **Przechowywanie punktów odzyskiwania:** Domyślnie 24 godziny. Ta wartość określa długość okna przechowywania dla każdego punktu odzyskiwania. Replikowane maszyny wirtualne można odzyskać do dowolnego punktu w tym oknie.
    - **Częstotliwość migawek spójnych na poziomie aplikacji:** Wartość domyślna to godzina. Ta wartość określa częstotliwość tworzenia migawek spójnych na poziomie aplikacji.

        ![Tworzenie zasad replikacji](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy.png)

3. Zasady zostaną automatycznie skojarzone z serwerem konfiguracji.

    ![Kojarzenie zasad replikacji](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy2.png)

**Potrzebujesz dodatkowej pomocy?**

- Pełne instrukcje do wszystkich kroków można znaleźć w artykule [Konfigurowanie odzyskiwania po awarii dla lokalnych maszyn wirtualnych VMware](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Szczegółowe instrukcje pomogą Ci w [skonfigurowaniu środowiska źródłowego](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [wdrożeniu serwera konfiguracji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) i [skonfigurowaniu ustawień replikacji](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).
- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/extensions/agent-linux) na temat agenta gościa platformy Azure dla systemu Linux.

### <a name="enable-replication-for-the-web-vm"></a>Włączanie replikacji maszyny wirtualnej warstwy internetowej

Teraz administratorzy firmy Contoso mogą rozpocząć replikację maszyny wirtualnej **OSTICKETWEB**.

1. W obszarze **Replikowanie aplikacji** > **Źródło** >  **+Replikuj** wybierają ustawienia źródła.
2. Wskazują, że chcą włączyć maszyny wirtualne i wybierają ustawienia środowiska źródłowego, w tym serwer vCenter i serwer konfiguracji.

    ![Włączanie replikacji](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication-source.png)

3. Teraz określają ustawienia środowiska docelowego. Te ustawienia obejmują grupę zasobów i sieć, w której zostanie umieszczona maszyna wirtualna platformy Azure po przejściu w tryb failover, a także konto usługi Storage, na którym będą przechowywane zreplikowane dane.

     ![Włączanie replikacji](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication2.png)

4. Wybierają maszynę wirtualną **OSTICKETWEB** do replikacji.

    ![Włączanie replikacji](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication3.png)

5. W obszarze właściwości maszyny wirtualnej wybierają konto, które powinno być używane w celu automatycznego zainstalowania usługi mobilności na maszynie wirtualnej.

     ![Usługa mobilności](./media/contoso-migration-rehost-linux-vm-mysql/linux-mobility.png)

6. W obszarze **Ustawienia replikacji** > **Konfigurowanie ustawień replikacji** sprawdzają, czy zastosowano właściwe zasady replikacji, a następnie wybierają pozycję **Włącz replikację**. Usługa mobilności zostanie zainstalowana automatycznie.
7. Postęp replikacji można śledzić w obszarze **Zadania**. Po uruchomieniu zadania **Sfinalizuj ochronę** maszyna jest gotowa do przejścia w tryb failover.

**Potrzebujesz dodatkowej pomocy?**

Pełne instrukcje do wszystkich kroków można znaleźć w artykule [Enable replication (Włączanie replikacji)](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-5-migrate-the-database"></a>Krok 5. Migrowanie bazy danych

Administratorzy firmy Contoso migrują bazę danych przy użyciu funkcji tworzenia kopii zapasowych i przywracania za pomocą narzędzi MySQL. Instalują aplikację MySQL Workbench, tworzą kopię zapasową bazy danych z maszyny wirtualnej OSTICKETMYSQL, a następnie przywracają ją na serwer usługi Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalacja aplikacji MySQL Workbench

1. Sprawdzają [wymagania wstępne i pliki do pobrania aplikacji MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Instalują program MySQL Workbench dla systemu Windows zgodnie [z instrukcjami instalacji](https://dev.mysql.com/doc/workbench/en/wb-installing.html).
3. W programie MySQL Workbench tworzą połączenie usługi MySQL z maszyną OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. Eksportują bazę danych **osticket** do samodzielnego pliku lokalnego.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. Po utworzeniu lokalnej kopii zapasowej bazy danych tworzą połączenie z wystąpieniem usługi Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Teraz mogą zaimportować (przywrócić) bazę danych w wystąpieniu usługi Azure Database for MySQL z utworzonego samodzielnego pliku. Dla wystąpienia zostanie utworzony nowy schemat (osticket).

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

## <a name="step-6-migrate-the-vms-with-site-recovery"></a>Krok 6. Migrowanie maszyn wirtualnych za pomocą Site Recovery

Na koniec administratorzy firmy Contoso uruchamiają szybki test przejścia w tryb failover, a następnie przeprowadzają migrację maszyny wirtualnej.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Próba przejścia w tryb failover pozwala sprawdzić, czy wszystko działa zgodnie z oczekiwaniami, przed przeprowadzeniem faktycznej migracji.

1. Uruchamiają testowe przełączenie w tryb failover przy użyciu najnowszego dostępnego punktu w czasie (**Najnowszy przetworzony**).
2. Wybierają opcję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**, aby usługa Site Recovery podjęła próbę zamknięcia źródłowej maszyny wirtualnej przed jej przełączeniem w tryb failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się.
3. Próbne przełączenia do trybu failover:

    - Uruchamiane jest sprawdzanie wymagań wstępnych, aby upewnić się, że zostały spełnione wszystkie warunki migracji.
    - Tryb failover przetwarza dane, aby umożliwić utworzenie maszyny wirtualnej platformy Azure. Jeśli zostanie wybrany najnowszy punkt odzyskiwania, punkt odzyskiwania zostanie utworzony na podstawie danych.
    - Tworzona jest maszyna wirtualna platformy Azure przy użyciu danych przetworzonych w poprzednim kroku.

4. Po zakończeniu przechodzenia w tryb failover w witrynie Azure Portal będzie widoczna replika maszyny wirtualnej na platformie Azure. Administratorzy sprawdzają, czy maszyna wirtualna ma prawidłowy rozmiar, jest połączona z odpowiednią siecią i jest uruchomiona.
5. Gdy wszystko zostanie sprawdzone, przeprowadzają czyszczenie po przejściu do trybu failover oraz rejestrują i zapisują wszelkie obserwacje.

### <a name="migrate-the-vm"></a>migrowanie maszyny wirtualnej

Aby przeprowadzić migrację maszyny wirtualnej, administratorzy firmy Contoso tworzą plan odzyskiwania, który obejmuje maszynę wirtualną, i wykonują przejście w tryb failover na platformie Azure.

1. Tworzą plan i dodają do niego pozycję **OSTICKETWEB**.

    ![Plan odzyskiwania](./media/contoso-migration-rehost-linux-vm-mysql/recovery-plan.png)

2. Uruchamiają tryb failover z użyciem utworzonego planu. Wybierają najnowszy punkt odzyskiwania i określają, że usługa Site Recovery powinna podjąć próbę zamknięcia lokalnej maszyny wirtualnej przed wyzwoleniem trybu failover. Na stronie **Zadania** można śledzić postęp trybu failover.

    ![Tryb failover](./media/contoso-migration-rehost-linux-vm-mysql/failover1.png)

3. Podczas przełączania maszyn wirtualnych w tryb failover program vCenter Server wydaje polecenia zatrzymania dwóch maszyn wirtualnych uruchomionych na hoście ESXi.

    ![Tryb failover](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-failover.png)

4. Po przejściu w tryb failover administratorzy sprawdzają, czy maszyna wirtualna platformy Azure jest widoczna zgodnie z oczekiwaniami w witrynie Azure Portal.

    ![Tryb failover](./media/contoso-migration-rehost-linux-vm-mysql/failover2.png)

5. Po sprawdzeniu maszyny wirtualnej kończą migrację. Spowoduje to zatrzymanie replikacji maszyny wirtualnej oraz zatrzymanie naliczania opłat za usługę Site Recovery dla maszyny wirtualnej.

    ![Tryb failover](./media/contoso-migration-rehost-linux-vm-mysql/failover3.png)

**Potrzebujesz dodatkowej pomocy?**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure) o próbnym uruchamianiu trybu failover.
- [Dowiedz się](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans), jak utworzyć plan odzyskiwania.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover) na temat przechodzenia do trybu failover na platformie Azure.

### <a name="connect-the-vm-to-the-database"></a>Łączenie maszyny wirtualnej z bazą danych

W ostatnim kroku procesu migracji administratorzy firmy Contoso aktualizują parametry połączenia aplikacji tak, aby wskazywały usługę Azure Database for MySQL.

1. Konfigurują połączenie SSH z maszyną wirtualną OSTICKETMYSQL za pomocą programu Putty lub innego klienta SSH. Maszyna wirtualna jest prywatna, a więc nawiązują połączenie przy użyciu prywatnego adresu IP.

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm-mysql/db-connect.png)

    ![Łączenie z bazą danych](./media/contoso-migration-rehost-linux-vm-mysql/db-connect2.png)

2. Aktualizują ustawienia tak, aby maszyna wirtualna **OSTICKETWEB** mogła komunikować się z bazą danych **OSTICKETMYSQL**. Obecnie w konfiguracji jest na stałe zapisany lokalny adres IP 172.16.0.43.

    **Przed aktualizacją:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip1.png)

    **Po aktualizacji:**

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip2.png)

    ![Aktualizowanie adresu IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip3.png)

3. Ponownie uruchamiają usługę za pomocą polecenia **systemctl restart apache2**.

    ![Ponowne uruchamianie](./media/contoso-migration-rehost-linux-vm-mysql/restart.png)

4. Na koniec aktualizują rekordy DNS dla maszyny wirtualnej **OSTICKETWEB** na jednym z kontrolerów domeny firmy Contoso.

    ![Aktualizowanie rekordów DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji warstwy aplikacji osTicket działają na maszynach wirtualnych platformy Azure.

Teraz firma Contoso musi wykonać następujące czynności:

- Usunięcie maszyn wirtualnych VMware ze spisu programu vCenter.
- Usunięcie lokalnych maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie wewnętrznej dokumentacji tak, aby wskazywała nowe lokalizacje i adresy IP.
- Przegląd wszystkich zasobów korzystających z lokalnych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Firma Contoso skorzystała z usługi Azure Migrate z mapowaniem zależności do przeprowadzenia oceny maszyny wirtualnej **OSTICKETWEB** pod kątem migracji. Powinni teraz usunąć agentów (Microsoft Monitoring Agent i Microsoft Dependency Agent) zainstalowanych w tym celu z poziomu maszyny wirtualnej.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po uruchomieniu aplikacji firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Zabezpieczenia

Zespół ds. zabezpieczeń firmy Contoso sprawdza maszynę wirtualną i bazę danych, aby określić problemy z zabezpieczeniami.

- Administratorzy przeglądają sieciowe grupy zabezpieczeń używane do kontroli dostępu do maszyny wirtualnej. Sieciowe grupy zabezpieczeń zapewniają, że do aplikacji będzie przekazywany tylko dozwolony ruch.
- Rozważają również zabezpieczenie danych na dyskach maszyn wirtualnych przy użyciu usług Disk Encryption i Azure Key Vault.
- Nie skonfigurowano komunikacji między maszyną wirtualną a wystąpieniem bazy danych z użyciem protokołu SSL. Trzeba to zrobić, aby upewnić się, że hakerzy nie mogą zaatakować bazy danych.

Aby uzyskać więcej informacji, zobacz [najlepsze rozwiązania w zakresie zabezpieczeń dotyczące obciążeń IaaS na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/iaas).

### <a name="bcdr"></a>Zapewnienie ciągłości działania i odzyskiwanie po awarii

W celu zapewnienia ciągłości działania i odzyskiwania po awarii firma Contoso podejmuje następujące działania:

- **Zapewnienie bezpieczeństwa danych.** Firma Contoso tworzy kopie zapasowe danych na maszynie wirtualnej aplikacji za pomocą usługi Azure Backup. [Dowiedz się więcej](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nie trzeba konfigurować kopii zapasowej bazy danych. Usługa Azure Database for MySQL automatycznie tworzy kopie zapasowe i magazyny serwerów. Wybrano opcję użycia nadmiarowości geograficznej bazy danych, aby była odporna na awarie i gotowa do produkcji.
- **Zapewnienie ciągłości działania aplikacji.** Firma Contoso replikuje maszyny wirtualne aplikacji w regionie pomocniczym platformy Azure za pomocą usługi Site Recovery. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Po wdrożeniu zasobów firma Contoso przypisuje tagi platformy Azure zgodnie z decyzjami podjętymi na etapie wdrażania [infrastruktury platformy Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- Nie ma problemów z licencjonowaniem dla wdrożenia serwerów Contoso Ubuntu.
- Firma Contoso włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) o usłudze Azure Cost Management.
