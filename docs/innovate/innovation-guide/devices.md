---
title: 'Innowacje na platformie Azure: Interakcja za pomocą urządzeń'
description: Dowiedz się, jak platforma Azure zapewnia strukturę do tworzenia atrakcyjnych i efektywnych rozwiązań biznesowych za pośrednictwem połączonych i perceptywnych urządzeń brzegowych.
author: umarmohamedusman
ms.author: umarm
ms.date: 10/10/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0b876c402f18492b956b5ae561107ec6b57e63ee
ms.sourcegitcommit: bd9872320b71245d4e9a359823be685e0f4047c5
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83862113"
---
<!-- cSpell:ignore umarmohamedusman umarm Moovit -->

::: zone target="docs"

# <a name="azure-innovation-guide-interact-through-devices"></a>Przewodnik po innowacjach na platformie Azure: Interakcja za pośrednictwem urządzeń

::: zone-end

::: zone target="chromeless"

# <a name="interact-through-devices"></a>Interakcja za pośrednictwem urządzeń

::: zone-end

Wprowadzaj innowacje za pośrednictwem perceptywnych i połączonych tymczasowo urządzeń brzegowych. Organizuj miliony takich urządzeń, uzyskując i przetwarzając nieograniczone ilości danych, i korzystaj z rosnącej liczby środowisk obejmujących wiele czujników i urządzeń. Platforma Azure udostępnia strukturę, która umożliwia tworzenie angażujących i efektywnych rozwiązań biznesowych, korzystających z urządzeń znajdujących się na granicy sieci. Wszechobecne przetwarzanie, oparte na połączeniu platformy Azure z technologią sztucznej inteligencji, pozwala tworzyć dowolne typy inteligentnych aplikacji i systemów, jakie można sobie wyobrazić.

Klienci platformy Azure korzystają z ciągle rozszerzającego się zbioru połączonych systemów i urządzeń, które zbierają i analizują dane &mdash; blisko użytkowników i danych. Użytkownicy korzystają ze środowisk oraz analiz udostępnianych w czasie rzeczywistym i dostarczanych przez szybko reagujące aplikacje kontekstowe. Dzięki przeniesieniu części obciążenia na granicę sieci urządzenia wysyłają mniej komunikatów do chmury i szybciej reagują na zdarzenia przestrzenne.

