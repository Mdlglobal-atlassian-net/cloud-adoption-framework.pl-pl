---
title: Omówienie dziedziny Spójność zasobów
description: Zapoznaj się z podejściem do tworzenia dziedziny Spójność zasobów w ramach strategii utrzymania ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 70108bcd65a19f60861b89aa364044598ea1aad6
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756094"
---
# <a name="resource-consistency-discipline-overview"></a>Omówienie dziedziny Spójność zasobów

Spójność zasobów jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu utrzymania ładu opisanego w przewodniku Cloud Adoption Framework](../index.md). Ta dziedzina koncentruje się na sposobach opracowywania zasad związanych z operacyjnym zarządzaniem środowiskiem, aplikacją lub obciążeniem. Zespoły ds. operacji informatycznych często umożliwiają monitorowanie wydajności aplikacji, obciążeń i zasobów. Często wykonują one również zadania umożliwiające spełnienia wymagań dotyczących skali, korygują naruszenia Umów dotyczących poziomu usług (SLA) i proaktywnie unikają naruszeń umów SLA dotyczących wydajności za pomocą zautomatyzowanych rozwiązań. Z pięciu dziedzin utrzymania ładu w chmurze Spójność zasobów jest tą, która gwarantuje, że zasoby są spójnie konfigurowane w taki sposób, że można je wykryć za pomocą operacji informatycznych, są uwzględnione w rozwiązaniach w zakresie odzyskiwania i mogą być dołączone do procesów powtarzalnych operacji.

> [!NOTE]
> Dziedzina Spójność zasobów nie zastępuje istniejących zespołów IT, procesów i procedur, które umożliwiają organizacji skuteczne zarządzanie zasobami opartymi na chmurze. Najważniejszym zadaniem tej dziedziny jest identyfikowanie potencjalnych czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za zarządzanie zasobami w chmurze wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

W tej sekcji przewodnika Cloud Adoption Framework opisano sposób opracowywania dziedziny Spójność zasobów w ramach strategii utrzymania ładu w chmurze. Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie i dyskusje odpowiednich członków zespołów informatycznych odpowiedzialnych za implementowanie rozwiązań dotyczących spójności zasobów w organizacji i zarządzanie nimi.

Jeśli Twoja organizacja nie ma własnych specjalistów zajmujących się strategiami spójności zasobów, należy w ramach tej dziedziny rozważyć zatrudnienie zewnętrznych konsultantów. Ponadto należy wziąć pod uwagę skorzystanie z [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting) — usług wdrażania w chmurze będących częścią programu [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) — lub innych zewnętrznych ekspertów ds. wdrażania w chmurze, aby przedyskutować z nimi kwestie związane z jak najlepszym organizowaniem, śledzeniem i optymalizowaniem zasobów opartych na chmurze.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Spójność zasobów. Użyj [przykładowych deklaracji zasad](./policy-statements.md). Te przykłady mogą stanowić punkt wyjścia do zdefiniowania zasad Spójności zasobów.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

W poniższych sześciu krokach zamieszczono przykłady i potencjalne opcje, które należy wziąć pod uwagę podczas opracowywania zasad dziedziny Spójność zasobów. Każdy z tych kroków może stanowić punkt wyjścia do dyskusji w ramach zespołu ds. utrzymania ładu w chmurze oraz z zespołami informatycznymi w Twojej organizacji w celu opracowania zasad i procesów wymaganych do zarządzania czynnikami ryzyka powiązanymi z dziedziną Spójność zasobów.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Ikona szablonu](../../_images/govern/process-template.png) | <br> [Szablon dotyczący dziedziny Spójność zasobów](./template.md): Pobierz szablon umożliwiający dokumentowanie dziedziny Spójność zasobów. |
| <br> ![Ikona rodzajów ryzyka](../../_images/govern/process-risks.png) | <br> [Rodzaje ryzyka biznesowego](./business-risks.md): Poznaj przyczyny i czynniki ryzyka kojarzone zazwyczaj z dziedziną Spójność zasobów. |
| <br> ![Ikona metryk](../../_images/govern/process-metrics.png) | <br> [Wskaźniki i metryki](./metrics-tolerance.md): Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Spójność zasobów. |
| <br> ![Ikona zapewniania zgodności](../../_images/govern/process-enforce.png) | <br> [Procesy zapewniania zgodności zasad](./compliance-processes.md): Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Spójność zasobów. |
| <br> ![Ikona dojrzałości](../../_images/govern/process-maturity.png) | <br> [Dojrzałość](./discipline-improvement.md): Dostosuj dojrzałość dziedziny Zarządzanie chmurą do etapów wdrażania w chmurze.  |
| <br> ![Ikona łańcucha narzędzi](../../_images/govern/process-toolchain.png) | <br> [Łańcuch narzędzi](./toolchain.md): Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Spójność zasobów. |

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny [ryzyka biznesowego](./business-risks.md) w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)
