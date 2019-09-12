---
title: Najlepsze rozwiązania dotyczące zabezpieczania obciążeń migrowanych na platformę Azure i zarządzania nimi
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Po przeprowadzeniu migracji na platformę Azure należy zapoznać się z najlepszymi rozwiązaniami dotyczącymi obsługi i zabezpieczania zmigrowanych obciążeń oraz zarządzania nimi.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b7d2ac8d624115c9d843ded8a045cd68f4050650
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70825863"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące zabezpieczania i zarządzania nimi obciążeń migracji na platformę Azure

Jako użytkownik planowania i projektowania dotyczące migracji, oprócz myśleć o migracji, należy wziąć pod uwagę modelu zabezpieczeń i zarządzania na platformie Azure po migracji. W tym artykule opisano planowania oraz najlepsze rozwiązania dotyczące zabezpieczania wdrożenie systemu Azure, po przeprowadzeniu migracji i bieżących zadań Zachowaj uruchomiony pracę na optymalnym poziomie wdrożenia.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisanych w tym artykule opierają się na platformie Azure oraz z funkcji dostępnych w momencie pisania. Funkcje i możliwości zmiany w czasie.

## <a name="secure-migrated-workloads"></a>Zabezpieczanie zmigrowanych obciążeń

Po zakończeniu migracji najważniejszych zadań jest zabezpieczanie zmigrowanych obciążeń przed zagrożeniami wewnętrznymi i zewnętrznymi. Poniższe najlepsze rozwiązania ułatwiają osiągnięcie tego celu:

