---
title: Metodologia zarządzania dla chmury
description: Użyj podejścia do ładu przyrostowego opartego na minimalnym żywotnym produkcie (MVP), aby zapewnić obsługę zasad firmowych i szybko przejść do wdrożenia chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 3bfade6fee8d07b068165f4148ed134273d646f9
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83754393"
---
# <a name="govern-methodology-for-the-cloud"></a>Metodologia zarządzania dla chmury

Wdrażanie chmury to podróż, a nie cel. Po drodze istnieją wyraźne kamienie milowe i wymierne korzyści biznesowe. Ostatni stan wdrożenia chmury jest nieznany, gdy firma zacznie podróżować. Zarządzanie w chmurze pozwala utworzyć zabezpieczenia, dzięki którym firma będzie na odpowiedniej ścieżce podczas całej podróży.

Struktura wdrażania w chmurze zawiera przewodniki ładu, które opisują środowiska fikcyjnych firm, które są oparte na doświadczeniach rzeczywistych klientów. Każdy przewodnik polega na podążaniu za klientem podczas związanych z nadzorem aspektów wdrażania chmury.

## <a name="envision-an-end-state"></a>Przewidywanie stanu końcowego

Podróż bez celu to tylko tułaczka. Ważne jest, aby przed wykonaniem pierwszego kroku ustalić nieaktualną wizję stanu końcowego. Na następującej grafice informacyjnej przedstawiono układ odniesienia dla stanu końcowego. To nie jest punkt początkowy, ale pokazuje potencjalne miejsce docelowe.

![Grafika informacyjna dotycząca modelu nadzoru z przewodnika Cloud Adoption Framework](../_images/operational-transformation-govern-large.png)

Model nadzoru z przewodnika Cloud Adoption Framework identyfikuje obszary o kluczowym znaczeniu podczas podróży. Każdego z tych obszarów dotyczą różne rodzaje czynników ryzyka, które przedsiębiorstwa muszą uwzględnić podczas wdrażania kolejnych usług w chmurze. W ramach tej struktury przewodnik dotyczący zapewnienia ładu identyfikuje wymagane akcje dla zespołu ds. utrzymania ładu w chmurze. Podczas kolejnych etapów podróży poszczególne reguły modelu nadzoru z przewodnika Cloud Adoption Framework zostały bardziej szczegółowo opisane. Ogólnie należą do nich:

**Zasady firmowe:** Zasady firmowe — zarządzanie chmurą. Przewodnik po zapewnianiu ładu koncentruje się na konkretnych aspektach zasad firmowych:

- **Ryzyka biznesowe:** Identyfikowanie i zrozumienie zagrożeń firmy.
- **Zasady i zgodność:** Konwertowanie ryzyka na instrukcje zasad, które obsługują wszystkie wymagania dotyczące zgodności.
- **Procesy:** Zapewnienie przestrzegania określonych zasad.

**Pięć dyscyplin zarządzania chmurą:** Te dyscypliny obsługują zasady firmowe. Każda dyscyplina chroni firmę przed potencjalnymi problemami:

- Dyscyplina Cost Management
- Dyscyplina linii bazowej zabezpieczeń
- Dyscyplina spójności zasobów
- Dyscyplina linii bazowej tożsamości
- Dyscyplina wdrożenia

Zasadniczo zasady firmowe działają jako system wczesnego ostrzegania służący do wykrywania potencjalnych problemów. Dyscypliny ułatwiają zarządzanie ryzykiem i tworzeniem zabezpieczeń w firmie.

## <a name="grow-to-the-end-state"></a>Rozwój do stanu końcowego

Ponieważ wymagania dotyczące nadzoru będą zmieniać się w trakcie podróży po wdrażaniu chmury, wymagane jest inne podejście do nadzoru. Firmy nie mogą już czekać, aż mały zespół utworzy zabezpieczenia i plany na każdej drodze _przed wykonaniem pierwszego kroku_. Oczekuje się, że wyniki biznesowe będą osiągane szybciej i płynniej. Nadzór IT musi odbywać się szybko i nadążać za wymaganiami biznesowymi, aby być w gotowości podczas wdrażania chmury i uniknąć niezatwierdzonych zasobów IT.

Podejście polegające na **nadzorze przyrostowym** zapewnia takie cechy. Nadzór przyrostowy opiera się na niewielkim zestawie firmowych zasad, procesów i narzędzi służących do ustanowienia podstawy do wdrażania i zarządzania. Ta podstawa nosi nazwę **minimalnej koniecznej funkcjonalności (MVP, Minimum Viable Product)**. Minimalna konieczna funkcjonalność umożliwia zespołowi ds. utrzymania ładu szybkie włączenie nadzoru do implementacji w całym cyklu życia wdrożenia. Minimalna konieczna funkcjonalność może zostać ustanowiona w dowolnym momencie procesu wdrażania chmury. Dobrym sposobem jest jak najwcześniejszym przyjęciem MVP.

Możliwość szybkiego reagowania na zmieniające się czynniki ryzyka umożliwia zespołowi ds. utrzymania ładu w chmurze angażowanie się na nowe sposoby. Zespół ds. utrzymania ładu w chmurze może dołączyć do zespołu strategii chmury jako „zwiadowcy”, którzy będą poruszali się przed zespołami wdrażania w chmurze, kreślili trasy i szybko ustanawiali zabezpieczenia w celu zarządzania ryzykiem związanym z planami wdrażania. Te warstwy nadzoru just-in-time są znane jako **iteracje ładu**. Przy takim podejściu strategia ładu rozwija się jeden krok przed zespołami wdrażania chmury.

Na poniższym diagramie przedstawiono prostą minimalną konieczną funkcjonalność i trzy iteracje ładu. Podczas tych iteracji definiowane są dodatkowe zasady firmowe w celu rozwiązywania problemów związanych z nowymi czynnikami ryzyka. Następnie dyscyplina przyspieszania wdrażania stosuje te zmiany w ramach każdego wdrożenia.

![Przykład przyrostowego ulepszania ładu](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> Zarządzanie nie jest zamiennikiem kluczowych funkcji, takich jak zabezpieczenia, sieci, tożsamość, finanse, DevOps lub operacje. W trakcie procesu będą miały miejsce interakcje i zależności między elementami członkowskimi z każdej funkcji. Te elementy członkowskie powinny zostać uwzględnione przez zespół ds. utrzymania ładu w chmurze w celu przyspieszenia podejmowania decyzji i akcji.

## <a name="next-steps"></a>Następne kroki

Za pomocą [narzędzia testowego](https://cafbaseline.com) programu do oceny struktury wdrażania w chmurze można ocenić swoją transformację i ułatwić zidentyfikowanie luk w organizacji w sześciu kluczowych domenach zgodnie z definicją w strukturze.

> [!div class="nextstepaction"]
> [Ocenianie podróży transformacji](./benchmark.md)
