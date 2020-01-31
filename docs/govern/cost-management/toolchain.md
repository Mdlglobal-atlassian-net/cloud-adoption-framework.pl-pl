---
title: Narzędzia Cost Management na platformie Azure
description: Narzędzia Cost Management na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e35530fbf3a858c000cb78c0c076d7d56d5fbd86
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806411"
---
# <a name="cost-management-tools-in-azure"></a>Narzędzia Cost Management na platformie Azure

[Cost Management](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na sposobach tworzenia planów wydatków na chmurę, alokowania budżetów w chmurze, monitorowania i wymuszania budżetów w chmurze, wykrywania kosztów anomalii i dostosowywania planu ładu w chmurze, gdy rzeczywiste wydatki są niewyrównane.

Poniżej znajduje się lista narzędzi macierzystych platformy Azure, które mogą pomóc w zawczesnym wykorzystaniu zasad i procesów, które obsługują tę dyscyplinę ładu.

| Narzędzie | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Pakiet zawartości platformy Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Umowa Enterprise jest wymagane?     | Nie         | Nie         | Tak         | Nie         |
|Kontrola budżetu     | Nie         | Tak         | Nie         | Tak         |
|Monitoruj wydatki dotyczące pojedynczego zasobu    | Tak         | Tak         | Tak         | Nie         |
|Monitorowanie wydatków w wielu zasobach    | Nie         | Tak        | Tak         | Nie         |
|Kontrola wydatków w ramach pojedynczego zasobu     | Tak — rozmiar ręczny         | Tak         | Nie         | Tak         |
|Wymuś wydatki dla wielu zasobów    | Nie         | Tak         | Nie         | Tak         |
|Wymuszaj metadane ewidencjonowania aktywności zasobów    | Nie         | Nie         | Nie         | Tak         |
|Monitorowanie i wykrywanie trendów     | Tak          | Tak        | Tak         | Nie         |
|Wykrywanie anomalii wydatków     | Nie         | Tak        | Tak         | Nie        |
|Odchylenia Socialize     | Nie        | Tak        | Tak        | Nie        |
