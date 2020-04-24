---
title: Procesy zgodności zasad linii bazowej zabezpieczeń
description: Zapoznaj się z podejściem do tworzenia procesów, które obsługują dyscyplinę ładu zabezpieczeń w chmurze dla platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fb47ce9aea9baa27404ad927cee344cb0a9fec6c
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80433600"
---
# <a name="security-baseline-policy-compliance-processes"></a>Procesy zgodności zasad linii bazowej zabezpieczeń

W tym artykule omówiono podejście do przestrzegania zasad, które regulują [podstawy zabezpieczeń](./index.md). Skuteczne zarządzanie zabezpieczeniami w chmurze rozpoczyna się od cyklicznych procesów ręcznych zaprojektowanych w celu wykrywania luk w zabezpieczeniach i nakładania zasad w celu skorygowania zagrożeń bezpieczeństwa. Wymaga to regularnego zaangażowania zespołu nadzoru chmurowego i zainteresowanej firmy oraz udziałowców IT do przeglądania i aktualizowania zasad oraz zapewnienia zgodności z zasadami. Ponadto wiele procesów monitorowania i wymuszania można zautomatyzować lub uzupełnić narzędziem, aby zmniejszyć koszty zarządzania i umożliwić szybsze reagowanie na odchylenia zasad.

## <a name="planning-review-and-reporting-processes"></a>Planowanie, przeglądanie i raportowanie procesów

Najlepsze w chmurze narzędzia linii bazowej zabezpieczeń są takie same jak w przypadku procesów i zasad, które są przez nie obsługiwane. Poniżej znajduje się zestaw przykładowych procesów, które często korzystają z dyscypliny linii bazowej zabezpieczeń. Te przykłady są używane jako punkt wyjścia podczas planowania procesów, które umożliwią kontynuowanie aktualizacji zasad zabezpieczeń na podstawie zmian i opinii firmy z punktu widzenia działania.

**Wstępna ocena ryzyka i planowanie:** W ramach początkowego wdrożenia dyscypliny linii bazowej zabezpieczeń należy określić podstawowe zagrożenia biznesowe i tolerancje związane z zabezpieczeniami w chmurze. Te informacje służą do omówienia określonych zagrożeń technicznych z członkami zespołów IT i zabezpieczeń oraz opracowania bazowego zestawu zasad zabezpieczeń w celu ograniczenia tych zagrożeń w celu ustalenia wstępnej strategii zarządzania.

**Planowanie wdrożenia:** Przed wdrożeniem jakichkolwiek obciążeń lub zasobów wykonaj Przegląd zabezpieczeń, aby zidentyfikować wszelkie nowe zagrożenia i upewnić się, że spełnione są wszystkie wymagania dotyczące zasad zabezpieczeń i dostępu do danych.

**Testowanie wdrożenia:** W ramach procesu wdrażania dowolnego obciążenia lub zasobu zespół nadzorujący chmury, we współpracy z firmowymi zespołami ds. zabezpieczeń, będzie odpowiedzialny za przeglądanie wdrożenia w celu zweryfikowania zgodności z zasadami zabezpieczeń.

**Planowanie roczne:** Co roku należy przeprowadzić przegląd strategii odniesienia zabezpieczeń na wysokim poziomie. Zapoznaj się z przyszłymi priorytetami firmowymi i zaktualizowanymi strategiami wdrażania chmury, aby zidentyfikować potencjalne zwiększenie ryzyka i inne nowe wymagania dotyczące zabezpieczeń. Za pomocą tego czasu można także zapoznać się z najnowszymi najlepszymi rozwiązaniami dotyczącymi zabezpieczeń i zintegrować je z zasadami i przeglądać procesy.

**Kwartalne przeglądy i planowanie:** Co kwartał dokonuje przeglądu danych inspekcji zabezpieczeń i raportów zdarzeń, aby zidentyfikować zmiany wymagane przez zasady zabezpieczeń. W ramach tego procesu zapoznaj się z bieżącą cyberbezpieczeństwa poziomą, aby aktywnie przewidzieć nowe zagrożenia i zaktualizować zasady zgodnie z potrzebami. Po zakończeniu przeglądu Wyrównaj wskazówki dotyczące projektowania ze zaktualizowanymi zasadami.

Ten proces planowania jest również dobrym terminem do oszacowania bieżącego członkostwa w zespole nadzoru w chmurze w celu uzyskania luk w zabezpieczeniach związanych z nowymi lub zmianami zasad i zagrożeń związanych z bezpieczeństwem. Zaproś odpowiednich pracowników działu IT o uczestnictwo w recenzjach i planowaniu jako tymczasowych doradców technicznych lub stałych członków zespołu.

**Edukacja i szkolenia:** Co miesiąc, oferuj sesje szkoleniowe, aby upewnić się, że personel IT i deweloperzy są aktualne zgodnie z najnowszymi wymaganiami dotyczącymi zasad zabezpieczeń. W ramach tego procesu zapoznaj się z dokumentacją, wskazówkami lub innymi aktywami szkoleniowymi, aby upewnić się, że są one zsynchronizowane z najnowszymi instrukcjami zasad obowiązującymi w firmie.

