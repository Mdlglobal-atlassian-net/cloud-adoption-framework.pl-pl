---
title: Zagadnienia dotyczące strefy docelowej na platformie Azure
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, w jaki sposób strefa docelowa zapewnia podstawowy blok konstrukcyjny dowolnego środowiska wdrażania w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/09/2020
ms.topic: overview
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 98160a01647907609bfbc1b16d9a4ffe8e23e06c
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621526"
---
# <a name="landing-zone-considerations"></a>Zagadnienia dotyczące strefy docelowej

Strefa docelowa to podstawowy blok konstrukcyjny każdego środowiska wdrażania chmury. Termin _strefa docelowa_ odnosi się do środowiska, które zostało aprowizowane i przygotowane do hostowania obciążeń w środowisku chmury, takim jak platforma Azure. W pełni funkcjonalna strefa docelowa jest finalnym dostarczanym elementem dowolnej iteracji metodologii gotowości podręcznika Cloud Adoption Framework.

![Zagadnienia dotyczące strefy docelowej](../../_images/ready/landing-zone-considerations.png)

Na tej ilustracji przedstawiono główne kwestie do rozważenia podczas implementowania każdego wdrożenia strefy docelowej. Te kwestie można podzielić na trzy kategorie lub typy zagadnień: hosting, podstawy platformy Azure i ład.

## <a name="hosting-considerations"></a>Zagadnienia dotyczące hostingu

Wszystkie strefy docelowe zapewniają strukturę dla opcji hostingu. Struktura jest tworzona jawnie za pośrednictwem mechanizmów kontroli ładu lub organicznie przez wdrożenie usług w strefie docelowej. Następujące artykuły mogą pomóc w podjęciu decyzji, które zostaną odzwierciedlone w strategii lub innych skryptach automatyzacji tworzących strefę docelową:

- [Decyzje obliczeniowe](./compute-options.md): aby zminimalizować złożoność operacyjną, Wyrównaj Opcje obliczeniowe do celów strefy docelowej. Tę decyzję można wymusić przy użyciu łańcuchów narzędzi automatyzacji, takich jak inicjatywy usługi Azure Policy i strategie strefy docelowej.
- [Decyzje dotyczące magazynu](./storage-options.md): wybierz odpowiednie rozwiązanie usługi Azure Storage, aby obsłużyć wymagania dotyczące obciążenia.
- [Decyzje dotyczące sieci](./networking-options.md): wybierz pozycję usługi sieciowe, narzędzia i architektury, aby obsłużyć wymagania dotyczące obciążenia, zarządzania i łączności w organizacji.
- [Decyzje dotyczące bazy danych](./data-options.md): Ustal, która technologia bazy danych najlepiej nadaje się do wymagań związanych z obciążeniami.

## <a name="azure-fundamentals"></a>Podstawy platformy Azure

Każda strefa docelowa jest częścią szerszego rozwiązania do organizowania zasobów w środowisku chmury. Podstawy platformy Azure to podstawowe bloki konstrukcyjne dla organizacji.

- [Podstawowe pojęcia dotyczące platformy Azure](./fundamental-concepts.md): Poznaj podstawowe koncepcje i terminy, które są używane do organizowania zasobów na platformie Azure i jak koncepcje odnoszą się do siebie.
- [Przewodnik po decyzji o spójności zasobów](../../decision-guides/resource-consistency/index.md): w przypadku zrozumienia poszczególnych podstaw Przewodnik po decyzji organizacji zasobów może pomóc w podejmowaniu decyzji, które umożliwiają kształtowanie strefy docelowej.

## <a name="governance-considerations"></a>Zagadnienia związane z nadzorem

Metodologie ładu podręcznika Cloud Adoption Framework ustalają proces zapewniania ładu w całym środowisku. Istnieje jednak wiele przypadków użycia, które mogą wymagać podjęcia decyzji ładu w odniesieniu do strefy docelowej. W wielu scenariuszach, plany bazowe ładu są wymuszane w odniesieniu do strefy docelowej, nawet jeśli linie bazowe są rozwiązane całościowo. Jest to prawdziwe w przypadku pierwszych kilku stref docelowych wdrażanych przez organizację.

Następujące artykuły mogą pomóc w podjęciu decyzji dotyczących ładu dla strefy docelowej. Każdą decyzję można uwzględnić w planach bazowych ładu.

- **Wymagania związane z kosztami.** Na podstawie motywacji organizacji do wdrożenia chmury i zobowiązania operacyjne względem jej środowiska, może być konieczne wprowadzenie zmian w różnych konfiguracjach zarządzania kosztami dla strefy docelowej.
- **Monitorowanie decyzji.** W zależności od wymagań operacyjnych dla strefy docelowej można wdrożyć różne narzędzia do monitorowania. Artykuł na temat decyzji dotyczących monitorowania pomoże określić najbardziej odpowiednie narzędzia do wdrożenia.
- **Kontrola dostępu oparta na rolach.** [Kontrola dostępu na podstawie ról](../considerations/roles.md) na platformie Azure (RBAC) oferuje szczegółowe, oparte na grupach zarządzanie dostępem dla zasobów zorganizowanych wokół ról użytkownika.
- **Decyzje dotyczące zasad.** [Przykłady strategii platformy Azure](https://docs.microsoft.com/azure/governance/blueprints/samples) zawierają wstępnie utworzone strategie zgodności — każdą ze wstępnie zdefiniowanymi inicjatywami zasad. Decyzje dotyczące zasad ułatwiają wybór najlepszego planu lub inicjatywy zasad na podstawie Twoich wymagań i ograniczeń.
- **Utwórz [spójność chmury hybrydowej](./hybrid-consistency.md).** Utwórz rozwiązania chmury hybrydowej, które zapewniają organizacji korzyści z innowacji w chmurze przy zachowaniu wielu udogodnień zarządzania w środowisku lokalnym.
