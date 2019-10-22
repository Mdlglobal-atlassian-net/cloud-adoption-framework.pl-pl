---
title: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: be5cc97c7b42eb79f0ec9721376524dc2710e2c4
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683629"
---
# <a name="business-impact-in-cloud-management"></a>Wpływ na działalność w zarządzaniu chmurą

Przyjmij optymalną wartość, przygotuj dla najgorszej. W zarządzaniu działem IT można bezpiecznie założyć, że obciążenia wymagane do obsługi operacji biznesowej będą dostępne i będą wykonywane w ramach uzgodnionych ograniczeń na podstawie wybranej krytycznej. Aby jednak zarządzać inwestycjami, ważne jest zrozumienie wpływu działania firmy w przypadku wystąpienia awarii lub obniżenia wydajności. To znaczenie jest zilustrowane w poniższym grafie, który mapuje potencjalne przerwy w działaniu konkretnych obciążeń na wpływ na działalność biznesową w skali wartości względnej.

![Wpływ przerw w działaniach firmy](../../_images/manage/time-value-impact.png)

Aby utworzyć sprawiedliwą podstawę porównania wpływu na różne obciążenia w portfolio, Sugerowana jest Metryka czas/wartość. Metryka czas/wartość przechwytuje niekorzystny wpływ na awarie obciążenia. Ogólnie rzecz biorąc, ten wpływ jest rejestrowany w postaci bezpośredniej utraty przychodu lub przychodu operacyjnego w trakcie typowego okresu przestoju. Dokładniej, obliczanie ilości utraconego przychodu przez jednostkę czasu. Najbardziej typowym metryką czasu/wartości jest "wpływ na godzinę", co oznacza, że straty na dochody z przychodu są naliczane za godzinę przestoju.

Istnieje kilka metod, których można użyć do obliczenia wpływu. Z podobnymi wynikami można korzystać z dowolnej opcji w poniższych sekcjach. Ważne jest, aby użyć tego samego podejścia dla każdego obciążenia podczas obliczania chronionych strat w portfolio.

## <a name="start-with-estimates"></a>Rozpocznij od oszacowań

Bieżące modele operacyjne mogą utrudniać ustalenie dokładnego wpływu. Na szczęście niektóre systemy wymagają bardzo dokładnego obliczenia strat. W poprzednim kroku: klasyfikowanie stopnia krytycznego, sugerowano, że wszystkie obciążenia zaczynają się domyślnie od "średniej krytycznej". Obciążenia średnie o krytycznym znaczeniu zwykle otrzymują standardowy poziom obsługi zarządzania z stosunkowo małym wpływem na koszty operacyjne. Tylko wtedy, gdy obciążenie wymaga dodatkowych zasobów zarządzania operacyjnego, należy podać dokładne znaczenie finansowe.

W przypadku wszystkich obciążeń znormalizowanych wpływ na działalność biznesową służy jako zmienna priorytetyzacja podczas odzyskiwania systemów podczas awarii. Poza tymi ograniczonymi sytuacjami wpływ na działalność biznesową zostanie nieco niezmieniony w środowisku zarządzania operacjami. 

## <a name="calculating-time"></a>Obliczanie czasu

W zależności od charakteru obciążenia straty mogą być obliczane w różny sposób. W przypadku dużych systemów transakcyjnych, takich jak platforma handlu w czasie rzeczywistym, straty na milisekundy mogą być istotne. Rzadziej używane systemy, takie jak lista płac, nie mogą być używane co godzinę. Niezależnie od tego, czy częstotliwość użycia jest wysoka, czy niska, ważne jest, aby znormalizować zmienną czasową przy obliczaniu wpływu finansowego.

## <a name="calculating-total-impact"></a>Obliczanie całkowitego wpływu

Gdy potrzebne są dodatkowe inwestycje związane z zarządzaniem, ważniejsze jest, aby wpływ na działalność biznesową był bardziej precyzyjny. Konspekt kolejnych punktorów podejścia do obliczania strat w kolejności najdokładniejszych (od najdokładniejszych do najmniejszych dokładności):

- **Skorygowane straty:** Jeśli w przeszłości wystąpi duże zdarzenie utraty, takie jak huragan lub inna klęska żywiołowa, korygowanie oświadczeń mogło spowodować Wyliczenie rzeczywistych strat podczas przestoju. Te obliczenia są oparte na standardach branżowych ubezpieczenia do obliczania strat i zarządzania ryzykiem. Użycie skorygowanych strat jako łącznej liczby strat w określonym przedziale czasu może prowadzić do wysoce dokładnego projekcji.

- **Straty historyczne:** Jeśli środowisko lokalne zostało poniesione z powodu niestabilności infrastruktury, może to być nieco trudniejsze do obliczenia strat. Jednak formuły korygowania nadal mogą być używane wewnętrznie. Aby obliczyć wyniki historyczne, porównaj różnice w sprzedaży, przychody brutto i koszty operacyjne w trzech przedziałach czasu: przed, podczas i po awarii. Badanie tych różnic może identyfikować dokładne utraty, gdy żadne inne dane nie są dostępne.

- **Obliczanie całkowitego ubytku:** Jeśli żadne dane historyczne nie są dostępne, można uzyskać porównawczą wartość straty. W tym modelu należy określić średni przychód brutto za godzinę dla jednostki biznesowej. Przy założeniu, że pełna awaria systemu jest równa 100% strata przychodu jest słabo założeń podczas prognozowania inwestycji związanych z unikaniem strat. Można go jednak używać jako podstawy do porównywania wpływów na straty i określania priorytetów inwestycji.

Przed wprowadzeniem założeń dotyczących obliczeń związanych z utratą należy skontaktować się z działem finansowym w celu ustalenia najlepszego podejścia do obliczania potencjalnych strat związanych z awarią obciążenia.

## <a name="calculating-workload-impact"></a>Obliczanie wpływu obciążenia

W przypadku wykorzystywania danych historycznych do obliczania strat może istnieć wystarczająco dużo informacji, aby jasno określić wpływ poszczególnych obciążeń na te straty. Ta ocena polega na tym, że partnerstwo z firmą jest absolutnie krytyczne. Po obliczeniu całkowitego wpływu ten wpływ musi być przypisany do poszczególnych obciążeń. Ten rozkład wpływu powinien pochodzić od zainteresowanych uczestników firmy, który powinien wyrazić zgodę na względny i łączny wpływ poszczególnych obciążeń. Dodatkowo zespół powinien zaproponować opinię od kierownictwa firmy w celu sprawdzenia poprawności wyrównania. Niestety, wynik końcowy jest równy częściom rozpoznawania emocji i wiedzą z dziedziny. Znaczenie tego ćwiczenia polega na tym, że reprezentuje on logikę i przekonania uczestników działalności, którzy powinni mieć zamówienie w alokacji budżetu.

## <a name="using-the-template"></a>Korzystanie z szablonu

Poniższe kroki dotyczą czytelników, którzy używają [skoroszytu usługi Ops Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) do planowania zarządzania chmurą.

1. Każde obciążenie w "przykładowym" lub "czystym szablonie" powinno być aktualizowane przez firmę z użyciem wartości "czas/wartość" w każdym obciążeniu. Domyślnie "wpływ na czas/wartość" oznacza przewidywane straty na godzinę związane z awarią obciążenia.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu wpływu [zobowiązania mogą być wyrównane](./commitment.md).

> [!div class="nextstepaction"]
> [Dopasuj zobowiązania dotyczące zarządzania w firmie](./commitment.md)
