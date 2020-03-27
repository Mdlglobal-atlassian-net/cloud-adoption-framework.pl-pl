---
title: Co nowego
description: Dowiedz się więcej na temat aktualizacji platformy wdrażania Microsoft Cloud dla platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: a3e316d49acaaee00d5ecd10efac9aa15c2dbd49
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80353676"
---
# <a name="whats-new-in-the-microsoft-cloud-adoption-framework"></a>Co nowego w platformie wdrażania Microsoft Cloud

## <a name="fulfilling-the-vision"></a>Realizacja wizji

Struktura stała się ogólnie dostępna. Jednak nadal aktywnie tworzymy tę strukturę we współpracy z klientami, partnerami i zespołami wewnętrznymi. Aby zachęcić do partnerstwa, zawartość jest udostępniana, gdy tylko stanie się dostępna. Te publiczne wydania umożliwiają testowanie, weryfikowanie i stopniowe udoskonalanie wskazówek.

Znaczące zmiany są przechwytywane w następujących informacjach o wersji.

## <a name="migration-update-03022020"></a>Aktualizacja migracji: 03/02/2020

W tej wersji zawarto informacje na temat ciągłości podejścia migracji za pomocą wielu metodologii, takich jak strategia, planowanie, przygotowanie i migracja. Celem tej wersji jest ułatwienie czytelnikom zrozumienia ciągłego ulepszania planowania i wdrażania, ponieważ klienci kontynuują pracę z migracją. Wprowadzono następujące zmiany w celu zaspokojenia duchu tej wersji:

### <a name="new-articles"></a>Nowe artykuły

- [Zrównoważ konkurencyjne priorytety](../strategy/balance-competing-priorities.md): przedstawiają saldo w priorytetach występujących w każdej metodologii do informowania o strategiach klientów
- [Klasyfikacja podczas oceny procesów](../migrate/migration-considerations/assess/classify.md): przedstawia znaczenie klasyfikowania wszystkich zasobów i obciążeń przed migracją.

### <a name="restructure-landing-zone-process"></a>Restrukturyzacja procesu strefy wyładunkowej

Pierwsza strefa docelowa została wyściągana z przewodnika gotowości, aby można było korzystać z niej jako jej własnej sekcji. Takie podejście umożliwia rozwinięcie koncepcji stref wyładunkowych i opcji strefy docelowej. Prowadzi to również do tworzenia kilku nowych artykułów:

- [Co to jest strefa wyładunkowe?](../ready/landing-zone/index.md): definiuje termin strefy docelowej
- [Pierwsza strefa](../ready/landing-zone/first-landing-zone.md)docelowa: rozwija w porównaniu z różnymi strefami wyładunkowymi
- [Migrowanie strefy docelowej](../ready/landing-zone/migrate-landing-zone.md): przeniesiono wcześniejszy artykuł planu strefy docelowej, aby oddzielić definicję planu CAF od zaznaczenia pierwszej strefy docelowej, aby umożliwić im więcej opcji strefy wyładunkowej.
- Terraform — artykuł dotyczący [strefy wyładunkowej](../ready/landing-zone/terraform-landing-zone.md) : przeniesiony z sekcji "rozszerzony zakres" gotowej metodologii do nowej sekcji "strefa docelowa" metody gotowej do traktowania Terraforma jako obywatel pierwszej klasy w konwersacji strefy docelowej.
- Grupuj podstawowe zagadnienia dotyczące strefy docelowej w spisie treści w obszarze "podstawowe zagadnienia dotyczące strefy wyładunkowej".
- Przeniesiono najlepsze rozwiązania w zakresie zabezpieczeń z metodologii migrowania do nowej sekcji strefy docelowej wywoływanie "Popraw zabezpieczenia strefy wyładunkowej (dane poufne)", aby uwidocznić te wskazówki wcześniej w cyklu życia.

### <a name="refinements-to-the-azure-migration-guide"></a>Udoskonalenia przewodnika migracji platformy Azure

Wzorce ruchu użytkowników sugerują, że ta sekcja zawartości może być używana przez implementacje i architektów podczas pierwszej migracji. Aby zapewnić lepszą obsługę tych odbiorców, fokus przewodnika migracji został ulepszony, aby lepiej dostosować się do oryginalnego zamiaru ujawnienia czytelników do narzędzi używanych podczas pierwszej migracji.

- [Przegląd](../migrate/azure-migration-guide/index.md): wyraźniejszy opis przewodnika z ograniczoną liczbą kroków.
- [Ocena](../migrate/azure-migration-guide/assess.md): lepszym rozwiązaniem jest to, że ocena w tej fazie koncentruje się na ocenie dopasowania technicznego określonego obciążenia i powiązanych zasobów. Dodano sekcję założeń wymagających, aby zademonstrować, kto ten poziom oceny współdziała z podejściem do oceny przyrostowej wymienionym najpierw w metodologii planu.
- [Migrowanie](../migrate/azure-migration-guide/migrate.md): w odpowiedzi na opinie w ramach konferencji warstwy 1, odwołanie do UnifyCloud zostało dodane do opcji narzędzia innych firm.
- [Testowanie, optymalizowanie i podwyższanie poziomu](../migrate/azure-migration-guide/optimize-and-transform.md): wyrównywanie tytułu tego artykułu przy użyciu innych sugestii dotyczących ulepszeń procesów.

### <a name="refinements-to-migration-process-improvements"></a>Udoskonalenia dotyczące ulepszeń procesów migracji

- [Przegląd oceniania](../migrate/migration-considerations/assess/index.md): lepszym rozwiązaniem jest ocena w tej fazie, która koncentruje się na ocenie dopasowania technicznego określonego obciążenia i powiązanych zasobów.
- [Planowanie listy kontrolnej](../migrate/migration-considerations/prerequisites/planning-checklist.md): wyjaśnienie znaczenia operacji podczas planowania migracji w celu zapewnienia dobrego zarządzania obciążeniami, po migracji.

### <a name="placement-of-related-articles"></a>Umieszczanie powiązanych artykułów

Poniższa lista artykułów została przeniesiona. Ruch jest przekierowywany do nowej lokalizacji.

- Artykuł dotyczący najlepszych rozwiązań dotyczących [oceny](../plan/contoso-migration-assessment.md) : przeniesiono z sekcji "najlepsze praktyki" dotyczącej metodologii migrowania do nowej "najlepszej praktyki" dotyczącej metodologii planu. To przeniesienie uwidacznia czytelnikom praktyczną ocenę środowiska lokalnego wcześniej w cyklu życia.
- [Balansowanie artykułu portfolio](../strategy/balance-the-portfolio.md) : przeniesione z sekcji "rozszerzony zakres" metodologii migrowania do metodologii strategii. To przeniesienie udostępnia czytelnikom ten proces myśli wcześniej w cyklu życia.

### <a name="alignment-of-the-changes"></a>Wyrównanie zmian

- [Przegląd gotowości](../ready/index.md): należy zaktualizować cztery kroki w gotowym przeglądzie, aby odzwierciedlić proces rafinowany
- [Omówienie migracji](../migrate/index.md): należy zaktualizować kroki z omówienia migracji, aby odzwierciedlić proces rafinowany
- [Grafika metodologii migracji](../migrate/index.md): Aktualizacja do obrazu metodologii w celu odzwierciedlenia zmian
- [Ilustracja przedstawiająca przegląd](../index.md): aktualizacje grafiki przeglądowej w celu odzwierciedlenia zmian
