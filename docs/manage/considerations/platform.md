---
title: Operacje na platformie w zarządzaniu chmurą
description: Utwórz zrozumienie zależności w organizacji dla typowych operacji platformy w zarządzaniu chmurą.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 3480d0411e1a16eed18d14859cbb997706ccccb4
ms.sourcegitcommit: da7ebd67a0ebf29361f093f00e10217b212a2eb2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527622"
---
# <a name="platform-operations-in-cloud-management"></a>Operacje na platformie w zarządzaniu chmurą

Linia bazowa zarządzania chmurą obejmująca [spis i widoczność](./inventory.md), [zgodność operacyjną](./operational-compliance.md)oraz [ochronę i odzyskiwanie](./protect.md) mogą zapewnić wystarczający poziom zarządzania chmurą w przypadku większości obciążeń w portfolio IT. Taka linia bazowa jest jednak rzadko wystarczająca do obsługi pełnego portfolio. Ten artykuł jest oparty na najpopularniejszym następnym kroku zarządzania chmurą, operacji portfolio.

Szybkie badanie zasobów w portfolio IT wyróżnia wzorce między obsługiwanymi obciążeniami. W ramach tych obciążeń będą dostępne popularne platformy. W zależności od wcześniejszych decyzji technicznych w firmie te platformy mogą się różnić.

W przypadku niektórych organizacji nastąpi bardzo duże zależności od SQL Server, Oracle lub innych platform danych typu "open source". W innych organizacjach commonalities może być odblokowany na platformach hostingowych dla maszyn wirtualnych lub kontenerów. Nadal inne osoby mogą mieć wspólną zależność od aplikacji lub systemów Enterprise Resource Planning (ERP), takich jak SAP, Oracle czy inne.

Zrozumienie tych commonalities zespół zarządzający chmurą może specjalizację na wyższym poziomie wsparcia dla tych platform z priorytetami.

## <a name="establish-a-service-catalog"></a>Ustanów katalog usług

Celem operacji platformy jest utworzenie niezawodnych i powtarzalnych rozwiązań, których zespół wdrażania chmury może wykorzystać do dostarczania platformy, która zapewnia wyższy poziom zobowiązania biznesowego. To zobowiązanie może obniżyć prawdopodobieństwo lub częstotliwość przestojów, co zwiększa niezawodność. W przypadku awarii systemu zobowiązanie może również zmniejszyć ilość utraconych danych lub ich czas na odzyskanie. Takie zobowiązanie często obejmuje trwającą i scentralizowaną operację do obsługi platformy.

Ponieważ zespół zarządzający chmurą ustala więcej stopni zarządzania operacyjnego i specjalizacji związanych z określonymi platformami, te platformy są dodawane do rosnącego katalogu usług. Katalog usług umożliwia samoobsługowe wdrażanie platform w określonej konfiguracji, która jest zgodna z trwającymi operacjami platformy. W trakcie rozmowy w ramach biznesowej, zespoły ds. zarządzania chmurą i strategii chmury mogą zaproponować rozwiązania katalogu usług w celu poprawy niezawodności, czasu przestoju i zobowiązań związanych z odzyskiwaniem w kontrolowanym, powtarzalnym procesie.

W celu uzyskania informacji niektóre organizacje odnoszą się do wczesnego etapu wykazu usług jako _zatwierdzonej listy_. Podstawowa różnica polega na tym, że katalog usług obejmuje trwające zobowiązania operacyjne z centrum analiz doskonałości (CCoE). Lista zatwierdzonych jest podobna, ponieważ zawiera zatwierdzoną listę rozwiązań, które mogą być używane przez zespół w chmurze. Jednak zazwyczaj nie istnieje korzyść operacyjna skojarzona z aplikacjami na zatwierdzonej liście.

Podobnie jak debata między centralnym działem IT i CCoE, różnica stanowi jeden z priorytetów. Katalog usług zakłada dobry cel, ale zapewnia działania, zarządzanie i guardrails zabezpieczeń, które przyspieszają innowacje. Lista zatwierdzonych utrudnia innowacje do momentu, aż do rozwiązania można przekazywać operacje, zgodność i bramy zabezpieczeń. Oba rozwiązania są dostępne, ale wymagają od firmy podejmowania decyzji o delikatnej priorytetyzacji w celu inwestowania w innowacje lub zgodność.

### <a name="build-the-service-catalog"></a>Kompilowanie katalogu usług

Zarządzanie chmurą najprawdopodobniej zakończyło się niepowodzeniem w przypadku dostarczania katalogu usług w silosie. Odpowiednie opracowywanie wykazu wymaga partnerstwa między centralnym lub CCoEem. Ta metoda jest najbardziej pomyślna, gdy organizacja IT osiągnie poziom ważności CCoE, ale może być zaimplementowana wcześniej.

Podczas kompilowania katalogu usług w ramach modelu CCoE zespół platform w chmurze kompiluje platformę żądanego stanu. Zarządzanie chmurą i zespoły ds. zabezpieczeń w chmurze weryfikują nadzór i zgodność w ramach wdrożenia. Zespół zarządzający chmurą ustala bieżące operacje dla tej platformy. Zespół usługi Cloud Automation pakuje platformę do skalowalnego i powtarzalnego wdrożenia.

Po spakowaniu platformy zespół zarządzający chmurą może dodać go do rosnącego katalogu usług. Z tego miejsca zespół ds. wdrażania chmury może korzystać z pakietu lub innych elementów w katalogu podczas wdrażania. Gdy rozwiązanie przejdzie do środowiska produkcyjnego, firma realizuje dodatkowe korzyści wynikające z lepszego zarządzania operacyjną i potencjalnie zmniejsza zakłócenia biznesowe.

