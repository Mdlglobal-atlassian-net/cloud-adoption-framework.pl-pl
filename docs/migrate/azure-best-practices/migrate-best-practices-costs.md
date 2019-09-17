---
title: Najlepsze rozwiązania dotyczące obciążeń wyceny i zmiany rozmiaru migracji na platformę Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Poznaj najlepsze rozwiązania dotyczące określania kosztów i rozmiarów obciążeń migrowanych na platformę Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b358c4d07e4adb30c0420c9d1b3bc85c25e9ce95
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024935"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące obciążeń wyceny i zmiany rozmiaru migracji na platformę Azure

Podczas planowania i projektowania migracji skoncentrowanie się na kosztach zapewnia długoterminowy sukces migracji na platformę Azure. W trakcie realizacji projektu migracji niezwykle ważne jest, aby wszystkie zespoły (takie jak finansowy, zarządzania i zespoły deweloperów aplikacji) rozumiały powiązane koszty.

- Przed rozpoczęciem migracji należy oszacować wydatki związane z migracją i ustalić plan bazowy dla miesięcznych, kwartalnych i rocznych celów budżetowych — jest to klucz do sukcesu.
- Po migracji należy zoptymalizować koszty, ciągłe monitorowanie obciążeń i planowanie wzorce użycia w przyszłości. Zmigrowane zasoby, które zaczynają jako pewien typ obciążenia, mogą z czasem zmienić się w inny typ, w zależności od użycia, kosztów i zmieniających się wymagań firmy.

W tym artykule opisano najlepsze rozwiązania dotyczące kosztów i zmiany rozmiaru przed i po migracji.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisanych w tym artykule opierają się na platformie Azure oraz z funkcji dostępnych w momencie pisania. Funkcje i możliwości zmiany w czasie. Nie wszystkie zalecenia może być odpowiednie dla danego wdrożenia, więc wybierz, która Ci odpowiada.

## <a name="before-migration"></a>Przed migracją

Przed przeniesieniem obciążeń do chmury oszacuj miesięczny koszt uruchamiania ich na platformie Azure. Proaktywne zarządzanie kosztami chmury pomaga zachować zgodność z budżetem wydatków operacyjnych. Jeśli budżet jest ograniczony, należy wziąć to pod uwagę przed rozpoczęciem migracji. W celu obniżenia kosztów rozważ przekonwertowanie obciążeń na technologie bezserwerowe platformy Azure tam, gdzie jest to możliwe.

Najlepsze rozwiązania przedstawione w tej sekcji ułatwiają oszacowanie kosztów, określenie właściwych rozmiarów maszyn wirtualnych i magazynu, wykorzystanie korzyści użycia hybrydowego platformy Azure, użycie zarezerwowanych maszyn wirtualnych oraz oszacowanie wydatków na chmurę w subskrypcjach.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Najlepsze rozwiązanie: Oszacuj miesięczny koszt obciążeń

Aby przewidzieć miesięczny rachunek za zmigrowane obciążenia, możesz użyć kilku narzędzi.

- **Kalkulator cen platformy Azure:** Wybierasz produkty, które chcesz oszacować, na przykład maszyny wirtualne i magazyn. Wprowadzasz koszty do kalkulatora cen, aby utworzyć oszacowanie.

 ![Kalkulator cen platformy Azure](./media/migrate-best-practices-costs/pricing.png) *Kalkulator cen platformy Azure*

- **Azure Migrate:** Aby oszacować koszty, należy przejrzeć i uwzględnić wszystkie zasoby wymagane do uruchamiania obciążeń na platformie Azure. Aby uzyskać te dane, należy utworzyć spis zasobów, w tym serwerów, maszyn wirtualnych, baz danych i magazynów. Usługa Azure Migrate służy do zebrania tych informacji.

