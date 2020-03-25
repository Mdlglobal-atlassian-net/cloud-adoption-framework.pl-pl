---
title: Gotowość do umiejętności monitorowania w chmurze
description: Gotowość do umiejętności monitorowania w chmurze
author: BrianBlanchard
ms.author: magoedte
ms.date: 03/23/2020
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7e078bbeea12c71997474d372b0b6b838ed5f4a3
ms.sourcegitcommit: a1209c9dab369171e1fe0cdc6a58e3f6ae6a8f22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/25/2020
ms.locfileid: "80261539"
---
# <a name="skills-readiness-for-cloud-monitoring"></a>Gotowość do umiejętności monitorowania w chmurze

W fazie planu podróży migracji celem jest opracowanie planów niezbędnych do wdrożenia. Plany muszą również obejmować sposób obsługi tych obciążeń, zanim zostaną one przenoszone lub udostępnione w środowisku produkcyjnym, a nie później. Zainteresowane strony biznesowe oczekują cennych usług i oczekują ich bez zakłóceń. Członkowie personelu IT muszą poznać nowe umiejętności i dostosować je, aby efektywnie wykorzystać zintegrowane usługi platformy Azure w celu efektywnego monitorowania zasobów na platformie Azure i w środowiskach hybrydowych. 

Opracowywanie niezbędnych umiejętności może być przyspieszone przy użyciu następujących ścieżek szkoleniowych:

- Wprowadzenie do [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) omawia podstawowe pojęcia związane z zarządzaniem i wdrażaniem zasobów platformy Azure. Personel działu INFORMATYCZNego zarządzający doświadczeniem w przedsiębiorstwie powinien zrozumieć zakresy zarządzania, kontrolę dostępu opartą na rolach (RBAC) przy użyciu programu. Szablony Azure Resource Manager i zarządzanie zasobami przy użyciu interfejsu wiersza polecenia platformy Azure i Azure PowerShell.

