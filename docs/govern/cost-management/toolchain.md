---
title: Narzędzia Cost Management na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia Cost Management na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3b301f8dfcc50539f4325901cd32553368a0da55
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222636"
---
# <a name="cost-management-tools-in-azure"></a>Narzędzia Cost Management na platformie Azure

[Cost Management](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na sposobach tworzenia planów wydatków na chmurę, alokowania budżetów w chmurze, monitorowania i wymuszania budżetów w chmurze, wykrywania kosztów anomalii i dostosowywania planu ładu w chmurze, gdy rzeczywiste wydatki są niewyrównane.

Poniżej znajduje się lista narzędzi macierzystych platformy Azure, które mogą pomóc w zawczesnym wykorzystaniu zasad i procesów, które obsługują tę dyscyplinę ładu.

| Tool | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Pakiet zawartości platformy Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|Umowa Enterprise jest wymagane?     | Nie         | Nie         | Yes         | Nie         |
|Kontrola budżetu     | Nie         | Yes         | Nie         | Tak         |
|Monitoruj wydatki dotyczące pojedynczego zasobu    | Tak         | Yes         | Yes         | Nie         |
|Monitorowanie wydatków w wielu zasobach    | Nie         | Yes        | Yes         | Nie         |
|Kontrola wydatków w ramach pojedynczego zasobu     | Tak — rozmiar ręczny         | Tak         | Nie         | Tak         |
|Wymuś wydatki dla wielu zasobów    | Nie         | Yes         | Nie         | Tak         |
|Wymuszaj metadane ewidencjonowania aktywności zasobów    | Nie         | Nie         | Nie         | Tak         |
|Monitorowanie i wykrywanie trendów     | Tak          | Yes        | Yes         | Nie         |
|Wykrywanie anomalii wydatków     | Nie         | Yes        | Yes         | Nie        |
|Odchylenia Socialize     | Nie        | Yes        | Yes        | Nie        |
