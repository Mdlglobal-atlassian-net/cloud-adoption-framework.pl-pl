---
title: Ochrona i odzyskiwanie na platformie Azure
description: Dowiedz się, jak zapewnić stabilność biznesową dzięki skróceniu czasu odzyskiwania i zmniejszeniu prawdopodobieństwa przerwy w działalności.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: bd4a7d64cb6724865faab6ee1d19597368f654fd
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094712"
---
# <a name="protect-and-recover-in-azure"></a>Ochrona i odzyskiwanie na platformie Azure

_Ochrona i odzyskiwanie_ to trzecia i ostatnia dyscyplina każdego planu bazowego zarządzania chmurą.

![Plan bazowy zarządzania chmurą](../../_images/manage/management-baseline.png)

W artykule [Zgodność operacyjna na platformie Azure](./operational-compliance.md) opisano, w jaki sposób można zmniejszyć prawdopodobieństwa przerwania działalności biznesowej. W bieżącym artykule opisano, jak skrócić czas trwania przestojów, którym nie można zapobiec, i jak zmniejszyć ich wpływ na działalność.

Ta tabela zawiera sugerowane wartości minimalne planu bazowego zarządzania dla dowolnego środowiska klasy korporacyjnej:

|Proces  |Narzędzie  |Przeznaczenie  |
|---------|---------|---------|
|Ochrona danych|Azure Backup|Tworzenie kopii zapasowych danych i maszyn wirtualnych w chmurze.|
|Ochrona środowiska|Azure Security Center|Wzmocnienie bezpieczeństwa i zapewnienie zaawansowanej ochrony przed zagrożeniami w ramach obciążeń hybrydowych.|

::: zone target="docs"

## <a name="azure-backup"></a>Azure Backup

::: zone-end
::: zone target="chromeless"

## <a name="azure-backup"></a>[Azure Backup](#tab/UpdbackupateManagement)

::: zone-end

Usługa Azure Backup umożliwia tworzenie kopii zapasowej, ochronę i odzyskiwanie danych w chmurze firmy Microsoft. Usługa Azure Backup pozwala zastąpić dotychczasowe rozwiązania tworzenia kopii zapasowych, istniejące lokalnie lub poza siedzibą firmy, rozwiązaniem opartym na chmurze. To nowe rozwiązanie jest niezawodne, bezpieczne i konkurencyjne. Usługa Azure Backup może również być używana jako jedno, spójne rozwiązanie pomagające chronić i odzyskiwać zasoby lokalne.

### <a name="enable-backup-for-an-azure-vm"></a>Włączanie tworzenia kopii zapasowej maszyny wirtualnej platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Maszyny wirtualne** i wybierz maszynę wirtualną, którą chcesz zreplikować.
1. W okienku **Operacje** wybierz pozycję **Kopia zapasowa**.
1. Utwórz lub wybierz istniejący magazyn usługi Azure Recovery Services.
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

## <a name="azure-site-recovery"></a>[Azure Site Recovery](#tab/siterecovery)

::: zone-end

Azure Site Recovery to krytyczny składnik strategii odzyskiwania po awarii.

Usługa Site Recovery replikuje maszyny wirtualne i obciążenia hostowane w podstawowym regionie świadczenia usługi Azure. Następnie jest wykonywana replikacja do kopii hostowanej w regionie pomocniczym. Gdy w regionie podstawowym wystąpi awaria, nastąpi przełączenie w tryb failover do kopii działającej w regionie pomocniczym. Twoje aplikacje i usługi będą nadal dostępne, ale z regionu pomocniczego. To proaktywne podejście do odzyskiwania może znacznie skrócić czas odzyskiwania. Gdy środowisko odzyskiwania nie będzie już potrzebne, ruch produkcyjny może zostać przywrócony do oryginalnego środowiska.

### <a name="replicate-an-azure-vm-to-another-region-with-site-recovery"></a>Replikowanie maszyny wirtualnej platformy Azure do innego regionu przy użyciu usługi Site Recovery

Poniższe kroki przedstawiają proces replikacji maszyny wirtualnej platformy Azure do innego regionu (replikacja z platformy Azure do platformy Azure) przy użyciu usługi Site Recovery.
>
> [!TIP]
> W zależności od scenariusza dokładne kroki mogą się nieco różnić.
>

### <a name="enable-replication-for-the-azure-vm"></a>Włączanie replikacji maszyny wirtualnej platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Maszyny wirtualne** i wybierz maszynę wirtualną, którą chcesz zreplikować.
1. W okienku **Operacje** wybierz pozycję **Odzyskiwanie po awarii**.
1. Wybierz pozycję **Konfigurowanie odzyskiwania po awarii** > **Region docelowy**, a następnie wybierz region docelowy, do którego ma nastąpić replikacja.
1. Na potrzeby tego przewodnika Szybki start zaakceptuj wartości domyślne dla wszystkich pozostałych opcji.
1. Wybierz pozycję **Włącz replikację**. Spowoduje to uruchomienie zadania włączającego replikację dla maszyny wirtualnej.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="verify-settings"></a>Weryfikowanie ustawień

Po zakończeniu zadania replikacji można sprawdzić stan replikacji, zweryfikować kondycję replikacji i przetestować wdrożenie.

1. W menu maszyny wirtualnej wybierz pozycję **Odzyskiwanie po awarii**.
1. Sprawdź kondycję replikacji, utworzone punkty odzyskiwania oraz regiony źródłowy i docelowy na mapie.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

### <a name="learn-more"></a>Dowiedz się więcej

- [Omówienie usługi Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikowanie maszyny wirtualnej Azure do innego regionu](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)
