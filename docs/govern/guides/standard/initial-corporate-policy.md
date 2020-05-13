---
title: 'Standardowe zarządzanie przedsiębiorstwem: wstępne zasady firmowe'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby zdefiniować początkową sytuację ładu, ryzyko wczesnego etapu, wstępne instrukcje zasad i procesy wczesnego wymuszania.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c32193ee76899af327a2ed727de43f56f9d1ff63
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214552"
---
# <a name="standard-enterprise-governance-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Standardowy Przewodnik dotyczący zarządzania przedsiębiorstwem: wstępne zasady firmowe związane z strategią ładu

Następujące zasady firmowe określają początkową pozycję ładu, która jest punktem początkowym tego przewodnika. Ten artykuł definiuje wczesne zagrożenia, wstępne instrukcje zasad i wczesne procesy w celu wymuszenia instrukcji zasad.

> [!NOTE]
>Zasady firmowe nie są dokumentem technicznym, ale obejmują wiele decyzji technicznych. SPECJALISTa z ładu, opisany w [przeglądzie](./index.md) , ostatecznie pochodzi z tych zasad. Przed wdrożeniem programu MVP (ładu) organizacja powinna opracować zasady firmowe na podstawie własnych celów i ryzyka biznesowego.

## <a name="cloud-governance-team"></a>Zespół nadzorujący chmury

W tym opisie zespół zarządzający chmurą składa się z dwóch administratorów systemów, którzy uznały potrzebę zarządzania. W ciągu następnych kilku miesięcy dziedziczą one zadanie czyszczenia danych o obecności w chmurze firmy, a im tytuł _powierników w chmurze_. W kolejnych iteracjach ten tytuł będzie prawdopodobnie zmieniany.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Wskaźniki tolerancji

Aktualna tolerancja dla ryzyka jest wysoka i akceptowalnego poziomu do inwestowania w zarządzanie chmurą jest niska. W związku z tym wskaźniki tolerancji działają jako system wczesnego ostrzegania, aby wyzwolić większe inwestycje czasu i energii. Jeśli i gdy są obserwowane następujące wskaźniki, należy iteracyjnie poprawić strategię zarządzania.

- **Zarządzanie kosztami:** Skala wdrożenia przekracza wstępnie określone limity liczby zasobów lub miesięcznych kosztów.
- **Linia bazowa zabezpieczeń:** Uwzględnianie chronionych danych w zdefiniowanych planach wdrożenia chmury.
- **Spójność zasobów:** Uwzględnianie wszystkich aplikacji o znaczeniu krytycznym w określonych planach wdrożenia chmury.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Następne kroki

Te zasady firmowe przygotowuje zespół nadzorujący chmurę do wdrożenia programu MVP (ładu), który będzie podstawą do przyjęcia. Następnym krokiem jest zaimplementowanie tego programu MVP.

> [!div class="nextstepaction"]
> [Objaśniono najlepsze rozwiązania](./prescriptive-guidance.md)
