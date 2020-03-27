---
title: Przygotowanie do złożoności zarządzania zmianami Agile
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby przygotować architektów w chmurze do konwersacji z zarządzaniem projektami w celu wyjaśnienia koncepcji zarządzania zmianami.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 56c7d171d46813d7175e93759be10ce1423115b0
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355165"
---
<!-- cSpell:ignore ITSM TOGAF -->

# <a name="prepare-for-technical-complexity-agile-change-management"></a>Przygotowanie do złożoności technicznej: zarządzanie zmianami zwinnymi (Agile)

Gdy całe centrum danych można anulować i utworzyć ponownie za pomocą jednego wiersza kodu, procesy tradycyjne pozostają w tyle. Wskazówki w całej strukturze Cloud Adoption Framework opierają się na praktykach, takich jak zarządzanie usługami informatycznymi (narzędzia ITSM), Open Group Architecture Framework (TOGAF) itp. Jednak w celu zapewnienia elastyczności i czasu reakcji na zmianę w ramach działalności struktura kształtuje te metody, aby dostosować je do metodologii zwinnych oraz rozwiązań DevOps.

Podczas przechodzenia do modelu zwinnego, w którym kładzie się nacisk na elastyczność i iterację, złożoność techniczna i zarządzanie zmianami są obsługiwane inaczej niż w przypadku tradycyjnego modelu kaskadowego skoncentrowanego na serii liniowej kroków migracji. W tym artykule przedstawiono rozwiązanie wysokiego poziomu mające na celu zmianę zarządzania w ramach nakładu pracy związanego z migracją opartego na metodzie zwinnej. Po przeczytaniu tego artykułu będziesz mieć ogólną wiedzę na temat poziomów zarządzania zmianami oraz dokumentacji używanej podczas migracji przyrostowej. W oparciu o tę wiedzę na potrzeby wyboru i wdrożenia praktyk zwinnych wymagane są dodatkowe szkolenia i decyzje. Artykuł ten ma na celu przygotowanie architektów chmury do rozmowy z menedżerami projektów i wyjaśnienie ogólnej koncepcji zarządzania zmianami w ramach tego rozwiązania.

## <a name="address-technical-complexity"></a>Rozdziel złożoność techniczną

W przypadku zmiany dowolnego systemu technicznego, złożoność i współzależność stwarzają dla planów projektu ryzyko. Migracje do chmury nie są wyjątkiem. Podczas przenoszenia tysięcy lub &mdash;dziesiątków tysięcy&mdash; elementów zawartości do chmury takie ryzyko jeszcze rośnie. Wykrywanie i mapowanie wszystkich zależności w dużym majątku cyfrowym może potrwać lata. Jest niewiele firm, które mogłyby tolerować tak długi cykl analizy. Aby zrównoważyć zapotrzebowanie na analizę architektury i szybki rozwój firmy, struktura Cloud Adoption Framework koncentruje się na modelu INVEST do zarządzania listą prac produktu. W poniższych sekcjach podsumowano ten typ modelu.

## <a name="invest-in-workloads"></a>Model INVEST w obciążeniach

W strukturze Cloud Adoption Framework pojawia się termin _obciążenie_. Obciążenie to jednostka funkcji aplikacji, którą można migrować do chmury. Może to być pojedyncza aplikacja, warstwa aplikacji lub kolekcja aplikacji. Definicja jest elastyczna i może ulec zmianie w różnych frazach migracji. Struktura Cloud Adoption Framework używa terminu _invest_ do zdefiniowania obciążenia.

INVEST jest powszechnym akronimem w wielu metodologiach zwinnych do pisania historii użytkownika lub elementów listy prac i w obu przypadkach są to jednostki danych wyjściowych w narzędziach do zarządzania projektami zwinnymi. Wymierną jednostką danych wyjściowych w migracji jest zmigrowane obciążenie. Struktura Cloud Adoption Framework modyfikuje nieco akronim INVEST, aby utworzyć konstrukcję do definiowania obciążeń:

