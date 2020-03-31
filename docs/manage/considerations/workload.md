---
title: Operacje na obciążeniach w zarządzaniu chmurą
description: Zapoznaj się z podejściem do inwestowania w ciągłe operacje tych obciążeń o wysokim priorytecie, aby zwiększyć zobowiązania biznesowe.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 92453f3323a2479160bd7bd45e6ef5101c1d9f1b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430131"
---
# <a name="workload-operations-in-cloud-management"></a>Operacje na obciążeniach w zarządzaniu chmurą

Niektóre obciążenia mają kluczowe znaczenie dla sukcesu firmy. W przypadku tych obciążeń linia bazowa zarządzania jest niewystarczająca, aby zaspokoić wymagane zobowiązania biznesowe do zarządzania chmurą. Operacje na platformie mogą jeszcze nie być wystarczające, aby zaspokoić zobowiązania biznesowe. Ten wysoce istotny podzbiór obciążeń wymaga wyspecjalizowanego skoncentrowania się na sposobie działania obciążeń i sposobu ich obsługi.

W powrocie operacje związane z obciążeniem mogą prowadzić do zwiększenia wydajności, zmniejszenia ryzyka zakłócenia działania firmy oraz szybszego odzyskiwania w przypadku wystąpienia awarii systemu. W tym artykule omówiono podejście do inwestowania w ciągłe operacje tych obciążeń o wysokim priorytecie, aby zwiększyć zobowiązania biznesowe.

## <a name="when-to-invest-in-workload-operations"></a>Kiedy inwestować w operacje obciążeń

_Zasada wykresu Pareto_ (znana także jako _reguła 80/20_) określa, że 80 procent efektów pochodzi z 20 procent przyczyn. Gdy portfolio IT można zwiększyć organicznie w miarę upływu czasu, ta zasada jest często zilustrowana w przeglądzie portfolio IT. W zależności od efektu, który wymaga inwestycji, przyczyny mogą się różnić, ale ogólna zasada ma wartość PRAWDA:

- 80 procent błędów systemu jest wynikiem 20 procent typowych błędów lub usterek.
- 80 procent wartości biznesowej jest wynikiem 20 procent obciążeń w portfolio.
- 80 procent wysiłku związanego z migracją do chmury pochodzi z 20% obciążeń, które są przenoszone.
- 80 procent działań związanych z zarządzaniem chmurą będzie obsługiwać 20% zdarzeń usługi lub biletów problemów.
- 80 procent wpływu działania firmy na awarię będzie pochodzić z 20% systemów, na które wpływa awaria.

Operacje obciążeń powinny być stosowane tylko wtedy, gdy strategia wdrażania chmury, wyniki biznesowe i metryki operacyjne są dobrze zrozumiałe. Jest to zmiana modelu z klasycznego widoku IT. Tradycyjnie zakłada się, że wszystkie obciążenia miały ten sam stopień wsparcia i wymagają podobnych poziomów priorytetów.

Przed zainwestowaniem w szczegółowe operacje obciążeń zarówno IT, jak i biznesowe powinny zrozumieć uzasadnienie biznesowe i oczekiwania na zwiększenie inwestycji w zarządzanie chmurą.

## <a name="start-with-the-data"></a>Zacznij od danych

Operacje związane z obciążeniem rozpoczynają się od dokładnego poznania wydajności obciążeń i wymagań dotyczących obsługi. Zanim zespół zacznie inwestować w operacje związane z obciążeniem, musi mieć bogate dane dotyczące zależności obciążenia, wydajności aplikacji, diagnostyki baz danych, telemetrii maszyny wirtualnej i historii zdarzeń.

Te dane są przeznaczone do uzyskiwania informacji, które są przeznaczone do podejmowania decyzji dotyczących operacji.

## <a name="continued-observation"></a>Kontynuacja obserwacji

Dane początkowe i trwająca Telemetria mogą pomóc w formułowaniu i przetestowaniu teorie o wydajności obciążeń. Jednak trwające operacje obciążenia są umieszczane w ciągłej i rozszerzonej obserwacji wydajności obciążeń, dzięki czemu można skupić się na wydajności aplikacji i danych.

### <a name="test-the-automation"></a>Testowanie automatyzacji

Na poziomie aplikacji pierwsze wymagania dotyczące operacji związanych z obciążeniami to inwestycja w szczegółowe testy. Dla każdej aplikacji, która jest obsługiwana za pośrednictwem operacji obciążenia, należy nawiązać plan testu i regularnie go wykonać w celu dostarczenia testów funkcjonalnych i skalowalnych w aplikacjach.

Regularne testy telemetryczne mogą zapewnić natychmiastowe sprawdzenie różnych postanowień związanych z działaniem obciążenia. Ulepszanie wzorców operacyjnych i architektury może być wykonywane i testowane. Wynikowe różnicy zapewniają wyraźną analizę wpływu na dalsze inwestycje.

### <a name="understand-releases"></a>Informacje o wersjach

Dokładne zrozumienie cykli wydania i potoków wydań jest ważnym elementem operacji obciążenia.

