---
title: Rozszerzony plan bazowy zarządzania na platformie Azure
description: Skorzystaj z podręcznika Cloud Adoption Framework dla platformy Azure, aby uzyskać informacje o typowych usprawnieniach planu bazowego zarządzania.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4d17c8fe7251a4ce5281f94d8776ba5ceaddd181
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621231"
---
<!-- cSpell:ignore ITSMC -->

# <a name="enhanced-management-baseline-in-azure"></a>Rozszerzony plan bazowy zarządzania na platformie Azure

Pierwsze trzy dyscypliny zarządzania chmurą opisują plan bazowy zarządzania. W poprzednich artykułach tego przewodnika omówiono minimalną konieczną funkcjonalność (MVP) dla usług zarządzania chmurą, określaną jako plan bazowy zarządzania. W tym artykule przedstawiono kilka typowych usprawnień planu bazowego.

Celem planu bazowego zarządzania jest utworzenie spójnej oferty zapewniającej minimalny poziom zobowiązania biznesowego dla _wszystkich_ obsługiwanych obciążeń. Taki plan bazowy wspólnych, powtarzalnych ofert zarządzania umożliwia zespołowi skuteczne optymalizowanie zarządzania operacyjnego z minimalnymi odchyleniami.

Może być jednak konieczne zwiększenie zaangażowania w działalność biznesową, wykraczające poza zakres oferty standardowej. Na poniższej ilustracji i na liście przedstawiono trzy sposoby rozszerzenia planu bazowego zarządzania.

![Rozszerzenie planu bazowego zarządzania chmurą](../../_images/manage/beyond-the-baseline.png)

- **Rozszerzony plan bazowy zarządzania:**
  - Dodaj rozszerzenia planu bazowego zarządzania, jeśli większość obciążeń w portfolio ma wspólne wymaganie.
  - To zapewnia udoskonalone zobowiązania biznesowe dzięki dodatkowym, natywnym dla chmury narzędziom i procesom obsługi operacji.
  - Rozszerzenia planu bazowego nie powinny mieć wpływu na architekturę poszczególnych obciążeń.
- **Operacje obciążeń:**
  - Inwestycje w operacje największe na obciążenie.
  - Najwyższy poziom odporności.
  - Zalecane dla około 20% obciążeń, które zwiększają wartość biznesową.
  - Zwykle zarezerwowane dla obciążeń o dużym lub krytycznym znaczeniu.
- **Operacje platformy:**
  - Inwestycje w operacje są rozłożone na wiele obciążeń.
  - Ulepszenia w zakresie odporności wpływają na wszystkie obciążenia korzystające ze zdefiniowanej platformy.
  - Zalecane dla około 20% platform o krytycznym znaczeniu.
  - Zwykle zarezerwowane dla obciążeń o średniej i dużej ważności.

Zarówno operacje obciążeń, jak i operacje platformy wymagają zmian w zasadach projektowania i architektury. Ich wprowadzenie może zająć trochę czasu i spowodować zwiększenie kosztów operacyjnych. Rozszerzony plan bazowy zarządzania pozwala zmniejszyć liczbę obciążeń wymagających takich inwestycji, zapewniając wystarczającą poprawę zobowiązania biznesowego.

W tej tabeli przedstawiono kilka procesów i narzędzi oraz potencjalne efekty związane z używaniem rozszerzonych planów bazowych zarządzania:

| Dyscyplina  | Proces  | Narzędzie | Potencjalny wpływ | Dowiedz się więcej |
|---|---|---|---|---|
| Spis i widoczność | Śledzenie zmiany usługi | Azure Resource Graph | Lepszy wgląd w zmiany usług platformy Azure może pomóc w szybszym wykrywaniu negatywnych skutków lub korygowaniu. | [Omówienie usługi Azure Resource Graph](https://docs.microsoft.com/azure/governance/resource-graph/overview) |
| Spis i widoczność | Integracja zarządzania usługami IT (ITSM) | Łącznik zarządzania usługami IT | Automatyczne połączenie z narzędziem ITSM zapewnia lepsze rozeznanie. | [Łącznik zarządzania usługami IT (ITSMC)](https://docs.microsoft.com/azure/azure-monitor/platform/itsmc-overview) |
| Zgodność operacyjna | Automatyzacja operacji | Azure Automation | Automatyzacja zgodności operacyjnej umożliwia szybsze i bardziej precyzyjne reagowanie na zmianę. | Więcej informacji znajduje się w poniższych sekcjach. |
| Zgodność operacyjna | Automatyzacja wydajności | Azure Automation | Zautomatyzuj proces zapewnienia zgodności operacyjnej z oczekiwaniami dotyczącymi wydajności, aby rozwiązać typowe problemy ze skalowaniem lub rozmiarem określonych zasobów. | Więcej informacji znajduje się w poniższych sekcjach. |
| Zgodność operacyjna | Operacje w wielu chmurach | Azure Automation — hybrydowy proces roboczy elementu Runbook | Automatyzacja operacji w wielu chmurach. | [Omówienie hybrydowego procesu roboczego elementu Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker) |
| Zgodność operacyjna | Automatyzacja gościa |  Konfiguracja żądanego stanu (Desired State Configuration, DSC) | Oparta na kodzie konfiguracja systemów operacyjnych gościa zmniejsza liczbę błędów i odchyleń konfiguracji. | [Omówienie konfiguracji DSC](https://docs.microsoft.com/powershell/scripting/dsc/overview/overview) |
| Ochrona i odzyskiwanie | Powiadomienie o naruszeniu | Azure Security Center | Rozszerzenie ochrony o wyzwalacze odzyskiwania po naruszeniu zabezpieczeń. | Więcej informacji znajduje się w poniższych sekcjach. |

::: zone target="docs"

## <a name="azure-automation"></a>Azure Automation

::: zone-end
::: zone target="chromeless"

## <a name="azure-automation"></a>[Azure Automation](#tab/AzureAutomation)

::: zone-end

Usługa Azure Automation udostępnia scentralizowany system do zarządzania zautomatyzowanymi mechanizmami kontrolnymi. W usłudze Azure Automation można uruchamiać proste procesy korygowania, skalowania i optymalizacji w odpowiedzi na metryki środowiskowe. Te procesy zmniejszają nakład pracy związanej z ręcznym przetwarzaniem zdarzeń.

Najważniejsze jest to, że automatyczne korygowanie można wykonywać niemal w czasie rzeczywistym, co znacznie ogranicza przerwy w działaniu procesów biznesowych. Analiza najczęstszych przerw w działalności biznesowej umożliwia zidentyfikowanie działań, które można zautomatyzować.

### <a name="runbooks"></a>Elementy Runbook

Element Runbook to podstawowa jednostka kodu umożliwiająca wykonanie automatycznego korygowania. Elementy Runbook zawierają instrukcje korygowania lub odzyskiwania po wystąpieniu zdarzenia.

Aby utworzyć elementy Runbook lub zarządzać nimi:

1. Wybierz pozycję **Azure Automation**.
1. Wybierz pozycję **Konta usługi Automation** i zaznacz jedno z wyświetlonych kont.
1. Przejdź do pozycji **Automatyzacja procesów**.
1. Przedstawione opcje umożliwiają tworzenie elementów Runbook, harmonogramów i innych funkcji automatycznego korygowania oraz zarządzanie nimi.

::: zone target="chromeless"

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Automation%2FAutomationAccounts]" submitText="Go to Azure Automation" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
::: zone target="docs"

## <a name="azure-security-center"></a>Azure Security Center

::: zone-end
::: zone target="chromeless"

## <a name="azure-security-center"></a>[Azure Security Center](#tab/AzureSecurityCenter)

::: zone-end

Usługa Azure Security Center również odgrywa ważną rolę w strategii ochrony i odzyskiwania. Ułatwia ona monitorowanie zabezpieczeń maszyn, sieci, magazynu, usług danych i aplikacji.

Usługa Azure Security Center oferuje zaawansowane wykrywanie zagrożeń przy użyciu uczenia maszynowego i analizy behawioralnej, aby ułatwić identyfikację aktywnych zagrożeń atakujących zasoby platformy Azure. Ponadto udostępnia ona również ochronę przed zagrożeniami, która blokuje złośliwe oprogramowanie i inny niepożądany kod, a także zmniejsza obszar powierzchni narażony na ataki siłowe i inne ataki dotyczące sieci.

Gdy usługa Azure Security Center zidentyfikuje zagrożenie, wyzwala alert zabezpieczeń z krokami, które należy wykonać w odpowiedzi na atak. Udostępnia również raport z informacjami na temat wykrytego zagrożenia.

Usługa Azure Security Center jest oferowana w dwóch warstwach: Bezpłatna i Standardowa. Funkcje, takie jak rekomendacje dotyczące zabezpieczeń, są dostępne w warstwie Bezpłatna. Warstwa Standardowa zapewnia dodatkową ochronę, taką jak zaawansowane wykrywanie zagrożeń i ochrona obciążeń chmury hybrydowej.

::: zone target="chromeless"

### <a name="action"></a>Akcja

#### <a name="try-standard-tier-for-free-for-your-first-30-days"></a>Wypróbuj usługę w warstwie Standardowa bezpłatnie przez pierwsze 30 dni

Po włączeniu i skonfigurowaniu zasad zabezpieczeń dla zasobów subskrypcji w okienku **Zapobieganie** można wyświetlić stan zabezpieczeń zasobów oraz informacje o problemach. Listę tych problemów można również wyświetlić na kafelku **Zalecenia**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Aby zapoznać się z usługą Azure Security Center, przejdź do witryny [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

### <a name="learn-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
