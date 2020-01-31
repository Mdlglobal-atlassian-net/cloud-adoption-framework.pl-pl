---
title: Informacje o opcjach partnerstwa i pomocy technicznej
description: Opisuje opcje i metody wykonywania operacji związanych z migracją
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 9a525ab1c87f1cbb4c662c6f902e73de93c0204c
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76802467"
---
# <a name="understand-partnership-options"></a>Informacje o opcjach partnerstwa

Podczas migracji zespół wdrożeniowy ds. chmury wykonuje rzeczywistą migrację obciążeń do chmury. W przeciwieństwie do zadań związanych ze współdziałaniem i rozwiązywaniem problemów podczas definiowania [majątku cyfrowego](../../../digital-estate/index.md) lub tworzenia bazowej infrastruktury w chmurze na proces migracji będą się składać serie powtarzających się zadań wykonania. Poza wykonywaniem powtarzalnych czynności konieczne będzie prawdopodobnie wykonanie zadań związanych z testowaniem i dostrajaniem, które wymagają dokładnej znajomości wybranego dostawcy usług w chmurze. Powtarzalny charakter tego procesu sprawia, że może on być wykonywany przez partnera, dzięki czemu etatowi pracownicy nie będą nim tak obciążeni. Ponadto partnerzy mogą lepiej dawać sobie radę w sytuacjach wymagających głębokiej wiedzy technicznej, kiedy powtarzalne procesy napotykają anomalie wykonania.

Partnerzy mają tendencję utrzymywania ścisłej współpracy z jednym lub niewielką liczbą dostawców usług w chmurze. W celu lepszego zilustrowania opcji partnerstwa w pozostałej części tego artykułu przyjęto założenie, że wybranym dostawcą usług w chmurze jest platforma Microsoft Azure.

W trakcie planowania, kompilowania lub migrowania firma zazwyczaj ma cztery opcje partnerskie wykonywania:

- **Samoobsługa z przewodnikiem.** Istniejący zespół techniczny wykonuje migrację z pomocą firmy Microsoft.
- **FastTrack for Azure.** Aby przyspieszyć migrację, użyj programu Microsoft FastTrack for Azure.
- **Partner z zakresu rozwiązań.** Połącz się z partnerami z zakresu rozwiązań platformy Azure lub partnerami z zakresu rozwiązań w chmurze (CSP), aby przyspieszyć migrację.
- **Samoobsługa z pomocą techniczną.** Wykonanie jest realizowane przez istniejący personel techniczny z pomocą firmy Microsoft.

## <a name="guided-self-service"></a>Samoobsługa z przewodnikiem

Jeśli organizacja planuje samodzielnie przeprowadzić migrację na platformę Azure, firma Microsoft może wspierać ją na wszystkich etapach tej operacji. Aby uprościć proces migracji do platformy Azure, firma Microsoft i jej partnerzy opracowali rozbudowany zestaw architektur, przewodników, narzędzi i usług zmniejszających ryzyko i przyspieszających migrację maszyn wirtualnych, aplikacji oraz baz danych. Te narzędzia i usługi obsługują szeroki zakres systemów operacyjnych, języków programowania, struktur i baz danych.

