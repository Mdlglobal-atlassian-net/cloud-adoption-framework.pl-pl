---
title: Rozwiązywanie problemów dotyczących złożoności migrowania wielu regionów geograficznych
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Rozwiązywanie problemów dotyczących złożoności migrowania wielu regionów geograficznych.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3977618981212e2c0dc4dcd95ae14bf4dc773499
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905588"
---
# <a name="multiple-geographic-regions"></a>Wiele regionów geograficznych

Gdy firmy działają w wielu regionach geograficznych, można to spowodować wprowadzenie dodatkowej złożoności pracy związanej z migracją w chmurze. Złożoność ta przejawia się w trzech głównych obszarach: dystrybucja zasobów, profile dostępu użytkowników i wymagania dotyczące zgodności. Ważne jest, aby przed rozwiązaniem problemów związanych z wieloma regionami, zrozumieć zasięg potencjalnej złożoności.

## <a name="general-scope-expansion"></a>Rozszerzenie zakresu ogólnego

Poniższe podejście może pomóc ocenić potencjalne wyzwania i ustanowić ogólny sposób działania:

- Rozważ bardziej niezawodną implementację gotowości i ładu.
- Sporządź spis uwzględnionych obszarów geograficznych. Skompiluj listę regionów i krajów, których dotyczy migracja w chmurze.
- Udokumentuj wymagania dotyczące niezależności danych: czy zidentyfikowane kraje mają wymagania dotyczące zgodności, które regulują niezależność danych?
- Udokumentuj bazę użytkowników: czy migracja w chmurze wpłynie na pracowników, partnerów lub klientów w zidentyfikowanym kraju?
- Udokumentuj centra danych i zasoby: czy w zidentyfikowanym kraju istnieją zasoby, które mogą zostać uwzględnione podczas pracy związanej z migracją?

Dopasuj zmiany w procesie migracji, aby obsługiwać początkowy spis.

### <a name="documenting-complexity"></a>Dokumentowanie złożoności

Poniższa tabela może pomóc w dokumentowaniu wyników opisanych powyżej czynności:

|Region  |Country  |Pracownicy lokalni  |Lokalni użytkownicy zewnętrzni  |Centra danych lub zasoby lokalne |Wymagania dotyczące niezależności danych  |
|---------|---------|---------|---------|---------|---------|
|Ameryka Północna     |Stany Zjednoczone         |Tak         |Partnerzy i klienci         |Tak         |Nie         |
|Ameryka Północna     |Kanada         |Nie         |Klienci         |Tak         |Tak         |
|Europa     |Niemcy         |Tak         |Partnerzy i klienci         |Nie — tylko sieć         |Tak         |
|Azja i Pacyfik     |Korea Południowa         |Tak         |Partnerzy         |Tak         |Nie         |

<!-- markdownlint-disable MD026 -->

### <a name="why-is-data-sovereignty-relevant"></a>Dlaczego niezależność danych ma znaczenie?

Na całym świecie organizacje rządowe rozpoczęły ustanawianie wymagań dotyczących niezależności danych, takich jak Ogólne rozporządzenie o ochronie danych (RODO). Wymagania dotyczące zgodności tego rodzaju często wymagają lokalizacji w określonym regionie, a nawet w określonym kraju, aby chronić swoich obywateli. W niektórych przypadkach dane dotyczące klientów, pracowników lub partnerów muszą być przechowywane na platformie chmury w tym samym regionie, w którym znajduje się użytkownik końcowy.

