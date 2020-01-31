---
title: Udoskonalenie dyscypliny spójności zasobów
description: Udoskonalenie dyscypliny spójności zasobów
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0113c37aaca23374021d6790bcbb1db751ffcf4a
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807244"
---
# <a name="resource-consistency-discipline-improvement"></a>Udoskonalenie dyscypliny spójności zasobów

Dyscyplina spójności zasobów koncentruje się na sposobach ustanawiania zasad związanych z zarządzaniem środowiskiem, aplikacją lub obciążeniem. W ramach pięciu dyscyplin nadzoru w chmurze spójność zasobów obejmuje monitorowanie wydajności aplikacji, obciążeń i zasobów. Zawiera również zadania wymagane do spełnienia wymagań dotyczących skalowania, skorygowania naruszeń wydajności Umowa dotycząca poziomu usług (SLA) i aktywnego uniknięcia naruszeń umowy SLA poprzez automatyczne korygowanie.

W tym artykule przedstawiono niektóre potencjalne zadania, w których firma może uczestniczyć w ulepszaniu dyscypliny spójności zasobów. Te zadania mogą być podzielone na planowanie, kompilowanie, przyjmowanie i eksploatację etapów wdrażania rozwiązania w chmurze, które są następnie powtarzane na umożliwieniu rozwoju [przyrostowego podejścia do zarządzania chmurą](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cztery etapy wdrażania](../../_images/govern/adoption-phases.png)

*Rysunek 1. etapy wdrażania przyrostowego podejścia do ładu w chmurze.*

