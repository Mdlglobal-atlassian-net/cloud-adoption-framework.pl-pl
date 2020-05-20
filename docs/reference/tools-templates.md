---
title: Narzędzia i szablony
description: Znajdź narzędzia i szablony, które są dostępne w strukturze wdrażania w chmurze, aby ułatwić przyspieszenie wdrożenia chmury.
author: JanetCThomas
ms.author: janet
ms.date: 04/14/2020
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.topic: article
ms.openlocfilehash: eda7866700edb0a1e86776f1b0f23d95799d5b67
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621580"
---
<!-- cSpell:ignore Terraform's -->

# <a name="tools-and-templates"></a>Narzędzia i szablony

Struktura wdrażania w chmurze zawiera narzędzia, które ułatwiają szybkie wdrażanie zmian technicznych. Użyj tych narzędzi, szablonów i ocen, aby przyspieszyć wdrażanie chmury. Poniższe zasoby mogą pomóc w każdej fazie wdrażania. Niektóre narzędzia i szablony mogą być używane w wielu fazach.

## <a name="strategy"></a>Strategia

| Zasób | Opis |
|----------|-------------|
| [Monitor przejścia do chmury](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Zidentyfikuj ścieżkę wdrażania chmury dopasowaną do potrzeb Twojej firmy. |
| [Strategia &nbsp; i &nbsp; &nbsp; szablon planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Udokumentowanie decyzji w trakcie wykonywania strategii i planu wdrażania w chmurze. |

## <a name="plan"></a>Planowanie

| Zasób | Opis |
|----------|-------------|
| [Monitor przejścia do chmury](https://docs.microsoft.com/assessments/?mode=pre-assessment&id=cloud-journey-tracker) | Zidentyfikuj ścieżkę wdrażania chmury dopasowaną do potrzeb Twojej firmy. |
| [Strategia &nbsp; i &nbsp; &nbsp; szablon planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) | Udokumentowanie decyzji w trakcie wykonywania strategii i planu wdrażania w chmurze. |
| [Generator planu wdrażania chmury](../plan/template.md) | Normalizuj procesy, wdrażając zaległości do [Azure Boards](https://docs.microsoft.com/azure/devops/boards/get-started/what-is-azure-boards) przy użyciu szablonu planu wdrażania w chmurze. |

## <a name="ready"></a>Gotowy

| Zasób | Opis |
|----------|-------------|
| [Lista kontrolna gotowości](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/ready/readiness-checklist.docx) | Ta lista kontrolna służy do przygotowywania środowiska do zastosowania, w tym przygotowywania pierwszej strefy docelowej migracji, personalizowania strategii i jej rozszerzania. |
| [Szablon śledzenia nazewnictwa i tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) | Udokumentowanie decyzji o standardach nazewnictwa i znakowania w celu zapewnienia spójności i skrócenia czasu dołączenia. |
| [&nbsp;Plan CAF Foundation &nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Korzystaj z uproszczonej implementacji początkowego ładu, aby zapewnić praktyczne środowisko przy użyciu narzędzi do zarządzania na platformie Azure. |
| [Plan strefy docelowej migracji CAF](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone) | Udostępnianie i przygotowanie do obsługi obciążeń, które są migrowane z środowiska lokalnego do platformy Azure. Aby uzyskać więcej informacji na temat tego planu, zobacz [wdrażanie strefy wyładunkowej migracji](../ready/landing-zone/migrate-landing-zone.md). |
| [Terraform plan strefy ładunkowej](../ready/landing-zone/terraform-landing-zone.md) | Baza kodu typu open source dla wersji Terraform planów strefy ładunkowej CAF. |
| [Rejestr Terraform](https://registry.terraform.io/search?q=aztfmod) | Witryna sieci Web rejestru Terraform, przefiltrowana w celu wyświetlenia listy wszystkich modułów struktury wdrażania chmury, które są konieczne do utworzenia strefy docelowej Terraform. |

## <a name="govern"></a>Ład

| Zasób | Opis |
|----------|-------------|
| [Ocena testu porównawczego](https://cafbaseline.com) | Znajdź różnice między stanem bieżącym a priorytetami biznesowymi i uzyskaj odpowiednie zasoby, aby je zniwelować. |
| [&nbsp;Plan CAF Foundation &nbsp;](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/ready/migration-landing-zone-governance) | Lekka implementacja początkowego ładu, aby zapewnić praktyczne środowisko dotyczące narzędzi ładu na platformie Azure. |
| [Szablon procesu ładu](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Governance%20Discipline%20Template.docx) | Zdefiniuj podstawowy zestaw procesów ładu wykorzystywanych do wymuszania każdej dyscypliny ładu. |
| [Szablon procesu zarządzania kosztami](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Cost%20Management%20Discipline%20Template.docx) | Zdefiniuj instrukcje zasad i wskazówki dotyczące projektowania, które umożliwiają przedwczesne zarządzanie chmurą w organizacji i skoncentrowanie się na zarządzaniu kosztami. |
| [Szablon procesu przyspieszania wdrażania](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Deployment%20Acceleration%20Discipline%20Template.docx) | Zdefiniuj instrukcje zasad i wskazówki dotyczące projektowania, które umożliwiają przedwczesne zarządzanie chmurą w organizacji z fokusem na przyspieszeniu wdrażania. |
| [Szablon procesu tożsamości](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Identity%20Baseline%20Discipline%20Template.docx) | Zdefiniuj instrukcje zasad i wskazówki dotyczące projektowania, które umożliwiają przedwczesne zarządzanie chmurą w organizacji z uwzględnieniem wymagań dotyczących tożsamości. |
| [Szablon procesu spójności zasobów](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Resource%20Consistency%20Discipline%20Template.docx) | Zdefiniuj instrukcje zasad i wskazówki dotyczące projektowania, które umożliwiają przedwczesne zarządzanie chmurą w organizacji i skoncentrowanie się na spójności zasobów. |
| [Szablon procesu odniesienia zabezpieczeń](https://archcenter.blob.core.windows.net/cdn/fusion/governance/Security%20Baseline%20Discipline%20Template.docx) | Zdefiniuj instrukcje zasad i wskazówki dotyczące projektowania, które umożliwiają przedwczesne zarządzanie chmurą w organizacji z uwzględnieniem podstawy zabezpieczeń. |

## <a name="manage"></a>Zarządzanie

| Zasób | Opis |
|----------|-------------|
| [Przegląd architektury platformy Azure](https://docs.microsoft.com/assessments/?id=azure-architecture-review) | Ta ocena online pomoże w definiowaniu architektury i opcji operacji specyficznych dla obciążenia. |
| [&nbsp; &nbsp; Kod źródłowy najlepszych &nbsp; rozwiązań](https://github.com/Microsoft/CloudAdoptionFramework/tree/master/manage/Automation-Best-Practices) | Ten wdrożony kod źródłowy uzupełnia i przyspiesza wdrażanie najlepszych rozwiązań dla usług zarządzania serwerem Azure. Użyj tego kodu źródłowego, aby szybko włączyć zarządzanie operacjami i ustalić linię bazową operacji. |
| [Skoroszyt zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) | Udokumentowanie decyzji dotyczących zarządzania operacjami w chmurze oraz ułatwianie konwersacji z firmą w celu zapewnienia wyrównania dotyczącego umowy SLA, inwestycji w odporności i alokacji budżetu związanych z operacjami. |

## <a name="organize"></a>Organizowanie

| Zasób | Opis |
|----------|-------------|
| [Diagram RACI między zespołami](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx) | Pobierz i zmodyfikuj szablon arkusza kalkulacyjnego RACI, aby śledzić decyzje dotyczące struktury organizacyjnej w miarę upływu czasu. |
