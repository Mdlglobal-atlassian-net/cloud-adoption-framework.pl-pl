---
title: Tworzenie harmonogramów aktualizacji
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak zarządzać harmonogramami aktualizacji za pomocą Azure Portal lub nowych modułów poleceń cmdlet programu PowerShell.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 64f2ee1d148cc769325bdb60dabe2deba5d04351
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80356334"
---
# <a name="create-update-schedules"></a>Tworzenie harmonogramów aktualizacji

Harmonogramy aktualizacji można zarządzać przy użyciu Azure Portal lub nowych modułów poleceń cmdlet programu PowerShell.

Aby utworzyć harmonogram aktualizacji za pośrednictwem Azure Portal, zobacz [Planowanie wdrożenia aktualizacji](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

Moduł AZ. Automation obsługuje teraz Konfigurowanie zarządzania aktualizacjami przy użyciu Azure PowerShell. [Wersja 1.7.0](https://www.powershellgallery.com/packages/Az/1.7.0) modułu dodaje obsługę polecenia cmdlet [New-AzAutomationUpdateManagementAzureQuery](https://docs.microsoft.com/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0) . To polecenie cmdlet umożliwia użycie tagów, lokalizacji i zapisanych wyszukiwań w celu skonfigurowania harmonogramów aktualizacji dla elastycznej grupy maszyn.

## <a name="example-script"></a>Przykładowy skrypt

Przykładowy skrypt w tej sekcji ilustruje użycie tagowania i wykonywania zapytań w celu utworzenia dynamicznych grup maszyn, do których można zastosować harmonogramy aktualizacji. Wykonuje następujące czynności. Można odwołać się do implementacji określonych akcji podczas tworzenia własnych skryptów.

- Tworzy harmonogram aktualizacji Azure Automation, który jest uruchamiany w każdą sobotę o godzinie 8:00.
- Tworzy zapytanie dla komputerów spełniających następujące kryteria:
  - Wdrożone w lokalizacji `westus`, `eastus`lub `eastus2` platformy Azure
  - Do nich zastosowano tag `Owner` z wartością ustawioną na `JaneSmith`
  - Do nich zastosowano tag `Production` z wartością ustawioną na `true`
- Stosuje harmonogram aktualizacji do maszyn z kwerendą i ustawia dwugodzinne okno aktualizacji.

Przed uruchomieniem skryptu przykładowego należy się zalogować przy użyciu polecenia cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po uruchomieniu skryptu podaj następujące informacje:

- Identyfikator subskrypcji docelowej
- Docelowa Grupa zasobów
- Nazwa obszaru roboczego Log Analytics
- Nazwa konta Azure Automation

```powershell

    <#
        .SYNOPSIS
            This script orchestrates the deployment of the solutions and the agents.
        .Parameter SubscriptionName
        .Parameter WorkspaceName
        .Parameter AutomationAccountName
        .Parameter ResourceGroupName

    #>

    param (
        [Parameter(Mandatory=$true)]
        [string]$SubscriptionId,

        [Parameter(Mandatory=$true)]
        [string]$ResourceGroupName,

        [Parameter(Mandatory=$true)]
        [string]$WorkspaceName,

        [Parameter(Mandatory=$true)]
        [string]$AutomationAccountName,

        [Parameter(Mandatory=$false)]
        [string]$scheduleName = "SaturdayCriticalSecurity"
    )

    Import-Module Az.Automation

    $startTime = ([DateTime]::Now).AddMinutes(10)
    $schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -StartTime $startTime `
        -Name $scheduleName `
        -Description "Saturday patches" `
        -DaysOfWeek Saturday `
        -WeekInterval 1 `
        -ForUpdateConfiguration

    # Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

    $queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

    $query1Location =@("westus", "eastus", "eastus2")
    $query1FilterOperator = "Any"
    $ownerTag = @{"Owner"= @("JaneSmith")}
    $ownerTag.add("Production", "true")

    $DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Scope $queryScope `
        -Tag $ownerTag

    $AzureQueries = @($DGQuery)

    $UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
        -AutomationAccountName $AutomationAccountName `
        -Schedule $schedule `
        -Windows `
        -Duration (New-TimeSpan -Hours 2) `
        -AzureQuery $AzureQueries `
        -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z przykładami dotyczącymi implementacji [wspólnych zasad na platformie Azure](./common-policies.md) , które mogą pomóc zarządzać serwerami.

> [!div class="nextstepaction"]
> [Typowe zasady na platformie Azure](./common-policies.md)
