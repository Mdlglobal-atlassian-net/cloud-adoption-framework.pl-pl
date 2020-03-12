---
title: Wdrożenie planu wdrożenia chmury w usłudze Azure DevOps
description: Dowiedz się, jak szybko wdrożyć zaległość do usługi Azure DevOps za pomocą szablonu planu wdrażania w chmurze, który umożliwia dostosowanie działań związanych z wdrażaniem w chmurze do procesu standardowego.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 243094da7b92a374124474eaaf0c955b5fdb85ed
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140607"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>Plan wdrażania chmury i usługa Azure DevOps

Azure DevOps to zestaw narzędzi opartych na chmurze dla klientów platformy Azure, którzy zarządzają projektami iteracyjnymi. Zawiera także narzędzia do zarządzania potokumi wdrażania i innymi ważnymi aspektami DevOps.

W tym artykule dowiesz się, jak szybko wdrożyć zaległość do usługi Azure DevOps przy użyciu szablonu planu wdrażania w chmurze. Ten szablon służy do wyrównania działań związanych z wdrażaniem w chmurze do procesu standardowego w oparciu o wskazówki w strukturze wdrożenia chmury.

## <a name="create-your-cloud-adoption-plan"></a>Tworzenie planu wdrażania chmury

Aby wdrożyć plan wdrażania chmury, Otwórz [Generator demonstracji usługi Azure DevOps](https://aka.ms/adopt/plan/generator). To narzędzie spowoduje wdrożenie szablonu w dzierżawie usługi Azure DevOps. Korzystanie z narzędzia wymaga wykonania następujących czynności:

1. Sprawdź, czy w polu **wybrany szablon** jest ustawiony **plan wdrożenia chmury**. Jeśli tak nie jest, wybierz pozycję **Wybierz szablon** , aby wybrać odpowiedni szablon.
2. W polu listy rozwijanej **wybierz organizację** wybierz swoją organizację usługi Azure DevOps.
3. Wprowadź nazwę nowego projektu. Plan wdrażania w chmurze będzie miał tę nazwę, gdy zostanie wdrożony w dzierżawie usługi Azure DevOps.
4. Wybierz pozycję **Utwórz projekt** , aby utworzyć nowy projekt w dzierżawie na podstawie szablonu planu. Pasek postępu przedstawia postępy w kierunku wdrażania projektu.
5. Po zakończeniu wdrażania wybierz pozycję **Przejdź do projektu** , aby wyświetlić nowy projekt.

Po utworzeniu projektu przejdź do tej serii artykułów, aby zobaczyć, jak można zmodyfikować szablon w celu dostosowania go do planu wdrożenia w chmurze.

Aby uzyskać dodatkową pomoc techniczną i wskazówki dotyczące tego narzędzia, zobacz [Azure DevOps Services Generator demonstracji](https://docs.microsoft.com/azure/devops/demo-gen/?toc=/azure/devops/demo-gen/toc.json&bc=/azure/devops/demo-gen/breadcrumb/toc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Edytuj zbiorczo plan wdrażania chmury

Po wdrożeniu projektu planu można go zmodyfikować przy użyciu programu Microsoft Excel. Znacznie łatwiej jest tworzyć nowe obciążenia lub zasoby w planie przy użyciu programu Excel, niż przy użyciu środowiska przeglądarki Azure DevOps.

Aby przygotować stację roboczą do edycji zbiorczej, zobacz [zbiorcze Dodawanie lub modyfikowanie elementów roboczych za pomocą programu Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Korzystanie z planu wdrażania chmury

Plan wdrażania chmury organizuje działania według typu działania:

- **Epiki:** *Epiku* reprezentuje ogólną fazę cyklu wdrożenia chmury.
- **Funkcje:** Funkcje służą do organizowania określonych celów w każdej fazie. Na przykład migracja określonego obciążenia będzie jedną funkcją.
- **Historie użytkownika:** Grupa historie użytkownika działa w logicznych kolekcjach działań na podstawie określonego celu.
- **Zadania:** Zadania są rzeczywistą czynnością do wykonania.

W każdej warstwie działania są następnie sekwencjonowane na podstawie zależności. Działania są połączone z artykułami w strukturze wdrażania w chmurze w celu wyjaśnienia zamierzenia lub zadania.

Najwyraźniejszy widok planu wdrażania w chmurze pochodzi z widoku zaległości **epiki** . Aby uzyskać pomoc dotyczącą zmiany do widoku zaległości **epiki** , zobacz artykuł dotyczący [wyświetlania zaległości](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog). Z tego widoku można łatwo planować pracę i zarządzać nią wymaganą do ukończenia bieżącej fazy cyklu wdrażania.

> [!NOTE]
> Bieżący stan planu wdrażania w chmurze koncentruje się w dużym stopniu na wysiłki związane z migracją. Zadania związane z zarządzaniem, innowacyjnością lub operacjami muszą zostać wypełnione ręcznie.

## <a name="align-the-cloud-adoption-plan"></a>Dopasuj plan wdrażania chmury

Na stronach przeglądu faz strategii i planowania cyklu życia wdrożenia chmury każdy odwołuje się do [strategii i szablonu planowania struktury wdrażania w chmurze](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Ten szablon organizuje decyzje i punkty danych, które będą wyrównać szablon planu wdrożenia chmury przy użyciu określonych planów na potrzeby wdrażania. Jeśli jeszcze tego nie zrobiono, warto wykonać ćwiczenia związane z [strategią](../strategy/index.md) i [planowaniem](../plan/index.md) przed wyrównaniem nowego projektu.

Poniższe artykuły obsługują wyrównania planu wdrażania chmury:

- [Obciążenia](./workloads.md): Wyrównaj funkcje w migracja do chmury epiku, aby przechwytywać każde obciążenie, które ma zostać zmigrowane lub zmodernizowane. Dodawanie i modyfikowanie tych funkcji w celu przechwycenia nakładu pracy w celu przeprowadzenia migracji 10 najważniejszych obciążeń.
- [Zasoby](./assets.md): każdy zasób (maszyna wirtualna, aplikacja lub dane) jest reprezentowany przez scenariusze użytkownika w poszczególnych obciążeniach. Dodaj i zmodyfikuj te historie użytkownika, aby dostosować je do swoich cyfr.
- [Racjonalizacja](./review-rationalization.md): w miarę definiowania każdego obciążenia można zakwestionować początkowe założenia dotyczące tego obciążenia. Może to spowodować wprowadzenie zmian w zadaniach w ramach każdego elementu zawartości.
- [Tworzenie planów wydania](./iteration-paths.md): ścieżki iteracji ustanawiają plany wydania przez dostosowanie wysiłków do różnych wersji i iteracji.
- [Ustalanie osi czasu](./timelines.md): Definiowanie dat rozpoczęcia i zakończenia dla każdej iteracji powoduje utworzenie osi czasu do zarządzania ogólnym projektem.

Te pięć artykułów ułatwiają wykonywanie zadań związanych z wyrównywaniem wymaganych do rozpoczęcia zarządzania zastosowaniami. W następnym kroku zostanie rozpoczęte ćwiczenie wyrównania.

## <a name="next-steps"></a>Następne kroki

Rozpocznij wyrównywanie projektu planu przez [Definiowanie obciążeń i określanie priorytetów](./workloads.md).

> [!div class="nextstepaction"]
> [Definiowanie obciążeń i określanie priorytetów](./workloads.md)
