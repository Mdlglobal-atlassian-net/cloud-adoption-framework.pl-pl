---
title: Zarządzanie w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zarządzanie w chmurze w przewodniku Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: operate
layout: LandingPage
ms.openlocfilehash: 5a53b72747d20e8b7b2d3ca25a6ffc29b46e1203
ms.sourcegitcommit: 74c1eb00a3bfad1b24f43e75ae0340688e7aec48
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/28/2019
ms.locfileid: "72979891"
---
# <a name="cloud-management-in-the-cloud-adoption-framework"></a>Zarządzanie w chmurze w przewodniku Cloud Adoption Framework

Realizacja [strategii chmury](../strategy/index.md) wymaga starannego planowania, przygotowania i wdrożenia. Ale to ciągłe działanie zasobów cyfrowych daje konkretne wyniki biznesowe. Bez planu zapewniającego niezawodne i właściwie zarządzanie rozwiązaniami w chmurze wszelkie wysiłki przyniosą niewielkie rezultaty. Poniższe ćwiczenia pomagają opracować metody biznesowe i techniczne konieczne do zapewnienia zarządzania w chmurze, które wspomaga działania operacyjne.

## <a name="getting-started"></a>Wprowadzenie

Aby przygotować się na tę fazę cyklu wdrażania chmury, zalecane są następujące ćwiczenia:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-management-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Ustalenie planu bazowego zarządzania</h3>
Zdefiniuj sposób klasyfikowania elementów o krytycznym znaczeniu, narzędzia do zarządzania w chmurze i procesy wymagane do realizacji minimalnego zobowiązania w zarządzaniu operacjami.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./considerations/business-alignment.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Zdefiniowanie zobowiązań biznesowych</h3>
Udokumentuj obsługiwane obciążenia, aby ustalić zobowiązania operacyjne zgodne z potrzebami firmy oraz inwestycje w zarządzanie w chmurze dla każdego obciążenia.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./best-practices.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Rozwinięcie planu bazowego zarządzania</h3>
Na podstawie zobowiązań biznesowych i decyzji operacyjnych wykorzystaj dołączone najlepsze rozwiązania, aby wdrożyć wymagane narzędzia do zarządzania w chmurze.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./design-principles.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Zaawansowane operacje i zasady projektowania</h3>
Platformy lub obciążenia, które wymagają wyższego poziomu zobowiązania biznesowego, mogą wymagać bardziej szczegółowego przeglądu architektury w celu zapewnienia odporności i niezawodności.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="scalable-cloud-management-methodology"></a>Skalowalna metodologia zarządzania chmurą

Poprzednie kroki określają praktyczne sposoby realizacji metodologii zarządzania przedstawionej w przewodniku Cloud Adoption Framework.

![Metodologia zarządzania w przewodniku Cloud Adoption Framework](../_images/manage/caf-manage.png)

## <a name="creating-a-balanced-cloud-portfolio"></a>Tworzenie zrównoważonego portfolio chmury

Jak opisano w artykule dotyczącym [spójności biznesowej](./considerations/business-alignment.md), nie wszystkie obciążenia są krytyczne dla działania firmy. Każdy portfel obejmuje potrzeby zarządzania operacyjnego na różnym poziomie. Działania związane z zachowaniem spójności biznesowej pomagają określić wpływ na firmę i negocjować koszty zarządzania z firmą, aby zagwarantować najlepsze procesy i narzędzia do zarządzania operacyjnego.

## <a name="objective-of-this-content"></a>Cel tej zawartości

Wskazówki zawarte w tej sekcji przewodnika Cloud Adoption Framework służą dwóm celom:

- Przedstawiają praktyczne metody zarządzania operacyjnego, które odzwierciedlają typowe doświadczenia klientów.
- Pomagają utworzyć spersonalizowane rozwiązania do zarządzania na podstawie zobowiązań biznesowych.

Ta zawartość jest przeznaczona dla zespołu ds. operacji w chmurze. Jest również istotna dla architektów chmury, którzy muszą rozwinąć solidne podstawowe umiejętności z zakresu operacji w chmurze lub zasad projektowania w chmurze.

## <a name="intended-audience"></a>Docelowi odbiorcy

Zawartość przewodnika Cloud Adoption Framework dotyczy działalności biznesowej, technologii i kultury przedsiębiorstw. Ta sekcja przewodnika Cloud Adoption Framework dotyczy w szczególności zespołów ds. operacji IT, zapewniania ładu w zasobach IT, finansów, liderów biznesowych, sieci, tożsamości i wdrażania chmury. Różnorodne zależności między tym personelem wymagają od architektów chmury korzystających z tego przewodnika zastosowania podejścia ułatwiającego. Pomoc tym zespołom rzadko jest wysiłkiem jednorazowym.

Architekt chmury pełni rolę lidera myśli i osoby ułatwiającej kontakt między tymi odbiorcami. Zawartość tej kolekcji przewodników ma pomóc architektowi chmury w ułatwieniu odpowiednich konwersacji z odpowiednimi odbiorcami, aby umożliwić podjęcie koniecznych decyzji. Transformacja firmy, która jest napędzana i obsługiwana przez chmurę, zależy od tego, czy architekt chmury pomoże w podejmowaniu decyzji w zakresie działalności biznesowej i IT.

**Specjalizacja architekta chmury w tej sekcji:** Każda sekcja przewodnika Cloud Adoption Framework reprezentuje różną specjalizację lub wariant roli architekta chmury. Ta sekcja przewodnika Cloud Adoption Framework jest przeznaczona dla architektów chmury pasjonujących się operacjami i zarządzaniem rozwiązaniami wdrożeniowymi. W ramach tej struktury ci specjaliści są często nazywani specjalistami ds. *operacji w chmurze* lub zbiorczo *zespołem ds. operacji w chmurze*.

## <a name="use-this-guide"></a>Korzystanie z tego przewodnika

Jeśli chcesz postępować zgodnie z tym przewodnikiem od początku do końca, ta zawartość pomoże w opracowaniu solidnej strategii operacji w chmurze. Wskazówki przeprowadzą Cię przez teorię i implementację takiej strategii.

<!-- For a crash course on the theory and quick access to Azure implementation, get started with the [governance guides overview](./guide/index.md). Using this guidance, you can start small and iteratively improve your governance needs in parallel with cloud adoption efforts. -->

## <a name="next-steps"></a>Następne kroki

Zastosuj tę metodologię, aby opracować czytelne zobowiązania biznesowe.

> [!div class="nextstepaction"]
> [Opracowywanie czytelnych zobowiązań biznesowych](./considerations/business-alignment.md)
