---
title: Zastosuj zasady projektowania i zaawansowane operacje
description: Zastosuj zasady projektowania i zaawansowane operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 16762a0eae366c3bf1cd578faaf52df60e6c97b1
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807686"
---
# <a name="apply-design-principles-and-advanced-operations"></a>Zastosuj zasady projektowania i zaawansowane operacje

Pierwsze trzy dyscypliny zarządzania chmurą opisują plan bazowy zarządzania. Plan bazowy zarządzania powinien zawierać co najmniej standardowe zobowiązanie biznesowe, aby zminimalizować zakłócenia biznesowe i przyspieszyć odzyskiwanie w przypadku przerwania działania usługi. Większość linii bazowych zarządzania obejmuje skoncentrowany fokus na utrzymywaniu "spisu i widoczności", "zgodność operacyjna" oraz "Ochrona i odzyskiwanie".

Celem punktu odniesienia zarządzania jest utworzenie spójnej oferty zapewniającej minimalny poziom zobowiązania biznesowego dla wszystkich obsługiwanych obciążeń. Ta linia bazowa wspólnych, powtarzalnych ofert zarządzania umożliwia zespołowi dostarczanie wysoce zoptymalizowanego stopnia zarządzania operacyjnego przy minimalnym odchyleniu. Jednak oferta standardowa może nie zapewnić rozbudowanego, wystarczającego zobowiązania dla firmy.

Diagram w następnej sekcji ilustruje trzy sposoby przechodzenia poza linię bazową zarządzania.

Linia bazowa zarządzania powinna spełniać minimalne zobowiązanie wymagane przez 80 procent najniższych obciążeń o krytycznym znaczeniu w portfolio. Nie należy stosować linii bazowej do obciążeń o kluczowym znaczeniu. Nie powinna również być stosowana do popularnych platform, które są współużytkowane przez obciążenia. Te obciążenia wymagają skoncentrowania się na zasadach projektowania i zaawansowanych operacjach.

## <a name="advanced-operations-options"></a>Zaawansowane opcje operacji

Istnieją trzy sugerowane ścieżki na potrzeby ulepszania zobowiązań firmy poza planem bazowym zarządzania, jak pokazano na poniższym diagramie:

![Operacje zaawansowane](../_images/manage/beyond-the-baseline.png)

## <a name="enhanced-management-baseline"></a>Rozszerzona linia bazowa zarządzania

Zgodnie z opisem w przewodniku zarządzania systemu Azure, rozszerzona linia bazowa zarządzania używa natywnych narzędzi do obsługi chmury, aby zwiększyć czas przestoju i skrócić czas odzyskiwania. Ulepszenia są znaczące, ale mniej tak samo, jak przy użyciu obciążeń lub specjalizacji platformy. Zaletą ulepszonej linii bazowej zarządzania jest równie znacząca redukcja kosztów i czasu implementacji.

## <a name="management-specialization"></a>Specjalizacja zarządzania

Aspekty obciążeń i operacji na platformie mogą wymagać zmian w zakresie projektowania i reguł architektury. Te zmiany mogą zająć trochę czasu i mogą spowodować zwiększenie kosztów operacyjnych. Rozszerzony plan bazowy zarządzania pozwala zmniejszyć liczbę obciążeń wymagających takich inwestycji, zapewniając wystarczającą poprawę zobowiązania biznesowego.

W przypadku obciążeń, które gwarantują wyższy nakład inwestycyjny, aby sprostać zobowiązaniom biznesowym, specjalizacja operacji jest kluczowa.

## <a name="areas-of-management-specialization"></a>Obszary specjalizacji zarządzania

Istnieją dwa obszary specjalizacji:

- **Specjalizacja platformy:** Inwestować w bieżące operacje udostępnionej platformy, Dystrybuując inwestycje na wiele obciążeń.
- **Specjalizacja obciążenia:** Inwestować w bieżące operacje określonego obciążenia, ogólnie zarezerwowane dla obciążeń o kluczowym znaczeniu.

### <a name="central-it-or-cloud-center-of-excellence-ccoe"></a>Centralne centrum IT lub Cloud Center doskonałości (CCoE)

Decyzje między specjalizacją platformy a specjalizacją obciążeń opierają się na znaczeniu i wpływie poszczególnych obciążeń. Jednakże te decyzje są również wskazujące na większe decyzje kulturalne między Centralnym modelem organizacji IT i CCoE.

