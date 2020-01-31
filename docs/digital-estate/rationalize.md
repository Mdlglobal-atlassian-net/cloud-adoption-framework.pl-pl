---
title: Racjonalizacja majątku cyfrowego
description: Oceń swoje zasoby cyfrowe, aby określić, jak najlepiej hostować je w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: c618e6c1cf83199ae55df44397e07f3755fbb1f8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76804558"
---
# <a name="rationalize-the-digital-estate"></a>Racjonalizacja majątku cyfrowego

Racjonalizacja chmury to proces oceniania zasobów w celu ustalenia najlepszego podejścia do obsługi ich w chmurze. Po ustaleniu [podejścia](./approach.md) i zagregowaniu [spisu](./inventory.md)można rozpocząć racjonalizację chmury. Racjonalizacja chmury omawia najbardziej typowe opcje racjonalizacji.

## <a name="traditional-view-of-rationalization"></a>Tradycyjny widok racjonalizacji

Można łatwo zrozumieć racjonalizację podczas wizualizowania tradycyjnego procesu racjonalizacji jako złożonego drzewa decyzyjnego. Każdy element zawartości w obszarze cyfrowym jest podawany przez proces, który skutkuje jedną z pięciu odpowiedzi (5 RS). W przypadku małych Estates ten proces działa prawidłowo. W przypadku większych Estates jest to niewydajne i może prowadzić do znaczących opóźnień. Przeanalizujmy proces, aby zobaczyć dlaczego. Następnie przedstawimy bardziej wydajny model.

**Spis:** Dokładne spisy zasobów, w tym aplikacje, oprogramowanie, sprzęt, systemy operacyjne i metryki wydajności systemu, są wymagane do ukończenia pełnej racjonalizacji przy użyciu tradycyjnych modeli.

**Analiza ilościowa:** W drzewie decyzyjnym pytania ilościowe decydują o pierwszej warstwie decyzji. Często zadawane pytania są następujące: czy zasób jest używany dzisiaj? Jeśli tak, czy jest to zoptymalizowane i poprawnie dopasowane? Jakie zależności istnieją między elementami zawartości? Te pytania mają kluczowe znaczenie dla klasyfikacji spisu.

**Analiza jakościowa:** Kolejny zestaw decyzji wymaga analizy ludzkiej w formie analizy jakościowej. Często pytania, które znajdują się w tym miejscu, są unikatowe dla rozwiązania i mogą być odpowiedzi tylko przez zainteresowane strony i użytkowników zaawansowanych. Te decyzje zwykle opóźnią proces, co zmniejsza się znacznie. Ta analiza zwykle wykorzystuje od 40 do 80 godzin w danym miesiącu.

Aby uzyskać wskazówki dotyczące tworzenia listy pytań dotyczących analizy jakościowej, zobacz [podejścia do planowania elementów cyfrowych](./approach.md).

**Decyzja o racjonalizacji:** Dane jakościowe i ilościowe są tworzone w ramach praktycznego zespołu z racjonalizacją. Niestety, zespoły o wysokim stopniu racjonalizacji są kosztowne do wynajmu lub podjęcia miesięcy do szkolenia.

## <a name="rationalization-at-enterprise-scale"></a>Racjonalizacja na skalę przedsiębiorstwa

Jeśli ten proces jest czasochłonny i zniechęcające na cyfrową maszynę wirtualną 50, Wyobraź sobie, że jest to konieczne do przeprowadzenia transformacji biznesowej w środowisku z tysiącami maszyn wirtualnych i setek aplikacji. Wymagany nakład pracy może łatwo przekroczyć 1 500 nadgodzin i dziewięciu miesięcy planowania.

Chociaż pełna racjonalizacja jest stanem końcowym i świetnym sposobem przejścia w program, rzadko tworzy wysoki zwrot z inwestycji w odniesieniu do czasu i energii, która jest wymagana.

Gdy racjonalizacja jest niezbędna do podejmowania decyzji finansowych, warto zastanowić się nad organizacją usług profesjonalnych, która specjalizacji w celu przyspieszenia procesu. Nawet w przypadku, gdy pełna racjonalizacja może być kosztowne i czasochłonne, które opóźniają transformację lub wyniki biznesowe.

W pozostałej części tego artykułu opisano alternatywne podejście, znane jako racjonalizacja przyrostowa.

## <a name="incremental-rationalization"></a>Racjonalizacja przyrostowa

Pełna racjonalizacja dużej ilości cyfrowej jest podatna na ryzyko i może odnieść opóźnienia ze względu na złożoność. Przyjęto założenie, że opóźnione decyzje rozkładają obciążenie firmy, aby zmniejszyć ryzyko wystąpienia przeszkody. W miarę upływu czasu takie podejście tworzy model organiczny służący do opracowywania procesów i doświadczenia wymagane do bardziej wydajnego podejmowania kwalifikowaną decyzje o racjonalizacji.

