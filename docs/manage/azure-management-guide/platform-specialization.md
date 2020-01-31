---
title: Specjalizacja platformy dotycząca zarządzania chmurą na platformie Azure
description: Ulepsz operacje zarządzania chmurą charakterystyczne dla platformy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9c4f18c4c81dce2caa41b1dab5dddc394042f390
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808179"
---
# <a name="platform-specialization-for-cloud-management"></a>Specjalizacja platformy dotycząca zarządzania chmurą

Podobnie jak rozszerzony plan bazowy zarządzania, specjalizacja platformy to rozszerzenie wykraczające poza standardowy plan bazowy zarządzania. Na poniższej ilustracji i liście przedstawiono sposoby rozwijania planu bazowego zarządzania. Ten artykuł dotyczy opcji specjalizacji platformy.

![Rozszerzenie planu bazowego zarządzania chmurą](../../_images/manage/beyond-the-baseline.png)

- **Operacje obciążeń:** Inwestycje w operacje największe na obciążenie i najwyższy poziom odporności. Zalecamy operacje obciążeń dla około 20% obciążeń, które zwiększają wartość biznesową. Ta specjalizacja jest zazwyczaj zarezerwowana dla obciążeń o dużym lub krytycznym znaczeniu.
- **Operacje platformy:** Inwestycje w operacje są rozłożone na wiele obciążeń. Ulepszenia w zakresie odporności wpływają na wszystkie obciążenia korzystające ze zdefiniowanej platformy. Sugerujemy operacje platformy dla około 20% platform o krytycznym znaczeniu. Ta specjalizacja jest zazwyczaj zarezerwowana dla obciążeń o średniej i dużej ważności.
- **Rozszerzony plan bazowy zarządzania:** Relatywnie najniższe inwestycje w operacje. Ta specjalizacja nieco udoskonala zobowiązania biznesowe dzięki dodatkowym, natywnym dla chmury narzędziom i procesom obsługi operacji.

Zarówno operacje obciążeń, jak i operacje platformy wymagają zmian w zasadach projektowania i architektury. Ich wprowadzenie może zająć trochę czasu i spowodować zwiększenie kosztów operacyjnych. Rozszerzony plan bazowy zarządzania pozwala zmniejszyć liczbę obciążeń wymagających takich inwestycji, zapewniając wystarczającą poprawę zobowiązania biznesowego.

W tej tabeli przedstawiono kilka typowych procesów i narzędzi oraz potencjalne efekty związane z używaniem rozszerzonych planów bazowych zarządzania:

|Proces  |Narzędzie  |Przeznaczenie  |Sugerowany poziom zarządzania  |
|---------|---------|---------|---------|
|Ulepszanie projektu systemu|Azure Architecture Framework|Ulepszanie projektu architektury platformy w celu usprawnienia operacji|Nie dotyczy|
|Automatyzacja korygowania|Azure Automation|Reagowanie na zaawansowane dane platformy przy użyciu automatyzacji specyficznej dla platformy|Operacje platformy|
|Wykaz usług|Centrum aplikacji zarządzanych|Udostępnianie samoobsługowego katalogu zatwierdzonych rozwiązań, które spełniają standardy organizacji|Operacje platformy|
|Wydajność kontenerów|Usługa Azure Monitor dla kontenerów|Monitorowanie i diagnostyka kontenerów|Operacje platformy|
|Wydajność danych w modelu PaaS — platforma jako usługa|Azure SQL Analytics|Monitorowanie i diagnostyka baz danych PaaS|Operacje platformy|
|Wydajność danych w modelu IaaS — infrastruktura jako usługa|SQL Server Health Check|Monitorowanie i diagnostyka baz danych IaaS|Operacje platformy|

## <a name="high-level-process"></a>Przetwarzanie wysokiego poziomu

