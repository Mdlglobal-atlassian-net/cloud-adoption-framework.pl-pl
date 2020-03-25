---
title: Przewodnik po decyzjach dotyczących sieci zdefiniowanej programowo
description: Skorzystaj z przewodnika Cloud Adoption Framework, aby dowiedzieć się, w jaki sposób sieć zdefiniowana programowo zapewnia centralnie zarządzaną sieć wirtualną za pomocą oprogramowania.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: a07130e8d7ac201f7519658ea84e3ff9df33ecbb
ms.sourcegitcommit: 25cd1b3f218d0644f911737a6d5fd259461b2458
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/24/2020
ms.locfileid: "80225738"
---
# <a name="software-defined-networking-decision-guide"></a>Przewodnik po decyzjach dotyczących sieci zdefiniowanej programowo

Sieć zdefiniowana programowo (SDN, Software Defined Networking) to architektura sieci zaprojektowana z myślą o udostępnianiu wirtualnych funkcji związanych z pracą w sieci, które mogą być centralnie zarządzane, konfigurowane i modyfikowane za pośrednictwem oprogramowania. Sieć SDN umożliwia tworzenie sieci opartych na chmurze za pomocą zwirtualizowanych odpowiedników fizycznych routerów, zapór i innych urządzeń sieciowych używanych w sieciach lokalnych. Sieć SDN ma krytyczne znaczenie w procesie tworzenia bezpiecznych sieci wirtualnych na platformach chmury publicznej, takich jak Azure.

## <a name="networking-decision-guide"></a>Przewodnik po decyzjach związanych z siecią

![Wykres opcji sieci od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-software-defined-network.png)

