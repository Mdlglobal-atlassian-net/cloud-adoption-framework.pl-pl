<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="dependent-decisions"></a>Decyzje zależne

Następujące decyzje pochodzą z zespołów poza zespołem nadzoru chmurowego. Implementacja każdego z nich będzie pochodzić z tych samych zespołów. Jednak zespół nadzoru w chmurze jest odpowiedzialny za wdrożenie rozwiązania w celu sprawdzenia, czy te implementacje są spójne.

### <a name="identity-baseline"></a>Punkt odniesienia obsługi tożsamości

Linia bazowa tożsamości to podstawowy punkt początkowy dla całego ładu. Przed podjęciem próby zastosowania ładu należy ustanowić tożsamość. Ustanowiona strategia tożsamości będzie wymuszana przez rozwiązania do zarządzania.
W tym przewodniku ładu zespół zarządzający tożsamości implementuje wzorzec **[synchronizacji katalogu](~/decision-guides/identity/index.md#directory-synchronization)** :

- Kontrola RBAC będzie świadczona przez Azure Active Directory (Azure AD) przy użyciu synchronizacji katalogów lub "tego samego logowania", która została zaimplementowana podczas migracji firmy do pakietu Office 365. Aby uzyskać wskazówki dotyczące implementacji, zobacz [Architektura referencyjna dla integracji z usługą Azure AD](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad).
- Dzierżawa usługi Azure AD będzie również zarządzać uwierzytelnianiem i dostępem do zasobów wdrożonych na platformie Azure.

W ramach ładu SPECJALISTy zespół nadzoru będzie wymuszać stosowanie zreplikowanej dzierżawy za pomocą narzędzi do zarządzania subskrypcjami, omówione w dalszej części tego artykułu. W przyszłych iteracjach zespół nadzoru może również wymusić rozbudowane narzędzia w usłudze Azure AD, aby zwiększyć tę możliwość.

### <a name="security-baseline-networking"></a>Linia bazowa zabezpieczeń: sieć

Sieć definiowana przez oprogramowanie jest ważnym początkowym aspektem linii bazowej zabezpieczeń. Ustanowienie nadzoru SPECJALISTy zależy od wczesnych decyzji z zespołu ds. zarządzania zabezpieczeniami, aby określić sposób bezpiecznego konfigurowania sieci.

Ze względu na brak wymagań zabezpieczenia IT są bezpieczne i wymagają wzorca DMZ w **[chmurze](~/decision-guides/software-defined-network/cloud-dmz.md)** . Oznacza to, że Zarządzanie wdrożeniami platformy Azure będzie bardzo jasne.

- Subskrypcje platformy Azure mogą łączyć się z istniejącym centrum danych za pośrednictwem sieci VPN, ale muszą przestrzegać wszystkich istniejących lokalnych zasad ładu IT związanych z połączeniem strefy zdemilitaryzowana z chronionymi zasobami. Aby uzyskać wskazówki dotyczące wdrażania połączeń sieci VPN, zobacz [Architektura referencyjna sieci VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn).
- Decyzje dotyczące podsieci, zapory i routingu są obecnie odroczone do każdego potencjalnego klienta aplikacji/obciążenia.
- Przed wydaniem jakichkolwiek chronionych danych lub obciążeń o kluczowym znaczeniu jest wymagana dodatkowa analiza.

W tym wzorcu sieci w chmurze mogą łączyć się tylko z zasobami lokalnymi za pośrednictwem istniejącej sieci VPN zgodnej z platformą Azure. Ruch przez to połączenie będzie traktowany jak każdy ruch pochodzący ze strefy zdemilitaryzowana. Aby bezpiecznie obsługiwać ruch z platformy Azure, na lokalnym urządzeniu brzegowym mogą być wymagane dodatkowe uwagi.

Zespół ds. zarządzania chmurą aktywnie zaprosił członków zespołów sieci i zabezpieczeń IT do zwykłych spotkań, aby zachować dostęp do wymagań sieci i zagrożeń.

### <a name="security-baseline-encryption"></a>Linia bazowa zabezpieczeń: szyfrowanie

Szyfrowanie jest kolejną podstawową decyzją w ramach dyscypliny linii bazowej zabezpieczeń. Ponieważ firma aktualnie nie przechowuje żadnych chronionych danych w chmurze, zespół ds. zabezpieczeń zdecydował się na mniej agresywny wzór na potrzeby szyfrowania.
W tym momencie jest sugerowany **[wzorzec w chmurze na potrzeby szyfrowania](~/decision-guides/encryption/index.md#key-management)** , ale nie jest to wymagane w żadnym zespole programistycznym.

- Nie ustawiono żadnych wymagań dotyczących nadzoru dotyczących korzystania z szyfrowania, ponieważ bieżące zasady firmowe nie zezwalają na dane o kluczowym znaczeniu lub chronionych danych w chmurze.
- Przed przystąpieniem do zwalniania danych chronionych lub obciążeń o krytycznym znaczeniu wymagana jest dodatkowa analiza.

## <a name="policy-enforcement"></a>Wymuszanie zasad

Pierwszą decyzją dotyczącą przyspieszenia wdrożenia jest wzorzec do wymuszania. W tym opisie zespół nadzoru zdecydował się zaimplementować wzorzec **[zautomatyzowanego wymuszania](~/decision-guides/policy-enforcement/index.md#automated-enforcement)** .

- Azure Security Center zostaną udostępnione zespołom ds. zabezpieczeń i tożsamości w celu monitorowania zagrożeń bezpieczeństwa. Oba zespoły mogą również używać Security Center do identyfikowania nowych zagrożeń i ulepszania zasad firmowych.
- Kontrola RBAC jest wymagana we wszystkich subskrypcjach w celu zarządzania wymuszeniem uwierzytelniania.
- Azure Policy zostanie opublikowana w każdej grupie zarządzania i zastosowana do wszystkich subskrypcji. Jednak poziom wymuszanych zasad będzie bardzo ograniczony w tym początkowym programie ładu MVP.
- Mimo że są używane grupy zarządzania platformy Azure, oczekiwana jest stosunkowo prosta hierarchia.
- Plany platformy Azure będą używane do wdrażania i aktualizowania subskrypcji przez zastosowanie wymagań RBAC, Menedżer zasobów szablonów i Azure Policy między grupami zarządzania.

## <a name="apply-the-dependent-patterns"></a>Zastosuj wzorce zależne

Następujące decyzje reprezentują wzorce, które mają zostać wymuszone przez strategię wymuszania zasad powyżej:

**Linia bazowa tożsamości.** Plany platformy Azure będą ustawiać wymagania RBAC na poziomie subskrypcji, aby zapewnić, że spójna tożsamość jest skonfigurowana dla wszystkich subskrypcji.

**Linia bazowa zabezpieczeń: sieć.** Zespół zarządzający chmurą utrzymuje Menedżer zasobów szablon służący do ustanowienia bramy sieci VPN między platformą Azure i lokalnym urządzeniem sieci VPN. Gdy zespół aplikacji wymaga połączenia sieci VPN, zespół ds. zarządzania chmurą zastosuje szablon Menedżer zasobów bramy za pośrednictwem planów platformy Azure.

**Linia bazowa zabezpieczeń: szyfrowanie.** W tym momencie żadne wymuszanie zasad nie jest wymagane w tym obszarze. Będzie to oglądany podczas późniejszych iteracji.
