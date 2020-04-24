---
title: Refaktoryzacja Team Foundation Server wdrożenie Azure DevOps Services
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak refaktoryzację wdrożenia lokalnego Team Foundation Server (TFS) przez Migrowanie go do Azure DevOps Services na platformie Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 2751965389406262a5d72c9ea9d1a506218826bb
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997868"
---
<!-- cSpell:ignore contosodevmigration contosomigration onmicrosoft visualstudio sourceconnectionstring CONTOSOTFS DACPAC SQLDB SQLSERVERNAME INSTANCENAME azuredevopsmigration validateonly -->

# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Refaktoryzowanie wdrożenia serwera Team Foundation Server do usług Azure DevOps Services

W tym artykule pokazano, jak fikcyjna firma Contoso refaktoryzuje swoje lokalne wdrożenie serwera Team Foundation Server (TFS) przez migrację do usług Azure DevOps Services na platformie Azure. Zespół programistyczny firmy Contoso użył TFS do współpracy zespołowej i kontroli źródła przez pięć ostatnich lat. Teraz firma chce przeprowadzić migrację do rozwiązania chmurowego do programowania, testowania i kontroli źródła. Usługi Azure DevOps Services pomogą im w przejściu do modelu Azure DevOps i tworzeniu nowych aplikacji natywnych dla chmury.

## <a name="business-drivers"></a>Biznesowa siła napędowa

Zespół liderów IT we współpracy z partnerami biznesowymi firmy ustalił cele do osiągnięcia w przyszłości. Partnerzy nie są zbytnio zainteresowani narzędziami i technologiami deweloperskimi, ale uzgodniono następujące punkty:

- **Oprogramowanie:** Niezależnie od podstawowej firmy wszystkie firmy są teraz firmowymi oprogramowaniem, w tym contoso. Kierownictwo jest zainteresowane włączeniem działu IT w proces kierowania firmą poprzez wprowadzanie nowych rozwiązań dla użytkowników i nowych środowisk dla klientów.
- **Wydajność:** Firma Contoso musi usprawnić proces i usunąć niepotrzebne procedury dla deweloperów i użytkowników. Dzięki temu będzie mogła sprawniej spełniać oczekiwania klientów. Firma potrzebuje rozwiązań informatycznych, które pozwolą jej działać szybko, oszczędzając czas i pieniądze.
- **Elastyczność:** Firma Contoso musi reagować na potrzeby biznesowe i szybciej reagować niż w portalu Marketplace, aby zapewnić sukces w globalnej gospodarce. Rozwiązania IT nie mogą ograniczać firmy w działaniu.

## <a name="migration-goals"></a>Cele migracji

Zespół ds. chmury firmy Contoso ustalił cele migracji do usług Azure DevOps Services:

- Zespół potrzebuje narzędzia do migrowania danych do chmury. Jak najmniej procesów powinno być wykonywanych ręcznie.
- Migracja ma obejmować dane elementów roboczych i historię z ostatniego roku.
- Zespół nie chce konfigurować nowych nazw użytkowników i haseł. Wszystkie bieżące przypisania systemowe muszą być zachowane.
- Zespół chce zastąpić kontrolę wersji serwera Team Foundation (TFVC) kontrolą źródła w usłudze Git.
- Przejście do usługi Git będzie "migracją Tip", która importuje tylko najnowszą wersję kodu źródłowego. Nastąpi to podczas przestoju, gdy cała służbowa zostanie zatrzymana w miarę przesuwania kodu. Zespół ma świadomość, że po migracji będzie dostępna tylko aktualna historia gałęzi master.
- Zespół ma pewne obawy odnośnie do tej zmiany i chce przeprowadzić test przed wykonaniem pełnej migracji. Chce zachować dostęp do serwera TFS również po migracji do usług Azure DevOps Services.
- Zespół ma kilka kolekcji i chce zacząć od jednej, zawierającej tylko kilka projektów, aby lepiej poznać cały proces.
- Zespół ma świadomość, że kolekcje serwera TFS mają relację jeden-do-jednego z organizacjami usług Azure DevOps Services, a więc będą mieć wiele adresów URL. Jednak jest to zgodne z aktualnym modelem rozdzielenia baz kodu i projektów.

## <a name="proposed-architecture"></a>Proponowana architektura

