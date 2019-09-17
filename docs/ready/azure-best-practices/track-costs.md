---
title: Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e026ac8c46fd8c39d2c6ff36c3612fed2bed7e82
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022158"
---
# <a name="track-costs-across-business-units-environments-or-projects"></a>Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach

[Tworzenie organizacji świadomej w zakresie kosztów](../../organize/cost-conscious-organization.md) wymaga widoczności oraz prawidłowo zdefiniowanego dostępu (lub zakresu) do danych związanych z kosztami. W tym artykule z najlepszymi rozwiązaniami przedstawiono metody podejmowania decyzji i wdrażania podczas tworzenia mechanizmów śledzenia.

![Konspekt procesu uwzględniającego koszty](../../_images/ready/cost-optimization-process.png)

## <a name="establish-a-well-managed-environment-hierarchy"></a>Ustanowienie hierarchii dobrze zarządzanego środowiska

Kontrola kosztów, podobnie jak ład i inne konstrukcje zarządzania, zależy od dobrze zarządzanego środowiska. Ustanowienie takiego środowiska (szczególnie złożonego) wymaga spójnych procesów w klasyfikacji i organizacji wszystkich zasobów.

Zasoby obejmują wszystkie maszyny wirtualne, źródła danych i aplikacje wdrożone w chmurze. Platforma Azure oferuje kilka mechanizmów klasyfikowania i organizowania zasobów. W temacie [Scaling with multiple Azure subscriptions](../considerations/scaling-subscriptions.md) (Skalowanie za pomocą wielu subskrypcji platformy Azure) przedstawiono szczegółowe informacje dotyczące opcji organizowania zasobów według wielu kryteriów, aby ustanowić dobrze zarządzane środowisko. Ten artykuł koncentruje się na zastosowaniu podstawowych koncepcji platformy Azure w celu zapewnienia widoczności kosztów chmury.

### <a name="classification"></a>Klasyfikacja

*Tagowanie* to prosty sposób na klasyfikowanie zasobów. Tagowanie kojarzy metadane z zasobem. Te metadane mogą służyć do klasyfikowania zasobów na podstawie różnych punktów danych. Gdy tagi zostają użyte do klasyfikowania zasobów w ramach nakładu pracy związanego z zarządzaniem kosztami, firmy często potrzebują następujących tagów: jednostki biznesowej, działu, kodu rozliczeń, geografii, środowiska, projektu oraz obciążenia lub „kategoryzacji aplikacji”. Usługa Azure Cost Management może używać tych tagów do tworzenia różnych widoków danych kosztów.

Tagowanie jest podstawowym sposobem na zrozumienie danych w dowolnych raportach o kosztach. Stanowi podstawową część dowolnego dobrze zarządzanego środowiska. Jest to również pierwszy krok w celu ustalenia właściwego ładu w dowolnym środowisku.

Pierwszym krokiem w procesie dokładnego śledzenia informacji o kosztach w różnych jednostkach biznesowych, środowiskach i projektach jest zdefiniowanie standardu tagowania. Drugim krokiem jest upewnienie się, że standard tagowania jest stosowany w sposób spójny. Poniższe artykuły mogą pomóc w wykonaniu każdego z tych kroków:

- [Develop naming and tagging standards](../considerations/naming-and-tagging.md) (Opracowywanie standardów nazewnictwa i tagowania)
- [Establish a governance MVP to enforce tagging standards](../../govern/guides/complex/index.md) (Ustanowienie ładu w programie MVP, aby wymusić standardy tagowania)

### <a name="resource-organization"></a>Organizacja zasobów

Istnieje kilka metod organizowania zasobów. W tej sekcji przedstawiono najlepsze rozwiązanie oparte na potrzebach dużego przedsiębiorstwa, w którym struktury kosztów są rozmieszczone między różnymi jednostkami biznesowymi, lokalizacjami geograficznymi oraz organizacjami informatycznymi. Podobne najlepsze rozwiązanie dla mniejszej, mniej złożonej organizacji zostało opisane w temacie [Podróż po ładzie dla małych i średnich przedsiębiorstw](../../govern/guides/standard/index.md).

