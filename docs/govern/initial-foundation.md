---
title: Ustanów początkową podstawę ładu w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zacznij korzystać z ładu w chmurze, ustanawiając wstępną Fundację ładu Cloud.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3e1f2c1b54a55a740376ba1d1c45c13dc9e7e26d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026988"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Ustanów początkową podstawę ładu w chmurze

Opracowywanie zarządzania chmurą jest szerokim wysiłkiem. Istnieje trudne do osiągnięcia skuteczna równowaga między szybkością i kontrolą, szczególnie podczas wczesnych faz wdrożenia chmury. Wskazówki dotyczące ładu w strukturze wdrażania chmury pomagają zapewnić, że saldo jest realizowane przy użyciu podejścia Agile do wdrożenia.

Ten artykuł zawiera dwie opcje tworzenia początkowej podstawy dla zarządzania. Każda z tych opcji gwarantuje, że ograniczenia ładu mogą być skalowane i rozszerzane, gdy plan wdrożenia jest zaimplementowany i wymagania stają się bardziej jasno zdefiniowane. Domyślnie początkową podstawą jest założenie, że pozycja izoluje i kontroluje. Zawiera również więcej informacji na temat organizacji zasobów niż w przypadku zarządzania zasobami. Ten lekki punkt początkowy jest nazywany _minimalnym żywotnym produktem (MVP)_ dla zarządzania. Celem programu MVP jest zredukowanie przeszkód do ustanowienia początkowej pozycji zarządzania, a następnie umożliwienie szybkiego dojrzewania rozwiązania w celu rozwiązania różnych materialnych zagrożeń.

## <a name="already-using-the-cloud-adoption-framework"></a>Już korzystasz z platformy wdrażania chmury

Jeśli zostały przeprowadzone następujące czynności w ramach platformy wdrażania w chmurze, można już wdrożyć program ładu MVP. Wskazówki to podstawowy aspekt dowolnego modelu operacyjnego. Jest ona obecna w każdej fazie cyklu życia wdrożenia chmury. W związku z tym [Struktura wdrażania w chmurze](../index.md) zawiera wskazówki, które wprowadzają ładu do działań związanych z implementacją [planu wdrożenia chmury](../plan/index.md). Przykładem integracji z tym nadzorem jest użycie planów do wdrożenia co najmniej jednej strefy wyładunkowej znajdującej się w [gotowych](../ready/index.md) wskazówkach. Innym przykładem jest wskazówki dotyczące [skalowania subskrypcji](../ready/considerations/scaling-subscriptions.md). Jeśli wykonano dowolne z tych zaleceń, następujące sekcje MVP są po prostu przeglądem istniejących decyzji dotyczących wdrożenia. Po szybkim przeglądzie przejdź z wyprzedzeniem do [przedwcześnie rozwiązania do zarządzania początkowego i Zastosuj kontrolki najlepszych rozwiązań](./foundation-improvements.md).

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
                        <p>Przewodnik dla większości organizacji oparty na zalecanym modelu z dwoma subskrypcjami, przeznaczony dla wdrożeń w wielu regionach, które nie obejmują chmur publicznych i suwerennych/rządowych.</p>
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
> [Popraw początkową podstawę ładu](./foundation-improvements.md)
