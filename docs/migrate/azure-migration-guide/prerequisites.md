---
title: Wymagania wstępne dotyczące migracji na platformę Azure
description: Skorzystaj z podręcznika Cloud Adoption Framework dla platformy Azure, aby uzyskać informacje na temat przygotowania się do migracji na platformę Azure i wymagań wstępnych potrzebnych dla pomyślnego projektu migracji.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 777b68bcd7faa613681f2d9ebbdf6cffe4accc3f
ms.sourcegitcommit: 959cb0f63e4fe2d01fec2b820b8237e98599d14f
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/11/2020
ms.locfileid: "79094792"
---
::: zone target="chromeless"

# <a name="prerequisites"></a>Wymagania wstępne

::: zone-end

::: zone target="docs"

# <a name="prerequisites-for-migrating-to-azure"></a>Wymagania wstępne dotyczące migracji na platformę Azure

::: zone-end

Zasoby w tej sekcji ułatwią przygotowanie bieżącego środowiska do migracji na platformę Azure.

# <a name="overview"></a>[Omówienie](#tab/Overview)

Powody migracji na platformę Azure obejmują usuwanie zagrożeń związanych ze starszymi wersjami sprzętu, zmniejszanie wydatków inwestycyjnych, zwalnianie miejsca w centrum danych i szybkie uzyskiwanie zwrotów z inwestycji (ROI).

- **Eliminowanie starszego sprzętu.** Aplikacje mogą być hostowane w infrastrukturze, która zbliża się do końca okresu eksploatacji lub okresu świadczenia pomocy technicznej, zarówno w środowisku lokalnym, jak i u dostawcy hostingu. Migracja do chmury oferuje atrakcyjne rozwiązanie dotyczące tego wyzwania, ponieważ możliwość migracji „w stanie takim, w jakim jest” pozwala zespołowi szybko rozwiązać bieżące problemy związane z cyklem życia infrastruktury, a następnie skoncentrować się na długoterminowym planowaniu cyklu życia aplikacji i jej optymalizacji w chmurze.
- **Obsługa końca okresu świadczenia pomocy technicznej dla oprogramowania.** Aplikacje mogą być zależne od innych programów lub systemów operacyjnych, które zbliżają się do końca okresu świadczenia pomocy technicznej. Przejście na platformę Azure może zapewnić dodatkowe opcje pomocy technicznej dla tych zależności lub inne opcje migracji, które zminimalizują wymagania refaktoryzacji, w celu obsługi aplikacji w przyszłości. Na przykład zobacz temat dotyczący [dodatkowych opcji pomocy technicznej dla systemu Windows Server 2008 i programu SQL Server 2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support).
- **Zmniejszanie wydatków inwestycyjnych.** Hosting własnej infrastruktury serwerów wymaga znacznych inwestycji dotyczących sprzętu, oprogramowania, energii elektrycznej i personelu. Migrowanie do rozwiązania w chmurze może zapewnić znaczny spadek wydatków inwestycyjnych. W celu osiągnięcia największych redukcji wydatków inwestycyjnych być może trzeba będzie przeprojektować rozwiązanie. Migracja „w stanie takim, jakim jest” to jednak doskonały pierwszy krok.
- **Zwalnianie miejsca w centrum danych.** Platformę Azure można wybrać w celu zwiększenia pojemności centrum danych. Jednym ze sposobów osiągnięcia tego celu jest użycie chmury jako rozszerzenia możliwości środowiska lokalnego.
- **Szybkie realizowanie zwrotu z inwestycji.** Dzięki rozwiązaniom w chmurze osiąganie zwrotu z inwestycji (ROI) jest znacznie łatwiejsze, ponieważ model płatności w chmurze zapewnia doskonałe szczegółowe informacje dotyczące wykorzystania i promuje kulturę umożliwiającą realizację zwrotu z inwestycji.

Każdy z powyższych scenariuszy może być punktem wejścia do rozszerzania zasięgu chmury przy użyciu innej metodologii (ponowne hostowanie, refaktoryzacja, rekonstrukcja, przebudowanie lub zastąpienie).

## <a name="migration-characteristics"></a>Charakterystyka migracji

W tym przewodniku przyjęto założenie, że przed przeprowadzeniem migracji majątek cyfrowy obejmował głównie infrastrukturę hostowaną w środowisku lokalnym i mógł uwzględniać hostowane aplikacje o krytycznym znaczeniu dla firmy. Po pomyślnie zakończonej migracji dane mogą wyglądać bardzo podobnie do tego, jak wyglądały w środowisku lokalnym, ale z infrastrukturą hostowaną w zasobach w chmurze. Alternatywnie idealna struktura posiadanych danych będzie odmianą bieżącej struktury danych, ponieważ ma ona aspekty infrastruktury lokalnej ze składnikami, które zostały refaktoryzowane w celu optymalizacji platformy w chmurze i korzystania z jej zalet.

Ta podróż związana z migracją koncentruje się na osiągnięciu następujących celów:

- Rozwiązanie problemu końca eksploatacji starszego sprzętu.
- Zmniejszenie wydatków inwestycyjnych.
- Uzyskanie zwrotu z inwestycji.

