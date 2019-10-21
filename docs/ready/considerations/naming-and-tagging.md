---
title: 'Gotowe: zalecane konwencje nazewnictwa i tagowania'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ten artykuł zawiera szczegółowe zalecenia dotyczące nazewnictwa zasobów i tagowania mające na celu wsparcie działań związanych z wdrażaniem chmury przedsiębiorstwa.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: 242b397312fe466670d3f1a315059f72447b300b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548838"
---
# <a name="ready-recommended-naming-and-tagging-conventions"></a>Gotowe: zalecane konwencje nazewnictwa i tagowania

Organizowanie elementów zawartości opartych na chmurze w taki sposób, aby ułatwić zarządzanie operacyjne i spełniać wymogi dotyczące księgowania, jest typowym problemem podczas działań związanych z zastosowaniem chmury na dużą skalę. Dzięki zastosowaniu dobrze zdefiniowanych konwencji nazewnictwa i tagowania metadanych do zasobów hostowanych w chmurze pracownicy IT mogą szybko znajdować zasoby i nimi zarządzać. Dobrze zdefiniowane nazwy i tagi pomagają również w dopasowaniu kosztów użycia chmury do zespołów biznesowych przy użyciu mechanizmów obciążenia zwrotnego i księgowania w zakresie przewidywania kosztów.

[Zasady nazewnictwa centrum architektury platformy Azure i ograniczenia dotyczące usługi Azure Resources](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming) zawierają ogólne zalecenia i ograniczenia dotyczące platformy. W omówieniu poniżej rozwinięto te ogólne wytyczne, dodając bardziej szczegółowe zalecenia w celu wspierania działań związanych z wdrażaniem chmury w przedsiębiorstwie.

Zmiana nazw zasobów może być trudna. Przed rozpoczęciem każdego dużego wdrożenia chmury upewnij się, że Twoje zespoły wdrażające chmurę najpierw ustaliły pełną konwencję nazewnictwa.