Idź do: [Tylko usługa PaaS](./paas-only.md) | [Natywne dla chmury](./cloud-native.md) | [Strefa DMZ w chmurze](./cloud-dmz.md) [Hybrydowe](./hybrid.md) | [Model piasty i szprych](./hub-spoke.md) | [Dowiedz się więcej](#learn-more)

Sieć SDN oferuje kilka opcji z różnymi poziomami cen i złożoności. Powyższy przewodnik odnajdywania zawiera informacje referencyjne na temat szybkiego personalizowania tych opcji w celu najlepszego dopasowania ich do określonych strategii biznesowych i technologicznych.

Punkt szczytowy w tym przewodniku zależy od kilku kluczowych decyzji, które zespół ds. strategii chmury podjął, zanim zaczął podejmować decyzje dotyczące architektury sieci. Najważniejsze wśród nich to decyzje dotyczące [cyfrowej definicji infrastruktury](../../digital-estate/index.md) i [projektu subskrypcji](../subscriptions/index.md) (które mogą również wymagać danych wejściowych decyzji związanych z księgowością w chmurze i globalnej strategii rynkowej).

Prawdopodobieństwo, że ten punkt szczytowy znacząco wpłynie na małe wdrożenia w pojedynczym regionie z liczbą maszyn wirtualnych mniejszą niż 1000, jest niskie. Z drugiej strony decyzje dotyczące sieci SDN i ten kluczowy punkt szczytowy mogą mieć znaczący wpływ na duże operacje wdrażania z liczbą maszyn wirtualnych większą niż 1000, wieloma jednostkami biznesowymi lub wieloma rynkami geopolitycznymi.

## <a name="choose-the-right-virtual-networking-architectures"></a>Wybieranie właściwych architektur sieci wirtualnych

Ta sekcja rozszerza przewodnik po decyzjach, aby ułatwić wybór właściwych architektur sieci wirtualnych.

Istnieje wiele sposobów implementowania technologii SDN w celu tworzenia sieci wirtualnych opartych na chmurze. To, jak zdefiniujesz strukturę sieci wirtualnych używanych w migracji i jak te sieci będą wchodzić w interakcje z istniejącą infrastrukturą IT, będzie zależeć od kombinacji wymagań dotyczących obciążeń i ładu.

Podczas planowania, którą architekturę sieci wirtualnej lub kombinację architektur weźmiesz pod uwagę w procesie planowania migracji do chmury, należy odpowiedzieć na następujące pytania, aby ułatwić zidentyfikowanie właściwych rozwiązań dla organizacji:

| Pytanie | Tylko usługa PaaS | Natywne dla chmury | Strefa DMZ w chmurze | Połączenie hybrydowe | Gwiazda |
|-----|-----|-----|-----|-----|-----|
| Czy obciążenie będzie używać tylko usług PaaS i nie będzie wymagać możliwości sieciowych innych niż możliwości oferowane przez same usługi? | Yes | Nie | Nie | Nie | Nie |
| Czy obciążenie wymaga integracji z aplikacjami lokalnymi? | Nie | Nie | Yes | Yes | Yes |
| Czy ustanowiono dojrzałe zasady zabezpieczeń i bezpieczną łączność między sieciami lokalnymi i w chmurze? | Nie | Nie | Nie | Yes | Yes |
| Czy obciążenie wymaga usług uwierzytelniania nieobsługiwanych przez usługi tożsamości w chmurze, czy też musisz mieć bezpośredni dostęp do kontrolerów domeny w środowisku lokalnym? | Nie | Nie | Nie | Yes | Yes |
| Czy trzeba będzie wdrożyć dużą liczbę maszyn wirtualnych i obciążeń oraz zarządzać nimi? | Nie | Nie | Nie | Nie | Yes |
| Czy będzie trzeba udostępniać scentralizowane zarządzanie i łączność lokalną w przypadku delegowania kontroli nad zasobami do poszczególnych zespołów zajmujących się obciążeniami? | Nie | Nie | Nie | Nie | Yes |

## <a name="virtual-networking-architectures"></a>Architektury sieci wirtualnych

Dowiedz się więcej na temat podstawowych architektur sieci zdefiniowanych programowo:

- **[Tylko usługa PaaS](./paas-only.md):** większość produktów typu „platforma jako usługa” (PaaS) obsługuje ograniczony zestaw wbudowanych funkcji sieciowych i nie musi wymagać sieci jawnie zdefiniowanej programowo do obsługi wymagań dotyczących obciążenia.
- **[Natywne dla chmury](./cloud-native.md):** architektura natywna dla chmury obsługuje oparte na chmurze obciążenia przy użyciu sieci wirtualnych zbudowanych za pomocą domyślnych możliwości sieci zdefiniowanej programowo opartych na platformie w chmurze bez konieczności polegania na zasobach lokalnych lub innych zasobach zewnętrznych.
- **[Strefa DMZ w chmurze](./cloud-dmz.md):** obsługuje ograniczoną łączność między sieciami lokalnymi i w chmurze zabezpieczoną za pomocą implementacji strefy zdemilitaryzowanej, która ściśle kontroluje ruch między dwoma środowiskami.
- **[Hybrydowe](./hybrid.md):** hybrydowa architektura sieci w chmurze umożliwia sieciom wirtualnym w środowiskach chmur zaufanych uzyskiwanie dostępu do zasobów w środowisku lokalnym i na odwrót.
- **[Gwiazda](./hub-spoke.md):** architektura gwiazdy umożliwia centralne zarządzanie połączeniami zewnętrznymi i usługami udostępnionymi, wyodrębnianie poszczególnych obciążeń i rozwiązywanie potencjalnych problemów z limitami subskrypcji.

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat sieci zdefiniowanej programowo na platformie Azure, zobacz:

- [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Na platformie Azure podstawowe możliwości sieci SDN są oferowane przez usługę Azure Virtual Network, która działa jako analogia chmury do fizycznych sieci lokalnych. Sieci wirtualne działają jako domyślna granicy izolacji między zasobami na platformie.
- [Najlepsze rozwiązania z zakresu zabezpieczeń sieci na platformie Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) Zalecenia zespołu ds. zabezpieczeń platformy Azure dotyczące sposobu konfigurowania sieci wirtualnych w celu zminimalizowania luk w zabezpieczeniach.

## <a name="next-steps"></a>Następne kroki

Sieć zdefiniowana programowo to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
