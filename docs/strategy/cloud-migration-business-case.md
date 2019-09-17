---
title: Przygotowanie uzasadnienia biznesowego migracji do chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zagadnienia dotyczące tworzenia uzasadnienia biznesowego migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 055c50ca2a934000b7e8d11927bc5ba1d4f95494
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030566"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>Przygotowanie uzasadnienia biznesowego migracji do chmury

Migracje w chmurze mogą generować wczesne zwroty z inwestycji w działania związane z przekształcaniem w chmurze. Jednak opracowywanie jasnego uzasadnienia biznesowego z istotnymi kosztami i zwrotami może być złożonym procesem. Ten artykuł pomoże Ci w zawieszeniu, jakie dane są potrzebne, aby utworzyć model finansowy, który jest zgodny z wynikami migracji do chmury. Najpierw Dispel kilka mitów o migracji do chmury, dzięki czemu Twoja organizacja może uniknąć niektórych typowych błędów.

## <a name="dispelling-cloud-migration-myths"></a>Mitów migracji do chmury

**Omówienia Chmura jest zawsze tańsza.** Często uważa się, że działanie centrum danych w chmurze jest zawsze tańsze niż lokalne działanie. To założenie może być zwykle prawdziwe, ale nie zawsze jest to konieczne. Czasami koszty operacyjne chmury są wyższe. Te wyższe koszty często wynikają z słabego ładu kosztów, niewyrównanych architektur systemu, duplikowania procesów, nietypowych konfiguracji systemu lub większego kosztu kadr. Na szczęście można złagodzić wiele z tych problemów, aby utworzyć Wczesne zwrotne. Postępując zgodnie ze wskazówkami dotyczącymi [tworzenia uzasadnienia biznesowego](#building-the-business-justification) , można wykryć i uniknąć tych nieodpowiednich wyrównania. Odpisownia innych mitów opisanych tutaj może pomóc.

**Omówienia Wszystkie elementy powinny przejść do chmury.** W rzeczywistości niektóre sterowniki biznesowe mogą prowadzić do wyboru rozwiązania hybrydowego. Przed zakończeniem pracy z modelem biznesowym, należy przeprowadzić analizę w pierwszej kolejności, zgodnie z opisem w artykułach o znakach [cyfrowych](../digital-estate/5-rs-of-rationalization.md). Aby uzyskać więcej informacji na temat indywidualnych sterowników ilościowych związanych z racjonalizacją, zobacz [5 RS](../digital-estate/5-rs-of-rationalization.md). Jedno z tych metod będzie używać łatwo uzyskane dane spisu i krótkiej analizy ilościowej w celu zidentyfikowania obciążeń lub aplikacji, które mogą spowodować zwiększenie kosztów w chmurze. Metody te mogą również identyfikować zależności lub wzorce ruchu, które wymagają rozwiązania hybrydowego.

**Omówienia Dublowanie środowiska lokalnego pomoże mi zaoszczędzić pieniądze w chmurze.** W przypadku planowania poza cyframi nie są one wykrywane przez firmy w celu wykrycia niewykorzystanej pojemności ponad 50% środowiska aprowizacji. Jeśli zasoby są obsługiwane w chmurze w celu dopasowania do bieżącej aprowizacji, oszczędności kosztów są trudne do realizacji. Rozważ zmniejszenie rozmiaru wdrożonych zasobów, aby wyrównać wzorce użycia zamiast wzorców udostępniania.

**Omówienia Koszty serwera na potrzeby migracji do chmury.** Czasami to założenie ma wartość true. W przypadku niektórych firm ważna jest redukcja bieżących wydatków inwestycyjnych związanych z serwerami. Jest to jednak zależne od kilku czynników. Firmy z pięcioma lata do ośmiu lat cykl odświeżania sprzętu prawdopodobnie nie będą widzieć szybkiego powracania do migracji w chmurze. Firmy z znormalizowanymi lub wymuszonymi cyklami odświeżania mogą szybko trafiać do punktu przerwania. W obu przypadkach inne wydatki mogą być wyzwalaczami finansowymi, które uzasadniają migrację. Poniżej przedstawiono kilka przykładów kosztów, które są często używane w przypadku, gdy firmy podejmują wyłącznie serwerową lub tylko maszynę wirtualną widok kosztów:

- Koszty oprogramowania dla wirtualizacji, serwerów i programów pośredniczących mogą być wszechstronne. Dostawcy chmury eliminują niektóre z tych kosztów. Dwa przykłady dostawcy chmury obniżają koszty wirtualizacji to [korzyść użycia hybrydowego platformy Azure](https://azure.microsoft.com/pricing/hybrid-benefit/#services) i programy [rezerwacji platformy Azure](https://azure.microsoft.com/reservations) .
- Straty biznesowe wynikające z przerwy mogą szybko przekroczyć koszty sprzętu lub oprogramowania. Jeśli bieżące centrum danych jest niestabilne, Pracuj z firmą, aby określić wpływ przestoju na koszty sprzedaży lub rzeczywiste koszty biznesowe.
- Koszty środowiska mogą być również istotne. W przypadku średniej rodziny American, dom to największe inwestycje i najwyższy koszt w budżecie. Takie samo jest często prawdziwe w przypadku centrów danych. Koszty związane z nieruchomościami, obiektami i narzędziami stanowią godziwą część kosztów lokalnych. W przypadku wycofania centrów danych te pomieszczenia mogą być przenoszone lub firma może potencjalnie zostać wykorzystana z tych kosztów całkowicie.

**Omówienia Model wydatków operacyjnych jest lepszy niż model wydatków inwestycyjnych.** Zgodnie z opisem w artykule dotyczącej [wyników podatkowych](./business-outcomes/fiscal-outcomes.md) , model wydatków operacyjnych może być dobry. Jednak niektóre branże powodują ujemne wyświetlanie wydatków operacyjnych. Poniżej przedstawiono kilka przykładów, które spowodują wyzwolenie ściślejszej integracji z jednostkami księgowości i biznesowymi w odniesieniu do konwersacji wydatków operacyjnych:

- Gdy firma widzi zasoby kapitałowe jako czynnik do oceny działalności biznesowej, obniżki wydatków kapitałowych mogą być wynikiem ujemnym. Chociaż nie jest to standardowy Standard, ten tonacji jest najczęściej widziany w branży handlowej, produkcyjnej i budowlanej.
- Prywatna firma lub firma, która dąży do napływu kapitału, może rozważyć zwiększenie kosztów operacyjnych.
- Jeśli firma koncentruje się na ulepszaniu marż sprzedaży lub obniżeniu kosztu sprzedanych towarów (KWS), wydatki operacyjne mogą być wynikiem ujemnym.

Firmy mogą lepiej zobaczyć koszty operacyjne, które są bardziej korzystne niż wydatki inwestycyjne. Na przykład takie podejście może być dobrze odebrane przez firmy, które próbują poprawić przepływ środków pieniężnych, zmniejszyć nakłady inwestycyjne lub zmniejszyć liczbę zatrzymań zasobów.

Przed wprowadzeniem uzasadnienia biznesowego, które koncentruje się na konwersji z wydatków inwestycyjnych na koszty operacyjne, rozumiesz, że jest to lepsze dla Twojej firmy. Rozliczanie i zaopatrzenie mogą często pomóc w dopasowaniu komunikatów do celów finansowych.

**Omówienia Przejście do chmury przypomina Przerzucanie przełącznika.** Migracje są ręcznie intensywną transformację techniczną. Podczas opracowywania uzasadnienia biznesowego, szczególnie uzasadnienia, które są zależne od czasu, należy wziąć pod uwagę następujące aspekty, które mogą zwiększyć czas migracji zasobów:

- **Ograniczenia przepustowości:** Przepustowość między bieżącym centrum danych a dostawcą chmury będzie mieć dyski osi czasu podczas migracji.
- **Testowanie osi czasu:** Testowanie aplikacji w firmie w celu zapewnienia gotowości i wydajności może być czasochłonne. Wyrównywanie użytkowników zaawansowanych i procesów testowania ma kluczowe znaczenie.
- **Osie czasu migracji:** Ilość czasu i nakład pracy wymagany do wdrożenia migracji mogą zwiększyć koszty i spowodować opóźnienia. Przydzielenie pracowników lub partnerów z umową może również opóźnić proces. Plan powinien uwzględniać te przydziały.

Przeszkody techniczne i kulturowe mogą spowalniać wdrażanie w chmurze. Gdy czas jest ważnym aspektem uzasadnienia biznesowego, najlepszym rozwiązaniem jest odpowiednie zaplanowanie. Podczas planowania dwa podejścia mogą pomóc w ograniczeniu ryzyka dotyczącego osi czasu:

- Zainwestowaj czas i energię w zrozumieniu ograniczeń technicznych wdrażania. Naciskanie na szybkie przenoszenie może być wysokie, dlatego ważne jest, aby uwzględnić realistyczne osie czasu.
- Jeśli wystąpią przeszkody kulturowe lub ludzie, będą one miały większe skutki niż ograniczenia techniczne. Wdrożenie chmury tworzy zmianę, która tworzy odpowiednie przekształcenie. Niestety, ludzie czasami zmieniają się i mogą potrzebować dodatkowej pomocy technicznej, aby dostosować ją do planu. Zidentyfikuj najważniejszych osób w zespole, którzy nie mają do nich zmiany i ich wczesnego zaangażowania.

Aby zmaksymalizować gotowość i uniknąć ryzyka związanego z osią czasu, przygotuj zainteresowanych członków kierownictwa poprzez zdecydowane dostosowanie wartości biznesowej i wyników działalności biznesowej. Pomóż tym udziałowcom zrozumieć zmiany, które będą miały wynik transformacji. Wyczyść i ustaw realistyczne oczekiwania od początku. Gdy ludzie lub technologie przestaną działać, łatwiej jest zarejestrować wsparcie dla kierownictwa.

## <a name="building-the-business-justification"></a>Tworzenie uzasadnienia biznesowego

Poniższy proces definiuje podejście do opracowania uzasadnienia biznesowego migracji do chmury. Aby uzyskać więcej informacji na temat obliczeń i warunków finansowych, zapoznaj się z artykułem dotyczącym [modeli finansowych](./financial-models.md).

W przypadku najwyższego poziomu formuła do uzasadnienia biznesowego jest prosta. Niedelikatne punkty danych wymagane do wypełnienia formuły mogą być trudne do wyrównania. Na poziomie podstawowym uzasadnienie biznesowe koncentruje się na zwrocie z inwestycji (zwrotnej) skojarzonej z proponowaną zmianą techniczną. Formuła ogólna dla zwrotu z inwestycji to:

![Zwroty zwrotne (zysk z inwestycji pomniejszonej o koszty inwestycji) podzielone według kosztów inwestycji](../_images/strategy/formula-roi.png)

Możemy rozpakować to równanie, aby uzyskać widok specyficzny dla migracji formuł dla zmiennych wejściowych po prawej stronie równania. Pozostałe sekcje tego artykułu zawierają pewne zagadnienia, które należy wziąć pod uwagę.

## <a name="migration-specific-initial-investment"></a>Wstępne inwestycje specyficzne dla migracji

- Dostawcy usług w chmurze, np. Kalkulatory oferty platformy Azure, aby oszacować inwestycje w chmurę. [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing) to jeden przykład.
- Niektórzy dostawcy chmury udostępniają również Kalkulatory różnic kosztów. [Kalkulator całkowitego kosztu posiadania (TCO) na platformie Azure](https://azure.com/tco) to jeden przykład.
- W przypadku bardziej dopracowanych struktur kosztów należy wziąć pod uwagę ćwiczenie [planowania cyfr cyfrowych](../digital-estate/index.md) .
- Oszacuj koszt migracji.
- Oszacuj koszt wszelkich oczekiwanych możliwości szkoleniowych. [Microsoft Learn](/learn) może pomóc w ograniczeniu kosztów.
- W niektórych firmach czas zainwestowany przez istniejących członków personelu może być uwzględniony w początkowych kosztach. Aby uzyskać wskazówki, skontaktuj się z biurem finansowym.
- Przedyskutuj wszelkie dodatkowe koszty lub koszty obciążeń z biurem finansowym na potrzeby weryfikacji.

## <a name="migration-specific-revenue-deltas"></a>Różnice przychodu specyficzne dla migracji

Ten aspekt jest często zaszukiwany przez strategie tworzące uzasadnienie biznesowe dla migracji. W niektórych obszarach Chmura może obciąć koszty. Jednak ostateczny cel dowolnego przekształcenia polega na uzyskaniu lepszych wyników w czasie. Weź pod uwagę efekty podrzędne, aby poznać ulepszenia długoterminowych przychodów. Jakie nowe technologie będą dostępne dla Twojej firmy po migracji, której nie można użyć dzisiaj? Jakie projekty i cele biznesowe są blokowane przez zależności od starszych technologii? Jakie programy są wstrzymane, oczekujące duże nakłady inwestycyjne na technologię?

Po rozważeniu możliwości odblokowanych przez chmurę należy współpracować z firmą, aby obliczyć wzrost przychodu, który mógłby pochodzić z tych możliwości.

## <a name="migration-specific-cost-deltas"></a>Różnice kosztów specyficzne dla migracji

Oblicz zmiany w kosztach, które będą pochodzić z proponowanej migracji. Zobacz artykuł [Modele finansowe](./financial-models.md) , aby uzyskać szczegółowe informacje o typach różnic kosztów. Dostawcy chmury często oferują narzędzia do obliczania różnic kosztów. [Kalkulator całkowitego kosztu posiadania (TCO) na platformie Azure](https://azure.com/tco) to jeden przykład.

Inne przykłady kosztów, które mogą zostać zredukowane przez migrację w chmurze:

- Zakończenie lub zmniejszenie centrum danych (koszty środowiska)
- Zmniejszenie zużycia zużywanej mocy (koszty środowiska)
- Zakończenie stojaka (fizyczne odzyskiwanie zasobów)
- Unikanie odświeżania sprzętu (unikanie kosztów)
- Unikanie odnawiania oprogramowania (zmniejszenie kosztów operacyjnych lub unikanie kosztów)
- Konsolidacja dostawcy (redukcja kosztów operacyjnych i potencjalne obniżenie kosztów)

## <a name="when-roi-results-are-surprising"></a>Gdy wyniki zwrotu z inwestycji są zaskakujące

Jeśli zwrot z inwestycji dla migracji w chmurze nie jest zgodny z oczekiwaniami, możesz chcieć ponownie odwiedzić typowe mitów wymienione na początku tego artykułu.

Należy jednak pamiętać, że oszczędności kosztów nie zawsze są możliwe. Niektóre aplikacje kosztowo nie działają w chmurze niż w środowisku lokalnym. Te aplikacje mogą znacząco pochylić wyniki w analizie.

Gdy zwrot z inwestycji jest niższy niż 20%, weź pod uwagę ćwiczenie związane z [planowaniem cyfr cyfrowych](../digital-estate/index.md) , zwracając szczególną uwagę na [racjonalizację](../digital-estate/rationalize.md). Podczas analizy ilościowej przejrzyj każdą aplikację, aby znaleźć obciążenia, które pochylić wyniki. Warto usunąć te obciążenia z planu. Jeśli dane użycia są dostępne, należy rozważyć zmniejszenie rozmiaru maszyn wirtualnych w celu dopasowania go do użycia.

Jeśli zwrot z inwestycji jest nadal nieprawidłowo wyrównany, poszukaj pomocy od przedstawiciela handlowego firmy Microsoft lub skontaktuj [się z doświadczonym partnerem](https://azure.microsoft.com/migration/support).

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Utwórz model finansowy dla transformacji w chmurze](./financial-models.md)