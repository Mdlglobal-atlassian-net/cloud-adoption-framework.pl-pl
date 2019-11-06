---
title: Omówienie dziedziny Zarządzanie kosztami
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Objaśnienia dotyczące dziedziny Zarządzanie kosztami w odniesieniu do utrzymania ładu w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: ac6c3cb0a26cebf655a1161a3fd54197c795c283
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566426"
---
# <a name="cost-management-discipline-overview"></a>Omówienie dziedziny Zarządzanie kosztami

Zarządzanie kosztami jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu utrzymania ładu z przewodnika Cloud Adoption Framework](../index.md). Dla wielu klientów koszt utrzymania ładu stanowi główny problem podczas wdrażania technologii usług w chmurze. Potrzeby w zakresie równoważenia wydajności, tempo wdrażania i koszty usług w chmurze mogą być wyzwaniem. Jest to szczególnie istotne w czasie dużych przekształceń firmy obejmujących technologie usług w chmurze. W tej sekcji opisano metodę tworzenia dziedziny Zarządzanie kosztami w ramach strategii utrzymania ładu w chmurze.

> [!NOTE]
> Utrzymanie ładu dla dziedziny Zarządzanie kosztami nie zastępuje istniejących zespołów biznesowych, praktyk księgowych i procedur, które są zaangażowane w zarządzanie finansowe kosztami związanymi z infrastrukturą IT w organizacji. Najważniejszym zadaniem tej dziedziny jest identyfikowanie potencjalnych zagrożeń związanych z chmurą w odniesieniu do wydatków na infrastrukturę IT oraz przekazywanie wskazówek mających na celu ograniczenie ryzyka do zespołów biznesowych i informatycznych odpowiedzialnych za wdrażanie zasobów w chmurze i zarządzanie nimi.

Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie odpowiednich członków zespołów biznesowych i informatycznych oraz dyskusje z nimi. W szczególności dotyczy to liderów odpowiedzialnych za posiadanie obciążeń opartych na chmurze, zarządzanie nimi i płacenie za nie.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Zarządzanie kosztami. Aby wyświetlić przykładowe instrukcje zasad, zobacz artykuł [Instrukcje zasad dziedziny Zarządzanie kosztami](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

Sześć poniższych kroków ułatwi zdefiniowanie zasad utrzymania ładu umożliwiających kontrolowanie kosztów w środowisku.

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
                        <h3>Szablon dziedziny Zarządzanie kosztami</h3>
                        <p class="x-hidden-focus">Pobierz szablon umożliwiający dokumentowanie dziedziny Zarządzanie kosztami.</p>
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
                        <p class="x-hidden-focus">Poznaj przyczyny i zagrożenia skojarzone zazwyczaj z dziedziną Zarządzanie kosztami.</p>
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
                        <p class="x-hidden-focus">Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Zarządzanie kosztami.</p>
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
                        <p class="x-hidden-focus">Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Zarządzanie kosztami.</p>
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
                        <p class="x-hidden-focus">Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Zarządzanie kosztami.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny ryzyka biznesowego w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)

<!-- markdownlint-enable MD033 -->