Sprostanie temu wyzwaniu to duża motywacja do przeprowadzenia migracji w chmurze dla firm działających w skali globalnej. Aby spełnić wymagania dotyczące zgodności, niektóre firmy zdecydowały się wdrożyć duplikaty zasobów IT dla dostawców chmury w regionie. W przykładowej tabeli powyżej Niemcy są dobrym przykładem tego scenariusza. W tym przykładzie w Niemczech znajdują się klienci, partnerzy i pracownicy, ale nie ma żadnych istniejących zasobów IT. Firma może zdecydować się na wdrożenie niektórych zasobów do centrum danych w obszarze RODO, potencjalnie nawet przy użyciu niemieckich centrów danych platformy Azure. Zrozumienie danych, których dotyczy RODO, może pomóc zespołowi wdrożeniowemu ds. chmury zrozumieć najlepsze podejście do migracji w tym przypadku.

### <a name="why-is-the-location-of-end-users-relevant"></a>Dlaczego lokalizacja użytkowników końcowych jest ważna?

Firmy obsługujące użytkowników końcowych w wielu krajach opracowały rozwiązania techniczne dotyczące obsługi ruchu użytkowników końcowych. W niektórych przypadkach obejmuje to lokalizację zasobów. W innych scenariuszach firma może zdecydować się na wdrożenie globalnych rozwiązań sieci WAN w celu rozwiązania problemów z różnymi bazami użytkowników za pośrednictwem rozwiązań ukierunkowanych na sieć. We wszystkich przypadkach na strategię migracji mogą mieć wpływ profile użycia osobnych użytkowników końcowych.

Ze względu na to, że firma obsługuje pracowników, partnerów i klientów w Niemczech, ale w tym kraju nie ma obecnie centrów danych, najprawdopodobniej firma wdrożyła pewną formę rozwiązania dzierżawionego w celu skierowania tego ruchu do centrów danych w innych krajach. Ten istniejący routing stanowi znaczne ryzyko dla postrzeganej wydajności migrowanych aplikacji. Wprowadzanie dodatkowych przeskoków w ustalonej i dostrojonej globalnej sieci WAN może stworzyć wrażenie, że po migracji aplikacje działają z niedostateczną wydajnością. Znajdowanie i rozwiązywanie tych problemów może dodać do projektu znaczne opóźnienia. W każdym z poniższych procesów wskazówki dotyczące rozwiązywania problemów ze złożoności są przedstawione w ramach procesów dotyczących wymagań wstępnych, oceniania, migrowania i optymalizowania. Zrozumienie profilów użytkowników w poszczególnych krajach ma kluczowe znaczenie dla prawidłowego zarządzania tą złożonością.

### <a name="why-is-the-location-of-datacenters-relevant"></a>Dlaczego lokalizacja centrów danych jest ważna?

Lokalizacja istniejących centrów danych może mieć wpływ na strategię migracji. Poniżej przedstawiono kilka najczęstszych typów wpływu:

**Decyzje dotyczące architektury:** docelowy region/lokalizacja jest jednym z pierwszych kroków projektowania strategii migracji. Na ten element często wpływa lokalizacja istniejących zasobów. Ponadto dostępność usług w chmurze i koszt jednostkowy tych usług mogą różnić się w zależności od regionu. W związku z tym zrozumienie bieżącej i przyszłej lokalizacji zasobów wpływa na decyzje dotyczące architektury, a także może mieć wpływ na oszacowania budżetu.

**Zależności centrum danych:** na podstawie danych w powyższej tabeli można stwierdzić, że prawdopodobnie istnieją zależności między różnymi centrami danych na całym świecie. W wielu organizacjach, które działają na taką skalę, te zależności mogą nie być udokumentowane ani zrozumiałe. Metody służące do szacowania profilów użytkowników ułatwią zidentyfikowanie niektórych z tych zależności. Zalecamy jednak, aby w trakcie procesu oceny wykonać dodatkowe czynności w celu ograniczenia ryzyka związanego z tą złożonością.

## <a name="implementing-the-general-approach"></a>Implementowanie podejścia ogólnego

