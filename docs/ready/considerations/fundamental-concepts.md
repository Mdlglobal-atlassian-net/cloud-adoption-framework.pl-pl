---
title: Podstawowe pojęcia dotyczące platformy Azure
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby poznać podstawowe koncepcje i terminy używane na platformie Azure oraz jak koncepcje odnoszą się do siebie.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 869b3b9e0a283ce28c6fba7807d0282dcb53d9cf
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216337"
---
# <a name="azure-fundamental-concepts"></a>Podstawowe pojęcia dotyczące platformy Azure

Poznaj podstawowe pojęcia i terminy używane na platformie Azure i dowiedz się, jak te pojęcia odnoszą się do siebie nawzajem.

## <a name="azure-terminology"></a>Terminologia dotycząca platformy Azure

Rozpoczynając pracę związaną z wdrażaniem w chmurze platformy Azure warto znać następujące definicje:

- **Zasób:** Jednostka zarządzana przez platformę Azure. Przykłady: maszyny wirtualne platformy Azure, sieci wirtualne i konta magazynu.
- **Subskrypcja:** Kontener logiczny dla zasobów. Każdy zasób platformy Azure jest skojarzony tylko z jedną subskrypcją. Tworzenie subskrypcji to pierwszy krok w ramach wdrażania platformy Azure.
- **Konto platformy Azure:** Adres e-mail, który należy podać podczas tworzenia subskrypcji platformy Azure, to konto platformy Azure dla subskrypcji. Jednostka skojarzona z kontem e-mail jest odpowiedzialna za miesięczne koszty naliczane dla zasobów w ramach subskrypcji. Podczas tworzenia konta platformy Azure należy podać informacje kontaktowe i szczegółowe dane rozliczeniowe, takie jak karta kredytowa. Możesz użyć tego samego konta platformy Azure (adresu e-mail) dla wielu subskrypcji. Każda subskrypcja jest skojarzona tylko z jednym kontem platformy Azure.
- **Administrator konta:** Strona skojarzona z adresem e-mail używanym do tworzenia subskrypcji platformy Azure. Administrator konta jest odpowiedzialny za zapłacenie za wszystkie koszty wynikające z zasobów subskrypcji.
- **Azure Active Directory (Azure AD):** Usługa zarządzania tożsamościami i dostępem w chmurze firmy Microsoft. Usługa Azure AD umożliwia pracownikom logowanie się i dostęp do zasobów.
- **Dzierżawa usługi Azure AD:** Dedykowane i zaufane wystąpienie usługi Azure AD. Dzierżawa usługi Azure AD jest tworzona automatycznie, gdy organizacja rejestruje się po raz pierwszy w subskrypcji usługi w chmurze firmy Microsoft, takiej jak Microsoft Azure, Microsoft Intune lub Office 365. Dzierżawa usługi Azure reprezentuje jedną organizację.
- **Katalog usługi Azure AD:** Każda dzierżawa usługi Azure AD ma jeden, dedykowany i zaufany katalog. Katalog ten zawiera użytkowników, grupy i aplikacje dzierżawy. Katalog służy do obsługi funkcji związanych z zarządzaniem tożsamościami i dostępem do zasobów dzierżawy. Katalog może być skojarzony z wieloma subskrypcjami, ale każda subskrypcja jest skojarzona tylko z jednym katalogiem.
- **Grupy zasobów:** Kontenery logiczne używane do grupowania powiązanych zasobów w ramach subskrypcji. Każdy zasób może znajdować się tylko w jednej grupie zasobów. Grupy zasobów umożliwiają dokładniejsze grupowanie w ramach subskrypcji i są często używane do reprezentowania kolekcji zasobów wymaganych do obsługi obciążenia, aplikacji lub konkretnej funkcji w ramach subskrypcji.
- **Grupy zarządzania:** Kontenery logiczne, które są używane dla co najmniej jednej subskrypcji. Można zdefiniować hierarchię grup zarządzania, subskrypcji, grup zasobów i zasobów, aby efektywnie zarządzać dostępem, zasadami i zgodnością przez dziedziczenie.
- **Region:** Zestaw centrów danych platformy Azure, które są wdrażane w ramach określonego czasu oczekiwania. Centra danych są połączone za pomocą dedykowanej, regionalnej sieci o małym opóźnieniu. Większość zasobów platformy Azure działa w określonym regionie platformy Azure.

## <a name="azure-subscription-purposes"></a>Cele subskrypcji platformy Azure

Subskrypcja platformy Azure umożliwia realizację kilku celów. Subskrypcja platformy Azure to:

