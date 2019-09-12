---
title: Narzędzia i usługi zarządzania serwerem platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia i usługi zarządzania serwerem platformy Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5bf6ed10a69f18fcd1fac7c6597c035877e41d21
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834560"
---
# <a name="azure-server-management-tools-and-services"></a>Narzędzia i usługi zarządzania serwerem platformy Azure

Zgodnie z [omówieniem](/azure/architecture/cloud-adoption/operations/azure-server-management/) tej sekcji pakiet usług Azure Server Management Services obejmuje następujące obszary:

- [Migrate (Migracja)](#migrate)
- [Bezpieczeństwo](#secure)
- [Ochrona](#protect)
- [Monitorowanie](#monitor)
- [Konfigurowanie](#configure)
- [Decydując](#govern)

W poniższych sekcjach krótko opisano te obszary zarządzania i przedstawiono linki do szczegółowej zawartości dotyczącej głównych usług platformy Azure, które je obsługują.

## <a name="migrate"></a>Migrate (Migracja)

Usługi migracji mogą ułatwić Migrowanie obciążeń do platformy Azure. Aby zapewnić najlepsze wskazówki, usługa Azure Migrate rozpoczyna się od mierzenia wydajności serwera lokalnego i oceny przydatności do migracji. Po Azure Migrate zakończeniu oceny można przeprowadzić migrację maszyn lokalnych do platformy Azure za pomocą [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) i [Azure Database Migration Service](/azure/dms/dms-overview) .

## <a name="secure"></a>Bezpieczeństwo

[Azure Security Center](/azure/security-center/security-center-intro) to kompleksowa aplikacja do zarządzania zabezpieczeniami. Dzięki dołączeniu do Security Center można szybko uzyskać ocenę stanu zgodności z zabezpieczeniami i przepisami środowiska. Aby uzyskać instrukcje na temat dołączania serwerów do Azure Security Center, zobacz [Konfigurowanie usług zarządzania platformy Azure dla subskrypcji](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Ochrona

Aby chronić dane, należy zaplanować tworzenie kopii zapasowej, wysoką dostępność, szyfrowanie, autoryzację i pokrewne problemy operacyjne. Te tematy są szeroko omówione w trybie online, dlatego należy skoncentrować się na tworzeniu planu odzyskiwania po awarii firmy (BCDR). Zawieramy odwołania do dokumentacji opisującej szczegółowo, jak zaimplementować i wdrożyć ten typ planu.

Podczas budowania strategii ochrony danych należy najpierw rozważyć rozbicie aplikacji obciążeń na ich różne warstwy, ponieważ każda warstwa zwykle wymaga własnego unikatowego planu ochrony. Aby dowiedzieć się więcej o projektowaniu aplikacji do odporności, zobacz [projektowanie odpornych aplikacji na platformie Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Najbardziej podstawowa ochrona danych to kopia zapasowa. Aby przyspieszyć proces odzyskiwania w przypadku utraty serwera, należy utworzyć kopię zapasową nie tylko danych, ale także konfiguracje serwera. Tworzenie kopii zapasowych jest skutecznym mechanizmem do obsługi przypadkowego usuwania danych i ataku z wykorzystaniem oprogramowania wymuszającego okup. [Azure Backup](https://docs.microsoft.com/azure/backup) może pomóc w ochronie danych na platformie Azure i serwerach lokalnych z systemem Windows lub Linux. Aby uzyskać szczegółowe informacje o możliwościach i przewodnikach związanych z tą usługą, zobacz [dokumentację Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Odzyskiwanie za pomocą kopii zapasowej może zająć dużo czasu. Standard branżowy jest zwykle jeden dzień. Jeśli obciążenie wymaga ciągłości biznesowej w przypadku awarii sprzętu lub awarii centrum danych, należy rozważyć użycie funkcji replikacji. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) zapewnia ciągłą replikację maszyn wirtualnych, rozwiązanie, które zapewnia utratę danych na poziomie systemu operacyjnego. Site Recovery obsługuje również kilka scenariuszy replikacji, takich jak replikacja maszyn wirtualnych platformy Azure między dwoma regionami świadczenia usługi Azure, między serwerami lokalnymi i między środowiskiem lokalnym i platformą Azure. Aby uzyskać więcej informacji, zobacz [kompletna macierz replikacji Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

W przypadku danych serwera plików inna usługa do rozważenia jest [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning). Ta usługa umożliwia scentralizowanie udziałów plików w organizacji w Azure Files przy zachowaniu elastyczności, wydajności i zgodności lokalnego serwera plików. Aby korzystać z tej usługi, postępuj zgodnie z instrukcjami dotyczącymi wdrażania Azure File Sync.

## <a name="monitor"></a>Monitorowanie

[Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) udostępnia widok różnych zasobów, takich jak aplikacje, kontenery i maszyny wirtualne. Gromadzi również dane z kilku źródeł.

- Azure Monitor dla maszyn wirtualnych ([Insights](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)) oferuje szczegółowy widok kondycji maszyny wirtualnej, trendów wydajności i zależności. Usługa monitoruje kondycję systemów operacyjnych maszyn wirtualnych platformy Azure, zestawów skalowania maszyn wirtualnych i maszyn w środowisku lokalnym.
- Log Analytics ([dzienniki](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) to funkcja Azure monitor. Jego rolą jest centralny ogólny scenariusz zarządzania platformy Azure. Służy jako magazyn danych do analizy dzienników i dla wielu innych usług platformy Azure. Oferuje on bogaty język zapytań i aparat analityczny, który zapewnia wgląd w działanie aplikacji i zasobów.
- [Dziennik aktywności platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) jest również funkcją Azure monitor. Zapewnia wgląd w zdarzenia na poziomie subskrypcji występujące na platformie Azure.

## <a name="configure"></a>Konfigurowanie

Kilka usług mieści się w tej kategorii. Mogą one pomóc zautomatyzować zadania operacyjne, zarządzać konfiguracjami serwera, mierzyć zgodność aktualizacji, planować aktualizacje i wykrywać zmiany na serwerach. Te usługi są podstawowe do obsługi bieżących operacji.

- [Update Management](https://docs.microsoft.com/azure/automation/automation-update-management#viewing-update-assessments) automatyzuje wdrażanie poprawek w środowisku, w tym wdrażanie do wystąpień systemu operacyjnego działającego poza platformą Azure. Obsługuje zarówno systemy operacyjne Windows, jak i Linux i śledzi najważniejsze luki w zabezpieczeniach systemu operacyjnego i niezgodności spowodowane przez brakujące poprawki.
- [Change Tracking i spis](https://docs.microsoft.com/azure/automation/change-tracking) zapewniają wgląd w oprogramowanie, które jest uruchomione w danym środowisku, i wyświetla wszystkie zmiany, które wystąpiły.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) umożliwia uruchamianie skryptów Python i PowerShell oraz elementów Runbook w celu zautomatyzowania zadań w środowisku. Korzystając z tego [hybrydowego procesu roboczego elementu Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker), można również rozłożyć elementy Runbook do zasobów lokalnych.
- [Azure Automation konfiguracja stanu](https://docs.microsoft.com/azure/automation/automation-dsc-overview) umożliwia wypychanie konfiguracji stanu żądanego (DSC) programu PowerShell bezpośrednio z platformy Azure. Z kolei Konfiguracja DSC umożliwia monitorowanie i zachowanie konfiguracji systemów operacyjnych gościa i obciążeń.

## <a name="govern"></a>Ład

Przyjęcie i przechodzenie do chmury tworzy nowe wyzwania związane z zarządzaniem i wymaga innego sposób myśleniau podczas zmiany obciążenia zarządzania operacyjnego na monitorowanie i zarządzanie. Struktura wdrażania w chmurze dla platformy Azure zaczyna się od [ładu](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/overview). Wyjaśniono, jak przeprowadzić migrację do chmury, jak będzie wyglądała podróż i która powinna być uwzględniona.

Projekt ładu dla małych firm często różni się od projektowania ładu dla dużych przedsiębiorstw. Aby dowiedzieć się więcej o najlepszych rozwiązaniach dotyczących ładu dla małych i średnich firm, zobacz artykuł [o małym](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/journeys/small-to-medium-enterprise/overview)i średnim przewodniku dotyczącego zarządzania przedsiębiorstwem. Aby dowiedzieć się więcej o najlepszych rozwiązaniach dotyczących ładu dla dużych przedsiębiorstw, zobacz temat [duży Przewodnik dotyczący zarządzania przedsiębiorstwem](https://docs.microsoft.com/azure/architecture/cloud-adoption/governance/journeys/large-enterprise/overview).

## <a name="billing-information"></a>Informacja o rozliczeniach

Aby dowiedzieć się więcej o cenach dla usług zarządzania platformy Azure, przejdź do następujących stron:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Usługa Update Management platformy Azure](https://azure.microsoft.com/pricing/details/automation)

- [Usługa Azure Change Tracking i usługi spisu](https://azure.microsoft.com/pricing/details/automation)

- [Konfiguracja żądanego stanu](https://azure.microsoft.com/pricing/details/automation)

- [Usługa Azure Automation](https://azure.microsoft.com/pricing/details/automation)

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Usługa Azure File Sync](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Rozwiązanie Update Management platformy Azure jest bezpłatne, ale istnieje niewielkie koszty związane z wprowadzaniem danych. Zgodnie z zasadą, pierwsze 5 GB na miesiąc pozyskiwania danych jest bezpłatne. Zwykle obserwujemy, że każda maszyna korzysta z około 25 MB miesięcznie. Dzięki temu około 200 maszyn miesięcznie jest bezpłatnie oferowana. Dla każdego dodatkowego serwera pomnóż liczbę dodatkowych serwerów o 25 MB miesięcznie. Pomnóż, że koszt magazynu dla łącznej ilości magazynu jest wymagany. [Koszty magazynu są dostępne tutaj](https://azure.microsoft.com/pricing/details/storage/). Każdy dodatkowy serwer powinien mieć nominalnyy wpływ na koszt.
