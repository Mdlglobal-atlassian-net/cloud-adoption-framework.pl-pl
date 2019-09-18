---
title: Omówienie usług zarządzania serwerem na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do usług zarządzania serwerem na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4d1ada9d47e54f4b0d3828ce93b2d55f3eda8a34
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026372"
---
# <a name="overview-of-azure-server-management-services"></a>Omówienie usług zarządzania serwerem na platformie Azure

Usługi zarządzania serwerem na platformie Azure zapewniają klientom spójne środowisko zarządzania serwerami na dużą skalę. Usługi te obejmują systemy operacyjne Linux i Windows i mogą być używane w środowisku produkcyjnym, programistycznym i testowym. Ponadto mogą obsługiwać maszyny wirtualne IaaS platformy Azure, serwery fizyczne i maszyny wirtualne hostowane lokalnie lub w innych środowiskach hostingu. 

Pakiet usług zarządzania serwerem na platformie Azure obejmuje usługi przedstawione na poniższym diagramie. 

![Diagram modelu operacyjnego platformy Azure](./media/operations-diagram.png)

Wskazówki w tej sekcji przewodnika Microsoft Cloud Adoption Framework opisują normatywny i umożliwiający podjęcie działań plan wdrażania usług zarządzania serwerem w danym środowisku. Ten plan pomoże w szybkim zorientowaniu na te usługi i przeprowadzi Cię przez przyrostowy zestaw etapów zarządzania dla środowiska o dowolnym rozmiarze.

Dla uproszczenia podzieliliśmy ten przewodnik na trzy etapy:

![Trzy etapy dołączania pakietu zarządzania serwerem platformy Azure](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-management-services"></a>Dlaczego warto używać usług zarządzania platformy Azure?

Usługi zarządzania platformy Azure oferują następujące korzyści:

- **Natywność dla platformy Azure.** Usługi zarządzania są wbudowane i natywnie zintegrowane z usługą Azure Resource Manager. Te usługi są stale ulepszane w celu dostarczania nowych funkcji i możliwości.
- **Systemy Windows i Linux**. Komputery z systemami Windows i Linux mają takie samo spójne środowisko zarządzania.
- **Hybryda.** Usługi zarządzania obejmują maszyny wirtualne IaaS platformy Azure, a także serwery fizyczne i wirtualne hostowane lokalnie lub w innych środowiskach hostingu.
- **Bezpieczeństwo.** Firma Microsoft przeznacza znaczne zasoby na wszystkie formy zabezpieczeń. Te inwestycje nie tylko zapewniają ochronę chmurowej infrastruktury platformy Azure. Wynikająca z nich technologia i wiedza są rozszerzane w celu ochrony zasobów klienta, niezależnie od ich lokalizacji.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [narzędziami, usługami i planami](./prerequisites.md) związanymi z wdrożeniem pakietu zarządzania serwerem na platformie Azure.

> [!div class="nextstepaction"]
> [Wstępnie wymagane narzędzia i planowanie](./prerequisites.md)
