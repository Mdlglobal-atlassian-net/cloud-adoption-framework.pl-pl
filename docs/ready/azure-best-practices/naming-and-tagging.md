---
title: Zalecane konwencje nazewnictwa i tagowania
description: Ten artykuł zawiera szczegółowe zalecenia dotyczące nazewnictwa zasobów i tagowania mające na celu wsparcie działań związanych z wdrażaniem chmury przedsiębiorstwa.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: c85f4423ea61346e8692fd19ced0d53242733284
ms.sourcegitcommit: 35d01bccc8ecbec38f6247a065a309ec691ca810
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2020
ms.locfileid: "77213596"
---
# <a name="recommended-naming-and-tagging-conventions"></a>Zalecane konwencje nazewnictwa i tagowania

Organizowanie zasobów opartych na chmurze w taki sposób, aby pomoc w zakresie zarządzania operacyjnego i pomocy technicznej była powszechnym wyzwaniem w przypadku dużych wysiłków z tytułu wdrożenia w chmurze. Dzięki zastosowaniu dobrze zdefiniowanych konwencji nazewnictwa i tagowania metadanych do zasobów hostowanych w chmurze pracownicy IT mogą szybko znajdować zasoby i nimi zarządzać. Dobrze zdefiniowane nazwy i tagi pomagają również w dopasowaniu kosztów użycia chmury do zespołów biznesowych przy użyciu mechanizmów obciążenia zwrotnego i księgowania w zakresie przewidywania kosztów.

W Centrum architektury platformy Azure wskazówki dotyczące [reguł nazewnictwa i ograniczeń dotyczących zasobów platformy Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) są dostępne ogólne zalecenia i ograniczenia dotyczące platformy. W poniższej dyskusji przedstawiono wskazówki z bardziej szczegółowymi zaleceniami, które zaprojektowano w celu wspierania wysiłków związanych z wdrażaniem w chmurze przedsiębiorstwa.

Zmiana nazw zasobów może być trudna. Przed rozpoczęciem każdego dużego wdrożenia w chmurze należy określić priorytety ustanawiania kompleksowej konwencji nazewnictwa.

