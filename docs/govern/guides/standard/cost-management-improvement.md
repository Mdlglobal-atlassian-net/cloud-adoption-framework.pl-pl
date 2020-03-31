---
title: 'Standardowe zarządzanie przedsiębiorstwem: ulepszanie dyscypliny Cost Management'
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o dodawaniu kontroli kosztów do minimalnego produktu, który jest w dobrej kondycji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3d0a4e06a2aaa21f191130b937790408abf16952
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434294"
---
# <a name="standard-enterprise-guide-improve-the-cost-management-discipline"></a>Standardowa Przewodnik po przedsiębiorstwie: ulepszanie dyscypliny Cost Management

Ten artykuł postępuje zgodnie z opisami, dodając kontrolę kosztów do programu ładu MVP.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Wdrożenie wykracza poza wskaźnik tolerancji kosztów zdefiniowany w programie ładu MVP. Jest to dobry efekt, ponieważ odnosi się do migracji z centrum danych "DR". Zwiększenie wydatków uzasadnia teraz wyjustowanie inwestycji w zespół nadzoru chmurowego.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

W poprzedniej fazie tego przykładu wystąpiło wycofanie 100% centrum danych DR. Zespoły deweloperów aplikacji i analizy biznesowej były gotowe do ruchu produkcyjnego.

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- Zespół migracji rozpoczął Migrowanie maszyn wirtualnych z centrum danych produkcyjnych.
- Zespoły deweloperów aplikacji aktywnie wypychanie aplikacji produkcyjnych do chmury za pomocą potoków ciągłej integracji/ciągłego dostarczania. Te aplikacje mogą być w sposób aktywny skalowane z wymaganiami użytkownika.
- Zespół ds. analizy biznesowej udostępnia kilka narzędzi analizy predykcyjnej w chmurze. Woluminy danych zagregowane w chmurze nadal rośnie.
- Wszystkie te przyrosty obsługują zatwierdzone wyniki biznesowe. Jednak koszty zaczęły się Mushroom. Planowane budżety zwiększają się szybciej niż oczekiwano. Dyrektor finansowy potrzebuje ulepszonych metod zarządzania kosztami.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Monitorowanie kosztów i raportowanie należy dodać do rozwiązania w chmurze. Nadal jest to rozliczanie kosztów. Oznacza to, że płatność za usługi Cloud Services nadal pochodzi z zakupów IT. Jednak raportowanie powinno powiązać bezpośrednie koszty operacyjne z funkcjami, które zużywają koszty chmury. Ten model jest określany jako "Pokaż z tyłu" model ewidencjonowania aktywności w chmurze.

Zmiany bieżącego i przyszłego stanu ujawniają nowe zagrożenia, które będą wymagały nowych instrukcji zasad.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Kontrola budżetu:** Istnieje ryzyko związane z tym, że funkcje samoobsługowe spowodują nadmierne i nieoczekiwane koszty na nowej platformie. Procesy nadzoru dotyczące monitorowania kosztów i łagodzenia bieżących zagrożeń związanych z kosztami muszą być stosowane w celu zapewnienia ciągłego wyrównania z planowanym budżetem.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

- Rzeczywiste koszty mogą przekroczyć plan.
- Zmiany warunków firmy. W takim przypadku sytuacje, w których funkcja biznesowa musi korzystać z większej liczby usług w chmurze niż oczekiwano, prowadząc do wydatków na anomalie. Istnieje ryzyko, że dodatkowe wydatki będą uznawane za nadwyżkowe, w przeciwieństwie do niezbędnej korekty planu.
- Systemy mogą być nadmiernie zastrzegane, co powoduje nadwyżkowe wydatki.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika.

- Wszystkie koszty chmury powinny być monitorowane w oparciu o plan co tydzień przez zespół nadzoru. Raportowanie odchyleń między kosztami chmury i planem ma być współużytkowane z liderem IT i finansami. Wszystkie koszty w chmurze i Planowanie aktualizacji powinny być przeglądane z liderem IT i finansami.
- Wszystkie koszty muszą być przydzieleni do funkcji biznesowej w celach związanych z odpowiedzialnością.
- Zasoby w chmurze powinny być stale monitorowane pod kątem możliwości optymalizacji.
- Narzędzia do zarządzania chmurą muszą ograniczać opcje ustalania rozmiaru zasobów do zatwierdzonej listy konfiguracji. Narzędzia muszą mieć pewność, że wszystkie zasoby są wykrywalne i śledzone przez rozwiązanie do monitorowania kosztów.
- Podczas planowania wdrożenia należy udokumentować wszystkie wymagane zasoby w chmurze skojarzone z hostem obciążeń produkcyjnych. Ta dokumentacja pomoże udoskonalać budżety i przygotować dodatkową automatyzację, aby uniemożliwić korzystanie z bardziej kosztownych opcji. W ramach tego procesu należy wziąć pod uwagę różne narzędzia do zliczania oferowane przez dostawcę chmury, takie jak wystąpienia zarezerwowane lub obniżki kosztów licencji.
- Wszyscy właściciele aplikacji muszą brać udział w szkoleniach dotyczących optymalizacji obciążeń w celu lepszego sterowania kosztami chmury.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

W tej części artykułu zostanie zmieniony projekt ładu MVP, który obejmuje nowe zasady platformy Azure i implementację Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

1. Zaimplementuj Azure Cost Management.
    1. Ustanów właściwy zakres dostępu do wyrównania ze wzorcem subskrypcji i dyscypliną spójności zasobów. Przy założeniu, że wyrównanie jest stosowane w przypadku zarządzania MVP, zdefiniowanego w poprzednich artykułach, wymaga dostępu do **zakresu konta rejestracji** dla zespołu nadzoru chmurowego wykonywanego na potrzeby raportowania wysokiego poziomu. Dodatkowe zespoły poza zarządzaniem mogą wymagać dostępu do **zakresu grupy zasobów** .
    1. Ustanów budżet w Azure Cost Management.
    1. Przejrzyj i zapoznaj się z wstępnymi zaleceniami. Proces cykliczny obsługujący raportowanie.
    1. Skonfiguruj i wykonaj raportowanie Azure Cost Management, zarówno początkowych, jak i cyklicznych.
2. Azure Policy aktualizacji
    1. Przeprowadź inspekcję wartości tagowania, grupy zarządzania, subskrypcji i grupy zasobów, aby zidentyfikować wszelkie odchylenia.
    1. Ustanów opcje rozmiaru jednostki SKU, aby ograniczyć wdrożenia do jednostek SKU wymienionych w dokumentacji planowania wdrożenia.

## <a name="conclusion"></a>Podsumowanie

Dodanie tych procesów i zmian do ładu MVP pomaga skorygować wiele zagrożeń związanych z zarządzaniem kosztem. Wspólnie tworzą one widoczność, odpowiedzialność i optymalizacje, które są konieczne do kontrolowania kosztów.

## <a name="next-steps"></a>Następne kroki

Gdy wdrożenie chmury będzie kontynuowane i zapewnia dodatkową wartość biznesową, zagrożenia i potrzeby ładu chmury również zostaną zmienione. W przypadku fikcyjnej firmy w tym przewodniku następny krok polega na tym, że w celu zarządzania wieloma chmurami jest używane to inwestycje ładu.

> [!div class="nextstepaction"]
> [Rozwój wielochmurowy](./multicloud-improvement.md)
