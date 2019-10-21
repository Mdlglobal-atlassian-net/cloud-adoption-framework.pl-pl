---
title: 'Innowacje w chmurze: Zaangażuj aplikacje'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — Zaangażuj aplikacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/24/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5dcfbc34c31346b4efada049fc46effac149cd68
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72557260"
---
# <a name="engage-through-applications"></a>Zaangażuj aplikacje

Zgodnie z opisem w artykule dotyczącym [danych democratizing](./data.md), dane są nową olejem. Paliwa IT są najbardziej innowacje w całej sieci cyfrowej. W przypadku tego analogu aplikacje są stacjami paliw i infrastrukturami wymaganymi do uzyskania tego paliwa w odpowiednich rąk.

W niektórych przypadkach dane są wystarczające do zmiany dysku i zaspokajania potrzeb klientów. Zwykle rozwiązanie do potrzeb klientów będzie wymagało zastosowania aplikacji do kształtowania danych i utworzenia środowiska. Aplikacje są sposobem, w jaki udostępniamy użytkownika. Są one domem dla procesów wymaganych do reagowania na wyzwalacze klientów. Są to klienci, którzy chcą dostarczać dane i otrzymywać wskazówki. W tym artykule opisano kilka zasad, które będą pomocne w dostosowywaniu właściwych rozwiązań aplikacji w oparciu o te, które mają zostać sprawdzone.

## <a name="shared-code"></a>Udostępniony kod

