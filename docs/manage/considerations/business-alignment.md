---
title: Wyrównanie biznesowe w zarządzaniu chmurą
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak lepiej zarządzać operacjami w chmurze i rozwijać ściślejsze wyrównania biznesowe.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e06aca53ac70e602d13d2cc23d59d4b56c2cd152
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341440"
---
# <a name="create-business-alignment-in-cloud-management"></a>Tworzenie wyrównania biznesowego w zarządzaniu chmurą

W środowiskach lokalnych zasoby IT (aplikacje, maszyny wirtualne, hosty maszyn wirtualnych, dysk, serwery, urządzenia i źródła danych) są zarządzane przez dział IT do obsługi operacji związanych z obciążeniami. W warunkach INFORMATYCZNych obciążenie jest kolekcją zasobów IT, które obsługują konkretną operację biznesową. Aby ułatwić obsługę operacji w biznesie, zarządzanie IT zapewnia procesy, które zostały zaprojektowane w celu zminimalizowania zakłóceń do tych zasobów. Gdy organizacja przenosi się do chmury, zarządzanie i operacje przewyższają bit, dzięki czemu można opracowywać ściślejsze dostosowanie firmy.

## <a name="business-vernacular"></a>Vernacular biznesowa

Pierwszym krokiem podczas tworzenia wyrównania firmy jest zapewnienie wyrównania terminu. Zarządzanie IT, takie jak większość zawodów inżynieryjnych, miało amassed zbiór żargonów lub wysoce technicznych warunków. Warunki te mogą prowadzić do nieporozumień w przypadku uczestników współpracy i utrudniać mapowanie usług zarządzania na wartość biznesową.

Na szczęście proces opracowywania strategii wdrażania w chmurze i planu wdrażania chmury umożliwia idealne rozwiązanie do ponownego mapowania tych warunków. Proces ten umożliwia również tworzenie szans związanych z zarządzaniem działaniami w ramach współpracy z firmą. Poniższa seria artykułu przeprowadzi Cię przez nowe podejście w ramach trzech określonych terminów, które mogą pomóc w ulepszaniu konwersacji między udziałowcami biznesowymi: 

- Poziom  **[krytyczności](./criticality.md):** Mapowanie obciążeń na procesy biznesowe. Krytyczne znaczenie klasyfikacji do koncentracji inwestycji.
- **[Wpływ](./impact.md):** Zrozumienie wpływu potencjalnej awarii, aby pomóc w ocenie powrotu do inwestycji związanych z zarządzaniem chmurą.
- **[Zobowiązanie](./commitment.md):** opracowywanie prawdziwych partnerstwa przez tworzenie i dokumentowanie umów *z firmą*.

> [!NOTE]
> Podstawowe warunki te są klasycznymi postanowieniami IT, takimi jak SLA, RTO i RPO. Mapowanie konkretnych firm i warunki IT są szczegółowo omówione w artykule dotyczącym [zobowiązania](./commitment.md) .

## <a name="ops-management-planning-workbook"></a>Skoroszyt planowania zarządzania w Ops

Aby ułatwić przechwycenie decyzji wynikających z tej konwersacji dotyczącej wyrównania terminu, [skoroszyt zarządzania Ops](https://raw.githubusercontent.com/microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) jest dostępny w witrynie GitHub. Ten skoroszyt nie wykonuje umowy SLA ani obliczeń kosztów. Służy tylko do przechwycenia takich środków i prognozowania powrotu do unikania utraty strat.

Alternatywnie te same obciążenia i powiązane zasoby mogą być otagowane bezpośrednio na platformie Azure, jeśli rozwiązania zostały już wdrożone w chmurze.

## <a name="next-steps"></a>Następne kroki

Rozpocznij tworzenie wyrównania biznesowego przez określenie poziomu [krytycznego dla obciążenia](./criticality.md).

> [!div class="nextstepaction"]
> [Definiowanie krytycznego obciążenia](./criticality.md)