> [!NOTE]
> Każda firma ma inne wymagania w zakresie organizacji i zarządzania. Te zalecenia stanowią punkt wyjścia dla dyskusji w zespołach wdrożenia chmury.
>
> Ponieważ te dyskusje są realizowane, użyj następującego szablonu, aby przechwycić decyzje dotyczące nadawania nazw i tagowania wprowadzane podczas wyrównywania tych zaleceń do określonych potrzeb firmy.
>
> Pobierz [szablon śledzenia konwencji nazewnictwa i tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Nazewnictwo i tagowanie zasobów

Strategia nazewnictwa i tagowania obejmuje szczegóły biznesowe i operacyjne jako składniki nazw zasobów i tagów metadanych:

- Po stronie biznesowej tej strategii należy zapewnić, że nazwy zasobów i Tagi zawierają informacje o organizacji, które są konieczne do zidentyfikowania zespołów. Korzystaj z zasobów wraz z właścicielami biznesowymi, którzy odpowiadają za koszty zasobów.
- Aspekt operacyjny zapewnia, że nazwy i tagi zawierają informacje używane przez zespoły informatyczne do identyfikowania obciążenia, aplikacji, środowiska, ważności oraz inne informacje przydatne do zarządzania zasobami.

### <a name="resource-naming"></a>Nazewnictwo zasobów

Skuteczna konwencja nazewnictwa polega na tworzeniu nazw zasobów przez uwzględnienie w nazwie ważnych informacji dotyczących danego zasobu. Na przykład przy użyciu tych [zalecanych konwencji nazewnictwa](#sample-naming-convention)zasób publicznego adresu IP dla produkcyjnego obciążenia programu SharePoint jest nazwany w następujący sposób: `pip-sharepoint-prod-westus-001`.

Na podstawie tej nazwy można szybko zidentyfikować typ zasobu, skojarzone z nim obciążenie, jego środowisko wdrożeniowe oraz region świadczenia usługi Azure, w którym jest on hostowany.

#### <a name="naming-scope"></a>Zakres nazewnictwa

Wszystkie typy zasobów platformy Azure mają zakres definiujący poziom, którego nazwy zasobów muszą być unikatowe. W swoim zakresie zasób musi mieć unikatową nazwę.

Na przykład sieć wirtualna ma zakres grupy zasobów, co oznacza, że w danej grupie zasobów może istnieć tylko jedna sieć o nazwie `vnet-prod-westus-001`. Inne grupy zasobów mogą mieć własną sieć wirtualną o nazwie `vnet-prod-westus-001`. Innym przykładem są podsieci, które wchodzą w zakres sieci wirtualnych, co oznacza, że każda podsieć w sieci wirtualnej musi mieć unikatową nazwę.

Niektóre nazwy zasobów, takich jak usługi PaaS z publicznymi punktami końcowymi lub etykietami nazw DNS maszyn wirtualnych, mają zakresy globalne, co oznacza, że muszą być unikatowe na całej platformie Azure.

Nazwy zasobów mają limity długości. Jest ważne, aby podczas opracowywania konwencji nazewnictwa zrównoważyć kontekst osadzony w nazwie z jej zakresem i długością. Aby uzyskać więcej informacji o regułach nazewnictwa w zakresie dozwolonych znaków, zakresów i długości nazw dla typów zasobów, zobacz temat [Naming conventions for Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) (Konwencje nazewnictwa dla zasobów platformy Azure).

#### <a name="recommended-naming-components"></a>Zalecane składniki nazwy

Podczas konstruowania konwencji nazewnictwa zidentyfikuj kluczowe informacje, które mają być odzwierciedlone w nazwie zasobu. Różne informacje są istotne dla różnych typów zasobów. Poniższa lista zawiera przykłady informacji przydatnych podczas konstruowania nazw zasobów.

Składniki nazwy powinny być krótkie, aby zapobiegać przekraczaniu limitów długości nazw zasobów.

| Składnik nazwy | Opis | Przykłady |
| --- | --- | --- |
| Jednostka biznesowa | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach składnik ten może reprezentować pojedynczy korporacyjny element organizacyjny najwyższego poziomu. | _fin_, _mktg_, _product_, _it_, _corp_ |
| Typ subskrypcji | Opis podsumowujący przeznaczenie subskrypcji zawierającej zasób. Często składa się z typu środowiska wdrożeniowego lub określonych obciążeń. | _produkcyjny_, _współużytkowany_, _Klient_ |
| Nazwa aplikacji lub usługi | Nazwa aplikacji, obciążenia lub usługi, do której należy zasób. | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Środowisko wdrażania | Etap cyklu życia programowania dla obciążenia obsługiwanego przez zasób. | produkcja, _dev_, _pytań i odpowiedzi_, _etap_, _test_ |
| Region | Region świadczenia usługi Azure, w którym wdrożono zasób. | _zachodnie_, _eastus2_, _westeurope_, _usgovia_ |

#### <a name="recommended-resource-type-prefixes"></a>Zalecane prefiksy typów zasobów

Każde obciążenie może składać się z wielu pojedynczych zasobów i usług. Włączenie prefiksów typów zasobów do nazw zasobów ułatwia wizualne identyfikowanie składników aplikacji lub usług.

Poniższa lista zawiera zalecane prefiksy typów zasobów platformy Azure do użycia podczas definiowania konwencji nazewnictwa.

| Typ zasobu                       | Prefiks nazwy zasobu |
| ----------------------------------- | -------------------- |
| Grupa zasobów                      | rg-                  |
| Zestaw dostępności                    | skorzystać               |
| Usługa API Management              | interfejsu API                 |
| Sieć wirtualna                     | vnet-                |
| Brama sieci wirtualnej             | vnetgw-              |
| Połączenie bramy                  | cn-                  |
| Podsieć                              | snet-                |
| Sieciowa grupa zabezpieczeń              | nsg-                 |
| Tabela tras                         | Szlak               |
| Maszyna wirtualna                     | vm                   |
| Konto magazynu maszyn wirtualnych                  | stvm                 |
| Publiczny adres IP                           | pip-                 |
| Moduł równoważenia obciążenia                       | lb-                  |
| Karta sieciowa                                 | nic-                 |
| Magazyn kluczy                           | KV                  |
| Klaster AKS                         | AKS                 |
| Kontener AKS                       | Con                 |
| Service Bus                         | sb-                  |
| Kolejka Service Bus                   | sbq-                 |
| Temat Service Bus                   | sbt-                 |
| Plan usługi App Service                    | zamierza                |
| Aplikacja internetowa                             | aplikacje                 |
| Aplikacja funkcji                        | Func                |
| Usługa w chmurze                       | umożliwiają                 |
| Serwer Azure SQL Database           | Server                 |
| Baza danych Azure SQL Database                  | sqldb-               |
| Baza danych Cosmos DB                  | Cosmos              |
| Pamięć podręczna platformy Azure dla pamięci podręcznej Redis         | redis-               |
| Baza danych MySQL                      | mysql-               |
| Baza danych PostgreSQL                 | PSQL                |
| Azure SQL Data Warehouse            | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Konto magazynu                     | St                   |
| Azure StorSimple                    | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services            | koło zębate                 |
| Obszar roboczy usługi Azure Machine Learning    | mlw-                 |
| Azure Data Lake Storage             | dls                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight — Spark             | hdis-                |
| Azure HDInsight — Hadoop            | hdihd-               |
| Azure HDInsight — R Server          | hdir-                |
| Azure HDInsight — HBase             | hdihb-               |
| Power BI Embedded                   | PBI                 |
| Usługa Azure Stream Analytics              | asa-                 |
| Azure Data Factory                  | ADF                 |
| Centrum zdarzeń                           | evh-                 |
| Centrum IoT                             | rzeczy                 |
| Centra powiadomień                   | ntf-                 |
| Notification Hubs przestrzeń nazw         | ntfns-               |

### <a name="metadata-tags"></a>Tagi metadanych

Po zastosowaniu tagów metadanych do zasobów w chmurze można dołączyć informacje o tych elementach zawartości, których nie można było uwzględnić w nazwie zasobu. Te informacje służą do wykonywania bardziej zaawansowanego filtrowania i raportowania zasobów. Tagi te powinny zawierać kontekst dotyczący obciążenia lub aplikacji skojarzonych z zasobem, wymagania operacyjne oraz informacje o własności. Te informacje mogą być używane przez zespoły informatyczne lub biznesowe do odnajdywania zasobów lub generowania raportów dotyczących użycia zasobów i rozliczeń.

Tagi stosowane do zasobów i tagi wymagane lub opcjonalne są różne w różnych organizacjach. Poniższa lista zawiera przykłady typowych tagów przechwytujących ważny kontekst i informacje o zasobach. Użyj tej listy jako punktu wyjścia do ustanowienia własnych konwencji tagowania.

| Nazwa tagu                  | Opis                                                                                                                                                                                                    | Klucz               | Przykładowa wartość                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Nazwa aplikacji          | Nazwa aplikacji, usługi lub obciążenia, z którymi jest skojarzony zasób.                                                                                                                                 | _ApplicationName_ | _{nazwa aplikacji}_                                    |
| Nazwa osoby zatwierdzającej             | Osoba odpowiedzialna za zatwierdzenie kosztów związanych z tym zasobem.                                                                                                                                               | _Approver_        | _{e-mail}_                                       |
| Wymagany/zatwierdzony budżet  | Pieniądze przydzielone do tej aplikacji, usługi lub obciążenia.                                                                                                                                                    | _BudgetAmount_    | _{\$}_                                          |
| Jednostka biznesowa             | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach ten tag może reprezentować pojedynczy korporacyjny lub współużytkowany element organizacyjny najwyższego poziomu. | _BusinessUnit_    | _Finanse_, _Marketing_, _{Product Name}_ , _Corp_, _Shared_ |
| Centrum kosztu               | Księgowe centrum kosztu skojarzone z tym zasobem.                                                                                                                                                          | _CostCenter_      | _{numer}_                                      |
| Odzyskiwanie po awarii         | Ważność aplikacji, obciążenia lub usługi dla działania firmy.                                                                                                                                                | _DR_              | _Krytyczne_, _krytyczne_, _podstawowe_         |
| Data zakończenia projektu   | Data, na którą zaplanowano wycofanie aplikacji, obciążenia lub usługi.                                                                                                                                  | _EndDate_         | _{data}_                                        |
| Środowisko               | Środowisko wdrażania aplikacji, obciążenia lub usługi.                                                                                                                                              | _Env_             | Produkcja, _dev_, _pytań i odpowiedzi_, _etap_, _test_                    |
| Nazwa właściciela                | Właściciel aplikacji, obciążenia lub usługi.                                                                                                                                                                | _Właściciel_           | _{e-mail}_                                       |
| Nazwa żądającego            | Użytkownik, który zażądał utworzenia tej aplikacji.                                                                                                                                                          | _Requestor_       | _{e-mail}_                                       |
| Klasa usługi             | Poziom umowy dotyczącej poziomu usług aplikacji, obciążenia lub usługi.                                                                                                                                       | _ServiceClass_    | _Dev_, _brązowy_, _Silver_, Git _Gold_                     |
| Data rozpoczęcia projektu | Dzień, w którym nastąpiło pierwsze wdrożenie aplikacji, obciążenia lub usługi.                                                                                                                                           | _StartDate_       | _{data}_                                        |

## <a name="sample-naming-convention"></a>Przykładowa konwencja nazewnictwa

W poniższej sekcji przedstawiono przykłady schematów nazewnictwa dla często stosowanych typów zasobów platformy Azure, które są wdrażane podczas wdrażania chmury w przedsiębiorstwie.

<!-- markdownlint-disable MD033 -->

### <a name="subscriptions"></a>Subskrypcje

| Typ elementu zawartości   | Zakres                        | Format                                             | Przykłady                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Subskrypcja | Umowa dotycząca konta/przedsiębiorstwa | \<Jednostka biznesowa\>-\<Typ subskrypcji\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Grupy zasobów

| Typ elementu zawartości     | Zakres        | Format                                                     | Przykłady                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Grupa zasobów | Subskrypcja | RG-\<nazwę aplikacji lub usługi\>-\<typ subskrypcji\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Sieć wirtualna

| Typ elementu zawartości               | Zakres           | Format                                                                | Przykłady                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Azure Virtual Network          | Grupa zasobów  | vnet-\<Typ subskrypcji\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Brama wirtualna sieci wirtualnej     | Sieć wirtualna | vnetgw-v-\<typ subskrypcji\>-\<regionu\>-\<\#\#\#\>                 | <ul><li>vnetgw-v-Shared-eastus2-001 </li><li>vnetgw-v-prod-zachodni-001 </li><li>vnetgw-v-Client-eastus2-001</li></ul>                   |
| Brama lokalna sieci wirtualnej       | Brama wirtualna | vnetgw-l-\<typ subskrypcji\>-\<regionu\>-\<\#\#\#\>                 | <ul><li>vnetgw-l-Shared-eastus2-001 </li><li>vnetgw-l-prod-zachodni-001 </li><li>vnetgw-l-Client-eastus2-001</li></ul>                   |
| Połączenia typu lokacja-lokacja | Grupa zasobów  | cn-\<nazwa bramy lokalnej\>-to-\<nazwa bramy wirtualnej\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Połączenia sieci wirtualnych         | Grupa zasobów  | cn-\<subskrypcja1\>\<region1\>-to-\<subskrypcja2\>\<region2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                     |
| Podsieć                   | Sieć wirtualna | snet-\<subskrypcja\>-\<podregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Sieciowa grupa zabezpieczeń   | Podsieć lub karta sieciowa   | nsg-\<nazwa zasad lub nazwa aplikacji\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Publiczny adres IP                | Grupa zasobów  | pip-\<nazwa maszyny wirtualnej lub nazwa aplikacji\>-\<Środowisko\>-\<podregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Typ elementu zawartości         | Zakres          | Format                                                              | Przykłady                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Grupa zasobów | vm\<nazwa zasad lub nazwa aplikacji\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Konto magazynu maszyn wirtualnych | Globalny         | stvm\<typ wydajności\>\<nazwa aplikacji lub nazwa produktu\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Etykieta nazwy DNS          | Globalny         | \<Rekord maszyny wirtualnej\>.[\<region\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Grupa zasobów | lb-\<nazwa aplikacji lub rola\>\<Środowisko\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| Karta sieciowa                | Grupa zasobów | nic-\<\#\#\>-\<nazwa maszyny wirtualnej\>-\<subskrypcja\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>Usługi PaaS

| Typ elementu zawartości           | Zakres  | Format                                                              | Przykłady                                                                                 |
|----------------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure Web Apps       | Globalny | Nazwa aplikacji\<aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Functions      | Globalny | Func-\<nazwę aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{azurewebsites.net}] | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul> |
| usług Azure Cloud Services | Globalny | można\<nazwę aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{cloudapp.net}]       | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Typ elementu zawartości         | Zakres       | Format                                                     | Przykłady                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Globalny      | sb-\<Nazwa aplikacji\>-\<Środowisko\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Kolejki usługi Azure Service Bus | Service Bus | sbq-\<deskryptor kolejki\>                                   | <ul><li>sbq-messagequery</li></ul>                   |
| Tematy Azure Service Bus | Service Bus | SBT\<deskryptora zapytania\>                                   | <ul><li>sbt-messagequery</li></ul>                   |

### <a name="databases"></a>Bazy danych

| Typ elementu zawartości                          | Zakres              | Format                                | Przykłady                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Serwer Azure SQL Database           | Globalny             | Nazwa aplikacji SQL\<\>-\<środowisko\>      | <ul><li>SQL — Nawigator — prod </li><li>SQL-emisje — dev</li></ul>           |
| Azure SQL Database                  | Azure SQL Database | SQLDB\<>\<środowisku\>| <ul><li>SQLDB — użytkownicy — produkcja </li><li>SQLDB — użytkownicy — dev</li></ul>               |
| Azure Cosmos DB                     | Globalny             | Cosmos\<\>-\<środowisko\>   | <ul><li>Cosmos-Navigator-prod </li><li>Cosmos-emisje — dev</li></ul>       |
| Azure Cache for Redis               | Globalny             | redis-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Globalny             | mysql-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure Database for PostgreSQL       | Globalny             | PSQL\<\>-\<środowisko\>     | <ul><li>PSQL-Navigator-prod </li><li>PSQL-emisje — dev</li></ul>         |
| Azure SQL Data Warehouse            | Globalny             | sqldw-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | sqlstrdb-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Storage

| Typ elementu zawartości                              | Zakres  | Format                                                                        | Przykłady                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Konto usługi Azure Storage — zastosowanie ogólne     | Globalny | st\<nazwa magazynu\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Konto usługi Azure Storage — dzienniki diagnostyczne | Globalny | stdiag\<pierwsze 2 litery nazwy subskrypcji i numer\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                        | Globalny | ssimp\<Nazwa aplikacji\>\<Środowisko\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>SI i uczenie maszynowe

| Typ elementu zawartości                       | Zakres          | Format                            | Przykłady                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Globalny         | srch-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Grupa zasobów | koło zębate\<\>-\<środowisko\>   | <ul><li>koło zębate-Navigator-prod </li><li>koło zębate-emisje — dev</li></ul>     |
| Obszar roboczy usługi Azure Machine Learning | Grupa zasobów | MLW\<\>-\<środowisko\>   | <ul><li>MLW-Navigator-prod </li><li>MLW-emisje — dev</li></ul>     |

### <a name="analytics"></a>Analiza

| Typ elementu zawartości                | Zakres  | Format                             | Przykłady                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Globalny | ADF —\<nazwę aplikacji\>\<środowisku\>    | <ul><li>ADF — Nawigator — produkcja </li><li>ADF — emisje — dev</li></ul>     |
| Azure Data Lake Storage   | Globalny | dls\<Nazwa aplikacji\>\<Środowisko\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Globalny | dla\<Nazwa aplikacji\>\<Środowisko\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight — Spark   | Globalny | hdis-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight — Hadoop  | Globalny | hdihd-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight — R Server| Globalny | hdir-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight — HBase   | Globalny | hdihb-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Power BI Embedded         | Globalny | PBI\<\>\<środowisku\>    | <ul><li>PBI-Navigator-prod </li><li>PBI-emisje — dev</li></ul> |

### <a name="data-streams--internet-of-things-iot"></a>Strumienie danych/Internet rzeczy (IoT)

| Typ elementu zawartości                         | Zakres          | Format                             | Przykłady                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Usługa Azure Stream Analytics             | Grupa zasobów | asa-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Globalny         | Nazwa aplikacji IoT-\<\>-\<środowisko\>   | <ul><li>IoT-Navigator — prod </li><li>IoT-emisje — dev</li></ul>     |
| Azure Event Hubs                   | Globalny         | evh-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs            | Grupa zasobów | NTF\<\>-\<środowisko\>   | <ul><li>NTF-Navigator-prod </li><li>NTF-emisje — dev</li></ul>     |
| Przestrzeń nazw usługi Azure Notification Hubs  | Globalny         | ntfns\<\>-\<środowisko\> | <ul><li>ntfns-Navigator-prod </li><li>ntfns-emisje — dev</li></ul> |
