---
title: Model operacyjny chmury to teraz Microsoft Cloud Framework wdrażania dla platformy Azure
description: Dowiedz się więcej o korzystaniu z rozwiązań w zakresie modeli operacyjnych w chmurze w ramach struktury wdrażania w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 8d9bce8b12b3054c2f4a6aa0421e1d30d5011860
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819987"
---
# <a name="cloud-operating-model-is-now-part-of-the-microsoft-cloud-adoption-framework-for-azure"></a>Model operacyjny chmury jest teraz częścią platformy wdrażania Microsoft Cloud dla systemu Azure

Na początku 2018 firma Microsoft wyudostępniła model operacyjny w chmurze (COM). Model COM był przewodnikiem, który pomaga klientom zrozumieć **znaczenie** i **przyczynę** transformacji cyfrowej. Dzięki temu klienci mogą poznać wszystkie obszary, które są potrzebne do rozprowadzenia: strategii biznesowej, strategii kulturowej i strategii technologicznej. Co nie zostało uwzględnione w modelu COM, a to _, co_pozostało, co pozostało w tym miejscu?

W październiku 2018 rozpocząłmy przegląd wszystkich modeli, które zostały rozdzielone przez społeczność firmy Microsoft. znaleźliśmymy w 60 przybliżeniu różne modele wdrażania w chmurze. Zespół międzyfirmowy został opracowany w celu przełączenia wszystkiego ze sobą jako dedykowanego "produktu" ze zdefiniowanymi implementacjami w ramach usług, sprzedaży i marketingu. Ten nakład pracy culminated w tworzeniu jednego modelu, Microsoft Cloud Framework wdrażania dla platformy Azure, który ułatwia klientom zrozumienie tego, **co** i **dlaczego** i zapewnianie ujednoliconych wskazówek dotyczących sposobu, w **jaki** ułatwia im przyspieszenie Wdrażanie w chmurze. Celem tego projektu jest utworzenie jednego podejścia firmy Microsoft do wdrażania w chmurze.

## <a name="using-cloud-operating-model-practices-within-the-cloud-adoption-framework"></a>Korzystanie z rozwiązań modelu operacyjnego w chmurze w ramach struktury wdrażania chmury

W przypadku podobnego podejścia do modelu COM Czytelnicy powinni zacząć z jedną z następujących czynności:

- [Wprowadzenie do migracji do chmury](../getting-started/migrate.md)
- [Wprowadzenie do innowacji z obsługą chmury](../getting-started/innovate.md)
- [Pomyślne włączenie wdrażania](../getting-started/enable.md)

Wskazówki podane wcześniej w modelu COM nadal dotyczą struktury wdrażania chmury. Środowisko jest inne, ale struktura wdrożenia chmury jest po prostu rozszerzeniem tych wskazówek. Aby przejść z modelu COM do struktury wdrażania w chmurze, rozumiesz zakres i strukturę. W poniższych dwóch sekcjach opisano przechodzenie.

## <a name="scope"></a>Scope

COM ustanowił zakres składający się z następujących składników:

![Zakres struktury wdrażania chmury](../_images/caf-scope.png)

- **Strategia biznesowa:** Ustanów jasne cele biznesowe i wyniki, które mają być obsługiwane przez wdrażanie w chmurze.
- **Strategia technologiczna:** Wyrównaj strategię przenoszącą, aby zastanowić się nad przyjęciem chmury w celu dostosowania jej do strategii biznesowej.
- **Strategia dla osób:** Opracowuj strategię do uczenia się osób i zmieniania kultury, aby umożliwić sukces firmy.

Zakresy wysokiego poziomu modelu operacyjnego chmury i struktury wdrażania chmury są podobne. Firma, kultura i technologia są odzwierciedlone we wszystkich wskazówkach i każdej metodologii w ramach struktury wdrażania w chmurze.

> [!NOTE]
> Zakres struktury wdrażania chmury ma dwa znaczące punkty przejrzystości. W strukturze wdrażania w chmurze, Strategia biznesowa wykracza poza dokumentację kosztów&mdash;chmury, która ma na celu zrozumienie motywacji, pożądanych wyników, zwrotów i kosztów związanych z chmurą w celu utworzenia planów akcji i jasnego uzasadnienia biznesowego. W strukturze wdrażania w chmurze, strategia osób wykracza poza szkolenie, aby uwzględnić podejścia, które tworzą oczywisty termin zapadalności w kulturze. Kilka obszarów planu zawiera pokazy wpływu zarządzania Agile, integrację z DevOps, empatię klienta i Obsession, a także podejścia do tworzenia produktów w ramach produkcji.

## <a name="structure"></a>Struktura

COM zawiera Grafika informacyjna, w którym przedstawiono różne decyzje i akcje, które należy wykonać w trakcie działania w chmurze. Ta ilustracja zapewniała wyraźny sposób komunikowania się z następnymi krokami i decyzjami zależnymi.

Struktura wdrażania chmury jest zgodna z modelem podobnym. Jednak w miarę jak akcje i decyzje zostały rozwinięte w wielu drzewach decyzyjnych, złożoność szybko przetworzy jeden widok graficzny. Aby uprościć wskazówki i zwiększyć jej natychmiastową akcję, pojedyncza Grafika została rozmieszczona w następujących strukturach.

Na poziomie kierownictwa struktura wdrażania chmury została uproszczona w następujących trzech etapach wdrażania i dwóch podstawowych przewodników ładu.

![Struktura poziomu wykonawczego struktury wdrażania chmury](../_images/caf-structure.png)

Trzy etapy wdrażania to:

- **Zamierza** Zaplanuj plan biznesowy, aby zaprojektować wdrażanie w chmurze w celu wyrównania z żądanymi wynikami biznesowymi.
- **Gotowe** Przygotuj osoby, organizację i środowisko techniczne do wykonania planu wdrażania.
- **Wdrażanie:** Strategia techniczna wymagana do wykonania konkretnego planu wdrożenia w celu wyrównania z konkretną podróżą w celu realizacji wyników działalności biznesowej.

Trzy etapy wdrażania w chmurze zostały zamapowane na dwie konkretne podróże:

- [Migracja](../getting-started/migrate.md): Przenieś istniejące obciążenia do chmury.
- [Innowacje](../getting-started/innovate.md): Modernizacja istniejących obciążeń i tworzenie nowych produktów i usług.

Dodatkowe zasoby wymagane do pomyślnego wdrożenia chmury można znaleźć w temacie [Włączanie powodzenia wdrażania](../getting-started/enable.md).

## <a name="next-steps"></a>Następne kroki

Aby wznowić podróż, w której pozostał port COM, wybierz jedną z następujących kursów wdrażania w chmurze:

- [Wprowadzenie do migracji do chmury](../getting-started/migrate.md)
- [Wprowadzenie do innowacji z obsługą chmury](../getting-started/innovate.md)
- [Pomyślne włączenie wdrażania](../getting-started/enable.md)
