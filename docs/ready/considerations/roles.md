---
title: Zalecana kontrola dostępu oparta na rolach
description: Dowiedz się, jak oddzielić obowiązki w zespole i udzielić kontroli dostępu opartej na rolach, aby umożliwić użytkownikom i grupom wykonywanie zadań.
author: rotycenh
ms.author: brblanch
ms.date: 11/28/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: BrianBlanchard
ms.custom: virtual-network
ms.openlocfilehash: 2c7a57f339ad241f3d2f448a61d0553d1487bde7
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862623"
---
# <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach

Prawa dostępu opartego na grupach i uprawnieniach są dobrym rozwiązaniem. Zarządzanie grupami zamiast poszczególnymi użytkownikami upraszcza obsługę zasad dostępu, zapewnia spójne zarządzanie dostępem między różnymi zespołami i zmniejsza liczbę błędów konfiguracji. Przypisywanie użytkowników do odpowiednich grup i usuwanie ich z nich pomaga zachować aktualność uprawnień określonego użytkownika. [Kontrola dostępu oparta na rolach (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview) na platformie Azure oferuje szczegółowe zarządzanie dostępem dla zasobów zorganizowanych wokół ról użytkownika.

Omówienie zalecanych rozwiązań kontroli dostępu opartej na rolach w ramach strategii tożsamości i zabezpieczeń zawiera sekcja [Najlepsze rozwiązania dotyczące zabezpieczeń kontroli dostępu i zarządzania tożsamościami na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices#use-role-based-access-control).

## <a name="overview-of-role-based-access-control"></a>Omówienie kontroli dostępu opartej na rolach

Przy użyciu [kontroli dostępu opartej na rolach](https://docs.microsoft.com/azure/role-based-access-control/overview) można dokonać podziału obowiązków w zespole i nadawać określonym użytkownikom usługi Azure Active Directory (Azure AD), grupom, jednostkom usług lub jednostkom zarządzanym uprawnienia dostępu wystarczające do wykonania ich pracy. Zamiast udzielać wszystkim użytkownikom nieograniczonych uprawnień dostępu do subskrypcji lub zasobów platformy Azure możesz ograniczyć uprawnienia poszczególnych zestawów zasobów.

[Definicje ról kontroli dostępu opartej na rolach](https://docs.microsoft.com/azure/role-based-access-control/role-definitions) zawierają listę operacji, które są dozwolone lub niedozwolone dla użytkowników lub grup przypisanych do tej roli. [Zakres](https://docs.microsoft.com/azure/role-based-access-control/overview#scope) roli określa, których zasobów dotyczą zdefiniowane uprawnienia. Zakres można określić na wielu poziomach (grupa zarządzania, subskrypcja, grupa zasobów lub zasób). Zakresy mają strukturę relacji element nadrzędny/element podrzędny.

![Hierarchia zakresu kontroli dostępu opartej na rolach](../../_images/azure-best-practices/rbac-scope.png)

Aby uzyskać szczegółowe instrukcje dotyczące przypisywania użytkowników i grup do określonych ról i zakresów, zobacz [Zarządzanie dostępem do zasobów platformy Azure przy użyciu kontroli dostępu opartej na rolach](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

Podczas planowania strategii kontroli dostępu opartej na rolach należy zastosować model najniższych uprawnień, który polega na udzielaniu użytkownikom tylko uprawnień wymaganych do wykonania pracy. Na poniższym diagramie przedstawiono sugerowany wzorzec korzystania z kontroli dostępu opartej na rolach przy użyciu tego podejścia.

![Sugerowany wzorzec stosowania kontroli dostępu opartej na rolach](../../_images/azure-best-practices/rbac-least-privilege.png)

> [!NOTE]
> Im bardziej szczegółowo definiowane są uprawnienia, tym bardziej prawdopodobne, że kontrola dostępu stanie się złożona i trudna do zarządzania. Jest to szczególnie istotne wraz ze wzrostem rozmiaru majątku w chmurze. Unikaj uprawnień specyficznych dla zasobów. Zamiast tego należy użyć [grup zarządzania](https://docs.microsoft.com/azure/governance/management-groups) dla kontroli dostępu w całej firmie i [grup zasobów](https://docs.microsoft.com/azure/azure-resource-manager/management/overview#resource-groups) na potrzeby kontroli dostępu w ramach subskrypcji. Unikaj również uprawnień specyficznych dla użytkowników. Zamiast tego przypisz dostęp do [grup w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups).

## <a name="use-built-in-rbac-roles"></a>Korzystanie z wbudowanych ról RBAC

Platforma Azure udostępnia wiele wbudowanych definicji ról, w tym trzy podstawowe role do nadawania dostępu:

- Rola [Właściciel](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) umożliwia zarządzanie wszystkim, w tym dostępem do zasobów.
- Rola [Współautor](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) umożliwia zarządzanie wszystkim oprócz dostępu.
- Rola [Czytelnik](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader) umożliwia wyświetlanie wszystkiego, ale nie zezwala na wprowadzanie jakichkolwiek zmian.

Począwszy od tych podstawowych poziomów dostępu, dodatkowe wbudowane role zapewniają bardziej szczegółowe możliwości kontroli dostępu do określonych typów zasobów lub funkcji platformy Azure. Na przykład dostępem do maszyn wirtualnych można zarządzać, korzystając z następujących wbudowanych ról:

- Rola [logowania administratora maszyny wirtualnej](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-administrator-login) może wyświetlać maszyny wirtualne w portalu i zalogować się jako _administrator_.
- Rola [współautor maszyny wirtualnej](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) może zarządzać maszynami wirtualnymi, ale nie może uzyskać do nich dostępu ani do sieci wirtualnej lub konta magazynu, z którymi są połączone.
- Rola [logowania użytkownika maszyny wirtualnej](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-user-login) może wyświetlać maszyny wirtualne w portalu i zalogować się jako zwykły użytkownik.

Inny przykład korzystania z wbudowanych ról w celu zarządzania dostępem do określonych funkcji można znaleźć w omówieniu kontroli dostępu do funkcji śledzenia kosztów w [ramach śledzenia kosztów w różnych jednostkach, środowiskach i projektach](../azure-best-practices/track-costs.md#provide-the-right-level-of-cost-access).

Aby uzyskać pełną listę dostępnych wbudowanych ról, zobacz [Wbudowane role dla zasobów platformy Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).

## <a name="use-custom-roles"></a>Korzystanie z ról niestandardowych

Mimo że role wbudowane na platformie Azure obsługują szeroką gamę scenariuszy kontroli dostępu, mogą nie spełniać wszystkich potrzeb organizacji lub zespołu. Jeśli na przykład istnieje jedna grupa użytkowników odpowiedzialnych za zarządzanie maszynami wirtualnymi i zasobami usługi Azure SQL Database, możesz utworzyć rolę niestandardową w celu zoptymalizowania zarządzania wymaganą kontrolą dostępu.

Dokumentacja kontroli dostępu opartej na rolach na platformie Azure zawiera instrukcje dotyczące [tworzenia ról niestandardowych](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) oraz szczegółowe informacje na temat [działania definicji ról](https://docs.microsoft.com/azure/role-based-access-control/role-definitions).

## <a name="separation-of-responsibilities-and-roles-for-large-organizations"></a>Separacja obowiązków i ról w dużych organizacjach

Kontrola dostępu oparta na rolach umożliwia organizacjom przypisywanie różnych zespołów do różnych zadań związanych z zarządzaniem w ramach dużych majątków w chmurze. Umożliwia centralne zespoły IT kontrolować podstawowe funkcje dostępu i zabezpieczeń, zapewniając jednocześnie deweloperom oprogramowania i innym zespołom dużą ilość kontroli nad określonymi obciążeniami lub grupami zasobów.

W większości środowisk chmury może być również korzystne zastosowanie strategii kontroli dostępu opartej na wielu rolach z naciskiem na podział obowiązków między tymi rolami. To podejście wymaga zaangażowania wielu ról w wykonanie każdej znaczącej zmiany dotyczącej zasobów lub infrastruktury, co gwarantuje, że co najmniej jedna osoba musi sprawdzić i zatwierdzić zmianę. Ten podział obowiązków ogranicza możliwość dostępu pojedynczej osoby do poufnych danych lub wprowadzenia luk w zabezpieczeniach bez wiedzy pozostałych członków zespołu.

W poniższej tabeli przedstawiono typowy wzorzec podziału obowiązków IT na oddzielne role niestandardowe:

<!-- markdownlint-disable MD033 -->

| Grupa | Typowa nazwa roli | Zakres odpowiedzialności |
| --- | --- | --- |
| Operacje zabezpieczeń | SecOP | Zapewnia ogólny nadzór nad bezpieczeństwem. <br> Ustanawia i wymusza zasady zabezpieczeń, takie jak szyfrowanie w spoczynku. <br><br> Zarządza kluczami szyfrowania. <br><br> Zarządza regułami zapory. |
| Operacje sieciowe | Netops | Zarządza konfiguracją sieci i operacjami w sieciach wirtualnych, takimi jak trasy i komunikacja równorzędna. |
| Operacje na systemach | Sysops | Określa opcje infrastruktury obliczeniowej i magazynu oraz obsługuje wdrożone zasoby. |
| Programowanie, testowanie i operacje | DevOps | Kompiluje i wdraża funkcje i aplikacje obciążeń. <br><br> Obsługuje funkcje i aplikacje w celu spełnienia wymagań umów dotyczących poziomu usług (umowy SLA) i innych standardów jakości. |

<!-- markdownlint-enable MD033 -->

Podział akcji i uprawnień w tych rolach standardowych jest często taki sam w przypadku aplikacji, subskrypcji lub całej chmury, nawet jeśli te role są wykonywane przez różne osoby na różnych poziomach. Dlatego można utworzyć wspólny zestaw definicji ról kontroli dostępu opartej na rolach do zastosowania w różnych zakresach środowiska. Użytkownikom i grupom można przypisać wspólną rolę, ale tylko dla zakresu zasobów, grup zasobów, subskrypcji lub grup zarządzania, za zarządzanie którymi odpowiadają.

Na przykład w [topologii sieci gwiazdy i szprych](../azure-best-practices/hub-spoke-network-topology.md) z wieloma subskrypcjami może istnieć wspólny zestaw definicji ról dla centrum i wszystkich szprych obciążeń. Rolę NetOps subskrypcji centrum można przypisać do członków centralnych pracowników organizacji, którzy są odpowiedzialni za obsługę sieci dla usług udostępnionych używanych przez wszystkie obciążenia. Rolę NetOps subskrypcji satelity obciążenia można przypisać do członków tego konkretnego zespołu obciążenia, co pozwoli im na skonfigurowanie sieci w ramach tej subskrypcji w celu zapewnienia optymalnej obsługi wymagań dotyczących obciążenia. W obu przypadkach jest używana ta sama definicja roli, ale przypisania oparte na zakresie dają pewność, że użytkownicy mają tylko dostęp, którego potrzebują do wykonywania swojej pracy.
