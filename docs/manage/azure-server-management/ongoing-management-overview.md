---
title: Ciągłe zarządzanie i bezpieczeństwo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ciągłe zarządzanie i bezpieczeństwo
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7b77181dd8ef6efe655b56489e5d4e6b210382b6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71030402"
---
# <a name="phase-3-ongoing-management-and-security"></a>Etap 3: Ciągłe zarządzanie i bezpieczeństwo

Po dodaniu usług zarządzania platformy Azure należy skoncentrować się na konfiguracjach operacji i zabezpieczeń, które będą obsługiwać bieżące operacje. Zaczniemy zabezpieczać środowisko, przeglądając Azure Security Center. Następnie skonfigurujemy zasady w celu zapewnienia zgodności serwerów i automatyzowania typowych zadań. W tej sekcji omówiono następujące tematy:

- **[Zaleceń dotyczących zabezpieczeń.](#address-security-recommendations)** Azure Security Center oferuje sugestie zwiększające bezpieczeństwo środowiska. Po zaimplementowaniu tych zaleceń można zobaczyć wpływ odzwierciedlony w wyniku zabezpieczeń.
- **[Włącz zasady konfiguracji gościa.](./guest-configuration-policy.md)** Włącz funkcję konfiguracji gościa Azure Policy, aby przeprowadzić inspekcję ustawień w maszynie wirtualnej. Można na przykład sprawdzić, czy wszystkie certyfikaty wkrótce wygasną.
- **[Śledź i Ostrzegaj o zmianach krytycznych.](./enable-tracking-alerting.md)** Podczas rozwiązywania problemów, pierwsze pytanie, które należy wziąć pod uwagę, to "co zostało zmienione?" W tym artykule dowiesz się, jak śledzić zmiany i tworzyć alerty, aby aktywnie monitorować składniki krytyczne.
- **[Utwórz harmonogramy aktualizacji.](./update-schedules.md)** Zaplanuj instalację aktualizacji, aby upewnić się, że wszystkie serwery mają najnowsze.
- **[Typowe przykłady Azure Policy.](./common-policies.md)** Zawiera przykłady typowych zasad zarządzania.

## <a name="address-security-recommendations"></a>Zalecenia dotyczące zabezpieczeń adresów

Azure Security Center to centralne miejsce, w którym można zarządzać zabezpieczeniami środowiska. Zobaczysz ogólną ocenę i zamierzone zalecenia.

Zalecamy przejrzenie i zaimplementowanie zaleceń dostarczonych przez tę usługę. Aby uzyskać informacje na temat dodatkowych korzyści z Azure Security Center, zobacz [postęp Azure Security Center zalecenia](https://docs.microsoft.com/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Następne kroki

Dowiedz się [, jak włączyć funkcję konfiguracji gościa Azure Policy](./guest-configuration-policy.md) .

> [!div class="nextstepaction"]
> [Zasady konfiguracji gościa](./guest-configuration-policy.md)
