---
title: Przewodnik po decyzjach związanych z subskrypcjami
description: Informacje o strategiach projektowania subskrypcji i hierarchii grup zarządzania w celu organizowania zasobów platformy Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 515ae94c2feedbc7b111ec786551a4680a69f561
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80996020"
---
# <a name="subscription-decision-guide"></a>Przewodnik po decyzjach związanych z subskrypcjami

Efektywny projekt subskrypcji ułatwia organizacjom ustanowienie struktury do organizowania zasobów na platformie Azure podczas wdrażania chmury i zarządzania nimi. Ten przewodnik pomoże Ci zdecydować, kiedy utworzyć dodatkowe subskrypcje i rozszerzyć hierarchię grup zarządzania, aby wspierać priorytety firmy.

## <a name="prerequisites"></a>Wymagania wstępne

Wdrażanie platformy Azure rozpoczyna się od utworzenia subskrypcji platformy Azure, skojarzenia jej z kontem i wdrożenia w niej zasobów, takich jak maszyny wirtualne i bazy danych. Omówienie tych pojęć przedstawiono w temacie [Azure fundamental concepts](../../ready/considerations/fundamental-concepts.md) (Podstawowe pojęcia dotyczące platformy Azure).

- [Utwórz początkowe subskrypcje.](../../ready/azure-best-practices/initial-subscriptions.md)
- [Utwórz dodatkowe subskrypcje](../../ready/azure-best-practices/scale-subscriptions.md) w celu skalowania środowiska platformy Azure.
- [Organizuj subskrypcje i zarządzaj nimi](../../ready/azure-best-practices/organize-subscriptions.md), korzystając z grup zarządzania platformy Azure.

## <a name="modeling-your-organization"></a>Modelowanie organizacji

Każda organizacja jest inna, dlatego grupy zarządzania platformy Azure są elastyczne. Modelowanie infrastruktury chmury tak, aby odzwierciedlała hierarchię organizacji, pomaga w definiowaniu oraz stosowaniu zasad na wyższych poziomach hierarchii i poleganiu na dziedziczeniu jako na mechanizmie zapewniania, że te zasady będą automatycznie stosowane do grup zarządzania niżej w hierarchii. Chociaż subskrypcje można przenosić między różnymi grupami zarządzania, dobrze jest zaprojektować wstępną hierarchię grup zarządzania odzwierciedlającą przewidywane potrzeby organizacji.

Przed zakończeniem projektu subskrypcji należy zastanowić się, jak decyzje dotyczące [spójności zasobów](../resource-consistency/index.md) mogą wpływać na wybory tych elementów.

> [!NOTE]
> Umowy Enterprise Agreement (EA) platformy Azure umożliwiają definiowanie innej hierarchii organizacji na potrzeby rozliczeń. Ta hierarchia różni się od hierarchii grup zarządzania, która zapewnia model dziedziczenia na potrzeby łatwego stosowania odpowiednich zasad i mechanizmów kontroli dostępu do zasobów.

## <a name="subscription-design-strategies"></a>Strategie projektowania subskrypcji

Rozważ następujące strategie projektowania subskrypcji, aby sprostać priorytetom biznesowym.

### <a name="workload-separation-strategy"></a>Strategia rozdzielania obciążeń

W miarę tego, jak organizacja dodaje nowe obciążenia w chmurze, oddzielne własności subskrypcji lub podstawowe oddzielenie odpowiedzialności może spowodować powstanie wielu subskrypcji w grupach zarządzania w środowisku zarówno produkcyjnym, jak i nieprodukcyjnym. Chociaż to podejście zapewnia podstawowe oddzielenie obciążeń, nie pozwala w znacznym stopniu wykorzystać modelu dziedziczenia, aby automatycznie stosować zasady do podzestawu subskrypcji.

![Strategia rozdzielania obciążeń](../../_images/ready/management-group-hierarchy-v2.png)

### <a name="application-category-strategy"></a>Strategia kategorii aplikacji

