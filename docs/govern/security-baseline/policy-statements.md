---
title: Instrukcje dotyczące przykładowych zasad linii bazowej zabezpieczeń
description: Zapoznaj się z tymi przykładowymi instrukcjami zasad odniesienia zabezpieczeń, aby pomóc w sporządzaniu zasad w celu rozwiązania potrzeb organizacji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e3f2a6156d282e2db6fb8a7206251447f9e48f71
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219805"
---
# <a name="security-baseline-sample-policy-statements"></a>Instrukcje dotyczące przykładowych zasad linii bazowej zabezpieczeń

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te instrukcje powinny dostarczyć zwięzłe podsumowanie zagrożeń i plany postępowania z nimi. Każda definicja instrukcji powinna zawierać następujące informacje:

- **Ryzyko techniczne:** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad:** Jasne wyjaśnienie wymagań zasad.
- **Opcje techniczne:** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki, które mogą być używane przez zespoły IT i deweloperów podczas implementowania zasad.

Poniższe przykładowe instrukcje dotyczące zasad dotyczą typowych zagrożeń firmy związanych z zabezpieczeniami. Te instrukcje są przykładami, które można przywołać podczas sporządzania projektów instrukcji zasad w celu rozwiązania potrzeb organizacji. Te przykłady nie są przeznaczone do obsługi skryptów i mogą być dostępne różne opcje dotyczące ponoszenia określonych zagrożeń. Pracuj ściśle z biznesem, bezpieczeństwem i zespołami IT, aby identyfikować najlepsze zasady dla unikatowego zestawu zagrożeń.

## <a name="asset-classification"></a>Klasyfikacja zasobów

**Ryzyko techniczne:** Zasoby, które nie są prawidłowo identyfikowane jako krytyczne dla działalności lub obejmujące dane poufne, mogą nie otrzymać wystarczającej ochrony, prowadząc do potencjalnych przecieków danych lub zakłóceń działania firmy.

**Instrukcja zasad:** Wszystkie wdrożone zasoby muszą być pogrupowane według stopnia ważności i klasyfikacji danych. Klasyfikacje muszą zostać sprawdzone przez zespół ds. zarządzania chmurą i właściciela aplikacji przed wdrożeniem w chmurze.

**Potencjalna opcja projektowania:** Ustanów [standardy tagowania zasobów](../../decision-guides/resource-tagging/index.md) i upewnij się, że personel IT stosuje je spójnie ze wszystkimi wdrożonymi zasobami przy użyciu [tagów zasobów platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).

## <a name="data-encryption"></a>Szyfrowanie danych

**Ryzyko techniczne:** Istnieje ryzyko, że chronione dane są ujawniane podczas magazynu.

**Instrukcja zasad:** Wszystkie chronione dane muszą być szyfrowane, gdy są przechowywane.

**Potencjalna opcja projektowania:** Zapoznaj się z artykułem [Omówienie usługi Azure Encryption](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview) , aby poznać sposób wykonywania danych przechowywanych na platformie Azure. Należy również uwzględnić dodatkowe kontrolki, takie jak szyfrowanie danych konta i kontrola nad sposobem, w jaki można zmienić ustawienia konta magazynu.

## <a name="network-isolation"></a>Izolacja sieciowa

**Ryzyko techniczne:** Połączenia między sieciami i podsieciami w ramach sieci wprowadzają potencjalne luki w zabezpieczeniach, które mogą powodować wycieki danych lub zakłócać usługi o krytycznym znaczeniu.

**Instrukcja zasad:** Podsieci sieciowe zawierające chronione dane muszą być odizolowane od innych podsieci. Ruch sieciowy między podsieciami chronionych danych ma być regularnie poddawany inspekcji.

