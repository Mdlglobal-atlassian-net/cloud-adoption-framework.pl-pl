---
title: Włącz powodzenie klienta w trakcie podróży w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Włączanie sukcesu klienta w całej podróży w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: overview
layout: LandingPage
ms.openlocfilehash: cb5ba007c18643efe3b0c83b8ff247844cbbe7b2
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753290"
---
# <a name="enable-success-during-a-cloud-adoption-journey"></a>Włącz powodzenie w trakcie podróży w chmurze

Platforma wdrażania w chmurze to bezpłatne narzędzie samoobsługowe, które prowadzi czytelników przez różne wysiłki związane z wdrażaniem w chmurze. Struktura pomaga klientom w realizacji celów firmy, które mogą być włączone przez Microsoft Azure. Jednakże ta zawartość rozpoznaje również, że czytelnik może zająć się szeroką wyzwaniami biznesowymi, kulturami lub technicznymi, a czasami może wymagać niezależnej od chmury pozycji. W związku z tym, Każda sekcja niniejszych wskazówek rozpoczyna się od pierwszego podejścia do platformy Azure, a następnie przy użyciu teorii neutralnej dla chmury, która może być skalowana w wielu decyzjach gospodarczych i technicznych.

W tej architekturze włączenie jest podstawową kompozycją. Poniższa lista kontrolna wyszczególniono podstawowe zasady wdrażania rozwiązań w chmurze, które zapewniają, że przeprowadzenie podróży jest uznawane za pomyślne i w firmie:

- **Plan:** Ustanowienie jasnego [rezultatu biznesowego](../strategy/business-outcomes/index.md), jasno zdefiniowanego [planu podpisywania cyfrowego](../digital-estate/index.md)i dobrze zrozumiałego [wdrażania](../migrate/migration-considerations/prerequisites/migration-backlog-review.md).
- **Gotowe:** Zadbaj o gotowość personelu poprzez [plany umiejętności i nauki](../ready/technical-skills.md).
- **Działa:** Zdefiniuj model systemu operacyjnego, który można zarządzać, aby poprowadzić działania w trakcie i po jego przyjęciu.
  - **[Organizuj](../organize/index.md):** Wyrównaj osoby i zespoły, aby zapewnić prawidłowe operacje i wdrożenia w chmurze.
  - **Zarządzanie:** Wyrównaj odpowiednie [dyscypliny ładu](../govern/index.md) , aby stale stosować zarządzanie kosztami, ograniczanie ryzyka, zgodność i linie bazowe zabezpieczeń we wszystkich wdrożeniach chmurowych.
  - **Zarządzanie:** Ciągłe [Zarządzanie działaniem](../manage/index.md) portfolio IT w celu zminimalizowania przerw w procesach biznesowych i zapewnienia stabilności portfolio IT.
  - **Obsługa:** Wyrównaj prawidłowe [Opcje partnerstwa i pomocy technicznej](../migrate/migration-considerations/assess/partnership-options.md).

## <a name="additional-tools"></a>Dodatkowe narzędzia

Oprócz struktury wdrażania w chmurze firma Microsoft omawia dodatkowe tematy, które mogą zapewnić sukces. W tym artykule przedstawiono kilka typowych narzędzi, które mogą znacząco poprawić sukcesy poza zakresem platformy wdrażania chmury. Ustanowienie zarządzania chmurą, odpornych architektur, umiejętności technicznych i podejścia DevOps są istotne dla sukcesu ewentualnych wysiłków związanych z wdrażaniem w chmurze. Oznacz Tę stronę jako zasób do ponownego odwiedzania w ramach każdej podróży wdrożenia w chmurze.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsH">
<li style="display: flex; flex-direction: column;">
    <a href="../govern/guides/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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
    <a href="https://docs.microsoft.com/azure/architecture/framework/resiliency/overview" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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
                        <p>Proces tworzenia niezawodnej aplikacji w chmurze różni się od procesu opracowywania tradycyjnej aplikacji. Chociaż w przeszłości mógł zostać zakupiony sprzęt wysokiej klasy do skalowania w górę, w środowisku chmury przeprowadza się skalowanie w poziomie zamiast skalowania w górę. Zamiast próbować całkowicie zapobiegać awariom, celem jest minimalizacja wpływu awarii pojedynczego składnika.</p>
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
                        <h3>Centrum architektury Azure</h3>
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
