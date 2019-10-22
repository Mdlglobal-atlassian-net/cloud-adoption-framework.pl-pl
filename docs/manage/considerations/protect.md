---
title: Ochrona i odzyskiwanie — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ochrona i odzyskiwanie — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 2e055cb6105b9424259d2b8e86bdde7d64798479
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682452"
---
# <a name="protect-and-recover-in-cloud-management"></a>Ochrona i odzyskiwanie w programie Cloud Management

Po spełnieniu wymagań dotyczących [spisu i widoczności](./inventory.md) oraz [zgodności operacyjnej](./operational-compliance.md) zespoły zarządzania chmurą mogą przeszukiwać i przygotowywać potencjalne awarie obciążenia. Planując zarządzanie chmurą, zespół musi zacząć z założeniem, że coś się nie powiedzie.

Żadne rozwiązanie techniczne nie może stale oferować umowy SLA na 100% czasu. Rozwiązania z nadmiarowymi zastosowaniami architektury do dostarczania na "sześć 9" lub na 99,9999% czasu. Mimo że rozwiązanie "sześć 9" jest wyłączone przez 31,6 sekund w danym roku. Niestety, rzadko rozwiązania uzasadniają duże, trwające inwestycje operacyjne wymagane do osiągnięcia "sześciu 9" czasu pracy.

Przygotowanie do przestojów pozwoli zespołowi wykrywać błędy szybciej i szybciej odzyskiwać. Ta dyscyplina jest skoncentrowana na następnych krokach, które są dostępne po awarii systemu. Jak chronić obciążenia, aby można je było szybko odzyskać w przypadku wystąpienia awarii.

## <a name="translating-protection-and-recovery-conversations"></a>Translacja konwersacji dotyczących ochrony i odzyskiwania

Obciążenia obejmujące aplikacje, dane, maszyny wirtualne i inne zasoby. Każdy z tych zasobów może wymagać innego podejścia do ochrony i odzyskiwania. Ważnym aspektem tego dyscypliny jest ustanowienie spójnego zobowiązania w ramach linii bazowej zarządzania w celu zapewnienia punktu wyjścia podczas dyskusji biznesowej.

Co najmniej każdy element zawartości obsługujący dowolne obciążenie powinna mieć podejście bazowe z wyraźnym zobowiązaniem do szybkiego odzyskania (cele czasu odzyskiwania lub RTO) i ryzyka utraty danych (cele punktu odzyskiwania lub cel celu).

### <a name="recovery-time-objectives-rto"></a>Cele czasu odzyskiwania (RTO)

Po awarii RTO to ilość czasu, jaką należy podjąć w celu odzyskania danego systemu do stanu sprzed awarii. Dla każdego obciążenia, które będzie obejmowały czas wymagany do przywrócenia minimalnej niezbędnej funkcjonalności dla maszyn wirtualnych i aplikacji. Obejmuje to również ilość czasu wymaganą do przywrócenia danych wymaganych przez aplikacje.

W obszarze warunki biznesowe RTO reprezentuje czas, przez jaki proces biznesowy nie będzie działać. W przypadku obciążeń o znaczeniu krytycznym ta zmienna powinna być stosunkowo niska, co pozwala procesom biznesowym szybko wznowić działanie. W przypadku obciążeń o niższym priorytecie standardowy poziom RTO może nie mieć zauważalnego wpływu na wydajność firmy.

Linia bazowa zarządzania powinna określać standardowy cel czasu odzyskiwania dla obciążeń o krytycznym znaczeniu. Firma może następnie użyć tej linii bazowej jako sposobu na wyjustowanie dodatkowych inwestycji w czasy odzyskiwania.

### <a name="recovery-point-objectives-rpo"></a>Cele punktu odzyskiwania (RPO)

W większości systemów zarządzania chmurą dane są okresowo przechwytywane i przechowywane przy użyciu pewnej formy ochrony danych. Czas ostatniego przechwycenia danych jest określany jako punkt odzyskiwania. Awaria systemu może zostać przywrócona tylko do najnowszego punktu odzyskiwania.

Jeśli system ma cel punktu odzyskiwania mierzony w godzinach lub dniach, awaria systemu spowodowałaby utratę danych dla tych godzin lub dni między ostatnim punktem odzyskiwania a awarią. Cel punktu odzyskiwania wynoszący 1 dzień będzie teoretycznie skutkować utratą wszystkich transakcji w dniu, co prowadzi do błędu.

W przypadku systemów o krytycznym znaczeniu, cel punktu odzyskiwania mierzony w minutach lub sekundach może być bardziej odpowiedni, aby uniknąć utraty przychodu. Jednak krótszy cel punktu odzyskiwania zazwyczaj skutkuje wzrostem całkowitych kosztów zarządzania.

