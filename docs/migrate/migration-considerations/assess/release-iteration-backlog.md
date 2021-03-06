---
title: Lista prac iteracji i wydania
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak utworzyć listę prac iteracji i wydania w celu zorganizowania zadań.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 90b6ecf9f7f4914855bbeeaa0afc5d920a85eeb4
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214195"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Zarządzanie zmianami w procesie migracji przyrostowej

W tym artykule przyjęto założenie, że procesy migracji mają charakter przyrostowy i działają równolegle do [procesu zarządzania](../../../govern/index.md). Jednak te same wskazówki mogą mieć zastosowanie w przypadku wypełniania zadań początkowych w strukturze podziału pracy dla tradycyjnych podejść zarządzania zmianami kaskadowymi.

## <a name="release-backlog"></a>Lista prac wydania

_Lista prac wydania_ składa się z serii zasobów (m.in. maszyn wirtualnych, baz danych, plików i aplikacji), które trzeba najpierw zmigrować, zanim obciążenie będzie mogło zostać wydane do użytku w środowisku produkcyjnym w chmurze. Podczas każdej iteracji zespół wdrożeniowy ds. chmury dokumentuje i szacuje procesy wymagane do przeniesienia każdego zasobu do chmury. Zobacz sekcję „Lista prac iteracji” poniżej.

## <a name="iteration-backlog"></a>Lista prac iteracji

_Lista prac iteracji_ to lista szczegółowych zadań, których wykonanie jest niezbędne do zmigrowania określonej liczby zasobów z istniejącego majątku cyfrowego do chmury. Wpisy na tej liście często są przechowywane w narzędziu do zarządzania metody Agile, takim jak Azure DevOps, jako elementy robocze.

Przed rozpoczęciem pierwszej iteracji zespół wdrożeniowy ds. chmury określa czas trwania iteracji, zwykle od dwóch do czterech tygodni. Ten okres czasu ma duże znaczenie dla utworzenia czasu rozpoczęcia i zakończenia dla każdego zestawu zatwierdzonych działań. Utrzymywanie spójnych okien wykonywania ułatwia pomiar szybkości (tempa migracji) i dostosowanie do zmieniających się potrzeb biznesowych.

Przed każdą iteracją zespół przegląda listę prac wydania oraz ocenia nakłady pracy i priorytety dotyczące zasobów, które mają zostać zmigrowane. Następnie zobowiązuje się dostarczyć określoną liczbę ustalonych migracji. Gdy zespół wdrożeniowy ds. chmury zaakceptuje to, lista zadań staje się _listą prac bieżącej iteracji_.

Podczas każdej iteracji członkowie zespołu pracują jako samoorganizujący zespół, aby spełniać zobowiązania z listy prac bieżącej iteracji.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu i zaakceptowaniu listy prac iteracji przez zespół wdrożeniowy ds. chmury można sfinalizować [zatwierdzenia zarządzania zmianami](./approve.md).

> [!div class="nextstepaction"]
> [Zatwierdzanie zmian architektury przed migracją](./approve.md)