- Usługa Azure Migrate umożliwia odnalezienie i ocenia środowisku lokalnych w celu zapewnienia magazynu.
- Usługa Azure Migrate można mapować i wyświetlić zależności między maszynami wirtualnymi, aby mieć pełny obraz.
- Ocena usługi Azure Migratea zawiera szacowany koszt.
  - Koszty obliczeń: Uwzględniając rozmiar maszyny wirtualnej platformy Azure zalecany podczas tworzenia oceny, usługa Azure Migrate oblicza szacowane miesięczne koszty maszyn wirtualnych za pomocą interfejsu API rozliczeń. Oszacowanie bierze pod uwagę ustawienia dotyczące systemu operacyjnego, pakietu Software Assurance, wystąpień zarezerwowanych, czasu działania maszyny wirtualnej, lokalizacji i waluty. Agreguje koszt wszystkich maszyn wirtualnych uwzględnionych w ocenie i oblicza łączny miesięczny koszt obliczeń.
  - Koszty magazynu: Usługa Azure Migrate oblicza łączny miesięczny koszt magazynu, agregując koszty magazynów wszystkich maszyn wirtualnych w ocenie. Możesz obliczyć miesięczny koszt magazynu dla konkretnej maszyny, agregując miesięczny koszt wszystkich podłączonych do niej dysków.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    *Ocena usługi Azure Migrate*

**Dowiedz się więcej:**

- [Użyj](https://azure.microsoft.com/pricing/calculator) kalkulatora cen platformy Azure.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/migrate/migrate-overview) usługa Azure migrate.
- [Przeczytaj informacje](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) na temat ocen usługi Azure Migrate.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/dms/dms-overview) o usłudze Azure Database Migration Service.

## <a name="best-practice-right-size-vms"></a>Najlepsze rozwiązanie: Określ właściwy rozmiar maszyn wirtualnych

Podczas wdrażania maszyn wirtualnych platformy Azure do obsługi obciążeń można wybrać różne opcje. Każdy typ maszyny wirtualnej ma określone funkcje i różne kombinacje procesora CPU, pamięci i dysków. Maszyny wirtualne zostały pogrupowane w sposób przedstawiony poniżej:

**Typ** | **Szczegóły** | **Korzystanie**
--- | --- | ---
**Zastosowania ogólne** | Zrównoważona moc procesora CPU w stosunku do pamięci. | Dobra opcja na potrzeby testowania i programowania, małych i średnich baz danych oraz serwerów internetowych o niewielkim i średnim ruchu.
**Optymalizacja pod kątem obliczeń** | Duża moc procesora CPU w stosunku do pamięci. | Dobra opcja w przypadku serwerów internetowych o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji.
**Optymalizacja pod kątem pamięci** | Duża ilość pamięci w stosunku do procesora CPU. | Dobra opcja w przypadku relacyjnych baz danych, średnich i dużych pamięci podręcznych oraz analizowania w pamięci.
**Optymalizacja pod kątem magazynu** | Wysoka przepływność dysku i duża liczba operacji we/wy. | Dobre dla danych big data, bazy danych SQL i NoSQL.
**Optymalizacja pod kątem procesora GPU** | Maszyny wirtualne wyspecjalizowane pod. Jednym lub wieloma procesorami GPU. | Duże grafiki i edytowania materiałów wideo.
**Wysoka wydajność** | Najszybszym i najbardziej wydajnymi procesorami CPU. Maszyny wirtualne z interfejsami opcjonalnej sieci o wysokiej przepływności (RDMA) | Krytyczne aplikacje o wysokiej wydajności.

- Ważne jest, aby zrozumieć różnice cenowe między tymi maszynami wirtualnymi i długoterminowe efekty budżetowe.
- Każdy typ obejmuje kilka serii maszyn wirtualnych.
- Ponadto, kiedy wybierzesz maszynę wirtualną w ramach serii, możesz skalować maszynę wirtualną w górę i w dół w obrębie tej serii. Na przykład, DSv2\_2 można skalować w górę do DSv2\_4, ale nie można zmienić na różnych serii, takich jak Fsv2\_2.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) o typach maszyn wirtualnych i rozmiaru oraz rozmiary mapy do typów.
- [Zaplanuj](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) ustalanie rozmiarów maszyn wirtualnych.
- [Zapoznaj się](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) z przykładową oceną dla fikcyjnej firmy Contoso.

## <a name="best-practice-select-the-right-storage"></a>Najlepsze rozwiązanie: Wybierz odpowiedni magazyn

Dostrajanie i konserwacja magazynów lokalnych (SAN lub NAS) oraz sieci do ich obsługi może być kosztowne i czasochłonne. Do chmury, aby zmniejszyć operacyjne i zarządzania problemy najczęściej są migrowane dane plików (magazyn). Firma Microsoft oferuje kilka opcji przenoszenia danych na platformie Azure, a potrzebne do podejmowania decyzji o tych opcjach. Pobrania odpowiedni typ magazynu danych można zapisać organizacji kilka tysięcy dolarów każdego miesiąca. Kilka istotnych kwestii:

