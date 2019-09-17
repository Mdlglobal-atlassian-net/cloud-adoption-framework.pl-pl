---
title: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny linii bazowej tożsamości'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny linii bazowej tożsamości'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/06/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0c17f9043dd88f401b07293a6b93e50ccefe0137
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028840"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-identity-baseline-discipline"></a>Przewodnik dotyczący zarządzania złożonymi przedsiębiorstwami: Ulepszanie dyscypliny linii bazowej tożsamości

Ten artykuł postępuje zgodnie z opisami, dodając kontrolki bazowe tożsamości do programu ładu MVP.

## <a name="advancing-the-narrative"></a>Przesuwanie narracji

Uzasadnienie biznesowe migracji dwóch centrów danych zostało zatwierdzone przez dyrektora finansowego. Podczas analizy wykonalności technicznej wykryto kilka przeszkody:

- Chronione dane i aplikacje o krytycznym znaczeniu reprezentują 25% obciążeń w dwóch centrach danych. Nie można wyeliminować ani do momentu, gdy bieżące zasady zarządzania dotyczą wrażliwych danych osobowych i aplikacji o znaczeniu krytycznym.
- 7% zasobów w tych centrach danych nie jest zgodnych z chmurą. Zostaną one przeniesione do innego centrum danych przed zakończeniem kontraktu centrum danych.
- 15% zasobów w centrum danych (750 maszyn wirtualnych) ma zależność od starszego uwierzytelniania lub usługi uwierzytelniania wieloskładnikowego innej firmy.
- Połączenie sieci VPN, które łączy istniejące centra danych i platformę Azure, nie oferuje wystarczającej szybkości transmisji lub opóźnieniu dla migracji ilości zasobów w ramach dwuletniego osi czasu, aby wycofać centrum danych.

Pierwsze dwa przeszkody są zarządzane równolegle. W tym artykule opisano rozdzielczość trzeciej i czwartej przeszkody.

### <a name="expanding-the-cloud-governance-team"></a>Rozwijanie zespołu ładu w chmurze

Zespół ds. zarządzania chmurą. Mając na uwadze potrzebę dodatkowej pomocy w zakresie zarządzania tożsamościami, administrator systemów z zespołu linii bazowej tożsamości uczestniczy w tygodniowym spotkaniu, aby zapewnić, że istniejący członkowie zespołu wiedzą o zmianach.

### <a name="changes-in-the-current-state"></a>Zmiany w bieżącym stanie

Zespół IT ma zatwierdzenie do przeniesienia do planu CIO i dyrektora finansowego w celu wycofania dwóch centrów danych. Należy jednak pamiętać, że 750 (15%) zasoby w tych centrach danych będą musiały zostać przeniesione poza chmurą.

### <a name="incrementally-improve-the-future-state"></a>Przyrostowe ulepszanie stanu w przyszłości

Nowe przyszłe plany stanu wymagają bardziej niezawodnego rozwiązania odniesienia tożsamości do migrowania maszyn wirtualnych 750 ze starszymi wymaganiami uwierzytelniania. Poza tymi dwoma centrami danych ten test powinien wpływać na podobne wartości procentowe zasobów w innych centrach danych.

Przyszły stan teraz wymaga również połączenia od dostawcy chmury do rozwiązania MPLS/dzierżawionego przez firmę.

Zmiany bieżącego i przyszłego stanu ujawniają nowe zagrożenia, które będą wymagały nowych instrukcji zasad.

## <a name="changes-in-tangible-risks"></a>Zmiany w materialnym ryzyku

**Zakłócenia biznesowe podczas migracji.** Migracja do chmury tworzy kontrolowane, powiązane z czasem ryzyko, które może być zarządzane. Przeniesienie sprzętu z przedawnieniem do innej części świata jest znacznie bardziej ryzykowne. Aby uniknąć przerw w działaniu działalności biznesowej, wymagana jest strategia zaradcza.

**Istniejące zależności tożsamości.** Zależności dotyczące istniejących usług uwierzytelniania i tożsamości mogą opóźniać lub uniemożliwiać migrację niektórych obciążeń do chmury. Niepowodzenie zwrócenia dwóch centrów danych w czasie spowoduje naliczenie milionów dolarów w opłatach za dzierżawę centrum danych.

To ryzyko biznesowe można rozszerzyć na kilka zagrożeń technicznych:

