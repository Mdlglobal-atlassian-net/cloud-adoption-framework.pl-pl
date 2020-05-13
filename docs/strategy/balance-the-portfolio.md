---
title: Równoważenie portfela
description: Odkryj strategie umożliwiające zrównoważenie migracji, innowacji i eksperymentów, aby maksymalnie wykorzystać możliwości migracji do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: f241899ff97b3ded1e5c2c82c4b0c6724843a411
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218972"
---
<!-- docsTest:ignore "Team 1" "Team 2" -->
<!-- cSpell:ignore CSAT -->

# <a name="balance-the-portfolio"></a>Równoważenie portfela

Wdrażanie w chmurze jest nakładem pracy związanym z zarządzaniem portfelem, Cleverly jako implementacją techniczną. Podobnie jak w przypadku wszystkich ćwiczeń związanych z zarządzaniem portfolio, bilansowanie portfolio ma kluczowe znaczenie. Na poziomie strategicznym oznacza to zrównoważenie migracji, innowacji i eksperymentów w celu maksymalnego wykorzystania chmury. Gdy wysiłki związane z wdrażaniem chmury są zbyt daleko w jednym kierunku, złożoność znajdzie swój sposób na wysiłki. W tym artykule przedstawimy Czytelnikowi podejścia do osiągnięcia równowagi portfela.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Bilansowanie portfolio ma charakter strategiczny. W związku z tym zaprezentowane w nim podejście jest równie strategiczne. Aby podstawić strategię w podejmowaniu decyzji opartych na danych, w tym artykule przyjęto założenie, że czytelnik ocenia istniejący [podpis cyfrowy](../digital-estate/index.md) lub rozpoczął ten proces. Celem tego podejścia jest pomoc w ocenie obciążeń, aby zapewnić odpowiednią równowagę portfela przez pytania jakościowe i udoskonalanie portfela.

<!-- docsTest:ignore 2M months years datacenters improvement TODO -->

### <a name="document-business-outcomes"></a>Dokumentacja wyników biznesowych

Przed przeprowadzeniem zrównoważenia portfolio ważne jest, aby udokumentować i udostępniać wyniki biznesowe związane z pracą w chmurze. Poniższa tabela ułatwia dokumentowanie i udostępnianie żądanych wyników biznesowych. Należy pamiętać, że większość firm dąży do osiągnięcia wielu wyników jednocześnie. Celem tego ćwiczenia jest wyjaśnienie rezultatów, które są najbardziej bezpośrednio związane z nakładem pracy w zakresie migracji do chmury:

| Wynik  | Mierzony przez  | Cel  | Horyzont czasowy  | Priorytet tego nakładu pracy  |
|---------|---------|---------|---------|---------|
| Zmniejsz koszty IT     | Budżet centrum danych         | Ogranicz do $2 mln USD     | 12 miesięcy         | 1.         |
| Wyjście centrum danych     | Wyjdź z centrów danych         | 2 centra danych         | 6 miesięcy         | 2.         |
| Zwiększenie sprawności biznesowej     | Szybsze wejście na rynek  | Skrócenie czasu wdrożenia o sześć miesięcy         | 2 lata         | 3.        |
| Ulepszanie środowiska klienta     | Zadowolenie klienta (CSAT)         | Poprawa o 10%         | 12 miesięcy         | 4.         |

> [!IMPORTANT]
> Powyższa tabela jest przykładem fikcyjnym i nie powinna być używana do określania priorytetów. W wielu przypadkach ta tabela może być traktowana jako Antywzorzec przez umieszczenie oszczędności kosztów powyżej środowiska klienta.

Powyższa tabela może dokładnie przedstawiać priorytety zespołu strategii chmury i zespołu wdrażania chmury. Ze względu na znaczne ograniczenia czasowe ten zespół kładzie większy nacisk na redukcję kosztów IT i traktuje priorytetowo wyjście z centrum danych jako środek do osiągnięcia żądanego obniżenia kosztów IT. Jednak dzięki udokumentowaniu konkurencyjnych priorytetów w tej tabeli zespół wdrożeniowy ds. chmury może ułatwiać zespołowi strategicznemu ds. chmury identyfikowanie możliwości lepszego dopasowania implementacji nadrzędnej strategii portfela.

