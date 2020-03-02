---
title: Konfigurowanie usług zarządzania serwerem Azure dla subskrypcji
description: Konfigurowanie usług zarządzania serwerem Azure dla subskrypcji
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: dd3cbd9deda4d0325f014be4bc793b59aa973788
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223390"
---
# <a name="configure-azure-server-management-services-at-scale"></a>Konfigurowanie usług zarządzania serwerem Azure na dużą skalę

Należy wykonać te dwa zadania, aby dołączyć usługi zarządzania serwerem Azure do serwerów:
- Wdrażanie agentów usług na serwerach
- Włącz rozwiązania do zarządzania

W tym artykule opisano trzy procesy, które są niezbędne do wykonania tych zadań:

1. Wdróż wymaganych agentów na maszynach wirtualnych platformy Azure za pomocą Azure Policy
1. Wdróż wymaganych agentów na serwerach lokalnych
1. Włączanie i Konfigurowanie rozwiązań

> [!NOTE]
> Przed dołączeniem maszyn wirtualnych do usług zarządzania serwerem Azure Utwórz wymagane [log Analytics obszar roboczy i konto Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

## <a name="use-azure-policy-to-deploy-extensions-to-azure-vms"></a>Używanie Azure Policy do wdrażania rozszerzeń na maszynach wirtualnych platformy Azure

Wszystkie rozwiązania do zarządzania, które zostały omówione w [narzędziu Azure Management Tools i Services](./tools-services.md) , wymagają zainstalowania agenta log Analytics na maszynach wirtualnych platformy Azure i serwerach lokalnych. Możesz dołączać maszyny wirtualne platformy Azure na dużą skalę przy użyciu Azure Policy. Przypisz zasady, aby upewnić się, że Agent jest zainstalowany na maszynach wirtualnych platformy Azure i połączony z prawidłowym obszarem roboczym Log Analytics.

Azure Policy ma wbudowaną [inicjatywę Policy](https://docs.microsoft.com/azure/governance/policy/concepts/definition-structure#initiatives) , która obejmuje agenta log Analytics i [agenta zależności firmy Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), który jest wymagany przez Azure monitor dla maszyn wirtualnych.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Aby uzyskać więcej informacji na temat różnych agentów monitorowania platformy Azure, zobacz [Omówienie agentów monitorowania platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Przypisywanie zasad

Aby przypisać zasady, które opisano w poprzedniej sekcji:

1. W Azure Portal przejdź do pozycji **Azure Policy** > **przypisania** > **Przypisz inicjatywę**.

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale1.png)

2. Na stronie **przypisywanie zasad** Ustaw **zakres** , wybierając przycisk wielokropka (...), a następnie wybierz grupę lub subskrypcję zarządzania. Opcjonalnie możesz wybrać grupę zasobów. Następnie wybierz **pozycję Wybierz** w dolnej części strony **zakres** . Zakres określa, które zasoby lub grupy zasobów są przypisane do zasad.

3. Wybierz wielokropek ( **...** ) obok pozycji **Definicja zasad** , aby otworzyć listę dostępnych definicji. Aby odfiltrować definicje inicjatyw, wprowadź **Azure monitor** w polu **wyszukiwania** :

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale2.png)

4. **Nazwa przypisania** zostanie automatycznie wypełniona przy użyciu wybranej nazwy zasad, ale można ją zmienić. Możesz również dodać opcjonalny opis, aby uzyskać więcej informacji o tym przypisaniu zasad. Pole **przypisane przez** jest wypełniane automatycznie na podstawie tego, kto jest zalogowany. To pole jest opcjonalne i obsługuje wartości niestandardowe.

5. Dla tych zasad wybierz **log Analytics obszar roboczy** , który ma zostać skojarzony z agentem usługi log Analytics.

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale3.png)

6. Zaznacz pole wyboru **zarządzana lokalizacja tożsamości** . Jeśli te zasady mają typ [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), do wdrożenia zasad będzie wymagana tożsamość zarządzana. W portalu konto zostanie utworzone zgodnie z wyborem pola wyboru.

7. Wybierz opcję **Przypisz**.

Po zakończeniu pracy Kreatora przypisanie zasad zostanie wdrożone w środowisku. Zastosowanie zasad może potrwać do 30 minut. Aby przetestować tę funkcję, Utwórz nowe maszyny wirtualne po 30 minutach i sprawdź, czy Microsoft Monitoring Agent jest domyślnie włączona na maszynie wirtualnej.

## <a name="install-agents-on-on-premises-servers"></a>Instalowanie agentów na serwerach lokalnych