- **Niezależne:** Obciążenie nie powinno mieć żadnych niedostępnych zależności. Aby obciążenie zostało uznane za zmigrowane, wszystkie zależności powinny być dostępne i uwzględnione w nakładzie prac związanych z migracją.
- **Zbywalne:** W miarę przeprowadzania dodatkowego odnajdywania zostanie zmieniona definicja obciążenia. Architekci planujący migrację mogą negocjować czynniki dotyczące zależności. Przykłady punktów negocjacji mogą obejmować wstępną wersję funkcji, udostępnianie funkcji za pośrednictwem sieci hybrydowej lub pakowanie wszystkich zależności w jednej wersji.
- **Cenne:** Wartość w obciążeniu jest mierzona przez możliwość zapewnienia użytkownikom dostępu do obciążeń produkcyjnych.
- **Estimable:** Wszystkie zależności, zasoby, czas migracji, wydajność i koszty chmury powinny być estimable i powinny być szacowane przed migracją.
- **Małe:** Celem jest przypakowanie obciążeń w jednym przebiegu. Jednak nie zawsze może to być możliwe. Zamiast tego zachęcamy zespoły do planowania przebiegów i wersji tak, aby zminimalizować czas wymagany do przeniesienia obciążenia do środowiska produkcyjnego.
- **Weryfikowalne:** Zawsze powinien być zdefiniowany sposób testowania lub sprawdzania poprawności zakończenia migracji obciążenia.

Ten akronim nie musi być ściśle przestrzegany, ale powinien pomóc w wyjaśnieniu definicji terminu _obciążenie_.

## <a name="migration-backlog-aligning-business-priorities-and-timing"></a>Zaległości migracji: wyrównywanie priorytetów i terminów firmy

Zaległości migracji umożliwiają śledzenie teczki najwyższego poziomu obciążeń, które można migrować. Zachęcamy, aby przed migracją zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury przeprowadziły przegląd bieżącego [majątku cyfrowego](../../../digital-estate/index.md) oraz uzgodniły uporządkowaną według priorytetów listę obciążeń do migracji. Ta lista stanowi podstawę początkowej listy prac związanych z migracją.

Początkowo obciążenia listy prac związanych z migracją prawdopodobnie nie spełnią kryteriów INVEST przedstawionych w poprzedniej sekcji. Zamiast tego służą jako logiczne grupowanie zasobów z początkowego spisu jako symbol zastępczy na potrzeby pracy w przyszłości. Te symbole zastępcze mogą nie być dokładne z technicznego punktu widzenia, ale stanowią podstawę do koordynacji z działaniami biznesowymi.

![Relacja między migracją, wersją i listą prac iteracji użytymi podczas procesu migracji](../../../_images/migrate/backlog-relationships.png)

*Migracja, wersja i lista prac iteracji śledzą różne poziomy aktywności podczas procesów migracji.*

W ramach każdej listy prac migracji zespół zarządzający zmianami powinien dążyć do uzyskania następujących informacji dotyczących obciążeń w planie. Co najmniej te dane powinny być dostępne dla wszystkich obciążeń, które mają priorytet dla migracji w następnych dwóch lub trzech wersjach.

### <a name="migration-backlog-data-points"></a>Punkty danych listy prac migracji

- **Wpływ na firmę.** Zrozumienie wpływu na firmę w przypadku opuszczenia spodziewanej osi czasu lub zmniejszenia funkcjonalności podczas blokowania okien.
- **Względny priorytet biznesowy.** Uporządkowana lista obciążeń oparta na priorytetach firmy.
- **Właściciel firmy.** Ustal jedną osobę odpowiedzialną za podejmowanie decyzji biznesowych w odniesieniu do tego obciążenia.
- **Właściciel techniczny.** Ustal jedną osobę odpowiedzialną za podejmowanie decyzji technicznych związanych z tym obciążeniem.
- **Oczekiwane osie czasu.** Po zaplanowaniu ukończenia migracji.
- **Obciążenie zostaje zablokowane.** Horyzonty czasowe, w których obciążenie nie powinno kwalifikować się do zmiany.
- **Nazwa obciążenia.**
- **Początkowy spis.** Wszystkie zasoby wymagane do zapewnienia funkcjonalności obciążenia, w tym maszyny wirtualne, urządzenia IT, potoki danych, aplikacji, wdrażania itp. Te informacje są prawdopodobnie niedokładne.

## <a name="release-backlog-aligning-business-change-and-technical-coordination"></a>Zaległości wydania: wyrównywanie zmian w firmie i koordynacji technicznej

