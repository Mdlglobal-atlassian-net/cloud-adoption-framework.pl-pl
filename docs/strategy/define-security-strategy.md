---
title: Definiowanie strategii zabezpieczeń
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak utworzyć uzasadnienie biznesowe migracji do chmury.
author: MarkSimos
ms.author: mas
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 36fa032ce989dedd393886e7154aa46e1c7e376b
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229927"
---
<!-- cSpell:ignore MarkSimos NIST CISO COVID -->

# <a name="define-a-security-strategy"></a>Definiowanie strategii zabezpieczeń

Ostateczne cele organizacji zabezpieczeń nie zmieniają się wraz z wdrażaniem usług w chmurze, ale w jaki sposób te cele zostaną zmienione. Zespoły zabezpieczeń muszą nadal skupić się na obniżeniu ryzyka biznesowego przed atakami i pracą w celu uzyskania poufności, integralności i gwarancji dostępności wbudowanych w wszystkie systemy informacyjne i dane.

## <a name="modernize-your-security-strategy"></a>Modernizacja strategii zabezpieczeń

Zespoły zabezpieczeń muszą przeprowadzić modernizację strategii, architektur i technologii, ponieważ organizacja przyjmuje chmurę i wykonuje ją w miarę upływu czasu. Podczas gdy rozmiar i liczba zmian mogą początkowo wydawać się zniechęcające, modernizacja programu zabezpieczeń umożliwia zachowanie pewnych obciążeń bolesnym związanych ze starszymi metodami. Organizacja może tymczasowo korzystać z starszej strategii i narzędzi, ale takie podejście jest trudne do utrzymania w tempie zmian w chmurze i środowisku zagrożeń:

- Zespoły ds. zabezpieczeń mogą pozostać bez podejmowania decyzji o przyjęciu w chmurze, jeśli przyjmują starsze sposób myślenia bezpieczeństwa "Długość broni", gdzie odpowiedź zawsze zaczyna się od "No" (zamiast współpracować z działem IT i zespołami biznesowymi w celu zmniejszenia ryzyka podczas włączania działalności biznesowej).
- Zespoły ds. zabezpieczeń będą mieć trudny czas na wykrywanie i obronność przed atakami w chmurze, jeśli używają tylko starszego narzędzia lokalnego i są przeznaczone wyłącznie do obwodu sieci Doctrine na wszystkie zabezpieczenia i monitorowanie. Ochrona w skali chmury umożliwia korzystanie z natywnych możliwości wykrywania i automatyzacji w chmurze oraz wprowadzenie obwodu tożsamości w celu ułatwienia monitorowania i ochrony zasobów w chmurze i urządzeniach przenośnych.

Ponieważ ta transformacja może być istotna, zalecamy zespołom ds. zabezpieczeń podejście Agile do modernizacji zabezpieczeń, które szybko modernizacj najbardziej krytyczne aspekty strategii, a następnie nieustannie ulepszają się po tym czasie.

### <a name="security-of-the-cloud-and-from-the-cloud"></a>Bezpieczeństwo chmury i chmury

Gdy organizacja przyjmuje usługi w chmurze, zespoły ds. zabezpieczeń będą działać na dwa główne cele:

- **Bezpieczeństwo \* \* chmury (Zabezpieczanie zasobów w chmurze):** zabezpieczenia należy zintegrować z planowaniem i działaniem usług w chmurze w celu zapewnienia spójnego stosowania tych podstawowych zabezpieczeń do wszystkich zasobów.
- **Zabezpieczenia \* z \* chmury (przy użyciu chmury do przekształcania zabezpieczeń):** zabezpieczenia należy od razu rozpocząć planowanie i zastanawiamy się, jak używać technologii chmurowych do modernizacji narzędzi i procesów zabezpieczeń, szczególnie natywnie zintegrowanych narzędzi zabezpieczeń. Więcej i więcej narzędzi zabezpieczeń jest hostowanych w chmurze i zapewnia możliwości trudne lub niemożliwe w środowisku lokalnym.

Wiele organizacji rozpoczyna od traktowania zasobów w chmurze jako dodatkowego _wirtualnego centrum_danych, co działa bardzo dobrze jako punkt wyjścia dla bezpieczeństwa chmury. W miarę modernizacji organizacji przy użyciu zabezpieczeń z chmury, większość z nich będzie szybko rozwijać ten model. Zabezpieczanie określonego oprogramowania centrum danych za pomocą narzędzi hostowanych w chmurze umożliwia korzystanie z możliwości wykraczających poza modele lokalne, które oferuje:

- Szybkie Włączanie i skalowanie funkcji zabezpieczeń.
- Wysoce efektywny spis zasobów i wykrywanie higieny konfiguracji zabezpieczeń.
- Ciągła ocena stan zabezpieczeń i kontroli w organizacji.
- Zdecydowanie udoskonalone wykrywanie zagrożeń, które wykorzystuje ogromne repozytoria analizy zagrożeń i praktycznie nieograniczone przetwarzanie/magazynowanie w chmurze.

### <a name="the-right-level-of-security-friction"></a>Właściwy poziom tarcia w zakresie zabezpieczeń

Bezpieczeństwo naturalnie tworzy tarcie, które spowalniają procesy, ma kluczowe znaczenie dla zidentyfikowania, które elementy są w dobrej kondycji w DevOps i procesach IT, a które nie są:

- W **dobrej kondycji:** Podobnie jak odporność w ćwiczeniu sprawia, że jest to mięśnie, integracja właściwego poziomu zabezpieczeń wzmacnia system lub aplikację, wymuszając sprawne znaczenie w odpowiednim czasie. Zwykle jest to rozwiązanie, w jaki sposób i jak osoba atakująca może próbować naruszyć bezpieczeństwo aplikacji lub systemu podczas projektowania oraz przeglądać, identyfikować i idealnym rozwiązaniem w przypadku, gdy atakujący może wykorzystać w kodzie oprogramowania, konfiguracjach lub praktykach operacyjnych.
- **Tarcie w złej kondycji:** Utrudnia większą wartość niż chroni. Często zdarza się to, gdy usterki zabezpieczeń wygenerowane przez narzędzia mają wysoką fałszywą dodatnią częstotliwość (na przykład fałszywe alarmy) lub kiedy problemy związane z zabezpieczeniami są znacznie przekraczające potencjalny wpływ ataku.

### <a name="standalone-and-integrated-responsibilities"></a>Autonomiczne i zintegrowane obowiązki

Zapewnienie poufności, integralności i zapewnienia dostępności wymaga, aby eksperci zabezpieczeń mogli korzystać z dedykowanych funkcji zabezpieczeń, a także ściśle współpracować z innymi zespołami w organizacji:

- **Unikatowe funkcje zabezpieczeń:** Zespoły ds. zabezpieczeń wykonują niezależne funkcje, które nie znajdują się w innym miejscu w organizacji, takie jak operacje zabezpieczeń, zarządzanie lukami w zabezpieczeniach i inne funkcje.
- **Integrowanie zabezpieczeń z innymi funkcjami:** Zespoły ds. zabezpieczeń pełnią również rolę ekspertów w zakresie innych zespołów i działających w organizacji, którzy tworzą inicjatywy biznesowe, oceniają ryzyko, projektują i opracowują aplikacje oraz obsługują systemy IT. Zespoły ds. zabezpieczeń poinformują te zespoły o doświadczeniu i kontekście ataków na ataki, metodach ataków i trendach, które mogą umożliwić nieautoryzowany dostęp, a także o opcjach zaradczych lub obejśćch oraz ich potencjalnych korzyściach lub pułapek. Ta funkcja zabezpieczeń jest podobna do jakości funkcji, ponieważ będzie ona tkana w wielu miejscach w dużej i małej obsłudze pojedynczego wyniku.

Wykonywanie tych obowiązków przy jednoczesnym zapewnieniu szybkiego tempa zmian w chmurze i transformacji firmy wymaga od zespołów ds. zabezpieczeń modernizacji narzędzi, technologii i procesów.

## <a name="transformations-mindsets-and-expectations"></a>Przekształcenia, mindsets i oczekiwania

Wiele organizacji zarządza łańcuchem wielu jednoczesnych transformacji w organizacji. Te wewnętrzne przekształcenia zwykle zaczynają się, ponieważ niemal wszystkie rynki zewnętrzne są przekształcane w celu spełnienia nowych preferencji klientów dotyczących technologii mobilnych i chmurowych. Organizacje często stoją na konkurencyjnym zagrożeniu nowych uruchomień i cyfrowej transformacji tradycyjnych konkurentów, którzy mogą zakłócać rynek.

![Łańcuch wielu jednoczesnych transformacji w organizacji](../_images/security/transformation-chain.png)

Proces transformacji wewnętrznej zazwyczaj obejmuje:

- **Cyfrowa transformacja** firmy w celu przechwytywania nowych szans i utrzymania konkurencyjności w odniesieniu do natywnych startów cyfrowych.
- **Przekształcanie technologii** organizacji informatycznej w celu wspierania inicjatywy z usługami w chmurze, nowoczesnymi praktykami programistycznymi i powiązanymi zmianami.
- **Przekształcanie zabezpieczeń** zarówno w celu adaptacji do chmury, jak i w coraz większym stopniu zaawansowanym środowisku zagrożeń.

### <a name="internal-conflict-can-be-costly"></a>Konflikt wewnętrzny może być kosztowny

Zmiana powoduje utworzenie obciążenia i konfliktu, co może spowodować podjęcie decyzji w celu zatrzymania. Jest to szczególnie ważne w przypadku zabezpieczeń, w przypadku których ryzyko związane z bezpieczeństwem jest często nieważne w ekspertach (zespoły ds. zabezpieczeń), a nie na właścicielu zasobów (właściciele firmy), którzy są odpowiedzialni za wyniki biznesowe i inne rodzaje ryzyka. Ta niewłaściwie umieszczona odpowiedzialność często zdarza się, ponieważ Wszyscy udziałowcy nieprawidłowo wyświetlają zabezpieczenia jako Rozwiązywanie problemów technicznych lub bezwzględnych, a nie dynamiczne, ciągłe ryzyko, takie jak Espionage korporacyjne i inne tradycyjne działania karne.

W tym czasie przekształcenie wszystkie zespoły muszą aktywnie współpracować w celu ograniczenia konfliktu, który może jednocześnie Derail kluczowe projekty i zespoły incentivize w celu obejścia ograniczenia ryzyka bezpieczeństwa. Internecine konfliktu między zespołami może skutkować:

- **Zwiększone ryzyko związane z bezpieczeństwem** , takie jak unikanie zdarzeń w zakresie zabezpieczeń lub zwiększenie szkód firmy przed atakami (zwłaszcza gdy zespoły uzyskują sfrustrowani przez zabezpieczenia i pomijają normalne procesy lub gdy nieaktualne podejścia zabezpieczeń są łatwo pomijane przez osoby atakujące).
- **Negatywny wpływ na działalność firmy lub misja** , na przykład gdy procesy biznesowe nie są odpowiednio włączone lub zaktualizowane, aby spełniały wymagania dotyczące rynku (często w przypadku procesów zabezpieczeń, które mają kluczowe inicjatywy biznesowe).

Niezwykle ważne jest, aby zachować świadomość kondycji relacji w ramach i między zespołami, aby pomóc im w przejściu do przesuwanej krajobrazu, która może pozostawać cennych członków zespołu niezabezpieczonych i nierozstrzygniętych. Ponowienie, empatię i edukacja na tych mindsetsach oraz pozytywny potencjał przyszłości ułatwią zespołowi nawigowanie po tym okresie, co zapewnia dobre wyniki bezpieczeństwa dla organizacji.

Liderzy mogą pomóc w wprowadzeniu zmian kulturowych z konkretnymi krokami aktywnymi, takimi jak:

- Publiczne modelowanie zachowań oczekiwanych przez zespoły.
- Jest przejrzysty na temat wyzwań związanych ze zmianami, w tym wyróżnianie własnych problemów do dostosowania.
- Regularnie przypominaj zespoły o pilności i ważności modernizacji i integracji zabezpieczeń.

### <a name="cybersecurity-resilience"></a>Odporność cyberbezpieczeństwa

Wiele klasycznych strategii zabezpieczeń koncentruje się wyłącznie na zapobieganiu atakom, które nie są wystarczające dla nowoczesnych zagrożeń. Zespoły zabezpieczeń muszą upewnić się, że ich strategia wykracza poza tę, a także umożliwia szybkie wykrywanie, reagowanie i odzyskiwanie ataków, aby zwiększyć odporność. Organizacje muszą założyć, że osoby atakujące spowodują naruszenie niektórych zasobów (nazywanych czasami "naruszeniem") i działają w celu zapewnienia, że zasoby i projekty techniczne są zrównoważone w zakresie zapobiegania atakom ataków i zarządzania atakami (zamiast standardowej metody domyślnego podejścia tylko do próby zapobiegania atakom).

Wiele organizacji już korzysta z tej drogi, ponieważ zarządzali stałym wzrostem ilości i złożoności ataków w ostatnich latach. Ta podróż często rozpoczyna się od pierwszego zdarzenia, które może być wydarzeniem emocjonalnej, w którym osoby tracą wcześniejszą usterkę i bezpieczeństwo. Chociaż nie jest to poważny w przypadku utraty życia, to zdarzenie może wyzwolić podobne emocji rozpoczynające się od odmowy i ostatecznie kończące się na akceptacji. Takie założenie "Niepowodzenie" może być trudne do zaakceptowania w pierwszej kolejności, ale ma silną zgodność z dobrze ustanowioną zasadą inżynierii "awaryjne", a założenie umożliwia zespołom skoncentrowanie się na lepszej definicji sukcesu: odporność.

