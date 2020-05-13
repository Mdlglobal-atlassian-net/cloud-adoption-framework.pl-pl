---
title: Motywacje i ryzyko biznesowe w dyscyplinie przyspieszenia wdrożenia
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć ryzyko biznesowe dyscypliny wdrożenia, które mogą być używane w strategii ładu.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6cd6d309b5c44c55d0409b759950662eccb9f50a
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220451"
---
# <a name="motivations-and-business-risks-in-the-deployment-acceleration-discipline"></a>Motywacje i ryzyko biznesowe w dyscyplinie przyspieszenia wdrożenia

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę przyspieszenia wdrożenia w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów ryzyka biznesowego, które dotyczą instrukcji zasad.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Trafność

Systemy lokalne są często wdrażane przy użyciu obrazów linii bazowej lub skryptów instalacji. Dodatkowa konfiguracja jest zwykle konieczna, co może wiązać się z wieloma krokami lub interwencją człowieka. Te procesy ręczne są podatne na błędy i często skutkują "dryfem konfiguracji", wymagając czasochłonnych zadań związanych z rozwiązywaniem problemów i korygowaniem.

Większość zasobów platformy Azure można wdrożyć i skonfigurować ręcznie za pośrednictwem Azure Portal. Takie podejście może być wystarczające dla Twoich potrzeb, gdy istnieje tylko kilka zasobów do zarządzania. Jednak po rozmieszczeniu Twojej chmury organizacja powinna zacząć integrować automatyzację z procesami wdrażania, aby upewnić się, że zasoby w chmurze zapobiegają dryfowi lub innym problemom wprowadzonym przez procesy ręczne. Przyjęcie podejścia DevOps lub [DevSecOps](https://www.microsoft.com/devsecops) jest często najlepszym sposobem na Zarządzanie wdrożeniami w miarę wczesnych wysiłków związanych z wdrażaniem w chmurze.

Wydajny plan przyspieszania wdrażania zapewnia, że zasoby w chmurze są wdrażane, aktualizowane i poprawnie skonfigurowane, a tym samym w ten sposób. Termin zapadalności strategii przyspieszenia wdrożenia może być również znaczącym czynnikiem w [strategii Cost Management](../cost-management/index.md). Automatyczne Inicjowanie obsługi i konfiguracja zasobów w chmurze pozwala na skalowanie zasobów w dół lub w dół, gdy zapotrzebowanie jest niskie lub ograniczone od czasu, dzięki czemu płacisz tylko za zasoby, które są potrzebne.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina wdrożenia pozwala próbować rozwiązać następujące ryzyko biznesowe. Podczas wdrażania chmury Monitoruj następujące elementy pod kątem istotności:

- **Przerwanie działania usługi:** Brak przewidywalnych powtarzalnych procesów wdrażania lub niezarządzanych zmian konfiguracji systemu może zakłócać normalne operacje i spowodować utratę produktywności lub utratę działalności firmy.
- **Przekroczenia kosztów:** Nieoczekiwane zmiany w konfiguracji zasobów systemowych mogą utrudnić zidentyfikowanie głównych przyczyn problemów, zwiększając koszty rozwoju, operacji i konserwacji.
- **Nieefektywność organizacyjna:** Bariery między zespołami programistycznymi, operacyjnymi i bezpieczeństwa mogą spowodować liczne wyzwania dla efektywnego wdrożenia technologii chmurowych i rozwoju ujednoliconego modelu ładu chmurowego.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu dyscypliny wdrożenia](./template.md) można udokumentować ryzyko biznesowe, które mogą zostać wprowadzone przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Metryki, wskaźniki i tolerancja ryzyka](./metrics-tolerance.md)
