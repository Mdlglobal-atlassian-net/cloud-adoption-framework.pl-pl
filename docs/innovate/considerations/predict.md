---
title: Przewidywanie i wpływ na zachowanie klienta
description: Korzystanie z modelowania predykcyjnego w celu opracowywania funkcji predykcyjnych za pomocą danych, szczegółowych informacji, wzorców, prognoz i interakcji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: bbbed6fd267a6cac7b052c28a0b902c233d74374
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80427372"
---
# <a name="predict-and-influence"></a>Przewidywanie i wpływ

Istnieją dwie klasy aplikacji w gospodarce cyfrowej: *historyczne* i *predykcyjne*. Wiele potrzeb klientów można spełnić wyłącznie przy użyciu danych historycznych, w tym niemal danych w czasie rzeczywistym. Większość rozwiązań koncentruje się głównie na agregowaniu danych. Następnie przetwarzają i udostępniają te dane z powrotem do klienta w formie środowiska cyfrowego lub otoczenia.

Ponieważ modelowanie predykcyjne jest bardziej opłacalne i łatwo dostępne, klienci będą mogli korzystać z wydajnych środowisk, które prowadzą do lepszego podejmowania decyzji i działań. Jednak żądanie nie zawsze sugeruje rozwiązanie predykcyjne. W większości przypadków widok historyczny może zapewnić wystarczającą ilość danych, aby umożliwić klientowi samodzielne podejmowanie decyzji.

Niestety, klienci często mają widok Myopic, który prowadzi do decyzji na podstawie ich natychmiastowego otoczenia i sfery wpływu. Ponieważ opcje i decyzje zwiększają liczbę i wpływ, ten widok Myopic może nie spełniać potrzeb klientów. W tym samym czasie, gdy hipoteza jest sprawdzana na dużą skalę, firma dostarczająca rozwiązanie może zobaczyć tysiące lub miliony decyzji klientów. Takie podejście Big-Picture sprawia, że można zobaczyć szerokie wzorce i wpływ tych wzorców. Funkcja predykcyjna to poważniejsze inwestycje, gdy zrozumienie tych wzorców jest niezbędne do podejmowania decyzji, które najlepiej obsłużyć klienta.

## <a name="examples-of-predictions-and-influence"></a>Przykłady prognoz i wpływu

Różne aplikacje i środowiska otoczenia wykorzystują dane do prognozowania:

- **Handel elektroniczny:** W oparciu o zakupione inne osoby, witryna internetowa handlu elektronicznego sugeruje produkty, które mogą być dodawane do koszyka.
- **Zastosowana rzeczywistość:** IoT oferuje bardziej zaawansowane wystąpienia funkcji predykcyjnych. Na przykład urządzenie w wierszu zestawu wykrywa wzrost temperatury maszyny. Oparty na chmurze model predykcyjny określa, jak odpowiedzieć. Na podstawie tego przewidywania inne urządzenie spowalnia linię zestawu do momentu, aż maszyna będzie mogła chłodnić.
- **Produkty konsumenckie:** Telefony komórkowe, domy i sieci, a nawet samochody — wszystkie wykorzystują funkcje predykcyjne, których wykorzystują, aby zasugerować zachowanie użytkowników w oparciu o czynniki takie jak lokalizacja lub dzień. Gdy prognozowanie i hipoteza wstępna są wyrównane, Prognoza prowadzi do działania. W bardzo wczesnym etapie to wyrównanie może sprawiać, że produkty takie jak samodzielny samochód są w rzeczywistości.

## <a name="develop-predictive-capabilities"></a>Opracowywanie funkcji predykcyjnych

