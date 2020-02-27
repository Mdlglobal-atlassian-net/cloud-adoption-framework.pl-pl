---
title: Pięć dziedzin nadzoru chmury
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o Cost Management, przyspieszeniu wdrażania, linii bazowej tożsamości, spójności zasobów i linii bazowej zabezpieczeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d50364a621e57b95e26f5686f4d470984530e161
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707683"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Pięć dziedzin nadzoru chmury

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Wszelkie zmiany procesów firmy lub platform technologicznych wprowadzają ryzyko. Zespoły nadzorujące chmur, których członkowie są czasami znane jako powiernika chmury, są zadaniem z ograniczeniami tego ryzyka i zapewnieniem minimalnego zakłócenia wdrażania lub wysiłków innowacji.<br/><br/>Model nadzoru struktury wdrażania chmury obejmuje te decyzje (bez względu na wybraną platformę chmury), koncentrując się na <a href="./corporate-policy.md">rozwoju zasad korporacyjnych</a> i <a href="#disciplines-of-cloud-governance">pięciu dyscyplinach zarządzania chmurą</a>. <a href="./guides/index.md">Przewodniki projektowe</a> z możliwością podejmowania działań pokazują ten model przy użyciu usług platformy Azure. Zapoznaj się z zasadami dotyczącymi modelu ładu Framework wdrażania w chmurze poniżej.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Rysunek 1 — Diagram zasad firmowych i pięć dyscyplin nadzoru chmurowego.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Dyscypliny zarządzania chmurą

W przypadku każdej platformy w chmurze istnieją typowe dyscypliny ładu, które ułatwiają informowanie zasad i wyrównanie łańcuchy narzędzi. Te dyscypliny przedstawiają decyzje dotyczące właściwego poziomu automatyzacji i egzekwowania zasad firmowych na platformach w chmurze.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Cost Management</h3>
                        <p>Koszt jest podstawowym problemem dla użytkowników w chmurze. Opracowywanie zasad kontroli kosztów dla wszystkich platform w chmurze.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Punkt odniesienia zabezpieczeń</h3>
                        <p>Zabezpieczenia to złożonego tematu, który jest unikatowy dla każdej firmy. Po ustaleniu wymagań dotyczących zabezpieczeń zasady zarządzania chmurą i egzekwowanie stosują te wymagania w konfiguracjach sieci, danych i zasobów.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Punkt odniesienia obsługi tożsamości</h3>
                        <p>Niespójności w zakresie wymagań dotyczących tożsamości mogą zwiększyć ryzyko naruszenia. Dyscyplina linii bazowej tożsamości polega na tym, że tożsamość jest spójna w ramach wysiłków związanych z wdrażaniem w chmurze.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Spójność zasobów</h3>
                        <p>Operacje w chmurze zależą od spójnej konfiguracji zasobów. Dzięki narzędziom ładu można spójnie konfigurować zasoby, aby zarządzać ryzykiem związanym z dołączaniem, dryfem, odnajdywaniem i odzyskiwaniem.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Przyspieszanie wdrażania</h3>
                        <p>Scentralizowanie, standaryzacja i spójność w podejścia do wdrażania i konfigurowania usprawniania praktyk ładu. Po podaniu przez narzędzia do zarządzania oparte na chmurze tworzą one współczynnik chmury, który może przyspieszyć działania wdrożenia.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
