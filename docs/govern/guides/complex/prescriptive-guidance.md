---
title: 'Kompleksowe zarządzanie przedsiębiorstwem: wyjaśniono najlepsze rozwiązania'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby utworzyć minimalny produkt żywotny (MVP) dla zarządzania, który odzwierciedla najlepsze rozwiązania dla złożonego przedsiębiorstwa.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dcd7c58a1e89539dcec62cf63615c4fb88d9fe08
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83754901"
---
# <a name="governance-guide-for-complex-enterprises-best-practices-explained"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: objaśniono najlepsze rozwiązania

Przewodnik dotyczący ładu rozpoczyna się od zestawu początkowych [zasad firmowych](./initial-corporate-policy.md). Te zasady służą do ustanowienia minimalnego produktu żywotnego dla ładu, który odzwierciedla [najlepsze rozwiązania](./index.md).

W tym artykule omówiono strategie wysokiego poziomu, które są wymagane do utworzenia programu MVP (ładu). Rdzeń programu ładu MVP to [dyscyplina wdrażania](../../deployment-acceleration/index.md). Narzędzia i wzorce stosowane na tym etapie umożliwiają udoskonalenia przyrostowe, które są konieczne do rozwinięcia ładu w przyszłości.

## <a name="governance-mvp-initial-governance-foundation"></a>SPECJALISTa-ładu (początkowa ładu)

Szybkie wdrażanie ładu i zasad firmowych jest osiągalne dzięki kilku prostym zasadom i narzędziom do zarządzania opartemu na chmurze. Są to pierwsze trzy dyscypliny ładu do podejścia w każdym procesie zarządzania. Każda dyscyplina zostanie omówiona w tym artykule.

<!--docsTest:ignore "Identity Baseline, Security Baseline, and Deployment Acceleration disciplines" -->

Aby ustalić punkt początkowy, ten artykuł zawiera omówienie strategii wysokiego poziomu związanych z zasadami odniesienia, linii bazowej zabezpieczeń i przyspieszenia wdrożenia, które są wymagane do utworzenia MVP, które będą stanowić podstawę dla wszystkich rozwiązań.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proces implementacji

Implementacja programu ładu MVP ma zależności dotyczące tożsamości, zabezpieczeń i sieci. Po rozwiązaniu zależności zespół nadzorujący chmury podejmie decyzję o kilku aspektach zarządzania. Decyzje z zespołu nadzoru chmurowego i z zespołów pomocniczych zostaną wdrożone za pośrednictwem jednego pakietu aktywów wymuszania.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp-implementation-flow.png)

Tę implementację można również opisać przy użyciu prostej listy kontrolnej:

1. Prośba o decyzje dotyczące podstawowych zależności: tożsamości, sieci i szyfrowania.
1. Określ wzorzec, który ma być używany podczas wymuszania zasad firmowych.
1. Określ odpowiednie wzorce ładu na potrzeby spójności zasobów, tagowania zasobów oraz rejestrowania i raportowania.
1. Zaimplementuj narzędzia ładu dostosowane do wybranego wzorca wymuszania zasad, aby zastosować zależne decyzje i decyzje nadzoru.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Stosowanie wzorców zdefiniowanych przez ładu

Zespół ds. zarządzania chmurą będzie odpowiedzialny za następujące decyzje i implementacje. Wiele będzie wymagało danych wejściowych od innych zespołów, ale zespół nadzorujący chmury może być w stanie zarówno podjąć decyzję, jak i implementację. W poniższych sekcjach przedstawiono decyzje podejmowane w przypadku użycia i szczegółowe informacje o każdej decyzji.

### <a name="subscription-design"></a>Projekt subskrypcji

