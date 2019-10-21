---
title: Osie czasu w planie wdrażania chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Osie czasu w planie wdrażania chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: c5bafd4504a0df9570bf65846a5a077e54e158ca
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72549030"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Osie czasu w planie wdrażania chmury

W poprzednim artykule z tej serii, obciążenia i zadania zostały przypisane do [wydań i iteracji](./iteration-paths.md). Te przydziały ponoszą oszacowania osi czasu w tym artykule.

Struktury podziału pracy (SPP) są często używane w sekwencyjnych narzędziach do zarządzania projektami. Przedstawiają one, jak zadania zależne będą wykonywane z upływem czasu. Struktury te działają dobrze, gdy zadania są sekwencyjnie. Współzależności między zadaniami znajdującymi się w temacie Wdrażanie w chmurze sprawiają, że takie struktury są trudne do zarządzania. Aby wypełnić tę lukę, możesz oszacować osie czasu na podstawie przypisań ścieżek iteracji, ukrywając złożoność.

## <a name="estimate-timelines"></a>Szacowanie osi czasu

Aby utworzyć oś czasu, Zacznij od wersji. Te cele wydania tworzą datę docelową dla dowolnego wpływu na działalność biznesową. Iteracje ułatwiają wyrównywanie tych wersji z określonymi okresami czasowymi.

Jeśli na osi czasu są wymagane więcej szczegółowych punktów kontrolnych, użyj przypisania iteracji, aby wskazać punkty kontrolne. W tym celu należy założyć, że ostatnie wystąpienie zadania związanego z obciążeniem może stanowić punkt końcowy. Zespoły zwykle często otagują końcowe zadanie jako punkt kontrolny.

Dla każdego poziomu szczegółowości Użyj ostatniego dnia iteracji jako daty dla każdego punktu kontrolnego. To wiąże zakończenie wdrażania obciążenia z określoną datą. Możesz śledzić datę w arkuszu kalkulacyjnym lub w sekwencyjnym narzędziu do zarządzania projektami, takim jak Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Plany dostarczania na platformie Azure DevOps

Jeśli używasz usługi Azure DevOps do zarządzania planem wdrażania chmury, rozważ użycie rozszerzenia [Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans) . To rozszerzenie może szybko utworzyć wizualną reprezentację osi czasu opartą na przypisaniach iteracji i wersji.
