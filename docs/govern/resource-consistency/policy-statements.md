---
title: Instrukcje dotyczące przykładowych zasad spójności zasobów
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Instrukcje dotyczące przykładowych zasad spójności zasobów
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f2e15ad1640bec4e289c49a1f9dcf83de7c04ec3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221983"
---
# <a name="resource-consistency-sample-policy-statements"></a>Instrukcje dotyczące przykładowych zasad spójności zasobów

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te instrukcje powinny dostarczyć zwięzłe podsumowanie zagrożeń i plany postępowania z nimi. Każda definicja instrukcji powinna zawierać następujące informacje:

- **Ryzyko techniczne:** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad:** Jasne wyjaśnienie wymagań zasad.
- **Opcje projektowania:** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki, które mogą być używane przez zespoły IT i deweloperów podczas implementowania zasad.

Poniższe przykładowe instrukcje dotyczące zasad umożliwiają rozwiązywanie typowych zagrożeń firmy związanych ze spójnością zasobów. Te instrukcje są przykładami, które można przywołać podczas sporządzania projektów instrukcji zasad w celu rozwiązania potrzeb organizacji. Te przykłady nie są przeznaczone do obsługi skryptów i mogą być dostępne różne opcje dotyczące ponoszenia określonych zagrożeń. Ścisła współpraca z firmowymi i zespołami IT w celu zidentyfikowania najlepszych zasad dla unikatowego zestawu zagrożeń.

## <a name="tagging"></a>Znakowanie

**Ryzyko techniczne:** Bez odpowiedniego tagowania metadanych skojarzonego ze wdrożonymi zasobami operacje IT nie mogą określać priorytetu pomocy technicznej lub optymalizacji zasobów w zależności od wymaganej umowy SLA, ważności operacji biznesowej lub kosztów operacyjnych. Może to spowodować błędną alokację zasobów IT oraz potencjalne opóźnienia w rozwiązywaniu problemów.

**Instrukcja zasad:** Następujące zasady zostaną zaimplementowane:

- Wdrożone zasoby powinny być znakowane przy użyciu następujących wartości:
  - Koszt
  - Zagrożenia
  - Umowa SLA
  - Środowisko
- Narzędzia ładu muszą sprawdzać poprawność tagowania związanego z kosztami, krytycznością, umową SLA, aplikacją i środowiskiem. Wszystkie wartości muszą być wyrównane do wstępnie zdefiniowanych wartości zarządzanych przez zespół nadzoru.

**Potencjalne opcje projektu:** Na platformie Azure [Tagi metadanych standardowej wartości nazwy](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) są obsługiwane w przypadku większości typów zasobów. [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) służy do wymuszania określonych tagów w ramach tworzenia zasobów.

## <a name="ungoverned-subscriptions"></a>Nieregulowane subskrypcje

**Ryzyko techniczne:** Arbitralne Tworzenie subskrypcji i grup zarządzania może prowadzić do izolowanych sekcji nieruchomości w chmurze, które nie podlegają prawidłowym zasadom zarządzania.

**Instrukcja zasad:** Tworzenie nowych subskrypcji lub grup zarządzania dla wszystkich aplikacji o znaczeniu krytycznym lub chronionych danych będzie wymagało przeglądu od zespołu zarządzającego chmurą. Zatwierdzone zmiany zostaną zintegrowane z odpowiednim przypisaniem strategii.

**Potencjalne opcje projektu:** Zablokuj dostęp administracyjny do [grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups) organizacji do zatwierdzonych członków zespołu ładu, którzy będą kontrolować proces tworzenia subskrypcji i kontroli dostępu.

## <a name="manage-updates-to-virtual-machines"></a>Zarządzanie aktualizacjami maszyn wirtualnych

**Ryzyko techniczne:** Maszyny wirtualne, które nie są aktualne wraz z najnowszymi aktualizacjami i poprawkami oprogramowania, są narażone na problemy z bezpieczeństwem lub wydajnością, co może spowodować zakłócenia w działaniu usługi.

**Instrukcja zasad:** Narzędzia ładu muszą wymusić włączenie aktualizacji automatycznych na wszystkich wdrożonych maszynach wirtualnych. Naruszenia muszą zostać sprawdzone za pomocą zespołów zarządzania operacyjnego i korygowane zgodnie z zasadami operacji. Zasoby, które nie są automatycznie aktualizowane, muszą być uwzględnione w procesach należących do operacji IT.

