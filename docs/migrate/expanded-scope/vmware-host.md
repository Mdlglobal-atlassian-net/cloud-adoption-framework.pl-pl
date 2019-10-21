---
title: Przyspieszanie migracji przy użyciu hostów VMWare
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przyspieszanie migracji przy użyciu hostów VMWare
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b09c1dcbb36e5f630ca0ae86c95c5c874e29d60b
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558209"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Przyspieszanie migracji przy użyciu hostów VMWare

Migrowanie całego hosta VMWare może przenosić wiele obciążeń i wielu zasobów w ramach jednego wysiłku migracji. Poniższe wskazówki pomogą rozszerzyć zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) za pomocą migracji hosta VMware.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Większość tego nakładu pracy wymaganego do rozwinięcia tego zakresu będzie miała miejsce w ramach wymagań wstępnych i procesów migracji związanych z migracją.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Podczas migrowania pierwszego hosta VMWare na platformę Azure istnieje kilka wymagań wstępnych, które muszą zostać spełnione, aby przygotować wymagania dotyczące tożsamości, sieci i zarządzania. Po spełnieniu tych wymagań wstępnych każdy dodatkowy host powinien wymagać znacznie mniejszego wysiłku do migracji. Te wymagania wstępne są dostosowane do kilku kluczowych wysiłków: Zabezpieczanie środowiska platformy Azure, zarządzania chmurą prywatną i sieci prywatnej chmury.

### <a name="secure-your-azure-environment"></a>Zabezpiecz swoje środowisko platformy Azure

Zaimplementuj odpowiednie rozwiązanie w chmurze dla usług RBAC i łączności sieciowej w środowisku platformy Azure. [Przewodnik po środowisku](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) może pomóc w tej implementacji.

### <a name="private-cloud-management"></a>Zarządzanie chmurą prywatną

Istnieją dwa wymagane zadania i jedno opcjonalne zadanie do ustanowienia zarządzania chmurą prywatną. [Eskalacja uprawnień w chmurze prywatnej](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) oraz [obciążenia DNS i DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) są wymagane najlepsze rozwiązania.

Jeśli celem jest [Migrowanie obciążeń przy użyciu rozproszonych sieci warstwy 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), to trzecie najlepsze rozwiązanie będzie wymagane.

### <a name="private-cloud-networking"></a>Sieć prywatna w chmurze

Po ustaleniu wymagań związanych z zarządzaniem sieci w chmurze prywatnej można nawiązać przy użyciu następujących najlepszych rozwiązań:

- [Połączenie sieci VPN z chmurą prywatną](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokalne połączenie sieciowe z usługą ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Połączenie sieci wirtualnej platformy Azure z usługą ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurowanie rozpoznawania nazw DNS](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integracja z planem wdrażania chmury

Po spełnieniu wymagań wstępnych każdy host VMWare zostanie uwzględniony w [planie wdrożenia chmury](../../plan/template.md). W ramach planu wdrażania chmury należy dodać każdy host do migracji jako [odrębne obciążenie](../../plan/workloads.md). W każdym obciążeniu maszyny wirtualne do migracji mogą być dodawane jako [zasoby](../../plan/workloads.md). Aby przeprowadzić zbiorcze dodawanie obciążeń i zasobów do planu wdrożenia, zobacz [Dodawanie/Edytowanie elementów roboczych w programie Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas każdej iteracji zespół ds. wdrażania działa w zaległościach w celu migrowania obciążeń o najwyższym priorytecie. Proces nie zmienia się w rzeczywistości z hostami VMWare. Gdy następne obciążenie w zaległości jest hostem VMWare, jedyną zmianą będzie użycie narzędzia.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

Poniżej przedstawiono kilka przykładów narzędzi, których można użyć w celu przepracowania migracji:

- [Natywne narzędzia VMWare](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Alternatywnie można migrować obciążenia za pośrednictwem trybu failover odzyskiwania po awarii przy użyciu następujących narzędzi:

- [Tworzenie kopii zapasowych maszyn wirtualnych obciążeń](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Skonfiguruj chmurę prywatną jako lokację odzyskiwania po awarii przy użyciu Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Skonfiguruj chmurę prywatną jako lokację odzyskiwania po awarii przy użyciu programu VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager.md?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Następne kroki

Wróć do [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md), aby upewnić się, że metoda migracji jest w pełni dopasowana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
