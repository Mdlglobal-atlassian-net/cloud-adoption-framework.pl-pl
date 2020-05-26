---
title: 'Sieć zdefiniowana przez oprogramowanie: Hub i szprych'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak sieć gwiazdy organizuje infrastrukturę sieci w wielu połączonych sieciach wirtualnych.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9f77d4a13b83c6d22592f36c924c2dd11164e27b
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83814362"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Sieć zdefiniowana przez oprogramowanie: Hub i szprych

Model sieci piasty i szprych organizuje infrastrukturę sieci opartą na platformie Azure w wielu połączonych sieciach wirtualnych. Ten model pozwala wydajniej zarządzać typowymi wymaganiami dotyczącymi komunikacji lub bezpieczeństwa i obsłużyć potencjalne ograniczenia dotyczące subskrypcji.

W _modelu gwiazdy centrum jest siecią_ wirtualną, która pełni rolę centralnej lokalizacji do zarządzania łącznością zewnętrzną i usługami hostingu używanymi przez wiele obciążeń. _Szprychy_ to sieci wirtualne, które obsługują obciążenia i łączą się z centralnym koncentratorem za pomocą [komunikacji równorzędnej sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).

Cały ruch przechodzący z lub z sieci szprych obciążenia jest kierowany przez sieć centralną, w której może być kierowany, sprawdzany lub zarządzany w inny sposób przez centralne zarządzane reguły lub procesy IT.

Ten model ma na celu rozwiązanie następujących problemów:

- **Oszczędność kosztów i efektywność zarządzania.** Scentralizowanie usług, które mogą być współużytkowane przez wiele obciążeń, takich jak wirtualne urządzenia sieciowe (urządzeń WUS) i serwery DNS, w jednej lokalizacji pozwala na zminimalizowanie nadmiarowych zasobów i nakładu pracy związanego z zarządzaniem w wielu obciążeniach.
- **Limity subskrypcji.** Duże obciążenia oparte na chmurze mogą wymagać użycia większej ilości zasobów niż jest to dozwolone w ramach jednej subskrypcji platformy Azure. Komunikacja równorzędna sieci wirtualnych obciążenia z różnych subskrypcji do centrum może pokonać te ograniczenia. Aby uzyskać więcej informacji, zobacz [limity dotyczące sieci platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#networking-limits).
- **Rozdzielenie obaw.** Możliwość wdrażania pojedynczych obciążeń między centralnymi zespołami IT i zespołami obciążeń.

Na poniższym diagramie przedstawiono przykładową architekturę Hub i szprych, w tym centralnie zarządzane połączenie hybrydowe.

![Architektura sieci Hub i szprych](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

Architektura gwiazdy jest często używana wraz z architekturą sieci hybrydowej, co zapewnia centralne zarządzane połączenie ze środowiskiem lokalnym współdzielonym przez wiele obciążeń. W tym scenariuszu cały ruch poruszający się między obciążeniami i lokalnymi przechodzi przez centrum, gdzie można zarządzać i zabezpieczać.

## <a name="hub-and-spoke-assumptions"></a>Założenia gwiazdy i szprych

Implementacja architektury sieci wirtualnych Hub i gwiazdy zakłada następujące kwestie:

- Wdrożenia w chmurze obejmują obciążenia hostowane w oddzielnych środowiskach roboczych, takich jak programowanie, testowanie i produkcja, to wszystko polega na zestawie typowych usług, takich jak DNS lub usługi katalogowe.
- Obciążenia nie muszą komunikować się ze sobą, ale mają wspólne wymagania dotyczące komunikacji zewnętrznej i usług udostępnionych.
- Twoje obciążenia wymagają więcej zasobów niż jest dostępne w ramach jednej subskrypcji platformy Azure.
- Należy zapewnić zespoły obciążeń z delegowanymi prawami do zarządzania za pośrednictwem własnych zasobów, zachowując centralną kontrolę zabezpieczeń przed połączeniem zewnętrznym.

## <a name="global-hub-and-spoke"></a>Centrum globalne i szprycha

Architektury Hub i szprych są zwykle implementowane przy użyciu sieci wirtualnych wdrożonych w tym samym regionie świadczenia usługi Azure, aby zminimalizować opóźnienia między sieciami. Duże organizacje z globalnym zasięgiem mogą wymagać wdrożenia obciążeń w wielu regionach w celu zapewnienia dostępności, odzyskiwania po awarii lub wymagań prawnych. Model gwiazdy umożliwia korzystanie z [globalnej sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) platformy Azure w celu rozbudowania scentralizowanych usług zarządzania i współużytkowanych w różnych regionach oraz obsługi obciążeń rozmieszczonych na całym świecie.

## <a name="learn-more"></a>Więcej tutaj

Aby poznać architektury referencyjne pokazujące, jak zaimplementować sieci piasty i szprych na platformie Azure, zobacz:

- [Implementowanie topologii sieci gwiazdy i gwiazdy na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementowanie topologii sieci gwiazdy i gwiazdy przy użyciu usług udostępnionych na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
