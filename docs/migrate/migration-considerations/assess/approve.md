---
title: Zatwierdzanie zmian architektury przed migracją
description: Dowiedz się, jak sklasyfikować zmiany architektury, gdy są one wymagane, a także ustanowić odpowiednie działania zatwierdzania.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3d674cfe0378613530adb329ae21b9c379742e91
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312088"
---
# <a name="approve-architecture-changes-before-migration"></a>Zatwierdzanie zmian architektury przed migracją

Podczas procesu oceny migracji każde obciążenie jest oceniane, projektowane i szacowane w celu opracowania planu przyszłego stanu dla obciążenia. Niektóre obciążenia można zmigrować do chmury bez zmian w architekturze. Zachowanie konfiguracji i architektury lokalnej może ograniczyć ryzyko i usprawnić proces migracji. Niestety, nie każda aplikacja może działać w chmurze bez wprowadzenia zmian w architekturze. Gdy wymagane są zmiany architektury, ten artykuł może pomóc w klasyfikacji zmian i zawiera wskazówki dotyczące właściwych działań związanych z zatwierdzeniem.

## <a name="business-impact-and-approval"></a>Znaczenie zatwierdzania dla działalności firmy

Podczas migracji niektóre elementy mogą ulec zmianie w sposób mający wpływ na działalność firmy. Chociaż czasami nie można uniknąć zmiany, nieujawnione jest skutkiem niejawnych lub nieudokumentowanych zmian. Aby zapewnić wsparcie uczestnikom projektu w trakcie pracy nad migracją, ważne jest, aby uniknąć zaskakujących prób. Zaskoczenie właścicieli aplikacji lub uczestników projektu w firmie może spowolnić lub wstrzymać proces wdrożenia chmury.

Przed migracją należy przygotować właściciela służbowego dla wszystkich zmian, które mogą wpływać na procesy biznesowe, takie jak zmiany w:

- umowy dotyczące poziomu usług;
- wzorce dostępu lub wymagania dotyczące zabezpieczeń, które mają wpływ na użytkownika końcowego;
- praktyki przechowywania danych;
- wydajność podstawowych aplikacji.

Nawet wtedy, gdy obciążenie można zmigrować z minimalnymi zmianami lub bez nich, nadal może to mieć wpływ na działalność. Procesy replikacji mogą zmniejszać wydajność systemów produkcyjnych. Zmiany w środowisku związane z przygotowaniami do migracji mogą spowodować ograniczenia wydajności routingu lub sieci. Istnieje wiele dodatkowych wpływów, które mogą wynikać z replikacji, przemieszczenia lub podwyższenia poziomu.

Regularne działania związane z zatwierdzaniem mogą pomóc zminimalizować liczbę nieprzewidzianych sytuacji wynikających ze zmian lub spadku wydajności bądź ich uniknąć. Zespół wdrożeniowy ds. chmury powinien wykonać proces zatwierdzania na końcu procesu oceny, przed rozpoczęciem procesu migracji.

## <a name="existing-culture"></a>Istniejąca kultura

Zespoły IT prawdopodobnie opracowały i wdrożyły mechanizmy zarządzania zmianami dotyczącymi zasobów lokalnych. Te mechanizmy podlegają zwykle tradycyjnym procesom zarządzania zmianami opartym na bibliotece ITIL (Information Technology Infrastructure Library). W wielu przedsiębiorstwach, w których odbywa się migracja, tymi procesami kieruje zespół zarządzania zmianą (CAB), który jest odpowiedzialny za sprawdzanie, dokumentowanie i zatwierdzanie wszystkich wniosków o zmianę związanych z IT (RFC).

Do zespołu zarządzania zmianą zwykle należą eksperci z wielu zespołów IT i zespołów biznesowych, którzy szczegółowo rozpatrują wszystkie zmiany związane z IT z różnych perspektyw. Proces zatwierdzania plików przez zespół zarządzania zmianą jest sprawdzonym sposobem zmniejszania ryzyka i minimalizowania wpływu zmian dotyczących stabilnych obciążeń zarządzanych przez dział IT na działalność firmy.

## <a name="technical-approval"></a>Zatwierdzenie techniczne

Gotowość organizacji do zatwierdzania zmian technicznych jest jedną z najczęstszych przyczyn niepowodzenia migracji do chmury. Z powodu serii zatwierdzeń technicznych zostaje wstrzymanych więcej projektów niż z powodu jakiegokolwiek braku w platformie chmurowej. Przygotowanie organizacji do zatwierdzania zmian technicznych jest wymaganiem ważnym dla powodzenia migracji. Poniżej przedstawiono kilka najlepszych rozwiązań, które dają pewność, że organizacja jest gotowa do zatwierdzania technicznego.

### <a name="itil-change-advisory-board-challenges"></a>Wyzwania dla zespołu zarządzania zmianą ITIL

