---
title: Uzyskiwanie zgodności w chmurze hybrydowej
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak definiować podejście do tworzenia spójności chmury hybrydowej.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7b2433b787683cf8ecaaf4a1f7a858aa18bf682c
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79093040"
---
# <a name="create-hybrid-cloud-consistency"></a>Uzyskiwanie zgodności w chmurze hybrydowej

W tym artykule opisano metody wysokiego poziomu dotyczące tworzenia spójności chmury hybrydowej.

Hybrydowe modele wdrażania podczas migracji mogą zmniejszyć ryzyko i przyczynić się do płynnego przejścia do infrastruktury. Platformy w chmurze oferują największy poziom elastyczności, gdy chodzi o procesy biznesowe. Wiele organizacji wątpliwości się w celu przejścia do chmury. Zamiast tego wolą zachować pełną kontrolę nad ich najbardziej poufnymi danymi. Niestety serwery lokalne nie pozwalają na takie same innowacje jak w przypadku chmury. Rozwiązanie hybrydowe w chmurze oferuje szybkość innowacji w chmurze oraz kontrolę nad zarządzaniem lokalnymi.

## <a name="integrate-hybrid-cloud-consistency"></a>Integrowanie spójności chmury hybrydowej

Rozwiązanie w chmurze hybrydowej umożliwia organizacjom skalowanie zasobów obliczeniowych. Eliminuje to również potrzebę wykonywania dużych nakładów inwestycyjnych do obsługi krótkoterminowych przekroczeń popytu. Zmiany w firmie mogą zwiększyć konieczność zwolnienia zasobów lokalnych w celu uzyskania bardziej poufnych danych lub aplikacji. Anulowanie aprowizacji zasobów w chmurze jest łatwiejsze, szybsze i tańsze. Płacisz tylko za zasoby, których Twoja organizacja tymczasowo używa, zamiast konieczności kupowania i konserwowania dodatkowych zasobów. Takie podejście zmniejsza ilość sprzętu, który może pozostawać bezczynny w długim okresie czasu. Przetwarzanie w chmurze hybrydowej zapewnia wszystkie korzyści wynikające z elastyczności i skalowalności w chmurze, co pozwala na najniższe ryzyko narażenia na dane.

![tworzenia hybrydowej spójności w chmurze w ramach tożsamości, zarządzania, zabezpieczeń, danych, programowania i DevOps](../../_images/hybrid-consistency.png)
*rysunek 1 — Tworzenie hybrydowej spójności w chmurze między tożsamościami, zarządzaniem, zabezpieczeniami, danymi, programowaniem i DevOps.*

Prawdziwe rozwiązanie w chmurze hybrydowej musi udostępniać cztery składniki, z których każdy ma znaczące korzyści:

- **Wspólna tożsamość dla aplikacji lokalnych i w chmurze:** Ten składnik zwiększa produktywność użytkowników, umożliwiając użytkownikom logowanie jednokrotne do wszystkich aplikacji. Zapewnia także spójność aplikacji i użytkowników między granicami sieci lub chmury.
- **Zintegrowane zarządzanie i zabezpieczenia w chmurze hybrydowej:** Ten składnik zapewnia spójny sposób monitorowania i zabezpieczania środowiska oraz zarządzania nim, co zapewnia lepszy wgląd i kontrolę.
- **Spójna platforma danych na potrzeby centrum i chmury:** Ten składnik tworzy przenośność danych, w połączeniu z bezproblemowym dostępem do usług lokalnych i danych w chmurze w celu uzyskania szczegółowego wglądu w wszystkie źródła danych.
- **Ujednolicone programowanie i DevOps w chmurze i lokalnych centrach danych:** Ten składnik umożliwia przenoszenie aplikacji między tymi dwoma środowiskami zgodnie z wymaganiami. Produktywność dla deweloperów zwiększa się, ponieważ obie lokalizacje mają teraz to samo środowisko programistyczne.

Poniżej przedstawiono kilka przykładów tych składników z perspektywy platformy Azure:

