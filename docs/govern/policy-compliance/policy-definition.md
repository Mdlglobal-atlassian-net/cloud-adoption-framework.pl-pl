---
title: Zdefiniuj zasady firmowe ładu Cloud
description: Skorzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak ustanawiać zasady, które odnoszą się do znanych zagrożeń i tolerancji ryzyka podczas podróży w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: bb7ff19f7def1d41fa8a205667345ae0673503e4
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83399404"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Zdefiniuj zasady firmowe na potrzeby ładu w chmurze

Po przeanalizowaniu znanego ryzyka i powiązanej tolerancji ryzyka dla podróży w chmurze w organizacji, następnym krokiem jest ustanowienie zasad, które jawnie rozwiążą się z tymi zagrożeniami, i zdefiniujemy kroki potrzebne do ich skorygowania, jeśli jest to możliwe.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>Jak przygotować firmowe zasady IT do użycia w chmurze?

Zarówno w tradycyjnym, jak i w przyrostowym modelu zapewniania ładu zasady firmowe tworzą roboczą definicję ładu. Większość akcji podejmowanych w celu zapewnienia ładu IT koncentruje się na implementowaniu technologii w celu monitorowania, wymuszania, obsługiwania i automatyzowania tych zasad firmowych. Ład w chmurze jest oparty na podobnych pojęciach.

![Ład korporacyjny i dyscypliny ładu](../../_images/operational-transformation-govern-large.png)

_Rysunek 1. Ład korporacyjny i dyscypliny ładu._

Na powyższym obrazie przedstawiono relację między ryzykiem biznesowym, zasadami i zgodnością oraz mechanizmami monitorowania i wymuszania, które muszą współdziałać w ramach strategii zarządzania. Pięć dyscyplin zarządzania chmurą pozwala zarządzać tymi interakcjami i korzystać z strategii.

Ład w chmurze to wynik trwającego dłuższy czas wdrażania, ponieważ naprawdę trwała transformacja nie dokonuje się w ciągu jednego dnia. Próba zapewnienia kompletnego ładu w chmurze za pomocą szybkiej i agresywnej metody przed przeprowadzeniem kluczowych zmian zasad firmy rzadko daje oczekiwane wyniki. Zamiast tego zaleca się wprowadzanie przyrostowych zmian.

Informacje o strukturze wdrożenia chmury to cykl zakupów, który może umożliwić jego autentyczną transformację. Ponieważ nie istnieje duże wymaganie pozyskiwania wydatków inwestycyjnych, inżynierowie mogą zacząć eksperymentować i wdrażać. W większości firm wyeliminowanie we wdrażaniu bariery wydatków inwestycyjnych może prowadzić do szybszego generowania informacji zwrotnych, organicznego rozwoju i wykonywania przyrostowego.

Przejście do wdrażania w chmurze wymaga przejścia na wyższy poziom w zapewnianiu ładu. W wielu organizacjach przekształcenia zasad firmowych poprawiają ład i zwiększają stopień zgodności za pośrednictwem przyrostowych zmian zasad i zautomatyzowanego stosowania tych zmian. Takie zachowania można skonfigurować za pomocą nowo zdefiniowanych możliwości u dostawcy usług w chmurze.

<!-- markdownlint-enable MD026 -->

## <a name="review-existing-policies"></a>Przegląd istniejących zasad

Zgodnie z trwającym procesem nadzoru zasady powinny być regularnie analizowane z pracownikami IT i uczestnikami projektu, aby zapewnić, że zasoby hostowane w chmurze nadal utrzymują zgodność z ogólnymi celami i wymaganiami firmy. Zrozumienie nowych czynników ryzyka i akceptowalnego poziomu ich tolerowania może skłonić do [przejrzenia istniejących zasad](./cloud-policy-review.md) w celu określenia wymaganego poziomu ładu, odpowiedniego dla Twojej organizacji.

