---
title: Zarządzanie dostępem do zasobów na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Wyjaśnienie konstrukcji zarządzania dostępem do zasobów na platformie Azure: Azure Resource Manager, subskrypcje, grupy zasobów i zasoby'
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 46c6de1ecaba5b8278138114b6aa27a2608bfb74
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030860"
---
# <a name="resource-access-management-in-azure"></a>Zarządzanie dostępem do zasobów na platformie Azure

Zarządzanie [chmurą](../index.md) zawiera pięć dyscyplin nadzoru chmurowego, w tym zarządzania zasobami. [Co to jest zarządzanie dostępem do zasobów —](./index.md) omówienie sposobu, w jaki funkcja zarządzania dostępem do zasobów mieści się w dyscyplinie zarządzania zasobami. Aby dowiedzieć się, jak zaprojektować model ładu, ważne jest zrozumienie formantów zarządzania dostępem do zasobów na platformie Azure. Konfiguracja tych formantów zarządzania dostępem do zasobów stanowi podstawę modelu zarządzania.

Zacznij od przeszukania sposobu wdrażania zasobów na platformie Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>Co to jest zasób platformy Azure?

Na platformie Azure termin " _zasób_ " odnosi się do jednostki zarządzanej przez platformę Azure. Na przykład maszyny wirtualne, sieci wirtualne i konta magazynu są określane jako zasoby platformy Azure.

![Diagram zasobu](../../_images/govern/design/governance-1-9.png)
*rysunek 1 — zasób.*

## <a name="what-is-an-azure-resource-group"></a>Co to jest Grupa zasobów platformy Azure?