- Azure Active Directory (Azure AD) współpracuje z lokalnym Active Directory, aby zapewnić wspólną tożsamość dla wszystkich użytkowników. Logowanie jednokrotne w środowisku lokalnym i za pośrednictwem chmury ułatwia użytkownikom bezpieczne uzyskiwanie dostępu do potrzebnych aplikacji i zasobów. Administratorzy mogą zarządzać kontrolami bezpieczeństwa i zarządzania, a także mieć elastyczność dostosowywania uprawnień bez wpływu na środowisko użytkownika.
- Platforma Azure oferuje zintegrowane usługi zarządzania i zabezpieczeń dla infrastruktury chmurowej i lokalnej. Te usługi obejmują zintegrowany zestaw narzędzi służących do monitorowania, konfigurowania i ochrony chmur hybrydowych. To kompleksowe podejście do zarządzania przeznaczone wyłącznie dla rzeczywistych wyzwań, które są związane z organizacjami uwzględniającymi rozwiązanie w chmurze hybrydowej.
- Chmura hybrydowa platformy Azure udostępnia typowe narzędzia, które zapewniają bezproblemowy i wydajny bezpieczny dostęp do wszystkich danych. Usługi Azure Data Services łączą się z Microsoft SQL Server, aby utworzyć spójną platformę danych. Spójny model chmury hybrydowej umożliwia użytkownikom współdziałanie z danymi operacyjnymi i analitycznymi. Te same usługi są udostępniane lokalnie i w chmurze na potrzeby magazynowania danych, analizy danych i wizualizacji danych.
- Usługi Azure Cloud Services połączone z Azure Stack lokalnie zapewniają ujednolicone programowanie i DevOps. Spójność w chmurze i lokalnie oznacza, że zespół DevOps może tworzyć aplikacje działające w dowolnym środowisku i można je łatwo wdrożyć w odpowiedniej lokalizacji. Możesz również ponownie używać szablonów w ramach rozwiązania hybrydowego, które upraszczają procesy DevOps.

## <a name="azure-stack-in-a-hybrid-cloud-environment"></a>Azure Stack w środowisku chmury hybrydowej

Azure Stack to hybrydowe rozwiązanie w chmurze, które umożliwia organizacjom uruchamianie usług spójnych na platformie Azure w swoich centrach danych. Zapewnia ona uproszczone środowisko programistyczne, zarządzania i zabezpieczeń, które są spójne z usługami w chmurze publicznej platformy Azure. Azure Stack to rozszerzenie platformy Azure. Możesz użyć jej do uruchamiania usług platformy Azure z lokalnych środowisk, a następnie przejść do chmury platformy Azure, jeśli i w razie potrzeby.

Za pomocą Azure Stack można wdrażać i obsługiwać zarówno IaaS, jak i PaaS, korzystając z tych samych narzędzi i oferując takie samo środowisko jak w przypadku chmury publicznej platformy Azure. Zarządzanie Azure Stack, bez względu na to, czy za pomocą portalu interfejsu użytkownika sieci Web, czy za pomocą programu PowerShell, ma spójny wygląd i działanie dla administratorów IT i użytkowników końcowych na platformie Azure.

Platforma Azure i Azure Stack otwieranie nowych hybrydowych przypadków użycia zarówno dla aplikacji biznesowych, jak i wewnętrznych.

- **Rozwiązania brzegowe i rozłączone.** Aby rozwiązać wymagania dotyczące opóźnień i połączeń, klienci mogą przetwarzać dane lokalnie w Azure Stack a następnie agregować je na platformie Azure w celu dalszej analizy. Mogą używać typowej logiki aplikacji w obu. Wielu klientów interesuje ten scenariusz tej krawędzi w różnych kontekstach, takich jak piętra fabryki, statki wycieczkowe i napędy z kopalni.
- **Aplikacje w chmurze, które spełniają różne regulacje.** Klienci mogą opracowywać i wdrażać aplikacje na platformie Azure, zapewniając pełną elastyczność wdrażania lokalnego na Azure Stack w celu spełnienia wymagań prawnych lub zasad. Nie są wymagana żadne zmiany w kodzie. Przykłady aplikacji obejmują globalne inspekcje, raportowanie finansowe, handel wymianą walut, gry online i raportowanie wydatków. Klienci czasami zapoznają się z wdrażaniem różnych wystąpień tej samej aplikacji na platformie Azure lub Azure Stack, w oparciu o wymagania biznesowe i techniczne. Mimo że platforma Azure spełnia większość wymagań, Azure Stack uzupełnia podejście wdrożenia w razie potrzeby.
- **Model aplikacji w chmurze w środowisku lokalnym.** Klienci mogą używać usług sieci Web, kontenerów, bezserwerowych i mikrousług platformy Azure, aby aktualizować i poszerzać istniejące aplikacje lub tworzyć nowe. Można używać spójnych procesów DevOps na platformie Azure w chmurze i Azure Stack lokalnych. Istnieje coraz więcej zainteresowania modernizacji aplikacji, nawet w przypadku podstawowych aplikacji o znaczeniu strategicznym.

