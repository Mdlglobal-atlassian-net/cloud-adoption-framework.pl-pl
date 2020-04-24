---
title: Projektowanie i wdrażanie aplikacji
description: Dowiedz się więcej o korzystaniu z Kubernetes w strukturze wdrażania w chmurze na potrzeby tworzenia aplikacji i architektury.
author: sabbour
ms.author: asabbour
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5381580fc947c71ba651c96e73874c047246991c
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997687"
---
<!-- cSpell:ignore asabbour sabbour autoscaler Istio Linkerd -->

# <a name="application-development-and-deployment"></a>Projektowanie i wdrażanie aplikacji

Badaj wzorce i praktyki związane z tworzeniem aplikacji, Konfiguruj potoki DevOps i wdrażaj najlepsze rozwiązania inżynieryjne dla inżynierów niezawodności (SRE).

## <a name="plan-train-and-proof"></a>Planowanie, uczenie i weryfikacja

Po rozpoczęciu pracy Poniższa lista kontrolna i zasoby ułatwią planowanie tworzenia i wdrażania aplikacji. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy przygotowanie środowiska deweloperskiego i konfiguracji przebiegu?
> - Jak będzie można określić strukturę folderu projektu, aby obsługiwał Programowanie aplikacji Kubernetes?
> - Czy zostały zidentyfikowane wymagania dotyczące stanu, konfiguracji i magazynu aplikacji?

