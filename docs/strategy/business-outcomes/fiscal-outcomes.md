---
title: Przykłady wyników fiskalnych
description: Przykłady wyników fiskalnych
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 7ee0451bd356cfc3fb4c7648f0bbf6b10ab0145f
ms.sourcegitcommit: 011332538dbc6774b732f7b9f2b89d6c8aa90c36
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2020
ms.locfileid: "79023839"
---
# <a name="examples-of-fiscal-outcomes"></a>Przykłady wyników fiskalnych

Na najwyższym poziomie konwersacje fiskalne składają się z trzech podstawowych koncepcji:

- **Przychód:** W wyniku sprzedaży towarów lub usług będzie więcej pieniędzy na działalność biznesową.
- **Koszt:** W przypadku tworzenia, marketingu, sprzedaży lub dostarczania towarów lub usług będzie mniej pieniędzy.
- **Zysk:** Chociaż są rzadkie, niektóre przekształcenia mogą jednocześnie zwiększyć przychód i obniżyć koszty. Jest to wynik zysku.

W pozostałej części tego artykułu objaśniono te wyniki fiskalne w kontekście transformacji w chmurze.

> [!NOTE]
> Poniższe przykłady są hipotetyczne i nie powinny być uznawane za gwarancję powracania w przypadku przyjęcia strategii chmurowej.

## <a name="revenue-outcomes"></a>Wyniki przychodu

### <a name="new-revenue-streams"></a>Nowe strumienie przychodu

Chmura może pomóc w tworzeniu możliwości dostarczania nowych produktów klientom lub dostarczania istniejących produktów w nowy sposób. Nowe strumienie przychodu są innowacyjne, przedsiębiorcze i atrakcyjne dla wielu osób w świecie biznesowym. Nowe strumienie przychodu są również podatne na awarie i są traktowane przez wiele firm jako wysokie ryzyko. Gdy proponowane są wyniki związane z przychodem, prawdopodobnie wystąpi odporność. Aby dodać wiarygodność do tych wyników, partner z liderem firmy, który jest sprawdzoną innowacyjnością. Sprawdzenie, czy strumień przychodu jest wczesny w procesie, pozwala uniknąć przeszkody firmy.

- **Przykład:** Firma sprzedała książki za ponad sto lat. Pracownik firmy zdaje sobie sprawę, że zawartość może być dostarczana elektronicznie. Pracownik tworzy urządzenie, które może zostać sprzedane w księgarni, co pozwala bezpośrednio pobrać te same książki, co wiąże się $X z nową książką sprzedaży.

### <a name="revenue-increases"></a>Wzrost przychodu

Dzięki globalnym skalowaniu i zasięgowi cyfrowemu Chmura może pomóc firmom w zwiększeniu przychodów z istniejących strumieni przychodów. Często ten typ wyników pochodzi z wyrównania ze liderem sprzedaży lub marketingu.

- **Przykład:** Firma, która sprzedaje widżety, może sprzedawać więcej elementów widget, jeśli sprzedawcy mogą bezpiecznie uzyskać dostęp do wykazu cyfrowego i poziomów zapasów firmy. Niestety, te dane są tylko w systemach ERP firmy, do których można uzyskać dostęp tylko za pośrednictwem urządzenia połączonego z siecią. Utworzenie usługi elewacji do interfejsu z systemem ERP i udostępnienie listy katalogów i niewrażliwych poziomów zapasów do aplikacji w chmurze umożliwi sprzedawcom uzyskanie dostępu do danych, których potrzebują, podczas gdy jest to klient z klientem. Rozszerzanie lokalnych Active Directory przy użyciu Azure Active Directory (Azure AD) i integrowanie dostępu opartego na rolach z aplikacją umożliwi firmie zagwarantowanie, że dane pozostaną bezpieczne. Ten prosty projekt może mieć wpływ na przychód z istniejącej linii produktu o _x%_ .

### <a name="profit-increases"></a>Wzrost zysku

Rzadko pojedynczy nakład pracy powoduje zwiększenie przychodu i obniżenie kosztów. Jeśli jednak to robi, należy wyrównać wyniki z jednego lub większej liczby przychodów z co najmniej jednym z kosztów, aby przekazać żądany wynik.

## <a name="cost-outcomes"></a>Wyniki kosztów

### <a name="cost-reduction"></a>Obniżka kosztów

