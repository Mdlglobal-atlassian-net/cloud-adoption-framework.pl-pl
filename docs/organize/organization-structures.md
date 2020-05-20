---
title: Struktury dla dorosłych zespołów
description: Użyj tych przykładów wspólnych struktur zespołu, aby znaleźć strukturę organizacyjną, która najlepiej odpowiada Twoim potrzebom operacyjnym podczas wdrażania w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/18/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 777f89ea13c33ad5318c221d07c7c8ea3958c06c
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621444"
---
<!-- cSpell:ignore ccoe -->

# <a name="mature-team-structures"></a>Struktury dla dorosłych zespołów

Każda funkcja w chmurze jest udostępniana przez kogoś podczas każdego wysiłku związanego z wdrażaniem w chmurze. Te przydziały i struktury zespołu mogą tworzyć organiczne lub mogą być zamierzone celowo w celu dopasowania do zdefiniowanej struktury zespołu.

Zgodnie z potrzebami wdrażania, należy więc koniecznie zrównoważenie i struktura. Obejrzyj ten film wideo, aby zapoznać się z omówieniem wspólnych struktur zespołu na różnych etapach okresu ważności organizacji.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4wvTS]

Poniższa ilustracja i lista przedstawia te struktury na podstawie typowych etapów dojrzewania. Użyj tych przykładów, aby znaleźć strukturę organizacyjną, która najlepiej odpowiada Twoim potrzebom operacyjnym.

![Cykl rozwoju organizacji](../_images/ready/org-ready-maturity.png)

Struktury organizacyjne przechodzą przez wspólny model zapadalności, który jest przedstawiony tutaj:

