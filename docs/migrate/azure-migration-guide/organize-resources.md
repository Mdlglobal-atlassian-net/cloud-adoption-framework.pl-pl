---
title: Skuteczne organizowanie zasobów platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Najlepsze rozwiązania umożliwiające efektywne organizowanie zasobów platformy Azure w celu ułatwienia zarządzania.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 19299c5855600524f3335b00272974790d83c8fa
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022769"
---
# <a name="organize-your-azure-resources"></a>Organizowanie zasobów platformy Azure

Poniższe funkcje i najlepsze rozwiązania pozwalają zabezpieczyć zasoby krytyczne dla systemu. Oznaczanie zasobów tagami, dzięki czemu można je śledzić według wartości, które są istotne dla organizacji.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[Grupy zarządzania i hierarchia platformy Azure](#tab/AzureManagmentGroupsAndHierarchy)

Struktura organizacyjna zasobów platformy Azure ma cztery poziomy: grupy zarządzania, subskrypcje, grupy zasobów i zasoby. Na poniższej ilustracji przedstawiono relacje tych poziomów.

![Diagram przedstawiający relację hierarchii zarządzania](./media/organize-resources/scope-levels.png)

- **Grupy zarządzania:** są to kontenery, które ułatwiają zarządzanie dostępem, zasadami i zgodnością w wielu subskrypcjach. Wszystkie subskrypcje w grupie zarządzania automatycznie dziedziczą warunki zastosowane do tej grupy zarządzania.
- **Subskrypcje:** subskrypcja grupuje konta użytkowników i zasobów, które zostały utworzone przez te konta użytkowników. Każda subskrypcja ma limity lub limity przydziału ilości zasobów, które można tworzyć i stosować. Organizacje mogą używać subskrypcji do zarządzania kosztami i zasobami, które są tworzone przez użytkowników, zespoły lub projekty.
- **Grupy zasobów:** Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje internetowe, bazy danych i konta magazynu, oraz zarządzania nimi.
- **Zasoby:** zasoby to tworzone przez Ciebie wystąpienia usług, takie jak maszyny wirtualne, magazyn lub bazy danych SQL.

## <a name="scope-of-management-settings"></a>Zakres ustawień zarządzania

Ustawienia zarządzania, takie jak zasady i kontrola dostępu na podstawie ról, można stosować na dowolnym poziomie zarządzania. Zasięg zastosowania ustawienia jest określany na podstawie wybranego poziomu. Niższe poziomy dziedziczą ustawienia z wyższych poziomów. Na przykład zasady stosowane do subskrypcji są również stosowane do wszystkich grup zasobów i zasobów w ramach tej subskrypcji.

Krytyczne ustawienia zwykle warto stosować na wyższych poziomach, a wymagania specyficzne dla projektu na niższych poziomach. Może na przykład zajść potrzeba upewnienia się, że wszystkie zasoby w organizacji zostaną wdrożone w określonych regionach. W tym celu należy do subskrypcji zastosować zasady, które określą dozwolone lokalizacje. Kiedy inni użytkownicy w organizacji będą dodawać nowe grupy zasobów i zasoby, dozwolone lokalizacje będą automatycznie wymuszane. Dowiedz się więcej na temat zasad w sekcji dotyczącej zarządzania, zabezpieczeń i zgodności tego przewodnika.

Zalecamy, aby podczas planowania strategii zgodności pracować z osobami, które pełnią w organizacji role związane z następującymi obszarami: bezpieczeństwo i zgodność, administracja IT, architektura przedsiębiorstwa, sieć, finanse i zaopatrzenie.

::: zone target="docs"

## <a name="create-a-management-level"></a>Tworzenie poziomu zarządzania

Możesz utworzyć grupę zarządzania, dodatkowe subskrypcje lub grupy zasobów.

### <a name="create-management-group"></a>Tworzenie grupy zarządzania

Utwórz grupę zarządzania, która ułatwia zarządzanie dostępem, zasadami i zgodnością w wielu subskrypcjach.

1. Przejdź do pozycji [Grupy zarządzania](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Wybierz pozycję **Dodaj grupę zarządzania**.

### <a name="create-subscription"></a>Tworzenie subskrypcji

Subskrypcje umożliwiają zarządzanie kosztami i zasobami, które są tworzone przez użytkowników, zespoły lub projekty.

1. Przejdź do pozycji [Subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Wybierz pozycję **Dodaj**.

### <a name="create-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów do przechowywania zasobów, takich jak aplikacje internetowe, bazy danych i konta magazynu, które współużytkują ten sam cykl życia, uprawnienia i zasady.

1. Przejdź do pozycji [Grupy zasobów](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Wybierz pozycję **Dodaj**.
1. Wybierz **subskrypcję**, w ramach której chcesz utworzyć grupę zasobów.
1. Wprowadź nazwę **grupy zasobów**.
1. Wybierz **region** dla lokalizacji grupy zasobów.

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz:

- [Informacje o zarządzaniu dostępem do zasobów na platformie Azure](../../govern/resource-consistency/resource-access-management.md)
- [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview)
- [Limity usług subskrypcji](https://docs.microsoft.com/azure/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Akcje

**Tworzenie grupy zarządzania:**

Utwórz grupę zarządzania, która ułatwia zarządzanie dostępem, zasadami i zgodnością w wielu subskrypcjach.

1. Przejdź do pozycji **Grupy zarządzania**.
1. Wybierz pozycję **Dodaj grupę zarządzania**.

::: form action="OpenBlade[#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade]" submitText="Go to Management groups" :::

**Tworzenie dodatkowej subskrypcji:**

Subskrypcje umożliwiają zarządzanie kosztami i zasobami, które są tworzone przez użytkowników, zespoły lub projekty.

1. Przejdź do pozycji **Subskrypcje**.
1. Wybierz pozycję **Dodaj**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

**Tworzenie grupy zasobów:**

Utwórz grupę zasobów do przechowywania zasobów, takich jak aplikacje internetowe, bazy danych i konta magazynu, które współużytkują ten sam cykl życia, uprawnienia i zasady.

1. Przejdź do pozycji **Grupy zasobów**.
1. Wybierz pozycję **Dodaj**.
1. Wybierz **subskrypcję**, w ramach której chcesz utworzyć grupę zasobów.
1. Wprowadź nazwę **grupy zasobów**.
1. Wybierz **region** dla lokalizacji grupy zasobów.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

# <a name="naming-standardstabnamingstandards"></a>[Standardy nazewnictwa](#tab/NamingStandards)

Odpowiedni standard nazewnictwa ułatwia identyfikowanie zasobów w portalu, na rachunku i w ramach skryptów. Prawdopodobnie masz już standardy nazewnictwa dla infrastruktury lokalnej. Podczas dodawania platformy Azure do środowiska należy rozszerzyć te standardy nazewnictwa na zasoby platformy Azure. Standardy nazewnictwa ułatwiają wydajniejsze zarządzanie środowiskiem na wszystkich poziomach. Usługi Azure Policy można używać jako narzędzia wymuszania standardów nazewnictwa w całym środowisku platformy Azure.

::: zone target="docs"

Zalecamy zapoznanie się ze [wskazówkami dotyczącymi wzorców i rozwiązań](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions), a następnie stosowanie ich.

>[!TIP]
>Należy unikać używania znaków specjalnych (`-` lub `_`) jako pierwszego lub ostatniego znaku w dowolnej nazwie. Te znaki sprawiają, że większość reguł walidacji kończy się niepowodzeniem.

::: zone-end

| Jednostka | Zakres | Długość | Wielkość liter | Prawidłowe znaki | Sugerowany wzorzec | Przykład |
| --- | --- | --- | --- | --- | --- | --- |
|Grupa zasobów |Subskrypcja |1-90 |Bez uwzględniania wielkości liter |Alfanumeryczne, podkreślenie, nawiasy, łącznik, kropka (z wyjątkiem znaków na końcu) i znaki Unicode |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Zestaw dostępności |Grupa zasobów |1-80 |Bez uwzględniania wielkości liter |Alfanumeryczne, podkreślenie i łącznik |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Tag |Skojarzona jednostka |512 (nazwa), 256 (wartość) |Bez uwzględniania wielkości liter |Alfanumeryczne |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Tagi zasobów](#tab/ResourceTags)

Tagi ułatwiają szybkie identyfikowanie zasobów i grup zasobów. Stosowanie tagów do zasobów platformy Azure umożliwia ich logiczne zorganizowanie według kategorii. Każdy tag składa się z nazwy i wartości. Na przykład można zastosować nazwę „Środowisko” i wartość „Produkcyjne” do wszystkich zasobów w środowisku produkcyjnym.

Po zastosowaniu tagów można pobrać wszystkie zasoby w subskrypcji o nazwie i wartości konkretnego tagu. Tagi umożliwiają pobieranie powiązanych zasobów z różnych grup zasobów, które są pomocne w przypadku organizowania zasobów na potrzeby rozliczeń lub zarządzania.

Tagów można używać do wielu innych celów. Najczęstsze zastosowania to:

- **Metadane i dokumentacja:** administratorzy mogą łatwo wyświetlać szczegółowe informacje o zasoby, z którymi pracują, stosując tag, na przykład „ProjectOwner”.
- **Automatyzacja:** można używać regularnie uruchamianych skryptów, które mogą wykonywać akcję w oparciu o wartość tagu, taką jak „ShutdownTime” lub „DeprovisionDate”.
- **Rozliczenia:** tagi mogą być wyświetlane na fakturze. Można ich używać, aby ułatwić dzielenie rachunku na segmenty za pomocą tagów, takich jak „CostCenter” lub „BillTo”.

Każdy zasób lub grupa zasobów może mieć co najwyżej 15 par nazwa/wartość tagu. Jednak to ograniczenie dotyczy tylko tagów stosowanych bezpośrednio do grupy zasobów lub zasobu.

Aby uzyskać więcej informacji na temat tagowania, zobacz [konwencje nazewnictwa Centrum architektury platformy Azure dla zasobów platformy Azure](../../ready/considerations/naming-and-tagging.md#metadata-tags).

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Stosowanie tagu zasobu

Aby zastosować tag do grupy zasobów:

1. Przejdź do pozycji [Grupy zasobów](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Wybierz grupę zasobów.
1. Wybierz pozycję **Tagi**.
1. Wprowadź nową nazwę i wartość lub użyj listy rozwijanej, aby wybrać istniejącą nazwę i wartość.

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zobacz [Organizowanie zasobów platformy Azure przy użyciu tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Akcja

**Stosowanie tagu zasobu:**

Aby zastosować tag do grupy zasobów:

1. Przejdź do pozycji **Grupy zasobów**.
1. Wybierz grupę zasobów.
1. Wybierz pozycję **Tagi**.
1. Wprowadź nową nazwę i wartość lub wybierz istniejącą nazwę i wartość.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups]" submitText="Go to resource groups" :::

::: zone-end
