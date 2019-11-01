---
title: Wdrażanie strefy docelowej migracji na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak wdrożyć strefę docelową migracji na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit
ms.openlocfilehash: b3adddc6b68d07084ec8c3909d6c8010c25bb387
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73239855"
---
# <a name="deploy-a-migration-landing-zone"></a>Wdrażanie strefy docelowej migracji

Termin *strefa docelowa migracji* jest używany do opisania środowiska, które zostało ustanowione i przygotowane do hostowania obciążeń migrowanych ze środowiska lokalnego na platformę Azure. Strefa docelowa migracji to ostateczny element dostarczany przewodnika Instalatora platformy Azure. Ten artykuł łączy ze sobą wszystkie tematy dotyczące gotowości omówione w tym przewodniku i stosuje podjęte decyzje do wdrożenia pierwszej strefy docelowej migracji.

W poniższych sekcjach opisano strefę docelową używaną często do ustanowienia środowiska odpowiedniego do użycia podczas migracji. Środowisko lub strefa docelowa opisana w tym artykule jest uwzględniona również w strategii platformy Azure. Strategia strefy docelowej migracji w strukturze wdrażania chmury umożliwia wdrożenie zdefiniowanego środowiska za pomocą jednego kliknięcia.

## <a name="purpose-of-the-blueprint"></a>Przeznaczenie strategii

Strategia strefy docelowej migracji w strukturze wdrażania chmury powoduje utworzenie strefy docelowej. Ta strefa docelowa jest celowo ograniczona. Zaprojektowano ją w celu utworzenia spójnego punktu początkowego, który zapewnia przestrzeń do nauki infrastruktury jako kodu. W przypadku niektórych procesów migracji ta strefa docelowa może być wystarczająca do spełnienia Twoich wymagań. Prawdopodobnie konieczna będzie zmiana pewnych elementów strategii w celu spełnienia unikatowych ograniczeń.

## <a name="blueprint-alignment"></a>Dostosowywanie strategii

Na poniższej ilustracji przedstawiono strategię strefy docelowej migracji w strukturze wdrażania chmury w odniesieniu do wymagań dotyczących złożoności i zgodności architektury.

![Dostosowywanie strategii](../../_images/ready/blueprint-overview.png)