Takie podejście jest oparte na informacjach wymiernych. W związku z tym podejście to będzie zgodne z modelem opartym na danych w procesie rozwiązywania problemów z złożonością migracji globalnej.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Zaleca się, aby zespół wdrożeniowy ds. chmury rozpoczął proces migracji prostego obciążenia przy użyciu [przewodnika dotyczącego migracji na platformę Azure](../azure-migration-guide/index.md) przed podjęciem próby obsługi procesów na skalę globalną. Dzięki temu zespół będzie obeznany z ogólnym procesem migracji w chmurze przed próbą wykonania bardziej złożonego scenariusza migracji.

Gdy zakres migracji obejmuje wiele regionów, zespół wdrożeniowy ds. chmury powinien ocenić następujące zagadnienia dotyczące gotowości:

- Niezależność danych może wymagać lokalizacji niektórych zasobów, ale istnieje wiele zasobów, które mogą nie podlegać tym ograniczeniom zgodności. Elementy, takie jak rejestrowanie, raportowanie, routing sieciowy, tożsamość i inne centralne usługi IT, mogą być hostowane jako usługi udostępnione w wielu subskrypcjach, a nawet w wielu regionach. Zaleca się, aby zespół rozwiązań w chmurze mógł oszacować model usługi udostępniania dla tych usług, jak opisano w temacie dotyczącym [architektury referencyjnej topologii gwiazdy z usługami udostępnionymi](/azure/architecture/reference-architectures/hybrid-networking/shared-services)
- W przypadku wdrażania wielu wystąpień podobnych środowisk fabryka środowisk może stworzyć spójność, poprawić zarządzanie i przyspieszyć wdrażanie. W przypadku [podróży do zapewnienia ładu w dużych przedsiębiorstwach](../../governance/journeys/complex-enterprise/index.md) jest ustanawiane podejście, które tworzy fabrykę środowisk przeprowadzającą skalowanie w wielu regionach.

Gdy zespół zdobędzie doświadczenie dotyczące podejścia obejmującego punkty odniesienia, a elementy gotowości zostaną dopasowane, trzeba będzie wziąć pod uwagę kilka wymagań wstępnych opartych na danych:

