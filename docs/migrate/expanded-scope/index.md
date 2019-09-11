---
title: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 125c6d044fd766896971aced5bedbc515c14417f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817336"
---
# <a name="expanded-scope-for-cloud-migration"></a>Zakres rozszerzony dla migracji do chmury

[Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md) dostępny w przewodniku Cloud Adoption Framework jest sugerowanym punktem początkowym dla czytelników, którzy są zainteresowani migracją z ponownym hostowaniem na platformę Azure (nazywaną także migracją metodą „lift and shift”). Ten przewodnik przeprowadzi Cię przez szereg wymagań wstępnych, narzędzi oraz podejść związanych z migrowaniem maszyn wirtualnych do chmury.

Stanowi on dobrą podstawę umożliwiającą zapoznanie się z tym typem migracji, jednak wprowadza kilka założeń. Te założenia są zgodne z oczekiwaniami dużej części czytelników przewodnika Cloud Adoption Framework, ponieważ oferują uproszczone podejście do migracji. Niniejsza sekcja przewodnika Cloud Adoption Framework odnosi się do pewnych scenariuszy migracji o rozszerzonym zakresie i pomaga zaplanować prace, kiedy te założenia nie mają zastosowania.

## <a name="cloud-migration-expanded-scope-checklist"></a>Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury

Poniższa lista kontrolna zawiera typowe obszary złożoności, które mogą wymagać rozszerzenia zakresu migracji poza [Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md).

- **Zmiany zakresu związane z działalnością biznesową:**
  - [Równoważenie portfela](./balance-the-portfolio.md)
  - [Obsługa rynków globalnych](./multiple-regions.md)
  - Świadomość kosztów podczas migracji *(dostępne w 3 kwartale 2019 r.)*
- **Zmiany zakresu związane z kulturą:**
  - Zarządzanie zmianami i procesy zatwierdzania *(dostępne w 3 kwartale 2019 r.)*
  - Gotowość kadry zarządzającej *(dostępne w 3 kwartale 2019 r.)*
  - [Gotowość w zakresie umiejętności](./suggested-skills.md)
  - Dostosowywanie pomocy technicznej (partnerstwo, usługi i wsparcie) *(dostępne w 3 kwartale 2019 r.)*
- **Zmiany zakresu związane ze strategią techniczną:**
  - Istniejące ograniczenia dotyczące centrum danych *(dostępne w 3 kwartale 2019 r.)*
  - Migrowanie na dużą skalę — migracje o dużej pojemności lub szybkości *(dostępne w 3 kwartale 2019 r.)*
  - [Wiele centrów danych](./multiple-datacenters.md)
  - [Wymagania dotyczące danych przekraczają pojemność sieci](./network-capacity-exceeded.md)
  - Dokumentacja dotycząca rozwiązań i zarządzania zmianami *(dostępne w 3 kwartale 2019 r.)*
  - [Strategia utrzymania ładu i zgodności](./governance-or-compliance.md)
- **Zmiany zakresu związane z obciążeniami:**
  - Tworzenie architektury obciążeń pod kątem odporności *(dostępne w 3 kwartale 2019 r.)*
  - Dostosowanie migracji do wzorców aplikacji *(dostępne w 3 kwartale 2019 r.)*

Jeśli którykolwiek z tych obszarów złożoności pokrywa się z Twoim scenariuszem, ta sekcja przewodnika Cloud Adoption Framework prawdopodobnie będzie zawierać wskazówki, które pomogą Ci prawidłowo dostosować zakres w procesie migracji.

Każdy z tych scenariuszy został opisany w różnych artykułach w tej sekcji przewodnika Cloud Adoption Framework.

## <a name="scope-options-explained"></a>Objaśnienie opcji zakresu

Aby ułatwić zrozumienie każdego scenariusza rozszerzania zakresu, na poniższej liście krótko podsumowano tytuły użyte na powyższej liście kontrolnej.

### <a name="business-driven-scope-changes"></a>Zmiany zakresu związane z działalnością biznesową

- **Równoważenie portfela wdrażania chmury:** Zespół ds. strategii chmury chce więcej zainwestować w migrację (ponowny hosting istniejących obciążeń i aplikacji przy minimalnych modyfikacjach) lub innowacje (refaktoryzacja lub ponowne tworzenie tych obciążeń i aplikacji przy użyciu nowoczesnej technologii chmurowej). Często równowaga między tymi dwoma priorytetami jest kluczem do sukcesu. W tym przewodniku temat równoważenia portfela wdrożenia chmury jest popularny i został omówiony na każdym etapie procesu migracji.
- **Obsługa rynków globalnych:** Firma działa w wielu regionach geograficznych z różnymi wymaganiami dotyczącymi niezależności danych. Aby spełnić te wymagania, należy uwzględnić dodatkowe kwestie podczas przeglądu wymagań wstępnych i dystrybucji zasobów w trakcie migracji.

