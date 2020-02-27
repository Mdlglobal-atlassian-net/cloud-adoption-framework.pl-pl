---
title: Przeprowadź przegląd zasad w chmurze
description: Dowiedz się, jak przeprowadzić modernizację istniejących firmowych zasad IT, aby zapewnić odpowiedni poziom zarządzania ryzykiem dla zasobów opartych na chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e4235830eee8e57581214f3eabb46c32ebcf975b
ms.sourcegitcommit: af45c1c027d7246d1a6e4ec248406fb9a8752fb5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/27/2020
ms.locfileid: "77709128"
---
<!-- markdownlint-disable MD026 -->

# <a name="conduct-a-cloud-policy-review"></a>Przeprowadź przegląd zasad w chmurze

Przegląd zasad w chmurze to pierwszy krok w kierunku [ładu](../index.md) w chmurze. Celem tego procesu jest modernizacja istniejących firmowych zasad IT. Po zakończeniu zaktualizowane zasady zapewniają odpowiedni poziom zarządzania ryzykiem dla zasobów opartych na chmurze. W tym artykule opisano proces przeglądu zasad w chmurze i jego znaczenie.

## <a name="why-perform-a-cloud-policy-review"></a>Dlaczego należy przeprowadzić przegląd zasad w chmurze?

Większość firm zarządza nimi przez wykonywanie procesów, które są wyrównywane przy użyciu zasad. W małych firmach te zasady mogą anecdotal i przetwarzać wiele procesów. W miarę rozwoju działalności firmy w dużych przedsiębiorstwach zasady i procesy są bardziej jasno udokumentowane i konsekwentnie wykonywane.

W przypadku firmowych zasad IT, zależności od przeszłych decyzji technicznych mają tendencje do seep do zarządzania zasadami. Na przykład wspólne dla wszystkich procesów odzyskiwania po awarii obejmuje zasady, które mają możliwość wykonywania kopii zapasowych na taśmach poza siedzibą firmy. To dołączenie zakłada zależność od jednego typu technologii (kopie zapasowe na taśmach), która może nie być już najbardziej odpowiednim rozwiązaniem.

Przekształcenia w chmurze tworzą naturalny punkt przegięcia, aby ponownie uwzględnić starsze decyzje dotyczące zasad. Możliwości techniczne i procesy domyślne zmieniają się w sposób istotny w chmurze, tak jak w przypadku dziedziczenia zagrożeń. Korzystając z poprzedniego przykładu, zasady tworzenia kopii zapasowej na taśmie wynikające z ryzyka single point of failure przez utrzymywanie danych w jednej lokalizacji, a firma musi zminimalizować profil ryzyka przez ograniczenie tego ryzyka. W przypadku wdrożenia w chmurze istnieje kilka opcji, które zapewniają takie samo Łagodzenie ryzyka, o znacznie niższych celach dotyczących czasu odzyskiwania (RTO). Na przykład:

- Rozwiązanie natywne w chmurze może umożliwić replikację geograficzną Azure SQL Database.
- Rozwiązanie hybrydowe może używać Azure Site Recovery do replikowania obciążenia IaaS na platformę Azure.

Podczas wykonywania transformacji w chmurze zasady często określają wiele narzędzi, usług i procesów dostępnych dla zespołów wdrażania chmury. Jeśli te zasady są oparte na starszych technologiach, mogą utrudniać działania zespołu w celu zmiany dysku. W najgorszym przypadku ważne zasady są całkowicie ignorowane przez zespół migracji w celu umożliwienia obejścia tego problemu. Nie jest to akceptowalny wynik.

## <a name="the-cloud-policy-review-process"></a>Proces przeglądu zasad w chmurze

Przeglądy zasad w chmurze przedstawiają istniejące zagadnienia dotyczące zarządzania i zabezpieczeń IT przy użyciu [pięciu dyscyplin](../index.md)nadzoru w chmurze: [Cost Management](../cost-management/index.md), [linia bazowa zabezpieczeń](../security-baseline/index.md), [linia bazowa tożsamości](../identity-baseline/index.md), [spójność zasobów](../resource-consistency/index.md)i [przyspieszenie wdrożenia](../deployment-acceleration/index.md).

W przypadku każdej z tych dyscyplin proces przeglądu następuje w następujących krokach:

1. Zapoznaj się z istniejącymi zasadami lokalnymi związanymi z konkretną dyscypliną, szukając dwóch kluczowych punktów danych: starszych zależności i zidentyfikowanych zagrożeń firmy.
2. Oceń każde ryzyko biznesowe, pytając o pytanie proste: "czy ryzyko biznesowe nadal istnieje w modelu chmury?".
3. Jeśli nadal istnieje ryzyko, napisz ponownie zasady, wprowadzając odpowiednie środki zaradcze, a nie rozwiązanie techniczne.
4. Zapoznaj się z zaktualizowanymi zasadami przy użyciu zespołów wdrażania chmury, aby zrozumieć potencjalne rozwiązania techniczne dotyczące wymaganego ograniczenia.

## <a name="example-of-a-policy-review-for-a-legacy-policy"></a>Przykład przeglądu zasad dla starszych zasad

Aby podać przykład procesu, ponownie Użyj zasad tworzenia kopii zapasowej na taśmie w poprzedniej sekcji:

- Zasady firmowe mają możliwość tworzenia kopii zapasowych na taśmach poza siedzibą firmy dla wszystkich systemów produkcyjnych. W tych zasadach można zobaczyć dwa interesujące punkty danych:
  - Starsza zależność od rozwiązania do tworzenia kopii zapasowej na taśmie
  - Zakładane ryzyko biznesowe związane z przechowywaniem kopii zapasowych w tej samej lokalizacji fizycznej co sprzęt produkcyjny.
- Czy nadal istnieje ryzyko? Tak. Nawet w chmurze zależność od jednej funkcji tworzy pewne ryzyko. Istnieje mniejsze prawdopodobieństwo tego ryzyka, które ma wpływ na działalność, która nie była obecna w rozwiązaniu lokalnym, ale nadal istnieje ryzyko.
- Ponowne Zapisywanie zasad. W przypadku awarii obejmującej całe centrum danych musi istnieć możliwość przywrócenia systemów produkcyjnych w ciągu 24 godzin od przestoju w innym centrum i w innej lokalizacji geograficznej.
  - Należy również wziąć pod uwagę, że oś czasu określona w powyższym zapotrzebowaniu może zostać ustawiona przez ograniczenia techniczne, które nie są już obecne w chmurze. Upewnij się, że rozumiesz ograniczenia techniczne i możliwości chmury przed zastosowaniem starszej RTO/celu punktu odzyskiwania.
- Zapoznaj się z zespołami wdrażania chmury. W zależności od implementowanego rozwiązania istnieje wiele metod przestrzegania tych zasad spójności zasobów.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat klasyfikacji danych w strategii zarządzania chmurą.

> [!div class="nextstepaction"]
> [Klasyfikacja danych](./data-classification.md)
