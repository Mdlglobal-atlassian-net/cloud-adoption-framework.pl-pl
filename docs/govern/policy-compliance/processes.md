---
title: Ustalanie procesów zapewniania zgodności zasad
description: Utwórz strategię i procesy, aby upewnić się, że wdrożenie w chmurze pozostaje zgodne z wymaganiami dotyczącymi zasad. 
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b7bdcd96786a232ef810794cf93546275a9603b0
ms.sourcegitcommit: afe10f97fc0e0402a881fdfa55dadebd3aca75ab
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80430813"
---
<!-- markdownlint-disable MD026 -->

# <a name="establish-policy-adherence-processes"></a>Ustalanie procesów zapewniania zgodności zasad

Po ustaleniu zasad dotyczących chmury i opracowaniu projektu przewodnika projektowego należy utworzyć strategię w celu zapewnienia zgodności wdrożenia w chmurze z wymaganiami dotyczącymi zasad. Ta strategia będzie musiała obejmować bieżące procesy przeglądu i komunikacji zespołu nadzoru w chmurze, ustanawiać kryteria dotyczące sytuacji, w których naruszenia zasad wymagają akcji i definiowania wymagań dla zautomatyzowanych systemów monitorowania i zgodności, które będą Wykrywaj naruszenia i Wyzwalaj akcje korygowania.

Zapoznaj się z sekcjami dotyczącymi korporacyjnych [przewodników ładu](../guides/index.md) , aby poznać Przykłady sposobu dopasowania procesu do planu nadzoru w chmurze.

## <a name="prioritize-policy-adherence-processes"></a>Ustalanie priorytetów procesów przestrzegania zasad

Ile inwestycji w procesy projektowania jest wymagane do obsługi celów zasad? W zależności od wielkości i dojrzałości wdrożenia w chmurze, nakładu pracy wymaganego do ustanowienia procesów, które obsługują zgodność, oraz kosztów związanych z tym nakładem mogą się znacznie różnić.

W przypadku małych wdrożeń składających się z zasobów deweloperskich i testowych wymagania dotyczące zasad mogą być proste i wymagają kilku dedykowanych zasobów do adresowania. Z drugiej strony, niezwykle ważne wdrożenie w chmurze o wysokim priorytecie w zakresie zabezpieczeń i wydajności może wymagać zespołu kadr, obszernych procesów wewnętrznych i niestandardowych narzędzi do monitorowania do obsługi celów zasad.

Pierwszym krokiem w definiowaniu strategii przestrzegania zasad jest określenie, jak procesy omówione poniżej mogą obsługiwać wymagania dotyczące zasad. Określ, jak dużo wysiłku ma być zainwestowany w te procesy, a następnie użyj tych informacji, aby utworzyć realistyczne plany budżetu i kadr, aby spełnić te wymagania.

## <a name="establish-cloud-governance-team-processes"></a>Ustanów procesy zespołu nadzoru chmurowego

Przed zdefiniowaniem wyzwalaczy do korygowania zgodności zasad należy określić ogólne procesy, które będą używane przez zespół, oraz informacje o udostępnianiu i eskalacji między personelem działu IT i zespołem nadzoru chmurowego.

### <a name="assign-cloud-governance-team-members"></a>Przypisz członków zespołu nadzoru w chmurze

Zespół ds. zarządzania chmurą zapewni ciągłe wskazówki dotyczące zgodności zasad i obsługuje problemy związane z zasadami, które napływają podczas wdrażania i obsługi zasobów w chmurze. Podczas kompilowania tego zespołu należy zaprosić członków personelu, którzy mają wiedzę fachową w dziedzinach objętych zdefiniowanymi instrukcjami zasad i określonymi zagrożeniami.

W przypadku początkowych wdrożeń testowych może to być ograniczone do kilku administratorów systemu odpowiedzialnych za ustalenie podstaw zarządzania. Jako że Twoje procesy nadzoru zakończyły się, przejrzyj regularnie członkostwo zespołu wskazówek dotyczących chmury, aby upewnić się, że możesz poprawnie rozwiązać nowe potencjalne ryzyko i wymagania dotyczące zasad. Zidentyfikuj członków działu IT i służbowych z odpowiednimi doświadczeniami lub zainteresowaniami w określonych obszarach nadzoru i Dołącz je do swoich zespołów na stałe lub tymczasowe, zgodnie z potrzebami.

### <a name="reviews-and-policy-iteration"></a>Przeglądy i iteracje zasad

Po wdrożeniu dodatkowych zasobów i obciążeń zespół ds. zarządzania chmurą musi upewnić się, że nowe obciążenia lub zasoby będą zgodne z wymaganiami dotyczącymi zasad. Oceń nowe wymagania z zespołów programistycznych obciążeń, aby upewnić się, że ich planowane wdrożenia zostaną wyrównane do przewodników projektowych, i zaktualizuj zasady tak, aby obsługiwały te wymagania w razie potrzeby.

Zaplanuj ocenę nowych potencjalnych zagrożeń i aktualizowanie instrukcji zasad i zaprojektowanie przewodników zgodnie z wymaganiami. Współpracuj z pracownikami działu IT i zespołami obciążeń, aby regularnie szacować nowe funkcje i usługi platformy Azure. Zaplanuj także regularne przeglądy w każdym z pięciu dyscyplin ładu, aby zapewnić, że zasady są aktualne i zgodne.

