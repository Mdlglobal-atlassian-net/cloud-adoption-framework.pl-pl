---
title: Przewodnik po decyzjach dotyczących nazewnictwa i tagowania zasobów
description: Dowiedz się więcej o podejściach do nazewnictwa i tagowania oraz odpowiednich opcjach związanych z organizowaniem zasobów w chmurze w ramach przewodnika Cloud Adoption Framework dla platformy Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 475b9e944188384a72cb3b8670a1ff607e7895f6
ms.sourcegitcommit: 388e32dd4861039149c846c926c0e9230cf28ae3
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/12/2020
ms.locfileid: "79140409"
---
<!-- cSpell:ignore catalogsearch northamerica jsmith contactalias catsearchowners businessprocess businessimpact revenueimpact -->

# <a name="resource-naming-and-tagging-decision-guide"></a>Przewodnik po decyzjach dotyczących nazewnictwa i tagowania zasobów

Organizowanie zasobów opartych na chmurze jest jednym z najważniejszych zadań działu IT, chyba że obsługujesz tylko proste wdrożenia. Organizowanie zasobów służy trzem podstawowym celom:

- **Zarządzanie zasobami:** zespoły IT muszą szybko znaleźć zasoby skojarzone z konkretnymi obciążeniami, środowiskami, grupami własności albo innymi ważnymi informacjami. Organizowanie zasobów ma krytyczne znaczenie w przypadku przypisywania ról organizacyjnych oraz uprawnień dostępu na potrzeby zarządzania zasobami.
- **Automatyzacja:** oprócz tworzenia zasobów, którymi dział IT może łatwiej zarządzać, prawidłowy schemat organizacyjny pozwala na korzystanie z zalet automatyzacji jako części tworzenia zasobu, monitorowania operacji i tworzenia procesów metodyki DevOps.
- **Księgowość:** informowanie grup biznesowych o użyciu zasobów w chmurze wymaga, aby dział IT wiedział, których zasobów używają określone obciążenia i zespoły. Aby obsługiwać metody, takie jak księgowanie z użyciem obciążenia zwrotnego i przewidywania kosztów, zasoby w chmurze należy zorganizować tak, aby odzwierciedlały własność i użycie.

## <a name="tagging-decision-guide"></a>Przewodnik po decyzjach związanych z tagowaniem

![Wykres opcji tagowania od najprostszych do najbardziej złożonych, powiązany z hiperlinkami poniżej](../../_images/decision-guides/decision-guide-resource-tagging.png)

