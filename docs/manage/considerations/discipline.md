---
title: Poziomy zarządzania w zarządzaniu chmurą
description: Dowiedz się, jak zawęzić opcje zarządzania chmurą do spójnego zestawu procesów i narzędzi, które można zaoferować w przypadku obciążeń hostowanych w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: c57b2326475f9434aee0b98cf69bf85956ce076e
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527106"
---
# <a name="management-leveling-across-cloud-management-disciplines"></a>Bilansowanie zarządzania w różnych dziedzinach zarządzania chmurą

Klucze do właściwego zarządzania w każdym środowisku to spójne i powtarzalne procesy. Istnieją nieograniczone opcje dla elementów, które można wykonać na platformie Azure. Podobnie istnieją podejścia niezliczone do zarządzania chmurą. Aby zapewnić spójność i powtarzalność, ważne jest zawężenie tych opcji do spójnego zestawu procesów zarządzania i narzędzi, które będą oferowane w przypadku obciążeń hostowanych w chmurze.

## <a name="suggested-management-levels"></a>Sugerowane poziomy zarządzania

Ponieważ obciążenia w portfolio IT różnią się, jest mało prawdopodobne, że w każdym obciążeniu wystarczą jeden poziom zarządzania. Aby ułatwić obsługę różnorodnych obciążeń i zobowiązań firmy, zalecamy, aby zespół operacji w chmurze lub zespół operacyjny platformy ustanowił kilka poziomów zarządzania operacjami.

![Zarządzanie poziomami zarządzania i data_spłaty w strukturze wdrażania chmury](../../_images/manage/cloud-management-maturity.png)

Jako punkt początkowy należy rozważyć ustanowienie poziomów zarządzania, które są wyświetlane na powyższym diagramie i sugerowane na poniższej liście:

- **Linia bazowa zarządzania:** Linia bazowa zarządzania chmurą (lub linia bazowa zarządzania) to zdefiniowany zestaw narzędzi, procesów i spójnych cen, które stanowią podstawę dla wszystkich zarządzania chmurą na platformie Azure. Aby utworzyć linię bazową zarządzania chmurą i określić, które narzędzia mają być uwzględnione w ofercie linii bazowej dla Twojej firmy, zapoznaj się z listą w sekcji "dyscypliny zarządzania chmurą".
- **Rozszerzona linia bazowa:** Niektóre obciążenia mogą wymagać ulepszeń linii bazowej, które nie muszą być specyficzne dla jednej platformy lub obciążenia. Chociaż te udoskonalenia nie są opłacalne dla każdego obciążenia, powinny istnieć typowe procesy, narzędzia i rozwiązania dla dowolnego obciążenia, które może uzasadnić koszt dodatkowej pomocy technicznej zarządzania.
- **Specjalizacja platformy:** W każdym danym środowisku niektóre popularne platformy są używane przez wiele obciążeń. Ten ogólny wspólny architektura architektury nie zmienia się w przypadku, gdy firmy przyjmie chmurę. Specjalizacja platformy to podwyższony poziom zarządzania, który stosuje wiedzę o zakresie danych i architektury w celu zapewnienia wyższego poziomu zarządzania operacyjnego. Przykłady specjalizacji platformy obejmują funkcje zarządzania specyficzne dla SQL Server, kontenerów, Active Directory lub innych usług, które mogą być lepiej zarządzane przez spójne, powtarzalne procesy, narzędzia i architektury.
- **Specjalizacja obciążenia:** W przypadku obciążeń, które mają prawdziwie krytyczne znaczenie, może być uzasadnione obniżenie kosztów w zakresie zarządzania obciążeniem. Specjalizacja obciążeń stosuje dane telemetryczne obciążenia, aby określić bardziej zaawansowane podejścia do codziennego zarządzania. Te same dane często identyfikują ulepszenia automatyzacji, wdrażania i projektowania, które mogłyby prowadzić do zwiększenia stabilności, niezawodności i odporności poza możliwościami w zakresie zarządzania operacyjnego.
- **Nieobsługiwane:** Równie ważne jest, aby komunikować się z typowymi procesami zarządzania, które nie są dostarczane przez dyscypliny zarządzania chmurą dla obciążeń, które są klasyfikowane jako nieobsługiwane lub niekrytyczne.

Organizacje mogą również zdecydować się na [obsługę funkcji związanych z co najmniej jednym z tych poziomów zarządzania dla usługodawcy](https://www.microsoft.com/cloud-adoption-framework-offers?ot=manage). Dostawcy usług mogą korzystać z [usługi Azure Lighthouse](https://azure.com/lighthouse) w celu zapewnienia większej dokładności i przejrzystości.

Pozostałe artykuły w tej serii dotyczą procesów, które są często dostępne w ramach każdej z tych dyscyplin.
Równolegle w [przewodniku zarządzania systemu Azure](../azure-management-guide/index.md) zademonstrowano narzędzia, które mogą obsługiwać poszczególne procesy. Aby uzyskać pomoc dotyczącą tworzenia linii bazowej zarządzania, Zacznij od przewodnika zarządzania platformy Azure. Po ustaleniu linii bazowej ta seria artykułu i towarzyszące najlepsze rozwiązania mogą pomóc rozszerzyć tę linię bazową w celu zdefiniowania innych poziomów obsługi zarządzania.

## <a name="cloud-management-disciplines"></a>Dyscypliny zarządzania chmurą

Każdy sugerowany poziom zarządzania może wywoływać różne dyscypliny zarządzania chmurą. Mapowanie zostało jednak zaprojektowane, aby ułatwić znalezienie sugerowanych procesów i narzędzi do dostarczenia na odpowiednim poziomie zarządzania chmurą.

W większości przypadków opisany wcześniej *poziom odniesienia zarządzania* składa się z procesów i narzędzi z następujących dyscyplin. W każdym przypadku kilka procesów i narzędzi są wyróżnione w celu pokazania *rozszerzonych funkcji linii bazowej*.

- **Spis i widoczność:** Podstawowa linia bazowa zarządzania powinna zawierać środki tworzenia spisu zasobów i umożliwia wgląd w stan uruchomienia każdego elementu zawartości.
- **Zgodność operacyjna:** Regularne zarządzanie konfiguracją, ustalaniem rozmiarów, kosztami i wydajnością zasobów jest kluczem do obsługi oczekiwań wydajności i linii bazowej zarządzania.
- **Ochrona i odzyskiwanie:** Minimalizacja przerw w działaniu i przyspieszanie odzyskiwania może pomóc uniknąć ubytków wydajności i przychodów. Wykrywanie i odzyskiwanie są ważnymi aspektami tej dyscypliny w ramach każdej linii bazowej zarządzania.

Poziom specjalizacji platformy zarządzania ściągają z procesów i narzędzi, które są wyrównane z dyscyplinami operacji platformy. Podobnie poziom specjalizacji obciążeń jest pobierany z procesów i narzędzi, które są wyrównane z dyscyplinami operacji obciążenia.

## <a name="next-steps"></a>Następne kroki

Następnym krokiem do definiowania każdego poziomu zarządzania chmurą jest zrozumienie [spisu i widoczności](./inventory.md).

> [!div class="nextstepaction"]
> [Opcje spisu i widoczności](./inventory.md)