- Starsza wersja uwierzytelniania może nie być dostępna w chmurze, ograniczając wdrażanie niektórych aplikacji.
- Bieżące rozwiązanie do uwierzytelniania wieloskładnikowego innej firmy może nie być dostępne w chmurze, ograniczając wdrożenie niektórych aplikacji.
- Przechodzenie lub przeniesienie może spowodować awarię lub dodanie kosztów.
- Szybkość i stabilność sieci VPN może utrudniać migrację.
- Ruch wprowadzający chmurę może powodować problemy z zabezpieczeniami w innych częściach sieci globalnej.

## <a name="incremental-improvement-of-the-policy-statements"></a>Przyrostowe ulepszanie instrukcji zasad

Poniższe zmiany zasad pomogą skorygować nowe zagrożenia i implementację przewodnika.

- Wybrany dostawca chmury musi oferować środki uwierzytelniania za pośrednictwem starszych metod.
- Wybrany dostawca usług w chmurze musi oferować metodę uwierzytelniania przy użyciu bieżącego rozwiązania do uwierzytelniania wieloskładnikowego innej firmy.
- Należy nawiązać połączenie prywatne między dostawcą chmury i dostawcą odpływ firmy, łącząc dostawcę chmury z globalną siecią centrów danych.
- Dopóki nie zostaną spełnione wystarczające wymagania dotyczące zabezpieczeń, żaden przychodzący ruch publiczny nie może uzyskać dostępu do zasobów firmy hostowanych w chmurze. Wszystkie porty są blokowane z dowolnego źródła poza globalną siecią WAN.

## <a name="incremental-improvement-of-the-best-practices"></a>Przyrostowe ulepszanie najlepszych rozwiązań

Projekt ładu MVP zmienia się w celu uwzględnienia nowych zasad platformy Azure i implementacji Active Directory na maszynie wirtualnej. Razem te dwa zmiany projektu spełniają nowe instrukcje dotyczące zasad firmowych.

Oto nowe najlepsze rozwiązania:

- **Bezpieczny hybrydowy plan sieci wirtualnej:** Lokalna Strona sieci hybrydowej powinna być skonfigurowana w taki sposób, aby zezwalała na komunikację między następującym rozwiązaniem i lokalnymi serwerami Active Directory. To najlepsze rozwiązanie wymaga obwodu DMZ, aby umożliwić Active Directory Domain Services między granicami sieci.
- **Szablony Azure Resource Manager:**
    1. Zdefiniuj sieciowej grupy zabezpieczeń do blokowania ruchu zewnętrznego i zezwalania na ruch wewnętrzny.
    1. Wdróż dwie Active Directory maszyny wirtualne w parze z równoważeniem obciążenia na podstawie złota obrazu. Przy pierwszym rozruchu ten obraz uruchamia skrypt programu PowerShell w celu przyłączenia do domeny i zarejestrowania się w usługach domenowych. Aby uzyskać więcej informacji, zobacz [rozszerzając Active Directory Domain Services (AD DS) na platformę Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain).
- Azure Policy: Zastosuj sieciowej grupy zabezpieczeń do wszystkich zasobów.
- Plan platformy Azure:
    1. Utwórz plan o nazwie `active-directory-virtual-machines`.
    1. Dodaj do planu wszystkie Active Directory szablony i zasady.
    1. Opublikuj plan w odpowiedniej grupie zarządzania.
    1. Zastosuj plan do dowolnej subskrypcji wymagającej starszej wersji usługi uwierzytelniania wieloskładnikowego lub innej firmy.
    1. Wystąpienie Active Directory uruchomione na platformie Azure może być teraz używane jako rozszerzenie lokalnego Active Directory rozwiązanie, które umożliwia integrację z istniejącym narzędziem uwierzytelniania wieloskładnikowego i zapewnianie uwierzytelniania opartego na oświadczeniach. istniejące Active Directory funkcje.

## <a name="conclusion"></a>Wniosek

Dodanie tych zmian do ładu SPECJALISTy pomaga skorygować wiele zagrożeń w tym artykule, co pozwoli każdemu zespołowi rozwiązań w chmurze na szybkie przechodzenie do Roadblock.

## <a name="next-steps"></a>Następne kroki

Gdy wdrożenie chmury będzie kontynuowane i zapewnia dodatkową wartość biznesową, zagrożenia i potrzeby ładu chmury również zostaną zmienione. Poniżej przedstawiono kilka zmian, które mogą wystąpić. W przypadku tej fikcyjnej firmy następnym wyzwalaczem jest dołączenie chronionych danych do planu wdrażania chmury. Ta zmiana wymaga dodatkowych kontroli zabezpieczeń.

> [!div class="nextstepaction"]
> [Ulepszanie dyscypliny linii bazowej zabezpieczeń](./security-baseline-improvement.md)
