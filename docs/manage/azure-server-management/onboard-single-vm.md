---
title: Włączanie usług zarządzania serwerem na jednej maszynie wirtualnej do oceny
description: Włączanie usług zarządzania serwerem na jednej maszynie wirtualnej do oceny
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d73b9f5a13150b0c3b13feff3f21a765a36ac4a8
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808043"
---
# <a name="enable-server-management-services-on-a-single-vm-for-evaluation"></a>Włączanie usług zarządzania serwerem na jednej maszynie wirtualnej do oceny

Dowiedz się, jak włączyć usługi zarządzania serwerem na jednej maszynie wirtualnej do oceny.

> [!NOTE]
> Przed zaimplementowaniem usług zarządzania systemu Azure na maszynie wirtualnej Utwórz wymagany [obszar roboczy log Analytics i konto Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

Usługi zarządzania serwerem Azure można łatwo dołączać do poszczególnych maszyn wirtualnych w Azure Portal. Możesz zapoznać się z tymi usługami przed ich dołączeniem. Po wybraniu wystąpienia maszyny wirtualnej wszystkie rozwiązania na liście [narzędzi do zarządzania i usług](./tools-services.md) są wyświetlane w menu **operacje** lub **monitorowanie** . Wybierz rozwiązanie i postępuj zgodnie z instrukcjami kreatora, aby dołączyć go.

![Zrzut ekranu ustawień maszyny wirtualnej w Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Zasoby powiązane

Aby uzyskać więcej informacji na temat sposobu dołączania tych rozwiązań do poszczególnych maszyn wirtualnych, zobacz:

- [Dołączanie rozwiązań Update Management, Change Tracking i spisu z maszyny wirtualnej platformy Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Dołączanie monitorowania platformy Azure dla maszyn wirtualnych](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak używać Azure Policy do dołączania maszyn wirtualnych platformy Azure na dużą skalę.

> [!div class="nextstepaction"]
> [Konfigurowanie usług zarządzania platformy Azure dla subskrypcji](./onboard-at-scale.md)
