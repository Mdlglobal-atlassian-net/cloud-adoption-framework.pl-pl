---
title: Najlepsze rozwiązania dotyczące migracji na platformę Azure
description: Użyj struktury wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak zaimplementować narzędzia niezbędne do zachowania zgodności z najlepszymi rozwiązaniami dotyczącymi migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 90ec573d59c88187081fd640d9eb769977b787cf
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79091429"
---
# <a name="best-practices-for-cloud-migration"></a>Najlepsze rozwiązania dla migracji do chmury

Jeśli chcesz przeprowadzić migrację na platformę Azure, zaleca się skorzystanie z [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) w strukturze wdrażania chmury. Ten przewodnik przeprowadzi Cię przez szereg narzędzi oraz podejść związanych z migrowaniem maszyn wirtualnych do chmury. Ta sekcja struktury wdrażania chmury dotyczy wielu najlepszych rozwiązań, które wykraczają poza podstawowe narzędzia natywne dla chmury.

## <a name="cloud-migration-best-practice-checklist"></a>Lista kontrolna najlepszych rozwiązań dotyczących migracji do chmury

Poniższa lista kontrolna zawiera typowe obszary złożoności, które mogą wymagać rozszerzenia zakresu migracji poza [Przewodnik po migracji na platformę Azure](../azure-migration-guide/index.md).

### <a name="business-driven-scope-expansion"></a>Aspekty biznesowe rozszerzenia zakresu

- **[Obsługa rynków globalnych](./multiple-regions.md):** Firma działa w wielu regionach geograficznych z różnymi wymaganiami dotyczącymi niezależności danych. Aby spełnić te wymagania, należy uwzględnić dodatkowe kwestie podczas przeglądu wymagań wstępnych i dystrybucji zasobów w trakcie migracji.

### <a name="technology-driven-scope-expansion"></a>Aspekty technologiczne rozszerzenia zakresu

- **[Migracja hostów VMware](./vmware-host.md):** Migracja hostów VMware może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym hostem VMware można przenieść wiele obciążeń do chmury metodą „lift and shift”. Po migracji te maszyny wirtualne i obciążenia mogą pozostać w programie VMware lub zostać przeniesione do nowoczesnych rozwiązań chmurowych.
- **[Migracja serwerów SQL](./sql-migration.md):** Migracja serwerów SQL może przyspieszyć ogólny proces migracji. Wraz z każdym migrowanym serwerem SQL można przenieść wiele baz danych i usług, potencjalnie przyspieszając wiele obciążeń.
- **[Wiele centrów danych](./multiple-datacenters.md):** Migracja wielu centrów danych zdecydowanie zwiększa złożoność. Podczas procesów oceny, migracji, optymalizacji i zarządzania omówiono dodatkowe zagadnienia związane z przygotowaniem bardziej złożonych środowisk.
- **[Wymagania dotyczące danych przekraczają pojemność sieci](./network-capacity-exceeded.md):** Firmy często decydują się na migrację do chmury, ponieważ pojemność, szybkość lub stabilność istniejącego centrum danych nie jest już zadowalająca. Niestety te same ograniczenia zwiększają złożoność procesu migracji, co wymaga dodatkowego planowania w procesach oceny i migracji.
- **[Strategia utrzymania ładu lub zgodności](./governance-or-compliance.md):** Jeśli ład i zgodność są ważne z punktu widzenia powodzenia migracji, wymagana jest dodatkowa współpraca między zespołem ds. ładu w zasobach IT i zespołem ds. wdrożenia chmury.

Jeśli którykolwiek z tych obszarów złożoności występuje w Twoim scenariuszu, ta sekcja przewodnika Cloud Adoption Framework prawdopodobnie będzie zawierać wskazówki, które pomogą Ci prawidłowo dostosować zakres w procesie migracji.

Każdy z tych scenariuszy został opisany w różnych artykułach w tej sekcji przewodnika Cloud Adoption Framework.

## <a name="next-steps"></a>Następne kroki

Przejrzyj spis treści po lewej stronie, aby znaleźć tematy dotyczące określonych potrzeb lub zmian zakresu. Przeglądanie tych scenariuszy można też zacząć od pierwszego rozszerzenia zakresu na liście, dotyczącego [obsługi rynków globalnych](./multiple-regions.md).

> [!div class="nextstepaction"]
> [Obsługa rynków globalnych](./multiple-regions.md)
