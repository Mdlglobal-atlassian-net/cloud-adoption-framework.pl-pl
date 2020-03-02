---
title: Przyspiesz migrację, migrując wystąpienie SQL Server
description: Migrowanie całych wystąpień SQL Server może przyspieszyć migrację obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: c41a8ebbce9fa4a8f0036c2aa395706f44069263
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78225498"
---
# <a name="accelerate-migration-by-migrating-multiple-databases-or-entire-sql-servers"></a>Przyspieszanie migracji przez Migrowanie wielu baz danych lub całych serwerów SQL

Migrowanie całych wystąpień SQL Server może przyspieszyć migrację obciążeń. Poniższe wskazówki rozszerzają zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) przez Migrowanie wystąpienia SQL Server poza nakładem pracy związanym z migracją obciążenia. Takie podejście umożliwia przepełnienie migracji wielu obciążeń przy użyciu jednej migracji platformy danych. Większość wysiłku wymaganego do rozwinięcia tego zakresu występuje w procesach wymagań wstępnych, oceny, migracji i optymalizacji.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Czy ten rozszerzony zakres jest dla Ciebie prawidłowy?

Rozwiązanie zalecane w [przewodniku migracji platformy Azure](../azure-migration-guide/index.md) polega na migracji każdej struktury danych wraz ze skojarzonymi obciążeniami w ramach jednego wysiłku migracji. Iteracyjne podejście do migracji ogranicza proces odnajdywania, oceny i inne zadania, które mogą tworzyć blokowanie i powolne zwraca wartość biznesową.

Niektóre struktury danych mogą jednak być migrowane bardziej wydajnie za pomocą oddzielnej migracji na platformę danych. Poniżej przedstawiono kilka przykładów:

