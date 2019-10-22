---
title: 'Innowacje w chmurze: przewidywanie i wpływ'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — przewidywanie i wpływ
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: e6187bc926aacd9a09e67b8cd2bfe94e5a4a42dd
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72682622"
---
# <a name="predict-and-influence"></a>Przewidywanie i wpływ

Istnieją dwie klasy aplikacji w gospodarce cyfrowej: historyczne i predykcyjne. Wiele potrzeb klientów można spełnić wyłącznie przy użyciu danych historycznych, w tym niemal danych w czasie rzeczywistym. Większość rozwiązań koncentruje się głównie na agregowaniu danych. Następnie przetwarzają i udostępniają te dane z powrotem do klienta w formie środowiska cyfrowego lub otoczenia.

Ponieważ modelowanie predykcyjne jest tańsze i łatwo dostępne, środowisko do przesyłania dalej na żądanie klientów pozwala na lepsze podejmowanie decyzji i działań. Jednak ten popyt nie zawsze musi prowadzić do rozwiązania predykcyjnego. W większości scenariuszy widok historyczny może zapewnić wystarczającą ilość danych, aby umożliwić klientowi samodzielne podejmowanie decyzji.

Niestety, klienci mają widok Myopic, który prowadzi do decyzji na podstawie ich natychmiastowego otoczenia i sfery wpływu. W miarę jak opcje i decyzje zwiększają się w liczbie i wpływie, ten widok Myopic może nie prowadzić do spełnienia potrzeby klienta. W tym samym czasie, gdy hipoteza jest sprawdzana na dużą skalę, firma dostarczająca rozwiązanie może zobaczyć tysiące lub miliony decyzji klientów. Istnieje możliwość wyświetlenia wzorców i wpływu tych wzorców. Funkcja predykcyjna jest inwestowana, gdy zrozumienie tych wzorców jest wymagane do podejmowania decyzji, które spełniają potrzeby klientów.

## <a name="examples-of-predictions-and-influence"></a>Przykłady prognoz i wpływu

Korzystanie z danych w celu tworzenia prognoz można zobaczyć w różnych aplikacjach i otoczenia.

- **handlu elektronicznego:** Sugerowane elementy to przykładowe przewidywania. W zależności od tego, co inni zakupiły, witryna sieci Web może sugerować produkty, które mogą być dodawane do koszyka.
- **Zastosowana rzeczywistość:** Oferta IoT oferuje bardziej zaawansowane przykłady. Jedno urządzenie w wierszu zestawu wykrywa wzrost temperatury maszyn. Oparty na chmurze model predykcyjny określa, jak odpowiedzieć. W oparciu o takie przewidywania inne urządzenie jest nakazać spowolnieniu linii montażowej, dopóki maszyna nie będzie chłodna.
- **Produkty konsumenckie:** Telefony komórkowe, domy., a nawet cały samochód zawierają pewną część możliwości predykcyjnych, sugerując działania oparte na czynnikach, takich jak lokalizacja lub dzień. Gdy prognozowanie i hipoteza początkowa są wyrównane, te przewidywania wpływają na Twoje zachowania. Gdy obie stają się bardzo dojrzałe, Prognoza prowadzi do działania, takiego jak samochód samodzielny.

## <a name="developing-predictive-capabilities"></a>Opracowywanie funkcji predykcyjnych