Linia bazowa zarządzania powinna skupić się na najdłuższym akceptowalnym punkcie odzyskiwania w celu zminimalizowania kosztów. Zespół zarządzający chmurą może następnie zwiększyć cel punktu odzyskiwania dla określonych platform lub obciążeń, co wymagałoby większej ilości inwestycji.

## <a name="protect-and-recover-workloads"></a>Ochrona i odzyskiwanie obciążeń

Większość obciążeń w środowisku IT obsługuje bardzo mały proces biznesowy lub techniczny. Systemy, które nie mają wpływu na działalność biznesową, często nie uzasadniają zwiększonej ilości inwestycji wymaganych do odzyskania szybko lub Minimalizuj utratę danych. Ustanowienie linii bazowej pozwala firmie jasno zrozumieć, jaki poziom obsługi odzyskiwania może być oferowany w spójnym, zarządzanym punkcie cen. Dzięki temu zainteresowane strony biznesowe mogą oszacować wartość zwiększonej inwestycji w odzyskiwanie.

W przypadku większości zespołów zarządzania chmurą rozszerzona linia bazowa z określonymi zobowiązaniami RPO/RTO dla różnych zasobów zapewnia najbardziej preferowaną ścieżkę do wzajemnego zobowiązania biznesowego. W poniższych sekcjach przedstawiono kilka typowych rozszerzonych linii bazowych, które umożliwiają firmie łatwe dodawanie funkcji ochrony i odzyskiwania przez powtarzalny proces.

### <a name="protect-and-recover-data"></a>Ochrona i odzyskiwanie danych

Dane są raczej najbardziej cenne zasoby w gospodarce cyfrowej. Możliwość bardziej wydajnego ochrony i odzyskiwania danych jest najbardziej powszechną linią bazową. W przypadku danych, które mają wpływ na obciążenie produkcyjne, utrata danych może być bezpośrednio równa utracie przychodu lub straci zyskowność. Ogólnie zaleca się, aby zespoły zarządzania chmurą zapewniały poziom rozbudowanej linii bazowej zarządzania, który obsługuje popularne platformy danych.

Przed zaimplementowaniem operacji platformy często działy zarządzania chmurą mogą obsługiwać ulepszone operacje dla platformy jako platformy danych usługi. Na przykład łatwo jest, aby zespół zarządzający chmurą wymusił wyższą częstotliwość tworzenia kopii zapasowych lub wieloregionowej replikacji dla rozwiązań SQL Azure lub Cosmo DB. Dzięki temu zespół programistyczny może łatwo ulepszyć cel punktu odzyskiwania przez po prostu modernizację ich platform danych.

Ten proces myśli zostanie oglądany bardziej szczegółowo w [dyscypliny działania platformy](./platform.md).

### <a name="protect-and-recover-vms"></a>Ochrona i odzyskiwanie maszyn wirtualnych

Większość obciążeń ma pewną zależność od maszyn wirtualnych. Te maszyny wirtualne obsługują różne aspekty rozwiązania. Aby obciążenie obsługiwało proces biznesowy po awarii systemu, należy szybko odzyskać liczbę tych maszyn wirtualnych.

Każda minuta przestoju na tych maszynach wirtualnych może być równa utracie przychodu lub zmniejszyć zyskowność. Gdy przestój na maszynach wirtualnych ma bezpośredni wpływ na wydajność działania firmy, RTO jest bardzo ważne. Maszyny wirtualne można odzyskiwać szybciej przy użyciu replikacji do lokacji dodatkowej i zautomatyzowanego odzyskiwania, ale ten model jest określany jako model odzyskiwania gorąca. W najwyższym stanie odzyskiwania maszyny wirtualne można zreplikować do w pełni funkcjonalnej, dodatkowej lokacji. To bardziej kosztowne podejście jest nazywane modelem odzyskiwania o wysokiej dostępności lub gorąco-gorącą.

Każdy z powyższych modeli zmniejsza cel czasu odzyskiwania, co przyspiesza przywrócenie możliwości procesu biznesowego. Jednak każdy model również skutkuje znacznie większymi kosztami zarządzania chmurą.

Ten proces myśli zostanie oglądany bardziej szczegółowo w [dyscypliny działania obciążenia](./workload.md).

## <a name="next-steps"></a>Następne kroki

Gdy ten składnik linii bazowej zarządzania zostanie osiągnięty, zespół może uzyskać dalej, aby uniknąć przerw w działaniu [operacji platformy](./platform.md) i [obciążeń](./workload.md).

> [!div class="nextstepaction"]
> Operacje na [platformie](./platform.md) 
> [operacji obciążenia](./workload.md)
