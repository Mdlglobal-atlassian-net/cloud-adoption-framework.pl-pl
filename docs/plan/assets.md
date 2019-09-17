---
title: Wyrównywanie zasobów do obciążeń z priorytetami
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyrównywanie zasobów do obciążeń z priorytetami
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9d98a9e368f71310a05ae6242ef75a57771824d5
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70828710"
---
# <a name="align-assets-to-prioritized-workloads"></a>Dopasuj zasoby do obciążeń z priorytetyzacją

Obciążenie to koncepcyjny opis kolekcji elementów zawartości: Maszyny wirtualne, aplikacje i źródła danych. W poprzednim artykule, [określanie priorytetów i Definiowanie obciążeń](./workloads.md), wydała wskazówki dotyczące zbierania danych, które definiują obciążenie. Przed migracją niektóre dane wejściowe techniczne z tej listy wymagają dodatkowej weryfikacji. Ten artykuł pomaga w sprawdzeniu poprawności następujących danych wejściowych:

- **Aplikacje**: Wyświetl listę wszystkich aplikacji uwzględnionych w tym obciążeniu.
- **Maszyny wirtualne/serwery**: Wyświetl listę wszystkich maszyn wirtualnych lub serwerów uwzględnionych w obciążeniu.
- **Źródła danych**: Wyświetl listę wszystkich źródeł danych uwzględnionych w obciążeniu.
- **Zależności**: Wyświetl listę wszystkich zależności zasobów, które nie są uwzględnione w obciążeniu.

Istnieje kilka opcji związanych z montażem tych danych. Poniżej przedstawiono kilka najczęstszych metod.

## <a name="alternative-inputs-migrate-modernize-innovate"></a>Alternatywne dane wejściowe: Migrowanie, modernizacja, innowacje

Celem powyższych punktów danych jest przechwycenie względnych nakładów technicznych i zależności jako pomocy do priorytetyzacji. W zależności od żądanego przejścia może być konieczne zebranie alternatywnych punktów danych w celu zapewnienia obsługi właściwej priorytetyzacji.

**Migracja:** W przypadku czystych wysiłków związanych z migracją istniejący spis i zależności zasobów stanowią godziwą miarę relatywnej złożoności.

**Modernizowanie** Gdy celem obciążenia jest modernizacja aplikacji lub innych zasobów, te punkty danych są nadal trwałymi środkami złożoności. Można jednak dodać dane wejściowe dla możliwości modernizacji do dokumentacji dotyczącej obciążeń.

**Innowacje:** Gdy dane lub logika biznesowa zmieniają się istotnie podczas nakładu pracy związanej z wdrażaniem w chmurze, uważa się, że typ transformacji jest innowacyjny. Ta sama wartość jest prawdziwa podczas tworzenia nowych danych lub nowej logiki biznesowej. W przypadku jakichkolwiek scenariuszy innowacji migracja zasobów będzie prawdopodobnie stanowić najmniejszą ilość wymaganego nakładu pracy. Dla tych scenariuszy zespół powinien opracować zestaw danych technicznych, aby zmierzyć relatywną złożoność.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate udostępnia zestaw funkcji grupowania, które mogą przyspieszyć agregację aplikacji, maszyn wirtualnych, źródeł danych i zależności. Po zdefiniowaniu pojęciowych obciążeń można ich użyć jako podstawy grupowania zasobów na podstawie mapowania zależności.

Dokumentacja Azure Migrate zawiera wskazówki dotyczące [sposobu grupowania maszyn w oparciu o zależności](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies).

## <a name="configuration-management-database"></a>Baza danych zarządzania konfiguracją

Niektóre organizacje mają dobrze obsługiwaną bazę danych zarządzania konfiguracją (CMDB) w ramach istniejących narzędzi do zarządzania operacjami. Mogą oni korzystać z programu CMDB, aby dostarczyć punkty danych wejściowych omówione wcześniej.

## <a name="next-steps"></a>Następne kroki

[Sprawdź decyzje](./review-rationalization.md) dotyczące racjonalizacji na podstawie wyrównania zasobów i definicji obciążeń.

> [!div class="nextstepaction"]
> [Przegląd decyzji o racjonalizacji](./review-rationalization.md)