> [!NOTE]
> Jeszcze jedną zaletą tej podróży obejmującej migrację jest dodatkowy model wsparcia oprogramowania dla systemów Windows 2008 i Windows 2008 R2 oraz programów SQL Server 2008 i SQL Server 2008 R2. Aby uzyskać więcej informacji, zobacz:
>
> - [Systemy Windows Server 2008 i Windows Server 2008 R2](https://www.microsoft.com/cloud-platform/windows-server-2008).
> - [Programy SQL Server 2008 i SQL Server 2008 R2](https://www.microsoft.com/sql-server/sql-server-2008).

# <a name="understand-migration-approaches"></a>[Omówienie podejść do migracji](#tab/Approach)

Wybór strategii i narzędzi używanych do migrowania aplikacji na platformę Azure w dużej mierze zależy od względów biznesowych, wymagań technologicznych i harmonogramów w Twojej firmie, a także od pełnego obrazu rzeczywistego obciążenia i zasobów (infrastruktury, aplikacji i danych), które są migrowane.

Przed określeniem strategii migracji do chmury należy przeanalizować aplikacje kandydackie, aby zidentyfikować ich zgodność z technologiami hostingu w chmurze. [Przewodnik po decyzjach dotyczących narzędzi migracji](../../decision-guides/migrate-decision-guide/index.md) w obrębie struktury wdrażania chmury ułatwi Ci rozpoczęcie pracy z tym procesem.

Migracja skoncentrowana na usłudze IaaS, w ramach której serwery (wraz ze skojarzonymi z nimi aplikacjami i danymi) są ponownie hostowane w chmurze przy użyciu maszyn wirtualnych, to często najprostsze podejście do przenoszenia obciążeń do chmury. Należy jednak pamiętać, że poprawne konfigurowanie, zabezpieczanie i konserwowanie maszyn wirtualnych może wymagać znacznie więcej czasu i doświadczenia w zakresie IT niż w przypadku usług PaaS na platformie Azure. Jeśli planujesz użycie usługi Azure Virtual Machines, uwzględnij przyszłe nakłady na konserwację wymagane do wdrażania poprawek i aktualizowania środowiska maszyn wirtualnych oraz zarządzania nim.

Podczas oceniania obciążeń związanych z migracją zidentyfikuj aplikacje, które do działania nie wymagają znaczących modyfikacji przeprowadzanych za pomocą technologii PaaS, takich jak usługa Azure App Service, lub orkiestratorów, takich jak usługa Azure Kubernetes Service. Te aplikacje powinny być pierwszymi kandydatami do modernizacji i optymalizacji chmury.

## <a name="learn-more"></a>Dowiedz się więcej

- [Przewodnik po decyzjach dotyczących narzędzi migracji w obrębie struktury wdrażania chmury](../../decision-guides/migrate-decision-guide/index.md)
- [5 zasad racjonalizacji](../../digital-estate/5-rs-of-rationalization.md)

# <a name="planning-checklist"></a>[Lista kontrolna dotycząca planowania](#tab/Checklist)

Przed rozpoczęciem migracji należy spełnić pewne wymagania wstępne. Szczegóły tych działań różnią się w zależności od migrowanego środowiska. Można zastosować następującą ogólną listę kontrolną:

> [!div class="checklist"]
>
> - **Identyfikowanie osób biorących udział w projekcie:** zidentyfikuj kluczowe osoby, które mają rolę do odegrania podczas migracji lub które będą stanowić część jej wyniku.
> - **Identyfikowanie kluczowych kamieni milowych:** aby efektywnie planować osie czasu migracji, zidentyfikuj kluczowe kamienie milowe do osiągnięcia.
> - **Identyfikowanie strategii migracji:** ustal, z których z 5 zasad racjonalizacji będziesz korzystać.
> - **Ocena dopasowania pod względem technicznym:** zweryfikuj gotowość techniczną i przydatność do migracji, a także określ poziom pomocy, której możesz wymagać od partnerów zewnętrznych lub działu pomocy technicznej platformy Azure.
> - **Planowanie migracji:** przeprowadź szczegółową ocenę i planowanie wymagane do przygotowania zasobów (infrastruktury, aplikacji i danych), a także infrastruktury platformy Azure do migracji.
> - **Testowanie migracji:** zweryfikuj plan migracji, wykonując migrację testową w ograniczonym zakresie.
> - **Migrowanie usług:** Wykonaj faktyczną migrację.
> - **Czynności po migracji:** zapoznaj się z informacjami o tym, co jest wymagane po przeprowadzeniu migracji środowiska na platformę Azure.

Jeśli wybierzesz podejście do migracji obejmujące ponowne hostowanie, istotne będzie również wykonanie następujących działań:

> [!div class="checklist"]
>
> - **Dostosowanie ładu:** czy osiągnięto porozumienie dotyczące dostosowania ładu do podstaw migracji?
> - **Sieć:** należy wybrać strategię sieci i dopasować ją do wymagań dotyczących zabezpieczeń infrastruktury IT.
> - **Tożsamość:** należy dopasować strategię tożsamości hybrydowych do planu zarządzania tożsamościami i wdrażania chmury.

::: zone target="docs"

<!-- markdownlint-disable MD024 -->

## <a name="learn-more"></a>Dowiedz się więcej

- [5 zasad racjonalizacji](../../digital-estate/5-rs-of-rationalization.md)
- [Przewodnik po decyzjach dotyczących narzędzi migracji](../../decision-guides/migrate-decision-guide/index.md)
- [Lista kontrolna dotycząca planowania w obrębie struktury wdrażania chmury](../migration-considerations/prerequisites/planning-checklist.md)

::: zone-end
