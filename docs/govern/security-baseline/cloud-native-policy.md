---
title: Zasady linii bazowej zabezpieczeń w chmurze
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zasady linii bazowej zabezpieczeń w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9d11dff3ce8900d3dc95e1061af87313eae47a1b
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73752539"
---
# <a name="cloud-native-security-baseline-policy"></a>Zasady linii bazowej zabezpieczeń w chmurze

[Linia bazowa zabezpieczeń](./index.md) jest jednym z [pięciu dyscyplin zarządzania chmurą](../governance-disciplines.md). Ta dyscyplina koncentruje się na ogólnych tematach zabezpieczeń, w tym o ochronie sieci, zasobów cyfrowych, danych itp. Zgodnie z opisem w [przewodniku przegląd zasad](../policy-compliance/cloud-policy-review.md), struktura wdrażania chmury obejmuje trzy poziomy przykładowych zasad: natywne, korporacyjne i chmurowe, które są zgodne z zasadami dla każdej dyscypliny. W tym artykule omówiono przykładowe natywne zasady w chmurze dotyczące dyscypliny linii bazowej zabezpieczeń.

> [!NOTE]
> Firma Microsoft nie jest w stanie podyktować zasad firmowych ani INFORMATYCZNych. Ten artykuł pomoże Ci przygotować się do przeglądu zasad wewnętrznych. Przyjęto założenie, że te przykładowe zasady zostaną rozszerzone, zweryfikowane i przetestowane względem zasad korporacyjnych przed podjęciem próby jej użycia. Użycie tych przykładowych zasad jest niezalecane.

## <a name="policy-alignment"></a>Wyrównanie zasad

Te przykładowe zasady umożliwiają syntezę scenariusza natywnego w chmurze, co oznacza, że narzędzia i platformy udostępniane przez platformę Azure są wystarczające do zarządzania ryzykiem biznesowym związanym z wdrożeniem. W tym scenariuszu przyjęto założenie, że prosta konfiguracja domyślnych usług platformy Azure zapewnia wystarczającą ochronę zasobów.

## <a name="cloud-security-and-compliance"></a>Bezpieczeństwo chmury i jej zgodność z przepisami

Zabezpieczenia są zintegrowane z każdym aspektem platformy Azure, oferując unikatowe zalety zabezpieczeń wynikające z globalnej analizy zabezpieczeń, zaawansowanych kontrolek ukierunkowanych przez klienta oraz bezpiecznej, zaostrzonej infrastruktury. Ta zaawansowana kombinacja pomaga chronić aplikacje i dane, wspierać działania związane z zapewnianiem zgodności oraz udostępniać ekonomiczne zabezpieczenia organizacjom dowolnej wielkości. Takie podejście tworzy silną pozycję początkową dla wszelkich zasad zabezpieczeń, ale nie Negate koniecznie silnych rozwiązań z zakresu bezpieczeństwa związanych z używanymi usługami zabezpieczeń.

### <a name="built-in-security-controls"></a>Wbudowane mechanizmy zabezpieczeń

Trudno jest zachować silną infrastrukturę zabezpieczeń, gdy kontrola zabezpieczeń nie jest intuicyjna i należy ją skonfigurować osobno. Platforma Azure oferuje wbudowane mechanizmy kontroli zabezpieczeń w różnych usługach, które ułatwiają ochronę danych i obciążeń szybko oraz zarządzanie ryzykiem w środowiskach hybrydowych. Zintegrowane rozwiązania partnerskie pozwalają również łatwo przenieść istniejące zabezpieczenia do chmury.

### <a name="cloud-native-identity-policies"></a>Natywne zasady tożsamości w chmurze

Tożsamość staje się nową płaszczyzną kontroli granic dla bezpieczeństwa, przyjmując tę rolę z tradycyjnego ukierunkowanej na sieć. Obwody sieci stają się coraz bardziej porowate i ochrona obwodowa nie może być skuteczna, ponieważ była przed pojawieniuem urządzeń (BYOD) i aplikacjami w chmurze. Usługa Azure Identity Management i kontrola dostępu umożliwiają bezproblemowe i bezpieczny dostęp do wszystkich aplikacji.

Przykładowe zasady natywne w chmurze dotyczące tożsamości w katalogach w chmurze i lokalnych mogą obejmować wymagania podobne do następujących:

- Autoryzowany dostęp do zasobów przy użyciu kontroli dostępu opartej na rolach (RBAC), uwierzytelniania wieloskładnikowego i logowania jednokrotnego (SSO).
- Szybkie łagodzenie tożsamości użytkowników podejrzanych o naruszenie zabezpieczeń.
- Just-in-Time (JIT), przyznany dostęp do poszczególnych zadań, aby ograniczyć narażenie na uprzywilejowane poświadczenia administratora.
- Rozszerzona tożsamość użytkownika i dostęp do zasad w wielu środowiskach za pośrednictwem Azure Active Directory.

