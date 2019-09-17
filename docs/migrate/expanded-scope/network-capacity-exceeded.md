---
title: Przekroczono pojemność sieci
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wymagania dotyczące magazynu przekraczają pojemność sieci podczas prac nad migracją.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9b1078cbb6b7ca40b7a38ea56ae803fd61e67449
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024771"
---
# <a name="storage-requirements-exceed-network-capacity-during-a-migration-effort"></a>Wymagania dotyczące magazynu przekraczają pojemność sieci podczas prac nad migracją

Podczas migracji do chmury zasoby są replikowane i synchronizowane przez sieć między istniejącym centrum danych a chmurą. Niektóre wymagania dotyczące wielkości danych różnych obciążeń nie są nietypowe w przypadku przekroczenia pojemności sieci. W takim scenariuszu proces migracji może być częściowo spowolniony lub w niektórych przypadkach całkowicie zatrzymany. Poniższe wskazówki rozszerzają zakres [przewodnika migracji platformy Azure](../azure-migration-guide/index.md) i udostępniają rozwiązanie, które będzie skuteczne w odniesieniu do ograniczeń sieci.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Większość nakładu pracy wymaganego do rozszerzenia tego zakresu będzie potrzebna w ramach procesów wymagań wstępnych, oceniania i realizacji migracji.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

**Weryfikacja obszarów ryzyka związanych z pojemnością sieci:** [Racjonalizacja majątku cyfrowego](../../digital-estate/rationalize.md) jest szczególnie zalecanym warunkiem wstępnym — zwłaszcza, gdy występują problemy z nadmiernym obciążeniem dostępnej pojemności sieci. Podczas racjonalizacji majątku cyfrowego tworzone są [spisy zasobów cyfrowych](../../digital-estate/inventory.md). Spis powinien obejmować istniejące wymagania dotyczące magazynu w ramach majątku cyfrowego. Jak opisano [w obszarach ryzyka związanych z replikacją: Fizyka replikacji](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication)— ten spis może służyć do oszacowania **łącznej wielkości danych migracji**, którą można porównać do całkowitej **dostępnej przepustowości migracji**. Jeśli to porównanie jest niezgodne z wymaganym **czasem na zmianę biznesową**, ten artykuł może pomóc przyspieszyć proces migracji, skracając czas wymagany do przeprowadzenia migracji centrum danych.

**Transfer w trybie offline niezależnych magazynów danych:** Na poniższej ilustracji przedstawiono przykłady transferów danych w trybie online i offline za pomocą urządzenia Azure Data Box. Te metody mogą służyć do dostarczania dużych ilości danych do chmury przed migracją obciążenia. Podczas transferu danych w trybie offline dane źródłowe są kopiowane do urządzenia Azure Data Box. Następnie są one fizycznie dostarczane do firmy Microsoft i przenoszone na konto magazynu Azure w postaci pliku lub obiektu blob. Ten proces może służyć do dostarczania danych, które nie są bezpośrednio powiązane z konkretnym obciążeniem, przed rozpoczęciem innych działań związanych z migracją. Umożliwia to zmniejszenie ilości danych, które muszą zostać dostarczone przez sieć w celu ukończenia migracji, i obejście ograniczeń sieci.

