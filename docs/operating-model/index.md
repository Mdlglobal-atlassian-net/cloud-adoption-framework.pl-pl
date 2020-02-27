---
title: Wprowadzenie do modelu operacyjnego
description: Omówienie modelu operacyjnego na potrzeby przewodnika Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: operating-model
ms.openlocfilehash: 093f404ce4e8a5a9c5f60b5ee3bb81064ba5b3f8
ms.sourcegitcommit: 10f687bb1316db509fc1a3dbde72e107a467d72a
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/26/2020
ms.locfileid: "77629287"
---
# <a name="establish-an-operating-model-for-the-cloud"></a>Ustanawianie modelu operacyjnego dla chmury

Wdrażanie chmury to proces iteracyjny skoncentrowany na działaniach w chmurze. Strategia chmury określa przebieg transformacji cyfrowej, wyznaczając kierunki programów biznesowych, w ramach których różne zespoły realizują projekty wdrażania. Etapy planowania i gotowości pomagają w zapewnieniu powodzenia w każdym z tych istotnych aspektów. Wszystkie etapy wdrażania chmury to faktyczne projekty, mające określone cele, terminy i budżety, którymi można zarządzać.

Te działania związane z wdrażaniem można relatywnie łatwo monitorować i mierzyć, nawet jeśli dotyczą wielu planowanych iteracji i wydań. Każda faza cyklu wdrażania jest ważna. Na każdym etapie mogą potencjalnie wystąpić przeszkody o charakterze biznesowym, kulturowym lub technologicznym. Jednak każda z faz w dużej mierze zależy od bazowego modelu operacyjnego.

**O ile wdrażanie opisuje działania, model operacyjny definiuje elementy „kto” i „jak”, niezbędne dla procesu wdrażania.**

Kultura firmy może całkowicie zrujnować strategię. Model operacyjny odzwierciedla kulturę IT, ujmując ją w szereg mierzalnych procesów. Gdy chmura bazuje na solidnym modelu operacyjnym, kultura będzie napędzać realizację strategii, procesu wdrażania i wartości biznesowych. Natomiast bez modelu operacyjnego nawet pomyślne wdrożenie przyniesie co najwyżej krótkotrwałe rezultaty. Długotrwałe powodzenie wymaga równoległego rozwijania modelu wdrażania i modelu operacyjnego.

## <a name="establish-your-operating-model"></a>Ustanawianie modelu operacyjnego

Obecne modele operacyjne można skalować, tak aby wspierały wdrożenie chmury. Nowoczesny model operacyjny pomaga w usuwaniu nietechnicznych czynników blokujących wdrażanie chmury.

Ta sekcja przewodnika Cloud Adoption Framework przedstawia praktyczny model operacyjny, ułatwiający podejmowanie decyzji nietechnicznych. Ten model operacyjny składa się z trzech metodologii, które są pomocne podczas tworzenia własnego chmurowego modelu operacyjnego:

- [Utrzymanie ładu](../govern/index.md): Zapewnij spójność wszystkich działań wdrożeniowych. Dostosuj je do wymagań dotyczących ładu i zgodności, aby zachować dobrze zarządzane środowisko międzychmurowe.
- [Zarządzanie](../manage/index.md): Dopasowanie bieżących procesów operacyjnego zarządzania technologią w celu maksymalizacji zyskiwanej wartości i minimalizacji zakłóceń.
- [Organizowanie](../organize/index.md): Organizacja różnych zespołów i funkcji wspierających model operacyjny będzie rozwijać się wraz z tym modelem.

## <a name="align-operating-models"></a>Dopasowanie modeli operacyjnych

Chmura i gospodarka cyfrowa zwróciły uwagę na potrzebę stosowania większej liczby modeli operacyjnych. Czasem ta potrzeba wynika z konieczności obsługi wielu chmur publicznych. Jeszcze częściej wiąże się z przejściem ze środowiska lokalnego do chmury. W obu scenariuszach ważne jest dopasowanie tych modeli operacyjnych w sposób zapewniający maksymalną wydajność przy minimalnej nadmiarowości.

Analitycy przewidują, że wdrażane będą rozwiązania z wieloma chmurami i dużymi ilościami danych. Działanie wielu klientów wskazuje na słuszność tego przewidywania. Niestety klienci zgłaszają poważne trudności w obsłudze wielu chmur. Duplikowanie zasobów, procesów, umiejętności i technologii prowadzi do zwiększenia kosztów, a nie do oszczędności, na jakie wskazywały prognozy dotyczące chmury. Aby tego uniknąć, klienci powinni przyjąć wyspecjalizowany model operacyjny. Jeśli dopasowuje się różne modele operacyjne, jednym z nich zawsze powinien być **ogólny model operacyjny**. Dodatkowe **wyspecjalizowane modele operacyjne** powinny z kolei być stosowane w konkretnych sytuacjach, odbiegających od modelu standardowego.

- **Ogólny model operacyjny:** Ogólny model operacyjny dotyczy jednej publicznej lub prywatnej platformy chmurowej. Operacje tej platformy definiują standardy, zasady i procesy operacyjne. Ten model operacyjny powinien być podstawą realizacji strategii chmury. W tym modelu celem jest korzystanie z podstawowego dostawcy usług w chmurze na potrzeby większości działań związanych z wdrażaniem chmury.

- **Wyspecjalizowany model operacyjny:** Określone wyniki biznesowe mogą być realizowane lepiej z pomocą alternatywnego dostawcy usług w chmurze. W uzasadnionych biznesowo sytuacjach do nowego dostawcy usług w chmurze stosuje się standardy, zasady i procesy ujęte w ogólnym modelu operacyjnym, ale zmodyfikowane stosownie do danego przypadku.

Jeśli jako platformę podstawową wybrano platformę Azure, wskazówki i najlepsze rozwiązania opisane w powyższych sekcjach dotyczących modelu operacyjnego będą bardzo przydatne podczas tworzenia własnego modelu operacyjnego. W tej strukturze uwzględniono jednak, że nie wszyscy nasi czytelnicy wybrali platformę Azure jako podstawową. Z uwagi na potrzeby tego szerszego grona odbiorców treści teoretyczne z poszczególnych sekcji można zastosować do modeli operacyjnych chmury publicznej lub prywatnej z podobnymi wynikami.

## <a name="next-steps"></a>Następne kroki

Ustanowienie ładu to typowy pierwszy krok w kierunku ustanowienia modelu operacyjnego dla chmury.

> [!div class="nextstepaction"]
> [Więcej informacji o ładzie w chmurze](../govern/index.md)
