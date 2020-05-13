---
title: Typowe przykłady Azure Policy
description: Użyj struktury wdrażania w chmurze dla platformy Azure, aby zapewnić zgodność z wymaganiami dotyczącymi zasad, tworząc zasady za pomocą poleceń cmdlet programu PowerShell.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 074762c6d02c6da1cd6812064e20f63a44aa4bd7
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217289"
---
# <a name="common-azure-policy-examples"></a>Typowe przykłady Azure Policy

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) może pomóc w zastosowaniu ładu w zasobach w chmurze. Ta usługa może pomóc w tworzeniu guardrails, które zapewniają zgodność całej firmy z wymaganiami dotyczącymi zasad zarządzania. Aby utworzyć zasady, użyj Azure Portal lub poleceń cmdlet programu PowerShell. W tym artykule przedstawiono przykłady poleceń cmdlet programu PowerShell.

> [!NOTE]
> W przypadku Azure Policy zasady wymuszania (**deployIfNotExists**) nie są automatycznie wdrażane na istniejących maszynach wirtualnych. Aby zachować zgodność z maszynami wirtualnymi, należy przeprowadzić korygowanie. Aby uzyskać więcej informacji, zobacz [korygowanie niezgodnych zasobów przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Typowe przykłady zasad

W poniższych sekcjach opisano niektóre powszechnie używane zasady.

### <a name="restrict-resource-regions"></a>Ograniczanie regionów zasobów

Zgodność z przepisami i zasadami często zależy od kontroli lokalizacji fizycznej, w której są wdrażane zasoby. Możesz użyć wbudowanych zasad, aby zezwolić użytkownikom na tworzenie zasobów tylko w niektórych dozwolonych regionach świadczenia usługi Azure.

Aby znaleźć te zasady w portalu, wyszukaj frazę "lokalizacja" na stronie definicji zasad. Lub Uruchom to polecenie cmdlet, aby znaleźć zasady:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq 'BuiltIn') -and ($_.Properties.displayName -like '*location*') }
```

Poniższy skrypt przedstawia sposób przypisywania zasad. Zmień `$SubscriptionID` wartość tak, aby wskazywała na subskrypcję, do której chcesz przypisać zasady. Przed uruchomieniem skryptu Użyj polecenia cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) , aby się zalogować.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{ "listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyParam
```

Za pomocą tego skryptu można również zastosować inne zasady omówione w tym artykule. Wystarczy zamienić identyfikator GUID w wierszu, który ustawia `$AllowedLocationPolicy` Identyfikator GUID zasad, które chcesz zastosować.

### <a name="block-certain-resource-types"></a>Blokuj wybrane typy zasobów

Do blokowania niektórych typów zasobów można także użyć innych zasad wbudowanych, które służą do kontrolowania kosztów.

Aby znaleźć te zasady w portalu, wyszukaj ciąg "dozwolone typy zasobów" na stronie definicji zasad. Lub Uruchom to polecenie cmdlet, aby znaleźć zasady:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Po określeniu zasad, które mają być używane, można zmodyfikować przykład programu PowerShell w sekcji [Ogranicz obszary zasobów](#restrict-resource-regions) , aby przypisać zasady.

### <a name="restrict-vm-size"></a>Ogranicz rozmiar maszyny wirtualnej

Platforma Azure oferuje szeroką gamę rozmiarów maszyn wirtualnych do obsługi różnych obciążeń. Aby kontrolować budżet, możesz utworzyć zasady, które zezwalają na tylko podzbiór rozmiarów maszyn wirtualnych w Twoich subskrypcjach.

### <a name="deploy-antimalware"></a>Wdróż oprogramowanie chroniące przed złośliwym kodem

Za pomocą tych zasad można wdrożyć rozszerzenie Microsoft _IaaSAntimalware_ z konfiguracją domyślną na maszynach wirtualnych, które nie są chronione przez oprogramowanie chroniące przed złośliwym kodem.

Identyfikator GUID zasad to `2835b622-407b-4114-9198-6f7064cbe0dc` .

Poniższy skrypt przedstawia sposób przypisywania zasad. Aby użyć skryptu, Zmień `$SubscriptionID` wartość tak, aby wskazywała na subskrypcję, do której chcesz przypisać zasady. Przed uruchomieniem skryptu Użyj polecenia cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0) , aby się zalogować.

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location "eastus" with the value that you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat innych dostępnych narzędzi i usług zarządzania serwerem.

> [!div class="nextstepaction"]
> [Narzędzia i usługi zarządzania serwerem platformy Azure](./tools-services.md)