1. [Tylko zespół wdrażania chmury](#cloud-adoption-team-only)
2. [Najlepsze rozwiązanie MVP](#best-practice-minimum-viable-product-mvp)
3. [Centralne zasoby IT](#central-it)
4. [Wyrównanie strategiczne](#strategic-alignment)
5. [Wyrównanie operacyjne](#operational-alignment)
6. [Cloud Center doskonałości (CCoE)](#cloud-center-of-excellence)

Większość firm zaczyna się od małego _zespołu wdrażania w chmurze_. Zaleca się jednak ustanowienie struktury organizacyjnej, która jest bardziej podobna do struktury najlepszego rozwiązania [MVP](#best-practice-minimum-viable-product-mvp) .

## <a name="cloud-adoption-team-only"></a>Tylko zespół wdrażania chmury

Jądrem wszystkich działań związanych z wdrażaniem w chmurze jest zespół ds. wdrażania w chmurze. Ten zespół udostępnia zmiany techniczne, które umożliwiają wdrażanie. W zależności od celów nakładu pracy ten zespół może obejmować różnorodną gamę członków zespołu, którzy obsługują szeroki zestaw zadań technicznych i służbowych.

W przypadku wysiłków dotyczących małych i wczesnych etapów ten zespół może być tak mały jako jedna osoba. W przypadku większych lub późnych wysiłków często istnieje kilka zespołów wdrażania w chmurze, z których każdy ma około sześciu inżynierów. Niezależnie od rozmiaru lub zadań, spójny aspekt dowolnego zespołu wdrażania w chmurze polega na tym, że umożliwia dołączanie rozwiązań do chmury. W przypadku niektórych organizacji może to być wystarczająca struktura organizacyjna. Artykuł z [zespołu wdrażania w chmurze](./cloud-adoption.md) zawiera dokładniejszy wgląd w strukturę, kompozycję i funkcję zespołu wdrożenia chmury.

> [!WARNING]
> Działające _tylko_ z zespołem wdrażania w chmurze (lub wieloma zespołami wdrażania w chmurze) jest uznawany za _Antywzorzec_ i należy je unikać. Należy wziąć pod uwagę co najmniej [najlepsze rozwiązanie MVP](#best-practice-minimum-viable-product-mvp).

## <a name="best-practice-minimum-viable-product-mvp"></a>Najlepsze rozwiązanie: minimalny produkt żywotny (MVP)

Zalecamy, aby dwa zespoły mogły utworzyć saldo w ramach wysiłków związanych z wdrażaniem w chmurze. Te dwa zespoły są odpowiedzialne za różne funkcje w trakcie nakładu pracy.

- **Zespół ds. wdrażania chmury:** Ten zespół jest odpowiedzialny za rozwiązania techniczne, wyrównanie biznesowe, zarządzanie projektami i operacje dla przyjętych rozwiązań.
- **Zespół ds. zarządzania chmurą:** Aby zrównoważyć zespół ds. zarządzania chmurą, zespół nadzorujący w chmurze jest przeznaczony do zapewnienia doskonałości rozwiązań, które zostały przyjęte. Zespół ds. zarządzania chmurą jest odpowiedzialny za działanie platformy, operacje na platformie, zarządzanie i automatyzację.

To sprawdzona metoda jest uważana za SPECJALISTę, ponieważ może ona nie być trwała. Każdy zespół ma wiele systemyów, jak przedstawiono na [wykresach *odpowiedzialnych* ](./raci-alignment.md), do których można się skontaktować.

W poniższych sekcjach opisano w pełni zatrudnioną strukturę organizacyjną oraz podejścia do dostosowania odpowiedniej struktury do organizacji.

## <a name="central-it"></a>Centralne zasoby IT

W miarę skalowania, zespół nadzorujący chmurę może się zadbać o to, aby zachować możliwości innowacji z wielu zespołów wdrażania chmury. Jest to szczególnie prawdziwe w środowiskach, które mają silną zgodność, operacje lub wymagania dotyczące zabezpieczeń. Na tym etapie często firma może przenieść obowiązki chmury do istniejącego centralnego zespołu IT. Jeśli ten zespół może ponownie ocenić narzędzia, procesy i osoby, aby lepiej obsługiwać wdrażanie w chmurze na dużą skalę, w tym centralny zespół IT może zwiększyć znaczącą wartość. Dostosowanie się do specjalistów z dziedziny działania, Automatyzacja, bezpieczeństwa i administrowania w celu modernizacji centralnych może zapewnić efektywne innowacje operacyjne.

Niestety, Centralna faza IT może być jedną z riskiest faz w organizacji. Centralny zespół IT musi znajdować się w tabeli o silnym wzroście sposób myślenia. Jeśli zespół przegląda chmurę jako okazję do wzrostu i adaptacji, wówczas może zapewnić doskonałą wartość w całym procesie. Jeśli jednak centralny zespół IT przegląda wdrożenie chmury przede wszystkim jako zagrożenie dla istniejącego modelu, centralny zespół IT przejdzie do przeszkody dla zespołów wdrażania chmury i celów, które są przez nie obsługiwane. Niektóre centralne zespoły IT wykorzystały miesiące, a nawet lat próbujących wymusić wymuszenie wyrównania przez chmurę przy użyciu podejścia lokalnego, z tylko negatywnymi wynikami. Chmura nie wymaga zmiany wszystkiego w Centralnym, ale wymaga znaczącej zmiany. Jeśli odporność na zmiany jest powszechnie rozpowszechniona w centralnym zespole IT, ta faza dojrzałości może szybko stać się antywzorcem kulturowym.

Plany wdrożenia chmury mocno koncentrują się na platformie jako usługa (PaaS), DevOps lub innych rozwiązania, które wymagają mniejszej liczby operacji, są mniej znaczące, aby zobaczyć wartość w tej fazie dojrzałości. W przeciwieństwie do tego typy rozwiązań są najprawdopodobniej utrudnione lub blokowane przez próby scentralizowania IT. Wyższego poziomu dojrzałości, podobnie jak w przypadku usługi [Cloud Center doskonałości (CCoE)](#cloud-center-of-excellence), najprawdopodobniej da pozytywne wyniki dla tych typów wysiłków. Aby zrozumieć różnice między centralnym działem IT w chmurze i CCoE, zobacz [Cloud Center of doskonałości](./cloud-center-of-excellence.md).

## <a name="strategic-alignment"></a>Wyrównanie strategiczne

W miarę wzrostu inwestycji w rozwiązania w chmurze i zrealizowania wartości biznesowej, zainteresowane strony biznesowe często stają się coraz bardziej zaangażowane. Zdefiniowany zespół strategii chmury, jak ilustruje poniższy obraz, wyrównuje te zainteresowane strony biznesowe, aby zmaksymalizować wartość zrealizowaną przez inwestycje z wdrażaniem w chmurze.

Gdy płatność odbywa się w sposób organiczny, w wyniku wysiłków związanych z wdrażaniem w chmurze, dostosowanie strategiczne jest zwykle poprzedzone przez rząd nadzoru lub centralny zespół IT. Gdy działania związane z wdrażaniem w chmurze są liderem firmy, fokus dotyczący modelu operacyjnego i organizacji jest zamierzony wcześniej. Tam, gdzie to możliwe, wyniki biznesowe i zespół strategii chmury powinny być zdefiniowane wczesnie w procesie.

## <a name="operational-alignment"></a>Wyrównanie operacyjne

Realizowanie wartości biznesowej z działań związanych z wdrażaniem w chmurze wymaga stabilnych operacji. Operacje w chmurze mogą wymagać nowych narzędzi, procesów lub umiejętności. Gdy stabilne operacje IT są wymagane do osiągnięcia wyników działalności biznesowej, ważne jest dodanie zdefiniowanego zespołu operacji w chmurze, jak pokazano tutaj.

Operacje w chmurze mogą być dostarczane przez istniejące role operacji IT. Nie zdarza się jednak, że operacje w chmurze są delegowane do innych stron poza operacjami IT. Dostawcy usług zarządzanych, zespoły DevOps i jednostka biznesowa często zakładają obowiązki związane z operacjami w chmurze, z obsługą i guardrails udostępnianymi przez operacje IT. Jest to coraz częściej popularne w przypadku działań związanych z wdrażaniem w chmurze, które koncentrują się mocno na wdrożeniach DevOps lub PaaS

## <a name="cloud-center-of-excellence"></a>Centrum doskonałości chmury

W przypadku najwyższego stanu zapadalności Centrum rozwiązań w chmurze pozwala wyrównać zespoły do nowoczesnego modelu operacyjnego w chmurze. Takie podejście zapewnia centralne funkcje IT, takie jak ładu, zabezpieczenia, platforma i Automatyzacja.

Podstawowa różnica między tą strukturą a centralną strukturą IT jest skoncentrowana na samoobsługi. Zespoły w tej strukturze organizują z zamiarem delegowania kontroli tak dużo, jak to możliwe. Dostosowanie praktyk zarządzania i zgodności do rozwiązań natywnych w chmurze tworzy mechanizmy guardrails i ochrony. W przeciwieństwie do centralnego modelu IT podejście natywne w chmurze maksymalizuje innowacje i minimalizuje obciążenie operacyjne. Aby ten model został przyjęty, firma i jej Liderzy muszą wzajemnie porozumienie o modernizacji procesów IT. Ten model jest mało prawdopodobny i często wymaga wsparcia Executive.

## <a name="next-steps"></a>Następne kroki

Po dopasowaniu do pewnego etapu dojrzałości struktury organizacyjnej można użyć [wykresów Raci](./raci-alignment.md) do dopasowania odpowiedzialności i odpowiedzialności za każdy zespół.

> [!div class="nextstepaction"]
> [Dopasuj odpowiedni wykres RACI](./raci-alignment.md)
