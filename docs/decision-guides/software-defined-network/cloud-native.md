---
title: 'Sieć zdefiniowana przez oprogramowanie: Natywne dla chmury'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Omówienie natywnych usług sieci wirtualnych w chmurze.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: d9dda8b5cb91b97da2da50bc747cb3bd6b31947e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023577"
---
# <a name="software-defined-networking-cloud-native"></a>Sieć zdefiniowana przez oprogramowanie: Natywne dla chmury

Natywna Sieć wirtualna w chmurze jest wymagana w przypadku wdrażania zasobów IaaS, takich jak maszyny wirtualne, na platformę chmury. Dostęp do sieci wirtualnych ze źródeł zewnętrznych, podobnie jak w przypadku sieci Web, musi być jawnie zainicjowany. Te typy sieci wirtualnych obsługują Tworzenie podsieci, reguł routingu oraz urządzeń wirtualnych i zarządzania ruchem.

Natywna w chmurze Sieć wirtualna nie ma żadnych zależności w lokalnych lub innych zasobach w chmurze do obsługi obciążeń hostowanych w chmurze. Wszystkie wymagane zasoby są obsługiwane zarówno w sieci wirtualnej, jak i przy użyciu zarządzanych ofert PaaS.

## <a name="cloud-native-assumptions"></a>Założenia natywne w chmurze

Wdrożenie natywnej sieci wirtualnej w chmurze zakłada następujące kwestie:

- Obciążenia wdrożone w sieci wirtualnej nie mają żadnych zależności od aplikacji lub usług, które są dostępne tylko w sieci lokalnej. O ile nie zapewniają punktów końcowych dostępnych za pośrednictwem publicznej sieci Internet, aplikacje i usługi hostowane wewnętrznie lokalnie nie są używane przez zasoby hostowane na platformie chmurowej.
- Zarządzanie tożsamościami i kontrola dostępu zależy od usług tożsamości platformy w chmurze lub serwerów IaaS hostowanych w środowisku chmury. Nie musisz bezpośrednio łączyć się z usługami tożsamości hostowanymi lokalnie lub innymi lokalizacjami zewnętrznymi.
- Usługi tożsamości nie muszą obsługiwać logowania jednokrotnego przy użyciu katalogów lokalnych.

Natywne sieci wirtualne w chmurze nie mają zależności zewnętrznych. Sprawia to, że są one proste do wdrożenia i skonfigurowania, a w efekcie ta architektura jest często najlepszym wyborem dla eksperymentów lub innych mniejszych, samodzielnych lub szybko iternych wdrożeń.

Dodatkowe problemy, które zespół rozwiązań w chmurze powinien wziąć pod uwagę podczas omawiania architektury sieci wirtualnej natywnej w chmurze, to m.in.:

- Istniejące obciążenia przeznaczone do uruchamiania w lokalnym centrum danych mogą wymagać rozległej modyfikacji, aby korzystać z funkcji opartych na chmurze, takich jak magazyn lub usługi uwierzytelniania.
- Sieci natywne w chmurze są zarządzane wyłącznie za pośrednictwem narzędzi do zarządzania platformą w chmurze, dlatego mogą prowadzić do zarządzania i rozbieżności zasad z istniejących standardów IT.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat natywnych sieci wirtualnych w chmurze na platformie Azure, zobacz:

- [Azure Virtual Network: Prowadnice](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm). Nowo utworzone sieci wirtualne platformy Azure są domyślnie natywne w chmurze. Te przewodniki ułatwiają planowanie projektowania i wdrażania sieci wirtualnych.
- [Limity subskrypcji: Sieć](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits). Każda pojedyncza Sieć wirtualna i połączone zasoby mogą istnieć tylko w ramach jednej subskrypcji i są ograniczone przez limity subskrypcji.
