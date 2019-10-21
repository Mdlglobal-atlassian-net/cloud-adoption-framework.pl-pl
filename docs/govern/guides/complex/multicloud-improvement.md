---
title: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: poprawa chmury'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: poprawa chmury'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4279f088dd985b26c87d28a580b8351d45d9384e
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72547656"
---
# <a name="governance-guide-for-complex-enterprises-multicloud-improvement"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: poprawa chmury

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Firma Microsoft uznaje, że klienci mogą zastosować wiele chmur do określonych celów. Fikcyjna firma w tym przewodniku nie jest wyjątkiem. Równolegle ze swoją podróżą w zakresie wdrażania platformy Azure, sukces biznesowy doprowadził do nabycia niewielkiej, ale dodatkowej firmy. Firma pracuje nad wszystkimi swoimi operacjami IT na innym dostawcy chmury.

W tym artykule opisano, jak zmieniają się zmiany podczas integrowania nowej organizacji. Na potrzeby postanowień przyjęto, że firma Microsoft zakończyła wszystkie iteracje ładu opisane w tym przewodniku ładu.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

W poprzedniej fazie tego rozpisania firma zaczęła wdrożyć kontrolę kosztów i monitorowanie kosztów, ponieważ wydatki w chmurze staną się częścią zwykłych wydatków operacyjnych firmy.

Od tej pory zmieniono pewne zmiany, które wpłyną na nadzór:

- Tożsamość jest kontrolowana przez lokalne wystąpienie Active Directory. Tożsamość hybrydowa jest ułatwiona poprzez replikację do Azure Active Directory.
- Operacje IT lub operacje w chmurze są w dużej mierze zarządzane przez Azure Monitor i powiązane możliwości automatyzacji.
- Odzyskiwanie po awarii i ciągłość biznesowa (DRBC) jest kontrolowane przez wystąpienia magazynu Azure.
- Azure Security Center służy do monitorowania naruszeń zabezpieczeń i ataków.
- Azure Security Center i Azure Monitor są używane do monitorowania zarządzania chmurą.
- Plany platformy Azure, Azure Policy i grupy zarządzania są używane do automatyzowania zgodności z zasadami.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Celem jest zintegrowanie firmy pozyskiwania z istniejącymi operacjami wszędzie tam, gdzie to możliwe.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Koszt pozyskiwania przez firmę:** Nabycie nowej firmy szacuje się na zyskowność w ciągu około pięciu lat. Ze względu na powolnej częstotliwości powrotu tablica chce kontrolować koszty pozyskiwania, tak jak to możliwe. Istnieje ryzyko związane z kontrolą kosztów i integracją techniczną ze sobą.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

- Istnieje ryzyko związane z migracją w chmurze, które produkują dodatkowe koszty pozyskiwania.
- Istnieje również ryzyko, że nowe środowisko nie jest prawidłowo regulowane lub nie spowodowało naruszeń zasad.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika.

- Wszystkie zasoby w chmurze dodatkowej muszą być monitorowane za pomocą istniejących narzędzi do zarządzania operacyjnego i monitorowania zabezpieczeń.
- Wszystkie jednostki organizacyjne muszą być zintegrowane z istniejącym dostawcą tożsamości.
- Podstawowy dostawca tożsamości powinien zarządzać uwierzytelnianiem zasobów w chmurze pomocniczej.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

W tej części artykułu Ulepszono projekt ładu MVP w celu uwzględnienia nowych zasad platformy Azure i implementacji Azure Cost Management. Te dwie zmiany w projekcie zostaną spełnione w ramach nowych instrukcji dotyczących zasad firmowych.

1. Połącz sieci. Wykonywane przez sieci i zabezpieczenia INFORMATYCZNe, obsługiwane przez zarządzanie.
    1. Dodanie połączenia od dostawcy MPLS lub dzierżawy do nowej chmury spowoduje integrację sieci. Dodanie tabel routingu i konfiguracji zapory umożliwi sterowanie dostępem i ruchem między środowiskami.
2. Konsolidowanie dostawców tożsamości. W zależności od obciążeń obsługiwanych w chmurze dodatkowej istnieje wiele opcji konsolidacji dostawców tożsamości. Poniżej przedstawiono kilka przykładów:
    1. W przypadku aplikacji, które uwierzytelniają się za pomocą protokołu OAuth 2, użytkownicy w Active Directory w chmurze pomocniczej mogą być po prostu zreplikowane do istniejącej dzierżawy usługi Azure AD.
    2. W drugiej skrajnym federacji między dwoma lokalnymi dostawcami tożsamości wszyscy użytkownicy z nowych domen Active Directory mogą być replikowane na platformę Azure.
3. Dodaj zasoby do Azure Site Recovery.
    1. Azure Site Recovery została skompilowana jako narzędzie hybrydowe i wielochmurowe od początku.
    2. Maszyny wirtualne w chmurze pomocniczej mogą być chronione za pomocą tych samych Azure Site Recoveryych procesów, które są używane do ochrony zasobów lokalnych.
4. Dodaj zasoby do Azure Cost Management.
    1. Azure Cost Management zostało skompilowane jako narzędzie wielochmurowe od początku.
    2. Maszyny wirtualne w chmurze pomocniczej mogą być zgodne z Azure Cost Managementami dla niektórych dostawców chmury. Mogą obowiązywać dodatkowe koszty.
5. Dodaj zasoby do Azure Monitor.
    1. Azure Monitor zostało skompilowane jako narzędzie chmury hybrydowej od początku.
    2. Maszyny wirtualne w chmurze pomocniczej mogą być zgodne z Azure Monitor agentami, co umożliwia ich uwzględnienie w Azure Monitor monitorowania operacyjnego.
6. Narzędzia wymuszania ładu.
    1. Wymuszanie ładu jest specyficzne dla chmury.
    2. Zasady firmowe ustanowione w przewodniku ładu nie są specyficzne dla chmury. Chociaż implementacja może się różnić w zależności od chmury, można zastosować instrukcje zasad do dostawcy pomocniczego.

Wdrożenie wielochmurowe powinno być zawarte w miejscu, w którym jest wymagane na podstawie wymagań technicznych lub określonych wymagań firmy. W miarę rozwoju rozwiązania do obsługi rozwiązań w chmurze, w związku z czym złożoność i zagrożenia bezpieczeństwa.

## <a name="next-steps"></a>Następne kroki

W wielu dużych przedsiębiorstwach może być blokowanych przez pięć dyscyplin zarządzania chmurą. W następnym artykule zawarto kilka dodatkowych pomysłów dotyczących tworzenia zespołu sportowego, aby pomóc w zapewnieniu długoterminowej sukcesów w chmurze.

> [!div class="nextstepaction"]
> [Wiele warstw ładu](./multiple-layers-of-governance.md)