Chociaż ważne jest zrozumienie [linii bazowej tożsamości](../identity-baseline/index.md) w kontekście linii bazowej zabezpieczeń, [pięć dyscyplin nadzoru chmurowego](../index.md) wywołuje [linię bazową tożsamości](../identity-baseline/index.md) jako własną dyscyplinę, niezależnie od linii bazowej zabezpieczeń.

### <a name="network-access-policies"></a>Zasady dostępu do sieci

Kontrola sieci obejmuje konfigurację, zarządzanie i zabezpieczanie elementów sieci, takich jak sieci wirtualne, równoważenie obciążenia, DNS i bramy. Kontrolki zapewniają sposób komunikowania się i współpracy usług. Platforma Azure oferuje niezawodną i bezpieczną infrastrukturę sieciową, która obsługuje wymagania dotyczące łączności aplikacji i usług. Możliwe jest połączenie sieciowe między zasobami znajdującymi się na platformie Azure, między zasobami lokalnymi i hostowanymi przez platformę Azure oraz z Internetu i platformy Azure.

Zasady natywne w chmurze dla kontrolek sieci mogą obejmować wymagania podobne do następujących:

- Połączenia hybrydowe z zasobami lokalnymi mogą nie być dozwolone w zasadach natywnych w chmurze. W przypadku niepotrzebnego połączenia hybrydowego przykładem bardziej niezawodnej Zasady zabezpieczeń przedsiębiorstwa będzie bardziej odpowiednie odwołanie.
- Użytkownicy mogą nawiązywać bezpieczne połączenia z platformą Azure i na nim przy użyciu sieci wirtualnych i sieciowych grup zabezpieczeń.
- Natywna Zapora systemu Windows Azure chroni hosty przed złośliwym ruchem sieciowym przez ograniczony dostęp do portów. Dobrym przykładem tych zasad jest wymóg blokowania ruchu (lub nie włączania) bezpośrednio do maszyny wirtualnej za pośrednictwem protokołu SSH/RDP.
- Usługi, takie jak usługa Azure Application Gateway Web Application Firewall (WAF) i Azure DDoS Protection zabezpieczenia aplikacji i zapewniają dostępność dla maszyn wirtualnych działających na platformie Azure. Tych funkcji nie należy wyłączać.

### <a name="data-protection"></a>Ochrona danych

Jednym z kluczy ochrony danych w chmurze jest uwzględnienie możliwych stanów, w których mogą wystąpić dane, oraz tego, jakie kontrolki są dostępne dla każdego stanu. Na potrzeby najlepszych rozwiązań dotyczących zabezpieczeń i szyfrowania danych platformy Azure zalecenia są skoncentrowane na następujących stanach danych:

- Formanty szyfrowania danych są wbudowane w usługi z maszyn wirtualnych do magazynu i SQL Database.
- Dane przenoszone między chmurami i klientami mogą być chronione przy użyciu standardowych protokołów szyfrowania.
- Azure Key Vault pozwala użytkownikom chronić i kontrolować klucze kryptograficzne, hasła, ciągi połączeń i certyfikaty używane przez aplikacje i usługi w chmurze.
- Azure Information Protection ułatwia klasyfikowanie, etykietowanie i ochronę poufnych danych w aplikacjach.

Chociaż te funkcje są wbudowane w platformę Azure, każda z powyższych elementów wymaga konfiguracji i może zwiększyć koszty. Wyrównanie każdej funkcji natywnej w chmurze z [strategią klasyfikacji danych](../policy-compliance/data-classification.md) jest wysoce zalecane.

### <a name="security-monitoring"></a>Monitorowanie zabezpieczeń

Monitorowanie zabezpieczeń jest aktywną strategią, która przeprowadza inspekcję zasobów, aby identyfikować systemy, które nie spełniają standardów organizacyjnych lub najlepszych rozwiązań. Azure Security Center zapewnia ujednoliconą linię bazową zabezpieczeń i zaawansowaną ochronę przed zagrożeniami w ramach obciążeń chmury hybrydowej. Za pomocą Security Center można stosować zasady zabezpieczeń w ramach obciążeń, ograniczać podatność na zagrożenia oraz wykrywać ataki i reagować na nie, w tym:

- Ujednolicony widok zabezpieczeń we wszystkich obciążeniach lokalnych i w chmurze z Azure Security Center.
- Ciągłe monitorowanie i oceny zabezpieczeń, aby zapewnić zgodność i skorygować wszelkie luki w zabezpieczeniach.
- Interaktywne narzędzia i kontekstowe analizy zagrożeń w celu usprawnienia badania.
- Obszerne rejestrowanie i integracja z istniejącymi informacjami o zabezpieczeniach.
- Zmniejsza potrzebę korzystania z kosztownych, niezintegrowanych rozwiązań z zakresu zabezpieczeń.

