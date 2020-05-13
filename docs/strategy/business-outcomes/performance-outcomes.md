---
title: Przykłady wyników wydajności
description: Użyj platformy wdrażania w chmurze dla platformy Azure, aby zrozumieć wyniki wydajności w kontekście transformacji w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 5b96c9216619a881ec9ad5a09e77ef9b3955bdb0
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83216286"
---
# <a name="examples-of-performance-outcomes"></a>Przykłady wyników wydajności

Zgodnie z opisem w części [wyniki biznesowe](./index.md)kilka potencjalnych rezultatów działania może stanowić podstawę dla każdej rozmowy transformującej transformację z firmą. Ten artykuł koncentruje się na typowej mierze biznesowej: wydajności.

W dzisiejszym świecie technicznym klienci zakładają, że aplikacje będą działać prawidłowo i są zawsze dostępne. Gdy to oczekiwanie nie jest spełnione, spowoduje to uszkodzenie reputacji, które może być kosztowne i długotrwałe.

## <a name="performance"></a>Wydajność

Największe usługi chmury obliczeniowej działają w ogólnoświatowej sieci zabezpieczonych centrów danych, które są regularnie uaktualniane do najnowszej generacji szybkiego i wydajnego sprzętu komputerowego. Zapewnia to kilka korzyści w ramach jednego korporacyjnego centrum danych, na przykład krótsze opóźnienia sieci dla aplikacji i większe oszczędności skali.

Przekształć swoją firmę i Obniż koszty dzięki infrastrukturze energooszczędnej, która obejmuje ponad 100 wysoce bezpiecznych udogodnień na całym świecie, połączone z jedną z największych sieci na ziemi. Platforma Azure oferuje więcej regionów globalnych niż jakikolwiek inny dostawca usług w chmurze. Umożliwia to przetłumaczenie na skalę, która jest wymagana w celu wprowadzenia aplikacji bliżej użytkowników na całym świecie, zachowania miejsca zamieszkania danych oraz zapewnienia kompleksowej zgodności i opcji odporności dla klientów.

- **Przykład 1:** Firma usług pracowała z dostawcą hostingu obsługującym wiele zasobów infrastruktury operacyjnej. Te systemy były przyczyną częstej awarii i niskiej wydajności. Firma przebiegła swoje zasoby na platformę Azure, aby korzystać z kontroli umów SLA i wydajności w chmurze. Czas przestoju, który poniósł koszt IT około $15 000 USD na minutę. Po upływie czterech i ośmiu godzin przestojów miesięcznie można było łatwo uzasadnić tę transformację organizacyjną.

- **Przykład 2:** Firma inwestycyjna dla odbiorców była na wczesnych etapach pracy innowacyjnej aplikacji z obsługą chmury. Procesy Agile i DevOps były również wymagalne, ale wydajność aplikacji została przerwana. Jako bardziej dojrzała transformacja firma rozpoczęła program do monitorowania i automatyzowania ustalania rozmiarów na podstawie wymagań dotyczących użycia. Firma eliminuje problemy związane z ustalaniem rozmiaru przy użyciu narzędzi do zarządzania wydajnością platformy Azure, co powoduje wzrost zaskakujące transakcji.

## <a name="reliability"></a>Niezawodność

Chmura obliczeniowa umożliwia łatwiejsze i tańsze tworzenie kopii zapasowych danych, odzyskiwanie po awarii oraz ciągłość działania firmy, ponieważ dane mogą być dublowane w wielu nadmiarowych lokacjach w sieci dostawcy chmury.

Jedną z najważniejszych funkcji jest zapewnienie, że dane firmowe nigdy nie są tracone i aplikacje pozostają dostępne pomimo awarii serwera, przerwy w zasilaniu lub klęski żywiołowej. Dane można chronić i odzyskiwać, wykonując kopię zapasową na platformie Azure.

Azure Backup to proste rozwiązanie, które zmniejsza koszty związane z infrastrukturą przy jednoczesnym zapewnieniu ulepszonych mechanizmów zabezpieczeń w celu ochrony danych przed oprogramowaniem wymuszającego okup. Jedno rozwiązanie umożliwia ochronę obciążeń uruchomionych na platformie Azure i lokalnie w systemach Linux, Windows, VMware i funkcji Hyper-V. Możesz zapewnić ciągłość działania, zachowując swoje aplikacje na platformie Azure.

Azure Site Recovery ułatwia testowanie odzyskiwania po awarii przez replikowanie aplikacji między regionami platformy Azure. Możesz również replikować lokalne maszyny wirtualne VMware i Hyper-V oraz serwery fizyczne do platformy Azure, aby pozostać dostępne, Jeśli lokacja główna ulegnie awarii. Można także odzyskać obciążenia do lokacji głównej, gdy zostanie ona uruchomiona ponownie.

- **Przykład:** Firma naftowa i gaz używa technologii platformy Azure do implementowania pełnego odzyskiwania lokacji. Firma zdecydowała się nie w pełni wdrożyć chmurę na potrzeby codziennych operacji, ale funkcje ciągłości działalności biznesowej i odzyskiwania po awarii (BCDR) chmury nadal chronią centrum danych. Ponieważ huragan miało setki kilometrów, ich partner implementacji uruchomił odzyskiwanie lokacji do platformy Azure. Przed wyhuraganem nie działa wszystkie zasoby o kluczowym znaczeniu, które zostały uruchomione na platformie Azure, co uniemożliwia ewentualne przestoje.

## <a name="next-steps"></a>Następne kroki

Dowiedz się [, jak używać szablonu wyniku biznesowego](./business-outcome-template.md).

> [!div class="nextstepaction"]
> [Korzystanie z szablonu wyniku biznesowego](./business-outcome-template.md)
