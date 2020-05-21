---
title: Zgodność operacyjna na platformie Azure
description: Dowiedz się, jak zapewnić stabilność biznesową w ramach zgodności operacyjnej dzięki zmniejszeniu prawdopodobieństwa awarii lub ograniczeniu luk w zabezpieczeniach.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7aeb83064faa4105214d47149fbf9e789add47d3
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621221"
---
<!-- cSpell:ignore WSUS getting started -->

# <a name="operational-compliance-in-azure"></a>Zgodność operacyjna na platformie Azure

_Zgodność operacyjna_ to druga dyscyplina w planie bazowym zarządzania chmurą.

![Plan bazowy zarządzania chmurą](../../_images/manage/management-baseline.png)

Poprawa zgodności operacyjnej zmniejsza prawdopodobieństwo wystąpienia awarii związanej z odchyleniem konfiguracji lub pojawienia się luk w zabezpieczeniach spowodowanych zastosowaniem nieprawidłowych poprawek systemów.

Ta tabela zawiera sugerowane wartości minimalne planu bazowego zarządzania dla dowolnego środowiska klasy korporacyjnej.

| Proces | Narzędzie | Przeznaczenie |
|---|---|---|
| Zarządzanie poprawkami | Zarządzanie aktualizacjami | Planowanie aktualizacji i zarządzanie nimi |
| Wymuszanie zasad | Azure Policy | Wymuszanie zasad w celu zapewnienia zgodności środowiska i gościa |
| Konfiguracja środowiska | Azure Blueprints | Zautomatyzowana zgodność dla podstawowych usług |
| Konfiguracja zasobu | Desired State Configuration | Zautomatyzowana konfiguracja w systemie operacyjnym gościa i niektóre aspekty środowiska |

::: zone target="docs"

## <a name="update-management"></a>Zarządzanie aktualizacjami

::: zone-end
::: zone target="chromeless"

## <a name="update-management"></a>[Zarządzanie aktualizacjami](#tab/UpdateManagement)

::: zone-end

W celu przeprowadzania ocen i wdrożeń aktualizacji na komputerach zarządzanych przez rozwiązanie Update Management są używane następujące konfiguracje:

- Program Microsoft Monitoring Agent (MMA) dla systemu Windows lub Linux.
- Platforma PowerShell Desired State Configuration (DSC) dla systemu Linux.
- Hybrydowy proces roboczy elementu Runbook w usłudze Azure Automation.
- Usługa Microsoft Update lub Windows Server Update Services (WSUS) dla komputerów z systemem Windows.