Rozwiązania, które regularnie zapewniają dokładne Funkcje predykcyjne, zazwyczaj obejmują pięć podstawowych cech: dane, szczegółowe informacje, wzorce, przewidywania i interakcje. Każda z nich jest wymagana do opracowania funkcji predykcyjnych. Podobnie jak w przypadku wszystkich wspaniałych innowacji, rozwój możliwości predykcyjnych będzie wymagał [zobowiązania do iteracji](./index.md#commitment-to-iteration). W każdej iteracji jedna lub więcej z następujących cech zostanie przedwcześnie w celu zweryfikowania coraz bardziej złożonych zaszeregów klientów.

![Kroki do predykcyjnych funkcji](../../_images/innovate/predict-and-influence.png)

> [!CAUTION]
> Jeśli hipoteza klienta opracowana z myślą o rozpoczęciu [kompilacji z artykułem empatię klienta](./build.md) obejmuje funkcje predykcyjne, może to dotyczyć tego artykułu. Jednak funkcje predykcyjne wymagają znaczących inwestycji związanych z czasem i energią. Gdy możliwości predykcyjne są [skokami technicznymi](./build.md#reduce-complexity-and-delay-technical-spikes), w przeciwieństwie do źródła osiągalnej wartości klienta, sugerowane jest opóźnienie prognoz do momentu zweryfikowania hipotezy dla klientów na dużą skalę.

## <a name="data"></a>Dane

Najłatwiejszym z powyższych cech są dane. Każda z wcześniejszych dyscyplin związanych z tworzeniem wynalazków cyfrowych spowoduje wygenerowanie danych. Te dane mogą przyczynić się do rozwoju prognoz. Aby uzyskać więcej wskazówek na temat sposobów pobierania danych do rozwiązania predykcyjnego, zobacz artykuły dotyczące [democratizing danych](./data.md) lub [manipulowania urządzeniami](./devices.md).

Niektóre źródła danych mogą służyć do dostarczania funkcji predykcyjnych:

## <a name="insights"></a>Szczegółowe informacje

Eksperci z dziedziny wykorzystują dane dotyczące potrzeb klientów i zachowań, aby rozwijać podstawowe informacje biznesowe z badania danych pierwotnych. Te szczegółowe informacje mogą wskazywać wystąpienia żądanych zachowań klientów (lub alternatywne wyniki niepożądane). Podczas iteracji w prognozach te informacje mogą pomóc w zidentyfikowaniu potencjalnych korelacji, które mogą mieć wpływ na pozytywne wyniki. Aby uzyskać wskazówki dotyczące włączania ekspertów z dziedziny, zobacz artykuł dotyczący [democratizing danych](./data.md).

## <a name="patterns"></a>Wzorce

Ludzkie problemy związane z wykrywaniem wzorców w dużych ilościach danych. Komputery zostały zaprojektowane do tego celu. Uczenie maszynowe przyspiesza ten cel dzięki wykrywaniu wzorców w dużej ilości danych, nazywanych modelem uczenia maszynowego. Te wzorce są następnie stosowane za pomocą algorytmów uczenia maszynowego, aby przewidzieć, co się stanie po wprowadzeniu nowego zestawu punktów danych do algorytmów.

Korzystając ze szczegółowych informacji jako punktu początkowego, uczenie maszynowe i stosują modele predykcyjne do danych, aby korzystać z wzorców w danych. Przez wiele iteracji szkolenia, testowania i wdrażania te modele i algorytmy mogą dokładnie przewidzieć przyszłe wyniki.

[Usługa Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) to natywne narzędzie w chmurze na platformie Azure do kompilowania i uczenia modeli na podstawie danych. To narzędzie obejmuje również [przepływ pracy przyspieszania opracowywania algorytmów uczenia maszynowego](https://docs.microsoft.com/azure/machine-learning/service/concept-azure-machine-learning-architecture). Tego przepływu pracy można użyć do opracowania algorytmów przy użyciu interfejsu wizualizacji lub języka Python.

Aby uzyskać bardziej niezawodne modele uczenia maszynowego, [usługi ml w usłudze Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview) zapewniają platformę uczenia maszynowego utworzoną na Apache Hadoop klastrów. Takie podejście umożliwia bardziej szczegółową kontrolę nad źródłowymi klastrami, magazynem i węzłami obliczeniowymi. Korzystanie z usługi Azure HDInsight zapewnia również bardziej zaawansowaną integrację za pomocą narzędzi, takich jak skalowanie i platforma Spark, w celu tworzenia prognoz opartych na zintegrowanych i pozyskiwanych danych, nawet w pracy z danymi ze strumienia. [Rozwiązanie do prognozowania opóźnień lotów](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-scaler-sparkr) pokazuje każdą z tych zaawansowanych funkcji do przewidywania opóźnień lotów w zależności od warunków pogodowych. Rozwiązanie HDInsight umożliwia również kontrolę nad przedsiębiorstwami, takimi jak bezpieczeństwo danych, dostęp do sieci i monitorowanie wydajności.

## <a name="predictions"></a>Prognozy

Po skompilowaniu i przeszkoleniu wzorca można go stosować przy użyciu interfejsów API, które mogą robić przewidywania podczas dostarczania środowiska cyfrowego. Większość z tych interfejsów API jest zbudowana z dobrze przeszkolonych modeli opartych na wzorcu danych. Jednak w miarę jak większa liczba klientów wdraża typowe obciążenia w chmurze, dostawcy chmury mogą zapewnić wspólne interfejsy API przewidywania, aby umożliwić szybsze wdrażanie prognoz.

[Cognitive Services platformy Azure](https://docs.microsoft.com/azure/cognitive-services) to przykład przewidywalnej kompilacji interfejsu API przez dostawcę chmury. Ta usługa zawiera predykcyjne interfejsy API do moderowania zawartości, wykrywania anomalii lub sugestie dotyczące personalizowania zawartości. Te interfejsy API są gotowe do użycia na podstawie wspólnych wzorców zawartości, które firma Microsoft wykorzystuje do uczenia modeli. Każdy z tych interfejsów API czyni prognozowanie na podstawie danych, które są podawane do interfejsu API.

[Usługa Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning) umożliwia wdrożenie niestandardowych algorytmów, które można tworzyć i uczeni wyłącznie na podstawie własnych danych. Dowiedz się więcej o wdrażaniu prognoz przy użyciu [Azure Machine Learning.](https://docs.microsoft.com/azure/machine-learning/service/how-to-deploy-and-where)

Artykuł dotyczący [konfigurowania klastrów usługi HDInsight](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-provision-linux-clusters) omawia procesy umożliwiające Uwidacznianie prognoz opracowanych dla usług ml w usłudze Azure HDInsight.

## <a name="interactions"></a>Interakcje

Po udostępnieniu prognoz za pomocą interfejsu API przewidywanie może być używane w wpływie na zachowania klientów. Ma to wpływ na formę interakcji. Interakcja z algorytmem uczenia maszynowego odbywa się w innych środowiskach cyfrowych lub otoczenia. Dane są zbierane za pośrednictwem aplikacji lub środowiska, ale dane są uruchamiane za pośrednictwem algorytmów uczenia maszynowego. Gdy algorytm przewiduje wynik, to prognozowanie może być współużytkowane z klientem za pomocą istniejącego środowiska.

Dowiedz się więcej o interakcjach w [rozwiązaniu o regulowanej rzeczywistości](./devices.md#adjusted-reality), aby uzyskać więcej szczegółowych informacji na temat tworzenia interakcji w środowisku otoczenia.

## <a name="next-steps"></a>Następne kroki

W oparciu o wiedzę uzyskaną w zakresie [innowacyjności](./invention.md) w ramach [metodologii](./index.md) innowacji, o której wiadomo, że masz narzędzia techniczne wymagane do [kompilowania z empatię](./build.md).

> [!div class="nextstepaction"]
> [Kompiluj z empatię](./build.md)
