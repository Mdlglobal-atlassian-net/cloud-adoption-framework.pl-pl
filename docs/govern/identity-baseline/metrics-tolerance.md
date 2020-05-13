---
title: Metryki i wskaźniki tolerancji ryzyka w dyscyplinie linii bazowej tożsamości.
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak określić tolerancję ryzyka biznesowego związanego z dyscypliną linii bazowej tożsamości.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: bbe36f12e6331a85f024af1835b66c30e35bf430
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83218649"
---
# <a name="identity-baseline-metrics-indicators-and-risk-tolerance"></a>Metryki linii bazowej tożsamości, wskaźniki i tolerancja ryzyka

Dowiedz się więcej na temat określania wielkości tolerancji ryzyka biznesowego związanego z dyscypliną linii bazowej tożsamości. Definiowanie metryk i wskaźników pomaga utworzyć przypadek biznesowy do inwestowania w okres zapadalności tej dyscypliny.

## <a name="metrics"></a>Metryki

Zarządzanie tożsamościami koncentruje się na identyfikowaniu, uwierzytelnianiu i autoryzacji osób, grup użytkowników lub zautomatyzowanych procesów oraz zapewnianiu im odpowiedniego dostępu do zasobów we wdrożeniach w chmurze. W ramach analizy ryzyka warto zebrać dane związane z usługami tożsamości, aby określić, jakie ryzyko wiąże się z ryzykiem oraz jak ważne inwestycje w dyscypliny linii bazowej Twojej tożsamości dotyczą planowanych wdrożeń w chmurze.

Poniżej przedstawiono przykłady przydatnych metryk, które należy zebrać, aby pomóc w ocenie tolerancji ryzyka w ramach dyscypliny linii bazowej tożsamości:

- **Rozmiar systemów tożsamości.** Łączna liczba użytkowników, grup lub innych obiektów zarządzanych przez systemy tożsamości.
- **Ogólny rozmiar infrastruktury usług katalogowych.** Liczba lasów katalogów, domen i dzierżawców używanych w organizacji.
- **Zależność od starszych lub lokalnych mechanizmów uwierzytelniania.** Liczba obciążeń, które są zależne od starszych lub wieloskładnikowych mechanizmów usługi uwierzytelniania.
- **Zakres usług katalogowych wdrożonych w chmurze.** Liczba lasów katalogów, domen i dzierżawców, które zostały wdrożone w chmurze.
- **Active Directory serwerów wdrożonych w chmurze.** Liczba serwerów Active Directory wdrożonych w chmurze.
- **Jednostki organizacyjne wdrożone w chmurze.** Liczba Active Directory jednostek organizacyjnych (OU) wdrożonych w chmurze.
- **Zakres Federacji.** Liczba systemów zarządzania tożsamościami federacyjnych z systemami organizacji.
- **Użytkownicy z podwyższonym poziomem uprawnień.** Liczba kont użytkowników z podwyższonym poziomem dostępu do zasobów lub narzędzi do zarządzania.
- **Użycie kontroli dostępu opartej na rolach.** Liczba subskrypcji, grup zasobów lub poszczególnych zasobów, które nie są zarządzane przez funkcję kontroli dostępu opartej na rolach (RBAC) za pośrednictwem grup.
- **Oświadczenia uwierzytelniania.** Liczba prób uwierzytelnienia użytkownika zakończonych powodzeniem i niepowodzeniem.
- **Oświadczenia autoryzacji.** Liczba pomyślnych i nieudanych prób uzyskania dostępu do zasobów przez użytkowników.
- **Naruszone konta.** Liczba kont użytkowników, których zabezpieczenia zostały naruszone.

## <a name="risk-tolerance-indicators"></a>Wskaźniki tolerancji ryzyka

Ryzyko związane z linią bazową tożsamości jest w dużym stopniu związane z złożonością infrastruktury tożsamości w organizacji. Jeśli wszyscy użytkownicy i grupy są zarządzani przy użyciu jednego katalogu lub macierzystego dostawcy tożsamości przy użyciu minimalnej integracji z innymi usługami, poziom ryzyka będzie prawdopodobnie niewielki. Jednak w miarę wzrostu potrzeb firmy systemy zarządzania tożsamościami mogą wymagać obsługi bardziej złożonych scenariuszy, takich jak wiele katalogów do obsługi wewnętrznej organizacji lub Federacji z zewnętrznymi dostawcami tożsamości. Ponieważ te systemy stają się bardziej skomplikowane, zwiększa się ryzyko.

We wczesnych etapach wdrażania chmury Pracuj z zespołem ds. zabezpieczeń IT i zainteresowanymi stronami biznesowymi, aby identyfikować [zagrożenia biznesowe](./business-risks.md) związane z tożsamością, a następnie określić akceptowalny poziom odniesienia dla tolerancji ryzyka związanego z tożsamościami. W tej części struktury wdrażania w chmurze przedstawiono przykłady, ale szczegóły dotyczące zagrożeń i linii bazowych dla firmy lub wdrożeń mogą się różnić.

