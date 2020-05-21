---
title: Migrowanie elementów zawartości
description: Zainicjuj migrację na platformę Azure, dobierając właściwe narzędzia do użycia, w tym narzędzia natywne, narzędzia innych firm i narzędzia do zarządzania projektami.
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 574dba7b2c5db10b007dcf6cb7ecdd6dc93a0111
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401164"
---
<!-- cSpell:ignore Cloudamize agentless uncontained SSMA Carbonite Movere -->

# <a name="deploy-workloads-and-assets-infrastructure-apps-and-data"></a>Wdrażanie obciążeń i zasobów (infrastruktury, aplikacji i danych)

W tej fazie podróży należy użyć danych wyjściowych fazy oceny do zainicjowania migracji środowiska. Ten przewodnik pomaga zidentyfikować odpowiednie narzędzia pozwalające ukończyć ten proces, między innymi narzędzia natywne, narzędzia innych firm oraz narzędzia do zarządzania projektami.

<!-- markdownlint-disable MD025 -->

# <a name="native-migration-tools"></a>[Narzędzia natywne migracji](#tab/Tools)

W poniższych sekcjach opisano narzędzia natywne platformy Azure dostępne do przeprowadzenia migracji lub do jej ułatwienia. Aby uzyskać informacje na temat doboru odpowiednich narzędzi do wspierania działań związanych z migracją, zobacz temat [Przewodnik po decyzjach dotyczących narzędzi migracji](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Usługa Azure Migrate zapewnia ujednolicone i elastyczne środowisko migracji. Usługa Azure Migrate zapewnia jedno dedykowane środowisko do śledzenia podróży migracji w fazach oceny i migracji na platformę Azure. Umożliwia ona korzystanie z wybranych narzędzi i śledzenie postępu migracji w ramach tych narzędzi.

Usługa Azure Migrate zapewnia następujące funkcje:

1. Ulepszone możliwości oceny i migracji:
    - Oceny funkcji Hyper-V.
    - Ulepszona ocena programu VMware.
    - Migracja bez agenta maszyn wirtualnych programu VMware na platformę Azure.
1. Ujednolicenie oceny, migracji i śledzenia postępu.
1. Elastyczne podejście dzięki integracji z niezależnym dostawcą oprogramowania (np. Cloudamize).

Aby przeprowadzić migrację przy użyciu usługi Azure Migrate, wykonaj następujące kroki:

1. Wyszukaj usługę Azure Migrate w obszarze **Wszystkie usługi**. Aby kontynuować, wybierz pozycję **Azure Migrate**.
1. Wybierz opcję **Dodaj narzędzie**, aby rozpocząć projekt migracji.
1. Wybierz subskrypcję, grupę zasobów i lokalizację geograficzną, aby przeprowadzić migrację.
1. Wybierz kolejno opcje **Wybierz narzędzie oceny** > **Azure Migrate: Ocena serwera** >  **Dalej**.
1. Wybierz opcję **Przejrzyj i dodaj narzędzia** i sprawdź konfigurację. Wybierz pozycję **Dodaj narzędzia**, aby zainicjować zadanie tworzenia projektu migracji i zarejestrować wybrane rozwiązania.

### <a name="learn-more"></a>Dowiedz się więcej

- [Samouczek usługi Azure Migrate — migrowanie serwerów fizycznych lub zwirtualizowanych na platformę Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

Usługa Azure Site Recovery może zarządzać migracją zasobów lokalnych na platformę Azure. Może również zarządzać odzyskiwaniem po awarii maszyn lokalnych i maszyn wirtualnych platformy Azure i organizować ten proces w celu zapewnienia ciągłości działania i odzyskiwania po awarii (BCDR).

W poniższych krokach przedstawiono proces korzystania z usługi Site Recovery w celu migracji:

> [!TIP]
> W zależności od scenariusza faktyczne kroki mogą być nieco inne. Aby uzyskać więcej informacji, zobacz artykuł [Migrate on-premises machines to Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure) (Migrowanie maszyn lokalnych na platformę Azure).

### <a name="prepare-azure-site-recovery-service"></a>Przygotowanie usługi Azure Site Recovery

1. W witrynie Azure Portal wybierz opcje **+Utwórz zasób > Narzędzia do zarządzania > Backup i Site Recovery**.
1. Jeśli magazyn odzyskiwania nie został jeszcze utworzony, ukończ pracę kreatora, aby utworzyć zasób **Magazyn usługi Recovery Services**.
1. W menu **Zasób** wybierz kolejno pozycje **Site Recovery > Przygotuj infrastrukturę > Cel ochrony**.
1. W obszarze **Cel ochrony** wybierz elementy do migracji.
    1. **VMware:** Wybierz kolejno pozycje **Na platformę Azure > Tak, za pomocą programu VMware vSphere Hypervisor**.
    1. **Maszyna fizyczna:** Wybierz kolejno pozycje **Na platformę Azure > Bez wirtualizacji/inne**.
    1. **Hyper-V:** Wybierz kolejno pozycje **Na platformę Azure > Tak, za pomocą funkcji Hyper-V**. Jeśli program VMM zarządza maszynami wirtualnymi funkcji Hyper-V, wybierz pozycję **Tak**.

### <a name="configure-migration-settings"></a>Konfigurowanie ustawień migracji

1. Skonfiguruj odpowiednio środowisko źródłowe.
1. Skonfiguruj środowisko docelowe.
    1. Wybierz kolejno pozycje **Przygotowywanie infrastruktury > Docelowa**, a następnie wybierz subskrypcję platformy Azure do użycia.
    1. Określ model wdrażania usługi Resource Manager.
    1. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.
1. Skonfiguruj zasady replikacji.
1. Włącz replikację.
1. Uruchom migrację testową (test pracy w trybie failover).

### <a name="migrate-to-azure-using-failover"></a>Migrowanie na platformę Azure przy użyciu trybu failover

1. W obszarze **Ustawienia > Zreplikowane elementy** wybierz maszynę wirtualną > **Tryb failover**.
1. W obszarze **Tryb failover** wybierz **Punkt odzyskiwania**, którego chcesz użyć do przełączenia do trybu failover. Wybierz najnowszy punkt odzyskiwania.
1. Skonfiguruj ustawienia klucza szyfrowania zgodnie z wymaganiami.
1. Wybierz pozycję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**. Usługa Site Recovery spróbuje zamknąć maszyny wirtualne przed przejściem do trybu failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się. Na stronie Zadania można śledzić postęp trybu failover.
1. Sprawdź, czy maszyna wirtualna Azure jest wyświetlana na platformie Azure zgodnie z oczekiwaniami.
1. W obszarze **Replikowane elementy** kliknij prawym przyciskiem myszy maszynę wirtualną i wybierz pozycję **Zakończ migrację**.
1. Wykonaj wszystkie kroki wykonywane po migracji zgodnie z wymaganiami (zobacz odpowiednie informacje w tym przewodniku).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Aby uzyskać więcej informacji, zobacz:

- [Migrowanie maszyn lokalnych na platformę Azure](https://docs.microsoft.com/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Usługa Azure Database Migration Service jest w pełni zarządzaną usługą, która umożliwia bezproblemową migrację z wielu źródeł baz danych na platformy danych Azure przy minimalnych przestojach (migracja w trybie online). Usługa Azure Database Migration Service wykonuje wszystkie wymagane kroki. Możesz zainicjować swoje projekty migracji z gwarancją, że w procesie są wykorzystywane najlepsze rozwiązania zalecane przez firmę Microsoft.

### <a name="create-an-azure-database-migration-service-instance"></a>Tworzenie wystąpienia usługi Azure Database Migration Service

Jeśli usługa Azure Database Migration Service jest używana po raz pierwszy, należy zarejestrować dostawcę zasobów dla subskrypcji platformy Azure:

1. Wybierz kolejno pozycje **Wszystkie usługi** i **Subskrypcje**, a następnie wybierz subskrypcję docelową.
1. Wybierz pozycję **Dostawcy zasobów**.
1. Wyszukaj element `migration`, a następnie po prawej stronie pozycji **Microsoft.DataMigration** wybierz pozycję **Zarejestruj**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Po zarejestrowaniu dostawcy zasobów można utworzyć wystąpienie usługi Azure Database Migration Service.

1. Wybierz pozycję **+Utwórz zasób** i wyszukaj na platformie handlowej pozycję **Azure Database Migration Service**.
1. Ukończ pracę kreatora **Tworzenie usługi migracji** i wybierz pozycję **Utwórz**.

Usługa jest teraz gotowa do migracji obsługiwanych źródłowych baz danych (na przykład SQL Server, MySQL, PostgreSQL lub MongoDB).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Aby uzyskać więcej informacji, zobacz:

- [Omówienie usługi Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview)
- [Tworzenie wystąpienia usługi Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal)
- [Usługa Azure Migrate w witrynie Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade)
- [Witryna Azure portal: tworzenie projektu migracji](https://portal.azure.com/#create/Microsoft.AzureMigrate)

::: zone-end

## <a name="data-migration-assistant"></a>Data Migration Assistant

Narzędzie Data Migration Assistant (DMA) ułatwia uaktualnianie do nowoczesnej platformy danych dzięki możliwości wykrywania problemów ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych w nowej wersji platformy SQL Server lub bazy danych Azure SQL Database. DMA zaleca ulepszenia poprawiające wydajność i niezawodność środowiska docelowego i umożliwia przenoszenie schematu, danych i obiektów otwartych z serwera źródłowego na serwer docelowy.

> [!NOTE]
> W przypadku dużych migracji (pod względem liczby i rozmiaru baz danych) zaleca się użycie usługi Azure Database Migration Service, która może migrować bazy danych na dużą skalę.
>

Zacznij korzystać z narzędzia Data Migration Assistant, wykonując następujące kroki:

1. Pobierz i zainstaluj narzędzie Data Migration Assistant z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=53595).
1. Utwórz ocenę, wybierając ikonę **Nowy (+)** i wybierając typ projektu **Ocena**.
1. Ustaw typ serwera źródłowego i serwera docelowego, a następnie wybierz pozycję **Utwórz**.
1. Skonfiguruj opcje oceny zgodnie z wymaganiami (zalecane są wszystkie ustawienia domyślne).
1. Dodaj bazy danych do oceny.
1. Wybierz pozycję **Dalej**, aby rozpocząć ocenę.
1. Wyświetl wyniki w zestawie narzędzi Data Migration Assistant.

W przypadku przedsiębiorstwa zalecamy zastosowanie rozwiązania przedstawionego w temacie [Assess an enterprise and consolidate assessment reports with DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports) (Ocena przedsiębiorstwa i konsolidowanie raportów oceny za pomocą narzędzia DMA) do oceny wielu serwerów, połączenia raportów, a następnie użycia dostarczonych raportów usługi Power BI do analizy wyników.

Aby uzyskać więcej informacji, m.in. szczegółowe instrukcje dotyczące użycia, zobacz:

- [Data Migration Assistant overview](https://docs.microsoft.com/sql/dma/dma-overview) (Omówienie narzędzia Data Migration Assistant)
- [Assess an enterprise and consolidate assessment reports with DMA](https://docs.microsoft.com/sql/dma/dma-consolidatereports) (Ocena przedsiębiorstwa i konsolidowanie raportów oceny za pomocą narzędzia DMA)
- [Analyze consolidated assessment reports created by Data Migration Assistant with Power BI](https://docs.microsoft.com/sql/dma/dma-powerbiassesreport) (Analizowanie skonsolidowanych raportów oceny utworzonych przez narzędzie Data Migration Assistant za pomocą usługi Power BI)

## <a name="sql-server-migration-assistant"></a>Asystent migracji do programu SQL Server

Asystent migracji do programu Microsoft SQL Server (SSMA) to narzędzie służące do automatyzowania migracji bazy danych do programu SQL Server z programów Microsoft Access, DB2, MySQL, Oracle i SAP ASE. Ogólna koncepcja polega na zbieraniu, ocenianiu, a następnie przeglądaniu za pomocą tych narzędzi, jednak ze względu na wariancje procesu dla każdego z systemów źródłowych zalecamy przejrzenie szczegółowej [dokumentacji dotyczącej Asystenta migracji do programu SQL Server](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant).

Aby uzyskać więcej informacji, zobacz:

- [Omówienie dotyczące Asystenta migracji do programu SQL Server](https://docs.microsoft.com/sql/ssma/sql-server-migration-assistant)

## <a name="database-experimentation-assistant"></a>Asystent eksperymentowania z bazą danych

Asystent eksperymentowania z bazą danych jest nowym rozwiązaniem do testowania A/B dla uaktualnień platformy SQL Server. Pomaga w ocenie wersji docelowej platformy SQL dla danego obciążenia. Klienci, którzy uaktualniają z poprzednich wersji programu SQL Server (SQL Server 2005 i nowszych) do dowolnej nowej wersji programu SQL Server, mogą korzystać z tych metryk analizy.

Asystent eksperymentowania z bazą danych obejmuje następujące działania przepływu pracy:

- **Przechwytywanie:** Pierwszym krokiem testowania A/B programu SQL Server jest przechwycenie śladu na serwerze źródłowym. Serwer źródłowy jest zazwyczaj serwerem produkcyjnym.
- **Ponowne odtwarzanie:** Drugim krokiem testowania A/B programu SQL Server jest ponowne odtworzenie przechwyconego pliku śledzenia na serwerach docelowych. Następnie należy zebrać obszerne ślady z ponownych odtworzeń na potrzeby analizy.
- **Analiza:** Ostatnim krokiem jest wygenerowanie raportu analizy przy użyciu śladów ponownego odtwarzania. Raport analizy może pomóc w uzyskaniu szczegółowych informacji na temat wpływu proponowanej zmiany na wydajność.

Aby uzyskać więcej informacji, zobacz:

- [Overview of Database Experimentation Assistant](https://docs.microsoft.com/sql/dea/database-experimentation-assistant-overview) (Omówienie dotyczące Asystenta eksperymentowania z bazą danych)

## <a name="azure-cosmos-db-data-migration-tool"></a>Narzędzie do migracji danych usługi Azure Cosmos DB

Narzędzie do migracji danych usługi Azure Cosmos DB umożliwia importowanie danych z różnych źródeł do kolekcji i tabel usługi Azure Cosmos DB. Dane można importować z plików JSON, plików CSV, kodu SQL, bazy danych MongoDB, usługi Azure Table Storage, bazy danych Amazon DynamoDB, a nawet z kolekcji interfejsu API SQL usługi Azure Cosmos DB. Narzędzie do migracji danych może być również używane podczas migracji z kolekcji z pojedynczą partycją do kolekcji z wieloma partycjami na potrzeby interfejsu SQL API.

Aby uzyskać więcej informacji, zobacz:

- [Narzędzie do migracji danych usługi Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/import-data)

<!-- markdownlint-disable MD025 -->

# <a name="third-party-migration-tools"></a>[Narzędzia migracji innych firm](#tab/third-party-tools)

Niektóre narzędzia migracji innych firm i usługi niezależnych dostawców oprogramowania mogą pomóc w procesie migracji. Wszystkie oferują różne korzyści i zalety. Do tych narzędzi należą:

## <a name="unifycloud"></a>UnifyCloud

UnifyCloud to usługa niezależnego dostawcy oprogramowania, która zapewnia narzędzia do automatyzowania oceny, migracji i modernizacji.

[Dowiedz się więcej](https://www.unifycloud.com)

## <a name="cloudamize"></a>Cloudamize

Cloudamize to usługa niezależnego dostawcy oprogramowania, która obejmuje wszystkie fazy strategii migracji.

[Dowiedz się więcej](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto zapewnia replikację wirtualną obsługującą zarówno środowisko Microsoft Hyper-V, jak i VMware vSphere.

[Dowiedz się więcej](https://www.zerto.com/modernize)

## <a name="carbonite"></a>Carbonite

Usługa Carbonite zapewnia rozwiązania do migracji serwerów i danych umożliwiające migrowanie obciążeń do środowiska fizycznego, wirtualnego lub chmurowego, z takich środowisk lub pomiędzy nimi.

[Dowiedz się więcej](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere jest rozwiązaniem do odnajdywania, które zapewnia dane i szczegółowe informacje potrzebne do zaplanowania migracji do chmury oraz ciągłego i niezawodnego optymalizowania, monitorowania i analizowania środowisk informatycznych.

[Dowiedz się więcej](https://www.movere.io)

## <a name="azure-cosmos-db-partners"></a>Partnerzy usługi Azure Cosmos DB

Do obsługi migracji w usłudze Azure Cosmos DB dla baz danych NoSQL można wybrać opcje spośród wielu dostępnych narzędzi i doświadczonych partnerów zajmujących się integracją systemów.

[Dowiedz się więcej](https://docs.microsoft.com/azure/cosmos-db/partners-migration-cosmosdb#migration-tools)

Odwiedź [Centrum migracji platformy Azure](https://azure.microsoft.com/migration/support), aby odnaleźć organizacje oferujące gotowe do użycia technologiczne rozwiązania partnerskie odpowiednie do swoich scenariuszy migracji i dowiedzieć się więcej na temat dodatkowych narzędzi migracji innych firm oraz usług pomocy technicznej.

W [przewodniku po migracji bazy danych na platformę Azure](https://datamigration.microsoft.com) przedstawiono szereg opcji i szczegółowych wskazówek dotyczących migracji przy użyciu rozwiązań natywnych i partnerskich.

# <a name="project-management-tools"></a>[Narzędzia do zarządzania projektami](#tab/project-management-tools)

Jeśli projekty nie są śledzone i zarządzane, istnieje większe prawdopodobieństwo wystąpienia problemów. Uważamy, że aby osiągnąć zamierzony cel, należy korzystać z narzędzia do zarządzania projektami. Dostępnych jest wiele różnych narzędzi i menedżerowie projektów w organizacji mogą już mieć swoje ulubione.

Sugerowanym narzędziem do zarządzania projektami podczas migracji do chmury jest usługa Azure DevOps. Aby przyspieszyć korzystanie z usługi Azure DevOps, przewodnik Cloud Adoption Framework obejmuje narzędzie do automatycznego wdrażania szablonu projektu. Ten szablon obejmuje zadania często wykonywane podczas pracy związanej z migracją. Wdróż ten szablon przy użyciu [tych instrukcji](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/template). Następnie możesz zmodyfikować ten szablon w celu odzwierciedlenia [obciążeń](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/workloads) i [zasobów](https://docs.microsoft.com/azure/architecture/cloud-adoption/plan/assets) do zmigrowania.

Firma Microsoft oferuje też następujące narzędzia do zarządzania projektami, które mogą ze sobą współdziałać, aby zapewnić szersze możliwości:

- [Microsoft Planner](https://tasks.office.com): prosta, wizualna metoda organizowania pracy zespołowej.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): zarządzanie projektami i portfolio, zarządzanie zdolnościami produkcyjnymi zasobów, zarządzanie finansami, zarządzanie grafikiem i harmonogramem.
- [Microsoft Teams](https://products.office.com/microsoft-teams): narzędzie do współpracy i komunikacji zespołowej. Rozwiązanie Teams można również zintegrować z narzędziem Planner oraz innymi narzędziami, aby ułatwić współpracę.
- [Azure DevOps Services](https://azure.microsoft.com/services/devops): do korzystania z usługi Azure DevOps nie jest wymagany szablon planowania przewodnika Cloud Adoption Framework. Usługi można używać bez tego szablonu, aby zarządzać infrastrukturą jak kodem lub używać elementów roboczych i tablic do zarządzania projektami. Z czasem Twoja organizacja może skorzystać z funkcji ciągłej integracji/ciągłego wdrażania.

Nie są to jedyne dostępne narzędzia. Wiele innych narzędzi innych firm jest szeroko używanych w społeczności zajmującej się zarządzaniem projektami.

## <a name="set-up-for-devops"></a>Przygotowanie do zastosowania metodyki DevOps

Migracja do technologii chmurowych stanowi świetną okazję do przygotowania organizacji do wprowadzenia metodyki DevOps i ciągłej integracji/ciągłego wdrażania. Nawet jeśli Twoja organizacja zarządza tylko infrastrukturą, gdy zaczniesz zarządzać infrastrukturą jak kodem i korzystać z wzorców i praktyk branżowych metodyki DevOps, możesz rozpocząć zwiększanie elastyczności za pomocą potoków ciągłej integracji/ciągłego wdrażania, co pozwoli na szybsze dostosowanie do scenariuszy zmiany, rozwoju, wydania, a nawet odzyskiwania.

Usługa Azure DevOps zapewnia wszystkie wymagane funkcje i integrację z platformą Azure, środowiskami lokalnymi, a nawet z innymi chmurami. Aby uzyskać więcej informacji, zobacz [usługę Azure DevOps](https://azure.microsoft.com/services/devops). Aby uzyskać dostęp do szkolenia z przewodnikiem, zobacz [CI/CD with Azure DevOps — Quickstart (Ciągła integracja/ciągłe wdrażanie w usłudze Azure DevOps — Szybki start)](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

## <a name="suggested-skills"></a>Sugerowane umiejętności

Microsoft Learn to nowe podejście do uczenia się. Gotowość do nowych obowiązków związanych z umiejętnościami, które dotyczą wdrażania chmury, nie przychodzi łatwo. Microsoft Learn oferuje bardziej satysfakcjonującą metodę praktycznego uczenia się, która ułatwia szybsze osiąganie celów. Zdobywaj punkty i poziomy i osiągaj więcej.

Poniżej znajduje się przykład dostosowanej ścieżki szkoleniowej w środowisku Microsoft Learn, która uzupełnia wytyczne konfigurowania pod kątem metodyki DevOps w strukturze Cloud Adoption Framework.

[Tworzenie aplikacji za pomocą usługi Azure DevOps](https://docs.microsoft.com/learn/paths/build-applications-with-azure-devops): Współpracuj z innymi osobami w celu tworzenia aplikacji przy użyciu usług Azure Pipelines i GitHub. Uruchamiaj testy automatyczne w potoku, aby weryfikować jakość kodu. Skanuj kod źródłowy i składniki innych firm pod kątem potencjalnych luk w zabezpieczeniach. Definiuj wiele potoków, które współpracują ze sobą w celu skompilowania aplikacji. Kompiluj aplikacje przy użyciu zarówno agentów hostowanych przez firmę Microsoft, jak i własnych agentów kompilacji.

# <a name="cost-management"></a>[Zarządzanie kosztami](#tab/ManageCost)

Podczas migrowania zasobów do środowiska chmury należy przeprowadzać okresową analizę kosztów. Pomoże to uniknąć nieoczekiwanych opłat za użycie, ponieważ proces migracji może spowodować, że Twoje usługi zostaną objęte dodatkowymi wymaganiami w zakresie użycia. Można również zmienić rozmiar zasobów w zależności od potrzeb, aby zrównoważyć koszt i obciążenie, co zostało omówione bardziej szczegółowo w sekcji [Optymalizowanie i przekształcanie](./optimize-and-transform.md).
