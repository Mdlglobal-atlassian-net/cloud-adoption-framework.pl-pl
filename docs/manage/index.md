---
title: Zarządzanie w chmurze
description: Użyj struktury wdrażania chmury dla platformy Azure, aby dowiedzieć się, jak opracować rozwiązania biznesowe i techniczne potrzebne do efektywnego zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ee28a021d3e58aae70efe0092bbef4698c897459
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400851"
---
# <a name="cloud-management-in-the-cloud-adoption-framework"></a>Zarządzanie w chmurze w przewodniku Cloud Adoption Framework

Realizacja [strategii chmury](../strategy/index.md) wymaga starannego planowania, przygotowania i wdrożenia. Ale to ciągłe działanie zasobów cyfrowych daje konkretne wyniki biznesowe. Bez planu zapewniającego niezawodne i właściwie zarządzanie rozwiązaniami w chmurze wszelkie wysiłki przyniosą niewielkie rezultaty. Poniższe ćwiczenia pomagają opracować metody biznesowe i techniczne konieczne do zapewnienia zarządzania w chmurze, które wspomaga działania operacyjne.

## <a name="get-started"></a>Rozpoczęcie pracy

Aby przygotować się na tę fazę cyklu wdrażania chmury, zalecane są następujące ćwiczenia:

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![1](../_images/icons/1.png)     | [Ustalenie planu bazowego zarządzania](./azure-management-guide/index.md): Zdefiniuj sposób klasyfikowania elementów o krytycznym znaczeniu, narzędzia do zarządzania w chmurze i procesy wymagane do realizacji minimalnego zobowiązania w zarządzaniu operacjami.                                |
| <br> ![2](../_images/icons/2.png)     | [Zdefiniowanie zobowiązań biznesowych](./considerations/business-alignment.md): Udokumentuj obsługiwane obciążenia, aby ustalić zobowiązania operacyjne zgodne z potrzebami firmy oraz inwestycje w zarządzanie w chmurze dla każdego obciążenia.                                |
| <br> ![3](../_images/icons/3.png)     | [Rozwinięcie planu bazowego zarządzania](./best-practices.md): Na podstawie zobowiązań biznesowych i decyzji operacyjnych wykorzystaj dołączone najlepsze rozwiązania, aby wdrożyć wymagane narzędzia do zarządzania w chmurze.                                |
| <br> ![4](../_images/icons/4.png)      | [Zaawansowane operacje i zasady projektowania](./design-principles.md): Platformy lub obciążenia, które wymagają wyższego poziomu zobowiązania biznesowego, mogą wymagać bardziej szczegółowego przeglądu architektury w celu zapewnienia odporności i niezawodności.  |

Poprzednie kroki określają praktyczne sposoby realizacji metodologii zarządzania przedstawionej w przewodniku Cloud Adoption Framework.

<!-- cSpell:ignore CAF -->

![Metodologia zarządzania w przewodniku Cloud Adoption Framework](../_images/manage/caf-manage.png)

Zgodnie z omówieniem w artykule dotyczącym [spójności biznesowej](./considerations/business-alignment.md) nie wszystkie obciążenia są krytyczne dla działania firmy. Każdy portfel obejmuje potrzeby zarządzania operacyjnego na różnym poziomie. Działania związane z zachowaniem spójności biznesowej pomagają określić wpływ na firmę i negocjować koszty zarządzania z firmą, aby zagwarantować najlepsze procesy i narzędzia do zarządzania operacyjnego.

Wskazówki zawarte w sekcji Zarządzanie przewodnika Cloud Adoption Framework służą dwóm celom:

- Przedstawiają praktyczne metody zarządzania operacyjnego, które odzwierciedlają typowe doświadczenia klientów.
- Pomagają utworzyć spersonalizowane rozwiązania do zarządzania na podstawie zobowiązań biznesowych.

Ta zawartość jest przeznaczona dla zespołu ds. operacji w chmurze. Jest również istotna dla architektów chmury, którzy muszą rozwinąć solidne podstawowe umiejętności z zakresu operacji w chmurze lub zasad projektowania w chmurze.

Zawartość przewodnika Cloud Adoption Framework dotyczy działalności biznesowej, technologii i kultury przedsiębiorstw. Ta sekcja przewodnika Cloud Adoption Framework dotyczy w szczególności zespołów ds. operacji IT, zapewniania ładu w zasobach IT, finansów, liderów biznesowych, sieci, tożsamości i wdrażania chmury. Różnorodne zależności między tym personelem wymagają od architektów chmury korzystających z tego przewodnika zastosowania podejścia ułatwiającego. Pomoc tym zespołom rzadko jest wysiłkiem jednorazowym.

Architekt chmury pełni rolę lidera myśli i osoby ułatwiającej kontakt między tymi odbiorcami. Zawartość tej kolekcji przewodników ma pomóc architektowi chmury w ułatwieniu odpowiednich konwersacji z odpowiednimi odbiorcami, aby umożliwić podjęcie koniecznych decyzji. Transformacja firmy, która jest napędzana i obsługiwana przez chmurę, zależy od tego, czy architekt chmury pomoże w podejmowaniu decyzji w zakresie działalności biznesowej i IT.

Każda sekcja przewodnika Cloud Adoption Framework reprezentuje różną specjalizację lub wariant roli architekta chmury. Ta sekcja przewodnika Cloud Adoption Framework jest przeznaczona dla architektów chmury pasjonujących się operacjami i zarządzaniem rozwiązaniami wdrożeniowymi. W ramach tej struktury ci specjaliści są często nazywani specjalistami ds. _operacji w chmurze_ lub zbiorczo _zespołem ds. operacji w chmurze_.

Jeśli chcesz postępować zgodnie z tym przewodnikiem od początku do końca, ta zawartość pomoże w opracowaniu solidnej strategii operacji w chmurze. Wskazówki przeprowadzą Cię przez teorię i implementację takiej strategii.

Stosując tę metodologię, możesz też [opracować czytelne zobowiązania biznesowe](./considerations/business-alignment.md).

<!-- TODO: For a crash course on the theory and quick access to Azure implementation, get started with the [governance guides overview](TODO). Using this guidance, you can start small and iteratively improve your governance needs in parallel with cloud adoption efforts. -->
