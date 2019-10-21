---
title: Przyspieszanie migracji przy użyciu migracji SQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przyspieszanie migracji przy użyciu migracji SQL
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4af94af91874ac666f45a917eed003b3cf881c51
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558222"
---
# <a name="accelerate-migration-with-a-sql-migration"></a>Przyspieszanie migracji przy użyciu migracji SQL

Migrowanie całych wystąpień SQL Server może przyspieszyć migrację obciążeń. Poniższe wskazówki pomogą rozszerzyć zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) przez migrowanie SQL Server poza nakładem pracy związanym z migracją obciążenia. Takie podejście umożliwia przepełnienie migracji wielu obciążeń przy użyciu jednej migracji platformy danych.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Większość wysiłku wymaganego do rozwinięcia tego zakresu będzie miała miejsce w procesie wymagań wstępnych, oceny, migracji i optymalizacji.

<!-- markdownlint-disable MD026 -->

## <a name="is-this-expanded-scope-right-for-you"></a>Czy ten rozszerzony zakres jest dla Ciebie prawidłowy?

Zalecanym podejściem opisanym w [przewodniku migracji platformy Azure](../azure-migration-guide/index.md) jest Migrowanie każdej struktury danych obok skojarzonych obciążeń w ramach jednego wysiłku migracji. Iteracyjne podejście do migracji ogranicza proces odnajdywania, oceny i inne zadania, które mogą tworzyć blokowanie i powolne zwraca wartość biznesową.

Niektóre struktury danych mogą jednak być migrowane bardziej wydajnie za pomocą oddzielnej migracji na platformę danych. Poniżej przedstawiono kilka przykładów, które mogą prowadzić do korzystania z tych rozszerzonych wskazówek dotyczących zakresu:

