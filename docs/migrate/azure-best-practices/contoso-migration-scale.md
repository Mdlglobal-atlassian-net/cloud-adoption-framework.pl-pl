---
title: Skalowanie migracji na platformę Azure
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak zaplanować i przeprowadzić migrację do platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 8c3ee0a75efa74aa1599399358bac267c5ffe1de
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091923"
---
# <a name="scale-a-migration-to-azure"></a>Skalowanie migracji na platformę Azure

W tym artykule przedstawiono sposób, w jaki fikcyjna firma Contoso przeprowadza migrację na platformę Azure na dużą skalę. Firma rozważa, jak zaplanować i przeprowadzić migrację ponad 3000 obciążeń, 8000 baz danych i ponad 10 000 maszyn wirtualnych.

## <a name="business-drivers"></a>Cele biznesowe

Zespół liderów IT w ścisłej współpracy z partnerami biznesowymi firmy ustalił, co firma będzie chciała osiągnąć dzięki migracji:

- **Reagowanie na rosnące potrzeby biznesowe.** Firma Contoso rozwija się, co powoduje przeciążenie lokalnych systemów i infrastruktury.
- **Zwiększenie wydajności.** Firma Contoso chce usunąć niepotrzebne procedury oraz usprawnić procesy deweloperów i użytkowników. Firma chce, aby dział IT był szybki i nie tracił czasu ani pieniędzy, co pozwoli szybciej realizować wymagania klientów.
- **Zwiększenie elastyczności.** Firma Contoso chce lepiej odpowiadać na zapotrzebowania w branży. Musi być w stanie reagować szybciej na zmiany na rynku, aby odnosić sukcesy w gospodarce światowej. Nie może utrudniać pracy ani stać się przeszkodą biznesową.
- **Skalowalność.** W miarę rozwoju firmy Contoso jej dział IT musi zapewnić systemy, które będą mogły rosnąć w tym samym tempie.
- **Udoskonalenie modeli kosztów.** Firma Contoso chce zmniejszyć wymagania inwestycyjne w budżecie IT. Firma Contoso chce wykorzystać zdolność chmury do skalowania i zmniejszenia zapotrzebowania na drogi sprzęt.
- **Obniżenie kosztów licencjonowania.** Firma Contoso chce zminimalizować koszty chmury.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele tej migracji. Na podstawie tych celów określono najlepszą metodę migracji.

**Wymagania** | **Szczegóły**
--- | ---
**Szybkie przejście na platformę Azure** | Firma Contoso chce jak najszybciej zacząć przenosić aplikacje i maszyny wirtualne na platformę Azure.
**Pełna inwentaryzacja** | Firma Contoso potrzebuje kompletnego spisu wszystkich aplikacji, baz danych i maszyn wirtualnych w organizacji.
**Ocenianie i klasyfikowanie aplikacji** | Firma Contoso chce w pełni korzystać z chmury. Domyślnie firma Contoso zakłada, że wszystkie usługi będą działały jako PaaS. Opcja IaaS zostanie użyta, jeśli opcja PaaS nie będzie odpowiednia.
**Szkolenia i przechodzenie do DevOps** | Firma Contoso chce przejść do modelu DevOps. Firma Contoso zapewni szkolenia dotyczące platformy Azure i DevOps oraz zreorganizuje zespoły w razie potrzeby.

Po ustaleniu zamierzonych celów i wymagań firma Contoso przegląda zużycie zasobów IT i identyfikuje proces migracji.

## <a name="current-deployment"></a>Bieżące wdrożenie

Po zaplanowaniu i skonfigurowaniu [infrastruktury platformy Azure](./contoso-migration-infrastructure.md) i wypróbowaniu różnych kombinacji migracji w celu weryfikacji koncepcji zgodnie z opisem w powyższej tabeli firma Contoso jest gotowa do przystąpienia do pełnej migracji na platformę Azure na dużą skalę. Firma Contoso chce przeprowadzić migrację następujących elementów.

<!--markdownlint-disable MD033 -->

**Element** | **Wielkość** | **Szczegóły**
--- | --- | ---
**Obciążenia** | Ponad 3000 aplikacji | Aplikacje działają na maszynach wirtualnych.<br/><br/>  Aplikacje działają w technologiach Windows, SQL i OSS LAMP.
**Bazy danych** | Około 8500 | Bazy danych obejmują SQL Server, MySQL, PostgreSQL.
**Maszyny wirtualne** | Ponad 35 000 | Maszyny wirtualne działają na hostach VMware i zarządzane przez serwery vCenter.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Proces migracji

Teraz, gdy firma Contoso ustaliła czynniki biznesowe i cele migracji, określa czterotorowe podejście do procesu migracji:

- **Faza 1: Ocena.** Wykrycie bieżących zasobów i sprawdzenie są one odpowiednie do migracji na platformę Azure.
- **Faza 2: Migrowanie.** Przeniesienie zasobów na platformę Azure. Sposób przenoszenia aplikacji i obiektów na platformę Azure będzie zależeć od aplikacji i zamierzonych celów.
- **Faza 3: Optymalizacja.** Po przeniesieniu zasobów na platformę Azure firma Contoso potrzebuje ulepszyć i usprawnić je w celu zapewnienia maksymalnej wydajności i efektywności.
- **Faza 4: bezpieczna i zarządzana.** Kiedy wszystko jest na swoim miejscu, firma Contoso korzysta teraz z zasobów i usług do zabezpieczania i zarządzania platformy Azure w celu utrzymania ładu, zabezpieczenia i monitorowania swoich aplikacji w chmurze na platformie Azure.