W chmurze obliczeniowej można zredukować wydatki inwestycyjne dotyczące sprzętu i oprogramowania, konfigurować centra danych, uruchamiać centra danych w lokacji i tak dalej. Koszty stojaków serwerów, rundy energii elektrycznej na potrzeby zasilania i chłodzenia oraz specjaliści IT do zarządzania infrastrukturą. Zamknięcie centrum danych może obniżyć zobowiązania z tytułu wydatków inwestycyjnych. Jest to często określane jako "Uzyskiwanie informacji o firmie centrum danych". Obniżka kosztu jest zwykle mierzona w dolarach w bieżącym budżecie, które mogą obejmować od jednej do pięciu lat w zależności od tego, jak dyrektor zarządza finansami.

- **Przykład #1:** Centrum danych firmy zużywa znaczną część rocznego budżetu IT. Umożliwia ona przeprowadzenie migracji w chmurze i przejście zasobów w tym centrum danych do rozwiązań infrastruktury jako usługi (IaaS).
- **Przykład #2:** Firma holdingowa niedawno uzyskała nową firmę. W ramach przejęcia warunki określają, że nowa jednostka powinna zostać usunięta z bieżących centrów danych w ciągu sześciu miesięcy. Niewykonanie tej czynności spowoduje powstanie 1 000 000 USD miesięcznie od firmy holdingowej. Przenoszenie zasobów cyfrowych do chmury w ramach migracji do chmury może pozwolić na szybką likwidację starych zasobów.
- **Przykład #3:** Firma podatkowa korzystająca z podatku dochodowego, która pozyskuje odbiorców w przypadku 70 procent rocznego przychodu w ciągu pierwszych trzech miesięcy roku. Pozostała część roku, jej duża inwestycja w IT jest stosunkowo nieaktywny. Migracja w chmurze może umożliwić jej wdrożenie pojemności obliczeniowej/hostingu wymaganej przez te trzy miesiące. W pozostałych dziewięciu miesiącach koszty IaaS mogą być znacząco ograniczone przez zmniejszenie wpływu obliczeń.

<!-- cSpell:ignore Coverdell Coverdell's Sorensen -->

### <a name="example-coverdell"></a>Przykład: Coverdell

Coverdell zmodernizowanie infrastruktury w celu nanoszenia oszczędności kosztów na platformie Azure. Coverdell decyzję o zainwestowaniu na platformę Azure, a następnie przeanalizować sieci witryn sieci Web, aplikacji, danych i infrastruktury w ramach tego środowiska, doprowadziło do większej oszczędności kosztów niż w przypadku Twojej firmy. Migracja do środowiska przeznaczonego tylko na platformę Azure eliminuje 54 000 USD za miesięczne koszty usług wspólnej lokalizacji. Dzięki nowemu infrastrukturze w dziedzinie zjednoczonej firmy Coverdell oczekuje na zaoszczędzenie szacowanego 1 000 000 USD w ciągu najbliższych dwóch lat.

> "Uzyskanie dostępu do stosu technologii Azure umożliwia otwarcie drzwi dla niektórych skalowalnych, łatwych w implementacji i wysoko dostępnych rozwiązań, które są oszczędne. Dzięki temu nasze architekty mogą być znacznie bardziej kreatywne dzięki dostarczanym przez nie rozwiązaniom.  
> Ryan Sorensen  
> Dyrektor ds. projektowania aplikacji i architektury przedsiębiorstwa  
> Coverdell

### <a name="cost-avoidance"></a>Unikanie kosztów

Zakończenie centrum danych może również zapewnić uniknięcie kosztów, uniemożliwiając w przyszłości cykle odświeżania. Cykl odświeżania to proces kupowania nowego sprzętu i oprogramowania w celu zastąpienia systemów lokalnych. Na platformie Azure sprzęt i system operacyjny są rutynowie utrzymywane, poprawiane i odświeżane bez dodatkowych kosztów dla klientów. Dzięki temu dyrektor finansowy może usunąć planowane przyszłe wydatki na podstawie długoterminowych prognoz finansowych. Unikanie kosztów jest mierzone w dolarach. Różni się to od obniżenia kosztów, zwykle koncentrując się na przyszłym budżecie, który nie został jeszcze w pełni zatwierdzony.

- **Przykład:** Centrum danych firmy jest przeznaczone do odnawiania dzierżawy w ciągu sześciu miesięcy. Centrum danych jest w trakcie obsługi przez osiem lat. Cztery lata temu wszystkie serwery zostały odświeżone i zwirtualizowane, co kosztuje miliony dolarów firmy. W następnym roku firma planuje odświeżanie sprzętu i oprogramowania ponownie. Migrowanie zasobów w tym centrum danych w ramach migracji do chmury umożliwi uniknięcie kosztów przez usunięcie zaplanowanego odświeżania z prognozowanego budżetu w następnym roku. Może ona również generować obniżkę kosztów przez zmniejszenie lub wyeliminowanie kosztów leasingu nieruchomości.