- [Praca z usługą Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Dowiedz się, jak korzystać z monitorowania, ocen i zaleceń udostępnianych w usłudze Azure Security Center.
- [Szyfrowanie danych](#best-practice-encrypt-data): Poznaj najlepsze rozwiązania dotyczące szyfrowania danych na platformie Azure.
- [Konfigurowanie oprogramowania chroniącego przed złośliwym kodem](#best-practice-protect-vms-with-antimalware): Chroń maszyny wirtualne przed złośliwym oprogramowaniem i złośliwymi atakami.
- [Zabezpieczanie aplikacji internetowych](#best-practice-secure-web-apps): Zabezpiecz poufne informacje w zmigrowanych aplikacjach internetowych.
- [Przegląd subskrypcji](#best-practice-review-subscriptions-and-resource-permissions): Sprawdź, kto może uzyskać dostęp do subskrypcji i zasobów platformy Azure po migracji.
- [Praca z dziennikami](#best-practice-review-audit-and-security-logs): Regularnie przeglądaj dzienniki inspekcji i zabezpieczeń platformy Azure.
- [Przegląd innych funkcji zabezpieczeń](#best-practice-evaluate-other-security-features): Poznaj i oceń zaawansowane funkcje zabezpieczeń oferowane przez platformę Azure.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Najlepsze rozwiązanie: Postępowanie zgodnie z zaleceniami usługi Azure Security Center

Firma Microsoft dokłada wszelkich starań w celu zapewnienia, że administratorzy dzierżawy platformy Azure mają informacje konieczne do włączenia funkcji zabezpieczeń chroniących obciążenia przed atakami. Usługa Azure Security Center zapewnia ujednolicone zarządzanie zabezpieczeniami. W Centrum zabezpieczeń można stosować zasady zabezpieczeń na potrzeby różnych obciążeń, ograniczania ujawniania zagrożenia i wykrywanie oraz reagowanie na ataki. Usługa Security Center analizuje zasobów i konfiguracje dla dzierżaw usługi Azure i sprawia, że zalecenia dotyczące zabezpieczeń, w tym:

- **Scentralizowane zarządzanie zasadami** — zapewnianie zgodności z firmowymi lub prawnymi wymaganiami dotyczącymi zabezpieczeń przez centralne zarządzanie zasadami zabezpieczeń we wszystkich obciążeniach chmury hybrydowej.
- **Ciągła ocena zabezpieczeń** — monitorowanie poziomu bezpieczeństwa maszyn, sieci, magazynu i usług danych oraz aplikacji pod kątem potencjalnych problemów z zabezpieczeniami.
- **Praktyczne zalecenia** — korygowanie luk w zabezpieczeniach, zanim zostaną wykorzystane przez osoby atakujące, dzięki zaleceniom dotyczącym zabezpieczeń z określonymi priorytetami i możliwością wykonywania akcji.
- **Alerty i zdarzenia uszeregowane według priorytetów** — zdarzenia i alerty zabezpieczeń uszeregowane według priorytetów pozwalają koncentrować się najpierw na krytycznych zagrożeniach.

Oprócz ocen i zaleceń usługa Azure Security Center udostępnia inne funkcje zabezpieczeń, które mogą zostać włączone dla określonych zasobów.

- **Dostęp just-in-time (JIT).** Zmniejsz obszar podatny na ataki sieciowe za pomocą funkcji just-in-time zapewniającej kontrolowany dostęp do portów zarządzania na maszynach wirtualnych platformy Azure.
  - Gdy w Internecie jest otwarty port RDP 3389 maszyny wirtualnej, naraża on ją na stałe działania złośliwego użytkownika. Azure adresy IP są dobrze znane i hakerów stale sondować ich atakom na otwarte porty 3389.
  - Po prostu w zabezpieczeń sieci w czasie używa grup (NSG) i przychodzące zasady tego limitu ilość czasu, który określony port jest otwarty.
  - Przy użyciu dokładnie na czas włączone, usługa Security Center sprawdza, czy użytkownik ma uprawnienia dostępu zapisu kontroli dostępu opartej na rolach dla maszyny Wirtualnej. Ponadto można określić zasady, w jaki sposób użytkownicy mogą łączyć się maszyn wirtualnych. Jeśli uprawnienia są poprawne, żądanie dostępu zostanie zatwierdzone i usługi Security Center konfiguruje sieciowych grup zabezpieczeń, aby zezwolić na ruch przychodzący do wybranych portów ilości czasu można określić. Po upływie tego czasu sieciowe grupy zabezpieczeń powrócą do poprzedniego stanu.
- **Funkcje adaptacyjnego sterowania aplikacjami.** Zapobiegaj działaniu oprogramowania i złośliwego oprogramowanie na maszynach wirtualnych, kontrolując uruchamiane na nich aplikacje przy użyciu dynamicznych list dozwolonych.
  - Funkcje adaptacyjnego sterowania aplikacjami umożliwiają zatwierdzanie aplikacji i zapobiegają instalowaniu niezatwierdzonych lub niesprawdzonych aplikacji na maszynach wirtualnych przez nieautoryzowanych użytkowników lub administratorów.
    - Możesz blokować próby uruchomienia złośliwych aplikacji lub generować alerty z tym związane, unikać niechcianych lub złośliwych aplikacji oraz zapewniać zgodność z zasadami zabezpieczeń aplikacji w organizacji.
- **Monitorowanie integralności plików.** Zapewnij integralność plików działających na maszynach wirtualnych.
  - Nie tylko instalowanie oprogramowania powoduje problemy z maszyną wirtualną. Modyfikacja pliku systemowego może spowodować obniżenie wydajności lub niepowodzenia maszyny Wirtualnej. Plik integralności monitorowanie sprawdza, czy pliki systemowe i ustawienia rejestru dotyczące zmian i powiadamia, jeśli coś jest zaktualizowane.
  - Zaleceniem usługi Security Center, które pliki powinny monitorować.

**Dowiedz się więcej:**

- [Dowiedz się więcej](/azure/security-center/security-center-intro) o usłudze Azure Security Center.
- [Dowiedz się więcej](/azure/security-center/security-center-just-in-time) o tylko dostęp do maszyny Wirtualnej w czasie.
- [Dowiedz się więcej o](/azure/security-center/security-center-adaptive-application) stosowanie funkcje adaptacyjnego sterowania aplikacjami.
- [Rozpoczynanie pracy](/azure/security-center/security-center-file-integrity-monitoring) z monitorowaniem integralności plików.

## <a name="best-practice-encrypt-data"></a>Najlepsze rozwiązanie: Szyfrowanie danych

Szyfrowanie jest ważnym elementem najlepszych rozwiązań dotyczących zabezpieczeń na platformie Azure. Zapewnienie włączonego szyfrowania na wszystkich poziomach pozwala zapobiec uzyskaniu dostępu do poufnych danych przez nieuprawnione strony. Dotyczy to danych przesyłanych i magazynowanych.

### <a name="encryption-for-iaas"></a>Szyfrowanie na potrzeby usług IaaS

- **Maszyny wirtualne:** W przypadku maszyn wirtualnych możesz użyć usługi Azure Disk Encryption do zaszyfrowania dysków maszyn wirtualnych IaaS z systemem Windows i Linux.
  - Ta usługa korzysta z funkcji BitLocker dla systemu Windows oraz funkcji DM-Crypt dla systemu Linux, aby zapewnić szyfrowanie woluminów dysków systemu operacyjnego i danych.
  - Możesz użyć klucza szyfrowania utworzonego przez platformę Azure lub podać własne klucze szyfrowania chronione w usłudze Azure Key Vault.
  - Za pomocą szyfrowania dysku danych maszyny Wirtualnej IaaS jest zabezpieczona na poziomie rest (operacja na dysku) i podczas rozruchu maszyny Wirtualnej.
    - Usługa Azure Security Center wygeneruje alert, jeśli będą istnieć niezaszyfrowane maszyny wirtualne.
- **Usługa Storage:** Chroń dane przechowywane w usłudze Azure Storage.
  - Dane przechowywane na kontach usługi Azure Storage można zaszyfrować przy użyciu wygenerowanych przez firmę Microsoft kluczy AES zgodnych ze standardem FIPS 140-2 lub przy użyciu własnych kluczy.
  - Szyfrowanie usługi Storage jest włączona dla wszystkich kont magazynu z nowymi i istniejącymi i nie może być wyłączony.

### <a name="encryption-for-paas"></a>Szyfrowanie dla usług PaaS

W przeciwieństwie do usług IaaS, gdzie zarządzasz własnymi maszynami wirtualnymi i infrastrukturą, w modelu PaaS platforma i infrastruktura jest zarządzana przez dostawcę, co pozwala Ci się skupić na podstawowej logice i możliwościach aplikacji. W przypadku tylu różnych typów usług PaaS poszczególne usługi są oceniane indywidualnie pod kątem bezpieczeństwa. Jako przykład sprawdźmy, w jaki sposób możemy włączyć szyfrowanie dla usługi Azure SQL Database.

- **Funkcja Always Encrypted:** Użyj Kreatora funkcji Always Encrypted w programie SQL Server Management Studio, aby chronić dane magazynowane.
  - Klucz funkcji Always Encrypted jest tworzony w celu szyfrowania danych w pojedynczej kolumnie.
  - Zawsze zaszyfrowane klucze mogą być przechowywane w postaci zaszyfrowanej w metadanych bazy danych lub przechowywane w magazynach zaufanych takich jak usługi Azure Key Vault.
  - Aby użyć tej funkcji, prawdopodobnie konieczne będzie wprowadzenie zmian w aplikacji.
- **Szyfrowanie Transparent Data Encryption (TDE):** Chroń bazę danych Azure SQL Database za pomocą szyfrowania i deszyfrowania w czasie rzeczywistym, powiązanych kopii zapasowych i magazynowanych plików dzienników transakcji.
  - Szyfrowanie TDE umożliwia wykonywanie działań szyfrowania bez wprowadzania zmian w warstwie aplikacji.
  - Funkcja TDE można użyć kluczy szyfrowania udostępniana przez firmę Microsoft, lub możesz podać własne klucze przy użyciu własnego klucza obsługi.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/security/azure-security-disk-encryption-overview) usługa Azure Disk Encryption dla maszyn wirtualnych IaaS.
- [Włącz](/azure/security/azure-security-disk-encryption-windows) szyfrowania dla maszyn wirtualnych Windows IaaS.
- [Dowiedz się więcej o](/azure/storage/common/storage-service-encryption) szyfrowanie usługi Azure Storage dla danych magazynowanych.
- [Odczyt](/azure/sql-database/sql-database-always-encrypted-azure-key-vault) z omówieniem funkcji zawsze zaszyfrowane.
- [Przeczytaj o](/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) TDE dla bazy danych Azure SQL.
- [Informacje](/azure/sql-database/transparent-data-encryption-byok-azure-sql) o szyfrowaniu TDE za pomocą usługi Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Najlepsze rozwiązanie: Zabezpieczanie maszyn wirtualnych za pomocą oprogramowania chroniącego przed złośliwym kodem

W przypadku starszych maszyn wirtualnych zmigrowanych na platformę Azure często zdarza się, że nie posiadają one oprogramowania chroniącego przed złośliwym kodem na odpowiednim poziomie. Platforma Azure udostępnia bezpłatne rozwiązanie punktu końcowego, które pomaga chronić maszyny wirtualne przed wirusami, programami szpiegującymi i innym złośliwym oprogramowaniem.

- Microsoft Antimalware dla platformy Azure generuje alerty, gdy wiadomo, że próbuje zainstalować złośliwego lub niechcianego oprogramowania.
- To rozwiązanie jednego agenta, działającego w tle bez interwencji człowieka.
- W usłudze Azure Security Center można łatwo zidentyfikować maszyny wirtualne, które nie program endpoint protection, uruchamianie i instalowanie Microsoft Antimalware, zgodnie z potrzebami.

![Ochrony przed złośliwym kodem dla maszyn wirtualnych](./media/migrate-best-practices-security-management/antimalware.png)
*ochrony przed złośliwym kodem dla maszyn wirtualnych*

**Dowiedz się więcej:**

- [Informacje](/azure/security/azure-security-antimalware) o rozwiązaniu Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Najlepsze rozwiązanie: Zabezpieczanie aplikacji internetowych

Zmigrowanych aplikacji internetowych dotyczy kilka problemów:

- Większość aplikacji sieci web w starszej wersji się zwykle poufnych informacji w plikach konfiguracji. Pliki zawierające informacje takie mogą spowodować problemy z zabezpieczeniami, gdy aplikacje są kopie zapasowe lub w przypadku, gdy kod aplikacji jest zaznaczone pole wyboru do wyewidencjonowane z kontroli źródła.
- Ponadto podczas migrowania aplikacji internetowych znajdujących się na maszynie wirtualnej prawdopodobnie ta maszyna zostanie przeniesiona z sieci lokalnej i środowiska chronionego przez zaporę do środowiska internetowego. Upewnij się, że skonfigurowano rozwiązanie, które spełnia takie same funkcje, jak lokalne zasoby ochrony.

Platforma Azure zapewnia kilka rozwiązań:

- **Usługa Azure Key Vault:** Obecnie deweloperzy aplikacji internetowych podejmują kroki w celu zapewnienia, że poufne informacje nie będą wyciekać z tych plików. Jedną z metod zabezpieczania informacji jest wyodrębnienie ich z plików i umieszczenie w magazynie Azure Key Vault.
  - Możesz używać usługi Key Vault w celu centralizacji przechowywania kluczy tajnych aplikacji i kontrolowanie ich dystrybucji. Pozwala to uniknąć konieczności przechowywania informacji o zabezpieczeniach w plikach aplikacji.
  - Aplikacje mogą bezpiecznie uzyskiwać dostęp do informacji znajdujących się w magazynie przy użyciu identyfikatorów URI bez konieczności używania niestandardowego kodu.
  - Usługa Azure Key Vault pozwala zablokować dostęp za pośrednictwem kontroli zabezpieczeń platformy Azure i bezproblemowo implementować „klucze przerzucane”. Firma Microsoft nie ma wglądu w Twoje dane ani nie może ich wyodrębniać.
- **Funkcja App Service Environment:** Jeśli migrowana aplikacja wymaga dodatkowej ochrony, możesz rozważyć użycie funkcji App Service Environment i zapory aplikacji internetowej do ochrony zasobów tej aplikacji.
  - Funkcja Azure App Service Environment zapewnia w pełni izolowane i dedykowane środowisko, w którym można uruchamiać aplikacje App Service, takie jak aplikacje internetowe systemu Windows i Linux, kontenery platformy Docker, aplikacje mobilne i funkcje.
  - Jest to przydatne w przypadku aplikacji o bardzo dużej skali, wymagających izolacji lub mających duże użycie pamięci.
- **Zapora aplikacji internetowej:** Funkcja usługi Azure Application Gateway, która zapewnia scentralizowaną ochronę aplikacji internetowych.
  - Chroni aplikacje internetowe bez konieczności modyfikowania kodu zaplecza.
  - Zapewnia jednoczesną ochronę wielu aplikacji internetowych za bramą aplikacji.
  - Zapora aplikacji internetowej może być monitorowana przy użyciu usługi Azure Monitor i jest zintegrowana z usługą Azure Security Center.

![Zabezpieczanie aplikacji internetowych](./media/migrate-best-practices-security-management/web-apps.png)

*Usługa Azure Key Vault*

**Dowiedz się więcej:**

- [Omówienie](/azure/key-vault/key-vault-overview) usługi Azure Key Vault.
- [Informacje](/azure/application-gateway/waf-overview) o zaporze aplikacji internetowej.
- [Wprowadzenie](/azure/app-service/environment/intro) do środowisk App Service Environment.
- [Omówienie sposobu](/azure/key-vault/tutorial-web-application-keyvault) konfigurowania aplikacji internetowej w celu odczytywania wpisów tajnych z magazynu Key Vault.
- [Informacje](/azure/application-gateway/waf-overview) o zaporze aplikacji internetowej.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Najlepsze rozwiązanie: Przeglądanie subskrypcji i uprawnień do zasobów

Podczas migrowania obciążeń i uruchamiania ich na platformie Azure pracownicy z dostępem do obciążeń wykonują różne zadania. Zespół ds. zabezpieczeń powinien regularnie przeglądać dostęp do dzierżawy i grup zasobów platformy Azure. Na platformie Azure dostępne są oferty związane z zarządzaniem tożsamościami i zabezpieczeniami kontroli dostępu, co obejmuje kontrolę dostępu na podstawie ról w celu autoryzowania uprawnień dostępu do zasobów platformy Azure.

- Za pomocą kontroli dostępu na podstawie ról przypisywane są uprawnienia dostępu dla podmiotów zabezpieczeń. Podmioty zabezpieczeń reprezentuje użytkowników, grup (zbiór użytkowników), usługi podmiotów zabezpieczeń (tożsamości używane przez aplikacje i usługi), a zarządzane tożsamości (tożsamość usługi Azure Active Directory automatycznie zarządzane przez platformę Azure).
- RBAC można przypisać role do zasad zabezpieczeń, takich jak właściciela, współautora i czytelnika i roli definicje (zbiór uprawnień), które definiują operacje, które mogą być wykonywane przez role.
- Za pomocą kontroli dostępu na podstawie ról można również ustawiać zakresy określające granicę dla roli. Zakres można ustawić na kilku poziomach, na przykład dla grupy zarządzania, subskrypcji, grupy zasobów lub zasobu.
- Upewnij się, że administratorzy z dostępem do platformy Azure mają dostęp tylko do wybranych przez Ciebie zasobów. Jeśli wstępnie zdefiniowane role na platformie Azure nie są wystarczająco szczegółowe, możesz utworzyć role niestandardowe w celu oddzielenia i ograniczenia uprawnień dostępu.

![Kontrola dostępu](./media/migrate-best-practices-security-management/subscription.png)
*kontrola dostępu — IAM*

**Dowiedz się więcej:**

- [Temat](/azure/role-based-access-control/overview) RBAC.
- [Dowiedz się,](/azure/role-based-access-control/role-assignments-portal) zarządzanie dostępem przy użyciu RBAC i witryny Azure portal.
- [Informacje](/azure/role-based-access-control/custom-roles) o rolach niestandardowych.

## <a name="best-practice-review-audit-and-security-logs"></a>Najlepsze rozwiązanie: Przeglądanie dzienników inspekcji i zabezpieczeń

Usługa Azure Active Directory (Azure AD) udostępnia dzienniki aktywności, które są wyświetlane w usłudze Azure Monitor. W dziennikach przechwytywane są operacje wykonywane w ramach dzierżawy platformy Azure wraz z datą ich przeprowadzenia oraz wykonawcą.

- Dzienniki inspekcji wyświetlanie historii zadań w ramach dzierżawy. Działania logowania rejestruje show, który wykonuje zadania.
- Dostęp do raportów zabezpieczeń zależy od licencji usługi Azure AD. W wersjach Bezpłatna i Podstawowa otrzymujesz listę ryzykownych użytkowników i logowań. W wersjach Premium 1 i Premium 2 otrzymujesz podstawowe informacje o zdarzeniach.
- Dzienniki aktywności możesz kierować do różnych punktów końcowych w celu długoterminowego przechowywania i wglądu w dane.
- Staraj się regularnie przeglądać dzienniki lub zintegruj narzędzia do zarządzania informacjami i zdarzeniami zabezpieczeń (SIEM, security information and event management) w celu automatycznego przeglądania nieprawidłowości. Jeśli nie używasz Premium 1 lub 2, należy wykonać analizy samodzielnie, lub korzystając z systemu SIEM. Analiza obejmuje wyszukiwanie ryzykownych logowań i zdarzeń oraz innych wzorców ataków użytkowników.

![Użytkownicy i grupy](./media/migrate-best-practices-security-management/azure-ad.png)

*Użytkownicy i grupy usługi AAD*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) Dzienniki aktywności usługi Azure AD w usłudze Azure Monitor.
- [Informacje o sposobie](/azure/active-directory/reports-monitoring/concept-audit-logs) przeprowadzania inspekcji raportów aktywności w portalu usługi Azure AD.

## <a name="best-practice-evaluate-other-security-features"></a>Najlepsze rozwiązanie: Ocenianie innych funkcji zabezpieczeń

Platforma Azure udostępnia inne funkcje zabezpieczeń, które zapewniają zaawansowane opcje ochrony. Niektóre z tych najlepszych rozwiązań wymagają licencji na dodatki i opcji premium.

- **Zaimplementuj jednostki administracyjne usługi Azure AD.** Delegowanie obowiązków administracyjnych do pracowników działu pomocy technicznej może być skomplikowane przy użyciu jedynie podstawowej kontroli dostępu platformy Azure. Umożliwienie pracownikom działu pomocy technicznej dostępu do wszystkich grup w usłudze Azure AD może nie być idealnym podejściem w kontekście zabezpieczeń organizacji. Za pomocą funkcji Aktualizacje automatyczne umożliwia oddzielenie czynności związanych z zasobami platformy Azure do kontenerów w podobny sposób jak w środowisku lokalnym jednostki organizacyjne (OU). Do korzystania z jednostki analizy użycia AU administratora musi mieć licencję usługi Azure AD premium. [Dowiedz się więcej](/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Użyj uwierzytelniania wieloskładnikowego.** Jeśli masz licencję usługi Azure AD w warstwie Premium, możesz włączyć i wymusić uwierzytelnianie wieloskładnikowe na kontach administratorów. Wyłudzanie informacji jest najpopularniejszym sposobem naruszania zabezpieczeń poświadczeń kont. Gdy złośliwy użytkownik ma poświadczenia konta administratora, nie ma możliwości zatrzymywania go przed wykonaniem mających poważne konsekwencje akcji, takich jak usunięcie wszystkich grup zasobów. Uwierzytelnianie wieloskładnikowe można ustanowić na kilka sposobów, w tym za pomocą poczty e-mail, aplikacji uwierzytelniania i wiadomości SMS. Jako administrator możesz wybrać najmniej natarczywą opcję. Uwierzytelnianie wieloskładnikowe integruje się z funkcją analizy zagrożeń i zasadami dostępu warunkowego w celu losowego wymagania odpowiedzi na wyzwanie uwierzytelniania wieloskładnikowego. Dowiedz się więcej o [wskazówkach dotyczących zabezpieczeń](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) oraz o [sposobie konfigurowania uwierzytelniania wieloskładnikowego](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Zaimplementuj dostęp warunkowy.** W większości małych i średnich organizacji administratorzy platformy Azure i zespół pomocy technicznej prawdopodobnie znajdują się w jednej lokalizacji geograficznej. W takim przypadku większość nazw logowań będzie pochodzić z tych samych obszarów. Jeśli adresy IP tych lokalizacji są dość statyczne, logiczne jest, że nazwy logowania administratorów nie będą pochodzić spoza tych obszarów. Nawet w przypadku, gdy zdalny złośliwy użytkownik narusza poświadczenia administratora, możesz zaimplementować funkcje zabezpieczeń, takie jak dostęp warunkowy połączony z uwierzytelnianiem wieloskładnikowym, aby zapobiec logowaniu z lokalizacji zdalnych lub sfałszowanych lokalizacji z losowych adresów IP. [Dowiedz się więcej](/azure/active-directory/conditional-access/overview) o dostępie warunkowym i [przejrzyj najlepsze rozwiązania](/azure/active-directory/conditional-access/best-practices) dotyczące dostępu warunkowego w usłudze Azure AD.
- **Przejrzyj uprawnienia aplikacji dla przedsiębiorstw.** W miarę upływu czasu administratorzy wybierają linki firmy Microsoft i innych firm bez znajomości ich wpływu na organizację. Linki mogą zawierać ekrany zgody, na których przypisywane są uprawnienia do aplikacji platformy Azure, i mogą zezwalać na dostęp do odczytu danych usługi Azure AD lub nawet pełny dostęp do zarządzania całą subskrypcją platformy Azure. Należy regularnie przeglądać aplikacje, którym administratorzy i użytkownicy zezwolili na dostęp do zasobów platformy Azure. Upewnij się, że te aplikacje mają tylko wymagane uprawnienia. Dodatkowo co kwartał lub półrocze możesz wysyłać wiadomość e-mail do użytkowników z linkiem do stron aplikacji, aby pamiętali oni o aplikacjach, którym zezwolili na dostęp do danych organizacji. [Dowiedz się więcej](/azure/active-directory/manage-apps/application-types) o typach aplikacji i [sposobu kontrolowania](/azure/active-directory/manage-apps/remove-user-or-group-access-portal) przypisań aplikacji w usłudze Azure AD.

## <a name="managed-migrated-workloads"></a>Zarządzane zmigrowanych obciążeń

W tej sekcji zalecimy niektóre najlepsze rozwiązania dotyczące zarządzania platformą Azure, co obejmuje:

- [Zarządzanie zasobami](#best-practice-name-resource-groups): Najlepsze rozwiązania dotyczące grup zasobów i zasobów platformy Azure, w tym nazwy inteligentne, zapobieganie przypadkowemu usunięciu, zarządzanie uprawnieniami zasobów i efektywne tagowanie zasobów.
- [Korzystanie ze strategii](#best-practice-implement-blueprints): Zapoznaj się z krótkim omówieniem dotyczącym korzystania ze strategii w celu tworzenia środowisk wdrażania i zarządzania nimi.
- [Przegląd architektury](#best-practice-review-azure-reference-architectures): Zapoznaj się z przykładowymi architekturami platformy Azure zawierającymi informacje przydatne podczas tworzenia wdrożeń po migracji.
- [Konfigurowanie grup zarządzania](#best-practice-manage-resources-with-azure-management-groups): Jeśli masz wiele subskrypcji, możesz zebrać je w grupach zarządzania i zastosować ustawienia nadzoru względem tych grup.
- [Konfigurowanie zasad dostępu](#best-practice-deploy-azure-policy): Zastosuj zasady zgodności względem zasobów platformy Azure.
- [Implementowanie strategii BCDR](#best-practice-implement-a-bcdr-strategy): Utwórz strategię ciągłości działania i odzyskiwania po awarii (BCDR, business continuity and disaster recovery), aby zapewnić bezpieczeństwo danych, odporność środowiska i działanie zasobów w przypadku wystąpienia awarii.
- [Zarządzanie maszynami wirtualnymi](#best-practice-use-managed-disks-and-availability-sets): Grupuj maszyny wirtualne w grupach dostępności w celu zapewnienia odporności i wysokiej dostępności. Używaj dysków zarządzanych, aby ułatwić zarządzanie dyskami i magazynami maszyn wirtualnych.
- [Monitorowanie użycia zasobów](#best-practice-monitor-resource-usage-and-performance): Włącz rejestrowanie diagnostyczne dla zasobów platformy Azure, twórz alerty i podręczniki na potrzeby aktywnego rozwiązywania problemów oraz korzystaj z pulpitu nawigacyjnego platformy Azure w celu uzyskania jednolitego wglądu w kondycję i stan wdrożenia.
- [Zarządzanie pomocą techniczną i aktualizacjami](#best-practice-manage-updates): Zapoznaj się z planem pomocy technicznej platformy Azure i sposobem jego implementowania, uzyskaj najlepsze rozwiązania dotyczące zapewniania aktualizacji maszyn wirtualnych oraz odpowiednio ustaw procesy w celu zarządzania zmianami.

## <a name="best-practice-name-resource-groups"></a>Najlepsze rozwiązanie: Nazywanie grup zasobów

Zapewnienie, że grupy zasobów mają znaczące nazwy, które mogą zostać łatwo rozpoznane przez administratorów i członków zespołu pomocy technicznej i po których mogą się oni łatwo poruszać, w znaczący sposób zwiększy produktywność i wydajność.

- Zalecamy stosowanie konwencji nazewnictwa platformy Azure.
- W przypadku synchronizowania lokalnej usługi Active Directory z usługą Azure AD przy użyciu programu Azure AD Connect należy rozważyć dopasowanie nazw lokalnych grup zabezpieczeń do nazw grup zasobów na platformie Azure.

![Nadawanie nazw](./media/migrate-best-practices-security-management/naming.png)

*Nazewnictwo grup zasobów*

**Dowiedz się więcej:**

- [Informacje](/azure/architecture/best-practices/naming-conventions) o konwencji nazewnictwa.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Najlepsze rozwiązanie: Implementowanie blokad usuwania dla grup zasobów

Zniknięcie grupy zasobów z powodu przypadkowego usunięcia jest bardzo niekorzystne. Zalecamy zaimplementowanie blokad usuwania, aby nie miało to miejsca.

![Usuwanie blokad](./media/migrate-best-practices-security-management/locks.png)

*Usuwanie blokad*

**Dowiedz się więcej:**

- [Informacje](/azure/azure-resource-manager/resource-group-lock-resources) o blokowaniu zasobów w celu uniemożliwienia nieoczekiwanych zmian.

## <a name="best-practice-understand-resource-access-permissions"></a>Najlepsze rozwiązanie: Informacje o uprawnieniach dostępu do zasobów

Właściciel subskrypcji ma dostęp do wszystkich grup zasobów i zasobów w ramach subskrypcji.

- Dodaj użytkowników oszczędnie do wartościowych przypisania. Zrozumienie konsekwencje tego rodzaju uprawnień jest ważne w ochronie środowiska, bezpieczne i stabilne.
- Upewnij się, że umieść zasoby w odpowiednich zasobach w grupach:
  - Zgodne ze sobą zasobów przy użyciu podobnych cyklu życia. W idealnym przypadku nie powinno być konieczne przejście zasobu, gdy należy usunąć całą grupę zasobów.
  - Zasoby, które obsługują funkcję lub obciążenia powinny być umieszczone razem dla uproszczonego zarządzania.

**Dowiedz się więcej:**

- [Informacje](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) o organizowaniu subskrypcji i grup zasobów.

## <a name="best-practice-tag-resources-effectively"></a>Najlepsze rozwiązanie: Efektywne tagowanie zasobów

W wielu przypadkach użycie tylko nazwy grupy zasobów powiązanej z zasobami nie zapewni wystarczającej ilości metadanych do efektywnej implementacji takich mechanizmów, jak rozliczenia wewnętrzne lub zarządzanie w ramach subskrypcji.

- Najlepszym rozwiązaniem należy użyć tagów usługi Azure można dodać przydatne metadane, które można tworzyć zapytania i zgłoszone.
- Tagi umożliwiają celu logicznego uporządkowania zasobów przy użyciu właściwości zdefiniowanych przez użytkownika. Tagi można zastosować do grupy zasobów lub zasobów bezpośrednio.
- Tagi mogą być stosowane na grupę zasobów lub poszczególnych zasobów. Tagi grupy zasobów nie są dziedziczone przez zasoby w grupie.
- Tagowanie możesz zautomatyzować przy użyciu programu PowerShell lub Azure Automation. Możesz również oznaczyć poszczególne grupy i zasoby. -podejście do tagowania lub samoobsługowe. Jeśli posiadasz system żądania zmian i zarządzania nimi, możesz w łatwy sposób użyć informacji w żądaniu w celu wypełnienia tagów zasobów specyficznych dla firmy.

![Tagowanie](./media/migrate-best-practices-security-management/tagging.png)
*Tagowanie*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/azure-resource-manager/resource-group-using-tags) i tagowania tag ograniczenia.
- [Przegląd](/azure/azure-resource-manager/resource-group-using-tags#powershell) przykłady programu PowerShell i interfejsu wiersza polecenia skonfigurować znakowanie i zastosować znaczniki z grupy zasobów do jej zasobów.
- [Informacje](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) o najlepszych rozwiązaniach dotyczących tagowania na platformie Azure.

## <a name="best-practice-implement-blueprints"></a>Najlepsze rozwiązanie: Implementowanie strategii

Usługę Azure Blueprints można porównać do planu, który pozwala inżynierowi lub architektowi naszkicować parametry projektu. Usługa ta umożliwia architektom chmury i centralnym grupom IT definiowanie powtarzalnego zestawu zasobów platformy Azure, który implementuje standardy, wzorce i wymagania organizacji oraz jest z nimi zgodny. Usługa Azure Blueprints umożliwia zespołom programistów szybkie tworzenie nowych środowisk spełniających wymagania dotyczące zgodności organizacji, które posiadają zestaw wbudowanych składników — takich jak sieć — przyspieszających opracowywanie i dostarczanie.

- Za pomocą strategii można orkiestrować wdrożenia grup zasobów, szablony usługi Azure Resource Manager oraz przypisania zasad i ról.
- Strategie są przechowywane w dystrybuowanej globalnie usłudze Azure Cosmos DB. Obiekty strategii są replikowane w wielu regionach świadczenia usługi Azure. Replikacja zapewnia małe opóźnienia, wysoką dostępność i spójny dostęp do planu, niezależnie od określonego regionu, do którego planu służy do wdrażania zasobów.

**Dowiedz się więcej:**

- [Odczyt](/azure/governance/blueprints/overview) o schematy.
- [Przegląd](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) przykładu strategii służącego do przyspieszenia sztucznej inteligencji w dziedzinie opieki zdrowotnej.

## <a name="best-practice-review-azure-reference-architectures"></a>Najlepsze rozwiązanie: Przegląd architektur referencyjnych na platformie Azure

Tworzenie bezpiecznych, skalowalnych i możliwych do zarządzanych obciążeń na platformie Azure może być czasochłonnym zadaniem. Za pomocą ciągłych zmian może być trudne na bieżąco z różnymi funkcjami dla optymalnego środowiska. Odwołanie do poznania może być przydatne podczas projektowania i Migrowanie obciążeń. Platforma Azure i Azure partnerów utworzone kilka przykładowych architektur referencyjnych dla różnych typów środowisk. Te przykłady są przeznaczone do zapewnienia pojęcia, które może uczyć się od i budowanie na.

Architektury referencyjne są uporządkowane według scenariusza. Zawierają one zalecane praktyki oraz porady dotyczące zarządzania, dostępności, skalowalności i zabezpieczeń.
Funkcja Azure App Service Environment zapewnia w pełni izolowane i dedykowane środowisko, w którym można uruchamiać aplikacje App Service, takie jak aplikacje internetowe systemu Windows i Linux, kontenery platformy Docker, aplikacje mobilne i funkcje. Usługa App Service dodaje możliwości platformy Azure do swojej aplikacji z zabezpieczenia, równoważenie obciążenia, automatycznego skalowania i automatyczne zarządzanie. Możesz również korzystać z zalet funkcji metodyki DevOps, takich jak ciągłe wdrażanie z DevOps platformy Azure i GitHub, Zarządzanie pakietami tymczasowe środowiska, domena niestandardowa i certyfikaty SSL. Usługa App Service jest przydatne w przypadku aplikacji, które wymagają izolacji i bezpiecznego dostępu do sieci i te, które używają wysokiej ilości pamięci i innych zasobów, które chcesz skalować.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/architecture/reference-architectures) architektury referencyjne platformy Azure.
- [Przegląd](/azure/architecture/example-scenario) przykładowych scenariuszy platformy Azure.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Najlepsze rozwiązanie: Zarządzanie zasobami przy użyciu grup zarządzania platformy Azure

Jeśli Twoja organizacja ma wiele subskrypcji, konieczne jest zarządzanie dostępem, zasadami i zgodnością na ich potrzeby. Grupy zarządzania platformy Azure zapewniają poziom zakresu powyżej subskrypcji.

- Subskrypcje są organizowane w kontenerach nazywanych grupami zarządzania, do których należy zastosować swoje warunki nadzoru.
- Wszystkie subskrypcje w grupie zarządzania automatycznie dziedziczą warunki grupy zarządzania.
- Grupy zarządzania zapewniają zarządzanie klasy korporacyjnej na dużą skalę niezależnie od typu subskrypcji.
- Możesz na przykład zastosować zasady grupy zarządzania ograniczające regiony, w których można tworzyć maszyny wirtualne. Te zasady są następnie stosowane względem wszystkich grup zarządzania, subskrypcji i zasobów w ramach tej grupy zarządzania.
- Możesz utworzyć elastyczną strukturę grup zarządzania i subskrypcji w celu organizowania zasobów w hierarchię na potrzeby ujednoliconego zarządzania zasadami i dostępem.

Na poniższym diagramie przedstawiono przykład tworzenia hierarchii dla nadzoru przy użyciu grup zarządzania.

![Grupy zarządzania](./media/migrate-best-practices-security-management/management-groups.png)
*grup zarządzania*

**Dowiedz się więcej:**

- [Dodatkowe informacje](/azure/governance/management-groups/index) o organizowaniu zasobów w grupy zarządzania.

## <a name="best-practice-deploy-azure-policy"></a>Najlepsze rozwiązanie: Wdrażanie usługi Azure Policy

Azure Policy to usługa platformy Azure, która umożliwia tworzenie i przypisywanie zasad oraz zarządzanie nimi.

- Zasady wymuszają różne reguły i efekty dotyczące zasobów, dzięki czemu zasoby te pozostają zgodne ze standardami firmy i umów dotyczących poziomu usług.
- Usługa Azure Policy daje w wyniku skanowania dla osób, które nie są zgodne z zasadami dotyczącymi zasobów.
- Na przykład można utworzyć zasadę, która zezwala na tylko określony rozmiar jednostki SKU dla maszyn wirtualnych w danym środowisku. Usługa Azure Policy oceni tego ustawienia podczas tworzenia i aktualizowania zasobów, a podczas skanowania istniejących zasobów.
- System Azure oferuje wbudowane zasady, które można przypisać lub możesz utworzyć swój własny.

![Usługa Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*usługa Azure Policy*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](/azure/governance/policy/overview) usługi Azure Policy.
- [Informacje](/azure/governance/policy/tutorials/create-and-manage) o tworzeniu zasad i zarządzania nimi w celu wymuszania zgodności.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Najlepsze rozwiązanie: Implementowanie strategii BCDR

Planowanie ciągłości działalności biznesowej i odzyskiwania po awarii (BCDR) jest niezwykle ważnym zadaniem, które należy wykonać w ramach procesu planowania migracji na platformę Azure. W postanowieniach prawnych umowy mogą zawierać klauzulę dotyczącą siły wyższej, która usprawiedliwia niespełnienie zobowiązań ze względu na siłę wyższą, taką jak huragany lub trzęsienia ziemi. Posiadasz jednak również zobowiązania dotyczące możliwości zapewnienia ciągłego działania usług i odzyskania (w razie potrzeby) po awarii. Może to mieć decydujące znaczenie dla przyszłości Twojej firmy.

Ogólnie Twoja strategia BCDR musi obejmować:

- **Tworzenie kopii zapasowych danych:** Jak zapewnić bezpieczeństwo danych, aby można je było w łatwy sposób odzyskać w przypadku wystąpienia awarii.
- **Odzyskiwanie po awarii:** Jak zapewnić odporność i dostępność aplikacji w przypadku wystąpienia awarii.

### <a name="set-up-bcdr"></a>Konfigurowanie strategii BCDR

Podczas migrowania na platformę Azure ważne jest, aby zrozumieć, że chociaż platforma Azure zapewnia te wbudowane funkcje odporności, należy zaprojektować wdrożenie na platformie Azure w taki sposób, aby skorzystać z zalet funkcji i usług platformy Azure zapewniających wysoką dostępność, odzyskiwanie po awarii i tworzenie kopii zapasowych.

- Twoje rozwiązanie BCDR będzie zależeć od celów firmy i używanej strategii wdrażania na platformie Azure. W przypadku wdrożeń w modelu infrastruktura jako usługa (IaaS) i platforma jako usługa (PaaS) stawiane są różne wyzwania względem strategii BCDR.
- Po utworzeniu rozwiązania BCDR powinny być regularnie testowane, aby sprawdzić, czy Twoja strategia jest nadal odpowiednia.

### <a name="back-up-an-iaas-deployment"></a>Tworzenie kopii zapasowej wdrożenia IaaS

W większości przypadków obciążenie lokalne jest wycofywane po migracji, a lokalna strategia tworzenia kopii zapasowych danych musi zostać rozszerzona lub zastąpiona. Jeśli przeprowadzasz migrację całego centrum danych na platformę Azure, konieczne jest zaprojektowanie i zaimplementowanie pełnego rozwiązania do tworzenia kopii zapasowych przy użyciu technologii platformy Azure lub zintegrowanych rozwiązań innych firm.

W przypadku obciążeń uruchomionych w ramach maszyn wirtualnych IaaS platformy Azure należy wziąć pod uwagę następujące rozwiązania:

- **Usługa Azure Backup:** Zapewnia kopie zapasowe spójne na poziomie aplikacji dla maszyn wirtualnych z systemami Windows i Linux.
- **Migawki magazynu:** Tworzy migawki magazynu obiektów blob.

#### <a name="azure-backup"></a>Azure Backup

Usługa Azure Backup tworzy punkty odzyskiwania danych przechowywane w magazynie platformy Azure. Usługa Azure Backup może tworzyć kopie zapasowe dysków maszyn wirtualnych platformy Azure i dane usługi Azure Files (wersja zapoznawcza). Usługa pliki Azure udostępniają udziałów plików w chmurze, dostępne za pośrednictwem protokołu SMB.

Za pomocą usługi Azure Backup można tworzyć kopie zapasowe maszyn wirtualnych na kilka sposobów.

- **Bezpośrednie tworzenie kopii zapasowych na podstawie ustawień maszyny wirtualnej.** Możesz utworzyć kopię zapasową maszyn wirtualnych za pomocą usługi Azure Backup bezpośrednio z poziomu opcji maszyny wirtualnej w witrynie Azure Portal. Możliwe jest tworzenie kopii zapasowej maszyny wirtualnej raz dziennie i przywracanie dysku maszyny wirtualnej w razie potrzeby. Usługa Azure Backup wykonuje migawki danych z uwzględnieniem aplikacji (usługa VSS), a na maszynie wirtualnej nie jest zainstalowany żaden agent.
- **Bezpośrednie tworzenie kopii zapasowych w magazynie usług Recovery Services.** Możesz utworzyć kopię zapasową maszyn wirtualnych IaaS, wdrażając magazyn Recovery Services w usłudze Azure Backup. Zapewnia to pojedynczą lokalizację do śledzenia kopii zapasowych i zarządzania nimi, a także szczegółowe opcje tworzenia kopii zapasowych i przywracania. Kopia zapasowa jest tworzona maksymalnie trzy razy dziennie na poziomie plików/folderów. Nie uwzględnia ona aplikacji, a system Linux nie jest obsługiwany. Zainstaluj agenta usług Microsoft Azure Recovery Services (MARS) na każdej maszynie wirtualnej, dla której chcesz utworzyć kopię zapasową za pomocą tej metody.
- **Ochrona maszyny wirtualnej na serwerze Azure Backup Server.** Serwer Azure Backup Server jest udostępniany bezpłatnie wraz z usługą Azure Backup. Kopia zapasowa maszyny wirtualnej jest tworzona w lokalnym magazynie serwera Azure Backup Server. Następnie wykonywana jest kopia zapasowa serwera Azure Backup Server na platformie Azure w magazynie. Kopia zapasowa uwzględnia aplikację i posiada pełny stopień szczegółowości dotyczący częstotliwości wykonywania kopii zapasowych i przechowywania. Możesz tworzyć kopię zapasową na poziomie aplikacji, na przykład tworząc kopie zapasową programu SQL Server lub SharePoint.

W celu zapewnienia bezpieczeństwa usługa Azure Backup szyfruje dane w locie przy użyciu algorytmu AES 256 i wysyła je za pośrednictwem protokołu HTTPS do platformy Azure. Kopia zapasowa danych magazynowanych na platformie Azure jest szyfrowana przy użyciu [usługi Storage (SSE)](/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) oraz danych do przesyłania i magazynowania.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/backup/backup-introduction-to-azure-backup) poszczególnych typów kopii zapasowych.
- [Planowanie infrastruktury kopii zapasowych](/azure/backup/backup-azure-vms-introduction) maszyn wirtualnych platformy Azure.

#### <a name="storage-snapshots"></a>Migawek magazynu

Maszyny wirtualne platformy Azure są przechowywane jako stronicowe obiekty BLOB w usłudze Azure Storage.

- Migawki przechwytują stan obiektu blob w określonym punkcie w czasie.
- Jako alternatywną metodę tworzenia kopii zapasowych dysków maszyny Wirtualnej platformy Azure możesz migawki obiektów blob storage i skopiować je do innego konta magazynu.
- Możesz skopiować cały obiekt blob, lub użyć migawek przyrostowych kopii — kopiowanie tylko przyrostowe zmiany i zmniejszenia miejsca do magazynowania.
- Jako dodatkowe środki zabezpieczeń aby umożliwić usuwania nietrwałego dla kont usługi blob storage. Po włączeniu tej funkcji usunięty obiekt blob jest oznaczany do usunięcia, ale nie jest natychmiast przeczyszczany. W okresie przejściowym można przywrócić obiekt blob.

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/storage/blobs/storage-blobs-introduction) usługi Azure blob storage.
- [Dowiedz się, jak](/azure/storage/blobs/storage-blob-snapshots) utworzyć migawki obiektu blob.
- [Przejrzyj przykładowy scenariusz](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) dla kopii zapasowej z magazynu obiektów blob.
- [Informacje](/azure/storage/blobs/storage-blob-soft-delete) o usuwaniu nietrwałym.
- [Odzyskiwanie po awarii i wymuszone przechodzenie w tryb failover (wersja zapoznawcza) w usłudze Azure Storage](/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Tworzenie kopii zapasowych przez inne firmy

Ponadto można użyć rozwiązania innych firm do tworzenia kopii zapasowych maszyn wirtualnych platformy Azure i kontenerów magazynów w magazynie lokalnym lub w chmurze innych dostawców. [Dowiedz się w więcej](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) o rozwiązaniach do tworzenia kopii zapasowych w witrynie Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Konfigurowanie odzyskiwania po awarii dla aplikacji IaaS

Oprócz ochrony danych w ramach planowania strategii BCDR należy uwzględnić sposób utrzymywania dostępności aplikacji i obciążeń na wypadek awarii. W przypadku obciążeń uruchomionych w ramach maszyn wirtualnych IaaS platformy Azure i usługi Azure Storage należy wziąć pod uwagę następujące rozwiązania:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Usługa Azure Site Recovery jest podstawowy usługa zapewniających, maszyn wirtualnych platformy Azure może być przełączany w tryb online i aplikacji maszyny Wirtualnej, udostępnionych podczas wystąpienia awarii.

Usługa Site Recovery replikuje maszyny wirtualne z podstawowego do pomocniczego regionu platformy Azure. W przypadku awarii, w trybie Failover maszyny wirtualne z regionu podstawowego, a nadal mieć dostęp do nich jak zwykle w regionie pomocniczym. Gdy awaria zostanie usunięta, maszyny wirtualne mogą powrócić do regionu podstawowego.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Site Recovery*

**Dowiedz się więcej:**

- [Przegląd](/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) scenariuszy odzyskiwania po awarii dla maszyn wirtualnych platformy Azure.
- [Omówienie sposobu](/azure/site-recovery/azure-to-azure-replicate-after-migration) konfigurowania odzyskiwanie po awarii dla maszyny wirtualnej platformy Azure po przeprowadzeniu migracji.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Najlepsze rozwiązanie: Używanie dysków zarządzanych i zestawów dostępności

Platforma Azure używa zestawów dostępności do logicznego grupowania maszyn wirtualnych i izolowania maszyn wirtualnych w zestawie od innych zasobów. Maszyny wirtualne w zestawie dostępności są rozproszone w wielu domenach błędów z oddzielnymi podsystemami w celu ochrony przed awariami lokalnymi. Są także rozproszone w wielu domenach aktualizacji, dzięki czemu nie wszystkie maszyny wirtualne w zestawie są ponownie uruchamiane w tym samym czasie.

Funkcja Dyski zarządzane na platformie Azure upraszcza zarządzanie dyskami maszyn wirtualnych usługi Azure IaaS dzięki zarządzaniu skojarzonymi z tymi dyskami kontami magazynu.

- Zalecamy używanie dysków zarządzanych, jeśli jest to możliwe. Musisz określić typ magazynu, przeznaczonych do użycia i rozmiar dysku, potrzebujesz, a platforma Azure utworzy i zarządza dysku, w tle.
- Możesz również przekonwertować istniejące dyski zarządzane.
- Należy utworzyć maszyny wirtualne w zestawach dostępności w celu zapewnienia wysokiej odporności i dostępności. W przypadku wystąpienia planowanych lub nieplanowanych awarii zestawy dostępności zapewniają, że co najmniej jedna z maszyn wirtualnych w zestawie będzie nadal dostępna.

![Dyski zarządzane](./media/migrate-best-practices-security-management/managed-disks.png)

*Dyski zarządzane*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](/azure/virtual-machines/windows/managed-disks-overview) z dyskami zarządzanymi.
- [Dowiedz się więcej o](/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) konwertowanie dysków zarządzanych.
- [Informacje o sposobie](/azure/virtual-machines/windows/manage-availability) zarządzania dostępnością maszyn wirtualnych z systemem Windows na platformie Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Najlepsze rozwiązanie: Monitorowanie użycia zasobów i wydajności

Możliwe, że Twoje obciążenia zostały już przeniesione na platformę Azure, aby móc skorzystać z jej ogromnych możliwości skalowania. Przenoszenie obciążenia nie oznacza to jednak, że Azure automatycznie wdroży skalowanie bez interwencji użytkownika. Na przykład:

- Jeśli marketingowe organizacji wypycha nowy anons TV, która napędza 300% więcej ruchu, może to spowodować problemy z dostępnością lokacji. Właśnie został zmigrowany obciążenie może napotkać ograniczenia przypisane i awarii.
- Innym przykładem mogą być rozproszone ataki (DDoS) typu "odmowa usługi" na obciążeniu zmigrowane. W takim przypadku nie można skalować, ale aby zapobiec osiągnięciu zasobów źródła ataków.

Tych dwóch przypadkach mają różne metody rozwiązywania, ale obie można na potrzeby szczegółowych informacji o tym, co się dzieje z użycia i monitorowania wydajności.

- Usługa Azure Monitor może pomóc powierzchni te metryki i udostępniać odpowiedzi alerty, automatycznego skalowania, usługa event hubs, logic apps i więcej.
- Oprócz monitorowania platformy Azure, można zintegrować monitorowanie dzienników platformy Azure dla zdarzeń inspekcji i wydajności aplikacji SIEM innych firm.

![Usługa Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*usługa Azure Monitor*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/azure-monitor/overview) usługa Azure Monitor.
- [Uzyskaj wskazówki](/azure/architecture/best-practices/monitoring) do monitorowania i diagnostyki.
- [Dowiedz się więcej o](/azure/architecture/best-practices/auto-scaling) skalowania automatycznego.
- [Informacje o sposobie](/azure/security-center/security-center-export-data-to-siem) kierowania danych platformy Azure do narzędzia SIEM.

## <a name="best-practice-enable-diagnostic-logging"></a>Najlepsze rozwiązanie: Włączanie rejestrowania diagnostycznego

Zasoby platformy Azure generują znaczną liczbę metryk rejestrowania i danych telemetrycznych.

- Domyślnie większość typów zasobów nie ma włączone rejestrowanie diagnostyczne.
- Włączając rejestrowanie diagnostyczne różnych zasobów, wykonywanie zapytań o dane rejestrowania i tworzyć alerty i elementy playbook na jego podstawie.
- Po włączeniu rejestrowania diagnostycznego każdego zasobu mają określone kategorie. Należy wybrać co najmniej jedną kategorię rejestrowania i lokalizację danych dziennika. Dzienniki mogą być wysyłane do konta magazynu, centrum zdarzeń lub dzienników usługi Azure Monitor.

![Rejestrowanie diagnostyczne](./media/migrate-best-practices-security-management/diagnostics.png)
*Rejestrowanie diagnostyczne*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) zbieranie i wykorzystywanie danych dziennika.
- [Informacje](/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema) o tym, co jest obsługiwane podczas rejestrowania diagnostycznego.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Najlepsze rozwiązanie: Konfigurowanie alertów i podręczników

Gdy funkcja rejestrowania diagnostycznego jest włączona dla zasobów platformy Azure, możesz rozpocząć korzystanie z danych rejestrowania w celu tworzenia alertów niestandardowych.

- Alerty aktywnie powiadamiają użytkownika warunki znajdują się w danych monitorowania. Następnie można zgłosić problemy, zanim użytkownicy systemu, zwróć uwagę, ich. Może generować alerty na elementów, takich jak wartości metryk, zapytań funkcji przeszukiwania dzienników, zdarzenia dziennika aktywności, kondycji platformy i dostępności witryny sieci Web.
- Gdy alerty są wyzwalane, można uruchomić elementu Playbook aplikacji logiki. Podręcznik ułatwia Automatyzowanie i organizowanie odpowiedzi na określony alert. Elementy playbook są oparte na usłudze Azure Logic Apps. Szablony aplikacji logiki można użyć do tworzenia elementów playbook lub tworzyć własne.
- Prostym przykładem można utworzyć alert, który wyzwala sytuacji skanowanie portów dla sieciowej grupy zabezpieczeń. Można skonfigurować elementu playbook, który jest uruchamiany i zablokuje adres IP punktu początkowego skanowania.
- Innym przykładem mogą być aplikacji za pomocą przeciek pamięci. Gdy użycie pamięci pobiera do pewnego momentu, elementu playbook można odtworzyć proces.

![Alerty](./media/migrate-best-practices-security-management/alerts.png)
*alertów*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/monitoring-and-diagnostics/monitoring-overview-alerts) alertów.
- [Informacje](/azure/security-center/security-center-playbooks) o podręcznikach zabezpieczeń, które odpowiadają na alerty usługi Security Center.

## <a name="best-practice-use-the-azure-dashboard"></a>Najlepsze rozwiązanie: Korzystanie z pulpitu nawigacyjnego platformy Azure

Witryna Azure Portal to ujednolicona konsola internetowa umożliwiająca tworzenie i monitorowanie wszelkiego rodzaju aplikacji — od prostych aplikacji internetowych po złożone aplikacje w chmurze — oraz zarządzanie nimi. Obejmuje ona dostosowywalny pulpit nawigacyjny oraz opcje ułatwień dostępu.

- Można utworzyć wiele pulpitów nawigacyjnych i udostępnianie ich innym osobom, które mają dostęp do subskrypcji platformy Azure.
- W tym modelu udostępnionego członkowie zespołu mają wgląd w środowisku platformy Azure, umożliwiając im stosować proaktywne podejście związane z zarządzaniem systemy w chmurze.

![Pulpit nawigacyjny platformy Azure](./media/migrate-best-practices-security-management/dashboard.png)
*pulpitu nawigacyjnego platformy Azure*

**Dowiedz się więcej:**

- [Dowiedz się, jak](/azure/azure-portal/azure-portal-dashboards) Tworzenie pulpitu nawigacyjnego.
- [Informacje](/azure/azure-portal/azure-portal-dashboards-structure) o strukturze pulpitu nawigacyjnego.

## <a name="best-practice-understand-support-plans"></a>Najlepsze rozwiązanie: Informacje o planach pomocy technicznej

W pewnym momencie konieczna będzie współpraca z pracownikami Twojego działu pomocy technicznej lub pracownikiem pomocy technicznej firmy Microsoft. Posiadanie zestawu zasad i procedur na potrzeby pomocy technicznej podczas scenariuszy, takich jak odzyskiwanie awaryjne, ma kluczowe znaczenie. Ponadto administratorzy i pracownicy działu pomocy technicznej powinni być przeszkoleni w implementowaniu tych zasad.

- W przypadku mało prawdopodobnego zdarzenia, gdy usługa platformy Azure wpływa na obciążenie, administratorzy powinni wiedzieć, w jaki sposób przesłać bilet pomocy technicznej do firmy Microsoft w najbardziej odpowiedni i wydajny sposób.
- Zapoznaj się z różnymi planami pomocy technicznej oferowanymi na platformie Azure. One należeć do zakresu od czasów odpowiedzi przeznaczonych dla deweloperów wystąpień w wersji Premier pomocy technicznej i czas odpowiedzi z mniej niż 15 minut.

![Plany pomocy technicznej](./media/migrate-best-practices-security-management/support.png)
*plany pomocy technicznej*

**Dowiedz się więcej:**

- [Zapoznaj się z omówieniem](https://azure.microsoft.com/support/options) Azure plany pomocy technicznej.
- [Dodatkowe informacje](https://azure.microsoft.com/support/legal/sla) o umowach dotyczących poziomu usług (SLA).

## <a name="best-practice-manage-updates"></a>Najlepsze rozwiązanie: Zarządzanie aktualizacjami

Zapewnianie, że na maszynach wirtualnych platformy Azure będzie działać system operacyjny i oprogramowanie w aktualnej wersji, to bardzo trudne zadanie. Możliwość udostępnienia wszystkich maszyn wirtualnych, aby aktualizacje, które potrzebują oraz do automatycznego wypychania te aktualizacje są bardzo przydatne.

- Zarządzanie aktualizacjami w usłudze Azure Automation umożliwia zarządzanie aktualizacjami systemu operacyjnego dla komputerów z systemem Windows i Linux komputerów, które są wdrażane na platformie Azure, lokalnie i w chmurze innych dostawców.
- Umożliwiają szybko ocenić stan dostępnych aktualizacji na wszystkich komputerach agentów zarządzania aktualizacjami i zarządzanie instalacją aktualizacji.
- Zarządzanie aktualizacjami dla maszyn wirtualnych można włączyć bezpośrednio z konta usługi Azure Automation. Można również zaktualizować pojedynczej maszyny Wirtualnej na stronie maszyny Wirtualnej w witrynie Azure portal.
- Ponadto maszyny wirtualne platformy Azure mogą być rejestrowane z System Center Configuration Manager. Można następnie Migrowanie obciążeń programu Configuration Manager na platformę Azure i wykonaj raportowania oraz aktualizowanie oprogramowania za pomocą interfejsu jednej sieci web.

![Maszyna wirtualna aktualizacje](./media/migrate-best-practices-security-management/updates.png)
*aktualizacji*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/automation/automation-update-management) rozwiązanie update management na platformie Azure.
- [Dowiedz się, jak](/azure/automation/oms-solution-updatemgmt-sccmintegration) integracji programu Configuration Manager przy użyciu rozwiązania update management.
- [Często zadawane pytania dotyczące](/sccm/core/understand/configuration-manager-on-azure) program Configuration Manager na platformie Azure.

## <a name="implement-a-change-management-process"></a>Implementowanie procesu zarządzania zmianami

Podobnie jak w przypadku każdego systemu produkcyjnego wprowadzanie zmiany dowolnego typu może wpłynąć na środowisko. Proces zarządzania zmianami wymagający przesłania żądań w celu wprowadzenia zmian w systemach produkcyjnych jest cennym dodatkiem w zmigrowanym środowisku.

- Można tworzyć najlepsze praktyki platformy zarządzania zmianami zwiększyć świadomość w administratorów i personelu pomocy technicznej.
- Aby ułatwić zarządzanie konfiguracją i śledzenie zmian dla migrowanych przepływów pracy, można użyć usługi Azure Automation.
- Gdy wymuszanie proces zarządzania zmianami, połączyć zmiany platformy Azure, można użyć dzienników inspekcji dzienniki, aby prawdopodobnie (lub nie) istniejącego żądania zmiany. Jeśli więc zobaczysz zmianę bez odpowiadającego jej żądania zmiany, możesz zbadać, dlaczego wystąpił problem w procesie.

Na platformie Azure istnieje rozwiązanie do śledzenia zmian w usłudze Azure Automation:

- Rozwiązanie śledzi zmiany w oprogramowaniu i plikach systemu Windows oraz Linux, kluczach rejestru systemu Windows, usługach systemu Windows i demonach systemu Linux.
- Zmiany na monitorowanych serwerach są wysyłane do usługi Azure Monitor w chmurze w celu przetworzenia.
- Logika jest stosowana do odebranych danych, a usługa w chmurze rejestruje dane.
- Na pulpicie nawigacyjnym śledzenia zmian możesz łatwo zobaczyć zmiany, które zostały wprowadzone w ramach infrastruktury serwera.

![Zarządzanie zmianami](./media/migrate-best-practices-security-management/change.png)
*Zarządzanie zmianami*

**Dowiedz się więcej:**

- [Dowiedz się więcej o](/azure/automation/automation-change-tracking) śledzenie zmian.
- [Dowiedz się więcej o](/azure/automation/automation-intro) możliwości usługi Azure Automation.

## <a name="next-steps"></a>Kolejne kroki

Przejrzyj najlepsze rozwiązania:

- [Najlepsze praktyki](migrate-best-practices-networking.md) sieci po zakończeniu migracji.
- [Najlepsze praktyki](migrate-best-practices-costs.md) usługi cost management po migracji.
