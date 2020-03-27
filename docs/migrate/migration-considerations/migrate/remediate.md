---
title: Korygowanie zasobów przed migracją
description: Dowiedz się, jak skorygować wszystkie zasoby, które są określane jako niezgodne z wybranym dostawcą chmury przed rozpoczęciem migracji.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0805868195912807c50a49d781928865f2f82ca9
ms.sourcegitcommit: ea63be7fa94a75335223bd84d065ad3ea1d54fdb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80355218"
---
# <a name="remediate-assets-prior-to-migration"></a>Korygowanie zasobów przed migracją

Podczas procesu oceny migracji zespół chce zidentyfikować konfiguracje, które mogłyby spowodować niezgodność zasobu z wybranym dostawcą chmury. *Korygowanie* jest punktem kontrolnym w procesie migracji, w którym można upewnić się, że te niezgodności zostały rozwiązane. W tym artykule omówiono kilka przykładowych typowych zadań korygowania. Przedstawiono również ramowy proces ułatwiający zdecydowanie, czy korygowanie jest mądrą inwestycją.

## <a name="common-remediation-tasks"></a>Typowe zadania korygowania

W każdym środowisku firmowym istnieje dług techniczny. Częściowo jest on oczekiwany i oznacza dobrą kondycję środowiska. Decyzje dotyczące architektury, które dobrze pasowały do środowiska lokalnego, mogą nie być odpowiednie na platformie chmury. W każdym przypadku typowe zadania korygowania mogą być wymagane w celu przygotowania zasobów do migracji. Poniżej przedstawiono kilka przykładów:

- **Drobne uaktualnienia hosta.** Czasami nieaktualny host musi zostać uaktualniony przed replikacją.
- **Drobne uaktualnienia systemu operacyjnego gościa.** Najprawdopodobniej system operacyjny będzie wymagać poprawek lub uaktualnienia przed replikacją.
- **Modyfikacje umowy SLA.** Na platformie chmury znacznie zmieniają się procesy tworzenia kopii zapasowej lub odzyskiwania. Prawdopodobnie procesy tworzenia kopii zapasowych zapasów będą potrzebować drobnych modyfikacji, aby zapewnić ciągłość działania w chmurze.
- **Migracja usługi PaaS.** W niektórych przypadkach wdrożenie PaaS struktury danych lub aplikacji może być wymagane do przyspieszenia wdrożenia. Aby przygotować rozwiązanie do wdrożenia usługi PaaS, czasami trzeba wprowadzić drobne modyfikacje.
- **Zmiany kodu usługi PaaS.** Nierzadko przygotowanie aplikacji niestandardowych do korzystania z usługi PaaS wymaga drobnych modyfikacji kodu. Przykłady mogą obejmować metody, które m.in. zapisują na dysku lokalnym lub używają stanu sesji w pamięci.
- **Zmiany konfiguracji aplikacji.** Migrowane aplikacje mogą wymagać zmian zmiennych, takich jak ścieżki sieciowe do zasobów zależnych, zmiany konta usługi lub aktualizacje zależnych adresów IP.
- **Drobne zmiany ścieżek sieciowych.** Wzorce routingu mogą wymagać modyfikacji w celu prawidłowego kierowania ruchu użytkowników do nowych zasobów.
    > [!NOTE]
    > To nie jest Routing produkcyjny do nowych zasobów, ale raczej konfiguracja pozwala na ogólne kierowanie do zasobów.

## <a name="large-scale-remediation-tasks"></a>Zadania korygowania na dużą skalę

Gdy centrum danych jest prawidłowo obsługiwane i aktualizowane, a jego poprawki są wprowadzane w odpowiedni sposób, prawdopodobnie potrzeba korygowania będzie mała. Rozbudowane środowiska z możliwością korygowania są często używane w dużych przedsiębiorstwach, organizacjach, w których przeprowadzono operację zmniejszenia dużego działu IT, niektórych starszych środowiskach usług zarządzanych i środowiskach z możliwością nabywania. W każdym z tych typów środowisk korygowanie może zużywać znaczną część pracy związanej z migracją. Kiedy poniższe zadania korygujące są często wykonywane i mają negatywny wpływ na szybkość migracji lub spójność, warto rozważyć przeniesienie korygowania do równoległego nakładu pracy i zespołu (podobnie jak wdrażanie chmury i zarządzanie chmurą działają równolegle).