Azure Stack jest oferowana za pośrednictwem dwóch opcji wdrażania:

- **Azure Stack zintegrowane systemy:** Azure Stack zintegrowane systemy są oferowane przez firmę Microsoft i partnerów sprzętowych, aby utworzyć rozwiązanie, które zapewnia kompleksowe innowacje w chmurze z prostym zarządzaniem. Ponieważ Azure Stack jest oferowana jako zintegrowany system sprzętu i oprogramowania, uzyskuje się elastyczność i kontrolę przy jednoczesnym wdrażaniu innowacji z chmury. Azure Stack zakres zintegrowanych systemów w rozmiarze od 4 do 12 węzłów. Są one wspólnie obsługiwane przez partnera sprzętu i firmę Microsoft. Użyj Azure Stack zintegrowanych systemów, aby włączyć nowe scenariusze dla obciążeń produkcyjnych.
- **Azure Stack Development Kit:** Microsoft Azure Stack Development Kit to wdrożenie z jednym węzłem Azure Stack. Można jej użyć do szacowania i uczenia się Azure Stack. Zestawu można także użyć jako środowiska deweloperskiego, w którym można opracowywać przy użyciu interfejsów API i narzędzi, które są spójne z platformą Azure. Azure Stack Development Kit nie jest przeznaczona do użycia w środowisku produkcyjnym.

## <a name="azure-stack-one-cloud-ecosystem"></a>Azure Stack ekosystem w chmurze

Aby przyspieszyć Azure Stack inicjatywy, możesz skorzystać z pełnego ekosystemu platformy Azure:

- Platforma Azure zapewnia, że większość aplikacji i usług certyfikowanych na platformie Azure będzie działała Azure Stack. Kilka niezależnych dostawców oprogramowania rozszerza swoje rozwiązania na Azure Stack. Ci dostawcy oprogramowania to: Bitnami, Docker, Kemp Technologies, Pivoting Cloud Foundry, Red Hat Enterprise Linux i SUSE Linux.
- Można wybrać Azure Stack dostarczana i obsługiwana jako w pełni zarządzana usługa. Wielu partnerów będzie mieć już dostępne oferty usług zarządzanych na platformie Azure i Azure Stack. Ci partnerzy obejmują Tieto, Yourhosting, Revera, napęd i NTT. Ci partnerzy dostarczają usługi zarządzane dla systemu Azure za pośrednictwem programu Cloud Solution Provider (CSP). Rozszerzają one oferty w celu uwzględnienia rozwiązań hybrydowych.
- Na przykład kompletne, w pełni zarządzane rozwiązanie w chmurze hybrydowej, firma Avanade oferuje ofertę wszystko-część. Obejmuje to usługi transformacji w chmurze, oprogramowanie, infrastrukturę, instalację i konfigurację oraz bieżące usługi zarządzane. Dzięki temu klienci mogą korzystać z Azure Stack tak samo jak na platformie Azure.
- Dostawcy mogą pomóc przyspieszyć modernizację aplikacji, tworząc kompleksowe rozwiązania platformy Azure dla klientów. Wprowadzają one głębokie zestawy umiejętności platformy Azure, informacje o domenie i branży oraz specjalistyczne informacje, takie jak DevOps. Każda Azure Stack w chmurze to szansa dla dostawcy, aby zaprojektować rozwiązanie i prowadzić do wdrożenia systemu. Mogą również dostosowywać dołączone funkcje i dostarczać działania operacyjne. Przykłady dostawców obejmują firma Avanade, DXC, usługi firmy Dell EMC, nieczołową grupę konsultingową, HPE Pointnext i PwC (dawniej PricewaterhouseCoopers).
