---
title: Wirtualne centrum danych Azure
description: Zasoby dla usługi wirtualnego centrum danych Microsoft Azure
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
keywords: Azure
layout: LandingPage
ms.openlocfilehash: 39cb6ac3c31873431206d8c6c525c9ce3467653f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030006"
---
# <a name="azure-virtual-datacenter-and-the-enterprise-control-plane"></a>Wirtualne centrum danych Azure oraz rozwiązanie Enterprise Control Plane

Wirtualne centrum danych Azure to podejście oparte na maksymalnym wykorzystaniu możliwości platformy Azure w chmurze przy jednoczesnym respektowaniu istniejących zasad dotyczących zabezpieczeń i sieci. W przypadku wdrażania obciążeń korporacyjnych w chmurze organizacje IT i jednostki biznesowe muszą równoważyć zarządzanie z elastycznością deweloperów. Wirtualne centrum danych Azure udostępnia modele umożliwiające osiągnięcie tej równowagi z większym naciskiem na zarządzanie.

## <a name="resources"></a>Zasoby

<!-- markdownlint-disable MD033 -->

<table>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Concepts"><img src="../_images/vdc/virtual-datacenter.svg" alt="Virtual Datacenter e-book" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Concepts">Wirtualne centrum danych Azure: Pojęcia</a></h3>
        <p>W książce elektronicznej pokazano, jak wdrożyć obciążenia przedsiębiorstwa na platformie chmury Azure z zachowaniem istniejących zabezpieczeń i zasad sieci.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="./networking-vdc.md"><img src="../_images/vdc/vdc-network.png" alt="Network Perspective" /></a></td>
    <td>
        <h3><a href="./networking-vdc.md">Wirtualne centrum danych Azure: Perspektywa sieci</a></h3>
        <p>W tym artykule online zamieszczono omówienie wzorców sieciowych i projektów, których można użyć do rozwiązywania problemów ze skalą architektury, wydajności i zabezpieczeniami. Problemy te stanowią wyzwanie dla wielu klientów, którzy rozważają przechodzenie do chmury na dużą skalę.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Lift"><img src="../_images/vdc/vdc-lift-and-shift.png" alt="Lift and Shift Guide" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Lift">Wirtualne centrum danych Azure: Przewodnik migrowania metodą „lift-and-shift”</a></h3>
        <p>W tym dokumencie przedstawiono proces, którego mogą używać pracownicy działu IT w przedsiębiorstwie lub osoby podejmujące decyzje, aby zidentyfikować i zaplanować migrację aplikacji i serwerów do platformy Azure przy użyciu metody „lift and shift”, minimalizując wszelkie dodatkowe koszty deweloperskie przy jednoczesnej optymalizacji opcji hostingu w chmurze.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Deck"><img src="../_images/vdc/vdc-deck.png" alt="Presentation Deck" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Deck">Wirtualne centrum danych Azure: Prezentacja</a></h3>
        <p>W tej prezentacji przedstawiono wskazówki i narzędzia związane z wirtualnym centrum danych Azure. Omówiono w niej cele wirtualnego centrum danych, sterowniki klientów, regiony platformy Azure, elementy automatyzacji wirtualnego centrum danych, przemysłowe i zaufane wirtualne centra danych Azure, a kończy się ona planem działania związanym ze wskazówkami CIO. Dostępne są również informacje dotyczące pomocy technicznej i szkoleń.</p>
    </td>
</tr>
</table>

<!-- markdownlint-enable MD033 -->

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-azure-virtual-datacenter"></a>Co to jest wirtualne centrum danych Azure?

Wdrażanie obciążeń do chmury niesie ze sobą potrzebę rozwijania i utrzymywania zaufania do chmury na takim samym poziomie, jak zaufanie do istniejących centrów danych. Pierwszy model wytycznych wirtualnego centrum danych Azure został opracowany w celu zaspokojenia tej potrzeby przez zablokowane podejście do infrastruktury wirtualnej. Ta metoda nie jest odpowiednia dla wszystkich użytkowników. Została zaprojektowana z myślą o wspieraniu korporacyjnych grup IT w ramach rozwijania infrastruktury lokalnej do chmury publicznej Azure. Nazywamy to podejście modelem zaufanego rozszerzenia centrum danych. Wraz z upływem czasu będą oferowane inne modele, w tym modele umożliwiające bezpieczny dostęp do Internetu bezpośrednio z wirtualnego centrum danych.

<!-- markdownlint-disable MD033 -->

<img src="../_images/vdc/vdc-components.svg" alt="Virtual Datacenter components" style="max-width:700px;"/>

<!-- markdownlint-enable MD033 -->

Te cztery składniki umożliwiają istnienie wirtualnego centrum danych Azure: tożsamość, szyfrowanie, sieć zdefiniowana przez oprogramowanie oraz zgodność (w tym dzienniki i raportowanie).

W modelu wirtualnego centrum danych Azure możesz zastosować zasady izolacji, przekształcić chmurę w centrum bardziej przypominające znane fizyczne centra danych, a także zapewnić wymagane poziomy zabezpieczeń i zaufania. Umożliwiają to cztery składniki rozpoznawalne przez dowolny korporacyjny zespół IT: sieć zdefiniowana przez oprogramowanie, szyfrowanie, zarządzanie tożsamościami oraz podstawowe standardy i certyfikaty dotyczące zgodności platformy Azure. Te cztery składniki są kluczem do przekształcenia wirtualnego centrum danych w zaufane rozszerzenie istniejących inwestycji w infrastrukturę.

Czytaj dalej książkę elektroniczną [Pojęcia dotyczące wirtualnego centrum danych Azure](https://azure.microsoft.com/resources/azure-virtual-datacenter).
