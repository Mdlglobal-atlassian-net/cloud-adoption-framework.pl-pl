---
title: Przewodniki podejmowania decyzji dotyczących architektury
description: Użyj tych podstawowych modeli i wzorców składników infrastruktury wdrożenia w chmurze do obsługi określonych scenariuszy wdrażania w chmurze.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9552ba8b168e79f247916ae86f8e7721282baddb
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140239"
---
# <a name="architectural-decision-guides"></a>Przewodniki podejmowania decyzji dotyczących architektury

Przewodniki podejmowania decyzji dotyczących architektury w przewodniku Cloud Adoption Framework opisują wzorce i modele pomocne podczas tworzenia wskazówek dotyczących projektowania ładu w chmurze. Każdy przewodnik po decyzjach koncentruje się na jednym podstawowym składniku infrastruktury wdrożeń w chmurze i zawiera listę wzorców lub modeli przeznaczonych do obsługi określonych scenariuszy wdrażania w chmurze.

Kiedy zaczniesz ustanawiać ład w chmurze dla swojej organizacji, praktyczne podróże po ładzie zapewnią Ci podstawowy harmonogram działania. Jednak te podróże przyjmują pewne założenia dotyczące wymagań i priorytetów, które mogą nie odzwierciedlać sytuacji w Twojej organizacji.

Te przewodniki po decyzjach uzupełniają przykładowe podróże po ładzie, dostarczając alternatywne wzorce i modele, które ułatwiają dostosowanie wyborów dotyczących projektu architektury dokonanych w przykładowym przewodniku po decyzjach do swoich własnych wymagań.

## <a name="decision-guidance-categories"></a>Kategorie przewodników po decyzjach

Każda z poniższych kategorii reprezentuje fundamentalną technologię wszystkich wdrożeń w chmurze. W przykładowych podróżach po ładzie decyzje dotyczące projektu związane z tymi technologiami podejmowane są w oparciu o potrzeby przykładowych firm — niektóre z tych decyzji mogą nie być zgodne z potrzebami Twojej organizacji. W poniższych sekcjach omówiono alternatywne opcje dla każdej z tych kategorii, co umożliwia wybranie wzorca lub modelu lepiej dopasowanego do własnych wymagań.

[Subskrypcje](./subscriptions/index.md): Zaplanuj strukturę kont i projekt subskrypcji swojego wdrożenia chmury tak, aby pasowały do modelu własności, rozliczeń i funkcji zarządzania Twojej organizacji.

[Tożsamość](./identity/index.md): Zintegruj usługi zarządzania tożsamościami oparte na chmurze ze swoimi istniejącymi zasobami tożsamości, aby obsługiwać autoryzację i kontrolę dostępu w ramach swojego środowiska IT.

[Wymuszanie zasad](./policy-enforcement/index.md): Zdefiniuj i wymuś takie reguły zasad organizacyjnych dla zasobów i obciążeń wdrożonych w chmurze, które są zgodne z Twoimi wymaganiami dotyczącymi ładu.

[Spójność zasobów](./resource-consistency/index.md): Upewnij się, że wdrożenia i organizacja Twoich zasobów opartych na chmurze są dostosowane w celu wymuszenia zarządzania zasobami i wymagań dotyczących zasad.

[Tagowanie zasobów](./resource-tagging/index.md): Zorganizuj swoje zasoby oparte na chmurze tak, aby obsługiwały modele rozliczeń, podejścia do księgowości w chmurze i funkcje zarządzania oraz aby zoptymalizować wykorzystanie zasobów i koszty. Tagowanie zasobów wymaga spójnego i dobrze zorganizowanego schematu nazewnictwa i metadanych.

[Sieci zdefiniowane programowo](./software-defined-network/index.md): Wdrażaj bezpieczne obciążenia w chmurze za pomocą szybkiego wdrażania i modyfikacji wirtualnych funkcji sieciowych. Sieci zdefiniowane programowo mogą obsługiwać zwinne przepływy pracy, izolować zasoby i integrować systemy oparte na chmurze z istniejącą infrastrukturą IT.

[Szyfrowanie](./encryption/index.md): Zabezpiecz poufne dane przy użyciu szyfrowania, aby dostosować je do wymagań dotyczących zasad zabezpieczeń i zgodności w Twojej organizacji.

[Rejestrowanie i raportowanie](./logging-and-reporting/index.md): Monitoruj dane dzienników generowane przez zasoby oparte na chmurze. Analizowanie danych zapewnia wgląd w związane z kondycją informacje dotyczące operacji, konserwacji i stanu zgodności Twoich obciążeń.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, w jaki sposób subskrypcje i konta tworzą podstawę wdrożenia w chmurze.

> [!div class="nextstepaction"]
> [Projekt subskrypcji](./subscriptions/index.md)
