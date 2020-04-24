---
title: 'Standardowe zarządzanie przedsiębiorstwami: ulepszanie dyscypliny linii bazowej zabezpieczeń'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak dodać kontrolki zabezpieczeń obsługujące przeniesienie chronionych danych do chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9078c8e01a7b711a18ecf83a1243da3813fc5afd
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80431047"
---
# <a name="standard-enterprise-governance-guide-improve-the-security-baseline-discipline"></a>Standardowy Przewodnik dotyczący zarządzania przedsiębiorstwem: ulepszanie dyscypliny linii bazowej zabezpieczeń

W tym artykule zawarto opisy, dodając formanty zabezpieczeń, które obsługują przeniesienie chronionych danych do chmury.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Liderzy firmy byli zadowolony z wyników eksperymentów wczesnych na etapie opracowywania aplikacji przez ten program, a na przykład aplikacje i zespoły analizy biznesowej. Aby zrealizować materialne wartości biznesowe z tych eksperymentów, te zespoły muszą mieć możliwość integrowania chronionych danych z rozwiązaniami. Powoduje to zaimplementowanie zmian w zasadach firmowych, ale wymaga również zwiększenia przyrostu implementacji zarządzania chmurą, zanim chronione dane będą mogły być gruntami w chmurze.

### <a name="changes-to-the-cloud-governance-team"></a>Zmiany w zespole ładu w chmurze

Mając na względzie wpływ zmieniających się opisów i pomocy technicznej, zespół ds. zarządzania chmurą jest teraz przeglądany inaczej. Dwóch administratorów systemu, którzy uruchomili zespół, są teraz oglądani jako doświadczeni architektów w chmurze. W miarę rozwoju tej narracji ich postrzeganie przesunie się od powierników chmury do większej roli ochrony chmury.

Różnica jest delikatna, dlatego jest ważnym rozróżnieniem podczas kompilowania kultury IT ukierunkowanej na zarządzanie. Powiernik w chmurze czyści messesy opracowane przez innowacyjne architektów w chmurze. Dwie role mają naturalne tarcie i przeciwieństwo do siebie celów. Z drugiej strony opiekun w chmurze pomaga zapewnić bezpieczeństwo chmury, dzięki czemu inne architektzy chmury mogą szybko przełączać się do mniej Messes. Ponadto opiekun chmury obejmuje tworzenie szablonów, które przyspieszają wdrażanie i przyjmowanie, dzięki czemu akcelerator innowacyjny, a także usługa Defender z pięciu dyscyplin nadzoru chmurowego.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

Na początku tego rozwinięcia zespoły deweloperów aplikacji nadal pracowały w wydajności tworzenia i testowania, a zespół analizy biznesowej był nadal w fazie eksperymentalnej. Obsługiwane są dwa środowiska infrastruktury hostowanej o nazwie prod i DR.

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- Zespół programistyczny aplikacji wdrożył potok ciągłej integracji/ciągłego wdrażania, aby wdrożyć aplikację natywną w chmurze przy użyciu ulepszonego środowiska użytkownika. Ta aplikacja nie współdziała jeszcze z chronionymi danymi, więc nie jest gotowa do produkcji.
- Zespół ds. analizy biznesowej aktywnie nadzoruje dane w chmurze z poziomu logistyki, spisu i źródeł innych firm. Te dane są używane do kierowania nowych prognoz, które mogą kształtować procesy biznesowe. Jednak te przewidywania i szczegółowe informacje nie są funkcjonalne, dopóki dane klienta i finansowe nie będą mogły zostać zintegrowane z platformą danych.
- Zespół IT postępuje zgodnie z planami CIO i DYREKTORów, aby wycofać centrum danych DR. Ponad 1 000 zasobów 2 000 w centrum danych odzyskiwania po awarii zostało wycofane lub zmigrowane.
- Ustalone przez siebie zasady dotyczące danych osobowych i danych finansowych zostały zmodernizowane. Jednak nowe zasady firmowe są zależne od implementacji związanych z nimi zasad zabezpieczeń i zarządzania. Zespoły nadal są wstrzymane.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Wczesne eksperymenty przez zespoły deweloperów aplikacji i analizy biznesowej pokazują potencjalne udoskonalenia dotyczące doświadczeń klientów i decyzji opartych na danych. Oba zespoły chcą rozszerzyć przyjęcie chmury w ciągu następnych 18 miesięcy przez wdrożenie tych rozwiązań w środowisku produkcyjnym.

