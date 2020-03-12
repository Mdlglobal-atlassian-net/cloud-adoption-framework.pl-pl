---
title: Omówienie zarządzania platformą Azure
description: Poznaj przewodnik Cloud Adoption Framework dla platformy Azure dzięki tym informacjom o podstawowych narzędziach potrzebnych do zarządzania środowiskami produkcyjnymi platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b6d17a410c1903d984b5a1c756f51f7c5145ff9c
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140290"
---
::: zone target="docs"

# <a name="azure-management-guide-before-you-start"></a>Przewodnik po zarządzaniu platformą Azure: Przed rozpoczęciem

> [!NOTE]
> Ten przewodnik jest punktem wyjścia do wskazówek dotyczących innowacji w przewodniku Cloud Adoption Framework. Jest dostępny także w centrum Szybki start platformy Azure. Porada w dalszej części tego artykułu zawiera link do centrum Szybki start platformy Azure.

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Przed rozpoczęciem

::: zone-end

Przewodnik po zarządzaniu platformą Azure pomaga klientom platformy Azure w utworzeniu planu bazowego zarządzania w celu zapewnienia spójności zasobów na platformie Azure. Przedstawia podstawowe narzędzia potrzebne w każdym środowisku produkcyjnym platformy Azure, zwłaszcza takim, w którym hostowane są dane poufne. Aby uzyskać więcej informacji, najlepsze rozwiązania i informacje dotyczące przygotowywania środowiska w chmurze, zobacz [sekcję dotyczącą gotowości w przewodniku Cloud Adoption Framework](../index.md).

## <a name="scope-of-this-guide"></a>Zakres tego przewodnika

Ten przewodnik zawiera informacje na temat sposobu wyboru narzędzi na potrzeby planu bazowego zarządzania. Przedstawiono w nim również sposoby rozszerzania tego planu bazowego lub budowania odporności wykraczającej poza plan bazowy.

> [!div class="checklist"]
>
> - **Spis i widoczność:** Tworzenie spisu zasobów w wielu chmurach. Zwiększanie widoczności stanu uruchomienia każdego zasobu.
> - **Zgodność operacyjna:** Wprowadzanie mechanizmów kontroli i procesów zapewniających, że wszystkie stany są prawidłowo skonfigurowane i działają w dobrze zarządzanym środowisku.
> - **Ochrona i odzyskiwanie:** Zapewnianie, że wszystkie zarządzane zasoby są chronione i mogą zostać odzyskane za pomocą narzędzi uwzględnionych w planie bazowym zarządzania.
> - **Opcje rozszerzania planu bazowego:** Ocena typowych dodatków do planu bazowego dostosowanych do potrzeb biznesowych.
> - **Operacje platformy:** Rozszerzanie planu bazowego zarządzania z użyciem dobrze zdefiniowanego katalogu usług i centralnie zarządzanych platform.
> - **Operacje obciążeń:** Rozszerzanie planu bazowego zarządzania w celu koncentracji na obciążeniach o krytycznym znaczeniu.

## <a name="management-baseline"></a>Plan bazowy zarządzania

Plan bazowy zarządzania określa minimalny zestaw narzędzi i procesów, które należy stosować wobec wszystkich zasobów w środowisku. W planie bazowym zarządzania można uwzględnić również kilka opcji dodatkowych. Kilka kolejnych artykułów jest poświęconych przyspieszaniu wdrażania funkcji zarządzania w chmurze poprzez skupienie się na minimalnym wymaganym zestawie opcji zamiast na wszystkich opcjach, które są dostępne.

::: zone target="docs"

> [!TIP]
> Aby zapoznać się z tym przewodnikiem w środowisku interaktywnym, skorzystaj z witryny Azure Portal. Przejdź do [centrum Szybki start platformy Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) w witrynie Azure Portal, a następnie wybierz pozycję **Przewodnik po zarządzaniu platformą Azure**. Następnie postępuj zgodnie z instrukcjami krok po kroku.

Następny krok to [Spis i widoczność](./inventory.md).

::: zone-end

::: zone target="chromeless"

Ten przewodnik zawiera listę interaktywnych kroków, które umożliwiają wypróbowanie omawianych funkcji. Aby wrócić do miejsca, w którym przerwano pracę, przejdź do niego, korzystając z linków do stron nadrzędnych.

::: zone-end
