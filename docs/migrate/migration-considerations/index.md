---
title: Model migracji opisany w przewodniku Cloud Adoption Framework
description: Model migracji opisany w przewodniku Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: db298f40598bc1060c56901d95f7b325ce548abe
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214365"
---
# <a name="cloud-adoption-framework-migration-model"></a>Model migracji opisany w przewodniku Cloud Adoption Framework

W tej części opisu modelu migracji Cloud Adoption Framework wyjaśniono zasady dotyczące tego modelu. Wszędzie tam, gdzie to możliwe, w tej zawartości starano się zachować neutralne podejście co do dostawcy, prowadząc Cię przez procesy i działania, które można zastosować w ramach każdej migracji do chmury, niezależnie od wybranego dostawcy chmury.

## <a name="understand-migration-motivations"></a>Omówienie celów migracji

Migracja do chmury stanowi wysiłek związany z zarządzaniem portfolio, który jest sprytnie ukryty pod postacią wdrożenia technicznego. Podczas procesu migracji zdecydujesz się na przeniesienie niektórych zasobów, zainwestowanie w inne oraz wycofanie przestarzałych lub nieużywanych zasobów. W ramach tego procesu pewne zasoby zostaną zoptymalizowane, poddane refaktoryzacji lub całkowicie zastąpione. Każda z tych decyzji powinna być zgodna z celami migracji do chmury. Najbardziej pomyślne migracje idą również o krok dalej i dostosowują te decyzje do żądanych wyników biznesowych.

Model migracji opisany w przewodniku Cloud Adoption Framework wymaga przeprowadzenia procesu zapewnienia gotowości biznesowej do wdrożenia chmury przez organizację. Pamiętaj, aby zapoznać się z wskazówkami dotyczącymi [planowania](../../strategy/index.md) i [gotowości](../../ready/index.md) w ramach modelu Cloud Adoption Framework w celu określenia celów biznesowych i innych powodów migracji do chmury, jak również wymaganych planów lub szkoleń w organizacji przed przeprowadzeniem procesu migracji w odpowiedniej skali.

> [!NOTE]
> Mimo że planowanie biznesowe jest istotne, równie ważne jest podejście rozwojowe. Równolegle do szerzej zakrojonego planowania biznesowego przez zespół strategiczny ds. chmury, sugerujemy rozpoczęcie migracji pierwszego obciążenia przez zespół wdrożeniowy ds. chmury jako wstępu do działań związanych z migracją na większą skalę. Ta początkowa migracja umożliwi zespołowi uzyskanie praktycznego doświadczenia dotyczącego problemów biznesowych i technicznych związanych z migracją.

## <a name="envision-an-end-state"></a>Przewidywanie stanu końcowego

Przed rozpoczęciem działań związanych z migracją należy określić w przybliżeniu oczekiwany stan końcowy. Na poniższym diagramie przedstawiono punkt początkowy dla infrastruktury, aplikacji i danych w środowisku lokalnym, który definiuje Twój _majątek cyfrowy_. Podczas procesu migracji te zasoby są przenoszone przy użyciu jednej z pięciu strategii migracji opisanych w temacie [Pięć zasad racjonalizacji](../../digital-estate/5-rs-of-rationalization.md).

![Grafika informacyjna dotycząca opcji migracji](../../_images/migrate/migration-options.png)

Migracja i modernizacja obciążeń może obejmować zakres od prostej migracji opartej na _ponownym hostowaniu_ (nazywanej także migracją _lift and shift_) przy użyciu funkcji infrastruktury jako usługi (IaaS), które nie wymagają wprowadzania zmian w kodzie i aplikacji, przez _refaktoryzację_ z minimalnymi zmianami, po _zmianę architektury_ w celu zmodyfikowania i rozszerzenia kodu i funkcji aplikacji, aby wykorzystać możliwości technologii chmurowych.

Natywne strategie chmurowe i strategie typu „platforma jako usługa” (PaaS) polegają na _przebudowaniu_ lokalnych obciążeń przy użyciu ofert platformy Azure i usług zarządzanych. Obciążenia, które mają odpowiednik w postaci ofert w pełni zarządzanego oprogramowania jako usługi (SaaS) w chmurze, można często całkowicie _zastąpić_ tymi usługami w ramach procesu migracji.

> [!NOTE]
> W okresie publicznej wersji zapoznawczej modelu Cloud Adoption Framework w tej części opisu tego modelu podkreślana jest strategia migracji oparta na ponownym hostowaniu. Mimo że rozwiązania PaaS i SaaS zostały omówione jako alternatywy, gdy ma to zastosowanie, skupiono się głównie na migracji obciążeń opartych na maszynach wirtualnych przy użyciu możliwości rozwiązań IaaS.
>
> W pozostałych częściach i przyszłych iteracjach tej zawartości pozostałe podejścia zostaną omówione bardziej szczegółowo. Ogólne omówienie rozszerzania zakresu migracji w celu uwzględnienia bardziej złożonych strategii migracji zawiera artykuł dotyczący równoważenia portfolio.

## <a name="incremental-migration"></a>Migracja przyrostowa

Model migracji Cloud Adoption Framework jest oparty na przyrostowym procesie przekształcenia do chmury. Przyjęto założenie, że organizacja rozpocznie od początkowej migracji do chmury o ograniczonym zakresie, która jest często nazywana pierwszym obciążeniem. Ten nakład pracy będzie rozszerzany przyrostowo o dodatkowe obciążenia wraz z ulepszaniem procesów migracji przez zespoły operacyjne.

Narzędzia do migracji do chmury, takie jak usługa [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview), umożliwiają migrację całych centrów danych złożonych z dziesiątek tysięcy maszyn wirtualnych. Jednak operacje biznesowe i istniejące działy IT rzadko mogą udźwignąć tak szybkie tempo zmian. Z tego względu wiele organizacji dzieli nakład pracy związany z migracją na wiele iteracji, przenosząc jedno obciążenie (lub zbiór obciążeń) na iterację.

Zasady dotyczące tego modelu przyrostowego są oparte na wykonaniu procesów i spełnieniu wymagań wstępnych, do których odwołuje się następująca grafika informacyjna.

![Model migracji opisany w przewodniku Cloud Adoption Framework](../../_images/migrate/methodology.png)

Spójne stosowanie tych zasad reprezentuje końcowy cel procesów migracji do chmury i nie powinno być traktowane jako punkt początkowy. W miarę doskonalenia wysiłków związanych z migracją należy korzystać ze wskazówek w tej sekcji, które ułatwiają definiowanie najlepszego procesu zgodnego z potrzebami organizacji.

## <a name="next-steps"></a>Następne kroki

Zacznij poznawanie tego modelu od [sprawdzenia wymagań wstępnych migracji](./prerequisites/index.md).

> [!div class="nextstepaction"]
> [Wymagania wstępne migracji](./prerequisites/index.md)
