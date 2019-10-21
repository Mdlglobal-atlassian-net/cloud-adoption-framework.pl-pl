---
title: 'Innowacje w chmurze: przyjęcie akceptacji'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — wdrażanie
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 727686b70c7fb604274f74da7a043f589f79fa4c
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557221"
---
# <a name="empower-adoption"></a>Przyjęcie akceptacji

Ostatecznym testem innowacji jest reagowanie klientów na Twoje wynalazki. Czy hipoteza zakończyła się prawdziwie? Czy klienci korzystają z rozwiązania? Czy skalowanie jest zgodne z potrzebami żądanej wartości procentowej użytkowników? Co najważniejsze, kontynuują wycofywanie? Żadne z tych pytań nie może być zadawane, dopóki rozwiązanie MVP nie zostanie wdrożone. W tym artykule skupmy się na dyscyplinie podejmowania akceptacji.

## <a name="reducing-friction-to-adoption"></a>Zmniejszanie tarcia do przyjęcia

Istnieje kilka najważniejszych punktów tarcia do wdrożenia, które można zminimalizować za pomocą kombinacji technologii i procesów. W przypadku czytników, którzy znają procesy ciągłej integracji/ciągłego wdrażania lub DevOpsi, następujące kwestie będą wyglądać bardzo podobnie. Celem tego artykułu jest ustanowienie punktu wyjścia dla zespołów wdrażania w chmurze, które będą omawiać innowacje opałowe i zwrotne pętle. Dłuższy termin, ten punkt początkowy może wzrosnąć do bardziej niezawodnej ciągłej integracji/ciągłego wdrażania lub DevOps podejścia, jak produkty i zespoły.

