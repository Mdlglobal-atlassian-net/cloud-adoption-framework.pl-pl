---
title: 'Wprowadzenie: Zabezpieczanie środowiska przedsiębiorstwa'
description: Rozpocznij integrowanie zabezpieczeń w kluczowych punktach w trakcie działań i operacji związanych z wdrażaniem w chmurze.
author: JanetCThomas
ms.author: janet
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 3de015250a7fd14e01eb14094e564f51e0425648
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229329"
---
<!-- docsTest:ignore Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template -->

<!-- cSpell:ignore CISO passwordless -->

# <a name="get-started-implementing-security-across-the-enterprise-environment"></a>Wprowadzenie: implementowanie zabezpieczeń w całym środowisku przedsiębiorstwa

Zabezpieczenia umożliwiają firmie poprzez tworzenie gwarancji poufności, integralności i dostępności z krytycznym kątem ochrony przed potencjalnym wpływem na operacje spowodowane przez wewnętrzne i zewnętrzne złośliwe i niezamierzone działania. W tym przewodniku przedstawiono podstawowe kroki, które spowodują złagodzenie lub uniknięcie ryzyka biznesowego przed atakami cyberbezpieczeństwa poprzez szybkie ustanowienie podstawowych praktyk bezpieczeństwa w chmurze i integrację zabezpieczeń z procesem wdrażania chmury.

Kroki przedstawione w tym przewodniku są przeznaczone dla wszystkich ról, które obsługują gwarancje bezpieczeństwa w środowiskach chmury i strefach wypełniania. Dotyczy to zarówno priorytetu natychmiastowego ograniczenia ryzyka, wskazówek dotyczących tworzenia nowoczesnej strategii zabezpieczeń, operacjonalizowania podejścia i wykonywania tej strategii.

W tym przewodniku wprowadzenie uwzględniono różne elementy z platformy wdrażania w chmurze:

![Wprowadzenie do zabezpieczeń przedsiębiorstwa](../_images/get-started/security-map.png)

Zgodnie z krokami w tym przewodniku pomożesz zintegrować zabezpieczenia w krytycznych punktach w procesie, aby uniknąć przeszkód wdrażania w chmurze i ograniczyć niepotrzebne zakłócenia biznesowe lub operacyjne.

Firma Microsoft oferuje wbudowane możliwości i zasoby ułatwiające przyspieszenie wdrożenia tych wskazówek dotyczących zabezpieczeń w odniesieniu do Microsoft Azure (przywoływane w tym dokumencie). Te zasoby zostały zaprojektowane w celu ułatwienia ustalenia, monitorowania i wymuszania zabezpieczeń oraz są często aktualizowane i analizowane.

Ten diagram przedstawia całościowe podejście, które firma Microsoft zaleca w przypadku korzystania ze wskazówek dotyczących zabezpieczeń i narzędzi platformy w celu zapewnienia widoczności i kontroli nad zasobami w chmurze na platformie Azure.

![Diagram zabezpieczeń](../_images/security/security-diagram.png)

Wykonaj następujące kroki, aby zaplanować i wykonać strategię zabezpieczania zasobów w chmurze oraz korzystanie z chmury do modernizacji operacji zabezpieczeń:

## <a name="step-1-establish-essential-security-practices"></a>Krok 1. ustanawianie podstawowych praktyk związanych z bezpieczeństwem

Zabezpieczenia w chmurze zaczynają się od rozwiązań dźwiękowych. Bez względu na to, czy pracujesz już w chmurze, czy planuje się w przyszłości, ważne jest, aby szybko ustanowić podstawowe rozwiązania w zakresie zabezpieczeń.

