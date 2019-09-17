---
title: Refaktoryzowanie aplikacji do obsługi pomocy technicznej systemu Linux pod kątem usług Azure App Service i Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, w jaki sposób firma Contoso refaktoryzuje lokalną aplikację systemu Linux przez migrowanie jej do usługi Azure App Service przy użyciu usługi GitHub dla warstwy internetowej i usługi Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e504d4032fc019af43ec7cb1e8513504196559a2
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024211"
---
# <a name="refactor-a-linux-app-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Refaktoryzowanie aplikacji systemu Linux do wielu regionów za pomocą usług Azure App Service, Traffic Manager i Azure Database for MySQL

W tym artykule pokazano, w jaki sposób fikcyjna firma Contoso refaktoryzuje dwuwarstwową aplikację PHP Apache MySQL opartą na systemie Linux (LAMP), która migruje ją ze środowiska lokalnego na platformę Azure przy użyciu integracji usług Azure App Service oraz GitHub i usługi Azure Database for MySQL.

Używana w tym przykładzie aplikacja do obsługi pomocy technicznej, osTicket, jest dostępna jako aplikacja open source. Jeśli chcesz użyć jej do własnych celów testowych, możesz pobrać ją z witryny [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się i przenosi na nowe rynki. Potrzebuje więc dodatkowych agentów obsługi klienta.
- **Skalowalność.** Rozwiązanie należy skompilować tak, aby firma Contoso mogła dodawać kolejnych agentów obsługi klienta w miarę rozwoju firmy.
- **Zwiększanie odporności.**  W przeszłości problemy z systemem dotyczyły tylko użytkowników wewnętrznych. Dzięki nowemu modelowi biznesowemu wpłynie to na użytkowników zewnętrznych, a firma Contoso wymaga, aby aplikacja działała przez cały czas.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury w firmie Contoso określił cele migracji, aby wybrać najlepszą metodę migracji:

- Aplikacja powinna skalować poza bieżącą lokalną pojemność i wydajność. Firma Contoso przenosi aplikację, aby wykorzystać możliwości skalowania na żądanie na platformie Azure.
- Firma Contoso chce przenieść bazę kodu aplikacji do potoku ciągłego dostarczania. Ponieważ zmiany aplikacji są wypychane do usługi GitHub, firma Contoso chce wdrażać te zmiany bez wykonywania zadań dla pracowników operacyjnych.
- Aplikacja musi być odporna oraz oferować możliwości wzrostu i przechodzenia w tryb failover. Firma Contoso chce wdrożyć aplikację w dwóch różnych regionach platformy Azure i skonfigurować ją do skalowania automatycznego.
- Firma Contoso chce zminimalizować zadania administratora bazy danych po przeniesieniu aplikacji do chmury.

## <a name="solution-design"></a>Projekt rozwiązania

Po określeniu swoich celów i wymagań firma Contoso planuje i ocenia rozwiązanie do wdrożenia oraz ustala proces migracji, w tym usługi platformy Azure, które będą używane do tego celu.

## <a name="current-architecture"></a>Bieżąca architektura

- Ta aplikacja działa na dwóch maszynach wirtualnych (OSTICKETWEB i OSTICKETMYSQL).
- Maszyny wirtualne znajdują się na hoście VMware ESXi **contosohost1.contoso.com** (wersja 6.5).
- Środowisko VMware jest zarządzane przez program vCenter Server 6.5 (**vcenter.contoso.com**) uruchomiony na maszynie wirtualnej.
- Firma Contoso ma lokalne centrum danych (contoso-datacenter) i lokalny kontroler domeny (**contosodc1**).

![Bieżąca architektura](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Proponowana architektura

Oto proponowana architektura:

- Aplikacja warstwy internetowej w systemie OSTICKETWEB będzie migrowana przez skompilowanie usługi Azure App Service w dwóch regionach platformy Azure. Usługa Azure App Service dla systemu Linux zostanie zaimplementowana przy użyciu kontenera Docker w języku PHP 7.0.
- Kod aplikacji zostanie przeniesiony do usługi GitHub, a aplikacja internetowa Azure App Service zostanie skonfigurowana do ciągłego dostarczania za pomocą usługi GitHub.
- Serwery aplikacji platformy Azure zostaną wdrożone zarówno w regionie podstawowym (Wschodnie stany USA 2), jak i dodatkowym (Środkowe stany USA).
- Usługa Traffic Manager zostanie skonfigurowana przed dwoma aplikacjami internetowymi w obydwu regionach.
- Usługa Traffic Manager zostanie skonfigurowana w trybie priorytetu, aby wymusić ruch przez region Wschodnie stany USA 2.
- Jeśli serwer aplikacji platformy Azure w regionie Wschodnie stany USA 2 przejdzie w tryb offline, użytkownicy będą mogli uzyskać dostęp do aplikacji w trybie failover w regionie Środkowe stany USA.
- Baza danych aplikacji będzie migrowana do usługi Azure Database for MySQL przy użyciu narzędzi rozwiązania MySQL Workbench. Kopia zapasowa lokalnej bazy danych zostanie utworzona lokalnie, a lokalna baza danych zostanie przywrócona bezpośrednio do usługi Azure Database for MySQL.
- Baza danych będzie znajdować się w regionie podstawowym Wschodnie stany USA 2 w podsieci bazy danych (PROD-DB-EUS2) w sieci produkcyjnej (VNET-PROD-EUS2):
- Ponieważ migracja dotyczy obciążenia produkcyjnego, zasoby platformy Azure dla aplikacji będą znajdować się w grupie zasobów produkcyjnych **ContosoRG**.
- Zasób usługi Traffic Manager zostanie wdrożony w grupie zasobów infrastruktury firmy Contoso **ContosoInfraRG**.
- Lokalne maszyny wirtualne w centrum danych firmy Contoso zostaną zlikwidowane po zakończeniu migracji.

![Architektura scenariusza](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi proces migracji w następujący sposób:

1. W pierwszym kroku administratorzy firmy Contoso konfigurują infrastrukturę platformy Azure, w tym funkcje, takie jak aprowizowanie usługi Azure App Service, konfigurowanie usługi Traffic Manager i aprowizowanie wystąpienia usługi Azure Datbase for MySQL.
2. Po przygotowaniu platformy Azure migrują oni bazę danych za pomocą rozwiązania MySQL Workbench.
3. Gdy baza danych będzie działać na platformie Azure, uruchomią oni prywatne repozytorium usługi GitHub na potrzeby usługi Azure App Service z ciągłym dostarczaniem i załadują je za pomocą aplikacji osTicket.
4. W witrynie Azure Portal administratorzy załadują aplikację z usługi GitHub do kontenera Docker z usługą Azure App Service.
5. Zmodyfikują też ustawienia systemu DNS i skonfigurują skalowanie automatyczne dla aplikacji.

![Proces migracji](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Usługi Azure

**Usługa** | **Opis** | **Koszty**
--- | --- | ---
[Usługa Azure App Service](https://azure.microsoft.com/services/app-service) | Usługa uruchamia i skaluje aplikacje za pomocą usługi Azure PaaS dla witryn internetowych. | Ceny są ustalane na podstawie rozmiaru wystąpień oraz wymaganych funkcji. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/app-service/windows).
[Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Moduł równoważenia obciążenia używający systemu DNS do kierowania użytkowników do platformy Azure lub zewnętrznych usług i witryn internetowych. | Cennik jest ustalany na podstawie liczby odebranych zapytań DNS oraz liczby monitorowanych punktów końcowych. | [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/traffic-manager).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | Baza danych opiera się na aparacie serwera MySQL typu open-source. Udostępnia ona w pełni zarządzaną, gotową do używania w przedsiębiorstwie bazę danych MySQL w wersji Community jako usługę do opracowywania i wdrażania aplikacji. | Cennik oparty na wymaganiach dotyczących obliczeń, magazynu i kopii zapasowych. [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/mysql).

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do realizacji tego scenariusza.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Szczegóły**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje wcześniej w tej serii artykułów. Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Infrastruktura platformy Azure wymagana do migracji](./contoso-migration-infrastructure.md).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Aprowizowanie usługi Azure App Service.** Administratorzy firmy Contoso będą aprowizować aplikacje internetowe w regionach podstawowym i pomocniczym.
> - **Krok 2. Konfigurowanie usługi Traffic Manager.** Konfigurują oni usługę Traffic Manager przed aplikacjami internetowymi na potrzeby ruchu routingu i równoważenia obciążenia.
> - **Krok 3. Aprowizowanie systemu MySQL.** Na platformie Azure aprowizują oni wystąpienie usługi Azure Database for MySQL.
> - **Krok 4. Migrowanie bazy danych.** Migrują oni bazę danych za pomocą rozwiązania MySQL Workbench.
> - **Krok 5. Konfigurowanie usługi GitHub.** Konfigurują oni lokalne repozytorium GitHub dla witryn internetowych/kodu aplikacji.
> - **Krok 6. Wdrażanie aplikacji internetowych.** Wdrażają oni aplikacje internetowe z usługi GitHub.

## <a name="step-1-provision-azure-app-service"></a>Krok 1: Aprowizowanie usługi Azure App Service

Administratorzy firmy Contoso aprowizują obsługę dwóch aplikacji internetowych (po jednej w każdym regionie) przy użyciu usługi Azure App Service.

1. Tworzą zasób aplikacji internetowej w regionie podstawowym Wschodnie stany USA 2 (**osticket-eus2**) w witrynie Azure Marketplace.
2. Umieszczają zasób w produkcyjnej grupie zasobów **ContosoRG**.

    ![Aplikacja platformy Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Tworzą nowy plan App Service w regionie podstawowym (**APP-SVP-EUS2**) przy użyciu rozmiaru standardowego.

     ![Aplikacja platformy Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Wybierają system operacyjny Linux z stosem środowiska uruchomieniowego PHP 7.0, który jest kontenerem platformy Docker.

    ![Aplikacja platformy Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Tworzą drugą aplikację internetową (**osticket-cus**) i plan usługi App Service dla regionu Środkowe stany USA.

    ![Aplikacja platformy Azure](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**Potrzebujesz dalszej pomocy?**

- Dowiedz się więcej o [aplikacjach internetowych usługi Azure App Service](https://docs.microsoft.com/azure/app-service/overview).
- Dowiedz się więcej o [usłudze Azure App Service dla systemu Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Krok 2: Konfigurowanie usługi Traffic Manager

Administratorzy firmy Contoso konfigurują usługę Traffic Manager tak, aby kierowała przychodzące żądania internetowe do aplikacji internetowych działających w warstwie internetowej aplikacji osTicket.

1. Tworzą zasób usługi Traffic Manager (**osticket.trafficmanager.net**) w witrynie Azure Marketplace. Używają routingu priorytetowego, aby region Wschodnie stany USA 2 był lokacją główną. Umieszczają zasób w grupie zasobów infrastruktury (**ContosoInfraRG**). Zauważ, że usługa Traffic Manager jest globalna i nie jest powiązana z określoną lokalizacją.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Teraz konfigurują usługę Traffic Manager za pomocą punktów końcowych. Dodają aplikację internetową Wschodnie stany USA 2 jako lokację główną (**osticket-eus2**) i aplikację Środkowe stany USA jako lokację dodatkową (**osticket-cus**).

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Po dodaniu punktów końcowych administratorzy mogą je monitorować.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**Potrzebujesz dalszej pomocy?**

- Dowiedz się więcej o usłudze [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Dowiedz się więcej o [kierowaniu ruchu do priorytetowego punktu końcowego](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Krok 3: Aprowizowanie usługi Azure Database for MySQL

Administratorzy firmy Contoso aprowizują wystąpienie bazy danych MySQL w regionie podstawowym Wschodnie stany USA 2.

1. W witrynie Azure Portal tworzą zasób usługi Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Dodają nazwę **contosoosticket** dla usługi bazy danych platformy Azure. Dodają bazę danych do grupy zasobów produkcyjnych **ContosoRG** i określają jej poświadczenia.
3. Wersja lokalnej bazy danych MySQL to 5.7, dlatego wybierają tę wersję w celu zachowania zgodności. Używają rozmiarów domyślnych, które spełniają wymagania dotyczące bazy danych.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. W obszarze **Opcje nadmiarowości kopii zapasowej** wybierają pozycję **Geograficznie nadmiarowe**. Ta opcja umożliwia przywrócenie bazy danych w regionie dodatkowym Środkowe stany USA w przypadku wystąpienia awarii. Tę opcję można skonfigurować tylko podczas aprowizowania bazy danych.

    ![Nadmiarowość](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Konfigurują zabezpieczenia połączeń. W bazie danych w obszarze **Zabezpieczenia połączeń** konfigurują reguły zapory, aby umożliwić bazie danych dostęp do usług platformy Azure.

6. Dodają adres IP klienta lokalnej stacji roboczej do początkowego i końcowego adresu IP. Dzięki temu aplikacje internetowe mogą uzyskiwać dostęp do bazy danych MySQL razem z klientem bazy danych, który przeprowadza migrację.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Krok 4: Migrowanie bazy danych

Administratorzy firmy Contoso migrują bazę danych przy użyciu funkcji tworzenia kopii zapasowych i przywracania za pomocą narzędzi MySQL. Instalują aplikację MySQL Workbench, tworzą kopię zapasową bazy danych z maszyny wirtualnej OSTICKETMYSQL, a następnie przywracają ją na serwer usługi Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Zainstaluj program MySQL Workbench

1. Sprawdzają [wymagania wstępne i pliki do pobrania aplikacji MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Instalują program MySQL Workbench dla systemu Windows zgodnie [z instrukcjami instalacji](https://dev.mysql.com/doc/workbench/en/wb-installing.html). Maszyna, na której jest on instalowany, musi być dostępna dla maszyny wirtualnej OSTICKETMYSQL i platformy Azure za pośrednictwem Internetu.
3. W programie MySQL Workbench tworzą połączenie usługi MySQL z maszyną OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Eksportują bazę danych **osticket** do samodzielnego pliku lokalnego.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Po utworzeniu lokalnej kopii zapasowej bazy danych tworzą połączenie z wystąpieniem usługi Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Teraz mogą zaimportować (przywrócić) bazę danych w wystąpieniu usługi Azure Database for MySQL z utworzonego samodzielnego pliku. Dla wystąpienia zostanie utworzony nowy schemat (osticket).

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Po przywróceniu danych można tworzyć dotyczące ich zapytania przy użyciu programu Workbench. Dane te będą również wyświetlane w witrynie Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Na koniec muszą zaktualizować informacje o bazie danych w aplikacjach internetowych. W wystąpieniu usługi MySQL otwierają obszar **Parametry połączenia**.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. Na liście parametrów znajdują ustawienia aplikacji internetowej i wybierają opcję ich kopiowania.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Otwierają okno Notatnika i wklejają ciąg do nowego pliku, a następnie aktualizują go w celu dopasowania do ustawień bazy danych osticket, wystąpienia usługi MySQL i poświadczeń.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. Mogą sprawdzić nazwę serwera i dane logowania w obszarze **Omówienie** wystąpienia usługi MySQL w witrynie Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Krok 5. Konfigurowanie usługi GitHub

Administratorzy firmy Contoso tworzą nowe prywatne repozytorium GitHub i konfigurują połączenie z bazą danych osTicket w usłudze Azure Database for MySQL. Następnie ładują aplikację internetową do usługi Azure App Service.

1. Przechodzą do publicznego repozytorium usługi GitHub oprogramowania OsTicket oraz tworzą jego rozwidlenie na koncie usługi GitHub firmy Contoso.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Po utworzeniu rozwidlenia przechodzą do folderu **include** i wyszukują plik **ost-config.php**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Plik jest otwarty w przeglądarce, a administratorzy go edytują.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. W edytorze aktualizują szczegóły bazy danych, w szczególności elementy **DBHOST** i **DBUSER**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Następnie zatwierdzają zmiany.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Dla każdej aplikacji internetowej (**osticket-eus2** i **osticket-cus**) modyfikują **ustawienia aplikacji** w witrynie Azure Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Wprowadzają parametry połączenia o nazwie **osticket** i kopiują je z Notatnika do **obszaru wartości**. Wybierają opcję **MySQL** na liście rozwijanej obok parametrów i zapisują ustawienia.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Krok 6: Konfigurowanie aplikacji internetowych

W ostatnim kroku procesu migracji administratorzy firmy Contoso konfigurują aplikacje internetowe za pomocą witryn internetowych osTicket.

1. W podstawowej aplikacji internetowej (**osticket-eus2**) otwierają **opcję wdrażania** i ustawiają źródło na **GitHub**.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Wybierają opcje wdrażania.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Po ustawieniu opcji konfiguracja zostanie wyświetlona jako oczekująca w witrynie Azure Portal.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Po zaktualizowaniu konfiguracji i załadowaniu aplikacji internetowej osTicket z usługi GitHub do kontenera Docker, na którym działa usługa Azure App Service, lokacja zostanie wyświetlona jako aktywna.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Powtarzają powyższe kroki dla pomocniczej aplikacji internetowej (**osticket-cus**).
6. Po skonfigurowaniu lokacji będzie ona dostępna za pośrednictwem profilu usługi Traffic Manager. Nazwa DNS to nowa lokalizacja aplikacji osTicket. [Dowiedz się więcej](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Firma Contoso chce mieć łatwą do zapamiętania nazwę DNS. Tworzą oni rekord aliasu (CNAME) **osticket.contoso.com**, który wskazuje na nazwę usługi Traffic Manager w systemie DNS na kontrolerach domeny.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Konfigurują aplikacje internetowe **osticket-eus2** i **osticket-cus**, aby zezwalać na niestandardowe nazwy hostów.

    ![Konfigurowanie aplikacji](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Konfigurowanie skalowania automatycznego

Na koniec ustawiają automatyczne skalowanie dla aplikacji. Dzięki temu, gdy agenci będą korzystać z aplikacji, wystąpienia aplikacji będą zwiększane i zmniejszane zgodnie z potrzebami biznesowymi.

1. W usłudze App Service **App-SRV-EUS2** otwierają **jednostkę skalowania**.
2. Konfigurują nowe ustawienie automatycznego skalowania z pojedynczą regułą, która zwiększa liczbę wystąpień o jeden, gdy wartość procentowa procesora dla bieżącego wystąpienia wynosi powyżej 70% przez 10 minut.

    ![Automatyczne skalowanie](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Konfigurują to samo ustawienie w usłudze **APP-SRV-CUS**, aby upewnić się, że takie zachowanie będzie stosowane w przypadku przełączenia aplikacji w tryb failover do regionu pomocniczego. Jedyną różnicą jest to, że ustawiają domyślne wystąpienie na 1, ponieważ dotyczy to tylko trybu failover.

   ![Automatyczne skalowanie](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji aplikacja osTicket jest refaktoryzowana w celu uruchamiania w aplikacji internetowej Azure App Service z ciągłym dostarczaniem przy użyciu prywatnego repozytorium GitHub. Aplikacja działa w dwóch regionach w celu zwiększenia odporności. Baza danych osTicket jest uruchamiana w usłudze Azure Database for MySQL po migracji na platformę usługi PaaS.

W celu oczyszczenia zasobów firma Contoso musi wykonać następujące czynności:

- Usunięcie maszyn wirtualnych VMware ze spisu programu vCenter.
- Usunięcie lokalnych maszyn wirtualnych z lokalnych zadań kopii zapasowej.
- Zaktualizowanie wewnętrznej dokumentacji tak, aby wskazywała nowe lokalizacje i adresy IP.
- Przegląd wszystkich zasobów korzystających z lokalnych maszyn wirtualnych i zaktualizowanie wszystkich ustawień lub dokumentów w celu uwzględnienia nowej konfiguracji.
- Ponowne skonfigurowanie monitorowania, aby wskazywało na adres URL osticket-trafficmanager.net, w celu sprawdzania, czy aplikacja została uruchomiona i działa.

## <a name="review-the-deployment"></a>Przegląd wdrożenia

Po uruchomieniu aplikacji firma Contoso musi w pełni zoperacjonalizować i zabezpieczyć nową infrastrukturę.

### <a name="security"></a>Bezpieczeństwo

Zespół ds. zabezpieczeń firmy Contoso sprawdził aplikację, aby określić problemy z zabezpieczeniami. Stwierdzono, że komunikacja między aplikacją osTicket i wystąpieniem bazy danych MySQL nie została skonfigurowana pod kątem protokołu SSL. Trzeba to zrobić, aby upewnić się, że hakerzy nie mogą zaatakować bazy danych. [Dowiedz się więcej](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).

### <a name="backups"></a>Tworzenie kopii zapasowych

- Aplikacje internetowe osTicket nie zawierają danych stanu, więc nie trzeba tworzyć kopii zapasowej.
- Nie trzeba konfigurować kopii zapasowej bazy danych. Usługa Azure Database for MySQL automatycznie tworzy kopie zapasowe i magazyny serwerów. Wybrano opcję użycia nadmiarowości geograficznej bazy danych, aby była odporna na awarie i gotowa do produkcji. Kopie zapasowe mogą być używane do przywracania serwera do punktu w czasie. [Dowiedz się więcej](https://docs.microsoft.com/azure/mysql/concepts-backup).

### <a name="licensing-and-cost-optimization"></a>Licencjonowanie i optymalizacja kosztów

- Brak problemów z licencjonowaniem dla wdrożenia PaaS.
- Firma Contoso włączy usługę Azure Cost Management licencjonowaną przez firmę Cloudyn, podmiot zależny firmy Microsoft. Jest to rozwiązanie do zarządzania kosztami wielu chmur, które ułatwia korzystanie z platformy Azure i innych zasobów w chmurze oraz zarządzanie nimi. [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.
