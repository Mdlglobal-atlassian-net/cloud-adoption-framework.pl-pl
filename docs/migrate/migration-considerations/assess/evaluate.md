---
title: Ocena gotowości obciążeń
description: Dowiedz się, co jest potrzebne do oszacowania gotowości obciążenia do migracji do chmury. Dowiesz się, jak sprawdzać poprawność wszystkich zasobów i skojarzonych zależności.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4321cf289bcab6fbee061fbff27d45fd8d695eac
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432791"
---
# <a name="evaluate-workload-readiness"></a>Ocena gotowości obciążeń

To działanie koncentruje się na ocenie gotowości obciążenia do migracji do chmury. W trakcie tego działania zespół wdrożeniowy ds. chmury weryfikuje, czy wszystkie zasoby i skojarzone zależności są zgodne z wybranym modelem wdrażania i dostawcą chmury. W trakcie procesu zespół dokumentuje wszelkie działania wymagane do [skorygowania](../migrate/remediate.md) problemów ze zgodnością.

## <a name="evaluation-assumptions"></a>Założenia oceny

Większość zasad dotyczących omawiania zawartości w strukturze wdrażania w chmurze to niezależny od w chmurze. Jednak proces oceny gotowości musi być w dużej mierze specyficzny dla każdej konkretnej platformy w chmurze. W poniższych wskazówkach przyjęto założenie zamiaru migracji na platformę Azure. Przyjęto również, że dla [działań związanych z replikacją](../migrate/replicate.md) używana jest usługa Azure Migrate (znana również jako usługa Azure Site Recovery). Aby zapoznać się z alternatywnymi narzędziami, zobacz [opcje replikacji](../migrate/replicate-options.md).

W tym artykule nie są przechwytywane wszystkie możliwe działania ewaluacyjne. Zakłada się, że każde środowisko i wynik biznesowy będą określać specyficzne wymagania. Aby przyspieszyć tworzenie tych wymagań, w pozostałej części tego artykułu opisano kilka typowych działań oceny związanych z oceną [infrastruktury](#common-infrastructure-evaluation-activities), [bazy danych](#common-database-evaluation-activities) i [sieci](#common-network-evaluation-activities).

## <a name="common-infrastructure-evaluation-activities"></a>Typowe działania oceny infrastruktury

- Wymagania dotyczące oprogramowania VMware: [zapoznaj się z wymaganiami Azure Site Recovery dla programu VMware](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix).
- Wymagania dotyczące funkcji Hyper-V: [zapoznaj się z wymaganiami dotyczącymi Azure Site Recovery funkcji Hyper-v](https://docs.microsoft.com/azure/site-recovery/hyper-v-azure-support-matrix).

Pamiętaj o udokumentowaniu wszelkich rozbieżności w konfiguracji hosta, konfiguracji zreplikowanej maszyny wirtualnej, wymaganiach dotyczących magazynu lub konfiguracji sieci.

## <a name="common-database-evaluation-activities"></a>Typowe działania oceny bazy danych

- Udokumentowanie celów punktu odzyskiwania i celów czasu odzyskiwania bieżącego wdrożenia bazy danych. Są one używane w [działaniach dotyczących architektury](./architect.md) w celu ułatwienia podejmowania decyzji.
- Udokumentowanie wszelkich wymagań dotyczących konfiguracji o wysokiej dostępności. Aby uzyskać pomoc dotyczącą wymagań programu SQL Server, zobacz [Przewodnik po rozwiązaniach wysokiej dostępności programu SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).
- Ocena zgodności rozwiązań PaaS. [Przewodnik migracji danych platformy Azure](https://datamigration.microsoft.com) mapuje lokalne bazy danych na zgodne rozwiązania PaaS platformy Azure, takie jak [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) lub [Azure DB](https://docs.microsoft.com/azure/sql-database) dla [MySQL](https://docs.microsoft.com/azure/mysql), [PostgreSQL](https://docs.microsoft.com/azure/postgresql)lub [MariaDB](https://docs.microsoft.com/azure/mariadb).
- Gdy zgodność rozwiązań PaaS jest opcją bez konieczności korygowania, należy skonsultować się z zespołem odpowiedzialnym za [działania dotyczące architektury](./architect.md). Migracje PaaS mogą zapewnić znaczną oszczędność czasu i obniżyć całkowity koszt posiadania w przypadku większości rozwiązań w chmurze.
- Jeśli zgodność rozwiązań PaaS jest opcją, ale wymagane jest korygowanie, należy skonsultować się z zespołami odpowiedzialnymi za [działania dotyczące architektury](./architect.md) i [działania korygujące](../migrate/remediate.md). W wielu scenariuszach korzyści z migracji PaaS dla rozwiązań baz danych mogą przeważać nad zwiększeniem czasu korygowania.
- Udokumentowanie rozmiaru i szybkości zmian dla każdej bazy danych, która ma zostać poddana migracji.
- Jeśli to możliwe, należy udokumentować wszystkie aplikacje lub inne zasoby, które wykonują wywołania do poszczególnych baz danych.

> [!NOTE]
> Synchronizacja dowolnego zasobu zużywa przepustowość podczas procesów replikacji. Bardzo powszechnym błędem jest przeoczenie zużycia przepustowości wymaganego do utrzymania synchronizacji zasobów między punktem replikacji a wydaniem. Bazy danych są typowymi konsumentami przepustowości podczas cykli wydania, a szczególnie dotyczy to baz danych z dużymi magazynami lub dużą częstotliwością zmian. Należy rozważyć podejście polegające na replikowaniu struktury danych, z kontrolowanymi aktualizacjami przed testowaniem akceptacyjnym przez użytkowników i wydaniem. W takich scenariuszach alternatywy dla usługi Azure Site Recovery mogą być bardziej odpowiednie. Aby uzyskać więcej informacji, zobacz wskazówki w [przewodniku po migracji danych na platformę Azure](https://datamigration.microsoft.com).

## <a name="common-network-evaluation-activities"></a>Typowe działania oceny sieci

- Obliczenie całkowitej ilości miejsca do magazynowania dla wszystkich maszyn wirtualnych, które mają być replikowane podczas iteracji prowadzących do wydania.
- Obliczenie wartości dryfu lub zmiany ilości miejsca w magazynie dla wszystkich maszyn wirtualnych, które mają być replikowane podczas iteracji prowadzących do wydania.
- Obliczenie wymagań dotyczących przepustowości dla każdej iteracji przez zsumowanie całkowitej ilości miejsca do magazynowania i dryfu.
- Obliczenie niewykorzystanej przepustowości dostępnej w bieżącej sieci do zweryfikowania na wyrównanie iteracji.
- Udokumentowanie przepustowości potrzebnej do osiągnięcia przewidywanej prędkości migracji. Jeśli w celu zapewnienia wymaganej przepustowości konieczne są jakiekolwiek działania korygujące, należy powiadomić zespół odpowiedzialny za [działania korygujące](../migrate/remediate.md).

> [!NOTE]
> Całkowita ilość miejsca do magazynowania bezpośrednio wpływa na wymagania dotyczące przepustowości podczas replikacji początkowej. Jednak dryf magazynu będzie kontynuowany od punktu replikacji do momentu wydania. Oznacza to, że dryf ma skumulowany wpływ na dostępną przepustowość.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu oceny systemu dane wyjściowe posłużą do opracowania nowej [architektury chmury](./architect.md).

> [!div class="nextstepaction"]
> [Definiowanie architektury obciążeń przed migracją](./architect.md)
