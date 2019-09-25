---
title: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny spójności zasobów'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny spójności zasobów'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9875fb2ebc6948d22ac6eaf350f9784b61fd4dc3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223813"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny spójności zasobów

Ten artykuł postępuje zgodnie z opisami, dodając kontrolki spójności zasobów do ładu MVP, aby obsługiwały aplikacje o znaczeniu strategicznym.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Zespoły wdrażania chmury spełniały wszystkie wymagania dotyczące przenoszenia chronionych danych. Dzięki tym aplikacjom zobowiązania SLA są dostępne dla firmy i potrzebne do pomocy technicznej. Bezpośrednio nad zespołem, który migruje dwa centra danych, wiele aplikacji i zespołów analizy biznesowej jest gotowych do rozpoczęcia uruchamiania nowych rozwiązań w środowisku produkcyjnym. Operacje IT są nowe dla operacji w chmurze i muszą szybko zintegrować istniejące procesy operacyjne.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

- Aktywnie przenosi obciążenia produkcyjne z chronionymi danymi na platformę Azure. Niektóre obciążenia o niskim priorytecie obsługują ruch produkcyjny. Więcej można obciąć natychmiast po zarejestrowaniu się operacji IT na gotowości do obsługi obciążeń.
- Zespoły programistyczne aplikacji są gotowe do ruchu w środowisku produkcyjnym.
- Zespół analizy biznesowej jest gotowy do integrowania prognoz i wglądu w systemy, w których działają operacje dla trzech jednostek biznesowych.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

- Operacje IT są nowe dla operacji w chmurze i muszą szybko zintegrować istniejące procesy operacyjne.
- Zmiany bieżącego i przyszłego stanu ujawniają nowe zagrożenia, które będą wymagały nowych instrukcji zasad.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Zakłócenia biznesowe:** Istnieje ryzyko związane z każdą nową platformą powodującą zakłócenia procesów biznesowych o kluczowym znaczeniu. Zespół operacyjny IT i zespoły wykonujące różne wydłużać w chmurze są stosunkowo niezawodnie związane z operacjami w chmurze. Zwiększa to ryzyko przerwania działania i należy je skorygować i zarządzać nimi.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

1. Niewyrównane procesy operacyjne mogą prowadzić do przestoju, którego nie można wykryć ani szybko wyeliminować.
2. Zewnętrzna wtargnięcie lub ataki typu "odmowa usługi" mogą spowodować przerwanie działania biznesowego.
3. Zasoby o kluczowym znaczeniu mogą nie zostać prawidłowo odnalezione i dlatego nie działają prawidłowo.
4. Niewykrywalne lub nieoznaczone elementy zawartości mogą nie być obsługiwane przez istniejące procesy zarządzania operacyjnego.
5. Konfiguracja wdrożonych zasobów może nie spełniać oczekiwań wydajności.
6. Rejestrowanie może nie być poprawnie rejestrowane i scentralizowane, aby można było rozwiązywać problemy z wydajnością.
7. Zasady odzyskiwania mogą zakończyć się niepowodzeniem lub dłużej niż oczekiwano.
8. Niespójne procesy wdrażania mogą powodować luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
9. Nałożenia konfiguracyjne lub pominięte poprawki mogą spowodować niezamierzone luki w zabezpieczeniach, które mogą prowadzić do przecieków danych lub przerw w działaniu.
10. Konfiguracja może nie wymusić wymagań zdefiniowanych umowy SLA lub zatwierdzono wymagania dotyczące odzyskiwania.
11. Wdrożone systemy operacyjne lub aplikacje mogą nie spełniać wymagań związanych z funkcjonalnością systemu operacyjnego i aplikacji.
12. Istnieje ryzyko niespójności wynikające z wielu zespołów pracujących w chmurze.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika. Na liście jest wyświetlana wartość Long, ale wdrażanie tych zasad może być prostsze.

