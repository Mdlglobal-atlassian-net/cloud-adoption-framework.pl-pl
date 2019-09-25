---
title: Ocena tolerancja ryzyka
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie ryzyka biznesowego związanego z przekształcaniem w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 2b8bc595377b2748bd00f306659a46196115e91d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223546"
---
# <a name="evaluate-risk-tolerance"></a>Ocena tolerancja ryzyka

Każda decyzja biznesowa tworzy nowe ryzyko. W ten sposób inwestycja w jakikolwiek sposób wiąże się z ryzykiem strat. Nowe produkty lub usługi tworzą ryzyka związane z awarią rynku. Zmiany w bieżących produktach lub usługach mogą zmniejszyć udział w rynku. Transformacja chmury nie zapewnia rozwiązania Magical do codziennego ryzyka biznesowego. W przeciwieństwie do siebie, połączone rozwiązania (w chmurze lub lokalnie) wprowadzają nowe zagrożenia. Wdrażanie zasobów w dowolnej funkcji połączonej z siecią również rozszerza potencjalne profile zagrożeń przez ujawnienie słabych zabezpieczeń do znacznie szerszej społeczności globalnej. Na szczęście dostawcy chmury wiedzą o zmianach, zwiększaniu i dodawaniu zagrożeń. Zainwestowali się silnie, aby zredukować te zagrożenia i zarządzać nimi w imieniu swoich klientów.

Ten artykuł nie koncentruje się na ryzyku w chmurze. Zamiast tego omawia ryzyko biznesowe związane z różnymi formami transformacji w chmurze. W dalszej części tego artykułu dyskusje przeniesieją fokus, aby omówić sposoby zrozumieć tolerancję biznesową dla ryzyka.

<!-- markdownlint-disable MD026 -->

## <a name="what-business-risks-are-associated-with-a-cloud-transformation"></a>Jakie zagrożenia biznesowe są związane z przekształceniem w chmurze?

Prawdziwe zagrożenia biznesowe opierają się na szczegółach określonych transformacji. Kilka typowych zagrożeń zapewnia konwersację Starter w celu zrozumienia zagrożeń specyficznych dla firmy.

> [!IMPORTANT]
> Przed przeczytaniem poniższych informacji należy pamiętać, że każde z tych zagrożeń może być zarządzane. Celem tego artykułu jest informowanie i przygotowanie czytelników do bardziej wydajnej dyskusji w zakresie zarządzania ryzykiem.