Realizacja etapów nie przebiega seryjnie w organizacji. Każdy element projektu migracji firmy Contoso będzie na innym etapie procesu oceny i migracji. Optymalizacja, zabezpieczenia i zarządzanie będą realizowane w miarę upływu czasu.

## <a name="phase-1-assess"></a>Faza 1: Ocena

Firma Contoso zaczyna proces od wykrywania i oceny lokalnych aplikacji, danych i infrastruktury. Oto, co firma Contoso wykona:

- Firma Contoso potrzebuje odnaleźć aplikacje, mapować zależności między aplikacjami i decydować o kolejności i priorytecie migracji.
- Podczas oceniania firma Contoso będzie budować całościowy spis aplikacji i zasobów. Wraz z nowym spisem firma Contoso będzie używać istniejącej bazy danych zarządzania konfiguracją (CMDB) oraz katalogu usług i zaktualizuje ich zawartość.
  - Baza danych CMDB zawiera konfiguracje techniczne aplikacji firmy Contoso.
  - Katalog usług umożliwia dokumentowanie szczegółów operacyjnych aplikacji, w tym skojarzonych partnerów biznesowych i umów dotyczących poziomu usług (umów SLA).

### <a name="discover-apps"></a>Odnajdywanie aplikacji

Firma Contoso ma tysiące aplikacji działających na wielu serwerach. Oprócz bazy danych CMDB i katalogu usług firma Contoso potrzebuje narzędzi do odnajdywania i oceny.

- Narzędzia muszą zapewniać mechanizm, który może wprowadzać dane oceny do procesu migracji.
- Narzędzia służące do oceny muszą udostępniać dane, które ułatwiają tworzenie inteligentnego spisu zasobów fizycznych i wirtualnych firmy Contoso. Dane powinny zawierać informacje o profilu i metryki wydajności.
- Po ukończeniu odnajdywania firma Contoso powinna mieć pełny spis zasobów i skojarzonych z nimi metadanych. Ten spis będzie używany do definiowania planu migracji.

### <a name="identify-classifications"></a>Identyfikacja klasyfikacji

Firma Contoso identyfikuje kilka typowych kategorii do klasyfikacji zasobów w spisie. Te klasyfikacje mają kluczowe znaczenie dla podejmowania decyzji firmy Contoso na potrzeby migracji. Lista klasyfikacji pomaga określić priorytety migracji i zidentyfikować złożone problemy.

**Kategoria** | **Przypisana wartość** | **Szczegóły**
--- | --- | ---
Grupa biznesowa | Lista nazw grup biznesowych | Która grupa jest odpowiedzialna za element spisu?
Kandydat do weryfikacji koncepcji | T/N | Czy aplikacja może być używana do weryfikacji koncepcji lub wczesnego przyjęcia migracji do chmury?
Dług techniczny | Brak/Pewien/Poważny | Czy element spisu uruchamia lub wykorzystuje nieobsługiwane produkty, platformy lub systemy operacyjne?
Konsekwencje dotyczące zapory | T/N | Czy aplikacja komunikuje się z ruchem internetowym/zewnętrznym?  Czy jest zintegrowana z zaporą?
Problemy z zabezpieczeniami | T/N | Czy istnieją znane problemy z zabezpieczeniami aplikacji?  Czy aplikacja używa nieszyfrowanych danych lub nieaktualnych platform?

### <a name="discover-app-dependencies"></a>Odkrywanie zależności aplikacji

W ramach procesu oceny firma Contoso potrzebuje określić, gdzie działają aplikacje oraz ustalić zależności i połączenia między serwerami aplikacji. Firma Contoso mapuje środowisko etapami.

1. W pierwszym kroku firma Contoso odkrywa, jak serwery i maszyny mapują się do poszczególnych aplikacji, lokalizacji sieciowych i grup.
2. Dzięki tym informacjom firma Contoso może jasno identyfikować aplikacje, które mają kilka zależności i są odpowiednie do szybkiej migracji.
3. Firma Contoso może użyć mapowania, aby ułatwić im zidentyfikowanie bardziej złożonych zależności i komunikacji między serwerami aplikacji. Firma Contoso może następnie zgrupować te serwery logicznie według reprezentowanych aplikacji i zaplanować strategię migracji na podstawie tych grup.

Po zakończeniu mapowania firma Contoso może zapewnić, że wszystkie składniki aplikacji są identyfikowane i uwzględniane podczas kompilowania planu migracji.

