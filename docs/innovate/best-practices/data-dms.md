---
title: Narzędzia innowacyjne do migrowania danych
description: Dowiedz się więcej na temat Azure Database Migration Service i innych narzędzi, które umożliwiają migrowanie i modernizację danych w celu przygotowania do wynalazków i innowacji w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: cd4009e8201cf6267e9da297ce13987cb025139e
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/28/2020
ms.locfileid: "78171280"
---
# <a name="collect-data-through-the-migration-and-modernization-of-existing-data-sources"></a>Zbierz dane za pomocą migracji i modernizacji istniejących źródeł danych

Firmy często mają różne rodzaje istniejących danych, które mogą [zdemokratyzuj proces](../considerations/data.md). Gdy hipoteza klienta wymaga użycia istniejących danych do kompilowania nowoczesnych rozwiązań, pierwszym krokiem może być migracja i modernizacja danych w celu przygotowania do wynalazków i innowacji. Aby dostosować się do istniejących wysiłków związanych z migracją w ramach planu wdrażania w chmurze, można łatwiej przeprowadzić migrację i modernizację w ramach [metodologii migracji](../../migrate/index.md).

## <a name="use-of-this-article"></a>Korzystanie z tego artykułu

W tym artykule przedstawiono szereg metod, które są wyrównane do procesu migracji. Najlepiej dostosować te podejścia do standardowej łańcucha narzędzi migracji.

W trakcie procesu oceny w ramach metodologii migracji zespół ds. wdrażania chmury ocenia bieżący stan i żądany przyszły stan dla zmigrowanego elementu zawartości. Gdy ten proces jest częścią nakładu pracy innowacyjnej, zespoły do wdrażania chmury mogą korzystać z tego artykułu, aby pomóc w dokonaniu tych ocen.

## <a name="primary-toolset"></a>Podstawowy zestaw narzędzi

Podczas migrowania i modernizacji danych lokalnych, najbardziej typowym wyborem narzędzia platformy Azure jest [Azure Database Migration Service](https://docs.microsoft.com/azure/dms). Ta usługa jest częścią szerszego [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) łańcucha narzędzi. W przypadku istniejących SQL Server źródeł danych [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview) może pomóc w ocenie i migracji niewielkiej liczby struktur danych.

Aby zapewnić obsługę migracji Oracle i NoSQL, można również użyć [Database Migration Service](https://docs.microsoft.com/azure/dms) dla niektórych typów baz danych Source-to-target. Przykłady obejmują od Oracle do PostgreSQL i MongoDB do Cosmos DB. Często zespoły ds. wdrażania używają narzędzi partnerskich lub skryptów niestandardowych do migracji do Azure Cosmos DB, usługi Azure HDInsight lub opcji maszyny wirtualnej w oparciu o infrastrukturę jako usługę (IaaS).

## <a name="considerations-and-guidance"></a>Zagadnienia i wskazówki

W przypadku używania Azure Database Migration Service do migracji i modernizacji danych należy zrozumieć:

- Bieżąca platforma do hostowania źródła danych.
- Bieżąca wersja.
- Przyszła platforma i wersja, która najlepiej obsługuje hipotezę klienta lub cel.

W poniższej tabeli przedstawiono pary źródłowe i docelowe do przejrzenia w zespole migracji. Każda para zawiera wybór narzędzi i link do pokrewnego przewodnika.

### <a name="migration-type"></a>Typ migracji

W przypadku migracji offline przestój aplikacji rozpoczyna po rozpoczęciu migracji. W przypadku migracji online przestój jest ograniczony do czasu migracji jednorazowej na końcu procesu migracji.

Zalecamy, aby określić akceptowalny przestój biznesowy i przetestować migrację w trybie offline. Należy to sprawdzić, czy czas przywracania spełnia akceptowalne przestoje. Jeśli czas przywracania jest nieakceptowalny, wykonaj migrację online.

|Źródło  |Docelowy  |Narzędzie  |Typ migracji  |Wskazówki  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|Database Migration Service|W trybie offline|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|Database Migration Service|W trybie offline|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server RDS|Azure SQL Database lub Azure SQL Database wystąpienia zarządzanego|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|
|MySQL|Azure Database for MySQL|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mysql-azure-mysql-online)|
|PostgreSQL|Azure Database for PostgreSQL|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-postgresql-azure-postgresql-online)|
|MongoDB|Azure Cosmos DB interfejs API Mongo|Database Migration Service|W trybie offline|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db)|
|MongoDB|Azure Cosmos DB interfejs API Mongo|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-mongodb-cosmos-db-online)|
|Oracle|Różne opcje platformy jako usługi (PaaS) i IaaS|Narzędzie lub Azure Migrate partnera|W trybie offline lub online|[Drzewo decyzyjne](../../migrate/expanded-scope/data-oracle-migration.md)|
|Różne opcje NoSQL DB|Cosmo DB lub IaaS opcje|Migracje proceduralne lub Azure Migrate|W trybie offline lub online|[Drzewo decyzyjne](../../migrate/expanded-scope/data-no-sql-migration.md)|
