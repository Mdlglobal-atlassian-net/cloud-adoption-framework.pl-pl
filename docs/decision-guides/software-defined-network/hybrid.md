---
title: 'Sieć zdefiniowana przez oprogramowanie: sieć hybrydowa'
description: Omówienie sposobu, w jaki sieci wirtualne umożliwiają łączenie sieci wirtualnych w chmurze z zasobami lokalnymi.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 61ce3447a852ec8aa1caa0737b0f3757f0f26450
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806615"
---
# <a name="software-defined-networking-hybrid-network"></a>Sieć zdefiniowana przez oprogramowanie: sieć hybrydowa

Architektura sieci hybrydowej w chmurze pozwala sieciom wirtualnym uzyskiwać dostęp do zasobów i usług lokalnych oraz na odwrót przy użyciu dedykowanego połączenia sieci WAN, takiego jak ExpressRoute, lub innej metody połączenia w celu bezpośredniego łączenia sieci.

![Sieć hybrydowa](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/expressroute.png)

W przypadku kompilowania natywnej architektury sieci wirtualnej w chmurze, hybrydowa Sieć wirtualna jest izolowana po utworzeniu. Dodanie łączności do środowiska lokalnego umożliwia dostęp do i z sieci lokalnej, mimo że cały ruch przychodzący do zasobów w sieci wirtualnej musi być jawnie dozwolony. Połączenie można zabezpieczyć przy użyciu urządzeń zapory wirtualnej i reguł routingu w celu ograniczenia dostępu lub można określić, które usługi są dostępne między dwiema sieciami przy użyciu natywnych funkcji routingu w chmurze lub wdrażać wirtualne urządzenia sieciowe (urządzeń WUS) na zarządzanie ruchem.

Mimo że architektura sieci hybrydowej obsługuje połączenia sieci VPN, preferowane połączenia WAN, takie jak ExpressRoute, są zalecane z powodu wyższej wydajności i zwiększonego poziomu zabezpieczeń.

## <a name="hybrid-assumptions"></a>Założenia hybrydowe

Wdrożenie hybrydowej sieci wirtualnej obejmuje następujące założenia:

- Zespoły zabezpieczeń IT dostosowane do lokalnych i opartych na chmurze zasad zabezpieczeń sieci w celu zapewnienia, że sieci wirtualne oparte na chmurze mogą być zaufane do bezpośredniego komunikowania się z systemami lokalnymi.
- Obciążenia oparte na chmurze wymagają dostępu do magazynu, aplikacji i usług hostowanych w sieciach lokalnych lub innych firm, a użytkownicy lub aplikacje w lokalnym komputerze muszą mieć dostęp do zasobów hostowanych w chmurze.
- Należy przeprowadzić migrację istniejących aplikacji i usług, które są zależne od zasobów lokalnych, ale nie należy wystawić zasobów na potrzeby ponownego opracowywania, aby usunąć te zależności.
- Łączenie sieci lokalnych z zasobami w chmurze za pośrednictwem sieci VPN lub dedykowanej sieci WAN nie jest blokowane przez zasady firmowe, wymagania dotyczące suwerenności danych ani inne problemy ze zgodnością z przepisami.
- Obciążenia nie wymagają wielu subskrypcji w celu obejścia limitów zasobów subskrypcji lub obciążenia obejmują wiele subskrypcji, ale nie wymagają centralnego zarządzania łącznością lub usługami współdzielonymi używanymi przez zasoby rozproszone w wiele subskrypcji.

Przed zaimplementowaniem implementacji hybrydowej architektury sieci wirtualnej należy wziąć pod uwagę następujące zagadnienia w chmurze:

- Łączenie sieci lokalnych z sieciami w chmurze zwiększa złożoność wymagań w zakresie zabezpieczeń. Obie sieci muszą być zabezpieczone przed zagrożeniami zewnętrznymi i nieautoryzowanym dostępem ze stron środowiska hybrydowego.
- Skalowanie liczby i rozmiaru obciążeń w środowisku chmury hybrydowej może zwiększyć znaczącą złożoność zarządzania routingiem i ruchem.
- Aby zachować spójne zarządzanie w całej organizacji, należy opracować zgodne zasady zarządzania i kontroli dostępu.

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat sieci hybrydowej na platformie Azure, zobacz:

- [Architektura referencyjna sieci hybrydowej](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute). Hybrydowe sieci wirtualne platformy Azure używają obwodu usługi ExpressRoute lub sieci VPN platformy Azure do łączenia sieci wirtualnej z istniejącymi zasobami IT w organizacji, które nie są hostowane na platformie Azure. W tym artykule omówiono opcje tworzenia sieci hybrydowej na platformie Azure.
