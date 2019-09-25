---
title: Konfigurowanie usług zarządzania platformy Azure dla subskrypcji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Konfigurowanie usług zarządzania platformy Azure dla subskrypcji
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a5b1d551f52ae8800e9a29d4c8a92c14965645cc
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221501"
---
# <a name="configure-azure-management-services-at-scale"></a>Konfigurowanie usług zarządzania platformy Azure na dużą skalę

Dołączanie usług zarządzania platformy Azure do serwerów obejmuje dwa zadania: wdrażanie agentów usług na serwerach i włączanie rozwiązań do zarządzania. W tym artykule opisano następujące procesy, które umożliwią wykonanie następujących zadań:

- [Wdrażanie wymaganych agentów na maszynach wirtualnych platformy Azure przy użyciu Azure Policy](#deploy-extensions-to-azure-vms-using-azure-policy)
- [Wdrażanie wymaganych agentów na serwerach lokalnych](#install-required-agents-on-on-premises-servers)
- [Włączanie i Konfigurowanie rozwiązań](#enable-and-configure-solutions)

> [!NOTE]
> Przed dołączeniem maszyn wirtualnych do usług zarządzania platformy Azure Utwórz wymagane [obszary robocze log Analytics i Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

## <a name="deploy-extensions-to-azure-vms-using-azure-policy"></a>Wdrażanie rozszerzeń na maszynach wirtualnych platformy Azure przy użyciu Azure Policy

Wszystkie rozwiązania do zarządzania omówione w ramach [narzędzi i usług zarządzania platformy Azure](./tools-services.md) wymagają zainstalowania agenta log Analytics na maszynach wirtualnych platformy Azure i na serwerach lokalnych. Możesz dołączać maszyny wirtualne platformy Azure na dużą skalę przy użyciu Azure Policy. Przypisz zasady, aby upewnić się, że Agent jest zainstalowany na wszystkich maszynach wirtualnych platformy Azure i połączony z prawidłowym obszarem roboczym Log Analytics.

Azure Policy ma wbudowaną inicjatywę [Policy](/azure/governance/policy/index#initiative-definition) , która obejmuje zarówno agenta log Analytics, jak i [agenta zależności Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), który jest wymagany przez Azure monitor dla maszyn wirtualnych.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Aby uzyskać więcej informacji na temat różnych agentów monitorowania platformy Azure, zobacz [Omówienie agentów monitorowania platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Przypisz zasady

Aby przypisać zasady wymienione w poprzedniej sekcji:

1. W Azure Portal przejdź do pozycji **Azure Policy** > **przypisania** > **Przypisz inicjatywę**.

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale1.png)

2. Na stronie **przypisywanie zasad** wybierz **zakres** , klikając przycisk wielokropka (...), a następnie wybierz grupę lub subskrypcję zarządzania. Opcjonalnie możesz wybrać grupę zasobów. Zakres określa, które zasoby lub grupy zasobów są przypisane do zasad. Następnie wybierz **pozycję Wybierz** w dolnej części strony **zakres** .

3. Wybierz wielokropek (...) obok pozycji **Definicja zasad** , aby otworzyć listę dostępnych definicji. Definicję inicjatywy można filtrować, wprowadzając **Azure monitor** w polu **wyszukiwania** :

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale2.png)

4. **Nazwa przypisania** zostanie automatycznie wypełniona przy użyciu wybranej nazwy zasad, ale można ją zmienić. Możesz również dodać opcjonalny opis, aby uzyskać więcej informacji o tym przypisaniu zasad. Pole **przypisane przez** jest wypełniane automatycznie na podstawie tego, kto jest zalogowany. To pole jest opcjonalne i można wprowadzić wartości niestandardowe.

5. Dla tych zasad wybierz **log Analytics obszar roboczy** , który ma zostać skojarzony z agentem usługi log Analytics.

    ![Zrzut ekranu przedstawiający interfejs zasad portalu](./media/onboarding-at-scale3.png)

6. Sprawdź **lokalizację zarządzanej tożsamości**. Jeśli te zasady są typu [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), do wdrożenia zasad będzie wymagane tożsamość zarządzana. W portalu konto zostanie utworzone, jak wskazano zaznaczenie pola wyboru.

7. Wybierz opcję **Przypisz**.

Po zakończeniu pracy Kreatora przypisanie zasad zostanie wdrożone w środowisku. Zastosowanie zasad może potrwać do 30 minut. Możesz go przetestować, tworząc nowe maszyny wirtualne po 30 minutach, a następnie sprawdzając, czy Microsoft Monitoring Agent (MMA) jest domyślnie włączona na maszynie wirtualnej.

## <a name="install-required-agents-on-on-premises-servers"></a>Instalowanie wymaganych agentów na serwerach lokalnych

> [!NOTE]
> Przed dołączeniem serwerów do usług zarządzania platformy Azure Utwórz wymagany [obszar roboczy log Analytics i konto Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) .

W przypadku serwerów lokalnych należy ręcznie pobrać i zainstalować [agenta log Analytics oraz agenta zależności firmy Microsoft](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) i skonfigurować go tak, aby łączył się z prawidłowym obszarem roboczym. Aby to zrobić, określ identyfikator obszaru roboczego i informacje o kluczu, które można znaleźć, przechodząc do obszaru roboczego log Analytics w Azure Portal i wybierając pozycję **Ustawienia** > **Zaawansowane ustawienia**.

![Zrzut ekranu przedstawiający zaawansowane ustawienia obszaru roboczego Log Analytics w Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Włączanie i Konfigurowanie rozwiązań

Aby włączyć rozwiązania, należy skonfigurować obszar roboczy Log Analytics. Do dołączania maszyn wirtualnych platformy Azure i serwerów lokalnych zostaną pobrane rozwiązania z obszarów roboczych Log Analytics, do których są połączone.

W tej sekcji omówiono następujące rozwiązania:

- [Zarządzanie aktualizacjami](#update-management)
- [Change Tracking i spis](#change-tracking-and-inventory-solutions)
- [Dziennik aktywności platformy Azure](#azure-activity-log)
- [Agent Health Log Analytics platformy Azure](#azure-log-analytics-agent-health)
- [Ocena oprogramowania chroniącego przed złośliwym kodem](#antimalware-assessment)
- [Azure Monitor dla maszyn wirtualnych](#azure-monitor-for-vms)
- [Azure Security Center](#azure-security-center)

### <a name="update-management"></a>Zarządzanie aktualizacjami

Rozwiązania Update Management, Change Tracking i spisu wymagają zarówno obszaru roboczego Log Analytics, jak i konta usługi Automation. Aby upewnić się, że te zasoby są prawidłowo skonfigurowane, Zalecamy dołączenie do konta usługi Automation. Aby uzyskać więcej informacji, zobacz Dołączanie [rozwiązań Update Management, Change Tracking i spisu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Zalecamy włączenie rozwiązania Update Management dla wszystkich serwerów. Update Management jest bezpłatny dla maszyn wirtualnych platformy Azure i serwerów lokalnych. Jeśli włączysz Update Management za pomocą konta usługi Automation, w obszarze roboczym zostanie utworzona [Konfiguracja zakresu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) . Należy ręcznie zaktualizować zakres w celu uwzględnienia maszyn objętych usługą aktualizacji.

Aby uwzględnić wszystkie istniejące serwery, a także serwery w przyszłości, należy usunąć konfigurację zakresu. Aby to zrobić, Wyświetl konto usługi Automation w Azure Portal i wybierz pozycję **Update Management** > **Zarządzanie komputerem** > **na wszystkich dostępnych i przyszłych maszynach**. Włączenie tego ustawienia umożliwia wszystkim maszynom wirtualnym platformy Azure podłączonym do obszaru roboczego używanie Update Management.

![Zrzut ekranu przedstawiający Update Management w Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Rozwiązania Change Tracking i spisu

Aby dołączyć rozwiązania Change Tracking i spisu, wykonaj te same czynności co w przypadku Update Management. Aby uzyskać więcej informacji na temat dołączania tych rozwiązań z konta usługi Automation, zobacz Dołączanie [rozwiązań Update Management, Change Tracking i spisu](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Rozwiązanie Change Tracking jest bezpłatne dla maszyn wirtualnych platformy Azure i kosztów $6 na węzeł miesięcznie dla serwerów lokalnych. Ten koszt obejmuje konfigurację Change Tracking, spisu i żądanego stanu. Jeśli chcesz zarejestrować tylko określone serwery lokalne, możesz zrezygnować z tych serwerów. Zalecamy dołączenie wszystkich serwerów produkcyjnych.

#### <a name="opt-in-via-the-azure-portal"></a>Zezwól na za pośrednictwem Azure Portal

1. Przejdź do konta usługi Automation z włączonym Change Tracking i spisem.
2. Wybierz pozycję **śledzenie zmian**.
3. Wybierz pozycję **Zarządzaj maszynami** w prawym górnym okienku.
4. Wybierz pozycję **Włącz na wybranych maszynach**i wybierz maszyny, które mają być włączone, klikając przycisk **Dodaj** obok nazwy maszyny.
5. Wybierz pozycję **Włącz** , aby włączyć rozwiązanie dla tych maszyn.

![Zrzut ekranu przedstawiający Change Tracking w Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Zgoda na korzystanie z zapisanych wyszukiwań

Alternatywnie można skonfigurować konfigurację zakresu do wyboru w przypadku serwerów lokalnych. Konfiguracja zakresu używa zapisanych wyszukiwań.

Aby utworzyć lub zmodyfikować zapisane wyszukiwanie, wykonaj następujące czynności:

1. Przejdź do obszaru roboczego Log Analytics, który jest połączony z kontem usługi Automation skonfigurowanym w poprzednich krokach.

2. W obszarze **Ogólne**wybierz pozycję **zapisane wyszukiwania**.

3. W polu **Filtr** wprowadź **Change Tracking** , aby odfiltrować listę zapisanych wyszukiwań. W wynikach wybierz pozycję **MicrosoftDefaultComputerGroup**.

4. Wprowadź nazwę komputera lub VMUUID, aby uwzględnić komputery, na których chcesz zrezygnować Change Tracking.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > Nazwa serwera musi być dokładnie zgodna z wartością uwzględnioną w wyrażeniu i nie powinna zawierać sufiksu nazwy domeny.

5. Wybierz pozycję **Zapisz**.

6. Domyślnie konfiguracja zakresu jest połączona z **MicrosoftDefaultComputerGroup** zapisanym wyszukiwaniem i zostanie automatycznie zaktualizowana.

### <a name="azure-activity-log"></a>Dziennik aktywności platformy Azure

[Dziennik aktywności platformy Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) jest również częścią Azure monitor. Zapewnia wgląd w zdarzenia na poziomie subskrypcji występujące na platformie Azure.

Aby dodać to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi** i wybierz pozycję **Zarządzanie +**  > **rozwiązania**ładu.
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj **Activity Log Analytics** i wybierz ją.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

### <a name="azure-log-analytics-agent-health"></a>Azure Log Analytics Agent Health

Rozwiązanie Agent Health Log Analytics platformy Azure zapewnia wgląd w kondycję, wydajność i dostępność serwerów z systemami Windows i Linux.

Aby dodać to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi** i wybierz pozycję **Zarządzanie +**  > **rozwiązania**ładu.
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj **usługę Azure log Analytics Agent Health** i wybierz ją.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

Po zakończeniu tworzenia wystąpienie zasobu obszaru roboczego wyświetla **AgentHealthAssessment** w przypadku wybrania opcji **Wyświetl** > **rozwiązania**.

### <a name="antimalware-assessment"></a>Ocena oprogramowania chroniącego przed złośliwym kodem

Antimalware Assessment rozwiązanie pomaga identyfikować serwery, które są zainfekowane lub w zwiększonej ryzyku zainfekowania przez złośliwe oprogramowanie.

Aby dodać to rozwiązanie:

1. W Azure Portal Otwórz **wszystkie usługi** i wybierz pozycję **Zarządzanie +**  > **rozwiązania**ładu.
2. W widoku **rozwiązania** wybierz pozycję **Dodaj**.
3. Wyszukaj **Antimalware Assessment** i wybierz ją.
4. Wybierz pozycję **Utwórz**.

Należy określić **nazwę obszaru** roboczego, który został utworzony w poprzedniej sekcji, w której jest włączone rozwiązanie.

Po zakończeniu tworzenia wystąpienie zasobu obszaru roboczego wyświetli **oprogramowanie chroniące przed złośliwym kodem** w przypadku wybrania opcji **Wyświetl** > **rozwiązania**.

### <a name="azure-monitor-for-vms"></a>Usługa Azure Monitor dla maszyn wirtualnych

[Azure monitor dla maszyn wirtualnych](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) można włączyć za pomocą strony widok dla wystąpienia maszyny wirtualnej, zgodnie z opisem w poprzednim artykule, [Włącz usługi zarządzania na jednej maszynie wirtualnej do oceny](./onboard-single-vm.md). Rozwiązań nie należy włączać bezpośrednio na stronie **rozwiązań** , jak w przypadku innych rozwiązań opisanych w tym artykule. W przypadku wdrożeń na dużą skalę może być łatwiejsze używanie [automatyzacji](./onboarding-automation.md) do włączania prawidłowych rozwiązań w obszarze roboczym.

### <a name="azure-security-center"></a>Azure Security Center

W tych wskazówkach zalecamy, aby domyślnie dołączyć wszystkie serwery do Azure Security Center warstwy *bezpłatna* . Ta opcja zapewnia podstawowy poziom oceny zabezpieczeń i zalecenia dotyczące działań związanych z zabezpieczeniami dla danego środowiska. Uaktualnienie do warstwy *standardowa* Security Center oferuje dodatkowe korzyści, które zostały szczegółowo omówione na [stronie cennika Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Aby włączyć Azure Security Center warstwy Bezpłatna, wykonaj następujące czynności:

1. Przejdź do strony portalu **Security Center** .
2. Wybierz pozycję **zasady zabezpieczeń** w obszarze **zasady & zgodność**.
3. Znajdź zasób obszaru roboczego Log Analytics, który został utworzony w okienku po prawej stronie.
4. Wybierz pozycję **Edytuj ustawienia >** dla tego obszaru roboczego.
5. Wybierz **warstwę cenową**.
6. Wybierz opcję **bezpłatna** .
7. Wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak używać automatyzacji do dołączania serwerów i tworzenia alertów.

> [!div class="nextstepaction"]
> [Zautomatyzowana konfiguracja dołączania i alertu](./onboarding-automation.md)
