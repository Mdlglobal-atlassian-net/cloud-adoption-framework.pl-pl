---
title: Opcje replikacji
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć proces replikacji i przyczynę replikacji migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 584ac5e962c9432e6a1824b3cbb88ff7cb24a35f
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432522"
---
# <a name="replication-options"></a>Opcje replikacji

Przed rozpoczęciem migracji należy się upewnić, że systemy podstawowe są bezpieczne i będą nadal działać bez problemów. Ewentualne przestoje zakłócają pracę użytkowników lub klientów, a także są czasochłonne i kosztowne. Migracja nie polega tylko na wyłączeniu lokalnych maszyn wirtualnych i skopiowaniu ich na platformę Azure. Narzędzia do migracji muszą uwzględniać replikację asynchroniczną lub synchroniczną, aby zagwarantować, że działające systemy będzie można skopiować na platformę Azure bez przestojów. I co najważniejsze, systemy muszą być zsynchronizowane ze swoimi lokalnymi odpowiednikami. Może również zajść potrzeba przetestowania zmigrowanych zasobów w izolowanych partycjach na platformie Azure, aby się upewnić, że obciążenia działają zgodnie z oczekiwaniami.

W zawartości przewodnika Cloud Adoption Framework przyjęto założenie, że usługa Azure Migrate (lub Azure Site Recovery) to najbardziej odpowiednie narzędzie do replikowania zasobów do chmury. Dostępne są jednak również inne opcje. W tym artykule omówiono te opcje, aby ułatwić podjęcie odpowiedniej decyzji.

## <a name="azure-site-recovery-also-known-as-azure-migrate"></a>Usługa Azure Site Recovery (znana również jako Azure Migrate)

Usługa [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) organizuje odzyskiwanie po awarii i zarządza nim w przypadku maszyn wirtualnych platformy Azure, lokalnych maszyn wirtualnych i serwerów fizycznych. Za pomocą usługi Site Recovery można również zarządzać migracją maszyn lokalnych i innych dostawców usług w chmurze na platformę Azure. Replikować można maszyny lokalne na platformę Azure lub maszyny wirtualne platformy Azure do regionu pomocniczego. Następnie można przełączyć maszynę wirtualną z lokacji głównej do pomocniczej i ukończyć proces migracji. Korzystając z usługi Azure Site Recovery, można zrealizować różne scenariusze migracji:

- **Migracja ze środowiska lokalnego na platformę Azure.** Przeprowadzenie migracji lokalnych maszyn wirtualnych VMware, maszyn wirtualnych funkcji Hyper-V oraz serwerów fizycznych na platformę Azure. W tym celu należy wykonać niemal te same czynności co w przypadku pełnego odzyskiwania po awarii. Wystarczy po prostu nie przełączać maszyn z powrotem z platformy Azure do lokacji lokalnej.
- **Migracja między regionami świadczenia usługi Azure.** Przeprowadzanie migracji maszyn wirtualnych platformy Azure między regionami świadczenia usługi Azure. Po zakończeniu migracji należy skonfigurować odzyskiwanie po awarii dla maszyn wirtualnych platformy Azure będących teraz w regionie pomocniczym, do którego przeprowadzono migrację.
- **Migracja z innej chmury na platformę Azure.** Wystąpienia obliczeniowe aprowizowane przez innych dostawców usług w chmurze można migrować do maszyn wirtualnych platformy Azure. Na potrzeby migracji usługa Site Recovery traktuje te wystąpienia jako serwery fizyczne.

![Azure Site Recovery](../../../_images/migrate/asr-replication-image.png)
*Przenoszenie zasobów na platformę Azure lub do innych chmur za pomocą usługi Azure Site Recovery*

Po przeprowadzeniu oceny infrastruktury lokalnej i infrastruktury chmury na potrzeby migracji usługa Azure Site Recovery współtworzy strategię migracji przez replikowanie maszyn lokalnych. Postępując według następujących prostych kroków, możesz skonfigurować migrację lokalnych maszyn wirtualnych, serwerów fizycznych i wystąpień maszyn wirtualnych w chmurze na platformę Azure:

- Weryfikowanie wymagań wstępnych
- Przygotowywanie zasobów platformy Azure
- Przygotowywanie lokalnej maszyny wirtualnej lub wystąpień w chmurze na potrzeby migracji
- Wdrażanie serwera konfiguracji
- Włączanie replikacji maszyn wirtualnych
- Testowanie trybu failover w celu upewnienia się, że wszystkie funkcje działają
- Uruchamianie jednokrotnego przejścia w tryb failover na platformie Azure

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Ta usługa pomaga zmniejszyć złożoność migracji do chmury przez użycie jednej, kompleksowej usługi zamiast wielu narzędzi. Usługa [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) została zaprojektowana jako bezproblemowe i kompleksowe rozwiązanie do przenoszenia lokalnych baz danych SQL Server do chmury. Jest ona w pełni zarządzaną usługą umożliwiającą bezproblemową migrację z wielu źródeł baz danych do platform danych platformy Azure przy minimalnych przestojach. Usługa ta integruje niektóre funkcje istniejących narzędzi i usług, zapewniając klientom kompleksowe rozwiązanie o wysokiej dostępności.

Za pomocą narzędzia Data Migration Assistant usługa generuje raporty z ocenami, które zawierają zalecenia prowadzące użytkownika przez zmiany wymagane przed migracją. Użytkownik decyduje, czy te wymagane zalecenia zostaną wykonane. Gdy wszystko będzie gotowe do rozpoczęcia procesu migracji, usługa Azure Database Migration Service wykona wszystkie skojarzone kroki. Możesz uruchomić proces migracji i spokojnie pozostawić go bez nadzoru, mając pewność, że podczas jego wykonywania zostaną wybrane najlepsze rozwiązania określone przez firmę Microsoft.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu replikacji można rozpocząć [działania dotyczące przemieszczania](./stage.md).

> [!div class="nextstepaction"]
> [Działania dotyczące przemieszczania podczas migracji](./stage.md)
