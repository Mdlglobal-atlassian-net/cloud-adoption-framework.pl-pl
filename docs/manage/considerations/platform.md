---
title: Operacje na platformie — zarządzanie chmurą i operacje
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Operacje na platformie — zarządzanie chmurą i operacje
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/07/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: aab6dbe2ff8b1037a86317d00d717b4b22052c59
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72558053"
---
# <a name="platform-operations-in-cloud-management"></a>Operacje na platformie w zarządzaniu chmurą

Linia bazowa zarządzania chmurą obejmująca [spis i widoczność](./inventory.md), [zgodność operacyjną](./operational-compliance.md)oraz [ochronę i odzyskiwanie](./protect.md) mogą zapewnić wystarczający poziom zarządzania chmurą w przypadku większości obciążeń w portfolio IT. Jednak rzadko wystarcza do obsługi pełnego portfolio. Ten artykuł jest oparty na najpopularniejszym następnym kroku zarządzania chmurą, operacji portfolio.

Szybkie badanie zasobów w portfolio IT spowoduje wyróżnienie wzorców między obsługiwanymi obciążeniami. W ramach tych obciążeń będzie dostępnych wiele popularnych platform. W zależności od wcześniejszych decyzji technicznych w ramach firmy te platformy mogą być szeroko różne. W przypadku niektórych organizacji nastąpi duże zależności od programu SQL Server, Oracle lub innych platform danych typu "open source". W innych organizacjach commonalities może być odblokowany na platformach hostingowych dla maszyn wirtualnych lub kontenerów. Nadal inne osoby mogą mieć wspólną zależność od aplikacji lub systemów korporacyjnych do planowania zasobów przedsiębiorstwa (ERP), takich jak SAP, Oracle czy innych.

Zrozumienie tych commonalities umożliwia zespołowi zarządzania chmurom specjalizację na wyższym poziomie wsparcia dla tych platform z priorytetami.

## <a name="establish-a-service-catalog"></a>Ustanów katalog usług

Celem operacji platformy jest utworzenie niezawodnych i powtarzalnych rozwiązań, które mogą być używane przez zespół wdrażania w chmurze w celu zapewnienia platformy, która zapewnia wyższy poziom zobowiązania biznesowego. To zobowiązanie może obniżyć prawdopodobieństwo lub częstotliwość przestoju, zwiększając niezawodność. Zobowiązania mogą również zmniejszyć ilość utraconych danych lub czas do odzyskania w przypadku awarii systemu. To zobowiązanie często obejmuje trwającą i scentralizowaną operację do obsługi platformy.

Ponieważ zespół zarządzający chmurą ustala więcej stopni zarządzania operacyjnego i specjalizacji związanych z określonymi platformami, te platformy są dodawane do rosnącego katalogu usług. Ten katalog usług umożliwia samoobsługowe wdrażanie platform w określonej konfiguracji, która jest zgodna z trwającymi operacjami platformy. Podczas konwersacji związanych z wyrównaniaem firmy, zarządzanie chmurą i zespoły strategii chmury mogą zaproponować rozwiązania katalogu usług w celu poprawy niezawodności, czasu przestoju i zobowiązań związanych z odzyskiwaniem w kontrolowanym, powtarzalnym procesie.

W przypadku dokumentacji niektóre organizacje odwołują się do katalogu usługi wczesnego etapu jako "zatwierdzonej listy". Podstawowa różnica polega na tym, że katalog usług obejmuje trwające zobowiązania operacyjne z centrum usługi Cloud doskonałości. "Lista zatwierdzonych" jest podobna, ponieważ udostępnia wstępnie zatwierdzoną listę rozwiązań, których zespół może używać w chmurze, ale nie jest to zwykle korzyść operacyjna skojarzona z aplikacjami "zatwierdzone listy". Podobnie jak debata między centralnym działem IT i CCoE, różnica stanowi jeden z priorytetów. Katalog usług zakłada dobry cel, ale zapewnia działania, zarządzanie i guardrails zabezpieczeń, które przyspieszają innowacje. "Lista zatwierdzonych" utrudnia innowacje do momentu, aż do rozwiązania mogą zostać przesłane bramy operacji, zgodności i zabezpieczeń. Oba są wydajnymi rozwiązaniami, ale wymagają od firmy podejmowania decyzji o delikatnej priorytetyzacji w celu inwestowania w innowacje lub zgodność.

### <a name="building-the-service-catalog"></a>Kompilowanie katalogu usług

Zarządzanie chmurą najprawdopodobniej zakończyło się niepowodzeniem w przypadku dostarczania katalogu usług w silosie. Odpowiednie opracowywanie wykazu wymaga partnerstwa między centralnym działem IT, a centrum w chmurze doskonałości (CCoE). Ta metoda jest najbardziej pomyślna, gdy organizacja IT osiągnie poziom ważności CCoE, ale może być zaimplementowana wcześniej.

Podczas kompilowania katalogu usług w ramach modelu CCoE zespół platform w chmurze kompiluje żądaną platformę stanu. Zarządzanie chmurą i zespoły ds. zabezpieczeń w chmurze weryfikują nadzór i zgodność w ramach wdrożenia. Zespół zarządzający chmurą ustala bieżące operacje dla tej platformy. Zespół usługi Cloud Automation pakuje platformę do skalowalnego i powtarzalnego wdrożenia.

Po spakowaniu zespół zarządzający chmurą może dodać pakiet do rosnącego katalogu usług. Z tego miejsca zespół ds. wdrażania w chmurze może korzystać z tego pakietu lub innych elementów w katalogu podczas wdrażania. Gdy rozwiązanie przejdzie do środowiska produkcyjnego, firma uzyskuje dodatkowe korzyści wynikające z lepszego zarządzania operacyjnego i potencjału zmniejszonych przerw w działaniu firmy.