- Dane, które nie są dostępne w wielu i nie jest krytyczne dla prowadzonej działalności, nie musi być umieszczone w magazynie najbardziej kosztowne.
- Z drugiej strony ważne dane krytyczne dla działania firmy powinny się znajdować na wyższe opcje magazynu warstwy.
- Podczas planowania migracji należy pobrać magazynu danych i klasyfikowania je według ważności, w celu zamapowania go na najbardziej odpowiednim magazynu. Należy wziąć pod uwagę budżetu i koszty, a także wydajność. Koszt nie powinien być zawsze głównym czynnikiem podejmowania decyzji. Pobrania tańszych opcji może spowodować obciążenie na wydajność i dostępność zagrożenia.

### <a name="storage-data-types"></a>Typy danych magazynu

System Azure oferuje różne typy magazynu danych.

<!--markdownlint-disable MD033 -->

**Typ danych** | **Szczegóły** | **Użycie**
--- | --- |  ---
**Obiekty blob** | Zoptymalizowane pod kątem przechowywania dużych ilości pozbawionych struktury obiektów, takich jak dane tekstowe lub binarne<br/><br/> | Dostęp do danych z dowolnego miejsca za pośrednictwem protokołu HTTP/HTTPS. | Użycie dla scenariuszy dostępu losowa i przesyłania strumieniowego. Na przykład do udostępniania obrazów i dokumentów bezpośrednio w przeglądarce, przesyłanie strumieniowe audio i wideo i przechowywania danych odzyskiwania kopii zapasowych i odzyskiwanie po awarii.
**Pliki** | Zarządzane udziały plików udostępnianych za pośrednictwem protokołu SMB 3.0 | Podczas migrowania lokalnych udziałów plików i w celu zapewnienia wielu połączeń/dostępu do danych plików.
**Dyski** | Oparte na stronicowych obiektach blob.<br/><br/> Typ dysku (szybkość): Standard (HDD lub SSD) lub Premium (SSD).<br/><br/>Zarządzanie dyskami: Niezarządzane (Ty zarządzasz ustawieniami dysku i magazynem) lub zarządzane (wybierasz typ dysku, a platforma Azure nim zarządza). | Na potrzeby maszyn wirtualnych używaj dysków w warstwie Premium. Używanie dysków zarządzanych dla proste zarządzanie i skalowania.
**kolejki** | Store i pobierania dużej liczby wiadomości, dostępne za pośrednictwem uwierzytelnionych połączeń (HTTP lub HTTPS) | Połącz składniki aplikacji za pomocą Kolejkowanie komunikatów asynchronicznych.
**Tabele** | Store tabel. | Teraz część interfejsu API tabeli usługi Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Poziomy dostępu

Usługa Azure storage udostępnia różne opcje do uzyskiwania dostępu do danych obiektów blob bloku. Wybieranie warstwy odpowiednich uprawnień dostępu pomaga upewnić się, że blok danych obiektów blob w sposób najbardziej efektywny.

<!--markdownlint-disable MD033 -->

**Typ** | **Szczegóły** | **Użycie**
--- | --- | ---
**gorąca** | Magazyn wyższe koszty niż Superpaska. Niższe opłaty za dostęp niż Superpaska.<br/><br/>Jest to domyślna warstwa. | Użyj dla danych aktywnie używany, w których korzysta się często.
**chłodna** | Niższe koszty magazynowania niż gorąca. Wyższe opłaty za dostęp niż gorąca.<br/><br/> Store dla co najmniej 30 dni. | Store krótkoterminowej, dane są dostępne, ale używanych rzadko.
**Archiwizowanie** | Używane dla poszczególnych blokowych obiektów blob.<br/><br/> Najbardziej ekonomiczna opcja dla magazynu. Dostęp do danych jest droższe niż gorące i zimne. | Na użytek dane, które mogą tolerować serwera godzin opóźnienia w pobieraniu i pozostaną w warstwie, przez co najmniej 180 dni.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy kont magazynu

System Azure oferuje różne rodzaje kont magazynu i warstwy wydajności.

<!--markdownlint-disable MD033 -->