Takie podejście można wykorzystać do transferu danych HDFS, kopii zapasowych, archiwów, serwerów plików, aplikacji itp. Istniejące wskazówki techniczne wyjaśniają, jak używać tego podejścia do transferu danych z [magazynu HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) lub z dysków przy użyciu protokołów [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs) i [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) lub [usługi kopiowania danych](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do urządzenia Data Box.

Istnieją również [rozwiązania partnerskie innych firm](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) wykorzystujące urządzenia Azure Data Box do migracji metodą „Seed and Feed”, w której duża ilość danych jest transferowana w trybie offline; dane te są później synchronizowane w mniejszej skali przez sieć.

![Transfer danych w trybie offline i online za pomocą urządzenia Azure Data Box](../../_images/migrate/databox.png)

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

Jeśli wymagania dotyczące magazynu (lub obciążeń) przekraczają pojemność sieci, urządzenie Azure Data Box może być nadal używane do transferu danych w trybie offline.

Ogólne stanowisko firmy Microsoft polega na tym, że transmisja przez sieć jest podejściem zalecanym, chyba że sieć jest niedostępna. Ta sugestia wynika z szybkości transferu. Transferowanie danych przez sieć (nawet w przypadku ograniczonej przepustowości) jest przeważnie szybsze niż fizyczne dostarczenie tej samej ilości danych przy użyciu mechanizmu transferu w trybie offline, takiego jak urządzenie Data Box.

Jeśli jest dostępna łączność z platformą Azure, należy przeprowadzić analizę przed użyciem urządzenia Data Box, szczególnie jeśli migracja obciążenia jest zależna od czasu. Urządzenie Data Box jest zalecane tylko wtedy, gdy czas przesyłania niezbędnych danych przekracza czas na wypełnienie, dostarczenie i przywrócenie danych przy użyciu urządzenia Data Box.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

**Analiza pojemności sieci:** Jeśli istnieje obawa, że wymagania dotyczące transferu danych związane z obciążeniem mogą przekroczyć pojemność sieci, zespół ds. wdrażania chmury doda do procesu oceny dodatkowe zadanie analizy o nazwie „analiza pojemności sieci”. Podczas tej analizy członek zespołu z doświadczeniem w zakresie zagadnień dotyczących sieci lokalnych i łączności sieciowej oszacuje dostępną pojemność sieci oraz wymaganego czasu transferu danych. Dostępna pojemność zostanie porównana z wymaganiami dotyczącymi magazynu wszystkich zasobów do migracji w bieżącej wersji. Jeśli wymagania dotyczące magazynu przekraczają dostępną przepustowość, zasoby obsługujące obciążenie zostaną wybrane do transferu w trybie offline.

> [!IMPORTANT]
> Po zakończeniu analizy może być konieczne zaktualizowanie planu wydania tak, aby odzwierciedlał czas wymagany do dostarczenia, przywrócenia i zsynchronizowania zasobów przeznaczonych do transferowania w trybie offline.

**Analiza odchylenia:** Każdy zasób, który ma zostać przeniesiony w trybie offline, powinien zostać przeanalizowany pod względem odchyleń w odniesieniu do magazynu i konfiguracji. Odchylenie w odniesieniu do magazynu to liczba zmian w magazynie w określonym czasie. Odchylenie w odniesieniu do konfiguracji to liczba zmian w konfiguracji zasobu w określonym czasie. Od momentu, gdy magazyn zostanie skopiowany do momentu, gdy poziom zasobu zostanie podwyższony do środowiska produkcyjnego, może dojść do utraty odchylenia. Jeśli to odchylenie musi być odzwierciedlone w migrowanym zasobie, wymagana będzie pewna forma synchronizacji między lokalnym a migrowanym zasobem. Należy je oflagować i uwzględnić podczas wykonywania migracji.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

W przypadku korzystania z mechanizmów transferu w trybie offline [procesy replikacji](../migration-considerations/migrate/replicate.md) nie są zwykle wymagane. Natomiast mogą być wymagane [procesy synchronizacji](../migration-considerations/migrate/replicate.md). Interpretacja wyników analizy odchylenia wykonanej podczas procesu oceny umożliwia powiadomienie o zadaniach wymaganych podczas migracji, jeśli zasób jest transferowany w trybie offline.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

**Kopiowanie magazynu:** Takie podejście można wykorzystać do transferu danych HDFS, kopii zapasowych, archiwów, serwerów plików, aplikacji itp. Istniejące wskazówki techniczne wyjaśniają, jak używać tego podejścia do transferu danych z [magazynu HDFS](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) lub z dysków przy użyciu protokołów [SMB](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data), [NFS](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-nfs) i [REST](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-rest) lub [usługi kopiowania danych](https://docs.microsoft.com/azure/databox/data-box-deploy-copy-data-via-copy-service) do urządzenia Data Box.

Istnieją również [rozwiązania partnerskie innych firm](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) wykorzystujące urządzenia Azure Data Box do migracji metodą „Seed and Feed”, w której duża ilość danych jest transferowana w trybie offline; dane są później synchronizowane w mniejszej skali przez sieć.

**Dostarczenie urządzenia:** Po skopiowaniu danych urządzenie można [dostarczyć do firmy Microsoft.](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up) Po otrzymaniu i zaimportowaniu urządzenia dane będą dostępne na koncie magazynu Azure.

**Przywrócenie zasobu:** [Należy sprawdzić dostępność danych](https://docs.microsoft.com/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) na koncie magazynu. Po zweryfikowaniu dane mogą być używane jako obiekty blob lub w usłudze Azure Files. Jeśli dane są plikami VHD/VHDX, plik można przekonwertować na dyski zarządzane. Te dyski zarządzane można następnie zastosować do utworzenia wystąpienia maszyny wirtualnej, która tworzy replikę oryginalnego lokalnego zasobu.

**Synchronizacja:** Jeśli synchronizacja odchylenia jest wymagana dla migrowanego zasobu, dopóki zasób nie zostanie przywrócony do synchronizowania plików można używać jednego z [rozwiązań partnerskich innych firm](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box).

## <a name="optimize-and-promote-process-changes"></a>Zmiany procesu optymalizacji i podwyższania poziomu

Ta zmiana zakresu nie wpłynie na działania optymalizacji.

## <a name="secure-and-manage-process-changes"></a>Zmiany procesu zabezpieczania i zarządzania

Ta zmiana zakresu nie wpłynie na działania zabezpieczania i zarządzania.

## <a name="next-steps"></a>Następne kroki

Wróć do [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md), aby upewnić się, że metoda migracji jest w pełni dopasowana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
