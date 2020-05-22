---
title: Metryki i wskaźniki tolerancji ryzyka w Cost Management dyscypliny
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby określić metryki i wskaźniki tolerancji ryzyka związane z zarządzaniem kosztami w systemie zarządzania chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ea26a5dcefa2f7bcde2c33ad4482ac8aadf06156
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755062"
---
# <a name="risk-tolerance-metrics-and-indicators-in-the-cost-management-discipline"></a>Metryki i wskaźniki tolerancji ryzyka w Cost Management dyscypliny

Dowiedz się więcej na temat określania wielkości tolerancji ryzyka biznesowego powiązanego z dyscypliną Cost Managementową. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy do inwestowania w okres zapadalności tej dyscypliny.

## <a name="metrics"></a>Metryki

Zarządzanie kosztami zwykle koncentruje się na metrykach związanych z kosztami. W ramach analizy ryzyka warto zebrać dane dotyczące bieżących i planowanych wydatków związanych z obciążeniami opartymi na chmurze, aby określić, jakie ryzyko wiąże się z założeniami i jak ważne inwestycje w Cost Management dyscypliny są przeznaczone dla planowanych wdrożeń w chmurze.

Poniżej przedstawiono przykłady przydatnych metryk, które należy zebrać, aby pomóc w ocenie tolerancji ryzyka w ramach dyscypliny Cost Management:

- **Wydatki roczne:** Łączny koszt roczny usług świadczonych przez dostawcę chmury.
- **Wydatki miesięczne:** Łączny miesięczny koszt usług świadczonych przez dostawcę chmury.
- **Prognozowany w porównaniu do rzeczywistego współczynnika:** Współczynnik porównujący prognozowane i rzeczywiste wydatki (co miesiąc lub roczny).
- **Tempo wdrożenia (od miesiąca do miesiąca):** Wartość procentowa różnic w kosztach chmury od miesiąca do miesiąca.
- **Skumulowany koszt:** Suma naliczanych dziennych wydatków, rozpoczynając od początku miesiąca.
- **Trendy wydatków:** Trend wydatków związany z budżetem.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

W przypadku wdrożeń na wczesnych małych skalę, takich jak tworzenie i testowanie lub eksperymentalne pierwsze obciążenia, zarządzanie kosztami może być stosunkowo niskiego ryzyka. Po wdrożeniu większej ilości zasobów zwiększa się ryzyko i tolerancja firmy dla ryzyka prawdopodobnie odrzuci. Ponadto, ponieważ więcej zespołów wdrażania w chmurze ma możliwość konfigurowania lub wdrażania zasobów w chmurze, zwiększa się ryzyko i zmniejsza tolerancję. Z drugiej strony, opracowywanie dyscypliny Cost Management będzie podejmować osoby z fazy wdrażania chmury w celu wdrożenia bardziej innowacyjnych technologii.

We wczesnych etapach wdrażania chmury będziesz współpracować z firmą, aby określić linię bazową tolerancji ryzyka. Po utworzeniu linii bazowej należy określić kryteria, które spowodują wyzwolenie inwestycji w Cost Management dyscypliny. Te kryteria będą prawdopodobnie inne dla każdej organizacji.

Po zidentyfikowaniu [ryzyka biznesowego](./business-risks.md), będziesz współpracować z firmą, aby identyfikować testy porównawcze, których można użyć do identyfikacji wyzwalaczy, które mogłyby zwiększyć ryzyko. Poniżej przedstawiono kilka przykładów tego, jak metryki, takie jak wymienione powyżej, można porównać z tolerancją linii bazowej ryzyka, aby wskazać potrzebę prowadzenia dalszych inwestycji w zarządzanie kosztami.

- **Oparte na zobowiązaniach (najbardziej typowe):** Firma, która jest zobowiązana do wydatków _$x, 000000_ ten rok na dostawcę chmury. Potrzebują oni Cost Management dyscypliny, aby zapewnić, że firma nie przekroczy swoich celów wydatków o więcej niż 20% i że będą korzystać z co najmniej 90% zobowiązania.
- **Wyzwalacz wartości procentowej:** Firma z wydatkami na chmurę, która jest stabilna dla systemów produkcyjnych. Jeśli to zmieni się o ponad _x%_, to w przypadku Cost Management dyscypliny jest to bardzo wiele inwestycji.
- **Wyzwalacz** nadmiernej aprowizacji: Firma, która uważa wdrożone rozwiązania, jest nadmiernie inicjowana. Zarządzanie kosztami jest inwestycją priorytetową do momentu zaprezentowania właściwego wyrównania aprowizacji i użycia zasobów.
- **Wyzwalacz wydatków miesięcznych:** Firma, która spędza ponad _$x 000 miesięcznie,_ jest uznawana za zmienny koszt. Jeśli wydatki przekroczą tę kwotę w danym miesiącu, będą musieli inwestować w koszty zarządzania.
- **Wyzwalacz wydatków rocznych:** Firma z budżetem IT R&D, która umożliwia wyliczanie _$x, 000_ rocznie na eksperymentowanie w chmurze. Mogą oni uruchamiać obciążenia produkcyjne w chmurze, ale nadal są uznawane za eksperymentalne rozwiązania, Jeśli budżet nie przekroczy tej kwoty. W przypadku przekroczenia budżetu konieczne będzie traktowanie budżetu, takiego jak inwestycja w produkcję, i ścisłe Zarządzanie wydatkami.
- **Koszty operacyjne — niekorzystne (nietypowe):** Jako firma są averse do kosztów operacyjnych i będą musieli kontrolować koszty zarządzania przed wdrożeniem obciążeń deweloperskich/testowych.

## <a name="next-steps"></a>Następne kroki

Użyj [szablonu zasad Cost Management](./template.md) , aby udokumentować metryki i wskaźniki tolerancji, które są wyrównane do bieżącego planu wdrażania w chmurze.

Zapoznaj się z przykładowymi zasadami Cost Management jako punkt wyjścia do opracowania własnych zasad w celu rozwiązania określonych zagrożeń dla firmy, które są dostosowane do planów wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