Każdy zasób na platformie Azure musi należeć do [grupy zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Grupa zasobów to po prostu konstrukcja logiczna, która grupuje wiele zasobów, dzięki czemu można nimi zarządzać jako pojedynczą jednostką. Na przykład zasoby, które mają podobny cykl życia, takie jak zasoby dla [aplikacji n-warstwowej](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) , można utworzyć lub usunąć jako grupę.

![Diagram grupy zasobów zawierającej](../../_images/govern/design/governance-1-10.png)
*rysunek 2. Grupa zasobów zawiera zasób.*

Grupy zasobów i zawarte w nich zasoby są skojarzone z **subskrypcją**platformy Azure.

## <a name="what-is-an-azure-subscription"></a>Co to jest subskrypcja platformy Azure?

Subskrypcja platformy Azure jest podobna do grupy zasobów, ponieważ jest to konstrukcja logiczna, która grupuje grupy zasobów i ich zasoby. Jednak subskrypcja platformy Azure jest również skojarzona z kontrolkami używanymi przez Azure Resource Manager. Co to oznacza? Zapoznaj się z Azure Resource Manager, aby dowiedzieć się więcej o relacji między działem IT i subskrypcją platformy Azure.

![Diagram subskrypcji](../../_images/govern/design/governance-1-11.png)
platformy Azure*3 — subskrypcja platformy Azure.*

## <a name="what-is-azure-resource-manager"></a>Co to jest Azure Resource Manager?

W [jaki sposób działa platforma Azure?](../../getting-started/what-is-azure.md) dowiesz się, że platforma Azure obejmuje "fronton" z wieloma usługami, które organizują wszystkie funkcje platformy Azure. Jedna z tych usług jest [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager), a ta usługa obsługuje interfejs API RESTful używany przez klientów do zarządzania zasobami.

![Diagram Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*rysunku 4 — Azure Resource Manager.*

Na poniższej ilustracji przedstawiono trzech klientów: Program [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Portal](https://portal.azure.com)i [interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure):

![Diagram klientów platformy Azure łączących się z interfejsem API](../../_images/govern/design/governance-1-13.png)
Azure Resource Manager*rysunek 5 — klienci platformy Azure nawiązują połączenie z interfejsem API Azure Resource Manager RESTful.*

Gdy ci klienci łączą się z Azure Resource Manager przy użyciu interfejsu API RESTful, Azure Resource Manager nie obejmuje funkcji bezpośredniego zarządzania zasobami. Zamiast tego większość typów zasobów na platformie Azure ma własnego [**dostawcę zasobów**](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![Dostawcy](../../_images/govern/design/governance-1-14.png)
zasobów platformy Azure*rysunek 6 — dostawcy zasobów platformy Azure.*

Gdy klient wysyła żądanie zarządzania określonym zasobem, Azure Resource Manager nawiązuje połączenie z dostawcą zasobów dla tego typu zasobu w celu ukończenia żądania. Na przykład jeśli klient wysyła żądanie zarządzania zasobem maszyny wirtualnej, Azure Resource Manager nawiązuje połączenie z dostawcą zasobów **Microsoft. COMPUTE** .

![Azure Resource Manager łączenie z dostawcą](../../_images/govern/design/governance-1-15.png)
zasobów Microsoft. COMPUTE,*rysunek 7 — Azure Resource Manager nawiązuje połączenie z dostawcą zasobów **Microsoft. COMPUTE** w celu zarządzania zasobem określonym w żądaniu klienta.*

Azure Resource Manager wymaga od klienta określenia identyfikatora dla subskrypcji i grupy zasobów, aby zarządzać zasobem maszyny wirtualnej.

Teraz, gdy wiesz już, jak działa Azure Resource Manager, Wróć do omówienia sposobu, w jaki subskrypcja platformy Azure jest skojarzona z kontrolkami używanymi przez Azure Resource Manager. Aby można było wykonać dowolne żądanie zarządzania zasobami Azure Resource Manager, zostanie sprawdzony zestaw kontrolek.

Pierwsza kontrola polega na tym, że żądanie musi zostać wykonane przez zweryfikowanego użytkownika, a Azure Resource Manager ma zaufaną relację z [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory) w celu zapewnienia funkcjonalności tożsamości użytkowników.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*rysunek 8 — Azure Active Directory.*

W usłudze Azure AD użytkownicy są segmentacj do **dzierżawców**. Dzierżawca to logiczna konstrukcja, która reprezentuje bezpieczne, dedykowane wystąpienie usługi Azure AD zwykle skojarzone z organizacją. Każda subskrypcja jest skojarzona z dzierżawą usługi Azure AD.

![Dzierżawa usługi Azure AD skojarzona z](../../_images/govern/design/governance-1-17.png)
subskrypcją *— rysunek 9 — dzierżawa usługi Azure AD skojarzona z subskrypcją.*

Każde żądanie klienta dotyczące zarządzania zasobem w określonej subskrypcji wymaga, aby użytkownik miał konto w skojarzonej dzierżawie usługi Azure AD.

Następna kontrolka to sprawdzenie, czy użytkownik ma wystarczające uprawnienia, aby wykonać żądanie. Uprawnienia są przypisywane do użytkowników przy użyciu [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Użytkownicy przypisani do ról](../../_images/govern/design/governance-1-18.png)
*RBAC rysunek 10. Każdy użytkownik w dzierżawie ma przypisaną co najmniej jedną rolę RBAC.*

Rola RBAC określa zestaw uprawnień, które użytkownik może wykonać względem określonego zasobu. Te uprawnienia są stosowane po przypisaniu roli do użytkownika. Na przykład [wbudowana rola **właściciela** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) umożliwia użytkownikowi wykonywanie dowolnych akcji względem zasobu.

Następna kontrolka to sprawdzenie, czy żądanie jest dozwolone w ustawieniach określonych dla [zasad zasobów platformy Azure](https://docs.microsoft.com/azure/governance/policy). Zasady zasobów platformy Azure określają operacje dozwolone dla określonego zasobu. Na przykład zasady zasobów platformy Azure mogą określać, że użytkownicy mogą tylko wdrażać określony typ maszyny wirtualnej.

![Rysunek 11 zasad](../../_images/govern/design/governance-1-19.png)
*dotyczących zasobów platformy Azure. Zasady zasobów platformy Azure.*

Kolejna kontrola to sprawdzenie, czy żądanie nie przekracza [limitu subskrypcji platformy Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Na przykład Każda subskrypcja ma limit 980 grup zasobów na subskrypcję. Jeśli Otrzymano żądanie wdrożenia dodatkowej grupy zasobów po osiągnięciu limitu, zostanie ono odrzucone.

![Liczba limitów](../../_images/govern/design/governance-1-20.png)
*zasobów platformy Azure 12. Limity zasobów platformy Azure.*

Ostatnia kontrola polega na sprawdzeniu, czy żądanie jest w ramach zobowiązania finansowego skojarzonego z subskrypcją. Na przykład jeśli żądanie dotyczy wdrożenia maszyny wirtualnej, Azure Resource Manager sprawdza, czy subskrypcja zawiera wystarczające informacje o płatności.

![Zobowiązanie finansowe skojarzone z subskrypcją](../../_images/govern/design/governance-1-21.png)
*nr 13. Zobowiązanie finansowe jest powiązane z subskrypcją.*

## <a name="summary"></a>Podsumowanie

W tym artykule przedstawiono sposób zarządzania dostępem do zasobów na platformie Azure przy użyciu Azure Resource Manager.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz sposób zarządzania dostępem do zasobów na platformie Azure, przejdź do, aby dowiedzieć się, jak zaprojektować model ładu [dla prostego obciążenia](./governance-simple-workload.md) lub dla [wielu zespołów](./governance-multiple-teams.md) korzystających z tych usług.

> [!div class="nextstepaction"]
> [Przegląd dotyczący zarządzania](../index.md)
