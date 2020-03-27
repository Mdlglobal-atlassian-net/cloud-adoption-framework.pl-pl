---
title: 'Złożone funkcje nadzoru korporacyjnego: ulepszanie dyscypliny linii bazowej zabezpieczeń'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak dodać kontrolki zabezpieczeń obsługujące przeniesienie chronionych danych do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: de9fd12afe7445c5cdd3b4ae8c1eba9c7cb07f19
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80357069"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-security-baseline-discipline"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: ulepszanie dyscypliny linii bazowej zabezpieczeń

W tym artykule zawarto opisy, dodając formanty zabezpieczeń, które obsługują przeniesienie chronionych danych do chmury.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

CIO pozostały w miesiącach, współpracując ze współpracownikami i pracownikami prawnymi firmy. Konsultant ds. zarządzania z doświadczeniem w cyberbezpieczeństwa został zaangażowany, aby pomóc istniejącym zabezpieczeniom IT i zespołom zarządzającym IT nowym zasadom dotyczącym chronionych danych. Grupa była w stanie wspierać obsługę tablicy w celu zastąpienia istniejących zasad, co pozwala na hostowanie poufnych danych osobowych i finansowych przez zatwierdzonych dostawców chmury. Wymaga to przyjęcia zestawu wymagań dotyczących zabezpieczeń i procesu ładu w celu zweryfikowania i udokumentowania zgodności z tymi zasadami.

W ciągu ostatnich 12 miesięcy zespoły wdrażania chmury wyczyścili większość zasobów 5 000 z dwóch centrów danych, które zostaną wycofane. 350 niezgodnych zasobów zostało przeniesionych do alternatywnego centrum danych. Pozostaną tylko maszyny wirtualne 1 250 zawierające chronione dane.

### <a name="changes-in-the-cloud-governance-team"></a>Zmiany w zespole ładu w chmurze

Zespół ds. zarządzania chmurą nadal zmienia się wraz z opisami. Dwie osoby z członkami zespołu znajdują się teraz wśród najbardziej zakrytych architektów w chmurze w firmie. Zbiór skryptów konfiguracyjnych został wyhodowany jako nowe zespoły z myślą o innowacyjnych nowych wdrożeniach. Zespół nadzorujący chmury również wzrosnął. Ostatnio członkowie zespołu ds. operacji IT przyłączyły działania zespołu ładu w chmurze w celu przygotowania do operacji w chmurze. Architektzy chmury, którzy pomogą sprzyjać tej społeczności, są postrzegani jako opiekunowie chmury i akceleratory chmury.

Różnica jest delikatna, dlatego jest ważnym rozróżnieniem podczas kompilowania kultury IT ukierunkowanej na zarządzanie. Powiernik w chmurze czyści messesy opracowane przez innowacyjne architektów w chmurze, a dwie role mają naturalne tarcie i sprzeciwianie się. Ochrona w chmurze pomaga zapewnić bezpieczną pracę w chmurze, dzięki czemu inne architektzy w chmurze mogą szybko przełączać się do mniejszej liczby Messes. Akcelerator w chmurze wykonuje obie funkcje, ale również jest uwzględniany w tworzeniu szablonów w celu przyspieszenia wdrożenia i przyjęcia, stając się akceleratorem innowacji oraz z pięciu dyscyplin nadzoru chmurowego.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

W poprzedniej fazie tego przykładu firma rozpoczęła proces wycofywania dwóch centrów danych. Ten ciągły nakład pracy obejmuje Migrowanie niektórych aplikacji ze starszymi wymaganiami dotyczącymi uwierzytelniania, które wymagają ulepszeń przyrostowych dla linii bazowej tożsamości, opisanych w [poprzednim artykule](./identity-baseline-improvement.md).

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- Tysiące zasobów IT i firm zostały wdrożone w chmurze.
- Zespół programistyczny aplikacji wdrożył potok ciągłej integracji i ciągłego wdrażania (CI/CD) w celu wdrożenia aplikacji natywnej w chmurze z ulepszonym środowiskiem użytkownika. Ta aplikacja nie współdziała jeszcze z chronionymi danymi, więc nie jest gotowa do produkcji.
- Zespół ds. analizy biznesowej aktywnie nadzoruje dane w chmurze na podstawie danych logistycznych, spisu i innych firm. Te dane są używane do kierowania nowych prognoz, które mogą kształtować procesy biznesowe. Jednak te przewidywania i szczegółowe informacje nie są funkcjonalne, dopóki dane klienta i finansowe nie będą mogły zostać zintegrowane z platformą danych.
- Zespół IT wprowadza postępy w planach CIO i DYREKTORów, aby wycofać dwa centra danych. Prawie 3 500 zasobów w dwóch centrach danych zostało wycofane lub zmigrowane.
- Zasady dotyczące poufnych danych osobistych i finansowych zostały zmodernizowane. Jednak nowe zasady firmowe są zależne od implementacji związanych z nimi zasad zabezpieczeń i zarządzania. Zespoły nadal są wstrzymane.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