### <a name="inventory-reduce-discovery-data-points"></a>Spis: Zmniejsz liczbę punktów danych odnajdywania

Niektóre organizacje zainwestowają czas, energię i koszty w celu zapewnienia dokładnego, w czasie rzeczywistym spisu pełnej cyfrowej. Nieprzerwane, kradzież, cykle odświeżania i dołączanie pracownika często uzasadnia szczegółowe śledzenie zasobów urządzeń użytkowników końcowych. Jednak zwrot z inwestycji związanych z utrzymywaniem dokładnego serwera i spisu aplikacji w tradycyjnym lokalnym centrum danych jest często niski. Większość organizacji IT ma inne problemy, które należy spełnić, aby nie śledzić użycia stałych zasobów w centrum danych.

W przypadku transformacji w chmurze spis bezpośrednio jest skorelowany z kosztami operacyjnymi. Dokładne planowanie jest wymagane w celu zapewnienia odpowiednich danych spisu. Niestety, bieżące opcje skanowania środowiska mogą opóźniać decyzje według tygodni lub miesięcy. Na szczęście kilka lew może przyspieszyć zbieranie danych.

Skanowanie oparte na agencie jest najczęściej cytowanym opóźnieniem. Niezawodne dane, które są wymagane dla tradycyjnej racjonalizacji, często mogą być zbierane tylko przy użyciu agenta uruchomionego na każdym z zasobów. Ta zależność od agentów często spowalnia postęp, ponieważ może wymagać informacji o zabezpieczeniach, działaniach i funkcjach administracyjnych.

W procesie zwiększania racjonalizacji rozwiązanie bez agenta może służyć do początkowego odnajdywania w celu przyspieszenia wczesnych decyzji. W zależności od stopnia złożoności w środowisku rozwiązanie oparte na agentach może być nadal wymagane. Można go jednak usunąć ze ścieżki krytycznej do zmiany firmy.

### <a name="quantitative-analysis-streamline-decisions"></a>Analiza ilościowa: Usprawnij decyzje

Bez względu na sposób odnajdywania spisu analizy ilościowe mogą być na początku podejmowane decyzje i założenia. Jest to szczególnie ważne podczas próby zidentyfikowania pierwszego obciążenia lub, gdy celem racjonalizacji jest porównanie kosztów wysokiego poziomu. W procesie zwiększania racjonalizacji zespół strategii chmury i zespoły wdrożeniowe chmury ograniczają [pięć pięciu](./5-rs-of-rationalization.md) decyzji i stosują te czynniki ilościowe. Usprawnia to analizę i zmniejsza ilość danych początkowych wymaganych do zmiany dysku.

Na przykład jeśli organizacja jest w pośrodku migracji IaaS do chmury, można założyć, że większość obciążeń zostanie wycofana lub przeszukana.

### <a name="qualitative-analysis-temporary-assumptions"></a>Analiza jakościowa: tymczasowe założenia

Zmniejszając liczbę potencjalnych wyników, łatwiej jest uzyskać wstępną decyzję dotyczącą przyszłego stanu elementu zawartości. Po zmniejszeniu tych opcji można także zmniejszyć liczbę pytań na ten wczesny etap.

Jeśli na przykład opcje są ograniczone do rehostowania lub wycofywania, firma musi odpowiedzieć tylko na jedno pytanie podczas wstępnej racjonalizacji, czyli czy wycofać element zawartości.

"Analiza sugeruje, że żaden użytkownik nie korzysta aktywnie z tego elementu zawartości. Czy ma to dokładne znaczenie? Takie pytanie binarne jest zwykle znacznie łatwiejsze do uruchomienia za pomocą analizy jakościowej.

To usprawnione podejście zapewnia podstawy, plany finansowe, strategię i kierunek. W późniejszych działaniach każdy element zawartości przechodzi przez dalszą racjonalizację i analizę jakościową, aby oszacować inne opcje. Wszystkie założenia, które należy wykonać w tej wstępnej racjonalizacji, są testowane przed

## <a name="challenge-assumptions"></a>Założenia wyzwania

Wynik poprzedniej sekcji stanowi niekompletną racjonalizację, która jest założeń. Następnie należy zastanowić się, że założono niektóre z tych założeń.

### <a name="retire-assets"></a>Wycofywanie zasobów

