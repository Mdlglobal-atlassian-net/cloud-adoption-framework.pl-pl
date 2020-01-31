---
title: Wiele centrów danych
description: Wiele centrów danych
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9156df0b76f6edf1d249d5d724e0a5d0f4fd8e15
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76803079"
---
# <a name="multiple-datacenters"></a>Wiele centrów danych

Często zakres migracji obejmuje przejście w wielu centrach danych. Poniższe wskazówki pomogą rozszerzyć zakres [przewodnika dotyczącego migracji na platformę Azure](../azure-migration-guide/index.md) w celu uwzględnienia wielu centrów danych.

## <a name="general-scope-expansion"></a>Ogólne rozszerzenie zakresu

Większość nakładu pracy wymaganego do rozszerzenia tego zakresu będzie potrzebna w ramach procesów wymagań wstępnych, oceniania i optymalizacji migracji.

## <a name="suggested-prerequisites"></a>Sugerowane wymagania wstępne

Przed rozpoczęciem migracji należy utworzyć epiki w narzędziu do zarządzania projektami, aby reprezentować każde centrum danych, które będzie migrowane. Następnie ważne jest, aby zrozumieć motywacje i wyniki biznesowe uzasadniające migrację. Te motywacje mogą służyć do określania priorytetów listy epików (lub centrów danych). Jeśli na przykład migracja wynika z zamiaru opuszczenia centrów danych przed odnowieniem dzierżawy, priorytet każdego epiku zostanie przydzielony w oparciu o datę odnowienia dzierżawy.

W ramach każdego epiku obciążenia do oceny i migracji byłyby zarządzane jako funkcje. Każdy zasób w ramach danego obciążenia będzie zarządzany jako scenariusz użytkownika. Praca wymagana do oceny, migracji, optymalizacji, promowania i zabezpieczania każdego zasobu oraz zarządzania nim byłaby reprezentowana jako zadania dla każdego zasobu.

Przebiegi lub iteracje następnie składałyby się z serii zadań wymaganych do przeprowadzenia migracji zasobów i scenariuszy użytkownika zatwierdzonych przez zespół wdrożeniowy ds. chmury. Wersje następnie składałyby się z co najmniej jednego obciążenia lub funkcji, których poziom ma zostać podwyższony do środowiska produkcyjnego.

## <a name="assess-process-changes"></a>Zmiany procesu oceniania

Największa zmiana w procesie oceniania — w przypadku rozszerzania zakresu na wiele centrów danych — jest związana z dokładną rejestracją i priorytetyzacją obciążeń oraz zależności w centrach danych.

### <a name="suggested-action-during-the-assess-process"></a>Sugerowana akcja w trakcie procesu oceny

**Oceń zależności między centrami danych:** [Narzędzia wizualizacji zależności w Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) mogą pomóc w wykrywaniu zależności. Mówiąc ogólnie, użycie tego zestawu narzędzi przed migracją jest dobrym rozwiązaniem. Jednak w przypadku obsługi złożoności na poziomie globalnym jest to niezbędny krok do procesu oceny. Za pośrednictwem [grupowania zależności](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies) wizualizacja może ułatwić identyfikację adresów IP i portów zasobów wymaganych do obsługi obciążenia.

> [!IMPORTANT]
> Dwie ważne uwagi: pierwszy ekspert, który ma świadomość rozmieszczenia zasobów i schematy adresów IP, jest wymagany do identyfikowania zasobów, które znajdują się w dodatkowym centrum danych. Po drugie ważne jest, aby oszacować zależności podrzędne i klientów w wizualizacji w celu zrozumienia zależności dwukierunkowych.

## <a name="migrate-process-changes"></a>Zmiany procesu migracji

Migrowanie wielu centrów danych jest podobne do konsolidowania centrów danych. Po migracji chmura staje się rozwiązaniem obejmującym pojedyncze centrum danych dla wielu zasobów. Najbardziej prawdopodobnym rozszerzeniem zakresu podczas migracji jest walidacja i dopasowanie adresów IP.

### <a name="suggested-action-during-the-migrate-process"></a>Sugerowana akcja w trakcie procesu migracji

Poniżej przedstawiono działania, które znacząco wpływają na sukces migracji w chmurze:

- **Oceń konflikty sieci:** W przypadku konsolidowania centrów danych do jednego dostawcy chmury istnieje prawdopodobieństwo utworzenia sieci, DNS lub innych konfliktów. Podczas migracji ważne jest przetestowanie pod kątem konfliktów, aby uniknąć zakłóceń w działaniu systemów produkcyjnych hostowanych w chmurze.
- **Aktualizowanie tabel routingu:** Często modyfikacje tabel routingu są wymagane podczas konsolidowania sieci lub centrów danych.

## <a name="optimize-and-promote-process-changes"></a>Optymalizacja i podwyższenie poziomu zmian procesu

W trakcie optymalizacji mogą być wymagane dodatkowe testy.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Sugerowana akcja w trakcie procesu optymalizacji i podwyższania poziomu

Przed podwyższeniem poziomu należy uwzględnić dodatkowe poziomy testowania podczas rozszerzania zakresu. Podczas testowania ważne jest przetestowanie pod kątem routingu lub innych konfliktów sieci. Ponadto ważne jest odizolowanie wdrożonej aplikacji i przetestowanie jej w celu sprawdzenia, czy wszystkie zależności zostały poddane migracji do chmury. W takim przypadku izolacja oznacza oddzielenie wdrożonego środowiska od sieci produkcyjnych. Dzięki temu można zidentyfikować pominięte zasoby, które nadal działają lokalnie.

## <a name="secure-and-manage-process-changes"></a>Zabezpieczanie zmian procesu oraz zarządzanie nimi

Procesy zabezpieczania i zarządzania nie powinny zostać zmienione podczas rozszerzania zakresu w ten sposób.

## <a name="next-steps"></a>Następne kroki

Wróć do [listy kontrolnej dotyczącej zakresu rozszerzonego](./index.md), aby upewnić się, że metoda migracji jest w pełni dopasowana.

> [!div class="nextstepaction"]
> [Lista kontrolna dotycząca zakresu rozszerzonego](./index.md)
