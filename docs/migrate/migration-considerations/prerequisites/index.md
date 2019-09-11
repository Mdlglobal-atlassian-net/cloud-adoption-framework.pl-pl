---
title: Wymagania wstępne migracji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wymagania wstępne migracji
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 96ab62dc2adf17890989160c0af4fb80636b31b9
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818169"
---
# <a name="prerequisites-for-migration"></a>Wymagania wstępne dotyczące migracji

Przed rozpoczęciem migracji docelowe _środowisko_ migracji musi być przygotowane na nadchodzące zmiany. W tym przypadku środowisko oznacza podstawową infrastrukturę techniczną w chmurze. Środowisko oznacza również środowisko biznesowe i sposób myślenia o migracji. Podobnie środowisko obejmuje kulturę zespołów dokonujących zmiany i odbierających wyniki pracy. Brak przygotowania do tych zmian jest najczęstszą przyczyną niepowodzenia migracji. Ta seria artykułów poprowadzi Cię przez sugerowane wymagania wstępne w celu przygotowania środowiska.

## <a name="objective"></a>Cel

Zapewnienie gotowości przedsiębiorstwa, kultury i infrastruktury technicznej przed rozpoczęciem wykonywania iteracyjnego planu migracji.

## <a name="review-business-drivers"></a>Przegląd celów biznesowych

Przed rozpoczęciem jakiejkolwiek migracji do chmury należy zapoznać się ze wskazówkami dotyczącymi [planowania](../../../business-strategy/index.md) i [gotowości](../../../ready/index.md) w przewodniku Cloud Adoption Framework, aby upewnić się, że organizacja jest przygotowana na wdrożenie chmury i procesy migracji. W szczególności należy sprawdzić wymagania biznesowe i oczekiwane wyniki migracji:

- [Wprowadzenie: Migracja](../../../getting-started/migrate.md)
- [Dlaczego przechodzimy do chmury?](../../../business-strategy/motivations-why-are-we-moving-to-the-cloud.md)

## <a name="definition-of-done"></a>Definicja *gotowości*

Wymagania wstępne są spełnione, gdy spełnione są następujące warunki:

- **Gotowość biznesowa** Zespół ds. strategii w chmurze zdefiniował listę prac związanych z migracją wysokiego poziomu i określił ich priorytet w celu reprezentacji części infrastruktury cyfrowej przeznaczonej do migracji w ciągu następnych dwóch lub trzech wydań. Zespół ds. strategii w chmurze i zespół ds. wdrażania chmury uzgodnił początkową strategię zarządzania zmianami.
- **Gotowość kultury** Uzgodniono role, obowiązki i oczekiwania zespołu ds. wdrażania chmury, zespołu ds. strategii w chmurze oraz objętych użytkowników dotyczące obciążeń, które zostaną zmigrowane w ciągu następnych dwóch lub trzech wydań.
- **Gotowość techniczna** Strefa docelowa (lub przydzielone miejsce hostingowe w chmurze), do której zostaną przeniesione zmigrowane zasoby, spełnia minimalne wymagania dotyczące hostowania pierwszego migrowanego obciążenia.

> [!CAUTION]
> Przygotowanie jest kluczem do powodzenia migracji. Jednak nadmierne przygotowywania mogą prowadzić do *paraliżu analitycznego* polegającego na poświęcaniu zbyt dużej ilości czasu na planowanie, co może poważnie opóźnić migrację. Procesy i wymagania wstępne zdefiniowane w tej sekcji mają na celu ułatwienie podejmowania decyzji, ale nie należy pozwalać, aby uniemożliwiały czynienie rzeczywistych postępów.
>
> Do pierwszej migracji wybierz względnie proste obciążenie. Użyj procesów omówionych w tej sekcji, planując i wdrażając tę pierwszą migrację. Ta pierwsza migracja szybko zademonstruje zespołowi zasady dotyczące chmury i zmusi go do poznania działania chmury. W miarę zdobywania doświadczenia przez zespół należy wykorzystywać zdobytą wiedzę w ramach większych i bardziej złożonych migracji.

## <a name="accountability-during-prerequisites"></a>Odpowiedzialność w fazie wymagań wstępnych

Dwa zespoły są odpowiedzialne za gotowość w fazie wymagań wstępnych:

- **Zespół ds. strategii chmury:** Ten zespół jest odpowiedzialny za zidentyfikowanie i przydzielenie priorytetów do pierwszych dwóch lub trzech obciążeń będących kandydatami do migracji.
- **Zespół ds. wdrażania chmury:** Ten zespół jest odpowiedzialny za sprawdzenie gotowości środowiska technicznego i możliwości migracji proponowanych obciążeń.

Jeden członek każdego zespołu będzie odpowiedzialny za każdą z trzech definicji gotowości określonych w poprzedniej sekcji.

## <a name="responsibilities-during-prerequisites"></a>Obowiązki w fazie wymagań wstępnych

Oprócz odpowiedzialności wysokiego poziomu istnieją również akcje, za które powinny być bezpośrednio odpowiedzialne poszczególne osoby lub grupy. Poniżej przedstawiono kilka obowiązków, które mają wpływ na te działania:

- **Określanie priorytetów biznesowych** Podejmij decyzje biznesowe dotyczące migrowanych obciążeń i ogólnych ograniczeń czasowych. Aby uzyskać więcej informacji, zobacz temat [Cele biznesowe migracji do chmury](../../../business-strategy/motivations-why-are-we-moving-to-the-cloud.md).
- **Gotowość do zarządzania zmianami** Określ plan śledzenia zmian technicznych podczas migracji i poinformuj o nim. Więcej informacji na ten temat będzie dostępnych w III kwartale 2019 r.
- **Uzgadnianie stanowiska użytkowników biznesowych** Określ plan przygotowania społeczności użytkowników biznesowych na wykonanie migracji. Więcej informacji na ten temat będzie dostępnych w III kwartale 2019 r.
- **Spis i analiza infrastruktury cyfrowej** Wykonanie narzędzi wymaganych do utworzenia spisu i analizy infrastruktury cyfrowej. Aby uzyskać więcej informacji, zobacz omówienie [infrastruktury cyfrowej](../../../digital-estate/index.md) w przewodniku Cloud Adoption Framework.
- **Gotowość chmury** Oceń docelowe środowisko wdrażania, aby mieć pewność, że spełnia ono wymagania kilku pierwszych kandydujących obciążeń. Aby uzyskać więcej informacji, zobacz temat [Gotowość na platformę Azure — przewodnik](../../../ready/azure-readiness-guide/index.md).

Pozostałe artykuły w tej serii pomagają w wykonaniu poszczególnych czynności.

## <a name="next-steps"></a>Następne kroki

Po uzyskaniu ogólnej wiedzy na temat wymagań wstępnych można podjąć [wczesne decyzje dotyczące migracji](./decisions.md), aby spełnić pierwsze wymaganie wstępne.

> [!div class="nextstepaction"]
> [Wczesne decyzje dotyczące migracji](./decisions.md)
