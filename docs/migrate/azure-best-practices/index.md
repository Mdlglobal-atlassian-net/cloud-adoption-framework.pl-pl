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
ms.openlocfilehash: e8a7ae0af3b64a6d7e04555fe64a6189d964b3ff
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816571"
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
