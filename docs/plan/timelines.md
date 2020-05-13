---
title: Osie czasu w planie wdrażania chmury
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak oszacować osie czasu na podstawie planu wdrożenia chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: e5407f2f78942d22c5fa07b277f600d5440ddc04
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214025"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Osie czasu w planie wdrażania chmury

W poprzednim artykule z tej serii, obciążenia i zadania zostały przypisane do [wydań i iteracji](./iteration-paths.md). Te przydziały ponoszą oszacowania osi czasu w tym artykule.

Struktury podziału pracy są często używane w sekwencyjnych narzędziach do zarządzania projektami. Przedstawiają one, jak zadania zależne będą wykonywane z upływem czasu. Struktury te działają dobrze, gdy zadania są sekwencyjnie. Współzależności między zadaniami znajdującymi się w temacie Wdrażanie w chmurze sprawiają, że takie struktury są trudne do zarządzania. Aby wypełnić tę lukę, możesz oszacować osie czasu na podstawie przypisań ścieżek iteracji, ukrywając złożoność.

## <a name="estimate-timelines"></a>Szacowanie osi czasu

Aby utworzyć oś czasu, Zacznij od wersji. Te cele wydania tworzą datę docelową dla dowolnego wpływu na działalność biznesową. Iteracje ułatwiają wyrównywanie tych wersji z określonymi okresami czasowymi.

Jeśli na osi czasu są wymagane więcej szczegółowych punktów kontrolnych, użyj przypisania iteracji, aby wskazać punkty kontrolne. W tym celu należy założyć, że ostatnie wystąpienie zadania związanego z obciążeniem może stanowić punkt końcowy. Zespoły zwykle często otagują końcowe zadanie jako punkt kontrolny.

Dla każdego poziomu szczegółowości Użyj ostatniego dnia iteracji jako daty dla każdego punktu kontrolnego. To wiąże zakończenie wdrażania obciążenia z określoną datą. Możesz śledzić datę w arkuszu kalkulacyjnym lub w sekwencyjnym narzędziu do zarządzania projektami, takim jak Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Plany dostarczania na platformie Azure DevOps

<!-- docsTest:ignore "Microsoft Delivery Plans" -->

Jeśli używasz usługi Azure DevOps do zarządzania planem wdrażania chmury, rozważ użycie [rozszerzenia Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemname=ms.vss-plans). To rozszerzenie może szybko utworzyć wizualną reprezentację osi czasu opartą na przypisaniach iteracji i wersji.
