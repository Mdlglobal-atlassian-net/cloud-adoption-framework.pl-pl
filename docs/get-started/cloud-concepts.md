---
title: 'Wprowadzenie: udokumentowanie decyzji o wyrównaniu'
description: Zrozumienie i udokumentowanie początkowych decyzji wymaganych do przejazdu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: 0c59a383f47629dd16cd81bc6865812fcaca4679
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83229810"
---
<!-- docsTest:ignore CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template -->

# <a name="get-started-understand-and-document-foundational-alignment-decisions"></a>Wprowadzenie: zrozumienie i udokumentowanie decyzji o wyrównaniu

Podróż wdrażanie w chmurze umożliwia odblokowanie wielu korzyści firmowych, technicznych i organizacyjnych za pomocą różnych podróży. Niezależnie od tego, co chcesz zrobić, jeśli podróż obejmuje chmurę, istnieje kilka pierwszych decyzji, które powinny być zrozumiałe dla każdego zaangażowanego zespołu. Podczas pracy w tym przewodniku należy zarejestrować te decyzje przy użyciu [wstępnego szablonu decyzji](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx) , aby szybko dołączać członków zespołu, którzy uczestniczą w ogólnym cyklu wdrażania usługi Cloud.

> [!NOTE]
> Kliknięcie dowolnego z poniższych kroków spowoduje przełączenie się do spisu treści struktury wdrażania chmury, aby uwzględnić podstawowe koncepcje, które są używane później, aby pomóc zespołowi zaimplementować odpowiednie wskazówki. Utwórz zakładkę na tej stronie, aby często wrócić do tej listy kontrolnej.

## <a name="step-1-understand-how-azure-works"></a>Krok 1. zrozumienie, jak działa platforma Azure

Jeśli wybrano platformę Azure jako dostawcę chmury do obsługi kursu wdrożenia w chmurze, ważne jest, aby zrozumieć, [jak działa platforma Azure](./what-is-azure.md).

**Zespoły, elementy dostarczane i wskazówki pomocnicze:**

Wszystkie osoby korzystające z cyklu wdrażania w chmurze powinny mieć podstawowe informacje na temat działania platformy Azure.

## <a name="step-2-understand-initial-azure-concepts"></a>Krok 2. zrozumienie początkowych koncepcji platformy Azure

Platforma Azure jest oparta na zestawie [podstawowych koncepcji](../ready/considerations/fundamental-concepts.md) , które są wymagane do uzyskania głębokiej rozmowy dotyczącej strategii technicznej w odniesieniu do implementacji platformy Azure.

**Zespoły, elementy dostarczane i wskazówki pomocnicze:**

Wszystkie osoby należące do wdrożenia platformy Azure w ramach strategii technologicznej powinny zrozumieć warunki i definicje w podstawowych koncepcjach.

## <a name="step-3-review-the-portfolio"></a>Krok 3. przeglądanie portfolio

Niezależnie od wybranego dostawcy chmury, wszystkie decyzje dotyczące hostingu w chmurze i środowiska są uruchamiane z uwzględnieniem ogólnego portfela obciążeń. Struktura wdrażania chmury obejmuje kilka narzędzi do poznania i oceniania portfolio.

**Dostarczane**

- Zanotuj lokalizację, stan i osobę odpowiedzialną za dokumentację portfolio w [początkowym szablonie decyzji](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Podstawowe pojęcia](../ready/considerations/fundamental-concepts.md) ułatwiają zrozumienie najważniejszych tematów platformy Azure przed rozpoczęciem wdrażania chmury.
- W celu uzyskania pomocy dotyczącej obciążeń i zasobów, które zostały przeniesione do zespołu operacji w chmurze, można uzyskać informacje o skoroszycie i wyrównaniu [zarządzania operacjami](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/manage/opsmanagementworkbook.xlsx) biznesowymi.
- [Plan wdrażania w chmurze](../plan/plan-intro.md) zawiera zaległości dotyczące obciążeń i zasobów, które są styczeń do wdrożenia w chmurze.
- [Analiza cyfr cyfrowych](../digital-estate/approach.md) to podejście do dokumentowania istniejących obciążeń i zasobów, które są styczeń do wdrożenia w chmurze. Na platformie Azure symbol cyfrowy jest najlepiej reprezentowany w narzędziu o nazwie [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-support-matrix).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury jest odpowiedzialny za definiowanie sposobu wyświetlania portfolio. | <li> Aby można było utworzyć te widoki, wiele zespołów będzie korzystać z poniższych wskazówek. Wszyscy osoby mające zastosowanie w chmurze powinni wiedzieć, gdzie znaleźć widok portfolio, aby wspierać decyzje w dalszej części tego procesu. |

## <a name="step-4-define-portfolio-hierarchy-depth-to-align-the-portfolio"></a>Krok 4. Definiowanie głębokości hierarchii portfolio w celu wyrównania portfolio

Zasoby hostingu i obciążenia w chmurze mogą być proste, składające się z pojedynczego obciążenia i jego zasobów pomocniczych. W przypadku innych klientów strategia wdrażania chmury może obejmować tysiące obciążeń i wiele bardziej dodatkowych zasobów. Hierarchia portfolio zawiera podstawowe nazwy poszczególnych poziomów hierarchii, które ułatwiają tworzenie wspólnego języka dla organizacji, niezależnie od dostawcy chmury.

**Dostarczane**

