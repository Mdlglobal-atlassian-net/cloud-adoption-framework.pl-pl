---
title: Włącz pomyślne klienta w ramach dowolnej podróży w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Włącz pomyślne klienta w ramach dowolnej podróży w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: f36e524fea15df572df8ef74c6b5c81f5fa08932
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829243"
---
# <a name="enable-success-across-any-cloud-adoption-journey"></a>Włącz sukces w ramach dowolnej podróży w chmurze

Platforma wdrażania Microsoft Cloud dla platformy Azure jest świadczona bezpłatnie narzędziem samoobsługowym, które ułatwia czytelnikom korzystanie z różnych wysiłków związanych z wdrażaniem w chmurze. Celem tej zawartości jest ułatwienie klientom osiągnięcia celów firmy, które można włączyć na platformie Azure. Jednakże ta zawartość odnosi się również do tego, że czytelnik może zająć się wyzwaniami biznesowymi, kulturami lub technicznymi, które mogą mieć charakter szeroki i czasami wymagają niezależnej od chmury pozycji. W związku z tym, Każda sekcja niniejszych wskazówek rozpoczyna się od pierwszego podejścia do platformy Azure, ale ma teoretyczne teorię chmury, która może być skalowana między decyzjami biznesowymi i technicznymi.

W tej architekturze włączenie jest podstawową kompozycją. Poniższa lista kontrolna zawiera szereg tematów, które powinny być osadzone w ramach wszelkich wysiłków związanych z wdrażaniem w chmurze w celu zapewnienia, że podróż zakończyła się sukcesem i działaniem:

- **Zamierza** Ustanawianie jasnego [rezultatu biznesowego](../business-strategy/business-outcomes/index.md), zdefiniowanego [planu podpisywania cyfrowego](../digital-estate/index.md)oraz dobrze rozumianych [wpisów zaległości](../migrate/migration-considerations/prerequisites/migration-backlog-review.md).
- **Gotowe** Zadbaj o gotowość personelu poprzez [plany umiejętności i nauki](../ready/technical-skills.md).
- **Prowadzenie** Zdefiniuj model systemu operacyjnego, który można zarządzać, aby poprowadzić działania w trakcie i po jego przyjęciu.
  - **[Organizowanie](../organization/index.md):** Wyrównaj osoby i zespoły, aby zapewnić prawidłowe operacje i wdrożenia w chmurze.
  - **Decydując** Wyrównaj odpowiednie [dyscypliny ładu](../governance/index.md) , aby stale stosować zarządzanie kosztami, ograniczanie ryzyka, zgodność i linie bazowe zabezpieczeń we wszystkich wdrożeniach chmurowych.
  - **Zarządzanie:** Trwające [operacje](../operations/index.md) portfolio IT umożliwiają zminimalizowanie przerw w procesach biznesowych i zapewnienie stabilności portfolio IT.
  - **Pomocy** Wyrównaj prawidłowe [Opcje partnerstwa i pomocy technicznej](../migrate/migration-considerations/assess/partnership-options.md).

## <a name="additional-tools"></a>Dodatkowe narzędzia

Oprócz struktury wdrażania w chmurze firma Microsoft omawia dodatkowe tematy, które mogą zapewnić sukces. W tym artykule przedstawiono kilka typowych narzędzi, które mogą znacząco poprawić sukcesy poza zakresem platformy wdrażania chmury. Ustanowienie zarządzania chmurą, odpornych architektur, umiejętności technicznych i podejścia DevOps są istotne dla sukcesu ewentualnych wysiłków związanych z wdrażaniem w chmurze. Czytelnik jest Doradzaną zakładką tej strony jako zasób do ponownego odwiedzania w ramach każdej podróży wdrożenia w chmurze.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../governance/journeys/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Cloud Adoption Framework governance model" src="../_images/operational-transformation-govern-highres.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Zarządzanie chmurą</h3>
                        <p>Zrozumienie ryzyka biznesowego, mapowanie tych zagrożeń na odpowiednie zasady i procesy. Korzystanie z narzędzi do zarządzania chmurą i pięciu dyscyplin zarządzania chmurą minimalizuje ryzyko i zwiększa prawdopodobieństwo sukcesu. Zarządzanie chmurą pomaga w kontroli kosztów, tworzeniu spójności, ulepszaniu zabezpieczeń i przyspieszeniu wdrażania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/reliability" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Resilient architecture" src="https://docs.microsoft.com/azure/architecture/resiliency/images/redundancy.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Niezawodna architektura (odporność)</h3>
                        <p>Proces tworzenia niezawodnej aplikacji w chmurze różni się od procesu opracowywania tradycyjnej aplikacji. Chociaż w przeszłości mógł zostać zakupiony sprzęt wysokiej klasy do skalowania w górę, w środowisku chmury przeprowadza się skalowanie w poziomie zamiast skalowania w górę. Zamiast zapobiegać wszystkim awariom, dąży się do minimalizacji wpływu awarii pojedynczego składnika.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="../ready/technical-skills.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Build Technical Skills" src="https://docs.microsoft.com/media/learn/Product/Learn/learningpath_graphic.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Budowanie umiejętności technicznych</h3>
                        <p>Największym narzędziem do pomocy w rozmyślnym przyjęciu w chmurze jest dobrze szkolony zespół. Rozwijaj umiejętności istniejących członków zespołu biznesowego i technicznego przy użyciu ukierunkowanych ścieżek szkoleniowych.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/devops/learn/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Learn DevOps" src="https://docs.microsoft.com/azure/devops/learn/_img/learn-devops.svg" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Podejście DevOps</h3>
                        <p>Transformacja historyczna firmy Microsoft jest poddana głównemu podejściu sposób myślenia do kultury i DevOps podejście do wykonania technicznego. Struktura wdrażania chmury jest osadzona w całym środowisku. Aby przyspieszyć wdrażanie DevOps, zapoznaj się z zawartością uczenia DevOps</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://docs.microsoft.com/azure/architecture/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Architecture Center" src="https://docs.microsoft.com/azure/architecture/example-scenario/data/media/architecture-data-warehouse.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Centrum architektury platformy Azure</h3>
                        <p>Rozwiązania architektury, architektury referencyjne, przykładowe scenariusze, najlepsze rozwiązania i wzorce projektowania w chmurze pomagające w architekturze rozwiązań działających na platformie Azure.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="https://azure.microsoft.com/pricing/calculator/" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img alt="Azure Pricing Calculator" src="../_images/calculator-preview.png" data-linktype="external" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Kalkulator cen platformy Azure</h3>
                        <p>Oblicz koszt różnych składników platformy Azure wymaganych do utworzenia lub migracji wybranego rozwiązania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

Dzięki zrozumieniu najlepszych rozwiązań w zakresie wdrażania chmury, prawdopodobieństwo sukcesu w trakcie [migracji](./migrate.md) lub [innowacji](./innovate.md) będzie znacznie wyższe.

> [!div class="nextstepaction"]
> [Migrate (Migracja)](./migrate.md)
>
> [Wprowadzaj innowacje](./innovate.md)
