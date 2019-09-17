---
title: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Wstępne zasady korporacyjne związane z strategią ładu'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Wstępne zasady korporacyjne związane z strategią ładu'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2d8c2923820883561f75902830425b1bd81eb846
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71029285"
---
# <a name="governance-guide-for-complex-enterprises-initial-corporate-policy-behind-the-governance-strategy"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Wstępne zasady korporacyjne związane z strategią ładu

Poniższe zasady korporacyjne określają początkową pozycję ładu, która jest punktem początkowym tego przewodnika. Ten artykuł definiuje wczesne zagrożenia, wstępne instrukcje zasad i wczesne procesy w celu wymuszenia instrukcji zasad.

> [!NOTE]
>Zasady firmowe nie są dokumentem technicznym, ale obejmują wiele decyzji technicznych. SPECJALISTa z ładu, opisany w [przeglądzie](./index.md) , ostatecznie pochodzi z tych zasad. Przed wdrożeniem programu MVP (ładu) organizacja powinna opracować zasady firmowe na podstawie własnych celów i ryzyka biznesowego.

## <a name="cloud-governance-team"></a>Zespół nadzorujący chmury

CIO ostatnio posiadała spotkanie z zespołem nadzoru IT, aby zrozumieć historię danych osobowych i zasad o znaczeniu krytycznym, a następnie zapoznać się ze skutkem zmiany tych zasad. CIO również omawiać ogólny potencjał chmury dla IT i firmy.

Po spotkaniu dwóch członków zespołu nadzoru IT zażądało uprawnień do badania i wspierania wysiłków związanych z planowaniem chmury. Rozpoznanie potrzeby zarządzania i możliwości jego ograniczenia w tle, dyrektor ds. zarządzania IT obsługuje ten pomysł. Dzięki temu zespół ds. zarządzania chmurą został urodzony. W ciągu następnych kilku miesięcy dziedziczą one czyszczenie wielu błędów wykonanych podczas eksploracji w chmurze z perspektywy ładu. Spowoduje to zdobycie monikera _powierników w chmurze_. W kolejnych iteracjach ten przewodnik pokazuje, jak ich role zmieniają się wraz z upływem czasu.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Wskaźniki tolerancji

Aktualna tolerancja ryzyka jest wysoka i akceptowalnego poziomu do inwestowania w zarządzanie chmurą jest niska. W związku z tym wskaźniki tolerancji działają jako system wczesnego ostrzegania, aby wyzwolić inwestycje czasu i energii. W przypadku przestrzegania następujących wskaźników warto postępować zgodnie z strategią ładu.

- **Cost Management:** Skalowanie wdrożenia przekracza 1 000 zasobów do chmury, a miesięczne wydatki przekraczają $10 000 USD miesięcznie.
- **Linia bazowa tożsamości:** Dołączanie aplikacji ze starszymi lub wieloskładnikowymi wymaganiami usługi uwierzytelnianie wieloskładnikowe.
- **Linia bazowa zabezpieczeń:** Uwzględnianie chronionych danych w zdefiniowanych planach wdrożenia chmury.
- **Spójność zasobów:** Uwzględnianie wszystkich aplikacji o znaczeniu krytycznym w określonych planach wdrożenia chmury.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Następne kroki

Te zasady firmowe przygotowuje zespół nadzorujący chmurę do wdrożenia programu MVP (ładu), który będzie podstawą do przyjęcia. Następnym krokiem jest zaimplementowanie tego programu MVP.

> [!div class="nextstepaction"]
> [Wskazówki dotyczące preskryptowe wyjaśnione](./prescriptive-guidance.md)
