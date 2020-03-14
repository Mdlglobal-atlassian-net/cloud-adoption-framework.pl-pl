---
title: Zalecane konwencje nazewnictwa i tagowania
description: Zapoznaj się ze szczegółowymi zaleceniami dotyczącymi nazewnictwa zasobów i tagowania, które są przeznaczone do obsługi wysiłków w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/05/2020
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness, fasttrack-edit
ms.openlocfilehash: 119a0b64fe81e593404735e5ce6bc0c656ab23e2
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312504"
---
<!-- cSpell:ignore eastus westus westeurope usgovia accountlookup messagequery -->

# <a name="recommended-naming-and-tagging-conventions"></a>Zalecane konwencje nazewnictwa i tagowania

Organizuj swoje zasoby w chmurze w celu zapewnienia obsługi działań związanych z zarządzaniem i księgowością. Dobrze zdefiniowane konwencje nazewnictwa i określania metadanych ułatwiają szybkie lokalizowanie zasobów i zarządzanie nimi. Te konwencje ułatwiają również kojarzenie kosztów użycia chmury z zespołami biznesowymi za pośrednictwem mechanizmów księgowości obciążenia zwrotnego i przewidywanych kosztów.

W Centrum architektury platformy Azure wskazówki dotyczące [reguł nazewnictwa i ograniczeń dotyczących zasobów platformy Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) są dostępne ogólne zalecenia i ograniczenia dotyczące platformy. W poniższej dyskusji przedstawiono wskazówki z bardziej szczegółowymi zaleceniami, które zaprojektowano w celu wspierania wysiłków związanych z wdrażaniem w chmurze przedsiębiorstwa.

Zmiana nazw zasobów może być trudna. Przed rozpoczęciem każdego dużego wdrożenia w chmurze Ustanów kompleksową konwencję nazewnictwa.

