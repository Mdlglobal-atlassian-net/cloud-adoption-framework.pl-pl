---
title: Migracja do chmury
description: Dowiedz się, jak ustanowić iteracyjne procesy oceniania, migrowania, optymalizacji i zabezpieczania obciążeń, które chcesz migrować do chmury, oraz zarządzania nimi.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: b341996c45c4a0c5b7d8467419c3117f939afa20
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120756"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Migracja do chmury w podręczniku Cloud Adoption Framework

Każdy [plan wdrożenia chmury](../plan/index.md) w skali przedsiębiorstwa będzie zawierać obciążenia, które nie gwarantują znacznych inwestycji w przypadku tworzenia nowej logiki biznesowej. Te obciążenia można przenieść do chmury za pomocą różnorodnych podejść: metodą „lift and shift” czy „lift and optimize” albo przez modernizację. Każda z tych metod jest traktowana jako migracja. Poniższe ćwiczenia pomogą ustanowić iteracyjne procesy oceniania, migrowania, optymalizacji i zabezpieczania tych obciążeń oraz zarządzania nimi.

## <a name="getting-started"></a>Wprowadzenie

Aby przygotować się na tę fazę cyklu wdrażania chmury, zalecane są następujące ćwiczenia:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migrowanie pierwszego obciążenia</h3>
Korzystając z przewodnika po migracji na platformę Azure, zapoznaj się z narzędziami natywnymi dla platformy Azure i podejściem do migracji.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Scenariusze migracji</h3>
Korzystając z dodatkowych podejść i narzędzi do migracji, podejmij działania w innych scenariuszach migracji.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Najlepsze rozwiązania</h3>
Reaguj na typowe potrzeby związane z migracją, stosując spójne najlepsze rozwiązania.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Ulepszenia procesu</h3>
Migracja to działanie mocno obciążone procesami. W miarę skalowania pracy związanej z migracją za pomocą tych ulepszeń procesów oceniaj i dopracowuj różne aspekty migracji.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

Ta metodologia i powyższe kroki opierają się na poniższych założeniach:

- Metodologia rządząca przebiegami migracji pasuje do fal migracji lub wydań, które są zdefiniowane przy użyciu metodologii Planowania, Gotowości i Wdrażania. W każdym przebiegu migracji partia obciążeń jest migrowana do chmury.
- Przed migrowaniem obciążeń zidentyfikowano, skonfigurowano i wdrożono co najmniej jedną [strefę docelową](../ready/index.md) spełniającą potrzeby krótkoterminowego planu wdrożenia chmury.
- Migracja jest najczęściej kojarzona z terminami _„lift-and-shift”_ i _ponowne hostowanie_. Ta metodologia i powyższe kroki opierają się na założeniu, że samego podejścia ponownego hostowania nie należy stosować dla żadnego centrum danych, a dla obciążeń należy je stosować tylko w niewielu przypadkach. Choć wiele obciążeń można ponownie hostować, klienci częściej wolą modernizować konkretne zasoby obciążenia. W trakcie tego iteracyjnego procesu jedną z najczęściej omawianych kwestii jest równowaga między szybkością i modernizacją.

## <a name="migration-effort"></a>Nakład pracy związany z migracją

Nakład pracy wymagany do migracji obciążeń zwykle mieści się w trzech typach prac (lub faz) dla każdego obciążenia: Ocena obciążeń, wdrażanie obciążeń i wydawanie obciążeń. Ta sekcja przewodnika Cloud Adoption Framework uczy czytelników, jak zmaksymalizować zwrot z każdej fazy wymaganej do migracji obciążenia do środowiska produkcyjnego.

W standardowej dwutygodniowej iteracji doświadczony zespół ds. migracji może ukończyć ten proces dla 2–5 obciążeń o niskiej i średniej złożoności. Bardziej złożone obciążenia, takie jak SAP, mogą wymagać kilku dwutygodniowych iteracji, aby ukończyć wszystkie trzy fazy pracy związanej z migracją dla pojedynczego obciążenia. Środowisko i stopień złożoności mają znaczny wpływ na osie czasu i szybkość migracji.

![Proces migracji opisany w przewodniku Cloud Adoption Framework](../_images/migrate/methodology.png)

