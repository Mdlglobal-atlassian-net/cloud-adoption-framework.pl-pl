---
title: Tworzenie stref wyładunkowych przy użyciu Terraform
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak tworzyć strefy wyładunkowe przy użyciu Terraform.
author: arnaudlh
ms.author: arnaul
ms.date: 10/16/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 99d5e42f8c7e506ba28617022f2a8076c9501979
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239759"
---
# <a name="use-terraform-to-build-your-landing-zones"></a>Tworzenie stref wyładunkowych przy użyciu Terraform

Platforma Azure zapewnia natywne usługi do wdrażania stref wyładunkowej. Inne narzędzia innych firm mogą również pomóc w tym wysiłku. Jednym z tych narzędzi, które klienci i partnerzy często używają Hashicorp, jest Terraform. W tej sekcji przedstawiono sposób użycia prototypowej strefy docelowej do wdrożenia podstawowych możliwości rejestrowania, ewidencjonowania aktywności i zabezpieczeń dla subskrypcji platformy Azure.

## <a name="purpose-of-the-landing-zone"></a>Przeznaczenie strefy docelowej

Podstawowa strefa wyrzucania w chmurze wdrażania dla usługi Terraform ma ograniczony zestaw obowiązków i funkcji w celu wymuszenia rejestrowania, ewidencjonowania aktywności i zabezpieczeń. Ta strefa docelowa została zaprojektowana, aby wymusić spójność zasobów wdrożonych w środowisku za pomocą standardowych składników znanych jako moduły Terraform.

## <a name="using-standard-modules"></a>Używanie modułów standardowych