> [!TIP]
> Jeśli Twoja organizacja korzysta z dostawców lub innych zaufanych partnerów firmy, jednym z największych zagrożeń dla firmy, które należy wziąć pod uwagę, może być brak [zgodności z przepisami](./regulatory-compliance.md) obowiązującymi przez te organizacje zewnętrzne. Tego ryzyka często nie można skorygować, a zamiast tego mogą wymagać ścisłego przestrzegania wymagań przez wszystkie strony. Przed rozpoczęciem przeglądu zasad upewnij się, że zostały zidentyfikowane i zapoznaj się z wymaganiami dotyczącymi zgodności innych firm.

## <a name="create-cloud-policy-statements"></a>Tworzenie instrukcji dotyczących zasad w chmurze

Zasady IT oparte na chmurze określają wymagania, standardy i cele wymagane przez personel IT i zautomatyzowane systemy. Decyzje dotyczące zasad są podstawowym czynnikiem w [projekcie architektury chmury](./governance-alignment.md) oraz sposobem implementacji [procesów przestrzegania zasad](./processes.md).

Poszczególne instrukcje dotyczące zasad chmury to wskazówki dotyczące rozwiązywania określonych zagrożeń zidentyfikowanych podczas procesu oceny ryzyka. Te zasady można zintegrować z szeroką dokumentacją zasad korporacyjnych, więc oświadczenia dotyczące zasad w chmurze omówione w ramach przewodnika wdrażania w chmurze mają bardziej zwięzłe podsumowanie zagrożeń i planów postępowania z nimi. Każda definicja powinna zawierać następujące informacje:

- **Ryzyko biznesowe:** Podsumowanie ryzyka, którego dotyczy ta zasada.
- **Instrukcja zasad:** Zwięzłe wyjaśnienie wymagań zasad i celów.
- **Wskazówki dotyczące projektowania lub technicznego:** Zalecenia z możliwością wykonania akcji, specyfikacje lub inne wskazówki dotyczące obsługi i wymuszania tych zasad, których zespoły IT i deweloperzy mogą używać podczas projektowania i kompilowania wdrożeń w chmurze.

Jeśli potrzebujesz pomocy w rozpoczęciu definiowania zasad, zapoznaj się z tematami [ładu](../governance-disciplines.md) , które zostały wprowadzone w sekcji ładu przegląd. Artykuły dla każdej z tych dyscyplin obejmują przykłady typowych zagrożeń dla firmy, które występują podczas przechodzenia do chmury i przykładowych zasad służących do korygowania tych zagrożeń. Na przykład zobacz [przykładowe definicje zasad](../cost-management/policy-statements.md)w Cost Management dyscypliny.

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Stopniowe zarządzanie i integrowanie z istniejącymi zasadami

Planowane dodatki do środowiska chmury powinny zawsze być zbadane pod kątem zgodności z istniejącymi zasadami, a zasady zostały zaktualizowane w celu uwzględnienia wszelkich problemów, które nie zostały jeszcze omówione. Należy również przeprowadzić regularne [przeglądy zasad w chmurze](./cloud-policy-review.md) , aby upewnić się, że zasady chmury są aktualne i zsynchronizowane z nowymi zasadami firmowymi.

Konieczność integracji zasad w chmurze ze starszymi zasadami IT zależy głównie od dojrzałości procesów nadzoru chmurowego i rozmiaru chmury. Zapoznaj się z artykułem na temat [stopniowego zarządzania i zasad MVP,](./index.md) Aby uzyskać szersze Omówienie kwestii związanych z integracją zasad podczas przekształcania w chmurze.

## <a name="next-steps"></a>Następne kroki

Po zdefiniowaniu zasad należy wykonać wersję roboczą przewodnika projektowego architektury, aby udostępnić personelowi IT i deweloperom wskazówki umożliwiające podjęcie odpowiednich działań.

> [!div class="nextstepaction"]
> [Dopasuj Przewodnik dotyczący projektowania ładu przy użyciu zasad firmowych](./governance-alignment.md)
