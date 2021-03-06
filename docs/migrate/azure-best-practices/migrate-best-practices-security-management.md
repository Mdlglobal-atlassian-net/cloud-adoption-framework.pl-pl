---
title: Zabezpieczanie obciążeń i zarządzanie nimi na platformie Azure
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby poznać najlepsze rozwiązania dotyczące obsługi i zabezpieczania zmigrowanych obciążeń oraz zarządzania nimi.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 56abab2dbbc1acaa397fd04564bec45a8ebc5f8e
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862572"
---
<!-- cSpell:ignore FIPS SIEM majeure NSGs -->

# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Najlepsze rozwiązania dotyczące zabezpieczania obciążeń zmigrowanych na platformę Azure i zarządzania nimi

Podczas planowania i projektowania migracji oprócz kwestii związanych z samą migracją należy wziąć pod uwagę model zabezpieczeń i zarządzania na platformie Azure, który będzie używany po przeprowadzaniu migracji. W tym artykule opisano planowanie i najlepsze rozwiązania dotyczące zabezpieczania wdrożenia na platformie Azure po migracji oraz najlepsze rozwiązania dotyczące bieżących zadań, dzięki czemu wdrożenie będzie działać na optymalnym poziomie.

> [!IMPORTANT]
> Najlepsze rozwiązania i opinie opisane w tym artykule dotyczą funkcji usług i platformy Azure dostępnych w momencie pisania artykułu. Funkcje i możliwości zmieniają się w miarę upływu czasu.

## <a name="secure-migrated-workloads"></a>Zabezpieczanie migrowanych obciążeń

Po przeprowadzeniu migracji najistotniejszym zadaniem jest zabezpieczenie zmigrowanych obciążeń przed wewnętrznymi i zewnętrznymi zagrożeniami. Poniższe najlepsze rozwiązania ułatwiają osiągnięcie tego celu:

- [Pracuj z Azure Security Center](#best-practice-follow-azure-security-center-recommendations): Dowiedz się, jak korzystać z monitorowania, ocen i zaleceń zapewnianych przez Azure Security Center.
- [Szyfruj dane](#best-practice-encrypt-data): Uzyskaj najlepsze rozwiązania dotyczące szyfrowania danych na platformie Azure.
- [Konfiguracja oprogramowania chroniącego przed złośliwym kodem](#best-practice-protect-vms-with-antimalware): Chroń maszyny wirtualne przed złośliwym oprogramowaniem i złośliwymi atakami.
- [Zabezpieczanie aplikacji sieci Web](#best-practice-secure-web-apps): Zabezpiecz poufne informacje w zmigrowanych aplikacjach sieci Web.
- [Przejrzyj subskrypcje](#best-practice-review-subscriptions-and-resource-permissions): Sprawdź, kto może uzyskiwać dostęp do subskrypcji i zasobów platformy Azure po migracji.
- [Pracuj z dziennikami](#best-practice-review-audit-and-security-logs): regularnie Przeglądaj dzienniki inspekcji i zabezpieczeń platformy Azure.
- Zapoznaj się z [innymi funkcjami zabezpieczeń](#best-practice-evaluate-other-security-features): Poznaj i Oceń zaawansowane funkcje zabezpieczeń oferowane przez platformę Azure.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Najlepsze rozwiązanie: Postępuj zgodnie z zaleceniami Azure Security Center

Firma Microsoft dokłada wszelkich starań w celu zapewnienia, że administratorzy dzierżawy platformy Azure mają informacje konieczne do włączenia funkcji zabezpieczeń chroniących obciążenia przed atakami. Usługa Azure Security Center zapewnia ujednolicone zarządzanie zabezpieczeniami. Z poziomu usługi Security Center możesz stosować zasady zabezpieczeń względem różnych obciążeń, ograniczać podatność na zagrożenia i wykrywać ataki oraz reagować na nie. Usługa Security Center analizuje zasoby i konfiguracje w ramach dzierżaw platformy Azure i udostępnia zalecenia dotyczące zabezpieczeń, w tym:

- **Scentralizowane zarządzanie zasadami:** Zapewnienie zgodności z wymaganiami firmy lub przepisami bezpieczeństwa przez centralne zarządzanie zasadami zabezpieczeń we wszystkich obciążeniach chmury hybrydowej.
- **Ciągła ocena zabezpieczeń:** Monitoruj stan zabezpieczeń maszyn, sieci, magazynu i usług danych oraz aplikacji, aby wykrywać potencjalne problemy z zabezpieczeniami.
- **Rekomendacje** z możliwością wykonania: Koryguj luki w zabezpieczeniach, zanim będą mogły zostać wykorzystane przez osoby atakujące z zaleceniami dotyczącymi zabezpieczeń i z możliwością podejmowania działań.
- **Alerty i zdarzenia z priorytetami:** Najpierw należy skoncentrować się na najważniejszych zagrożeniach przy użyciu priorytetów alertów zabezpieczeń i zdarzeń.

Oprócz ocen i zaleceń usługa Azure Security Center udostępnia inne funkcje zabezpieczeń, które mogą zostać włączone dla określonych zasobów.

- **Dostęp just-in-Time (JIT).** Zmniejsz obszar podatny na ataki sieciowe za pomocą funkcji just-in-time zapewniającej kontrolowany dostęp do portów zarządzania na maszynach wirtualnych platformy Azure.
  - Gdy w Internecie jest otwarty port RDP 3389 maszyny wirtualnej, naraża on ją na stałe działania złośliwego użytkownika. Adresy IP platformy Azure są dobrze znane, a hakerzy ciągle sondują je w celu ataków na otwarte porty 3389.
  - Funkcja just-in-time korzysta z sieciowych grup zabezpieczeń i reguł przychodzących ograniczających czas, przez który określony port jest otwarty.
  - Po włączeniu funkcji just-in-time usługa Security Center sprawdza, czy użytkownik ma uprawnienia dostępu do zapisu w ramach kontroli dostępu na podstawie ról dla maszyny wirtualnej. Dodatkowo możesz określić reguły dotyczące sposobu, w jaki użytkownicy mogą nawiązywać połączenie z maszynami wirtualnymi. Jeśli uprawnienia są prawidłowe, żądanie dostępu zostanie zatwierdzone, a usługa Security Center skonfiguruje sieciowe grupy zabezpieczeń w taki sposób, aby zezwalały na ruch przychodzący do wybranych portów przez określony przez Ciebie czas. Po upływie tego czasu sieciowe grupy zabezpieczeń powrócą do poprzedniego stanu.
- **Adaptacyjne kontrolki aplikacji.** Zapobiegaj działaniu oprogramowania i złośliwego oprogramowanie na maszynach wirtualnych, kontrolując uruchamiane na nich aplikacje przy użyciu dynamicznych list dozwolonych.
  - Funkcje adaptacyjnego sterowania aplikacjami umożliwiają zatwierdzanie aplikacji i zapobiegają instalowaniu niezatwierdzonych lub niesprawdzonych aplikacji na maszynach wirtualnych przez nieautoryzowanych użytkowników lub administratorów.
    - Możesz blokować próby uruchomienia złośliwych aplikacji lub generować alerty z tym związane, unikać niechcianych lub złośliwych aplikacji oraz zapewniać zgodność z zasadami zabezpieczeń aplikacji w organizacji.
- **Monitorowanie integralności plików.** Zapewnij integralność plików działających na maszynach wirtualnych.
  - Nie musisz instalować oprogramowania, aby powodować problemy z maszyną wirtualną. Zmiana pliku systemowego może również spowodować awarię maszyny wirtualnej lub obniżenie jej wydajności. Monitorowanie integralności plików służy do sprawdzania plików systemowych oraz ustawień rejestru pod kątem zmian i powiadamiania użytkownika, gdy zostały wprowadzone jakiekolwiek aktualizacje.
  - Usługa Security Center zaleca, które pliki należy monitorować.

**Dowiedz się więcej:**

- Dowiedz się więcej o [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro).
- Dowiedz się więcej [na temat dostępu just in Time do maszyny wirtualnej](https://docs.microsoft.com/azure/security-center/security-center-just-in-time).
- Dowiedz się więcej na temat [stosowania adaptacyjnych kontrolek aplikacji](https://docs.microsoft.com/azure/security-center/security-center-adaptive-application).
- [Rozpoczynanie pracy](https://docs.microsoft.com/azure/security-center/security-center-file-integrity-monitoring) z monitorowaniem integralności plików.

## <a name="best-practice-encrypt-data"></a>Najlepsze rozwiązanie: szyfrowanie danych

Szyfrowanie jest ważnym elementem najlepszych rozwiązań dotyczących zabezpieczeń na platformie Azure. Zapewnienie włączonego szyfrowania na wszystkich poziomach pozwala zapobiec uzyskaniu dostępu do poufnych danych przez nieuprawnione strony. Dotyczy to danych przesyłanych i magazynowanych.

### <a name="encryption-for-iaas"></a>Szyfrowanie na potrzeby usług IaaS

- **Maszyny wirtualne:** W przypadku maszyn wirtualnych można użyć Azure Disk Encryption do szyfrowania dysków maszyn wirtualnych z systemami Windows i Linux IaaS.
  - Ta usługa korzysta z funkcji BitLocker dla systemu Windows oraz funkcji DM-Crypt dla systemu Linux, aby zapewnić szyfrowanie woluminów dysków systemu operacyjnego i danych.
  - Możesz użyć klucza szyfrowania utworzonego przez platformę Azure lub podać własne klucze szyfrowania chronione w usłudze Azure Key Vault.
  - Dzięki użyciu usługi Disk Encryption dane maszyny wirtualnej IaaS są zabezpieczone podczas ich magazynowania (na dysku) oraz podczas rozruchu maszyny wirtualnej.
    - Usługa Azure Security Center wygeneruje alert, jeśli będą istnieć niezaszyfrowane maszyny wirtualne.
- **Magazyn:** Ochrona danych przechowywanych w usłudze Azure Storage.
  - Dane przechowywane na kontach usługi Azure Storage można zaszyfrować przy użyciu wygenerowanych przez firmę Microsoft kluczy AES zgodnych ze standardem FIPS 140-2 lub przy użyciu własnych kluczy.
  - Szyfrowanie usługi Storage jest włączone dla wszystkich nowych i istniejących kont magazynu i nie można go wyłączyć.

### <a name="encryption-for-paas"></a>Szyfrowanie na potrzeby usług PaaS

W przeciwieństwie do usług IaaS, gdzie zarządzasz własnymi maszynami wirtualnymi i infrastrukturą, w modelu PaaS platforma i infrastruktura jest zarządzana przez dostawcę, co pozwala Ci się skupić na podstawowej logice i możliwościach aplikacji. W przypadku tylu różnych typów usług PaaS poszczególne usługi są oceniane indywidualnie pod kątem bezpieczeństwa. Jako przykład sprawdźmy, w jaki sposób możemy włączyć szyfrowanie dla usługi Azure SQL Database.

- **Always Encrypted:** Użyj Kreatora Always Encrypted w SQL Server Management Studio, aby chronić dane przechowywane.
  - Klucz funkcji Always Encrypted jest tworzony w celu szyfrowania danych w pojedynczej kolumnie.
  - Klucze funkcji Always Encrypted mogą być przechowywane jako zaszyfrowane w metadanych bazy danych lub w zaufanych magazynach kluczy, takich jak magazyn Azure Key Vault.
  - Aby użyć tej funkcji, prawdopodobnie konieczne będzie wprowadzenie zmian w aplikacji.
- **Przezroczyste szyfrowanie danych (TDE):** Ochrona Azure SQL Database przy użyciu szyfrowania w czasie rzeczywistym oraz odszyfrowywania bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku.
  - Szyfrowanie TDE umożliwia wykonywanie działań szyfrowania bez wprowadzania zmian w warstwie aplikacji.
  - TDE może używać kluczy szyfrowania dostarczonych przez firmę Microsoft lub można przenieść własny klucz.

**Dowiedz się więcej:**

- Dowiedz się więcej [na temat Azure Disk Encryption maszyn wirtualnych i zestawów skalowania maszyn wirtualnych](https://docs.microsoft.com/azure/security/fundamentals/azure-disk-encryption-vms-vmss).
- Włącz [Azure Disk Encryption dla maszyn wirtualnych z systemem Windows](https://docs.microsoft.com/azure/virtual-machines/windows/disk-encryption-overview).
- Dowiedz się więcej o [usłudze Azure szyfrowanie usługi Storage w przypadku danych przechowywanych w spoczynku](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).
- Zapoznaj się z [omówieniem Always Encrypted](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault).
- Zapoznaj się [z informacjami na temat przezroczystego szyfrowania danych dla SQL Database i usługi Azure Synapse](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-azure-sql).
- Dowiedz się więcej o [usłudze Azure SQL transparent Data Encryption z kluczem zarządzanym przez klienta](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql).

## <a name="best-practice-protect-vms-with-antimalware"></a>Najlepsze rozwiązanie: Ochrona maszyn wirtualnych przed złośliwym oprogramowaniem

W przypadku starszych maszyn wirtualnych zmigrowanych na platformę Azure często zdarza się, że nie posiadają one oprogramowania chroniącego przed złośliwym kodem na odpowiednim poziomie. Platforma Azure udostępnia bezpłatne rozwiązanie punktu końcowego, które pomaga chronić maszyny wirtualne przed wirusami, programami szpiegującymi i innym złośliwym oprogramowaniem.

- Rozwiązanie Microsoft Antimalware dla platformy Azure generuje alerty w przypadku próby instalacji znanego złośliwego lub niepożądanego oprogramowania.
- Jest to rozwiązanie w ramach jednego agenta, które działa w tle bez interwencji człowieka.
- W usłudze Azure Security Center możesz łatwo zidentyfikować maszyny wirtualne, które nie mają uruchomionej ochrony punktu końcowego, i w razie potrzeby zainstalować rozwiązanie Microsoft Antimalware.

  ![Oprogramowanie chroniące przed złośliwym kodem dla maszyn wirtualnych](./media/migrate-best-practices-security-management/antimalware.png)
  _Oprogramowanie chroniące przed złośliwym kodem dla maszyn wirtualnych_

**Dowiedz się więcej:**

- Informacje o [programie Microsoft chroniącym przed złośliwym oprogramowaniem dla platformy Azure Cloud Services i Virtual Machines](https://docs.microsoft.com/azure/security/fundamentals/antimalware).

## <a name="best-practice-secure-web-apps"></a>Najlepsze rozwiązanie: Zabezpieczanie aplikacji sieci Web

Zmigrowanych aplikacji internetowych dotyczy kilka problemów:

- W większości starszych aplikacji internetowych informacje poufne są zwykle przechowywane w plikach konfiguracyjnych. Pliki zawierające takie informacje mogą powodować problemy z bezpieczeństwem w przypadku tworzenia kopii zapasowej aplikacji lub podczas wyewidencjonowywania lub ewidencjonowania kodu aplikacji w ramach kontroli kodu źródłowego.
- Ponadto podczas migrowania aplikacji internetowych znajdujących się na maszynie wirtualnej prawdopodobnie ta maszyna zostanie przeniesiona z sieci lokalnej i środowiska chronionego przez zaporę do środowiska internetowego. Upewnij się, że skonfigurowano rozwiązanie, które spełnia takie same funkcje, jak lokalne zasoby ochrony.

Platforma Azure zapewnia kilka rozwiązań:

- **Azure Key Vault:** Obecnie deweloperzy aplikacji sieci Web podejmują kroki w celu zapewnienia, że poufne informacje nie będą wyciekać z tych plików. Jedną z metod zabezpieczania informacji jest wyodrębnienie ich z plików i umieszczenie w magazynie Azure Key Vault.
  - Za pomocą magazynu Key Vault można scentralizować przechowywanie wpisów tajnych aplikacji i kontrolować ich dystrybucję. Pozwala to uniknąć konieczności przechowywania informacji o zabezpieczeniach w plikach aplikacji.
  - Aplikacje mogą bezpiecznie uzyskiwać dostęp do informacji znajdujących się w magazynie przy użyciu identyfikatorów URI bez konieczności używania niestandardowego kodu.
  - Usługa Azure Key Vault pozwala zablokować dostęp za pośrednictwem kontroli zabezpieczeń platformy Azure i bezproblemowo implementować „klucze przerzucane”. Firma Microsoft nie ma wglądu w Twoje dane ani nie może ich wyodrębniać.
- **App Service Environment:** Jeśli migrowana aplikacja wymaga dodatkowej ochrony, można rozważyć dodanie App Service Environment i zapory aplikacji sieci Web w celu ochrony zasobów aplikacji.
  - Funkcja Azure App Service Environment zapewnia w pełni izolowane i dedykowane środowisko, w którym można uruchamiać aplikacje App Service, takie jak aplikacje internetowe systemu Windows i Linux, kontenery platformy Docker, aplikacje mobilne i funkcje.
  - Jest to przydatne w przypadku aplikacji o bardzo dużej skali, wymagających izolacji lub mających duże użycie pamięci.
- **Zapora aplikacji sieci Web:** Funkcja platformy Azure Application Gateway, która zapewnia scentralizowaną ochronę aplikacji sieci Web.
  - Chroni aplikacje internetowe bez konieczności modyfikowania kodu zaplecza.
  - Zapewnia jednoczesną ochronę wielu aplikacji internetowych za bramą aplikacji.
  - Zaporę aplikacji sieci Web można monitorować przy użyciu Azure Monitor i jest ona zintegrowana z Azure Security Center.

  ![Zabezpieczanie aplikacji internetowych ](./media/migrate-best-practices-security-management/web-apps.png)
   _Azure Key Vault_

**Dowiedz się więcej:**

- Zapoznaj się z [omówieniem Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/overview).
- Dowiedz się więcej o [zaporze aplikacji sieci Web](https://docs.microsoft.com/azure/application-gateway/waf-overview).
- Zapoznaj [się z wprowadzeniem do środowiska App Service](https://docs.microsoft.com/azure/app-service/environment/intro).
- Dowiedz się, jak [skonfigurować aplikację sieci Web do odczytywania wpisów tajnych z Key Vault](https://docs.microsoft.com/azure/key-vault/tutorial-web-application-keyvault).
- Dowiedz się więcej o [zaporze aplikacji sieci Web](https://docs.microsoft.com/azure/application-gateway/waf-overview).

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Najlepsze rozwiązanie: przeglądanie subskrypcji i uprawnień zasobów

Podczas migrowania obciążeń i uruchamiania ich na platformie Azure pracownicy z dostępem do obciążeń wykonują różne zadania. Zespół ds. zabezpieczeń powinien regularnie przeglądać dostęp do dzierżawy i grup zasobów platformy Azure. Na platformie Azure dostępne są oferty związane z zarządzaniem tożsamościami i zabezpieczeniami kontroli dostępu, co obejmuje kontrolę dostępu na podstawie ról w celu autoryzowania uprawnień dostępu do zasobów platformy Azure.

- Za pomocą kontroli dostępu na podstawie ról przypisywane są uprawnienia dostępu dla podmiotów zabezpieczeń. Podmioty zabezpieczeń reprezentują użytkowników, grupy (zestaw użytkowników), jednostki usług (tożsamość używana przez aplikacje i usługi) oraz tożsamości zarządzane (tożsamość usługi Azure Active Directory automatycznie zarządzana przez platformę Azure).
- Za pomocą kontroli dostępu na podstawie ról można przypisywać role do podmiotów zabezpieczeń, takich jak właściciel, współautor i czytelnik, oraz definicji ról (kolekcja uprawnień) określających operacje, które mogą być wykonywane przez role.
- Za pomocą kontroli dostępu na podstawie ról można również ustawiać zakresy określające granicę dla roli. Zakres można ustawić na kilku poziomach, na przykład dla grupy zarządzania, subskrypcji, grupy zasobów lub zasobu.
- Upewnij się, że Administratorzy z dostępem do platformy Azure mają dostęp tylko do zasobów, na które chcesz zezwolić. Jeśli wstępnie zdefiniowane role na platformie Azure nie są wystarczająco szczegółowe, możesz utworzyć role niestandardowe w celu oddzielenia i ograniczenia uprawnień dostępu.

  ![Kontrola dostępu](./media/migrate-best-practices-security-management/subscription.png)
  _Kontrola dostępu — zarządzanie dostępem i tożsamościami_

**Dowiedz się więcej:**

- [Informacje](https://docs.microsoft.com/azure/role-based-access-control/overview) o kontroli dostępu na podstawie ról.
- [Informacje](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) o zarządzaniu dostępem przy użyciu kontroli dostępu na podstawie ról i witryny Azure Portal.
- Dowiedz się więcej o [rolach niestandardowych](https://docs.microsoft.com/azure/role-based-access-control/custom-roles).

## <a name="best-practice-review-audit-and-security-logs"></a>Najlepsze rozwiązanie: przegląd dzienników inspekcji i zabezpieczeń

Usługa Azure Active Directory (Azure AD) udostępnia dzienniki aktywności, które są wyświetlane w usłudze Azure Monitor. W dziennikach przechwytywane są operacje wykonywane w ramach dzierżawy platformy Azure wraz z datą ich przeprowadzenia oraz wykonawcą.

- Dzienniki inspekcji zawierają historię zadań w dzierżawie. Dzienniki aktywności logowania zawierają informacje o wykonawcy danego zadania.
- Dostęp do raportów zabezpieczeń zależy od licencji usługi Azure AD. W obszarze bezpłatna i podstawowa otrzymujesz listę ryzykownych użytkowników i logowania. W wersjach Premium 1 i Premium 2 są uzyskiwane podstawowe informacje o zdarzeniach.
- Dzienniki aktywności możesz kierować do różnych punktów końcowych w celu długoterminowego przechowywania i wglądu w dane.
- Staraj się regularnie przeglądać dzienniki lub zintegruj narzędzia do zarządzania informacjami i zdarzeniami zabezpieczeń (SIEM, security information and event management) w celu automatycznego przeglądania nieprawidłowości. Jeśli nie korzystasz z wersji Premium 1 ani 2, konieczne będzie samodzielnie wykonanie wielu analiz lub użycie w tym celu systemu SIEM. Analiza obejmuje wyszukiwanie ryzykownych logowań i zdarzeń oraz innych wzorców ataków użytkowników.

  ![Użytkownicy i grupy ](./media/migrate-best-practices-security-management/azure-ad.png)
   _usługi Azure AD Użytkownicy i grupy_

**Dowiedz się więcej:**

- Dowiedz się więcej o [dziennikach aktywności usługi Azure AD w Azure monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor).
- Dowiedz się [, jak przeprowadzać inspekcję raportów o działaniach w portalu usługi Azure AD](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs).

## <a name="best-practice-evaluate-other-security-features"></a>Najlepsze rozwiązanie: Oceń inne funkcje zabezpieczeń

Platforma Azure udostępnia inne funkcje zabezpieczeń, które zapewniają zaawansowane opcje ochrony. Niektóre z tych najlepszych rozwiązań wymagają licencji na dodatki i opcji premium.

- **Zaimplementuj jednostki administracyjne usługi Azure AD.** Delegowanie obowiązków administracyjnych do pracowników działu pomocy technicznej może być skomplikowane przy użyciu jedynie podstawowej kontroli dostępu platformy Azure. Umożliwienie pracownikom działu pomocy technicznej dostępu do wszystkich grup w usłudze Azure AD może nie być idealnym podejściem w kontekście zabezpieczeń organizacji. Korzystanie z jednostek administracyjnych umożliwia rozdzielenie zasobów platformy Azure na kontenery w podobny sposób, jak w przypadku lokalnych jednostek organizacyjnych. Aby użyć jednostek administracyjnych, ich administrator musi mieć licencję usługi Azure AD w wersji Premium. [Dowiedz się więcej](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Użyj uwierzytelniania wieloskładnikowego.** Jeśli masz licencję usługi Azure AD w warstwie Premium, możesz włączyć i wymusić uwierzytelnianie wieloskładnikowe na kontach administratorów. Wyłudzanie informacji jest najpopularniejszym sposobem naruszania zabezpieczeń poświadczeń kont. Gdy złośliwy użytkownik ma poświadczenia konta administratora, nie ma możliwości zatrzymywania go przed wykonaniem mających poważne konsekwencje akcji, takich jak usunięcie wszystkich grup zasobów. Uwierzytelnianie wieloskładnikowe można ustanowić na kilka sposobów, w tym za pomocą poczty e-mail, aplikacji uwierzytelniania i wiadomości SMS. Jako administrator możesz wybrać najmniej natarczywą opcję. Uwierzytelnianie wieloskładnikowe integruje się z funkcją analizy zagrożeń i zasadami dostępu warunkowego w celu losowego wymagania odpowiedzi na wyzwanie uwierzytelniania wieloskładnikowego. Dowiedz się więcej o [wskazówkach dotyczących zabezpieczeń](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) oraz o [sposobie konfigurowania uwierzytelniania wieloskładnikowego](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Zaimplementuj dostęp warunkowy.** W większości małych i średnich organizacji administratorzy platformy Azure i zespół pomocy technicznej prawdopodobnie znajdują się w jednej lokalizacji geograficznej. W takim przypadku większość nazw logowań będzie pochodzić z tych samych obszarów. Jeśli adresy IP tych lokalizacji są dość statyczne, logiczne jest, że nazwy logowania administratorów nie będą pochodzić spoza tych obszarów. Nawet jeśli zdalny zły aktor narusza poświadczenia administratora, można zaimplementować funkcje zabezpieczeń, takie jak dostęp warunkowy połączony z uwierzytelnianiem wieloskładnikowym, aby uniemożliwić logowanie się z lokalizacji zdalnych lub sfałszowanych lokalizacji z losowych adresów IP. [Dowiedz się więcej](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) o dostępie warunkowym i [przejrzyj najlepsze rozwiązania](https://docs.microsoft.com/azure/active-directory/conditional-access/best-practices) dotyczące dostępu warunkowego w usłudze Azure AD.
- **Przejrzyj uprawnienia aplikacji dla przedsiębiorstw.** W miarę upływu czasu administratorzy wybierają linki firmy Microsoft i innych firm bez znajomości ich wpływu na organizację. Linki mogą zawierać ekrany zgody, na których przypisywane są uprawnienia do aplikacji platformy Azure, i mogą zezwalać na dostęp do odczytu danych usługi Azure AD lub nawet pełny dostęp do zarządzania całą subskrypcją platformy Azure. Należy regularnie przeglądać aplikacje, którym administratorzy i użytkownicy zezwolili na dostęp do zasobów platformy Azure. Upewnij się, że te aplikacje mają tylko wymagane uprawnienia. Dodatkowo co kwartał lub półrocze możesz wysyłać wiadomość e-mail do użytkowników z linkiem do stron aplikacji, aby pamiętali oni o aplikacjach, którym zezwolili na dostęp do danych organizacji. [Dowiedz się więcej](https://docs.microsoft.com/azure/active-directory/manage-apps/application-types) o typach aplikacji [oraz o sposobie kontrolowania](https://docs.microsoft.com/azure/active-directory/manage-apps/remove-user-or-group-access-portal) przypisań aplikacji w usłudze Azure AD.

## <a name="managed-migrated-workloads"></a>Migrowane obciążenia zarządzane

W tej sekcji zalecimy niektóre najlepsze rozwiązania dotyczące zarządzania platformą Azure, co obejmuje:

- [Zarządzanie zasobami](#best-practice-name-resource-groups): najlepsze rozwiązania dotyczące grup zasobów i zasobów platformy Azure, takich jak inteligentne nazewnictwo, zapobieganie przypadkowemu usuwaniu, zarządzanie uprawnieniami zasobów i efektywne tagowanie zasobów.
- [Korzystanie z planów](#best-practice-implement-blueprints): zwięzłe omówienie korzystania z planów do tworzenia środowisk wdrażania i zarządzania nimi.
- [Przejrzyj architektury](#best-practice-review-azure-reference-architectures): Przejrzyj przykładowe architektury platformy Azure, aby dowiedzieć się, jak budować wdrożenia po migracji.
- [Konfigurowanie grup zarządzania](#best-practice-manage-resources-with-azure-management-groups): Jeśli masz wiele subskrypcji, możesz zebrać je do grup zarządzania i zastosować ustawienia ładu do tych grup.
- [Konfigurowanie zasad dostępu](#best-practice-deploy-azure-policy): stosowanie zasad zgodności do zasobów platformy Azure.
- [Zaimplementuj strategię BCDR](#best-practice-implement-a-bcdr-strategy): przeprowadzenie strategii zachowania ciągłości działania i odzyskiwania po awarii (BCDR) w celu zapewnienia bezpieczeństwa danych, odporności na środowisko i zasobów w przypadku wystąpienia awarii.
- [Zarządzanie maszynami wirtualnymi](#best-practice-use-managed-disks-and-availability-sets): grupowanie maszyn wirtualnych w grupy dostępności w celu zapewnienia odporności i wysokiej dostępności. Używaj dysków zarządzanych, aby ułatwić zarządzanie dyskami i magazynami maszyn wirtualnych.
- [Monitorowanie użycia zasobów](#best-practice-monitor-resource-usage-and-performance): Włączanie rejestrowania diagnostycznego dla zasobów platformy Azure, tworzenie alertów i elementy PlayBook na potrzeby aktywnego rozwiązywania problemów oraz korzystanie z pulpitu nawigacyjnego platformy Azure w celu jednolitego wglądu w kondycję i stan wdrożenia.
- [Zarządzanie obsługą i aktualizacjami](#best-practice-manage-updates): Poznaj swój plan pomocy technicznej platformy Azure oraz sposób jego implementacji, uzyskaj najlepsze rozwiązania dotyczące aktualizowania maszyn wirtualnych oraz umieszczania procesów w celu zarządzania zmianami.

## <a name="best-practice-name-resource-groups"></a>Najlepsze rozwiązanie: Nazwa grupy zasobów

Zapewnienie, że grupy zasobów mają znaczące nazwy, które mogą zostać łatwo rozpoznane przez administratorów i członków zespołu pomocy technicznej i po których mogą się oni łatwo poruszać, w znaczący sposób zwiększy produktywność i wydajność.

- Zalecamy stosowanie konwencji nazewnictwa platformy Azure.
- W przypadku synchronizowania lokalnej usługi Active Directory z usługą Azure AD przy użyciu programu Azure AD Connect należy rozważyć dopasowanie nazw lokalnych grup zabezpieczeń do nazw grup zasobów na platformie Azure.

  ![Nazywanie ](./media/migrate-best-practices-security-management/naming.png)
   _nazw grup zasobów_

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [zalecanych konwencji nazewnictwa](../../ready/azure-best-practices/naming-and-tagging.md).

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Najlepsze rozwiązanie: implementowanie blokad usuwania dla grup zasobów

Zniknięcie grupy zasobów z powodu przypadkowego usunięcia jest bardzo niekorzystne. Zalecamy zaimplementowanie blokad usuwania, aby nie miało to miejsca.

  ![Usuń blokady ](./media/migrate-best-practices-security-management/locks.png) _Usuń blokady_

**Dowiedz się więcej:**

- Dowiedz się więcej o [blokowaniu zasobów, aby uniknąć nieoczekiwanych zmian](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources).

## <a name="best-practice-understand-resource-access-permissions"></a>Najlepsze rozwiązanie: zrozumienie uprawnień dostępu do zasobów

Właściciel subskrypcji ma dostęp do wszystkich grup zasobów i zasobów w ramach subskrypcji.

- Z rozwagą dodawaj osoby do tego istotnego przypisania. Zrozumienie znaczenia tych rodzajów uprawnień jest ważne w kontekście zapewnienia bezpieczeństwa i stabilności środowiska.
- Upewnij się, że zasoby są umieszczane w odpowiednich grupach zasobów:
  - Dopasuj ze sobą zasoby z podobnym cyklem życia. W idealnym przypadku nie będzie wymagane przeniesienie zasobu w razie konieczności usunięcia całej grupy zasobów.
  - Zasoby obsługujące funkcję lub obciążenie należy umieścić razem w celu uproszczenia zarządzania.

**Dowiedz się więcej:**

- Dowiedz się więcej o [organizowaniu subskrypcji i grup zasobów](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).

## <a name="best-practice-tag-resources-effectively"></a>Najlepsze rozwiązanie: wydajne Dodawanie tagów do zasobów

W wielu przypadkach użycie tylko nazwy grupy zasobów powiązanej z zasobami nie zapewni wystarczającej ilości metadanych do efektywnej implementacji takich mechanizmów, jak rozliczenia wewnętrzne lub zarządzanie w ramach subskrypcji.

- Najlepszym rozwiązaniem jest użycie tagów platformy Azure w celu dodania przydatnych metadanych, względem których mogą być wykonywane zapytania i raporty.
- Tagi stanowią sposób logicznego organizowania zasobów przy użyciu zdefiniowanych właściwości. Tagi można stosować bezpośrednio względem grup zasobów lub zasobów.
- Tagi można również stosować względem grupy zasobów lub poszczególnych zasobów. Tagi grupy zasobów nie są dziedziczone przez zasoby w grupie.
- Tagowanie możesz zautomatyzować przy użyciu programu PowerShell lub Azure Automation. Możesz również oznaczyć poszczególne grupy i zasoby. -podejście do tagowania lub samoobsługowe. Jeśli posiadasz system żądania zmian i zarządzania nimi, możesz w łatwy sposób użyć informacji w żądaniu w celu wypełnienia tagów zasobów specyficznych dla firmy.

  ![Tagowanie](./media/migrate-best-practices-security-management/tagging.png)
  _Tagowanie_

**Dowiedz się więcej:**

- Dowiedz się więcej o [znakowaniu i ograniczeniach tagów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).
- Zapoznaj [się z przykładami programu PowerShell i interfejsu wiersza polecenia, aby skonfigurować tagowanie i zastosować do zasobów Tagi z grupy zasobów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources#powershell).
- [Informacje](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) o najlepszych rozwiązaniach dotyczących tagowania na platformie Azure.

## <a name="best-practice-implement-blueprints"></a>Najlepsze rozwiązanie: implementowanie planów

Usługę Azure Blueprints można porównać do planu, który pozwala inżynierowi lub architektowi naszkicować parametry projektu. Usługa ta umożliwia architektom chmury i centralnym grupom IT definiowanie powtarzalnego zestawu zasobów platformy Azure, który implementuje standardy, wzorce i wymagania organizacji oraz jest z nimi zgodny. Usługa Azure Blueprints umożliwia zespołom programistów szybkie tworzenie nowych środowisk spełniających wymagania dotyczące zgodności organizacji, które posiadają zestaw wbudowanych składników — takich jak sieć — przyspieszających opracowywanie i dostarczanie.

- Za pomocą strategii można orkiestrować wdrożenia grup zasobów, szablony usługi Azure Resource Manager oraz przypisania zasad i ról.
- Strategie są przechowywane w dystrybuowanej globalnie usłudze Azure Cosmos DB. Obiekty strategii są replikowane w wielu regionach świadczenia usługi Azure. Replikacja zapewnia małe opóźnienia, wysoką dostępność oraz spójny dostęp do strategii niezależnie od regionu, w którym zasoby są wdrażane w ramach strategii.

**Dowiedz się więcej:**

- [Informacje](https://docs.microsoft.com/azure/governance/blueprints/overview) o strategiach.
- Zapoznaj się z [przykładowym planem przyspieszenia w dziedzinie ochrony zdrowia AI](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare).

## <a name="best-practice-review-azure-reference-architectures"></a>Najlepsze rozwiązanie: przegląd architektur referencyjnych platformy Azure

Tworzenie bezpiecznych, skalowalnych i możliwych do zarządzanych obciążeń na platformie Azure może być czasochłonnym zadaniem. W przypadku ciągłych zmian nadążanie za różnymi funkcjami wymaganymi w celu optymalnego środowiska może być skomplikowane. Dodatkowe informacje mogą być przydatne podczas projektowania i migrowania obciążeń. Twórcy platformy Azure i ich partnerzy utworzyli kilka przykładowych architektur referencyjnych na potrzeby różnych typów środowisk. Te przykłady zaprojektowano w celu udostępnienia pomysłów, na podstawie których można się uczyć się i tworzyć.

Architektury referencyjne są uporządkowane według scenariusza. Zawierają one najlepsze rozwiązania i wskazówki dotyczące zarządzania, dostępności, skalowalności i zabezpieczeń.
Funkcja Azure App Service Environment zapewnia w pełni izolowane i dedykowane środowisko, w którym można uruchamiać aplikacje App Service, takie jak aplikacje internetowe systemu Windows i Linux, kontenery platformy Docker, aplikacje mobilne i funkcje. Usługa App Service dodaje do aplikacji możliwości platformy Azure, takie jak zabezpieczenia, równoważenie obciążenia, automatyczne skalowanie i automatyczne zarządzanie. Umożliwia również korzystanie z funkcji metodyki DevOps, takich jak ciągłe wdrażanie z usług Azure DevOps i GitHub, zarządzanie pakietami, środowiska przejściowe, domena niestandardowa i certyfikaty SSL. Usługa App Service jest przydatna w przypadku aplikacji, które wymagają izolacji i bezpiecznego dostępu do sieci, oraz aplikacji, które korzystają z dużej ilości pamięci i innych zasobów wymagających skalowania.

**Dowiedz się więcej:**

- Poznaj [architektury referencyjne platformy Azure](https://docs.microsoft.com/azure/architecture/reference-architectures).
- Zapoznaj się z [przykładowymi scenariuszami platformy Azure](https://docs.microsoft.com/azure/architecture/example-scenario).

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Najlepsze rozwiązanie: zarządzanie zasobami za pomocą grup zarządzania platformy Azure

Jeśli Twoja organizacja ma wiele subskrypcji, konieczne jest zarządzanie dostępem, zasadami i zgodnością na ich potrzeby. Grupy zarządzania platformy Azure zapewniają poziom zakresu powyżej subskrypcji.

- Subskrypcje są organizowane w kontenerach nazywanych grupami zarządzania, do których należy zastosować swoje warunki nadzoru.
- Wszystkie subskrypcje w grupie zarządzania automatycznie dziedziczą warunki grupy zarządzania.
- Grupy zarządzania zapewniają zarządzanie klasy korporacyjnej na dużą skalę niezależnie od typu subskrypcji.
- Możesz na przykład zastosować zasady grupy zarządzania ograniczające regiony, w których można tworzyć maszyny wirtualne. Te zasady są następnie stosowane względem wszystkich grup zarządzania, subskrypcji i zasobów w ramach tej grupy zarządzania.
- Możesz utworzyć elastyczną strukturę grup zarządzania i subskrypcji w celu organizowania zasobów w hierarchię na potrzeby ujednoliconego zarządzania zasadami i dostępem.

Na poniższym diagramie przedstawiono przykład tworzenia hierarchii dla nadzoru przy użyciu grup zarządzania.

  ![Grupy zarządzania](./media/migrate-best-practices-security-management/management-groups.png) _Grupy zarządzania_

**Dowiedz się więcej:**

- Dowiedz się więcej o [organizowaniu zasobów w grupach zarządzania](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="best-practice-deploy-azure-policy"></a>Najlepsze rozwiązanie: wdrażanie Azure Policy

Azure Policy to usługa platformy Azure, która umożliwia tworzenie i przypisywanie zasad oraz zarządzanie nimi.

- Zasady wymuszają różne reguły i efekty dotyczące zasobów, dzięki czemu zasoby te pozostają zgodne ze standardami firmy i umowami dotyczącymi poziomu usług.
- Usługa Azure Policy ocenia zasoby i skanuje je pod kątem braku zgodności z zasadami.
- Możesz na przykład utworzyć zasady, które zezwalają tylko na określony rozmiar jednostki SKU dla maszyn wirtualnych w środowisku. Usługa Azure Policy oceni to ustawienie podczas tworzenia i aktualizowania zasobów oraz podczas skanowania istniejących zasobów.
- Na platformie Azure dostępne są pewne wbudowane zasady, które można przypisać. Możesz również utworzyć własne zasady.

  ![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
  _Azure Policy_

**Dowiedz się więcej:**

- Zapoznaj się z [omówieniem Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview).
- Dowiedz się więcej [na temat tworzenia zasad i zarządzania nimi w celu wymuszenia zgodności](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage).

## <a name="best-practice-implement-a-bcdr-strategy"></a>Najlepsze rozwiązanie: implementowanie strategii BCDR

Planowanie ciągłości działalności biznesowej i odzyskiwania po awarii (BCDR) jest niezwykle ważnym zadaniem, które należy wykonać w ramach procesu planowania migracji na platformę Azure. W postanowieniach prawnych umowy mogą zawierać klauzulę dotyczącą siły wyższej, która usprawiedliwia niespełnienie zobowiązań ze względu na siłę wyższą, taką jak huragany lub trzęsienia ziemi. Posiadasz jednak również zobowiązania dotyczące możliwości zapewnienia ciągłego działania usług i odzyskania (w razie potrzeby) po awarii. Może to mieć decydujące znaczenie dla przyszłości Twojej firmy.

Ogólnie Twoja strategia BCDR musi obejmować:

- **Kopia zapasowa danych:** Jak zapewnić bezpieczeństwo danych, aby można je było łatwo odzyskać w przypadku wystąpienia awarii.
- **Odzyskiwanie po awarii:** Jak zapewnić odporność i dostępność aplikacji w przypadku wystąpienia awarii.

### <a name="set-up-bcdr"></a>Konfigurowanie strategii BCDR

Podczas migrowania na platformę Azure ważne jest, aby zrozumieć, że chociaż platforma Azure zapewnia te wbudowane funkcje odporności, należy zaprojektować wdrożenie na platformie Azure w taki sposób, aby skorzystać z zalet funkcji i usług platformy Azure zapewniających wysoką dostępność, odzyskiwanie po awarii i tworzenie kopii zapasowych.

- Twoje rozwiązanie BCDR będzie zależeć od celów firmy i używanej strategii wdrażania na platformie Azure. W przypadku wdrożeń w modelu infrastruktura jako usługa (IaaS) i platforma jako usługa (PaaS) stawiane są różne wyzwania względem strategii BCDR.
- Po utworzeniu rozwiązania BCDR powinny być regularnie testowane, aby sprawdzić, czy Twoja strategia jest nadal odpowiednia.

### <a name="back-up-an-iaas-deployment"></a>Tworzenie kopii zapasowej wdrożenia IaaS

W większości przypadków obciążenie lokalne jest wycofywane po migracji, a lokalna strategia tworzenia kopii zapasowych danych musi zostać rozszerzona lub zastąpiona. Jeśli przeprowadzasz migrację całego centrum danych na platformę Azure, konieczne jest zaprojektowanie i zaimplementowanie pełnego rozwiązania do tworzenia kopii zapasowych przy użyciu technologii platformy Azure lub zintegrowanych rozwiązań innych firm.

W przypadku obciążeń uruchomionych w ramach maszyn wirtualnych IaaS platformy Azure należy wziąć pod uwagę następujące rozwiązania:

- **Azure Backup:** Zapewnia kopie zapasowe spójne na poziomie aplikacji dla maszyn wirtualnych z systemami Windows i Linux.
- **Migawki magazynu:** Tworzy migawki magazynu obiektów BLOB.

#### <a name="azure-backup"></a>Azure Backup

Usługa Azure Backup tworzy punkty odzyskiwania danych przechowywane w magazynie platformy Azure. Usługa Azure Backup może tworzyć kopie zapasowe dysków maszyn wirtualnych platformy Azure i dane usługi Azure Files (wersja zapoznawcza). Usługa Azure Files zapewnia udziały plików w chmurze dostępne za pośrednictwem protokołu SMB.

Za pomocą usługi Azure Backup można tworzyć kopie zapasowe maszyn wirtualnych na kilka sposobów.

- **Bezpośrednie tworzenie kopii zapasowych na podstawie ustawień maszyny wirtualnej.** Możesz utworzyć kopię zapasową maszyn wirtualnych za pomocą usługi Azure Backup bezpośrednio z poziomu opcji maszyny wirtualnej w witrynie Azure Portal. Można utworzyć kopię zapasową maszyny wirtualnej raz dziennie, a dysk maszyny wirtualnej można przywrócić w razie konieczności. Usługa Azure Backup wykonuje migawki danych z uwzględnieniem aplikacji (usługa VSS), a na maszynie wirtualnej nie jest zainstalowany żaden agent.
- **Bezpośrednie tworzenie kopii zapasowych w magazynie usług Recovery Services.** Możesz utworzyć kopię zapasową maszyn wirtualnych IaaS, wdrażając magazyn Recovery Services w usłudze Azure Backup. Zapewnia to pojedynczą lokalizację do śledzenia kopii zapasowych i zarządzania nimi, a także szczegółowe opcje tworzenia kopii zapasowych i przywracania. Kopia zapasowa jest tworzona maksymalnie trzy razy dziennie na poziomie plików/folderów. Nie uwzględnia ona aplikacji, a system Linux nie jest obsługiwany. Zainstaluj agenta usług Microsoft Azure Recovery Services (MARS) na każdej maszynie wirtualnej, dla której chcesz utworzyć kopię zapasową za pomocą tej metody.
- **Ochrona maszyny wirtualnej na serwerze Azure Backup Server.** Serwer Azure Backup Server jest udostępniany bezpłatnie wraz z usługą Azure Backup. Kopia zapasowa maszyny wirtualnej jest tworzona w lokalnym magazynie serwera Azure Backup Server. Następnie wykonywana jest kopia zapasowa serwera Azure Backup Server na platformie Azure w magazynie. Kopia zapasowa uwzględnia aplikację i posiada pełny stopień szczegółowości dotyczący częstotliwości wykonywania kopii zapasowych i przechowywania. Możesz tworzyć kopię zapasową na poziomie aplikacji, na przykład tworząc kopie zapasową programu SQL Server lub SharePoint.

W celu zapewnienia bezpieczeństwa Azure Backup szyfruje dane w locie przy użyciu algorytmu AES-256 i wysyła je za pośrednictwem protokołu HTTPS do platformy Azure. Kopia zapasowa danych magazynowanych na platformie Azure jest szyfrowana przy użyciu [usługi Storage (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption) oraz danych do przesyłania i magazynowania.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
_Azure Backup_

**Dowiedz się więcej:**

- Dowiedz się więcej o usłudze [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview) .
- Planowanie [infrastruktury kopii zapasowych dla maszyn wirtualnych platformy Azure](https://docs.microsoft.com/azure/backup/backup-azure-vms-introduction).

#### <a name="storage-snapshots"></a>Migawki magazynu

Maszyny wirtualne platformy Azure są przechowywane jako stronicowe obiekty blob w usłudze Azure Storage.

- Migawki przechwytują stan obiektu blob w określonym punkcie w czasie.
- Jako alternatywną metodę tworzenia kopii zapasowych dla dysków maszyn wirtualnych platformy Azure możesz utworzyć migawkę obiektów blob magazynu, a następnie skopiować je do innego konta magazynu.
- Możesz skopiować cały obiekt blob lub użyć kopii migawki przyrostowej, aby skopiować tylko zmiany różnicowe i zmniejszyć ilość miejsca do magazynowania.
- Jako dodatkowe środki ostrożności możesz włączyć usuwanie nietrwałe dla kont magazynu obiektów blob. Po włączeniu tej funkcji usunięty obiekt blob jest oznaczany do usunięcia, ale nie jest natychmiast przeczyszczany. W okresie przejściowym można przywrócić obiekt blob.

**Dowiedz się więcej:**

- Dowiedz się więcej o [usłudze Azure Blob Storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).
- Dowiedz się, jak [utworzyć migawkę obiektu BLOB](https://docs.microsoft.com/azure/storage/blobs/storage-blob-snapshots).
- [Przegląd przykładowego scenariusza](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) dotyczącego tworzenia kopii zapasowych magazynu obiektów blob.
- [Informacje](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) o usuwaniu nietrwałym.
- [Odzyskiwanie po awarii i wymuszone przechodzenie w tryb failover (wersja zapoznawcza) w usłudze Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-disaster-recovery-guidance)

#### <a name="third-party-backup"></a>Tworzenie kopii zapasowych przez inne firmy

Dodatkowo możesz użyć rozwiązań innych firm do tworzenia kopii zapasowych maszyn wirtualnych i kontenerów magazynu platformy Azure w magazynie lokalnym lub u innych dostawców chmury. Aby uzyskać więcej informacji, zobacz [rozwiązania do tworzenia kopii zapasowych w portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1).

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Konfigurowanie odzyskiwania po awarii dla aplikacji IaaS

Oprócz ochrony danych BCDR planowanie musi uwzględniać sposób utrzymywania dostępności aplikacji i obciążeń w przypadku wystąpienia awarii. W przypadku obciążeń uruchomionych w ramach maszyn wirtualnych IaaS platformy Azure i usługi Azure Storage należy wziąć pod uwagę następujące rozwiązania:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery to podstawowa usługa platformy Azure, która zapewnia, że maszyny wirtualne platformy Azure mogą być dostępne w trybie online, a aplikacje maszyn wirtualnych dostępne w czasie awarii.

Usługa Site Recovery replikuje maszyny wirtualne z podstawowego do pomocniczego regionu platformy Azure. Gdy będzie miała miejsce awaria, maszyny wirtualne przechodzą w tryb failover z regionu podstawowego i są nadal normalnie dostępne w regionie pomocniczym. Gdy awaria zostanie usunięta, maszyny wirtualne mogą powrócić do regionu podstawowego.

  ![Azure Site Recovery ](./media/migrate-best-practices-security-management/site-recovery.png) _Site Recovery_

**Dowiedz się więcej:**

- Przejrzyj [scenariusze odzyskiwania po awarii dla maszyn wirtualnych platformy Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-disaster-recovery-guidance).
- Dowiedz się, jak [skonfigurować odzyskiwanie po awarii dla maszyny wirtualnej platformy Azure po migracji](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-replicate-after-migration).

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Najlepsze rozwiązanie: używanie dysków zarządzanych i zestawów dostępności

Platforma Azure używa zestawów dostępności do logicznego grupowania maszyn wirtualnych i izolowania maszyn wirtualnych w zestawie od innych zasobów. Maszyny wirtualne w zestawie dostępności są rozproszone w wielu domenach błędów z oddzielnymi podsystemami, które chronią przed awariami lokalnymi. Maszyny wirtualne są również rozproszone w wielu domenach aktualizacji, co uniemożliwia jednoczesne ponowne uruchomienie wszystkich maszyn wirtualnych w zestawie.

Usługa Azure Managed disks upraszcza zarządzanie dyskami dla maszyn wirtualnych platformy Azure przez zarządzanie kontami magazynu skojarzonymi z dyskami maszyn wirtualnych.

- W miarę możliwości używaj dysków zarządzanych. Wystarczy określić typ magazynu, który ma być używany, oraz rozmiar potrzebnego dysku, a platforma Azure utworzy dysk i będzie nim zarządzać.
- Istniejące dyski można przekonwertować na dyski zarządzane.
- Aby zapewnić wysoką odporność i dostępność, należy utworzyć maszyny wirtualne w zestawach dostępności. W przypadku wystąpienia planowanych lub nieplanowanych przestojów zestawy dostępności zapewniają, że co najmniej jedna maszyna wirtualna w zestawie pozostaje dostępna.

  ![Dyski zarządzane z dyskami zarządzanymi ](./media/migrate-best-practices-security-management/managed-disks.png)
   _Managed disks_

**Dowiedz się więcej:**

- Zapoznaj się z [omówieniem usługi Managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).
- Dowiedz się więcej [na temat konwertowania dysków na zarządzane](https://docs.microsoft.com/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks).
- Dowiedz się [, jak zarządzać dostępnością maszyn wirtualnych z systemem Windows na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Najlepsze rozwiązanie: monitorowanie użycia i wydajności zasobów

Możliwe, że Twoje obciążenia zostały już przeniesione na platformę Azure, aby móc skorzystać z jej ogromnych możliwości skalowania. Przeniesienie obciążenia nie oznacza jednak, że platforma Azure automatycznie zaimplementuje skalowanie bez Twojego udziału. Przykład:

- Jeśli Twoja organizacja marketingowa publikuje nową reklamę telewizyjną, która powoduje zwiększenie ruchu o 300%, może to spowodować problemy z dostępnością lokacji. Nowo zmigrowane obciążenie może przekroczyć przydzielone limity i ulec awarii.
- Innym przykładem może być rozproszony atak typu „odmowa usługi” (DDoS) względem zmigrowanego obciążenia. W takim przypadku możesz nie chcieć przeprowadzać skalowania, ale zapobiec uzyskaniu dostępu do Twoich zasobów przez źródło ataków.

Te dwa przypadki można rozwiązać na różne sposoby, ale w obu z nich potrzebne są informacje o sytuacji dotyczącej monitorowania użycia i wydajności.

- Usługa Azure Monitor może pomóc Ci w udostępnieniu tych metryk oraz zapewnić odpowiedź z alertami, skalowaniem automatycznym, centrami zdarzeń, aplikacjami logiki i nie tylko.
- Oprócz monitorowania platformy Azure możesz zintegrować aplikację SIEM innej firmy w celu monitorowania dzienników platformy Azure pod kątem zdarzeń inspekcji i wydajności.

  ![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
  _Azure Monitor_

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview).
- [Najlepsze rozwiązania](https://docs.microsoft.com/azure/architecture/best-practices/monitoring) dotyczące monitorowania i diagnostyki.
- Dowiedz się więcej na temat [skalowania](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling)automatycznego.
- Dowiedz się, jak [kierować dane platformy Azure do narzędzia Siem](https://docs.microsoft.com/azure/security-center/security-center-export-data-to-siem).

## <a name="best-practice-enable-diagnostic-logging"></a>Najlepsze rozwiązanie: Włączanie rejestrowania diagnostycznego

Zasoby platformy Azure generują znaczną liczbę metryk rejestrowania i danych telemetrycznych.

- Domyślnie większość typów zasobów nie ma włączonego rejestrowania diagnostycznego.
- Dzięki włączeniu rejestrowania diagnostycznego w ramach zasobów możesz wykonywać zapytania względem danych rejestrowania oraz tworzyć oparte na nich alerty i podręczniki.
- Po włączeniu rejestrowania diagnostycznego każdy zasób będzie miał określony zestaw kategorii. Należy wybrać co najmniej jedną kategorię rejestrowania i lokalizację danych dziennika. Dzienniki mogą być wysyłane do konta magazynu, centrum zdarzeń lub dzienników usługi Azure Monitor.

![Rejestrowanie diagnostyczne](./media/migrate-best-practices-security-management/diagnostics.png)
_Rejestrowanie diagnostyczne_

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [zbierania i używania danych dzienników](https://docs.microsoft.com/azure/azure-monitor/platform/platform-logs-overview).
- [Informacje](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-logs-schema) o tym, co jest obsługiwane podczas rejestrowania diagnostycznego.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Najlepsze rozwiązanie: Konfigurowanie alertów i elementy PlayBook

Gdy funkcja rejestrowania diagnostycznego jest włączona dla zasobów platformy Azure, możesz rozpocząć korzystanie z danych rejestrowania w celu tworzenia alertów niestandardowych.

- Alerty proaktywnie powiadamiają o znalezieniu określonych warunków w danych monitorowania. Dzięki temu możesz rozwiązywać problemy przed zauważeniem ich przez użytkowników. Możesz generować alerty dotyczące takich elementów, jak wartości metryk, zapytania wyszukiwania w dziennikach, zdarzenia dzienników aktywności, kondycja platformy i dostępność witryny internetowej.
- Po wyzwoleniu alertów możesz uruchomić podręcznik aplikacji logiki. Podręcznik pomaga automatyzować i orkiestrować odpowiedź na określony alert. Podręczniki są oparte na aplikacjach Azure Logic Apps. Za pomocą szablonów aplikacji logiki możesz tworzyć podręczniki. Możesz również tworzyć własne podręczniki.
- Prostym przykładem jest utworzenie alertu, który jest wyzwalany w przypadku wystąpienia skanowania portów w ramach sieciowej grupy zabezpieczeń. Możesz skonfigurować podręcznik, który uruchamia i blokuje adres IP, z którego pochodzi skanowanie.
- Innym przykładem może być aplikacja z przeciekiem pamięci. Gdy użycie pamięci dojdzie do określonego punktu, podręcznik może odtworzyć proces.

  ![Alerty](./media/migrate-best-practices-security-management/alerts.png)
  _Alerty_

**Dowiedz się więcej:**

- Dowiedz się więcej o [alertach](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview).
- Dowiedz się więcej na temat [elementy PlayBook zabezpieczeń, które reagują na alerty Security Center](https://docs.microsoft.com/azure/security-center/security-center-playbooks).

## <a name="best-practice-use-the-azure-dashboard"></a>Najlepsze rozwiązanie: korzystanie z pulpitu nawigacyjnego platformy Azure

Witryna Azure Portal to ujednolicona konsola internetowa umożliwiająca tworzenie i monitorowanie wszelkiego rodzaju aplikacji — od prostych aplikacji internetowych po złożone aplikacje w chmurze — oraz zarządzanie nimi. Obejmuje ona dostosowywalny pulpit nawigacyjny oraz opcje ułatwień dostępu.

- Możesz tworzyć wiele pulpitów nawigacyjnych i udostępniać je innym osobom, które mają dostęp do Twoich subskrypcji platformy Azure.
- Dzięki temu udostępnionemu modelowi Twój zespół ma wgląd w środowisko platformy Azure, co umożliwia proaktywne zarządzanie systemami w chmurze.

  ![Pulpit nawigacyjny platformy Azure](./media/migrate-best-practices-security-management/dashboard.png)
  _Pulpit nawigacyjny platformy Azure_

**Dowiedz się więcej:**

- Dowiedz się, jak [utworzyć pulpit nawigacyjny](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards).
- Poznaj [strukturę pulpitu nawigacyjnego](https://docs.microsoft.com/azure/azure-portal/azure-portal-dashboards-structure).

## <a name="best-practice-understand-support-plans"></a>Najlepsze rozwiązanie: Poznaj plany pomocy technicznej

W pewnym momencie konieczna będzie współpraca z pracownikami Twojego działu pomocy technicznej lub pracownikiem pomocy technicznej firmy Microsoft. Posiadanie zestawu zasad i procedur na potrzeby pomocy technicznej podczas scenariuszy, takich jak odzyskiwanie awaryjne, ma kluczowe znaczenie. Ponadto administratorzy i pracownicy działu pomocy technicznej powinni być przeszkoleni w implementowaniu tych zasad.

- W przypadku mało prawdopodobnego zdarzenia, gdy usługa platformy Azure wpływa na obciążenie, administratorzy powinni wiedzieć, w jaki sposób przesłać bilet pomocy technicznej do firmy Microsoft w najbardziej odpowiedni i wydajny sposób.
- Zapoznaj się z różnymi planami pomocy technicznej oferowanymi na platformie Azure. Różnią się one czasem odpowiedzi — od dedykowanego dla wystąpień deweloperskich, do pomocy technicznej pomocy technicznej Premier z czasem odpowiedzi krótszym niż 15 minut.

  ![Plany pomocy technicznej](./media/migrate-best-practices-security-management/support.png)
  _Plany pomocy technicznej_

**Dowiedz się więcej:**

- Zapoznaj się [z omówieniem planów pomocy technicznej systemu Azure](https://azure.microsoft.com/support/options).
- Dowiedz się więcej o [umowach dotyczących poziomu usług (umowy SLA)](https://azure.microsoft.com/support/legal/sla).

## <a name="best-practice-manage-updates"></a>Najlepsze rozwiązanie: Zarządzanie aktualizacjami

Zapewnianie, że na maszynach wirtualnych platformy Azure będzie działać system operacyjny i oprogramowanie w aktualnej wersji, to bardzo trudne zadanie. Możliwość sprawdzenia wszystkich maszyn wirtualnych w celu ustalenia potrzebnych aktualizacji, a następnie automatyczne wypchnięcie tych aktualizacji, jest niezwykle cenna.

- Rozwiązanie Update Management w usłudze Azure Automation służy do zarządzania aktualizacjami systemu operacyjnego dla maszyn z systemami Windows i Linux, które są wdrożone na platformie Azure, lokalnie i u innych dostawcach chmury.
- Użyj rozwiązania Update Management, aby przeprowadzić szybką ocenę stanu dostępnych aktualizacji na wszystkich komputerach agentów i zarządzanie instalacją tych aktualizacji.
- Możesz włączyć rozwiązanie Update Management dla maszyn wirtualnych bezpośrednio z poziomu konta usługi Azure Automation. Możesz również zaktualizować pojedynczą maszynę wirtualną na stronie maszyny wirtualnej w witrynie Azure Portal.
- Ponadto maszyny wirtualne platformy Azure można zarejestrować za pomocą programu System Center Configuration Manager. Następnie możesz przeprowadzić migrację obciążenia programu Configuration Manager na platformę Azure oraz wykonać raportowanie i aktualizacje oprogramowania z poziomu pojedynczego interfejsu internetowego.

  ![Aktualizacje maszyn wirtualnych](./media/migrate-best-practices-security-management/updates.png)
  _Aktualizacje maszyn wirtualnych_

**Dowiedz się więcej:**

- Dowiedz się więcej [na temat zarządzania aktualizacjami na platformie Azure](https://docs.microsoft.com/azure/automation/automation-update-management).
- Dowiedz się, jak [zintegrować Configuration Manager z usługą Update Management](https://docs.microsoft.com/azure/automation/oms-solution-updatemgmt-sccmintegration).
- [Często zadawane pytania](https://docs.microsoft.com/sccm/core/understand/configuration-manager-on-azure) dotyczące programu Configuration Manager na platformie Azure.

## <a name="implement-a-change-management-process"></a>Implementowanie procesu zarządzania zmianami

Podobnie jak w przypadku każdego systemu produkcyjnego wprowadzanie zmiany dowolnego typu może wpłynąć na środowisko. Proces zarządzania zmianami wymagający przesłania żądań w celu wprowadzenia zmian w systemach produkcyjnych jest cennym dodatkiem w zmigrowanym środowisku.

- Możesz utworzyć platformy najlepszych rozwiązań na potrzeby zarządzania zmianami w celu zwiększenia świadomości administratorów i pracowników działu pomocy technicznej.
- Usługa Azure Automation ułatwia zarządzanie konfiguracją i śledzenie zmian na potrzeby zmigrowanych przepływów pracy.
- Podczas wymuszania procesu zarządzania zmianami możesz użyć dzienników inspekcji w celu połączenia dzienników zmian platformy Azure z przypuszczalnie istniejącymi żądaniami zmian. Jeśli więc zobaczysz zmianę bez odpowiadającego jej żądania zmiany, możesz zbadać, dlaczego wystąpił problem w procesie.

Na platformie Azure istnieje rozwiązanie do śledzenia zmian w usłudze Azure Automation:

- Rozwiązanie śledzi zmiany w oprogramowaniu i plikach systemu Windows oraz Linux, kluczach rejestru systemu Windows, usługach systemu Windows i demonach systemu Linux.
- Zmiany na monitorowanych serwerach są wysyłane do usługi Azure Monitor w chmurze w celu przetworzenia.
- Logika jest stosowana do odebranych danych, a usługa w chmurze rejestruje dane.
- Na pulpicie nawigacyjnym rozwiązania Change Tracking można łatwo wyświetlić zmiany wprowadzone w infrastrukturze serwera.

  ![Zarządzanie zmianami](./media/migrate-best-practices-security-management/change.png)
  _Zarządzanie zmianami_

**Dowiedz się więcej:**

- Dowiedz się więcej na temat [Change Tracking](https://docs.microsoft.com/azure/automation/automation-change-tracking).
- Dowiedz się więcej o [możliwościach Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro).

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z innymi najlepszymi rozwiązaniami:

- [Najlepsze rozwiązania](./migrate-best-practices-networking.md) dotyczące sieci po migracji.
- [Najlepsze rozwiązania](./migrate-best-practices-costs.md) dotyczące zarządzania kosztami po migracji.
