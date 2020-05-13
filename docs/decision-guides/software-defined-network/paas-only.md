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
ms.openlocfilehash: 4c2a8e4e87e1ad99fedf002b0f13854949345916
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215011"
---
# <a name="software-defined-networking-paas-only"></a>Sieć definiowana przez oprogramowanie: tylko PaaS

Podczas implementowania zasobu platformy jako usługi (PaaS) proces wdrażania automatycznie tworzy przyjętą sieć podstawową z ograniczoną liczbą kontroli nad tą siecią, w tym równoważenia obciążenia, blokowanie portów i połączeniami z innymi usługami PaaS.

Na platformie Azure można [wdrożyć](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services) kilka typów zasobów PaaS lub [połączyć je](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) z siecią wirtualną, umożliwiając integrację tych zasobów z istniejącą infrastrukturą sieci wirtualnej. Inne usługi, takie jak [App Service Environment](https://docs.microsoft.com/azure/app-service/environment/intro), [Azure KUBERNETES Service (AKS)](https://docs.microsoft.com/azure/aks/intro-kubernetes)i [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) muszą zostać wdrożone w ramach sieci wirtualnej. Jednak w wielu przypadkach PaaS tylko architekturę sieciową, która polega tylko na domyślnych natywnych możliwościach sieci udostępnianych przez zasoby PaaS, jest wystarczająca do spełnienia wymagań związanych z zarządzaniem obciążeniem i ruchem.

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
