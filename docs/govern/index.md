---
title: Ład w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure
description: Skorzystaj z przewodnika Cloud Adoption Framework dla platformy Azure, aby dowiedzieć się, jak oceniać istniejące zasady, tworzyć początkowe podstawy ładu oraz iteracyjnie dodawać narzędzia ładu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 37c7b219699d2d70c1f0493fbb146933f8eeee21
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218666"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Ład w przewodniku Microsoft Cloud Adoption Framework dla platformy Azure

Chmura tworzy nowe paradygmaty dotyczące technologii, które obsługują firmy. Te nowe paradygmaty zmieniają też sposób stosowania tych technologii, zarządzania nimi i nadzorowania ich. Kiedy całe centra danych można praktycznie zniszczyć, a następnie utworzyć ponownie za pomocą jednego wiersza kodu wykonanego z poziomu nienadzorowanego procesu, oznacza to, że należy przemyśleć tradycyjne podejścia. Jest to szczególnie istotne w przypadku ładu.

Nadzór nad ładem w chmurze jest procesem iteracyjnym. W przypadku organizacji z istniejącymi zasadami regulującymi lokalne środowiska IT ład chmury powinien uzupełniać te zasady. Jednak poziom integracji zasad firmowych między środowiskiem lokalnym i chmurą będzie różny w zależności od dojrzałości ładu chmury i majątku cyfrowego w chmurze. Z upływem czasu majątek w chmurze będzie się rozwijać, a wraz z nim zasady i procesy dotyczące ładu chmury. Poniższe ćwiczenia ułatwiają rozpoczęcie tworzenia początkowych podstaw ładu.

<!-- markdownlint-disable MD033 -->
<!-- docsTest:disable TODO -->

| | |
|---|---|
| ![1](../_images/icons/1.png)     | <br>[Metodologia](./methodology.md): Zbierz podstawową wiedzę na temat metodologii zapewniania ładu w chmurze w ramach przewodnika Cloud Adoption Framework i zacznij myśleć o stanie końcowym.                                |
| ![2](../_images/icons/2.png)     | <br>[Punkt odniesienia](./benchmark.md): Oceń stan bieżący i stan przyszły w celu ustalenia wizji na potrzeby stosowania struktury.                                |
| ![3](../_images/icons/3.png)     | <br>[Początkowe podstawy ładu](./initial-foundation.md): Rozpocznij stosowanie nadzoru nad ładem, używając małego, łatwego w implementacji zestawu narzędzi do nadzoru. Te początkowe podstawy ładu są nazywane minimalną konieczną funkcjonalnością (MVP).                                |
| ![4](../_images/icons/4.png)      | <br>[Udoskonalanie początkowych podstaw ładu](./foundation-improvements.md): W trakcie realizacji planu wdrażania chmury iteracyjnie dodawaj mechanizmy kontroli ładu w celu obsługi pojawiających się czynników ryzyka, zbliżając się do stanu końcowego.  |

## <a name="objective-of-this-content"></a>Cel tej zawartości

Wskazówki zawarte w tej sekcji przewodnika Cloud Adoption Framework służą dwóm celom:

- Podanie przykładów praktycznych przewodników dotyczących ładu, które reprezentują typowe doświadczenia klientów. Każdy przykład obejmuje zagadnienia związane z ryzykiem biznesowym, zasadami firmowymi umożliwiającymi ograniczenie ryzyka oraz wskazówki dotyczące projektu w celu implementacji rozwiązań technicznych. Z konieczności wskazówki dotyczące projektu są specyficzne dla platformy Azure. Pozostałą zawartość tych przewodników można stosować w podejściach niezależnych od chmury lub wielochmurowych.
- Pomoc w utworzeniu spersonalizowanych rozwiązań ładu spełniających różne potrzeby biznesowe. Te potrzeby obejmują utrzymanie ładu w wielu chmurach publicznych za pośrednictwem szczegółowych wskazówek dotyczących opracowywania zasad firmowych, procesów i narzędzi.

Ta zawartość jest przeznaczona dla zespołu ds. utrzymania ładu w chmurze. Jest również istotna dla architektów chmury, którzy muszą rozwinąć solidne podstawowe umiejętności z zakresu ładu w chmurze.

## <a name="intended-audience"></a>Docelowi odbiorcy

Zawartość przewodnika Cloud Adoption Framework dotyczy działalności biznesowej, technologii i kultury przedsiębiorstw. Ta sekcja przewodnika Cloud Adoption Framework dotyczy w szczególności zespołów ds. zabezpieczeń IT, zapewniania ładu w zasobach IT, finansów, liderów biznesowych, sieci, tożsamości i wdrożenia chmury. Różnorodne zależności między tym personelem wymagają od architektów chmury korzystających z tego przewodnika zastosowania podejścia ułatwiającego. Pomoc tym zespołom może być wysiłkiem jednorazowym. W niektórych przypadkach interakcje z innym personelem będą długotrwałe.

Architekt chmury pełni rolę lidera myśli i osoby ułatwiającej kontakt między tymi odbiorcami. Zawartość tej kolekcji przewodników ma pomóc architektowi chmury w ułatwieniu odpowiednich konwersacji z odpowiednimi odbiorcami, aby umożliwić podjęcie koniecznych decyzji. Transformacja firmy, która jest napędzana i obsługiwana przez chmurę, zależy od tego, czy architekt chmury pomoże w podejmowaniu decyzji w zakresie działalności biznesowej i IT.

**Specjalizacja architekta chmury w tej sekcji:** Każda sekcja przewodnika Cloud Adoption Framework reprezentuje różną specjalizację lub wariant roli architekta chmury. Ta sekcja przewodnika Cloud Adoption Framework jest przeznaczona dla architektów chmury pasjonujących się unikaniem lub ograniczaniem ryzyka technicznego. Niektórzy dostawcy chmury nazywają tych specjalistów _strażnikami chmury_, my jednak wolimy określenie _opiekunowie chmury_ lub zbiorczo _zespół ds. utrzymania ładu w chmurze_. Artykuły dotyczące każdego praktycznego przewodnika dotyczącego ładu pokazują, jak skład i rola zespołu ds. utrzymania ładu w chmurze może zmieniać się wraz z upływem czasu.

## <a name="use-this-guide"></a>Korzystanie z tego przewodnika

Zapoznanie się z całą treścią metodologii Ład pomoże Ci w opracowaniu niezawodnej strategii zapewnienia ładu w chmurze równolegle do wdrożenia chmury. Te wskazówki przeprowadzą Cię przez teorię i implementację takiej strategii.

Aby zapoznać się z przyspieszonym kursem teoretycznym i uzyskać szybki dostęp do implementacji platformy Azure, zacznij od [przeglądu przewodników dotyczących ładu](./guides/index.md). Dzięki tym wskazówkom możesz zacząć od czegoś małego i iteracyjnie rozwijać swoje potrzeby w zakresie utrzymania ładu równolegle do prac nad wdrożeniem chmury.
