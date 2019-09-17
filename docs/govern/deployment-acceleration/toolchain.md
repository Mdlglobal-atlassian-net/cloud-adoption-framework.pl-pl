---
title: Narzędzia do przyspieszania wdrażania na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia do przyspieszania wdrażania na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b9cf2edd1edafb4390b89465dba4a8e8dcfc1b0e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030373"
---
# <a name="deployment-acceleration-tools-in-azure"></a>Narzędzia do przyspieszania wdrażania na platformie Azure

[Przyspieszenie wdrożenia](./index.md) to jedno z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dziedzina koncentruje się na sposobach ustanawiania zasad umożliwiających nadzorowanie konfigurowania lub wdrażania zasobów. W pięciu dyscyplinach zarządzania chmurą, dyscyplina wdrożenia obejmuje wyrównanie wdrożenia i konfiguracji. Może to się odbywać za pośrednictwem działań ręcznych lub w pełni zautomatyzowanych działań metodyki DevOps. W obu przypadkach uwzględnione zasady byłyby w dużym stopniu takie same.

Powierniki chmury, opiekunowie chmury i architektzy w chmurze, którzy mają zainteresowanie zarządzaniem, mogą zainwestować dużo czasu w dyscypliny przyspieszenia wdrożenia, który kodyfikacje zasady i wymagania w ramach wielu wysiłków w zakresie wdrażania chmury. Narzędzia w tym łańcucha narzędzi są ważne dla zespołu nadzoru chmurowego i powinny być wysokim priorytetem dla ścieżki szkoleniowej dla zespołu.

Poniżej znajduje się lista narzędzi platformy Azure, które mogą pomóc w zakończeniu zasad i procesów, które obsługują tę dyscyplinę ładu.

|  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Grupy zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups) | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) | [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Wykres zasobów platformy Azure](https://docs.microsoft.com/azure/governance/resource-graph/overview) | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management) |
|---------|---------|---------|---------|---------|---------|---------|
|Implementowanie zasad firmowych     |Tak |Nie  |Nie  |Nie | Nie |Nie |
|Stosowanie zasad w ramach subskrypcji     |Wymagane |Tak  |Nie  |Nie | Nie |Nie |
|Wdróż zdefiniowane zasoby     |Nie |Nie  |Yes  |Nie | Nie |Nie |
|Tworzenie w pełni zgodnych środowisk      |Wymagane |Wymagane  |Wymagane  |Tak | Nie |Nie |
|Zasady inspekcji      |Tak |Nie  |Nie  |Nie | Nie |Nie |
|Tworzenie zapytań dotyczących zasobów platformy Azure      |Nie |Nie  |Nie  |Nie |Yes |Nie |
|Raport dotyczący kosztów zasobów      |Nie |Nie  |Nie  |Nie |Nie |Tak |

Poniżej znajdują się dodatkowe narzędzia, które mogą być wymagane do osiągnięcia określonych celów przyspieszenia wdrożenia. Często te narzędzia są używane poza zespołem nadzoru, ale nadal są uważane za aspekty przyspieszenia wdrożenia jako dyscypliny.

|  | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Usługa Azure DevOps](https://docs.microsoft.com/azure/devops/index) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|
|Wdrażanie ręczne (pojedynczy element zawartości)     | Tak | Yes  | Nie  | Nie efektywnie | Nie | Tak |
|Wdrażanie ręczne (pełne środowisko)     | Nie efektywnie | Tak | Nie  | Nie efektywnie | Nie | Tak |
|Zautomatyzowane wdrażanie (pełne środowisko)     | Nie  | Yes  | Nie  | Yes  | Nie | Tak |
|Aktualizacja konfiguracji pojedynczego zasobu     | Tak | Tak | Nie efektywnie | Nie efektywnie | Nie | Tak — podczas replikacji |
|Aktualizacja konfiguracji pełnego środowiska     | Nie efektywnie | Tak | Yes | Yes  | Nie | Tak — podczas replikacji |
|Zarządzanie dryfem konfiguracji     | Nie efektywnie | Nie efektywnie | Tak  | Yes  | Nie | Tak — podczas replikacji |
|Utwórz zautomatyzowany potok, aby wdrożyć kod i skonfigurować zasoby (DevOps)     | Nie | Nie | Nie | Yes | Nie | Nie |

Oprócz narzędzi macierzystych platformy Azure wymienionych powyżej często klienci mogą korzystać z narzędzi innych firm, aby ułatwić przyspieszenie wdrożenia i wdrożenia DevOps.
