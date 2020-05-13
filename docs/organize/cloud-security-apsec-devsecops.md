---
title: Informacje o zabezpieczeniach aplikacji i funkcjach DevSecOps
description: Informacje o zabezpieczeniach aplikacji i funkcjach DevSecOps.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 04/30/2020
ms.openlocfilehash: 723b7339c29870f267c4b469f2b8a0de79ee026b
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83228458"
---
# <a name="application-security-and-devsecops-functions"></a>Zabezpieczenia aplikacji i funkcje DevSecOps

Celem zabezpieczeń aplikacji i DevSecOps jest integrowanie zabezpieczeń z procesami tworzenia i niestandardowymi aplikacjami biznesowymi (LOB).

## <a name="modernization"></a>Modernizacja

Tworzenie aplikacji jest błyskawicznie przetwarzane w wielu aspektach jednocześnie obejmujących model zespołu DevOps, DevOps szybkie wydanie erze i techniczne składanie aplikacji za pośrednictwem usług w chmurze i interfejsów API. Zobacz, w jaki sposób chmura zmienia relacje zabezpieczeń i obowiązki, aby uzyskać więcej informacji o tych zmianach.

Ta modernizacja modeli programistycznych antiquated przedstawia zarówno szansę, jak i wymaganie modernizacji zabezpieczeń aplikacji i procesów programistycznych. Synteza zabezpieczeń w procesach DevOps jest często określana jako DevSecOps i zmiany dysków, w tym:

<!-- TODO: Link needed below? -->
- **Zabezpieczenia są zintegrowane, a nie poza zatwierdzeniem:** Gwałtowny tempo zmian w programowaniu aplikacji sprawia, że klasyczne i nieaktualne podejście do "skanowania" i "Raport". Te starsze podejścia nie pomogą w rozwiązaniu z wersjami bez konieczności programowania, aby zachowywać i zwiększać opóźnienia na rynku, niedostateczne wykorzystanie deweloperów i wzrost zaległości problemu.
  - **Przesuń w lewo** , aby zaangażować zabezpieczenia wcześniej w procesach tworzenia aplikacji w miarę jak rozwiązanie problemów jest tańsze, szybsze i bardziej efektywne. Jeśli użytkownik zaczeka, aż zostanie rozszerzania ciastka, będzie trudniejszy do zmiany kształtu.
  - **Integracja natywna:** Należy bezproblemowo zintegrować rozwiązania dotyczące zabezpieczeń, aby uniknąć nieprawidłowej kondycji w przepływach pracy deweloperskiej i procesach ciągłej integracji/ciągłego wdrażania (CI/CD). Aby dowiedzieć się, jak usługi GitHub zbliżają się do tego, zobacz [Zabezpieczanie oprogramowania](https://github.blog/2019-09-18-securing-software-together/).
  - **Bezpieczeństwo wysokiej jakości:** Zabezpieczenia muszą zapewniać informacje i wskazówki dotyczące wysokiej jakości, dzięki którym deweloperzy mogą szybko rozwiązywać problemy i nie mogą tracić czasu dewelopera na fałszywie dodatnich.
  - **Przezbieżna kultura:** Role zabezpieczeń, programowania i operacji powinny współtworzyć najważniejsze elementy w współdzielonej kulturze, wartości udostępnione i wspólnych celach oraz accountabilities.
- **Zabezpieczenia Agile:** Przełączenie zabezpieczeń z "musi być idealne do dostarczania" do podejścia Agile, które rozpoczyna się od minimalnego poziomu zabezpieczeń aplikacji (oraz dla procesów, w których można je opracowywać), które są stale udoskonalane przyrostowo.
- Należy wdrożyć infrastrukturę i funkcje zabezpieczeń w **chmurze** w celu usprawnienia procesów programistycznych podczas integrowania zabezpieczeń.
- **Zarządzanie ryzykiem łańcucha dostaw:** Należy zastosować podejście "bez zaufania" do oprogramowania typu Open Source (OSS) i składników innych firm, które sprawdza integralność i zapewnia, że poprawki i aktualizacje błędów są stosowane do tych składników.
- **Ciągła nauka:** Szybka wersja usługi dla deweloperów (nazywana czasami usługami Platform as a Service, PaaS) i zmiana kompozycji aplikacji oznacza, że członkowie zespołu deweloperów, Ops i zabezpieczeń będą stale uczyć się nowej technologii.
- Programowe **podejście** do zabezpieczeń aplikacji w celu zapewnienia ciągłego ulepszania podejścia Agile.

Aby uzyskać dodatkowy kontekst, zobacz [Microsoft Secure Development cykl życia](https://www.microsoft.com/sdl).

## <a name="team-composition-and-key-relationships"></a>Kompozycja zespołu i relacje między kluczami

Funkcje Security Application i DevSecOps są idealnym rozwiązaniem przez deweloperów i zespołów operacyjnych obsługujących zabezpieczenia (z obsługą ekspertów z dziedziny zabezpieczeń).

Ta funkcja często współdziała z innymi funkcjami i ekspertami, w tym:.

- Architektura i operacje związane z zabezpieczeniami
- Zabezpieczenia infrastruktury
- Komunikacja (szkolenia i narzędzia)
- Bezpieczeństwo osób
- Tożsamość i klucze
- Zespoły zarządzania zgodnością/ryzykiem
- Główne liderzy biznesowi lub ich przedstawiciele

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z funkcją [zabezpieczenia danych](./cloud-security-data-security.md).