> [!NOTE]
> Każda firma ma inne wymagania w zakresie organizacji i zarządzania. Te zalecenia stanowią punkt wyjścia dla dyskusji w zespołach wdrożenia chmury.
>
> Ponieważ te dyskusje są realizowane, użyj następującego szablonu, aby przechwycić decyzje dotyczące nadawania nazw i tagowania wprowadzane podczas wyrównywania tych zaleceń do określonych potrzeb firmy.
>
> Pobierz [szablon śledzenia konwencji nazewnictwa i tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Nazewnictwo i tagowanie zasobów

Strategia nazewnictwa i tagowania obejmuje szczegóły biznesowe i operacyjne jako składniki nazw zasobów i tagów metadanych:

- Po stronie biznesowej tej strategii należy zapewnić, że nazwy zasobów i Tagi zawierają informacje organizacyjne, które są konieczne do zidentyfikowania zespołów. Korzystaj z zasobów wraz z właścicielami biznesowymi, którzy odpowiadają za koszty zasobów.
- Aspekt operacyjny zapewnia, że nazwy i tagi zawierają informacje używane przez zespoły informatyczne do identyfikowania obciążenia, aplikacji, środowiska, ważności oraz inne informacje przydatne do zarządzania zasobami.

## <a name="resource-naming"></a>Nazewnictwo zasobów

Skuteczna konwencja nazewnictwa polega na tworzeniu nazw zasobów przez uwzględnienie w nazwie ważnych informacji dotyczących danego zasobu. Na przykład przy użyciu tych [zalecanych konwencji nazewnictwa](#example-names)zasób publicznego adresu IP dla produkcyjnego obciążenia programu SharePoint jest nazwany w następujący sposób: `pip-sharepoint-prod-westus-001`.

Na podstawie tej nazwy można szybko zidentyfikować typ zasobu, skojarzone z nim obciążenie, jego środowisko wdrożeniowe oraz region świadczenia usługi Azure, w którym jest on hostowany.

### <a name="naming-scope"></a>Zakres nazewnictwa

Wszystkie typy zasobów platformy Azure mają zakres definiujący poziom, którego nazwy zasobów muszą być unikatowe. W swoim zakresie zasób musi mieć unikatową nazwę.

Na przykład sieć wirtualna ma zakres grupy zasobów, co oznacza, że w danej grupie zasobów może istnieć tylko jedna sieć o nazwie `vnet-prod-westus-001`. Inne grupy zasobów mogą mieć własną sieć wirtualną o nazwie `vnet-prod-westus-001`. Innym przykładem są podsieci, które wchodzą w zakres sieci wirtualnych, co oznacza, że każda podsieć w sieci wirtualnej musi mieć unikatową nazwę.

Niektóre nazwy zasobów, takich jak usługi PaaS z publicznymi punktami końcowymi lub etykietami nazw DNS maszyn wirtualnych, mają zakresy globalne, co oznacza, że muszą być unikatowe na całej platformie Azure.

Nazwy zasobów mają limity długości. Jest ważne, aby podczas opracowywania konwencji nazewnictwa zrównoważyć kontekst osadzony w nazwie z jej zakresem i długością. Aby uzyskać więcej informacji o regułach nazewnictwa w zakresie dozwolonych znaków, zakresów i długości nazw dla typów zasobów, zobacz temat [Naming conventions for Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) (Konwencje nazewnictwa dla zasobów platformy Azure).

### <a name="recommended-naming-components"></a>Zalecane składniki nazwy

Podczas konstruowania konwencji nazewnictwa zidentyfikuj kluczowe informacje, które mają być odzwierciedlone w nazwie zasobu. Różne informacje są istotne dla różnych typów zasobów. Poniższa lista zawiera przykłady informacji przydatnych podczas konstruowania nazw zasobów.

Składniki nazwy powinny być krótkie, aby zapobiegać przekraczaniu limitów długości nazw zasobów.

| Składnik nazwy            | Opis                                                                                                                                                                                                      | Przykłady                                         |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Jednostka biznesowa               | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach składnik ten może reprezentować pojedynczy korporacyjny element organizacyjny najwyższego poziomu. | _fin_, _mktg_, _product_, _it_, _corp_           |
| Typ subskrypcji           | Opis podsumowujący przeznaczenie subskrypcji zawierającej zasób. Często składa się z typu środowiska wdrożeniowego lub określonych obciążeń.                                                       | _produkcyjny_, _współużytkowany_, _Klient_                       |
| Nazwa aplikacji lub usługi | Nazwa aplikacji, obciążenia lub usługi, do której należy zasób.                                                                                                                                    | _navigator_, _emissions_, _sharepoint_, _hadoop_ |
| Środowisko wdrażania      | Etap cyklu życia programowania dla obciążenia obsługiwanego przez zasób.                                                                                                                              | produkcja, _dev_, _pytań i odpowiedzi_, _etap_, _test_             |
| Region                      | Region świadczenia usługi Azure, w którym wdrożono zasób.                                                                                                                                                                 | _zachodnie_, _eastus2_, _westeurope_, _usgovia_     |

### <a name="recommended-resource-type-prefixes"></a>Zalecane prefiksy typów zasobów

Każde obciążenie może składać się z wielu pojedynczych zasobów i usług. Włączenie prefiksów typów zasobów do nazw zasobów ułatwia wizualne identyfikowanie składników aplikacji lub usług.

Poniższa lista zawiera zalecane prefiksy typów zasobów platformy Azure do użycia podczas definiowania konwencji nazewnictwa.

<!-- cSpell:disable -->

### <a name="general"></a>Ogólne

| Typ elementu zawartości                      | Prefiks nazwy |
|---------------------------------|-------------|
| Grupa zasobów                  | rg-         |
| Definicja zasad               | zasad     |
| Wystąpienie usługi API Management | APIM       |

### <a name="networking"></a>Sieć

| Typ elementu zawartości                       | Prefiks nazwy |
|----------------------------------|-------------|
| Sieć wirtualna                  | vnet-       |
| Podsieć                           | snet-       |
| Interfejs sieciowy (NIC)          | nic-        |
| Publiczny adres IP                | pip-        |
| Moduł równoważenia obciążenia (wewnętrzny)         | lbi-        |
| Moduł równoważenia obciążenia (zewnętrzny)         | lbe-        |
| Sieciowa grupa zabezpieczeń     | nsg-        |
| Grupa zabezpieczeń aplikacji (ASG) | ASG        |
| Brama sieci lokalnej            | LGW        |
| Brama sieci wirtualnej          | vgw-        |
| Połączenie VPN                   | cn-         |
| Brama aplikacji              | agw-        |
| Tabela tras                      | Szlak      |
| Profil usługi Traffic Manager          | traf-       |

### <a name="compute-and-web"></a>Obliczenia i sieć Web

| Typ elementu zawartości                  | Prefiks nazwy |
|-----------------------------|-------------|
| Maszyna wirtualna             | vm          |
| Zestaw skalowania maszyn wirtualnych   | VMSS       |
| Zestaw dostępności            | skorzystać      |
| Konto magazynu maszyn wirtualnych          | stvm        |
| Połączona maszyna Azure Arc | arcm-       |
| Wystąpienie kontenera          | ACI        |
| Klaster AKS                 | AKS        |
| Klaster usługi Service Fabric      | SF         |
| Środowisko usługi App Service     | ASE        |
| Plan usługi App Service            | zamierza       |
| Aplikacja internetowa                     | aplikacje        |
| Aplikacja funkcji                | Func       |
| Usługa w chmurze               | umożliwiają        |
| Notification Hubs           | ntf-        |
| Notification Hubs przestrzeń nazw | ntfns-      |

### <a name="databases"></a>Bazy danych

| Typ elementu zawartości                     | Prefiks nazwy |
|--------------------------------|-------------|
| Serwer Azure SQL Database      | Server        |
| Baza danych Azure SQL Database             | sqldb-      |
| Baza danych Cosmos DB             | Cosmos     |
| Wystąpienie usługi Azure cache for Redis | redis-      |
| Baza danych MySQL                 | mysql-      |
| Baza danych PostgreSQL            | PSQL       |
| Azure SQL Data Warehouse       | sqldw-      |
| SQL Server Stretch Database    | sqlstrdb-   |

### <a name="storage"></a>Storage

| Typ elementu zawartości       | Prefiks nazwy |
|------------------|-------------|
| Konto magazynu  | St          |
| Azure StorSimple | ssimp       |

### <a name="ai--machine-learning"></a>SI i uczenie maszynowe

| Typ elementu zawartości                       | Prefiks nazwy |
|----------------------------------|-------------|
| Azure Cognitive Search           | srch-       |
| Azure Cognitive Services         | koło zębate        |
| Obszar roboczy usługi Azure Machine Learning | mlw-        |

### <a name="analytics-and-iot"></a>Analiza i IoT

| Typ elementu zawartości                      | Prefiks nazwy |
|---------------------------------|-------------|
| Serwer Azure Analysis Services  | definicj         |
| Azure Databricks obszar roboczy      | dbw-        |
| Usługa Azure Stream Analytics          | asa-        |
| Azure Data Factory              | ADF        |
| Konto Data Lake Store         | dls         |
| Konto Data Lake Analytics     | dla         |
| Centrum zdarzeń                       | evh-        |
| HDInsight — klaster Hadoop      | usługi     |
| HDInsight — klaster HBase       | HBase      |
| HDInsight — klaster Kafka       | Kafka      |
| HDInsight — klaster Spark       | Spark      |
| Klaster usługi HDInsight — burza       | burz      |
| Klaster usług HDInsight-ML | MLS        |
| Centrum IoT                         | rzeczy        |
| Power BI Embedded               | PBI        |

### <a name="integration"></a>Integracja

| Typ elementu zawartości        | Prefiks nazwy |
|-------------------|-------------|
| Aplikacje logiki        | logiki      |
| Service Bus       | sb-         |
| Kolejka Service Bus | sbq-        |
| Temat Service Bus | sbt-        |

### <a name="management-and-governance"></a>Zarządzanie i nadzór

| Typ elementu zawartości              | Prefiks nazwy |
|-------------------------|-------------|
| Potrzeby               | BP         |
| Magazyn kluczy               | KV         |
| Obszar roboczy usługi Log Analytics | rejestrowane        |
| Application Insights    | appi-       |
| Magazyn usługi Recovery Services | rsv-        |

### <a name="migration"></a>Migracja

| Typ elementu zawartości                          | Prefiks nazwy |
|-------------------------------------|-------------|
| Projekt Azure Migrate               | migr-       |
| Wystąpienie Database Migration Service | DMS        |
| Magazyn usługi Recovery Services             | rsv-        |

<!-- cSpell:enable -->

## <a name="metadata-tags"></a>Tagi metadanych

Po zastosowaniu tagów metadanych do zasobów w chmurze można dołączyć informacje o tych elementach zawartości, których nie można było uwzględnić w nazwie zasobu. Te informacje służą do wykonywania bardziej zaawansowanego filtrowania i raportowania zasobów. Tagi te powinny zawierać kontekst dotyczący obciążenia lub aplikacji skojarzonych z zasobem, wymagania operacyjne oraz informacje o własności. Te informacje mogą być używane przez zespoły informatyczne lub biznesowe do odnajdywania zasobów lub generowania raportów dotyczących użycia zasobów i rozliczeń.

Tagi stosowane do zasobów i tagi wymagane lub opcjonalne są różne w różnych organizacjach. Poniższa lista zawiera przykłady typowych tagów przechwytujących ważny kontekst i informacje o zasobach. Użyj tej listy jako punktu wyjścia do ustanowienia własnych konwencji tagowania.

| Nazwa tagu                  | Opis                                                                                                                                                                                                          | Klucz               | Przykładowa wartość                                              |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|------------------------------------------------------------|
| Nazwa aplikacji          | Nazwa aplikacji, usługi lub obciążenia, z którymi jest skojarzony zasób.                                                                                                                                       | _ApplicationName_ | _{nazwa aplikacji}_                                               |
| Nazwa osoby zatwierdzającej             | Osoba odpowiedzialna za zatwierdzenie kosztów związanych z tym zasobem.                                                                                                                                                     | _Approver_        | _{e-mail}_                                                  |
| Wymagany/zatwierdzony budżet  | Pieniądze przydzielone do tej aplikacji, usługi lub obciążenia.                                                                                                                                                          | _BudgetAmount_    | _{\$}_                                                     |
| Jednostka biznesowa             | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach ten tag może reprezentować pojedynczy korporacyjny lub współużytkowany element organizacyjny najwyższego poziomu. | _BusinessUnit_    | _Finanse_, _Marketing_, _{Product Name}_ , _Corp_, _Shared_ |
| Centrum kosztu               | Księgowe centrum kosztu skojarzone z tym zasobem.                                                                                                                                                                | _CostCenter_      | _{numer}_                                                 |
| Odzyskiwanie po awarii         | Ważność aplikacji, obciążenia lub usługi dla działania firmy.                                                                                                                                                       | _DR_              | _Krytyczne_, _krytyczne_, _podstawowe_                |
| Data zakończenia projektu   | Data, na którą zaplanowano wycofanie aplikacji, obciążenia lub usługi.                                                                                                                                         | _EndDate_         | _{data}_                                                   |
| Środowisko               | Środowisko wdrażania aplikacji, obciążenia lub usługi.                                                                                                                                                     | _Env_             | Produkcja, _dev_, _pytań i odpowiedzi_, _etap_, _test_                       |
| Nazwa właściciela                | Właściciel aplikacji, obciążenia lub usługi.                                                                                                                                                                      | _Właściciel_           | _{e-mail}_                                                  |
| Nazwa żądającego            | Użytkownik, który zażądał utworzenia tej aplikacji.                                                                                                                                                                 | _Requestor_       | _{e-mail}_                                                  |
| Klasa usługi             | Poziom umowy dotyczącej poziomu usług aplikacji, obciążenia lub usługi.                                                                                                                                              | _ServiceClass_    | _Dev_, _Bronze_, _Silver_, _Gold_                          |
| Data rozpoczęcia projektu | Dzień, w którym nastąpiło pierwsze wdrożenie aplikacji, obciążenia lub usługi.                                                                                                                                                  | _StartDate_       | _{data}_                                                   |

## <a name="example-names"></a>Przykładowe nazwy

W poniższej sekcji przedstawiono przykłady nazw wspólnych typów zasobów platformy Azure w ramach wdrożenia w chmurze przedsiębiorstwa.

<!-- cSpell:disable -->

<!-- markdownlint-disable MD024 MD033 -->

### <a name="example-names-general"></a>Przykładowe nazwy: ogólne

| Typ elementu zawartości                      | Zakres                              | Format                                                      | Przykłady                                                                                                                |
|---------------------------------|------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Subskrypcja                    | Koncie <br/>Enterprise Agreement | \<Jednostka biznesowa\>-\<Typ subskrypcji\>-\<\#\#\#\>          | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul>                                        |
| Grupa zasobów                  | Subskrypcja                       | RG-\<nazwę aplikacji lub usługi\>-\<typ subskrypcji\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |
| Wystąpienie usługi API Management | Globalny                             | APIM\<aplikacji lub nazwy usługi\>                                | APIM-Navigator-prod                                                                                                     |

### <a name="example-names-networking"></a>Przykładowe nazwy: sieć

| Typ elementu zawartości                   | Zakres           | Format                                                               | Przykłady                                                                                                                      |
|------------------------------|-----------------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| Sieć wirtualna              | Grupa zasobów  | vnet-\<Typ subskrypcji\>-\<Region\>-\<\#\#\#\>                     | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                      |
| Podsieć                       | Sieć wirtualna | snet-\<subskrypcja\>-\<podregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                      |
| Interfejs sieciowy (NIC)      | Grupa zasobów  | nic-\<\#\#\>-\<nazwa maszyny wirtualnej\>-\<subskrypcja\>\<\#\#\#\>                   | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>                 |
| Publiczny adres IP            | Grupa zasobów  | pip-\<nazwa maszyny wirtualnej lub nazwa aplikacji\>-\<Środowisko\>-\<podregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                              |
| Moduł równoważenia obciążenia                | Grupa zasobów  | lb-\<nazwa aplikacji lub rola\>\<Środowisko\>\<\#\#\#\>                     | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| Sieciowa grupa zabezpieczeń | Podsieć lub karta sieciowa   | sieciowej grupy zabezpieczeń — Nazwa zasad\<lub nazwa aplikacji\>-\<\#\#\#\>                           | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>             |
| Brama sieci lokalnej        | Brama wirtualna | LGW\<typ subskrypcji\>-\<regionu\>-\<\#\#\#\>                      | <ul><li>LGW-Shared-eastus2-001 </li><li>LGW-prod-zachodni-001 </li><li>LGW-Client-eastus2-001</li></ul>                         |
| Brama sieci wirtualnej      | Sieć wirtualna | vgw\<typ subskrypcji\>-\<regionu\>-\<\#\#\#\>                      | <ul><li>vgw-Shared-eastus2-001 </li><li>vgw-prod-zachodni-001 </li><li>vgw-Client-eastus2-001</li></ul>                         |
| Połączenie lokacja-lokacja      | Grupa zasobów  | cn-\<nazwa bramy lokalnej\>-to-\<nazwa bramy wirtualnej\>                | <ul><li>CN-LGW-Shared-eastus2-001-to-vgw-Shared-eastus2-001 </li><li>CN-LGW-Shared-eastus2-001-to-Shared-zachodnie-001</li></ul> |
| Połączenie VPN               | Grupa zasobów  | cn-\<subskrypcja1\>\<region1\>-to-\<subskrypcja2\>\<region2\>-     | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                  |
| Tabela tras                  | Grupa zasobów  | Nazwa tabeli tras\<trasy\>                                           | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                                        |
| Etykieta nazwy DNS                    | Globalny          | \<Rekord maszyny wirtualnej\>.[\<region\>.cloudapp.azure.com]                   | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                                      |

### <a name="example-names-compute-and-web"></a>Przykładowe nazwy: obliczenia i sieci Web

| Typ elementu zawartości                  | Zakres          | Format                                                              | Przykłady                                                                                                                          |
|-----------------------------|----------------|---------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Maszyna wirtualna             | Grupa zasobów | vm\<nazwa zasad lub nazwa aplikacji\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Konto magazynu maszyn wirtualnych          | Globalny         | stvm\<typ wydajności\>\<nazwa aplikacji lub nazwa produktu\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Aplikacja internetowa                     | Globalny         | Nazwa aplikacji\<aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{azurewebsites.net}]   | <ul><li>app-navigator-prod-001.azurewebsites.net </li><li>app-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Aplikacja funkcji                | Globalny         | Func-\<nazwę aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{azurewebsites.net}]  | <ul><li>func-navigator-prod-001.azurewebsites.net </li><li>func-accountlookup-dev-001.azurewebsites.net</li></ul>                 |
| Usługa w chmurze               | Globalny         | można\<nazwę aplikacji\>-\<środowisku\>-\<\#\#\#\>. [{cloudapp.net}]        | <ul><li>could-navigator-prod-001.azurewebsites.net </li><li>could-accountlookup-dev-001.azurewebsites.net</li></ul>                   |
| Centrum powiadomień            | Grupa zasobów | NTF\<\>-\<środowisko\>                                    | <ul><li>NTF-Navigator-prod </li><li>NTF-emisje — dev</li></ul>                                                                   |
| Notification Hubs przestrzeń nazw | Globalny         | ntfns\<\>-\<środowisko\>                                  | <ul><li>ntfns-Navigator-prod </li><li>ntfns-emisje — dev</li></ul>                                                               |

