---
title: Regulowanie i ustalanie wielkości zasobów platformy Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać najlepsze rozwiązania związane z wyceną i ustalaniem wielkości zasobów na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ad35877a912fd9d52a74c7f44c91bd9fedb559a5
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755128"
---
<!-- docsTest:ignore ARO -->

# <a name="best-practices-for-costing-and-sizing-resources-hosted-in-azure"></a>Najlepsze rozwiązania związane z wyceną i ustalaniem wielkości zasobów hostowanych na platformie Azure

Podczas dostarczania dyscyplin ładu zarządzanie kosztami jest cyklicznym motywem na poziomie przedsiębiorstwa. Dzięki optymalizacji kosztów i zarządzaniu nimi możesz zapewnić długoterminowe sukcesy środowiska platformy Azure. Niezwykle ważne jest, aby wszystkie zespoły (takie jak finanse, zarządzanie i zespoły deweloperów aplikacji) zrozumieć powiązane koszty i regularnie je przeglądać.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule są oparte na funkcjach platformy i usług na platformie Azure, które były dostępne w momencie pisania. Funkcje i możliwości zmieniają się w miarę upływu czasu. Nie wszystkie rekomendacje zostaną zastosowane do wdrożenia, więc wybierz, co najlepiej sprawdza się w danej sytuacji.

## <a name="best-practices-by-team-and-accountability"></a>Najlepsze rozwiązania według zespołu i odpowiedzialności

Zarządzanie kosztami w całym przedsiębiorstwie to funkcja zarządzania chmurą i działania w chmurze. Wszystkie decyzje dotyczące zarządzania kosztami powodują zmianę zasobów, które obsługują obciążenie. Gdy te zmiany wpłyną na architekturę obciążenia, wymagane są dodatkowe zagadnienia w celu zminimalizowania wpływu na użytkowników końcowych i funkcje biznesowe. Zespół przyznający chmurę, który skonfigurował lub opracował to obciążenie, może obtrzymać odpowiedzialność za ukończenie tych rodzajów zmian.

- **Tagowanie ma kluczowe znaczenie dla wszystkich rządów.** Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa i znakowania](../../ready/azure-best-practices/naming-and-tagging.md) i [Wymuś konwencje tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)
- **Zidentyfikuj możliwości o odpowiednim rozmiarze.** Przejrzyj bieżące wymagania dotyczące wykorzystania zasobów i wydajności w całym środowisku.
- **Zmień rozmiar:** Zmodyfikuj każdy zasób, aby użyć najmniejszego wystąpienia lub jednostki SKU, które może obsługiwać wymagania dotyczące wydajności poszczególnych zasobów.
- **Pozioma nad skalą pionową.** Użycie wielu małych wystąpień może pozwolić na łatwiejsze skalowanie ścieżki, która jest pojedynczym większym wystąpieniem. Pozwala to na automatyzację skalowania, co powoduje utworzenie optymalizacji kosztów.

## <a name="operational-cost-management-best-practices"></a>Najlepsze rozwiązania związane z zarządzaniem kosztami operacyjnymi

Następujące najlepsze rozwiązania są zwykle wykonywane przez członka zarządu chmury lub zespołu operacji w chmurze, zgodnie z poprawkami i innymi procesami konserwacji zaplanowanej. Każdy z tych najlepszych rozwiązań odwzorowuje wskazówki dotyczące podejmowania działań w dalszej części tego artykułu.

- **Tagowanie ma kluczowe znaczenie dla wszystkich rządów:** Upewnij się, że wszystkie obciążenia i zasoby są zgodne z [właściwymi konwencjami nazewnictwa i znakowania](../../ready/azure-best-practices/naming-and-tagging.md) i [Wymuś konwencje tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags)
- **Zidentyfikuj możliwości o odpowiednim rozmiarze:** Przejrzyj bieżące wymagania dotyczące wykorzystania zasobów i wydajności w środowisku, aby zidentyfikować zasoby, które pozostawały niedostatecznie wykorzystane przez pewien czas (zwykle więcej niż 90 dni).
- Alokacje **jednostek SKU o odpowiednim rozmiarze:** Zmodyfikuj nieużywany zasób, aby użyć najmniejszego wystąpienia lub jednostki SKU, które może obsługiwać wymagania dotyczące wydajności poszczególnych zasobów.
- Automatyczne **zamykanie dla maszyn wirtualnych:** Jeśli maszyna wirtualna nie jest w użyciu, należy rozważyć automatyczne wyłączenie. Maszyna wirtualna nie zostanie usunięta ani zlikwidowana, ale przestanie zużywać koszty obliczeniowe i pamięci, dopóki nie zostanie ponownie włączona.
- Automatyczne **Zamykanie wszystkich zasobów nieprodukcyjnych:** Jeśli maszyna wirtualna jest częścią środowiska produkcyjnego, w odróżnieniu od środowiska deweloperskiego, należy ustanowić zasady Autozamykania, aby zmniejszyć niewykorzystane koszty. Jeśli to możliwe, użyj Azure DevTest Labs jako opcji samoobsługowej, aby ułatwić deweloperom popełnienie konta kosztem.
- **Zamknij i likwidowanie niewykorzystanych zasobów:** Tak, podaliśmy ją dwa razy. Jeśli zasób nie został użyty w ciągu ponad 90 dni i nie ma wymaganego przestoju, należy go wyłączyć. Co ważniejsze, jeśli maszyna została zatrzymana lub wyłączona przez ponad 90 dni, Wyłącz obsługę administracyjną i Usuń ten zasób. Sprawdź, czy wszystkie zasady przechowywania danych są spełnione przy użyciu kopii zapasowej lub innych mechanizmów.
- **Wyczyść dyski oddzielone:** Usuwanie nieużywanego magazynu, szczególnie magazynu maszyn wirtualnych, który nie jest już dołączony do żadnych maszyn wirtualnych.
- **Nadmiarowość w odpowiednim rozmiarze:** Jeśli zasób nie wymaga dużego stopnia nadmiarowości, Usuń magazyn Geograficznie nadmiarowy.
- **Dostosuj parametry automatycznego skalowania:** Monitorowanie operacyjne prawdopodobnie nie obejmuje wzorców użycia dla różnych zasobów. Kiedy te wzorce użycia mapują na parametry używane do tworzenia zachowań skalowania automatycznego, często zespół operacyjny może dostosować parametry automatycznego skalowania, aby zaspokoić zapotrzebowanie sezonowe lub zmiany w ramach alokacji budżetu. Zapoznaj się z najlepszymi rozwiązaniami związanymi z zarządzaniem kosztem obciążenia

