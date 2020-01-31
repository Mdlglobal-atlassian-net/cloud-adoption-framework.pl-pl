---
title: Tworzenie świadomych kosztów organizacji
description: Zapoznaj się z najlepszymi rozwiązaniami dotyczącymi tworzenia organizacji świadomej kosztów.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.openlocfilehash: 42025e9e7459aae8731b6269d6bc5512acde64e4
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76800903"
---
# <a name="build-a-cost-conscious-organization"></a>Tworzenie świadomej organizacji kosztów

Jak opisano w obszarze [motywacje: Dlaczego przenosimy się do chmury?](../strategy/motivations.md), istnieje wiele powodów, dla których firma może przyjąć chmurę. Gdy obniżka kosztów jest podstawowym sterownikiem, ważne jest, aby utworzyć organizację o niskich kosztach.

Zapewnienie obnoszenia kosztów nie jest działaniem jednorazowym. Podobnie jak w przypadku innych tematów wdrażania w chmurze, jest to iteracyjne. Na poniższym diagramie przedstawiono ten proces, aby skoncentrować się na trzech działaniach zależnych: *widoczność*, *odpowiedzialność*i *Optymalizacja*. Procesy te są odtwarzane na makrach i mikropoziomach, które opisano szczegółowo w tym artykule.

![y ekonomiczny proces](../_images/ready/cost-optimization-process.png)
*rysunek 1 — Zarys organizacji świadomej kosztów.*

## <a name="general-cost-conscious-processes"></a>Ogólne procesy świadome kosztów

- **Widoczność:** Aby organizacja mogła mieć świadomość kosztów, potrzebuje wglądu w te koszty. Widoczność w niedrogiej organizacji wymaga spójnej sprawozdawczości dla zespołów przyjmujących chmurę, zespołów, którzy zarządzają budżetami i zespoły zarządzania, którzy są odpowiedzialni za koszty. Widoczność ta jest realizowana przez ustanowienie:
  - Właściwy zakres raportowania.
  - Właściwa organizacja zasobów (grupy zarządzania, grupy zasobów, subskrypcje).
  - Wyczyść strategie tagowania.
  - Właściwa kontrola dostępu (RBAC).

- **Odpowiedzialność:** Odpowiedzialność jest ważna jako widoczność. Odpowiedzialność zaczyna się od wyraźnych budżetów na potrzeby wysiłków. Budżety powinny być dobrze ustanowione, jasno przekazane i oparte na realistycznych oczekiwaniach. Odpowiedzialność wymaga iteracyjnego procesu i wzrostu sposób myślenia na odpowiedni poziom odpowiedzialności.

- **Optymalizacja:** Optymalizacja to akcja, która tworzy obniżki kosztów. Podczas optymalizacji alokacje zasobów są modyfikowane w celu zmniejszenia kosztów obsługi różnych obciążeń. Ten proces wymaga iteracji i eksperymentowania. Każde zmniejszenie kosztów zmniejsza wydajność. Znalezienie odpowiedniej równowagi między kontrolą kosztów a oczekiwaniami użytkowników końcowych wymaga wprowadzenia danych przez wiele stron.

W poniższych sekcjach opisano role, które *zespół strategii chmury*, *zespół ds. rozwoju chmury,* *zespół nadzoru chmurowego*i *centrum w chmurze doskonałości* (CCoE) odgrywają w opracowaniu kosztownej organizacji.

## <a name="cloud-strategy-team"></a>Zespół strategii chmury

Tworzenie przytomności kosztów do działań związanych z wdrażaniem w chmurze zaczyna się na poziomie lidera. Aby obowiązywać w długim okresie, [zespół strategii chmury](./cloud-strategy.md) powinien obejmować członka zespołu finansowego. Jeśli Struktura finansowa zawiera dla menedżerów firmy konto, które są przeznaczone dla kosztów rozwiązań, należy zazapraszać je również do przyłączenia do zespołu. Oprócz podstawowych działań, które są zwykle przypisane do zespołu strategii chmurowej, wszyscy członkowie zespołu strategii chmury powinni również być odpowiedzialni za:

- **Widoczność:** Zespół ds. strategii chmury i [zarządzania chmurą](./cloud-governance.md) musi znać rzeczywiste koszty związane z wdrażaniem w chmurze. Mając na uwadze widok tego zespołu, powinien mieć dostęp do wielu zakresów kosztów, aby analizować decyzje dotyczące wydatków. Zazwyczaj dyrektor musi widzieć łączny koszt wszystkich wydatków w chmurze. Jednak jako aktywni członkowie zespołu ds. strategii chmury powinni również mieć możliwość wyświetlania kosztów na jednostkę biznesową lub za jednostkę rozliczeniową w celu weryfikacji przewidywanych kosztów, obciążenia zwrotnego lub innych [modeli ewidencjonowania aktywności w chmurze](../strategy/cloud-accounting.md).

- **Odpowiedzialność:** Należy ustalić budżety między strategią chmury, [zarządzaniem chmurą](./cloud-governance.md)i zespołami [wdrażania chmury](./cloud-adoption.md) w oparciu o oczekiwane działania związane z przyjmowaniem. Gdy wystąpią odchylenia od budżetu, zespół strategii chmur i zespół nadzoru chmury muszą szybko określić najlepszy sposób działania, aby skorygować odchylenia.

- **Optymalizacja:** W trakcie optymalizacji, zespół strategii chmury może reprezentować inwestycję i wartość zwrotną określonych obciążeń. Jeśli obciążenie ma wartość strategiczną lub wpływ na działalność finansową, należy uważnie monitorować zadania optymalizacji kosztów. W przypadku braku strategicznego wpływu na organizację i braku kosztu związanego z niską wydajnością obciążenia zespół strategii chmury może zatwierdzać przepełnienie. Aby zapewnić te decyzje, zespół musi mieć możliwość wyświetlania kosztów dla zakresu poszczególnych projektów.

## <a name="cloud-adoption-team"></a>Zespół ds. wdrażania chmury

[Zespół ds. wdrażania w chmurze](./cloud-adoption.md) jest w centrum wszystkich działań związanych z wdrażaniem. W związku z tym są one pierwszym wierszem obrony przed przetrwaniem. Ten zespół ma aktywną rolę we wszystkich trzech fazach kosztów.

- **Propagowan**

  - **Świadomość:** Ważne jest, aby zespół ds. wdrażania w chmurze miał wgląd w cele oszczędności kosztów. Po prostu, że nakłady na wdrażanie w chmurze będą pomocne w obniżeniu kosztów. *Konkretna* widoczność jest ważna. Na przykład jeśli celem jest zmniejszenie kosztu posiadania centrum danych o 3% lub rocznych kosztach operacyjnych o 7%, należy ujawnić te cele wczesne i jasno.
  - Dane **telemetryczne:** Ten zespół wymaga wglądu w wpływ ich decyzji. W trakcie migracji lub innowacji, ich decyzje mają bezpośredni wpływ na koszty i wydajność. Zespół musi zrównoważyć te dwa konkurujące czynniki. Monitorowanie wydajności i monitorowanie kosztów, które są objęte zakresem aktywnych projektów zespołu, są ważne, aby zapewnić konieczność widoczności.

- **Odpowiedzialność:** Zespół ds. wdrażania w chmurze musi mieć świadomość wszelkich wstępnie ustawionych budżetów, które są powiązane z ich przyjęciem. Gdy rzeczywiste koszty nie są wyrównane z budżetem, istnieje możliwość utworzenia odpowiedzialności. Odpowiedzialności nie są równe karaniu zespołu adopcji za przekroczenie budżetu, ponieważ nadwyżka budżetowa może wynikać z niezbędnych decyzji dotyczących wydajności. Zamiast tego, odpowiedzialność oznacza, że zespół poinformuje o celach i o tym, jak ich decyzje wpływają na te cele. Ponadto odpowiedzialność obejmuje podanie okna dialogowego, w którym zespół może komunikować się z decyzjami, które doprowadziły do przetworzenia. Jeśli te decyzje są nieprawidłowo dopasowane do celów projektu, ten nakład pracy zapewnia dobrą szansę partnerowi z zespołem ds. strategii chmury w celu podejmowania lepszych decyzji.

- **Optymalizacja:** Jest to proces równoważenia postępu, ponieważ Optymalizacja zasobów może zmniejszyć wydajność obsługiwanych przez nich obciążeń. Czasami przewidywane lub budżetowane oszczędności nie mogą być zrealizowane dla obciążenia, ponieważ obciążenie nie jest odpowiednio wykonywane w przypadku zasobów budżetowych. W takich przypadkach zespół wdrażania chmury musi podejmować decyzje i zgłaszać zmiany do zespołu strategii chmury i zespołu nadzoru chmurowego, aby umożliwić skorygowanie budżetów lub decyzji dotyczących optymalizacji.

