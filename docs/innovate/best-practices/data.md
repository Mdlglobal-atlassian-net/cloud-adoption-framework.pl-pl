---
title: 'Innowacje w chmurze: narzędzia do zdemokratyzuj proces danych na platformie Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia do zdemokratyzuj proces danych na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 1a4c6574ccef3f8373fe149e8756e49555cd0171
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557936"
---
# <a name="tools-to-democratize-data-in-azure"></a>Narzędzia do zdemokratyzuj proces danych na platformie Azure

Zgodnie z opisem w artykule teoretycznym dotyczącym [danych democratizing](../considerations/data.md), wiele innowacji może być dostarczanych z minimalnymi inwestycjami technicznymi. Niezliczone przykłady najważniejszych innowacji, które wymagały nieco więcej niż surowe dane. Democratizing dane są związane z inwestycją w niewielkim stopniu, gdy jest to konieczne, aby skontaktować się z klientami przy użyciu danych, aby korzystać z informacji na temat Począwszy od danych, można szybko przetestować hipotezę przed rozwinięciem do szerszej, bardziej kosztownej liczby cyfr. Gdy coraz więcej hipotez jest rafinowanych, a wynalazki zaczynają zostać przyjęte na dużą skalę, poniższe procesy będą poszczególni pomocą w przygotowaniu do obsługi operacyjnej innowacji.

![Podejście do struktury wdrażania chmury do danych democratizing](../../_images/innovate/democratize-data.png)

## <a name="alignment-to-the-methodology"></a>Wyrównanie do metodologii

Ten typ możliwości cyfrowych można przyspieszyć w każdej fazie poniższego procesu, również powyższym. Wskazówki techniczne umożliwiające przyspieszenie rozdzielania cyfr cyfrowych są wymienione w spisie treści po lewej stronie. Te artykuły zostały pogrupowane w te same fazy, aby dostosować wskazówki do ogólnej metodologii:

- **Udostępnianie danych:** Pierwszym krokiem w democratizing danych jest udostępnienie go w sposób otwarty.
- **Dane dotyczące zarządzania:** Upewnij się, że wszelkie poufne dane są zabezpieczone, śledzone i zarządzane przed udostępnieniem.
- **Scentralizowane dane:** Czasami konieczne jest zapewnienie scentralizowanej platformy do udostępniania i zarządzania danymi.
- **Zbierz dane:** Migracja, integracja, pozyskiwanie i Wirtualizacja mogą zbierać istniejące dane, które mają być scentralizowane, regulowane i udostępniane.

Zaleca się, aby zespoły rozwiązań do wdrażania w chmurze przechodzą do stosu, tak jak jest to konieczne, aby określić priorytet fokusu na potrzeby klientów nad architekturą w każdej iteracji. Opóźnienie wzrostu technicznego na korzyść klienta przyspiesza weryfikację hipotez. W związku z tym wszystkie wskazówki są mapowane na cztery procesy powyżej najwyższego wpływu na klientów na najwyższy wpływ techniczny. W każdym z nich znajdziesz wskazówki dotyczące różnych potencjalnych metod, które platforma Azure może przyspieszyć [Kompilowanie danych za pomocą empatię klientów](../considerations/build.md).

## <a name="toolchain"></a>Łańcuch narzędzi

Na platformie Azure następujące narzędzia są najczęściej wykorzystywane do przyspieszenia cyfrowego rozróżnienia na każdą z powyższych faz: Power BI, Azure Data Catalog, Azure SQL Data Warehouse, Cosmos DB, bazy danych platformy Azure dla PostgreSQL, MySQL, MariaDB, PostgreSQL, platforma Azure Data Lake, usługa migracji danych platformy Azure, Azure SQL Database (z wystąpieniami lub bez nich), Azure Data Factory, Azure Stream Analytics, SQL Server Integration Services, Azure Stack, StorSimple bazy danych Azure SQL, Azure Files, File Sync i PolyBase.

Zgodnie z podejściem do rozliczeń na dużą skalę, aspekty poszczególnych rozwiązań będą wymagały uściślenia i działania technicznego. W takim przypadku jest możliwe, że będą wymagane więcej z tych usług. Na razie użyj spisu treści po lewej stronie, aby znaleźć wskazówki dotyczące narzędzi systemu Azure związanych z procesem wymaganym do testowania hipotezy.

## <a name="get-started"></a>Rozpocznij

Spis treści po lewej stronie zawiera wiele artykułów, które ułatwiają rozpoczęcie pracy z każdym z narzędzi w tej łańcucha narzędzi.

> [!NOTE]
> Niektóre linki mogą opuścić strukturę wdrażania chmury, aby ułatwić przechodzenie poza zakres tej struktury.
