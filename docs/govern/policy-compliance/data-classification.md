---
title: Co to jest klasyfikacja danych?
description: Klasyfikacja danych umożliwia określenie i przypisanie wartości do danych organizacji, a także udostępnia wspólny punkt początkowy dla ładu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e64acdc08f975662d3176964acbc2c0dcd53e3e4
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83224242"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Co to jest klasyfikacja danych?

Klasyfikacja danych umożliwia określenie i przypisanie wartości do danych organizacji, a także udostępnia wspólny punkt początkowy dla ładu. Proces klasyfikacji danych umożliwia kategoryzowanie danych według czułości i wpływu na działalność biznesową w celu identyfikowania zagrożeń. Gdy dane są klasyfikowane, można nimi zarządzać w sposób chroniący poufne lub ważne dane przed kradzieżą lub utratą.

## <a name="understand-data-risks-then-manage-them"></a>Zrozumienie zagrożeń związanych z danymi, a następnie zarządzanie nimi

Przed zarządzaniem ryzykiem należy je zrozumieć. W przypadku odpowiedzialności za naruszenie danych zrozumienie rozpoczyna się od klasyfikacji danych. Klasyfikacja danych to proces kojarzenia cech metadanych z każdym zasobem w formie cyfrowej, który identyfikuje typ danych skojarzonych z tym elementem zawartości.

Każdy element zawartości zidentyfikowany jako potencjalny kandydat do migracji lub wdrożenia w chmurze powinien mieć udokumentowane metadane, aby zarejestrować klasyfikację danych, krytyczne znaczenie biznesowe i rozliczenia. Te trzy punkty klasyfikacji mogą być długim sposobem na zrozumienie i łagodzenie zagrożeń.

## <a name="classifications-microsoft-uses"></a>Klasyfikacje stosowane przez firmę Microsoft

Poniżej znajduje się lista klasyfikacji używanych przez firmę Microsoft. W zależności od branży lub istniejących wymagań w zakresie zabezpieczeń, standardy klasyfikacji danych mogą już istnieć w organizacji. Jeśli nie istnieje Norma standardowa, warto użyć tej przykładowej klasyfikacji, aby lepiej zrozumieć swój własny i cyfrowy profil.

- **Niefirma:** Dane pochodzące z Twojego osobistego okresu użytkowania, które nie należą do firmy Microsoft.
- **Publiczny:** Dane biznesowe dostępne bezpłatnie i zatwierdzone do użytku publicznego.
- **Ogólne:** Dane biznesowe, które nie są przeznaczone dla odbiorców publicznych.
- **Poufne:** Dane biznesowe, które mogą spowodować szkody dla firmy Microsoft, jeśli są udostępniane.
- **Wysoce poufne:** Dane biznesowe, które mogłyby spowodować, że firma Microsoft będzie mieć wiele szkód, jeśli są one udostępniane.

## <a name="tagging-data-classification-in-azure"></a>Klasyfikowanie klasyfikacji danych na platformie Azure

Tagi zasobów są dobrym rozwiązaniem dla magazynu metadanych i można użyć tych tagów do zastosowania informacji o klasyfikacji danych do wdrożonych zasobów. Chociaż tagowanie zasobów w chmurze według klasyfikacji nie zastępuje formalnego procesu klasyfikacji danych, zapewnia cenne narzędzie do zarządzania zasobami i stosowania zasad. [Azure Information Protection](https://docs.microsoft.com/azure/information-protection/what-is-information-protection) to doskonałe rozwiązanie ułatwiające klasyfikowanie _danych_ , bez względu na to, gdzie się znajduje (lokalnie, na platformie Azure lub w innym miejscu). Rozważmy ją jako część ogólnej strategii klasyfikacji.

Aby uzyskać dodatkowe informacje na temat tagowania zasobów na platformie Azure, zobacz [Używanie tagów do organizowania zasobów platformy Azure i hierarchii zarządzania](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).

## <a name="next-steps"></a>Następne kroki

Zastosuj klasyfikacje danych podczas jednej z akcji ładu, które należy wykonać.

> [!div class="nextstepaction"]
> [Wybierz Przewodnik dotyczący ładu z możliwością działania](../guides/index.md)
