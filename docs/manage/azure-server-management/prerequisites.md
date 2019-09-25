---
title: Planowanie wymagań wstępnych dotyczących usług zarządzania serwerem Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wstępnie wymagane narzędzia i planowanie dla usług zarządzania serwerem Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 17538d7c49278a00a5927b0110a2591a03d59e5c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221470"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Etap 1: Planowanie wymagań wstępnych dotyczących usług zarządzania serwerem Azure

W tej fazie zapoznajesz się z pakietem zarządzania programem Azure Server i planujesz sposób wdrażania zasobów wymaganych do wdrożenia tych rozwiązań do zarządzania.

## <a name="understand-the-tools-and-services"></a>Poznaj narzędzia i usługi

Przejrzyj [Narzędzia i usługi zarządzania serwerem Azure](./tools-services.md) , aby zapoznać się ze szczegółowymi informacjami na temat obszarów zarządzania, które są związane z trwającymi operacjami platformy Azure i usługami i narzędziami platformy Azure, które pomagają Ci w tych obszarach. Spełnienie wymagań związanych z zarządzaniem będzie wymagało użycia kilku z tych usług jednocześnie. Te narzędzia są często przywoływane w tym przewodniku.

W poniższych sekcjach omówiono planowanie i przygotowanie wymagane do korzystania z tych narzędzi i usług.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Log Analytics obszar roboczy i planowanie konta usługi Automation

Wiele usług, które będą używane do dołączania usług zarządzania platformy Azure, wymaga obszaru roboczego Log Analytics i połączonego konta Azure Automation.

[Obszar roboczy log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) jest unikatowym środowiskiem do przechowywania Azure monitor danych dziennika. Każdy obszar roboczy ma własne repozytorium danych i konfigurację. Źródła danych i rozwiązania są skonfigurowane do przechowywania danych w określonych obszarach roboczych. Rozwiązania do monitorowania platformy Azure wymagają, aby wszystkie serwery były połączone z obszarem roboczym, dzięki czemu można przechowywać dane dziennika i uzyskiwać do nich dostęp.

Niektóre usługi zarządzania wymagają konta [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) . Korzystając z tych kont i Azure Automation możliwości, można zintegrować usługi platformy Azure i inne systemy publiczne w celu wdrażania i konfigurowania procesów zarządzania serwerem oraz zarządzania nimi.

Następujące usługi zarządzania serwerem Azure wymagają połączonego obszaru roboczego Log Analytics i konta usługi Automation do działania:

