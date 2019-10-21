---
title: 'Innowacje w chmurze: pomiar'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — Zmierz zawartość
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 00928171c3bfba1638a7e8e43ea08df4745754d2
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557650"
---
# <a name="measure-for-customer-impact"></a>Miary wpływu klientów

Istnieje kilka sposobów pomiaru wpływu na klientów. Ten artykuł pomoże w definiowaniu miar, które mogą pomóc w sprawdzeniu poprawnych zastąpień utworzonych podczas próby [kompilacji z empatię klienta](./build.md).

## <a name="strategic-metrics"></a>Metryki strategiczne

W [fazie strategii](../../strategy/index.md) cyklu życia wdrożenia w chmurze czytelnicy są przekierują się tworzeniem i dokumentacją dla [motywacji](../../strategy/motivations.md) i wyników działania [biznesowego](../../strategy/business-outcomes/index.md). Te ćwiczenia zapewniają zestaw metryk do użycia jako test wpływu klientów. W przypadku pomyślnego nawiązania innowacji wyniki są wyrównane z celami strategicznymi.

Przed ustanowieniem metryk uczenia należy zdefiniować niewielką liczbę metryk strategicznych, które mają wpływ na innowacje. Ogólnie rzecz biorąc, te metryki strategiczne będą wyrównane do co najmniej jednego z następujących obszarów wyników: [elastyczność biznesowa](../../strategy/business-outcomes/agility-outcomes.md), [zaangażowanie klientów](../../strategy/business-outcomes/engagement-outcomes.md), [osiągnięcie klientów](../../strategy/business-outcomes/reach-outcomes.md), [wpływ finansowy](../../strategy/business-outcomes/fiscal-outcomes.md)lub w przypadku innowacji operacyjnych: [rozwiązanie Wydajność](../../strategy/business-outcomes/fiscal-outcomes.md).

