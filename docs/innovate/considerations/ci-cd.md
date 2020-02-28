---
title: Przyjmowanie rozwiązań dzięki rozdaniom cyfrowym
description: Użyj modelu dojrzałości metodologii innowacje, aby zmniejszyć liczbę problemów, które spowalniają wdrażanie, zachowując przy tym najlepsze rozwiązania.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: bfaacd1f07b24a3d88b03aa577e1f1ca38493423
ms.sourcegitcommit: 10637acba8c857a6f5aa8c4a80c0649903f60402
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/28/2020
ms.locfileid: "78170566"
---
# <a name="empower-adoption"></a>Zwiększanie akceptacji

Ostatecznym testem innowacji jest reagowanie klientów na Twoje wynalazki. Czy hipoteza zakończyła się prawdziwie? Czy klienci korzystają z rozwiązania? Czy skalowanie jest zgodne z potrzebami żądanej wartości procentowej użytkowników? Co najważniejsze, kontynuują wycofywanie? Żadne z tych pytań nie może zostać poproszonych, dopóki nie zostanie wdrożony minimalny, żywotny rozwiązanie produktu (MVP). W tym artykule skupmy się na dyscyplinie podejmowania akceptacji.

## <a name="reduce-friction-that-affects-adoption"></a>Zmniejsz liczbę problemów, które mają wpływ na wdrażanie

Istnieje kilka najważniejszych punktów tarcia do wdrożenia, które można zminimalizować za pomocą kombinacji technologii i procesów. W przypadku czytelników mających wiedzę o ciągłej integracji (CI) i procesach ciągłego wdrażania (CD) lub DevOps są znane następujące informacje: Ten artykuł ustanawia punkt wyjścia dla zespołów do wdrażania w chmurze, które reagują na innowacyjność i pętle. W przyszłości ten punkt początkowy może wzmocnić bardziej niezawodną ciągłość/CD lub DevOps podejścia jako produkty i zespoły.

