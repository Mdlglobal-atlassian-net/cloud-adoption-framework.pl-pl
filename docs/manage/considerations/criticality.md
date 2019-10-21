---
title: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Krytyczne znaczenie biznesowe — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 6e372156d3fd8d765bcafeeff3a6919aa7f8ead3
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557624"
---
# <a name="business-criticality-in-cloud-management"></a>Krytyczne znaczenie biznesowe w zarządzaniu chmurą

Dla każdej firmy istnieje niewielka liczba obciążeń, które są zbyt ważne, aby zakończyć się niepowodzeniem. Gdy te obciążenia są w stanie awarii lub obniżeniu wydajności, niekorzystny wpływ na dochody i zyskowność można uzyskać w całej firmie. Te obciążenia są uważane za krytyczne.

Z drugiej strony, niektóre obciążenia mogą zaczynać miesiące w danym momencie bez użycia. Niska wydajność lub przerwy w obciążeniu nie są pożądane, ale wpływ jest odizolowany i ograniczony.

Zrozumienie znaczenia każdego obciążenia w portfolio IT to pierwszy krok w kierunku wzajemnych zobowiązań związanych z zarządzaniem chmurą.
Na poniższej ilustracji przedstawiono wspólne wyrównanie między skalą o krytycznym znaczeniu i standardowe zobowiązania podejmowane przez firmę.

![Wyrównanie poziomu krytycznego i zarządzania](../../_images/manage/cloud-criticality-alignment.png)

## <a name="criticality-scale"></a>Skalowanie krytyczne

Pierwszym krokiem związanym z wyrównaniem krytycznym dla działania firmy jest utworzenie skali krytycznej. Poniżej znajduje się przykładowa Skala, która może być używana jako odwołanie, lub szablon do tworzenia własnej skali.

|Zagrożenia  |Widok biznesowy  |
|---------|---------|
|Krytyczne znaczenie dla działalności|Ma wpływ na misja firmy i może mieć zauważalny wpływ na firmowe zestawienie zysków i strat.|
|Krytyczne dla jednostki|Ma wpływ na misja określonej jednostki biznesowej i instrukcje dotyczące zysków i strat jednostek biznesowej.|
|Wysoka|Może nie utrudniać pracy, ale ma wpływ na procesy o wysokiej ważności. Wymierne straty mogą być wymierne w przypadku awarii.|
|Średnie|Przyczyną może być wpływ na procesy. Straty są niskie lub wymierne, ale prawdopodobnie uszkodzenie marki lub straty w strumieniu.|
|Niska|Wpływ na procesy biznesowe jest niewymierny. Nie jest możliwe uszkodzenie marki ani straty w strumieniu. Prawdopodobnie zostanie zlokalizowany wpływ na jednego zespołu.|
|Nieobsługiwane|Żaden właściciel firmy, zespół lub proces skojarzony z tym obciążeniem nie może uzasadnić inwestycji w bieżące zarządzanie obciążeniem|

Firma jest powszechna w przypadku firm, które uwzględniają dodatkowe klasyfikacje krytyczne charakterystyczne dla branżowych, pionowych lub określonych procesów biznesowych. Przykłady dodatkowych klasyfikacji obejmują:

- **Zgodność — krytyczne:** W silnie regulowanej branży niektóre obciążenia mogą być krytyczne w ramach nakładu pracy, aby zachować wymagania dotyczące zgodności.
- **Krytyczne dla zabezpieczeń:** Niektóre obciążenia mogą nie być krytyczne dla działalności, ale może to spowodować utratę danych lub niezamierzony dostęp do chronionych informacji.
- **Krytyczne dla bezpieczeństwa:** W przypadku istnienia lub fizycznego bezpieczeństwa pracowników i klientów podczas awarii może być konieczne klasyfikowanie obciążeń jako krytycznych dla bezpieczeństwa.

## <a name="importance-of-accurate-criticality"></a>Znaczenie dokładnej krytycznej ważności

W dalszej części tego procesu zespół zarządzający chmurą będzie używać tej klasyfikacji do określenia wielkości nakładu pracy wymaganej do spełnienia poziomów stopnia krytycznego. W środowiskach lokalnych program Operations Management jest często kupowany i traktowany jak niezbędne obciążenia biznesowe, z niewielkimi dodatkowymi kosztami operacyjnymi. W chmurze usługa Operations Management (na przykład cała chmura) jest kupowana na podstawie zasobów jako miesięczne koszty operacyjne.

Ze względu na to, że istnieje jasne i bezpośrednie koszty zarządzania operacjami w chmurze, ważne jest odpowiednie dostosowanie kosztów i odpowiednich skalowalności.

## <a name="select-a-default-criticality"></a>Wybierz domyślną wartość krytyczną

Wstępne przegląd każdego obciążenia w portfolio może być czasochłonne. W celu zapewnienia, że to wysiłki nie zablokuje szerszej strategii chmurowej, zaleca się, aby dział IT i firma zgadzali się na domyślną wartość krytyczną, która ma zastosowanie do wszystkich obciążeń.

Zgodnie z powyższym skalowaniem o krytycznym znaczeniu zaleca się użycie "średniego" krytycznego jako domyślnego. Dzięki temu zespół strategii chmurowej będzie mógł szybko identyfikować obciążenia, które wymagają wyższego poziomu zagrożenia.

## <a name="using-the-template"></a>Korzystanie z szablonu

Poniższe kroki dotyczą czytelników, którzy używają [skoroszytu usługi Ops Management](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) do planowania zarządzania chmurą.

1. Skalę krytyczne można zarejestrować na karcie Skala skoroszytu.
2. Każde obciążenie w "przykładowym" lub "czystym szablonie" powinno zostać zaktualizowane w celu odzwierciedlenia domyślnej krytycznej w kolumnie "krytyczne".
3. Poprawne wartości powinny być wprowadzane przez firmę w celu odzwierciedlenia wszelkich odchyleń od domyślnej krytycznej.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu stanu krytycznego należy [obliczyć i zarejestrować wpływ na działalność biznesową](./impact.md).

> [!div class="nextstepaction"]
> [Oblicz i zarejestruj wpływ na firmę](./impact.md)
