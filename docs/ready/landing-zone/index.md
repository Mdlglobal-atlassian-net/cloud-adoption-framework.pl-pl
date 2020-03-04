---
title: Co to jest strefa docelowa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się, w jaki sposób strefa docelowa zapewnia podstawowy blok konstrukcyjny dowolnego środowiska wdrażania chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 6db16b50115f2ba145dd4980dc5d57867f438de7
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78228363"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Co to jest strefa docelowa?

Infrastruktura jako kod to naturalny etap większości wdrożeń chmury. Wdrożenie pierwszych stref docelowych w chmurze jest typowym punktem wyjścia w celu przejścia do tworzenia środowiska stawiającego kod na pierwszym miejscu. Ten artykuł pomoże w zrozumieniu terminu _strefa docelowa_ i innych powiązanych terminów.

## <a name="landing-zone-definition"></a>Definicja strefy docelowej

Strefa docelowa to podstawowy blok konstrukcyjny każdego środowiska wdrażania chmury. Termin _strefa docelowa_ odnosi się do konstrukcji logicznej obejmującej wszystkie warunki, które muszą być spełnione, aby umożliwić odpowiednie wdrożenie chmury.

**Zakres:** W pełni funkcjonalna strefa docelowa bierze pod uwagę wszystkie zasoby platformy, które są wymagane do spełnienia potrzeb klienta dotyczących wdrożenia.

**Refaktoryzacja:** W pełni funkcjonalna strefa docelowa jest finalnym dostarczanym elementem dowolnej iteracji metodologii gotowości przewodnika Cloud Adoption Framework. Podczas każdej iteracji baza kodu definiująca strefę docelową zostanie zrefaktoryzowana lub rozwinięta. Po refaktoryzacji strefa docelowa może zostać zmodyfikowana lub ponownie wdrożona, aby spełniać nowe potrzeby związane z wdrożeniem chmury.

**Cel:** Celem podejścia opierającego się na strefie docelowej jest utworzenie wspólnego zestawu spójnych implementacji platformy. Te spójne implementacje muszą być stosowane w celu zapewnienia, że aplikacje będą mieć dostęp do wymaganych składników po wdrożeniu. W związku z tym każda iteracja strefy docelowej musi zostać zaprojektowana i wdrożona zgodnie z wymaganiami planu wdrażania chmury i strategii projektowania subskrypcji.

**Podstawowe przeznaczenie:** Podstawowym przeznaczeniem strefy docelowej jest upewnienie się, że gdy aplikacja zostanie umieszczona na platformie Azure, wszystkie elementy niezbędne do jej działania będą już gotowe.

## <a name="landing-zone-usage"></a>Użycie strefy docelowej

Strefy docelowe nie muszą odróżniać wdrożenia IaaS od wdrożenia PaaS. Jednak strefy docelowe są specjalnie tworzone w celu wspierania planu wdrożenia przez realizowanie strategii subskrypcji. Wsparcie planu wdrożenia może wymagać wielu stref docelowych z różnymi wymaganymi składnikami.

Przeznaczenie i zakres ogólnego planu wdrożenia chmury określi wymagane elementy niezbędne do działania. Dodatkowe wymagania dotyczące ładu, zgodności, zabezpieczeń i zarządzania operacyjnego prawdopodobnie poszerzą początkowy zakres strefy docelowej. Na wczesnych etapach wdrażania strefy docelowe mogą obejmować mniej elementów niezbędnych do działania w wyniku zdefiniowanych wymagań i akceptowalnych zagrożeń.  Gdy istnieje wiele stref docelowych, często każda strefa docelowa jest zależna od centrów udostępniających wymagane mechanizmy kontroli w ramach modelu usług udostępnionych.

## <a name="related-terms"></a>Powiązane terminy

- **Usługi udostępnione:** Obciążenia często mają udostępnione zależności, które są używane przez wiele różnych obciążeń. Podejście obejmujące usługi udostępnione przenosi wiele z tych typowych zależności do jednej konstrukcji logicznej.

- **Model piasty i szprych:** Jedną z implementacji podejścia obejmującego usługi udostępnione jest model piasty i szprych. W tym modelu piasta to jedna konstrukcja logiczna służąca do hostowania wszystkich usług udostępnionych. Strefy docelowe działają jak szprychy rozchodzące się od piasty, w oparciu o typowe zależności.

- **Niezależna strefa docelowa:** Niektóre podejścia do stref docelowych nie wymagają dedykowanego centrum. Najczęściej zdarza się to wtedy, gdy wszystkie zasoby produkcyjne (aplikacje, dane i maszyny wirtualne) w planie wdrożenia chmury mogą być bezpiecznie hostowane i zarządzane w jednym środowisku.

## <a name="next-steps"></a>Następne kroki

Aby rozpocząć korzystanie ze stref docelowych, [wybierz pierwszą strefę docelową](./first-landing-zone.md).

> [!div class="nextstepaction"]
> [Wybieranie pierwszej strefy docelowej](./first-landing-zone.md)
