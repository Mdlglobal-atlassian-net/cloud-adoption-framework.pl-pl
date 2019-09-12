---
title: Zautomatyzowana konfiguracja dołączania i alertu
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zautomatyzowana konfiguracja dołączania i alertu
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 86997d8c433c23d6ecbe5d3ac124623d318099c0
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833091"
---
# <a name="automate-onboarding"></a>Automatyzowanie dołączania

Aby zwiększyć wydajność wdrażania usług zarządzania systemu Azure, należy rozważyć automatyzację wdrażania usług zarządzania przy użyciu rekomendacji omówionych w poprzednich sekcjach niniejszych wskazówek. Skrypt i przykładowe szablony, które znajdują się w poniższych sekcjach, są punktami początkowymi do tworzenia własnych automatyzacji procesów dołączania.

## <a name="onboarding-by-using-automation"></a>Dołączanie przy użyciu automatyzacji

Te wskazówki zawierają obsługę repozytorium GitHub przykładowego kodu, [CloudAdoptionFramework](https://aka.ms/CAF/manage/automation-samples), który zawiera przykładowe skrypty i szablony Azure Resource Manager ułatwiające automatyzację wdrażania usług zarządzania serwerem Azure.

Te przykładowe pliki ilustrują sposób korzystania z Azure PowerShell poleceń cmdlet do automatyzacji następujących zadań:

1. Utwórz [obszar roboczy log Analytics](/azure/azure-monitor/platform/manage-access) (lub Użyj istniejącego obszaru roboczego, jeśli spełnia wymagania&mdash;, zobacz [Planowanie obszaru roboczego](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Utwórz konto usługi Automation (lub Użyj istniejącego konta, jeśli spełnia wymagania&mdash;, zobacz [Planowanie obszaru roboczego](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Połącz konto usługi Automation z obszarem roboczym Log Analytics (niewymagane w przypadku przechodzenia przez portal).

4. Włącz Update Management i Change Tracking i spis dla obszaru roboczego.

5. Dołączanie maszyn wirtualnych platformy Azure przy użyciu Azure Policy (zasady instalują Log Analytics agenta i Agent zależności na maszynach wirtualnych platformy Azure).

6. Dołączanie serwerów lokalnych przez zainstalowanie na nich agenta Log Analytics.

Pliki opisane w poniższej tabeli są używane w tym przykładzie i można je dostosować do obsługi własnych scenariuszy wdrażania.

| Nazwa pliku | Opis |
|-----------|-------------|
| New-AMSDeployment.ps1 | Główny, aranżacja skrypt, który automatyzuje dołączanie. Ten skrypt programu PowerShell wymaga istniejącej subskrypcji, ale spowoduje utworzenie grup zasobów, lokalizacji, obszaru roboczego i kont usługi Automation, jeśli nie istnieją. |
| Workspace-AutomationAccount.json | Szablon Menedżer zasobów, który służy do wdrażania zasobów obszaru roboczego i konta usługi Automation. |
| WorkspaceSolutions.json | Szablon Menedżer zasobów, który umożliwia korzystanie z żądanych rozwiązań w obszarze roboczym Log Analytics. |
| ScopeConfig.json | Szablon Menedżer zasobów, który używa modelu zgody dla serwerów lokalnych z rozwiązaniem do śledzenia zmian. Korzystanie z modelu zgody jest opcjonalne. |
| Enable-VMInsightsPerfCounters.ps1 | Skrypt programu PowerShell, który umożliwia VMInsight dla serwerów i konfiguruje liczniki wydajności. |
| ChangeTracking-Filelist.json | Szablon Menedżer zasobów, który definiuje listę plików, które będą monitorowane przez Change Tracking. |

Można uruchomić New-AMSDeployment. ps1 przy użyciu następującego polecenia:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak skonfigurować podstawowe alerty w celu powiadomienia zespołu o zdarzeniach i problemach związanych z zarządzaniem kluczami.

> [!div class="nextstepaction"]
> [Konfigurowanie alertów podstawowych](./setup-alerts.md)