**Typ konta** | **Szczegóły** | **Użycie**
--- | --- | ---
**Ogólnego przeznaczenia v2 standardowa** | Obsługuje obiekty BLOB (Blokuj, strony, dołącz), plików, dysków, kolejek i tabel.<br/><br/> Obsługuje warstwy dostępu gorąca, chłodna i archiwum. Magazyn ZRS jest obsługiwane. | Używane w przypadku większości scenariuszy i większości typów danych. Konta magazynu w warstwie Standardowa mogą być oparte na dyskach HDD lub SSD.
**Ogólnego przeznaczenia w wersji 2, Premium** | Obsługuje dane z magazynu obiektów Blob (stronicowych obiektów blob). Obsługuje warstwy dostępu gorąca, chłodna i archiwum. Magazyn ZRS jest obsługiwane.<br/><br/> Przechowywane na dyskach SSD. | Firma Microsoft zaleca używanie dla wszystkich maszyn wirtualnych.
**Ogólnego przeznaczenia w wersji 1** | Obsługa warstw dostępu nie jest obsługiwane. Nie obsługuje magazynu ZRS | Użyj, jeśli aplikacje wymagają modelu klasycznym wdrożeniu platformy Azure.
**Obiekt blob** | Specjalne konto magazynu do przechowywania obiektów bez struktury. Udostępnia blokowych obiektów blob i uzupełnialnych obiektów blob w tylko (nie plik, kolejka, tabela lub dysku magazynu usługi). Zawiera ten sam trwałość, dostępność, skalowalność i wydajność jako ogólnego przeznaczenia w wersji 2. | Nie można przechowywać stronicowych obiektów blob w ramach tych kont i dlatego nie można przechowywać pliki wirtualnego dysku twardego. Można ustawić warstwy dostępu gorąca lub chłodna.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Opcje nadmiarowości magazynu

Konta magazynu można użyć różne rodzaje nadmiarowości w celu zapewnienia odporności i wysokiej dostępności.