### <a name="example-names-databases"></a>Przykładowe nazwy: bazy danych

| Typ elementu zawartości                     | Zakres              | Format                                 | Przykłady                                                                  |
|--------------------------------|--------------------|----------------------------------------|---------------------------------------------------------------------------|
| Serwer Azure SQL Database      | Globalny             | Nazwa aplikacji SQL\<\>-\<środowisko\>       | <ul><li>SQL — Nawigator — prod </li><li>SQL-emisje — dev</li></ul>           |
| Baza danych Azure SQL Database             | Azure SQL Database | SQLDB\<>\<środowisku\> | <ul><li>SQLDB — użytkownicy — produkcja </li><li>SQLDB — użytkownicy — dev</li></ul>               |
| Baza danych Cosmos DB             | Globalny             | Cosmos\<\>-\<środowisko\>    | <ul><li>Cosmos-Navigator-prod </li><li>Cosmos-emisje — dev</li></ul>     |
| Wystąpienie usługi Azure cache for Redis | Globalny             | redis-\<Nazwa aplikacji\>-\<Środowisko\>     | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Baza danych MySQL                 | Globalny             | mysql-\<Nazwa aplikacji\>-\<Środowisko\>     | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Baza danych PostgreSQL            | Globalny             | PSQL\<\>-\<środowisko\>      | <ul><li>PSQL-Navigator-prod </li><li>PSQL-emisje — dev</li></ul>         |
| Azure SQL Data Warehouse       | Globalny             | sqldw-\<Nazwa aplikacji\>-\<Środowisko\>     | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database    | Azure SQL Database | sqlstrdb-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="example-names-storage"></a>Przykładowe nazwy: Storage