Po utworzeniu planu bazowego należy ustanowić minimalne wzorce reprezentujące nieakceptowalny wzrost w zidentyfikowanych zagrożeniach. Te progi działają jako wyzwalacze, gdy konieczne jest podjęcie działań w celu rozwiązania tych zagrożeń. Poniżej przedstawiono kilka przykładów metryk związanych z tożsamościami, takich jak te omówione powyżej, mogą uzasadniać zwiększenie inwestycji w dyscypliny linii bazowej tożsamości.

- **Wyzwalacz numeru konta użytkownika.** Firma z więcej niż _x_ użytkownikami, grupami lub innymi obiektami zarządzanymi w systemach tożsamości może skorzystać z inwestycji w dyscypliny linii bazowej tożsamości, aby zapewnić wydajne zarządzanie na wielu kontach.
- **Lokalny wyzwalacz zależności tożsamości.** Firma planuje migrację obciążeń do chmury wymagającej starszych możliwości uwierzytelniania lub uwierzytelniania wieloskładnikowego innej firmy, aby zmniejszyć ryzyko związane z refaktoryzacją lub dodatkowym wdrożeniem infrastruktury chmurowej.
- **Wyzwalacz złożoności usług katalogowych.** Firma utrzymująca więcej niż _x_ numerów of_ poszczególne lasy, domeny i dzierżawy katalogu powinny inwestować w dyscyplinę bazową tożsamości, aby zmniejszyć ryzyko związane z zarządzaniem kontami oraz problemy z wydajnością związane z wieloma poświadczeniami użytkowników rozmieszczonych w wielu systemach.
- **Wyzwalacz usług katalogowych hostowanych w chmurze.** Firma zarządza maszynami wirtualnymi _x_ Active Directory Server (VM) hostowanymi w chmurze lub mającymi _x_ jednostki organizacyjne (OU) zarządzane na tych serwerach w chmurze, może korzystać z inwestycji w dyscypliny podstawowej tożsamości w celu optymalizacji integracji z dowolnymi lokalnymi lub innymi zewnętrznymi usługami tożsamości.
- **Wyzwalacz Federacji.** Firma implementująca federacji tożsamości z _x_ zewnętrznymi systemami zarządzania tożsamościami może korzystać z inwestycji w dyscypliny linii bazowej tożsamości, aby zapewnić spójne zasady organizacyjne w obrębie federacyjnych elementów członkowskich.
- **Wyzwalacz dostępu z podwyższonym poziomem uprawnień.** Firma mająca więcej niż _x%_ użytkowników z podwyższonym poziomem uprawnień do narzędzi do zarządzania i zasobów powinna rozważyć zainwestowanie w dyscypliny linii bazowej tożsamości, aby zminimalizować ryzyko przypadkowego nadmiernego zainicjowania dostępu do użytkowników.
- **Wyzwalacz RBAC.** Firma o wartości poniżej _x%_ zasobów przy użyciu metod kontroli dostępu opartej na rolach powinna rozważyć inwestowanie w dyscypliny linii bazowej tożsamości, aby zidentyfikować zoptymalizowane sposoby przypisywania dostępu użytkowników do zasobów.
- **Wyzwalacz błędu uwierzytelniania.** Firma, w której błędy uwierzytelniania reprezentują ponad _x%_ prób, powinna inwestować w dyscyplinę bazową tożsamości, aby upewnić się, że metody uwierzytelniania nie są objęte atakiem zewnętrznym i że użytkownicy mogą prawidłowo się uwierzytelniać.
- **Wyzwalacz błędu autoryzacji.** Firma, w której próby dostępu są odrzucane ponad _x%_ czasu, powinien inwestować w dyscyplinę bazową tożsamości w celu ulepszania aplikacji i aktualizowania kontroli dostępu, a następnie identyfikować potencjalnie złośliwe próby dostępu.
- **Naruszony wyzwalacz konta.** Firma z ponad 1 złamanym kontem powinna zainwestować w dyscyplinę bazową tożsamości, aby zwiększyć siłę i bezpieczeństwo mechanizmów uwierzytelniania oraz poprawić mechanizmy korygowania zagrożeń związanych z naruszonymi kontami.

Dokładne metryki i wyzwalacze służące do oceny tolerancji ryzyka i poziom inwestycji w dyscyplinę bazową tożsamości będą specyficzne dla organizacji, ale powyższe przykłady powinny służyć jako przydatny dla dyskusji w zespole nadzoru chmurowego.

## <a name="next-steps"></a>Następne kroki

[Szablon dyscypliny linii bazowej tożsamości](./template.md) służy do dokumentowania metryk i wskaźników tolerancji, które są wyrównane do bieżącego planu wdrażania chmury.

Zapoznaj się z przykładowymi zasadami odniesienia tożsamości jako punktem wyjścia do opracowania własnych zasad w celu rozwiązania określonych zagrożeń dla firmy, które są dostosowane do planów wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Przeglądanie przykładowych zasad](./policy-statements.md)
