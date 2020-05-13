---
title: Narzędzia innowacyjne do interakcji urządzeń
description: Dowiedz się więcej na temat narzędzi platformy Azure, które umożliwiają współpracę z urządzeniami i środowiskami otoczenia, które rozszerzają naturalne otoczenie i zachowania klientów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 401acfb2a0689fe54d43c29a8ab32a8d6e218670
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219771"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Narzędzia do współpracy z urządzeniami na platformie Azure

Zgodnie z opisem w artykule koncepcyjnym dotyczącym [współdziałania z urządzeniami](../considerations/devices.md)urządzenia służące do współdziałania z klientem zależą od ilości otoczenia wymaganego do zapewnienia potrzeb klienta i podejmowania przez niego akceptacji. Szybkość wyzwalacza, która monituje potrzebę klienta, oraz możliwość rozwiązania tego problemu pozwala określić czynniki w przypadku powtarzania użycia. Środowiska otoczenia pomagają skrócić czas odpowiedzi i utworzyć lepsze środowisko dla klientów, osadzając rozwiązanie w bezpośrednim otoczeniu klientów.

![Podejście platformy wdrażania w chmurze do współpracy z urządzeniami](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Dostosowywanie do metodologii

Ten typ możliwości cyfrowych można dostarczyć przy użyciu dowolnego z następujących poziomów środowiska otoczenia. Te poziomy są wyrównane z metodologią, jak pokazano na powyższym obrazie. Spis treści po lewej stronie tej strony zawiera wskazówki techniczne umożliwiające przyspieszenie rozdzielania cyfr cyfrowych. Te artykuły są pogrupowane według poziomu środowiska otoczenia, aby dostosować je do metodologii.

- **Środowisko mobilne:** Aplikacje mobilne są zwykle częścią otoczenia klienta. W niektórych scenariuszach urządzenie przenośne może zapewnić wystarczającą interakcję, aby zapewnić otoczenie rozwiązania.
- **Rzeczywistość mieszana:** Czasami naturalna otoczenie klienta musi być zmieniana w rzeczywistości mieszanej. Zaangażowanie klienta w ten rzeczywistości mieszanej może zapewnić formę środowiska otoczenia.
- **Rzeczywistość zintegrowana:** Przechodzenie bliżej Ambience, zintegrowane rozwiązania o rzeczywistości koncentrują się na użyciu fizycznego urządzenia klienta, aby zintegrować rozwiązanie z naturalnymi zachowaniami.
- **Zastosowana rzeczywistość:** Gdy dowolne z powyższych rozwiązań korzysta z analizy predykcyjnej w celu zapewnienia interakcji z klientem w naturalnym otoczeniu tego klienta, rozwiązanie to tworzy najwyższą formę środowiska otoczenia.

## <a name="toolchain"></a>Łańcuch narzędzi

Na platformie Azure często używasz następujących narzędzi do przyspieszenia cyfrowego napełniania na każdym z wcześniejszych poziomów rozwiązań otoczenia. Te narzędzia są pogrupowane w oparciu o ilość doświadczenia wymaganego do zmniejszenia złożoności narzędzi do wyrównywania z tymi środowiskami.

<!-- markdownlint-disable MD033 -->

| Kategoria | narzędzia |
|---|---|
| Środowiska mobilne | <li> Azure App Service <li> PowerApps <li> Microsoft Flow <li> Intune |
| Rzeczywistość mieszana | <li> Unity <li> Azure Spatial Anchors <li> HoloLens |
| Rzeczywistość zintegrowana | <li> Azure IoT Hub <li> Azure Sphere <li> Azure Kinect DK |
| Rzeczywistość dostosowana | <li> Chmura IoT z urządzeniem <li> Azure Digital bliźniaczych reprezentacji + HoloLens |

<!--markdownlint-enable MD033 -->

## <a name="get-started"></a>Rozpoczęcie pracy

Spis treści po lewej stronie tej strony zawiera wiele artykułów. Te artykuły ułatwiają rozpoczęcie pracy z każdym z narzędzi w tej łańcucha narzędzi.

> [!NOTE]
> Niektóre linki mogą opuścić strukturę wdrażania chmury, aby ułatwić przechodzenie poza zakres tej struktury.
