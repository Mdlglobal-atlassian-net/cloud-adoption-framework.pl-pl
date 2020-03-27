---
title: Definiowanie obciążeń i określanie priorytetów dla wdrażania w chmurze
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak definiować i określać priorytety obciążeń dla planu wdrożenia chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8d9297534f04b6656b584fa82d565e9119599f26
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80354694"
---
# <a name="define-and-prioritize-workloads-for-a-cloud-adoption-plan"></a>Definiowanie i ustalanie priorytetów obciążeń dla planu wdrażania chmury

Ustanowienie jasnych, priorytetowych priorytetów jest jednym z kluczy tajnych, aby pomyślnie zaakceptowanić chmurę. Naturalny Temptation polega na zainwestowaniu czasu w celu zdefiniowania wszystkich obciążeń, które mogą być narażone podczas wdrażania w chmurze. Ale to counterproductive, szczególnie wczesne w procesie wdrażania.

Zamiast tego zalecamy, aby zespół koncentruje się na dokładnej priorytetyzacji i udokumentowaniu pierwszych 10 obciążeń. Po rozpoczęciu wdrażania planu wdrażania zespół może zachować listę kolejnych 10 obciążeń o najwyższym priorytecie. To podejście zapewnia wystarczającą ilość informacji do zaplanowania dla następnych kilku iteracji.

Ograniczenie planu do 10 obciążeń zaleca elastyczność i wyrównanie priorytetów jako zmiany kryteriów firmy. Takie podejście sprawia również, że zespół rozwiązań w chmurze może uczyć się i udoskonalać oszacowania. Najważniejsze jest usunięcie obszernego planu jako bariery do efektywnej zmiany biznesowej.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-workload"></a>Co to jest obciążenie?

W kontekście wdrożenia chmury obciążenie to zbiór zasobów IT (serwerów, maszyn wirtualnych, aplikacji, danych lub urządzeń), które zbiorczo obsługują zdefiniowany proces. Obciążenia mogą obsługiwać więcej niż jeden proces. Obciążenia mogą również być zależne od innych zasobów udostępnionych lub większych platform. Jednak obciążenie powinno mieć zdefiniowane granice dotyczące zasobów zależnych i procesów, które są zależne od obciążenia. Często obciążenia mogą być wizualizowane przez monitorowanie ruchu sieciowego między zasobami IT.

## <a name="prerequisites"></a>Wymagania wstępne

Strategiczne dane wejściowe z listy wymagań wstępnych znacznie ułatwiają wykonywanie następujących zadań. Aby uzyskać pomoc dotyczącą zbierania danych opisanych w tym artykule, zapoznaj się z [wymaganiami wstępnymi](./prerequisites.md).

## <a name="initial-workload-prioritization"></a>Początkowa priorytetyzacja obciążeń

Podczas procesu [racjonalizacji przyrostowej](../digital-estate/rationalize.md)zespół powinien wyrazić zgodę na podejście "moc 10", które składa się z 10 obciążeń priorytetowych. Te obciążenia stanowią początkową granicę planowania wdrożenia.

W przypadku podjęcia decyzji o tym, że nie jest wymagana racjonalizacja dotyczącej typu cyfrowego, firma Microsoft zaleca, aby zespoły wdrożenia chmury i zespół strategii chmurowych zgadzali się na listę 10 aplikacji, które będą stanowić początkowy fokus migracji. Zalecamy dalsze, aby te 10 obciążeń zawierało kombinację prostych obciążeń (mniej niż 10 zasobów w ramach wdrożenia samodzielnego) i bardziej złożonych obciążeń. Te 10 obciążeń rozpocznie proces priorytetyzacji obciążenia.

> [!NOTE]
> Moc 10 służy jako początkowa granica planowania, aby skoncentrować energię i inwestycje w fazie wczesnego etapu analizy. Jednak czynność analizowania i definiowania obciążeń może spowodować zmiany na liście obciążeń priorytetowych.

## <a name="add-workloads-to-your-cloud-adoption-plan"></a>Dodawanie obciążeń do planu wdrażania chmury

W poprzednim artykule [Plan wdrażania chmury i Azure DevOps](./template.md)został utworzony plan wdrażania chmury w usłudze Azure DevOps.

