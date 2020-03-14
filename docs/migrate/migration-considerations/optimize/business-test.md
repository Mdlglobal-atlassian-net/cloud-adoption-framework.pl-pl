---
title: Wskazówki dotyczące testowania biznesowego podczas migracji
description: Dowiedz się, w jaki sposób testowanie biznesowe jest używane do żądania weryfikacji, że wydajność rozwiązania jest w linii z oczekiwaniami i nie utrudnia procesów biznesowych.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 675eda4aeb2109c21c2e3f47a100a985fd6e2861
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79311762"
---
# <a name="guidance-for-business-testing-uat-during-migration"></a>Wskazówki dotyczące testowania biznesowego (testowania akceptacyjnego przez użytkowników) podczas migracji

Tradycyjnie postrzegane jako funkcja działu IT, testowanie akceptacyjne przez użytkowników podczas transformacji firmy może być organizowane wyłącznie przez dział IT. Jednak ta funkcja jest często najbardziej efektywnie wykonywana jako funkcja biznesowa. Dział IT obsługuje wtedy to działanie biznesowe, ułatwiając testowanie, opracowując plany testowania i automatyzując testy, gdy jest to możliwe. Chociaż może być często używany jako surogat na potrzeby testowania, nic nie może zastąpić obserwacji rzeczywistych użytkowników próbujących wykorzystać nowe rozwiązanie w kontekście rzeczywistego lub zreplikowanego procesu biznesowego.

> [!NOTE]
> Jeśli jest dostępne, zautomatyzowane testowanie jest znacznie bardziej efektywnym i wydajnym sposobem testowania dowolnego systemu. Jednak migracje do chmury często najbardziej koncentrują się na starszych systemach lub co najmniej stabilnych systemach produkcyjnych. Często te systemy nie są zarządzane przez dokładne i dobrze obsługiwane testy automatyczne. W tym artykule przyjęto założenie, że żadne takie testy nie są dostępne w czasie migracji.

Drugą najlepszą metodą po testowaniu automatycznym jest testowanie zmian procesów i technologii przez użytkowników zaawansowanych. Użytkownicy zaawansowani to użytkownicy, którzy często wykonują rzeczywiste procesy wymagające interakcji z narzędziem lub zestawem narzędzi technologii. Mogą być reprezentowani przez zewnętrznego klienta korzystającego z witryny handlu elektronicznego do kupowania towarów lub usług. Użytkownicy zaawansowani mogą być również reprezentowani przez grupę pracowników wykonujących proces biznesowy, na przykład centrum telefonicznej obsługi klienta obsługujące klientów i rejestrujące ich wrażenia.

Celem testowania biznesowego jest poproszenie użytkowników zaawansowanych o zweryfikowanie nowego rozwiązania i potwierdzenie, że działa ono zgodnie z oczekiwaniami i nie utrudnia procesów biznesowych. Jeśli ten cel nie jest spełniony, testowanie biznesowe służy jako pętla opinii, która może pomóc w określeniu, jak i dlaczego obciążenie nie spełnia oczekiwań.

## <a name="business-activities-during-business-testing"></a>Działania biznesowe podczas testowania biznesowego

Podczas testowania biznesowego pierwsza iteracja jest określana ręcznie bezpośrednio z klientami. Jest to najczystsza, ale najbardziej czasochłonna forma pętli opinii.

- **Zidentyfikowanie użytkowników zaawansowanych.** Firma ogólnie lepiej zna użytkowników zaawansowanych, na których najbardziej wpływa zmiana techniczna.
- **Uzgodnienie i przygotowanie użytkowników zaawansowanych.** Upewnij się, że użytkownicy zaawansowani znają cele biznesowe, pożądane wyniki i oczekiwane zmiany procesów biznesowych. Przygotuj ich oraz ich strukturę zarządzania do procesu testowania.
- **Zaangażowanie w interpretację pętli opinii.** Pomóż pracownikom działu IT zrozumieć wpływ różnych punktów opinii użytkowników zaawansowanych.
- **Wyjaśnienie zmiany procesu.** Gdy transformacja może wyzwolić zmianę procesów biznesowych, poinformuj o zmianie i wszelkich wpływach na elementy podrzędne.
- **Określenie priorytetów opinii.** Pomóż zespołowi IT ustalić priorytety opinii na podstawie znaczenia dla działalności firmy.

Czasami dział IT może zatrudniać analityków lub właścicieli produktów, którzy mogą działać per procura na potrzeby określonych działań testowania biznesowego. Jednak uczestnictwo firm jest wysoce preferowane i prawdopodobnie przyniesie korzystne wyniki biznesowe.

## <a name="it-activities-during-business-testing"></a>Działania działu IT podczas testowania biznesowego

Dział IT jest jednym z odbiorców danych wyjściowych testowania biznesowego. Pętle opinii ujawniane podczas testowania biznesowego ostatecznie stają się elementami roboczymi, które definiują zmiany techniczne lub zmiany procesów. Jako adresat dział IT powinien pomagać w uproszczeniu, zbieraniu opinii oraz zarządzaniu wynikowymi działaniami technicznymi. Typowe działania wykonywane przez dział IT podczas testowania biznesowego obejmują:

- Zapewnianie struktury i logistyki na potrzeby testowania biznesowego.
- Pomoc podczas testowania.
- Udostępnianie metod i procesów na potrzeby rejestrowania opinii.
- Pomaganie firmie w ustalaniu priorytetów i weryfikowaniu opinii.
- Opracowywanie planów związanych ze zmianami technicznymi.
- Identyfikowanie istniejących testów automatycznych, które mogą usprawnić testowanie przez użytkowników zaawansowanych.
- W przypadku zmian, które mogą wymagać wielokrotnego wdrożenia lub testowania, badanie procesów testowania, definiowanie testów porównawczych i tworzenie automatyzacji w celu dalszego usprawnienia testowania przez użytkowników zaawansowanych.

## <a name="next-steps"></a>Następne kroki

W połączeniu z testowaniem biznesowym [optymalizacja zmigrowanych zasobów](./optimize.md) może poprawić wydajność kosztów i obciążeń.

> [!div class="nextstepaction"]
> [Testy porównawcze i zmiana rozmiaru zasobów w chmurze](./optimize.md)
