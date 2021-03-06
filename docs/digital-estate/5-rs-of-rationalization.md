---
title: Racjonalizacja chmury
description: Dowiedz się więcej na temat racjonalizacji chmury, procesu oceny zasobów, aby określić najlepszy sposób migracji lub modernizacji poszczególnych elementów zawartości w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/16/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 5c4098e2d5655d3b0fbb7fcb1c5a0470547421f3
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83753558"
---
# <a name="cloud-rationalization"></a>Racjonalizacja chmury

Racjonalizacja chmury to proces oceniania zasobów w celu ustalenia najlepszego sposobu migracji lub modernizacji każdego elementu zawartości w chmurze. Aby uzyskać więcej informacji na temat procesu racjonalizacji, zobacz [co to jest znak cyfrowy?](./index.md).

## <a name="rationalization-context"></a>Kontekst racjonalizacji

_Pięć_ kandydatów wymienionych w tym artykule jest świetnym sposobem na oznaczenie potencjalnego przyszłego stanu wszelkich obciążeń, które są uważane za kandydata w chmurze. Ten proces etykietowania powinien być umieszczony w prawidłowym kontekście przed podjęciem próby racjonalizacji środowiska. Aby zapewnić ten kontekst, przejrzyj następujący mitów:

### <a name="myth-its-easy-to-make-rationalization-decisions-early-in-the-process"></a>Omówienia: łatwo jest szybko podejmować decyzje o racjonalizacji w procesie

 Dokładne racjonalizacja wymaga głębokiej znajomości obciążeń i skojarzonych zasobów (aplikacji, maszyn wirtualnych i danych). Najważniejsze decyzje podejmowane są z dokładnością. Zalecamy korzystanie z [procesu racjonalizacji przyrostowej](./rationalize.md#incremental-rationalization).

### <a name="myth-cloud-adoption-has-to-wait-for-all-workloads-to-be-rationalized"></a>Omówienia: wdrażanie w chmurze musi oczekiwać na uzasadnienie wszystkich obciążeń

Racjonalizacja całego portfolio IT lub nawet jednego centrum danych może opóźnić realizację wartości biznesowej według miesięcy lub nawet lat. W miarę możliwości należy unikać pełnej racjonalizacji. Zamiast tego należy użyć [mocy 10 podejścia do wydania planowania](./rationalize.md#release-planning) , aby podejmować odpowiednie decyzje dotyczące kolejnych 10 obciążeń, które są styczeń na potrzeby wdrażania w chmurze.

### <a name="myth-business-justification-has-to-wait-for-all-workloads-to-be-rationalized"></a>Omówienia: uzasadnienie biznesowe musi oczekiwać na uzasadnienie wszystkich obciążeń

Aby opracować uzasadnienie biznesowe dla wysiłku związanego z wdrażaniem w chmurze, należy wprowadzić kilka podstawowych założeń na poziomie portfela. Gdy motywacje są wyrównane do innowacyjności, założono, że architektura zostanie wdrożona. Gdy motywacje są wyrównane do migracji, założono, że rehosty. Te założenia mogą przyspieszyć proces uzasadnienia biznesowego. Założenia są następnie zakwestionowane i budżety są udoskonalane w fazie oceny poszczególnych cykli wdrażania obciążeń.

Zapoznaj się z poniższą piątą z pięciu usprawnień, aby zaznajomić się z długoterminowym procesem. Podczas opracowywania planu wdrażania w chmurze wybierz opcję, która najlepiej odpowiada Twoim potrzebom, rezultatom biznesowym i bieżącemu środowisku stanu. Celem na potrzeby racjonalizacji cyfrowej jest ustawienie linii bazowej, a nie podniesienia poziomu każdego obciążenia.

## <a name="the-five-rs-of-rationalization"></a>Pięć zasad racjonalizacji

Pięć z pięciu usprawnień, które są wymienione w tym miejscu, opisują najbardziej typowe opcje racjonalizacji.

## <a name="rehost"></a>Zmienianie hosta

Zgodnie z potrzebami migracji przenoszonych _i przenoszonych_ na przechodzenie przenoszone jest bieżący zasób stanu do wybranego dostawcy chmury z minimalnymi zmianami ogólnej architektury.

Typowe sterowniki mogą obejmować:

- Zmniejszenie wydatków inwestycyjnych.
- Zwalnianie miejsca w centrum danych.
- Osiągnięcie szybkiego powrotu do inwestycji w chmurę.

Czynniki analizy ilościowej:

- Rozmiar maszyny wirtualnej (procesor, pamięć, magazyn).
- Zależności (ruch sieciowy).
- Zgodność zasobów.

Czynniki analizy jakościowej:

- Tolerancja zmiany.
- Priorytety biznesowe.
- Krytyczne zdarzenia biznesowe.
- Zależności procesów.

## <a name="refactor"></a>Refaktoryzacja

Opcje platforma jako usługa (PaaS) umożliwiają zmniejszenie kosztów operacyjnych skojarzonych z wieloma aplikacjami. Dobrym pomysłem jest nieznacznie Refaktoryzacja aplikacji do modelu opartego na PaaS.

"Refaktoryzacja" odnosi się również do procesu tworzenia aplikacji w kodzie refaktoryzacji, aby umożliwić aplikacji dostarczanie nowych możliwości biznesowych.

Typowe sterowniki mogą obejmować:

- Szybsze i krótsze aktualizacje.
- Przenośność kodu.
- Większa wydajność chmury (zasoby, szybkość, koszt, operacje zarządzane).

Czynniki analizy ilościowej:

- Rozmiar zasobu aplikacji (procesor CPU, pamięć, magazyn).
- Zależności (ruch sieciowy).
- Ruch użytkownika (wyświetlenia stron, czas na stronie, czas ładowania).
- Platforma programistyczna (Języki, platforma danych, usługi warstwy środkowej).
- Baza danych (procesor CPU, pamięć, magazyn, wersja).

Czynniki analizy jakościowej:

- Dalsze inwestycje biznesowe.
- Opcje i osie czasu.
- Zależności procesów firmy.

## <a name="rearchitect"></a>Zmienianie architektury

Niektóre aplikacje przedawniania nie są zgodne z dostawcami chmury ze względu na decyzje dotyczące architektury, które zostały wykonane podczas kompilowania aplikacji. W takich przypadkach może być konieczne ponowne zaprojektowanie aplikacji przed przekształceniem.

W innych przypadkach aplikacje, które są zgodne z chmurą, ale nie są natywne w chmurze, mogą powodować wzrost kosztów i efektywność operacyjną dzięki ponownemu tworzeniu architektury rozwiązania w aplikacji natywnej w chmurze.

Typowe sterowniki mogą obejmować:

- Skalowalność i elastyczność aplikacji.
- Łatwiejsze wdrażanie nowych możliwości chmury.
- Mieszanie stosów technologicznych.

Czynniki analizy ilościowej:

- Rozmiar zasobu aplikacji (procesor CPU, pamięć, magazyn).
- Zależności (ruch sieciowy).
- Ruch użytkownika (wyświetlenia stron, czas na stronie, czas ładowania).
- Platforma programistyczna (Języki, platforma danych, usługi warstwy środkowej).
- Baza danych (procesor CPU, pamięć, magazyn, wersja).

Czynniki analizy jakościowej:

- Rosnące inwestycje biznesowe.
- Koszty operacyjne.
- Potencjalni pętle opinii i DevOps inwestycje.

## <a name="rebuild"></a>Ponowne kompilowanie

W niektórych scenariuszach różnica, którą należy przezwyciężyć w celu przeniesienia aplikacji, może być zbyt duża, aby uzasadnić dalsze inwestycje. Jest to szczególnie ważne w przypadku aplikacji, które wcześniej spełniały potrzeby biznesowe, ale są teraz nieobsługiwane lub nieprawidłowo wyrównane z bieżącymi procesami biznesowymi. W takim przypadku tworzony jest nowy podstawowy kod, który będzie wyrównany z podejściem [natywnym w chmurze](https://azure.microsoft.com/overview/cloudnative) .

Typowe sterowniki mogą obejmować:

- Przyspieszanie innowacji.
- Szybsze tworzenie aplikacji.
- Zmniejszenie kosztów operacyjnych.

Czynniki analizy ilościowej:

- Rozmiar zasobu aplikacji (procesor CPU, pamięć, magazyn).
- Zależności (ruch sieciowy).
- Ruch użytkownika (wyświetlenia stron, czas na stronie, czas ładowania).
- Platforma programistyczna (Języki, platforma danych, usługi warstwy środkowej).
- Baza danych (procesor CPU, pamięć, magazyn, wersja).

Czynniki analizy jakościowej:

- Odrzucanie zadowolenia użytkowników końcowych.
- Procesy biznesowe ograniczone przez funkcje.
- Potencjalny koszt, doświadczenie lub zyski z przychodów.

## <a name="replace"></a>Replace

Rozwiązania są zwykle implementowane przy użyciu najlepszej technologii i metody dostępnej w danym momencie. Czasami aplikacje SaaS (Software as a Service) mogą zapewnić wszystkie niezbędne funkcje aplikacji hostowanej. W tych scenariuszach obciążenie może zostać zaplanowane do przyszłego zastąpienia, co skutecznie eliminuje je z wysiłku transformacji.

Typowe sterowniki mogą obejmować:

- Ujednolicenie najlepszych praktyk branżowych.
- Przyspieszanie wdrażania podejścia sterowanego procesami biznesowymi.
- Ponowna alokacja inwestycji programistycznych do aplikacji, które tworzą zróżnicowane lub zalety konkurencji.

Czynniki analizy ilościowej:

- Ogólne redukcje kosztów operacyjnych.
- Rozmiar maszyny wirtualnej (procesor, pamięć, magazyn).
- Zależności (ruch sieciowy).
- Zasoby do wycofania.
- Baza danych (procesor CPU, pamięć, magazyn, wersja).

Czynniki analizy jakościowej:

- Analiza kosztów związanych z bieżącą architekturą w porównaniu z rozwiązaniem SaaS.
- Mapy procesów firmy.
- Schematy danych.
- Procesy niestandardowe lub zautomatyzowane.

## <a name="next-steps"></a>Następne kroki

Zbiorczo można zastosować te pięć informacji o racjonalizacji do cyfr cyfrowych, aby ułatwić podejmowanie decyzji o racjonalizacji w przyszłości.

> [!div class="nextstepaction"]
> [Co to jest majątek cyfrowy?](./index.md)
