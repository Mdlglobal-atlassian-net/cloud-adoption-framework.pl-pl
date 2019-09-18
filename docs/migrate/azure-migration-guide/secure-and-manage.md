---
title: Zabezpieczenia i zarządzanie
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zabezpieczenia i zarządzanie
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: d16af8b5b9c70dfdaf08f7bfe280dbd42ed4f8c7
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022755"
---
# <a name="secure-and-manage"></a>Zabezpieczanie i zarządzanie

Po przeprowadzeniu migracji środowiska na platformę Azure należy wziąć pod uwagę zabezpieczenia i metody używane do zarządzania środowiskiem. Platforma Azure udostępnia wiele funkcji i możliwości w celu spełnienia tych wymagań w rozwiązaniu.

# <a name="azure-monitortabmonitor"></a>[Azure Monitor](#tab/monitor)

Usługa Azure Monitor maksymalizuje dostępność i wydajność aplikacji zapewniając kompleksowe rozwiązanie do zbierania i analizowania danych telemetrycznych ze środowisk chmurowych i lokalnych oraz podejmowania działań w oparciu o nie. Pomaga interpretować działanie aplikacji i proaktywnie identyfikuje problemy dotyczące aplikacji i zasobów, od których zależą.

## <a name="use-and-configure-azure-monitor"></a>Konfigurowanie usługi Azure Monitor i korzystanie z niej

1. Przejdź do obszaru **Monitorowanie** w witrynie Azure Portal.
2. Wybierz widok **Metryki**, **Dzienniki** lub **Kondycja usługi** w celu wyświetlenia ogólnych informacji.
3. Wybierz dowolne ze szczegółowych informacji.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Go to Azure Monitor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Dowiedz się więcej

- [Omówienie usługi Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview)

::: zone-end

# <a name="azure-service-healthtabservicehealth"></a>[Azure Service Health](#tab/servicehealth)

Usługa Azure Service Health udostępnia spersonalizowane wskazówki i pomoc techniczną, gdy napotkasz problemy z usługami platformy Azure. Może ona generować powiadomienia, pomagać zrozumieć znaczenie problemów i informować na bieżąco o rozwiązywaniu problemów. Może też ułatwić przygotowanie się do zaplanowanej konserwacji i zmian, które mogą wpłynąć na dostępność zasobów.

Usługa Azure Service Health udostępnia następujące dane:

- **Stan platformy Azure:** globalny widok kondycji usług platformy Azure.
- **Kondycja usługi:** spersonalizowany widok kondycji usług Azure.
- **Kondycja zasobu:** dokładniejszy widok kondycji poszczególnych zasobów ustanowiowanych przez usługi platformy Azure.

W połączeniu te środowiska umożliwiają uzyskanie pełnego wglądu w kondycję platformy Azure z odpowiednim poziomem szczegółowości.

## <a name="access-service-health"></a>Uzyskiwanie dostępu do usługi Service Health

1. Przejdź do obszaru **Monitorowanie** w witrynie Azure Portal.
2. Wybierz pozycję **Service Health**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Dowiedz się więcej

