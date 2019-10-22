---
title: Kompiluj konsensus na wartość biznesową innowacji w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak budować konsensus na wartość biznesową innowacji w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 643da95396a4983c2642fabcf21340264d0cd1c9
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683342"
---
# <a name="building-consensus-on-the-business-value-of-innovation"></a>Kompilowanie konsensusu na wartość biznesową innowacji

Pierwszym krokiem do opracowania nowych innowacji jest zidentyfikowanie, w jaki sposób innowacje będą mieć wpływ na wartość biznesową. W tym ćwiczeniu zawarto monit z prośbą o określenie znaczenia inwestycji więcej czasu.

## <a name="qualifying-questions"></a>Pytania kwalifikujące

Przed rozpoczęciem opracowywania jakichkolwiek rozwiązań (w chmurze lub lokalnie) Sprawdź poprawność kryteriów wartości biznesowej:

1. Jakie są wymagane przez klientów wyszukiwanie w tym rozwiązaniu?
2. Jakie możliwości może utworzyć rozwiązanie dla firmy?
3. Jakie wyniki biznesowe można osiągnąć przy użyciu tego rozwiązania?
4. Które motywacje firmy byłyby obsługiwane w tym rozwiązaniu?

Jeśli odpowiedzi na wszystkie cztery pytania są dobrze udokumentowane, pozostała część tego ćwiczenia może nie być potrzebna. Na szczęście Ta dokumentacja może być łatwo przetestowana. W celu przetestowania zarówno dokumentacji, jak i ogólnego wyrównania, hostować krótkie spotkanie z zatwierdzonymi zainteresowanymi podmiotami biznesowymi oraz oddzielne krótkie spotkanie z zaangażowanym zespołem programistycznym. W przypadku obu spotkań należy zadać cztery powyższe pytania i porównać wyniki.

> [!NOTE]
> Istniejąca dokumentacja **nie powinna** być udostępniana członkom zespołu przed spotkaniem. W przypadku istnienia rzeczywistego wyrównania identyfikatory GUID powinny być odwołujące się (lub jeszcze lepsze) przez członków każdej grupy.

> [!WARNING]
> Nie Ułatwiaj spotkania. Jest to test wyrównania, a nie ćwiczenie tworzenia wyrównania. Podczas uruchamiania spotkania upewnij się, że uczestnicy są świadomi celu przetestowania kierunkowego dostosowania z istniejącymi umowami w zespole. Ustanów tylko limit czasu. Zatwierdź do pięciu minut na pytanie i ustaw czasomierz dla każdego z nich. Zamknij to pytanie w ciągu pięciu minut, nawet jeśli odpowiedź nie zostanie uzgodniona.

Jeśli odpowiedzi są wyrównane kierunekowo, ale reprezentują różne języki i zainteresowania każdej grupy, należy wziąć pod uwagę Victory. Wszystko jest gotowe do dalszego opracowywania rozwiązań.

Jeśli jedna lub dwie odpowiedzi są wyrównane kierunekowo, należy się rozejść. Są one już lepiej wyrównane niż w przypadku większości organizacji. Przyszłe sukcesy są bardzo prawdopodobnie z niewielkimi potrzebami w zakresie ciągłego inwestowania. Zapoznaj się z każdą z poniższych sekcji, aby zapoznać się z pomysłami, które mogą pomóc w tworzeniu dalszych wyrównania.

Jeśli zespół nie odpowie na wszystkie cztery pytania w ciągu 30 minut, wówczas wyrównanie i następujące działania mogą mieć duży wpływ na tę pracę i inne. Zwróć szczególną uwagę na każdą z następujących sekcji.

## <a name="address-the-big-picture-first"></a>Najpierw Zaadresuj duży obraz

Struktura wdrażania w chmurze jest zgodna z określoną ścieżką, korzystając z strategii, planowania, gotowości i przyjęcia. Innowacje w chmurze mieszczą się w fazie wdrażania tego procesu. Gdy odpowiedzi na pytania 3 i 4 powyżej (wyniki i motywacje) są nieprawidłowo wyrównane, oznacza to, że coś zostało pominięte w fazie strategii cyklu życia wdrożenia chmury. Kilka z następujących scenariuszy może być w trakcie odtwarzania.

- **Możliwość wyrównania:** Gdy zainteresowane strony biznesowe nie mogą wyrazić zgody na motywacje i wyniki biznesowe związane z wysiłkią innowacyjną w chmurze, jest to objaw większego wyzwania. Ćwiczenia w [fazie strategii chmury](../strategy/index.md) mogą być przydatne podczas opracowywania wyrównania między uczestnikami biznesowymi. Ponadto zdecydowanie zaleca się, aby ten sam uczestnik projektu mógł utworzyć [zespół strategii chmurowej](../organize/cloud-strategy.md) , który spełnia regularnie.

- **Szansa komunikacji:** Gdy zespół programistyczny nie jest w stanie wyrazić zgody na motywacje i wyniki biznesowe, może to być objawem strategicznych luk w komunikacji. Przegląd strategii chmury z zespołem wdrażania chmury można szybko rozwiązać ten blok. Po upływie kilku tygodni od przejrzenia zespół powinien powtórzyć zadanie kwalifikujące się do realizacji.

