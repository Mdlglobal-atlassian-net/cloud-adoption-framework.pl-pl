---
title: Spis i widoczność na platformie Azure
description: Informacje o tym, co należy zarządzać (spisem) oraz jak te zarządzane obciążenia i zasoby zmieniają się z upływem czasu (widoczność).
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b3c963341e7e13020cb4e67fca29db14569fa6b3
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223953"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Spis i widoczność w zarządzaniu chmurą

Zarządzanie operacyjną ma jasno zależność od danych. Spójne zarządzanie wymaga informacji o tym, co jest zarządzane (spisu) oraz o tym, jak te zarządzane obciążenia i zasoby zmieniają się z upływem czasu (widoczność). Wyczyść szczegółowe informacje o zapasach i widoczności ułatwiają zespołowi skuteczne zarządzanie środowiskiem. Wszystkie inne działania i procesy zarządzania operacyjnego są kompilowane w tych dwóch obszarach.

Kilka klasycznych fraz dotyczących znaczenia miar ustawia ton dla tego artykułu:

- Zarządzaj tym zagadnieniami.
- Możesz zarządzać tylko możliwościami, które można zmierzyć.
- Jeśli nie możesz go zmierzyć, może nie mieć znaczenia.

Dyscyplina spisu i widoczności kompiluje na te ponadczasowegoe frazy. Przed efektywnym ustanowieniem procesów zarządzania operacyjnego należy zebrać dane i stworzyć właściwy poziom widoczności dla właściwych zespołów.

## <a name="common-customer-challenges"></a>Typowe wyzwania dla klientów

Jeśli procesy spisu i widoczności są stale stosowane, zespoły zarządzania operacyjnego mogą pogorszyć się od większej liczby przerw w działalności biznesowej, dłuższego czasu na odzyskiwanie i większych nakładów pracy wymaganych do rozwiązywania problemów i klasyfikacja. Ponieważ zmiany mają niekorzystny wpływ na aplikacje o wyższym priorytecie i większą liczbę zasobów, każda z tych metryk rośnie jeszcze szybciej.

Te wyzwania wynikają z niewielkiej liczby pytań, na które można odpowiedzieć tylko za pośrednictwem spójnych danych/telemetrii:

- Jak działa różnica w bieżącym stanie od standardowej telemetrii wydajności operacyjnej?
- Jakie zasoby powodują zakłócenia biznesowe na poziomie obciążenia?
- Jakie zasoby należy skorygować, aby przywrócić akceptowalną wydajność tego obciążenia lub procesu biznesowego?
- Kiedy ma zostać rozpoczęte odróżnienie? Co to jest wyzwalacz?
- Które zmiany zostały wprowadzone w podstawowych zasobach? Przez kogo?
- Czy zmiany zostały zamierzone? Niepożądanych?
- Jak zmiany wpływają na dane telemetryczne wydajności?

Jeśli nie jest to możliwe, można odpowiedzieć na te pytania bez bogatego, scentralizowanego źródła danych dzienników i telemetrii. Aby włączyć zarządzanie chmurą przez zapewnienie spójnej konfiguracji wymaganej do scentralizowania danych, usługa bazowa musi najpierw zacząć od definiowania procesów. Procesy powinny przechwycić, jak taka konfiguracja wymusza zbieranie danych w celu obsługi składników spisu i widoczności w następnej sekcji.

## <a name="components-of-inventory-and-visibility"></a>Składniki spisu i widoczności

Tworzenie widoczności na dowolnej platformie w chmurze wymaga kilku najważniejszych składników:

- Odpowiedzialność i widoczność
- Spis
- Rejestrowanie centralne
- Śledzenie zmian
- Telemetria wydajności

### <a name="responsibility-and-visibility"></a>Odpowiedzialność i widoczność