Wraz z rozwojem infrastruktury chmurowej organizacji są zazwyczaj tworzone dodatkowe subskrypcje w celu obsługi aplikacji, które znacząco różnią się pod względem stopnia krytyczności dla działania firmy, wymagań dotyczących zgodności, opcji kontroli dostępu lub potrzeb związanych z ochroną danych. Tworzone na podstawie początkowych subskrypcji środowiska produkcyjnego i nieprodukcyjnego subskrypcje obsługujące te kategorie aplikacji są odpowiednio zorganizowane w ramach grup zarządzania środowiska produkcyjnego lub nieprodukcyjnego. Subskrypcje te zazwyczaj należą do personelu centralnego zespołu ds. operacji informatycznych i są przez niego administrowane.

![Strategia kategorii aplikacji](../../_images/infra-subscriptions/application.png)

Każda organizacja wybierze inny sposób kategoryzowania aplikacji, często oddzielając subskrypcje na podstawie określonych aplikacji lub usług albo wzdłuż linii archetypów aplikacji. Ta kategoryzacja jest często projektowana z myślą o obsłudze obciążeń, które będą prawdopodobnie zużywać większość limitów zasobów subskrypcji, albo osobnych obciążeń o kluczowym znaczeniu, aby upewnić się, że nie są one konkurencyjne względem innych obciążeń w ramach tych limitów. Niektóre obciążenia, które mogą uzasadniać oddzielną subskrypcję, to:

- Obciążenia niezbędne dla działalności.
- Aplikacje, które są częścią kosztu własnego sprzedaży (COGS, Cost of Goods Sold) w firmie. Przykład: każde wystąpienie widżetu firmy X zawiera moduł Azure IoT, który wysyła dane telemetryczne. Może to wymagać dedykowanej subskrypcji dla celów księgowości i zarządzania w ramach kosztu własnego sprzedaży.
- Aplikacje podlegają wymogom prawnym, takim jak ustawy HIPAA lub FedRAMP.

### <a name="functional-strategy"></a>Strategia funkcjonalna

Strategia funkcjonalna organizuje subskrypcje i konta wzdłuż linii funkcjonalnych, takich jak obsługa finansów, sprzedaży lub infrastruktury informatycznej, używając hierarchii grup zarządzania.

### <a name="business-unit-strategy"></a>Strategia jednostki biznesowej

Strategia jednostki biznesowej grupuje subskrypcje i konta na podstawie kategorii zysków i strat, jednostki biznesowej, działu, centrum zysków lub podobnej struktury biznesowej przy użyciu hierarchii grup zarządzania.

### <a name="geographic-strategy"></a>Strategia geograficzna

W przypadku organizacji prowadzących globalną działalność strategia geograficzna grupuje subskrypcje i konta na podstawie regionów geograficznych, używając hierarchii grup zarządzania.

## <a name="mixing-subscription-strategies"></a>Mieszanie strategii subskrypcji

Hierarchie grup zarządzania mogą mieć do sześciu poziomów głębokości. Zapewnia to elastyczność pozwalającą na utworzenie hierarchii, która łączy kilka z tych strategii, w celu spełnienia potrzeb konkretnej organizacji. Na przykład poniższy diagram przedstawia hierarchię organizacji łączącą strategię jednostki biznesowej ze strategią geograficzną.

![Mieszana strategia subskrypcji](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Powiązane zasoby

- [Resource access management in Azure](../../govern/resource-consistency/resource-access-management.md) (Zarządzanie dostępem do zasobów na platformie Azure)
- [Multiple layers of governance in large enterprises](../../govern/guides/complex/multiple-layers-of-governance.md) (Wiele warstw nadzoru w dużych przedsiębiorstwach)
- [Multiple geographic regions](../../migrate/azure-best-practices/multiple-regions.md) (Wiele regionów geograficznych)

## <a name="next-steps"></a>Następne kroki

Projekt subskrypcji to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać dodatkowe strategie używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
