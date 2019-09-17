---
title: Jak można wyrównać wysiłki na rzecz istotnych metryk uczenia?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie koncepcji metryk uczenia
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: f761f85fa4b21b35e8428985707176624b92a5ec
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026633"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-can-we-align-efforts-to-meaningful-learning-metrics"></a>Jak można wyrównać wysiłki na rzecz istotnych metryk uczenia?

[Przegląd wyników firmy](./business-outcomes/index.md) omawiane sposoby mierzenia i przekazywania wpływu transformacji na działalność biznesową. Niestety, aby niektóre z tych wyników mogły dawać wymierne wyniki, może upłynąć kilka lat. Na tablicach i w języku C są nieszczęśliwe raporty, które pokazują różnicę 0% przez długi czas.

Metryki uczenia są tymczasowymi, krótszymi metrykami, które mogą być powiązane z dłuższymi wynikami biznesowymi. Te metryki są wyrównane z sposób myśleniaem wzrostu i umożliwiają umieszczenie kultury w celu zwiększenia odporności. Zamiast wyróżniania przewidywanego braku postępu w kierunku długoterminowego celu biznesowego, metryki szkoleniowe wyróżnią wczesne wskaźniki sukcesu. Metryki również wyróżnią wczesne wskaźniki niepowodzeń, co może dawać największą szansę na naukę i dostosowanie planu.

Tak jak w przypadku większości materiału w tej strukturze założono, że znasz już [drogę transformacji](../govern/guides/index.md) , która najlepiej odpowiada Twoim potrzebom biznesowym. W tym artykule przedstawiono kilka metryk uczenia dla każdej przekształcenia transformacji w celu zilustrowania koncepcji.

## <a name="cloud-migration"></a>Migracja do chmury

Ta transformacja koncentruje się na kosztach, złożoności i wydajności, z uwzględnieniem operacji IT. Najłatwiej mierzone dane związane z tym przekształcaniem to przenoszenie zasobów do chmury. W tym rodzaju transformacji cyfra cyfrowa jest mierzona przez maszyny wirtualne, stojaki lub Klastry obsługujące te maszyny wirtualne, koszty operacyjne centrum danych, wymagane wydatki inwestycyjne w celu utrzymywania systemów i amortyzację tych zasobów w miarę upływu czasu.

Ponieważ maszyny wirtualne są przenoszone do chmury, zależność od lokalnych starszych zasobów jest ograniczona. Koszt konserwacji zasobów jest również zmniejszany. Niestety firmy nie mogą korzystać z obniżki kosztów, dopóki nie zostaną anulowane aprowizacji klastrów i dzierżawy centrum danych wygaśnie. W wielu przypadkach pełna wartość nakładu pracy nie jest realizowana do momentu ukończenia cykli amortyzacji.

Przed rozpoczęciem sporządzania sprawozdań finansowych zawsze Wyrównaj się do DYREKTORa finansowego lub finansów. Jednakże zespoły IT mogą generalnie oszacować bieżące koszty pieniężne i przyszłe wartości pieniężne dla każdej maszyny wirtualnej na podstawie zużycia procesora CPU, pamięci i magazynu. Następnie można zastosować tę wartość do każdej zmigrowanej maszyny wirtualnej w celu oszacowania natychmiastowego oszczędności kosztów i przyszłej wartości pieniężnej nakładu pracy.

## <a name="application-innovation"></a>Innowacje aplikacji

Innowacyjne aplikacje obsługujące chmurę koncentrują się na doświadczeniu klienta oraz gotowości klienta do korzystania z produktów i usług oferowanych przez firmę. Jest to czasochłonne, aby zwiększyć liczbę zmian, które mają wpływ na zachowania klienta lub zakupu. Jednak cykle innowacji aplikacji są znacznie krótsze niż w innych formach transformacji. Tradycyjną wskazówką jest rozpoczęcie od zrozumienie określonych zachowań, które mają wpływ na te zachowania, oraz ich użycie jako metryki szkoleniowej. Na przykład w aplikacji handlu elektronicznego łączne zakupy lub zakup dodatków mogą być zachowaniem docelowym. W przypadku firmowego wideo strumienie wideo w czasie, które mogą być miejscem docelowym.

Metryki związane z zachowaniem klienta polega na tym, że można z łatwością mieć wpływ na zmienne zewnętrzne. Często ważne jest, aby uwzględnić powiązane dane statystyczne z metrykami uczenia. Te powiązane dane statystyczne mogą obejmować erze wydania, błędy rozwiązane według wydania, pokrycie kodu testów jednostkowych, liczbę wyświetleń stron, przepływność stron, czas ładowania strony i inne metryki wydajności aplikacji. Każdy z nich może przedstawiać różne działania i zmiany w bazie kodu oraz środowisko klienta w celu skorelowania wzorców zachowania klienta wyższego poziomu.

## <a name="data-innovation"></a>Innowacje dotyczące danych

Zmiana branży, zakłócenie rynków lub przekształcanie produktów/usług może potrwać lata. Eksperymentowanie danych z obsługą chmury jest kluczem do mierzenia sukcesu. Być przezroczyste przez udostępnienie metryk prognoz, takich jak prawdopodobieństwo procentu, liczba eksperymentów zakończonych niepowodzeniem i ilość przeszkolonych modeli. Błędy będą gromadzone szybciej niż sukcesy. Te metryki mogą być discouraging i ważne jest, aby zespół wykonawczy rozumieł czas i inwestycje potrzebne do poprawnego wykorzystania danych.

Z drugiej strony, niektóre wskaźniki pozytywne są często powiązane z uczeniem opartym na danych: scentralizowanie zestawów danych heterogenicznych, danych wejściowych i Democratization danych. Gdy zespół uczy się od klienta jutro, rzeczywiste wyniki mogą być tworzone dzisiaj. Dodatkowe metryki dotyczące uczenia mogą obejmować:

- Liczba dostępnych modeli
- Liczba użytych źródeł danych partnera
- Urządzenia wytwarzające dane wejściowe
- Ilość danych przychodzących
- Typy danych

Jeszcze bardziej cenna Metryka to liczba pulpitów nawigacyjnych utworzonych na podstawie połączonych źródeł danych. Ta liczba odzwierciedla bieżące procesy biznesowe, na które mają wpływ nowe źródła danych. Udostępniając nowe źródła danych otwarte, firma może korzystać z danych za pomocą narzędzi do raportowania, takich jak Power BI, aby tworzyć przyrostowe szczegółowe informacje i prowadzić zmiany w firmie.

## <a name="next-steps"></a>Następne kroki

Gdy metryki szkoleniowe są wyrównane, możesz rozpocząć [ocenianie cyfr cyfrowych](../digital-estate/index.md) przed tymi metrykami. Wynikiem będzie [zaległości transformacji lub zaległości migracji](../migrate/migration-considerations/prerequisites/technical-complexity.md).

> [!div class="nextstepaction"]
> [Ocenianie cyfrowego podpisywania](../digital-estate/index.md)
