---
title: 'Standardowe zarządzanie przedsiębiorstwem: wyjaśniono najlepsze rozwiązania'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby utworzyć minimalny produkt żywotny (MVP) dla zarządzania, który odzwierciedla najlepsze rozwiązania dla standardowego przedsiębiorstwa.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 328577aae931194517e015973a935de24b580a96
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80995243"
---
# <a name="standard-enterprise-governance-guide-best-practices-explained"></a>Standardowy Przewodnik dotyczący zarządzania przedsiębiorstwem: objaśniono najlepsze rozwiązania

Przewodnik dotyczący ładu rozpoczyna się od zestawu początkowych [zasad firmowych](./initial-corporate-policy.md). Te zasady są używane do ustanowienia ładu SPECJALISTy, który odzwierciedla [najlepsze rozwiązania](./index.md).

W tym artykule omówiono strategie wysokiego poziomu, które są wymagane do utworzenia programu MVP (ładu). Rdzeń programu ładu MVP to dyscyplina [wdrażania](../../deployment-acceleration/index.md) . Narzędzia i wzorce stosowane na tym etapie umożliwiają udoskonalenia przyrostowe, które są konieczne do rozwinięcia ładu w przyszłości.

## <a name="governance-mvp-initial-governance-foundation"></a>SPECJALISTa-ładu (początkowa ładu)

Szybkie wdrażanie ładu i zasad firmowych jest osiągalne dzięki kilku prostym zasadom i narzędziom do zarządzania opartemu na chmurze. Są to trzy pierwsze dyscypliny do podejścia w każdym procesie zarządzania. Każda dyscyplina zostanie szczegółowo opisana w tym artykule.

Aby ustalić punkt początkowy, ten artykuł zawiera omówienie strategii wysokiego poziomu związanych z zasadami odniesienia, linii bazowej zabezpieczeń i przyspieszeniem wdrażania, które są wymagane do utworzenia MVP (ładu), który będzie stanowić podstawę dla całego wdrożenia.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proces implementacji

Implementacja programu ładu MVP ma zależności dotyczące tożsamości, zabezpieczeń i sieci. Po rozwiązaniu zależności zespół nadzorujący chmury podejmie decyzję o kilku aspektach zarządzania. Decyzje z zespołu nadzoru chmurowego i z zespołów pomocniczych zostaną wdrożone za pośrednictwem jednego pakietu aktywów wymuszania.

![Przykład programu MVP ładu przyrostowego](../../../_images/govern/governance-mvp-implementation-flow.png)

Tę implementację można również opisać przy użyciu prostej listy kontrolnej:

1. Prośba o decyzje dotyczące podstawowych zależności: tożsamości, sieci, monitorowania i szyfrowania.
2. Określ wzorzec, który ma być używany podczas wymuszania zasad firmowych.
3. Określ odpowiednie wzorce ładu dotyczące spójności zasobów, tagowania zasobów oraz dyscyplin rejestrowania i raportowania.
4. Zaimplementuj narzędzia ładu dostosowane do wybranego wzorca wymuszania zasad, aby zastosować zależne decyzje i decyzje nadzoru.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Stosowanie wzorców zdefiniowanych przez ładu

Zespół ds. zarządzania chmurą jest odpowiedzialny za następujące decyzje i implementacje. Wiele wymaga danych wejściowych z innych zespołów, ale zespół nadzorujący chmury może być członkiem zarówno decyzji, jak i implementacji. W poniższych sekcjach przedstawiono decyzje podejmowane w przypadku użycia i szczegółowe informacje o każdej decyzji.

### <a name="subscription-design"></a>Projekt subskrypcji

Decyzja dotycząca tego, w jaki sposób konstrukcja subskrypcji pozwala określić, jak subskrypcje platformy Azure mają być strukturalne i w jaki sposób grupy zarządzania platformy Azure będą używane do wydajnego zarządzania dostępem, zasadami i zgodnością z tą subskrypcją. W tych rozdziałach zespół nadzoru ustanowił subskrypcje dla wzorców produkcji i nieprodukcyjnej subskrypcji [produkcji](../../../ready/azure-best-practices/initial-subscriptions.md) i nieprodukcyjnych.