<!-- markdownlint-disable MD033 -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Przygotuj środowisko programistyczne.** Skonfiguruj swoje środowisko przy użyciu narzędzi potrzebnych do tworzenia kontenerów i konfigurowania przepływu pracy programistycznej. | [Praca z platformą Docker w Visual Studio Code](https://code.visualstudio.com/docs/azure/docker) <br/>[Praca&nbsp;z&nbsp;Kubernetes&nbsp;w&nbsp;programie&nbsp;Visual Studio Code](https://code.visualstudio.com/docs/azure/kubernetes) <br/> [Wprowadzenie do Azure Dev Spaces](https://docs.microsoft.com/azure/dev-spaces/about) |
> | **Konteneryzowanie aplikację.** Zapoznaj się z kompleksowym doświadczeniem programistycznym Kubernetes, w tym tworzeniem szkieletu aplikacji, przepływami pracy w pętli wewnętrznej, strukturami zarządzania aplikacjami, potokami ciągłej integracji/ciągłego wdrażania, agregacji dzienników, monitorowaniem i metrykami aplikacji. | [Konteneryzowanie aplikacje przy użyciu platformy Docker i Kubernetes (książka elektroniczna)](https://azure.microsoft.com/resources/containerize-your-apps-with-docker-and-kubernetes) <br/> [Kompleksowe środowisko programistyczne Kubernetes na platformie Azure (seminarium internetowe)](https://info.microsoft.com/AU-AzureApp-WBNR-FY20-11Nov-12-ContainerizeYourApplicationswithKubernetesonAzure-SRDEM10557_LP02OnDemandRegistration-ForminBody.html) |
> | **Zapoznaj się z typowymi scenariuszami Kubernetes.** Kubernetes jest często traktowane jako platforma do dostarczania mikrousług, ale staje się znacznie szerszym platformą. Obejrzyj ten film wideo, aby dowiedzieć się więcej o typowych scenariuszach Kubernetes, takich jak analiza wsadowa i przepływ pracy.    | [Typowe&nbsp;scenariusze&nbsp;&nbsp;używania&nbsp;Kubernetes&nbsp;(wideo)](https://www.youtube.com/watch?v=zd8vYhrFXp4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=7) |
> | **Przygotuj swoją aplikację do Kubernetes.** Przygotuj układ systemu plików aplikacji dla Kubernetes i Organizuj go na potrzeby tygodniowych lub codziennych wersji. Dowiedz się, jak proces wdrażania Kubernetes umożliwia niezawodne, nieprzerwane uaktualnienia. | [Projekt i układ projektu dla pomyślnie Kubernetes aplikacji (seminarium internetowe)](https://info.microsoft.com/ww-OnDemandRegistration-successful-kubernetes-applications-webinar.html) <br/> [Jak działają wdrożenia Kubernetes (wideo)](https://www.youtube.com/watch?v=mNK14yXIZF4&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=3) </br> [Przechodzenie przez Warsztat AKS](https://aka.ms/learn/aksworkshop) |
> | **Zarządzanie magazynem aplikacji.** Zapoznaj się z wymaganiami dotyczącymi wydajności i metodami dostępu dla zasobników, aby zapewnić odpowiednie opcje magazynu. Należy również zaplanować sposoby tworzenia kopii zapasowych i testowania procesu przywracania dołączonego magazynu. | [Podstawowe informacje o aplikacjach stanowych w Kubernetes (wideo)](https://www.youtube.com/watch?v=GieXzb91I40&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=9) <br/> [Stan i dane w aplikacjach platformy Docker](https://docs.microsoft.com/dotnet/architecture/microservices/architect-microservice-container-applications/docker-application-state-data) <br/>[Opcje magazynu w usłudze Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/operator-best-practices-storage) |
> | **Zarządzaj wpisami tajnymi aplikacji.** Nie przechowuj poświadczeń w kodzie aplikacji. Magazyn kluczy powinien służyć do przechowywania i pobierania kluczy i poświadczeń.  | [Jak działa Kubernetes i zarządzanie konfiguracją (wideo)](https://www.youtube.com/watch?v=vRcQOZLnKUk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=11) <br/> [Informacje o zarządzaniu wpisami tajnymi w programie Kubernetes (wideo)](https://www.youtube.com/watch?v=KmhM33j5WYk&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=10) <br/>[Używanie Azure Key Vault z Kubernetes](https://github.com/Azure/kubernetes-keyvault-flexvol) <br/>[Uwierzytelnianie i dostęp do zasobów platformy Azure przy użyciu tożsamości pod](https://github.com/Azure/aad-pod-identity) |

## <a name="deploy-to-production-and-apply-best-practices"></a>Wdrażanie w środowisku produkcyjnym i stosowanie najlepszych rozwiązań

Podczas przygotowywania aplikacji do produkcji należy zaimplementować minimalny zestaw najlepszych rozwiązań. Na tym etapie Skorzystaj z poniższej listy kontrolnej. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy można monitorować wszystkie aspekty aplikacji?
> - Czy masz zdefiniowane wymagania dotyczące zasobów dla aplikacji? Jak są wymagane skalowanie?
> - Czy można wdrażać nowe wersje aplikacji bez wpływu na systemy produkcyjne?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Skonfiguruj gotowość i kontrole kondycji na żywo.** Kubernetes używa gotowości i kontroli na żywo, aby dowiedzieć się, kiedy aplikacja jest gotowa do odbierania ruchu i gdy należy ponownie uruchomić. Bez definiowania takich kontroli Kubernetes nie będzie w stanie określić, czy aplikacja jest uruchomiona.   | [Kontrole na żywo i gotowości](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes) |
> | **Konfigurowanie rejestrowania, monitorowania aplikacji i alertów.** Monitorowanie kontenerów ma krytyczne znaczenie, szczególnie w przypadku korzystania z klastra produkcyjnego w odpowiedniej skali z wieloma aplikacjami. Zalecana metoda rejestrowania dla aplikacji kontenerowych jest zapisywany w strumieniach Standard Output (stdout) i Standard Error (stderr).   | [Logowanie w Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging) <br/> [Wprowadzenie do monitorowania i wysyłania alertów dla Kubernetes (wideo)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Azure Monitor kontenerów](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Włączanie i wyświetlanie dzienników węzła master platformy Kubernetes w usłudze Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/view-master-logs)  <br/> [Wyświetlanie dzienników Kubernetes, zdarzeń i metryk pod w czasie rzeczywistym](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-livedata-overview) |
> | **Zdefiniuj wymagania dotyczące zasobów dla aplikacji.** Podstawowym sposobem zarządzania zasobami obliczeniowymi w klastrze Kubernetes jest użycie żądań i limitów. Te żądania i limity informują usługę Kubernetes Scheduler, jakie zasoby obliczeniowe należy przypisać.     | [Definiuj&nbsp;żądania&nbsp;&nbsp;&nbsp;zasobów&nbsp;i limity](https://docs.microsoft.com/azure/aks/developer-best-practices-resource-management) |
> | **Skonfiguruj wymagania dotyczące skalowania aplikacji.** Rozwiązanie Kubernetes obsługuje automatyczne skalowanie zasobników w poziomie, umożliwiające dostosowywanie liczby zasobników we wdrożeniu do użycia procesora lub innych wybranych metryk. Aby można było korzystać ze skalowania automatycznego, wszystkie kontenery w swoich zasobnikach muszą mieć zdefiniowane żądania procesora CPU i limity.    | [Konfigurowanie automatycznego skalowania w poziomie](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale#autoscale-pods) |
> | **Wdrażaj aplikacje za pomocą zautomatyzowanego potoku i DevOps.**  Pełna automatyzacja wszystkich kroków między przekazaniem kodu do wdrożenia produkcyjnego umożliwia zespołom skoncentrowanie się na tworzeniu kodu i usuwa narzuty oraz potencjalnego błędu ludzkiego w ręcznych krokach żmudnych. Wdrażanie nowego kodu jest szybsze i mniej ryzykowne, dzięki czemu zespoły stają się bardziej elastyczne, wydajniejsze i bardziej niedbają o uruchomionym kodzie.    | [Rozwijanie praktyk metodyki DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices) <br/> [Konfigurowanie potoku kompilacji Kubernetes (wideo)](https://www.youtube.com/watch?v=5irsAdKoEBU&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=6) <br/> [Centrum wdrażania usługi Azure Kubernetes](https://docs.microsoft.com/azure/aks/deployment-center-launcher) <br/> [Akcje GitHub dotyczące wdrażania w usłudze Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/kubernetes-action) <br/>  [Ciągłej integracji/ciągłego wdrażania w usłudze Azure Kubernetes Service z usługą Jenkins](https://docs.microsoft.com/azure/aks/jenkins-continuous-deployment) |

## <a name="optimize-and-scale"></a>Optymalizowanie i skalowanie

Teraz, gdy aplikacja jest w środowisku produkcyjnym, jak można zoptymalizować przepływ pracy i przygotować swoją aplikację i zespół do skalowania? Użyj listy kontrolnej Optymalizacja i skalowanie, aby przygotować. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy istnieją problemy z aplikacjami, które są wyodrębniane z aplikacji?
> - Czy można zachować niezawodność systemu i aplikacji, podczas gdy nadal trwa iteracja nowych funkcji i wersji?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby                                                                                                     |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Wdróż bramę interfejsu API.** Brama interfejsu API służy jako przód drzwi do mikrousług, oddziela klientów od mikrousług, dodaje dodatkową warstwę zabezpieczeń i zmniejsza złożoność mikrousług, eliminując obciążenie związane z obcinaniem.     | [Korzystanie z usługi Azure API Management z mikrousługami wdrożonymi w usłudze Azure Kubernetes Service](https://docs.microsoft.com/azure/api-management/api-management-kubernetes) |
> | **Wdróż siatkę usług.** Siatka usług zapewnia takie możliwości jak zarządzanie ruchem, odporność, zasady, zabezpieczenia, silna tożsamość i przestrzeganie obciążeń. Aplikacja jest oddzielona od tych możliwości operacyjnych, a siatka usług przenosi je z warstwy aplikacji do warstwy infrastruktury.     | [Jak&nbsp;&nbsp;działa&nbsp;&nbsp;siatka usług w&nbsp;Kubernetes&nbsp;(wideo)](https://www.youtube.com/watch?v=izVWk7rYqWI&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=15&t=0s) <br/> [Informacje o usłudze Service siatk](https://docs.microsoft.com/azure/aks/servicemesh-about) <br/> [Korzystanie z Istio z usługą Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/servicemesh-istio-about) <br/> [Używanie konsolidatora z usługą Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/servicemesh-linkerd-about) <br/> [Korzystanie z Consul z usługą Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/servicemesh-consul-about) |
> | **Zaimplementuj praktyki Inżynieria niezawodności (SRE).**  Inżynieria ds. niezawodności (SRE) jest sprawdzonym podejściem do utrzymania decydującej niezawodności systemu i aplikacji podczas iterowania z prędkością wymaganą przez portal Marketplace.   | [Wprowadzenie do inżynierii niezawodności lokacji (SRE)](https://docs.microsoft.com/learn/modules/intro-to-site-reliability-engineering) <br/> [DevOps w firmie Microsoft: gra Streaming SRE](https://azure.microsoft.com/resources/devops-at-microsoft-game-streaming-sre) |
