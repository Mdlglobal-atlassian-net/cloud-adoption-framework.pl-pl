---
title: Ustanów początkową podstawę ładu w chmurze
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby rozpocząć pracę z zasadami zarządzania chmurą, ustanawiając początkową podstawę zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 7ce353a03c57e89800d65edc5cdfbdec8c53d092
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218496"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Ustanów początkową podstawę ładu w chmurze

Opracowywanie zarządzania chmurą jest szerokim wysiłkiem. Istnieje trudne do osiągnięcia skuteczna równowaga między szybkością i kontrolą, szczególnie podczas wykonywania wczesnych metodologii w ramach wdrożenia chmury. Wskazówki dotyczące ładu w strukturze wdrażania chmury pomagają zapewnić, że saldo jest realizowane przy użyciu podejścia Agile do wdrożenia.

Ten artykuł zawiera dwie opcje tworzenia początkowej podstawy dla zarządzania. Każda z tych opcji gwarantuje, że ograniczenia ładu mogą być skalowane i rozszerzane, gdy plan wdrożenia jest zaimplementowany i wymagania stają się bardziej jasno zdefiniowane. Domyślnie początkową podstawą jest założenie, że pozycja izoluje i kontroluje. Zawiera również więcej informacji na temat organizacji zasobów niż w przypadku zarządzania zasobami. Ten lekki punkt początkowy jest nazywany _minimalnym żywotnym produktem (MVP)_ dla zarządzania. Celem programu MVP jest zredukowanie przeszkód do ustanowienia początkowej pozycji zarządzania, a następnie umożliwienie szybkiego dojrzewania rozwiązania w celu rozwiązania różnych materialnych zagrożeń.

## <a name="already-using-the-cloud-adoption-framework"></a>Już korzystasz z platformy wdrażania chmury

Jeśli zostały przeprowadzone następujące czynności w ramach platformy wdrażania w chmurze, być może już wdrożono program ładu MVP. Zarządzanie to podstawowy aspekt dowolnego modelu operacyjnego. Jest ona obecna w każdej metodologii cyklu życia wdrożenia chmury. W związku z tym [Struktura wdrażania w chmurze](../index.yml) zawiera wskazówki, które wprowadzają ładu do działań związanych z implementacją [planu wdrożenia chmury](../plan/index.md). Przykładem integracji ładu jest użycie planów do wdrożenia co najmniej jednej strefy wyładunkowej, która znajduje się w gotowych wskazówkach dotyczących [metodologii](../ready/index.md) . Innym przykładem jest wskazówki dotyczące [skalowania subskrypcji](../ready/azure-best-practices/scale-subscriptions.md). Jeśli wykonano dowolne z tych zaleceń, następujące sekcje MVP są po prostu przeglądem istniejących decyzji dotyczących wdrożenia. Po szybkim przeglądzie przejdź z wyprzedzeniem do [przedwcześnie rozwiązania do zarządzania początkowego i Zastosuj kontrolki najlepszych rozwiązań](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Ustanów początkową podstawę ładu

Poniżej przedstawiono dwa różne przykłady początkowych podstaw ładu (nazywanych również ładu MVP) w celu zastosowania solidnej podstawy do zarządzania nowymi lub istniejącymi wdrożeniami. Wybierz MVP, który najlepiej odpowiada potrzebom firmy, aby rozpocząć pracę:

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./guides/standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Standardowy przewodnik dotyczący ładu</h3>
                        <p>Przewodnik dla większości organizacji oparty na zalecanym początkowym modelu z dwiema subskrypcjami, przeznaczonym do wdrożeń w wielu regionach, ale nie w przypadku chmur publicznych i suwerennych/rządowych.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./guides/complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Przewodnik dotyczący ładu dla przedsiębiorstw złożonych</h3>
                        <p>Przewodnik dla przedsiębiorstw, które są zarządzane przez wiele niezależnych jednostek biznesowych IT lub obejmują chmurę publiczną i suwerenną/rządową.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

Po utworzeniu podstawy ładu należy zastosować odpowiednie zalecenia, aby poprawić rozwiązanie i chronić je przed niematerialnymi zagrożeniami.

> [!div class="nextstepaction"]
> [Udoskonalanie początkowych podstaw ładu](./foundation-improvements.md)
