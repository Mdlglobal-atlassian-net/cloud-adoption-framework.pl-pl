---
title: Zasady konfiguracji gościa
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak używać rozszerzenia konfiguracji gościa Azure Policy do inspekcji ustawień konfiguracji na maszynie wirtualnej platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 938934e1a45d8f8abebede6cca8dcd9987cfb7e0
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861467"
---
# <a name="guest-configuration-policy"></a>Zasady konfiguracji gościa

Aby przeprowadzić inspekcję ustawień konfiguracji maszyny wirtualnej, można użyć rozszerzenia [konfiguracji gościa](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration) Azure Policy. Konfiguracja gościa jest obecnie obsługiwana tylko na maszynach wirtualnych platformy Azure.

Aby znaleźć listę zasad konfiguracji gościa, wyszukaj "Konfiguracja gościa" na stronie portalu Azure Policy. Lub Uruchom to polecenie cmdlet w oknie programu PowerShell, aby znaleźć listę:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Funkcja konfiguracji gościa jest regularnie aktualizowana w celu obsługi dodatkowych zestawów zasad. Regularnie sprawdzaj dostępność nowych obsługiwanych zasad i Oceń, czy będą one przydatne.

<!-- TODOBACKLOG: Update these links when available. 

By default, we recommend that you enable the following policies:

- **Preview:** Audit to verify that password-security settings are correct on Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Wdrożenie

Użyj następującego przykładowego skryptu programu PowerShell, aby wdrożyć te zasady w następujący sposób:

- Sprawdź, czy ustawienia zabezpieczeń hasła na komputerach z systemem Windows i Linux są ustawione prawidłowo.
- Sprawdź, czy certyfikaty nie zbliżają się do wygaśnięcia na maszynach wirtualnych z systemem Windows.

 Przed uruchomieniem tego skryptu Użyj polecenia cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) , aby się zalogować. Po uruchomieniu skryptu należy podać nazwę subskrypcji, do której chcesz zastosować zasady.

```powershell

    # Assign Guest Configuration policy.

    param (
        [Parameter(Mandatory=$true)]
        [string] $SubscriptionName
    )

    $Subscription = Get-AzSubscription -SubscriptionName $SubscriptionName
    $scope = "/subscriptions/" + $Subscription.Id

    $PasswordPolicy = Get-AzPolicySetDefinition -Name "3fa7cbf5-c0a4-4a59-85a5-cca4d996d5a6"
    $CertExpirePolicy = Get-AzPolicySetDefinition -Name "b6f5e05c-0aaa-4337-8dd4-357c399d12ae"

    New-AzPolicyAssignment -Name "PasswordPolicy" -DisplayName "[Preview]: Audit that password security settings are set correctly inside Linux and Windows machines" -Scope $scope -PolicySetDefinition $PasswordPolicy -AssignIdentity -Location eastus

    New-AzPolicyAssignment -Name "CertExpirePolicy" -DisplayName "[Preview]: Audit that certificates are not expiring on Windows VMs" -Scope $scope -PolicySetDefinition $CertExpirePolicy -AssignIdentity -Location eastus

```

## <a name="next-steps"></a>Następne kroki

Dowiedz się [, jak włączyć śledzenie zmian i alerty](./enable-tracking-alerting.md) w przypadku krytycznych zmian plików, usług, oprogramowania i rejestru.

> [!div class="nextstepaction"]
> [Włącz śledzenie i alerty dla zmian krytycznych](./enable-tracking-alerting.md)