Zgodnie z opisem w temacie [mierzenie wpływu klientów](./measure.md), pozytywna weryfikacja każdej hipotezy wymaga iteracji i określenia. Wystąpił znacznie więcej błędów niż w przypadku usługi WINS w dowolnym cyklu innowacji. Jest to oczekiwane. Jeśli jednak klient potrzebuje, hipotezy i rozwiązania wyrównania w odpowiedniej skali, świat zmieni się szybko. Ten artykuł ma na celu minimalizowanie wzejść [technicznych](./build.md#reduce-complexity-and-delay-technical-spikes) , które spowalniają innowacje, ale nadal dbają o zachowanie kilku stałych najlepszych rozwiązań. Dzięki temu projekt zespołowy będzie pomocny w przyszłości, a na potrzeby dostarczania bieżących klientów.

## <a name="empowering-adoption-the-maturity-model"></a>Zatwierdzanie przyjęcia: model zapadalności

Głównym celem [metodologii innowacji](./index.md) jest skompilowanie partnerstwa klienta i przyspieszenie pętli opinii, co prowadzi do innowacji rynkowych. Poniższy obraz i sekcje zawierają opis wstępnych implementacji, które obsługują tę metodologię.

![Przyjęcie przyjęcia: model zapadalności](../../_images/innovate/empower-adoption-maturity.png)

- [Udostępnione rozwiązanie](#shared-solution): Ustanów centralne repozytorium dla wszystkich aspektów rozwiązania.
- [Pętle opinii](#feedback-loops): Upewnij się, że pętle opinii mogą być zarządzane spójnie przez iteracje.
- [Ciągła integracja](#continuous-integration): regularnie Kompiluj i Konsoliduj rozwiązanie.
- [Niezawodne testowanie](#reliable-testing): sprawdzanie jakości rozwiązań i oczekiwane zmiany w celu zapewnienia niezawodności metryk testowania.
- [Wdrażanie rozwiązań](#solution-deployment): Wdrażaj rozwiązania, aby zespół mógł szybko udostępniać zmiany klientom.
- [Zintegrowane pomiary](#integrated-measurements): Dodaj metryki uczenia do pętli opinii, aby wyczyścić analizę przez cały zespół.

Aby zminimalizować liczbę techniczną, założono, że data_spłaty będą początkowo niskie dla każdej z tych zasad. Ale bez ograniczeń planuje się, dopasowując do narzędzi i procesów, które mogą być skalowane w miarę jak długo są bardziej szczegółowe. Na platformie Azure usługa [GitHub](https://guides.github.com) i [usługa Azure DevOps](https://docs.microsoft.com/azure/devops) umożliwiają małym zespołom rozpoczęcie pracy z niewielkim tarciem. Zespoły te mogą wzrosnąć, aby obejmowały tysiące deweloperów, którzy współpracują nad rozwiązaniami skalowania i testują setki postanowień klientów. W pozostałej części tego artykułu przedstawiono krótkie i rozłożone małe podejście do podejmowania wdrożenia w ramach każdej z tych zasad.

## <a name="shared-solution"></a>Rozwiązanie udostępnione

Zgodnie z opisem w temacie [mierzenie wpływu klientów](./measure.md), pozytywna weryfikacja każdej hipotezy wymaga iteracji i określenia. Wystąpił znacznie więcej błędów niż w przypadku usługi WINS w dowolnym cyklu innowacji. Jest to oczekiwane. Jeśli jednak klient potrzebuje, hipotezy i rozwiązania wyrównania w odpowiedniej skali, świat zmieni się szybko.

W przypadku skalowania innowacji nie ma więcej cennych narzędzi niż udostępniona baza kodu dla rozwiązania. Niestety, nie istnieje niezawodny sposób przewidywania iteracji lub tego, który SPECJALISTy będzie miał wygraną kombinację. Dlatego nigdy nie jest zbyt wczesny do ustanowienia udostępnionej bazy kodu lub repozytorium. Jest to jedno podejście [techniczne](./build.md#reduce-complexity-and-delay-technical-spikes) , które nigdy nie powinno być opóźnione. Gdy zespół iteruje przez różne rozwiązania MVP, udostępnione repozytorium umożliwia łatwą współpracę i przyspieszenie opracowywania. Gdy zmiany w rozwiązaniu przeciągnieją metryki szkoleniowe w dół, Kontrola wersji umożliwia wycofanie do wcześniejszej, bardziej efektywnej wersji rozwiązania.

Najczęściej przyjętym narzędziem do zarządzania repozytoriami kodu jest [GitHub](https://guides.github.com), który umożliwia tworzenie repozytorium kodu udostępnionego za pomocą zaledwie kilku kliknięć. Ponadto funkcja [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) platformy Azure DevOps może służyć do tworzenia repozytorium [git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) lub [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="feedback-loops"></a>Cykle wymiany opinii

Udostępnienie klientowi części rozwiązania jest kluczem do tworzenia partnerstwa dla klientów w fazie innowacji. Jest to realizowane w części przez [zmierzenie wpływu klientów na klienta](./measure.md). Wymaga rozmowy i bezpośredniego testowania z klientem. Obie funkcje generują opinię, która musi być efektywnie zarządzana.

Każdy punkt opinii to potencjalne rozwiązanie wymagane przez klienta. Co więcej, każdy bit bezpośredniej opinii klientów reprezentuje okazję do usprawnienia partnerstwa. Jeśli opinia przekieruje je do rozwiązania MVP, poświęci to klientowi. Nawet jeśli niektóre opinie nie są funkcjonalne, po prostu są one przejrzyste i decyduje o tym, że jest to niezauważalne, aby zmniejszyć [sposób myślenia wzrostu](./learn.md#growth-mindset) i skupić się na [ciągłym uczeniu](./learn.md#continuous-learning).

[Usługa Azure DevOps](https://docs.microsoft.com/azure/devops) obejmuje sposoby [żądania, dostarczania i zarządzania opiniami](https://docs.microsoft.com/azure/devops/project/feedback). Każdy z tych narzędzi służy do scentralizowania informacji zwrotnych, dzięki czemu zespół może podjąć odpowiednie działania i zapewnić dalsze działanie w ramach usługi w postaci przezroczystej pętli opinii.

## <a name="continuous-integration"></a>Ciągła integracja

W miarę jak wydłużać skala i hipotezy są coraz bliżej prawdziwe innowacje na dużą skalę, liczba mniejszych hipotez, które mają zostać przetestowane, będzie szybko rosnąć. Aby uzyskać dokładne pętle opinii i płynne procesy przyjmowania, ważne jest, aby każda z tych hipotez była zintegrowana i obsługiwała hipotezę podstawową, która zauważa za innowacje. Oznacza to, że konieczne jest również szybkie przechodzenie do innowacji i rozwoju, co wymaga wielu deweloperów do testowania różnic hipotezy podstawowej. W celu późniejszego przygotowania do rozwoju można nawet potrzebować wielu zespołów deweloperów, z których każdy kompiluje się w ramach udostępnionego rozwiązania. Ciągła integracja to pierwszy krok w kierunku zarządzania wszystkimi ruchomymi częściami.

W przypadku ciągłej integracji zmiany kodu są często scalane z gałęzią główną. Zautomatyzowane procesy kompilowania i testowania sprawdzają, czy kod w głównej gałęzi jest zawsze jakości produkcji. Gwarantuje to, że deweloperzy pracują ze sobą, aby opracowywać udostępnione rozwiązania zapewniające dokładne i niezawodne pętle opinii.

Usługa Azure DevOps i [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) zapewniają możliwości ciągłej integracji za pomocą zaledwie kilku kliknięć w serwisie GitHub lub w różnych repozytoriach.
Dowiedz się więcej o [ciągłej integracji](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration)lub aby uzyskać więcej informacji, zobacz [laboratorium praktyczne](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration). Istnieją również architektury rozwiązań umożliwiających przyspieszenie tworzenia potoków ciągłej integracji/ciągłego wdrażania [za pomocą usługi Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="reliable-testing"></a>Niezawodne testowanie

Wady w dowolnym rozwiązaniu mogą tworzyć fałszywie dodatnie lub fałszywe wartości ujemne. Nieoczekiwane błędy mogą łatwo prowadzić do błędnej interpretacji metryk wdrażania użytkownika. Mogą również generować negatywną opinię od klientów, którzy nie reprezentują dokładnie testu hipotezy.

Podczas wczesnych iteracji rozwiązania MVP oczekiwane są wady; Wczesne osoby zatwierdzające mogą nawet je znaleźć endearing. W wczesnych wersjach testowanie akceptacji jest zwykle nieistniejące. Jednak jeden aspekt kompilowania z empatię dotyczy weryfikacji potrzeb i hipotez. Oba te elementy można wykonać za pomocą testów jednostkowych na poziomie kodu i testów akceptacji ręcznej przed wdrożeniem. Wspólnie zapewniają one pewne metody niezawodności w testowaniu. Należy dążyć do automatyzacji dobrze zdefiniowanej serii testów kompilacji, jednostkowych i akceptacji. Zapewni to niezawodne metryki związane z bardziej szczegółowymi ulepszeniami hipotez i rozwiązaniami uzyskanymi.

Funkcja [Azure test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) udostępnia narzędzia do tworzenia i obsługi planów testów podczas ręcznego lub automatycznego wykonywania testów.

## <a name="solution-deployment"></a>Wdrażanie rozwiązania

Być może najbardziej znaczący aspekt podejmowania akceptacji dotyczy zdolności do kontrolowania wydania rozwiązania klientom. Zapewniając samoobsługowy lub zautomatyzowany potok w celu zwolnienia rozwiązania dla klientów, można przyspieszyć pętlę opinii. Dzięki umożliwieniu klientom szybkiej współpracy ze zmianami w rozwiązaniu należy zaprosić je do procesu. Takie podejście wyzwala również szybsze testowanie hipotez, co zmniejsza założenia i potencjalną reakcję.

Jest to kilka metod wdrażania rozwiązania. Poniżej przedstawiono trzy najczęstsze:

- **Ciągłe wdrażanie** to najbardziej zaawansowaną metodę, ponieważ automatycznie wdraża zmiany kodu w środowisku produkcyjnym. W przypadku dojrzałych zespołów, które testują hipotezy dojrzałe, ciągłe wdrażanie może być niezwykle cenne.
- W wczesnych etapach tworzenia **ciągłe dostarczanie** może być bardziej odpowiednie. W przypadku ciągłego dostarczania wszystkie zmiany kodu są automatycznie wdrażane w środowisku podobnym do produkcji. Deweloperzy, osoby podejmujące decyzje biznesowe i inni członkowie zespołu mogą korzystać z tego środowiska, aby sprawdzić, czy ich praca jest gotowa do produkcji. Za pomocą tej metody można także testować hipotezę z klientami bez wpływu na trwającą działalność biznesową.
- **Wdrożenie ręczne** to najmniej zaawansowane podejście do zarządzania wydaniami. Jak sugeruje nazwa, ktoś w zespole ręcznie wdraża najnowsze zmiany kodu. Takie podejście jest podatne na błędy, niezawodne i uznawane za antywzorców przez najbardziej sezonowe inżynierów.

Podczas pierwszej iteracji rozwiązania MVP wdrożenie ręczne jest wspólne, pomimo wcześniejszej oceny. Gdy rozwiązanie jest niezwykle płynne i opinia klientów jest nieznana, istnieje duże ryzyko związane z resetowaniem całego rozwiązania (lub nawet hipotezą podstawową). Oto ogólna zasada wdrażania ręcznego: brak potwierdzenia klienta, Automatyzacja wdrażania.

Inwestycja wczesna może prowadzić do utraty czasu. Co więcej, można utworzyć zależności od potoku wydania, które sprawiają, że zespół będzie bardziej odporny na wczesne przestawianie. Po kilku pierwszych iteracjach lub w odpowiedzi na Opinie klientów sugeruje potencjalne sukcesy, bardziej zaawansowany model wdrożenia powinien być szybko przyjęty.

Na dowolnym etapie weryfikacji hipotez, usługa Azure DevOps i [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) zapewniają ciągłe dostarczanie i ciągłe wdrażanie. Dowiedz się więcej na temat [ciągłego dostarczania](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery)lub zapoznaj się z [ćwiczeniami](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment)praktycznymi. Architektura rozwiązania może również przyspieszyć tworzenie potoków ciągłej integracji/ciągłego wdrażania [za pomocą usługi Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Pomiary zintegrowane

Gdy [mierzy się wpływ na klientów](./measure.md), ważne jest, aby zrozumieć, w jaki sposób klienci reagują na zmiany w rozwiązaniu. Te dane, znane jako *Telemetria*, zapewniają wgląd w akcje podejmowane przez użytkownika (lub kohorta użytkowników) podczas pracy z rozwiązaniem. Na podstawie tych danych można łatwo uzyskać weryfikację ilościową hipotez. Te metryki mogą być następnie używane do dostosowywania rozwiązania i generowania bardziej szczegółowych zapisów. Te delikatne zmiany ułatwiają przedwczesne roztwory w kolejnych iteracjach, co ostatecznie prowadzi do powtórnego wdrażania na dużą skalę.

Na platformie Azure [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) udostępnia narzędzia i interfejs do zbierania i przeglądania danych ze środowiska klienta. Możesz zastosować te obserwacje i szczegółowe informacje, aby uściślić zaległości przy użyciu [Azure Boards](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Następne kroki

Po uzyskaniu informacji o narzędziach i procesach niezbędnych do wprowadzenia akceptacji, należy zapoznać się z bardziej zaawansowaną dyscypliną innowacji: [współdziałanie z urządzeniami](./devices.md). Ta dyscyplina może pomóc w zmniejszeniu barier między fizycznymi i cyfrowymi środowiskami, dzięki czemu rozwiązanie jest jeszcze łatwiejsze.

> [!div class="nextstepaction"]
> [Korzystanie z urządzeń](./devices.md)
