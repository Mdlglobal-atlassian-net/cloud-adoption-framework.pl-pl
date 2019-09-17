---
title: Decyzje projektowe dotyczące gotowości bazy danych na platformę Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decyzje projektowe dotyczące gotowości bazy danych na platformę Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e95817396fb898c3460874e0e63bf793628a4d16
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022049"
---
# <a name="data-design-decisions"></a>Decyzje projektowe dotyczące danych

Przygotowując środowisko strefy docelowej do wdrożenia w chmurze, należy określić wymagania dotyczące danych na potrzeby hostowania obciążeń. Produkty i usługi bazy danych platformy Azure obsługują szeroką gamę scenariuszy i możliwości w zakresie magazynu danych. Sposób konfiguracji środowiska strefy docelowej do obsługi wymagań w zakresie danych zależy od wymagań technicznych i biznesowych oraz związanych z zarządzaniem obciążeniami.

## <a name="identify-data-services-requirements"></a>Identyfikowanie wymagań w zakresie usług danych

W ramach oceny i przygotowania strefy docelowej należy zidentyfikować magazyny danych, które muszą być obsługiwane przez tę strefę. Ten proces polega na ocenie poszczególnych aplikacji i usług, które składają się na obciążenia, aby określić ich wymagania w zakresie magazynów danych i dostępu. Po zidentyfikowaniu i udokumentowaniu tych wymagań można utworzyć zasady dla strefy docelowej w celu kontrolowania dozwolonych typów zasobów w zależności od potrzeb związanych z obciążeniami.

W przypadku każdej aplikacji lub usługi, która zostanie wdrożona w środowisku strefy docelowej, należy użyć następującego drzewa decyzyjnego jako punktu wyjścia, aby ułatwić określenie odpowiednich usług w zakresie magazynu danych:

![Drzewo decyzyjne usług baz danych platformy Azure](../../_images/ready/data-decision-tree.png)

### <a name="key-questions"></a>Kluczowe pytania

Odpowiedz na następujące pytania dotyczące obciążeń, gdyż pomoże to podjąć decyzje na podstawie drzewa decyzyjnego usług baz danych platformy Azure:

