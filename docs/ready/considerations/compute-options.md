---
title: Przejrzyj opcje obliczeń
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak ustalić wymagania dotyczące obliczeń dotyczących obsługi obciążeń.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: ded91b479fc18a832aa1f977284f979dcb9856bb
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80432148"
---
# <a name="review-your-compute-options"></a>Przejrzyj opcje obliczeń

Określenie wymagań obliczeniowych dotyczących hostowania obciążeń jest najważniejszym zagadnieniem podczas przygotowywania do wdrożenia chmury. Produkty i usługi obliczeniowe platformy Azure obsługują szeroką gamę scenariuszy i możliwości obliczeniowych obciążeń. Sposób konfigurowania środowiska strefy docelowej do obsługi wymagań obliczeniowych zależy od wymagań technicznych i biznesowych oraz związanych z zarządzaniem, które dotyczą obciążenia.

## <a name="identify-compute-services-requirements"></a>Identyfikowanie wymagań usług obliczeniowych

W ramach oceny i przygotowania strefy docelowej należy zidentyfikować funkcje sieciowe, które muszą być przez nią obsługiwane. Ten proces polega na ocenie poszczególnych aplikacji i usług, które składają się na obciążenia, w celu określenia wymagań dotyczących środowiska obliczeniowego i hostingu. Po zidentyfikowaniu i udokumentowaniu wymagań można utworzyć zasady dla strefy docelowej w celu kontrolowania dozwolonych typów zasobów i konfiguracji w zależności od potrzeb związanych z obciążeniem.

W przypadku każdej aplikacji lub usługi, która zostanie wdrożona w środowisku strefy docelowej, należy skorzystać z następującego drzewa decyzyjnego jako punktu wyjścia, aby ułatwić określenie wymagań dotyczących usług obliczeniowych:

![Drzewo decyzyjne usług obliczeniowych platformy Azure](../../_images/ready/compute-decision-tree.png)

> [!NOTE]
> Więcej informacji na temat sposobów oceny opcji środowiska obliczeniowego dla poszczególnych aplikacji lub usług zawiera [przewodnik dotyczący architektury aplikacji na platformie Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview).

### <a name="key-questions"></a>Kluczowe pytania

Odpowiedz na następujące pytania dotyczące obciążeń, aby ułatwić podejmowanie decyzji na podstawie drzewa decyzyjnego usług obciążeniowych platformy Azure:

