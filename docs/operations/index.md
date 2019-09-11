---
title: Wprowadzenie do zarządzania operacyjnego
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Omówienie zarządzania operacyjnego w strukturze wdrażania chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: ed8afc403f217475cb69d4f0bf6742fe64443ae3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818441"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Tworzenie działań związanych z zarządzaniem operacyjnym w chmurze

Wdrożenie chmury pozwala szybciej zwiększyć wartość biznesową. Jednak rzeczywista wartość biznesowa jest uzyskiwana za pośrednictwem ciągłych, stabilnych operacji dotyczących zasobów technologicznych wdrożonych w chmurze. Ta sekcja struktury wdrażania chmury przeprowadza czytelnika przez różne metody przejścia na zarządzanie operacyjne w chmurze.

## <a name="actionable-best-practices"></a>Najlepsze rozwiązania dotyczące zasobów z możliwością działania

Współczesne rozwiązania do zarządzania operacyjnego zapewniają wgląd w operacje w wielu chmurach. Zasoby zarządzane za pomocą poniższych najlepszych rozwiązań mogą być przechowywane w chmurze, istniejącym centrum danych lub nawet u konkurencyjnego dostawcy usług w chmurze. Obecnie struktura obejmuje dwa najlepsze rozwiązania referencyjne, które pomagają w dojrzały sposób zarządzać operacjami w chmurze:

* [Zarządzanie serwerem na platformie Azure](./azure-server-management/index.md): przewodnik z wprowadzeniem do narzędzi i usług natywnych dla chmury potrzebnych do zarządzania operacjami.
* [Monitorowanie hybrydowe](./monitor/index.md): wielu klientów już dokonało znaczących inwestycji w usługę System Center Operations Manager. Przewodnik monitorowania hybrydowego ułatwia tym klientom porównanie i zestawienie narzędzi do raportowania natywnych dla chmury za pomocą narzędzi usługi Operations Manager. Ułatwi to wybór narzędzi do zarządzania operacyjnego.

## <a name="cloud-operations"></a>Operacje w chmurze

Oba te najlepsze rozwiązania mają na celu opracowanie metodologii zarządzania operacjami na przyszłość.

![Metodologia zarządzania strukturą CAF](../_images/operate/caf-manage.png)

**Dopasowanie działalności:** W metodologii zarządzania wszystkie obciążenia są klasyfikowane według krytyczności i wartości biznesowej. Tę klasyfikację można zmierzyć w ramach analizy wpływu, która polega na obliczeniu utraconej wartości związanej z obniżeniem wydajności lub przerwami w działalności. Dzięki tym wymiernym danym wpływu na przychody zespoły ds. operacji w chmurze mogą wspólnie z firmą może ustalić zobowiązanie, które równoważy koszty i wydajność.

**Dyscypliny operacji w chmurze:** Dopasowanie firmy znacząco ułatwia śledzenie i raportowanie odpowiednich dyscyplin operacji w chmurze dla poszczególnych obciążeń. Podejmowanie decyzji w każdej dyscyplinie można przełożyć na okresy zobowiązania, które są łatwo zrozumiałe dla firmy. Dzięki rozwiązaniu opartemu na współpracy biorący udział w projekcie stają się partnerami w znajdowaniu równowagi między kosztami i wydajnością.

* Spis i widoczność: Zarządzanie operacjami wymaga rozwiązania do tworzenia spisu zasobów i zapewniania wglądu w stan uruchomienia każdego zasobu.
* Zgodność operacyjna: Regularne zarządzanie konfiguracją, rozmiarami, kosztami i wydajnością zasobów ma kluczowe znaczenie dla spełnienia oczekiwań dotyczących wydajności.
* Ochrona i odzyskiwanie: Minimalizowanie przerw w operacjach i szybsze odzyskiwanie pomagają uniknąć spadku wydajności i przychodów. Kluczowymi aspektami tej dyscypliny są wykrywanie i odzyskiwanie.
* Operacje platformy: Wszystkie środowiska IT zawierają zestaw powszechnie stosowanych platform. Te platformy mogą obejmować magazyny danych, takie jak SQL Server lub HDInsight. Inne popularne platformy mogą obejmować takie rozwiązania kontenerów jak Kubernetes lub AKS. Niezależnie od platform dojrzałość operacji platformy polega na dostosowywaniu operacji zgodnie ze sposobem wdrożenia i konfiguracji tych popularnych platform oraz ich użycia przez obciążenia.
* Operacje obciążeń: Na najwyższym poziomie dojrzałości operacyjnej zespoły operacji w chmurze mogą dostosowywać operacje pod kątem obciążeń, które mają zasadnicze znaczenie dla sukcesu firmy. W przypadku tych obciążeń o wysokim znaczeniu dostępne dane mogą pomóc w automatyzacji korygowania, rozmiaru lub ochrony obciążeń na podstawie ich użycia.

Dodatkowe wskazówki, takie jak [Projektowanie platformy przeglądu (nazwa kodowa: zasady projektowania w chmurze)](/azure/architecture/reliability), mogą pomóc w podejmowaniu szczegółowych decyzji dotyczących architektury dla poszczególnych obciążeń w ramach powyższych dyscyplin.

Ta sekcja struktury wdrażania chmury korzysta z informacji zawartych w każdym z tych tematów, aby zwiększyć dojrzałość operacji w chmurze w Twojej organizacji.
