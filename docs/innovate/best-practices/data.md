---
title: Narzędzia innowacyjne do zdemokratyzuj proces danych
description: Dowiedz się więcej na temat Azure Data Catalog i innych usług, które ułatwiają szybkie testowanie hipotez przed rozwinięciem do szerszej, bardziej kosztownej liczby cyfr.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 613e1ebaa3341b9aa96af659d0eb03cbc21a1303
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80425604"
---
# <a name="tools-to-democratize-data-in-azure"></a>Narzędzia do zdemokratyzuj proces danych na platformie Azure

Zgodnie z opisem w artykule pojęciowym dotyczącym [danych democratizing](../considerations/data.md), możesz dostarczać wiele innowacji z niewielkimi inwestycjami technicznymi. Wiele ważnych innowacji wymaga nieco więcej niż nieprzetworzone dane. Democratizing dane są inwestowane jako niewielki zasób, gdy jest to konieczne, aby zaangażować klientów korzystających z danych w celu skorzystania z istniejących informacji.

Począwszy od danych, można szybko przetestować hipotezę przed rozwinięciem do szerszej, bardziej kosztownej liczby cyfr. Po dodaniu większej liczby hipotez i przystąpieniu do przyjęcia wynalazków na dużą skalę następujące procesy ułatwią przygotowanie się do obsługi operacyjnej innowacji.

![Podejście do struktury wdrażania chmury do danych democratizing](../../_images/innovate/democratize-data.png)

## <a name="alignment-to-the-methodology"></a>Dostosowywanie do metodologii

Ten typ możliwości cyfrowych można przyspieszyć w każdej fazie następujących procesów, jak pokazano na powyższym obrazie. Wskazówki techniczne umożliwiające przyspieszenie oddzielania cyfr cyfrowych są wymienione w spisie treści po lewej stronie tej strony. Te artykuły są pogrupowane według fazy, aby dostosować wskazówki do ogólnej metodologii.

- **Udostępnianie danych:** Pierwszy krok polega na tym, że dane democratizing są udostępniane w sposób otwarty.
- **Dane dotyczące zarządzania:** Upewnij się, że wszelkie poufne dane są zabezpieczone, śledzone i zarządzane przed udostępnieniem.
- **Scentralizowane dane:** Czasami trzeba zapewnić scentralizowaną platformę do udostępniania i zarządzania danymi.
- **Zbierz dane:** Migracja, integracja, pozyskiwanie i Wirtualizacja mogą zbierać istniejące dane, które mają być scentralizowane, regulowane i udostępniane.

W każdej iteracji zespoły rozwiązań w chmurze powinny przechodzić wyłącznie do stosu, ponieważ wymagają one skoncentrowania się na potrzebach klientów nad architekturą. Opóźnienie wzmocneń technicznych na korzyść klientów przyspiesza weryfikację hipotez.

Wszystkie wskazówki są mapowane na cztery poprzednie procesy. Wskazówki dotyczące zakresu od najwyższego do najwyższego skutku technicznego. W każdym procesie zobaczysz wskazówki dotyczące różnych potencjalnych metod, które platforma Azure może skrócić do [kompilowania z empatię klientów](../considerations/build.md).

## <a name="toolchain"></a>Łańcuch narzędzi

Na platformie Azure następujące narzędzia są często używane do przyspieszenia cyfrowego rozróżnienia w poprzednich fazach:

- [Power BI](https://docs.microsoft.com/power-bi)
- [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog)
- [Azure Synapse Analytics](https://docs.microsoft.com/azure/synapse-analytics)
- [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db)
- [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql)
- [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql)
- [Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb)
- [Skalowanie Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-nodes)
- [Azure Data Lake](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms)
- [Azure SQL Database z wystąpieniami zarządzanymi lub bez nich](https://docs.microsoft.com/azure/sql-database)
- [Azure Data Factory](https://docs.microsoft.com/azure/data-factory)
- [Usługa Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics)
- [Usługi SQL Server Integration Services](https://docs.microsoft.com/sql/integration-services)
- [Azure Stack](https://docs.microsoft.com/azure-stack)
- [SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database)
- [Microsoft Azure StorSimple](https://docs.microsoft.com/azure/storsimple)
- [Azure Files](https://docs.microsoft.com/azure/storage/files)
- [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)
- [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase)

Zgodnie z podejściem do rozliczeń na dużą skalę, aspekty poszczególnych rozwiązań wymagają uściślania i działania techniczne. W takim przypadku może być wymagana większa liczba tych usług. Skorzystaj ze spisu treści po lewej stronie tej strony, aby uzyskać wskazówki dotyczące narzędzi platformy Azure, które są istotne dla procesu testowania hipotez.

## <a name="get-started"></a>Rozpoczęcie pracy

Spis treści po lewej stronie tej strony zawiera wiele artykułów. Te artykuły ułatwiają rozpoczęcie pracy z każdym z narzędzi w tej łańcucha narzędzi.

> [!NOTE]
> Niektóre linki mogą opuścić strukturę wdrażania chmury, aby ułatwić przechodzenie poza zakres tej struktury.
