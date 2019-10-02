---
title: Scentralizowanie operacji zarządzania
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wskazówki dotyczące scentralizowania operacji zarządzania
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b8e4e37ba9a771937b11f08f1abae45de2f818ab
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/02/2019
ms.locfileid: "71804732"
---
# <a name="centralize-management-operations"></a>Scentralizowanie operacji zarządzania

W przypadku większości organizacji korzystanie z pojedynczej dzierżawy usługi Azure Active Directory (Azure AD) dla wszystkich użytkowników upraszcza operacje zarządzania i zmniejsza koszty konserwacji, ponieważ wszystkie zadania zarządzania mogą być wyznaczonymi użytkownikami, grupami użytkowników lub jednostkami usługi w ramach tego dzierżaw. Jeśli to możliwe, zalecamy używanie tylko jednej dzierżawy usługi Azure AD dla Twojej organizacji.

Istnieją jednak sytuacje, które mogą wymagać od organizacji utrzymania wielu dzierżawców usługi Azure AD. Na przykład może być wymagana wiele dzierżawców z powodu:

- Całkowicie niezależne jednostki zależne.
- Działa niezależnie w wielu lokalizacje geograficzne.
- Wymagania prawne lub dotyczące zgodności.
- Pozyskiwanie innych organizacji (czasami czasowo do czasu zdefiniowania długoterminowej strategii konsolidacji dzierżawców).

W przypadkach, gdy wymagana jest architektura z wieloma dzierżawcami, [usługa Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) zapewnia sposób scentralizowania i usprawniania operacji zarządzania. Subskrypcje z wielu dzierżawców można dołączać do [zarządzania zasobami delegowanymi przez platformę Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management), umożliwiając określonym użytkownikom w dzierżawie zarządzającej wykonywanie [funkcji zarządzania między dzierżawcami](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) w scentralizowany i skalowalny sposób.

Załóżmy na przykład, że organizacja ma jedną dzierżawę, *dzierżawcę a*. Organizacja uzyskuje dwie dodatkowe dzierżawy, *dzierżawę B* i *dzierżawcę C*, a także masz przyczyny biznesowe, które wymagają utrzymania ich jako osobnych dzierżawców.

Organizacja chce używać tych samych definicji zasad, metod tworzenia kopii zapasowych i procesów zabezpieczeń we wszystkich dzierżawach. Ponieważ masz już użytkowników (w tym grupy użytkowników i jednostek usługi) odpowiedzialnych za wykonywanie tych zadań w ramach dzierżawy A, możesz dołączyć wszystkie subskrypcje w ramach dzierżawy B i dzierżawy C, aby Ci użytkownicy w dzierżawie mogli wykonać te czynności widoku. Dzierżawa A następnie będzie dzierżawą zarządzającą dla dzierżawy B i dzierżawy C.

![Użytkownicy w dzierżawie to zarządzanie zasobami w dzierżawie B i w ramach dzierżawy C](../_images/manage/enterprise-azure-lighthouse.jpg)

Aby uzyskać więcej informacji, zobacz [Azure Lighthouse w scenariuszach dla przedsiębiorstw](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
