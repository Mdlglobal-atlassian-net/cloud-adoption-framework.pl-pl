---
title: Przygotowywanie firmowych zasad IT pod kątem chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie pojęcia zasad firmowych w odniesieniu do ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e86eb3408b635eac7c299ae594999ddf619ab81e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816792"
---
<!-- markdownlint-disable MD026 -->

# <a name="prepare-corporate-it-policy-for-the-cloud"></a>Przygotowywanie firmowych zasad IT pod kątem chmury

Ład w chmurze to wynik trwającego dłuższy czas wdrażania, ponieważ naprawdę trwała transformacja nie dokonuje się w ciągu jednego dnia. Próba zapewnienia kompletnego ładu w chmurze za pomocą szybkiej i agresywnej metody przed przeprowadzeniem kluczowych zmian zasad firmy rzadko daje oczekiwane wyniki. Zamiast tego zaleca się wprowadzanie przyrostowych zmian.

Elementami, dzięki którym wyróżnia się nasz przewodnik Cloud Adoption Framework, są cykl zakupu i sposób, w jaki umożliwia on autentyczną transformację. Ponieważ nie jest wymagane pozyskiwanie dużych nakładów inwestycyjnych, inżynierowie mogą wcześniej rozpocząć eksperymentowanie i wdrażanie. W większości firm wyeliminowanie we wdrażaniu bariery wydatków inwestycyjnych może prowadzić do szybszego generowania informacji zwrotnych, organicznego rozwoju i wykonywania przyrostowego.

Przejście do wdrażania w chmurze wymaga przejścia na wyższy poziom w zapewnianiu ładu. W wielu organizacjach przekształcenia zasad firmowych poprawiają ład i zwiększają stopień zgodności za pośrednictwem przyrostowych zmian zasad i zautomatyzowanego stosowania tych zmian. Takie zachowania można skonfigurować za pomocą nowo zdefiniowanych możliwości u dostawcy usług w chmurze.

W tym artykule opisano kluczowe działania, które mogą pomóc w kształtowaniu zasad firmowych w celu włączenia rozszerzonego modelu ładu.

## <a name="define-corporate-policy-to-mature-cloud-governance"></a>Definiowanie zasad firmowych zapewniających ustabilizowany ład w chmurze

Zarówno w tradycyjnym, jak i w przyrostowym modelu zapewniania ładu zasady firmowe tworzą roboczą definicję ładu. Większość akcji podejmowanych w celu zapewnienia ładu IT koncentruje się na implementowaniu technologii w celu monitorowania, wymuszania, obsługiwania i automatyzowania tych zasad firmowych. Ład w chmurze jest oparty na podobnych pojęciach.

![Ład korporacyjny i dyscypliny ładu](../../_images/operational-transformation-govern-highres.png)

*Rysunek 1 — ład korporacyjny i dyscypliny ładu.*

Na powyższej ilustracji pokazano interakcje występujące między ryzykiem biznesowym, zasadami i zgodnością, monitorowaniem oraz wymuszaniem prowadzące do utworzenia strategii ładu. Niżej przedstawiono pięć dyscyplin zapewniających ład w chmurze i zrealizowanie strategii.

## <a name="review-existing-policies"></a>Przegląd istniejących zasad

Na powyższej ilustracji strategia utrzymywania ładu (ryzyko, zasady i zgodność, monitorowanie i wymuszanie) rozpoczyna się od rozpoznania czynników ryzyka biznesowego. Zrozumienie sposobu, w jaki [ryzyko biznesowe](understanding-business-risk.md) zmienia się w chmurze, jest pierwszym krokiem do tworzenia długotrwałej strategii utrzymania ładu w chmurze. Praca z jednostkami biznesowymi w celu opracowania dokładnego [miernika tolerancji na ryzyko w biznesie](risk-tolerance.md) pomaga zrozumieć, jaki jest poziom ryzyka, któremu należy przeciwdziałać. Zrozumienie nowych czynników ryzyka i akceptowalnego poziomu ich tolerowania może skłonić do [przejrzenia istniejących zasad](what-is-a-cloud-policy-review.md) w celu określenia wymaganego poziomu ładu, odpowiedniego dla Twojej organizacji.

> [!TIP]
> Jeśli Twoja organizacja jest zarządzana według przepisów obowiązujących w innej firmie, jednym z największych czynników ryzyka biznesowego, jakie należy wziąć pod uwagę, może być ryzyko zapewnienia [zgodności z przepisami](what-is-regulatory-compliance.md). Takiemu ryzyku często nie można przeciwdziałać, a jedynym wyjściem może być zapewnienie ścisłej zgodności. Przed rozpoczęciem przeglądu zasad należy dokładnie zapoznać się z wymaganiami dotyczącymi zgodności z przepisami innej firmy.

## <a name="an-incremental-approach-to-cloud-governance"></a>Przyrostowy model utrzymania ładu w chmurze

W modelu przyrostowym utrzymania ładu w chmurze przyjmuje się założenie, że nie jest akceptowalne przekroczenie [tolerancji biznesowej na ryzyko](risk-tolerance.md). Zamiast tego przyjmuje się, że rolą utrzymania ładu jest przyspieszenie wprowadzania zmian w firmie, pomoc inżynierom w zrozumieniu wytycznych dotyczących architektury i upewnienie się, że [czynniki ryzyka biznesowego](understanding-business-risk.md) są regularnie monitorowane i korygowane. Z drugiej strony tradycyjna rola utrzymania ładu może stanowić dla inżynierów lub dla całej firmy barierę przed wdrażaniem.

