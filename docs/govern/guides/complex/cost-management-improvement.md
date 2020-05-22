---
title: 'Złożone przedsięwzięcia korporacyjne: ulepszanie dyscypliny Cost Management'
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o dodawaniu kontroli kosztów do minimalnego produktu, który jest w dobrej kondycji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6ea51d75a2c75fd8e75ade42eb3c9fe15def67b4
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83754954"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-cost-management-discipline"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: ulepszanie dyscypliny Cost Management

Ten artykuł postępuje zgodnie z opisami, dodając kontrolki kosztów do nadzoru nad produktem minimalnym (MVP).

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Wdrożenie wykracza poza wskaźnik tolerancji zdefiniowany w programie ładu MVP. Zwiększenie nakładu wydatków uzasadnia teraz odinwestycję czasu od zespołu nadzoru w chmurze w celu monitorowania i kontrolowania wzorców wydatków.

Jako czysty sterownik innowacji nie jest już widoczny głównie jako centrum kosztów. Ponieważ organizacja IT dostarcza więcej wartości, CIO i dyrektor finansowy zgadzają się, że czas jest w stanie przesunąć rolę, jaką odgrywa w firmie. Od innych zmian dyrektor finansowy chce przetestować bezpośrednie podejście do księgowania w chmurze dla kanadyjskiej gałęzi jednej z jednostek biznesowych. Jedno z dwóch wycofanych centrów danych dotyczyło wyłącznie zasobów hostowanych przez kanadyjskie jednostki biznesowe. W tym modelu w kanadyjskiej oddzieleniu jednostka biznesowa zostanie naliczona bezpośrednio za wydatki operacyjne związane z zasobami hostowanymi. Ten model pozwala skupić się na niższym stopniu na zarządzaniu wydatkami innej osoby i nie tylko przy tworzeniu wartości. Zanim to przejście będzie możliwe, należy rozpocząć wykonywanie narzędzi do zarządzania kosztami.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

W poprzedniej fazie tego przykładu zespół IT aktywnie przenosi obciążenia produkcyjne z chronionymi danymi na platformę Azure.

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- zasoby 5 000 zostały usunięte z dwóch centrów danych oflagowanych do wycofania. Zakup i zabezpieczenia IT są teraz anulowania aprowizacji pozostałych zasobów fizycznych.
- Zespoły deweloperów aplikacji wprowadziły potoki ciągłej integracji/ciągłego wdrażania, aby wdrożyć niektóre aplikacje natywne w chmurze, znacząco wpływając na środowiska klienta.
- Zespół analizy biznesowej utworzył procesy agregacji, nadzoru, wglądu i przewidywania, które mają materialne korzyści dla operacji biznesowych. Przewidywania te umożliwiają teraz umożliwienie nowych produktów i usług.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Monitorowanie kosztów i raportowanie należy dodać do rozwiązania w chmurze. Raportowanie powinno wiązać się z bezpośrednimi kosztami operacyjnymi dla funkcji, które zużywają koszty chmury. Dodatkowe raporty powinny umożliwiać działowi IT monitorowanie wydatków i zapewnienie wytycznych dotyczących zarządzania kosztami. W przypadku gałęzi kanadyjskiej dział zostanie rozliczony bezpośrednio.

## <a name="changes-in-risk"></a>Zmiany ryzyka

**Kontrola budżetu:** Istnieje ryzyko związane z tym, że funkcje samoobsługowe spowodują nadmierne i nieoczekiwane koszty na nowej platformie. Procesy nadzoru dotyczące monitorowania kosztów i łagodzenia bieżących zagrożeń związanych z kosztami muszą być stosowane w celu zapewnienia ciągłego wyrównania z planowanym budżetem.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

- Istnieje ryzyko faktycznego kosztu przekroczenia planu.
- Zmiany warunków firmy. W takim przypadku sytuacje, w których funkcja biznesowa musi korzystać z większej liczby usług w chmurze niż oczekiwano, prowadząc do wydatków na anomalie. Istnieje ryzyko, że te dodatkowe koszty będą uznawane za nadmiarowe, w przeciwieństwie do wymaganej korekty planu. Jeśli to się powiedzie, eksperyment kanadyjski powinien pomóc w skorygowaniu tego ryzyka.
- Istnieje ryzyko nadmiernej aprowizacji systemów, co powoduje nadwyżkowe wydatki.

