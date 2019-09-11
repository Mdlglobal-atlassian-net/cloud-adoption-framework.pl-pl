---
title: Najlepsze rozwiązania dotyczące gotowości na platformę Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do najlepszych rozwiązań dotyczących gotowości na platformę Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f1d4423e230d2eeff524a864f163e0cb13dc065b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818271"
---
# <a name="best-practices-for-azure-readiness"></a>Najlepsze rozwiązania dotyczące gotowości na platformę Azure

Dużą część gotowości na chmurę stanowi wyposażenie personelu w umiejętności techniczne niezbędne do rozpoczęcia pracy nad wdrożeniem chmury oraz przygotowanie docelowego środowiska migracji na zasoby i obciążenia, które zostaną przeniesione do chmury. Poniższe tematy zawierają najlepsze rozwiązania i dodatkowe wskazówki, które pomogą zespołowi w ustanowieniu i przygotowaniu środowiska platformy Azure.

## <a name="azure-fundamentals"></a>Podstawy platformy Azure

Skorzystaj z poniższych wskazówek podczas organizowania i wdrażania zasobów w środowisku platformy Azure:

- [Podstawowe pojęcia dotyczące platformy Azure](../considerations/fundamental-concepts.md). Poznaj podstawowe pojęcia i terminy używane w odniesieniu do platformy Azure. Dowiedz się także, jak te pojęcia odnoszą się do siebie nawzajem.
- [Zalecane konwencje nazewnictwa i tagowania](../considerations/name-and-tag.md). Zapoznaj się z szczegółowymi zaleceniami dotyczącymi nazewnictwa i tagowania zasobów. Te zalecenia ułatwiają wdrażanie chmury w przedsiębiorstwie.
- [Skalowanie za pomocą wielu subskrypcji platformy Azure](../considerations/scaling-subscriptions.md). Poznaj strategie skalowania za pomocą wielu subskrypcji platformy Azure.
- [Organizowanie zasobów przy użyciu grup zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups/?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak za pomocą grup zarządzania platformy Azure można zarządzać zasobami, rolami, zasadami i wdrożeniem w wielu subskrypcjach.
- [Uzyskiwanie spójności w chmurze hybrydowej](../../infrastructure/misc/hybrid-consistency.md). Utwórz rozwiązania chmury hybrydowej, które zapewniają korzyści związane z innowacjami w chmurze przy zachowaniu wielu udogodnień zarządzania w środowisku lokalnym.

## <a name="networking"></a>Networking

Skorzystaj z poniższych wskazówek, aby przygotować infrastrukturę sieci w chmurze do obsługi obciążeń:

- [Decyzje dotyczące sieci](../considerations/network-decisions.md). Wybierz usługi, narzędzia i architektury sieciowe, które spełnią wymagania Twojej organizacji w zakresie obciążeń, zapewnienia ładu i łączności.
- [Planowanie sieci wirtualnej](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak zaplanować sieci wirtualne na podstawie wymagań dotyczących izolacji, łączności i lokalizacji.
- [Najlepsze rozwiązania z zakresu zabezpieczeń sieci](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Poznaj najlepsze rozwiązania dotyczące rozwiązywania typowych problemów z zabezpieczeniami sieci za pomocą wbudowanych możliwości platformy Azure.
- [Sieci obwodowe](./perimeter-networks.md). Sieci obwodowe, znane również jako strefy zdemilitaryzowane (DMZ), umożliwiają bezpieczną łączność między sieciami w chmurze i sieciami w środowisku lokalnym lub w fizycznym centrum danych, wraz z wychodzącymi i przychodzącymi połączeniami internetowymi.
- [Topologia sieci typu gwiazda](./hub-spoke-network-topology.md). Gwiazda to model sieci umożliwiający efektywne zarządzanie typowymi wymaganiami dotyczącymi komunikacji i zabezpieczeń w przypadku złożonych obciążeń. Jednocześnie obsługuje potencjalne ograniczenia platformy Azure.

## <a name="identity-and-access-control"></a>Tożsamość i kontrola dostępu

Skorzystaj z poniższych wskazówek podczas projektowania infrastruktury tożsamości i kontroli dostępu, aby zwiększyć bezpieczeństwo obciążeń i wydajność zarządzania nimi.

- [Najlepsze rozwiązania dotyczące zabezpieczeń kontroli dostępu i zarządzania tożsamościami na platformie Azure](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Poznaj najlepsze rozwiązania dotyczące zarządzania tożsamościami i kontroli dostępu przy użyciu wbudowanych funkcji platformy Azure.
- [Najlepsze rozwiązania dotyczące kontroli dostępu na podstawie ról](./roles.md). Kontrola dostępu oparta na rolach na platformie Azure (RBAC) oferuje szczegółowe, oparte na grupach zarządzanie dostępem dla zasobów zorganizowanych wokół ról użytkownika.
- [Zabezpieczanie uprzywilejowanego dostępu dla wdrożeń hybrydowych i wdrożeń w chmurze w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Skorzystaj z usługi Azure Active Directory, aby mieć pewność, że dostęp i konta administratorów w Twojej organizacji są zabezpieczone w środowisku chmurowym i lokalnym.

## <a name="storage"></a>Magazyn

- [Wskazówki dotyczące usługi Azure Storage](../considerations/storage-guidance.md). Wybierz odpowiednie rozwiązanie magazynu na platformie Azure do obsługi swoich scenariuszy użycia.
- [Przewodnik po zabezpieczeniach usługi Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-security-guide?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się więcej na temat funkcji zabezpieczeń w usłudze Azure Storage.

## <a name="databases"></a>Bazy danych

- [Wybieranie odpowiedniej opcji programu SQL Server na platformie Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Wybierz rozwiązanie PaaS lub IaaS, które najlepiej obsłuży Twoje obciążenia programu SQL Server.
- [Najlepsze rozwiązania dotyczące zabezpieczeń bazy danych](https://docs.microsoft.com/azure/security/azure-database-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Poznaj najlepsze rozwiązania dotyczące zabezpieczeń bazy danych na platformie Azure.
- [Wybór odpowiedniego magazynu danych](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview). Wybór odpowiedniego magazynu danych przystosowanego do wymagań jest kluczową decyzją projektową. Istnieją dosłownie setki implementacji do wyboru spośród baz danych SQL i NoSQL. Magazyny danych często są pogrupowane według sposobu strukturyzowania danych oraz typów operacji, które obsługują. W tym artykule opisano kilka typowych modeli magazynowania danych.

## <a name="cost-management"></a>Zarządzanie kosztami

- [Śledzenie kosztów w różnych jednostkach biznesowych, środowiskach i projektach](./track-costs.md). Poznaj najlepsze rozwiązania dotyczące tworzenia odpowiednich mechanizmów śledzenia kosztów.
- [Jak zoptymalizować inwestycję w chmurę za pomocą usługi Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Zaimplementuj strategię zarządzania kosztami i poznaj dostępne narzędzia do obsługi zadań związanych z kosztami.
- [Tworzenie budżetów i zarządzanie nimi](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak tworzyć budżety i zarządzać nimi przy użyciu usługi Azure Cost Management.
- [Eksportowanie danych kosztów](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak tworzyć eksportowane dane i zarządzać nimi w usłudze Azure Cost Management.
- [Optymalizowanie kosztów na podstawie rekomendacji](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak identyfikować nie w pełni wykorzystywane zasoby, i podejmij działania w celu zmniejszenia kosztów przy użyciu usług Azure Cost Management i Azure Advisor.
- [Monitorowanie użycia i wydatków za pomocą alertów o kosztach](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Dowiedz się, jak używać alertów usługi Cost Management, aby monitorować użycie i wydatki na platformie Azure.
