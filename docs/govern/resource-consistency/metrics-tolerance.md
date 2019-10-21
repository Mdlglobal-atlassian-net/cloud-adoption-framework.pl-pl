---
title: Metryki spójności zasobów, wskaźniki i tolerancja ryzyka
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Metryki spójności zasobów, wskaźniki i tolerancja ryzyka
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2a6f59c09533fc400871d549e32c9b7d56024551
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548070"
---
# <a name="resource-consistency-metrics-indicators-and-risk-tolerance"></a>Metryki spójności zasobów, wskaźniki i tolerancja ryzyka

Ten artykuł pomoże Ci określić tolerancję ryzyka biznesowego, która odnosi się do spójności zasobów. Zdefiniowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy do składania inwestycji w celu wykupu dyscypliny spójności zasobów.

## <a name="metrics"></a>Metryki

Dyscyplina spójności zasobów koncentruje się na rozwiązywaniu zagrożeń związanych z zarządzaniem operacyjnymi wdrożeń w chmurze. W ramach analizy ryzyka warto zebrać dane związane z operacjami IT, aby określić, jakie ryzyko ma być narażone, oraz jak ważne inwestycje w zarządzanie spójnością zasobów to planowane wdrożenia w chmurze.

Każda organizacja ma inne scenariusze operacyjne, ale następujące elementy stanowią przydatne przykłady metryk, które należy zebrać podczas oceny tolerancji ryzyka w dyscyplinie spójności zasobów:

- **Zasoby w chmurze.** Łączna liczba zasobów wdrożonych w chmurze.
- **Nieoznaczone zasoby.** Liczba zasobów bez wymaganej księgowości, wpływu na działalność lub Tagi organizacyjne.
- **Nieużywane zasoby.** Liczba zasobów, w przypadku których wszystkie możliwości pamięci, procesora lub sieci są stale niedostateczne.
- **Wyczerpanie zasobów.** Liczba zasobów, w przypadku których obciążenie pamięci, procesora lub sieci są wyczerpane.
- **Wiek zasobu.** Czas od ostatniego wdrożenia lub modyfikacji zasobu.
- **Maszyny wirtualne w warunku krytycznym.** Liczba wdrożonych maszyn wirtualnych, w których wykryto co najmniej jeden krytyczny problem, który należy rozwiązać, aby przywrócić normalne funkcje.
- **Alerty według ważności.** Łączna liczba alertów dla wdrożonego elementu zawartości podzielona według ważności.
- **Linki sieci w złej kondycji.** Liczba zasobów z problemami z łącznością sieciową.
- **Punkty końcowe usługi w złej kondycji.** Liczba problemów z punktami końcowymi sieci zewnętrznych.
- **Zdarzenia dotyczące kondycji usługi dostawcy chmury.** Liczba zakłóceń lub zdarzeń wydajności spowodowanych przez dostawcę chmury.
- **Umowy dotyczące poziomu usług.** Może to obejmować zobowiązania firmy Microsoft dotyczące czasu przestoju i łączności usług platformy Azure, a także zobowiązania podejmowane przez firmę klientom zewnętrznym i wewnętrznym.
- **Dostępność usługi.** Procent rzeczywistych obciążeń hostowanych w chmurze w porównaniu z oczekiwanym przestojem.
- **Cel czasu odzyskiwania (RTO).** Maksymalny akceptowalny czas, przez jaki aplikacja może być niedostępna po zdarzeniu.
- **Cel punktu odzyskiwania (RPO).** Maksymalny czas trwania utraty danych, który jest akceptowalny podczas awarii. Jeśli na przykład przechowujesz dane w pojedynczej bazie danych bez replikacji do innych baz danych i co godzinę wykonujesz kopię zapasową, możesz stracić nawet godzinę danych.
- **Średni czas do odzyskania (MTTR).** Średni czas wymagany do przywrócenia składnika po awarii.
- **Średni czas między błędami (MTBF).** Czas, przez jaki składnik może oczekiwać na uruchomienie między przestojem. Ta Metryka może pomóc w obliczeniu, jak często usługa stanie się niedostępna.
- **Kondycja kopii zapasowej.** Liczba kopii zapasowych aktywnie zsynchronizowanych.
- **Kondycja odzyskiwania.** Liczba pomyślnie wykonanych operacji odzyskiwania.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

Platformy w chmurze oferują podstawowy zestaw funkcji, które umożliwiają zespołom wdrożenia efektywne zarządzanie małymi wdrożeniami bez konieczności dodatkowego planowania i procesów. W efekcie małe tworzenie/testowanie lub eksperymentalne pierwsze obciążenia, które obejmują stosunkowo małą ilość zasobów opartych na chmurze, reprezentują niski poziom ryzyka i prawdopodobnie nie będą potrzebne w drodze formalnych zasad spójności zasobów.

Jednak w miarę wzrostu rozmiaru chmury w celu zarządzania zasobami staje się znacznie trudniejsze. Dzięki większej liczbie zasobów w chmurze zdolność do określania własności zasobów i zasobów kontroli jest istotna dla minimalizowania zagrożeń. Ponieważ coraz więcej obciążeń o znaczeniu krytycznym są wdrażane w chmurze, czas działania usługi stanie się bardziej krytyczny, a odporność na przerwy w obciążeniu usługi nie zmniejsza się szybko.

