---
title: Skalowanie za pomocą wielu subskrypcji platformy Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, jak skalować za pomocą wielu subskrypcji platformy Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: fbfe025b5e324ec685fcec3001cc8705ac001beb
ms.sourcegitcommit: 57390e3a6f7cd7a507ddd1906e866455fa998d84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2019
ms.locfileid: "73243268"
---
# <a name="scaling-with-multiple-azure-subscriptions"></a>Skalowanie za pomocą wielu subskrypcji platformy Azure

Organizacje często potrzebują więcej niż jednej subskrypcji platformy Azure w wyniku limitów zasobów i innych zagadnień związanych z zarządzaniem. Ważne jest opracowanie strategii skalowania subskrypcji.

## <a name="production-and-nonproduction-workloads"></a>Obciążenia produkcyjne i nieprodukcyjne

Podczas wdrażania pierwszego obciążenia produkcyjnego na platformie Azure należy zacząć od dwóch subskrypcji: jednej dla środowiska produkcyjnego i jednego dla środowiska nieprodukcyjnego (deweloperskiego/testowego).

![Podstawowy model subskrypcji pokazujący klucze obok pola "produkcja" i "nieprodukcja"](../../_images/ready/basic-subscription-model.png)

Zalecamy zastosowanie tego podejścia z kilku powodów:

- Platforma Azure ma specjalne oferty subskrypcji dla obciążeń deweloperskich/testowych. Oferty te obejmują obniżone stawki za usługi platformy Azure i licencjonowanie.
- Środowiska produkcyjne i nieprodukcyjne będą prawdopodobnie mieć różne zestawy zasad platformy Azure. Użycie oddzielnych subskrypcji ułatwia stosowanie odrębnych zestawów zasad na poziomie subskrypcji.
- Możesz potrzebować niektórych typów zasobów platformy Azure w ramach subskrypcji deweloperskiej/testowej do testowania. Korzystając z oddzielnej subskrypcji, można używać tych typów zasobów bez udostępniania ich w środowisku produkcyjnym.
- Subskrypcji deweloperskich/testowych możesz używać jako izolowanych środowisk piaskownicy. Takie piaskownice umożliwiają administratorom i deweloperom szybkie tworzenie i usuwanie całych zestawów zasobów platformy Azure. Taka izolacja może również pomóc w rozwiązywaniu problemów z ochroną danych i zabezpieczeniami.
- Progi akceptowalnych kosztów mogą się różnić dla subskrypcji produkcyjnej i deweloperskiej/testowej.

## <a name="other-reasons-for-multiple-subscriptions"></a>Dlaczego warto rozważyć zakup wielu subskrypcji

Inne sytuacje mogą wymagać użycia dodatkowych subskrypcji. Rozszerzając swój majątek w chmurze, należy wziąć pod uwagę następujące kwestie.