- Wczesne eksperymenty związane z projektowaniem aplikacji i zespołami analizy biznesowej pokazują potencjalne udoskonalenia dotyczące doświadczeń klientów i decyzji opartych na danych. Obydwie zespoły chce rozszerzyć przyjęcie chmury w ciągu następnych 18 miesięcy przez wdrożenie tych rozwiązań w środowisku produkcyjnym.
- Opracowano uzasadnienie biznesowe dotyczące migrowania pięciu centrów danych na platformę Azure, co dodatkowo zmniejszy koszty IT i zapewni większą elastyczność biznesową. W przypadku mniejszej skali wycofanie tych centrów danych jest oczekiwane w celu podwójnego zmniejszenia kosztów.
- Budżety wydatków inwestycyjnych i wydatków operacyjnych są zatwierdzone do wdrożenia wymaganych zasad zabezpieczeń i zarządzania, narzędzi i procesów. Oczekiwane oszczędności kosztów wynikające z wycofania centrum danych są zbyt małe, aby można było płacić za tę nową inicjatywę. Liderzy i działalność biznesowa mają pewność, że inwestycja przyspiesza realizację postanowień w innych obszarach. Zespół ds. zarządzania chmurą Grassroots stał się uznanym zespołem z dedykowanym liderem i personelem.
- Zbiorowo zespoły wdrażania chmury, zespół ds. zarządzania chmurą, zespół zabezpieczeń IT i zespół nadzoru IT zaimplementują wymagania dotyczące bezpieczeństwa i zarządzania, aby umożliwić zespołom wdrażania chmury Migrowanie chronionych danych do chmury.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Naruszenie danych:** Istnieje związek związany z naruszeniami danych podczas wdrażania nowej platformy danych. Technicy stosujące technologie chmury wzrosły do wdrożenia rozwiązań, które mogą obniżyć to ryzyko. Należy wdrożyć niezawodną strategię zabezpieczeń i nadzoru, aby upewnić się, że technicy te spełniają te obowiązki.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

1. Aplikacje o krytycznym znaczeniu lub chronione dane mogą zostać przypadkowo wdrożone.
2. Chronione dane mogą zostać ujawnione podczas przechowywania ze względu na słabe decyzje dotyczące szyfrowania.
3. Nieautoryzowani użytkownicy mogą uzyskać dostęp do chronionych danych.
4. Zewnętrzna wtargnięcie może spowodować dostęp do chronionych danych.
5. Zewnętrzna wtargnięcie lub ataki typu "odmowa usługi" mogą spowodować przerwanie działania biznesowego.
6. Zmiany w organizacji lub zatrudnianiu mogą pozwolić na nieautoryzowany dostęp do chronionych danych.
7. Nowe programy wykorzystujące luki w zabezpieczeniach mogą tworzyć szanse dla włamania lub nieautoryzowanego dostępu.
8. Niespójne procesy wdrażania mogą powodować luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
9. Nałożenia konfiguracyjne lub pominięte poprawki mogą spowodować niezamierzone luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
10. Różne urządzenia brzegowe mogą zwiększyć koszty operacji sieciowych.
11. Różne konfiguracje urządzeń mogą prowadzić do wglądu w konfigurację i naruszają zabezpieczenia.
12. Zespół Cyberbezpieczeństway stwarza ryzyko od wygenerowania kluczy szyfrowania na platformie jednego dostawcy chmury. Chociaż to zgłoszenie jest nieuzasadnione, zostało zaakceptowane przez zespół w czasie.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika. Na liście jest wyświetlana wartość Long, ale wdrażanie tych zasad może być prostsze.

