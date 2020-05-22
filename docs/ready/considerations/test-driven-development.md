---
title: Programowanie oparte na testach dla stref wyładunkowej
description: Programowanie oparte na testach dla stref wyładunkowej
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: d7aa0f388f68e876569ef2e8c3638b77af8ed033
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755731"
---
# <a name="test-driven-development-tdd-for-landing-zones"></a>Programowanie sterowane testami dla stref docelowych

Programowanie oparte na testach to typowy proces opracowywania oprogramowania i DevOps, który poprawia jakość nowych funkcji i ulepszeń w dowolnym rozwiązaniu opartym na kodzie. Infrastruktura oparta na chmurze, a odpowiedni kod źródłowy mogą używać tego procesu, aby zapewnić, że strefy wyładunkowe spełniają wymagania podstawowe i są wysokiej jakości. Ten proces jest szczególnie przydatny, gdy strefy wypełniania są opracowywane i refaktoryzacj w ramach równoległego nakładu pracy programistycznej.

![Proces projektowania oparty na testach dla stref wyładunku w chmurze](../../_images/ready/test-driven-development-process.png)

W chmurze infrastruktura jest wyjściem kodu. Dobrze skonstruowany, testowany i sprawdzony kod tworzy strefę docelową. W przypadku [definicji stref wyładunkowych](../landing-zone/index.md)"strefa docelowa jest środowiskiem do hostowania obciążeń, a wstępne Inicjowanie obsługi administracyjnej za pomocą kodu. Obejmuje ona podstawowe możliwości przy użyciu zdefiniowanego zestawu usług w chmurze i najlepszych rozwiązań w celu **pomyślnego skonfigurowania**". W tym artykule opisano jedno podejście do korzystania z projektowania opartego na testach w celu spełnienia ostatniej części tej definicji, podczas gdy spełnione są wymagania dotyczące jakości, bezpieczeństwa, działania i zarządzania.

Takie podejście może służyć do zaspokajania prostych żądań funkcji podczas wczesnego opracowywania. W dalszej części cyklu wdrażania w chmurze proces ten może służyć do spełnienia wymagań dotyczących zabezpieczeń, operacji, zarządzania lub zgodności.

## <a name="definition-of-done"></a>Definicja gotowości

"Konfiguracja dla sukcesu" jest instrukcją subiektywną. Niniejszy dokument zawiera zespół platformy Cloud Platform z niewielkimi informacjami z możliwością podejmowania działań podczas tworzenia lub refaktoryzacji strefy. Brak przejrzystości może prowadzić do nieodebranych oczekiwań i luk w zabezpieczeniach w środowisku chmury. Przed refaktoryzacją lub zwiększeniem strefy docelowej zespół platformy Cloud Platform powinien zasięgnąć przejrzystości dotyczącej definicji gotowej dla każdej strefy docelowej.

Definicja gotowe to prosta Umowa między zespołem platformy Cloud Platform i innymi, których dotyczą zespoły. Niniejsza Umowa zawiera opis funkcji dodanej wartości, które powinny być uwzględniane w dowolnych działaniach związanych z programowaniem strefy. Często definicja gotowe jest listą kontrolną, która jest wyrównana do krótkoterminowego planu wdrożenia chmury. W przypadku dorosłych procesów te oczekiwane funkcje na liście kontrolnej będą miały własne kryteria akceptacji, aby utworzyć jeszcze większą przejrzystość. Gdy każda funkcja dodanej wartości spełnia kryteria akceptacji, strefa docelowa jest wystarczająco skonfigurowana, aby umożliwić pomyślne wypróbowanie bieżącego rzutu lub wydania.

Ponieważ zespoły przyjmują dodatkowe obciążenia i funkcje w chmurze, definicje kryteriów ukończenia i akceptacji staną się coraz bardziej skomplikowane.

## <a name="test-driven-development-cycle"></a>Cykl programowania oparty na testach

Cykl, który sprawia, że Programowanie oparte na testach jest często nazywany czerwonym/zielonym testem. W tym podejściu zespół platformy Cloud Platform rozpoczyna się od testu zakończonego niepowodzeniem (Red test) w oparciu o definicję gotowych i zdefiniowanych kryteriów akceptacji. Dla każdej funkcji lub kryteriów akceptacji zespół platform w chmurze ukończy zadania programistyczne do momentu, aż test zakończy się powodzeniem (zielony test). Cykl programistyczny bazujący na testach (test czerwony/zielony) powtarza podstawowe kroki na poniższej ilustracji i poniższej liście do momentu spełnienia pełnej definicji gotowej.

![Proces projektowania oparty na testach dla stref wyładunku w chmurze](../../_images/ready/test-driven-development-process.png)