Specjalizacja obciążeń często wyzwala zmianę kulturową. Tradycyjnie i centralne tworzenie procesów kompilacji, które mogą zapewnić pomoc techniczną w skali. Obsługa skalowania jest bardziej osiągalna dla powtarzających się usług, które znajdują się w linii bazowej zarządzania, rozszerzonej linii bazowej lub nawet operacji na platformie. Specjalizacja obciążeń nie jest często skalowana. Brak skalowania utrudnia scentralizowanej organizacji IT zapewnienie niezbędnej pomocy technicznej bez osiągania ograniczeń skali organizacyjnej.

Alternatywnie Centrum rozwiązań doskonałości przeskaluje się w drodze nigdy wykonywane celowo delegowania odpowiedzialności i selektywnej centralizacji. Specjalizacja obciążeń jest lepiej wyrównana z delegowanym podejściem do CCoE.

Naturalne wyrównanie ról w CCoE jest opisane w następujący sposób:

- Zespół platformy w chmurze pomaga tworzyć popularne platformy, które obsługują wiele zespołów wdrożenia chmury.
- Zespół usługi Cloud Automation rozszerza te platformy do zasobów do wdrożenia w katalogu usług.
- Zarządzanie chmurą umożliwia centralne zarządzanie punktem odniesienia i ułatwia korzystanie z katalogu usług.
- Jednak jednostka biznesowa (w formie zespołu DevOps Business lub zespołu wdrażania w chmurze) jest odpowiedzialna za codzienne operacje związane z obciążeniem, potokiem lub wydajnością.

Podobnie jak w przypadku wyrównania obszarów zarządzania, centralne modele IT i CCoE mogą ogólnie dostarczać w ramach specjalizacji platformy przy minimalnych zmianach kulturowych. Dostarczanie w ramach specjalizacji obciążeń może być nieco bardziej skomplikowane dla centralnych zespołów IT.

## <a name="management-specialization-processes"></a>Procesy specjalizacji zarządzania

W ramach każdej specjalizacji następujący dwuetapowy proces jest dostarczany w postaci podejścia do iteracji. Takie podejście wymaga partnerstwa między wdrożeniem chmury, platformą chmury, automatyzacją chmury i ekspertami zarządzania chmurą w celu utworzenia realnej i świadomej pętli do przesyłania opinii.

- **Ulepszanie projektu systemu:** Usprawnij projektowanie typowych systemów (platform) lub określonych obciążeń, aby skutecznie zminimalizować przerwy.
- **Automatyzacja korygowania:** Niektóre ulepszenia nie są opłacalne. W takich przypadkach może być bardziej zrozumiałe, aby zautomatyzować korygowanie i zmniejszyć wpływ przerw.
- **Skaluj rozwiązanie:** Ulepszona funkcja projektowania i automatycznego korygowania systemów pozwala skalować te zmiany w środowisku za pośrednictwem katalogu usług.
- **Ciągłe ulepszanie:** Możesz użyć różnych narzędzi do monitorowania, aby poznać przyrostowe udoskonalenia dla adresu w następnym przebiegu projektowania, automatyzacji i skalowania systemu.

### <a name="improve-system-design"></a>Ulepszanie projektu systemu

Ulepszanie projektu systemu to najbardziej efektywne podejście do usprawnienia operacji na każdej typowej platformie. Ulepszenia projektowania systemu mogą pomóc zwiększyć stabilność i zmniejszyć liczbę przerw w działaniu firmy. Projektowanie poszczególnych systemów jest poza zakresem widoku środowiska na platformie Cloud Adoption Framework. W ramach uzupełnienia tej platformy usługa Azure Architecture Framework oferuje najlepsze rozwiązania w zakresie poprawy odporności i projektowania określonego systemu. Można zastosować te ulepszenia projektowe do projektowania systemów platformy lub określonego obciążenia.

Usługa Azure Architecture Framework koncentruje się na poprawie pięciu filarów projektowania systemu:

- **Skalowalność:** Skalowanie wspólnych zasobów platformy w celu obsługi zwiększonego obciążenia.
- **Dostępność:** Zmniejszenie prawdopodobieństwa biznesowego przez zwiększenie potencjału czasu przestoju.
- **Odporność:** Zwiększenie czasów odzyskiwania w celu skrócenia czasu trwania przerw w działaniu.
- **Zabezpieczenia:** Ochrona aplikacji i danych przed zagrożeniami zewnętrznymi.
- **Zarządzanie:** Procesy operacji specyficzne dla tych typowych zasobów platformy.

