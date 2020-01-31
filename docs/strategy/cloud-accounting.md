---
title: Czym jest księgowość w chmurze?
description: Wyjaśnienie koncepcji ewidencjonowania aktywności w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 008958e0542a52f022bbf2ba3183fbfb8c78b9ee
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806819"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>Czym jest księgowość w chmurze?

Chmura zmienia sposób kont IT w sposób opisany w temacie [Tworzenie modelu finansowego na potrzeby transformacji w chmurze](./financial-models.md). Różne modele ewidencjonowania aktywności IT są znacznie łatwiejsze do obsługi ze względu na sposób przydzielania przez chmurę kosztów. Dlatego ważne jest, aby zrozumieć, jak uwzględnić koszty związane z chmurą przed rozpoczęciem podróży w chmurze. W tym artykule opisano najbardziej typowe modele ewidencjonowania aktywności w chmurze.

## <a name="traditional-it-accounting-cost-center-model"></a>Tradycyjne ewidencjonowanie aktywności IT (model centrum kosztów)

Często warto rozważyć przeanalizowanie centrum kosztów. W tradycyjnym modelu księgowości IT konsoliduje możliwości zakupu dla wszystkich zasobów IT. Jak wskazano w artykule [Modele finansowe](./financial-models.md) , kupowanie może obejmować licencje na oprogramowanie, cykliczne opłaty za Licencjonowanie programu CRM, zakup pulpitów pracowników i inne duże koszty.

Gdy program służy jako centrum kosztów, postrzegana wartość jest w dużym stopniu wyświetlana przez soczewkę zarządzania zaopatrzeniem. To postrzeganie utrudnia odwiedzanie przez zarząd lub inne kierownictwo w zrozumieniu prawdziwej wartości. Koszty zaopatrzenia umożliwiają pochylenie tego widoku poprzez zmniejszenie wszelkich innych wartości dodanych przez organizację. Ten widok wyjaśnia, dlaczego często jest on podzielony na obowiązki DYREKTORa lub dyrektor. To postrzeganie jest ograniczone i może być krótkie.

## <a name="central-it-accounting-profit-center-model"></a>Centralne ewidencjonowanie aktywności IT (model centrum zysków)

Aby przezwyciężyć widok centrum kosztów, niektóre dyrektorzy działu informatyki wybrały dla centralnego modelu INFORMATYCZNego księgowości. W modelu tego typu jest on traktowany jak konkurencyjna jednostka biznesowa i element równorzędny do tworzenia przychodów jednostek gospodarczych. W niektórych przypadkach ten model może być całkowicie logiczny. Na przykład niektóre organizacje mają profesjonalny dział usług IT generujący strumień przychodów. Często centralne modele IT nie generują znaczących przychodów, co utrudnia wyjustowanie modelu.

Niezależnie od modelu przychodu centralne modele ewidencjonowania aktywności IT są unikatowe ze względu na to, jak dział IT stanowi o kosztach. W tradycyjnym modelu IT zespół IT rejestruje koszty i płaci te koszty z udostępnionych funduszy, takich jak operacje i konserwacja (O & M) lub dedykowane konto zysków i strat (P & L).

W centralnym modelu księgowości IT zespół IT oznacza usługi świadczone na potrzeby obciążania, zarządzania i innych szacowanych kosztów. Następnie należy rozrachunkować konkurencyjne jednostki biznesowe dla oznaczonych usług. W tym modelu CIO oczekuje się zarządzania P & L związanego z sprzedażą tych usług. Pozwala to na tworzenie niepełnych kosztów IT i rywalizacji między centralnym działem IT i jednostkami biznesowymi, szczególnie w przypadku konieczności ponoszenia kosztów lub braku zgody na umowy SLA. W miarę możliwości technologii lub zmiany rynkowej każda nowa technologia spowodowałaby zakłócenie w centralnej & L, co utrudnia transformację.

## <a name="chargeback"></a>Obciążenia zwrotnego

Jednym z typowych pierwszych kroków w przypadku zmiany jego reputacji jako centrum kosztów jest implementacja obciążenia zwrotnego modelu ewidencjonowania aktywności. Ten model jest szczególnie powszechny w mniejszych przedsiębiorstwach lub wysoce wydajnych organizacjach IT. W modelu obciążenia zwrotnego wszystkie koszty działu IT powiązane z konkretną jednostką biznesową są traktowane jak koszty operacyjne w budżecie jednostki biznesowej. Ta metoda ogranicza skumulowany wpływ na IT, co pozwala na bardziej jasne zwiększenie wartości biznesowej.

W starszym modelu lokalnym obciążenia zwrotnego jest trudne do zrealizowania, ponieważ ktoś nadal musi przenieść duże wydatki i amortyzację kapitału. Ciągła konwersja z wydatków inwestycyjnych do kosztów operacyjnych związanych z użyciem jest trudną eksploatacją księgową. Ten problem jest głównym powodem tworzenia tradycyjnego modelu księgowości IT i centralnego modelu ewidencjonowania aktywności IT. Model wydatków operacyjnych z rachunku kosztów w chmurze jest prawie wymagany, jeśli chcesz efektywnie dostarczyć model obciążenia zwrotnego.

Ale nie należy implementować tego modelu bez uwzględnienia konsekwencji. Poniżej przedstawiono kilka konsekwencji, które są unikatowe dla modelu obciążenia zwrotnego:

- Obciążenia zwrotnego skutkuje ogromną redukcją ogólnego budżetu IT. W przypadku organizacji IT, które są niewydajne lub wymagają szerokiej złożoności w zakresie operacji lub konserwacji, ten model może ujawnić te wydatki w złej kondycji.
- Utrata kontroli jest powszechną konsekwencją. In highly political environments, chargeback can result in loss of control and staff being reallocated to the business. This could create significant inefficiencies and reduce IT's ability to consistently meet SLAs or project requirements.
- Difficulty accounting for shared services is another common consequence. If the organization has grown through acquisition and is carrying technical debt as a result, it's likely that a high percentage of shared services must be maintained to keep all systems working together effectively.

Cloud transformations include solutions to these and other consequences associated with a chargeback model. But each of those solutions includes implementation and operating expenses. The CIO and CFO should carefully weigh the pros and cons of a chargeback model before considering one.

## <a name="showback-or-awareness-back"></a>Showback or awareness-back

For larger enterprises, a showback or awareness-back model is a safer first step in the transition from cost center to value center. This model doesn't affect financial accounting. In fact, the P&Ls of each organization don't change. The biggest shift is in mindset and awareness. In a showback or awareness-back model, IT manages the centralized, consolidated buying power as an agent for the business. In reports back to the business, IT attributes any direct costs to the relevant business unit, which reduces the perceived budget directly consumed by IT. IT also plans budgets based on the needs of the associated business units, which allows IT to more accurately account for costs associated to purely IT initiatives.

This model provides a balance between a true chargeback model and more traditional models of IT accounting.

## <a name="impact-of-cloud-accounting-models"></a>Impact of cloud accounting models

The choice of accounting models is crucial in system design. The choice of accounting model can affect subscription strategies, naming standards, tagging standards, and policy and blueprint designs.

After you've worked with the business to make decisions about a cloud accounting model and [global markets](./global-markets.md), you have enough information to [develop an Azure foundation](../ready/index.md).

> [!div class="nextstepaction"]
> [Develop an Azure foundation](../ready/index.md)
