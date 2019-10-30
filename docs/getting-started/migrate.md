---
title: Rozpocznij podróż do migracji w chmurze na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Rozpocznij podróż do migracji w chmurze na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 8870f5ebeab855ec841ed00d109245a1efdeff20
ms.sourcegitcommit: 7ffb0427bba71177f92618b2f980e864b72742f4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2019
ms.locfileid: "73048320"
---
# <a name="begin-a-cloud-migration-journey-in-azure"></a>Rozpocznij podróż do migracji w chmurze na platformie Azure

Użyj platformy wdrażania Microsoft Cloud dla platformy Azure, aby rozpocząć podróż do migracji do chmury. Ta struktura zawiera kompleksowe wskazówki dotyczące przenoszenia starszych obciążeń aplikacji do chmury przy użyciu innowacyjnych technologii opartych na chmurze.

## <a name="executive-summary"></a>Podsumowanie dla kierownictwa

Platforma wdrażania w chmurze pomaga klientom podejmować uproszczone podróże w chmurze. Ta struktura zawiera szczegółowe informacje dotyczące kompleksowej podróży w chmurze, rozpoczynając od docelowych rezultatów firmy, a następnie dopasowując gotowość do chmury i oceny z jasno określonymi celami biznesowymi. Te wyniki są osiągane przez zdefiniowaną ścieżkę do wdrożenia chmury. Po wdrożeniu opartym na migracji zdefiniowana ścieżka koncentruje się głównie na migrowaniu obciążeń lokalnych do chmury. Czasami ta podróż obejmuje modernizację obciążeń, aby zwiększyć zwrot z inwestycji w miarę wysiłków związanych z migracją.

Ta platforma została zaprojektowana głównie dla architektów chmury i zespołów strategii chmurowej, które prowadzą do rozwoju chmury. Jednak wiele tematów w tej strukturze dotyczy innych ról w firmie i. Architektzy chmury często sprawują rolę ułatwiającą zaangażowanie każdej z odpowiednich ról. To podsumowanie dotyczące programu Executive zostało zaprojektowane z założeniami, aby przygotować różne role przed ułatwieniem konwersacji.

> [!NOTE]
> Te wskazówki są obecnie publiczną wersją zapoznawczą. W ramach tej wersji zapoznawczej są dokładnie przetestowane informacje o terminologii, podejściach i wskazówkach. W związku z tym spis treści i wskazówki mogą ulec zmianie nieco w czasie.

## <a name="motivations"></a>Przesłanki

Migracje w chmurze mogą pomóc firmom w osiągnięciu żądanych wyników firmy. Wyraźne kierowanie motywacji, sterowników firmowych i pomiarów sukcesu są istotną kwestią dla podejmowania świadomych decyzji związanych z migracją w chmurze. Poniższa tabela klasyfikuje motywacje w celu ułatwienia tej konwersacji. Przyjęto założenie, że większość firm będzie miała motywacje dla każdej klasyfikacji. Celem tej tabeli nie jest ograniczanie wyników, ale zamiast tego warto ułatwić określanie priorytetów ogólnych celów i motywacji:

<!-- markdownlint-disable MD033 -->

|Krytyczne zdarzenia biznesowe | Motywacje migracji | Motywacje innowacji |
|---------|---------|---------|
| Wyjście centrum danych<br/><br/>Fuzje, pozyskiwanie lub zbycie<br/><br/>Obniżki wydatków inwestycyjnych<br/><br/>Koniec wsparcia dla technologii o kluczowym znaczeniu<br/><br/>Odpowiedź na zmiany zgodności z przepisami<br/><br/>Spełniaj nowe wymagania dotyczące suwerenności danych<br/><br/>Zmniejsz zakłócenia i zwiększ stabilność IT|Redukcja kosztów<br/><br/>Zmniejszenie liczby dostawców lub technicznych<br/><br/>Optymalizacja operacji wewnętrznych<br/><br/>Zwiększenie sprawności biznesowej<br/><br/>Przygotuj się na nowe możliwości techniczne<br/><br/>Skalowanie w celu spełnienia wymagań dotyczących rynku<br/><br/>Skalowanie w celu spełnienia wymagań geograficznych|Przygotuj się na nowe możliwości techniczne<br/><br/>Twórz nowe możliwości techniczne<br/><br/>Skalowanie w celu spełnienia wymagań dotyczących rynku<br/><br/>Skalowanie w celu spełnienia wymagań geograficznych<br/><br/>Ulepszanie środowisk i zaangażowania klientów<br/><br/>Przekształć produkty lub usługi<br/><br/>Zakłócenie rynku dzięki nowym produktom lub usługom|