Teraz można reprezentować obciążenia na mocy 10 list w planie wdrożenia chmury. Najprostszym sposobem na to jest przeprowadzenie edycji zbiorczej w programie Microsoft Excel. Aby przygotować stację roboczą do edycji zbiorczej, zobacz [zbiorcze Dodawanie lub modyfikowanie elementów roboczych za pomocą programu Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

Krok 5 w tym artykule informuje o wybraniu **listy danych wejściowych**. Zamiast tego wybierz pozycję **Lista zapytań**. Następnie na liście rozwijanej **Wybierz zapytanie** wybierz zapytanie **szablon obciążenia** . Ta kwerenda ładuje wszystkie działania związane z migracją pojedynczego obciążenia do arkusza kalkulacyjnego.

Po załadowaniu elementów roboczych dla szablonu obciążenia wykonaj następujące kroki, aby rozpocząć dodawanie nowych obciążeń:

1. Skopiuj wszystkie elementy, które mają tag **szablonu obciążenia** , w skrajnej prawej kolumnie.
2. Wklej skopiowane wiersze poniżej ostatniego wiersza w tabeli.
3. Zmień komórkę tytułu nowej funkcji z **szablonu obciążenia** na nazwę nowego obciążenia.
4. Wklej nową komórkę Nazwa obciążenia do kolumny Tag dla wszystkich wierszy poniżej nowej funkcji. Należy zachować ostrożność, aby nie zmieniać tagów ani nazw wierszy związanych z rzeczywistą funkcją **szablonu obciążenia** . Te elementy robocze będą potrzebne podczas dodawania kolejnego obciążenia do planu wdrożenia chmury.
5. Przejdź do kroku 8 w instrukcje dotyczące edycji zbiorczej, aby opublikować arkusz. Ten krok powoduje utworzenie wszystkich elementów roboczych wymaganych do migracji obciążenia.

Powtórz kroki od 1 do 5 dla każdego z obciążeń z listy możliwości 10.

## <a name="define-workloads"></a>Definiowanie obciążeń

Po zdefiniowaniu priorytetów początkowych i dodaniu obciążeń do planu, każde z obciążeń można zdefiniować za pomocą bardziej zaawansowanej analizy jakościowej. Przed dołączeniem dowolnego obciążenia do planu wdrażania w chmurze spróbuj udostępnić następujące punkty danych dla każdego obciążenia.

### <a name="business-inputs"></a>Dane wejściowe biznesowe

| Punkt danych | Opis | Dane wejściowe |
|---|---|---|
| Nazwa obciążenia | Co to jest to obciążenie? |         |
| Opis obciążenia | W jednym zdaniu, co robi to obciążenie? |         |
| Motywacje dotyczące wdrażania | Które z motywacji wdrażania chmury wpływają na to obciążenie? |         |
| Główny sponsor | Których dotyczy ten Uczestnik, który jest głównym sponsorem wnioskującym o poprzednie motywacje? |         |
| Jednostka biznesowa | Która jednostka biznesowa jest odpowiedzialna za koszt tego obciążenia? |         |
| Procesy biznesowe | Które procesy biznesowe mają wpływ na zmiany obciążenia? |         |
| Zespoły biznesowe | Które zespoły biznesowe mają wpływ na zmiany? |         |
| Zainteresowane strony biznesowe | Czy istnieją jakiekolwiek kierownictwo, których zmiany mogą wpływać na działalność? |         |
| Wyniki biznesowe | Jak firma będzie mierzyć sukces tego nakładu pracy? |         |
| Metryki | Jakie metryki będą używane do śledzenia sukcesu? |         |
| Zgodność | Czy istnieją jakieś wymagania dotyczące zgodności innych firm dla tego obciążenia? |         |
| Właściciele aplikacji | Kto jest odpowiedzialny za wpływ wszystkich aplikacji skojarzonych z tym obciążeniem? |         |
| Okresy zawieszania działalności biznesowej | Czy istnieją jakieś przypadki, w których firma nie będzie zezwalać na zmianę? |         |
| Lokalizacje geograficzne | Czy każdy lokalizacje geograficzne ma wpływ na to obciążenie? |         |

### <a name="technical-inputs"></a>Dane techniczne

| Punkt danych | Opis | Dane wejściowe |
|---|---|---|
| Podejście do wdrażania | Czy to przyjęcie jest kandydatem do migracji lub innowacji? |         |
| Klient Ops aplikacji | Wyświetl listę stron odpowiedzialnych za wydajność i dostępność tego obciążenia. |         |
| Umowy SLA | Wyświetl listę umów dotyczących poziomu usług (wymagania RTO/RPO). |         |
| Zagrożenia | Wyświetl listę bieżącej krytycznej aplikacji. |         |
| Klasyfikacja danych | Wyświetl listę klasyfikacji czułości danych. |         |
| Lokalizacje geograficzne operacyjny | Utwórz listę wszystkich lokalizacje geograficzne, w których obciążenie jest lub powinny być hostowane. |         |
| Aplikacje | Określ początkową listę lub liczbę wszystkich aplikacji uwzględnionych w tym obciążeniu. |         |
| Maszyny wirtualne | Określ początkową listę lub liczbę wszystkich maszyn wirtualnych lub serwerów uwzględnionych w obciążeniu. |         |
| Źródła danych | Określ początkową listę lub liczbę wszystkich źródeł danych uwzględnionych w obciążeniu. |         |
| Zależności | Wyświetl listę wszystkich zależności zasobów, które nie są uwzględnione w obciążeniu. |         |
| Lokalizacje geograficzne ruchu użytkownika | Utwórz listę lokalizacje geograficzne, która ma znaczną kolekcję ruchu użytkownika. |         |

## <a name="confirm-priorities"></a>Potwierdź priorytety

Na podstawie zebranych danych zespół strategii chmury i zespół wdrażania w chmurze powinien spełnić wymagania w celu ponownego oszacowania priorytetów. Wyjaśnienie punktów danych firmy może monitować o zmianę priorytetów. Złożoność techniczna lub zależności mogą skutkować zmianami związanymi z przydzielaniem kadr, osiami czasu lub sekwencjonowaniem wysiłków technicznych.

Po zakończeniu przeglądu oba zespoły powinny mieć doświadczenie z potwierdzeniem wynikających z tego priorytetu. Ten zestaw udokumentowanych, zweryfikowanych i potwierdzonych priorytetów jest zaległą pracą wdrożenia chmury.

## <a name="next-steps"></a>Następne kroki

W przypadku wszystkich obciążeń w zaległych zaległościach wdrożenia w chmurze zespół jest gotowy do [wyrównywania zasobów](./assets.md).

> [!div class="nextstepaction"]
> [Dopasuj zasoby dla obciążeń z priorytetyzacją](./assets.md)