W tradycyjnych środowiskach lokalnych hosting małych niewykorzystanych zasobów rzadko powoduje znaczący wpływ na koszty roczne. Z kilkoma wyjątkami, nakładu pracy, które są wymagane do przeanalizowania i wycofania rzeczywistego środka trwałego, jest zmniejszenie kosztów związanych z oczyszczaniem i wycofywanie tych zasobów.

Jednak po przejściu do modelu ewidencjonowania aktywności w chmurze wycofane zasoby mogą generować znaczne oszczędności w rocznych kosztach operacyjnych i w ramach wysiłków związanych z migracją.

Nierzadko zdarza się, aby organizacje wycofali 20% lub więcej ich cyfr cyfrowych po zakończeniu analizy ilościowej. Przed podjęciem decyzji o takiej akcji zalecamy przeprowadzenie dalszej analizy jakościowej. Po potwierdzeniu tego stanu wycofanie tych zasobów może wyprodukować pierwszy Victory z inwestycji w migrację w chmurze. W wielu przypadkach jest to jeden z największych czynników oszczędności kosztów. W związku z tym firma Microsoft zaleca, aby zespół strategii chmury nadzorował weryfikację i emeryturę zasobów, równolegle z fazą kompilacji procesu migracji, aby umożliwić wczesne wygranie finansowe.

### <a name="program-adjustments"></a>Korekty programu

Firma rzadko loguje się tylko do jednej podróży transformującej. Wybór między obniżką kosztów, wzrostem rynku i nowymi strumieniami przychodów jest rzadko podejmowana w postaci binarnej. W związku z tym zaleca się, aby zespół strategii chmury pracował z działem IT w celu identyfikowania zasobów na potrzeby równoległych wysiłków transformacji, które są poza zakresem podstawowej podróży transformacji.

W przykładzie migracji IaaS podanym w tym artykule:

- Poproszenie zespołu DevOps o identyfikację zasobów, które są już częścią automatyzacji wdrożenia, i usunięcie tych zasobów z podstawowego planu migracji.

- Zwróć się do zespołów danych i R & D, aby identyfikować zasoby, które obsługują nowe strumienie przychodu i usuwać je z podstawowego planu migracji.

Ta ukierunkowana na program analiza jakościowa może być wykonywana szybko i tworzy wyrównanie między wieloma zaległościami migracji.

Nadal może być konieczne rozważenie niektórych zasobów jako zasobów rehosta przez pewien czas. Po wstępnym zakończeniu migracji można przeprowadzić fazę w dalszej części.

## <a name="select-the-first-workload"></a>Wybierz pierwsze obciążenie

Implementacja pierwszego obciążenia jest kluczem do testowania i uczenia się. Jest to pierwsza okazja do pokazania i utworzenia sposób myślenia wzrostu.

### <a name="business-criteria"></a>Kryteria biznesowe

Aby zapewnić przejrzystość biznesową, zidentyfikuj obciążenie, które jest obsługiwane przez członka jednostki biznesowej zespołu strategii chmurowej. Najlepiej wybrać jedną z nich, w której zespół ma przyznany udział i silną motywację do przejścia do chmury.

### <a name="technical-criteria"></a>Kryteria techniczne

Wybierz obciążenie, które ma minimalne zależności i można je przenieść jako niewielką grupę zasobów. Zalecamy wybranie obciążenia ze zdefiniowaną ścieżką do testowania, aby ułatwić sprawdzanie poprawności.

Pierwsze obciążenie jest często wdrażane w eksperymentalnym środowisku bez możliwości działania ani zarządzania. Ważne jest, aby wybrać obciążenie, które nie współdziała z bezpiecznymi danymi.

### <a name="qualitative-analysis"></a>Analiza jakościowa

Zespoły rozwiązań w chmurze i zespół strategii chmury mogą współdziałać ze sobą, aby analizować to małe obciążenie. Ta współpraca tworzy kontrolowaną możliwość tworzenia i testowania kryteriów analizy jakościowej. Mniejsza populacja pozwala na zbadanie użytkowników, których dotyczy ten komunikat, oraz ukończenie szczegółowej analizy jakościowej w ciągu tygodnia lub mniej. W przypadku typowych czynników analizy jakościowej zapoznaj się z konkretną tarczą racjonalizacji w [5 RS](./5-rs-of-rationalization.md).

### <a name="migration"></a>Migracja

Równolegle z ciągłą racjonalizacją zespół ds. wdrażania chmury może rozpocząć migrację małego obciążenia, aby rozwijać uczenie w następujących kluczowych obszarach:

