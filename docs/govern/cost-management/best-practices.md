---
title: Regulowanie i ustalanie wielkości zasobów platformy Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać najlepsze rozwiązania związane z wyceną i ustalaniem wielkości zasobów na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1e175ee448467d9796b1483f66568389fc5d24b0
ms.sourcegitcommit: 825f9ae5b6cdd2fa6cb18c14a9733ba9106194f2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81646878"
---
# <a name="best-practices-for-costing-and-sizing-resources-hosted-in-azure"></a>Najlepsze rozwiązania związane z wyceną i ustalaniem wielkości zasobów hostowanych na platformie Azure

Podczas dostarczania dyscyplin ładu zarządzanie kosztami jest cyklicznym motywem na poziomie przedsiębiorstwa. Dzięki optymalizacji kosztów i zarządzaniu nimi możesz zapewnić długoterminowe sukcesy środowiska platformy Azure. Niezwykle ważne jest, aby wszystkie zespoły (takie jak finanse, zarządzanie i zespoły deweloperów aplikacji) zrozumieć powiązane koszty i regularnie je przeglądać.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule są oparte na funkcjach platformy i usług na platformie Azure, które były dostępne w momencie pisania. Funkcje i możliwości zmieniają się w miarę upływu czasu. Nie wszystkie rekomendacje zostaną zastosowane do wdrożenia, więc wybierz, co najlepiej sprawdza się w danej sytuacji.

## <a name="best-practices-by-team-and-accountability"></a>Najlepsze rozwiązania według zespołu i odpowiedzialności

Zarządzanie kosztami w całym przedsiębiorstwie to funkcja zarządzania chmurą i działania w chmurze. Jednakże wszystkie decyzje związane z zarządzaniem kosztami powodują zmianę zasobów, które obsługują obciążenie. Gdy te zmiany wpłyną na architekturę obciążenia, wymagane są dodatkowe zagadnienia w celu zminimalizowania wpływu na użytkowników końcowych i funkcje biznesowe. Zespół przyznający chmurę, który skonfigurował lub opracował to obciążenie, może obtrzymać odpowiedzialność za ukończenie tych rodzajów zmian.

W tym artykule opisano najlepsze rozwiązania dotyczące dwóch kategorii: najlepszych rozwiązań operacyjnych i najlepszych rozwiązań dotyczących obciążenia. Chociaż zarządzanie, operacje i zespoły adopcji powinny być wyrównane na wszystkich zmianach optymalizacji kosztów, seperation do tych dwóch sekcji ułatwia zilustrowanie, kiedy rozdzielenie cła jest jasne.

## <a name="operational-cost-management-best-practices"></a>Najlepsze rozwiązania związane z zarządzaniem kosztami operacyjnymi

Następujące najlepsze rozwiązania są zwykle wykonywane przez członka zarządu chmury lub zespołu operacji w chmurze, zgodnie z poprawkami i innymi procesami konserwacji zaplanowanej. Każdy z tych najlepszych rozwiązań odwzorowuje wskazówki umożliwiające podjęcie odpowiednich działań w dalszej części artykułu.

- **Tagowanie ma kluczowe znaczenie dla wszystkich rządów:** Upewnij się, że wszystkie obciążenia i zasoby są zgodne z **[właściwymi konwencjami nazewnictwa i znakowania](../../ready/azure-best-practices/naming-and-tagging.md)** i [Wymuś konwencje tagowania przy użyciu usługi Azure](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)
- **Zidentyfikuj możliwości o odpowiednim rozmiarze:** Przejrzyj bieżące wymagania dotyczące wykorzystania zasobów i wydajności w środowisku, aby identyfikować zasoby, które jeszcze nie były używane przez pewien czas (zwykle więcej niż 90 dni).
- **Jednostki SKU o odpowiednim rozmiarze:**: Modyfikuj nieużywany zasób, aby użyć najmniejszego wystąpienia lub jednostki SKU, która może obsługiwać wymagania dotyczące wydajności poszczególnych zasobów.
- Automatyczne **zamykanie dla maszyn wirtualnych:** Jeśli maszyna wirtualna nie jest w użyciu, należy rozważyć automatyczne wyłączenie. Maszyna wirtualna nie zostanie usunięta ani zlikwidowana, ale przestanie zużywać koszty obliczeniowe i pamięci, dopóki nie zostanie ponownie włączona.
- **Automatyczne zamykanie wszystkich nieprodukcyjnych zasobów:**: Jeśli maszyna wirtualna jest częścią środowiska produkcyjnego, w odróżnieniu od środowisk programistycznych należy ustanowić zasady automatycznego zamykania, aby zmniejszyć niewykorzystane koszty. Jeśli jest to możliwe, Skorzystaj z rozwiązań deweloperskich i testowych, aby ułatwić deweloperom utrzymywanie kosztów.
- **Zamknij i likwidowanie niewykorzystanych zasobów:** Tak, podaliśmy ją dwa razy. Jeśli zasób nie został użyty w ciągu ponad 90 dni i nie ma wymaganego przestoju, należy go wyłączyć. Co ważniejsze, jeśli maszyna została zatrzymana lub wyłączona przez ponad 90 dni, Wyłącz obsługę administracyjną i Usuń ten zasób. * Sprawdź, czy wszystkie zasady przechowywania danych są spełnione przy użyciu kopii zapasowej lub innych mechanizmów.
- **Wyczyść dyski oddzielone:** Usuwanie nieużywanego magazynu, szczególnie magazynu maszyn wirtualnych, który nie jest już dołączony do żadnych maszyn wirtualnych.
- **Nadmiarowość w odpowiednim rozmiarze:** Jeśli zasób nie wymaga dużego stopnia nadmiarowości, Usuń magazyn Geograficznie nadmiarowy.
- **Dostosuj parametry automatycznego skalowania:** Montioring operacyjny może odkryte wzorce użycia dla różnych zasobów. Kiedy te wzorce użycia mapują do parametrów używanych do obsługi zachowań automatycznego skalowania, ich wspólne dla zespołu operacji dostosowuje parametry automatycznego skalowania, aby zaspokoić zapotrzebowanie sezonowe &/or zmiany w alokacje budżetu. * Zapoznaj się z najlepszymi rozwiązaniami związanymi z zarządzaniem kosztami dotyczącymi obciążeń.

