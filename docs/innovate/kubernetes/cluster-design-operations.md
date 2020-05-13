---
title: Projektowanie i operacje klastra
description: Dowiedz się więcej na temat Kubernetes w strukturze wdrażania chmury na potrzeby projektowania i operacji klastra.
author: sabbour
ms.author: asabbour
ms.date: 12/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: d48a451a9cb6bcedb4f680701f9a6752df24e6a3
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83223987"
---
<!-- cSpell:ignore asabbour sabbour autoscaler PDBs -->

# <a name="cluster-design-and-operations"></a>Projektowanie i operacje klastra

Określ konfigurację klastra i projekt sieci. Skalowalność w przyszłości dzięki automatyzowaniu aprowizacji infrastruktury. Zapewnienie wysokiej dostępności dzięki zaplanowaniu ciągłości działania i odzyskiwania po awarii.

## <a name="plan-train-and-proof"></a>Planowanie, uczenie i weryfikacja

Po rozpoczęciu pracy Poniższa lista kontrolna i zasoby ułatwią planowanie projektu klastra. Należy mieć możliwość udzielenia odpowiedzi na te pytania:

<!-- markdownlint-disable MD033 -->

> [!div class="checklist"]
>
> - Czy zostały zidentyfikowane wymagania dotyczące projektu sieci dla klastra?
> - Czy istnieją obciążenia z różnymi wymaganiami? Ile pul węzłów można używać?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Zidentyfikuj zagadnienia dotyczące projektowania sieci.** Omówienie zagadnień dotyczących projektowania sieci klastrów, porównywania modeli sieci i wybierania wtyczki sieci Kubernetes, która odpowiada Twoim potrzebom.    | [Korzystającą wtyczki kubenet i interfejs sieciowy kontenera platformy Azure (CNI)](https://docs.microsoft.com/azure/aks/concepts-network#azure-virtual-networks) <br/> [Korzystanie z sieci korzystającą wtyczki kubenet z własnymi zakresami adresów IP w usłudze Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-kubenet) <br/> [Konfigurowanie sieci Azure CNI w usłudze Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/configure-azure-cni) <br/> [Bezpieczny projekt sieci dla klastra AKS](https://github.com/azure/sg-aks-workshop/blob/master/cluster-design/NetworkDesign.md) |
> | **Utwórz wiele pul węzłów.** Aby obsługiwać aplikacje, które mają różne wymagania dotyczące obliczeń lub magazynu, można opcjonalnie skonfigurować klaster z wieloma pulami węzłów. Na przykład użyj dodatkowych pul węzłów, aby udostępnić procesory GPU dla aplikacji intensywnie korzystających z obliczeń lub uzyskać dostęp do magazynu SSD o wysokiej wydajności.   | [Tworzenie i zarządzanie wieloma pulami węzłów klastra w usłudze Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/use-multiple-node-pools) |
> | **Określ wymagania dotyczące dostępności.** Aby zapewnić wyższy poziom dostępności aplikacji, klastry mogą być dystrybuowane między strefami dostępności. Te strefy są fizycznie oddzielone centrami danych w danym regionie. Gdy składniki klastra są dystrybuowane w wielu strefach, klaster Cano tolerowanie awarii w jednej z tych stref. Aplikacje i operacje zarządzania są nadal dostępne nawet wtedy, gdy w całym centrum danych wystąpił problem.   | [Tworzenie klastra usługi Azure Kubernetes Service (AKS) korzystającego ze stref dostępności](https://docs.microsoft.com/azure/aks/availability-zones) |

## <a name="go-to-production-and-apply-best-practices"></a>Przejdź do środowiska produkcyjnego i Zastosuj najlepsze rozwiązania

Podczas przygotowywania aplikacji do produkcji należy zaimplementować minimalny zestaw najlepszych rozwiązań. Na tym etapie Skorzystaj z poniższej listy kontrolnej. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy można bezpiecznie ponownie wdrożyć infrastrukturę klastra?
> - Czy zastosowano przydziały zasobów?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |---|---|
> | **Automatyzowanie aprowizacji klastra.** Za pomocą infrastruktury jako kodu można zautomatyzować Inicjowanie obsługi infrastruktury w celu zapewnienia większej odporności podczas awarii i zwiększyć elastyczność, aby szybko wdrożyć infrastrukturę w razie potrzeby. | [Tworzenie klastra Kubernetes za pomocą usługi Azure Kubernetes Service przy użyciu Terraform](https://docs.microsoft.com/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks) |
> | **Zaplanuj dostępność przy użyciu budżetów przerwań.** Aby zachować dostępność aplikacji, należy zdefiniować budżety zakłócania (plików PDB) w celu zapewnienia, że w klastrze są dostępne co najmniej w trakcie awarii sprzętu lub uaktualnień klastra. | [Planowanie dostępności przy użyciu budżetów przerwań](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets) |
> | **Wymuszaj limity przydziału zasobów w przestrzeniach nazw.** Planowanie i stosowanie przydziałów zasobów na poziomie przestrzeni nazw. Limity przydziału można ustawić dla zasobów obliczeniowych, zasobów magazynu i liczby obiektów. | [Wymuszaj przydziały zasobów](https://docs.microsoft.com/azure/aks/operator-best-practices-scheduler#enforce-resource-quotas) |

## <a name="optimize-and-scale"></a>Optymalizowanie i skalowanie

Teraz, gdy aplikacja jest w środowisku produkcyjnym, jak można zoptymalizować przepływ pracy i przygotować swoją aplikację i zespół do skalowania? Użyj listy kontrolnej Optymalizacja i skalowanie, aby przygotować. Powinno być możliwe udzielenie odpowiedzi na te pytania:

> [!div class="checklist"]
>
> - Czy masz plan zapewnienia ciągłości biznesowej i odzyskiwania po awarii?
> - Czy można skalować klaster, aby spełniał wymagania aplikacji?
> - Czy możesz monitorować klaster i kondycję aplikacji i odbierać alerty?

<!-- -->

> [!div class="tdCol2BreakAll"]
>
> | Lista kontrolna  | Zasoby |
> |------------------------------------------------------------------|-----------------------------------------------------------------|
> | **Automatyczne skalowanie klastra w celu spełnienia wymagań aplikacji.** Aby zachować zapotrzebowanie na aplikacje, może być konieczne dostosowanie liczby węzłów, które automatycznie uruchamiają obciążenia przy użyciu automatycznego skalowania klastra. | [Konfigurowanie automatycznego skalowania klastra Kubernetes](https://docs.microsoft.com/azure/aks/cluster-autoscaler)    |
> | **Zaplanuj ciągłość działania i odzyskiwanie po awarii.** Zaplanuj wdrożenie z wieloregionem, Utwórz plan migracji magazynu i Włącz replikację geograficzną dla obrazów kontenerów. | [Najlepsze rozwiązania dotyczące wdrożeń regionów](https://docs.microsoft.com/azure/aks/operator-best-practices-multi-region)  <br/> [Azure Container Registry replikację geograficzną](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication)  |
> | **Skonfiguruj monitorowanie i rozwiązywanie problemów na dużą skalę.** Skonfiguruj alerty i monitorowanie dla aplikacji w Kubernetes. Dowiedz się więcej na temat konfiguracji domyślnej, sposobu integrowania bardziej zaawansowanych metryk i sposobu dodawania własnych niestandardowych monitorów i alertów w celu niezawodnego działania aplikacji. | [Wprowadzenie do monitorowania i wysyłania alertów dla Kubernetes (wideo)](https://www.youtube.com/watch?v=W7aN_z-cyUw&list=PLLasX02E8BPCrIhFrc_ZiINhbRkYMKdPT&index=16) <br/> [Konfigurowanie alertów za pomocą Azure Monitor dla kontenerów](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) <br/> [Przeglądanie dzienników diagnostycznych składników głównych](https://docs.microsoft.com/azure/aks/view-master-logs) <br/> [Diagnostyka usługi Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/concepts-diagnostics)    |
