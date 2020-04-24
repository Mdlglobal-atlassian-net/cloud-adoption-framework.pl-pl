---
title: Złożoność kulturowa dopasowania ról i obowiązków
description: Użyj struktury wdrażania w chmurze dla platformy Azure, aby przygotować się do złożoności kulturalnej przez dostosowanie ról i obowiązków do zwiększenia przejrzystości podczas procesu migracji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: fe86c196e03e8908d3c9bb409cc3896286729015
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80429074"
---
# <a name="prepare-for-cultural-complexity-aligning-roles-and-responsibilities"></a>Przygotowanie na złożoność kulturową: wyrównywanie ról i obowiązków

Zrozumienie kultury wymaganej do obsługi istniejących centrów danych jest istotne dla sukcesu każdej migracji. W niektórych organizacjach zarządzanie centrum danych jest ograniczone do scentralizowanych zespołów operacyjnych IT. W takich scentralizowanych zespołach role i obowiązki są zwykle dobrze zdefiniowane i zrozumiałe dla całego zespołu. W przypadku większych przedsiębiorstw, szczególnie tych, które muszą spełniać wymagania zgodności z innymi organizacjami, kultura jest zróżnicowana i złożona. Złożoność kulturowa może prowadzić do powstawania trudnych do zrozumienia przeszkód, których eliminowanie jest czasochłonne.

W każdym scenariuszu należy zainwestować dokumentację ról i obowiązków wymaganych do przeprowadzenia migracji. W tym artykule opisano niektóre role i obowiązki występujące w ramach migracji centrum danych, które służą jako szablon dokumentacji ułatwiający zapewnianie przejrzystości w trakcie procesu.

## <a name="business-functions"></a>Funkcje biznesowe

W każdej migracji istnieje kilka najważniejszych funkcji, które powinny być w firmie wykonywane, o ile jest to możliwe. Często dział IT jest w stanie wykonać poniższe zadania. Jednak zaangażowanie innych pracowników może pomóc w usuwaniu barier w dalszej części procesu wdrażania. Zapewnia również zaangażowanie najważniejszych osób biorących udział w projekcie przez cały proces migracji.

| Proces | Działanie | Opis |
|---------|---------|---------|
| Ocena | Cele biznesowe | Zdefiniuj oczekiwane wyniki biznesowe procesu migracji. |
| Ocena | Priorytety | Upewnij się, że uwzględniono zmieniające się priorytety firmy i warunki rynkowe. |
| Ocena | Uzasadnienie | Zweryfikuj założenia będące podstawą zmieniających się uzasadnień biznesowych. |
| Ocena | Ryzyko | Pomóż zespołowi wdrożeniowemu ds. chmury zrozumieć wpływ rzeczywistego ryzyka biznesowego. |
| Ocena | Zatwierdzenie | Sprawdź i zatwierdź wpływ proponowanych zmian architektury na firmę. |
| Optymalizacja | Plan zmian | Zdefiniuj plan stosowania zmian w firmie, w tym okresów niskiej aktywności i blokowania zmian. |
| Optymalizacja | Testowanie | Zaangażuj zaawansowanych użytkowników, którzy mogą sprawdzić poprawność działania i funkcjonalność. |
| Zabezpieczanie i zarządzanie | Wpływ przerw | Pomóż zespołowi wdrożeniowemu ds. chmury określić wpływ przerw na działanie procesów biznesowych. |
| Zabezpieczanie i zarządzanie | Walidacja umowy dotyczącej poziomu usług (SLA) | Pomóż zespołowi wdrożeniowemu ds. chmury w definiowaniu umów dotyczących poziomu usług i akceptowalnych tolerancji dla przerw w działaniu firmy. |

Ostatecznie zespół wdrożeniowy ds. chmury jest odpowiedzialny za każde z tych działań. Jednak określenie obowiązków i dbanie o stałe tempo pracy w celu ukończenia tych działań zgodnie ustalonym rytmem może poprawić współpracę między osobami biorącymi udział w projekcie i spójność z działaniami biznesowymi.