Specjalizacja platformy obejmuje zdyscyplinowane wykonywanie czterech poniższych procesów w ramach podejścia iteracyjnego. Każdy z tych procesów omówiono bardziej szczegółowo w kolejnych sekcjach tego artykułu.

- **Ulepszanie projektu systemu:** Usprawnij projektowanie typowych systemów lub platform, aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach większy sens może mieć automatyzacja korygowania i ograniczenie wpływu przerw.
- **Skalowanie rozwiązania:** W miarę ulepszania projektu systemów i zautomatyzowanego korygowania zmiany te można skalować na całe środowisko za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Różne narzędzia do monitorowania umożliwiają wykrywanie ulepszeń przyrostowych. Te ulepszenia można wprowadzić w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

::: zone target="docs"

## <a name="improve-system-design"></a>Ulepszanie projektu systemu

::: zone-end
::: zone target="chromeless"

## <a name="improve-system-designtabsystemsdesign"></a>[Ulepszanie projektu systemu](#tab/SystemsDesign)

::: zone-end

Ulepszanie projektu systemu to najbardziej efektywne podejście do usprawnienia operacji na każdej typowej platformie. Ulepszenia projektu systemu sprzyjają wzrostowi stabilności i ograniczeniu przerw w działaniu. Projektowanie poszczególnych systemów jest poza zakresem widoku środowiska w rozwiązaniu Cloud Adoption Framework dla platformy Azure.

W ramach uzupełnienia tego rozwiązania usługa Azure Architecture Framework oferuje najlepsze rozwiązania w zakresie poprawy odporności i projektowania określonego systemu. Te udoskonalenia projektowe można stosować do projektowania systemów platformy lub określonego obciążenia.

Usługa Azure Architecture Framework koncentruje się na poprawie pięciu filarów projektowania systemu:

- **Skalowalność:** Skalowanie typowych zasobów platformy w celu obsługi zwiększonego obciążenia
- **Dostępność:** Ograniczenie przerw w działaniu przez zwiększenie potencjału czasu pracy
- **Odporność:** Skrócenie czasu odzyskiwania w celu ograniczenia czasu trwania przerw
- **Bezpieczeństwo:** Ochrona aplikacji i danych przed zagrożeniami zewnętrznymi
- **Zarządzanie:** Procesy operacyjne charakterystyczne dla tych typowych zasobów platformy

Dług techniczny i błędy architektury powodują większość przerw w działalności biznesowej. W przypadku istniejących wdrożeń ulepszenia projektowania systemów można widzieć jako płatności związane z istniejącym długiem technicznym. W przypadku nowych wdrożeń te ulepszenia można widzieć jako unikanie długu technicznego.

Na poniższej karcie **Zautomatyzowane korygowanie** pokazano sposoby korygowania długu technicznego, którego nie można lub nie należy się pozbywać.

Dowiedz się więcej na temat usługi [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/guide/pillars), aby ulepszyć projektowanie systemu.

W miarę ulepszania projektu systemu wracaj do tego artykułu, aby znaleźć nowe możliwości ulepszania i skalowania tych ulepszeń w swoim środowisku.

::: zone target="docs"

## <a name="automated-remediation"></a>Zautomatyzowane korygowanie

::: zone-end
::: zone target="chromeless"

## <a name="automated-remediationtabautomatedremediation"></a>[Zautomatyzowane korygowanie](#tab/AutomatedRemediation)

::: zone-end

Niektórych długów technicznych nie można się pozbyć. Rozwiązanie może być zbyt drogie w naprawie lub może być zaplanowane, ale czas trwania projektu może być długi. Może się zdarzyć, że przerwa w działalności nie ma znaczącego wpływu na firmę. Może też się okazać, że priorytetem firmy jest szybkie odzyskiwanie, a nie inwestowanie w odporność.

Jeśli pozbycie się długu technicznego nie jest najbardziej pożądane, następnym krokiem jest zazwyczaj zautomatyzowane korygowanie. Najpopularniejszą metodą zautomatyzowanego korygowania jest wykrywanie trendów i zapewnienie zautomatyzowanego korygowania przy użyciu usług Azure Automation i Azure Monitor.

