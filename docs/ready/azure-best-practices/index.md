---
title: Najlepsze rozwiązania dotyczące gotowości na platformę Azure
description: Poznaj najlepsze rozwiązania i dodatkowe wskazówki, które pomogą zespołowi w ustanowieniu i przygotowaniu środowiska platformy Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 107764931a6188f6976c5cfb8af0f74082c21e2b
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997783"
---
# <a name="best-practices-for-azure-readiness"></a>Najlepsze rozwiązania dotyczące gotowości na platformę Azure

Gotowość na chmurę wymaga wyposażenia personelu w umiejętności techniczne niezbędne do rozpoczęcia pracy nad wdrożeniem chmury oraz przygotowania docelowego środowiska migracji na zasoby i obciążenia, które zostaną przeniesione do chmury. Przeczytaj te najlepsze rozwiązania i dodatkowe wskazówki, aby pomóc zespołowi w przygotowaniu środowiska platformy Azure.

## <a name="azure-fundamentals"></a>Podstawy platformy Azure

Zorganizuj i wdróż zasoby w środowisku platformy Azure.

- [Podstawowe pojęcia dotyczące platformy Azure](../considerations/fundamental-concepts.md). Poznaj kluczowe pojęcia i terminy związane z platformą Azure oraz sposób, w jaki te pojęcia się ze sobą wiążą.
- [Utwórz początkowe subskrypcje](./initial-subscriptions.md). Ustanów początkowy zestaw subskrypcji platformy Azure, aby rozpocząć wdrażanie chmury.
- [Skaluj środowisko platformy Azure przy użyciu wielu subskrypcji](../azure-best-practices/scale-subscriptions.md). Poznaj przyczyny i strategie tworzenia dodatkowych subskrypcji w celu skalowania środowiska platformy Azure.
- [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](../azure-best-practices/organize-subscriptions.md). Dowiedz się, jak za pomocą grup zarządzania platformy Azure można zarządzać zasobami, rolami, zasadami i wdrożeniem w wielu subskrypcjach.
- [Stosuj zalecane konwencje nazewnictwa i tagowania](../azure-best-practices/naming-and-tagging.md). Zapoznaj się z szczegółowymi zaleceniami dotyczącymi nazewnictwa i tagowania zasobów. Te zalecenia ułatwiają wdrażanie chmury w przedsiębiorstwie.
- [Uzyskiwanie spójności w chmurze hybrydowej](../considerations/hybrid-consistency.md). Utwórz rozwiązania chmury hybrydowej, które zapewniają korzyści związane z innowacjami w chmurze przy zachowaniu wielu udogodnień zarządzania w środowisku lokalnym.

## <a name="networking"></a>Sieć

Przygotuj infrastrukturę sieci w chmurze do obsługi obciążeń.

- [Decyzje dotyczące sieci](../considerations/networking-options.md). Wybierz usługi, narzędzia i architektury sieciowe, które spełnią wymagania Twojej organizacji w zakresie obciążeń, zapewnienia ładu i łączności.
- [Planowanie sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Zaplanuj sieci wirtualne na podstawie wymagań dotyczących izolacji, łączności i lokalizacji.
- [Najlepsze rozwiązania z zakresu zabezpieczeń sieci](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Poznaj najlepsze rozwiązania dotyczące rozwiązywania typowych problemów z zabezpieczeniami sieci za pomocą wbudowanych funkcji platformy Azure.
- [Sieci obwodowe](./perimeter-networks.md). Umożliw bezpieczną łączność między sieciami w chmurze i sieciami w środowisku lokalnym lub w fizycznym centrum danych, wraz z wychodzącymi i przychodzącymi połączeniami internetowymi.
- [Topologia sieci piasty i szprych](./hub-spoke-network-topology.md). Wydajnie zarządzaj typowymi wymaganiami dotyczącymi komunikacji lub zabezpieczeń w przypadku skomplikowanych obciążeń i reaguj na potencjalne ograniczenia subskrypcji platformy Azure.

## <a name="identity-and-access-control"></a>Tożsamość i kontrola dostępu

Zaprojektuj infrastrukturę tożsamości i kontroli dostępu, aby zwiększyć bezpieczeństwo obciążeń i wydajność zarządzania nimi.

- [Najlepsze rozwiązania dotyczące zabezpieczeń kontroli dostępu i zarządzania tożsamościami na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Poznaj najlepsze rozwiązania dotyczące zarządzania tożsamościami i kontroli dostępu przy użyciu wbudowanych funkcji platformy Azure.
- [Najlepsze rozwiązania dotyczące kontroli dostępu na podstawie ról](../considerations/roles.md). Umożliw szczegółowe, oparte na grupach zarządzanie dostępem dla zasobów zorganizowanych wokół ról użytkownika.
- [Zabezpieczanie uprzywilejowanego dostępu dla wdrożeń hybrydowych i wdrożeń w chmurze w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Upewnij się, że konta uprzywilejowane i konta z dostępem administracyjnym w Twojej organizacji są zabezpieczone w środowisku chmurowym i lokalnym.

## <a name="storage"></a>Storage

- [Wskazówki dotyczące usługi Azure Storage](../considerations/storage-options.md). Wybierz odpowiednie rozwiązanie magazynu na platformie Azure do obsługi swoich scenariuszy użycia.
- [Przewodnik po zabezpieczeniach usługi Azure Storage](https://docs.microsoft.com/azure/storage/blobs/security-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się więcej na temat funkcji zabezpieczeń w usłudze Azure Storage.

## <a name="databases"></a>Bazy danych

- [Wybieranie odpowiedniej opcji programu SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Wybierz rozwiązanie PaaS lub IaaS, które najlepiej obsłuży Twoje obciążenia programu SQL Server.
- [Najlepsze rozwiązania dotyczące zabezpieczeń bazy danych](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Poznaj najlepsze rozwiązania dotyczące zabezpieczeń bazy danych na platformie Azure.
- [Wybór odpowiedniego magazynu danych](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Wybierz odpowiedni magazyn danych, który spełnia Twoje wymagania. Dostępne są setki opcji implementacji w przypadku baz danych SQL i NoSQL. Magazyny danych często są pogrupowane według sposobu strukturyzowania danych oraz typów operacji, które obsługują. W tym artykule opisano kilka typowych modeli magazynu.

## <a name="cost-management"></a>Zarządzanie kosztami

- [Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach](./track-costs.md). Poznaj najlepsze rozwiązania dotyczące tworzenia odpowiednich mechanizmów śledzenia kosztów.
- [Jak zoptymalizować inwestycję w chmurę za pomocą usługi Azure Cost Management](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Zaimplementuj strategię zarządzania kosztami i poznaj dostępne narzędzia do obsługi zadań związanych z kosztami.
- [Tworzenie budżetów i zarządzanie nimi](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się, jak tworzyć budżety i zarządzać nimi przy użyciu usługi Azure Cost Management.
- [Eksportowanie danych kosztów](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się, jak eksportować dane kosztów przy użyciu usługi Azure Cost Management.
- [Optymalizowanie kosztów na podstawie rekomendacji](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się, jak identyfikować nie w pełni wykorzystywane zasoby, i zmniejsz koszty przy użyciu usług Azure Cost Management i Azure Advisor.
- [Monitorowanie użycia i wydatków za pomocą alertów o kosztach](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/_bread/toc.json). Dowiedz się, jak używać alertów usługi Cost Management, aby monitorować użycie i wydatki na platformie Azure.
