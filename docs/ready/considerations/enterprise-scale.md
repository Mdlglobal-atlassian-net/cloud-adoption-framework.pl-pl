---
title: Rozpoczynanie pracy ze skalą korporacyjną strefy wyładunkowe
description: Rozpoczynanie pracy ze skalą korporacyjną strefy wyładunkowe
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 1e34cf58fd3f9827a3cf8dd1ffd866fdcfcca1f7
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215232"
---
# <a name="start-with-enterprise-scale-landing-zones"></a>Rozpoczynanie pracy ze skalą korporacyjną strefy wyładunkowe

Czasami zespół platformy w chmurze może być niewielki i skalowalny. Zespoły pracowały przez lata w ramach ograniczeń istniejącego środowiska lokalnego w firmie w celu uzyskania dostępu do bieżącego stanu zapadalności w zakresie zabezpieczeń, operacji i zarządzania. Replikacja żądanych procesów, narzędzi i architektur w oparciu o nowe ograniczenia środowiska chmury zajmie trochę czasu. Aby przyspieszyć proces uczenia się, wymagany jest nieco inny punkt początkowy. Porównanie poniższego obrazu ze [wskazówkami dotyczącymi wczesnego refaktoryzacji w ramach tej metodologii](../landing-zone/refactor.md), podstawowa zmiana jest punktem początkowym, który jest teraz bardziej skomplikowany, co więcej w dalszej części tego artykułu.

![Ilustracja refaktoryzacji strefy ładunkowej — opisana w dalszej części tego artykułu](../../_images/ready/refactor-enterprise-scale.png)

<!-- markdownlint-disable MD026 -->

## <a name="qualifiers-should-i-start-with-enterprise-scale"></a>Kwalifikatory: czy należy zacząć od skali przedsiębiorstwa?

W przypadku większości gotowych wzorców podejście "Rozpocznij małe i rozwijające" jest preferowane, ponieważ umożliwia zespołowi uczenie się od prawdziwych środowisk. W przypadku firm, które pasują do odwołań w tym artykule, jest wymagane bardziej niezawodne podejście.

### <a name="scale-and-speed"></a>Skalowanie i szybkość

Gdy zespół adopcji ma cel midterm (w ciągu 24 miesięcy), aby hostować ponad 1 000 zasobów (aplikacji, infrastruktury lub zasobów danych) w chmurze, nie ma wystarczająco dużo czasu, aby dowiedzieć się więcej na temat podejścia praktycznego. Aby zapewnić niezbędną prędkość i skalę dla dużego przedsiębiorstwa, należy ustawić wiele kryteriów.

### <a name="security-compliance-and-culture"></a>Zabezpieczenia, zgodność i kultura

Aby można było zacząć dowolnie, wiele motywacji w biznesie może wymagać strefy wyładunkowej i usług udostępnionych w skali przedsiębiorstwa. Konieczność rozwiązania strefy centralnej w skali przedsiębiorstwa może być oczywista dla firm, których firmy są zbudowane wokół danych poufnych i złożonych architektur zależnych. Może to być również oczywiste, gdy firmy wymagają środowiska chmury, które spełniają rygorystyczne wymagania innych firm przed rozpoczęciem korzystania z chmury. Kultury z głęboko głównymi centralnymi modelami kontroli IT mogą również potrzebować architektury, która rozpoczyna się od scentralizowanej kontroli w celu przekazywania wymagań dotyczących kontroli zmian.

### <a name="all-in-on-the-cloud"></a>Wszystkie — w chmurze

Najbardziej typowym sterownikiem strefy wyładunkowej skali przedsiębiorstwa są firmy, które decydują o przejściu na chmurę w chmurze. Może to wynikać z zakończenia centrum danych lub przepływu masy, aby być bardziej Agile jako firma. Bez względu na to, że ta decyzja biznesowa zazwyczaj wymaga skalowania i szybkości wdrażania. Ta kombinacja wymagań utrudnia czas potrzebny na naukę i przygotowanie się do poufnych danych i usługi krytycznej w chmurze.

