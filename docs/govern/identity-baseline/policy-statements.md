---
title: Przykładowe instrukcje zasad linii bazowej tożsamości
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby uzyskać przykładowe instrukcje zasad linii bazowej tożsamości, które mogą pomóc w zaprojektowaniu instrukcji zasad.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: c3543299d323c8be6bf7ee88d6e9205c307e24f9
ms.sourcegitcommit: 7d3fc1e407cd18c4fc7c4964a77885907a9b85c0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/16/2020
ms.locfileid: "80997441"
---
# <a name="identity-baseline-sample-policy-statements"></a>Przykładowe instrukcje zasad linii bazowej tożsamości

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te instrukcje powinny dostarczyć zwięzłe podsumowanie zagrożeń i plany postępowania z nimi. Każda definicja instrukcji powinna zawierać następujące informacje:

- **Ryzyko techniczne:** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad:** Jasne wyjaśnienie wymagań zasad.
- **Opcje projektowania:** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki, które mogą być używane przez zespoły IT i deweloperów podczas implementowania zasad.

Poniższe przykładowe instrukcje dotyczące zasad dotyczą typowych zagrożeń związanych z tożsamościami. Te instrukcje są przykładami, które można przywołać podczas sporządzania projektów instrukcji zasad w celu rozwiązania potrzeb organizacji. Te przykłady nie są przeznaczone do obsługi skryptów i mogą być dostępne różne opcje dotyczące ponoszenia określonych zagrożeń. Ścisła współpraca z firmowymi i zespołami IT w celu zidentyfikowania najlepszych zasad dla unikatowego zestawu zagrożeń.

## <a name="lack-of-access-controls"></a>Brak kontroli dostępu

**Ryzyko techniczne:** Ustawienia kontroli dostępu niewystarczające lub ad hoc mogą spowodować ryzyko nieautoryzowanego dostępu do zasobów poufnych lub o znaczeniu krytycznym.

**Instrukcja zasad:** Wszystkie zasoby wdrożone w chmurze powinny być kontrolowane przy użyciu tożsamości i ról zatwierdzonych przez bieżące zasady zarządzania.

**Potencjalne opcje projektowania:** [Azure Active Directory dostęp warunkowy](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) jest domyślnym mechanizmem kontroli dostępu na platformie Azure.

## <a name="overprovisioned-access"></a>Dostęp z nadmierną obsługą administracyjną

**Ryzyko techniczne:** Użytkownicy i grupy z kontrolą nad zasobami poza ich obszarem odpowiedzialności mogą spowodować nieautoryzowane modyfikacje prowadzące do awarii lub luk w zabezpieczeniach.

**Instrukcja zasad:** Następujące zasady zostaną zaimplementowane:

- Model dostępu o najniższych uprawnieniach zostanie zastosowany do wszystkich zasobów związanych z aplikacjami o kluczowym znaczeniu lub chronionych danych.
- Podwyższone uprawnienia powinny być wyjątkiem, a wszystkie takie wyjątki muszą być rejestrowane przez zespół nadzorujący chmurę. Wyjątki będą regularnie poddawane inspekcji.

