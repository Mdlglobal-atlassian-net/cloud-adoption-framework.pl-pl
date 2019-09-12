---
title: Centrum doskonałości chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Opisuje sposób tworzenia centrum doskonałości (CCoE).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 9726cc5bea1d8f7852dbb8831fc211dda2f4f4f7
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906307"
---
# <a name="cloud-center-of-excellence"></a>Centrum doskonałości chmury

Elastyczność biznesowa i techniczna to podstawowe cele większości organizacji IT. Cloud Center of doskonałości (CCoE) to funkcja, która tworzy równowagę między szybkością i stabilnością.

## <a name="function-structure"></a>Struktura funkcji

CCoE wymaga współpracy między każdą z następujących możliwości:

- Wdrażanie w chmurze (w szczególnych architektach rozwiązań)
- Strategia chmury (w przypadku menedżerów programu i projektu)
- Ład w chmurze
- Platforma w chmurze
- Automatyzacja chmury

## <a name="impact-and-cultural-change"></a>Wpływ i zmiana kulturowa

Gdy ta funkcja jest prawidłowo strukturalna i obsługiwana, uczestnicy mogą przyspieszyć innowacje i migracje, jednocześnie zmniejszając całkowity koszt zmian i zwiększając elastyczność biznesową. Po pomyślnym wdrożeniu ta funkcja może generować zauważalne redukcje w czasie wprowadzania na rynek. Podobnie jak w przypadku najlepszych praktyk zespołów, wzrost wskaźników jakości może być widoczny, w tym niezawodność, wydajność wydajności, bezpieczeństwo, łatwość utrzymania i zadowolenie klientów. Te korzyści w zakresie wydajności, elastyczności i jakości są szczególnie istotne, jeśli firma planuje zaimplementowanie wysiłków migracji w chmurze na dużą skalę lub chęci do korzystania z chmury w celu zwiększenia innowacji związanych z rozróżnieniem rynku.

Po pomyślnym utworzeniu modelu CCoE będzie on miał znaczny wpływ na zmianę kulturowe. Podstawową podstawą podejścia CCoE jest to, że służy on jako Broker, partner lub przedstawiciel firmy. Ten model to wzór przesunięty od tradycyjnego widoku jako jednostkę operacji lub warstwę abstrakcji między zasobami biznesowymi i INFORMATYCZNymi.

Poniższa ilustracja przedstawia analogową zmianę kulturową. Bez podejścia CCoE, zamierza skupić się na zapewnianiu kontroli i odpowiedzialności centralnej, działającej podobnie jak stoplights. Gdy CCoE się powiedzie, fokus jest odpowiedzialny za wolne i delegowane odpowiedzialności, które są bardziej podobne do Roundabout w przecięciu.

![Analoging dla zmiany modelu CCoE](../_images/ready/ccoe-paradigm-shift.png)

Żaden z metod przedstawionych w powyższym obrazie analogowym nie jest prawidłowy lub nieprawidłowy. są one jedynie alternatywnymi widokami odpowiedzialności i zarządzania. Jeśli wolisz stworzyć model samoobsługowy, który umożliwia jednostkom biznesowym podejmowanie własnych decyzji przy zachowaniu zestawu wytycznych i ustalonych, powtarzalnych kontrolek, model CCoE może pasować do strategii technologicznej.

## <a name="key-responsibilities"></a>Kluczowe obowiązki

Głównym cłem zespołu CCoE jest przyspieszenie wdrażania chmury za pomocą rozwiązań natywnych lub hybrydowych.

Celem CCoE jest:

- Pomóż w tworzeniu nowoczesnej organizacji INFORMATYCZNej za pomocą podejścia Agile do przechwytywania i implementowania wymagań firmy.
- Użyj pakietów wdrożeniowych wielokrotnego użytku, które są zgodne z zasadami zarządzania zabezpieczeniami, zgodności i usług.
- Obsługa funkcjonalnej platformy platformy Azure w celu wyrównania przy użyciu procedur operacyjnych.
- Przejrzyj i zatwierdź korzystanie z narzędzi natywnych w chmurze.
- W miarę upływu czasu można znormalizować i zautomatyzować często używane składniki i rozwiązania platformy.

