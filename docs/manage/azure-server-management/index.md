---
title: Omówienie usług zarządzania serwerem na platformie Azure
description: Wprowadzenie do usług zarządzania serwerem na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d83b84ca63043646591c4e2f5b3e5f82fc53c102
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76808060"
---
# <a name="overview-of-azure-server-management-services"></a>Omówienie usług zarządzania serwerem na platformie Azure

Usługi zarządzania serwerami na platformie Azure zapewniają spójne środowisko zarządzania serwerami na dużą skalę. Te usługi obejmują systemy operacyjne Linux i Windows. Można ich używać w środowiskach produkcyjnych, deweloperskich i testowych. Usługi zarządzania serwerami mogą obsługiwać maszyny wirtualne IaaS platformy Azure, serwery fizyczne i maszyny wirtualne hostowane lokalnie lub w innych środowiskach hostingu.

Pakiet usług zarządzania serwerami na platformie Azure obejmuje usługi przedstawione na poniższym diagramie: ![Diagram modelu operacyjnego platformy Azure](./media/operations-diagram.png)

Ta sekcja przewodnika Microsoft Cloud Adoption Framework zawiera normatywny i umożliwiający podjęcie działań plan wdrażania usług zarządzania serwerami w danym środowisku. Ten plan pomoże w szybkim zorientowaniu na te usługi i przeprowadzi Cię przez przyrostowy zestaw etapów zarządzania dla środowiska o dowolnym rozmiarze.

Dla uproszczenia podzieliliśmy ten przewodnik na trzy etapy:

![Trzy etapy dołączania pakietu zarządzania serwerem platformy Azure](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-server-management-services"></a>Dlaczego warto korzystać z usług zarządzania serwerami na platformie Azure?

Usługi zarządzania serwerami na platformie Azure oferują następujące korzyści:

- **Natywność dla platformy Azure:** Usługi zarządzania serwerami są wbudowane i natywnie zintegrowane z usługą Azure Resource Manager. Te usługi są stale ulepszane w celu dostarczania nowych funkcji i możliwości.
- **Systemy Windows i Linux:** Komputery z systemami Windows i Linux uzyskują takie samo spójne środowisko zarządzania.
- **Hybrydowe:** Usługi zarządzania serwerami obejmują maszyny wirtualne IaaS platformy Azure, a także serwery fizyczne i wirtualne hostowane lokalnie lub w innych środowiskach hostingu.
- **Bezpieczeństwo:** Firma Microsoft przeznacza znaczne zasoby na wszystkie formy zabezpieczeń. Te inwestycje nie tylko zapewniają ochronę infrastruktury platformy Azure. Wynikająca z nich technologia i wiedza są rozszerzane w celu ochrony zasobów klienta, niezależnie od ich lokalizacji.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [narzędziami, usługami i planami](./prerequisites.md) związanymi z wdrożeniem pakietu zarządzania serwerem na platformie Azure.

> [!div class="nextstepaction"]
> [Wstępnie wymagane narzędzia i planowanie](./prerequisites.md)
