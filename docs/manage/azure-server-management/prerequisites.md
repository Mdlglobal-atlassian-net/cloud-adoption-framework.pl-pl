---
title: Planowanie usług zarządzania serwerem Azure
description: Informacje na temat narzędzi i przygotowanie do zasobów wymaganych do zarządzania usługami zarządzania serwerem Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 1eaa3abcef760d31d2107ddf1922b13d52e8441c
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80434097"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Faza 1: planowanie wymagań wstępnych dla usług zarządzania serwerem Azure

W tej fazie zapoznajesz się z pakietem zarządzania programem Azure Server i planujesz sposób wdrażania zasobów wymaganych do wdrożenia tych rozwiązań do zarządzania.

## <a name="understand-the-tools-and-services"></a>Poznaj narzędzia i usługi

Zapoznaj się z tematem [Narzędzia i usługi zarządzania serwerem Azure](./tools-services.md) , aby zapoznać się z szczegółowym omówieniem:

- Obszary zarządzania, które są związane z trwającymi operacjami platformy Azure.
- Usługi i narzędzia platformy Azure, które ułatwiają obsługę w tych obszarach.

Do spełnienia wymagań związanych z zarządzaniem będziesz używać kilku z tych usług. Te narzędzia są często przywoływane w tym przewodniku.

W poniższych sekcjach omówiono planowanie i przygotowanie wymagane do korzystania z tych narzędzi i usług.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Log Analytics obszar roboczy i planowanie konta usługi Automation

Wiele usług, które będą używane do dołączania usług zarządzania platformy Azure, wymaga obszaru roboczego Log Analytics i połączonego konta Azure Automation.

[Obszar roboczy usługi Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) to unikatowe środowisko do przechowywania danych dziennika usługi Azure Monitor. Każdy obszar roboczy ma własne repozytorium danych i konfigurację. Konfiguracja źródeł danych i rozwiązań umożliwia przechowywanie danych w określonych obszarach roboczych. Rozwiązania do monitorowania platformy Azure wymagają połączenia wszystkich serwerów z obszarem roboczym, co pozwala przechowywać dane dziennika i uzyskiwać do nich dostęp.

Niektóre usługi zarządzania wymagają konta [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) . Korzystając z tego konta i możliwości Azure Automation, można zintegrować usługi platformy Azure i inne systemy publiczne w celu wdrażania i konfigurowania procesów zarządzania serwerem oraz zarządzania nimi.

Następujące usługi zarządzania serwerem Azure wymagają połączonego obszaru roboczego Log Analytics i konta usługi Automation:

