---
title: Najlepsze rozwiązania dotyczące migracji na platformę Azure
description: Wprowadzenie do najlepszych rozwiązań dotyczących migracji na platformę Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 5cc4a0cfdfe605fdd374055e782db2f0ce47c13f
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807295"
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
