---
title: Testy porównawcze i zmiana rozmiaru zasobów w chmurze
description: Testy porównawcze i zmiana rozmiaru zasobów w chmurze
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7198bdc1332a9d55bca68a04fe1384727dc7284a
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76801838"
---
# <a name="benchmark-and-resize-cloud-assets"></a>Testy porównawcze i zmiana rozmiaru zasobów w chmurze

Monitorowanie użycia i wydatków ma kluczowe znaczenie dla infrastruktur chmurowych. Organizacje płacą za zasoby wykorzystywane w czasie. Gdy użycie przekracza progi określone w umowie, nieoczekiwane koszty za użycie nadwyżkowe mogą szybko narastać. Raporty usługi Cost Management ułatwiają monitorowanie wydatków w celu analizowania i śledzenia użycia chmury, kosztów i trendów. Używając raportów czasu dodatkowego, możesz wykrywać anomalie różniące się od normalnych trendów. Nieefektywności we wdrożeniu w chmurze są widoczne w raportach optymalizacji. Zwróć uwagę na nieefektywności w raportach analizy kosztów.

W tradycyjnych lokalnych modelach infrastruktury IT zgłaszanie zapotrzebowania na systemy IT jest kosztowne i czasochłonne. Procesy często wymagają długich cykli przeglądu wydatków inwestycyjnych i mogą wymagać nawet rocznego procesu planowania. W związku z tym typową praktyką jest kupowanie więcej niż potrzeba. Równie powszechną praktyką wśród administratorów IT jest nadmierne aprowizowanie zasobów w ramach przygotowania na przewidywane przyszłe zapotrzebowanie.

W chmurze modele ewidencjonowania i aprowizacji eliminują opóźnienia, które prowadzą do nadmiernych zakupów. Gdy zasób wymaga dodatkowych zasobów, można go skalować w górę lub w dół niemal natychmiast. Oznacza to, że rozmiar zasobów można bezpiecznie zmniejszyć, aby zminimalizować ilość wykorzystanych zasobów oraz ponoszone koszty. Podczas testów porównawczych i optymalizacji zespół wdrożeniowy ds. chmury stara się znaleźć równowagę między wydajnością a kosztami, aprowizując zasoby tak, aby były nie większe i nie mniejsze niż to konieczne do spełnienia wymagań produkcyjnych.

<!-- markdownlint-disable MD026 -->

## <a name="should-assets-be-optimized-during-or-after-the-migration"></a>Czy zasoby powinny być optymalizowane podczas migracji czy po niej?

Kiedy zasób powinien być optymalizowany &mdash; podczas czy po migracji? Prosta odpowiedź brzmi: *podczas i po*. Nie jest to jednak całkowicie dokładna odpowiedź. Aby to wyjaśnić, zapoznaj się z dwoma podstawowymi scenariuszami optymalizacji rozmiaru zasobów:

- **Planowana zmiana rozmiaru.** Często zasób jest ewidentnie zbyt duży i nie w pełni wykorzystywany, w związku z czym należy zmienić jego rozmiar podczas wdrażania. W tym przypadku określenie, czy rozmiar zasobu został pomyślnie zmieniony, wymaga testowania akceptacyjnego przez użytkowników po migracji. Jeśli użytkownik zaawansowany nie doświadcza żadnych strat wydajności i funkcjonalności podczas testowania, można wnioskować, że rozmiar tego zasobu został ustalony pomyślnie.
- **Optymalizacja.** W przypadkach, gdy potrzeba optymalizacji jest niejasna, zespoły IT powinny używać podejścia opartego na danych do zarządzania rozmiarem zasobów. Korzystając z wzorców wydajności zasobów, zespół IT może podejmować decyzje o najbardziej odpowiednim rozmiarze, usługach, skali i architekturze rozwiązania. Następnie może zmienić rozmiar i przetestować teorie wydajności po migracji.

Podczas migracji można używać popartych wiedzą i doświadczeniem przypuszczeń i eksperymentować z rozmiarem. Jednak prawdziwa optymalizacja zasobów wymaga danych opartych na rzeczywistej wydajności w środowisku chmury. W celu zapewnienia prawdziwej optymalizacji zespół IT musi najpierw zaimplementować metody monitorowania wydajności i wykorzystania zasobów.

## <a name="benchmark-and-optimize-with-azure-cost-management"></a>Testy porównawcze i optymalizacja przy użyciu usługi Azure Cost Management

Usługa [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview) licencjonowana przez firmę Cloudyn, podmiot zależny firmy Microsoft, zapewnia przejrzyste i dokładne zarządzanie wydatkami na chmurę. Ta usługa monitoruje, przeprowadza testy porównawcze, przydziela i optymalizuje koszty chmury.

Dane historyczne mogą pomóc w zarządzaniu kosztami przez analizowanie użycia i kosztów w czasie w celu zidentyfikowania trendów, które następnie są używane do prognozowania przyszłych wydatków. Usługa Cost Management zawiera także przydatne raporty kosztów planowanych. Alokacja kosztów zarządza kosztami, analizując koszty na podstawie zasad tagowania. Alokacji kosztów można użyć na potrzeby przewidywanych kosztów i obciążeń zwrotnych, aby uwidocznić wykorzystanie zasobów i związane z tym koszty oraz wpływać na zachowania zużycia lub obciążać klientów dzierżawy. Kontrola dostępu ułatwia zarządzanie kosztami, zapewniając, że użytkownicy i zespoły mają dostęp tylko do potrzebnych im danych usługi Cost Management. Generowanie alertów ułatwia zarządzanie kosztami, automatycznie generując powiadomienia, gdy występują nietypowe lub nadmiarowe wydatki. Alerty mogą także automatycznie powiadamiać innych uczestników projektu o anomaliach wydatków i ryzykach związanych z nadmiarowymi wydatkami. Różne raporty obsługują alerty oparte na budżecie i progach kosztów.

## <a name="improve-efficiency"></a>Poprawa wydajności

Za pomocą usługi Cost Management możesz określić optymalne użycie maszyn wirtualnych, zidentyfikować bezczynne maszyny wirtualne lub usunąć bezczynne maszyny wirtualne oraz niedołączone dyski. Korzystając z informacji zawartych w raportach optymalizacji rozmiaru i raportach nieefektywności, sporządź plan zmniejszenia rozmiaru lub usunięcia bezczynnych maszyn wirtualnych.

## <a name="next-steps"></a>Następne kroki

Po przetestowaniu i zoptymalizowaniu obciążenia jest czas na [przygotowanie obciążenia do podwyższenia jego poziomu](./ready.md).

> [!div class="nextstepaction"]
> [Przygotowywanie zmigrowanego obciążenia do podwyższenia poziomu do produkcyjnego](./ready.md)
