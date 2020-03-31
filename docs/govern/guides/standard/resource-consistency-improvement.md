---
title: 'Standardowe zarządzanie przedsiębiorstwem: zwiększanie spójności zasobów'
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się więcej o ulepszaniu planu bazowego zarządzania i dodawaniu kontroli odzyskiwania, określania rozmiarów i monitorowania w celu korygowania zagrożeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6228bc4a2f4a2217ab7cd226ace5075c91a52dfc
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434206"
---
# <a name="standard-enterprise-governance-guide-improving-resource-consistency"></a>Standardowy Przewodnik dotyczący zarządzania przedsiębiorstwem: zwiększanie spójności zasobów

W tym artykule opisano sposób dodawania kontroli spójności zasobów do obsługi aplikacji o znaczeniu strategicznym.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Nowe środowiska klienta, nowe narzędzia do prognozowania i migrowana infrastruktura kontynuują postęp. Firma jest teraz gotowa do rozpoczęcia korzystania z tych zasobów w pojemności produkcyjnej.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

W poprzedniej fazie tego rozbudowy aplikacje i zespoły analizy biznesowej były prawie gotowe do integrowania danych klienta i finansów z obciążeniami produkcyjnymi. Zespół IT był w trakcie wycofywania centrum danych programu DR.

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- Wystąpiło wycofanie 100% centrum danych DR przed zaplanowanym harmonogramem. W procesie zestaw zasobów w produkcyjnym centrum danych został zidentyfikowany jako kandydat migracji do chmury.
- Zespoły deweloperów aplikacji są teraz gotowe do ruchu produkcyjnego.
- Zespół analizy biznesowej jest gotowy do podawania prognoz i wglądu w systemy operacyjne w centrum danych produkcyjnych.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Przed rozpoczęciem korzystania z wdrożeń platformy Azure w produkcyjnych procesach roboczych, operacje w chmurze muszą zostać dojrzałe. W związku z tym wymagane są dodatkowe zmiany ładu, aby zapewnić, że zasoby mogą działać prawidłowo.

Zmiany bieżącego i przyszłego stanu ujawniają nowe zagrożenia, które będą wymagały nowych instrukcji zasad.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Zakłócenia biznesowe:** Istnieje ryzyko związane z każdą nową platformą powodującą zakłócenia procesów biznesowych o kluczowym znaczeniu. Zespół operacyjny IT i zespoły wykonujące różne wydłużać w chmurze są stosunkowo niezawodnie związane z operacjami w chmurze. Zwiększa to ryzyko przerwania działania i należy je skorygować i zarządzać nimi.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

1. Zewnętrzna wtargnięcie lub ataki typu "odmowa usługi" mogą spowodować przerwanie działania biznesowego.
2. Zasoby o kluczowym znaczeniu mogą nie zostać prawidłowo odnalezione i w związku z tym mogą nie być prawidłowo obsługiwane.
3. Niewykrywalne lub nieoznaczone elementy zawartości mogą nie być obsługiwane przez istniejące procesy zarządzania operacyjnego.
4. Konfiguracja wdrożonych zasobów może nie spełniać oczekiwań wydajności.
5. Rejestrowanie może nie być poprawnie rejestrowane i scentralizowane, aby można było rozwiązywać problemy z wydajnością.
6. Zasady odzyskiwania mogą zakończyć się niepowodzeniem lub dłużej niż oczekiwano.
7. Niespójne procesy wdrażania mogą powodować luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
8. Nałożenia konfiguracyjne lub pominięte poprawki mogą spowodować niezamierzone luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
9. Konfiguracja może nie wymusić wymagań zdefiniowanych umowy SLA lub zatwierdzono wymagania dotyczące odzyskiwania.
10. Wdrożone systemy operacyjne lub aplikacje mogą nie spełniać wymagań związanych z ograniczaniem funkcjonalności.
11. Dzięki temu wiele zespołów pracujących w chmurze istnieje ryzyko niespójności.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika. Lista będzie wyglądać długa, ale stosowanie tych zasad może być łatwiejsze niż wyświetlona.

