---
title: Organizowanie wielu subskrypcji platformy Azure i zarządzanie nimi
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o tworzeniu hierarchii grup zarządzania w celu uproszczenia zarządzania subskrypcjami i zasobami.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 7f232b6af4dc501b775d99a567cdca11dc0500a2
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223426"
---
# <a name="organize-and-manage-multiple-azure-subscriptions"></a>Organizowanie wielu subskrypcji platformy Azure i zarządzanie nimi

Jeśli masz tylko kilka subskrypcji, niezależne zarządzanie nimi jest stosunkowo proste. Jeśli jednak masz wiele subskrypcji, Utwórz hierarchię grup zarządzania ułatwiającą zarządzanie subskrypcjami i zasobami.

## <a name="azure-management-groups"></a>Grupy zarządzania platformy Azure

Grupy zarządzania platformy Azure umożliwiają wydajne zarządzanie dostępem, zasadami i zgodnością z subskrypcjami organizacji. Każda grupa zarządzania jest kontenerem dla co najmniej jednej subskrypcji.

Grupy zarządzania są uporządkowane w jednej hierarchii. Ta hierarchia jest definiowana w dzierżawie usługi Azure Active Directory (Azure AD) w celu dopasowania jej do struktury i potrzeb organizacji. Najwyższy poziom jest nazywany _główną grupą zarządzania_. W hierarchii można zdefiniować maksymalnie sześć poziomów grup zarządzania. Każda subskrypcja jest zawarta tylko w jednej grupie zarządzania.

Platforma Azure udostępnia cztery poziomy zakresu zarządzania:

- Grupy zarządzania
- Subskrypcje
- Grupy zasobów
- Zasoby

Każdy dostęp lub zasady zastosowane na jednym poziomie w hierarchii są dziedziczone przez niższe poziomy. Właściciel zasobu lub właściciel subskrypcji nie może zmienić odziedziczonych zasad. To ograniczenie pomaga ulepszyć zarządzanie.

> [!NOTE]
> Dziedziczenie tagów nie jest jeszcze obsługiwane, ale będzie dostępne wkrótce.

Ten model dziedziczenia umożliwia rozmieszczenie subskrypcji w hierarchii, tak aby każda subskrypcja była zgodna z odpowiednimi zasadami i zabezpieczeniami.

![Cztery poziomy zakresu do organizowania zasobów platformy Azure](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Każdy dostęp lub zasady w głównej grupie zarządzania dotyczy wszystkich zasobów w katalogu. Należy starannie rozważyć, które elementy są definiowane w tym zakresie. Należy uwzględnić tylko te przypisania, które muszą być dostępne.

## <a name="create-your-management-group-hierarchy"></a>Tworzenie hierarchii grup zarządzania

Podczas definiowania hierarchii grup zarządzania należy najpierw utworzyć główną grupę zarządzania. Następnie przenieś wszystkie istniejące subskrypcje z katalogu do głównej grupy zarządzania. Nowe subskrypcje są zawsze tworzone w głównej grupie zarządzania. Później można przenieść je do innej grupy zarządzania.

Przeniesienie subskrypcji do istniejącej grupy zarządzania powoduje, że dziedziczy zasad i przypisań ról z hierarchii grupy zarządzania powyżej. Po ustanowieniu wielu subskrypcji dla obciążeń platformy Azure Możesz utworzyć dodatkowe subskrypcje zawierające usługi platformy Azure, które są udostępniane przez inne subskrypcje.

Jeśli spodziewasz się, że środowisko platformy Azure zostanie powiększone, należy utworzyć grupy zarządzania dla produkcji i nieprodukcyjnej teraz oraz zastosować odpowiednie zasady i kontroli dostępu na poziomie grupy zarządzania. Nowe subskrypcje będą dziedziczyć odpowiednie kontrolki, gdy zostaną dodane do każdej grupy zarządzania.

![Przykład hierarchii grup zarządzania](../../_images/ready/management-group-hierarchy-v2.png)

## <a name="example-use-cases"></a>Przykładowe przypadki użycia

Podstawowe przykłady korzystania z grup zarządzania do rozdzielania różnych obciążeń:

- **Obciążenia produkcyjne i nieprodukcyjne:** Grupy zarządzania umożliwiają łatwiejsze zarządzanie różnymi rolami i zasadami między subskrypcjami produkcyjnymi i nieprodukcyjnymi. Na przykład subskrypcje nieprodukcyjne mogą przyznawać deweloperom dostęp współautorów, natomiast w przypadku deweloperów produkcyjnych mają dostęp tylko do czytnika.
- **Usługi wewnętrzne i usługi zewnętrzne:** Przedsiębiorstwa często mają różne wymagania, zasady i role dla usług wewnętrznych i zewnętrznych usług dostępnych dla klientów.

## <a name="related-resources"></a>Powiązane zasoby

Zapoznaj się z poniższymi zasobami, aby dowiedzieć się więcej na temat organizowania zasobów platformy Azure i zarządzania nimi.

- [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups)
- [Podnoszenie poziomu dostępu w celu zarządzania wszystkimi subskrypcjami platformy Azure i grupami zarządzania](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Przenoszenie zasobów platformy Azure do innej grupy zasobów lub subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [zalecanymi konwencjami nazewnictwa i tagowania](./naming-and-tagging.md), które warto stosować podczas wdrażania zasobów platformy Azure.

> [!div class="nextstepaction"]
> [Zalecane konwencje nazewnictwa i tagowania](./naming-and-tagging.md)