- Firma Contoso przeniesie swoje projekty z serwera TFS do chmury i nie będzie już hostować projektów ani funkcji kontroli źródła w środowisku lokalnym.
- Serwer TFS zostanie poddany migracji do usług Azure DevOps Services.
- Obecnie firma Contoso ma jedną kolekcję serwera TFS o nazwie `ContosoDev`, która zostanie przeniesiona do organizacji usług Azure DevOps Services o nazwie `contosodevmigration.visualstudio.com`.
- Projekty, elementy robocze, błędy i iteracje z ostatniego roku zostaną zmigrowane do Azure DevOps Services.
- Firma Contoso będzie używać usługi Azure Active Directory, skonfigurowanej podczas [wdrażania infrastruktury platformy Azure](./contoso-migration-infrastructure.md) na początkowym etapie planowania migracji.

![Architektura scenariusza](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Proces migracji

Firma Contoso przeprowadzi proces migracji w następujący sposób:

1. Wymagane jest znaczące przygotowanie. Najpierw firma Contoso musi uaktualnić implementację TFS do obsługiwanego poziomu. Firma Contoso korzysta obecnie z wersji serwera TFS 2017 Update 3, ale do przeprowadzenia migracji bazy danych jest wymagana obsługiwana wersja 2018 z najnowszymi aktualizacjami.
2. Po uaktualnieniu firma Contoso uruchomi narzędzie do migracji serwera TFS i przeprowadzi walidację kolekcji.
3. Firma Contoso utworzy zestaw plików przygotowania i przeprowadzi próbną migrację.
4. Następnie firma Contoso przeprowadzi kolejną, pełną migrację, obejmującą elementy robocze, błędy, przebiegi i kod.
5. Po migracji firma Contoso przeniesie swój kod z rozwiązania do kontroli wersji serwera Team Foundation do usługi Git.

![Proces migracji](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Wymagania wstępne

Oto elementy, których firma Contoso potrzebuje do realizacji tego scenariusza.

<!-- markdownlint-disable MD033 -->

**Wymagania** | **Uzyskać**
--- | ---
**Subskrypcja platformy Azure** | Firma Contoso utworzyła subskrypcje we wcześniejszym artykule z tej serii. Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Jeśli bezpłatne konto właśnie zostało utworzone, jesteś administratorem subskrypcji i możesz wykonywać wszystkie akcje.<br/><br/> Jeśli używasz istniejącej subskrypcji i nie jesteś jej administratorem, musisz skontaktować się z administratorem w celu uzyskania uprawnień właściciela lub współautora.<br/><br/> Jeśli potrzebujesz bardziej szczegółowych uprawnień, zapoznaj się z [tym artykułem](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infrastruktura platformy Azure** | Firma Contoso skonfigurowała infrastrukturę platformy Azure zgodnie z opisem w artykule [Azure infrastructure for Migration (Infrastruktura platformy Azure wymagana do migracji)](./contoso-migration-infrastructure.md).
**Lokalny serwer TFS** | W środowisku lokalnym musi działać wersja serwera TFS 2018 Update 2 lub musi zostać przeprowadzone uaktualnienie do tej wersji w ramach procesu migracji.

## <a name="scenario-steps"></a>Etapy scenariusza

Firma Contoso przeprowadzi migrację w następujący sposób:

> [!div class="checklist"]
>
> - **Krok 1. Tworzenie konta usługi Azure Storage.** To konto magazynu będzie używane podczas procesu migracji.
> - **Krok 2. Uaktualnianie programu TFS.** Firma Contoso uaktualni wdrożenie do wersji TFS 2018 Update 2.
> - **Krok 3. Weryfikowanie kolekcji.** Firma Contoso przeprowadzi walidację kolekcji serwera TFS w ramach przygotowania do migracji.
> - **Krok 4. Kompilowanie pliku przygotowania.** Firma Contoso utworzy pliki migracji za pomocą narzędzia do migracji serwera TFS.

## <a name="step-1-create-a-storage-account"></a>Krok 1. Tworzenie konta magazynu

1. Administratorzy firmy Contoso tworzą konto magazynu (**contosodevmigration**) w witrynie Azure Portal.
2. Umieszczają je w regionie pomocniczym używanym na potrzeby trybu failover — Środkowe stany USA. Używają standardowego konta ogólnego przeznaczenia z magazynem lokalnie nadmiarowym.

    ![Konto magazynu](./media/contoso-migration-tfs-vsts/storage1.png)

**Potrzebujesz dalszej pomocy?**

- [Wprowadzenie do usługi Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).
- [Utwórz konto magazynu](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

## <a name="step-2-upgrade-tfs"></a>Krok 2. Uaktualnianie TFS

Administratorzy firmy Contoso uaktualniają serwer TFS do wersji TFS 2018 Update 2. Przed rozpoczęciem:

- Pobierają one [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads).
- Sprawdzają [wymagania sprzętowe](https://docs.microsoft.com/azure/devops/server/requirements) i zapoznają się z [informacjami o wersji](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) oraz [potencjalnymi problemami z uaktualnieniem](https://docs.microsoft.com/azure/devops/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).

Administratorzy przeprowadzają uaktualnienie w następujący sposób:

1. Na początek wykonują kopię zapasową serwera TFS (na maszynie wirtualnej VMware) oraz migawkę programu VMware.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. Po uruchomieniu instalatora serwera TFS wybierają lokalizację instalacji. Instalator wymaga dostępu do Internetu.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. Po zakończeniu instalacji zostanie uruchomiony Kreator konfiguracji serwera.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. Po weryfikacji Kreator ukończy uaktualnianie.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. Administratorzy sprawdzają instalację serwera TFS, przeglądając projekty, elementy robocze i kod.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Niektóre uaktualnienia serwera TFS wymagają uruchomienia Kreatora konfigurowania funkcji po zakończeniu uaktualniania. [Dowiedz się więcej](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).

**Potrzebujesz dalszej pomocy?**

Dowiedz się więcej na temat [uaktualniania serwera TFS](https://docs.microsoft.com/azure/devops/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Krok 3. Sprawdzanie poprawności kolekcji TFS

Administratorzy firmy Contoso uruchamiają narzędzie do migracji serwera TFS dla bazy danych kolekcji ContosoDev, aby przeprowadzić jej walidację przed migracją.

1. Pobierają i rozpakowują [narzędzie do migracji serwera TFS](https://www.microsoft.com/download/details.aspx?id=54274). Należy pobrać wersję odpowiednią do uruchomionej wersji aktualizacji serwera TFS. Wersję można sprawdzić w konsoli administracyjnej.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. Uruchamiają narzędzie, aby przeprowadzić walidację, określając adres URL kolekcji projektów:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. Narzędzie zwraca błąd.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. Administratorzy znajdują pliki dziennika w folderze `Logs`, tuż przed lokalizacją narzędzia. Plik dziennika jest generowany dla każdej istotnej walidacji. W pliku `TfsMigration.log` znajdują się najważniejsze informacje.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. Administratorzy znajdują następujący wpis, związany z tożsamością.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. Uruchamiają polecenie `TfsMigrator validate /help` w wierszu polecenia i widzą, że do walidacji tożsamości jest wymagane polecenie `/tenantDomainName`.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. Ponownie uruchamiają polecenie walidacji, dołączając tę wartość wraz z nazwą usługi Azure AD: `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Na wyświetlonym ekranie logowania w usłudze Azure AD wprowadzają poświadczenia użytkownika będącego administratorem globalnym.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. Walidacja przebiega pomyślnie i jest potwierdzona przez narzędzie.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Krok 4. Tworzenie plików migracji

Po zakończeniu walidacji administratorzy firmy Contoso mogą użyć narzędzia do migracji serwera TFS do utworzenia plików migracji.

1. Uruchamiają krok Prepare (Przygotowanie) w tym narzędziu.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep1.png)

    Krok Przygotuj wykonuje następujące czynności:
    - Skanowanie kolekcji w celu znalezienia listy wszystkich użytkowników i wypełnienia dziennika mapowania tożsamości (**IdentityMapLog.csv**).
    - Przygotowanie połączenia z usługą Azure Active Directory w celu znalezienia dopasowań dla wszystkich tożsamości.
    - Firma Contoso wdrożyła już usługę Azure AD i zsynchronizowała ją przy użyciu narzędzia Azure AD Connect, więc w kroku Prepare powinno być możliwe znalezienie pasujących tożsamości i oznaczenie ich jako aktywne.

2. Na wyświetlonym ekranie logowania w usłudze Azure AD administratorzy wprowadzają poświadczenia administratora globalnego.

    ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep2.png)

3. Krok Prepare zostaje ukończony i narzędzie zgłasza pomyślne wygenerowanie plików importu.

    ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep3.png)

4. Administratorzy widzą teraz, że w nowym folderze zostały utworzone pliki IdentityMapLog.csv oraz import.json.

    ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep4.png)

5. Plik import.json określa ustawienia importowania. Są to informacje takie jak wybrana nazwa organizacji oraz dane konta magazynu. Większość pól jest wypełniana automatycznie. Niektóre pola wymagają wprowadzenia danych przez użytkownika. Firma Contoso otwiera plik i dodaje nazwę organizacji usług Azure DevOps Services, która ma zostać utworzona: **contosodevmigration**. W przypadku tej nazwy adres URL usług Azure DevOps Services będzie następujący: **contosodevmigration.visualstudio.com**.

    ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > Organizację należy utworzyć przed migracją, ale można ją zmienić po zakończeniu migracji.

6. Administratorzy przeglądają plik dziennika mapowania tożsamości, zawierający konta, które zostaną przeniesione do usług Azure DevOps Services podczas importowania.

    - Tożsamości aktywne oznaczają tożsamości, które zostaną przekształcone w użytkowników usług Azure DevOps Services po zaimportowaniu.
    - Po migracji te tożsamości otrzymają licencje usług Azure DevOps Services i będą wyświetlane jako użytkownicy w organizacji.
    - Te tożsamości oznaczone są jako **Active** (Aktywne) w kolumnie **Expected Import Status** (Oczekiwany stan po zaimportowaniu) w tym pliku.

    ![Przygotowanie](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Krok 5. Migracja do Azure DevOps Services

Po wykonaniu czynności przygotowawczych administratorzy firmy Contoso mogą przystąpić do migracji. Po migracji sposób kontroli wersji zostanie zmieniony z kontroli wersji serwera Team Foundation na usługę Git.

Przed rozpoczęciem administratorzy wspólnie z zespołem deweloperów planują czas przestoju, w którym kolekcja zostanie przełączona w tryb offline na potrzeby migracji. Proces migracji obejmuje następujące czynności:

1. **Odłączenie kolekcji.** Gdy kolekcja jest dołączona i w trybie online, dane tożsamości związane z tą kolekcją znajdują się w bazie danych konfiguracji serwera TFS. W momencie odłączenia kolekcji od serwera TFS jest wykonywana kopia tych danych tożsamości, pakowana razem z kolekcją w celu przeniesienia. Bez tych danych nie można wykonać importu tożsamości. Zaleca się, aby kolekcja została odłączona do momentu zakończenia importowania, ponieważ nie ma możliwości importowania zmian, które wystąpiły podczas importowania.
2. **Wygenerowanie kopii zapasowej.** Następnym krokiem procesu migracji jest wygenerowanie kopii zapasowej, którą można będzie zaimportować do usług Azure DevOps Services. Pakiety aplikacji warstwy danych (DACPAC) to funkcja programu SQL Server umożliwiająca spakowanie zmian bazy danych w jednym pliku i wdrożenie ich w innych wystąpieniach programu SQL. Można go również przywrócić bezpośrednio do Azure DevOps Services i służy jako metoda pakowania do pobierania danych kolekcji do chmury. Firma Contoso użyje narzędzia SqlPackage.exe do wygenerowania pakietu DACPAC. To narzędzie jest częścią zestawu SQL Server Data Tools.
3. **Przekazywanie do magazynu.** Po utworzeniu pakietu DACPAC należy przekazać go do usługi Azure Storage. Po przekazaniu firma otrzyma sygnaturę dostępu współdzielonego (SAS) umożliwiającą uzyskanie dostępu do magazynu z poziomu narzędzia do migracji serwera TFS.
4. **Uzupełnienie importu.** Firma Contoso może następnie uzupełnić brakujące pola w pliku importu, w tym ustawienie pakietu DACPAC. Aby rozpocząć pracę z nimi, określ, że chcą przeprowadzić import w trybie **suchym** , aby sprawdzić, czy wszystko działa prawidłowo przed pełną migracją.
5. **Wykonaj import suchego przebiegu.** Importy w postaci suchej-uruchomieniowej pomagają w testowaniu migracji kolekcji. Przebiegi suche mają ograniczoną żywotność, dlatego są usuwane przed uruchomieniem migracji produkcyjnej. Przebiegi próbne są usuwane automatycznie po określonym czasie. Informacja o planowanym czasie usunięcia przebiegu próbnego jest zawarta w otrzymanej po zakończeniu importu wiadomości e-mail z komunikatem o powodzeniu. Należy odnotować tę informację i odpowiednio dostosować plan.
6. **Wykonanie migracji produkcyjnej.** Po zakończeniu migracji suchej-Run Administratorzy contoso przeprowadzają ostateczną migrację, aktualizując plik **Import. JSON** i ponownie uruchamiając operację importowania.

### <a name="detach-the-collection"></a>Odłączanie kolekcji

Przed odłączeniem kolekcji administratorzy firmy Contoso wykonują lokalną kopię zapasową programu SQL Server oraz migawkę serwera TFS w programie VMware.

1. W konsoli administracyjnej serwera TFS wybierają kolekcję, która ma zostać odłączona (**ContosoDev**).

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate1.png)

2. Na karcie **General** (Ogólne) wybierają pozycję **Detach Collection** (Odłącz kolekcję).

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate2.png)

3. W kreatorze Detach Team Project Collection (Odłączanie kolekcji projektów zespołowych) w sekcji **Service Message** (Komunikat usługi) wpisują komunikat dla użytkowników, którzy będą próbowali połączyć się z projektami w kolekcji.

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate3.png)

4. W **trakcie odłączania postęp**monitorują postęp, a następnie wybierają pozycję **dalej** po zakończeniu procesu.

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate4.png)