W przypadku dużego przedsiębiorstwa następujący model grup zarządzania, subskrypcji i grup zasobów utworzy hierarchię, która umożliwi każdemu zespołowi uzyskanie poziomu widoczności odpowiedniego do wykonywania swoich obowiązków. Gdy przedsiębiorstwo wymaga kontroli kosztów, aby zapobiec przekroczeniu budżetu, może stosować narzędzia do zarządzania, takie jak Azure Blueprints lub Azure Policy, do subskrypcji w tej strukturze, aby szybko blokować przyszłe błędy związane z kosztami.

![Diagram organizacji zasobów w dużym przedsiębiorstwie](../../_images/govern/large-enterprise-resource-organization.png)

Na diagramie powyżej katalog główny hierarchii grupy zarządzania zawiera węzeł dla każdej jednostki biznesowej. W tym przykładzie firma międzynarodowa musi mieć wgląd w regionalne jednostki biznesowe, więc tworzy węzeł do geografii w obszarze poszczególnych jednostek biznesowych w hierarchii.

W ramach każdej geografii istnieje osobny węzeł dla środowisk produkcyjnych i nieprodukcyjnych, który umożliwia odizolowanie kosztów, dostępu i kontroli ładu. Aby umożliwić bardziej wydajne operacje oraz rozsądniejsze inwestowanie w nie, firma korzysta z subskrypcji, aby dodatkowo odizolować środowiska produkcyjne o różnym stopniu zobowiązań w zakresie wydajności operacyjnej. Wreszcie firma wykorzystuje grupy zasobów do przechwytywania jednostek funkcji do wdrożenia, nazywanych aplikacjami.

Na diagramie przedstawiono najlepsze rozwiązania oprócz następujących opcji:

- Wiele firm ogranicza operacje do jednego regionu geopolitycznego. Takie podejście ogranicza potrzebę różnicowania dyscyplin ładu lub danych kosztów na podstawie lokalnych wymagań dotyczących niezależności danych. W takich przypadkach węzeł geografii jest zbędny.
- Niektóre firmy wolą dodatkowo dzielić środowiska programistyczne, testowe i kontroli jakości na oddzielne subskrypcje.
- Gdy firma integruje zespół Cloud Center of Excellence (CCoE), subskrypcje usług udostępnionych na poszczególnych węzłach geografii mogą zmniejszyć liczbę zduplikowanych zasobów.
- Nakłady pracy związane z wdrażaniem na mniejszą skalę mogą obejmować mniejszą hierarchię zarządzania. Można często zobaczyć jeden węzeł główny dla firmowego działu informatycznego z jednym poziomem węzłów podrzędnych w hierarchii dla różnych środowisk. Nie stanowi to naruszenia najlepszych rozwiązań dla dobrze zarządzanego środowiska. Jednak utrudnia to zapewnienie modelu dostępu z najmniejszymi prawami do kontroli kosztów i innych ważnych funkcji.

W pozostałej części tego artykułu przyjęto, że użyto najlepszego rozwiązania na diagramie powyżej. Jednak artykuły poniżej mogą pomóc w zastosowaniu tego rozwiązania do organizacji zasobów, która najlepiej pasuje do Twojej firmy:

- [Scaling with multiple Azure subscriptions](../considerations/scaling-subscriptions.md) (Skalowanie za pomocą wielu subskrypcji platformy Azure)
- [Deploying a Governance MVP to govern well-managed environment standards](../../govern/guides/complex/index.md) (Wdrażanie ładu programu MVP w celu nadzorowania standardów dobrze zarządzanego środowiska)

## <a name="provide-the-right-level-of-cost-access"></a>Zapewnienie odpowiedniego poziomu dostępu do kosztów

Zarządzanie kosztami to wysiłek zespołowy. W sekcji dotyczącej gotowości organizacji struktury Cloud Adoption Framework określono niewielką liczbę głównych zespołów oraz opisano, jak te zespoły wspierają nakłady pracy związane z wdrażaniem chmury. W tym artykule poszerzono definicje zespołów, aby określić zakres i role, które mają zostać przypisane do członków poszczególnych zespołów w celu uzyskania odpowiedniego poziomu widoczności danych dotyczących zarządzania kosztami.

- *Role* określają, co użytkownik może zrobić z różnymi zasobami.
- *Zakres* określa, w przypadku których zasobów użytkownik może podjąć te działania (użytkownik, grupa, jednostka usługi lub tożsamość zarządzana).

