---
title: Omówienie przykładów migracji aplikacji na platformę Azure
description: Omówienie przykładów migracji aplikacji opisanych w sekcji dotyczącej migracji podręcznika Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 639d90285c1500a661e872931456f63c188daafc
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337457"
---
# <a name="application-migration-patterns-and-examples"></a>Wzorce i przykłady dotyczące migracji aplikacji

Ta sekcja podręcznika Cloud Adoption Framework zawiera przykłady kilku typowych scenariuszy migracji i pokazuje, jak można migrować lokalną infrastrukturę do chmury platformy [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure).

## <a name="introduction"></a>Wprowadzenie

Platforma Azure zapewnia dostęp do rozbudowanego zestawu usług w chmurze. Deweloperzy i informatycy mogą korzystać z tych usług, aby tworzyć i wdrażać aplikacje oraz zarządzać nimi przy użyciu różnych narzędzi i platform za pośrednictwem globalnej sieci centrów danych. Jeśli Twoja firma ma problem z przejściem do środowiska cyfrowego, chmura platformy Azure może ułatwić określenie sposobu optymalizacji zasobów i operacji, komunikację z klientami i pracownikami oraz przekształcanie produktów.

Jednak w przypadku platformy Azure uwzględniono fakt, że mimo wszystkich zalet chmury w zakresie szybkości, elastyczności, wydajności, niezawodności i minimalizowania kosztów wiele organizacji będzie musiało jeszcze przez jakiś czas korzystać z lokalnych centrów danych. W odpowiedzi na problemy z dostosowaniem chmury platforma Azure udostępnia strategię chmury hybrydowej, która stanowi pomost między lokalnymi centrami danych i chmurą publiczną platformy Azure. Dotyczy to na przykład używania zasobów w chmurze platformy Azure, takich jak usługa Azure Backup, która umożliwia ochronę zasobów lokalnych, lub usługa Azure Analytics zapewniająca wgląd w obciążenia lokalne.

W ramach strategii chmury hybrydowej platforma Azure udostępnia rozwijające się rozwiązania do migrowania lokalnych aplikacji i obciążeń do chmury. Wystarczy wykonać proste czynności, aby kompleksowo ocenić zasoby lokalne i określić, jak będą działać w chmurze platformy Azure. Następnie po przeprowadzeniu szczegółowej oceny można bez obaw zmigrować zasoby na platformę Azure. Gdy zasoby są uruchomione na platformie Azure, można je zoptymalizować w celu zachowania i poprawy dostępu, elastyczności, bezpieczeństwa i niezawodności.

## <a name="migration-patterns"></a>Wzorce migracji

Strategie migracji do chmury można podzielić na cztery ogólne wzorce: ponowne hostowanie, refaktoryzacja, zmiana architektury i ponowne kompilowanie. To, którą strategię chcesz przyjąć, zależy od Twoich celów biznesowych i celów migracji. Można też zastosować kilka wzorców jednocześnie. Można na przykład wybrać opcję rehostować proste aplikacje lub aplikacje, które nie mają krytycznego znaczenia dla Twojej firmy, ale rozbudowanych aplikacji, które są bardziej skomplikowane i mają krytyczne znaczenie dla firmy. Przyjrzyjmy się tym wzorcom.

<!-- markdownlint-disable MD033 -->

