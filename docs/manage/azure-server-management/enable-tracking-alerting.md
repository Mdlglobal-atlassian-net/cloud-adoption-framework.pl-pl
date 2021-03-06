---
title: Śledzenie i alerty dotyczące zmian krytycznych
description: Włącz śledzenie i alerty dotyczące krytycznych zmian w środowisku hybrydowym za pomocą usługi Azure Change Tracking i spisu.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 1fa20d37c5cc7813220ff5862743f3179f4aefcd
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83861518"
---
<!-- cSpell:ignore HKEY kusto -->

# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Włącz śledzenie i alerty dla zmian krytycznych

Usługa Azure Change Tracking i spis zapewniają alerty dotyczące stanu konfiguracji środowiska hybrydowego i zmian w tym środowisku. Może zgłosić krytyczne zmiany plików, usług, oprogramowania i rejestru, które mogą mieć wpływ na wdrożone serwery.

Domyślnie usługa spisu Azure Automation nie monitoruje plików ani ustawień rejestru. Rozwiązanie udostępnia listę kluczy rejestru, które zalecamy do monitorowania. Aby wyświetlić tę listę, przejdź do konta usługi Automation w Azure Portal, a następnie wybierz **Inventory**pozycję  >  **Edytuj ustawienia**spisu.

![Zrzut ekranu przedstawiający Widok spisu Azure Automation w Azure Portal](./media/change-tracking1.png)

Aby uzyskać więcej informacji na temat poszczególnych kluczy rejestru, zobacz [śledzenie zmian kluczy rejestru](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Wybierz dowolny klucz do obliczenia, a następnie włącz go. To ustawienie jest stosowane do wszystkich maszyn wirtualnych, które są włączone w bieżącym obszarze roboczym.

Możesz również użyć usługi do śledzenia krytycznych zmian plików. Na przykład możesz chcieć śledzić plik C:\windows\System32\drivers\etc\HOSTS, ponieważ system operacyjny używa go do mapowania nazw hostów na adresy IP. Zmiany w tym pliku mogą spowodować problemy z łącznością lub przekierować ruch do niebezpiecznych witryn sieci Web.

Aby włączyć śledzenie zawartości plików dla hostów, wykonaj kroki opisane w temacie [Włączanie śledzenia zawartości plików](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

Możesz również dodać alert dotyczący zmian w plikach, które są śledzone. Załóżmy na przykład, że chcesz ustawić alert dla zmian w pliku Hosts. Wybierz **log Analytics** na pasku poleceń lub przeszukaj dziennik dla połączonego obszaru roboczego log Analytics. W Log Analytics Użyj następującego zapytania, aby wyszukać zmiany w pliku hosts:

  ```kusto
  ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
  ```

![Zrzut ekranu edytora zapytań Log Analytics w Azure Portal](./media/change-tracking2.png)

To zapytanie wyszukuje zmiany zawartości plików o ścieżce zawierającej wyraz "hosty". Możesz również wyszukać konkretny plik, zmieniając parametr path. (Na przykład `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"` .)
  
Gdy zapytanie zwróci wyniki, wybierz pozycję **Nowa reguła alertu** , aby otworzyć Edytor reguł alertów. Możesz również przejść do tego edytora za pośrednictwem Azure Monitor w Azure Portal.

W edytorze reguły alertu przejrzyj zapytanie i Zmień logikę alertów, jeśli jest to konieczne. W tym przypadku chcemy, aby alert został zgłoszony w przypadku wykrycia jakichkolwiek zmian na dowolnym komputerze w środowisku.

![Zrzut ekranu edytora reguł alertów Log Analytics w Azure Portal](./media/change-tracking3.png)

Po ustawieniu logiki warunku można przypisać grupy akcji do wykonywania akcji w odpowiedzi na alert. W tym przykładzie, gdy zostanie zgłoszony alert, wysyłane są wiadomości e-mail i zostanie utworzony bilet narzędzia ITSM. Możesz wykonać wiele innych przydatnych akcji, takich jak wyzwalanie funkcji platformy Azure, Azure Automation elementu Runbook, elementów webhook lub aplikacji logiki.

![Zrzut ekranu przedstawiający przykładową podsumowanie reguły alertu w Azure Portal](./media/change-tracking4.png)

Po ustawieniu wszystkich parametrów i logiki Zastosuj alert do środowiska.

## <a name="tracking-and-alerting-examples"></a>Przykłady śledzenia i alertów

W tej sekcji przedstawiono inne typowe scenariusze śledzenia i alertów, które mogą być używane.

### <a name="driver-file-changed"></a>Zmieniono plik sterownika

Użyj następującego zapytania, aby wykryć, czy pliki sterowników zostały zmienione, dodane lub usunięte. Jest to przydatne do śledzenia zmian w krytycznych plikach systemowych.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Określona usługa została zatrzymana

Użyj następującego zapytania, aby śledzić zmiany w usługach krytycznych dla systemu.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Zainstalowane nowe oprogramowanie

W przypadku środowisk, które wymagają zablokowania konfiguracji oprogramowania, należy użyć następującego zapytania.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Określona wersja oprogramowania jest lub nie jest zainstalowana na komputerze

Użyj następującego zapytania, aby ocenić zabezpieczenia. Ta kwerenda zawiera odwołania do `ConfigurationData` dzienników spisu i zawiera informacje o ostatnio zgłoszonym stanie konfiguracji, a nie zmianach.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-the-registry"></a>Znana Biblioteka DLL została zmieniona w rejestrze

Użyj następującego zapytania, aby wykryć zmiany w dobrze znanych kluczach rejestru.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak Azure Automation mogą [tworzyć harmonogramy aktualizacji](./update-schedules.md) w celu zarządzania aktualizacjami serwerów.

> [!div class="nextstepaction"]
> [Tworzenie harmonogramów aktualizacji](./update-schedules.md)
