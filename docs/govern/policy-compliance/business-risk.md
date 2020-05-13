---
title: Zrozumienie ryzyka biznesowego podczas migracji do chmury
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jakie są procesy zarządzania ryzykiem, które pomagają ocenić, zrozumieć, zrównoważyć i skorygować ryzyko związane z migracją.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: e0da2ec011f2fc6a823868d877780906ab472111
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83224310"
---
<!-- markdownlint-disable MD026 -->

# <a name="understand-business-risk-during-cloud-migration"></a>Zrozumienie ryzyka biznesowego podczas migracji do chmury

Zrozumienie ryzyka biznesowego to jeden z najważniejszych elementów transformacji chmury. Zasady dotyczące dysków ryzyka i wpływające na wymagania dotyczące monitorowania i wymuszania. Ryzyko zdecydowanie wpływa na sposób zarządzania obsługą cyfrową, lokalną lub chmurą.

<!-- markdownlint-enable MD026 -->

## <a name="relativity-of-risk"></a>Relativity ryzyka

Ryzyko jest względne. Niewielka firma z kilkoma zasobami IT w zamkniętym budynku ma niewielki czynnik ryzyka. Dodaj użytkowników i połączenie internetowe z dostępem do tych zasobów, tym ryzyku. Gdy mała firma rośnie do stanu listy Fortune 500, ryzyka są wykładniczo większe. W miarę jak przychód, proces biznesowy, liczba pracowników i zasoby INFORMATYCZNe kumulują się, ryzyka zwiększają się i łączą. Zasoby IT, które ułatwiają generowanie przychodów, są zagrożone ryzykiem zatrzymywania tego strumienia przychodów w przypadku awarii. Każdy moment przestoju odpowiada za straty. Podobnie jak w przypadku gromadzenia danych, ryzyko naruszenia klientów rośnie.

W tradycyjnym lokalnym świecie zespół zarządzający IT koncentruje się na ocenie ryzyka, tworzeniu procesów zarządzania tymi zagrożeniami i wdrażaniu systemów w celu zapewnienia, że środki zaradcze zostały pomyślnie wdrożone. Te wysiłki działają w celu zrównoważenia ryzyka wymaganego do działania w połączonym i nowoczesnych środowisku biznesowym.

## <a name="understand-business-risks-in-the-cloud"></a>Zrozumienie zagrożeń firmy w chmurze

W trakcie transformacji istnieją takie same względne zagrożenia.

- W trakcie wczesnego eksperymentu kilka zasobów jest wdrażanych z niewielkimi danymi. Ryzyko jest małe.
- Po wdrożeniu pierwszego obciążenia ryzyka zajmują trochę czasu. To ryzyko można łatwo skorygować, wybierając nieodłącznie zagrożoną aplikację z niewielką bazą użytkownika.
- Ponieważ większe obciążenia przechodzą w tryb online, ryzyka zmieniają się w każdej wersji. Nowe aplikacje są na bieżąco i są zmieniane.
- Gdy firma przenosi pierwsze 10 lub 20 aplikacji w tryb online, profil ryzyka jest znacznie różny niż w przypadku, gdy aplikacja 1000th przechodzi do środowiska produkcyjnego w chmurze.

Zasoby, które są gromadzone w tradycyjnym miejscu, w którym jest to możliwe, w miarę upływu czasu. Termin zapadalności działalności biznesowej i zespołów IT prawdopodobnie rośnie w podobny sposób. Ten równoległy wzrost może być w stanie utworzyć niezbędny bagaż zasad.

Podczas transformacji w chmurze firma i zespoły IT mają możliwość resetowania tych zasad i tworzenia nowych przy użyciu dojrzałych sposób myślenia.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-business-risk-mvp"></a>Co to jest SPECJALISTa z zakresu ryzyka biznesowego?

**Minimalny, żywotny produkt** jest często używany do definiowania najmniejszej jednostki elementu, który może generować wartości materialne. W przypadku wystąpienia ryzyka biznesowego zespół ds. zarządzania chmurą rozpoczyna się od założenia, że niektóre zasoby zostaną wdrożone w środowisku chmury w pewnym momencie. Są w nim nieznane te zasoby, a zespół może nie mieć pewności, jakie typy danych będą przechowywane w tych zasobach.

Podczas planowania ryzyka biznesowego zespół ds. zarządzania chmurą może skompilować dla najgorszego scenariusza i zmapować każde możliwe zasady do chmury. Jednak zidentyfikowanie wszystkich potencjalnych zagrożeń w firmie dla wszystkich scenariuszy użycia w chmurze może zająć dużo czasu i wysiłku, a także opóźnić implementację zarządzania dla obciążeń w chmurze. Nie jest to zalecane, ale jest opcją.

