---
title: Wyrównywanie obowiązków między zespołami
description: Dowiedz się, jak wyrównać zakres obowiązków między zespołami.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 87ff20e3e81b8b01e6405984a63a9192184a4fa5
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76800699"
---
# <a name="align-responsibilities-across-teams"></a>Wyrównaj odpowiedzialności między zespołami

Dowiedz się, jak wyrównać zakres obowiązków dla zespołów, opracowując macierz międzyzespołową, która identyfikuje osoby odpowiedzialne, obsługujące, *konsultowane i poinformowane* (Raci). Ten artykuł zawiera przykładową matrycę RACI dla struktur organizacyjnych opisanych w temacie [ustanawianie struktur zespołu](./organization-structures.md):

- [Tylko zespół wdrażania chmury](#cloud-adoption-team-only)
- [Najlepsze rozwiązanie MVP](#best-practice-minimum-viable-product-mvp)
- [Środkowe IT](#central-it)
- [Wyrównanie strategiczne](#strategic-alignment)
- [Wyrównanie operacyjne](#operational-alignment)
- [Cloud Center doskonałości (CCoE)](#cloud-center-of-excellence-ccoe)

Aby śledzić decyzje dotyczące struktury organizacyjnej w miarę upływu czasu, należy pobrać i zmodyfikować [szablon arkusza kalkulacyjnego Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).

Przykłady w tym artykule określają następujące konstrukcje RACI:

- Jeden zespół, który jest *odpowiedzialny* za funkcję.
- Zespoły *odpowiedzialne* za wyniki.
- Zespoły, które powinny być *konsultowane* podczas planowania.
- Zespoły, które powinny być *poinformowane* po zakończeniu pracy.

Ostatni wiersz każdej tabeli (z wyjątkiem pierwszej) zawiera link do najbardziej wyrównanej możliwości chmury w celu uzyskania dodatkowych informacji.

## <a name="cloud-adoption-team-only"></a>Tylko zespół wdrażania chmury

|  |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury |Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|

## <a name="best-practice-minimum-viable-product-mvp"></a>Najlepsze rozwiązanie: minimalny produkt żywotny (MVP)

|  |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury|Accountable|Accountable|Accountable|Accountable|Zapoznaj się z tematem|Zapoznaj się z tematem|Zapoznaj się z tematem|Nich|
|Zespół nadzorujący chmury|Zapoznaj się z tematem|Nich|Nich|Nich|Accountable|Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[zarządzanie chmurą](./cloud-governance.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md)|

## <a name="central-it"></a>Centralne zasoby IT

| |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury  |Accountable|Accountable|Prowadzenie    |Prowadzenie|Nich   |Nich   |Nich   |Nich   |
|Zespół nadzorujący chmury|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Zapoznaj się z tematem  |Prowadzenie|Nich   |
|Centralne zasoby IT           |Zapoznaj się z tematem  |Nich   |Accountable   |Accountable   |Prowadzenie  |Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[Ład w chmurze](./cloud-governance.md)|[Środkowe IT](./central-it.md)|[Środkowe IT](./central-it.md)|[Środkowe IT](./central-it.md)|

## <a name="strategic-alignment"></a>Wyrównanie strategiczne

|  |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Accountable|Nich   |Nich   |Nich   |Nich   |
|CCoE model RACI      |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[zarządzanie chmurą](./cloud-governance.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md)|

## <a name="operational-alignment"></a>Wyrównanie operacyjne

|  |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Nich   |
|Zespół ds. operacji w chmurze|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Prowadzenie|Accountable|Zapoznaj się z tematem  |Nich   |Accountable|Zapoznaj się z tematem  |
|CCoE model RACI      |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Accountable|Prowadzenie|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[zarządzanie chmurą](./cloud-governance.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md)|

## <a name="cloud-center-of-excellence-ccoe"></a>Cloud Center doskonałości (CCoE)

|  |Dostarczanie rozwiązania  |Spójność biznesowa  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje platformy  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Nich   |
|Zespół ds. operacji w chmurze|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Prowadzenie|Accountable|Zapoznaj się z tematem  |Nich   |Accountable|Zapoznaj się z tematem  |
|Zespół nadzorujący chmury|Zapoznaj się z tematem  |Nich   |Nich   |Zapoznaj się z tematem  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Nich   |
|Zespół platformy w chmurze  |Zapoznaj się z tematem  |Nich   |Nich   |Zapoznaj się z tematem  |Zapoznaj się z tematem  |Accountable|Prowadzenie|Prowadzenie|
|Zespół usługi Cloud Automation|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Zapoznaj się z tematem  |Prowadzenie|Prowadzenie|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[zarządzanie chmurą](./cloud-governance.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|Platforma [CCoE](./cloud-center-of-excellence.md)-w [chmurze](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md)|

## <a name="next-steps"></a>Następne kroki

Aby śledzić decyzje dotyczące struktury organizacji w miarę upływu czasu, należy pobrać i zmodyfikować [szablon arkusza kalkulacyjnego Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx). Skopiuj i zmodyfikuj najlepiej wyrównany przykład z macierzy RACI w tym artykule.

> [!div class="nextstepaction"]
> [Pobierz szablon arkusza kalkulacyjnego odpowiedzialności](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)
