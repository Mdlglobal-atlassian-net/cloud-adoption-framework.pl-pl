---
title: Przykładowe instrukcje dotyczące zasad przyspieszania wdrażania
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przykładowe instrukcje dotyczące zasad przyspieszania wdrażania
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4a2b1666332ca884dfb95b2b2372f3b5518bd635
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026565"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Przykładowe instrukcje dotyczące zasad przyspieszania wdrażania

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te instrukcje powinny dostarczyć zwięzłe podsumowanie zagrożeń i plany postępowania z nimi. Każda definicja instrukcji powinna zawierać następujące informacje:

- **Ryzyko techniczne.** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad.** Jasne wyjaśnienie wymagań zasad.
- **Opcje projektowania.** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki, które mogą być używane przez zespoły IT i deweloperów podczas implementowania zasad.

Poniższe przykładowe instrukcje dotyczące zasad dotyczą typowych zagrożeń firmy związanych z konfiguracją. Te instrukcje są przykładami, które można przywołać podczas sporządzania projektów instrukcji zasad w celu rozwiązania potrzeb organizacji. Te przykłady nie są przeznaczone do obsługi skryptów i mogą być dostępne różne opcje dotyczące ponoszenia określonych zagrożeń. Ścisła współpraca z firmowymi i zespołami IT w celu zidentyfikowania najlepszych zasad dla unikatowego zestawu zagrożeń.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Zależność od ręcznego wdrożenia lub konfiguracji systemów

**Ryzyko techniczne:** Poleganie na interwencji ludzkiej podczas wdrażania lub konfiguracji zwiększa prawdopodobieństwo wystąpienia błędu ludzkiego i zmniejsza powtarzalność i przewidywalność wdrożeń i konfiguracji systemu. Zwykle prowadzi to do wolniejszego wdrażania zasobów systemowych.

**Instrukcja zasad:** Wszystkie zasoby wdrożone w chmurze powinny być wdrażane za pomocą szablonów lub skryptów automatyzacji wszędzie tam, gdzie to możliwe.

**Potencjalne opcje projektu:** [Szablony Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) udostępniają podejście "infrastruktura jako kod" do wdrażania zasobów na platformie Azure. [Bloki konstrukcyjne platformy Azure](https://github.com/mspnp/template-building-blocks/wiki) udostępniają narzędzie wiersza polecenia i zestaw szablonów Menedżer zasobów zaprojektowanych w celu uproszczenia wdrażania zasobów platformy Azure.

## <a name="lack-of-visibility-into-system-issues"></a>Brak wglądu w problemy systemowe

**Ryzyko techniczne:** Niewystarczające monitorowanie i Diagnostyka systemów firmowych uniemożliwiają pracownikom operacji identyfikowanie i korygowaniem problemów przed wystąpieniem awarii systemu i znacząco wydłużyć czas wymagany do prawidłowego rozwiązania awarii.

**Instrukcja zasad:** Następujące zasady zostaną zaimplementowane:

- Kluczowe metryki i środki diagnostyki zostaną zidentyfikowane dla wszystkich systemów i składników produkcyjnych, a narzędzia do monitorowania i diagnostyki zostaną zastosowane do tych systemów i monitorowane regularnie przez pracowników operacyjnych.
- Operacje będą brane pod uwagę przy użyciu narzędzi do monitorowania i diagnostyki w środowiskach nieprodukcyjnych, takich jak przygotowanie i kontrola jakości, aby identyfikować problemy systemowe przed ich wystąpieniem w środowisku produkcyjnym.

**Potencjalne opcje projektu:** [Azure monitor](https://docs.microsoft.com/azure/azure-monitor), która obejmuje także Log Analytics i Application Insights, oferuje narzędzia do zbierania i analizowania danych telemetrycznych, które pomagają zrozumieć, jak działają aplikacje i aktywnie identyfikują problemy wpływające na nie i zasoby, od których zależą.

## <a name="configuration-security-reviews"></a>Przeglądy zabezpieczeń konfiguracji

**Ryzyko techniczne:** W miarę upływu czasu nowe zagrożenia lub problemy związane z bezpieczeństwem mogą zwiększyć ryzyko nieautoryzowanego dostępu do zabezpieczonych zasobów.

**Instrukcja zasad:** Procesy nadzoru chmur muszą obejmować kwartalne przeglądy z zespołami zarządzania konfiguracją w celu identyfikowania złośliwych aktorów lub wzorców użytkowania, które powinny być blokowane przez konfigurację zasobów w chmurze.

**Potencjalne opcje projektu:** Ustanów kwartalne spotkanie przeglądowe dotyczące zabezpieczeń, które obejmuje członków zespołu nadzoru i personel IT odpowiedzialny za konfigurację aplikacji i zasobów w chmurze. Zapoznaj się z istniejącymi danymi i metrykami zabezpieczeń, aby ustalić luki w bieżącym narzędziu do przyspieszania wdrażania i narzędziach, a także zasady aktualizacji w celu skorygowania wszelkich nowych zagrożeń.

## <a name="next-steps"></a>Następne kroki

Skorzystaj z przykładów przedstawionych w tym artykule jako punktu wyjścia do opracowania zasad, które wiążą się z konkretnymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania w chmurze.

Aby rozpocząć tworzenie własnych niestandardowych instrukcji zasad związanych z zarządzaniem tożsamościami, Pobierz [szablon linii bazowej tożsamości](./template.md).

Aby przyspieszyć wdrażanie tego dyscypliny, wybierz [Przewodnik dotyczący ładu](../guides/index.md) z możliwością działania, który najlepiej odpowiada Twojemu środowisku. Następnie zmodyfikuj projekt, aby uwzględnić określone decyzje dotyczące zasad firmowych.

Opracowywanie zagrożeń i odporności, ustanawianie procesu do zarządzania zasadami przyspieszenia wdrożenia i ich przekazywania.

> [!div class="nextstepaction"]
> [Ustanawianie procesów zgodności z zasadami](./compliance-processes.md)
