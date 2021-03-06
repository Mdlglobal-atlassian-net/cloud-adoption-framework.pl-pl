---
title: Konfigurowanie podstawowych alertów
description: Dowiedz się, w jaki sposób używać usług zarządzania serwerem Azure do konfigurowania alertów i powiadomień, które pomagają zespołom IT poznać wszelkie problemy.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: ecc0dd8b3a91461d5c5d1dd1ce4c062646d974fb
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80430499"
---
# <a name="set-up-basic-alerts"></a>Konfigurowanie podstawowych alertów

Kluczową częścią zarządzania zasobami jest otrzymywanie powiadomień w przypadku wystąpienia problemów. Alerty z wyprzedzeniem powiadamiają o kluczowych warunkach na podstawie wyzwalaczy z metryk, dzienników lub problemów z kondycją usługi. W ramach dołączania usług zarządzania serwerem Azure można skonfigurować alerty i powiadomienia, które pomagają zespołom IT poznać wszelkie problemy.

## <a name="azure-monitor-alerts"></a>Alerty Azure Monitor

Usługa Azure Monitor oferuje funkcje [alertów](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) , które umożliwiają powiadamianie użytkownika za pośrednictwem poczty e-mail lub wiadomości, gdy coś się nie stało. Te możliwości są oparte na wspólnej platformie monitorowania danych, która obejmuje dzienniki i metryki wygenerowane przez serwery i inne zasoby. Korzystając ze wspólnego zestawu narzędzi w Azure Monitor, można analizować dane połączone z wielu zasobów i używać ich do wyzwalania alertów. Te wyzwalacze mogą obejmować:

- Wartości metryk.
- Zapytania wyszukiwania w dzienniku.
- Zdarzenia dziennika aktywności.
- Kondycja podstawowej platformy Azure.
- Testy dostępności witryny sieci Web.

Zapoznaj się z [listą źródeł danych Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) , aby uzyskać bardziej szczegółowy opis źródeł danych monitorowania zbieranych przez tę usługę.

Aby uzyskać szczegółowe informacje dotyczące ręcznego tworzenia alertów i zarządzania nimi za pomocą Azure Portal, zapoznaj się z [dokumentacją Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Zautomatyzowane wdrażanie zalecanych alertów

W tym przewodniku zalecamy utworzenie zestawu 15 alertów na potrzeby podstawowego monitorowania infrastruktury. Znajdź skrypty wdrażania w [repozytorium GitHub usługi Azure alert Toolkit](https://github.com/Microsoft/manageability-toolkits).

Ten pakiet tworzy alerty dla:

- Mało miejsca na dysku
- Niska dostępna pamięć
- Duże użycie procesora CPU
- Nieoczekiwane zamknięcia
- Uszkodzone systemy plików
- Typowe błędy sprzętu

Pakiet używa sprzętu serwera firmy HP jako przykładu. Zmień ustawienia w skojarzonym pliku konfiguracji, aby odzwierciedlić sprzęt producenta OEM. Do pliku konfiguracji można również dodać więcej liczników wydajności. Aby wdrożyć pakiet, uruchom plik New-CoreAlerts. ps1.

## <a name="next-steps"></a>Następne kroki

Informacje o mechanizmach operacji i zabezpieczeń, które obsługują bieżące operacje.

> [!div class="nextstepaction"]
> [Ciągłe zarządzanie i bezpieczeństwo](./ongoing-management-overview.md)
