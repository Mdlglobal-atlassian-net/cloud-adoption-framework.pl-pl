---
title: Powiąż za pośrednictwem aplikacji do roznalazeków cyfrowych
description: Zapoznaj się z tematem tworzenie rozwiązań aplikacji do tworzenia kształtów i tworzenie środowisk, które angażują klientów i wspierają innowacje.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: cede336255183abec06311137abfe4e023116c03
ms.sourcegitcommit: 0ea426f2f471eb7310c6f09478be1306cf7bf0d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78341780"
---
# <a name="engage-through-applications"></a>Zaangażuj aplikacje

Zgodnie z opisem w [zdemokratyzuj proces danych](./data.md), dane są nową olejem. Paliwa IT są najbardziej innowacje w całej sieci cyfrowej. W przypadku tego analogu aplikacje są stacjami paliw i infrastrukturą wymaganą do uzyskania tego paliwa w odpowiednich rąk.

W niektórych przypadkach same dane są wystarczające do zmiany dysku i zaspokajania potrzeb klientów. Ogólnie, jednak rozwiązania dla klientów wymagają, aby aplikacje miały kształtować dane, i utworzyć środowisko. Aplikacje są sposobem, w jaki udostępniamy użytkownika. Są one domem dla procesów wymaganych do reagowania na wyzwalacze klientów. Są one odbiorcami, aby zapewnić dane i uzyskać wskazówki. Ten artykuł zawiera podsumowanie kilku zasad, które mogą pomóc w rozwiązaniu użytkownika z odpowiednim rozwiązaniem aplikacji w oparciu o te, które mają być zweryfikowane.

![Angażowanie przez aplikacje](../../_images/innovate/engage-via-apps.png)

## <a name="shared-code"></a>Udostępniony kod

