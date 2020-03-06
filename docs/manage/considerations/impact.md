---
title: Wpływ na działalność w zarządzaniu chmurą
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak określić i zrozumieć wpływ obniżenia poziomu wydajności przez firmę.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: bdd45861141b8fe69f8c13a49bdb6d387acd12ba
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341185"
---
# <a name="business-impact-in-cloud-management"></a>Wpływ na działalność w zarządzaniu chmurą

Przyjmij optymalną wartość, przygotuj dla najgorszej. W zarządzaniu IT można bezpiecznie założyć, że obciążenia wymagane do obsługi operacji biznesowej będą dostępne i będą wykonywane w ramach uzgodnionych ograniczeń na podstawie wybranej krytycznej. Aby jednak zarządzać inwestycjami, ważne jest, aby zrozumieć wpływ na działalność firmy w przypadku wystąpienia awarii lub obniżenia wydajności. Jest to zilustrowane na poniższym grafie, który mapuje potencjalne zakłócenia biznesowe dla konkretnych obciążeń do wpływu na działalność biznesową w skali wartości względnej.

![Wpływ przerw w działaniach firmy](../../_images/manage/time-value-impact.png)

Aby utworzyć sprawiedliwą podstawę porównania wpływu na różne obciążenia w portfolio, Sugerowana jest Metryka czas/wartość. Metryka czas/wartość przechwytuje niekorzystny wpływ na awarie obciążenia. Ogólnie rzecz biorąc, ten wpływ jest rejestrowany w postaci bezpośredniej utraty przychodu lub przychodu operacyjnego w trakcie typowego okresu przestoju. Dokładniej mówiąc, oblicza ilość utraconego przychodu przez jednostkę czasu. Najbardziej typowa Metryka czas/wartość ma *wpływ na godzinę*, co oznacza spadek przychodów z tytułu działalności operacyjnej na godzinę przestoju.

Do obliczenia wpływu można użyć kilku metod. Możesz zastosować dowolną z opcji w poniższych sekcjach, aby osiągnąć podobne wyniki. Ważne jest, aby użyć tego samego podejścia dla każdego obciążenia w przypadku obliczenia chronionych strat w portfolio.

## <a name="start-with-estimates"></a>Rozpocznij od oszacowań

Bieżące modele operacyjne mogą utrudnić ustalenie dokładnego wpływu. Na szczęście niektóre systemy wymagają bardzo dokładnego obliczenia strat. W poprzednim kroku *przeklasyfikowanie ma krytyczne znaczenie*, dlatego zaleca się rozpoczęcie wszystkich obciążeń z domyślną *średnią krytycznością*. Obciążenia średnie o krytycznym znaczeniu zwykle otrzymują standardowy poziom obsługi zarządzania z stosunkowo małym wpływem na koszty operacyjne. Tylko wtedy, gdy obciążenie wymaga dodatkowych zasobów zarządzania operacyjnego, może być konieczne dokładne znaczenie finansowe.

W przypadku wszystkich obciążeń znormalizowanych, wpływ na działalność biznesową służy jako zmienna priorytetyzacja podczas odzyskiwania systemów podczas awarii. Poza tymi ograniczonymi sytuacjami wpływ na działalność biznesową nie zmienia się w środowisku zarządzania operacjami.

## <a name="calculate-time"></a>Oblicz czas

W zależności od charakteru obciążenia można w różny sposób obliczyć straty. W przypadku dużych systemów transakcyjnych, takich jak Platforma handlowa w czasie rzeczywistym, straty na milisekundy mogą być istotne. Rzadziej używane systemy, takie jak lista płac, mogą nie być używane co godzinę. Niezależnie od tego, czy częstotliwość użycia jest wysoka, czy niska, ważne jest, aby znormalizować zmienną czasową przy obliczaniu wpływu finansowego.

## <a name="calculate-total-impact"></a>Oblicz Całkowity wpływ

