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
ms.openlocfilehash: 44e566d1f2936c51e61f8a1bd4211af2000f454b
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565062"
---
# <a name="protect-and-recover-in-cloud-management"></a>Ochrona i odzyskiwanie w programie Cloud Management

Po spełnieniu wymagań związanych ze [spisem i widocznością](./inventory.md) oraz [zgodnością operacyjną](./operational-compliance.md)zespoły zarządzające chmurą mogą przewidzieć i przygotować się do potencjalnej awarii obciążenia. Po zaplanowaniu zarządzania chmurą zespoły muszą zacząć od założenia, że coś się nie powiedzie.

Żadne rozwiązanie techniczne nie może stale oferować umowy SLA na 100% czasu. Rozwiązania z nadmiarowymi zastosowaniami architektury do dostarczania na "sześć 9" lub na 99,9999 procent czasu. Mimo że rozwiązanie "sześć 9" jest wyłączone przez 31,6 sekund w danym roku. Niestety, jest to rzadkie rozwiązanie, aby mieć gwarancję dużej, trwającej inwestycji operacyjnej, która jest wymagana do osiągnięcia "sześciu 9" czasu pracy.

Przygotowanie do przestojów pozwala zespołowi wykrywać błędy szybciej i szybciej odzyskiwać. Ten dyscyplina dotyczy kroków, które są dostępne natychmiast po awarii systemu. Jak chronić obciążenia, aby można je było szybko odzyskać w przypadku wystąpienia awarii?

## <a name="translate-protection-and-recovery-conversations"></a>Tłumaczenie konwersacji dotyczących ochrony i odzyskiwania

Obciążenia polegające na tym, że operacje w biznesie składają się z aplikacji, danych, maszyn wirtualnych i innych zasobów. Każdy z tych zasobów może wymagać innego podejścia do ochrony i odzyskiwania. Ważnym aspektem tego dyscypliny jest ustanowienie spójnego zobowiązania w ramach linii bazowej zarządzania, które może zapewnić punkt wyjścia podczas dyskusji biznesowej.

Co najmniej każdy element zawartości, który obsługuje dowolne obciążenie, powinien mieć podejście bazowe z wyraźnym zobowiązaniem do przyspieszenia odzyskiwania (cele czasu odzyskiwania lub RTO) i ryzyka utraty danych (cele punktu odzyskiwania lub cel celu).

### <a name="recovery-time-objectives-rto"></a>Cele czasu odzyskiwania (RTO)

Po awarii RTO to czas, jaki należy podjąć w celu odzyskania dowolnego systemu w stanie sprzed awarii. Dla każdego obciążenia, które będzie obejmowały czas wymagany do przywrócenia minimalnej niezbędnej funkcjonalności dla maszyn wirtualnych i aplikacji. Obejmuje to również ilość czasu wymaganą do przywrócenia danych wymaganych przez aplikacje.

W obszarze warunki biznesowe RTO reprezentuje czas, przez jaki proces biznesowy nie będzie działać. W przypadku obciążeń o kluczowym znaczeniu ta zmienna powinna być stosunkowo niska, co pozwala procesom biznesowym szybko wznowić działanie. W przypadku obciążeń o niższym priorytecie standardowy poziom RTO może nie mieć zauważalnego wpływu na wydajność firmy.

Linia bazowa zarządzania powinna ustanowić standardowy RTO dla obciążeń niekrytycznych dla działalności. Firma może następnie użyć tej linii bazowej jako sposobu na wyjustowanie dodatkowych inwestycji w czasy odzyskiwania.

### <a name="recovery-point-objectives-rpo"></a>Cele punktu odzyskiwania (RPO)

W większości systemów zarządzania chmurą dane są okresowo przechwytywane i przechowywane przy użyciu pewnej formy ochrony danych. Czas ostatniego przechwycenia danych jest określany jako punkt odzyskiwania. Awaria systemu może zostać przywrócona tylko do najnowszego punktu odzyskiwania.

Jeśli system ma cel punktu odzyskiwania mierzony w godzinach lub dniach, awaria systemu spowodowałaby utratę danych dla tych godzin lub dni między ostatnim punktem odzyskiwania a awarią. Cel punktu odzyskiwania wynoszący 1 dzień będzie teoretycznie skutkować utratą wszystkich transakcji w dniu, co prowadzi do błędu.

W przypadku systemów o znaczeniu krytycznym, cel punktu odzyskiwania mierzony w minutach lub sekundach może być bardziej odpowiedni do wykorzystania, aby uniknąć utraty przychodu. Jednak krótszy cel punktu odzyskiwania zazwyczaj skutkuje zwiększeniem całkowitych kosztów zarządzania.

