---
title: Co to jest strefa docelowa?
description: Dowiedz się, w jaki sposób strefa docelowa zapewnia podstawowy blok konstrukcyjny dowolnego środowiska wdrażania chmury.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/25/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: fbb39153dc729b7822c53520e9424a5280cb013a
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621745"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-a-landing-zone"></a>Co to jest strefa docelowa?

Infrastruktura jako kod to typowe wymaganie w większości wdrożeń chmury. Przejście do tworzenia środowisk typu „code-first” („najpierw kod”) może wymagać od członków zespołu dodatkowego okresu nauki i wprowadzenia zmian w różnych aspektach operacji, zabezpieczeń, zapewnienia ładu i zgodności. Wdrożenie oddzielnych, planowo tworzonych stref docelowych może skrócić ten okres nauki i pomóc zespołowi w terminowym realizowaniu planów wdrożenia. W tym artykule przedstawione zostaną definicje terminu _strefa docelowa_ i innych powiązanych terminów. Inne artykuły w tej serii zawierają instrukcje tworzenia stref docelowych.

## <a name="prerequisite-to-landing-zone-deployment"></a>Wymagania wstępne związane z wdrażaniem strefy docelowej

Przed zdefiniowaniem stref docelowych należy poznać pokrewny termin: _podstawy platformy_. W każdym środowisku (w chmurze, lokalnym lub hybrydowym) znajdziemy zbór _podstawowych narzędzi_ używanych do obsługi wszystkich, różnorodnych obciążeń. Te obciążenia są potrzebne firmie do działania. Dział IT potrzebuje tych podstawowych narzędzi do zarządzania całym _portfolio_ obciążeń, zapewnienia ładu i zabezpieczenia ich. Aby uzyskać więcej informacji na temat tych pokrewnych terminów i zależności między nimi, zobacz [Hierarchia portfolio](../../reference/fundamental-concepts/hosting-hierarchy.md).

**Podstawy platformy:** Przed wdrożeniem stref docelowych zakłada się, że dla strefy docelowej są dostępne scentralizowane mechanizmy sterowania na potrzeby tożsamości, zabezpieczeń, operacji, zapewnienia zgodności i ładu, zawarte we wspólnych _podstawach platformy_ używanych do obsługi wszystkich obciążeń na danej platformie w chmurze. Wszystkie obciążenia w każdej strefie docelowej będą sterowane za pomocą tych mechanizmów, co zapewnia wspólny punkt odniesienia dla wszystkich _wspólnych filarów architektury_, do których należą zabezpieczenia, niezawodność, wydajność, koszt i operacje w chmurze.

**Podział obowiązków:** Należy wprowadzić wyraźny podział obowiązków na pracę związaną z obciążeniami wykonywaną w strefie docelowej oraz działanie narzędzi zarządzanych poza strefą docelową. Ten podział obowiązków umożliwia właściwe zapewnienie ładu i zgodności. Ponadto gwarantuje, że każdy zespół rozważy i omówi wszelkie wyjątki od zasad firmowych zamiast szybko tworzyć obejścia, które mogłyby naruszyć bezpieczeństwo środowiska.

> [!CAUTION]
> Podział obowiązków nie powinien zniechęcać zespołów przed korzystaniem z tych najlepszych rozwiązań ze względu na aktualne zatrudnienie czy struktury zespołów. Na wczesnych etapach wdrażania chmury może się zdarzyć, że jeden zespół ds. wdrożenia będzie tymczasowo wykonywał wszystkie obowiązki związane z wdrożeniem technologii chmury, zapewnieniem ładu, zabezpieczeniami i operacjami w kontekście kilku wybranych obciążeń. Jeśli plan przygotowany na przyszłość obejmuje podział obowiązków, czy nawet izolację zadań, to jest to nadal sugerowane najlepsze rozwiązanie.