## <a name="common-roles-and-responsibilities"></a>Typowe role i obowiązki

Każdy proces w ramach dyskusji dotyczącej zasad migracji struktury wdrażania chmury (CAF) zawiera artykuł dotyczący procesu, w którym przedstawiono konkretne działania umożliwiające uzgodnienie ról i obowiązków. W celu zachowania przejrzystości podczas wykonywania należy przypisać do każdego działania pojedynczą osobę odpowiedzialną wraz z wszelkimi osobami odpowiedzialnymi wymaganymi do obsługi tych działań. Jednak poniższa lista zawiera szereg typowych ról i obowiązków, które mają większy wpływ na wykonanie migracji. Te role należy zidentyfikować na wczesnym etapie migracji.

> [!NOTE]
> W poniższej tabeli należy rozpocząć dopasowywanie ról i osób odpowiedzialnych. Tę kolumnę należy dostosować do istniejących procesów, aby zapewnić ich wydajne wykonywanie. Najlepiej jest, gdy jedna osoba jest wyznaczona jako osoba odpowiedzialna.

| Proces | Działanie | Opis | Strona odpowiedzialna |
|---------|---------|---------|---------|
| Wymagania wstępne | Majątek cyfrowy | Na podstawie wyników biznesowych dopasuj istniejący spis do podstawowych założeń. | zespół strategiczny ds. chmury |
| Wymagania wstępne | Lista prac związanych z migracją | Określ priorytet sekwencji obciążeń, które mają zostać zmigrowane. | zespół strategiczny ds. chmury |
| Ocena | Architektura | Zweryfikuj wstępne założenia w celu zdefiniowania architektury docelowej na podstawie metryk użycia. | zespół wdrożeniowy ds. chmury |
| Ocena | Zatwierdzenie | Zatwierdź proponowaną architekturę. | zespół strategiczny ds. chmury |
| Migrate (Migracja) | Dostęp w celu replikacji | Uzyskaj dostęp do istniejących hostów i zasobów lokalnych w celu ustanowienia procesów replikacji. | zespół wdrożeniowy ds. chmury |
| Optymalizacja | Gotowy | Przed podwyższeniem poziomu sprawdź, czy system spełnia wymagania dotyczące wydajności i kosztów. | zespół wdrożeniowy ds. chmury |
| Optymalizacja | Podwyższanie poziomu | Uprawnienia do podwyższenia poziomu obciążenia do środowiska produkcyjnego i przekierowania ruchu produkcyjnego. | zespół wdrożeniowy ds. chmury |
| Zabezpieczanie i zarządzanie | Przeniesienie operacji | Udokumentuj systemy produkcyjne przed operacjami produkcyjnymi. | zespół wdrożeniowy ds. chmury |

> [!CAUTION]
> W przypadku tych działań uprawnienia i autoryzacja znacznie wpływają na stronę odpowiedzialną, która musi mieć bezpośredni dostęp do systemów produkcyjnych w istniejącym środowisku lub środki zabezpieczające dostęp za pośrednictwem innych odpowiedzialnych podmiotów. Określenie tej strony odpowiedzialnej bezpośrednio wpływa na strategię podwyższania poziomu podczas migracji i optymalizacji procesów.

## <a name="next-steps"></a>Następne kroki

Gdy zespół ma ogólne zrozumienie ról i obowiązków, czas rozpoczęcia przygotowywania szczegółów technicznych migracji. Zrozumienie [złożoności technicznej i zarządzania zmianami](./technical-complexity.md) może pomóc w przygotowaniu zespołu wdrożeniowego ds. chmury na złożoność techniczną migracji przez dostosowanie do procesu zarządzania zmianami przyrostowymi.

> [!div class="nextstepaction"]
> [Złożoność techniczna i zarządzanie zmianami](./technical-complexity.md)
