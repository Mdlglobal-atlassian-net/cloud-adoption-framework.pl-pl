---
title: 'Innowacje w chmurze: narzędzia do współpracy z urządzeniami na platformie Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia do współpracy z urządzeniami na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: a10a0ad39db6e7683603208938a87664c7928414
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557273"
---
# <a name="tools-to-interact-with-devices-in-azure"></a>Narzędzia do współpracy z urządzeniami na platformie Azure

Zgodnie z opisem w artykule teoretycznym dotyczącym [współpracy z urządzeniami](../considerations/devices.md)urządzenia używane do współpracy z klientem są zależne od poziomu otoczenia, który jest potrzebny do zapewnienia potrzeb klientów i podejmowania odpowiednich czynności. Szybkość z wyzwalaczem decydującym o potrzebach, a zdolność rozwiązania do zaspokajania potrzeb klientów to określenie współczynnika powtarzania użycia. Środowiska otoczenia ułatwiają skrócenie czasu odpowiedzi i stworzenie lepszego środowiska dla klientów przez osadzenie rozwiązania w bezpośrednim otoczeniu klientów.

![Podejście platformy wdrażania w chmurze do współpracy z urządzeniami](../../_images/innovate/ambient-experiences.png)

## <a name="alignment-to-the-methodology"></a>Wyrównanie do metodologii

Ten typ wynalazku cyfrowego może być dostarczany za pomocą jednego z następujących poziomów środowiska otoczenia, zgodnie z metodologią, jak powyżej. Wskazówki techniczne umożliwiające przyspieszenie rozdzielania cyfr cyfrowych są wymienione w spisie treści po lewej stronie. Te artykuły zostały pogrupowane na te same poziomy środowiska otoczenia, aby dostosować je do metodologii:

- **Środowisko mobilne:** Aplikacje mobilne są zwykle częścią otoczenia klientów. W niektórych scenariuszach urządzenie przenośne może zapewnić wystarczający poziom interaktywności, aby zapewnić otoczenie rozwiązania.
- **Rzeczywistość mieszana:** Czasami naturalna otoczenie klienta musi być zmieniana w rzeczywistości mieszanej. Klienci korzystający z tej rzeczywistości mieszanej mogą zapewnić formę środowiska otoczenia.
- **Rzeczywistość zintegrowana:** Przechodzenie bliżej Ambience, zintegrowane rozwiązania rzeczywistość koncentrują się na korzystaniu z urządzenia, które istnieje w rzeczywistości fizycznej klienta, aby zintegrować rozwiązanie z naturalnymi zachowaniami.
- **Zastosowana rzeczywistość:** Gdy dowolne z rozwiązań otaczających powyżej wykorzystuje analizę predykcyjną w celu zapewnienia interakcji z klientem w naturalnym otoczeniu, rozwiązanie tworzy najwyższą formę środowiska otoczenia.

## <a name="toolchain"></a>Łańcuch narzędzi

Na platformie Azure następujące narzędzia są często wykorzystywane do przyspieszenia cyfrowego rozróżnienia na każdym z poziomów otoczenia. Te narzędzia zostały pogrupowane na podstawie poziomu doświadczenia wymaganego do zmniejszenia złożoności narzędzi do wyrównywania w narzędziach z wymaganymi środowiskami.

- Środowisko mobilne: App Service, PowerApps, Microsoft Flow, Intune
- Rzeczywistość mieszana: Unity, kotwice przestrzenne platformy Azure, HoloLens
- Rzeczywistość: Azure IoT Hub, Azure Sphere, urządzenia Kinect DK
- Dostosowana rzeczywistość: IoT Cloud to Device, Digital bliźniaczych reprezentacji + HoloLens

## <a name="get-started"></a>Rozpocznij

Spis treści po lewej stronie zawiera wiele artykułów, które ułatwiają rozpoczęcie pracy z każdym z narzędzi w tej łańcucha narzędzi.

> [!NOTE]
> Niektóre linki mogą opuścić strukturę wdrażania chmury, aby ułatwić przechodzenie poza zakres tej struktury.