## <a name="workload-cost-management-best-practices"></a>Najlepsze rozwiązania związane z zarządzaniem kosztami obciążeń

Przed wprowadzeniem zmian w architekturze zapoznaj się z potencjalnym klientem technicznym dla obciążenia. Ułatwiają przegląd obciążeń przy użyciu funkcji [Przegląd architektury platformy Azure](/assessments/?id=azure-architecture-review) i [struktury architektury platformy Azure](/azure/architecture/framework/) , aby podkierować decyzje dotyczące następujących typów zmian architektury.

- **App Services platformy Azure.** Sprawdź wymagania produkcyjne dla wszystkich planów usługi App Service w warstwie Premium. Bez znajomości wymagań firmy dotyczących obciążenia i konfiguracji podstawowych zasobów trudno ustalić, czy wymagany jest plan usługi App Service w warstwie Premium.
- **Pozioma nad skalą pionową.** Użycie wielu małych wystąpień może pozwolić na łatwiejsze skalowanie ścieżki, która jest pojedynczym większym wystąpieniem. Pozwala to na automatyzację skalowania, co powoduje utworzenie optymalizacji kosztów. Jednak aby obciążenie było skalowane w poziomie, zespół techniczny musi sprawdzić, czy aplikacja jest idempotentne. Osiągnięcie skali poziomej może najpierw wymagać zmian w kodzie i konfiguracji różnych warstw aplikacji.
- **Automatycznego skalowania.** Włącz funkcję automatycznego skalowania dla wszystkich usług aplikacji, aby umożliwić nadużycie liczbę mniejszych maszyn wirtualnych. Włączenie automatycznego skalowania ma takie samo wymagania idempotentne, które wymaga poznania architektury obciążenia. Obciążenie i zasoby pomocnicze muszą być zatwierdzone do skalowania w poziomie i automatycznego skalowania przez zespół przyjęcia przed wprowadzeniem jakichkolwiek zmian operacyjnych.
- **Implementuj technologie bezserwerowe:** Obciążenia maszyn wirtualnych są często migrowane "zgodnie z oczekiwaniami", aby uniknąć przestoju. Często maszyny wirtualne mogą hostować zadania, które są sporadyczne i trwają krótko lub, alternatywnie, wiele godzin. Są to na przykład maszyny wirtualne, na których są uruchamiane zadania zaplanowane, takie jak Harmonogram zadań systemu Windows lub skrypty programu PowerShell. Kiedy te zadania nie są uruchomione, koszty związane z maszyną wirtualną i magazynem dysków i tak są naliczane. Po migracji należy rozważyć zmianę architektury warstw obciążenia na technologie bezserwerowe, takie jak Azure Functions lub Azure Batch zadań.

## <a name="actionable-best-practices"></a>Najlepsze rozwiązania dotyczące zasobów z możliwością działania

Pozostała część tego artykułu zawiera taktyczne przykłady najlepszych rozwiązań operacyjnych, które mogą być wykonywane przez zespół ds. zarządzania chmurą lub w chmurze w celu optymalizacji kosztów w całym przedsiębiorstwie.

## <a name="before-adoption"></a>Przed przyjęciem

Przed przeniesieniem obciążeń do chmury oszacuj miesięczny koszt uruchamiania ich na platformie Azure. Proaktywne zarządzanie kosztami chmury pomaga zachować zgodność z budżetem wydatków operacyjnych. Najlepsze rozwiązania w tej sekcji ułatwiają szacowanie kosztów i wykonywanie odpowiednich rozmiarów dla maszyn wirtualnych i magazynu przed wdrożeniem obciążeń w chmurze.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Najlepsze rozwiązanie: oszacowanie miesięcznych kosztów obciążeń

Aby obsłużyć miesięczne rozliczenia zasobów platformy Azure, istnieje kilka narzędzi, których można użyć.

- **Kalkulator cen platformy Azure:** Wybierasz produkty, które chcesz oszacować, na przykład maszyny wirtualne i magazyn. Wprowadzasz koszty do kalkulatora cen, aby utworzyć oszacowanie.

 ![Kalkulator cen platformy Azure](../../migrate/azure-best-practices/media/migrate-best-practices-costs/pricing.png) *Kalkulator cen platformy Azure*