**Comiesięczne przeglądy audytu i raportowania:** Co miesiąc należy przeprowadzić inspekcję we wszystkich wdrożeniach w chmurze w celu zapewnienia ciągłego wyrównania przy użyciu zasad zabezpieczeń. Przejrzyj działania związane z zabezpieczeniami z personelem działu IT i zidentyfikuj wszelkie problemy ze zgodnością, które nie zostały jeszcze obsłużone w ramach trwającego procesu monitorowania i wymuszania. Wynikiem tego przeglądu jest raport dotyczący zespołu strategii chmury i każdego zespołu wdrażania w chmurze w celu komunikowania się ogólnego przestrzegania zasad. Raport jest również przechowywany na potrzeby inspekcji i przepisów prawnych.

## <a name="ongoing-monitoring-processes"></a>Procesy trwającego monitorowania

Ustalanie, czy strategia ładu zabezpieczeń zakończyła się pomyślnie, zależy od widoczności bieżącego i wcześniejszego stanu infrastruktury chmurowej. Bez możliwości analizowania odpowiednich metryk i danych dotyczących kondycji i aktywności zasobów w chmurze nie można identyfikować zmian zagrożeń ani wykrywać naruszeń tolerancji ryzyka. Bieżące procesy zarządzania omówione powyżej wymagają danych dotyczących jakości, aby zapewnić możliwość modyfikacji zasad w celu lepszego zabezpieczenia infrastruktury przed zmianami zagrożeń i wymagań w zakresie zabezpieczeń.

Upewnij się, że Twoje zabezpieczenia i zespoły IT zaimplementowali zautomatyzowane systemy monitorowania dla infrastruktury chmurowej, które przechwytują odpowiednie dane dzienników potrzebne do oszacowania ryzyka. Możliwość aktywnego monitorowania tych systemów w celu zapewnienia wykrywania monitów i łagodzenia potencjalnych naruszeń zasad oraz zapewnienia zgodności strategii monitorowania z wymaganiami dotyczącymi zabezpieczeń.

## <a name="violation-triggers-and-enforcement-actions"></a>Wyzwalacze naruszenia i akcje wymuszania

Ze względu na to, że niezgodność zabezpieczeń może prowadzić do zagrożenia krytycznego i zagrożeń danych oraz zagrożeń związanych z zakłóceniami usług, zespół nadzorujący chmury powinien mieć wgląd w poważne naruszenia zasad. Upewnij się, że personel działu IT ma jasne ścieżki eskalacji do zgłaszania problemów z zabezpieczeniami do członków zespołu nadzoru najlepiej dopasowane do identyfikowania i weryfikowania problemów z zasadami.

W przypadku wykrycia naruszeń należy podjąć akcje, aby szybko dostosować je za pomocą zasad najszybciej, jak to możliwe. Zespół IT może zautomatyzować większość wyzwalaczy naruszenia przy użyciu narzędzi opisanych w [punkcie odniesienia zabezpieczeń łańcucha narzędzi dla platformy Azure](./toolchain.md).

Następujące wyzwalacze i akcje wymuszania zawierają przykłady, które można przywołać podczas planowania użycia danych monitorowania do rozwiązywania naruszeń zasad:

- **Wykryto zwiększenie ataków.** Jeśli którykolwiek z zasobów napotyka 25% wzrostu DDoS lub ataków typu "z przepisami". Śledź informacje o problemach i aktualizacjach, jeśli konieczna jest zmiana zasad w celu zapobieżenia przyszłym zdarzeniom.
- **Wykryto niesklasyfikowane dane.** Każde źródło danych bez odpowiedniej ochrony prywatności, bezpieczeństwa lub wpływu na działalność biznesową będzie miało odmowę dostępu do momentu zastosowania klasyfikacji przez właściciela danych i odpowiedniego poziomu ochrony danych.
- **Wykryto problem z kondycją zabezpieczeń.** Wyłącz dostęp do wszystkich maszyn wirtualnych, które mają znane luki w zabezpieczeniach lub złośliwego oprogramowania, które zostały zidentyfikowane do momentu zainstalowania odpowiednich poprawek lub oprogramowania zabezpieczającego. Zaktualizuj wskazówki dotyczące zasad w celu uwzględnienia wszelkich nowo wykrytych zagrożeń.
- **Wykryto lukę w zabezpieczeniach.** Dostęp do dowolnych zasobów niejawnie dozwolonych przez zasady dostępu do sieci powinien wyzwolić alert dla personelu zabezpieczeń IT i odpowiedniego właściciela obciążenia. Śledź informacje o problemach i aktualizacjach, jeśli konieczna jest zmiana zasad w celu ograniczenia przyszłych zdarzeń.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu zarządzania chmurą](./template.md)można udokumentować procesy i wyzwalacze, które są wyrównane do bieżącego planu wdrożenia chmury.

Aby uzyskać wskazówki dotyczące wykonywania zasad zarządzania chmurą w wyrównaniu z planami wdrażania, zapoznaj się z artykułem dotyczącym ulepszania dyscypliny.

> [!div class="nextstepaction"]
> [Poprawa dyscypliny linii bazowej zabezpieczeń](./discipline-improvement.md)
