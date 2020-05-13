---
title: Cost Management przykładowe instrukcje zasad
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby uzyskać przykładowe instrukcje zasad Cost Management, które ułatwią Szkicowanie instrukcji zasad.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d686d50b98cbdef31c48d27f20d1c66f942e0818
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83220502"
---
# <a name="cost-management-sample-policy-statements"></a>Cost Management przykładowe instrukcje zasad

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te instrukcje powinny dostarczyć zwięzłe podsumowanie zagrożeń i plany postępowania z nimi. Każda definicja instrukcji powinna zawierać następujące informacje:

- **Ryzyko biznesowe:** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad:** Jasne wyjaśnienie wymagań zasad.
- **Opcje projektowania:** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki, które mogą być używane przez zespoły IT i deweloperów podczas implementowania zasad.

Poniższe przykładowe instrukcje dotyczące zasad dotyczą typowych zagrożeń związanych z kosztami firmy. Te instrukcje są przykładami, które można przywołać podczas sporządzania projektów instrukcji zasad w celu rozwiązania potrzeb organizacji. Te przykłady nie są zalecane, a istnieje kilka opcji zasad związanych z poszczególnymi zagrożeniami. Ścisła współpraca z firmowymi i zespołami IT w celu zidentyfikowania najlepszych zasad dla unikatowego zestawu zagrożeń.

## <a name="future-proofing"></a>Weryfikacja w przyszłości

**Ryzyko biznesowe:** Bieżące kryteria, które nie uzasadniają inwestycji w Cost Management dyscypliny zespołu zarządzającego. Przewiduje się jednak takie inwestycje w przyszłości.

**Instrukcja zasad:** Należy skojarzyć wszystkie zasoby wdrożone w chmurze z jednostką rozliczeniową oraz aplikacją lub obciążeniem. Te zasady zapewniają, że dyscyplina Cost Management będzie obowiązywać.

**Opcje projektowania:** Aby uzyskać informacje na temat tworzenia platformy Future-The-The-test Foundation, zobacz dyskusje związane z tworzeniem programu ładu MVP w [przewodnikach projektowych](../guides/index.md) z możliwością podejmowania działań, które znajdują się w wytycznych dotyczących struktury wdrożenia chmury.

## <a name="budget-overruns"></a>Przekroczenia budżetu

**Ryzyko biznesowe:** Wdrażanie samoobsługowe polega na ryzyku przespędzania.

**Instrukcja zasad:** Wszystkie wdrożenia w chmurze muszą być przydzieleni do jednostki rozliczeniowej z zatwierdzonym budżetem i mechanizmem limitów budżetowych.

**Opcje projektowania:** Na platformie Azure budżet można kontrolować za pomocą [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/manage-budgets).

## <a name="underutilization"></a>Niepożytkowanie

**Ryzyko biznesowe:** Firma ma przedpłatę za usługi w chmurze lub złożyła roczne zobowiązanie do wypoświęcania określonej kwoty. Istnieje ryzyko, że nie będzie można użyć uzgodnionej kwoty, co spowodowało utratę inwestycji.

**Instrukcja zasad:** Każda jednostka rozliczeniowa z przydzielonym budżetem w chmurze będzie spotykać się rocznie w celu ustawienia budżetów, co kwartał w celu dostosowania budżetów i comiesięcznego przydzielenia czasu na przegląd planowanych i rzeczywistych wydatków. Należy omówić wszystkie odchylenia większe niż 20% od lidera jednostki rozliczeniowej miesięcznie. Do celów śledzenia należy przypisać wszystkie zasoby do jednostki rozliczeniowej.

**Opcje projektowania:**

- Na platformie Azure planowane i rzeczywiste wydatki mogą być zarządzane za pośrednictwem [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis).
- Istnieje kilka opcji grupowania zasobów według jednostki rozliczeniowej. Na platformie Azure [model spójności zasobów](../../decision-guides/resource-consistency/index.md) powinien być wybierany razem z zespołem nadzoru i stosowany do wszystkich zasobów.

