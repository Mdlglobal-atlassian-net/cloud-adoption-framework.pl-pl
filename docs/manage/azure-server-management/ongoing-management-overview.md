---
title: Ciągłe zarządzanie i bezpieczeństwo
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak należy skoncentrować się na konfiguracjach operacji i zabezpieczeń, które będą obsługiwały bieżące operacje.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: d006773b66bf9e41301c4d2e9b34018394594e28
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80430534"
---
# <a name="phase-3-ongoing-management-and-security"></a>Faza 3: bieżące zarządzanie i zabezpieczenia

Po dodaniu usług zarządzania serwera Azure należy skoncentrować się na konfiguracjach operacji i zabezpieczeń, które będą obsługiwać bieżące operacje. Zaczniemy zabezpieczać środowisko, przeglądając Azure Security Center. Następnie skonfigurujemy zasady w celu zapewnienia zgodności serwerów i automatyzowania typowych zadań. W tej sekcji omówiono następujące tematy:

- **[Zaleceń dotyczących zabezpieczeń.](#address-security-recommendations)** Azure Security Center oferuje sugestie zwiększające bezpieczeństwo środowiska. Po zaimplementowaniu tych zaleceń zobaczysz wpływ odzwierciedlony w ocenę zabezpieczeń.
- **[Włącz zasady konfiguracji gościa.](./guest-configuration-policy.md)** Użyj funkcji konfiguracji gościa Azure Policy, aby przeprowadzić inspekcję ustawień w maszynie wirtualnej. Można na przykład sprawdzić, czy wszystkie certyfikaty wkrótce wygasną.
- **[Śledź i Ostrzegaj o zmianach krytycznych.](./enable-tracking-alerting.md)** W przypadku rozwiązywania problemów z pierwszym pytaniem, które należy wziąć pod uwagę, jest "Co zmieniono?". W tym artykule dowiesz się, jak śledzić zmiany i tworzyć alerty, aby aktywnie monitorować składniki krytyczne.
- **[Utwórz harmonogramy aktualizacji.](./update-schedules.md)** Zaplanuj instalację aktualizacji, aby upewnić się, że wszystkie serwery mają najnowsze.
- **[Typowe przykłady Azure Policy.](./common-policies.md)** W tym artykule przedstawiono przykłady typowych zasad zarządzania.

## <a name="address-security-recommendations"></a>Zalecenia dotyczące zabezpieczeń adresów

Azure Security Center to centralne miejsce, w którym można zarządzać zabezpieczeniami środowiska. Zobaczysz ogólną ocenę i zamierzone zalecenia.

Zalecamy przejrzenie i zaimplementowanie zaleceń dostarczonych przez tę usługę. Aby uzyskać informacje na temat dodatkowych korzyści z Azure Security Center, zobacz [postęp Azure Security Center zalecenia](https://docs.microsoft.com/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Następne kroki

Dowiedz się [, jak włączyć funkcję konfiguracji gościa Azure Policy](./guest-configuration-policy.md) .

> [!div class="nextstepaction"]
> [Zasady konfiguracji gościa](./guest-configuration-policy.md)
