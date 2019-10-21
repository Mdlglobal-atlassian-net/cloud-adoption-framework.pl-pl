---
title: Wskazówki dotyczące bezpieczeństwa systemu Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Jakie wskazówki dotyczące zabezpieczeń zapewnia firma Microsoft?
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8449878d46c939c58f690e585aac07fa0e827484
ms.sourcegitcommit: 35c162d2d09ec1c4a57d3d57a5db1d56ee883806
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/17/2019
ms.locfileid: "72548049"
---
<!-- markdownlint-disable MD026 -->

# <a name="microsoft-security-guidance"></a>Wskazówki dotyczące zabezpieczeń firmy Microsoft

## <a name="tools"></a>Narzędzia

Firma Microsoft wprowadziła [platformę zaufania usługi](https://servicetrust.microsoft.com) i Menedżera zgodności, aby pomóc w następujących kwestiach:

- Przezwyciężenie wyzwań związanych z zarządzaniem zgodnością.
- Spełnienie obowiązków związanych z wymaganiami prawnymi.
- Przeprowadzaj inspekcje samoobsługowe i oceniaj ryzyko użycia usługi w chmurze przedsiębiorstwa.

Te narzędzia zostały zaprojektowane w celu ułatwienia organizacjom zaspokajania złożonych obowiązków dotyczących zgodności i zwiększania możliwości ochrony danych podczas wybierania i używania usług Microsoft Cloud.

**Platforma zaufania usługi (STP)** zawiera szczegółowe informacje i narzędzia, które ułatwiają zaspokajanie potrzeb korzystania z usług Microsoft Cloud, takich jak Azure, Office 365, Dynamics 365 i Windows. STP to jednokrotne, szczegółowe informacje o zabezpieczeniach, przepisach, zgodności i ochronie prywatności dotyczące Microsoft Cloud. Jest to miejsce, w którym publikowane są informacje i zasoby niezbędne do samoobsługowego oceny ryzyka dotyczącego usług i narzędzi w chmurze. Usługa STP została utworzona w celu ułatwienia śledzenia działań zgodności z przepisami w ramach platformy Azure, w tym:

- **Menedżer zgodności:** Menedżer zgodności, narzędzie do oceny ryzyka opartego na przepływie pracy na platformie zaufania usługi firmy Microsoft, umożliwia śledzenie, przypisywanie i weryfikowanie działań w zakresie zgodności z przepisami organizacji związanych z usługami Microsoft Cloud, takimi jak Office 365, Dynamics 365 i Azure. Więcej szczegółów można znaleźć w następnej sekcji.
- **Dokumenty zaufania:** Obecnie istnieją trzy kategorie przewodników, które zapewniają dużo zasobów do oceny Microsoft Cloud; Dowiedz się więcej o działaniach firmy Microsoft w zakresie bezpieczeństwa, zgodności i prywatności; ułatwiają one ulepszanie funkcji ochrony danych. Należą do nich:
- **Raporty inspekcji:** Raporty inspekcji umożliwiają bieżące korzystanie z najnowszych informacji dotyczących ochrony prywatności, bezpieczeństwa i zgodności dla usług Microsoft Cloud. Obejmuje to ISO, SOC, FedRAMP i inne raporty audytu, litery i materiały związane z niezależnymi inspekcjami innych firm w ramach usług Microsoft Cloud, takich jak Azure, Office 365, Dynamics 365 i innych.
- **Przewodniki dotyczące ochrony danych:** Przewodniki dotyczące ochrony danych zawierają informacje dotyczące sposobu, w jaki usługi Microsoft Cloud Services chronią dane, oraz sposobu zarządzania zabezpieczeniami i zgodnością danych w chmurze w organizacji. Obejmuje to głębokie, szczegółowe oficjalne dokumenty, które zawierają szczegółowe informacje na temat sposobu, w jaki firma Microsoft projektuje i obsługuje usługi w chmurze, często zadawane pytania, raporty z końca roku oceny zabezpieczeń, możliwości testowania i wskazówki ułatwiające przeprowadzenie oceny ryzyka i poprawę danych możliwości ochrony.
- **Plan zabezpieczeń i zgodności platformy Azure:** Plany zapewniają zasoby ułatwiające tworzenie i uruchamianie aplikacji opartych na chmurze, które ułatwiają przestrzeganie rygorystycznych przepisów i standardów. Dzięki większej liczbie certyfikatów niż każdy inny dostawca usług w chmurze możesz mieć pewność, że w systemie Azure są dostępne następujące plany:
  - Omówienie i wskazówki dotyczące branżowych.
  - Macierz obowiązków klienta.
  - Architektura referencyjna z modelami zagrożeń.
  - Macierze implementacji kontroli.
  - Automatyzacja wdrażania architektury referencyjnej.
  - Zasoby związane z ochroną prywatności: Dokumentacja oceny wpływu na dane, żądania podmiotu danych (żądania podmiotów danych) i powiadomienia o naruszeniu danych są udostępniane w ramach własnego programu w celu obsługi Ogólne rozporządzenie o ochronie danych (Rodo).
- **Rozpocznij pracę z usługą Rodo:** Produkty i usługi firmy Microsoft pomagają organizacjom spełnić wymagania Rodo podczas zbierania lub przetwarzania danych osobowych. STP zaprojektowano w celu udostępnienia informacji o możliwościach usługi firmy Microsoft, których można użyć do rozwiązywania określonych wymagań Rodo. Dokumentacja może pomóc w Rodo odpowiedzialności i zrozumieniu środków technicznych i organizacyjnych. Dokumentacja dotycząca ocen wpływu na ochronę danych, żądania podmiotu danych (żądania podmiotów danych) i powiadomienia o naruszeniu danych są dostarczane w celu włączenia ich do własnego programu w celu obsługi Rodo.
  - **Żądania podmiotu danych:** Rodo przyznaje osobom (lub podmiotom danych) pewne prawa związane z przetwarzaniem danych osobowych. Obejmuje to prawo do poprawiania nieprawidłowych danych, wymazywania danych lub ograniczania ich przetwarzania, a także odbierania ich danych i realizacji żądania przesyłania danych do innego kontrolera.
  - **Naruszenie danych:** Rodo zezwala na wymagania dotyczące powiadomień dla kontrolerów danych i procesorów w przypadku naruszenia danych osobowych. STP zawiera informacje o tym, w jaki sposób firma Microsoft próbuje uniknąć naruszeń w pierwszym miejscu, w jaki sposób firma Microsoft wykrywa naruszenie i jak firma Microsoft reaguje na wypadek naruszenia i powiadomi Cię jako kontroler danych.
  - **Ocena wpływu ochrony danych:** Firma Microsoft pomaga kontrolerom w pełni Rodo oceny wpływu na ochronę danych. Rodo zawiera wyczerpującą listę przypadków, w których należy przeprowadzić DPIAs, na przykład automatyczne przetwarzanie na potrzeby profilowania i podobnych działań; przetwarzanie na dużą skalę specjalnych kategorii danych osobowych i systematyczne monitorowanie dostępnego publicznie obszaru na dużą skalę.
  - **Inne zasoby:** Oprócz wskazówek dotyczących narzędzi omówionych w powyższych sekcjach, STP również udostępnia inne zasoby, w tym zgodność regionalną, dodatkowe zasoby dla Centrum zabezpieczeń i zgodności, a także często zadawane pytania dotyczące platformy zaufania usługi, Menedżer zgodności i prywatność/Rodo.
- **Zgodność regionalna:** W przypadku usługi STP dostępne są liczne dokumenty dotyczące zgodności i wskazówki dla Usługi online firmy Microsoft spełniające wymagania dotyczące zgodności dla różnych regionów, w tym Republiki Czeskiej, polskiej i Rumunii.

## <a name="unique-intelligent-insights"></a>Unikatowy inteligentny wgląd w szczegółowe dane

Wraz ze wzrostem ilości i złożoności sygnałów zabezpieczeń, określenie, czy te sygnały są wiarygodnymi zagrożeniami, a następnie działające, trwa zbyt długo. Firma Microsoft oferuje niezrównaną szeroką skalę analizy zabezpieczeń, która została dostarczona w skali chmury, aby pomóc w szybkim wykrywaniu i korygowaniu zagrożeń. [Przeczytaj więcej](https://docs.microsoft.com/azure/security-center/security-center-intro)

## <a name="azure-threat-intelligence"></a>Analiza zagrożeń platformy Azure

Używając opcji Analiza zagrożeń dostępnej w usłudze Security Center, administratorzy IT mogą identyfikować zagrożenia dla bezpieczeństwa środowiska. Na przykład mogą zidentyfikować, czy określony komputer jest częścią botnetu. Komputery mogą stać się węzłami w botnecie, gdy osoby atakujące bezprawnie zainstalują złośliwe oprogramowanie, które potajemnie łączy komputer z centrum sterowania. Analiza zagrożeń może też identyfikować potencjalne zagrożenia pochodzące z tajnych kanałów komunikacji, takich jak podziemny Internet.

Aby umożliwić używanie analizy zagrożeń, usługa Security Center korzysta z danych, które pochodzą z wielu źródeł firmy Microsoft. Security Center używa tego do identyfikowania potencjalnych zagrożeń związanych ze środowiskiem. Okienko analiza zagrożeń składa się z trzech głównych opcji:

- Typy wykrytych zagrożeń
- Pochodzenie zagrożeń
- Mapa analizy zagrożeń

## <a name="machine-learning-in-azure-security-center"></a>Uczenie maszynowe w Azure Security Center

Azure Security Center głęboko analizuje wiele danych z różnych rozwiązań firmy Microsoft i partnerów, aby pomóc Ci w osiągnięciu większego poziomu zabezpieczeń. Aby móc korzystać z tych danych, firma wykorzystuje naukę o danych i uczenie maszynowe w celu zapobiegania zagrożeniom, wykrywania i ostatecznie dochodzenia.

Szeroko Azure Machine Learning pomaga osiągnąć dwa wyniki:

## <a name="next-generation-detection"></a>Wykrywanie nowej generacji

Osoby atakujące są coraz bardziej zautomatyzowane i zaawansowane. Wykorzystują one również naukę danych. Umożliwiają one odwracanie ochrony i systemów kompilacji, które obsługują mutacje w działaniu. Mogą one zamaskowane działania jako szum i szybko poznać błędy. Uczenie maszynowe pomaga nam odpowiedzieć na te zmiany.

## <a name="simplified-security-baseline"></a>Uproszczona linia bazowa zabezpieczeń

Podejmowanie efektywnych decyzji w zakresie bezpieczeństwa nie jest proste. Wymaga to bezpieczeństwa i doświadczenia. Chociaż niektóre duże organizacje mają takich ekspertów, nie są one dostępne w wielu firmach. Azure Machine Learning pozwala klientom na korzystanie z mądry innych organizacji podczas podejmowania decyzji o zabezpieczeniach.

## <a name="behavioral-analytics"></a>Analiza behawioralna

Analiza behawioralna to metoda, która polega na analizie danych i porównywaniu ich z kolekcją znanych wzorców. Wzorce te nie są jednak prostymi sygnaturami. Są one określane przez złożone algorytmy uczenia maszynowego, które są stosowane do dużych zestawów danych. Są one również określane przez specjalistów od analizy, którzy dokonują dokładnej analizy złośliwych zachowań. Azure Security Center może korzystać z analizy behawioralnej w celu identyfikowania zasobów narażonych na podstawie analizy dzienników maszyn wirtualnych, dzienników urządzeń sieci wirtualnej, dzienników sieci szkieletowej, zrzutów awaryjnych i innych źródeł.