Najlepszym rozwiązaniem jest zaproponowanie modelu z najmniejszymi uprawnieniami podczas przypisywania osób do różnych ról i zakresów.

### <a name="roles"></a>Role

Usługa Azure Cost Management obsługuje następujące wbudowane role dla poszczególnych zakresów:

- [Właściciel](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner). Może wyświetlać koszty i wszystkim zarządzać, m.in. konfiguracją kosztów.
- [Współautor](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Może wyświetlać koszty i wszystkim zarządzać, m.in. konfiguracją kosztów, ale z wyłączeniem kontroli dostępu.
- [Czytelnik](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader). Może wszystko wyświetlać, m.in. dane dotyczące kosztów i konfigurację, ale nie może wprowadzać żadnych zmian.
- [Współautor zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor). Może wyświetlać koszty i zarządzać konfiguracją kosztów.
- [Czytelnik zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) może wyświetlać dane i konfigurację kosztów.

Najlepszym rozwiązaniem jest przypisanie członkom wszystkich zespołów roli współautora zarządzania kosztami. Ta rola zapewnia dostęp niezbędny do tworzenia budżetów i eksportów oraz zarządzania nimi w celu skuteczniejszego monitorowania i tworzenia raportów kosztów. Jednak członkowie [zespołu ds. strategii chmury](../../organize/cloud-strategy.md) powinni mieć tylko rolę czytelnika zarządzania kosztami. Wynika to z faktu, że nie zajmują się oni ustalaniem budżetów w narzędziu usługi Azure Cost Management.

### <a name="scope"></a>Scope

Poniższe ustawienia zakresu i ról zapewnią niezbędną widoczność w zakresie zarządzania kosztami. To najlepsze rozwiązanie może wymagać drobnych zmian w celu dostosowania do decyzji związanych z organizacją zasobów.

- [Zespół ds. wdrażania chmury](../../organize/cloud-adoption.md). Odpowiedzialność za bieżące zmiany w optymalizacji wymaga uprawnień dostępu współautora zarządzania kosztami na poziomie grupy zasobów.

  - **Środowisko pracy**. Zespół ds. wdrażania chmury powinien już mieć przynajmniej dostęp [współautora](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) do wszystkich grup zasobów, których to dotyczy, lub przynajmniej grup związanych z działaniami tworzenia/testowania lub bieżącego wdrażania. Nie jest wymagane żadne dodatkowe ustawienie zakresu.
  - **Środowiska produkcyjne**. Jeśli podział odpowiedzialności zostanie dobrze zaplanowany, zespół ds. wdrażania chmury prawdopodobnie nie będzie miał już dostępu do grup zasobów związanych ze swoimi projektami. Grupy zasobów, które obsługują wystąpienia produkcyjne swoich obciążeń, będą potrzebować dodatkowego zakresu, aby udzielić temu zespołowi dostępu do wpływu, jaki mają te decyzje na koszty produkcji. Ustawienie zakresu [współautora zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) dla produkcyjnych grup zasobów dla tego zespołu umożliwi zespołowi monitorowanie kosztów i ustalanie budżetów na podstawie użycia i bieżącej inwestycji w obsługiwane obciążenia.

- [Zespół ds. strategii chmury](../../organize/cloud-strategy.md). Obowiązek śledzenia kosztów w wielu projektach i jednostkach biznesowych wymaga, by czytelnik zarządzania kosztami miał na poziomie głównym dostęp do hierarchii grupy zarządzania.

  - Nadaj [czytelnikowi zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) dostęp do tego zespołu w grupie zarządzania. Zapewni to stały dostęp do wszystkich wdrożeń skojarzonych z subskrypcjami objętymi tą hierarchią grupy zarządzania.

- [Zespół ds. zarządzania w chmurze](../../organize/cloud-governance.md). Obowiązki związane z zarządzaniem kosztami, dostosowaniem budżetu i raportowaniem we wszystkich nakładach pracy związanych z wdrażaniem powodują, że współautor zarządzania kosztami powinien mieć dostęp na poziomie głównym do hierarchii grupy zarządzania.

  - W dobrze zarządzanym środowisku zespół ds zarządzania w chmurze ma już prawdopodobnie wyższy poziom dostępu, co sprawia, że dodatkowe przypisanie zakresu do [współautora zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) jest zbędne.

- [Cloud Center of Excellence](../../organize/cloud-center-of-excellence.md). Odpowiedzialność za zarządzanie kosztami związanymi z udostępnionymi usługami wymaga, aby współautor zarządzania kosztami miał dostęp na poziomie subskrypcji. Ponadto zespół ten może wymagać, by współautor zarządzania kosztami miał dostęp do grup zasobów lub subskrypcji zawierających zasoby wdrożone przy użyciu automatyzacji CCoE, aby zrozumieć, jak ta automatyzacja wpływa na koszty.

  - **Usługi udostępnione**. W przypadku zaangażowania zespołu Cloud Center of Excellence najlepszym rozwiązaniem jest, by zasoby zarządzane przez CCoE były obsługiwane ze scentralizowanej subskrypcji na usługi udostępnione w ramach modelu układu gwiaździstego. W tym scenariuszu zespół CCoE ma prawdopodobnie dostęp do tej subskrypcji w roli współautora lub właściciela, co sprawia, że dodatkowe przypisanie do zakresu [współautora zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) jest zbędne.
  - **Automatyzacja i sterowanie przez zespół CCoE**. Zespół CCoE często zapewnia sterowanie i skrypty wdrażania automatycznego zespołom ds. wdrażania chmury. Zespół CCoE ma obowiązek wiedzieć, jaki wpływ mają te akceleratory na koszty. Aby uzyskać taką widoczność, zespół potrzebuje dostępu w roli [współautora zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) do grup zasobów lub subskrypcji, na których działają te akceleratory.

- **Zespół ds. operacji w chmurze**. Odpowiedzialność za zarządzanie bieżącymi kosztami środowisk produkcyjnych wymaga dostępu w roli współautora zarządzania kosztami do wszystkich subskrypcji produkcyjnych.

  - Ogólne zalecenie umieszcza zasoby produkcyjne i nieprodukcyjne w osobnych subskrypcjach, które podlegają węzłom hierarchii grupy zarządzania skojarzonym ze środowiskami produkcyjnymi. W dobrze zarządzanym środowisku członkowie zespołu operacyjnego prawdopodobnie mają już dostęp do subskrypcji produkcyjnych w roli właściciela lub współautora, co sprawia, że rola [współautora zarządzania kosztami](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) staje się zbędna.

## <a name="additional-cost-management-resources"></a>Dodatkowe zasoby związane z zarządzaniem kosztami

Usługa Azure Cost Management to dobrze udokumentowane narzędzie do ustalania budżetów i uzyskiwania wglądu w koszty chmury na platformie Azure lub AWS. Po ustanowieniu dostępu do dobrze zarządzanej hierarchii środowiska następujące artykuły mogą ułatwić korzystanie z tego narzędzia w celu monitorowania i kontrolowania kosztów.

### <a name="get-started-with-azure-cost-management"></a>Wprowadzenie do usługi Azure Cost Management

Aby uzyskać więcej informacji na temat rozpoczynania pracy z usługą Azure Cost Management, zobacz temat [How to optimize your cloud investment with Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json) (Jak zoptymalizować inwestycję w chmurę przy użyciu usługi Azure Cost Management).

### <a name="use-azure-cost-management"></a>Korzystanie z usługi Azure Cost Management

- [Tworzenie budżetów i zarządzanie nimi](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets)
- [Eksportowanie danych kosztów](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data)
- [Optymalizowanie kosztów na podstawie rekomendacji](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Monitorowanie użycia i wydatków za pomocą alertów o kosztach](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending)

### <a name="use-azure-cost-management-to-govern-aws-costs"></a>Użycie usługi Azure Cost Management do zarządzania kosztami AWS

- [Integracja raportów o kosztach i użyciu AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-set-up-configure)
- [Zarządzanie kosztami AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-manage)

### <a name="establish-access-roles-and-scope"></a>Ustanawianie dostępu, ról i zakresu

- [Informacje o zakresie zarządzania kosztami](https://docs.microsoft.com/azure/cost-management/understand-work-scopes)
- [Ustawianie zakresu dla grupy zasobów](https://docs.microsoft.com/azure/role-based-access-control/quickstart-assign-role-user-portal)
