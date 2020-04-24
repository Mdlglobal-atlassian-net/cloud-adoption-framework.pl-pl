---
title: Narzędzia innowacyjne do interakcji urządzeń
description: Dowiedz się więcej na temat narzędzi platformy Azure, które umożliwiają współpracę z urządzeniami i środowiskami otoczenia, które rozszerzają naturalne otoczenie i zachowania klientów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: f6dfc621d20f2f2d3135e99be197e3fdfd315bdc
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80425400"
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

- Środowisko mobilne: Azure App Service, PowerApps, Microsoft Flow, Intune
- Rzeczywistość mieszana: Unity, kotwice przestrzenne platformy Azure, HoloLens
- Stan zintegrowany: Azure IoT Hub, Azure Sphere, Azure urządzenia Kinect DK
- Dostosowana rzeczywistość: IoT Cloud to Device, Azure Digital bliźniaczych reprezentacji + HoloLens

## <a name="get-started"></a>Rozpoczęcie pracy

Spis treści po lewej stronie tej strony zawiera wiele artykułów. Te artykuły ułatwiają rozpoczęcie pracy z każdym z narzędzi w tej łańcucha narzędzi.

> [!NOTE]
> Niektóre linki mogą opuścić strukturę wdrażania chmury, aby ułatwić przechodzenie poza zakres tej struktury.