Aby zmniejszyć koszty, linia bazowa zarządzania powinna skupić się na najdłuższym akceptowalnym celu punktu odzyskiwania. Zespół zarządzający chmurą może następnie zwiększyć cel punktu odzyskiwania dla określonych platform lub obciążeń, co wymagałoby większej ilości inwestycji.

## <a name="protect-and-recover-workloads"></a>Ochrona i odzyskiwanie obciążeń

Większość obciążeń w środowisku IT obsługuje bardzo mały proces biznesowy lub techniczny. Systemy, które nie mają systemowego wpływu na operacje biznesowe, często nie uzasadniają zwiększonej ilości inwestycji wymaganej do szybkiego odzyskania lub zminimalizowania utraty danych. Tworząc linię bazową, firma może jasno zrozumieć, jaki poziom obsługi odzyskiwania może być oferowany w spójnym, zarządzanym punkcie cen. Te informacje ułatwiają uczestnikom firmy ocenę wartości zwiększonej inwestycji w odzyskiwanie.

W przypadku większości zespołów zarządzania w chmurze rozszerzona linia bazowa ze szczegółowymi zobowiązaniami RPO/RTO dla różnych zasobów zapewnia najbardziej preferowaną ścieżkę do wzajemnych zobowiązań. W poniższych sekcjach przedstawiono kilka typowych rozszerzonych linii bazowych, które umożliwiają firmie łatwe dodawanie funkcji ochrony i odzyskiwania przez powtarzalny proces.

### <a name="protect-and-recover-data"></a>Ochrona i odzyskiwanie danych

Dane są raczej najbardziej cenne zasoby w gospodarce cyfrowej. Możliwość bardziej wydajnego ochrony i odzyskiwania danych jest najbardziej powszechną linią bazową. W przypadku danych, które mają wpływ na obciążenie produkcyjne, utrata danych może być bezpośrednio równa utracie przychodu lub straci zyskowność. Ogólnie zachęcamy zespoły zarządzania chmurą do oferowania poziomu rozszerzonej linii bazowej zarządzania, która obsługuje popularne platformy danych.

Przed zaimplementowaniem operacji platformy przez zespoły zarządzające chmurą często można obsługiwać ulepszone operacje na platformie danych platformy jako usługi (PaaS). Na przykład łatwo jest, aby zespół zarządzający chmurą wymusił wyższą częstotliwość tworzenia kopii zapasowych lub wieloregionowej replikacji dla rozwiązań Azure SQL Database lub Azure Cosmos DB. Dzięki temu zespół programistyczny może łatwo ulepszyć cel punktu odzyskiwania przez po prostu modernizację ich platform danych.

Aby dowiedzieć się więcej o tym procesie myśli, zapoznaj się z artykułem [dyscyplina operacji platformy](./platform.md).

### <a name="protect-and-recover-vms"></a>Ochrona i odzyskiwanie maszyn wirtualnych

Większość obciążeń ma pewną zależność od maszyn wirtualnych, które obsługują różne aspekty rozwiązania. Aby obciążenie obsługiwało proces biznesowy po awarii systemu, należy szybko odzyskać wiele maszyn wirtualnych.

Każda minuta przestoju na tych maszynach wirtualnych może być równa utracie przychodu lub zmniejszyć zyskowność. Gdy czas przestoju maszyny wirtualnej ma bezpośredni wpływ na wydajność działania firmy, RTO jest bardzo ważne. Maszyny wirtualne można odzyskiwać szybciej przy użyciu replikacji do lokacji dodatkowej i zautomatyzowanego odzyskiwania, modelu, który jest określany jako model odzyskiwania gorąca. W najwyższym stanie odzyskiwania maszyny wirtualne można zreplikować do w pełni funkcjonalnej, dodatkowej lokacji. To bardziej kosztowne podejście jest określane jako model odzyskiwania wysokiej dostępności lub gorąca i gorąca.

Każdy z powyższych modeli zmniejsza RTO, co umożliwia szybsze przywracanie możliwości procesu biznesowego. Jednak każdy model również skutkuje znacznie większymi kosztami zarządzania chmurą.

Aby uzyskać więcej informacji na temat tego procesu myśli, zobacz [dyscyplina operacji obciążenia](./workload.md).

## <a name="next-steps"></a>Następne kroki

Po spełnieniu tego składnika linii bazowej zarządzania zespół będzie mógł kontynuować, aby uniknąć przerw w działaniu [operacji platformy](./platform.md) i [obciążeń](./workload.md).

> [!div class="nextstepaction"]
> Operacje na [platformie](./platform.md)
> [operacji obciążenia](./workload.md)
