---
title: Narzędzia bazowe zabezpieczeń na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie narzędzi, które mogą ułatwić ulepszoną linię bazową zabezpieczeń na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3bf3eea5486fbd349094663dc5f37527f5042bb5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221687"
---
# <a name="security-baseline-tools-in-azure"></a>Narzędzia bazowe zabezpieczeń na platformie Azure

[Linia bazowa zabezpieczeń](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na sposobach ustanawiania zasad chroniących sieć, zasoby i najważniejsze dane, które będą znajdować się w rozwiązaniu dostawcy chmury. W ramach pięciu dyscyplin nadzoru chmurowego dyscyplina odniesienia zabezpieczeń obejmuje klasyfikację cyfrowej i danych. Obejmuje to również dokumentację zagrożeń, tolerancję biznesową i strategie zaradcze związane z bezpieczeństwem danych, zasobów i sieci. Z perspektywy technicznej ta dyscyplina obejmuje również zaangażowanie w decyzje dotyczące [szyfrowania](../../decision-guides/encryption/index.md), [wymagań sieci](../../decision-guides/software-defined-network/index.md), [hybrydowych strategii tożsamości](../../decision-guides/identity/index.md)i narzędzi do [automatyzowania wymuszania](../../decision-guides/policy-enforcement/index.md) zasad zabezpieczeń między [grupami zasobów](../../decision-guides/resource-consistency/index.md).

Poniższa lista narzędzi systemu Azure może pomóc w podniesienia zasad i procesów obsługujących linię bazową zabezpieczeń.

| Tool | [Azure Portal](https://azure.microsoft.com/features/azure-portal)Menedżerzasobów / [](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Usługa Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Stosowanie kontroli dostępu do zasobów i tworzenie zasobów   | Tak                             | Nie              | Yes      | Nie           | Nie                    | Nie            |
| Bezpieczne sieci wirtualne                                    | Tak                             | Nie              | Nie       | Yes          | Nie                    | Nie            |
| Szyfruj dyski wirtualne                                     | Nie                              | Yes             | Nie       | Nie           | Nie                    | Nie            |
| Szyfruj magazyn PaaS i bazy danych                         | Nie                              | Yes             | Nie       | Nie           | Nie                    | Nie            |
| Zarządzanie hybrydowymi usługami tożsamości                            | Nie                              | Nie              | Yes      | Nie           | Nie                    | Nie            |
| Ogranicz dozwolone typy zasobów                         | Nie                              | Nie              | Nie       | Yes          | Nie                    | Nie            |
| Wymuszaj ograniczenia geograficzne-regionalne                          | Nie                              | Nie              | Nie       | Yes          | Nie                    | Nie            |
| Monitorowanie kondycji zabezpieczeń sieci i zasobów          | Nie                              | Nie              | Nie       | Nie           | Yes                   | Tak           |
| Wykrywanie złośliwego działania                                  | Nie                              | Nie              | Nie       | Nie           | Yes                   | Tak           |
| Zapobiegawczo wykrywaj luki w zabezpieczeniach                        | Nie                              | Nie              | Nie       | Nie           | Yes                   | Nie            |
| Konfigurowanie kopii zapasowej i odzyskiwania po awarii                     | Tak                             | Nie              | Nie       | Nie           | Nie                    | Nie            |

Aby uzyskać pełną listę narzędzi i usług zabezpieczeń platformy Azure, zobacz [usługi i technologie zabezpieczeń dostępne na platformie Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

Często klienci mogą korzystać z narzędzi innych firm w celu ułatwienia działań związanych z bezpieczeństwem linii bazowej. Aby uzyskać więcej informacji, zobacz artykuł [integracja rozwiązań zabezpieczeń w Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Oprócz narzędzi zabezpieczeń [Centrum zaufania Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment) zawiera obszerne wskazówki, raporty i powiązane dokumenty, które mogą pomóc w wykonywaniu oceny ryzyka w ramach procesu planowania migracji.