## <a name="meeting-cadence"></a>Erze spotkania

CCoE jest funkcją podaną przez cztery zespoły o dużej zapotrzebowaniu. Ważne jest, aby umożliwić współpracę organiczną i śledzenie wzrostu za pomocą wspólnego repozytorium/wykazu rozwiązań. Maksymalizuj interakcje naturalne, ale Zminimalizuj spotkania. Gdy ta funkcja jest dojrzała, zespoły powinny próbować ograniczyć liczbę przeznaczonych spotkań. Uczestnictwo w spotkaniach cyklicznych, takich jak spotkania wydania obsługiwane przez zespół ds. wdrażania chmury, udostępnia dane wejściowe. Równolegle, spotkanie po każdym planie wydania może zapewnić minimalny punkt dotykowy dla tego zespołu.

## <a name="solutions-and-controls"></a>Rozwiązania i kontrolki

Każdy element członkowski CCoE jest związany z zrozumieniem niezbędnych ograniczeń, ryzyka i ochrony, które doprowadziły do bieżącego zestawu formantów IT. Zbiorowe wysiłki CCoE powinny mieć na celu uwzględnienie rozwiązań w chmurze (lub hybrydowych), które umożliwiają odpowiednie wyniki biznesowe samoobsługi. W miarę tworzenia rozwiązań są one udostępniane różnym zespołom w formie formantów lub automatyzacji, które służą jako guardrails do różnych wysiłków. Te guardrails pomoc w kierowaniu działań związanych z przepływem pracy różnych zespołów i delegowanie obowiązków do uczestników w różnych procesach migracji lub innowacji.

Przykłady tego przejścia:

| Scenariusz | Rozwiązanie CCoE | Rozwiązanie po CCoE |
|---------|---------|---------|
| Inicjowanie obsługi administracyjnej SQL Server produkcyjnych | Zespoły sieci, IT i danych udostępniają różne składniki w ciągu kilku dni lub nawet tygodni. | Zespół wymagający serwera wdraża wystąpienie PaaS Azure SQL Database. Można również użyć prezatwierdzonego szablonu do wdrożenia wszystkich zasobów IaaS w chmurze w godzinach. |
| Inicjowanie obsługi administracyjnej środowiska programistycznego | Zespoły Network, IT, Development i DevOps wyrażają zgodę na specyfikacje i wdrożenie środowiska. | Zespół programistyczny definiuje własne specyfikacje i wdraża środowisko na podstawie przydzielonych budżetów. |
| Aktualizuj wymagania dotyczące zabezpieczeń, aby zwiększyć ochronę danych | Zespoły sieci, IT i zabezpieczeń umożliwiają aktualizowanie różnych urządzeń sieciowych i maszyn wirtualnych w wielu środowiskach w celu dodania ochrony. | Narzędzia do zarządzania chmurą służą do aktualizowania zasad, które mogą być stosowane natychmiast do wszystkich zasobów we wszystkich środowiskach w chmurze. |

## <a name="negotiations"></a>Negocjacji

W katalogu głównym dowolnego wysiłku CCoE jest proces trwającej negocjacji. Zespół CCoE negocjuje z istniejącymi funkcjami IT, aby zmniejszyć centralną kontrolę. Wady dla działalności firmy w tej negocjacji to swoboda, elastyczność i szybkość. Wartość handlu dla istniejących zespołów IT jest dostarczana jako nowe rozwiązania. Nowe rozwiązania zapewniają istniejący zespół IT z co najmniej jedną z następujących korzyści:

- Możliwość automatyzowania typowych problemów.
- Ulepszenia spójności (skrócenie w codziennym frustrations).
- Możliwość uczenia i wdrożenia nowych rozwiązań technicznych.
- Zmniejszenie zdarzeń o wysokiej ważności (mniej krótkich poprawek lub późnych odpowiedzi na pager).
- Możliwość rozszerzenia zakresu technicznego, który zajmuje się szerszymi tematami.
- Uczestnictwo w rozwiązaniach biznesowych wyższego poziomu, które dotyczą wpływu technologii.
- Zmniejszenie menial zadań konserwacyjnych.
- Zwiększenie strategii technologicznej i automatyzacji.

