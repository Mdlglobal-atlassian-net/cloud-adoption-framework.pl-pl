---
title: Cost Management metryki, wskaźniki i tolerancję ryzyka
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Objaśnienia dotyczące dziedziny Zarządzanie kosztami w odniesieniu do utrzymania ładu w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: be1d4456ac8924c87241089c637fa3aacc38fb47
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027645"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Cost Management metryki, wskaźniki i tolerancję ryzyka

Ten artykuł ma na celu ułatwienie określenia tolerancji ryzyka biznesowego, która odnosi się do Cost Management. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy dla inwestycji w Cost Management dyscypliny.

## <a name="metrics"></a>Metryki

Cost Management zwykle koncentruje się na metrykach związanych z kosztami. W ramach analizy ryzyka warto zebrać dane dotyczące bieżących i planowanych wydatków związanych z obciążeniami opartymi na chmurze, aby określić, jakie ryzyko ma być narażone, oraz jak ważne inwestycje w zarządzanie kosztami podlegają strategii wdrażania chmury.

Poniżej przedstawiono przykłady przydatnych metryk, które należy zebrać, aby pomóc w ocenie tolerancji ryzyka w ramach dyscypliny Cost Management:

- **Wydatki roczne:** Łączny koszt roczny usług świadczonych przez dostawcę chmury.
- **Wydatki miesięczne:** Łączny miesięczny koszt usług świadczonych przez dostawcę chmury.
- **Prognozowany w porównaniu do rzeczywistego współczynnika:** Współczynnik porównujący prognozowane i rzeczywiste wydatki (co miesiąc lub roczny).
- **Współczynnik wdrożenia (MOM):** Wartość procentowa różnic w kosztach chmury od miesiąca do miesiąca.
- **Skumulowany koszt:** Suma naliczanych dziennych wydatków, rozpoczynając od początku miesiąca.
- **Trendy wydatków:** Trend wydatków związany z budżetem.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

W przypadku wczesnych wdrożeń na dużą skalę, takich jak tworzenie i testowanie lub eksperymentalne pierwsze obciążenia, Cost Management może być relatywnie niskiego ryzyka. Po wdrożeniu większej ilości zasobów wzrasta ryzyko i tolerancja biznesowa dla ryzyka prawdopodobnie odrzuci. Ponadto, ponieważ więcej zespołów wdrażania w chmurze ma możliwość konfigurowania lub wdrażania zasobów w chmurze, zwiększa się ryzyko i zmniejsza tolerancję. Z drugiej strony rozwój dyscypliny Cost Management zajmie się innymi osobami w fazie wdrażania chmury, aby wdrożyć bardziej innowacyjne nowe technologie.

We wczesnych etapach wdrażania chmury będziesz współpracować z firmą, aby określić linię bazową tolerancji ryzyka. Po utworzeniu linii bazowej należy określić kryteria, które spowodują wyzwolenie inwestycji w Cost Management dyscypliny. Te kryteria będą prawdopodobnie inne dla każdej organizacji.

Po zidentyfikowaniu [ryzyka biznesowego](./business-risks.md), będziesz współpracować z firmą, aby identyfikować testy porównawcze, których można użyć do identyfikacji wyzwalaczy, które mogłyby zwiększyć ryzyko. Poniżej przedstawiono kilka przykładów tego, jak te metryki, takie jak wymienione powyżej, można porównać z tolerancją linii bazowej ryzyka, aby wskazać potrzebę prowadzenia dalszych inwestycji w Cost Management.

- **Oparte na zobowiązaniach (najbardziej typowe):** Firma, która jest zobowiązana do wydatków $X, 000000 ten rok na dostawcę chmury. Potrzebują oni Cost Management dyscypliny, aby zapewnić, że firma nie przekroczy swoich celów wydatków o więcej niż 20% i że będą korzystać z co najmniej 90% tego zobowiązania.
- **Wyzwalacz wartości procentowej:** Firma z wydatkami na chmurę, która jest stabilna dla systemów produkcyjnych. Jeśli ta zmiana jest większa o ponad _x%_ , to dyscyplina Cost Management będzie uważana za inwestycje.
- **Wyzwalacz nadmiernej aprowizacji:** Firma, która uważa wdrożone rozwiązania, jest nadmiernie inicjowana. Cost Management jest inwestycją priorytetową, dopóki nie będą mogli udowodnić właściwego wyrównania aprowizacji i wykorzystania zasobów.
- **Wyzwalacz wydatków miesięcznych:** Firma, która spędza ponad $x 000 miesięcznie, jest uznawana za zmienny koszt. Jeśli wydatki przekroczą tę kwotę w danym miesiącu, będą musieli inwestować w Cost Management.
- **Wyzwalacz wydatków rocznych:** Firma z budżetem IT R & D, która umożliwia wyliczanie $X, 000 rocznie na eksperymentowanie w chmurze. Mogą oni uruchamiać obciążenia produkcyjne w chmurze, ale nadal będą uznawane za eksperymentalne rozwiązania, Jeśli budżet nie przekroczy tej kwoty. Po przekroczeniu tej opcji będzie konieczne traktowanie budżetu, takiego jak inwestycja w produkcję i ścisłe Zarządzanie wydatkami.
- **Koszty operacyjne — niekorzystne (nietypowe):** Jako firma averse się z kosztami operacyjnymi i przed wdrożeniem obciążeń deweloperskich/testowych będzie wymagało Cost Managementych kontroli.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), metryk dokumentu i wskaźniki tolerancji, które są wyrównane do bieżącego planu wdrożenia chmury.

Zapoznaj się z przykładowymi zasadami Cost Management jako punkt wyjścia do opracowania zasad, które dotyczą konkretnych zagrożeń firmy, które są dostosowane do planów wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
