---
title: Jakie wymagania należy spełnić, aby podwyższyć poziom zmigrowanego zasobu do środowiska produkcyjnego?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proces migracji w chmurze, który koncentruje się na zadaniach migrowania obciążeń do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb025eacb7743f470b15e2714ed65a05c21034a1
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825473"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>Jakie wymagania należy spełnić, aby podwyższyć poziom zmigrowanego zasobu do środowiska produkcyjnego?

Podwyższenie poziomu do środowiska produkcyjnego oznacza zakończenie migracji obciążenia do chmury. Po podwyższeniu poziomu zasobu i wszystkich jego zależności ruch produkcyjny zostanie przekierowany. Przekierowanie ruchu powoduje, że zasoby lokalne stają się niepotrzebne, co umożliwia ich wycofanie.

Proces podwyższania poziomu różni się w zależności od architektury obciążenia. Istnieje jednak kilka spójnych wymagań wstępnych i kilka typowych zadań. W tym artykule opisano każde z nich i służy on jako rodzaj listy kontrolnej przed podwyższeniem poziomu.

## <a name="prerequisite-processes"></a>Procesy wymagane wstępnie

Każdy z następujących procesów należy wykonać, udokumentować i sprawdzić przed wdrożeniem w środowisku produkcyjnym:

- **[Ocena](../assess/index.md):** Obciążenie zostało ocenione pod kątem zgodności z chmurą.
- **[Tworzenie architektury](../assess/architect.md):** Struktura obciążenia została prawidłowo zaprojektowana w celu jej dostosowania do wybranego dostawcy usług w chmurze.
- **[Replikacja](../migrate/replicate.md):** Zasoby zostały zreplikowane do środowiska chmury.
- **[Przygotowanie](../migrate/stage.md):** Zreplikowane zasoby zostały przywrócone w przygotowanym wystąpieniu środowiska chmury.
- **[Testowanie biznesowe](./business-test.md):** Obciążenie zostało w pełni przetestowane i sprawdzone przez użytkowników firmy.
- **[Plan zmian biznesowych](./business-change-plan.md):** Firma udostępniła plan wprowadzania zmian zgodnie z podwyższeniem poziomu do środowiska produkcyjnego. Powinien on obejmować plan wdrażania użytkowników, zmiany w procesach biznesowych, użytkowników, którzy wymagają szkoleń, oraz harmonogramy różnych działań.
- **[Gotowość](./ready.md):** Ogólnie rzecz biorąc, przed podwyższeniem poziomu należy wprowadzić szereg zmian technicznych.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Najlepsze rozwiązania, które należy zastosować przed podwyższeniem poziomu

Następujące zmiany techniczne będą prawdopodobnie musiały zostać wprowadzone i udokumentowane jako część procesu podwyższania poziomu:

- **Wyrównanie domen** Niektóre zasady firmowe wymagają oddzielnych domen do przygotowania i produkcji. Upewnij się, że wszystkie zasoby są przyłączone do właściwej domeny.
- **Routing użytkowników** Sprawdź, czy użytkownicy uzyskują dostęp do obciążenia za pomocą odpowiednich tras sieciowych. Sprawdź spójność oczekiwań dotyczących wydajności.
- **Wyrównanie tożsamości** Sprawdź, czy użytkownicy przekierowani do aplikacji mają odpowiednie uprawnienia w domenie, aby móc hostować aplikację.
- **Wydajność** Wykonaj ostateczną walidację wydajności obciążeń, aby zminimalizować nieprzewidziane sytuacje.
- **Walidacja ciągłości działania i odzyskiwania po awarii** Upewnij się, że odpowiednie procesy tworzenia kopii zapasowych i odzyskiwania działają zgodnie z oczekiwaniami.
- **Klasyfikacja danych** Sprawdź poprawność klasyfikacji danych, aby się upewnić, że wdrożono odpowiednie zabezpieczenia i zasady.
- **Weryfikacja przez głównego specjalistę ds. zabezpieczeń informacji (CISO)** Upewnij się, że specjalista ds. zabezpieczeń informacji sprawdził obciążenie, ryzyko biznesowe, tolerancję ryzyka i strategie zaradcze.

## <a name="final-step-promote"></a>Ostatni krok: Podwyższenie poziomu

Obciążenia będą wymagały różnych poziomów szczegółowych przeglądów i procesów podwyższania poziomu. Jednak ponowne wyrównanie sieci jest wspólnym krokiem końcowym dla wszystkich wydań związanych z podwyższeniem poziomu. Gdy wszystko jest gotowe, zaktualizuj rekordy DNS lub adresy IP w celu przekierowania ruchu do zmigrowanego obciążenia.

## <a name="next-steps"></a>Następne kroki

Podwyższenie poziomu obciążenia sygnalizuje ukończenie wydania. Jednak równolegle z migracją wycofane zasoby muszą zostać [zlikwidowane](./decommission.md) i wycofane z użycia.

> [!div class="nextstepaction"]
> [Likwidowanie wycofanych zasobów](./decommission.md)
