---
title: Optymalizowanie i przekształcanie
description: Optymalizowanie i przekształcanie
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 5d9ec518069023a8db763a9fc21f7c4847053be6
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807006"
---
# <a name="optimize-and-transform"></a>Optymalizowanie i przekształcanie

Po przeprowadzeniu migracji usług na platformę Azure następnym etapem jest przejrzenie rozwiązania pod kątem możliwych obszarów optymalizacji. Może to obejmować przegląd projektu rozwiązania, dobór wielkości usług oraz analizowanie kosztów.

Ta faza może być również okazją do optymalizacji środowiska i jego ewentualnej transformacji. Na przykład można wykonać migrację metodą „ponownego hostowania”, a po uruchomieniu usług na platformie Azure można ponownie przejrzeć konfigurację rozwiązań lub używane usługi, a także wykonać kilka operacji „refaktoryzacji” w celu modernizacji i zwiększenia funkcjonalności rozwiązania.

# <a name="right-size-assetstaboptimize"></a>[Zasoby o odpowiedniej wielkości](#tab/optimize)

Za pomocą portalu usługi Azure, interfejsu wiersza polecenia lub programu PowerShell można zmienić zakres wszystkich usług platformy Azure, które korzystają z modelu kosztów opartych na użyciu. Pierwszym krokiem podczas prawidłowej zmiany wielkości usługi jest sprawdzenie metryk użycia. Usługa Azure Monitor zapewnia dostęp do tych metryk. Może być konieczne skonfigurowanie kolekcji metryk dla analizowanej usługi i zapewnienie odpowiedniego czasu na zebranie znaczących danych na podstawie wzorców obciążenia.

1. Przejdź do obszaru **Monitor**.
1. Wybierz opcję **Metryki** i skonfiguruj wykres, aby wyświetlić metryki dla usługi przeznaczonej do analizy.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/metrics]" submitText="Go to Monitor" :::

::: zone-end

Poniżej wymieniono niektóre typowe usługi, których wielkość można zmienić.

## <a name="resize-a-virtual-machine"></a>Zmienianie rozmiaru maszyny wirtualnej

Usługa Azure Migrate wykonuje analizę doboru wielkości jako część fazy oceny wstępnej migracji, a rozmiar maszyn wirtualnych migrowanych przy użyciu tego narzędzia zostanie dobrany w zależności od wymagań wstępnej migracji.

Jednak w przypadku maszyn wirtualnych utworzonych lub migrowanych przy użyciu innych metod lub w przypadkach, gdy wymagania dotyczące maszyny wirtualnej po migracji wymagają dopasowania, warto dokładniej dostosować rozmiar maszyny wirtualnej.

1. Przejdź do obszaru **Maszyny wirtualne**.
1. Wybierz wymaganą maszynę wirtualną z listy.
1. Wybierz opcję **Rozmiar** oraz wymagany nowy rozmiar z listy. W celu znalezienia wymaganego rozmiaru może być konieczne dostosowanie filtrów.
1. Wybierz opcję **Zmień rozmiar**.

Należy pamiętać, że zmiana rozmiarów produkcyjnych maszyn wirtualnych może spowodować zakłócenia w działaniu usługi. Spróbuj zastosować prawidłowe rozmiary maszyn wirtualnych przed podwyższeniem ich poziomu do środowiska produkcyjnego.


::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

- [Zarządzanie rezerwacjami zasobów platformy Azure](https://docs.microsoft.com/azure/billing/billing-manage-reserved-vm-instance)
- [Zmienianie rozmiaru maszyny wirtualnej z systemem Windows](https://docs.microsoft.com/azure/virtual-machines/windows/resize-vm)
- [Zmienianie rozmiaru maszyny wirtualnej z systemem Linux przy użyciu interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/virtual-machines/linux/change-vm-size)

W celu sprawdzenia użycia partnerzy mogą skorzystać z Centrum partnerskiego.

- [Ustalanie rozmiarów maszyn wirtualnych Microsoft Azure na potrzeby maksymalnego użycia rezerwacji](https://docs.microsoft.com/partner-center/azure-usage)

::: zone-end

## <a name="resize-a-storage-account"></a>Zmienianie rozmiaru konta magazynu

1. Przejdź do obszaru **Konta magazynu**.
1. Wybierz wymagane konto magazynu.
1. Wybierz opcję **Konfiguruj** i dostosuj właściwości konta magazynu, tak aby odpowiadały Twoim wymaganiom.
1. Wybierz pozycję **Zapisz**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2FStorageAccounts]" submitText="Go to Storage Accounts" :::

::: zone-end

## <a name="resize-a-sql-database"></a>Zmienianie rozmiaru bazy danych SQL

1. Przejdź do obszaru **Bazy danych SQL** lub **Serwery SQL**, a następnie wybierz serwer.
1. Wybierz wymaganą bazę danych.
1. Wybierz opcję **Konfiguruj** oraz wymagany rozmiar nowej warstwy usługi.
1. Wybierz przycisk **Zastosuj**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Sql%2Fservers%2Fdatabases]" submitText="Go to SQL Databases" :::

::: zone-end

# <a name="cost-managementtabmanagecost"></a>[Zarządzanie kosztami](#tab/ManageCost)

Ważne jest, aby przeprowadzić analizę i przegląd kosztów. Zapewnia to możliwość zmiany rozmiaru zasobów w zależności od potrzeb w celu zrównoważenia kosztów i obciążeń.

Usługa Azure Cost Management współdziała z usługą Azure Advisor podczas ustalania zaleceń dotyczących optymalizacji kosztów. Narzędzie Azure Advisor pomaga przeprowadzić optymalizację i zwiększyć wydajność, identyfikując zasoby w stanie bezczynności i niedostatecznie używane.

1. Przejdź do obszaru **Zarządzanie kosztami i rozliczenia**.
1. Wybierz pozycję **Zalecenia doradcy** i kartę **Koszty**.
1. Użyj opcji **Wpływ** i **Potencjalne roczne oszczędności**, aby przejrzeć potencjalne korzyści.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/ModernBillingMenuBlade/Overview]" submitText="Go to Cost Management + Billing" :::

::: zone-end

Możesz również użyć narzędzia **Advisor** i wybrać kartę **Koszty**, aby określić zalecenia dotyczące potencjalnego obniżenia kosztów.

> [!TIP]
> W przypadku usług, które nie wymagają ciągłej dostępności, wdrożenie rozwiązania do uruchamiania, zatrzymywania lub wstrzymania usługi w zależności potrzeb może ułatwić zarządzanie kosztami (na przykład Azure Virtual Machines lub Azure SQL Data Warehouse).
>

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

- [Samouczek: Optymalizowanie kosztów na podstawie zaleceń](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Zapobieganie nieoczekiwanym opłatom za pomocą funkcji rozliczeń i zarządzania kosztami platformy Azure](https://docs.microsoft.com/azure/billing/billing-getting-started)
- [Eksplorowanie kosztów za pomocą funkcji analizy kosztów](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis)

::: zone-end
