---
title: Metryki, wskaźniki i odporność na przyspieszenie wdrożenia
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Metryki, wskaźniki i odporność na przyspieszenie wdrożenia
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5049b41abc03c5f59d0d750373b48a39b0638084
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027759"
---
# <a name="deployment-acceleration-metrics-indicators-and-risk-tolerance"></a>Metryki, wskaźniki i odporność na przyspieszenie wdrożenia

Ten artykuł ma na celu ułatwienie określenia tolerancji ryzyka biznesowego, które wiążą się z przyspieszeniem wdrażania. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy dla inwestycji w okres zapadalności dyscypliny wdrożenia.

## <a name="metrics"></a>Metryki

Dyscyplina wdrożenia koncentruje się na ryzyku związanym z konfiguracją, wdrażaniem, aktualizowaniem i konserwowaniem zasobów w chmurze. Poniższe informacje są przydatne podczas przyjmowania tej dyscypliny zarządzania chmurą:

- **Niepowodzenia wdrożenia:** Procent wdrożeń, które kończą się niepowodzeniem lub powodują błędne skonfigurowanie zasobów.
- **Czas wdrożenia:** Ilość czasu wymagana do wdrożenia aktualizacji w istniejącym systemie.
- **Niezgodność elementów zawartości:** Liczba lub procent zasobów, które są niezgodne ze zdefiniowanymi zasadami.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

Ryzyko związane z przyspieszeniem wdrażania jest w dużym stopniu związane z liczbą i złożonością systemów opartych na chmurze wdrożonych dla przedsiębiorstwa. Wraz ze wzrostem ilości danych w chmurze liczba wdrożonych systemów oraz częstotliwość aktualizowania zasobów w chmurze zostanie zwiększona. Zależności między zasobami powiększają istotność zapewnienia właściwej konfiguracji zasobów i projektowania systemów pod kątem odporności, jeśli co najmniej jeden z zasobów napotka nieoczekiwany Przestój.

<!-- "en-us" location is required for the URL below. -->

Rozważ przyjęcie kultury organizacyjnej DevOps lub [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) na wczesnej platformie w podróży wdrażania w chmurze. Tradycyjni korporacyjne organizacje IT często korzystają z silosów, zabezpieczeń i zespołów programistycznych, które często nie współpracują ze sobą lub są nawet adversarial lub nieszkodliwe. Aby zapewnić wczesne Rozwiązywanie problemów i integrowanie najważniejszych osób biorących udział w każdym z zespołów, może pomóc w zapewnieniu elastyczności wdrożenia chmury, gdy pozostała bezpieczna i dobrze zarządzana.

Współpracuj z zespołem DevSecOps oraz zainteresowanymi stronami biznesowymi, aby identyfikować [zagrożenia biznesowe](./business-risks.md) związane z konfiguracją, a następnie określić akceptowalny punkt odniesienia dla tolerancji ryzyka konfiguracji. W tej sekcji wskazówek dotyczących struktury wdrażania chmury przedstawiono przykłady, ale szczegóły dotyczące zagrożeń i linii bazowych dla Twojej firmy lub wdrożeń będą prawdopodobnie inne.

Po utworzeniu planu bazowego należy ustanowić minimalne wzorce reprezentujące nieakceptowalny wzrost w zidentyfikowanych zagrożeniach. Te progi działają jako Wyzwalacze w przypadku, gdy konieczne jest podjęcie działań w celu skorygowania tych zagrożeń. Poniżej przedstawiono kilka przykładów sposobu, w jaki metryki związane z konfiguracją, takie jak te omówione powyżej, mogą uzasadniać zwiększenie inwestycji w dyscyplinę wdrażania.

- **Wyzwalacze dryfu konfiguracji:** Firma, która ma nieoczekiwane zmiany w konfiguracji kluczowych składników systemowych lub niepowodzeń wdrażania lub aktualizacji systemów, powinna inwestować w dyscyplinę przyspieszenia wdrożenia w celu zidentyfikowania głównych przyczyn i kroków związanych z korygowaniem.
- **Wyzwalacze braku zgodności:** Jeśli liczba zasobów poza zgodności przekracza określony próg (jako łączną liczbę zasobów lub procent całkowitej ilości zasobów), firma powinna inwestować w ulepszenia dyscypliny wdrożenia, aby upewnić się, że wszystkie zasoby Konfiguracja pozostaje w zgodności w całym cyklu życia tego zasobu.
- **Wyzwalacze harmonogramu projektu:** Jeśli czas wdrożenia zasobów i aplikacji firmy często przekroczy wartość progową, firma powinna inwestować w procesy przyspieszania wdrażania, aby wprowadzać lub ulepszać zautomatyzowane wdrożenia w celu zapewnienia spójności i przewidywalności. Czasy wdrożenia mierzone w dniach lub nawet tygodniach zwykle wskazują na nieoptymalną strategię wdrażania.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), metryk dokumentu i wskaźniki tolerancji, które są wyrównane do bieżącego planu wdrożenia chmury.

Zapoznaj się z przykładowymi zasadami przyspieszenia wdrożenia w celu opracowania zasad związanych z konkretnymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
