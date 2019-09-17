---
title: Wyrównywanie obowiązków między zespołami
titleSuffix: Microsoft Cloud adoption Framework for Azure
description: Dowiedz się, jak wyrównać zakres obowiązków między zespołami.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 818d2fa74c480b8aee36c4d268ae7a83cb93fab3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71027256"
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

|  |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury |Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|Accountable|

## <a name="best-practice-minimum-viable-product-mvp"></a>Najlepsze rozwiązanie: minimalny produkt żywotny (MVP)

|  |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury|Accountable|Accountable|Accountable|Accountable|Zapoznaj się z tematem|Zapoznaj się z tematem|Zapoznaj się z tematem|Nich|
|Zespół nadzorujący chmury|Zapoznaj się z tematem|Nich|Nich|Nich|Accountable|Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[ładu w chmurze](./cloud-governance.md)|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md) CCoE|

## <a name="central-it"></a>Centralne zasoby IT

| |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół ds. wdrażania chmury  |Accountable|Accountable|Prowadzenie    |Prowadzenie|Nich   |Nich   |Nich   |Nich   |
|Zespół nadzorujący chmury|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Zapoznaj się z tematem  |Prowadzenie|Nich   |
|Centralne zasoby IT           |Zapoznaj się z tematem  |Nich   |Accountable   |Accountable   |Prowadzenie  |Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[Ład w chmurze](./cloud-governance.md)|[Środkowe IT](./central-it.md)|[Środkowe IT](./central-it.md)|[Środkowe IT](./central-it.md)|

## <a name="strategic-alignment"></a>Wyrównanie strategiczne

|  |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Accountable|Nich   |Nich   |Nich   |Nich   |
|CCoE model RACI      |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Accountable|Accountable|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[ładu w chmurze](./cloud-governance.md)|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md) CCoE|

## <a name="operational-alignment"></a>Wyrównanie operacyjne

|  |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Nich   |
|Zespół ds. operacji w chmurze|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Prowadzenie|Accountable|Zapoznaj się z tematem  |Nich   |Accountable|Zapoznaj się z tematem  |
|CCoE model RACI      |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Accountable|Accountable|Prowadzenie|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[ładu w chmurze](./cloud-governance.md)|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md) CCoE|

## <a name="cloud-center-of-excellence-ccoe"></a>Cloud Center doskonałości (CCoE)

|  |Dostarczanie rozwiązania  |Wyrównanie biznesowe  |Zarządzanie zmianami  |Operacje rozwiązania  |Ład |Data_spłaty platformy  |Operacje na platformie  |Automatyzacja platformy  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Zespół strategii chmury  |Zapoznaj się z tematem  |Accountable|Accountable|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Nich   |Nich   |Nich   |
|Zespół ds. wdrażania chmury  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Nich   |
|Zespół ds. operacji w chmurze|Zapoznaj się z tematem  |Zapoznaj się z tematem  |Prowadzenie|Accountable|Zapoznaj się z tematem  |Nich   |Accountable|Zapoznaj się z tematem  |
|Zespół nadzorujący chmury|Zapoznaj się z tematem  |Nich   |Nich   |Zapoznaj się z tematem  |Accountable|Zapoznaj się z tematem  |Prowadzenie|Nich   |
|Zespół platformy w chmurze  |Zapoznaj się z tematem  |Nich   |Nich   |Zapoznaj się z tematem  |Zapoznaj się z tematem  |Accountable|Prowadzenie|Prowadzenie|
|Zespół usługi Cloud Automation|Zapoznaj się z tematem  |Nich   |Nich   |Nich   |Zapoznaj się z tematem  |Prowadzenie|Prowadzenie|Accountable|
||||||||||
|Wyrównana możliwość chmury|[Wdrażanie chmury](./cloud-adoption.md)|[Strategia chmury](./cloud-strategy.md)|[Strategia chmury](./cloud-strategy.md)|[Operacje w chmurze](./cloud-operations.md)|[](./cloud-center-of-excellence.md)CCoE-[ładu w chmurze](./cloud-governance.md)|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Platforma w chmurze](./cloud-platform.md) CCoE|[](./cloud-center-of-excellence.md)-[Automatyzacja chmury](./cloud-automation.md) CCoE|

## <a name="next-steps"></a>Następne kroki

Aby śledzić decyzje dotyczące struktury organizacji w miarę upływu czasu, należy pobrać i zmodyfikować [szablon arkusza kalkulacyjnego Raci](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx). Skopiuj i zmodyfikuj najlepiej wyrównany przykład z macierzy RACI w tym artykule.

> [!div class="nextstepaction"]
> [Pobierz szablon arkusza kalkulacyjnego odpowiedzialności](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)
