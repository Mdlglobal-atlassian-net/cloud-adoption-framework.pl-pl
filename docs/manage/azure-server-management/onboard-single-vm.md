---
title: Włączanie usług zarządzania na jednej maszynie wirtualnej na potrzeby oceny
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Włączanie usług zarządzania na jednej maszynie wirtualnej na potrzeby oceny
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e9d5e17e87d79d8d1fdf7239298a973959103a37
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028654"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Włączanie usług zarządzania na jednej maszynie wirtualnej na potrzeby oceny

Dowiedz się, jak włączyć usługi zarządzania na jednej maszynie wirtualnej do oceny.

> [!NOTE]
> Przed dołączeniem maszyn wirtualnych do usług zarządzania platformy Azure Utwórz wymagane [obszary robocze log Analytics i Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

Dołączanie poszczególnych maszyn wirtualnych do usług zarządzania serwerem Azure jest proste w Azure Portal. Portal umożliwia zapoznanie się z tymi usługami przed dołączeniem ich do maszyn wirtualnych. Po wybraniu wystąpienia maszyny wirtualnej wszystkie rozwiązania omówione na liście [narzędzi i usług zarządzania](./tools-services.md) są wyświetlane w menu **operacje** lub w menu **monitorowanie** . Możesz wybrać każde rozwiązanie i użyć kreatora, aby dołączyć go.

![Zrzut ekranu ustawień maszyny wirtualnej w Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Powiązane zasoby

Aby uzyskać więcej informacji na temat dołączania poszczególnych maszyn wirtualnych do poszczególnych rozwiązań, zobacz:

- [Dołączanie rozwiązań Update Management, Change Tracking i spisu z maszyny wirtualnej platformy Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Dołączanie monitorowania platformy Azure dla maszyny wirtualnej](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak używać Azure Policy do dołączania maszyn wirtualnych platformy Azure na dużą skalę.

> [!div class="nextstepaction"]
> [Konfigurowanie usług zarządzania platformy Azure dla subskrypcji](./onboard-at-scale.md)
