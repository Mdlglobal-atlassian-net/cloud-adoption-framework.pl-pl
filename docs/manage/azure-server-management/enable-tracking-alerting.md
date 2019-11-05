---
title: Włącz śledzenie i alerty dla zmian krytycznych
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Włącz śledzenie i alerty dla zmian krytycznych
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 32f0a5f9b5d0fabe9e1989e54293b74aeb130b96
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73565431"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Włącz śledzenie i alerty dla zmian krytycznych

Usługa Azure Change Tracking i spis zapewniają alerty dotyczące stanu konfiguracji środowiska hybrydowego i wszelkich zmian w tym środowisku. Można monitorować krytyczne zmiany plików, usług, oprogramowania i rejestru, które mogą mieć wpływ na wdrożone serwery.

Domyślnie usługa spisu Azure Automation nie monitoruje plików ani ustawień rejestru. Rozwiązanie udostępnia listę kluczy rejestru, które zalecamy do monitorowania. Aby wyświetlić tę listę, przejdź do konta usługi Automation w Azure Portal i wybierz pozycję **spis** > **Edytuj ustawienia**.

![Zrzut ekranu przedstawiający Widok spisu Azure Automation w Azure Portal](./media/change-tracking1.png)

Aby uzyskać więcej informacji na temat poszczególnych kluczy rejestru, zobacz [śledzenie zmian kluczy rejestru](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Możesz obliczyć i włączyć każdy klucz, wybierając go. To ustawienie jest stosowane do wszystkich maszyn wirtualnych włączonych w bieżącym obszarze roboczym.

Można także śledzić krytyczne zmiany plików. Na przykład możesz chcieć śledzić plik C:\windows\System32\drivers\etc\HOSTS, ponieważ system operacyjny używa go do mapowania nazw hostów na adresy IP. Wszelkie zmiany w tym pliku mogą spowodować problemy z łącznością lub przekierować ruch do niebezpiecznych witryn sieci Web.

Aby włączyć śledzenie zawartości plików dla plików Hosts, wykonaj kroki opisane w temacie [Włączanie śledzenia zawartości plików](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Możesz również dodać alert dotyczący zmian wprowadzonych w śledzonych plikach. Załóżmy na przykład, że chcesz ustawić alert dla zmian wprowadzonych w pliku Hosts. Zacznij od przechodzenia do Log Analytics, wybierając pozycję **log Analytics** na pasku poleceń lub otwierając wyszukiwanie w dzienniku dla połączonego obszaru roboczego log Analytics. Po zakończeniu Log Analytics Wyszukaj zmiany zawartości w pliku hosts przy użyciu następującej kwerendy:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Zrzut ekranu edytora zapytań Log Analytics w Azure Portal](./media/change-tracking2.png)

To zapytanie wyszukuje zmiany zawartości plików o ścieżce zawierającej wyraz "hosty". Możesz również wyszukać konkretny plik, zmieniając parametr path. (Na przykład `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`.)
  
Gdy zapytanie zwróci wyniki, wybierz pozycję **Nowa reguła alertu** , aby otworzyć Edytor reguł alertów. Możesz również przejść do tego edytora za pośrednictwem Azure Monitor w Azure Portal.

W Edytorze reguł alertów przejrzyj zapytanie i Zmień logikę alertów, jeśli zachodzi taka potrzeba. W tym przypadku chcemy, aby alert został zgłoszony w przypadku wykrycia jakichkolwiek zmian na dowolnym komputerze w środowisku.

![Zrzut ekranu edytora reguł alertów Log Analytics w Azure Portal](./media/change-tracking3.png)

Po ustawieniu logiki warunku można przypisać grupy akcji do wykonywania akcji w odpowiedzi na alert. W tym przykładzie, gdy zostanie zgłoszony alert, wysyłane są wiadomości e-mail i zostanie utworzony bilet narzędzia ITSM. Możesz wykonać wiele innych przydatnych akcji, takich jak wyzwalanie funkcji platformy Azure, Azure Automation elementu Runbook, elementów webhook lub aplikacji logiki.

![Zrzut ekranu przedstawiający przykładową podsumowanie reguły alertu w Azure Portal](./media/change-tracking4.png)

Po ustawieniu wszystkich parametrów i logiki Zastosuj alert do środowiska.

## <a name="more-tracking-and-alerting-examples"></a>Więcej przykładów śledzenia i alertów

Poniżej przedstawiono inne typowe scenariusze śledzenia i zgłaszania alertów, które warto wziąć pod uwagę:

### <a name="driver-file-changed"></a>Zmieniono plik sterownika

Wykrywaj, czy pliki sterowników zostały zmienione, dodane lub usunięte. Przydatne do śledzenia zmian w krytycznych plikach systemowych.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Określona usługa została zatrzymana

Przydatne do śledzenia zmian w usługach krytycznych dla systemu.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Zainstalowane nowe oprogramowanie

Przydatne w środowiskach, w których należy zablokować konfiguracje oprogramowania.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Określona wersja oprogramowania jest lub nie jest zainstalowana na komputerze

Przydatne do oceny zabezpieczeń. Zwróć uwagę, że to zapytanie odwołuje się `ConfigurationData`, które zawiera dzienniki spisu i raporty ostatniego raportowanego stanu konfiguracji, a nie zmian.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-registry"></a>Znana Biblioteka DLL została zmieniona przez rejestr

Przydatne do wykrywania zmian w dobrze znanych kluczach rejestru.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak zarządzać aktualizacjami serwerów, [tworząc harmonogramy aktualizacji](./update-schedules.md) za pomocą Azure Automation.

> [!div class="nextstepaction"]
> [Tworzenie harmonogramów aktualizacji](./update-schedules.md)
