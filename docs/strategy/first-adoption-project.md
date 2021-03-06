---
title: Pierwszy projekt wdrażania chmury
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby poznać procesy wdrażania chmury i działania obciążeń hostowanych w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 31c0335cd4f1a6d8ef8e4793e3f6fb4fa383d339
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83221488"
---
<!-- markdownlint-disable MD026 -->

# <a name="first-cloud-adoption-project"></a>Pierwszy projekt wdrażania chmury

Jest to krzywa szkoleniowa i zobowiązanie czasowe związane z planowaniem wdrażania w chmurze. Nawet w przypadku doświadczonych zespołów, odpowiednie planowanie jest czasochłonne: czas na dostosowanie uczestników projektu, czas zbierania i analizowania danych, czas na weryfikację długoterminowych decyzji oraz czas na dostosowanie osób, procesów i technologii. W najbardziej wydajnych wysiłkach planowanie zwiększa się równolegle z wdrażaniem, ulepszanie przy użyciu poszczególnych wersji i każdej migracji obciążenia do chmury. Ważne jest, aby zrozumieć różnicę między planem wdrażania chmury a strategią wdrażania chmury. Potrzebujesz dobrze zdefiniowanej strategii, aby ułatwić i poprowadzić implementację planu wdrażania w chmurze.

<!-- docsTest:ignore "Strategy, Plan, Ready, Adopt, and Operate phases" -->

Platforma wdrażania w chmurze dla platformy Azure przedstawia procesy wdrażania chmury oraz obsługę obciążeń hostowanych w chmurze. Każdy proces w fazach strategii, planowania, gotowości, przyjęcia i eksploatacji wymaga niewielkich rozwinięcia umiejętności technicznych, gospodarczych i operacyjnych. Niektóre z tych umiejętności mogą pochodzić z uczenia bezpośredniego. Jednak wiele z nich jest najbardziej efektywnie nabytych przez praktyczne środowisko pracy.

Rozpoczęcie pierwszego procesu wdrażania równolegle z programowaniem planu zapewnia pewne korzyści:

- Ustanów sposób myślenia wzrostu, aby zachęcić do uczenia się i eksploracji.
- Zapewnij zespołowi możliwość tworzenia niezbędnych umiejętności.
- Twórz sytuacje, które zachęcają do współpracy.
- Zidentyfikuj luki w zakresie umiejętności i potencjalne potrzeby partnerstwa.
- Podaj materialne dane wejściowe planu.

## <a name="first-project-criteria"></a>Kryteria pierwszego projektu

Pierwszy projekt wdrożenia powinien zostać wyrównany do Twoich [motywacji](./motivations.md) na potrzeby wdrożenia w chmurze. W miarę możliwości pierwszy projekt powinien również przedstawiać postępy w kierunku zdefiniowanego [wyniku biznesowego](./business-outcomes/business-outcome-template.md).

## <a name="first-project-expectations"></a>Pierwsze oczekiwania projektu

Projekt pierwszego wdrożenia zespołu prawdopodobnie spowoduje powstanie w środowisku produkcyjnym pewnego rodzaju. Ale nie zawsze jest to przypadek. Wczesne ustalenie odpowiednich oczekiwań. Oto kilka oczekiwań, aby ustawić:

- Ten projekt jest źródłem uczenia się.
- Ten projekt może skutkować wdrożeniem produkcyjnym, ale prawdopodobnie najpierw będzie potrzebny dodatkowy nakład pracy.
- Dane wyjściowe tego projektu to zestaw jasno określonych wymagań, aby zapewnić dłuższe rozwiązanie produkcyjne.

## <a name="first-project-examples"></a>Pierwsze przykłady projektu

Aby można było obsłużyć powyższe kryteria, ta lista zawiera przykład pierwszego projektu dla każdej kategorii motywacji:

- **Krytyczne zdarzenia biznesowe:** Gdy krytyczne zdarzenie biznesowe jest główną motywacją, implementacja narzędzia, takiego jak [Azure Site Recovery](../migrate/azure-migration-guide/migrate.md#azure-site-recovery) , może być dobrym pierwszym projektem. Podczas migracji można użyć tego narzędzia do szybkiej migracji zasobów centrum danych. Jednak podczas pierwszego projektu można używać go w sposób czysty jako narzędzie do odzyskiwania po awarii, co zmniejsza zależności od zasobów odzyskiwania po awarii w centrum danych.

- **Motywacje migracji:** Gdy migracja jest główną motywacją, warto zacząć od migracji niekrytycznego obciążenia. [Przewodnik po konfiguracji platformy Azure](../ready/azure-setup-guide/index.md) i [Przewodnik migracji platformy Azure](../migrate/azure-migration-guide/index.md) mogą zapewnić wskazówki dotyczące migracji pierwszego obciążenia.

- **Motywacje innowacji:** Gdy innowacje są główną motywacją, tworzenie dostosowanego środowiska deweloperskiego/testowego może być doskonałym pierwszym projektem.

Dodatkowe przykłady projektów z pierwszego wdrożenia obejmują:

- **Ciągłość działania i odzyskiwanie po awarii (BCDR):** Poza Azure Site Recovery można zaimplementować wiele strategii BCDR jako pierwszy projekt.
- **Nieprodukcja:** Wdróż wystąpienie nieprodukcyjne w obciążeniu.
- **Archiwizuj:** Chłodny magazyn może nakładać na zasoby centrum danych. Przeniesienie tych danych do chmury jest trwałą szybką licytacją.
- **Koniec wsparcia (EOS):** Migrowanie zasobów, które osiągnęły koniec wsparcia, to kolejna szybka wersja, która kompiluje umiejętności techniczne. Może to również stanowić niedrogią możliwość uniknięcia kosztownych umów pomocy technicznej lub kosztów licencjonowania.
- **Interfejs pulpitu wirtualnego (VDI):** Tworzenie pulpitów wirtualnych dla pracowników zdalnych umożliwia szybkie wygranie. W niektórych przypadkach ten pierwszy ten projekt może również zmniejszyć zależność od kosztownych sieci prywatnych na korzyść publicznej łączności z Internetem.
- Tworzenie **i testowanie:** Usuń tworzenie i testowanie z środowisk lokalnych, aby zapewnić deweloperom kontrolę, elastyczność i samoobsługową obsługę.
- **Proste aplikacje (mniej niż pięć):** Unowocześnienie i migrowanie prostej aplikacji, aby szybko uzyskać środowisko programistyczne i operacyjne.
- **Laboratoria wydajności:** Gdy w ustawieniach laboratorium potrzebna jest wysoka wydajność, użyj chmury, aby szybko i ekonomicznie obsługiwać te laboratoria przez krótki czas.
- **Platforma danych:** Tworzenie danych usługi Data Lake przy użyciu skalowalnych obciążeń obliczeniowych, raportowania lub uczenia maszynowego oraz Migrowanie do zarządzanych baz danych przy użyciu metod zrzutów/przywracania lub usług migracji danych.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat strategii [równoważenia konkurencyjnych priorytetów](./balance-competing-priorities.md).

> [!div class="nextstepaction"]
> [Zrównoważone priorytety konkurencji](./balance-competing-priorities.md)
