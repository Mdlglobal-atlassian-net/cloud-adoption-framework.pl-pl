---
title: Decyzje, które mają wpływ na migrację
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby podejmować odpowiednie decyzje i wybrać działania wykonywania, które będą obsługiwać pomyślne Migrowanie.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: dd818e65e6f9064119b27dfb5ea87b8a04bda671
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83222134"
---
<!-- cSpell:ignore migrateable -->

# <a name="decisions-that-affect-migration"></a>Decyzje, które mają wpływ na migrację

Podczas migracji występuje kilka czynników wpływających na decyzje i działania związane z realizacją. W tym artykule wyjaśniono główną motywację tych decyzji i przedstawiono kilka pytań dotyczących zasad migracji w tej sekcji wskazówek dotyczących struktury wdrażania chmury.

## <a name="business-outcomes"></a>Wyniki biznesowe

Cel każdego procesu wdrożenia może mieć znaczny wpływ na sugerowane podejście do jego wykonania.

- **Migracji.** Pilne czynniki biznesowe, szybkość wdrażania lub oszczędności kosztów to przykłady wyników operacyjnych. Te wyniki mają kluczowe znaczenie dla wysiłków, które przekształcają przejściowe zmiany w infrastrukturze IT lub modelach operacyjnych w wartość biznesową. Sekcja Migracja struktury wdrażania chmury skupia się w dużym stopniu na wynikach biznesowych związanych z migracją.
- **Innowacje aplikacji.** Poprawa jakości obsługi klienta oraz rosnący udział w rynku to przykłady wyników przyrostowych. Te wyniki są skutkiem kolekcji zmian przyrostowych ukierunkowanych na potrzeby i wymagania bieżących klientów.
- **Innowacje bazujące na danych.** Nowe produkty i usługi, szczególnie te, które pochodzą z mocy danych, są przykładami nieprzerwanych rezultatów. Te wyniki są skutkiem eksperymentów i prognoz z wykorzystaniem danych w celu zakłócenia status quo na rynku.

Każda firma chce uzyskiwać wiele takich wyników. Bez działań nie ma klientów i odwrotnie. Wdrażanie chmury nie różni się pod tym względem. Firmy często pracują nad osiągnięciem każdego z tych wyników, ale próbują skupić się na wszystkich jednocześnie, co powoduje zbytnie rozproszenie wysiłków i spowalnia postęp prac, które mogą być najbardziej korzystne dla firmy.

To wymaganie wstępne nie jest zaleceniem, aby wybrać jeden z tych trzech celów, a jedynie ma na celu ułatwienie zespołowi strategicznemu ds. chmury i zespołowi wdrożeniowemu ds. chmury określenie zestawu priorytetów operacyjnych, którymi należy kierować się podczas wykonywania migracji w ciągu następnych trzech do sześciu miesięcy. Te priorytety należy określić przez uporządkowanie tych opcji w kolejności od _najważniejszej_ do _najmniej ważnej_ w odniesieniu do nakładu pracy, który ten zespół może wykonać w ciągu następnego kwartału lub dwóch.

### <a name="act-on-migration-outcomes"></a>Działania dotyczące wyników migracji

Jeśli wyniki operacyjne są najwyższej rangi na liście, ta sekcja struktury wdrażania w chmurze będzie odpowiadała Twojemu zespołowi. W tej sekcji założono, że konieczna jest priorytetyzacja szybkości i oszczędności kosztów jako kluczowych wskaźników wydajności (KPI), co sprawia, że model migracji do wdrożenia jest zgodny z wynikami. Model skoncentrowany na migracji jest silnie predykatowo związany z przenoszeniem i przenoszeniem zasobów infrastruktury jako usługi (IaaS) w celu wyczerpywania centrum danych i tworzenia oszczędności kosztów. W takim modelu może mieć miejsce modernizacja, ale jest ona drugorzędnym celem, dopóki nie zostanie zrealizowana główna misja migracji.

### <a name="act-on-application-innovations"></a>Działaj na innowacje aplikacji

