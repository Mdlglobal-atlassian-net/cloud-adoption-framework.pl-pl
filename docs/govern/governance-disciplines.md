---
title: Pięć dziedzin nadzoru chmury
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o Cost Management, przyspieszeniu wdrażania, linii bazowej tożsamości, spójności zasobów i linii bazowej zabezpieczeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 550dd724ae6a8eedd34b5a8ffc2146425500bc59
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83400599"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Pięć dziedzin nadzoru chmury

<!-- docsTest:ignore "Disciplines of Cloud Governance" "Cost Management" "Deployment Acceleration" "Identity Baseline" "Resource Consistency" "Security Baseline" -->
<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| Wszelkie zmiany procesów firmy lub platform technologicznych wprowadzają ryzyko. Zespoły nadzorujące chmur, których członkowie są czasami znane jako powiernika chmury, są zadaniem z ograniczeniami tego ryzyka i zapewnieniem minimalnego zakłócenia wdrażania lub wysiłków innowacji. <br><br> Model nadzoru struktury wdrażania chmury obejmuje te decyzje, niezależnie od wybranej platformy chmurowej, koncentrując się na [rozwoju zasad korporacyjnych](./corporate-policy.md) i [pięciu dyscyplinach zarządzania chmurą](#disciplines-of-cloud-governance). [Przewodniki projektowe](./guides/index.md) z możliwością podejmowania działań pokazują ten model przy użyciu usług platformy Azure. Zapoznaj się z zasadami dotyczącymi modelu ładu Framework wdrażania w chmurze poniżej. | <br><br> [![Diagram modelu ładu struktury wdrażania w chmurze: zasady firmowe i dyscypliny ładu](../_images/operational-transformation-govern-thumbnail.png)](../_images/operational-transformation-govern-large.png#lightbox) <br> _Rysunek 1. wizualne zasady firmowe i pięć dyscyplin nadzoru chmurowego._ |

## <a name="disciplines-of-cloud-governance"></a>Dyscypliny zarządzania chmurą

W przypadku każdej platformy w chmurze istnieją typowe dyscypliny ładu, które ułatwiają informowanie zasad i wyrównanie łańcuchy narzędzi. Te dyscypliny przedstawiają decyzje dotyczące właściwego poziomu automatyzacji i egzekwowania zasad firmowych na platformach w chmurze.

| | |
|---|---|
| <br> ![Cost Management](../_images/govern/cost-management.png) | <br> [Cost Management](./cost-management/index.md): koszt jest podstawowym problemem dla użytkowników w chmurze. Opracowywanie zasad kontroli kosztów dla wszystkich platform w chmurze. |
| <br> ![Punkt odniesienia zabezpieczeń](../_images/govern/security-baseline.png) | <br> [Linia bazowa zabezpieczeń](./security-baseline/index.md): zabezpieczenia są skomplikowanym podmiotem, które są unikatowe dla każdej firmy. Po ustaleniu wymagań dotyczących zabezpieczeń zasady zarządzania chmurą i egzekwowanie stosują te wymagania w konfiguracjach sieci, danych i zasobów.|
| <br> ![Punkt odniesienia obsługi tożsamości](../_images/govern/identity-baseline.png) | <br> [Linia bazowa tożsamości](./identity-baseline/index.md): niespójności w zakresie wymagań dotyczących tożsamości mogą zwiększyć ryzyko naruszenia. Dyscyplina linii bazowej tożsamości polega na tym, że tożsamość jest spójna w ramach wysiłków związanych z wdrażaniem w chmurze. |
| <br> ![Spójność zasobów](../_images/govern/resource-consistency.png) | <br> [Spójność zasobów](./resource-consistency/index.md): operacje w chmurze zależą od spójnej konfiguracji zasobów. Dzięki narzędziom ładu można spójnie konfigurować zasoby, aby zarządzać ryzykiem związanym z dołączaniem, dryfem, odnajdywaniem i odzyskiwaniem. |
| <br> ![Przyspieszanie wdrażania](../_images/govern/deployment-acceleration.png) | <br> [Przyspieszenie wdrożenia](./deployment-acceleration/index.md): scentralizowaność, standaryzacja i spójność w podejścia do wdrożenia i konfiguracji ulepszania praktyk nadzoru. Po podaniu przez narzędzia do zarządzania oparte na chmurze tworzą one współczynnik chmury, który może przyspieszyć działania wdrożenia. |