### <a name="education"></a>Edukacja

Zgodność z zasadami wymaga, aby pracownicy IT i deweloperzy mogli zrozumieć wymagania dotyczące zasad, które mają wpływ na ich obszary odpowiedzialności. Zaplanuj, aby przeznaczyć zasoby na decyzje i wymagania oraz poinformować wszystkie odpowiednie zespoły dotyczące przewodników projektowych, które obsługują wymagania dotyczące zasad.

Wraz ze zmianami zasad, regularne aktualizowanie dokumentacji i materiałów szkoleniowych oraz zapewnienie wysiłków edukacyjnych komunikuje się z odpowiednim personelem działu IT.

Na różnych etapach podróży w chmurze może okazać się, że najlepiej skontaktować się z partnerami i programami szkoleniowymi w dziedzinie profesjonalnych, aby usprawnić edukację swojego zespołu, zarówno technicznie, jak i proceduralne. Ponadto wiele można znaleźć, że formalne certyfikaty są cennym uzupełnieniem portfela edukacji i powinny być brane pod uwagę.

### <a name="establish-escalation-paths"></a>Ustanów ścieżki eskalacji

Jeśli zasób wyjdzie z zgodności, który zostanie powiadomiony? Jeśli pracownicy działu IT wykrywają problemy ze zgodnością z zasadami, którzy się z nimi kontaktowają? Upewnij się, że proces eskalacji do zespołu zarządzania chmurą jest jasno zdefiniowany. Upewnij się, że te kanały komunikacyjne zostały zaktualizowane w celu odzwierciedlenia zmian pracowników i organizacji.

## <a name="violation-triggers-and-actions"></a>Wyzwalacze naruszenia i akcje

Po zdefiniowaniu zespołu nadzoru chmurowego i jego procesów należy jawnie określić, jakie są odpowiednie dla naruszeń zgodności, które będą wyzwalać akcje i jakie te działania powinny być.

### <a name="define-triggers"></a>Definiuj wyzwalacze

Dla każdej z zestawień zasad należy przejrzeć wymagania, aby określić, co stanowi naruszenie zasad. Generuj wyzwalacze przy użyciu informacji, które zostały już ustanowione jako część procesu definicji zasad.

- **Tolerancja ryzyka:** Utwórz wyzwalacze naruszenia na podstawie metryk i wskaźników ryzyka, które zostały określone w ramach [analizy tolerancji ryzyka](./risk-tolerance.md).
- **Zdefiniowane wymagania dotyczące zasad:** Oświadczenia zasad mogą zapewniać umowę dotyczącą poziomu usług (SLA), ciągłość biznesową i odzyskiwanie po awarii (BCDR) lub wymagania dotyczące wydajności, które powinny być używane jako podstawa dla wyzwalaczy zgodności.

### <a name="define-actions"></a>Zdefiniuj akcje

Każdy wyzwalacz naruszenia powinien mieć odpowiadającą akcję. Akcje wyzwalane zawsze powiadamiają odpowiedniego pracownika działu IT lub członka zespołu nadzoru o chmurze w przypadku wystąpienia naruszenia. To powiadomienie może prowadzić do ręcznego przeglądu problemu ze zgodnością lub podzieloną wstępnie zdefiniowanego procesu korygowania w zależności od typu i ważności wykrytego naruszenia.

Przykładowe wyzwalacze naruszenia i akcje:

| Dyscyplina ładu chmury | Przykładowy wyzwalacz | Przykładowa akcja |
|-----------------------------|----------------|---------------|
| Cost Management | Miesięczne wydatki na chmurę są większe niż 20% wyższe niż oczekiwano. | Powiadom lidera jednostki rozliczeniowej, który rozpocznie przegląd użycia zasobów. |
| Punkt odniesienia zabezpieczeń | Wykrywaj podejrzane działania użytkownika. | Powiadom zespół ds. zabezpieczeń IT i Wyłącz podejrzane konto użytkownika. |
| Spójność zasobów | Użycie procesora CPU dla obciążenia jest większe niż 90%. | Powiadom zespół ds. operacji IT i Skaluj dodatkowe zasoby, aby obsłużyć obciążenie. |

## <a name="automation-of-monitoring-and-compliance"></a>Automatyzacja monitorowania i zgodności

Po zdefiniowaniu wyzwalaczy i akcji naruszenia zgodności można rozpocząć planowanie, jak najlepiej korzystać z narzędzi do rejestrowania i raportowania oraz innych funkcji platformy w chmurze, aby pomóc zautomatyzować strategię monitorowania i zgodności z zasadami.

Aby uzyskać pomoc przy wyborze najlepszego wzorca monitorowania dla danego wdrożenia, zobacz [Przewodnik rejestrowania i zgłaszania decyzji](../../decision-guides/logging-and-reporting/index.md).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o zgodności z przepisami w chmurze.

> [!div class="nextstepaction"]
> [Zgodność z przepisami](./regulatory-compliance.md)