Aby uzyskać wskazówki dotyczące zautomatyzowanego korygowania, zobacz [Azure Automation i alerty](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

::: zone target="docs"

## <a name="scale-the-solution-with-a-service-catalog"></a>Skalowanie rozwiązania przy użyciu katalogu usług

::: zone-end
::: zone target="chromeless"

## <a name="scale-the-solution-with-a-service-catalogtabservicecatalog"></a>[Skalowanie rozwiązania przy użyciu katalogu usług](#tab/ServiceCatalog)

::: zone-end

Podstawą specjalizacji platformy i operacji platformy jest dobrze zarządzany katalog usług. Korzystając z niego, można skalować ulepszenia projektowania i korygowania systemów w środowisku.

Zespół platformy w chmurze współpracuje z zespołem automatyzacji chmury, tworząc powtarzalne rozwiązania dla najpopularniejszych platform w dowolnym środowisku. Jeśli jednak te rozwiązania nie są wykorzystywane w sposób spójny, zarządzanie chmurą zapewnia nieco więcej niż oferta planu bazowego.

Aby zmaksymalizować wdrożenie i zminimalizować nakłady na konserwację dowolnej zoptymalizowanej platformy, należy dodać platformę do katalogu usług na platformie Azure. Każdą aplikację w katalogu można wdrożyć do użytku wewnętrznego za pośrednictwem katalogu usług lub jako ofertę platformy handlowej dla użytkowników zewnętrznych.

Aby uzyskać instrukcje dotyczące publikowania w katalogu usług, zapoznaj się z serią artykułów na stronie [publikowania w katalogu usług](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="deploy-applications-from-the-service-catalog"></a>Wdrażanie aplikacji z katalogu usług

1. W witrynie Azure Portal przejdź do pozycji **Centrum aplikacji zarządzanych (wersja zapoznawcza)** .
2. W okienku **Przeglądaj** wybierz pozycję **Aplikacje w katalogu usług**.
3. Kliknij pozycję **+ Dodaj**, aby wybrać definicję aplikacji z katalogu usług firmy.

Zostaną wyświetlone wszystkie obsługiwane aplikacje zarządzane.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/browseServiceCatalog]" submitText="Go to Virtual Machines" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

### <a name="manage-service-catalog-applications"></a>Zarządzanie aplikacjami w katalogu usług

1. W witrynie Azure Portal przejdź do pozycji **Centrum aplikacji zarządzanych (wersja zapoznawcza)** .
1. W okienku **Usługa** wybierz pozycję **Aplikacje w katalogu usług**.

Zostaną wyświetlone wszystkie obsługiwane aplikacje zarządzane.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Appliance/ManagedAppsHubBlade/serviceServiceCatalogApps]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="continuous-improvement"></a>Ciągłe ulepszanie

::: zone-end
::: zone target="chromeless"

## <a name="continuous-improvementtabcontinuousimprovement"></a>[Ciągłe ulepszanie](#tab/ContinuousImprovement)

::: zone-end

Specjalizacja i operacje platformy zależą od silnych cykli wymiany opinii między zespołami wdrażania, platformy, automatyzacji i zarządzania. Osadzenie tych cykli wymiany opinii w danych pomaga każdemu zespołowi podejmować mądre decyzje. W przypadku operacji platformy w celu osiągnięcia długoterminowych zobowiązań biznesowych ważne jest użycie szczegółowych informacji dotyczących scentralizowanej platformy.

Dwie najpopularniejsze platformy centralnego zarządzana to kontenery i SQL Server. Te artykuły mogą ułatwić rozpoczęcie pracy ze zbieraniem danych ciągłego ulepszania na tych platformach:

- [Wydajność kontenerów](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Wydajność bazy danych PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Wydajność bazy danych IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
