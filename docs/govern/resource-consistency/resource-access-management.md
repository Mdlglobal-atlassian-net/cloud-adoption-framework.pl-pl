---
title: Zarządzanie dostępem do zasobów na platformie Azure
description: Poznaj pojęcia związane z zarządzaniem dostępem do zasobów platformy Azure, takie jak Azure Resource Manager, subskrypcje, grupy zasobów i zasoby.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 23212be551ace2808757836a0e7ac135363dd8e3
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218190"
---
# <a name="resource-access-management-in-azure"></a>Zarządzanie dostępem do zasobów na platformie Azure

[Metodologia rządząca](../index.md) przedstawia pięć dyscyplin nadzoru chmurowego, w tym zarządzanie zasobami. [Co to jest zarządzanie dostępem do zasobów —](./index.md) omówienie sposobu, w jaki funkcja zarządzania dostępem do zasobów mieści się w dyscyplinie zarządzania zasobami. Aby dowiedzieć się, jak zaprojektować model ładu, ważne jest zrozumienie formantów zarządzania dostępem do zasobów na platformie Azure. Konfiguracja tych formantów zarządzania dostępem do zasobów stanowi podstawę modelu zarządzania.

Zacznij od przeszukania sposobu wdrażania zasobów na platformie Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Co to jest zasób platformy Azure?

Na platformie Azure termin " _zasób_ " odnosi się do jednostki zarządzanej przez platformę Azure. Na przykład maszyny wirtualne, sieci wirtualne i konta magazynu są określane jako zasoby platformy Azure.

![Diagram zasobu ](../../_images/govern/design/governance-1-9.png)
 _rysunek 1: zasób._

## <a name="what-is-an-azure-resource-group"></a>Co to jest Grupa zasobów platformy Azure?