Każde podejście do zarządzania zmianami ma swój własny zestaw kontroli i procesów zatwierdzania. Migracja to seria ciągłych zmian, które na początku są niejednoznaczne i stają się coraz bardziej przejrzyste i zrozumiałe dopiero w trakcie wykonywania. Dlatego najlepiej sprawdzają się rozwiązania, w których migracja jest oparta na podejściach do zarządzania zmianami opartych na metodzie Agile, w których zespół strategiczny ds. chmury pełni rolę właściciela produktu.

Jednak skala i częstotliwość zmian podczas migracji do chmury nie jest zgodna z naturą procesów ITIL. Wymagania związane z zatwierdzaniem przez zespół zarządzania zmianą mogą stanowić ryzyko dla pomyślnej migracji, spowalniając lub wstrzymując cały proces. Ponadto na wczesnych etapach migracji niejednoznaczność jest duża, a wiedza specjalistyczna w tej dziedzinie – mała. Przez kilka pierwszych migracji obciążeń lub wydań zespół wdrożeniowy ds. chmury często dopiero się uczy. Dlatego zespół może mieć trudności z dostarczeniem typów danych wymaganych do uzyskania zatwierdzenia zespołu zarządzania zmianą.

Poniższe najlepsze rozwiązania mogą pomóc zespołowi zarządzania zmianą zachować pewien komfort podczas migracji i jednocześnie uniknąć pełnienia roli bolesnej blokady.

### <a name="standardize-change"></a>Standaryzacja zmian

Dla zespołu wdrożeniowego ds. chmury może być kuszące szczegółowe rozważanie decyzji dotyczących architektury dla każdego obciążenia migrowanego do chmury. Równie kuszące jest użycie migracji do chmury jako katalizatora refaktoryzacji wcześniejszych decyzji dotyczących architektury. Niezależnie od tego, czy organizacja migruje kilkaset maszyn wirtualnych czy kilkadziesiąt obciążeń, każdym podejściem można prawidłowo zarządzać. Podczas migrowania centrum danych składającego się z 1000 lub więcej zasobów każde z tych podejść jest uważane za antywzorzec wysokiego ryzyka, który znacząco zmniejsza prawdopodobieństwo sukcesu. Modernizacja, refaktoryzacja i zmiana architektury każdej aplikacji wymaga różnorodnych zestawów umiejętności i znaczących zmian, a te zadania tworzą zależności dotyczące wysiłków ludzkich na dużą skalę. Każda z tych zależności zwiększa ryzyko niepowodzenia migracji.

W artykule dotyczącym [racjonalizacji majątku cyfrowego](../../../digital-estate/rationalize.md) omówiono wpływ podstawowych założeń przyjętych podczas racjonalizacji majątku cyfrowego na elastyczność i oszczędność czasu. Standaryzacja zmian ma dodatkową korzyść. Wybierając domyślne podejście racjonalizacyjne do zarządzania procesem migracji, zespół doradczy ds. chmury lub właściciel produktu może sprawdzić i zatwierdzić zastosowanie jednej zmiany do długiej listy obciążeń. Ogranicza to konieczność zatwierdzania technicznego poszczególnych obciążeń do tych, które wymagają znaczącej zmiany architektury w celu zapewnienia zgodności z chmurą.

### <a name="clarify-expectations-and-roles-of-approvers"></a>Wyjaśnienie oczekiwań i ról osób zatwierdzających

Przed oceną pierwszego obciążenia zespół strategiczny ds. chmury powinien udokumentować oczekiwania wszystkich osób zaangażowanych w zatwierdzenie zmiany i poinformować o nich. To proste działanie może zapobiec kosztownym opóźnieniom, gdy zespół wdrożeniowy ds. chmury jest w pełni zaangażowany.

### <a name="seek-approval-early"></a>Wczesne występowanie o zatwierdzenie

Jeśli to możliwe, zmiany techniczne powinny być wykrywane i dokumentowane w trakcie procesu oceny. Niezależnie od procesów zatwierdzania zespół wdrożeniowy ds. chmury powinien wcześnie angażować osoby zatwierdzające. Im szybciej rozpocznie się zatwierdzanie zmiany, tym mniejsze jest prawdopodobieństwo, że proces zatwierdzania zablokuje działania związane z migracją.

## <a name="next-steps"></a>Następne kroki

Zastosowanie tych najlepszych rozwiązań powinno ułatwić integrowanie właściwych zatwierdzeń o niskim ryzyku w procesie migracji. Po zatwierdzeniu zmian dotyczących obciążeń zespół wdrożeniowy ds. chmury jest gotowy do [migracji obciążeń](../migrate/index.md).

> [!div class="nextstepaction"]
> [Migrowanie obciążeń](../migrate/index.md)