### <a name="capital-expenses-vs-operating-expenses"></a>Koszty kapitałowe a koszty operacyjne

Przed przeprowadzeniem dyskusji na temat kosztów warto zrozumieć dwie podstawowe opcje kosztów: wydatki inwestycyjne i koszty operacyjne.

Poniższe terminy pomogą zrozumieć różnice między kosztami kapitałowymi i kosztami operacyjnymi podczas dyskusji biznesowej o podróży transformującej.

- **Kapitał** jest środkiem pieniężnym i zasobami należącymi do firmy w celu współtworzenia określonych celów, takich jak zwiększenie pojemności serwera lub utworzenie aplikacji.
- **Nakłady inwestycyjne** generują korzyści w długim okresie. Te wydatki są zwykle niecykliczne i powodują pozyskiwanie trwałych zasobów. Tworzenie aplikacji może zakwalifikować się jako nakłady inwestycyjne.
- **Wydatki operacyjne** są ciągłymi kosztami działania firmy. Korzystanie z usług w chmurze w modelu płatność zgodnie z rzeczywistym użyciem może zakwalifikować się jako wydatki operacyjne.
- **Zasoby są zasobami** gospodarczymi, które mogą być własnością lub być kontrolowane w celu utworzenia wartości. Wszystkie serwery, jeziora i aplikacje mogą być uznawane za zasoby.
- **Amortyzacja** to spadek wartości elementu zawartości w miarę upływu czasu. W odniesieniu do wydatków kapitałowych i konwersacji związanych z kosztami, amortyzacja polega na tym, jak koszty zasobu są przyliczane w okresach, w których są używane. Na przykład jeśli tworzysz aplikację w tym roku, ale oczekujesz średniego okresu istnienia na pięć lat (takich jak większość aplikacji komercyjnych), koszt zespołu deweloperów i niezbędnych narzędzi wymaganych do utworzenia i wdrożenia bazy kodu będzie amortyzowany nawet na pięć czterocyfrowy.
- **Jest to proces szacowania,** ile jest cennych firmy. W większości branż wycenia bazuje na zdolności firmy do generowania przychodów i zysków, przy jednoczesnym poszanowaniu kosztów operacyjnych wymaganych do utworzenia towarów, które zapewniają ten przychód. W niektórych branżach, takich jak sprzedaż detaliczna lub w niektórych typach transakcji, takich jak prywatna kapitału, zasoby i amortyzacja mogą odgrywać znaczną część oceny firmy.

Często jest to bezpieczne trafienie, które w różnych kierownikach, w tym dyrektor ds. inwestycji (CIO), zanotują najlepsze wykorzystanie kapitału do rozwoju firmy w odpowiednim kierunku. CIOnie środków w celu przeprowadzenia konwersji contentiousych wydatków inwestycyjnych na wyznaczną odpowiedzialność za wydatki operacyjne może być atrakcyjny przez siebie. W wielu branżach dyrektorzy ds. finansów (CFOs) aktywnie dążą do lepszego kojarzenia z kosztami związanymi z sprzedażą.

Jednak przed skojarzeniem każdej transformacji z tym typem kapitału a konwersją kosztów operacyjnych, warto zaspokoić członków zespołów DYREKTORów lub CIOów, aby zobaczyć, która struktura kosztów jest preferowana przez firmę. W niektórych organizacjach zmniejszenie wydatków inwestycyjnych na rzecz wydatków operacyjnych jest wysoce *niepożądanym* wynikiem. Jak wspomniano wcześniej, takie podejście jest czasami widoczne w detalicznych, holdingowych i prywatnych kapitale kapitałowym, które zwiększają wartość w tradycyjnych modelach księgowości zasobów, które stanowią małą wartość w adresie IP. Jest on również widoczny w organizacjach, które mają negatywny wpływ na to, kiedy pochodzą one od pracownika działu IT lub innych funkcji w przeszłości.

W przypadku pożądanego modelu wydatków operacyjnych Poniższy przykład może być opłacalnym wynikiem działalności:

- **Przykład:** Centrum danych firmy jest obecnie amortyzowane o _x USD_ rocznie przez następne trzy lata. Oczekuje się, że do odświeżenia sprzętu w następnym roku jest wymagana dodatkowa wartość _y USD_ . Możemy przekonwertować wydatki inwestycyjne na model wydatków operacyjnych z parzystą stawką z _USD_ na miesiąc, co pozwala na lepsze zarządzanie kosztami korzystania z technologii i odpowiedzialność za nie.

## <a name="next-steps"></a>Następne kroki

Dowiedz się [więcej o](./agility-outcomes.md)sposobach zdobywania elastyczności.

> [!div class="nextstepaction"]
> [Wyniki elastyczność](./agility-outcomes.md)
