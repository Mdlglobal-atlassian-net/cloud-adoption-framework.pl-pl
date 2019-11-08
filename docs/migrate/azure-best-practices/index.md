---
title: Najlepsze rozwiązania dotyczące migracji na platformę Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do najlepszych rozwiązań dotyczących migracji na platformę Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1519adff06d600b9829c9b7ff3ca82a0aa5a0160
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753377"
---
# <a name="azure-migration-best-practices"></a>Najlepsze rozwiązania dotyczące migracji na platformę Azure

Platforma Azure udostępnia kilka narzędzi ułatwiających wykonanie zadań migracji. Ta sekcja przewodnika Cloud Adoption Framework ma pomóc czytelnikom w implementacji tych narzędzi w sposób zgodny z najlepszymi rozwiązaniami dotyczącymi migracji. Te najlepsze rozwiązania są dostosowane do poszczególnych procesów w ramach modelu migracji opisanego w przewodniku Cloud Adoption Framework, który przedstawiono poniżej.

Rozwiń dowolny proces w spisie treści po lewej stronie, aby zobaczyć najlepsze rozwiązania wymagane na ogół podczas tego procesu.

![Model migracji opisany w przewodniku Cloud Adoption Framework](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> Planowanie majątku cyfrowego i ocena zasobów reprezentują dwa różne poziomy planowania i oceny migracji:
>
> - **Planowanie majątku cyfrowego:** Należy zaplanować lub zracjonalizować majątek cyfrowy podczas planowania, aby ustalić ogólną listę prac związanych z migracją. Jednak ten plan opiera się na pewnych założeniach i szczegółach, które trzeba zweryfikować, zanim będzie można przeprowadzić migrację obciążenia.
> - **Ocena zasobów:** Przed migracją obciążenia należy ocenić jego poszczególne zasoby, aby sprawdzić zgodność z chmurą oraz poznać architekturę i ograniczenia dotyczące ustalania rozmiaru. Ten proces pozwala zweryfikować założenia początkowe i udostępnia szczegółowe informacje potrzebne do migracji pojedynczego zasobu.
