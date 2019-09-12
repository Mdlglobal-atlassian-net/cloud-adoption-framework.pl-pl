---
title: 'Standardowa Przewodnik po przedsiębiorstwie: Opisowe zagadnienia związane z strategią ładu'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ten opis określa przypadek użycia dla ładu podczas podróży w ramach wdrożenia chmury w standardowej firmie.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7de9e8cd7b7b14d4ad58830da74d3206700cc61c
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908542"
---
# <a name="standard-enterprise-guide-the-narrative-behind-the-governance-strategy"></a>Standardowa Przewodnik po przedsiębiorstwie: Opisowe zagadnienia związane z strategią ładu

Poniższe kroki opisują przypadek użycia dla ładu podczas podróży w ramach wdrożenia [chmury w standardowej firmie](./index.md). Przed wdrożeniem podróży należy zrozumieć założenia i racjonalne uzasadnienie, które są odzwierciedlone w tych rozdziałach. Następnie można lepiej dostosować strategię ładu do swojej organizacji.

## <a name="back-story"></a>Historia z tyłu

Tablica dyrektorów rozpoczęła rok z planami, aby Energize działalność na kilka sposobów. Są one wypychane, aby zwiększyć komfort pracy klientów w celu uzyskania udziału w rynku. Są one również wypychane w przypadku nowych produktów i usług, które poprowadzą firmę jako lidera w branży. Zainicjowano również równoległe wysiłki w celu zmniejszenia ilości odpadów i wycinania niepotrzebnych kosztów. Chociaż zastraszanie, działania tablicy i lidera pokazują, że ten nakład pracy jest skoncentrowany jako możliwy do przyszłego wzrostu.

W przeszłości CIO firmy została wykluczona z tych strategicznych konwersacji. Jednakże, ponieważ przyszła wizja jest wewnętrznie połączona z rozwojem technicznym, ma miejsce w tabeli, aby pomóc w tym obszernym planie. Teraz oczekiwane jest dostarczenie na nowe sposoby. Zespół nie przygotowuje się do wprowadzania tych zmian i prawdopodobnie nie będzie się uczyć z krzywą szkoleniową.

## <a name="business-characteristics"></a>Charakterystyka firmy

Firma ma następujący profil biznesowy:

- Wszystkie transakcje sprzedaży i operacje znajdują się w jednym kraju z niską wartością procentową klientów globalnych.
- Firma działa jako jedna jednostka biznesowa, z uwzględnieniem budżetu w zakresie funkcji, w tym sprzedaży, marketingu, operacji i.
- Najpopularniejsze widoki biznesowe jako środki trwałe lub centrum kosztów.

## <a name="current-state"></a>Bieżący stan

Oto bieżący stan operacji w firmie i w chmurze:

- Działa dwa środowiska infrastruktury hostowanej. Jedno środowisko zawiera zasoby produkcyjne. Drugie środowisko zawiera odzyskiwanie po awarii i niektóre zasoby deweloperskie/testowe. Te środowiska są hostowane przez dwóch różnych dostawców. Odnosi się to do tych dwóch centrów danych, odpowiednio do produkcji i DR.
- Wprowadzono chmurę przez Migrowanie wszystkich kont e-mail użytkowników końcowych do pakietu Office 365. Ta migracja została ukończona sześć miesięcy temu. W chmurze wdrożono kilka innych zasobów IT.
- Zespoły deweloperów aplikacji działają w ramach możliwości tworzenia i testowania, aby dowiedzieć się więcej o możliwościach natywnych w chmurze.
- Zespół analizy biznesowej (BI) prowadzi eksperymentowanie z danymi Big Data w chmurze i nadzorowanie danych na nowych platformach.
- Firma ma zdefiniowane przez siebie zasady, które wskazują, że dane klienta i dane finansowe nie mogą być hostowane w chmurze, co ogranicza aplikacje o znaczeniu krytycznym w bieżących wdrożeniach.
- Inwestycje IT są kontrolowane w dużym stopniu według kosztów kapitałowych. Te inwestycje są planowane rocznie. W ciągu kilku lat inwestycje obejmowały nieco więcej niż podstawowe wymagania dotyczące konserwacji.

## <a name="future-state"></a>Przyszły stan

Następujące zmiany są przewidywane w ciągu następnych kilku lat:

- CIO przegląda zasady dotyczące danych osobowych i danych finansowych, aby umożliwić przyszłe cele stanu.
- Zespoły projektowe i analizy biznesowej chcą wystawić rozwiązania w chmurze w środowisku produkcyjnym w ciągu najbliższych 24 miesięcy w oparciu o wizję i nowe produkty.
- W tym roku zespół IT ukończy wycofywanie obciążeń związanych z odzyskiwaniem po awarii w centrum danych DR przez Migrowanie maszyn wirtualnych 2 000 do chmury. Oczekuje się, że w ciągu najbliższych pięciu lat zostanie wygenerowane szacowane oszczędności kosztów $25M USD.
    ![Koszty lokalne w porównaniu z kosztami platformy Azure, które pokazują zwrot z $25M USD w ciągu najbliższych pięciu lat](../../../_images/governance/calculator-small-to-medium-enterprise.png)
- Firma planuje zmienić sposób jej inwestycji, zmieniając rozmieszczenie zaliczonych wydatków kapitałowych jako kosztów operacyjnych w ramach tego rozwiązania. Ta zmiana zapewni większą kontrolę kosztów i umożliwi jej przyspieszenie innych planowanych wysiłków.

## <a name="next-steps"></a>Następne kroki

Firma opracowała zasady firmowe, aby kształtować implementację ładu. Zasady firmowe obejmują wiele decyzji technicznych.

> [!div class="nextstepaction"]
> [Zapoznaj się z początkowymi zasadami firmy](./initial-corporate-policy.md)
