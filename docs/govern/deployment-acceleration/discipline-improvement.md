---
title: Udoskonalenie ulepszeń wdrożenia
description: Udoskonalenie ulepszeń wdrożenia
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c5f07137ac1ca8c3ddbc4717dba5622096551862
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76805935"
---
# <a name="deployment-acceleration-discipline-improvement"></a>Udoskonalenie ulepszeń wdrożenia

Dyscyplina wdrożenia koncentruje się na tworzeniu zasad, które gwarantują, że zasoby są wdrażane i konfigurowane spójnie i powtarzane i pozostają zgodne w całym cyklu życia. W ramach pięciu dyscyplin nadzoru w chmurze przyspieszenie wdrożenia obejmuje decyzje dotyczące automatyzowania wdrożeń, kontroli źródłowego artefaktów wdrożenia, monitorowania wdrożonych zasobów w celu utrzymania żądanego stanu i inspekcji zgodności. luk.

W tym artykule przedstawiono niektóre potencjalne zadania, w których firma może uczestniczyć w ulepszaniu rozwoju dyscypliny wdrożenia. Te zadania mogą być podzielone na planowanie, kompilowanie, przyjmowanie i eksploatację etapów wdrażania rozwiązania w chmurze, które są następnie powtarzane na umożliwieniu rozwoju [przyrostowego podejścia do zarządzania chmurą](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cztery etapy wdrażania](../../_images/govern/adoption-phases.png)

*Rysunek 1. etapy wdrażania przyrostowego podejścia do ładu w chmurze.*

