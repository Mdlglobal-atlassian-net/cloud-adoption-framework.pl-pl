---
title: 'Sieć zdefiniowana przez oprogramowanie: chmura natywna'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej na temat natywnych sieci wirtualnych, które są wymagane do wdrażania maszyn wirtualnych w chmurze.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a69c196d76db7f633acdfcf0aff6ad72a11872e5
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83215028"
---
# <a name="software-defined-networking-cloud-native"></a>Sieć zdefiniowana przez oprogramowanie: chmura natywna

Natywna Sieć wirtualna w chmurze jest wymagana podczas wdrażania zasobów IaaS, takich jak maszyny wirtualne, na platformę chmury. Dostęp do sieci wirtualnych ze źródeł zewnętrznych, podobnie jak w przypadku sieci Web, musi być jawnie zainicjowany. Te typy sieci wirtualnych obsługują Tworzenie podsieci, reguł routingu oraz urządzeń wirtualnych i zarządzania ruchem.

Natywna w chmurze Sieć wirtualna nie ma żadnych zależności od zasobów lokalnych lub innych niż zasoby w chmurze w celu obsługi obciążeń hostowanych w chmurze. Wszystkie wymagane zasoby są obsługiwane zarówno w sieci wirtualnej, jak i przy użyciu zarządzanych ofert PaaS.

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

- [Przewodniki dotyczące usługi Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm): nowo utworzone sieci wirtualne są domyślnie natywne w chmurze. Te przewodniki ułatwiają planowanie projektowania i wdrażania sieci wirtualnych.
- [Limity dotyczące sieci platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits#networking-limits): Każda sieć wirtualna i połączone zasoby istnieją w jednej subskrypcji. Te zasoby są ograniczone przez limity subskrypcji.