Po ustanowieniu zobowiązań dla każdego obciążenia, [odpowiedzialność za zarządzanie](./commitment.md#management-responsibility) jest kluczowym czynnikiem. Delegowana odpowiedzialność tworzy potrzebę delegowania widoczności. Pierwszym krokiem w kierunku spisu i widoczności jest upewnienie się, że osoby odpowiedzialne mają dostęp do odpowiednich danych. Przed zaimplementowaniem dowolnych natywnych narzędzi w chmurze w celu zapewnienia widoczności upewnij się, że każde narzędzie monitorowania zostało skonfigurowane z odpowiednim dostępem i zakresem dla każdego zespołu operacji.

### <a name="inventory"></a>Spis

Jeśli nikt nie wie, że zasób istnieje, trudno jest zarządzać zasobami. Aby można było zarządzać zasobem lub obciążeniem, musi on być uwzględniony w spisie i sklasyfikowany. Pierwszym krokiem technicznym w kierunku stabilnych operacji jest weryfikacja spisu i Klasyfikacja tego spisu.

### <a name="central-logging"></a>Rejestrowanie centralne

Scentralizowane rejestrowanie ma kluczowe znaczenie dla widoczności, która jest wymagana dziennie przez zespoły zarządzania operacjami. Wszystkie zasoby wdrożone w chmurze powinny rejestrować dzienniki w centralnej lokalizacji. Na platformie Azure Centralna lokalizacja to usługa log Analytics. Scentralizowane zarządzanie dyskami rejestrowania raporty dotyczące zarządzania zmianami, kondycji usług, konfiguracji i większości innych aspektów operacji IT.

Wymuszanie spójnego korzystania z centralnego rejestrowania to pierwszy krok w kierunku ustanowienia powtarzalnych operacji. Wymuszanie można wykonać przy użyciu zasad firmowych. Jeśli jednak jest to możliwe, wymuszanie powinno być zautomatyzowane, aby zapewnić spójność.

### <a name="change-tracking"></a>Śledzenie zmian

Zmiana to jedna stała w środowisku technologicznym. Świadomość i zrozumienie zmian w wielu obciążeniach jest istotne dla niezawodnych operacji. Każde rozwiązanie do zarządzania chmurą powinno uwzględniać sposób, w jaki można zrozumieć, jak i dlaczego zmiany techniczne. Bez tych punktów danych działania naprawcze są znacząco utrudnione.

### <a name="performance-telemetry"></a>Telemetria wydajności

Zobowiązania biznesowe dotyczące zarządzania chmurą są określane przez dane. Aby prawidłowo zachować zobowiązania, zespół operacyjny w chmurze musi najpierw zrozumieć dane telemetryczne dotyczące stabilności, wydajności i operacji obciążenia oraz zasobów, które obsługują obciążenie.

Bieżące kondycje i działania sieci, systemu DNS, systemów operacyjnych i innych podstawowych aspektów środowiska są kluczowymi punktami danych, które są wskaźnikami do ogólnej kondycji dowolnego obciążenia.

## <a name="processes"></a>Procesy

Być może ważniejsze niż funkcje platformy zarządzania chmurą, procesy zarządzania chmurą będą realizować zobowiązania dotyczące operacji w firmie. Każda metodologia zarządzania chmurą powinna obejmować co najmniej następujące procesy:

- **Aktywne monitorowanie:** Gdy odchylenia mają negatywny wpływ na operacje biznesowe, które odnoszą się do tych odchyleń? Jakie działania podejmują w celu skorygowania odchyleń?
- **Proaktywne monitorowanie:** W przypadku wykrycia odchyleń, ale nie ma to wpływ na operacje biznesowe, w jaki sposób odnoszą się do nich, i przez kogo?
- **Raportowanie zobowiązań:** Jak nawiązać się z zobowiązaniami biznesowymi, które komunikują się z zainteresowanymi stronami biznesowymi?
- **Przeglądy budżetowe:** Jaki jest proces przeglądania tych zobowiązań względem kosztów budżetowych? Jaki jest proces dostosowywania wdrożonego rozwiązania lub zobowiązań w celu utworzenia wyrównania?
- **Ścieżki eskalacji:** Jakie ścieżki eskalacji są dostępne, gdy którykolwiek z powyższych procesów nie spełnia wymagań firmy?

Istnieje kilka innych procesów związanych ze spisem i widocznością. Poprzednia lista została zaprojektowana z myślą o rozdaniu myśli w zespole operacji. Udzielenie odpowiedzi na te pytania ułatwi opracowywanie niektórych niezbędnych procesów, a także prawdopodobnie wyzwala nowe, bardziej szczegółowe pytania.

## <a name="responsibilities"></a>Zakres odpowiedzialności

Gdy opracowujesz procesy do monitorowania operacyjnego, równie ważne jest określenie obowiązków związanych z codziennymi operacjami i regularnym wsparciem poszczególnych procesów.

W centralnej organizacji INFORMATYCZNej zapewnimy wiedzę operacyjną. W przypadku problemów wymagających korygowania firma będzie mieć charakter doradczy.

W centrum usługi w chmurze w organizacji doskonałości działalność biznesowa zapewni wiedzę i odpowiedzialność za zarządzanie tymi procesami. Może skupić się na automatyzacji i obsłudze zespołów, gdy działają one w środowisku.

Jednak są to typowe obowiązki. Organizacje często wymagają kombinacji obowiązków, aby spełnić zobowiązania biznesowe.

## <a name="act-on-inventory-and-visibility"></a>Działania dotyczące spisu i widoczności

Bez względu na platformę chmury pięć składników spisu i widoczności są używane do obsługi większości procesów operacyjnych. Wszystkie kolejne dyscypliny będą kompilować dane, które są przechwytywane. W następnych artykułach w tej serii opisano sposoby działania tych danych i integrowanie innych źródeł danych.

### <a name="share-visibility"></a>Widoczność udziału

Dane bez akcji generują niewielki zwrot. Zarządzanie chmurą może wzwiększyć poza natywne narzędzia i procesy w chmurze. Aby obsłużyć szersze procesy, może być konieczne zwiększenie poziomu linii bazowej zarządzania chmurą w celu uwzględnienia raportów, integracji zarządzania usługami IT lub scentralizowania danych. W przypadku różnych faz działania w ramach zarządzania chmurą może być konieczne uwzględnienie co najmniej jednego z następujących elementów.

### <a name="report"></a>Raport

Procesy w trybie offline i komunikacja dotyczące zobowiązań do uczestników współpracy często wymagają raportowania. Raportowanie samoobsługowe lub raportowanie okresowe może być składnikiem niezbędnym do rozbudowanego planu bazowego zarządzania.

### <a name="it-service-management-itsm-integration"></a>Integracja zarządzania usługami IT (ITSM)

Integracja narzędzia ITSM jest często pierwszym przykładem działania w zakresie spisu i widoczności. Gdy powstają odchylenia od oczekiwanych wzorców wydajności, integracja narzędzia ITSM używa alertów z platformy chmury, aby wyzwolić bilety w osobnym narzędziu do zarządzania usługami, aby wyzwolić działania naprawcze. Niektóre modele operacyjne mogą wymagać integracji narzędzia ITSM jako aspektu rozszerzonej linii bazowej zarządzania.

### <a name="data-centralization"></a>Scentralizowanie danych

Istnieje wiele powodów, dla których firma może wymagać wielu dzierżawców w ramach jednego dostawcy chmury. W tych scenariuszach scentralizowane zarządzanie danymi jest wymaganym składnikiem ulepszonej linii bazowej zarządzania, ponieważ może ona zapewnić widoczność w poszczególnych dzierżawcach lub środowiskach.

## <a name="next-steps"></a>Następne kroki

Zgodność operacyjna kompiluje możliwości spisu przez zastosowanie automatyzacji zarządzania i kontrolek. Zobacz, jak [zgodność operacyjna](./operational-compliance.md) jest mapowana na procesy.

> [!div class="nextstepaction"]
> [Planowanie zgodności operacyjnej](./operational-compliance.md)
