---
title: Projekt nadzoru dla jednego obciążenia
description: Poznaj proces projektowania modelu zarządzania zasobami na platformie Azure w celu obsługi jednego zespołu i prostego obciążenia. 
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: efdca4c5848e8815166fd2ddf308d40ae62f75a1
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223725"
---
# <a name="governance-design-for-a-simple-workload"></a>Projekt nadzoru dla jednego obciążenia

Celem tych wskazówek jest ułatwienie poznania procesu projektowania modelu zarządzania zasobami na platformie Azure w celu obsługi jednego zespołu i prostego obciążenia. Zapoznaj się z zestawem hipotetycznych wymagań ładu, a następnie przejdź do kilku przykładowych implementacji, które spełniają te wymagania.

Naszym celem jest wdrożenie prostych obciążeń na platformie Azure. W wyniku tego są spełnione następujące wymagania:

- Zarządzanie tożsamościami dla pojedynczego **właściciela obciążenia** , który jest odpowiedzialny za wdrażanie i utrzymywanie prostego obciążenia. Właściciel obciążenia wymaga uprawnień do tworzenia, odczytywania, aktualizowania i usuwania zasobów oraz uprawnienia do delegowania tych praw innym użytkownikom w systemie zarządzania tożsamościami.
- Zarządzaj wszystkimi zasobami dla prostego obciążenia jako pojedynczą jednostką zarządzania.

## <a name="azure-licensing"></a>Licencjonowanie platformy Azure

Przed rozpoczęciem projektowania naszego modelu zarządzania należy zrozumieć, w jaki sposób platforma Azure jest licencjonowana. Wynika to z faktu, że konta administracyjne skojarzone z licencją platformy Azure mają najwyższy poziom dostępu do zasobów platformy Azure. Te konta administracyjne stanowią podstawę modelu zarządzania.