- Subskrypcje mają różne limity dla różnych typów zasobów. Na przykład liczba sieci wirtualnych w subskrypcji jest ograniczona. Gdy subskrypcja wkrótce osiągnie limit, należy utworzyć kolejną subskrypcję i umieścić w niej nowe zasoby.

  Aby uzyskać więcej informacji, zobacz [Limity, przydziały i ograniczenia usług i subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

- Każda subskrypcja może zaimplementować własne zasady dla typów zasobów do wdrożenia i obsługiwanych regionów.

- Subskrypcje w regionach chmury publicznej i regionach w chmurze suwerennych lub rządowych mają różne ograniczenia. Wynikają one często z różnych poziomów klasyfikacji danych w poszczególnych środowiskach.

- W przypadku całkowitej segregacji różnych grup użytkowników z powodów związanych z zabezpieczeniami lub zgodnością mogą być wymagane oddzielne subskrypcje. Na przykład Krajowa organizacja rządowa może potrzebować ograniczyć dostęp do subskrypcji tylko dla obywateli.

- Różne subskrypcje mogą mieć różne typy ofert z indywidualnymi warunkami i korzyściami.

- Między właścicielami subskrypcji i właścicielem wdrażanych zasobów mogą istnieć problemy związane z zaufaniem. Korzystanie z innej subskrypcji z inną własność może jednak wyeliminować te problemy, ale również należy wziąć pod uwagę problemy dotyczące sieci i ochrony danych, które zostaną nawiązane w tym wdrożeniu.

- Rygorystyczne kontrole finansowe lub geopolityczne mogą wymagać oddzielnych ustaleń finansowych dla określonych subskrypcji. Te problemy mogą obejmować zagadnienia dotyczące suwerenności danych, firm z wieloma jednostkami zależnymi, a także oddzielnego księgowania i rozliczeń za jednostki biznesowe w różnych krajach i różnych walutach.

- Zasoby platformy Azure utworzone przy użyciu klasycznego modelu wdrażania należy wyizolować w oddzielnej subskrypcji. Zabezpieczenia zasobów klasycznych różnią się od zabezpieczeń zasobów wdrażanych za pomocą narzędzia Azure Resource Manager. Nie można zastosować zasad platformy Azure do zasobów klasycznych.

- Administratorzy usługi korzystający z zasobów klasycznych mają takie same uprawnienia jak właściciele subskrypcji z kontrolą dostępu opartą na rolach. Trudno jest wystarczająco ograniczyć dostęp tych administratorów usługi w subskrypcji, w której zasoby klasyczne są używane w połączeniu z zasobami narzędzia Resource Manager.

Można również utworzyć dodatkowe subskrypcje z innych powodów biznesowych lub technicznych specyficznych dla organizacji. Mogą występować dodatkowe koszty związane z ruchem przychodzącym i wychodzącym danych przesyłanych między subskrypcjami.

Wiele typów zasobów można przenosić między subskrypcjami lub używać zautomatyzowanych wdrożeń w celu migracji zasobów do innej subskrypcji. Aby uzyskać więcej informacji, zobacz [Przenoszenie zasobów platformy Azure do innej grupy zasobów lub subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="managing-multiple-subscriptions"></a>Zarządzanie wieloma subskrypcjami

Jeśli masz tylko kilka subskrypcji, niezależne zarządzanie nimi jest stosunkowo proste. Jeśli jednak masz wiele subskrypcji, rozważ utworzenie hierarchii grup zarządzania, aby uprościć zarządzanie subskrypcjami i zasobami.

Grupy zarządzania umożliwiają wydajne zarządzanie dostępem, zasadami i zgodnością z subskrypcjami organizacji. Każda grupa zarządzania jest kontenerem dla co najmniej jednej subskrypcji.

Grupy zarządzania są uporządkowane w jednej hierarchii. Ta hierarchia jest definiowana w dzierżawie usługi Azure Active Directory (Azure AD) w celu dopasowania jej do struktury i potrzeb organizacji. Najwyższy poziom jest nazywany *główną grupą zarządzania*. W hierarchii można zdefiniować maksymalnie sześć poziomów grup zarządzania. Każda subskrypcja jest zawarta tylko w jednej grupie zarządzania.

Platforma Azure oferuje cztery poziomy zakresu zarządzania: grupy zarządzania, subskrypcje, grupy zasobów i zasoby. Każdy dostęp lub zasady zastosowane na jednym poziomie w hierarchii są dziedziczone przez niższe poziomy. Właściciel zasobu lub właściciel subskrypcji nie może zmienić odziedziczonych zasad. To ograniczenie pomaga ulepszyć zarządzanie.

> [!NOTE]
> Pamiętaj, że dziedziczenie tagów nie jest obecnie dostępne, ale zostanie wkrótce udostępnione.

Przy użyciu tego modelu dziedziczenia można rozmieścić subskrypcje w hierarchii, tak aby w każdej subskrypcji były stosowane odpowiednie zasady i kontrole zabezpieczeń.

![Cztery poziomy zakresu do organizowania zasobów platformy Azure](../../ready/azure-setup-guide/media/organize-resources/scope-levels.png)

Każdy dostęp lub zasady w głównej grupie zarządzania dotyczy wszystkich zasobów w katalogu. Należy starannie rozważyć, które elementy są definiowane w tym zakresie. Należy uwzględnić tylko te przypisania, które muszą być dostępne.

Podczas początkowego definiowania hierarchii grup zarządzania należy najpierw utworzyć główną grupę zarządzania. Następnie można przenieść wszystkie istniejące subskrypcje z katalogu do głównej grupy zarządzania. Nowe subskrypcje są zawsze tworzone w głównej grupie zarządzania. Później można przenieść je do innej grupy zarządzania.

Gdy subskrypcja jest przenoszona do istniejącej grupy zarządzania, dziedziczy zasady i przypisania ról z hierarchii grupy zarządzania powyżej. Po utworzeniu wielu subskrypcji dla obciążeń platformy Azure należy utworzyć dodatkowe subskrypcje, które będą zawierać usługi platformy Azure udostępniane przez inne subskrypcje.

![Przykład hierarchii grupy zarządzania](../../_images/ready/management-group-hierarchy.png)

Aby uzyskać więcej informacji, zobacz [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="tips-for-creating-new-subscriptions"></a>Porady dotyczące tworzenia nowych subskrypcji

- Określ, kto będzie odpowiedzialny za tworzenie nowych subskrypcji.
- Zdecyduj, jakie zasoby subskrypcja będzie zawierać domyślnie.
- Zdecyduj, jak powinny wyglądać wszystkie standardowe subskrypcje. Rozważ kwestie związane z kontrolą dostępu opartą na rolach, zasadami, tagami zasobami infrastruktury.
- Jeśli to możliwe, podczas tworzenia nowych subskrypcji [używaj nazwy głównej usługi](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription). Zdefiniuj grupę zabezpieczeń, która może żądać nowych subskrypcji za pośrednictwem zautomatyzowanego przepływu pracy.
- Jeśli jesteś klientem mającym umowę Enterprise (EA), poproś pomoc techniczną platformy Azure o zablokowanie możliwości tworzenia subskrypcji niezwiązanych z umową EA dla organizacji.

## <a name="related-resources"></a>Zasoby powiązane

- [Podstawowe pojęcia dotyczące platformy Azure](../considerations/fundamental-concepts.md).
- [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups).
- [Podnoszenie poziomu dostępu w celu zarządzania wszystkimi subskrypcjami platformy Azure i grupami zarządzania](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin)
- [Przenoszenie zasobów platformy Azure do innej grupy zasobów lub subskrypcji](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources)

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z [zalecanymi konwencjami nazewnictwa i tagowania](./naming-and-tagging.md), które warto stosować podczas wdrażania zasobów platformy Azure.

> [!div class="nextstepaction"]
> [Zalecane konwencje nazewnictwa i tagowania](./naming-and-tagging.md)
