---
title: Przegląd decyzji dotyczących racjonalizacji
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak przeglądać decyzje o racjonalizacji i przygotować się do ułatwienia rozmowy z firmą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 90a6718c028023e1bae101b35fff873dd47e4ab2
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80427953"
---
# <a name="review-rationalization-decisions"></a>Przegląd decyzji dotyczących racjonalizacji

W trakcie początkowej fazy strategii i planowania zalecamy zastosowanie podejścia [przyrostowego](../digital-estate/rationalize.md#incremental-rationalization) do cyfrowego podpisywania. Jednak takie podejście osadza niektóre założenia w podejmowanych decyzjach. Firma Microsoft zaleca zespołom ds. strategii chmurowych i zespołom wdrażania chmury przeglądanie tych decyzji w postaci uproszczonej dokumentacji dotyczącej obciążeń. Ten przegląd jest również dobrym terminem obejmującym zainteresowane strony biznesowe i sponsora wykonawczego w przyszłości.

> [!IMPORTANT]
> Dalsze sprawdzanie poprawności decyzji o racjonalizacji zostanie przeprowadzone w fazie oceny migracji. Ta weryfikacja koncentruje się na przeglądzie biznesowym w celu odpowiedniego dopasowania zasobów.

Aby zweryfikować decyzje z racjonalizacją, Skorzystaj z poniższych pytań, aby ułatwić rozmowę z firmą. Pytania są pogrupowane według przewidywanego wyrównania.

## <a name="innovation-indicators"></a>Wskaźniki innowacji

Jeśli wspólny przegląd następujących pytań spowoduje odpowiedź "tak", obciążenie może być lepszym kandydatem do innowacji. Takie obciążenie nie zostanie zmigrowane za pośrednictwem dźwigu i Shift ani modernizacji modelu. Zamiast tego, logika biznesowa lub struktury danych zostaną utworzone w postaci nowej lub rozbudowanej aplikacji. Takie podejście może być bardziej pracochłonne i czasochłonne. Jednak w przypadku obciążenia, które reprezentuje znaczące zwroty biznesowe, inwestycja jest uzasadniona.

- Czy aplikacje w tym obciążeniu tworzą zróżnicowanie rynkowe?
- Czy istnieją proponowane lub zatwierdzone inwestycje mające na celu ulepszenie środowisk związanych z aplikacjami w tym obciążeniu?
- Czy dane w tym obciążeniu udostępniają nowe oferty produktów lub usług?
- Czy istnieją proponowane lub zatwierdzone inwestycje mające na celu wykorzystanie danych skojarzonych z tym obciążeniem?
- Czy wpływ na zróżnicowanie rynku lub nowe oferty mają być wymierne? Jeśli tak, to czy zwrócenie wyjustuje zwiększony koszt innowacji podczas wdrażania chmury?

Poniższe dwa pytania mogą pomóc w uwzględnieniu scenariuszy technicznych wysokiego poziomu w ocenie racjonalizacji. Odpowiedź "tak" w celu zidentyfikowania sposobu księgowania lub zmniejszenia kosztu związanego z innowacjami.

- Czy struktura danych lub logika biznesowa ulegnie zmianie w trakcie wdrażania chmury?
- Czy istnieje potok wdrożenia używany do wdrożenia tego obciążenia w środowisku produkcyjnym?

Jeśli odpowiedź na pytanie ma wartość "tak", zespół powinien rozważyć włączenie tego obciążenia jako kandydata innowacji. Co najmniej zespół powinien oznaczyć to obciążenie na potrzeby przeglądu architektury, aby identyfikować możliwości modernizacji.

## <a name="migration-indicators"></a>Wskaźniki migracji

Migracja to szybszy i tańszy sposób wdrażania chmury. Ale nie wykorzystuje możliwości innowacji. Przed zainwestowaniem w innowacje należy odpowiedzieć na następujące pytania. Mogą one pomóc w ustaleniu, czy model migracji nie ma zastosowania do obciążeń.

- Czy kod źródłowy obsługujący tę aplikację jest stabilny? Czy spodziewasz się, że pozostanie stabilna i niezmieniona w trakcie przedziału czasowego tego cyklu wydania?
- Czy to obciążenie obsługuje obecnie produkcyjne procesy biznesowe? Czy zostanie to zrobione w toku tego cyklu wydania?
- Czy ten nakład pracy związany z wdrażaniem chmury zwiększa stabilność i wydajność tego obciążenia?
- Czy zmniejszenie kosztów wiąże się z tym obciążeniem?
- Zmniejsza złożoność operacyjną dla tego obciążenia w ramach tego nakładu pracy?
- Czy innowacje są ograniczone przez bieżącą architekturę czy procesy operacji IT?

Jeśli odpowiedź na dowolne z tych pytań to "tak", należy rozważyć model migracji dla tego obciążenia. To zalecenie jest prawdziwe, nawet jeśli obciążenie jest kandydatem do innowacji.

Wyzwania dotyczące złożoności operacyjnej, kosztów, wydajności lub stabilności mogą przeszkodzić w biznesie. Możesz użyć chmury, aby szybko tworzyć ulepszenia związane z tymi wyzwaniami. Jeśli ma to zastosowanie, zalecamy użycie podejścia do migracji w celu pierwszej stabilizacji obciążenia. Następnie możesz rozwijać możliwości innowacyjne w stabilnym środowisku w chmurze Agile. Ta metoda zapewnia krótkoterminowe i zmniejsza koszty związane z długotrwałą zmianą.

> [!IMPORTANT]
> Modele migracji obejmują modernizację przyrostową. Korzystanie z architektur platformy jako usługi (PaaS) jest typowym aspektem działań migracji. Tak więc zbyt małe zmiany konfiguracji, które korzystają z tych usług platformy. Granica migracji jest definiowana jako istotna zmiana logiki biznesowej lub pomocniczych struktur firmy. Taka zmiana jest uważana za nakłady innowacyjne.

## <a name="update-the-project-plan"></a>Aktualizowanie planu projektu

Umiejętności wymagane w celu przepracowania migracji różnią się od umiejętności wymaganych do wysiłku innowacji. Podczas wdrażania planu wdrażania w chmurze Zalecamy przypisanie migracji i wysiłków innowacji do różnych zespołów. Każdy zespół ma własne iteracje, wydanie i planowanie cadences. Przypisanie oddzielnych zespołów zapewnia elastyczność procesu, aby zachować jeden plan wdrażania w chmurze, a jednocześnie księgowy na potrzeby innowacji i migracji.

Gdy zarządzasz planem wdrażania chmury w usłudze Azure DevOps, to zarządzanie zostanie odzwierciedlone przez zmianę nadrzędnego elementu pracy (lub epiku) z migracji w chmurze na potrzeby innowacji w chmurze. Ta subtelna zmiana pomaga upewnić się, że wszyscy uczestnicy planu wdrożenia chmury mogą szybko śledzić wymagane nakłady pracy i zmiany w podejmowanych działaniach zaradczych. To śledzenie pomaga również w dopasowaniu właściwych przypisań do odpowiedniego zespołu wdrażania w chmurze.

W przypadku dużych, złożonych planów wdrażania z wieloma różnymi projektami należy rozważyć zaktualizowanie ścieżki iteracji. Zmiana ścieżki obszaru sprawia, że obciążenie jest widoczne tylko dla zespołu przypisanego do tej ścieżki obszaru. Ta zmiana może ułatwić zespołowi wdrażanie w chmurze, zmniejszając liczbę widocznych zadań. Jednak zwiększa złożoność procesów zarządzania projektami.

## <a name="next-steps"></a>Następne kroki

[Ustanów iteracje i plany wydań,](./iteration-paths.md) aby rozpocząć planowanie pracy.

> [!div class="nextstepaction"]
> [Ustanów iteracje i plany wydań,](./iteration-paths.md) aby rozpocząć planowanie pracy.