- **Koniec usługi:** Szybkie przenoszenie wystąpienia SQL Server jako izolowanej iteracji w ramach większego nakładu pracy migracji może zapobiec wyzwaniom w zakresie końca usługi. Ten przewodnik pomoże zintegrować migrację SQL Server w szerszym procesie migracji. Jeśli jednak migrujesz/uaktualniasz SQL Server niezależnie od innych nakładów związanych z wdrażaniem w chmurze, [informacje na temat SQL Server końca okresu użytkowania](/sql/sql-server/end-of-support/sql-server-end-of-life-overview) lub dokumentacji dotyczącej [migracji SQL Server](/sql/sql-server/migrate/index) mogą zapewnić wyraźniejsze wskazówki.
- **SQL Server Services:** Struktura danych jest częścią szerszego rozwiązania, które wymaga SQL Server uruchomionego na maszynie wirtualnej. Jest to typowe rozwiązanie, które korzysta z usług SQL Server, takich jak SQL Server Reporting Services, SQL Server Integration Services lub SQL Server Analysis Services.
- **Bazy danych o wysokiej gęstości i niskim użyciu:** Wystąpienie SQL Server ma wysoką gęstość baz danych. Każda z tych baz danych ma niskie ilości transakcji i wymaga niewiele w przypadku zasobów obliczeniowych. Należy rozważyć inne, bardziej nowoczesne rozwiązania, ale podejście infrastruktury jako usługi (IaaS) może skutkować znacznie mniejszym kosztem działania.
- **Łączny koszt posiadania:** Jeśli ma to zastosowanie, możesz zastosować [korzyści użycia hybrydowego platformy Azure](https://azure.microsoft.com/pricing/hybrid-benefit) na liście cenowej tworzącej najniższy koszt posiadania dla wystąpień SQL Server. Jest to szczególnie powszechne w przypadku klientów, którzy obsługują SQL Server w scenariuszach wielochmurowych.
- **Akcelerator migracji:** Migracja wystąpienia SQL Server może przenosić kilka baz danych w jednej iteracji. Takie podejście czasami umożliwia późniejsze skoncentrowanie się na aplikacjach i maszynach wirtualnych, co oznacza, że można migrować więcej obciążeń w jednej iteracji.
- **Migracja oprogramowania VMware:** Wspólna architektura lokalna obejmuje aplikacje i maszyny wirtualne na hoście wirtualnym oraz bazy danych na komputerze bez systemu operacyjnego. W tym scenariuszu można migrować całe wystąpienia SQL Server w celu obsługi migracji hosta VMware do usługi Azure VMware. Aby uzyskać więcej informacji, zobacz [migracja hosta VMware](./vmware-host.md).

Jeśli żadne z powyższych kryteriów nie mają zastosowania do tej migracji, najlepszym rozwiązaniem może być kontynuowanie [standardowego procesu migracji](../index.md). W procesie standardowym struktury danych są migrowane iteracyjnie wraz z każdym obciążeniem.

Jeśli ten przewodnik jest zgodny z kryteriami, przejdź do tego rozszerzonego przewodnika dotyczącego zakresu jako nakładu pracy w ramach [standardowego procesu migracji](../index.md). W fazie wymagań wstępnych można zintegrować ten nakład pracy z ogólnym planem wdrażania.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Przed przeprowadzeniem migracji SQL Server Rozpocznij od rozwinięcia cyfrowej sieci, dołączając do niej dane. W obszarze danych rejestruje się spis zasobów danych, które są rozważane do migracji. W poniższych tabelach przedstawiono podejście do rejestrowania danych.

### <a name="server-inventory"></a>Spis serwerów

Poniżej znajduje się przykład spisu serwerów:

|SQL Server|Przeznaczenie|Wersja|[Zagrożenia](../../manage/considerations/criticality.md)|[Czułości](../../govern/policy-compliance/data-classification.md)|Liczba baz danych|SSIS|SSRS|SSAS|Klaster|Liczba węzłów|
|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL — 01|Aplikacje podstawowe|2016|Operacje krytyczne dla działalności firmy|Wysoce poufne|40|N/D|N/D|N/D|Tak|3|
|SQL — 02|Aplikacje podstawowe|2016|Operacje krytyczne dla działalności firmy|Wysoce poufne|40|N/D|N/D|N/D|Tak|3|
|SQL — 03|Aplikacje podstawowe|2016|Operacje krytyczne dla działalności firmy|Wysoce poufne|40|N/D|N/D|N/D|Tak|3|
|SQL — 04|BI|2012|Wysoki|XX|6|N/D|Poufne|Tak — moduł wielowymiarowy|Nie|1|
|SQL – 05|Integracja|2008 R2|Niski|Ogólne|20|Tak|N/D|N/D|Nie|1|

### <a name="database-inventory"></a>Spis bazy danych

Poniżej znajduje się przykład spisu bazy danych dla jednego z powyższych serwerów:

|Serwer|Baza danych|[Zagrożenia](../../manage/considerations/criticality.md)|[Czułości](../../govern/policy-compliance/data-classification.md)|Wyniki Data Migration Assistant (DMA)|Korygowanie DMA|Platforma docelowa|
|---------|---------|---------|---------|---------|---------|---------|
|SQL — 01|BAZA DANYCH — 1|Operacje krytyczne dla działalności firmy|Wysoce poufne|Zgodność|N/D|Azure SQL Database|
|SQL — 01|BAZA DANYCH — 2|Wysoki|Poufne|Wymagana zmiana schematu|Zaimplementowane zmiany|Azure SQL Database|
|SQL — 01|BAZA DANYCH — 3|Wysoki|Ogólne|Zgodność|N/D|Wystąpienie zarządzane Azure SQL|
|SQL — 01|BAZA DANYCH 4|Niski|Wysoce poufne|Wymagana zmiana schematu|Zmiany zaplanowane|Wystąpienie zarządzane Azure SQL|
|SQL — 01|BAZA DANYCH 5|Operacje krytyczne dla działalności firmy|Ogólne|Zgodność|N/D|Wystąpienie zarządzane Azure SQL|
|SQL — 01|DB-6|Wysoki|Poufne|Zgodność|N/D|Azure SQL Database|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integracja z planem wdrażania chmury

Po zakończeniu tego procesu odnajdywania można go uwzględnić w [planie wdrożenia chmury](../../plan/template.md). W ramach planu wdrażania chmury Dodaj każde wystąpienie SQL Server, które ma zostać zmigrowane jako [odrębne obciążenie](../../plan/workloads.md). W ramach każdego obciążenia bazy danych i usługi (SSIS, SSAS, SSRS) mogą być dodawane jako [zasoby](../../plan/workloads.md). Aby dodać obciążenia i zasoby zbiorczo do planu wdrożenia, zobacz [Dodawanie i edytowanie elementów roboczych w programie Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Po dołączeniu obciążeń i zasobów do planu i zespół może kontynuować proces migracji standardowej przy użyciu planu wdrażania. Gdy zespół adopcji przejdzie do procesu oceny, migracji i optymalizacji, współczynnik zmian omówionych w poniższych sekcjach.

## <a name="assessment-process-changes"></a>Zmiany procesu oceny

Jeśli dowolna baza danych w planie można migrować do platformy danych platformy jako usługi (PaaS), Użyj usługi DMA, aby oszacować zgodność wybranej bazy danych. Gdy baza danych wymaga konwersji schematu, należy wykonać te konwersje w ramach procesu oceny, aby uniknąć przerw w potoku migracji.

### <a name="suggested-action-during-the-assessment-process"></a>Sugerowana akcja w trakcie procesu oceny

W przypadku baz danych, które można migrować do rozwiązania PaaS, podczas procesu oceny są wykonywane następujące akcje:

- **Ocenianie za pomocą DMA:** Użyj Data Migration Assistant, aby wykrywać problemy ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych w docelowym Azure SQL Database wystąpieniu zarządzanym. Użyj usługi DMA, aby zalecać ulepszenia wydajności i niezawodności oraz przenieść schemat, dane i niezawarte obiekty z serwera źródłowego na serwer docelowy. Aby uzyskać więcej informacji, zobacz [Data Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview).
- **Koryguj i Konwertuj:** Na podstawie danych wyjściowych DMA przekonwertuj schemat danych źródłowych, aby skorygować problemy ze zgodnością. Przetestuj przekonwertowany schemat danych za pomocą aplikacji zależnych.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas migracji można wybrać spośród wielu różnych narzędzi i metod. Jednak każde podejście odbywa się w prostym procesie: Migruj schemat, dane i obiekty. Następnie zsynchronizuj dane z docelowym źródłem danych.

Celem i źródłem struktury i usług danych może być to, że te dwa etapy raczej nie są skomplikowane. Poniższe sekcje ułatwiają zrozumienie najlepszych narzędzi do wyboru w oparciu o decyzje dotyczące migracji.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

Sugerowana ścieżka migracji i synchronizacji używa kombinacji następujących trzech narzędzi. W poniższych sekcjach przedstawiono bardziej złożone opcje migracji i synchronizacji, które umożliwiają szeroką gamę rozwiązań docelowych i źródłowych.

|Opcja migracji|Przeznaczenie|
|---------|---------|
|[Azure Database Migration Service](https://docs.microsoft.com/sql/dma/dma-overview)|Obsługuje w trybie online (minimalne przestoje) i w trybie offline (jednorazowe) migracje na dużą skalę do Azure SQL Database wystąpienia zarządzanego. Obsługuje migrację z: SQL Server 2005, SQL Server 2008 i SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 i SQL Server 2017.|
|[Replikacja transakcyjna](https://docs.microsoft.com/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Replikacja transakcyjna do Azure SQL Databaseego wystąpienia zarządzanego jest obsługiwana w przypadku migracji z programu: SQL Server 2012 (SP2 CU8, SP3 lub nowszego), SQL Server 2014 (RTM CU10 lub nowszych, lub z dodatkiem SP1 CU3 lub nowszym), SQL Server 2016, SQL Server 2017.|
|[Ładowanie zbiorcze](https://docs.microsoft.com/sql/t-sql/statements/bulk-insert-transact-sql)|Użyj ładowania zbiorczego do Azure SQL Database wystąpienia zarządzanego dla danych przechowywanych w: SQL Server 2005, SQL Server 2008 i SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 i SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Wskazówki i samouczki dotyczące sugerowanego procesu migracji

Wybór najlepszej wskazówki dotyczącej migracji przy użyciu Azure Database Migration Service jest uzależniony od wybranej platformy źródłowej i docelowej. Poniższa tabela zawiera linki do samouczków dla każdego standardowego podejścia do migracji bazy danych SQL przy użyciu Azure Database Migration Service.

|Element źródłowy  |Środowisko docelowe  |Narzędzie  |Typ migracji  |Wskazówki  |
|---------|---------|---------|---------|---------|
|SQL Server|Azure SQL Database|Database Migration Service|Taśma|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|SQL Server|Azure SQL Database|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|Database Migration Service|Taśma|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server RDS|Azure SQL Database (lub wystąpienie zarządzane)|Database Migration Service|Sieci|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Wskazówki i samouczki dotyczące różnych usług do równoważnych rozwiązań PaaS

Po przeniesieniu baz danych z wystąpienia SQL Server do Azure Database Migration Service, schemat i dane mogą być hostowane w wielu rozwiązaniach PaaS. Jednak inne wymagane usługi mogą nadal działać na tym serwerze. Poniższe trzy samouczki ułatwiają przechodzenie usług SSIS, SSAS i SSRS do równoważnych usługi PaaS na platformie Azure.

|Element źródłowy  |Środowisko docelowe  |Narzędzie  |Typ migracji  |Wskazówki  |
|---------|---------|---------|---------|---------|
|SQL Server Integration Services|Azure Data Factory Integration Runtime|Azure Data Factory|Taśma|[Samouczek](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Services — Model tabelaryczny|Azure Analysis Services|SQL Server Data Tools|Taśma|[Samouczek](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|SQL Server Reporting Services|Serwer raportów usługi Power BI|Power BI|Taśma|[Samouczek](https://docs.microsoft.com/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Wskazówki i samouczki dotyczące migracji z SQL Server do wystąpienia IaaS SQL Server

Po przeprowadzeniu migracji baz danych i usług do wystąpień PaaS nadal mogą istnieć struktury i usługi danych, które nie są zgodne z PaaS. Gdy istniejące ograniczenia uniemożliwiają Migrowanie struktur lub usług danych, poniższy samouczek ułatwia Migrowanie różnych zasobów w portfolio danych do rozwiązań IaaS platformy Azure.

To podejście służy do migrowania baz danych lub innych usług w wystąpieniu SQL Server.

|Element źródłowy  |Środowisko docelowe  |Narzędzie  |Typ migracji  |Wskazówki  |
|---------|---------|---------|---------|---------|
|SQL Server pojedynczego wystąpienia|SQL Server w IaaS|Różnych|Taśma|[Samouczek](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Zmiany procesu optymalizacji

Podczas optymalizacji można testować, optymalizować i awansować do produkcji każdej struktury danych, usługi lub SQL Server wystąpienia. Jest to największy wpływ na odchylenie od modelu migracji dla obciążenia.

W idealnym przypadku można migrować zależne obciążenia, aplikacje i maszyny wirtualne w ramach tej samej iteracji co wystąpienie SQL Server. W przypadku wystąpienia tego idealnego scenariusza można testować obciążenie wraz ze źródłem danych. Po przetestowaniu można podwyższyć poziom struktury danych do produkcji i zakończyć proces synchronizacji.

Teraz Rozważmy scenariusz, w którym istnieje znaczący odstęp czasu między migracją bazy danych i migracją obciążeń. Niestety, może to być największą zmianę w procesie optymalizacji podczas migracji, która nie jest zależna od obciążenia. W przypadku migrowania wielu baz danych w ramach migracji SQL Server te bazy danych mogą współistnieć zarówno w chmurze, jak i lokalnie, w przypadku wielu iteracji. W tym czasie musisz zachować synchronizację danych do momentu migracji, przetestowania i promowania zasobów zależnych.

Do czasu promowania wszystkich obciążeń zależnych ty i Twój zespół jest odpowiedzialny za obsługę synchronizacji danych z systemu źródłowego do systemu docelowego. Ta synchronizacja wykorzystuje przepustowość sieci, koszty chmury i najważniejsze godziny pracy. Odpowiednie wyrównanie planu wdrożenia w ramach obciążenia SQL Server migracji oraz wszystkich zależnych obciążeń i aplikacji może obniżyć koszty.

### <a name="suggested-action-during-the-optimization-process"></a>Sugerowana akcja w procesie optymalizacji

Podczas procesów optymalizacji wykonaj następujące zadania dla każdej iteracji, aż wszystkie struktury i usługi danych zostały podwyższone do środowiska produkcyjnego.

1. Sprawdź poprawność synchronizacji danych.
2. Przetestuj wszystkie zmigrowane aplikacje.
3. Zoptymalizuj strukturę aplikacji i danych w celu dostrojenia kosztów.
4. Podnieś poziom aplikacji do środowiska produkcyjnego.
5. Testowanie ciągłego ruchu lokalnego z lokalną bazą danych.
6. Przerwij synchronizację wszelkich danych podniesionych do środowiska produkcyjnego.
7. Przerwij oryginalną źródłową bazę danych.

Do momentu przekroczenia kroku 5 nie można przerwać baz danych i synchronizacji. Dopóki wszystkie bazy danych w wystąpieniu SQL Server przeprowadziły przez wszystkie siedem kroków, należy traktować lokalne wystąpienie SQL Server jako produkcyjne. Należy zachować całą synchronizację.

## <a name="next-steps"></a>Następne kroki

Wróć do [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md), aby upewnić się, że metoda migracji jest w pełni dopasowana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
