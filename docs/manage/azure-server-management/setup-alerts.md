---
title: Konfigurowanie podstawowych alertów
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurowanie podstawowych alertów
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5b11a97e78d5fcd1b2a2cc866f5a7062bc6a2977
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027853"
---
# <a name="set-up-basic-alerts"></a>Konfigurowanie podstawowych alertów

Kluczową częścią zarządzania zasobami jest otrzymywanie powiadomień w przypadku wystąpienia problemów. alerty proaktywnie powiadamiają o warunkach krytycznych. Mogą opierać się na wyzwalaczach z metryk, dzienników lub problemów z kondycją usługi. W ramach dołączania usług zarządzania serwerem Azure można skonfigurować alerty i powiadomienia, które mogą pomóc zespołom IT poznać wszelkie problemy.

## <a name="azure-monitor-alerts"></a>Alerty Azure Monitor

Azure Monitor oferuje [](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) funkcje alertów w celu powiadomienia użytkownika za pośrednictwem poczty e-mail lub wiadomości, gdy coś się nie stało. Te możliwości są oparte na wspólnej platformie monitorowania danych, która obejmuje dzienniki i metryki wygenerowane przez serwery i inne zasoby. Ta platforma pozwala analizować dane połączone z wielu zasobów przy użyciu wspólnego zestawu narzędzi w Azure Monitor, którego można użyć do wyzwalania alertów. Te wyzwalacze mogą obejmować:

- Wartości metryk.
- Zapytania wyszukiwania w dzienniku.
- Zdarzenia dziennika aktywności.
- Kondycja podstawowej platformy Azure.
- Testy dostępności witryny sieci Web.

Zapoznaj się z [listą źródeł danych Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) , aby uzyskać bardziej szczegółowy opis źródeł danych monitorowania zbieranych przez tę usługę.

Aby uzyskać szczegółowe informacje dotyczące ręcznego tworzenia alertów i zarządzania nimi przy użyciu portalu, zapoznaj się z [dokumentacją Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Zautomatyzowane wdrażanie zalecanych alertów

W tym przewodniku zalecamy włączenie zestawu 15 alertów na potrzeby podstawowego monitorowania infrastruktury. Skrypty wdrażania można znaleźć w [repozytorium GitHub usługi Azure alert Toolkit](https://github.com/Microsoft/manageability-toolkits).

Ten pakiet tworzy alerty dotyczące małej ilości miejsca na dysku, małej ilości dostępnej pamięci, dużego użycia procesora CPU, nieoczekiwanych zamknięć, uszkodzonych systemów plików i typowych awarii sprzętu. Pakiet używa sprzętu serwera firmy HP jako przykładu. Należy zmienić ustawienia w skojarzonym pliku konfiguracji, aby odzwierciedlić sprzęt producenta OEM. Do pliku konfiguracji można również dodać więcej liczników wydajności. Aby wdrożyć pakiet, uruchom plik New-CoreAlerts. ps1.

## <a name="next-steps"></a>Następne kroki

Informacje o mechanizmach operacji i zabezpieczeń, które obsługują bieżące operacje.

> [!div class="nextstepaction"]
> [Bieżące zarządzanie i zabezpieczenia](./ongoing-management-overview.md)
