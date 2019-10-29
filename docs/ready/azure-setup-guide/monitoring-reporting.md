---
title: Monitorowanie i raportowanie na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak skonfigurować monitorowanie, raportowanie i alerty dla środowiska zarządzania platformy Azure.
author: timleyden
ms.author: tileyden
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC, setup
ms.localizationpriority: high
ms.openlocfilehash: 1be663168815af9067268cd18d9db51cfe10291c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548879"
---
# <a name="monitoring-and-reporting-in-azure"></a>Monitorowanie i raportowanie na platformie Azure

Platforma Azure oferuje wiele usług, które stanowią kompleksowe rozwiązanie umożliwiające zbieranie, analizowanie oraz działanie na podstawie danych telemetrycznych z aplikacji użytkownika oraz zasobów platformy Azure, które je obsługują. Mogą one również monitorować krytyczne zasoby lokalne, aby zapewnić hybrydowe środowisko monitorowania.

# <a name="azure-monitortabazuremonitor"></a>[Azure Monitor](#tab/AzureMonitor)

Usługa Azure Monitor oferuje jedno ujednolicone centrum zawierające wszystkie dane monitorowania i diagnostyki na platformie Azure. Można ją wykorzystać, aby uzyskać wgląd w zasoby. Usługa Azure Monitor umożliwia znajdowanie problemów i ich rozwiązywanie oraz optymalizowanie wydajności. Pozwala ona również zrozumieć zachowanie klientów.

- **Monitorowanie i wizualizowanie metryk** Metryki to wartości liczbowe udostępniane przez zasoby platformy Azure, które pomagają zrozumieć kondycję systemów. Można dostosowywać wykresy w pulpitach nawigacyjnych i używać skoroszytów na potrzeby raportowania.

- **Wykonywanie zapytań o dzienniki i ich analizowanie** dzienniki obejmują dzienniki aktywności i dzienniki diagnostyczne z platformy Azure. Można zbierać dodatkowe dzienniki z innych rozwiązań do zarządzania i monitorowania na potrzeby zasobów w chmurze lub środowisku lokalnym. Do agregowania wszystkich tych danych służy usługa Log Analytics, która udostępnia centralne repozytorium. Z tego miejsca można uruchamiać zapytania, aby pomóc w rozwiązywaniu problemów lub zwizualizować dane.

- **Konfigurowanie alertów i akcji** alerty proaktywnie powiadamiają o warunkach krytycznych. Na podstawie wyzwalaczy związanych z problemami dotyczącymi metryk, dzienników lub kondycji usługi można podejmować akcje naprawcze. Można skonfigurować różne powiadomienia i akcje, a następnie wysyłać dane do narzędzi do zarządzania usługami IT.

::: zone target="docs"

 Rozpocznij monitorowanie następujących elementów:

- [Aplikacje](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Containers](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Maszyny wirtualne](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Sieci](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Aby monitorować inne zasoby, znajdź dodatkowe rozwiązania w witrynie Azure Marketplace.

Aby zapoznać się z usługą Azure Monitor, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>Akcja

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

::: zone-end

# <a name="azure-service-healthtabazureservicehealth"></a>[Azure Service Health](#tab/AzureServiceHealth)

Usługa Azure Service Health udostępnia spersonalizowany widok kondycji usług platformy Azure i używanych regionów. Informacje na temat aktywnych problemów są publikowane w usłudze Service Health, aby ułatwić zrozumienie wpływu na zasoby. Dzięki regularnym aktualizacjom będziesz otrzymywać informacje o rozwiązaniu problemu.

Publikujemy też zdarzenia planowanej konserwacji usługi Service Health, aby informować Cię o zmianach, które mogą wpłynąć na dostępność zasobów. Skonfiguruj alerty usługi Service Health, aby otrzymywać powiadomienia, gdy problemy z usługą, planowana konserwacja lub inne zmiany mogą mieć wpływ na usługi platformy Azure i regiony, których używasz.

Usługa Azure Service Health udostępnia następujące dane:

- **Stan platformy Azure:** globalny widok kondycji usług platformy Azure.
- **Kondycja usługi:** spersonalizowany widok kondycji usług Azure.
- **Kondycja zasobu:** dokładniejszy widok kondycji poszczególnych zasobów.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

## <a name="action"></a>Akcja

Aby skonfigurować alert usługi Service Health:

1. Przejdź do pozycji **Service Health**.
2. Wybierz pozycję **Alerty dotyczące kondycji**.
3. Utwórz alert dotyczący kondycji usługi.

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

Aby skonfigurować alert usługi Service Health, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Service Health](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabazureadvisor"></a>[Azure Advisor](#tab/AzureAdvisor)

Azure Advisor to bezpłatny, spersonalizowany konsultant, który ułatwia stosowanie i implementowanie najlepszych rozwiązań dotyczących wdrożeń platformy Azure. Analizuje on konfigurację zasobów i dane telemetryczne użycia, a następnie generuje rekomendacje dotyczące rozwiązań w zakresie optymalizacji środowiska. Rekomendacje są podzielone na cztery kategorie:

- **Wysoka dostępność:** w celu poprawienia ciągłości działania aplikacji krytycznych dla działania firmy. Rekomendacje mogą obejmować dodawanie maszyn wirtualnych do zestawu lub dodawanie punktów końcowych geograficznie nadmiarowych.
- **Bezpieczeństwo:** w celu wykrywania zagrożeń i luk w zabezpieczeniach, które mogą prowadzić do naruszeń zabezpieczeń. Rekomendacje mogą obejmować stosowanie szyfrowania dysku i włączanie sieciowych grup zabezpieczeń.
- **Wydajność:** w celu zwiększenia szybkości aplikacji. Rekomendacje mogą obejmować zwiększanie wydajności zapytań języka SQL przez tworzenie indeksów lub ponowne konfigurowanie ustawień usługi Traffic Manager.
- **Koszty:** w celu zoptymalizowania i zredukowania ogólnych wydatków związanych z platformą Azure. Rekomendacje mogą obejmować zmianę rozmiaru lub zamykanie rzadko używanych maszyn wirtualnych lub przełączanie do rezerwacji platformy Azure w celu obniżenia całkowitego kosztu posiadania.

Rekomendacje w usłudze Advisor są tworzone w oparciu o wdrażane zasoby i akcje wykonywane na platformie Azure. Można regularnie zapoznawać się z najnowszymi rekomendacjami usługi Advisor.

::: zone target="chromeless"

## <a name="action"></a>Akcja

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Explore Azure Advisor" :::

::: zone-end

::: zone target="docs"

Aby zapoznać się z usługą Azure Advisor, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorBlade).

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Advisor](https://docs.microsoft.com/azure/advisor).

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Usługa Azure Security Center również odgrywa ważną rolę w strategii monitorowania. Ułatwia ona monitorowanie zabezpieczeń maszyn, sieci, magazynu, usług danych i aplikacji. Usługa Security Center oferuje zaawansowane wykrywanie zagrożeń przy użyciu uczenia maszynowego i analizy behawioralnej, aby ułatwić identyfikację aktywnych zagrożeń atakujących zasoby platformy Azure. Ponadto udostępnia ona również ochronę przed zagrożeniami, która blokuje złośliwe oprogramowanie i inny niepożądany kod, a także zmniejsza obszar powierzchni narażony na ataki siłowe i inne ataki dotyczące sieci.

Gdy usługa Security Center zidentyfikuje zagrożenie, wyzwala alert zabezpieczeń z krokami, które należy wykonać w odpowiedzi na atak. Udostępnia również raport z informacjami na temat wykrytego zagrożenia.

Usługa Azure Security Center jest oferowana w dwóch warstwach: bezpłatna i standardowa. Funkcje, takie jak rekomendacje dotyczące zabezpieczeń, są dostępne bezpłatnie. Warstwa standardowa zapewnia dodatkową ochronę, taką jak zaawansowane wykrywanie zagrożeń i ochrona obciążeń chmury hybrydowej.

::: zone target="chromeless"

## <a name="action"></a>Akcja

**Wypróbuj usługę w warstwie Standardowa bezpłatnie przez pierwsze 30 dni.**

Po włączeniu i skonfigurowaniu zasad zabezpieczeń dla zasobów subskrypcji w sekcji **Zapobieganie** można wyświetlać stan zabezpieczeń zasobów oraz informacje o problemach. Listę tych problemów można również wyświetlić na kafelku **Zalecenia**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Aby zapoznać się z usługą Azure Security Center, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
