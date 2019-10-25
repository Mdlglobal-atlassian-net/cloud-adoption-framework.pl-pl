---
title: 'Innowacje w chmurze: dane Zdemokratyzuj proces'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — dane Zdemokratyzuj proces
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 80cd8c74f283436d9f32ce647c27bb7c67d3c92c
ms.sourcegitcommit: 15898374495761bfb76cee719e0f9189856884e6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/24/2019
ms.locfileid: "72888888"
---
# <a name="democratize-data"></a>Zdemokratyzuj proces dane

Potencjał węgla, ropy naftowej i ludzi był trzema najbardziej wynikowymi zasobami w trakcie rewolucji przemysłowej. Te zasoby są tworzone przez firmy, przesunięte rynki i ostatecznie zmienione. W przypadku oszczędności cyfrowych istnieją trzy równe zasoby: dane, urządzenia i potencjał ludzki. Każdy z tych zasobów jest doskonałym potencjałem innowacji. W ramach każdego wysiłku innowacji dane są nową olejem.

W każdej firmie dzisiaj istnieją kieszenie danych, które mogą zostać użyte do szybszego znajdowania i zaspokajania potrzeb klientów. Niestety, proces wyszukiwania danych na potrzeby innowacji jest kosztowny i czasochłonny. Wiele z najbardziej cennych rozwiązań dla klientów to niewypełnienia, ponieważ odpowiednie osoby nie mogą uzyskać dostępu do potrzebnych danych.

Democratization danych to proces uzyskiwania tych danych do właściwych rąk związanych z wprowadzaniem innowacji. Ten proces może potrwać kilka kształtów, ale ogólnie obejmują rozwiązania pozyskiwania lub zintegrowanego przetwarzania danych pierwotnych, scentralizowania danych, udostępniania danych i zabezpieczania danych. Po pomyślnym przeprowadzeniu ekspertów w firmie może wykorzystać dane do przetestowania tych danych. W wielu przypadkach zespoły wdrożeniowe chmury mogą [kompilować empatię klienta](./build.md) przy użyciu tylko danych, co skutkuje szybkim wpływem na potrzeby istniejących klientów.

## <a name="process-of-democratizing-data"></a>Proces danych democratizing

Poniższe etapy przeprowadzą decyzje i podejścia wymagane do przyjęcia rozwiązania, które demokratyzuje dane. Poszczególne fazy mogą nie być wymagane do utworzenia określonego rozwiązania. Należy jednak ocenić każdy podczas kompilowania rozwiązania do hipotezy klienta. Każdy z nich stanowi unikatowe podejście do tworzenia innowacyjnych rozwiązań.

![Proces dla danych democratizing](../../_images/innovate/democratize-data.png)

### <a name="share-data"></a>Udostępnianie danych

Podczas [kompilowania za pomocą empatię klienta](./build.md)wszystkie procesy koncentrują się na klientach w rozwiązaniu technicznym. Democratizing dane nie są wyjątkiem, więc zaczynamy od udostępniania danych. Aby zdemokratyzuj proces dane, musi on zawierać rozwiązanie, które udostępnia dane konsumentowi danych. Konsumentem danych może być bezpośredni klient lub serwer proxy, który podejmuje decyzje dla klientów. Zatwierdzeni użytkownicy z danymi mogą analizować, przejrzeć i raportować dane dotyczące scentralizowanych danych bez wsparcia dla personelu działu IT.

Wiele udanych innowacji zostało uruchomionych jako MVP, które dostarczają ręcznych procesów opartych na danych w imieniu klienta. W tym modelu Concierge pracownik jest odbiorcą danych. Pracownik korzysta z danych, aby pomóc klientowi. Za każdym razem, gdy klient powiąże się z ręczną pomocą techniczną, hipoteza może zostać przetestowana i sprawdzona. Takie podejście jest często ekonomicznie sposobem na testowanie hipotezy skoncentrowanej na kliencie przed zainwestowaniem w zintegrowane rozwiązania.

