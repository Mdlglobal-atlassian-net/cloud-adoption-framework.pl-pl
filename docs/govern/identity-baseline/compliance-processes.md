---
title: Procesy zgodności zasad linii bazowej tożsamości
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesy zgodności zasad linii bazowej tożsamości
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6b92072ed182eefc596ab446638a87b4fd560080
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73566214"
---
# <a name="identity-baseline-policy-compliance-processes"></a>Procesy zgodności zasad linii bazowej tożsamości

W tym artykule omówiono podejście do przestrzegania zasad, które regulują [podstawową tożsamość](./index.md). Skuteczne zarządzanie tożsamościami rozpoczyna się od powtarzalnych ręcznych procesów, które są pomocne podczas wdrażania zasad dotyczących tożsamości i poprawek. Wymaga to regularnego zaangażowania zespołu nadzoru chmurowego i zainteresowanej firmy oraz udziałowców IT do przeglądania i aktualizowania zasad oraz zapewnienia zgodności z zasadami. Ponadto wiele procesów monitorowania i wymuszania można zautomatyzować lub uzupełnić narzędziem, aby zmniejszyć koszty zarządzania i umożliwić szybsze reagowanie na odchylenia zasad.

## <a name="planning-review-and-reporting-processes"></a>Planowanie, przeglądanie i raportowanie procesów

Narzędzia do zarządzania tożsamościami oferują możliwości i funkcje, które znacznie ułatwiają zarządzanie użytkownikami i kontrolę dostępu w ramach wdrożenia w chmurze. Jednak wymagają one również dobrze przemyślanych procesów i zasad, aby wspierać cele organizacji. Poniżej znajduje się zestaw przykładowych procesów, które często korzystają z dyscypliny linii bazowej tożsamości. Użyj tych przykładów jako punktu wyjścia podczas planowania procesów, które umożliwią dalszą aktualizację zasad tożsamości na podstawie zmian w firmie i informacji zwrotnych z zespołów IT z zamiarem włączenia wytycznych ładu do działania.

**Wstępna ocena ryzyka i planowanie:** W ramach początkowego wdrożenia dyscypliny linii bazowej tożsamości Zidentyfikuj podstawowe zagrożenia biznesowe i tolerancje związane z zarządzaniem tożsamościami w chmurze. Te informacje służą do omówienia określonych zagrożeń technicznych związanych z członkami zespołów IT odpowiedzialnych za zarządzanie usługami tożsamości i opracowywania bazowego zestawu zasad zabezpieczeń w celu ograniczenia tych zagrożeń w celu ustalenia początkowej strategii zarządzania.

**Planowanie wdrożenia:** Przed wdrożeniem należy przejrzeć wymagania dostępu dla wszelkich obciążeń i opracować strategię kontroli dostępu, która jest dopasowana do ustanowionych firmowych zasad tożsamości. Udokumentowanie wszelkich luk między potrzebami i bieżącymi zasadami w celu ustalenia, czy są wymagane aktualizacje zasad, i zmodyfikuj zasady w razie potrzeby.

**Testowanie wdrożenia:** W ramach wdrożenia zespół nadzorujący chmury, we współpracy z zespołami IT odpowiedzialnymi za usługi tożsamości, będzie odpowiedzialny za przeglądanie wdrożenia w celu weryfikacji zgodności z zasadami tożsamości.

**Planowanie roczne:** W skali rocznej należy przeprowadzić przegląd strategii zarządzania tożsamościami na wysokim poziomie. Przejrzyj planowane zmiany w środowisku usług tożsamości i Zaktualizowano strategie wdrażania chmury, aby zidentyfikować potencjalne zwiększenie ryzyka lub konieczność modyfikacji bieżących wzorców infrastruktury tożsamości. Użyj tego czasu, aby zapoznać się z najnowszymi najlepszymi rozwiązaniami w zakresie zarządzania tożsamościami i zintegrować je z zasadami i przeglądać procesy.

**Planowanie kwartalne:** Co kwartał przeprowadza się ogólny przegląd danych inspekcji tożsamości i kontroli dostępu, a także spotyka się z zespołami wdrażania chmury w celu zidentyfikowania potencjalnych nowych zagrożeń lub wymagań operacyjnych, które wymagają aktualizacji zasad tożsamości lub zmian w kontroli dostępu strategii.

Ten proces planowania jest również dobrym terminem do oszacowania bieżącego członkostwa zespołu nadzoru w chmurze w celu uzyskania luk w wiedzy dotyczącej nowych lub zmienionych zasad i zagrożeń związanych z tożsamościami. Zaproś odpowiednich pracowników działu IT o uczestnictwo w recenzjach i planowaniu jako tymczasowych doradców technicznych lub stałych członków zespołu.