![Mapowanie zależności](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Szacowanie aplikacji

Jako ostatni krok w procesie odnajdywania i oceny firma Contoso może oszacować wyniki oceny i mapowania, aby dowiedzieć się, jak migrować każdą aplikację w katalogu usług.

W celu ujęcia tego procesu szacowania forma Contoso dodała do spisu kilka dodatkowych klasyfikacji.

**Kategoria** | **Przypisana wartość** | **Szczegóły**
--- | --- | ---
Grupa biznesowa | Lista nazw grup biznesowych | Która grupa jest odpowiedzialna za element spisu?
Kandydat do weryfikacji koncepcji | T/N | Czy aplikacja może być używana do weryfikacji koncepcji lub wczesnego przyjęcia migracji do chmury?
Dług techniczny | Brak/Pewien/Poważny | Czy element spisu uruchamia lub wykorzystuje nieobsługiwane produkty, platformy lub systemy operacyjne?
Konsekwencje dotyczące zapory | T/N | Czy aplikacja komunikuje się z ruchem internetowym/zewnętrznym?  Czy jest zintegrowana z zaporą?
Problemy z zabezpieczeniami | T/N | Czy istnieją znane problemy z zabezpieczeniami aplikacji?  Czy aplikacja używa nieszyfrowanych danych lub nieaktualnych platform?
Strategia migracji | Ponowne hostowanie/Refaktoryzacja/Zmiana architektury/Ponowna kompilacja | Jakiego rodzaju migracja jest potrzebna dla aplikacji? W jaki sposób aplikacja zostanie wdrożona na platformie Azure? [Dowiedz się więcej](./contoso-migration-overview.md#migration-patterns).
Złożoność techniczna | 1–5 | Jak złożona jest migracja? Ta wartość powinna być definiowana przez dział DevOps firmy Contoso i odpowiednich partnerów.
Znaczenie biznesowe | 1–5 | Jak ważna jest aplikacja dla firmy? Na przykład niewielka aplikacja grupy roboczej może uzyskać wynik 1, a krytyczna aplikacja używana w całej organizacji może uzyskać wynik 5. Ten wynik będzie miał wpływ na poziom priorytetu migracji.
Priorytet migracji | 1/2/3 | Jaki jest priorytet migracji aplikacji?
Ryzyko migracji | 1–5 | Jaki jest poziom ryzyka migracji aplikacji? Ta wartość powinna być uzgodniona przez dział DevOps firmy Contoso i odpowiednich partnerów.

### <a name="figure-out-costs"></a>Ustalanie kosztów

Aby ustalić koszty i potencjalne oszczędności związane z migracją na platformę Azure, firma Contoso może użyć [kalkulatora całkowitego kosztu posiadania (TCO)](https://azure.microsoft.com/pricing/tco/calculator), aby obliczyć i porównać koszt TCO platformy Azure z porównywalnym wdrożeniem lokalnym.

### <a name="identify-assessment-tools"></a>Identyfikowanie narzędzi oceny

Firma Contoso decyduje, którego narzędzia użyć do odnajdywania, oceny i inwentaryzacji. Firma Contoso identyfikuje kombinację narzędzi i usług platformy Azure, natywnych narzędzi aplikacji i skryptów oraz narzędzi partnerskich. W szczególności firma Contoso jest zainteresowana tym, jak usługa Azure Migrate może posłużyć do oceny na dużą skalę.

#### <a name="azure-migrate"></a>Azure Migrate

Usługa Azure Migrate pomaga odnajdywać i oceniać lokalne maszyny wirtualne VMware podczas przygotowywania do migracji na platformę Azure. Poniżej przedstawiono działanie usługi Azure Migrate:

1. Odnajdywanie: odnajdywanie lokalnych maszyn wirtualnych VMware.
    - Usługa Azure Migrate obsługuje odnajdywanie z wielu serwerów vCenter (szeregowo) i może uruchamiać odnajdywanie w oddzielnych projektach Azure Migrate.
    - Usługa Azure Migrate przeprowadza odnajdywanie przy użyciu maszyny wirtualnej VMware z uruchomionym modułem zbierającym migracji. Ten sam moduł zbierający może odnajdywać maszyny wirtualne na różnych serwerach vCenter i wysyłać dane do różnych projektów.
2. Oceń gotowość: Oceń, czy maszyny lokalne są odpowiednie do działania na platformie Azure. Ocena obejmuje:
    - Zalecenia dotyczące rozmiaru: Uzyskaj zalecenia dotyczące rozmiarów maszyn wirtualnych platformy Azure na podstawie historii wydajności lokalnych maszyn wirtualnych.
    - Szacowane miesięczne koszty: Uzyskaj szacowane koszty uruchamiania maszyn lokalnych na platformie Azure.
3. Identyfikowanie zależności: Wizualizacja zależności maszyn lokalnych w celu utworzenia optymalnych grup komputerów na potrzeby oceny i migracji.

![Azure Migrate](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Migrowanie na dużą skalę

Firma Contoso musi prawidłowo korzystać z usługi Azure Migrate, uwzględniając skalę tej migracji.

- Firma Contoso przeprowadzi ocenę poszczególnych aplikacji przy użyciu usługi Azure Migrate. To zapewnia, że usługa Azure Migrate zwraca aktualne dane do witryny Azure Portal.
- Administratorzy firmy Contoso czytają informacje o [wdrażaniu Azure Migrate na dużą skalę](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment)
- Firma Contoso zauważa ograniczenia usługi Azure Migrate, które zostały podsumowane w poniższej tabeli.

**Akcja** | **Limit**
--- | ---
Tworzenie projektu w usłudze Azure Migrate | 10 000 maszyn wirtualnych
Odnajdywanie | 10 000 maszyn wirtualnych
Ocena | 10 000 maszyn wirtualnych

Firma Contoso użyje usługi Azure Migrate w następujący sposób:

- Firma Contoso zorganizuje maszyny wirtualne w folderach w programie vCenter. Dzięki temu będzie można łatwo skupić się podczas uruchamiania oceny na maszynach wirtualnych w określonym folderze.
- Usługa Azure Migrate używa rozwiązania Azure Service Map w celu oceny zależności między maszynami. Wymaga to zainstalowania agentów na maszynach wirtualnych do oceny.
  - Firma Contoso będzie używać zautomatyzowanych skryptów do instalowania wymaganych agentów systemu Windows lub Linux.
  - Dzięki skryptom firma Contoso może wypchnąć instalację do maszyn wirtualnych w folderze vCenter.

#### <a name="database-tools"></a>Narzędzia bazy danych

Jako uzupełnienie usługi Azure Migrate firma Contoso koncentruje się na korzystaniu z narzędzi przeznaczonych do oceny bazy danych. Narzędzia, takie jak [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017) ułatwią ocenę baz danych SQL Server do migracji.

Narzędzie Data Migration Assistant (DMA) może pomóc firmie Contoso ustalić, czy lokalne bazy danych są zgodne z zakresem rozwiązań bazodanowych platformy Azure, takich jak Azure SQL Database, program SQL Server działający na maszynie wirtualnej platformy Azure IaaS i wystąpienie zarządzane usługi Azure SQL.

Oprócz DMS firma Contoso ma inne skrypty, których używa do odnajdywania i dokumentowania baz danych SQL Server. Znajdują się one w repozytorium GitHub.

#### <a name="partner-assessment-tools"></a>Partnerskie narzędzia oceny

Istnieje kilka innych narzędzi partnerskich, które mogą pomóc firmie Contoso w ocenie środowiska lokalnego do migracji na platformę Azure. [Dowiedz się więcej](https://azure.microsoft.com/migration/partners) na temat partnerów migracji na platformę Azure.

## <a name="phase-2-migrate"></a>Faza 2: Migrowanie

Wraz z ukończeniem oceny firma Contoso musi identyfikować narzędzia służące do przenoszenia jej aplikacji, danych i infrastruktury na platformę Azure.

### <a name="migration-strategies"></a>Strategie migracji

Istnieją cztery szerokie strategie migracji, które firma Contoso może rozważyć.

<!--markdownlint-disable MD033 -->

**Strategia** | **Szczegóły** | **Użycie**
--- | --- | ---
**Ponowne hostowanie** | Jest to opcja bez kodu, która jest często określana jako przechodzenie _i_ przenoszenie do platformy Azure.<br/><br/> Aplikacje są jest migrowane bez zmian, co umożliwia wykorzystanie zalet chmury bez ryzyka i kosztów związanych z wprowadzaniem zmian w kodzie. | Firma Contoso może ponownie hostować mniej strategiczne aplikacje bez konieczności wprowadzania zmian w kodzie.
**Refaktoryzacja** | Ta strategia, określana również jako „ponowne pakowanie”, wymaga minimalnych zmian kodu lub konfiguracji aplikacji potrzebnych, aby połączyć aplikację z usługą Azure PaaS i zapewnić lepsze wykorzystanie możliwości chmury. | Firma Contoso może poddać refaktoryzacji aplikacje strategiczne, aby zachować tę samą podstawową funkcjonalność, ale przenieść ich działanie na platformę Azure, taką jak Azure App Service.<br/><br/> Wymaga to minimalnych zmian w kodzie.<br/><br/> Z drugiej strony firma Contoso będzie musiała zachować platformę maszyny wirtualnej, ponieważ nie będzie ona zarządzana przez firmę Microsoft.
**Zmiana architektury** | Ta strategia modyfikuje lub rozszerza bazę kodu aplikacji w celu optymalizacji architektury aplikacji na potrzeby możliwości i skalowania chmury.<br/><br/> Aplikacja jest modernizowana w celu zapewnienia odpornej, wysoce skalowalnej architektury z możliwością niezależnego wdrażania.<br/><br/> Usługi Azure pozwalają przyspieszyć ten proces, bezproblemowo skalować aplikacje i łatwo nimi zarządzać.
**Ponowna kompilacja** | Ta strategia polega na ponownym kompilowaniu aplikacji od podstaw, z wykorzystaniem natywnych technologii chmury.<br/><br/> Rozwiązanie PaaS platformy Azure zapewnia kompletne środowisko deweloperskie i środowisko wdrażania w chmurze. Eliminuje to pewne wydatki i złożoność licencji na oprogramowanie oraz eliminuje konieczność użycia podstawowej infrastruktury aplikacji, oprogramowania pośredniczącego i innych zasobów. | Firma Contoso może ponownie napisać kod najważniejszych aplikacji od podstaw, aby korzystać z technologii chmurowych, takich jak komputer bezserwerowy lub mikrousługi.<br/><br/> Firma Contoso będzie zarządzać aplikacją i usługami, które opracowuje, a platforma Azure zarządza wszystkim innym.

<!--markdownlint-enable MD033 -->

Należy również zastanowić się nad danymi, szczególnie w przypadku wielu baz danych posiadanych przez firmę Contoso. Podejście domyślne firmy Contoso polega na użyciu usług PaaS, takich jak Azure SQL Database, aby w pełni korzystać z funkcji chmury. Przenosząc bazy danych do usługi PaaS, firma Contoso będzie musiała tylko zachować dane, pozostawiając podstawową platformę firmie Microsoft.

### <a name="evaluate-migration-tools"></a>Narzędzia szacowania migracji

Firma Contoso korzysta głównie z kilku usług i narzędzi platformy Azure do migracji:

- [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): organizuje odzyskiwanie po awarii i migruje lokalne maszyny wirtualne na platformę Azure.
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview): migruje lokalne bazy danych, takie jak SQL Server, MySQL i Oracle do platformy Azure.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery to podstawowa usługa platformy Azure do organizowania odzyskiwania po awarii i migracji z platformy Azure oraz z lokacji lokalnych na platformę Azure.

1. Site Recovery umożliwia organizowanie replikacji z lokacji lokalnych na platformę Azure.
2. Po skonfigurowaniu i uruchomieniu replikacji maszyny lokalne można przełączać w tryb failover na platformę Azure, kończąc proces migracji.

Firma Contoso już [ukończyła weryfikację koncepcji](./contoso-migration-rehost-vm.md), aby zobaczyć, jak usługa Site Recovery może pomóc w migracji do chmury.

##### <a name="use-site-recovery-at-scale"></a>Użyj Site Recovery na dużą skalę

Firma Contoso planuje przeprowadzić migrację do wielu przesunięć i przesunięcia. W celu zapewnienia takiego działania usługa Site Recovery będzie przeprowadzać replikację partiami po około 100 maszyn wirtualnych jednocześnie. Aby ustalić, jak to będzie działać, firma Contoso potrzebuje przeprowadzić planowanie wydajności dla proponowanej migracji Site Recovery.

- Firma Contoso musi zebrać informacje o rozmiarach ruchu. W szczególności:
  - Firma Contoso musi określić częstotliwość zmian dla maszyn wirtualnych, które mają być replikowane.
  - Firma Contoso musi także wziąć pod uwagę łączność sieciową z lokacji lokalnej na platformę Azure.
- W odpowiedzi na wymagania dotyczące pojemności i ilości, firma Contoso będzie potrzebowała przydzielić odpowiednią przepustowość na podstawie dziennego współczynnika zmian danych dotyczących wymaganych maszyn wirtualnych, aby osiągnąć cel punktu odzyskiwania (RPO).
- Na koniec należy ustalić, ile serwerów jest potrzebnych do uruchamiania składników usługi Site Recovery, które są potrzebne do wdrożenia.

###### <a name="gather-on-premises-information"></a>Zbieranie informacji lokalnych

Firma Contoso może użyć narzędzia [Planista wdrażania usługi Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-deployment-planner), aby wykonać następujące czynności:

- Firma Contoso może używać narzędzia do zdalnego profilowania maszyn wirtualnych bez wpływu na środowisko produkcyjne. Ułatwia to ustalanie wymagań dotyczących przepustowości i pamięci masowej na potrzeby replikacji i trybu failover.
- Firma Contoso może uruchomić narzędzie bez instalowania składników usługi Site Recovery w środowisku lokalnym.
- Narzędzie zbiera informacje o zgodnych i niezgodnych maszynach wirtualnych, dyskach przypadających na maszynę wirtualną oraz współczynnikach zmian danych na poszczególnych dyskach. Ponadto identyfikuje wymagania dotyczące przepustowości sieci i infrastruktury platformy Azure potrzebnej do pomyślnej replikacji i przełączanie w tryb failover.
- Firma Contoso musi upewnić się, że narzędzie planisty jest następnie uruchamiane na komputerach z systemem Windows Server, które spełniają minimalne wymagania dotyczące serwera konfiguracji usługi Site Recovery. Serwer konfiguracji jest maszyną Site Recovery, która jest potrzebna do replikowania lokalnych maszyn wirtualnych VMware.

###### <a name="identify-site-recovery-requirements"></a>Identyfikowanie wymagań usługi Site Recovery

Oprócz replikowanych maszyn wirtualnych usługa Site Recovery wymaga kilku składników do migracji VMware.

<!--markdownlint-disable MD033 -->

**Składnik** | **Szczegóły**
--- | ---
**Serwer konfiguracji** | Zwykle maszyna wirtualna VMware skonfigurowana przy użyciu szablonu OVF.<br/><br/> Składnik serwera konfiguracji służy do koordynowania komunikacji między środowiskiem lokalnym i platformą Azure oraz do zarządzania replikacją danych.
**Serwer przetwarzania** | Domyślnie instalowany na serwerze konfiguracji.<br/><br/> Składnik serwera przetwarzania odbiera dane replikacji, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła je do magazynu Azure.<br/><br/> Serwer przetwarzania instaluje także usługę Azure Site Recovery Mobility Service na maszynach wirtualnych, które będą replikowane, i przeprowadza automatycznie odnajdywanie lokalnych maszyn wirtualnych.<br/><br/> Wdrożenia skalowane wymagają dodatkowych, autonomicznych serwerów przetwarzania w celu obsługi dużych ilości ruchu związanego z replikacją.
**Mobility Service** | Agent usługi Mobility Service jest instalowany na każdej maszynie wirtualnej VMware, która zostanie zmigrowana przy użyciu usługi Site Recovery.

<!--markdownlint-enable MD033 -->

Firma Contoso potrzebuje dowiedzieć się, jak wdrażać te składniki, na podstawie zagadnień związanych z pojemnością.

<!--markdownlint-disable MD033 -->

**Składnik** | **Wymagania pojemności**
--- | ---
**Maksymalny dzienny współczynnik zmian** | Pojedynczy serwer przetwarzania może obsłużyć dziennie do 2 TB zmian. Ponieważ maszyna wirtualna może korzystać tylko z jednego serwera przetwarzania, maksymalna szybkość dziennej zmiany danych obsługiwana dla zreplikowanej maszyny wirtualnej wynosi 2 TB.
**Maksymalna przepływność** | Standardowe konto usługi magazynu Azure może obsłużyć maksymalnie 20 000 żądań na sekundę, a liczba operacji wejścia/wyjścia na sekundę (IOPS) w ramach replikacji maszyny wirtualnej powinna mieścić się w tym limicie. Na przykład, jeśli maszyna wirtualna ma 5 dysków, a każdy dysk generuje 120 operacji we/wy na sekundę (rozmiar 8K) na maszynie wirtualnej, będzie się mieścić w limicie 500 operacji we/wy na sekundę na każdym dysku.<br/><br/> Należy pamiętać, że liczba potrzebnych kont magazynu jest równa łącznej liczbie operacji we/wy na sekundę na maszynie źródłowej, podzielonej przez 20 000. Replikowana maszyna może należeć tylko do jednego konta magazynu na platformie Azure.
**Serwer konfiguracji** | W oparciu o szacunkową łączną replikację 100 = 200 maszyn wirtualnych w firmie Contoso i [wymagania dotyczące ustalania wielkości serwera konfiguracji](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server) firma Contoso oszacowała, że potrzebuje następującej maszyny serwera konfiguracji:<br/><br/> Procesor: 16 procesorów wirtualnych vCPU (2 gniazda &#215; 8 rdzeni o 2,5 GHz)<br/><br/> Pamięć: 32 GB<br/><br/> Dysk pamięci podręcznej: 1 TB<br/><br/> Szybkość zmian danych: 1 TB do 2 TB.<br/><br/> Oprócz określania wymagań dotyczących rozmiarów firma Contoso potrzebuje upewnić się, że serwer konfiguracji jest optymalnie zlokalizowany, w tej samej sieci i segmencie LAN co maszyny wirtualne, które będą migrowane.
**Serwer przetwarzania** | Firma Contoso będzie wdrażać autonomiczny dedykowany serwer przetwarzania z możliwością replikowania 100–200 maszyn wirtualnych:<br/><br/> Procesor: 16 procesorów wirtualnych vCPU (2 gniazda &#215; 8 rdzeni o 2,5 GHz)<br/><br/> Pamięć: 32 GB<br/><br/> Dysk pamięci podręcznej: 1 TB<br/><br/> Szybkość zmian danych: 1 TB do 2 TB.<br/><br/> Serwer przetwarzania będzie działać intensywnie i dlatego powinien znajdować się na hoście ESXi, który może obsłużyć dyskowe operacje we/wy, ruch sieciowy i procesor wymagany do replikacji. Firma Contoso rozważy zastosowanie w tym celu dedykowanego hosta.
**Sieć** | Firma Contoso przejrzała bieżącą infrastrukturę międzylokacyjnej sieci VPN i zdecydowała się na wdrożenie usługi Azure ExpressRoute. Implementacja ma kluczowe znaczenie, ponieważ zmniejszy opóźnienie i zwiększy przepustowość do głównego regionu Azure firmy Contoso, czyli Wschodnie stany USA 2.<br/><br/> **Monitorowanie:** Firma Contoso będzie musiała starannie monitorować przepływ danych z serwera przetwarzania. Jeśli dane przeciążą przepustowość sieci, firma Contoso [rozważyć ograniczanie przepustowości serwera przetwarzania](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth).
**Azure Storage** | Firma Contoso musi określić odpowiedni typ i liczbę docelowych kont magazynu platformy Azure na potrzeby migracji. Usługa Site Recovery replikuje dane maszyn wirtualnych do magazynu Azure.<br/><br/> Usługa Site Recovery może przeprowadzać replikację do kont magazynu w warstwie Standardowa lub Premium (SSD).<br/><br/> W celu podjęcia decyzji na temat magazynu firma Contoso musi przejrzeć [limity przestrzeni dyskowej](https://docs.microsoft.com/azure/virtual-machines/windows/disks-types) i wziąć pod uwagę oczekiwany wzrost oraz zwiększone użycie w miarę upływu czasu. Mając na względzie szybkość i priorytet migracji, firma Contoso zdecydowała się korzystać z dysków SSD Premium.<br/><br/>
Firma Contoso podjęła decyzję o użyciu dysków zarządzanych dla wszystkich maszyn wirtualnych wdrożonych na platformie Azure. Wymagana liczba operacji we/wy decyduje o wyborze dysków HDD w warstwie Standardowa, SSD w warstwie Standardowa lub Premium (SSD).<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Usługa Azure Database Migration Service jest w pełni zarządzaną usługą, która umożliwia bezproblemową migrację z wielu źródeł baz danych na platformy danych Azure przy minimalnych przestojach.

- Usługa DMS integruje funkcjonalność istniejących narzędzi i usług. Wykorzystuje narzędzie Data Migration Assistant (DMA) do generowania raportów oceny, które określają zalecania dotyczące zgodności bazy danych i wymaganych modyfikacji.
- Usługa DMS korzysta z prostego, samodzielnego procesu migracji, z inteligentną oceną ułatwiającą rozwiązywanie potencjalnych problemów przed migracją.
- Usługa DMS może przeprowadzać migrację na dużą skalę z wielu źródeł do docelowej bazy danych Azure.
- Usługa DMS zapewnia wsparcie od wersji SQL Server 2005 do SQL Server 2017.

Usługa DMS nie jest jedynym narzędziem do migracji bazy danych firmy Microsoft. Zapoznaj się z [porównaniem narzędzi i usług](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services).

##### <a name="use-dms-at-scale"></a>Korzystanie z funkcji DMS na dużą skalę

Firma Contoso będzie używać usługi DMS podczas migrowania z programu SQL Server.

- W przypadku ustanowienia usługi DMS firma Contoso potrzebuje poprawnie określić rozmiar i dokonać konfiguracji w celu zoptymalizowania wydajności migracji danych. Firma Contoso wybierze opcję „warstwa krytyczna dla działania firmy z 4 rdzeniami wirtualnymi”, w ten sposób pozwalając usłudze korzystać z wielu procesorów wirtualnych na potrzeby przetwarzania równoległego i szybszych transferów danych.

    ![Skalowanie DMS](./media/contoso-migration-scale/dms.png)

- Inna taktyką skalowania dla firmy Contoso jest tymczasowo skalowanie w górę wystąpienia docelowego bazy danych Azure SQL lub MySQL do jednostki SKU warstwy Premium podczas migracji danych. Pozwala to zminimalizować ograniczanie przepustowości bazy danych, które mogłoby mieć wpływ na działania transferu danych w przypadku korzystania z jednostek SKU niższego poziomu.

##### <a name="use-other-tools"></a>Korzystanie z innych narzędzi

Oprócz DMS firma Contoso może używać innych narzędzi i usług do identyfikowania informacji o maszynach wirtualnych.

- Firma ma skrypty pomocne w ręcznych migracjach. Są one dostępne w repozytorium GitHub.
- Do migracji mogą być również wykorzystywane różne [narzędzia partnerskie](https://azure.microsoft.com/migration/partners).

## <a name="phase-3-optimize"></a>Faza 3: Optymalizacja

Po przeniesieniu zasobów na platformę Azure firma Contoso potrzebuje usprawnić je, aby zwiększyć wydajność i zmaksymalizować zwrot z inwestycji przy użyciu narzędzi do zarządzania kosztami. Ponieważ platforma Azure jest usługą z opłatami za użycie, zrozumienie sposobu działania systemów i upewnienie się, że ich rozmiary są prawidłowe, jest krytyczne dla firmy Contoso.

### <a name="azure-cost-management"></a>Azure Cost Management

Aby jak najlepiej wykorzystać inwestycję w chmurę, firma Contoso będzie korzystać z bezpłatnego narzędzia Azure Cost Management.

- To licencjonowane rozwiązanie stworzone przez Cloudyn, jednostkę zależną firmy Microsoft, umożliwia firmie Contoso przejrzyste i dokładne zarządzanie wydatkami na chmurę. Zapewnia narzędzia do monitorowania, przydzielania i przycinania kosztów chmury.
- Usługa Azure Cost Management oferuje proste raporty pulpitu nawigacyjnego, które ułatwiają przydzielanie kosztów, przewidywanie kosztów i obciążenia zwrotne.
- Usługa Cost Management pozwala optymalizować wydatki na chmurę przez identyfikowanie niedostatecznie wykorzystywanych zasobów, którymi firma Contoso może później zarządzać oraz je dostosowywać.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/cost-management/overview) na temat usługi Azure Cost Management.

![Zarządzanie kosztami](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Narzędzia natywne

Firma Contoso będzie również używać skryptów do lokalizowania nieużywanych zasobów.

- W przypadku dużych migracji często występują fragmenty danych, takie jak wirtualne dyski twarde (VHD), które wiążą się z opłatą, ale nie zapewniają żadnej wartości dla firmy. Skrypty są dostępne w repozytorium GitHub.
- Firma Contoso będzie korzystać z pracy wykonanej przez dział IT firmy Microsoft i rozważyć wdrożenie zestawu narzędzi optymalizacji zasobów platformy Azure.
- Firma Contoso może wdrożyć konto Azure Automation przy użyciu wstępnie skonfigurowanych elementów Runbook i harmonogramów do swojej subskrypcji, a następnie zacząć oszczędzać pieniądze. Optymalizacja zasobów platformy Azure odbywa się automatycznie w ramach subskrypcji po włączeniu lub utworzeniu harmonogramu, obejmując optymalizację nowych zasobów.
- Zapewnia to zdecentralizowane możliwości automatyzacji w celu obniżenia kosztów. Funkcje obejmują:
  - Automatyczne odkładanie maszyn wirtualnych platformy Azure na postawie niskiego zużycia procesora.
  - Planowanie harmonogramu odkładania i wybudzania maszyn wirtualnych platformy Azure.
  - Planowanie harmonogramu odkładania i wybudzania maszyn wirtualnych platformy Azure w kolejności rosnącej i malejącej przy użyciu tagów platformy Azure.
  - Zbiorcze usuwanie grup zasobów na żądanie.
- Rozpocznij pracę z zestawem narzędzi ARO w tym [ repozytorium GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### <a name="partner-optimization-tools"></a>Partnerskie narzędzia optymalizacji

Można używać narzędzi partnerskich, takich jak [Hanu](https://hanu.com/insight) i [Scalr]( https://www.scalr.com/cost-optimization).

## <a name="phase-4-secure-and-manage"></a>Faza 4: Zabezpieczanie i zarządzanie

Na tym etapie Contoso używa zasobów platformy Azure do zabezpieczania i zarządzania w celu utrzymania ładu, zabezpieczenia i monitorowania aplikacji chmury na platformie Azure. Te zasoby ułatwiają działanie zabezpieczonego i dobrze zarządzanego środowiska podczas używania produktów dostępnych w witrynie Azure Portal. Firma Contoso zaczyna korzystać z tych usług podczas migracji, a dzięki obsłudze hybrydowego wdrożenia platformy Azure kontynuuje używanie wielu z tych rozwiązań w celu uzyskania spójnego środowiska w całej chmurze hybrydowej.

### <a name="security"></a>Bezpieczeństwo

Firma Contoso polega na usłudze Azure Security Center, która zapewnia ujednolicone zarządzanie zabezpieczeniami i zaawansowaną ochronę przed zagrożeniami na potrzeby różnych obciążeń chmury hybrydowej.

- Usługa Security Center zapewnia pełny wgląd w zabezpieczenia aplikacji chmury na platformie Azure i kontrolę nad nimi.
- Firma Contoso może szybko wykrywać zagrożenia i podejmować odpowiednie akcje, a także zmniejszyć narażenie na ataki, dzięki włączeniu adaptacyjnej ochrony przed zagrożeniami.

[Dowiedz się](https://azure.microsoft.com/services/security-center) więcej na temat usługi Security Center.

### <a name="monitoring"></a>Monitorowanie

Firma Contoso potrzebuje wglądu w kondycję i wydajność nowo zmigrowanych aplikacji, infrastruktury i danych, które działają teraz na platformie Azure. Firma Contoso będzie używać wbudowanych narzędzi platformy Azure do monitorowania chmury, takich jak Azure Monitor, obszar roboczy usługi Log Analytics i Application Insights.

- Dzięki tym narzędziom firma Contoso może łatwo gromadzić dane ze źródeł i uzyskiwać dokładne informacje. Na przykład firma Contoso może mierzyć użycie procesora, dysku i pamięci swoich maszyn wirtualnych, wyświetlać zależności w ramach aplikacji i sieci dotyczące wielu maszyn wirtualnych oraz śledzić wydajność aplikacji.
- Firma Contoso będzie używać tych narzędzi do monitorowania chmury w celu podejmowania działań i zapewniania integracji z rozwiązaniami usług.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) o monitorowaniu platformy Azure.

### <a name="business-continuity-and-disaster-recovery"></a>Ciągłość działania i odzyskiwanie po awarii

Firma Contoso będzie potrzebować strategii ciągłości działania i odzyskiwania po awarii (BCDR) dla swoich zasobów platformy Azure.

- Platforma Azure zapewnia [wbudowane funkcje BCDR](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications), aby zapewnić bezpieczeństwo danych i działanie aplikacji/usług.
- Oprócz wbudowanych funkcji firma Contoso chce mieć pewność, że może przeprowadzić odzyskiwanie w razie awarii, uniknąć kosztownych przerw w działaniu firmy, osiągać cele zgodności oraz chronić dane przed oprogramowaniem wymuszającym okup i błędami ludzkimi. W tym celu:
  - Firma Contoso będzie wdrażać usługę Azure Backup jako ekonomiczne rozwiązanie do tworzenia kopii zapasowych zasobów platformy Azure. Ponieważ jest to wbudowane, firma Contoso może skonfigurować kopie zapasowe w chmurze w kilku prostych krokach.
  - Firma Contoso skonfiguruje odzyskiwanie po awarii dla maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery do replikacji, trybu failover i powrotu po awarii między określonymi przez nią regionami platformy Azure. To zapewni, że aplikacje działające na maszynach wirtualnych platformy Azure pozostaną dostępne w regionie pomocniczym firmy Contoso, wybranym na wypadek wystąpienia awarii w regionie podstawowym. [Dowiedz się więcej](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

## <a name="conclusion"></a>Podsumowanie

W tym artykule firma Contoso zaplanowała migrację na platformę Azure na dużą skalę. Proces migracji został podzielony na cztery etapy. Od oceny i migracji, przez optymalizację, aż do zabezpieczenia i zarządzania po ukończeniu migracji. Najważniejsze, aby zaplanować projekt migracji jako cały proces, jednak rozdzielając migrację systemów w organizacji na podstawie klasyfikacji i liczb, które mają znaczenie biznesowe. Dzięki ocenie danych i zastosowaniu klasyfikacji projekt może być podzielony na serię mniejszych migracji, które mogą być przeprowadzone bezpiecznie i szybko. Suma tych mniejszych migracji szybko doprowadzi do dużej pomyślnej migracji na platformę Azure.