## <a name="changes-to-the-policy-statements"></a>Zmiany w instrukcjach zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika.

- Wszystkie koszty chmury powinny być monitorowane w oparciu o plan co tydzień przez zespół ds. zarządzania chmurą. Raportowanie odchyleń między kosztami chmury i planem ma być współużytkowane z liderem IT i finansami. Wszystkie koszty w chmurze i Planowanie aktualizacji powinny być przeglądane z liderem IT i finansami.
- Wszystkie koszty muszą być przydzieleni do funkcji biznesowej w celach związanych z odpowiedzialnością.
- Zasoby w chmurze powinny być stale monitorowane pod kątem możliwości optymalizacji.
- Narzędzia do zarządzania chmurą muszą ograniczać opcje ustalania rozmiaru zasobów do zatwierdzonej listy konfiguracji. Narzędzia muszą mieć pewność, że wszystkie zasoby są wykrywalne i śledzone przez rozwiązanie do monitorowania kosztów.
- Podczas planowania wdrożenia należy udokumentować wszystkie wymagane zasoby w chmurze skojarzone z hostem obciążeń produkcyjnych. Ta dokumentacja pomoże udoskonalać budżety i przygotować dodatkowe narzędzia do automatyzacji, aby uniemożliwić korzystanie z bardziej kosztownych opcji. W ramach tego procesu należy wziąć pod uwagę różne narzędzia do zliczania oferowane przez dostawcę chmury, takie jak wystąpienia zarezerwowane lub obniżki kosztów licencji.
- Wszyscy właściciele aplikacji muszą brać udział w szkoleniach dotyczących optymalizacji obciążeń w celu lepszego sterowania kosztami chmury.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

Ta część artykułu poprawi projekt ładu MVP, aby uwzględnić nowe zasady platformy Azure i implementację Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

1. Wprowadź zmiany w portalu Azure Enterprise, aby obciążyć administratora działu dla kanadyjskiego wdrożenia.
2. Zaimplementuj Azure Cost Management.
    1. Ustal zakres dostępu odpowiedni do dopasowania przy użyciu wzorca subskrypcji i wzorca grupowania zasobów. Przy założeniu, że wyrównanie jest stosowane w przypadku zarządzania MVP, zdefiniowanego w poprzednich artykułach, wymaga to dostępu do **zakresu kont rejestracji** dla zespołu nadzoru chmurowego wykonywanego na potrzeby raportowania wysokiego poziomu. Dodatkowe zespoły poza nadzorem, takie jak zespół ds. zakupów, będą wymagały dostępu do **zakresu grupy zasobów** .
    2. Ustanów budżet w Azure Cost Management.
    3. Przejrzyj i zapoznaj się z wstępnymi zaleceniami. Zaleca się wykonanie cyklicznego procesu do obsługi procesu raportowania.
    4. Skonfiguruj i wykonaj raportowanie Azure Cost Management, zarówno początkowych, jak i cyklicznych.
3. Aktualizacja Azure Policy.
    1. Tagowanie inspekcji, grupy zarządzania, subskrypcji i wartości grupy zasobów, aby zidentyfikować wszelkie odchylenia.
    2. Ustanów opcje rozmiaru jednostki SKU, aby ograniczyć wdrożenia do jednostek SKU wymienionych w dokumentacji planowania wdrożenia.

## <a name="conclusion"></a>Podsumowanie

Dodanie powyższych procesów i zmian do ładu MVP pomaga skorygować wiele zagrożeń związanych z zarządzaniem kosztami. Wspólnie tworzą one widoczność, odpowiedzialność i optymalizacje, które są konieczne do kontrolowania kosztów.

## <a name="next-steps"></a>Następne kroki

Gdy wdrożenie chmury zostanie powiększone i oferuje dodatkową wartość biznesową, zagrożenia i potrzeby ładu chmury również zostaną zmienione. W przypadku tej fikcyjnej firmy następny krok polega na tym, że inwestycje ładu są używane do zarządzania wieloma chmurami.

> [!div class="nextstepaction"]
> [Poprawa chmury](./multicloud-improvement.md)
