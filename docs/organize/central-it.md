---
title: Centralne możliwości IT
description: Dowiedz się więcej na temat tworzenia centralnych możliwości IT.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 17f2395a435d8a29202595caec17932b406a1303
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806938"
---
# <a name="central-it-capabilities"></a>Centralne możliwości IT

W miarę skalowania rozwiązań związanych z zarządzaniem chmurą same możliwości zarządzania chmurą mogą nie być wystarczające do zarządzania wysiłkami. Gdy przyjęcie jest stopniowe, zespoły będą w sposób ekologiczny rozwijać umiejętności i procesy wymagane do przygotowania do chmury w czasie.

Jeśli jednak jeden zespół wdrażania w chmurze używa chmury w celu osiągnięcia wyników działalności dla dużej firmy, to najprawdopodobniej będzie to w przypadku stopniowego wdrażania. Powodzenie następuje po sukcesie. Ma to również zastosowanie w przypadku wdrażania w chmurze, ale ma to miejsce w skali chmury. Gdy wdrożenie chmurowe rozszerza się z jednego zespołu do wielu zespołów, konieczne jest dodatkowe wsparcie z istniejących pracowników działu IT. However, those staff members may lack the training and experience required to support the cloud using cloud-native IT tools. This often drives the formation of a central IT team governing the cloud.

> [!CAUTION]
> While this is a common maturity step, it can present a high risk to adoption, potentially blocking innovation and migration efforts if not managed effectively. See the risk section below to learn how to mitigate the risk of centralization becoming a cultural antipattern.

## <a name="possible-sources-for-central-it-expertise"></a>Possible sources for central IT expertise

The skills needed to provide centralized IT capabilities could be provided by:

- An existing Central IT team
- Enterprise architects
- IT operations
- IT governance
- IT infrastructure
- Networking
- Tożsamość
- Wirtualizacja
- Ciągłość biznesowa i odzyskiwanie po awarii
- Application owners within IT

> [!WARNING]
> Central IT should only be applied in the cloud when existing delivery on-premises is based on a Central IT model. If the current on-premises model is based on delegated control, consider a cloud center of excellence (CCoE) approach for a more compatible alternative.

## <a name="key-responsibilities"></a>Key responsibilities

Adapt existing IT practices to ensure adoption efforts result in well-governed, well-managed environments in the cloud.

The following tasks are typically executed regularly:

### <a name="strategic-tasks"></a>Strategic tasks

- Review:
  - [business outcomes](../strategy/business-outcomes/index.md)
  - [financial models](../strategy/financial-models.md)
  - [motivations for cloud adoption](../strategy/motivations.md)
  - [business risks](../govern/policy-compliance/risk-tolerance.md)
  - [rationalization of the digital estate](../digital-estate/index.md)
- Monitor adoption plans and progress against the [prioritized migration backlog](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identify and prioritize platform changes that are required to support the migration backlog.
- Act as an intermediary or translation layer between cloud adoption needs and existing IT teams.
- Leverage existing IT teams to accelerate platform capabilities and enable adoption.

### <a name="technical-tasks"></a>Technical tasks

- Build and maintain the cloud platform to support solutions.
- Define and implement the platform architecture.
- Operate and manage the cloud platform.
- Continuously improve the platform.
- Keep up with new innovations in the cloud platform.
- Deliver new cloud capabilities to support business value creation.
- Suggest self-service solutions.
- Ensure that solutions meet existing governance and compliance requirements.
- Create and validate deployment of platform architecture.
- Review release plans for sources of new platform requirements.

## <a name="meeting-cadence"></a>Meeting cadence

Central IT expertise usually comes from a working team. Expect participants to commit much of their daily schedules to alignment efforts. Contributions aren't limited to meetings and feedback cycles.

## <a name="central-it-risks"></a>Central IT risks

Each of the cloud capabilities and phases of organizational maturity are prefixed with the word "cloud". Central IT is the only exception. Central IT became prevalent when all IT assets could be housed in few locations, managed by a small number of teams, and controlled through a single operations management platform. Global business practices and the digital economy have largely reduced the instances of those centrally managed environments.

In the modern view of IT, assets are globally distributed. Responsibilities are delegated. Operations management is delivered by a mixture of internal staff, managed service providers, and cloud providers. In the digital economy, IT management practices are transitioning to a model of self-service and delegated control with clear guardrails to enforce governance. Central IT can be a valuable contributor to cloud adoption by becoming a cloud broker and a partner for innovation and business agility.

Central IT as a function is well positioned to take valuable knowledge and practices from existing on-premises models and apply those practices to cloud delivery. However, this process will require change. New processes, new skills, and new tools are required to support cloud adoption at scale. When Central IT adapts, it becomes an important partner in cloud adoption efforts. However, if Central IT doesn't adapt to the cloud, or attempts to use the cloud as a catalyst for tight-grain controls, Central IT quickly becomes a blocker to adoption, innovation, and migration.

The measures of this risk are speed and flexibility. The cloud simplifies adopting new technologies quickly. When new cloud capabilities can be deployed within minutes, but Central IT reviews add weeks or months to the deployment process, then these centralized processes become a major impediment to business success. When this indicator is encountered, consider alternative strategies to IT delivery.

### <a name="exceptions"></a>Wyjątki

Many industries require rigid adherence to third-party compliance. Some compliance requirements still demand centralized IT control. Delivering on these compliance measures can add time to deployment processes, especially for new technologies that haven't been used broadly. In these scenarios, expect delays in deployment during the early stages of adoption. Similar situations my exist for companies that deal with sensitive customer data, but may not be governed by a third-party compliance requirement.

### <a name="operate-within-the-exceptions"></a>Operate within the exceptions

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
