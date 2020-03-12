---
title: Topologia sieci piasty i szprych
description: Więcej informacji na temat topologii sieci Hub i szprych w celu skuteczniejszego zarządzania typowymi wymaganiami dotyczącymi komunikacji lub zabezpieczeń.
author: tracsman
ms.author: jonor
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: rossort
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: a2827273aa3fd28478c2615610f74f32b155a299
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092599"
---
<!-- cSpell:ignore tracsman jonor rossort NVAs -->

# <a name="hub-and-spoke-network-topology"></a>Topologia sieci piasty i szprych

*Piasta i szprychy* to model sieci umożliwiający bardziej efektywne zarządzanie typowymi wymaganiami dotyczącymi komunikacji i zabezpieczeń. Pomaga również uniknąć ograniczeń subskrypcji platformy Azure. Ten model dotyczy następujących kwestii:

- **Oszczędność kosztów i efektywność zarządzania**. Scentralizowanie w jednej lokalizacji usług, które mogą być współużytkowane przez wiele obciążeń, takich jak wirtualne urządzenia sieciowe (NVA) i serwery DNS, umożliwia działowi IT zminimalizowanie nadmiarowych zasobów i zadań związanych z zarządzaniem.
- **Pokonywanie ograniczeń subskrypcji**. Duże obciążenia oparte na chmurze mogą wymagać użycia większej ilości zasobów, niż jest to dozwolone w pojedynczej subskrypcji platformy Azure. Komunikacja równorzędna sieci wirtualnych obciążenia z różnych subskrypcji do centrum może pokonać te ograniczenia. Aby uzyskać więcej informacji, zobacz [limity subskrypcji](https://docs.microsoft.com/azure/azure-subscription-service-limits).
- **Separacja problemów**. Poszczególne obciążenia można wdrożyć między centralnymi zespołami IT i zespołami obciążeń.

Dodatkowa struktura i możliwości oferowane przez ten model mogą nie przynieść korzyści mniejszym majątkom w chmurze. Jednak większe działania związane z wdrażaniem w chmurze powinny uwzględniać implementację architektury sieci typu Hub i szprychy, jeśli mają one jakiekolwiek problemy wymienione wcześniej.

> [!NOTE]
> Lokacja architektury referencyjnej platformy Azure zawiera przykładowe szablony, których można użyć jako podstawy do implementowania własnych sieci Hub i szprych:
>
> - [Implementowanie topologii sieci gwiazdy i gwiazdy na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
> - [Implementowanie topologii sieci gwiazdy i gwiazdy przy użyciu usług udostępnionych na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)

## <a name="overview"></a>Omówienie

![Przykłady topologii sieci gwiazdy i gwiazdy][1]

Jak pokazano na diagramie, platforma Azure obsługuje dwa typy centrów i satelitów. Obsługuje ona komunikację, zasoby udostępnione i scentralizowane zasady zabezpieczeń („centrum sieci wirtualnej” na diagramie) lub typ wirtualnej sieci WAN („wirtualna sieć WAN” na diagramie) na potrzeby wielkoskalowej komunikacji między oddziałami lub między oddziałem i platformą Azure.

Piasta to centralna strefa sieciowa, która kontroluje i sprawdza ruch przychodzący i wychodzący między strefami: Internet, środowisko lokalne i szprychy. Topologia gwiazdy umożliwia działowi IT efektywną metodę wymuszania zasad zabezpieczeń w centralnej lokalizacji. Minimalizuje również ryzyko błędnej konfiguracji i ekspozycji.

Piasta zawiera często wspólne składniki usługi używane przez szprychy. Poniżej przedstawiono typowe usługi centralne:

- Infrastruktura usługi Active Directory systemu Windows Server, wymagana do uwierzytelniania użytkowników innych firm, którzy uzyskują dostęp z niezaufanych sieci przed uzyskaniem dostępu do obciążeń w szprysze. Obejmuje ona powiązane usługi Active Directory Federation Services (AD FS).
- Usługa DNS do rozpoznawania nazw obciążeń w szprychach, do uzyskiwania dostępu do zasobów lokalnych i w Internecie, jeśli usługa [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) nie jest używana.
- Infrastruktura kluczy publicznych (PKI) do implementowania obciążeń logowania jednokrotnego.
- Kontrola przepływu ruchu TCP i UDP między strefami sieciowymi szprych i Internetem.
- Sterowanie przepływem między szprychami i środowiskiem lokalnym.
- W razie konieczności sterowanie przepływem między jedną szprychą a inną.

Używając infrastruktury piasty udostępnionej w celu obsługi wielu szprych, można zminimalizować nadmiarowość, uprościć zarządzanie i obniżyć koszt całkowity.

Rolą każdej szprychy może być hostowanie różnych typów obciążeń. Szprychy zapewniają również modularne podejście do powtarzających się wdrożeń tych samych obciążeń. Przykłady to programowanie i testowanie, testowanie akceptacji przez użytkowników, przygotowanie i produkcja.

Szprychy mogą również dzielić różne grupy w obrębie organizacji i umożliwiać ich tworzenie. Przykładem są grupy usługi Azure DevOps. Wewnątrz szprychy można wdrażać podstawowe obciążenia lub złożone obciążenia wielowarstwowe z kontrolą ruchu między warstwami.

## <a name="subscription-limits-and-multiple-hubs"></a>Ograniczenia subskrypcji i wiele piast

Na platformie Azure każdy składnik, niezależnie od typu, jest wdrażany w ramach subskrypcji platformy Azure. Izolacja składników platformy Azure w różnych subskrypcjach platformy Azure może spełniać różne wymagania biznesowe, takie jak konfigurowanie różnych poziomów dostępu i autoryzacji.

Pojedyncze implementacje Hub i szprychy mogą być skalowane do dużej liczby szprych. Jednak podobnie jak w przypadku każdego systemu informatycznego, istnieją ograniczenia platformy. Wdrożenie piasty jest powiązane z określoną subskrypcją platformy Azure, która ma ograniczenia i limity. Przykładem jest maksymalna liczba komunikacji równorzędnych sieci wirtualnych. Aby uzyskać więcej informacji, zobacz [Limity, przydziały i ograniczenia usług i subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

W przypadkach, gdy ograniczenia mogą stanowić problem, można skalować w górę architekturę, rozszerzając model z jednej piasty i szprych do klastra piast i szprych. Możesz połączyć wiele piast w jednym lub większej liczbie regionów świadczenia usługi Azure za pomocą komunikacji równorzędnej sieci wirtualnych, usługi Azure ExpressRoute, wirtualnej sieci WAN lub sieci VPN typu lokacja-lokacja.

![Klaster piast i szprych][2]

Wprowadzenie wielu piast zwiększa koszt i nakłady pracy związane z zarządzaniem w systemie. Jest to usprawiedliwione tylko skalowalnością, ograniczeniami systemu lub nadmiarowością i replikacją regionalną na potrzeby wydajności użytkownika lub odzyskiwania po awarii. W scenariuszach wymagających wielu piast wszystkie piasty powinny dążyć do oferowania tego samego zestawu usług w celu ułatwienia zadań operacyjnych.

## <a name="interconnection-between-spokes"></a>Wzajemne połączenia między szprychami

Istnieje możliwość zaimplementowania złożonych, wielowarstwowych obciążeń w obrębie jednej szprychy. Konfiguracje wielowarstwowe można implementować przy użyciu podsieci (jedna dla każdej warstwy) w tej samej sieci wirtualnej i przy użyciu sieciowych grup zabezpieczeń do filtrowania przepływów.

Architekt może chcieć wdrożyć obciążenie wielowarstwowe w wielu sieciach wirtualnych. Za pomocą komunikacji równorzędnej sieci wirtualnych szprychy mogą łączyć się z innymi szprychami w tej samej piaście lub w różnych piastach.

Typowym przykładem tego scenariusza jest przypadek, w którym serwery przetwarzania aplikacji znajdują się w jednej szprysze lub sieci wirtualnej. Baza danych jest wdrażana w innej szprysze lub sieci wirtualnej. W takim przypadku można łatwo połączyć szprychy za pomocą komunikacji równorzędnej sieci wirtualnych, aby uniknąć przesyłania danych przez piastę. Rozwiązaniem jest przeprowadzenie starannej architektury i przeglądu zabezpieczeń, aby upewnić się, że pominięcie centrum nie pomija ważnych punktów zabezpieczeń lub inspekcji, które mogą istnieć tylko w centrum.

![Szprychy połączone ze sobą i z piastą][3]

Szprychy mogą być również połączone ze szprychą, która pełni rolę piasty. Takie podejście tworzy hierarchię dwupoziomową: szprycha na wyższym poziomie (poziom 0) staje się piastą dla małych szprych (poziom 1) w hierarchii. Szprychy wdrożenia gwiazdy i gwiazdy są wymagane do przekazywania ruchu do centralnego koncentratora, dzięki czemu ruch może być przesyłany do miejsca docelowego w sieci lokalnej lub w publicznym Internecie. Architektura z dwoma poziomami koncentratorów wprowadza skomplikowany Routing, który usuwa zalety prostej relacji gwiazdy i satelity.

<!-- images -->

[1]: ../../_images/azure-best-practices/network-hub-spoke-high-level.png "Ogólny przykład piasty i szprych"
[2]: ../../_images/azure-best-practices/network-hub-spokes-cluster.png "Klaster piast i szprych"
[3]: ../../_images/azure-best-practices/network-spoke-to-spoke.png "Szprycha do szprychy"
