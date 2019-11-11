---
title: Zarządzanie kosztami i rozliczeniami dla zasobów platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak interpretować faktury oraz konfigurować budżety i płatności dotyczące zasobów platformy Azure.
author: dchimes
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: c9a02a6d98929455d8d8f6c163825f69de7996be
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73562571"
---
# <a name="manage-costs-and-billing-for-your-azure-resources"></a>Zarządzanie kosztami i rozliczeniami dla zasobów platformy Azure

Zarządzanie kosztami to proces efektywnego planowania i kontrolowania kosztów związanych z działalnością. Zadania zarządzania kosztami są zazwyczaj wykonywane przez zespoły ds. finansów, zarządzania i aplikacji. Usługa Azure Cost Management może ułatwić planowanie z uwzględnieniem kosztów. Ułatwia ona również efektywne analizowanie kosztów i podejmowanie działań mających na celu optymalizację wydatków dotyczących chmury.

Aby uzyskać więcej informacji na temat integrowania procesów zarządzania kosztami chmury w całej organizacji, zapoznaj się z artykułem przewodnika Cloud Adoption Framework dotyczącym [śledzenia kosztów w jednostkach biznesowych, środowiskach i projektach](../azure-best-practices/track-costs.md).

## <a name="manage-your-costs-with-azure-cost-management"></a>Zarządzanie kosztami przy użyciu usługi Azure Cost Management

Usługa Azure Cost Management oferuje kilka sposobów, które ułatwiają przewidywanie kosztów i zarządzanie nimi:

- **Analiza kosztów chmury** pomaga w badaniu i analizowaniu kosztów. Możesz wyświetlić zagregowany koszt dla swojego konta lub koszty skumulowane w czasie.
- **Monitorowanie za pomocą budżetów** umożliwia utworzenie budżetu i skonfigurowanie alertów, które ostrzegają, gdy zbliżasz się do przekroczenia budżetu.
- **Optymalizowanie za pomocą rekomendacji** ułatwia identyfikowanie zasobów w stanie bezczynności i niedostatecznie używanych zasobów, dzięki czemu można podjąć działania w celu zmniejszeniu strat.
- **Zarządzanie fakturami i płatnościami** zapewnia wgląd w inwestycję w chmurę.

::: zone target="docs"

### <a name="predict-and-manage-costs"></a>Przewidywanie kosztów i zarządzanie nimi

1. Przejdź do obszaru [Zarządzanie kosztami i rozliczenia](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Wybierz pozycję **Zarządzanie kosztami**.
1. Zapoznaj się z funkcjami, które ułatwiają analizowanie i optymalizowanie kosztów chmury.

### <a name="manage-invoices-and-payment-methods"></a>Zarządzanie fakturami i formami płatności

1. Przejdź do obszaru [Zarządzanie kosztami i rozliczenia](https://portal.azure.com/#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview).
1. Wybierz pozycję **Faktury** lub **Formy płatności** w sekcji **Rozliczenia** w okienku po lewej stronie.

## <a name="billing-and-subscription-support"></a>Pomoc techniczna dotycząca rozliczeń i subskrypcji

Oferujemy 24-godzinny dostęp do pomocy technicznej dotyczącej rozliczeń i subskrypcji dla klientów platformy Azure. Jeśli potrzebujesz pomocy, aby zrozumieć użycie platformy Azure, utwórz wniosek o pomoc techniczną.

### <a name="create-a-support-request"></a>Tworzenie żądania obsługi

Aby przesłać nowe żądanie obsługi:

1. Przejdź do pozycji [Pomoc i obsługa techniczna](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Wybierz pozycję **Nowe żądanie obsługi**.

### <a name="view-a-support-request"></a>Wyświetlanie żądania obsługi

Aby wyświetlić swoje wnioski o pomoc techniczną i ich stan:

1. Przejdź do pozycji [Pomoc i obsługa techniczna](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).
1. Wybierz pozycję **Wszystkie żądania obsługi**.

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Dokumentacja dotycząca rozliczeń i zarządzania kosztami na platformie Azure](https://docs.microsoft.com/azure/billing)
- [Cloud Adoption Framework: Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach](../azure-best-practices/track-costs.md)
- [Cloud Adoption Framework: Dyscyplina ładu zarządzania kosztami](../../govern/cost-management/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Akcje

**Przewidywanie kosztów i zarządzanie nimi:**

1. Przejdź do obszaru **Zarządzanie kosztami i rozliczenia**.
1. Wybierz pozycję **Zarządzanie kosztami**.

**Zarządzanie fakturami i formami płatności:**

1. Przejdź do obszaru **Zarządzanie kosztami i rozliczenia**.
1. Wybierz pozycję **Faktury** lub **Formy płatności** w sekcji **Rozliczenia** w okienku po lewej stronie.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" ::: form-end

**Pomoc techniczna dotycząca rozliczeń i subskrypcji:**

Oferujemy 24-godzinny dostęp do pomocy technicznej dotyczącej rozliczeń i subskrypcji dla klientów platformy Azure. Jeśli potrzebujesz pomocy, aby zrozumieć użycie platformy Azure, utwórz wniosek o pomoc techniczną.

**Tworzenie żądania obsługi:**

Aby przesłać nowe żądanie obsługi:

1. Przejdź do pozycji **Pomoc i obsługa techniczna**.
2. Wybierz pozycję **Nowe żądanie obsługi**.

**Wyświetlanie żądania obsługi:** Aby wyświetlić swoje wnioski o pomoc techniczną i ich stan:

1. Przejdź do pozycji **Pomoc i obsługa techniczna**.
2. Wybierz pozycję **Wszystkie żądania obsługi**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview]" submitText="Go to Help + Support" ::: form-end

::: zone-end
