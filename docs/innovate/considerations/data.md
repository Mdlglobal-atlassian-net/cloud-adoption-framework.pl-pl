---
title: Zdemokratyzuj proces dane za pomocą roznalazeków cyfrowych
description: Dowiedz się więcej na temat Democratization, proces uzyskiwania danych do właściwych wskazówek w celu przetestowania rzeczy i innowacji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: eb54bd4c583878fb72b4e7401fd05662ca87bc63
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83224140"
---
# <a name="democratize-data"></a>Demokratyzowanie danych

Potencjał węgla, ropy naftowej i ludzi był trzema najbardziej wynikowymi zasobami podczas rewolucji przemysłowej. Te zasoby są tworzone przez firmy, przesunięte rynki i ostatecznie zmienione. W przypadku oszczędności cyfrowych istnieją trzy równe zasoby: dane, urządzenia i potencjał ludzki. Każdy z tych zasobów zawiera doskonałe możliwości innowacji. W przypadku każdego wysiłku innowacji w nowoczesnej era dane są nową ropy naftowej.

W każdej firmie dzisiaj istnieją kieszenie danych, które mogą być używane do bardziej efektywnego znajdowania i zaspokajania potrzeb klientów. Niestety, proces wyszukiwania danych na potrzeby innowacji jest kosztowny i czasochłonny. Wiele z najbardziej cennych rozwiązań dla klientów to niewypełnienia, ponieważ odpowiednie osoby nie mogą uzyskać dostępu do potrzebnych danych.

Democratization danych to proces uzyskiwania tych danych do właściwych rąk związanych z wprowadzaniem innowacji. Ten proces może potrwać kilka formularzy, ale zazwyczaj obejmuje rozwiązania dla pozyskiwanych lub zintegrowanych danych pierwotnych, scentralizowania danych, udostępniania danych i zabezpieczania danych. Po pomyślnym wykonaniu tych metod eksperci w firmie mogą używać danych do testowania form. W wielu przypadkach zespoły wdrożeniowe chmury mogą [kompilować empatię klienta](./build.md) przy użyciu tylko danych i szybko rozwiązywać istniejące potrzeby klientów.

## <a name="process-of-democratizing-data"></a>Proces danych democratizing

Poniższe etapy przeprowadzą decyzje i podejścia wymagane do przyjęcia rozwiązania, które demokratyzuje dane. Nie każda faza musi być wymagana do utworzenia określonego rozwiązania. Należy jednak ocenić każdą fazę, gdy tworzysz rozwiązanie do hipotezy klienta. Każdy z nich stanowi unikatowe podejście do tworzenia innowacyjnych rozwiązań.

