---
title: Ocena każdego obciążenia i uściślanie planów
description: Skorzystaj z podręcznika Cloud Adoption Framework dla platformy Azure w celu oceny możliwości środowiska do migracji oraz metod, które należy wziąć pod uwagę.
author: matticusau
ms.author: mlavery
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: bbe61dfa9962d194ddb994b6753c2cbd07a9997f
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "81120723"
---
# <a name="assess-workloads-and-refine-plans"></a>Ocena obciążeń i uściślanie planów

Zasoby w tym przewodniku pomagają ocenić każde obciążenie, zakwestionować założenia dotyczące możliwości migracji poszczególnych obciążeń oraz podjąć ostateczne decyzje dotyczące architektury w przypadku opcji migracji.

<!-- markdownlint-disable MD025 -->

# <a name="tools"></a>[Narzędzia](#tab/Tools)

Jeśli nie zastosowano wskazówek określonych w powyższych linkach, prawdopodobnie będziesz potrzebować danych i narzędzia do oceny, aby podjąć świadome decyzje dotyczące migracji. Usługa Azure Migrate jest natywnym narzędziem do oceny **oraz** migracji na platformę Azure. Jeśli jeszcze tego nie zrobiono, wykonaj te kroki, aby utworzyć nowy projekt migracji serwera i zebrać niezbędne dane.

## <a name="azure-migrate"></a>Azure Migrate

Usługa Azure Migrate ocenia lokalną infrastrukturę, aplikacje i dane pod kątem migracji na platformę Azure. Ta usługa:

- Ocenia możliwość migracji zasobów lokalnych.
- Określa rozmiary na podstawie wydajności.
- Szacuje koszty uruchamiania zasobów lokalnych na platformie Azure.

Ta usługa jest przeznaczona dla osób, które zamierzają przeprowadzić migrację metodą „lift-and-shift” lub dopiero zaczęły oceniać możliwość migracji. Po zakończeniu oceny przeprowadź migrację za pomocą usługi Azure Migrate.

