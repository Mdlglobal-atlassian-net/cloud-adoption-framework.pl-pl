---
title: Co nowego
description: Zapoznaj się z najnowszymi aktualizacjami platformy wdrażania Microsoft Cloud platformy Azure.
author: JanetCThomas
ms.author: janet
ms.date: 03/09/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 1ec13eca60f8e3ed4f2d30b9c4c1b6b0138905a3
ms.sourcegitcommit: d660484d534bc61fc60470373f3fcc885a358219
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/18/2020
ms.locfileid: "79510811"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Co nowego w strukturze Microsoft Cloud wdrażania dla platformy Azure

Poniżej znajduje się lista najnowszych zmian wprowadzonych w strukturze wdrożenia chmury.

Ta struktura jest wbudowana w współpracę z klientami, partnerami i wewnętrznymi zespołami firmy Microsoft. Nowa i zaktualizowana zawartość jest publikowana, gdy staną się dostępne. Te wersje umożliwiają przetestowanie, zweryfikowanie i dostosowanie wskazówek wraz z nami. Zachęcamy do współpracy z nami w celu utworzenia struktury wdrażania w chmurze dla platformy Azure.

## <a name="march-2020"></a>Marzec 2020

W odpowiedzi na opinie o ciągłości migracji przy użyciu wielu sekcji środowiska wdrażania chmury, w tym strategii, planowania, gotowości i migracji, wprowadziliśmy następujące aktualizacje. Te aktualizacje zostały zaprojektowane w celu ułatwienia zrozumienia procesu planowania i wdrażania w trakcie kontynuowania podróży migracji.

### <a name="strategy-updates"></a>Aktualizacje strategii

| Artykuł                                                                       | Opis                                                                                                                                    |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [Równoważenie portfela](../strategy/balance-the-portfolio.md)                 | Przeniesiono ten artykuł, aby pojawił się wcześniej w metodologii strategii. Dzięki temu można uwidocznić proces myśli wcześniej w cyklu życia. |
| [Równoważenie&nbsp;konkurencyjnych priorytetów&nbsp;](../strategy/balance-competing-priorities.md) | **Nowy artykuł**: zawiera opis bilansu priorytetów w ramach metodologii w celu poinformowania o strategii.                                         |

### <a name="plan-updates"></a>Planowanie aktualizacji

| Artykuł                                                             | Opis                                                                                                                                                                           |
|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Ocena&nbsp;najlepszych&nbsp;](../plan/contoso-migration-assessment.md) | Ten artykuł został przeniesiony do nowej sekcji "najlepsze praktyki" dotyczącej metodologii planu. Dzięki temu można uwidocznić sposób oceny środowisk lokalnych wcześniej w cyklu życia. |

### <a name="ready-updates"></a>Gotowe aktualizacje

| Artykuł                                                                   | Opis                                                                                                              |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| [Co&nbsp;jest&nbsp;&nbsp;ego&nbsp;strefy docelowej?](../ready/landing-zone/index.md)                 | **Nowy artykuł**: określa termin strefy docelowej.                                                                          |
| [Pierwsza strefa docelowa](../ready/landing-zone/first-landing-zone.md)         | **Nowy artykuł**: rozwija się, porównując różne strefy wyładunkowe.                                                     |
| [Migrowanie strefy wyładunkowej](../ready/landing-zone/migrate-landing-zone.md)     | Oddzielona definicja planu wdrożenia chmury z wyboru pierwszej strefy docelowej.         |
| [Strefa docelowa Terraform](../ready/landing-zone/terraform-landing-zone.md) | Przeniesiono do nowej sekcji "strefa docelowa" przygotowanej metodologii, aby podwyższyć poziom Terraform w konwersacji strefy docelowej. |

### <a name="migration-updates"></a>Aktualizacje migracji

| Artykuł                                                                                          | Opis                                                                                                                                                             |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Omówienie](../migrate/azure-migration-guide/index.md)                                            | Zaktualizowano o wyraźniejszy opis przewodnika i mniejszą liczbę kroków.                                                                                                        |
| [Szacowaniu](../migrate/azure-migration-guide/assess.md)                                             | Dodano sekcję "trudne założenia", aby zademonstrować, jak ten poziom oceny współdziała z podejściem do oceny przyrostowej wymienionym w metodologii planu. |
| [Klasyfikacja podczas oceniania procesów](../migrate/migration-considerations/assess/classify.md) | **Nowy artykuł**: zawiera opis znaczenia klasyfikowania wszystkich zasobów i obciążeń przed migracją.                                                                    |
| [Migrate (Migracja)](../migrate/azure-migration-guide/migrate.md)                                           | Dodano odwołanie do UnifyCloud w opcjach narzędzi innych firm, w odpowiedzi na opinie w ramach konferencji warstwy 1.                                                         |
| [Testowanie,&nbsp;Optymalizacja,&nbsp;i&nbsp;podwyższanie poziomu](../migrate/azure-migration-guide/optimize-and-transform.md)        | Wyrównuje tytuł tego artykułu z innymi sugestiami dotyczącymi ulepszeń procesów.                                                                                           |
| [Przegląd oceny](../migrate/migration-considerations/assess/index.md)                           | Zaktualizowano w celu zilustrowania, że ocena w tej fazie koncentruje się na ocenie dopasowania technicznego określonego obciążenia i powiązanych zasobów.                               |
| [Lista kontrolna dotycząca planowania](../migrate/migration-considerations/prerequisites/planning-checklist.md)    | Zaktualizowano w celu wyjaśnienia znaczenia wyrównania operacji podczas planowania działań związanych z migracją w celu zapewnienia dobrego zarządzania obciążeniem po migracji.                  |
