---
title: 'Motywacje: Dlaczego przenosimy do chmury?'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ewidencjonowanie aktywności w chmurze i przechodzenie do chmury
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 65ef12ca476ca624ae1e71cce2e62d41141873a9
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561606"
---
<!-- markdownlint-disable MD026 -->

# <a name="motivations-why-are-we-moving-to-the-cloud"></a>Motywacje: Dlaczego przenosimy do chmury?

"Dlaczego przenosimy do chmury?" jest wspólnym pytaniem dotyczącym interesów firmowych i technicznych. Jeśli odpowiedź to "nasz zespół (lub CIO lub kierowników na poziomie C") poinformuje nas o przejściu do chmury, "jest mało prawdopodobne, że firma osiągnie odpowiednie wyniki.

W tym artykule omówiono kilka przyczyn migracji do chmury, które mogą pomóc w wykorzystaniu bardziej pomyślnych wyników firmy. Te opcje ułatwiają konwersację na temat motywacji i, a ostatecznie wyniki biznesowe.

## <a name="motivations"></a>Przesłanki

Przekształcenia biznesowe obsługiwane przez wdrożenie chmury mogą być zależne od różnych motywacji. Istnieje duże ryzyko, że w tym samym czasie mają zastosowanie kilka motywacji. Celem list w poniższej tabeli jest ułatwienie dla platformy Spark koncepcji, które są istotne. Z tego miejsca można ustalić priorytety i oceniać potencjalne wpływ motywacji. W tym artykule zalecamy, aby zespół rozwiązań w chmurze spełniał różne kierownictwo i liderzy biznesowi, korzystając z poniższej listy, aby zrozumieć, które z tych motywacji wpływają na działania związane z wdrażaniem chmury.

<!-- markdownlint-disable MD033 -->

| Krytyczne zdarzenia biznesowe | Migracja | Innowacja |
|---|---|---|
| Wyjście centrum danych<br/><br/>Fuzja, pozyskiwanie lub zbycie<br/><br/>Zmniejszenie wydatków inwestycyjnych<br/><br/>Koniec wsparcia dla technologii o kluczowym znaczeniu<br/><br/>Odpowiedź na zmiany zgodności z przepisami<br/><br/>Nowe wymagania dotyczące suwerenności danych<br/><br/>Zmniejszenie przerw w działaniu i poprawa stabilności IT | Redukcja kosztów<br/><br/>Zmniejszenie liczby dostawców lub technicznych<br/><br/>Optymalizacja operacji wewnętrznych<br/><br/>Zwiększ elastyczność biznesową<br/><br/>Przygotowanie do nowych możliwości technicznych<br/><br/>Skalowanie w celu spełnienia wymagań dotyczących rynku<br/><br/>Skalowanie w celu spełnienia wymagań geograficznych | Przygotowanie do nowych możliwości technicznych<br/><br/>Tworzenie nowych możliwości technicznych<br/><br/>Skalowanie w celu spełnienia wymagań dotyczących rynku<br/><br/>Skalowanie w celu spełnienia wymagań geograficznych<br/><br/>Udoskonalone doświadczenia i zaangażowanie klientów<br/><br/>Przekształcanie produktów lub usług<br/><br/>Zakłócenia rynku dzięki nowym produktom lub usługom |

## <a name="classify-your-motivations"></a>Klasyfikowanie motywacji

Twoje motywacje do wdrożenia w chmurze będzie prawdopodobnie znajdować się w wielu kategoriach. Gdy tworzysz listę motywacji, trendy prawdopodobnie pojawią się. Motywacje mogą być powiązane z jedną klasyfikacją niż z innymi. Użyj klasyfikacji dominującej, aby pomóc w opracowaniu strategii wdrażania chmury.