Nie jest możliwe, aby żaden z dokumentów mógł uwzględnić wymagania wszystkich firm. W tym artykule opisano sugerowane minimalne i potencjalne przykładowe działania dla każdej fazy procesu ładu. Początkowym celem tych działań jest ułatwienie tworzenia programu MVP dla [zasad](../guides/index.md#an-incremental-approach-to-cloud-governance) i ustanowienie platformy do ulepszania zasad. Zespół ds. zarządzania chmurą będzie musiał zdecydować, jak dużo inwestować w te działania, aby usprawnić możliwości ładu planu bazowego tożsamości.

> [!CAUTION]
> Nie są one wyrównane do określonych zasad firmy lub wymagań dotyczących zgodności innych firm. Te wskazówki mają na celu ułatwienie obsługi konwersacji, które będą prowadzić do wyrównania obu wymagań przy użyciu modelu ładu chmurowego.

## <a name="planning-and-readiness"></a>Planowanie i gotowość

W tej fazie działania ładu mostkuje podział między wynikami biznesowymi i strategiami, które mogą być funkcjonalne. W trakcie tego procesu zespół lidera definiuje określone metryki, mapuje te metryki na cyfrę elektroniczną i rozpoczyna planowanie ogólnego wysiłku migracji.

**Minimalna sugerowane działania:**

- Oceń [łańcucha narzędzi opcje przyspieszania wdrażania](./toolchain.md) i Implementuj strategię hybrydową, która jest odpowiednia dla Twojej organizacji.
- Opracowywanie dokumentów z instrukcjami dotyczącymi architektury i dystrybucji do kluczowych uczestników projektu.
- Zaangażuj i powiąż osoby i zespoły, których dotyczy rozwój wytycznych dotyczących architektury.
- Uczenie zespołów programistycznych i pracowników działu IT w celu zrozumienia zasad i strategii DevSecOps oraz znaczenia w pełni zautomatyzowanych wdrożeń w ramach przyspieszenia wdrożenia.

**Potencjalne działania:**

- Zdefiniuj role i przydziały, które będą zarządzać przyspieszeniem wdrożenia w chmurze.

## <a name="build-and-predeployment"></a>Kompilacja i prewdrażanie

**Minimalna sugerowane działania:**

- W przypadku nowych aplikacji opartych na chmurze wprowadź w pełni zautomatyzowane wdrożenia na początku procesu tworzenia oprogramowania. Ta inwestycja poprawi niezawodność procesów testowych i zapewnia spójność w środowiskach deweloperskich, pytań i odpowiedzi.
- Wszystkie artefakty wdrożenia, takie jak szablony wdrażania lub skrypty konfiguracyjne, są przechowywane przy użyciu platformy kontroli źródła, takiej jak GitHub lub Azure DevOps.
- Przechowuj wszystkie wpisy tajne, hasła, certyfikaty i parametry połączeń w [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)
- Rozważmy test pilotażowy przed wdrożeniem [przyspieszania wdrażania łańcucha narzędzi](./toolchain.md), aby upewnić się, że usprawnia wdrożenia tak jak to możliwe. Zastosuj opinię z testów pilotażowych w fazie prewdrażania, powtarzając się w razie konieczności.
- Oceń logiczną i fizyczną architekturę aplikacji, a także Zidentyfikuj możliwości automatyzacji wdrażania zasobów aplikacji lub Popraw fragmenty architektury przy użyciu innych zasobów opartych na chmurze.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury w celu uwzględnienia planów wdrażania i wdrożenia użytkowników oraz dystrybucji do kluczowych udziałowców.
- Kontynuuj, aby wypróbować ludzi i zespoły, których dotyczą wskazówki dotyczące architektury.

**Potencjalne działania:**

- Zdefiniuj potok ciągłej integracji i ciągłego wdrażania (CI/CD), aby w pełni zarządzać udostępnianymi aktualizacjami aplikacji za pomocą środowisk programistycznych, pytań i odpowiedzi.

## <a name="adopt-and-migrate"></a>Zastosuj i Migruj

Migracja to proces przyrostowy, który koncentruje się na przeniesieniu, testowaniu i wdrażaniu aplikacji lub obciążeń w istniejącym obszarze cyfrowym.

**Minimalna sugerowane działania:**

- Migruj [przyspieszenie wdrażania łańcucha narzędzi](./toolchain.md) od projektowania do produkcji.
- Aktualizacja dokumentu z instrukcjami dotyczącymi architektury i dystrybucja do kluczowych uczestników projektu.
- Opracowywanie materiałów edukacyjnych i dokumentacji, świadomości, zachęt i innych programów w celu ułatwienia deweloperom i przyjęciu rozwiązań IT.

**Potencjalne działania:**

- Upewnij się, że najlepsze rozwiązania zdefiniowane w fazie kompilacji i wdrożenia są prawidłowo wykonywane.
- Upewnij się, że każda aplikacja lub obciążenie jest zgodne z strategią przyspieszania wdrażania przed wydaniem.

## <a name="operate-and-post-implementation"></a>Działanie i po wdrożeniu

Po zakończeniu transformacji zarządzanie i działania muszą być aktywne w przypadku naturalnego cyklu życia aplikacji lub obciążenia. Ta faza zarządzania terminem spłaty koncentruje się na działaniach, które często są stosowane po wdrożeniu rozwiązania, a cykl transformacji zaczyna się ustabilizować.

**Minimalna sugerowane działania:**

- Dostosuj [przyspieszenie wdrażania łańcucha narzędzi](./toolchain.md) na podstawie zmian potrzeb związanych z tożsamościami w organizacji.
- Automatyzuj powiadomienia i raporty, aby otrzymywać alerty o potencjalnych problemach z konfiguracją lub złośliwych zagrożeniach.
- Monitorowanie i raportowanie dotyczące użycia aplikacji i zasobów.
- Zgłoś metryki po wdrożeniu i Dystrybuuj je do zainteresowanych stron.
- Popraw wskazówki dotyczące architektury w celu zaplanowania przyszłych procesów wdrażania.
- Kontynuuj komunikację z i uczenie odpowiednich osób i zespołów w regularnych odstępach czasu, aby zapewnić stałe przestrzeganie wytycznych dotyczących architektury.

**Potencjalne działania:**

- Skonfiguruj narzędzie do monitorowania i raportowania konfiguracji żądanego stanu.
- Regularnie Przeglądaj narzędzia i skrypty konfiguracyjne, aby usprawnić procesy i zidentyfikować typowe problemy.
- Pracuj z zespołami programistycznymi, operacyjnymi i ds. zabezpieczeń, aby pomóc w wczesnych praktykach DevSecOps i podzielić silosy organizacyjne, które prowadzą do niewydajności.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz koncepcję zarządzania tożsamościami w chmurze, Przeanalizuj [linię bazową tożsamości łańcucha narzędzi](./toolchain.md) , aby identyfikować narzędzia i funkcje platformy Azure, które będą potrzebne podczas tworzenia dyscypliny ładu planu bazowego tożsamości na platformie Azure.

> [!div class="nextstepaction"]
> [Łańcucha narzędzi linii bazowej tożsamości dla platformy Azure](./toolchain.md)