1. Wszystkie wdrożone zasoby muszą być pogrupowane według stopnia ważności i klasyfikacji danych. Klasyfikacje muszą być przeglądane przez zespół ładu chmury i aplikację przed wdrożeniem w chmurze.
2. Aplikacje, które przechowują lub uzyskują dostęp do chronionych danych, są zarządzane inaczej niż te, które nie są. Należy je podzielić na mniejsze, aby uniknąć niezamierzonego dostępu do chronionych danych.
3. Wszystkie chronione dane muszą być szyfrowane, gdy są przechowywane.
4. Uprawnienia podwyższonego poziomu w dowolnym segmencie zawierającym chronione dane powinny być wyjątkiem. Wszelkie takie wyjątki będą rejestrowane w zespole ładu chmur i regularnie poddawane inspekcji.
5. Podsieci sieciowe zawierające chronione dane muszą być odizolowane od innych podsieci. Ruch sieciowy między podsieciami chronionych danych zostanie regularnie poddany inspekcji.
6. Nie można bezpośrednio uzyskać dostępu do podsieci zawierającej chronione dane za pośrednictwem publicznego Internetu lub między centrami danych. Dostęp do tych podsieci musi być kierowany za pośrednictwem podsieci pośrednich. Cały dostęp do tych podsieci musi następować przez rozwiązanie zapory, które może wykonywać funkcje skanowania pakietów i blokowania.
7. Narzędzia ładu muszą przeprowadzać inspekcję i wymuszać wymagania dotyczące konfiguracji sieci zdefiniowane przez zespół zarządzania zabezpieczeniami.
8. Narzędzia ładu muszą ograniczać wdrożenie maszyny wirtualnej tylko do zatwierdzonych obrazów.
9. Zawsze, gdy jest to możliwe, zarządzanie konfiguracją węzła powinna stosować wymagania dotyczące zasad do konfiguracji dowolnego systemu operacyjnego gościa. Zarządzanie konfiguracją węzła powinno uwzględniać istniejące inwestycje w zasady grupy obiekcie (GPO) dla konfiguracji zasobów.
10. Narzędzia ładu będą przeprowadzać inspekcję, czy aktualizacje automatyczne są włączone dla wszystkich wdrożonych zasobów. Gdy jest to możliwe, zostaną wymuszone aktualizacje automatyczne. Gdy nie są wymuszane przez narzędzia, naruszenia poziomu węzła muszą zostać sprawdzone za pomocą zespołów zarządzania operacyjnego i skorygowane zgodnie z zasadami operacji. Zasoby, które nie są automatycznie aktualizowane, muszą być uwzględnione w procesach należących do operacji IT.
11. Utworzenie nowych subskrypcji lub grup zarządzania dla wszystkich aplikacji o znaczeniu krytycznym lub chronionych danych wymaga przeglądu od zespołu nadzoru w chmurze, aby zapewnić prawidłowe przypisanie strategii.
12. Model dostępu o najniższych uprawnieniach zostanie zastosowany do wszystkich subskrypcji, które zawierają aplikacje o kluczowym znaczeniu lub chronione dane.
13. Dostawca chmury musi być w stanie zintegrować klucze szyfrowania zarządzane przez istniejące rozwiązanie lokalne.
14. Dostawca chmury musi być w stanie obsłużyć istniejące rozwiązanie urządzenia brzegowego i wszystkie wymagane konfiguracje do ochrony wszelkich publicznie uwidocznionych granic sieci.
15. Dostawca chmury musi być w stanie obsłużyć udostępnianie połączenia z globalną siecią WAN przy użyciu transmisji danych przesyłanej przez istniejące rozwiązanie urządzenia brzegowego.
16. Trendy i luki w zabezpieczeniach, które mogą mieć wpływ na wdrożenia w chmurze, powinny być regularnie weryfikowane przez zespół ds. zabezpieczeń, aby zapewnić aktualizacje narzędzi linii bazowej zabezpieczeń używanej w chmurze.
17. Narzędzia do wdrażania muszą zostać zatwierdzone przez zespół ds. zarządzania chmurą, aby zapewnić ciągły nadzór nad wdrożonymi zasobami.
18. Skrypty wdrażania muszą być utrzymywane w centralnym repozytorium dostępnym dla zespołu ładu chmury w celu okresowego przeglądania i inspekcji.
19. Procesy nadzoru muszą obejmować inspekcje w punkcie wdrożenia oraz regularne cykle w celu zapewnienia spójności wszystkich zasobów.
20. Wdrożenie wszelkich aplikacji, które wymagają uwierzytelnienia klienta, musi używać zatwierdzonego dostawcy tożsamości, który jest zgodny z podstawowym dostawcą tożsamości dla użytkowników wewnętrznych.
21. Procesy nadzoru w chmurze muszą obejmować kwartalne przeglądy z zespołami linii bazowej tożsamości w celu identyfikowania złośliwych aktorów lub wzorców użytkowania, które powinny być blokowane przez konfigurację zasobów w chmurze.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

