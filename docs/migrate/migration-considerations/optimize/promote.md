---
title: Wymagania dotyczące podniesienia poziomu zmigrowanego zasobu do środowiska produkcyjnego
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać typowe zadania i standardowe wymagania wstępne dotyczące promowania zmigrowanego zasobu do środowiska produkcyjnego.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: dc67072e80cc752a1167ad453a56fd96f6890874
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219244"
---
<!-- cSpell:ignore CISO -->

<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Jakie wymagania należy spełnić, aby podwyższyć poziom zmigrowanego zasobu do środowiska produkcyjnego?

Promocja do produkcji oznacza zakończenie migracji obciążenia do chmury. Po podwyższeniu poziomu zasobu i wszystkich jego zależności ruch produkcyjny zostanie przekierowany. Przekierowanie ruchu powoduje, że zasoby lokalne stają się niepotrzebne, co umożliwia ich wycofanie.

Proces podwyższania poziomu różni się w zależności od architektury obciążenia. Istnieje jednak kilka spójnych wymagań wstępnych i kilka typowych zadań. W tym artykule opisano każdy z nich i służy jako rodzaj listy kontrolnej przed promocją.

## <a name="prerequisite-processes"></a>Procesy wymagane wstępnie

Każdy z następujących procesów należy wykonać, udokumentować i sprawdzić przed wdrożeniem w środowisku produkcyjnym:

- ** [Oceń](../assess/index.md):** Obciążenie zostało ocenione pod kątem zgodności z chmurą.
- ** [Architekt](../assess/architect.md):** Struktura obciążenia została prawidłowo zaprojektowana tak, aby była wyrównana do wybranego dostawcy chmury.
- ** [Replikacja](../migrate/replicate.md):** Zasoby zostały zreplikowane do środowiska chmury.
- ** [Etap](../migrate/stage.md):** Zreplikowane zasoby zostały przywrócone w przygotowanym wystąpieniu środowiska chmury.
- ** [Testowanie biznesowe](./business-test.md):** Obciążenie zostało w pełni przetestowane i sprawdzone przez użytkowników firmy.
- ** [Plan zmiany firmy](./business-change-plan.md):** Firma udostępniła Plan wprowadzania zmian zgodnie z promocją produkcyjną. powinno to obejmować plan wdrażania użytkowników, zmiany w procesach biznesowych, użytkowników, którzy wymagają szkoleń, oraz osi czasu dla różnych działań.
- ** [Gotowe](./ready.md):** Ogólnie rzecz biorąc, przed podwyższeniem poziomu należy wprowadzić serię zmian technicznych.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Najlepsze rozwiązania, które należy zastosować przed podwyższeniem poziomu

Następujące zmiany techniczne będą prawdopodobnie musiały zostać wprowadzone i udokumentowane jako część procesu podwyższania poziomu:

- **Wyrównanie domen** Niektóre zasady firmowe wymagają oddzielnych domen do przygotowania i produkcji. Upewnij się, że wszystkie zasoby są przyłączone do właściwej domeny.
- **Routing użytkowników** Sprawdź, czy użytkownicy uzyskują dostęp do obciążenia za pomocą odpowiednich tras sieciowych. Sprawdź spójność oczekiwań dotyczących wydajności.
- **Wyrównanie tożsamości** Sprawdź, czy użytkownicy przekierowani do aplikacji mają odpowiednie uprawnienia w domenie, aby móc hostować aplikację.
- **Skuteczności.** Wykonaj ostateczną walidację wydajności obciążeń, aby zminimalizować nieprzewidziane sytuacje.
- **Walidacja ciągłości działania i odzyskiwania po awarii** Upewnij się, że odpowiednie procesy tworzenia kopii zapasowych i odzyskiwania działają zgodnie z oczekiwaniami.
- **Klasyfikacja danych.** Sprawdź poprawność klasyfikacji danych, aby się upewnić, że wdrożono odpowiednie zabezpieczenia i zasady.
- **Weryfikacja przez głównego specjalistę ds. zabezpieczeń informacji (CISO)** Upewnij się, że specjalista ds. zabezpieczeń informacji sprawdził obciążenie, ryzyko biznesowe, tolerancję ryzyka i strategie zaradcze.

## <a name="final-step-promote"></a>Ostatni krok: Podnieś poziom

Obciążenia będą wymagały różnych poziomów szczegółowych przeglądów i procesów podwyższania poziomu. Jednak ponowne wyrównanie sieci jest wspólnym krokiem końcowym dla wszystkich wydań związanych z podwyższeniem poziomu. Gdy wszystko jest gotowe, zaktualizuj rekordy DNS lub adresy IP w celu przekierowania ruchu do zmigrowanego obciążenia.

## <a name="next-steps"></a>Następne kroki

Podwyższenie poziomu obciążenia sygnalizuje ukończenie wydania. Jednak równolegle z migracją wycofane zasoby muszą zostać [zlikwidowane](./decommission.md) i wycofane z użycia.

> [!div class="nextstepaction"]
> [Likwidowanie wycofanych zasobów](./decommission.md)
