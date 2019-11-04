---
title: Przewodnik po decyzjach dotyczących narzędzi migracji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przewodnik po decyzjach dotyczących narzędzi migracji
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.openlocfilehash: f493f53d2cc316a0e4ff7ae75211c5e41bc9d8a8
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73238827"
---
# <a name="migration-tools-decision-guide"></a>Przewodnik po decyzjach dotyczących narzędzi migracji

Wybór strategii i narzędzi używanych do migrowania aplikacji na platformę Azure w dużej mierze będzie zależeć od względów biznesowych, strategii technologicznych i harmonogramów w Twojej firmie, a także od pełnego obrazu rzeczywistego obciążenia i zasobów (infrastruktury, aplikacji i danych), które są migrowane. Przedstawione poniżej drzewo decyzyjne zawiera ogólne wskazówki dotyczące wybierania najlepszych narzędzi na podstawie decyzji związanych z migracją. To drzewo decyzyjne należy traktować jako punkt wyjścia.

Decyzja o przeprowadzeniu migracji przy użyciu technologii platformy jako usługi (PaaS) lub infrastruktury jako usługi (IaaS) zależy od równowagi między kosztami, czasem, istniejącym długiem technicznym i długoterminowymi zwrotami. Technologia IaaS to często najszybsza droga do chmury, wymagająca najmniejszych zmian obciążenia. Technologia PaaS może wymagać modyfikacji struktury danych lub kodu źródłowego, jednak generuje znaczące długoterminowe korzyści w postaci zmniejszenia kosztów operacyjnych i większej elastyczności technicznej. Na poniższym diagramie termin _modernizowanie_ został użyty w celu odzwierciedlenia decyzji o zmodernizowaniu zasobu podczas migracji i przeprowadzaniu migracji zmodernizowanego zasobu na platformę PaaS.

![Przykładowe drzewo decyzyjne dotyczące narzędzi migracji.](../../_images/migrate/migration-tools-decision-tree.png)

## <a name="key-questions"></a>Kluczowe pytania

Udzielenie odpowiedzi na poniższe pytania umożliwia podjęcie decyzji na podstawie powyższego drzewa.

