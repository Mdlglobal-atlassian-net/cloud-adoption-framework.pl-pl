---
title: Narzędzia do przyspieszania wdrażania na platformie Azure
description: Zobacz, jak narzędzia natywne platformy Azure mogą pomóc w dojrzałych zasadach i procesach, które obsługują dyscyplinę ładu Deployment Acceleration.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b6fac6af93c68f22561b578cfe598bc9d847c902
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434495"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Narzędzia do przyspieszania wdrażania na platformie Azure

[Przyspieszenie wdrożenia](./index.md) to jedno z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dziedzina koncentruje się na sposobach ustanawiania zasad umożliwiających nadzorowanie konfigurowania lub wdrażania zasobów. W pięciu dyscyplinach zarządzania chmurą, dyscyplina wdrożenia obejmuje wyrównanie wdrożenia i konfiguracji. Może to się odbywać za pośrednictwem działań ręcznych lub w pełni zautomatyzowanych działań metodyki DevOps. W obu przypadkach uwzględnione zasady byłyby w dużym stopniu takie same.

Powierniki chmury, opiekunowie chmury i architektzy w chmurze, którzy mają zainteresowanie zarządzaniem, mogą zainwestować dużo czasu w dyscypliny przyspieszenia wdrożenia, który kodyfikacje zasady i wymagania w ramach wielu wysiłków w zakresie wdrażania chmury. Narzędzia w tym łańcucha narzędzi są ważne dla zespołu nadzoru chmurowego i powinny być wysokim priorytetem dla ścieżki szkoleniowej dla zespołu.

Poniżej znajduje się lista narzędzi platformy Azure, które mogą pomóc w zakończeniu zasad i procesów, które obsługują tę dyscyplinę ładu.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Grupy zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Wykres zasobów platformy Azure](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Implementowanie zasad firmowych     |Yes |Nie  |Nie  |Nie | Nie |Nie |
|Stosowanie zasad w ramach subskrypcji     |Wymagany |Yes  |Nie  |Nie | Nie |Nie |
|Wdróż zdefiniowane zasoby     |Nie |Nie  |Yes  |Nie | Nie |Nie |
|Tworzenie w pełni zgodnych środowisk      |Wymagany |Wymagany  |Wymagany  |Yes | Nie |Nie |
|Zasady inspekcji      |Yes |Nie  |Nie  |Nie | Nie |Nie |
|Tworzenie zapytań dotyczących zasobów platformy Azure      |Nie |Nie  |Nie  |Nie |Yes |Nie |
|Raport dotyczący kosztów zasobów      |Nie |Nie  |Nie  |Nie |Nie |Yes |

Poniżej znajdują się dodatkowe narzędzia, które mogą być wymagane do osiągnięcia określonych celów przyspieszenia wdrożenia. Często te narzędzia są używane poza zespołem nadzoru, ale nadal są uważane za aspekty przyspieszenia wdrożenia jako dyscypliny.

|  | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Wdrażanie ręczne (pojedynczy element zawartości)     | Yes | Yes  | Nie  | Nie efektywnie | Nie | Yes |
|Wdrażanie ręczne (pełne środowisko)     | Nie efektywnie | Yes | Nie  | Nie efektywnie | Nie | Yes |
|Zautomatyzowane wdrażanie (pełne środowisko)     | Nie  | Yes  | Nie  | Yes  | Nie | Yes |
|Aktualizacja konfiguracji pojedynczego zasobu     | Yes | Yes | Nie efektywnie | Nie efektywnie | Nie | Tak — podczas replikacji |
|Aktualizacja konfiguracji pełnego środowiska     | Nie efektywnie | Yes | Yes | Yes  | Nie | Tak — podczas replikacji |
|Zarządzanie dryfem konfiguracji     | Nie efektywnie | Nie efektywnie | Yes  | Yes  | Nie | Tak — podczas replikacji |
|Utwórz zautomatyzowany potok, aby wdrożyć kod i skonfigurować zasoby (DevOps)     | Nie | Nie | Nie | Yes | Nie | Nie |

Oprócz narzędzi macierzystych platformy Azure wymienionych powyżej często klienci mogą korzystać z narzędzi innych firm, aby ułatwić przyspieszenie wdrożenia i wdrożenia DevOps.
