---
title: Wdrażanie strefy docelowej migracji na platformie Azure
description: Dowiedz się, jak wdrożyć strefę docelową migracji na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: a76a09e40fc11511213c0f496c9332ba9a05962f
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997840"
---
<!-- cSpell:ignore vCPUs jumpbox -->

# <a name="deploy-a-migration-landing-zone"></a>Wdrażanie strefy docelowej migracji

Termin *strefa docelowa migracji* jest używany do opisania środowiska, które zostało ustanowione i przygotowane do hostowania obciążeń migrowanych ze środowiska lokalnego na platformę Azure.

## <a name="deploy-the-first-landing-zone"></a>Wdrażanie pierwszej strefy docelowej

Przed rozpoczęciem korzystania ze planu strefy wyładunkowej migracji w strukturze wdrażania chmury, należy zapoznać się z następującymi założeniami, decyzjami i zaleceniami dotyczącymi implementacji. Jeśli te wskazówki są zgodne z żądanym planem wdrożenia chmury, plan [strefy wyładunkowej migracji](https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone) można wdrożyć przy użyciu [kroków wdrażania][deploy-sample].

> [!div class="nextstepaction"]
> [Wdróż przykład strategii][deploy-sample]

## <a name="assumptions"></a>Założenia

Ta początkowa strefa początkowa obejmuje następujące założenia lub ograniczenia. Jeśli te założenia są zgodne z ograniczeniami, można użyć strategii w celu utworzenia pierwszej strefy docelowej. Strategię można również rozszerzyć, aby utworzyć strategię strefy docelowej, która jest zgodna z unikatowymi ograniczeniami.

- **Limity subskrypcji:** Nie oczekuje się, że ten nakład pracy nie przekracza [limitów subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits).
- **Zgodność:** W tej strefie wyładunkowej nie są wymagane żadne wymagania dotyczące zgodności innych firm.
- **Złożoność architektury:** Złożoność architektury nie wymaga dodatkowych subskrypcji produkcyjnych.
- **Usługi udostępnione:** Na platformie Azure nie ma istniejących usług udostępnionych, które wymagają, aby ta subskrypcja była traktowana jak szprycha w architekturze gwiazdy.
- **Ograniczony zakres produkcyjny:** Ta strefa docelowa może potencjalnie obsługiwać obciążenia produkcyjne. Nie jest to jednak odpowiednie środowisko do obsługi poufnych danych ani obciążeń o kluczowym znaczeniu.

Jeśli te założenia są zgodne z obecnymi potrzebami dotyczącymi przyjęcia, ten plan może być punktem wyjścia do kompilowania strefy docelowej.

## <a name="decisions"></a>Decyzje

Strategia strefy docelowej odzwierciedla następujące decyzje.

| Składnik                    | Decyzje                                                                                         | Alternatywne podejścia                                                                                                                                                                                                                                                                |
|------------------------------|---------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Narzędzia migracji              | Usługa Azure Site Recovery zostanie wdrożona i utworzony zostanie projekt usługi Azure Migrate.                | [Przewodnik po decyzjach dotyczących narzędzi migracji](../../decision-guides/migrate-decision-guide/index.md)                                                                                                                                                                                               |
| Rejestrowanie i monitorowanie       | Zostanie zainicjowany obszar roboczy usługi Operational Insights i konto magazynu diagnostycznego.                |                                                                                                                                                                                                                                                                                       |
| Sieć                      | Zostanie utworzona sieć wirtualna z podsieciami dla bramy, zapory, serwera przesiadkowego i strefy docelowej.  | [Decyzje dotyczące sieci](../considerations/networking-options.md)                                                                                                                                                                                                                       |
| Tożsamość                     | Przyjęto założenie, że subskrypcja jest już skojarzona z wystąpieniem usługi Azure Active Directory. | [Najlepsze rozwiązania dotyczące zarządzania tożsamościami](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) |
| Zasady                       | W tej strategii założono, że nie mają być stosowane żadne zasady platformy Azure.                        |                                                                                                                                                                                                                                                                                       |
| Projekt subskrypcji          | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej                                              | [Tworzenie subskrypcji początkowych](../azure-best-practices/initial-subscriptions.md)                                                                                                                                                                                                      |
| Grupy zasobów              | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej                                              | [Skalowanie subskrypcji](../azure-best-practices/scale-subscriptions.md)                                                                                                                                                                                                                 |
| Grupy zarządzania            | nd. — zaprojektowana dla jednej subskrypcji produkcyjnej                                              | [Organizowanie subskrypcji i zarządzanie nimi](../azure-best-practices/organize-subscriptions.md)                                                                                                                                                                                                |
| Dane                         | Nie dotyczy                                                                                               | [Wybierz poprawną opcję SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) i [wskazówki dotyczące usługi Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)                       |
| Magazyn                      | Nie dotyczy                                                                                               | [Wskazówki dotyczące usługi Azure Storage](../considerations/storage-options.md)                                                                                                                                                                                                                        |
| Standardy nazewnictwa i tagowania | Nie dotyczy                                                                                               | [Najlepsze rozwiązania dotyczące nazewnictwa i tagowania](../azure-best-practices/naming-and-tagging.md)                                                                                                                                                                                                    |
| Zarządzanie kosztami              | Nie dotyczy                                                                                               | [Śledzenie kosztów](../azure-best-practices/track-costs.md)                                                                                                                                                                                                                              |
| Wystąpienia obliczeniowe                      | Nie dotyczy                                                                                               | [Opcje obliczeń](../considerations/compute-options.md)                                                                                                                                                                                                                               |

## <a name="customize-or-deploy-a-landing-zone"></a>Dostosowywanie lub wdrażanie strefy docelowej

Dowiedz się więcej i Pobierz przykład referencyjny dotyczący migracji planu strefy docelowej dla wdrożenia lub dostosowania z [przykładów Azure Blueprint][deploy-sample].

> [!div class="nextstepaction"]
> [Wdróż przykład strategii][deploy-sample]

Aby uzyskać wskazówki dotyczące dostosowań, które należy wykonać w tym planie lub w rezultacie docelowej strefy, zobacz [zagadnienia dotyczące strefy docelowej](../considerations/index.md).

## <a name="next-steps"></a>Następne kroki

Po wdrożeniu pierwszej strefy docelowej można przystąpić do [rozszerzania strefy docelowej](../considerations/index.md)

> [!div class="nextstepaction"]
> [Rozszerzanie strefy docelowej](../considerations/index.md)

<!-- links -->

[deploy-sample]: https://docs.microsoft.com/azure/governance/blueprints/samples/caf-migrate-landing-zone/deploy