> [!NOTE]
> Każda firma ma inne wymagania w zakresie organizacji i zarządzania. Zalecenia przedstawione w tym artykule stanowią punkt wyjścia do dyskusji w zespołach wdrażających chmurę.
>
> W trakcie tych dyskusji korzystaj z poniższego szablonu, aby zarejestrować decyzje dotyczące nazewnictwa i tagowania podejmowane podczas dostosowywania tych zaleceń do konkretnych potrzeb firmy.
>
> Pobierz [szablon śledzenia konwencji nazewnictwa i tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Nazewnictwo i tagowanie zasobów

Strategia nazewnictwa i tagowania obejmuje szczegóły biznesowe i operacyjne jako składniki nazw zasobów i tagów metadanych:

- Biznesowy aspekt tej strategii pozwala zapewnić, że nazwy zasobów oraz tagi obejmują informacje organizacyjne konieczne do zidentyfikowania zespołów. Korzystaj z zasobów wraz z właścicielami biznesowymi, którzy odpowiadają za koszty zasobów.
- Aspekt operacyjny zapewnia, że nazwy i tagi zawierają informacje używane przez zespoły informatyczne do identyfikowania obciążenia, aplikacji, środowiska, ważności oraz inne informacje przydatne do zarządzania zasobami.

### <a name="resource-naming"></a>Nazewnictwo zasobów

Skuteczna konwencja nazewnictwa polega na tworzeniu nazw zasobów przez uwzględnienie w nazwie ważnych informacji dotyczących danego zasobu. Na przykład w przypadku użycia zalecanych konwencji nazewnictwa, omówionych [w dalszej części tego artykułu](#sample-naming-convention) zasób publicznego adresu IP dla obciążenia produkcyjnego programu SharePoint otrzymuje następującą nazwę: `pip-sharepoint-prod-westus-001`.

Na podstawie tej nazwy można szybko zidentyfikować typ zasobu, skojarzone z nim obciążenie, jego środowisko wdrożeniowe oraz region świadczenia usługi Azure, w którym jest on hostowany.

#### <a name="naming-scope"></a>Zakres nazewnictwa

Wszystkie typy zasobów platformy Azure mają zakres, który definiuje poziom, którego nazwy zasobów muszą być unikatowe. W swoim zakresie zasób musi mieć unikatową nazwę.

Na przykład sieć wirtualna ma zakres grupy zasobów, co oznacza, że w danej grupie zasobów może istnieć tylko jedna sieć o nazwie `vnet-prod-westus-001`. Inne grupy zasobów mogą mieć własną sieć wirtualną o nazwie `vnet-prod-westus-001`. Innym przykładem są podsieci, które wchodzą w zakres sieci wirtualnych, co oznacza, że każda podsieć w sieci wirtualnej musi mieć unikatową nazwę.

Niektóre nazwy zasobów, takich jak usługi PaaS z publicznymi punktami końcowymi lub etykietami nazw DNS maszyn wirtualnych, mają zakresy globalne, co oznacza, że muszą być unikatowe na całej platformie Azure.

Nazwy zasobów mają limity długości. Jest ważne, aby podczas opracowywania konwencji nazewnictwa zrównoważyć kontekst osadzony w nazwie z jej zakresem i długością. Aby uzyskać więcej informacji o regułach nazewnictwa w zakresie dozwolonych znaków, zakresów i długości nazw dla typów zasobów, zobacz temat [Naming conventions for Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Konwencje nazewnictwa dla zasobów platformy Azure).

#### <a name="recommended-naming-components"></a>Zalecane składniki nazwy

Podczas konstruowania konwencji nazewnictwa zidentyfikuj kluczowe informacje, które mają być odzwierciedlone w nazwie zasobu. Różne informacje są istotne dla różnych typów zasobów. Poniższa lista zawiera przykłady informacji przydatnych podczas konstruowania nazw zasobów.

Składniki nazwy powinny być krótkie, aby zapobiegać przekraczaniu limitów długości nazw zasobów.

| Składnik nazwy | Opis | Przykłady |
| --- | --- | --- |
| Jednostka biznesowa | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach składnik ten może reprezentować pojedynczy korporacyjny element organizacyjny najwyższego poziomu. | *fin*, *mktg*, *product*, *it*, *corp* |
| Typ subskrypcji | Opis podsumowujący przeznaczenie subskrypcji zawierającej zasób. Często składa się z typu środowiska wdrożeniowego lub określonych obciążeń. | *prod,* *shared, client* |
| Nazwa aplikacji lub usługi | Nazwa aplikacji, obciążenia lub usługi, do której należy zasób. | *navigator*, *emissions*, *sharepoint*, *hadoop* |
| Środowisko wdrażania | Etap cyklu życia programowania dla obciążenia obsługiwanego przez zasób. | *prod, dev, qa, stage, test* |
| Region | Region świadczenia usługi Azure, w którym wdrożono zasób. | *westus, eastus2, westeurope, usgovia* |

#### <a name="recommended-resource-type-prefixes"></a>Zalecane prefiksy typów zasobów

Każde obciążenie może składać się z wielu pojedynczych zasobów i usług. Włączenie prefiksów typów zasobów do nazw zasobów ułatwia wizualne identyfikowanie składników aplikacji lub usług.

Poniższa lista zawiera zalecane prefiksy typów zasobów platformy Azure do użycia podczas definiowania konwencji nazewnictwa.

| Typ zasobu                       | Prefiks nazwy zasobu |
| ----------------------------------- | -------------------- |
| Grupa zasobów                      | rg-                  |
| Usługa Azure Virtual Network               | vnet-                |
| Brama sieci wirtualnej             | vnet-gw-             |
| Połączenie bramy                  | cn-                  |
| Podsieć                              | snet-                |
| Sieciowa grupa zabezpieczeń              | nsg-                 |
| Tabela tras                         | Szlak               |
| Azure Virtual Machines              | vm-                  |
| Konto magazynu maszyn wirtualnych                  | stvm                 |
| Publiczny adres IP                           | pip-                 |
| Azure Load Balancer                 | lb-                  |
| Karta sieciowa                                 | nic-                 |
| Azure Key Vault                     | KV                  |
| Azure Kubernetes Service            | AKS                 |
| Azure Service Bus                   | sb-                  |
| Kolejki usługi Azure Service Bus            | sbq-                 |
| Aplikacje usługi Azure App Service              | azapp-               |
| Aplikacje Azure Functions                | azfun-               |
| Azure Cloud Services                | azcs-                |
| Azure SQL Database                  | sqldb-               |
| Azure Cosmos DB (dawniej Azure DocumentDB) | cosdb-               |
| Azure Cache for Redis               | redis-               |
| Azure Database for MySQL            | mysql-               |
| Azure SQL Data Warehouse            | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Azure Storage                       | stor                 |
| Azure StorSimple                    | ssimp                |
| Usługa Azure Search                        | srch-                |
| Azure Cognitive Services            | cs-                  |
| Obszar roboczy usługi Azure Machine Learning    | aml-                 |
| Azure Data Lake Storage             | dls                  |
| Azure Data Lake Analytics           | dla                  |
| Azure HDInsight — Spark             | hdis-                |
| Azure HDInsight — Hadoop            | hdihd-               |
| Azure HDInsight — R Server          | hdir-                |
| Azure HDInsight — HBase             | hdihb-               |
| Usługa Power BI Embedded                   | pbiemb               |
| Usługa Azure Stream Analytics              | asa-                 |
| Azure Data Factory                  | df-                  |
| Azure Event Hubs                    | evh-                 |
| Azure IoT Hub                       | aih-                 |
| Azure Notification Hubs             | anh-                 |
| Przestrzeń nazw usługi Azure Notification Hubs   | anhns-               |

### <a name="metadata-tags"></a>Tagi metadanych

Po zastosowaniu tagów metadanych do zasobów w chmurze można dołączyć informacje o tych elementach zawartości, których nie można było uwzględnić w nazwie zasobu. Te informacje służą do wykonywania bardziej zaawansowanego filtrowania i raportowania zasobów. Tagi te powinny zawierać kontekst dotyczący obciążenia lub aplikacji skojarzonych z zasobem, wymagania operacyjne oraz informacje o własności. Te informacje mogą być używane przez zespoły informatyczne lub biznesowe do odnajdywania zasobów lub generowania raportów dotyczących użycia zasobów i rozliczeń.

Tagi stosowane do zasobów i tagi wymagane lub opcjonalne są różne w różnych organizacjach. Poniższa lista zawiera przykłady typowych tagów przechwytujących ważny kontekst i informacje o zasobach. Użyj tej listy jako punktu wyjścia do ustanowienia własnych konwencji tagowania.

| Nazwa tagu                  | Opis                                                                                                                                                                                                    | Klucz               | Przykładowa wartość                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Nazwa aplikacji          | Nazwa aplikacji, usługi lub obciążenia, z którymi jest skojarzony zasób.                                                                                                                                 | *ApplicationName* | *{nazwa aplikacji}*                                    |
| Nazwa osoby zatwierdzającej             | Osoba odpowiedzialna za zatwierdzenie kosztów związanych z tym zasobem.                                                                                                                                               | *Approver*        | *{e-mail}*                                       |
| Wymagany/zatwierdzony budżet  | Pieniądze przydzielone do tej aplikacji, usługi lub obciążenia.                                                                                                                                                    | *BudgetAmount*    | *{\$}*                                          |
| Jednostka biznesowa             | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. W mniejszych organizacjach ten tag może reprezentować pojedynczy korporacyjny lub współużytkowany element organizacyjny najwyższego poziomu. | *BusinessUnit*    | *FINANSE, MARKETING, {nazwa produktu}, CORP, SHARED* |
| Centrum kosztu               | Księgowe centrum kosztu skojarzone z tym zasobem.                                                                                                                                                          | *CostCenter*      | *{numer}*                                      |
| Odzyskiwanie po awarii         | Ważność aplikacji, obciążenia lub usługi dla działania firmy.                                                                                                                                                | *DR*              | *Mission-critical, Critical, Essential*         |
| Data zakończenia projektu   | Data, na którą zaplanowano wycofanie aplikacji, obciążenia lub usługi.                                                                                                                                  | *EndDate*         | *{data}*                                        |
| Środowisko               | Środowisko wdrażania aplikacji, obciążenia lub usługi.                                                                                                                                              | *Env*             | *Prod, Dev, QA, Stage, Test*                    |
| Nazwa właściciela                | Właściciel aplikacji, obciążenia lub usługi.                                                                                                                                                                | *Właściciel*           | *{e-mail}*                                       |
| Nazwa żądającego            | Użytkownik, który zażądał utworzenia tej aplikacji.                                                                                                                                                          | *Requestor*       | *{e-mail}*                                       |
| Klasa usługi             | Poziom umowy dotyczącej poziomu usług aplikacji, obciążenia lub usługi.                                                                                                                                       | *ServiceClass*    | *Dev, Bronze, Silver, Gold*                     |
| Data rozpoczęcia projektu | Dzień, w którym nastąpiło pierwsze wdrożenie aplikacji, obciążenia lub usługi.                                                                                                                                           | *StartDate*       | *{data}*                                        |

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
| Grupa zasobów | Subskrypcja | rg-\<Nazwa aplikacji / usługi\>-\<Typ subskrypcji\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Sieć wirtualna

| Typ elementu zawartości               | Zakres           | Format                                                                | Przykłady                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Usługa Azure Virtual Network          | Grupa zasobów  | vnet-\<Typ subskrypcji\>-\<Region\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Brama wirtualna sieci wirtualnej     | Sieć wirtualna | vnet-gw-v-\<Typ subskrypcji\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-v-shared-eastus2-001 </li><li>vnet-gw-v-prod-westus-001 </li><li>vnet-gw-v-client-eastus2-001</li></ul>                   |
| Brama lokalna sieci wirtualnej       | Brama wirtualna | vnet-gw-l-\<Typ subskrypcji\>-\<Region\>-\<\#\#\#\>                 | <ul><li>vnet-gw-l-shared-eastus2-001 </li><li>vnet-gw-l-prod-westus-001 </li><li>vnet-gw-l-client-eastus2-001</li></ul>                   |
| Połączenia typu lokacja-lokacja | Grupa zasobów  | cn-\<nazwa bramy lokalnej\>-to-\<nazwa bramy wirtualnej\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Połączenia sieci wirtualnych         | Grupa zasobów  | cn-\<subskrypcja1\>\<region1\>-to-\<subskrypcja2\>\<region2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                     |
| Podsieć                   | Sieć wirtualna | snet-\<subskrypcja\>-\<podregion\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Sieciowa grupa zabezpieczeń   | Podsieć lub karta sieciowa   | nsg-\<nazwa zasad lub nazwa aplikacji\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Publiczny adres IP                | Grupa zasobów  | pip-\<nazwa maszyny wirtualnej lub nazwa aplikacji\>-\<Środowisko\>-\<podregion\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Typ elementu zawartości         | Zakres          | Format                                                              | Przykłady                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Grupa zasobów | vm\<nazwa zasad lub nazwa aplikacji\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Konto magazynu maszyn wirtualnych | Cały świat         | stvm\<typ wydajności\>\<nazwa aplikacji lub nazwa produktu\>\<region\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Etykieta nazwy DNS          | Cały świat         | \<Rekord maszyny wirtualnej\>.[\<region\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Grupa zasobów | lb-\<nazwa aplikacji lub rola\>\<Środowisko\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| Karta sieciowa                | Grupa zasobów | nic-\<\#\#\>-\<nazwa maszyny wirtualnej\>-\<subskrypcja\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>Usługi PaaS

| Typ elementu zawartości     | Zakres  | Format                                                              | Przykłady                                                                                 |
|----------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure App Service    | Cały świat | azapp-\<Nazwa aplikacji\>-\<Środowisko\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azapp-navigator-prod-001.azurewebsites.net </li><li>azapp-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Aplikacja usługi Azure Functions   | Cały świat | azfun-\<Nazwa aplikacji\>-\<Środowisko\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azfun-navigator-prod-001.azurewebsites.net </li><li>azfun-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Cały świat | azcs-\<Nazwa aplikacji\>-\<Środowisko\>-\<\#\#\#\>.[{cloudapp.net}]       | <ul><li>azcs-navigator-prod-001.azurewebsites.net </li><li>azcs-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Typ elementu zawartości         | Zakres       | Format                                                     | Przykłady                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Cały świat      | sb-\<Nazwa aplikacji\>-\<Środowisko\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Kolejki usługi Azure Service Bus | Service Bus | sbq-\<deskryptor kolejki\>                                   | <ul><li>sbq-messagequery</li></ul>                   |

### <a name="databases"></a>Bazy danych

| Typ elementu zawartości                          | Zakres              | Format                                | Przykłady                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL Database                  | Cały świat             | sqldb-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>sqldb-navigator-prod </li><li>sqldb-emissions-dev</li></ul>       |
| Azure Cosmos DB (dawniej DocumentDB) | Cały świat             | cosdb-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>cosdb-navigator-prod </li><li>cosdb-emissions-dev</li></ul>       |
| Azure Cache for Redis               | Cały świat             | redis-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Cały świat             | mysql-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure SQL Data Warehouse                  | Cały świat             | sqldw-\<Nazwa aplikacji\>-\<Środowisko\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | sqlstrdb-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Usługa Storage

| Typ elementu zawartości                              | Zakres  | Format                                                                        | Przykłady                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Konto usługi Azure Storage — zastosowanie ogólne     | Cały świat | st\<nazwa magazynu\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Konto usługi Azure Storage — dzienniki diagnostyczne | Cały świat | stdiag\<pierwsze 2 litery nazwy subskrypcji i numer\>\<region\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                              | Cały świat | ssimp\<Nazwa aplikacji\>\<Środowisko\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>SI i uczenie maszynowe

| Typ elementu zawartości                       | Zakres          | Format                            | Przykłady                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Usługa Azure Search                     | Cały świat         | srch-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services               | Grupa zasobów | cs-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>cs-navigator-prod </li><li>cs-emissions-dev</li></ul>     |
| Obszar roboczy usługi Azure Machine Learning | Grupa zasobów | aml-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>aml-navigator-prod </li><li>aml-emissions-dev</li></ul>   |

### <a name="analytics"></a>Analiza

| Typ elementu zawartości                | Zakres  | Format                             | Przykłady                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Cały świat | df-\<Nazwa aplikacji\>\<Środowisko\>     | <ul><li>df-navigator-prod </li><li>df-emissions-dev</li></ul>       |
| Azure Data Lake Storage   | Cały świat | dls\<Nazwa aplikacji\>\<Środowisko\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Azure Data Lake Analytics | Cały świat | dla\<Nazwa aplikacji\>\<Środowisko\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight — Spark         | Cały świat | hdis-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight — Hadoop        | Cały świat | hdihd-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight — R Server      | Cały świat | hdir-\<Nazwa aplikacji\>-\<Środowisko\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight — HBase         | Cały świat | hdihb-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Usługa Power BI Embedded         | Cały świat | pbiemb\<Nazwa aplikacji\>\<Środowisko\>  | <ul><li>pbiem-navigator-prod </li><li>pbiem-emissions-dev</li></ul> |

### <a name="internet-of-things-iot"></a>Internet rzeczy (IoT)

| Typ elementu zawartości                         | Zakres          | Format                             | Przykłady                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics na urządzeniach brzegowych IoT Edge | Grupa zasobów | asa-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Cały świat         | aih-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>aih-navigator-prod </li><li>aih-emissions-dev</li></ul>     |
| Azure Event Hubs                          | Cały świat         | evh-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs                   | Grupa zasobów | anh-\<Nazwa aplikacji\>-\<Środowisko\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Przestrzeń nazw usługi Azure Notification Hubs         | Cały świat         | anhns-\<Nazwa aplikacji\>-\<Środowisko\> | <ul><li>anhns-navigator-prod </li><li>anhns-emissions-dev</li></ul> |
