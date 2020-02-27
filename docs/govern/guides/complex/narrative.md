---
title: 'Złożone przedsięwzięcie korporacyjne: Opis pomocniczy'
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby utworzyć przypadek użycia dla ładu w ramach złożonej podróży w chmurze w ramach kompleksowej organizacji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7c2cfcc76153e999b2ca9d50b63cf0a72cfb2c14
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "77706918"
---
# <a name="governance-guide-for-complex-enterprises-the-supporting-narrative"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Opis pomocniczy

Poniższe opisy stanowią przypadek użycia dla ładu, [podczas gdy złożona jest przepodróż w chmurze złożonego przedsiębiorstwa](./index.md). Przed przystąpieniem do zaleceń w przewodniku należy zrozumieć założenia i przyczynę, które są odzwierciedlone w tym opisie. Następnie można lepiej dostosować strategię ładu do swojej organizacji.

## <a name="back-story"></a>Historia z tyłu

Klienci potrzebują lepszego środowiska podczas korzystania z tej firmy. Bieżące środowisko spowodowało spadek rynku i doprowadziło do tego, że pracownicy zatrudniają dyrektora cyfrowego (CDO). Składnik CDO współpracuje z marketingiem i sprzedażą w celu przetworzenia transformacji cyfrowej, która zapewnia lepszą wydajność. Ponadto kilka jednostek roboczych niedawno zatrudnianych analityków danych do danych farmy i usprawnienia wielu czynności ręcznych dzięki uczeniu i prognozie. Obsługuje te działania, w których to możliwe. Istnieją jednak działania "w tle", które wykraczają poza konieczną kontrolę nadzoru i zabezpieczeń.

Organizacja IT również ma swoje wyzwania. Finanse planują dalsze obniżki w budżecie IT w ciągu najbliższych pięciu lat, co prowadzi do niepotrzebnych wydatków. Z drugiej strony, Rodo i inne wymagania dotyczące suwerenności danych wymuszają inwestowanie w zasoby w dodatkowych krajach do lokalizowania danych. Dwa z istniejących centrów danych są zaległe w przypadku odświeżania sprzętu, co powoduje dalsze problemy związane z zadowoleniem pracowników i klientów. Trzy więcej centrów danych wymaga odświeżenia sprzętu podczas wykonywania pięcioletniego planu. Dyrektor finansowy wypycha CIO, aby wziąć pod uwagę chmurę jako alternatywę dla tych centrów danych w celu zwolnienia wydatków inwestycyjnych.

CIO ma innowacyjne pomysły, które mogą pomóc firmie, ale jej zespoły są ograniczone do walki z pożarami i kontrolowaniem kosztów. W luncheon z elementem CDO i jednym z liderów jednostki biznesowej, Konwersacja migracji w chmurze wygenerowała zainteresowanie elementami równorzędnymi CIO. Trzy liderzy dążą do wspierania siebie nawzajem przy użyciu chmury, aby osiągnąć cele biznesowe i rozpoczęły etapy wdrażania w chmurze.

## <a name="business-characteristics"></a>Charakterystyka firmy

Firma ma następujący profil biznesowy:

- Sprzedaż i operacje obejmują wiele obszarów geograficznych z klientami globalnymi na wielu rynkach.
- Firma zwiększyła się w drodze pozyskiwania i działa w trzech jednostkach firmy w oparciu o docelową bazę klientów. Budżetowanie jest złożoną macierzą między jednostkami biznesowymi i funkcjami.
- Najpopularniejsze widoki biznesowe jako środki trwałe lub centrum kosztów.

## <a name="current-state"></a>Bieżący stan

Oto bieżący stan operacji w firmie i w chmurze:

- Działa ponad 20 prywatnych centrów danych na całym świecie.
- Ze względu na rozwój organiczny i wiele lokalizacje geograficzne, istnieje kilka zespołów IT, które mają unikatowe wymagania dotyczące suwerenności danych i zgodności, które mają wpływ na jedną jednostkę biznesową działającą w określonej lokalizacji geograficznej.
- Każde centrum danych jest połączone z serią regionalnych linii dzierżawionych, tworząc luźno przyłączoną globalną sieć WAN.
- Wprowadzono chmurę przez Migrowanie wszystkich kont e-mail użytkowników końcowych do pakietu Office 365. Ta migracja została ukończona ponad sześć miesięcy temu. Od tej pory tylko kilka zasobów IT zostało wdrożonych w chmurze.
- Podstawowy zespół programistyczny składnika CDO działa w ramach tworzenia i testowania możliwości w celu uzyskania informacji o możliwościach natywnych w chmurze.
- Jedna jednostka biznesowa eksperymentuje z danymi Big Data w chmurze. Zespół usługi BI w tym zakresie bierze udział w tym wysiłku.
- Istniejące zasady ładu IT określają, że dane osobowe klienta i dane finansowe muszą być hostowane przez zasoby należące bezpośrednio do firmy. Te zasady blokują wdrażanie w chmurze dla wszystkich aplikacji o kluczowym znaczeniu lub chronionych danych.
- Inwestycje IT są kontrolowane w dużym stopniu według kosztów kapitałowych. Te inwestycje są planowane rocznie i często obejmują plany dla trwającej konserwacji, a także ustanowione cykle odświeżania od trzech do pięciu lat w zależności od centrum danych.
- Większość inwestycji w technologię, które nie są wyrównane do planu rocznego, są rozwiązywane przez wysiłki IT w tle. Te działania są zwykle zarządzane przez jednostki biznesowe i finansowane za pośrednictwem kosztów operacyjnych jednostki biznesowej.

## <a name="future-state"></a>Przyszły stan

Następujące zmiany są przewidywane w ciągu następnych kilku lat:

- CIO to wiodący nakład na unowocześnienie zasad związanych z danymi osobistymi i finansowymi w celu wspierania przyszłych celów. Dwaj członkowie zespołu nadzoru IT mają wgląd w ten nakład pracy.
- CIO chce korzystać z migracji w chmurze jako funkcji wymuszania w celu poprawy spójności i stabilności między jednostkami biznesowymi i lokalizacje geograficzne. Natomiast w przyszłości należy przestrzegać wszelkich zewnętrznych wymagań dotyczących zgodności, które wymagają odchylenia od standardowych podejścia do określonych zespołów IT.
- Jeśli wczesne eksperymenty w aplikacji dev i BI pokażą wiodące wskaźniki sukcesu, chcą, aby wystawić w ciągu najbliższych 24 miesięcy rozwiązania produkcyjne o małych skali.
- CIO i dyrektor finansowy posiadają architekta i wiceprzewodniczący infrastruktury do tworzenia analiz kosztów i studiów wykonalności. Te wysiłki określają, czy firma może i powinna przenieść zasoby 5 000 do chmury w ciągu następnych 36 miesięcy. Pomyślna migracja zezwoli CIO na wyeliminowanie dwóch centrów danych, co zmniejsza koszty za pośrednictwem $100 mln USD w ramach planu pięciu lat. Jeśli trzy do czterech centrów danych mogą mieć podobne wyniki, budżet zostanie przywrócony do czerni, dzięki czemu budżet CIO będzie obsługiwał bardziej innowacyjne inicjatywy.
    ![koszty lokalne w porównaniu z kosztami platformy Azure, które pokazują powrót z $100 mln USD w ciągu najbliższych pięciu lat](../../../_images/govern/calculator-enterprise.png)
- Wraz z tym obniżeniem kosztów firma planuje zmienić zarządzanie niektórymi inwestycjami IT, zmieniając rozmieszczenie zaliczonych wydatków inwestycyjnych jako kosztów operacyjnych w ramach tego kosztu. Ta zmiana zapewni większą kontrolę kosztów, której można użyć do przyspieszenia innych planowanych wysiłków.

## <a name="next-steps"></a>Następne kroki

Firma opracowała zasady firmowe, aby kształtować implementację ładu. Zasady firmowe obejmują wiele decyzji technicznych.

> [!div class="nextstepaction"]
> [Zapoznaj się z początkowymi zasadami firmy](./initial-corporate-policy.md)