> [!NOTE]
> Przed dołączeniem usług zarządzania serwerem Azure do serwerów należy utworzyć wymagany [obszar roboczy log Analytics i konto Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

W przypadku serwerów lokalnych należy ręcznie pobrać i zainstalować [agenta log Analytics oraz agenta zależności firmy Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) i skonfigurować go tak, aby łączył się z prawidłowym obszarem roboczym. Należy określić identyfikator obszaru roboczego i informacje o kluczu. Aby uzyskać te informacje, przejdź do obszaru roboczego Log Analytics w Azure Portal, a następnie wybierz pozycję **ustawienia** > **Ustawienia zaawansowane**.

![Zrzut ekranu przedstawiający zaawansowane ustawienia obszaru roboczego Log Analytics w Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Włączanie i Konfigurowanie rozwiązań

Korzystanie z rozwiązań wymaga skonfigurowania obszaru roboczego usługi Log Analytics. Do dołączania maszyn wirtualnych platformy Azure i serwerów lokalnych zostaną pobrane rozwiązania z obszarów roboczych Log Analytics, do których są połączone.

### <a name="update-management"></a>Zarządzanie aktualizacjami

Rozwiązania Update Management, Change Tracking i spisu wymagają zarówno obszaru roboczego Log Analytics, jak i konta usługi Automation. Aby upewnić się, że te zasoby są prawidłowo skonfigurowane, Zalecamy dołączenie do konta usługi Automation. Aby uzyskać więcej informacji, zobacz Dołączanie [rozwiązań Update Management, Change Tracking i spisu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Zalecamy włączenie rozwiązania Update Management dla wszystkich serwerów. Update Management jest bezpłatny dla maszyn wirtualnych platformy Azure i serwerów lokalnych. Jeśli włączysz Update Management za pomocą konta usługi Automation, w obszarze roboczym zostanie utworzona [Konfiguracja zakresu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) . Należy ręcznie zaktualizować zakres w celu uwzględnienia maszyn, które są objęte usługą Update Management.

Aby uwzględnić istniejące serwery oraz serwery w przyszłości, należy usunąć konfigurację zakresu. W tym celu Wyświetl konto usługi Automation w Azure Portal. Wybierz pozycję **Update Management** > **Zarządzanie komputerem** > **Włącz na wszystkich dostępnych i przyszłych maszynach**. To ustawienie umożliwia wszystkim maszynom wirtualnym platformy Azure, które są połączone z obszarem roboczym używanie Update Management.

![Zrzut ekranu przedstawiający Update Management w Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Rozwiązania Change Tracking i spisu

Aby dołączyć rozwiązania Change Tracking i spisu, wykonaj te same czynności co w przypadku Update Management. Aby uzyskać więcej informacji na temat sposobu dołączania tych rozwiązań z konta usługi Automation, zobacz Dołączanie [rozwiązań Update Management, Change Tracking i spisu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Rozwiązanie Change Tracking jest bezpłatne dla maszyn wirtualnych platformy Azure i kosztów $6 na węzeł miesięcznie dla serwerów lokalnych. Ten koszt obejmuje konfigurację Change Tracking, spisu i żądanego stanu. Jeśli chcesz zarejestrować tylko określone serwery lokalne, możesz zrezygnować z tych serwerów. Zalecamy dołączenie wszystkich serwerów produkcyjnych.

#### <a name="opt-in-via-the-azure-portal"></a>Zezwól na za pośrednictwem Azure Portal

1. Przejdź do konta usługi Automation z włączonym Change Tracking i spisem.
2. Wybierz pozycję **śledzenie zmian**.
3. Wybierz pozycję **Zarządzaj maszynami** w prawym górnym okienku.
4. Wybierz pozycję **Włącz na wybranych maszynach**. Następnie wybierz pozycję **Dodaj** obok nazwy maszyny.
5. Wybierz pozycję **Włącz** , aby włączyć rozwiązanie dla tych maszyn.

![Zrzut ekranu przedstawiający Change Tracking w Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Zgoda na korzystanie z zapisanych wyszukiwań

Alternatywnie można skonfigurować konfigurację zakresu do wyboru w przypadku serwerów lokalnych. Konfiguracja zakresu używa zapisanych wyszukiwań.

Aby utworzyć lub zmodyfikować zapisane wyszukiwanie, wykonaj następujące kroki:

1. Przejdź do obszaru roboczego Log Analytics, który jest połączony z kontem usługi Automation skonfigurowanym w poprzednich krokach.

1. W obszarze **Ogólne**wybierz pozycję **zapisane wyszukiwania**.

1. W polu **Filtr** wprowadź **Change Tracking** , aby odfiltrować listę zapisanych wyszukiwań. W wynikach wybierz pozycję **MicrosoftDefaultComputerGroup**.

1. Wprowadź nazwę komputera lub VMUUID, aby uwzględnić komputery, na których chcesz zrezygnować Change Tracking.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Nazwa serwera musi dokładnie pasować do wartości w wyrażeniu i nie powinna zawierać sufiksu nazwy domeny.

1. Wybierz pozycję **Zapisz**. Domyślnie konfiguracja zakresu jest połączona z **MicrosoftDefaultComputerGroup** zapisanym wyszukiwaniem. Zostanie ona automatycznie zaktualizowana.

### <a name="azure-activity-log"></a>Dziennik aktywności platformy Azure

[Dziennik aktywności platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) jest również częścią Azure monitor. Zapewnia wgląd w zdarzenia na poziomie subskrypcji występujące na platformie Azure.

Aby zaimplementować to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi**, a następnie wybierz pozycję **Management + zarządzanie** **rozwiązaniami** > .
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj **Activity Log Analytics** i wybierz ją.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agent Health

Rozwiązanie Agent Health Log Analytics platformy Azure przedstawia raporty dotyczące kondycji, wydajności i dostępności serwerów z systemami Windows i Linux.

Aby zaimplementować to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi**, a następnie wybierz pozycję **Management + zarządzanie** **rozwiązaniami** > .
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj **usługę Azure log Analytics Agent Health** i wybierz ją.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

Po zakończeniu tworzenia wystąpienie zasobu obszaru roboczego wyświetla **AgentHealthAssessment** w przypadku wybrania opcji **Wyświetl** > **rozwiązania**.

### <a name="antimalware-assessment"></a>Ocena oprogramowania chroniącego przed złośliwym kodem

Antimalware Assessment rozwiązanie pomaga identyfikować serwery, które są zainfekowane lub w zwiększonej ryzyku zainfekowania przez złośliwe oprogramowanie.

Aby zaimplementować to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi**, wybierz pozycję Wybierz **zarządzanie i nadzór** > **rozwiązania**.
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj, a następnie wybierz pozycję **Antimalware Assessment**.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

Po zakończeniu tworzenia wystąpienie zasobu obszaru roboczego wyświetli **oprogramowanie chroniące przed złośliwym kodem** w przypadku wybrania opcji **Wyświetl** > **rozwiązania**.

### <a name="azure-monitor-for-vms"></a>Usługa Azure Monitor dla maszyn wirtualnych

[Azure monitor dla maszyn wirtualnych](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) można włączyć za pomocą strony widok dla wystąpienia maszyny wirtualnej, zgodnie z opisem w temacie [Włączanie usług zarządzania na jednej maszynie wirtualnej do oceny](./onboard-single-vm.md). Rozwiązań nie należy włączać bezpośrednio na stronie **rozwiązań** , podobnie jak w przypadku innych rozwiązań opisanych w tym artykule. W przypadku wdrożeń na dużą skalę może być łatwiejsze używanie [automatyzacji](./onboarding-automation.md) do włączania prawidłowych rozwiązań w obszarze roboczym. 

### <a name="azure-security-center"></a>Azure Security Center

Zalecamy, aby dołączyć wszystkie serwery co najmniej do Azure Security Center warstwy *bezpłatna* . Ta opcja zapewnia podstawowy poziom oceny zabezpieczeń i zalecenia dotyczące działań związanych z zabezpieczeniami dla danego środowiska. W przypadku uaktualnienia do warstwy *standardowa* uzyskasz dodatkowe korzyści, które są szczegółowo omówione na [stronie cennika Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Aby włączyć Azure Security Center warstwy Bezpłatna, wykonaj następujące kroki:

1. Przejdź do strony portalu **Security Center** .
2. W obszarze **zasady &AMP; zgodność**wybierz pozycję **zasady zabezpieczeń**.
3. Znajdź zasób obszaru roboczego Log Analytics, który został utworzony w okienku po prawej stronie.
4. Wybierz pozycję **Edytuj ustawienia** dla tego obszaru roboczego.
5. Wybierz **warstwę cenową**.
6. Wybierz opcję **bezpłatna** .
7. Wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak używać automatyzacji do dołączania serwerów i tworzenia alertów.

> [!div class="nextstepaction"]
> [Zautomatyzowana konfiguracja dołączania i alertu](./onboarding-automation.md)