## <a name="workload-cost-management-best-practices"></a>Najlepsze rozwiązania związane z zarządzaniem kosztami obciążeń

Przed wprowadzeniem zmian w architekturze zapoznaj się z potencjalnym klientem technicznym dla obciążenia. Ułatwiają przegląd obciążenia, korzystając z [dobrze zaprojektowanej Microsoft Azure przeglądowej](https://docs.microsoft.com/assessments/?id=azure-architecture-review) i [Microsoft Azure dobrze zaprojektowanej struktury](https://docs.microsoft.com/azure/architecture/framework) do podejmowania decyzji dotyczących następujących typów zmian architektury.

- **Azure App Service.** Sprawdź wymagania produkcyjne dla wszystkich planów App Service warstwy Premium. Bez znajomości wymagań firmy związanych z obciążeniem i podstawową konfiguracją zasobów, trudno ustalić, czy wymagany jest plan warstwy Premium.
- **Pozioma nad skalą pionową.** Użycie wielu małych wystąpień może pozwolić na łatwiejsze skalowanie ścieżki, która jest pojedynczym większym wystąpieniem. Pozwala to na automatyzację skalowania, co powoduje utworzenie optymalizacji kosztów. Aby obciążenie było skalowane w poziomie, zespół techniczny musi sprawdzić, czy aplikacja jest idempotentne. Osiągnięcie skali poziomej może najpierw wymagać zmian w kodzie i konfiguracji różnych warstw aplikacji.
- **Automatycznego skalowania.** Włącz funkcję automatycznego skalowania dla wszystkich usług aplikacji, aby umożliwić nadużycie liczbę mniejszych maszyn wirtualnych. Włączenie automatycznego skalowania ma takie samo wymagania idempotentne, które wymaga poznania architektury obciążenia. Obciążenie i zasoby pomocnicze muszą być zatwierdzone do skalowania w poziomie i automatycznego skalowania przez zespół przyjęcia przed wprowadzeniem jakichkolwiek zmian operacyjnych.
- **Implementuj technologie bezserwerowe:** Obciążenia maszyn wirtualnych są często migrowane "zgodnie z oczekiwaniami", aby uniknąć przestoju. Często maszyny wirtualne mogą hostować zadania, które są sporadyczne i trwają krótko lub, alternatywnie, wiele godzin. Są to na przykład maszyny wirtualne, na których są uruchamiane zadania zaplanowane, takie jak Harmonogram zadań systemu Windows lub skrypty programu PowerShell. Kiedy te zadania nie są uruchomione, koszty związane z maszyną wirtualną i magazynem dysków i tak są naliczane. Po migracji należy rozważyć przeprowadzenie ponownej architektury warstw obciążenia do technologii bezserwerowych, takich jak Azure Functions lub Azure Batch zadań.

## <a name="actionable-best-practices"></a>Najlepsze rozwiązania dotyczące zasobów z możliwością działania

Pozostała część tego artykułu zawiera taktyczne przykłady najlepszych rozwiązań operacyjnych, które mogą być wykonywane przez zespół ds. zarządzania chmurą lub w chmurze w celu optymalizacji kosztów w całym przedsiębiorstwie.

## <a name="before-adoption"></a>Przed przyjęciem

Przed przeniesieniem obciążeń do chmury oszacuj miesięczny koszt uruchamiania ich na platformie Azure. Proaktywne zarządzanie kosztami chmury pomaga zachować zgodność z budżetem wydatków operacyjnych. Najlepsze rozwiązania w tej sekcji ułatwiają szacowanie kosztów i wykonywanie odpowiednich rozmiarów dla maszyn wirtualnych i magazynu przed wdrożeniem obciążeń w chmurze.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Najlepsze rozwiązanie: oszacowanie miesięcznych kosztów obciążeń

Aby obsłużyć miesięczne rozliczenia zasobów platformy Azure, istnieje kilka narzędzi, których można użyć.

<!-- TODO: Change "input costs" -->
- **Kalkulator cen platformy Azure:** Wybierz produkty, które chcesz oszacować, na przykład maszyny wirtualne i magazyn, a następnie wprowadź koszty do kalkulatora, aby utworzyć oszacowanie.

    ![Kalkulator cen platformy Azure](../../migrate/azure-best-practices/media/migrate-best-practices-costs/pricing.png) _Kalkulator cen platformy Azure_

- **Azure Migrate:** Aby oszacować koszty, należy przejrzeć i uwzględnić wszystkie zasoby wymagane do uruchamiania obciążeń na platformie Azure. Aby uzyskać te dane, należy utworzyć spis zasobów, w tym serwerów, maszyn wirtualnych, baz danych i magazynów. Aby zebrać te informacje, można użyć usługi Azure Migrate.
  - Usługa Azure Migrate odnajduje i ocenia Twoje środowisko lokalne w celu dostarczenia spisu.
  - Usługa Azure Migrate może zamapować i pokazać zależności między maszynami wirtualnymi, aby przedstawić pełny obraz.
  - Ocena usługi Azure Migratea zawiera szacowany koszt.
    - **Koszty obliczeń:** Przy użyciu zalecanego rozmiaru maszyny wirtualnej platformy Azure podczas tworzenia oceny Azure Migrate używa interfejsy API rozliczeń platformy Azure do obliczania szacowanego miesięcznego kosztu maszyny wirtualnej. Oszacowanie uwzględnia system operacyjny, program Software Assurance, zarezerwowane wystąpienia, czas działania maszyny wirtualnej, lokalizację i ustawienia waluty. Agreguje koszt wszystkich maszyn wirtualnych uwzględnionych w ocenie i oblicza łączny miesięczny koszt obliczeń.
    - **Koszt magazynu:** Azure Migrate oblicza łączne miesięczne koszty magazynowania, sumując koszty magazynowania wszystkich maszyn wirtualnych w ocenie. Możesz obliczyć miesięczny koszt magazynu dla konkretnej maszyny, agregując miesięczny koszt wszystkich podłączonych do niej dysków.

    ![Azure Migrate](../../migrate/azure-best-practices/media/migrate-best-practices-costs/assess.png)
    _Ocena usługi Azure Migrate_

**Dowiedz się więcej:**

- Skorzystaj z [kalkulatora cen platformy Azure](https://azure.microsoft.com/pricing/calculator).
- Zapoznaj się [z omówieniem Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview).
- Przeczytaj informacje na temat [Azure Migrate ocen](https://docs.microsoft.com/azure/migrate/concepts-assessment-calculation).
- Dowiedz się więcej na temat [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).

## <a name="best-practice-right-size-vms"></a>Najlepsze rozwiązania: maszyny wirtualne o odpowiednim rozmiarze

Podczas wdrażania maszyn wirtualnych platformy Azure do obsługi obciążeń można wybrać różne opcje. Każdy typ maszyny wirtualnej ma określone funkcje i różne kombinacje procesora CPU, pamięci i dysków. Maszyny wirtualne zostały pogrupowane w sposób przedstawiony poniżej:

| **Typ** | **Szczegóły** | **Użycie** |
|---|---|---|
| **Ogólnego przeznaczenia** | Zrównoważona moc procesora CPU w stosunku do pamięci. | Jest to dobre dla testowania i opracowywania, małych i średnich baz danych, z niskim i średnim woluminem. | Serwery sieci Web ruchu. |
| **Optymalizacja pod kątem obliczeń** | Duża moc procesora CPU w stosunku do pamięci. | Dobra opcja w przypadku serwerów internetowych o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji. |
| **Optymalizacja pod kątem pamięci** | Duża ilość pamięci w stosunku do procesora CPU. | Dobra opcja w przypadku relacyjnych baz danych, średnich i dużych pamięci podręcznych oraz analizowania w pamięci. |
| **Optymalizacja pod kątem magazynu** | Wysoka przepływność dysku i we/wy. | Odpowiednie dla baz danych Big Data, SQL i NoSQL. |
| **Optymalizacja pod kątem procesora GPU** | Wyspecjalizowane maszyny wirtualne. Jeden lub wiele procesorów GPU. | Duże obciążenie grafiką i edytowaniem wideo. |
| **Wysoka wydajność** | Najszybszy i najbardziej wydajny procesor CPU. Maszyny wirtualne z opcjonalnymi interfejsami sieciowymi o wysokiej przepływności (RDMA). | Krytyczne aplikacje o wysokiej wydajności. |

- Ważne jest, aby zrozumieć różnice cenowe między tymi maszynami wirtualnymi i długoterminowe efekty budżetowe.
- Każdy typ obejmuje kilka serii maszyn wirtualnych.
- Ponadto w przypadku wybrania maszyny wirtualnej w ramach serii a można skalować maszynę wirtualną w górę i w dół w tej serii. Na przykład dsv2 \_ 2 można skalować w górę do dsv2 \_ 4, ale nie można go zmienić na inną serię, taką jak FSV2 \_ 2.

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

<!-- markdownlint-disable MD033 -->

| **Typ danych** | **Szczegóły** | **Użycie** |
| ---|---|---|
| **Obiekty blob** | Zoptymalizowany pod kątem przechowywania dużych ilości obiektów bez struktury, takich jak dane tekstowe lub binarne. | Uzyskiwanie dostępu do danych z dowolnego miejsca za pośrednictwem protokołu HTTP/HTTPS. | Używane na potrzeby scenariuszy przesyłania strumieniowego i dostępu losowego. Na przykład w celu udostępniania obrazów i dokumentów bezpośrednio w przeglądarce, strumieniowego przesyłania wideo i audio oraz przechowywania danych kopii zapasowych i odzyskiwania po awarii. |
| **Pliki** | Zarządzane udziały plików dostępne za pośrednictwem protokołu SMB 3,0. | Używane podczas migrowania lokalnych udziałów plików i zapewniania wielu dostępu i połączeń do danych plików. |
| **Dyski** | Oparte na stronicowych obiektach blob. <br><br> Typ dysku (szybkość): standardowy dysk twardy, standardowy dysk SSD, dysk SSD Premium lub Ultra Disks. <br><br> Zarządzanie dyskami: niezarządzane (Zarządzanie ustawieniami dysków i magazynem) lub zarządzanie (można wybrać typ dysku, a platforma Azure zarządza dyskiem). | Używaj dysków w warstwie Premium na potrzeby maszyn wirtualnych. Na potrzeby łatwego zarządzania i skalowania używaj dysków zarządzanych. |
| **Kolejki** | Przechowywanie i pobieranie dużej liczby komunikatów, do których można uzyskać dostęp za pośrednictwem uwierzytelnionych wywołań (HTTP lub HTTPS). | Łączenie składników aplikacji za pomocą asynchronicznego kolejkowania komunikatów. |
| **Tabele** | Przechowuje tabele. | Teraz jest to część interfejsu API tabeli usługi Azure Cosmos DB. |

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Poziomy dostępu

Usługa Azure Storage oferuje różne opcje uzyskiwania dostępu do danych blokowych obiektów BLOB. Wybranie odpowiedniej warstwy dostępu pozwala zapewnić, że dane blokowych obiektów blob są przechowywane w najbardziej opłacalny sposób.

<!-- markdownlint-disable MD033 -->

| **Warstwa dostępu** | **Szczegóły** | **Użycie** |
| --- | --- | --- |
| **Gorąca** | Wyższe koszty magazynowania, niższy dostęp i koszty transakcji <br><br> Jest to domyślna Warstwa dostępu. | Służy do przechowywania danych w przypadku aktywnego użycia, gdy dostęp do danych jest uzyskiwany często. |
| **Chłodna** | Niższe koszty magazynowania, wyższe koszty dostępu i transakcji. <br><br> Przechowywanie przez co najmniej 30 dni. | Przechowywanie krótkoterminowe, dane są dostępne, ale dostęp do nich jest uzyskiwany rzadko. |
| **Archiwum** | Używana na potrzeby pojedynczych blokowych obiektów blob. <br><br> Najbardziej ekonomiczna opcja magazynu. Najniższe koszty magazynowania, najwyższa cena dostępu i transakcji. | Użycie w przypadku danych, które mogą tolerować kilka godzin opóźnienia pobierania i będą przechowywane w warstwie archiwum przez co najmniej 180 dni. |

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Typy konta magazynu

Platforma Azure oferuje różne typy kont magazynu i warstw wydajności.

<!-- markdownlint-disable MD033 -->

| **Typ konta** | **Szczegóły** | **Użycie** |
| --- | --- | --- |
| **Warstwa standardowa w wersji 2 do osiągnięcia** | Obsługuje obiekty blob (blokowe, stronicowe, dołączania), pliki, dyski, kolejki i tabele. <br><br> Obsługuje warstwy dostępu gorąca, chłodna i archiwalna. Magazyn strefowo nadmiarowy (ZRS) jest obsługiwany. | Używane w przypadku większości scenariuszy i większości typów danych. Standardowe konta magazynu mogą być oparte na DYSKach twardych lub SSD. |
| **Warstwa Premium ogólnego przeznaczenia w wersji 2** | Obsługuje dane magazynu obiektów blob (stronicowe obiekty blob). Obsługuje warstwy dostępu gorąca, chłodna i archiwalna. Magazyn strefowo nadmiarowy jest obsługiwany. <br><br> Dane są przechowywane na dysku SSD. | Firma Microsoft zaleca używanie tego typu konta dla wszystkich maszyn wirtualnych. |
| **Ogólnego przeznaczenia, wersja 1** | Obsługa warstw dostępu nie jest obsługiwana. Nie obsługuje magazynu strefowo nadmiarowego | Używane, jeśli aplikacje potrzebują klasycznego modelu wdrażania platformy Azure. |
| **Tworzenia** | Specjalne konto magazynu do przechowywania obiektów bez struktury. Zapewnia blokowe obiekty blob i tylko dołączanie obiektów BLOB (bez plików, kolejek, tabel lub usług magazynu). Zapewnia taką samą trwałość, dostępność, skalowalność i wydajność jak ogólnego przeznaczenia w wersji 2. | Nie można przechowywać stronicowych obiektów BLOB na tych kontach, dlatego nie można przechowywać plików VHD. Warstwę dostępu można ustawić na gorącą lub chłodną. |

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Opcje nadmiarowości magazynu

Konta magazynu mogą wykorzystywać różne typy nadmiarowości na potrzeby zapewnienia odporności i wysokiej dostępności.

| **Typ** | **Szczegóły** | **Użycie** |
| --- | --- | --- |
| **Magazyn lokalnie nadmiarowy (LRS)** | Chroni przed awarią lokalną przez replikację w ramach pojedynczej jednostki magazynowej do oddzielnej domeny błędów i domeny aktualizacji. Przechowuje wiele kopii danych w jednym centrum danych. Zapewnia co najmniej 99,999999999% czasu trwałości obiektów w danym roku. | Warte rozważenia, jeśli aplikacja przechowuje dane, które można łatwo odtworzyć. |
| **Magazyn strefowo nadmiarowy (ZRS)** | Chroni przed awarią centrum danych przez replikowanie w trzech klastrach magazynu w jednym regionie. Każdy klaster magazynu jest fizycznie oddzielony i zlokalizowany we własnej strefie dostępności. Zapewnia co najmniej 99,9999999999 procentową trwałość obiektów w danym roku przez przechowywanie wielu kopii danych w wielu centrach lub regionach. | Warto rozważyć, jeśli potrzebujesz spójności, trwałości i wysokiej dostępności. Może nie chronić przed awarią regionalną, jeśli ma ona trwały wpływ na wiele stref. |
| **Magazyn Geograficznie nadmiarowy (GRS)** | Chroni przed awarią całego regionu przez replikowanie danych do regionu pomocniczego, który ma setki kilometrów od początku. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Dane repliki są niedostępne, dopóki firma Microsoft nie zainicjuje przejścia w tryb failover do regionu pomocniczego. Jeśli nastąpi przełączenie w tryb failover, możliwy jest dostęp do odczytu i zapisu. |
| **Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)** | Podobne do GRS. Zapewnia co najmniej 99.99999999999999% trwałości obiektów w danym roku. | Zapewnia dostępność i 99,99% odczytu, umożliwiając dostęp do odczytu z drugiego regionu używanego przez GRS. |

**Dowiedz się więcej:**

- [Przejrzyj](https://azure.microsoft.com/pricing/details/storage) cennik usługi Azure Storage.
- [Dowiedz się więcej o](https://docs.microsoft.com/azure/storage/common/storage-import-export-service) Usługa Azure Import/Export umożliwia wdrażanie dużych ilości danych w obiektach Blob i plikach platformy Azure.
- [Porównaj](https://docs.microsoft.com/azure/storage/common/storage-introduction) typy danych magazynu, takie jak obiekty blob, pliki i dyski.
- Dowiedz się więcej o [warstwach dostępu](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers).
- [Przejrzyj](https://docs.microsoft.com/azure/storage/common/storage-account-overview) różne typy kont magazynu.
- Dowiedz się więcej o [nadmiarowości usługi Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-redundancy), w tym LRS, ZRS, GRS i dostęp do odczytu.
- Dowiedz się więcej o [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="after-adoption"></a>Po przyjęciu

Przed przyjęciem prognozy kosztów są zależne od decyzji podejmowanych przez właścicieli obciążeń i zespół ds. wdrażania chmury. Chociaż zespół nadzoru może pomóc w wpływie tych decyzji, może być konieczne wykonanie niewielkiej akcji dla zespołu rządowego.

Gdy zasoby są w środowisku produkcyjnym, dane mogą być agregowane i trendy analizowane na poziomie środowiska. Te dane ułatwiają zespołowi nadzoru podejmowanie decyzji o wielkości i użyciu niezależnie od rzeczywistych wzorców użytkowania i bieżącej architektury stanu.

- Analizuj dane, aby wygenerować linię bazową budżetu dla grup zasobów i zasobów platformy Azure.
- Identyfikuj wzorce użycia, które umożliwiają zmniejszenie rozmiaru i zatrzymywanie lub wstrzymywanie zasobów w celu dodatkowego obniżenia kosztów.

Najlepsze rozwiązania w tej sekcji obejmują używanie Korzyść użycia hybrydowego platformy Azure i zarezerwowanych maszyn wirtualnych, zmniejszenie wydatków związanych z chmurą w ramach subskrypcji, używanie Azure Cost Management do budżetowania i analizy kosztów, monitorowania zasobów oraz implementowania budżetów grup zasobów oraz optymalizowania monitorowania, magazynu i maszyn wirtualnych.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefit"></a>Najlepsze rozwiązanie: korzystanie z Korzyść użycia hybrydowego platformy Azure

Dzięki wieloletnim inwestycjom w oprogramowanie systemów, takich jak Windows Server i SQL Server, firma Microsoft ma niepowtarzalną możliwość zaoferowania klientom wartości w chmurze ze znacznymi rabatami, na które inni dostawcy usług w chmurze niekoniecznie mogą sobie pozwolić.

Zintegrowane portfolio produktów firmy Microsoft, obejmujące środowisko lokalne i platformę Azure, stanowi przewagę konkurencyjną i ekonomiczną. Jeśli obecnie masz system operacyjny lub inne licencje na oprogramowanie w ramach programu Software Assurance (SA), możesz posłużyć się tymi licencjami w chmurze dla programu z usługą Korzyść użycia hybrydowego platformy Azure.

**Dowiedz się więcej:**

- [Zapoznaj](https://azure.microsoft.com/pricing/hybrid-benefit) się z kalkulatorem oszczędności korzyść użycia hybrydowego platformy Azure.
- Dowiedz się więcej [na temat korzyść użycia hybrydowego platformy Azure dla systemu Windows Server](https://azure.microsoft.com/pricing/hybrid-benefit).
- [Przejrzyj](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server.

## <a name="best-practice-use-reserved-vm-instances"></a>Najlepsze rozwiązanie: korzystanie z wystąpień zarezerwowanych maszyn wirtualnych

Większość platform w chmurze jest skonfigurowana pod kątem płatności zgodnie z rzeczywistym użyciem. Ten model zawiera wady, ponieważ nie zawsze wiadomo, jak dynamiczne będą obciążenia. Kiedy określasz jasne intencje dla obciążenia, bierzesz udział w planowaniu infrastruktury.

Za pomocą Azure Reserved VM Instances jest przedpłata za jeden rok lub trzy lata dla wystąpień maszyn wirtualnych.

- Przedpłata wiąże się z rabatem na używane zasoby.
- Możesz znacząco obniżyć koszty maszyn wirtualnych, SQL Database obliczeń, Azure Cosmos DB lub innych kosztów zasobów nawet o 72% w przypadku cen z opcją płatność zgodnie z rzeczywistym użyciem.
- Rezerwacje umożliwiają skorzystanie z rabatu na rozliczenia i nie mają wpływu na stan środowiska uruchomieniowego Twoich zasobów.
- Wystąpienia zarezerwowane można anulować.

![Wystąpienia zarezerwowane ](../../migrate/azure-best-practices/media/migrate-best-practices-costs/reserve.png)
 _— rysunek 1: zarezerwowane maszyny wirtualne platformy Azure._

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [Azure Reservations](https://docs.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations).
- Przeczytaj [często zadawane pytania dotyczące wystąpień zarezerwowanych](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq).
- Zapoznaj się ze [wskazówkami dotyczącymi cen dla SQL Server maszyn wirtualnych platformy Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Najlepsze rozwiązanie: agregowanie wydatków w chmurze w ramach subskrypcji

To nieuniknione, że w końcu będziesz mieć więcej niż jedną subskrypcję platformy Azure. Możesz na przykład potrzebować dodatkowej subskrypcji w celu rozdzielenia granic środowiska deweloperskiego i produkcyjnego lub możesz mieć platformę, która wymaga oddzielnej subskrypcji dla każdego klienta. Możliwość agregowania raportowania danych ze wszystkich subskrypcji na jednej platformie jest wartościową funkcją.

W tym celu można użyć interfejsów API usługi Azure Cost Management. Następnie, po zagregowaniu danych do jednego źródła, takiego jak baza danych SQL Azure, można użyć narzędzi, takich jak usługa Power BI, aby uwidocznić zagregowane dane. Można tworzyć zagregowane raporty subskrypcji i raporty szczegółowe. Na przykład w przypadku użytkowników, którzy potrzebują proaktywnie wglądu w koszty zarządzania, można utworzyć określone widoki kosztów na podstawie działów, grup zasobów lub innych informacji. Nie musisz zapewniać im pełnego dostępu do danych rozliczeniowych platformy Azure.

**Dowiedz się więcej:**

- Zapoznaj się z [omówieniem](https://docs.microsoft.com/azure/billing/billing-consumption-api-overview) interfejsów API użycia platformy Azure.
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
- Dowiedz się, jak [zoptymalizować koszty z zaleceń](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations)i [uniknąć nieoczekiwanych opłat](https://docs.microsoft.com/azure/billing/billing-getting-started).
- Dowiedz się więcej o zestawie [narzędzi optymalizacji zasobów platformy Azure (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-reduce-nonproduction-costs"></a>Najlepsze rozwiązanie: zmniejszanie kosztów nieprodukcyjnych

Środowiska programistyczne, testowe i gwarancja jakości są niezbędne podczas cyklu projektowania. Niestety, w przypadku tych środowisk często nie ma potrzeby obsługi administracyjnej, gdy przestaną być przydatne. Regularne przegląd nieużywanych środowisk nieprodukcyjnych może mieć natychmiastowe wpływ na koszty.

Dodatkowo należy wziąć pod uwagę ogólne obniżki kosztów dla środowisk nieprodukcyjnych:

- Zmniejsz ilość zasobów nieprodukcyjnych, aby korzystać z niższych maszyn wirtualnych serii B i magazynu w warstwie Standardowa.
- Zastosuj zasady platformy Azure, aby wymagać obniżenia kosztów zasobów dla wszystkich zasobów nieprodukcyjnych.

**Dowiedz się więcej:**

- [Użyj tagów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) , aby identyfikować cele deweloperskie, testowe lub pytania dotyczące zmiany rozmiarów lub zakończenia.
- [Maszyny wirtualne Autozamykania](https://docs.microsoft.com/azure/cost-management-billing/manage/getting-started#consider-cost-cutting-features-like-auto-shutdown-for-vms) ustawiają nocny czas zakończenia dla maszyn wirtualnych. Użycie tej funkcji spowoduje zatrzymanie maszyn wirtualnych nieprodukcyjnych w każdej porze nocnej, co wymaga od deweloperów ponownego uruchomienia tych maszyn wirtualnych, gdy są one gotowe do wznowienia rozwoju.
- Zachęcaj zespoły programistyczne do używania [Azure DevTest Labs](https://docs.microsoft.com/azure/lab-services/devtest-lab-overview) , aby określić własne podejścia do kontroli kosztów i uniknąć wpływu standardowego chronometrażu automatycznego zamykania w poprzednim kroku.

## <a name="best-practice-use-azure-cost-management"></a>Najlepsze rozwiązanie: Użyj Azure Cost Management

Firma Microsoft oferuje usługę Azure Cost Management, która ułatwia śledzenie wydatków:

- Ułatwia monitorowanie i kontrolowanie wydatków na platformę Azure oraz optymalizowanie użycia zasobów.
- Przegląda całą subskrypcję i wszystkie jej zasoby oraz wyświetla rekomendacje.
- Oferuje pełny interfejs API do integrowania zewnętrznych narzędzi i systemów finansowych na potrzeby raportowania.
- Śledzi użycie zasobów i zarządza kosztami chmury przy użyciu pojedynczego, ujednoliconego widoku.
- Dostarcza rozbudowane szczegółowe informacje operacyjne i finansowe, które ułatwiają podejmowanie świadomych decyzji.

W Azure Cost Management można:

- **Utwórz budżet:** Utwórz budżet dla odpowiedzialności finansowej.
  - Możesz uwzględnić usługi, których używasz, lub zasubskrybować określony okres (miesięcznie, kwartalnie, rocznie) i zakres (subskrypcje/grupy zasobów). Możesz na przykład utworzyć budżet subskrypcji platformy Azure dla okresu miesięcznego, kwartalnego lub rocznego.
    - Po utworzeniu budżetu będzie on widoczny w analizie kosztów. Przeglądanie budżetu względem bieżących wydatków jest jednym z pierwszych kroków potrzebnych podczas analizowania kosztów i wydatków.
  - W przypadku przekroczenia progów budżetu można wysyłać powiadomienia e-mail.
  - Dane zarządzania kosztów można eksportować do usługi Azure Storage w celu przeprowadzenia analizy.

    ![Wyświetlanie budżetów w Azure Cost Management ](../../migrate/azure-best-practices/media/migrate-best-practices-costs/budget.png)
     _Azure Cost Management budżet_

- **Wykonaj analizę kosztów:** Skorzystaj z analizy kosztów, aby eksplorować i analizować koszty organizacji, aby ułatwić zrozumienie sposobu naliczania kosztów i identyfikowania trendów wydatków.
  - Analiza kosztów jest dostępna dla użytkowników usługi EA.
  - Można wyświetlić dane analizy kosztów dla różnych zakresów, w tym według działu, konta, subskrypcji lub grupy zasobów.
  - Możesz uzyskać analizę kosztów pokazującą łączne koszty dla bieżącego miesiąca oraz skumulowane koszty dzienne.

    ![Rysunek analizy Azure Cost Management ](../../migrate/azure-best-practices/media/migrate-best-practices-costs/analysis.png)
     _: Azure Cost Management Analysis._

- **Pobierz zalecenia:** Zapoznaj się z zaleceniami klasyfikatora, które pokazują, jak można zoptymalizować i poprawić wydajność.

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/cost-management/overview) usługi Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices) zoptymalizować inwestycję w chmurę za pomocą usługi Azure Cost Management.
- [Dowiedz się, jak](https://docs.microsoft.com/azure/cost-management/use-reports) używać raportów usługi Azure Cost Management.
- [Zapoznaj się z samouczkiem](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations) dotyczącym optymalizowania kosztów za pomocą rekomendacji.
- [Przejrzyj](https://docs.microsoft.com/rest/api/consumption/budgets) interfejsy API użycia platformy Azure.

## <a name="best-practice-implement-resource-group-budgets"></a>Najlepsze rozwiązanie: implementowanie budżetów grup zasobów

Grupy zasobów są często używane w celu reprezentowania granic kosztów. Biorąc pod uwagę ten wzorzec użycia, zespół platformy Azure kontynuuje opracowywanie nowych i udoskonalonych sposobów śledzenia i analizowania wydatków na zasoby na różnych poziomach, z uwzględnieniem możliwości tworzenia budżetów na poziomie grupy zasobów i zasobów.

- Budżet grupy zasobów ułatwia śledzenie kosztów związanych z grupą zasobów.
- Gdy budżet zostanie wykorzystany lub przekroczony, możesz wyzwalać alerty lub uruchamiać wiele różnych podręczników.

**Dowiedz się więcej:**

- [Dowiedz się, jak](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario) zarządzać kosztami przy użyciu budżetów platformy Azure.
- [Postępuj zgodnie z samouczkiem](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets), aby utworzyć budżet platformy Azure i zarządzać nim.

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

W przypadku zastosowania najlepszych rozwiązań w zakresie wybierania magazynu przed wdrożeniem prawdopodobnie wykorzystaniu pewne korzyści. Prawdopodobnie możesz zoptymalizować dodatkowe koszty magazynowania. W miarę upływu czasu obiekty blob i pliki stają się nieaktualne. Dane mogą nie być już używane, ale ze względu na wymagania prawne trzeba je przechowywać przez określony okres. W związku z tym może nie być konieczne przechowywanie go w magazynie o wysokiej wydajności, który został użyty do oryginalnego wdrożenia.

Identyfikowanie i przenoszenie nieaktualnych danych do tańszych obszarów magazynowania może mieć ogromny wpływ na miesięczny budżet magazynu i oszczędność kosztów. Platforma Azure oferuje wiele sposobów, które ułatwiają identyfikację i przechowywanie tych nieaktualnych danych.

- Skorzystaj z zalet warstw dostępu dla magazynu ogólnego przeznaczenia w wersji 2, przenosząc mniej ważne dane z warstwy gorąca do chłodna i archiwalna.
- Użyj rozwiązania StorSimple, które pomoże Ci w przeniesieniu nieaktualnych danych na podstawie zasad niestandardowych.

**Dowiedz się więcej:**

- Dowiedz się więcej o [warstwach dostępu](https://docs.microsoft.com/azure/storage/blobs/storage-blob-storage-tiers).
- [Zapoznaj się z omówieniem](https://docs.microsoft.com/azure/azure-monitor/overview) rozwiązania StorSimple i z [cennikiem rozwiązania StorSimple](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Najlepsze rozwiązanie: Automatyzacja optymalizacji maszyn wirtualnych

Celem uruchamiania maszyny wirtualnej w chmurze jest zmaksymalizowanie używanego procesora, pamięci i dysku. Jeśli odkryjesz maszyny wirtualne, które nie są zoptymalizowane lub są nieużywane przez długie okresy czasu, warto je wyłączyć lub skalować je w dół przy użyciu zestawów skalowania maszyn wirtualnych.

Możesz zoptymalizować maszynę wirtualną za pomocą Azure Automation, zestawów skalowania maszyn wirtualnych, automatycznego zamykania oraz rozwiązań opartych na skrypcie lub innych firm.

**Dowiedz się więcej:**

- [Dowiedz się](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision), jak używać pionowego skalowania automatycznego.
- [Zaplanuj](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) automatyczne uruchamianie maszyny wirtualnej.
- [Dowiedz się](https://docs.microsoft.com/azure/automation/automation-solution-vm-management), jak uruchamiać maszyny wirtualne lub zatrzymywać je poza godzinami pracy w usłudze Azure Automation.
- Uzyskaj więcej informacji na temat [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview)i [zestawu narzędzi optymalizacji zasobów platformy Azure (ARO)](https://github.com/azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-use-logic-apps-and-runbooks-with-budgets-api"></a>Najlepsze rozwiązanie: używanie Logic Apps i elementów Runbook z interfejsem API budżetów

Platforma Azure udostępnia interfejs API REST, który może uzyskiwać dostęp do informacji rozliczeniowych dzierżawy.

- Korzystając z interfejsu API budżetów, można zintegrować systemy zewnętrzne i przepływy pracy wyzwalane przez metryki, które są tworzone na podstawie danych interfejsu API.
- Dane dotyczące użycia i zasobów można pobierać do preferowanych narzędzi do analizy danych.
- Interfejs API użycia zasobów platformy Azure i interfejs API usługi Azure Resource RateCard mogą ułatwić dokładne przewidywanie i zarządzanie kosztami.
- Interfejsy API są implementowane jako dostawca zasobów i są dołączone do interfejsów API udostępnianych przez Azure Resource Manager.
- Interfejs API budżetów można zintegrować z elementami Runbook Azure Logic Apps i Azure Automation.

**Dowiedz się więcej:**

- Dowiedz się więcej o [interfejsie API budżetów](https://docs.microsoft.com/rest/api/consumption/budgets).
- [Uzyskaj wgląd](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) w użycie platformy Azure przy użyciu interfejsy API rozliczeń platformy Azure.

## <a name="next-steps"></a>Następne kroki

Mając świadomość najlepszych rozwiązań, przejrzyj [Cost Management łańcucha narzędzi](./toolchain.md) , aby zidentyfikować narzędzia i funkcje platformy Azure, które ułatwiają wykonywanie tych najlepszych praktyk.

> [!div class="nextstepaction"]
> [Cost Management łańcucha narzędzi dla platformy Azure](./toolchain.md)
