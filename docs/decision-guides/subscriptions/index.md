---
title: Przewodnik po decyzjach związanych z subskrypcjami
description: Zapoznaj się z wzorcami projektowymi subskrypcji i grupami zarządzania jako podstawową usługą do organizowania zasobów podczas migracji na platformę Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: f00377f4da5a3c95114571af36e4a759a26c63f3
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707955"
---
# <a name="subscription-decision-guide"></a>Przewodnik po decyzjach związanych z subskrypcjami

Skuteczny projekt subskrypcji ułatwia organizacjom ustanowienie struktury do organizowania zasobów na platformie Azure podczas wdrażania chmury.

Każdy zasób na platformie Azure, taki jak maszyna wirtualna lub baza danych, jest skojarzony z subskrypcją. Wdrażanie platformy Azure rozpoczyna się od utworzenia subskrypcji platformy Azure, skojarzenia jej z kontem i wdrożenia zasobów w subskrypcji. Omówienie tych pojęć przedstawiono w temacie [Azure fundamental concepts](../../ready/considerations/fundamental-concepts.md) (Podstawowe pojęcia dotyczące platformy Azure).

Wraz z rozwojem Twojej infrastruktury cyfrowej na platformie Azure będzie prawdopodobnie konieczne utworzenie dodatkowych subskrypcji w celu spełnienia wymagań. Platforma Azure umożliwia definiowanie hierarchii grup zarządzania do organizowania subskrypcji i łatwego stosowania właściwych zasad do odpowiednich zasobów. Aby uzyskać więcej informacji, zobacz [Scaling with multiple Azure subscriptions](../../ready/azure-best-practices/scaling-subscriptions.md) (Skalowanie z wieloma subskrypcjami platformy Azure).

Podstawowe przykłady korzystania z grup zarządzania do rozdzielania różnych obciążeń:

- **Obciążenia produkcyjne a nieprodukcyjne:** niektóre przedsiębiorstwa tworzą grupy zarządzania, aby oddzielić subskrypcje produkcyjne i nieprodukcyjne. Grupy zarządzania jeszcze bardziej ułatwiają tym klientom zarządzanie rolami i zasadami. Na przykład subskrypcja nieprodukcyjna może umożliwić deweloperom dostęp typu **Współautor**, ale w środowisku produkcyjnym mają tylko dostęp typu **Czytelnik**.
- **Usługi wewnętrzne a usługi zewnętrzne:** bardzo podobnie jak w przypadku obciążeń środowisk produkcyjnych i nieprodukcyjnych przedsiębiorstwa często mają różne wymagania, zasady i role dla usług wewnętrznych w porównaniu z usługami zewnętrznymi przeznaczonymi dla klientów.

Ten przewodnik po podejmowaniu decyzji pomaga rozważyć różne podejścia do organizowania hierarchii grup zarządzania.

## <a name="subscription-design-patterns"></a>Wzorce projektowe subskrypcji

Każda organizacja jest inna, dlatego grupy zarządzania platformy Azure są elastyczne. Modelowanie infrastruktury chmury tak, aby odzwierciedlała hierarchię organizacji, pomaga w definiowaniu oraz stosowaniu zasad na wyższych poziomach hierarchii i poleganiu na dziedziczeniu jako na mechanizmie zapewniania, że te zasady będą automatycznie stosowane do grup zarządzania niżej w hierarchii. Chociaż subskrypcje można przenosić między różnymi grupami zarządzania, dobrze jest zaprojektować wstępną hierarchię grup zarządzania odzwierciedlającą przewidywane potrzeby organizacji.

Przed zakończeniem projektu subskrypcji należy zastanowić się, jak decyzje dotyczące [spójności zasobów](../resource-consistency/index.md) mogą wpływać na wybory tych elementów.

> [!NOTE]
> Umowy Enterprise Agreement (EA) platformy Azure umożliwiają definiowanie innej hierarchii organizacji na potrzeby rozliczeń. Ta hierarchia różni się od hierarchii grup zarządzania, która zapewnia model dziedziczenia na potrzeby łatwego stosowania odpowiednich zasad i mechanizmów kontroli dostępu do zasobów.

Poniższe wzorce subskrypcji odzwierciedlają wstępny wzrost stopnia zaawansowania projektów subskrypcji. Dalej przedstawiono kilka bardziej zaawansowanych hierarchii, które mogą dobrze pasować do Twojej organizacji:

### <a name="single-subscription"></a>Subskrypcja pojedyncza

Subskrypcja pojedyncza na konto może być wystarczająca w przypadku organizacji, które muszą wdrażać małą liczbę zasobów hostowanych w chmurze. Jest to pierwszy wzorzec subskrypcji, który jest implementowany po rozpoczęciu procesu wdrażania chmury, co pozwala na małe wdrożenia eksperymentalne lub wdrożenia na potrzeby weryfikacji koncepcji wdrożeń. Umożliwiają one eksplorowanie możliwości chmury.

### <a name="production-and-nonproduction-pattern"></a>Wzorzec dla środowiska produkcyjnego i nieprodukcyjnego