Jeśli Twoje podstawowe sterowniki są udostępniane na udziale w rynku i w środowisku klienta, ta sekcja nie może być najlepszą częścią struktury wdrażania chmury, aby przekierować wysiłki zespołu. Innowacje dotyczące aplikacji wymagają planu skoncentrowanego na modernizacji i przeniesieniu obciążeń, niezależnie od podstawowej infrastruktury. W takim przypadku wskazówki zawarte w tej sekcji mogą zawierać istotne informacje, ale mogą nie być najlepszym podejściem do podejmowania kluczowych decyzji.

### <a name="act-on-data-innovations"></a>Działaj na innowacje dotyczące danych

Jeśli dane, eksperymentowanie, badania i programowanie (R&D) lub nowe produkty są priorytetem w ciągu następnych sześciu miesięcy lub w ten sposób, ta sekcja nie może być najlepszą częścią struktury wdrażania w chmurze, aby przekierować wysiłki zespołu. W przypadku wszelkich wysiłków związanych z innowacjami dotyczącymi danych warto skorzystać ze wskazówek dotyczących migracji istniejących danych źródłowych. Jednak wysiłki powinny być skupione w szerszym zakresie na ruchu przychodzącym i integracji dodatkowych źródeł danych. Rozszerzenie tych wskazówek o prognozy i nowe środowiska jest znacznie ważniejsze niż migracja zasobów IaaS.

## <a name="effort"></a>Nakład pracy

Nakład pracy związany z migracją może się znacznie różnić w zależności od rozmiaru i złożoności obciążeń. Migracja mniejszych obciążeń obejmująca kilkaset maszyn wirtualnych jest procesem taktycznym, który można zaimplementować przy użyciu zautomatyzowanych narzędzi, takich jak usługa [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview). Z kolei migracja dużego przedsiębiorstwa obejmująca setki tysięcy obciążeń wymaga wysoce strategicznego procesu i może być związana z szeroko zakrojoną refaktoryzacją, przebudową i zastępowaniem istniejących aplikacji integrujących możliwości platformy jako usługi (PaaS) oraz oprogramowania jako usługi (SaaS). [Identyfikacja i zrównoważenie zakresu](../../../strategy/balance-the-portfolio.md) planowanych migracji ma krytyczne znaczenie.

Przed podjęciem jakichkolwiek decyzji, które mogą mieć długoterminowy wpływ na bieżący program migracji, należy koniecznie osiągnąć porozumienie dotyczące następujących decyzji.

### <a name="effort-type"></a>Typ nakładu pracy

W przypadku każdej migracji znaczącej skali (więcej niż 250 maszyn wirtualnych) zasoby są migrowane przy użyciu różnych opcji przejścia, które zostały omówione w pięciu rozwiązaniach: ponowne _hostowanie_, _Refaktoryzacja_ _,_ _rekonstrukcja_, ponowna kompilacja i _zastąpienie_.

Niektóre obciążenia są modernizowane w ramach procesu _przebudowy_ lub _zmiany architektury_, co umożliwia utworzenie nowocześniejszych aplikacji z nowymi funkcjami i możliwościami technicznymi. Inne zasoby przechodzą przez proces _refaktoryzacji_ , na przykład przechodzenie do kontenerów lub inne bardziej nowoczesne metody hostingu i działania, które nie muszą mieć wpływu na bazę kodu rozwiązań. Często maszyny wirtualne i inne zasoby, które są bardziej dobrze ustanowione, przechodzą przez proces ponownego _hostowania_ , przenosząc te zasoby z centrum danych do chmury. Niektóre obciążenia można migrować do chmury, ale zamiast tego należy je _zastąpić_ przy użyciu usług w chmurze opartych na usługach (SaaS), które spełniają te same potrzeby biznesowe &mdash; , na przykład korzystając z pakietu Office 365 jako alternatywy do migrowania wystąpień programu Exchange Server.

