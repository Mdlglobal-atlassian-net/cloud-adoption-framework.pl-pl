---
title: Zmierz wpływ klienta
description: Zdefiniuj odpowiedni przepływ klienta i ustal metryki uczenia, aby mierzyć zachowanie i wdrażanie klientów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 49377f419a8b5315a9f4a544fca37579b6dfbcaa
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80427395"
---
# <a name="measure-for-customer-impact"></a>Mierzenie wpływu na klientów

Istnieje kilka sposobów pomiaru wpływu na klientów. Ten artykuł pomoże Ci zdefiniować metryki, aby sprawdzić poprawność postanowień, które wystąpiły w wyniku wysiłku do [kompilowania z empatię klientów](./build.md).

## <a name="strategic-metrics"></a>Metryki strategiczne

W [fazie strategii](../../strategy/index.md) cyklu życia wdrożenia chmury sprawdzimy [motywacje](../../strategy/motivations.md) i [wyniki biznesowe](../../strategy/business-outcomes/index.md). Te praktyki zawierają zestaw metryk, za pomocą których można testować wpływ klientów. Po pomyślnym nadaniu innowacji można zobaczyć wyniki, które są wyrównane z celami strategicznymi.

Przed ustanowieniem metryk uczenia należy zdefiniować niewielką liczbę metryk strategicznych, na które mają wpływ te innowacje. Ogólnie rzecz biorąc, te strategiczne metryki są wyrównane z co najmniej jednym z następujących obszarów wyników: [elastyczność biznesowa](../../strategy/business-outcomes/agility-outcomes.md), [zaangażowanie klientów](../../strategy/business-outcomes/engagement-outcomes.md), [zasięg klienta](../../strategy/business-outcomes/reach-outcomes.md), [wpływ finansowy](../../strategy/business-outcomes/fiscal-outcomes.md)lub w przypadku innowacji operacyjnych: [wydajność rozwiązania](../../strategy/business-outcomes/fiscal-outcomes.md).