### <a name="skill-requirements"></a>Wymagania dotyczące kwalifikacji

Począwszy od skali przedsiębiorstwa założono, że zespół platformy Cloud Platform ma budżety w skali przedsiębiorstwa. Ten kwalifikator zakłada, że zespół ma więcej umiejętności w chmurze niż większość innych firm. Umiejętności te mogą pochodzić z istniejącej historii mniejszych skalowalnych rozwiązań w chmurze w ramach firmy. Umiejętności mogą być również dodawane przez przeciąganie się z doświadczonym personelem lub praca z wysoce doświadczonymi partnerami. W obu kierunkach wymagane są następujące umiejętności, aby zacząć od skali przedsiębiorstwa.

Sugerowane umiejętności:

- Szczegółowa wiedza na temat architektury w wybranym dostawcy chmury.
- Wszechstronne środowisko pracy dzięki infrastrukturze opartej na chmurze, jako podejścia do kodu.
- Umiarkowana znajomość usługi GitHub lub innych repozytoriów kodu źródłowego, takich jak rozgałęzianie i strategie żądania ściągnięcia.
- Środowisko umożliwiające działanie z automatycznymi wdrożeniami z kodu źródłowego do dostawcy chmury.

Jeśli te umiejętności nie są dostępne w zespole platformy w chmurze (za pomocą personelu, partnerów lub innych mechanizmów pomocy technicznej), podejście "Rozpocznij małe i rozszerzone" może szybko dotrzeć do gotowości przedsiębiorstwa przy użyciu wyższej jakości danych wyjściowych. Takie podejście byłoby tańsze, a zdobycie umiejętności w ramach istniejącego zespołu.

## <a name="start-with-an-enterprise-scale-landing-zones"></a>Rozpocznij pracę z strefami wyładunkowymi w skali przedsiębiorstwa

Firma Microsoft ma obszerną historię inwestowania w narzędzia i podejścia ułatwiające klientom tworzenie i Zarządzanie strefami wyładunkowymi w skali przedsiębiorstwa. W ostatnich latach wystąpiły wskazówki i narzędzia na platformie Azure. To podejście inwestycyjne kontynuuje działanie i może skutkować regularnymi aktualizacjami tej sekcji tego artykułu.

![Ilustracja refaktoryzacji strefy wyładunkowej](../../_images/ready/refactor-enterprise-scale.png)

Każdy z poniższych szablonów zapewnia klientom początkową strefę docelową skalowania w przedsiębiorstwie, w tym wzorce infrastruktury:

- [Usługi udostępnione ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-shared)
- [Obciążenie środowiska App Service Environment/bazy danych SQL ISO 27001](https://docs.microsoft.com/azure/governance/blueprints/samples/iso27001-ase-sql-workload)
- [Oficjalne Królestwo brytyjskie i Zjednoczone Królestwo NHS](https://docs.microsoft.com/azure/governance/blueprints/samples/ukofficial)

Dodatkowe przykłady artykułu dotyczącego [planów platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/samples) można użyć jako "Red/Green" w przypadku stref wyładunkowych skali przedsiębiorstwa. Zastosowanie tych planów zapewni, że środowisko spełnia standardy zgodności przed wdrożeniem. Takie późniejsze podejście jest szczególnie przydatne w przypadku weryfikowania stref wyładunkowych innych firm lub partnerów przed przyjęciem chmury:

## <a name="next-steps"></a>Następne kroki

Wybierz jedną z planów strefy ładunkowej skali przedsiębiorstwa.
Z tego względu te same wskazówki w obszarze [Rozpocznij mały i rozwiń](./index.md) mogą służyć do rozszerzania stref wyładunkowych w skali korporacyjnej w celu dopasowania do różnych wymagań.

> [!div class="nextstepaction"]
> [Wznów wskazówki "Rozpocznij małe i rozwijane" przy użyciu strefy docelowej skalowania korporacyjnego jako źródła początkowego](./index.md)
