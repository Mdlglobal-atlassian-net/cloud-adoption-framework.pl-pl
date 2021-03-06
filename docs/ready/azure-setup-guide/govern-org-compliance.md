---
title: Ład Azure, zabezpieczenia i zgodność
description: Dowiedz się, jak skonfigurować ład, zabezpieczenia i zgodność w środowisku platformy Azure przy użyciu podręcznika Cloud Adoption Framework dla platformy Azure.
author: tvuylsteke
ms.author: kfollis
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: a44dcdf49d2dad17236f4f1dc009758acf4230fc
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621624"
---
<!-- cSpell:ignore tvuylsteke >

<!-- markdownlint-disable MD024 MD025 -->

# <a name="governance-security-and-compliance-in-azure"></a>Ład, zabezpieczenia i zgodność na platformie Azure

Podczas ustanawiania zasad firmowych i planowania strategii utrzymywania ładu możesz skorzystać z narzędzi i usług, takich jak Azure Policy, Azure Blueprints i Azure Security Center, aby wymusić i zautomatyzować decyzje dotyczące ładu w organizacji. Przed rozpoczęciem planowania ładu, użyj [narzędzia do porównywania stanu nadzoru nad ładem](https://cafbaseline.com), aby zidentyfikować potencjalne luki w podejściu do ładu w organizacji. Aby uzyskać więcej informacji na temat opracowywania procesów ładu, zobacz [metodologię Ład](../../govern/index.md).

# <a name="azure-blueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

Usługa Azure Blueprints umożliwia architektom chmury i centralnym grupom technologii informatycznych zdefiniowanie powtarzalnego zestawu zasobów platformy Azure, który implementuje standardy, wzorce i wymagania organizacji oraz jest z nimi zgodny. Usługa Azure Blueprints umożliwia zespołom programistów szybkie tworzenie i wdrażanie nowych środowisk z przekonaniem, że zostały one utworzone zgodnie z zasadami organizacji za pomocą zestawu wbudowanych składników, takich jak sieć, przyspieszających opracowywanie i dostarczanie.

Usługa Blueprints umożliwia deklaratywne organizowanie i wdrażanie różnych szablonów zasobów i innych artefaktów, takich jak:

- Przypisania ról.
- Przypisania zasad.
- Szablony usługi Azure Resource Manager.
- Grupy zasobów.

## <a name="create-a-blueprint"></a>Tworzenie strategii

Aby utworzyć strategię:

::: zone target="chromeless"

1. Przejdź do sekcji **Strategie: wprowadzenie**.
1. W sekcji **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. Wprowadź **nazwę strategii** i wybierz odpowiednią **lokalizację definicji**.
1. Wybierz opcję **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Wybierz pozycję **Zapisz wersję roboczą**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Przejdź do sekcji [Strategie: wprowadzenie](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. W sekcji **Tworzenie strategii** wybierz pozycję **Utwórz**.
1. Przefiltruj listę strategii, aby wybrać odpowiednią strategię.
1. Wprowadź **nazwę strategii** i wybierz odpowiednią **lokalizację definicji**.
1. Wybierz opcję **Dalej: Artefakty >>** i przejrzyj artefakty uwzględnione w strategii.
1. Wybierz pozycję **Zapisz wersję roboczą**.

::: zone-end

## <a name="publish-a-blueprint"></a>Publikowanie strategii

Aby opublikować artefakty strategii w subskrypcji:

::: zone target="chromeless"

1. Przejdź do sekcji **Strategie: Definicje strategii**.
1. Wybierz strategię utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. Podaj **wersję** (np. _1.0_) i wszelkie **uwagi dotyczące zmian**, a następnie wybierz pozycję **Publikuj**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Przejdź do sekcji [Strategie: Definicje strategii](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Wybierz definicję strategii utworzoną w poprzednim kroku.
1. Przejrzyj definicję strategii i wybierz pozycję **Opublikuj strategię**.
1. Podaj **wersję** (np. _1.0_) i wszelkie **uwagi dotyczące zmian**, a następnie wybierz pozycję **Publikuj**.

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących spójności zasobów](../../decision-guides/resource-consistency/index.md)
- [Przykłady strategii opartych na standardach](https://docs.microsoft.com/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end

# <a name="azure-policy"></a>[Azure Policy](#tab/AzurePolicy)

Usługa Azure Policy umożliwia tworzenie i przypisywanie zasad oraz zarządzanie nimi. Te zasady wymuszają reguły zasobów, dzięki czemu zasoby te pozostają zgodne ze standardami firmy i umowami dotyczącymi poziomu usług. Usługa Azure Policy skanuje zasoby w celu zidentyfikowania zasobów, które nie są zgodne z implementowanymi zasadami. Możesz na przykład stosować zasady dopuszczające uruchamianie w środowisku tylko określonego rozmiaru maszyny wirtualnej. W przypadku implementowania tych zasad następuje oszacowanie istniejących maszyn wirtualnych w danym środowisku i wszystkich nowo wdrożonych maszyn wirtualnych. Podczas oceny zasad są generowane zdarzenia związane ze zgodnością, których można używać do monitorowania i raportowania.

Rozważ typowe zasady dotyczące następujących kwestii:

- Wymuszanie tagowania zasobów i grup zasobów.
- Ograniczanie regionów dla wdrożonych zasobów.
- Ograniczanie użycia kosztownych jednostek SKU dla określonych zasobów.
- Inspekcja użycia ważnych funkcji opcjonalnych, takich jak dyski zarządzane przez platformę Azure.

::: zone target="chromeless"

## <a name="action"></a>Akcja

Przypisz wbudowane zasady do grupy zarządzania, subskrypcji lub grupy zasobów.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

## <a name="apply-a-policy"></a>Stosowanie zasad

Aby zastosować zasady do grupy zasobów:

1. Przejdź do usługi [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Wybierz pozycję **Przypisz zasady**.

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Policy](https://docs.microsoft.com/azure/governance/policy)
- [Cloud Adoption Framework: Przewodnik podejmowania decyzji dotyczących wymuszania zasad](../../decision-guides/policy-enforcement/index.md)

::: zone-end

# <a name="azure-security-center"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Usługa Azure Security Center odgrywa ważną rolę w strategii zarządzania. Te funkcje pomagają być na bieżąco w zakresie zabezpieczeń, ponieważ wykonują następujące zadania:

- Udostępnianie ujednoliconego widoku zabezpieczeń w obciążeniach.
- Zbieranie, wyszukiwanie i analizowanie danych zabezpieczeń z różnych źródeł, w tym zapór i innych rozwiązań partnerskich.
- Udostępnianie rekomendacji dotyczących zabezpieczeń, które umożliwiają podjęcie odpowiednich działań w celu rozwiązania problemów, zanim zostaną one wykorzystane do ataków.
- Stosowanie zasad zabezpieczeń do obciążeń w chmurze hybrydowej w celu zapewnienia zgodności ze standardami zabezpieczeń.

Wiele funkcji zabezpieczeń, takich jak zasady zabezpieczeń i rekomendacje, jest dostępnych bezpłatnie. Niektóre z bardziej zaawansowanych funkcji, np. dostęp just in time do maszyn wirtualnych i obsługa obciążeń hybrydowych, są dostępne w ramach warstwy Standardowa usługi Security Center. Dostęp just in time do maszyn wirtualnych może pomóc w zmniejszeniu obszaru podatnego na ataki sieciowe dzięki kontroli dostępu do portów zarządzania na maszynach wirtualnych platformy Azure.

> [!TIP]
> Usługa Azure Security Center jest domyślnie włączana w każdej subskrypcji. Zalecamy włączenie funkcji zbierania danych z maszyn wirtualnych, aby umożliwić usłudze Azure Security Center zainstalowanie agenta i rozpoczęcie zbierania danych.

::: zone target="docs"

Aby zapoznać się z usługą Azure Security Center, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center)
- [Dostęp just in time do maszyny wirtualnej](https://docs.microsoft.com/azure/security-center/security-center-just-in-time#how-does-just-in-time-access-work)
- [Warstwy cenowe usługi Security Center](https://azure.microsoft.com/pricing/details/security-center)
- [Cloud Adoption Framework: dziedzina Punkt odniesienia zabezpieczeń](../../govern/security-baseline/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Akcja

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end