- W przypadku bieżącego fokusu działy nie są wymagane. Wdrożenia powinny być ograniczone w ramach pojedynczej jednostki rozliczeniowej. Na etapie przyjmowania nie można nawet mieć umowy Enterprise Agreement umożliwiającej scentralizowane rozliczanie. Jest to możliwe, że ten poziom wdrożenia jest zarządzany przez pojedynczą subskrypcję platformy Azure z opcją płatność zgodnie z rzeczywistym użyciem.
- Bez względu na użycie portalu EA lub istnienie umowy Enterprise Agreement, model subskrypcji powinien nadal być zdefiniowany i uzgodniony, aby zminimalizować przekroczenie kosztów administracyjnych.
- Wspólna konwencja nazewnictwa powinna zostać uzgodniona w ramach projektu subskrypcji w oparciu o poprzednie dwa punkty.

### <a name="resource-consistency"></a>Spójność zasobów

Decyzje dotyczące spójności zasobów określają narzędzia, procesy i nakłady potrzebne do zapewnienia spójnego wdrażania i konfigurowania zasobów platformy Azure w ramach subskrypcji. W tym opisie **[spójność wdrożenia](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** została wybrana jako wzorzec spójności zasobów podstawowych.

- Grupy zasobów są tworzone dla aplikacji przy użyciu podejścia cyklu życia. Wszystkie elementy, które są tworzone, konserwowane i wycofane, powinny znajdować się w jednej grupie zasobów. Aby uzyskać więcej informacji, zobacz [Przewodnik po decyzji o spójności zasobów](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy należy zastosować do wszystkich subskrypcji ze skojarzonej grupy zarządzania.
- W ramach procesu wdrażania szablony spójności zasobów platformy Azure dla grupy zasobów powinny być przechowywane w kontroli źródła.
- Każda grupa zasobów jest skojarzona z określonym obciążeniem lub aplikacją na podstawie opisanego powyżej podejścia cyklu życia.
- Grupy zarządzania platformy Azure umożliwiają aktualizowanie projektów ładu jako dojrzałych zasad firmowych.
- Rozbudowana implementacja Azure Policy może przekroczyć zobowiązania dotyczące czasu zespołu i może nie zapewniać w tym momencie ogromnej wartości. Należy jednak utworzyć proste zasady domyślne i zastosować je do każdej grupy zarządzania w celu wymuszenia niewielkiej liczby bieżących instrukcji zasad ładu w chmurze. Te zasady określają implementację określonych wymagań ładu. Te implementacje można następnie zastosować dla wszystkich wdrożonych zasobów.

>[!IMPORTANT]
>Gdy zasób w grupie zasobów nie będzie już współużytkować tego samego cyklu życia, powinien zostać przeniesiony do innej grupy zasobów. Przykłady obejmują typowe bazy danych i składniki sieciowe. Chociaż mogą one obsłużać opracowywaną aplikację, mogą również być w innych grupach zasobów.

### <a name="resource-tagging"></a>Tagowanie zasobów

Decyzje dotyczące tagowania zasobów określają sposób stosowania metadanych do zasobów platformy Azure w ramach subskrypcji w celu obsługi operacji, zarządzania i ewidencjonowania aktywności. W tym opisie wzorzec **[klasyfikacji](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** został wybrany jako domyślny model dla tagowania zasobów.

- Wdrożone zasoby powinny być otagowane przy użyciu:
  - Klasyfikacja danych
  - Zagrożenia
  - Umowa SLA
  - Środowisko
- Te cztery wartości umożliwią zarządzanie decyzjami, działaniami i zabezpieczeniami.
- Jeśli ten przewodnik dotyczący ładu jest implementowany dla jednostki biznesowej lub zespołu w ramach większej firmy, znakowanie powinno również zawierać metadane dla jednostki rozliczeniowej.

### <a name="logging-and-reporting"></a>Rejestrowanie i raportowanie

Decyzje dotyczące rejestrowania i raportowania określają, w jaki sposób dane dzienników są przechowywane i jak narzędzia do monitorowania i raportowania, które informują personel działu IT o kondycji operacyjnej, są strukturalne. W tym opisie zasugerowano [wzorzec natywny w chmurze](../../../decision-guides/logging-and-reporting/index.md#cloud-native)* * na potrzeby rejestrowania i raportowania.

## <a name="incremental-improvement-of-governance-processes"></a>Przyrostowe ulepszanie procesów ładu

Zgodnie z zmianami ładu niektóre instrukcje zasad nie mogą być kontrolowane przez zautomatyzowane narzędzia. Inne zasady będą powodować wysiłki zespołu ds. zabezpieczeń IT i lokalnego zespołu zarządzania tożsamościami z upływem czasu. Aby ułatwić zarządzanie nowymi zagrożeniami, zespół ds. zarządzania chmurą nadzoruje następujące procesy.

**Przyspieszenie wdrożenia:** Zespół ds. zarządzania chmurą przeglądał skrypty wdrażania w wielu zespołach. Utrzymują one zestaw skryptów, które służą jako szablony wdrażania. Te szablony są używane przez zespoły wdrażania i DevOps w chmurze w celu szybszego definiowania wdrożeń. Każdy z tych skryptów zawiera wymagania niezbędne do wymuszenia zestawu zasad ładu bez dodatkowych wysiłków od inżynierów rozwiązań w chmurze. W curators tych skryptów zespół nadzorujący chmury może szybko zaimplementować zmiany zasad. W wyniku nadzoru skryptów zespół ds. zarządzania chmurą jest traktowany jako źródło przyspieszenia wdrażania. Powoduje to utworzenie spójności między wdrożeniami, bez ścisłego wymuszenia przestrzegania.

**Szkolenia inżynierów:** Zespół ds. zarządzania chmurą oferuje wielomiesięczne sesje szkoleniowe i utworzył dwa filmy wideo dla inżynierów. Te materiały ułatwiają inżynierom szybkie zapoznanie się z kulturą ładu i wykonywanie czynności wykonywanych podczas wdrożeń. Zespół dodaje zasoby szkoleniowe, które pokazują różnicę między wdrożeniami produkcyjnymi i nieprodukcyjnymi, dzięki czemu inżynierowie będą zrozumieć, jak nowe zasady wpłyną na przyjęcie. Powoduje to utworzenie spójności między wdrożeniami, bez ścisłego wymuszenia przestrzegania.

**Planowanie wdrożenia:** Przed wdrożeniem dowolnego elementu zawartości zawierającego chronione dane zespół nadzorujący chmury będzie przeglądać skrypty wdrażania, aby sprawdzić poprawność wyrównania ładu. Istniejące zespoły z wcześniej zatwierdzonymi wdrożeniami zostaną poddane inspekcji przy użyciu narzędzi programistycznych.

**Miesięczne inspekcje i raportowanie:** Każdy miesiąc zespół nadzorujący chmury uruchamia inspekcję wszystkich wdrożeń w chmurze, aby zweryfikować dalsze wyrównanie do zasad. Gdy zostaną odnalezione odchylenia, są one udokumentowane i udostępniane zespołom wdrożenia chmury. Gdy wymuszanie nie powoduje ryzyka przerwania działania lub wycieku danych, zasady są automatycznie wymuszane. Na końcu inspekcji zespół ds. zarządzania chmurą kompiluje Raport dla zespołu strategii chmury i każdego zespołu adopcji w chmurze, aby komunikować się ogólnie z zasadami. Raport jest również przechowywany na potrzeby inspekcji i przepisów prawnych.

**Kwartalne przeglądy zasad:** W każdym kwartale zespół ds. zarządzania chmurą i zespół strategii chmury będą przeglądać wyniki inspekcji i zasugerować zmiany w zasadach firmowych. Wiele z tych sugestii jest wynikiem ciągłego ulepszania i obserwacji wzorców użytkowania. Zatwierdzone zmiany zasad są zintegrowane z narzędziami do zarządzania podczas kolejnych cykli inspekcji.

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

Po zaimplementowaniu tego przewodnika każdy zespół rozwiązań w chmurze może przechodzić przez solidną podstawę zarządzania. W tym samym czasie zespół ds. zarządzania chmurą będzie działał w celu ciągłego aktualizowania zasad korporacyjnych i dyscyplin nadzoru.

Dwa zespoły będą używać wskaźników tolerancji do identyfikowania następnego zestawu ulepszeń niezbędnych do kontynuowania obsługi wdrożenia chmury. W przypadku fikcyjnej firmy w tym przewodniku następnym krokiem jest ulepszenie podstawy zabezpieczeń w celu zapewnienia obsługi przeniesienia chronionych danych do chmury.

> [!div class="nextstepaction"]
> [Ulepszanie dyscypliny linii bazowej zabezpieczeń](./security-baseline-improvement.md)
