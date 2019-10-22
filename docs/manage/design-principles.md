---
title: Zastosuj zasady projektowania i zaawansowane operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zastosuj zasady projektowania i zaawansowane operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 8595dbadf5a10e19303a50f8eead1ae753612586
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683581"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Zastosuj zasady projektowania i zaawansowane operacje

Pierwsze trzy dyscypliny zarządzania chmurą opisują linię bazową zarządzania. Plan bazowy zarządzania powinien zawierać co najmniej standardowe zobowiązanie biznesowe, aby zminimalizować zakłócenia biznesowe i przyspieszyć odzyskiwanie w przypadku przerwania działania usługi. Większość linii bazowych zarządzania obejmuje skoncentrowany nacisk na utrzymanie "spisu i widoczności", "zgodność operacyjna" oraz "Ochrona i odzyskiwanie".

Celem punktu odniesienia zarządzania jest utworzenie spójnej oferty zapewniającej minimalny poziom zobowiązania biznesowego dla wszystkich obsługiwanych obciążeń. Ta linia bazowa wspólnych, powtarzalnych ofert zarządzania pozwala zespołowi zapewnić wysoce zoptymalizowany stopień zarządzania operacyjnego przy minimalnym odchyleniu. Jednak oferta standardowa może nie zapewniać szerokiej ilości wolnego zobowiązania dla firmy. Poniższy obraz i punktory przedstawiają trzy sposoby przechodzenia poza linię bazową zarządzania.

Linia bazowa zarządzania powinna spełniać minimalne zobowiązanie wymagane przez 80% najniższych obciążeń o krytycznym znaczeniu w portfolio. Nie należy stosować linii bazowej do obciążeń o kluczowym znaczeniu. Nie powinna również być stosowana do popularnych platform udostępnionych w ramach obciążeń. Wymagają one skoncentrowania się na zasadach projektowania i zaawansowanych operacjach.

## <a name="advanced-operations-options"></a>Zaawansowane opcje operacji

Istnieją trzy sugerowane ścieżki na potrzeby ulepszania zobowiązań firmy poza planem bazowym zarządzania.

