---
title: Gotowość do umiejętności monitorowania w chmurze
description: Gotowość do umiejętności monitorowania w chmurze
author: BrianBlanchard
ms.author: magoedte
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d7d621f8f25b5369c4b9d39341c3e735b0996493
ms.sourcegitcommit: 871d0256a2d448e22b4ab8054e906fc2db946518
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/20/2020
ms.locfileid: "83705945"
---
<!-- cSpell:ignore kusto ITIL -->

# <a name="skills-readiness-for-cloud-monitoring"></a>Gotowość do umiejętności monitorowania w chmurze

W fazie planu podróży migracji celem jest opracowanie planów niezbędnych do wdrożenia. Plany muszą również obejmować sposób obsługi tych obciążeń, zanim zostaną one przenoszone lub udostępnione w środowisku produkcyjnym, a nie później. Zainteresowane strony biznesowe oczekują cennych usług i oczekują ich bez zakłóceń. Członkowie personelu IT muszą poznać nowe umiejętności i dostosować je, aby efektywnie korzystać z zintegrowanych usług platformy Azure w celu efektywnego monitorowania zasobów na platformie Azure i w środowiskach hybrydowych.

Opracowywanie niezbędnych umiejętności może być przyspieszone przy użyciu poniższych ścieżek szkoleniowych. Są one zorganizowane od podstaw, a następnie podzielono na trzy podstawowe domeny podmiotu — infrastrukturę, aplikację i analizę danych.  

## <a name="fundamentals"></a>Podstawy

- Wprowadzenie do [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) omawia podstawowe pojęcia związane z zarządzaniem i wdrażaniem zasobów platformy Azure. Personel działu INFORMATYCZNego zarządzający doświadczeniem w przedsiębiorstwie powinien zrozumieć zakresy zarządzania, kontrolę dostępu opartą na rolach (RBAC) przy użyciu programu. Szablony Azure Resource Manager i zarządzanie zasobami przy użyciu interfejsu wiersza polecenia platformy Azure i Azure PowerShell.

- Wprowadzenie do [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) pomaga dowiedzieć się, jak można używać Azure Policy do tworzenia i przypisywania zasad oraz zarządzania nimi. Azure Policy można wdrożyć i skonfigurować agentów Azure Monitor, włączyć monitorowanie za pomocą Azure Monitor dla maszyn wirtualnych i Azure Security Center, wdrożyć ustawienia diagnostyczne, Przeprowadź inspekcję ustawień konfiguracji gościa i nie tylko.