W przyrostowym modelu utrzymania ładu w chmurze występuje czasami naturalna różnica zdań między zespołami tworzącymi nowe rozwiązania biznesowe i zespołami zabezpieczającymi firmę przed czynnikami ryzyka. Jednak w tym modelu te dwa zespoły mogą stać się równorzędnymi partnerami pracującymi w przyrostach lub przebiegach. Jako równorzędni partnerzy, zespół ds. ładu w chmurze i zespoły ds. wdrożeń w chmurze rozpoczynają razem pracę, aby ujawnić i ocenić czynniki ryzyka oraz znaleźć sposób radzenia sobie z nimi. Skoncentrowanie się na wspólnym celu może zmniejszyć różnice zdań między zespołami i doprowadzić do współpracy między nimi.

## <a name="minimum-viable-product-mvp-for-policy"></a>Minimalna konieczna funkcjonalność (MVP) dla zasad

Pierwszym etapem budowania partnerstwa między zespołami ds. ładu w chmurze i wdrażania jest zawarcie umowy dotyczącej minimalnej koniecznej funkcjonalności dla zasad. Minimalna konieczna funkcjonalność ładu w chmurze powinna zakładać, że czynniki ryzyka biznesowego są na początku niewielkie, ale prawdopodobnie będą się zwiększały wraz z wdrażaniem coraz większej liczby usług w chmurze.

Na przykład ryzyko biznesowe jest małe w przypadku firmy wdrażającej pięć maszyn wirtualnych, które nie zawierają żadnych danych o wysokim znaczeniu dla jej działalności. W dalszym etapie procesu wdrażania w chmurze, kiedy liczba maszyn wirtualnych osiągnie 1000 i firma zaczyna przenosić do nich dane o wysokim znaczeniu, rośnie ryzyko biznesowe.

Minimalna konieczna funkcjonalność zasad próbuje zdefiniować podstawy zasad niezbędne do wdrożenia pierwszych _x_ maszyn wirtualnych lub pierwszych _x_ aplikacji, gdzie _x_ to jeszcze niewielka liczba wdrażanych jednostek. Ten zestaw zasad wymaga kilku ograniczeń, ale będzie zawierać podstawowe elementy potrzebne do szybkiego przejścia z jednego poziomu przyrostowego wdrażania w chmurze do następnego. Dzięki opracowaniu przyrostowych zasad strategia utrzymania ładu będzie rozszerzać się wraz z upływem czasu. Dzięki takim małym zmianom minimalna konieczna funkcjonalność zasad rozwinie się w równoważność funkcji, na co wpływ będą miały wyniki ćwiczenia przeglądu zasad.

## <a name="incremental-policy-growth"></a>Przyrostowe rozszerzanie się zasad

Przyrostowe rozszerzanie się zasad to kluczowy mechanizm rozszerzania się zasad i zwiększania ładu w chmurze wraz z upływem czasu. Jest również kluczowym wymaganiem umożliwiającym wdrażanie przyrostowego modelu utrzymania ładu. Aby ten model działał sprawnie, zespół ds. utrzymania ładu musi dbać o nadchodzące alokacje czasu w każdym przebiegu, aby móc ocenić i zaimplementować zmieniające się dyscypliny ładu.

**Wymagania dotyczące czasu przebiegu:** Na początku każdej iteracji poszczególne zespoły ds. wdrażania w chmurze tworzą listę zasobów, które mają zostać zmigrowane lub wdrożone w bieżącym przyroście. Zespół ds. utrzymania ładu w chmurze powinien mieć wystarczająco dużo czasu na przejrzenie tej listy, zweryfikowanie klasyfikacji danych dla zasobów, ocenienie wszelkich nowych czynników ryzyka skojarzonych z każdym zasobem, zaktualizowanie wskazówek dotyczących architektury i poinformowanie członków zespołu o zmianach. Te czynności zajmują zwykle od 10 do 30 godzin dla każdego przebiegu. Na tym poziomie zaangażowania powinien zostać również wyznaczony co najmniej jeden pracownik zajmujący się wyłącznie zarządzaniem ładem podczas tego dużego projektu wdrażania w chmurze.

**Wymagania dotyczące czasu wydania:** Na początku każdego wydania zespoły ds. wdrażania w chmurze oraz zespół ds. strategii w chmurze powinny określić priorytety listy aplikacji lub obciążeń, które mają zostać zmigrowane w bieżącej iteracji, a także priorytety działań dotyczących zmian w firmie. Te punkty danych umożliwią zespołowi ds. utrzymania ładu w chmurze wczesne rozpoznanie nowych czynników ryzyka biznesowego. Dzięki temu będzie można w odpowiednim czasie wprowadzić zmiany w firmie i zmierzyć tolerancję na ryzyko w biznesie.

## <a name="next-steps"></a>Następne kroki

Podstawą skutecznych strategii zarządzania chmurą jest zrozumienie ryzyka biznesowego.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./understanding-business-risk.md)