### <a name="extending-cloud-native-policies"></a>Rozszerzanie zasad natywnych w chmurze

Korzystanie z chmury może obniżyć część obciążeń związanych z zabezpieczeniami. Firma Microsoft zapewnia fizyczne zabezpieczenia centrów danych platformy Azure i pomaga chronić platformę w chmurze przed zagrożeniami związanymi z infrastrukturą, takimi jak atak DDoS. Z uwagi na to, że firma Microsoft ma tysiące specjalistów cyberbezpieczeństwa pracujących nad bezpieczeństwem codziennie, zasoby wykrywające, zapobiegające lub zmniejszają cyberattacks są istotne. W rzeczywistości organizacje używane do obaw o to, czy chmura była zabezpieczona, a teraz wiedzą, że poziom inwestycji w osoby i wyspecjalizowane infrastruktury podejmowane przez dostawców, takich jak firma Microsoft, ułatwiają bezpieczniejsze korzystanie z chmury niż większość lokalnych centrów danych.
Korzystanie z chmury może obniżyć część obciążeń związanych z zabezpieczeniami. Firma Microsoft zapewnia fizyczne zabezpieczenia centrów danych platformy Azure i pomaga chronić platformę w chmurze przed zagrożeniami związanymi z infrastrukturą, takimi jak atak DDoS. Z uwagi na to, że firma Microsoft ma tysiące specjalistów cyberbezpieczeństwa pracujących nad bezpieczeństwem codziennie, zasoby wykrywające, zapobiegające lub zmniejszają cyberattacks są istotne. W rzeczywistości organizacje używane do obaw o to, czy chmura była zabezpieczona, a teraz wiedzą, że poziom inwestycji w osoby i wyspecjalizowane infrastruktury podejmowane przez dostawców, takich jak firma Microsoft, ułatwiają bezpieczniejsze korzystanie z chmury niż większość lokalnych centrów danych.

Nawet w przypadku inwestycji w natywną w chmurze linię bazową zabezpieczeń zaleca się, aby wszystkie zasady linii bazowej zabezpieczeń rozszery domyślne zasady w chmurze. Poniżej przedstawiono przykłady zasad rozszerzonych, które należy wziąć pod uwagę, nawet w środowisku macierzystym w chmurze:

- **Zabezpieczanie maszyn wirtualnych.** Zabezpieczenia powinny mieć najwyższy priorytet w każdej organizacji i wydajnie wymagają kilku rzeczy. Należy ocenić stan zabezpieczeń, chronić przed zagrożeniami bezpieczeństwa, a następnie szybko wykrywać zagrożenia i reagować na nie.
- **Ochrona zawartości maszyny wirtualnej.** Konfigurowanie zwykłych zautomatyzowanych kopii zapasowych jest niezbędne do ochrony przed błędami użytkowników. Jest to niewystarczające, chociaż należy również upewnić się, że kopie zapasowe są bezpieczne z cyberattacks i są dostępne, gdy będą potrzebne.
- **Monitorowanie aplikacji.** Ten wzorzec obejmuje kilka zadań, w tym uzyskiwanie wglądu w kondycję maszyn wirtualnych, zrozumienie interakcji między nimi oraz ustanawianie sposobów monitorowania aplikacji uruchamianych przez te maszyny wirtualne. Wszystkie te zadania są niezbędne do utrzymywania działania aplikacji na zegarie.
- **Zabezpiecz i Przeprowadź inspekcję dostępu do danych.** Organizacje powinny przeprowadzać inspekcję całego dostępu do danych i korzystać z zaawansowanych funkcji uczenia maszynowego, aby wywoływać odchylenia od zwykłych wzorców dostępu.
- **Tryb failover.** Operacje w chmurze, które mają niską tolerancję dla niepowodzenia, muszą mieć możliwość przełączenia w tryb failover lub odzyskania z cyberbezpieczeństwa lub zdarzenia platformy. Te procedury nie mogą być po prostu udokumentowane, ale powinny być rozłożone kwartalnie.

## <a name="next-steps"></a>Następne kroki

Po zapoznaniu się z przykładowymi zasadami odniesienia zabezpieczeń dla rozwiązań natywnych w chmurze Wróć do [przewodnika po przeglądzie zasad](../policy-compliance/cloud-policy-review.md) , aby rozpocząć Kompilowanie tego przykładu w celu utworzenia własnych zasad wdrożenia chmury.

> [!div class="nextstepaction"]
> [Tworzenie własnych zasad przy użyciu przewodnika przeglądu zasad](../policy-compliance/cloud-policy-review.md)
