---
title: Omówienie dziedziny Przyspieszanie wdrażania
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Objaśnienia dotyczące dziedziny Przyspieszanie wdrażania w odniesieniu do ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 55dc7554e72f5ca1e2a19a29cf93f8b075b93c9b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025884"
---
# <a name="deployment-acceleration-discipline-overview"></a>Omówienie dziedziny Przyspieszanie wdrażania

Przyspieszenie wdrażania jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu ładu z przewodnika Cloud Adoption Framework](../index.md). Ta dziedzina koncentruje się na sposobach ustanawiania zasad umożliwiających nadzorowanie konfigurowania lub wdrażania zasobów. Przyspieszanie wdrażania, jedna z pięciu dziedzin utrzymania ładu w chmurze, obejmuje wdrażanie, dostosowywanie konfiguracji oraz możliwość ponownego wykorzystania skryptów. Może to się odbywać za pośrednictwem działań ręcznych lub w pełni zautomatyzowanych działań metodyki DevOps. W obu przypadkach zasady pozostają w dużym stopniu takie same. Gdy ta dziedzina dojrzeje, zespół ds. utrzymania ładu w chmurze może być partnerem w metodyce DevOps i strategiach wdrażania, przyspieszając wdrożenia i usuwając bariery w celu wdrożenia chmury dzięki zastosowaniu zasobów do ponownego wykorzystania.

W tym artykule opisano proces przyspieszania wdrażania występujący w firmie na etapach planowania, kompilowania, wdrażania i obsługi implementowania rozwiązania w chmurze. Żaden pojedynczy dokument nie może opisać wszystkich wymagań wszystkich firm. W związku z tym każda sekcja tego artykułu przedstawia sugerowane minimum i możliwe działania. Celem tych działań jest pomoc w utworzeniu [specjalisty od zasad](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy), ale także ustanowienie struktury na potrzeby ulepszania [zasad przyrostowych](../policy-compliance/index.md#incremental-policy-growth). Zespół ds. utrzymania ładu w chmurze powinien zdecydować, jak dużo zainwestować w te działania, aby poprawić dziedzinę Przyspieszanie wdrażania.

> [!NOTE]
> Dziedzina Przyspieszanie wdrażania nie zastępuje istniejących zespołów IT, procesów i procedur, które umożliwiają organizacji skuteczne wdrażanie i konfigurowanie zasobów opartych na chmurze. Najważniejszym zadaniem tej dziedziny jest identyfikowanie potencjalnych czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za zarządzanie zasobami w chmurze wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie odpowiednich członków zespołów biznesowych i informatycznych oraz dyskusje z nimi. W szczególności dotyczy to liderów odpowiedzialnych za wdrażanie i konfigurowanie obciążeń opartych na chmurze.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Przyspieszanie wdrażania. Aby wyświetlić przykładowe instrukcje zasad, zobacz artykuł [Instrukcje zasad dziedziny Przyspieszanie wdrażania](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="developing-deployment-acceleration-governance-policy-statements"></a>Tworzenie instrukcji zasad utrzymania ładu dla dziedziny Przyspieszanie wdrażania

Sześć poniższych kroków pomoże określić zasady utrzymania ładu umożliwiające kontrolę wdrażania i konfigurowania zasobów w środowisku chmury.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Szablon dziedziny Przyspieszanie wdrażania</h3>
                        <p class="x-hidden-focus">Pobierz szablon umożliwiający dokumentowanie dziedziny Przyspieszanie wdrażania</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Rodzaje ryzyka biznesowego</h3>
                        <p class="x-hidden-focus">Poznaj przyczyny i zagrożenia skojarzone zazwyczaj z dziedziną Przyspieszanie wdrażania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Wskaźniki i metryki</h3>
                        <p class="x-hidden-focus">Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Przyspieszanie wdrażania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Procesy zapewniania zgodności zasad</h3>
                        <p class="x-hidden-focus">Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Przyspieszanie wdrażania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Dojrzałość</h3>
                        <p class="x-hidden-focus">Dostosowywanie dojrzałości dziedziny Zarządzanie chmurą do etapów wdrażania w chmurze.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Łańcuch narzędzi</h3>
                        <p class="x-hidden-focus">Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Przyspieszanie wdrażania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny [ryzyka biznesowego](./business-risks.md) w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)

<!-- markdownlint-enable MD033 -->
