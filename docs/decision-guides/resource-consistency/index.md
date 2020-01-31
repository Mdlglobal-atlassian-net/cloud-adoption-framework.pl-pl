---
title: Przewodnik podejmowania decyzji dotyczących spójności zasobów
description: Dowiedz się więcej o spójności zasobów podczas planowania migracji na platformę Azure.
author: doodlemania2
ms.author: dermar
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 6f995a3f6ffb26f408a45610d7d0674e02bf6a31
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76806700"
---
# <a name="resource-consistency-decision-guide"></a>Przewodnik podejmowania decyzji dotyczących spójności zasobów

[Projekt subskrypcji](../subscriptions/index.md) platformy Azure określa sposób organizowania zasobów w chmurze w odniesieniu do struktury organizacji, praktyk księgowych i wymagań dotyczących obciążenia. Oprócz tego poziomu struktury spełnienie wymagań dotyczących zasad ładu organizacyjnego dla infrastruktury w chmurze wymaga umiejętności spójnego organizowania i wdrażania zasobów oraz zarządzania nimi w ramach subskrypcji.

![Wykres opcji spójności zasobów od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-resource-consistency.png)

Idź do: [Grupowanie podstawowe](#basic-grouping) | [Spójność wdrożenia](#deployment-consistency) | [Spójność zasad](#policy-consistency) | [Spójność hierarchiczna](#hierarchical-consistency) | [Spójność zautomatyzowana](#automated-consistency)

Decyzje dotyczące poziomu wymagań w odniesieniu do spójności zasobów infrastruktury w chmurze są uzależnione przede wszystkim od następujących czynników: rozmiaru infrastruktury cyfrowej po zakończeniu migracji, wymagań dotyczących firmy lub środowiska, które nie pasują ściśle do metod projektowania istniejącej subskrypcji, lub konieczności wymuszania ładu w miarę upływu czasu po wdrożeniu zasobów.

Wraz ze wzrostem znaczenia tych czynników coraz ważniejsze stają się korzyści wynikające z zapewnienia spójnego wdrażania, grupowania i zarządzania zasobami opartymi na chmurze. Aby osiągnąć bardziej zaawansowane poziomy spójności zasobów w celu spełnienia rosnących wymagań, trzeba włożyć więcej pracy w automatyzację, narzędzia i wymuszanie spójności, co z kolei skutkuje koniecznością poświęcenia dodatkowego czasu na zarządzanie zmianami i śledzenie.

## <a name="basic-grouping"></a>Grupowanie podstawowe

Na platformie Azure [grupy zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) stanowią podstawowy mechanizm organizacji zasobów umożliwiający logiczne grupowanie zasobów w ramach subskrypcji.

Grupy zasobów działają jak kontenery dla zasobów o typowym cyklu życia i ograniczeniach zarządzania współdzielonego, takich jak wymagania dotyczące zasad lub kontroli dostępu opartej na rolach (RBAC). Grup zasobów nie można zagnieżdżać, a zasoby mogą należeć tylko do jednej grupy zasobów. Wszystkie akcje płaszczyzny sterowania działają na wszystkie zasoby w grupie zasobów. Na przykład usunięcie grupy zasobów powoduje również usunięcie wszystkich zasobów w obrębie tej grupy. Zgodnie z preferowanym wzorcem zarządzania grupami zasobów należy rozważyć następujące kwestie:

1. Czy zawartość grupy zasobów jest wspólnie tworzona?
1. Czy zawartość grupy zasobów jest wspólnie zarządzana, aktualizowana i monitorowana? Czy wszystkie te operacje są wykonywane przez te same osoby lub zespoły?
1. Czy zawartość grupy zasobów jest wspólnie wycofywana?

Jeśli odpowiesz _Nie_ na którekolwiek z powyższych pytań, odpowiedni zasób należy umieścić w innym miejscu, w innej grupie zasobów.

> [!IMPORTANT]
> Grupy zasobów są również specyficzne dla regionu, ale typowe dla zasobów jest to, że znajdują się w różnych regionach w ramach tej samej grupy zasobów, ponieważ są wspólnie zarządzane w sposób opisany powyżej. Aby uzyskać więcej informacji na temat wyboru regionu, zobacz [Przewodnik po decyzjach związanych z regionami](../regions/index.md).

## <a name="deployment-consistency"></a>Spójność wdrożenia

Opierając się na mechanizmie podstawowego grupowania zasobów, platforma Azure udostępnia system wdrażania zasobów w środowisku chmury przy użyciu szablonów. Przy użyciu szablonów można tworzyć spójne konwencje organizacji i nazewnictwa podczas wdrażania obciążeń, wymuszając te aspekty projektu wdrażania zasobów i zarządzania.

[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/template-deployment-overview) umożliwiają wielokrotne wdrażanie zasobów w spójnym stanie przy użyciu wstępnie określonej konfiguracji i struktury grupy zasobów. Szablony usługi Resource Manager pomagają w zdefiniowaniu zestawu standardów jako podstawy dla wdrożeń.

Na przykład można mieć standardowy szablon do wdrażania obciążenia serwera internetowego, który zawiera dwie maszyny wirtualne jako serwery internetowe w połączeniu z modułem równoważenia obciążenia rozdzielającym ruch między serwerami. Za pomocą tego szablonu można ponownie utworzyć identyczny strukturalnie zestaw składający się z maszyn wirtualnych i modułu równoważenia obciążenia za każdym razem, gdy jest potrzebne tego typu obciążenie, zmieniając tylko nazwę wdrożenia i używane adresy IP.

Można również programowo wdrażać te szablony i integrować je z systemami ciągłej integracji/ciągłego wdrażania.

## <a name="policy-consistency"></a>Spójność zasad

Aby zapewnić stosowanie zasad utrzymania ładu podczas tworzenia zasobów, część projektu grupowania zasobów obejmuje użycie typowej konfiguracji podczas wdrażania zasobów.

Łącząc grupy zasobów i ustandaryzowane szablony usługi Resource Manager, można wymuszać standardy dotyczące ustawień wymaganych we wdrożeniu i reguł usługi [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) stosowanych do poszczególnych zasobów lub grup zasobów.

Na przykład może być wymagane, aby wszystkie maszyny wirtualne wdrożone w ramach subskrypcji łączyły się ze wspólną podsiecią zarządzaną przez centralny zespół IT. Można utworzyć standardowy szablon do wdrażania maszyn wirtualnych obciążenia, aby utworzyć oddzielną grupę zasobów dla obciążenia i wdrożyć w niej wymagane maszyny wirtualne. Ta grupa zasobów musiałaby mieć regułę zasad umożliwiającą dołączanie do udostępnionej podsieci tylko interfejsów sieciowych należących do grupy zasobów.

Aby uzyskać bardziej szczegółowe omówienie wymuszania decyzji dotyczących zasad w ramach wdrożenia w chmurze, zobacz [Wymuszanie zasad](../policy-enforcement/index.md).

## <a name="hierarchical-consistency"></a>Spójność hierarchiczna

Grupy zasobów umożliwiają obsługę dodatkowych poziomów hierarchii w organizacji w ramach subskrypcji dzięki stosowaniu reguł usługi Azure Policy i kontrolek dostępu na poziomie grupy zasobów. Jednak w miarę zwiększania rozmiaru infrastruktury w chmurze może być konieczna obsługa bardziej skomplikowanych wymagań dotyczących ładu między subskrypcjami, z których można korzystać, używając hierarchii Przedsiębiorstwo/Dział/Konto/Subskrypcja w ramach umowy Azure Enterprise Agreement.

[Grupy zarządzania platformy Azure](https://docs.microsoft.com/azure/governance/management-groups) umożliwiają organizowanie subskrypcji w bardziej zaawansowane struktury organizacyjne dzięki możliwości grupowania ich w hierarchię inną niż hierarchia z umowy Enterprise Agreement. Ta alternatywna hierarchia umożliwia stosowanie kontroli dostępu i mechanizmów wymuszania zasad w wielu subskrypcjach i zawartych w nich zasobach. Hierarchie grup zarządzania umożliwiają dopasowywanie subskrypcji infrastruktury w chmurze do operacji lub wymagań dotyczących ładu biznesowego. Aby uzyskać więcej informacji, zobacz [przewodnik po decyzji dotyczącej subskrypcji](../subscriptions/index.md).

## <a name="automated-consistency"></a>Spójność zautomatyzowana

W przypadku dużych wdrożeń w chmurze ład globalny staje się ważniejszy i bardziej skomplikowany. Kluczowe jest automatyczne stosowanie i wymuszanie wymagań w zakresie utrzymania ładu podczas wdrażania zasobów, a także spełnianie zaktualizowanych wymagań dotyczących istniejących wdrożeń.

Usługa [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) umożliwia organizacjom obsługę globalnego ładu dla dużych infrastruktur w chmurze na platformie Azure. Usługa Blueprints ma dużo większe możliwości tworzenia kompletnych aranżacji procesu wdrażania, które umożliwiają wdrażanie zasobów i stosowanie reguł zasad, niż standardowe szablony usługi Azure Resource Manager. Usługa Blueprints umożliwia obsługę wersji, aktualizowanie wszystkich subskrypcji, w których została użyta strategia, oraz blokowanie wdrożonych subskrypcji w celu uniknięcia nieautoryzowanego tworzenia i modyfikowania zasobów.

Te pakiety wdrożeniowe umożliwiają zespołom informatyków i deweloperów błyskawiczne wdrażanie nowych obciążeń i zasobów sieciowych zgodnych ze zmieniającymi się wymaganiami w zakresie zasad organizacyjnych. Usługę Blueprints można również zintegrować z potokami ciągłej integracji/ciągłego wdrażania, aby stosować poprawione standardy utrzymania ładu do wdrożeń podczas ich aktualizowania.

## <a name="next-steps"></a>Następne kroki

Spójność zasobów to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
