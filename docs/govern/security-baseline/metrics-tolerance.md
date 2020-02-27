---
title: Metryki i wskaźniki tolerancji ryzyka dla linii bazowej zabezpieczeń
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak określić tolerancję ryzyka biznesowego związanego z linią bazową zabezpieczeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5f85fd62f78b3be30faab452f12113790e6455d8
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "77707343"
---
# <a name="security-baseline-metrics-indicators-and-risk-tolerance"></a>Metryki linii bazowej zabezpieczeń, wskaźniki i tolerancja ryzyka

Ten artykuł pomoże Ci określić tolerancję ryzyka biznesowego, która odnosi się do linii bazowej zabezpieczeń. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy na potrzeby inwestycji w wykupu dyscypliny linii bazowej zabezpieczeń.

## <a name="metrics"></a>Metryki

Linia bazowa zabezpieczeń zwykle koncentruje się na identyfikowaniu potencjalnych luk w zabezpieczeniach wdrożeń w chmurze. W ramach analizy ryzyka warto zebrać dane związane ze środowiskiem zabezpieczeń, aby określić, jak ryzyko ma stanowić zagrożenie, oraz jak ważne inwestycje w zarządzanie odniesieniami w firmie podlegają planowanym wdrożeniom w chmurze.

Każda organizacja ma inne środowiska i wymagania dotyczące zabezpieczeń oraz różne potencjalne źródła danych zabezpieczeń. Poniżej przedstawiono przykłady przydatnych metryk, które należy zebrać, aby pomóc w ocenie tolerancji ryzyka w ramach dyscypliny linii bazowej zabezpieczeń:

- **Klasyfikacja danych:** Liczba przechowywanych w chmurze danych i usług, które są niesklasyfikowane zgodnie z zasadami zachowania poufności, zgodności lub wpływów obowiązujących w organizacji.
- **Liczba poufnych magazynów danych:** Liczba punktów końcowych magazynu lub baz danych zawierających dane poufne i powinna być chroniona.
- **Liczba niezaszyfrowanych magazynów danych:** Liczba poufnych magazynów danych, które nie są zaszyfrowane.
- Obszar narażony na **ataki:** Ile łącznych źródeł danych, usług i aplikacji będzie hostowanych w chmurze. Jaki procent tych źródeł danych jest klasyfikowany jako poufne? Jaki procent tych aplikacji i usług jest krytyczny dla działalności?
- **Normy omówione:** Liczba standardów zabezpieczeń zdefiniowanych przez zespół ds. zabezpieczeń.
- **Zasoby objęte usługą:** Wdrożone zasoby, które są objęte standardami zabezpieczeń.
- **Zgodność ze standardami ogólnymi:** Stosunek zgodności przestrzegania standardów zabezpieczeń.
- **Ataki według ważności:** Ile koordynowanych prób zakłócania usług hostowanych w chmurze, na przykład ataków rozproszonego typu "odmowa usługi" (DDoS), czy środowisko infrastruktury? Jaki jest rozmiar i ważność tych ataków?
- **Ochrona przed złośliwym oprogramowaniem:** Procent wdrożonych maszyn wirtualnych, dla których zainstalowano wszystkie wymagane oprogramowanie chroniące przed złośliwym oprogramowaniem, zaporą lub innym oprogramowaniem zabezpieczającym.
- **Opóźnienie poprawek:** Jak długo została zastosowana poprawka systemu operacyjnego i oprogramowania dla maszyn wirtualnych.
- **Zalecenia dotyczące kondycji zabezpieczeń:** Liczba zaleceń dotyczących oprogramowania zabezpieczającego, które rozwiązują standardy kondycji wdrożonych zasobów uporządkowane według ważności.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

Platformy w chmurze oferują podstawowy zestaw funkcji umożliwiających małym zespołom wdrażania Konfigurowanie podstawowych ustawień zabezpieczeń bez konieczności dodatkowego planowania. W związku z tym małe zadania deweloperskie/testowe lub eksperymentalne, które nie obejmują danych poufnych, reprezentują stosunkowo niski poziom ryzyka i prawdopodobnie nie będą potrzebne wiele w sposób formalnych zasad dotyczących zabezpieczeń. Jednak, gdy tylko ważne dane lub funkcje o kluczowym znaczeniu są przenoszone do chmury, zwiększa się ryzyko bezpieczeństwa, natomiast tolerancja dla tego ryzyka zmniejsza się szybko. Coraz więcej danych i funkcji jest wdrażanych w chmurze, tym bardziej prawdopodobnie potrzebna jest zwiększona inwestycja w dyscyplinę bazową zabezpieczeń.