### <a name="culture-driven-scope-changes"></a>Zmiany zakresu związane z kulturą

- **Zarządzanie zmianami i procesy zatwierdzania:** Kiedy kultura Twojej organizacji jest złożona, wysoce matrycowa lub rozdzielona, procesy związane z zarządzaniem zmianami i zatwierdzeniami stają się trudne. Wskazówki dotyczące zarządzania tymi złożonościami można znaleźć w opisach procesów oceniania, migracji i optymalizacji.
- **Gotowość kadry zarządzającej:** Odpowiedni poziom wsparcia kadry zarządzającej i kierownictwa ma kluczowe znaczenie dla powodzenia prac związanych z migracją. Jeśli zespół kadry zarządzającej nie chce się zaangażować, raczej nie wesprze wysiłków pracowników. Tę złożoność opisano w procesach dotyczących wymagań wstępnych i oceny.
- **Gotowość w zakresie umiejętności:** Jeśli zespół wdrażania chmury lub inne zespoły pomocnicze nie są gotowe do wykonania, może to szybko skomplikować wszystkie etapy procesu migracji. Ten problem został omówiony dla każdego procesu migracji na specjalnej stronie poświęconej gotowości w zakresie umiejętności.
- **Dostosowywanie pomocy technicznej (partnerstwo, usługi i opcje wsparcia):** W realizacji każdego z przedstawionych procesów mogą pomóc partnerzy, usługi i wsparcie od dostawcy chmury. Każda sekcja procesu zawiera stronę z dalszym opisem opcji dostosowania pomocy technicznej.

### <a name="technical-strategy-driven-scope-changes"></a>Zmiany zakresu związane ze strategią techniczną

- **Istniejące ograniczenia dotyczące centrum danych:** Firmy często decydują się na migrację do chmury, ponieważ pojemność, szybkość i stabilność istniejącego centrum danych nie jest już zadowalająca. Niestety te same ograniczenia zwiększają złożoność procesu migracji, co wymaga dodatkowego planowania w procesach oceny i migracji.
- **Migracja w dużej skali:** Migracje obejmujące więcej niż 2000 zasobów prawdopodobnie spotkają się z ograniczeniami, które wymagają dodatkowego planowania i zdyscyplinowanego podejścia do wykonania. Procesy oceny i migracji zostały dostosowane w celu uwzględnienia złożoności skali.
- **Wiele centrów danych:** Migracja wielu centrów danych zdecydowanie zwiększa złożoność. Podczas procesów oceny, migracji, optymalizacji i zarządzania omówiono te dodatkowe zagadnienia.
- **Dokumentacja dotycząca rozwiązań i zarządzania zmianami:** Duże spisy majątku cyfrowego, skomplikowane architektury rozwiązań, długotrwały dług techniczny oraz współzależności mogą przyczynić się do złożoności, którymi należy się zająć podczas procesów oceny, migracji i optymalizacji.
- **Strategia utrzymania ładu i zgodności:** Jeśli ład i zgodność są ważne z punktu widzenia powodzenia migracji, wymagana jest dodatkowa współpraca między zespołem ds. ładu w zasobach IT i zespołem ds. wdrożenia chmury.

### <a name="workload-specific-scope-changes"></a>Zmiany zakresu związane z obciążeniami

- **Tworzenie architektury obciążeń pod kątem odporności:** Wspólne zasady projektowania w chmurze mogą pomóc przygotować obciążenia o krytycznym znaczeniu do zwiększenia odporności. Ten artykuł wyjaśnia, jaki wpływ na proces migracji ma wymaganie dotyczące odporności obciążenia. Udostępnia on także kilka typowych zasad, które warto uwzględnić w ogólnej konfiguracji środowiska, aby poprawić jego odporność.
- **Dostosowanie migracji do wzorców aplikacji:** Wzorzec migracji obciążenia może mieć wpływ na wybraną ścieżkę migracji. W tym artykule opisano kilka zmian zakresu, które można zintegrować z poziomem elementu roboczego listy prac związanych z migracją, aby odzwierciedlić różne podejścia do migracji poszczególnych obciążeń.

## <a name="next-steps"></a>Następne kroki

Przejrzyj spis treści po lewej stronie, aby znaleźć tematy dotyczące określonych potrzeb lub zmian zakresu. Alternatywnie przeglądanie tych scenariuszy można zacząć od pierwszego rozszerzenia zakresu na liście dotyczącego [równoważenia portfela](./balance-the-portfolio.md).

> [!div class="nextstepaction"]
> [Równoważenie portfela](./balance-the-portfolio.md)
