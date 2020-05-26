---
title: Przewodnik po decyzjach związanych z tożsamością
description: Dowiedz się, w jaki sposób usługi zarządzania dostępem i tożsamościami (IAM, identity and access management) umożliwiają zarządzanie kontrolą dostępu w chmurze.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 3c89c5347032d0dcec68344066ac00028fedb7bd
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83753788"
---
<!-- cSpell:ignore Kerberos NTLM SAML -->

# <a name="identity-decision-guide"></a>Przewodnik po decyzjach związanych z tożsamością

W dowolnym środowisku, zarówno lokalnym, hybrydowym, jak i tylko w chmurze, dział IT musi kontrolować, którzy administratorzy, użytkownicy i grupy mają dostęp do zasobów. Usługi zarządzania dostępem i tożsamościami (IAM, identity and access management) umożliwiają zarządzanie kontrolą dostępu w chmurze.

![Wykres opcji tożsamości od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-identity.png)

Idź do: [Określanie wymagań dotyczących integracji tożsamości](#determine-identity-integration-requirements) | [Punkt odniesienia chmury](#cloud-baseline) | [Synchronizacja katalogów](#directory-synchronization) | [Usługi domenowe hostowane w chmurze](#cloud-hosted-domain-services) | [Usługi Active Directory Federation Services](#active-directory-federation-services) | [Dowiedz się więcej](#learn-more)

Dostępne są różne rozwiązania do zarządzania tożsamościami w środowisku chmury. Różnią się one kosztami i złożonością. Kluczowym czynnikiem w tworzeniu struktury opartych na chmurze usług zarządzania tożsamościami jest poziom integracji wymagany przez istniejącą infrastrukturę tożsamości w środowisku lokalnym.

Usługa Azure Active Directory (Azure AD) zapewnia podstawowy poziom kontroli dostępu i zarządzania tożsamościami dla zasobów na platformie Azure. Jeśli lokalna infrastruktura usługi Active Directory organizacji ma złożoną strukturę lasu lub niestandardowe jednostki organizacyjne, obciążenia oparte na chmurze mogą wymagać synchronizacji katalogu z usługą Azure AD dla zachowania spójności zestawu tożsamości, grup i ról między środowiskiem lokalnym i środowiskiem w chmurze. Ponadto obsługa aplikacji korzystających z mechanizmów uwierzytelniania w starszej wersji może wymagać wdrożenia usługi Active Directory Domain Services (AD DS) w chmurze.

Zarządzanie tożsamościami w chmurze jest procesem iteracyjnym. W przypadku początkowego wdrożenia można rozpocząć od rozwiązania natywnego dla chmury z małym zestawem użytkowników i odpowiednich ról. W miarę dojrzewania migracji konieczne może być zintegrowanie rozwiązania do obsługi tożsamości za pomocą synchronizacji katalogów lub dodanie usług domenowych w ramach wdrożeń w chmurze. Ponownie sprawdzaj swoją strategię dotyczącą obsługi tożsamości przy każdej iteracji procesu migracji.

## <a name="determine-identity-integration-requirements"></a>Określanie wymagań dotyczących integracji tożsamości

| Pytanie | Punkt odniesienia chmury | Synchronizacja katalogów | Usługi domenowe hostowane w chmurze | Usługi Active Directory Federation Services |
|------|------|------|------|------|
| Czy obecnie nie masz usługi katalogowej w środowisku lokalnym? | Yes | Nie | Nie | Nie |
| Czy Twoje obciążenia muszą korzystać ze wspólnego zestawu użytkowników i grup między środowiskiem w chmurze i lokalnym? | Nie | Yes | Nie | Nie |
| Czy Twoje obciążenia są zależne od mechanizmów uwierzytelniania w starszej wersji, takich jak Kerberos lub NTLM? | Nie | Nie | Yes | Yes |
| Czy wymagasz logowania jednokrotnego u wielu dostawców tożsamości? | Nie | Nie | Nie | Yes |

W ramach planowania migracji na platformę Azure należy określić najlepszy sposób integracji istniejącego zarządzania tożsamościami i usług zarządzania tożsamościami w chmurze. Poniżej przedstawiono typowe scenariusze integracji.

### <a name="cloud-baseline"></a>Punkt odniesienia chmury

Usługa Azure AD to natywny system zarządzania dostępem i tożsamościami (IAM, Identity and Access Management) służący do przyznawania użytkownikom i grupom dostępu do funkcji zarządzania na platformie Azure. Jeśli Twoja organizacja nie ma istotnego lokalnego rozwiązania do zarządzania tożsamościami i planujesz migrację obciążeń, aby były zgodne z mechanizmami uwierzytelniania opartego na chmurze, warto zacząć tworzenie infrastruktury tożsamości przy użyciu usługi Azure AD jako podstawy.

**Założenia dotyczące punktu odniesienia chmury:** Użycie czysto natywnej dla chmury infrastruktury tożsamości obejmuje następujące założenia:

- Zasoby oparte na chmurze nie będą zależne od lokalnych usług katalogowych ani serwerów usługi Active Directory lub obciążenia można modyfikować w celu usunięcia tych zależności.
- Migrowane obciążenia aplikacji lub usługi obsługują mechanizmy uwierzytelniania zgodne z usługą Azure AD lub można łatwo je modyfikować w celu ich obsługi. Usługa Azure AD opiera się na mechanizmach uwierzytelniania gotowych do użycia w Internecie, takich jak SAML, OAuth i OpenID Connect. Istniejące obciążenia, które są zależne od metody uwierzytelniania w starszej wersji z użyciem protokołów takich jak Kerberos lub NTLM, mogą wymagać zrefaktoryzowania przed migracją do chmury przy użyciu wzorca punktu odniesienia chmury.

> [!TIP]
> Całkowita migracja usług zarządzania tożsamościami do usługi Azure AD eliminuje potrzebę utrzymywania własnej infrastruktury tożsamości, znaczne upraszczając zarządzanie zasobami IT.
>
> Jednak usługa Azure AD nie zastępuje w pełni tradycyjnej infrastruktury usługi Active Directory. Funkcje katalogu, takie jak metody uwierzytelniania ze starszej wersji, zarządzanie komputerami lub zasady grupy, mogą nie być dostępne bez konieczności wdrożenia dodatkowych narzędzi lub usług w chmurze.
>
> W przypadku scenariuszy, w których konieczna jest integracja lokalnej usługi tożsamości lub usług domenowych z wdrożeniami chmury, zapoznaj się z zagadnieniami synchronizacji katalogów i wzorców usług domenowych hostowanych w chmurze, które omówiono poniżej.

### <a name="directory-synchronization"></a>Synchronizacja katalogów

W przypadku organizacji z istniejącą lokalną infrastrukturą usługi Active Directory synchronizacja katalogów jest często najlepszym rozwiązaniem mającym na celu zachowanie istniejących użytkowników i zarządzanie dostępem przy jednoczesnym zapewnieniu wymaganych możliwości zarządzania tożsamościami i dostępem do zarządzania zasobami w chmurze. Ten proces stale replikuje informacje o katalogu między usługami Azure AD i lokalnymi usługami katalogowymi, umożliwiając wspólne poświadczenia dla użytkowników i spójny system tożsamości, roli i uprawnień w całej organizacji.

> [!NOTE]
> Organizacje, które zaadaptowały usługi Office 365, mogły już wdrożyć [synchronizację katalogów](https://docs.microsoft.com/office365/enterprise/set-up-directory-synchronization) między ich lokalną infrastrukturą usługi Active Directory i usługą Azure Active Directory.

**Założenia dotyczące synchronizacji katalogów:** Korzystanie z rozwiązania do obsługi zsynchronizowanych tożsamości obejmuje następujące założenia:

- Należy utrzymywać wspólny zestaw kont użytkowników i grup w chmurze oraz w obrębie lokalnej infrastruktury IT.
- Lokalne usługi zarządzania tożsamościami obsługują replikację za pomocą usługi Azure AD.

> [!TIP]
> Wszelkie obciążenia oparte na chmurze, które zależą od mechanizmów uwierzytelniania w starszej wersji udostępnianych przez serwery usługi Active Directory w środowisku lokalnym i które nie są obsługiwane przez usługę Azure AD, nadal będą wymagać łączności z usługami domenowymi w środowisku lokalnym lub z serwerami wirtualnymi w środowisku chmury, które udostępnia te usługi. Używanie usług zarządzania tożsamościami w środowisku lokalnym wprowadza również zależności dla łączności między sieciami w chmurze i lokalnymi.

### <a name="cloud-hosted-domain-services"></a>Usługi domenowe hostowane w chmurze

Jeśli masz obciążenia, które są zależne od uwierzytelniania opartego na oświadczeniach z wykorzystaniem starszych protokołów, takich jak Kerberos lub NTLM, a obciążeń tych nie można refaktoryzować w celu akceptowania nowoczesnych protokołów uwierzytelniania, takich jak SAML lub OAuth i OpenID Connect, konieczna może być migracja niektórych usług domenowych do chmury jako część wdrożenia w chmurze.

Ten wzorzec obejmuje wdrażanie maszyn wirtualnych z usługą Active Directory w sieciach wirtualnych opartych na chmurze w celu zapewnienia usług Active Directory Domain Services (AD DS) dla zasobów w chmurze. Wszelkie istniejące aplikacje i usługi migrowane do sieci w chmurze powinny mieć możliwość używania tych serwerów katalogów hostowanych w chmurze za pomocą drobnych zmian.

Prawdopodobnie istniejące katalogi i usługi domenowe nadal będą używane w środowisku lokalnym. W tym scenariuszu zalecane jest także używane synchronizacji katalogów w celu zapewnienia wspólnego zestawu użytkowników i ról w środowisku w chmurze i lokalnym.

**Założenia dotyczące usług domenowych hostowanych w chmurze:** Wykonywanie migracji katalogu obejmuje następujące założenia:

- Obciążenia zależą od uwierzytelniania opartego na oświadczeniach z wykorzystaniem protokołów takich jak Kerberos lub NTLM.
- Obciążenia maszyn wirtualnych muszą być przyłączone do domeny w celu zarządzania lub stosowania zasad grupy usługi Active Directory.

> [!TIP]
> Migracja katalogu połączona z usługami domenowymi hostowanymi w chmurze zapewnia dużą elastyczność podczas migrowania istniejących obciążeń, lecz hosting maszyn wirtualnych w ramach sieci wirtualnej w chmurze w celu dostarczenia tych usług zwiększa złożoność zadań działu IT dotyczących zarządzania. W miarę dojrzewania środowiska migracji do chmury należy sprawdzić długoterminowe wymagania w zakresie hostowania tych serwerów. Należy rozważyć, czy refaktoryzacja istniejących obciążeń na potrzeby zapewnienia zgodności z dostawcami tożsamości w chmurze, takimi jak usługa Azure Active Directory, może zmniejszyć zapotrzebowanie na serwery hostowane w chmurze.

### <a name="active-directory-federation-services"></a>Usługi Active Directory Federation Services

Federacja tożsamości ustanawia relacje zaufania w wielu systemach zarządzania tożsamościami w celu zapewnienia typowych możliwości uwierzytelniania i autoryzacji. Następnie można obsługiwać możliwości logowania jednokrotnego w wielu domenach w ramach organizacji lub systemów tożsamości zarządzanych przez klientów lub partnerów biznesowych.

Usługa Azure AD obsługuje federację domen usługi Active Directory w środowisku lokalnym za pomocą usług [Active Directory Federation Services (AD FS)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-fed-whatis). Aby uzyskać więcej informacji na temat sposobu wdrażania tego rozwiązania na platformie Azure, zobacz [Rozszerzanie usług AD FS na platformę Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs).

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat usługi zarządzania tożsamościami na platformie Azure, zobacz:

- **[Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis).** Usługa Azure AD dostarcza usługi zarządzania tożsamościami oparte na chmurze. Umożliwia zarządzanie dostępem do zasobów platformy Azure i kontrolę zarządzania tożsamościami, rejestrację urządzeń, inicjowanie obsługi użytkowników, kontrolę dostępu do aplikacji i ochronę danych.
- **[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity).** Narzędzie Azure AD Connect umożliwia łączenie wystąpień usługi Azure AD z istniejącymi rozwiązaniami zarządzania tożsamościami, umożliwiając synchronizację istniejącego katalogu w chmurze.
- **[Kontrola dostępu na podstawie ról (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview).** Usługa Azure AD zapewnia kontrolę RBAC w celu efektywnego i bezpiecznego zarządzania dostępem do zasobów na płaszczyźnie zarządzania. Zadania i obowiązki są zorganizowane w role, do których są przypisani użytkownicy. Funkcja RBAC umożliwia kontrolę nad tym, kto ma dostęp do zasobów oraz jakie działania użytkownik może wykonywać na takich zasobach.
- **[Azure AD Privileged Identity Management (PIM)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure).** Usługa PIM obniża czas ekspozycji uprawnień dostępu do zasobów i zwiększa widoczność korzystania z nich dzięki raportom i alarmom. Ogranicza przypadki podejmowania przez użytkowników uprawnień dokładnie na czas (JIT, just in time) lub nadawania uprawnień na krótszy czas, po którym uprawnienia są automatycznie odbierane.
- **[Integrowanie lokalnych domen usługi Active Directory z usługą Azure Active Directory](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad).** Ta architektura referencyjna zawiera przykład synchronizacji katalogów między domenami usługi Active Directory w środowisku lokalnym i usługą Azure AD.
- **[Rozszerzanie usług Active Directory Domain Services (AD DS) na platformę Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain).** Ta architektura referencyjna zawiera przykład wdrażania serwerów usługi AD DS w celu rozszerzenia usług domenowych na zasoby oparte na chmurze.
- **[Rozszerzanie usług Active Directory Federation Services (AD FS) na platformę Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs).** Ta architektura referencyjna przedstawia konfigurację usługi Active Directory Federation Services (AD FS) w celu przeprowadzenia uwierzytelniania federacyjnego i autoryzacji przy użyciu katalogu usługi Azure AD.

## <a name="next-steps"></a>Następne kroki

Tożsamość to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury, zobacz [Omówienie przewodników dotyczących podejmowania decyzji](../index.md).

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