Większość przerw w działalności biznesowej oznacza jakąś formę długu technicznego lub brak w architekturze. W przypadku istniejących wdrożeń ulepszenia projektowania systemów można widzieć jako płatności związane z istniejącym długiem technicznym. W przypadku nowych wdrożeń ulepszenia projektowania systemów można widzieć jako unikanie długu technicznego. W następnej sekcji "Automatyczne korygowanie" są sprawdzane sposoby rozwiązywania długów technicznych, których nie można rozwiązać ani nie należy ich dotyczyć.

Aby ulepszyć projekt systemu, Dowiedz się więcej o [architekturze architektury platformy Azure](https://docs.microsoft.com/azure/architecture/guide/pillars). W miarę ulepszania projektu systemu Wróć do tego artykułu, aby znaleźć nowe możliwości ulepszania i skalowania ulepszeń w środowisku.

### <a name="automated-remediation"></a>Zautomatyzowane korygowanie

Nie można rozwiązać niektórych długów technicznych ani nie należy do nich. Rozwiązanie może być zbyt drogie w naprawie. Może być planowana, ale może być długi czas trwania projektu. Przerwa działające w firmie może nie mieć znaczącego wpływu na działalność biznesową, a priorytet firmy ma na celu szybkie odzyskanie, zamiast inwestowania w odporności.

Jeśli pozbycie się długu technicznego nie jest najbardziej pożądane, następnym krokiem jest zazwyczaj zautomatyzowane korygowanie. Najpopularniejszą metodą zautomatyzowanego korygowania jest wykrywanie trendów i zapewnienie zautomatyzowanego korygowania przy użyciu usług Azure Automation i Azure Monitor.

Aby uzyskać wskazówki dotyczące zautomatyzowanego korygowania, zobacz [Azure Automation i alerty](https://docs.microsoft.com/azure/automation/automation-create-alert-triggered-runbook).

### <a name="scale-the-solution-with-a-service-catalog"></a>Skalowanie rozwiązania przy użyciu katalogu usług

Podstawą specjalizacji platformy i operacji platformy jest dobrze zarządzany katalog usług. Jest to sposób skalowania ulepszeń projektowania i korygowania systemów w środowisku. Zespół platformy w chmurze współpracuje z zespołem automatyzacji chmury, tworząc powtarzalne rozwiązania dla najpopularniejszych platform w dowolnym środowisku. Ale jeśli te rozwiązania nie są stosowane w sposób ciągły, zarządzanie chmurą może zapewnić nieco więcej niż ofertę bazową.

Aby zmaksymalizować wdrożenie i zminimalizować obciążenie związane z konserwacją dowolnej zoptymalizowanej platformy, należy dodać platformę do katalogu usług. Każdą aplikację w katalogu można wdrożyć do użytku wewnętrznego za pośrednictwem katalogu usług lub jako ofertę platformy handlowej dla użytkowników zewnętrznych.

Informacje o publikowaniu w katalogu usług znajdują się w sekcji w temacie [Publikowanie w katalogu usług](https://docs.microsoft.com/azure/managed-applications/publish-service-catalog-app).

### <a name="continuous-improvement"></a>Ciągłe ulepszanie

Specjalizacja i operacje platformy zależą od silnych cykli wymiany opinii między zespołami wdrażania, platformy, automatyzacji i zarządzania. Osadzenie tych cykli wymiany opinii w danych pozwala każdemu zespołowi podejmować mądre decyzje. W przypadku operacji na platformie w celu osiągnięcia długoterminowych zobowiązań gospodarczych należy skorzystać z szczegółowych informacji, które są specyficzne dla scentralizowanej platformy. Ponieważ kontenery i SQL Server są dwa najpopularniejsze platformy zarządzane centralnie, należy rozważyć wprowadzenie do zbierania danych ciągłego ulepszania, przeglądając następujące artykuły:

- [Wydajność kontenerów](https://docs.microsoft.com/azure/azure-monitor/insights/container-insights-overview)
- [Wydajność bazy danych PaaS](https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql)
- [Wydajność bazy danych IaaS](https://docs.microsoft.com/azure/azure-monitor/insights/sql-assessment)