### <a name="move-fast-while-maintaining-balance"></a>Szybkość zmian przy zachowaniu równowagi

Wskazówki dotyczące [przyrostowej racjonalizacji majątku cyfrowego](../digital-estate/index.md) sugerują podejście, w którym racjonalizacja rozpoczyna się od pozycji niezrównoważonej. Zespół strategiczny ds. chmury powinien oszacować każde obciążenie pod kątem zgodności z podejściem do ponownego hostowania. Takie podejście jest sugerowane, ponieważ pozwala na szybką ocenę złożonego majątku cyfrowego na podstawie danych ilościowych. Takie wstępne założenie umożliwia zespołowi wdrożeniowemu ds. chmury szybkie zaangażowanie i skrócenie czasu oczekiwania na wyniki biznesowe. Jednak, zgodnie z opisem w tym artykule, to pytania jakościowe będą zapewniały niezbędną równowagę portfela. W tym artykule opisano proces tworzenia uzgodnionego salda.

### <a name="importance-of-sunset-and-retire-decisions"></a>Znaczenie decyzji o wycofaniu

W tabeli z powyższej sekcji [Dokumentowanie wyników biznesowych](#document-business-outcomes) pominięto kluczowy wynik, który mógłby ułatwić osiągnięcie pierwszorzędnego celu redukcji kosztów IT. W przypadku klasyfikacji obniżenia kosztów w dowolnym miejscu listy wyników biznesowych ważne jest, aby wziąć pod uwagę potencjalną liczbę wycofywanych obciążeń. W niektórych scenariuszach oszczędności kosztów mogą pochodzić z braku migracji obciążeń, które nie uzasadniają krótkoterminowych inwestycji. Niektórzy klienci zgłosili oszczędności kosztów przekraczające 20% łącznego obniżenia kosztów przez wycofanie niewykorzystywanych obciążeń.

Aby zrównoważyć portfel, lepiej odzwierciedlając decyzje o wycofaniu, zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury są zachęcane do zadawania następujących pytań dotyczących każdego obciążenia w ramach procesów oceny i migracji:

- Czy obciążenie było używane przez użytkowników końcowych w ciągu ostatnich sześciu miesięcy?
- Czy ruch użytkowników końcowych jest stały lub wzrastający?
- Czy to obciążenie będzie potrzebne firmie w ciągu 12 miesięcy od teraz?

Jeśli odpowiedź na dowolne z tych pytań to "nie", obciążenie może być kandydatem do wycofania. Jeśli możliwość wycofania zostanie potwierdzona przez właściciela aplikacji, migracja obciążenia może nie mieć sensu. To prowadzi do kilku pytań jakościowych:

- Czy można ustanowić plan wycofania tego obciążenia?
- Czy to obciążenie może zostać wycofane przed wyjściem z centrum danych?

Jeśli odpowiedzi na oba te pytania to "tak", _warto rozważyć_ niemigrowanie obciążenia. Takie podejście może pomóc osiągnąć cele zmniejszenia kosztów i wyjścia z centrum danych.

Jeśli odpowiedź na pytanie ma wartość "nie", może być konieczne ustanowienie planu do obsługi obciążenia, dopóki będzie możliwe jego wycofanie. Ten plan może obejmować przeniesienie zasobów do tańszego lub alternatywnego centrum danych, co również umożliwia osiągnięcie celów zmniejszenia kosztów i wyjścia z jednego centrum danych.

## <a name="adopt-process-changes"></a>Przyjmowanie zmian procesów

Równoważenie portfela wymaga dodatkowej analizy jakościowej w fazie wdrażania, co pomoże w zwiększeniu wymiernej racjonalizacji portfolio.

Na podstawie danych z tabeli w powyższej sekcji [Dokumentowanie wyników biznesowych](#document-business-outcomes) prawdopodobne jest ryzyko, że portfel dąży zbyt daleko do modelu wykonywania skoncentrowanego na migracji. Jeśli obsługa klienta miałaby najwyższy priorytet, bardziej prawdopodobny byłby portfel bardziej nastawiony na innowacje. Żadne z tych podejść nie jest prawidłowe lub złe, ale zbytnie dążenie w jednym kierunku zwykle skutkuje mniejszymi zyskami, niepotrzebnie zwiększa złożoność i wydłuża czas wykonywania nakładów pracy zakresie wdrażania w chmurze.

Aby zmniejszyć złożoność, należy postępować zgodnie z tradycyjnym podejściem do racjonalizacji portfolio, ale w modelu iteracyjnym. Poniższe kroki przedstawiają model jakościowy takiego podejścia:

- Zespół strategiczny ds. chmury utrzymuje priorytetową listę prac dotyczącą obciążeń, które mają zostać poddane migracji.
- Zespół strategiczny ds. chmury i zespół wdrożeniowy ds. chmury prowadzą spotkanie dotyczące planowania wydania przed ukończeniem każdego wydania.
- W trakcie spotkania dotyczącego planowania wydania zespoły uzgadniają od 5 do 10 najważniejszych obciążeń na priorytetyzowanej liście prac.
- Poza spotkaniem planowania wydania zespół wdrożeniowy ds. chmury zadaje właścicielom aplikacji i ekspertom dziedzinowym następujące pytania:
  - Czy ta aplikacja może zostać zastąpiona odpowiednikiem platformy jako usługi (PaaS)?
  - Czy ta aplikacja jest aplikacją innej firmy?
  - Czy zatwierdzono budżet inwestycji w ciągłe tworzenie aplikacji w ciągu najbliższych 12 miesięcy?
  - Czy dodatkowy rozwój tej aplikacji poprawi środowisko klienta? Utworzy przewagę konkurencyjną? Wygeneruje dodatkowy przychód firmy?
  - Czy dane w ramach tego obciążenia przyczyniają się do dalszych innowacji związanych z technologiami analizy biznesowej, uczenia maszynowego, Internetu rzeczy lub pokrewnymi?
  - Czy obciążenie jest zgodne z nowoczesnymi platformami aplikacji, takimi jak Azure App Service?
- Odpowiedzi na powyższe pytania i wszelka inna wymagana analiza jakościowa wpływają następnie na korekty priorytetyzowanej listy prac. Te korekty mogą obejmować:
  - Jeśli obciążenie nadawałoby się do zastąpienia przy użyciu rozwiązania PaaS, mogłoby zostać całkowicie usunięte z listy prac migracji. Co więcej, dodatkowe poszczególna staranność do podjęcia decyzji między rehostem a zastępowaniem zostanie dodane jako zadanie, tymczasowo zmniejszając priorytet tego obciążenia z zaległości migracji.
  - Jeśli obciążenie jest (lub powinno być) przechodzące na rozwój, najlepiej pasuje do modelu refaktoryzacji — Rebuild-rekonstrukcja. Ponieważ innowacje i migracja wymagają różnych umiejętności technicznych, aplikacje, które są dostosowane do refaktoryzacji-rekonstrukcja-Rebuild, powinny być zarządzane przez zaległości innowacyjne zamiast zaległości migracji.
  - Jeśli obciążenie jest częścią dalszej innowacji, wtedy może mieć sens refaktoryzacja platformy danych, ale z pozostawieniem warstw aplikacji jako kandydata do ponownego hostowania. Niewielka refaktoryzacja platformy danych obciążenia może często być wprowadzona do listy prac migracji lub innowacji. Ten wynik racjonalizacji może skutkować bardziej szczegółowymi elementami roboczymi na liście prac, ale w przeciwnym razie priorytety nie zostałyby zmienione.
  - Jeśli obciążenie nie jest strategiczne, ale jest zgodne z nowoczesnymi, opartymi na chmurze platformami hostingu aplikacji, rozsądne może być przeprowadzenie niewielkiej refaktoryzacji aplikacji w celu wdrożenia jej jako nowoczesnej aplikacji. Może to przyczynić się do ogólnego oszczędności przez zredukowanie ogólnych wymagań licencyjnych IaaS i systemów operacyjnych migracji do chmury.
  - Jeśli obciążenie jest aplikacją innej firmy, a dane obciążenia nie są planowane do użycia w dalszych innowacjach, najlepszym rozwiązaniem może być pozostawienie opcji ponownego hostowania na liście prac.

Pytania te nie powinny stanowić zakresu analizy jakościowej wykonanej dla każdego obciążenia, ale mogą one pomóc w rozmowie dotyczącym złożoności niezrównoważonego portfolio.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Podczas migracji działania równoważenia portfolio mogą mieć negatywny wpływ na szybkość migracji (szybkość, z jaką są migrowane zasoby). Poniższe wskazówki posłużą do rozwinięcia kwestii, dlaczego i jak należy dostosować pracę, aby uniknąć przerw w wysiłkach związanych z migracją.

Racjonalizacja portfela wymaga różnorodności technicznych nakładów pracy. Zespoły wdrożeniowe ds. chmury mają pokusę dopasowania tej różnorodności portfela w ramach wysiłków związanych z migracją. Biznesowi uczestnicy projektu chcą współpracować z pojedynczym zespołem wdrożeniowym ds. chmury w celu prowadzenia całej listy prac migracji. Rzadko jest to zalecanym podejściem, a w wielu przypadkach może zmniejszać produktywność.

Te różnorodne wysiłki należy podzielić na segmenty w dwóch lub większej liczbie zespołów wdrażania w chmurze. Korzystanie z modelu dwuzespołowego jako przykładowego trybu wykonywania, zespół 1 jest zespołem migracji, a zespół 2 jest zespołem ds. innowacji. W przypadku większych nakładów te zespoły mogą być dodatkowo podzielona na inne podejścia, takie jak zastępowanie/PaaS działań lub drobne refaktoryzacje. Poniżej przedstawiono umiejętności i role wymagane do rehostowania, refaktoryzacji lub drobnego refaktoryzacji:

**Rehostowanie:** Rehostowanie wymaga, aby członkowie zespołu implementują zmiany ukierunkowane na infrastrukturę. Zasadniczo odbywa się to przy użyciu narzędzia, takiego jak Azure Site Recovery, do migrowania maszyn wirtualnych lub innych zasobów na platformę Azure. Ta praca dobrze pasuje do administratorów centrum danych lub realizatorów IT. Zespół ds. migracji do chmury ma odpowiednią strukturę, aby wykonać tę pracę na dużą skalę. Jest to najszybszy sposób migrowania istniejących zasobów w większości scenariuszy.

**Refaktoryzacja:** Refaktoryzacja wymaga, aby członkowie zespołu mogli modyfikować kod źródłowy, zmieniać architekturę aplikacji lub przyjmować nowe usługi w chmurze. Zasadniczo ten w tych nakładach pracy wykorzystuje się narzędzia programistyczne, takie jak program Visual Studio i narzędzia potoku wdrażania, takie jak Azure DevOps, do ponownego wdrożenia zmodernizowanych nowoczesnych aplikacji na platformie Azure. Ta praca jest dopasowana do ról wytwarzania aplikacji lub ról wytwarzania potoku DevOps. Zespół ds. innowacji w chmurze jest najlepszym strukturą do dostarczania tej pracy. Zastępowanie istniejących zasobów zasobami w chmurze w tym podejściu może zająć więcej czasu, ale natywne funkcje chmury mogą być korzystne dla aplikacji.

**Niewielka Refaktoryzacja:** Niektóre aplikacje można nowoczesny z niewielkim refaktoryzacją na poziomie danych lub aplikacji. Ta praca wymaga, aby członkowie zespołu wdrażali dane na platformach danych opartych na chmurze lub wprowadzali niewielkie zmiany konfiguracji w aplikacjach. Może to wymagać ograniczonego wsparcia ekspertów zajmujących się danymi lub rozwojem aplikacji. Jednak ta praca jest podobna do pracy wykonywanej przez realizatorów IT podczas wdrażania aplikacji innych firm. Pracę tę można łatwo dopasować do zespołu ds. migracji do chmury lub zespołu strategicznego ds. chmury. Chociaż ten nakład pracy nie zbliża się do szybkości migracji polegającej na ponownym hostowaniu, jego wykonanie zajmuje mniej czasu niż nakład pracy na refaktoryzację.

Podczas migracji należy podzielić wysiłki na trzy sposoby wymienione powyżej i wykonane przez odpowiedni zespół w odpowiedniej iteracji. Chociaż należy zróżnicować portfolio, należy również upewnić się, że wysiłki są bardzo skoncentrowane i segregowane.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się ze sposobem, w jaki [globalne decyzje rynkowe](./global-markets.md) mogą wpłynąć na podróż transformację.

> [!div class="nextstepaction"]
> [Opis rynków globalnych](./global-markets.md)
