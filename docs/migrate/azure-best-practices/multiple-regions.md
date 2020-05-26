---
title: Przewodnik po decyzjach związanych z regionami
description: Dowiedz się więcej na temat regionów platformy w chmurze oraz czynników i cech, które mogą wpływać na wybór regionów platformy Azure.
author: doodlemania2
ms.author: dermar
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 0445ba3048a7b16b792cd144c29d1643aefe0d09
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83815314"
---
# <a name="azure-regions"></a>Regiony świadczenia usługi Azure

Platforma Azure składa się z wielu regionów na całym świecie. Każdy [region świadczenia usługi Azure](https://azure.microsoft.com/global-infrastructure/regions) ma specyficzne cechy, dlatego wybór regionu do użycia jest niezwykle ważny.

1. **Dostępne usługi:** Usługi, które są wdrażane w poszczególnych regionach, różnią się w zależności od różnych czynników. Dla swojego obciążenia wybierz region, który zawiera żądaną usługę. Aby uzyskać więcej informacji o dostępnych usługach w poszczególnych regionach, zobacz [Dostępność produktów według regionów](https://azure.microsoft.com/global-infrastructure/services).
1. **Pojemność:** Każdy region ma maksymalną pojemność. Chociaż jest to zwykle abstrakcyjne od użytkownika końcowego, może to mieć wpływ na typy subskrypcji, które mogą wdrażać typy usług i w jakich okolicznościach. Różni się to od limitów przydziału subskrypcji. Jeśli planujesz migrację z dużą ilością danych na platformę Azure, możesz zapoznać się z lokalnym zespołem ds. pól platformy Azure lub menedżerem kont, aby upewnić się, że można go wdrożyć w odpowiedniej skali.
1. **Ograniczenia:** Niektóre ograniczenia są wprowadzane do wdrożenia usług w określonych regionach. Na przykład niektóre regiony są dostępne tylko jako miejsce docelowe kopii zapasowej lub pracy w trybie failover. Inne istotne ograniczenia to [wymagania dotyczące niezależności danych](https://azure.microsoft.com/global-infrastructure/geographies).
1. **Suwerenność:** Niektóre regiony są przeznaczone dla konkretnych suwerennych jednostek. Wszystkie regiony są regionami platformy Azure, ale te niezależne regiony są całkowicie odizolowane od reszty platformy Azure, nie muszą być zarządzane przez firmę Microsoft i mogą być ograniczone do określonych typów klientów. Te niezależne regiony są następujące:
    1. [Chiny platformy Azure](https://azure.microsoft.com/global-infrastructure/china)
    1. [Azure (Niemcy](https://azure.microsoft.com/global-infrastructure/germany)): przestarzałe na rzecz standardowych regionów świadczenia usługi Azure w Niemczech
    1. [Wersja platformy Azure dla administracji USA](https://azure.microsoft.com/global-infrastructure/government)
    1. Uwaga: w [Australii](https://azure.microsoft.com/global-infrastructure/australia) firma Microsoft zarządza dwoma regionami, ale są one udostępniane dla instytucji rządowych Australii oraz jej klientów i wykonawców, w związku z czym obowiązują w nich podobne ograniczenia klienta co w przypadku innych chmur suwerennych.

## <a name="operate-in-multiple-geographic-regions"></a>Działanie w wielu regionach geograficznych

Gdy firmy działają w wielu regionach geograficznych w celu zapewnienia odporności, może to spowodować dodatkową złożoność. Złożoność ta przejawia się w czterech głównych obszarach:

- Dystrybucja zasobów
- Profile dostępu użytkowników
- Wymagania dotyczące zgodności
- Odporność regionalna

Wraz z uzyskiwaniem informacji dotyczących złożonych kwestii, zaczniesz rozumieć, jak ważny jest wybór regionu w kontekście ogólnej strategii wdrażania chmury. Zacznijmy od zagadnień związanych z siecią.

## <a name="networking-considerations"></a>Zagadnienia dotyczące pracy w sieci

Każde niezawodne wdrożenie w chmurze wymaga dobrze przemyślanej sieci, która uwzględnia regiony platformy Azure. Po uwzględnieniu powyższych cech względem regionów, w których ma zostać przeprowadzone wdrożenie, należy wdrożyć sieć. Wyczerpujące omówienie sieci wykracza poza zakres tego artykułu, jednak należy uwzględnić pewne kwestie:

- Regiony platformy Azure są wdrażane w parach. W przypadku awarii regionu, inny region w ramach tej samej granicy geopolitycznej jest wyznaczony jako jego sparowany region. Rozważ wdrożenie w regionach sparowanych jako podstawowa i pomocnicza strategia odporności. Brazylia Południowa to istotny wyjątek, którego sparowany region jest Południowo-środkowe stany USA. Aby uzyskać więcej informacji, zobacz [regiony sparowane na platformie Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

  - Usługa Azure Storage obsługuje [Magazyn Geograficznie nadmiarowy (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs) , co oznacza, że trzy kopie danych są przechowywane w regionie podstawowym, a trzy dodatkowe kopie są przechowywane w sparowanym regionie. Nie można zmienić parowania w przypadku magazynu geograficznie nadmiarowego.
  - Usługi oparte na magazynie geograficznie nadmiarowym usługi Azure Storage mogą korzystać z tej możliwości sparowanego regionu. W tym celu aplikacje i sieci muszą być ukierunkowane na obsługę tej możliwości.
  - Jeśli nie planujesz używać GRS do obsługi regionalnej potrzeby odporności, nie należy używać sparowanego regionu jako pomocniczego. W przypadku awarii regionalnej nastąpi intensywne wykorzystanie zasobów w sparowanym regionie w miarę migrowania zasobów. Uniknięcie takiego obciążenia może przyspieszyć proces odzyskiwania przez odzyskiwanie do lokacji alternatywnej.
  > [!WARNING]
  > Nie należy próbować używać magazynu geograficznie nadmiarowego platformy Azure do tworzenia kopii zapasowych maszyn wirtualnych ani ich odzyskiwania. Zamiast tego można zastosować usługi [Azure Backup](https://azure.microsoft.com/services/backup) i [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery) wraz z [dyskami zarządzanymi platformy Azure](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) do obsługi odporności obciążeń IaaS.

- Usługi Azure Backup i Azure Site Recovery współpracują ze sobą w ramach zaprojektowanej sieci, aby ułatwić zapewnienie odporności regionalnej na potrzeby usług IaaS i kopii zapasowych danych. Upewnij się, że sieć jest zoptymalizowana, dzięki czemu transfery danych pozostaną w sieci szkieletowej firmy Microsoft i będą korzystać z [wirtualnych sieci równorzędnych](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview), jeśli będzie to możliwe. Niektóre większe organizacje z wdrożeniami globalnymi mogą zamiast tego używać [ExpressRoute Premium](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) do kierowania ruchu między regionami, które mogą zaoszczędzić regionalne opłaty za ruch wychodzący.

- Grupy zasobów platformy Azure są konstrukcjami specyficznymi dla regionu. Jest to jednak normalne, że zasoby należące do grupy zasobów istnieją w wielu regionach. W tej sytuacji należy koniecznie pamiętać, że w przypadku awarii regionalnej operacje płaszczyzny sterowania względem grupy zasobów zakończą się niepowodzeniem w regionie, w którym miała miejsce awaria, nawet jeśli zasoby w innych regionach (w ramach tej grupy zasobów) będą nadal działać. Może to mieć wpływ zarówno na projekt sieci, jak i projekt grupy zasobów.

- Wiele usług PaaS na platformie Azure obsługuje [punkty końcowe usługi](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) lub usługę [Private Link](https://docs.microsoft.com/azure/private-link/private-link-overview). Oba te rozwiązania w istotny sposób wpływają na kwestie dotyczące sieci w kontekście odporności regionalnej, migracji i zarządzania.

- Wiele usług PaaS korzysta z własnych rozwiązań zapewniających odporność. Na przykład zarówno Azure SQL Database, jak i Azure Cosmos DB umożliwiają łatwą replikację do dodatkowych regionów _x_ . W przypadku niektórych usług, np. Azure DNS, nie obowiązują zależności regionalne. Podejmując decyzję o usługach używanych w procesie wdrażania, pamiętaj, aby w pełni zrozumieć możliwości przełączania w tryb failover i kroki odzyskiwania, które mogą być wymagane dla każdej usługi platformy Azure.

- Oprócz wdrażania w wielu regionach w celu zapewnienia obsługi odzyskiwania po awarii, wiele organizacji wybiera wdrożenie zgodnie ze wzorcem aktywne/aktywne, dzięki czemu nie jest wymagane przełączenie w tryb failover. Ma to dodatkową zaletę w postaci zapewniania globalnego równoważenia obciążenia oraz dodatkowego zwiększenia odporności na uszkodzenia i wydajności sieci. Aby skorzystać z tego wzorca, aplikacje muszą obsługiwać działanie w trybie aktywne/aktywne w wielu regionach.

> [!WARNING]
> Regiony platformy Azure to konstrukcje o wysokiej dostępności, a dla usług uruchomionych w ramach tych regionów zastosowanie mają umowy dotyczące poziomu usług. Nigdy jednak nie należy stosować zależności w pojedynczym regionie w przypadku aplikacji o strategicznym znaczeniu. Należy zawsze brać pod uwagę awarię regionalną i ćwiczyć wykonywanie kroków dotyczących odzyskiwania i ograniczania ryzyka.

Po uwzględnieniu topologii sieci, która będzie wymagana do zapewnienia odpowiedniego działania, konieczne będzie utworzenie dodatkowej dokumentacji i dostosowanie procesu. Poniższe podejście może pomóc ocenić potencjalne wyzwania i ustanowić ogólny sposób działania:

- Rozważ bardziej niezawodną implementację gotowości i ładu.
- Sporządź spis uwzględnionych obszarów geograficznych. Skompiluj listę regionów i krajów, których dotyczy problem.
- Udokumentuj wymagania dotyczące niezależności danych. czy zidentyfikowane kraje mają wymagania dotyczące zgodności, które regulują niezależność danych?
- Udokumentuj bazę użytkowników. czy migracja w chmurze wpłynie na pracowników, partnerów lub klientów w zidentyfikowanym kraju?
- Udokumentuj centra danych i zasoby. czy w zidentyfikowanym kraju istnieją zasoby, które mogą zostać uwzględnione podczas pracy związanej z migracją?
- Udokumentuj wymagania dotyczące regionalnej dostępności jednostek SKU i przechodzenia w tryb failover.

Dopasuj zmiany w procesie migracji, aby obsługiwać początkowy spis.

## <a name="document-complexity"></a>Złożoność dokumentu

Poniższa tabela może pomóc w dokumentowaniu wyników opisanych powyżej czynności:

| Region        | Kraj     | Pracownicy lokalni | Lokalni użytkownicy zewnętrzni   | Centra danych lub zasoby lokalne | Wymagania dotyczące niezależności danych |
|---------------|-------------|-----------------|------------------------|-----------------------------|-------------------------------|
| Ameryka Północna | Stany Zjednoczone         | Tak             | Partnerzy i klienci | Yes                         | Nie                            |
| Ameryka Północna | Kanada      | Nie              | Klienci              | Tak                         | Tak                           |
| Europa        | Niemcy     | Tak             | Partnerzy i klienci | Nie — tylko sieć           | Tak                           |
| Azja i Pacyfik  | Korea Południowa | Tak             | Partnerzy               | Tak                         | Nie                            |

<!-- markdownlint-disable MD026 -->

## <a name="relevance-of-data-sovereignty"></a>Znaczenie dla suwerenności danych

Na całym świecie organizacje rządowe rozpoczęły ustanawianie wymagań dotyczących niezależności danych, takich jak Ogólne rozporządzenie o ochronie danych (RODO). Wymagania dotyczące zgodności tego rodzaju często wymagają lokalizacji w określonym regionie, a nawet w określonym kraju, aby chronić swoich obywateli. W niektórych przypadkach dane dotyczące klientów, pracowników lub partnerów muszą być przechowywane na platformie chmury w tym samym regionie, w którym znajduje się użytkownik końcowy.

Sprostanie temu wyzwaniu to duża motywacja do przeprowadzenia migracji w chmurze dla firm działających w skali globalnej. Aby spełnić wymagania dotyczące zgodności, niektóre firmy zdecydowały się wdrożyć duplikaty zasobów IT dla dostawców chmury w regionie. W powyższej tabeli Niemcy są dobrym przykładem tego scenariusza. W tym przykładzie w Niemczech znajdują się klienci, partnerzy i pracownicy, ale nie ma żadnych istniejących zasobów IT. Firma może zdecydować się na wdrożenie niektórych zasobów do centrum danych w obszarze RODO, potencjalnie nawet przy użyciu niemieckich centrów danych platformy Azure. Zrozumienie danych, których dotyczy RODO, może pomóc zespołowi wdrożeniowemu ds. chmury zrozumieć najlepsze podejście do migracji w tym przypadku.

### <a name="why-is-the-location-of-end-users-relevant"></a>Dlaczego lokalizacja użytkowników końcowych jest ważna?

Firmy obsługujące użytkowników końcowych w wielu krajach opracowały rozwiązania techniczne dotyczące obsługi ruchu użytkowników końcowych. W niektórych przypadkach obejmuje to lokalizację zasobów. W innych scenariuszach firma może zdecydować się na wdrożenie globalnych rozwiązań sieci WAN w celu rozwiązania problemów z różnymi bazami użytkowników za pośrednictwem rozwiązań ukierunkowanych na sieć. We wszystkich przypadkach na strategię migracji mogą mieć wpływ profile użycia osobnych użytkowników końcowych.

Ze względu na to, że firma obsługuje pracowników, partnerów i klientów w Niemczech, ale w tym kraju nie ma obecnie centrów danych, najprawdopodobniej firma wdrożyła pewną formę rozwiązania dzierżawionego w celu skierowania tego ruchu do centrów danych w innych krajach. Ten istniejący routing stanowi znaczne ryzyko dla postrzeganej wydajności migrowanych aplikacji. Wprowadzanie dodatkowych przeskoków w ustalonej i dostrojonej globalnej sieci WAN może stworzyć wrażenie, że po migracji aplikacje działają z niedostateczną wydajnością. Znajdowanie i rozwiązywanie tych problemów może dodać do projektu znaczne opóźnienia. W każdym z poniższych procesów wskazówki dotyczące rozwiązywania problemów ze złożoności są przedstawione w ramach procesów dotyczących wymagań wstępnych, oceniania, migrowania i optymalizowania. Zrozumienie profilów użytkowników w poszczególnych krajach ma kluczowe znaczenie dla prawidłowego zarządzania tą złożonością.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Dlaczego lokalizacja centrów danych jest ważna?

Lokalizacja istniejących centrów danych może mieć wpływ na strategię migracji. Poniżej przedstawiono kilka najczęstszych typów wpływu:

**Decyzje dotyczące architektury:** Region docelowy jest jednym z pierwszych kroków projektowania strategii migracji. Na ten element często wpływa lokalizacja istniejących zasobów. Ponadto dostępność usług w chmurze i koszt jednostkowy tych usług mogą różnić się w zależności od regionu. W związku z tym zrozumienie bieżącej i przyszłej lokalizacji zasobów wpływa na decyzje dotyczące architektury, a także może mieć wpływ na oszacowania budżetu.

**Zależności centrum danych:** Na podstawie danych w powyższej tabeli prawdopodobnie istnieją zależności między różnymi centrami danych na całym świecie. W wielu organizacjach, które działają na taką skalę, te zależności mogą nie być udokumentowane ani zrozumiałe. Metody służące do szacowania profilów użytkowników ułatwią zidentyfikowanie niektórych z tych zależności. Zalecamy jednak, aby w trakcie procesu oceny wykonać dodatkowe czynności w celu ograniczenia ryzyka związanego z tą złożonością.

## <a name="implementing-the-general-approach"></a>Implementowanie podejścia ogólnego

Takie podejście jest oparte na informacjach wymiernych. W związku z tym podejście to będzie zgodne z modelem opartym na danych w procesie rozwiązywania problemów z złożonością migracji globalnej.

Gdy zakres migracji obejmuje wiele regionów, zespół wdrożeniowy ds. chmury powinien ocenić następujące zagadnienia dotyczące gotowości:

- Niezależność danych może wymagać lokalizacji niektórych zasobów, ale istnieje wiele zasobów, które mogą nie podlegać tym ograniczeniom zgodności. Elementy, takie jak rejestrowanie, raportowanie, routing sieciowy, tożsamość i inne centralne usługi IT, mogą być hostowane jako usługi udostępnione w wielu subskrypcjach, a nawet w wielu regionach. Zespół ds. wdrażania chmury powinien oszacować użycie modelu usługi udostępniania usług, jak opisano w temacie dotyczącym [architektury referencyjnej topologii gwiazdy z usługami udostępnionymi](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
- W przypadku wdrażania wielu wystąpień podobnych środowisk fabryka środowisk może stworzyć spójność, poprawić zarządzanie i przyspieszyć wdrażanie. W przypadku [przewodnika dotyczącego ładu dla przedsiębiorstw złożonych](../../govern/guides/complex/index.md) jest ustanawiane podejście, które tworzy środowisko skalujące się w wielu regionach.

Gdy zespół zdobędzie doświadczenie dotyczące podejścia obejmującego punkty odniesienia, a elementy gotowości zostaną dopasowane, należy wziąć pod uwagę kilka wymagań wstępnych opartych na danych:

- **Ogólne odnajdywanie:** Wypełnij powyższą tabelę [złożoności dokumentu](#document-complexity) .
- **Przeprowadź analizę profilu użytkownika w każdym kraju, którego to dotyczy:** Ważne jest, aby zrozumieć ogólne informacje o routingu użytkowników końcowych na wczesnym etapie procesu migracji. Zmiana globalnych linii dzierżawy i dodanie połączeń, takich jak usługa ExpressRoute, do centrum danych w chmurze może wymagać miesięcy opóźnienia pracy w sieci. Ten problem należy rozwiązać na jak najwcześniejszym etapie procesu.
- **Wstępna racjonalizacja cyfrowej:** Za każdym razem, gdy złożoność jest wprowadzana do strategii migracji, należy przeprowadzić wstępną racjonalizację w zakresie cyfr. Aby uzyskać pomoc, zapoznaj się ze wskazówkami dotyczącymi [racjonalizacji majątku cyfrowego](../../digital-estate/index.md).
  - **Dodatkowe wymagania dotyczące podpisywania cyfrowego:** Ustanów zasady tagowania, aby identyfikować wszelkie obciążenia, których dotyczą wymagania dotyczące suwerenności danych. Wymagane tagi powinny rozpoczynać się na etapie racjonalizacji majątku cyfrowego i przechodzić do migrowanych zasobów.
- **Oceń model gwiazdy:** Systemy rozproszone często używają wspólnych zależności. Zależności te mogą być często obsługiwane za pośrednictwem implementacji modelu gwiazdy. Chociaż taki model jest poza zakresem dla procesu migracji, należy oznaczyć go do uwzględnienia podczas przyszłych iteracji [gotowych procesów](../../ready/index.md).
- **Priorytetyzacja zaległości migracji:** Gdy zmiany w sieci są wymagane do obsługi wdrożenia produkcyjnego obciążenia, które obsługuje wiele regionów, ważne jest, aby zespół strategii chmury śledził eskalacji dotyczące tych zmian w sieci i zarządzać nimi. Wyższy poziom wsparcia kadry kierowniczej pomoże w przyspieszaniu zmiany. Jednak bardziej istotny wpływ polega na tym, że zespół ds. strategii może zmienić priorytet listy prac, aby zapewnić, że globalne obciążenia nie będą blokowane przez zmiany sieci. W przypadku takich obciążeń należy określać priorytety tylko po zakończeniu wprowadzania zmian sieci.

Te wymagania wstępne pomogą w ustanowieniu procesów, które mogą rozwiązać problemy z tym stopniem złożoności podczas wykonywania strategii migracji.

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

W przypadku złożoności globalnej bazy zasobów użytkowników istnieje kilka kluczowych działań, które należy dodać do oceny kandydatów do migracji. Każda z tych zmian zwiększy czytelność wpływu na użytkowników i zasoby globalne dzięki podejściu opartemu na danych.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

**Oceń zależności między centrami danych:** [Narzędzia wizualizacji zależności w Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) mogą pomóc w wykrywaniu zależności. Najlepszym rozwiązaniem jest użycie tych narzędzi przed migracją. W przypadku obsługi złożoności na poziomie globalnym jest to niezbędny krok do procesu oceny. Za pośrednictwem [grupowania zależności](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) wizualizacja może ułatwić identyfikację adresów IP i portów zasobów wymaganych do obsługi obciążenia.

> [!IMPORTANT]
> Dwie ważne uwagi: pierwszy ekspert, który ma świadomość rozmieszczenia zasobów i schematy adresów IP, jest wymagany do identyfikowania zasobów, które znajdują się w dodatkowym centrum danych. Po drugie ważne jest, aby oszacować zależności podrzędne i klientów w wizualizacji w celu zrozumienia zależności dwukierunkowych.

**Identyfikuj wpływ na użytkowników globalnych:** Dane wyjściowe analizy profilu użytkownika wymaganego wstępnie powinny identyfikować wszelkie obciążenia, których dotyczą globalne profile użytkowników. Gdy kandydat do migracji znajduje się na liście uwzględnionych obciążeń, architekt przygotowujący migrację powinien skonsultować się z ekspertami w dziedzinie sieci i operacji, aby zweryfikować oczekiwania dotyczące wydajności i routingu sieci. Architektura powinna obejmować przynajmniej połączenie usługi ExpressRoute między najbliższym centrum operacji sieciowych i platformą Azure. [Architektura referencyjna dla połączeń usługi ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute) może pomóc w konfiguracji niezbędnego połączenia.

**Projektowanie pod kątem zgodności:** Dane wyjściowe analizy profilu użytkownika wymaganego wstępnie powinny identyfikować wszelkie obciążenia, na które mają wpływ wymagania dotyczące niezależności danych. W trakcie wykonywania działań architektury w procesie oceny przypisany architekt powinien skonsultować się z ekspertami z dziedziny zgodności, aby poznać wymagania dotyczące migracji/wdrożenia w wielu regionach. Te wymagania znacząco wpłyną na strategie projektowania. Architektury referencyjne dla [wieloregionowych aplikacji internetowych](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) mogą pomóc w projektowaniu.

> [!WARNING]
> W przypadku korzystania z dowolnej spośród powyższych architektur referencyjnych może być konieczne wykluczenie określonych elementów danych z procesów replikacji, aby spełniać wymagania dotyczące niezależności danych. Spowoduje to dodanie dodatkowego kroku do procesu podwyższania poziomu.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas migrowania aplikacji, którą należy wdrożyć w wielu regionach, zespół ds. wdrażania chmury musi wziąć pod uwagę kilka kwestii. Dotyczą one projektu magazynu usługi Azure Site Recovery, projektu serwera konfiguracji/przetwarzania, projektów przepustowości sieci i synchronizacji danych.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

**Projekt magazynu Azure Site Recovery:** Azure Site Recovery to sugerowane narzędzie do replikacji w chmurze i synchronizowania zasobów cyfrowych z platformą Azure. Usługa Site Recovery replikuje dane dotyczące zasobów do magazynu usługi Site Recovery, który jest powiązany z określoną subskrypcją w określonym regionie i centrum danych platformy Azure. W przypadku replikowania zasobów do drugiego regionu może być wymagany drugi magazyn usługi Site Recovery.

**Projekt konfiguracji/serwera przetwarzania:** Site Recovery współpracuje z lokalnym wystąpieniem konfiguracji i serwera przetwarzania, który jest powiązany z pojedynczym magazynem Site Recovery. Oznacza to, że może być konieczne zainstalowanie drugiego wystąpienia tych serwerów w źródłowym centrum danych w celu ułatwienia replikacji.

**Projektowanie przepustowości sieci:** Podczas replikacji i trwającej synchronizacji dane binarne są przenoszone przez sieć ze źródłowego centrum danych do magazynu Site Recovery w docelowym centrum danych platformy Azure. Ten proces zużywa przepustowość. W przypadku duplikowania obciążenia do drugiego regionu ilość zużytej przepustowości zostanie podwojona. Gdy przepustowość jest ograniczona lub obciążenie wiąże się z dużą ilością konfiguracji lub dryfem danych, może to zakłócać czas wymagany do przeprowadzenia migracji. Co ważniejsze, może mieć to wpływ na środowisko użytkowników lub aplikacji, które nadal zależą od przepustowości centrum danych.

**Synchronizacja danych:** Często największy odpływ przepustowości pochodzi z synchronizacji platformy danych. Zgodnie z definicją w architekturach referencyjnych dla [wieloregionowych aplikacji internetowych](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) synchronizacja danych jest często wymagana w celu dopasowania aplikacji. Jeśli jest to żądany stan operacyjny aplikacji, może być konieczne przeprowadzenie synchronizacji między źródłową platformą danych i wszystkimi platformami w chmurze przed migracją zasobów aplikacji i warstwy środkowej.
**Synchronizacja danych:** Często największy odpływ przepustowości pochodzi z synchronizacji platformy danych. Zgodnie z definicją w architekturach referencyjnych dla [wieloregionowych aplikacji internetowych](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) synchronizacja danych jest często wymagana w celu dopasowania aplikacji. Jeśli jest to żądany stan operacyjny aplikacji, może być konieczne przeprowadzenie synchronizacji między źródłową platformą danych i wszystkimi platformami w chmurze przed migracją zasobów aplikacji i warstwy środkowej.

**Odzyskiwanie po awarii z platformy Azure do platformy Azure:** Alternatywna opcja może zwiększyć złożoność. Jeśli osie czasu i synchronizacja danych zbliżają się do wdrożenia dwuetapowego, usługa [Odzyskiwanie po awarii Azure–Azure](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture) może być akceptowalnym rozwiązaniem. W tym scenariuszu obciążenie jest migrowane do pierwszego centrum danych platformy Azure przy użyciu jednego magazynu usługi Site Recovery oraz projektu serwera konfiguracji lub przetwarzania. Po przetestowaniu obciążenia można je odzyskać do drugiego centrum danych platformy Azure z migrowanych zasobów. Takie podejście zmniejsza wpływ na zasoby w źródłowym centrum danych i korzysta z większych szybkości transferu oraz ograniczeń przepustowości dostępnych między centrami danych platformy Azure.

> [!NOTE]
> Takie podejście może zwiększyć krótkoterminowy koszt migracji, ponieważ może spowodować naliczenie dodatkowych opłat za przepustowość ruchu wychodzącego.

## <a name="optimize-and-promote-process-changes"></a>Optymalizacja i podwyższenie poziomu zmian procesu

Rozwiązywanie problemów z globalną złożonością podczas optymalizacji i podwyższania poziomu może wymagać zduplikowanej pracy w każdym z dodatkowych regionów. W przypadku przyjęcia jednego wdrożenia można nadal wymagać duplikowania testowania biznesowego i planów zmian biznesowych.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Sugerowana akcja w trakcie procesu optymalizacji i podwyższania poziomu

**Optymalizacja pretestowa:** Testy początkowej automatyzacji mogą identyfikować potencjalne możliwości optymalizacji, podobnie jak w przypadku dowolnego wysiłku migracji. W przypadku obciążeń globalnych ważne jest, aby testować obciążenie w poszczególnych regionach niezależnie, ponieważ drobne zmiany konfiguracji w sieci lub docelowym centrum danych platformy Azure mogą mieć wpływ na wydajność.

**Plany zmian firmy:** W przypadku każdego złożonego scenariusza migracji należy utworzyć plan zmiany biznesowej w celu zapewnienia jasnej komunikacji dotyczącej wszelkich zmian w procesach biznesowych, środowiska użytkownika i chronometrażu działań koniecznych do integracji zmian. W przypadku globalnych działań związanych z migracją plan powinien obejmować zagadnienia dotyczące użytkowników końcowych w poszczególnych lokalizacjach geograficznych.

**Testowanie biznesowe:** W połączeniu z planem zmian w firmie testy biznesowe mogą być wymagane w każdym regionie w celu zapewnienia odpowiedniej wydajności i przestrzegania zmodyfikowanych wzorców routingu sieciowego.

**Loty podwyższania poziomu:** Często promocja odbywa się jako pojedyncze działanie, przekierowywanie ruchu produkcyjnego do zmigrowanych obciążeń. W przypadku globalnych działań dotyczących wydań podwyższenie poziomu powinno być przeprowadzane w ramach pakietów testowych (lub wstępnie zdefiniowanych kolekcji użytkowników). Dzięki temu zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury będą mogły skuteczniej obserwować wydajność i ulepszać obsługę użytkowników w poszczególnych regionach. Pakiety testowe podwyższania poziomu są często kontrolowane na poziomie sieci przez zmianę routingu konkretnych zakresów adresów IP z zasobów obciążeń źródłowych do nowo migrowanych zasobów. Po przeprowadzeniu migracji określonej kolekcji użytkowników końcowych można przekierować następną grupę.

**Optymalizacja lotu:** Jedną z zalet lotów promocji jest umożliwienie dokładniejszych obserwacji i dodatkowej optymalizacji wdrożonych zasobów. Po krótkim okresie użycia w produkcji przez pierwszy pakiet testowy zaleca się uściślenie migrowanych zasobów, jeśli jest dozwolone przez procedury operacyjne działu IT.