- **Koniec usługi:** Szybkie przenoszenie wystąpienia SQL Server, aby uniknąć problemów z końcowym użyciem usługi, można uzasadnić korzystanie z tego przewodnika poza standardowymi wysiłkami migracji.
- **SQL Server Services:** Struktura danych jest częścią szerszego rozwiązania, które wymaga SQL Server uruchomionego na maszynie wirtualnej. Jest to typowe rozwiązanie, które wykorzystuje SQL Server usług, takich jak SQL Server Reporting Services, SQL Server Integration Services lub SQL Server Analysis Services.
- **Bazy danych o wysokiej gęstości i niskim użyciu:** SQL Server ma wysoką gęstość baz danych. Każda z tych baz danych ma niskie ilości transakcji i wymaga niewielkich zasobów obliczeniowych. Należy wziąć pod uwagę inne nowoczesne rozwiązania, ale podejście IaaS może skutkować znacznie mniejszym kosztem działania.
- **Łączny koszt posiadania:** Jeśli ma to zastosowanie, korzyści z używania [hybrydowej platformy Azure](https://azure.microsoft.com/pricing/hybrid-benefit) można zastosować do cennika, który tworzy najniższy koszt posiadania serwerów SQL. Jest to szczególnie powszechne w przypadku klientów, którzy obsługują SQL Server w scenariuszach wielochmurowych.
- **Akcelerator migracji:** Migracja i przesunięcia wystąpienia SQL Server mogą przenosić kilka baz danych w jednej iteracji. Takie podejście czasami umożliwia późniejsze skoncentrowanie się na aplikacjach i maszynach wirtualnych, co pozwala na przeprowadzenie migracji większej liczby obciążeń w jednej iteracji.
- **Migracja oprogramowania VMware:** Wspólna architektura lokalna obejmuje aplikacje i maszyny wirtualne na hoście wirtualnym i bazach danych na komputerze bez systemu operacyjnego. Podczas migrowania tej wspólnej architektury migracja hosta VMWare do usługi Azure VMWare Service (Automatyczna synchronizacja) może być poprowadzona w tym przewodniku w celu przeprowadzenia migracji całych wystąpień SQL Server w celu obsługi tych hostów wirtualnych. Aby uzyskać uzupełniające wskazówki, zobacz [migracja hosta VMware](./vmware-host.md).

Jeśli żadne z powyższych kryteriów nie mają zastosowania do tej migracji, najlepszym rozwiązaniem może być kontynuowanie [standardowego procesu migracji](../index.md). W procesie standardowym struktury danych są migrowane iteracyjnie wraz z każdym obciążeniem.

Jeśli ten przewodnik jest zgodny z kryteriami, przejdź do tego rozszerzonego przewodnika dotyczącego zakresu jako nakładu pracy w ramach [standardowego procesu migracji](../index.md). W fazie wymagań wstępnych nakład pracy można zintegrować z ogólnym planem wdrażania.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Przed przeprowadzeniem migracji SQL Server Rozpocznij od rozwinięcia **cyfrowej** sieci, dołączając do niej dane. W obszarze danych rejestruje się spis zasobów danych, które są brane pod uwagę podczas migracji. W poniższych tabelach przedstawiono podejście do rejestrowania danych.

### <a name="server-inventory"></a>Spis serwerów

Poniżej znajduje się przykład spisu serwerów dla serwerów SQL:

|Oprogramowanie SQL Server|Przeznaczenie|Wersja|[Zagrożenia](../../manage/considerations/criticality.md)|[Czułości](../../govern/policy-compliance/data-classification.md)|Liczba baz danych|SSIS|USŁUG|SSAS|Klaster|Liczba węzłów|
|---------|---------|---------|---------|---------|---------|---------|---------|
|SQL — 01|Aplikacje podstawowe|2016|Krytyczne znaczenie dla działalności|Wysoce poufne|40|ND|ND|ND|Tak|3|
|SQL — 02|Aplikacje podstawowe|2016|Krytyczne znaczenie dla działalności|Wysoce poufne|40|ND|ND|ND|Tak|3|
|SQL — 03|Aplikacje podstawowe|2016|Krytyczne znaczenie dla działalności|Wysoce poufne|40|ND|ND|ND|Tak|3|
|SQL — 04|BI|2012|Wysoka|XX|6|ND|Mając|Tak — moduł wielowymiarowy|Nie|1|
|SQL – 05|Integracja|2008 R2|Niska|Ogólne|20|Tak|ND|ND|Nie|1|

### <a name="database-inventory"></a>Spis bazy danych

Poniżej znajduje się przykład spisu bazy danych dla jednego z powyższych serwerów SQL:

|Serwer|Database (Baza danych)|[Zagrożenia](../../manage/considerations/criticality.md)|[Czułości](../../govern/policy-compliance/data-classification.md)|Wyniki DMA|Korygowanie DMA|Platforma docelowa|
|---------|---------|---------|---------|---------|---------|---------|
|SQL — 01|BAZA DANYCH — 1|Krytyczne znaczenie dla działalności|Wysoce poufne|Zgodność|ND|Azure SQL Database|
|SQL — 01|BAZA DANYCH — 2|Wysoka|Mając|Wymagana zmiana schematu|Zaimplementowane zmiany|Azure SQL Database|
|SQL — 01|BAZA DANYCH — 1|Wysoka|Ogólne|Zgodność|ND|Wystąpienie zarządzane Azure SQL|
|SQL — 01|BAZA DANYCH — 1|Niska|Wysoce poufne|Wymagana zmiana schematu|Zmiany zaplanowane|Wystąpienie zarządzane Azure SQL|
|SQL — 01|BAZA DANYCH — 1|Krytyczne znaczenie dla działalności|Ogólne|Zgodność|ND|Wystąpienie zarządzane Azure SQL|
|SQL — 01|BAZA DANYCH — 2|Wysoka|Mając|Zgodność|ND|Azure SQL Database|

### <a name="integration-with-the-cloud-adoption-plan"></a>Integracja z planem wdrażania chmury

Po zakończeniu odnajdywania plan może zostać uwzględniony w [planie wdrożenia chmury](../../plan/template.md). W ramach planu wdrażania chmury Dodaj każde wystąpienie SQL Server, które ma zostać zmigrowane jako [odrębne obciążenie](../../plan/workloads.md). W ramach każdego obciążenia bazy danych i usługi (SSIS, SSAS, SSRS) mogą być dodawane jako [zasoby](../../plan/workloads.md). Aby dodać obciążenia i zasoby zbiorczo do planu wdrożenia, zobacz [Dodawanie i edytowanie elementów roboczych w programie Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Po dołączeniu obciążeń i zasobów do planu zespół może kontynuować proces migracji standardowej przy użyciu planu wdrożenia, aby zaplanować wysiłki. Gdy zespół adopcji przejdzie do oceny, migracji i procesów optymalizacji, należy wziąć pod uwagę następujące zmiany.

## <a name="assessment-process-changes"></a>Zmiany procesu oceny

Jeśli dowolna baza danych w planie można migrować do platformy danych platformy jako usługi (PaaS), użyj Data Migration Assistant, aby oszacować zgodność wybranej bazy danych. Gdy baza danych wymaga konwersji schematu, zaleca się, aby te konwersje zostały wykonane w ramach procesu oceny, aby uniknąć przerw w potoku migracji.

### <a name="suggested-action-during-the-assessment-process"></a>Sugerowana akcja w trakcie procesu oceny

W przypadku baz danych, które można migrować do rozwiązania PaaS, w trakcie procesu oceny zostaną wykonane następujące działania.

- **Oceń przy użyciu Data Migration Assistant:** Za pomocą Data Migration Assistant Wykrywaj problemy ze zgodnością, które mogą mieć wpływ na funkcjonalność bazy danych w docelowym Azure SQL Database wystąpieniu zarządzanym, aby zalecać ulepszenia wydajności i niezawodności oraz przenosić schemat, dane i niezawarte obiekty z serwera źródłowego na serwer docelowy. Aby uzyskać więcej informacji, zobacz [Data Migration Assistant](/sql/dma/dma-overview).
- **Koryguj i Konwertuj:** Na podstawie danych wyjściowych Data Migration Assistant Konwertuj schemat danych źródłowych, aby skorygować problemy ze zgodnością. Przetestuj przekonwertowany schemat danych za pomocą aplikacji zależnych.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas migracji istnieje wiele narzędzi i opcji podejścia. Jednak każde podejście odbywa się w prostym procesie: Migruj schemat, dane i obiekty. Synchronizuj dane z docelowym źródłem danych.

Celem i źródłem struktury i usług danych może być to, że te dwa etapy raczej nie są skomplikowane. Zapoznaj się z każdą z poniższych sekcji, aby poznać najlepsze wybór narzędzi w oparciu o decyzje dotyczące migracji.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

Sugerowana ścieżka migracji i synchronizacji używa kombinacji następujących trzech narzędzi. W poniższych sekcjach przedstawiono bardziej złożone opcje migracji i synchronizacji, które umożliwiają szeroką gamę rozwiązań docelowych i źródłowych.

|Opcja migracji|Przeznaczenie|
|---------|---------|
|[Azure Database Migration Service](/sql/dma/dma-overview)|Usługa Azure DMS obsługuje w trybie online (minimalne przestoje) i offline (jednorazowo) migracje na dużą skalę do Azure SQL Database wystąpienia zarządzanego z SQL Server 2005, SQL Server 2008 i SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 i SQL Server 2017.|
|[Replikacja transakcyjna](/sql/relational-databases/replication/administration/enhance-transactional-replication-performance)|Replikacja transakcyjna do Azure SQL Databaseego wystąpienia zarządzanego jest obsługiwana w przypadku migracji z programu: SQL Server 2012 (SP2 CU8, SP3 lub nowszego), SQL Server 2014 (RTM CU10 lub nowszych lub z dodatkiem SP1 CU3 lub nowszym), SQL Server 2016, SQL Server 2017|
|[Ładowanie zbiorcze](/sql/t-sql/statements/bulk-insert-transact-sql)|Użyj ładowania zbiorczego do Azure SQL Database wystąpienia zarządzanego dla danych przechowywanych w SQL Server 2005, SQL Server 2008 i SQL Server 2008 R2, SQL Server 2012, SQL Server 2014, SQL Server 2016 i SQL Server 2017.|

### <a name="guidance-and-tutorials-for-suggested-migration-process"></a>Wskazówki i samouczki dotyczące sugerowanego procesu migracji

Wybór najlepszej wskazówki dotyczącej migracji za pomocą usługi DMS jest uzależniony od wybranej platformy źródłowej i docelowej. W poniższej tabeli przedstawiono samouczki dla każdego standardowego podejścia do migracji bazy danych SQL przy użyciu usługi DMS.

|Źródło  |Cel  |Narzędzie  |Typ migracji  |Wskazówka  |
|---------|---------|---------|---------|---------|
|Oprogramowanie SQL Server|Azure SQL Database|DMS|Stanie|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-azure-sql)|
|Oprogramowanie SQL Server|Azure SQL Database|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-azure-sql-online)|
|Oprogramowanie SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|DMS|Stanie|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)|
|Oprogramowanie SQL Server|Wystąpienie zarządzane usługi Azure SQL Database|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)|
|SQL Server RDS|Azure SQL Database (lub wystąpienie zarządzane)|DMS|Online|[Samouczek](https://docs.microsoft.com/azure/dms/tutorial-rds-sql-server-azure-sql-and-managed-instance-online)|

### <a name="guidance-and-tutorials-for-various-services-to-equivalent-paas-solutions"></a>Wskazówki i samouczki dotyczące różnych usług do równoważnych rozwiązań PaaS

Po przeniesieniu baz danych z programu SQL Server do usługi DMS schemat i dane mogą być hostowane w wielu rozwiązaniach PaaS. Jednak inne wymagane usługi mogą nadal działać na tym serwerze. Poniższe trzy samouczki będą pomocne w przenoszeniu usług SSIS, SSAS i SSRS do usługi PaaS na platformie Azure.

|Źródło  |Cel  |Narzędzie  |Typ migracji  |Wskazówka  |
|---------|---------|---------|---------|---------|
|SQL Server usługi integracji|Data Factory Integration Runtime|Azure Data Factory|Stanie|[Samouczek](https://docs.microsoft.com/azure/data-factory/create-azure-ssis-integration-runtime)|
|SQL Server Analysis Service — Model tabelaryczny|Usługa Azure Analysis Service|SSDT|Stanie|[Samouczek](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)|
|Usługa raportowania SQL Server|Serwer raportowania Power BI|Power BI|Stanie|[Samouczek](/power-bi/report-server/migrate-report-server)|

### <a name="guidance-and-tutorials-for-migration-from-sql-server-to-an-iaas-instance-of-sql-server"></a>Wskazówki i samouczki dotyczące migracji z SQL Server do wystąpienia IaaS SQL Server

Po przeprowadzeniu migracji baz danych i usług do wystąpień PaaS nadal mogą istnieć struktury i usługi danych, które nie są zgodne z PaaS. Gdy istniejące ograniczenia uniemożliwiają Migrowanie struktur lub usług danych, poniższy samouczek ułatwia Migrowanie różnych zasobów w portfolio danych do rozwiązań IaaS platformy Azure.

Takie podejście może służyć do migrowania baz danych na SQL Server lub innych usług działających na źródłowym serwerze SQL.

|Źródło  |Cel  |Narzędzie  |Typ migracji  |Wskazówka  |
|---------|---------|---------|---------|---------|
|SQL Server pojedynczego wystąpienia|SQL Server w IaaS|Różnych|Stanie|[Samouczek](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)|

## <a name="optimization-process-changes"></a>Zmiany procesu optymalizacji

Podczas optymalizacji każda struktura danych, usługa lub SQL Server mogą być testowane, optymalizowane i promowane w środowisku produkcyjnym. Jest to największy wpływ na odchylenie od modelu migracji obciążeń.

W idealnym przypadku, zależne obciążenia, aplikacje i maszyny wirtualne będą migrowane w ramach tej samej iteracji co wystąpienie SQL Server. Kiedy ten idealny scenariusz występuje, obciążenie może być testowane wraz ze źródłem danych. Po przetestowaniu można wspierać strukturę danych do środowiska produkcyjnego, a proces synchronizacji można przerwać.

Niestety, największe zmiany w procesie optymalizacji podczas migracji bez obsługi obciążeń są dostępne, gdy istnieje znaczący odstęp czasu między migracją bazy danych i migracją obciążeń. W przypadku migrowania wielu baz danych w ramach migracji SQL Server te bazy danych mogą współistnieć zarówno w chmurze, jak i lokalnie dla wielu iteracji. W tym przedziale czasowym istnieje potrzeba zachowania synchronizacji danych, dopóki te zasoby zależne nie zostaną zmigrowane, przetestowane i podwyższone.

Przed podwyższeniem poziomu wszystkich obciążeń zależnych zespół będzie odpowiedzialny za obsługę synchronizacji danych z systemu źródłowego do systemu docelowego. Ta synchronizacja zużywa przepustowość sieci, koszty chmury i najważniejsze osoby. Odpowiednie wyrównanie planu wdrożenia w ramach migracji SQL Server "obciążenie" i wszystkie zależne obciążenia/aplikacje spowoduje zredukowanie tego kosztu.

### <a name="suggested-action-during-the-optimization-process"></a>Sugerowana akcja w procesie optymalizacji

Podczas procesów optymalizacji następujące zadania powinny zostać wykonane w każdej iteracji, dopóki wszystkie struktury i usługi danych nie zostaną podwyższone do środowiska produkcyjnego.

1. Sprawdź poprawność synchronizacji danych.
2. Przetestuj wszystkie zmigrowane aplikacje.
3. Zoptymalizuj strukturę aplikacji i danych w celu dostrojenia kosztów.
4. Podnieś poziom aplikacji do środowiska produkcyjnego.
5. Testowanie ciągłego ruchu lokalnego z lokalną bazą danych.
6. Przerwij synchronizację wszelkich danych podniesionych do środowiska produkcyjnego.
7. Przerwij oryginalną źródłową bazę danych.

Do momentu zakończenia kroku 5 nie można zakończyć baz danych ani synchronizacji. Dopóki wszystkie bazy danych na SQL Server przeprowadziły kroki 1-7, lokalne SQL Server powinno być traktowane jako produkcja i należy utrzymywać wszystkie synchronizacje.

## <a name="next-steps"></a>Następne kroki

Wróć do [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md), aby upewnić się, że metoda migracji jest w pełni dopasowana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