- **Czy inwestycja czasu, energii i zasobów budżetowych w modernizację platformy aplikacji podczas migracji byłaby opłacalna?** Technologie PaaS, takie jak usługi Azure App Service i Azure Functions, mogą zwiększyć elastyczność wdrażania i zmniejszyć złożoność zarządzania maszynami wirtualnymi do hostowania aplikacji. Jednak aplikacje mogą wymagać refaktoryzacji, zanim będą mogły skorzystać z tych natywnych dla chmury możliwości, co potencjalnie może znacząco wydłużyć czas migracji i zwiększyć związane z nią koszty. Jeśli można przeprowadzić migrację aplikacji do technologii PaaS przy minimalnych modyfikacjach, jest ona prawdopodobnie dobrym kandydatem do modernizacji. Jeśli wymagana by była rozległa refaktoryzacja, lepszym wyborem może okazać się migracja przy użyciu maszyn wirtualnych opartych na technologii IaaS.
- **Czy inwestycja czasu, energii i zasobów budżetowych w modernizację platformy danych podczas migracji byłaby opłacalna?** Podobnie jak w przypadku migracji aplikacji, opcje magazynu zarządzanego PaaS platformy Azure, takie jak usługi Azure SQL Database, Cosmos DB i Azure Storage, oferują znaczące korzyści w zakresie zarządzania i elastyczności, ale migracja do tych usług może wymagać refaktoryzacji istniejących danych i aplikacji, które z nich korzystają. Platformy danych często wymagają znacznie mniejszej refaktoryzacji niż platforma aplikacji. Z tego względu platformy danych bardzo często są modernizowane, mimo że platforma aplikacji pozostaje taka sama. Jeśli można przeprowadzić migrację danych do usługi danych zarządzanych przy minimalnych zmianach, jest to dobry kandydat do modernizacji. W przypadku danych, których refaktoryzacja w celu skorzystania z tych usług PaaS wymagałaby rozległych inwestycji czasowych i budżetowych, lepiej przeprowadzić migrację przy użyciu maszyn wirtualnych opartych na technologii IaaS, aby uzyskać zgodność z istniejącymi możliwościami hostingu.
- **Czy aplikacja obecnie działa na dedykowanych maszynach wirtualnych, czy współdzieli hosting z innymi aplikacjami?** Aplikację działającą na dedykowanych maszynach wirtualnych można łatwiej zmigrować do opcji hostingu PaaS, niż aplikację działającą na serwerach udostępnionych.
- **Czy migracja danych przekroczy przepustowość sieci?** Pojemność sieci między lokalnymi źródłami danych i platformą Azure może być wąskim gardłem migracji danych. Jeśli danych, które chcesz przetransferować, dotyczą ograniczenia przepustowości uniemożliwiające wydajną i terminową migrację, warto przyjrzeć się alternatywnym mechanizmom transferu lub opcjom w trybie offline. [Artykuł na temat replikacji migracji](../../migrate/migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) w przewodniku Cloud Adoption Framework opisuje, jak ograniczenia replikacji mogą wpłynąć na proces migracji. W ramach oceniania migracji skonsultuj się ze swoimi zespołami IT w celu zweryfikowania, czy przepustowość Waszej sieci lokalnej i sieci WAN jest w stanie obsłużyć wymagania dotyczące migracji. Zapoznaj się też ze [scenariuszem migracji o rozszerzonym zakresie, kiedy wymagania dotyczące magazynu przekraczają pojemność sieci podczas migracji](../../migrate/expanded-scope/network-capacity-exceeded.md#suggested-prerequisites).
- **Czy aplikacja korzysta z istniejącego potoku DevOps?** W wielu przypadkach można z łatwością zrefaktoryzować usługę Azure Pipelines, aby wdrożyć aplikacje w środowiskach hostingu opartych na chmurze.
- **Czy dane mają skomplikowane wymagania dotyczące magazynu danych?** Aplikacje produkcyjne zwykle wymagają magazynu danych, który jest wysoce dostępny, oferuje funkcję Zawsze włączone oraz podobne funkcje czasu działania usługi i ciągłości. Opcje zarządzanej bazy danych opartej na technologii PaaS platformy Azure, takie jak usługi Azure SQL Database, Azure Database for MySQL i Azure Cosmos DB, oferują umowy dotyczące poziomu usług zapewniające 99,99% czasu pracy. Z drugiej strony, oparty na technologii IaaS serwer SQL Server na maszynach wirtualnych platformy Azure oferuje umowy dotyczące poziomu usług z jednym wystąpieniem zapewniające 99,95% czasu pracy. Jeśli danych nie można zmodernizować w celu skorzystania z opcji magazynu w technologii PaaS, zagwarantowanie wyższych czasów działania usług IaaS będzie obejmować bardziej skomplikowane scenariusze magazynowania danych, takie jak uruchomienie zawsze włączonych klastrów serwera SQL Server i stałe synchronizowanie danych między wystąpieniami. Może to generować duże koszty związane z hostingiem i konserwacją, dlatego zrównoważenie wymagań dotyczących czasu działania, pracy związanej z modernizacją i ogólnego wpływu na budżet jest tak ważne w procesie rozważania opcji migracji danych.

## <a name="innovation-and-migration"></a>Innowacje i migracja

Mimo że w przewodniku Cloud Adoption Framework podkreślono [migrację przyrostową](../../migrate/index.md#migration-implementation), początkowa decyzja dotycząca narzędzi i strategii migracji nie wyklucza przyszłych innowacji w celu zaktualizowania aplikacji, aby można było skorzystać z możliwości oferowanych przez platformę Azure. Nawet jeśli początkowe procesy migracji skupiają się głównie na ponownym hostingu przy użyciu technologii IaaS, warto regularnie przyglądać się swoim aplikacjom hostowanym w chmurze, aby badać możliwości optymalizacji.

## <a name="learn-more"></a>Dowiedz się więcej

- **[Podstawy chmury: Omówienie opcji obliczeniowych na platformie Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview).** Zawiera informacje dotyczące możliwości opcji obliczeniowych rozwiązań Azure IaaS i PaaS.
- **[Podstawy chmury: Wybór odpowiedniego magazynu danych](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview).** Omówienie opcji magazynowania technologii PaaS dostępnych na platformie Azure.
- **[Migracja o rozszerzonym zakresie: Wymagania dotyczące danych przekraczają pojemność sieci podczas prac nad migracją](../../migrate/expanded-scope/network-capacity-exceeded.md).** Omówienie alternatywnych mechanizmów migracji danych dla scenariuszy, w których migracja danych jest utrudniona przez dostępną przepustowość sieci.
- **[SQL Database: Wybieranie odpowiedniej opcji programu SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas#business-motivations-for-choosing-databases-managed-instances-or-sql-virtual-machines).** Omówienie opcji i uzasadnień biznesowych dotyczących hostowania obciążeń programu SQL Server w środowisku hostowanej infrastruktury (IaaS) lub hostowanej usługi (PaaS).