W większości scenariuszy pewne zdarzenie biznesowe wymusza tymczasową migrację zasobów w ramach procesu _ponownego hostowania_, po którym następuje bardziej istotne dodatkowe przejście z zastosowaniem jednej z innych strategii migracji po przeniesieniu do chmury. Ten proces jest często nazywany _przeniesieniem do chmury_.

Podczas procesu [racjonalizacji majątku cyfrowego](../../../digital-estate/calculate.md) te typy decyzji są stosowane do każdego zasobu przeznaczonego do migracji. Jednak wymaganiem wstępnym na tym etapie jest przyjęcie założenia bazowego. Która z tych pięciu strategii migracji jest najbardziej zgodna z celami biznesowymi lub wynikam biznesowymi tego wysiłku związanego z migracją? Ta decyzja stanowi założenie przewodnie podczas całej migracji.

### <a name="effort-scale"></a>Skala nakładu pracy

Skala migracji to kolejna ważna decyzja należąca do wymagań wstępnych. Procesy wymagane do migrowania zasobów 1 000 różnią się od procesów wymaganych do przenoszenia zasobów 10 000. Przed rozpoczęciem jakiejkolwiek migracji należy odpowiedzieć na następujące pytania:

- **Ile zasobów obsługują obecnie migrowane obciążenia?** Zasoby obejmują struktury danych, aplikacje, maszyny wirtualne i niezbędne urządzenia IT. Zalecamy wybranie stosunkowo małego obciążenia jako pierwszego kandydata do migracji.
- **Ile z tych zasobów obejmuje plan migracji?** Często działanie pewnej części zasobów zostaje zakończone w ramach procesu migracji, z powodu braku stałej zależności użytkowników końcowych.
- **Jakie są szacowane szacunkowe skalowanie zasobów?** W przypadku obciążeń przeznaczonych do migracji należy oszacować liczbę zasobów pomocniczych, takich jak aplikacje, maszyny wirtualne, źródła danych i urządzenia IT. Zapoznaj się z sekcją dotyczącą [majątku cyfrowego](../../../digital-estate/index.md) w strukturze wdrażania chmury, aby uzyskać wskazówki dotyczące identyfikowania odpowiednich zasobów.

### <a name="effort-timing"></a>Harmonogram prac

Często migracje są spowodowane ważnym zdarzeniem biznesowym, które jest zależne od czasu. Na przykład częstą motywacją jest zakończenie lub odnowienie kontraktu hostingu innej firmy. Chociaż istnieje wiele potencjalnych zdarzeń, które wymagają migracji, współużytkują wspólny czynnik: datę końcową. Ważne jest zrozumienie harmonogramu zdarzeń biznesowych, aby móc prawidłowo planować i weryfikować działania.

## <a name="recap"></a>Podsumowanie

Przed kontynuowaniem należy udokumentować następujące założenia i udostępnić je zespołowi strategicznemu ds. chmury i zespołom wdrożeniowym ds. chmury:

- wyniki biznesowe,
- Role, udokumentowane i ulepszone do _oceny_, _migracji_, _optymalizacji_i _zabezpieczania procesów migracji oraz zarządzania nimi_ .
- Definicje gotowych, udokumentowanych i rafinowanych w celu _oceny_, _migracji_, _optymalizacji_i _zabezpieczania procesów migracji oraz zarządzania nimi_ .
- Typ nakładu pracy
- Skala nakładu pracy
- Harmonogram prac

## <a name="next-steps"></a>Następne kroki

Po zrozumieniu tego procesu wśród zespołu czasu na zapoznanie się z wymaganiami technicznymi. [Lista kontrolna planowania migracji](./planning-checklist.md) pomaga zapewnić gotowość podstawowych elementów technicznych do migracji.

Po zrozumieniu tego procesu wśród zespołu, jego czasu na zapoznanie się z wymaganiami technicznymi [Lista kontrolna planowania migracji](./planning-checklist.md) pomoże zapewnić, że platforma techniczna jest gotowa do migracji.

> [!div class="nextstepaction"]
> [Zapoznaj się z listą kontrolną planowania migracji](./planning-checklist.md)