1. Wszystkie wdrożone zasoby muszą być pogrupowane według stopnia ważności i klasyfikacji danych. Klasyfikacje muszą być przeglądane przez zespół ładu chmury i właściciela aplikacji przed wdrożeniem w chmurze.
2. Podsieci zawierające aplikacje o znaczeniu krytycznym muszą być chronione przez rozwiązanie zapory, które może wykrywać wtargnięcie i odpowiadać na ataki.
3. Narzędzia ładu muszą przeprowadzać inspekcję i wymuszać wymagania dotyczące konfiguracji sieci zdefiniowane przez zespół zarządzania zabezpieczeniami.
4. Narzędzia ładu muszą sprawdzać poprawność wszystkich zasobów związanych z aplikacjami o znaczeniu krytycznym lub chronionych danych, które są objęte monitorowaniem i optymalizacją zasobów.
5. Narzędzia ładu muszą sprawdzić, czy odpowiedni poziom danych rejestrowania jest zbierany dla wszystkich aplikacji o kluczowym znaczeniu lub chronionych danych.
6. Proces ładu musi sprawdzać poprawność wdrożenia kopii zapasowej, odzyskiwania i umowy SLA dla aplikacji o kluczowym znaczeniu i chronionych danych.
7. Narzędzia ładu muszą ograniczać wdrożenia maszyny wirtualnej tylko do zatwierdzonych obrazów.
8. Narzędzia ładu muszą wymusić, że aktualizacje automatyczne są blokowane we wszystkich wdrożonych zasobach, które obsługują aplikacje o znaczeniu strategicznym. Naruszenia muszą zostać sprawdzone za pomocą zespołów zarządzania operacyjnego i korygowane zgodnie z zasadami operacji. Zasoby, które nie są automatycznie aktualizowane, muszą być uwzględnione w procesach należących do operacji IT.
9. Narzędzia ładu muszą sprawdzać poprawność tagowania związanego z kosztami, krytycznością, umową SLA, aplikacją i klasyfikacją danych. Wszystkie wartości muszą być wyrównane do wstępnie zdefiniowanych wartości zarządzanych przez zespół nadzoru.
10. Procesy nadzoru muszą obejmować inspekcje w punkcie wdrożenia oraz regularne cykle w celu zapewnienia spójności wszystkich zasobów.
11. Trendy i luki w zabezpieczeniach, które mogą mieć wpływ na wdrożenia w chmurze, powinny być regularnie przeglądane przez zespół ds. zabezpieczeń, aby zapewnić aktualizacje narzędzi do zarządzania zabezpieczeniami używane w chmurze.
12. Przed wprowadzeniem do środowiska produkcyjnego należy dodać wszystkie aplikacje o kluczowym znaczeniu oraz chronione dane do wyprodukowanego rozwiązania do monitorowania operacyjnego. Nie można zwolnić zasobów, które nie mogą zostać odnalezione przez wybrane narzędzia do obsługi operacji IT. Wszelkie zmiany wymagane do odnajdywania zasobów muszą zostać wprowadzone do odpowiednich procesów wdrażania, aby zapewnić, że zasoby będą wykrywalne w przyszłych wdrożeniach.
13. Po ich wykryciu zespoły zarządzania operacyjnego będą mieć rozmiar zasobów, aby zapewnić, że zasoby spełniają wymagania dotyczące wydajności.
14. Narzędzia do wdrażania muszą zostać zatwierdzone przez zespół ds. zarządzania chmurą, aby zapewnić ciągły nadzór nad wdrożonymi zasobami.
15. Skrypty wdrażania muszą być utrzymywane w centralnym repozytorium dostępnym dla zespołu ładu chmury w celu okresowego przeglądania i inspekcji.
16. Procesy nadzoru ładu muszą sprawdzać, czy wdrożone zasoby są prawidłowo skonfigurowane, zgodnie z wymaganiami umowy SLA i odzyskiwania.

## <a name="incremental-improvement-of-governance-practices"></a>Przyrostowe ulepszanie praktyk w zakresie zapewniania ładu

W tej części artykułu zostanie zmieniony projekt ładu MVP, który obejmuje nowe zasady platformy Azure i implementację Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

