---
title: 'Sieć definiowana przez oprogramowanie: tylko PaaS'
description: Dowiedz się więcej o zaletach i ograniczeniach modelu architektonicznego "PaaS" w ramach oprogramowania zdefiniowanego w chmurze.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: e5351d14c6200056e4c5b43f622f655a23e79668
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83753570"
---
# <a name="software-defined-networking-paas-only"></a>Sieć definiowana przez oprogramowanie: tylko PaaS

Podczas implementowania zasobu platformy jako usługi (PaaS) proces wdrażania automatycznie tworzy przyjętą sieć podstawową z ograniczoną liczbą kontroli nad tą siecią, w tym równoważenia obciążenia, blokowanie portów i połączeniami z innymi usługami PaaS.

Na platformie Azure można wdrożyć kilka typów zasobów PaaS w [sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services) lub [połączyć się z siecią wirtualną](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview), integrując te zasoby z istniejącą infrastrukturą sieci wirtualnej. Inne usługi, takie jak [App Service Environment](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure KUBERNETES Service (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes)i [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) muszą zostać wdrożone w ramach sieci wirtualnej. W wielu przypadkach architektura sieci PaaS, która polega wyłącznie na domyślnych natywnych możliwościach sieci zapewnianych przez zasoby PaaS, jest wystarczająca do spełnienia wymagań związanych z zarządzaniem obciążeniem i ruchem.

Jeśli rozważasz architekturę sieci PaaS, upewnij się, że wymagane są odpowiednie założenia dostosowane do Twoich wymagań.

## <a name="paas-only-assumptions"></a>PaaS — tylko założenia

Wdrożenie architektury sieci PaaS-Only zakłada następujące kwestie:

- Wdrażana aplikacja jest aplikacją autonomiczną lub zależy tylko od innych zasobów PaaS, które nie wymagają sieci wirtualnej.
- Zespoły operacji IT mogą aktualizować narzędzia, szkolenia i procesy w celu obsługi zarządzania, konfiguracji i wdrażania autonomicznych aplikacji PaaS.
- Aplikacja PaaS nie jest częścią szerszego wysiłku związanego z migracją w chmurze, który obejmuje zasoby IaaS.

Te założenia są minimalnymi kwalifikatorami wyrównanymi do wdrożenia sieci PaaS. Chociaż takie podejście może być zgodne z wymaganiami jednego wdrożenia aplikacji, każdy zespół wdrażania w chmurze powinien wziąć pod uwagę następujące długoterminowe pytania:

- Czy to wdrożenie zostanie rozwinięte w zakresie lub w skali, aby wymagać dostępu do innych zasobów innych niż PaaS?
- Czy inne wdrożenia PaaS są planowane poza bieżącym rozwiązaniem?
- Czy w organizacji są planowane inne migracje w chmurze?

Odpowiedzi na te pytania nie uniemożliwiają zespołowi wyboru opcji PaaS, ale należy wziąć pod uwagę przed podjęciem ostatecznej decyzji.