**Wzorzec** | **Definicja** | **Kiedy stosować**
--- | --- | ---
**Ponowne hostowanie** | Często określana jako _przenoszony i przesunięty_ proces migracji. Ta opcja nie wymaga wprowadzania zmian w kodzie i umożliwia szybką migrację istniejących aplikacji na platformę Azure. Każda aplikacja jest migrowana bez zmian, co umożliwia wykorzystanie zalet chmury bez ryzyka i kosztów związanych z wprowadzaniem zmian w kodzie. | Gdy musisz szybko przenieść aplikacje do chmury.<br/><br/> Gdy chcesz przenieść aplikację bez zmian.<br/><br/> Gdy aplikacje są zaprojektowane w sposób umożliwiający wykorzystanie skalowalności usług [IaaS platformy Azure](https://azure.microsoft.com/overview/what-is-iaas) po migracji.<br/><br/> Gdy aplikacje są ważne dla Twojej firmy, ale nie musisz wprowadzać natychmiastowych zmian w ich możliwościach.
**Refaktoryzacja** | Refaktoryzacja (często określana jako „ponowne tworzenie pakietów”) wymaga wprowadzenia minimalnych zmian w aplikacjach, tak aby umożliwić połączenie ich z usługami [PaaS platformy Azure](https://azure.microsoft.com/overview/what-is-paas) i wykorzystanie możliwości, jakie daje chmura.<br/><br/> Możesz na przykład migrować istniejące aplikacje do usługi Azure App Service lub Azure Kubernetes Service.<br/><br/> Możesz również refaktoryzować relacyjne i nierelacyjne bazy danych, korzystając z opcji takich jak wystąpienie zarządzane usługi Azure SQL Database czy usługi Azure Database for MySQL, Azure Database for PostgreSQL i Azure Cosmos DB. | Kiedy możliwe jest przeprowadzenie ponownego umieszczania Twojej aplikacji w pakietach pod kątem pracy na platformie Azure.<br/><br/> Jeśli chcesz zastosować innowacyjne rozwiązania metodyki DevOps dostępne na platformie Azure lub rozważasz użycie metodyki DevOps ze strategią kontenerów dla obciążeń.<br/><br/> W przypadku refaktoryzacji musisz wziąć pod uwagę przenośność istniejącego kodu podstawowego i dostępne umiejętności deweloperskie.
**Zmiana architektury** | Zmiana architektury na potrzeby migracji ma na celu modyfikację i rozszerzenie funkcjonalności aplikacji i kodu podstawowego w celu zoptymalizowania architektury aplikacji pod kątem skalowalności w chmurze.<br/><br/> Możesz na przykład podzielić aplikację monolityczną na grupę współdziałających mikrousług, które można łatwo skalować.<br/><br/> Możesz też zmienić architekturę swoich relacyjnych i nierelacyjnych baz danych na w pełni zarządzane rozwiązanie bazy danych, takie jak wystąpienie zarządzane usługi Azure SQL Database lub usługi Azure Database for MySQL, Azure Database for PostgreSQL i Azure Cosmos DB. | Gdy aplikacje wymagają wprowadzenia dużych zmian w celu udostępnienia nowych funkcji lub zapewnienia skutecznego działania na platformie w chmurze.<br/><br/> Jeśli chcesz korzystać z istniejących inwestycji w aplikacje, Spełniaj wymagania dotyczące skalowalności, stosuj innowacyjne praktyki DevOps i Minimalizuj użycie maszyn wirtualnych.
**Ponowna kompilacja** | Ponowne kompilowanie to wyższy poziom — polega na ponownym skompilowaniu aplikacji od podstaw przy użyciu technologii w chmurze platformy Azure.<br/><br/> Można na przykład tworzyć aplikacje zielonego pola z technologiami [natywnymi w chmurze](https://azure.com/cloudnative) , takimi jak Azure Functions, Azure AI, Azure SQL Database Managed Instance i Azure Cosmos DB. | Jeśli konieczne jest szybkie tworzenie zawartości, a istniejące aplikacje mają ograniczoną funkcjonalność lub okres eksploatacji.<br/><br/> Gdy firma jest gotowa do wprowadzenia innowacji (w tym rozwiązań metodyki DevOps oferowanych przez platformę Azure), tworzenia nowych aplikacji przy użyciu technologii natywnych dla chmury i korzystania z najnowszych rozwiązań w dziedzinie sztucznej inteligencji, łańcucha bloków i Internetu rzeczy.

<!-- markdownlint-enable MD033 -->

## <a name="migration-example-articles"></a>Artykuły zawierające przykłady migracji

W tej sekcji przedstawiono przykłady kilku typowych scenariuszy migracji. Każdy przykład zawiera informacje w tle i szczegółowe scenariusze wdrażania, które ilustrują sposób konfigurowania infrastruktury migracji i oceny przydatności zasobów lokalnych na potrzeby migracji. Więcej artykułów zostanie dodanych do tej sekcji w przyszłości.

![Typowe projekty migracji/modernizacji](./media/migration-patterns.png)

*Typowe kategorie projektów migracji i modernizacji.*

Podsumowanie artykułów w tej serii znajduje się poniżej.

- Każdy scenariusz uwzględnia nieco inne cele biznesowe, które determinują strategię migracji.
- W przypadku każdego scenariusza wdrożenia zapewniamy informacje na temat celów biznesowych, proponowanej architektury, czynności do wykonania podczas migracji, zaleceń dotyczących czyszczenia zasobów oraz kolejnych czynności, które należy wykonać po zakończeniu migracji.

### <a name="assessment"></a>Ocena

**Artykuł** | **Szczegóły**
--- | ---
[Assess on-premises resources for migration to Azure (Ocena zasobów lokalnych pod kątem migracji do platformy Azure)](../../plan/contoso-migration-assessment.md) | W tym artykule o najlepszych rozwiązaniach opisano sposób uruchamiania oceny aplikacji lokalnej działającej w oprogramowaniu VMware. W tym artykule Przykładowa organizacja ocenia maszyny wirtualne aplikacji przy użyciu usługi Azure Migrate, a aplikacja SQL Server bazę danych przy użyciu Data Migration Assistant.

### <a name="infrastructure"></a>Infrastruktura

**Artykuł** | **Szczegóły**
--- | ---
[Deploy Azure infrastructure (Wdrażanie infrastruktury platformy Azure)](./contoso-migration-infrastructure.md) | W tym artykule pokazano, jak organizacja może przygotować swoją lokalną infrastrukturę i infrastrukturę platformy Azure do migracji. Przykładowa architektura utworzona w tym artykule jest używana również w innych przykładach przedstawionych w tej sekcji.

### <a name="windows-server-workloads"></a>Obciążenia systemu Windows Server

**Artykuł** | **Szczegóły**
--- | ---
[Rehost an app on Azure VMs (Ponowne hostowanie aplikacji na maszynach wirtualnych platformy Azure)](./contoso-migration-rehost-vm.md) | W tym artykule przedstawiono przykład migrowania lokalnych maszyn wirtualnych aplikacji na maszyny wirtualne platformy Azure przy użyciu usługi Site Recovery.
[Rearchitect an app in Azure containers and Azure SQL Database (Zmienianie architektury aplikacji w kontenerach platformy Azure i usłudze Azure SQL Database)](./contoso-migration-rearchitect-container-sql.md) | W tym artykule przedstawiono przykład migrowania aplikacji z jednoczesną zmianą architektury warstwy internetowej aplikacji na kontener systemu Windows uruchomiony w usłudze Azure Service Fabric oraz zmianą bazy danych na usługę Azure SQL Database.

### <a name="linux-workloads"></a>Obciążenia systemu Linux

**Artykuł** | **Szczegóły**
--- | ---
[Rehost a Linux app on Azure VMs and Azure Database for MySQL (Ponowne hostowanie aplikacji systemu Linux na maszynach wirtualnych platformy Azure i w usłudze Azure Database for MySQL)](./contoso-migration-rehost-linux-vm-mysql.md) | W tym artykule przedstawiono przykład migrowania aplikacji hostowanej w systemie Linux na maszyny wirtualne platformy Azure przy użyciu usługi Site Recovery. Baza danych aplikacji jest migrowana do usługi Azure Database for MySQL za pomocą programu MySQL Workbench.
[Rehost a Linux app on Azure VMs (Ponowne hostowanie aplikacji systemu Linux na maszynach wirtualnych platformy Azure)](./contoso-migration-rehost-linux-vm.md) | Ten przykład pokazuje, jak ukończyć podnieśność i przesunięcia migracji aplikacji opartej na systemie Linux na maszyny wirtualne platformy Azure przy użyciu usługi Site Recovery.

### <a name="sql-server-workloads"></a>Obciążenia programu SQL Server

**Artykuł** | **Szczegóły**
--- | ---
[Rehost an app on an Azure VM and SQL Database Managed Instance (Ponowne hostowanie aplikacji na maszynie wirtualnej platformy Azure i w wystąpieniu zarządzanym usługi SQL Database)](./contoso-migration-rehost-vm-sql-managed-instance.md) | W tym artykule przedstawiono przykład przenośnika i przesunięcia migracji na platformę Azure dla aplikacji lokalnej. Ten proces polega na migrowaniu maszyny wirtualnej frontonu aplikacji przy użyciu [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)i bazy danych aplikacji do Azure SQL Database wystąpienia zarządzanego przy użyciu [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).
[Rehost an app on Azure VMs and in a SQL Server Always On availability group (Ponowne hostowanie aplikacji na maszynach wirtualnych platformy Azure i w zawsze włączonych grupach dostępności programu SQL Server)](./contoso-migration-rehost-vm-sql-ag.md) | W tym przykładzie pokazano, jak migrować aplikacje i dane przy użyciu maszyn wirtualnych z programem SQL Server hostowanych na platformie Azure. W tej metodzie użyto usługi Site Recovery do migrowania maszyn wirtualnych aplikacji oraz usługi Azure Database Migration Service do migrowania bazy danych aplikacji do klastra programu SQL Server chronionego przez zawsze włączoną grupę dostępności.

### <a name="aspnet-php-and-java-apps"></a>Aplikacje ASP.NET, PHP i Java

**Artykuł** | **Szczegóły**
--- | ---
[Refactor an app in an Azure web app and Azure SQL Database (Refaktoryzacja aplikacji w aplikacji internetowej platformy Azure i usłudze Azure SQL Database)](./contoso-migration-refactor-web-app-sql.md) | W tym przykładzie pokazano, jak migrować lokalną aplikację opartą na systemie Windows do aplikacji internetowej platformy Azure, a bazę danych aplikacji do wystąpienia programu Azure SQL Server za pomocą usługi Data Migration Assistant.
[Refactor a Linux app to multiple regions using Azure App Service, Azure Traffic Manager, and Azure Database for MySQL (Refaktoryzacja aplikacji systemu Linux do wielu regionów za pomocą usług Azure App Service, Azure Traffic Manager i Azure Database for MySQL)](./contoso-migration-refactor-linux-app-service-mysql.md) | W tym przykładzie pokazano, jak migrować lokalną aplikację opartą na systemie Linux do aplikacji internetowej platformy Azure w wielu regionach platformy Azure przy użyciu usługi Azure Traffic Manager zintegrowanej z usługą GitHub w celu ciągłego dostarczania. Baza danych aplikacji jest migrowana do wystąpienia usługi Azure Database for MySQL.
[Rebuild an app in Azure (Ponowne kompilowanie aplikacji na platformie Azure)](./contoso-migration-rebuild.md) | W tym artykule pokazano przykład ponownego kompilowania aplikacji lokalnej przy użyciu wielu funkcji i usług zarządzanych platformy Azure, takich jak Azure App Service, Azure Kubernetes Service, Azure Functions, Azure Cognitive Services i Azure Cosmos DB.
[Refactor Team Foundation Server on Azure DevOps Services (Refaktoryzacja serwera Team Foundation Server w usłudze Azure DevOps Services)](./contoso-migration-tfs-vsts.md) | W tym artykule pokazano przykład migracji lokalnego wdrożenia serwera Team Foundation Server do usługi Azure DevOps Services na platformie Azure.

### <a name="migration-scaling"></a>Skalowanie migracji

**Artykuł** | **Szczegóły**
--- | ---
[Scale a migration to Azure (Skalowanie migracji na platformę Azure)](./contoso-migration-scale.md) | W tym artykule pokazano, jak przykładowa organizacja przygotowuje się do pełnej, skalowanej migracji na platformę Azure.

### <a name="demo-apps"></a>Aplikacje przykładowe

Przykładowe artykuły podane w tej sekcji wykorzystują dwie aplikacje demonstracyjne: SmartHotel360 i osTicket.

- **SmartHotel360:** Ta aplikacja została opracowana przez firmę Microsoft jako aplikacja testowa, której można używać podczas pracy z platformą Azure. Jest to aplikacja typu open source i można pobrać ją z witryny [GitHub](https://github.com/Microsoft/SmartHotel360). Jest to aplikacja ASP.NET połączona z bazą danych programu SQL Server. W scenariuszach omówionych w tych artykułach bieżąca wersja tej aplikacji jest wdrożona na dwóch maszynach wirtualnych VMware z systemem Windows Server 2008 R2 i programem SQL Server 2008 R2. Te maszyny wirtualne aplikacji są hostowane lokalnie i są zarządzane przez program vCenter Server.
- **osTicket:** Aplikacja do tworzenia biletów w ramach usługi Open Source działająca w systemie Linux. Można ją pobrać z witryny [GitHub](https://github.com/osTicket/osTicket). W scenariuszach omówionych w tych artykułach bieżąca wersja tej aplikacji jest wdrożona lokalnie na dwóch maszynach wirtualnych VMware z systemem Ubuntu 16.04 LTS, korzystających z platformy Apache 2, języka PHP 7.0 i programu MySQL 5.7