Opisany w temacie [mierzenie wpływu klientów](./measure.md), pozytywna weryfikacja każdej hipotezy wymaga iteracji i określenia. W trakcie jakiegokolwiek cyklu innowacji będziesz mieć więcej błędów niż usługa WINS. Jest to oczekiwane. Jednakże, gdy klient potrzebuje, hipotezy i rozwiązania wyrównania w skali, światowy zmiany zmieniają się szybko. Ten artykuł ma na celu minimalizowanie wzrostu [technicznego](./build.md#reduce-complexity-and-delay-technical-spikes) , co może spowolnić innowacje, ale upewnić się, że zostały wdrożone kilka pełnych najlepszych rozwiązań. Dzięki temu projekt zespołowy będzie pomocny w przyszłości, ale dostarczenie na bieżących potrzeby klientów.

## <a name="empowering-adoption---maturity-model"></a>Dodanie modelu przyjęcia-data_spłaty

Głównym celem [metodologii innowacji](./index.md) jest skompilowanie partnerstwa klienta i przyspieszenie pętli opinii, co prowadzi do innowacji rynkowych.
Poniższy obraz i części zawartości opisują wstępne implementacje, które będą obsługiwały metodologię.

![Model przyjęcia-data_spłaty](../../_images/innovate/empower-adoption-maturity.png)

- [Udostępnione rozwiązanie](#shared-solution): Ustanów centralne repozytorium dla wszystkich aspektów rozwiązania.
- [Pętle opinii](#feedback-loops): Upewnij się, że pętle opinii mogą być zarządzane spójnie przez iteracje.
- [Ciągła integracja](#continuous-integration): regularnie Kompiluj i Konsoliduj rozwiązanie.
- [Niezawodne testowanie](#reliable-testing): Weryfikuj jakość rozwiązania i oczekiwane zmiany na dysku zapewniają środki.
- [Wdrażanie rozwiązania](#solution-deployment): wdrożenie rozwiązania umożliwiającego zespołowi szybkie udostępnianie zmian klientom.
- [Zintegrowane pomiary](#integrated-measurements): Dodaj metryki uczenia do pętli opinii, aby wyczyścić analizę przez cały zespół.

W przypadku zminimalizowania technicznego należy zastanowić się, że data_spłaty będą początkowo niskie dla każdej z tych zasad. Ale Planuj z wyprzedzeniem, dopasowując się do narzędzi i procesów, które mogą być skalowane w miarę jak niejednoznaczności. Na platformie Azure kombinację usług [GitHub](https://guides.github.com) i [Azure DevOps](https://docs.microsoft.com/azure/devops) umożliwiają małym zespołom szybkie rozpoczęcie pracy. Następnie zwiększ się do tysięcy deweloperów, którzy współpracują z rozwiązaniami skalowania, które testują setki z nich. W pozostałej części tego artykułu przedstawiono plan Big, a w tym celu należy rozpocząć małe podejście w celu przyjęcia wdrożenia w ramach każdej z tych zasad.

## <a name="shared-solution"></a>Udostępnione rozwiązanie

Opisany w temacie [mierzenie wpływu klientów](./measure.md), pozytywna weryfikacja każdej hipotezy wymaga iteracji i określenia. W trakcie jakiegokolwiek cyklu innowacji będziesz mieć więcej błędów niż usługa WINS. Jest to oczekiwane. Jednakże, gdy klient potrzebuje, hipotezy i rozwiązania wyrównania w skali, światowy zmiany zmieniają się szybko.

W przypadku skalowania innowacji nie ma więcej cennych narzędzi niż udostępniona baza kodu dla rozwiązania. Niestety, nie ma sposobu przewidywania iteracji lub tego, który SPECJALISTy będzie miał wygraną kombinację. Dlatego nigdy nie jest zbyt wczesny do ustanowienia udostępnionej bazy kodu lub repozytorium. Jest to jedno podejście [techniczne](./build.md#reduce-complexity-and-delay-technical-spikes) , które nigdy nie powinno być opóźnione. Gdy zespół iteruje w różnych rozwiązaniach MVP, udostępnione repozytorium pozwoli na łatwe współdziałanie i przyspieszenie opracowywania. Gdy zmiany w rozwiązaniu spowodują negatywny wpływ na metryki uczenia, Kontrola wersji może pozwolić na wycofanie do poprzedniej, bardziej wydajnej wersji rozwiązania.

Najbardziej typowym narzędziem do zarządzania repozytoriami kodu jest [GitHub](https://guides.github.com) , która umożliwia tworzenie repozytorium udostępnionego kodu za pomocą kilku kliknięć. Ponadto funkcja [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) platformy Azure DevOps może służyć do tworzenia repozytorium [git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) lub [Team Foundation](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="feedback-loops"></a>Pętle opinii

Klucz służący do tworzenia partnerstwa dla klientów w ramach cyklu innowacji polega na tym, że klient jest częścią rozwiązania. Jest to realizowane na podstawie długości ramion przez [zmierzenie wpływu klientów](./measure.md). Ściślej, wymaga to rozmowy i bezpośredniego testowania z klientem. Oba wyniki muszą być zarządzane.

Każdy punkt opinii to potencjalne rozwiązanie wymagane przez klienta. Co ważniejsze, każdy bit opinii bezpośrednio od klienta jest okazją do usprawnienia partnerstwa. Jeśli opinia przekieruje ją do rozwiązania MVP, świętuje go z klientem. Nawet jeśli opinia nie jest poddana akcji, po prostu jest przejrzysta w celu określenia priorytetu opinii, zademonstrowanie [sposób myślenia wzrostu](./learn.md#growth-mindset) i skoncentrowanie się na [ciągłym uczeniu](./learn.md#continuous-learning).

[Usługa Azure DevOps](https://docs.microsoft.com/azure/devops) obejmuje sposoby [żądania, dostarczania i zarządzania opiniami](https://docs.microsoft.com/azure/devops/project/feedback). Każdy z tych narzędzi służy do scentralizowania opinii, dzięki czemu zespół może podjąć działania i zgłosić opinię, zapewniając przejrzystą pętlę opinii.

## <a name="continuous-integration"></a>Integracja ciągła

W miarę jak wydłużać skala i hipotezy są coraz bardziej zbliżone do prawdziwych innowacji na dużą skalę, liczba mniejszych hipotez, które mają być testowane, szybko rośnie. Aby uzyskać dokładne pętle opinii i płynne procesy przyjmowania, ważne jest, aby każda z tych hipotez była zintegrowana i obsługiwała hipotezę podstawową, która zauważa za innowacje. Niestety, trzeba również szybko przechodzić do innowacji i wzrosnąć, co będzie wymagało od wielu deweloperów testowania wariantów hipotez podstawowych. W celu późniejszego przygotowania do rozwoju może zaistnieć potrzeba wielu zespołów deweloperów, którzy tworzą w ramach rozwiązania udostępnionego. Ciągła integracja to pierwszy krok w kierunku zarządzania różnymi ruchomymi częściami.

W przypadku ciągłej integracji zmiany kodu są często scalane z gałęzią główną. Zautomatyzowane procesy kompilowania i testowania zapewniają, że kod w głównej gałęzi jest zawsze w jakości produkcyjnej. Gwarantuje to, że deweloperzy pracują ze sobą, aby opracowywać udostępnione rozwiązania zapewniające dokładne i niezawodne pętle opinii.

Usługa Azure DevOps i [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) udostępniają możliwości ciągłej integracji za pomocą kilku kliknięć, usług GitHub lub różnych repozytoriów.
Dowiedz się więcej o [ciągłej integracji](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-integration) lub uruchamiaj w [laboratorium](https://www.azuredevopslabs.com/labs/azuredevops/continuousintegration) praktycznym, aby uzyskać więcej informacji. Istnieją również architektury rozwiązań umożliwiających przyspieszenie tworzenia potoków ciągłej integracji/ciągłego wdrażania [przy użyciu usługi Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="reliable-testing"></a>Niezawodne testowanie

Wady w dowolnym rozwiązaniu mogą tworzyć fałszywie dodatnie lub fałszywe wartości ujemne. Nieoczekiwane błędy mogą łatwo prowadzić do błędnej interpretacji metryk wdrażania użytkownika. Może również prowadzić do negatywnej opinii od klientów, którzy nie reprezentują prawidłowo testu hipotezy.

Podczas wczesnych iteracji rozwiązania MVP są oczekiwane wady, wczesne osoby zatwierdzające mogą nawet je znaleźć endearing. W wczesnych wersjach testowanie akceptacji prawdopodobnie będzie nieistniejące. Jednak jednym aspektem kompilowania za pomocą empatię jest Weryfikacja potrzeb i hipotez. Oba te elementy można wykonać za pomocą testów jednostkowych na poziomie kodu i testów akceptacji ręcznej przed wdrożeniem. Razem te będą zapewniały pewne metody niezawodności podczas testowania. Dłuższe, dobrze zdefiniowane serie testów kompilowania, jednostkowych i akceptacji, powinny być zautomatyzowane, aby zapewnić niezawodne metryki związane z dokładniejszymi ulepszeniami ziarna hipotez i rozwiązaniami.

[Azure test Plans](https://docs.microsoft.com/azure/devops/test/track-test-status?view=azure-devops) udostępnia narzędzia do tworzenia i obsługi planów testów podczas ręcznego lub automatycznego wykonywania testów.

## <a name="solution-deployment"></a>Wdrażanie rozwiązania

Prawdopodobnie najbardziej znaczącym aspektem podejmowania akceptacji jest możliwość kontrolowania wydania rozwiązania dla klientów. Dostarczenie samoobsługowego lub zautomatyzowanego potoku w celu zwolnienia rozwiązania dla klientów przyspiesza pętlę opinii. Umożliwienie klientom szybkiego działania ze zmianami w rozwiązaniu, zaprasza klienta do procesu. Umożliwia również szybsze testowanie hipotez, skracając założenia i potencjalną replikę.

Oto kilka metod wdrażania rozwiązań, poniżej przedstawiono trzy najczęstsze podejścia:

- Najbardziej zaawansowane podejście, **ciągłe wdrażanie**, automatycznie wdraża zmiany kodu w środowisku produkcyjnym. W przypadku dojrzałych zespołów testowanie hipotez, ciągłe wdrażanie może być niezwykle cenne.
- W wczesnych etapach tworzenia **ciągłe dostarczanie** może być bardziej odpowiednie. W przypadku ciągłego dostarczania wszystkie zmiany kodu są automatycznie wdrażane w środowisku podobnym do produkcji. Deweloperzy, osoby podejmujące decyzje biznesowe i inni w zespole mogą korzystać z tego środowiska w celu sprawdzenia, czy ich praca jest gotowa do produkcji. Może również służyć do testowania hipotezy dla klientów bez wpływu na trwającą działalność biznesową.
- **Wdrożenie ręczne** to najmniej zaawansowane podejście do zarządzania wydaniami. Jak sugeruje nazwa, ktoś w zespole ręcznie wdroży najnowsze zmiany kodu. Takie podejście jest podatne na błędy, niezawodne i uznawane za antywzorców przez najbardziej sezonowe inżynierów.

Podczas pierwszej iteracji rozwiązania MVP wdrożenie ręczne jest powszechnym podejściem, w odróżnieniu od powyższego opisu. Gdy rozwiązanie jest niezwykle płynne i opinia klientów jest nieznana, istnieje znaczne ryzyko resetowania całego rozwiązania (lub nawet hipotezy podstawowej). Ogólna reguła wdrażania ręcznego: brak potwierdzenia klienta, Automatyzacja wdrażania. Inwestycja wczesna może prowadzić do utraty czasu. Co więcej, można utworzyć zależności od potoku wydania, które sprawiają, że zespół będzie bardziej odporny na wczesne przestawianie. Po kilku pierwszych iteracjach lub w odpowiedzi na Opinie klientów sugeruje potencjalne sukcesy, bardziej zaawansowany model wdrożenia powinien być szybko przyjęty.

Na dowolnym etapie weryfikacji hipotez, usługa Azure DevOps i [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines) udostępniają funkcje ciągłego dostarczania i ciągłego wdrażania za pomocą zaledwie kilku kliknięć. Aby uzyskać więcej informacji, Dowiedz się więcej na temat [ciągłego dostarczania](https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery) lub przebiegu w [laboratorium](https://www.azuredevopslabs.com/labs/azuredevops/continuousdeployment) praktycznym. Architektury rozwiązań mogą również przyspieszyć tworzenie potoków ciągłej integracji/ciągłego wdrażania [przy użyciu usługi Azure DevOps](https://azure.microsoft.com/solutions/devops).

## <a name="integrated-measurements"></a>Pomiary zintegrowane

Podczas [mierzenia wpływu na klientów](./measure.md)należy zrozumieć, w jaki sposób klienci reagują na zmiany w rozwiązaniu. Te dane, nazywane telemetrią, zawierają informacje o akcjach, które zostały wykonane przez użycie (lub kohorta użytkowników) podczas korzystania z rozwiązania. Na podstawie tych danych można łatwo uzyskać weryfikację ilościową hipotez. Te metryki mogą być następnie używane do dostosowywania rozwiązania i generowania bardziej szczegółowych zapisów. Te delikatne zmiany ułatwiają przedwczesne roztwory w kolejnych iteracjach, co ostatecznie prowadzi do powtórnego wdrażania na dużą skalę.

Na platformie Azure [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) udostępnia narzędzia i interfejs, które umożliwiają zbieranie i przeglądanie danych ze środowiska klienta. Te spostrzeżenia i szczegółowe informacje mogą służyć do uściślenia zaległości przy użyciu [Azure Boards](https://docs.microsoft.com/azure/devops/boards).

## <a name="next-steps"></a>Następne kroki

Zrozumienie narzędzi i procesów, które są niezbędne do uzyskania akceptacji, umożliwia przeanalizowanie bardziej zaawansowanej dyscypliny innowacji, [współdziałanie z urządzeniami](./devices.md). Co może pomóc w zmniejszeniu barier między fizycznymi i cyfrowymi środowiskami, dzięki czemu rozwiązanie jest jeszcze łatwiejsze.

> [!div class="nextstepaction"]
> [Korzystanie z urządzeń](./devices.md)
