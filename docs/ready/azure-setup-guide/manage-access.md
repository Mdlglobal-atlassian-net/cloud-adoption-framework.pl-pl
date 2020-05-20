---
title: Zarządzanie dostępem do środowiska platformy Azure
description: Dowiedz się, jak skonfigurować kontrolę dostępu w środowisku platformy Azure przy użyciu funkcji kontroli dostępu na podstawie ról (RBAC).
author: LijuKodicheraJayadevan
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 94f51b92b50dabff8551e30e476d2738c3f2fef7
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621651"
---
<!-- cSpell:ignore LijuKodicheraJayadevan -->

# <a name="manage-access-to-your-azure-environment-with-role-based-access-control"></a>Zarządzanie dostępem do środowiska platformy Azure przy użyciu kontroli dostępu na podstawie ról

Określanie, kto może uzyskiwać dostęp do zasobów platformy Azure i subskrypcji, to ważna część strategii zarządzania platformą Azure, a przypisywanie praw dostępu opartych na grupach i uprawnieniach jest dobrym rozwiązaniem. Zarządzanie grupami zamiast poszczególnymi użytkownikami upraszcza obsługę zasad dostępu, zapewnia spójne zarządzanie dostępem między różnymi zespołami i zmniejsza liczbę błędów konfiguracji. Kontrola dostępu oparta na rolach (RBAC) na platformie Azure jest podstawową metodą zarządzania dostępem na platformie Azure.

Funkcja RBAC umożliwia szczegółowe zarządzanie dostępem do zasobów na platformie Azure. Ułatwia ona zarządzanie osobami mającymi dostęp do zasobów platformy Azure, czynnościami, jakie mogą wykonywać, oraz zakresami, do których mają dostęp.

Podczas planowania strategii kontroli dostępu należy przyznać użytkownikom najniższe uprawnienia, które są wymagane, aby mogli wykonywać swoją pracę. Na poniższej ilustracji przedstawiono sugerowany wzorzec przypisywania funkcji RBAC.

![Diagram przedstawiający role funkcji RBAC](./media/manage-access/role-examples.png)

Zalecamy, aby podczas planowania metodologii dostępu i kontroli pracować z osobami, które pełnią w organizacji role związane z następującymi obszarami: bezpieczeństwo i zgodność, administracja IT i architektura przedsiębiorstwa.

Struktura wdrażania chmury zawiera dodatkowe wskazówki dotyczące [stosowania kontroli dostępu opartej na rolach](../considerations/roles.md) w ramach procesów wdrażania chmury.

::: zone target="chromeless"

## <a name="actions"></a>Akcje

**Udzielanie dostępu do grupy zasobów:**

Aby udzielić użytkownikowi dostępu do grupy zasobów:

1. Przejdź do pozycji **Grupy zasobów**.
1. Wybierz grupę zasobów.
1. Wybierz pozycję **Kontrola dostępu (IAM)** .
1. Wybierz pozycję **+ Dodaj** > **Dodaj przypisanie roli**.
1. Wybierz rolę, a następnie przypisz dostęp do użytkownika, grupy lub jednostki usługi.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2FSubscriptions%2FResourceGroups]" submitText="Go to resource groups" ::: form-end

**Udzielanie dostępu do subskrypcji:**

Aby udzielić użytkownikowi dostępu do subskrypcji:

1. Przejdź do pozycji **Subskrypcje**.
1. Wybierz subskrypcję.
1. Wybierz pozycję **Kontrola dostępu (IAM)** .
1. Wybierz pozycję **+ Dodaj** > **Dodaj przypisanie roli**.
1. Wybierz rolę, a następnie przypisz dostęp do użytkownika, grupy lub jednostki usługi.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to subscriptions" ::: form-end

::: zone-end

::: zone target="docs"

## <a name="grant-resource-group-access"></a>Udzielanie dostępu do grupy zasobów

Aby udzielić użytkownikowi dostępu do grupy zasobów:

1. Przejdź do pozycji [Grupy zasobów](https://portal.azure.com/#blade/HubsExtension/BrowseResourceGroups).
1. Wybierz grupę zasobów.
1. Wybierz pozycję **Kontrola dostępu (IAM)** .
1. Wybierz pozycję **+ Dodaj** > **Dodaj przypisanie roli**.
1. Wybierz rolę, a następnie przypisz dostęp do użytkownika, grupy lub jednostki usługi.

## <a name="grant-subscription-access"></a>Udzielanie dostępu do subskrypcji

Aby udzielić użytkownikowi dostępu do subskrypcji:

1. Przejdź do pozycji [Subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Wybierz subskrypcję.
1. Wybierz pozycję **Kontrola dostępu (IAM)** .
1. Wybierz pozycję **+ Dodaj** > **Dodaj przypisanie roli**.
1. Wybierz rolę, a następnie przypisz dostęp do użytkownika, grupy lub jednostki usługi.

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Czym jest kontrola dostępu oparta na rolach (RBAC)?](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Struktura wdrażania chmury: Korzystanie z kontroli dostępu opartej na rolach](../considerations/roles.md)

::: zone-end
