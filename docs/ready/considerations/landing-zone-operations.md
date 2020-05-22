---
title: Ulepszanie operacji strefy docelowej
description: Ulepszanie operacji strefy docelowej
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1e338974e3720609640b23e7123fc003801cb371
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756519"
---
# <a name="improve-landing-zone-operations"></a>Ulepszanie operacji strefy docelowej

Operacje strefy wyładunkowej zapewniają początkową podstawę do zarządzania operacjami. W miarę skalowania operacji te udoskonalenia spowodują, że w celu spełnienia rosnących wymagań w zakresie doskonałości, niezawodności i wydajności.

## <a name="landing-zone-operations-best-practices"></a>Najlepsze praktyki dotyczące operacji strefy wyładunkowej

Poniższe linki zapewniają najlepsze rozwiązania dotyczące ulepszania operacji strefy wyładunkowej.

- [Zarządzanie serwerem Azure](../../manage/azure-server-management/index.md): Przewodnik dołączania umożliwiający dołączenie natywnych narzędzi i usług w chmurze wymaganych do zarządzania operacjami.
- [Monitorowanie hybrydowe](../../manage/monitor/index.md): wielu klientów wprowadziło już znaczną inwestycję w System Center Operations Manager. W przypadku tych klientów ten przewodnik dotyczący monitorowania hybrydowego może pomóc im w porównywaniu i rozróżnieniu natywnych narzędzi do raportowania w chmurze za pomocą narzędzi Operations Manager. To porównanie ułatwia podjęcie decyzji o narzędziach, które mają być używane do zarządzania operacyjnego.
- [Scentralizowanie operacji zarządzania](../../manage/centralize-operations.md): Użyj usługi Azure Lighthouse, aby scentralizować Zarządzanie operacjami w wielu dzierżawach platformy Azure.
- [Ustanów przegląd sprawności operacyjnej](../../manage/operational-fitness-review.md): przegląd środowiska pod kątem sprawności operacyjnej.
- Najlepsze rozwiązania dotyczące operacji związanych z obciążeniem:
  - [Lista kontrolna odporności](https://docs.microsoft.com/azure/architecture/checklist/resiliency-per-service?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Analiza trybu błędu](https://docs.microsoft.com/azure/architecture/resiliency/failure-mode-analysis?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Odzyskiwanie po zakłóceniach usługi obejmujących cały region](https://docs.microsoft.com/azure/architecture/resiliency/recovery-loss-azure-region?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Odzyskiwanie po uszkodzeniu lub przypadkowym usunięciu danych](https://docs.microsoft.com/azure/architecture/framework/resiliency/data-management?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="four-steps-to-improve-operations-beyond-a-single-landing-zone"></a>Cztery kroki w celu poprawienia operacji poza jedną strefą docelową

[Zarządzanie metodologią](../../manage/index.md) zawiera ogólne wskazówki dotyczące tworzenia pojemności zarządzania operacjami [.](../../manage/index.md) Stosujemy podstawową strukturę tej metodologii oraz następujące kroki z tej metody, aby usprawnić operacje i operacje strefy wyładunkowej we wszystkich strefach wyładunkowych.

<!-- cSpell:ignore caf -->

![Zarządzanie metodologią](../../_images/manage/caf-manage.png)

1. [Ustanów linię bazową zarządzania](../../manage/azure-server-management/index.md): punkt odniesienia zarządzania stanowi podstawę do zarządzania operacjami. Wskazówki w ramach tego pierwszego kroku można zastosować do każdej strefy docelowej w celu usprawnienia operacji początkowych.
2. [Zdefiniuj zobowiązania biznesowe](../../manage/considerations/business-alignment.md): zrozumienie stanu krytycznego i wpływu poszczególnych obciążeń w ramach strefy docelowej spowoduje ustanowienie "definicji gotowe" dla wszelkich bieżących ulepszeń zarządzania dla każdej strefy docelowej. Ten proces również określi wymagania dotyczące niezawodności, wydajności i operacji dla każdego obciążenia.
3. [Rozwiń linię bazową zarządzania](../../manage/best-practices.md): ten zestaw najlepszych rozwiązań może zostać zastosowany w celu usprawnienia operacji strefy wyładunkowej poza początkową linią bazową.
4. [Zaawansowane operacje i zasady projektowania](../../manage/design-principles.md): przegląd projektowania i operacji konkretnych obciążeń, platform lub pełnych stref wyładunkowych w celu spełnienia bardziej szczegółowych wymagań.

## <a name="test-driven-development-cycle"></a>Cykl programowania oparty na testach

Przed rozpoczęciem wszelkich ulepszeń zabezpieczeń należy zrozumieć "definicję gotowe" i wszystkie "kryteria akceptacji". Aby uzyskać więcej informacji, zapoznaj się z artykułami dotyczącymi [opracowywania testów w strefach lądowania](./test-driven-development.md) i [opracowywanie testów na platformie Azure](./azure-test-driven-development.md).

![Proces projektowania oparty na testach dla stref wyładunku w chmurze](../../_images/ready/test-driven-development-process.png)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [usprawnić zarządzanie strefami wyładunkowymi](./landing-zone-governance.md) , aby obsługiwać wdrażanie na dużą skalę.

> [!div class="nextstepaction"]
> [Ulepszanie ładu strefy docelowej](./landing-zone-governance.md)
