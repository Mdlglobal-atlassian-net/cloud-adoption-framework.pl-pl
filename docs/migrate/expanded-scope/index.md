---
title: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ee164f75b4f3748fce027d0c6c98db5200dcdd71
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548506"
---
# <a name="expanded-scope-for-cloud-migration"></a>Zakres rozszerzony dla migracji do chmury

[Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md) dostępny w przewodniku Cloud Adoption Framework jest sugerowanym punktem początkowym dla czytelników, którzy są zainteresowani migracją z ponownym hostowaniem na platformę Azure (nazywaną także migracją metodą „lift and shift”). Ten przewodnik przeprowadzi Cię przez szereg wymagań wstępnych, narzędzi oraz podejść związanych z migrowaniem maszyn wirtualnych do chmury.

Stanowi on dobrą podstawę umożliwiającą zapoznanie się z tym typem migracji, jednak wprowadza kilka założeń. Te założenia są zgodne z oczekiwaniami wielu czytelników przewodnika Cloud Adoption Framework, ponieważ oferują uproszczone podejście do migracji. Niniejsza sekcja przewodnika Cloud Adoption Framework odnosi się do pewnych scenariuszy migracji o rozszerzonym zakresie i pomaga zaplanować prace, kiedy te założenia nie mają zastosowania.

## <a name="cloud-migration-expanded-scope-checklist"></a>Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury

Poniższa lista kontrolna zawiera typowe obszary złożoności, które mogą wymagać rozszerzenia zakresu migracji poza [Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>Aspekty biznesowe rozszerzenia zakresu

- **[Równoważenie portfela](./balance-the-portfolio.md):** Zespół ds. strategii chmury chce więcej zainwestować w migrację (ponowny hosting istniejących obciążeń i aplikacji przy minimalnych modyfikacjach) lub innowacje (refaktoryzacja lub ponowne tworzenie tych obciążeń i aplikacji przy użyciu nowoczesnej technologii chmurowej). Często równowaga między tymi dwoma priorytetami jest kluczem do sukcesu. W tym przewodniku temat równoważenia portfela wdrożenia chmury jest popularny i został omówiony na każdym etapie procesu migracji.
- **[Obsługa rynków globalnych](../../decision-guides/regions/index.md):** Firma działa w wielu regionach geograficznych z różnymi wymaganiami dotyczącymi niezależności danych. Aby spełnić te wymagania, należy uwzględnić dodatkowe kwestie podczas przeglądu wymagań wstępnych i dystrybucji zasobów w trakcie migracji.

### <a name="technology-driven-scope-expansion"></a>Aspekty technologiczne rozszerzenia zakresu

- **[Migracja hostów VMWare](./vmware-host.md):** Migracja hostów VMWare może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym hostem VMWare można przenieść wiele obciążeń do chmury metodą „lift and shift”. Po migracji te maszyny wirtualne i obciążenia mogą pozostać w programie VMWare lub zostać przeniesione do nowoczesnych rozwiązań chmurowych.
- **[Migracja serwerów SQL](./sql-migration.md):** Migracja serwerów SQL może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym serwerem SQL można przenieść wiele baz danych i usług, potencjalnie przyspieszając wiele obciążeń.
- **[Wiele centrów danych](./multiple-datacenters.md):** Migracja wielu centrów danych zdecydowanie zwiększa złożoność. Podczas procesów oceny, migracji, optymalizacji i zarządzania omówiono dodatkowe zagadnienia związane z przygotowaniem bardziej złożonych środowisk.
- **[Wymagania dotyczące danych przekraczają pojemność sieci](./network-capacity-exceeded.md):** Firmy często decydują się na migrację do chmury, ponieważ pojemność, szybkość lub stabilność istniejącego centrum danych nie jest już zadowalająca. Niestety te same ograniczenia zwiększają złożoność procesu migracji, co wymaga dodatkowego planowania w procesach oceny i migracji.
- **[Strategia utrzymania ładu lub zgodności](./governance-or-compliance.md):** Jeśli ład i zgodność są ważne z punktu widzenia powodzenia migracji, wymagana jest dodatkowa współpraca między zespołem ds. ładu w zasobach IT i zespołem ds. wdrożenia chmury.

Jeśli którykolwiek z tych obszarów złożoności występuje w Twoim scenariuszu, ta sekcja przewodnika Cloud Adoption Framework prawdopodobnie będzie zawierać wskazówki, które pomogą Ci prawidłowo dostosować zakres w procesie migracji.

Każdy z tych scenariuszy został opisany w różnych artykułach w tej sekcji przewodnika Cloud Adoption Framework.

## <a name="next-steps"></a>Następne kroki

Przejrzyj spis treści po lewej stronie, aby znaleźć tematy dotyczące określonych potrzeb lub zmian zakresu. Przeglądanie tych scenariuszy można też zacząć od pierwszego rozszerzenia zakresu na liście, dotyczącego [równoważenia portfela](./balance-the-portfolio.md).

> [!div class="nextstepaction"]
> [Równoważenie portfela](./balance-the-portfolio.md)