W kontekście migracji _wydanie_ jest działaniem, które wdraża w środowisku produkcyjnym co najmniej jedno obciążenie. Wydanie zazwyczaj obejmuje kilka iteracji lub prace techniczne. Reprezentuje jednak jedną iterację zmiany w firmie. Wydanie pojawia się po przygotowaniu co najmniej jednego obciążenia do podwyższenia poziomu produkcji. Decyzja o spakowaniu wydania jest podejmowana, gdy zmigrowane obciążenia stanowią wystarczającą wartość dla firmy, aby uzasadnić wprowadzenie zmian w środowisku biznesowym. Wersje są wykonywane w połączeniu z [planem zmian w firmie](../optimize/business-change-plan.md) po zakończeniu [testowania biznesowego](../optimize/business-test.md). Zespół strategiczny ds. chmury jest odpowiedzialny za planowanie i nadzorowanie wykonania wydania w celu zapewnienia, że wymagana zmiana w firmie zostanie wydana.

*Lista prac wydania* to plan przyszłego stanu określający nadchodzące wydanie. Lista prac wydania pełni rolę pośrednią między zarządzaniem zmianami w firmie (*lista prac migracji*) a zarządzaniem zmianami technicznymi (*lista prac przebiegu*). Lista prac wydania składa się z listy obciążeń uzyskanych z listy prac migracji, które są dostosowane do określonego podzestawu realizacji wyniku działania biznesowego. Zdefiniowanie i przesłanie listy prac wydania do zespołu wdrożeniowego ds. chmury stanowi sygnał do dokładniejszej analizy i planowania migracji. Gdy zespół wdrożeniowy ds. chmury sprawdzi informacje techniczne związane z wydaniem, może podjąć decyzję o zatwierdzeniu wydania, ustanawiając oś czasu wydania w oparciu o bieżącą wiedzę.

Mając na względzie stopień analizy wymagany do zweryfikowania wydania, zespół strategiczny ds. chmury powinien obsługiwać uruchomioną listę kolejnych dwóch do czterech wydań. Przed zdefiniowaniem i przesłaniem wydania zespół powinien również podjąć próbę zweryfikowania jak największej liczby następujących informacji. Zdyscyplinowany zespół strategiczny ds. chmury mający możliwość utrzymywania kolejnych czterech wydań może znacząco zwiększyć spójność i dokładność szacowania osi czasu wydania.

### <a name="release-backlog-data-points"></a>Punkty danych listy prac wydania

Zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury współpracują ze sobą, aby dodać następujące punkty danych dla wszelkich obciążeń na liście prac wydania:

- **Szczegółowy spis.** Walidacja wymaganych zasobów do migracji. Często walidacja jest przeprowadzana za pomocą danych z dzienników lub monitorowania na poziomie hosta, sieci lub systemu operacyjnego w celu zapewnienia dokładnych informacji na temat zależności sieciowych i sprzętowych poszczególnych zasobów w ramach obciążenia standardowego.
- **Wzorce użycia.** Informacje dotyczące wzorców użycia od użytkowników końcowych. Wzorce te często obejmują analizę rozkładu geograficznego użytkowników końcowych, trasy sieciowe, sezonowe wzrosty użycia, dzienne/godzinowe wzrosty użycia oraz kompozycję użytkownika końcowego (wewnętrzną i zewnętrzną).
- **Oczekiwania dotyczące wydajności.** Analiza dostępnych danych dziennika przechwytywania przepływności, wyświetleń stron, tras sieciowych i innych danych wydajności wymaganych do replikowania środowiska użytkownika końcowego.
- **Zależności.** Analiza wzorców ruchu sieciowego i użycia aplikacji w celu zidentyfikowania wszelkich dodatkowych zależności obciążeń, które powinny być zorientowane na sekwencjonowanie i gotowość na środowisko. Nie dołączaj obciążenia do wydania, dopóki nie zostanie spełnione jedno z następujących kryteriów:
  - Wszystkie obciążenia zależne zostały zmigrowane.
  - Wdrożono konfiguracje sieci i zabezpieczeń, aby umożliwić obciążeniu dostęp do wszystkich zależności zgodnie z istniejącymi oczekiwaniami dotyczącymi wydajności.
