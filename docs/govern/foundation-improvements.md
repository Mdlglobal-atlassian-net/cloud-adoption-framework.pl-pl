---
title: Popraw początkową podstawę ładu w chmurze
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak stopniowo ulepszać początkową podstawę zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 456e9105cd4d8425681664bc9cbcb74d54f7f58f
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400577"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Popraw początkową podstawę ładu w chmurze

W tym artykule przyjęto założenie, że ustanowiono [wstępną Fundację ładu Cloud](./initial-foundation.md). Zgodnie z zaimplementowanym planem wdrażania chmury, materialne zagrożenia wypadają z proponowanych metod, za pomocą których zespoły chcą przyjąć chmurę. W miarę jak te zagrożenia są stosowane w przypadku konwersacji w ramach planowania wydań, należy skorzystać z następującej siatki, aby szybko określić kilka najlepszych rozwiązań, które zapoznają się z planem wdrożenia, aby zapobiec zagrożeniom spowodowanym rzeczywistym zagrożeniem.

## <a name="maturity-vectors"></a>Wektory zapadalności

W dowolnym momencie następujące najlepsze rozwiązania można zastosować do początkowego ładu, aby sprostać ryzyku lub potrzebom wymienionym w poniższej tabeli.

> [!IMPORTANT]
> Organizacja zasobów może mieć wpływ na sposób stosowania tych najlepszych rozwiązań. Ważne jest, aby zacząć od zaleceń, które najlepiej dopasowują się do początkowej podstawy ładu Cloud, która została zaimplementowana w poprzednim kroku.

| Ryzyko/zapotrzebowanie | Przedsiębiorstwo standardowe | Przedsiębiorstwo złożone |
|---|---|---|
| Poufne dane w chmurze | [Ulepszenia w ramach dziedziny](./guides/standard/security-baseline-improvement.md) | [Ulepszenia w ramach dziedziny](./guides/complex/security-baseline-improvement.md) |
| Aplikacje o kluczowym znaczeniu w chmurze | [Ulepszenia w ramach dziedziny](./guides/standard/resource-consistency-improvement.md) | [Ulepszenia w ramach dziedziny](./guides/complex/resource-consistency-improvement.md) |
| Zarządzanie kosztami chmury | [Ulepszenia w ramach dziedziny](./guides/standard/cost-management-improvement.md) | [Ulepszenia w ramach dziedziny](./guides/complex/cost-management-improvement.md) |
| Rozwiązanie wielochmurowe | [Ulepszenia w ramach dziedziny](./guides/standard/multicloud-improvement.md) | [Ulepszenia w ramach dziedziny](./guides/complex/multicloud-improvement.md) |
| Złożone/starsze Zarządzanie tożsamościami | Nie dotyczy | [Ulepszenia w ramach dziedziny](./guides/complex/identity-baseline-improvement.md) |
| Wiele warstw nadzoru | Nie dotyczy | [Ulepszenia w ramach dziedziny](./guides/complex/multiple-layers-of-governance.md) |

## <a name="next-steps"></a>Następne kroki

Oprócz zastosowania najlepszych rozwiązań, metodologia działania w chmurze wdrażania chmury można dostosować do własnych ograniczeń firmy. Po zastosowaniu stosownych zaleceń [Oceń zasady firmowe, aby zrozumieć dodatkowe wymagania dotyczące dostosowywania](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Ocenianie zasad firmowych](./corporate-policy.md)