**Wspólne obowiązki:** _Podstawy platformy_ zapewniają scentralizowane mechanizmy zarządzania platformą w chmurze. Nadal wspólnym obowiązkiem wszystkich członków zespołu jest uwzględnianie w swojej pracy wymagań związanych z obsługą tożsamości, zabezpieczeniami, operacjami, zgodnością i zapewnieniem ładu. Przed wdrożeniem jakiejkolwiek technologii w strefie docelowej należy rozważyć to, jakie narzędzia zapewniają _podstawy platformy_, a co trzeba będzie wdrożyć w strefie docelowej w celu realizacji wspólnych obowiązków.

> [!IMPORTANT]
> Deweloperzy i architekci wdrażający rozwiązania w strefie docelowej mogą skorzystać z przewodnika [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/), aby uwzględnić i wykorzystać wspólne filary architektury podczas projektowania, tworzenia i obsługi obciążeń działających w strefie docelowej.

## <a name="landing-zone-definition"></a>Definicja strefy docelowej

_Strefa docelowa_ to część środowiska w chmurze aprowizowana przy użyciu kodu i przeznaczona do obsługi **określonego obciążenia lub większej liczby obciążeń**. Strefy docelowe zapewniają dostęp do podstawowych narzędzi i mechanizmów sterowania i stanowią zgodną lokalizację do wprowadzania innowacji i tworzenia nowych obciążeń w chmurze lub migrowania istniejących obciążeń do chmury. Strefy docelowe wykorzystują zdefiniowane zestawy usług w chmurze i najlepszych rozwiązań, ułatwiając pomyślne wdrożenie.

Mówiąc ściślej, strefa docelowa to podstawowy blok konstrukcyjny każdego środowiska wdrażania chmury. Termin _strefa docelowa_ odnosi się do konstrukcji logicznej umożliwiającej współistnienie obciążeń, będącej dodatkiem do _podstaw platformy_. Podstawy platformy i strefy docelowe łącznie obejmują wszystko, co potrzebne do umożliwienia wdrożenia chmury w całym portfolio rozwiązań informatycznych.

**Zakres:** W pełni funkcjonalna strefa docelowa bierze pod uwagę wszystkie narzędzia platformy, które są wymagane do spełnienia potrzeb klienta dotyczących wdrożenia.

**Refaktoryzacja:** W pełni funkcjonalna strefa docelowa jest finalnym dostarczanym elementem dowolnej iteracji metodologii gotowości przewodnika Cloud Adoption Framework. Podczas każdej iteracji baza kodu definiująca strefę docelową zostanie zrefaktoryzowana lub rozwinięta. Po refaktoryzacji strefa docelowa może zostać zmodyfikowana lub ponownie wdrożona, aby spełniać nowe potrzeby związane z wdrożeniem chmury.

**Cel:** W podejściu opartym na strefach docelowych celem jest utworzenie wspólnego zestawu spójnych wdrożeń platformy, umożliwiającego zespołom wdrożeniowym korzystanie z zarządzanych centralnie _podstaw platformy_. Te spójne implementacje muszą być stosowane w celu zapewnienia, że aplikacje będą mieć dostęp do wymaganych składników po wdrożeniu. W związku z tym każda iteracja strefy docelowej musi zostać zaprojektowana i wdrożona zgodnie z wymaganiami planu wdrażania chmury i strategii projektowania subskrypcji.

**Podstawowe przeznaczenie:** Podstawowym przeznaczeniem strefy docelowej jest zapewnienie, że gdy aplikacja zostanie umieszczona w chmurze, wszystkie elementy i narzędzia niezbędne do jej działania będą już gotowe.

**Korzyści:** Strefy docelowe i wspólne podstawy platformy łącznie zapewniają spójność w zakresie _wspólnych filarów architektury_, którymi są zabezpieczenia, niezawodność, wydajność, koszt i operacje w chmurze. To połączenie zmniejsza też nakład pracy wymagany do zarządzania operacjami, ładem i zgodnością w całym portfolio rozwiązań informatycznych. W kontekście rosnących wymagań związanych z wdrażaniem chmury strefy docelowe minimalizują zakres refaktoryzacji i wdrożeń wymaganych do skalowania wdrożenia zgodnie z potrzebami.

