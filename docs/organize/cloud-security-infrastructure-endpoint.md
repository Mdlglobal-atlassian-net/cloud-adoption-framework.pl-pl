---
title: Funkcja infrastruktury chmurowej i zabezpieczeń punktu końcowego
description: Zapoznaj się z funkcją infrastruktury chmurowej i zabezpieczeniami punktów końcowych.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: 427ab031953652c32c77a24e73fb0a0e4cfa10af
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755432"
---
# <a name="function-of-cloud-infrastructure-and-endpoint-security"></a>Funkcja infrastruktury chmurowej i zabezpieczeń punktu końcowego

Zespół ds. zabezpieczeń w chmurze, który współpracuje z infrastrukturą i zabezpieczeniami punktu końcowego, zapewnia ochronę zabezpieczeń, środków wykrywających i kontrolki odpowiedzi dla składników infrastruktury i sieci używanych przez aplikacje i użytkowników przedsiębiorstwa.

## <a name="modernization"></a>Modernizacja

Zdefiniowane przez oprogramowanie centra danych i inne technologie chmury pomagają rozwiązać wyzwania od dawna dba z zabezpieczeniami infrastruktury i punktu końcowego, w tym:

- **Odnajdywanie błędów spisu i konfiguracji** jest znacznie bardziej niezawodne dla zasobów hostowanych w chmurze, ponieważ są one natychmiast widoczne (a fizycznym centrum danych).
- **Zarządzanie** lukami w zabezpieczeniach polega na rozwojem krytycznej części ogólnej stan zarządzania zabezpieczeniami.
- **Dodanie technologii kontenerów** , które mają być zarządzane i zabezpieczone przez zespoły infrastruktury i sieci w miarę jak organizacja przyjmuje tę technologię w szerokim stopniu. Zapoznaj się z przykładem [zabezpieczenia kontenera w Security Center](https://docs.microsoft.com/azure/security-center/container-security) .
- **Konsolidacja** i narzędzia upraszczające agenta zabezpieczeń w celu zmniejszenia obciążenia i wydajności agentów zabezpieczeń i narzędzi.
- **Listy dozwolonych aplikacji** i filtrowanie sieci wewnętrznej stają się znacznie łatwiejsze w konfigurowaniu i wdrażaniu dla serwerów hostowanych w chmurze (przy użyciu zestawów reguł generowanych przez usługę Machine Learning). Zapoznaj się z przykładowymi [kontrolkami aplikacji](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application) i [adaptacyjną funkcjonalnością sieci](https://docs.microsoft.com/azure/security-center/security-center-adaptive-network-hardening) dla platformy Azure.
- **Zautomatyzowane szablony** konfigurowania infrastruktury i zabezpieczeń są znacznie łatwiejsze dzięki zdefiniowanym przez oprogramowanie centrami danych w chmurze. Przykładem platformy Azure są [plany platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/overview)
- **Just in Time (JIT) i wystarczy uzyskać dostęp (jea)** w celu zapewnienia praktycznego dostępu do uprzywilejowanych uprawnień dla serwerów i punktów końcowych.
- **Środowisko użytkownika** ma krytyczne znaczenie, gdy użytkownicy coraz częściej mogą wybrać lub zakupić swoje urządzenia końcowe.
- **Ujednolicone zarządzanie punktami końcowymi** umożliwia zarządzanie Stanami zabezpieczeń wszystkich urządzeń z punktami końcowymi, w tym komputerami przenośnymi i tradycyjnymi, a także zapewnianie krytycznych sygnałów integralności urządzeń w przypadku nierównych rozwiązań
- **Architektury i mechanizmy zabezpieczeń sieci** są częściowo ograniczane do architektur aplikacji w chmurze, ale pozostają one podstawową miarą zabezpieczeń. Aby uzyskać więcej informacji, zobacz [zabezpieczenia sieci i zawieranie](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment).

## <a name="team-composition-and-key-relationships"></a>Kompozycja zespołu i relacje między kluczami

Infrastruktura chmurowa i zabezpieczenia punktu końcowego często współdziałają z następującymi rolami:

- Architektura i operacje IT
- Architektura zabezpieczeń
- Centrum operacji zabezpieczeń
- Zespół ds. zgodności
- Zespół ds. inspekcji

## <a name="next-steps"></a>Następne kroki

Przejrzyj funkcję [analizy zagrożeń](./cloud-security-threat-intelligence.md).
