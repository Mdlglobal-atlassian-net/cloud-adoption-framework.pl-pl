---
title: Podejścia do planowania majątku cyfrowego
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej o różnych podejściach do planowania w formie elektronicznej.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 6a9d82e0211b36a2d34b54deca50227a62d7298e
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753126"
---
# <a name="approaches-to-digital-estate-planning"></a>Podejścia do planowania majątku cyfrowego

Planowanie elementów cyfrowych może potrwać kilka form, w zależności od potrzebnych wyników i rozmiaru istniejącej nieruchomości. Istnieją różne metody, które można wykonać. Ważne jest, aby ustawić oczekiwania dotyczące podejścia wczesnego do planowania cykli. Niejasne oczekiwania często prowadzą do opóźnień związanych z dodatkowymi ćwiczeniami zbierającymi spis. W tym artykule przedstawiono trzy podejścia do analizy.

## <a name="workload-driven-approach"></a>Podejście oparte na obciążeniu

Podejście do oceny w górnej części ocenia aspekty zabezpieczeń. Zabezpieczenia obejmują kategoryzację danych (wysoki, średni lub niski wpływ na działalność), wymagania dotyczące zgodności, suwerenności i bezpieczeństwa. Takie podejście ocenia złożoność architektury wysokiego poziomu. Oceniane są takie aspekty, jak uwierzytelnianie, struktura danych, wymagania dotyczące opóźnień, zależności i stron życia aplikacji.

Podejście do góry mierzy także wymagania operacyjne aplikacji, takie jak poziomy usług, integracja, okna obsługi, monitorowanie i wgląd w szczegółowe dane. Gdy wszystkie te aspekty zostały przeanalizowane i wzięte pod uwagę, wynikowy wynik związany z migracją tej aplikacji do poszczególnych platform w chmurze: IaaS, PaaS i SaaS.

Ponadto Ocena z góry ocenia korzyści finansowe aplikacji, takie jak efektywność operacyjna, całkowity koszt posiadania, zwrot z inwestycji i inne odpowiednie metryki finansowe. Ocena sprawdza także sezonowości aplikacji (na przykład czy istnieją czasy, w których są tworzone żądania?) i ogólne obciążenie obliczeniowe.

Sprawdza również obsługiwane typy użytkowników (niezależny/ekspert, zawsze/okazjonalnie zalogowany) oraz wymaganą skalowalność i elastyczność. Na koniec Ocena ma na celu zbadanie wymagań dotyczących ciągłości działalności biznesowej i odporności, a także zależności dotyczących uruchamiania aplikacji w przypadku wystąpienia zakłóceń usługi.

> [!TIP]
> Takie podejście wymaga wywiadów i anecdotal opinii od uczestników biznesowych i technicznych. Dostępność kluczowych użytkowników stanowi największe ryzyko dla chronometrażu. Anecdotal charakter źródeł danych utrudnia generowanie dokładnego kosztu lub oszacowania czasu. Planuj z wyprzedzeniem harmonogramy i sprawdzaj poprawność zbieranych danych.

## <a name="asset-driven-approach"></a>Podejście oparte na zasobach

Podejście oparte na zasobach zapewnia plan oparty na zasobach, które obsługują aplikację do migracji. W tym podejściu dane statystyczne użycia są ściągane z bazy danych zarządzania konfiguracją (CMDB) lub innych narzędzi do oceny infrastruktury.

Takie podejście zwykle zakłada model wdrożenia IaaS jako linię bazową. W tym procesie analiza szacuje atrybuty każdego elementu zawartości: pamięć, liczba procesorów (rdzenie procesora CPU), miejsce do magazynowania systemu operacyjnego, dyski danych, karty sieciowe (nic), protokół IPv6, równoważenie obciążenia sieciowego, klastrowanie, wersja systemu operacyjnego. wersja bazy danych (w razie potrzeby), obsługiwane domeny i składniki innych firm lub pakiety oprogramowania, między innymi. Zasoby, które są spisem w tym podejściu, są następnie wyrównane z obciążeniami lub aplikacjami dla celów grupowania i mapowania zależności.

> [!TIP]
> To podejście wymaga bogatego źródła danych statystycznych użycia. Czas wymagany do skanowania spisu i zbierania danych to największe ryzyko dla chronometrażu. Źródła danych niskiego poziomu mogą pominąć zależności między zasobami lub aplikacjami. Zaplanuj co najmniej jeden miesiąc, aby skanować spis. Sprawdź poprawność zależności przed wdrożeniem.

## <a name="incremental-approach"></a>Podejście przyrostowe

Zdecydowanie sugerujemy podejście przyrostowe, tak jak w przypadku wielu procesów w strukturze wdrożenia chmury. W przypadku planowania typu cyfrowego, które jest równe procesowi Multiphase:

- **Początkowa analiza kosztów:** Jeśli wymagana jest weryfikacja finansowa, należy zacząć od metody opartej na zasobach, opisanej wcześniej, aby uzyskać początkowe obliczenie kosztów dla całej cyfrowej, bez racjonalizacji. Stanowi to wynik testu porównawczego dla najgorszego przypadku.

- **Planowanie migracji:** Po złożeniu zespołu strategii chmurowej Utwórz początkową zaległości migracji przy użyciu opartego na obciążeniu podejścia opartego na ich zbiorowej wiedzy i ograniczonej wywiadów z pracownikami. Takie podejście szybko tworzy uproszczoną ocenę obciążenia, aby sprzyjać współpracy.

- **Planowanie wydania:** W każdej wersji dziennik zaległości migracji zostaje oczyszczony i podlega zmianie priorytetów, aby skoncentrować się na najbardziej odpowiednim wpływie na działalność biznesową. W trakcie tego procesu kolejne pięć do dziesięciu obciążeń są wybierane jako wydania z priorytetami. W tym momencie zespół strategii chmury zainwestował czas wykonywania wyczerpujących rozwiązań opartych na obciążeniu. Opóźnienie tej oceny do momentu, aż wydanie zostanie wyrównane lepiej, nie będzie uwzględniać czasu uczestników projektu. Ponadto opóźnia inwestycję w pełną analizę do momentu, gdy firma zacznie zobaczyć wyniki z wcześniejszych wysiłków.

- **Analiza wykonywania:** Przed przeprowadzeniem migracji, modernizacji lub replikowania dowolnego elementu zawartości należy ocenić go zarówno indywidualnie, jak i w ramach zbiorczego wydania. W tym momencie dane z podejścia początkowej klasy zasobów można scrutinized, aby zapewnić dokładne określanie rozmiarów i ograniczeń operacyjnych.

> [!TIP]
> Takie przyrostowe podejście umożliwia usprawnione planowanie i przyspieszone wyniki. Ważne jest, aby wszystkie strony miały świadomość podejścia do opóźnionej podejmowania decyzji. Jest to równie ważne, aby założenia wprowadzone na każdym etapie zostały udokumentowane w celu uniknięcia utraty szczegółowych informacji.

## <a name="next-steps"></a>Następne kroki

Po wybraniu podejścia można zebrać spis.

> [!div class="nextstepaction"]
> [Zbierz dane spisu](./inventory.md)