Nie jest możliwe, aby żaden z dokumentów mógł uwzględnić wymagania wszystkich firm. W tym artykule opisano sugerowane minimalne i potencjalne przykładowe działania dla każdej fazy procesu ładu. Początkowym celem tych działań jest ułatwienie tworzenia programu MVP dla [zasad](../guides/index.md#an-incremental-approach-to-cloud-governance) i ustanowienie platformy do ulepszania zasad. Zespół ds. zarządzania chmurą będzie musiał zdecydować, jak dużo inwestować w te działania, aby zwiększyć możliwości zarządzania spójnością zasobów.

> [!CAUTION]
> Nie są one wyrównane do określonych zasad firmy lub wymagań dotyczących zgodności innych firm. Te wskazówki mają na celu ułatwienie obsługi konwersacji, które będą prowadzić do wyrównania obu wymagań przy użyciu modelu ładu chmurowego.

## <a name="planning-and-readiness"></a>Planowanie i gotowość

W tej fazie działania ładu mostkuje podział między wynikami biznesowymi i strategiami, które mogą być funkcjonalne. W trakcie tego procesu zespół lidera definiuje określone metryki, mapuje te metryki na cyfrę elektroniczną i rozpoczyna planowanie ogólnego wysiłku migracji.

**Minimalna sugerowane działania:**

- Oceń opcje [łańcucha narzędzi spójności zasobów](./toolchain.md) .
- Zapoznaj się z wymaganiami dotyczącymi licencjonowania dla strategii chmury.
- Opracowywanie dokumentów z instrukcjami dotyczącymi architektury i dystrybucji do kluczowych uczestników projektu.
- Zapoznaj się z usługą Resource Manager, za pomocą której można wdrażać i monitorować wszystkie zasoby rozwiązania oraz zarządzać nimi jako grupą.
- Zaangażuj i powiąż osoby i zespoły, których dotyczy rozwój wytycznych dotyczących architektury.
- Dodaj priorytetowe zadania wdrażania zasobów do zaległości migracji.

**Potencjalne działania:**

- Współpracuj z zainteresowanymi stronami biznesowymi i zespołem ds. strategii chmurowej, aby zrozumieć odpowiednie podejście do księgowania w chmurze i rozwiązania do księgowania kosztów w ramach jednostek i organizacji jako całości.
- Zdefiniuj wymagania dotyczące [monitorowania i wymuszania zasad](./compliance-processes.md) .
- Zapoznaj się z wartością biznesową i kosztem przestoju, aby zdefiniować zasady korygowania i wymagania SLA.
- Należy określić, czy wdrażane jest [proste obciążenie](./governance-simple-workload.md) , czy wiele strategii ładu [zespołu](./governance-multiple-teams.md) dla zasobów.
- Określ wymagania dotyczące skalowalności planowanych obciążeń.

## <a name="build-and-predeployment"></a>Kompilacja i prewdrażanie

Do pomyślnej migracji środowiska wymagane są pewne wymagania techniczne i nietechniczne. Ten proces koncentruje się na decyzjach, gotowości i infrastrukturze podstawowej, która przejdzie do migracji.

**Minimalna sugerowane działania:**

- Zaimplementuj [łańcucha narzędzi spójności zasobów](./toolchain.md) , przechodząc do etapu preinstalacji.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury i dystrybucja do kluczowych uczestników projektu.
- Implementuj zadania wdrażania zasobów w zaległej migracji z priorytetami.
- Opracowywanie materiałów edukacyjnych i dokumentacji, świadomości, zachęt i innych programów w celu ułatwienia wdrażania użytkowników.

**Potencjalne działania:**

- Wybierz [strategię projektu subskrypcji](../../decision-guides/subscriptions/index.md), wybierając wzorce subskrypcji, które najlepiej pasują do potrzeb organizacji i obciążenia.
- Użyj strategii [spójności zasobów](../../decision-guides/resource-consistency/index.md) , aby wymusić wymuszanie wytycznych dotyczących architektury w czasie.
- Implementowanie [nazewnictwa zasobów i określanie wzorców](../../decision-guides/resource-tagging/index.md) dla zasobów w celu dopasowania do wymagań organizacyjnych i księgowych.
- Aby utworzyć proaktywne zarządzanie punktem w czasie, użyj szablonów wdrażania i automatyzacji, aby wymusić wspólne konfiguracje i spójną strukturę grupowania podczas wdrażania zasobów i grup zasobów.
- Ustanów model uprawnień najniższych przywilejów, w którym użytkownicy domyślnie nie mają uprawnień.
- Określ, kto w organizacji jest właścicielem poszczególnych obciążeń i kont oraz kto musi mieć dostęp do tych zasobów lub ich modyfikować. Zdefiniuj role w chmurze i obowiązki zgodne z tymi potrzebami i Użyj tych ról jako podstawy kontroli dostępu.
- Zdefiniuj zależności między zasobami.
- Zaimplementuj automatyczne skalowanie zasobów, aby dopasować wymagania zdefiniowane w etapie planu.
- Przeprowadzenie wydajności dostępu w celu mierzenia jakości odebranych usług.
- Rozważ wdrożenie [zasad](https://docs.microsoft.com/azure/governance/policy/overview) w celu zarządzania wymuszeniem umowy SLA przy użyciu ustawień konfiguracji i reguł tworzenia zasobów.

## <a name="adopt-and-migrate"></a>Zastosuj i Migruj

Migracja to proces przyrostowy, który koncentruje się na przeniesieniu, testowaniu i wdrażaniu aplikacji lub obciążeń w istniejącym obszarze cyfrowym.

**Minimalna sugerowane działania:**

- Migruj [łańcucha narzędzi spójności zasobów](./toolchain.md) ze wstępnego wdrożenia do środowiska produkcyjnego.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury i dystrybucja do kluczowych uczestników projektu.
- Opracowywanie materiałów edukacyjnych i dokumentacji, świadomości, zachęt i innych programów w celu ułatwienia wdrażania użytkowników.
- Przeprowadź migrację wszelkich istniejących automatycznych skryptów korygujących lub narzędzi do obsługi określonych wymagań umowy SLA.

**Potencjalne działania:**

- Ukończ i przetestuj monitorowanie oraz dane raportowania przy użyciu wybranej platformy lokalnego, bramy w chmurze lub rozwiązania hybrydowego.
- Ustal, czy należy wprowadzić zmiany w umowie SLA lub zasadach zarządzania dla zasobów.
- Ulepszanie zadań operacji przez implementację funkcji zapytań w celu efektywnego znajdowania zasobów w całej chmurze.
- Dopasuj zasoby, aby zmienić potrzeby biznesowe i wymagania dotyczące zarządzania.
- Upewnij się, że maszyny wirtualne, sieci wirtualne i konta magazynu odzwierciedlają rzeczywiste potrzeby dostępu do zasobów podczas każdej wersji, a następnie dostosuj je w razie potrzeby.
- Sprawdź, czy automatyczne skalowanie zasobów spełnia wymagania dotyczące dostępu.
- Przejrzyj dostęp użytkowników do zasobów, grup zasobów i subskrypcji platformy Azure, a następnie dostosuj kontrolę dostępu w razie potrzeby.
- Monitoruj zmiany w planach dostępu do zasobów i Weryfikuj ich w przypadku konieczności uzyskania dodatkowych uprawnień.
- Zaktualizuj zmiany w dokumencie wytyczne dotyczące architektury w celu odzwierciedlenia rzeczywistych kosztów.
- Ustal, czy Twoja organizacja wymaga jasnego wyrównania finansowego do & LS dla jednostek roboczych.
- W przypadku organizacji globalnych należy zaimplementować wymagania dotyczące zgodności z umową SLA lub suwerenności.
- W przypadku agregacji w chmurze Wdróż rozwiązanie bramy dla dostawcy chmury.
- W przypadku narzędzi, które nie zezwalają na opcje hybrydowe lub bramy ścisłie integrują monitorowanie za pomocą narzędzia do monitorowania operacyjnego obejmującego wszystkie centra danych i chmurę.

## <a name="operate-and-post-implementation"></a>Działanie i po wdrożeniu

Po zakończeniu transformacji zarządzanie i działania muszą być aktywne w przypadku naturalnego cyklu życia aplikacji lub obciążenia. Ta faza zarządzania terminem spłaty koncentruje się na działaniach, które często są stosowane po wdrożeniu rozwiązania, a cykl transformacji zaczyna się ustabilizować.

**Minimalna sugerowane działania:**

- Dostosuj [łańcucha narzędzi spójności zasobów](./toolchain.md) na podstawie aktualizacji potrzebnych Cost Management organizacji.
- Rozważ automatyzację wszelkich powiadomień i raportów, aby odzwierciedlić rzeczywiste użycie zasobów.
- Udoskonalenie wytycznych dotyczących architektury w celu zaplanowania przyszłych procesów wdrażania.
- Okresowe informowanie zespołów, których to dotyczy, w celu zapewnienia stałego przestrzegania wytycznych dotyczących architektury.

**Potencjalne działania:**

- Dostosuj plany kwartalnie, aby odzwierciedlały zmiany rzeczywistych zasobów.
- Automatyczne stosowanie i wymuszanie wymagań ładu w przyszłych wdrożeniach.
- Oceń nieużywane zasoby i ustal, czy są one kontynuowane.
- Wykrywanie nieprawidłowych wyrównań i anomalii między planowanym i rzeczywistym użyciem zasobów.
- Pomóż zespołom wdrażania chmury i zespołowi strategii chmury w zrozumieniu i rozwiązywaniu tych anomalii.
- Ustal, czy należy wprowadzić zmiany spójności zasobów dla rozliczeń i umowy SLA.
- Oceń narzędzia do rejestrowania i monitorowania, aby określić, czy rozwiązanie lokalne, bramy w chmurze lub rozwiązania hybrydowe wymagają dostosowania.
- W przypadku jednostek biznesowych i grup rozproszonych geograficznie należy określić, czy organizacja powinna rozważyć użycie dodatkowych funkcji zarządzania chmurą, takich jak [grupy zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups) , w celu lepszego zastosowania scentralizowanych zasad i spełnienia wymagań umowy SLA.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz koncepcję zarządzania zasobami w chmurze, przejdź do, aby dowiedzieć się więcej na temat [sposobu zarządzania dostępem do zasobów](./resource-access-management.md) na platformie Azure w celu uczenia się, jak projektować model ładu dla [prostego obciążenia](./governance-simple-workload.md) lub dla [wielu zespołów](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> Informacje [na temat zarządzania dostępem do zasobów na platformie azure](./resource-access-management.md)
> informacje [o umowach dotyczących poziomu usług dla platformy Azure](https://azure.microsoft.com/support/legal/sla)
> informacje [o rejestrowaniu, raportowaniu i monitorowaniu](../../decision-guides/logging-and-reporting/index.md)
