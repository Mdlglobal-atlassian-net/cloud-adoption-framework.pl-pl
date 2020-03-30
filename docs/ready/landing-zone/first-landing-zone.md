---
title: Zagadnienia dotyczące strefy docelowej na platformie Azure
description: Dowiedz się, w jaki sposób strefa docelowa zapewnia podstawowy blok konstrukcyjny dowolnego środowiska wdrażania chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 594f10968e45477895fcc5dcd1b2a95d16d7c861
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392652"
---
# <a name="first-landing-zone"></a>Pierwsza strefa docelowa

Infrastruktura jako kod to naturalny etap większości wdrożeń chmury. Wdrożenie pierwszej strefy wyładunkowej w chmurze jest wspólnym punktem wyjścia w trakcie przechodzenia do środowiska opartego na kodzie. Ten artykuł pomoże Ci zrozumieć termin _strefy docelowej_ i zdecydować, która strefa docelowa jest najbardziej odpowiednia dla bieżących potrzeb.

## <a name="code-first-approach-to-landing-zones"></a>Podejście pierwszego kodu do stref wyładunkowej

Na poniższej ilustracji przedstawiono różne opcje dla stref wyładunkowej. Poniższe opcje ułatwiają wybranie właściwej strefy docelowej już dziś. Pomaga również w ustaleniu wymagań w zakresie przyszłych potrzeb strefy wyładunkowej.

![Opcje strefy wyładunkowej](../../_images/ready/landing-zone-options.png)

A. Zacznij od kodu, aby tworzyć spójne, powtarzające się strefy przeładunkowe. Jeśli masz doświadczenie w przypadku refaktoryzacji (lub rafinacji kodu i infrastruktury) w trakcie nauki, Zacznij od lekkiej bazy kodu, takiej jak infrastruktura wdrożenia chmury. Takie podejście przyspiesza powodzenie wdrażania i tworzy praktyczne możliwości uczenia się. Jednak tego typu początkowa strefa docelowa nie jest przeznaczona do obsługi poufnych danych ani obciążeń o kluczowym znaczeniu, bez konieczności dodatkowego refaktoryzacji.

B. Wraz ze wzrostem ilości i wymagania stają się bardziej jasno zidentyfikowane, zespoły wdrażania i platformy będą refaktoryzacji stref umieszczania na podstawie ich informacji. Proces rozszerzania stref ładunkowych przygotowuje środowiska w celu uzyskania bardziej złożonych wymagań dotyczących zgodności lub architektury. [Rozszerzanie strefy ładunkowej](../considerations/index.md) zawiera przewodniki i linki do najlepszych rozwiązań w celu zaplanowania wysiłków. Rozszerzanie strefy docelowej może pomóc w spełnieniu wymagań związanych z zabezpieczeniami, działaniami i nadzorem.

C. Niektóre plany wdrażania w chmurze podlegają zewnętrznym wymaganiom dotyczącym zgodności. Aby zmniejszyć obciążenie spełniające te wymagania, platforma Azure udostępnia kilka przykładowych planów platformy Azure. Niektóre przykłady można dodać do pierwszego wstępnego planu. Inne przykłady obejmują również określoną implementację, która może być w pierwszej strefie docelowej.

D. Gdy Partner udostępnia bieżące usługi zarządzane lub ma umowę na dostarczenie planu wdrożenia, zazwyczaj udostępni własną strefę docelową. Użycie strefy docelowej partnera może przyspieszyć wdrażanie i zapewnić spójne wymagania dotyczące zarządzania operacyjnego. Należy jednak wprowadzić dodatkowe zagadnienia dotyczące zarządzania wewnętrznego i wymagań dotyczących zabezpieczeń, aby zapewnić wyrównanie.

> [!NOTE]
> Przed przystąpieniem do działania z podejściem pierwszym i refaktoryzacją kodu, Czytelnicy powinni znać [konkurencyjne priorytety związane z tą decyzją](../../strategy/balance-competing-priorities.md#balance-during-ready). W przypadku wybrania podejścia do strefy wyładunkowej ważne jest zapoznanie się z niezbędną równowagę między "czasem do przyjęcia" i "długoterminowymi operacjami".

## <a name="choosing-a-first-landing-zone"></a>Wybieranie pierwszej strefy docelowej

Wybór pierwszej strefy docelowej zależy od wielu zmiennych. Poniższa siatka przechwytuje niektóre opcje dla pierwszej strefy wypchnięcia wraz ze zmiennymi, które mogą spowodować podjęcie decyzji.

| Strefa docelowa                                 | Środowisko chmury  | Skalowanie             | Czas odnajdowania | Produkcja gotowa | Połączenie hybrydowe             | Dane poufne     | Krytyczne znaczenie dla działalności   | Zgodność         |
|----------------------------------------------|-------------------|-------------------|----------------|------------------|--------------------|--------------------|--------------------|--------------------|
| [CAF migrację](./migrate-landing-zone.md)     | Nowość w chmurze      | zasoby < 1 000    | od 1 do 5 dni    | Ograniczony zakres — > | Wymagane rozszerzenie | Wymagane rozszerzenie | Wymagane rozszerzenie | Wymagane rozszerzenie |
| [CAF Terraform](./terraform-landing-zone.md) | Różne szablony | Różne szablony | od 10 do 20 tygodni | Ograniczony zakres — > | Dostępne moduły  | Dostępne moduły  | Dostępne moduły  | Dostępne moduły  |

W poniższej tabeli przedstawiono te same strefy wyładunkowe z nieco różnych perspektyw, co prowadzi do bardziej szczegółowych procesów decyzyjnych.

| Strefa docelowa                                 | Centrum                          | Znajdowało    | Model chmury | Technologia      |
|----------------------------------------------|------------------------------|----------|-------------|-----------------|--|--|--|
| [CAF migrację](./migrate-landing-zone.md)     | Wymagany jest składnik refaktoryzacji            | Dołączono | Tylko platforma Azure  | Azure Blueprint |
| [CAF Terraform](./terraform-landing-zone.md) | Uwzględnione w module VDC       | Dołączono | Rozwiązanie wielochmurowe  | Terraform       |

## <a name="next-steps"></a>Następne kroki

Jeśli nadal nie masz pewności co do wyboru pierwszej strefy docelowej, zalecamy rozpoczęcie od [CAF migracji strefy docelowej](./migrate-landing-zone.md).

> [!div class="nextstepaction"]
> [CAF Migrowanie planu strefy ładunkowej](./migrate-landing-zone.md)
