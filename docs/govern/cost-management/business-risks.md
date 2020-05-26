---
title: Motywacje i zagrożenia biznesowe w dyscyplinie Cost Management
description: Poznaj przykłady typowych rozwiązań klienta Cost Management dyscypliny w ramach strategii nadzoru chmurowego.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 048c41f56247ff7f8878d3fdd05506ed46224768
ms.sourcegitcommit: 070e6a60f05519705828fcc9c5770c3f9f986de5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83815093"
---
<!-- cSpell:ignore prepurchases -->

# <a name="motivations-and-business-risks-in-the-cost-management-discipline"></a>Motywacje i zagrożenia biznesowe w dyscyplinie Cost Management

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują Cost Management dyscyplinę w ramach strategii nadzoru chmurowego. Zawiera również kilka przykładów ryzyka biznesowego, które dotyczą instrukcji zasad.

## <a name="relevance"></a>Trafność

W odniesieniu do ładu kosztów, wdrażanie w chmurze powoduje utworzenie zmiany modelu. Zarządzanie kosztami w tradycyjnym lokalnym świecie odbywa się na podstawie cykli odświeżania, pozyskiwania centrów danych, odnawiania hostów i cyklicznych problemów z konserwacją. Możesz prognozować, planować i udoskonalać te koszty, aby dostosować je do budżetów rocznych wydatków inwestycyjnych.

W przypadku rozwiązań w chmurze wiele firm będzie miało coraz bardziej aktywne podejście do zarządzania kosztami. W wielu przypadkach firmy będą kupować lub zatwierdzić korzystanie z zestawu usług Cloud Services. W tym modelu przyjęto założenie, że maksymalizacja rabatów w zależności od tego, jak dużo planów firmy na wydatki z konkretnym dostawcą chmury, powoduje utworzenie postrzegania aktywnego, planowanego cyklu kosztów. To postrzeganie będzie miało rzeczywistość tylko wtedy, gdy firma również realizuje dyscypliny zarządzania dla dorosłych kosztów.

Chmura oferuje funkcje samoobsługowe, które wcześniej były niesłyszalne w tradycyjnych lokalnych centrach danych. Te nowe możliwości pozwalają firmom na bardziej elastyczne, mniej restrykcyjne i bardziej otwarte wdrożenie nowych technologii. Minusem samoobsługi polega na tym, że użytkownicy końcowi mogą nieświadomie przekroczyć przydzieloną liczbę budżetów. Z drugiej strony mogą wystąpić zmiany w planach i nieoczekiwane użycie usług Cloud Services w prognozie. Potencjalna zmiana w obu kierunkach uzasadnia inwestycję w Cost Management dyscypliny w zespole ładu.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina Cost Management próbuje rozwiązać podstawowe ryzyko biznesowe związane z kosztami związanymi z obsługą obciążeń opartych na chmurze. Pracuj z firmą, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i implementowania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe ryzyka związane z kosztami, których można użyć jako punktu wyjścia dla dyskusji w zespole nadzoru chmurowego:

- **Kontrola budżetu:** Niesterowanie budżetem może prowadzić do nadmiernych wydatków u dostawcy chmury.
- **Utrata użycia:** Przed zakupami lub zobowiązaniami, które nie są używane, mogą spowodować utratę inwestycji.
- **Anomalie wydatków:** Nieoczekiwane skoki w dowolnym kierunku mogą być wskaźnikami nieprawidłowego użycia.
- **Zasoby** o nadmiernej aprowizacji: Po wdrożeniu zasobów w konfiguracji, która przekracza wymagania aplikacji lub maszyny wirtualnej, mogą one tworzyć odpady.

## <a name="next-steps"></a>Następne kroki

Użyj [szablonu zasad Cost Management](./template.md) , aby udokumentować ryzyko biznesowe, które mogą zostać wprowadzone przez bieżący plan wdrożenia chmury.

Po uzyskaniu wiedzy o realistycznych zagrożeniach firmy następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
