---
title: Tworzenie początkowych subskrypcji platformy Azure
description: Rozpocznij wdrażanie platformy Azure, tworząc wstępne subskrypcje.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ba648a2e26085b8a13b698097c54d184c27f8fff
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80433324"
---
# <a name="create-your-initial-azure-subscriptions"></a>Tworzenie początkowych subskrypcji platformy Azure

Rozpocznij wdrażanie platformy Azure, tworząc początkowy zestaw subskrypcji. Dowiedz się, jakie subskrypcje należy zacząć od wymagań wstępnych.

## <a name="your-first-two-subscriptions"></a>Twoje pierwsze dwie subskrypcje

Zacznij od utworzenia dwóch subskrypcji:

- Utwórz jedną subskrypcję platformy Azure w celu uwzględnienia obciążeń produkcyjnych.
- Tworzenie drugiej subskrypcji jako środowiska nieprodukcyjnego (deweloperskiego/testowego) za pomocą [oferty platformy Azure do tworzenia i testowania](https://azure.microsoft.com/pricing/dev-test) niższych cen.

![Początkowy model subskrypcji pokazujący klucze obok pola "produkcja" i "nieprodukcja"](../../_images/ready/initial-subscription-model.png)

Takie podejście ma wiele korzyści:

- Używanie osobnych subskrypcji w środowiskach produkcyjnych i nieprodukcyjnych tworzy granicę, która upraszcza i zapewnia zarządzanie zasobami.
- Platforma Azure ma konkretne oferty subskrypcji dotyczącej tworzenia i testowania dla obciążeń nieprodukcyjnych. Oferty te zapewniają obniżone stawki za usługi platformy Azure i Licencjonowanie oprogramowania.
- Środowiska produkcyjne i nieprodukcyjne będą prawdopodobnie mieć różne zestawy zasad platformy Azure. Korzystanie z oddzielnych subskrypcji ułatwia stosowanie każdej odrębnej zasady na poziomie subskrypcji.
- Możesz zezwolić na niektóre typy zasobów platformy Azure w ramach subskrypcji nieprodukcyjnej na potrzeby testowania. Te dostawcy zasobów można włączyć w ramach subskrypcji nieprodukcyjnej bez udostępniania ich w środowisku produkcyjnym.
- Subskrypcji deweloperskich/testowych możesz używać jako izolowanych środowisk piaskownicy. Te Piaskownice umożliwiają administratorom i deweloperom szybkie tworzenie i rozłączanie całych zestawów zasobów platformy Azure. Taka izolacja może również pomóc w rozwiązywaniu problemów z ochroną danych i zabezpieczeniami.
- Dopuszczalne progi kosztu, które można zdefiniować, będą prawdopodobnie różnić się między subskrypcjami produkcji i tworzenia/testowania.

## <a name="sandbox-subscriptions"></a>Subskrypcje piaskownicy

Jeśli masz cele innowacyjne w ramach strategii wdrażania chmury, rozważ utworzenie co najmniej jednej subskrypcji piaskownicy. Możesz zastosować zasady zabezpieczeń, aby zachować te subskrypcje testowe odizolowane od środowisk produkcyjnych i nieprodukcyjnych. Użytkownicy mogą łatwo eksperymentować z możliwościami platformy Azure w tych środowiskach izolowanych. Użyj oferty tworzenia i testowania platformy Azure, aby utworzyć te subskrypcje.

![Początkowy model subskrypcji pokazujący klucze obok pól oznaczonych jako "Product", "nieprodukcyjne" i "Piaskownice"](../../_images/ready/initial-subscription-model-with-sandboxes.png)

## <a name="shared-services-subscription"></a>Subskrypcja usług udostępnionych

Jeśli planujesz hostowanie **ponad 1 000 maszyn wirtualnych lub wystąpień obliczeniowych w chmurze w ciągu 24 miesięcy**, Utwórz kolejną subskrypcję platformy Azure, aby hostować usługi udostępnione. Dzięki temu będzie można z góry przygotować się do obsługi architektury korporacyjnej przedsiębiorstwa.

![Początkowy model subskrypcji pokazujący klucze obok pól "Product" i "udostępnione usługi"](../../_images/ready/initial-subscription-model-with-shared-services.png)

## <a name="next-steps"></a>Następne kroki

Przejrzyj przyczyny, dla których warto [utworzyć dodatkowe subskrypcje platformy Azure](./scale-subscriptions.md) spełniające Twoje wymagania.

> [!div class="nextstepaction"]
> [Tworzenie dodatkowych subskrypcji w celu skalowania środowiska platformy Azure](./scale-subscriptions.md)
