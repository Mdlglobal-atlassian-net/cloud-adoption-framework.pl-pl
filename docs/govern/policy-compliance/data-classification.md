---
title: Co to jest klasyfikacja danych?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Co to jest klasyfikacja danych?
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d293aa5b4427b8f714175b85c6bb5197b53f107a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027204"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-data-classification"></a>Co to jest klasyfikacja danych?

Klasyfikacja danych umożliwia określenie i przypisanie wartości do danych organizacji, a to wspólny punkt wyjścia dla zarządzania. Proces klasyfikacji danych umożliwia kategoryzowanie danych według czułości i wpływu na działalność biznesową w celu identyfikowania zagrożeń. Gdy dane są klasyfikowane, można je zarządzać w sposób chroniący poufne lub ważne dane przed kradzieżą lub utratą.

## <a name="understand-data-risks-then-manage-them"></a>Zrozumienie zagrożeń związanych z danymi, a następnie zarządzanie nimi

Przed zarządzaniem ryzykiem należy je zrozumieć. W przypadku odpowiedzialności za naruszenie danych zrozumienie rozpoczyna się od klasyfikacji danych. Klasyfikacja danych to proces kojarzenia cechy meta danych z każdym zasobem w formie cyfrowej, który identyfikuje typ danych skojarzonych z tym elementem zawartości.

Firma Microsoft sugeruje, że każdy element zawartości, który został zidentyfikowany jako potencjalny kandydat do migracji lub wdrożenia w chmurze, powinien mieć udokumentowane dane, aby zarejestrować klasyfikację danych, krytyczne znaczenie biznesowe i odpowiedzialność za rozliczenia. Te trzy punkty klasyfikacji mogą być długim sposobem na zrozumienie i łagodzenie zagrożeń.

## <a name="microsofts-data-classification"></a>Klasyfikacja danych firmy Microsoft

Poniżej znajduje się lista klasyfikacji używanych przez firmę Microsoft. W zależności od branży lub istniejących wymagań w zakresie zabezpieczeń, standardy klasyfikacji danych mogą już istnieć w organizacji. Jeśli nie istnieje Norma standardowa, zachęcamy do korzystania z tej przykładowej klasyfikacji, aby lepiej zrozumieć swój własny i cyfrowy profil.

- **Niefirma:** Dane z osobistego okresu życia, które nie należą do firmy Microsoft.
- **Społeczeństwo** Dane biznesowe dostępne bezpłatnie i zatwierdzone do użytku publicznego.
- **Ogólne:** Dane biznesowe, które nie są przeznaczone dla odbiorców publicznych.
- **Mając** Dane biznesowe, które mogą spowodować szkody dla firmy Microsoft, jeśli są udostępniane.
- **Wysoce poufne:** Dane biznesowe, które mogłyby spowodować, że firma Microsoft będzie mieć wiele szkód, jeśli są one udostępniane.

## <a name="tagging-data-classification-in-azure"></a>Klasyfikowanie klasyfikacji danych na platformie Azure

Każdy dostawca chmury powinien oferować mechanizm rejestrowania metadanych dotyczących dowolnego elementu zawartości. W przypadku platformy Azure, znaczniki zasobów to sugerowane podejście do magazynu metadanych. te Tagi mogą służyć do stosowania informacji o klasyfikacji danych do wdrożonych zasobów. Mimo że oznakowanie zasobów w chmurze według klasyfikacji nie zastępuje formalnego procesu klasyfikacji danych, zapewnia cenne narzędzie do zarządzania zasobami i stosowania zasad.

Aby uzyskać dodatkowe informacje na temat tagowania zasobów na platformie Azure, zobacz artykuł dotyczący [używania tagów do organizowania zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="next-steps"></a>Następne kroki

Zastosuj klasyfikacje danych podczas jednej z akcji ładu, które należy wykonać.

> [!div class="nextstepaction"]
> [Wybierz Przewodnik dotyczący ładu z możliwością działania](../guides/index.md)