- Wzmocnij umiejętności dzięki platformie dostawcy chmury.
- Zdefiniuj podstawowe usługi (i standardy platformy Azure), które muszą być odpowiednie do długoterminowej wizji.
- Lepiej zrozumieć, jak operacje mogą wymagać zmiany w dalszej części transformacji.
- Zapoznaj się ze wszystkimi nieodłącznymi zagrożeniami biznesowymi i tolerancją biznesową dla tych zagrożeń.
- Ustanów linię bazową lub minimalny produkt żywotny (MVP) na potrzeby zarządzania w oparciu o tolerancję ryzyka dla działalności firmy.

## <a name="release-planning"></a>Planowanie wydania

Podczas gdy zespół ds. wdrażania w chmurze wykonuje migrację lub implementację pierwszego obciążenia, zespół strategii chmury może rozpocząć ustawianie priorytetów pozostałych aplikacji i obciążeń.

### <a name="power-of-10"></a>Moc 10

Tradycyjne podejście do racjonalizacji próbuje spełnić wszystkie przewidywalne potrzeby. Na szczęście plan dla każdej aplikacji często nie jest wymagany do rozpoczęcia podróży transformacji. W modelu przyrostowym moc 10 zapewnia dobry punkt wyjścia. W tym modelu zespół strategii chmury wybiera pierwsze 10 aplikacji do migracji. Te dziesięć obciążeń powinny zawierać kombinację prostych i złożonych obciążeń.

### <a name="build-the-first-backlogs"></a>Kompiluj pierwsze zaległości

Zespoły wdrożenia chmury i zespół strategii chmury mogą współdziałać z analizą jakościową dla pierwszych 10 obciążeń. Ten nakład pracy powoduje utworzenie pierwszej priorytetyzacji zaległości migracji oraz pierwszej priorytetyzacji zaległych wersji. Ta metoda umożliwia zespołom iteracyjne wykonywanie iteracji i zapewnia wystarczająco dużo czasu, aby utworzyć odpowiedni proces analizy jakościowej.

### <a name="mature-the-process"></a>Przedwczesne procesy

Po zaakceptowaniu przez dwa zespoły kryteriów analizy jakościowej można wykonać zadanie oceny w każdej iteracji. Osiągnięcie konsensusu w kryteriach oceny zwykle wymaga od dwóch do trzech wydań.

Po przeniesieniu oceny do procesu wykonywania przyrostowego migracji zespół rozwiązań w chmurze może szybciej wykonywać iteracje w zakresie oceny i architektury. Na tym etapie zespół strategii chmury jest również abstrakcyjny, co skraca czas ich opróżniania. Dzięki temu zespół strategii chmury może skoncentrować się na priorytetyzacji aplikacji, które nie znajdują się jeszcze w określonej wersji, co zapewnia ścisłe wyrównanie z zmianami warunków rynkowych.

Nie wszystkie aplikacje z priorytetami są gotowe do migracji. Sekwencjonowanie może ulec zmianie, ponieważ zespół wykonuje dokładniejszą analizę jakości i odnajduje zdarzenia biznesowe i zależności, które mogą monitować o zmianę priorytetyzacji zaległości. Niektóre wydania mogą grupować ze sobą niewielką liczbę obciążeń. Inne osoby mogą tylko zawierać pojedyncze obciążenie.

Zespół wdrażania w chmurze może uruchamiać iteracje, które nie generują kompletnej migracji obciążenia. Im mniejsze obciążenie i mniejszą liczbę zależności, tym bardziej prawdopodobnie obciążenie będzie pasować do jednego przebiegu lub iteracji. Z tego powodu zaleca się, aby pierwsze kilka aplikacji w zaległości wydania było małe i zawierać kilka zależności zewnętrznych.

## <a name="end-state"></a>Stan końcowy

Wraz z upływem czasu, połączenie zespołu do wdrażania w chmurze i zespołu strategii chmurowej przeprowadzi pełną racjonalizację spisu. Jednak takie przyrostowe podejście umożliwia zespołom szybkie szybsze działanie w procesie racjonalizacji. Pomaga również przekształceniu transformację, aby szybko dać rzeczowe wyniki biznesowe, bez konieczności przeprowadzenia analizy z góry.

W niektórych przypadkach model finansowy może być zbyt ścisły, aby podejmować decyzje bez dodatkowej racjonalizacji. W takich przypadkach może być konieczne bardziej tradycyjne podejście do racjonalizacji.

## <a name="next-steps"></a>Następne kroki

Wynikiem wysiłku związanego z racjonalizacją jest priorytetowe zaległości wszystkich zasobów, których dotyczy wybrana transformacja. Ta zaległość jest teraz gotowa do użycia jako podstawa dla modeli kosztów usług Cloud Services.

> [!div class="nextstepaction"]
> [Wyrównaj modele kosztów z użyciem cyfr cyfrowych](./calculate.md)
