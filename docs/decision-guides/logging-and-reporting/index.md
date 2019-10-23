---
title: Przewodnik po decyzjach dotyczących rejestrowania i raportowania
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej o rejestrowaniu, raportowaniu i monitorowaniu jako usługach podstawowych w ramach migracji na platformę Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 082b9ccdcc94548b46a5a220cfe83768f7c4cbf6
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547892"
---
# <a name="logging-and-reporting-decision-guide"></a>Przewodnik po decyzjach dotyczących rejestrowania i raportowania

Wszystkie organizacje potrzebują mechanizmów umożliwiających powiadamianie zespołów IT o problemach dotyczących wydajności, czasu pracy i zabezpieczeń zanim staną się one poważne. Skuteczna strategia monitorowania pozwala zrozumieć, jak działają poszczególne składniki, które tworzą obciążenia i infrastrukturę sieci. W kontekście migracji do chmury publicznej, integracja funkcji rejestrowania i raportowania z istniejącymi systemami monitorowania z możliwością informowania odpowiedniego personelu IT o zdarzeniach i metrykach, ma krytyczne znaczenie dla realizacji celów organizacji dotyczących czasu pracy, zabezpieczeń i zgodności z zasadami.

![Wykres opcji rejestrowania, raportowania i monitorowania od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-logging-and-reporting.png)