- **Azure Migrate:** Aby oszacować koszty, należy przejrzeć i uwzględnić wszystkie zasoby wymagane do uruchamiania obciążeń na platformie Azure. Aby uzyskać te dane, należy utworzyć spis zasobów, w tym serwerów, maszyn wirtualnych, baz danych i magazynów. Aby zebrać te informacje, można użyć usługi Azure Migrate.

  - Usługa Azure Migrate odnajduje i ocenia Twoje środowisko lokalne w celu dostarczenia spisu.
  - Usługa Azure Migrate może zamapować i pokazać zależności między maszynami wirtualnymi, aby przedstawić pełny obraz.
  - Ocena usługi Azure Migratea zawiera szacowany koszt.
    - **Koszty obliczeń:** Przy użyciu zalecanego rozmiaru maszyny wirtualnej platformy Azure podczas tworzenia oceny, Azure Migrate korzysta z interfejsu API rozliczeń, aby obliczyć szacowane miesięczne koszty maszyn wirtualnych. Oszacowanie bierze pod uwagę ustawienia dotyczące systemu operacyjnego, pakietu Software Assurance, wystąpień zarezerwowanych, czasu działania maszyny wirtualnej, lokalizacji i waluty. Agreguje koszt wszystkich maszyn wirtualnych uwzględnionych w ocenie i oblicza łączny miesięczny koszt obliczeń.
    - **Koszt magazynu:** Azure Migrate oblicza łączne miesięczne koszty magazynowania, sumując koszty magazynowania wszystkich maszyn wirtualnych w ocenie. Możesz obliczyć miesięczny koszt magazynu dla konkretnej maszyny, agregując miesięczny koszt wszystkich podłączonych do niej dysków.

    ![Azure Migrate](../../migrate/azure-best-practices/media/migrate-best-practices-costs/assess.png)
    *Ocena usługi Azure Migrate*

**Dowiedz się więcej:**

- Skorzystaj z [kalkulatora cen platformy Azure](https://azure.microsoft.com/pricing/calculator).
- Zapoznaj się [z omówieniem Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview).
- Przeczytaj informacje na temat [Azure Migrate ocen](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation).
- Dowiedz się więcej na temat [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).

## <a name="best-practice-right-size-vms"></a>Najlepsze rozwiązania: maszyny wirtualne o odpowiednim rozmiarze

Podczas wdrażania maszyn wirtualnych platformy Azure do obsługi obciążeń można wybrać różne opcje. Każdy typ maszyny wirtualnej ma określone funkcje i różne kombinacje procesora CPU, pamięci i dysków. Maszyny wirtualne zostały pogrupowane w sposób przedstawiony poniżej:

**Typ** | **Uzyskać** | **Użycie**
--- | --- | ---
**Zastosowania ogólne** | Zrównoważona moc procesora CPU w stosunku do pamięci. | Dobra opcja na potrzeby testowania i programowania, małych i średnich baz danych oraz serwerów internetowych o niewielkim i średnim ruchu.
**Optymalizacja pod kątem obliczeń** | Duża moc procesora CPU w stosunku do pamięci. | Dobra opcja w przypadku serwerów internetowych o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji.
**Optymalizacja pod kątem pamięci** | Duża ilość pamięci w stosunku do procesora CPU. | Dobra opcja w przypadku relacyjnych baz danych, średnich i dużych pamięci podręcznych oraz analizowania w pamięci.
**Optymalizacja pod kątem magazynu** | Wysoka przepływność dysku i duża liczba operacji we/wy. | Odpowiednie dla baz danych Big Data, SQL i NoSQL.
**Optymalizacja pod kątem procesora GPU** | Wyspecjalizowane maszyny wirtualne. Jeden lub wiele procesorów GPU. | Duże obciążenie grafiką i edytowaniem wideo.
**Wysoka wydajność** | Najszybszy i najbardziej wydajny procesor CPU. Maszyny wirtualne z opcjonalnymi interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA) | Krytyczne aplikacje o wysokiej wydajności.

- Ważne jest, aby zrozumieć różnice cenowe między tymi maszynami wirtualnymi i długoterminowe efekty budżetowe.
- Każdy typ obejmuje kilka serii maszyn wirtualnych.
- Ponadto, kiedy wybierzesz maszynę wirtualną w ramach serii, możesz skalować maszynę wirtualną w górę i w dół w obrębie tej serii. Na przykład maszynę DSv2\_2 można skalować w górę do DSv2\_4, ale nie można zmienić jej serii na przykład na Fsv2\_2.

**Dowiedz się więcej:**

- Dowiedz się więcej o [typach maszyn wirtualnych i](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)rozmiarach oraz rozmiarze mapowania do typów.
- Planowanie [ustalania rozmiarów maszyn wirtualnych](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs).
- Zapoznaj się z [przykładową oceną fikcyjnej firmy Contoso](../../plan/contoso-migration-assessment.md).

## <a name="best-practice-select-the-right-storage"></a>Najlepsze rozwiązanie: wybierz odpowiedni magazyn

Dostrajanie i konserwacja magazynów lokalnych (SAN lub NAS) oraz sieci do ich obsługi może być kosztowne i czasochłonne. Dane plików (magazynu) są często migrowane do chmury, co pomaga zminimalizować nakład pracy związany z zadaniami operacyjnymi i zarządzaniem. Firma Microsoft oferuje kilka opcji przenoszenia danych na platformę Azure. Musisz podjąć decyzje związane z tymi opcjami. Wybranie odpowiedniego typu magazynu dla danych może zaoszczędzić organizacji kilka tysięcy dolarów miesięcznie. Oto kilka kwestii do rozważenia:

