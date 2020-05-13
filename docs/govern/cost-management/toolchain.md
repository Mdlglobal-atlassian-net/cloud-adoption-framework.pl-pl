---
title: Narzędzia Cost Management na platformie Azure
description: Zobacz, jak narzędzia natywne platformy Azure mogą pomóc w dojrzałych zasadach i procesach, które obsługują dyscyplinę Cost Management.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6f2e08a85df87f7973f19ebd83b71de0f2003189
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220485"
---
# <a name="cost-management-tools-in-azure"></a>Narzędzia Cost Management na platformie Azure

[Dyscyplina Cost Management](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na sposobach tworzenia planów wydatków na chmurę, alokowania budżetów w chmurze, monitorowania i wymuszania budżetów w chmurze, wykrywania kosztów anomalii i dostosowywania planu ładu w chmurze, gdy rzeczywiste wydatki są niewyrównane.

Poniżej znajduje się lista narzędzi macierzystych platformy Azure, które mogą pomóc w zawczesnym wykorzystaniu zasad i procesów, które obsługują tę dyscyplinę.

<!-- TODO: Content packs are deprecated. -->

| Narzędzie | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/cost-management-billing-overview)  | [Pakiet zawartości platformy Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
| Umowa Enterprise jest wymagane?     | Nie         | Nie         | Yes         | Nie         |
| Kontrola budżetu     | Nie         | Yes         | Nie         | Yes         |
| Monitoruj wydatki dotyczące pojedynczego zasobu    | Tak         | Tak         | Yes         | Nie         |
| Monitorowanie wydatków w wielu zasobach    | Nie         | Yes        | Yes         | Nie         |
| Kontrola wydatków w ramach pojedynczego zasobu     | Tak — rozmiar ręczny         | Yes         | Nie         | Yes         |
| Wymuś wydatki dla wielu zasobów    | Nie         | Yes         | Nie         | Yes         |
| Wymuszaj metadane ewidencjonowania aktywności zasobów    | Nie         | Nie         | Nie         | Yes         |
| Monitorowanie i wykrywanie trendów     | Tak          | Tak        | Yes         | Nie         |
| Wykrywanie anomalii wydatków     | Nie         | Yes        | Yes         | Nie        |
| Odchylenia Socialize     | Nie        | Yes        | Yes        | Nie        |
