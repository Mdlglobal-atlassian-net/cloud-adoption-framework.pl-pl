---
title: Operacje obciążeń — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Operacje obciążeń — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5f250362e93a81c6bb38ef11e8659484ef023182
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683730"
---
# <a name="workload-operations-in-cloud-management"></a>Operacje na obciążeniach w zarządzaniu chmurą

Niektóre obciążenia mają kluczowe znaczenie dla sukcesu firmy. W przypadku tych obciążeń linia bazowa zarządzania nie wystarcza do spełnienia wymagań firmy wymaganych do zarządzania chmurą. Operacje na platformie mogą jeszcze nie być wystarczające, aby zaspokoić zobowiązania biznesowe. Ten wysoce istotny podzbiór obciążeń wymaga wyspecjalizowanego skoncentrowania się na sposobie działania obciążeń i sposobu ich obsługi.

W powrocie operacje związane z obciążeniem mogą prowadzić do zwiększenia wydajności, zmniejszenia ryzyka zakłócenia działania firmy oraz szybszego odzyskiwania w przypadku wystąpienia awarii systemu. W tym artykule przedstawiono podejście do inwestowania w dalsze operacje dotyczące tych obciążeń o wysokim priorytecie, aby zwiększyć zobowiązania biznesowe.

## <a name="when-to-invest-in-workload-operations"></a>Kiedy inwestować w operacje obciążeń

Zasada wykresu Pareto (znana także jako reguła 80/20) stwierdza, że 80% efektów pochodzi z 20% przyczyn. Gdy portfolio IT można zwiększyć organicznie w miarę upływu czasu, ta reguła może być często widoczna w przeglądzie portfolio IT. W zależności od wpływu inwestycji Przyczyna może się różnić, ale zasada ogólna ma wartość PRAWDA:

- 80% błędów systemu jest wynikiem 20% typowych błędów lub usterek
- 80% wartości biznesowej może pochodzić z 20% obciążeń w portfolio
- 80% wysiłku do migracji do chmury pochodzi z 20% przenoszonych obciążeń
- 80% wysiłków związanych z zarządzaniem chmurą będzie obsługiwać 20% zdarzeń usługi lub biletów problemów
- 80% wpływu działania firmy na awarie będzie pochodzić z 20% systemów, na które wpłynie awaria

Operacje obciążeń powinny być stosowane tylko wtedy, gdy strategia wdrażania chmury, wyniki biznesowe i metryki operacyjne są dobrze zrozumiałe. Jest to zmiana modelu z klasycznego widoku IT. Tradycyjnie zakłada się, że wszystkie obciążenia miały ten sam stopień wsparcia i wymagają podobnych poziomów priorytetów.

Przed zainwestowaniem w szczegółowe operacje obciążeń, zarówno IT, jak i firma powinny zrozumieć uzasadnienie biznesowe i oczekiwania na zwiększenie inwestycji w zarządzanie chmurą.

## <a name="start-with-the-data"></a>Zacznij od danych

Operacje związane z obciążeniem rozpoczynają się od dokładnego poznania wydajności obciążeń i wymagań dotyczących obsługi. Przed rozpoczęciem inwestowania w operacje obciążeniowe zespół musi mieć zaawansowane dane dotyczące: zależności obciążenia, wydajność aplikacji, Diagnostyka bazy danych, dane telemetryczne maszyn wirtualnych i historię zdarzeń.

Te dane są przeznaczone do uzyskiwania informacji, które są przeznaczone do podejmowania decyzji dotyczących operacji.

## <a name="continued-observation"></a>Kontynuacja obserwacji

Dane początkowe i trwająca Telemetria mogą pomóc w formułowaniu i testowaniu teorie dotyczących wydajności obciążeń. Jednak trwające operacje obciążenia są umieszczane w ciągłej i poszerzonej obserwacji wydajności obciążeń, dzięki czemu można uzyskać duży nacisk na wydajność aplikacji i danych.

### <a name="testing-automation"></a>Automatyzacja testowania

Na poziomie aplikacji pierwsze wymagania dotyczące operacji związanych z obciążeniami to inwestycja w szczegółowe testy. W przypadku dowolnej aplikacji obsługiwanej przez operacje obciążenia plan testu powinien być ustalony i regularnie wykonywany w celu dostarczenia testów funkcjonalnych i skalowalnych w aplikacjach.

Standardowe dane telemetryczne testu umożliwiają natychmiastowe sprawdzenie poprawności różnych postanowień dotyczących działania obciążenia. Udoskonalenie wzorców operacyjnych i architektonicznych mogą być wykonywane i testowane, natomiast różnica w tych wynikach zapewnia przejrzystą analizę wpływu na dalsze inwestycje.

### <a name="understand-releases"></a>Informacje o wersjach

Jasne zrozumienie cykli wydania i potoków wydań jest ważnym elementem operacji obciążenia.