- **Czy potrzebujesz pełnej kontroli lub własności oprogramowania baz danych albo systemu operacyjnego hosta?** Niektóre scenariusze wymagają posiadania dużego zakresu kontroli lub własności konfiguracji oprogramowania i serwerów hosta na potrzeby obciążeń baz danych. W tych scenariuszach można wdrożyć niestandardowe maszyny wirtualne typu infrastruktura jako usługa (IaaS), aby w pełni kontrolować wdrażanie i konfigurację usług danych. Jeśli te wymagania nie są spełnione, usługi bazy danych zarządzane przez platformę jako usługę (PaaS) mogą zmniejszyć koszty związane z zarządzaniem i operacjami.
- **Czy obciążenia będą korzystać z technologii relacyjnej bazy danych?** Jeśli tak, jakiej technologii zamierzasz używać? Platforma Azure oferuje możliwości zarządzanej bazy danych PaaS dla [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), [MySQL](https://docs.microsoft.com/azure/mysql/overview), [PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) i [MariaDB](https://docs.microsoft.com/azure/mariadb/overview).
- **Czy obciążenia będą używać programu SQL Server?** Na platformie Azure obciążenia można uruchamiać [w programie SQL Server w usłudze IaaS na maszynach wirtualnych platformy Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) lub w [usłudze hostowanej w ramach usługi Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) w usłudze PaaS. Wybór opcji do użycia zależy przede wszystkim od tego, czy chcesz zarządzać bazą danych, stosować poprawki i tworzyć kopie zapasowe, czy też chcesz delegować te operacje na platformę Azure. W niektórych scenariuszach problemy ze zgodnością mogą wymagać użycia programu SQL Server w usłudze IaaS. Aby uzyskać więcej informacji na temat wybierania prawidłowej opcji dla obciążeń, zobacz temat [Choose the right SQL Server option in Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) (Wybieranie odpowiedniej opcji programu SQL Server na platformie Azure).
- **Czy obciążenia będą korzystać z magazynu bazy danych kluczy/wartości?** Usługa [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) oferuje bardzo wydajne buforowane rozwiązanie magazynu danych kluczy/wartości, które może wspierać szybkie, skalowalne aplikacje. Usługa [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) również oferuje możliwości magazynu kluczy/wartości ogólnego przeznaczenia.
- **Czy obciążenia będą korzystać z danych dokumentu lub grafu?** [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) to wielomodelowa usługa bazy danych, która obsługuje szeroką gamę typów danych i interfejsów API. Usługa Azure Cosmos DB również oferuje możliwości bazy danych dokumentów i grafów.
- **Czy obciążenia będą korzystać z danych rodziny kolumn?** Klaster [Apache HBase w usłudze Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) bazuje na oprogramowaniu Apache Hadoop. Obsługuje ono duże ilości danych bez struktury i z częściową strukturą w bazie danych bez schematu uporządkowanej według rodzin kolumn.
- **Czy Twoje obciążenia będą wymagały możliwości analizy danych o wysokiej wydajności?** Za pomocą usługi [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) można skutecznie przechowywać petabajty danych strukturalnych oraz wykonywać dotyczące ich zapytania. W przypadku obciążeń danych big data bez struktury można użyć usługi [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) do przechowywania i analizy petabajtowych plików i bilionów obiektów.
- **Czy obciążenia będą wymagać możliwości wyszukiwarki?** Za pomocą usługi [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) można tworzyć indeksy wyszukiwania oparte na chmurze, ulepszone przy użyciu sztucznej inteligencji, które można zintegrować z aplikacjami.
- **Czy obciążenia będą korzystać z danych szeregów czasowych?** Usługa [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-overview) służy do przechowywania, wizualizacji i wykonywania zapytań dotyczących dużych ilości danych szeregów czasowych, np. danych generowanych przez urządzenia IoT.

> [!NOTE]
> Więcej informacji na temat oceny opcji baz danych dla poszczególnych aplikacji lub usług znajduje się w temacie [Azure application architecture guide](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-comparison) (Kryteria wyboru magazynu danych).

## <a name="common-database-scenarios"></a>Typowe scenariusze baz danych

W poniższej tabeli przedstawiono kilka wymagań w zakresie typowych scenariuszy użycia oraz usługi baz danych zalecane do ich obsługi:

| **Scenariusz** | **Usługa danych** |
|-----|-----|
| Potrzebuję wielomodelowej bazy danych o globalnej dystrybucji z obsługą rozwiązań NoSQL. | [Usługi Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) |
| Potrzebuję w pełni zarządzanej relacyjnej bazy danych z szybkim inicjowaniem obsługi, skalowaniem na bieżąco oraz wbudowaną inteligencją i zabezpieczeniami. | [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) |
| Potrzebuję w pełni zarządzanej i skalowalnej relacyjnej bazy danych MySQL o wysokiej dostępności i z wbudowanymi zabezpieczeniami bez dodatkowych kosztów. | [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) |
| Potrzebuję w pełni zarządzanej i skalowalnej relacyjnej bazy danych PostgreSQL o wysokiej dostępności i z wbudowanymi zabezpieczeniami bez dodatkowych kosztów. | [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) |
| Planuję obsługę aplikacji SQL Server przedsiębiorstwa w chmurze i przejęcie pełnej kontroli nad systemem operacyjnym serwera. | [Program SQL Server w usłudze Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) |
| Potrzebuję w pełni zarządzanego elastycznego magazynu danych z zabezpieczeniami na każdym poziomie skalowania bez dodatkowych kosztów. | [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) |
| Potrzebuję zasobów usługi Data Lake Storage, które mogą obsługiwać klastry Hadoop lub dane systemu plików HDFS. | [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) |
| Potrzebuję wysokiej przepływności i dostępu do danych ze stałymi, niskimi opóźnieniami, co pozwoli na obsługę szybkich i skalowalnych aplikacji. | [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) |
| Potrzebuję w pełni zarządzanej i skalowalnej relacyjnej bazy danych MariaDB o wysokiej dostępności i z wbudowanymi zabezpieczeniami bez dodatkowych kosztów. | [Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb/overview) |

## <a name="regional-availability"></a>Dostępność regionalna

Platforma Azure pozwala na dostarczanie usług w potrzebnej skali, aby dotrzeć do klientów i partnerów,  _gdziekolwiek są_. Kluczową kwestią podczas planowania wdrożenia w chmurze jest określenie, który region świadczenia usługi Azure będzie obsługiwać zasoby obciążenia.

Większość usług bazy danych jest ogólnie dostępna w większości regionów Azure. Istnieje jednak kilka regionów, głównie przeznaczonych dla instytucji rządowych, które obsługują tylko podzbiór tych produktów. Przed podjęciem decyzji o regionach, w których zostaną wdrożone zasoby baz danych, zalecamy zapoznanie się ze [stroną z regionami](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=data-factory,sql-server-stretch-database,redis-cache,database-migration,sql-data-warehouse,postgresql,mariadb,cosmos-db,mysql,sql-database) w celu sprawdzenia najnowszego stanu dostępności regionalnej.

Aby dowiedzieć się więcej o globalnej infrastrukturze platformy Azure, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/global-infrastructure/regions). Aby uzyskać szczegółowe informacje o ogólnych usługach dostępnych w poszczególnych regionach platformy Azure, można także wyświetlić  [dostępność produktów według regionów](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all).

