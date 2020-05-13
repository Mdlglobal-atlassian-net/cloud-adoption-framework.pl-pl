---
title: Jak produkty platformy Azure obsługują hierarchię portfolio?
description: Jak produkty platformy Azure obsługują hierarchię portfolio?
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: c4ab25ee9cf9a72f6b5a5750157601510d5d050d
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229966"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-do-azure-products-support-the-portfolio-hierarchy"></a>Jak produkty platformy Azure obsługują hierarchię portfolio?

W [zrozumieniu i dostosowywaniu hierarchii portfolio](./hosting-hierarchy.md)zestaw definicji dla hierarchii portfolio i mapowania roli ustanowił hierarchię zakresu dla większości podejścia portfolio. Zgodnie z opisem w tym artykule, mogą nie być potrzebne wszystkie poziomy lub _zakresy_ podane poniżej. Minimalizacja liczby warstw zmniejsza złożoność, dlatego nie należy wyświetlać tych warstw jako wymaganych najlepszych rozwiązań.

W tym artykule przedstawiono sposób, w jaki każdy poziom lub zakres hierarchii jest obsługiwany na platformie Azure za pomocą narzędzi organizacji, narzędzi wdrażania i zarządzania, a także niektórych rozwiązań w strukturze wdrożenia chmury.

## <a name="organizing-the-hierarchy-in-azure"></a>Organizowanie hierarchii na platformie Azure

Azure Resource Manager zawiera kilka podejścia do organizacji, które ułatwiają organizowanie zasobów na każdym poziomie hierarchii chmur.

> [!NOTE]
> Paski slajdów poniżej przedstawiają wspólne warianty w wyrównaniu. Szare części suwaków są wspólne, ale powinny być używane tylko wtedy, gdy jest to wymagane przez konkretne wymagania biznesowe. Na poniższej ilustracji opisano tylko sugerowane najlepsze rozwiązanie.

![Organizacja zasobów wyrównana do hierarchii](../../_images/ready/hierarchy-with-organizing-tools.png)

- **Portfolio:** Jednostka biznesowa lub gospodarcza prawdopodobnie nie będzie zawierać żadnych zasobów technicznych, ale może mieć wpływ na decyzje dotyczące kosztów. Jednostki korporacyjne i biznesowe powinny być reprezentowane w węzłach głównych hierarchii grupy zarządzania.
- **Platformy w chmurze:** Każde środowisko powinno mieć własny węzeł w hierarchii grupy zarządzania.
- **Strefy wyładunkowe i fundacje platform:** Każda strefa docelowa powinna być reprezentowana jako subskrypcja. Podobnie znalezione platformy powinny być zawarte w własnych subskrypcjach. Istnieją różne projekty subskrypcji, które mogą wywoływać subskrypcję na chmurę lub za obciążenie, co spowoduje zmianę narzędzia do organizowania dla każdego z nich.
- **Obciążenie:** Każde obciążenie powinno być reprezentowane jako Grupa zasobów. Grupy zasobów są również często używane do reprezentowania rozwiązań, wdrożeń lub innych grup zasobów technicznych.
- **Zasób:** Każdy element zawartości jest z własnej reprezentowany jako zasób na platformie Azure.

### <a name="organize-with-tags"></a>Organizuj przy użyciu tagów

Często istnieją różne odmiany od najlepszych rozwiązań. Odchylenia od powyższych najlepszych praktyk powinny być rejestrowane przez tagowanie wszystkich elementów zawartości za pomocą znacznika, aby reprezentować każdą z odpowiednich warstw hierarchii. Aby uzyskać więcej informacji, zobacz [zalecane konwencje nazewnictwa i tagowania](../../ready/azure-best-practices/naming-and-tagging.md).