- **Pożądane rozwiązanie migracji.** Na poziomie listy prac migracji przyjęty nakład pracy związany z migracją stanowi jedyne kryterium używane podczas analizy. Na przykład, jeśli wynikiem biznesowym jest wyjście z istniejącego centrum danych, przyjmuje się, że wszystkie migracje stanowią scenariusz ponownego hostowania na liście prac migracji. Na liście prac wydania zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury powinny oszacować długoterminową wartość dodatkowych funkcji, modernizacji i stałych inwestycji rozwojowych w celu ocenienia, czy należy zastosować bardziej nowoczesne rozwiązanie.
- **Kryteria testowania biznesowego.** Po dodaniu obciążenia do listy prac migracji należy uzgodnić kryteria testowania. W niektórych przypadkach kryteria testowania mogą zostać ograniczone do testu wydajności w oparciu o zdefiniowaną grupę użytkowników zaawansowanych. Jednak na potrzeby weryfikacji statystycznej wymagany jest automatyczny test wydajnościowy, który również powinien zostać przeprowadzony. Istniejące wystąpienie aplikacji często nie ma możliwości testowania automatycznego. Jeśli tak się dzieje, architekci chmury często współpracują z użytkownikami zaawansowanymi w celu przygotowania testu obciążeniowego punktu odniesienia na istniejącym rozwiązaniu, aby zapewnić test porównawczy, który będzie używany podczas migracji.

### <a name="release-backlog-cadence"></a>Terminy listy prac wydania

W przypadku migracji nowszeh wydania pojawiają się regularnie. Szybkość pracy zespołu wdrożeniowego ds. chmury często się normalizuje, generując wydanie co dwie do czterech iteracji (mniej więcej co miesiąc lub co dwa miesiące). Powinien to być jednak wynik organiczny. Tworzenie sztucznej cadences wydania może negatywnie wpłynąć na zdolność zespołu wdrażania chmury do osiągnięcia spójnej przepływności.

Aby zapewnić stabilny wpływ na działalność biznesową, zespół strategiczny ds. chmury powinien ustanowić miesięczny proces wydania w firmie, aby utrzymać systematyczny dialog, jak również wyrazić oczekiwania, zgodnie z którymi minie kilka miesięcy, zanim będzie można przewidzieć regularny cykl wydania.

## <a name="sprint-or-iteration-backlog-aligning-technical-change-and-effort"></a>Zaległości przebiegu lub iteracji: wyrównywanie zmian technicznych i nakładów pracy

*Przebieg* lub *iteracja* to spójna, ograniczona czasowo jednostka pracy. W procesie migracji jest ona często mierzona w przyrostach dwutygodniowych. Nie jest to jednak możliwe w przypadku iteracji tygodniowych lub czterech tygodni. Tworzenie iteracji ograniczonych czasowo powoduje wymuszenie spójnych interwałów ukończenia nakładów pracy i pozwala na częstsze dostosowywanie planów na podstawie nowych informacji. W trakcie danego przebiegu są zwykle wykonywane zadania oceny, migracji i optymalizacji obciążeń zdefiniowane na liście prac migracji. Te jednostki pracy powinny być śledzone i zarządzane w tym samym narzędziu do zarządzania projektami, co lista prac migracji i wydania, aby zapewnić spójność na każdym poziomie zarządzania zmianami.

Działanie *listy prac przebiegu* lub *listy prac iteracji* polega na ukończeniu prac technicznych w ramach jednego przebiegu lub jednej iteracji, co prowadzi do migracji poszczególnych zasobów. Te prace powinny pochodzić z listy migrowanych obciążeń. W przypadku korzystania z narzędzi takich jak Azure DevOps (wcześniej Visual Studio Online) do zarządzania projektami elementy robocze w przebiegu będą elementami podrzędnymi elementów listy prac produktu na liście prac wydania oraz w epikach na liście prac migracji. Taka relacja nadrzędny-podrzędny umożliwia przejrzystość na wszystkich poziomach zarządzania zmianami.

W ramach jednego przebiegu lub jednej iteracji zespół wdrożeniowy ds. chmury pomoże zapewnić zatwierdzoną ilość pracy technicznej, prowadząc do migracji zdefiniowanego obciążenia. Jest to wynik końcowy strategii zarządzania zmianami. Po ich ukończeniu można te nakłady pracy przetestować, zatwierdzając gotowość produkcyjną obciążenia przygotowanego w chmurze.

### <a name="large-or-complex-sprint-structures"></a>Duże lub złożone struktury przebiegu

W przypadku małej migracji z udziałem samodzielnego zespołu ds. migracji jeden przebieg może obejmować wszystkie cztery fazy migracji dla jednego obciążenia (*oceny*, *migracji*, *optymalizacji* oraz *zabezpieczania i zarządzania*). Zazwyczaj każdy z tych procesów jest współużytkowany przez wiele zespołów w różnych elementach roboczych w wielu przebiegach. W zależności od typu nakładu pracy, jego skali i ról przebiegi te mogą mieć różną formę.