W pozostałych sześciu miesiącach zespół ds. zarządzania chmurą będzie wdrażał wymagania dotyczące zabezpieczeń i zarządzania, aby umożliwić zespołom wdrażania chmury Migrowanie chronionych danych w tych centrach.

Zmiany bieżącego i przyszłego stanu ujawniają nowe zagrożenia, które wymagają nowych instrukcji zasad.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Naruszenie danych:** W przypadku przyjęcia nowej platformy danych istnieje wzrost zobowiązań związanych z potencjalnymi naruszeniami danych. Technicy stosujące technologie chmury wzrosły do wdrożenia rozwiązań, które mogą obniżyć to ryzyko. Należy wdrożyć niezawodną strategię zabezpieczeń i nadzoru, aby upewnić się, że technicy te spełniają te obowiązki.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

1. Aplikacje o krytycznym znaczeniu lub chronione dane mogą zostać przypadkowo wdrożone.
2. Chronione dane mogą zostać ujawnione podczas przechowywania ze względu na słabe decyzje dotyczące szyfrowania.
3. Nieautoryzowani użytkownicy mogą uzyskać dostęp do chronionych danych.
4. Zewnętrzna wtargnięcie może spowodować uzyskanie dostępu do chronionych danych.
5. Zewnętrzna wtargnięcie lub ataki typu "odmowa usługi" mogą spowodować przerwanie działania biznesowego.
6. Zmiany organizacji lub zatrudnienia mogą pozwolić na nieautoryzowany dostęp do chronionych danych.
7. Nowe programy wykorzystujące luki w zabezpieczeniach mogą tworzyć nowe możliwości włamania lub dostępu.
8. Niespójne procesy wdrażania mogą spowodować luki w zabezpieczeniach, co może prowadzić do przecieków danych lub przerw w działaniu.
9. W przypadku nieoczekiwanych luk w zabezpieczeniach nastąpi przeznaczenie konfiguracyjne lub nieodebrane poprawki, co może prowadzić do przecieków danych lub przerw w działaniu.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika. Lista będzie wyglądać długa, ale stosowanie tych zasad może być łatwiejsze niż wyświetlona.

