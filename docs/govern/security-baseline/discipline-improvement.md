---
title: Poprawa dyscypliny linii bazowej zabezpieczeń
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Poprawa dyscypliny linii bazowej zabezpieczeń
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8ad6b84a67bb81459fbd78ebe413a93c1a58e099
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030621"
---
# <a name="security-baseline-discipline-improvement"></a>Poprawa dyscypliny linii bazowej zabezpieczeń

Dyscyplina linii bazowej zabezpieczeń koncentruje się na sposobach ustanawiania zasad chroniących sieć, zasoby i najważniejsze dane, które będą znajdować się w rozwiązaniu dostawcy chmury. W pięciu dyscyplinach zarządzania chmurą linia bazowa zabezpieczeń obejmuje klasyfikację cyfrowej i danych. Zawiera również dokumentację dotyczącą ryzyka, tolerancję biznesową i strategie zaradcze związane z bezpieczeństwem danych, zasobów i sieci. Z perspektywy technicznej obejmuje to również zaangażowanie w decyzje dotyczące [szyfrowania](../../decision-guides/encryption/index.md), [wymagań sieci](../../decision-guides/software-defined-network/index.md), [hybrydowych strategii tożsamości](../../decision-guides/identity/index.md)i [procesów](./compliance-processes.md) używanych do tworzenia zasad linii bazowej zabezpieczeń w chmurze.

W tym artykule przedstawiono niektóre potencjalne zadania, w których firma może uczestniczyć w programie w celu lepszego opracowania i przedwczesnego dyscypliny linii bazowej zabezpieczeń. Te zadania mogą być podzielone na planowanie, kompilowanie, przyjmowanie i eksploatację etapów wdrażania rozwiązania w chmurze, które są następnie powtarzane na umożliwieniu rozwoju [przyrostowego podejścia do zarządzania chmurą](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cztery etapy wdrażania](../../_images/govern/adoption-phases.png)

*Rysunek 1. etapy wdrażania przyrostowego podejścia do ładu w chmurze.*

