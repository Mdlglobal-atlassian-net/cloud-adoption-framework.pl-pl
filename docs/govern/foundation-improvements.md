---
title: Popraw początkową podstawę ładu w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak stopniowo ulepszać początkową podstawę zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/03/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d4a0338daa65ea4269077f15acee05cd99a5fb10
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027641"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Popraw początkową podstawę ładu w chmurze

W tym artykule przyjęto założenie, że ustanowiono [wstępną Fundację ładu Cloud](./initial-foundation.md). Zgodnie z zaimplementowanym planem wdrażania chmury, materialne zagrożenia wypadają z proponowanych metod, za pomocą których zespoły chcą przyjąć chmurę. Ponieważ te czynniki ryzyka są wykorzystywane w rozmowach dotyczących planowania wydań, należy skorzystać z poniższej siatki, aby szybko określić kilka zalecanych praktyk, które zapoznają się z planem wdrożenia, aby zapobiec zagrożeniom spowodowanym zagrożeniami.

## <a name="maturity-vectors"></a>Wektory zapadalności

W dowolnym momencie można zastosować następujące wskazówki dotyczące programu do wstępnego ładu, aby rozwiązać zagrożenie lub potrzeby opisane w poniższej tabeli.

> [!IMPORTANT]
> Organizacja zasobów może mieć wpływ na sposób stosowania niniejszych wskazówek. Ważne jest, aby zacząć od zaleceń, które najlepiej dopasowują się do początkowej podstawy ładu Cloud, która została zaimplementowana w poprzednim kroku.

|Ryzyko/zapotrzebowanie | Mały średni korporacyjny | Duże przedsiębiorstwa |
|---|---|---|
|Poufne dane w chmurze|[Wskazówki dotyczące skryptów](./guides/standard/security-baseline-improvement.md)|[Wskazówki dotyczące skryptów](./guides/complex/security-baseline-improvement.md)|
|Aplikacje o znaczeniu strategicznym w chmurze|[Wskazówki dotyczące skryptów](./guides/standard/resource-consistency-improvement.md)|[Wskazówki dotyczące skryptów](./guides/complex/resource-consistency-improvement.md)|
|Zarządzanie kosztami chmury|[Wskazówki dotyczące skryptów](./guides/standard/cost-management-improvement.md)|[Wskazówki dotyczące skryptów](./guides/complex/cost-management-improvement.md)|
|Rozwiązanie wielochmurowe|[Wskazówki dotyczące skryptów](./guides/standard/multicloud-improvement.md)|[Wskazówki dotyczące skryptów](./guides/complex/multicloud-improvement.md)|
|Złożone/starsze Zarządzanie tożsamościami|         |[Wskazówki dotyczące skryptów](./guides/complex/identity-baseline-improvement.md)|
|Wiele warstw nadzoru|         |[Wskazówki dotyczące skryptów](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Następne kroki

Oprócz zastosowania wskazówek wstępnych, metodologia ładu w strukturze wdrażania w chmurze może być dostosowywana w celu dopasowania do unikatowych ograniczeń firmy. Po zastosowaniu stosownych zaleceń [Oceń zasady firmowe, aby zrozumieć dodatkowe wymagania dotyczące dostosowywania](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Oceń zasady firmowe](./corporate-policy.md)