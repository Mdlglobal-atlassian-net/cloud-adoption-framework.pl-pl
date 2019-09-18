---
title: Ład w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure
description: Uzyskaj informacje o ładzie w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 899306c60be3750cd6165763a63d1d5b1f5eb0a6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026326"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Ład w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure

Chmura tworzy nowe paradygmaty dotyczące technologii, które obsługują firmy. Te nowe paradygmaty zmieniają też sposób stosowania tych technologii, zarządzania nimi i nadzorowania ich. Kiedy całe centra danych można praktycznie zniszczyć, a następnie utworzyć ponownie za pomocą jednego wiersza kodu wykonanego z poziomu nienadzorowanego procesu, oznacza to, że należy przemyśleć tradycyjne podejścia. Jest to szczególnie istotne w przypadku ładu.

## <a name="get-started-with-cloud-governance"></a>Wprowadzenie do ładu w chmurze

Nadzór nad ładem w chmurze jest procesem iteracyjnym. W przypadku organizacji z istniejącymi zasadami regulującymi lokalne środowiska IT ład chmury powinien uzupełniać te zasady. Jednak poziom integracji zasad firmowych między środowiskiem lokalnym i chmurą będzie różny w zależności od dojrzałości ładu chmury i majątku cyfrowego w chmurze. Z upływem czasu majątek w chmurze będzie się rozwijać, a wraz z nim zasady i procesy dotyczące ładu chmury. Poniższe ćwiczenia ułatwiają rozpoczęcie tworzenia początkowych podstaw ładu.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./methodology.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Metodologia</h3>
Zbierz podstawową wiedzę na temat metodologii zapewniania ładu w chmurze w ramach przewodnika Cloud Adoption Framework i zacznij myśleć o stanie końcowym.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./benchmark.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Punkt odniesienia</h3>
Oceń stan bieżący i stan przyszły w celu ustalenia wizji na potrzeby stosowania struktury.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./initial-foundation.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Początkowe podstawy ładu</h3>
Rozpocznij stosowanie nadzoru nad ładem, używając małego, łatwego w implementacji zestawu narzędzi do nadzoru. Te początkowe podstawy ładu są nazywane minimalną konieczną funkcjonalnością (MVP).
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./foundation-improvements.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Udoskonalanie początkowych podstaw ładu</h3>
W trakcie realizacji planu wdrażania chmury iteracyjnie dodawaj mechanizmy kontroli ładu w celu obsługi pojawiających się czynników ryzyka, zbliżając się do stanu końcowego.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="objective-of-this-content"></a>Cel tej zawartości

Wskazówki zawarte w tej sekcji przewodnika Cloud Adoption Framework służą dwóm celom:

- Podanie przykładów praktycznych przewodników dotyczących ładu, które reprezentują typowe doświadczenia klientów. Każdy przykład obejmuje zagadnienia związane z ryzykiem biznesowym, zasadami firmowymi umożliwiającymi ograniczenie ryzyka oraz wskazówki dotyczące projektu w celu implementacji rozwiązań technicznych. Z konieczności wskazówki dotyczące projektu są specyficzne dla platformy Azure. Pozostałą zawartość tych przewodników można stosować w podejściach niezależnych od chmury lub wielochmurowych.
- Pomoc w utworzeniu spersonalizowanych rozwiązań ładu spełniających różne potrzeby biznesowe. Te potrzeby obejmują utrzymanie ładu w wielu chmurach publicznych za pośrednictwem szczegółowych wskazówek dotyczących opracowywania zasad firmowych, procesów i narzędzi.

Ta zawartość jest przeznaczona dla zespołu ds. utrzymania ładu w chmurze. Jest również istotna dla architektów chmury, którzy muszą rozwinąć solidne podstawowe umiejętności z zakresu ładu w chmurze.

## <a name="intended-audience"></a>Docelowi odbiorcy

Zawartość przewodnika Cloud Adoption Framework dotyczy działalności biznesowej, technologii i kultury przedsiębiorstw. Ta sekcja przewodnika Cloud Adoption Framework dotyczy w szczególności zespołów ds. zabezpieczeń IT, zapewniania ładu w zasobach IT, finansów, liderów biznesowych, sieci, tożsamości i wdrożenia chmury. Różnorodne zależności między tym personelem wymagają od architektów chmury korzystających z tego przewodnika zastosowania podejścia ułatwiającego. Pomoc tym zespołom może być wysiłkiem jednorazowym. W niektórych przypadkach interakcje z innym personelem będą długotrwałe.

Architekt chmury pełni rolę lidera myśli i osoby ułatwiającej kontakt między tymi odbiorcami. Zawartość tej kolekcji przewodników ma pomóc architektowi chmury w ułatwieniu odpowiednich konwersacji z odpowiednimi odbiorcami, aby umożliwić podjęcie koniecznych decyzji. Transformacja firmy, która jest napędzana i obsługiwana przez chmurę, zależy od tego, czy architekt chmury pomoże w podejmowaniu decyzji w zakresie działalności biznesowej i IT.

**Specjalizacja architekta chmury w tej sekcji:** Każda sekcja przewodnika Cloud Adoption Framework reprezentuje różną specjalizację lub wariant roli architekta chmury. Ta sekcja przewodnika Cloud Adoption Framework jest przeznaczona dla architektów chmury pasjonujących się unikaniem lub ograniczaniem ryzyka technicznego. Niektórzy dostawcy chmury nazywają tych specjalistów *strażnikami chmury*, my jednak wolimy określenie *opiekunowie chmury* lub zbiorczo *zespół ds. utrzymania ładu w chmurze*. Artykuły dotyczące każdego praktycznego przewodnika dotyczącego ładu pokazują, jak skład i rola zespołu ds. utrzymania ładu w chmurze może zmieniać się wraz z upływem czasu.

## <a name="use-this-guide"></a>Korzystanie z tego przewodnika

Jeśli chcesz postępować zgodnie z tym przewodnikiem od początku do końca, ta zawartość pomoże w opracowaniu solidnej strategii utrzymania ładu w chmurze równolegle do implementacji chmury. Wskazówki przeprowadzą Cię przez teorię i implementację takiej strategii.

Aby zapoznać się z przyspieszonym kursem teoretycznym i uzyskać szybki dostęp do implementacji platformy Azure, zacznij od [przeglądu przewodników dotyczących ładu](./guides/index.md). Dzięki tym wskazówkom możesz zacząć od czegoś małego i iteracyjnie rozwijać swoje potrzeby w zakresie utrzymania ładu równolegle do prac nad wdrożeniem chmury.

## <a name="next-steps"></a>Następne kroki

Zbierz podstawową wiedzę na temat metodologii zapewniania ładu w chmurze w ramach przewodnika Cloud Adoption Framework.

> [!div class="nextstepaction"]
> [Zrozumienie metodologii](./methodology.md)
