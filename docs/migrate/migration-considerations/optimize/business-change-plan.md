---
title: Opracowywanie planu zmiany biznesowej
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, w jaki sposób plan zmian firmy może pomóc w zaimplementowaniu szerszego planu wdrażania użytkowników.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 117f8bebd157069703add28348667abe88ddf96e
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80432430"
---
# <a name="business-change-plan"></a>Plan zmian biznesowych

Tradycyjnie odpowiedzialność za nadzór nad wydawaniem nowych obciążeń należała do działu IT. Podczas znacznej transformacji, takiej jak migracja centrum danych lub migracja w chmurze, można zastosować podobny wzorzec wdrażania potencjalnego klienta działu IT. Jednak tradycyjne podejście może spowodować niewykorzystanie szans uzyskania dodatkowej wartości biznesowej. Z tego powodu przed podwyższeniem poziomu migrowanego obciążenia do środowiska produkcyjnego zalecane jest zaimplementowanie szerszego podejścia do wdrażania użytkowników. W tym artykule opisano sposoby dodawania wartości do standardowego planu wdrażania użytkowników dzięki użyciu planu zmian biznesowych.

## <a name="traditional-user-adoption-approach"></a>Tradycyjne podejście do wdrażania użytkowników

Plany wdrażania użytkowników koncentrują się na sposobie wdrażania nowej technologii lub zmiany danej technologii przez użytkowników. To podejście zostało przetestowane pod kątem czasu, który zajmuje użytkownikom rozpoczęcie pracy z nowymi narzędziami. W typowym planie wdrażania użytkowników dział IT koncentruje się na instalacji, konfiguracji, konserwacji i szkoleniach związanych ze zmianami technicznymi wprowadzanymi w środowisku biznesowym.

Chociaż podejścia mogą się różnić, ogólne motywy są wspólne dla większości planów wdrażania użytkowników. Motywy te są zwykle oparte na kontroli ryzyka i podejściu ułatwiającym dostosowanie do przyrostowych ulepszeń. Macierz Eason pokazana na poniższym rysunku reprezentuje czynniki wspierające te motywy w szerokim spektrum typów wdrażania.

![Macierz Eason z zagadnieniami dotyczącymi wdrażania użytkowników](../../../_images/migrate/eason-matrix.jpg)

*Macierz Eason typów wdrażania użytkowników.*

Te motywy często opierają się na założeniu, że wprowadzanie nowych rozwiązań dla użytkowników powinno koncentrować się głównie na kontroli ryzyka i upraszczaniu zmian. Ponadto dział IT skupia się głównie na ryzyku związanym ze zmianą technologiczną i upraszczaniu wprowadzania tej zmiany.

## <a name="create-business-change-plans"></a>Tworzenie planów zmian firmy

Plan zmian biznesowych wykracza poza zmianę techniczną i zakłada, że każde wydanie w ramach działań związanych z migracją wymaga pewnego poziomu zmian w procesie biznesowym. Plan ten obejmuje strumienie wychodzące i przychodzące związane ze zmianami technicznymi. Poniższe pytania ułatwiają uczestnikom spojrzenie na proces wdrażania użytkowników z perspektywy zmian biznesowych w celu zmaksymalizowania ich wpływu na firmę:

**Pytania dotyczące strumieni wychodzących.** Pytania dotyczące strumieni wychodzących są związane z wpływem lub zmianami, które zachodzą przed wdrożeniem użytkowników:

- Czy oczekiwany [wynik biznesowy](../../../strategy/business-outcomes/index.md) został osiągnięty?
- Czy wpływ na firmę jest mapowany na zdefiniowane [metryki szkoleniowe](../../../strategy/learning-metrics.md)?
- Które procesy biznesowe i zespoły korzystają z zalet tego rozwiązania technicznego?
- Kto w firmie może najlepiej zidentyfikować użytkowników zaawansowanych na potrzeby testowania i formułowania opinii?
- Czy wybrani liderzy biznesowi brali udział w priorytetyzacji i planowaniu migracji?
- Czy istnieją powiązane z firmą zdarzenia lub daty o krytycznym znaczeniu, które mogą mieć wpływ na tę zmianę?
- Czy plan zmian biznesowych maksymalizuje wpływ, ale minimalizuje zakłócenia działania firmy?
- Czy przestoje są oczekiwane? Czy informacje na temat przedziału czasu przestoju zostały przekazane użytkownikom końcowym?

**Pytania dotyczące strumieni przychodzących.** Po zakończeniu wdrażania można rozpocząć zmianę biznesową. Niestety w tym momencie kończy się wiele planów wdrażania użytkowników. Pytania dotyczące strumieni przychodzących ułatwiają zespołowi strategicznemu ds. chmury skoncentrowanie się na transformacji po zakończeniu zmiany technicznej:

- Czy użytkownicy biznesowi dobrze reagują na zmiany?
- Czy po wdrożeniu zmiany biznesowej jest obsługiwana przewidywana wydajność?
- Czy procesy biznesowe lub środowiska klienta zmieniają się w oczekiwany sposób?
- Czy do zrealizowania metryk szkoleniowych są wymagane dodatkowe zmiany?
- Czy zmiany zostały dopasowane do docelowych wyników działalności biznesowej? Jeśli nie, dlaczego?
- Czy do współtworzenia wyników działalności biznesowej są wymagane dodatkowe zmiany?
- Czy w wyniku tej zmiany zaobserwowano jakiekolwiek negatywne skutki?

Plan zmian biznesowych różni się w zależności od firmy. Celem tych pytań jest usprawnienie integracji firmy ze zmianami skojarzonymi z poszczególnymi wersjami. Dzięki przeanalizowaniu każdej wersji nie jako zmiany technologicznej do wdrożenia, ale jako planu zmian biznesowych można zwiększyć szansę osiągnięcia wyników działalności firmy.

## <a name="next-steps"></a>Następne kroki

Po udokumentowaniu i zaplanowaniu zmiany biznesowej można rozpocząć [testowanie biznesowe](./business-test.md).

> [!div class="nextstepaction"]
> [Wskazówki dotyczące testowania biznesowego (testowania akceptacyjnego przez użytkowników) podczas migracji](./business-test.md)

## <a name="references"></a>Dokumentacja

<!-- cSpell:ignore Eason -->

- Eason, K. (1988) _technologia informacyjna i zmiana organizacyjna_, Nowy Jork: Taylor i Francis.
