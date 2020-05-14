---
title: Omówienie dziedziny Punkt odniesienia zabezpieczeń
description: Zapoznaj się z podejściem do tworzenia dziedziny Punkt odniesienia zabezpieczeń w ramach strategii utrzymania ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 9c8bc1a9dd0c475a72db73ad032dabd1ff83f476
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219856"
---
# <a name="security-baseline-discipline-overview"></a>Omówienie dziedziny Punkt odniesienia zabezpieczeń

Punkt odniesienia zabezpieczeń jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu utrzymania ładu z przewodnika Cloud Adoption Framework](../index.md). Zabezpieczenia są składnikiem każdego wdrożenia IT, a chmura wprowadza unikatowe zagadnienia związane z bezpieczeństwem. Wiele firm podlega wymaganiom prawnym, dlatego ochrona poufnych danych stała się głównym priorytetem organizacji, która rozważa przekształcenie do chmury. Identyfikowanie potencjalnych zagrożeń w środowisku chmury oraz ustanawianie procesów i procedur umożliwiających eliminowanie tych zagrożeń powinno mieć priorytet dla każdego zespołu IT zajmującego się zabezpieczeniami lub cyberbezpieczeństwem. Dziedzina Punkt odniesienia zabezpieczeń gwarantuje, że wymagania techniczne i ograniczenia zabezpieczeń są spójnie stosowane w środowiskach w chmurze w miarę dojrzewania wymagań.

> [!NOTE]
> Dyscyplina Punkt odniesienia zabezpieczeń nie zastąpi istniejących zespołów, procesów i procedur IT, które umożliwiają w organizacji zabezpieczanie zasobów wdrożonych w organizacji. Najważniejszym zadaniem tej dziedziny jest identyfikowanie związanych z bezpieczeństwem czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za infrastrukturę zabezpieczeń wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

W tym artykule opisano metodę tworzenia dziedziny Punkt odniesienia zabezpieczeń w ramach strategii utrzymania ładu w chmurze. Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie odpowiednich członków zespołów IT i zespołów ds. zabezpieczeń oraz dyskusje z nimi. W szczególności dotyczy to liderów technicznych odpowiedzialnych za implementowanie usług obsługi sieci, szyfrowania i tożsamości.

Podejmowanie właściwych decyzji dotyczących zabezpieczeń ma kluczowe znaczenie, jeśli chcesz osiągnąć sukces podczas wdrożeń w chmurze i szerzej pojmowany sukces biznesowy. Jeśli Twoja organizacja nie ma własnych specjalistów zajmujących się cyberbezpieczeństwem, należy w ramach tej dziedziny rozważyć zatrudnienie zewnętrznych konsultantów ds. bezpieczeństwa. Ponadto należy wziąć pod uwagę skorzystanie z [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting) — usług wdrażania w chmurze będących częścią programu [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) — lub innych zewnętrznych ekspertów ds. wdrażania w chmurze, aby przedyskutować z nimi kwestie związane z tą dziedziną.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Punkt odniesienia zabezpieczeń. Przykładowe instrukcje zasad można zobaczyć w artykule [Instrukcje zasad dziedziny Punkt odniesienia zabezpieczeń](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

W poniższych sześciu krokach zamieszczono przykłady i potencjalne opcje, które należy wziąć pod uwagę podczas opracowywania dziedziny Punkt odniesienia zabezpieczeń. Każdy z tych kroków może stanowić punkt wyjścia do dyskusji w ramach zespołu ds. utrzymania ładu w chmurze oraz z zespołami biznesowymi, informatycznymi i zajmującymi się zabezpieczeniami w organizacji w celu opracowania zasad i procesów wymaganych do zarządzania czynnikami ryzyka powiązanymi z zabezpieczeniami.

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
                        <h3>Szablon dotyczący dziedziny Punkt odniesienia zabezpieczeń</h3>
                        <p class="x-hidden-focus">Pobierz szablon umożliwiający dokumentowanie dziedziny Punkt odniesienia zabezpieczeń.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
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
                        <p class="x-hidden-focus">Poznaj przyczyny i czynniki ryzyka kojarzone zazwyczaj z dziedziną Punkt odniesienia zabezpieczeń.</p>
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
                        <p class="x-hidden-focus">Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Punkt odniesienia zabezpieczeń.</p>
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
                        <p class="x-hidden-focus">Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Punkt odniesienia zabezpieczeń.</p>
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
                        <p class="x-hidden-focus">Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Punkt odniesienia zabezpieczeń.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny ryzyka biznesowego w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)