Zespół, który może szybciej i dokładnie reagować na Opinie klientów, zmiany rynkowe oraz szanse na innowacje, będzie prowadzić do innowacji na rynku. Pierwsza zasada innowacyjnych aplikacji została zakreślona w [omówieniu wzrostu sposób myślenia](./learn.md#growth-mindset), "Udostępnij kod". Innowacje w czasie mogą pochodzić tylko z punktu skupienia na kulturze. W celu utrzymania innowacji wymagane są różne perspektywy i wkłady.

Aby zapewnić gotowość do innowacji, cały rozwój aplikacji powinien rozpoczynać się od udostępnionego repozytorium kodu. Najbardziej typowym narzędziem do zarządzania repozytoriami kodu jest [GitHub](https://guides.github.com/), który umożliwia tworzenie repozytorium udostępnionego kodu za pomocą kilku kliknięć. Alternatywnie funkcja [Azure Repos](/azure/devops/repos/get-started/what-is-repos?view=azure-devops) platformy Azure DevOps może służyć do tworzenia repozytorium [git](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git) lub [Team Foundation](/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc) .

## <a name="citizen-developers"></a>Deweloperzy deweloperów

Profesjonalni deweloperzy są istotnym składnikiem innowacji. Gdy hipoteza zawiedzie dokładnie na dużą skalę, Profesjonalni deweloperzy są zobowiązani do stabilizacji i przygotowania rozwiązania do skalowania. Większość zasad, do których odwołuje się ten artykuł, będzie wymagała wsparcia dla profesjonalnych deweloperów. Niestety bieżące trendy sugerują, że istnieje więcej otwartych rozwiązań dla profesjonalnych deweloperów, a następnie istnieją deweloperzy. Dodatkowo koszt i tempo innowacji mogą być mniej korzystne, gdy wymagane jest rigors programowanie profesjonalne. Deweloperzy deweloperów umożliwiają skalowanie wysiłków programistycznych i przyspieszenie testowania wczesnej hipotez.

Deweloperzy deweloperów mogą być niezależni, gdy wczesne poprawność można zweryfikować przy użyciu narzędzi, takich jak [powerapps](https://docs.microsoft.com/powerapps/powerapps-overview) dla interfejsów aplikacji, [Konstruktor AI](/powerapps/use-ai-builder) dla procesów i prognoz, [Microsoft Flow](https://docs.microsoft.com/flow) dla przepływów pracy lub [Power BI](https://docs.microsoft.com/power-bi) dla danych wyrażon.

> [!NOTE]
> W przypadku korzystania z nich deweloperzy mogą testować, że profesjonalne deweloperzy zapewniają pomoc techniczną, przegląd i wskazówki. Po sprawdzeniu hipotezy na dużą skalę proces przejścia aplikacji do bardziej niezawodnego modelu programowania przyspieszy powracanie do innowacji. Dzięki profesjonalnym deweloperom w ramach wczesnych definicji procesów mogą wystąpić późniejsze przejścia.

## <a name="modern-web-experiences"></a>Nowoczesne środowiska sieci Web

Gdy aplikacja lub środowisko jest wymagane do zaspokajania potrzeb klientów, nowoczesne aplikacje sieci Web mogą być najszybszym sposobem na spełnienie tego zapotrzebowania. Nowoczesne środowiska sieci Web mogą szybko współpracować z klientami wewnętrznymi lub zewnętrznymi i umożliwiać szybką iterację rozwiązania.

Azure App Service zapewnia środowisko hostingu dla aplikacji, które usuwają obciążenie związane z zarządzaniem infrastrukturą i stosowaniem poprawek systemu operacyjnego. Zapewnia automatyzację skalowania, aby zaspokoić wymagania użytkowników, ale jest powiązany przez zdefiniowane limity, aby zachować koszty kontroli. App Service zapewnia obsługę pierwszej klasy dla języków takich jak ASP.NET, ASP.NET Core, Java, Ruby, Node. js, PHP lub Python. Jeśli istnieje potrzeba hostowania innego stosu środowiska uruchomieniowego, aplikacja sieci Web dla kontenera oferuje możliwość szybkiego i łatwego hostowania kontenera Docker w środowisku App Service, aby umożliwić hostowanie niestandardowego stosu kodu w środowisku, w którym znajduje się serwer Busin ES.

## <a name="cloud-native-solutions"></a>Rozwiązania natywne w chmurze

Natywne aplikacje w chmurze są kompilowane od podstaw. Natywne aplikacje w chmurze są zoptymalizowane pod kątem skalowania i wydajności w chmurze. Aplikacje natywne w chmurze są zwykle tworzone przy użyciu mikrousług, bezserwerowych, opartych na zdarzeniach lub opartych na kontenerach. Najczęściej natywne rozwiązania w chmurze wykorzystują kombinację architektur mikrousług, usług zarządzanych i ciągłego dostarczania, aby osiągnąć niezawodność i krótszy czas wprowadzenia na rynek.

Natywne rozwiązanie w chmurze umożliwia scentralizowanym zespołom programistycznym zachowanie kontroli nad logiką biznesową, bez konieczności stosowania scentralizowanych rozwiązań. Ten typ rozwiązania tworzy również kotwicę, aby zapewnić spójność dla deweloperów i nowoczesnych środowisk. Na koniec rozwiązania do obsługi chmurowej zapewniają akcelerator innowacyjny, zwalniając obywateli i profesjonalnych deweloperów do bezpiecznego wprowadzania innowacji i z minimalnymi blokadami.

## <a name="innovate-through-existing-solutions"></a>Wprowadzanie innowacji przez istniejące rozwiązania

Wiele postanowień klienta można najlepiej dostarczyć przez nowoczesne wersje istniejącego rozwiązania. Gdy bieżąca logika biznesowa spełnia potrzeby klientów (lub jest naprawdę blisko), można przyspieszyć innowacje, kompilując je na podstawie nowoczesnego rozwiązania.

Większość form modernizacji, w tym niewielkie Refaktoryzacja aplikacji, jest uwzględniona w [metodologii migracji](../../migrate/index.md) w ramach struktury wdrażania chmury. Ta metodologia prowadzi zespoły do wdrażania rozwiązań chmurowych poprzez procesy umożliwiające Migrowanie sieci [cyfrowych](../../digital-estate/index.md) do chmury. [Przewodnik migracji platformy Azure](../../migrate/azure-migration-guide/index.md) zapewnia usprawnione podejście do tej samej metodologii, która jest odpowiednia dla niewielkiej liczby obciążeń lub nawet pojedynczej aplikacji.

Po przeprowadzeniu migracji i modernizacji istnieją różne sposoby wykorzystania rozwiązania podczas tworzenia nowych innowacyjnych rozwiązań dla potrzeb klientów. Na przykład [deweloperzy deweloperów](#citizen-developers) mogą testować jednostronne aplikacje lub profesjonalne deweloperzy mogą tworzyć [nowoczesne środowiska internetowe](#modern-web-experiences) lub [natywne rozwiązania w chmurze](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Zwiększ istniejące rozwiązanie

Rozszerzanie rozwiązania to jedna powszechna forma modernizacji. Takie podejście może być najszybszą ścieżką do innowacyjności, gdy następujące są prawdziwe hipotezy klienta:

- Istniejąca logika biznesowa powinna być zgodna z istniejącym klientem i musi być bliska.
- Ulepszone środowisko będzie lepiej spełniało potrzeby określonego klienta kohorta.
- Logika biznesowa wymagana przez rozwiązanie MVP jest scentralizowana, zwykle za pośrednictwem [N-warstwowego](/azure/architecture/guide/architecture-styles/n-tier), usług sieci Web, interfejsów API i [mikrousług](/azure/architecture/guide/architecture-styles/microservices) . Takie podejście polega na zapakowaniu istniejące rozwiązanie z nowym doświadczeniem hostowanym w chmurze. Na platformie Azure to rozwiązanie prawdopodobnie będzie aktywne na platformie Azure App Services.

### <a name="rebuild-an-existing-solution"></a>Kompiluj ponownie istniejące rozwiązanie

Jeśli aplikacja nie może być łatwo rozszerzona, może być konieczne Refaktoryzacja rozwiązania. W tym podejściu obciążenie zostanie zmigrowane do chmury. Po migracji części aplikacji są modyfikowane lub duplikowane jako usługi sieci Web lub [mikrousługi](/azure/architecture/guide/architecture-styles/microservices), które są wdrażane równolegle z istniejącym rozwiązaniem. Rozwiązanie oparte na usługach równoległych może być traktowane jak rozszerzone rozwiązanie. To rozwiązanie po prostu otacza istniejące rozwiązanie nowym środowiskom hostowanym w chmurze. Na platformie Azure to rozwiązanie prawdopodobnie będzie aktywne na platformie Azure App Services.

> [!CAUTION]
> Refaktoryzacja/rearchitektura rozwiązań lub scentralizowana logika biznesowa może szybko stać się czasochłonnym wzrostem [technicznym](./build.md#reduce-complexity-and-delay-technical-spikes), w przeciwieństwie do źródła wartości klienta. Jest to ryzykowne dla innowacji, szczególnie wczesne w przypadku weryfikacji hipotez. Mając nieco dużo kreatywności w projektowaniu rozwiązania, powinna istnieć ścieżka do programu MVP, która nie wymaga refaktoryzacji istniejących rozwiązań. Należy opóźnić refaktoryzację, dopóki nie zostanie sprawdzona Poprzednia hipoteza w odpowiedniej skali.

## <a name="operating-model-innovations"></a>Innowacje modelu operacyjnego

Poza nowoczesnymi innowacyjnymi podejścia do tworzenia aplikacji wprowadzono innowacje dotyczące operacji na aplikacjach. Podejścia zostały zduplikowane w wielu przesunięciach organizacyjnych. Jednym z najbardziej widocznych elementów jest przenoszenie modeli operacyjnych usługi [Cloud Center](../../organize/cloud-center-of-excellence.md) . W pełni zatrudnione i dojrzałe zespoły biznesowe mają możliwość zapewnienia własnej obsługi operacyjnej rozwiązania.

Typ samoobsługowego modelu zarządzania operacyjnego, który znajduje się w centrum analiz doskonałości, umożliwia ściślejsze kontrolki i szybsze iteracje w środowisku rozwiązania. Jest to realizowane przez przeniesienie kontroli operacyjnej i odpowiedzialności do zespołu biznesowego.

Gdy celem jest skalowanie lub zaspokajanie globalnego zapotrzebowania na istniejące rozwiązanie, takie podejście może być wystarczające do zweryfikowania hipotezy klienta. Po przeprowadzeniu migracji i niewielkiej modernizacji zespół biznesowy będzie miał możliwość skalowania rozwiązań w celu przetestowania różnorodnych postanowień dotyczących kohorty klientów, którzy są zainteresowani wydajnością, dystrybucją globalną lub innymi niezbędnymi potrzebami klientów składowa.

## <a name="reduce-overhead-and-management"></a>Zmniejszenie kosztów i zarządzania

Im większa jest obsługa w rozwiązaniu, tym wolniejsze rozwiązanie będzie się powtarzać. Przyspieszenie innowacji przez zredukowanie liczby operacji wpływa na dostępną szybkość.

Aby przygotować się do wielu iteracji wymaganych do dostarczenia innowacyjnego rozwiązania, ważne jest, aby wziąć pod uwagę. Minimalizacja obciążeń operacyjnych na początku procesu przez preferowanie opcji bezserwerowych.

Na platformie Azure Opcje aplikacji bezserwerowych mogą obejmować [Azure App Service](https://docs.microsoft.com/azure/app-service/overview), [Service Fabric](https://docs.microsoft.com/azure/architecture/example-scenario/infrastructure/service-fabric-microservices), [kontenery](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql)itp.

Równolegle platforma Azure zapewnia opcje danych transakcji bezserwerowych, co również zmniejsza obciążenie. [Lista produkty bazy danych](https://docs.microsoft.com/azure/#pivot=products&panel=databases) zawiera opcje hostingu danych bez konieczności stosowania pełnej platformy danych.

## <a name="next-steps"></a>Następne kroki

W zależności od hipotez i rozwiązania zasady w tym artykule mogą pomóc w projektowaniu aplikacji, które spełniają definicje MVP i angażują użytkowników. Dalej są to zasady umożliwiające [przyjęcie](./ci-cd.md)rozwiązań, które pozwolą na szybsze pobieranie aplikacji i danych do klientów.

> [!div class="nextstepaction"]
> [Przyjęcie akceptacji](./ci-cd.md)
