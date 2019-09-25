---
title: Dopasuj Przewodnik dotyczący projektowania ładu w chmurze przy użyciu zasad firmowych
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dopasuj Przewodnik dotyczący projektowania ładu w chmurze przy użyciu zasad firmowych
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: b1d5562b6e8248f371e01473d141aefecf1554b4
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223747"
---
# <a name="align-your-cloud-governance-design-guide-with-corporate-policy"></a>Dopasuj Przewodnik dotyczący projektowania ładu w chmurze przy użyciu zasad firmowych

Po [zdefiniowaniu zasad w chmurze](./policy-definition.md) na podstawie [zidentyfikowanych zagrożeń](./business-risk.md)należy wygenerować wskazówki umożliwiające podjęcie odpowiednich działań, które są dostosowane do tych zasad dla personelu i deweloperów IT, do których się odwołuje. Szkicowanie przewodnika projektowego dotyczącego zarządzania chmurą umożliwia określenie określonych rozwiązań strukturalnych, technologicznych i procesów opartych na zestawieniach zasad wygenerowanych dla każdej z [pięciu dyscyplin ładu](../governance-disciplines.md).

Przewodnik projektowy dotyczący zarządzania chmurą powinien określać opcje architektury i wzorce projektowe dla każdego z głównych składników infrastruktury wdrożeń w chmurze, które najlepiej spełniają wymagania dotyczące zasad. Wraz z tymi należy zapewnić ogólne wyjaśnienie technologii, narzędzi i procesów, które będą obsługiwać każdą z tych decyzji projektowych.

Mimo że analizy ryzyka i instrukcje dotyczące zasad mogą, w pewnym stopniu, być niezależny od platformy w chmurze, przewodnik projektowy powinien zawierać szczegóły implementacji specyficzne dla platformy, które mogą być używane przez zespoły IT i deweloperskie podczas tworzenia i wdrażania obciążeń opartych na chmurze. Skup się na architekturze, narzędziach i funkcjach wybranej platformy podczas podejmowania decyzji projektowych i zapewniania wskazówek.

Podczas gdy Przewodnik projektowania w chmurze powinien wziąć pod uwagę niektóre szczegóły techniczne związane z każdym składnikiem infrastruktury, nie są one przeznaczone do obszernych dokumentów technicznych ani specyfikacji. Upewnij się, że prowadnice zawierają wskazówki dotyczące zasad i jasno stwierdzają decyzje dotyczące projektowania w formacie łatwym dla pracowników, którzy rozumieją i wiedzą.

<!-- markdownlint-enable MD033 -->

## <a name="using-the-actionable-governance-guides"></a>Korzystanie z przewodników ładu z możliwością działania

Jeśli planujesz korzystanie z platformy Azure na potrzeby wdrożenia w chmurze, struktura wdrażania w chmurze zawiera [przewodniki ładu](../guides/index.md) z możliwością działania ilustrujące przyrostowe podejście modelu ładu Framework wdrażania w chmurze. Te przewodniki dotyczące narracji obejmują szereg typowych scenariuszy wdrażania, w tym ryzyka biznesowego, wymagania dotyczące tolerancji i instrukcje zasad, które przystąpiły do tworzenia minimalnego produktu, który jest w dobrej kondycji. Te przewodniki przedstawiają syntezę rzeczywistego środowiska klienta w ramach procesu wdrażania chmury na platformie Azure.

Chociaż każde wdrożenie chmury ma unikatowe cele, priorytety i wyzwania, te przykłady powinny dostarczyć dobry szablon służący do konwertowania zasad na wskazówki. Wybierz najbliższy scenariusz do swojej sytuacji jako punkt początkowy i Mold go, aby dopasować się do konkretnych potrzeb zasad.

## <a name="next-steps"></a>Następne kroki

Mając wskazówki dotyczące projektowania, ustal procesy przestrzegania zasad, aby zapewnić zgodność z zasadami.

> [!div class="nextstepaction"]
> [Ustanów procesy przestrzegania zasad](./processes.md)
