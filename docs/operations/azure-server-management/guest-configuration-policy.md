---
title: Zasady konfiguracji gościa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zasady konfiguracji gościa
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d51cef67c96057b1929ed8cc86396f20338e932b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70833221"
---
# <a name="guest-configuration-policy"></a>Zasady konfiguracji gościa

Rozszerzenie [konfiguracji gościa](/azure/governance/policy/concepts/guest-configuration) Azure Policy umożliwia inspekcję ustawień konfiguracji na maszynie wirtualnej. Konfiguracja gościa jest obecnie obsługiwana tylko na maszynach wirtualnych platformy Azure.

Listę zasad konfiguracji gościa można znaleźć, wyszukując kategorię "Konfiguracja gościa" na stronie portalu Azure Policy. Możesz również znaleźć listę, uruchamiając to polecenie cmdlet w oknie programu PowerShell:

```powershell
Get-AzPolicySetDefinition | where-object {$_.Properties.metadata.category -eq "Guest Configuration"}
```

> [!NOTE]
> Funkcja konfiguracji gościa jest regularnie aktualizowana w celu obsługi dodatkowych zestawów zasad. Sprawdzaj, czy nowe obsługiwane zasady są okresowo i oceniaj, czy są one przydatne w Twoich potrzebach.

<!-- TODO: Update these links when available. 

By default, we recommend enabling the following policies:

- [Preview]: Audit to verify password security settings are set correctly inside Linux and Windows machines.
- Audit to verify that certificates are not nearing expiration on Windows VMs.

-->

## <a name="deployment"></a>Wdrożenie

Aby wdrożyć te zasady, można użyć następującego przykładowego skryptu programu PowerShell:

- Sprawdź, czy ustawienia zabezpieczeń hasła na komputerach z systemem Windows i Linux są ustawione prawidłowo.
- Sprawdź, czy certyfikaty nie zbliżają się do wygaśnięcia na maszynach wirtualnych z systemem Windows.

 Przed uruchomieniem tego skryptu należy zalogować się przy użyciu polecenia cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) . Po uruchomieniu skryptu należy podać nazwę subskrypcji, do której chcesz zastosować zasady.

```powershell
#Assign Guest Configuration policy.
param (
    [Parameter(Mandatory=$true)]
    [string]$SubscriptionName
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
