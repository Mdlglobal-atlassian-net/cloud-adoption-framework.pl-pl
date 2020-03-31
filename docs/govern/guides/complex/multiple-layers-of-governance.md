---
title: 'Złożone zarządzanie przedsiębiorstwem: wiele warstw ładu'
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej na temat większego stopnia złożoności z wieloma warstwami zarządzania w dużych przedsiębiorstwach.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 36c2653876f0d254a282a7f7ed3abaee2ca82656
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434398"
---
# <a name="governance-guide-for-complex-enterprises-multiple-layers-of-governance"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: wiele warstw ładu

Gdy duże przedsiębiorstwa wymagają wielu warstw nadzoru, istnieją wyższe poziomy złożoności, które muszą zostać wdrożone w ramach ładu i nowszych ulepszeń.

Kilka typowych przykładów takich złożoności obejmują:

- Rozproszone funkcje ładu.
- Firmowe dział IT wspierające organizacje IT.
- Firma IT wspiera geograficznie rozproszone organizacje IT.

W tym artykule przedstawiono różne sposoby nawigowania po tym typie złożoności.

## <a name="large-enterprise-governance-is-a-team-sport"></a>Duże zarządzanie przedsiębiorstwem to sport zespołu

Duże przedsiębiorstwa często mają zespoły lub pracowników, którzy koncentrują się na dyscyplinach wymienionych w tym przewodniku. W tym przewodniku przedstawiono jedno podejście do tworzenia ładu zespołu sportowego.

W wielu dużych przedsiębiorstwach może być blokowanych przez pięć dyscyplin zarządzania chmurą. Opracowywanie wiedzy w chmurze w zakresie tożsamości, zabezpieczeń, operacji, wdrożeń i konfiguracji w całym przedsiębiorstwie. Całościowe wdrażanie zasad ładu IT i bezpieczeństwo IT może spowolnić innowacje przez miesiące lub nawet lata. Należy zrównoważyć potrzebę biznesową, aby zapewnić ochronę istniejących zasobów.

Nieodłączne możliwości chmury mogą usuwać blokowania do innowacji, ale zwiększać ryzyko. W tym przewodniku ładu pokazano, jak Przykładowa firma stworzyła guardrails, aby zarządzać ryzykiem. Zamiast korzystać z poszczególnych dyscyplin wymaganych do ochrony środowiska, zespół zarządzający chmurą prowadzi do podejścia opartego na ryzyku, który może zostać wdrożony, podczas gdy inne zespoły tworzą wymagane płatności w chmurze. Co najważniejsze, ponieważ każdy zespół osiąga płatność w chmurze, nadzór stosuje swoje rozwiązania całościowo. Ponieważ każdy zespół dojrzały i dodaje do ogólnego rozwiązania, zespół ds. zarządzania chmurą może otworzyć bramy etapów, co umożliwia wprowadzanie dodatkowych innowacji i wdrażanie.

Ten model ilustruje rozwój partnerstwa między zespołem nadzoru chmurowego i istniejącymi zespołami korporacyjnymi (zabezpieczenia, zarządzanie IT, Sieć, tożsamość i inne). Przewodnik rozpoczyna się od ładu MVP i rośnie do całościowego stanu końcowego za pomocą iteracji ładu.

## <a name="requirements-to-supporting-such-a-team-sport"></a>Wymagania dotyczące wspierania takiego zespołu sportowego

Pierwszym wymaganiem modelu ładu Multilayer jest zrozumienie hierarchii ładu. Udzielenie odpowiedzi na następujące pytania ułatwi zapoznanie się z ogólną hierarchią ładu:

- W jaki sposób ewidencjonowanie aktywności w chmurze (rozliczenia dla usług w chmurze) jest przydzielono w jednostkach biznesowych?
- Jak są przyliczane obowiązki nadzoru między firmowymi i dla każdej jednostki biznesowej?
- Jakie typy środowisk ma zarządzać każda z tych jednostek?

## <a name="central-governance-of-a-distributed-governance-hierarchy"></a>Centralne zarządzanie rozproszonej hierarchii ładu

Narzędzia takie jak grupy zarządzania umożliwiają tworzenie struktury hierarchii zgodnej z hierarchią ładu w firmie. Narzędzia, takie jak plany platformy Azure, mogą stosować zasoby do różnych warstw tej hierarchii. Plany platformy Azure mogą być poddane wersji i można zastosować różne wersje do grup zarządzania, subskrypcji lub grup zasobów. Każdy z tych koncepcji został opisany bardziej szczegółowo w temacie ładu MVP.

Ważnym aspektem każdego z tych narzędzi jest możliwość zastosowania wielu planów do hierarchii programu. Dzięki temu rząd może być procesem warstwowym. Poniżej znajduje się przykład tego hierarchicznego zastosowania ładu:

- **Firma IT:** Firma tworzy zestaw standardów i zasad, które mają zastosowanie do wszystkich rozwiązań chmurowych. Jest to materiałowy plan "linii bazowej". Następnie należy do niej należeć hierarchia grupy zarządzania, co zapewnia, że wersja planu bazowego jest stosowana do wszystkich subskrypcji w hierarchii.
- **Jednostki regionalne lub biznesowe:** Różne zespoły IT mogą stosować dodatkową warstwę ładu, tworząc własny plan. Te plany spowodują utworzenie dodatkowych zasad i standardów. Po opracowaniu firma może zastosować te plany do odpowiednich węzłów w hierarchii grupy zarządzania.
- **Zespoły wdrażania chmury:** Szczegółowe decyzje i implementacje dotyczące aplikacji lub obciążeń mogą być podejmowane przez każdego zespołu adopcji w chmurze w kontekście wymagań ładu. Czasami zespół może również zażądać dodatkowych szablonów spójności zasobów platformy Azure, aby przyspieszyć wdrażanie.

Szczegóły dotyczące wdrożenia ładu na każdym poziomie będą wymagały koordynacji między poszczególnymi członkami zespołu. Udoskonalenia ładu i ładu, które opisano w tym przewodniku, mogą pomóc w dostosowywaniu tej koordynacji.