**Potencjalne opcje projektu:** W przypadku hostowanych maszyn wirtualnych platformy Azure Możesz zapewnić spójne zarządzanie aktualizacjami przy użyciu [rozwiązania Update Management w Azure Automation](https://docs.microsoft.com/azure/automation/automation-update-management).

## <a name="deployment-compliance"></a>Zgodność wdrożenia

**Ryzyko techniczne:** Skrypty wdrażania i narzędzia automatyzacji, które nie są w pełni zbadane przez zespół ds. zarządzania chmurą, mogą spowodować wdrożenia zasobów, które naruszają zasady.

**Instrukcja zasad:** Następujące zasady zostaną zaimplementowane:

- Narzędzia do wdrażania muszą zostać zatwierdzone przez zespół ds. zarządzania chmurą, aby zapewnić ciągły nadzór nad wdrożonymi zasobami.
- Skrypty wdrażania muszą być utrzymywane w centralnym repozytorium dostępnym dla zespołu ładu chmury w celu okresowego przeglądania i inspekcji.

**Potencjalne opcje projektu:** Spójne korzystanie z [planów platformy Azure](https://docs.microsoft.com/azure/governance/blueprints) do zarządzania zautomatyzowanymi wdrożeniami pozwala na spójne wdrożenia zasobów platformy Azure, które są zgodne ze standardami i zasadami zarządzania obowiązującymi w organizacji.

## <a name="monitoring"></a>Monitorowanie

**Ryzyko techniczne:** Nieprawidłowo zaimplementowane lub niespójne monitorowanie oprzyrządowania może uniemożliwić wykrywanie problemów z kondycją obciążeń lub innych naruszeń zasad.

**Instrukcja zasad:** Następujące zasady zostaną zaimplementowane:

- Narzędzia ładu muszą sprawdzać, czy wszystkie zasoby są uwzględniane w monitorowaniu dla niszczenia zasobów, zabezpieczeń, zgodności i optymalizacji.
- Narzędzia ładu muszą sprawdzić, czy odpowiedni poziom danych rejestrowania jest zbierany dla wszystkich aplikacji i danych.

**Potencjalne opcje projektu:** [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) jest domyślną usługą monitorowania na platformie Azure, a spójne monitorowanie można wymusić za pośrednictwem [planów platformy Azure](https://docs.microsoft.com/azure/governance/blueprints) podczas wdrażania zasobów.

## <a name="disaster-recovery"></a>Odzyskiwanie po awarii

**Ryzyko techniczne:** Awaria zasobów, usuwanie lub uszkodzenie może spowodować zakłócenie aplikacji lub usług o znaczeniu krytycznym, a także utratę poufnych danych.

**Instrukcja zasad:** Wszystkie aplikacje o kluczowym znaczeniu i chronione dane muszą mieć wdrożone rozwiązania do tworzenia kopii zapasowych i odzyskiwania, aby zminimalizować wpływ awarii na firmę lub awarie systemu.

**Potencjalne opcje projektu:** Usługa [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) udostępnia funkcje tworzenia kopii zapasowej, odzyskiwania i replikacji, które minimalizują czas przestoju w scenariuszach ciągłości biznesowej i odzyskiwania po awarii (BCDR).

## <a name="next-steps"></a>Następne kroki

Skorzystaj z przykładów przedstawionych w tym artykule jako punktu wyjścia do opracowania zasad, które wiążą się z konkretnymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania w chmurze.

Aby rozpocząć tworzenie własnych niestandardowych instrukcji zasad związanych ze spójnością zasobów, Pobierz [szablon spójności zasobów](./template.md).

Aby przyspieszyć wdrażanie tego dyscypliny, wybierz [Przewodnik dotyczący ładu](../guides/index.md) z możliwością działania, który najlepiej odpowiada Twojemu środowisku. Następnie zmodyfikuj projekt, aby uwzględnić określone decyzje dotyczące zasad firmowych.

Opracowywanie zagrożeń i odporności, ustanawianie procesu do zarządzania zasadami spójności zasobów i ich komunikacji.

> [!div class="nextstepaction"]
> [Ustanawianie procesów zgodności z zasadami](./compliance-processes.md)