We wczesnych etapach wdrażania chmury Pracuj z zespołem ds. zabezpieczeń IT i zainteresowanymi stronami biznesowymi, aby identyfikować [zagrożenia biznesowe](./business-risks.md) związane z bezpieczeństwem, a następnie określić akceptowalną podstawę do odporności na zagrożenia bezpieczeństwa. W tej części struktury wdrażania w chmurze przedstawiono przykłady, ale szczegóły dotyczące zagrożeń i linii bazowych dla firmy lub wdrożeń mogą się różnić.

Po utworzeniu planu bazowego należy ustanowić minimalne wzorce reprezentujące nieakceptowalny wzrost w zidentyfikowanych zagrożeniach. Te progi działają jako Wyzwalacze w przypadku, gdy konieczne jest podjęcie działań w celu skorygowania tych zagrożeń. Poniżej przedstawiono kilka przykładów sposobu, w jaki metryki zabezpieczeń, takie jak omówione powyżej, mogą uzasadniać zwiększenie inwestycji w dyscypliny linii bazowej zabezpieczeń.

- **Wyzwalacz obciążeń o kluczowym znaczeniu.** Firma wdraża obciążenia o kluczowym znaczeniu dla chmury, które powinny inwestować w dyscyplinę bazową zabezpieczeń, aby zapobiec potencjalnemu zakłóceniom w zakresie usług lub wrażliwych danych.
- **Wyzwalacz chronionych danych.** Dane hostingowe firmy w chmurze, które mogą być klasyfikowane jako poufne, prywatne lub w inny sposób związane z przepisami. Muszą one mieć dyscyplinę bazową zabezpieczeń, aby zapewnić, że te dane nie podlegają utracie, narażeniu lub kradzieżie.
- **Wyzwalacz ataków zewnętrznych.** Firma, która napotyka poważne ataki na infrastrukturę sieci _x_ razy w miesiącu, może skorzystać z dyscypliny linii bazowej zabezpieczeń.
- **Wyzwalacz zgodności ze standardami.** Firma mająca więcej niż _x%_ zasobów poza zgodnością ze standardami bezpieczeństwa powinna inwestować w dyscyplinę bazową zabezpieczeń w celu zapewnienia spójnego stosowania standardów w infrastrukturze IT.
- **Wyzwalacz rozmiaru nieruchomości w chmurze.** Firma hostującym więcej niż _x_ aplikacji, usług lub źródeł danych. Duże wdrożenia w chmurze mogą korzystać z inwestycji w dyscypliny linii bazowej zabezpieczeń, aby zapewnić, że ich ogólna powierzchnia ataku jest odpowiednio chroniona przed nieautoryzowanym dostępem lub innymi zagrożeniami zewnętrznymi.
- **Wyzwalacz zgodności oprogramowania zabezpieczającego.** Firma, w której jest mniej niż _x%_ wdrożonych maszyn wirtualnych, ma zainstalowane wymagane oprogramowanie zabezpieczające. Dyscypliny linii bazowej zabezpieczeń można użyć do zapewnienia spójnego instalowania oprogramowania na całym oprogramowaniu.
- **Wywoływanie wyzwalacza.** Firma, w której wdrożono maszyny wirtualne lub usługi, w ciągu ostatnich _x_ dni nie zastosowano poprawek systemu operacyjnego lub oprogramowania. Dyscypliny linii bazowej zabezpieczeń można użyć w celu zapewnienia aktualności poprawek w wymaganym harmonogramie.
- **Ukierunkowane na zabezpieczenia.** Niektóre firmy będą mieć rygorystyczne wymagania dotyczące zabezpieczeń i poufności danych nawet w przypadku obciążeń testowych i eksperymentalnych. Te firmy będą musiały inwestować w dyscyplinę bazową zabezpieczeń przed rozpoczęciem wdrażania.

Dokładne metryki i wyzwalacze używane do oceny tolerancji ryzyka i poziom inwestycji w dyscypliny linii bazowej zabezpieczeń będą specyficzne dla organizacji, ale powyższe przykłady powinny służyć jako przydatny dla dyskusji w zespole nadzoru chmurowego.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), metryk dokumentu i wskaźniki tolerancji, które są wyrównane do bieżącego planu wdrożenia chmury.

Zapoznaj się z przykładowymi zasadami odniesienia zabezpieczeń jako punkt wyjścia do opracowania zasad, które wiążą się z konkretnymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania chmury.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