We wczesnych etapach wdrażania chmury Pracuj z zespołem ds. operacji IT oraz zainteresowanymi stronami biznesowymi, aby identyfikować [zagrożenia biznesowe](./business-risks.md) związane ze spójnością zasobów, a następnie określić akceptowalną podstawę do odporności na ryzyko. W tej części struktury wdrażania w chmurze przedstawiono przykłady, ale szczegóły dotyczące zagrożeń i linii bazowych dla firmy lub wdrożeń mogą się różnić.

Po utworzeniu planu bazowego należy ustanowić minimalne wzorce reprezentujące nieakceptowalny wzrost w zidentyfikowanych zagrożeniach. Te progi działają jako Wyzwalacze w przypadku, gdy konieczne jest podjęcie działań w celu skorygowania tych zagrożeń. Poniżej przedstawiono kilka przykładów sposobu, w jaki metryki operacyjne, takie jak te omówione powyżej, mogą uzasadniać zwiększenie inwestycji w dyscyplinę spójności zasobów.

- **Tagowanie i wyzwalacz nazewnictwa.** Firma z więcej niż _x_ zasobami nie wymaga informacji o znakowaniu lub nie przestrzega zgodności ze standardami nazewnictwa, należy rozważyć inwestowanie w dyscyplinę spójności zasobów, aby pomóc w zapewnieniu zgodności ze standardami i zapewnić spójność ich stosowania zasoby wdrożone w chmurze.
- **Wyzwalacz zasobów o nadmiernej aprowizacji.** Jeśli firma ma więcej niż _x%_ zasobów regularnie przy użyciu niewielkich ilości dostępnych pamięci, procesora lub sieci, inwestycje w dyscyplinę spójności zasobów są sugerowane w celu zoptymalizowania użycia zasobów dla tych elementów.
- **Wyzwalacz nadmiernie zainicjowanych zasobów.** Jeśli firma ma więcej niż _x%_ zasobów, regularne wyczerpanie większości dostępnych możliwości pamięci, procesora lub sieci, inwestycje w dyscyplinę spójności zasobów są sugerowane w celu zapewnienia, że zasoby te są niezbędne do zapobiegania przerwy w świadczeniu usług.
- **Wyzwalacz wieku zasobu.** Firma z więcej niż _x_ zasobami, które nie zostały zaktualizowane _w ciągu kilku_ miesięcy, może skorzystać z inwestycji w dyscyplinę spójności zasobów, której celem jest zapewnienie, że aktywne zasoby są w dobrej kondycji, a jednocześnie wycofane z przestarzałych lub Inne nieużywane zasoby.
- **Wyzwalacz umowy dotyczącej poziomu usług.** Firma, która nie może spełnić swoich umów dotyczących poziomu usług klientom zewnętrznym ani partnerom wewnętrznym, powinna inwestować w dyscyplinę wdrożenia w celu zmniejszenia przestojów systemu.
- **Wyzwalacze czasu odzyskiwania.** W przypadku przekroczenia przez firmę wymaganych progów czasu odzyskiwania po awarii systemu należy zainwestować w udoskonalenie projektu dyscypliny i systemów przyspieszenia wdrożenia w celu ograniczenia lub wyeliminowania błędów lub skutku przestoju poszczególnych składników.
- **Wyzwalacz kondycji maszyny wirtualnej.** Firma, która ma więcej niż _x%_ maszyn wirtualnych, na których występuje krytyczny problem z kondycją, powinna inwestować w dyscyplinę spójności zasobów, aby zidentyfikować problemy i zwiększyć stabilność maszyny wirtualnej.
- **Wyzwalacz kondycji sieci.** Firma mająca więcej niż _x%_ podsieci sieciowych lub punktów końcowych, w których występują problemy z łącznością, powinna inwestować w dyscyplinę spójności zasobów w celu identyfikowania i rozwiązywania problemów z siecią.
- **Wyzwalacz pokrycia kopii zapasowej.** Firma z zasobami o znaczeniu strategicznym ( _x%)_ bez aktualnych kopii zapasowych w miejscu może korzystać z zwiększonej nakładu pracy w dyscyplinie spójności zasobów, aby zapewnić spójną strategię tworzenia kopii zapasowych.
- **Wyzwalacz kondycji kopii zapasowej.** Firma mająca więcej niż _x%_ awarii operacji przywracania powinna inwestować w dyscyplinę spójności zasobów, aby zidentyfikować problemy związane z tworzeniem kopii zapasowych i zapewnić ochronę ważnych zasobów.

Dokładne metryki i wyzwalacze służące do oceny tolerancji ryzyka i poziom inwestycji w dyscyplinie spójności zasobów będą specyficzne dla organizacji, ale powyższe przykłady powinny służyć jako przydatny dla dyskusji w ramach ładu w chmurze. Dział.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), metryk dokumentu i wskaźniki tolerancji, które są wyrównane do bieżącego planu wdrożenia chmury.

Zapoznaj się z przykładowymi zasadami spójności zasobów jako punktem początkowym w celu opracowania zasad, które wiążą się z określonymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania chmury

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