| Typ elementu zawartości                        | Zakres  | Format                                                                        | Przykłady                                                              |
|-----------------------------------|--------|-------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| Konto magazynu (ogólne użycie)     | Globalny | st\<nazwa magazynu\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Konto magazynu (dzienniki diagnostyczne) | Globalny | stdiag\<pierwsze 2 litery nazwy subskrypcji i numer\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                  | Globalny | ssimp\<Nazwa aplikacji\>\<Środowisko\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="example-names-ai--machine-learning"></a>Przykładowe nazwy: AI + Machine Learning

| Typ elementu zawartości                       | Zakres          | Format                            | Przykłady                                                          |
|----------------------------------|----------------|-----------------------------------|-------------------------------------------------------------------|
| Azure Cognitive Search           | Globalny         | srch-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services         | Grupa zasobów | koło zębate\<\>-\<środowisko\>  | <ul><li>koło zębate-Navigator-prod </li><li>koło zębate-emisje — dev</li></ul>   |
| Obszar roboczy usługi Azure Machine Learning | Grupa zasobów | MLW\<\>-\<środowisko\>  | <ul><li>MLW-Navigator-prod </li><li>MLW-emisje — dev</li></ul>   |

### <a name="example-names-analytics-and-iot"></a>Przykładowe nazwy: analizy i IoT

