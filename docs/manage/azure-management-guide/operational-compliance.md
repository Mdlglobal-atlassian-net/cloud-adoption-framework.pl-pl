---
title: Zgodność operacyjna na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zapewnianie stabilności biznesowej dzięki zwiększeniu zgodności operacyjnej
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7073df6b697da49429d4086d9f8f3f113583e52d
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557095"
---
# <a name="operational-compliance-in-azure"></a>Zgodność operacyjna na platformie Azure

Zgodność operacyjna to druga dyscyplina w planie bazowym zarządzania chmurą.

![Plan bazowy zarządzania chmurą](../../_images/manage/management-baseline.png)

Poprawa zgodności operacyjnej zmniejsza prawdopodobieństwo wystąpienia awarii związanej z odchyleniem konfiguracji lub pojawienia się luk w zabezpieczeniach spowodowanych niestosowaniem prawidłowych poprawek systemów.

Poniższa tabela zawiera sugerowane wartości minimalne planu bazowego zarządzania dla dowolnego środowiska klasy korporacyjnej.

|Proces  |Narzędzie  |Przeznaczenie  |
|---------|---------|---------|
|Zarządzanie poprawkami|Zarządzanie aktualizacjami|Planowanie aktualizacji i zarządzanie nimi|
|Wymuszanie zasad|Azure Policy|Wymuszanie zasad w celu zapewnienia zgodności środowiska i gościa|
|Środowisko — Konfigurowanie|Azure Blueprint|Zautomatyzowana zgodność dla podstawowych usług|

::: zone target="docs"

## <a name="update-management"></a>Zarządzanie aktualizacjami

::: zone-end
::: zone target="chromeless"

## <a name="update-managementtabupdatemanagement"></a>[Zarządzanie aktualizacjami](#tab/UpdateManagement)

::: zone-end

W celu przeprowadzania ocen i wdrożeń aktualizacji na komputerach zarządzanych przez rozwiązanie Update Management są używane następujące konfiguracje:

- Program Microsoft Monitoring Agent (MMA) dla systemu Windows lub Linux
- Platforma PowerShell Desired State Configuration (DSC) dla systemu Linux
- Hybrydowy proces roboczy elementu runbook usługi Automation
- Usługa Microsoft Update lub Windows Server Update Services (WSUS) dla komputerów z systemem Windows

Aby uzyskać więcej informacji, zobacz [Rozwiązanie Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)

> [!WARNING]
> Przed rozpoczęciem korzystania z rozwiązania Update Management należy dołączyć maszyny wirtualne lub całą subskrypcję do usług Log Analytics i Azure Automation.
> Dostępne są dwie metody dołączania — przed rozpoczęciem korzystania z rozwiązania Update Management należy wybrać jedną z nich.
>
> - [Pojedyncza maszyna wirtualna](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-single-vm)
> - [Cała subskrypcja](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/azure-server-management/onboard-at-scale)

### <a name="manage-updates"></a>Zarządzanie aktualizacjami

Aby zastosować zasady do grupy zasobów:

1. Wybierz pozycję [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts).
2. Wybierz z listy **konto usługi Automation**.
3. Znajdź sekcję **Zarządzanie konfiguracją** w obszarze nawigacji w portalu.
4. Tworzenie spisu, zarządzanie zmianami i konfiguracja stanu — dowolnej z tych usług można używać do kontrolowania stanu i zgodności operacyjnej zarządzanych maszyn wirtualnych.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Usługa Azure Policy jest używana w procesach nadzoru nad ładem. Jednak jest ona również pomocna w procesach zarządzania chmurą. Oprócz przeprowadzania inspekcji i korygowania zasobów platformy Azure za pomocą usługi Azure Policy można przeprowadzać inspekcję ustawień wewnątrz maszyny. Taka weryfikacja jest wykonywana przez klienta i rozszerzenie konfiguracji gościa. Rozszerzenie to, obsługiwane za pośrednictwem klienta, umożliwia weryfikację następujących ustawień:

- Konfiguracja systemu operacyjnego
- Konfiguracja lub obecność aplikacji
- Ustawienia środowiska

Aktualnie konfiguracja gościa usługi Azure Policy umożliwia przeprowadzanie tylko inspekcji ustawień wewnątrz maszyny. Stosowanie konfiguracji nie jest obsługiwane.

::: zone target="chromeless"

### <a name="action"></a>Akcja

Przypisz wbudowane zasady do grupy zarządzania, subskrypcji lub grupy zasobów.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

### <a name="apply-a-policy"></a>Stosowanie zasad

Aby zastosować zasady do grupy zasobów:

1. Przejdź do usługi [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Wybierz pozycję **Przypisz zasady**.

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Azure Policy — konfiguracja gościa](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących wymuszania zasad](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprints

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

::: zone-end

Usługa Azure Blueprints umożliwia architektom chmury i centralnym grupom technologii informatycznych zdefiniowanie powtarzalnego zestawu zasobów platformy Azure, który implementuje standardy, wzorce i wymagania organizacji oraz jest z nimi zgodny. Usługa Azure Blueprints umożliwia zespołom programistów szybkie tworzenie i wdrażanie nowych środowisk z przekonaniem, że zostały one utworzone zgodnie z zasadami organizacji za pomocą zestawu wbudowanych składników — takich jak sieć — przyspieszających opracowywanie i dostarczanie.

Usługa Blueprints umożliwia deklaratywne organizowanie i wdrażanie różnych szablonów zasobów i innych artefaktów, takich jak:

- Przypisania ról.
- Przypisania zasad.
- Szablony usługi Azure Resource Manager.
- Grupy zasobów.

Zastosowanie strategii może wymusić zgodność operacyjną w środowisku, jeśli nie zostało to jeszcze zrobione przez zespół ds. utrzymania ładu w chmurze.

### <a name="create-a-blueprint"></a>Tworzenie strategii

Aby utworzyć strategię:

::: zone target="chromeless"

1. Przejdź do pozycji **Blueprints — Wprowadzenie**.
1. W sekcji **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. Wprowadź **nazwę strategii** i wybierz odpowiednią **lokalizację definicji**.
1. Kliknij przycisk **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Kliknij pozycję **Zapisz wersję roboczą**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Przejdź do pozycji [Blueprints — Wprowadzenie](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. W sekcji **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. Wprowadź **nazwę strategii** i wybierz odpowiednią **lokalizację definicji**.
1. Kliknij przycisk **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Kliknij pozycję **Zapisz wersję roboczą**.

::: zone-end

### <a name="publish-a-blueprint"></a>Publikowanie strategii

Aby opublikować artefakty strategii w subskrypcji:

::: zone target="chromeless"

1. Przejdź obszaru **Strategie — Definicje strategii**.
1. Wybierz strategię utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. Podaj **wersję** (np. „1.0”) i wszelkie **uwagi dotyczące zmian**, a następnie wybierz pozycję **Publikuj**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Przejdź obszaru [Strategie — Definicje strategii](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wybierz strategię utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. Podaj **wersję** (np. „1.0”) i wszelkie **uwagi dotyczące zmian**, a następnie wybierz pozycję **Publikuj**.

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących spójności zasobów](../../decision-guides/resource-consistency/index.md)
- [Przykłady strategii opartych na standardach](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