- **Narzędzia do oceny i migracji.** Platforma Azure oferuje szeroką gamę narzędzi, które mogą być używane w różnych fazach transformacji w chmurze, w tym do oceny istniejącej infrastruktury. Więcej informacji można znaleźć w sekcji „Ocena” w rozdziale „Migracja” poniżej.
- **[Microsoft Cloud Adoption Framework](../../index.md).** Ta struktura zapewnia strukturalne podejście do wdrażania i migracji w chmurze. Jest on oparty na najlepszych rozwiązaniach w wielu klientach obsługiwanych przez firmę Microsoft i jest zorganizowany jako seria kroków, od architektury i projektowania do wdrożenia. Dla każdego kroku udostępniono pomocne wskazówki, które ułatwią zaprojektowanie architektury aplikacji.
- **[Wzorce projektowe oparte na chmurze](https://docs.microsoft.com/azure/architecture/patterns).** Platforma Azure udostępnia przydatne wzorce projektowe oparte na chmurze służące do tworzenia niezawodnych, skalowalnych i bezpiecznych obciążeń w chmurze. Dla każdego wzorca opisano problem rozwiązywany przez ten wzorzec, uwagi dotyczące stosowania wzorca oraz przykład oparty na platformie Azure. Większość wzorców zawiera przykłady lub fragmenty kodu, które pokazują sposób implementacji wzorca na platformie Azure. Są jednak one odpowiednie dla dowolnego systemu rozproszonego, hostowanego na platformie Azure lub na innych platformach w chmurze.
- **[Podstawy chmury](https://docs.microsoft.com/azure/architecture/guide).** Podstawy ułatwiają naukę podstawowych metod implementacji kluczowych pojęć. Ten przewodnik pomaga inżynierom projektować rozwiązania, które wykraczają poza pojedynczą usługę platformy Azure.
- **[Przykładowe scenariusze](https://docs.microsoft.com/azure/architecture/example-scenario).** Ten przewodnik zawiera odwołania do prawdziwych implementacji klientów, opisując narzędzia, metody i procesy, które zostały kiedyś zastosowane przez klientów w celu osiągnięcia określonych celów biznesowych.
- **[Architektury referencyjne](https://docs.microsoft.com/azure/architecture/reference-architectures).** Architektury referencyjne są uporządkowane według scenariuszy, a powiązane ze sobą architektury odpowiednio pogrupowane. Każda architektura zawiera najlepsze rozwiązania, a także zagadnienia dotyczące skalowalności, dostępności, możliwości zarządzania i zabezpieczeń. Większość obejmuje również rozwiązanie gotowe do wdrożenia.

## <a name="fasttrack-for-azure"></a>FastTrack for Azure

Usługa [FastTrack for Azure](https://azure.microsoft.com/roadmap/fasttrack-for-azure) zapewnia bezpośrednią pomoc od inżynierów ds. platformy Azure, którzy wraz z partnerami pomagają klientom szybko i pewnie kompilować rozwiązania platformy Azure. Usługa FastTrack oferuje najlepsze rozwiązania i narzędzia wykorzystywane w prawdziwych środowiskach klientów. Ułatwiają one klientom instalowanie, konfigurowanie i wdrażanie do produkcji rozwiązań platformy Azure. Są to między innymi:

- Migracja centrum danych
- System Windows Server na platformie Azure
- System Linux na platformie Azure
- SAP w systemie Azure
- Ciągłość biznesowa i odzyskiwanie po awarii (BCDR)
- Obliczenia o wysokiej wydajności*
- Aplikacje natywne dla chmury
- DevOps
- Modernizacja aplikacji
- Analizy w skali chmury**
- Inteligentne aplikacje
- Agenci inteligentni**
- Modernizacja danych z użyciem platformy Azure
- Zabezpieczenia i zarządzanie
- Dane rozproszone globalnie
- IoT***

*Ograniczona wersja zapoznawcza w Stanach Zjednoczonych, Zjednoczonym Królestwie i Europie Zachodniej

**Ograniczona wersja zapoznawcza w Zjednoczonym Królestwie i Europie Zachodniej

***Dostępne w drugiej połowie 2019 r.

W typowym zastosowaniu usługi FastTrack for Azure firma Microsoft pomaga zdefiniować wizję biznesową w celu pomyślnego zaplanowania i opracowania rozwiązań platformy Azure. Zespół ocenia potrzeby architektury i udostępnia wskazówki, zasady projektowania, narzędzia oraz zasoby ułatwiające tworzenie i wdrażanie rozwiązań platformy Azure oraz zarządzanie nimi. Zespół organizuje wykwalifikowanych partnerów do obsługi usług wdrażania na żądanie i okresowo sprawdza, czy wdrożenie przebiega zgodnie z planem, oraz pomaga w usunięciu czynników blokujących.

Główne fazy typowej asysty w ramach programu FastTrack for Azure to:

- **Odnajdywanie.** Identyfikuj kluczowe osoby biorące udział w projekcie, poznawaj cele lub wizje dotyczące rozwiązywanych problemów, a następnie oceniaj potrzeby dotyczące architektury.
- **Włączenie rozwiązania.** Poznaj zasady projektowania podczas tworzenia aplikacji, przeglądaj architekturę aplikacji i rozwiązań, a także wskazówki i narzędzia dotyczące wdrażania od weryfikacji koncepcji (PoC) po środowisko produkcyjne.
- **Ciągłe partnerstwo.** Inżynierowie platformy Azure i menedżerowie programu często sprawdzają, czy wdrożenie przebiega zgodnie z harmonogramem, i pomagają w usuwaniu blokad.

## <a name="microsoft-services-offerings-aligned-to-cloud-adoption-framework-approaches"></a>Oferty usług firmy Microsoft dostosowane do struktury wdrażania chmury

![Metoda z wykorzystaniem struktury wdrażania chmury usług firmy Microsoft](../../../_images/migrate/mcs-program-approach.jpg)

**Oceń:** Usługi firmy Microsoft korzystają z [ujednoliconego, opartego na danych i narzędziowego podejścia](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) składającego się z warsztatów architektonicznych, informacji w czasie rzeczywistym platformy Azure, modeli zagrożeń związanych z zabezpieczeniami i tożsamościami, a także różnych narzędzi, które zapewniają wgląd w wyzwania, zagrożenia, zalecenia i problemy związane z istniejącym środowiskiem platformy Azure przy użyciu tego samego klucza, takiego jak [plan modernizacji wysokiego poziomu](https://download.microsoft.com/download/F/7/2/F72FAD7E-8BBD-4E04-8C7B-9AC4FE04A150/Cloud_Adoption_Discovery_and_Roadmap_Datasheet.pdf)

**Zastosuj:** Korzystając z usług firmy Microsoft " [Azure Cloud Foundation](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf)", ustal podstawowe projekty platformy Azure, wzorce i architekturę ładu, mapując wymagania do najbardziej odpowiedniej architektury referencyjnej i planuj, Projektuj i wdrażaj infrastrukturę, zarządzanie, zabezpieczenia i tożsamość wymagane dla obciążeń.

**Migracja/Optymalizacja:** [Rozwiązanie do modernizacji w chmurze](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) usług firmy Microsoft oferuje kompleksowe podejście do przenoszenia aplikacji i infrastruktury na platformę Azure, a także optymalizację i modernizację po wdrożeniu w chmurze.

**Innowacje:** [Rozwiązanie Cloud Center (CCoE) dla](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) usług firmy Microsoft oferuje DevOpse szkoleńe i korzysta z zasad DevOps związanych z wbudowanymi w chmurze funkcjami zarządzania usługami i zabezpieczeniami, które ułatwiają tworzenie innowacji biznesowych, zwiększanie elastyczności i skrócenie czasu wprowadzania wartości w ramach bezpiecznych, przewidywalnych i elastycznych usług dostarczania i zarządzania operacjami.

## <a name="azure-support"></a>Pomoc techniczna systemu Azure

Jeśli masz pytania lub potrzebujesz pomocy, [utwórz wniosek o pomoc techniczną](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Jeśli wniosek o pomoc techniczną wymaga szczegółowych wskazówek, zapoznaj się z [planami pomocy technicznej platformy Azure](https://azure.microsoft.com/support/plans), aby dostosować najlepszy plan do swoich potrzeb.

## <a name="azure-solutions-partner"></a>Partner rozwiązań platformy Azure

Dostawcy rozwiązań certyfikowani przez firmę Microsoft specjalizują się w dostarczaniu aktualnych rozwiązań klienckich opartych na technologii Microsoft na całym świecie. Zoptymalizuj swoją działalność w chmurze z pomocą doświadczonego partnera.

Uzyskaj pomoc od partnerów oferujących gotowe lub niestandardowe rozwiązania dla platformy Azure oraz partnerów, którzy mogą pomóc we wdrażaniu tych rozwiązań i w zarządzaniu nimi:

- **[Znajdź partnera z zakresu rozwiązań w chmurze](https://www.microsoft.com/solution-providers/home).** Certyfikowany partner z zakresu rozwiązań w chmurze może pomóc w pełni wykorzystać chmurę, oceniając cele biznesowe dotyczące wdrożenia w chmurze oraz identyfikując odpowiednie rozwiązanie w chmurze, które spełnia potrzeby biznesowe i pomaga zwiększyć wydajność oraz efektywność biznesową.
- **[Znajdź partnera usługi zarządzanej](https://www.microsoft.com/solution-providers/search?cacheId=16a3b49b-fef2-449d-bdf0-628008114cca).** Partner usługi zarządzanej na platformie Azure (MSP) pomaga w przeniesieniu działalności na platformę Azure przez zarządzanie wszystkimi aspektami przejścia do chmury. Partnerzy usługi zarządzanej zapewniają kompleksowe doradztwo od konsultacji do migracji i zarządzania operacjami, dzięki czemu klienci poznają wszystkie korzyści związane z wdrażaniem w chmurze. Zapewniają oni również typową pomoc techniczną, obsługę aprowizacji i rozliczeń — z elastycznym modelem biznesowym płatności zgodnie z rzeczywistym użyciem (PAYG).

## <a name="next-steps"></a>Następne kroki

Po wybraniu partnera i strategii pomocy technicznej można zaktualizować [listy prac związanych z wydaniem i iteracją](./release-iteration-backlog.md), aby odzwierciedlały planowane wysiłki i przypisania.

> [!div class="nextstepaction"]
> [Zarządzanie zmianami przy użyciu list prac związanych z wydaniem i iteracją](./release-iteration-backlog.md)
