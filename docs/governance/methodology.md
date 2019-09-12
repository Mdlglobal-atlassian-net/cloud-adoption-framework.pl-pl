---
title: Metodologia ładu chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zbierz podstawową wiedzę na temat metodologii zapewniania ładu w chmurze w ramach przewodnika Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 43a03112342534a995dae3386b55ac1d98122b50
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70827124"
---
# <a name="cloud-governance-methodology"></a>Metodologia ładu chmury

Wdrażanie chmury to podróż, a nie cel. Po drodze istnieją wyraźne kamienie milowe i wymierne korzyści biznesowe. Jednak gdy firma rozpoczyna podróż, ostateczny stan wdrożenia chmury jest nieznany. Zarządzanie w chmurze pozwala utworzyć zabezpieczenia, dzięki którym firma będzie na odpowiedniej ścieżce podczas całej podróży.

Struktura wdrażania w chmurze zawiera przewodniki ładu, które opisują środowiska fikcyjnych firm, które są oparte na doświadczeniach rzeczywistych klientów. Każdy przewodnik polega na podążaniu za klientem podczas związanych z nadzorem aspektów wdrażania chmury.

## <a name="envision-an-end-state"></a>Przewidywanie stanu końcowego

Podróż bez celu to tylko tułaczka. Przed podjęciem pierwszego kroku należy ustalić przybliżoną wizję stanu końcowego. Na następującej grafice informacyjnej przedstawiono układ odniesienia dla stanu końcowego. Nie przedstawia punktu początkowego, ale potencjalny cel.

![Grafika informacyjna dotycząca modelu nadzoru Cloud Adoption Framework](../_images/operational-transformation-govern-highres.png)

Model nadzoru Cloud Adoption Framework identyfikuje obszary o kluczowym znaczeniu podczas podróży. Każdego z tych obszarów dotyczą różne rodzaje czynników ryzyka, które przedsiębiorstwa muszą uwzględnić podczas wdrażania kolejnych usług w chmurze. W ramach tej struktury przewodnik dotyczący zapewnienia ładu identyfikuje wymagane akcje dla zespołu ds. utrzymania ładu w chmurze. Podczas kolejnych etapów podróży poszczególne reguły modelu nadzoru z przewodnika Cloud Adoption Framework zostały bardziej szczegółowo opisane. Ogólnie należą do nich:

**Zasady firmowe:** Zasady firmowe sterują nadzorem chmury. Przewodnik po zapewnianiu ładu koncentruje się na konkretnych aspektach zasad firmowych:

- **Czynniki ryzyka biznesowego:** Identyfikowanie i interpretowanie firmowych czynników ryzyka.
- **Zasady i zgodność:** Konwertowanie czynników ryzyka na instrukcje zasad, które obsługują wymagania dotyczące zgodności.
- **Procesy:** Zapewnienie zgodności z określonymi zasadami.

**Pięć dyscyplin nadzoru chmury:** Te dyscypliny obsługują zasady firmowe. Każda dyscyplina chroni firmę przed potencjalnymi problemami:

- Cost Management
- Punkt odniesienia zabezpieczeń
- Spójność zasobów
- Punkt odniesienia obsługi tożsamości
- Przyspieszanie wdrażania

Zasadniczo zasady firmowe działają jako system wczesnego ostrzegania służący do wykrywania potencjalnych problemów. Dyscypliny ułatwiają zarządzanie ryzykiem i tworzeniem zabezpieczeń w firmie.

## <a name="grow-to-the-end-state"></a>Rozwój do stanu końcowego

Ponieważ wymagania dotyczące nadzoru będą zmieniać się w trakcie podróży po wdrażaniu chmury, wymagane jest inne podejście do nadzoru. Firmy nie mogą już czekać, aż mały zespół utworzy zabezpieczenia i plany na każdej drodze *przed wykonaniem pierwszego kroku*. Oczekuje się, że wyniki biznesowe będą osiągane szybciej i płynniej. Nadzór IT musi odbywać się szybko i nadążać za wymaganiami biznesowymi, aby być w gotowości podczas wdrażania chmury i uniknąć niezatwierdzonych zasobów IT.

Podejście polegające na **nadzorze przyrostowym** zapewnia takie cechy. Nadzór przyrostowy opiera się na niewielkim zestawie firmowych zasad, procesów i narzędzi służących do ustanowienia podstawy do wdrażania i zarządzania. Ta podstawa nosi nazwę **minimalnej koniecznej funkcjonalności (MVP, Minimum Viable Product)** . Minimalna konieczna funkcjonalność umożliwia zespołowi ds. utrzymania ładu szybkie włączenie nadzoru do implementacji w całym cyklu życia wdrożenia. Minimalna konieczna funkcjonalność może zostać ustanowiona w dowolnym momencie procesu wdrażania chmury. Dobrą praktyką jest jednak wdrożenie jej możliwie jak najszybciej.

Możliwość szybkiego reagowania na zmieniające się czynniki ryzyka umożliwia zespołowi ds. utrzymania ładu w chmurze angażowanie się na nowe sposoby. Zespół ds. utrzymania ładu w chmurze może dołączyć do zespołu strategii chmury jako „zwiadowcy”, którzy będą poruszali się przed zespołami wdrażania w chmurze, kreślili trasy i szybko ustanawiali zabezpieczenia w celu zarządzania ryzykiem związanym z planami wdrażania. Te warstwy nadzoru just-in-time są znane jako **iteracje ładu**. Przy takim podejściu strategia ładu rozwija się jeden krok przed zespołami wdrażania chmury.

Na poniższym diagramie przedstawiono prostą minimalną konieczną funkcjonalność i trzy iteracje ładu. Podczas tych iteracji definiowane są dodatkowe zasady firmowe w celu rozwiązywania problemów związanych z nowymi czynnikami ryzyka. Następnie dyscyplina przyspieszania wdrażania stosuje te zmiany w ramach każdego wdrożenia.

![Przykład przyrostowego ulepszania ładu](../_images/governance/incremental-governance-example.png)

> [!NOTE]
> Zarządzanie nie jest zamiennikiem kluczowych funkcji, takich jak zabezpieczenia, sieci, tożsamość, finanse, DevOps lub operacje. W trakcie procesu będą miały miejsce interakcje i zależności między elementami członkowskimi z każdej funkcji. Te elementy członkowskie powinny zostać uwzględnione przez zespół ds. utrzymania ładu w chmurze w celu przyspieszenia podejmowania decyzji i akcji.

## <a name="next-steps"></a>Następne kroki

Za pomocą [narzędzia testowego](https://cafbaseline.com) programu do oceny struktury wdrażania w chmurze można ocenić swoją transformację i ułatwić zidentyfikowanie luk w organizacji w sześciu kluczowych domenach zgodnie z definicją w strukturze.

> [!div class="nextstepaction"]
> [Ocenianie podróży transformacji](./benchmark.md)
