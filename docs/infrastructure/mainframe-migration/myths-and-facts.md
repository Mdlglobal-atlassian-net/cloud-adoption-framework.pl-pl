---
title: 'Migracja komputera mainframe: mitów i fakty'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migruj aplikacje ze środowisk mainframe na platformę Azure, czyli sprawdzoną, wysoce dostępną i skalowalną infrastrukturę dla systemów, które obecnie działają na komputerach mainframe.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4adf229b1ffca1d1360d197ab09a04f0d9584ef8
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547921"
---
# <a name="mainframe-myths-and-facts"></a>Mitów i fakty komputera mainframe

Komputery mainframe są widoczne w sposób wyraźny w historii obliczeń i nie są przeznaczone do obsługi wysoce określonych obciążeń. Większość wyrazów, że Komputery mainframe są sprawdzoną platformą z długotrwałymi procedurami operacyjnymi, które sprawiają, że są niezawodne, niezawodne środowiska. Na potrzeby obciążeń zwrotnych są dostępne oprogramowanie oparte na użyciu, mierzone w milionu instrukcji na sekundę (MIPS).

Niezawodność, dostępność i moc obliczeniowa komputerów mainframe podjęto na prawie Mythical. Aby oszacować obciążenia komputera mainframe, które są najbardziej odpowiednie dla platformy Azure, najpierw należy rozróżnić mitów od rzeczywistości.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Omówienia: Komputery mainframe nigdy nie przechodzą i mają co najmniej pięć 9 dostępności

Sprzęt komputerowy i systemy operacyjne są wyświetlane jako niezawodne i stabilne. Jednak ma to na celu zaplanowanie przestojów i ponownych uruchomień (nazywanych początkowymi ładowaniami programu lub IPLs). Gdy te zadania są brane pod uwagę, rozwiązanie mainframe często ma więcej niż dwie lub trzy 9e dostępności, co jest równoznaczne z tym, że serwery z technologią wysokiej klasy są oparte na architekturze Intel.

Komputery mainframe również pozostają jako podatne na awarie jako inne serwery i wymagają systemów zasilaczy awaryjnych (UPS) do obsługi tego typu awarii.

## <a name="myth-mainframes-have-limitless-scalability"></a>Omówienia: Komputery mainframe mają nieograniczony skalowalność

Skalowalność komputera mainframe zależy od pojemności oprogramowania systemu, takiego jak system kontroli informacji o klientach (CICS) i pojemności nowych wystąpień aparatów i magazynów mainframe. Niektóre duże firmy, które wykorzystują Komputery mainframe, dostosowały swoje CICS do wydajności i w inny sposób nie rozwinęły możliwości największych dostępnych komputerów mainframe.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Omówienia: serwery z technologią Intel nie są tak zaawansowane jak Komputery mainframe

Nowe komputery z systemami opartymi na architekturze Intel muszą mieć tyle pojemności obliczeniowych jak Komputery mainframe.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Omówienia: chmura nie może obsłużyć aplikacji o znaczeniu strategicznym dla dużych firm, takich jak instytucje finansowe

Mogą istnieć pewne izolowane wystąpienia, w których rozwiązania w chmurze są bardzo krótkie, zwykle ponieważ nie można dystrybuować algorytmów aplikacji. Te kilka przykładów są wyjątkami, a nie z regułą.

## <a name="summary"></a>Podsumowanie

Z tego względu platforma Azure oferuje alternatywną platformę, która jest w stanie dostarczać równoważne funkcje i funkcje komputera mainframe oraz znacznie niższy koszt. Ponadto łączny koszt posiadania (TCO) w chmurze oparty na subskrypcjach jest znacznie tańszy niż Komputery mainframe.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Przełączenie z komputerów mainframe na platformę Azure](./migration-strategies.md)
