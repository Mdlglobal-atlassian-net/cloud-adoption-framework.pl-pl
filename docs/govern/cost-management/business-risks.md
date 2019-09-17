---
title: Cost Management motywacje i ryzyko biznesowe
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cost Management motywacje i ryzyko biznesowe
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 328352ac7ccd8cacbc92cc09ce0c07e2843afcf1
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030833"
---
# <a name="cost-management-motivations-and-business-risks"></a>Cost Management motywacje i ryzyko biznesowe

W tym artykule omówiono przyczyny, w których klienci zazwyczaj przyjmują Cost Management dyscyplinę w ramach strategii nadzoru chmurowego. Zawiera również kilka przykładów ryzyka biznesowego, które dotyczą instrukcji zasad.

<!-- markdownlint-disable MD026 -->

## <a name="is-cost-management-relevant"></a>Czy jest Cost Management istotne?

W odniesieniu do ładu kosztów, wdrażanie w chmurze powoduje utworzenie zmiany modelu. Zarządzanie kosztami w tradycyjnym lokalnym świecie odbywa się na podstawie cykli odświeżania, pozyskiwania centrów danych, odnawiania hostów i cyklicznych problemów z konserwacją. Możesz prognozować, planować i udoskonalać każdy z tych kosztów, aby dostosować je do budżetów rocznych wydatków inwestycyjnych.

W przypadku rozwiązań w chmurze wiele firm będzie miało coraz bardziej aktywne podejście do Cost Management. W wielu przypadkach firmy będą kupować lub zatwierdzić korzystanie z zestawu usług Cloud Services. W tym modelu przyjęto założenie, że maksymalizacja rabatów w zależności od tego, jak dużo planów firmy na wydatki z konkretnym dostawcą chmury, powoduje utworzenie postrzegania aktywnego, planowanego cyklu kosztów. Jednak to postrzeganie stanie się rzeczywistością tylko wtedy, gdy firma także implementuje wczesne Cost Management dyscypliny.

Chmura oferuje funkcje samoobsługowe, które wcześniej były niesłyszalne w tradycyjnych lokalnych centrach danych. Te nowe możliwości pozwalają firmom na bardziej elastyczne, mniej restrykcyjne i bardziej otwarte wdrożenie nowych technologii. Jednak minusem samoobsługi polega na tym, że użytkownicy końcowi mogą nieświadomie przekroczyć przydzieloną liczbę budżetów. Z drugiej strony mogą wystąpić zmiany w planach i nieoczekiwane użycie usług Cloud Services w prognozie. Potencjalna zmiana w obu kierunkach uzasadnia inwestycję w Cost Management dyscypliny w zespole ładu.

## <a name="business-risk"></a>Ryzyko biznesowe

Dyscyplina Cost Management próbuje rozwiązać podstawowe ryzyko biznesowe związane z kosztami związanymi z obsługą obciążeń opartych na chmurze. Pracuj z firmą, aby identyfikować te zagrożenia i monitorować każdy z nich w celu zapewnienia przydatności podczas planowania i implementowania wdrożeń w chmurze.

Zagrożenia będą się różnić między organizacjami, ale poniżej przedstawiono typowe ryzyka związane z kosztami, których można użyć jako punktu wyjścia dla dyskusji w zespole nadzoru chmurowego:

- **Kontrola budżetu:** Niesterowanie budżetem może prowadzić do nadmiernych wydatków u dostawcy chmury.
- **Utrata użycia:** Przed zakupami lub zobowiązaniami, które nie są używane, mogą wynikać z inwestycji.
- **Anomalie wydatków:** Nieoczekiwane skoki w dowolnym kierunku mogą być wskaźnikami nieprawidłowego użycia.
- **Zasoby o nadmiernej aprowizacji:** Gdy zasoby są wdrażane w konfiguracji, która przekracza potrzeby aplikacji lub maszyny wirtualnej, może zwiększyć koszty i utworzyć odpady.

## <a name="next-steps"></a>Następne kroki

Korzystając z [szablonu zarządzania chmurą](./template.md), dokumentuj ryzyka biznesowego, które mogą być wprowadzane przez bieżący plan wdrożenia chmury.

Po ustaleniu realistycznych zagrożeń handlowych, następnym krokiem jest udokumentowanie tolerancji firmy dla ryzyka oraz wskaźników i kluczowych metryk, aby monitorować tę tolerancję.

> [!div class="nextstepaction"]
> [Omówienie wskaźników, metryk i tolerancji ryzyka](./metrics-tolerance.md)