Zespoły, które szybciej i dokładnie reagują na Opinie klientów, zmiany rynkowe i okazje do innowacji zazwyczaj prowadzą do innowacji na rynku. Pierwsza zasada innowacyjnych aplikacji jest sumowana w [omówieniu wzrostu sposób myślenia](./learn.md#growth-mindset): "Udostępnij kod". W miarę upływu czasu innowacje są skoncentrowane na skoncentrowaniu się na kulturze. Aby utrzymać innowacje, wymagane są różne perspektywy i wkłady.

Aby zapewnić gotowość do innowacji, cały rozwój aplikacji powinien rozpoczynać się od udostępnionego repozytorium kodu. Najczęściej przyjętym narzędziem do zarządzania repozytoriami kodu jest [GitHub](https://guides.github.com), co pozwala szybko utworzyć udostępnione repozytorium kodu. Alternatywnie, [Azure Repos](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops) to zestaw narzędzi do kontroli wersji w programie Azure DevOps Services, których można użyć do zarządzania kodem. Azure Repos zapewnia dwa typy kontroli wersji:

- [Git](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#git): rozproszony system kontroli wersji
- [Kontrola wersji serwera Team Foundation (TFVC)](https://docs.microsoft.com/azure/devops/repos/get-started/what-is-repos?view=azure-devops#tfvc): scentralizowany system kontroli wersji

## <a name="citizen-developers"></a>Amatorscy deweloperzy

Profesjonalni deweloperzy są istotnym składnikiem innowacji. Gdy hipoteza zawiedzie dokładnie na dużą skalę, Profesjonalni deweloperzy są zobowiązani do stabilizacji i przygotowania rozwiązania do skalowania. Większość zasad, do których odwołuje się ten artykuł, wymaga wsparcia dla profesjonalnych deweloperów. Niestety bieżące trendy sugerują, że w przypadku deweloperów korzystających z oprogramowania dla profesjonalistów nie są deweloperzy. Ponadto koszt i tempo innowacji mogą być mniej korzystne, gdy profesjonalne programowanie jest uznawane za niezbędne. W odpowiedzi na te wyzwania deweloperzy deweloperów umożliwiają skalowanie wysiłków programistycznych i przyspieszenie testowania hipotezy wczesnej.

Wykorzystanie deweloperów może być opłacalne i skuteczne, gdy wczesne poprawność może być zweryfikowana za pomocą narzędzi takich jak [powerapps](https://docs.microsoft.com/powerapps/powerapps-overview) dla interfejsów aplikacji, [Konstruktor AI](https://docs.microsoft.com/powerapps/use-ai-builder) dla procesów i prognoz, [Microsoft Flow](https://docs.microsoft.com/flow) dla przepływów pracy i [Power BI](https://docs.microsoft.com/power-bi) do zużycia danych.

> [!NOTE]
> Gdy polegasz na programistach deweloperów do testowania form, zaleca się, aby niektórzy Profesjonalni deweloperzy mogli zapewnić pomoc techniczną, przegląd i wskazówki. Po sprawdzeniu hipotezy na dużą skalę proces przenoszenia aplikacji do bardziej niezawodnego modelu programowania przyspieszy powracanie do innowacji. W przypadku wczesnych deweloperów w definicjach procesów możesz w późniejszym czasie korzystać z przejść.

## <a name="intelligent-experiences"></a>Inteligentne środowiska

Inteligentne środowiska łączą szybkość i skalę nowoczesnych aplikacji sieci Web dzięki analizie usług poznawczych i botów. Sama każda z tych technologii może być wystarczająca do zaspokajania potrzeb klientów. W przypadku, gdy są one inteligentne, rozszerzają spektrum potrzeb, które mogą być zaspokajane przez środowisko cyfrowe, jednocześnie pomagając w rozwiązaniu kosztów deweloperskich.

### <a name="modern-web-apps"></a>Nowoczesne aplikacje internetowe

Gdy aplikacja lub środowisko jest wymagane do spełnienia potrzeby klienta, nowoczesne aplikacje sieci Web mogą być najszybszym sposobem na przechodzenie. Nowoczesne środowiska sieci Web mogą szybko współpracować z klientami wewnętrznymi lub zewnętrznymi i umożliwiać szybką iterację rozwiązania.

### <a name="infusing-intelligence"></a>Dodawanie inteligencji

Dostęp do uczenia maszynowego i sztucznej analizy jest coraz większy dla deweloperów. Szerokie udostępnienie wspólnych interfejsów API za pomocą funkcji predykcyjnych pozwala deweloperom lepiej spełnić wymagania klienta dzięki rozszerzonemu dostępowi do danych i prognoz.

Dodanie analizy do rozwiązania może umożliwić zamianę mowy na tekst, tłumaczenie tekstu, obsługę komputera, a nawet Wyszukiwanie wizualne. Dzięki tym rozszerzonym funkcjom deweloperzy mogą tworzyć rozwiązania, które wykorzystują inteligencję do tworzenia interaktywnego i nowoczesnego środowiska.

### <a name="bots"></a>Botów

Botów zapewniają środowisko, które może być mniej podobne do korzystania z komputera i bardziej przypominające pracę z osobą — co najmniej z inteligentnym robotem. Mogą one służyć do przesuwania prostych, powtarzalnych zadań (takich jak rezerwacja na obiad lub gromadzenie informacji o profilu) do zautomatyzowanych systemów, które mogą nie wymagać bezpośredniej interwencji ludzkiej. Użytkownicy z bot za pomocą tekstu, kart interaktywnych i mowy. Interakcja bot może przedziałować od szybkiego pytania i odpowiedzi na zaawansowaną konwersację, która inteligentnie zapewnia dostęp do usług.

Botów to wiele takich jak nowoczesne aplikacje sieci Web: są one aktywne w Internecie i używają interfejsów API do wysyłania i odbierania wiadomości. Zawartość bot różni się znacznie w zależności od rodzaju bot. Nowoczesne oprogramowanie bot opiera się na stosie technologii i narzędzi, które zapewniają coraz bardziej skomplikowane środowiska na różnych platformach. Jednak proste bot może po prostu odebrać komunikat i odtworzyć go z powrotem do użytkownika przy użyciu bardzo małego kodu.

Botów mogą wykonywać te same czynności co w przypadku innych typów oprogramowania: odczytywanie i zapisywanie plików, korzystanie z baz danych i interfejsów API oraz obsługę zwykłych zadań obliczeniowych. Dzięki temu botów się, że używają mechanizmów ogólnie zarezerwowanych do komunikacji między ludźmi i ludźmi.

## <a name="cloud-native-solutions"></a>Rozwiązania natywne w chmurze

Aplikacje natywne w chmurze są kompilowane od podstaw i są zoptymalizowane pod kątem skalowania i wydajności w chmurze. Aplikacje natywne w chmurze są zwykle tworzone przy użyciu mikrousług, bezserwerowych, opartych na zdarzeniach lub opartych na kontenerach. W większości przypadków natywne rozwiązania w chmurze wykorzystują kombinację architektur mikrousług, usług zarządzanych i ciągłego dostarczania, aby osiągnąć niezawodność i krótszy czas wprowadzenia na rynek.

Natywne rozwiązanie w chmurze umożliwia scentralizowanym zespołom programistycznym zachowanie kontroli nad logiką biznesową bez konieczności stosowania monolitycznych, scentralizowanych rozwiązań. Ten typ rozwiązania tworzy również kotwicę, aby zapewnić spójność w zakresie danych na potrzeby deweloperów i nowoczesnych środowisk. Dzięki rozwiązaniom macierzystym w chmurze można korzystać z akceleratora innowacji, zwalniając przez deweloperów i profesjonalę specjalistów do bezpiecznego wprowadzania innowacji i z minimalnymi blokowaniem.

## <a name="innovate-through-existing-solutions"></a>Wprowadzanie innowacji przez istniejące rozwiązania

Wiele postanowień klienta można najlepiej dostarczyć przez nowoczesne wersje istniejącego rozwiązania. Gdy bieżąca logika biznesowa spełnia potrzeby klientów (lub jest naprawdę blisko), może być możliwe przyspieszenie innowacji przez skompilowanie w oparciu o nowoczesne rozwiązanie.

Większość form modernizacji, w tym niewielkie Refaktoryzacja aplikacji, jest uwzględniona w [metodologii migracji](../../migrate/index.md) w ramach struktury wdrażania chmury. Ta metodologia prowadzi zespoły do wdrażania rozwiązań chmurowych przez proces migrowania sieci [cyfrowej](../../digital-estate/index.md) do chmury. [Przewodnik migracji platformy Azure](../../migrate/azure-migration-guide/index.md) zapewnia usprawnione podejście do tej samej metodologii, która jest odpowiednia dla niewielkiej liczby obciążeń lub nawet pojedynczej aplikacji.

Po przeprowadzeniu migracji i modernizacji rozwiązania istnieją różne sposoby tworzenia nowych, innowacyjnych rozwiązań dla potrzeb klientów. Na przykład [deweloperzy deweloperów](#citizen-developers) mogą testować założenia lub profesjonalne deweloperzy mogą tworzyć [inteligentne środowiska](#intelligent-experiences) lub [natywne rozwiązania w chmurze](#cloud-native-solutions).

### <a name="extend-an-existing-solution"></a>Zwiększ istniejące rozwiązanie

Rozszerzanie rozwiązania to jedna powszechna forma modernizacji. Takie podejście może być najszybszą ścieżką do innowacyjności, gdy następujące są prawdziwe hipotezy klienta:

- Istniejąca logika biznesowa powinna być zgodna z istniejącym klientem i musi być bliska.
- Ulepszone środowisko będzie lepiej spełniało potrzeby określonego klienta kohorta.
- Logika biznesowa wymagana przez rozwiązanie o minimalnym żywotnym wykorzystaniu produktu (MVP) jest scentralizowana, zazwyczaj za pośrednictwem platformy [N-warstwowej](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), usług sieci Web, interfejsów API i [mikrousług](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices) . Takie podejście polega na zapakowaniu istniejące rozwiązanie w ramach nowego środowiska hostowanego w chmurze. Na platformie Azure to rozwiązanie prawdopodobnie będzie aktywne na platformie Azure App Services.

### <a name="rebuild-an-existing-solution"></a>Kompiluj ponownie istniejące rozwiązanie

Jeśli aplikacja nie może być łatwo rozszerzona, może być konieczne Refaktoryzacja rozwiązania. W tym podejściu obciążenie zostanie zmigrowane do chmury. Po migracji aplikacji części tego elementu są modyfikowane lub duplikowane jako usługi sieci Web lub [mikrousługi](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices), które są wdrażane równolegle z istniejącym rozwiązaniem. Rozwiązanie oparte na usługach równoległych może być traktowane jak rozszerzone rozwiązanie. To rozwiązanie po prostu otacza istniejące rozwiązanie nowym środowiskom hostowanym w chmurze. Na platformie Azure to rozwiązanie prawdopodobnie będzie aktywne na platformie Azure App Services.

> [!CAUTION]
> Refaktoryzacja lub rearchitektura rozwiązań lub scentralizowana logika biznesowa może szybko wyzwolić czasochłonne przeznaczenie [techniczne](./build.md#reduce-complexity-and-delay-technical-spikes)zamiast źródła wartości klienta. Jest to ryzykowne dla innowacji, szczególnie wczesne w przypadku weryfikacji hipotez. Mając nieco dużo kreatywności w projektowaniu rozwiązania, powinna istnieć ścieżka do programu MVP, która nie wymaga refaktoryzacji istniejących rozwiązań. Można opóźnić refaktoryzację do momentu, gdy hipoteza wstępna zostanie zweryfikowana na dużą skalę.

## <a name="operating-model-innovations"></a>Innowacje modelu operacyjnego

Oprócz nowoczesnych innowacyjnych metod tworzenia aplikacji w *operacjach*aplikacji wprowadzono znaczące innowacje. Te podejścia zostały zduplikowane w wielu przesunięć organizacyjnych. Jednym z najbardziej widocznych jest usługa [Cloud Center z](../../organize/cloud-center-of-excellence.md) modelem operacyjnym. W pełni zatrudnione i dojrzałe zespoły biznesowe mają możliwość zapewnienia własnej obsługi operacyjnej rozwiązania.

Typ samoobsługowego modelu zarządzania operacyjnego, który znajduje się w centrum rozwiązań w chmurze, umożliwia ściślejsze kontrolki i szybsze iteracje w środowisku rozwiązania. Cele te są realizowane przez przeniesienie kontroli operacyjnej i odpowiedzialności do zespołu biznesowego.

Jeśli próbujesz skalować lub spełnić globalne zapotrzebowanie na istniejące rozwiązanie, takie podejście może być wystarczające do zweryfikowania hipotezy klienta. Po przeprowadzeniu migracji i niewielkiej modernizacji rozwiązania zespół biznesowy może go skalować w celu przetestowania różnorodnych zabiegów. Zazwyczaj obejmują one kohorty klientów, którzy są zainteresowani wydajnością, dystrybucją globalną i innymi potrzebami klientów.

## <a name="reduce-overhead-and-management"></a>Zmniejszenie kosztów i zarządzania

Im większa jest obsługa w rozwiązaniu, tym wolniejsze rozwiązanie będzie się powtarzać. Oznacza to, że można przyspieszyć innowacje, zmniejszając wpływ operacji na dostępną przepustowość.

Aby przygotować się do wielu iteracji wymaganych do dostarczenia innowacyjnego rozwiązania, ważne jest, aby myśleć. Na przykład zminimalizować obciążenia operacyjne wczesne w procesie przez preferowanie opcji bezserwerowych. Na platformie Azure Opcje aplikacji bezserwerowych mogą zawierać [Azure App Service](https://docs.microsoft.com/azure/app-service/overview) lub [kontenery](https://docs.microsoft.com/azure/architecture/cloud-adoption/migrate/azure-best-practices/contoso-migration-rearchitect-container-sql).

Równolegle, platforma Azure zapewnia opcje danych transakcji bezserwerowych, które również zmniejszają koszty. [Lista produkty bazy danych](/azure/) zawiera opcje hostingu danych bez konieczności stosowania pełnej platformy danych.

## <a name="next-steps"></a>Następne kroki

W zależności od hipotez i rozwiązania zasady w tym artykule mogą pomóc w projektowaniu aplikacji, które spełniają definicje MVP i angażują użytkowników. W dalszej części znajdują się zasady umożliwiające [podjęcie przyjęcia](./ci-cd.md), które umożliwiają szybsze i wydajne uzyskiwanie aplikacji i danych do klientów.

> [!div class="nextstepaction"]
> [Przyjęcie akceptacji](./ci-cd.md)
