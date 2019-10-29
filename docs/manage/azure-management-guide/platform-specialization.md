---
title: Specjalizacja platformy dotycząca zarządzania chmurą na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ulepsz operacje zarządzania chmurą charakterystyczne dla platformy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0386a8c30758cce6c1c3d23bfa73d1f90e919692
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72556976"
---
# <a name="platform-specialization-for-cloud-management"></a>Specjalizacja platformy dotycząca zarządzania chmurą

Podobnie jak rozszerzony plan bazowy zarządzania, specjalizacja platformy to rozszerzenie wykraczające poza standardowy plan bazowy zarządzania. Poniżej przedstawiono wizualizację i listę punktowaną metod rozwinięcia planu bazowego zarządzania. Ten artykuł dotyczy opcji specjalizacji platformy.

![Rozszerzenie planu bazowego zarządzania chmurą](../../_images/manage/beyond-the-baseline.png)

- **Operacje obciążeń:** Inwestycje w operacje największe na obciążenie. Najwyższy poziom odporności. Zalecane dla +/-20% obciążeń, które zwiększają wartość biznesową. Zazwyczaj zarezerwowane dla obciążeń o dużym lub krytycznym znaczeniu.
- **Operacje platformy:** Inwestycje w operacje są rozłożone na wiele obciążeń. Ulepszenia w zakresie odporności mają wpływ na wszystkie obciążenia, które korzystają ze zdefiniowanej platformy. Zalecane dla +/-20% platform o krytycznym znaczeniu. Zazwyczaj zarezerwowane dla obciążeń o średniej i dużej ważności.
- **Rozszerzony plan bazowy zarządzania:** Relatywnie najniższe inwestycje w operacje. Nieco udoskonalone zobowiązania biznesowe dzięki dodatkowym, natywnym dla chmury narzędziom i procesom obsługi operacji.

Zarówno operacje związane z obciążeniami, jak i z platformą wymagają zmian w projekcie i architekturze. Ich wprowadzenie może zająć trochę czasu i spowodować zwiększenie kosztów operacyjnych. Rozszerzony plan bazowy zarządzania pozwala zmniejszyć liczbę obciążeń wymagających takich inwestycji, zapewniając wystarczającą poprawę zobowiązania biznesowego.

W poniższej tabeli przedstawiono kilka typowych procesów i narzędzi oraz potencjalnych efektów związanych z używaniem rozszerzonych planów bazowych zarządzania.

|Proces  |Narzędzie  |Przeznaczenie  |Sugerowany poziom zarządzania  |
|---------|---------|---------|---------|
|Ulepszanie projektu systemu|Azure Architecture Framework|Ulepszanie projektu architektury platformy w celu usprawnienia operacji|
|Automatyzacja korygowania|Azure Automation|Reagowanie na zaawansowane dane platformy przy użyciu automatyzacji specyficznej dla platformy|Operacje platformy|
|Katalog usług|Centrum aplikacji zarządzanych|Udostępnianie samoobsługowego katalogu zatwierdzonych rozwiązań, które spełniają standardy organizacji|Operacje platformy|
|Wydajność kontenerów|Usługa Azure Monitor dla kontenerów|Monitorowanie i diagnostyka kontenerów|Operacje platformy|
|Wydajność danych PaaS|Azure SQL Analytics|Monitorowanie i diagnostyka baz danych PaaS|Operacje platformy|
|Wydajność danych IaaS|SQL Server Health Check|Monitorowanie i diagnostyka baz danych IaaS|Operacje platformy|

## <a name="high-level-process"></a>Przetwarzanie wysokiego poziomu

Specjalizacja platformy obejmuje zdyscyplinowane wykonywanie czterech poniższych procesów w ramach podejścia iteracyjnego. Każdy z tych procesów omówiono bardziej szczegółowo w kolejnych sekcjach tego artykułu.

- **Ulepszanie projektu systemu:** Usprawnij projektowanie typowych systemów (lub platform), aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach większy sens może mieć automatyzacja korygowania i ograniczenie wpływu przerw.
- **Skalowanie rozwiązania:** W miarę ulepszania projektu systemów i zautomatyzowanego korygowania zmiany te można skalować na całe środowisko za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Różne narzędzia do monitorowania umożliwiają wykrywanie ulepszeń przyrostowych, które można wprowadzić w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

::: zone target="docs"

