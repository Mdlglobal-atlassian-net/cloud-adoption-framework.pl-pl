---
title: Automatyzowanie dołączania
description: Użyj plików przykładowych dołączania, aby ułatwić sobie automatyzację wdrożenia usług zarządzania serwerem Azure w celu zwiększenia wydajności.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: cb612930318ed2ecd355cb5466f50650086d7f4c
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80430568"
---
# <a name="automate-onboarding"></a>Automatyzowanie dołączania

Aby zwiększyć wydajność wdrażania usług zarządzania systemu Azure, należy rozważyć automatyzację wdrożenia zgodnie z opisem w poprzednich sekcjach niniejszych wskazówek. Skrypt i przykładowe szablony podane w poniższych sekcjach są punktami początkowymi do tworzenia własnych automatyzacji procesów dołączania.

Te wskazówki zawierają obsługę repozytorium GitHub przykładowego kodu, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples). Repozytorium zawiera przykładowe skrypty i szablony Azure Resource Manager, które ułatwiają automatyzację wdrażania usług zarządzania serwerem Azure.

Przykładowe pliki ilustrują sposób korzystania z Azure PowerShell poleceń cmdlet do automatyzacji następujących zadań:

- Utwórz [obszar roboczy log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access). (Lub Użyj istniejącego obszaru roboczego, jeśli spełnia wymagania. Aby uzyskać szczegółowe informacje, zobacz [Planowanie obszaru roboczego](./prerequisites.md#log-analytics-workspace-and-automation-account-planning).

- Utwórz konto usługi Automation. (Lub Użyj istniejącego konta, jeśli spełnia wymagania. Aby uzyskać szczegółowe informacje, zobacz temat [Planowanie obszaru roboczego](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

- Połącz konto usługi Automation i obszar roboczy Log Analytics. Ten krok nie jest wymagany, jeśli użytkownik jest dołączany przy użyciu Azure Portal.

- Włącz Update Management i Change Tracking i spis dla obszaru roboczego.

- Dołączanie maszyn wirtualnych platformy Azure przy użyciu Azure Policy. Zasady instalują agenta Log Analytics i Agent zależności Microsoft na maszynach wirtualnych platformy Azure.

- Dołączanie serwerów lokalnych przez zainstalowanie na nich agenta Log Analytics.

Pliki opisane w poniższej tabeli są używane w tym przykładzie. Można je dostosować do obsługi własnych scenariuszy wdrażania.

| Nazwa pliku | Opis |
|-----------|-------------|
| New-AMSDeployment. ps1 | Główny, aranżacja skrypt, który automatyzuje dołączanie. Tworzy grupy zasobów, lokalizacje, obszary robocze i konta usługi Automation, jeśli jeszcze nie istnieją. Ten skrypt programu PowerShell wymaga istniejącej subskrypcji. |
| Workspace — AutomationAccount. JSON | Szablon Menedżer zasobów, który służy do wdrażania zasobów obszaru roboczego i konta usługi Automation. |
| WorkspaceSolutions. JSON | Szablon Menedżer zasobów, który umożliwia korzystanie z żądanych rozwiązań w obszarze roboczym Log Analytics. |
| ScopeConfig. JSON | Menedżer zasobów szablon, który używa modelu zgody dla serwerów lokalnych z rozwiązaniem Change Tracking. Korzystanie z modelu zgody jest opcjonalne. |
| Enable-VMInsightsPerfCounters. ps1 | Skrypt programu PowerShell, który umożliwia usłudze VM Insights dla serwerów i konfiguruje liczniki wydajności. |
| Śledzenia zmian-FileList. JSON | Szablon Menedżer zasobów, który definiuje listę plików, które będą monitorowane przez Change Tracking. |

Użyj następującego polecenia, aby uruchomić New-AMSDeployment. ps1:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak skonfigurować podstawowe alerty w celu powiadomienia zespołu o zdarzeniach i problemach związanych z zarządzaniem kluczami.

> [!div class="nextstepaction"]
> [Konfigurowanie podstawowych alertów](./setup-alerts.md)
