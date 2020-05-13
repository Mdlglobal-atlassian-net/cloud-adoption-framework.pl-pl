---
title: Nabieranie kosztów i ustalanie wielkości obciążeń migrowanych do platformy Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać najlepsze rozwiązania związane z wyceną i ustalaniem wielkości obciążeń migrowanych do platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 05d511419a27d00e87abfae156110749a20029d8
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222372"
---
<!-- docsTest:ignore ARO -->

# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące określania kosztów i rozmiarów obciążeń migrowanych na platformę Azure

Podczas planowania i projektowania migracji skoncentrowanie się na kosztach zapewnia długoterminowy sukces migracji na platformę Azure. W trakcie realizacji projektu migracji niezwykle ważne jest, aby wszystkie zespoły (takie jak finansowy, zarządzania i zespoły deweloperów aplikacji) rozumiały powiązane koszty.

- Przed rozpoczęciem migracji należy oszacować wydatki związane z migracją i ustalić plan bazowy dla miesięcznych, kwartalnych i rocznych celów budżetowych — jest to klucz do sukcesu.
- Po migracji należy zoptymalizować koszty, stale monitorować obciążenia i zaplanować przyszłe wzorce użycia. Zmigrowane zasoby, które zaczynają jako pewien typ obciążenia, mogą z czasem zmienić się w inny typ, w zależności od użycia, kosztów i zmieniających się wymagań firmy.

W tym artykule opisano najlepsze rozwiązania dotyczące określania kosztów i rozmiarów obciążeń przed migracją i po niej.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule dotyczą funkcji usług i platformy Azure dostępnych w momencie pisania artykułu. Funkcje i możliwości zmieniają się w miarę upływu czasu. Nie wszystkie rekomendacje mogą dotyczyć danego wdrożenia, więc wybierz te, które są odpowiednie w Twoim przypadku.

## <a name="before-migration"></a>Przed migracją

Przed przeniesieniem obciążeń do chmury oszacuj miesięczny koszt uruchamiania ich na platformie Azure. Proaktywne zarządzanie kosztami chmury pomaga zachować zgodność z budżetem wydatków operacyjnych. Jeśli budżet jest ograniczony, należy wziąć to pod uwagę przed rozpoczęciem migracji. W celu obniżenia kosztów rozważ przekonwertowanie obciążeń na technologie bezserwerowe platformy Azure tam, gdzie jest to możliwe.

Najlepsze rozwiązania przedstawione w tej sekcji ułatwiają oszacowanie kosztów, określenie właściwych rozmiarów maszyn wirtualnych i magazynu, wykorzystanie korzyści użycia hybrydowego platformy Azure, użycie zarezerwowanych maszyn wirtualnych oraz oszacowanie wydatków na chmurę w subskrypcjach.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Najlepsze rozwiązanie: oszacowanie miesięcznych kosztów obciążeń

Aby przewidzieć miesięczny rachunek za zmigrowane obciążenia, możesz użyć kilku narzędzi.

<!-- TODO: Change "input costs" -->
- **Kalkulator cen platformy Azure:** Wybierz produkty, które chcesz oszacować, na przykład maszyny wirtualne i magazyn, a następnie wprowadź koszty do kalkulatora, aby utworzyć oszacowanie.

 ![Kalkulator cen platformy Azure](./media/migrate-best-practices-costs/pricing.png) _Kalkulator cen platformy Azure_

- **Azure Migrate:** Aby oszacować koszty, należy przejrzeć i uwzględnić wszystkie zasoby wymagane do uruchamiania obciążeń na platformie Azure. Aby uzyskać te dane, należy utworzyć spis zasobów, w tym serwerów, maszyn wirtualnych, baz danych i magazynów. Aby zebrać te informacje, można użyć usługi Azure Migrate.

- Usługa Azure Migrate odnajduje i ocenia Twoje środowisko lokalne w celu dostarczenia spisu.
- Usługa Azure Migrate może zamapować i pokazać zależności między maszynami wirtualnymi, aby przedstawić pełny obraz.
- Ocena usługi Azure Migratea zawiera szacowany koszt.
  - Koszty obliczeń: przy użyciu rozmiaru maszyny wirtualnej platformy Azure zalecane podczas tworzenia oceny, Azure Migrate używa interfejsy API rozliczeń platformy Azure, aby obliczyć szacowane miesięczne koszty maszyn wirtualnych. Oszacowanie bierze pod uwagę ustawienia dotyczące systemu operacyjnego, pakietu Software Assurance, wystąpień zarezerwowanych, czasu działania maszyny wirtualnej, lokalizacji i waluty. Agreguje koszt wszystkich maszyn wirtualnych uwzględnionych w ocenie i oblicza łączny miesięczny koszt obliczeń.
  - Koszt magazynu: Azure Migrate oblicza łączne miesięczne koszty magazynowania, sumując koszty magazynowania wszystkich maszyn wirtualnych w ocenie. Możesz obliczyć miesięczny koszt magazynu dla konkretnej maszyny, agregując miesięczny koszt wszystkich podłączonych do niej dysków.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    _Ocena usługi Azure Migrate_

