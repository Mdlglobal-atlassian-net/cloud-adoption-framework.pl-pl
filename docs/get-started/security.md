---
title: 'Wprowadzenie: Zabezpieczanie środowiska przedsiębiorstwa'
description: Rozpocznij integrowanie zabezpieczeń w kluczowych punktach w trakcie działań i operacji związanych z wdrażaniem w chmurze.
author: JanetCThomas
ms.author: janet
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 0ea7caddcc0bcc6e5f2564c2833341b54b9347e3
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83752258"
---
<!-- cSpell:ignore CISO passwordless -->

# <a name="get-started-implement-security-across-the-enterprise-environment"></a>Wprowadzenie: implementowanie zabezpieczeń w środowisku przedsiębiorstwa

Zabezpieczenia pomagają w tworzeniu gwarancji poufności, integralności i dostępności dla firmy. Wysiłki w zakresie zabezpieczeń mają krytyczne znaczenie dla ochrony przed potencjalnym wpływem operacji spowodowanych przez wewnętrzne i zewnętrzne złośliwe i niezamierzone działania. 

Ten przewodnik wprowadzający zawiera opis kluczowych kroków, które spowodują złagodzenie lub uniknięcie ryzyka biznesowego przed atakami cyberbezpieczeństwa. Może to pomóc w szybkim ustaleniu podstawowych praktyk związanych z bezpieczeństwem w chmurze i zintegrowaniu zabezpieczeń z procesem wdrażania chmury.

Kroki przedstawione w tym przewodniku są przeznaczone dla wszystkich ról, które obsługują gwarancje zabezpieczeń w środowiskach chmurowych i strefach wypełniania. Zadania obejmują priorytetowe natychmiastowe Łagodzenie ryzyka, wskazówki dotyczące tworzenia nowoczesnej strategii zabezpieczeń, operacjonalizowania podejście i wykonywania tej strategii.

Ten przewodnik zawiera elementy z platformy wdrażania Microsoft Cloud dla platformy Azure:

![Wprowadzenie do zabezpieczeń przedsiębiorstwa](../_images/get-started/security-map.png)

Przestrzeganie kroków opisanych w tym przewodniku pomoże zintegrować zabezpieczenia w krytycznych punktach w procesie. Celem jest uniknięcie przeszkód wdrażania w chmurze i zmniejszenie niepotrzebnego zakłócenia biznesowego lub operacyjnego.

Firma Microsoft oferuje wbudowane możliwości i zasoby ułatwiające przyspieszenie wdrożenia tych wskazówek dotyczących zabezpieczeń w Microsoft Azure. Zobaczysz te zasoby, do których odwołuje się w tym przewodniku. Są one zaprojektowane w celu ułatwienia ustalenia, monitorowania i wymuszania zabezpieczeń oraz są często aktualizowane i analizowane.

Na poniższym diagramie przedstawiono całościowe podejście do korzystania ze wskazówek dotyczących zabezpieczeń i narzędzi platformy w celu zapewnienia widoczności i kontroli nad zasobami w chmurze na platformie Azure. Zalecamy takie podejście.

![Diagram zabezpieczeń](../_images/security/security-diagram.png)

Poniższe kroki służą do planowania i wykonywania strategii zabezpieczania zasobów w chmurze i korzystania z chmury w celu modernizacji operacji zabezpieczeń.

## <a name="step-1-establish-essential-security-practices"></a>Krok 1. ustanawianie podstawowych praktyk związanych z bezpieczeństwem

Zabezpieczenia w chmurze zaczynają się od rozwiązań dźwiękowych. Bez względu na to, czy pracujesz już w chmurze, czy planujesz w przyszłości, ważne jest, aby szybko ustalić podstawowe rozwiązania w zakresie zabezpieczeń.

