---
title: Tworzenie początkowych subskrypcji platformy Azure
description: Rozpocznij wdrażanie platformy Azure, tworząc wstępne subskrypcje.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 975248025ff170ff872fdd5970f548a8fc83c953
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215402"
---
# <a name="create-your-initial-azure-subscriptions"></a>Tworzenie początkowych subskrypcji platformy Azure

Rozpocznij wdrażanie platformy Azure, tworząc początkowy zestaw subskrypcji. Dowiedz się, jakie subskrypcje należy zacząć od wymagań wstępnych.

## <a name="your-first-two-subscriptions"></a>Twoje pierwsze dwie subskrypcje

Zacznij od utworzenia dwóch subskrypcji:

- Utwórz jedną subskrypcję platformy Azure w celu uwzględnienia obciążeń produkcyjnych.
- Utwórz drugą subskrypcję, która będzie stanowić Środowisko nieprodukcyjne (deweloperskie/testowe), korzystając z [oferty usługi Azure Dev/Test](https://azure.microsoft.com/pricing/dev-test) dla niższych cen.

![Początkowy model subskrypcji pokazujący klucze obok pola "produkcja" i "nieprodukcja"](../../_images/ready/initial-subscription-model.png)

<!-- docsTest:ignore Dev/Test -->

Takie podejście ma wiele korzyści:

- Używanie osobnych subskrypcji w środowiskach produkcyjnych i nieprodukcyjnych tworzy granicę, która upraszcza i zapewnia zarządzanie zasobami.
- Oferty subskrypcji na platformę Azure Dev/Test są dostępne dla obciążeń nieprodukcyjnych. Oferty te zapewniają obniżone stawki za usługi platformy Azure i Licencjonowanie oprogramowania.
- Środowiska produkcyjne i nieprodukcyjne będą prawdopodobnie mieć różne zestawy zasad platformy Azure. Korzystanie z oddzielnych subskrypcji ułatwia stosowanie każdej odrębnej zasady na poziomie subskrypcji.
- Możesz zezwolić na niektóre typy zasobów platformy Azure w ramach subskrypcji nieprodukcyjnej na potrzeby testowania. Te dostawcy zasobów można włączyć w ramach subskrypcji nieprodukcyjnej bez udostępniania ich w środowisku produkcyjnym.
- Subskrypcji deweloperskich/testowych możesz używać jako izolowanych środowisk piaskownicy. Te Piaskownice umożliwiają administratorom i deweloperom szybkie tworzenie i rozłączanie całych zestawów zasobów platformy Azure. Taka izolacja może również pomóc w rozwiązywaniu problemów z ochroną danych i zabezpieczeniami.
- Dopuszczalne progi kosztu, które można zdefiniować, będą prawdopodobnie różnić się między subskrypcjami produkcji i tworzenia/testowania.

## <a name="sandbox-subscriptions"></a>Subskrypcje piaskownicy

Jeśli cele innowacyjne są częścią strategii wdrażania chmury, należy rozważyć utworzenie co najmniej jednej subskrypcji piaskownicy. Możesz zastosować zasady zabezpieczeń, aby zachować te subskrypcje testowe odizolowane od środowisk produkcyjnych i nieprodukcyjnych. Użytkownicy mogą łatwo eksperymentować z możliwościami platformy Azure w tych środowiskach izolowanych. Użyj oferty tworzenia i testowania platformy Azure, aby utworzyć te subskrypcje.

![Początkowy model subskrypcji pokazujący klucze obok pól oznaczonych jako "Product", "nieprodukcyjne" i "Piaskownice"](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Subskrypcja usług udostępnionych

Jeśli planujesz hostowanie **ponad 1 000 maszyn wirtualnych lub wystąpień obliczeniowych w chmurze w ciągu 24 miesięcy**, Utwórz kolejną subskrypcję platformy Azure, aby hostować usługi udostępnione. Dzięki temu będzie można z góry przygotować się do obsługi architektury korporacyjnej przedsiębiorstwa.

![Początkowy model subskrypcji pokazujący klucze obok pól "Product" i "udostępnione usługi"](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Następne kroki

Przejrzyj przyczyny, dla których warto [utworzyć dodatkowe subskrypcje platformy Azure](./scale-subscriptions.md) spełniające Twoje wymagania.

> [!div class="nextstepaction"]
> [Tworzenie dodatkowych subskrypcji w celu skalowania środowiska platformy Azure](./scale-subscriptions.md)