Z kolei podejście MVP pozwala zespołowi definiować początkowy punkt początkowy i zestaw założeń, które byłyby prawdziwe dla większości/wszystkich zasobów. Ten SPECJALISTa korzystający z tego ryzyka biznesowego będzie obsługiwał początkowe wdrożenia w chmurze o małych możliwościach skalowania lub testowania, a następnie używać ich jako podstawy do stopniowego identyfikowania i korygowaniem nowych zagrożeń związanych z potrzebami biznesowymi lub dodaniu dodatkowych obciążeń do środowiska chmury. Ten proces umożliwia zastosowanie zarządzania w całym procesie wdrażania chmury.

Poniżej przedstawiono kilka podstawowych przykładów ryzyka biznesowego, które mogą zostać uwzględnione w ramach programu MVP:

- Wszystkie zasoby są zagrożone usunięciem (w wyniku błędu, błędu lub konserwacji).
- Wszystkie zasoby są zagrożone generowaniem zbyt dużej ilości wydatków.
- Wszystkie zasoby mogą zostać naruszone przez słabe hasła lub ustawienia niezabezpieczone.
- Każdy element zawartości z otwartymi portami narażony na Internet ma ryzyko złamania.

Powyższe przykłady są przeznaczone do ustanowienia ryzyka biznesowego MVP jako teorii. Rzeczywista lista będzie unikatowa dla każdego środowiska.
Po ustaleniu ryzyka biznesowego, można je przekonwertować na [zasady](./index.md) , aby skorygować każde ryzyko.

<!-- markdownlint-enable MD026 -->

## <a name="incremental-risk-mitigation"></a>Przyrostowe Łagodzenie ryzyka

Ponieważ Organizacja wdraża więcej obciążeń w chmurze, zespoły deweloperów będą korzystać z coraz większej ilości zasobów w chmurze. W każdej iteracji są tworzone i przemieszczane nowe zasoby. W każdej wersji obciążenia są readied do podwyższania poziomu produkcji. Każdy z tych cyklów ma możliwość wprowadzenia wcześniej niezidentyfikowanych zagrożeń firmy.

Przy założeniu, że SPECJALISTa z ryzykiem biznesowym jest punktem początkowym dla początkowych działań związanych z wdrażaniem w chmurze, zarządzanie może zostać zawczesne w połączeniu z rosnącym użyciem zasobów w chmurze Gdy zespół zarządzający chmurą działa równolegle z zespołami wdrażania w chmurze, rozwój ryzyka biznesowego może zostać rozmieszczony w miarę ich zidentyfikowania, zapewniając stabilny, ciągły model do opracowywania terminów zarządzania.

Każdy przygotowany zasób może być łatwo klasyfikowany zgodnie z ryzykiem. Dokumenty klasyfikacji danych mogą być kompilowane lub tworzone równolegle z cyklami przejściowymi. Profil ryzyka i punkty ekspozycji mogą być również udokumentowane. W miarę upływu czasu niezwykle przejrzysty widok ryzyka biznesowego będzie się skupić w całej organizacji.

Każdy z iteracji zespół nadzorujący chmury może współpracować z zespołem ds. strategii chmurowej, aby szybko komunikować się z nowymi zagrożeniami, strategiami zaradczymi, kompromisami i potencjalnymi kosztami. Dzięki temu uczestnicy biznesowi i Liderzy IT mogą uzyskać dostęp do partnerów w dojrzałych, dobrze świadomych decyzjach. Następnie te decyzje informują o terminie zapadalności zasad. W razie potrzeby zmiany zasad generują nowe elementy robocze dla okresów ważności systemów infrastruktury podstawowej. Gdy wymagane są zmiany w systemach przemieszczania, zespoły wdrożenia chmury mają dużo czasu na wprowadzenie zmian, podczas gdy firma testuje systemy przemieszczane i opracowuje plan wdrażania użytkownika.

Takie podejście minimalizuje ryzyko, a jednocześnie umożliwia zespołowi szybkie przenoszenie. Gwarantuje również, że czynniki ryzyka są natychmiast rozwiązywane i rozwiązywane przed wdrożeniem.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak oszacować tolerancję ryzyka podczas wdrażania chmury.

> [!div class="nextstepaction"]
> [Ocena tolerancja ryzyka](./risk-tolerance.md)