- **Fabryka migracji.** Migracje na dużą skalę czasami wymagają rozwiązania, które przypomina fabrykę w modelu wykonania. W tym modelu różne zespoły zostają przydzielone do wykonania określonego procesu migracji (lub podzestawu procesu). Po ukończeniu dane wyjściowe przebiegu jednego zespołu wypełniają listę prac dla następnego zespołu. Jest to wydajne rozwiązanie do migracji ponownego hostowania na dużą skalę wielu potencjalnych obciążeń obejmujących tysiące maszyn wirtualnych przechodzących przez fazy oceny, architektury, korygowania i migracji. Jednak, aby to rozwiązanie było skuteczne, niezbędne jest nowe jednorodne środowisko obejmujące usprawnione zarządzanie zmianami i procesy zatwierdzenia.
- **Fale migracji.** Inne rozwiązanie, które dobrze sprawdza się w przypadku dużych migracji, to model fal. W tym modelu podział pracy nie jest już tak oczywisty. Zespoły angażują się w wykonanie procesu migracji poszczególnych obciążeń. Jednak charakter każdego przebiegu jest inny. W jednym przebiegu zespół może ukończyć ocenę i pracę z architekturą. W innym przebiegu może zakończyć pracę z migracją. Jeszcze inny przebieg może koncentrować się na optymalizacji i wydaniu produkcji. Takie rozwiązanie pozwala, aby zespół podstawowy zachował zgodność z obciążeniami, które są dla niego widoczne w całym procesie. Podczas korzystania z tego rozwiązania różnorodność umiejętności i przełączanie kontekstu mogą zmniejszyć potencjalną szybkość pracy zespołu, spowalniając nakład pracy związany z migracją. Ponadto przeszkody w cyklach zatwierdzania mogą powodować znaczne opóźnienia. W przypadku tego modelu ważne jest, aby zachować opcje na liście prac wydania w celu utrzymania ciągłości działań zespołu w okresach zablokowanych. Ważne jest również, aby przeszkolić więcej członków zespołu i upewnić się, że zestawy umiejętności są wyrównane z motywem każdego przebiegu.

### <a name="sprint-backlog-data-points"></a>Punkty danych listy prac przebiegu

Wynik przebiegu przechwytuje i dokumentuje zmiany wprowadzone w obciążeniu, a tym samym zamyka pętlę zarządzania zmianami. Po zakończeniu należy udokumentować co najmniej następujące kwestie. W trakcie wykonywania przebiegu dokumentację tę należy sporządzić razem z technicznymi elementami roboczymi.

- **Wdrożone zasoby.** Wszystkie zasoby wdrożone w chmurze na potrzeby obsługi obciążenia.
- **Korygowanie.** Wszelkie zmiany zasobów w celu przygotowania do migracji do chmury.
- **Konfiguracja.** Wybrana konfiguracja wszystkich wdrożonych zasobów, w tym wszelkich odwołań do skryptów konfiguracji.
- **Model wdrażania.** Rozwiązanie używane podczas wdrażania zasobu w chmurze, w tym odwołań do skryptów lub narzędzi wdrażania.
- **Architektura.** Dokumentacja architektury wdrożonej w chmurze.
- **Metryki wydajności.** Dane wyjściowe testowania automatycznego lub testowania biznesowego wykonywanego w celu sprawdzenia wydajności w czasie wdrażania.
- **Unikatowe wymagania lub konfiguracja.** Wszelkie unikatowe aspekty wymagań w zakresie wdrażania, konfiguracji lub wymagań technicznych niezbędnych do obsługi obciążenia.
- **Zatwierdzenie operacyjne.** Zakończenie walidacji gotowości operacyjnej przez właściciela aplikacji oraz pracowników działu informatycznego odpowiedzialnych za zarządzanie obciążeniem po jego wdrożeniu.
- **Zatwierdzenie architektury.** Akceptacja właściciela obciążenia i zespołu wdrożeniowego ds. chmury w celu walidacji wszelkich zmian architektury wymaganych do obsługi poszczególnych zasobów.

## <a name="next-steps"></a>Następne kroki

Po określeniu rozwiązań w zakresie zarządzania zmianami nadszedł czas, by przedstawić ostatnie wymaganie wstępne. Zobacz temat [Migration backlog review](./migration-backlog-review.md) (Przegląd listy prac migracji).

> [!div class="nextstepaction"]
> [Migration backlog review](./migration-backlog-review.md) (Przegląd listy prac migracji)