**Dowiedz się więcej:**

- [Użyj](https://azure.microsoft.com/pricing/calculator) kalkulatora cen platformy Azure.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/migrate/migrate-services-overview) usługi Azure Migrate.
- [Przeczytaj informacje](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation) na temat ocen usługi Azure Migrate.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/dms/dms-overview) o usłudze Azure Database Migration Service.

## <a name="best-practice-right-size-vms"></a>Najlepsze rozwiązania: maszyny wirtualne o odpowiednim rozmiarze

Podczas wdrażania maszyn wirtualnych platformy Azure do obsługi obciążeń można wybrać różne opcje. Każdy typ maszyny wirtualnej ma określone funkcje i różne kombinacje procesora CPU, pamięci i dysków. Maszyny wirtualne zostały pogrupowane w sposób przedstawiony poniżej:

| **Typ** | **Szczegóły** | **Użycie** |
| --- | --- | --- |
| **Zastosowania ogólne** | Zrównoważona moc procesora CPU w stosunku do pamięci. | Dobra opcja na potrzeby testowania i programowania, małych i średnich baz danych oraz serwerów internetowych o niewielkim i średnim ruchu. |
| **Optymalizacja pod kątem obliczeń** | Duża moc procesora CPU w stosunku do pamięci. | Dobra opcja w przypadku serwerów internetowych o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji. |
| **Optymalizacja pod kątem pamięci** | Duża ilość pamięci w stosunku do procesora CPU. | Dobra opcja w przypadku relacyjnych baz danych, średnich i dużych pamięci podręcznych oraz analizowania w pamięci. |
| **Optymalizacja pod kątem magazynu** | Wysoka przepływność dysku i duża liczba operacji we/wy. | Dobra opcja w przypadku danych big data oraz baz danych SQL i NoSQL. |
| **Optymalizacja pod kątem procesora GPU** | Wyspecjalizowane maszyny wirtualne. Jeden lub wiele procesorów GPU. | Duże obciążenie grafiką i edytowaniem wideo. |
| **Wysoka wydajność** | Najszybszy i najbardziej wydajny procesor CPU. Maszyny wirtualne z opcjonalnymi interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA) | Krytyczne aplikacje o wysokiej wydajności. |