W programie Exchange dla tych korzyści istniejąca funkcja IT może być transakcją następujących wartości, niezależnie od tego, czy są prawdziwe czy postrzegane:

- Wykrywanie kontroli z ręcznych procesów zatwierdzania.
- Wykrywanie stabilności z kontroli zmian.
- Sense bezpieczeństwa zadań przed ukończeniem niezbędnych, niepowtarzalnych zadań.
- Wykrywanie spójności, które wynikają z przestrzegania istniejących dostawców rozwiązań IT.

W dobrej kondycji firmy, ten proces negocjacji jest dynamiczną konwersacją między elementami równorzędnymi i partnerskimi zespołami IT. Szczegóły techniczne mogą być złożone, ale można nimi zarządzać, gdy rozumieją one cel i wspierają wysiłki CCoE. Gdy ta wartość jest mniejsza niż pomoc techniczna, Poniższa sekcja dotycząca włączania sukcesu CCoE może pomóc w przezwyciężeniu kultur kultury.

## <a name="enabling-ccoe-success"></a>Włączanie CCoE

Przed przystąpieniem do tego modelu należy sprawdzić poprawność odporności firmy na sposób myślenia wzrostu i wygodę o wydaniu centralnych obowiązków. Jak wspomniano powyżej, celem CCoE jest wymiana kontroli nad elastyczność i szybkość.

Ten typ zmiany obejmuje czas, eksperymentowanie i negocjowanie. Podczas tego procesu dojrzewania wystąpią nierówności i ustawienia. Jeśli jednak zespół pozostanie sumienni i nie zostanie zaakceptowany z eksperymentu, istnieje wysokie prawdopodobieństwo pomyślnego poprawienia elastyczności, szybkości i niezawodności. Jednym z największych czynników dotyczących sukcesu lub niepowodzenia CCoE jest obsługa od lidera i kluczowych uczestników projektu.

### <a name="key-stakeholders"></a>Najważniejsze osoby zainteresowane

Liderem jest pierwszy i najbardziej oczywisty uczestnik projektu. Menedżerowie IT będą odgrywać ważną część. Jednak w trakcie tego procesu jest wymagana obsługa CIO i innych liderów IT na poziomie kierownictwa.

Mniej oczywisty jest potrzebą dla uczestników biznesowych. Elastyczność biznesowa i czas wprowadzenia na rynek to kluczowe motywacje do tworzenia CCoE. W związku z tym najważniejsze osoby biorące udział w tych obszarach powinny mieć przyznane zainteresowanie. Przykłady uczestników biznesowych obejmują liderów biznesowych, kadry kierowniczej, dyrektorów operacji i właścicieli produktów biznesowych.

### <a name="business-stakeholder-support"></a>Wsparcie biznesowe uczestnika

CCoE wysiłki mogą być przyspieszone z pomocą techniczną zainteresowanych stron firmy. Większość wysiłków związanych z CCoEem jest skoncentrowana na rozwinięcia długoterminowych ulepszeń biznesowych i szybkości. Zdefiniowanie wpływu bieżących modeli operacyjnych i wartości ulepszeń jest przydatne jako narzędzie przewodnika i negocjowania dla CCoE. Dokumentowanie następujących elementów jest sugerowane dla wsparcia CCoE:

- Ustanów zestaw wyników i celów działalności, które są oczekiwane w wyniku elastyczności i szybkości działania firmy.
- Jasno definiować wyłączane punkty utworzone przez bieżące procesy IT (takie jak szybkość, elastyczność, stabilność i wyzwania dotyczące kosztów).
- Jasno określaj historyczny wpływ tych problemów, takich jak utracony udział w rynku, korzyści dla konkurentów w funkcjach i funkcje, słabe środowiska klienta i wzrost budżetu.
- Zdefiniuj możliwości poprawy biznesowe, które są blokowane przez bieżące punkty i modele operacyjne.
- Ustanów osie czasu i metryki związane z tymi szansami.