- **Odnajdywanie ogólne:** wypełnij powyższą tabelę [Dokumentowanie złożoności](#documenting-complexity).
- **Przeprowadzenie analizy profilu użytkownika w każdym uwzględnionym kraju:** ważne jest, aby zrozumieć ogólny proces routingu użytkowników końcowych na wczesnym etapie procesu migracji. Zmiana globalnych linii dzierżawy i dodanie połączeń, takich jak usługa ExpressRoute, do centrum danych w chmurze może wymagać miesięcy opóźnienia pracy w sieci. Ten problem należy rozwiązać na jak najwcześniejszym etapie procesu.
- **Początkowa racjonalizacja majątku cyfrowego:** za każdym razem, gdy złożoność jest wprowadzana do strategii migracji, należy przeprowadzić wstępną racjonalizację majątku cyfrowego. Aby uzyskać pomoc, zapoznaj się ze wskazówkami dotyczącymi [racjonalizacji majątku cyfrowego](../../digital-estate/index.md).
  - **Dodatkowe wymagania dotyczące majątku cyfrowego:** ustanów zasady tagowania, aby identyfikować wszystkie obciążenia, których dotyczą wymagania związane z niezależnością danych. Wymagane tagi powinny rozpoczynać się na etapie racjonalizacji majątku cyfrowego i przechodzić do migrowanych zasobów.
- **Ocenianie modelu gwiazdy:** systemy rozproszone często używają wspólnych zależności. Zależności te mogą być często obsługiwane za pośrednictwem implementacji modelu gwiazdy. Chociaż taki model jest poza zakresem dla procesu migracji, należy oznaczyć go do uwzględnienia podczas przyszłych iteracji [gotowych procesów](../../ready/index.md).
- **Priorytetyzacja listy prac związanych z migracją:** Jeśli do obsługi wdrożenia produkcyjnego obciążenia w wielu regionach są wymagane zmiany sieci, ważne jest, aby zespół strategiczny ds. chmury śledził eskalacje tych zmian i zarządzał nimi. Wyższy poziom wsparcia kadry kierowniczej pomoże w przyspieszaniu zmiany. Jednak bardziej istotny wpływ polega na tym, że zespół ds. strategii może zmienić priorytet listy prac, aby zapewnić, że globalne obciążenia nie będą blokowane przez zmiany sieci. W przypadku takich obciążeń należy określać priorytety tylko po zakończeniu wprowadzania zmian sieci.

Te wymagania wstępne pomogą w ustanowieniu procesów, które mogą rozwiązać problemy z tym stopniem złożoności podczas wykonywania strategii migracji.

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

W przypadku pracy ze złożonościami globalnej bazy zasobów użytkowników istnieje kilka kluczowych działań, które należy dodać do oceny kandydatów do migracji. Każda z tych zmian zwiększy czytelność wpływu na użytkowników i zasoby globalne dzięki podejściu opartemu na danych.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

**Ocenianie zależności między centrami danych:** [narzędzia wizualizacji zależności w usłudze Azure Migrate](/azure/migrate/concepts-dependency-visualization) mogą pomóc w dokładnym określeniu zależności. Mówiąc ogólnie, użycie tego zestawu narzędzi przed migracją jest dobrym rozwiązaniem. Jednak w przypadku obsługi złożoności na poziomie globalnym jest to niezbędny krok do procesu oceny. Za pośrednictwem [grupowania zależności](/azure/migrate/how-to-create-group-machine-dependencies) wizualizacja może ułatwić identyfikację adresów IP i portów zasobów wymaganych do obsługi obciążenia.

> [!IMPORTANT]
> Dwie ważne uwagi: Po pierwsze do zidentyfikowania zasobów, które znajdują się w dodatkowym centrum danych, będzie potrzebny ekspert z dziedziny rozmieszczania zasobów i schematów adresów IP. Po drugie ważne jest, aby oszacować zależności podrzędne i klientów w wizualizacji w celu zrozumienia zależności dwukierunkowych.

**Identyfikowanie wpływu na użytkowników globalnych:** dane wyjściowe analizy profilu użytkownika wymaganego wstępnie powinny identyfikować wszelkie obciążenia, na które mają wpływ globalne profile użytkowników. Gdy kandydat do migracji znajduje się na liście uwzględnionych obciążeń, architekt przygotowujący migrację powinien skonsultować się z ekspertami w dziedzinie sieci i operacji, aby zweryfikować oczekiwania dotyczące wydajności i routingu sieci. Architektura powinna obejmować przynajmniej połączenie usługi ExpressRoute między najbliższym centrum operacji sieciowych i platformą Azure. [Architektura referencyjna dla połączeń usługi ExpressRoute](/azure/architecture/reference-architectures/hybrid-networking/expressroute) może pomóc w konfiguracji niezbędnego połączenia.

**Projektowanie pod kątem zgodności:** dane wyjściowe analizy profilu użytkownika wymaganego wstępnie powinny identyfikować wszelkie obciążenia, na które mają wpływ wymagania dotyczące niezależności danych. W trakcie wykonywania działań architektury w procesie oceny przypisany architekt powinien skonsultować się z ekspertami z dziedziny zgodności, aby poznać wymagania dotyczące migracji/wdrożenia w wielu regionach. Te wymagania znacząco wpłyną na strategie projektowania. Architektury referencyjne dla [wieloregionowych aplikacji internetowych](/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) mogą pomóc w projektowaniu.

> [!WARNING]
> W przypadku korzystania z dowolnej spośród powyższych architektur referencyjnych może być konieczne wykluczenie określonych elementów danych z procesów replikacji, aby spełniać wymagania dotyczące niezależności danych. Spowoduje to dodanie dodatkowego kroku do procesu podwyższania poziomu.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas migrowania aplikacji, która musi zostać wdrożona w wielu regionach, zespół wdrożeniowy ds. chmury musi wziąć pod uwagę kilka kwestii. Dotyczą one projektu magazynu usługi Azure Site Recovery, projektu serwera konfiguracji/przetwarzania, projektów przepustowości sieci i synchronizacji danych.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

**Projekt magazynu usługi Microsoft Azure Site Recovery:** usługa Azure Site Recovery to sugerowane narzędzie do replikacji w chmurze i synchronizowania zasobów cyfrowych z platformą Azure. Usługa Site Recovery replikuje dane dotyczące zasobów do magazynu usługi Site Recovery, który jest powiązany z określoną subskrypcją w określonym regionie i centrum danych platformy Azure. W przypadku replikowania zasobów do drugiego regionu może być wymagany drugi magazyn usługi Site Recovery.

**Projekt serwera konfiguracji/przetwarzania:** Usługa Site Recovery współpracuje z lokalnym wystąpieniem serwera konfiguracji i przetwarzania, który jest powiązany z pojedynczym magazynem usługi Site Recovery. Oznacza to, że może być konieczne zainstalowanie drugiego wystąpienia tych serwerów w źródłowym centrum danych w celu ułatwienia replikacji.

**Projekt przepustowości sieci:** Podczas replikacji i trwającej synchronizacji dane binarne są przenoszone przez sieć ze źródłowego centrum danych do magazynu usługi Site Recovery w docelowym centrum danych platformy Azure. Ten proces zużywa przepustowość. W przypadku duplikowania obciążenia do drugiego regionu ilość zużytej przepustowości zostanie podwojona. Gdy przepustowość jest ograniczona lub obciążenie wiąże się z dużą ilością konfiguracji lub dryfem danych, może to zakłócać czas wymagany do przeprowadzenia migracji. Co ważniejsze, może mieć to wpływ na środowisko użytkowników lub aplikacji, które nadal zależą od przepustowości centrum danych.

**Synchronizacja danych:** Często największy odpływ przepustowości pochodzi z synchronizacji platformy danych. Zgodnie z definicją w architekturach referencyjnych dla [wieloregionowych aplikacji internetowych](/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) synchronizacja danych jest często wymagana w celu dopasowania aplikacji. Jeśli jest to żądany stan operacyjny aplikacji, może być konieczne przeprowadzenie synchronizacji między źródłową platformą danych i wszystkimi platformami w chmurze przed migracją zasobów aplikacji i warstwy środkowej.
**Synchronizacja danych:** Często największy odpływ przepustowości pochodzi z synchronizacji platformy danych. Zgodnie z definicją w architekturach referencyjnych dla [wieloregionowych aplikacji internetowych](/azure/architecture/reference-architectures/app-service-web-app/multi-region) i [wieloregionowych aplikacji n-warstwowych](/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) synchronizacja danych jest często wymagana w celu dopasowania aplikacji. Jeśli jest to żądany stan operacyjny aplikacji, może być konieczne przeprowadzenie synchronizacji między źródłową platformą danych i wszystkimi platformami w chmurze przed migracją zasobów aplikacji i warstwy środkowej.

**Odzyskiwanie po awarii Azure–Azure:** jest to alternatywna opcja, która może jeszcze bardziej obniżyć stopień złożoności. Jeśli osie czasu i synchronizacja danych zbliżają się do wdrożenia dwuetapowego, usługa [Odzyskiwanie po awarii Azure–Azure](/azure/site-recovery/azure-to-azure-architecture) może być akceptowalnym rozwiązaniem. W tym scenariuszu obciążenie jest migrowane do pierwszego centrum danych platformy Azure przy użyciu jednego magazynu usługi Site Recovery oraz projektu serwera konfiguracji lub przetwarzania. Po przetestowaniu obciążenia można je odzyskać do drugiego centrum danych platformy Azure z migrowanych zasobów. Takie podejście zmniejsza wpływ na zasoby w źródłowym centrum danych i korzysta z większych szybkości transferu oraz ograniczeń przepustowości dostępnych między centrami danych platformy Azure.

> [!NOTE]
> Takie podejście może zwiększyć krótkoterminowy koszt migracji, ponieważ może spowodować naliczenie dodatkowych opłat za przepustowość ruchu wychodzącego.

## <a name="optimize-and-promote-process-changes"></a>Zmiany procesu optymalizacji i podwyższania poziomu

Rozwiązywanie problemów z globalną złożonością podczas optymalizacji i podwyższania poziomu może wymagać zduplikowanej pracy w każdym z dodatkowych regionów. W przypadku przyjęcia jednego wdrożenia można nadal wymagać duplikowania testowania biznesowego i planów zmian biznesowych.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Sugerowana akcja w trakcie procesu optymalizacji i podwyższania poziomu

**Wstępne testowanie optymalizacji:** początkowe testowanie automatyzacji może zidentyfikować potencjalne możliwości optymalizacji, podobnie jak w przypadku dowolnych czynności związanych z migracją. W przypadku obciążeń globalnych ważne jest, aby testować obciążenie w poszczególnych regionach niezależnie, ponieważ drobne zmiany konfiguracji w sieci lub docelowym centrum danych platformy Azure mogą mieć wpływ na wydajność.

**Plan zmian biznesowych:** w przypadku każdego złożonego scenariusza migracji zaleca się utworzenie planu zmiany biznesowej w celu zapewnienia jasnej komunikacji dotyczącej wszelkich zmian procesów biznesowych, środowiska użytkownika i harmonogramu działań koniecznych do zintegrowania zmian. W przypadku globalnych działań związanych z migracją plan powinien obejmować zagadnienia dotyczące użytkowników końcowych w poszczególnych lokalizacjach geograficznych.

**Testowanie biznesowe:** w połączeniu z planem zmian biznesowych testowe biznesowe może być wymagane w każdym regionie w celu zapewnienia odpowiedniej wydajności i przestrzegania zmodyfikowanych wzorców routingu sieciowego.

**Pakiet testowy podwyższania poziomu:** Często podwyższenie poziomu odbywa się jako pojedyncze działanie, które powoduje przekierowanie ruchu produkcyjnego do migrowanych obciążeń. W przypadku globalnych działań dotyczących wydań zaleca się, aby podwyższenie poziomu była przeprowadzane w ramach pakietów testowych (lub wstępnie zdefiniowanych kolekcji użytkowników). Dzięki temu zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury będą mogły skuteczniej obserwować wydajność i ulepszać obsługę użytkowników w poszczególnych regionach. Pakiety testowe podwyższania poziomu są często kontrolowane na poziomie sieci przez zmianę routingu konkretnych zakresów adresów IP z zasobów obciążeń źródłowych do nowo migrowanych zasobów. Po przeprowadzeniu migracji określonej kolekcji użytkowników końcowych można przekierować następną grupę.

**Optymalizacja pakietów testowych:** Jedną z zalet pakietów testowych podwyższania poziomu jest umożliwienie dokładniejszych obserwacji i dodatkowej optymalizacji wdrożonych zasobów. Po krótkim okresie użycia w produkcji przez pierwszy pakiet testowy zaleca się uściślenie migrowanych zasobów, jeśli jest dozwolone przez procedury operacyjne działu IT.

## <a name="next-steps"></a>Następne kroki

Osobny punkt złożoności, często odnoszący się do wielu regionów, to potrzeba przygotowania do migracji [wielu centrów danych](./multiple-datacenters.md). Mimo że jej charakter jest podobny, ta złożoność jest związana z ilością zasobów do migracji podczas przenoszenia wielu centrów danych do chmury.

> [!div class="nextstepaction"]
> [Migrowanie wielu centrów danych](./multiple-datacenters.md)