Jeśli chcesz wziąć pod uwagę dodatkowe inwestycje związane z zarządzaniem, ważniejsze jest, że wpływ na działalność biznesową jest bardziej precyzyjny. Następujące trzy podejścia do obliczania strat są uporządkowane od najdokładniejszych do najdokładniejszych:

- **Skorygowane straty:** Jeśli Twoja firma napotkała poważne zdarzenie utraty w przeszłości, takie jak huragan lub inna klęska żywiołowa, korygowanie oświadczeń mogło spowodować Wyliczenie rzeczywistych strat podczas przestoju. Te obliczenia są oparte na standardach branżowych ubezpieczenia do obliczania strat i zarządzania ryzykiem. Użycie skorygowanych strat jako łącznej liczby strat w określonym przedziale czasu może prowadzić do wysoce dokładnego projekcji.

- **Straty historyczne:** Jeśli środowisko lokalne pozostało w przeszłości od przestoju wynikające z niestabilności infrastruktury, może to być nieco trudniejsze do obliczenia strat. Można jednak nadal stosować formuły dostosowywania używane wewnętrznie. Aby obliczyć straty historyczne, porównaj różnice w sprzedaży, przychody brutto i koszty operacyjne w trzech przedziałach czasu: przed, podczas i po awarii. Badając te różnice, można zidentyfikować dokładne straty, gdy nie są dostępne żadne inne dane.

- **Obliczanie całkowitego ubytku:** Jeśli dane historyczne nie są dostępne, można utworzyć wynik porównawczy. W tym modelu określisz średni przychód brutto za godzinę dla jednostki biznesowej. W przypadku prognozowania inwestycji związanych z unikaniem strat nie jest uzasadnione, aby założyć, że pełna awaria systemu jest równa 100% strat. Można jednak używać tego założeń jako podstawy do porównywania wpływów na straty i określania priorytetów inwestycji.

Przed wprowadzeniem pewnych założeń dotyczących potencjalnych strat związanych z przestojem obciążenia warto skontaktować się z działem finansowym w celu ustalenia najlepszego podejścia do takich obliczeń.

## <a name="calculate-workload-impact"></a>Oblicz wpływ na obciążenie

Gdy obliczasz straty przez zastosowanie danych historycznych, możesz mieć wystarczającą ilość informacji, aby jasno określić udział poszczególnych obciążeń z tymi stratami. Wykonanie tej oceny polega na tym, że partnerstwo w firmie jest absolutnie krytyczne. Po obliczeniu całkowitego wpływu ten wpływ musi być przypisany do każdego z obciążeń. Ten rozkład wpływu powinien pochodzić od zainteresowanych uczestników firmy, który powinien wyrazić zgodę na względny i łączny wpływ poszczególnych obciążeń. W tym celu zespół powinien zażądanie opinii od kierownictwa firmy w celu sprawdzenia poprawności wyrównania. Taka opinia jest często równa części rozpoznawania emocji i wiedzy fachowej. Należy pamiętać, że to ćwiczenie reprezentuje logikę i przekonania uczestników działalności, którzy powinni mieć zamówienie w alokacji budżetu.

## <a name="use-the-template"></a>Korzystanie z szablonu

Jeśli używasz [skoroszytu zarządzania operacjami](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) do planowania zarządzania chmurą, rozważ wykonanie następujących czynności:

- Każda firma powinna aktualizować każde obciążenie w *przykładowym* lub *czystym szablonie* z *wpływem na czas/wartość* każdego obciążenia. Domyślnie wpływ na *czas/wartość* reprezentuje przewidywane straty na godzinę związane z awarią obciążenia.

## <a name="next-steps"></a>Następne kroki

Gdy firma ma zdefiniowany wpływ, można [wyrównać zobowiązania](./commitment.md).

> [!div class="nextstepaction"]
> [Dopasuj zobowiązania dotyczące zarządzania w firmie](./commitment.md)
