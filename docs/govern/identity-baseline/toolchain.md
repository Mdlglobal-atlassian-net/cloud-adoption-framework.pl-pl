---
title: Narzędzia linii bazowej tożsamości na platformie Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Narzędzia linii bazowej tożsamości na platformie Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 72060f16add37d62a4747c5fe9d5aef49fe04c58
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222123"
---
# <a name="identity-baseline-tools-in-azure"></a>Narzędzia linii bazowej tożsamości na platformie Azure

[Linia bazowa tożsamości](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na sposobach ustanawiania zasad zapewniających spójność i ciągłość tożsamości użytkowników niezależnie od dostawcy chmury, który obsługuje aplikację lub obciążenie.

Następujące narzędzia są zawarte w przewodniku odnajdywania na tożsamości hybrydowej.

**Active Directory (lokalnie):** Active Directory jest dostawcą tożsamości najczęściej używanym w przedsiębiorstwie do przechowywania i weryfikowania poświadczeń użytkownika.

**Azure Active Directory:** Oprogramowanie jako usługa (SaaS) równoważne Active Directory, które może federowanie z Active Directory lokalnymi.

**Active Directory (IaaS):** Wystąpienie aplikacji Active Directory działającej na maszynie wirtualnej na platformie Azure.

Tożsamość jest płaszczyzną kontroli zabezpieczeń IT. W związku z tym uwierzytelnianie jest ochroną dostępną w organizacji do chmury. Organizacje potrzebują płaszczyzny kontroli tożsamości, która zwiększa bezpieczeństwo i utrzymuje bezpieczeństwo aplikacji w chmurze przed intruzami.

## <a name="cloud-authentication"></a>Uwierzytelnianie w chmurze

Wybór odpowiedniej metody uwierzytelniania to pierwszy problem dotyczący organizacji, które chcą przenieść aplikacje do chmury.

Po wybraniu tej metody usługa Azure AD obsługuje proces logowania użytkowników. W połączeniu z bezproblemowym logowaniem jednokrotnym użytkownicy mogą logować się do aplikacji w chmurze bez konieczności ponownego wprowadzania poświadczeń. Przy użyciu uwierzytelniania w chmurze możesz wybrać jedną z dwóch opcji:

**Synchronizacja skrótów haseł w usłudze Azure AD:** Najprostszy sposób na włączenie uwierzytelniania dla obiektów katalogu lokalnego w usłudze Azure AD. Tej metody można również użyć w połączeniu z dowolną metodą jako kopię zapasową metody uwierzytelniania trybu failover w przypadku awarii serwera lokalnego.

**Uwierzytelnianie przekazywane przez usługę Azure AD:** Zapewnia trwałe sprawdzanie poprawności hasła dla usług uwierzytelniania usługi Azure AD przy użyciu agenta oprogramowania działającego na co najmniej jednym serwerze lokalnym.

> [!NOTE]
> W przypadku firm z wymaganiem bezpieczeństwa aby natychmiast wymusić lokalne Stany konta użytkownika, zasady haseł i godziny logowania, należy rozważyć metodę uwierzytelniania przekazywanego.

**Uwierzytelnianie federacyjne:**

Po wybraniu tej metody usługa Azure AD przekaże proces uwierzytelniania do oddzielnego zaufanego systemu uwierzytelniania, takiego jak lokalny Active Directory Federation Services (AD FS) lub zaufanego dostawcę federacyjnego innej firmy, aby sprawdzić poprawność hasła użytkownika.

Artykuł [wybierający właściwą metodę uwierzytelniania dla Azure Active Directory](https://docs.microsoft.com/azure/security/azure-ad-choose-authn) zawiera drzewo decyzyjne ułatwiające wybranie najlepszego rozwiązania dla Twojej organizacji.

Poniższa tabela zawiera listę natywnych narzędzi, które mogą pomóc w przedwczesnej polityce i procesach, które obsługują tę dyscyplinę ładu.

<!-- markdownlint-disable MD033 -->

|Badan|Synchronizacja skrótów haseł + bezproblemowe logowanie jednokrotne|Uwierzytelnianie przekazywane i bezproblemowe logowanie jednokrotne|Federacja z usługami AD FS|
|:-----|:-----|:-----|:-----|
|Gdzie jest wykonywane uwierzytelnianie?|W chmurze|W chmurze po bezpiecznej weryfikacji hasła przy użyciu lokalnego agenta uwierzytelniania|Lokalnie|
|Jakie są wymagania dotyczące serwera lokalnego poza systemem aprowizacji: Azure AD Connect?|Brak|Jeden serwer dla każdego dodatkowego agenta uwierzytelniania|Co najmniej dwa serwery AD FS<br><br>Dwa lub więcej serwerów WAP w sieci obwodowej/strefy DMZ|
|Jakie są wymagania dotyczące lokalnego Internetu i sieci poza systemem aprowizacji?|Brak|[Wychodzący dostęp do Internetu](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-quick-start) z serwerów z uruchomionymi agentami uwierzytelniania|[Przychodzący dostęp do Internetu](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-requirements) do serwerów WAP na obrzeżu<br><br>Dostęp do sieci przychodzącej do serwerów AD FS z serwerów WAP na obrzeżu<br><br>Równoważenie obciążenia sieciowego|
|Czy istnieje wymagania dotyczące certyfikatu SSL?|Nie|Nie|Tak|
|Czy istnieje rozwiązanie do monitorowania kondycji?|Niewymagana|Stan agenta udostępniany przez [Centrum administracyjne Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication)|[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)|
|Czy użytkownicy uzyskują Logowanie jednokrotne do zasobów w chmurze z urządzeń przyłączonych do domeny w sieci firmowej?|Tak, aby [bezproblemowe logowanie](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) jednokrotne|Tak, aby [bezproblemowe logowanie](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) jednokrotne|Tak|
|Jakie typy logowania są obsługiwane?|UserPrincipalName + hasło<br><br>Zintegrowane uwierzytelnianie systemu Windows za pomocą bezproblemowego [logowania](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) jednokrotnego<br><br>[Alternatywny identyfikator logowania](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-custom)|UserPrincipalName + hasło<br><br>Zintegrowane uwierzytelnianie systemu Windows za pomocą bezproblemowego [logowania](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) jednokrotnego<br><br>[Alternatywny identyfikator logowania](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-faq)|UserPrincipalName + hasło<br><br>sAMAccountName + hasło<br><br>Zintegrowane uwierzytelnianie systemu Windows<br><br>[Certyfikat i uwierzytelnianie karty inteligentnej](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)<br><br>[Alternatywny identyfikator logowania](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)|
|Czy funkcja Windows Hello dla firm jest obsługiwana?|[Model zaufania kluczy](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model zaufania certyfikatów z usługą Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Model zaufania kluczy](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model zaufania certyfikatów z usługą Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Model zaufania kluczy](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Model zaufania certyfikatów](/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs)|
|Jakie są opcje usługi uwierzytelniania wieloskładnikowego?|[Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Formanty niestandardowe z dostępem warunkowym *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Formanty niestandardowe z dostępem warunkowym *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Serwer usługi Azure MFA](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfaserver-deploy)<br><br>[Uwierzytelnianie wieloskładnikowe innej firmy](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)<br><br>[Formanty niestandardowe z dostępem warunkowym *](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|
|Jakie Stany kont użytkowników są obsługiwane?|Wyłączone konta<br>(opóźnienie do 30 minut)|Wyłączone konta<br><br>Konto zablokowane<br><br>Konto wygasło<br><br>Hasło wygasło<br><br>Godziny logowania|Wyłączone konta<br><br>Konto zablokowane<br><br>Konto wygasło<br><br>Hasło wygasło<br><br>Godziny logowania|
|Jakie są opcje dostępu warunkowego?|[Dostęp warunkowy usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Dostęp warunkowy usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Dostęp warunkowy usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)<br><br>[AD FS regułami dotyczącymi roszczeń](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator)|
|Czy blokowane są obsługiwane starsze protokoły?|[Tak](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Tak](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Tak](/windows-server/identity/ad-fs/operations/access-control-policies-w2k12)|
|Czy można dostosować logo, obraz i opis na stronach logowania?|[Tak, z Azure AD — wersja Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Tak, z Azure AD — wersja Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Tak](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo)|
|Jakie zaawansowane scenariusze są obsługiwane?|[Blokada hasła inteligentnego](https://docs.microsoft.com/azure/active-directory/active-directory-secure-passwords)<br><br>[Raporty dotyczące przecieków poświadczeń](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events)|[Blokada hasła inteligentnego](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout)|System uwierzytelniania z wieloma opóźnieniami w wielu lokacjach<br><br>[Blokada AD FS ekstranetu](/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection)<br><br>[Integracja z systemami tożsamości innych firm](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility)|

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Kontrolki niestandardowe w dostępie warunkowym usługi Azure AD nie obsługują obecnie rejestracji urządzeń.

## <a name="next-steps"></a>Następne kroki

[Oficjalny dokument struktury cyfrowej transformacji tożsamości](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html?LCID=EN-US) zawiera opis kombinacji i rozwiązań do wyboru i integracji każdego z tych składników.

[Narzędzie Azure AD Connect](https://aka.ms/aadconnectwiz) ułatwia integrację katalogów lokalnych z usługą Azure AD.