Gdy odpowiedź na krytyczne zdarzenia biznesowe ma najwyższy priorytet, ważne jest, aby wcześniej prowadzić [implementację w chmurze](../getting-started/migrate.md#cloud-implementation), często równolegle z strategią i planowaniem. To podejście wymaga wzrostu sposób myślenia i gotowości do iteracyjnego ulepszania procesów, w oparciu o wyznanie bezpośrednich lekcji.

Gdy migracja ma najwyższy priorytet, [strategia i planowanie](../getting-started/migrate.md#cloud-strategy-and-planning) będą odgrywać istotną rolę wczesną w procesie. Zalecamy [zaimplementowanie pierwszego obciążenia](../getting-started/migrate.md#cloud-implementation) równolegle z planowaniem, aby ułatwić zespołowi zrozumienie i przewidywanie wszelkich krzywych szkoleniowych, które są związane z wdrażaniem w chmurze.

Gdy innowacyjność jest najwyższy priorytetem, strategia i planowanie będą wymagać dalszych inwestycji na wczesnych okresach w celu zapewnienia równowagi w portfelu i porozumieniu inwestycji dokonanych podczas wdrażania chmury. Aby uzyskać dodatkowe informacje i wskazówki, zobacz [Omówienie podróży innowacji](../getting-started/innovate.md).

Aby zapewnić podejmowanie decyzji, wszyscy uczestnicy procesu migracji powinni mieć jasno świadomość ich motywacji. W poniższej sekcji opisano sposób, w jaki klienci mogą kierować i podejmować decyzje dotyczące podejmowania decyzji w ramach spójnych, strategicznych metod.

## <a name="motivation-driven-strategies"></a>Strategie oparte na motywacji

W tej sekcji przedstawiono najważniejsze informacje dotyczące *migracji* i *innowacji* oraz ich odpowiednie strategie.

### <a name="migration"></a>Migracja

Motywacje *migracji* wymienione w górnej części tabeli motywacji są najbardziej popularne, ale nie zawsze są najbardziej znaczące, przyczyny wdrożenia chmury. Te wyniki są ważne do osiągnięcia, ale najprawdopodobniej są używane do przechodzenia do innych, bardziej użytecznych Worldviews. Ta ważna pierwsza czynność wdrożenia chmury jest często nazywana *migracją w chmurze*. Struktura odnosi się do strategii wykonywania migracji w chmurze za pomocą [migracji](../getting-started/migrate.md)warunkowej.

Niektóre motywacje są dobrze wyrównane z strategią migrowania. W górnej części tej listy najczęstsze znaczenie mają znacznie mniej wpływu na działalność biznesową niż te, które znajdują się na końcu listy.

- Oszczędność kosztów.
- Zmniejszenie poziomu dostawcy lub w zakresie technicznym.
- Optymalizacja operacji wewnętrznych.
- Zwiększając elastyczność biznesową.
- Przygotowanie do nowych możliwości technicznych.
- Skalowanie w celu spełnienia wymagań dotyczących rynku.
- Skalowanie w celu spełnienia wymagań geograficznych.

### <a name="innovation"></a>Innowacja

Dane są nowym asortymentem. Nowoczesne aplikacje są łańcuchem dostaw, który umożliwia korzystanie z tych danych w różnych środowiskach. Na współczesnym rynku biznesowym trudno znaleźć analizie przekształceń produkt lub usługę, które nie są oparte na usłudze Data, szczegółowe informacje i środowiska klienta. Motywacje, które pojawiają się niżej na liście *innowacji* , są dostosowane do strategii technologicznej, która jest określana w tym środowisku jako [innowacje](../getting-started/innovate.md).

Poniższa lista zawiera motywacje, które powodują, że organizacja IT może skupić się więcej na strategii innowacji niż Strategia migracji.

- Zwiększając elastyczność biznesową.
- Przygotowanie do nowych możliwości technicznych.
- Tworzenie nowych możliwości technicznych.
- Skalowanie w celu spełnienia wymagań dotyczących rynku.
- Skalowanie w celu spełnienia wymagań geograficznych.
- Ulepszanie środowisk i zaangażowania klientów.
- Transformowanie produktów lub usług.

## <a name="next-steps"></a>Następne kroki

Zrozumienie przewidywanych rezultatów działania biznesowego ułatwia prowadzenie konwersacji, które należy znać, aby móc korzystać z dopasowań i obsługi metryk, w zależności od strategii biznesowej. Następnie zapoznaj się z omówieniem wyników działalności biznesowej, które są często powiązane z przechodzeniem do chmury.

> [!div class="nextstepaction"]
> [Przegląd wyników firmy](./business-outcomes/index.md)
