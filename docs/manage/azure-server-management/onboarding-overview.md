---
title: Dołączanie usług zarządzania serwerem Azure
description: Dołączanie usług zarządzania serwerem Azure z informacjami o maszynach wirtualnych platformy Azure i serwerach lokalnych.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 0396ccaf952bc9d7812304af5d1d9c9952b751cc
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219635"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Faza 2: dołączanie usług zarządzania serwerem Azure

Po zapoznaniu się z [narzędziami](./tools-services.md) i [planowaniem](./prerequisites.md) związanym z usługami zarządzania systemu Azure można przystąpić do drugiej fazy. Faza 2 zawiera wskazówki krok po kroku dotyczące dołączania tych usług do zasobów platformy Azure. Zacznij od oceny tego procesu dołączania przed jego wdrożeniem w środowisku użytkownika.

> [!NOTE]
> Podejścia automatyzacji omówione w kolejnych sekcjach niniejszych wskazówek są przeznaczone dla wdrożeń, które nie mają jeszcze serwerów wdrożonych w chmurze. Wymagają one posiadania roli właściciela w ramach subskrypcji, aby utworzyć wszystkie wymagane zasoby i zasady. Jeśli utworzono już Log Analytics obszary robocze i konta usługi Automation, zalecamy przekazanie tych zasobów do odpowiednich parametrów podczas uruchamiania przykładowych skryptów automatyzacji.

## <a name="onboarding-processes"></a>Procesy dołączania

Ta sekcja wskazówek obejmuje następujące procesy dołączania dla maszyn wirtualnych platformy Azure i serwerów lokalnych:

- **Włącz usługi zarządzania na jednej maszynie wirtualnej do oceny przy użyciu portalu**. Użyj tego procesu, aby zaznajomić się z usługami zarządzania serwerem platformy Azure.
- **Skonfiguruj usługi zarządzania dla subskrypcji przy użyciu portalu**. Ten proces ułatwia skonfigurowanie środowiska platformy Azure w taki sposób, aby wszystkie nowe maszyny wirtualne, które są obsługiwane, automatycznie używały usług zarządzania. Użyj tej metody, jeśli wolisz Azure Portal środowiska w skryptach i wierszach poleceń.
- **Skonfiguruj usługi zarządzania dla subskrypcji przy użyciu Azure Automation**. Ten proces jest w pełni zautomatyzowany. Po prostu Utwórz subskrypcję, a skrypty skonfigurują środowisko do korzystania z usług zarządzania dla nowo zainicjowanej maszyny wirtualnej. Użyj tej metody, jeśli znasz skrypty i szablony Azure Resource Manager programu PowerShell, lub jeśli chcesz się z nimi zapoznać.

Procedury dla każdego z tych podejścia są różne.

> [!NOTE]
> W przypadku korzystania z Azure Portal sekwencja kroków dołączania różni się od zautomatyzowanych kroków dołączania. Portal oferuje prostsze środowisko dołączania.

Na poniższym diagramie przedstawiono zalecany model wdrażania dla usług zarządzania:

![Diagram zalecanego modelu wdrażania](./media/recommended-deployment.png)

Jak pokazano na powyższym diagramie, Agent Log Analytics ma zarówno konfigurację _autorejestrowania_ _, jak_ i konfiguracji niezależną dla serwerów lokalnych:

- **Rejestruj ponownie:** Gdy Agent Log Analytics jest zainstalowany na serwerze i skonfigurowany do łączenia się z obszarem roboczym, rozwiązania, które są włączone w tym obszarze roboczym, są automatycznie stosowane na serwerze.
- **Zgoda na uczestnictwo:** Nawet jeśli Agent jest zainstalowany i połączony z obszarem roboczym, rozwiązanie nie zostanie zastosowane, chyba że zostanie dodane do konfiguracji zakresu serwera w obszarze roboczym.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak dołączać pojedynczą maszynę wirtualną za pomocą portalu, aby oszacować proces dołączania.

> [!div class="nextstepaction"]
> [Dołączanie pojedynczej maszyny wirtualnej platformy Azure do oceny](./onboard-single-vm.md)
