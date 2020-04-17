---
title: Spis i widoczność na platformie Azure
description: Poznaj narzędzia, które zapewniają wgląd w stan uruchomienia zasobów oraz umożliwiają tworzenie spisu tych zasobów w celu zebrania danych.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9647ec56145d54537541ee70bbdb2280c9cae2ac
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80426811"
---
# <a name="inventory-and-visibility-in-azure"></a>Spis i widoczność na platformie Azure

_Spis i widoczność_ to pierwsza z trzech dyscyplin planu bazowego zarządzania chmurą.

![Plan bazowy zarządzania chmurą](../../_images/manage/management-baseline.png)

To najważniejsza dyscyplina, ponieważ zebranie odpowiednich danych operacyjnych ma kluczowe znaczenie podczas podejmowania decyzji dotyczących operacji. Zespoły zarządzania chmurą muszą wiedzieć, jakimi zasobami zarządzają i jak są obsługiwane te zasoby. W tym artykule opisano różne narzędzia, które zapewniają wgląd w stan uruchomienia zasobów oraz umożliwiają tworzenie spisu tych zasobów.

Poniższa tabela zawiera sugerowane wartości minimalne planu bazowego zarządzania dla dowolnego środowiska klasy korporacyjnej.

|Proces  |Narzędzie  |Przeznaczenie  |
|---------|---------|---------|
|Monitorowanie kondycji usług platformy Azure|Azure Service Health|Monitorowanie kondycji i wydajności oraz diagnostyka usług działających na platformie Azure|
|Scentralizowane dzienniki|Log Analytics|Centralne rejestrowanie dla wszystkich celów związanych z widocznością|
|Scentralizowane monitorowanie|Azure Monitor|Centralne monitorowanie danych operacyjnych i trendów|
|Śledzenie zmian i spisu maszyn wirtualnych|Azure Change Tracking and Inventory|Tworzenie spisu maszyn wirtualnych i monitorowanie zmian na poziomie systemu operacyjnego gościa|
|Monitorowanie subskrypcji|Dziennik aktywności platformy Azure|Monitorowanie zmian na poziomie subskrypcji|
|Monitorowanie systemu operacyjnego gościa|Usługa Azure Monitor dla maszyn wirtualnych|Monitorowanie zmian i wydajności maszyn wirtualnych|
|Monitorowanie sieci|Azure Network Watcher|Monitorowanie zmian i wydajności sieci|
|Monitorowanie systemu DNS|Analiza DNS|Zabezpieczenia, wydajność i operacje systemu DNS|

::: zone target="docs"

## <a name="azure-service-health"></a>Azure Service Health

::: zone-end
::: zone target="chromeless"

## <a name="azure-service-health"></a>[Azure Service Health](#tab/AzureServiceHealth)

::: zone-end

Usługa Azure Service Health udostępnia spersonalizowany widok kondycji usług i regionów platformy Azure. Informacje na temat aktywnych problemów są publikowane w usłudze Service Health, aby ułatwić zrozumienie wpływu na zasoby. Dzięki regularnym aktualizacjom będziesz otrzymywać informacje o rozwiązaniu problemów.

W usłudze Service Health publikujemy też zdarzenia planowanej konserwacji, aby informować Cię o zmianach, które mogą wpłynąć na dostępność zasobów. Skonfiguruj alerty usługi Service Health, aby otrzymywać powiadomienia, gdy problemy z usługą, planowana konserwacja lub inne zmiany mogą mieć wpływ na usługi i regiony platformy Azure.

Usługa Azure Service Health udostępnia następujące dane:

- **Stan platformy Azure:** globalny widok kondycji usług platformy Azure.
- **Kondycja usługi:** spersonalizowany widok kondycji usług Azure.
- **Kondycja zasobu:** dokładniejszy widok kondycji poszczególnych zasobów.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby skonfigurować alert usługi Service Health:

1. Przejdź do pozycji **Service Health**.
2. Wybierz pozycję **Alerty dotyczące kondycji**.
3. Utwórz alert dotyczący kondycji usługi.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

