---
title: Szacowanie kosztów chmury przed migracją
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie procesu szacowania kosztów chmury przed migracją.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: be4fe4616b4f0599075ceac2b9c0838949b350c8
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548483"
---
# <a name="estimate-cloud-costs"></a>Szacowanie kosztów chmury

Podczas migracji występuje kilka czynników, które mogą wpływać na decyzje i działania związane z realizacją. Aby ułatwić zrozumienie, które z tych opcji są najlepsze w danych sytuacjach, w tym artykule omówiono różne opcje szacowania kosztów chmury.

## <a name="digital-estate-size"></a>Rozmiar majątku cyfrowego

Rozmiar majątku cyfrowego ma bezpośredni wpływ na decyzje dotyczące migracji. Migracje obejmujące mniej niż 250 maszyn wirtualnych można oszacować znacznie łatwiej niż migrację obejmującą ponad 10 000 maszyn wirtualnych. Zdecydowanie zaleca się wybranie mniejszego obciążenia jako pierwszej migracji. Dzięki temu Twój zespół może dowiedzieć się, jak oszacować koszty prostej migracji przed podjęciem próby oszacowania większych i bardziej skomplikowanych migracji obciążeń.

Należy jednak pamiętać, że mniejsze migracje pojedynczych obciążeń mogą nadal obejmować bardzo zróżnicowane ilości zasobów pomocniczych. Jeśli migracja obejmuje mniej niż 1000 maszyn wirtualnych, narzędzie takie jak [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview) powinno być wystarczające do zebrania danych dotyczących zapasów i utworzenia prognozy kosztów. Dodatkowe opcje i narzędzia do szacowania kosztów opisano w artykule dotyczącym [obliczania kosztu majątku cyfrowego](../../../digital-estate/calculate.md).

W przypadku 1000 Estates Digital + Unit wciąż istnieje możliwość podziału oszacowania na cztery lub pięć iteracji możliwych do działania, co umożliwia zarządzanie procesem szacowania. W przypadku większych majątków lub gdy wymagany jest wyższy stopień dokładności prognozy, prawdopodobnie będzie wymagane bardziej kompleksowe podejście, jak to opisane w sekcji „[Majątek cyfrowy](../../../digital-estate/index.md)” przewodnika Cloud Adoption Framework.

## <a name="accounting-models"></a>Modele księgowania

Modele księgowania

Jeśli znasz tradycyjne procesy zaopatrzenia IT, szacowanie w chmurze może wydawać się obce. W przypadku wdrażania technologii chmurowych odchodzi się od sztywnego, ustrukturyzowanego modelu wydatków kapitałowych i przyjmuje się płynny model kosztów operacyjnych. W tradycyjnym modelu wydatków kapitałowych zespół IT próbuje skonsolidować siłę nabywczą dla kilku obciążeń w różnych programach, aby scentralizować pulę udostępnionych zasobów, które mogłyby obsługiwać każde z tych rozwiązań. W chmurowym modelu kosztów operacyjnych koszty można przypisać bezpośrednio do potrzeb w zakresie obsługi poszczególnych obciążeń, zespołów lub jednostek biznesowych. Takie podejście pozwala na bardziej bezpośrednie przypisywanie kosztów do obsługiwanego klienta wewnętrznego. W przypadku szacowania kosztów ważne jest, aby najpierw zrozumieć, jaka część nowych funkcji księgowości będzie używana przez zespół IT.

Jeśli chcesz zreplikować starsze podejście do wydatków inwestycyjnych, użyj danych wyjściowych jednego z podejść sugerowanych w sekcji „[Wielkość majątku cyfrowego](#digital-estate-size)” powyżej, aby uzyskać podstawę kosztu rocznego. Następnie pomnóż ten koszt roczny przez typowy cykl odświeżania sprzętu firmy. Cykl odświeżania sprzętu to szybkość, z jaką firma zastępuje starzejący się sprzęt, zwykle mierzona w latach. Roczny wskaźnik uruchomień pomnożony przez cykl odświeżania sprzętu tworzy strukturę kosztów podobną do wzorca wydatków inwestycyjnych.

## <a name="next-steps"></a>Następne kroki

Po oszacowaniu kosztów można rozpocząć migrację. Przed rozpoczęciem migracji warto jednak przejrzeć [opcje partnerstwa i pomocy technicznej](./partnership-options.md).

> [!div class="nextstepaction"]
> [Informacje o opcjach partnerstwa](./partnership-options.md)