- [Update Management platformy Azure](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Change Tracking i spis](https://docs.microsoft.com/azure/automation/change-tracking)
- [Hybrydowy proces roboczy elementu Runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Konfiguracja żądanego stanu](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

Druga faza niniejszych wskazówek koncentruje się na wdrażaniu usług i skryptów automatyzacji. Przedstawiono w nim sposób tworzenia obszaru roboczego Log Analytics i konta usługi Automation. Wskazówki te pokazują również, w jaki sposób używać Azure Policy, aby zapewnić, że nowe maszyny wirtualne są połączone z prawidłowym obszarem roboczym.

W przykładach w tych wskazówkach przyjęto założenie wdrożenia, które nie ma jeszcze serwerów wdrożonych w chmurze. Aby dowiedzieć się więcej na temat zasad i zagadnień związanych z planowaniem obszarów roboczych, zobacz [Zarządzanie danymi dzienników i obszarami roboczymi w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Zagadnienia dotyczące planowania

Podczas przygotowywania obszarów roboczych i kont potrzebnych do dołączania usług zarządzania należy wziąć pod uwagę następujące zagadnienia:

- **Lokalizacje geograficzne platformy Azure i zgodność z przepisami:** Regiony platformy Azure są zorganizowane w *lokalizacje geograficzne*. [Lokalizacja geograficzna platformy Azure](https://azure.microsoft.com/global-infrastructure/geographies) zapewnia, że wymagania dotyczące miejsca zamieszkania, suwerenności, zgodności i odporności są honorowane w granicach geograficznych. Jeśli Twoje obciążenia podlegają jurysdykcji danych lub innych wymaganiach dotyczących zgodności, należy wdrożyć obszary robocze i usługi Automation w regionach w tej samej lokalizacji geograficznej platformy Azure co obsługiwane przez nie zasoby obciążenia.
- **Liczba obszarów roboczych:** Jako zasada identyfikatora GUID należy utworzyć minimalną liczbę obszarów roboczych wymaganych dla każdej lokalizacji geograficznej platformy Azure. Zalecamy co najmniej jeden obszar roboczy dla każdej lokalizacji geograficznej platformy Azure, w której znajdują się zasoby obliczeniowe lub magazynowe. To wstępne wyrównanie pomaga uniknąć problemów z przepisami w przyszłości w przypadku migrowania danych do różnych lokalizacje geograficzne.
- **Przechowywanie i** przenoszące dane: Podczas tworzenia obszarów roboczych lub kont usługi Automation może być również konieczne uwzględnienie zasad przechowywania danych lub wymagań dotyczących pułapek danych. Aby uzyskać więcej informacji na temat tych zasad i dodatkowych zagadnień związanych z planowaniem obszarów roboczych, zobacz [Zarządzanie danymi dzienników i obszarami roboczymi w Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Mapowanie regionu:** Łączenie obszaru roboczego Log Analytics i konta Azure Automation jest obsługiwane tylko w niektórych regionach świadczenia usługi Azure. Na przykład jeśli obszar roboczy Log Analytics jest hostowany w regionie *wschodniego* , należy utworzyć połączone konto usługi Automation w regionie *EastUS2* , które będzie używane z usługami zarządzania. Jeśli masz konto usługi Automation, które zostało utworzone w innym regionie, nie można połączyć się z obszarem roboczym w *Wschodzie*. Wybór regionów wdrożenia może znacząco wpłynąć na wymagania dotyczące lokalizacji geograficznej platformy Azure. Zapoznaj się z [tabelą mapowanie regionów](https://docs.microsoft.com/azure/automation/how-to/region-mappings) , aby określić, który region powinien obsługiwać obszary robocze i konta usługi Automation.
- **Wieloadresowości obszaru roboczego:** Agent Log Analytics platformy Azure obsługuje wieloadresowości w niektórych scenariuszach, ale podczas działania w tej konfiguracji Agent obejmuje kilka ograniczeń i wyzwań. Jeśli firma Microsoft nie zaleca tego konkretnego scenariusza, nie zalecamy konfigurowania wieloadresowości na agencie Log Analytics.

## <a name="resource-placement-examples"></a>Przykłady umieszczania zasobów

Istnieje kilka różnych modeli umożliwiających wybranie subskrypcji, w której umieścisz obszar roboczy Log Analytics i konto usługi Automation. Krótko mówiąc, umieść obszar roboczy i konta usługi Automation w ramach subskrypcji należącej do zespołu odpowiedzialnego za wdrożenie usługi Update Management i usługi Change Tracking i spisu.

Poniżej przedstawiono przykłady niektórych sposobów wdrażania obszarów roboczych i kont usługi Automation.

### <a name="placement-by-geography"></a>Umieszczanie według położenia geograficznego

Małe i średnie środowiska mają jedną subskrypcję i wiele zasobów obejmujących wiele lokalizacje geograficzneów platformy Azure. W przypadku tych środowisk należy utworzyć jeden Log Analytics obszar roboczy i jedno konto Azure Automation w każdej lokalizacji geograficznej.

Możesz utworzyć obszar roboczy i konto Azure Automation, tak jak jedna para w każdej grupie zasobów. Następnie wdróż parę w odpowiedniej lokalizacji geograficznej na maszynach wirtualnych.

Alternatywnie, jeśli zasady zgodności danych nie wymuszają, że zasoby znajdują się w określonych regionach, można utworzyć jedną parę, aby zarządzać wszystkimi maszynami wirtualnymi. Zalecamy również umieszczenie pary obszaru roboczego i konta usługi Automation w osobnych grupach zasobów w celu zapewnienia bardziej szczegółowej kontroli dostępu opartej na rolach (RBAC).

Przykład na poniższym diagramie ma jedną subskrypcję z dwiema grupami zasobów, z których każdy znajduje się w innej lokalizacji geograficznej:

![Model obszarów roboczych dla środowisk małych i średnich](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Umieszczanie w subskrypcji zarządzania

Większe środowiska obejmują wiele subskrypcji i mają centralny dział IT, który jest właścicielem monitorowania i zgodności. W przypadku tych środowisk Utwórz pary obszarów roboczych i kont usługi Automation w ramach subskrypcji zarządzania IT. W tym modelu zasoby maszyn wirtualnych w lokalizacji geograficznej przechowują swoje dane w odpowiednim obszarze roboczym geograficznym w subskrypcji zarządzania IT. Jeśli zespoły aplikacji muszą uruchamiać zadania automatyzacji, ale nie wymagają połączonego obszaru roboczego i konta usługi Automation, mogą tworzyć oddzielne konta usługi Automation w swoich własnych subskrypcjach aplikacji.

![Model obszaru roboczego dla dużych środowisk](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Rozmieszczenie zdecentralizowane

W alternatywnym modelu dla dużych środowisk zespół programistyczny aplikacji może być odpowiedzialny za stosowanie poprawek i zarządzania. W takim przypadku należy umieścić pary obszar roboczy i konto usługi Automation w ramach subskrypcji zespołu aplikacji obok innych zasobów.

  ![Model konta obszaru roboczego dla środowisk zdecentralizowanych](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Tworzenie obszaru roboczego i konta usługi Automation

Po wybraniu najlepszego sposobu umieszczania i organizowania par obszarów roboczych i kont upewnij się, że te zasoby zostały utworzone przed rozpoczęciem procesu dołączania. Przykłady automatyzacji w dalszej części tego przewodnika tworzą dla Ciebie parę obszaru roboczego i konta usługi Automation. Jeśli jednak chcesz dołączyć do programu przy użyciu Azure Portal i nie masz istniejącego obszaru roboczego i pary kont usługi Automation, musisz go utworzyć.

Aby utworzyć obszar roboczy Log Analytics przy użyciu Azure Portal, zobacz [Tworzenie obszaru roboczego](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). Następnie utwórz pasujące konto usługi Automation dla każdego obszaru roboczego, wykonując kroki opisane w temacie [Tworzenie konta Azure Automation](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> Po utworzeniu konta usługi Automation przy użyciu Azure Portal Portal domyślnie próbuje utworzyć konta Uruchom jako dla zasobów Azure Resource Manager i klasyczny model wdrażania. Jeśli nie masz klasycznych maszyn wirtualnych w środowisku i nie jesteś współadministratorem subskrypcji, Portal tworzy konto Uruchom jako dla Menedżer zasobów, ale podczas wdrażania klasycznego konta Uruchom jako zostanie wygenerowany błąd. Jeśli nie planujesz obsługi zasobów klasycznych, możesz zignorować ten błąd.
>
> Możesz również utworzyć konta Uruchom jako przy użyciu [programu PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#creating-a-run-as-account-using-powershell).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak [dołączyć serwery](./onboarding-overview.md) do usług zarządzania serwerem Azure.

> [!div class="nextstepaction"]
> [Dołączanie do usług zarządzania serwerem Azure](./onboarding-overview.md)