**Typ** | **Szczegóły** | **Użycie**
--- | --- | ---
**Magazyn lokalnie nadmiarowy (LRS)** | Chroni przed awarią lokalną przez replikację w ramach pojedynczej jednostki magazynowej do oddzielnej domeny błędów i domeny aktualizacji. Zachowuje wiele kopii danych w jednym centrum danych. Zawiera co najmniej 99,999999999% (11 9\'s) trwałości obiektów w danym roku. | Warte rozważenia, jeśli aplikacja przechowuje dane, które można łatwo odtworzyć.
**Magazyn strefowo nadmiarowy (ZRS)** | Chroni przed awarią centrum danych przez replikowanie w trzech klastrach magazynu w jednym regionie. Każdy klaster magazynu jest fizycznie oddzielony i zlokalizowany we własnej strefie dostępności. Zapewnia trwałość obiektów na poziomie co najmniej 99.9999999999% (12 9-tek) w danym roku przez przechowywanie wielu kopii danych w wielu centrach danych lub regionach.\' | Warto rozważyć, jeśli potrzebujesz spójności, trwałości i wysokiej dostępności. Może nie chronić przed awarią regionalną, jeśli ma ona trwały wpływ na wiele stref.
**Magazyn geograficznie nadmiarowy (GRS)** | Chroni przed awarią całego regionu przez replikowanie danych do regionu pomocniczego znajdującego się setki kilometrów od regionu podstawowego. Zawiera co najmniej 99,99999999999999% (16 9\'s) trwałości obiektów w danym roku. | Replika danych jest niedostępna, chyba że firma Microsoft zainicjuje tryb failover do regionu pomocniczego. Jeśli nastąpi przełączenie w tryb failover, możliwy jest dostęp do odczytu i zapisu.
**Dostęp do odczytu z magazynu geograficznie nadmiarowego (RA-GRS)** | Podobne do GRS. Zawiera co najmniej 99,99999999999999% (16 9\'s) trwałości obiektów w danym roku | Zapewnia i dostępność przez 99,99% dostępności do odczytu, umożliwiając dostęp do odczytu z drugiego regionu magazynu grs.

**Dowiedz się więcej:**

- [Przegląd](https://azure.microsoft.com/pricing/details/storage) cennik usługi Azure Storage.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) Azure Import/Export migracja dużych ilości danych obiektów blob platformy Azure i plików.
- [Porównaj](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) obiektów blob, pliki i typy danych magazynu dysku.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) dotyczące warstwy dostępu.
- [Przegląd](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) różnych typów kont magazynu.
- Dowiedz się więcej o [nadmiarowości magazynu](https://docs.microsoft.com/azure/storage/common/storage-redundancy), [LRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), i [geograficznie Nadmiarowy](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-geo-redundant-storage).
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) o usłudze Azure Files.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Najlepsze rozwiązanie: Wykorzystaj korzyści użycia hybrydowego platformy Azure

Dzięki wieloletnim inwestycjom w oprogramowanie systemów, takich jak Windows Server i SQL Server, firma Microsoft ma niepowtarzalną możliwość zaoferowania klientom wartości w chmurze ze znacznymi rabatami, na które inni dostawcy usług w chmurze niekoniecznie mogą sobie pozwolić.

Zintegrowany pakiet produktów na lokalnym/Azure Microsoft generuje zalety konkurencyjnym i kosztów. Jeśli masz obecnie system operacyjny lub inne licencjonowania oprogramowania za pośrednictwem programu software assurance (SA), możesz korzystać ze te licencje do chmury dzięki korzyści użycia hybrydowego platformy Azure.

**Dowiedz się więcej:**

- [Przyjrzyj się](https://azure.microsoft.com/pricing/hybrid-benefit) Kalkulator korzyści użycia hybrydowego.
- [Dowiedz się więcej](https://azure.microsoft.com/pricing/hybrid-benefit) o korzyści użycia hybrydowego dla systemu Windows Server.
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-use-reserved-vm-instances"></a>Najlepsze rozwiązanie: Użyj wystąpień zarezerwowanych maszyn wirtualnych

Większość platform w chmurze jest skonfigurowana pod kątem płatności zgodnie z rzeczywistym użyciem. Będzie to przedstawia zalety modelu, a ponieważ nie zawsze wiadomo, jak dynamiczna obciążenia. Po określeniu wyczyść zamiarach w przypadku obciążeń, ułatwiają planowanie infrastruktury.

Korzystając z wystąpieniami zarezerwowanymi maszyn wirtualnych platformy Azure, przedpłaty dla nich lub trzy lata termin wystąpienia maszyny Wirtualnej.

- Przedpłaty zawiera rabat w wysokości wykorzystane zasoby.
- Maszyny Wirtualnej, obliczeń bazy danych SQL, usługi Azure Cosmos DB i innych kosztów zasobów mogą znacznie zmniejszyć do 72% na ceny zgodnie z rzeczywistym użyciem.
- Rezerwacje Podaj rozliczeń rabat, a nie wpływają na stan środowiska uruchomieniowego zasobów.
- Możesz anulować zarezerwowane wystąpienia.

![Zarezerwowane wystąpienia](./media/migrate-best-practices-costs/reserve.png)
*zarezerwowane maszyn wirtualnych na platformie Azure*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) rezerwacje platformy Azure.
- [Odczyt](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) wystąpień zarezerwowanych — często zadawane pytania.
- [Uzyskaj wskazówki dotyczące cen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Najlepsze rozwiązanie: Agreguj wydatki w chmurze z wielu subskrypcji

To nieuniknione, że w końcu będziesz mieć więcej niż jedną subskrypcję platformy Azure. Na przykład może być konieczne dodatkową subskrypcję do oddzielania granice rozwoju i produkcji lub może być to platforma, która wymaga oddzielnej subskrypcji dla każdego klienta. O możliwość agregowania danych raportowania we wszystkich subskrypcjach w pojedynczej platformy jest funkcją wartościowe.

Aby to zrobić, można użyć interfejsów API usługi Azure Cost Management. Następnie po agregowanie danych do pojedynczego źródła, takich jak Azure SQL, można użyć narzędzi, takich jak usługa Power BI pozwala przedstawić dane zagregowane. Można tworzyć zagregowane raporty subskrypcji i raporty szczegółowe. Na przykład w przypadku użytkowników, którzy potrzebują proaktywnego wglądu w koszty zarządzania, można utworzyć określone widoki kosztów na podstawie działu, grupy zasobów itd. Nie musisz zapewniać im pełnego dostępu do danych rozliczeniowych platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) interfejsu API użycia platformy Azure.
- [Dowiedz się więcej o](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) nawiązywania połączenia z usługi Azure Consumption Insights w programie Power BI Desktop.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/billing/billing-manage-access) zarządzanie dostępem do informacji rozliczeniowych dla platformy Azure przy użyciu kontroli dostępu opartej na rolach (RBAC).

## <a name="after-migration"></a>Po migracji

Po zakończeniu pomyślną migrację obciążeń oraz kilku tygodni od zbierania danych użycia będziesz mieć dalsze kosztów zasobów.

- Jak możesz analizować dane, można uruchomić generowania budżetu punkt odniesienia dla grup zasobów platformy Azure i zasobów.
- Następnie jak poznać, gdzie jest poświęcony budżetu chmury, możesz analizować sposób jeszcze bardziej ograniczyć koszty.

Najlepsze rozwiązania przedstawione w tej sekcji obejmują użycie usługi Azure Cost Management na potrzeby analizy i ustalenia budżetu kosztów, monitorowanie zasobów i implementowanie budżetów grup zasobów oraz optymalizowanie monitorowania, magazynu i maszyn wirtualnych.

## <a name="best-practice-use-azure-cost-management"></a>Najlepsze rozwiązanie: Korzystanie z usługi Azure Cost Management

Firma Microsoft oferuje usługę Azure Cost Management, która ułatwia śledzenie wydatków:

- Ułatwia monitorowanie i kontrolowanie wydatków na platformę Azure oraz optymalizowanie użycia zasobów.
- Przegląda cały subskrypcji i wszystkie jej zasoby i przygotowuje zalecenia.
- Zapewnia pełną interfejsu API do integracji z zewnętrznymi narzędziami i systemami finansowych dla raportowania.
- Śledzenie użycia zasobów i zarządzania kosztami chmury z jednym, ujednoliconym widoku.
- Udostępnia operacyjnymi i finansowymi szczegółowe informacje ułatwiające podejmowanie świadomych decyzji.

W usłudze Cost Management możesz wykonywać następujące zadania:

- **Tworzenie budżetu:** Utwórz budżet na potrzeby rozliczeń finansowych.
  - Możesz uwzględnić usługi, których używasz, lub zasubskrybować określony okres (miesięcznie, kwartalnie, rocznie) i zakres (subskrypcje/grupy zasobów). Możesz na przykład utworzyć budżet subskrypcji platformy Azure dla okresu miesięcznego, kwartalnego lub rocznego.
    - Po utworzeniu budżetu, jest wyświetlana na analizy kosztów. Przeglądanie budżetu względem bieżących wydatków jest jednym z pierwszych kroków w razie analizując koszty i wydatki.
  - Mogą być wysyłane powiadomienia e-mail, po osiągnięciu progów budżetu.
  - Dane zarządzania kosztami można wyeksportować do usługi Azure Storage w celu analizy.

    ![Budżet usługi Cost Management](./media/migrate-best-practices-costs/budget.png)
    *Budżet usługi Azure Cost Management*

- **Przeprowadzanie analizy kosztów:** Przeprowadź analizę kosztów, aby eksplorować i analizować koszty organizacji, co pomoże Ci zrozumieć, jak są naliczane koszty, i zidentyfikować trendy wydatków.
  - Analiza kosztów jest dostępna dla użytkowników usługi EA.
  - Dane analizy kosztów można wyświetlić dla różnych zakresów, w tym według działu, konta, subskrypcji lub grupy zasobów.
  - Możesz uzyskać analizę kosztów pokazującą łączne koszty dla bieżącego miesiąca oraz skumulowane koszty dzienne.

    ![Analiza usługi Cost Management](./media/migrate-best-practices-costs/analysis.png)
    *Analiza usługi Azure Cost Management*
- **Uzyskiwanie rekomendacji:** Zapoznaj się z rekomendacjami usługi Advisor, które pokazują, jak można zoptymalizować i poprawić wydajność.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/cost-management/overview) z usługi Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices) optymalizacji inwestycji w chmurę dzięki usłudze Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management/use-reports) korzystanie z raportów w usłudze Azure Cost Management.
- [Pobierz samouczek](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) dotyczące optymalizacji kosztów z zaleceń.
- [Przejrzyj](https://docs.microsoft.com/rest/api/consumption/budgets) interfejs API użycia platformy Azure.

## <a name="best-practice-monitor-resource-utilization"></a>Najlepsze rozwiązanie: Monitoruj wykorzystanie zasobów

Na platformie Azure płacisz za to, z czego korzystasz, gdy zasoby są używane, i nie płacisz, gdy nie są używane. W przypadku maszyn wirtualnych rozliczanie ma miejsce, gdy maszyna wirtualna zostanie przydzielona. Po cofnięciu przydziału maszyny wirtualnej opłaty nie są naliczane. Pamiętając o tym powinien monitorować maszyny wirtualne w użyciu i Sprawdź zmiany rozmiaru maszyny Wirtualnej.

- Stale ocenia obciążenia maszyny Wirtualnej do określenia podstawy.
- Na przykład jeśli obciążenie jest używany w dużym stopniu od poniedziałku do piątku, 8: 00 do 18: 00, jednak rzadko używana poza tymi godzinami, możesz obniżyć maszyn wirtualnych poza godziny szczytu. Może to oznaczać, zmienianie rozmiarów maszyn wirtualnych lub zestawów za pomocą skalowania maszyn wirtualnych do maszyn wirtualnych z funkcją automatycznego skalowania w górę lub w dół.
- Niektóre firmy "Odłóż", maszyn wirtualnych przez umieszczenie ich w kalendarzu, który określa kiedy powinna być dostępna, a jeśli one nie potrzebne.
- Oprócz monitorowania maszyn wirtualnych, należy monitorować inne zasoby sieciowe, takie jak usługa ExpressRoute i brama sieci wirtualnej, pod kątem nadmiernego i niedostatecznego użycia.
- Użycie maszyny wirtualnej można monitorować za pomocą narzędzi firmy Microsoft, takich jak usługi Azure Cost Management, Azure Monitor i Azure Advisor. Dostępne są również narzędzia innych firm.

**Dowiedz się więcej:**

- Zapoznaj się z omówieniem programu [usługi Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) i [usługi Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview).
- [Pobierz](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) Advisor koszt zalecenia.
- [Dowiedz się, jak [zoptymalizować koszty na podstawie rekomendacji](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) i [uniknąć nieoczekiwanych opłat](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Dowiedz się więcej o zestawie narzędzi [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Najlepsze rozwiązanie: Zaimplementuj budżety grup zasobów

Grupy zasobów są często używane w celu reprezentowania granic kosztów. Wraz z tego wzorca użycia zespołu platformy Azure nadal twórz nowe i ulepszone sposoby śledzić i analizować zasobów wydatków na różnych poziomach, w tym możliwość tworzenia budżet na grupę zasobów i zasoby.

- Budżet grupy zasobów ułatwia śledzenie kosztów skojarzonych z grupą zasobów.
- Można wyzwalać alerty i uruchomić szeroką gamę elementów playbook, ponieważ osiągnięto lub przekroczono budżetu.

**Dowiedz się więcej:**

- [Dowiedz się, jak](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) Zarządzanie kosztami przy użyciu budżetów platformy Azure.
- [Postępuj zgodnie z samouczkiem](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json), aby utworzyć budżet platformy Azure i zarządzać nim.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Najlepsze rozwiązanie: Zoptymalizuj przechowywanie usługi Azure Monitor

Po przeniesieniu zasobów na platformę Azure i włączeniu dla nich rejestrowania danych diagnostycznych generowanych jest wiele danych dziennika. Te dane dziennika jest typowo wysyłana do konta magazynu, który jest mapowany do obszaru roboczego usługi Log Analytics.

- Im dłużej okres przechowywania danych dziennika większej ilości danych należy.
- Nie wszystkie dane dzienników są równe, i niektóre zasoby powoduje generowanie większej ilości danych dziennika niż inne.
- Ze względu na przepisy i zgodności prawdopodobne jest, że konieczne będzie przechowywać dane dziennika dla niektórych zasobów, które są dłuższe niż inne.
- Staranne wiersz powinien Przeprowadź między optymalizacji kosztów magazynu dziennika i przechowywanie danych dziennika, które są potrzebne.
- Firma Microsoft zaleca, ocena i konfigurowanie rejestrowania natychmiast po zakończeniu migracji, aby nie pieniądze wydatków zachowywanie dzienników znaczenia.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) na temat monitorowania użycia i szacowanych kosztów.

## <a name="best-practice-optimize-storage"></a>Najlepsze rozwiązanie: Zoptymalizuj magazyn

Jeśli przed migracją magazyn został wybrany zgodnie z najlepszymi rozwiązaniami, prawdopodobnie przynosi to pewne korzyści. Są jednak nadal można optymalizować koszty prawdopodobnie dodatkowego miejsca do magazynowania. Wraz z upływem czasu plików i obiektów blob stają się nieaktualne. Dane nie mogą być używane z już jednak wymagania prawne może oznaczać konieczność zapewnienia jego przez pewien okres. W efekcie nie może być konieczne zapisać go w używanym do migracji oryginalny magazyn o wysokiej wydajności.

Identyfikowanie i przeniesienie starych danych na tańsze obszary do przechowywania może mieć duży wpływ na budżetu miesięczny magazynu i oszczędności kosztów. System Azure oferuje wiele sposobów, aby pomóc w identyfikacji, a następnie zapisywania tej nieaktualnych danych.

- Korzystaj z warstwy dostępu dla magazynu ogólnego przeznaczenia w wersji 2, przenoszenie mniej ważnych danych z warstwy gorąca do warstwy chłodna i archiwizacji.
- Za pomocą usługi StorSimple można przenieść nieaktualnych danych na podstawie zasad niestandardowych.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) dotyczące warstwy dostępu.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/azure-monitor/overview) rozwiązania StorSimple i z [cennikiem rozwiązania StorSimple](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Najlepsze rozwiązanie: Zautomatyzuj optymalizację maszyn wirtualnych

Celem uruchamiania maszyny wirtualnej w chmurze jest zmaksymalizowanie używanego procesora, pamięci i dysku. Jeśli odkryjesz maszyny wirtualne, które nie są zoptymalizowane lub są nieużywane przez długie okresy czasu, warto je wyłączyć lub skalować je w dół przy użyciu zestawów skalowania maszyn wirtualnych.

Maszynę wirtualną można zoptymalizować za pomocą usługi Azure Automation, zestawów skalowania maszyn wirtualnych, automatycznego zamykania oraz rozwiązań opartych na skrypcie lub rozwiązań innych firm.

**Dowiedz się więcej:**

- [Dowiedz się, jak](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) Użyj skalowania automatycznego w pionie.
- [Harmonogram](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) autostart maszyny Wirtualnej.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) uruchamianiem lub zatrzymywaniem maszyn wirtualnych poza godzinami pracy w usłudze Azure Automation.
- [Uzyskaj więcej informacji] o usłudze [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) i zestawie narzędzi [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Najlepsze rozwiązania: Używaj usługi Logic Apps i elementów runbook z interfejsem API budżetów

Platforma Azure oferuje interfejs API REST, który ma dostęp do informacji rozliczeniowych dzierżawy.

- Interfejs API budżetów umożliwia integrowanie systemów zewnętrznych i przepływów pracy, które są wyzwalane przez metryk, który kompilujesz z danymi interfejsu API.
- Możesz ściągnąć dane dotyczące użycia i zasobów do narzędzia do analizy danych preferowany.
- Interfejsy API usługi RateCard i użycia zasobów platformy Azure mogą ułatwić dokładne przewidywanie kosztów i zarządzanie nimi.
- Interfejsy API są zaimplementowane jako dostawcy zasobów i są uwzględniane w interfejsach API udostępnianych przez usługę Azure Resource Manager.
- Interfejs API budżetów można zintegrować z usługi Azure Logic Apps i elementów Runbook.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/rest/api/consumption/budgets) dotyczących budżetów interfejsu API.
- [Uzyskaj wgląd](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) w użycie platformy Azure za pomocą interfejsu API rozliczeń.

## <a name="best-practice-implement-serverless-technologies"></a>Najlepsze rozwiązanie: Zaimplementuj technologie bezserwerowe

Obciążenia maszyn wirtualnych są często migrowane „w stanie takim, w jakim są”, aby uniknąć przestoju. Często maszyny wirtualne mogą być hostowane zadania, które są tymczasowymi, biorąc krótki okres, aby uruchomić, lub też wiele godzin. Na przykład maszyny wirtualne, które są uruchamiane zaplanowane zadania, takie jak Windows zadań harmonogramu lub skryptów programu PowerShell. Podczas tych zadań nie są uruchomione, niemniej one przejmowania maszyny Wirtualnej i dysku koszty magazynowania.

Po migracji i po przeprowadzeniu szczegółowego przeglądu zadań tego typu warto rozważyć zmigrowanie ich do technologii bezserwerowych, takich jak usługa Azure Functions lub zadania usługi Azure Batch. Dzięki takiemu rozwiązaniu nie trzeba już zarządzać maszynami wirtualnymi ani ich konserwować, co zapewnia dodatkowe oszczędności kosztów.

**Dowiedz się więcej:**

- Dowiedz się więcej o usłudze [Azure Functions](https://azure.microsoft.com/services/functions).
- Dowiedz się więcej o usłudze [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Następne kroki

Przejrzyj najlepsze rozwiązania:

- [Najlepsze praktyki](./migrate-best-practices-security-management.md) zabezpieczeń i zarządzania po migracji.
- [Najlepsze praktyki](./migrate-best-practices-networking.md) sieci po zakończeniu migracji.
