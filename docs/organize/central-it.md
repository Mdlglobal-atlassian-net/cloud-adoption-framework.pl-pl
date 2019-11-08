---
title: Centralne możliwości IT
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej na temat tworzenia centralnych możliwości IT.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 25e9ecd4d911766864d81a5ff34f00caf82e86bf
ms.sourcegitcommit: 6f287276650e731163047f543d23581d8fb6e204
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753629"
---
# <a name="central-it-capabilities"></a>Centralne możliwości IT

W miarę skalowania rozwiązań związanych z zarządzaniem chmurą same możliwości zarządzania chmurą mogą nie być wystarczające do zarządzania wysiłkami. Gdy przyjęcie jest stopniowe, zespoły będą w sposób ekologiczny rozwijać umiejętności i procesy wymagane do przygotowania do chmury w czasie.

Jeśli jednak jeden zespół wdrażania w chmurze używa chmury w celu osiągnięcia wyników działalności dla dużej firmy, to najprawdopodobniej będzie to w przypadku stopniowego wdrażania. Powodzenie następuje po sukcesie. Ma to również zastosowanie w przypadku wdrażania w chmurze, ale ma to miejsce w skali chmury. Gdy wdrożenie chmurowe rozszerza się z jednego zespołu do wielu zespołów, konieczne jest dodatkowe wsparcie z istniejących pracowników działu IT. Jednak Ci członkowie personelu mogą nie mieć szkoleń i doświadczeń wymaganych do obsługi chmury przy użyciu natywnych narzędzi IT w chmurze. Często dotyczy to tworzenia centralnych zespołów IT zarządzających chmurą.

> [!CAUTION]
> Chociaż jest to typowy etap zapadalności, może to stanowić wysokie ryzyko dla przyjęcia, potencjalnie blokując innowacje i wysiłki w zakresie migracji, jeśli nie jest to efektywnie zarządzane. Zapoznaj się z sekcją ryzyko poniżej, aby dowiedzieć się, jak ograniczyć ryzyko scentralizowanego działania centralizacji.

## <a name="possible-sources-for-central-it-expertise"></a>Możliwe źródła dla centralnej wiedzy IT

Umiejętności niezbędne do zapewnienia scentralizowanych możliwości IT mogą być udostępniane przez:

- Istniejący centralny zespół IT
- Enterprise Architects
- Operacje IT
- Zarządzanie IT
- Infrastruktura IT
- Networking
- Tożsamość
- Wirtualizacja
- Ciągłość biznesowa i odzyskiwanie po awarii
- Właściciele aplikacji w ramach tej

> [!WARNING]
> Centralna usługa powinna być stosowana tylko w chmurze, gdy istniejąca usługa dostarczania jest oparta na centralnym modelu IT. Jeśli bieżący model lokalny jest oparty na delegowanej kontroli, weź pod uwagę podejście do rozwiązania Cloud Center of doskonałości (CCoE) w celu uzyskania bardziej zgodnej alternatywy.

## <a name="key-responsibilities"></a>Kluczowe obowiązki

Dostosuj istniejące praktyki IT, aby zapewnić, że wysiłki w zakresie wdrażania są dobrym sposobem, dobrze zarządzane środowiska w chmurze.

Następujące zadania są zwykle wykonywane regularnie:

### <a name="strategic-tasks"></a>Zadania strategiczne

- Ponownego
  - [wyniki biznesowe](../strategy/business-outcomes/index.md)
  - [Modele finansowe](../strategy/financial-models.md)
  - [motywacje do wdrożenia w chmurze](../strategy/motivations.md)
  - [ryzyka biznesowe](../govern/policy-compliance/risk-tolerance.md)
  - [Racjonalizacja podpisu cyfrowego](../digital-estate/index.md)