- **Szansa do priorytetyzacji:** Strategia chmury jest zasadniczo hipotezą na poziomie kierownictwa. Najlepsze strategie chmury są otwarte do iteracji i informacji zwrotnych. Jeśli obie zespoły rozumieją strategię, ale nadal nie mogą w sposób nieznacznie wyrównać odpowiedzi na te pytania, priorytety mogą być nieprawidłowo wyrównane. Sesja z zespołem wdrażania w chmurze i zespołem strategii chmury mogą pomóc w wysiłkach obu grup. W trakcie tej sesji zespół wdrażania w chmurze udostępnia swoje wyrównane odpowiedzi do pytań na wielkie zdjęcie. Z tego miejsca konwersacja zespołu ds. rozwiązań w chmurze i zespołu strategii chmury mogą wyróżnić możliwości w celu lepszego dopasowania priorytetów.

Te duże szanse na zdjęcia często ujawniają sposoby lepszego dostosowania tego rozwiązania z strategią chmury. To ćwiczenie ma dwa typowe wyniki:

- Te konwersacje mogą prowadzić do ulepszeń strategii chmury i lepszego przedstawienia tego ważnego potrzeb klienta. Taka zmiana może skutkować lepszym wsparciem dla zespołu.
- Z drugiej strony, ta konwersacja może wskazywać, że inwestycja w inne rozwiązanie jest bardziej odpowiednia dla zespołu wdrożenia chmury. W takim przypadku Rozważ Migrowanie tego rozwiązania przed kontynuowaniem inwestowania w innowacje. Alternatywnie, może to wskazywać, że podejście programisty do deweloperów jest niezbędne do przetestowania wartości biznesowej jako pierwszej. W obu przypadkach ułatwi to zespołowi uniknięcie tworzenia dużych inwestycji z ograniczonymi wynikami firmy.

## <a name="address-solution-alignment"></a>Wyrównanie rozwiązania adresu

Bardzo często odpowiedzi na pytania 1 i 2 (zapotrzebowanie klienta i szansa biznesowa) są niezgodne. Jest to szczególnie typowe w przypadku wczesnych etapów pomysłów i programowania. Znalezienie równowagi między zbyt dużą i zbyt małą definicją jest trudne dla wielu zespołów programistycznych. W strukturze wdrażania chmury, metodyki Lean, takie jak Build-Measure-Dowiedz się, są sugerowane jako najlepszy sposób odpowiedzi na te pytania. Na poniższej liście przedstawiono okazje i podejścia do tworzenia wyrównania.

- **Okazja do hipotezy:** Często różne osoby zainteresowane i zespoły programistyczne mogą korzystać z zbyt wielu oczekiwań dla rozwiązania. W takim przypadku jest to znak, że hipoteza jest zbyt niejasne. Postępując zgodnie ze wskazówkami dotyczącymi [tworzenia z empatię klienta](./considerations/build.md) , aby utworzyć wyraźniejszy hipotezę.
- **Możliwość kompilacji:** Gdy zespoły są nieprawidłowo wyrównane, ponieważ nie zgadzają się na sposób rozwiązania klienta, zazwyczaj wskazuje, że zespół jest [opóźniony przez przedwcześnie podejście techniczne](./considerations/build.md#reduce-complexity-and-delay-technical-spikes). Aby zapewnić, że zespół koncentruje się na kliencie, Zacznij od pierwszej iteracji i Kompiluj mały MVP, aby zająć się jego częścią. Aby uzyskać dodatkowe wskazówki ułatwiające zespołowi przechodzenie do przodu, zobacz [Tworzenie cyfr cyfrowych](./considerations/invention.md).
- **Szansa szkoleniowa:** Gdy zespół jest nieprawidłowo wyrównany, ponieważ potrzebują szczegółowych wymagań technicznych i szerokich wymagań funkcjonalnych, pokazuje możliwość szkolenia w metodologiach Agile. Gdy Kultura zespołu nie jest gotowa do procesów Agile, może być trudne do innowacji i zapewnienia tempa na rynku. Aby poznać zasoby szkoleniowe dotyczące DevOps i metod agile, zobacz:
  - [Rozwijanie praktyk DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)
  - [Tworzenie aplikacji za pomocą usługi Azure DevOps](https://docs.microsoft.com/learn/paths/build-applications-with-azure-devops)
  - [Wdrażanie aplikacji za pomocą usługi Azure DevOps](https://docs.microsoft.com/learn/paths/deploy-applications-with-azure-devops/)

Korzystanie z tej metodologii i narzędzi do zarządzania zaległościami w każdej sekcji wymienionej powyżej może pomóc w tworzeniu wyrównania rozwiązania.

## <a name="next-steps"></a>Następne kroki

Gdy propozycja wartości biznesowej zostanie prawidłowo wyrównana i przekazana, czas na rozpoczęcie tworzenia rozwiązania. Powróć do [ćwiczenia innowacje](./index.md) , aby uzyskać wskazówki dotyczące następnych kroków.

> [!div class="nextstepaction"]
> [Wróć do ćwiczenia innowacje w celu wykonania następnych kroków](./index.md)