- Ważne jest, aby zrozumieć różnice cenowe między tymi maszynami wirtualnymi i długoterminowe efekty budżetowe.
- Każdy typ obejmuje kilka serii maszyn wirtualnych.
- Ponadto, kiedy wybierzesz maszynę wirtualną w ramach serii, możesz skalować maszynę wirtualną w górę i w dół w obrębie tej serii. Na przykład maszynę DSv2\_2 można skalować w górę do DSv2\_4, ale nie można zmienić jej serii na przykład na Fsv2\_2.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) o typach i rozmiarach maszyn wirtualnych oraz mapowaniu rozmiarów na typy.
- [Zaplanuj](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs) ustalanie rozmiarów maszyn wirtualnych.
- [Zapoznaj się](https://docs.microsoft.com/azure/migrate/contoso-migration-assessment) z przykładową oceną dla fikcyjnej firmy Contoso.

## <a name="best-practice-select-the-right-storage"></a>Najlepsze rozwiązanie: wybierz odpowiedni magazyn

Dostrajanie i konserwacja magazynów lokalnych (SAN lub NAS) oraz sieci do ich obsługi może być kosztowne i czasochłonne. Dane plików (magazynu) są często migrowane do chmury, co pomaga zminimalizować nakład pracy związany z zadaniami operacyjnymi i zarządzaniem. Firma Microsoft oferuje kilka opcji przenoszenia danych na platformę Azure. Musisz podjąć decyzje związane z tymi opcjami. Wybranie odpowiedniego typu magazynu dla danych może zaoszczędzić organizacji kilka tysięcy dolarów miesięcznie. Oto kilka kwestii do rozważenia:

- Dane, które nie są dostępne w większości i nie są krytyczne dla firmy, nie muszą być umieszczane w najbardziej kosztownej pamięci masowej.
- Z kolei dla ważnych danych, o krytycznym znaczeniu dla firmy, należy wybrać opcje magazynu w wyższej warstwie.
- Podczas planowania migracji wykonaj spis danych i sklasyfikuj je według ważności, aby zamapować je na najbardziej odpowiedni magazyn. Weź pod uwagę budżet i koszt, a także wydajność. Koszt nie powinien być głównym czynnikiem wpływającym na podejmowanie decyzji. Wybranie najtańszej opcji może wystawić obciążenie na ryzyko związane z wydajnością i dostępnością.

### <a name="storage-data-types"></a>Typy danych magazynów

Platforma Azure udostępnia różne typy danych magazynu.

<!-- markdownlint-disable MD033 -->

| **Typ danych** | **Szczegóły** | **Wykorzystywani** |
| --- | --- |  --- |
| **Obiekty blob** | Zoptymalizowany pod kątem przechowywania dużych ilości obiektów bez struktury, takich jak dane tekstowe lub binarne. <br><br> | Uzyskiwanie dostępu do danych z dowolnego miejsca za pośrednictwem protokołu HTTP/HTTPS. | Używane na potrzeby scenariuszy przesyłania strumieniowego i dostępu losowego. Na przykład w celu udostępniania obrazów i dokumentów bezpośrednio w przeglądarce, strumieniowego przesyłania wideo i audio oraz przechowywania danych kopii zapasowych i odzyskiwania po awarii. |
| **Pliki** | Zarządzane udziały plików dostępne za pośrednictwem protokołu SMB 3.0 | Używane podczas migrowania lokalnych udziałów plików i w celu obsłużenia wielu żądań dostępu/połączeń do danych plików. |
| **Dyski** | Oparte na stronicowych obiektach blob. <br><br> Typ dysku (prędkość): standardowy (dysk twardy lub SSD) lub Premium (SSD). <br><br> Zarządzanie dyskami: niezarządzane (Zarządzanie ustawieniami dysków i magazynem) lub zarządzanie (można wybrać typ dysku, a platforma Azure zarządza dyskiem). | Na potrzeby maszyn wirtualnych używaj dysków w warstwie Premium. Na potrzeby łatwego zarządzania i skalowania używaj dysków zarządzanych. |
| **Kolejki** | Przechowywanie i pobieranie dużej liczby komunikatów, do których można uzyskać dostęp za pośrednictwem wywołań uwierzytelnionych (HTTP lub HTTPS) | Łączenie składników aplikacji za pomocą asynchronicznego kolejkowania komunikatów. |
| **Tabele** | Przechowuje tabele. | Teraz jest to część interfejsu API tabeli usługi Azure Cosmos DB. |

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Poziomy dostępu

Magazyn platformy Azure oferuje różne opcje uzyskiwania dostępu do danych blokowych obiektów blob. Wybranie odpowiedniej warstwy dostępu pozwala zapewnić, że dane blokowych obiektów blob są przechowywane w najbardziej opłacalny sposób.

<!-- markdownlint-disable MD033 -->

| **Typ** | **Szczegóły** | **Wykorzystywani** |
| --- | --- | --- |
| **Gorąca** | Wyższy koszt przechowywania, niż w warstwie Chłodna. Niższe opłaty za dostęp, niż w warstwie Chłodna. <br><br> Jest to warstwa domyślna. | Służy do przechowywania danych w przypadku aktywnego użycia, gdy dostęp do danych jest uzyskiwany często. |
| **Chłodna** | Niższy koszt przechowywania, niż w warstwie Gorąca. Wyższe opłaty za dostęp, niż w warstwie Gorąca. <br><br> Przechowywanie przez co najmniej 30 dni. | Przechowywanie krótkoterminowe, dane są dostępne, ale dostęp do nich jest uzyskiwany rzadko. |
| **Archiwum** | Używana na potrzeby pojedynczych blokowych obiektów blob. <br><br> Najbardziej ekonomiczna opcja magazynu. Dostęp do danych jest droższy, niż w warstwach Gorąca i Chłodna. | Używana na potrzeby danych, które można pobierać z opóźnieniem kilku godzin i które pozostaną w tej warstwie przez co najmniej 180 dni. |

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy konta magazynu

Platforma Azure oferuje różne typy kont magazynu i warstw wydajności.

<!-- markdownlint-disable MD033 -->

| **Typ konta** | **Szczegóły** | **Wykorzystywani** |
| --- | --- | --- |
| **Ogólnego przeznaczenia w wersji 2, Standardowa** | Obsługuje obiekty blob (blokowe, stronicowe, dołączania), pliki, dyski, kolejki i tabele. <br><br> Obsługuje warstwy dostępu Gorąca, Chłodna i Archiwum. Magazyn strefowo nadmiarowy jest obsługiwany. | Używane w przypadku większości scenariuszy i większości typów danych. Konta magazynu w warstwie Standardowa mogą być oparte na dyskach HDD lub SSD. |
| **Ogólnego przeznaczenia w wersji 2, Premium** | Obsługuje dane magazynu obiektów blob (stronicowe obiekty blob). Obsługuje warstwy dostępu Gorąca, Chłodna i Archiwum. Magazyn strefowo nadmiarowy jest obsługiwany. <br><br> Dane są przechowywane na dysku SSD. | Firma Microsoft zaleca używanie tego typu konta dla wszystkich maszyn wirtualnych. |
| **Ogólnego przeznaczenia, wersja 1** | Obsługa warstw dostępu nie jest obsługiwana. Nie obsługuje magazynu strefowo nadmiarowego | Używane, jeśli aplikacje potrzebują klasycznego modelu wdrażania platformy Azure. |
| **Obiekt blob** | Specjalne konto magazynu do przechowywania obiektów bez struktury. Zapewnia tylko blokowe obiekty blob i obiekty blob dołączania (bez plików, kolejek, tabel i usług magazynu). Zapewnia taką samą trwałość, dostępność, skalowalność i wydajność, jak konto ogólnego przeznaczenia w wersji 2. | Na tych kontach nie można przechowywać stronicowych obiektów blob, a zatem nie można przechowywać plików VHD. Warstwę dostępu można ustawić na Gorącą lub Chłodną. |

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Opcje nadmiarowości magazynu

Konta magazynu mogą wykorzystywać różne typy nadmiarowości na potrzeby zapewnienia odporności i wysokiej dostępności.

| **Typ** | **Szczegóły** | **Wykorzystywani** |
| --- | --- | --- |
| **Magazyn lokalnie nadmiarowy (LRS)** | Chroni przed awarią lokalną przez replikację w ramach pojedynczej jednostki magazynowej do oddzielnej domeny błędów i domeny aktualizacji. Przechowuje wiele kopii danych w jednym centrum danych. Zapewnia co najmniej 99,999999999% czasu trwałości obiektów w danym roku. | Warte rozważenia, jeśli aplikacja przechowuje dane, które można łatwo odtworzyć. |
| **Magazyn strefowo nadmiarowy (ZRS)** | Chroni przed awarią centrum danych przez replikowanie w trzech klastrach magazynu w jednym regionie. Każdy klaster magazynu jest fizycznie oddzielony i zlokalizowany we własnej strefie dostępności. Zapewnia co najmniej 99,9999999999 procentową trwałość obiektów w danym roku przez przechowywanie wielu kopii danych w wielu centrach lub regionach. | Warto rozważyć, jeśli potrzebujesz spójności, trwałości i wysokiej dostępności. Może nie chronić przed awarią regionalną, jeśli ma ona trwały wpływ na wiele stref. |
| **Magazyn geograficznie nadmiarowy (GRS)** | Chroni przed awarią całego regionu przez replikowanie danych do regionu pomocniczego znajdującego się setki kilometrów od regionu podstawowego. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Dane repliki są niedostępne, dopóki firma Microsoft nie zainicjuje przejścia w tryb failover do regionu pomocniczego. Jeśli nastąpi przełączenie w tryb failover, możliwy jest dostęp do odczytu i zapisu. |
| **Dostęp do odczytu z magazynu geograficznie nadmiarowego (RA-GRS)** | Podobne do GRS. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Zapewnia dostępność i 99,99% odczytu, umożliwiając dostęp do odczytu z drugiego regionu używanego przez GRS. |

**Dowiedz się więcej:**

- [Przejrzyj](https://azure.microsoft.com/pricing/details/storage) cennik usługi Azure Storage.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) o usłudze Azure Import/Export na potrzeby migracji dużych ilości danych do obiektów blob i plików platformy Azure.
- [Porównaj](https://docs.microsoft.com/azure/storage/common/storage-decide-blobs-files-disks) typy danych magazynu, takie jak obiekty blob, pliki i dyski.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o warstwach dostępu.
- [Przejrzyj](https://docs.microsoft.com/azure/storage/common/storage-account-overview) różne typy kont magazynu.
- Dowiedz się więcej o [nadmiarowości usługi Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy), w tym LRS, ZRS, GRS i dostęp do odczytu.
- Dowiedz się więcej o [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Najlepsze rozwiązanie: korzystanie z korzyści użycia hybrydowego platformy Azure

Dzięki wieloletnim inwestycjom w oprogramowanie systemów, takich jak Windows Server i SQL Server, firma Microsoft ma niepowtarzalną możliwość zaoferowania klientom wartości w chmurze ze znacznymi rabatami, na które inni dostawcy usług w chmurze niekoniecznie mogą sobie pozwolić.

Zintegrowane portfolio produktów firmy Microsoft, obejmujące środowisko lokalne i platformę Azure, stanowi przewagę konkurencyjną i ekonomiczną. Jeśli obecnie posiadasz licencję systemu operacyjnego lub innego oprogramowania w ramach pakietu Software Assurance (SA), możesz przenieść te licencje do chmury za pośrednictwem programu Korzyść użycia hybrydowego platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj się](https://azure.microsoft.com/pricing/hybrid-benefit) z kalkulatorem korzyści użycia hybrydowego.
- [Dowiedz się więcej](https://azure.microsoft.com/pricing/hybrid-benefit) o korzyści użycia hybrydowego dla systemu Windows Server.
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-use-reserved-vm-instances"></a>Najlepsze rozwiązanie: korzystanie z wystąpień zarezerwowanych maszyn wirtualnych

Większość platform w chmurze jest skonfigurowana pod kątem płatności zgodnie z rzeczywistym użyciem. Ten model zawiera wady, ponieważ nie zawsze wiadomo, jak dynamiczne będą obciążenia. Kiedy określasz jasne intencje dla obciążenia, bierzesz udział w planowaniu infrastruktury.

Korzystając z Azure Reserved VM Instances, przedpłata za jeden rok lub trzy lata dla wystąpień maszyn wirtualnych.

- Przedpłata wiąże się z rabatem na używane zasoby.
- Możesz znacząco obniżyć koszty maszyn wirtualnych, obliczeń w usłudze SQL Database, usługi Azure Cosmos DB lub innych zasobów nawet o 72% w porównaniu z cenami w modelu płatności zgodnie z rzeczywistym użyciem.
- Rezerwacje umożliwiają skorzystanie z rabatu na rozliczenia i nie mają wpływu na stan środowiska uruchomieniowego Twoich zasobów.
- Wystąpienia zarezerwowane można anulować.

![Wystąpienia zarezerwowane](./media/migrate-best-practices-costs/reserve.png)
_Zarezerwowane maszyny wirtualne platformy Azure_

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [Azure Reservations](https://docs.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations).
- Przeczytaj [często zadawane pytania dotyczące wystąpień zarezerwowanych](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq).
- Zapoznaj się ze [wskazówkami dotyczącymi cen dla SQL Server maszyn wirtualnych platformy Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Najlepsze rozwiązanie: agregowanie wydatków w chmurze w ramach subskrypcji

To nieuniknione, że w końcu będziesz mieć więcej niż jedną subskrypcję platformy Azure. Możesz na przykład potrzebować dodatkowej subskrypcji w celu rozdzielenia granic środowiska deweloperskiego i produkcyjnego lub możesz mieć platformę, która wymaga oddzielnej subskrypcji dla każdego klienta. Możliwość agregowania raportowania danych ze wszystkich subskrypcji na jednej platformie jest wartościową funkcją.

W tym celu można użyć interfejsów API usługi Azure Cost Management. Następnie, po zagregowaniu danych do jednego źródła, takiego jak baza danych SQL Azure, można użyć narzędzi, takich jak usługa Power BI, aby uwidocznić zagregowane dane. Można tworzyć zagregowane raporty subskrypcji i raporty szczegółowe. Na przykład w przypadku użytkowników, którzy potrzebują proaktywnie wglądu w koszty zarządzania, można utworzyć określone widoki kosztów na podstawie działów, grup zasobów lub innych informacji. Nie musisz zapewniać im pełnego dostępu do danych rozliczeniowych platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) interfejsu API użycia platformy Azure.
- [Dowiedz się więcej](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) na temat nawiązywania połączenia z usługą Azure Consumption Insights w programie Power BI Desktop.
- [Dowiedz się](https://docs.microsoft.com/azure/billing/billing-manage-access), jak zarządzać dostępem do informacji rozliczeniowych dla platformy Azure przy użyciu kontroli dostępu opartej na rolach (RBAC).

## <a name="after-migration"></a>Po migracji

Po pomyślnej migracji obciążeń i kilku tygodniach zbierania danych dotyczących użycia będziesz mieć jasny obraz kosztów zasobów.

- W miarę analizowania danych możesz rozpocząć generowanie planu bazowego budżetu dla grup zasobów i zasobów platformy Azure.
- Następnie, gdy już będziesz wiedzieć, gdzie jest wydawany budżet na chmurę, możesz przeprowadzić analizę, jak dodatkowo ograniczyć koszty.

Najlepsze rozwiązania przedstawione w tej sekcji obejmują użycie usługi Azure Cost Management na potrzeby analizy i ustalenia budżetu kosztów, monitorowanie zasobów i implementowanie budżetów grup zasobów oraz optymalizowanie monitorowania, magazynu i maszyn wirtualnych.

## <a name="best-practice-use-azure-cost-management"></a>Najlepsze rozwiązanie: Użyj Azure Cost Management

Firma Microsoft oferuje usługę Azure Cost Management, która ułatwia śledzenie wydatków:

- Ułatwia monitorowanie i kontrolowanie wydatków na platformę Azure oraz optymalizowanie użycia zasobów.
- Przegląda całą subskrypcję i wszystkie jej zasoby oraz wyświetla rekomendacje.
- Zapewnia pełny interfejs API do integrowania narzędzi zewnętrznych i systemów finansowych na potrzeby raportowania.
- Śledzi użycie zasobów i zarządza kosztami chmury przy użyciu pojedynczego, ujednoliconego widoku.
- Dostarcza rozbudowane szczegółowe informacje operacyjne i finansowe, które ułatwiają podejmowanie świadomych decyzji.

W usłudze Cost Management możesz wykonywać następujące zadania:

- **Utwórz budżet:** Utwórz budżet dla odpowiedzialności finansowej.
  - Możesz uwzględnić usługi, których używasz, lub zasubskrybować określony okres (miesięcznie, kwartalnie, rocznie) i zakres (subskrypcje/grupy zasobów). Możesz na przykład utworzyć budżet subskrypcji platformy Azure dla okresu miesięcznego, kwartalnego lub rocznego.
    - Po utworzeniu budżetu będzie on widoczny w analizie kosztów. Przeglądanie budżetu względem bieżących wydatków jest jednym z pierwszych kroków potrzebnych podczas analizowania kosztów i wydatków.
  - W przypadku przekroczenia progów budżetu można wysyłać powiadomienia e-mail.
  - Dane zarządzania kosztami można wyeksportować do usługi Azure Storage w celu analizy.

    ![Budżet usługi Cost Management](./media/migrate-best-practices-costs/budget.png)
    _Budżet usługi Azure Cost Management_

- **Wykonaj analizę kosztów:** Skorzystaj z analizy kosztów, aby eksplorować i analizować koszty organizacji, aby ułatwić zrozumienie sposobu naliczania kosztów i identyfikowania trendów wydatków.
  - Analiza kosztów jest dostępna dla użytkowników usługi EA.
  - Dane analizy kosztów można wyświetlić dla różnych zakresów, w tym według działu, konta, subskrypcji lub grupy zasobów.
  - Możesz uzyskać analizę kosztów pokazującą łączne koszty dla bieżącego miesiąca oraz skumulowane koszty dzienne.

    ![Rysunek analizy Azure Cost Managementej ](./media/migrate-best-practices-costs/analysis.png)
     _: Analiza Azure Cost Management_
- **Pobierz zalecenia:** Zapoznaj się z zaleceniami klasyfikatora, które pokazują, jak można zoptymalizować i poprawić wydajność.

**Dowiedz się więcej:**

- Zapoznaj się z omówieniem [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview).
- Dowiedz się, jak [zoptymalizować inwestycję w chmurę za pomocą Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices).
- Dowiedz się, jak [używać raportów Azure Cost Management](https://docs.microsoft.com/azure/cost-management/use-reports).
- Zapoznaj się z [samouczkiem dotyczącym optymalizacji kosztów z zaleceń](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations).
- Zapoznaj się z [interfejsem API użycia platformy Azure](https://docs.microsoft.com/rest/api/consumption/budgets).

## <a name="best-practice-monitor-resource-utilization"></a>Najlepsze rozwiązanie: monitorowanie wykorzystania zasobów

Na platformie Azure płacisz za to, z czego korzystasz, gdy zasoby są używane, i nie płacisz, gdy nie są używane. W przypadku maszyn wirtualnych rozliczanie ma miejsce, gdy maszyna wirtualna zostanie przydzielona. Po cofnięciu przydziału maszyny wirtualnej opłaty nie są naliczane. Mając to na uwadze, należy monitorować użycie maszyn wirtualnych i weryfikować ich rozmiar.

- Stale oceniaj obciążenia maszyn wirtualnych, aby określać plany bazowe.
- Jeśli na przykład obciążenie jest często używane od poniedziałku do piątku w godzinach od 8:00 do 18:00, i prawie nie używane poza tymi godzinami, możesz obniżyć poziom maszyn wirtualnych poza godzinami szczytu. Może to oznaczać zmianę rozmiarów maszyn wirtualnych lub użycie zestawów skalowania maszyn wirtualnych w celu automatycznego skalowania maszyn wirtualnych w górę lub w dół.
- Niektóre firmy „usypiają” maszyny wirtualne, stosując dla nich kalendarz, który określa, kiedy powinny być dostępne, a kiedy nie są potrzebne.
- Oprócz monitorowania maszyn wirtualnych, należy monitorować inne zasoby sieciowe, takie jak usługa ExpressRoute i brama sieci wirtualnej, pod kątem nadmiernego i niedostatecznego użycia.
- Użycie maszyny wirtualnej można monitorować za pomocą narzędzi firmy Microsoft, takich jak usługi Azure Cost Management, Azure Monitor i Azure Advisor. Dostępne są również narzędzia innych firm.

**Dowiedz się więcej:**

- Zapoznaj się z omówieniem usług [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) i [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview).
- [Uzyskaj](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) rekomendacje dotyczące kosztów w usłudze Advisor.
- [Dowiedz się, jak [zoptymalizować koszty na podstawie rekomendacji](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations) i [uniknąć nieoczekiwanych opłat](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Dowiedz się więcej o zestawie narzędzi [Azure Resource Optimization (ARO) Toolkit](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Najlepsze rozwiązanie: implementowanie budżetów grup zasobów

Grupy zasobów są często używane w celu reprezentowania granic kosztów. Biorąc pod uwagę ten wzorzec użycia, zespół platformy Azure kontynuuje opracowywanie nowych i udoskonalonych sposobów śledzenia i analizowania wydatków na zasoby na różnych poziomach, z uwzględnieniem możliwości tworzenia budżetów na poziomie grupy zasobów i zasobów.

- Budżet grupy zasobów ułatwia śledzenie kosztów związanych z grupą zasobów.
- Gdy budżet zostanie wykorzystany lub przekroczony, możesz wyzwalać alerty lub uruchamiać wiele różnych podręczników.

**Dowiedz się więcej:**

- [Dowiedz się, jak](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) zarządzać kosztami za pomocą budżetów platformy Azure.
- [Postępuj zgodnie z samouczkiem](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets), aby utworzyć budżet platformy Azure i zarządzać nim.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Najlepsze rozwiązanie: Optymalizowanie Azure Monitor przechowywania

Po przeniesieniu zasobów na platformę Azure i włączeniu dla nich rejestrowania danych diagnostycznych generowanych jest wiele danych dziennika. Zazwyczaj te dane dziennika są wysyłane na konto magazynu, które jest mapowane na obszar roboczy usługi Log Analytics.

- Im dłuższy okres przechowywania danych dziennika, tym więcej masz danych.
- Nie wszystkie dane dziennika są tak samo ważne, a niektóre zasoby generują więcej danych, niż inne.
- Ze względu na przepisy i zgodność, prawdopodobnie dane dzienników dla niektórych zasobów trzeba będzie przechowywać dłużej, niż inne.
- Należy bardzo uważnie rozważyć tę kwestię i zrównoważyć optymalizację kosztów magazynu dzienników i zachowanie potrzebnych danych dziennika.
- Zalecamy ocenę i skonfigurowanie rejestrowania natychmiast po zakończeniu migracji, aby nie wydawać pieniędzy na przechowywanie dzienników, które nie mają znaczenia.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/azure-monitor/platform/usage-estimated-costs) na temat monitorowania użycia i szacowanych kosztów.

## <a name="best-practice-optimize-storage"></a>Najlepsze rozwiązanie: Optymalizowanie magazynu

Jeśli przed migracją magazyn został wybrany zgodnie z najlepszymi rozwiązaniami, prawdopodobnie przynosi to pewne korzyści. Istnieją jednak prawdopodobnie dodatkowe koszty magazynowania, które nadal można zoptymalizować. W miarę upływu czasu obiekty blob i pliki stają się nieaktualne. Dane mogą nie być już używane, ale ze względu na wymagania prawne trzeba je przechowywać przez określony okres. W związku z tym być może nie trzeba przechowywać ich w magazynie o wysokiej wydajności, który był używany na potrzeby pierwotnej migracji.

Identyfikowanie i przenoszenie nieaktualnych danych do tańszych obszarów magazynowania może mieć ogromny wpływ na miesięczny budżet magazynu i oszczędność kosztów. Platforma Azure oferuje wiele sposobów, które ułatwiają identyfikację i przechowywanie tych nieaktualnych danych.

- Korzystaj z zalet warstw dostępu dla magazynu ogólnego przeznaczenia w wersji 2, które umożliwiają przeniesienie mniej ważnych danych z warstwy gorąca do chłodna i archiwalna.
- Użyj rozwiązania StorSimple, które pomoże Ci w przeniesieniu nieaktualnych danych na podstawie zasad niestandardowych.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o warstwach dostępu.
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/azure-monitor/overview) rozwiązania StorSimple i z [cennikiem rozwiązania StorSimple](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Najlepsze rozwiązanie: Automatyzacja optymalizacji maszyn wirtualnych

Celem uruchamiania maszyny wirtualnej w chmurze jest zmaksymalizowanie używanego procesora, pamięci i dysku. Jeśli odkryjesz maszyny wirtualne, które nie są zoptymalizowane lub są nieużywane przez długie okresy czasu, warto je wyłączyć lub skalować je w dół przy użyciu zestawów skalowania maszyn wirtualnych.

Możesz zoptymalizować maszynę wirtualną za pomocą Azure Automation, zestawów skalowania maszyn wirtualnych, automatycznego zamykania oraz rozwiązań opartych na skrypcie lub innych firm.

**Dowiedz się więcej:**

- [Dowiedz się](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision), jak używać pionowego skalowania automatycznego.
- [Zaplanuj](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) automatyczne uruchamianie maszyny wirtualnej.
- [Dowiedz się](https://docs.microsoft.com/azure/automation/automation-solution-vm-management), jak uruchamiać maszyny wirtualne lub zatrzymywać je poza godzinami pracy w usłudze Azure Automation.
- Uzyskaj więcej informacji na temat [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview)i [zestawu narzędzi optymalizacji zasobów platformy Azure (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Najlepsze rozwiązania: używanie Logic Apps i elementów Runbook z interfejsem API budżetów

Platforma Azure oferuje interfejs API REST, który ma dostęp do informacji rozliczeniowych dzierżawy.

- Korzystając z interfejsu API budżetów, można zintegrować systemy zewnętrzne i przepływy pracy wyzwalane przez metryki, które są tworzone na podstawie danych interfejsu API.
- Dane dotyczące użycia i zasobów można pobierać do preferowanych narzędzi do analizy danych.
- Interfejsy API usługi RateCard i użycia zasobów platformy Azure mogą ułatwić dokładne przewidywanie kosztów i zarządzanie nimi.
- Interfejsy API są implementowane jako dostawca zasobów i są uwzględniane w interfejsach API uwidacznianych przez usługę Azure Resource Manager.
- Interfejs API budżetów można zintegrować z usługą Azure Logic Apps i elementami Runbook.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/rest/api/consumption/budgets) o interfejsie API budżetów.
- [Uzyskaj wgląd](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) w użycie platformy Azure za pomocą interfejsu API rozliczeń.

## <a name="best-practice-implement-serverless-technologies"></a>Najlepsze rozwiązanie: implementowanie technologii bezserwerowych

Obciążenia maszyn wirtualnych są często migrowane „w stanie takim, w jakim są”, aby uniknąć przestoju. Często maszyny wirtualne mogą hostować zadania, które są sporadyczne i trwają krótko lub, alternatywnie, wiele godzin. Są to na przykład maszyny wirtualne, na których są uruchamiane zadania zaplanowane, takie jak Harmonogram zadań systemu Windows lub skrypty programu PowerShell. Kiedy te zadania nie są uruchomione, koszty związane z maszyną wirtualną i magazynem dysków i tak są naliczane.

Po migracji i po przeprowadzeniu szczegółowego przeglądu zadań tego typu warto rozważyć zmigrowanie ich do technologii bezserwerowych, takich jak usługa Azure Functions lub zadania usługi Azure Batch. Dzięki takiemu rozwiązaniu nie trzeba już zarządzać maszynami wirtualnymi ani ich konserwować, co zapewnia dodatkowe oszczędności kosztów.

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [Azure Functions](https://azure.microsoft.com/services/functions).
- Dowiedz się więcej o usłudze [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z innymi najlepszymi rozwiązaniami:

- [Najlepsze rozwiązania](./migrate-best-practices-security-management.md) w zakresie zabezpieczeń i zarządzania po migracji.
- [Najlepsze rozwiązania](./migrate-best-practices-networking.md) dotyczące sieci po migracji.
