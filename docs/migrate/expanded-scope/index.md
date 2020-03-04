---
title: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
description: Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ba6c768f98e3b74b0478fef0a86e6d8ac5537f1c
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78222332"
---
# <a name="expanded-scope-for-cloud-migration"></a>Zakres rozszerzony dla migracji do chmury

[Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md) dostępny w przewodniku Cloud Adoption Framework jest sugerowanym punktem początkowym dla czytelników, którzy są zainteresowani migracją z ponownym hostowaniem na platformę Azure (nazywaną także migracją metodą „lift and shift”). Ten przewodnik przeprowadzi Cię przez szereg wymagań wstępnych, narzędzi oraz podejść związanych z migrowaniem maszyn wirtualnych do chmury.

Stanowi on dobrą podstawę umożliwiającą zapoznanie się z tym typem migracji, jednak wprowadza kilka założeń. Te założenia są zgodne z oczekiwaniami wielu czytelników przewodnika Cloud Adoption Framework, ponieważ oferują uproszczone podejście do migracji. Niniejsza sekcja przewodnika Cloud Adoption Framework odnosi się do pewnych scenariuszy migracji o rozszerzonym zakresie i pomaga zaplanować prace, kiedy te założenia nie mają zastosowania.

## <a name="cloud-migration-expanded-scope-checklist"></a>Lista kontrolna dotycząca zakresu rozszerzonego migracji do chmury

Poniższa lista kontrolna zawiera typowe obszary złożoności, które mogą wymagać rozszerzenia zakresu migracji poza [Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>Aspekty biznesowe rozszerzenia zakresu

- **[Obsługa rynków globalnych](../../decision-guides/regions/index.md):** Firma działa w wielu regionach geograficznych z różnymi wymaganiami dotyczącymi niezależności danych. Aby spełnić te wymagania, należy uwzględnić dodatkowe kwestie podczas przeglądu wymagań wstępnych i dystrybucji zasobów w trakcie migracji.

### <a name="technology-driven-scope-expansion"></a>Aspekty technologiczne rozszerzenia zakresu

- **[Migracja hostów VMware](./vmware-host.md):** Migracja hostów VMware może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym hostem VMware można przenieść wiele obciążeń do chmury metodą „lift and shift”. Po migracji te maszyny wirtualne i obciążenia mogą pozostać w programie VMware lub zostać przeniesione do nowoczesnych rozwiązań chmurowych.
- **[Migracja serwerów SQL](./sql-migration.md):** Migracja serwerów SQL może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym serwerem SQL można przenieść wiele baz danych i usług, potencjalnie przyspieszając wiele obciążeń.
- **[Wiele centrów danych](./multiple-datacenters.md):** Migracja wielu centrów danych zdecydowanie zwiększa złożoność. Podczas procesów oceny, migracji, optymalizacji i zarządzania omówiono dodatkowe zagadnienia związane z przygotowaniem bardziej złożonych środowisk.
- **[Wymagania dotyczące danych przekraczają pojemność sieci](./network-capacity-exceeded.md):** Firmy często decydują się na migrację do chmury, ponieważ pojemność, szybkość lub stabilność istniejącego centrum danych nie jest już zadowalająca. Niestety te same ograniczenia zwiększają złożoność procesu migracji, co wymaga dodatkowego planowania w procesach oceny i migracji.
- **[Strategia utrzymania ładu lub zgodności](./governance-or-compliance.md):** Jeśli ład i zgodność są ważne z punktu widzenia powodzenia migracji, wymagana jest dodatkowa współpraca między zespołem ds. ładu w zasobach IT i zespołem ds. wdrożenia chmury.

Jeśli którykolwiek z tych obszarów złożoności występuje w Twoim scenariuszu, ta sekcja przewodnika Cloud Adoption Framework prawdopodobnie będzie zawierać wskazówki, które pomogą Ci prawidłowo dostosować zakres w procesie migracji.

Każdy z tych scenariuszy został opisany w różnych artykułach w tej sekcji przewodnika Cloud Adoption Framework.

## <a name="next-steps"></a>Następne kroki

Przejrzyj spis treści po lewej stronie, aby znaleźć tematy dotyczące określonych potrzeb lub zmian zakresu. Przeglądanie tych scenariuszy można też zacząć od pierwszego rozszerzenia zakresu na liście, dotyczącego [obsługi rynków globalnych](../../decision-guides/regions/index.md).

> [!div class="nextstepaction"]
> [Obsługa rynków globalnych](../../decision-guides/regions/index.md)