Ta sekcja modyfikuje projekt ładu MVP w celu uwzględnienia nowych zasad platformy Azure i implementacji Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

Nowe najlepsze rozwiązania są podzielone na dwie kategorie: korporacyjne IT (centrum) i wdrażanie w chmurze (szprych).

**Ustanowienie firmowej subskrypcji centrum IT i satelity w celu scentralizowania linii bazowej zabezpieczeń:** W ramach tego najlepszego rozwiązania istniejąca pojemność ładu jest opakowana przez [topologię Hub i szprychy z usługami udostępnionymi](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services), a kilka najważniejszych dodatków z zespołu nadzoru chmurowego.

1. Repozytorium usługi Azure DevOps. Utwórz repozytorium w usłudze Azure DevOps, aby przechowywać i wypełniać wszystkie odpowiednie szablony Azure Resource Manager i konfiguracje inicjowane przez skrypty.
2. Szablon gwiazdy:
    1. Wskazówki w [topologii Hub i szprych z](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) architekturą referencyjną usług udostępnionych mogą służyć do generowania Menedżer zasobów szablonów dla zasobów wymaganych w firmowym centrum IT.
    2. Korzystając z tych szablonów, tę strukturę można powtarzać w ramach strategii ładu centralnej.
    3. Oprócz bieżącej architektury referencyjnej należy utworzyć szablon sieciowej grupy zabezpieczeń, aby przechwytywać wymagania dotyczące blokowania portów lub listy dozwolonych dla sieci wirtualnej, aby hostować zaporę. Ta sieciowa Grupa zabezpieczeń różni się od wcześniejszych grup, ponieważ będzie to pierwsza sieciowa Grupa zabezpieczeń zezwalająca na ruch publiczny do sieci wirtualnej.
3. Utwórz zasady platformy Azure. Utwórz zasady o nazwie `Hub NSG Enforcement`, aby wymusić konfigurację sieciowej grupy zabezpieczeń przypisanej do dowolnej sieci wirtualnej utworzonej w ramach tej subskrypcji. Zastosuj wbudowane zasady konfiguracji gościa w następujący sposób:
    1. Inspekcja serwerów sieci Web systemu Windows korzystających z bezpiecznych protokołów komunikacyjnych.
    2. Inspekcja ustawień zabezpieczeń hasła w maszynach z systemem Linux i Windows.
4. Firmowy plan IT
    1. Utwórz plan platformy Azure o nazwie `corporate-it-subscription`.
    2. Dodaj szablony Hub i szprych oraz zasady `Hub NSG Enforcement`.
5. Rozwijanie w hierarchii początkowej grupy zarządzania.
    1. Dla każdej grupy zarządzania, która zażądała obsługi chronionych danych, plan `corporate-it-subscription-blueprint` zapewnia przyspieszone rozwiązanie centrum.
    2. Ponieważ grupy zarządzania w tym fikcyjnym przykładzie zawierają hierarchię regionalną oprócz hierarchii jednostek biznesowej, plan ten zostanie wdrożony w każdym regionie.
    3. Dla każdego regionu w hierarchii grupy zarządzania Utwórz subskrypcję o nazwie `Corporate IT Subscription`.
    4. Zastosuj plan `corporate-it-subscription-blueprint` do każdego wystąpienia regionalnego.
    5. Spowoduje to utworzenie centrum dla każdej jednostki biznesowej w każdym regionie. Uwaga: dalsze oszczędności kosztów można osiągnąć, ale udostępnianie centrów w różnych jednostkach roboczych w poszczególnych regionach.
