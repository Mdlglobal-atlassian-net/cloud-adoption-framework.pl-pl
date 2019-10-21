---
title: Wyrównanie biznesowe — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyrównanie biznesowe — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9c6884d57b9238f58921b14ec3ddbbe3623506af
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558144"
---
# <a name="create-business-alignment-in-cloud-management"></a>Tworzenie wyrównania biznesowego w zarządzaniu chmurą

W środowiskach lokalnych zasoby IT (aplikacje, maszyny wirtualne, hosty maszyn wirtualnych, dysk, serwery, urządzenia i źródła danych) są zarządzane przez dział IT do obsługi operacji związanych z obciążeniami. W warunkach INFORMATYCZNych obciążenie jest kolekcją zasobów IT, które obsługują konkretną operację biznesową. W środowiskach lokalnych zarządzanie działem IT realizuje Projektowanie procesów, aby zminimalizować zakłócenia dla tych zasobów IT, próbując zminimalizować zakłócenia w operacjach związanych z obsługą techniczną. Podczas przechodzenia do chmury zarządzanie i operacje są zmieniane na bit, dzięki czemu można rozwijać ściślejsze dostosowanie firmy.

## <a name="business-vernacular"></a>Vernacular biznesowa

Pierwszym krokiem w tworzeniu wyrównania biznesowego jest wyrównanie warunku. Zarządzanie IT, takie jak większość zawodów inżynieryjnych, obejmuje rzetelny żargon lub wysoce techniczne warunki. Te warunki mogą prowadzić do nieporozumień w przypadku uczestników współpracy i utrudniać mapowanie usług zarządzania na wartość biznesową.

Na szczęście procesy opracowywania strategii wdrażania chmurowego i planu wdrażania chmury tworzą pomysł dla ponownego mapowania warunków. Tworzy również doskonałą okazję do rozmyślenia zobowiązań związanych z zarządzaniem operacyjnymi w ramach współpracy z firmą. Poniższa seria artykułu przeprowadzi Cię przez nowe podejście w ramach trzech określonych terminów, które mogą poprawić konwersacje ze stronami biznesowymi:

- **[Krytyczność](./criticality.md)** : mapowanie obciążeń na procesy biznesowe. Krytyczne znaczenie klasyfikacji do koncentracji inwestycji.
- **[Wpływ](./impact.md)** : Poznaj wpływ potencjalnej awarii, aby pomóc w ocenie powrotu do inwestycji związanych z zarządzaniem chmurą.
- **[Zobowiązanie](./commitment.md)** : opracowywanie prawdziwych partnerstwa przez tworzenie i dokumentowanie umów **z firmą**.

> [!NOTE]
> Poniżej każdego z tych warunków są klasyczne warunki IT, takie jak SLA, RTO i RPO. Mapowanie firm i warunki IT są omówione bardziej szczegółowo w artykule dotyczącym zobowiązania.

## <a name="ops-management-planning-workbook"></a>Skoroszyt planowania zarządzania w Ops

Aby ułatwić przechwycenie decyzji w wyniku tej rozmowy, [skoroszyt zarządzania Ops](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) jest dostępny w naszym repozytorium GitHub. Ten skoroszyt nie wykonuje umowy SLA ani obliczeń kosztów. Służy tylko jako przewodnik do przechwytywania tych miar i prognozy zwracanych działań związanych z uniknięciem utraty strat.

Alternatywnie te same obciążenia i powiązane zasoby mogą być otagowane bezpośrednio na platformie Azure, jeśli rozwiązania zostały już wdrożone w chmurze.

## <a name="next-steps"></a>Następne kroki

Rozpocznij tworzenie wyrównania biznesowego przez określenie poziomu [krytycznego dla obciążenia](./criticality.md).

> [!div class="nextstepaction"]
> [Definiowanie krytycznego obciążenia](./criticality.md)