## <a name="improve-system-design"></a>Ulepszanie projektu systemu

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Ulepszanie projektu systemu](#tab/SystemsDesign)

::: zone-end

Ulepszanie projektu systemu to najbardziej efektywne podejście do usprawnienia operacji na każdej typowej platformie. Ulepszenia projektu systemu sprzyjają wzrostowi stabilności i ograniczeniu przerw w działaniu. Projektowanie poszczególnych systemów jest poza zakresem widoku środowiska na platformie Cloud Adoption Framework. W ramach uzupełnienia tej platformy usługa Azure Architecture Framework oferuje najlepsze rozwiązania w zakresie poprawy odporności i projektowania określonego systemu. Te udoskonalenia projektowe można stosować do projektowania systemów platformy lub określonego obciążenia.

Usługa Azure Architecture Framework koncentruje się na poprawie pięciu filarów projektowania systemu:

- **Skalowalność:** Skalowanie typowych zasobów platformy w celu obsługi zwiększonego obciążenia.
- **Dostępność:** Ograniczenie przerw w działaniu przez zwiększenie potencjału czasu pracy.
- **Odporność:** Skrócenie czasu odzyskiwania w celu ograniczenia czasu trwania przerw.
- **Bezpieczeństwo:** Ochrona aplikacji i danych przed zagrożeniami zewnętrznymi.
- **Zarządzanie:** Procesy operacyjne charakterystyczne dla tych typowych zasobów platformy.

Większość przerw w działalności biznesowej oznacza jakąś formę długu technicznego lub brak w architekturze. W przypadku istniejących wdrożeń ulepszenia projektowania systemów można widzieć jako płatności związane z istniejącym długiem technicznym. W przypadku nowych wdrożeń ulepszenia projektowania systemów można widzieć jako unikanie długu technicznego. Następna karta „Zautomatyzowane korygowanie” szuka sposobów usuwania długu technicznego, którego nie można lub nie należy się pozbywać.

Dowiedz się więcej na temat usługi [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars), aby ulepszyć projektowanie systemu.

W miarę ulepszania projektu systemu wracaj do tego artykułu, aby znaleźć nowe możliwości ulepszania i skalowania tych ulepszeń w swoim środowisku.

::: zone target="docs"

## <a name="automated-remediation"></a>Zautomatyzowane korygowanie

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Zautomatyzowane korygowanie](#tab/AutomatedRemediation)

::: zone-end

Niektórych długów technicznych nie można się pozbyć. Rozwiązanie może być zbyt drogie w naprawie. Rozwiązanie może być zaplanowane, ale czas trwania projektu może być długi. Może się zdarzyć, że przerwa w działalności nie ma znaczącego wpływu na firmę lub że priorytetem firmy jest szybkie odzyskiwanie, a nie inwestowanie w odporność.

Jeśli pozbycie się długu technicznego nie jest najbardziej pożądane, następnym krokiem jest zazwyczaj zautomatyzowane korygowanie. Najpopularniejszą metodą zautomatyzowanego korygowania jest wykrywanie trendów i zapewnienie zautomatyzowanego korygowania przy użyciu usług Azure Automation i Azure Monitor.

Aby uzyskać wskazówki dotyczące zautomatyzowanego korygowania, zobacz ten artykuł na stronie [Azure Automation i alerty](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skalowanie rozwiązania przy użyciu katalogu usług

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Skalowanie rozwiązania przy użyciu katalogu usług](#tab/ServiceCatalog)

::: zone-end

Podstawą specjalizacji platformy i operacji platformy jest dobrze zarządzany katalog usług. Jest to sposób skalowania ulepszeń projektowania i korygowania systemów w środowisku. Zespół platformy w chmurze współpracuje z zespołem automatyzacji chmury, tworząc powtarzalne rozwiązania dla najpopularniejszych platform w dowolnym środowisku. Jeśli jednak te rozwiązania nie są wykorzystywane w sposób spójny, zarządzanie chmurą zapewnia nieco więcej niż oferta planu bazowego.

Aby zmaksymalizować wdrożenie i zminimalizować nakłady na konserwację dowolnej zoptymalizowanej platformy, należy dodać platformę do katalogu usług na platformie Azure. Każdą aplikację w katalogu można wdrożyć do użytku wewnętrznego za pośrednictwem katalogu usług lub jako ofertę platformy handlowej dla użytkowników zewnętrznych.

Aby uzyskać instrukcje dotyczące publikowania w katalogu usług, zapoznaj się z serią artykułów na stronie [publikowania w katalogu usług](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Wdrażanie aplikacji z katalogu usług

1. W witrynie Azure Portal wyszukaj pozycję **Centrum aplikacji zarządzanych (wersja zapoznawcza)** .
2. Kliknij pozycję **Aplikacje w katalogu usług** w sekcji **Przeglądaj** nawigacji w portalu.
3. Kliknij pozycję **+ Dodaj**, aby wybrać definicję aplikacji z katalogu usług firmy.

W tym miejscu są wyświetlane wszystkie obsługiwane aplikacje zarządzane.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Zarządzanie aplikacjami w katalogu usług

1. W witrynie Azure Portal wyszukaj pozycję **Centrum aplikacji zarządzanych (wersja zapoznawcza)** .
2. Kliknij pozycję **Aplikacje w katalogu usług** w sekcji **Usługa** nawigacji w portalu.

W tym miejscu są wyświetlane wszystkie obsługiwane aplikacje zarządzane.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Ciągłe ulepszanie

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Ciągłe ulepszanie](#tab/ContinuousImprovement)

::: zone-end

Specjalizacja i operacje platformy zależą od silnych cykli wymiany opinii między zespołami wdrażania, platformy, automatyzacji i zarządzania. Osadzenie tych cykli wymiany opinii w danych pozwala każdemu zespołowi podejmować mądre decyzje. W przypadku operacji platformy w celu osiągnięcia długoterminowych zobowiązań biznesowych ważne jest wykorzystanie szczegółowych informacji dotyczących scentralizowanej platformy. Ponieważ dwie najpopularniejsze platformy centralnego zarządzana to kontenery i SQL Server, poniżej przedstawiono kilka artykułów ułatwiających rozpoczęcie pracy ze zbieraniem danych ciągłego ulepszania.

[Wydajność kontenera](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
[Wydajność bazy danych PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
[Wydajność bazy danych IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