| Typ elementu zawartości                  | Zakres          | Format                              | Przykłady                                                              |
|-----------------------------|----------------|-------------------------------------|-----------------------------------------------------------------------|
| Azure Data Factory          | Globalny         | ADF —\<nazwę aplikacji\>\<środowisku\>     | <ul><li>ADF — Nawigator — produkcja </li><li>ADF — emisje — dev</li></ul>       |
| Usługa Azure Stream Analytics      | Grupa zasobów | asa-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>       |
| Konto Data Lake Analytics | Globalny         | dla\<Nazwa aplikacji\>\<Środowisko\>      | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>           |
| Konto Data Lake Storage   | Globalny         | dls\<Nazwa aplikacji\>\<Środowisko\>      | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>           |
| Centrum zdarzeń                   | Globalny         | evh-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>       |
| HDInsight — klaster HBase   | Globalny         | HBase\<\>-\<środowisko\>  | <ul><li>HBase-Navigator-prod </li><li>HBase-emisje — dev</li></ul>   |
| HDInsight — klaster Hadoop  | Globalny         | Nazwa aplikacji usługi Hadoop —\<\>-\<środowisko\> | <ul><li>Hadoop — Nawigator — produkcja </li><li>Hadoop — emisje — dev</li></ul> |
| HDInsight — klaster Spark   | Globalny         | Nazwa aplikacji platformy Spark-\<\>-\<środowisko\>  | <ul><li>Spark-Navigator — prod </li><li>Spark-emisje — dev </li></ul>  |
| Centrum IoT                     | Globalny         | Nazwa aplikacji IoT-\<\>-\<środowisko\>    | <ul><li>IoT-Navigator — prod </li><li>IoT-emisje — dev</li></ul>       |
| Power BI Embedded           | Globalny         | PBI\<\>\<środowisku\>     | <ul><li>PBI-Navigator-prod </li><li>PBI-emisje — dev</li></ul>       |

### <a name="example-names-integration"></a>Przykładowe nazwy: integracja

| Typ elementu zawartości        | Zakres       | Format                                                     | Przykłady                                                      |
|-------------------|-------------|------------------------------------------------------------|---------------------------------------------------------------|
| Service Bus       | Globalny      | sb-\<Nazwa aplikacji\>-\<Środowisko\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Kolejka Service Bus | Service Bus | sbq-\<deskryptor kolejki\>                                   | <ul><li>sbq-messagequery</li></ul>                            |
| Temat Service Bus | Service Bus | SBT\<deskryptora zapytania\>                                   | <ul><li>sbt-messagequery</li></ul>                            |
