---
title: Tworzenie stref wyładunkowych przy użyciu Terraform
description: Dowiedz się, jak tworzyć strefy wyładunkowe przy użyciu Terraform.
author: arnaudlh
ms.author: arnaul
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 8eee7eeaf2406a94ee703054ed5f1b9e369bf5a2
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755656"
---
<!-- cSpell:ignore arnaudlh arnaul Arnaud vCPUs eastasia southeastasia lalogs tfvars -->

# <a name="use-terraform-to-build-your-landing-zones"></a>Tworzenie stref wyładunkowych przy użyciu Terraform

Platforma Azure zapewnia natywne usługi do wdrażania stref wyładunkowej. Inne narzędzia innych firm mogą również pomóc w tym wysiłku. Jednym z tych narzędzi, których klienci i partnerzy często używają do wdrażania stref wyładunkowej, jest HashiCorp Terraform. W tej sekcji pokazano, jak za pomocą przykładowej strefy wyładunkowej wdrożyć funkcje ładu podstawowe, Księgowość i zabezpieczenia dla subskrypcji platformy Azure.

## <a name="purpose-of-the-landing-zone"></a>Przeznaczenie strefy docelowej

Platforma wdrażania w chmurze wykryła, że strefa docelowa dla usługi Terraform udostępnia funkcje do wymuszania rejestrowania, ewidencjonowania aktywności i zabezpieczeń. Ta strefa docelowa korzysta ze standardowych składników znanych jako moduły Terraform, aby wymusić spójność zasobów wdrożonych w środowisku.

## <a name="use-standard-modules"></a>Używanie modułów standardowych

