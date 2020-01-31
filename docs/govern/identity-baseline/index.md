---
title: Omówienie dziedziny Punkt odniesienia obsługi tożsamości
description: Objaśnienia dotyczące dziedziny Punkt odniesienia obsługi tożsamości w odniesieniu do utrzymania ładu w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 1ac3041abc6e4721366f8270ce37d6bf6885b140
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806190"
---
# <a name="identity-baseline-discipline-overview"></a>Omówienie dziedziny Punkt odniesienia obsługi tożsamości

Punkt odniesienia obsługi tożsamości jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu ładu z przewodnika Cloud Adoption Framework](../index.md). Obsługa tożsamości jest coraz częściej traktowana jako główny obwód zabezpieczeń w chmurze, co stanowi odstępstwo od tradycyjnego modelu zabezpieczeń sieci. Usługi zarządzania tożsamościami zapewniają podstawowe mechanizmy obsługujące kontrolę dostępu i organizację w środowiskach IT, a dziedzina Punkt odniesienia obsługi tożsamości stanowi uzupełnienie [dziedziny Punkt odniesienia zabezpieczeń](../security-baseline/index.md) przez stałe stosowanie wymagań dotyczących uwierzytelniania i autoryzacji w projektach dotyczących wdrażania w chmurze.

> [!NOTE]
> Utrzymanie ładu punktu odniesienia obsługi tożsamości nie zastąpi istniejących zespołów, procesów i procedur IT, które umożliwiają w organizacji zabezpieczanie usług zarządzania tożsamościami i zarządzanie nimi. Głównym celem tej dziedziny jest zidentyfikowanie potencjalnych czynników ryzyka biznesowego powiązanych z obsługą tożsamości i dostarczenie personelowi IT odpowiedzialnemu za implementowanie, obsługę i działanie infrastruktury zarządzania tożsamościami wskazówek umożliwiających ograniczenie tego ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

W tej sekcji przewodnika Cloud Adoption Framework opisano model tworzenia dziedziny Punkt odniesienia obsługi tożsamości w ramach strategii utrzymania ładu w chmurze. Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie i dyskusje odpowiednich członków zespołów informatycznych odpowiedzialnych za implementowanie rozwiązań zarządzania tożsamościami w organizacji i zarządzanie nimi.

Jeśli Twoja organizacja nie ma własnych specjalistów zajmujących się punktem odniesienia obsługi tożsamości i zabezpieczeniami, należy w ramach tej dziedziny rozważyć zatrudnienie zewnętrznych konsultantów. Ponadto należy wziąć pod uwagę skorzystanie z [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services) — usług wdrażania w chmurze będących częścią programu [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) — lub innych zewnętrznych partnerów ds. wdrażania w chmurze, aby przedyskutować z nimi kwestie związane z tą dziedziną.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Punkt odniesienia obsługi tożsamości. Przykładowe instrukcje zasad można zobaczyć w artykule [Instrukcje zasad dziedziny Punkt odniesienia obsługi tożsamości](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

W poniższych sześciu krokach zamieszczono przykłady i potencjalne opcje, które należy wziąć pod uwagę podczas opracowywania zasad utrzymania ładu dziedziny Punkt odniesienia obsługi tożsamości. Każdy z tych kroków może stanowić punkt wyjścia do dyskusji w ramach zespołu ds. utrzymania ładu w chmurze oraz z zespołami informatycznymi w Twojej organizacji w celu opracowania zasad i procesów wymaganych do zarządzania czynnikami ryzyka powiązanymi z obsługą tożsamości.

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
                        <h3>Szablon dziedziny Punkt odniesienia obsługi tożsamości</h3>
                        <p class="x-hidden-focus">Pobierz szablon umożliwiający dokumentowanie dziedziny Punkt odniesienia obsługi tożsamości.</p>
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
                        <p class="x-hidden-focus">Poznaj przyczyny i czynniki ryzyka kojarzone zazwyczaj z dziedziną Punkt odniesienia obsługi tożsamości.</p>
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
                        <p class="x-hidden-focus">Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Punkt odniesienia obsługi tożsamości.</p>
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
                        <p class="x-hidden-focus">Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Punkt odniesienia obsługi tożsamości.</p>
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
                        <p class="x-hidden-focus">Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Punkt odniesienia obsługi tożsamości.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny [ryzyka biznesowego](./business-risks.md) w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)
