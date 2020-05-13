---
title: Programowanie oparte na testach (TDD) dla stref wypełniania na platformie Azure.
description: Programowanie oparte na testach (TDD) dla stref wypełniania na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: b4edc0f0e485c040045bc8c1b7bce6c91f3d13f9
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83221913"
---
# <a name="test-driven-development-tdd-for-landing-zones-in-azure"></a>Programowanie oparte na testach (TDD) dla stref wypełniania na platformie Azure

Zgodnie z opisem w poprzednim artykule na [potrzeby projektowania na podstawie testów dla stref](./test-driven-development.md)wypełniania, cykle TDD zaczynają się testem, który sprawdza kryteria akceptacji określonej funkcji wymaganej do dostarczenia planu wdrożenia chmury. Aby sprawdzić, czy kryteria akceptacji zostały spełnione, można rozszerzyć lub Refaktoryzacja strefy docelowej. W tym artykule opisano natywne w chmurze łańcucha narzędzi na platformie Azure w celu zautomatyzowania cykli programistycznych opartych na testach.

## <a name="azure-tools-to-support-landing-zone-tdd-cycles"></a>Narzędzia platformy Azure obsługujące cykle dla strefy ładunkowej

![Narzędzia programistyczne oparte na testach na platformie Azure](../../_images/ready/azure-tdd-tools.png)

Łańcucha narzędzi i usługi zarządzania natywnego platformy Azure można łatwo zintegrować z programowaniem opartym na testach w celu utworzenia stref wyładunkowych. Każdy z tych narzędzi służy do określonego celu, co ułatwia tworzenie, testowanie i wdrażanie strefy docelowej w postaci wyrównania z cyklami TDD.

## <a name="microsoft-provided-test-and-deployment-templates-to-accelerate-tdd"></a>Szablony testów i wdrożeń udostępniane przez firmę Microsoft w celu przyspieszenia TDD

Poniższe przykłady są udostępniane przez firmę Microsoft do celów zarządzania. Jednak każdy z nich może być używany jako test lub seria testów w cyklu programistycznym opartym na testach dla stref wypełniania. Więcej informacji na temat każdego narzędzia w poniższej sekcji.

- Plany platformy Azure udostępniają różne [przykłady planów](https://docs.microsoft.com/azure/governance/blueprints/samples), w tym zasady testowania i szablonów dla wdrożenia. Te przykłady strategii mogą przyspieszyć rozwój, wdrażanie i testowanie działań w cyklach TDD.
- Azure Policy obejmuje również [wbudowane inicjatywy zasad](https://docs.microsoft.com/azure/governance/policy/samples/built-in-initiatives), które mogą służyć do testowania i wymuszania pełnej definicji gotowej dla strefy docelowej. Azure Policy obejmuje [wbudowane definicje zasad](https://docs.microsoft.com/azure/governance/policy/samples/built-in-policies) , które mogą spełniać poszczególne kryteria akceptacji w ramach definicji gotowe.
- Program Azure Graph zawiera zaawansowane [przykłady zapytań](https://docs.microsoft.com/azure/governance/resource-graph/samples/advanced), które mogą służyć do zrozumienia, jak obciążenia są wdrażane w ramach strefy docelowej na potrzeby scenariuszy testowania zaawansowanego.
- [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/resources/templates) udostępniają szablony kodu źródłowego, aby pomóc w przyspieszaniu wdrażania stref i obciążeń.

Każdy z powyższych przykładów może służyć jako narzędzia przyspieszające cykle TDD. Te przykłady są uruchamiane w narzędziach ładu w poniższych sekcjach, które umożliwiają zespołom platformy w chmurze Tworzenie własnego kodu źródłowego i testów.

## <a name="azure-governance-tools-that-can-accelerate-tdd-cycles"></a>Narzędzia ładu platformy Azure, które mogą przyspieszyć cykle usługi TDD

[Azure Policy](https://docs.microsoft.com/azure/governance/policy): gdy wdrożenia lub próby wdrożenia odbiegają od zasad ładu, Azure Policy może zapewnić automatyczne wykrywanie, ochronę i rozwiązywanie problemów. Ale Azure Policy również zapewnia podstawowy mechanizm testowania kryteriów akceptacji w "definicji gotowe". W cyklu TDD można utworzyć definicję zasad w celu przetestowania pojedynczych kryteriów akceptacji. Analogicznie, wszystkie kryteria akceptacji można dodać do inicjatywy Policy przypisanej do całej subskrypcji. Takie podejście zapewnia mechanizm "Red Tests" Przed zmodyfikowaniem strefy docelowej. Gdy strefa docelowa spełnia definicję gotowe, może być użyta do wymuszenia kryteriów testowych, aby uniknąć zmian w kodzie, które spowodują, że test zakończy się niepowodzeniem w przyszłych wydaniach.

[Plany platformy Azure](https://docs.microsoft.com/azure/governance/blueprints): Azure Blueprint zasad grupy i innych narzędzi wdrażania do powtarzalnego pakietu, który można przypisać do wielu stref wyładunkowej. Plany są przydatne, gdy wiele wysiłków podejmuje wspólne definicje gotowe, które warto zaktualizować w czasie. Może także ułatwić wdrożenie w trakcie kolejnych działań w celu rozwinięcia i refaktoryzacji stref wyładunkowych.

[Wykres zasobów platformy Azure](https://docs.microsoft.com/azure/governance/resource-graph): Wykres zasobów zawiera język zapytań służący do tworzenia testów opartych na danych, opartych na informacjach dotyczących zasobów wdrożonych w ramach strefy wyładunkowej. W dalszej części planu wdrażania to narzędzie może również definiować złożone testy na podstawie interakcji między zasobami obciążeń a podstawowym środowiskiem chmury.

[Szablony Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview): te szablony stanowią podstawowy kod źródłowy dla każdego środowiska wdrożonego na platformie Azure. W przypadku korzystania z narzędzi innych firm, takich jak Terraform, do opracowania kodu źródłowego, który wdraża strefę wyładunkowe, narzędzia te generują własne szablony. Te szablony są następnie przesyłane do Azure Resource Manager.

[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview): Menedżer zasobów zapewnia spójną platformę do kompilowania i wdrażania funkcji. Na tej platformie są zarządzane wdrożenia strefy docelowej z kodu źródłowego.

## <a name="next-steps"></a>Następne kroki

Aby rozpocząć refaktoryzację pierwszej strefy docelowej, Oceń [podstawowe zagadnienia dotyczące strefy docelowej](./basic-considerations.md).

> [!div class="nextstepaction"]
> [Zagadnienia dotyczące strefy docelowej w warstwie Podstawowa](./basic-considerations.md)
