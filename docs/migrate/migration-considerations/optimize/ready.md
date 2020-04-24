---
title: Przygotowanie zmigrowanej aplikacji do podwyższenia poziomu środowiska produkcyjnego
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać sprawdzanie poprawności, która dotyczy przygotowania zmigrowanej aplikacji do podwyższania poziomu produkcji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2ad912c7bc2e61465a81e278714f5018c2373f7f
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80429231"
---
# <a name="prepare-a-migrated-application-for-production-promotion"></a>Przygotowanie zmigrowanej aplikacji do podwyższenia poziomu środowiska produkcyjnego

Po podwyższeniu poziomu obciążenia ruch użytkowników w środowisku produkcyjnym zostaje skierowany do zmigrowanych zasobów. Działania w zakresie gotowości zapewniają możliwość przygotowania obciążenia do tego ruchu. Poniżej przedstawiono kilka kwestii branżowych i technologicznych, które ułatwią działania w zakresie gotowości.

## <a name="validate-the-business-change-plan"></a>Walidacja planu zmian biznesowych

Przekształcanie ma miejsce, gdy użytkownicy biznesowi lub klienci wykorzystują rozwiązanie techniczne do wykonywania procesów umożliwiających prowadzenie działalności. Gotowość stanowi doskonałą okazję do walidacji [planu zmian biznesowych](./business-change-plan.md) oraz zagwarantowania odpowiedniego przeszkolenia zaangażowanych zespołów biznesowych i technicznych. W szczególności należy się upewnić, czy zostały prawidłowo przekazane następujące kwestie techniczne dotyczące planu zmian:

- Odbyło się szkolenie dla użytkowników końcowych (lub przynajmniej zostało zaplanowane).
- Wszystkie okna awarii zostały przekazane i zatwierdzone.
- Dane produkcyjne zostały zsynchronizowane i sprawdzone przez użytkowników końcowych.
- Sprawdź czas podwyższenia poziomu i wdrożenia; upewnij się, że osie czasu oraz zmiany zostały przekazane użytkownikom końcowym.

## <a name="final-technical-readiness-tests"></a>Końcowe testy gotowości technicznej

*Faza gotowości* jest ostatnim krokiem przed wydaniem produkcyjnym. Oznacza to, że jest to również ostatnia okazja do przetestowania obciążenia. Poniżej przedstawiono kilka testów sugerowanych w tej fazie:

- **Testowanie izolacji sieciowej.** Przetestuj i monitoruj ruch sieciowy, aby zapewnić odpowiednią izolację oraz zagwarantować, że nie będzie nieoczekiwanych luk w zabezpieczeniach sieci. Upewnij się również, że żaden routing sieciowy, który ma zostać odcięty podczas uruchomienia produkcyjnego, nie obejmuje nieoczekiwanego ruchu.
- **Testowanie zależności.** Upewnij się, że wszystkie zależności aplikacji obciążenia zostały zmigrowane i są dostępne ze zmigrowanych zasobów.
- **Testowanie ciągłości działania i odzyskiwania po awarii (BCDR).** Sprawdź, czy zostały ustanowione wszystkie umowy SLA dotyczące kopii zapasowych i odzyskiwania po awarii. Jeśli to możliwe, wykonaj pełne odzyskiwanie zasobów z rozwiązania BCDR.
- **Testowanie trasy przez użytkownika końcowego.** Sprawdź wzorce ruchu i routing dla ruchu użytkowników końcowych. Upewnij się, że wydajność sieci jest zgodna z oczekiwaniami.
- **Końcowe sprawdzenie wydajności.** Upewnij się, że testy wydajności zostały ukończone i zatwierdzone przez użytkowników końcowych. Wykonaj wszystkie automatyczne testy wydajności.

## <a name="final-business-validation"></a>Końcowa walidacja pod kątem biznesowym

Po sprawdzeniu poprawności planu zmian w firmie i gotowości technicznej proces walidacji biznesowej należy zakończyć wykonując następujące czynności:

- **Sprawdzenie kosztów (plan a stan faktyczny).** Testowanie może spowodować powstanie zmian w ustalaniu wielkości i architektury. Upewnij się, że faktyczne ceny wdrożenia nadal odpowiadają oryginalnemu planowi.
- **Przekazanie i wykonanie planu uruchomienia produkcyjnego.** Przed uruchomieniem produkcyjnym poinformuj o nim, a następnie wykonaj odpowiednie instrukcje.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu wszystkich działań w zakresie gotowości nadszedł czas na [podwyższenie poziomu obciążenia](./promote.md).

> [!div class="nextstepaction"]
> [Jakie wymagania należy spełnić, aby podwyższyć poziom zmigrowanego zasobu do środowiska produkcyjnego?](./promote.md)
