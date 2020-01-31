---
title: Cost Management procesów zgodności z zasadami
description: Cost Management procesów zgodności z zasadami
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6a6f5c5d13a98b6c210fececb2d6372e7f95626b
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76804150"
---
# <a name="cost-management-policy-compliance-processes"></a>Cost Management procesów zgodności z zasadami

W tym artykule omówiono sposób tworzenia procesów, które obsługują [Cost Management](./index.md) dyscypliny ładu. Efektywne zarządzanie kosztami chmury rozpoczyna się od cyklicznych procesów ręcznych zaprojektowanych w celu zapewnienia zgodności z zasadami. Wymaga to regularnego zaangażowania zespołu nadzoru chmurowego i zainteresowanych uczestników firmy o przeglądanie i aktualizowanie zasad i zapewnienie zgodności z zasadami. Ponadto wiele procesów monitorowania i wymuszania można zautomatyzować lub uzupełnić narzędziem, aby zmniejszyć koszty zarządzania i umożliwić szybsze reagowanie na odchylenia zasad.

## <a name="planning-review-and-reporting-processes"></a>Planowanie, przeglądanie i raportowanie procesów

Najlepsze Cost Management narzędzia w chmurze są takie same jak w przypadku procesów i zasad, które są przez nie obsługiwane. Poniżej znajduje się zestaw przykładowych procesów, które często są wykorzystywane w dyscyplinach Cost Management. Użyj tych przykładów jako punktu wyjścia podczas planowania procesów, które umożliwią dalszą aktualizację zasad kosztów na podstawie zmian i opinii firmy z zespołów gospodarczych podlegających wskazówkom dotyczącym ładu kosztów.

**Wstępna ocena ryzyka i planowanie:** W ramach początkowego wdrożenia dyscypliny Cost Management należy określić podstawowe zagrożenia biznesowe i tolerancje związane z kosztami chmury. Te informacje służą do omówienia związanych z budżetem i ryzykiem kosztów z członkami zespołów firmy i opracowania bazowego zestawu zasad pozwalających wyeliminować te zagrożenia w celu ustalenia wstępnej strategii zarządzania.

**Planowanie wdrożenia:** Przed wdrożeniem dowolnego elementu zawartości Ustanów prognozowany budżet w oparciu o oczekiwaną alokację w chmurze. Upewnij się, że informacje o własności i księgowaniu dla wdrożenia zostały udokumentowane.

**Planowanie roczne:** W skali rocznej należy przeprowadzić analizę zbiorczą wszystkich wdrożonych i wdrożonych zasobów. Wyrównaj budżety według jednostek biznesowej, działów, zespołów i innych odpowiednich działów, aby umożliwić samoobsługowe wdrażanie. Upewnij się, że lider poszczególnych jednostek rozliczeniowych ma świadomość budżetu i śledzenie wydatków.

Jest to czas, który należy wykonać przed zobowiązaniem lub w celu zmaksymalizowania rabatu. Warto wyrównać budżet roczny w roku obrachunkowym dostawcy w chmurze, co pozwala na dalsze użycie opcji rabatu na koniec roku.

**Planowanie kwartalne:** Corocznie Przejrzyj budżety z każdym liderem jednostki rozliczeniowej, aby wyrównać prognozowanie i rzeczywiste wydatki. W przypadku zmiany planu lub nieoczekiwanych wzorców wydatków należy wyrównać i ponownie przydzielić budżet.

Ten kwartalny proces planowania to również dobry moment na ocenę bieżącego członkostwa zespołu nadzoru w chmurze w celu uzyskania luk w wiedzy dotyczącej bieżących lub przyszłych planów firmy. Zaproś odpowiednich pracowników i właścicieli obciążeń o uczestnictwo w recenzjach i planowaniu jako tymczasowych klasyfikatorów lub stałych członków zespołu.

**Edukacja i szkolenia:** Co miesiąc, oferuj sesje szkoleniowe, aby upewnić się, że biznes i pracownicy IT są aktualne zgodnie z najnowszymi wymaganiami dotyczącymi zasad Cost Management. W ramach tego procesu zapoznaj się z dokumentacją, wskazówkami lub innymi aktywami szkoleniowymi, aby upewnić się, że są one zsynchronizowane z najnowszymi instrukcjami zasad obowiązującymi w firmie.

**Miesięczne raportowanie:** Miesięczne raporty są raportowane w oparciu o prognozę. Powiadamiaj liderów rozliczeń o wszelkich nieoczekiwanych odchyleniach.

Te podstawowe procesy ułatwią dostosowanie wydatków i ustanowienie podstawy Cost Management dyscypliny.

## <a name="processes-for-ongoing-monitoring"></a>Procesy do ciągłego monitorowania

Pomyślna strategia ładu Cost Management jest zależna od widoczności przeszłych, bieżących i planowanych przyszłych wydatków związanych z chmurą. Bez możliwości analizowania odpowiednich metryk i danych istniejących kosztów nie można identyfikować zmian ryzyka ani wykrywać naruszeń tolerancji ryzyka. Bieżące procesy ładu omówione powyżej wymagają danych dotyczących jakości, aby zapewnić możliwość modyfikacji zasad w celu lepszego zabezpieczenia infrastruktury przed zmianami wymagań firmy i użycia chmury.

Upewnij się, że zespoły IT zaimplementowali zautomatyzowane systemy do monitorowania wydatków i użycia w chmurze dla nieplanowanych odchyleń od przewidywanych kosztów. Ustanów systemy raportowania i zgłaszania alertów w celu zapewnienia wykrywania monitów i łagodzenia potencjalnych naruszeń zasad.

## <a name="compliance-violation-triggers-and-enforcement-actions"></a>Wyzwalacze naruszenia zgodności i akcje wymuszania

W przypadku wykrycia naruszeń należy wykonać akcje wymuszania, aby dostosować je za pomocą zasad. Można zautomatyzować większość wyzwalaczy naruszenia przy użyciu narzędzi opisanych w [Cost Management łańcucha narzędzi dla platformy Azure](./toolchain.md).

Poniżej przedstawiono przykłady wyzwalaczy:

- **Miesięczne odchylenia budżetu:** Omawiaj odchylenia w miesięcznych wydatkach, które przekraczają 20% współczynnik prognozowania w stosunku do wartości rzeczywistej przy użyciu lidera jednostki rozliczeniowej. Rejestrowanie rozwiązań i zmian w prognozie.
- **Tempo wdrażania:** Każde odchylenia na poziomie subskrypcji przekraczającym 20% spowoduje wyzwolenie przeglądu z liderem jednostki rozliczeniowej. Rejestrowanie rozwiązań i zmian w prognozie.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu zarządzania chmurą](./template.md)można udokumentować procesy i wyzwalacze, które są wyrównane do bieżącego planu wdrożenia chmury.

Aby uzyskać wskazówki dotyczące wykonywania zasad zarządzania chmurą w wyrównaniu z planami wdrażania, zapoznaj się z artykułem Cost Management dotyczącym ulepszania dyscypliny.

> [!div class="nextstepaction"]
> [Ulepszanie dyscypliny Cost Management](./discipline-improvement.md)