- Dane, które nie są dostępne w większości i nie mają krytyczne znaczenie dla firmy, nie powinny być umieszczane w najbardziej kosztownej pamięci masowej.
- Z kolei dla ważnych danych, o krytycznym znaczeniu dla firmy, należy wybrać opcje magazynu w wyższej warstwie.
- Podczas planowania wdrożenia należy pobrać spis danych i sklasyfikować go według ważności, aby zamapować go na najbardziej odpowiedni magazyn. Weź pod uwagę budżet i koszt, a także wydajność. Koszt nie powinien być głównym czynnikiem wpływającym na podejmowanie decyzji. Wybranie najtańszej opcji może wystawić obciążenie na ryzyko związane z wydajnością i dostępnością.

### <a name="storage-data-types"></a>Typy danych magazynów

Platforma Azure udostępnia różne typy danych magazynu.

<!--markdownlint-disable MD033 -->

**Typ danych** | **Uzyskać** | **Wykorzystywani**
--- | --- |  ---
**Obiekty blob** | Zoptymalizowane do przechowywania olbrzymich ilości obiektów niestrukturalnych, takich jak dane tekstowe lub binarne<br/><br/> | Uzyskiwanie dostępu do danych z dowolnego miejsca za pośrednictwem protokołu HTTP/HTTPS. | Używane na potrzeby scenariuszy przesyłania strumieniowego i dostępu losowego. Na przykład w celu udostępniania obrazów i dokumentów bezpośrednio w przeglądarce, strumieniowego przesyłania wideo i audio oraz przechowywania danych kopii zapasowych i odzyskiwania po awarii.
**Pliki** | Zarządzane udziały plików dostępne za pośrednictwem protokołu SMB 3.0 | Używane podczas migrowania lokalnych udziałów plików i w celu obsłużenia wielu żądań dostępu/połączeń do danych plików.
**Dyski** | Oparte na stronicowych obiektach blob.<br/><br/> Typ dysku (prędkość): standardowy (dysk twardy lub SSD) lub Premium (SSD).<br/><br/>Zarządzanie dyskami: niezarządzane (Zarządzanie ustawieniami dysków i magazynem) lub zarządzanie (można wybrać typ dysku, a platforma Azure zarządza dyskiem). | Na potrzeby maszyn wirtualnych używaj dysków w warstwie Premium. Na potrzeby łatwego zarządzania i skalowania używaj dysków zarządzanych.
**Kolejki** | Przechowywanie i pobieranie dużej liczby komunikatów, do których można uzyskać dostęp za pośrednictwem wywołań uwierzytelnionych (HTTP lub HTTPS) | Łączenie składników aplikacji za pomocą asynchronicznego kolejkowania komunikatów.
**Tabele** | Przechowuje tabele. | Teraz jest to część interfejsu API tabeli usługi Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Poziomy dostępu

Magazyn platformy Azure oferuje różne opcje uzyskiwania dostępu do danych blokowych obiektów blob. Wybranie odpowiedniej warstwy dostępu pozwala zapewnić, że dane blokowych obiektów blob są przechowywane w najbardziej opłacalny sposób.

<!--markdownlint-disable MD033 -->

**Typ** | **Uzyskać** | **Wykorzystywani**
--- | --- | ---
**Gorąca** | Wyższy koszt przechowywania, niż w warstwie Chłodna. Niższe opłaty za dostęp, niż w warstwie Chłodna.<br/><br/>Jest to warstwa domyślna. | Służy do przechowywania danych w przypadku aktywnego użycia, gdy dostęp do danych jest uzyskiwany często.
**Chłodna** | Niższy koszt przechowywania, niż w warstwie Gorąca. Wyższe opłaty za dostęp, niż w warstwie Gorąca.<br/><br/> Przechowywanie przez co najmniej 30 dni. | Przechowywanie krótkoterminowe, dane są dostępne, ale dostęp do nich jest uzyskiwany rzadko.
**Archiwum** | Używana na potrzeby pojedynczych blokowych obiektów blob.<br/><br/> Najbardziej ekonomiczna opcja magazynu. Dostęp do danych jest droższy, niż w warstwach Gorąca i Chłodna. | Używana na potrzeby danych, które można pobierać z opóźnieniem kilku godzin i które pozostaną w tej warstwie przez co najmniej 180 dni.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy konta magazynu

Platforma Azure oferuje różne typy kont magazynu i warstw wydajności.

<!--markdownlint-disable MD033 -->