Rozwiązania, które regularnie zapewniają dokładne Funkcje predykcyjne, zazwyczaj obejmują pięć podstawowych cech: *dane*, *szczegółowe informacje*, *wzorce*, *przewidywania*i *interakcje*. Każdy aspekt jest wymagany do opracowania funkcji predykcyjnych. Podobnie jak w przypadku wszystkich wspaniałych innowacji, rozwój możliwości predykcyjnych wymaga [zobowiązania do iteracji](./index.md#commitment-to-iteration). W każdej iteracji jedna lub więcej z następujących cech jest przedwcześnie w celu zweryfikowania coraz większej liczby skomplikowanych klientów.

![Kroki do predykcyjnych funkcji](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Jeśli hipoteza klienta opracowana w [ramach kompilacji z empatię klienta](./build.md) obejmuje funkcje predykcyjne, opisane zasady mogą być stosowane. Jednak funkcje predykcyjne wymagają znaczących inwestycji w czas i energię. W przypadku, gdy funkcje predykcyjne są osiągnięciami [technicznymi](./build.md#reduce-complexity-and-delay-technical-spikes), a nie ze źródłem prawdziwej wartości klienta, sugerujemy, aby opóźnić przewidywania do momentu zweryfikowania postanowień klienta w odpowiedniej skali.

## <a name="data"></a>Dane

Dane to większość cech wymienionych wcześniej. Każda z dyscyplin związanych z programowaniem cyfr cyfrowych generuje dane. Te dane oczywiście przyczyniają się do rozwoju prognoz. Aby uzyskać więcej wskazówek na temat sposobów pobierania danych do rozwiązania predykcyjnego, zobacz [Democratizing Data](./data.md) and [współdziała z urządzeniami](./devices.md).

Różne źródła danych mogą służyć do dostarczania funkcji predykcyjnych:

## <a name="insights"></a>Insights

Eksperci z branży wykorzystują dane dotyczące potrzeb klientów i zachowań, aby opracowywać podstawowe informacje biznesowe z badania danych pierwotnych. Te szczegółowe informacje mogą wskazywać wystąpienia żądanych zachowań klientów (lub, w tym niepożądane wyniki). Podczas iteracji w prognozach te szczegółowe informacje mogą pomóc w zidentyfikowaniu potencjalnych korelacji, które ostatecznie generują pozytywne wyniki. Aby uzyskać wskazówki dotyczące włączania ekspertów z dziedziny, zobacz [dane Democratizing](./data.md).

## <a name="patterns"></a>Wzorce

Osoby zawsze próbowały wykrywać wzorce w dużych ilościach danych. Komputery zostały zaprojektowane do tego celu. Uczenie maszynowe przyspiesza to dzięki wykrywaniu precyzyjnych wzorców, które obejmują model uczenia maszynowego. Wzorce te są następnie stosowane za pomocą algorytmów uczenia maszynowego do przewidywania wyników, gdy nowy zestaw danych jest wprowadzany do algorytmów.

Korzystając z wglądu w dane jako punkt wyjścia, uczenie maszynowe opracowuje i stosuje modele predykcyjne w celu użycia wzorców w danych. Dzięki wielu iteracjom szkoleń, testowania i wdrażania te modele i algorytmy mogą dokładnie przewidzieć przyszłe wyniki.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) to usługa w chmurze na platformie Azure do kompilowania i uczenia modeli na podstawie danych. To narzędzie obejmuje również [przepływ pracy przyspieszania opracowywania algorytmów uczenia maszynowego](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Tego przepływu pracy można użyć do opracowania algorytmów za pomocą interfejsu wizualnego lub języka Python.

Aby uzyskać bardziej niezawodne modele uczenia maszynowego, [usługi ml w usłudze Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) zapewniają platformę uczenia maszynowego utworzoną na Apache Hadoop klastrów. Takie podejście umożliwia bardziej szczegółową kontrolę nad źródłowymi klastrami, magazynem i węzłami obliczeniowymi. Usługa Azure HDInsight oferuje również bardziej zaawansowaną integrację za pomocą narzędzi, takich jak skalowanie i platforma Spark, w celu tworzenia prognoz opartych na zintegrowanych i pozyskiwanych danych, nawet w pracy z danymi ze strumienia. [Rozwiązanie do prognozowania opóźnień lotów](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) pokazuje każdą z zaawansowanych możliwości, które są używane do przewidywania opóźnień lotów na podstawie warunków pogodowych. Rozwiązanie HDInsight umożliwia również kontrolę nad przedsiębiorstwami, takimi jak bezpieczeństwo danych, dostęp do sieci i monitorowanie wydajności.

## <a name="predictions"></a>Prognozy

Po skompilowaniu i przeszkoleniu wzorca można zastosować go za pomocą interfejsów API, co może powodować przewidywania podczas dostarczania cyfrowego środowiska. Większość z tych interfejsów API jest zbudowana z dobrze przeszkolonych modeli opartych na wzorcu danych. Gdy coraz więcej klientów wdraża codzienne obciążenia w chmurze, interfejsy API przewidywania używane przez dostawców chmury prowadzą do szybszego wdrażania.

[Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services) to przykład PREDYKCYJNEGO interfejsu API utworzonego przez dostawcę chmury. Ta usługa obejmuje interfejsy API predykcyjne służące do moderowania zawartości, wykrywania anomalii oraz sugestie dotyczące personalizowania zawartości. Te interfejsy API są gotowe do użycia i są oparte na dobrze znanych wzorcach zawartości, które firma Microsoft używa do uczenia modeli. Każdy z tych interfejsów API wykonuje prognozy na podstawie danych, które są podawane do interfejsu API.

[Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) umożliwia wdrożenie niestandardowych algorytmów, które można tworzyć i wyszkolić wyłącznie na podstawie własnych danych. Dowiedz się więcej o wdrażaniu prognoz przy użyciu [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where).

[Konfiguracja klastrów usługi HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) omawia procesy umożliwiające Uwidacznianie prognoz utworzonych dla usług ml w usłudze Azure HDInsight.

## <a name="interactions"></a>Interakcje

Po udostępnieniu prognoz za pomocą interfejsu API można jej użyć w celu wywierania wpływu na zachowanie klienta. Ma to wpływ na formę interakcji. Interakcja z algorytmem uczenia maszynowego odbywa się w innych środowiskach cyfrowych lub otoczenia. Ponieważ dane są zbierane za pomocą aplikacji lub środowiska, są uruchamiane za pomocą algorytmów uczenia maszynowego. Gdy algorytm przewiduje wynik, to prognozowanie może być współużytkowane z klientem za pomocą istniejącego środowiska.

Dowiedz się więcej na temat sposobu tworzenia środowiska otoczenia poprzez [roztwory o rzeczywistości](./devices.md#adjusted-reality).

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [dyscyplinami wynalazku](./invention.md) i [metodologią innowacji](./index.md), możesz teraz przystąpić do uczenia się, jak [tworzyć za pomocą empatię klientów](./build.md).

> [!div class="nextstepaction"]
> [Kompiluj z empatię](./build.md)