Idź do: [Konwencje nazewnictwa punktów odniesienia](#baseline-naming-conventions) | [Wzorce tagowania wzorców](#resource-tagging-patterns) | [Dowiedz się więcej](#learn-more)

Podejście do tagowania może być proste lub złożone, z naciskiem na różne elementy: od wspierania zespołów IT zarządzających obciążeniami w chmurze do integrowania informacji odnoszących się do wszystkich aspektów działalności biznesowej.

Jeśli dział IT zastosuje podejście skoncentrowane na tagowaniu, takie jak tagowanie oparte na obciążeniu, funkcji lub środowisku, spowoduje to znacznie łatwiejsze zredukowanie stopnia złożoności procesu monitorowania zasobów i podejmowania decyzji dotyczących zarządzania na podstawie wymagań operacyjnych.

Schematy tagowania, które są skoncentrowane na działalności biznesowej, takie jak księgowość, własność firmy lub stopień krytyczności dla działania firm, mogą wymagać zainwestowania dłuższego czasu podczas tworzenia standardów tagowania, które odzwierciedlają zainteresowania firmy, oraz obsługi tych standardów wraz z upływem czasu. Jednak wynikiem tego procesu jest system tagowania zapewniający ulepszoną możliwość uwzględniania kosztów i wartości zasobów IT w ramach ogólnej działalności firmy. To skojarzenie wartości biznesowej zasobu z jego kosztami operacyjnymi jest jednym z pierwszych kroków zmieniania sposobu postrzegania centrum kosztu infrastruktury IT w szerszej organizacji.

## <a name="baseline-naming-conventions"></a>Konwencje nazewnictwa punktów odniesienia

Standardowa konwencja nazewnictwa to punkt wyjścia do organizowania zasobów hostowanych w chmurze. Prawidłowo ustrukturyzowany system nazw pozwala szybko identyfikować zasoby na potrzeby zarządzania i księgowości. Jeśli w innych częściach organizacji istnieją konwencje nazewnictwa IT, należy zastanowić się, czy konwencje nazewnictwa w chmurze mają być z nimi zgodne, czy też trzeba ustanowić odrębne standardy oparte na chmurze.

Należy również zauważyć, że różne typy zasobów platformy Azure mają różne [wymagania w zakresie nazewnictwa](../../ready/azure-best-practices/naming-and-tagging.md). Konwencje nazewnictwa muszą być zgodne z tymi wymaganiami dotyczącymi nazewnictwa.

## <a name="resource-tagging-patterns"></a>Wzorce tagowania zasobów

W przypadku organizacji bardziej zaawansowanej niż mogłaby obsłużyć tylko prosta konwencja nazewnictwa platformy w chmurze obsługują możliwość tagowania zasobów.

*Tagi* to elementy metadanych dołączone do zasobów. Tagi składają się z pary ciągów klucz/wartość. Wartości do uwzględnienia w tych parach zależą od Ciebie, ale zastosowanie spójnego zestawu tagów globalnych jako części kompleksowych zasad nazewnictwa i tagowania to kluczowy element ogólnych zasad dotyczących ładu.

W ramach procesu planowania użyj poniższych pytań, aby ułatwić określenie rodzaju informacji, które muszą obsługiwać tagi zasobów:

- Czy zasady nazewnictwa i tagowania trzeba zintegrować z istniejącymi zasadami nazewnictwa i zasadami organizacyjnymi w firmie?
- Czy będzie wdrażany system księgowy z obciążeniem zwrotnym lub przewidywaniem kosztów? Czy trzeba skojarzyć zasoby z informacjami księgowymi dla działów, grup biznesowych i zespołów na poziomie bardziej szczegółowym niż pozwala na to prosty podział na poziomie subskrypcji?
- Czy tagowanie musi reprezentować szczegóły, takie jak wymagania dotyczące zgodności z regulacjami prawnymi dla zasobu? Co zrobić ze szczegółami operacyjnymi, takimi jak wymagania dotyczące czasu pracy, harmonogramy poprawek lub wymagania dotyczące zabezpieczeń?
- Jakie tagi będą wymagane w przypadku wszystkich zasobów w oparciu o centralne zasady IT? Jakie tagi będą opcjonalne? Czy poszczególne zespoły mogą implementować własne niestandardowe schematy tagowania?

Typowe wzorce tagowania wymienione poniżej przedstawiają przykłady organizowania zasobów w chmurze przy użyciu tagowania. Te wzorce nie są przeznaczone do stosowania wyłącznego i można ich używać w sposób równoległy, co zapewni wiele sposobów organizowania zasobów zgodnie z potrzebami firmy.

<!-- markdownlint-disable MD033 -->

| Typ tagu | Przykłady | Opis |
|-----|-----|-----|
| Funkcjonalny            | app = catalogsearch1 <br/>tier = web <br/>webserver = apache<br/>env = prod <br/>env = staging <br/>env = dev                 | Kategoryzuje zasoby na podstawie ich przeznaczenia w ramach obciążenia, środowiska, w którym zostały wdrożone, albo innych szczegółów funkcji lub operacji.                                 |
| Klasyfikacja        | confidentiality=private<br/>sla = 24hours                                 | Klasyfikuje zasób według sposobu jego użycia i zastosowanych wobec niego zasad                               |
| Księgowość            | department = finance <br/>project = catalogsearch <br/>region = northamerica | Umożliwia kojarzenie zasobów z określonymi grupami w organizacji na potrzeby rozliczeń |
| Partnerstwo           | owner = jsmith <br/>contactalias = catsearchowners<br/>stakeholders = user1;user2;user3<br/>                       | Udostępnia informacje o osobach (poza działem IT), które są związane z zasobem lub na które zasób wpływa w inny sposób                      |
| Przeznaczenie               | businessprocess=support<br/>businessimpact=moderate<br/>revenueimpact=high   | Dopasowuje zasoby do funkcji biznesowych w celu podejmowania lepszych decyzji inwestycyjnych dotyczących obsługi  |

<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji na temat nazewnictwa i tagowania na platformie Azure, zobacz:

- [Konwencje nazewnictwa dla zasobów platformy Azure](https://docs.microsoft.com/azure/architecture/best-practices/resource-naming). Te wskazówki dotyczą zalecanych konwencji nazewnictwa zasobów platformy Azure.
- [Organizowanie zasobów platformy Azure przy użyciu tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags). Tagi można stosować na platformie Azure na poziomie grupy zasobów i indywidualnego zasobu, co zapewnia elastyczność określania stopnia szczegółowości dowolnych raportów księgowych w oparciu o zastosowane tagi.

## <a name="next-steps"></a>Następne kroki

Tagowanie zasobów to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Przejdź do [omówienia przewodników dotyczących podejmowania decyzji](../index.md), aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury.

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
