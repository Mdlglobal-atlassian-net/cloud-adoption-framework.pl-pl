---
title: Motywacje i ryzyko biznesowe w dyscyplinie linii bazowej zabezpieczeń
description: Poznaj przykłady typowych rozwiązań związanych z bezpieczeństwem w ramach strategii nadzoru chmurowego i zobacz, jak to zrobić.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5e0e9b51ec666d48b886f37913a4a0d5441dd78d
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217782"
---
# <a name="motivations-and-business-risks-in-the-security-baseline-discipline"></a>Motywacje i ryzyko biznesowe w dyscyplinie linii bazowej zabezpieczeń

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę bazową zabezpieczeń w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów potencjalnego ryzyka biznesowego, które mogą być dyskowymi instrukcjami zasad.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Trafność

Bezpieczeństwo jest kluczowym problemem dla każdej organizacji IT. Wdrożenia w chmurze mają wiele takich samych zagrożeń bezpieczeństwa jak obciążenia hostowane w tradycyjnych lokalnych centrach danych. Jednak charakter platformy chmury publicznej, z braku bezpośredniej własności fizycznego sprzętu do przechowywania i uruchamiania obciążeń, oznacza, że zabezpieczenia chmury wymagają własnych zasad i procesów.

Jednym z podstawowych elementów, które określają Zarządzanie zabezpieczeniami w chmurze poza tradycyjnymi zasadami zabezpieczeń, jest łatwość tworzenia zasobów, potencjalnie dodając luki w zabezpieczeniach przed wdrożeniem. Elastyczność technologii, takich jak [SDN (Software Defined Networking)](../../decision-guides/software-defined-network/index.md) , zapewnia szybką zmianę topologii sieci opartej na chmurze, dzięki czemu można również łatwo zmodyfikować ogólną powierzchnię ataku w sieci w nieprzewidziany sposób. Platformy w chmurze udostępniają także narzędzia i funkcje, które mogą ulepszyć możliwości zabezpieczeń w sposób niemożliwy w środowiskach lokalnych.

Kwota zainwestowana w zasady zabezpieczeń i procesy będzie zależeć od rodzaju wdrożenia w chmurze. Wdrożenia testów początkowych mogą wymagać tylko najbardziej podstawowych zasad zabezpieczeń, a obciążenie o kluczowym znaczeniu będzie wymagało złożonych i rozbudowanych potrzeb związanych z bezpieczeństwem. Wszystkie wdrożenia będą musiały współpracować z dyscypliną na pewnym poziomie.

Dyscyplina linii bazowej zabezpieczeń obejmuje zasady firmowe i procesy ręczne, które można wprowadzić w celu ochrony wdrożenia w chmurze przed zagrożeniami bezpieczeństwa.

> [!NOTE]
>Chociaż ważne jest zrozumienie [dyscypliny linii bazowej tożsamości](../identity-baseline/index.md) w kontekście dyscypliny linii bazowej zabezpieczeń i sposobu odnoszącego się do kontroli dostępu, [pięć dyscyplin zarządzania chmurą](../index.md) traktuje je jako odrębne dyscypliny.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina linii bazowej zabezpieczeń próbuje rozwiązać podstawowe ryzyko biznesowe związane z zabezpieczeniami. Pracuj z firmą, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i implementowania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe zagrożenia związane z zabezpieczeniami, których można użyć jako punktu wyjścia dla dyskusji w zespole nadzoru chmurowego:

- **Naruszenie danych:** Nieumyślne narażenie lub utrata poufnych danych hostowanych w chmurze może prowadzić do utraty klientów, zagadnień umownych lub konsekwencji prawnych.
- **Przerwanie działania usługi:** Awarie i inne problemy z wydajnością wynikające z niezabezpieczonej infrastruktury przerywają normalne operacje i mogą spowodować utratę wydajności lub utratę działalności firmy.

## <a name="next-steps"></a>Następne kroki

Użyj [szablonu dyscypliny podstawy zabezpieczeń](./template.md) , aby udokumentować ryzyko biznesowe, które mogą zostać wprowadzone przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
