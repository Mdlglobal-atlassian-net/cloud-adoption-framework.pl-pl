---
title: Procesy zgodności z zasadami spójności zasobów
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać podejście do tworzenia procesów, które obsługują dyscyplinę ładu o spójności zasobów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dd9f23a35e4e97605c23fbc52d32433eab97539b
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80433666"
---
# <a name="resource-consistency-policy-compliance-processes"></a>Procesy zgodności z zasadami spójności zasobów

W tym artykule omówiono podejście do procesu przestrzegania zasad, które regulują [spójność zasobów](./index.md). Efektywne zarządzanie spójnością zasobów w chmurze rozpoczyna się od cyklicznych procesów ręcznych zaprojektowanych w celu zidentyfikowania niewydajnej sprawności działania, usprawnienia zarządzania wdrożonymi zasobami i zapewnienia, że obciążenia o kluczowym znaczeniu mają minimalne zakłócenia. Te procesy ręczne są uzupełniane przy użyciu monitorowania, automatyzacji i narzędzi, aby zmniejszyć koszty zarządzania i zapewnić szybszą odpowiedź na odchylenia zasad.

## <a name="planning-review-and-reporting-processes"></a>Planowanie, przeglądanie i raportowanie procesów

Platformy w chmurze zapewniają tablicę narzędzi do zarządzania i funkcji, których można użyć do organizowania, aprowizacji, skalowania i minimalizowania przestojów. Korzystanie z tych narzędzi do efektywnej struktury i obsługi wdrożeń w chmurze w sposób, który koryguje potencjalne zagrożenia, wymaga dobrze przemyślanych procesów i zasad, a także ścisłej współpracy z zespołami operacyjnymi IT i uczestnikami biznesowymi.

Poniżej znajduje się zestaw przykładowych procesów często powiązanych z dyscypliną spójności zasobów. Te przykłady są używane jako punkt wyjścia podczas planowania procesów, które umożliwią kontynuowanie aktualizacji zasad spójności zasobów na podstawie zmian w firmie i informacji zwrotnych z rozwoju i zespołów IT z uwzględnieniem wskazówek do działania.

**Wstępna ocena ryzyka i planowanie:** W ramach początkowego wdrożenia dyscypliny spójności zasobów należy określić podstawowe zagrożenia biznesowe i tolerancje związane z operacjami i zarządzaniem nimi. Te informacje służą do omówienia określonych zagrożeń technicznych z członkami zespołów IT i właścicieli obciążeń w celu opracowania bazowego zestawu zasad spójności zasobów przeznaczonych do korygowania tych zagrożeń, co ustanawia wstępną strategię nadzoru.

**Planowanie wdrożenia:** Przed wdrożeniem dowolnego elementu zawartości wykonaj przegląd w celu zidentyfikowania nowych zagrożeń operacyjnych. Ustanów wymagania dotyczące zasobów i oczekiwane wzorce popytu oraz Zidentyfikuj wymagania dotyczące skalowalności i potencjalne możliwości optymalizacji użycia. Upewnij się również, że plany tworzenia kopii zapasowych i odzyskiwania są wykonywane.

**Testowanie wdrożenia:** W ramach wdrożenia zespół ds. zarządzania chmurą, we współpracy z zespołami operacyjnymi w chmurze, będzie odpowiedzialny za przejrzenie wdrożenia w celu weryfikacji zgodności z zasadami spójności zasobów.

**Planowanie roczne:** Co roku należy przeprowadzić przegląd strategii spójności zasobów na wysokim poziomie. Zapoznaj się z przyszłymi planami lub priorytetami rozwinięcia firmy oraz zaktualizuj strategie wdrażania chmury, aby identyfikować potencjalne zwiększenie ryzyka lub inne nowe wymagania dotyczące spójności zasobów. Użyj tego czasu, aby zapoznać się z najnowszymi najlepszymi rozwiązaniami dotyczącymi spójności zasobów w chmurze i zintegrować je z zasadami i przeglądać procesy.

**Kwartalne przeglądy i planowanie:** Co kwartał dokonuje przeglądu danych operacyjnych i raportów zdarzeń, aby zidentyfikować zmiany wymagane w zasadach spójności zasobów. W ramach tego procesu zapoznaj się z tematem zmiany użycia zasobów i wydajności w celu zidentyfikowania zasobów, które wymagają zwiększenia lub zmniejszenia alokacji zasobów i zidentyfikowania wszelkich obciążeń lub zasobów, które są kandydatami do wycofania.

Ten proces planowania jest również dobrym terminem do oszacowania bieżącego członkostwa w zespole nadzoru w chmurze na potrzeby luk w wiedzy dotyczącej nowych lub zmienionych zasad i zagrożeń związanych ze spójnością zasobów jako dyscypliny. Zaproś odpowiednich pracowników działu IT o uczestnictwo w recenzjach i planowaniu jako tymczasowych doradców technicznych lub stałych członków zespołu.

**Edukacja i szkolenia:** Co miesiąc, oferuj sesje szkoleniowe, aby upewnić się, że personel IT i deweloperzy są aktualne zgodnie z najnowszymi wymaganiami dotyczącymi zasad spójności zasobów. W ramach tego procesu zapoznaj się z dokumentacją lub innymi aktywami szkoleniowymi, aby upewnić się, że są one zsynchronizowane z najnowszymi instrukcjami zasad obowiązującymi w firmie.