## <a name="data-residency-and-compliance-requirements"></a>Wymagania dotyczące miejsca przechowywania danych oraz ich zgodności

Twoich obciążeń często dotyczą wymagania prawne i umowne związane z magazynem danych. Te wymagania mogą się różnić w zależności od lokalizacji organizacji, jurysdykcji, której podlegają zasoby fizyczne obsługujące magazyny danych, oraz od sektora działalności. Ze względu na obowiązki związane z danymi, należy wziąć pod uwagę następujące elementy: klasyfikacja danych, lokalizacja danych oraz odpowiednie obowiązki w zakresie ochrony danych w ramach modelu dzielenia się odpowiedzialnością. Aby łatwiej zrozumieć te wymagania, zobacz oficjalny dokument  [Rezydencja i bezpieczeństwo zgodnych danych na platformie Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Niektóre działania związane ze zgodnością mogą obejmować kontrolowanie tego, gdzie będą fizycznie umieszczone zasoby bazy danych. Regiony świadczenia usługi Azure są zorganizowane w grupy nazywane lokalizacjami geograficznymi.  [Lokalizacja geograficzna platformy Azure](https://azure.microsoft.com/global-infrastructure/geographies)  zapewnia, że wymagania z zakresu odporności, zgodności, niezależności i rezydencji danych są honorowane w granicach geograficznych i politycznych. Jeśli obciążenia podlegają suwerenności danych lub innym wymaganiom dotyczącym zgodności, należy wdrożyć zasoby magazynu w regionach, które znajdują się w zgodnej lokalizacji geograficznej platformy Azure.

## <a name="establish-controls-for-database-services"></a>Ustanawianie kontrolek dla usług baz danych

Podczas przygotowywania środowiska strefy docelowej można ustanowić kontrolki ograniczające magazyny danych, które mogą być wdrażane przez poszczególnych użytkowników. Kontrolki te ułatwiają zarządzanie kosztami i ograniczają zagrożenia bezpieczeństwa, a jednocześnie umożliwiają deweloperom i zespołom IT wdrażanie i konfigurowanie zasobów, które są potrzebne do obsługi obciążeń.

Po określeniu i udokumentowaniu wymagań strefy docelowej można użyć usługi [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) w celu kontrolowania zasobów baz danych, na których tworzenie zezwolisz użytkownikom. Kontrolki mogą mieć postać [zezwolenia lub odmowy tworzenia typów zasobów baz danych](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Można na przykład ograniczyć możliwości użytkowników tylko do tworzenia zasobów usługi Azure SQL Database. Za pomocą zasad można również kontrolować opcje dozwolone podczas tworzenia zasobu, takie jak [ograniczanie możliwości ustanawiania jednostek SKU usługi SQL Database](https://docs.microsoft.com/azure/governance/policy/samples/allowed-sql-db-skus) lub zezwalanie na instalację na maszynie wirtualnej w usłudze IaaS [tylko określonych wersji programu SQL Server](https://docs.microsoft.com/azure/governance/policy/samples/require-sql-12).

Zakres zasad może obejmować zasoby, grupy zasobów, subskrypcje i grupy zarządzania. Zasady można uwzględniać w definicjach usługi [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) i stosować je wielokrotnie w całej chmurze.