5. W sekcji **Readiness Checks** (Kontrola gotowości) po zakończeniu kontroli wybierają pozycję **Detach** (Odłącz).

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate5.png)

6. Wybierają pozycję **Close** (Zamknij), aby zakończyć.

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate6.png)

7. Kolekcja nie jest już wymieniona w konsoli administracyjnej serwera TFS.

    ![Migrate (Migracja)](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Generowanie pakietu DACPAC

Firma Contoso tworzy kopię zapasową (pakiet DACPAC) do zaimportowania w usługach Azure DevOps Services.

- Do utworzenia pakietu DACPAC jest używane narzędzie SqlPackage.exe z zestawu SQL Server Data Tools. Istnieje wiele wersji programu sqlpackage. exe zainstalowanych z narzędziami SQL Server Data Tools, które znajdują się w folderach z nazwami, takimi jak 120, 130 i 140. Ważne jest, aby użyć odpowiedniej wersji do przygotowania pakietu DACPAC.

- W przypadku wersji serwera TFS 2018 należy użyć narzędzia SqlPackage.exe z folderu o numerze 140 lub wyższym. W przypadku CONTOSOTFS ten plik znajduje się w:`C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140`

Administratorzy firmy Contoso generują pakiet DACPAC w następujący sposób:

1. Otwierają wiersz polecenia i przechodzą do lokalizacji pliku SqlPackage.exe. Wpisują następujące polecenie, aby wygenerować pakiet DACPAC:

    `SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory`

    ![Backup](./media/contoso-migration-tfs-vsts/backup1.png)

2. Po uruchomieniu polecenia zostanie wyświetlony następujący komunikat.

    ![Backup](./media/contoso-migration-tfs-vsts/backup2.png)

3. Administratorzy weryfikują właściwości pliku DACPAC.

    ![Backup](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Przekazywanie pliku do magazynu

Po utworzeniu pliku DACPAC firma Contoso przekazuje go do usługi Azure Storage.

1. Administratorzy pobierają i instalują [Eksplorator usługi Azure Storage](https://azure.microsoft.com/features/storage-explorer).

    ![Upload](./media/contoso-migration-tfs-vsts/backup5.png)

2. Łączą się z subskrypcją i znajdują konto magazynu utworzone na potrzeby migracji (**contosodevmigration**). Tworzą nowy kontener obiektów blob o nazwie **azuredevopsmigration**.

    ![Upload](./media/contoso-migration-tfs-vsts/backup6.png)

3. Wskazują plik DACPAC do przekazania jako blokowy obiekt blob.

    ![Upload](./media/contoso-migration-tfs-vsts/backup7.png)

4. Po przekazaniu pliku wybierają nazwę pliku i polecenie **Generuj sygnaturę dostępu współdzielonego**. Rozszerzają one kontenery obiektów BLOB w ramach konta magazynu, wybierają kontener z plikami importu, a następnie wybierają **sygnaturę dostępu współdzielonego**.

    ![Upload](./media/contoso-migration-tfs-vsts/backup8.png)

5. Zaakceptuj wartości domyślne, a następnie wybierz pozycję **Utwórz**. Umożliwia to dostęp przez 24 godziny.

    ![Upload](./media/contoso-migration-tfs-vsts/backup9.png)

6. Kopiują adres URL sygnatury dostępu współdzielonego, aby móc użyć go w narzędziu do migracji serwera TFS.

    ![Upload](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> Migracja musi nastąpić w dozwolonym przedziale czasu — w przeciwnym razie uprawnienia wygasną.
> Nie należy generować klucza SAS w witrynie Azure Portal. Klucze wygenerowane w ten sposób mają zakres ograniczony do konta i nie można ich użyć do importowania.

### <a name="fill-in-the-import-settings"></a>Uzupełnianie ustawień importu

Wcześniej administratorzy firmy Contoso częściowo wypełnili plik specyfikacji importu (import.json). Teraz muszą dodać pozostałe ustawienia.

Otwierają plik import.json i wypełniają następujące pola:

- **Lokalizacja:** Lokalizacja klucza sygnatury dostępu współdzielonego wygenerowanego powyżej.
- **Dacpac:** Ustaw nazwę pliku DACPAC, który został przekazany do konta magazynu. Rozszerzenie „dacpac” musi zostać uwzględnione.
- **Nieporttype:** Ustaw na DryRun teraz.

![Ustawienia importu](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="perform-a-dry-run-migration"></a>Przeprowadzanie migracji w postaci suchej

Administratorzy firmy Contoso zaczynają przeprowadzić migrację do poziomu suchych danych, aby upewnić się, że wszystko działa zgodnie z oczekiwaniami.

1. Otwierają wiersz polecenia i przechodzą do lokalizacji narzędzia TfsMigration (`C:\TFSMigrator`).
2. W pierwszym kroku wykonują walidację pliku importu. Chcą mieć pewność, że jest poprawnie sformatowany i że klucz SAS działa.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. Walidacja zwraca błąd z informacją, że czas wygaśnięcia klucza SAS powinien być dłuższy.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test1.png)

4. Za pomocą Eksploratora usługi Azure Storage administratorzy tworzą nowy klucz SAS, ustawiając czas wygaśnięcia na siedem dni.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test2.png)

5. Aktualizują plik `import.json` i ponownie uruchamiają walidację. Tym razem walidacja kończy się pomyślnie.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test3.png)

6. Administratorzy uruchamiają przebieg próbny:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Zwracany jest komunikat potwierdzający uruchomienie migracji. Należy odnotować, przez jaki czas będą przechowywane przygotowane dane po przeprowadzeniu przebiegu próbnego.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test4.png)

8. Po wyświetleniu ekranu logowania w usłudze Azure AD należy wprowadzić poświadczenia administratora firmy Contoso.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test5.png)

