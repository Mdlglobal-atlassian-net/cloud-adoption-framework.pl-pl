---
title: Szacowanie kosztów chmury przed migracją
description: Poznaj czynniki, które mogą mieć wpływ na decyzje i działania wykonywane, a także różne opcje szacowania kosztów chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3537c41610a49b2fd600bb5d81197c515e5c6164
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219380"
---
# <a name="estimate-cloud-costs"></a>Szacowanie kosztów chmury

Podczas migracji występuje kilka czynników, które mogą wpływać na decyzje i działania związane z realizacją. Aby ułatwić zrozumienie, które z tych opcji są najlepsze w danych sytuacjach, w tym artykule omówiono różne opcje szacowania kosztów chmury.

## <a name="digital-estate-size"></a>Rozmiar majątku cyfrowego

Rozmiar majątku cyfrowego ma bezpośredni wpływ na decyzje dotyczące migracji. Migracje obejmujące mniej niż 250 maszyn wirtualnych można oszacować znacznie łatwiej niż migrację obejmującą ponad 10 000 maszyn wirtualnych. Zdecydowanie zaleca się wybranie mniejszego obciążenia jako pierwszej migracji. Dzięki temu Twój zespół może dowiedzieć się, jak oszacować koszty prostej migracji przed podjęciem próby oszacowania większych i bardziej skomplikowanych migracji obciążeń.

Należy jednak pamiętać, że mniejsze migracje pojedynczych obciążeń mogą nadal obejmować bardzo zróżnicowane ilości zasobów pomocniczych. Jeśli migracja obejmuje mniej niż 1000 maszyn wirtualnych, narzędzie takie jak [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-services-overview) powinno być wystarczające do zebrania danych dotyczących zapasów i utworzenia prognozy kosztów. Dodatkowe opcje i narzędzia do szacowania kosztów opisano w artykule dotyczącym [obliczania kosztu majątku cyfrowego](../../../digital-estate/calculate.md).

W przypadku 1000 Estates Digital + Unit wciąż istnieje możliwość podziału oszacowania na cztery lub pięć iteracji możliwych do działania, co umożliwia zarządzanie procesem szacowania. W przypadku większych Estates lub gdy wymagana jest wyższy stopień dokładności prognozy, prawdopodobnie wymagane jest bardziej kompleksowe podejście, takie jak opisane w sekcji dotyczącej możliwości [cyfrowej](../../../digital-estate/index.md) struktury wdrożenia chmury.

## <a name="accounting-models"></a>Modele księgowania

Modele księgowania

Jeśli znasz tradycyjne procesy zaopatrzenia IT, szacowanie w chmurze może wydawać się obce. W przypadku wdrażania technologii chmurowych odchodzi się od sztywnego, ustrukturyzowanego modelu wydatków kapitałowych i przyjmuje się płynny model kosztów operacyjnych. W tradycyjnym modelu wydatków kapitałowych zespół IT próbuje skonsolidować siłę nabywczą dla kilku obciążeń w różnych programach, aby scentralizować pulę udostępnionych zasobów, które mogłyby obsługiwać każde z tych rozwiązań. W chmurowym modelu kosztów operacyjnych koszty można przypisać bezpośrednio do potrzeb w zakresie obsługi poszczególnych obciążeń, zespołów lub jednostek biznesowych. Takie podejście pozwala na bardziej bezpośrednie przypisywanie kosztów do obsługiwanego klienta wewnętrznego. W przypadku szacowania kosztów ważne jest, aby najpierw zrozumieć, jaka część nowych funkcji księgowości będzie używana przez zespół IT.

Aby można było przeprowadzić replikację rozliczenia w ramach rozliczeń w ramach konta, należy użyć danych wyjściowych z dowolnego podejścia sugerowanego w powyższej sekcji [rozmiaru obszaru cyfrowego](#digital-estate-size) do uzyskania rocznego kosztu. Następnie pomnóż ten koszt roczny przez typowy cykl odświeżania sprzętu firmy. Cykl odświeżania sprzętu to szybkość, z jaką firma zastępuje starzejący się sprzęt, zwykle mierzona w latach. Roczny wskaźnik uruchomień pomnożony przez cykl odświeżania sprzętu tworzy strukturę kosztów podobną do wzorca wydatków inwestycyjnych.

## <a name="next-steps"></a>Następne kroki

Po oszacowaniu kosztów można rozpocząć migrację. Przed rozpoczęciem migracji warto jednak przejrzeć [opcje partnerstwa i pomocy technicznej](./partnership-options.md).

> [!div class="nextstepaction"]
> [Informacje o opcjach partnerstwa](./partnership-options.md)