1. Wszystkie wdrożone zasoby muszą być pogrupowane według stopnia ważności i klasyfikacji danych. Klasyfikacje muszą być przeglądane przez zespół ładu chmury i właściciela aplikacji przed wdrożeniem w chmurze.
2. Aplikacje, które przechowują lub uzyskują dostęp do chronionych danych, są zarządzane inaczej niż te, które nie są. Należy je podzielić na mniejsze, aby uniknąć niezamierzonego dostępu do chronionych danych.
3. Wszystkie chronione dane muszą być szyfrowane, gdy są przechowywane. Chociaż jest to wartość domyślna dla wszystkich kont usługi Azure Storage, może być konieczna dodatkowa strategia szyfrowania, w tym szyfrowanie danych w ramach konta magazynu, szyfrowanie maszyn wirtualnych i szyfrowanie na poziomie bazy danych podczas korzystania z języka SQL na maszynie wirtualnej (TDE i szyfrowanie kolumn).
4. Uprawnienia podwyższonego poziomu w dowolnym segmencie zawierającym chronione dane powinny być wyjątkiem. Wszelkie takie wyjątki będą rejestrowane w zespole ładu chmur i regularnie poddawane inspekcji.
5. Podsieci sieciowe zawierające chronione dane muszą być odizolowane od innych podsieci. Ruch sieciowy między podsieciami chronionych danych zostanie regularnie poddany inspekcji.
6. Nie można bezpośrednio uzyskać dostępu do podsieci zawierającej chronione dane za pośrednictwem publicznego Internetu lub między centrami danych. Dostęp do tych podsieci musi być kierowany za pośrednictwem podsieci pośrednich. Każdy dostęp do tych podsieci musi następować przez rozwiązanie zapory, które może wykonywać funkcje skanowania pakietów i blokowania.
7. Narzędzia ładu muszą przeprowadzać inspekcję i wymuszać wymagania dotyczące konfiguracji sieci zdefiniowane przez zespół zarządzania zabezpieczeniami.
8. Narzędzia ładu muszą ograniczać wdrożenie maszyny wirtualnej tylko do zatwierdzonych obrazów.
9. Zawsze, gdy jest to możliwe, zarządzanie konfiguracją węzła powinna stosować wymagania dotyczące zasad do konfiguracji dowolnego systemu operacyjnego gościa.
10. Narzędzia ładu muszą wymusić włączenie aktualizacji automatycznych dla wszystkich wdrożonych zasobów. Naruszenia muszą zostać sprawdzone za pomocą zespołów zarządzania operacyjnego i korygowane zgodnie z zasadami operacji. Zasoby, które nie są automatycznie aktualizowane, muszą być uwzględnione w procesach należących do operacji IT.
11. Tworzenie nowych subskrypcji lub grup zarządzania dla wszystkich aplikacji o znaczeniu krytycznym lub chronionych danych będzie wymagało przeglądu od zespołu zarządzającego chmurą, aby upewnić się, że jest przypisany odpowiedni plan.
12. Model dostępu o najniższych uprawnieniach zostanie zastosowany do każdej grupy zarządzania lub subskrypcji zawierającej aplikacje o kluczowym znaczeniu lub chronione dane.
13. Trendy i luki w zabezpieczeniach, które mogą mieć wpływ na wdrożenia w chmurze, powinny być regularnie przeglądane przez zespół ds. zabezpieczeń, aby zapewnić aktualizacje narzędzi do zarządzania zabezpieczeniami używane w chmurze.
14. Narzędzia do wdrażania muszą zostać zatwierdzone przez zespół ds. zarządzania chmurą, aby zapewnić ciągły nadzór nad wdrożonymi zasobami.
15. Skrypty wdrażania muszą być utrzymywane w centralnym repozytorium dostępnym dla zespołu ładu chmury w celu okresowego przeglądania i inspekcji.
16. Procesy nadzoru muszą obejmować inspekcje w punkcie wdrożenia oraz regularne cykle w celu zapewnienia spójności wszystkich zasobów.
17. Wdrożenie wszelkich aplikacji, które wymagają uwierzytelnienia klienta, musi używać zatwierdzonego dostawcy tożsamości, który jest zgodny z podstawowym dostawcą tożsamości dla użytkowników wewnętrznych.
18. Procesy ładu chmury muszą obejmować kwartalne przeglądy z zespołami zarządzania tożsamościami. Te przeglądy mogą ułatwić identyfikację złośliwych aktorów lub wzorców użytkowania, które powinny być blokowane przez konfigurację zasobów w chmurze.

## <a name="incremental-improvement-of-governance-practices"></a>Przyrostowe ulepszanie praktyk w zakresie zapewniania ładu

Projekt ładu MVP zmieni się w taki sposób, aby obejmował nowe zasady platformy Azure i implementację Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

1. Sieci i zespoły ds. zabezpieczeń IT definiują wymagania sieciowe. Zespół ds. zarządzania chmurą będzie obsługiwał konwersację.
2. Tożsamość i zespoły zabezpieczeń IT definiują wymagania dotyczące tożsamości i wprowadzają niezbędne zmiany w lokalnej implementacji Active Directory. Zespół nadzorujący chmury będzie przeglądać zmiany.
3. Utwórz repozytorium w usłudze Azure DevOps, aby przechowywać i wypełniać wszystkie odpowiednie szablony Azure Resource Manager i konfiguracje inicjowane przez skrypty.
4. Implementacja Azure Security Center:
    1. Skonfiguruj Azure Security Center dla każdej grupy zarządzania zawierającej klasyfikacje chronionych danych.
    2. Domyślnie Ustaw automatyczne Inicjowanie obsługi, aby zapewnić zgodność z poprawkami.
    3. Ustanów konfiguracje zabezpieczeń systemu operacyjnego. Zespół ds. zabezpieczeń IT określi konfigurację.
    4. Obsługa zespołu ds. zabezpieczeń IT w początkowym użyciu Security Center. Przechodzenie Security Center do zespołu ds. zabezpieczeń IT, ale utrzymuje dostęp do celów ciągłego ulepszania zarządzania.
    5. Utwórz szablon Menedżer zasobów, który odzwierciedla zmiany wymagane do Security Center konfiguracji w ramach subskrypcji.