1. Wszystkie wdrożone zasoby muszą być pogrupowane według stopnia ważności i klasyfikacji danych. Klasyfikacje muszą być przeglądane przez zespół ładu chmury i właściciela aplikacji przed wdrożeniem w chmurze.
2. Podsieci zawierające aplikacje o znaczeniu krytycznym muszą być chronione przez rozwiązanie zapory, które może wykrywać wtargnięcie i odpowiadać na ataki.
3. Narzędzia ładu muszą kontrolować i wymuszać wymagania dotyczące konfiguracji sieci zdefiniowane przez zespół linii bazowej zabezpieczeń.
4. Narzędzia ładu muszą sprawdzić, czy wszystkie zasoby dotyczące aplikacji o znaczeniu krytycznym lub chronionych danych są uwzględniane w monitorowaniu w celu wyczerpania zasobów i optymalizacji.
5. Narzędzia ładu muszą sprawdzić, czy odpowiedni poziom danych rejestrowania jest zbierany dla wszystkich aplikacji o kluczowym znaczeniu lub chronionych danych.
6. Proces ładu musi sprawdzać poprawność wdrożenia kopii zapasowej, odzyskiwania i umowy SLA dla aplikacji o kluczowym znaczeniu i chronionych danych.
7. Narzędzia ładu muszą ograniczać wdrożenie maszyny wirtualnej tylko do zatwierdzonych obrazów.
8. Narzędzia ładu muszą wymusić, że aktualizacje automatyczne są **blokowane** we wszystkich wdrożonych zasobach, które obsługują aplikacje o znaczeniu strategicznym. Naruszenia muszą zostać sprawdzone za pomocą zespołów zarządzania operacyjnego i korygowane zgodnie z zasadami operacji. Zasoby, które nie są automatycznie aktualizowane, muszą być zawarte w procesach należących do operacji IT, aby szybko i efektywnie aktualizować te serwery.
9. Narzędzia ładu muszą sprawdzać poprawność tagowania związanego z kosztami, krytycznością, umową SLA, aplikacją i klasyfikacją danych. Wszystkie wartości muszą być wyrównane do wstępnie zdefiniowanych wartości zarządzanych przez zespół zarządzający chmurą.
10. Procesy nadzoru muszą obejmować inspekcje w punkcie wdrożenia oraz regularne cykle w celu zapewnienia spójności wszystkich zasobów.
11. Trendy i luki w zabezpieczeniach, które mogą mieć wpływ na wdrożenia w chmurze, powinny być regularnie weryfikowane przez zespół ds. zabezpieczeń, aby zapewnić aktualizacje narzędzi linii bazowej zabezpieczeń używanej w chmurze.
12. Przed wprowadzeniem do środowiska produkcyjnego należy dodać wszystkie aplikacje o kluczowym znaczeniu oraz chronione dane do wyprodukowanego rozwiązania do monitorowania operacyjnego. Nie można wyszukać elementów zawartości, które nie mogą zostać odnalezione przez wybrane narzędzia do wykonywania operacji IT do użycia w środowisku produkcyjnym. Wszelkie zmiany wymagane do odnajdywania zasobów muszą zostać wprowadzone do odpowiednich procesów wdrażania, aby zapewnić, że zasoby będą wykrywalne w przyszłych wdrożeniach.
13. Po ich odnalezieniu można sprawdzić poprawność wielkości zasobów przez zespoły zarządzania operacyjnego, aby sprawdzić, czy zasób spełnia wymagania dotyczące wydajności.
14. Narzędzia do wdrażania muszą zostać zatwierdzone przez zespół ds. zarządzania chmurą, aby zapewnić ciągły nadzór nad wdrożonymi zasobami.
15. Skrypty wdrażania muszą być utrzymywane w centralnym repozytorium dostępnym dla zespołu ładu chmury w celu okresowego przeglądania i inspekcji.
16. Procesy nadzoru ładu muszą sprawdzać, czy wdrożone zasoby są prawidłowo skonfigurowane, zgodnie z wymaganiami umowy SLA i odzyskiwania.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

