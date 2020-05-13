---
title: Narzędzia spójności zasobów na platformie Azure
description: Zobacz, jak narzędzia natywne platformy Azure mogą pomóc w dojrzałych zasadach i procesach, które obsługują dyscyplinę spójności zasobów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a64cbd53cdd4c524b370681ebedf1f8282ac2a93
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217952"
---
# <a name="resource-consistency-tools-in-azure"></a>Narzędzia spójności zasobów na platformie Azure

[Spójność zasobów](./index.md) to jedno z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dziedzina koncentruje się na sposobach opracowywania zasad związanych z operacyjnym zarządzaniem środowiskiem, aplikacją lub obciążeniem. W ramach pięciu dyscyplin nadzoru w chmurze dyscyplina spójności zasobów obejmuje monitorowanie aplikacji, obciążeń i wydajności zasobów. Obejmuje to również zadania wymagane do spełnienia wymagań dotyczących skalowania, korygowania naruszeń umów SLA dotyczących wydajności i aktywnego uniknięcia naruszeń umowy SLA dla wydajności poprzez automatyczne korygowanie.

Poniżej znajduje się lista narzędzi platformy Azure, które mogą pomóc w zakończeniu zasad i procesów, które obsługują tę dyscyplinę.

| Narzędzie | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview)  | [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) | [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) | [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) |
|---------|---------|---------|---------|---------|---------|---------|---------|
| Wdrażanie zasobów                             | Tak | Tak | Tak | Yes | Nie  | Nie | Nie |
| Zarządzanie zasobami                             | Tak | Tak | Tak | Yes | Nie  | Nie | Nie |
| Wdrażanie zasobów przy użyciu szablonów             | Nie  | Yes | Nie  | Yes | Nie  | Nie | Nie |
| Wdrożenie środowiska aranżacjowego          | Nie  | Nie  | Yes | Nie  | Nie  | Nie | Nie |
| Definiowanie grup zasobów                       | Tak | Tak | Yes | Nie  | Nie  | Nie | Nie |
| Zarządzanie obciążeniami i właścicielami kont           | Tak | Tak | Yes | Nie  | Nie  | Nie | Nie |
| Zarządzanie dostępem warunkowym do zasobów       | Tak | Tak | Yes | Nie  | Nie  | Nie | Nie |
| Konfigurowanie użytkowników RBAC                         | Yes | Nie  | Nie  | Nie  | Yes | Nie | Nie |
| Przypisywanie ról i uprawnień do zasobów | Tak | Tak | Yes | Nie  | Yes | Nie | Nie |
| Definiowanie zależności między zasobami        | Nie  | Yes | Yes | Nie  | Nie  | Nie | Nie |
| Zastosuj kontrolę dostępu                         | Tak | Tak | Yes | Nie  | Yes | Nie | Nie |
| Ocenianie dostępności i skalowalności          | Nie  | Nie  | Nie  | Yes | Nie  | Nie | Nie |
| Stosowanie tagów do zasobów                      | Tak | Tak | Yes | Nie  | Nie  | Nie | Nie |
| Przypisywanie reguł Azure Policy                    | Tak | Tak | Yes | Nie  | Nie  | Nie | Nie |
| Zastosuj automatyczne korygowanie                  | Nie  | Nie  | Nie  | Yes | Nie  | Nie | Nie |
| Zarządzanie rozliczeniami                               | Yes | Nie  | Nie  | Nie  | Nie  | Nie | Nie |
| Planowanie zasobów na potrzeby odzyskiwania po awarii         | Tak | Tak | Yes | Nie  | Nie  | Yes | Tak |
| Odzyskiwanie danych podczas awarii lub naruszenia umowy SLA     | Nie | Nie  | Nie  | Nie  | Nie  | Yes | Tak |
| Odzyskiwanie aplikacji i danych podczas awarii lub naruszenia umowy SLA     | Nie | Nie  | Nie  | Nie  | Nie  | Yes | Tak |

Wraz z tymi narzędziami i funkcjami spójności zasobów konieczne będzie monitorowanie wdrożonych zasobów pod kątem problemów z wydajnością i kondycją. [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) to domyślne rozwiązanie do monitorowania i raportowania na platformie Azure. Azure Monitor udostępnia funkcje monitorowania zasobów w chmurze. Ta lista pokazuje, która funkcja rozwiązuje typowe wymagania dotyczące monitorowania.

| Narzędzie | [Azure Portal](https://azure.microsoft.com/features/azure-portal) | [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) | [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) | [Interfejs API REST usługi Azure Monitor](https://docs.microsoft.com/rest/api/monitor) |
|----------------------------------------------------|--------------|----------------------|---------------|------------------------|
| Rejestruj dane telemetryczne maszyny wirtualnej                 | Nie           | Nie                   | Yes           | Nie                     |
| Rejestruj dane telemetryczne sieci wirtualnych              | Nie           | Nie                   | Yes           | Nie                     |
| Dane telemetryczne usług log PaaS Services                   | Nie           | Nie                   | Yes           | Nie                     |
| Rejestruj dane telemetryczne aplikacji                     | Nie           | Yes                  | Nie            | Nie                     |
| Konfigurowanie raportów i alertów                       | Yes          | Nie                   | Nie            | Yes                    |
| Planowanie regularnych raportów lub analizy niestandardowej        | Nie           | Nie                   | Nie            | Nie                     |
| Wizualizowanie i analizowanie danych dzienników i wydajności     | Yes          | Nie                   | Nie            | Nie                     |
| Integracja z rozwiązaniem do monitorowania lokalnego lub innej firmy     | Nie           | Nie                   | Nie            | Yes                    |

Podczas planowania wdrożenia należy rozważyć miejsce przechowywania danych rejestrowania oraz sposób integracji opartych na chmurze [usług raportowania i monitorowania](../../decision-guides/logging-and-reporting/index.md) z istniejącymi procesami i narzędziami.

> [!NOTE]
> Organizacje używają również narzędzi DevOps innych firm do monitorowania obciążeń i zasobów. Aby uzyskać więcej informacji, zobacz [integracje narzędzi DevOps](https://azure.microsoft.com/products/devops-tool-integrations).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tworzyć i przypisywać [definicje zasad](https://docs.microsoft.com/azure/governance/policy) oraz zarządzać nimi na platformie Azure.
