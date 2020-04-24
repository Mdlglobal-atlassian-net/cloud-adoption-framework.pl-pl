---
title: Model operacyjny chmury to teraz platforma wdrażania w chmurze dla platformy Azure
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, co, dlaczego i jak przyspieszać Wdrażanie chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d1ba5e26214a0b60a4fe9fefb23d1dffaf8fa4ed
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "79023866"
---
# <a name="cloud-operating-model-is-now-part-of-the-microsoft-cloud-adoption-framework-for-azure"></a>Model operacyjny chmury jest teraz częścią platformy wdrażania Microsoft Cloud dla systemu Azure

Na początku 2018 roku firma Microsoft udostępniła przewodnik Cloud Operating Model (COM). Model COM był przewodnikiem, który pomaga klientom zrozumieć **znaczenie** i **przyczynę** transformacji cyfrowej. Dzięki temu klienci mogą poznać wszystkie obszary, które są potrzebne do rozprowadzenia: strategii biznesowej, strategii kulturowej i strategii technologicznej. Co nie zostało uwzględnione w modelu COM, były konkretnymi krokami, _do_ których pozostali klienci zastanawiali się w tym miejscu? ".

W październiku 2018 rozpocząłmy przegląd wszystkich modeli, które zostały rozdzielone przez społeczność firmy Microsoft. znaleźliśmymy w 60 przybliżeniu różne modele wdrażania w chmurze. Zespół międzyfirmowy został opracowany w celu przełączenia wszystkiego ze sobą jako dedykowanego "produktu" ze zdefiniowanymi implementacjami w ramach usług, sprzedaży i marketingu. Ten nakład pracy culminated przy tworzeniu jednego modelu, Microsoft Cloud Framework wdrażania dla platformy Azure, zaprojektowany w celu ułatwienia klientom zrozumienia tego, **co** i **dlaczego** i zapewnić ujednolicone wskazówki dotyczące tego, **jak** ułatwić im przyspieszenie wdrożenia chmury. Celem tego projektu jest utworzenie jednego podejścia firmy Microsoft do wdrażania w chmurze.

## <a name="using-cloud-operating-model-practices-within-the-cloud-adoption-framework"></a>Korzystanie z rozwiązań modelu operacyjnego w chmurze w ramach struktury wdrażania chmury

W przypadku podobnego podejścia do modelu COM Czytelnicy powinni zacząć z jedną z następujących czynności:

- [Rozpoczęcie podróży migracji do chmury](../getting-started/migrate.md)
- [Wprowadzanie innowacji poprzez wdrażanie w chmurze](../getting-started/innovate.md)
- [Zapewnianie pomyślnego wdrożenia chmury](../getting-started/enable.md)

Wskazówki podane wcześniej w modelu COM nadal dotyczą struktury wdrażania chmury. Środowisko jest inne, ale struktura wdrożenia chmury jest po prostu rozszerzeniem tych wskazówek. Aby przejść z modelu COM do struktury wdrażania w chmurze, rozumiesz zakres i strukturę. W poniższych dwóch sekcjach opisano przechodzenie.

## <a name="scope"></a>Zakres

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

- **Plan:** Zaplanuj plan biznesowy, aby zaprojektować wdrażanie w chmurze w celu wyrównania z żądanymi wynikami biznesowymi.
- **Gotowe:** Przygotuj osoby, organizację i środowisko techniczne do wykonania planu wdrażania.
- **Zastosuj:** Strategia techniczna wymagana do wykonania konkretnego planu wdrożenia w celu wyrównania z konkretną podróżą w celu realizacji wyników działalności biznesowej.

Trzy etapy wdrażania w chmurze zostały zamapowane na dwie konkretne podróże:

- [Migrowanie](../getting-started/migrate.md): Przenieś istniejące obciążenia do chmury.
- [Innowacje](../getting-started/innovate.md): modernizowanie istniejących obciążeń i tworzenie nowych produktów i usług.

Dodatkowe zasoby wymagane do pomyślnego wdrożenia chmury można znaleźć w temacie [Włączanie powodzenia wdrażania](../getting-started/enable.md).

## <a name="next-steps"></a>Następne kroki

Aby wznowić podróż, w której pozostał port COM, wybierz jedną z następujących kursów wdrażania w chmurze:

- [Wprowadzenie do migracji do chmury](../getting-started/migrate.md)
- [Wprowadzenie do innowacji z obsługą chmury](../getting-started/innovate.md)
- [Pomyślne włączenie wdrażania](../getting-started/enable.md)