Decyzja dotycząca tego, w jaki sposób konstrukcja subskrypcji pozwala określić, jak subskrypcje platformy Azure mają być strukturalne i w jaki sposób grupy zarządzania platformy Azure będą używane do wydajnego zarządzania dostępem, zasadami i zgodnością z tą subskrypcją. W tym opisie zespół nadzoru zdecydował się na [strategię mieszanych subskrypcji](../../../decision-guides/subscriptions/index.md#mix-subscription-strategies).

- W miarę istnienia nowych żądań dotyczących zasobów platformy Azure _dział_ powinien zostać ustanowiony dla każdej głównej jednostki biznesowej w każdej lokalizacji geograficznej. W ramach każdego z działów należy utworzyć _subskrypcje_ dla każdej aplikacji Archetype.
- Aplikacja Archetype to metoda grupowania aplikacji z podobnymi potrzebami. Typowe przykłady obejmują:
  - Aplikacje z chronionymi danymi, zarządzanymi aplikacjami (na przykład HIPAA lub FedRAMP).
  - Aplikacje o niskim ryzyku.
  - Aplikacje z zależnościami lokalnymi.
  - Oprogramowanie SAP lub inne aplikacje mainframe na platformie Azure.
  - Aplikacje, które poszerzają lokalne aplikacje SAP lub mainframe.
  Każda organizacja ma unikatowe potrzeby na podstawie klasyfikacji danych i typów aplikacji, które obsługują działalność biznesową. Mapowanie zależności podpisu cyfrowego może pomóc w definiowaniu Archetypes aplikacji w organizacji.
- Wspólna konwencja nazewnictwa powinna zostać przyjęta w ramach projektu subskrypcji, zgodnie z powyższym opisem.

### <a name="resource-consistency"></a>Spójność zasobów

Decyzje dotyczące spójności zasobów określają narzędzia, procesy i nakłady potrzebne do zapewnienia spójnego wdrażania i konfigurowania zasobów platformy Azure w ramach subskrypcji. W tym opisie [spójność wdrożenia](../../../decision-guides/resource-consistency/index.md#deployment-consistency) została wybrana jako wzorzec spójności zasobów podstawowych.

- Grupy zasobów są tworzone dla aplikacji przy użyciu podejścia cyklu życia. Wszystkie elementy, które są tworzone, konserwowane i wycofane, powinny znajdować się w jednej grupie zasobów. Aby uzyskać więcej informacji, zobacz [Przewodnik po decyzji o spójności zasobów](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy należy zastosować do wszystkich subskrypcji ze skojarzonej grupy zarządzania.
- W ramach procesu wdrażania szablony spójności zasobów platformy Azure dla grupy zasobów powinny być przechowywane w kontroli źródła.
- Każda grupa zasobów jest skojarzona z określonym obciążeniem lub aplikacją na podstawie opisanego powyżej podejścia cyklu życia.
- Grupy zarządzania platformy Azure umożliwiają aktualizowanie projektów ładu jako dojrzałych zasad firmowych.
- Rozbudowana implementacja Azure Policy może przekroczyć zobowiązania dotyczące czasu zespołu i może nie zapewniać w tym momencie ogromnej wartości. Należy utworzyć proste zasady domyślne i zastosować je do każdej grupy zarządzania, aby wymusić niewielką liczbę bieżących instrukcji zasad ładu chmury. Te zasady określają implementację określonych wymagań ładu. Te implementacje można następnie zastosować dla wszystkich wdrożonych zasobów.

>[!IMPORTANT]
>Gdy zasób w grupie zasobów nie będzie już współużytkować tego samego cyklu życia, powinien zostać przeniesiony do innej grupy zasobów. Przykłady obejmują typowe bazy danych i składniki sieciowe. Chociaż mogą one obsłużać opracowywaną aplikację, mogą również być w innych grupach zasobów.

### <a name="resource-tagging"></a>Tagowanie zasobów

Decyzje dotyczące tagowania zasobów określają sposób stosowania metadanych do zasobów platformy Azure w ramach subskrypcji w celu obsługi operacji, zarządzania i ewidencjonowania aktywności. W tym opisie wzorzec [księgowości](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns) został wybrany jako domyślny model dla tagowania zasobów.

- Wdrożone zasoby powinny być oznaczone wartościami dla:
  - Jednostka działu lub rozliczeń
  - Lokalizacja geograficzna
  - Klasyfikacja danych
  - Zagrożenia
  - Umowa SLA
  - Środowisko
  - Archetype aplikacji
  - Aplikacja
  - Właściciel aplikacji
- Te wartości, wraz z grupą zarządzania systemu Azure i subskrypcją skojarzoną ze wdrożonym elementem zawartości, będą podejmować decyzje dotyczące zarządzania, działania i zabezpieczeń.

### <a name="logging-and-reporting"></a>Rejestrowanie i raportowanie

Decyzje dotyczące rejestrowania i raportowania określają, w jaki sposób dane dzienników są przechowywane i jak narzędzia do monitorowania i raportowania, które informują personel działu IT o kondycji operacyjnej, są strukturalne. W tym rozwinięcia można zasugerować wzorzec [monitorowania hybrydowego](../../../decision-guides/logging-and-reporting/index.md) do rejestrowania i raportowania, ale nie jest to wymagane w żadnym zespole programistycznym.

- Obecnie nie ma żadnych wymagań dotyczących ładu dotyczących konkretnych punktów danych, które mają być zbierane w celach rejestrowania lub raportowania. Jest to charakterystyczne dla tego fikcyjnych opisów i powinny być uznawane za antywzorców. Standardy rejestrowania powinny być określane i wymuszane najszybciej, jak to możliwe.
- Wymagana jest dodatkowa Analiza przed wydaniem jakichkolwiek chronionych danych lub obciążeń o krytycznym znaczeniu.
- Przed obsługą chronionych danych lub obciążeń o krytycznym znaczeniu, istniejące lokalne rozwiązanie do monitorowania operacyjnego należy udzielić dostępu do obszaru roboczego używanego do rejestrowania. Aplikacje są wymagane do spełnienia wymagań dotyczących zabezpieczeń i rejestrowania związanych z użyciem tej dzierżawy, jeśli aplikacja ma być obsługiwana w ramach zdefiniowanej umowy SLA.

## <a name="incremental-of-governance-processes"></a>Przyrost procesów ładu

Niektóre instrukcje zasad nie mogą być kontrolowane przez zautomatyzowane narzędzia. Inne zasady będą wymagały okresowego nakładu pracy z firmowymi i lokalnymi punktami odniesienia tożsamości. Zespół nadzorujący chmury musi nadzorować następujące procesy w celu zaimplementowania ostatnich ośmiu instrukcji zasad:

**Zmiany zasad firmowych:** Zespół nadzorujący w chmurze wprowadzi zmiany w projekcie ładu MVP, aby przyjąć nowe zasady. Wartością ładu MVP jest umożliwienie automatycznego wymuszania nowych zasad.

**Przyspieszenie wdrożenia:** Zespół ds. zarządzania chmurą przeglądał skrypty wdrażania w wielu zespołach. Zachowały one zestaw skryptów, które służą jako szablony wdrażania. Te szablony mogą być używane przez zespoły wdrażania chmury i zespoły DevOps do szybszego definiowania wdrożeń. Każdy skrypt zawiera wymagania dotyczące wymuszania zasad ładu i dodatkowe wysiłki z zakresu inżynierów rozwiązań w chmurze nie są wymagane. Curators te skrypty mogą szybciej wdrażać zmiany zasad. Ponadto są one wyświetlane jako akceleratory przyjęcia. Zapewnia to spójne wdrożenia bez ścisłego egzekwowania przestrzegania.

**Szkolenia inżynierów:** Zespół ds. zarządzania chmurą oferuje wielomiesięczne sesje szkoleniowe i utworzył dwa filmy wideo dla inżynierów. Oba zasoby ułatwiają inżynierom szybkie rozpoczęcie pracy nad kulturą ładu i sposób wykonywania wdrożeń. Zespół dodaje aktywa szkoleniowe, aby zademonstrować różnicę między wdrożeniami w środowisku produkcyjnym i nieprodukcyjnym, które ułatwiają inżynierom zrozumienie, jak nowe zasady wpływają na wdrażanie. Zapewnia to spójne wdrożenia bez ścisłego egzekwowania przestrzegania.

**Planowanie wdrożenia:** Przed wdrożeniem dowolnego elementu zawartości zawierającego chronione dane zespół ds. zarządzania chmurą będzie odpowiedzialny za przeglądanie skryptów wdrożenia w celu weryfikacji wyrównania ładu. Istniejące zespoły z wcześniej zatwierdzonymi wdrożeniami zostaną poddane inspekcji przy użyciu narzędzi programistycznych.

**Miesięczne inspekcje i raportowanie:** Każdy miesiąc zespół nadzorujący chmury uruchamia inspekcję wszystkich wdrożeń w chmurze, aby zweryfikować dalsze wyrównanie do zasad. Gdy zostaną odnalezione odchylenia, są one udokumentowane i udostępniane zespołom wdrożenia chmury. Gdy wymuszanie nie powoduje ryzyka przerwania działania lub wycieku danych, zasady są automatycznie wymuszane. Na końcu inspekcji zespół ds. zarządzania chmurą kompiluje Raport dla zespołu strategii chmury i każdego zespołu adopcji w chmurze, aby komunikować się ogólnie z zasadami. Raport jest również przechowywany na potrzeby inspekcji i przepisów prawnych.

**Kwartalne przeglądy zasad:** W każdym kwartale zespół ds. nadzoru chmurowego i zespół strategii chmury mogą przeglądać wyniki inspekcji i zasugerować zmiany w zasadach firmowych. Wiele z tych sugestii jest wynikiem ciągłego ulepszania i obserwacji wzorców użytkowania. Zatwierdzone zmiany zasad są zintegrowane z narzędziami do zarządzania podczas kolejnych cykli inspekcji.

## <a name="alternative-patterns"></a>Wzorce alternatywne

Jeśli którykolwiek z wzorców wybranych w tym przewodniku ładu nie jest wyrównany do wymagań czytnika, dostępne są alternatywy dla każdego wzorca:

- [Wzorce szyfrowania](../../../decision-guides/encryption/index.md)
- [Wzorce tożsamości](../../../decision-guides/identity/index.md)
- [Wzorce rejestrowania i raportowania](../../../decision-guides/logging-and-reporting/index.md)
- [Wzorce wymuszania zasad](../../../decision-guides/policy-enforcement/index.md)
- [Wzorce spójności zasobów](../../../decision-guides/resource-consistency/index.md)
- [Wzorce tagowania zasobów](../../../decision-guides/resource-tagging/index.md)
- [Wzorce sieci zdefiniowane przez oprogramowanie](../../../decision-guides/software-defined-network/index.md)
- [Wzorce projektowe subskrypcji](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Następne kroki

Po wdrożeniu tych wskazówek każdy zespół rozwiązań w chmurze może kontynuować pracę z ciągłym zarządzaniem. W tym samym czasie zespół ds. zarządzania chmurą będzie działał w celu ciągłego aktualizowania zasad firmowych i dyscyplin nadzoru.

Oba zespoły będą używać wskaźników tolerancji do identyfikowania następnego zestawu ulepszeń niezbędnych do kontynuowania obsługi wdrożenia chmury. Następnym krokiem dla tej firmy jest przyrostowe ulepszenie planu bazowego zarządzania w celu obsługi aplikacji ze starszymi lub niezależnymi wymaganiami usługi uwierzytelniania wieloskładnikowego.

> [!div class="nextstepaction"]
> [Udoskonalanie dziedziny Punktu odniesienia obsługi tożsamości](./identity-baseline-improvement.md)