- Wprowadzenie do [interfejsu wiersza polecenia (CLI) platformy Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest), czyli międzyplatformowego środowiska wiersza polecenia do zarządzania zasobami platformy Azure. Należy również zapoznać się z tematem wprowadzenie do [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1). Oferty serwisu LinkedIn — w ramach kursu na poziomie początku [uczenia się narzędzi do zarządzania platformy Azure](https://www.linkedin.com/learning/learning-azure-management-tools), sesji obejmujących interfejs wiersza polecenia platformy Azure i języki programowania programu PowerShell:

  - [Użyj interfejsu wiersza polecenia platformy Azure](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli).
  - [Rozpoczynanie pracy z programem Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell)

- Dowiedz się, jak zabezpieczyć zasoby przy użyciu zasad, kontroli dostępu opartej na rolach i innych usług platformy Azure, wyświetlając opcję [Implementuj zabezpieczenia zarządzania zasobami na platformie Azure](https://docs.microsoft.com/learn/paths/implement-resource-mgmt-security).

- Wprowadzenie do [monitorowania Microsoft Azure zasobów i obciążeń](https://app.pluralsight.com/library/courses/microsoft-azure-resources-workloads-monitoring-update/table-of-contents) pozwala dowiedzieć się, jak używać narzędzi do monitorowania Microsoft Azure do monitorowania zasobów sieciowych platformy Azure, a także zasobów lokalnych.

## <a name="infrastructure-monitoring"></a>Monitorowanie infrastruktury

- [Zaprojektowanie strategii monitorowania infrastruktury w Microsoft Azure](https://www.pluralsight.com/courses/microsoft-azure-monitoring-strategy-infrastructure-design-update) pomaga uzyskać podstawowe informacje o możliwościach i rozwiązaniach związanych z monitorowaniem na platformie Azure. 

- [Monitorowanie klastrów Kubernetes](https://www.youtube.com/watch?time_continue=3&v=RjsNmapggPU&feature=emb_logo) zapewnia pośredni szczegółowe poziomu, który pomaga poznać monitorowanie klastra Kubernetes za pomocą Azure monitor dla kontenerów.

- Informacje na temat Azure Monitor sposobu monitorowania danych z [usługi Azure Storage i HDInsight](https://www.pluralsight.com/courses/microsoft-azure-data-storage-monitoring).

- [Element PlayBook monitorowania bazy danych Microsoft Azure](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) eksploruje kluczowe możliwości monitorowania, których można użyć do uzyskania szczegółowych informacji o Azure SQL Database, Azure SQL Data Warehouse i Azure Cosmos DB.

- [Monitorowanie Microsoft Azure sieci hybrydowych w chmurze](https://www.pluralsight.com/courses/microsoft-azure-hybrid-cloud-networks-monitoring) to zaawansowany kurs, który pomaga dowiedzieć się, jak za pomocą narzędzi monitorowania platformy Azure wizualizować, konserwować i optymalizować sieci wirtualne platformy Azure oraz połączenia wirtualnej sieci prywatnej dla implementacji chmury hybrydowej.

- [Usługa Azure ARC dla serwerów](https://docs.microsoft.com/azure/azure-arc/servers/overview)pozwala dowiedzieć się, jak zarządzać komputerami z systemami Windows i Linux hostowanymi poza platformą Azure, podobnie jak w przypadku zarządzania natywnymi maszynami wirtualnymi platformy Azure.

## <a name="application-monitoring"></a>Monitorowanie aplikacji

- Dowiedz się, w jaki sposób [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ułatwia Wyświetlanie dostępności i wydajności aplikacji i usług w jednym miejscu. Pluralsight oferuje następujące kursy, aby pomóc:

  - [Microsoft Azure inżynier DevOps: Optymalizacja mechanizmów przesyłania opinii](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) ułatwia przygotowanie do korzystania z Azure monitor, w tym Application Insights, monitorowania i optymalizowania aplikacji sieci Web.

  - [Microsoft Azure Developer: monitorowanie wydajności](https://app.pluralsight.com/library/courses/microsoft-azure-performance-monitoring). Rozpocznij pracę z tym kursem dotyczącym korzystania z Azure Monitor Application Insights w celu kompleksowego monitorowania składników aplikacji działających na platformie Azure.
  
  - [Microsoft Azure monitorowania element PlayBook Database](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) pomaga dowiedzieć się, jak zaimplementować i używać monitorowania Azure SQL Database, Azure SQL Data Warehouse i Azure Cosmos DB.

  - [Instrumentacja aplikacji za pomocą Azure Monitor Application Insights](https://app.pluralsight.com/library/courses/microsoft-azure-application-insights-web-application-instrument) to szczegółowey kurs dotyczący używania zestawu SDK Application Insights do zbierania danych telemetrycznych i zdarzeń z aplikacji ze składnikami kątowymi i Node. js.

  - [Debugowanie i Profilowanie aplikacji](https://www.pluralsight.com/courses/devintersection-azureai-session-31) to nagrywanie z sesji konferencji firmy Microsoft przy użyciu i interpretacji danych udostępnianych przez Azure Monitor Application Insights Snapshot Debugger i profilera.

## <a name="data-analysis"></a>Analiza danych

- Dowiedz się, jak pisać [zapytania dzienników w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries). Język zapytań Kusto jest podstawowym zasobem służącym do pisania zapytań dzienników Azure Monitor w celu eksplorowania i analizowania danych dzienników między zebranymi danymi z zależności aplikacji zasobów platformy Azure i hybrydowych, w tym aplikacji na żywo. 

- [Kusto Query Language (KQL) od podstaw](https://www.pluralsight.com/courses/kusto-query-language-kql-from-scratch) to kompleksowy kurs, który obejmuje szczegółowe przykłady dotyczące szerokiego zakresu przypadków użycia i technik analizy dzienników w Azure monitor dziennikach. 

## <a name="deeper-skills-exploration"></a>Nabywanie głębszych umiejętności

Poza tymi początkowymi opcjami rozwijania umiejętności dostępne są różnorodne opcje uczenia.

### <a name="typical-mappings-of-cloud-it-roles"></a>Typowe mapowanie ról IT w chmurze

Firma Microsoft wraz ze swoimi partnerami oferuje różnorodne opcje, dzięki którym wszyscy zainteresowani mogą rozwijać swoje umiejętności, korzystając z usług platformy Azure:

- [Centrum kariery Microsoft IT Pro](https://www.microsoft.com/itpro): służy jako bezpłatny zasób online, który ułatwia zamapowanie ścieżki kariery w chmurze. Dowiedz się, co sugerują eksperci branżowi dla Twoje roli związanej z chmurą i umiejętności, które do tego prowadzą. Zapoznaj się z materiałami szkoleniowymi w swoim własnym tempie, aby nabyć najpotrzebniejsze umiejętności.

Zdobądź oficjalne potwierdzenie swojej wiedzy na temat platformy Azure, korzystając ze [szkoleń i egzaminów certyfikacyjnych dotyczących platformy Microsoft Azure]( https://www.microsoft.com/learning/certification-overview.aspx).

## <a name="azure-devops-and-project-management"></a>Azure DevOps i zarządzanie projektami

Hybrydowe środowisko chmury zakłóca jego działanie z niezdefiniowanymi rolami, obowiązkami i działaniami. Organizacje muszą przejść do nowoczesnych rozwiązań związanych z zarządzaniem usługami, w tym metod agile i DevOps, aby lepiej zaspokoić potrzeby przekształceń i optymalizacji współczesnych firm.

W ramach migracji do platformy monitorowania w chmurze zespół IT odpowiedzialny za zarządzanie monitorowaniem w przedsiębiorstwie musi obejmować szkolenia Agile i uczestnictwo w działaniach DevOps. Obejmuje to również zastosowanie do _deweloperów_ w DevOps przez podejmowanie wymagań i włączenie zorganizowanych wymagań Agile, aby dostarczać z minimalnymi, żywotnymi rozwiązaniami do monitorowania, które są w sposób iteracyjny i zgodne z potrzebami biznesowymi. Aby kontrola źródła mogła zarządzać pakietami rozwiązań monitorowania iteracyjnego i innymi powiązanymi zabezpieczeniami, Połącz projekt Azure DevOps Server z repozytorium GitHub Enterprise Server. Zapewnia to link między zatwierdzeniami GitHub i żądaniami ściągnięcia do elementów roboczych. Za pomocą usługi GitHub Enterprise na potrzeby programowania można obsłużyć integrację z ciągłym monitorowaniem i wdrożeniem, a przy użyciu Azure Boards do planowania i śledzenia pracy.

Aby dowiedzieć się więcej, zapoznaj się z następującymi tematami:

- [Rozpocznij pracę z usługą Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops).

- [Poznaj podstawy dla białego pasa w dojo DevOps](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation)

- [Rozwijanie praktyk metodyki DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices)

- [Automatyzacja wdrożeń przy użyciu usługi Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops)

## <a name="other-considerations"></a>Inne zagadnienia

Klienci często nie mają trudności z zarządzaniem, konserwacją i dostarczaniem oczekiwanych firm (oraz do organizacji IT) dla usług, za które jest naliczana opłata. Monitorowanie jest traktowane jako rdzeń do zarządzania infrastrukturą i działalnością firmy, a jednocześnie koncentruje się na pomiarach jakości usług i obsługi klienta. Aby osiągnąć te cele, należy określić podstawę za pomocą narzędzia ITSM w połączeniu z DevOps, co pomoże zespołowi monitorującemu w zawieszeniu, jak zarządzać, dostarczać i obsługiwać usługę monitorowania. Przyjęcie platformy narzędzia ITSM Framework pozwala zespołowi monitorującemu działać jako dostawca i uzyskać uznanie jako zaufany czynnik biznesowy przez dostosowanie do strategicznych celów i potrzeb organizacji.

Zapoznaj się z poniższymi tematami, aby zrozumieć aktualizacje dotyczące najpopularniejszych wytycznych usługi narzędzia ITSM Framework w [wersji 4 i w chmurze obliczeniowej](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud), które koncentrują się na dołączeniu do istniejących wskazówek dotyczących biblioteki ITIL z najlepszymi rozwiązaniami od DevOps, Agile i Lean. Należy również wziąć pod uwagę [architekturę referencyjną IT4IT](https://www.opengroup.org/it4it) , która dostarcza alternatywny plan na potrzeby przekształcania go przy użyciu struktury niezależny od procesu.

## <a name="learn-more"></a>Dowiedz się więcej

Aby odnaleźć dodatkowe ścieżki szkoleniowe, przejrzyj [katalog Microsoft Learn](https://docs.microsoft.com/learn/browse). Użyj filtru Role, aby dopasować ścieżki szkoleniowe do swojej roli.