Funkcje [struktury NIST cyberbezpieczeństwa](https://www.nist.gov/cyberframework) stanowią przydatny Przewodnik dotyczący zrównoważenia inwestycji między komplementarnymi działaniami umożliwiającymi identyfikację, ochronę, wykrywanie, reagowanie i odzyskiwanie w strategii odpornej na błędy.

Więcej informacji na temat odporności cyberbezpieczeństwa i ostateczne cele formantów cyberbezpieczeństwa zostały omówione w temacie [jak zachować ryzyko organizacji](https://docs.microsoft.com/azure/architecture/framework/security/resilience).

### <a name="how-the-cloud-is-changing-security"></a>Jak chmura zmienia zabezpieczenia

Przechodzenie do chmury w celu zapewnienia bezpieczeństwa jest większe niż w przypadku prostej zmiany technologicznej, to metoda zmiany generacji w technologii zbliżone na komputery stacjonarne i serwery korporacyjne. Pomyślnie przechodzenie tej zmiany wymaga podstawowych zmian w oczekiwaniach i sposób myślenia przez zespoły ds. zabezpieczeń. Przyjęcie odpowiednich mindsets i oczekiwania spowoduje zmniejszenie konfliktu w organizacji i zwiększenie skuteczności zespołów ds. zabezpieczeń.

Chociaż mogą one być częścią dowolnego planu modernizacji zabezpieczeń, szybkim tempem zmian w chmurze jest przyjęcie ich pilnego priorytetu.

- **Partnerstwo z udostępnionymi celami.** W tym wieku szybko podejmowanych decyzji i stałych ewolucji procesów zabezpieczenia nie mogą już przyjąć podejścia "Długość broni" w celu zatwierdzenia lub odrzucenia zmian w środowisku. Zespoły ds. zabezpieczeń muszą ściśle współpracować z firmowymi i zespołami INFORMATYCZNymi w celu ustalenia wspólnych celów dotyczących produktywności, niezawodności i zabezpieczeń oraz współdziałania z tymi partnerami w celu ich osiągnięcia.

  To partnerstwo stanowi ostateczną formę "przesunięcia w lewo" &mdash; zasady integracji zabezpieczeń wcześniej w procesach w celu łatwiejszego i skuteczniejszego rozwiązywania problemów z zabezpieczeniami. Wymaga to zmiany kultury przez wszystkie osoby, które są związane (z zabezpieczeniami, działalnością i IT), co wymaga każdego do poznania kultury i norm innych grup, jednocześnie jednocześnie uczą inne osoby.

  Zespoły zabezpieczeń muszą:

  - Zapoznaj się z **informacjami** biznesowymi i celami IT oraz o tym, dlaczego każdy z nich jest ważny, i jak zastanawiasz się, jak je przetwarzać.
  - **Udostępnianie** , dlaczego zabezpieczenia są ważne w kontekście tych celów i zagrożeń związanych z działalnością, jakie inne zespoły mogą wykonać w celu spełnienia celów związanych z bezpieczeństwem i ich działania.

  Chociaż nie jest to proste zadanie, niezbędne jest zapewnienie stałej ochrony organizacji i jej zasobów. Takie partnerstwo prawdopodobnie spowoduje, że w przypadku, gdy tylko minimalne cele dotyczące zabezpieczeń, działalności i niezawodności mogą być spełnione, ale przyrostowo ulepszane w miarę upływu czasu.

- **Bezpieczeństwo jest ciągłym ryzykiem, a nie problemem.** Nie można dokonać przestępczości "Rozwiąż". Na swoim rdzeńu bezpieczeństwo jest tylko dyscypliną zarządzania ryzykiem, która polega na skoncentrowaniu się na złośliwych działaniach, a nie na zdarzeniach naturalnych. Podobnie jak w przypadku wszystkich zagrożeń, nie jest to problem, który może zostać rozwiązany przez rozwiązanie, jest to połączenie prawdopodobieństwa i wpływu szkód z negatywnego zdarzenia na atak. Jest to najbardziej porównywalne z tradycyjnymi firmami Espionage i karnymi, w przypadku których organizacje mają motywację ataków na ludzi, którzy mają zachętę finansową do pomyślnego zaatakowania organizacji.

- **Sukces w zakresie produktywności lub zabezpieczeń wymaga obu tych opcji.** Organizacja musi skupić się na bezpieczeństwie i produktywności w dzisiejszych "innowacyjności" i stanie się nieistotnym środowisku. Jeśli organizacja nie jest wydajna i nie prowadzi nowych innowacji, może ona utracić konkurencyjność w portalu Marketplace, która powoduje nieprzerwanie finansowe lub ostatecznie niepowodzenie. Jeśli organizacja nie jest zabezpieczona i traci kontrolę nad zasobami w przypadku osób atakujących, może ona utracić swoją konkurencyjność w portalu Marketplace, która powoduje nieprzerwanie finansowe i ostatecznie kończy się niepowodzeniem.

- **Nikt nie jest idealny.** Żadna organizacja nie doskonale nadaje się do korzystania z chmury, a nie od firmy Microsoft. Zespoły IT i ds. zabezpieczeń firmy Microsoft grappleą wiele z tych samych wyzwań, które są używane przez naszych klientów, na przykład w celu polepszenia sposobu tworzenia struktur programów i zrównoważenia obsługi starszych programów z obsługą innowacji brzegowych, a nawet przerw w działaniu technologii w usługach w chmurze. Ponieważ te zespoły douczyją się, jak lepiej obsługiwać i zabezpieczyć chmurę, aktywnie udostępniają swoje doświadczenia z wykorzystaniem takich dokumentów jak te, a także z innymi osobami w [witrynie pokazu IT](https://www.microsoft.com/itshowcase), ale stale dostarczając opinię naszym zespołom inżynieryjnym i dostawcom innych firm, aby usprawnić ich oferty.

  W oparciu o nasze środowisko zalecamy, aby zespoły były utrzymywane w standardzie ciągłego uczenia się i ulepszania, a nie w standardzie doskonałej jakości.

- **Okazja do przekształcenia.** Ważne jest, aby wyświetlać transformację cyfrową jako pozytywną okazję do zabezpieczeń. Chociaż łatwo jest zobaczyć potencjalne downsides i ryzyko tej zmiany, można łatwo pominąć ogromną okazję do oddzielenia roli zabezpieczeń i zdobycia stanowiska w tabeli, w której podejmowane są decyzje. Współdziałanie z firmą może skutkować zwiększeniem poziomu zabezpieczeń, ograniczyć wastefulie powtarzające się działania i zwiększyć bezpieczeństwo, ponieważ będą one bardziej połączone z misjami organizacji.

## <a name="adopting-the-shared-responsibility-model"></a>Przyjęcie współużytkowanego modelu odpowiedzialności

Hosting usług IT w chmurze polega na rozdzieleniu obowiązków operacyjnych i bezpieczeństwa związanych z obciążeniami między dostawcą chmury a dzierżawcą klienta. Wszystkie zespoły zabezpieczeń muszą analizować i zrozumieć ten współużytkowany model odpowiedzialności, aby dostosować ich procesy, narzędzia i zestawy umiejętności do nowego świata. Pomoże to uniknąć nieumyślnego tworzenia luk lub nakładania się na stan zabezpieczeń, co skutkuje ryzykiem związanym z bezpieczeństwem lub zasobami.

Na tym diagramie przedstawiono sposób dystrybucji obowiązków związanych z zabezpieczeniami między dostawcami chmury i organizacjami klientów w chmurze w niezawodnym partnerstwie:

![Współdzielone obowiązki zabezpieczeń](../_images/security/security-responsibilities.png)

Ponieważ istnieją różne modele usług w chmurze, obowiązki dla każdego obciążenia różnią się w zależności od tego, czy jest ono hostowane w oprogramowaniu jako usługa (SaaS), platforma jako usługa (PaaS), infrastruktura jako usługa (IaaS), czy w lokalnym centrum danych.

## <a name="building-security-initiatives"></a>Tworzenie inicjatyw dotyczących zabezpieczeń

Ten diagram ilustruje trzy podstawowe inicjatywy bezpieczeństwa, które powinny być stosowane w przypadku większości programów zabezpieczeń, aby dostosować ich strategię zabezpieczeń i cele programu zabezpieczającego dla chmury:

![Podstawowe inicjatywy bezpieczeństwa](../_images/security/primary-security-initiatives.png)

Tworzenie odpornych stan zabezpieczeń w chmurze wymaga kilku równoległych metod uzupełniających:

- **Zaufanie, ale weryfikacja:** W przypadku obowiązków wykonywanych przez dostawcę chmury organizacje powinny przyjmować podejście "zaufanie, ale sprawdzenie". Organizacje powinny oszacować praktyki bezpieczeństwa swoich dostawców chmury i kontroli bezpieczeństwa oferowanych przez nich w celu zapewnienia, że dostawca chmury spełnia wymagania w zakresie bezpieczeństwa organizacji.

- **Modernizacja infrastruktury i zabezpieczeń aplikacji:** Dla elementów technicznych w obszarze kontroli organizacji należy określić priorytety modernizacji narzędzi zabezpieczających i skojarzyć zestawy umiejętności, aby zminimalizować luki w zabezpieczeniach w chmurze. Składa się to z dwóch różnych uzupełniających się działań:

  - **Zabezpieczenia infrastruktury:** Organizacje powinny korzystać z chmury w celu modernizacji podejścia do ochrony i monitorowania typowych składników używanych przez wiele aplikacji, takich jak systemy operacyjne, sieci, systemy operacyjne i infrastruktura kontenerów. Te możliwości chmury często obejmują zarządzanie składnikami infrastruktury w środowiskach IaaS i lokalnych. Optymalizacja tej strategii jest ważna, ponieważ ta infrastruktura jest zależna od aplikacji i danych, które są w nim uruchomione, co często pozwala na krytyczne procesy biznesowe i przechowywanie krytycznych danych firmowych.
  - **Zabezpieczenia aplikacji:** Organizacje powinny również modernizowane sposób zabezpieczania unikatowych aplikacji i technologii opracowanych przez program lub w organizacji. Ta dyscyplina zmienia się szybko wraz z wdrażaniem procesów DevOps Agile, zwiększeniem użycia składników typu open source oraz wprowadzeniem interfejsów API chmury i usług w chmurze w celu zastąpienia składników aplikacji lub aplikacji programu InterConnect.

    Uzyskanie tego prawa ma kluczowe znaczenie, ponieważ te aplikacje często umożliwiają krytyczne procesy biznesowe i przechowują krytyczne dane biznesowe.

  - **Nowoczesny obwód:** Organizacje powinny mieć kompleksowe podejście do ochrony danych w ramach wszystkich obciążeń, organizacje powinny stworzyć nowoczesne strefy spójnych, centralnie zarządzanych kontroli tożsamości, aby chronić swoje dane, urządzenia i konta. Jest to wysoce wpływ na strategię o zerowej relacji zaufania szczegółowo omówioną w module 3 warsztatu CISO i więcej zasobów.

### <a name="security-and-trust"></a>Zabezpieczenia i zaufanie

Należy zauważyć, że użycie słowa "Ufaj" w zabezpieczeniach może być mylące. Ta dokumentacja odnosi się do niej na dwa sposoby ilustrujące przydatne zastosowania tej koncepcji:

- [Zerowe zaufanie](https://www.microsoft.com/security/business/zero-trust) to typowy termin branżowy dla strategicznego podejścia do zabezpieczeń, który zakłada, że sieć firmowa lub intranetowa jest nieszkodliwa (zaufanego "zero Trust") i odpowiednio zaprojektuje zabezpieczenia.
- [Relacja zaufania, ale weryfikacja](https://en.wikipedia.org/wiki/trust,_but_verify) jest wyrażeniem, które przechwytuje istotę dwóch różnych organizacji współpracujących ze sobą w kierunku wspólnego celu, mimo że niektóre inne potencjalnie rozbieżne zainteresowania. To zwięzłe przechwycenie wielu wszystkie szczegóły wczesnych etapów partnera z komercyjnym dostawcą chmury dla organizacji.

Dostawca usług w chmurze i ich praktyki i procesy mogą być odpowiedzialne za spełnienie wymagań umownych i prawnych oraz mogą uzyskać lub utracić zaufanie. Sieć jest niedziałającym połączeniem, które nie może być podatne na ataki, jeśli są używane przez osoby atakujące (podobnie jak w przypadku osób, które nie mogą korzystać z podróży służbowych).

## <a name="how-cloud-is-changing-security-relationships-and-responsibilities"></a>Jak chmura zmienia relacje zabezpieczeń i obowiązki

Podobnie jak w przypadku poprzednich przejść do nowej generacji technologii, takich jak komputer stacjonarny i serwer korporacyjny, przechodzenia do chmury obliczeniowej zakłócają długotrwałe relacje, role, obowiązki i zestawy umiejętności. Opisy zadań, które zostały ponoszone do ponad ostatnich dekad, nie są czyste do firmy, która teraz zawiera możliwości chmury. Gdy branża wspólnie pracuje nad normalizacją nowego modelu, organizacje będą musieli skupić się na tym, jak to możliwe, aby ułatwić zarządzanie niedokładnością niejednoznaczności w tym okresie.

Zespoły zabezpieczeń wpływają na te zmiany w biznesie i technologii, które wspierają, a także własne działania związane z modernizacją w celu lepszego ukierunkowania aktorów. Osoby atakujące aktywnie rozwijają się w celu ciągłego przeszukiwania najłatwiejszych luk w zabezpieczeniach, takich jak ludzie, proces i technologia firmy, a zabezpieczenia muszą opracowywać możliwości i umiejętności umożliwiające rozwiązanie tych kątów.

W tej sekcji opisano najważniejsze relacje, które często zmieniają się w trakcie podróży do chmury, w tym lekcje zdobyte w przypadku minimalizowania ryzyka i uwzględniania możliwości ulepszania:

- **Między bezpieczeństwem a uczestnikami biznesowymi:** Liderzy zabezpieczeń muszą coraz bardziej zwiększyć partnera, aby umożliwić organizacjom zredukowanie ryzyka. Liderzy zabezpieczeń powinni wspierać decyzje biznesowe jako ekspert (msp) i powinni dążyć do wzrostu zaufanych doradców do tych liderów firmy. Ta relacja pomaga zagwarantować, że liderzy biznesowi uwzględnią zagrożenia dla bezpieczeństwa podczas podejmowania decyzji firmy, informują o bezpieczeństwie priorytetów firmy i pomagają zapewnić, że inwestycje w zabezpieczenia są odpowiednio priorytetowe wraz z innymi inwestycjami.

- **Między liderem zabezpieczeń i członkami zespołu:** Lider powinien pobrać te informacje z lidera firmy z powrotem do swoich zespołów, aby poprowadzić swoje priorytety inwestycyjne.

  Poprzez ustawienie tonu współpracy z liderami biznesowymi i ich zespołami, a nie z klasyczną "długością broni", liderzy zabezpieczeń mogą uniknąć adversarial dynamicznego, który przeszkadza w realizacji celów związanych z bezpieczeństwem i produktywnością.

  Liderzy zabezpieczeń powinni dążyć do zapewnienia użytkownikom przejrzystości w zakresie zarządzania swoimi codziennymi decyzjami dotyczącymi wydajności i kompromisów związanych z bezpieczeństwem, ponieważ mogą one być nowe w wielu zespołach.

- **Między zespołami aplikacji i infrastruktury (i dostawcami chmury):** Ta relacja polega na znaczących zmianach ze względu na wiele trendów w branży IT i bezpieczeństwa, które mają na celu zwiększenie wydajności innowacji i produktywności dla deweloperów.

  Stare normy i funkcje organizacyjne zostały zakłócone, ale nadal pojawiają się nowe normy i funkcje, dlatego zalecamy zaakceptowanie niejednoznaczności, aktualność i eksperymentowanie z działaniami w organizacji do momentu jego wykonania. Firma Microsoft nie zaleca stosowania podejścia "czekaj i zobacz" w tym miejscu, ponieważ może to spowodować, że Twoja organizacja będzie mieć istotną konkurencyjną wadą.

  Trendy te są trudne dla tradycyjnych norm dotyczących ról i relacji między aplikacjami i infrastrukturą:

  - **DevOps — odmowa dyscyplin:** W swoim idealnym stanie to efektywnie tworzy pojedynczy, wysoce funkcjonalny zespół, który łączy oba zestawy wiedzy z zagadnieniami, aby szybko wprowadzać innowacje, aktualizować aktualizacje i rozwiązywać problemy (zabezpieczenia i inne). Chociaż ten idealny stan zajmie trochę czasu, a obowiązki w środku nadal będą bardzo niejednoznaczne, organizacje już wykorzystaniu pewne korzyści wynikające z szybkiego wydania z powodu tego podejścia do współpracy. Firma Microsoft zaleca integrację zabezpieczeń z tym cyklem, aby ułatwić naukę tych kultur, udostępnianie informacji o zabezpieczeniach i współdziałanie ze wspólnym celem szybkiego uwalniania bezpiecznych i niezawodnych aplikacji.

  ![DevOps — odmowa dyscyplin](../_images/security/devops-disciplines.png)

  - **Kontenerach staje się wspólnym składnikiem infrastruktury:** Aplikacje są coraz bardziej hostowane i zorganizowane według technologii, takich jak Docker, Kubernetes i podobne technologie. Technologie te upraszczają programowanie i wydawanie przez abstrakcję wielu elementów instalacji i konfiguracji bazowego systemu operacyjnego.

  ![Infrastruktura kontenerach](../_images/security/containerization.png)

  Kontenery rozpoczęte jako technologia projektowania aplikacji zarządzane przez zespoły programistyczne stają się powszechnym składnikiem infrastruktury, który jest coraz bardziej przenoszony do zespołów infrastruktury. To przejście jest nadal w toku w wielu organizacjach, ale jest to naturalny i pozytywny kierunek, w jakim można najlepiej rozwiązać problemy z tradycyjnymi zestawami umiejętności infrastruktury, takimi jak sieć, magazyn i zarządzanie pojemnością.

  Zespoły infrastruktury i członkowie zespołu ds. zabezpieczeń powinni mieć zapewnione szkolenia, procesy i narzędzia ułatwiające zarządzanie, monitorowanie i zabezpieczanie tej technologii.

  - **Usługi bezserwerowe i aplikacje w chmurze:** Jedną z tendencji dominującej w branży jest teraz skrócenie czasu i pracy programistycznej wymaganej do kompilowania lub aktualizowania aplikacji.

    ![Usługi bezserwerowe i aplikacje w chmurze](../_images/security/serverless-model.png)

    Deweloperzy są również coraz bardziej korzystający z usług w chmurze, aby:

    - Uruchamiaj kod zamiast aplikacji hostingowych na maszynach wirtualnych i serwerach.
    - Udostępniaj funkcje aplikacji zamiast opracowywania własnych składników. Doprowadziło to do modelu _bezserwerowego_ , który korzysta z istniejących usług w chmurze dla typowych funkcji. Liczba i różnorodność usług Cloud Services (i ich tempo innowacji) również przekroczyła zdolność zespołów zabezpieczeń do analizowania i zatwierdzania użycia tych usług, pozostawiając im wybór między zezwoleniem deweloperom na korzystanie z dowolnej usługi, próbując zapobiec używaniu przez zespoły deweloperów niezatwierdzonych usług lub próbować znaleźć lepszy sposób.
    - **Aplikacje bezkodowe i aplikacje zaawansowane:** Kolejną tendencją jest użycie technologii bezkodowych, takich jak Microsoft PowerShell Apps. Ta technologia umożliwia osobom bez znajomości programowania Tworzenie aplikacji, które osiągają wyniki biznesowe. Ze względu na to, że niska intensywność i wysoka wartość, ten trend może szybko wzrosnąć popularność, a specjaliści ds. bezpieczeństwa mogą szybko zrozumieć swoje konsekwencje. Działania dotyczące zabezpieczeń powinny być skoncentrowane na obszarach, w których człowiek może wprowadzić błąd w aplikacji, a mianowicie o projekcie aplikacji i uprawnień zasobów za pośrednictwem modelowania zagrożeń składników aplikacji, interakcji/relacji i uprawnień roli.

- **Między deweloperami i autorami składników Open Source:** Deweloperzy mogą również zwiększyć wydajność dzięki użyciu składników i bibliotek typu open source zamiast opracowywania własnych składników. Pozwala to zwiększyć wydajność, ale również stwarza zagrożenie bezpieczeństwa przez utworzenie zależności zewnętrznej i wymaganie prawidłowego zachowania i poprawki tych składników. Deweloperzy efektywnie zakładają ryzyko związane z bezpieczeństwem i innymi usterkami, gdy korzystają z tych składników i muszą upewnić się, że plan ogranicza te działania w tych samych standardach jak kod, który opracuje.

- **Między aplikacjami i danymi:** Linia między bezpieczeństwem danych i aplikacji staje się rozmyciem i nowe regulacje tworzą potrzebę bliższej współpracy między zespołami danych/ds. ochrony prywatności i zespołami ds. zabezpieczeń:

  - Algorytmy uczenia maszynowego **(Machine Learning):** algorytmy uczenia maszynowego są podobne do aplikacji, które są przeznaczone do przetwarzania danych w celu utworzenia wyniku. Kluczowe różnice są następujące:

    - **Uczenie maszynowe o wysokiej wartości:** Uczenie maszynowe często przyznaje znaczącą przewagę konkurencyjną i często uznaje się za poufne własności intelektualne oraz tajemnicę handlową.

    - **Nadruk czułości:** Nadzorowane Uczenie maszynowe jest dostrojone przy użyciu zestawów danych, które wydrukowały charakterystykę DataSet w algorytmie. W związku z tym algorytm dostrojony może być traktowany jako poufny ze względu na zestaw danych używany do uczenia go. Na przykład szkolenie algorytmu uczenia maszynowego w celu znalezienia zasad tajnych armii na mapie przy użyciu zestawu danych z tajnych zasad armii spowoduje, że będzie to poufny element zawartości.

    > [!NOTE]
    > Nie wszystkie przykłady są oczywiste, więc niezwykle ważne jest, aby przenieść zespół wspólnie z właściwymi udziałowcami z zespołów nauki o danych, zainteresowanych podmiotów, zespołów ds. zabezpieczeń, zespołów ochrony prywatności i innych. Zespoły te powinny być odpowiedzialne za spełnienie typowych celów innowacji i odpowiedzialności. Powinny one rozwiązywać typowe problemy, takie jak sposób i miejsce przechowywania kopii danych w niezabezpieczonych konfiguracjach, sposób klasyfikowania algorytmów, a także wszelkie problemy związane z organizacjami.
    >
    > Firma Microsoft opublikowała nasze [zasady odpowiedzialne za AI](https://www.microsoft.com/ai/responsible-ai) , aby poprowadzić własne zespoły i naszych klientów.

    - **Własność i prywatność danych:** Takie jak Rodo zwiększają widoczność problemów z danymi i aplikacji. Zespoły aplikacji mogą teraz kontrolować, chronić i śledzić poufne dane na poziomie porównywalnym ze śledzeniem danych finansowych według banków i instytucji finansowych. Właściciele danych i zespoły aplikacji muszą kompilować bogate informacje o tym, które aplikacje danych są przechowywane i jakie są wymagane formanty.

- **Między organizacjami i dostawcami chmury:** Jako organizacje obsługujące obciążenia w chmurze są wprowadzane do relacji biznesowej z każdym z tych dostawców chmury. Korzystanie z usług w chmurze często zapewnia wartość biznesową, taką jak:

  - Przyspieszenie **inicjatyw transformacji cyfrowej** przez skrócenie czasu wprowadzenia na rynek nowych funkcji.

  - **Zwiększając wartość działań informatycznych i zabezpieczeń** , zwalniając zespoły do skoncentrowania się na wyższych wartościach (wyrównanych do działalności), a nie na niższych zadaniach podstawowych, które są bardziej wydajne przez usługi w chmurze w ich imieniu.

  - **Zwiększona niezawodność i czas odpowiedzi:** Większość nowoczesnych chmur ma także wyjątkowo wysoki czas pracy w porównaniu z tradycyjnymi lokalnymi centrami danych i pokazuje, że mogą szybko skalować (na przykład w trakcie COVID-19 Pandemic) i zapewniać odporność po zdarzeniach naturalnych, takich jak pioruny

    W przypadku wyjątkowo korzystnej zmiany w chmurze nie są jeszcze ryzykowne. Ponieważ organizacje przyjmują usługi w chmurze, powinny rozważyć potencjalne obszary ryzyka, w tym:

  - **Ciągłość działania i odzyskiwanie po awarii:** Czy dostawca usług w chmurze jest finansowo objęty modelem biznesowym, który prawdopodobnie przejdzie i poprawi się w trakcie korzystania z usługi przez organizację? Czy dostawca chmury wprowadził przepisy pozwalające zapewnić ciągłość klienta w przypadku, gdy dostawca napotyka błąd finansowy lub inny, na przykład dostarczając kod źródłowy do klientów lub otwierając go?

    Aby uzyskać więcej informacji i dokumentów dotyczących kondycji finansowej firmy Microsoft, zobacz [relacje dla inwestorów firmy Microsoft](https://www.microsoft.com/investor).

  - **Zabezpieczenia:** Czy dostawca chmury postępuje zgodnie z najlepszymi rozwiązaniami dotyczącymi zabezpieczeń? Czy zostało to zweryfikowane przez niezależne organy regulacyjne?

    - Usługa [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/risk-score) umożliwia odnajdywanie użycia ponad 16 000 aplikacji w chmurze, które są pozycjonowane i oceniane w oparciu o więcej niż 70 czynniki ryzyka, aby zapewnić ciągły wgląd w użycie chmury, obserwowanie go oraz ryzyko związane z programowaniem w organizacji.
    - [Portal zaufania usługi firmy Microsoft](https://servicetrust.microsoft.com) udostępnia certyfikaty zgodności z przepisami, raporty inspekcji, testy pióra i są dostępne dla klientów. Te dokumenty obejmują wiele szczegółów wewnętrznych rozwiązań z zakresu zabezpieczeń (zwłaszcza raport SOC 2 typu 2 i FedRAMP umiarkowany plan zabezpieczeń systemu).

  - **Konkurent firmy:** Czy dostawca chmury ma znaczącą konkurencję biznesową w branży? Czy masz wystarczającą ochronę w ramach kontraktu usług w chmurze lub innych środków, aby chronić swoją firmę przed potencjalnie szkodliwymi działaniami?

    Zapoznaj się z [tym artykułem](https://www.cnbc.com/2019/03/16/why-volkswagen-chose-microsoft-azure-over-aws.html) , aby uzyskać komentarz dotyczący sposobu, w jaki firma Microsoft unika konkurowania z klientami w chmurze.

  - **Wielochmurowe:** Wiele organizacji ma de facto lub celową strategię wielochmurową. Może to być celowy cel, aby ograniczyć zależność od pojedynczego dostawcy lub uzyskać dostęp do unikatowych najlepszych rozwiązań w zakresie rasy, ale może się również zdarzyć, że deweloperzy wybierają preferowane lub znane usługi w chmurze lub że organizacja nabyła inną firmę. Bez względu na to, Strategia ta może wprowadzać potencjalne zagrożenia i koszty, które muszą być zarządzane, w tym:

    - **Przestój z wielu zależności:** Systemy zaprojektowane w celu wykorzystania wielu chmur są narażone na większą liczbę źródeł ryzyka, ponieważ zakłócenia w dostawcach chmury (lub ich użycie przez zespół) może spowodować przestoje i zakłócenia Twojej firmy. Ta zwiększona złożoność systemu zwiększa również prawdopodobieństwo zakłócenia zdarzeń, ponieważ członkowie zespołu mogą w pełni zrozumieć bardziej skomplikowany system.
    - **Negocjowanie potęgi:** W przypadku większych organizacji należy wziąć pod uwagę, czy jedna chmura (wzajemne zobowiązanie/partnerstwo) czy strategia wielochmurowa (możliwość zmiany firmy) będzie miała większy wpływ na dostawców chmury w celu uzyskania priorytetów.
    - **Zwiększone obciążenie związane z konserwacją:** Zasoby IT i zabezpieczeń są już nadmiernie nakładane na podstawie istniejących obciążeń i zachowują zmiany z jednej platformy w chmurze. Każda dodatkowa platforma jeszcze bardziej zwiększa te obciążenie i przejmuje członków zespołu przed działaniami wyższymi, takimi jak usprawnienie procesu technicznego w celu przyspieszenia innowacji w biznesie, konsultowania się z grupami biznesowymi w celu skuteczniejszego korzystania z technologii itd.
    - **Personel i szkolenia:** Organizacje często nie uwzględniają wymagań związanych z personelem, które są niezbędne do obsługi wielu platform i szkolenia wymaganego do obsługi wiedzy i waluty nowych funkcji, które są publikowane w szybkim tempie.