- Dowiedz się, jak zabezpieczyć zasoby przy użyciu zasad, kontroli dostępu opartej na rolach i innych usług platformy Azure, wyświetlając opcję [Implementuj zabezpieczenia zarządzania zasobami na platformie Azure](https://docs.microsoft.com//learn/paths/implement-resource-mgmt-security/). 

- Wprowadzenie do [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) pomaga dowiedzieć się, jak można używać Azure Policy do tworzenia i przypisywania zasad oraz zarządzania nimi. Azure Policy można wdrożyć i skonfigurować agentów Azure Monitor, włączyć monitorowanie za pomocą Azure Monitor dla maszyn wirtualnych i Azure Security Center, wdrożyć ustawienia diagnostyczne, Przeprowadź inspekcję ustawień konfiguracji gościa i nie tylko.

- Wprowadzenie do [interfejsu wiersza polecenia](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest) (CLI) platformy Azure, czyli międzyplatformowego środowiska wiersza polecenia do zarządzania zasobami platformy Azure. Należy również zapoznać się z tematem wprowadzenie do [Azure PowerShell](https://docs.microsoft.com/powershell/azure/?view=azps-3.6.1). Oferty serwisu LinkedIn — w ramach kursu na poziomie początku [uczenia się narzędzi do zarządzania platformy Azure](https://www.linkedin.com/learning/learning-azure-management-tools), sesji obejmujących interfejs wiersza polecenia platformy Azure i języki programowania programu PowerShell:

   - [Użyj interfejsu wiersza polecenia platformy Azure](https://www.linkedin.com/learning/learning-azure-management-tools/use-the-azure-cli).
   
   - [Wprowadzenie do Azure PowerShell](https://www.linkedin.com/learning/learning-azure-management-tools/understand-azure-powershell) 

- Dowiedz się, jak pisać [zapytania dzienników w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries).  Język zapytań Kusto jest podstawowym zasobem służącym do pisania zapytań dzienników Azure Monitor w celu eksplorowania i analizowania danych dzienników między zebranymi danymi z zależności aplikacji zasobów platformy Azure i hybrydowych, w tym aplikacji na żywo.

- Dowiedz się, w jaki sposób [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview) ułatwia Wyświetlanie dostępności i wydajności aplikacji i usług w jednym miejscu. Pluralsight oferuje następujące kursy, aby pomóc:

   - [Microsoft Azure monitorowanie i zarządzanie IaaSą](https://www.pluralsight.com/courses/azure-iaas-monitoring-management-getting-started) pomaga dowiedzieć się, jak używać Azure monitor do podstawowego monitorowania obciążeń działających w systemie IaaS.

   - [Monitorowanie Microsoft Azure zasobów i obciążeń](https://www.pluralsight.com/courses/microsoft-azure-resources-workloads-monitoring) pomaga dowiedzieć się, jak używać narzędzi monitorowania Microsoft Azure do monitorowania zasobów sieci platformy Azure (a także Premium).

   - [Microsoft Azure inżynier DevOps: Optymalizacja mechanizmów przesyłania opinii](https://www.pluralsight.com/courses/microsoft-azure-optimize-feedback-mechanisms) pomaga przygotować się do korzystania z Azure monitor, w tym Application Insights i log Analytics do monitorowania i optymalizowania aplikacji sieci Web.

   - [Microsoft Azure monitorowania element PlayBook Database](https://www.pluralsight.com/courses/microsoft-azure-database-playbook-monitoring) pomaga dowiedzieć się, jak zaimplementować i używać monitorowania Azure SQL Database, Azure SQL Data Warehouse i Azure Cosmos DB.

- [Usługa Azure ARC dla serwerów](https://docs.microsoft.com/azure/azure-arc/servers/overview)pozwala dowiedzieć się, jak zarządzać komputerami z systemami Windows i Linux hostowanymi poza platformą Azure, podobnie jak w przypadku zarządzania natywnymi maszynami wirtualnymi platformy Azure.

## <a name="deeper-skills-exploration"></a>Nabywanie głębszych umiejętności

Poza tymi początkowymi opcjami rozwijania umiejętności dostępne są różnorodne opcje uczenia.

### <a name="typical-mappings-of-cloud-it-roles"></a>Typowe mapowanie ról IT w chmurze

Firma Microsoft wraz ze swoimi partnerami oferuje różnorodne opcje, dzięki którym wszyscy zainteresowani mogą rozwijać swoje umiejętności, korzystając z usług platformy Azure:

- [Centrum kariery Microsoft IT Pro](https://www.microsoft.com/itpro): służy jako bezpłatny zasób online, który ułatwia zamapowanie ścieżki kariery w chmurze. Dowiedz się, co sugerują eksperci branżowi dla Twoje roli związanej z chmurą i umiejętności, które do tego prowadzą. Zapoznaj się z materiałami szkoleniowymi w swoim własnym tempie, aby nabyć najpotrzebniejsze umiejętności.

Zdobądź oficjalne potwierdzenie swojej wiedzy na temat platformy Azure, korzystając ze [szkoleń i egzaminów certyfikacyjnych dotyczących platformy Microsoft Azure]( https://www.microsoft.com/learning/azure-certification.aspx).

## <a name="azure-devops-and-project-management"></a>Azure DevOps i zarządzanie projektami

Hybrydowe środowisko chmury zakłóca jego działanie z niezdefiniowanymi rolami, obowiązkami i działaniami. Organizacje muszą przejść do nowoczesnych rozwiązań związanych z zarządzaniem usługami, w tym metod agile i DevOps, aby lepiej zaspokoić potrzeby przekształceń i optymalizacji współczesnych firm. 

W ramach migracji do platformy monitorowania w chmurze zespół IT odpowiedzialny za zarządzanie monitorowaniem w przedsiębiorstwie musi obejmować szkolenia Agile i uczestnictwo w działaniach DevOps. Obejmuje to również zastosowanie do *deweloperów* w DevOps przez podejmowanie wymagań i włączenie zorganizowanych wymagań Agile, aby dostarczać z minimalnymi, żywotnymi rozwiązaniami do monitorowania, które są w sposób iteracyjny i zgodne z potrzebami biznesowymi. Aby kontrola źródła mogła zarządzać pakietami rozwiązań monitorowania iteracyjnego i innymi powiązanymi zabezpieczeniami, Połącz projekt Azure DevOps Server z repozytorium GitHub Enterprise Server. Zapewnia to link między zatwierdzeniami GitHub i żądaniami ściągnięcia do elementów roboczych. Za pomocą usługi GitHub Enterprise na potrzeby programowania można obsłużyć integrację z ciągłym monitorowaniem i wdrożeniem, a przy użyciu Azure Boards do planowania i śledzenia pracy.

Aby dowiedzieć się więcej, zapoznaj się z następującymi tematami:

- [Rozpocznij pracę z usługą Azure DevOps](https://docs.microsoft.com/learn/modules/get-started-with-devops/). 

- [Dowiedz się więcej na temat DevOps Dojo — biały pas](https://docs.microsoft.com/learn/paths/devops-dojo-white-belt-foundation/)

- [Rozwijanie praktyk DevOps](https://docs.microsoft.com/learn/paths/evolve-your-devops-practices/)

- [Automatyzacja wdrożeń przy użyciu usługi Azure DevOps](https://docs.microsoft.com/learn/paths/automate-deployments-azure-devops/)

## <a name="other-considerations"></a>Inne zagadnienia

Klienci często nie mają trudności z zarządzaniem, konserwacją i dostarczaniem oczekiwanych firm (oraz do organizacji IT) dla usług, za które jest naliczana opłata. Monitorowanie jest traktowane jako rdzeń do zarządzania infrastrukturą i działalnością firmy, a jednocześnie koncentruje się na pomiarach jakości usług i obsługi klienta.  Aby osiągnąć te cele, należy określić podstawę za pomocą narzędzia ITSM w połączeniu z DevOps, co pomoże zespołowi monitorującemu w zawieszeniu, jak zarządzać, dostarczać i obsługiwać usługę monitorowania. Przyjęcie platformy narzędzia ITSM Framework pozwala zespołowi monitorującemu działać jako dostawca i uzyskać uznanie jako zaufany czynnik biznesowy przez dostosowanie do strategicznych celów i potrzeb organizacji.

Zapoznaj się z poniższymi tematami, aby zrozumieć aktualizacje dotyczące najpopularniejszych wytycznych usługi narzędzia ITSM Framework w [wersji 4 i w chmurze obliczeniowej](https://www.axelos.com/case-studies-and-white-papers/itil-4-and-the-cloud), które koncentrują się na dołączeniu do istniejących wskazówek dotyczących biblioteki ITIL z najlepszymi rozwiązaniami od DevOps, Agile i Lean. Należy również wziąć pod uwagę [architekturę referencyjną IT4IT](https://www.opengroup.org/it4it) , która dostarcza alternatywny plan na potrzeby przekształcania go przy użyciu struktury niezależny od procesu.

## <a name="learn-more"></a>Dowiedz się więcej

Aby odnaleźć dodatkowe ścieżki szkoleniowe, przejrzyj [katalog Microsoft Learn](https://docs.microsoft.com/learn/browse). Użyj filtru role, aby wyrównać ścieżki szkoleniowe do roli.