**Potencjalne opcje projektu:** Zapoznaj się z [najlepszymi rozwiązaniami w zakresie zarządzania tożsamościami platformy Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-best-practices) , aby wdrożyć strategię kontroli dostępu opartej na ROLACH (RBAC), która ogranicza dostęp w zależności od [potrzeb znajomości](https://wikipedia.org/wiki/Need_to_know) zasad [zabezpieczeń i najniższych uprawnień](https://wikipedia.org/wiki/Principle_of_least_privilege) .

## <a name="lack-of-shared-management-accounts-between-on-premises-and-the-cloud"></a>Brak współużytkowanych kont zarządzania między środowiskiem lokalnym i chmurą

**Ryzyko techniczne:** Zarządzanie IT lub pracownicy administracyjni z kontami w Active Directory lokalnymi mogą nie mieć wystarczających uprawnień dostępu do zasobów w chmurze, które mogą nie być w stanie skutecznie rozwiązywać problemów z działaniem lub zabezpieczeniami.

**Instrukcja zasad:** Wszystkie grupy w lokalnej infrastrukturze Active Directory, które mają podwyższony poziom uprawnień, powinny być mapowane do zatwierdzonej roli RBAC.

**Potencjalne opcje projektu:** Zaimplementuj rozwiązanie do obsługi tożsamości hybrydowej między Azure Active Directory opartymi na chmurze i lokalnymi Active Directory i Dodaj wymagane grupy lokalne do ról RBAC niezbędnych do wykonania ich pracy.

## <a name="weak-authentication-mechanisms"></a>Słabe mechanizmy uwierzytelniania

**Ryzyko techniczne:** Systemy zarządzania tożsamościami z niewystarczająco bezpiecznymi metodami uwierzytelniania użytkowników, takimi jak podstawowe kombinacje użytkownika/hasła, mogą prowadzić do naruszenia lub zaatakowana haseł, co zapewnia duże ryzyko nieautoryzowanego dostępu do systemów w chmurze.

**Instrukcja zasad:** Wszystkie konta są wymagane do logowania się do zabezpieczonych zasobów przy użyciu metody uwierzytelniania wieloskładnikowego.

**Potencjalne opcje projektu:** W przypadku Azure Active Directory implementowanie [usługi Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) w ramach procesu autoryzacji użytkownika.

## <a name="isolated-identity-providers"></a>Izolowani dostawcy tożsamości

**Ryzyko techniczne:** Niezgodni dostawcy tożsamości mogą spowodować brak możliwości udostępnienia zasobów lub usług klientom lub innym partnerom biznesowym.

**Instrukcja zasad:** Wdrożenie wszelkich aplikacji, które wymagają uwierzytelnienia klienta, musi używać zatwierdzonego dostawcy tożsamości, który jest zgodny z podstawowym dostawcą tożsamości dla użytkowników wewnętrznych.

**Potencjalne opcje projektu:** Zaimplementuj [Federacji z Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) między wewnętrznymi i dostawcami tożsamości klienta lub Użyj [Azure Active Directory B2B](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

## <a name="identity-reviews"></a>Przeglądy tożsamości

**Ryzyko techniczne:** W miarę wprowadzania zmian w czasie, dodanie nowych wdrożeń w chmurze lub innych problemów związanych z bezpieczeństwem może zwiększyć ryzyko nieautoryzowanego dostępu do zabezpieczonych zasobów.

**Instrukcja zasad:** Procesy nadzoru chmur muszą obejmować kwartalne przeglądy z zespołami zarządzania tożsamościami w celu identyfikowania złośliwych aktorów lub wzorców użytkowania, które powinny być blokowane przez konfigurację zasobów w chmurze.

**Potencjalne opcje projektu:** Ustanów kwartalne spotkanie przeglądowe dotyczące zabezpieczeń, które obejmuje członków zespołu nadzoru i personel IT odpowiedzialny za zarządzanie usługami tożsamości. Zapoznaj się z istniejącymi danymi i metrykami zabezpieczeń, aby ustalić luki w bieżącym zarządzaniu tożsamościami i narzędziach, a także zasady aktualizacji, aby skorygować wszelkie nowe zagrożenia.

## <a name="next-steps"></a>Następne kroki

Skorzystaj z przykładów przedstawionych w tym artykule jako punktu wyjścia do tworzenia zasad w celu rozwiązywania określonych zagrożeń firmy, które są dostosowane do planów wdrażania w chmurze.

Aby rozpocząć tworzenie własnych niestandardowych instrukcji zasad związanych z punktem odniesienia tożsamości, Pobierz [szablon linii bazowej tożsamości](./template.md).

Aby przyspieszyć wdrażanie tego dyscypliny, wybierz [Przewodnik dotyczący ładu](../guides/index.md) z możliwością działania, który najlepiej odpowiada Twojemu środowisku. Następnie zmodyfikuj projekt, aby uwzględnić określone decyzje dotyczące zasad firmowych.

Tworzenie na podstawie ryzyka i tolerancji, ustanowienie procesu zarządzania zasadami odniesienia tożsamości i ich komunikacji.

> [!div class="nextstepaction"]
> [Ustanawianie procesów zgodności z zasadami](./compliance-processes.md)
