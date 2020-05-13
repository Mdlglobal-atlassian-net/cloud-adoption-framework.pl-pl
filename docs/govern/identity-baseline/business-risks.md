---
title: Motywacje i ryzyko biznesowe w dyscyplinie linii bazowej tożsamości
description: Zapoznaj się z przykładami typowych rozwiązań dla klientów w ramach strategii nadzoru chmurowego.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 370dfa7a040a41e22f23741ca30cf3a305de7f29
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219890"
---
# <a name="motivations-and-business-risks-in-the-identity-baseline-discipline"></a>Motywacje i ryzyko biznesowe w dyscyplinie linii bazowej tożsamości

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę bazową tożsamości w ramach strategii nadzoru chmurowego. Zawiera również kilka przykładów ryzyka biznesowego, które dotyczą instrukcji zasad.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Trafność

Tradycyjne katalogi lokalne zostały zaprojektowane tak, aby umożliwić firmom ścisłą kontrolę uprawnień i zasad dla użytkowników, grup i ról w swoich sieciach wewnętrznych i centrach danych. Te katalogi zazwyczaj obsługują implementacje z jedną dzierżawą, z usługami mającymi zastosowanie tylko w środowisku lokalnym.

Usługi tożsamości w chmurze rozszerzają możliwości uwierzytelniania i kontroli dostępu w organizacji do Internetu. Obsługują one Wielodostępność i mogą służyć do zarządzania użytkownikami i zasadami dostępu w aplikacjach i wdrożeniach w chmurze. Platformy chmury publicznej mają natywne usługi tożsamości obsługujące zadania związane z zarządzaniem i wdrażaniem oraz mogą mieć [różne poziomy integracji](../../decision-guides/identity/index.md) z istniejącymi lokalnymi rozwiązaniami do obsługi tożsamości. Wszystkie te funkcje mogą spowodować, że zasady tożsamości w chmurze są bardziej skomplikowane niż wymagania dotyczące tradycyjnych rozwiązań lokalnych.

Znaczenie planu bazowego tożsamości dla wdrożenia w chmurze będzie zależeć od wielkości zespołu i konieczności zintegrowania rozwiązania do obsługi tożsamości opartej na chmurze z istniejącą lokalną usługą tożsamości. Początkowe wdrożenia testów mogą nie wymagać wielu działań w zakresie organizacji użytkownika ani zarządzania nimi, ale w miarę dojrzałości w chmurze, prawdopodobnie trzeba będzie obsługiwać bardziej skomplikowaną integrację organizacji i scentralizowane zarządzanie.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina linii bazowej tożsamości próbuje rozwiązać podstawowe zagrożenia biznesowe związane z usługami tożsamości i kontrolą dostępu. Pracuj z firmą, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i implementowania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe zagrożenia związane z tożsamościami, których można użyć jako punktu wyjścia dla dyskusji w zespole ładu chmury:

- **Nieautoryzowany dostęp.** Poufne dane i zasoby, do których mogą uzyskiwać dostęp nieautoryzowani użytkownicy, mogą prowadzić do przecieków danych lub przerw w działaniu usługi, naruszają granice bezpieczeństwa organizacji i narażają zobowiązania biznesowe lub prawne.
- **Brak efektywności ze względu na wiele rozwiązań w zakresie tożsamości.** Organizacje z wieloma dzierżawcami usługi Identity Services mogą wymagać wielu kont dla użytkowników. Może to prowadzić do nieefektywności dla użytkowników, którzy muszą pamiętać wiele zestawów poświadczeń oraz do zarządzania kontami w wielu systemach. Jeśli przypisania dostępu użytkowników nie są aktualizowane w ramach rozwiązań tożsamości jako personel, zespoły i cele biznesowe, zasoby w chmurze mogą być narażone na nieautoryzowany dostęp lub użytkownicy nie mogą uzyskać dostępu do wymaganych zasobów.
- **Brak możliwości udostępniania zasobów partnerom zewnętrznym.** Trudności z dodawaniem zewnętrznych partnerów firmy do istniejących rozwiązań do obsługi tożsamości mogą uniemożliwić wydajne udostępnianie zasobów i komunikację biznesową.
- **Lokalne zależności tożsamości.** Starsze mechanizmy uwierzytelniania lub uwierzytelnianie wieloskładnikowe innej firmy mogą nie być dostępne w chmurze, co wymaga przetestowania obciążeń lub dodatkowych usług tożsamości do wdrożenia w chmurze. Wymaganie może opóźnić się lub zapobiec migracji oraz zwiększyć koszty.

## <a name="next-steps"></a>Następne kroki

[Szablon dyscypliny linii bazowej tożsamości](./template.md) służy do dokumentowania ryzyka biznesowego, które mogą być wprowadzane przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