**Typ konta** | **Uzyskać** | **Wykorzystywani**
--- | --- | ---
**Ogólnego przeznaczenia w wersji 2, Standardowa** | Obsługuje obiekty blob (blokowe, stronicowe, dołączania), pliki, dyski, kolejki i tabele.<br/><br/> Obsługuje warstwy dostępu Gorąca, Chłodna i Archiwum. Magazyn strefowo nadmiarowy (ZRS) jest obsługiwany. | Używane w przypadku większości scenariuszy i większości typów danych. Konta magazynu w warstwie Standardowa mogą być oparte na dyskach HDD lub SSD.
**Ogólnego przeznaczenia w wersji 2, Premium** | Obsługuje dane magazynu obiektów blob (stronicowe obiekty blob). Obsługuje warstwy dostępu Gorąca, Chłodna i Archiwum. Magazyn strefowo nadmiarowy jest obsługiwany.<br/><br/> Dane są przechowywane na dysku SSD. | Firma Microsoft zaleca używanie tego typu konta dla wszystkich maszyn wirtualnych.
**Ogólnego przeznaczenia, wersja 1** | Obsługa warstw dostępu nie jest obsługiwana. Nie obsługuje magazynu strefowo nadmiarowego | Używane, jeśli aplikacje potrzebują klasycznego modelu wdrażania platformy Azure.
**Obiekt blob** | Specjalne konto magazynu do przechowywania obiektów bez struktury. Zapewnia blokowe obiekty blob i tylko dołączanie obiektów BLOB (bez plików, kolejek, tabel lub usług magazynu). Zapewnia taką samą trwałość, dostępność, skalowalność i wydajność jak Ogólnego przeznaczenia v2. | Na tych kontach nie można przechowywać stronicowych obiektów blob, a zatem nie można przechowywać plików VHD. Warstwę dostępu można ustawić na Gorącą lub Chłodną.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Opcje nadmiarowości magazynu

Konta magazynu mogą wykorzystywać różne typy nadmiarowości na potrzeby zapewnienia odporności i wysokiej dostępności.

**Typ** | **Uzyskać** | **Wykorzystywani**
--- | --- | ---
**Magazyn lokalnie nadmiarowy (LRS)** | Chroni przed awarią lokalną przez replikację w ramach pojedynczej jednostki magazynowej do oddzielnej domeny błędów i domeny aktualizacji. Przechowuje wiele kopii danych w jednym centrum danych. Zapewnia co najmniej 99,999999999% czasu trwałości obiektów w danym roku. | Warte rozważenia, jeśli aplikacja przechowuje dane, które można łatwo odtworzyć.
**Magazyn strefowo nadmiarowy (ZRS)** | Chroni przed awarią centrum danych przez replikowanie w trzech klastrach magazynu w jednym regionie. Każdy klaster magazynu jest fizycznie oddzielony i zlokalizowany we własnej strefie dostępności. Zapewnia co najmniej 99,9999999999 procentową trwałość obiektów w danym roku przez przechowywanie wielu kopii danych w wielu centrach lub regionach. | Warto rozważyć, jeśli potrzebujesz spójności, trwałości i wysokiej dostępności. Może nie chronić przed awarią regionalną, jeśli ma ona trwały wpływ na wiele stref.
**Magazyn geograficznie nadmiarowy (GRS)** | Chroni przed awarią całego regionu przez replikowanie danych do regionu pomocniczego, który ma setki kilometrów od początku. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Dane repliki są niedostępne, dopóki firma Microsoft nie zainicjuje przejścia w tryb failover do regionu pomocniczego. Jeśli nastąpi przełączenie w tryb failover, możliwy jest dostęp do odczytu i zapisu.
**Dostęp do odczytu z magazynu geograficznie nadmiarowego (RA-GRS)** | Podobne do GRS. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Zapewnia dostępność i 99,99% odczytu, umożliwiając dostęp do odczytu z drugiego regionu używanego przez GRS.

**Dowiedz się więcej:**