> [!NOTE]
> Jeśli Twoja organizacja ma istniejące [Umowa Enterprise firmy Microsoft](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) , które nie obejmuje platformy Azure, można dodać platformę Azure, wykonując zobowiązania pieniężne z góry. Aby uzyskać więcej informacji, zobacz [Licencjonowanie platformy Azure dla przedsiębiorstwa](https://azure.microsoft.com/pricing/enterprise-agreement).

Po dodaniu platformy Azure do Umowa Enterprise organizacji zostanie wyświetlony monit o utworzenie **konta platformy Azure**. Podczas procesu tworzenia konta utworzono **właściciela konta platformy Azure** , a także dzierżawę usługi Azure Active Directory (Azure AD) z kontem **administratora globalnego** . Dzierżawa usługi Azure AD to logiczna konstrukcja, która reprezentuje bezpieczne, dedykowane wystąpienie usługi Azure AD.

![konto platformy Azure z menedżerem kont platformy Azure i administratorem globalnym usługi Azure AD](../../_images/govern/design/governance-3-0.png)
*rysunek 1 — konto platformy Azure z menedżerem kont i administratorem globalnym usługi Azure AD.*

## <a name="identity-management"></a>Zarządzanie tożsamościami

System Azure ufa tylko [usłudze Azure AD](https://docs.microsoft.com/azure/active-directory) w celu uwierzytelniania użytkowników i autoryzowania dostępu użytkowników do zasobów, dzięki czemu usługa Azure AD jest naszym systemem zarządzania tożsamościami. Administrator globalny usługi Azure AD ma najwyższy poziom uprawnień i może wykonywać wszystkie działania związane z tożsamością, w tym tworzenie użytkowników i przypisywanie uprawnień.

Naszym wymaganiem jest zarządzanie tożsamościami dla jednego **właściciela obciążenia** , który jest odpowiedzialny za wdrażanie i utrzymywanie prostego obciążenia. Właściciel obciążenia wymaga uprawnień do tworzenia, odczytywania, aktualizowania i usuwania zasobów oraz uprawnienia do delegowania tych praw innym użytkownikom w systemie zarządzania tożsamościami.

Nasz Administrator globalny usługi Azure AD utworzy konto **właściciela obciążenia** dla właściciela obciążenia:

![Administrator globalny usługi Azure AD tworzy konto właściciela obciążenia](../../_images/govern/design/governance-1-2.png)
*rysunku 2 — Administrator globalny usługi Azure AD tworzy konto użytkownika właściciela obciążenia.*

Nie można przypisać uprawnienia dostępu do zasobów, dopóki ten użytkownik nie zostanie dodany do **subskrypcji**, więc należy to zrobić w następnych dwóch sekcjach.

## <a name="resource-management-scope"></a>Zakres zarządzania zasobami

Wraz ze wzrostem liczby zasobów wdrożonych przez organizację zwiększa się również złożoność tych zasobów. Platforma Azure implementuje logiczną hierarchię kontenerów, aby umożliwić organizacji zarządzanie zasobami w grupach na różnych poziomach szczegółowości, nazywanych również **zakresem**.

Najwyższy poziom zakresu zarządzania zasobami to poziom **subskrypcji** . Subskrypcja jest tworzona przez **właściciela konta**platformy Azure, który ustanawia zobowiązania finansowe i jest odpowiedzialny za zapłacenie za wszystkie zasoby platformy Azure skojarzone z subskrypcją:

![właściciel konta Azure tworzy subskrypcję](../../_images/govern/design/governance-1-3.png)
*rysunku 3 — właściciel konta platformy Azure tworzy subskrypcję.*

Po utworzeniu subskrypcji **właściciel konta** platformy Azure kojarzy dzierżawę usługi Azure AD z subskrypcją, a ta dzierżawa usługi Azure AD jest używana do uwierzytelniania i autoryzowania użytkowników:

![właściciel konta platformy Azure kojarzy dzierżawę usługi Azure AD z subskrypcją](../../_images/govern/design/governance-1-4.png)
*rysunek 4 — właściciel konta platformy Azure kojarzy dzierżawę usługi Azure AD z subskrypcją.*

Być może zauważono, że nie istnieje żaden użytkownik skojarzony z subskrypcją, co oznacza, że nikt nie ma uprawnień do zarządzania zasobami. W rzeczywistości **właściciel konta** jest właścicielem subskrypcji i ma uprawnienia do wykonania dowolnej akcji dotyczącej zasobu w subskrypcji. Jednakże w praktyce **właściciel konta** jest bardziej niż prawdopodobnie osobą finansową w organizacji i nie jest odpowiedzialny za tworzenie, odczytywanie, aktualizowanie i usuwanie zasobów — te zadania będą wykonywane przez **właściciela obciążenia**. W związku z tym należy dodać **właściciela obciążenia** do subskrypcji i przypisać uprawnienia.

Ponieważ **właściciel konta** jest obecnie jedynym użytkownikiem z uprawnieniami do dodawania **właściciela obciążenia** do subskrypcji, Dodaj **właściciela obciążenia** do subskrypcji:

![właściciel konta platformy Azure dodaje do subskrypcji * * właściciela obciążenia * *,](../../_images/govern/design/governance-1-5.png)
*rysunek 5 — właściciel konta platformy Azure dodaje właściciela obciążenia do subskrypcji.*

**Właściciel konta** platformy Azure przyznaje uprawnienia **właścicielowi obciążenia** , przypisując rolę [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control) . Rola RBAC określa zestaw uprawnień, które **właściciel obciążenia** ma dla danego typu zasobu lub zestawu typów zasobów.

Zwróć uwagę, że w tym przykładzie **właściciel konta** ma przypisaną [wbudowaną rolę **właściciela** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner):

![* * z właścicielem obciążenia * * została przypisana wbudowana rola właściciela](../../_images/govern/design/governance-1-6.png)
*rysunek 6 — właściciel obciążenia ma przypisaną wbudowaną rolę właściciela.*

Wbudowana rola **właściciela** przyznaje wszystkim uprawnienia **właścicielowi obciążenia** w zakresie subskrypcji.

> [!IMPORTANT]
> **Właściciel konta** platformy Azure jest odpowiedzialny za zobowiązania finansowe skojarzone z subskrypcją, ale **właściciel obciążenia** ma takie same uprawnienia. **Właściciel konta** musi ufać **właścicielowi obciążenia** w celu wdrożenia zasobów objętych budżetem subskrypcji.

Następnym poziomem zakresu zarządzania jest poziom **grupy zasobów** . Grupa zasobów jest kontenerem logicznym dla zasobów. Operacje zastosowane na poziomie grupy zasobów mają zastosowanie do wszystkich zasobów w grupie. Należy również pamiętać, że uprawnienia dla każdego użytkownika są dziedziczone z następnego poziomu, chyba że zostaną jawnie zmienione w tym zakresie.

Aby to zilustrować, przyjrzyjmy się tym, co się stanie, gdy **właściciel obciążenia** tworzy grupę zasobów:

![* * właściciel obciążenia * * tworzy grupę zasobów](../../_images/govern/design/governance-1-7.png)
*rysunek 7. właściciel obciążenia tworzy grupę zasobów i dziedziczy rolę właściciela wbudowanego w zakresie grupy zasobów.*

Ponownie wbudowana rola **właściciela** przyznaje wszystkim uprawnienia **właścicielowi obciążenia** w zakresie grupy zasobów. Jak wspomniano wcześniej, ta rola jest dziedziczona z poziomu subskrypcji. Jeśli w tym zakresie jest przypisana inna rola, ma ona zastosowanie tylko do tego zakresu.

Najniższy poziom zakresu zarządzania znajduje się na poziomie **zasobu** . Operacje zastosowane na poziomie zasobu dotyczą tylko samego zasobu. Ponownie uprawnienia na poziomie zasobu są dziedziczone z zakresu grupy zasobów. Na przykład przyjrzyjmy się, co się stanie, jeśli **właściciel obciążenia** wdroży [sieć wirtualną](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) w grupie zasobów:

![* * właściciel obciążenia * * tworzy zasób](../../_images/govern/design/governance-1-8.png)
*rysunek 8 — właściciel obciążenia tworzy zasób i dziedziczy wbudowaną rolę właściciela w zakresie zasobów.*

**Właściciel obciążenia** dziedziczy rolę właściciela w zakresie zasobów, co oznacza, że właściciel obciążenia ma wszystkie uprawnienia do sieci wirtualnej.

## <a name="implement-the-basic-resource-access-management-model"></a>Implementowanie podstawowego modelu zarządzania dostępem do zasobów

Przejdźmy, aby dowiedzieć się, jak zaimplementować model ładu zaprojektowany wcześniej.

Aby rozpocząć, organizacja wymaga konta platformy Azure. Jeśli Twoja organizacja ma istniejące [Umowa Enterprise firmy Microsoft](https://www.microsoft.com/licensing/licensing-programs/enterprise.aspx) , które nie obejmuje platformy Azure, można dodać platformę Azure, wykonując zobowiązania pieniężne z góry. Aby uzyskać więcej informacji, zobacz [Licencjonowanie platformy Azure dla przedsiębiorstwa](https://azure.microsoft.com/pricing/enterprise-agreement).

Po utworzeniu konta platformy Azure należy określić osobę w organizacji jako **właściciela konta**platformy Azure. Domyślnie zostanie utworzona dzierżawa usługi Azure Active Directory (Azure AD). **Właściciel konta** platformy Azure musi [utworzyć konto użytkownika](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) dla osoby w organizacji, która jest **właścicielem obciążenia**.

Następnie **właściciel konta** platformy Azure musi [utworzyć subskrypcję](https://docs.microsoft.com/partner-center/create-a-new-subscription) i skojarzyć z nią [dzierżawcę usługi Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory) .

Teraz, gdy subskrypcja została utworzona i skojarzona jest dzierżawa usługi Azure AD, możesz [dodać **właściciela obciążenia** do subskrypcji przy użyciu wbudowanej roli **właściciela** ](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#to-assign-a-user-as-an-administrator).

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Wdrażanie podstawowego obciążenia na platformie Azure](../../infrastructure/virtual-machines/basic-workload.md)
> [!div class="nextstepaction"]
> [Informacje o dostępie do zasobów dla wielu zespołów](./governance-multiple-teams.md)
