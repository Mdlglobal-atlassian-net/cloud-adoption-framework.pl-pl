---
title: Ochrona i odzyskiwanie na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zapewnianie stabilności biznesowej dzięki skróceniu czasu odzyskiwania
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: a79164435772f571849d0a836f43b53ce3bca087
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557010"
---
# <a name="protect-and-recover-in-azure"></a>Ochrona i odzyskiwanie na platformie Azure

Ochrona i odzyskiwanie to trzecia i ostatnia dyscyplina każdego planu bazowego zarządzania chmurą.

![Plan bazowy zarządzania chmurą](../../_images/manage/management-baseline.png)

W ostatnim artykule „Zgodność operacyjna” opisano, w jaki sposób można zmniejszyć prawdopodobieństwa przerwania działalności biznesowej. W tym artykule „Ochrona i odzyskiwanie” opisano, jak skrócić czas trwania przestojów, którym nie można zapobiec, i jak zmniejszyć ich wpływ na działalność.

Poniższa tabela zawiera sugerowane wartości minimalne planu bazowego zarządzania dla dowolnego środowiska klasy korporacyjnej.

|Proces  |Narzędzie  |Przeznaczenie  |
|---------|---------|---------|
|Ochrona danych|Azure Backup|Tworzenie kopii zapasowych danych i maszyn wirtualnych w chmurze|
|Ochrona środowiska|Azure Security Center|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backuptabupdbackupatemanagement"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Azure Backup to oparta na platformie Azure usługa, która umożliwia tworzenie kopii zapasowej (lub ochronę) i odzyskiwanie danych w chmurze Microsoft Cloud. Usługa Azure Backup pozwala zastąpić dotychczasowe rozwiązania tworzenia kopii zapasowych, istniejące lokalnie lub poza siedzibą firmy, rozwiązaniem opartym na chmurze, które jest niezawodne, bezpieczne i konkurencyjne cenowo. Można jej również używać jako jedno, spójne rozwiązanie do ochrony i odzyskiwania zasobów lokalnych.

### <a name="enable-backup-for-an-azure-vm"></a>Włączanie tworzenia kopii zapasowej maszyny wirtualnej platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Maszyny wirtualne** i wybierz maszynę wirtualną, którą chcesz zreplikować.
1. W obszarze **Operacje** wybierz pozycję **Kopia zapasowa**.
1. Utwórz lub wybierz istniejący magazyn usług Recovery Services.
1. Wybierz pozycję **Utwórz (lub edytuj) nowe zasady**.
1. Skonfiguruj harmonogram i okres przechowywania.
1. Kliknij przycisk **OK**.
1. Wybierz pozycję **Włącz wykonywanie kopii zapasowej**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Omówienie](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)

## <a name="azure-site-recovery"></a>Azure Site Recovery

::: zone-end
::: zone target="chromeless"

## <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery to krytyczny składnik strategii odzyskiwania po awarii.

Usługa Azure Site Recovery umożliwia replikowanie maszyn wirtualnych i obciążeń hostowanych w podstawowym regionie platformy Azure do kopii hostowanej w regionie pomocniczym. Gdy w regionie podstawowym wystąpi awaria, obciążenie można uruchomić w trybie pracy awaryjnej w regionie pomocniczym i nadal uzyskiwać dostęp do aplikacji i usług. To proaktywne podejście do odzyskiwania może znacznie skrócić czas odzyskiwania. Gdy środowisko odzyskiwania nie jest już potrzebne, ruch produkcyjny może zostać przywrócony do oryginalnego środowiska.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikowanie maszyny wirtualnej platformy Azure do innego regionu przy użyciu usługi Site Recovery

Poniższe kroki przedstawiają proces replikacji maszyny wirtualnej platformy Azure do innego regionu (z platformy Azure do platformy Azure) przy użyciu usługi Site Recovery:

>
> [!TIP]
> Zależności od scenariusza dokładne kroki mogą się nieco różnić.
>

### <a name="enable-replication-for-the-azure-vm"></a>Włączanie replikacji maszyny wirtualnej platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Maszyny wirtualne** i wybierz maszynę wirtualną, którą chcesz zreplikować.
1. W obszarze **Operacja** wybierz pozycję **Odzyskiwanie po awarii**.
1. W obszarze **Konfigurowanie odzyskiwania po awarii** > **Region docelowy** wybierz region docelowy, w którym maszyna będzie replikowana.
1. W przypadku tego przewodnika Szybki Start należy zaakceptować ustawienia domyślne.
1. Wybierz pozycję **Włącz replikację**. Spowoduje to uruchomienie zadania włączającego replikację dla maszyny wirtualnej.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Weryfikowanie ustawień

Po zakończeniu zadania replikacji można sprawdzić stan replikacji, zweryfikować kondycję replikacji i przetestować wdrożenie.

1. W menu maszyny wirtualnej wybierz pozycję **Odzyskiwanie po awarii**.
2. Sprawdź kondycję replikacji, utworzone punkty odzyskiwania oraz regiony źródłowy i docelowy na mapie.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

- [Omówienie usługi Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikowanie maszyny wirtualnej Azure do innego regionu](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