- **Częste uaktualnienia hosta.** Jeśli do zakończenia migracji obciążenia jest wymagana duża liczba hostów, prawdopodobnie wystąpią obciążenia pracy zespołu ds. migracji. Może być konieczne przerwanie działania aplikacji i rozwiązywanie problemów związanych z korygowaniem przed uwzględnieniem odpowiednich aplikacji w jakichkolwiek planowanych wersjach.
- **Częste uaktualnienia systemu operacyjnego gościa.** Duże przedsiębiorstwa często mają serwery z nieaktualnymi wersjami systemu Linux lub Windows. Oprócz oczywistych zagrożeń bezpieczeństwa związanych z nieaktualnym systemem operacyjnym, występują również problemy z niezgodnością, które uniemożliwiają migrowanie uwzględnionych obciążeń. Jeśli duża liczba maszyn wirtualnych wymaga korygowania systemu operacyjnego, warto podzielić te działania na iterację równoległą.
- **Znaczące zmiany kodu.** Starsze aplikacje niestandardowe mogą wymagać znacznie większej liczby modyfikacji w celu przygotowania ich do wdrożenia usługi PaaS. W takim przypadku może być konieczne usunięcie ich z listy prac migracji w całości i zarządzanie nimi w całkowicie osobnym programie.

## <a name="decision-framework"></a>Platforma decyzyjna

Korygowanie mniejszych obciążeń może być proste, co jest jednym z powodów, dla których zaleca się wybranie mniejszego obciążenia w przypadku początkowej migracji. Jednak w miarę rozwoju działań dotyczących migracji i rozpoczynania pracy nad większymi obciążeniami, korygowanie może stać się procesem czasochłonnym i kosztownym. Na przykład działania korygujące dotyczące migracji systemu Windows Server 2003, które obejmują pulę zasobów z ponad 5000 maszyn wirtualnych, może opóźnić migrację o wiele miesięcy. Gdy wymagane jest takie korygowanie na dużą skalę, następujące pytania mogą pomóc w podjęciu decyzji:

- Czy wszystkie obciążenia, na które ma wpływ korygowanie, zostały zidentyfikowane i zastąpione na liście prac migracji?
- Czy w przypadku nieuwzględnionych obciążeń migracja będzie wygeneruje podobny zwrot z inwestycji?
- Czy uwzględnione zasoby można korygować w sposób dopasowany do oryginalnej osi czasu migracji? Jaki wpływ mają zmiany osi czasu na zwrot z inwestycji?
- Czy z ekonomicznego punktu widzenia możliwe jest korygowanie zasobów równolegle z pracą dotyczącą migracji?
- Czy personel ma wystarczającą przepustowość do korygowania i migrowania? Czy partner powinien być zaangażowany w wykonywanie jednego lub obu zadań?

Jeśli odpowiedzi na te pytania nie są satysfakcjonujące, warto rozważyć użycie kilku alternatywnych metod, które przekraczają zadania podstawowej strategii ponownego hostowania usługi IaaS:

- **Konteneryzacja.** Niektóre zasoby mogą być hostowane w środowisku kontenerów bez korygowania. Może to spowodować niekorzystną wydajność i nie rozwiązuje problemów dotyczących zabezpieczeń ani zgodności.
- **Automatyzacja.** W zależności od wymagań związanych z obciążeniem i korygowaniem bardziej zyskowne może być wykonanie skryptu wdrożenia do nowych zasobów przy użyciu podejścia obejmującego metodykę DevOps.
- **Przebudowa.** Jeśli koszty korygowania są bardzo wysokie, a wartość biznesowa jest równie wysoka, obciążenie może być dobrym kandydatem do przebudowy lub ponownego utworzenia architektury.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu korygowania [działania związane z replikacją](./replicate.md) są gotowe.

> [!div class="nextstepaction"]
> [Replikowanie zasobów](./replicate.md)