Idź do: [Planowanie infrastruktury monitorowania](#planning-your-monitoring-infrastructure) | [Natywne dla chmury](#cloud-native) | [Rozszerzenie lokalne](#on-premises-extension) | [Agregacja za pomocą bramy](#gateway-aggregation) | [Monitorowanie hybrydowe (lokalne)](#hybrid-monitoring-on-premises) | [Monitorowanie hybrydowe (w chmurze)](#hybrid-monitoring-cloud-based) | [Wielochmurowe](#multicloud) | [Więcej informacji](#learn-more)

Punkt przegięcia podczas określania strategii rejestrowania i raportowania w chmurze zależy głównie od istniejących inwestycji dokonanych w organizacji w procesy operacyjne, a w pewnym stopniu od wymagań dotyczących obsługi strategii wielochmurowej.

Istnieje kilka sposobów rejestrowania i raportowania działań w chmurze. Rejestrowanie natywne dla chmury i scentralizowane to dwie typowe opcje typu „oprogramowanie jako usługa” (SaaS) oparte na modelu subskrypcyjnym i liczbie subskrypcji.

## <a name="planning-your-monitoring-infrastructure"></a>Planowanie infrastruktury monitorowania

Podczas planowania wdrożenia należy rozważyć, gdzie będą przechowywane dane rejestrowania oraz w jaki sposób usługi raportowania i monitorowania w chmurze zostaną zintegrowane z istniejącymi procesami i narzędziami.

| Pytanie | Natywne dla chmury | Rozszerzenie lokalne | Monitorowanie hybrydowe | Agregacja za pomocą bramy |
|-----|-----|-----|-----|-----|
| Czy masz istniejącą lokalną infrastrukturę monitorowania? | Nie | Yes | Yes |  Nie |
| Czy masz wymagania, które uniemożliwiają przechowywanie danych dzienników w zewnętrznych lokalizacjach przechowywania? | Nie | Yes | Nie | Nie |
| Czy potrzebujesz zintegrować monitorowanie w chmurze z systemami lokalnymi? | Nie | Nie | Yes | Nie |
Czy potrzebujesz przetwarzać lub filtrować dane telemetryczne przed ich przesłaniem do systemów monitorowania? | Nie | Nie | Nie | Yes |

### <a name="cloud-native"></a>Natywne dla chmury

Jeśli w Twojej organizacji nie ma obecnie wdrożonych systemów rejestrowania i raportowania lub planowane wdrożenie nie musi być zintegrowane z istniejącymi lokalnymi lub zewnętrznymi systemami monitorowania, natywne rozwiązanie SaaS w chmurze, takie jak usługa [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview), jest najprostszym wyborem.

W tym scenariuszu wszystkie dane dzienników są rejestrowane i przechowywane w chmurze, a narzędzia do rejestrowania i raportowania umożliwiające przetwarzanie i wyświetlanie informacji przez pracowników działu IT są zapewnione na platformie Azure oraz w usłudze Azure Monitor.

Niestandardowe rozwiązania do rejestrowania oparte na usłudze Azure Monitor mogą być wdrażane ad hoc dla każdej subskrypcji lub obciążenia w mniejszych lub eksperymentalnych wdrożeniach i są zorganizowane w scentralizowany sposób, umożliwiając monitorowanie danych dzienników w całej infrastrukturze chmury.

**Założenia dotyczące rozwiązań natywnych dla chmury.** W przypadku użycia systemu rejestrowania i raportowania natywnego dla chmury przyjmowane są następujące założenia:

- Nie jest konieczna integracja danych dzienników z obciążeń w chmurze z istniejącymi systemami lokalnymi.
- Nie będziesz używać systemów raportowania w chmurze do monitorowania systemów lokalnych.

### <a name="on-premises-extension"></a>Rozszerzenie lokalne

Użycie rozwiązań w chmurze do rejestrowania i monitorowania, takich jak usługa Azure Monitor, może wymagać dużego nakładu pracy związanego z przebudową aplikacji i usług migrowanych do chmury. W takich przypadkach rozsądne może okazać się umożliwienie tym obciążeniom dalszego wysyłania danych telemetrycznych do istniejących systemów lokalnych.

W celu zapewnienia obsługi tego podejścia zasoby w chmurze będą musiały komunikować się bezpośrednio z systemami lokalnymi przy użyciu kombinacji [sieci hybrydowej](../software-defined-network/hybrid.md) i [usług domenowych hostowanych w chmurze](../identity/index.md#cloud-hosted-domain-services). Dzięki temu sieć wirtualna w chmurze działa jako rozszerzenie sieci środowiska lokalnego. W związku z tym obciążenia hostowane w chmurze mogą komunikować się bezpośrednio z lokalnym systemem rejestrowania i raportowania.

To podejście wykorzystuje istniejące inwestycje w narzędzia do monitorowania z niewielkimi modyfikacjami aplikacji lub usług wdrożonych w chmurze. Jest to często najszybsze podejście umożliwiające zapewnienie obsługi monitorowania podczas migracji metodą „lift and shift”. Jednak nie będzie ono rejestrować danych dzienników generowanych przez zasoby PaaS i SaaS w chmurze oraz będzie pomijać wszystkie dzienniki dotyczące maszyn wirtualnych generowane przez platformę chmury, takie jak zawierające informacje o stanie maszyn wirtualnych. Z tego względu ten wzorzec powinien stanowić tymczasowe rozwiązanie, dopóki nie zostanie wdrożone bardziej kompleksowe, hybrydowe rozwiązanie do monitorowania.

Założenia dotyczące wyłącznie rozwiązań lokalnych:

- Dane dzienników muszą być przechowywane wyłącznie w środowisku lokalnym w celu spełnienia wymagań technicznych lub z powodu wymagań prawnych bądź dotyczących zasad.
- Systemy lokalne nie obsługują hybrydowych rozwiązań do rejestrowania i raportowania lub agregacji za pomocą bramy.
- Aplikacje bazujące na chmurze mogą przesyłać dane telemetryczne bezpośrednio do lokalnych systemów rejestrowania lub agenci monitorowania, którzy mogą przesyłać dane do systemów lokalnych, mogą być wdrażani na maszynach wirtualnych obciążeń.
- Obciążenia nie są zależne od usług PaaS lub SaaS, które wymagają rozwiązań do rejestrowania i raportowania w chmurze.

### <a name="gateway-aggregation"></a>Agregacja za pomocą bramy

W przypadku scenariuszy, w których ilość danych telemetrycznych z chmury jest duża lub istniejące lokalne systemy monitorowania muszą rejestrować zmodyfikowane dane zanim mogą one być przetwarzane, może być wymagana usługa [agregacji za pomocą bramy](https://docs.microsoft.com/azure/architecture/patterns/gateway-aggregation).

Usługa bramy jest wdrażana u dostawcy usług w chmurze. Następnie odpowiednie aplikacje i usługi są konfigurowane w celu przesyłania danych telemetrycznych do bramy zamiast do domyślnego systemu rejestrowania. Brama może następnie przetwarzać dane: agregując, łącząc lub formatując je w inny sposób przed przesłaniem ich do usługi monitorowania w celu ich pozyskania i analizy.

Ponadto brama może służyć do agregowania i wstępnego przetwarzania danych telemetrycznych powiązanych z systemami natywnymi dla chmury lub hybrydowymi.

Założenia agregacji za pomocą bramy:

- Oczekujesz dużej ilości danych telemetrycznych z aplikacji lub usług w chmurze.
- Potrzebujesz formatować lub w inny sposób optymalizować dane telemetryczne przed ich przesłaniem do systemów monitorowania.
- Systemy monitorowania mają interfejsy API lub inne mechanizmy dostępne na potrzeby pozyskiwania danych dzienników po zakończeniu przetwarzania przez bramę.

### <a name="hybrid-monitoring-on-premises"></a>Monitorowanie hybrydowe (lokalne)

Hybrydowe rozwiązanie do monitorowania łączy dane dzienników z zasobów lokalnych i w chmurze w celu zapewnienia zintegrowanego widoku stanu operacyjnego infrastruktury IT.

Jeśli masz istniejące inwestycje w lokalne systemy monitorowania, których zastąpienie byłoby trudne lub kosztowne, może być konieczne zintegrowanie danych telemetrycznych z obciążeń w chmurze z lokalnymi rozwiązaniami do monitorowania. W hybrydowym, lokalnym systemie monitorowania lokalne dane telemetryczne nadal korzystają z istniejącego lokalnego systemu monitorowania. Dane telemetryczne z chmury są wysyłane bezpośrednio do lokalnego systemu monitorowania lub wysyłane do usługi Azure Monitor, a następnie kompilowane i pozyskiwane przez lokalny system w regularnych odstępach czasu.

**Założenia dotyczące lokalnego, hybrydowego rozwiązania do monitorowania** W przypadku użycia lokalnego systemu rejestrowania i raportowania do monitorowania hybrydowego przyjmowane są następujące założenia:

- Istniejące lokalne systemy raportowania muszą być używane do monitorowania obciążeń w chmurze.
- Wymagane jest zachowanie własności lokalnych danych dzienników.
- Lokalne systemy zarządzania udostępniają interfejsy API lub inne mechanizmy umożliwiające pozyskiwanie danych dzienników z systemów w chmurze.

> [!TIP]
> Ze względu na iteracyjny charakter migracji do chmury prawdopodobnie konieczne będzie przejście z różnych rozwiązań do monitorowania natywnych dla chmury i lokalnych na częściowo hybrydowe podejście, gdy integracja zasobów w chmurze z ogólną infrastrukturą IT osiągnie dojrzałość.

### <a name="hybrid-monitoring-cloud-based"></a>Monitorowanie hybrydowe (oparte na chmurze)

Jeśli nie ma konieczności zachowania lokalnego systemu monitorowania lub chcesz zastąpić lokalne systemy monitorowania scentralizowanym rozwiązaniem w chmurze, możesz również zintegrować lokalne dane dzienników z usługą Azure Monitor w celu zapewnienia scentralizowanego systemu monitorowania w chmurze.

Podobnie jak w przypadku podejścia opartego na rozwiązaniu lokalnym, w tym scenariuszu obciążenia w chmurze będą przesyłać dane telemetryczne bezpośrednio do usługi Azure Monitor, a aplikacje lokalne będą przesyłać dane telemetryczne bezpośrednio do usługi Azure Monitor lub agregować te dane lokalnie ma potrzeby pozyskiwania przez usługę Azure Monitor w regularnych odstępach czasu. Usługa Azure Monitor będzie następnie służyć jako główny system monitorowania i raportowania dla całej infrastruktury IT.

Założenia dotyczące monitorowania hybrydowego opartego na chmurze: W przypadku użycia systemów rejestrowania i raportowania opartych na chmurze dla monitorowania hybrydowego przyjmowane są następujące założenia:

- Użytkownik nie polega na istniejących lokalnych systemach monitorowania.
- Obciążenia nie mają wymagań prawnych lub dotyczących zasad związanych z przechowywaniem danych dzienników lokalnie.
- Systemy monitorowania w chmurze udostępniają interfejsy API lub inne mechanizmy umożliwiające pozyskiwanie danych dzienników z lokalnych aplikacji lub usług.

### <a name="multicloud"></a>Rozwiązanie wielochmurowe

Integracja funkcji rejestrowania i raportowania na wielu platformach w chmurze może być skomplikowana. Usług oferowanych przez poszczególne platformy często nie da się bezpośrednio porównać, a funkcje rejestrowania i telemetrii oferowane przez te usługi również się różnią.
Obsługa rejestrowania wielochmurowego często wymaga użycia usług bramy w celu przetwarzania danych dzienników do wspólnego formatu zanim zostaną one przesłane do hybrydowego rozwiązania do rejestrowania.

## <a name="learn-more"></a>Dowiedz się więcej

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) jest domyślną usługą raportowania i monitorowania dla platformy Azure. Oferuje ona następujące możliwości:

- Ujednolicona platforma do gromadzenia danych telemetrycznych aplikacji, danych telemetrycznych hostów (takich jak maszyny wirtualne), metryk kontenerów, metryk platformy Azure oraz dzienników zdarzeń.
- Narzędzia do tworzenia wizualizacji, zapytań, alertów i analiz. Zapewnia szczegółowe informacje o maszynach wirtualnych, systemów operacyjnych gościa, sieciach wirtualnych i zdarzeniach aplikacji obciążeń.
- [Interfejsy API REST](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough) do integracji z usługami zewnętrznymi oraz automatyzacji usług monitorowania i zgłaszania alertów.
- [Integracja](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-partners) z wieloma popularnymi innymi dostawcami.

## <a name="next-steps"></a>Następne kroki

Rejestrowanie i raportowanie to jeden z podstawowych składników infrastruktury wymagających podjęcia decyzji dotyczących architektury w trakcie procesu wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