Zrozumienie cykli może przygotować się do potencjalnych przerw i umożliwić zespołowi proaktywne rozwiązanie wszelkich wydań, które mogą spowodować niekorzystny wpływ na operacje. Dzięki temu zespół zarządzający chmurą może również współdziałać z zespołami wdrażania, aby stale ulepszać jakość produktu i rozwiązywać wszelkie usterki, które mogą mieć wpływ na stabilność.

Co ważniejsze, zrozumienie potoków wydań może znacząco poprawić cel punktu odzyskiwania (RPO) obciążenia. W wielu scenariuszach najszybszą i najdokładniejszą ścieżką do odzyskiwania aplikacji jest potok wersji. W przypadku warstw aplikacji, które zmieniają się tylko wtedy, gdy występuje Nowa wersja, może być konieczne zainwestowanie w optymalizację potoku niż w przypadku odzyskiwania aplikacji z tradycyjnych procesów tworzenia kopii zapasowych.

Mimo że potok wdrożenia może być największą ścieżką do odzyskania, może być również najszybszą ścieżką do skorygowania. Gdy aplikacja ma szybki, wydajny i niezawodny potok wydania, zespół zarządzający chmurą ma możliwość zautomatyzowania wdrożenia do nowego hosta jako formy zautomatyzowanego korygowania.

Może istnieć wiele innych szybszych i bardziej efektywnych mechanizmów korygowania i odzyskiwania. Jeśli jednak użycie istniejącego potoku może być zgodne z zobowiązaniami biznesowymi i kapitalizacją w istniejących inwestycjach DevOps, istniejący potok może być rozwiązaniem alternatywnym.

### <a name="clearly-communicate-changes-to-the-workload"></a>Wyraźnie komunikuj zmiany w obciążeniu

Zmiany w obciążeniu należą do największych zagrożeń związanych z operacjami obciążeń. W przypadku dowolnego obciążenia na poziomie operacji obciążenia zarządzania chmurą zespół zarządzający chmurą powinien dokładnie dostosować się do zespołów wdrażania chmury, aby zrozumieć zmiany pochodzące z poszczególnych wersji. Ta inwestycja w proaktywnie rozumieniu będzie miała bezpośredni pozytywny wpływ na stabilność operacyjną.

## <a name="improve-outcomes"></a>Popraw wyniki

Inwestycje danych i komunikacji w obciążeniu będą zwracać sugestie dotyczące ulepszeń operacji w ramach jednego z trzech obszarów:

- Rozwiązywanie długów technicznych
- Zautomatyzowane korygowanie
- Udoskonalony projekt systemu

### <a name="technical-debt-resolution"></a>Rozwiązywanie długów technicznych

Najlepsze plany operacji obciążenia nadal wymagają korygowania. Ponieważ zespół zarządzający chmurą dąży do poprawienia problemów z wdrażaniem i wydaniami, zespół powinien regularnie przekazywać wymagania naprawcze w celu zapewnienia, że zadłużenie techniczne i usterki są ciągłym priorytetem dla zespołów programistycznych.

### <a name="automated-remediation"></a>Zautomatyzowane korygowanie

Stosując zasadę wykresu Pareto, możemy powiedzieć, że 80 procent ujemnego wpływu na działalność może wynikać z 20% zdarzeń usługi. Gdy nie można rozesłać tych zdarzeń w normalnych cyklach programistycznych, inwestycje w automatyzację korygującą mogą znacząco obniżyć liczbę przerw w działaniu firmy.

### <a name="improved-system-design"></a>Udoskonalony projekt systemu

W przypadku rozwiązywania długów technicznych i zautomatyzowanego korygowania wady systemu są typową przyczyną większości awarii systemu. Możesz mieć największy wpływ na ogólne operacje obciążeń, przestrzegając kilku zasad projektowania:

- **Skalowalność:** Zdolność systemu do obsługi zwiększonego obciążenia.
- **Dostępność:** Procent czasu, przez który system jest funkcjonalny i działa.
- **Odporność:** Zdolność systemu do odzyskiwania sprawności po awarii i kontynuowania działania.
- **Zarządzanie:** Procesy operacji, które przechowują system w środowisku produkcyjnym.
- **Zabezpieczenia:** Ochrona aplikacji i danych przed zagrożeniami.

Aby pomóc w ulepszaniu ogólnych operacji, Platforma [architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) zapewnia podejście do oceny konkretnych obciążeń do przystąpienia do tych filarów. Można zastosować filary mogą być stosowane do operacji na platformie i operacji obciążeń.

## <a name="next-steps"></a>Następne kroki

Mając pełną wiedzę na temat zarządzania metodologią w ramach platformy wdrażania w chmurze, można już zaimplementować zasady zarządzania chmurą. Aby uzyskać wskazówki dotyczące podejmowania tej metodologii w środowisku operacji, zobacz [zarządzanie chmurą w strukturze wdrożenia chmury w](../index.md) cyklu życia.

> [!div class="nextstepaction"]
> [Zastosuj tę metodologię](../index.md)