Podstawowe narzędzia do udostępniania danych bezpośrednio dla odbiorców danych obejmują samoobsługowe raportowanie lub dane osadzone w innych środowiskach przy użyciu narzędzi takich jak [Power BI](https://docs.microsoft.com/power-bi).

> [!NOTE]
> Przed udostępnieniem danych należy pamiętać o następujących sekcjach. Udostępnianie danych może wymagać zarządzania w celu zapewnienia ochrony danych udostępnionych. Dalsze dane mogą być rozłożone między wiele chmur i mogą wymagać scentralizowania. Większość danych może nawet znajdować się w aplikacjach, które będą wymagały zbierania danych przed ich udostępnieniem.

### <a name="govern-data"></a>Zarządzanie danymi

Udostępnianie danych może szybko utworzyć SPECJALISTę, który może być używany w konwersacjach klientów. Jednak same dane to tylko dane. Aby przekształcić udostępnione dane w wiedzę z możliwością podejmowania działań, często wymagane jest zwiększenie liczby bitów. Po sprawdzeniu hipotezy przy użyciu udostępniania danych kolejna faza rozwoju jest często zarządzaniem danymi.

Zarządzanie danymi jest szerokim tematem, który może wymagać jego własnej dedykowanej struktury. Jest to poza zakresem [struktury wdrożenia chmury](../../index.md). Istnieje jednak kilka aspektów nadzoru nad danymi, które należy wziąć pod uwagę, gdy tylko zostanie sprawdzona hipoteza klienta. Poniżej przedstawiono kilka przykładów tych pytań:

- **Czy dane są udostępnione poufne?** [Dane powinny być klasyfikowane](../../govern/policy-compliance/data-classification.md) przed wszelkimi publicznymi udziałami w celu ochrony interesów klientów i firmy.
- **Czy dane są poufne, czy zostały zabezpieczone?** Ochrona danych poufnych powinna być wymagana w przypadku dowolnych danych z demokratyzacją. Przykładowe obciążenie dotyczące [zabezpieczania rozwiązań danych](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/securing-data-solutions) zawiera kilka odwołań do zabezpieczania danych.
- **Czy dane są w wykazie?** Przechwycenie szczegółowych informacji o udostępnianych danych będzie pomocne w zarządzaniu długoterminowymi danymi. Narzędzia do dokumentowania danych, takie jak Azure Data Catalog, mogą znacznie ułatwić ten proces w chmurze. Wskazówki dotyczące [adnotacji danych](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-annotate) i [dokumentacji źródeł danych](https://docs.microsoft.com/azure/data-catalog/data-catalog-how-to-documentation) mogą pomóc przyspieszyć proces.

Gdy Democratization danych jest ważne dla hipotez ukierunkowanych na klienta, zarządzanie danymi udostępnionymi powinno znajdować się w tym miejscu w planie wydania, aby chronić klientów, odbiorców danych i firmę.

### <a name="centralize-data"></a>Scentralizowanie danych

Gdy dane są zakłócone w środowisku IT, szanse na innowacje mogą być wyjątkowo ograniczone, kosztowne i czasochłonne. Chmura udostępnia nowe możliwości w celu scentralizowania danych między różnymi silosami danych. Gdy jest wymagane scentralizowanie wielu źródeł danych do [kompilowania przy użyciu usługi Customer empatię](./build.md) , Chmura może przyspieszyć testowanie hipotez.

> [!CAUTION]
> Scentralizowanie danych jest typowym ryzykiem w każdym procesie innowacji. Gdy centralizacji danych jest [technicznym](./build.md#reduce-complexity-and-delay-technical-spikes)wzrostem, w przeciwieństwie do źródła wartości klienta, sugerowane jest opóźnienie centralizacji do momentu zweryfikowania hipotezy klienta.

Jeśli jest wymagane scentralizowanie danych, pierwszym krokiem jest zdefiniowanie odpowiedniego magazynu danych dla danych scentralizowanych. Zalecanym podejściem jest ustanowienie magazynu danych w chmurze. Ta skalowalna opcja zapewni centralne miejsce dla wszystkich danych. Ten typ rozwiązania jest dostępny w opcjach przetwarzania analitycznego online (OLAP) lub danych Big Data.

Architektury referencyjne dla rozwiązań [OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-analytical-processing) i [danych Big Data](https://docs.microsoft.com/azure/architecture/data-guide/big-data) mogą pomóc w wyborze najbardziej odpowiedniego rozwiązania na platformie Azure. Jeśli jest wymagane rozwiązanie hybrydowe, architektura referencyjna umożliwiająca [rozszerzanie danych lokalnych](https://docs.microsoft.com/azure/architecture/data-guide/scenarios/hybrid-on-premises-and-cloud) może również przyspieszyć opracowywanie rozwiązań.

> [!IMPORTANT]
> W zależności od potrzeb klientów i rozwiązania wyrównane rozwiązanie może być wystarczające. Architekt chmury powinien zwrócić się do zespołu w celu uwzględnienia niższych rozwiązań kosztów, które mogłyby spowodować szybsze sprawdzanie poprawności hipotezy klienta, szczególnie podczas wczesnego rozwoju. Sekcja dotycząca zbierania danych poniżej spowoduje utworzenie konspektu kilku scenariuszy, które mogą monitować o inne rozwiązanie.

### <a name="collect-data"></a>Zbieranie danych

Gdy dane muszą być scentralizowane w celu zapewnienia potrzeby klienta, bardzo prawdopodobnie trzeba będzie zbierać dane z różnych źródeł i przenosić je do scentralizowanego magazynu danych. Istnieją dwa podstawowe formy zbierania danych: integracja i pozyskiwanie. Każdy z nich zapewnia inny sposób zbierania danych.

**Integracja:** Istniejące dane, które znajdują się w istniejącym magazynie danych, można zintegrować z scentralizowanym magazynem danych przy użyciu tradycyjnych technik przenoszenia danych. Jest to szczególnie typowe w przypadku scenariuszy obejmujących magazyn danych w chmurze. Te techniki składają się z wyodrębniania danych z istniejącego magazynu danych. Następnie ładowania danych do centralnego magazynu danych. W pewnym momencie w tym procesie dane są często przekształcane, aby były bardziej użyteczne i istotne w sklepie centralnym.

Narzędzia oparte na chmurze przenoszą te techniki do narzędzi do użycia z opcją płatność za użycie, co zmniejsza barierę do wprowadzenia do zbierania i scentralizowania danych. Narzędzia, takie jak Data Migration Service i Data Factory, to dwa typowe przykłady na platformie Azure. Przykładem takiego rozwiązania jest architektura referencyjna dla usługi [Fabryka danych z magazynem danych OLAP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/etl) .

Pozyskiwanie **:** Niektóre dane nie znajdują się w żadnym z istniejących magazynów danych. Gdy dane przejściowe są podstawowym źródłem innowacji, należy rozważyć alternatywne podejścia. Przejściowe dane można znaleźć w różnych istniejących źródłach, takich jak aplikacje, interfejsy API, strumienie danych, urządzenia IoT, łańcucha bloków, pamięć podręczna aplikacji, zawartość multimedialna lub nawet pliki proste.

Te różne formy danych można zintegrować z centralnym magazynem danych w ramach rozwiązania OLAP lub danych Big Data. Jednak w przypadku wczesnych iteracji dla cykli kompilacji, przetwarzanie transakcyjne online (OLTP) może być większe niż wystarczające, aby sprawdzić hipotezę klienta. Rozwiązania OLTP nie stanowią najwyższej jakości rozwiązania do raportowania. Jednak w przypadku [kompilowania z klientem empatię](./build.md) na potrzeby klienta ma wyższy priorytet niż decyzje dotyczące narzędzi technicznych. Gdy hipoteza klienta zostanie zweryfikowana na dużą skalę, może być wymagana bardziej odpowiednia platforma. Architektura referencyjna w [magazynach danych OLTP](https://docs.microsoft.com/azure/architecture/data-guide/relational-data/online-transaction-processing) może pomóc w ustaleniu, który magazyn danych jest odpowiedni dla danego rozwiązania.

**Wirtualizacja:** Integracja i pozyskiwanie danych może czasami spowolnić innowacje. Jeśli rozwiązanie do wirtualizacji danych jest już dostępne, może to być bardziej odpowiednie podejście. Pozyskiwanie i integracja pozwala na duplikowanie wymagań dotyczących magazynu/programowania, Dodawanie opóźnień danych, zwiększanie obszaru podatności na ataki, iniekcje problemów z jakością i zwiększanie wysiłków ładu. Wirtualizacja danych to bardziej nowoczesny alternatywa, która pozostawia oryginalne dane w jednej lokalizacji i tworzy przekazujące lub buforowane zapytania dotyczące danych źródłowych.

SQL Server 2017 i Azure SQL Data Warehouse obu typów [obsługi,](/sql/relational-databases/polybase/polybase-guide) który jest podejściem do wirtualizacji danych najczęściej używanym na platformie Azure.

## <a name="next-steps"></a>Następne kroki

Przy użyciu strategii democratizing danych na miejscu następnym krokiem jest oszacowanie podejścia do [zaangażowania klientów za pomocą aplikacji](./apps.md).

> [!div class="nextstepaction"]
> [Angażowanie klientów za poorednictwem aplikacji](./apps.md)
