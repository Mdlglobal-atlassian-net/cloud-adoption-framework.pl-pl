---
title: 'Sieć zdefiniowana przez oprogramowanie: Tylko usługa PaaS'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Omówienie modelu PaaS-Only dla sieci zdefiniowanej przez oprogramowanie w chmurze.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 704dbb16be57c4203199ca972aa61b520eece3ca
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023547"
---
# <a name="software-defined-networking-paas-only"></a>Sieć zdefiniowana przez oprogramowanie: Tylko usługa PaaS

W przypadku zaimplementowania zasobu platformy jako usługi (PaaS) proces wdrażania automatycznie tworzy przydzieloną sieć podstawową z ograniczoną liczbą kontroli nad tą siecią, w tym Równoważenie obciążenia, blokowanie portów i połączenia z innymi PaaS Services.

Na platformie Azure można [wdrożyć](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services) kilka typów zasobów PaaS lub [połączyć je](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) z siecią wirtualną, umożliwiając integrację tych zasobów z istniejącą infrastrukturą sieci wirtualnej. Inne usługi, takie jak [środowiska App Service](https://docs.microsoft.com/azure/app-service/environment/intro), [usługi Azure Kubernetes Services](https://docs.microsoft.com/azure/aks/intro-kubernetes)i [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) , muszą zostać wdrożone w ramach sieci wirtualnej. Jednak w wielu przypadkach PaaS tylko architekturę sieciową, która polega tylko na domyślnych natywnych możliwościach sieci udostępnianych przez zasoby PaaS, jest wystarczająca do spełnienia wymagań związanych z zarządzaniem obciążeniem i ruchem.

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
