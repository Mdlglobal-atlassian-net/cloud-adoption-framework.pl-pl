---
title: Spis i widoczność — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Spis i widoczność — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: fe46ec035bb732ec82931358c7e79b41b4f18bd5
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558066"
---
# <a name="inventory-and-visibility-in-cloud-management"></a>Spis i widoczność w zarządzaniu chmurą

Zarządzanie operacyjną ma jasno zależność od danych. Spójne zarządzanie wymaga jasnego poznania informacji o tym, co jest zarządzane (spisu) i jak te zarządzane obciążenia i zasoby zmieniają się z upływem czasu (widoczność). Jednocześnie przejrzystość spisu i widoczność pozwala zespołowi na efektywne zarządzanie środowiskiem. Wszystkie inne działania i procesy zarządzania operacyjnego kompilują się w tych dwóch obszarach szczegółowych informacji.

Kilka klasycznych fraz dotyczących ważnych pomiarów ustawia ton dla tego artykułu: Zarządzaj zagadnieniami. Możesz zarządzać tylko możliwościami, które można zmierzyć. Jeśli nie możesz go zmierzyć, może nie mieć znaczenia. Dyscyplina spisu i widoczności kompiluje na te ponadczasowegoe frazy. Przed ustanowieniem procesów zarządzania operacyjnego należy zebrać dane i stworzyć właściwy poziom widoczności dla właściwych zespołów.

## <a name="common-customer-challenges"></a>Typowe wyzwania dla klientów

Gdy procesy spisu i widoczności nie są stale stosowane, zespoły zarządzania operacyjnego poniosły wyższą liczbę przerw w działalności biznesowej, dłuższy czas do odzyskania i więcej nakładów pracy wymaganych do rozwiązywania problemów i klasyfikacja. Ponieważ zmiany wpływają na aplikacje o wyższym priorytecie i większą liczbę elementów zawartości, każda z tych metryk rośnie jeszcze szybciej.

Te wyzwania wynikają z niewielkiej liczby pytań, na które można odpowiedzieć tylko za pośrednictwem spójnych danych/telemetrii:

- Jak działa różnica w bieżącym stanie od standardowej telemetrii wydajności operacyjnej?
- Jakie zasoby powodują zakłócenia biznesowe na poziomie obciążenia?
- Jakie zasoby należy skorygować, aby przywrócić akceptowalną wydajność tego obciążenia/procesu biznesowego?
- Kiedy ma zostać rozpoczęte odróżnienie? Co to jest wyzwalacz?
- Które zmiany zostały wprowadzone w podstawowych zasobach? Przez kogo?
- Czy zmiany zostały zamierzone? Niepożądanych?
- Jak zmieniły się dane telemetryczne wydajności.

Trudno, jeśli nie można odpowiedzieć na te pytania bez zaawansowanego, scentralizowanego źródła danych dzienników i telemetrii. Aby włączyć zarządzanie chmurą, usługa bazowa musi najpierw zacząć od definicji procesów, aby zapewnić spójną konfigurację wymaganą do scentralizowania danych. Procesy te powinny przechwycić, w jaki sposób konfiguracja będzie wymuszać zbieranie danych w celu obsługi składników spisu i widoczności w następnej sekcji.

## <a name="components-of-inventory-and-visibility"></a>Składniki spisu i widoczności

Tworzenie widoczności na dowolnej platformie w chmurze wymaga kilku najważniejszych składników:

1. Odpowiedzialność i widoczność
2. Spis
3. Rejestrowanie centralne
4. Śledzenie zmian
5. Telemetria wydajności

### <a name="responsibility-and-visibility"></a>Odpowiedzialność i widoczność

