---
title: Przewodnik po decyzjach dotyczących nazewnictwa i tagowania zasobów
description: Dowiedz się więcej o podejściach do nazewnictwa i tagowania oraz odpowiednich opcjach związanych z organizowaniem zasobów w chmurze w ramach przewodnika Cloud Adoption Framework dla platformy Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 2865f9a7ceb6d20828e76ad4da3a7ae5ebd81ba3
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83753489"
---
<!-- cSpell:ignore catalogsearch northamerica jsmith contactalias catsearchowners businessprocess businessimpact revenueimpact -->

# <a name="resource-naming-and-tagging-decision-guide"></a>Przewodnik po decyzjach dotyczących nazewnictwa i tagowania zasobów

Organizowanie zasobów opartych na chmurze jest najważniejszym zadaniem działu IT, chyba że obsługujesz tylko proste wdrożenia. Użyj standardów nazewnictwa i tagowania, aby uporządkować zasoby z następujących powodów:

- **Zarządzanie zasobami:** zespoły IT muszą móc szybko znajdować zasoby skojarzone z konkretnymi obciążeniami, środowiskami, grupami własności albo innymi ważnymi informacjami. Organizowanie zasobów ma krytyczne znaczenie w przypadku przypisywania ról organizacyjnych oraz uprawnień dostępu na potrzeby zarządzania zasobami.
- **Zarządzanie kosztami i ich optymalizacja:** informowanie grup biznesowych o użyciu zasobów w chmurze wymaga, aby dział IT wiedział, z których zasobów i obciążeń korzystają poszczególne zespoły. Tagi powiązane z kosztami obsługują następujące tematy:

  - [Modele księgowania kosztów w chmurze](../../strategy/cloud-accounting.md)
  - [Obliczenia zwrotu z inwestycji](../../strategy/financial-models.md#return-on-investment)
  - [Śledzenie kosztów](../../ready/azure-best-practices/track-costs.md)
  - [Budżety](https://docs.microsoft.com/azure/cost-management-billing/costs/tutorial-acm-create-budgets?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Alerty](https://docs.microsoft.com/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?toc=/azure/cloud-adoption-framework/toc.json&bc=/azure/cloud-adoption-framework/_bread/toc.json)
  - [Cykliczne śledzenie i raportowanie wydatków](../../govern/cost-management/compliance-processes.md)
  - [Optymalizacje po implementacji](../../govern/cost-management/discipline-improvement.md#operate-and-post-implementation)
  - [Taktyki optymalizacji kosztów](../../govern/guides/complex/cost-management-improvement.md#incremental-improvement-of-the-best-practices)
- **Zarządzanie operacjami:** Widoczność dla zespołu ds. zarządzania operacjami w zakresie zobowiązań biznesowych i umów SLA jest ważnym aspektem bieżących operacji. Aby była dobrze zarządzana, konieczne jest tagowanie [znaczenia krytycznego dla misji](../../manage/considerations/criticality.md).
- **Bezpieczeństwo:** Klasyfikacja danych i wpływ na bezpieczeństwo to istotny punkt danych dla zespołu, gdy pojawią się naruszenia lub inne problemy związane z bezpieczeństwem. Aby można było bezpiecznie pracować, wymagane jest tagowanie określające [klasyfikację danych](../../govern/policy-compliance/data-classification.md).
- **Ład i zgodność z przepisami:** Utrzymanie spójności między zasobami pomaga zidentyfikować odchylenia od uzgodnionych zasad. [W tym artykule dotyczącym podstaw ładu](../../govern/guides/complex/prescriptive-guidance.md#resource-tagging) pokazano, w jaki sposób jeden z poniższych wzorców może pomóc przy wdrażaniu praktyk ładu. Dostępne są podobne wzorce do oceny zgodności z przepisami za pomocą tagów.
- **Automatyzacja:** oprócz tworzenia zasobów, którymi dział IT może łatwiej zarządzać, prawidłowy schemat organizacyjny pozwala na korzystanie z zalet automatyzacji jako części tworzenia zasobu, monitorowania operacji i tworzenia procesów metodyki DevOps.
- **Optymalizacja obciążenia:** Tagowanie może pomóc zidentyfikować wzorce i rozwiązać ogólne problemy. Tag może także ułatwić zidentyfikowanie zasobów wymaganych do obsługi pojedynczego obciążenia. Tagowanie wszystkich zasobów związanych z poszczególnymi obciążeniami pozwala na dokładniejszą analizę obciążeń o kluczowym znaczeniu w celu podjęcia trafnych decyzji dotyczących architektury.

## <a name="tagging-decision-guide"></a>Przewodnik po decyzjach związanych z tagowaniem

![Wykres opcji tagowania od najmniej do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-resource-tagging.png)

Idź do: [Konwencje nazewnictwa punktów odniesienia](#baseline-naming-conventions) | [Wzorce tagowania wzorców](#resource-tagging-patterns) | [Dowiedz się więcej](#learn-more)

Podejście do tagowania może być proste lub złożone, z naciskiem na różne elementy: od wspierania zespołów IT zarządzających obciążeniami w chmurze do integrowania informacji odnoszących się do wszystkich aspektów działalności biznesowej.

Zastosowanie przez dział IT podejścia skoncentrowanego na tagowaniu, takiego jak tagowanie oparte na obciążeniu, aplikacji, funkcji lub środowisku, znacznie zmniejsza złożoność procesu monitorowania zasobów i upraszcza podejmowanie decyzji dotyczących zarządzania na podstawie wymagań operacyjnych.

Schematy tagowania, które są skoncentrowane na działalności biznesowej, takie jak księgowość, własność firmy lub stopień krytyczności dla działania firm, mogą wymagać zainwestowania dłuższego czasu podczas tworzenia standardów tagowania, które odzwierciedlają zainteresowania firmy, oraz obsługi tych standardów wraz z upływem czasu. Dzięki tej inwestycji powstaje system tagowania, który zapewnia lepszą księgowość kosztów i wartości zasobów IT dla całej firmy. To skojarzenie wartości biznesowej zasobu z jego kosztami operacyjnymi jest jednym z pierwszych kroków zmieniania sposobu postrzegania centrum kosztu infrastruktury IT w szerszej organizacji.

## <a name="baseline-naming-conventions"></a>Konwencje nazewnictwa punktów odniesienia

Standardowa konwencja nazewnictwa to punkt wyjścia do organizowania zasobów hostowanych w chmurze. Prawidłowo ustrukturyzowany system nazw pozwala szybko identyfikować zasoby na potrzeby zarządzania i księgowości. Jeśli w innych częściach organizacji istnieją konwencje nazewnictwa IT, należy zastanowić się, czy konwencje nazewnictwa w chmurze mają być z nimi zgodne, czy też trzeba ustanowić odrębne standardy oparte na chmurze.

> [!NOTE]
> [Reguły i ograniczenia nazewnictwa](https://docs.microsoft.com/azure/azure-resource-manager/management/resource-name-rules) są różne dla różnych zasobów platformy Azure. Konwencje nazewnictwa muszą być zgodne z tymi regułami.

## <a name="resource-tagging-patterns"></a>Wzorce tagowania zasobów

W przypadku organizacji bardziej zaawansowanej niż mogłaby obsłużyć tylko prosta konwencja nazewnictwa platformy w chmurze obsługują możliwość tagowania zasobów.

Tagi to elementy metadanych dołączone do zasobów. Tagi składają się z pary ciągów klucz/wartość. Wartości do uwzględnienia w tych parach zależą od Ciebie, ale zastosowanie spójnego zestawu tagów globalnych jako części kompleksowych zasad nazewnictwa i tagowania to kluczowy element ogólnych zasad dotyczących ładu.

W ramach procesu planowania użyj poniższych pytań, aby ułatwić określenie rodzaju informacji, które muszą obsługiwać tagi zasobów:

- Czy zasady nazewnictwa i tagowania trzeba zintegrować z istniejącymi zasadami nazewnictwa i zasadami organizacyjnymi w firmie?
- Czy będzie wdrażany system księgowy z obciążeniem zwrotnym lub przewidywaniem kosztów? Czy trzeba skojarzyć zasoby z informacjami księgowymi dla działów, grup biznesowych i zespołów na poziomie bardziej szczegółowym niż pozwala na to prosty podział na poziomie subskrypcji?
- Czy tagowanie musi reprezentować szczegóły, takie jak wymagania dotyczące zgodności z regulacjami prawnymi dla zasobu? Co zrobić ze szczegółami operacyjnymi, takimi jak wymagania dotyczące czasu pracy, harmonogramy poprawek lub wymagania dotyczące zabezpieczeń?
- Jakie tagi będą wymagane w przypadku wszystkich zasobów w oparciu o centralne zasady IT? Jakie tagi będą opcjonalne? Czy poszczególne zespoły mogą implementować własne niestandardowe schematy tagowania?

Typowe wzorce tagowania wymienione poniżej przedstawiają przykłady organizowania zasobów w chmurze przy użyciu tagowania. Te wzorce nie są przeznaczone do stosowania wyłącznego i można ich używać w sposób równoległy, co zapewni wiele sposobów organizowania zasobów zgodnie z potrzebami firmy.

<!-- markdownlint-disable MD033 -->
<!-- docsTest:disable -->

| Typ tagu | Przykłady | Opis |
|-----|-----|-----|
| Funkcjonalny | app&nbsp;=&nbsp;catalogsearch1 <br> tier&nbsp;=&nbsp;web <br> webserver&nbsp;=&nbsp;apache <br> env&nbsp;=&nbsp;prod <br> env&nbsp;=&nbsp;staging <br> env&nbsp;=&nbsp;dev | Kategoryzuje zasoby na podstawie ich przeznaczenia w ramach obciążenia, środowiska, w którym zostały wdrożone, albo innych szczegółów funkcji lub operacji. |
| Klasyfikacja | confidentiality&nbsp;=&nbsp;private <br> SLA&nbsp;=&nbsp;24hours | Klasyfikuje zasób według sposobu jego użycia i zastosowanych wobec niego zasad. |
| Księgowość | department&nbsp;=&nbsp;finance <br> program&nbsp;=&nbsp;business-initiative <br> region&nbsp;=&nbsp;northamerica | Umożliwia skojarzenie zasobu z określonymi grupami w organizacji na potrzeby rozliczeń. |
| Partnerstwo | owner&nbsp;=&nbsp;jsmith <br> contactalias&nbsp;=&nbsp;catsearchowners <br> stakeholders&nbsp;=&nbsp;user1;user2;user3 | Udostępnia informacje o osobach (poza działem IT), które są związane z zasobem lub na które zasób wpływa w inny sposób. |
| Przeznaczenie | businessprocess&nbsp;=&nbsp;support <br> businessimpact&nbsp;=&nbsp;moderate <br> revenueimpact&nbsp;=&nbsp;high | Dopasowuje zasoby do funkcji biznesowych w celu lepszego wsparcia decyzji inwestycyjnych. |

<!-- docsTest:enable -->
<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat nazewnictwa i tagowania na platformie Azure, zobacz:

- [Konwencje nazewnictwa dla zasobów platformy Azure](../../ready/azure-best-practices/naming-and-tagging.md). Te wskazówki dotyczą zalecanych konwencji nazewnictwa zasobów platformy Azure.
- [Organizowanie zasobów platformy Azure i hierarchii zarządzania przy użyciu tagów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources). Tagi można stosować na platformie Azure na poziomie grupy zasobów i indywidualnego zasobu, co zapewnia elastyczność określania stopnia szczegółowości dowolnych raportów księgowych w oparciu o zastosowane tagi.

## <a name="next-steps"></a>Następne kroki

Tagowanie zasobów to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