1. Zespół operacyjny w chmurze będzie definiować narzędzia monitorowania operacyjnego i zautomatyzowane narzędzia do korygowania. Zespół ds. zarządzania chmurą będzie obsługiwał te procesy odnajdywania. W tym przypadku użycia zespół operacyjny w chmurze wybiera Azure Monitor jako podstawowe narzędzie do monitorowania aplikacji o krytycznym znaczeniu.
2. Utwórz repozytorium w usłudze Azure DevOps, aby przechowywać i wypełniać wszystkie odpowiednie szablony Menedżer zasobów i konfiguracje inicjowane przez skrypty.
3. Implementacja magazynu Recovery Services platformy Azure:
    1. Zdefiniuj i Wdróż magazyn Recovery Services platformy Azure na potrzeby procesów tworzenia kopii zapasowych i odzyskiwania.
    2. Utwórz szablon Menedżer zasobów na potrzeby tworzenia magazynu w ramach każdej subskrypcji.
4. Azure Policy aktualizacji dla wszystkich subskrypcji:
    1. Przeprowadzaj inspekcję i wymuszanie stopnia ważności i klasyfikacji danych w ramach wszystkich subskrypcji, aby identyfikować wszystkie subskrypcje z zasobami o kluczowym znaczeniu.
    2. Inspekcja i wymuszanie używania tylko zatwierdzonych obrazów.
5. Implementacja Azure Monitor:
    1. Po zidentyfikowaniu obciążenia o krytycznym znaczeniu należy utworzyć obszar roboczy Azure Monitor.
    2. Podczas testowania wdrożenia zespół operacyjny chmury wdraża niezbędnych agentów i testy odnajdywania.
6. Aktualizacja Azure Policy dla wszystkich subskrypcji, które zawierają aplikacje o znaczeniu krytycznym.
    1. Inspekcja i wymuszanie aplikacji sieciowej grupy zabezpieczeń na wszystkich kartach sieciowych i podsieciach. Sieć i zabezpieczenia IT definiują sieciowej grupy zabezpieczeń.
    2. Inspekcja i wymuszanie użycia zatwierdzonych podsieci sieciowych i sieci wirtualnych dla każdego interfejsu sieciowego.
    3. Inspekcja i wymuszanie ograniczenia zdefiniowanych przez użytkownika tabel routingu.
    4. Inspekcja i wymuszanie wdrażania agentów Azure Monitor dla wszystkich maszyn wirtualnych.
    5. Inspekcja i wymuszanie, że magazyny usługi Azure Recovery Services istnieją w ramach subskrypcji.
7. Konfiguracja zapory:
    1. Zidentyfikuj konfigurację zapory platformy Azure spełniającą wymagania dotyczące zabezpieczeń. Alternatywnie Zidentyfikuj urządzenie innej firmy zgodne z platformą Azure.
    1. Utwórz szablon Menedżer zasobów, aby wdrożyć zaporę z wymaganymi konfiguracjami.
8. Plan platformy Azure:
    1. Utwórz nowy plan platformy Azure o nazwie `protected-data`.
    2. Dodaj zaporę i szablony magazynu platformy Azure do planu.
    3. Dodaj nowe zasady dla chronionych subskrypcji danych.
    4. Opublikuj plan w dowolnej grupie zarządzania, która będzie hostować aplikacje o kluczowym znaczeniu.
    5. Zastosuj nowy plan do każdej powiązanej subskrypcji, a także istniejące plany.

## <a name="conclusion"></a>Podsumowanie

Te dodatkowe procesy i zmiany wprowadzane przez ładu MVP są pomocne w korygowaniu wielu zagrożeń związanych z zarządzaniem zasobami. Razem dodają funkcje kontroli odzyskiwania, rozmiarów i monitorowania, które umożliwiają wykonywanie operacji opartych na chmurze.

## <a name="next-steps"></a>Następne kroki

Gdy wdrożenie chmury będzie kontynuowane i zapewnia dodatkową wartość biznesową, zagrożenia i potrzeby ładu chmury również zostaną zmienione. W przypadku fikcyjnej firmy w tym przewodniku następnym wyzwalaczem jest, gdy skala wdrożenia przekroczy 100 zasobów do chmury, lub miesięczne wydatki przekraczają $1 000 miesięcznie. W tym momencie zespół nadzorujący chmury dodaje Cost Management kontrolek.

> [!div class="nextstepaction"]
> [Ulepszanie Cost Management](./cost-management-improvement.md)