- **Naruszenie danych:** Liczba jednego ryzyka skojarzonego z dowolnym transformacjęm jest ochroną danych. Przecieki danych mogą spowodować znaczące szkody dla firmy, co prowadzi do utraty klientów, obniżenia biznesowej lub nawet odpowiedzialności prawnej. Wszelkie zmiany sposobu, w jaki dane są przechowywane, przetwarzane lub wykorzystywane, tworzą ryzyko. Przekształcenia w chmurze tworzą wysoki stopień zmian w zakresie zarządzania danymi, więc ryzyko nie powinno być podejmowane w sposób jasny. [Poziom odniesienia zabezpieczeń](../security-baseline/index.md), [Klasyfikacja danych](./data-classification.md)i [racjonalizacja przyrostowa](../../digital-estate/rationalize.md#incremental-rationalization) mogą pomóc w zarządzaniu tym ryzykiem.

- **Przerwanie działania usługi:** Działania biznesowe i środowiska klienta często polegają na operacjach technicznych. Przekształcenia w chmurze spowodują zmianę w operacjach IT. W niektórych organizacjach ta zmiana jest mała i łatwa do dostosowania. W innych organizacjach te zmiany mogą wymagać ponownego narzędzia, przeszkolenia lub nowych metod obsługi operacji w chmurze. Im większa zmiana, tym większy potencjalny wpływ na działalność biznesową i obsługę klienta. Zarządzanie tym ryzykiem wymaga zaangażowania firmy w planowanie transformacji. Planowanie wersji i wybór pierwszego obciążenia w artykule z [racjonalizacją przyrostową](../../digital-estate/rationalize.md#incremental-rationalization) omawia sposoby wybierania obciążeń dla projektów transformacji. Rolą biznesową w tym działaniu jest komunikacja polegające na tym, że ryzyko związane z ryzykiem związanym z zmianami obciążeń priorytetyzacji. Pomoc w wyborze obciążeń, które mają niższy wpływ na operacje, obniży ogólny czynnik ryzyka.

- **Kontrola budżetu:** Modele kosztów zmieniają się w chmurze. Ta zmiana może stworzyć ryzyko związane z przekroczeniem kosztów lub zwiększyć koszt sprzedanych towarów (KWS), szczególnie bezpośrednio związane z nimi koszty operacyjne. Gdy firma współpracuje ściśle z działem IT, możliwe jest utworzenie przejrzystości dotyczącej kosztów i usług używanych przez różne jednostki biznesowe, programy lub projekty. [Cost Management](../cost-management/index.md) zawiera przykłady sposobów prowadzenia działalności biznesowej i jej partnerów w tym temacie.

Powyżej przedstawiono kilka typowych zagrożeń wymienionych przez klientów. Zespół nadzorujący chmury i zespoły rozwiązań w chmurze mogą rozpocząć tworzenie profilu ryzyka, ponieważ są migrowane i readied w wersji produkcyjnej. Przygotuj się na konwersacje, aby określić, uściślić i zarządzać ryzykiem na podstawie żądanych wyników i nakładów pracy.

## <a name="understanding-risk-tolerance"></a>Poznanie tolerancji ryzyka

Identyfikowanie ryzyka to dość bezpośredni proces. Zagrożenia związane z IT są ogólnie standardowe w branży. Jednak tolerancja dla tego ryzyka jest specyficzna dla każdej organizacji. Jest to punkt, w którym konwersacje biznesowe i IT są w trakcie rozwieszania. Każda Strona rozmowy jest zasadniczo mówiąca o innym języku. Poniższe porównania i pytania są przeznaczone do uruchamiania rozmów, które pomagają każdej stronie lepiej zrozumieć i obliczą tolerancję ryzyka.

## <a name="simple-use-case-for-comparison"></a>Prosty przypadek użycia do porównania

Aby pomóc w zrozumieniu tolerancji ryzyka, przejdźmy do danych klienta. Jeśli firma w żadnej branży ogłasza dane klientów na niezabezpieczonym serwerze, ryzyko techniczne tego lub kradzieży tych danych jest w pełni takie samo. Jednak tolerancja firmy dla tego ryzyka będzie się różnić w zależności od rodzaju i potencjalnej wartości danych.

- Firmy w dziedzinie opieki zdrowotnej i finansów w Stany Zjednoczone podlegają sztywnym wymaganiom dotyczącym zgodności innych firm. Przyjęto założenie, że dane osobowe lub dane związane z opieką zdrowotną są niezwykle poufne. Istnieją poważne konsekwencje dla tych typów firm, jeśli są one uwzględnione w scenariuszu ryzyka powyżej. Ich tolerancja będzie niezwykle niska. Wszystkie dane klienta opublikowane wewnątrz lub poza siecią będą musiały podlegać zasadom zgodności innych firm.
- Firma do gier, której dane klienta są ograniczone do nazwy użytkownika, czasy odtwarzania i wysokie wyniki, nie mogą mieć znaczących skutków poza utratą w reputacji, jeśli prowadzą do powyższego zachowania. Mimo że niezabezpieczone dane są zagrożone, wpływ tego ryzyka jest niewielki. W związku z tym tolerancja dla ryzyka w tym przypadku jest wysoka.
- Średniej wielkości przedsiębiorstwa, która zapewnia usługom czyszczenia dywanów tysiącom klientów, będzie między tymi dwoma skrajnymi tolerancjami. Dane klientów mogą być bardziej niezawodne, zawierające szczegółowe informacje, takie jak adres lub numer telefonu. Oba te elementy mogą być traktowane jako dane osobowe i powinny być chronione. Niemniej jednak mogą nie istnieć żadne szczególne wymagania ładu, które mają na celu zabezpieczenie danych. Z perspektywy INFORMATYCZNej odpowiedź jest prosta i zabezpiecza dane. Z perspektywy biznesowej może nie być to proste. Aby określić poziom tolerancji dla tego ryzyka, firma będzie musiała uzyskać więcej szczegółów.

W następnej sekcji udostępniono kilka przykładowych pytań, które mogą pomóc firmie określić poziom odporności na ryzyko dla przypadków użycia powyżej lub innych.

## <a name="risk-tolerance-questions"></a>Pytania dotyczące tolerancji ryzyka

W tej sekcji wymieniono pytania wywołujące konwersacje w trzech kategoriach: wpływ na utratę, prawdopodobieństwo utraty i koszty korygowania. Gdy firma i partner IT odnoszą się do każdego z tych obszarów, można łatwo określić decyzję o wydatkach na zarządzanie ryzykiem oraz ogólną tolerancję dla określonego ryzyka.

**Wpływ na utratę:** Pytania dotyczące określania wpływu ryzyka. Odpowiedzi na te pytania mogą być trudne. Oszacowanie wpływu jest najlepsze, ale czasami sama konwersacja jest wystarczająca, aby zrozumieć tolerancję. Zakresy są również akceptowalne, szczególnie jeśli obejmują założenia, które określają te zakresy.

- Czy to ryzyko może naruszać wymagania dotyczące zgodności innych firm?
- Czy to ryzyko może naruszać wewnętrzne zasady firmowe?
- Czy to ryzyko może spowodować utratę życia, koniec lub właściwość?
- Czy ten czynnik ryzyka może być opłacalny dla klientów i udziału w rynku? Jeśli tak, czy można to posłużyć do policzalnego kosztu?
- Czy to zagrożenie może stworzyć negatywne środowiska klienta? Czy te środowiska mogą mieć wpływ na sprzedaż lub dochody?
- Czy w tym ryzyku można utworzyć nową odpowiedzialność prawną? Jeśli tak, czy istnieje pierwszeństwo dla nieprawidłowych nagród w tych typach przypadków?
- Czy może to spowodować zatrzymanie operacji firmowych? Jeśli tak, jak długo będą działać operacje?
- Czy może to spowodować spowolnienie operacji biznesowej? Jeśli tak, jak wolno i jak długo?
- Czy na tym etapie transformacji czy jest to ryzyko jednorazowe czy powtarzane?
- Czy ryzyko zwiększa się i zmniejsza częstotliwość w miarę postępu transformacji?
- Czy ryzyko zwiększa się i zmniejsza prawdopodobieństwo z upływem czasu?
- Czy ryzyko związane z czasem jest poufne? Czy ryzyko zostanie przekazane lub nastąpi gorsze, jeśli nie jest to rozkierowane?

Te pytania podstawowe będą prowadzić do wielu innych. Po zbadaniu dialogu w dobrej kondycji zaleca się zapisanie odpowiednich zagrożeń i, gdy jest to możliwe, ilościowe.

**Koszty korygowania ryzyka:** Pytania dotyczące określania kosztów usuwania lub w inny sposób minimalizowania ryzyka. Te pytania mogą być dość bezpośrednie, szczególnie w przypadku reprezentowania ich w zakresie.

- Czy istnieje jasne rozwiązanie i jaki jest koszt IT?
- Czy istnieją opcje zapobiegania i minimalizowania tego ryzyka? Jaki jest zakres kosztów dla tych rozwiązań?
- Co jest potrzebne od firmy, aby wybrać najlepsze, jasne rozwiązanie?
- Co jest potrzebne od firmy w celu sprawdzenia kosztów?
- Jakie inne korzyści mogą pochodzić z rozwiązania, które spowodowałoby usunięcie tego ryzyka?

Te pytania umożliwiają uproszczenie rozwiązań technicznych wymaganych do zarządzania lub usuwania zagrożeń. Jednak te pytania komunikują się z tymi rozwiązaniami w sposób, w jaki firma może szybko zintegrować się z procesem decyzyjnym.

**Prawdopodobieństwo utraty:** Pytania, aby określić, jak najprawdopodobniej jest to, że ryzyko stanie się rzeczywistością. Jest to najbardziej trudny obszar do określenia ilościowego. Zamiast tego zaleca się, aby zespół ładu w chmurze utworzył kategorie do komunikowania się z prawdopodobieństwem na podstawie danych pomocniczych. Poniższe pytania mogą pomóc w tworzeniu kategorii, które są zrozumiałe dla zespołu.

- Czy istnieją jakieś badania dotyczące prawdopodobieństwa zrealizowania tego ryzyka?
- Czy dostawca może dostarczyć odwołania lub dane statystyczne dotyczące prawdopodobieństwa wpływu?
- Czy istnieją inne firmy w odpowiednim sektorze lub w pionie, które zostały już trafione w tym ryzyku?
- Poszukaj jeszcze innych firm, które zostały już trafione w tym ryzyku?
- Czy to ryzyko jest unikatowe dla elementu, który jest niewłaściwie wykonywany przez firmę?

Po udzieleniu odpowiedzi na te pytania wraz z pytaniami ustalonymi przez zespół ds. zarządzania chmurą mogą pojawić się grupy prawdopodobieństwa. Poniżej przedstawiono kilka przykładów grupowania, które ułatwią rozpoczęcie pracy:

- **Brak wskazania:** Nie wykonano wystarczającej liczby badań, aby określić prawdopodobieństwo.
- **Niskie ryzyko:** Bieżące badania wskazują na realizację ryzyka.
- **Przyszłe ryzyko:** Bieżące prawdopodobieństwo jest niskie. Jednak kontynuowanie wdrażania wymagałoby nowej analizy.
- **Średnie ryzyko:** Istnieje prawdopodobieństwo, że ryzyko wpłynie na firmę.
- **Wysokie ryzyko:** W miarę upływu czasu może to spowodować, że firma będzie korzystać z tego ryzyka.
- **Zmniejszanie ryzyka:** Ryzyko ma średni poziom. Jednak działania w branży lub w firmie zmniejszają prawdopodobieństwo wpływu.

**Określanie tolerancji:**

Trzy powyższe pytania powinny mieć paliwo wystarczające dane, aby określić początkową tolerancję. Gdy ryzyko i prawdopodobieństwo są niskie, a koszty korygowania ryzyka są wysokie, firma jest mało prawdopodobne, aby przeprowadzić inwestycję w korygowanie. Gdy ryzyko i prawdopodobieństwo są wysokie, firma może rozważyć inwestycję, o ile koszty nie przekroczą potencjalnych zagrożeń.

## <a name="next-steps"></a>Następne kroki

Ten typ konwersacji może pomóc firmie i bardziej efektywnie oszacować tolerancję. Te konwersacje mogą być używane podczas tworzenia zasad MVP oraz podczas przeprowadzania przeglądów zasad.

> [!div class="nextstepaction"]
> [Zdefiniuj zasady firmowe](./policy-definition.md)