## <a name="landing-zone-usage"></a>Użycie strefy docelowej

Strefy docelowe nie muszą odróżniać wdrożenia IaaS od wdrożenia PaaS. Jednak strefy docelowe są specjalnie tworzone w celu wspierania planu wdrożenia przez realizowanie strategii subskrypcji. Wsparcie planu wdrożenia może wymagać wielu stref docelowych z różnymi wymaganymi składnikami.

Przeznaczenie i zakres ogólnego planu wdrożenia chmury określi wymagane elementy niezbędne do działania. Dodatkowe wymagania dotyczące ładu, zgodności, zabezpieczeń i zarządzania operacyjnego prawdopodobnie poszerzą początkowy zakres strefy docelowej. Na wczesnych etapach wdrażania strefy docelowe mogą obejmować mniej elementów niezbędnych do działania w wyniku zdefiniowanych wymagań i akceptowalnych zagrożeń. Gdy istnieje wiele stref docelowych, często każda strefa docelowa jest zależna od centrów udostępniających wymagane mechanizmy kontroli w ramach modelu usług udostępnionych.

## <a name="decentralized-operations"></a>Operacje zdecentralizowane

W niektórych zdecentralizowanych organizacjach projekt wdrożenia zakłada istnienie zespołów ds. obciążeń, ponoszących **wyłączną odpowiedzialność** za wdrożenie i obsługę swoich izolowanych obciążeń, co obejmuje zabezpieczenia, zapewnienie ładu, zarządzanie operacjami i inne funkcje. W przypadku takich zespołów obciążenie może działać we własnym, izolowanym środowisku, bez zależności od podstaw platformy. Takie środowiska specyficzne dla obciążeń obejmowałyby niespójne implementacje zabezpieczeń, niezawodności, wydajności, kosztów i operacji w chmurze. W związku z tym nie powinny być nazywane strefami docelowymi. Tego typu zespoły mogą skorzystać z przewodnika [Azure Architecture Framework](https://docs.microsoft.com/azure/architecture/framework/), który pomoże im w niezależnym zaprojektowaniu, utworzeniu i zoptymalizowaniu każdego obciążenia.

> [!IMPORTANT]
> Podobna, ale odrębna, jest następująca sytuacja: na wczesnym etapie cyklu wdrażania chmury mniejsze zespoły mogą z konieczności działać w sposób podobny do organizacji zdecentralizowanych. Jeśli zespoły działają w sposób zdecentralizowany z powodu konkretnych okoliczności (a nie planowo), również należy stosować najlepsze rozwiązanie obejmujące strefy docelowe.

## <a name="portfolio-hierarchy"></a>Hierarchia portfolio

Strefy docelowe to jedna z warstw ogólnej hierarchii portfolio, zgodnie z opisem w sekcji dotyczącej wymagań wstępnych. Istnienie stref docelowych wskazuje, że firma obsługuje szersze portfolio rozwiązań, przy wsparciu różnych zespołów, procesów i scentralizowanych _podstaw platformy_. Aby uzyskać więcej informacji kontekstowych na temat miejsca stref docelowych w ogólnym projekcie portfolio, zobacz artykuł poświęcony [hierarchii portfolio](../../reference/fundamental-concepts/hosting-hierarchy.md). Aby uzyskać więcej informacji o produktach dostępnych na platformie Azure umożliwiających zarządzanie różnymi warstwami hierarchii portfolio, zobacz [Obsługa hierarchii platformy Azure](../../reference/fundamental-concepts/hierarchy-azure-tools.md).

## <a name="next-steps"></a>Następne kroki

Przed utworzeniem pierwszej strefy docelowej ważne jest zapoznanie się z [zasadami refaktoryzacji](./refactor.md), które rządzą tym podejściem.

> [!div class="nextstepaction"]
> [Refaktoryzacja stref docelowych](./refactor.md)
