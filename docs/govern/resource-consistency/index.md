---
title: Omówienie dziedziny Spójność zasobów
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Omówienie dziedziny Spójność zasobów
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 5e7da35bb2b88c8f24abf09f8d3d2a708f732c1c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222090"
---
# <a name="resource-consistency-discipline-overview"></a>Omówienie dziedziny Spójność zasobów

Spójność zasobów jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu utrzymania ładu opisanego w przewodniku Cloud Adoption Framework](../index.md). Ta dziedzina koncentruje się na sposobach opracowywania zasad związanych z operacyjnym zarządzaniem środowiskiem, aplikacją lub obciążeniem. Zespoły ds. operacji informatycznych często umożliwiają monitorowanie wydajności aplikacji, obciążeń i zasobów. Często wykonują one również zadania umożliwiające spełnienia wymagań dotyczących skali, korygują naruszenia Umów dotyczących poziomu usług (SLA) i proaktywnie unikają naruszeń umów SLA dotyczących wydajności za pomocą zautomatyzowanych rozwiązań. Z pięciu dziedzin utrzymania ładu w chmurze Spójność zasobów jest dziedziną, która gwarantuje, że zasoby są spójnie konfigurowane w taki sposób, że można je wykryć za pomocą operacji informatycznych, są uwzględnione w rozwiązaniach w zakresie odzyskiwania i mogą być dołączone do procesów powtarzalnych operacji.

> [!NOTE]
> Ład dotyczący spójności zasobów nie zastępuje istniejących zespołów IT, procesów i procedur, które umożliwiają organizacji skuteczne zarządzanie zasobami opartymi na chmurze. Najważniejszym zadaniem tej dziedziny jest identyfikowanie potencjalnych czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za zarządzanie zasobami w chmurze wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

W tej sekcji przewodnika Cloud Adoption Framework opisano sposób opracowywania dziedziny Spójność zasobów w ramach strategii utrzymania ładu w chmurze. Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie i dyskusje odpowiednich członków zespołów informatycznych odpowiedzialnych za implementowanie rozwiązań dotyczących spójności zasobów w organizacji i zarządzanie nimi.

Jeśli Twoja organizacja nie ma własnych specjalistów zajmujących się strategiami spójności zasobów, należy w ramach tej dziedziny rozważyć zatrudnienie zewnętrznych konsultantów. Ponadto należy wziąć pod uwagę skorzystanie z [Microsoft Consulting Services](https://www.microsoft.com/enterprise/services) — usług wdrażania w chmurze będących częścią programu [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) — lub innych zewnętrznych ekspertów ds. wdrażania w chmurze, aby przedyskutować z nimi kwestie związane z jak najlepszym organizowaniem, śledzeniem i optymalizowaniem zasobów opartych na chmurze.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Spójność zasobów. Przykładowe instrukcje zasad można zobaczyć w artykule [Instrukcje zasad dziedziny Spójność zasobów](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="developing-resource-consistency-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu dziedziny Spójność zasobów

W poniższych sześciu krokach zamieszczono przykłady i potencjalne opcje, które należy wziąć pod uwagę podczas opracowywania zasad utrzymania ładu dziedziny Spójność zasobów. Każdy z tych kroków może stanowić punkt wyjścia do dyskusji w ramach zespołu ds. utrzymania ładu w chmurze oraz z zespołami informatycznymi w Twojej organizacji w celu opracowania zasad i procesów wymaganych do zarządzania czynnikami ryzyka powiązanymi ze spójnością zasobów.

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
                        <h3>Szablon dziedziny Spójność zasobów</h3>
                        <p class="x-hidden-focus">Pobierz szablon umożliwiający dokumentowanie dziedziny Spójność zasobów.</p>
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
                        <p class="x-hidden-focus">Poznaj przyczyny i czynniki ryzyka kojarzone zazwyczaj z dziedziną Spójność zasobów.</p>
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
                        <p class="x-hidden-focus">Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Spójność zasobów.</p>
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
                        <p class="x-hidden-focus">Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Spójność zasobów.</p>
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
                        <p class="x-hidden-focus">Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Spójność zasobów.</p>
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