Oprócz spełnienia wszelkich jawnych wymagań dotyczących zgodności z przepisami zaleca się wykonanie następujących kroków, aby sprostać najważniejszym wyzwaniom związanym z bezpieczeństwem w przypadku przechodzenia do chmury.

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
- **Długoterminowe decyzje dotyczące architektury:** Ustanowienie długoterminowej podstawy z właściwymi decyzjami. Są one bardzo trudne i kosztowne do późniejszej zmiany.
  - [Twórz strategię segmentacji przedsiębiorstwa i wyrównujej z nią architektury techniczne (segmentacja sieci, segmentacja tożsamości itp.)](https://docs.microsoft.com/azure/architecture/framework/security/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)
  - [Pojedynczy Katalog przedsiębiorstwa](https://docs.microsoft.com/azure/architecture/framework/security/identity#single-enterprise-directory)
  - [Strategia uwierzytelniania dla usług](https://docs.microsoft.com/azure/architecture/framework/security/applications-services#prefer-identity-authentication-over-keys)
  - [Strategia przypisywania uprawnień](https://docs.microsoft.com/azure/architecture/framework/security/critical-impact-accounts#avoid-granular-and-custom-permissions)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze <br><br><br> | <li> Zespół strategii chmury <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

W tym początkowym kroku zespół nadzoru powinien również rozpocząć koordynację tworzenia linii bazowych zabezpieczeń, które mogą być monitorowane, zarządzane i wymuszane w różnych środowiskach. Dodatkowe wskazówki dotyczące tworzenia tego programu opisano w sekcji Krok 4 poniżej.

> [!NOTE]
> Każda organizacja powinna definiować własne standardy minimalne, ponieważ stan ryzyka i dalsza tolerancja tego ryzyka może się znacznie różnić w zależności od branży, kultury i innych czynników. Na przykład bank może nie tolerować żadnych potencjalnych szkód dla ich reputacji od nawet drobnego ataku w systemie testowym, w którym niektóre organizacje mogą w niewielkim stopniu zatwierdzić to samo ryzyko w przypadku przyspieszenia przekształcenia cyfrowego o trzy do sześciu miesięcy.

## <a name="step-2-modernize-security-strategy"></a>Krok 2. modernizacja strategii zabezpieczeń

Skuteczne zabezpieczenia w chmurze wymagają solidnej strategii, która odzwierciedla bieżące środowisko zagrożeń i charakter platformy w chmurze, która obsługuje zasoby przedsiębiorstwa. Przejrzysta strategia usprawnia wysiłki wszystkich zespołów, zapewniając bezpieczne i zrównoważone środowisko chmury przedsiębiorstwa, które zmniejsza ryzyko biznesowe. Strategia zabezpieczeń musi umożliwiać zdefiniowanie wyników działalności biznesowej, ograniczyć ryzyko do akceptowalnego poziomu i zapewnić produktywność pracowników.

Strategia zabezpieczeń w chmurze zapewnia jasne wskazówki dla wszystkich zespołów pracujących nad technologią, procesami i gotowością użytkowników do tego wdrożenia. Strategia powinna informować o architekturze i możliwościach chmury oraz o architekturze i możliwościach związanych z bezpieczeństwem oraz mieć wpływ na szkolenia i edukację zespołów.

**Dostarczane**

Krok strategii powinien skutkować dokumentem, który można łatwo przekazać do wielu udziałowców w organizacji, w tym między innymi kierownictwem zespołu liderów organizacji.

Z tego powodu zaleca się przechwycenie strategii w prezentacji, aby ułatwić łatwą dyskusję i aktualizowanie. Może to być również obsługiwane w dokumencie, w zależności od kultury i preferencji.

- **Prezentacja strategii:** Może istnieć jedna Prezentacja strategii lub można również utworzyć zbiorczą wersję dla odbiorców.
  - **Pełna Prezentacja:** Powinno to obejmować pełny zestaw elementów strategii zabezpieczeń w głównej prezentacji lub w opcjonalnych slajdach odwołań.
  - **Podsumowania Executive:** Wersje, które mają być używane z starszymi kierownikami i członkami zarządu, które zawierają tylko krytyczne elementy istotne dla ich roli, takich jak akceptowalnego poziomu ryzyka, najważniejsze priorytety lub akceptowane ryzyka.
- Możesz również rejestrować motywacje, wyniki i uzasadnienie biznesowe w [szablonie strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx).

**Najlepsze rozwiązania dotyczące tworzenia strategii zabezpieczeń:**

Programy udane zawierają te elementy w procesie strategii zabezpieczeń:

- **Dopasuj ścisłą strategię biznesową:** Karta zabezpieczeń ma chronić wartość biznesową, więc ma kluczowe znaczenie dla dopasowania wszystkich wysiłków związanych z zabezpieczeniami do tego celu i zminimalizowania konfliktu wewnętrznego.
  - **Utwórz wspólne zrozumienie:** Wymagań firmy, IT i bezpieczeństwa.
  - **Wczesne integrowanie zabezpieczeń z wdrażaniem w chmurze:** Aby uniknąć ostatnich minut kryzysowych przed uniknięciem zagrożeń.
  - **Podejście Agile:** W celu natychmiastowego ustanowienia minimalnych wymagań dotyczących zabezpieczeń i ciągłego ulepszania zabezpieczeń w czasie.
  - **Zmiana kultury zabezpieczeń:** Dzięki zamierzonym aktywnym akcjom lidera.

Aby uzyskać więcej informacji, zobacz [przekształcenia, mindsets i oczekiwania](../strategy/define-security-strategy.md#transformations-mindsets-and-expectations).

- **Modernizacja strategii zabezpieczeń:** Strategia zabezpieczeń powinna obejmować zagadnienia dotyczące wszystkich aspektów nowoczesnego środowiska technologicznego, obecnego zagrożenia i bezpieczeństwa zasobów społecznościowych.
  - **Dostosuj do współużytkowanego modelu odpowiedzialności** w chmurze.
  - **Uwzględnij wszystkie typy chmur i wielochmurowe.**
  - **Preferuj natywne kontrolki chmurowe** , aby uniknąć niepotrzebnych i szkodliwych problemów.
  - **Integracja z zabezpieczeniami społeczności:** Aby zachować aktualność ewolucji osoby atakującej.

**Powiązane zasoby dla dodatkowego kontekstu:**

- [Ewolucja środowiska zagrożeń, ról i strategii cyfrowych](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#evolution-of-threat-environment-roles--digital-strategies-2004)
- [Przekształcanie zabezpieczeń, strategii, narzędzi i zagrożeń](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#transformation-of-security-strategies-tools--threats-1513)
- Zagadnienia dotyczące strategii dotyczącej architektury wdrażania w chmurze:
  - [Modernizacja strategii zabezpieczeń](../strategy/define-security-strategy.md#modernize-your-security-strategy)
  - [Odporność cyberbezpieczeństwa](../strategy/define-security-strategy.md#cybersecurity-resilience)
  - [Jak chmura zmienia relacje zabezpieczeń i obowiązki](../strategy/define-security-strategy.md#how-the-cloud-is-changing-security)

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół liderów zabezpieczeń (Dyrektor ds. bezpieczeństwa informacji (CISO) lub równoważny) | <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Zespół ds. wdrażania chmury <li> Centrum w chmurze doskonałości lub środkowe |

**Zatwierdzanie strategii:** Kierownictwo i liderzy biznesowi z odpowiedzialnością za wyniki biznesowe lub ryzyka biznesowego w organizacji (mogą to być między innymi Zarząd w zależności od organizacji).

## <a name="step-3-develop-a-security-plan"></a>Krok 3. opracowywanie planu zabezpieczeń

Planowanie powoduje, że strategia zabezpieczeń jest wykonywana przez definiowanie wyników, punktów kontrolnych, osi czasu i właścicieli zadań. Ten plan zawiera również opis ról i obowiązków zespołów.

Planowanie zabezpieczeń i Planowanie wdrażania chmury nie powinno być wykonywane w izolacji. Niezwykle ważne jest, aby zapraszać zespół ds. zabezpieczeń w chmurze na wczesne cykle planowania, aby uniknąć przestojów pracy lub zwiększyć ryzyko związane z wykryciem zbyt późnych problemów z zabezpieczeniami. Planowanie zabezpieczeń najlepiej sprawdza się wraz ze szczegółowymi wiedzą i świadomością dotyczącą cyfrowego podpisywania oraz istniejącym portfolio IT, który pochodzi z pełnego zintegrowania z procesem planowania chmury.

**Dostarczane**

- **Plan zabezpieczeń:** Powinna być częścią głównej dokumentacji dotyczącej planowania dla chmury i może być dokumentem przy użyciu [strategii i szablonu planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx), szczegółowego talii slajdów, pliku projektu lub kombinacji tych formatów w zależności od wielkości, kultury i standardowych praktyk organizacji.

- Plan zabezpieczeń powinien obejmować wszystkie z tych elementów:

  - **Plan funkcji organizacyjnych:** Dlatego zespoły wiedzą, w jaki sposób bieżące role zabezpieczeń i obowiązki zmieniają się w ramach przejścia do chmury.
    - W **planie umiejętności związanych z bezpieczeństwem** należy wspierać członków zespołu podczas nawigowania po znaczących zmianach technologicznych, rolach i obowiązków.
  - **Plan zabezpieczeń i możliwości techniczne:** Do przewodnika zespołów technicznych.
  Firma Microsoft udostępnia architektury referencyjne i możliwości technologiczne, które ułatwiają tworzenie architektury i planów, w tym:
    - [Usługa Azure Components i Model referencyjny](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) umożliwiające przyspieszenie planowania i projektowania ról zabezpieczeń platformy Azure.
      ![Model zarządzania systemu Azure — model ](../_images/security/azure-administration-model.png)
       ![ RBAC Azure](../_images/security/azure-rbac-model.png)
    - [Architektura referencyjna programu Microsoft cyberbezpieczeństwae](https://aka.ms/mcra) , aby utworzyć ogólną architekturę cyberbezpieczeństwa dla przedsiębiorstwa hybrydowego obejmującego zasoby lokalne i w chmurze.
    - [Architektura referencyjna centrum operacji zabezpieczeń (SOC)](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks#part-1-introduction---soc-learnings-strategies-and-technical-integration-2430) do modernizacji wykrywania zabezpieczeń, odpowiedzi i odzyskiwania.
    - [Nieufają architekturze referencyjnej dostępu użytkowników](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-3#part-5-zero-trust-user-access-reference-architecture-842) do modernizacji architektury kontroli dostępu dla generacji w chmurze.
    - [Azure Security Center](https://docs.microsoft.com/azure/security-center/) i usługi [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/) , aby zabezpieczyć zasoby w chmurze.
  - **Świadomość zabezpieczeń i plan edukacji:** ASO wszystkie zespoły mają podstawowe krytyczne informacje o zabezpieczeniach.
  - **Oznaczenie czułości zasobu:** Aby wyznaczyć poufne zasoby przy użyciu taksonomii dopasowanej do wpływu na działalność biznesową (opracowane wspólnie przez zainteresowane strony biznesowe, zespoły ds. zabezpieczeń i inne zainteresowane osoby).

- **Przyjmij środowisko hybrydowe:** Obejmuje to aplikacje SaaS (Software as a Service), środowiska lokalne i wiele infrastruktury chmurowej jako usługi (jeśli dotyczy).
- **Aktualizowanie planu chmury ze zmianami zabezpieczeń:** Zaktualizuj inne sekcje głównego planu wdrażania chmury, aby odzwierciedlić zmiany wyzwalane przez plan zabezpieczeń.

**Najlepsze rozwiązania dotyczące planowania zabezpieczeń:** Plan zabezpieczeń prawdopodobnie zakończy się niepowodzeniem, jeśli planowanie obejmuje następujące kwestie:

- **Wdrażanie zabezpieczeń Agile:** Najpierw Ustanów minimalne wymagania dotyczące zabezpieczeń i Przenieś wszystkie elementy niekrytyczne do listy o ustalonej wartości z priorytetem.
Nie powinna to być tradycyjny szczegółowy plan 3-5 roku, ponieważ środowisko chmury i zagrożeń zmienia zbyt szybko, aby ten typ planu był użyteczny. Twój plan powinien skupić się na tworzeniu kroków początkowych i końcowych:
  - **Szybki serwer WINS:** Szczegółowy plan dla natychmiastowego użytku w celu przechwycenia szybkiego usługi WINS i rozpoczęcia dłuższych inicjatyw, które pozwolą na zapewnienie dużego wpływu. Może to być 3-12 miesięcy w zależności od kultury organizacyjnej, standardowych praktyk i innych czynników.
  - **Wyczyść wizję** żądanego stanu końcowego, aby Przewodnik po procesie planowania każdego zespołu (co może potrwać kilka lat).
- **Udostępnianie planu w szerokim** stopniu: Aby zwiększyć świadomość, opinie od uczestników projektu i kupować je.
- **Poznaj strategiczne wyniki:** Upewnij się, że plan jest wyrównany do i osiąga strategiczne wyniki opisane w strategii zabezpieczeń
- **Własność, odpowiedzialność i terminy:** Upewnij się, że właściciele dla każdego zadania są zidentyfikowani i są zaangażowani w wykonywanie tego zadania w określonym przedziale czasu.
- **Nawiąż połączenie z bezpieczeństwem ludzkim:** Aby zaangażować osoby w ten okres do przekształceń i nowych oczekiwań:
  - **Aktywnie wspierające transformację członków zespołu:** Dzięki jasnej komunikacji i szkoleń na:
    - Jakie umiejętności muszą uczyć się
    - Dlaczego muszą je poznać (i korzyści wynikające z tego)
    - Jak uzyskać tę wiedzę (i udostępnić zasoby ułatwiające ich naukę).
  Można to udokumentować przy użyciu [szablonu strategii i planu](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx) oraz korzystać z [szkoleń dotyczących zabezpieczeń w trybie online firmy Microsoft](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction) , aby ułatwić edukację członków zespołu.
  - Zwróć **uwagę na świadomość zabezpieczeń:** Aby pomóc ludziom w prawdziwym połączeniu z ich częścią zachowania bezpieczeństwa organizacji.
- **Zapoznaj się z tematami i wskazówkami firmy Microsoft:** Firma Microsoft opublikowała szczegółowe informacje i perspektywy, aby pomóc organizacji w planowaniu transformacji na chmurę i nowoczesnej strategii zabezpieczeń, w tym zarejestrowanych szkoleń, dokumentacji i najlepszych praktyk dotyczących zabezpieczeń oraz zalecanych standardów.
  Aby uzyskać wskazówki techniczne ułatwiające tworzenie planu i architektury, zobacz [dokumentację zabezpieczeń firmy Microsoft](https://docs.microsoft.com/security).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze | <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Wszelkie zespoły ryzyka w organizacji <li> Centrum w chmurze doskonałości lub środkowe |

**Zatwierdzenie planu zabezpieczeń:** Zespół lidera zabezpieczeń (CISO lub równoważny).

## <a name="step-4-secure-new-workloads"></a>Krok 4. bezpieczne nowe obciążenia

Znacznie łatwiej jest zacząć w stanie bezpiecznym, niż przeprojektowywania zabezpieczenia później do środowiska. Zdecydowanie zalecamy rozpoczęcie od bezpiecznej konfiguracji, aby upewnić się, że obciążenia są migrowane do i opracowywane i przetestowane w bezpiecznym środowisku.

W trakcie implementacji [strefy wyładunkowej](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone) wiele decyzji może mieć wpływ na profile bezpieczeństwa i ryzyka. Zespół ds. zabezpieczeń w chmurze powinien przejrzeć konfigurację strefy wyładunkowej, aby upewnić się, że spełnia on standardy i wymagania dotyczące zabezpieczeń w punktach odniesienia zabezpieczeń organizacji.

**Dostarczane**

- Upewnij się, że nowe strefy wyładunkowe spełniają wymagania dotyczące zgodności i bezpieczeństwa organizacji.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- **Mieszaj istniejące wymagania i zalecenia dotyczące chmury:** Zacznij od zalecanych wskazówek, a następnie dostosuj je do unikatowych wymagań dotyczących zabezpieczeń. Mamy problemy z próbą wymuszenia istniejących lokalnych zasad i standardów, ponieważ często odwołują się one do nieaktualnej metody lub podejścia do zabezpieczeń. Firma Microsoft opublikowała wskazówki ułatwiające tworzenie linii bazowych zabezpieczeń:
  - [Standardy zabezpieczeń platformy Azure dotyczące strategii i architektury](https://docs.microsoft.com/security/compass/compass): zalecenia dotyczące strategii i architektury, które umożliwiają kształtowanie stan zabezpieczeń środowiska.
  - [Testy wydajnościowe platformy Azure](https://docs.microsoft.com/azure/security/benchmarks/introduction): konkretne zalecenia dotyczące konfiguracji zabezpieczania środowisk platformy Azure.
  - [Szkolenie dotyczące linii bazowej zabezpieczeń platformy Azure](https://docs.microsoft.com/learn/modules/create-security-baselines).
- **Podaj guardrails:** Powinny one mieć zautomatyzowane inspekcje zasad i wymuszania. W tych nowych środowiskach zespoły powinny dążyć do inspekcji i wymuszać linie bazowe zabezpieczeń organizacji, aby zminimalizować nieprzewidziane zabezpieczenia podczas rozwoju, a także ciągłej integracji i ciągłego wdrażania (CI/CD) obciążeń.
Firma Microsoft oferuje kilka natywnych możliwości platformy Azure, które umożliwiają:
  - Security [Score](https://docs.microsoft.com/azure/security-center/secure-score-security-controls): Ocena oceniana stan zabezpieczeń platformy Azure, która pozwala śledzić wysiłki i projekty zabezpieczeń w organizacji.
  - [Plany platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/overview): architektzy w chmurze i centralne grupy IT mogą definiować powtarzalny zestaw zasobów platformy Azure, które implementują i stosują standardy, wzorce i wymagania organizacji.
  - [Azure Policy](https://docs.microsoft.com/azure/governance/policy/): podstawą możliwości widoczności i kontroli używanych przez te inne usługi. Azure Policy jest zintegrowana z usługą [Azure Resource Manager (ARM)](https://docs.microsoft.com/azure/azure-resource-manager), dzięki czemu można przeprowadzać inspekcję zmian i wymuszać zasady dla dowolnego zasobu na platformie Azure przed, w trakcie lub po jego utworzeniu.
- [Ulepszanie operacji strefy wyładunkowej](../ready/considerations/landing-zone-security.md): Użyj najlepszych rozwiązań w celu zwiększenia bezpieczeństwa w danej strefie docelowej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zabezpieczeń w chmurze | <li> Zespół ds. wdrażania chmury <li> Zespół platformy w chmurze <li> Zespół strategii chmury <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-5-secure-existing-cloud-workloads"></a>Krok 5. Zabezpieczanie istniejących obciążeń w chmurze

Wiele organizacji już wdrożono zasoby w środowiskach chmury przedsiębiorstwa, które nie stosowały najlepszych rozwiązań w zakresie zabezpieczeń, tworząc zwiększone ryzyko biznesowe.

Po upewnieniu się, że nowe aplikacje i strefy wyładunkowe są zgodne z najlepszymi rozwiązaniami w zakresie bezpieczeństwa, należy skoncentrować się na wprowadzaniu istniejących środowisk do tych samych standardów.

**Dostarczane**

- Upewnij się, że wszystkie istniejące środowiska chmury i strefy wyładunkowe spełniają wymagania dotyczące zgodności i bezpieczeństwa organizacji.
- Przetestuj gotowość operacyjną wdrożeń produkcyjnych przy użyciu zasad linii bazowej zabezpieczeń.
- Weryfikuj przestrzeganie wskazówek dotyczących projektowania linii bazowej zabezpieczeń i wymagania dotyczące zabezpieczeń.

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Użyj tych samych linii bazowych zabezpieczeń, które zostały skompilowane w [kroku 4](#step-4-secure-new-workloads) jako idealnego stanu. Może być konieczne dostosowanie niektórych ustawień zasad tylko do inspekcji zamiast wymuszania ich.
- Zrównoważ ryzyko związane z działaniem i bezpieczeństwem. Ponieważ te środowiska mogą hostować systemy produkcyjne, które umożliwiają krytyczne procesy biznesowe, może być konieczne stopniowe wdrożenie ulepszeń zabezpieczeń, aby uniknąć ryzyka przestoju operacyjnego.
- Ustalanie priorytetów wykrywania i korygowania zagrożeń bezpieczeństwa przez krytyczne znaczenie biznesowe, począwszy od obciążeń, które mają duży wpływ na działalność biznesową, w przypadku naruszenia bezpieczeństwa i obciążeń mających wysokie ryzyko.

Aby uzyskać więcej informacji, zobacz [Identyfikowanie i klasyfikowanie aplikacji o krytycznym znaczeniu dla firmy](https://docs.microsoft.com/azure/architecture/framework/security/applications-services?toc=/security/compass/toc.json&bc=/security/compass/breadcrumb/toc.json#identify-and-classify-business-critical-applications).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. wdrażania chmury | <li> Zespół ds. wdrażania chmury <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Zespół nadzorujący chmury <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="step-6-govern-to-manage-and-improve-security-posture"></a>Krok 6. Zarządzanie Stanami zabezpieczeń i ich ulepszanie

Podobnie jak w przypadku wszystkich nowoczesnych dyscyplin, bezpieczeństwo jest procesem iteracyjnym, który powinien skupić się na ciągłym ulepszaniu. Stan zabezpieczeń może również zaistnieć, jeśli organizacje nie będą w stanie skupić się na tym czasie.

Spójne zastosowanie wymagań dotyczących zabezpieczeń pochodzi z dyscypliny zarządzania dźwięku i zautomatyzowanych rozwiązań. Gdy linie bazowe zabezpieczeń są definiowane przez zespół ds. zabezpieczeń w chmurze, te wymagania powinny podlegać inspekcji, aby upewnić się, że są one stosowane spójnie ze wszystkimi środowiskami chmury (i są wymuszane w razie potrzeby).

**Dostarczane**

- Upewnij się, że linie bazowe zabezpieczeń organizacji są stosowane do wszystkich odpowiednich systemów i anomalii są poddawane inspekcji przy użyciu [bezpiecznego wyniku](https://docs.microsoft.com/azure/security-center/secure-score-security-controls) lub podobnego mechanizmu.
- Udokumentowanie zasad linii bazowej zabezpieczeń, procesów i wskazówek dotyczących projektu w [szablonie dyscypliny linii bazowej zabezpieczeń](../govern/security-baseline/template.md).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Użyj tych samych punktów odniesienia zabezpieczeń i mechanizmów inspekcji, które zostały skompilowane w [kroku 4](#step-4-secure-new-workloads) jako składniki techniczne monitorowania linii bazowych, uzupełnione o osoby i kontrolki procesów, aby zapewnić spójność.
- Upewnij się, że wszystkie obciążenia i zasoby są zgodne z właściwymi [konwencjami nazewnictwa](../ready/azure-best-practices/naming-and-tagging.md) i oznaczania i [wymuszania Konwencji tagowania przy użyciu Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/govern-tags) z określonym naciskiem na znaczniki dotyczące "czułości danych".
- Jeśli dopiero zaczynasz zarządzanie chmurą, ustal [zasady, procesy i dyscypliny ładu](../govern/index.md) przy użyciu metodologii rządzącej.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół nadzorujący chmury | <li> Zespół strategii chmury <li> Zespół ds. zabezpieczeń w chmurze <li> Centrum w chmurze doskonałości lub środkowe |

## <a name="next-steps"></a>Następne kroki

Te kroki przeprowadzą Cię przez proces wdrażania właściwej strategii, kontroli, procesów, umiejętności i kultury potrzebnej do spójnego zarządzania zagrożeniami bezpieczeństwa w całym przedsiębiorstwie.
W trakcie dalszej pracy z trybem zabezpieczeń w chmurze należy uwzględnić te następne kroki w kompilacji na tej wskazówki.

- Zapoznaj się z [dokumentacją dotyczącą zabezpieczeń firmy Microsoft](https://docs.microsoft.com/security) , która zawiera wskazówki techniczne ułatwiające specjalistom ds. zabezpieczeń tworzenie i ulepszanie strategii cyberbezpieczeństwa, architektury i priorytetów.
- Przejrzyj informacje o zabezpieczeniach [wbudowanych formantów zabezpieczeń usług platformy Azure](https://docs.microsoft.com/azure/security/fundamentals/security-controls).
- Przejrzyj narzędzia i usługi zabezpieczeń platformy Azure w [usługach i technologiach zabezpieczeń dostępnych na platformie Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).
- Zapoznaj się z [Centrum zaufania firmy Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment) , ponieważ zawiera obszerne wskazówki, raporty i powiązane dokumenty, które mogą pomóc w wykonywaniu ocen ryzyka w ramach procesów zgodności z przepisami.
- Zapoznaj się z dostępnymi narzędziami innych firm, aby ułatwić spełnienie wymagań dotyczących zabezpieczeń. Aby uzyskać więcej informacji, zobacz [integrowanie rozwiązań zabezpieczeń w Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).
