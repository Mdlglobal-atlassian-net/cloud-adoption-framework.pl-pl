---
title: Czym jest księgowość w chmurze?
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć typowe modele ewidencjonowania aktywności w chmurze dla tego rozwiązania podczas rozpoczęcia podróży migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 69f92ffaeb30b59bfa8ac2aeaea9aaad02e9aaeb
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216235"
---
<!-- cSpell:ignore CIOs -->

<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>Czym jest księgowość w chmurze?

Chmura zmienia sposób kont IT, zgodnie z opisem w temacie [Tworzenie modelu finansowego na potrzeby transformacji w chmurze](./financial-models.md). Różne modele ewidencjonowania aktywności IT są znacznie łatwiejsze do obsługi ze względu na sposób przydzielania przez chmurę kosztów. Dlatego ważne jest, aby zrozumieć, jak uwzględnić koszty związane z chmurą przed rozpoczęciem podróży w chmurze. W tym artykule opisano najbardziej typowe modele ewidencjonowania aktywności w chmurze.

## <a name="traditional-it-accounting-cost-center-model"></a>Tradycyjne ewidencjonowanie aktywności IT (model centrum kosztów)

Często warto rozważyć przeanalizowanie centrum kosztów. W tradycyjnym modelu księgowości IT konsoliduje możliwości zakupu dla wszystkich zasobów IT. Jak wskazano w artykule [Modele finansowe](./financial-models.md) , kupowanie może obejmować licencje na oprogramowanie, cykliczne opłaty za Licencjonowanie programu CRM, zakup pulpitów pracowników i inne duże koszty.

Gdy program służy jako centrum kosztów, postrzegana wartość jest w dużym stopniu wyświetlana przez soczewkę zarządzania zaopatrzeniem. To postrzeganie utrudnia odwiedzanie przez zarząd lub inne kierownictwo w zrozumieniu prawdziwej wartości. Koszty zaopatrzenia umożliwiają pochylenie tego widoku poprzez zmniejszenie wszelkich innych wartości dodanych przez organizację. Ten widok wyjaśnia, dlaczego często jest on podzielony na obowiązki dyrektora finansowego lub dyrektora ds. operacyjnych. To postrzeganie jest ograniczone i może być krótkie.

## <a name="central-it-accounting-profit-center-model"></a>Centralne ewidencjonowanie aktywności IT (model centrum zysków)

Aby przezwyciężyć widok centrum kosztów, niektóre dyrektorzy działu informatyki wybrały dla scentralizowanego modelu INFORMATYCZNego księgowości. W modelu tego typu jest on traktowany jak konkurencyjna jednostka biznesowa i element równorzędny do tworzenia przychodów jednostek gospodarczych. W niektórych przypadkach ten model może być całkowicie logiczny. Na przykład niektóre organizacje mają profesjonalny dział usług IT generujący strumień przychodów. Często scentralizowane modele IT nie generują znaczących przychodów, co utrudnia wyjustowanie modelu.

Niezależnie od modelu przychodów scentralizowane modele ewidencjonowania aktywności IT są unikatowe, ponieważ w jaki sposób dział IT jest odpowiedzialny za koszty. W tradycyjnym modelu IT zespół IT rejestruje koszty i płaci te koszty z udostępnionych funduszy, takich jak operacje i konserwacja (O&M) lub dedykowane konto zysków i strat (P&L).

W centralnym modelu księgowości IT zespół IT oznacza usługi świadczone na potrzeby obciążania, zarządzania i innych szacowanych kosztów. Następnie należy rozrachunkować konkurencyjne jednostki biznesowe dla oznaczonych usług. W tym modelu CIO oczekuje się zarządzania P&L związanego z sprzedażą tych usług. Pozwala to na tworzenie niepełnych kosztów IT i rywalizacji między centralnym działem IT i jednostkami biznesowymi, szczególnie w przypadku konieczności ponoszenia kosztów lub braku zgody na umowy SLA. W miarę możliwości technologii lub zmiany rynkowej każda nowa technologia spowodowałaby zakłócenie w centralnej&L, co utrudnia transformację.

## <a name="chargeback"></a>Obciążenia zwrotnego

Jednym z typowych pierwszych kroków w przypadku zmiany jego reputacji jako centrum kosztów jest implementacja obciążenia zwrotnego modelu ewidencjonowania aktywności. Ten model jest szczególnie powszechny w mniejszych przedsiębiorstwach lub wysoce wydajnych organizacjach IT. W modelu obciążenia zwrotnego wszystkie koszty działu IT powiązane z konkretną jednostką biznesową są traktowane jak koszty operacyjne w budżecie jednostki biznesowej. Ta metoda ogranicza skumulowany wpływ na IT, co pozwala na bardziej jasne zwiększenie wartości biznesowej.