9. Zostanie wyświetlony komunikat z informacjami o operacji importowania.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test6.png)

10. Po około 15 minutach administratorzy przechodzą do podanego adresu URL i widzą następujące informacje:

     ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test7.png)

11. Po zakończeniu migracji lider zespołu deweloperów firmy Contoso loguje się w usługach Azure DevOps Services, aby sprawdzić, czy próbna migracja przebiegła prawidłowo. Po uwierzytelnieniu w usłudze Azure DevOps Services należy wprowadzić kilka informacji, aby zweryfikować organizację.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test8.png)

12. W usługach Azure DevOps Services lider zespołu deweloperów może zobaczyć, że projekty zostały przeniesione do usług Azure DevOps Services. Jest też widoczna informacja, że organizacja zostanie usunięta za 15 dni.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test9.png)

13. Lider deweloperów otwiera jeden z projektów i otwiera **elementy** > robocze**przypisane do mnie**. W ten sposób można zobaczyć, że dane elementu roboczego zostały przeniesione wraz z danymi tożsamości.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test10.png)

14. Lider zespołu deweloperów sprawdza również inne projekty i kod, aby upewnić się, że kod źródłowy i historia także zostały przeniesione.

    ![Przebieg próbny](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Uruchamianie migracji produkcyjnej

Po zakończeniu przebiegu próbnego administratorzy firmy Contoso mogą przystąpić do migracji produkcyjnej. Usuwają przebieg próbny, aktualizują ustawienia importu i ponownie uruchamiają importowanie.

1. W portalu Azure DevOps Services usuwana jest organizacja w postaci suchego uruchamiania.
2. Aktualizują plik import.json, ustawiając w polu **ImportType** wartość **ProductionRun**.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full1.png)