Ponowne użycie składników jest podstawową zasadą infrastruktury jako kodu. Moduły są w definiowaniu standardów i spójności między wdrożeniem zasobów w środowiskach i między środowiskami. Zestaw modułów użytych do wdrożenia tej pierwszej strefy docelowej jest dostępny w oficjalnym [rejestrze Terraform](https://registry.terraform.io/search?q=aztfmod).

## <a name="architecture-diagram"></a>Diagram architektury

Pierwsza strefa początkowa wdraża następujące składniki w ramach subskrypcji:

![Strefa docelowa Foundation przy użyciu Terraform](../../_images/ready/foundations-terraform-landingzone.png)

## <a name="capabilities"></a>Możliwości

Wdrożone składniki i ich przeznaczenie obejmują następujące elementy:

| Składnik | odpowiedzialność za |
|---------|---------|
| Grupy zasobów | Podstawowe grupy zasobów, które są zbędne dla podstawy |
| Rejestrowanie aktywności | Inspekcja wszystkich działań subskrypcji i archiwizowania: </br> — Konto magazynu </br> -Event Hubs |  
| Rejestrowanie diagnostyczne | Wszystkie dzienniki operacji są przechowywane przez określoną liczbę dni: </br> — Konto magazynu </br> -Event Hubs |
| Log Analytics | Przechowuje wszystkie dzienniki operacji </br> Wdrażaj popularne rozwiązania w zakresie przeglądu najlepszych rozwiązań dotyczących aplikacji: </br> - NetworkMonitoring </br> - ADAssessment </br> -ADReplication </br> - AgentHealthAssessment </br> - DnsAnalytics </br> - KeyVaultAnalytics
| Security Center | Metryki i alerty dotyczące higieny zabezpieczeń wysyłane do poczty e-mail i numeru telefonu |

## <a name="use-this-blueprint"></a>Korzystanie z tej strategii

Przed użyciem strefy wyładunkowej programu Cloud proframework Foundation zapoznaj się z następującymi założeniami, decyzjami i wskazówkami dotyczącymi implementacji.

## <a name="assumptions"></a>Założenia

Podczas definiowania początkowej strefy wyładunkowej zostały uwzględnione następujące założenia lub ograniczenia. Jeśli te założenia są zgodne z ograniczeniami, można użyć strategii w celu utworzenia pierwszej strefy docelowej. Strategię można również rozszerzyć, aby utworzyć strategię strefy docelowej, która jest zgodna z unikatowymi ograniczeniami.

- **Limity subskrypcji:** W przypadku tego wysiłku nie można przekroczyć [limitów subskrypcji](https://docs.microsoft.com/azure/azure-subscription-service-limits). Dwa typowe wskaźniki to przekroczenie 25 000 maszyn wirtualnych lub 10 000 procesorów wirtualnych.
- **Zgodność:** Dla tej strefy wyładunkowej nie są wymagane żadne wymagania dotyczące zgodności innych firm.
- **Złożoność architektury:** Złożoność architektury nie wymaga dodatkowych subskrypcji produkcyjnych.
- **Usługi udostępnione:** Na platformie Azure nie ma istniejących usług udostępnionych, które wymagają, aby ta subskrypcja była traktowana jak szprycha w architekturze gwiazdy.

Jeśli te założenia pasują do bieżącego środowiska, ten plan może być dobrym sposobem na rozpoczęcie tworzenia strefy docelowej.

## <a name="design-decisions"></a>Decyzje projektowe

Następujące decyzje są reprezentowane w Terraformej strefie docelowej:

| Składnik | Decyzje | Alternatywne podejścia |
| --- | --- | --- |
|Rejestrowanie i monitorowanie | Zostanie użyty obszar roboczy Azure Monitor Log Analytics. Zostanie zainicjowana obsługa konta magazynu diagnostyki oraz centrum zdarzeń. |         |
|Sieć | N/A — sieć zostanie wdrożona w innej strefie docelowej. |[Decyzje dotyczące sieci](../considerations/networking-options.md) |
|Tożsamość | Przyjęto założenie, że subskrypcja jest już skojarzona z wystąpieniem usługi Azure Active Directory. | [Najlepsze rozwiązania dotyczące zarządzania tożsamościami](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) |
| Zasady | W tej strefie wyładunkowej założono, że nie mają być stosowane żadne zasady platformy Azure. | |
|Projekt subskrypcji | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej | [Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md) |
| Grupy zarządzania | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej |[Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md) |
| Grupy zasobów | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej | [Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md) |
| Dane | ND | [Wybierz poprawną opcję SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) i [wskazówki dotyczące usługi Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Usługa Storage|ND|[Wskazówki dotyczące usługi Azure Storage](../considerations/storage-options.md) |
| Standardy nazewnictwa | Po utworzeniu środowiska zostanie również utworzony unikatowy prefiks. Zasoby, które wymagają unikatowej nazwy globalnej (na przykład kont magazynu), używają tego prefiksu. Nazwa niestandardowa zostanie dołączona z losowym sufiksem. Użycie tagów jest wymagane zgodnie z opisem w poniższej tabeli. | [Najlepsze rozwiązania dotyczące nazewnictwa i tagowania](../azure-best-practices/naming-and-tagging.md) |
| Zarządzanie kosztami | ND | [Śledzenie kosztów](../azure-best-practices/track-costs.md) |
| Wystąpienia obliczeniowe | ND | [Opcje środowiska obliczeniowego](../considerations/compute-options.md) |

### <a name="tagging-standards"></a>Standardy tagowania

Następujący zestaw minimalnych tagów musi być obecny dla wszystkich zasobów i grup zasobów:

| Nazwa tagu | Opis | Klucz | Przykładowa wartość |
|--|--|--|--|
| Jednostka biznesowa | Wydział firmy najwyższego poziomu będący właścicielem subskrypcji lub obciążenia, do których należy zasób. | BusinessUnit | FINANSe, MARKETING, {Product Name}, CORP, SHARED |
| Cost Center | Księgowe centrum kosztu skojarzone z tym zasobem.| CostCenter | Liczba |
| Odzyskiwanie po awarii | Ważność aplikacji, obciążenia lub usługi dla działania firmy. | ROUTINGU | FUNKCJA ODZYSKIWANIA PO AWARII, KTÓRA NIE JEST DOSTĘPNA W PROGRAMIE DR |
| Środowisko | Środowisko wdrażania aplikacji, obciążenia lub usługi. |  Kopert | Produkcja, dev, pytań i odpowiedzi, etap, test, szkolenia |
| Nazwa właściciela | Właściciel aplikacji, obciążenia lub usługi.| Właściciel | e-mail |
| Typ wdrożenia | Definiuje sposób utrzymywania zasobów. | Typ wdrożenia | Ręczne, Terraform |
| Wersja | Wersja wdrożonego planu | version | v 0,1 |
| Nazwa aplikacji | Nazwa skojarzonej aplikacji, usługi lub obciążenia związanego z zasobem. | ApplicationName | "Nazwa aplikacji" |

## <a name="customize-and-deploy-your-first-landing-zone"></a>Dostosowywanie i wdrażanie pierwszej strefy docelowej

Można [sklonować strefę docelową programu Terraform Foundation](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready). Rozpoczęcie pracy z strefą docelową jest łatwe, modyfikując zmienne Terraform. W naszym przykładzie używamy **blueprint_foundations. sandbox. tfvars**, więc Terraform automatycznie ustawi wartości w tym pliku.

Przyjrzyjmy się różnym sekcjom zmiennych.

W tym pierwszym obiekcie tworzymy dwie grupy zasobów w `southeastasia` regionie o nazwie "-Hub-Core-sek" i "-Hub-Core-s" wraz z prefiksem dodanym w czasie wykonywania.

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

Następnie określimy regiony, w których możemy ustawić fundacje. W tym miejscu `southeastasia` zostanie użyty do wdrożenia wszystkich zasobów.

```hcl
location_map = {
    region1   = "southeastasia"
    region2   = "eastasia"
}
```

Następnie określamy okres przechowywania dzienników operacji i dzienników subskrypcji platformy Azure. Te dane będą przechowywane na oddzielnych kontach magazynu i w centrum zdarzeń, których nazwy są generowane losowo, ponieważ muszą być unikatowe.

```hcl
azure_activity_logs_retention = 365
azure_diagnostics_logs_retention = 60
```

W tags_hub określamy minimalny zestaw znaczników, które zostaną zastosowane do wszystkich utworzonych zasobów.

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

Następnie podaj nazwę usługi log Analytics i zestaw rozwiązań, które będą analizować wdrożenie. W tym miejscu zachowamy monitorowanie sieci, AD Assessment i replikację, DNS Analytics i Key Vault Analytics.

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

## <a name="getting-started"></a>Wprowadzenie

Po przejrzeniu konfiguracji można wdrożyć konfigurację w sposób wdrożony środowisko Terraform. Zaleca się jednak korzystanie z Rover, który jest kontenerem platformy Docker, który umożliwia wdrażanie z systemu Windows, Linux lub MacOS. Możesz rozpocząć pracę z [repozytorium GitHub Rover](https://github.com/aztfmod/rover).

## <a name="next-steps"></a>Następne kroki

Strefa docelowa programu Foundation określa podstawę dla złożonego środowiska w sposób rozłożony. Ta wersja zawiera zestaw bardzo prostych możliwości, które można rozszerzyć, wykonując następujące czynności:

- Dodawanie innych modułów do planu.
- Nakładanie warstwowych dodatkowych stref wyładunkowych na siebie.

Warstwowe strefy ładunkowe są dobrym sposobem na oddzielenie systemów, przechowywanie wersji każdego używanego składnika i umożliwienie szybkiego innowacji i stabilności w ramach wdrożenia infrastruktury jako kodu.

Przyszłe architektury referencyjne będą demonstrować koncepcję topologii gwiazdy.

> [!div class="nextstepaction"]
> [Zapoznaj się z przykładem strefy wyładunkowej Foundation przy użyciu Terraform](https://github.com/microsoft/CloudAdoptionFramework/tree/master/ready)