Gdy wszystko będzie gotowe do wdrożenia obciążenia w środowisku produkcyjnym, należy dodać kolejną subskrypcję. Dzięki temu można oddzielić produkcyjne dane i inne zasoby od środowisk tworzenia i opracowywania. Do zasobów w dwóch subskrypcjach można również łatwo stosować dwa różne zestawy zasad.

![Wzorzec subskrypcji dla środowiska produkcyjnego i przedprodukcyjnego](../../_images/ready/basic-subscription-model.png)

### <a name="workload-separation-pattern"></a>Wzorzec z rozdzieleniem obciążeń

W miarę tego, jak organizacja dodaje nowe obciążenia w chmurze, oddzielne własności subskrypcji lub podstawowe oddzielenie odpowiedzialności może spowodować powstanie wielu subskrypcji w grupach zarządzania w środowisku zarówno produkcyjnym, jak i nieprodukcyjnym. Chociaż to podejście zapewnia podstawowe oddzielenie obciążeń, nie pozwala w znacznym stopniu wykorzystać modelu dziedziczenia, aby automatycznie stosować zasady do podzestawu subskrypcji.

![Wzorzec z rozdzieleniem obciążeń](../../_images/ready/management-group-hierarchy.png)

### <a name="application-category-pattern"></a>Wzorzec kategorii aplikacji

Wraz z rozwojem infrastruktury chmurowej organizacji są zazwyczaj tworzone dodatkowe subskrypcje w celu obsługi aplikacji, które znacząco różnią się pod względem stopnia krytyczności dla działania firmy, wymagań dotyczących zgodności, opcji kontroli dostępu lub potrzeb związanych z ochroną danych. W ramach podejścia stanowiącego rozwinięcie wzorca z subskrypcjami dla środowiska produkcyjnego i nieprodukcyjnego te kategorie subskrypcji są zorganizowane w ramach grup zarządzania środowiska produkcyjnego lub nieprodukcyjnego. Subskrypcje te zazwyczaj należą do personelu centralnego zespołu ds. operacji informatycznych i są przez niego administrowane.

![Wzorzec kategorii aplikacji](../../_images/infra-subscriptions/application.png)

Każda organizacja wybierze inny sposób kategoryzowania aplikacji, często oddzielając subskrypcje na podstawie określonych aplikacji lub usług albo wzdłuż linii archetypów aplikacji. Ta kategoryzacja jest często projektowana z myślą o obsłudze obciążeń, które będą prawdopodobnie zużywać większość limitów zasobów subskrypcji, albo osobnych obciążeń o kluczowym znaczeniu, aby upewnić się, że nie są one konkurencyjne względem innych obciążeń w ramach tych limitów. Niektóre obciążenia, które mogą uzasadniać oddzielną subskrypcję w ramach tego wzorca, to:

- Obciążenia niezbędne dla działalności.
- Aplikacje, które są częścią kosztu własnego sprzedaży (COGS, Cost of Goods Sold) w firmie. Przykład: każde wystąpienie widżetu firmy X zawiera moduł Azure IoT, który wysyła dane telemetryczne. Może to wymagać dedykowanej subskrypcji dla celów księgowości i zarządzania w ramach kosztu własnego sprzedaży.
- Aplikacje podlegają wymogom prawnym, takim jak ustawy HIPAA lub FedRAMP.

### <a name="functional-pattern"></a>Wzorzec funkcjonalny

Ten wzorzec funkcjonalny organizuje subskrypcje i konta wzdłuż linii funkcjonalnych, takich jak obsługa finansów, sprzedaży lub infrastruktury informatycznej, używając hierarchii grup zarządzania.

### <a name="business-unit-pattern"></a>Wzorzec jednostki biznesowej

Ten wzorzec jednostki biznesowej grupuje subskrypcje i konta na podstawie kategorii zysków i strat, jednostki biznesowej, działu, centrum zysków lub podobnej struktury biznesowej przy użyciu hierarchii grup zarządzania.

### <a name="geographic-pattern"></a>Wzorzec geograficzny

W przypadku organizacji przeprowadzających operacje globalne ten wzorzec geograficzny grupuje subskrypcje i konta na podstawie regionów geograficznych, używając hierarchii grup zarządzania.

## <a name="mixed-patterns"></a>Wzorce mieszane

Hierarchie grup zarządzania mogą mieć do sześciu poziomów głębokości. Zapewnia to elastyczność pozwalającą na utworzenie hierarchii, która łączy kilka z tych wzorców, w celu spełnienia potrzeb konkretnej organizacji. Na przykład poniższy diagram przedstawia hierarchię organizacji łączącą wzorzec jednostki biznesowej z wzorcem geograficznym.

![Wzorzec subskrypcji mieszanej](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Powiązane zasoby

- [Resource access management in Azure](../../govern/resource-consistency/resource-access-management.md) (Zarządzanie dostępem do zasobów na platformie Azure)
- [Multiple layers of governance in large enterprises](../../govern/guides/complex/multiple-layers-of-governance.md) (Wiele warstw nadzoru w dużych przedsiębiorstwach)
- [Multiple geographic regions](../regions/index.md) (Wiele regionów geograficznych)

## <a name="next-steps"></a>Następne kroki

Projekt subskrypcji to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