- Zapisz odpowiednie potrzeby hierarchii w [początkowym szablonie decyzji](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z poziomami [hierarchii portfolio](../reference/fundamental-concepts/hosting-hierarchy.md) , aby wyrównać podstawowe warunki.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, wymuszanie i automatyzowanie hierarchii portfolio w celu kształtowania zasad firmowych w chmurze. | <li> Wszyscy użytkownicy, którzy korzystają z strategii technicznej dotyczącej rozwiązań w chmurze, powinni znać hierarchię portfolio i poziomy używanej hierarchii. |

## <a name="step-5-establish-a-naming-and-tagging-standard-across-the-portfolio"></a>Krok 5. ustalenie standardu nazewnictwa i znakowania w portfolio

Wszystkie istniejące obciążenia i zasoby powinny być prawidłowo nazwane i oznaczone jako zgodne ze standardem nazewnictwa i znakiem. Te standardy powinny być udokumentowane i dostępne jako odniesienia dla wszystkich członków zespołu. Jeśli to możliwe, standardy powinny być również automatycznie wymuszane w celu zapewnienia minimalnych wymagań dotyczących tagowania.

**Dostarczane**

- Zanotuj lokalizację, stan i stronę z kontami dla skoroszytu nazewnictwa i standardów tagowania w [początkowym szablonie decyzji](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Utwórz [Standard nazewnictwa i znakowanie](../ready/azure-best-practices/naming-and-tagging.md).
- Wypełnij [skoroszyt śledzenia konwencji nazewnictwa i tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) , aby śledzić decyzje.
- [Przejrzyj i zaktualizuj istniejące Tagi na platformie Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).
- [Wymuszaj zasady tagowania na platformie Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-policies).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, wymuszanie i automatyzowanie standardów nazewnictwa i tagowania, aby zapewnić spójność w portfolio. | <li> Przed wdrożeniem w chmurze wszystkie osoby, które brały w strategii technicznej dotyczącej rozwiązań w chmurze, powinny zapoznać się ze standardami nazewnictwa i znakowania. |

## <a name="step-6-create-a-resource-organization-design-to-implement-the-portfolio-hierarchy"></a>Krok 6. Tworzenie projektu organizacji zasobów w celu zaimplementowania hierarchii portfolio

Aby zapewnić spójne wyrównanie z decyzjami hierarchii portfolio, należy utworzyć projekt dla organizacji zasobów. Taki projekt umożliwia wyrównania narzędzi organizacyjnych od dostawcy chmury z hierarchią portfolio wymaganą do obsługi planu wdrożenia chmury. Ten projekt przeprowadzi implementację, wyjaśniając, które zasoby można wdrożyć w określonych granicach w środowiskach chmurowych.

**Dostarczane**

- Mapuj produkty platformy Azure na wyrównany poziom hierarchii portfolio w [początkowym szablonie decyzji](https://raw.githubusercontent.com/microsoft/cloudadoptionframework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Dowiedz [się, jak produkty platformy Azure obsługują hierarchię portfolio](../reference/fundamental-concepts/hierarchy-azure-tools.md).
- Przejrzyj istniejące subskrypcje, aby wyrównać wyrównanie do wybranej hierarchii portfolio.

Tworzenie strategii subskrypcji:

- Zacznij od [dwóch subskrypcji według projektu](../ready/azure-best-practices/initial-subscriptions.md).
  - Dodaj podstawowe projekty subskrypcji, aby uwzględnić typowe potrzeby przedsiębiorstwa, takie jak usługi udostępnione lub subskrypcje piaskownicy.
- [Zarządzaj wieloma subskrypcjami](../ready/azure-best-practices/organize-subscriptions.md) , ponieważ do obsługi planu wdrażania chmury są wymagane dodatkowe subskrypcje.
- Ustanów [jasne granice na podstawie hierarchii portfolio](../reference/fundamental-concepts/hierarchy-azure-tools.md#organizing-the-hierarchy-in-azure).
- W razie potrzeby [Przenieś grupy zasobów i zasoby między subskrypcjami](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription) , aby przestrzegać strategii organizacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, implementowanie i Automatyzowanie projektu organizacji zasobów w ramach portfolio. | <li> Przed wdrożeniem w chmurze wszyscy użytkownicy, którzy zapoznają się z strategią techniczną dotyczącą wdrażania w chmurze, powinni zapoznać się z projektem organizacji zasobów. |

## <a name="step-7-map-capabilities-teams-and-raci-to-fundamental-concepts"></a>Krok 7. mapowanie możliwości, zespołów i RACI na podstawowe koncepcje

Złożoność hierarchii portfolio pomoże w poinformowaniu o strukturach i metodologiach organizacyjnych w celu zaplanowania codziennych działań różnych zespołów.

**Dostarczane**

- Wypełnij przewodniki wprowadzenie do wyrównania organizacyjnego na podstawie tych podstawowych koncepcji.

<!-- docsTest:ignore Get Align -->

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Aby określić, które możliwości muszą być dostarczane przez dedykowane organizacje lub zespoły wirtualne, należy użyć wcześniejszych kroków jako [wskazówki](../reference/fundamental-concepts/hosting-hierarchy.md#hierarchy-accountability-and-guidance).
- Użyj [Rozpocznij: Wyrównaj swoją organizację](./org-alignment.md) , aby zastosować wskazówki dotyczące odpowiedzialności w hierarchii portfolio do diagramu Raci.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury jest odpowiedzialny za wyrównywanie wirtualnych lub dedykowanych struktur organizacyjnych w celu zapewnienia sukcesu ogólnego wdrożenia chmury. | <li> Wszystkie osoby uczestniczące w cyklu życia w chmurze powinny mieć zaznajomienie się z wyrównaniem osób i poziomów odpowiedzialności. |

## <a name="whats-next"></a>Co dalej

Kompiluj ten zestaw podstawowych koncepcji, korzystając z serii przewodników rozpoczynających pracę w tej części struktury wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Zastosuj podstawowe koncepcje do innych przewodników wprowadzających](./index.md)
