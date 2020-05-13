---
title: Metryki i wskaźniki tolerancji ryzyka w dyscyplinie przyspieszenia wdrożenia
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby określić tolerancję ryzyka biznesowego związany z dyscypliną wdrożenia.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ed92a62d83092a54aa86c58f7b453768fe71ad1f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220281"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-deployment-acceleration-discipline"></a>Metryki i wskaźniki tolerancji ryzyka w dyscyplinie przyspieszenia wdrożenia

Dowiedz się, jak określić sposób określania tolerancji ryzyka biznesowego związanego z dyscypliną przyspieszenia wdrożenia. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy do inwestowania w okres zapadalności tej dyscypliny.

## <a name="metrics"></a>Metryki

Przyspieszenie wdrażania skupia się na ryzyku związanym z konfiguracją, wdrażaniem, aktualizowaniem i konserwowaniem zasobów w chmurze. Poniższe informacje są przydatne podczas przyjmowania tej dyscypliny zarządzania chmurą:

- **Niepowodzenia wdrożenia:** Procent wdrożeń, które kończą się niepowodzeniem lub powodują błędne skonfigurowanie zasobów.
- **Czas wdrożenia:** Ilość czasu wymagana do wdrożenia aktualizacji w istniejącym systemie.
- **Niezgodność elementów zawartości:** Liczba lub procent zasobów, które są niezgodne ze zdefiniowanymi zasadami.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

Ryzyko związane z przyspieszeniem wdrażania jest w dużym stopniu związane z liczbą i złożonością systemów opartych na chmurze wdrożonych dla przedsiębiorstwa. Wraz ze wzrostem ilości danych w chmurze liczba wdrożonych systemów oraz częstotliwość aktualizowania zasobów w chmurze zostanie zwiększona. Zależności między zasobami powiększają istotność zapewnienia właściwej konfiguracji zasobów i projektowania systemów pod kątem odporności, jeśli co najmniej jeden z zasobów napotka nieoczekiwany Przestój.

Tradycyjni korporacyjne organizacje IT często korzystają z silosów, zabezpieczeń i zespołów programistycznych, które często nie współpracują ze sobą lub są nawet adversarial lub nieszkodliwe. Aby zapewnić wczesne Rozwiązywanie problemów i integrowanie najważniejszych osób biorących udział w każdym z zespołów, może pomóc w zapewnieniu elastyczności wdrożenia chmury, gdy pozostała bezpieczna i dobrze zarządzana. W związku z tym Rozważ przyjęcie kultury organizacyjnej DevOps lub [DevSecOps](https://www.microsoft.com/devsecops) na wczesnej platformie w podróży wdrożenia w chmurze.

Współpracuj z zespołem DevSecOps oraz zainteresowanymi stronami biznesowymi, aby identyfikować [zagrożenia biznesowe](./business-risks.md) związane z konfiguracją, a następnie określić akceptowalny punkt odniesienia dla tolerancji ryzyka konfiguracji. W tej sekcji wskazówek dotyczących struktury wdrażania chmury przedstawiono przykłady, ale szczegóły dotyczące zagrożeń i linii bazowych dla Twojej firmy lub wdrożeń będą prawdopodobnie inne.

Po utworzeniu planu bazowego należy ustanowić minimalne wzorce reprezentujące nieakceptowalny wzrost w zidentyfikowanych zagrożeniach. Te progi działają jako Wyzwalacze w przypadku, gdy konieczne jest podjęcie działań w celu skorygowania tych zagrożeń. Poniżej przedstawiono kilka przykładów sposobu, w jaki metryki związane z konfiguracją, takie jak te omówione powyżej, mogą uzasadniać zwiększenie inwestycji w dyscyplinę wdrażania.

- **Wyzwalacze dryfu konfiguracji:** Firma, która ma nieoczekiwane zmiany w konfiguracji kluczowych składników systemowych lub niepowodzeń wdrażania lub aktualizacji systemów, powinna inwestować w dyscyplinę przyspieszenia wdrożenia w celu zidentyfikowania głównych przyczyn i kroków związanych z korygowaniem.
- **Wyzwalacze braku zgodności:** Jeśli liczba zasobów poza zgodności przekracza określony próg (jako łączną liczbę zasobów lub procent całkowitej ilości zasobów), firma powinna inwestować w ulepszenia dyscypliny wdrożenia, aby upewnić się, że konfiguracja każdego zasobu pozostaje zgodna z całym cyklem życia tego zasobu.
- **Wyzwalacze harmonogramu projektu:** Jeśli czas wdrożenia zasobów i aplikacji firmy często przekroczy wartość progową, firma powinna inwestować w procesy przyspieszania wdrażania, aby wprowadzać lub ulepszać zautomatyzowane wdrożenia w celu zapewnienia spójności i przewidywalności. Czasy wdrożenia mierzone w dniach lub nawet tygodniach zwykle wskazują na nieoptymalną strategię wdrażania.

## <a name="next-steps"></a>Następne kroki

[Szablon dyscypliny przyspieszenia wdrożenia](./template.md) służy do dokumentowania metryk i wskaźników tolerancji, które są wyrównane do bieżącego planu wdrażania chmury.

Zapoznaj się z przykładowymi zasadami przyspieszenia wdrożenia w celu opracowania własnych zasad w celu rozwiązania określonych zagrożeń dla firmy, które są dostosowane do planów wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