Oprócz spełnienia wszelkich jawnych wymagań dotyczących zgodności z przepisami zaleca się wykonanie następujących kroków, aby sprostać najważniejszym wyzwaniom związanym z bezpieczeństwem, które w miarę poruszania się w chmurze.

**Elementy dostarczane i pomocnicze wskazówki:**

- **Techniczne:** Ograniczanie najważniejszych zagrożeń i zwiększanie widoczności i kontroli zasobów przez włączenie bezhaseł lub uwierzytelniania wieloskładnikowego dla administratorów i włączenie ochrony przed zagrożeniami dla zasobów w chmurze.
  - [Uwierzytelnianie wieloskładnikowe lub niewieloskładnikowe dla administratorów](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#passwordless-or-multi-factor-authentication-for-admins)
  - [Operacje zabezpieczeń](https://docs.microsoft.com/azure/architecture/framework/security/security-operations) i [Ochrona przed zagrożeniami w programie Azure Security Center](https://docs.microsoft.com/azure/security-center/threat-protection)
- **Proces:** Zapewnij szybkie decyzje dotyczące zabezpieczeń i ciągłe ulepszanie, przypisując role zabezpieczeń i obowiązki oraz ustanawiając proces odpowiedzi na zdarzenia.
  - [Jasne linie odpowiedzialności](https://docs.microsoft.com/azure/architecture/framework/security/governance#clear-lines-of-responsibility), [przypisywanie uprawnień do zarządzania środowiskiem](https://docs.microsoft.com/azure/architecture/framework/security/governance#assign-privileges-for-managing-the-environment)i operacjonalizować zabezpieczeń <!-- TODO: Improve this and add link to AAF article -->
  - Role i obowiązki zabezpieczeń <!-- TODO: add link to bookmark -->
  - [Przewodnik odwołuje się do odpowiedzi na zdarzenia](https://aka.ms/irrg)
- **Osoby:** Zapewnienie zespołów zabezpieczeń z edukacją, narzędziami i dostępem wymaganym do pomyślnego wdrożenia i działania podczas przejścia do środowiska chmury.
  - Zainformuj **wszystkich o koncepcji** rozwoju zabezpieczeń chmury i chmury:
    - [Ewolucja środowiska zagrożeń, ról i strategii cyfrowych](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
    - [Przekształcanie zabezpieczeń, strategii, narzędzi i zagrożeń](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
  - **Uczenie personelu technicznego** dotyczącego szczegółowych informacji technicznych na temat możliwości zabezpieczeń chmury dla platform, których używają. Firma Microsoft zapewnia obszerną [dokumentację zabezpieczeń platformy Azure](https://docs.microsoft.com/azure/security).
- **Długoterminowe decyzje dotyczące architektury:** Ustanowienie długoterminowej podstawy z właściwymi decyzjami. Są one trudne i kosztowne do późniejszej zmiany.
  - [Utwórz strategię segmentacji przedsiębiorstwa i Wyrównaj do niej architektury techniczne (segmentacja sieci, segmentacja tożsamości itp.)](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)
  - [Pojedynczy Katalog przedsiębiorstwa](https://docs.microsoft.com/azure/architecture/framework/security/identity#single-enterprise-directory)
  - [Strategia uwierzytelniania dla usług](https://docs.microsoft.com/azure/architecture/framework/security/applications-services#prefer-identity-authentication-over-keys)
  - [Strategia przypisywania uprawnień](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#avoid-granular-and-custom-permissions)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze <br><br><br> | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

W tym początkowym kroku zespół nadzoru powinien również rozpocząć koordynację tworzenia linii bazowych zabezpieczeń, które mogą być monitorowane, zarządzane i wymuszane w różnych środowiskach. Dodatkowe wskazówki dotyczące tworzenia tego programu opisano w dalszej części kroku 4.

> [!NOTE]
> Każda organizacja powinna definiować własne standardy minimalne. Stan ryzyka i dalsza tolerancja dla tego ryzyka może się znacznie różnić w zależności od branży, kultury i innych czynników. Na przykład bank może nie tolerować żadnego potencjalnego uszkodzenia swojej reputacji od nawet drobnego ataku na system testowy. Niektóre organizacje mogą w niewoli zatwierdzić to samo zagrożenie, jeśli przyspieszą transformację cyfrową o trzy do sześciu miesięcy.

## <a name="step-2-modernize-the-security-strategy"></a>Krok 2. modernizacja strategii zabezpieczeń

Efektywne zabezpieczenia w chmurze wymagają strategii, która odzwierciedla bieżące środowisko zagrożeń i charakter platformy w chmurze, która jest hostem zasobów przedsiębiorstwa. Przejrzysta strategia usprawnia wysiłki wszystkich zespołów, aby zapewnić bezpieczne i zrównoważone środowisko chmury przedsiębiorstwa. Strategia zabezpieczeń musi umożliwiać zdefiniowanie wyników działalności biznesowej, ograniczyć ryzyko do akceptowalnego poziomu i zapewnić produktywność pracowników.

Strategia zabezpieczeń w chmurze zawiera wskazówki dla wszystkich zespołów pracujących nad technologią, procesami i gotowością użytkowników do tego wdrożenia. Strategia powinna informować o architekturze i możliwościach chmury oraz o architekturze i możliwościach związanych z bezpieczeństwem oraz mieć wpływ na szkolenia i edukację zespołów.

**Dostarczane**

Krok strategii powinien skutkować dokumentem, który można łatwo komunikować z wieloma uczestnikami w organizacji. Uczestnicy projektu mogą potencjalnie obejmować kierownictwo zespołu lidera organizacji.

Zalecamy przechwycenie strategii w prezentacji, aby ułatwić łatwą dyskusję i aktualizowanie. Ta prezentacja może być obsługiwana w dokumencie, w zależności od kultury i preferencji.

- **Prezentacja strategii:** Może istnieć jedna Prezentacja strategii lub można również utworzyć zbiorcze wersje dla odbiorców lidera.
  - **Pełna Prezentacja:** Powinno to obejmować pełny zestaw elementów strategii zabezpieczeń w głównej prezentacji lub w opcjonalnych slajdach odwołań.
  - **Podsumowania Executive:** Wersje, które mają być używane z wyższym kierownictwem i członkami zarządu mogą zawierać tylko krytyczne elementy istotne dla ich roli, takie jak akceptowalnego poziomu ryzyka, najważniejsze priorytety lub akceptowane ryzyka.
- Możesz również rejestrować motywacje, wyniki i uzasadnienia biznesowe w ramach [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

**Najlepsze rozwiązania dotyczące tworzenia strategii zabezpieczeń:**

Programy udane zawierają te elementy w procesie strategii zabezpieczeń:

- **Dopasuj ścisłą strategię biznesową:** Karta zabezpieczeń ma chronić wartość biznesową. W tym celu należy dostosować wszystkie działania związane z zabezpieczeniami i zminimalizować konflikt wewnętrzny.
  - **Twórz wspólne informacje** o biznesie, IT i wymaganiach dotyczących zabezpieczeń.
  - Przede wszystkim należy **zintegrować zabezpieczenia** z wdrożeniem w chmurze, aby uniknąć sytuacji, w której przede wszystkim nie wystąpią zagrożenia.
  - **Użyj podejścia Agile** do natychmiastowego ustanowienia minimalnych wymagań dotyczących zabezpieczeń i ciągłego ulepszania zabezpieczeń w czasie.
  - **Zachęcaj do zmiany w kulturze bezpieczeństwa** dzięki zamierzonym aktywnym akcjom lidera.

  Aby uzyskać więcej informacji, zobacz [przekształcenia, mindsets i oczekiwania](../strategy/define-security-strategy.md#transformations-mindsets-and-expectations).

- **Modernizacja strategii zabezpieczeń:** Strategia zabezpieczeń powinna obejmować zagadnienia dotyczące wszystkich aspektów nowoczesnego środowiska technologicznego, obecnego zagrożenia i bezpieczeństwa zasobów społecznościowych.
  - **Dostosuj do współużytkowanego modelu odpowiedzialności** w chmurze.
  - **Uwzględnij wszystkie typy chmur i wdrożenia w chmurze**.
  - **Preferuj natywne kontrolki chmurowe** , aby uniknąć niepotrzebnych i szkodliwych problemów.
  - **Zintegruj społeczność zabezpieczeń** , aby zachować aktualność rozwoju osoby atakującej.

**Powiązane zasoby dla dodatkowego kontekstu:**

- [Ewolucja środowiska zagrożeń, ról i strategii cyfrowych](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
- [Przekształcanie zabezpieczeń, strategii, narzędzi i zagrożeń](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
- Zagadnienia dotyczące strategii dotyczące struktury wdrażania w chmurze:
  - [Modernizacja strategii zabezpieczeń](../strategy/define-security-strategy.md#modernize-your-security-strategy)
  - [Odporność cyberbezpieczeństwa](../strategy/define-security-strategy.md#cybersecurity-resilience)
  - [Jak chmura zmienia relacje zabezpieczeń i obowiązki](../strategy/define-security-strategy.md#how-the-cloud-is-changing-security)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół liderów zabezpieczeń (Dyrektor ds. bezpieczeństwa informacji (CISO) lub równoważny) | <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

**Zatwierdzanie strategii:** 

Te strategie powinny zostać zatwierdzone przez kierownictwo i liderów firmy z odpowiedzialnością za wyniki lub ryzyko związane z liniami biznesowymi w organizacji. Ta grupa może obejmować tablicę dyrektorów, w zależności od organizacji.

## <a name="step-3-develop-a-security-plan"></a>Krok 3. opracowywanie planu zabezpieczeń

Planowanie powoduje, że strategia zabezpieczeń jest wykonywana przez definiowanie wyników, punktów kontrolnych, osi czasu i właścicieli zadań. Ten plan zawiera również opis ról i obowiązków zespołów.

Planowanie zabezpieczeń i Planowanie wdrażania chmury nie powinno być wykonywane w izolacji. Ważne jest, aby zapraszać zespół ds. zabezpieczeń w chmurze na wczesne cykle planowania, aby uniknąć przestojów w pracy lub zwiększyć ryzyko związane z wykryciem zbyt późnych problemów z zabezpieczeniami. Planowanie zabezpieczeń najlepiej sprawdza się wraz ze szczegółowymi wiedzą i świadomością dotyczącą cyfrowego podpisywania oraz istniejącym portfolio IT, który pochodzi z pełnego zintegrowania z procesem planowania chmury.

**Dostarczane**

- **Plan zabezpieczeń:** Plan zabezpieczeń powinien być częścią głównej dokumentacji dotyczącej planowania chmury. Może to być dokument korzystający z [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), szczegółowego slajdu slajdów lub pliku projektu. Lub może być kombinacją tych formatów, w zależności od wielkości, kultury i standardowych praktyk organizacji.

  Plan zabezpieczeń powinien obejmować wszystkie z tych elementów:

  - **Plan funkcji organizacyjnych**, dzięki czemu zespoły wiedzą, w jaki sposób bieżące role zabezpieczeń i obowiązki zmieniają się wraz z przejściem do chmury.
  - W **planie umiejętności związanych z bezpieczeństwem** należy wspierać członków zespołu podczas nawigowania po znaczących zmianach technologicznych, rolach i obowiązków.
  - **Techniczne Omówienie architektury zabezpieczeń i możliwości** , które ułatwiają zespołom technicznym.
  Firma Microsoft udostępnia architektury referencyjne i możliwości technologiczne, które ułatwiają tworzenie architektury i planu, w tym:
    - [Usługa Azure Components i Model referencyjny](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) umożliwiające przyspieszenie planowania i projektowania ról zabezpieczeń platformy Azure.

      ![Model administrowania platformą Azure](../_images/security/azure-administration-model.png)
      
      ![Model RBAC platformy Azure](../_images/security/azure-rbac-model.png)
    - [Architektura referencyjna programu Microsoft cyberbezpieczeństwae](https://aka.ms/mcra) w celu utworzenia architektury cyberbezpieczeństwa dla przedsiębiorstwa hybrydowego, które obejmuje zasoby lokalne i w chmurze.
    - [Architektura referencyjna centrum operacji zabezpieczeń (SOC)](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks#part-1-introduction---soc-learnings-strategies-and-technical-integration-2430) do modernizacji wykrywania zabezpieczeń, odpowiedzi i odzyskiwania.
    - [Nieufają architekturze referencyjnej dostępu użytkowników](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-3#part-5-zero-trust-user-access-reference-architecture-842) do modernizacji architektury kontroli dostępu dla generacji w chmurze.
    - [Azure Security Center](https://docs.microsoft.com/azure/security-center/) i [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/) , aby zabezpieczyć zasoby w chmurze.
  - **Świadomość bezpieczeństwa i plan edukacji**, dlatego wszystkie zespoły mają podstawową wiedzę o zabezpieczeniach.
  - **Oznaczenie czułości zasobów** do wyznaczania wrażliwych zasobów przy użyciu taksonomii wyrównanej do działania biznesowego. Taksonomia jest tworzona wspólnie przez uczestników współpracy, zespoły ds. zabezpieczeń i inne zainteresowane strony.

- **Zmiany zabezpieczeń w planie chmury:** Zaktualizuj inne sekcje planu wdrażania w chmurze, aby odzwierciedlić zmiany wyzwalane przez plan zabezpieczeń.

**Najlepsze rozwiązania dotyczące planowania zabezpieczeń:** Plan zabezpieczeń prawdopodobnie zakończy się niepowodzeniem, jeśli planowanie obejmuje następujące kwestie:

- **Przyjmij środowisko hybrydowe:** Obejmuje to aplikacje SaaS (Software as a Service) i środowiska lokalne. Obejmuje ona również wielu dostawców usług Cloud Infrastructure as (IaaS) i Platform as a Service (PaaS), jeśli ma zastosowanie.
- **Przyjmowanie zabezpieczeń Agile:** Najpierw Ustanów minimalne wymagania dotyczące zabezpieczeń i Przenieś wszystkie elementy niekrytyczne do listy o ustalonej wartości z priorytetem.
Nie powinna to być tradycyjny, szczegółowy plan wynoszący 3-5 lat. Środowisko w chmurze i zagrożeń zmienia się zbyt szybko, aby ten typ planu był użyteczny. Twój plan powinien skupić się na tworzeniu kroków początkowych i końcowych:
  - **Szybki serwer WINS** do natychmiastowego użytku, który zapewni wysoki wpływ przed rozpoczęciem długoterminowych inicjatyw. Ramy czasowe mogą być 3-12 miesięcy, w zależności od kultury organizacyjnej, standardowych praktyk i innych czynników.
  - **Wyczyść wizję** żądanego stanu końcowego, aby Przewodnik po procesie planowania każdego zespołu (co może potrwać wiele lat).
- **Udostępnij plan w szerokim** stopniu: Zwiększ świadomość, opinię od uczestników projektu i skup się na nich.
- **Poznaj strategiczne wyniki:** Upewnij się, że plan jest wyrównany do i osiąga strategiczne wyniki opisane w strategii zabezpieczeń.
- **Ustawianie własności, odpowiedzialności i terminów ostatecznych:** Upewnij się, że właściciele dla każdego zadania są zidentyfikowani i są zaangażowani w wykonywanie tego zadania w określonym przedziale czasu.
- **Nawiąż połączenie z bezpieczeństwem ludzkim:** Zaangażuj ludzi w ten okres transformacji i nowych oczekiwań, wykonując następujące działania:
  - **Aktywnie obsługują transformację członków zespołu** dzięki jasnej komunikacji i szkoleń na:
    - Jakie umiejętności muszą poznać.
    - Dlaczego muszę poznać umiejętności (i korzyści wynikające z tego).
    - Jak uzyskać tę wiedzę (i udostępnić zasoby ułatwiające ich naukę).
  
    Plan można udokumentować przy użyciu [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Możesz też korzystać z [szkoleń z zakresu zabezpieczeń firmy Microsoft](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction) , aby ułatwić edukację członków zespołu.
  - **Zapewnienie świadomości bezpieczeństwa** mającej na celu ułatwienie użytkownikom bezpiecznego połączenia z ich częścią zachowania bezpieczeństwa organizacji.
- **Zapoznaj się z tematami i wskazówkami firmy Microsoft:** Firma Microsoft opublikowała szczegółowe informacje i perspektywy ułatwiające planowanie transformacji w chmurze i nowoczesnej strategii zabezpieczeń. Materiał obejmuje zarejestrowane szkolenia, dokumentację i najlepsze praktyki dotyczące zabezpieczeń oraz zalecane standardy.
  Aby uzyskać wskazówki techniczne ułatwiające tworzenie planu i architektury, zobacz [dokumentację zabezpieczeń firmy Microsoft](https://docs.microsoft.com/security).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Wszelkie zespoły ryzyka w organizacji <li> Centrum w chmurze doskonałości lub środkowe |

**Zatwierdzenie planu zabezpieczeń:** 

Zespół lidera zabezpieczeń (CISO lub równoważny) powinien zatwierdzić plan.

## <a name="step-4-secure-new-workloads"></a>Krok 4. bezpieczne nowe obciążenia

Znacznie łatwiej jest zacząć w stanie bezpiecznym, niż przeprojektowywania zabezpieczenia później do środowiska. Zdecydowanie zalecamy rozpoczęcie od bezpiecznej konfiguracji, aby upewnić się, że obciążenia są migrowane do i opracowywane i testowane w środowisku.

W trakcie implementacji [strefy wyładunkowej](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone) wiele decyzji może mieć wpływ na profile bezpieczeństwa i ryzyka. Zespół ds. zabezpieczeń w chmurze powinien przejrzeć konfigurację strefy wyładunkowej, aby upewnić się, że spełnia on standardy i wymagania dotyczące zabezpieczeń w punktach odniesienia zabezpieczeń organizacji.

**Dostarczane**

- Upewnij się, że nowe strefy wyładunkowe spełniają wymagania dotyczące zgodności i bezpieczeństwa organizacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- **Mieszaj istniejące wymagania i zalecenia dotyczące chmury:** Zacznij od zalecanych wskazówek, a następnie dostosuj je do unikatowych wymagań dotyczących zabezpieczeń. Mamy problemy z próbą wymuszenia istniejących lokalnych zasad i standardów, ponieważ często odwołują się one do nieaktualnej metody lub podejścia do zabezpieczeń. 

  Firma Microsoft opublikowała wskazówki ułatwiające tworzenie linii bazowych zabezpieczeń:
  - [Standardy zabezpieczeń platformy Azure dotyczące strategii i architektury](https://docs.microsoft.com/security/compass/compass): zalecenia dotyczące strategii i architektury, które umożliwiają kształtowanie stan zabezpieczeń środowiska.
  - [Testy wydajnościowe platformy Azure](https://docs.microsoft.com/azure/security/benchmarks/introduction): konkretne zalecenia dotyczące konfiguracji zabezpieczania środowisk platformy Azure.
  - [Szkolenie dotyczące linii bazowej zabezpieczeń platformy Azure](https://docs.microsoft.com/learn/modules/create-security-baselines).
- **Podaj guardrails:** Zabezpieczenia powinny obejmować zautomatyzowane inspekcje zasad i wymuszanie. W przypadku tych nowych środowisk zespoły powinny dążyć do inspekcji i wymuszania linii bazowych zabezpieczeń organizacji. Te wysiłki mogą pomóc zminimalizować nieprzewidziane zabezpieczenia podczas opracowywania obciążeń, a także ciągłej integracji i ciągłego wdrażania (CI/CD) obciążeń.

  Firma Microsoft oferuje kilka natywnych możliwości platformy Azure, które umożliwiają:
  - [Zastrzeżony](https://docs.microsoft.com/azure/security-center/secure-score-security-controls)wskaźnik: Użyj oceny ocenianej stan zabezpieczeń platformy Azure, aby śledzić wysiłki i projekty dotyczące zabezpieczeń w organizacji.
  - [Plany platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/overview): architektzy w chmurze i centralne grupy IT mogą definiować powtarzalny zestaw zasobów platformy Azure, które implementują i stosują standardy, wzorce i wymagania organizacji.
  - [Azure Policy](https://docs.microsoft.com/azure/governance/policy/): jest to podstawa możliwości widoczności i kontroli, z których korzystają inne usługi. Azure Policy jest zintegrowana z [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager), dzięki czemu można przeprowadzać inspekcję zmian i wymuszać zasady dla dowolnego zasobu na platformie Azure przed, w trakcie lub po jego utworzeniu.
- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-security.md): Użyj najlepszych rozwiązań w celu zwiększenia bezpieczeństwa w obrębie strefy docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze | <li> Zespół ds. wdrażania chmury <li> Zespół platformy w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-secure-existing-cloud-workloads"></a>Krok 5. Zabezpieczanie istniejących obciążeń w chmurze

W wielu organizacjach wdrożono już zasoby w środowiskach chmury przedsiębiorstwa bez zastosowania najlepszych rozwiązań w zakresie zabezpieczeń, które zwiększają ryzyko biznesowe.

Po upewnieniu się, że nowe aplikacje i strefy wyładunkowe są zgodne z najlepszymi rozwiązaniami w zakresie bezpieczeństwa, należy skoncentrować się na wprowadzaniu istniejących środowisk do tych samych standardów.

**Dostarczane**

- Upewnij się, że wszystkie istniejące środowiska chmury i strefy wyładunkowe spełniają wymagania dotyczące zgodności i bezpieczeństwa organizacji.
- Przetestuj gotowość operacyjną wdrożeń produkcyjnych przy użyciu zasad dla linii bazowych zabezpieczeń.
- Weryfikuj przestrzeganie wskazówek dotyczących projektowania i wymagania dotyczące zabezpieczeń dla linii bazowych zabezpieczeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Użyj tych samych linii bazowych zabezpieczeń, które zostały skompilowane w [kroku 4](#step-4-secure-new-workloads) jako idealnego stanu. Może być konieczne dostosowanie niektórych ustawień zasad tylko do inspekcji zamiast wymuszania ich.
- Zrównoważ ryzyko związane z działaniem i bezpieczeństwem. Ze względu na to, że te środowiska mogą hostować systemy produkcyjne, które umożliwiają krytyczne procesy biznesowe, może być konieczne stopniowe wdrożenie ulepszeń zabezpieczeń, aby uniknąć ryzyka przestoju operacyjnego.
- Ustalanie priorytetów wykrywania i korygowania zagrożeń bezpieczeństwa przez krytyczne znaczenie biznesowe. Zacznij od obciążeń, które mają duży wpływ na działalność biznesową w przypadku naruszenia zabezpieczeń i obciążeń, które mają wysokie ryzyko.

Aby uzyskać więcej informacji, zobacz [Identyfikowanie i klasyfikowanie aplikacji o krytycznym znaczeniu dla firmy](https://docs.microsoft.com/azure/architecture/framework/security/applications-services?toc=/security/compass/toc.json&bc=/security/compass/breadcrumb/toc.json#identify-and-classify-business-critical-applications).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. wdrażania chmury <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-govern-to-manage-and-improve-security-posture"></a>Krok 6. Zarządzanie Stanami zabezpieczeń i ich ulepszanie

Podobnie jak w przypadku wszystkich nowoczesnych dyscyplin, bezpieczeństwo jest procesem iteracyjnym, który powinien skupić się na ciągłym ulepszaniu. Stan zabezpieczeń może również zaistnieć, jeśli organizacje nie będą w stanie skupić się na tym czasie.

Spójne zastosowanie wymagań dotyczących zabezpieczeń pochodzi z dyscypliny zarządzania dźwięku i zautomatyzowanych rozwiązań. Gdy zespół ds. zabezpieczeń w chmurze definiuje linie bazowe zabezpieczeń, te wymagania powinny zostać poddane inspekcji, aby upewnić się, że są one stosowane spójnie ze wszystkimi środowiskami chmury (i są wymuszane, jeśli ma to zastosowanie).

**Dostarczane**

- Upewnij się, że linie bazowe zabezpieczeń organizacji są stosowane do wszystkich odpowiednich systemów. Inspekcja anomalii przy użyciu [bezpiecznego wyniku](https://docs.microsoft.com/azure/security-center/secure-score-security-controls) lub podobnego mechanizmu.
- Udokumentowanie zasad linii bazowej zabezpieczeń, procesów i wskazówek dotyczących projektu w [szablonie dyscypliny linii bazowej zabezpieczeń](../govern/security-baseline/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Użyj tych samych punktów odniesienia zabezpieczeń i mechanizmów inspekcji, które zostały skompilowane w [kroku 4](#step-4-secure-new-workloads) jako składniki techniczne monitorowania planów bazowych. Uzupełnij te linie bazowe z osobami i kontrolkami procesów, aby zapewnić spójność.
- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z właściwymi [konwencjami nazewnictwa i znakowania](../ready/azure-best-practices/naming-and-tagging.md). [Wymuś konwencje tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags), z określonym naciskiem na znaczniki dotyczące "czułości danych".
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustanawiaj [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="next-steps"></a>Następne kroki

Kroki przedstawione w tym przewodniku pomogły wdrożyć strategię, kontrolę, procesy, umiejętności i kulturę potrzebną do spójnego zarządzania zagrożeniami związanymi z zabezpieczeniami w całym przedsiębiorstwie.
W przypadku kontynuowania trybu działania zabezpieczeń chmury należy wziąć pod uwagę następujące kroki:

- Przejrzyj [dokumentację zabezpieczeń firmy Microsoft](https://docs.microsoft.com/security). Zawiera wskazówki techniczne ułatwiające specjalistom ds. zabezpieczeń tworzenie i ulepszanie strategii cyberbezpieczeństwa, architektury i priorytetów.
- Przejrzyj informacje o zabezpieczeniach [wbudowanej kontroli zabezpieczeń dla usług platformy Azure](https://docs.microsoft.com/azure/security/fundamentals/security-controls).
- Przejrzyj narzędzia i usługi zabezpieczeń platformy Azure w [usługach i technologiach zabezpieczeń dostępnych na platformie Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).
- Przejrzyj [Centrum zaufania firmy Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment). Zawiera obszerne wskazówki, raporty i powiązane dokumenty, które mogą pomóc w wykonywaniu ocen ryzyka w ramach procesów zgodności z przepisami.
- Zapoznaj się z dostępnymi narzędziami innych firm, aby ułatwić spełnienie wymagań dotyczących zabezpieczeń. Zobacz [integrowanie rozwiązań zabezpieczeń w Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).