## <a name="overprovisioned-assets"></a>Zasoby o nadmiernej aprowizacji

**Ryzyko biznesowe:** W tradycyjnych lokalnych centrach danych jest powszechną metodą wdrażania zasobów z dodatkowym planowaniem wydajności na potrzeby wzrostu w odległej przyszłości. Chmura może przeskalować się szybciej niż w przypadku tradycyjnego sprzętu. Opłaty za zasoby w chmurze są również naliczane na podstawie wydajności technicznej. Istnieje ryzyko dla starej praktycznej instalacji sztucznie niepłaskich wydatków na chmurę.

**Instrukcja zasad:** Każdy zasób wdrożony w chmurze musi być zarejestrowany w programie, który może monitorować wykorzystanie i zgłaszać pojemność przekraczającą 50% wykorzystania. Wszystkie zasoby wdrożone w chmurze muszą być zgrupowane lub otagowane w sposób logiczny, dlatego członkowie zespołu nadzoru mogą angażować właściciela obciążenia w odniesieniu do dowolnej optymalizacji zasobów nadmiernej aprowizacji.

**Opcje projektowania:**

- Na platformie Azure [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) mogą zapewnić zalecenia dotyczące optymalizacji.
- Istnieje kilka opcji grupowania zasobów według jednostki rozliczeniowej. Na platformie Azure [model spójności zasobów](../../decision-guides/resource-consistency/index.md) powinien być wybierany razem z zespołem nadzoru i stosowany do wszystkich zasobów.

## <a name="overoptimization"></a>Optymalizacja

**Ryzyko biznesowe:** Efektywne zarządzanie kosztami umożliwia tworzenie nowych zagrożeń. Optymalizacja wydatków jest odwrotna do wydajności systemu. W przypadku obniżenia kosztów istnieje ryzyko pogorszenia wydatków i produkowanie nieprawidłowych środowisk użytkowników.

**Instrukcja zasad:** Wszelkie zasoby, które bezpośrednio mają wpływ na środowisko klienta, muszą być identyfikowane za poorednictwem grupowania lub tagowania. Przed optymalizacją dowolnego elementu zawartości, który ma wpływ na środowisko klienta, zespół ds. zarządzania chmurą musi dostosować optymalizację w oparciu o co najmniej 90 dni. Udokumentowanie wszelkich serii sezonowych lub opartych na zdarzeniach, które są brane pod uwagę podczas optymalizowania zasobów.

**Opcje projektowania:**

- Na platformie Azure [funkcje usługi insights Azure monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-performance) mogą pomóc w analizie wykorzystania systemu.
- Istnieje kilka opcji grupowania i tagowania zasobów na podstawie ról. Na platformie Azure należy wybrać [model spójności zasobów](../../decision-guides/resource-consistency/index.md) w połączeniu z zespołem nadzoru i zastosować go do wszystkich zasobów.

## <a name="next-steps"></a>Następne kroki

Skorzystaj z przykładów przedstawionych w tym artykule jako punktu wyjścia do opracowania zasad, które wiążą się z konkretnymi zagrożeniami biznesowymi, które są dostosowane do planów wdrażania w chmurze.

Aby rozpocząć tworzenie własnych niestandardowych instrukcji zasad Cost Management, Pobierz [szablon zasad Cost Management](./template.md).

Aby przyspieszyć wdrażanie tego dyscypliny, wybierz [Przewodnik dotyczący ładu](../guides/index.md) z możliwością działania, który najlepiej odpowiada Twojemu środowisku. Następnie zmodyfikuj projekt, aby uwzględnić określone decyzje dotyczące zasad firmowych.

Opracowywanie zagrożeń i odporności, ustanawianie procesu w celu zarządzania zasadami Cost Management zasad i ich przekazywania.

> [!div class="nextstepaction"]
> [Ustanawianie procesów zgodności z zasadami](./compliance-processes.md)