> [!div class="checklist"]
>
> - Zasoby przemysłowe
> - [Microsoft HoloLens 2](https://docs.microsoft.com/hololens)
> - [Azure Sphere](https://docs.microsoft.com/azure-sphere/product-overview/what-is-azure-sphere)
> - [Azure Kinect DK](https://docs.microsoft.com/azure/kinect-dk/about-azure-kinect-dk)
> - Drony
> - [Azure SQL Edge](https://docs.microsoft.com/azure/azure-sql-edge/overview)
> - [IoT Plug and Play](https://docs.microsoft.com/azure/iot-pnp/overview-iot-plug-and-play)

<!-- markdownlint-disable MD025 -->

## <a name="global-scale-iot-service"></a>[Globalna usługa IoT](#tab/IoTHub)

<!-- markdownlint-enable MD025 -->

Projektuj rozwiązania umożliwiające dwukierunkową komunikację z miliardami urządzeń IoT. Korzystaj z gotowych danych telemetrycznych urządzenie-chmura, aby rozumieć stan urządzeń i definiować trasy komunikatów do innych usług platformy Azure wyłącznie za pośrednictwem konfiguracji. W ramach komunikatów przesyłanych z chmury do urządzeń możesz niezawodnie przesyłać polecenia i powiadomienia do połączonych urządzeń, a także śledzić dostarczanie komunikatów za pomocą potwierdzeń dostarczenia. Ponadto w razie potrzeby możesz automatycznie wysyłać ponownie komunikaty do urządzeń, korzystając ze sporadycznej łączności.

Oto kilka z dostępnych funkcji:

- **Kanał komunikacyjny z rozszerzonymi zabezpieczeniami** umożliwiający wysyłanie i odbieranie danych z urządzeń IoT.
- **Wbudowane funkcje zarządzania urządzeniami** i aprowizacji umożliwiające nawiązywanie połączeń z urządzeniami IoT i zarządzanie nimi w dużej skali.
- **Pełna integracja z usługą Event Grid** i bezserwerowe środowisko obliczeniowe upraszczające tworzenie aplikacji IoT.
- **Zgodność z usługą Azure IoT Edge** na potrzeby tworzenia hybrydowych aplikacji IoT.

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [IoT Hub](https://docs.microsoft.com/azure/iot-hub)

- [Usługa Azure IoT Hub Device Provisioning Service (DPS)](https://docs.microsoft.com/azure/iot-dps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby utworzyć centrum IoT:

1. Zobacz **IoT Hub**.
2. Wybierz pozycję **Utwórz centrum IoT**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FIotHubs]" submitText="Go to IoT Hub" :::

<!-- markdownlint-enable DOCSMD001 -->

Usługa Azure IoT Hub Device Provisioning to usługa pomocnika usługi IoT Hub zapewniająca bezobsługowe aprowizowanie urządzeń „just in time”.

<!-- markdownlint-disable MD024 -->

### <a name="action"></a>Akcja

Aby utworzyć usługę Azure IoT Hub Device Provisioning Service:

1. Przejdź do pozycji **Usługi Device Provisioning**.
2. Wybierz pozycję **Dodaj**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Devices%2FProvisioningServices]" submitText="Go to Device Provisioning Services" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="azure-digital-twins"></a>[Azure Digital Twins](#tab/DigitalTwins)

Twórz przestrzenne środowiska wielokrotnego użytku o wysokim stopniu skalowalności, które umożliwiają łączenie danych przesyłanych strumieniowo między światem fizycznym i światem cyfrowym. Zwiększ zaangażowanie klientów przy użyciu kompleksowych modeli środowisk fizycznych. Generuj wykresy analizy przestrzennej do modelowania relacji i interakcji między osobami, obszarami oraz urządzeniami. Wykonuj zapytania o dane z przestrzeni fizycznej, a nie z poziomu różnych czujników.

**Modele obiektów usługi Azure Digital Twins:** Przy użyciu modeli obiektów usługi Digital Twins można przedstawiać ontologię opisującą regiony, miejsca, piętra, biura, strefy i sale konferencyjne w budynku inteligentnym albo zakłady wytwarzające energię wraz ze stacjami podrzędnymi, zasoby energetyczne, a także klientów sieci energetycznej.

**Wykres analizy przestrzennej:** Hierarchiczny wykres przedstawiający obszary, urządzenia i osoby, zdefiniowany w modelu obiektów usługi Digital Twins, który obsługuje dziedziczenie, filtrowanie, przechodzenie, skalowalność i rozszerzalność. Przy użyciu kolekcji interfejsów API REST hostowanych na platformie Azure można korzystać z wykresu przestrzennego i zarządzać nim.

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Digital Twins](https://docs.microsoft.com/azure/digital-twins/about-digital-twins)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby utworzyć wystąpienie usługi Azure Digital Twins:

1. W okienku po lewej stronie wybierz pozycję **Utwórz zasób**.
2. Wyszukaj pozycję **digital twins** i wybierz pozycję **Digital Twins**.
3. Wybierz przycisk **Utwórz**, aby rozpocząć proces wdrażania.
4. Aby przejrzeć istniejące usługi Digital Twins, wybierz ten przycisk:

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.IoTSpaces%2FGraph]" submitText="Go to Digital Twins" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

<!-- markdownlint-disable MD025 -->

## <a name="location-intelligence"></a>[Analiza lokalizacji](#tab/AzureMaps)

Oprócz tradycyjnych możliwości używania lokalizacji, takich jak pobliskie miejsca, ruch i routing, usługa Azure Maps umożliwia przedsiębiorstwom tworzenie rozwiązań korzystających z analizy lokalizacji w czasie rzeczywistym i opartych na światowej klasy produktach w dziedzinie technologii mobilnych, opracowanych przez takich partnerów jak **TomTom** i **Moovit**. Łatwo integruj zaawansowane możliwości obsługi lokalizacji i mobilności z własnymi aplikacjami dzięki usługom geoprzestrzennym.

**Data Service (wersja zapoznawcza):** Przekazuj i przechowuj dane geoprzestrzenne do użycia na potrzeby operacji przestrzennych lub kompozycji obrazów w celu zmniejszania opóźnienia, zwiększania produktywności i włączania nowych scenariuszy w aplikacjach.

**Operacje przestrzenne:** Poszerz analizę lokalizacji, korzystając z biblioteki typowych geoprzestrzennych obliczeń matematycznych, w tym wirtualnego grodzenia, najbliższego punktu, długości ortodromy i buforów.

**Geolokalizacja:** Wyszukaj kraj, w którym znajduje się dany adres IP. Dostosowuj zawartość i usługi na podstawie lokalizacji użytkownika i uzyskuj informacje o dystrybucji geograficznej użytkowników.

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Maps](https://docs.microsoft.com/azure/azure-maps)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby użyć analizy lokalizacji:

1. Wybierz pozycję **Konta usługi Azure Maps**.
2. Wybierz pozycję **Utwórz konta usługi Azure Maps**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Maps%2FAccounts]" submitText="Go to Azure Maps Account" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="spatial-experiences"></a>[Środowiska przestrzenne](#tab/spatial)

Usługa Azure Spatial Anchors umożliwia deweloperom pracę z platformami rzeczywistości mieszanej w celu obserwowania przestrzeni, wyznaczania dokładnych punktów orientacyjnych i przywoływania tych punktów orientacyjnych z obsługiwanych urządzeń.

**Dodawanie kontekstu do świata rzeczywistego:** Pozwól użytkownikom lepiej zrozumieć ich dane (w odpowiednim miejscu i czasie), umieszczając treści cyfrowe i łącząc je z fizycznymi punktami orientacyjnymi.

**Udostępnianie hologramów na różnych urządzeniach:** Przyspiesz podejmowanie decyzji i uzyskiwanie wyników, dostarczając członkom zespołu i klientom obraz 3D na wybranych przez nich urządzeniach. Usługa Spatial Anchors ułatwia osobom przebywającym w tym samym miejscu korzystanie z aplikacji rzeczywistości mieszanej dla wielu użytkowników.

**Angażujące środowiska:** Utwórz relacje między zakotwiczeniami przestrzennymi, łącząc je ze sobą, w celu udostępnienia środowiska użytkownika, które może zawierać co najmniej dwa punkty orientacyjne umożliwiające użytkownikom wykonywanie zadań. Twoja aplikacja może pozwalać użytkownikom na umieszczanie wirtualnych artefaktów w świecie rzeczywistym. W środowisku przemysłowym użytkownik może otrzymywać informacje kontekstowe o maszynie, kierując na nią aparat obsługiwanego urządzenia.

Usługa Azure Spatial Anchors składa się z usługi zarządzanej i zestawów SDK klienta dla obsługiwanych platform urządzeń.

::: zone target="docs"

- [Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby używać środowisk przestrzennych:

1. Wybierz pozycję **Konta zakotwiczeń przestrzennych**.
2. Wybierz pozycję **Utwórz konta zakotwiczeń przestrzennych**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResource/resourceType/Microsoft.MixedReality%2FSpatialAnchorsAccounts]" submitText="Go to Spatial Anchors Accounts" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end

## <a name="azure-remote-rendering"></a>[Azure Remote Rendering](#tab/RemoteRender)

Renderuj w chmurze interaktywną zawartość 3D w wysokiej jakości i przesyłaj ją strumieniowo do urządzeń w czasie rzeczywistym. Obciążenia renderowania są powszechnie używane do tworzenia efektów specjalnych (VFX) w branży multimedialnej i rozrywkowej. Renderowanie jest również używane w wielu innych sektorach, takich jak reklama, produkcja, handel detaliczny oraz przemysł naftowy.

Proces renderowania wymaga dużej mocy obliczeniowej. Liczba generowanych ramek lub obrazów jest duża, a renderowanie każdego obrazu może trwać wiele godzin. Z tego względu renderowanie doskonale się nadaje do równoległego przetwarzania wsadowego, opartego na platformie Azure i usłudze Azure Batch.

::: zone target="docs"

### <a name="learn-more"></a>Dowiedz się więcej

- [Azure Remote Rendering](https://azure.microsoft.com/services/remote-rendering)

- [Renderowanie przy użyciu platformy Azure](https://docs.microsoft.com/azure/batch/batch-rendering-service)

::: zone-end

::: zone target="chromeless"

### <a name="action"></a>Akcja

Aby użyć usługi Remote Rendering:

1. Wybierz pozycję **Konta usługi Batch**.
2. Wybierz pozycję **Utwórz konta usługi Batch**.

<!-- markdownlint-disable DOCSMD001 -->

::: form action="OpenBlade[#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Batch%2FBatchAccounts]" submitText="Go to Azure Batch" :::

<!-- markdownlint-enable DOCSMD001 -->

::: zone-end