- Litera A znajduje po wewnętrznej stronie zakrzywionej linii, która oznacza zakres tej strategii. Ten zakres informuje, że strategia obejmuje ograniczoną złożoność architektury, ale jest oparta na względnie średnich wymaganiach dotyczących zgodności.
- Dla klientów, którzy mają architekturę o wysokim stopniu złożoności i rygorystyczne wymagania w zakresie zgodności, bardziej odpowiednie będzie użycie rozszerzonej strategii partnera lub jednego z [przykładów strategii opartych na standardach](https://docs.microsoft.com/azure/governance/blueprints/samples).
- Potrzeby większości klientów znajdują się między tymi dwoma skrajnymi przypadkami. Litera B reprezentuje proces opisany w artykułach na temat [zagadnień dotyczących strefy docelowej](../considerations/index.md). W przypadku klientów w tym obszarze można skorzystać ze wskazówek dotyczących podejmowania decyzji znajdujących się w tych artykułach, aby zidentyfikować węzły, które należy dodać do strategii strefy docelowej migracji w strukturze wdrażania chmury. Takie podejście umożliwia dostosowanie strategii do potrzeb.

## <a name="use-this-blueprint"></a>Korzystanie z tej strategii

Przed rozpoczęciem korzystania ze strategii strefy docelowej migracji w strukturze wdrażania chmury zapoznaj się z założeniami, decyzjami i wskazówkami dotyczącymi wdrażania.

## <a name="assumptions"></a>Założenia

Podczas definiowania tej początkowej strefy docelowej przyjęto następujące założenia i ograniczenia. Jeśli te założenia są zgodne z ograniczeniami, można użyć strategii w celu utworzenia pierwszej strefy docelowej. Strategię można również rozszerzyć, aby utworzyć strategię strefy docelowej, która jest zgodna z unikatowymi ograniczeniami.

- **Limity subskrypcji:** Nie oczekuje się, że ten nakład pracy nie przekracza [limitów subskrypcji](https://docs.microsoft.com/azure/azure-subscription-service-limits). Dwa typowe wskaźniki to przekroczenie 25 000 maszyn wirtualnych lub 10 000 procesorów wirtualnych.
- **Zgodność:** W tej strefie wyładunkowej nie są wymagane żadne wymagania dotyczące zgodności innych firm.
- **Złożoność architektury:** Złożoność architektury nie wymaga dodatkowych subskrypcji produkcyjnych.
- **Usługi udostępnione:** Na platformie Azure nie ma istniejących usług udostępnionych, które wymagają, aby ta subskrypcja była traktowana jak szprycha w architekturze gwiazdy.

Jeśli te założenia są dostosowane do bieżącego środowiska, ta strategia może być dobrym punktem wyjściowym do tworzenia strefy docelowej.

## <a name="decisions"></a>Decyzje

Strategia strefy docelowej odzwierciedla następujące decyzje.

| Składnik | Decyzje | Alternatywne podejścia |
|---------|---------|---------|
|Narzędzia migracji|Usługa Azure Site Recovery zostanie wdrożona i utworzony zostanie projekt usługi Azure Migrate.|[Przewodnik po decyzjach dotyczących narzędzi do migracji](../../decision-guides/migrate-decision-guide/index.md)|
|Rejestrowanie i monitorowanie|Zostanie zainicjowany obszar roboczy usługi Operational Insights i konto magazynu diagnostycznego.|         |
|Sieć|Zostanie utworzona sieć wirtualna z podsieciami dla bramy, zapory, serwera przesiadkowego i strefy docelowej.|[Decyzje dotyczące sieci](../considerations/networking-options.md)|
|Tożsamość|Przyjęto założenie, że subskrypcja jest już skojarzona z wystąpieniem usługi Azure Active Directory.|[Najlepsze rozwiązania dotyczące zarządzania tożsamościami](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)         |
|Zasady|W tej strategii założono, że nie mają być stosowane żadne zasady platformy Azure.|         |
|Projekt subskrypcji|nd. — zaprojektowana dla jednej subskrypcji produkcyjnej|[Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md)|
|Grupy zarządzania|nd. — zaprojektowana dla jednej subskrypcji produkcyjnej|[Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md)         |
|Grupy zasobów|nd. — zaprojektowana dla jednej subskrypcji produkcyjnej|[Skalowanie subskrypcji](../azure-best-practices/scaling-subscriptions.md)         |
|Dane|ND|[Wybierz poprawną opcję SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/architecture/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) i [wskazówki dotyczące usługi Azure Data Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Usługa Storage|ND|[Wskazówki dotyczące usługi Azure Storage](../considerations/storage-options.md)         |
|Standardy nazewnictwa i tagowania|ND|[Najlepsze rozwiązania dotyczące nazewnictwa i tagowania](../azure-best-practices/naming-and-tagging.md)         |
|Zarządzanie kosztami|ND|[Śledzenie kosztów](../azure-best-practices/track-costs.md)|
|Wystąpienia obliczeniowe|ND|[Opcje środowiska obliczeniowego](../considerations/compute-options.md)|

## <a name="customize-or-deploy-a-landing-zone-from-this-blueprint"></a>Dostosowywanie lub wdrażanie strefy docelowej przy użyciu tej strategii

Dowiedz się więcej i Pobierz przykład referencyjny struktury wdrażania w chmurze Migrowanie planu strefy ładunkowej w celu wdrożenia lub dostosowania z [przykładów planów platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/samples).

Przykłady strategii są również dostępne w portalu. Aby uzyskać szczegółowe informacje na temat sposobu tworzenia planu, zobacz [Azure Plans](./govern-org-compliance.md?tabs=azureblueprints#create-a-blueprint).

Aby uzyskać wskazówki dotyczące dostosowywania tej strategii lub utworzonej strefy docelowej, zobacz artykuły na temat [zagadnień dotyczących strefy docelowej](../considerations/index.md).

## <a name="next-steps"></a>Następne kroki

Po wdrożeniu strefy docelowej migracji można przystąpić do migracji obciążeń na platformę Azure.
Aby uzyskać wskazówki dotyczące narzędzi i procesów, które są wymagane do przeprowadzenia migracji pierwszego obciążenia, zobacz [Przewodnik po migracji na platformę Azure](../../migrate/azure-migration-guide/index.md).

> [!div class="nextstepaction"]
> [Migrowanie pierwszego obciążenia za pomocą przewodnika po migracji na platformę Azure](../../migrate/azure-migration-guide/index.md)
