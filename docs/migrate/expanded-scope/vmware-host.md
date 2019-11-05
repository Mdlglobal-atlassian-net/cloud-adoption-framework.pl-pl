---
title: Przyspieszanie migracji przy użyciu hostów VMware
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Przyspieszanie migracji przy użyciu hostów VMware
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 724a227407f431e08b5344dfd1280397bfca9b65
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566883"
---
# <a name="accelerate-migration-with-vmware-hosts"></a>Przyspieszanie migracji przy użyciu hostów VMware

Migrowanie całego hosta VMware może przenosić wiele obciążeń i wielu zasobów w ramach jednego wysiłku migracji. Poniższe wskazówki rozszerzają zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) za pomocą migracji hosta VMware. Większość wysiłku wymaganego do rozwinięcia tego zakresu występuje w ramach wymagań wstępnych i procesów migracji związanych z pracą związanymi z migracją.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Podczas migrowania pierwszego hosta VMware na platformę Azure należy spełnić pewne wymagania wstępne, aby przygotować wymagania dotyczące tożsamości, sieci i zarządzania. Po spełnieniu tych wymagań wstępnych każdy dodatkowy host powinien wymagać znacznie mniejszego wysiłku do migracji. Poniższe sekcje zawierają więcej szczegółowych informacji o wymaganiach wstępnych.

### <a name="secure-your-azure-environment"></a>Zabezpiecz swoje środowisko platformy Azure

Zaimplementuj odpowiednie rozwiązanie w chmurze na potrzeby kontroli dostępu opartej na rolach i łączności sieciowej w środowisku platformy Azure. [Przewodnik po środowisku](https://docs.microsoft.com/azure/vmware-cloudsimple/private-cloud-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) może pomóc w tej implementacji.

### <a name="private-cloud-management"></a>Zarządzanie chmurą prywatną

Istnieją dwa wymagane zadania i jedno opcjonalne zadanie do ustanowienia zarządzania chmurą prywatną. [Eskalacja uprawnień w chmurze prywatnej](https://docs.microsoft.com/azure/vmware-cloudsimple/escalate-privileges?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) oraz [obciążenia DNS i DHCP](https://docs.microsoft.com/azure/vmware-cloudsimple/dns-dhcp-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json) są wymagane najlepsze rozwiązania.

Jeśli celem jest [Migrowanie obciążeń przy użyciu rozproszonych sieci warstwy 2](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-layer-2-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json), ta trzecia Najlepsza Metoda jest również wymagana.

### <a name="private-cloud-networking"></a>Sieć chmury prywatnej

Po ustaleniu wymagań związanych z zarządzaniem można ustanowić sieć prywatną w chmurze, wykonując następujące najlepsze rozwiązania:

- [Połączenie sieci VPN z chmurą prywatną](https://docs.microsoft.com/azure/vmware-cloudsimple/set-up-vpn?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Lokalne połączenie sieciowe z usługą ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Połączenie sieci wirtualnej platformy Azure z usługą ExpressRoute](https://docs.microsoft.com/azure/vmware-cloudsimple/azure-expressroute-connection?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Konfigurowanie rozpoznawania nazw DNS](https://docs.microsoft.com/azure/vmware-cloudsimple/on-premises-dns-setup?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

### <a name="integration-with-the-cloud-adoption-plan"></a>Integracja z planem wdrażania chmury

Po spełnieniu innych wymagań wstępnych należy uwzględnić każdy host VMware w [planie wdrożenia chmury](../../plan/template.md). W ramach planu wdrażania chmury należy dodać każdy host do migracji jako [odrębne obciążenie](../../plan/workloads.md). W każdym obciążeniu Dodaj maszyny wirtualne, które mają zostać zmigrowane jako [zasoby](../../plan/workloads.md). Aby dodać obciążenia i zasoby do planu wdrożenia zbiorczo, zobacz [Dodawanie/Edytowanie elementów roboczych w programie Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas każdej iteracji zespół ds. wdrażania działa w zaległościach w celu migrowania obciążeń o najwyższym priorytecie. Proces nie zmienia się w rzeczywistości z hostami VMware. Gdy następne obciążenie w zaległości jest hostem VMware, jedyną zmianą będzie użycie narzędzia.

W celu przepracowania migracji można użyć następujących narzędzi:

- [Natywne narzędzia VMware](https://docs.microsoft.com/azure/vmware-cloudsimple/migrate-workloads?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Azure Data Box](https://docs.microsoft.com/azure/vmware-cloudsimple/migration-using-azure-data-box?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

Alternatywnie można migrować obciążenia za pośrednictwem trybu failover odzyskiwania po awarii przy użyciu następujących narzędzi:

- [Tworzenie kopii zapasowych maszyn wirtualnych obciążeń](https://docs.microsoft.com/azure/vmware-cloudsimple/backup-workloads-veeam?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Skonfiguruj chmurę prywatną jako lokację odzyskiwania po awarii przy użyciu Zerto](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-zerto?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)
- [Skonfiguruj chmurę prywatną jako lokację odzyskiwania po awarii przy użyciu programu VMware SRM](https://docs.microsoft.com/azure/vmware-cloudsimple/disaster-recovery-site-recovery-manager?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json)

## <a name="next-steps"></a>Następne kroki

Wróć do rozwiniętej listy kontrolnej zakresu, aby upewnić się, że metoda migracji jest w pełni wyrównana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