Podczas ustanawiania zobowiązań dla każdego obciążenia, [odpowiedzialność za zarządzanie](./commitment.md#management-responsibility) jest kluczowym czynnikiem. Delegowana odpowiedzialność tworzy potrzebę delegowania widoczności. Pierwszym krokiem w kierunku spisu i widoczności jest upewnienie się, że osoby odpowiedzialne mają dostęp do odpowiednich danych. Przed zaimplementowaniem wszelkich natywnych narzędzi w chmurze w celu zapewnienia widoczności upewnij się, że każde narzędzie monitorowania zostało skonfigurowane z odpowiednim dostępem i zakresem dla każdego zespołu operacji.

### <a name="inventory"></a>Spis

Jeśli nikt nie wie, że zasób istnieje, trudno jest zarządzać zasobami. Aby można było zarządzać zasobem lub obciążeniem, musi on być uwzględniony w spisie i sklasyfikowany. Pierwszym krokiem technicznym w kierunku stabilnych operacji jest weryfikacja spisu i Klasyfikacja tego spisu.

### <a name="central-logging"></a>Rejestrowanie centralne

Scentralizowane rejestrowanie ma krytyczne znaczenie dla potrzebnych zespołów zarządzania operacjami. Wszystkie zasoby wdrożone w chmurze powinny rejestrować dzienniki w centralnej lokalizacji. Na platformie Azure Centralna lokalizacja to usługa log Analytics. Scentralizowane zarządzanie dyskami rejestrowania dotyczy zarządzania zmianami, kondycji usług, konfiguracji i większości innych aspektów operacji IT.

Wymuszanie spójnego korzystania z centralnego rejestrowania to pierwszy krok w kierunku spójnych operacji powtarzalnych. Wymuszanie można wykonać przy użyciu zasad firmowych. Jednak jeśli możliwe jest wymuszenie, należy zautomatyzować, aby zapewnić spójność.

### <a name="change-tracking"></a>Śledzenie zmian

Zmiana to jedna stała w środowisku technologicznym. Świadomość i zrozumienie zmian w wielu obciążeniach jest istotne dla niezawodnych operacji. Każde rozwiązanie do zarządzania chmurą powinno uwzględniać sposób, w jaki można zrozumieć, jak i dlaczego zmiany techniczne. Bez tych punktów danych działania naprawcze są znacząco utrudnione.

### <a name="performance-telemetry"></a>Telemetria wydajności

Zobowiązania biznesowe dotyczące zarządzania chmurą są określane przez dane. Aby prawidłowo zachować zobowiązania, zespół operacyjny w chmurze musi najpierw zrozumieć dane telemetryczne dotyczące stabilności, wydajności i operacji obciążenia oraz zasobów, które obsługują obciążenie.

Bieżące kondycje i działania sieci, systemu DNS, systemów operacyjnych i innych podstawowych aspektów środowiska są kluczowymi punktami danych, które są używane do ogólnej kondycji wszelkich obciążeń.

## <a name="processes"></a>Procesy

Być może ważniejsze niż funkcje platformy zarządzania chmurą, procesy zarządzania chmurą będą realizować zobowiązania dotyczące operacji w firmie. Każda metodologia zarządzania chmurą powinna obejmować co najmniej następujące procesy:

- Monitorowanie reaktywne: gdy odchylenia mają wpływ na operacje biznesowe, które odnoszą się do tych odchyleń? Jakie działania podejmują w celu skorygowania odchyleń.
- Proaktywne monitorowanie: w przypadku wykrycia odchyleń, ale nie ma to wpływ na działalność biznesową, w jaki sposób te odchylenia są kierowane i przez kogo?
- Raportowanie zobowiązań: w jaki sposób nastąpi przystąpienie do działalności przekazanej uczestnikom zainteresowanych firm?
- Przeglądy budżetowe: Jakie są procesy przeglądania tych zobowiązań względem kosztów budżetowych? Jaki jest proces dostosowywania wdrożonego rozwiązania lub zobowiązań w celu utworzenia wyrównania?
- Ścieżki eskalacji: jakie ścieżki eskalacji są dostępne, gdy którykolwiek z powyższych procesów nie spełnia wymagań firmy?

Istnieje kilka więcej procesów związanych ze spisem i widocznością. Powyższa lista została zaprojektowana z myślą o rozproszeniu do zespołu operacji. Udzielenie odpowiedzi na te pytania spowoduje opracowanie niektórych niezbędnych procesów. Prawdopodobnie spowoduje to również wyzwolenie nowych bardziej szczegółowych pytań.

## <a name="responsibilities"></a>Zakres odpowiedzialności

Podczas opracowywania procesów monitorowania operacyjnego równie ważne jest określenie obowiązków związanych z codziennym działaniem i regularnym wsparciem poszczególnych procesów.

W centralnej organizacji INFORMATYCZNej zapewnimy wiedzę operacyjną. W przypadku problemów z korygowaniemem działalność biznesowa mogłaby mieć charakter doradczy.
W centrum usługi w chmurze w organizacji doskonałości działalność biznesowa zapewni wiedzę i odpowiedzialność za zarządzanie tymi procesami. Może skupić się na automatyzacji i obsłudze zespołów, gdy działają one w środowisku.

Jednak są to typowe obowiązki. Organizacje często wymagają kombinacji obowiązków, aby spełnić zobowiązania biznesowe.

## <a name="acting-on-inventory-and-visibility"></a>Działania dotyczące spisu i widoczności

Bez względu na platformę chmury pięć składników spisu i widoczności są używane do obsługi większości procesów operacyjnych. Wszystkie kolejne dyscypliny będą kompilować na przechwytywaniu danych. Poniższe artykuły w tej serii zawierają opis sposobów działania tych danych i integracji innych źródeł danych.

### <a name="sharing-visibility"></a>Widoczność udostępniania

Dane bez akcji generują niewielki zwrot. Zarządzanie chmurą może wzwiększyć poza natywne narzędzia i procesy w chmurze. Aby obsłużyć szersze procesy, może być konieczne zwiększenie poziomu linii bazowej zarządzania chmurą w celu uwzględnienia raportów, integracji zarządzania usługami IT lub scentralizowania danych. W przypadku różnych faz działania w ramach usługi Cloud Management może być konieczne uwzględnienie co najmniej jednego z następujących elementów.

### <a name="reporting"></a>Raportowanie

Procesy w trybie offline i komunikacja dotyczące zobowiązań do uczestników współpracy często wymagają raportowania. Raportowanie samoobsługowe lub raportowanie okresowe może być składnikiem niezbędnym do rozbudowanego planu bazowego zarządzania.

### <a name="it-service-management-itsm-integration"></a>Integracja z zarządzaniem usługami IT (narzędzia ITSM)

Integracja narzędzia ITSM jest często pierwszym przykładem działania w zakresie spisu i widoczności. Gdy powstają odchylenia od oczekiwanych wzorców wydajności, integracja narzędzia ITSM będzie używać alertów z poziomu platformy w chmurze do wyzwalania biletów w osobnym narzędziu do zarządzania usługami, aby wyzwolić działania naprawcze. Niektóre modele operacyjne mogą wymagać integracji narzędzia ITSM jako aspektu rozbudowanego planu bazowego zarządzania.

### <a name="data-centralization"></a>Scentralizowanie danych

Istnieje wiele powodów, dla których firma może wymagać wielu dzierżawców w ramach jednego dostawcy chmury. W tych scenariuszach scentralizowane zarządzanie danymi jest wymaganym składnikiem rozszerzonej linii bazowej zarządzania w celu zapewnienia widoczności w poszczególnych dzierżawcach lub środowiskach.

## <a name="next-steps"></a>Następne kroki

Zgodność operacyjna kompiluje możliwości spisu przez zastosowanie automatyzacji zarządzania i kontrolek. Zobacz, jak [zgodność operacyjna](./operational-compliance.md) jest mapowana na procesy.

> [!div class="nextstepaction"]
> [Planowanie zgodności operacyjnej](./operational-compliance.md)
