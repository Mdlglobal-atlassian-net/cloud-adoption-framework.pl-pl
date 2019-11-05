---
title: Przewodnik monitorowania chmury — gromadzenie odpowiednich danych
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Określ, kiedy używać Azure Monitor lub System Center Operations Manager w Microsoft Azure
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 05596379872fbfa9099297a55d4b75dedc0b672a
ms.sourcegitcommit: bf9be7f2fe4851d83cdf3e083c7c25bd7e144c20
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/04/2019
ms.locfileid: "73564945"
---
# <a name="cloud-monitoring-guide-collect-the-right-data"></a>Przewodnik po monitorowaniu chmur: Zbierz odpowiednie dane

W tym artykule opisano niektóre zagadnienia dotyczące zbierania danych monitorowania w aplikacji w chmurze.

Aby obserwować kondycję i dostępność rozwiązania w chmurze, należy skonfigurować narzędzia do monitorowania w celu zebrania poziomu sygnałów opartych na przewidywalnych Stanach niepowodzeń. Sygnały te są objawy błędu, a nie przyczyny. Narzędzia do monitorowania wykorzystują metryki i, w przypadku zaawansowanej diagnostyki i analizy głównych przyczyn, dzienników.

Uważnie planowanie monitorowania i migracji. Zacznij od uwzględnienia właściciela usługi monitorowania, kierownika operacji i innego powiązanego personelu w fazie planowania i Kontynuuj angażowanie się w cały cykl tworzenia i wydawania. Ich fokus będzie opracowywać konfigurację monitorowania opartą na następujących kryteriach:

- Co to jest kompozycja usługi i czy te zależności są monitorowane dzisiaj? Jeśli tak, czy istnieją wiele narzędzi? Czy istnieje możliwość konsolidacji, bez wprowadzania zagrożeń?
- Co to jest umowa SLA usługi i jak można ją wycenić i zgłosić?
- Jak powinien wyglądać pulpit nawigacyjny usługi w przypadku zgłoszenia zdarzenia? Jak powinien wyglądać pulpit nawigacyjny dla właściciela usługi i dla zespołu, który obsługuje usługę?
- Jakie metryki ma zasób do monitorowania?  
- Jak właściciel usługi, zespoły pomocy technicznej i inni pracownicy będą przeszukiwać dzienniki?

Odpowiedzi na te pytania i kryteria dotyczące alertów określają sposób korzystania z platformy monitorowania. Jeśli przeprowadzasz migrację z istniejącej platformy monitorowania lub zestawu narzędzi do monitorowania, użyj migracji jako możliwości, aby przeprowadzić ponowną ocenę zbieranych sygnałów. Jest to szczególnie prawdziwe, gdy istnieje kilka kosztów, które należy wziąć pod uwagę podczas migracji lub integracji z platformą monitorowania opartą na chmurze, taką jak Azure Monitor. Należy pamiętać, że dane monitorowania muszą być funkcjonalne. Musisz mieć zoptymalizowane zebrane dane, aby dać Ci "a 10 000" widok ogólnej kondycji usługi. Instrumentacja zdefiniowana do identyfikowania rzeczywistych zdarzeń powinna być prosta, przewidywalna i niezawodna, jak to możliwe.

## <a name="develop-a-monitoring-configuration"></a>Opracowywanie konfiguracji monitorowania

Właściciel i zespół usługi monitorowania zwykle postępuje zgodnie ze wspólnym zestawem działań w celu opracowania konfiguracji monitorowania. Te działania rozpoczynają się od początkowych etapów planowania, kontynuując testowanie i sprawdzanie poprawności w środowisku nieprodukcyjnym, a następnie przechodzą do wdrożenia produkcyjnego. Konfiguracje monitorowania są uzyskiwane z znanych trybów niepowodzeń, wyników testów symulowanych błędów i doświadczenia kilku osób w organizacji (inżynier usług, działania, inżynierowie i deweloperzy). Takie konfiguracje zakładają, że usługa już istnieje, jest migrowana do chmury i nie została przetworzona.

Aby uzyskać wyniki dotyczące jakości na poziomie usług, należy wcześniej monitorować kondycję i dostępność tych usług w procesie tworzenia oprogramowania. Jeśli projekt tej usługi lub aplikacji jest monitorowany jako zostawiać, wyniki nie będą się kończyły pomyślnie.

Aby zwiększyć szybsze rozwiązywanie incydentu, weź pod uwagę następujące zalecenia:

- Zdefiniuj pulpit nawigacyjny dla każdego składnika usługi.
- Skorzystaj z metryk, aby pomóc w dalszej zdiagnozowaniu i zidentyfikowaniu rozwiązania lub obejście problemu, jeśli nie można odzyskać głównej przyczyny.
- Korzystaj z możliwości przechodzenia do szczegółów pulpitu nawigacyjnego lub wspieraj Dostosowywanie widoku, aby udoskonalić go.
- Jeśli potrzebujesz pełnych dzienników, metryki powinny mieć pomoc w odkierowaniu do kryteriów wyszukiwania. Jeśli metryki nie pomogły, popraw je dla następnego zdarzenia.

Ten identyfikator GUID zestawu zasad może pomóc w przekroczeniu szczegółowych informacji, a także lepszym zarządzaniu usługą.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Strategia zgłaszania alertów](./alerting.md)
