---
title: Dołączanie do usług zarządzania serwerem Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dołączanie do usług zarządzania serwerem Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 330e297b4fb63eaa376e8b6dac0ccf77c2a16ef4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825135"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Etap 2: Dołączanie usług zarządzania serwerem Azure

Gdy znasz [Narzędzia](./tools-services.md) i [Planowanie](./prerequisites.md) związane z usługami zarządzania platformy Azure, możesz przystąpić do drugiej fazy, która zawiera wskazówki krok po kroku dotyczące dołączania tych usług do zasobów platformy Azure. Zacznij od oceny tego procesu dołączania przed jego wdrożeniem w środowisku użytkownika.

> [!NOTE]
> Podejścia automatyzacji omówione w kolejnych sekcjach niniejszych wskazówek są przeznaczone dla wdrożeń, które nie mają jeszcze serwerów wdrożonych w chmurze. Wymagają one posiadania roli właściciela w ramach subskrypcji, aby utworzyć wszystkie wymagane zasoby i zasady. Jeśli masz już Log Analytics obszar roboczy i zasoby konta usługi Automation, zalecamy przekazanie tych zasobów do odpowiednich parametrów podczas uruchamiania przykładowych skryptów automatyzacji.

## <a name="onboarding-processes"></a>Procesy dołączania

Ta sekcja wskazówek obejmuje następujące procesy dołączania dla maszyn wirtualnych platformy Azure i serwerów lokalnych:

- **Włącz usługi zarządzania na jednej maszynie wirtualnej do oceny przy użyciu portalu**. Użyj tego procesu, aby zaznajomić się z usługami zarządzania serwerem platformy Azure.
- **Skonfiguruj usługi zarządzania dla subskrypcji przy użyciu portalu**. Ten proces ułatwia skonfigurowanie środowiska platformy Azure w taki sposób, aby wszystkie nowe maszyny wirtualne, które są obsługiwane, automatycznie używały usług zarządzania. Użyj tej metody, jeśli wolisz Azure Portal środowiska w skryptach i wierszach poleceń.
- **Skonfiguruj usługi zarządzania dla subskrypcji przy użyciu Azure Automation**. Ten proces jest w pełni zautomatyzowany. Wystarczy utworzyć subskrypcję, a skrypty skonfigurują środowisko do korzystania z usług zarządzania dla nowo zainicjowanej maszyny wirtualnej. Użyj tej metody, jeśli znasz skrypty programu PowerShell i szablony Azure Resource Manager lub chcesz poznać ich użycie.

Procedury dla każdego z tych podejścia są różne.

> [!NOTE]
> Sekwencja kroków dołączania w przypadku korzystania z Azure Portal różni się od zautomatyzowanych kroków dołączania, ponieważ Portal oferuje prostsze środowisko dołączania.

Na poniższym diagramie przedstawiono zalecany model wdrażania dla usług zarządzania. 

![Diagram zalecanego modelu wdrażania](./media/recommended-deployment.png)

> [!NOTE]
> Jak pokazano na powyższym diagramie, Agent Log Analytics ma *zarówno konfigurację* autorejestrowania, jak i konfiguracji *automatycznej* dla serwerów lokalnych. *Automatyczne rejestrowanie* oznacza, że gdy Agent usługi log Analytics jest zainstalowany na serwerze i skonfigurowany do łączenia się z obszarem roboczym, rozwiązania włączone w tym obszarze roboczym zostaną automatycznie zastosowane do serwera programu. *Zgoda* oznacza, że nawet jeśli Agent jest zainstalowany i połączony z obszarem roboczym, rozwiązanie nie zostanie zastosowane, chyba że zostanie dodane do konfiguracji zakresu serwera w obszarze roboczym.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak dołączać pojedynczą maszynę wirtualną za pomocą portalu, aby oszacować proces dołączania.

> [!div class="nextstepaction"]
> [Dołączanie pojedynczej maszyny wirtualnej platformy Azure do oceny](./onboard-single-vm.md)
