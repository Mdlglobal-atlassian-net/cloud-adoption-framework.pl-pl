---
title: 'Sieć zdefiniowana przez oprogramowanie: Strefa DMZ w chmurze'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ta architektura sieci umożliwia ograniczony dostęp między sieciami lokalnymi i opartymi na chmurze.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 6dfee69d20afac27c735f2ff77abbadc2816ca26
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828346"
---
# <a name="software-defined-networking-cloud-dmz"></a>Sieć zdefiniowana przez oprogramowanie: Strefa DMZ w chmurze

Architektura sieci DMZ w chmurze umożliwia ograniczony dostęp między sieciami lokalnymi i opartymi na chmurze przy użyciu wirtualnej sieci prywatnej (VPN) do łączenia sieci. Chociaż model DMZ jest często używany w przypadku, gdy chcesz zabezpieczyć zewnętrzny dostęp do sieci, architektura strefy DMZ w chmurze omówiona w tym miejscu jest przeznaczona głównie do zabezpieczania dostępu do sieci lokalnej z zasobów w chmurze i na odwrót.

![Bezpieczna hybrydowa architektura sieci](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/images/dmz-private.png)

Ta architektura została zaprojektowana w celu obsługi scenariuszy, w których organizacja chce rozpocząć integrowanie obciążeń opartych na chmurze z obciążeniami lokalnymi, ale mogą nie mieć w pełni pełnych zasad zabezpieczeń w chmurze lub nie uzyskało bezpiecznego dedykowanego połączenia sieci WAN między dwa środowiska. W związku z tym sieci w chmurze powinny być traktowane jak strefy zdemilitaryzowana, aby zapewnić bezpieczeństwo usług lokalnych.

Strefa DMZ wdraża wirtualne urządzenia sieciowe (urządzeń WUS) w celu zaimplementowania funkcji zabezpieczeń, takich jak zapory i inspekcje pakietów. Ruch przechodzący między aplikacjami lokalnymi i opartymi na chmurze musi przechodzić przez strefę DMZ, w której może być przeprowadzana inspekcja. Połączenia sieci VPN i zasady określające, jaki ruch jest dozwolony w sieci DMZ, są ściśle kontrolowane przez zespoły ds. zabezpieczeń IT.

## <a name="cloud-dmz-assumptions"></a>Założenia strefy DMZ w chmurze

Wdrażanie strefy DMZ w chmurze obejmuje następujące założenia:

- Zespoły zabezpieczeń nie w pełni wyrównania wymagań i zasad dotyczących zabezpieczeń lokalnych i opartych na chmurze.
- Obciążenia oparte na chmurze wymagają dostępu do ograniczonego podzestawu usług hostowanych w sieciach lokalnych lub innych firm, a użytkownicy lub aplikacje w środowisku lokalnym potrzebują ograniczonego dostępu do zasobów hostowanych w chmurze.
- Zaimplementowanie połączenia sieci VPN między sieciami lokalnymi i dostawcą chmury nie jest blokowane przez zasady firmowe, wymagania prawne ani problemy ze zgodnością techniczną.
- Obciążenia nie wymagają wielu subskrypcji w celu obejścia limitów zasobów subskrypcji lub obejmują wiele subskrypcji, ale nie wymagają centralnego zarządzania łącznością lub usługami udostępnionymi używanymi przez zasoby rozproszone w wielu opłaty.

Przed zaimplementowaniem architektury sieci wirtualnych w chmurze DMZ należy wziąć pod uwagę następujące zagadnienia:

- Łączenie sieci lokalnych z sieciami w chmurze zwiększa złożoność wymagań w zakresie zabezpieczeń. Mimo że połączenia między sieciami w chmurze i środowiskiem lokalnym są zabezpieczone, nadal trzeba zapewnić zabezpieczenie zasobów w chmurze. Wszystkie publiczne adresy IP utworzone w celu uzyskania dostępu do obciążeń opartych na chmurze muszą być prawidłowo zabezpieczone przy użyciu publicznej, stałej [strefy DMZ](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz) lub [zapory platformy Azure](/azure/firewall).
- Architektura strefy DMZ w chmurze jest często używana jako trójwymiarowy, podczas gdy łączność jest dodatkowo zabezpieczona i zasady zabezpieczeń są wyrównane między sieciami lokalnymi i w chmurze, co umożliwia szersze wdrażanie architektury sieci hybrydowej w całej skali. Jednak może to dotyczyć również izolowanych wdrożeń z określonymi zabezpieczeniami, tożsamościami i łącznością, które spełniają podejście do obwodu w chmurze.

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat implementowania strefy DMZ w chmurze na platformie Azure, zobacz:

- [Implementowanie strefy DMZ między platformą Azure i lokalnym centrum danych](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid). W tym artykule omówiono sposób implementacji bezpiecznej hybrydowej architektury sieci na platformie Azure.
