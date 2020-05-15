---
title: Zarządzanie dopasowaniem organizacji
description: Użyj struktury wdrażania chmury dla platformy Azure, aby dowiedzieć się, jak ustanowić i utrzymać dopasowanie organizacji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 2a8bdf2e19d9db6912f66937a0053ee6102cbeac
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401028"
---
# <a name="manage-organizational-alignment"></a>Zarządzanie dopasowaniem organizacji

Wdrożenie chmury nie jest możliwe bez dobrze zorganizowanych ludzi. Pomyślne wdrożenie chmury jest wynikiem pracy odpowiednio wykwalifikowanych osób wykonujących właściwe typy zadań dopasowanych do przejrzyście zdefiniowanych celów biznesowych w dobrze zarządzanym środowisku. Dostarczenie efektywnego modelu operacyjnego na potrzeby chmury wymaga określenia struktur organizacyjnych obsadzonych odpowiednim personelem. W tym dokumencie omówiono metodę ustanawiania i utrzymywania odpowiednich struktur organizacyjnych w czterech krokach.

Poniższe ćwiczenia ułatwiają przejście procesu tworzenia strefy docelowej do obsługi wdrażania chmury.

<!-- markdownlint-disable MD033 -->

| | |
|---|---|
| <br> ![1](../_Images/icons/1.png)     | [Typ struktury](#structure-type): Zdefiniuj typ struktury organizacyjnej, który najlepiej odpowiada Twojemu modelowi operacyjnemu.                                |
| <br> ![2](../_Images/icons/2.png)     | [Funkcje w chmurze](#understand-required-cloud-functions): Poznaj funkcje chmury wymagane do wdrożenia i obsługi chmury.                                |
| <br> ![3](../_Images/icons/3.png)     | [Dojrzałe struktury zespołów](./organization-structures.md): Zdefiniuj zespoły, które mogą realizować różne funkcje w chmurze.                                |
| <br> ![4](../_Images/icons/4.png)      | [Macierz odpowiedzialności w modelu RACI](./raci-alignment.md): Jasno zdefiniowane role są ważnym aspektem każdego modelu operacyjnego. Skorzystaj z podanej macierzy odpowiedzialności w modelu RACI (Responsible, Accountable, Consulted, Informed), aby przydzielić role osób odpowiedzialnych za wykonanie zadania, nadzorujących wykonanie zadania, konsultujących wykonanie zadania i informowanych o wykonaniu zadania we wszystkich zespołach dla różnych funkcji modelu operacyjnego chmury.                        |

## <a name="structure-type"></a>Typ struktury

Poniższe struktury organizacyjne nie muszą być koniecznie mapowane na schemat organizacyjny. Schematy organizacyjne zwykle odzwierciedlają struktury zarządzania sterowania i kontroli. Z kolei następujące struktury organizacyjne mają na celu uchwycenie dopasowania ról i obowiązków. W elastycznej organizacji macierzowej najlepszym przedstawieniem tych struktur mogą być zespoły wirtualne. Nie ma żadnego ograniczenia sugerującego, że tych struktur organizacyjnych nie można przedstawić w schemacie organizacyjnym, ale nie jest to konieczne do utworzenia efektywnego modelu operacyjnego.

Pierwszym krokiem w zarządzaniu dopasowaniem organizacji jest ustalenie, jak należy wypełnić następujące struktury organizacyjne:

- **Dopasowanie schematu organizacyjnego:** Hierarchie zarządzania, zakres odpowiedzialności menedżerów i dopasowanie personelu będzie zgodne ze strukturami organizacyjnymi.
- **Zespoły wirtualne:** Struktury zarządzania i schematy organizacyjne pozostaną bez zmian. Zamiast tego zostaną utworzone zespoły wirtualne, którym będą przydzielane zadania dotyczące wymaganych funkcji.
- **Model mieszany:** Zwykle, aby osiągnąć cele transformacji, wymagane jest połączenie dopasowania schematu organizacyjnego i zespołów wirtualnych.

## <a name="understand-required-cloud-functions"></a>Poznanie wymaganych funkcji chmury

Poniżej znajduje się lista funkcji, które są wymagane do pomyślnego wdrożenia chmury i długoterminowych modeli operacyjnych. Po poznaniu tych funkcji można je dopasować do struktur organizacyjnych, stosownie do zatrudnienia i poziomu dojrzałości:

- [Strategia chmury](./cloud-strategy.md): Dopasowanie zmian technicznych do potrzeb biznesowych.
- [Wdrożenie chmury](./cloud-adoption.md): Dostarczanie rozwiązań technicznych.
- [Ład w chmurze](./cloud-governance.md): Zarządzanie ryzykiem.
- [Centralny zespół IT](./central-it.md): Pomoc techniczna od obecnych pracowników działu IT.
- [Operacje w chmurze](./cloud-operations.md): Wsparcie techniczne i obsługa przyjętych rozwiązań.
- [Centrum doskonałości chmury](./cloud-center-of-excellence.md): Zwiększanie jakości, szybkości i odporności wdrożenia.
- [Platforma w chmurze](./cloud-platform.md): Obsługa i rozwijanie platformy.
- [Automatyzacja chmury](./cloud-automation.md): Przyspieszanie wdrażania i innowacji.
- [Zabezpieczenia w chmurze](./cloud-security.md): Zarządzanie ryzykiem związanym z bezpieczeństwem informacji.

Do pewnego stopnia każda z powyższych funkcji jest realizowana w każdym wdrożeniu chmury, jawnie lub zgodnie ze zdefiniowaną strukturą zespołu.

Wraz z rozwojem potrzeb wdrożenia zwiększa się konieczność zachowania równowagi i struktury. Aby spełnić te wymagania, firmy często przechodzą proces rozwijania struktur organizacyjnych.

![Cykl rozwoju organizacji](../_images/ready/org-ready-maturity.png)

Artykuł na temat [określania dojrzałości struktur organizacyjnych](./organization-structures.md) zawiera dodatkowe szczegóły dotyczące każdego poziomu dojrzałości.

Aby śledzić decyzje dotyczące struktury organizacji w miarę upływu czasu, pobierz i zmodyfikuj [szablon arkusza kalkulacyjnego odpowiedzialności](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).