- **Umowa prawna.** Każda subskrypcja jest skojarzona z [ofertą platformy Azure](https://azure.microsoft.com/support/legal/offer-details), taką jak bezpłatna wersja próbna lub płatność zgodnie z rzeczywistym użyciem. Każda oferta ma określony plan taryfowy, korzyści oraz powiązane warunki i postanowienia. Ofertę platformy Azure można wybrać podczas tworzenia subskrypcji.
- **Umowa dotycząca płatności.** Podczas tworzenia subskrypcji należy podać informacje o płatności dla tej subskrypcji, takie jak numer karty kredytowej. W każdym miesiącu koszty wynikające z zasobów wdrożonych w ramach tej subskrypcji są obliczane i rozliczane za pośrednictwem tej metody płatności.
- **Granica skali.** Dla subskrypcji definiowane są limity skalowania. Zasoby subskrypcji nie mogą przekraczać ustawionych limitów skali. Na przykład istnieje ograniczenie liczby maszyn wirtualnych, które można utworzyć w ramach jednej subskrypcji.
- **Granica administracyjna.** Subskrypcja może działać jako granica administrowania, zabezpieczeń i zasad. Platforma Azure udostępnia również inne mechanizmy w celu spełnienia tych wymagań, takie jak grupy zarządzania, grupy zasobów i kontrola dostępu oparta na rolach.

## <a name="azure-subscription-considerations"></a>Zagadnienia dotyczące subskrypcji platformy Azure

Podczas tworzenia subskrypcji platformy Azure należy dokonać kilku najważniejszych wyborów dotyczących subskrypcji:

- **Kto jest odpowiedzialny za płatność za subskrypcję?** Strona skojarzona z adresem e-mail podanym podczas tworzenia subskrypcji jest domyślnie administratorem konta subskrypcji. Strona skojarzona z tym adresem e-mail jest odpowiedzialna za płatność za wszystkie koszty wynikające z zasobów subskrypcji.
- **Która oferta platformy Azure Cię interesuje?** Każda subskrypcja jest powiązana z określoną [ofertą platformy Azure](https://azure.microsoft.com/support/legal/offer-details). Możesz wybrać ofertę platformy Azure, która najlepiej odpowiada Twoim potrzebom. Na przykład jeśli zamierzasz używać subskrypcji do uruchamiania obciążeń nieprodukcyjnych, możesz wybrać ofertę oferty Płatność zgodnie z rzeczywistym użyciem — tworzenie i testowanie lub Enterprise — tworzenie i testowanie.

> [!NOTE]
> Podczas rejestracji na platformie Azure może zostać wyświetlony tekst _Utwórz konto platformy Azure_. Konto platformy Azure jest tworzone podczas tworzenia subskrypcji platformy Azure i kojarzenia subskrypcji z kontem e-mail.

## <a name="azure-administrative-roles"></a>Role administracyjne platformy Azure

Na platformie Azure definiowane są trzy typy ról do administrowania subskrypcjami, tożsamościami i zasobami:

- Role administratora klasycznej subskrypcji.
- Role kontroli dostępu opartej na rolach (RBAC) na platformie Azure.
- Role administratora usługi Azure Active Directory (Azure AD).

Rola administratora konta dla subskrypcji platformy Azure jest przypisywana do konta e-mail użytego do tworzenia subskrypcji platformy Azure. Administrator konta jest właścicielem rozliczenia subskrypcji. Administrator konta może zarządzać szczegółami subskrypcji w [Centrum konta platformy Azure](https://account.azure.com/subscriptions).

Domyślnie rola administratora konta dla subskrypcji platformy Azure jest również przypisywana do konta e-mail użytego do tworzenia subskrypcji platformy Azure. Jeśli jest używana kontrola dostępu oparta na rolach, administrator usługi ma uprawnienia do subskrypcji odpowiadające roli właściciela. Administrator usługi ma również pełny dostęp do witryny Azure Portal. Administrator konta może zmienić administratora usługi na inne konto e-mail.

Podczas tworzenia subskrypcji platformy Azure można ją skojarzyć z istniejącą dzierżawą usługi Azure AD. W przeciwnym razie zostanie utworzona nowa dzierżawa usługi Azure AD ze skojarzonym katalogiem. Rola administratora globalnego dla katalogu usługi Azure AD jest przypisywana do konta e-mail użytego do tworzenia subskrypcji usługi Azure AD.

Konto e-mail może być skojarzone z wieloma subskrypcjami platformy Azure. Administrator konta może przenieść subskrypcję na inne konto.

Aby zapoznać się ze szczegółowym opisem ról zdefiniowanych na platformie Azure, zobacz [Role klasycznego administratora subskrypcji, role kontroli dostępu opartej rolach platformy Azure i role administratora usługi Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Subskrypcje a regiony

Każdy zasób platformy Azure jest skojarzony logicznie tylko z jedną subskrypcją. Podczas tworzenia zasobu należy wybrać subskrypcję platformy Azure, w której ma zostać wdrożony ten zasób. Zasób można później przenieść do innej subskrypcji.

Subskrypcja nie jest powiązana z określonym regionem platformy Azure. Jednak każdy zasób platformy Azure jest wdrażany tylko w jednym regionie. Można mieć w wielu regionach zasoby, które są skojarzone z tą samą subskrypcją.

> [!NOTE]
> Większość zasobów platformy Azure jest wdrażanych w określonym regionie. Jednak niektóre typy zasobów są uznawane za zasoby globalne, na przykład zasady określane za pomocą usług Azure Policy.

## <a name="related-resources"></a>Powiązane zasoby

Poniższe zasoby zawierają szczegółowe informacje na temat pojęć omówionych w tym artykule:

- [Jak działa platforma Azure?](../../get-started/what-is-azure.md)
- [Zarządzanie dostępem do zasobów na platformie Azure](../../govern/resource-consistency/resource-access-management.md)
- [Przegląd Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview)
- [Kontrola dostępu oparta na rolach (RBAC) dla zasobów platformy Azure](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [Co to jest usługa Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
- [Kojarzenie subskrypcji platformy Azure z dzierżawą usługi Azure Active Directory lub dodawanie subskrypcji](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
- [Topologie obsługiwane w programie Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)
- [Subskrypcje, licencje, konta i dzierżawy dla ofert w chmurze firmy Microsoft](https://docs.microsoft.com/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz podstawowe pojęcia związane z platformą Azure, dowiedz się, jak [skalować za pomocą wielu subskrypcji platformy Azure](../azure-best-practices/scale-subscriptions.md).

> [!div class="nextstepaction"]
> [Skalowanie za pomocą wielu subskrypcji platformy Azure](../azure-best-practices/scale-subscriptions.md)