Zrozumienie cykli może przygotować się do potencjalnych przerw i umożliwić zespołowi proaktywne rozwiązywanie wszelkich wydań, które mogą spowodować niekorzystny wpływ na operacje. Dzięki temu zespół zarządzający chmurą może również współdziałać z zespołami wdrażania, aby stale ulepszać jakość produktu i usterek, co może mieć wpływ na stabilność.

Co ważniejsze, zrozumienie potoków wydań może znacząco poprawić RTO obciążenia. W wielu scenariuszach najszybszą i najdokładniejszą ścieżką do odzyskiwania aplikacji jest potok wersji. W przypadku warstw aplikacji, które zmieniają się tylko wtedy, gdy występuje Nowa wersja, może być konieczne zainwestowanie w optymalizację potoku, niż Odzyskiwanie aplikacji z tradycyjnych procesów tworzenia kopii zapasowych.

Potok wdrożenia może być najszybszą ścieżką do odzyskania, ale może być również najszybszą ścieżką do skorygowania. Gdy aplikacja ma szybki, wydajny i niezawodny potok wydania, zespół zarządzający chmurą ma możliwość zautomatyzowania wdrożenia do nowego hosta jako formy zautomatyzowanego korygowania.

Może istnieć wiele innych szybszych i bardziej efektywnych mechanizmów korygowania i odzyskiwania. Jeśli jednak użycie istniejącego potoku może być zgodne z zobowiązaniami biznesowymi i kapitalizacją w istniejących inwestycjach DevOps, może to być opłacalna alternatywa.

### <a name="clearly-communicate-changes-to-the-workload"></a>Wyraźnie komunikuj zmiany w obciążeniu

Zmiany w obciążeniu należą do największych zagrożeń związanych z operacjami obciążeń. Dla każdego obciążenia na poziomie operacji obciążenia zarządzania chmurą zespół zarządzający chmurą powinien być ściśle wyrównany do zespołów wdrażania chmury, aby zrozumieć zmiany pochodzące z poszczególnych wersji. Ta inwestycja w proaktywnie rozumieniu będzie miała bezpośredni wpływ na stabilność operacyjną.

## <a name="improve-outcomes"></a>Popraw wyniki

Bieżące operacje są zwykle udoskonalone na jeden z dwóch sposobów. Inwestycje danych i komunikacji w obciążeniu dają sugestie dotyczące ulepszeń na jednej z dwóch ścieżek: zautomatyzowane korygowanie lub Udoskonalony projekt systemu

### <a name="technical-debt-resolution"></a>Rozwiązywanie długów technicznych

Najlepsze plany operacji obciążenia nadal wymagają korygowania. Gdy zespół zarządzający chmurą dąży do pozostawania w kontakcie, aby poznać wysiłki i wydania dotyczące wdrożenia, podobnie jak zespół powinien regularnie udostępniać wymagania naprawcze w celu zapewnienia długu technicznego, a usterki są nadal priorytetem dla zespołów programistycznych.

### <a name="automate-remediation"></a>Automatyzacja korygowania

Zastosowanie zasady Pareto, 80% negatywnego wpływu na działalność, najkorzystniej z 20% zdarzeń usługi. Gdy nie można rozesłać tych zdarzeń w normalnych cyklach programistycznych, inwestycje w automatyzację korygującą mogą znacząco obniżyć liczbę przerw w działaniu firmy.

### <a name="improved-system-design"></a>Udoskonalony projekt systemu

W każdym przypadku (Rozwiązywanie długów technicznych lub automatyczne korygowanie) wady systemu są częstą przyczyną większości awarii systemu. Przestrzeganie kilku zasad projektowania może mieć największy wpływ na ogólne operacje związane z obciążeniem.

1. Skalowalność: zdolność systemu do obsługi zwiększonego obciążenia.
2. Dostępność: okres, w którym system jest funkcjonalny i działa.
3. Odporność: zdolność systemu do odzyskiwania sprawności po awarii i kontynuowania działania.
4. Zarządzanie: procesy operacji, które przechowują system w środowisku produkcyjnym.
5. Zabezpieczenia: Ochrona aplikacji i danych przed zagrożeniami.

Platforma [architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) oferuje podejście do oceny konkretnych obciążeń związanych z przystąpieniem do tych filarów, w celu poprawy ogólnych operacji. Te filary mogą być stosowane do operacji na platformie i operacji związanych z obciążeniami.

## <a name="next-steps"></a>Następne kroki

Mając pełną wiedzę na temat zarządzania metodologią w ramach platformy wdrażania w chmurze, można już zaimplementować zasady zarządzania chmurą. Zapoznaj się ze stroną docelową [dla fazy zarządzania](../index.md) cyklem życia wdrożenia, aby uzyskać wskazówki dotyczące podejmowania tej metodologii w środowisku operacji.

> [!div class="nextstepaction"]
> [Zastosuj tę metodologię](../index.md)