- [Update Management platformy Azure](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Change Tracking i spis](https://docs.microsoft.com/azure/automation/change-tracking)
- [Hybrydowy proces roboczy elementu Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Konfiguracja żądanego stanu](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

Druga faza niniejszych wskazówek koncentruje się na wdrażaniu usług i skryptów automatyzacji. Przedstawiono w nim sposób tworzenia obszaru roboczego Log Analytics i konta usługi Automation. Wskazówki te pokazują również, jak używać Azure Policy, aby zapewnić, że nowe maszyny wirtualne są połączone z prawidłowym obszarem roboczym.

Przykłady omówione w tym przewodniku zakładają wdrożenie, które nie ma jeszcze serwerów wdrożonych w chmurze. Aby dowiedzieć się więcej na temat zasad i zagadnień związanych z planowaniem obszarów roboczych, zobacz [Zarządzanie danymi dzienników i obszarami roboczymi w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Zagadnienia dotyczące planowania

Podczas przygotowywania obszarów roboczych i kont utworzonych w celu dołączania usług zarządzania należy zapoznać się z następującymi dyskusjami o problemach:

- **Lokalizacje geograficzne platformy Azure i zgodność z przepisami**. Regiony platformy Azure są zorganizowane w *lokalizacje geograficzne*. [Lokalizacja geograficzna platformy Azure](https://azure.microsoft.com/global-infrastructure/geographies) zapewnia, że wymagania dotyczące miejsca zamieszkania, suwerenności, zgodności i odporności są honorowane w granicach geograficznych. Jeśli obciążenia podlegają suwerenności danych lub innych wymaganiach dotyczących zgodności, należy wdrożyć obszary robocze i usługi Automation w regionach w tej samej lokalizacji geograficznej platformy Azure, w której są obsługiwane zasoby obciążeń.
- **Liczba obszarów roboczych**. Jako zasada identyfikatora GUID należy utworzyć minimalną liczbę obszarów roboczych wymaganych dla każdej lokalizacji geograficznej platformy Azure. Zalecamy co najmniej jeden obszar roboczy dla każdej lokalizacji geograficznej platformy Azure, w której znajdują się zasoby obliczeniowe lub magazynowe. To wstępne wyrównanie pomaga uniknąć problemów z przepisami w przyszłości podczas migrowania danych do różnych lokalizacje geograficzne.
- **Przechowywanie i limitowanie danych**. Podczas tworzenia obszarów roboczych lub kont usługi Automation może być również konieczne uwzględnienie zasad przechowywania danych lub wymagań dotyczących pułapek danych. Aby uzyskać więcej informacji na temat tych zasad i dodatkowych zagadnień związanych z planowaniem obszarów roboczych, zobacz [Zarządzanie danymi dzienników i obszarami roboczymi w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Mapowanie regionów**. Łączenie obszaru roboczego Log Analytics i konta Azure Automation jest obsługiwane tylko w niektórych regionach świadczenia usługi Azure. Na przykład jeśli obszar roboczy Log Analytics jest hostowany w regionie *wschodniego* , należy utworzyć połączone konto usługi Automation w regionie *EastUS2* , aby można było go używać z usługami zarządzania. Jeśli masz konto usługi Automation, które zostało utworzone w innym regionie, nie będzie można połączyć się z obszarem roboczym w *Wschodzie*. Wybór regionów wdrożenia może znacząco wpłynąć na wymagania dotyczące lokalizacji geograficznej platformy Azure. Zapoznaj się z [tabelą mapowanie regionów](https://docs.microsoft.com/azure/automation/how-to/region-mappings) , aby określić, który region powinien obsługiwać obszary robocze i konta usługi Automation.
- **Wieloadresowości obszaru roboczego**. Agent Log Analytics obsługuje wieloadresowości w niektórych scenariuszach, ale podczas uruchamiania w tej konfiguracji Agent obejmuje kilka ograniczeń i problemów. Chyba że firma Microsoft zaleca korzystanie z usługi wieloadresowości na potrzeby danego scenariusza, nie zalecamy konfigurowania wieloadresowości na agencie Log Analytics.

## <a name="resource-placement-examples"></a>Przykłady umieszczania zasobów

Istnieje kilka różnych modeli umożliwiających wybranie subskrypcji, w której umieścisz obszar roboczy Log Analytics i konto usługi Automation. W krótkim przypadku należy umieścić obszary robocze i usługi Automation w ramach subskrypcji należącej do zespołu, która jest odpowiedzialna za implementację usług Update Management i Change Tracking i spisu.

W poniższych przykładach pokazano, jak można wdrożyć obszary robocze i konta usługi Automation.

### <a name="placement-by-geography"></a>Umieszczanie według położenia geograficznego

W przypadku małych i średnich środowisk z pojedynczą subskrypcją i kilku zasobów obejmujących wiele lokalizacje geograficzneów platformy Azure Utwórz jeden Log Analytics obszar roboczy i jedno konto Azure Automation w każdej lokalizacji geograficznej.

Można utworzyć obszar roboczy i konto Azure Automation — jedną parę — w każdej grupie zasobów i wdrożyć parę w odpowiedniej lokalizacji geograficznej na maszynach wirtualnych. Alternatywnie, jeśli zasady zgodności danych nie określają, że zasoby znajdują się w określonych regionach, można utworzyć jedną parę, aby zarządzać wszystkimi maszynami wirtualnymi. Zalecamy również umieszczenie pary obszar roboczy i konto usługi Automation w osobnych grupach zasobów w celu zapewnienia bardziej szczegółowej kontroli dostępu opartej na rolach (RBAC).

Przykład na poniższym diagramie ma jedną subskrypcję z dwiema grupami zasobów, z których każdy znajduje się w innej lokalizacji geograficznej.

![Model obszarów roboczych dla środowisk małych i średnich](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Umieszczanie w subskrypcji zarządzania

W przypadku większych środowisk obejmujących wiele subskrypcji i scentralizowanego działu INFORMATYCZNego, który jest właścicielem monitorowania i zgodności, Utwórz pary obszarów roboczych i kont usługi Automation w ramach subskrypcji zarządzania IT. W tym modelu zasoby maszyny wirtualnej w lokalizacji geograficznej przechowują swoje dane w odpowiednim obszarze roboczym geograficznym w subskrypcji zarządzania IT. Zespoły aplikacji, które wymagają uruchamiania zadań automatyzacji, ale którzy nie wymagają połączonego obszaru roboczego i konta usługi Automation, mogą tworzyć oddzielne konta usługi Automation w swoich własnych subskrypcjach aplikacji.

![Model obszaru roboczego dla dużych środowisk](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Rozmieszczenie zdecentralizowane

W alternatywnym modelu dla dużych środowisk odpowiedzialność za stosowanie poprawek i zarządzanie może należeć do zespołu deweloperów aplikacji. W takim przypadku należy umieścić pary obszarów roboczych i automatyzacji w subskrypcjach zespołu aplikacji obok innych zasobów.

  ![Model konta obszaru roboczego dla środowisk zdecentralizowanych](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Tworzenie obszaru roboczego i konta usługi Automation

Po wybraniu najlepszego sposobu umieszczania i organizowania par obszarów roboczych i kont należy upewnić się, że te zasoby zostały utworzone przed rozpoczęciem procesu dołączania. Przykłady automatyzacji zawarte w dalszej części tego przewodnika tworzą dla Ciebie parę obszaru roboczego i konta usługi Automation. Jeśli jednak nie masz istniejącej pary obszaru roboczego i konta usługi Automation, musisz ją utworzyć, jeśli chcesz dołączyć do niej przy użyciu portalu.

Aby utworzyć obszar roboczy Log Analytics za pomocą Azure Portal, zobacz [Tworzenie obszaru roboczego](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Następnie utwórz pasujące konto usługi Automation dla każdego obszaru roboczego, wykonując kroki opisane w temacie [Tworzenie konta Azure Automation](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> Podczas tworzenia konta usługi Automation za pomocą Azure Portal, domyślne zachowanie próbuje utworzyć konta Uruchom jako dla zasobów Azure Resource Manager i klasyczny model wdrażania. Jeśli nie masz klasycznych maszyn wirtualnych w środowisku i nie jesteś współadministratorem subskrypcji, w portalu zostanie utworzone konto Uruchom jako dla Menedżer zasobów, ale podczas wdrażania klasycznego konta Uruchom jako zostanie wygenerowany błąd. Jeśli nie planujesz obsługi zasobów klasycznych, możesz zignorować ten błąd.
>
> Możesz również utworzyć konta Uruchom jako przy użyciu [programu PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#create-run-as-account-using-powershell).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [dołączyć serwery](./onboarding-overview.md) do usług zarządzania platformy Azure.

> [!div class="nextstepaction"]
> [Dołączanie do usług zarządzania serwerem Azure](./onboarding-overview.md)
