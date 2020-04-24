---
title: Tworzenie dodatkowych subskrypcji w celu skalowania środowiska platformy Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak opracować strategię skalowania środowiska przy użyciu wielu subskrypcji platformy Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 465f1771232f8df7226773fb8055052a846cacca
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997959"
---
# <a name="create-additional-subscriptions-to-scale-your-azure-environment"></a>Tworzenie dodatkowych subskrypcji w celu skalowania środowiska platformy Azure

Organizacje często używają wielu subskrypcji platformy Azure, aby uniknąć limitów zasobów na subskrypcję i lepiej zarządzać swoimi zasobami platformy Azure. Ważne jest, aby zdefiniować strategię skalowania subskrypcji.

## <a name="review-fundamental-concepts"></a>Zapoznaj się z podstawowymi pojęciami

Po rozwinięciu środowiska platformy Azure poza [subskrypcję początkową](./initial-subscriptions.md)ważne jest zapoznanie się z pojęciami dotyczącymi platformy Azure, takimi jak konta, dzierżawcy, katalogi i subskrypcje. Aby uzyskać więcej informacji, zobacz [podstawowe pojęcia dotyczące platformy Azure](../considerations/fundamental-concepts.md).

Inne zagadnienia mogą wymagać dodatkowych subskrypcji. Rozszerzając swój majątek w chmurze, należy wziąć pod uwagę następujące kwestie.

## <a name="technical-considerations"></a>Zagadnienia techniczne

**Limity subskrypcji:** Subskrypcje mają zdefiniowane limity dla niektórych typów zasobów. Na przykład liczba sieci wirtualnych w subskrypcji jest ograniczona. Gdy subskrypcja zbliża się do tych limitów, należy utworzyć kolejną subskrypcję i umieścić w niej dodatkowe zasoby. Aby uzyskać więcej informacji, zobacz [limity subskrypcji i usług platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#general-limits).

**Zasoby modelu klasycznego:** Jeśli używasz platformy Azure przez długi czas, możesz mieć zasoby, które zostały utworzone przy użyciu klasycznego modelu wdrażania. Zasady platformy Azure, kontrola dostępu oparta na rolach, grupowanie zasobów i Tagi nie mogą być stosowane do zasobów modelu klasycznego. Te zasoby należy przenieść do subskrypcji, które zawierają tylko klasyczne zasoby modelu.

**Koszty:** Mogą występować dodatkowe koszty związane z transferem danych przychodzących i wychodzących między subskrypcjami.

## <a name="business-priorities"></a>Priorytety biznesowe

Twoje priorytety biznesowe mogą prowadzić do tworzenia dodatkowych subskrypcji. Te priorytety obejmują:

- Innowacje
- Migracja
- Koszty
- Operacje
- Zabezpieczenia
- Nadzór

Aby poznać inne zagadnienia dotyczące skalowania subskrypcji, zapoznaj się z [przewodnikiem](../../decision-guides/subscriptions/index.md) dotyczącym decyzji o subskrypcji w strukturze wdrożenia chmury.

## <a name="moving-resources-between-subscriptions"></a>Przeniesienie zasobów między subskrypcjami

Gdy model subskrypcji rośnie, możesz zdecydować, że niektóre zasoby należą do innych subskrypcji. Wiele typów zasobów można przenosić między subskrypcjami. Możesz również użyć zautomatyzowanych wdrożeń, aby ponownie utworzyć zasoby w innej subskrypcji. Aby uzyskać więcej informacji, zobacz [Przenoszenie zasobów platformy Azure do innej grupy zasobów lub subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription).

## <a name="tips-for-creating-new-subscriptions"></a>Porady dotyczące tworzenia nowych subskrypcji

- Określ, kto jest odpowiedzialny za tworzenie nowych subskrypcji.
- Zdecyduj, które typy zasobów są domyślnie dostępne w ramach subskrypcji.
- Zdecyduj, jak powinny wyglądać wszystkie standardowe subskrypcje. Rozważ kwestie związane z kontrolą dostępu opartą na rolach, zasadami, tagami zasobami infrastruktury.
- Jeśli to możliwe, programowe [Tworzenie nowych subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/management/programmatically-create-subscription) za pośrednictwem nazwy głównej usługi. Musisz [udzielić uprawnienia do jednostki usługi](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) , aby utworzyć subskrypcje. Zdefiniuj grupę zabezpieczeń, która może żądać nowych subskrypcji za pośrednictwem zautomatyzowanego przepływu pracy.
- Jeśli jesteś klientem mającym umowę Enterprise (EA), poproś pomoc techniczną platformy Azure o zablokowanie możliwości tworzenia subskrypcji niezwiązanych z umową EA dla organizacji.

## <a name="next-steps"></a>Następne kroki

Utwórz hierarchię grup zarządzania ułatwiającą [organizowanie subskrypcji i zasobów oraz zarządzanie nimi](./organize-subscriptions.md).

> [!div class="nextstepaction"]
> [Organizowanie subskrypcji i zasobów oraz zarządzanie nimi](./organize-subscriptions.md)