3. Uruchamiają migrację tak samo, jak w przypadku przebiegu próbnego: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.
4. Zostaje wyświetlony komunikat z potwierdzeniem uruchomienia migracji i ostrzeżeniem, że dane mogą być przechowywane w bezpiecznym obszarze tymczasowym przez maksymalnie siedem dni.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full2.png)

5. Na ekranie logowania w usłudze Azure AD administratorzy wprowadzają poświadczenia administratora firmy Contoso.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full3.png)

6. Zostanie wyświetlony komunikat z informacjami o operacji importowania.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full4.png)

7. Po około 15 minutach administratorzy przechodzą do podanego adresu URL i widzą następujące informacje:

    ![Produkcja](./media/contoso-migration-tfs-vsts/full5.png)

8. Po zakończeniu migracji lider programu contoso dev zaloguje się do Azure DevOps Services, aby sprawdzić, czy migracja działała prawidłowo. Po zalogowaniu klient deweloperów może zobaczyć, że projekty zostały zmigrowane.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full6.png)

9. Lider deweloperów otwiera jeden z projektów i otwiera **elementy** > robocze**przypisane do mnie**. W ten sposób można zobaczyć, że dane elementu roboczego zostały przeniesione wraz z danymi tożsamości.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full7.png)

10. Lider zespołu deweloperów sprawdza też dane innych elementów roboczych w celu potwierdzenia.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full8.png)

