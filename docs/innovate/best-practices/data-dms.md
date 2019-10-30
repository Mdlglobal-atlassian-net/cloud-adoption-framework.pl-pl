---
title: 'Innowacje w chmurze: usługa migracji danych'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Innowacje w chmurze — usługa migracji danych
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 538cbc89fb592ecc19a5c25c42cf21231bfe05fe
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73047754"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Zbierz dane za pomocą migracji i modernizacji istniejących źródeł danych

Firmy często mają różnorodne istniejące dane, które można [oddemokratyzacjć](../considerations/data.md). Gdy hipoteza klienta wymaga użycia istniejących danych do kompilowania nowoczesnych rozwiązań, pierwszym krokiem może być migracja i modernizacja danych w celu przygotowania do wynalazków i innowacji. Aby dostosować się do istniejących wysiłków związanych z migracją w ramach planu wdrażania chmury, migracja i modernizacja mogą być łatwiej wykonywane w ramach [metodologii migracji](../../migrate/index.md).

## <a name="use-of-this-article"></a>Korzystanie z tego artykułu

W tym artykule opisano szereg metod, które są zgodne z procesem migracji, ale można je najlepiej dostosować do standardowej łańcucha narzędzi migracji. W trakcie procesu oceny w ramach metodologii migrowania zespół ds. rozwiązań w chmurze oceni bieżący stan i zażąda przyszłego stanu zasobów do migracji. Gdy ten proces jest częścią nakładu pracy innowacyjnej, zespoły do wdrażania chmury mogą używać tego artykułu do podejmowania tych decyzji.

## <a name="primary-toolset"></a>Podstawowy zestaw narzędzi

Podczas migrowania i modernizacji danych, które znajdują się w Premium, najbardziej typowym wyborem narzędzia platformy Azure jest [Usługa Data Migration Service (DMS)](https://docs.microsoft.com/azure/dms) , która jest częścią szerszego [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) łańcucha narzędzi. W przypadku istniejących źródeł danych SQL Server [Data Migration Assistant (DMA)](https://docs.microsoft.com/sql/dma/dma-overview) może także zapewnić pomoc w ocenie i migracji mniejszej liczby struktur danych.

Aby zapewnić obsługę migracji rozwiązań Oracle i NoSQL, można także użyć [usługi Data Migration Service (DMS)](https://docs.microsoft.com/azure/dms) dla niektórych typów źródeł docelowych baz danych, takich jak Oracle to PostgreSQL lub MongoDB, aby Cosmos DB. Jest to bardziej powszechne dla zespołów, które mogą korzystać z narzędzi innych firm lub niestandardowych skryptów migracji w celu migrowania do Cosmos DB, usługi HDInsight lub opcji maszyn wirtualnych opartych na IaaS.

## <a name="considerations-and-guidance"></a>Zagadnienia i wskazówki

W przypadku korzystania z usługi DMS do migracji i modernizacji danych ważne jest, aby zrozumieć bieżącą platformę do obsługi danych (źródłowych), wersji i przyszłej platformy i wersji, która najlepiej obsługuje hipotezę klienta. Poniżej znajduje się lista par źródłowych i docelowych, które należy przejrzeć z zespołem migracji. Każdy z nich zawiera wybór narzędzi i link do przewodnika w oparciu o te zagadnienia.

**Typ migracji:** W przypadku migracji w trybie offline przestój aplikacji rozpoczyna się po rozpoczęciu migracji. W przypadku migracji online przestój jest ograniczony do czasu migracji jednorazowej na końcu procesu migracji. Sugerujemy, aby zrozumieć, co to jest akceptowalny przestój biznesowy, i przetestować migrację w trybie offline, aby określić, czy czas przywracania spełnia te wymagania. Jeśli nie, wykonaj migrację w trybie online.

|Źródło  |Cel  |Narzędzie  |Typ migracji  |Wskazówka  |
|---------|---------|---------|---------|---------|
|Oprogramowanie SQL Server|Azure SQL Database|DMS|Stanie|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|Oprogramowanie SQL Server|Azure SQL Database|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|Oprogramowanie SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|DMS|Stanie|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|Oprogramowanie SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server RDS|Azure SQL Database (lub wystąpienie zarządzane)|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure Database for MySQL|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure Database for PostgreSQL|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|Istniejącą|Azure Cosmos DB interfejs API Mongo|DMS|Stanie|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Azure Cosmos DB interfejs API Mongo|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Zakres opcji PaaS & IaaS|Inna firma lub Azure Migrate|Poszczególne|[Drzewo decyzyjne](../../migrate/expanded-scope/data-oracle-migration.md)|
|Różne NoSQL baz danych|Cosmo DB lub IaaS opcje|Migracje proceduralne lub Azure Migrate|Poszczególne|[Drzewo decyzyjne](../../migrate/expanded-scope/data-no-sql-migration.md)|