Każdy zasób na platformie Azure musi należeć do [grupy zasobów](https://docs.microsoft.com/azure/azure-resource-manager/management/overview#resource-groups). Grupa zasobów to po prostu konstrukcja logiczna, która jednocześnie grupuje wiele zasobów, dzięki czemu można nimi zarządzać jako pojedynczą jednostką _w oparciu o cykl życia i zabezpieczenia_. Na przykład zasoby, które mają podobny cykl życia, takie jak zasoby dla [aplikacji n-warstwowej](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) , można utworzyć lub usunąć jako grupę. Można to zrobić w inny sposób: wszystkie informacje, które ponosisz, są zarządzane razem i są przestarzałe, razem z grupą zasobów.

![Diagram grupy zasobów zawierającej ](../../_images/govern/design/governance-1-10.png)
 _rysunek 2: Grupa zasobów zawiera zasób._

Grupy zasobów i zawarte w nich zasoby są skojarzone z **subskrypcją**platformy Azure.

## <a name="what-is-an-azure-subscription"></a>Co to jest subskrypcja platformy Azure?

Subskrypcja platformy Azure jest podobna do grupy zasobów, ponieważ jest to konstrukcja logiczna, która grupuje grupy zasobów i ich zasoby. Jednak subskrypcja platformy Azure jest również skojarzona z kontrolkami używanymi przez Azure Resource Manager. Zapoznaj się z Azure Resource Manager, aby dowiedzieć się więcej o relacji między działem IT i subskrypcją platformy Azure.

![Diagram subskrypcji platformy Azure ](../../_images/govern/design/governance-1-11.png)
 _— rysunek 3: subskrypcja platformy Azure._

## <a name="what-is-azure-resource-manager"></a>Co to jest Azure Resource Manager?

W [jaki sposób działa platforma Azure?](../../get-started/what-is-azure.md) dowiesz się, że platforma Azure obejmuje fronton z wieloma usługami, które organizują wszystkie funkcje platformy Azure. Jedna z tych usług jest [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager), a ta usługa obsługuje interfejs API RESTful używany przez klientów do zarządzania zasobami.

![Diagram Azure Resource Manager ](../../_images/govern/design/governance-1-12.png)
 _rysunku 4: Azure Resource Manager._

Na poniższej ilustracji przedstawiono trzech klientów: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Portal](https://portal.azure.com)i [interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure):

![Diagram klientów platformy Azure łączących się z interfejsem API Azure Resource Manager ](../../_images/govern/design/governance-1-13.png)
 _rysunek 5: klienci platformy Azure nawiązują połączenie z interfejsem API Azure Resource Manager RESTful._

Gdy ci klienci łączą się z Azure Resource Manager przy użyciu interfejsu API RESTful, Azure Resource Manager nie obejmuje funkcji bezpośredniego zarządzania zasobami. Zamiast tego większość typów zasobów na platformie Azure ma własnego [dostawcę zasobów](https://docs.microsoft.com/azure/azure-resource-manager/management/overview#terminology).

![Dostawcy zasobów platformy Azure ](../../_images/govern/design/governance-1-14.png)
 _rysunek 6: dostawcy zasobów platformy Azure._

Gdy klient wysyła żądanie zarządzania określonym zasobem, Azure Resource Manager nawiązuje połączenie z dostawcą zasobów dla tego typu zasobu w celu ukończenia żądania. Na przykład jeśli klient wysyła żądanie zarządzania zasobem maszyny wirtualnej, Azure Resource Manager nawiązuje połączenie z dostawcą zasobów **Microsoft. COMPUTE** .

![Azure Resource Manager łączenie z dostawcą zasobów Microsoft. COMPUTE, ](../../_images/govern/design/governance-1-15.png)
 _rysunek 7: Azure Resource Manager nawiązuje połączenie z dostawcą zasobów **Microsoft. COMPUTE** , aby zarządzać zasobem określonym w żądaniu klienta._

Azure Resource Manager wymaga od klienta określenia identyfikatora dla subskrypcji i grupy zasobów, aby zarządzać zasobem maszyny wirtualnej.

Teraz, gdy wiesz już, jak działa Azure Resource Manager, Wróć do omówienia sposobu, w jaki subskrypcja platformy Azure jest skojarzona z kontrolkami używanymi przez Azure Resource Manager. Aby można było wykonać dowolne żądanie zarządzania zasobami Azure Resource Manager, zostanie sprawdzony zestaw kontrolek.

Pierwsza kontrola polega na tym, że żądanie musi zostać wykonane przez zweryfikowanego użytkownika, a Azure Resource Manager ma zaufaną relację z [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory) w celu zapewnienia funkcjonalności tożsamości użytkowników.

![Azure Active Directory ](../../_images/govern/design/governance-1-16.png)
 _rysunek 8: Azure Active Directory._

W usłudze Azure AD użytkownicy są segmentacj do **dzierżawców**. Dzierżawca to logiczna konstrukcja, która reprezentuje bezpieczne, dedykowane wystąpienie usługi Azure AD zwykle skojarzone z organizacją. Każda subskrypcja jest skojarzona z dzierżawą usługi Azure AD.

![Dzierżawa usługi Azure AD skojarzona z subskrypcją ](../../_images/govern/design/governance-1-17.png)
 _rysunek 9: dzierżawa usługi Azure AD skojarzona z subskrypcją._

Każde żądanie klienta dotyczące zarządzania zasobem w określonej subskrypcji wymaga, aby użytkownik miał konto w skojarzonej dzierżawie usługi Azure AD.

Następna kontrolka to sprawdzenie, czy użytkownik ma wystarczające uprawnienia, aby wykonać żądanie. Uprawnienia są przypisywane do użytkowników przy użyciu [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Użytkownicy przypisani do ról RBAC ](../../_images/govern/design/governance-1-18.png)
 _rysunek 10: każdy użytkownik w dzierżawie ma przypisaną co najmniej jedną rolę RBAC._

Rola RBAC określa zestaw uprawnień, które użytkownik może wykonać względem określonego zasobu. Te uprawnienia są stosowane po przypisaniu roli do użytkownika. Na przykład [wbudowana rola **właściciela** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) umożliwia użytkownikowi wykonywanie dowolnych akcji względem zasobu.

Następna kontrolka to sprawdzenie, czy żądanie jest dozwolone w ustawieniach określonych dla [zasad zasobów platformy Azure](https://docs.microsoft.com/azure/governance/policy). Zasady zasobów platformy Azure określają operacje dozwolone dla określonego zasobu. Na przykład zasady zasobów platformy Azure mogą określać, że użytkownicy mogą tylko wdrażać określony typ maszyny wirtualnej.

![Rysunek 11 zasady dotyczące zasobów platformy Azure ](../../_images/govern/design/governance-1-19.png)
 _: zasady dotyczące zasobów platformy Azure._

Kolejna kontrola to sprawdzenie, czy żądanie nie przekracza [limitu subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits). Na przykład Każda subskrypcja ma limit 980 grup zasobów na subskrypcję. Jeśli Otrzymano żądanie wdrożenia dodatkowej grupy zasobów, gdy limit został osiągnięty, zostanie on odrzucony.

![Liczba limitów zasobów platformy Azure ](../../_images/govern/design/governance-1-20.png)
 _12: limity zasobów platformy Azure._

Ostatnia kontrola polega na sprawdzeniu, czy żądanie jest w ramach zobowiązania finansowego skojarzonego z subskrypcją. Na przykład jeśli żądanie dotyczy wdrożenia maszyny wirtualnej, Azure Resource Manager sprawdza, czy subskrypcja zawiera wystarczające informacje o płatności.

![Zobowiązanie finansowe powiązane z subskrypcją nr ](../../_images/govern/design/governance-1-21.png)
 _13: zobowiązanie finansowe jest skojarzone z subskrypcją._

## <a name="summary"></a>Podsumowanie

W tym artykule przedstawiono sposób zarządzania dostępem do zasobów na platformie Azure przy użyciu Azure Resource Manager.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz sposób zarządzania dostępem do zasobów na platformie Azure, przejdź do, aby dowiedzieć się, jak zaprojektować model ładu [dla prostego obciążenia](./governance-simple-workload.md) lub dla [wielu zespołów](./governance-multiple-teams.md) korzystających z tych usług.

> [!div class="nextstepaction"]
> [Przegląd dotyczący zarządzania](../index.md)