- **Tworzysz nowe aplikacji i usługi czy przeprowadzasz migrację z istniejących obciążeń lokalnych?** Tworzenie nowych aplikacji w ramach działań związanych z wdrażaniem w chmurze umożliwia pełne wykorzystanie nowoczesnych technologii hostingu opartego na chmurze od etapu projektowania.
- **Czy w przypadku migrowania istniejących obciążeń można korzystać z nowoczesnych technologii chmurowych?** Migrowanie obciążeń lokalnych wymaga analizy: można łatwo zoptymalizować istniejące aplikacje i usługi, aby móc korzystać z nowoczesnych technologii chmurowych, czy też rozwiązanie _i przesunięcia_ przewyższają wydajność dla obciążeń?
- **Czy aplikacje lub usługi mogą korzystać z kontenerów?** Jeśli Twoje aplikacje są dobrymi kandydatami do hostingu w kontenerach, możesz korzystać z efektywnego użycia zasobów, skalowalności i możliwości aranżacji oferowanych przez [usługi kontenerów platformy Azure](https://azure.microsoft.com/product-categories/containers). Do trwałego magazynowania konteneryzowanych aplikacji można używać usług [Azure Disk Storage](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) i [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).
- **Czy aplikacje są oparte na sieci Web czy na interfejsie API i czy korzystają z technologii PHP, ASP.NET, Node.js lub podobnych?** Aplikacje internetowe można wdrażać w zarządzanych wystąpieniach usługi [Azure App Service](https://docs.microsoft.com/azure/app-service/overview), dzięki czemu nie trzeba obsługiwać maszyn wirtualnych na potrzeby hostingu.
- **Czy wymagana będzie pełna kontrola nad systemem operacyjnym i środowiskiem hostingu obciążenia?** Jeśli istnieje potrzeba kontroli środowiska hostingu, w tym systemu operacyjnego, dysków, oprogramowania uruchamianego lokalnie i innych konfiguracji, aplikacje i usługi można hostować w usłudze [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines). Oprócz wyboru rozmiaru i warstw wydajności maszyny wirtualnej decyzje dotyczące magazynu dysków wirtualnych będą mieć wpływ na wydajność i umowy SLA związane z obciążeniami opartymi na rozwiązaniu infrastruktury jako usługi (IaaS). Aby uzyskać więcej informacji, zobacz dokumentację dotyczącą funkcji [Azure Disk Storage](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).
- **Czy obciążenie obejmuje możliwości obliczeń o wysokiej wydajności (HPC)?** Usługa [Azure Batch](https://docs.microsoft.com/azure/batch/batch-technical-overview) umożliwia planowanie zadań i automatyczne skalowanie zasobów obliczeniowych jako usługa platformy, co ułatwia uruchamianie na dużą skalę aplikacji równoległych i aplikacji HPC w chmurze.
- **Czy aplikacje będą korzystać z architektury mikrousług?** Aplikacje używające architektury opartej na mikrousługach mogą korzystać z zalet kilku zoptymalizowanych technologii obliczeniowych. Samodzielne obciążenia sterowane zdarzeniami mogą korzystać z usługi [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview) w celu tworzenia skalowalnych aplikacji bezserwerowych, które nie potrzebują infrastruktury. W przypadku aplikacji wymagających większej kontroli nad środowiskiem, w którym są uruchamiane mikrousługi, możesz skorzystać z usług kontenerów, takich jak [Azure Container Instances](https://docs.microsoft.com/azure/container-instances/container-instances-overview), [Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/intro-kubernetes) i [Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

> [!NOTE]
> Większość usług obliczeniowych platformy Azure jest używanych w połączeniu z usługą Azure Storage. Zapoznaj się ze [wskazówkami związanymi z podejmowaniem decyzji dotyczących magazynu](./storage-options.md), aby uzyskać informacje na temat powiązanych decyzji dotyczących magazynu.

## <a name="common-compute-scenarios"></a>Typowe scenariusze środowisk obliczeniowych

W poniższej tabeli przedstawiono kilka typowych scenariuszy użycia oraz usługi obliczeniowe zalecane do ich obsługi:

| **Scenariusz** | **Usługa obliczeniowa** |
| --- | --- |
| Chcę aprowizować maszyny wirtualne z systemami Linux i Windows w kilka sekund zgodnie z wybranymi konfiguracjami. | [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) |
| Chcę uzyskać wysoką dostępność dzięki skalowaniu automatycznemu w celu tworzenia tysięcy maszyn wirtualnych w kilka minut. | [Zestawy skalowania maszyn wirtualnych](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Chcę uprościć wdrażanie i obsługę platformy Kubernetes oraz zarządzanie nią. | [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Chcę przyspieszyć opracowywanie aplikacji za pomocą architektury bezserwerowej opartej na zdarzeniach. | [Azure Functions](https://azure.microsoft.com/services/functions) |
| Chcę tworzyć mikrousługi i aranżować kontenery w systemach Windows i Linux. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Chcę szybko tworzyć aplikacje internetowe i mobilne w chmurze za pomocą w pełni zarządzanej platformy. | [Azure App Service](https://azure.microsoft.com/services/app-service) |
| Chcę konteneryzować aplikacje i łatwo uruchamiać kontenery za pomocą jednego polecenia. | [Azure Container Instances](https://azure.microsoft.com/services/container-instances) |
| Chcę móc planować zadania i zarządzanie przetwarzaniem w skali chmury z możliwością skalowania do dziesiątek, setek lub tysięcy maszyn wirtualnych. | [Azure Batch](https://azure.microsoft.com/services/batch) |
| Chcę tworzyć aplikacje w chmurze i interfejsy API o wysokiej dostępności ułatwiające skoncentrowanie się na aplikacjach, a nie na sprzęcie. | [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services) |

## <a name="regional-availability"></a>Dostępność regionalna

Platforma Azure umożliwia dostarczanie usług w potrzebnej skali, aby dotrzeć do klientów i partnerów,  _gdziekolwiek są_. Kluczowym czynnikiem związanym z planowaniem wdrożenia w chmurze jest określenie, który region platformy Azure będzie obsługiwał zasoby obciążenia.

Niektóre opcje środowiska obliczeniowego, takie jak Azure App Service, są ogólnie dostępne w większości regionów, w których dostępna jest platforma Azure. Jednak niektóre usługi obliczeniowe są obsługiwane tylko w wybranych regionach. Niektóre typy maszyn wirtualnych i skojarzone z nimi typy magazynów mają ograniczoną dostępność regionalną. Przed podjęciem decyzji o regionach, w których zostaną wdrożone zasoby obliczeniowe, zalecamy zapoznanie się [ze stroną regionów](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines) w celu sprawdzenia najnowszego stanu dostępności regionalnej.

Aby dowiedzieć się więcej o globalnej infrastrukturze platformy Azure, zobacz  [stronę regionów platformy Azure](https://azure.microsoft.com/global-infrastructure/regions). Aby uzyskać szczegółowe informacje o tym, co jest dostępne w poszczególnych regionach platformy Azure, można także wyświetlić  [dostępność produktów według regionów](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all).

## <a name="data-residency-and-compliance-requirements"></a>Wymagania dotyczące miejsca przechowywania danych oraz ich zgodności

Wymagania prawne i umowne związane z magazynem danych będą często dotyczyć Twoich obciążeń. Te wymagania mogą się różnić w zależności od lokalizacji organizacji, jurysdykcji, w której pliki i dane są przechowywane i przetwarzane, oraz danego sektora działalności. Obowiązki związane z danymi, które należy wziąć pod uwagę, to między innymi klasyfikacja danych, lokalizacja danych oraz odpowiednie obowiązki związane z ochroną danych w ramach modelu dzielenia się odpowiedzialnością. Wiele rozwiązań obliczeniowych zależy od zasobów podłączonego magazynu. To wymaganie może mieć wpływ również na decyzje dotyczące środowiska obliczeniowego. Aby łatwiej zrozumieć te wymagania, zobacz oficjalny dokument  [Osiąganie rezydencji i bezpieczeństwa zgodnych danych na platformie Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Niektóre działania związane ze zgodnością mogą obejmować kontrolowanie, gdzie zasoby obliczeniowe będą się fizycznie znajdować. Regiony świadczenia usługi Azure są zorganizowane w grupy nazywane regionami geograficznymi.  [Lokalizacja geograficzna platformy Azure](https://azure.microsoft.com/global-infrastructure/geographies)  zapewnia, że wymagania z zakresu odporności, zgodności, niezależności i rezydencji danych są honorowane w granicach geograficznych i politycznych. Jeśli obciążenia podlegają suwerenności danych lub innym wymaganiom dotyczącym zgodności, należy wdrożyć zasoby magazynu w regionach, które znajdują się w zgodnej lokalizacji geograficznej platformy Azure.

## <a name="establish-controls-for-compute-services"></a>Ustanawianie kontrolek dla usług obliczeniowych

Podczas przygotowywania środowiska strefy docelowej można ustanowić kontrolki ograniczające zasoby, które mogą być wdrażane przez poszczególnych użytkowników. Kontrolki te ułatwiają zarządzanie kosztami i ograniczają zagrożenia bezpieczeństwa, a jednocześnie umożliwiają deweloperom i zespołom IT wdrażanie i konfigurowanie zasobów, które są potrzebne do obsługi obciążeń.

Po określeniu i udokumentowaniu wymagań strefy docelowej można użyć usługi [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) w celu kontrolowania zasobów obliczeniowych, na których tworzenie zezwolisz użytkownikom. Kontrolki mogą mieć postać [zezwolenia lub odmowy tworzenia typów zasobów obliczeniowych](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Można na przykład ograniczyć możliwości użytkowników tylko do tworzenia zasobów usługi Azure App Service lub Azure Functions. Za pomocą zasad można również kontrolować opcje dozwolone podczas tworzenia zasobu, takie jak [ograniczanie możliwości aprowizacji jednostek SKU maszyn wirtualnych](https://docs.microsoft.com/azure/governance/policy/samples/allowed-skus-storage) lub [zezwalanie tylko na określone obrazy maszyn wirtualnych](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Zakres zasad może obejmować zasoby, grupy zasobów, subskrypcje i grupy zarządzania. Zasady można uwzględniać w definicjach usługi [Azure Blueprint](https://docs.microsoft.com/azure/governance/blueprints/overview) i stosować je wielokrotnie w całej chmurze.