5. Aktualizuj zasady platformy Azure dla wszystkich subskrypcji:
    1. Przeprowadzaj inspekcję i Wymuszaj klasyfikację stopnia ważności i danych dla wszystkich grup zarządzania i subskrypcji, aby identyfikować subskrypcje z klasyfikacjami chronionych danych.
    2. Inspekcja i wymuszanie używania tylko zatwierdzonych obrazów.
6. Zaktualizuj zasady platformy Azure dla wszystkich subskrypcji, które zawierają klasyfikacje chronionych danych:
    1. Inspekcja i wymuszanie używania standardowych ról RBAC platformy Azure.
    2. Inspekcja i wymuszanie szyfrowania dla wszystkich kont magazynu i plików przechowywanych w poszczególnych węzłach.
    3. Inspekcja i wymuszanie aplikacji sieciowej grupy zabezpieczeń na wszystkich kartach sieciowych i podsieciach. Sieci i zespoły ds. zabezpieczeń IT definiują sieciowej grupy zabezpieczeń.
    4. Inspekcja i wymuszanie użycia zatwierdzonej podsieci sieciowej i sieci wirtualnej dla każdego interfejsu sieciowego.
    5. Inspekcja i wymuszanie ograniczenia zdefiniowanych przez użytkownika tabel routingu.
    6. Zastosuj wbudowane zasady konfiguracji gościa w następujący sposób:
        1. Inspekcja serwerów sieci Web systemu Windows korzystających z bezpiecznych protokołów komunikacyjnych.
        2. Inspekcja ustawień zabezpieczeń hasła w maszynach z systemem Linux i Windows.
7. Konfiguracja zapory:
    1. Zidentyfikuj konfigurację zapory platformy Azure, która spełnia niezbędne wymagania dotyczące zabezpieczeń. Alternatywnie Zidentyfikuj zgodne urządzenie innej firmy, które jest zgodne z platformą Azure.
    2. Utwórz szablon Menedżer zasobów, aby wdrożyć zaporę z wymaganymi konfiguracjami.
8. Plan platformy Azure:
    1. Utwórz nowy plan o nazwie `protected-data`.
    2. Dodaj zaporę i Azure Security Center szablonów do planu.
    3. Dodaj nowe zasady dla chronionych subskrypcji danych.
    4. Opublikuj plan w każdej grupie zarządzania, która aktualnie planuje hostowanie chronionych danych.
    5. Zastosuj nową strategię do każdej powiązanej subskrypcji, poza istniejącymi planami.

## <a name="conclusion"></a>Podsumowanie

Dodanie powyższych procesów i zmian do ładu MVP pomoże rozwiązać wiele zagrożeń związanych z zarządzaniem zabezpieczeniami. Razem dodają narzędzia do monitorowania sieci, tożsamości i zabezpieczeń, które są konieczne do ochrony danych.

## <a name="next-steps"></a>Następne kroki

Wdrożenie chmury kontynuuje się i zapewnia dodatkową wartość biznesową, ale również wymaga zmiany ryzyka i zarządzania chmurą. W przypadku fikcyjnej firmy w tym przewodniku następnym krokiem jest obsługa obciążeń o kluczowym znaczeniu. Jest to punkt, gdy są zbędne kontrolki spójności zasobów.

> [!div class="nextstepaction"]
> [Poprawianie spójności zasobów](./resource-consistency-improvement.md)
