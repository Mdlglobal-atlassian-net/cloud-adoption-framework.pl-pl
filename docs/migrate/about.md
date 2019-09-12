---
title: Migracja do chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do zawartości dotyczącej migracji do chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1bf9497684c1043d23eec48b1ab5d5f1f12ef752
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70829958"
---
# <a name="cloud-migration-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Migracja do chmury w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure

Migracja do chmury jest procesem przenoszenia istniejącego majątku cyfrowego na platformę w chmurze. W tym podejściu istniejące zasoby są replikowane do chmury z minimalnymi zmianami. Gdy aplikacja lub obciążenie zostanie uruchomione w chmurze, użytkownicy będą przenoszeni z istniejącego rozwiązania do rozwiązania w chmurze. Migracja do chmury jest jednym ze sposobów równoważenia portfolio chmury. Jest to często najszybsze i najbardziej elastyczne podejście krótkoterminowe. Natomiast niektórych zalet chmury nie można wykorzystać w przypadku tego podejścia bez dodatkowych modyfikacji w przyszłości. Klienci w przedsiębiorstwach i średnich firmach używają tego podejścia, aby przyspieszyć tempo zmian, uniknąć planowanych nakładów kapitałowych oraz zmniejszyć stałe koszty operacyjne.

## <a name="cloud-migration-guidance"></a>Wskazówki dotyczące migracji do chmury

Wskazówki zawarte w tej sekcji przewodnika Cloud Adoption Framework przygotowano z myślą o dwóch celach:

- Przedstawienie praktycznych przewodników migracji, które reprezentują typowe doświadczenia często napotykane przez klientów. W każdym przewodniku opisano proces i narzędzia potrzebne do pomyślnego przeprowadzenia migracji do chmury. Z konieczności wskazówki dotyczące projektu są specyficzne dla platformy Azure. Wszystkie inne rekomendacje zawarte w tych podręcznikach można zastosować jako część podejścia niezależnego od chmury lub wielochmurowego.
- Pomoc czytelnikom w utworzeniu spersonalizowanych planów migracji spełniających różne potrzeby biznesowe, w tym te dotyczące migracji do wielu chmur publicznych za pośrednictwem szczegółowych wskazówek dotyczących opracowywania procesów roli i obowiązków oraz kontrolek zarządzania zmianami.

Ta zawartość jest przeznaczona dla zespołu wdrożeniowego ds. chmury. Jest również istotna dla architektów chmury, którzy muszą rozwinąć solidne podstawowe umiejętności z zakresu migracji do chmury.

## <a name="intended-audience"></a>Docelowi odbiorcy

Wskazówki w przewodniku Cloud Adoption Framework dotyczą działalności biznesowej, technologii i kultury przedsiębiorstw. Ta sekcja ma znaczący wpływ na właścicieli aplikacji, personel ds. zarządzania zmianami (np. biura zarządzania projektami i personel ds. zarządzania metodą Agile), liderów biznesowych i finansowych oraz zespół wdrożeniowy ds. chmury. Między tymi osobami istnieją różnorodne zależności, które będą wymagały od architektów chmury korzystających z tego przewodnika zastosowania ułatwień. Pomoc tym zespołom może być wysiłkiem jednorazowym, jednak w niektórych przypadkach zaskutkuje powtarzającymi się interakcjami z tymi innymi osobami.

Architekt chmury pełni rolę lidera myśli i osoby ułatwiającej kontakt między tymi odbiorcami. Zawartość tej kolekcji przewodników ma pomóc architektowi chmury w ułatwieniu odpowiednich konwersacji z odpowiednimi odbiorcami, aby umożliwić podjęcie koniecznych decyzji. Transformacja firmy, która jest napędzana i obsługiwana przez chmurę, zależy od tego, czy architekt chmury pomoże w podejmowaniu decyzji w zakresie działalności biznesowej i IT.

**Specjalizacja architekta chmury w tej sekcji:** Każda sekcja przewodnika Cloud Adoption Framework reprezentuje różną specjalizację lub wariant roli architekta chmury. Tę sekcję zaprojektowano z myślą o architektach chmury z dużą wiedzą specjalistyczną o istniejącym środowisku lokalnym i jego wpływie na opcje migracji.

**Podział obowiązków:** W wielu przedsiębiorstwach wprowadzono podział obowiązków, aby ograniczyć dostęp do systemów produkcyjnych lub segmentów środowiska firmowego. W takim przypadku proces migracji staje się bardziej złożony. W niektórych przypadkach te role i obowiązki mogą wymagać wielu architektów chmury do przeprowadzenia całego procesu migracji.

**Opcje partnerstwa** W ramach każdego z tych procesów zespoły będą uczyć się nowych umiejętności i podejść do wykonania technicznego. Rozwijanie umiejętności technicznych aktualnych członków zespołu jest jedną z opcji podczas wykonywania. Drugą opcją jest zatrudnienie dodatkowych pracowników. Współpraca z podmiotami trzecimi może często zapewniać znaczne przyspieszenie i redukcje ryzyka. Artykuł [Opcje partnerstwa](./migration-considerations/assess/partnership-options.md) może pomóc w podjęciu decyzji o wyborze najlepszej opcji partnerstwa.

## <a name="next-steps"></a>Następne kroki

Czytelnikom, którzy chcą postępować zgodnie z tym przewodnikiem od początku do końca, ta zawartość pomoże w opracowaniu solidnej strategii migracji do chmury. Wskazówki przeprowadzają czytelnika przez teorię i implementację takiej strategii.

Na początek zaleca się, aby czytelnicy zapoznali się z [Przewodnikiem po migracji na platformę Azure](./azure-migration-guide/index.md) w celu poznania podstawowego zestawu narzędzi i podejść niezbędnych do migracji w typowym przypadku użycia. Potem podstawowe wskazówki można rozszerzyć zgodnie z potrzebami czytelników o [złożone scenariusze migracji](./expanded-scope/index.md), [najlepsze rozwiązania w zakresie migracji](./azure-best-practices/index.md) i [zagadnienia dotyczące migracji](./migration-considerations/index.md).

> [!div class="nextstepaction"]
> [Przewodnik po migracji na platformę Azure](./azure-migration-guide/index.md)