- **Utwórz test:** Zdefiniuj test w celu sprawdzenia, czy zostały spełnione kryteria akceptacji dla określonej wartości — Dodaj funkcję. Automatyzuj test wszędzie tam, gdzie to możliwe.
- **Testowanie strefy docelowej:** Uruchom nowy test i wszystkie istniejące testy. Jeśli wymagana funkcja nie została jeszcze osiągnięta przez poprzednie wysiłki programistyczne i nie obejmuje oferty dostawcy chmury, test powinien zakończyć się niepowodzeniem. Uruchomienie istniejących testów pomaga sprawdzić, czy nowy test nie zmniejsza niezawodności funkcji strefy wyładunkowej dostarczanych przez istniejący kod.
- **Rozwiń i refaktoryzację strefy docelowej:** Dodaj lub zmodyfikuj kod źródłowy, aby spełnić żądaną wartość — Dodaj funkcję i popraw ogólną jakość bazy kodu. Aby sprostać najpełniejszemu duchowi programowania opartego na testach, zespół platformy w chmurze może dodać kod, aby spełniał żądaną funkcję i nic nie rób. W tym samym czasie, jakość i konserwacja kodu są udostępnionym nakładem pracy. Po spełnieniu nowych żądań funkcji zespół platformy Cloud Platform powinien dążyć do ulepszania kodu przez usunięcie duplikatów i wyjaśnienie kodu. Uruchamianie testów między nowym kodem i refaktoryzacją kodu źródłowego jest wysoce zalecane.
- **Wdrażanie strefy docelowej:** Gdy kod źródłowy będzie w stanie zrealizować żądanie funkcji, należy wdrożyć zmodyfikowaną strefę docelową dla dostawcy chmury w środowisku testowym lub piaskownicy.
- **Testowanie strefy docelowej:** Przetestowanie strefy docelowej powinno sprawdzić, czy nowy kod spełnia kryteria akceptacji dla wymaganej funkcji. Po zakończeniu wszystkich testów funkcja jest uznawana za ukończoną, a kryteria akceptacji są uważane za spełnione.

Gdy wszystkie funkcje i kryteria akceptacji przechodzą skojarzone testy, strefa docelowa jest gotowa do obsługi następnej fazy planu wdrażania chmury.

## <a name="simple-example-of-a-definition-of-done"></a>Prosty przykład definicji gotowej

W przypadku wstępnego wysiłku migracji definicja gotowe może być zbyt prosta. Poniżej znajduje się przykład jednej z tych w porównaniu prostych przykładów.

- Początkowa strefa docelowa zostanie użyta do hostowania 10 obciążeń do celów nauki początkowej. Te obciążenia nie mają znaczenia dla działalności firmy i nie mają dostępu do poufnych danych. W przyszłości najprawdopodobniej te obciążenia zostaną wydane w środowisku produkcyjnym, ale nie będzie można zmienić jej znaczenia. Aby obsłużyć te obciążenia, zespół wdrażania chmury będzie musiał spełnić następujące kryteria:

- Segmentacja sieci do dopasowania z proponowanym projektem sieci.
- Dostęp do zasobów obliczeniowych, magazynu i sieci w celu hostowania obciążeń wyrównanych do odnajdowania urządzeń cyfrowych.
- Określanie nazw i tagowanie schematu do łatwego użycia.
- To środowisko powinno być traktowane jako _strefa zdemilitaryzowana (DMZ)_ z dostępem do publicznej sieci Internet.
- W trakcie podejmowania wysiłków zespół ds. wdrażania w chmurze chce, aby w celu zmiany konfiguracji usług był tymczasowy dostęp do środowiska.
- W przypadku tylko świadomości: przed wydaniem produkcyjnym te obciążenia będą wymagały integracji z firmowym dostawcą tożsamości w celu zarządzania trwającą tożsamością i dostępem do celów związanych z zarządzaniem operacjami. Czas, w którym powinien zostać odwołany dostęp zespołu wdrożenia chmury.

Ostatni z powyższych punktów nie jest kryterium funkcji ani akceptacji. Ale jest wskaźnikiem, że dodatkowe rozszerzenia będą wymagane i powinny być zbadane z innymi zespołami wczesnie.

## <a name="additional-examples-of-a-definition-of-done"></a>Dodatkowe przykłady definicji gotowe

Metodologia zarządzania w ramach platformy wdrażania w chmurze zawiera opisową drogę na podstawie naturalnego okresu zapadalności zespołu nadzoru. Osadzony w tej podróży to kilka przykładów "definicji gotowe" i "kryteria akceptacji" w postaci instrukcji zasad.

- [Początkowe instrukcje zasad](../../govern/guides/complex/initial-corporate-policy.md#policy-statements): Przykładowe zasady firmowe określające i wstępne definicje wykonywane na podstawie wymagań dotyczących wdrażania na wczesnym etapie.
- [Rozszerzanie tożsamości](../../govern/guides/complex/identity-baseline-improvement.md#incremental-improvement-of-the-policy-statements): Przykładowe zasady firmowe, w tym ("Definicja gotowe") spełniające wymagania rozszerzające Zarządzanie tożsamościami dla strefy docelowej.
- [Rozszerzanie zabezpieczeń](../../govern/guides/complex/security-baseline-improvement.md#incremental-improvement-of-the-policy-statements): Przykładowe zasady firmowe określające ("Definicja gotowe") spełniające wymagania dotyczące zabezpieczeń dostosowane do planu wdrożenia chmury referencyjnej.
- [Rozszerzanie operacji](../../govern/guides/complex/resource-consistency-improvement.md#incremental-improvement-of-the-policy-statements): Przykładowe zasady firmowe, w tym ("Definicja gotowe") spełniające podstawowe wymagania dotyczące zarządzania operacjami.
- [Rozszerzanie kosztów](../../govern/guides/complex/cost-management-improvement.md#changes-to-the-policy-statements): Przykładowe zasady firmowe, w tym ("Definicja gotowe") w celu spełnienia wymagań związanych z zarządzaniem kosztami.

Powyższe przykłady są podstawowymi przykładami, które ułatwiają opracowywanie "definicji gotowe" dla stref wyładunkowej. Dodatkowe przykładowe zasady są dostępne w ramach każdej [dyscypliny zarządzania chmurą](../../govern/governance-disciplines.md).

## <a name="next-steps"></a>Następne kroki

Aby przyspieszyć Programowanie oparte na testach na platformie Azure, zapoznaj się [z funkcjami projektowania opartymi na testach platformy Azure](./azure-test-driven-development.md).

> [!div class="nextstepaction"]
> [Programowanie oparte na testach na platformie Azure](./azure-test-driven-development.md)