> [!NOTE]
> Tworzenie katalogu usług wymaga dużej nakładu pracy i czasu z wielu zespołów. Korzystanie z katalogu usług lub dozwolonych jako mechanizmu kontroli spowoduje spowolnienie innowacji. Gdy innowacje są priorytetowe, wykazy usług powinny być opracowywane równolegle z innymi procesami wdrażania.

## <a name="defining-your-own-platform-operations"></a>Definiowanie własnych operacji na platformie

Narzędzia i procesy zarządzania mogą usprawnić operacje platformy. Jednak często nie wystarcza do osiągnięcia żądanego stanu stabilności i niezawodności. Prawdziwe operacje na platformie wymagają fokusu na filarach z jakością architektury. Gdy platforma uzasadnia dokładniejszą inwestycję w operacje, należy wziąć pod uwagę następujące pięć filarów, aby platforma stała się częścią katalogu usług:

1. Skalowalność: zdolność systemu do obsługi zwiększonego obciążenia.
2. Dostępność: okres, w którym system jest funkcjonalny i działa.
3. Odporność: zdolność systemu do odzyskiwania sprawności po awarii i kontynuowania działania.
4. Zarządzanie: procesy operacji, które przechowują system w środowisku produkcyjnym.
5. Zabezpieczenia: Ochrona aplikacji i danych przed zagrożeniami.

Platforma [architektury Azure](https://docs.microsoft.com/azure/architecture/guide/pillars) oferuje podejście do oceny konkretnych obciążeń związanych z przystąpieniem do tych filarów, w celu poprawy ogólnych operacji. Te filary mogą być stosowane do operacji na platformie i operacji związanych z obciążeniami.

## <a name="getting-started-with-specific-platforms"></a>Wprowadzenie do określonych platform

W przypadku typowych klientów platformy Azure poniżej przedstawiono popularne platformy, które mogą łatwo uzasadnić inwestycje w operacje na platformie. Zespoły zarządzania chmurą mogą zacząć korzystać z tych rozwiązań podczas kompilowania wymagań operacji platformy lub pełnego katalogu usług.

### <a name="paas-data-operations"></a>Operacje na danych PaaS

Dane są często pierwszą platformą w celu zagwarantowania inwestycji związanych z operacjami platformy. Gdy dane są hostowane w środowisku PaaS (Platform as a Service), zainteresowane strony biznesowe zażądają zredukowanego celu punktu odzyskiwania, aby zminimalizować utratę danych. W zależności od charakteru aplikacji mogą również zażądać obniżenia w RTO. W obu przypadkach architektura obsługująca rozwiązania danych opartych na PaaS może łatwo obsłużyć pewien zwiększony poziom obsługi zarządzania.

W większości scenariuszy koszt poprawy zobowiązań związanych z zarządzaniem jest łatwo uzasadniony, nawet w przypadku aplikacji, które nie są krytyczne. To ulepszenie operacji platformy jest tak popularne, że wiele zespołów zarządzania chmurą widzi je bardziej jako rozszerzoną linię bazową, a nie w celu potraktowania jej jako prawdziwej poprawy operacji platformy.

### <a name="iaas-data-operations"></a>Operacje na danych IaaS

Gdy dane są hostowane w tradycyjnym rozwiązaniu infrastruktury jako usługi (IaaS), nakład poprawy RTO i celu punktu odzyskiwania może być znacznie wyższy. Mimo że zainteresowane osoby biorące udział w osiąganiu lepszych zobowiązań związanych z zarządzaniem mają wpływ na decyzję PaaS a IaaS. Jeśli wszystko, zrozumienie podstawowych różnic w architekturze, może monitować firmę o poproszenie o PaaS rozwiązania lub zobowiązania, które pasują do tego, co jest dostępne w rozwiązaniach PaaS. Modernizacja wszelkich platform danych IaaS powinna być traktowana jako pierwszy krok operacji platformy.

Gdy modernizacja nie jest opcją, zespoły zarządzające chmurą będą często określać priorytety na platformach danych opartych na IaaS, jako pierwszą wymaganą usługę w katalogu usług. Umożliwienie biznesowym wybór między autonomicznymi serwerami danych i klastrami o wysokiej dostępności sprawia, że konwersacje zobowiązania biznesowe są znacznie prostsze. Podstawowa znajomość ulepszeń operacyjnych i zwiększonych kosztów umożliwi firmie podejmowanie najlepszych decyzji dotyczących procesów biznesowych i obsługi obciążeń.

### <a name="other-common-platform-operations"></a>Inne typowe operacje na platformie

Oprócz platform danych hosty maszyn wirtualnych mają być typową platformą na potrzeby ulepszeń operacji. Najczęściej Platforma chmurowa i zespoły zarządzania chmurą zainwestowają ulepszenia z hostami VMWare lub rozwiązaniami kontenerów w celu zwiększenia stabilności i niezawodności hostów, które obsługują maszyny wirtualne, które są obciążeniami. Prawidłowe operacje na jednym hoście lub kontenerze mogą poprawić cel/RTO kilku obciążeń. Takie podejście tworzy ulepszone zobowiązania biznesowe, ale dystrybuuje inwestycję. Razem udoskonalone zobowiązania i zmniejszone koszty znacznie ułatwiają Justowanie ulepszeń zarządzania chmurą i operacji na platformie.

## <a name="next-steps"></a>Następne kroki

Równolegle z ulepszeniami operacji platformy, zespoły zarządzające chmurą również koncentrują się na ulepszaniu [operacji obciążeń](./workload.md) dla najwyżej 20% lub mniej obciążeń produkcyjnych.

> [!div class="nextstepaction"]
> [Poprawianie operacji obciążenia](./workload.md)
