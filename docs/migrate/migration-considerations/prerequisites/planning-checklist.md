---
title: Lista kontrolna planowania środowiska migracji
description: Aby sprawdzić gotowość środowiska przed migracją, należy użyć listy kontrolnej planowania środowiska migracji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5e36757cd187b42a9ff8b976db886feb55f1b2e0
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223528"
---
# <a name="migration-environment-planning-checklist-validate-environmental-readiness-prior-to-migration"></a>Lista kontrolna planowania środowiska migracji: sprawdzanie gotowości środowiska przed migracją

W pierwszym etapie procesu migracji należy utworzyć odpowiednie środowisko w chmurze do odbierania, hostowania i obsługi migrowanych zasobów. Ten artykuł zawiera listę elementów do zweryfikowania w bieżącym środowisku przed migracją.

Poniższa lista kontrolna zawiera wskazówki dotyczące [gotowej metodologii](../../../ready/index.md) wdrożenia chmury. Zapoznaj się z tą sekcją, aby uzyskać wskazówki dotyczące wykonania poniższych czynności.

## <a name="effort-type-assumption"></a>Założenie typu nakładu pracy

W tym artykule założono podejście do migracji do chmury oparte na _ponownym hostowaniu_ lub _przeniesieniu do chmury_.

## <a name="governance-alignment"></a>Dostosowanie ładu

Pierwszą i najważniejszą decyzją dotyczącą środowiska gotowego do migracji jest wybór dostosowania ładu. czy osiągnięto porozumienie dotyczące dostosowania ładu do podstaw migracji? Zespół ds. wdrażania chmury powinien zrozumieć, czy migracja jest wypełniać w jednym środowisku z ograniczonym zarządzaniem, w pełni zarządzaną fabryką środowiskową, czy też pewną odmianą. Aby uzyskać dodatkowe wskazówki dotyczące wyrównania przez kierownictwo, zobacz [metodologia](../../../govern/index.md)zarządzania.

## <a name="operations-management-alignment"></a>Wyrównanie zarządzania operacjami

Przed migracją zasobów do chmury ważne jest zapoznanie się z wymaganiami i ograniczeniami dotyczącymi zarządzania operacjami. Środowisko migracji powinno zawierać co najmniej wszelkie implementacje wymagane do spełnienia planu bazowego operacji. Aby uzyskać dodatkowe wskazówki dotyczące wyrównania operacji, zobacz [Zarządzanie metodologią](../../../manage/index.md).

## <a name="cloud-readiness-implementation"></a>Wdrożenie gotowości chmury

Niezależnie od tego, czy zdecydujesz się na zastosowanie szerszej strategii ładu w chmurze dla początkowej migracji czy nie, musisz się upewnić, że środowisko wdrożenia w chmurze jest skonfigurowane w sposób umożliwiający obsługę obciążeń.

Jeśli planujesz zapewnienie zgodności migracji ze strategią ładu w chmurze od początku, musisz zastosować [Pięć dziedzin nadzoru chmury](../../../govern/governance-disciplines.md), aby łatwiej podejmować decyzje dotyczące zasad, łańcuchów narzędzi i mechanizmów wymuszania, które dostosują środowisko w chmurze do ogólnych wymagań przedsiębiorstwa. Zapoznaj się z [praktycznymi przewodnikami po projektowaniu rozwiązań utrzymania ładu](../../../govern/guides/index.md), aby uzyskać przykłady wdrożenia tego modelu przy użyciu usług platformy Azure.

Jeśli początkowe migracje nie są ściśle dostosowane do szerszej strategii ładu w chmurze, nadal konieczne jest rozwiązywanie ogólnych problemów związanych z organizacją, dostępem i planowaniem infrastruktury. Zapoznaj się z [przewodnikiem Instalatora platformy Azure](../../../ready/azure-setup-guide/index.md) , aby uzyskać pomoc dotyczącą tych decyzji dotyczących przygotowania do chmury.

> [!CAUTION]
> Zdecydowanie zalecamy opracowanie strategii ładu dla wszystkich procesów poza początkową migracją obciążeń.

Bez względu na stopień dostosowania ładu konieczne będzie podejmowanie decyzji związanych z następującymi tematami.

### <a name="resource-organization"></a>Organizacja zasobów

Na podstawie decyzji dotyczącej dostosowania ładu należy ustalić podejście do organizacji i wdrożenia zasobów przed migracją.

### <a name="nomenclature"></a>Nazewnictwo

Przed migracją należy ustalić spójne podejście do nazewnictwa zasobów oraz spójne schematy nazewnictwa.

### <a name="resource-governance"></a>Nadzór nad zasobami

Przed migracją należy podjąć decyzję dotyczącą narzędzi do zarządzania zasobami. Narzędzia nie muszą być w pełni wdrożone, ale należy wybrać kierunek i przetestować go. Zespół ds. nadzoru chmurowego powinien określić i wymagać wdrożenia minimalnego produktu żywotnego (MVP) na potrzeby narzędzi do zarządzania przed migracją.

## <a name="network"></a>Sieć

Obciążenia oparte na chmurze będą wymagać ustanowienia sieci wirtualnych do obsługi dostępu użytkowników końcowych i administratorów. W oparciu o organizację zasobów i decyzje dotyczące ładu zasobów należy wybrać podejście sieciowe i dostosować je do wymagań bezpieczeństwa IT. Ponadto decyzje dotyczące sieci powinny być dostosowane do wszelkich ograniczeń sieci hybrydowej wymaganych do obsługi obciążeń na liście prac związanych z migracją oraz obsługi dostępu do zasobów hostowanych lokalnie.

## <a name="identity"></a>Tożsamość

Usługi tożsamości oparte na chmurze są warunkiem wstępnym, aby można było oferować zarządzanie tożsamościami i dostępem (IAM) dla zasobów chmury. Przed kontynuowaniem należy dostosować strategię zarządzania tożsamościami przy użyciu planów wdrażania w chmurze. Na przykład podczas migrowania istniejących zasobów lokalnych należy rozważyć obsługę tożsamości hybrydowej przy użyciu [synchronizacji katalogów](../../../decision-guides/identity/index.md), aby umożliwić korzystanie ze spójnego zestawu poświadczeń użytkowników w środowisku lokalnym i chmurowym podczas migracji i po niej.

## <a name="next-steps"></a>Następne kroki

Jeśli środowisko spełnia wymagania minimalne, można je uznać za zatwierdzone pod względem gotowości do migracji. Sekcja [Złożoność kulturowa i zarządzanie zmianami](./cultural-complexity.md) zawiera informacje ułatwiające dopasowywanie ról i obowiązków w celu spełnienia odpowiednich oczekiwań podczas wykonywania planu.

> [!div class="nextstepaction"]
> [Złożoność kulturowa i zarządzanie zmianami](./cultural-complexity.md)
