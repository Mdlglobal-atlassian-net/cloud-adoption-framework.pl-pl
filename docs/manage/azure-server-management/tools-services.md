---
title: Usługi zarządzania serwerami na platformie Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o obszarach w ramach pakietu usług zarządzania serwerem platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7050b4b40508f9ac133322600625e016c270bb15
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219567"
---
# <a name="azure-server-management-tools-and-services"></a>Narzędzia i usługi zarządzania serwerem platformy Azure

Zgodnie z [omówieniem](./index.md) tych wskazówek, pakiet usług zarządzania serwerem platformy Azure obejmuje następujące zagadnienia:

- Migrate (Migracja)
- Bezpieczeństwo
- Ochrona
- Monitorowanie
- Konfigurowanie
- Ład

W poniższych sekcjach krótko opisano te obszary zarządzania i przedstawiono linki do szczegółowej zawartości dotyczącej głównych usług platformy Azure, które je obsługują.

## <a name="migrate"></a>Migrate (Migracja)

Usługi migracji mogą ułatwić Migrowanie obciążeń do platformy Azure. Aby zapewnić najlepsze wskazówki, usługa Azure Migrate rozpoczyna się od mierzenia wydajności serwera lokalnego i oceny przydatności do migracji. Po Azure Migrate zakończeniu oceny można przeprowadzić migrację maszyn lokalnych do platformy Azure za pomocą [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) i [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) .

