---
title: Priorytety biznesowe w procesie transformacji
description: Korzystaj z platformy wdrażania w chmurze dla platformy Azure, aby dowiedzieć się, jak zachować wyrównanie biznesowe podczas długotrwałego procesu transformacji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: df41ee9dfe94d0279f8a0c29982e8aff2dd83782
ms.sourcegitcommit: 5411c3b64af966b5c56669a182d6425e226fd4f6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79312054"
---
# <a name="business-priorities-maintaining-alignment"></a>Priorytety biznesowe: obsługa wyrównania

*Transformacja* jest często definiowana jako dramatyczna lub nagła zmiana. Na poziomie zarządu zmiana rzeczywiście może wydawać się dramatyczna. Jednak dla osób zaangażowanych w proces wprowadzania zmian w organizacji transformacja to pojęcie mylące. W swojej istocie transformacja to tak naprawdę seria prawidłowo wykonanych przejść z jednego stanu do drugiego.

Ilość czasu wymagana do usprawnienia lub przeniesienia obciążenia może się różnić w zależności od stopnia złożoności technicznej tego procesu. Jednak nawet jeśli ten proces może być sprawnie przeprowadzony w odniesieniu do jednego obciążenia lub grupy aplikacji, minie trochę czasu, zanim u użytkowników zajdą istotne zmiany. Rozpowszechnienie zmian w różnych warstwach istniejących procesów biznesowych może zająć jeszcze więcej czasu. Jeśli transformacja ma ukształtować wzorce zachowań wśród konsumentów, znaczące rezultaty mogą wystąpić po dłuższym czasie.

Niestety rynek nie czeka, aż firma wprowadzi zmiany. Wzorce zachowań konsumentów zmieniają się samoistnie i często nieoczekiwanie. Na postrzeganie firmy i jej produktów przez rynek mogą mieć wpływ media społecznościowe lub działanie konkurentów. Szybkie i nieoczekiwane zmiany na rynku wymagają od firm szybkiej reakcji.

Zdolność przeprowadzania procesów i wprowadzania zmian technicznych wymaga nieustannej pracy. Aby reagować na warunki rynkowe, trzeba działać skutecznie i podejmować szybkie decyzje. Jest w tym pewna sprzeczność, która może doprowadzić do utraty spójności z priorytetami. W tym artykule opisano sposoby na zachowanie kontroli nad transformacją podczas przeprowadzania migracji.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-business-and-technical-priorities-stay-aligned-during-a-migration"></a>W jaki sposób można utrzymać spójność priorytetów biznesowych i technicznych podczas migracji?

Zespół wdrożeniowy ds. chmury i zespół ds. ładu w chmurze skupiają się na wykonaniu bieżącej iteracji i bieżącego wydania. Iteracje zapewniają stabilne przyrosty pracy technicznej, co umożliwia uniknięcie kosztownych zakłóceń mogących spowodować spowolnienie procesu migracji. Wydania gwarantują, że wysiłek techniczny i energia skupiają się na celach biznesowych przyjętych w procesie migracji obciążeń. Projekt migracji może wymagać przeprowadzenia wielu wydań w dłuższym okresie. Do momentu zakończenia tego procesu warunki rynkowe mogą znacząco się zmienić.

Dlatego właśnie strategiczny zespół ds. chmury jednocześnie pracuje nad wykonaniem planu zmian biznesowych i przygotowaniem następnego wydania. Zespół strategiczny ds. chmury zwykle planuje co najmniej jedno wydanie naprzód i monitoruje zmiany warunków rynkowych, dostosowując do nich listę prac związanych z migracją. Koncentracja na zarządzaniu transformacją i dostosowywaniu planu prowadzi do tego, że naturalnie skupiamy się na odpowiednich obszarach pracy technicznej. Gdy zmieniają się priorytety biznesowe, firma jest tylko o jedno wydanie do tyłu, dzięki czemu może zachować elastyczność biznesową i techniczną.

## <a name="business-alignment-questions"></a>Pytania dotyczące zachowania spójności biznesowej

Następujące pytania mogą pomóc zespołowi strategicznemu ds. chmury w przygotowaniu listy prac związanych z migracją i określeniu właściwych priorytetów w celu zagwarantowania, że proces transformacji jest spójny z bieżącymi potrzebami biznesowymi.

- Czy zespół wdrożeniowy ds. chmury określił listę obciążeń gotowych do migracji?
- Czy zespół wdrożeniowy ds. chmury wybrał jedno obciążenie z tej listy obciążeń do początkowej migracji?
- Czy zespół wdrożeniowy ds. chmury i zespół ds. utrzymania ładu w chmurze mają wszystkie niezbędne dane dotyczące obciążenia i środowiska chmury, aby migracja przebiegła pomyślnie?
- Czy wybrane obciążenie ma największy wpływ na działalność firmy podczas kolejnego wydania?
- Czy są inne obciążenia, które są lepszymi kandydatami do migracji?

## <a name="tangible-actions"></a>Konkretne działania

Podczas wykonywania planu transformacji biznesowej zespół strategiczny ds. chmury monitoruje pozytywne i negatywne skutki. Gdy te obserwacje wskażą na konieczność wprowadzenia zmian technicznych, do listy prac wydania wprowadzane są korekty w formie elementów roboczych, które będą priorytetami podczas kolejnej iteracji.

Jeśli na rynku zachodzą zmiany, zespół strategiczny ds. chmury współpracuje z innymi osobami w firmie, aby opracować plan reakcji na te zmiany. Jeśli reakcja wymaga wprowadzenia zmian w priorytetach migracji, lista prac związanych z migracją jest odpowiednio korygowana. Obciążeniom, które poprzednio znajdowały się niżej na liście, nadawany jest wyższy priorytet.

## <a name="next-steps"></a>Następne kroki

Dzięki odpowiednio dostosowanym priorytetom biznesowym zespół wdrożeniowy ds. chmury może pewnie rozpocząć [ocenianie obciążeń](./evaluate.md) w celu opracowania planów architektury i migracji.

> [!div class="nextstepaction"]
> [Ocenianie obciążeń](./evaluate.md)