**Comiesięczne przeglądy audytu i raportowania:** Co miesiąc należy przeprowadzić inspekcję we wszystkich wdrożeniach w chmurze w celu zapewnienia ciągłego wyrównania przy użyciu zasad spójności zasobów. Przejrzyj powiązane działania z personelem działu IT i zidentyfikuj wszelkie problemy ze zgodnością, które nie zostały jeszcze obsłużone w ramach trwającego procesu monitorowania i wymuszania. Wynikiem tego przeglądu jest raport dotyczący zespołu strategii chmury i każdego zespołu wdrażania w chmurze w celu przekazywania ogólnej wydajności i przestrzegania zasad. Raport jest również przechowywany na potrzeby inspekcji i przepisów prawnych.

## <a name="ongoing-monitoring-processes"></a>Procesy trwającego monitorowania

Ustalanie, czy strategia ładu dotycząca spójności zasobów zakończyła się pomyślnie, zależy od widoczności bieżącego i wcześniejszego stanu infrastruktury chmurowej. Bez możliwości analizowania odpowiednich metryk i danych dotyczących kondycji i aktywności środowiska chmury nie można identyfikować zmian zagrożeń ani wykrywać naruszeń tolerancji ryzyka. Bieżące procesy ładu omówione powyżej wymagają danych dotyczących jakości, aby zapewnić możliwość modyfikacji zasad w celu zoptymalizowania użycia zasobów w chmurze i zwiększenia ogólnej wydajności obciążeń hostowanych w chmurze.

Upewnij się, że zespoły IT zaimplementowali zautomatyzowane systemy monitorowania dla infrastruktury chmurowej, które przechwytują odpowiednie dane dzienników potrzebne do oszacowania zagrożeń. Można aktywnie monitorować te systemy w celu zapewnienia wykrywania monitów i łagodzenia potencjalnych naruszeń zasad oraz upewnić się, że strategia monitorowania jest zgodne z potrzebami operacyjnymi.

## <a name="violation-triggers-and-enforcement-actions"></a>Wyzwalacze naruszenia i akcje wymuszania

Ze względu na to, że zgodność zasad spójności zasobów może prowadzić do krytycznych przerw w działaniu usługi lub znaczących przekroczeń kosztów, zespół nadzorujący chmury powinien mieć wgląd w zdarzenia niezgodności. Upewnij się, że personel działu IT ma jasne ścieżki eskalacji do raportowania tych problemów do członków zespołu nadzoru najlepiej dopasowane do identyfikowania i weryfikowania problemów z zasadami, które zostały wyeliminowane po wykryciu problemu.

W przypadku wykrycia naruszeń należy podjąć akcje, aby szybko dostosować je za pomocą zasad najszybciej, jak to możliwe. Zespół IT może zautomatyzować większość wyzwalaczy naruszenia przy użyciu narzędzi opisanych w [łańcucha narzędzi spójności zasobów dla platformy Azure](./toolchain.md).

Następujące wyzwalacze i akcje wymuszania zawierają przykłady, które można przywołać podczas planowania użycia danych monitorowania do rozwiązywania naruszeń zasad:

- **Wykryto zasób nadmiernej aprowizacji.** Zasoby wykryte przy użyciu mniejszej niż 60% pojemności procesora lub pamięci powinny automatycznie skalować w dół lub cofać obsługę administracyjną, aby obniżyć koszty.
- **Wykryto nieudostępniany zasób.** Zasoby wykryte przy użyciu ponad 80% pojemności procesora lub pamięci powinny automatycznie skalować w górę lub aprowizacji dodatkowe zasoby w celu zapewnienia dodatkowej pojemności.
- **Nieoznakowane tworzenie zasobów.** Każde żądanie utworzenia zasobu bez wymaganych tagów Meta zostanie odrzucone automatycznie.
- **Wykryto krytyczną awarię zasobów.** Pracownicy działu IT są powiadamiani o wszystkich wykrytych przestojach. Jeśli przestój nie zostanie natychmiast rozpoznawalny, personel będzie eskalować problem i powiadomić właścicieli obciążeń i zespół nadzorujący chmurę. Zespół ds. zarządzania chmurą będzie śledził problem do momentu rozwiązania problemu i aktualizacji, jeśli konieczna jest zmiana zasad w celu zapobieżenia przyszłym zdarzeniom.
- **Dryf konfiguracji.** Wykryte zasoby, które nie są zgodne z ustalonymi liniami bazowymi, powinny wyzwalać alerty i być automatycznie korygowane przy użyciu narzędzi do zarządzania konfiguracją, takich jak Azure Automation, Chef, Puppet lub rozwiązania ansible.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu zarządzania chmurą](./template.md)można udokumentować procesy i wyzwalacze, które są wyrównane do bieżącego planu wdrożenia chmury.

Aby uzyskać wskazówki dotyczące wykonywania zasad zarządzania chmurą w wyrównaniu z planami wdrażania, zapoznaj się z artykułem dotyczącym ulepszania dyscypliny.

> [!div class="nextstepaction"]
> [Udoskonalenie dyscypliny spójności zasobów](./discipline-improvement.md)
