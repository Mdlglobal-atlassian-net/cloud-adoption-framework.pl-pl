---
title: Jak działa platforma Azure?
description: Poznaj podstawowe informacje o strukturze wewnętrznej i działaniu platformy chmury platformy Azure oraz wirtualizacji chmury.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 91bfb288c841dbfaa367120d7c904642a3d9fb38
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434749"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>Jak działa platforma Azure?

Azure to platforma chmury publicznej firmy Microsoft. Platforma Azure oferuje dużą kolekcję usług, w tym możliwości platformy jako usługi (PaaS), infrastruktury jako usługi (IaaS) i usługi zarządzanej bazy danych. Ale co dokładnie to platforma Azure i jak to działa?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ixGo]

Platforma Azure, podobnie jak inne platformy w chmurze, opiera się na technologii znanej jako _Wirtualizacja_. Większość sprzętu komputerowego może być emulowana w oprogramowaniu, ponieważ większość sprzętu komputerowego jest po prostu zestawem instrukcji trwale lub częściowo zakodowanych w krzemie. Korzystając z warstwy emulacji, która mapuje instrukcje oprogramowania do instrukcji sprzętowych, zwirtualizowany sprzęt może być wykonywany w oprogramowaniu tak, jakby był to sam sprzęt.

Zasadniczo chmurą jest zestaw serwerów fizycznych w jednym lub kilku centrach danych, które wykonują zwirtualizowany sprzęt w imieniu klientów. W jaki sposób w chmurze można tworzyć, uruchamiać, zatrzymywać i usuwać miliony wystąpień zwirtualizowanego sprzętu w przypadku milionów klientów jednocześnie?

Aby to zrozumieć, przyjrzyjmy się architekturze sprzętu w centrum danych. W każdym centrum danych jest kolekcją serwerów znajdujących się w stojakach serwera. Każdy stojak serwera zawiera wiele **kaset** serwera, a także przełącznik sieci zapewniający łączność sieciową i jednostkę dystrybucji (PDU) dostarczającą moc. Stojaki są czasami pogrupowane razem w większych jednostkach nazywanych _klastrami_.

W każdym stojaku lub klastrze większość serwerów jest wyznaczonych do uruchamiania tych zwirtualizowanych wystąpień sprzętu w imieniu użytkownika. Jednak niektóre serwery uruchamiają oprogramowanie do zarządzania chmurą znane jako kontroler sieci szkieletowej. _Kontroler sieci szkieletowej_ jest aplikacją rozproszoną z wieloma obowiązkami. Przypisuje usługi, monitoruje kondycję serwera i usługi działające na nim, a serwery są uważane za niepowodzenie.

Każde wystąpienie kontrolera sieci szkieletowej jest połączone z innym zestawem serwerów, na których działa oprogramowanie aranżacji w chmurze, zazwyczaj nazywane _frontonem_. Fronton obsługuje usługi sieci Web, interfejsy API RESTful i wewnętrzne bazy danych platformy Azure używane dla wszystkich funkcji wykonywanych przez chmurę.

Na przykład fronton obsługuje usługi obsługujące żądania klientów, aby alokować zasoby platformy Azure, takie jak [maszyny wirtualne](https://docs.microsoft.com/azure/virtual-machines)i usługi, takie jak [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction). Najpierw fronton sprawdza użytkownika i sprawdza, czy użytkownik jest autoryzowany do przydzielenia żądanych zasobów. Jeśli tak, fronton sprawdza bazę danych w celu zlokalizowania stojaka serwera o wystarczającej pojemności, a następnie instruuje Kontroler sieci szkieletowej w tym stojaku, aby przydzielić zasób.

W związku z tym platforma Azure to ogromna kolekcja serwerów i sprzętu sieciowego, na których działa złożony zestaw aplikacji rozproszonych, aby organizować konfigurację i działanie zwirtualizowanego sprzętu i oprogramowania na tych serwerach. Jest to aranżacja, dzięki której platforma Azure zapewnia zaawansowane&mdash;użytkownicy nie będą już zobowiązani do obsługi i uaktualniania sprzętu, ponieważ platforma Azure wykonuje te same sceny w tle.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o wdrażaniu chmury przy użyciu platformy [wdrażania Microsoft Cloud dla platformy Azure](../index.md).

> [!div class="nextstepaction"]
> [Dowiedz się więcej na temat platformy wdrażania Microsoft Cloud dla platformy Azure](../index.md)
