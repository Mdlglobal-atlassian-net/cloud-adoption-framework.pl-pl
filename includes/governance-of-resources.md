<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->
> [!NOTE]
>W przypadku zmian wymagań biznesowych funkcja grup zarządzania platformy Azure umożliwia łatwą zmianę organizacji hierarchii zarządzania i przypisań grup subskrypcji. Należy jednak pamiętać, że przypisania zasad i ról zastosowane do grupy zarządzania są dziedziczone przez wszystkie subskrypcje poniżej tej grupy w hierarchii. Jeśli planujesz ponowne przypisywanie subskrypcji między grupami zarządzania, upewnij się, że masz świadomość zmian dotyczących przypisań zasad i ról, które może to powodować. Więcej informacji zawiera [dokumentacja grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups).

### <a name="governance-of-resources"></a>Zarządzanie zasobami

Zestaw zasad globalnych i ról RBAC zapewni poziom odniesienia dotyczący wymuszania ładu. Aby spełnić wymagania dotyczące zasad zespołu ds. zapewnienia ładu w chmurze, wdrożenie produktu o minimalnej wymaganej funkcjonalności utrzymania ładu wymaga wykonania następujących zadań:

1. Zidentyfikowanie definicji usługi Azure Policy niezbędnych do wymuszenia wymagań biznesowych Może to obejmować używanie definicji wbudowanych i tworzenie nowych definicji niestandardowych
2. Utworzenie definicji strategii przy użyciu tych zasad wbudowanych i niestandardowych oraz przypisań ról wymaganych przez produkt o minimalnej wymaganej funkcjonalności utrzymania ładu
3. Globalne zastosowanie zasad i konfiguracji przez przypisanie definicji strategii do wszystkich subskrypcji

#### <a name="identify-policy-definitions"></a>Identyfikowanie definicji zasad

Platforma Azure udostępnia kilka wbudowanych zasad i definicji ról, które można przypisać do dowolnej grupy zarządzania, subskrypcji lub grupy zasobów. Wiele typowych wymagań dotyczących ładu można spełnić za pomocą wbudowanych definicji. Jednak prawdopodobnie będzie też trzeba utworzyć definicje zasad niestandardowych na potrzeby obsługi konkretnych wymagań.

Definicje zasad niestandardowych są zapisywane w grupie zarządzania lub subskrypcji i są dziedziczone w hierarchii grupy zarządzania. Jeśli lokalizacją zapisywania definicji zasad jest grupa zarządzania, definicję zasad można przypisać do dowolnej z podrzędnych grup zarządzania lub subskrypcji tej grupy.

Ponieważ zasady wymagane do obsługi produktu o minimalnej wymaganej funkcjonalności utrzymania ładu mają zastosowanie do wszystkich bieżących subskrypcji, następujące wymagania biznesowe zostaną zaimplementowane przy użyciu połączenia definicji wbudowanych i definicji niestandardowych utworzonych w głównej grupie zarządzania:

1. Ogranicz listę dostępnych przypisań ról do zestawu wbudowanych ról platformy Azure autoryzowanego przez zespół ds. zapewnienia ładu w chmurze. Wymaga to [definicji zasad niestandardowych](https://github.com/azure/azure-policy/tree/master/samples/Authorization/allowed-role-definitions).
2. Wymagaj następujących tagów dla wszystkich zasobów: *Dział/jednostka rozliczeniowa*, _Lokalizacja geograficzna_, _Klasyfikacja danych_, _Krytyczność_, _SLA_, _Środowisko_, _Archetyp aplikacji_, _Aplikacja_ i _Właściciel aplikacji_. Można to zrealizować za pomocą definicji wbudowanej `Require specified tag`.
3. Wymagaj, aby tag `Application` zasobów był zgodny z nazwą odpowiedniej grupy zasobów. Można to zrealizować za pomocą definicji wbudowanej „Wymagaj tagu i jego wartości”.

Informacje na temat definiowania zasad niestandardowych zawiera [dokumentacja usługi Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/create-custom-policy-definition). Aby uzyskać wskazówki i przykłady zasad niestandardowych, skorzystaj z [witryny przykładów usługi Azure Policy](https://docs.microsoft.com/azure/governance/policy/samples) i powiązanego [repozytorium GitHub](https://github.com/azure/azure-policy).

#### <a name="assign-azure-policy-and-rbac-roles-using-azure-blueprints"></a>Przypisywanie zasad usługi Azure Policy i ról RBAC przy użyciu usługi Azure Blueprints

Zasady platformy Azure można przypisywać na poziomie grupy zasobów, subskrypcji i grupy zarządzania. Można je też uwzględniać w definicjach [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview). Mimo że wymagania dotyczące zasad zdefiniowane w tym produkcie o minimalnej wymaganej funkcjonalności utrzymania ładu mają zastosowanie do wszystkich bieżących subskrypcji, bardzo prawdopodobne jest, że przyszłe wdrożenia będą wymagać wyjątków lub alternatywnych zasad. W efekcie przypisanie zasad przy użyciu grup zarządzania, co powoduje dziedziczenie tych przypisań przez wszystkie subskrypcje podrzędne, może nie zapewniać elastyczności wystarczającej do obsługi tych scenariuszy.

Usługa Azure Blueprints umożliwia spójne przypisywanie zasad i ról, stosowanie szablonów usługi Resource Manager oraz wdrażanie grup zasobów w wielu subskrypcjach. Definicje strategii, podobnie jak definicje zasad, są zapisywane w grupach zarządzania lub subskrypcjach. Definicje zasad są dostępne za pośrednictwem dziedziczenia dla wszystkich elementów podrzędnych w hierarchii grupy zarządzania.

Zespół ds. zapewnienia ładu w chmurze zdecydował, że wymuszanie wymaganych zasad usługi Azure Policy i przypisań RBAC w subskrypcjach zostanie wdrożone przy użyciu usługi Azure Blueprints i powiązanych artefaktów:

1. W głównej grupie zarządzania utwórz definicję strategii o nazwie `governance-baseline`.
2. Dodaj następujące artefakty strategii do definicji strategii:
    1. Przypisania zasad dla niestandardowych definicji usługi Azure Policy na najwyższym poziomie grupy zarządzania
    2. Definicje grup zasobów dla wszystkich grup wymaganych w subskrypcjach tworzonych lub zarządzanych przez produkt o minimalnej wymaganej funkcjonalności utrzymania ładu
    3. Standardowe przypisania ról dla wszystkich grup wymaganych w subskrypcjach tworzonych lub zarządzanych przez produkt o minimalnej wymaganej funkcjonalności utrzymania ładu
3. Opublikuj definicję strategii.
4. Przypisz definicję strategii `governance-baseline` do wszystkich subskrypcji.

Więcej informacji na temat tworzenia definicji strategii i korzystania z nich zawiera [dokumentacja usługi Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview).

### <a name="secure-hybrid-vnet"></a>Bezpieczna hybrydowa sieć wirtualna

Określone subskrypcje często wymagają pewnego poziomu dostępu do zasobów lokalnych. Jest to typowe dla scenariuszy migracji lub scenariuszy programowania, w których zależne zasoby znajdują się w lokalnym centrum danych.

Dopóki nie zostanie w pełni ustanowiona relacja zaufania w środowisku chmury, należy ściśle kontrolować i monitorować całą dozwoloną komunikację między obciążeniami w środowisku lokalnym i w chmurze oraz zabezpieczyć sieć lokalną przed potencjalnym nieautoryzowanym dostępem z zasobów opartych na chmurze. W celu zapewnienia obsługi tych scenariuszy do produktu o minimalnej wymaganej funkcjonalności utrzymania ładu dodano następujące najlepsze rozwiązania:

1. Ustanów bezpieczną hybrydową sieć wirtualną w chmurze.
    1. [Architektura referencyjna sieci VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) określa wzorzec i model wdrożenia na potrzeby tworzenia usługi VPN Gateway na platformie VPN.
    2. Upewnij się, że lokalne mechanizmy zabezpieczeń i zarządzania ruchem traktują połączone sieci w chmurze jako niezaufane. Zasoby i usługi hostowane w chmurze powinny mieć dostęp tylko do autoryzowanych usług lokalnych.
    3. Upewnij się, że lokalne urządzenie brzegowe w lokalnym centrum danych jest zgodne z [wymaganiami usługi Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) i jest skonfigurowane do uzyskiwania dostępu do publicznej sieci Internet.
    4. Pamiętaj, że tuneli VPN nie należy traktować jako obwodów gotowych do użycia w warunkach produkcyjnych dla jakichkolwiek obciążeń z wyjątkiem tych najprostszych. Wszystkie obciążenia poza kilkoma najprostszymi wymagającymi łączności lokalnej powinny korzystać z usługi Azure ExpressRoute.
1. W głównej grupie zarządzania utwórz drugą definicję strategii o nazwie `secure-hybrid-vnet`.
    1. Dodaj szablon usługi Resource Manager dla usługi VPN Gateway jako artefakt definicji strategii.
    2. Dodaj szablon usługi Resource Manager dla sieci wirtualnej jako artefakt definicji strategii.
    3. Opublikuj definicję strategii.
1. Przypisz definicję strategii `secure-hybrid-vnet` do wszystkich subskrypcji wymagających łączności lokalnej. Tę definicję należy dodatkowo przypisać do definicji strategii `governance-baseline`.

Jedną z najważniejszych wątpliwości wskazywanych przez zespoły ds. zabezpieczeń IT i zespoły ds. tradycyjnego zarządzania jest ryzyko, że bezpieczeństwo istniejących zasobów zostanie naruszone na wczesnym etapie wdrożenia chmury. Powyższe podejście umożliwia zespołom ds. wdrażania chmury tworzenie i migrowanie rozwiązań hybrydowych przy mniejszym ryzyku dla zasobów lokalnych. Wraz ze wzrostem zaufania do środowiska w chmurze na kolejnych etapach można usunąć to tymczasowe rozwiązanie.

> [!NOTE]
> Powyższe wskazówki stanowią punkt początkowy umożliwiający szybkie utworzenie bazowego produktu o minimalnej wymaganej funkcjonalności utrzymania ładu. Jest to dopiero początek drogi dotyczącej ładu. Dodatkowe zmiany będą potrzebne podczas dalszego wdrażania chmury w firmie związanego z podejmowaniem większego ryzyka w następujących obszarach:
>
> - Obciążenia o krytycznym znaczeniu dla działalności
> - Zabezpieczone dane
> - Zarządzanie kosztami
> - Scenariusze z wieloma chmurami
>
> Ponadto szczegóły tego produktu o minimalnej wymaganej funkcjonalności są oparte na przykładowej drodze fikcyjnej firmy opisanej w kolejnych artykułach. Zdecydowanie zalecamy zapoznanie się z pozostałymi artykułami w tej serii przed zastosowaniem tych najlepszych rozwiązań.
