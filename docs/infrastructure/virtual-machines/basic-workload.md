---
title: Wdrażanie podstawowego obciążenia na platformie Azure
description: Zapoznaj się z podstawowymi składnikami infrastruktury chmurowej i podstawowymi obciążeniami, takimi jak podstawowe aplikacje sieci Web, pojedyncze maszyny wirtualne i sieci wirtualne.
author: alexbuckgit
ms.author: abuck
ms.date: 12/31/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 015999a9852625abe4ad02a60ad37fc162dd4861
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80425429"
---
# <a name="deploy-a-basic-workload-in-azure"></a>Wdrażanie podstawowego obciążenia na platformie Azure

Termin *obciążenie* jest zwykle definiowany jako samodzielna jednostka funkcjonalności, taka jak aplikacja lub usługa. Pomaga to w zapewnieniu obciążenia pod względem artefaktów kodu wdrożonych na serwerze, a także innych usług specyficznych dla aplikacji. Może to być przydatna definicja lokalnej aplikacji lub usługi, ale dla aplikacji w chmurze, które muszą być rozwinięte.

W chmurze obciążenie nie obejmuje tylko wszystkich artefaktów, ale również obejmuje także zasoby chmury. Uwzględniono zasoby w chmurze w ramach definicji ze względu na koncepcję znaną jako "infrastruktura jako kod". Jak już wiesz, [jak działa platforma Azure?](../../getting-started/what-is-azure.md), zasoby na platformie Azure są wdrażane przez usługę Orchestrator. Ta usługa Orchestrator udostępnia funkcje za pośrednictwem internetowego interfejsu API i można wywołać interfejs API sieci Web przy użyciu kilku narzędzi, takich jak program PowerShell, interfejs wiersza polecenia platformy Azure i Azure Portal. Oznacza to, że można określić zasoby platformy Azure w pliku możliwym do odczytu maszynowego, który może być przechowywany wraz z artefaktami kodu skojarzonymi z aplikacją.

Umożliwia to zdefiniowanie obciążenia w postaci artefaktów kodu i niezbędnych zasobów w chmurze, a tym samym umożliwienie odizolowania obciążeń. Obciążenia można izolować według sposobu organizowania zasobów, topologii sieci lub innych atrybutów. Celem izolacji obciążeń jest skojarzenie określonych zasobów obciążenia z zespołem, dzięki czemu zespół może niezależnie zarządzać wszystkimi aspektami tych zasobów. Umożliwia to wielu zespołom udostępnianie usług zarządzania zasobami na platformie Azure, jednocześnie zapobiegając przypadkowemu usunięciu lub modyfikacji zasobów.

Ta izolacja umożliwia również kolejną koncepcję, znaną jako DevOps. DevOps obejmuje praktyki programistyczne oprogramowania, które obejmują zarówno rozwój oprogramowania, jak i operacje IT, a także używa automatyzacji, jak to możliwe. Jedna z zasad DevOps jest znana jako ciągła integracja i ciągłe dostarczanie (CI/CD). Ciągła integracja dotyczy zautomatyzowanych procesów kompilacji, które są uruchamiane za każdym razem, gdy deweloper zatwierdzi zmianę kodu. Ciągłe dostarczanie odnosi się do zautomatyzowanych procesów, które wdrażają ten kod w różnych środowiskach, takich jak środowisko programistyczne do testowania lub środowisko produkcyjne do wdrożenia końcowego.

## <a name="basic-workload"></a>Podstawowe obciążenie

*Podstawowe obciążenie* jest zwykle zdefiniowane jako jedna aplikacja sieci Web lub Sieć wirtualna (VNET) z maszyną wirtualną.

> [!NOTE]
> Ten przewodnik nie obejmuje opracowywania aplikacji. Aby uzyskać więcej informacji na temat tworzenia aplikacji na platformie Azure, zobacz [Przewodnik po architekturze aplikacji platformy Azure](https://docs.microsoft.com/azure/architecture/guide).

Niezależnie od tego, czy obciążenie jest aplikacją sieci Web, czy maszyną wirtualną, każde z tych wdrożeń wymaga *grupy zasobów*. Użytkownik z uprawnieniami do tworzenia grupy zasobów musi wykonać tę czynność przed wykonaniem poniższych kroków.

## <a name="basic-web-application-paas"></a>Podstawowa aplikacja internetowa (PaaS)

W przypadku podstawowej aplikacji sieci Web Wybierz jeden z 5-minutowego przewodnika Szybki Start z [dokumentacji usługi Web Apps](https://docs.microsoft.com/azure/app-service) i postępuj zgodnie z instrukcjami.

> [!NOTE]
> Niektóre Przewodniki Szybki Start będą wdrażać grupę zasobów domyślnie. W takim przypadku nie jest konieczne jawne utworzenie grupy zasobów. W przeciwnym razie Wdróż aplikację sieci Web w utworzonej powyżej grupie zasobów.

Po wdrożeniu prostego obciążenia można dowiedzieć się więcej o najlepszych rozwiązaniach dotyczących wdrażania [podstawowej aplikacji sieci Web](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/basic-web-app) na platformie Azure.

## <a name="single-windows-or-linux-vm-iaas"></a>Pojedyncza maszyna wirtualna z systemem Windows lub Linux (IaaS)

W przypadku prostego obciążenia, które jest uruchamiane na maszynie wirtualnej, pierwszym krokiem jest wdrożenie sieci wirtualnej. Wszystkie zasoby infrastruktury jako usługi (IaaS) na platformie Azure, takie jak maszyny wirtualne, moduły równoważenia obciążenia i bramy, wymagają sieci wirtualnej. Dowiedz się więcej o [usłudze Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), a następnie postępuj zgodnie z instrukcjami dotyczącymi [wdrażania Virtual Network na platformie Azure przy użyciu portalu](https://docs.microsoft.com/azure/virtual-network/quick-create-portal). Po określeniu ustawień sieci wirtualnej w Azure Portal należy określić nazwę utworzonej powyżej grupy zasobów.

Następnym krokiem jest podjęcie decyzji o tym, czy wdrożyć pojedynczą maszynę wirtualną z systemem Windows lub Linux. W przypadku maszyny wirtualnej z systemem Windows wykonaj kroki, aby [wdrożyć maszynę wirtualną z systemem Windows na platformie Azure przy użyciu portalu](https://docs.microsoft.com/azure/virtual-machines/windows/quick-create-portal). Po określeniu ustawień dla maszyny wirtualnej w Azure Portal należy określić nazwę utworzonej powyżej grupy zasobów.

Po wykonaniu kroków i wdrożeniu maszyny wirtualnej można zapoznać się z [najlepszymi rozwiązaniami dotyczącymi uruchamiania maszyn wirtualnych z systemem Windows na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/single-vm). W przypadku maszyny wirtualnej z systemem Linux postępuj zgodnie z instrukcjami, aby [wdrożyć maszynę wirtualną z systemem Linux na platformie Azure przy użyciu portalu](https://docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal). Możesz również dowiedzieć się więcej o [najlepszych rozwiązaniach dotyczących uruchamiania maszyny wirtualnej z systemem Linux na platformie Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-linux/single-vm).

## <a name="next-steps"></a>Następne kroki

Zobacz [przewodniki dotyczące podejmowania decyzji dotyczących architektury](../../decision-guides/index.md) , jak używać podstawowych składników infrastruktury w chmurze platformy Azure.
