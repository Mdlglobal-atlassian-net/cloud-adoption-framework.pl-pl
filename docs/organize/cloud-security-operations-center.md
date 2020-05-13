---
title: Funkcje centrum operacji zabezpieczeń w chmurze
description: Informacje o możliwościach związanych z zabezpieczeniami w chmurze
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: 7c3044e4d5e970b9f78bb46bda2aadf11273e556
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83228640"
---
<!-- cSpell:ignore CISO MTTA MTTR SIEM NIST SOCs CDOC -->

# <a name="functions-of-a-cloud-security-operations-center-soc"></a>Funkcje centrum operacji zabezpieczeń w chmurze (SOC)

Głównym celem centrum operacji w chmurze zabezpieczeń (SOC) jest wykrywanie, reagowanie na i odzyskiwanie z aktywnych ataków na zasoby przedsiębiorstwa.

Jako dojrzały SOC, operacje zabezpieczeń powinny:

- Odreaguj na ataki wykryte przez narzędzia
- Proaktywne odszukanie ataków, które pozostały w przeszłości reaktywne wykrywania

## <a name="modernization"></a>Modernizacja

Wykrywanie zagrożeń i reagowanie na nie jest obecnie w znaczący sposób modernizacji na wszystkich poziomach.

- **Podniesienie poziomu zarządzania ryzykiem biznesowym:** SOC zwiększa się w kluczowym składniku zarządzania ryzykiem biznesowym w organizacji
- **Metryki i cele:** Śledzenie skuteczności SOC jest rozwijane od "czas wykrycia" do tych kluczowych wskaźników:
  - Czas *odpowiedzi* za pośrednictwem średniego czasu na potwierdzenie (MTTA)
  - *Szybkość korygowania* poprzez średni czas do skorygowania (MTTR)
- **Ewolucja technologii:** Technologia SOC jest rozwijana z wyłącznym użyciem statycznej analizy dzienników w SIEM, aby dodać korzystanie z wyspecjalizowanych narzędzi i zaawansowanych technik analizy. Zapewnia to szczegółowe informacje o zasobach, które zapewniają alerty o wysokiej jakości i środowisko dochodzeniowe, które uzupełniają widok szerokości SIEM. Oba typy narzędzi są coraz bardziej pomocne przy użyciu AI/Machine Learning (usługi AI/Machine Learning), analizy zachowań i zintegrowanej analizy zagrożeń (TI) w celu ułatwienia i określania priorytetów nietypowych działań, które mogą być złośliwymi osobami atakującymi.
- **Łowiectwo zagrożeń:** SOC dodają łowiectwo-polowanie zagrożeń, aby aktywnie identyfikować zaawansowani osoby atakujące i przełączać zakłócenia w przypadku kolejek analityków teraźniejszości.
- **Zarządzanie zdarzeniami:** Dyscypliny są formalne do koordynowania nietechnicznych elementów incydentów mających charakter prawny, komunikacji i innych zespołów.
**Integracja kontekstu wewnętrznego:** Aby pomóc w ustaleniu priorytetów działań SOC, takich jak względne ryzyko związane z niektórymi zagrożeniami dla kont użytkowników i urządzeń, czułość danych i aplikacji oraz granice izolacji najważniejszych zabezpieczeń w celu ścisłej obrony.

 Aby uzyskać więcej informacji, zobacz:

- [Operacje zabezpieczeń dotyczące strategii i architektury &mdash;](https://docs.microsoft.com/security/compass/security-operations-videos-and-decks)
- [CISO Workshop module 4B: strategia ochrony przed zagrożeniami](https://docs.microsoft.com/security/ciso-workshop/ciso-workshop-module-4b)
- Blog z serii cybernetycznymi obrony Operations Center (CDOC) [część 1](https://www.microsoft.com/security/blog/2019/02/21/lessons-learned-from-the-microsoft-soc-part-1-organization/), [część 2a](https://www.microsoft.com/security/blog/2019/04/23/lessons-learned-microsoft-soc-part-2-organizing-people/), część [2b](https://www.microsoft.com/security/blog/2019/06/06/lessons-learned-from-the-microsoft-soc-part-2b-career-paths-and-readiness/), część [3a](https://www.microsoft.com/security/blog/2019/10/07/ciso-series-lessons-learned-from-the-microsoft-soc-part-3a-choosing-soc-tools/), [część 3B](https://www.microsoft.com/security/blog/2019/12/23/ciso-series-lessons-learned-from-the-microsoft-soc-part-3b-a-day-in-the-life)
- [Przewodnik obsługi zdarzeń zabezpieczeń komputera NIST](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)
- [Przewodnik NIST dotyczący odzyskiwania zdarzeń cyberbezpieczeństwa](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-184.pdf)

## <a name="team-composition-and-key-relationships"></a>Kompozycja zespołu i relacje między kluczami

Centrum operacji zabezpieczeń w chmurze zwykle składa się z następujących typów ról.

- Operacje IT (Zamknij zwykły kontakt)
- Analiza zagrożeń
- Architektura zabezpieczeń
- Program niejawnego ryzyka
- Zasoby prawne i kadrowe
- Zespoły komunikacyjne
- Organizacja ryzyka (jeśli istnieje)
- Stowarzyszenia, społeczności i dostawcy specyficzne dla branż (przed wystąpieniem zdarzenia)

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z funkcją [architektury zabezpieczeń](./cloud-security-architecture.md).