Te punkty danych nie są na nim atakowane. Zamiast tego pomagają CCoE uczyć się od przeszłości i tworzyć realistyczne zaległości oraz planować ulepszenia.

**Ciągła pomoc techniczna i zaangażowanie:** Zespoły CCoE mogą przedstawiać szybkie zwroty w niektórych obszarach. Jednak cele wyższego poziomu, takie jak elastyczność biznesowa i czas wprowadzenia na rynek, mogą zająć dużo czasu. W trakcie dojrzewania istnieje duże ryzyko, że CCoE nie zostanie zaakceptowany lub wycofane, aby skoncentrować się na innych wysiłkach IT.

W okresie pierwszych sześciu do dziewięciu miesięcy CCoE się, że zainteresowane strony biznesowe przydzielą czas na spełnienie miesięcznego lidera IT i CCoE. W przypadku formalnych procedury do tych spotkań istnieje niewielkie zapotrzebowanie. Wystarczy pamiętać, że CCoE członkowie i ich kierownictwo znaczenia tego programu mogą wejść w sposób, aby CCoE sukces.

Ponadto zalecamy, aby zainteresowane strony biznesowe były poinformowane o postępie i zablokowaniu napotykanym przez zespół CCoE. Wiele z ich wysiłków będzie wyglądać jak techniczne minutiae. Jednak ważne jest, aby zainteresowane strony mogły zrozumieć postęp planu, dzięki czemu mogą one mieć wpływ na to, kiedy zespół rozwiąże pary lub rozprasza inne priorytety.

### <a name="it-stakeholder-support"></a>Pomoc techniczna dla działu IT

**Obsługa wizji:** Pomyślne CCoE pracy wymaga dużej liczby negocjacji z istniejącymi członkami zespołu IT. Po wykonaniu tych czynności wszystkie te składniki przyczyniają się do rozwiązania i zauważają się za odpowiednie zmiany. Jeśli tak się nie dzieje, niektórzy członkowie istniejącego zespołu IT mogą chcieć zamieścić mechanizmy kontroli z różnych powodów. Wsparcie dla udziałowców IT jest istotne dla sukcesu CCoE, gdy wystąpią takie sytuacje. Zachęcanie i wzmocnienie ogólnych celów CCoE jest ważne, aby rozwiązać blokować odpowiednie negocjacje. W rzadkich przypadkach zainteresowane strony IT mogą nawet wymagać dalszych czynności i rozdzielić zakleszczenie lub głos związany z CCoEem.

**Zachowaj fokus:** CCoE może być znaczącym zobowiązaniem dla dowolnego zespołu z ograniczoną ilością zasobów. Usuwanie silnych architektów z projektów krótkoterminowych do skoncentrowania się na długoterminowych korzyściach może stworzyć trudności dla członków zespołu, którzy nie są częścią CCoE. Ważne jest, aby skoncentrować się na tym, i że uczestnicy IT pozostają w stanie skupić się na celu CCoE. Obsługa liderów IT i udziałowców IT jest wymagana do rozróżnienia zakłóceń codziennych operacji na rzecz CCoE obowiązków.

**Utwórz bufor:** Zespół CCoE będzie eksperymentować z nowymi metodami. Niektóre z tych metod nie są dobrze wyrównane z istniejącymi operacjami lub ograniczeniami technicznymi. Istnieje realne ryzyko wystąpienia CCoE w przypadku, gdy eksperymenty kończą się niepowodzeniem. Ważne jest, aby zachęcić i buforować zespół z powodu skutków "szybkiej awarii". Równie ważne jest, aby zapewnić, że zespół jest odpowiedzialny za rozwój sposób myślenia, dzięki czemu są one dostępne do uczenia się i znajdowania lepszych rozwiązań.

## <a name="next-steps"></a>Następne kroki

W przypadku usługi Cloud Center doskonałości wymagane są zarówno [możliwości platformy w chmurze](./cloud-platform.md) , jak i [Automatyzacja chmury](./cloud-automation.md). Następnym krokiem jest dostosowanie [możliwości platformy w chmurze](./cloud-platform.md).

> [!div class="nextstepaction"]
> [Wyrównywanie możliwości platformy w chmurze](./cloud-platform.md)