Ta część artykułu poprawi projekt ładu MVP, aby uwzględnić nowe zasady platformy Azure i implementację Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

W przypadku korzystania z tego fikcyjnego przykładu zakłada się, że zmiany chronionych danych zostały już wykonane. W ramach tego najlepszego rozwiązania zostaną dodane wymagania dotyczące monitorowania operacyjnego, które będą przygotowywać subskrypcję aplikacji o kluczowym znaczeniu.

**Firmowa subskrypcja IT:** Dodaj następujące elementy do firmowej subskrypcji IT, która działa jako centrum.

1. Jako zależność zewnętrzna zespół operacyjny w chmurze będzie musiał definiować narzędzia do monitorowania operacyjnego, ciągłość działania i odzyskiwanie po awarii (BCDR) oraz automatyczne narzędzia do korygowania. Zespół ds. zarządzania chmurą może następnie obsługiwać niezbędne procesy odnajdywania.
    1. W tym przypadku użycia zespół operacyjny w chmurze wybiera Azure Monitor jako podstawowe narzędzie do monitorowania aplikacji o krytycznym znaczeniu.
    2. Zespół wybiera również Azure Site Recovery jako podstawowe narzędzia BCDR.
2. Implementacja Azure Site Recovery.
    1. Zdefiniuj i Wdróż Magazyn Azure Site Recovery na potrzeby procesów tworzenia kopii zapasowych i odzyskiwania.
    2. Utwórz szablon zarządzania zasobami platformy Azure na potrzeby tworzenia magazynu w ramach każdej subskrypcji.
3. Implementacja Azure Monitor.
    1. Po zidentyfikowaniu subskrypcji o krytycznym znaczeniu można utworzyć obszar roboczy usługi log Analytics.

**Subskrypcja wdrożenia poszczególnych chmur:** Poniżej zapewnią możliwość odnajdywania każdej subskrypcji przez rozwiązanie do monitorowania i gotowe do uwzględnienia w praktykach BCDR.

1. Azure Policy dla węzłów o kluczowym znaczeniu:
    1. Inspekcja i wymuszanie korzystania tylko z ról standardowych.
    2. Inspekcja i wymuszanie stosowania szyfrowania dla wszystkich kont magazynu.
    3. Inspekcja i wymuszanie użycia zatwierdzonej podsieci sieciowej i sieci wirtualnej dla każdego interfejsu sieciowego.
    4. Inspekcja i wymuszanie ograniczenia zdefiniowanych przez użytkownika tabel routingu.
    5. Inspekcja i egzekwowanie wdrożenia agentów Log Analytics dla maszyn wirtualnych z systemami Windows i Linux.
2. Plan platformy Azure:
    1. Utwórz plan o nazwie `mission-critical-workloads-and-protected-data`. Ten plan zastosuje zasoby oprócz planu chronionego danych.
    2. Dodaj nowe zasady platformy Azure do planu.
    3. Zastosuj plan do każdej subskrypcji, która będzie hostować aplikację o znaczeniu krytycznym.

## <a name="conclusion"></a>Podsumowanie

Dodanie tych procesów i zmian do ładu programu MVP pomaga skorygować wiele zagrożeń związanych z zarządzaniem zasobami. Razem dodają kontrolę odzyskiwania, rozmiarów i monitorowania, które są niezbędne do upoważnienia operacji obsługujących chmurę.

## <a name="next-steps"></a>Następne kroki

Gdy wdrożenie chmury zostanie powiększone i oferuje dodatkową wartość biznesową, również zostaną zmienione wymagania dotyczące ryzyka i zarządzania chmurą. W przypadku fikcyjnej firmy w tym przewodniku następnym wyzwalaczem jest, gdy skala wdrożenia przekroczy 1 000 zasobów do chmury, lub miesięczne wydatki przekraczają $10 000 USD miesięcznie. W tym momencie zespół nadzorujący chmury dodaje Cost Management kontrolek.

> [!div class="nextstepaction"]
> [Ulepszanie dyscypliny Cost Management](./cost-management-improvement.md)
