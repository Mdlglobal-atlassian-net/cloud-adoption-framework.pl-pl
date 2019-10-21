---
title: Popraw początkową podstawę ładu w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak stopniowo ulepszać początkową podstawę zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/13/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: fc06264bad61571aaa4735350a16e294492dd9c0
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547719"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Popraw początkową podstawę ładu w chmurze

W tym artykule przyjęto założenie, że ustanowiono [wstępną Fundację ładu Cloud](./initial-foundation.md). Zgodnie z zaimplementowanym planem wdrażania chmury, materialne zagrożenia wypadają z proponowanych metod, za pomocą których zespoły chcą przyjąć chmurę. W miarę jak te zagrożenia są stosowane w przypadku konwersacji w ramach planowania wydań, należy skorzystać z następującej siatki, aby szybko określić kilka najlepszych rozwiązań, które zapoznają się z planem wdrożenia, aby zapobiec zagrożeniom spowodowanym rzeczywistym zagrożeniem.

## <a name="maturity-vectors"></a>Wektory zapadalności

W dowolnym momencie następujące najlepsze rozwiązania można zastosować do początkowego ładu, aby sprostać ryzyku lub potrzebom wymienionym w poniższej tabeli.

> [!IMPORTANT]
> Organizacja zasobów może mieć wpływ na sposób stosowania tych najlepszych rozwiązań. Ważne jest, aby zacząć od zaleceń, które najlepiej dopasowują się do początkowej podstawy ładu Cloud, która została zaimplementowana w poprzednim kroku.

|Ryzyko/zapotrzebowanie | Przedsiębiorstwo standardowe | Przedsiębiorstwo złożone |
|---|---|---|
|Poufne dane w chmurze|[Ulepszanie dyscypliny](./guides/standard/security-baseline-improvement.md)|[Ulepszanie dyscypliny](./guides/complex/security-baseline-improvement.md)|
|Aplikacje o znaczeniu strategicznym w chmurze|[Ulepszanie dyscypliny](./guides/standard/resource-consistency-improvement.md)|[Ulepszanie dyscypliny](./guides/complex/resource-consistency-improvement.md)|
|Zarządzanie kosztami chmury|[Ulepszanie dyscypliny](./guides/standard/cost-management-improvement.md)|[Ulepszanie dyscypliny](./guides/complex/cost-management-improvement.md)|
|Rozwiązanie wielochmurowe|[Ulepszanie dyscypliny](./guides/standard/multicloud-improvement.md)|[Ulepszanie dyscypliny](./guides/complex/multicloud-improvement.md)|
|Złożone/starsze Zarządzanie tożsamościami|ND|[Ulepszanie dyscypliny](./guides/complex/identity-baseline-improvement.md)|
|Wiele warstw nadzoru|ND|[Ulepszanie dyscypliny](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Następne kroki

Oprócz zastosowania najlepszych rozwiązań, metodologia ładu w strukturze wdrożenia chmury można dostosować tak, aby pasowała do unikatowych ograniczeń firmy. Po zastosowaniu stosownych zaleceń [Oceń zasady firmowe, aby zrozumieć dodatkowe wymagania dotyczące dostosowywania](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Oceń zasady firmowe](./corporate-policy.md)