Udokumentowanie uzgodnionych metryk i częsty wpływ na wyniki. Ale nie oczekuje się, że żadne z tych metryk nie pojawią się dla kilku iteracji. Zobacz [zobowiązanie do iteracji](./index.md#commitment-to-iteration) , aby wyrównać oczekiwania.

Poza wskazówką i metrykami wyniku działania biznesowego pozostała część tego artykułu będzie koncentrować się na metrykach uczenia się, które zaprojektowano w celu założenia przejrzystych funkcji odnajdywania i iteracji Zobacz [zaangażowanie do przejrzystości](./index.md#commitment-to-transparency) , aby wyrównać oczekiwania.

## <a name="learning-metrics"></a>Metryki uczenia

Gdy pierwsza wersja dowolnego minimalnego produktu (MVP) jest udostępniona klientom, najlepiej na końcu pierwszej iteracji rozwoju, nie będzie to miało wpływu na metryki strategiczne. Kilka iteracji później zespół może nadal zoptymalizowaniem zmienić zachowania wystarczające do istotnie wpływania strategicznych metryk. W trakcie procesów szkoleniowych, takich jak Build-Measure-Learning Cycles, zaleca się, aby zespół przyjął metryki szkoleniowe. Te metryki mogą być łatwiej śledzone i wykorzystywane w okazjach do poznania się z nimi.

### <a name="customer-flow-and-learning-metrics"></a>Metryki przepływu i uczenia klientów

Jeśli rozwiązanie MVP zweryfikuje hipotezę skoncentrowaną na kliencie, rozwiązanie spowoduje zmianę niektórych zachowań klientów. Te zachowania w różnych kohorty klienta będą obsługiwać wyniki biznesowe. Na szczęście zmiana zachowań klientów jest często procesem wieloetapowym. Każdy krok zapewnia możliwość mierzenia wpływu, dzięki czemu zespół ds. przyjęcia może uczyć się i utworzyć lepsze rozwiązanie.

Informacje o zmianach zachowań klientów zaczynają się od mapowania żądanego przepływu utworzonego przez rozwiązanie MVP.

![Przepływ klientów służący do określania metryk uczenia](../../_images/innovate/customer-flow-learning-metrics.png)

W większości przypadków przepływ klienta będzie miał łatwo zdefiniowany punkt początkowy i nie więcej niż dwa punkty końcowe. Między punktem początkowym a końcowym są różne metryki uczenia, które mają być używane jako miary w pętli opinii:

1. **Punkt początkowy — początkowy wyzwalacz:** Punktem początkowym jest scenariusz, który wyzwala potrzebę tego rozwiązania. Gdy rozwiązanie jest kompilowane z empatię klienta, ten początkowy wyzwalacz powinien wzwoływać klienta, aby wypróbować rozwiązanie MVP.
2. **Klient musi spełniać następujące wymagania:** Hipoteza jest weryfikowana w przypadku, gdy zapotrzebowanie klienta zostało spełnione przy użyciu rozwiązania.
3. **Kroki rozwiązania:** Każdy krok wymagany do przeniesienia klienta z początkowego wyzwalacza do pomyślnego wyniku to krok rozwiązania. Każdy krok generuje metrykę uczenia na podstawie decyzji klienta, aby przejść do następnego kroku.
4. **Uzyskano indywidualne przyjęcie:** Przy następnym napotkaniu wyzwalacza, jeśli klient powróci do rozwiązania, aby ponownie spełnić wymagania, zostanie osiągnięte indywidualne przyjęcie.
5. **Wskaźnik wyniku prowadzenia działalności:** Gdy klient zachowuje się w sposób, który pozytywnie przyczynia się do zdefiniowanego wyniku działania biznesowego, zostanie zaobserwowany wskaźnik wyniku działania biznesowego.
6. **Prawdziwe innowacje:** Gdy "wskaźniki wyników działalności biznesowej" i "indywidualne przyjęcie" pojawiają się w odpowiedniej skali, prawdziwe są innowacje.

Każdy krok przepływu klienta generuje metryki szkoleniowe. Po każdej iteracji (lub wersji) przetestowana jest nowa wersja hipotezy. W tym samym czasie, dostosowania do rozwiązania są testowane w celu odzwierciedlenia zmian w hipotezie. Gdy klienci postępują zgodnie z określoną ścieżką w dowolnym z powyższych kroków, rejestrowana jest pozytywna Metryka. Gdy klienci odróżnią się od określonej ścieżki, aby sprostać potrzebom, rejestrowana jest ujemna Metryka.

Te liczniki wyrównania i odchyleń tworzą metryki szkoleniowe. Każdy z nich powinien być zarejestrowany i śledzony w miarę postępu zespołu wdrożenia w chmurze w kierunku realizacji rezultatów działania biznesowego i prawdziwych innowacji. W następnym artykule omówiono sposoby korzystania [z](./learn.md) tych metryk w celu uczenia się i tworzenia lepszych rozwiązań.

### <a name="grouping-and-observing-customer-partners"></a>Grupowanie i obserwowanie partnerów klientów

Pierwszym pomiarem w celu zdefiniowania metryk uczenia jest definicja partnera klienta. Każdy klient uczestniczący w cyklach innowacji kwalifikuje się jako partner klienta. Aby dokładnie mierzyć zachowanie, ważne jest, aby zdefiniować partnerów klientów w modelu kohorta. W tym modelu klienci są pogrupowani w celu najlepszego zrozumienia, jak reagują na wszelkie zmiany w programie MVP. Partnerzy klienta są często pogrupowani na podstawie punktów danych, takich jak następujące:

- **Eksperymentowanie lub Grupa koncentracji uwagi:** Grupowanie na podstawie klientów mających udział w konkretnym doświadczeniu w celu przetestowania zmian w czasie.
- **Segment:** Grupowanie klientów według rozmiaru firmy.
- W **pionie:** Grupowanie klientów według branżowych, które reprezentują.
- **Indywidualne dane demograficzne:** Grupowanie na podstawie osobistych demograficznych, takich jak wieku lub lokalizacji fizycznej.

Ten typ grupowania pozwala na sprawdzanie poprawności metryk uczenia w różnych sekcjach klientów, którzy wybierają partnera w trakcie wysiłków innowacyjnych. Wszystkie kolejne metryki powinny być zaobserwowane na podstawie definiowanego grupowania klientów.

## <a name="next-steps"></a>Następne kroki

Ponieważ metryki uczenia są gromadzone, zespół może zacząć [uczyć się z klientami](./learn.md).

> [!div class="nextstepaction"]
> [Dowiedz się więcej o klientach](./learn.md)

Niektóre koncepcje przedstawione w tym artykule zawierają informacje dotyczące tematów w pierwszej kolejności opisanej w temacie [Uruchamianie produkcji oszczędnej](http://theleanstartup.com/book), zapisaną przez Eric.
