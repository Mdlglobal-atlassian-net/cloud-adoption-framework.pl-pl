---
title: Likwidowanie wycofanych zasobów
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak prawidłowo zlikwidować wycofane zasoby z minimalnymi zakłóceniami działania firmy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a62ef520f948d8bea415e4a65749944b91bb16c8
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092758"
---
# <a name="decommission-retired-assets"></a>Likwidowanie wycofanych zasobów

Gdy obciążenie zostanie podwyższone do środowiska produkcyjnego, zasoby, które wcześniej hostowały obciążenie produkcyjne, nie będą już wymagane do obsługi operacji biznesowych. W tym momencie starsze zasoby są uważane za wycofane. Wycofane zasoby można następnie zlikwidować, zmniejszając koszty operacyjne. Likwidowanie zasobu może być tak proste jak wyłączenie zasilania tego zasobu i pozbycie się go w odpowiedzialny sposób. Niestety likwidowanie zasobów może czasami mieć niepożądane konsekwencje. Poniższe wskazówki mogą pomóc w prawidłowym likwidowaniu wycofanych zasobów z minimalnymi zakłóceniami działania firmy.

## <a name="cost-savings-realization"></a>Realizacja oszczędności kosztów

Gdy oszczędności są główną motywacją do migracji, likwidowanie jest ważnym krokiem. Dopóki zasób nie zostanie zlikwidowany, będzie zużywać nadal energię, wsparcie środowiskowe i inne zasoby, które zwiększają koszty. Po zlikwidowaniu zasobu można zacząć realizować oszczędności kosztów.

## <a name="continued-monitoring"></a>Ciągłe monitorowanie

Po podwyższeniu poziomu migrowanego obciążenia zasoby, które mają zostać wycofane, powinny być nadal monitorowane w celu sprawdzenia, czy żaden dodatkowy ruch produkcyjny nie jest kierowany do niewłaściwych zasobów.

## <a name="testing-windows-and-dependency-validation"></a>Okna testowania i walidacja zależności

Nawet przy najlepszym planowaniu obciążenia produkcyjne mogą nadal zawierać zależności od zasobów uważanych za wycofane. W takich przypadkach wyłączenie wycofanego zasobu może spowodować nieoczekiwane awarie systemu. W związku z tym zakończenie wszelkich zasobów powinno być obsługiwane przy użyciu tego samego poziomu rygoru, co działanie konserwacyjne systemu. Aby ułatwić zakończenie pracy z zasobem, należy określić odpowiednie okna testowania i przestojów.

## <a name="holding-period-and-data-validation"></a>Okres przechowywania i walidacja danych

Nierzadko w przypadku migracji dochodzi do pominięcia danych podczas procesów replikacji. Dotyczy to szczególnie starszych danych, które nie są regularnie używane. Po wyłączeniu wycofanego zasobu warto zachować go przez pewien czas, aby stanowił tymczasową kopię zapasową danych. Przed zniszczeniem wycofanych zasobów firmy powinny mieć co najmniej 30 dni na potrzeby przechowywania i testowania.

## <a name="next-steps"></a>Następne kroki

Po zlikwidowaniu wycofanych zasobów migracja zostanie zakończona. To dobry moment na udoskonalenie procesu migracji, a [retrospektywa](./retrospective.md) pozwoli na zaangażowanie zespołu wdrożeniowego ds. chmury w procesie przeglądu wydania w celu szkolenia i wprowadzenia ulepszeń.

> [!div class="nextstepaction"]
> [Retrospektywa](./retrospective.md)
