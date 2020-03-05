---
title: Model finansowy migracji do chmury
description: Dowiedz się, co należy zrobić, aby utworzyć model finansowy, który dokładnie reprezentuje pełną wartość biznesową transformacji w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: ebc85c5a76d9f53b0117567fc79de51488e9b51d
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337986"
---
# <a name="create-a-financial-model-for-cloud-transformation"></a>Tworzenie modelu finansowego transformacji do chmury

Utworzenie modelu finansowego, który dokładnie reprezentuje pełną wartość biznesową dowolnego przekształcenia w chmurze, może być skomplikowany. Modele finansowe i uzasadnienia biznesowe mogą się różnić w zależności od różnych organizacji. W tym artykule opisano niektóre formuły i przedstawiono kilka kwestii, które są często pominięte, gdy strategie tworzą modele finansowe.

## <a name="return-on-investment"></a>Zwrot z inwestycji

Zwrot z inwestycji jest często ważnym kryterium dla zestawu C-lub tablicy. Zwrot z inwestycji jest używany do porównywania różnych sposobów inwestowania ograniczonych zasobów inwestycyjnych. Formuła zwrotu z inwestycji jest dość prosta. Szczegóły potrzebne do utworzenia poszczególnych danych wejściowych formuły mogą nie być proste. W związku z tym zwrot z inwestycji jest ilością zwrotu wygenerowanego na podstawie początkowej inwestycje. Zwykle jest reprezentowane jako wartość procentowa:

![Zwroty zwrotne (zysk z inwestycji pomniejszonej o koszty inwestycji) podzielone według kosztów inwestycji](../_images/strategy/formula-roi.png)

W następnych sekcjach przeprowadzimy Cię przez dane, które będą potrzebne do obliczenia początkowej inwestycji i uzyskania zysku z inwestycji (zarobki).

## <a name="calculate-initial-investment"></a>Obliczanie inwestycji początkowej

Inwestycja początkowa to koszty kapitałowe i koszty operacyjne wymagane do ukończenia transformacji. Klasyfikacja kosztów może się różnić w zależności od modeli ewidencjonowania aktywności i preferencji DYREKTORów. Jednak ta kategoria obejmuje elementy, takie jak profesjonalne usługi, do przekształcania, licencje na oprogramowanie używane tylko w trakcie transformacji, koszt usług Cloud Services w trakcie przekształceń i potencjalnie koszt pracowników płatnych podczas transformacji .

Dodaj te koszty, aby utworzyć oszacowanie początkowej inwestycji.

## <a name="calculate-the-gain-from-investment"></a>Oblicz zysk z inwestycji

Obliczenie korzyści z inwestycji często wymaga drugiej formuły, która jest specyficzna dla wyników działalności biznesowej i skojarzonych zmian technicznych. Obliczanie zarobków jest trudniejsze niż Obliczanie obniżki kosztów.

Aby obliczyć zarobki, potrzebne są dwie zmienne:

![Zyskaj od inwestycji równych różnic przychodu i różnic kosztów](../_images/strategy/formula-gain-from-investment.png)

Te zmienne są opisane w poniższych sekcjach.

## <a name="revenue-deltas"></a>Różnice przychodu

Różnice przychodów powinny być prognozami w ramach partnerstwa ze stronami biznesowymi. Gdy zainteresowane strony biznesowe zgadzają się na wpływ przychodów, mogą służyć do usprawnienia postanowień.

## <a name="cost-deltas"></a>Różnice kosztów

Różnice kosztów to wielkość wzrostu lub zmniejszenia, która będzie powodowana przez transformację. Zmienne niezależne mogą wpływać na różnice kosztów. Zarobki są duże w oparciu o koszty, takie jak obniżki wydatków kapitałowych, unikanie kosztów operacyjnych i obniżki amortyzacji. W poniższych sekcjach opisano niektóre różnice kosztów, które należy wziąć pod uwagę.

### <a name="depreciation-reduction-or-acceleration"></a>Obniżka lub przyspieszenie amortyzacji

Aby uzyskać wskazówki dotyczące amortyzacji, skontaktuj się z działem FINANSOWYm lub zespołem finansowym. Poniższe informacje są przeznaczone do użycia jako ogólne informacje dotyczące tematu amortyzacji.

Gdy kapitał jest zainwestowany w ramach nabycia elementu zawartości, można użyć tej inwestycji na potrzeby finansowe lub podatkowe w celu uzyskania aktualnych korzyści w stosunku do oczekiwanych cykl życia zasobów. Niektóre firmy zobaczą amortyzację jako korzyść dodatnią. Inne widzą je jako zatwierdzone, bieżące wydatki podobne do innych cyklicznych wydatków przypisanych do rocznego budżetu IT.

Porozmawiaj z biurem finansowym, aby dowiedzieć się, czy możliwe jest wyeliminowanie amortyzacji, a jeśli spowodowałoby to pozytywny udział w różnicach kosztów.

### <a name="physical-asset-recovery"></a>Odzyskiwanie zasobów fizycznych

W niektórych przypadkach wycofane zasoby mogą być sprzedawane jako źródło przychodu. Ten przychód jest często podzielony na zmniejszenie kosztów dla uproszczenia. Jednak naprawdę wzrost przychodu i może być opodatkowany jako taki. Porozmawiaj z biurem finansowym, aby zrozumieć żywotność tej opcji oraz jak uwzględnić otrzymany przychód.