Aby dowiedzieć się więcej, zapoznaj się z [dokumentacją usługi Azure Service Health](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabadvisor"></a>[Azure Advisor](#tab/advisor)

Azure Advisor to spersonalizowany konsultant w zakresie chmury ułatwiający stosowanie najlepszych rozwiązań w celu zoptymalizowania wdrożeń platformy Azure. Analizuje on konfigurację zasobów i dane telemetryczne użycia. Następnie zaleca rozwiązania ułatwiające zwiększenie wydajności, poprawę bezpieczeństwa oraz zwiększenie wysokiej dostępności zasobów, a także szuka możliwości zmniejszenia ogólnych wydatków związanych z platformą Azure.

## <a name="access-azure-advisor"></a>Uzyskiwanie dostępu do usługi Azure Advisor

1. Przejdź do obszaru **Advisor** w witrynie Azure Portal lub wyszukaj zasób.
2. Wybierz pozycję **Wysoka dostępność**, **Zabezpieczenia**, **Wydajność**, **Koszt**

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Dowiedz się więcej

[Omówienie](https://docs.microsoft.com/azure/advisor/advisor-overview)

::: zone-end

# <a name="azure-security-centertabsecurity"></a>[Azure Security Center](#tab/security)

Usługa Azure Security Center to ujednolicony system zarządzania bezpieczeństwem infrastruktury. Jego zadaniem jest zwiększenie poziomu bezpieczeństwa centrów danych i zapewnienie zaawansowanej ochrony przed zagrożeniami w przypadku obciążeń hybrydowych w chmurze (&mdash;zarówno na platformie Azure, jak i poza nią&mdash;) oraz w środowisku lokalnym.

## <a name="access-azure-security-center"></a>Uzyskiwanie dostępu do usługi Azure Security Center

1. Przejdź do obszaru **Security Center** w witrynie Azure Portal lub wyszukaj zasób.
2. Wybierz pozycję **Rekomendacje**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/0]" submitText="Go to Security Center" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Dowiedz się więcej

[Omówienie](https://docs.microsoft.com/azure/security-center/security-center-intro)

::: zone-end

# <a name="azure-backuptabbackup"></a>[Azure Backup](#tab/backup)

Azure Backup to oparta na platformie Azure usługa, która umożliwia tworzenie kopii zapasowej (lub ochronę) i przywracanie danych w chmurze firmy Microsoft. Usługa Azure Backup pozwala zastąpić dotychczasowe rozwiązania tworzenia kopii zapasowych, istniejące lokalnie lub poza siedzibą firmy, rozwiązaniem opartym na chmurze, które jest niezawodne, bezpieczne i konkurencyjne cenowo.

## <a name="enable-backup-for-an-azure-vm"></a>Włączanie tworzenia kopii zapasowej maszyny wirtualnej platformy Azure

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

::: zone-end

# <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

Wcześniej w tym przewodniku opisano, jak można korzystać z usługi Azure Site Recovery podczas przeprowadzania migracji. Jednak stanowi ona również krytyczny składnik strategii odzyskiwania po awarii po zakończeniu migracji.

Usługa Azure Site Recovery umożliwia replikowanie maszyn wirtualnych i obciążeń hostowanych w podstawowym regionie platformy Azure do kopii hostowanej w regionie pomocniczym. Gdy w regionie podstawowym wystąpi awaria, obciążenie można uruchomić w trybie pracy awaryjnej w regionie pomocniczym i nadal uzyskiwać dostęp do aplikacji i usług. Po ponownym uruchomieniu głównej kopii maszyny wirtualnej można przełączyć obciążenie z powrotem do niej.

## <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replikowanie maszyny wirtualnej platformy Azure do innego regionu przy użyciu usługi Site Recovery

Poniższe kroki przedstawiają proces replikacji maszyny wirtualnej platformy Azure do innego regionu (z platformy Azure do platformy Azure) przy użyciu usługi Site Recovery:

>
> [!TIP]
> Zależności od scenariusza dokładne kroki mogą się nieco różnić.
>

## <a name="enable-replication-for-the-azure-vm"></a>Włączanie replikacji maszyny wirtualnej platformy Azure

1. W witrynie Azure Portal wybierz pozycję **Maszyny wirtualne** i wybierz maszynę wirtualną, którą chcesz zreplikować.
1. W obszarze **Operacja** wybierz pozycję **Odzyskiwanie po awarii**.
1. W obszarze **Konfigurowanie odzyskiwania po awarii** > **Region docelowy** wybierz region docelowy, w którym maszyna będzie replikowana.
1. W przypadku tego przewodnika Szybki Start należy zaakceptować ustawienia domyślne.
1. Wybierz pozycję **Włącz replikację**. Spowoduje to uruchomienie zadania włączającego replikację dla maszyny wirtualnej.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

## <a name="verify-settings"></a>Weryfikowanie ustawień

Po zakończeniu zadania replikacji można sprawdzić stan replikacji, zweryfikować kondycję replikacji i przetestować wdrożenie.

1. W menu maszyny wirtualnej wybierz pozycję **Odzyskiwanie po awarii**.
2. Sprawdź kondycję replikacji, utworzone punkty odzyskiwania oraz regiony źródłowy i docelowy na mapie.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Dowiedz się więcej

- [Omówienie usługi Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
- [Replikowanie maszyny wirtualnej Azure do innego regionu](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart)

::: zone-end