Nie jest możliwe, aby żaden z dokumentów mógł uwzględnić wymagania wszystkich firm. W tym artykule opisano sugerowane minimalne i potencjalne przykładowe działania dla każdej fazy procesu ładu. Początkowym celem tych działań jest ułatwienie tworzenia programu MVP dla [zasad](../guides/index.md#an-incremental-approach-to-cloud-governance) i ustanowienie platformy do ulepszania zasad. Zespół ds. zarządzania chmurą będzie musiał zdecydować, jak dużo inwestować w te działania, aby zwiększyć możliwości zarządzania punktami odniesienia zabezpieczeń.

> [!CAUTION]
> Nie są one wyrównane do określonych zasad firmy lub wymagań dotyczących zgodności innych firm. Te wskazówki mają na celu ułatwienie obsługi konwersacji, które będą prowadzić do wyrównania obu wymagań przy użyciu modelu ładu chmurowego.

## <a name="planning-and-readiness"></a>Planowanie i gotowość

W tej fazie działania ładu mostkuje podział między wynikami biznesowymi i strategiami, które mogą być funkcjonalne. W trakcie tego procesu zespół lidera definiuje określone metryki, mapuje te metryki na cyfrę elektroniczną i rozpoczyna planowanie ogólnego wysiłku migracji.

**Minimalna sugerowane działania:**

- Oceń opcje [łańcucha narzędzi linii bazowej zabezpieczeń](./toolchain.md) .
- Opracowywanie dokumentów z instrukcjami dotyczącymi architektury i dystrybucji do kluczowych uczestników projektu.
- Zaangażuj i powiąż osoby i zespoły, których dotyczy rozwój wytycznych dotyczących architektury.
- Dodaj priorytetowe zadania zabezpieczeń do zaległości migracji.

**Potencjalne działania:**

- Zdefiniuj schemat klasyfikacji danych.
- Przeprowadzaj proces planowania podpisywania elektronicznego, aby przeprowadzić spis bieżących zasobów IT, które ułatwiają procesy biznesowe i obsługują operacje.
- Przeprowadź [Przegląd zasad](../../govern/policy-compliance/cloud-policy-review.md) , aby rozpocząć proces modernizacji istniejących firmowych zasad zabezpieczeń IT i zdefiniować zasady MVP dotyczące znanych zagrożeń.
- Zapoznaj się z wytycznymi dotyczącymi zabezpieczeń platformy w chmurze. W przypadku platformy Azure można je znaleźć na [platformie zaufania usługi firmy Microsoft](https://www.microsoft.com/trustcenter/stp/default.aspx).
- Ustal, czy zasady linii bazowej zabezpieczeń obejmują [cykl rozwoju zabezpieczeń](https://www.microsoft.com/securityengineering/sdl).
- Oceń dane dotyczące sieci, danych i zasobów związanych z zasobami, które są zależne od od następnej do trzech wydań, i miernika tolerancji organizacji dla tych zagrożeń.
- Przejrzyj podstawowe trendy firmy Microsoft [w raporcie cyberbezpieczeństwa](https://www.microsoft.com/security/operations/security-intelligence-report) , aby zapoznać się z ogólnymi poziomami zabezpieczeń.
- Rozważ opracowanie roli [DevOps zabezpieczeń](https://www.microsoft.com/en-us/securityengineering/devsecops) w organizacji.

<!-- "en-us" location is required for the URL above. -->

## <a name="build-and-predeployment"></a>Kompilacja i prewdrażanie

Do pomyślnej migracji środowiska wymagane są pewne wymagania techniczne i nietechniczne. Ten proces koncentruje się na decyzjach, gotowości i infrastrukturze podstawowej, która przejdzie do migracji.

**Minimalna sugerowane działania:**

- Zaimplementuj swoją [linię bazową zabezpieczeń łańcucha narzędzi](./toolchain.md) , przechodząc do etapu preinstalacji.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury i dystrybucja do kluczowych uczestników projektu.
- Zaimplementuj zadania zabezpieczeń dla zaległości migracji z priorytetami.
- Opracowywanie materiałów edukacyjnych i dokumentacji, świadomości, zachęt i innych programów w celu ułatwienia wdrażania użytkowników.

**Potencjalne działania:**

- Określ strategię [szyfrowania](../../decision-guides/encryption/index.md) organizacji dla danych hostowanych w chmurze.
- Oceń strategię [tożsamości](../../decision-guides/identity/index.md) wdrożenia w chmurze. Określ, w jaki sposób rozwiązanie do tworzenia tożsamości oparte na chmurze będzie współistnieć lub zintegrowane z lokalnymi dostawcami tożsamości.
- Określ zasady granic sieci dla projektu [zdefiniowanej sieci komputerowej (SDN)](../../decision-guides/software-defined-network/index.md) w celu zapewnienia bezpieczeństwa zwirtualizowanych możliwości sieciowych.
- Oceń zasady dostępu o [najniższych uprawnieniach](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-delegate-by-task) organizacji i korzystaj z ról opartych na zadaniach, aby zapewnić dostęp do określonych zasobów.
- Zastosuj mechanizmy zabezpieczeń i monitorowania do wszystkich usług w chmurze i maszyn wirtualnych.
- Automatyzowanie [zasad zabezpieczeń](../../decision-guides/policy-enforcement/index.md) , jeśli jest to możliwe.
- Zapoznaj się z zasadami odniesienia zabezpieczeń i ustal, czy musisz zmodyfikować plany zgodnie z najlepszymi rozwiązaniami, takimi jak te opisane w [cyklu projektowania zabezpieczeń](https://www.microsoft.com/securityengineering/sdl).

## <a name="adopt-and-migrate"></a>Zastosuj i Migruj

Migracja to proces przyrostowy, który koncentruje się na przeniesieniu, testowaniu i wdrażaniu aplikacji lub obciążeń w istniejącym obszarze cyfrowym.

**Minimalna sugerowane działania:**

- Przeprowadź migrację [linii bazowej zabezpieczeń łańcucha narzędzi](./toolchain.md) z wstępnego wdrożenia do środowiska produkcyjnego.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury i dystrybucja do kluczowych uczestników projektu.
- Opracowywanie materiałów edukacyjnych i dokumentacji, świadomości, zachęt i innych programów w celu ułatwienia wdrażania użytkowników.

**Potencjalne działania:**

- Zapoznaj się z najnowszymi informacjami o zabezpieczeniach i zagrożeniami, aby zidentyfikować nowe zagrożenia biznesowe.
- Oceniaj tolerancję organizacji w celu obsługi nowych zagrożeń bezpieczeństwa, które mogą wystąpić.
- Zidentyfikuj odchylenia od zasad i wymuś poprawki.
- Dostosuj zabezpieczenia i automatyzację kontroli dostępu, aby zapewnić zgodność z zasadami.
- Upewnij się, że najlepsze rozwiązania zdefiniowane w fazie kompilacji i wdrożenia są prawidłowo wykonywane.
- Przejrzyj zasady dostępu o najniższych uprawnieniach i Dostosuj kontrolę dostępu, aby zmaksymalizować poziom zabezpieczeń.
- Przetestuj linię bazową zabezpieczeń łańcucha narzędzi względem obciążeń, aby identyfikować i rozwiązywać wszelkie luki w zabezpieczeniach.

## <a name="operate-and-post-implementation"></a>Działanie i po wdrożeniu

Po zakończeniu transformacji zarządzanie i działania muszą być aktywne w przypadku naturalnego cyklu życia aplikacji lub obciążenia. Ta faza zarządzania terminem spłaty koncentruje się na działaniach, które często są stosowane po wdrożeniu rozwiązania, a cykl transformacji zaczyna się ustabilizować.

**Minimalna sugerowane działania:**

- Weryfikuj i Uściślij [linię bazową zabezpieczeń łańcucha narzędzi](./toolchain.md).
- Dostosuj powiadomienia i raporty, aby otrzymywać alerty o potencjalnych problemach z zabezpieczeniami.
- Zawęzić wskazówki dotyczące architektury w celu zaplanowania przyszłych procesów wdrażania.
- Komunikuj się i przekazują okresowe zespoły, których dotyczy konieczność, aby zapewnić ciągłe przestrzeganie wytycznych dotyczących architektury.

**Potencjalne działania:**

- Odkryj wzorce i zachowanie dla obciążeń oraz skonfiguruj narzędzia do monitorowania i raportowania, aby identyfikować i powiadamiać o wszelkich nietypowych działaniach, dostępie lub użyciu zasobów.
- Stale Aktualizuj zasady monitorowania i raportowania, aby wykrywać Najnowsze luki w zabezpieczeniach, luki w zabezpieczeniach i ataki.
- Mają stosowane procedury umożliwiające szybkie zatrzymanie nieautoryzowanego dostępu i wyłączenie zasobów, które mogły zostać naruszone przez osobę atakującą.
- Regularnie zapoznaj się z najnowszymi najlepszymi rozwiązaniami w zakresie zabezpieczeń i stosuj zalecenia dotyczące funkcji zasad zabezpieczeń, automatyzacji i monitorowania, tam gdzie to możliwe.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz koncepcję zarządzania zabezpieczeniami w chmurze, przejdź do, aby dowiedzieć się więcej o [zabezpieczeniach i najlepszych rozwiązaniach, które firma Microsoft udostępnia](./azure-security-guidance.md) dla systemu Azure.

> [!div class="nextstepaction"]
> [Poznaj wskazówki dotyczące zabezpieczeń systemu Azure](./azure-security-guidance.md)
> [wprowadzenie do zabezpieczeń platformy Azure](https://docs.microsoft.com/azure/security/azure-security)
> [o rejestrowaniu, raportowaniu i monitorowaniu](../../decision-guides/logging-and-reporting/index.md)