W starszym modelu lokalnym obciążenia zwrotnego jest trudne do zrealizowania, ponieważ ktoś nadal musi przenieść duże wydatki i amortyzację kapitału. Ciągła konwersja z wydatków inwestycyjnych do kosztów operacyjnych związanych z użyciem jest trudną eksploatacją księgową. Ten problem jest głównym powodem tworzenia tradycyjnego modelu księgowości IT i centralnego modelu ewidencjonowania aktywności IT. Model wydatków operacyjnych z rachunku kosztów w chmurze jest prawie wymagany, jeśli chcesz efektywnie dostarczyć model obciążenia zwrotnego.

Ale nie należy implementować tego modelu bez uwzględnienia konsekwencji. Poniżej przedstawiono kilka konsekwencji, które są unikatowe dla modelu obciążenia zwrotnego:

- Obciążenia zwrotnego skutkuje ogromną redukcją ogólnego budżetu IT. W przypadku organizacji IT, które są niewydajne lub wymagają szerokiej złożoności w zakresie operacji lub konserwacji, ten model może ujawnić te wydatki w złej kondycji.
- Utrata kontroli jest powszechną konsekwencją. W wysoce politycznych środowiskach obciążenia zwrotnego może skutkować utratą kontroli i personelem przydzielonym do firmy. Może to spowodować znaczne zwiększenie wydajności i ograniczyć możliwość spójnego spełnienia wymagań umowy SLA lub projektu.
- Jest to kolejna wspólna konsekwencja dla usług udostępnionych. Jeśli organizacja zwiększyła się w drodze pozyskiwania i pełni rolę techniczną w związku z tym, prawdopodobnie należy zachować wysoką część usług udostępnionych, aby wszystkie systemy działały efektywnie.

Przekształcenia w chmurze obejmują rozwiązania do tych i inne konsekwencje związane z modelem obciążenia zwrotnego. Każdy z tych rozwiązań obejmuje implementację i koszty operacyjne. CIO i dyrektor finansowy powinni starannie zważyć specjalistów i wady modelu obciążenia zwrotnego przed uwzględnieniem ich.

## <a name="showback-or-awareness-back"></a>Przewidywanych kosztów lub świadomość

W przypadku większych przedsiębiorstw model przewidywanych kosztów lub z obsługą świadomości jest bezpieczniejszym pierwszym krokiem przejścia z centrum kosztów do centrum wartości. Ten model nie ma wpływu na księgowość finansową. W rzeczywistości P&LS każdej organizacji nie zmieni się. Największe przesunięcia jest w sposób myślenia i świadomości. W modelu "przewidywanych kosztów" lub "rozpoznawanie świadomości" zarządza scentralizowaną, skonsolidowaną mocą zakupu jako agentem dla firmy. W raportach z powrotem do firmy dział IT ponosi wszelkie bezpośrednie koszty do odpowiedniej jednostki biznesowej, co zmniejsza postrzegany budżet bezpośrednio przez dział IT. Planuje również budżety na podstawie potrzeb skojarzonych jednostek biznesowych, co pozwala na dokładniejsze uwzględnienie kosztów związanych z czystą inicjatywy IT.

Ten model zapewnia równowagę między rzeczywistym modelem obciążenia zwrotnego i bardziej tradycyjnymi modelami ewidencjonowania aktywności IT.

## <a name="impact-of-cloud-accounting-models"></a>Wpływ modeli ewidencjonowania aktywności w chmurze

Wybór modeli ewidencjonowania aktywności jest decydujący w projekcie systemu. Wybór modelu ewidencjonowania aktywności może mieć wpływ na strategie subskrypcji, standardy nazewnictwa, standardy tagowania oraz projekty zasad i planów.

Po przeprowadzeniu pracy z firmą w celu podejmowania decyzji dotyczących modelu ewidencjonowania aktywności w chmurze i [rynków globalnych](./global-markets.md)masz wystarczającą ilość informacji, aby [wybrać pierwszy projekt](./first-adoption-project.md)wdrożenia w chmurze.

> [!div class="nextstepaction"]
> [Wybierz swój pierwszy projekt wdrażania w chmurze](./first-adoption-project.md)
