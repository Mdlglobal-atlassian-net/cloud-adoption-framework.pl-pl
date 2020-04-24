---
title: Definiowanie architektury obciążeń przed migracją
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak zdefiniować nową architekturę przed rozpoczęciem migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e5211d263e2833b8cef41d3f8b3cc1d709b89d39
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80432904"
---
# <a name="architect-workloads-prior-to-migration"></a>Definiowanie architektury obciążeń przed migracją

Ten artykuł rozszerza proces oceny i zawiera przegląd działań związanych z definiowaniem architektury obciążeń w ramach danej iteracji. Jak opisano w artykule poświęconym [racjonalizacji przyrostowej](../../../digital-estate/rationalize.md), podczas każdej transformacji firmy, która wymaga migracji, przyjmowane są pewne założenia dotyczące architektury. W tym artykule wyjaśniono te założenia, przedstawiono kilka problemów, których można uniknąć, i zidentyfikowano możliwości przyspieszenia osiągnięcia wartości biznesowej przez zweryfikowanie tych założeń. Ten przyrostowy model architektury umożliwia zespołom szybsze działanie i uzyskanie wyników biznesowych.

## <a name="architecture-assumptions-prior-to-migration"></a>Założenia dotyczące architektury przed migracją

Następujące założenia są typowe dla dowolnego procesu migracji:

- **IaaS.** Często zakłada się, że migrowanie obciążeń obejmuje głównie przeniesienie maszyn wirtualnych z fizycznego centrum danych do centrum danych w chmurze za pomocą migracji IaaS, wymagając minimalnej przebudowy lub rekonfiguracji. Jest to tzw. Migracja _i przesunięcia_ . (Wyjątki przedstawiono w dalszej części artykułu).
- **Spójność architektury.** Zmiany w architekturze podstawowej podczas migracji znacząco zwiększają złożoność. Debugowanie zmienionego systemu na nowej platformie wprowadza wiele zmiennych, które mogą być trudne do izolowania. Z tego powodu obciążenia powinny być poddawane tylko drobnym zmianom podczas migracji, a wszelkie zmiany powinny być dokładnie przetestowane.
- **Test wycofania.** Migracje i hosting zasobów wiążą się z wydatkami operacyjnymi i potencjalnymi nakładami inwestycyjnymi. Przyjmuje się założenie, że wszystkie migrowane obciążenia zostały sprawdzone w celu zweryfikowania ciągłego użycia. Wycofanie nieużywanych zasobów zapewnia natychmiastowe oszczędności.
- **Zmiana rozmiaru zasobów.** Zakłada się, że niewiele zasobów lokalnych w pełni wykorzystuje przydzielone zasoby. Przed migracją przyjmuje się założenie, że rozmiar zasobów zostanie zmieniony w celu najlepszego dopasowania do rzeczywistych wymagań dotyczących użycia.
- **Wymagania dotyczące ciągłości działania i odzyskiwania po awarii (BCDR).** Zakłada się, że ustalona umowa SLA dotycząca obciążenia została wynegocjowana z firmą przed rozpoczęciem planowania wydania. Te wymagania prawdopodobnie spowodują wygenerowanie drobnych zmian architektury.
- **Przestój podczas migracji.** Podobnie przestój w celu podwyższenia poziomu obciążenia do produkcyjnego może mieć niekorzystny wpływ na działalność firmy. Czasami rozwiązania, które muszą przejść z minimalnym przestojem, wymagają zmiany architektury. Zakłada się, że przed planowaniem wydania ustanowiono ogólną interpretację wymagań dotyczących przestoju.

## <a name="roadblocks-that-can-be-avoided"></a>Przeszkody, których można uniknąć

Wymienione powyżej założenia mogą stwarzać przeszkody spowalniające postępy lub powodujące późniejsze problemy. Poniżej wskazano kilka przeszkód, które należy obserwować przed wydaniem:

- **Płacenie za dług techniczny.** Niektóre starsze obciążenia niosą ze sobą duży dług techniczny. Może to prowadzić do długoterminowych wyzwań, zwiększając koszty hostingu dla każdego dostawcy usług w chmurze. Gdy dług techniczny nienaturalnie zwiększa koszty hostingu, należy ocenić alternatywne architektury.
- **Wzorce ruchu użytkownika.** Istniejące rozwiązania mogą zależeć od istniejących wzorców routingu sieciowego. Te wzorce mogą powodować znaczne obniżenie wydajności. Ponadto wprowadzenie nowych hybrydowych rozwiązań sieci rozległej (WAN) może zająć kilka tygodni, a nawet miesięcy. Na wczesnym etapie procesu definiowania architektury należy przygotować się na te przeszkody przez rozważenie wzorców ruchu i zmian usług infrastruktury podstawowej.

## <a name="accelerate-business-value"></a>Przyspieszenie wartości biznesowej

Niektóre scenariusze mogą wymagać innej architektury niż przyjęta strategia ponownego hostingu przy użyciu usługi IaaS. Poniżej przedstawiono kilka przykładów:

- Alternatywy PaaS. Wdrożenia PaaS mogą obniżyć koszty hostingu i skrócić czas wymagany do przeprowadzenia migracji pewnych obciążeń. Aby zapoznać się z listą podejść, które mogą skorzystać z konwersji PaaS, zobacz artykuł dotyczący [oceniania zasobów](./evaluate.md).
- Wdrożenia inicjowane przez skrypty/DevOps. Jeśli obciążenie ma istniejące wdrożenie DevOps lub inne formy wdrożenia inicjowanego przez skrypt, koszt zmiany tych skryptów może być niższy niż koszt migracji zasobu.
- Działania korygujące. Działania korygujące wymagane do przygotowania obciążenia do migracji mogą wiązać się z dużym nakładem pracy. W niektórych przypadkach lepiej jest zmodernizować rozwiązanie niż korygować podstawowe problemy ze zgodnością.

W każdym z wyżej wymienionych scenariuszy alternatywna architektura może być najlepszym możliwym rozwiązaniem.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu nowej architektury można obliczyć [dokładne oszacowania kosztów](./estimate.md).

> [!div class="nextstepaction"]
> [Szacowanie kosztów chmury](./estimate.md)
