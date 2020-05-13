---
title: Motywacje i ryzyko biznesowe w dyscyplinie spójności zasobów
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać Typowe wdrożenie klienta dyscypliny spójności zasobów w ramach strategii nadzoru chmurowego.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 17b39eba50b11ee1124e174f3bc89f3e6dada3e2
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218258"
---
# <a name="motivations-and-business-risks-in-the-resource-consistency-discipline"></a>Motywacje i ryzyko biznesowe w dyscyplinie spójności zasobów

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę spójności zasobów w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów potencjalnego ryzyka biznesowego, które mogą być dyskowymi instrukcjami zasad.

<!-- markdownlint-disable MD026 -->

## <a name="relevance"></a>Trafność

Gdy chodzi o wdrażanie zasobów i obciążeń, Chmura zapewnia zwiększoną elastyczność i elastyczność w porównaniu z najbardziej tradycyjnymi lokalnymi centrami danych. Jednak te zalety oparte na chmurze również są sparowane z potencjalnymi wadą zarządzania, które mogą poważnie zagrozić sukcesem wdrożenia chmury. Jakie zasoby zostały wdrożone? Jakie zespoły są właścicielami zasobów? Czy masz wystarczającą ilość zasobów obsługujących obciążenie? Jak wiadomo, czy obciążenia są w dobrej kondycji?

Spójność zasobów jest niezwykle istotna, aby zapewnić, że zasoby są wdrażane, aktualizowane i konfigurowane spójnie w sposób powtarzalny, a przerwy w działaniu usługi są zminimalizowane i nieznacznie zagwarantowane.

Dyscyplina spójności zasobów jest zaangażowana w identyfikowanie i łagodzenie ryzyka biznesowego związanego z aspektami operacyjnymi wdrożenia w chmurze. Spójność zasobów obejmuje monitorowanie aplikacji, obciążeń i wydajności zasobów. Zawiera również zadania wymagane do spełnienia wymagań dotyczących skalowania, zapewniania możliwości odzyskiwania po awarii, łagodzenia naruszeń umów dotyczących poziomu usług (SLA) dotyczących wydajności i aktywnego uniknięcia naruszeń umów SLA poprzez automatyczne korygowanie.

Początkowe wdrożenia testów mogą nie wymagać znacznie więcej niż przyjmuje pewne nazewnictwo kursorów i standardy tagowania, aby zapewnić obsługę spójności zasobów. W miarę dojrzewania rozwiązań w chmurze i wdrażaniu bardziej skomplikowanych i krytycznych zasobów należy zainwestować w dyscyplinę spójności zasobów szybko.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina spójności zasobów próbuje rozwiązać podstawowe operacyjne działania biznesowe. Pracuj z firmą i zespołami IT, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i wdrażania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe czynniki ryzyka, których można użyć jako punktu wyjścia dla dyskusji w zespole ładu chmury:

- **Niezbędny koszt operacyjny.** Przestarzałe lub nieużywane zasoby lub zasoby, które są nadmiernie przydzielane w czasie niskiego popytu, Dodaj niepotrzebne koszty operacyjne.
- **Nieudostępniane zasoby.** Zasoby, które są większe niż przewidywane zapotrzebowanie, mogą spowodować zakłócenia działania firmy, ponieważ zasoby chmury są przeciążone na żądanie.
- **Nieefektywność zarządzania.** Brak spójnego nazewnictwa i metadanych tagowania skojarzonych z zasobami może prowadzić do pracowników działu IT, którzy mają trudności z wyszukiwaniem zasobów dla zadań zarządzania lub identyfikowaniem własności i informacjami księgowymi związanymi z zasobami. Powoduje to nieefektywność zarządzania, które może zwiększyć koszt i spowalniać czas odpowiedzi usługi lub inne problemy operacyjne.
- **Zakłócenia biznesowe.** Przerwy w działaniu usługi, które powodują naruszenia umów dotyczących poziomu usług (umowy SLA) obowiązujących w organizacji, mogą spowodować utratę firmy lub innych wpływów finansowych na firmę.

## <a name="next-steps"></a>Następne kroki

Za pomocą [szablonu dyscypliny spójności zasobów](./template.md) można udokumentować ryzyko biznesowe, które mogą zostać wprowadzone przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