6. Integrowanie obiektów zasad grupy (GPO) przy użyciu konfiguracji żądanego stanu (DSC):
    1. Konwertowanie obiektu zasad grupy na DSC — [projekt zarządzania Microsoft Baseline](https://github.com/Microsoft/BaselineManagement) w serwisie GitHub może przyspieszyć ten nakład pracy. Pamiętaj, aby przechowywać w repozytorium DSC równolegle z szablonami Menedżer zasobów.
    2. Wdróż konfigurację stanu Azure Automation do wszystkich wystąpień firmowej subskrypcji IT. Azure Automation może służyć do zastosowania DSC do maszyn wirtualnych wdrożonych w ramach obsługiwanych subskrypcji w grupie zarządzania.
    3. Bieżące plany planu, które umożliwiają włączenie niestandardowych zasad konfiguracji gościa. Po wydaniu tej funkcji użycie Azure Automation w ramach tego najlepszego rozwiązania nie będzie już wymagane.

**Zastosowanie dodatkowego ładu do subskrypcji wdrażania w chmurze (szprych):** W oparciu o `Corporate IT Subscription`, niewielkie zmiany w programie ładu SPECJALISTy mające zastosowanie do każdej subskrypcji przeznaczonej do obsługi aplikacji Archetypes mogą powodować szybkie ulepszanie.

We wcześniejszych zmianach iteracyjnych najlepszym rozwiązaniem jest zdefiniowanie sieciowych grup zabezpieczeń, aby blokować ruch publiczny i listy dozwolonych ruch wewnętrzny. Ponadto plan platformy Azure tymczasowo utworzył możliwości strefy DMZ i Active Directory. W tej iteracji będziemy dodaliśmy te zasoby jako bity, tworząc nową wersję planu platformy Azure.

1. Szablon komunikacji równorzędnej sieci. Ten szablon spowoduje równorzędną sieć wirtualną w każdej subskrypcji z centralną siecią wirtualną w firmowej subskrypcji IT.
    1. Architektura referencyjna z poprzedniej sekcji, [gwiazdy i topologii z usługami udostępnionymi](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services), wygenerowała Menedżer zasobów szablon służący do włączania komunikacji równorzędnej w sieci wirtualnej.
    2. Ten szablon może służyć jako przewodnik modyfikowania szablonu DMZ z wcześniejszej iteracji ładu.
    3. Teraz dodawana jest Komunikacja równorzędna sieci wirtualnych do sieci wirtualnej DMZ, która była wcześniej połączona z lokalnym urządzeniem brzegowym przez sieć VPN.
    4. Sieć VPN należy również usunąć z tego szablonu, aby upewnić się, że żaden ruch nie jest kierowany bezpośrednio do lokalnego centrum danych, bez przechodzenia przez firmową subskrypcję IT i zaporę. Możesz również ustawić tę sieć VPN jako obwód trybu failover w przypadku awarii obwodu ExpressRoute.
    5. Dodatkowa [Konfiguracja sieci](https://docs.microsoft.com/azure/automation/automation-dsc-overview#network-planning) będzie wymagana przez Azure Automation, aby zastosować DSC do hostowanych maszyn wirtualnych.
2. Zmodyfikuj grupę zabezpieczeń sieci. Zablokuj cały publiczny **i** bezpośredni ruch lokalny w sieciowej grupie zabezpieczeń. Jedyny ruch przychodzący powinien należeć przez równorzędną sieć wirtualną w firmowej subskrypcji IT.
    1. W poprzedniej iteracji utworzono grupę zabezpieczeń sieci, która blokuje cały ruch publiczny i listy dozwolonych cały ruch wewnętrzny. Teraz chcemy przetworzyć tę siećową grupę zabezpieczeń jako bitową.
    2. Nowa konfiguracja sieciowej grupy zabezpieczeń powinna blokować cały ruch publiczny oraz cały ruch z lokalnego centrum danych.
    3. Ruch wprowadzający tę sieć wirtualną powinien pochodzić tylko z sieci wirtualnej po drugiej stronie elementu równorzędnego sieci wirtualnej.
3. Implementacja Azure Security Center:
    1. Skonfiguruj Azure Security Center dla każdej grupy zarządzania zawierającej klasyfikacje chronionych danych.
    2. Domyślnie Ustaw automatyczne Inicjowanie obsługi, aby zapewnić zgodność z poprawkami.
    3. Ustanów konfiguracje zabezpieczeń systemu operacyjnego. Zabezpieczenia INFORMATYCZNe w celu zdefiniowania konfiguracji.
    4. Zapewnianie bezpieczeństwa IT w początkowym użyciu Azure Security Center. Przejście do zabezpieczeń IT przy użyciu usługi Security Center, ale zachowanie dostępu do ciągłego ulepszania zarządzania.
    5. Utwórz szablon Menedżer zasobów odzwierciedlający zmiany wymagane w przypadku konfiguracji Azure Security Center w ramach subskrypcji.
4. Aktualizacja Azure Policy dla wszystkich subskrypcji.
    1. Przeprowadzaj inspekcję i wymuszanie stopnia ważności i klasyfikacji danych we wszystkich grupach zarządzania i subskrypcjach, aby identyfikować wszystkie subskrypcje z chronionymi klasyfikacjami danych.
    2. Inspekcja i wymuszanie korzystania tylko z zatwierdzonych obrazów systemu operacyjnego.
    3. Inspekcja i wymuszanie konfiguracji gościa na podstawie wymagań dotyczących zabezpieczeń dla każdego węzła.
5. Aktualizacja Azure Policy dla wszystkich subskrypcji, które zawierają chronione klasyfikacje danych.
    1. Inspekcja i wymuszanie korzystania tylko z ról standardowych
    2. Inspekcja i wymuszanie stosowania szyfrowania dla wszystkich kont magazynu i plików przechowywanych w poszczególnych węzłach.
    3. Inspekcja i wymuszanie zastosowania nowej wersji sieciowej grupy zabezpieczeń DMZ.
    4. Inspekcja i wymuszanie użycia zatwierdzonej podsieci sieciowej i sieci wirtualnej dla każdego interfejsu sieciowego.
    5. Inspekcja i wymuszanie ograniczenia zdefiniowanych przez użytkownika tabel routingu.
6. Plan platformy Azure:
    1. Utwórz plan platformy Azure o nazwie `protected-data`.
    2. Dodaj do planu elementy równorzędne sieci wirtualnej, sieciowe grupy zabezpieczeń i Azure Security Center.
    3. Upewnij się, że szablon Active Directory z poprzedniej iteracji **nie** jest uwzględniony w planie. Wszystkie zależności dotyczące Active Directory będą udostępniane przez firmową subskrypcję IT.
    4. Przerwij wszystkie istniejące Active Directory maszyny wirtualne wdrożone w poprzedniej iteracji.
    5. Dodaj nowe zasady dla chronionych subskrypcji danych.
    6. Opublikuj plan w dowolnej grupie zarządzania, która będzie hostować chronione dane.
    7. Zastosuj nową strategię do każdej powiązanej subskrypcji wraz z istniejącymi planami.

## <a name="conclusion"></a>Podsumowanie

Dodanie tych procesów i zmian do ładu SPECJALISTy pomaga skorygować wiele zagrożeń związanych z zarządzaniem zabezpieczeniami. Razem dodają narzędzia do monitorowania sieci, tożsamości i zabezpieczeń, które są konieczne do ochrony danych.

## <a name="next-steps"></a>Następne kroki

Wdrożenie chmury kontynuuje się i zapewnia dodatkową wartość biznesową, ale również wymaga zmiany ryzyka i zarządzania chmurą. W przypadku fikcyjnej firmy w tym przewodniku następnym krokiem jest obsługa obciążeń o kluczowym znaczeniu. Jest to punkt, gdy są zbędne kontrolki spójności zasobów.

> [!div class="nextstepaction"]
> [Ulepszanie dyscypliny spójności zasobów](./resource-consistency-improvement.md)
