---
title: Zabezpieczenia klastra i aplikacji
description: Dowiedz się więcej na temat Kubernetes w strukturze wdrażania chmury w celu zapewnienia bezpieczeństwa klastrów i aplikacji.
author: sabbour
ms.author: asabbour
ms.topic: guide
ms.date: 03/20/2020
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 64a7f4097a75b54ef4f91b5889fa31fc3b98d61a
ms.sourcegitcommit: 1a4b140f09bdaa141037c54a4a3b5577cda269db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/30/2020
ms.locfileid: "80392742"
---
<!-- cSpell:ignore asabbour sabbour kured -->

# <a name="cluster-and-application-security"></a>Zabezpieczenia klastra i aplikacji

Zapoznaj się z usługą Kubernetes Security Essentials i zapoznaj się z bezpieczną konfiguracją klastrów i wskazówek dotyczących zabezpieczeń aplikacji.

## <a name="plan-train-and-proof"></a>Planowanie, uczenie i weryfikacja

Po rozpoczęciu pracy Poniższa lista kontrolna i zasoby ułatwią planowanie operacji klastra i zabezpieczeń. Należy mieć możliwość udzielenia odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy sprawdzono model zabezpieczeń i zagrożeń klastrów Kubernetes?
> - Czy klaster jest włączony na potrzeby kontroli dostępu opartej na rolach?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Zapoznaj się z oficjalnym dokumentem dotyczącym zabezpieczeń.** Główne cele bezpiecznego środowiska Kubernetes zapewniają, że uruchomione aplikacje są chronione, dzięki czemu problemy z zabezpieczeniami mogą być zidentyfikowane i rozwiązywane szybko, a przyszłe podobne problemy zostaną uniemożliwione. | [Ostateczny Przewodnik dotyczący zabezpieczania Kubernetes (oficjalny dokument)](https://clouddamcdnprodep.azureedge.net/gdc/gdc8LXmoZ/original)     |
> | **Zapoznaj się z konfiguracją zabezpieczeń dla węzłów klastra.** System operacyjny hosta z ograniczoną funkcjonalnością zabezpieczeń zmniejsza powierzchnię ataku i umożliwia bezpieczne wdrażanie kontenerów. | [Zabezpieczanie zabezpieczeń na hostach maszyn wirtualnych AKS](https://docs.microsoft.com/azure/aks/security-hardened-vm-host-image)     |
> | **Konfiguracja kontroli dostępu opartej na rolach (RBAC) klastra.** Ten mechanizm kontroli pozwala przypisywać użytkowników lub grupy użytkowników, uprawnienia do wykonywania takich czynności jak tworzenie lub modyfikowanie zasobów lub wyświetlanie dzienników z uruchamiania obciążeń aplikacji. | [Opis kontroli dostępu opartej na rolach (RBAC) w Kubernetes (wideo)](https://www.youtube.com/watch?v=G3R24JSlGjY&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=12) <br/> [Integrowanie usługi Azure AD z usługą Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/azure-ad-integration) <br/> [Ograniczanie dostępu do pliku konfiguracji klastra](https://docs.microsoft.com/azure/aks/control-kubeconfig-access)   |

## <a name="deploy-to-production-and-apply-best-practices"></a>Wdrażanie w środowisku produkcyjnym i stosowanie najlepszych rozwiązań

Podczas przygotowywania aplikacji do produkcji należy zaimplementować minimalny zestaw najlepszych rozwiązań. Na tym etapie Skorzystaj z poniższej listy kontrolnej. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy skonfigurowano reguły zabezpieczeń sieci dla ruchu przychodzącego, wychodzącego i komunikacji wewnętrznej pod?
> - Czy klaster jest skonfigurowany tak, aby automatycznie stosował aktualizacje zabezpieczeń węzłów?
> - Czy korzystasz z rozwiązania do skanowania zabezpieczeń dla klastrów i obciążeń kontenerów?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Kontroluj dostęp do klastrów przy użyciu członkostwa w grupie.** Skonfiguruj kontrolę dostępu opartą na rolach (RBAC) Kubernetes, aby ograniczyć dostęp do zasobów klastra lub do członkostwa w grupie. | [Kontrola dostępu do klastrów przy użyciu funkcji RBAC i grup usługi Azure AD](https://docs.microsoft.com/azure/aks/azure-ad-rbac)    |
> | **Utwórz zasady zarządzania kluczami tajnymi.** Bezpiecznie Wdrażaj poufne informacje, takie jak hasła i certyfikaty, i zarządzaj nimi, korzystając z funkcji zarządzania kluczami tajnymi w programie Kubernetes. | [Informacje o zarządzaniu wpisami tajnymi w programie Kubernetes (wideo)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) |
> | **Zabezpiecz ruch sieciowy wewnątrz sieci przy użyciu zasad sieciowych.** Stosuj zasadę najniższych uprawnień do kontroli przepływu ruchu sieciowego między zasobnikami w klastrze. | [Zabezpieczanie ruchu wewnątrzwspólnotowego przy użyciu zasad sieciowych](https://docs.microsoft.com/azure/aks/use-network-policies) |
> | **Ogranicz dostęp do serwera interfejsu API przy użyciu autoryzowanych adresów IP.** Zwiększ bezpieczeństwo klastra i Zminimalizuj obszar ataków, ograniczając dostęp do serwera interfejsu API do ograniczonego zestawu zakresów adresów IP. | [Bezpieczny dostęp do serwera interfejsu API](https://docs.microsoft.com/azure/aks/api-server-authorized-ip-ranges) |
> | **Ogranicz ruch wychodzący klastra.** Informacje o portach i adresach, które mają być dozwolone w przypadku ograniczenia ruchu wychodzącego dla klastra. Do zabezpieczenia ruchu wychodzącego i definiowania wymaganych portów i adresów można użyć zapory platformy Azure lub urządzenia zapory innej firmy. | [Sterowanie ruchem wychodzącym węzłów klastra w AKS](https://docs.microsoft.com/azure/aks/limit-egress-traffic) |
> | **Zabezpieczanie ruchu za pomocą zapory aplikacji sieci Web (WAF).** Korzystanie z usługi Azure Application Gateway jako kontrolera usług przychodzących dla klastrów Kubernetes.  | [Konfigurowanie usługi Azure Application Gateway jako kontrolera transferu danych przychodzących](https://docs.microsoft.com/azure/application-gateway/ingress-controller-overview)    |
> | **Zastosuj aktualizacje zabezpieczeń i jądra do węzłów procesu roboczego.** Poznaj środowisko aktualizacji węzłów AKS. W celu ochrony klastrów aktualizacje zabezpieczeń są automatycznie stosowane do węzłów systemu Linux w programie AKS. Te aktualizacje obejmują poprawki zabezpieczeń systemu operacyjnego lub aktualizacje jądra. Niektóre z tych aktualizacji wymagają ponownego uruchomienia węzła w celu ukończenia procesu. | [Użyj kured do automatycznego ponownego uruchamiania węzłów w celu zastosowania aktualizacji](https://docs.microsoft.com/azure/aks/node-updates-kured) |
> | **Skonfiguruj rozwiązanie do skanowania kontenera i klastra.** Kontenery skanowania są przekazywane do Azure Container Registry i uzyskują dokładniejszy wgląd w węzły klastra, ruch w chmurze i mechanizmy zabezpieczeń. | [Azure Container Registry integrację z usługą Security Center](https://docs.microsoft.com/azure/security-center/azure-container-registry-integration) <br/> [Integracja usługi Azure Kubernetes z usługą Security Center](https://docs.microsoft.com/azure/security-center/azure-kubernetes-service-integration)  |

## <a name="optimize-and-scale"></a>Optymalizowanie i skalowanie

Teraz, gdy aplikacja jest w środowisku produkcyjnym, jak można zoptymalizować przepływ pracy i przygotować swoją aplikację i zespół do skalowania? Użyj listy kontrolnej Optymalizacja i skalowanie, aby przygotować. Powinien być w stanie odpowiedzieć:

> [!div class="checklist"]
>
> - Czy można wymuszać zasady zarządzania i klastra na dużą skalę?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Wymuś zasady zarządzania klastrami.** Stosuj wymuszanie i zabezpieczenia w klastrach w scentralizowany, spójny sposób. | [Kontroluj wdrożenia za pomocą Azure Policy](https://docs.microsoft.com/azure/governance/policy/concepts/rego-for-aks)    |
> | **Okresowe obracanie certyfikatów klastra.** Kubernetes używa certyfikatów do uwierzytelniania z wieloma składnikami. Warto okresowo obracać te certyfikaty ze względów bezpieczeństwa lub zasad. | [Obróć certyfikaty w usłudze Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/certificate-rotation)    |
