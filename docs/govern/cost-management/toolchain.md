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
ms.openlocfilehash: a440cd0b73fc55e97fa6dc957ab08e39c9dbca1e
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862351"
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
