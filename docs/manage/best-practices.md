---
title: Wprowadzenie do zarządzania operacyjnego
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Omówienie zarządzania operacyjnego w strukturze wdrażania chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 23b9064b91744d5464f89ed4edf64c8d656514a5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558105"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Tworzenie działań związanych z zarządzaniem operacyjnym w chmurze

Wdrożenie chmury pozwala szybciej zwiększyć wartość biznesową. Jednak rzeczywista wartość biznesowa jest uzyskiwana za pośrednictwem ciągłych, stabilnych operacji dotyczących zasobów technologicznych wdrożonych w chmurze. Ta sekcja struktury wdrażania chmury przeprowadza czytelnika przez różne metody przejścia na zarządzanie operacyjne w chmurze.

## <a name="actionable-best-practices"></a>Najlepsze rozwiązania dotyczące zasobów z możliwością działania

Nowoczesne rozwiązania do zarządzania operacjami tworzą wielochmurowy widok operacji. Zasoby zarządzane przez następujące najlepsze rozwiązania mogą być aktywne w chmurze, w istniejącym centrum danych, a nawet w konkurencyjnym dostawcy chmury. Obecnie struktura obejmuje dwa najlepsze rozwiązania referencyjne, które pomagają w dojrzały sposób zarządzać operacjami w chmurze:

- [Zarządzanie serwerem Azure](./azure-server-management/index.md): Przewodnik po płycie w celu uwzględnienia natywnych narzędzi i usług w chmurze wymaganych do zarządzania operacjami.
- [Monitorowanie hybrydowe](./monitor/index.md): wielu klientów wprowadziło już znaczną inwestycję w System Center Operations Manager. Przewodnik monitorowania hybrydowego ułatwia tym klientom porównanie i zestawienie narzędzi do raportowania natywnych dla chmury za pomocą narzędzi usługi Operations Manager. Ułatwi to wybór narzędzi do zarządzania operacyjnego.

## <a name="cloud-operations"></a>Operacje w chmurze

Oba te najlepsze rozwiązania zostały skompilowane w ramach przyszłej metodologii stanu zarządzania operacjami.

![Zarządzanie metodologią wdrożenia chmury](../_images/manage/caf-manage.png)

**Wyrównanie biznesowe:** W metodzie zarządzania wszystkie obciążenia są klasyfikowane według stopnia ważności i wartości biznesowej. Tę klasyfikację można zmierzyć w ramach analizy wpływu, która polega na obliczeniu utraconej wartości związanej z obniżeniem wydajności lub przerwami w działalności. Dzięki tym wymiernym danym wpływu na przychody zespoły ds. operacji w chmurze mogą wspólnie z firmą może ustalić zobowiązanie, które równoważy koszty i wydajność.

**Dyscypliny operacji w chmurze:** Po wyrównaniu firmy jest znacznie łatwiejsze śledzenie i raportowanie właściwych dyscyplin operacji w chmurze dla każdego obciążenia. Podejmowanie decyzji w każdej dyscyplinie można przełożyć na okresy zobowiązania, które są łatwo zrozumiałe dla firmy. Dzięki rozwiązaniu opartemu na współpracy biorący udział w projekcie stają się partnerami w znajdowaniu równowagi między kosztami i wydajnością.

- **Spis i widoczność:** Program Operations Management wymaga co najmniej środków tworzenia spisu zasobów i zapewnienia widoczności w stanie uruchomienia każdego elementu zawartości.
- **Zgodność operacyjna:** Regularne zarządzanie konfiguracją, rozmiarem, kosztem i wydajnością zasobów jest kluczem do obsługi oczekiwań wydajności.
- **Ochrona i odzyskiwanie:** Minimalizacja przerw w działaniu i przyspieszanie odzyskiwania pozwala uniknąć strat wydajności i przychodów. Kluczowymi aspektami tej dyscypliny są wykrywanie i odzyskiwanie.
- **Operacje na platformie:** Wszystkie środowiska IT zawierają zestaw często używanych platform. Te platformy mogą obejmować magazyny danych, takie jak SQL Server lub HDInsight. Inne popularne platformy mogą obejmować takie rozwiązania kontenerów jak Kubernetes lub AKS. Niezależnie od platform dojrzałość operacji platformy polega na dostosowywaniu operacji zgodnie ze sposobem wdrożenia i konfiguracji tych popularnych platform oraz ich użycia przez obciążenia.
- **Operacje związane z obciążeniem:** W przypadku najwyższego poziomu zapadalności operacyjnego zespoły operacji w chmurze mogą dostosowywać operacje dotyczące obciążeń, które są kluczowe dla sukcesu firmy. W przypadku tych obciążeń o wysokim znaczeniu dostępne dane mogą pomóc w automatyzacji korygowania, rozmiaru lub ochrony obciążeń na podstawie ich użycia.

Dodatkowe wskazówki, takie jak [Struktura przeglądu projektu (o nazwie kodowej: zasady projektowania w chmurze)](https://docs.microsoft.com/azure/architecture/reliability) , mogą pomóc w podejmowaniu szczegółowych decyzji dotyczących architektury dotyczących poszczególnych obciążeń w ramach powyższych dyscyplin.

Ta sekcja podręcznika Cloud Adoption Framework korzysta z informacji zawartych w każdym z tych tematów, aby zwiększyć dojrzałość operacji w chmurze w Twojej organizacji.
