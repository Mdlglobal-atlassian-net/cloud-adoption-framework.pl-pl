---
title: Jak produkty platformy Azure obsługują hierarchię portfolio?
description: Jak produkty platformy Azure obsługują hierarchię portfolio?
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a4ff0091473a7ea2882625dcbffe2f00d91b4ff6
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401222"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-do-azure-products-support-the-portfolio-hierarchy"></a>Jak produkty platformy Azure obsługują hierarchię portfolio?

W [zrozumieniu i dostosowywaniu hierarchii portfolio](./hosting-hierarchy.md)zestaw definicji dla hierarchii portfolio i mapowania roli ustanowił hierarchię zakresu dla większości podejścia portfolio. Zgodnie z opisem w tym artykule, można nie potrzebować poszczególnych poziomów lub _zakresów_. Minimalizacja liczby warstw zmniejsza złożoność, dlatego te warstwy nie powinny być wyświetlane jako wymagania.

W tym artykule przedstawiono sposób, w jaki każdy poziom lub zakres hierarchii jest obsługiwany na platformie Azure za pomocą narzędzi organizacji, narzędzi wdrażania i zarządzania, a także niektórych rozwiązań w Microsoft Cloud Framework wdrażania dla platformy Azure.

## <a name="organizing-the-hierarchy-in-azure"></a>Organizowanie hierarchii na platformie Azure

Azure Resource Manager zawiera kilka podejścia do organizacji, które ułatwiają organizowanie zasobów na każdym poziomie hierarchii chmur.

Paski suwaka na poniższym diagramie przedstawiają wspólne warianty w wyrównaniu. Szare części suwaków są wspólne, ale powinny być używane tylko dla określonych wymagań firmy. Punkty po obrazie opisują sugerowane najlepsze rozwiązanie.

![Organizacja zasobów wyrównana do hierarchii](../../_images/ready/hierarchy-with-organizing-tools.png)

- **Portfolio:** Jednostka gospodarcza lub biznesowa prawdopodobnie nie będzie zawierać żadnych zasobów technicznych, ale może mieć wpływ na decyzje dotyczące kosztów. Jednostki korporacyjne i biznesowe są reprezentowane w węzłach głównych hierarchii grupy zarządzania.
- **Platformy w chmurze:** Każde środowisko ma swój własny węzeł w hierarchii grupy zarządzania.
- **Strefy wyładunkowe i platforma Cloud Foundation:** Każda strefa docelowa jest reprezentowana jako subskrypcja. Podobnie, fundacje platformy są zawarte w własnych subskrypcjach. Niektóre projekty subskrypcji mogą wywoływać subskrypcję na chmurę lub za obciążenie, co spowoduje zmianę narzędzia do organizowania dla każdego z nich.
- **Obciążenia:** Każde obciążenie jest reprezentowane jako Grupa zasobów. Grupy zasobów są często używane do reprezentowania rozwiązań, wdrożeń lub innych grup technicznych zasobów.
- **Zasoby:** Każdy element zawartości jest z własnej reprezentowany jako zasób na platformie Azure.

## <a name="organizing-with-tags"></a>Organizowanie za pomocą tagów

Odchylenia od najlepszych rozwiązań są wspólne. Można je zarejestrować, dodając znakowanie wszystkich zasobów. Użyj znacznika, aby reprezentować każdą z odpowiednich warstw hierarchii. Aby uzyskać więcej informacji, zobacz [zalecane konwencje nazewnictwa i tagowania](../../ready/azure-best-practices/naming-and-tagging.md).