11. Lider zespołu deweloperów sprawdza również inne projekty i kod, aby upewnić się, że kod źródłowy i historia także zostały przeniesione.

    ![Produkcja](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Zmiana sposobu kontroli źródła z kontroli wersji serwera Team Foundation na usługę GIT

Po zakończeniu migracji firma Contoso chce zmienić sposób zarządzania kodem źródłowym z kontroli wersji serwera Team Foundation na usługę Git. Administratorzy muszą zaimportować kod źródłowy znajdujący się obecnie w organizacji usług Azure DevOps Services jako repozytoria Git w tej samej organizacji.

1. W portalu usług Azure DevOps Services otwierają jedno z repozytoriów TFVC (**$/PolicyConnect**) i przeglądają je.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. Wybierają listę rozwijaną **Źródło** i pozycję **Importuj**.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. Dla **typu źródła**wybierają **TFVC**i określają ścieżkę do repozytorium. Decydują, że migracja nie będzie obejmowała historii.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Ze względu na różnice w sposobie przechowywania informacji o kontroli wersji pomiędzy kontrolą wersji serwera Team Foundation a usługą Git firma Contoso nie powinna migrować historii. Takie samo podejście zastosowała firma Microsoft podczas migracji systemu Windows i innych produktów z rozwiązania do scentralizowanej kontroli wersji do usługi Git.

4. Po zakończeniu importowania administratorzy przeglądają kod.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. Powtarzają proces dla drugiego repozytorium (**$/SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. Po przejrzeniu kodu źródłowego liderzy zespołu deweloperów uzgadniają, że migracja do usługi Azure DevOps Services została ukończona. Od teraz usługi Azure DevOps Services stanowią źródło dla wszystkich działań deweloperskich w zespołach uczestniczących w migracji.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**Potrzebujesz dalszej pomocy?**

[Dowiedz się więcej](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts) o importowaniu z kontroli wersji serwera Team Foundation.

## <a name="clean-up-after-migration"></a>Czyszczenie zasobów po migracji

Po zakończeniu migracji firma Contoso musi:

- Zapoznać się z informacjami o dodatkowych czynnościach związanych z importowaniem w artykule [Post import (Po imporcie)](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts).
- Usunąć repozytoria TFVC lub przełączyć je w tryb tylko do odczytu. Bazy kodu nie mogą być używane, ale mogą być przywoływane dla swojej historii.

## <a name="post-migration-training"></a>Szkolenie po migracji

Firma Contoso będzie musiała przeszkolić odpowiednich członków zespołów w zakresie korzystania z usług Azure DevOps Services i Git.