## <a name="secure"></a>Bezpieczeństwo

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) to kompleksowa aplikacja do zarządzania zabezpieczeniami. Dzięki dołączeniu do Security Center można szybko uzyskać ocenę stanu zgodności z zabezpieczeniami i przepisami środowiska. Aby uzyskać instrukcje na temat dołączania serwerów do Azure Security Center, zobacz [Konfigurowanie usług zarządzania platformy Azure dla subskrypcji](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Ochrona

Aby chronić dane, należy zaplanować tworzenie kopii zapasowej, wysoką dostępność, szyfrowanie, autoryzację i pokrewne problemy operacyjne. Te tematy są szeroko omówione w trybie online, dlatego należy skoncentrować się na tworzeniu planu ciągłości biznesowej i odzyskiwania po awarii (BCDR). Zawieramy odwołania do dokumentacji opisującej szczegółowo, jak zaimplementować i wdrożyć ten typ planu.

Podczas budowania strategii ochrony danych należy najpierw rozważyć rozdzielenie aplikacji obciążeń na ich różne warstwy. Takie podejście jest pomocne, ponieważ każda warstwa zazwyczaj wymaga własnego unikatowego planu ochrony. Aby dowiedzieć się więcej o projektowaniu aplikacji do odporności, zobacz [projektowanie odpornych aplikacji na platformie Azure](https://docs.microsoft.com/azure/architecture/resiliency).

Najbardziej podstawowa ochrona danych to kopia zapasowa. Aby przyspieszyć proces odzyskiwania w przypadku utraty serwerów, Utwórz kopię zapasową nie tylko danych, ale także konfiguracje serwera. Tworzenie kopii zapasowych jest skutecznym mechanizmem do obsługi przypadkowego usuwania danych i ataku z wykorzystaniem oprogramowania wymuszającego okup. [Azure Backup](https://docs.microsoft.com/azure/backup) może pomóc w ochronie danych na platformie Azure i serwerach lokalnych z systemem Windows lub Linux. Aby uzyskać szczegółowe informacje o tym, co można zrobić, zobacz [dokumentację Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Odzyskiwanie za pomocą kopii zapasowej może zająć dużo czasu. Standard branżowy jest zwykle jeden dzień. Jeśli obciążenie wymaga ciągłości biznesowej w przypadku awarii sprzętu lub awarii centrum danych, należy rozważyć użycie funkcji replikacji. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) zapewnia ciągłą replikację maszyn wirtualnych, rozwiązanie, które zapewnia utratę danych na poziomie systemu operacyjnego. Site Recovery obsługuje również kilka scenariuszy replikacji, takich jak replikacja:

- Maszyn wirtualnych platformy Azure między dwoma regionami świadczenia usługi Azure.
- Między serwerami lokalnymi.
- Między serwerami lokalnymi i platformą Azure.

Aby uzyskać więcej informacji, zobacz [kompletna macierz replikacji Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

W przypadku danych na serwerze plików można [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)inne usługi. Ta usługa ułatwia scentralizowanie udziałów plików w organizacji w Azure Files przy zachowaniu elastyczności, wydajności i zgodności lokalnego serwera plików. Aby korzystać z tej usługi, postępuj zgodnie z instrukcjami dotyczącymi wdrażania Azure File Sync.

## <a name="monitor"></a>Monitorowanie

[Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) udostępnia widok różnych zasobów, takich jak aplikacje, kontenery i maszyny wirtualne. Gromadzi również dane z kilku źródeł:

- [Azure monitor dla maszyn wirtualnych](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) zapewnia szczegółowy widok kondycji maszyny wirtualnej, trendów wydajności i zależności. Usługa monitoruje kondycję systemów operacyjnych maszyn wirtualnych platformy Azure, zestawów skalowania maszyn wirtualnych i maszyn w środowisku lokalnym.
- [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview) jest funkcją Azure monitor. Jego rolą jest centralny ogólny scenariusz zarządzania platformy Azure. Służy jako magazyn danych do analizy dzienników i dla wielu innych usług platformy Azure. Oferuje on bogaty język zapytań i aparat analityczny, który zapewnia wgląd w działanie aplikacji i zasobów.
- [Dziennik aktywności platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) jest również funkcją Azure monitor. Zapewnia wgląd w zdarzenia na poziomie subskrypcji występujące na platformie Azure.

## <a name="configure"></a>Konfigurowanie

Kilka usług mieści się w tej kategorii. Mogą one ułatwić:

- Automatyzowanie zadań operacyjnych.
- Zarządzanie konfiguracjami serwera.
- Mierzenie zgodności aktualizacji.
- Zaplanuj aktualizacje.
- Wykrywaj zmiany na serwerach.

Te usługi są niezbędne do obsługi bieżących operacji:

- [Update Management](https://docs.microsoft.com/azure/automation/automation-update-management) automatyzuje wdrażanie poprawek w środowisku, w tym wdrażanie w wystąpieniach systemu operacyjnego działającego poza platformą Azure. Obsługuje systemy operacyjne Windows i Linux oraz śledzi najważniejsze luki w zabezpieczeniach systemu operacyjnego i niezgodności spowodowane przez brakujące poprawki.
- [Change Tracking i spis](https://docs.microsoft.com/azure/automation/change-tracking) zapewniają wgląd w oprogramowanie, które jest uruchomione w danym środowisku, i wyróżnia wszystkie zmiany, które wystąpiły.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) umożliwia uruchamianie skryptów Python i PowerShell oraz elementów Runbook w celu zautomatyzowania zadań w środowisku. W przypadku korzystania z usługi Automation z [hybrydowym procesem roboczym elementu Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)można także rozciągnąć elementy Runbook do zasobów lokalnych.
- [Azure Automation konfiguracja stanu](https://docs.microsoft.com/azure/automation/automation-dsc-overview) umożliwia wypychanie konfiguracji stanu żądanego (DSC) programu PowerShell bezpośrednio z platformy Azure. Konfiguracja DSC umożliwia również monitorowanie i zachowywanie konfiguracji dla systemów operacyjnych gościa i obciążeń.

## <a name="govern"></a>Ład

Przyjęcie i przejście do chmury powoduje utworzenie nowych wyzwań związanych z zarządzaniem. Wymaga innego sposób myśleniau podczas zmiany obciążenia związanego z zarządzaniem operacyjną na monitorowanie i zarządzanie. Struktura wdrażania w chmurze dla platformy Azure zaczyna się od [ładu](../../govern/index.md). W ramach struktury wyjaśniono, jak przeprowadzić migrację do chmury, jak będzie wyglądała podróż i kto ma być uwzględniony.

Projekt dotyczący zarządzania organizacjami standardowymi często różni się od projektowania ładu dla złożonych przedsiębiorstw. Aby dowiedzieć się więcej o najlepszych rozwiązaniach dotyczących ładu dla standardowej organizacji, zobacz [Standardowy Przewodnik dotyczący zarządzania przedsiębiorstwem](../../govern/guides/standard/index.md). Aby dowiedzieć się więcej o najlepszych rozwiązaniach dotyczących ładu dla złożonego przedsiębiorstwa, zobacz Przewodnik dotyczący [ładu dla złożonych przedsiębiorstw](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Informacje o rozliczeniach

Aby dowiedzieć się więcej o cenach dla usług zarządzania platformy Azure, przejdź do następujących stron:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure Automation](https://azure.microsoft.com/pricing/details/automation), w tym:
  - Desired State Configuration
  - Usługa Update Management platformy Azure
  - Usługa Azure Change Tracking i usługi spisu

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Usługa Azure File Sync](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> Rozwiązanie Update Management platformy Azure jest bezpłatne, ale istnieje niewielkie koszty związane z wprowadzaniem danych. Zgodnie z zasadą, pierwsze 5 gigabajtów (GB) na miesiąc pozyskiwania danych są bezpłatne. Zwykle obserwujemy, że każda maszyna korzysta z około 25 MB miesięcznie. Tak więc około 200 maszyn miesięcznie jest bezpłatnych. Aby uzyskać więcej serwerów, pomnóż liczbę dodatkowych serwerów o 25 MB miesięcznie. Następnie pomnóż wynik przez cenę magazynu dla dodatkowego magazynu, którego potrzebujesz. Aby uzyskać informacje o kosztach, zobacz [Cennik usługi Azure Storage — Omówienie](https://azure.microsoft.com/pricing/details/storage). Każdy dodatkowy serwer ma zwykle nominalnyy wpływ na koszt.
