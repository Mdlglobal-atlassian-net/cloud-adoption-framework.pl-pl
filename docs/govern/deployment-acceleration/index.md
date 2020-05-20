---
title: Omówienie dziedziny Przyspieszanie wdrażania
description: Skorzystaj z przewodnika Cloud Adoption Framework dla platformy Azure, aby zapoznać się z przyspieszaniem wdrażania w odniesieniu do ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dbd60db37d5eb14b877f45c00956fd1869e9a0ba
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83620540"
---
# <a name="deployment-acceleration-discipline-overview"></a>Omówienie dziedziny Przyspieszanie wdrażania

Przyspieszenie wdrażania jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu ładu z przewodnika Cloud Adoption Framework](../index.md). Ta dziedzina koncentruje się na sposobach ustanawiania zasad umożliwiających nadzorowanie konfigurowania lub wdrażania zasobów. Dziedzina Przyspieszanie wdrażania, jedna z pięciu dziedzin utrzymania ładu w chmurze, obejmuje wdrażanie, dostosowywanie konfiguracji oraz możliwość ponownego wykorzystania skryptów. Może to się odbywać za pośrednictwem działań ręcznych lub w pełni zautomatyzowanych działań metodyki DevOps. W obu przypadkach zasady pozostają w dużym stopniu takie same. Gdy ta dziedzina dojrzeje, zespół ds. utrzymania ładu w chmurze może być partnerem w metodyce DevOps i strategiach wdrażania, przyspieszając wdrożenia i usuwając bariery w celu wdrożenia chmury dzięki zastosowaniu zasobów do ponownego wykorzystania.

W tym artykule opisano proces przyspieszania wdrażania występujący w firmie na etapach planowania, kompilowania, wdrażania i obsługi implementowania rozwiązania w chmurze. Żaden pojedynczy dokument nie może opisać wszystkich wymagań wszystkich firm. W związku z tym każda sekcja tego artykułu przedstawia sugerowane minimum i możliwe działania. Celem tych działań jest pomoc w utworzeniu [specjalisty od zasad](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy), ale także ustanowienie struktury na potrzeby ulepszania [zasad przyrostowych](../policy-compliance/index.md#incremental-policy-growth). Zespół ds. utrzymania ładu w chmurze powinien zdecydować, jak dużo zainwestować w te działania, aby poprawić dziedzinę Przyspieszanie wdrażania.

> [!NOTE]
> Dziedzina Przyspieszanie wdrażania nie zastępuje istniejących zespołów IT, procesów i procedur, które umożliwiają organizacji skuteczne wdrażanie i konfigurowanie zasobów opartych na chmurze. Najważniejszym zadaniem tej dziedziny jest identyfikowanie potencjalnych czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za zarządzanie zasobami w chmurze wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie odpowiednich członków zespołów biznesowych i informatycznych oraz dyskusje z nimi. W szczególności dotyczy to liderów odpowiedzialnych za wdrażanie i konfigurowanie obciążeń opartych na chmurze.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Przyspieszanie wdrażania. Aby wyświetlić przykładowe instrukcje zasad, zobacz artykuł [Instrukcje zasad dziedziny Przyspieszanie wdrażania](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

Sześć poniższych kroków pomoże określić zasady utrzymania ładu umożliwiające kontrolę wdrażania i konfigurowania zasobów w środowisku chmury.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Ikona szablonu](../../_images/govern/process-template.png) | <br> [Szablon dotyczący dziedziny Przyspieszanie wdrażania](./template.md): Pobierz szablon umożliwiający dokumentowanie dziedziny Przyspieszanie wdrażania. |
| <br> ![Ikona rodzajów ryzyka](../../_images/govern/process-risks.png) | <br> [Rodzaje ryzyka biznesowego](./business-risks.md): Poznaj przyczyny i zagrożenia skojarzone zazwyczaj z dziedziną Przyspieszanie wdrażania.|
| <br> ![Ikona metryk](../../_images/govern/process-metrics.png) | <br> [Wskaźniki i metryki](./metrics-tolerance.md): Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Przyspieszanie wdrażania. |
| <br> ![Ikona zapewniania zgodności](../../_images/govern/process-enforce.png) | <br> [Procesy zapewniania zgodności zasad](./compliance-processes.md): Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Przyspieszanie wdrażania. |
| <br> ![Ikona dojrzałości](../../_images/govern/process-maturity.png) | <br> [Dojrzałość](./discipline-improvement.md): Dostosuj dojrzałość dziedziny Zarządzanie chmurą do etapów wdrażania w chmurze.|
| <br> ![Ikona łańcucha narzędzi](../../_images/govern/process-toolchain.png) | <br> [Łańcuch narzędzi](./toolchain.md): Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Przyspieszanie wdrażania. |

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny [ryzyka biznesowego](./business-risks.md) w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)

<!-- markdownlint-enable MD033 -->