<!-- markdownlint-enable MD033 -->

Gdy odpowiedź na krytyczne zdarzenia biznesowe ma najwyższy priorytet, ważne jest, aby zaangażować [implementację w chmurze](#cloud-implementation) wcześniej, często równolegle z strategiami strategii i planowania. Takie podejście wymaga sposób myślenia wzrostu i gotowości do iteracyjnego ulepszania procesów, w oparciu o wyznanie bezpośrednich lekcji.

Gdy motywacje do migracji ma priorytet, [strategia i planowanie](#cloud-strategy-and-planning) będą odgrywać istotną rolę wczesną w procesie. Jednak zdecydowanie zaleca się, aby [implementacja](#cloud-implementation) pierwszego obciążenia była przeprowadzana równolegle z planowaniem, aby ułatwić zespołowi zrozumienie i zaplanowanie wszelkich krzywych uczenia związanych z chmurą.

Gdy motywacje innowacji są najwyższy priorytetem, strategia i planowanie będą wymagać dalszych inwestycji na wczesnych okresach w celu zapewnienia równowagi w portfelu i porozumieniu inwestycji dokonanych w chmurze. Aby uzyskać więcej informacji na temat realizacji motywacji innowacji, zobacz [Omówienie podróży innowacji](./innovate.md).

Przygotowanie wszystkich uczestników w ramach wysiłków związanych z migracją dzięki świadomości motywacji zapewni podejmowanie decyzji. W poniższej metodzie migracji opisano, jak firma Microsoft sugeruje klientom podjęcie tych decyzji w ramach spójnej metodologii.

## <a name="migration-approach"></a>Podejście do migracji

Struktura wdrażania w chmurze stanowi ogólny zbiór planów, gotowy, zastosowany w celu pogrupowania typów nakładu pracy w ramach dowolnego wdrożenia chmury. To podsumowanie programu Executive kompiluje się na tym przepływie wysokiego poziomu w celu ustalenia iteracji procesów, które mogą ułatwić podniesienie/przewinięcie/optymalizację wysiłków **i** modernizację w jednym podejściu w ramach wszystkich działań związanych z migracją w chmurze.

Takie podejście obejmuje dwie metodologie i obszary ostrości: strategia chmury & planowanie i implementację w chmurze. [Motywacja](#motivations) lub pożądany wynik biznesowy dla migracji w chmurze często określa, jak dużo zespół powinien inwestować w [strategię i planowanie](#cloud-strategy-and-planning) i [implementację](#cloud-implementation). Te motywacje mogą również wpływać na decyzje wykonywane sekwencyjnie lub równolegle.

## <a name="cloud-implementation"></a>Implementacja w chmurze

Implementacja w chmurze to proces iteracyjny służący do migrowania i modernizacji cyfrowego podpisywania w celu wyrównania z dokierowanymi wynikami biznesowymi i formantami zarządzania zmianami. W trakcie każdej iteracji obciążenia są migrowane lub zmodernizowane w sposób zgodny z strategią i planem. Decyzje dotyczące IaaS, PaaS lub hybrydowych są tworzone w fazie oceny w celu zoptymalizowania kontroli i wykonania. Te decyzje będą korzystać z narzędzi używanych podczas fazy migracji. Ten model może być używany z minimalnym strategią i planowaniem. Jednak, aby zapewnić największą wartość zwracaną przez firmę, zdecydowanie zaleca się, aby zarówno, jak i w firmie były wyrównane do jasnej strategii i zaplanować działania implementacji.

![Metodologia implementacji chmury platformy wdrażania w chmurze](../_images/operational-transformation-migrate.png)

Celem tego nakładu jest migracja lub modernizacja obciążeń. Obciążenie to zbiór infrastruktury, aplikacji i danych, które wspólnie obsługują typowe cele biznesowe lub wykonywanie wspólnego procesu biznesowego. Przykłady obciążeń mogą obejmować takie elementy, jak aplikacja biznesowa, rozwiązanie do obsługi płac HR, rozwiązanie CRM, przepływ pracy zatwierdzania dokumentów finansowych lub rozwiązanie analizy biznesowej. Obciążenia mogą również obejmować udostępnione zasoby techniczne, takie jak magazyn danych, który obsługuje kilka innych rozwiązań. W niektórych przypadkach obciążenie może być reprezentowane przez pojedynczy zasób, taki jak samodzielny serwer, aplikacja lub platforma danych.

Migracje w chmurze są często traktowane jako pojedynczy projekt w ramach szerszego programu w celu usprawnienia operacji, kosztów lub złożoności IT. Metodologia implementacji chmury pomaga w wyrównaniu wysiłków technicznych w ramach serii migracji obciążeń do wartości biznesowych wyższego poziomu, które opisano w strategii i planowaniu chmury.

**Pierwsze kroki:** Aby rozpocząć pracę z implementacją w chmurze, [Przewodnik migracji platformy Azure](../migrate/azure-migration-guide/index.md) i [Przewodnik po Instalatorze platformy Azure](../ready/azure-setup-guide/index.md) przedstawiają narzędzia i procesy wysokiego poziomu, które są konieczne do pomyślnego wykonania implementacji w chmurze. Migrowanie pierwszego obciążenia przy użyciu tych przewodników ułatwi zespołowi pokonanie wstępnych krzywych szkoleniowych w procesie planowania. Po wykonaniu tych czynności należy uzyskać dodatkowe zagadnienia dotyczące [rozwiniętej listy kontrolnej zakresu](../migrate/expanded-scope/index.md), najlepszych rozwiązań dotyczących [migracji](../migrate/azure-best-practices/index.md) i kwestii związanych z [migracją](../migrate/migration-considerations/index.md), aby wyrównać wskazówki dotyczące podstawowych ograniczeń, procesów, zespołu struktury i cele.

## <a name="cloud-strategy-and-planning"></a>Strategia i planowanie chmury

Strategia i planowanie chmury to metodologia, która koncentruje się na dostosowywaniu wyników, priorytetów i ograniczeń firmy w celu ustalenia jasnej strategii i planu migracji. Wynikowy plan (lub zaległości migracji) stanowi opis podejścia do migracji i modernizacji w całym portfolio IT, który może obejmować całe centra danych, wiele obciążeń lub różne kolekcje infrastruktury, aplikacji i danych. Prawidłowe zarządzanie portfolio IT w ramach wysiłków związanych z implementacją w chmurze pomoże Ci uzyskać odpowiednie wyniki biznesowe.

![Omówienie przewodnika Cloud Adoption Framework](../_images/caf-overview.png)

**Pierwsze kroki:** Pozostała część tego artykułu przygotowuje czytelnika do odpowiedniego zastosowania strategii chmurowej i planowania struktury wdrożenia w chmurze. Opisano w nim również dodatkowe zasoby i linki, które mogą pomóc czytelnikowi wdrożyć te podejście w celu zaplanowania wysiłków związanych z implementacją w chmurze.

### <a name="methodology-explained"></a>Wyjaśniono metodologię

Strategia chmurowa i planowanie rozwiązań w chmurze opracowano na podstawie przyrostowego podejścia do implementacji w chmurze, które jest dostosowane do strategii technologii Agile, dojrzałości kulturowej na podstawie podejścia do wzrostu sposób myślenia oraz strategii opartych na wyniki biznesowe. Ta metodologia składa się z następujących składników wysokiego poziomu, które są pomocne w implementacji każdej strategii.

Jak pokazano na powyższym obrazie, Ta struktura przedstawia decyzje strategiczne w niewielkiej liczbie zawartych procesów, które działają w modelu iteracyjnym. Chociaż opisano w dokumencie liniowym, każdy z następujących procesów jest oczekiwany równolegle z iteracjami implementacji w chmurze. Linki dla każdego procesu będą pomocne w definiowaniu stanu zakończenia i sposobach wykupu w kierunku żądanego stanu końcowego:

- **[Plan](../strategy/index.md):** Gdy wdrożenie techniczne jest wyrównane z jasnymi celami biznesowymi, znacznie ułatwia mierzenie i dostosowanie sukcesu w wielu działaniach związanych z implementacją w chmurze, bez względu na decyzje techniczne.
- **[Gotowe](../ready/index.md):** Przygotowanie firmy, kultury, osób i środowiska do wprowadzania zmian prowadzi do sukcesu w każdym wysiłku i przyspiesza implementację i zmienia projekty.
- **Zastosuj:** Zapewnij prawidłowe wdrożenie żądanych zmian, w ramach procesów IT i firmowych, aby osiągnąć wyniki biznesowe.
  - **[Migrowanie](../migrate/index.md):** iteracyjne wykonywanie [metodologii implementacji w chmurze](#cloud-implementation) przestrzegane przez testowany proces oceny, migracji, optymalizacji i bezpiecznego & zarządzania, aby utworzyć powtarzalny proces migracji obciążeń.
  - **[Innowacje](../innovate/index.md):** Zwiększ wartość biznesową, korzystając z działań innowacyjnych, które odblokują nowe umiejętności techniczne i rozbudowane możliwości biznesowe.
- **[Zarządzanie](../govern/index.md):** Wyrównaj zasady firmowe jako materialne czynniki ryzyka, które zostały skorygowane za pomocą zasad, procesów i narzędzi do zarządzania opartego na chmurze.
- **[Zarządzanie](../manage/index.md):** Rozwiń operacje IT, aby zapewnić, że rozwiązania oparte na chmurze mogą być obsługiwane za pośrednictwem bezpiecznych, ekonomicznych procesów przy użyciu nowoczesnych narzędzi do obsługi chmurowej.
- **[Organizuj](../organize/index.md):** Wyrównaj osoby i zespoły, aby zapewnić prawidłowe operacje i wdrożenia w chmurze.

W ramach tego środowiska migracji Ta platforma zostanie użyta w celu rozróżnienia, zarządzania zmianami i popełniania zespołów funkcjonalnych przez realizację wyników działalności biznesowej.

### <a name="common-cultural-changes-resulting-from-adherence-to-this-methodology"></a>Typowe zmiany kulturowe, które wynikają z przestrzegania tej metodologii

Nakład pracy związany z pożądanymi wynikami biznesowymi może spowodować nieznaczne zmiany w kulturze IT, a w pewnym stopniu kulturę biznesową. Poniżej przedstawiono kilka typowych zmian kulturowych, które są widoczne w tym procesie:

- Zespół IT może przyjąć nowe umiejętności do obsługi obciążeń w chmurze.
- Wykonanie migracji do chmury zachęca podejścia iteracyjne lub Agile.
- Włączenie zarządzania chmurą pozwala również na pobudzanie podejścia DevOps.
- Utworzenie zespołu strategii chmurowej może prowadzić do ściślejszej integracji między firmą i liderami IT.
- Zbiorczo te zmiany mają na celu prowadzić do rozwoju działalności biznesowej i INFORMATYCZNej.

Zmiana kulturowa nie jest celem migracji w chmurze lub struktury wdrażania chmury, ale jest to powszechnie spotykane wyniki.
Zmiany kulturowe nie są bezpośrednio podkierowane, a zamiast tego subtelne zmiany w kulturze są osadzane w sugerowanych ulepszeniach procesu i podejścia w całej wskazówki.

### <a name="common-technical-efforts-associated-with-this-methodology"></a>Typowe wysiłki techniczne związane z tą metodologią

Podczas wdrażania strategii chmury i planowania zespołu IT będzie skoncentrowany znaczną część czasu na migracji istniejących zasobów cyfrowych do chmury. W trakcie tego działania oczekiwane są minimalne zmiany w kodzie, ale mogą one być często ograniczone do zmian konfiguracji. W wielu przypadkach można dokonać silnego uzasadnienia biznesowego dla modernizacji w ramach migracji do chmury.

### <a name="common-workload-examples"></a>Typowe przykłady obciążeń

Strategia i planowanie chmury często kierują się szeroką kolekcją obciążeń i aplikacji. W portfolio są zwykle migrowane popularne aplikacje lub typy obciążeń. Poniżej przedstawiono kilka przykładów:

- Aplikacje biznesowe
- Aplikacje dla klientów
- Aplikacje innych firm
- Platformy do analizy danych
- Rozwiązania rozproszone globalnie
- Wysoce skalowalne rozwiązania

### <a name="common-technologies-migrated"></a>Popularne technologie zostały zmigrowane

Technologie migrowane do chmury ciągle rozszerzają się w miarę jak dostawcy chmury dodają nowe możliwości. Poniżej przedstawiono kilka przykładów technologii najczęściej widzianych podczas migracji:

- Windows i SQL Server
- Bazy danych systemu Linux i typu Open Source (OSS)
- Destructure/NoSQL bazy danych
- SAP w systemie Azure
- Analiza (magazyn danych, Data Lake)

## <a name="next-steps-lifecycle-solution"></a>Następne kroki: rozwiązanie cyklu życia

Platforma wdrażania w chmurze to rozwiązanie cyklu życia. Jest ona przeznaczona do ułatwienia czytelnikom, którzy dopiero zaczynają podróży, a także czytelnicy, którzy mają wgląd w migrację. W związku z tym zawartość jest bardzo kontekstowa i charakterystyczna dla odbiorców. Następne kroki są najlepiej wyrównane do procesu wysokiego poziomu, który czytelnik chce ulepszyć.

> [!div class="nextstepaction"]
> [Strategia](../strategy/index.md)
>
> [Planowanie](../plan/index.md)
>
> [Gotowe](../ready/index.md)
>
> [Migrate (Migracja)](../migrate/index.md)
>
> [Wprowadzaj innowacje](../innovate/index.md)
>
> [Decydując](../govern/index.md)
>
> [Zarządzanie](../manage/index.md)
>
> [Organizowanie](../organize/index.md)