Następujące punkty zawierają przegląd etapów tego procesu (przedstawionych powyżej):

- **Ocena obciążeń:** Ocena obciążeń w celu oceny kosztów, modernizacji i narzędzi wdrażania. Proces ten koncentruje się na weryfikacji lub podważaniu założeń poczynionych podczas wcześniejszych odkryć i ocen poprzez dokładniejsze przyjrzenie się opcjom racjonalizacji. Również na tym etapie wzorce i zależności użytkowników są badane bardziej szczegółowo, aby zapewnić, że obciążenia osiągną sukces techniczny po migracji.
- **Wdrażanie obciążeń:** Po ocenie obciążeń istniejące funkcje tych obciążeń są replikowane (lub ulepszane) w chmurze. Może to dotyczyć metody _lift and shift_ lub _ponownego hostowania_ w chmurze. Jednak częściej na tym etapie wiele zasobów obsługujących te obciążenia zostanie zmodernizowane, aby można było skorzystać z zalet chmury.
- **Wydawanie obciążeń:** Po replikacji funkcji do chmury obciążenia mogą być testowane, optymalizowane, dokumentowane i wydawane na potrzeby bieżących operacji. Podczas tego procesu krytyczne znaczenie ma przegląd migrowanych obciążeń i przekazywanie ich zespołom ds. ładu, zarządzania operacjami i bezpieczeństwa w celu zapewnienia ciągłej obsługi tych obciążeń.

> [!NOTE]
> W niektórych wczesnych iteracjach procesu migracji częstą praktyką jest ograniczenie do jednego obciążenia. Takie podejście maksymalizuje zachowanie umiejętności i zespołowi więcej czasu na eksperymentowanie i naukę.
> [!NOTE]
> Podczas budowania fabryki migracji niektóre zespoły mogą zdecydować o rozproszeniu każdej z powyższych faz na wiele zespołów i/lub wiele przebiegów. Takie podejście może poprawić powtarzalność i przyspieszyć migrację.

## <a name="migration-waves"></a>Fale migracji

Iteracje migracji zapewnią wartość techniczną poprzez migrację zasobów i obciążeń. Fala migracji to najmniejsza kolekcja obciążeń, która zapewnia namacalną i wymierną wartość biznesową. Każda iteracja powinna kończyć się raportem przedstawiającym wykonane działania techniczne. Jednak zmiany biznesowe i planowanie strategiczne na ogół odbywają się na nieco wyższym poziomie. Podczas gdy zespół wdrożeniowy ds. chmury dokłada starań w zakresie procesu migracji, zespół strategiczny ds. chmury koncentruje się na planowaniu kolejnych 1-2 fal migracji. Zespół strategiczny ds. chmury śledzi również postęp techniczny w postaci metryki uczenia się, aby lepiej zrozumieć terminy (osie czasu) realizacji wartości biznesowej. W związku z tym fale migracji są iteracyjnym podejściem do zarządzania zmianami, które pozwala śledzić wyniki biznesowe, osoby i osie czasu.

Jak przedstawiono na ilustracji w poprzedniej sekcji, procesy w metodologii [Planowanie](../plan/index.md), metodologii [Gotowość](../ready/index.md) i w pewnym stopniu metodologii [Strategia](../strategy/index.md) przewodnika Cloud Adoption Framework zapewniają konspekt planowania fal migracji i zarządzania nimi. Zarządzanie tymi falami ustali priorytety i określi nakłady pracy związane z migracją, które mają być dostarczone przez zespoły techniczne.

## <a name="next-steps"></a>Następne kroki

Powyższe kroki obejmujące „Wprowadzenie” oraz kolejne wskazówki zawarte w metodologii migracji ułatwią rozwinięcie umiejętności usprawniających wykonywanie procesów w ramach każdego przebiegu migracji. [Przewodnik po migracji na platformę Azure](./azure-migration-guide/index.md) to krótka seria artykułów, w których przedstawiono najbardziej typowe narzędzia i podejścia niezbędne podczas pierwszej fali migracji.

> [!div class="nextstepaction"]
> [Przewodnik po migracji na platformę Azure](./azure-migration-guide/index.md)
