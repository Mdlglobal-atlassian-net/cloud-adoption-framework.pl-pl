---
title: Ryzyko biznesowe spójności zasobów
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby poznać Typowe wdrożenie klienta dyscypliny spójności zasobów w ramach strategii nadzoru chmurowego.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3eff0f6130adc35d8c087d385d42b06e141f3c64
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80433495"
---
# <a name="resource-consistency-motivations-and-business-risks"></a>Motywacje spójności zasobów i ryzyko biznesowe

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują dyscyplinę spójności zasobów w ramach strategii zarządzania chmurą. Zawiera również kilka przykładów potencjalnego ryzyka biznesowego, które mogą być dyskowymi instrukcjami zasad.

<!-- markdownlint-disable MD026 -->

## <a name="resource-consistency-relevancy"></a>Dokładność spójności zasobów

Gdy chodzi o wdrażanie zasobów i obciążeń, Chmura zapewnia zwiększoną elastyczność i elastyczność w porównaniu z najbardziej tradycyjnymi lokalnymi centrami danych. Jednak te zalety oparte na chmurze również są sparowane z potencjalnymi wadą zarządzania, które mogą poważnie zagrozić sukcesem wdrożenia chmury. Jakie zasoby zostały wdrożone? Jakie zespoły są właścicielami zasobów? Czy masz wystarczającą ilość zasobów obsługujących obciążenie? Jak wiadomo, czy obciążenia są w dobrej kondycji?

Spójność zasobów jest niezwykle istotna, aby zapewnić, że zasoby są wdrażane, aktualizowane i konfigurowane spójnie w sposób powtarzalny, a przerwy w działaniu usługi są zminimalizowane i nieznacznie zagwarantowane.

Dyscyplina spójności zasobów jest zaangażowana w identyfikowanie i łagodzenie ryzyka biznesowego związanego z aspektami operacyjnymi wdrożenia w chmurze. Spójność zasobów obejmuje monitorowanie aplikacji, obciążeń i wydajności zasobów. Zawiera również zadania wymagane do spełnienia wymagań dotyczących skalowania, zapewnienia możliwości odzyskiwania po awarii, łagodzenia naruszeń wydajności Umowa dotycząca poziomu usług (SLA) i aktywnie unikania naruszeń umów SLA poprzez automatyczne korygowanie.

Początkowe wdrożenia testów mogą nie wymagać znacznie więcej niż przyjmuje pewne nazewnictwo kursorów i standardy tagowania, aby zapewnić obsługę spójności zasobów. W miarę dojrzewania rozwiązań w chmurze i wdrażaniu bardziej skomplikowanych i krytycznych zasobów należy zainwestować w dyscyplinę spójności zasobów szybko.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina spójności zasobów próbuje rozwiązać podstawowe operacyjne działania biznesowe. Pracuj z firmą i zespołami IT, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i wdrażania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe czynniki ryzyka, których można użyć jako punktu wyjścia dla dyskusji w zespole ładu chmury:

- **Niezbędny koszt operacyjny.** Przestarzałe lub nieużywane zasoby lub zasoby, które są nadmiernie przydzielane w czasie niskiego popytu, Dodaj niepotrzebne koszty operacyjne.
- **Nieudostępniane zasoby.** Zasoby, które są większe niż przewidywane zapotrzebowanie, mogą spowodować zakłócenia działania firmy, ponieważ zasoby chmury są przeciążone na żądanie.
- **Nieefektywność zarządzania.** Brak spójnego nazewnictwa i metadanych tagowania skojarzonych z zasobami może prowadzić do pracowników działu IT, którzy mają trudności z wyszukiwaniem zasobów dla zadań zarządzania lub identyfikowaniem własności i informacjami księgowymi związanymi z zasobami. Powoduje to nieefektywność zarządzania, które może zwiększyć koszt i spowalniać czas odpowiedzi usługi lub inne problemy operacyjne.
- **Zakłócenia biznesowe.** Przerwy w działaniu usługi, które powodują naruszenia umów dotyczących poziomu usług (umowy SLA) obowiązujących w organizacji, mogą skutkować utratą działalności lub innymi wpływami finansowymi firmy.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), dokumentuj ryzyka biznesowego, które mogą być wprowadzane przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