## <a name="cloud-governance-team"></a>Zespół nadzorujący chmury

Ogólnie rzecz biorąc, zespół zarządzający [chmurą](./cloud-governance.md) jest odpowiedzialny za zarządzanie kosztami w całym wysiłku związanym z wdrażaniem w chmurze. Zgodnie z opisem w temacie [Cost Management dyscyplin](../govern/cost-management/index.md) of the Cloud Reline propozycja metodologii, zarządzanie kosztami jest pierwszym z pięciu dyscyplin zarządzania chmurą. Te artykuły przedstawiają szereg bardziej szczegółowych obowiązków dla zespołu nadzoru chmurowego.

Ten nakład pracy koncentruje się na następujących działaniach, które są związane z programowaniem świadomej organizacji:

- **Widoczność:** Zespół ds. nadzoru chmurowego działa jako element równorzędny zespołu strategii chmury w celu planowania budżetów wdrażania w chmurze. Te dwa zespoły współpracują ze sobą, aby regularnie przeglądać rzeczywiste wydatki. Zespół ds. nadzoru w chmurze jest odpowiedzialny za zapewnienie spójnego, niezawodnego raportowania kosztów i telemetrii wydajności.

- **Odpowiedzialność:** Po wystąpieniu odchyleń budżetowych zespół strategii chmur i zespół nadzorujący chmur muszą szybko określić najlepszy sposób działania, aby skorygować odchylenia. Ogólnie rzecz biorąc, zespół ds. zarządzania chmurą będzie podejmować decyzje dotyczące tych decyzji. Czasami akcja może być prostym przeszkoleniem dla [zespołu](./cloud-adoption.md), którego to dotyczy. Zespół ds. ładu w chmurze może również pomóc zoptymalizować wdrożone zasoby, zmienić opcje odliczania, a nawet zaimplementować zautomatyzowane opcje kontroli kosztów, takie jak blokowanie wdrożenia nieplanowanych zasobów.

- **Optymalizacja:** Po migracji lub utworzeniu zasobów w chmurze można zastosować narzędzia do monitorowania do oceny wydajności i użycia tych zasobów. Prawidłowe dane monitorowania i wydajności mogą identyfikować zasoby, które powinny zostać zoptymalizowane. Zespół ds. zarządzania chmurą jest odpowiedzialny za zapewnienie, że narzędzia monitorowania i raportowania kosztów są stale wdrażane. Mogą również pomóc zespołom ds. przyjęcia identyfikować możliwości optymalizacji w oparciu o wydajność i telemetrię kosztów.

## <a name="cloud-center-of-excellence"></a>Centrum doskonałości chmury

Chociaż nie jest to zwykle odpowiedzialne za zarządzanie kosztami, CCoE może mieć znaczący wpływ na organizacje świadome kosztów. Wiele podstawowych decyzji IT wpływa na koszty w skali. Gdy CCoE jest częścią, koszty można zmniejszyć w przypadku wielu wysiłków związanych z wdrażaniem w chmurze.

- **Widoczność:** Wszystkie grupy zarządzania lub grupy zasobów, które są elementami głównych zasobów IT, powinny być widoczne dla zespołu CCoE. Zespół może używać tych danych do optymalizowania możliwości farmy.

- **Odpowiedzialność:** Chociaż zwykle nie jest to możliwe w przypadku kosztu, CCoE może zapewnić sobie możliwość tworzenia powtarzalnych rozwiązań, które minimalizują koszt i maksymalizują wydajność.

- **Optymalizacja:** Mając na CCoE widoczność wielu wdrożeń, zespół jest w idealnym miejscu, aby zasugerować wskazówki dotyczące optymalizacji i pomóc w przyjęciu zespołów lepiej dostroić zasoby.

## <a name="next-steps"></a>Następne kroki

Zastosowanie tych obowiązków na każdym poziomie firmy pomaga na zwiększeniu ekonomicznej organizacji. Aby rozpocząć postępowanie z tymi wskazówkami, zapoznaj się z [wprowadzeniem do gotowości organizacyjnej](./index.md) w celu ułatwienia identyfikacji właściwych struktur zespołu.

> [!div class="nextstepaction"]
> [Zidentyfikuj właściwe struktury zespołu](./index.md)