**Potencjalna opcja projektowania:** Na platformie Azure izolacja sieci i podsieci jest zarządzana za pomocą [usługi azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

## <a name="secure-external-access"></a>Bezpieczny dostęp zewnętrzny

**Ryzyko techniczne:** Umożliwienie dostępu do obciążeń z publicznej sieci Internet wprowadza ryzyko włamania wynikające z nieautoryzowanego narażenia na dane lub przerw w działaniu firmy.

**Instrukcja zasad:** Nie można bezpośrednio uzyskać dostępu do podsieci zawierającej chronione dane za pośrednictwem publicznej sieci Internet lub między centrami danych. Dostęp do tych podsieci musi być kierowany za pośrednictwem podsieci pośrednich. Cały dostęp do tych podsieci musi następować przez rozwiązanie zapory, które może wykonywać funkcje skanowania pakietów i blokowania.

**Potencjalna opcja projektowania:** Na platformie Azure Zabezpiecz publiczne punkty końcowe, wdrażając [strefę DMZ między publicznym Internetem a siecią opartą na chmurze](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json). Rozważ wdrożenie, konfigurację i automatyzację [zapory platformy Azure](https://docs.microsoft.com/azure/firewall/overview).

## <a name="ddos-protection"></a>Ochrona przed atakami DDOS

**Ryzyko techniczne:** Ataki rozproszonego typu "odmowa usługi" (DDoS) mogą spowodować przerwanie działania biznesowego.

**Instrukcja zasad:** Wdróż zautomatyzowane mechanizmy ograniczania DDoS do wszystkich dostępnych publicznie punktów końcowych sieci. Żadna publiczna witryna sieci Web utworzona przez IaaS nie powinna być udostępniona w Internecie bez DDoS.

**Potencjalna opcja projektowania:** Użyj [Azure DDoS Protection Standard](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) , aby zminimalizować zakłócenia spowodowane atakami DDoS.

## <a name="secure-on-premises-connectivity"></a>Bezpieczna łączność lokalna

**Ryzyko techniczne:** Nieszyfrowany ruch sieciowy między siecią w chmurze i lokalnie za pośrednictwem publicznej sieci Internet jest narażony na przechwycenie, co stanowi ryzyko ujawnienia danych.

**Instrukcja zasad:** Wszystkie połączenia między sieciami lokalnymi i w chmurze muszą odbywać się za pośrednictwem bezpiecznego szyfrowanego połączenia sieci VPN lub dedykowanego prywatnego łącza sieci WAN.

**Potencjalna opcja projektowania:** Na platformie Azure Użyj ExpressRoute lub sieci VPN platformy Azure do ustanowienia prywatnych połączeń między sieciami lokalnymi i w chmurze.

## <a name="network-monitoring-and-enforcement"></a>Monitorowanie i wymuszanie sieci

**Ryzyko techniczne:** Zmiany w konfiguracji sieci mogą prowadzić do nowych luk w zabezpieczeniach i zagrożeń związanych z narażeniem na dane.

**Instrukcja zasad:** Narzędzia ładu muszą kontrolować i wymuszać wymagania dotyczące konfiguracji sieci zdefiniowane przez zespół linii bazowej zabezpieczeń.

**Potencjalna opcja projektowania:** Na platformie Azure aktywność sieci można monitorować za pomocą [usługi azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview), a [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-network-recommendations) mogą pomóc w zidentyfikowaniu luk w zabezpieczeniach. Azure Policy pozwala ograniczyć zasoby sieciowe i zasady konfiguracji zasobów zgodnie z limitami zdefiniowanymi przez zespół ds. zabezpieczeń.

## <a name="security-review"></a>Przegląd zabezpieczeń

**Ryzyko techniczne:** W miarę upływu czasu nowe zagrożenia bezpieczeństwa i ataki typów ataków zwiększają ryzyko wystąpienia zasobów w chmurze lub zakłócają ich działanie.

**Instrukcja zasad:** Trendy i potencjalne luki w zabezpieczeniach, które mogą mieć wpływ na wdrożenia w chmurze, powinny być regularnie weryfikowane przez zespół ds. zabezpieczeń, aby zapewnić aktualizacje narzędzi linii bazowej zabezpieczeń używanych w chmurze.

**Potencjalna opcja projektowania:** Ustanów regularne spotkania przeglądów zabezpieczeń, które obejmują odpowiednich członków zespołu IT i nadzoru. Zapoznaj się z istniejącymi danymi i metrykami zabezpieczeń, aby ustalić luki w bieżącym narzędziu zasady i narzędzia bazowe zabezpieczeń oraz zaktualizować zasady w celu skorygowania wszelkich nowych zagrożeń. Użyj [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) i [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) , aby uzyskać wgląd w szczegółowe informacje na temat nowych zagrożeń związanych z wdrożeniami.

## <a name="next-steps"></a>Następne kroki

Przykłady wymienione w tym artykule mogą służyć jako punkt wyjścia do opracowania zasad, które dotyczą konkretnych zagrożeń związanych z zabezpieczeniami, które są dostosowane do planów wdrażania w chmurze.

Aby rozpocząć tworzenie własnych niestandardowych instrukcji zasad linii bazowej zabezpieczeń, Pobierz [szablon dyscypliny linii bazowej zabezpieczeń](./template.md).

Aby przyspieszyć wdrażanie tego dyscypliny, wybierz [Przewodnik dotyczący ładu](../guides/index.md) z możliwością działania, który najlepiej odpowiada Twojemu środowisku. Następnie zmodyfikuj projekt, aby uwzględnić określone decyzje dotyczące zasad firmowych.

Tworzenie na podstawie ryzyka i tolerancji, ustanowienie procesu zarządzania zasadami odniesienia zabezpieczeń i ich przekazywania.

> [!div class="nextstepaction"]
> [Ustanawianie procesów zgodności z zasadami](./compliance-processes.md)