Aby skonfigurować alert usługi Service Health, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Service Health](https://docs.microsoft.com/azure/service-health).

## <a name="log-analytics"></a>Log Analytics

::: zone-end
::: zone target="chromeless"

## <a name="log-analytics"></a>[Log Analytics](#tab/Log-Analytics)

::: zone-end

[Obszar roboczy usługi Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) to unikatowe środowisko do przechowywania danych dziennika usługi Azure Monitor. Każdy obszar roboczy ma własne repozytorium danych i konfigurację. Konfiguracja źródeł danych i rozwiązań umożliwia przechowywanie danych w określonych obszarach roboczych. Rozwiązania do monitorowania platformy Azure wymagają połączenia wszystkich serwerów z obszarem roboczym, co pozwala przechowywać dane dziennika i uzyskiwać do nich dostęp.

::: zone target="chromeless"

### <a name="action"></a>Akcja

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.OperationalInsights%2FWorkspaces]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z dokumentacją dotyczącą [tworzenia obszaru roboczego usługi Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace).

## <a name="azure-monitor"></a>Azure Monitor

::: zone-end
::: zone target="chromeless"

## <a name="azure-monitor"></a>[Azure Monitor](#tab/Azure-Monitor)

::: zone-end

Usługa Azure Monitor oferuje jedno ujednolicone centrum zawierające wszystkie dane monitorowania i diagnostyki na platformie Azure oraz zapewnia wgląd we wszystkie zasoby. Usługa Azure Monitor umożliwia znajdowanie problemów i ich rozwiązywanie oraz optymalizowanie wydajności. Pozwala ona również zrozumieć zachowanie klientów.

- **Monitorowanie i wizualizowanie metryk** Metryki to wartości liczbowe udostępniane przez zasoby platformy Azure. Pomagają one zrozumieć kondycję systemów. Można dostosowywać wykresy w pulpitach nawigacyjnych i używać skoroszytów na potrzeby raportowania.

- **Wykonywanie zapytań o dzienniki i ich analizowanie** dzienniki obejmują dzienniki aktywności i dzienniki diagnostyczne z platformy Azure. Można zbierać dodatkowe dzienniki z innych rozwiązań do zarządzania i monitorowania na potrzeby zasobów w chmurze lub środowisku lokalnym. Do agregowania wszystkich tych danych służy usługa Log Analytics, która udostępnia centralne repozytorium. Z tego miejsca można uruchamiać zapytania, aby pomóc w rozwiązywaniu problemów lub zwizualizować dane.

- **Konfigurowanie alertów i akcji** alerty powiadamiają o warunkach krytycznych. Na podstawie wyzwalaczy związanych z problemami dotyczącymi metryk, dzienników lub kondycji usługi można podejmować akcje naprawcze. Można skonfigurować różne powiadomienia i akcje, a także wysyłać dane do narzędzi do zarządzania usługami IT.

::: zone target="chromeless"

### <a name="action"></a>Akcja

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

::: zone target="docs"

 Rozpocznij monitorowanie następujących elementów:

- [Aplikacje](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containers](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Maszyny wirtualne](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Sieci](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Aby monitorować inne zasoby, znajdź dodatkowe rozwiązania w witrynie Azure Marketplace.

Aby zapoznać się z usługą Azure Monitor, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

## <a name="onboard-solutions"></a>Dołączanie rozwiązań

::: zone-end
::: zone target="chromeless"

## <a name="onboard-solutions"></a>[Dołączanie rozwiązań](#tab/Configure-solutions)

::: zone-end

Korzystanie z rozwiązań wymaga skonfigurowania obszaru roboczego usługi Log Analytics. Dołączone maszyny wirtualne platformy Azure i serwery lokalne mogą korzystać z rozwiązań za pośrednictwem połączonych obszarów roboczych usługi Log Analytics.

Wyróżniamy dwie metody dołączania:

- [Pojedyncza maszyna wirtualna](../../manage/azure-server-management/onboard-single-vm.md)
- [Cała subskrypcja](../../manage/azure-server-management/onboard-at-scale.md)

W poszczególnych artykułach znajdują się instrukcje dołączania tych rozwiązań:

- Zarządzanie aktualizacjami
- Śledzenie zmian i spis
- Dziennik aktywności platformy Azure
- Azure Log Analytics Agent Health
- Ocena oprogramowania chroniącego przed złośliwym kodem
- Usługa Azure Monitor dla maszyn wirtualnych
- Azure Security Center

Wszystkie wymienione wcześniej czynności ułatwiają skonfigurowanie spisu i widoczności.
