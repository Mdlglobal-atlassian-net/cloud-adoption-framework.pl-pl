---
title: Wprowadzenie do przewodnika migracji na platformę Azure
description: Dowiedz się, jak skutecznie wykonać migrację usług organizacji na platformę Azure, korzystając ze szczegółowych wskazówek.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 4d2bb420609bb703a1f32b0912eb9c17ccabe4e9
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225505"
---
# <a name="azure-migration-guide-before-you-start"></a>Przewodnik po migracji na platformę Azure: Przed rozpoczęciem

[Metodologia migracji przewodnika Cloud Adoption Framework](../index.md) prowadzi czytelników przez iteracyjny proces migrowania jednego obciążenia lub małej kolekcji obciążeń na wersję. W każdej iteracji przeprowadzany jest proces oceny, migracji oraz optymalizacji i podwyższania poziomu w celu zapewnienia, że obciążenia są gotowe do spełnienia wymagań produkcyjnych. Ten proces niezależny od chmury może prowadzić przez migrację do dowolnego dostawcy chmury.

W tym przewodniku przedstawiono uproszczoną wersję tego procesu na potrzeby migrowania ze środowiska lokalnego na platformę **Azure**.

::: zone target="docs"

> [!TIP]
> Aby zapoznać się z tym przewodnikiem w środowisku interaktywnym, skorzystaj z witryny Azure Portal. Przejdź do [centrum przewodników Szybki start platformy Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) w witrynie Azure Portal, wybierz pozycję **Migrowanie swojego środowiska na platformę Azure**, a następnie postępuj zgodnie z instrukcjami krok po kroku.

::: zone-end

## <a name="migration-tools"></a>[Narzędzia migracji](#tab/MigrationTools)

Ten przewodnik jest sugerowaną ścieżką pierwszej migracji na platformę Azure, ponieważ umożliwia on zapoznanie się z metodologią i narzędziami natywnymi dla chmury, które są najczęściej używane podczas migracji na platformę Azure. Te narzędzia są prezentowane na następujących stronach:

> [!div class="checklist"]
>
> - **Ocena dopasowania każdego obciążenia pod względem technicznym.** Sprawdź gotowość techniczną i możliwości migracji.
> - **Migrowanie usług.** Przeprowadź rzeczywistą migrację przez replikację zasobów lokalnych na platformę Azure.
> - **Zarządzanie kosztami i rozliczeniami:** Poznaj narzędzia wymagane do kontrolowania kosztów na platformie Azure.
> - **Optymalizowanie i podwyższanie poziomu.** Optymalizuj pod kątem równowagi między kosztem i wydajnością przed podwyższeniem poziomu obciążenia do środowiska produkcyjnego.
> - **Uzyskiwanie pomocy.** Korzystaj z pomocy i obsługi technicznej podczas wykonywania czynności związanych z migracją lub po migracji.

Przyjęto założenie, że strefa docelowa została już wdrożona, zgodnie z najlepszymi rozwiązaniami w [metodologii gotowości przewodnika Cloud Adoption Framework](../../ready/index.md).

## <a name="when-to-use-this-guide"></a>[Kiedy należy korzystać z tego przewodnika](#tab/WhenToUseThisGuide)

Narzędzia omówione w tym przewodniku obsługują szeroką gamę scenariuszy migracji, jednak w tym przewodniku skupiono się na ograniczonym nakładzie pracy przy _minimalnej złożoności_. Aby określić, czy ten przewodnik migracji jest odpowiedni dla Twojego projektu, zastanów się, czy następujące warunki mają zastosowanie w Twoim przypadku:

- Obciążenia na potrzeby początkowej migracji nie są krytyczne dla działania i nie zawierają poufnych danych.
- Wykonujesz migrację homogenicznego środowiska.
- Do wykonania migracji wymagane jest dopasowanie tylko kilku jednostek biznesowych.
- Nie planujesz automatyzacji całej migracji.
- Migrujesz niewielką liczbę serwerów.
- Mapowanie zależności składników do zmigrowania można łatwo zdefiniować.
- Twoja branża ma minimalne wymagania prawne dotyczące tej migracji.

Jeśli którykolwiek z tych warunków nie ma zastosowania w Twojej sytuacji, zamiast tego należy rozważyć skorzystanie z [przewodnika o rozszerzonym zakresie](../expanded-scope/index.md). Zalecamy również zgłoszenie się po pomoc do jednego z naszych zespołów Microsoft lub partnerów w przypadku wykonywania migracji wymagających przewodnika o rozszerzonym zakresie. Klienci, którzy kontaktują się z firmą Microsoft lub certyfikowanymi partnerami, odnoszą większy sukces w tych scenariuszach. Więcej informacji na temat uzyskiwania pomocy zawiera ten przewodnik.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Aby uzyskać więcej informacji, zobacz:

- [Przewodnik o rozszerzonym zakresie](../expanded-scope/index.md)

::: zone-end