![Azure Migrate — przegląd](./media/assess/azure-migrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Tworzenie nowego projektu migracji serwera

Rozpocznij ocenę migracji serwera przy użyciu usługi Azure Migrate, wykonując następujące czynności:

1. Wybierz opcję **Azure Migrate**.
1. W obszarze **Przegląd** wybierz pozycję **Ocena i migracja serwerów**.
1. Wybierz pozycję **Dodaj narzędzia**.
1. W obszarze **Odnajdywanie, ocena i migracja serwerów** wybierz pozycję **Dodaj narzędzia**.
1. W obszarze **Projekt migracji** wybierz subskrypcję platformy Azure i utwórz grupę zasobów, jeśli jej nie masz.
1. W obszarze **Szczegóły projektu** określ nazwę projektu i lokalizację geograficzną, w której chcesz utworzyć projekt, a następnie wybierz pozycję **Dalej**.
1. W obszarze **Wybierz narzędzie oceny**, wybierz pozycję **Pomiń teraz dodawanie narzędzia oceny > Dalej**.
1. W obszarze **Wybierz narzędzie migracji** wybierz pozycję **Azure Migrate: Server Migration > Dalej**.
1. W obszarze **Przegląd i dodawanie narzędzi** przejrzyj ustawienia, a następnie wybierz pozycję **Dodaj narzędzia**.
1. Po dodaniu narzędzia pojawia się ono w obszarze **Projekt usługi Azure Migrate > Serwery > Narzędzia migracji**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Migrate — przegląd](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrowanie serwerów fizycznych lub zwirtualizowanych na platformę Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Usługa Azure Migrate w witrynie Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Mapa usługi

Mapa usługi automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapuje komunikację między usługami. Dzięki usłudze Service Map można wyświetlać serwery w sposób, w jakich się o nich myśli: jako wzajemnie połączone systemy dostarczające usługi. Usługa Service Map pokazuje połączenia między serwerami i procesami, opóźnienie połączeń przychodzących i wychodzących oraz porty dla każdej architektury połączonej za pomocą protokołu TCP. Nie jest wymagana żadna konfiguracja, wystarczy zainstalować agenta.

Usługi Azure Migrate korzystają z usługi Service Map, aby zwiększyć możliwości raportowania i zależności w środowisku. Aby poznać wszystkie szczegóły tej integracji, zobacz [Wizualizacja zależności](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization). W przypadku korzystania z usługi Azure Migration nie ma dodatkowych kroków wymaganych do skonfigurowania usługi Service Map i korzystania z niej. Poniższe instrukcje udostępniono w celach informacyjnych użytkownikom, którzy chcą używać usługi Service Map do innych celów lub projektów.

### <a name="enable-dependency-visualization-using-service-map"></a>Włączanie wizualizacji zależności przy użyciu usługi Service Map

Aby można było używać wizualizacji zależności, pobierz i zainstaluj agenty na każdej maszynie lokalnej, która ma zostać przeanalizowana.

- [Program Microsoft Monitoring Agent (MMA)](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) musi być zainstalowany na każdej maszynie.
- [Agent zależności firmy Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) musi być zainstalowany na każdej maszynie.
- Ponadto w przypadku maszyn, które nie są połączone z Internetem, pobierz i zainstaluj na nich bramę usługi Log Analytics.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Dowiedz się więcej

- [Korzystanie z rozwiązania Service Map na platformie Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate i Service Map: wizualizacja zależności](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="challenge-assumptions"></a>[Kwestionowanie założeń](#tab/Challenge-Assumptions)

W idealnej migracji każdy zasób (infrastruktura, aplikacja lub dane) jest zgodny z platformą w chmurze oraz gotowy do migracji lub modernizacji. W rzeczywistości nie wszystkie obciążenia powinny być migrowane do chmury. Nie każdy zasób jest zgodny z platformami w chmurze. Przed migracją obciążenia do chmury oceń każde obciążenie i wszystkie zależne zasoby (infrastrukturę, aplikacje i dane).

W temacie [Metodologia planowania dla struktury Cloud Adoption Framework](../../plan/index.md) zaleca się stosowanie zasad [racjonalizacji przyrostowej](../../digital-estate/rationalize.md#incremental-rationalization) i [potęg dziesięciu](../../digital-estate/rationalize.md#release-planning) podczas oceny i planowania migracji. Te wskazówki obejmują też szczegółowe najlepsze rozwiązania dotyczące [szacowania majątku cyfrowego przy użyciu usługi Azure Migrate](../../plan/contoso-migration-assessment.md).

W powyższych linkach sugeruje się, że założenia są akceptowalne i często wskazane podczas etapów planowania migracji. Teraz jednak należy przystąpić do działań. Przed migracją do chmury należy zakwestionować te założenia na podstawie poszczególnych obciążeń.

## <a name="two-steps-of-incremental-rationalization"></a>Dwa kroki racjonalizacji przyrostowej

Pomyślne przeprowadzenie [racjonalizacji przyrostowej](../../digital-estate/rationalize.md#incremental-rationalization) wymaga dwóch równie ważnych kroków. Oba kroki wymagają danych i szczegółowych informacji o środowisku. Jednak każde podejście uwzględnia ilość czasu i szczegółowość wymagane do pomyślnego przeprowadzenia migracji.

- **[Planowanie wydań według zasady potęg dziesięciu](../../digital-estate/rationalize.md#release-planning):** Podczas wstępnej racjonalizacji i planowania wydań należy użyć tylko jednej z [5 zasad racjonalizacji](../../digital-estate/5-rs-of-rationalization.md) w ramach oceny. Przeprowadź oszacowanie i planowanie na podstawie opcji racjonalizacji, która najlepiej pasuje do ogólnych motywacji zdefiniowanych w [dokumencie dotyczącym strategii wdrażania chmury](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

- **Szczegółowa ocena poszczególnych obciążeń:** Założenia związane z planowaniem wydań według zasady potęg dziesięciu są wystarczające do utworzenia planu. Jednak te same założenia mogą powodować istotne problemy, jeśli nie zostaną ocenione przed migracją.

## <a name="challenge-assumptions-and-update-the-plan"></a>Kwestionowanie założeń i aktualizowanie planu

Dokładnie przejrzyj dane oceny w usłudze Azure Migrate lub wybranym narzędziu do oceny. Te dane zapewnią wgląd w problemy ze zgodnością, wymagania dotyczące korygowania, sugestie dotyczące rozmiarów i inne zagadnienia.

Przed migracją użyj tych danych oraz przeprowadź dyskusje w celu uzyskania informacji od właściciela produktu, zespołów programistycznych, administratorów i innych osób, aby ocenić możliwość migracji tego konkretnego obciążenia. Użyj uzyskanych informacji, aby zakwestionować podstawowe założenia dotyczące tego obciążenia. Jeśli ustalenia zmienią plan migracji lub wdrażania, odpowiednio zaktualizuj plan.

Pierwszym krokiem zakwestionowania tych założeń jest [przejrzenie wszystkich 5 zasad racjonalizacji](../../digital-estate/rationalize.md).

    - Czy przyjęta metoda racjonalizacji sprawdza się w przypadku tego obciążenia? Czy jest to najlepsza metoda?
    - Czy [fizyczne warunki replikacji](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication) wpłyną na migrację tego obciążenia?
    - Czy to obciążenie wymaga [działań korygujących](../migration-considerations/assess/evaluate.md) przed migracją?

Takie typy pytań pomagają zakwestionować założenia i ustalić najlepszą ścieżkę dla każdego obciążenia.

Aby uzyskać rozszerzoną listę pytań oraz zdefiniowany proces weryfikacji założeń, zobacz [omówienie ulepszeń procesu oceny](../migration-considerations/assess/index.md).

# <a name="scenarios-and-stakeholders"></a>[Scenariusze i osoby biorące udział w projekcie](#tab/Scenarios)

## <a name="scenarios"></a>Scenariusze

Ten przewodnik obejmuje następujące scenariusze:

- **Starszy sprzęt:** Migracja w celu uniezależnienia się od starszego sprzętu, w przypadku którego zbliża się koniec okresu świadczenia pomocy technicznej lub dostępności sprzętu.
- **Wzrost pojemności:** Zwiększenie pojemności zasobów (infrastruktury, aplikacji i danych) do wielkości, której nie jest w stanie zapewnić bieżąca infrastruktura.
- **Modernizacja centrum danych:** Powiększenie lub modernizacja centrum danych w technologii chmury, aby zapewnić nowoczesność i konkurencyjność firmy.
- **Modernizacja aplikacji lub usługi:** Aktualizacja aplikacji w celu korzystania z funkcji natywnych dla chmury. Nawet jeśli wstępnym celem jest strategia migracji na potrzeby zmiany hostowania, możliwość tworzenia planów przeglądu aplikacji lub usług oraz potencjalnej modernizacji jest typowym procesem w każdej migracji.

### <a name="organizational-alignment-and-stakeholders"></a>Zgodność organizacyjna i osoby biorące udział w projekcie

Pełna lista osób biorących udział w projekcie zależy od konkretnego projektu migracji. Najlepszym rozwiązaniem jest założenie, że na początku planowania migracji nie będą znane wszystkie osoby biorące udział w projekcie, ponieważ są one często identyfikowane tylko podczas niektórych faz projektu. Jednak przed rozpoczęciem każdego projektu migracji należy zidentyfikować najważniejszych liderów firmy z zakresu finansów, infrastruktury IT oraz grup ds. zastosowań, uczestniczących w ogólnych działaniach w zakresie migrowania organizacji do chmury.

Utworzenie podstawowego zespołu ds. strategii w chmurze, opartego na najważniejszych osobach biorących udział w projekcie, może pomóc w przygotowaniu organizacji do wdrożenia w chmurze i przeprowadzeniu ogólnych działań związanych z migracją w chmurze. Ten zespół jest odpowiedzialny za interpretację technologii chmurowych i procesów migracji, uzasadnienie biznesowe migracji oraz określenie najlepszych rozwiązań wysokiego poziomu na potrzeby migracji. Członkowie zespołu ułatwiają również identyfikację konkretnych osób biorących udział w projekcie z ramienia grup ds. zastosowań i firmy w celu zapewnienia pomyślnej migracji oraz współpracę z nimi.

Aby uzyskać więcej informacji o przygotowywaniu organizacji do migrowania do chmury, zobacz wskazówki na temat struktury Cloud Adoption Framework dotyczące [wstępnej zgodności organizacyjnej](../../plan/initial-org-alignment.md).

# <a name="timelines"></a>[Harmonogram](#tab/Timelines)

Klienci zwykle stwierdzają, że scenariusz migracji opisany w tym przewodniku można zrealizować w ciągu od jednego do sześciu miesięcy.

Podczas oceniania harmonogramu migracji rozważ następujące kwestie:

- **Zasoby (infrastruktury, aplikacji i danych) do zmigrowania:** Liczba i różnorodność zasobów.
- **Gotowość personelu:** Czy pracownicy są przygotowani do zarządzania nowym środowiskiem, czy są potrzebne szkolenia?
- **Finansowanie:** Czy uzyskano odpowiednie zatwierdzenia i budżet do zrealizowania migracji?
- **Zarządzanie zmianami:** Czy firma ma określone wymagania dotyczące implementacji zmian i zatwierdzania?
- **Regulacje branżowe:** Czy konieczne jest przestrzeganie przepisów branżowych?

# <a name="cost-management"></a>[Zarządzanie kosztami](#tab/ManageCost)

Ocena środowiska jest doskonałą okazją do uwzględnienia etapu analizy kosztów. Dzięki danym zbieranym w trakcie oceny uzyskujesz możliwość analizowania i przewidywania kosztów. Ta funkcja przewidywania kosztów powinna polegać na tym, że koszty korzystania z usługi są rozliczane w ramach kosztów jednorazowych (takich jak zwiększony ruch przychodzący).

Podczas migracji następujące czynniki wpływają na decyzje i działania związane z realizacją:

- **Wielkość majątku cyfrowego:** Interpretacja wielkości majątku cyfrowego będzie miała bezpośredni wpływ na decyzje i zasoby wymagane do przeprowadzenia migracji.
- **Modele księgowania:** Zmiana ustrukturyzowanego modelu wydatków kapitałowych na płynny model kosztów operacyjnych.

::: zone target="docs"

Następujące zasoby zawierają informacje pokrewne:

- [Szacowanie kosztów chmury](../migration-considerations/assess/estimate.md)

::: zone-end