**Edukacja i szkolenia:** Co miesiąc, oferuj sesje szkoleniowe, aby upewnić się, że personel IT i deweloperzy są aktualne zgodnie z najnowszymi wymaganiami dotyczącymi zasad dotyczących tożsamości. W ramach tego procesu zapoznaj się z dokumentacją, wskazówkami lub innymi aktywami szkoleniowymi, aby upewnić się, że są one zsynchronizowane z najnowszymi instrukcjami zasad obowiązującymi w firmie.

**Comiesięczne przeglądy audytu i raportowania:** Co miesiąc należy przeprowadzić inspekcję we wszystkich wdrożeniach w chmurze w celu zapewnienia ciągłego wyrównania przy użyciu zasad tożsamości. Ten przegląd umożliwia sprawdzenie dostępu użytkowników przed zmianami biznesowymi w celu zapewnienia, że użytkownicy mają prawidłowy dostęp do zasobów w chmurze i zapewniają spójność strategii dostępu, takich jak RBAC. Zidentyfikuj wszystkie konta uprzywilejowane i udokumentowanie ich przeznaczenia. Ten proces przeglądu powoduje utworzenie raportu dla zespołu strategii chmurowej i każdego zespołu wdrażania w chmurze, który szczegółowo określa ogólne przestrzeganie zasad. Raport jest również przechowywany na potrzeby inspekcji i przepisów prawnych.

## <a name="processes-for-ongoing-monitoring"></a>Procesy do ciągłego monitorowania

Ustalanie, czy strategia zarządzania tożsamościami jest pomyślna, zależy od widoczności bieżącego i wcześniejszego stanu systemów tożsamości. Bez możliwości analizowania odpowiednich metryk i danych związanych z wdrożeniem w chmurze nie można identyfikować zmian ryzyka ani wykrywać naruszeń tolerancji ryzyka. Bieżące procesy ładu omówione powyżej wymagają danych dotyczących jakości, aby zapewnić możliwość modyfikacji zasad w celu obsługi zmieniających się potrzeb firmy.

Upewnij się, że zespoły IT zaimplementowali zautomatyzowane systemy monitorowania dla usług tożsamości, które przechwytują dzienniki i informacje inspekcji potrzebne do oszacowania ryzyka. Można aktywnie monitorować te systemy w celu zapewnienia wykrywania monitów i łagodzenia potencjalnych naruszeń zasad oraz upewnić się, że wszelkie zmiany infrastruktury tożsamości są odzwierciedlone w strategii monitorowania.

## <a name="violation-triggers-and-enforcement-actions"></a>Wyzwalacze naruszenia i akcje wymuszania

Naruszenia zasad tożsamości mogą spowodować nieautoryzowany dostęp do poufnych danych i prowadzić do poważnej przerwy w działaniu aplikacji i usług. W przypadku wykrycia naruszeń należy podjąć akcje, aby szybko dostosować je za pomocą zasad najszybciej, jak to możliwe. Zespół IT może zautomatyzować większość wyzwalaczy naruszenia przy użyciu narzędzi opisanych w [punkcie odniesienia tożsamości łańcucha narzędzi](./toolchain.md).

Następujące wyzwalacze i akcje wymuszania zawierają przykłady, które można przywołać podczas planowania użycia danych monitorowania do rozwiązywania naruszeń zasad:

- **Wykryto podejrzane działanie:** Wykryto logowania użytkowników z anonimowych adresów IP serwera proxy, nieznane lokalizacje lub kolejne logowania z odległych lokalizacji geograficznych impossibly mogą wskazywać na potencjalne naruszenie konta lub złośliwe próby dostępu. Logowanie zostanie zablokowane do momentu zweryfikowania tożsamości użytkownika i zresetowania hasła.
- **Nieujawnione poświadczenia użytkownika:** Konta, które mają swoją nazwę użytkownika i hasło do Internetu, zostaną wyłączone do momentu zweryfikowania tożsamości użytkownika i zresetowania hasła.
- **Wykryto niewystarczającą kontrolę dostępu:** Wszelkie chronione zasoby, w przypadku których ograniczenia dostępu nie spełniają wymagań dotyczących zabezpieczeń, będą mieć zablokowany dostęp do momentu, gdy zasób nie zostanie objęty zgodnością.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu zarządzania chmurą](./template.md)można udokumentować procesy i wyzwalacze, które są wyrównane do bieżącego planu wdrożenia chmury.

Aby uzyskać wskazówki dotyczące wykonywania zasad zarządzania chmurą w wyrównaniu z planami wdrażania, zapoznaj się z artykułem dotyczącym ulepszania dyscypliny.

> [!div class="nextstepaction"]
> [Poprawa dyscypliny linii bazowej tożsamości](./discipline-improvement.md)