- [Przejrzyj](https://azure.microsoft.com/pricing/details/storage) cennik usługi Azure Storage.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) Usługa Azure Import/Export umożliwia wdrażanie dużych ilości danych w obiektach Blob i plikach platformy Azure.
- [Porównaj](https://docs.microsoft.com/azure/storage/common/storage-introduction?toc=/azure/storage/blobs/toc.json) typy danych magazynu, takie jak obiekty blob, pliki i dyski.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers) o warstwach dostępu.
- [Przejrzyj](https://docs.microsoft.com/azure/storage/common/storage-account-overview?toc=/azure/storage/blobs/toc.json) różne typy kont magazynu.
- Dowiedz się więcej o [nadmiarowości usługi Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy), w tym LRS, ZRS, GRS i dostęp do odczytu.
- Dowiedz się więcej o [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="after-adoption"></a>Po przyjęciu

Przed przyjęciem prognozy kosztów są zależne od decyzji podejmowanych przez właścicieli obciążeń i zespół ds. wdrażania chmury. Chociaż zespół nadzoru może pomóc w wpływie tych decyzji, może być konieczne wykonanie niewielkiej akcji dla zespołu rządowego.

Gdy zasoby są w środowisku produkcyjnym, dane mogą być agregowane i trendy analizowane na poziomie środowiska. Te dane ułatwiają zespołowi nadzoru podejmowanie decyzji o wielkości i użyciu niezależnie od rzeczywistych wzorców użytkowania i bieżącej architektury stanu.

- Analizuj dane, aby wygenerować linię bazową budżetu dla grup zasobów i zasobów platformy Azure.
- Identyfikuj wzorce użycia, które umożliwiają zredukowanie rozmiaru i/lub zatrzymanie/wstrzymanie zasobów w celu dodatkowego obniżenia kosztów.

Najlepsze rozwiązania w tej sekcji obejmują korzystanie z zalet hybrydowych platformy Azure oraz zarezerwowanych maszyn wirtualnych, zmniejszenie wydatków w chmurze w ramach subskrypcji przy użyciu Azure Cost Management do budżetowania i analizy kosztów, monitorowania zasobów oraz implementowania budżetów grup zasobów oraz optymalizowania monitorowania, magazynu i maszyn wirtualnych.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Najlepsze rozwiązanie: korzystanie z korzyści użycia hybrydowego platformy Azure

Dzięki wieloletnim inwestycjom w oprogramowanie systemów, takich jak Windows Server i SQL Server, firma Microsoft ma niepowtarzalną możliwość zaoferowania klientom wartości w chmurze ze znacznymi rabatami, na które inni dostawcy usług w chmurze niekoniecznie mogą sobie pozwolić.

Zintegrowane portfolio produktów firmy Microsoft, obejmujące środowisko lokalne i platformę Azure, stanowi przewagę konkurencyjną i ekonomiczną. Jeśli obecnie posiadasz licencję systemu operacyjnego lub innego oprogramowania w ramach pakietu Software Assurance (SA), możesz przenieść te licencje do chmury za pośrednictwem programu Korzyść użycia hybrydowego platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj się](https://azure.microsoft.com/pricing/hybrid-benefit) z kalkulatorem korzyści użycia hybrydowego.
- [Dowiedz się więcej](https://azure.microsoft.com/pricing/hybrid-benefit) o korzyści użycia hybrydowego dla systemu Windows Server.
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-use-reserved-vm-instances"></a>Najlepsze rozwiązanie: korzystanie z wystąpień zarezerwowanych maszyn wirtualnych

Większość platform w chmurze jest skonfigurowana pod kątem płatności zgodnie z rzeczywistym użyciem. Ten model zawiera wady, ponieważ nie zawsze wiadomo, jak dynamiczne będą obciążenia. Kiedy określasz jasne intencje dla obciążenia, bierzesz udział w planowaniu infrastruktury.

Korzystając z wystąpień zarezerwowanych maszyn wirtualnych platformy Azure, opłacasz z góry na rok lub trzy lata wystąpienie maszyny wirtualnej.

- Przedpłata wiąże się z rabatem na używane zasoby.
- Możesz znacząco obniżyć koszty maszyn wirtualnych, obliczeń w usłudze SQL Database, usługi Azure Cosmos DB lub innych zasobów nawet o 72% w porównaniu z cenami w modelu płatności zgodnie z rzeczywistym użyciem.
- Rezerwacje umożliwiają skorzystanie z rabatu na rozliczenia i nie mają wpływu na stan środowiska uruchomieniowego Twoich zasobów.
- Wystąpienia zarezerwowane można anulować.

![Wystąpienia zarezerwowane](../../migrate/azure-best-practices/media/migrate-best-practices-costs/reserve.png)
*Zarezerwowane maszyny wirtualne platformy Azure*

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) o rezerwacjach platformy Azure.
- [Przeczytaj](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) często zadawane pytania dotyczące wystąpień zarezerwowanych.
- [Uzyskaj wskazówki dotyczące cen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Najlepsze rozwiązanie: agregowanie wydatków w chmurze w ramach subskrypcji

To nieuniknione, że w końcu będziesz mieć więcej niż jedną subskrypcję platformy Azure. Możesz na przykład potrzebować dodatkowej subskrypcji w celu rozdzielenia granic środowiska deweloperskiego i produkcyjnego lub możesz mieć platformę, która wymaga oddzielnej subskrypcji dla każdego klienta. Możliwość agregowania raportowania danych ze wszystkich subskrypcji na jednej platformie jest wartościową funkcją.

W tym celu można użyć interfejsów API usługi Azure Cost Management. Następnie, po zagregowaniu danych do jednego źródła, takiego jak baza danych SQL Azure, można użyć narzędzi, takich jak usługa Power BI, aby uwidocznić zagregowane dane. Można tworzyć zagregowane raporty subskrypcji i raporty szczegółowe. Na przykład w przypadku użytkowników, którzy potrzebują proaktywnie wglądu w koszty zarządzania, można utworzyć określone widoki kosztów na podstawie działów, grup zasobów lub innych informacji. Nie musisz zapewniać im pełnego dostępu do danych rozliczeniowych platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) interfejsu API użycia platformy Azure.
- [Dowiedz się więcej](https://docs.microsoft.com/power-bi/desktop-connect-azure-consumption-insights) na temat nawiązywania połączenia z usługą Azure Consumption Insights w programie Power BI Desktop.
- [Dowiedz się](https://docs.microsoft.com/azure/billing/billing-manage-access), jak zarządzać dostępem do informacji rozliczeniowych dla platformy Azure przy użyciu kontroli dostępu opartej na rolach (RBAC).

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
- Dowiedz się, jak [zoptymalizować koszty z zaleceń](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/toc.json)i [uniknąć nieoczekiwanych opłat](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Dowiedz się więcej o zestawie narzędzi [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-reduce-non-production-costs"></a>Najlepsze rozwiązanie: zmniejszanie kosztów nieprodukcyjnych

Środowiska programistyczne, testowe i gwarancja jakości są niezbędne podczas cyklu projektowania. Niestety, w przypadku tych środowisk często nie ma potrzeby obsługi administracyjnej, gdy przestaną być przydatne. Regularne przegląd nieużywanych środowisk nieprodukcyjnych może mieć bezpośredni wpływ na koszty.

Dodatkowo należy wziąć pod uwagę ogólne obniżki kosztów w środowiskach nieprodukcyjnych:

- Zmniejsz ilość zasobów nieprodukcyjnych, aby korzystać z niższych ilości kosztów maszyn wirtualnych serii B i magazynu w warstwie Standardowa.
- Zastosuj zasady platformy Azure, aby wymagać obniżenia kosztów zasobów dla wszystkich zasobów nieprodukcyjnych.

**Dowiedz się więcej:**

- [Użyj tagów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) do identyfikowania celów deweloperskich, testowych lub pytań i odpowiedzi w celu zmiany rozmiarów i/lub zakończenia.
- [Maszyny wirtualne Autozamykania](https://docs.microsoft.com/azure/cost-management-billing/manage/getting-started#consider-cost-cutting-features-like-auto-shutdown-for-vms) ustawiają nocny czas zakończenia dla maszyn wirtualnych. Korzystanie z tej funkcji spowoduje zatrzymanie nieprodukcyjnych maszyn wirtualnych w każdej porze nocnej, co wymaga od deweloperów ponownego uruchomienia tych maszyn wirtualnych, gdy będą one gotowe do wznowienia rozwoju.
- Zachęcaj zespoły programistyczne do używania [Azure DevTest Labs](https://docs.microsoft.com/azure/lab-services/devtest-lab-overview) , aby określić własne podejścia do kontroli kosztów i uniknąć wpływu standardowego chronometrażu automatycznego zamykania w poprzednim kroku.

## <a name="best-practice-use-azure-cost-management"></a>Najlepsze rozwiązanie: Użyj Azure Cost Management

Firma Microsoft oferuje usługę Azure Cost Management, która ułatwia śledzenie wydatków:

- Ułatwia monitorowanie i kontrolowanie wydatków na platformę Azure oraz optymalizowanie użycia zasobów.
- Przegląda całą subskrypcję i wszystkie jej zasoby oraz wyświetla rekomendacje.
- Oferuje pełny interfejs API do integrowania zewnętrznych narzędzi i systemów finansowych na potrzeby raportowania.
- Śledzi użycie zasobów i zarządza kosztami chmury przy użyciu pojedynczego, ujednoliconego widoku.
- Dostarcza rozbudowane szczegółowe informacje operacyjne i finansowe, które ułatwiają podejmowanie świadomych decyzji.

W usłudze Cost Management możesz wykonywać następujące zadania:

- **Utwórz budżet:** Utwórz budżet dla odpowiedzialności finansowej.
  - Możesz uwzględnić usługi, których używasz, lub zasubskrybować określony okres (miesięcznie, kwartalnie, rocznie) i zakres (subskrypcje/grupy zasobów). Możesz na przykład utworzyć budżet subskrypcji platformy Azure dla okresu miesięcznego, kwartalnego lub rocznego.
    - Po utworzeniu budżetu będzie on widoczny w analizie kosztów. Przeglądanie budżetu względem bieżących wydatków jest jednym z pierwszych kroków potrzebnych podczas analizowania kosztów i wydatków.
  - W przypadku przekroczenia progów budżetu można wysyłać powiadomienia e-mail.
  - Dane zarządzania kosztami można wyeksportować do usługi Azure Storage w celu analizy.

    ![Budżet usługi Cost Management](../../migrate/azure-best-practices/media/migrate-best-practices-costs/budget.png)
    *Budżet usługi Azure Cost Management*

- **Wykonaj analizę kosztów:** Skorzystaj z analizy kosztów, aby eksplorować i analizować koszty organizacji, aby ułatwić zrozumienie sposobu naliczania kosztów i identyfikowania trendów wydatków.
  - Analiza kosztów jest dostępna dla użytkowników usługi EA.
  - Można wyświetlić dane analizy kosztów dla różnych zakresów, w tym według działu, konta, subskrypcji lub grupy zasobów.
  - Możesz uzyskać analizę kosztów pokazującą łączne koszty dla bieżącego miesiąca oraz skumulowane koszty dzienne.

    ![Analiza usługi Cost Management](../../migrate/azure-best-practices/media/migrate-best-practices-costs/analysis.png)
    *Analiza usługi Azure Cost Management*

- **Pobierz zalecenia:** Zapoznaj się z zaleceniami klasyfikatora, które pokazują, jak można zoptymalizować i poprawić wydajność.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/cost-management/overview) usługi Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) zoptymalizować inwestycję w chmurę za pomocą usługi Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management/use-reports) używać raportów usługi Azure Cost Management.
- [Zapoznaj się z samouczkiem](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=/azure/billing/toc.json) dotyczącym optymalizowania kosztów za pomocą rekomendacji.
- [Przejrzyj](https://docs.microsoft.com/rest/api/consumption/budgets) interfejs API użycia platformy Azure.

## <a name="best-practice-implement-resource-group-budgets"></a>Najlepsze rozwiązanie: implementowanie budżetów grup zasobów

Grupy zasobów są często używane w celu reprezentowania granic kosztów. Biorąc pod uwagę ten wzorzec użycia, zespół platformy Azure kontynuuje opracowywanie nowych i udoskonalonych sposobów śledzenia i analizowania wydatków na zasoby na różnych poziomach, z uwzględnieniem możliwości tworzenia budżetów na poziomie grupy zasobów i zasobów.

- Budżet grupy zasobów ułatwia śledzenie kosztów związanych z grupą zasobów.
- Gdy budżet zostanie wykorzystany lub przekroczony, możesz wyzwalać alerty lub uruchamiać wiele różnych podręczników.

**Dowiedz się więcej:**

- [Dowiedz się, jak](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) zarządzać kosztami za pomocą budżetów platformy Azure.
- [Postępuj zgodnie z samouczkiem](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/billing/toc.json), aby utworzyć budżet platformy Azure i zarządzać nim.

## <a name="best-practice-review-azure-advisor-recommendations"></a>Najlepsze rozwiązanie: przegląd Azure Advisor zaleceń

Azure Advisor zalecenia dotyczące kosztów określają możliwości obniżenia kosztów. Gdy budżety pojawiają się o wysokim poziomie lub użycie jest niskie, użyj tego raportu, aby szybko wyrównać koszty.

**Dowiedz się więcej:**

- [Przejrzyj zalecenia dotyczące kosztów Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) , aby podjąć natychmiastowe działania.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Najlepsze rozwiązanie: Optymalizowanie Azure Monitor przechowywania

Po przeniesieniu zasobów na platformę Azure i włączeniu dla nich rejestrowania danych diagnostycznych generowanych jest wiele danych dziennika. Zazwyczaj te dane dziennika są wysyłane na konto magazynu, które jest mapowane na obszar roboczy usługi Log Analytics.

- Im dłuższy okres przechowywania danych dziennika, tym więcej masz danych.
- Nie wszystkie dane dziennika są tak samo ważne, a niektóre zasoby generują więcej danych, niż inne.
- Ze względu na przepisy i zgodność, prawdopodobnie dane dzienników dla niektórych zasobów trzeba będzie przechowywać dłużej, niż inne.
- Równowaga między optymalizowaniem kosztów magazynu dzienników i przechowywaniem potrzebnych danych dziennika.
- Zalecamy ocenę i skonfigurowanie rejestrowania natychmiast po zakończeniu migracji, aby nie wydawać pieniędzy na przechowywanie dzienników, które nie mają znaczenia.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) na temat monitorowania użycia i szacowanych kosztów.

## <a name="best-practice-optimize-storage"></a>Najlepsze rozwiązanie: Optymalizowanie magazynu

W przypadku zastosowania najlepszych rozwiązań w zakresie wybierania magazynu przed wdrożeniem prawdopodobnie wykorzystaniu pewne korzyści. Istnieją jednak prawdopodobnie dodatkowe koszty magazynowania, które nadal można zoptymalizować. W miarę upływu czasu obiekty blob i pliki stają się nieaktualne. Dane mogą nie być już używane, ale ze względu na wymagania prawne trzeba je przechowywać przez określony okres. W związku z tym może nie być konieczne przechowywanie go w magazynie o wysokiej wydajności, który został użyty do oryginalnego wdrożenia.

Identyfikowanie i przenoszenie nieaktualnych danych do tańszych obszarów magazynowania może mieć ogromny wpływ na miesięczny budżet magazynu i oszczędność kosztów. Platforma Azure oferuje wiele sposobów, które ułatwiają identyfikację i przechowywanie tych nieaktualnych danych.

- Skorzystaj z zalet warstw dostępu dla magazynu ogólnego przeznaczenia w wersji 2, przenosząc mniej ważne dane z warstwy gorąca do chłodna i archiwalna.
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
- [Uzyskaj więcej informacji] o usłudze [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) i zestawie narzędzi [Azure Resource Optimization (ARO) Toolkit](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Najlepsze rozwiązania: używanie Logic Apps i elementów Runbook z interfejsem API budżetów

Platforma Azure udostępnia interfejs API REST, który może uzyskiwać dostęp do informacji rozliczeniowych dzierżawy.

- Korzystając z interfejsu API budżetów, można zintegrować systemy zewnętrzne i przepływy pracy wyzwalane przez metryki, które są tworzone na podstawie danych interfejsu API.
- Dane dotyczące użycia i zasobów można pobierać do preferowanych narzędzi do analizy danych.
- Interfejsy API usługi RateCard i użycia zasobów platformy Azure mogą ułatwić dokładne przewidywanie kosztów i zarządzanie nimi.
- Interfejsy API są implementowane jako dostawca zasobów i są uwzględniane w interfejsach API uwidacznianych przez usługę Azure Resource Manager.
- Interfejs API budżetów można zintegrować z usługą Azure Logic Apps i elementami Runbook.

**Dowiedz się więcej:**

- [Dowiedz się więcej](https://docs.microsoft.com/rest/api/consumption/budgets) o interfejsie API budżetów.
- [Uzyskaj wgląd](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) w użycie platformy Azure za pomocą interfejsu API rozliczeń.


## <a name="next-steps"></a>Następne kroki

Mając świadomość najlepszych rozwiązań, przejrzyj [Cost Management łańcucha narzędzi](./toolchain.md) , aby zidentyfikować narzędzia i funkcje platformy Azure, które ułatwiają wykonywanie tych najlepszych praktyk.

> [!div class="nextstepaction"]
> [Cost Management łańcucha narzędzi dla platformy Azure](./toolchain.md)