Aby uzyskać więcej informacji, zobacz [Rozwiązanie Update Management](https://docs.microsoft.com/azure/automation/automation-update-management).

> [!WARNING]
> Przed rozpoczęciem korzystania z rozwiązania Update Management należy dołączyć maszyny wirtualne lub całą subskrypcję do usług Log Analytics i Azure Automation.
>
> Wyróżniamy dwie metody dołączania:
>
> - [Pojedyncza maszyna wirtualna](../../manage/azure-server-management/onboard-single-vm.md)
> - [Cała subskrypcja](../../manage/azure-server-management/onboard-at-scale.md)
>
> Przed kontynuowaniem korzystania z rozwiązania Update Management należy wybrać jedną z nich.

### <a name="manage-updates"></a>Zarządzanie aktualizacjami

Aby zastosować zasady do grupy zasobów:

1. Wybierz pozycję [Azure Automation](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts).
1. Wybierz pozycję **Konta usługi Automation** i zaznacz jedno z wyświetlonych kont.
1. Przejdź do obszaru **Zarządzanie konfiguracją**.
1. Do kontrolowania stanu i zgodności operacyjnej zarządzanych maszyn wirtualnych można używać usług **Tworzenie spisu**, **Zarządzanie zmianami** i **Konfiguracja stanu**.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Assign Policy" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

## <a name="azure-policy"></a>Azure Policy

::: zone-end
::: zone target="chromeless"

## <a name="azure-policy"></a>[Azure Policy](#tab/AzurePolicy)

::: zone-end

Usługa Azure Policy jest używana w procesach nadzoru nad ładem. Jest ona również pomocna w procesach zarządzania chmurą. Za pomocą usługi Azure Policy można przeprowadzać inspekcję i korygowanie zasobów platformy Azure, a także inspekcję ustawień wewnątrz maszyny. Taka weryfikacja jest wykonywana przez klienta i rozszerzenie konfiguracji gościa. Rozszerzenie to, obsługiwane za pośrednictwem klienta, umożliwia weryfikację następujących ustawień:

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
- [Azure Policy: Konfiguracja gościa](https://docs.microsoft.com/azure/governance/policy/concepts/guest-configuration)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących wymuszania zasad](../../decision-guides/policy-enforcement/index.md)

## <a name="azure-blueprints"></a>Azure Blueprints

::: zone-end
::: zone target="chromeless"

## <a name="azure-blueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

::: zone-end

Dzięki usłudze Azure Blueprints architekci chmury i główne grupy IT mogą definiować powtarzalny zestaw zasobów platformy Azure. Te zasoby implementują standardy, wzorce i wymagania organizacji oraz zapewniają zgodność z nimi.

Usługa Azure Blueprints umożliwia zespołom programistycznym szybkie tworzenie i wdrażania nowych środowisk. Zespoły mogą również mieć pewność, że tworzone środowiska są zgodne ze standardami organizacji. Wszystko to dzięki zestawowi wbudowanych składników, na przykład do obsługi sieci, które przyspieszają proces programowania i dostarczania.

Usługa Blueprints umożliwia deklaratywne organizowanie i wdrażanie różnych szablonów zasobów i innych artefaktów, takich jak:

- Przypisania ról.
- Przypisania zasad.
- Szablony usługi Azure Resource Manager.
- Grupy zasobów.

Zastosowanie strategii może wymusić zgodność operacyjną w środowisku, jeśli nie zostało to jeszcze zrobione przez zespół ds. utrzymania ładu w chmurze.

### <a name="create-a-blueprint"></a>Tworzenie strategii

Aby utworzyć strategię:

::: zone target="chromeless"

1. Przejdź do sekcji **Strategie: wprowadzenie**.
1. W okienku **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. W polu **Nazwa strategii** wprowadź nazwę strategii.
1. Wybierz pozycję **Lokalizacja definicji**, a następnie wybierz odpowiednią lokalizację.
1. Wybierz opcję **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Wybierz pozycję **Zapisz wersję roboczą**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Przejdź do sekcji [Strategie: wprowadzenie](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. W okienku **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. W polu **Nazwa strategii** wprowadź nazwę strategii.
1. Wybierz pozycję **Lokalizacja definicji**, a następnie wybierz odpowiednią lokalizację.
1. Wybierz opcję **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Wybierz pozycję **Zapisz wersję roboczą**.

::: zone-end

### <a name="publish-a-blueprint"></a>Publikowanie strategii

Aby opublikować artefakty strategii w subskrypcji:

::: zone target="chromeless"

1. Przejdź obszaru **Strategie — Definicje strategii**.
1. Wybierz strategię utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. W polu **Wersja** wprowadź numer wersji, na przykład „1.0”.
1. W polu **Uwagi dotyczące zmian** wprowadź uwagi.
1. Wybierz pozycję **Publikuj**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Przejdź do sekcji [Strategie: Definicje strategii](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wybierz strategię utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. W polu **Wersja** wprowadź numer wersji, na przykład „1.0”.
1. W polu **Uwagi dotyczące zmian** wprowadź uwagi.
1. Wybierz pozycję **Publikuj**.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących spójności zasobów](../../decision-guides/resource-consistency/index.md)
- [Przykłady strategii opartych na standardach](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end
