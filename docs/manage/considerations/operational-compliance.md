---
title: Zgodność operacyjna — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zgodność operacyjna — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: bb6e4584da87d992f85b6ce90e21081c9c19d7c3
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682548"
---
# <a name="operational-compliance-in-cloud-management"></a>Zgodność operacyjna w zarządzaniu chmurą

Zgodność operacyjna jest oparta na dyscyplinach [spisu i widoczności](./inventory.md)jako pierwszy krok do wykonania w ramach zarządzania chmurą. Ta dyscyplina koncentruje się na zwykłych przeglądach telemetrii i wysiłkach naprawczych (proczynnych i reaktywnych korygowaniu). Ta dyscyplina jest podstawą do utrzymania równowagi między bezpieczeństwem, zarządzaniem, wydajnością i kosztami.

## <a name="components-of-operations-compliance"></a>Składniki zgodności operacji

Zachowanie zgodności z zobowiązaniami operacyjnymi wymaga analizy, automatyzacji i korygowania przez człowieka. Skuteczna zgodność operacyjna wymaga spójności w kilku krytycznych procesach:

1. Spójność zasobów
2. Spójność środowiska
3. Spójność konfiguracji zasobów
4. Spójność aktualizacji
5. Automatyzacja korygowania

### <a name="resource-consistency"></a>Spójność zasobów

Najbardziej skutecznym krokiem, jaki zespół zarządzający w chmurze może podjąć w kierunku zgodności operacyjnej, ustanawia spójność w zakresie organizacji i tagowania zasobów. Gdy zasoby są stale zorganizowane i znakowane, wszystkie inne zadania operacyjne stają się łatwiejsze. Aby uzyskać bardziej szczegółowe wskazówki dotyczące spójności zasobów, zapoznaj się z [etapem ładu](../../govern/index.md) cyklu życia wdrożenia chmury. W odróżnieniu od [początkowych artykułów do ładu Foundation](../../govern/initial-foundation.md) przedstawiono przykłady sposobów rozpoczynania tworzenia spójności zasobów.

### <a name="environment-consistency"></a>Spójność środowiska

Spójne środowiska lub strefy wyładunkowe to kolejny najważniejszy krok w kierunku zgodności operacyjnej. Gdy strefy wyładunkowe są spójne i wymuszane za poorednictwem zautomatyzowanych narzędzi, jest znacznie mniej skomplikowane do diagnozowania i rozwiązywania problemów operacyjnych. Aby uzyskać bardziej szczegółowe wskazówki dotyczące spójności środowiska, zobacz [Faza gotowości](../../ready/index.md) wdrożenia chmury. Ćwiczenia w tej fazie określają powtarzalny proces służący do definiowania i dojrzewania spójnego, jednokierunkowego podejścia do tworzenia środowisk opartych na chmurze.

### <a name="resource-configuration-consistency"></a>Spójność konfiguracji zasobów

Przy opracowywaniu rozwiązań nadzoru i gotowości zarządzanie chmurą powinno obejmować procesy ciągłego monitorowania i oceny przestrzegania wymagań spójności zasobów. W miarę wprowadzania zmian obciążeń lub nowych wersji należy koniecznie, aby procesy zarządzania chmurą szacować zmiany konfiguracji, które nie są łatwo regulowane za pośrednictwem zautomatyzowanych środków.

W przypadku wykrycia niespójności niektóre są rozwiązywane przez spójność aktualizacji, a inne mogą być automatycznie korygowane.

### <a name="update-consistency"></a>Spójność aktualizacji

Stabilność może prowadzić do stabilnych operacji. Jednak niektóre zmiany są wymagane w ramach procesów zarządzania chmurą. W szczególności regularne poprawki i zmiany wydajności są niezbędne do zredukowania przerw i kontrolowania kosztów.

Jedną z wielu wartości metody zarządzania chmurą dla dorosłych jest stabilizacja i kontrola koniecznych zmian.

Każda linia bazowa zarządzania chmurą powinna zawierać środki planowania, kontrolowania i możliwego automatyzacji niezbędnych aktualizacji. Te aktualizacje powinny zawierać co najmniej poprawki, ale mogą również obejmować wydajność, rozmiar i inne aspekty aktualizacji zasobów.

### <a name="remediation-automation"></a>Automatyzacja korygowania

Jako rozszerzona linia bazowa dla zarządzania chmurą, niektóre obciążenia mogą korzystać z automatycznego korygowania. Gdy obciążenie często napotyka problemy, których nie można rozwiązać za pomocą zmian kodu lub architektury, Automatyzacja korygowania może zmniejszyć obciążenie związane z zarządzaniem chmurą i zwiększyć zadowolenie użytkowników.

Wiele prowadziłoby do tego, że wszelkie problemy, które są powszechnie wystarczające do automatyzowania, powinny być rozwiązane przez rozwiązanie długu technicznego. Gdy długoterminowe rozwiązanie jest rozsądne, powinna to być opcja domyślna. Istnieją jednak różne scenariusze biznesowe, które utrudniają wyjustowanie dużych inwestycji w rozwiązaniu długu technicznego. Gdy nie można uzasadnić rozwiązywania długu technicznego, ale korygowanie jest często spotykane i kosztowne, automatyczne korygowanie jest następnym najlepszym rozwiązaniem.

## <a name="next-steps"></a>Następne kroki

[Ochrona i odzyskiwanie](./protect.md) to kolejne obszary, które należy wziąć pod uwagę w linii bazowej zarządzania chmurą.

> [!div class="nextstepaction"]
> [Ochrona i odzyskiwanie](./protect.md)