Udokumentowanie uzgodnionych metryk i śledzenie ich wpływu na często. Ale nie oczekuje się, że żadne z tych metryk nie pojawią się dla kilku iteracji. Aby uzyskać więcej informacji na temat ustawiania i wyrównywania oczekiwań we wszystkich zaangażowanych stronach, zobacz [zobowiązanie do iteracji](./index.md#commitment-to-iteration).

Poza wskazówką i metrykami wyniku biznesowego, pozostała część tego artykułu koncentruje się na metrykach uczenia się, które zaprojektowano w celu założenia przejrzystych funkcji odnajdywania i iteracji Aby uzyskać więcej informacji na temat tych aspektów, zobacz temat [zaangażowanie do przejrzystości](./index.md#commitment-to-transparency).

## <a name="learning-metrics"></a>Metryki uczenia

Gdy pierwsza wersja dowolnego minimalnego produktu (MVP) jest udostępniona klientom, najlepiej na końcu pierwszej iteracji rozwoju, nie będzie to miało wpływu na metryki strategiczne. Kilka iteracji później zespół może nadal zoptymalizowaniem zmienić zachowania wystarczające, aby materiał miał wpływ na metryki strategiczne. W trakcie procesów szkoleniowych, takich jak Build-Measure-Learning Cycles, firma Microsoft zaleca zespołowi przyjęcie metryk uczenia się. Te metryki śledzą i możliwości uczenia się.

### <a name="customer-flow-and-learning-metrics"></a>Metryki przepływu i uczenia klientów

Jeśli rozwiązanie MVP zweryfikuje hipotezę skoncentrowaną na kliencie, rozwiązanie spowoduje zmianę niektórych zachowań klientów. Te zmiany w kohorty klienta powinny poprawić wyniki biznesowe. Należy pamiętać, że zmiana zachowania klienta jest zwykle procesem wieloetapowym. Ponieważ każdy krok zapewnia możliwość mierzenia wpływu, zespół ds. przyjęcia może utrzymywać uczenie i budować lepsze rozwiązanie.

Informacje o zmianach zachowania klienta zaczynają się od mapowania przepływu, który masz nadzieję, że zobaczysz od rozwiązania MVP.

![Przepływ klientów służący do określania metryk uczenia](../../_images/innovate/customer-flow-learning-metrics.png)

W większości przypadków przepływ klienta będzie miał łatwo zdefiniowany punkt początkowy i nie więcej niż dwa punkty końcowe. Między punktem początkowym a końcowym są różne metryki uczenia, które mają być używane jako miary w pętli opinii:

1. **Punkt początkowy — wyzwalacz początkowy:** Punkt początkowy jest scenariuszem, który wyzwala potrzebę tego rozwiązania. Gdy rozwiązanie jest kompilowane z empatię klienta, ten początkowy wyzwalacz powinien wzwoływać klienta, aby wypróbować rozwiązanie MVP.
2. **Klient musi spełniać następujące wymagania:** Hipoteza jest weryfikowana w przypadku, gdy zapotrzebowanie klienta zostało spełnione przy użyciu rozwiązania.
3. **Kroki rozwiązania:** Termin ten odnosi się do czynności, które są wymagane do przeniesienia klienta z początkowego wyzwalacza do pomyślnego wyniku. W każdym kroku powstaje Metryka szkoleniowa oparta na decyzji klienta o przejściu do następnego kroku.
4. **Uzyskano indywidualne przyjęcie:** Przy następnym napotkaniu wyzwalacza, jeśli klient powróci do rozwiązania w celu uzyskania ich spełnienia, zostanie osiągnięte indywidualne przyjęcie.
5. **Wskaźnik wyniku prowadzenia działalności:** Gdy klient zachowuje się w sposób, który przyczynia się do zdefiniowanego wyniku działania biznesowego, zostanie zaobserwowany wskaźnik wyniku działania biznesowego.
6. **Prawdziwe innowacje:** Gdy *wskaźniki wyniku biznesowego* i *indywidualne przyjęcie* są wykonywane w odpowiedniej skali, zostały zrealizowane prawdziwe innowacje.

Każdy krok przepływu klienta generuje metryki szkoleniowe. Po każdej iteracji (lub wersji) przetestowana jest nowa wersja hipotezy. W tym samym czasie, dostosowania do rozwiązania są testowane w celu odzwierciedlenia zmian w hipotezie. Gdy klienci postępują zgodnie z określoną ścieżką w danym kroku, zostanie zarejestrowana Metryka pozytywna. Gdy klienci odróżnią od określonej ścieżki, rejestrowana jest ujemna Metryka.

Te liczniki wyrównania i odchyleń tworzą metryki szkoleniowe. Każdy z nich powinien być zarejestrowany i śledzony, gdy zespół wdrażający chmurę postępuje w kierunku wyników działalności biznesowej i prawdziwych innowacji. W temacie [Informacje o klientach](./learn.md)omówiono sposoby zastosowania tych metryk w celu uczenia się i skompilowania lepszych rozwiązań.

### <a name="grouping-and-observing-customer-partners"></a>Grupowanie i obserwowanie partnerów klientów

Pierwszym pomiarem definiującym metryki szkoleniowe jest definicja partnera klienta. Każdy klient, który uczestniczy w cyklach innowacji, kwalifikuje się jako partner klienta. Aby precyzyjnie mierzyć zachowanie, należy użyć modelu kohorta w celu zdefiniowania partnerów klientów. W tym modelu klienci są pogrupowani w celu wyostrzenia wiedzy o zmianach w programie MVP. Te grupy są zwykle podobne do następujących:

- **Eksperymentowanie lub Grupa koncentracji uwagi:** Grupowanie klientów na podstawie ich udziału w konkretnym eksperymentie przeznaczonym do testowania zmian w czasie.
- **Segment:** Grupowanie klientów według rozmiaru firmy.
- W **pionie:** Grupowanie klientów według *branżowych* , które reprezentują.
- **Indywidualne dane demograficzne:** Grupowanie na podstawie osobistych demograficznych, takich jak wiek i lokalizacja fizyczna.

Te typy grup ułatwiają Weryfikowanie metryk uczenia w różnych sekcjach klientów, którzy wybierają partnerów w ramach wysiłków związanych z innowacją. Wszystkie kolejne metryki powinny pochodzić z definiowanego grupowania klientów.

## <a name="next-steps"></a>Następne kroki

Jak są gromadzone metryki szkoleniowe, zespół może zacząć [uczyć się z klientami](./learn.md).

> [!div class="nextstepaction"]
> [Uczenie się wraz z klientami](./learn.md)

<!-- cSpell:ignore Ries -->

Niektóre koncepcje przedstawione w tym artykule zawierają informacje dotyczące tematów w pierwszej kolejności opisanej w temacie [Uruchamianie produkcji oszczędnej](http://theleanstartup.com/book), zapisaną przez Eric.