![Operacje zaawansowane](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Rozszerzona linia bazowa zarządzania

Zgodnie z opisem w przewodniku zarządzania systemu Azure, rozszerzona linia bazowa zarządzania używa natywnych narzędzi do obsługi chmury w celu zwiększenia czasu przestoju i skrócenia czasów odzyskiwania. Ulepszenia są znaczące, ale znacznie mniejsze niż w przypadku używania obciążeń lub specjalizacji platformy. Zaletą ulepszonej linii bazowej zarządzania jest równie znacząca redukcja kosztów i czasu implementacji.

## <a name="management-specialization"></a>Specjalizacja zarządzania

Aspekty obciążeń i operacji na platformie mogą wymagać zmian w regułach projektowania i architektury. Te zmiany mogą zająć trochę czasu i mogą spowodować zwiększenie kosztów operacyjnych. Aby zmniejszyć liczbę obciążeń wymagających takich inwestycji, rozszerzona linia bazowa zarządzania może zapewnić wystarczającą poprawę zobowiązania biznesowego.

W przypadku obciążeń, które gwarantują wyższy nakład inwestycyjny, aby sprostać zobowiązaniom biznesowym, specjalizacja operacji jest kluczowa.

## <a name="areas-of-management-specialization"></a>Obszary specjalizacji zarządzania

Istnieją dwa obszary specjalizacji:

- **Specjalizacja platformy:** Inwestować w bieżące operacje udostępnionej platformy, Dystrybuując inwestycje na wiele obciążeń.
- **Specjalizacja obciążenia:** Inwestować w bieżące operacje określonego obciążenia, ogólnie zarezerwowane dla obciążeń o znaczeniu krytycznym.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Centralne centrum IT lub Cloud Center doskonałości (CCoE)

Decyzje między specjalizacją platformy a specjalizacją obciążeń opierają się na znaczeniu i wpływie poszczególnych obciążeń. Jednakże niniejsza decyzja stanowi również wskazówkę o większej decyzji kulturalnej między Centralnym modelem organizacji IT i CCoE.

Specjalizacja obciążeń często wyzwala zmianę kulturową. Tradycyjnie i centralne tworzenie procesów kompilacji, które mogą zapewnić pomoc techniczną w skali. Obsługa skalowania jest bardziej osiągalna dla powtarzających się usług, które znajdują się w linii bazowej zarządzania, rozszerzonej linii bazowej lub nawet operacji na platformie. Specjalizacja obciążeń nie jest często skalowana. Brak skalowania utrudnia scentralizowanej organizacji IT zapewnienie niezbędnej pomocy technicznej bez osiągania ograniczeń skali organizacyjnej.

Alternatywnie rozwiązanie Cloud Center of doskonałości jest skalowane przez nigdy wykonywane celowo delegowanie odpowiedzialności i selektywnej centralizacji. Specjalizacja obciążeń jest lepiej wyrównana z delegowanym podejściem do CCoE. Poniżej przedstawiono proste wyrównanie ról w CCoE. Zespół platformy w chmurze pomaga tworzyć popularne platformy, które obsługują wiele zespołów wdrożenia chmury. Zespół usługi Cloud Automation rozszerza te elementy do zasobów do wdrożenia w katalogu usług. Zarządzanie chmurą umożliwia centralne zarządzanie punktem odniesienia i ułatwia korzystanie z katalogu usług. Jednak jednostka biznesowa (w formie zespołu DevOps Business lub zespołu wdrażania w chmurze) jest odpowiedzialna za codzienne operacje związane z obciążeniem, potokiem lub wydajnością.

W przypadku wyrównywania obszarów zarządzania centralne modele IT i CCoE mogą ogólnie dostarczać w ramach specjalizacji platformy przy minimalnych zmianach kulturowych. Dostarczanie w ramach specjalizacji obciążeń może być nieco bardziej skomplikowane dla centralnych zespołów IT.

## <a name="management-specialization-processes"></a>Procesy specjalizacji zarządzania

W ramach każdej specjalizacji Poniższy cztery kroki procesu są dostarczane w sposób iteracyjny. Takie podejście wymaga partnerstwa z wdrażaniem w chmurze, platformą chmury, automatyzacją chmury i ekspertami zarządzania chmurą w celu utworzenia realnej i świadomej pętli do przesyłania opinii.

- **Ulepszanie projektu systemu:** Usprawnij projektowanie typowych systemów (platform) lub określonych obciążeń, aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach może być bardziej zrozumiałe, aby zautomatyzować korygowanie i zmniejszyć wpływ przerw.
- **Skaluj rozwiązanie:** W miarę poprawy projektowania systemów i automatycznego korygowania te zmiany mogą być skalowane w całym środowisku za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Różne narzędzia do monitorowania mogą służyć do wykrywania ulepszeń przyrostowych, które mogą być rozkierowane w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

### <a name="improve-system-design"></a>Ulepszanie projektu systemu

Ulepszenie projektowania systemu to najbardziej efektywne podejście do ulepszania operacji na każdej wspólnej platformie. Dzięki udoskonaleniom projektu systemu stabilność może wzrosnąć, a przerwy w działaniu mogą ulec zmniejszeniu. Projektowanie poszczególnych systemów jest poza zakresem dla widoku środowiska wykonywanego w całej strukturze wdrożenia chmury. Jako uzupełnienie tego środowiska struktura architektury platformy Azure oferuje najlepsze rozwiązania w zakresie poprawy odporności i projektowania określonego systemu. Te udoskonalenia projektowe mogą być stosowane do projektowania systemów platformy lub określonego obciążenia.

Platforma architektury Azure koncentruje się na ulepszaniu pięciu filarów projektowania systemu:

- **Skalowalność:** Skalowanie wspólnych zasobów platformy w celu obsługi zwiększonego obciążenia.
- **Dostępność:** Zmniejszenie prawdopodobieństwa biznesowego przez zwiększenie potencjału czasu przestoju.
- **Odporność:** Zwiększ czas odzyskiwania, aby skrócić czas trwania przerw.
- **Zabezpieczenia:** Ochrona aplikacji i danych przed zagrożeniami zewnętrznymi.
- **Zarządzanie:** Procesy operacji specyficzne dla tych typowych zasobów platformy.

Większość przerw w działalności biznesowej jest równa pewnej liczbie długów technicznych lub niedoborów w architekturze. W przypadku istniejących wdrożeń ulepszenia projektowania systemów można wyświetlać jako płatności związane z istniejącym długem technicznym. W przypadku nowych wdrożeń ulepszenia projektowania systemów można wyświetlić jako unikanie długu technicznego. Na następnej karcie "Automatyczne korygowanie" są sprawdzane sposoby rozwiązywania długu technicznego, którego nie można rozwiązać ani czy nie.

Dowiedz się więcej o [strukturze architektury platformy Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) , aby poprawić projekt systemu. Ponieważ projekt systemu jest ulepszony, Wróć do tego artykułu, aby znaleźć nowe możliwości ulepszania i skalowania ulepszeń w danym środowisku.

### <a name="automated-remediation"></a>Automatyczne korygowanie

Niemniej w przypadku niektórych długów technicznych nie można rozwiązać tego problemu. Rozwiązanie może być zbyt kosztowne, aby można było je poprawić. Rozwiązanie może być zaplanowane, ale ma długi czas trwania projektu. Może się zdarzyć, że przerwa działające w firmie nie ma znaczącego wpływu na działalność firmy lub że priorytet firmy ma na celu szybkie odzyskanie, zamiast inwestowania w odporności.

Jeśli rozwiązanie długu technicznego nie jest pożądaną ścieżką, zautomatyzowane korygowanie jest zwykle żądanym następnym krokiem. Używanie Azure Automation i Azure Monitor do wykrywania trendów i zapewnienia automatycznego korygowania to najczęstsze podejście do automatycznego korygowania.

Aby uzyskać wskazówki dotyczące automatycznego korygowania, zobacz ten artykuł dotyczący [Azure Automation i alertów](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Skalowanie rozwiązania przy użyciu katalogu usług

Podstawą specjalizacji platformy i operacji platformy jest dobrze zarządzany katalog usług. Jest to sposób, w jaki ulepszenia projektowania i korygowania systemów są skalowane w środowisku. Zespół platformy w chmurze i zespół usługi Cloud Automation wyrównaniają, aby tworzyć powtarzalne rozwiązania dla najpopularniejszych platform w dowolnym środowisku. Ale jeśli te rozwiązania nie są stale wykorzystywane, zarządzanie chmurą może być nieco bardziej niż oferta podstawowa.

Aby zmaksymalizować wdrożenie i zminimalizować obciążenie związane z konserwacją dowolnej zoptymalizowanej platformy, należy dodać platformę do katalogu usług. Każdą aplikację w katalogu można wdrożyć do użytku wewnętrznego za pośrednictwem katalogu usług lub jako ofertę w portalu Marketplace dla użytkowników zewnętrznych.

Aby uzyskać instrukcje dotyczące publikowania w katalogu usług, zapoznaj się z serią artykułów w temacie [Publikowanie w katalogu usług](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Ciągłe ulepszanie

Specjalizacja platformy i operacje na platformie są zależne od pomyślnych pętli między przyjęciem, platformą, automatyzacją i zespołami zarządzania. Nadanie tych zwrotnych pętli w danych pozwala każdemu zespołowi podejmować decyzje. W przypadku operacji na platformie w celu osiągnięcia długoterminowych zobowiązań gospodarczych ważne jest wykorzystanie szczegółowych informacji dotyczących scentralizowanej platformy. Ponieważ kontenery i SQL Server są dwa najpopularniejsze platformy zarządzane centralnie, poniżej przedstawiono kilka artykułów ułatwiających rozpoczęcie pracy z zbieraniem danych ciągłego ulepszania.

Wydajność [kontenera](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview) 
[PaaS Database](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql) 
 wydajności bazy[danych IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
