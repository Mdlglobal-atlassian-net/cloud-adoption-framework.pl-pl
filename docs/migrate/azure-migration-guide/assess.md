---
title: Szacowanie majątku cyfrowego
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Szacowanie majątku cyfrowego
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: a2acba3f9aa06298922d2cc95d298d3792a9ada9
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240011"
---
# <a name="assess-the-digital-estate"></a>Szacowanie majątku cyfrowego

W idealnej migracji każdy zasób (infrastruktury, aplikacji lub danych) jest zgodny z platformą w chmurze oraz gotowy do migracji. W rzeczywistości nie wszystkie elementy można zmigrować do chmury. Ponadto nie każdy zasób jest zgodny z platformami w chmurze. Przed przeprowadzeniem migracji obciążenia do chmury ważne jest, aby ocenić obciążenie i każdy powiązany z nim zasób (infrastrukturę, aplikacje i dane).

Zasoby w tej sekcji ułatwią ocenę środowiska i określenie jego przydatności do migracji oraz metod, które należy wziąć pod uwagę.

<!-- markdownlint-disable MD025 -->

# <a name="toolstabtools"></a>[Narzędzia](#tab/Tools)

Poniższe narzędzia ułatwiają ocenę środowiska, określenie jego przydatności do migracji i najlepszego podejścia do wykorzystania. Aby uzyskać przydatne informacje na temat doboru odpowiednich narzędzi do obsługi zadań związanych z migracją, zobacz [Przewodnik doboru narzędzi migracji platformy wdrażania w chmurze](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Usługa Azure Migrate ocenia lokalną infrastrukturę, aplikacje i dane pod kątem migracji na platformę Azure. Obejmuje to ocenę gotowości zasobów lokalnych do migracji, określenie rozmiaru odpowiedniego do wydajności oraz oszacowanie kosztów uruchamiania zasobów lokalnych na platformie Azure. Ta usługa jest przeznaczona dla osób, które zamierzają przeprowadzić migrację metodą „lift-and-shift” lub dopiero zaczęły oceniać możliwość migracji. Po zakończeniu oceny usługę Azure Migrate można wykorzystać do wykonania migracji.

![Azure Migrate — przegląd](./media/assess/azuremigrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Tworzenie nowego projektu migracji serwera

Aby rozpocząć ocenę migracji serwera przy użyciu usługi Azure Migrate, wykonaj następujące kroki:

1. Wybierz opcję **Azure Migrate**.
1. W obszarze **Przegląd** kliknij pozycję **Ocena i migracja serwerów**.
1. Wybierz pozycję **Dodaj narzędzia**.
1. W obszarze **Odnajdywanie, ocena i migracja serwerów** kliknij pozycję **Dodaj narzędzia**.
1. W obszarze **Projekt migracji**wybierz subskrypcję platformy Azure i utwórz grupę zasobów, jeśli jej nie masz.
1. W obszarze **Szczegóły projektu** określ nazwę projektu i lokalizację geograficzną, w której chcesz utworzyć projekt, a następnie kliknij przycisk **Dalej**.
1. W obszarze **Wybierz narzędzie oceny**, wybierz pozycję **Pomiń teraz dodawanie narzędzia oceny > Dalej**.
1. W obszarze **Wybierz narzędzie migracji** wybierz pozycję **Azure Migrate: Server Migration > Dalej**.
1. W obszarze **Przegląd i dodawanie narzędzi** przejrzyj ustawienia, a następnie kliknij pozycję **Dodaj narzędzia**
1. Po dodaniu narzędzia pojawia się ono w obszarze **Projekt usługi Azure Migrate > Serwery > Narzędzia migracji**.

::: zone target="chromeless"

::: form action="Blade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Migrate — przegląd](https://docs.microsoft.com/azure/migrate/migrate-services-overview)
- [Migrowanie serwerów fizycznych lub zwirtualizowanych na platformę Azure](https://docs.microsoft.com/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Usługa Azure Migrate w witrynie Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview)

::: zone-end

## <a name="service-map"></a>Mapa usługi

Mapa usługi automatycznie odnajduje składniki aplikacji w systemach Windows i Linux oraz mapuje komunikację między usługami. Dzięki usłudze Service Map można wyświetlać serwery w sposób, w jakich się o nich myśli: jako wzajemnie połączone systemy dostarczające usługi. Usługa Service Map pokazuje połączenia między serwerami i procesami, opóźnienie połączeń przychodzących i wychodzących oraz porty dla każdej architektury połączonej za pomocą protokołu TCP. Nie jest wymagana żadna konfiguracja, wystarczy zainstalować agenta.

Usługi Azure Migrate korzystają z usługi Service Map, aby zwiększyć możliwości raportowania i zależności w środowisku. Wszystkie szczegóły tej integracji zostały opisane w [wizualizacji zależności](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization). W przypadku korzystania z usługi Azure Migration Service nie ma dodatkowych kroków wymaganych do skonfigurowania i korzystania z usługi Service Map. Poniższe instrukcje udostępniono w celach informacyjnych użytkownikom, którzy chcą używać usługi Service Map do innych celów lub projektów.

### <a name="enable-dependency-visualization-using-service-map"></a>Włączanie wizualizacji zależności przy użyciu usługi Service Map

Aby można było używać wizualizacji zależności, należy pobrać i zainstalować agenty na każdej maszynie lokalnej, która ma zostać przeanalizowana.

- [Program Microsoft Monitoring Agent (MMA) ](https://docs.microsoft.com/azure/log-analytics/log-analytics-agent-windows) musi być zainstalowany na każdej maszynie.
- [Agent zależności firmy Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) musi być zainstalowany na każdej maszynie.
- Ponadto w przypadku maszyn, które nie są połączone z Internetem, należy pobrać i zainstalować na nich bramę usługi Log Analytics.

<!-- markdownlint-disable MD024 -->

### <a name="learn-more"></a>Dowiedz się więcej

- [Korzystanie z rozwiązania Service Map na platformie Azure](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)
- [Azure Migrate i Service Map: wizualizacja zależności](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization)

# <a name="scenarios-and-stakeholderstabscenarios"></a>[Scenariusze i osoby biorące udział w projekcie](#tab/Scenarios)

## <a name="scenarios"></a>Scenariusze

Ten przewodnik zawiera informacje o następujących scenariuszach:

- **Starszy sprzęt:** Przeprowadzasz migrację, aby uniezależnić się od starszego sprzętu, dla którego zbliża się koniec okresu obowiązywania pomocy technicznej lub dostępności sprzętu.
- **Wzrost pojemności:** Należy zwiększyć pojemność zasobów (infrastruktury, aplikacji i danych) do wielkości, której nie jest w stanie zapewnić bieżąca infrastruktura.
- **Modernizacja centrum danych:** Należy powiększyć lub zmodernizować centrum danych w technologii chmury, aby zapewnić nowoczesność i konkurencyjność firmy.
- **Modernizacja aplikacji lub usługi:** Chcesz zaktualizować swoje aplikacje, aby korzystać z funkcji natywnych w chmurze. Nawet jeśli strategia migracji ponownego hostowania jest celem wstępnym, możliwość tworzenia planów przeglądu aplikacji lub usług oraz potencjalnej modernizacji jest typowym procesem w każdej migracji.

### <a name="organizational-alignment-and-stakeholders"></a>Zgodność organizacyjna i osoby biorące udział w projekcie

Pełna lista osób biorących udział w projekcie zależy od konkretnego projektu migracji. Najlepszym rozwiązaniem jest założenie, że na początku planowania migracji nie będą znane wszystkie osoby biorące udział w projekcie, ponieważ osoby te są często identyfikowane tylko podczas niektórych faz projektu. Jednak przed rozpoczęciem dowolnego projektu migracji można zidentyfikować najważniejszych liderów firmy z zakresu finansów, infrastruktury IT oraz grup ds. zastosowań, zainteresowanych ogólnymi działaniami w zakresie migracji do chmury.

Utworzenie podstawowego zespołu ds. strategii w chmurze, opartego na najważniejszych osobach biorących udział w projekcie, może pomóc w przygotowaniu organizacji do wdrożenia w chmurze i przeprowadzeniu ogólnych działań związanych z migracją w chmurze. Ten zespół jest odpowiedzialny za interpretację technologii chmurowych i procesów migracji, uzasadnienie biznesowe migracji oraz określenie najlepszych rozwiązań wysokiego poziomu na potrzeby migracji. Członkowie zespołu ułatwiają również identyfikację konkretnych osób biorących udział w projekcie z ramienia grup ds. zastosowań i firmy w celu zapewnienia pomyślnej migracji oraz współpracę z nimi.

Aby uzyskać więcej informacji na temat przygotowywania organizacji do działań związanych z migracją do chmury, zobacz artykuł dotyczący struktury wdrażania w chmurze na temat [wstępnej zgodności organizacyjnej](../../plan/initial-org-alignment.md).

# <a name="timelinestabtimelines"></a>[Harmonogram](#tab/Timelines)

Zgodnie z ogólną zasadą, klienci mogą założyć, że scenariusz migracji opisany w tym przewodniku można zrealizować w ciągu od jednego do sześciu miesięcy.

Oto kilka czynników, które należy wziąć pod uwagę podczas szacowania harmonogramu migracji:

- **Zasoby (infrastruktury, aplikacji i danych) do zmigrowania:** Liczba i różnorodność zasobów.
- **Gotowość personelu:** Czy pracownicy są przygotowani do zarządzania nowym środowiskiem, czy są potrzebne szkolenia?
- **Finansowanie:** Czy uzyskano odpowiednie zatwierdzenia i budżet do zrealizowania migracji?
- **Zarządzanie zmianami:** Czy firma ma określone wymagania dotyczące implementacji zmian i zatwierdzania?
- **Regulacje branżowe:** Czy konieczne jest przestrzeganie przepisów branżowych?

# <a name="cost-managementtabmanagecost"></a>[Zarządzanie kosztami](#tab/ManageCost)

Podczas oceniania środowiska jest to idealne rozwiązanie umożliwiające uwzględnienie kroku analizy kosztów. Dzięki danym zbieranym w trakcie przeprowadzania oceny uzyskujesz możliwość analizowania i przewidywania kosztów. Ta funkcja przewidywania kosztów powinna polegać na tym, że koszty korzystania z usługi są rozliczane w ramach kosztów jednorazowych (takich jak zwiększony ruch przychodzący).

Podczas migracji następujące czynniki wpływają na decyzje i działania związane z realizacją:

- **Wielkość majątku cyfrowego:** Interpretacja wielkości majątku cyfrowego będzie miała bezpośredni wpływ na decyzje i zasoby wymagane do przeprowadzenia migracji.
- **Modele księgowania:** Zmiana ustrukturyzowanego modelu wydatków kapitałowych na płynny model kosztów operacyjnych.

::: zone target="docs"

Następujące zasoby zawierają informacje pokrewne:

- [Szacowanie kosztów chmury](../migration-considerations/assess/estimate.md)

::: zone-end