![Proces dla danych democratizing](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Udostępnianie danych

Gdy [kompilujesz się z empatię klienta](./build.md), wszystkie procesy podnieśą potrzebę klienta w porównaniu z rozwiązaniem technicznym. Ponieważ dane democratizing nie są wyjątkiem, zaczynamy od udostępnienia danych. Aby zdemokratyzuj proces dane, musi on zawierać rozwiązanie, które udostępnia dane konsumentowi danych. Konsumentem danych może być bezpośredni klient lub serwer proxy, który podejmuje decyzje dla klientów. Zatwierdzeni użytkownicy danych mogą analizować, przejrzeć i raportować dane scentralizowanych danych bez wsparcia dla personelu działu IT.

Wiele udanych innowacji zostało uruchomionych jako minimalny produkt żywotny (MVP), który umożliwia ręczne dostarczanie procesów opartych na danych w imieniu klienta. W tym modelu Concierge pracownik jest odbiorcą danych. Pracownik korzysta z danych, aby pomóc klientowi. Za każdym razem, gdy klient przeprowadzi ręczną pomoc techniczną, hipoteza może zostać przetestowana i sprawdzona. Takie podejście jest często ekonomicznie sposobem na testowanie hipotezy skoncentrowanej na kliencie przed zainwestowaniem w zintegrowane rozwiązania.

Podstawowe narzędzia do udostępniania danych bezpośrednio z użytkownikami danych obejmują raporty samoobsługowe lub dane osadzone w innych środowiskach przy użyciu narzędzi takich jak [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Przed udostępnieniem danych upewnij się, że zostały one opisane w poniższych sekcjach. Udostępnianie danych może wymagać od ładu zapewnienia ochrony danych udostępnionych. Ponadto te dane mogą być rozłożone między wiele chmur i mogą wymagać scentralizowania. Większość danych może nawet znajdować się w aplikacjach, co wymaga zbierania danych, zanim będzie można je udostępnić.

### <a name="govern-data"></a>Zarządzanie danymi

Udostępnianie danych może szybko utworzyć MVP, którego możesz używać w konwersacjach klientów. Jednak aby przekształcić udostępnione dane w użyteczne i funkcjonalne informacje, jest to zwykle wymagane. Po sprawdzeniu hipotezy przy użyciu udostępniania danych kolejnym etapem programowania jest zwykle zarządzanie danymi.

Zarządzanie danymi jest szerokim tematem, który może wymagać własnej dedykowanej struktury. Ten stopień szczegółowości jest poza zakresem [struktury wdrożenia chmury](../../index.yml). Istnieje jednak kilka aspektów nadzoru nad danymi, które należy wziąć pod uwagę zaraz po sprawdzeniu poprawności hipotezy klienta. Przykład:

- **Czy dane są udostępnione poufne?** [Dane powinny zostać sklasyfikowane](../../govern/policy-compliance/data-classification.md) przed udostępnieniem publicznie, aby chronić interesy klientów i firmę.
- **Czy dane są poufne, czy zostały zabezpieczone?** Ochrona danych poufnych powinna być wymagana w przypadku dowolnych danych z demokratyzacją. Przykładowe obciążenie dotyczące [zabezpieczania rozwiązań danych](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions) zawiera kilka odwołań do zabezpieczania danych.
- **Czy dane są z katalogu?** Przechwycenie szczegółowych informacji o udostępnianych danych będzie pomocne w zarządzaniu długoterminowymi danymi. Narzędzia do dokumentowania danych, takie jak Azure Data Catalog, mogą znacznie ułatwić ten proces w chmurze. Wskazówki dotyczące [adnotacji danych](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) i [dokumentacji źródeł danych](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) mogą pomóc przyspieszyć proces.

Gdy Democratization danych jest istotna dla hipotez ukierunkowanych na klienta, upewnij się, że zarządzanie danymi udostępnionymi znajduje się w planie zlecenia. Pomoże to chronić klientów, konsumentów danych i firmę.

### <a name="centralize-data"></a>Centralizowanie danych

Gdy dane są zakłócone w środowisku IT, szanse na innowacje mogą być wyjątkowo ograniczone, kosztowne i czasochłonne. Chmura udostępnia nowe możliwości w celu scentralizowania danych między silosami danych. Gdy do [kompilowania z empatię klienta](./build.md)jest wymagane scentralizowanie wielu źródeł danych, Chmura może przyspieszyć testowanie hipotez.

> [!CAUTION]
> Scentralizowanie danych reprezentuje punkt ryzyka w procesie innowacji. Gdy centralizacji danych jest [technicznym](./build.md#reduce-complexity-and-delay-technical-spikes)wzrostem, a nie źródłem wartości klienta, sugerujemy, aby można było opóźnić scentralizowanie do momentu zweryfikowania postanowień klienta.

Jeśli jest wymagane scentralizowanie danych, należy najpierw zdefiniować odpowiedni magazyn danych dla scentralizowanych danych. Dobrym sposobem jest ustanowienie magazynu danych w chmurze. Ta skalowalna opcja zapewnia centralną lokalizację dla wszystkich danych. Ten typ rozwiązania jest dostępny w opcjach przetwarzania analitycznego online (OLAP) lub danych Big Data.

Architektury referencyjne dla rozwiązań [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) i [danych Big Data](https://docs.microsoft.com/azure/architecture/data-guide/big-data) mogą pomóc wybrać najbardziej odpowiednie rozwiązanie na platformie Azure. Jeśli jest wymagane rozwiązanie hybrydowe, architektura referencyjna umożliwiająca [rozszerzanie danych lokalnych](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) może również przyspieszyć opracowywanie rozwiązań.

> [!IMPORTANT]
> W zależności od potrzeb klientów i wyrównane rozwiązanie może być wystarczające. Architekt chmury powinien zwrócić się do zespołu w celu uwzględnienia niższych rozwiązań kosztów, które mogłyby spowodować szybsze sprawdzanie poprawności hipotezy klienta, szczególnie podczas wczesnego rozwoju. Poniższa sekcja dotycząca zbierania danych obejmuje niektóre scenariusze, które mogą zasugerować inne rozwiązanie w danej sytuacji.

### <a name="collect-data"></a>Zbieranie danych

Gdy potrzebujesz, aby dane były scentralizowane w celu sprostania potrzebom klientów, bardzo prawdopodobnie trzeba będzie zebrać dane z różnych źródeł i przenieść je do scentralizowanego magazynu danych. Istnieją dwa podstawowe formy zbierania danych: _integracja_ i pozyskiwanie _ingestion_.

**Integracja:** Dane, które znajdują się w istniejącym magazynie danych, można zintegrować z scentralizowanym magazynem danych przy użyciu tradycyjnych technik przenoszenia danych. Jest to szczególnie typowe w przypadku scenariuszy obejmujących magazyn danych w chmurze. Te techniki obejmują wyodrębnianie danych z istniejącego magazynu danych, a następnie ładowanie ich do centralnego magazynu danych. W pewnym momencie w tym procesie dane są zwykle przekształcane, aby były bardziej użyteczne i istotne w sklepie centralnym.

Narzędzia oparte na chmurze zostały zastosowane do narzędzi do płacenia za użycie, co zmniejsza barierę do wprowadzenia do zbierania i scentralizowania danych. Narzędzia takie jak Azure Database Migration Service i Azure Data Factory są dwa przykłady. Przykładem takiego rozwiązania jest architektura referencyjna dla usługi [Fabryka danych z magazynem danych OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) .

Pozyskiwanie **:** Niektóre dane nie znajdują się w istniejącym magazynie danych. Gdy dane przejściowe są podstawowym źródłem innowacji, warto rozważyć alternatywne podejścia. Przejściowe dane można znaleźć w różnych istniejących źródłach, takich jak aplikacje, interfejsy API, strumienie danych, urządzenia IoT, łańcucha bloków, pamięć podręczna aplikacji, zawartość multimedialna, a nawet w plikach prostych.

Te różne formy danych można zintegrować z centralnym magazynem danych w ramach rozwiązania OLAP lub danych Big Data. Jednak w przypadku wczesnych iteracji kompilacja – pomiar — uczenie się w cyklu przetwarzania transakcyjnego online (OLTP) może być większe niż wystarczające, aby sprawdzić hipotezę klienta. Rozwiązania OLTP nie są rozwiązaniem najwyższej jakości w żadnym scenariuszu sprawozdawczym. Jednak w przypadku [kompilowania z empatię klienta](./build.md)należy skupić się na potrzebach klientów niż w podejmowaniu decyzji dotyczących narzędzi technicznych. Po sprawdzeniu poprawności hipotezy klienta na dużą skalę może być wymagana bardziej odpowiednia platforma. Architektura referencyjna w [magazynach danych OLTP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) może pomóc w ustaleniu, który magazyn danych jest odpowiedni dla danego rozwiązania.

**Wirtualizacja:** Integracja i pozyskiwanie danych może czasami spowolnić innowacje. Gdy rozwiązanie do wirtualizacji danych jest już dostępne, może ono przedstawiać bardziej racjonalne podejście. Pozyskiwanie i integracja pozwala na duplikowanie wymagań dotyczących magazynu i rozwoju, Dodawanie opóźnień danych, zwiększanie obszaru podatności na ataki i wyzwolenie problemów z jakością oraz zwiększenie wysiłków ładu. Wirtualizacja danych to bardziej współczesna alternatywa, która pozostawia oryginalne dane w jednej lokalizacji i tworzy zapytania przekazywane lub buforowane z danymi źródłowymi.

SQL Server 2017 i Azure SQL Data Warehouse obu typów [obsługi,](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)który jest podejściem do wirtualizacji danych najczęściej używanym na platformie Azure.

## <a name="next-steps"></a>Następne kroki

Mając strategię dotyczącą democratizing danych, następnie chcesz oszacować podejścia do [zaangażowania klientów za pomocą aplikacji](./apps.md).

> [!div class="nextstepaction"]
> [Angażowanie klientów za poorednictwem aplikacji](./apps.md)