> [!NOTE]
> Tworzenie katalogu usług wymaga dużej nakładu pracy i czasu z wielu zespołów. Korzystanie z katalogu usług lub zatwierdzonej listy jako mechanizmu kontroli spowoduje spowolnienie innowacji. Gdy innowacje są priorytetowe, wykazy usług powinny być opracowywane równolegle z innymi procesami wdrażania.

## <a name="define-your-own-platform-operations"></a>Definiowanie własnych operacji platformy

Chociaż narzędzia do zarządzania i procesy mogą pomóc w ulepszaniu operacji platformy, to często nie wystarcza do osiągnięcia pożądanych Stanów stabilności i niezawodności. Prawdziwe operacje na platformie wymagają skoncentrowania się na filarach z jakością architektury. Gdy platforma uzasadnia dokładniejszą inwestycję w operacje, należy wziąć pod uwagę następujące pięć filarów, aby platforma stała się częścią katalogu usług:

- **Skalowalność:** Zdolność systemu do obsługi zwiększonego obciążenia.
- **Dostępność:** Procent czasu, przez który system jest funkcjonalny i działa.
- **Odporność:** Zdolność systemu do odzyskiwania sprawności po awarii i kontynuowania działania.
- **Zarządzanie:** Procesy operacji, które przechowują system w środowisku produkcyjnym.
- **Zabezpieczenia:** Ochrona aplikacji i danych przed zagrożeniami.

Platforma [architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) oferuje podejście do oceny konkretnych obciążeń związanych z przystąpieniem do tych filarów, w celu poprawy ogólnych operacji. Te filary mogą być stosowane do operacji na platformie i operacji związanych z obciążeniami.

## <a name="get-started-with-specific-platforms"></a>Wprowadzenie do określonych platform

Platformy omówione w następnych sekcjach są wspólne dla typowych klientów platformy Azure i mogą łatwo uzasadnić inwestycje w operacje na platformie. Zespoły zarządzające chmurą mogą zacząć od nich, gdy tworzą wymagania dotyczące operacji platformy lub pełnego katalogu usług.

### <a name="paas-data-operations"></a>Operacje na danych PaaS

Dane są często pierwszą platformą w celu zagwarantowania inwestycji związanych z operacjami platformy. Gdy dane są hostowane w środowisku usługi jako usługa (PaaS), zainteresowane strony biznesowe zażądają zmniejszonego celu punktu odzyskiwania (RPO), aby zminimalizować utratę danych. W zależności od charakteru aplikacji mogą również zażądać obniżenia celu czasu odzyskiwania (RTO). W obu przypadkach architektura, która obsługuje rozwiązania do obsługi danych opartych na PaaS, może łatwo obsłużyć większą liczbę poziomów zarządzania.

W większości scenariuszy koszt poprawy zobowiązań związanych z zarządzaniem jest łatwo uzasadniony, nawet w przypadku aplikacji, które nie są krytyczne. To ulepszenie operacji platformy jest tak popularne, że wiele zespołów zarządzania chmurą widzi je bardziej jako rozszerzoną linię bazową, a nie jako prawdziwe udoskonalenie operacji platformy.

### <a name="iaas-data-operations"></a>Operacje na danych IaaS

Gdy dane są hostowane w tradycyjnym rozwiązaniu infrastruktury jako usługi (IaaS), wysiłki w celu poprawy celu punktu odzyskiwania i RTO mogą być znacznie wyższe. Mimo że zainteresowane osoby biorące udział w osiąganiu lepszych zobowiązań związanych z zarządzaniem mają wpływ na PaaS i IaaS decyzje. Jeśli wszystko, zrozumienie podstawowych różnic w architekturze może zadawać firmie prośbę o PaaS rozwiązań lub zobowiązań, które pasują do możliwości dostępnych w rozwiązaniach PaaS. Modernizacja wszelkich platform danych IaaS powinna być traktowana jako pierwszy krok operacji platformy.

Gdy modernizacja nie jest opcją, zespoły zarządzające chmurą zwykle ustalają priorytety platform danych opartych na IaaS jako pierwszej wymaganej usługi w katalogu usług. Umożliwienie biznesowym wybór między autonomicznymi serwerami danych i klastrami o wysokiej dostępności sprawia, że konwersacje zobowiązania biznesowe są znacznie prostsze. Podstawowa znajomość ulepszeń operacyjnych i zwiększonych kosztów umożliwi firmie podejmowanie najlepszych decyzji dotyczących procesów biznesowych i obsługi obciążeń.

### <a name="other-common-platform-operations"></a>Inne typowe operacje na platformie

Oprócz platform danych hosty maszyn wirtualnych mają być typową platformą na potrzeby ulepszeń operacji. Najczęściej, Platforma chmury i zespoły zarządzania chmurą zainwestowali w usprawnienia na hostach VMware lub rozwiązaniach kontenerów. Takie inwestycje mogą zwiększyć stabilność i niezawodność hostów, które obsługują maszyny wirtualne, które z kolei zużywają obciążenia. Odpowiednie operacje dotyczące jednego hosta lub kontenera mogą poprawić cel punktu odzyskiwania lub RTO kilku obciążeń. Takie podejście tworzy ulepszone zobowiązania biznesowe, ale dystrybuuje inwestycję. Ulepszono zobowiązania i obniżane koszty, aby znacznie łatwiej było uzasadnić ulepszenia zarządzania chmurą i operacji na platformie.

## <a name="next-steps"></a>Następne kroki

Równolegle z ulepszeniami operacji platformy, zespoły zarządzania chmurą koncentrują się również na ulepszaniu [operacji obciążeń](./workload.md) dla najwyżej 20 procent obciążeń produkcyjnych.

> [!div class="nextstepaction"]
> [Poprawianie operacji obciążenia](./workload.md)
