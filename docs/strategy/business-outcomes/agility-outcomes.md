---
title: Przykłady wyników dotyczącej elastyczności
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć swoją sytuację na rynku firmy i konkurencyjną poziomą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: feff683b4b19018895cc7eb9ac3ede6b03cd5300
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218938"
---
# <a name="examples-of-agility-outcomes"></a>Przykłady wyników dotyczącej elastyczności

Zgodnie z opisem w temacie [wyniki biznesowe](./index.md), niektóre potencjalne wyniki biznesowe mogą stanowić podstawę dla każdej rozmowy transformującej transformację z firmą. Ten artykuł koncentruje się na timeliest Business Measure: elastyczność biznesowa. Informacje na temat pozycji rynkowej i konkurencyjnej poziomej firmy mogą pomóc w ideach wyników działalności biznesowej, które są celem podróży transformację firmy.

Tradycyjni funkcjonariusze inwestycji i zespoły IT były uważane za źródło stabilności w podstawowych procesach o krytycznym znaczeniu. Jest to nadal prawdziwe. Niektóre firmy mogą działać prawidłowo, gdy ich platforma IT jest niestabilna. Jednak w dzisiejszym świecie biznesowym jest dużo więcej. Może ona zostać rozszerzona o więcej niż proste centrum kosztów dzięki współpracy z firmą w celu zapewnienia korzyści na rynku. Wielu dyrektorów ds. inwestycji i kierownictwa zakłada, że stabilność jest po prostu podstawą dla tego elementu. W przypadku tych liderów elastyczność biznesowa jest miarą udziału w firmie.

<!-- markdownlint-disable MD026 -->

## <a name="why-is-agility-so-important"></a>Dlaczego taka elastyczność jest ważna?

Rynki zmieniają się w szybszym tempie niż kiedykolwiek wcześniej. Począwszy od 2015, tylko firmy 57 w listy Fortune 500 61 lat w późniejszym &mdash; 88,6 czasie. Oznacza to zmianę na rynku w poprzednio nieprawidłowym tempie. Nie ma to wpływu na działalność informatyczną i nawet agilities biznesową w organizacji na listy Fortune 500, ale te wyniki pomagają nam zrozumieć tempo, w jaki sposób nadal zmieniają się rynki.

W przypadku operatorów dominujących i współdziałania, elastyczność biznesowa może być różnicą między sukcesem lub niepowodzeniem inicjatywy biznesowej. Szybka adaptacja do zmian wprowadzonych na rynku może pomóc istniejącym klientom lub zastrzec udział w rynku od konkurentów. Wyniki związane z elastycznością w następnych sekcjach mogą pomóc w przekazywaniu informacji o chmurze podczas transformacji.

## <a name="time-to-market-outcome"></a>Wynik czasu na rynek

W trakcie wysiłków innowacyjnych w chmurze czas wprowadzenia na rynek to kluczowa miara umożliwiająca rozwiązanie zmiany rynku. W wielu przypadkach lider biznesowy może mieć istniejący budżet do tworzenia aplikacji lub uruchamiania nowego produktu. Jasno komunikuje się z korzyścią z przedziału czasowego na rynek, aby skierować ten lidera do podróży transformację budżetu.

- **Przykład 1:** Europejski Wydział firmy opartej na USA musi zapewnić zgodność z przepisami Rodo przez ochronę danych klienta w bazie danych, która obsługuje operacje na Wielkiej Brytanii. Ich istniejąca wersja SQL Server nie obsługuje wymaganego zabezpieczenia na poziomie wiersza. Uaktualnienie w miejscu byłoby zbyt uciążliwe. Przy użyciu Azure SQL Database do replikowania i uaktualniania bazy danych klient dodaje konieczną miarę zgodności w ciągu tygodni.

- **Przykład 2:** Firma logistyki wykryła niewykorzystany segment rynku, ale potrzebuje nowej wersji aplikacji sztandarowe do przechwycenia tego udziału w rynku. Ich większy konkurent ma takie samo odnajdywanie. Dzięki wykonaniu wysiłków programistycznych aplikacji obsługujących chmurę firma obejmuje Obsession klienta i podejście deweloperskie oparte na DevOpsach, aby zmniejszyć liczbę starszych konkurentów o _x_ miesiącach. Dzięki temu w systemie wejścia na rynek zabezpieczony jest podstawowy klient.

<!-- docsTest:ignore "Jamey Shiels" "Vice President of Digital Experience" "Aurora Health Care" -->

### <a name="aurora-health-care"></a>Opieka zdrowotna Aurora

System opieki zdrowotnej przekształca Usługi online w przyjazne środowisko cyfrowe. Aby przekształcić swoje usługi cyfrowe, Aurora opiekę zdrowotną swoich witryn internetowych na platformę Microsoft Azure i przyjęto strategię ciągłego innowacji.

<!-- cSpell:ignore Jamey Shiels -->

> "Jako zespół koncentrujemy się na rozwiązaniach o wysokiej jakości i szybkości. Wybranie platformy Azure było bardzo analizie przekształceńą decyzją dla nas ".
>
> Jamey Shiels
>
> Wiceprezes ds. funkcji cyfrowych
>
> Opieka zdrowotna Aurora

## <a name="provision-time"></a>Czas udostępniania

Gdy firma wymaga nowych usług IT lub skaluje się do istniejących usług, nabycie i udostępnienie nowego sprzętu lub zasobów wirtualnych może zająć kilka tygodni. Po migracji do chmury można łatwiej włączyć funkcję samoobsługowego udostępniania, co pozwala na skalowanie w godzinach pracy.

- **Przykład:** Firma z towarami opakowanymi w konsumenta wymaga utworzenia i rozdzielenia setek klastrów bazy danych na rok w celu spełnienia wymagań operacyjnych firmy. Lokalne hosty wirtualne mogą zapewnić szybkie udostępnianie, ale proces odzyskiwania zasobów wirtualnych jest powolny i wymaga znacznego czasu od zespołu. W związku z tym starsze środowisko lokalne cierpi z przeładowanie i może być rzadko zachowywać się z zapotrzebowaniem. Po przeprowadzeniu migracji do chmury można łatwiej zapewnić skryptowe Inicjowanie obsługi administracyjnej zasobów przy użyciu podejścia obciążenia zwrotnego do rozliczania. Dzięki temu firma może przełączać się tak szybko, jak to konieczne, ale nadal będzie można uwzględnić koszt zasobów, których wymagają. To działanie w chmurze ogranicza wdrożenia wyłącznie do budżetu firmy.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat [osiągniętych wyników](./reach-outcomes.md).

> [!div class="nextstepaction"]
> [Wyniki związane z zasięgiem](./reach-outcomes.md)