- Monitoruj plany wdrażania i postęp w odniesieniu do [zaległości migracji z priorytetami](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Zidentyfikuj i ustal priorytety zmian platformy, które są wymagane do obsługi zaległości migracji.
- Wykonaj działania jako pośrednią lub warstwę translacji między potrzebami wdrażania chmury a istniejącymi zespołami IT.
- Skorzystaj z istniejących zespołów IT, aby przyspieszyć możliwości platformy i włączyć wdrażanie.

### <a name="technical-tasks"></a>Zadania techniczne

- Kompiluj i obsługuj platformę w chmurze w celu obsługi rozwiązań.
- Zdefiniuj i Implementuj architekturę platformy.
- Pracuj i Zarządzaj platformą w chmurze.
- Ciągle ulepszaj platformę.
- Zadbaj o nowe innowacje na platformie chmury.
- Dostarczaj nowe możliwości chmury umożliwiające obsługę tworzenia wartości biznesowej.
- Sugeruj rozwiązania samoobsługowe.
- Upewnij się, że rozwiązania zaspokajają istniejące wymagania dotyczące zarządzania i zgodności.
- Utwórz i sprawdź poprawność wdrożenia architektury platformy.
- Zapoznaj się z planami wydania dla źródeł nowych wymagań platformy.

## <a name="meeting-cadence"></a>Erze spotkania

Centralna wiedza IT zazwyczaj pochodzi od zespołu roboczego. Oczekuje się, że uczestnicy zatwierdzają wiele codziennych harmonogramów do wyrównania. Udziały nie są ograniczone do spotkań i cykli przesyłania opinii.

## <a name="central-it-risks"></a>Centralne zagrożenia IT

Każda usługa w chmurze i fazy zapadalności w organizacji są poprzedzone wyrazem "Cloud". Jest to jedyny wyjątek. Centralna stała się ogólnie, gdy wszystkie zasoby IT mogły być przechowywane w kilku lokalizacjach, zarządzane przez małą liczbę zespołów i kontrolowane przez pojedynczą platformę zarządzania operacjami. Globalne praktyki biznesowe i oszczędności cyfrowe znacznie zmniejszają wystąpienia tych środowisk zarządzanych centralnie.

W nowoczesnych widokach zasoby są dystrybuowane globalnie. Obowiązki są delegowane. Zarządzanie operacjami jest realizowane przez kombinację pracowników wewnętrznych, dostawców usług zarządzanych i dostawców chmury. W przypadku korzystania z sieci cyfrowych praktyki zarządzania IT są przenoszone do modelu samoobsługowego i delegowanej kontroli z jasno guardrails, aby wymusić zarządzanie. Centralny dział IT może być cennym współautorem rozwiązań chmurowych przez przeprowadzeniem brokera w chmurze i partnera na potrzeby innowacji i elastyczność biznesową.

Centralnie jako funkcja jest również pozycjonowane, aby uzyskać cenne informacje i praktyki z istniejących modeli lokalnych i zastosować te praktyki do dostarczania w chmurze. Jednak ten proces będzie wymagał zmian. Nowe procesy, nowe umiejętności i nowe narzędzia są wymagane do obsługi wdrażania w chmurze na dużą skalę. Po dobieraniu centralnych rozwiązań IT jest to ważny partner w zakresie działań związanych z wdrażaniem w chmurze. Jeśli jednak centralna usługa nie dostosowuje się do chmury lub próbuje użyć chmury jako katalizatora dla kontrolek ścisłych, centralnie przestanie ona być blokowana do przyjęcia, innowacji i migracji.

Środki tego ryzyka to szybkość i elastyczność. Chmura upraszcza szybkie wdrażanie nowych technologii. Jeśli nowe możliwości chmury można wdrożyć w ciągu kilku minut, ale centralne przeglądy IT dodają tygodnie lub miesiące do procesu wdrażania, a następnie te scentralizowane procesy stają się główną przeszkód dla sukcesu firmy. Po napotkaniu tego wskaźnika należy rozważyć alternatywne strategie dotyczące dostarczania IT.

### <a name="exceptions"></a>Wyjątki

Wiele branż wymaga ścisłego przestrzegania zgodności z innymi firmami. Niektóre wymagania dotyczące zgodności nadal wymagają scentralizowanej kontroli IT. Dostarczanie na te środki zgodności może zwiększyć czas wdrożenia procesów wdrażania, szczególnie w przypadku nowych technologii, które nie były szeroko używane. W tych scenariuszach oczekiwane są opóźnienia wdrożenia na wczesnych etapach wdrażania. Podobne sytuacje występują dla firm, które zajmują się poufnymi danymi klienta, ale mogą nie podlegać wymogom zgodności innych firm.

### <a name="operate-within-the-exceptions"></a>Działa w ramach wyjątków

Gdy centralne procesy IT są wymagane, a procesy te tworzą odpowiednie punkty kontrolne w przyjęciu nowych technologii, te punkty kontrolne innowacji mogą być nadal szybko rozwiązywane. Wymagania dotyczące zarządzania i zgodności są przeznaczone do ochrony tych, które są poufne, a nie do ochrony wszystkiego. Chmura zapewnia proste mechanizmy pobierania i wdrażania izolowanych zasobów przy zachowaniu właściwych guardrails.

Dojrzały centralny zespół IT utrzymuje niezbędne zabezpieczenia, ale negocjuje praktyki, które nadal umożliwiają innowacje. Wykazanie tego poziomu zapadalności zależy od właściwej klasyfikacji i izolacji zasobów.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Przykładowe opisy działania w ramach wyjątków w celu podjęcia przyjęcia

Ta przykładowa ilustracja przedstawia podejście podejmowane przez dojrzały centralny zespół IT w celu przyjęcia wdrożenia.

Firma Contoso przyjęła centralny model IT na potrzeby obsługi zasobów w chmurze firmy. Aby można było dostarczyć ten model, mają one zaimplementowane ścisłe kontrolki dla różnych usług udostępnionych, na przykład połączeń sieciowych przychodzących. Dzięki temu można zmniejszyć narażenie środowiska chmury i zapewnić, że jedno urządzenie "ze szlifem" blokuje cały ruch w przypadku naruszenia. Stan zasad linii bazowej zabezpieczeń, który cały ruch przychodzący musi następować przez udostępnione urządzenie zarządzane przez centralny zespół IT.

Jednak jeden z zespołów wdrażania chmury wymaga teraz środowiska z dedykowanym i specjalnie skonfigurowanym połączeniem sieciowym, aby można było korzystać z określonej technologii chmury. Niedojrzały centralny zespół IT po prostu odrzuca żądanie i ustala priorytety swoich istniejących procesów na potrzeby wdrażania. Centralny zespół IT firmy Contoso jest inny. Szybko zidentyfikowały proste, czwarte rozwiązanie do tego dylematem: klasyfikacji, negocjacji, izolacji i automatyzacji.

**Klasyfikacja:** Ponieważ zespół ds. wdrażania chmury był na wczesnym etapie tworzenia nowego rozwiązania i nie miał żadnych poufnych danych ani wymagań związanych z obsługą techniczną, zasoby w środowisku zostały sklasyfikowane jako niskie ryzyko i niekrytyczne. Obowiązująca Klasyfikacja to znak zapadalności w centrali. Klasyfikowanie wszystkich zasobów i środowisk umożliwia wyczyszczenie zasad.

**Negocjowanie:** Sama klasyfikacja nie jest wystarczająca. Usługi udostępnione zostały wdrożone w celu spójnego działania zasobów poufnych i o kluczowym znaczeniu. Zmiana reguł spowoduje naruszenie zasad zarządzania i zgodności dla zasobów, które wymagają większej ochrony. Nie można nawiązać przyjęcia na koszt stabilności, bezpieczeństwa lub zarządzania. Prowadzi to do negocjacji z zespołem ds. wdrażania, aby odpowiedzieć na określone pytania. Czy zespół DevOps, który prowadzi działalność biznesową, będzie w stanie zapewnić zarządzanie operacjami w tym środowisku? Czy to rozwiązanie wymaga bezpośredniego dostępu do innych zasobów wewnętrznych? Jeśli zespół adopcji w chmurze jest wygodny dla tych kompromisów, może być możliwy ruch przychodzący.

**Izolacja:** Ponieważ firma może zapewnić własne bieżące zarządzanie operacjami, a ponieważ rozwiązanie nie polega na kierowaniu ruchu do innych zasobów wewnętrznych, można je odizolowywane w nowej subskrypcji. Ta subskrypcja jest również dodawana do oddzielnego węzła nowej hierarchii grupy zarządzania.

**Automatyzacja:** Kolejną oznaką zapadalności w tym zespole są zasady automatyzacji. Zespół używa Azure Policy do automatyzowania wymuszania zasad. Używają one również planów platformy Azure do automatyzowania wdrażania wspólnych składników platformy i wymuszania zgodności z określoną linią bazową tożsamości. W przypadku tej subskrypcji i innych w nowej grupie zarządzania zasady i szablony są nieco inne. Zasady blokujące przepustowość transferu danych przychodzących zostały zniesione. Zostały one zastąpione przez wymagania związane z kierowaniem ruchu przez subskrypcję usług udostępnionych, podobnie jak w przypadku ruchu przychodzącego, aby wymusić izolację ruchu. Ponieważ lokalne narzędzia do zarządzania operacjami nie mogą uzyskać dostępu do tej subskrypcji, agenci tego narzędzia nie są już wymagani. Wszystkie inne guardrailsy ładu wymagane przez inne subskrypcje w hierarchii grupy zarządzania nadal są wymuszane, co zapewnia wystarczającą guardrails.

Współczesne podejście do scentralizowanego zespołu IT firmy Contoso zapewniało rozwiązanie, które nie spowodowało naruszenia zasad zarządzania lub zgodności, ale nadal było to zalecane. To podejście do brokera, a nie posiadające natywne podejścia chmurowego do scentralizowanego, to pierwszy krok w kierunku tworzenia prawdziwej usługi Cloud Center doskonałości (CCoE). Przyjęcie tej metody w celu szybkiego rozwoju istniejących zasad umożliwi scentralizowanej kontroli, gdy jest to wymagane, i zarządzanie guardrails, gdy będzie możliwe zwiększenie elastyczności. NALEŻY zrównoważyć te dwa kwestie w celu zmniejszenia ryzyka związanego z centralnym użyciem w chmurze.

## <a name="next-steps"></a>Następne kroki

W miarę jak centralnie odnosi się do chmury, kolejny etap zapadalności jest zwykle niezależny od [operacji w chmurze](./cloud-operations.md). Dostępność natywnych narzędzi do zarządzania operacjami w chmurze i niższych kosztów operacyjnych dla rozwiązań PaaS-First często prowadzi do zespołów gospodarczych (lub bardziej szczegółowych zespołów DevOps w firmie) przy założeniu, że odpowiedzialność za operacje w chmurze.

> [!div class="nextstepaction"]
> [Możliwości operacji w chmurze](./cloud-operations.md)
