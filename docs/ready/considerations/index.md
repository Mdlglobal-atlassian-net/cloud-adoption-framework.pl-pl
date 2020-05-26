---
title: Rozszerzanie strefy docelowej
description: Skorzystaj z przewodnika Cloud Adoption Framework dla platformy Azure, aby dowiedzieć się, jak rozszerzyć strefę docelową.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 0964da23da680755ea9d6c35fef0996e986780b4
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756570"
---
# <a name="expand-your-landing-zone"></a>Rozszerzanie strefy docelowej

Ta sekcja metodologii Gotowość jest oparta na zasadach [refaktoryzacji strefy docelowej](../landing-zone/refactor.md). Jak opisano w tym artykule, podejście oparte na refaktoryzacji do infrastruktury jako kodu usuwa czynniki blokujące sukces firmy, jednocześnie minimalizując ryzyko. W tej serii artykułów przyjęto założenie, że pierwsza strefa docelowa została wdrożona, a teraz chcesz ją rozszerzyć, aby spełnić wymagania przedsiębiorstwa.

## <a name="shared-architecture-principles"></a>Zasady architektury udostępnionej

Rozszerzenie strefy docelowej zapewnia podejście „code first” w celu osadzenia poniższych zasad w strefie docelowej i, w szerszym zakresie, w całym środowisku chmury.

![Zasady architektury udostępnionej](../../_images/ready/shared-principles.png)

Te same zasady architektury są współużytkowane przez usługę [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview), rozwiązanie [Dobrze zaprojektowana struktura platformy Microsoft Azure](https://docs.microsoft.com/azure/architecture/framework) i rozwiązania w [Centrum architektury platformy Azure](https://docs.microsoft.com/azure/architecture).

## <a name="applying-these-principles-to-your-landing-zone-improvements"></a>Stosowanie tych zasad do ulepszeń strefy docelowej

W celu lepszego dopasowania do metodologii opisanych w podręczniku Cloud Adoption Framework, powyższe zasady pogrupowano w ulepszenia strefy docelowej umożliwiające podejmowanie akcji:

- Podstawowe zagadnienia: refaktoryzacja strefy docelowej w celu udoskonalenia hostingu, podstaw i innych podstawowych elementów.
- Rozszerzenia operacji: dodaj konfiguracje zarządzania operacjami, aby **poprawić wydajność, niezawodność i doskonałość operacyjną**.
- Rozszerzenia ładu: dodaj konfiguracje ładu, aby poprawić **koszt, niezawodność, bezpieczeństwo** i spójność.
- Rozszerzenia zabezpieczeń: dodaj konfiguracje **zabezpieczeń**, aby zwiększyć ochronę poufnych danych i krytycznych systemów.

> [!WARNING]
> Zespoły ds. wdrożenia, które mają cel średniookresowy (w ciągu 24 miesięcy), aby **hostować ponad 1000 zasobów (aplikacji, infrastruktury lub zasobów danych) w chmurze**, powinny rozważyć każde z tych rozszerzeń na początku swojej drogi do wdrożenia w chmurze. W przypadku wszystkich innych wzorców wdrażania rozszerzenia strefy docelowej mogą być równoległą iteracją, co umożliwia wczesny sukces biznesowy.

## <a name="next-steps"></a>Następne kroki

Przed refaktoryzacją pierwszej strefy docelowej ważne jest zrozumienie [rozwoju stref docelowych opartego na testach](./test-driven-development.md).

> [!div class="nextstepaction"]
> [Rozwój stref docelowych oparty na testach](./test-driven-development.md)
