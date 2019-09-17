---
title: Motywacje i zagrożenia biznesowe, które przyspieszają wdrażanie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej na temat dyscypliny wdrożenia w ramach strategii zarządzania chmurą.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: feaf5a7f0f2622c2b2289fe81315ea9ccf2ada4e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027429"
---
# <a name="deployment-acceleration-motivations-and-business-risks"></a>Motywacje do przyspieszenia wdrożenia i ryzyko biznesowe

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę przyspieszenia wdrożenia w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów ryzyka biznesowego, które dotyczą instrukcji zasad.

<!-- markdownlint-disable MD026 -->

## <a name="is-deployment-acceleration-relevant"></a>Czy przyspieszenie wdrożenia jest odpowiednie?

Systemy lokalne są często wdrażane przy użyciu obrazów linii bazowej lub skryptów instalacji. Dodatkowa konfiguracja jest zwykle konieczna, co może wiązać się z wieloma krokami lub interwencją człowieka. Te procesy ręczne są podatne na błędy i często skutkują "dryfem konfiguracji", wymagając czasochłonnych zadań związanych z rozwiązywaniem problemów i korygowaniem.

Większość zasobów platformy Azure można wdrożyć i skonfigurować ręcznie za pośrednictwem Azure Portal. Takie podejście może być wystarczające dla Twoich potrzeb, gdy istnieje tylko kilka zasobów do zarządzania. Jednak po rozmieszczeniu Twojej chmury organizacja powinna zacząć integrować automatyzację z procesami wdrażania, aby upewnić się, że zasoby w chmurze zapobiegają dryfowi lub innym problemom wprowadzonym przez procesy ręczne. Przyjęcie podejścia DevOps lub [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) jest często najlepszym sposobem na Zarządzanie wdrożeniami w miarę wczesnych wysiłków związanych z wdrażaniem w chmurze.

<!-- "en-us" location is required for the URL above. -->

Wydajny plan przyspieszania wdrażania zapewnia, że zasoby w chmurze są wdrażane, aktualizowane i poprawnie skonfigurowane, a tym samym w ten sposób. Termin zapadalności strategii przyspieszenia wdrożenia może być również znaczącym czynnikiem w [strategii Cost Management](../cost-management/index.md). Automatyczne Inicjowanie obsługi i konfiguracja zasobów w chmurze pozwala na skalowanie zasobów w dół lub w dół, gdy zapotrzebowanie jest niskie lub ograniczone od czasu, dzięki czemu płacisz tylko za zasoby, które są potrzebne.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina wdrożenia pozwala próbować rozwiązać następujące ryzyko biznesowe. Podczas wdrażania chmury Monitoruj następujące elementy pod kątem istotności:

- **Przerwanie działania usługi:** Brak przewidywalnych powtarzalnych procesów wdrażania lub niezarządzanych zmian konfiguracji systemu może zakłócać normalne operacje i spowodować utratę produktywności lub utratę działalności firmy.
- **Przekroczenia kosztów:** Nieoczekiwane zmiany w konfiguracji zasobów systemowych mogą utrudnić zidentyfikowanie głównych przyczyn problemów, zwiększając koszty rozwoju, operacji i konserwacji.
- **Nieefektywność organizacyjna:** Bariery między zespołami programistycznymi, operacyjnymi i bezpieczeństwa mogą spowodować liczne wyzwania dla efektywnego wdrożenia technologii chmurowych i rozwoju ujednoliconego modelu ładu chmurowego.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), dokumentuj ryzyka biznesowego, które mogą być wprowadzane przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Metryki, wskaźniki i tolerancja ryzyka](./metrics-tolerance.md)