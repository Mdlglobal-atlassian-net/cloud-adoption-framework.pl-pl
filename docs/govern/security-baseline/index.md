---
title: Omówienie dziedziny Punkt odniesienia zabezpieczeń
description: Zapoznaj się z podejściem do tworzenia dziedziny Punkt odniesienia zabezpieczeń w ramach strategii utrzymania ładu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4b5e98141b581eb9b39f3056f1025c7fe614ae70
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83398937"
---
# <a name="security-baseline-discipline-overview"></a>Omówienie dziedziny Punkt odniesienia zabezpieczeń

Punkt odniesienia zabezpieczeń jest jedną z [pięciu dziedzin utrzymania ładu w chmurze](../governance-disciplines.md) w ramach [modelu utrzymania ładu z przewodnika Cloud Adoption Framework](../index.md). Zabezpieczenia są składnikiem każdego wdrożenia IT, a chmura wprowadza unikatowe zagadnienia związane z bezpieczeństwem. Wiele firm podlega wymaganiom prawnym, dlatego ochrona poufnych danych stała się głównym priorytetem organizacji, która rozważa przekształcenie do chmury. Identyfikowanie potencjalnych zagrożeń w środowisku chmury oraz ustanawianie procesów i procedur umożliwiających eliminowanie tych zagrożeń powinno mieć priorytet dla każdego zespołu IT zajmującego się zabezpieczeniami lub cyberbezpieczeństwem. Dziedzina Punkt odniesienia zabezpieczeń gwarantuje, że wymagania techniczne i ograniczenia zabezpieczeń są spójnie stosowane w środowiskach w chmurze w miarę dojrzewania wymagań.

> [!NOTE]
> Dyscyplina Punkt odniesienia zabezpieczeń nie zastąpi istniejących zespołów, procesów i procedur IT, które umożliwiają w organizacji zabezpieczanie zasobów wdrożonych w organizacji. Najważniejszym zadaniem tej dziedziny jest identyfikowanie związanych z bezpieczeństwem czynników ryzyka biznesowego i przekazywanie pracownikom działu IT odpowiedzialnym za infrastrukturę zabezpieczeń wskazówek mających na celu ograniczenie ryzyka. Podczas tworzenia zasad i procesów utrzymania ładu należy uwzględnić odpowiednie zespoły informatyczne w procesach planowania i przeglądania.

W tym artykule opisano metodę tworzenia dziedziny Punkt odniesienia zabezpieczeń w ramach strategii utrzymania ładu w chmurze. Głównymi odbiorcami tych wskazówek są architekci chmury w organizacji oraz inni członkowie zespołu ds. utrzymania ładu w chmurze. Jednak decyzje, zasady i procesy wynikające z tej dziedziny powinny obejmować zaangażowanie odpowiednich członków zespołów IT i zespołów ds. zabezpieczeń oraz dyskusje z nimi. W szczególności dotyczy to liderów technicznych odpowiedzialnych za implementowanie usług obsługi sieci, szyfrowania i tożsamości.

Podejmowanie właściwych decyzji dotyczących zabezpieczeń ma kluczowe znaczenie, jeśli chcesz osiągnąć sukces podczas wdrożeń w chmurze i szerzej pojmowany sukces biznesowy. Jeśli Twoja organizacja nie ma własnych specjalistów zajmujących się cyberbezpieczeństwem, należy w ramach tej dziedziny rozważyć zatrudnienie zewnętrznych konsultantów ds. bezpieczeństwa. Ponadto należy wziąć pod uwagę skorzystanie z [Microsoft Consulting Services](https://www.microsoft.com/industry/services/consulting) — usług wdrażania w chmurze będących częścią programu [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) — lub innych zewnętrznych ekspertów ds. wdrażania w chmurze, aby przedyskutować z nimi kwestie związane z tą dziedziną.

## <a name="policy-statements"></a>Instrukcje zasad

Instrukcje zasad umożliwiające podejmowanie działań i wynikające z nich wymagania dotyczące architektury stanowią podstawę dziedziny Punkt odniesienia zabezpieczeń. Przykładowe instrukcje zasad można zobaczyć w artykule [Instrukcje zasad dziedziny Punkt odniesienia zabezpieczeń](./policy-statements.md). Te przykłady mogą posłużyć jako punkt wyjścia dla zasad utrzymania ładu w organizacji.

> [!CAUTION]
> Przykładowe zasady pochodzą z typowych doświadczeń klientów. W celu lepszego dostosowania tych zasad do określonych potrzeb w zakresie utrzymania ładu w chmurze wykonaj poniższe kroki, aby utworzyć instrukcje zasad spełniające unikatowe potrzeby firmy.

## <a name="develop-governance-policy-statements"></a>Opracowywanie instrukcji zasad utrzymania ładu

W poniższych sześciu krokach zamieszczono przykłady i potencjalne opcje, które należy wziąć pod uwagę podczas opracowywania dziedziny Punkt odniesienia zabezpieczeń. Każdy z tych kroków może stanowić punkt wyjścia do dyskusji w ramach zespołu ds. utrzymania ładu w chmurze oraz z zespołami biznesowymi, informatycznymi i zajmującymi się zabezpieczeniami w organizacji w celu opracowania zasad i procesów wymaganych do zarządzania czynnikami ryzyka powiązanymi z zabezpieczeniami.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![Ikona szablonu](../../_images/govern/process-template.png) | [Szablon dotyczący dziedziny Punkt odniesienia zabezpieczeń](./template.md): Pobierz szablon umożliwiający dokumentowanie dziedziny Punkt odniesienia zabezpieczeń. |
| <br> ![Ikona rodzajów ryzyka](../../_images/govern/process-risks.png) | [Rodzaje ryzyka biznesowego](./business-risks.md): Poznaj przyczyny i czynniki ryzyka kojarzone zazwyczaj z dziedziną Punkt odniesienia zabezpieczeń. |
| <br> ![Ikona metryk](../../_images/govern/process-metrics.png) | [Wskaźniki i metryki](./metrics-tolerance.md): Wskaźniki umożliwiające zrozumienie, czy to właściwy moment, aby zainwestować w dziedzinę Punkt odniesienia zabezpieczeń. |
| <br> ![Ikona zapewniania zgodności](../../_images/govern/process-enforce.png) | [Procesy zapewniania zgodności zasad](./compliance-processes.md): Sugerowane procesy umożliwiające obsługę zgodności z zasadami w dziedzinie Punkt odniesienia zabezpieczeń. |
| <br> ![Ikona dojrzałości](../../_images/govern/process-maturity.png) | [Dojrzałość](./discipline-improvement.md): Dostosuj dojrzałość dziedziny Zarządzanie chmurą do etapów wdrażania w chmurze. |
| <br> ![Ikona łańcucha narzędzi](../../_images/govern/process-toolchain.png) | [Łańcuch narzędzi](./toolchain.md): Usługi platformy Azure, które można zaimplementować w celu obsługi dziedziny Punkt odniesienia zabezpieczeń. |

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Następne kroki

Rozpocznij pracę od oceny ryzyka biznesowego w konkretnym środowisku.

> [!div class="nextstepaction"]
> [Omówienie ryzyka biznesowego](./business-risks.md)
