---
title: Bilansowanie zarządzania w różnych dziedzinach zarządzania chmurą
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Bilansowanie zarządzania w różnych dziedzinach zarządzania chmurą
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 294ea288af478e0e451c9fd38663a26acb10359d
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682588"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Bilansowanie zarządzania w różnych dziedzinach zarządzania chmurą

Kluczem do prawidłowego zarządzania w każdym środowisku jest spójność i powtarzalne procesy. Istnieją nieograniczone opcje dla elementów, które można wykonać na platformie Azure. Podobnie istnieją podejścia niezliczone do zarządzania chmurą. Aby zapewnić spójność i powtarzalność, ważne jest zawężenie tych opcji do spójnego zestawu procesów zarządzania i narzędzi, które będą oferowane dla obciążeń hostowanych w chmurze.

## <a name="suggested-management-levels"></a>Sugerowane poziomy zarządzania

Ponieważ obciążenia w portfelu IT nie są takie same, jest mało prawdopodobne, że w każdym obciążeniu wystarcza jeden poziom zarządzania. Aby obsługiwać różne obciążenia i różne zobowiązania biznesowe, zaleca się, aby zespół operacji w chmurze lub zespół operacyjny platformy ustanowił kilka poziomów zarządzania operacjami.

![Zarządzanie poziomami zarządzania i data_spłaty w strukturze wdrażania chmury](../../_images/manage/cloud-management-maturity.png)

Następujące poziomy zarządzania (podano również powyżej) to kilka sugerowanych poziomów służących jako punkt początkowy:

- **Linia bazowa zarządzania**: punkt odniesienia zarządzania chmurą (lub linia bazowa zarządzania) to zdefiniowany zestaw narzędzi, procesów i spójnych cen, które będą stanowić podstawę dla wszystkich zarządzania chmurą na platformie Azure. Aby ustanowić linię bazową zarządzania chmurą, zapoznaj się z tabelą w poniższej sekcji i ustal, które narzędzia zostaną dołączone do Twojej firmy.
- **Rozszerzona linia bazowa**: szereg obciążeń może wymagać ulepszeń linii bazowej, które nie muszą być specyficzne dla jednej platformy lub obciążenia. Chociaż te udoskonalenia nie są opłacalne dla każdego obciążenia, powinny istnieć typowe procesy, narzędzia i rozwiązania dla dowolnego obciążenia, które może obsłużyć dodatkowe wsparcie w zakresie zarządzania.
- **Specjalizacja platform**: w każdym danym środowisku istnieją popularne platformy, które są używane przez wiele różnych obciążeń. Ten ogólny wspólny architektura architektury nie zmienia się w przypadku, gdy firmy przyjmie chmurę. Specjalizacja platformy to podwyższony poziom zarządzania, który wykorzystuje wiedzę z zakresu danych i architektury w celu zapewnienia wyższego poziomu zarządzania operacyjnego. Przykłady specjalizacji platformy obejmują funkcje zarządzania specyficzne dla SQL Server, kontenerów, Active Directory lub innych usług, które mogą być lepiej zarządzane przez spójne, powtarzalne procesy, narzędzia i architektury.
- **Specjalizacja obciążeń**: w przypadku obciążeń, które są prawdziwie krytyczne, może być uzasadnione obniżenie kosztów, aby znacznie lepiej zarządzać tym obciążeniem. Specjalizacja obciążeń wykorzystuje telemetrię obciążenia, aby określić bardziej zaawansowane podejścia do codziennego zarządzania. Te same dane często identyfikują ulepszenia automatyzacji, wdrażania i projektowania, które mogłyby prowadzić do zwiększenia stabilności, niezawodności i odporności poza możliwościami w zakresie zarządzania operacyjnego.
- **Nieobsługiwane**: jest równie ważne, aby komunikować się z typowymi procesami zarządzania, które nie zostaną dostarczone przez dyscypliny zarządzania chmurą dla każdego obciążenia, które jest sklasyfikowane jako nieobsługiwane lub niekrytyczne.

Pozostałe artykuły w tej serii obejmują wiele procesów często znalezionych w ramach każdej z tych dyscyplin.
Równolegle w [przewodniku zarządzania systemu Azure](../azure-management-guide/index.md) zademonstrowano narzędzia, które mogą obsługiwać poszczególne procesy. Aby uzyskać pomoc w tworzeniu linii bazowej zarządzania, Zacznij od przewodnika zarządzania platformy Azure. Po nawiązaniu planu bazowego ta seria artykułu i towarzyszące najlepsze rozwiązania mogą pomóc rozszerzyć tę linię bazową w celu zdefiniowania innych poziomów obsługi zarządzania.

## <a name="cloud-management-disciplines"></a>Dyscypliny zarządzania chmurą

Każdy z sugerowanych poziomów zarządzania może wywoływać różne dyscypliny zarządzania chmurą. Mapowanie zostało jednak zaprojektowane, aby ułatwić znalezienie sugerowanych procesów i narzędzi do dostarczenia na odpowiednim poziomie zarządzania chmurą.

W większości przypadków podane powyżej "poziom odniesienia zarządzania" będzie obejmowało procesy i narzędzia z następujących dyscyplin. W każdym przypadku kilka procesów i narzędzi są wyróżnione w celu pokazania "ulepszonych funkcji bazowych".

- **Spis i widoczność**: co najmniej podstawowa linia bazowa zarządzania powinna zawierać środki spisu zasobów i umożliwiać wgląd w stan uruchomienia każdego elementu zawartości.
- **Zgodność operacyjna:** Regularne zarządzanie konfiguracją, ustalaniem rozmiarów, kosztami i wydajnością zasobów jest kluczem do obsługi oczekiwań wydajności i linii bazowej zarządzania.
- **Ochrona i odzyskiwanie:** Minimalizacja przerw w działaniu i przyspieszanie odzyskiwania pozwala uniknąć strat wydajności i przychodów. Wykrywanie i odzyskiwanie są ważnymi aspektami tej dyscypliny w ramach każdej linii bazowej zarządzania.

Poziom specjalizacji platformy zarządzania ściągają z procesów i narzędzi wyrównanych do dyscyplin operacji platformy.
Podobnie poziom specjalizacji obciążeń jest pobierany z procesów i narzędzi wyrównanych do dyscyplin operacji obciążenia.
  
## <a name="next-steps"></a>Następne kroki

Następnym krokiem do definiowania każdego poziomu zarządzania chmurą jest zrozumienie [spisu i widoczności](./inventory.md).

> [!div class="nextstepaction"]
> [Opcje spisu i widoczności](./inventory.md)
