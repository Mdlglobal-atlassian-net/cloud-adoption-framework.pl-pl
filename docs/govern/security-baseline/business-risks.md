---
title: Podstawowe zabezpieczenia — ryzyko biznesowe
description: Poznaj przykłady typowych rozwiązań związanych z bezpieczeństwem w ramach strategii nadzoru chmurowego i zobacz, jak to zrobić.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 40b92c15af9ea4677d049cc76902d33e6807f139
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433626"
---
# <a name="security-baseline-motivations-and-business-risks"></a>Podstawy zabezpieczeń i zagrożenia biznesowe

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę bazową zabezpieczeń w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów potencjalnego ryzyka biznesowego, które mogą być dyskowymi instrukcjami zasad.

<!-- markdownlint-disable MD026 -->

## <a name="security-baseline-relevancy"></a>Dokładność linii bazowej zabezpieczeń

Bezpieczeństwo jest kluczowym problemem dla każdej organizacji IT. Wdrożenia w chmurze mają wiele takich samych zagrożeń bezpieczeństwa jak obciążenia hostowane w tradycyjnych lokalnych centrach danych. Jednak charakter platformy chmury publicznej, z braku bezpośredniej własności fizycznego sprzętu do przechowywania i uruchamiania obciążeń, oznacza, że zabezpieczenia chmury wymagają własnych zasad i procesów.

Jednym z podstawowych elementów, które określają Zarządzanie zabezpieczeniami w chmurze poza tradycyjnymi zasadami zabezpieczeń, jest łatwość tworzenia zasobów, potencjalnie dodając luki w zabezpieczeniach przed wdrożeniem. Elastyczność technologii, takich jak [SDN (Software Defined Networking)](../../decision-guides/software-defined-network/index.md) , zapewnia szybką zmianę topologii sieci opartej na chmurze, dzięki czemu można również łatwo zmodyfikować ogólną powierzchnię ataku w sieci w nieprzewidziany sposób. Platformy w chmurze udostępniają także narzędzia i funkcje, które mogą ulepszyć możliwości zabezpieczeń w sposób niemożliwy w środowiskach lokalnych.

Kwota zainwestowana w zasady zabezpieczeń i procesy będzie zależeć od rodzaju wdrożenia w chmurze. Wdrożenia testów początkowych mogą wymagać tylko najbardziej podstawowych zasad zabezpieczeń, a obciążenie o kluczowym znaczeniu będzie wymagało złożonych i rozbudowanych potrzeb związanych z bezpieczeństwem. Wszystkie wdrożenia będą musiały współpracować z dyscypliną na pewnym poziomie.

Dyscyplina linii bazowej zabezpieczeń obejmuje zasady firmowe i procesy ręczne, które można wprowadzić w celu ochrony wdrożenia w chmurze przed zagrożeniami bezpieczeństwa.

> [!NOTE]
>Chociaż ważne jest, aby zrozumieć [linię bazową tożsamości](../identity-baseline/index.md) w kontekście linii bazowej zabezpieczeń i jak to odnosi się do Access Control, [pięć dyscyplin zarządzania chmurą](../index.md) wywołuje [linię bazową tożsamości](../identity-baseline/index.md) jako własną dyscyplinę, niezależnie od linii bazowej zabezpieczeń.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina linii bazowej zabezpieczeń próbuje rozwiązać podstawowe ryzyko biznesowe związane z zabezpieczeniami. Pracuj z firmą, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i implementowania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe zagrożenia związane z zabezpieczeniami, których można użyć jako punktu wyjścia dla dyskusji w zespole nadzoru chmurowego:

- **Naruszenie danych:** Nieumyślne narażenie lub utrata poufnych danych hostowanych w chmurze może prowadzić do utraty klientów, zagadnień umownych lub konsekwencji prawnych.
- **Przerwanie działania usługi:** Awarie i inne problemy z wydajnością wynikające z niezabezpieczonej infrastruktury przerywają normalne operacje i mogą spowodować utratę wydajności lub utratę działalności firmy.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), dokumentuj ryzyka biznesowego, które mogą być wprowadzane przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