### <a name="operational-cost-reductions"></a>Obniżki kosztów operacyjnych

Wydatki cykliczne wymagane do działania firmy często są nazywane kosztami operacyjnymi. Jest to szeroka Kategoria. W większości modeli ewidencjonowania aktywności obejmuje:

- Licencjonowanie oprogramowania.
- Wydatki hostingu.
- Rachunki elektryczne.
- Czynsze nieruchomości.
- Koszty chłodzenia.
- Pracownicy tymczasowi zobowiązani do wykonywania operacji.
- Wynajem sprzętu.
- Części zamienne.
- Kontrakty konserwacji.
- Napraw usługi.
- Usługi ciągłości działania i odzyskiwania po awarii (BCDR).
- Inne wydatki, które nie wymagają zatwierdzeń wydatków inwestycyjnych.

Ta kategoria zawiera jedno z największych różnic w zdobywaniu. Gdy rozważasz migrację do chmury, czas zainwestowany w taki sposób, że ta lista jest rzadko tracona. Podawaj pytania CIO i działu finansów, aby upewnić się, że są uwzględniane wszystkie koszty operacyjne.

### <a name="cost-avoidance"></a>Unikanie kosztów

Gdy wydatki operacyjne są oczekiwane, ale nie są jeszcze w zatwierdzonym budżecie, mogą nie mieścić się w kategorii redukcja kosztów. Na przykład jeśli licencje na oprogramowanie VMware i Microsoft muszą być ponownie negocjowane i płatne w następnym roku, nie są jeszcze w pełni kwalifikowanymi kosztami. Obniżki w odniesieniu do przewidywanych kosztów są traktowane jak koszty operacyjne w celu obliczenia różnic kosztów. Jednak nieformalnie powinny być określane jako "unikanie kosztów" do momentu zakończenia negocjacji i zatwierdzenia budżetu.

### <a name="soft-cost-reductions"></a>Obniżenie kosztów nieelastycznych

W niektórych firmach koszty uboczne, takie jak redukcje złożoności operacyjnej lub obniżki w przypadku personelu w czasie pełnym na potrzeby obsługi centrum danych, można również uwzględnić w różnicach kosztów. Jednak w tym koszty nietrwałe mogą nie być dobrym pomysłem. W przypadku dołączania obniżek kosztów ubocznych należy wstawić niezaudokumentowane założenie, że obniżka spowoduje oszczędność kosztów. Projekty technologiczne rzadko powodują rzeczywiste odzyskanie kosztów.

### <a name="headcount-reductions"></a>Redukcje liczby pracowników

Oszczędności czasu dla pracowników często są uwzględniane w ramach obniżenia kosztów. Gdy oszczędności czasu są mapowane na rzeczywiste zmniejszenie wynagrodzeń lub kadry IT, można je obliczyć osobno jako obniżki liczby pracowników.

Wspomniane w ten sposób umiejętności wymagane lokalnie są zwykle mapowane na podobny (lub wyższy) zestaw umiejętności wymaganych w chmurze. Dlatego, że osoby nie są zwykle wyłączone po migracji do chmury.

Wyjątek występuje, gdy pojemność operacyjna jest świadczona przez inną firmę lub dostawcę usług zarządzanych (MSP). Jeśli systemy IT są zarządzane przez inną firmę, koszty operacyjne mogą zostać zastąpione przez rozwiązanie natywne w chmurze lub natywne. Natywny w chmurze kod MSP prawdopodobnie działa wydajniej i może mieć niższy koszt. W takim przypadku obniżki kosztów operacyjnych należą do obliczeń kosztów.

### <a name="capital-expense-reductions-or-avoidance"></a>Redukcje i unikanie wydatków inwestycyjnych

Wydatki inwestycyjne różnią się nieco od kosztów operacyjnych. Ogólnie rzecz biorąc, Ta kategoria jest oparta na cyklach odświeżania lub rozszerzeniu centrum danych. Przykładem rozwinięcia centrum danych będzie nowy klaster o wysokiej wydajności, który będzie hostować rozwiązanie do obsługi danych Big Data lub hurtowe dane. Ten koszt zwykle mieści się w kategorii wydatków inwestycyjnych. Najczęściej są to podstawowe cykle odświeżania. Niektóre firmy mają sztywne cykle odświeżania sprzętu, co oznacza, że zasoby są wycofywane i zastępowane w regularnych cyklach (zwykle co trzy, pięć lub osiem lat). Te cykle często pokrywają się z cyklami dzierżawy zasobów lub prognozowanym okresem użytkowania sprzętu. Gdy trafi cykl odświeżania, pobierany jest koszt inwestycyjny w celu uzyskania nowego sprzętu.

W przypadku zatwierdzenia cyklu odświeżania i budżetowania przekształcenie w chmurze może pomóc wyeliminować ten koszt. Jeśli cykl odświeżania jest planowany, ale nie został jeszcze zatwierdzony, przekształcenie w chmurze może uniknąć wydatków inwestycyjnych. Oba redukcje byłyby dodawane do różnicy kosztów.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o modelach [ewidencjonowania aktywności w chmurze](./cloud-accounting.md) .

> [!div class="nextstepaction"]
> [Ewidencjonowanie aktywności w chmurze](./cloud-accounting.md)