Wielokrotne użycie składników jest podstawową zasadą infrastruktury jako kod. Moduły są w definiowaniu standardów i spójności między wdrożeniem zasobów w środowiskach i między środowiskami. Moduły używane do wdrożenia tej pierwszej strefy docelowej są dostępne w oficjalnym [rejestrze Terraform](https://registry.terraform.io/modules/aztfmod).

## <a name="architecture-diagram"></a>Diagram architektury

Pierwsza strefa początkowa wdraża następujące składniki w ramach subskrypcji:

![Podstawowa strefa przystankowa korzystająca z Terraform](../../_images/ready/foundations-terraform-landing-zone.png)

## <a name="capabilities"></a>Możliwości

Wdrożone składniki i ich przeznaczenie obejmują następujące elementy:

<!-- markdownlint-disable MD033 -->

| Składnik | Odpowiedzialność za |
|---|---|
| Grupy zasobów | Podstawowe grupy zasobów, które są zbędne dla podstawy |
| Dziennik aktywności | Inspekcja wszystkich działań subskrypcji i archiwizowania: <li> Konto magazynu <li> Azure Event Hubs |
| Rejestrowanie diagnostyczne | Wszystkie dzienniki operacji są przechowywane przez określoną liczbę dni: <li> Konto magazynu <li> Event Hubs |
| Log Analytics | Przechowuje wszystkie dzienniki operacji. Wdrażaj popularne rozwiązania w zakresie przeglądu najlepszych rozwiązań dotyczących aplikacji: <li> Networkmonitoring <li> Adassessment <li> Adreplication <li> Agenthealthassessment <li> Dnsanalytics <li> Keyvaultanalytics |
| Azure Security Center | Metryki i alerty dotyczące higieny zabezpieczeń wysyłane do poczty e-mail i numeru telefonu |

<!-- markdownlint-enable MD033 -->

## <a name="use-this-blueprint"></a>Korzystanie z tej strategii

Przed użyciem strefy wyładunkowej programu Cloud proframework Foundation zapoznaj się z następującymi założeniami, decyzjami i wskazówkami dotyczącymi implementacji.

## <a name="assumptions"></a>Założenia

Podczas definiowania początkowej strefy wyładunkowej zostały uwzględnione następujące założenia lub ograniczenia. Jeśli te założenia są zgodne z ograniczeniami, można użyć strategii w celu utworzenia pierwszej strefy docelowej. Strategię można również rozszerzyć, aby utworzyć strategię strefy docelowej, która jest zgodna z unikatowymi ograniczeniami.

- **Limity subskrypcji:** W przypadku tego wysiłku nie można przekroczyć [limitów subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits). Dwa typowe wskaźniki to przekroczenie 25 000 maszyn wirtualnych lub 10 000 procesorów wirtualnych.
- **Zgodność:** Dla tej strefy wyładunkowej nie są wymagane żadne wymagania dotyczące zgodności innych firm.
- **Złożoność architektury:** Złożoność architektury nie wymaga dodatkowych subskrypcji produkcyjnych.
- **Usługi udostępnione:** Na platformie Azure nie ma istniejących usług udostępnionych, które wymagają, aby ta subskrypcja była traktowana jak szprycha w architekturze gwiazdy.

Jeśli te założenia pasują do bieżącego środowiska, ten plan może być dobrym sposobem na rozpoczęcie tworzenia strefy docelowej.

## <a name="design-decisions"></a>Decyzje projektowe

Następujące decyzje są reprezentowane w Terraformej strefie docelowej:

| Składnik              | Decyzje                                                                                                                                                                                                                                                                | Alternatywne podejścia                                                                                                                                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Rejestrowanie i monitorowanie | Azure Monitor Log Analytics obszar roboczy jest używany. Obsługiwane jest konto magazynu diagnostyki oraz centrum zdarzeń.                                                                                                                                                        |                                                                                                                                                                                                                                                                 |
| Sieć                | Nie dotyczy sieci w innej strefie wyładunkowej.                                                                                                                                                                                                                    | [Decyzje dotyczące sieci](../considerations/networking-options.md)                                                                                                                                                                                                 |
| Tożsamość               | Przyjęto założenie, że subskrypcja jest już skojarzona z wystąpieniem usługi Azure Active Directory.                                                                                                                                                                        | [Najlepsze rozwiązania dotyczące zarządzania tożsamościami](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices)                                                                                                                               |
| Zasady                 | W tej strefie wyładunkowej założono, że nie mają być stosowane żadne zasady platformy Azure.                                                                                                                                                                                            |                                                                                                                                                                                                                                                                 |
| Projekt subskrypcji    | N/A — zaprojektowana dla jednej subskrypcji produkcyjnej.                                                                                                                                                                                                                     | [Tworzenie subskrypcji początkowych](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                  |
| Grupy zasobów        | N/A — zaprojektowana dla jednej subskrypcji produkcyjnej.                                                                                                                                                                                                                     | [Skalowanie subskrypcji](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                           |
| Grupy zarządzania      | N/A — zaprojektowana dla jednej subskrypcji produkcyjnej.                                                                                                                                                                                                                     | [Organizuj subskrypcje](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                     |
| Dane                   | Nie dotyczy                                                                                                                                                                                                                                                                      | [Wybierz poprawną opcję SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) i [wskazówki dotyczące usługi Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
| Magazyn                | Nie dotyczy                                                                                                                                                                                                                                                                      | [Wskazówki dotyczące usługi Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                  |
| Standardy nazewnictwa       | Po utworzeniu środowiska tworzony jest również unikatowy prefiks. Zasoby, które wymagają unikatowej nazwy globalnej (na przykład kont magazynu), używają tego prefiksu. Nazwa niestandardowa jest dołączana do losowego sufiksu. Użycie tagów jest wymagane zgodnie z opisem w poniższej tabeli. | [Najlepsze rozwiązania dotyczące nazewnictwa i tagowania](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                              |
| Zarządzanie kosztami        | Nie dotyczy                                                                                                                                                                                                                                                                      | [Śledzenie kosztów](../azure-best-practices/track-costs.md)                                                                                                                                                                                                        |
| Compute                | Nie dotyczy                                                                                                                                                                                                                                                                      | [Opcje obliczeń](../considerations/compute-options.md)                                                                                                                                                                                                         |

### <a name="tagging-standards"></a>Standardy tagowania

Minimalny zestaw tagów przedstawionych poniżej musi być obecny dla wszystkich zasobów i grup zasobów:

| Nazwa tagu          | Opis                                                                                        | Klucz             | Przykładowa wartość                                    |
|-------------------|----------------------------------------------------------------------------------------------------|-----------------|--------------------------------------------------|
| Jednostka biznesowa     | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. | Businessunit    | Finanse, Marketing, {Product Name}, Corp, Shared |
| Centrum kosztu       | Księgowe centrum kosztu skojarzone z tym zasobem.                                              | Costcenter      | Liczba                                           |
| Odzyskiwanie po awarii | Ważność aplikacji, obciążenia lub usługi dla działania firmy.                                     | Routingu              | Funkcja odzyskiwania po awarii, która nie jest dostępna w programie Dr                       |
| Środowisko       | Środowisko wdrażania aplikacji, obciążenia lub usługi.                                   | Env             | Produkcja, dev, pytań i odpowiedzi, etap, test, szkolenia             |
| Nazwa właściciela        | Właściciel aplikacji, obciążenia lub usługi.                                                    | Właściciel           | Poczta e-mail                                            |
| Typ wdrożenia   | Definiuje sposób utrzymywania zasobów.                                                    | Typ wdrożenia  | Ręczne, Terraform                                |
| Wersja           | Wdrożona wersja planu.                                                                 | Wersja         | V 0,1                                             |
| Nazwa aplikacji  | Nazwa skojarzonej aplikacji, usługi lub obciążenia związanego z zasobem.             | ApplicationName | "Nazwa aplikacji"                                       |

<!-- cSpell:ignore caf -->

## <a name="customize-and-deploy-your-first-landing-zone"></a>Dostosowywanie i wdrażanie pierwszej strefy docelowej

Można [sklonować strefę docelową programu Terraform Foundation](https://github.com/azure/caf-terraform-landingzones). Możesz łatwo rozpocząć pracę ze strefą docelową, modyfikując zmienne Terraform. W naszym przykładzie używamy **blueprint_foundations. sandbox. tfvars**, więc Terraform automatycznie ustawia wartości w tym pliku.

Przyjrzyjmy się różnym sekcjom zmiennych.

W tym pierwszym obiekcie tworzymy dwie grupy zasobów w `southeastasia` regionie o nazwie `-hub-core-sec` i `-hub-operations` wraz z prefiksem dodanym w czasie wykonywania.

```hcl
resource_groups_hub = {
    HUB-CORE-SEC    = {
        name = "-hub-core-sec"
        location = "southeastasia"
    }
    HUB-OPERATIONS  = {
        name = "-hub-operations"
        location = "southeastasia"
    }
}
```

Następnie określimy regiony, w których możemy ustawić fundacje. W tym miejscu `southeastasia` służy do wdrażania wszystkich zasobów.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Następnie określamy okres przechowywania dzienników operacji i dzienników subskrypcji platformy Azure. Te dane są przechowywane na oddzielnych kontach magazynu i w centrum zdarzeń, których nazwy są generowane losowo, ponieważ muszą być unikatowe.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

W tags_hub określamy minimalny zestaw znaczników, które są stosowane do wszystkich utworzonych zasobów.

```hcl
tags_hub = {
    environment     = "DEV"
    owner           = "Arnaud"
    deploymentType  = "Terraform"
    costCenter      = "65182"
    BusinessUnit    = "SHARED"
    DR              = "NON-DR-ENABLED"
}
```

Następnie określimy nazwę Log Analytics i zestaw rozwiązań, które analizują wdrożenie. W tym miejscu zachowamy monitorowanie sieci, Active Directory ocenę i replikację, analizę DNS i Key Vault Analytics.

```hcl

analytics_workspace_name = "lalogs"

solution_plan_map = {
    NetworkMonitoring = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/NetworkMonitoring"
    },
    ADAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADAssessment"
    },
    ADReplication = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/ADReplication"
    },
    AgentHealthAssessment = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/AgentHealthAssessment"
    },
    DnsAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/DnsAnalytics"
    },
    KeyVaultAnalytics = {
        "publisher" = "Microsoft"
        "product"   = "OMSGallery/KeyVaultAnalytics"
    }
}

```

Następnie skonfigurujemy parametry alertów dla Azure Security Center.

```hcl
# Azure Security Center Configuration
security_center = {
    contact_email   = "joe@contoso.com"
    contact_phone   = "+6500000000"
}
```

## <a name="get-started"></a>Wprowadzenie

Po przejrzeniu konfiguracji można wdrożyć konfigurację w sposób wdrożony środowisko Terraform. Zalecamy korzystanie z Rover, który jest kontenerem platformy Docker, który umożliwia wdrażanie z systemu Windows, Linux lub macOS. Możesz rozpocząć pracę z [strefami wyładunkowymi](https://github.com/azure/caf-terraform-landingzones).

## <a name="next-steps"></a>Następne kroki

Strefa docelowa programu Foundation określa podstawę dla złożonego środowiska w sposób rozłożony. Ta wersja zawiera zestaw prostych możliwości, które można rozszerzyć, wykonując następujące czynności:

- Dodawanie innych modułów do planu.
- Nakładanie warstwowych dodatkowych stref wyładunkowych na siebie.

Warstwowe strefy ładunkowe są dobrym sposobem na oddzielenie systemów, przechowywanie wersji każdego składnika, którego używasz, a także pozwala na szybkie innowacje i stabilność infrastruktury jako wdrożenie kodu.

Przyszłe architektury referencyjne będą demonstrować koncepcję topologii gwiazdy.

> [!div class="nextstepaction"]
> [Zapoznaj się z przykładem strefy wyładunkowej programu Foundation Terraform](https://github.com/azure/caf-terraform-landingzones)
