---
title: 'Wprowadzenie: udokumentowanie decyzji o wyrównaniu'
description: Zrozumienie i udokumentowanie początkowych decyzji wymaganych do przejazdu w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: ebcf336b72b91b8290b93fd16b5d1add709b8999
ms.sourcegitcommit: 5d6a7610e556f7b8ca69960ba76a3adfa9203ded
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2020
ms.locfileid: "83399705"
---
# <a name="get-started-understand-and-document-foundational-alignment-decisions"></a>Wprowadzenie: zrozumienie i udokumentowanie decyzji o wyrównaniu

Podróż wdrażania w chmurze umożliwia odblokowanie wielu korzyści firmowych, technicznych i organizacyjnych. Niezależnie od tego, co chcesz zrobić, jeśli podróż obejmuje chmurę, istnieje kilka pierwszych decyzji, które każdy zespół powinien zrozumieć. Podczas pracy w tym przewodniku należy zarejestrować te decyzje przy użyciu [wstępnego szablonu decyzji](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx). Szablon może pomóc szybko dołączać członków zespołu, którzy uczestniczą w cyklu życia wdrożenia chmury.

> [!NOTE]
> Wybranie dowolnego z poniższych linków może prowadzić do odbicia w spisie treści dla środowiska wdrażania Microsoft Cloud platformy Azure, co pozwala uzyskać podstawowe pojęcia, które będą używane później, aby pomóc zespołowi zaimplementować odpowiednie wskazówki. Utwórz zakładkę na tej stronie, aby często wrócić do tej listy kontrolnej.

## <a name="step-1-understand-how-azure-works"></a>Krok 1. zrozumienie, jak działa platforma Azure

Jeśli wybrano platformę Azure jako dostawcę chmury do obsługi kursu wdrożenia w chmurze, ważne jest, aby zrozumieć, [jak działa platforma Azure](./what-is-azure.md).

**Zespoły, elementy dostarczane i wskazówki pomocnicze:**

Wszyscy użytkownicy korzystający z rozwiązania do wdrażania w chmurze powinni mieć podstawową wiedzę na temat działania platformy Azure.

## <a name="step-2-understand-initial-azure-concepts"></a>Krok 2. zrozumienie początkowych koncepcji platformy Azure

Platforma Azure jest oparta na zestawie [podstawowych koncepcji](../ready/considerations/fundamental-concepts.md) , które są wymagane w przypadku głębokiej rozmowy dotyczącej strategii technicznej dla implementacji platformy Azure.

**Zespoły, elementy dostarczane i wskazówki pomocnicze:**

Wszyscy uczestnicy wdrożenia strategii technologicznej powinni zrozumieć warunki i definicje w podstawowych koncepcjach.

## <a name="step-3-review-the-portfolio"></a>Krok 3. przeglądanie portfolio

Niezależnie od tego, który dostawca usług w chmurze, wszystkie decyzje dotyczące hostingu w chmurze i środowiska są uruchamiane z zrozumieniem portfolio obciążeń. Struktura wdrażania w chmurze zawiera kilka narzędzi do poznania i oceniania portfolio.

**Dostarczane**

- Zanotuj lokalizację, stan i osobę odpowiedzialną za dokumentację portfolio w [początkowym szablonie decyzji](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- [Podstawowe pojęcia](../ready/considerations/fundamental-concepts.md) ułatwiają zrozumienie najważniejszych tematów platformy Azure przed rozpoczęciem wdrażania chmury.
- W celu uzyskania informacji o obciążeniach i zasobach, które zostały przeniesione do zespołu operacji w chmurze, należy zapoznać się ze [skoroszytem zarządzania operacjami](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/manage/opsmanagementworkbook.xlsx) i podejściem biznesowym.
- [Plan wdrażania w chmurze](../plan/plan-intro.md) zawiera zaległości dotyczące obciążeń i zasobów, które są styczeń do wdrożenia w chmurze.
- [Analiza cyfr cyfrowych](../digital-estate/approach.md) to podejście do dokumentowania istniejących obciążeń i zasobów, które są styczeń do wdrożenia w chmurze. Na platformie Azure symbol cyfrowy jest najlepiej reprezentowany w narzędziu o nazwie [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-support-matrix).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół strategii chmury jest odpowiedzialny za definiowanie sposobu wyświetlania portfolio. | <li> Aby można było utworzyć te widoki, wiele zespołów będzie korzystać z poniższych wskazówek. Wszyscy zainteresowani wdrożeniem chmury powinni wiedzieć, gdzie znaleźć widok portfolio, aby obsłużyć decyzje w dalszej części tego procesu. |

## <a name="step-4-define-portfolio-hierarchy-depth-to-align-the-portfolio"></a>Krok 4. Definiowanie głębokości hierarchii portfolio w celu wyrównania portfolio

Zasoby hostingu i obciążenia w chmurze mogą być proste, składające się z pojedynczego obciążenia i jego zasobów pomocniczych. W przypadku innych klientów strategia wdrażania chmury może obejmować tysiące obciążeń i wiele bardziej dodatkowych zasobów. Hierarchia portfolio zawiera wspólne nazwy poszczególnych poziomów, które ułatwiają tworzenie wspólnego języka dla organizacji, niezależnie od dostawcy chmury.

**Dostarczane**

- Zapisz odpowiednie potrzeby hierarchii w [początkowym szablonie decyzji](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Zapoznaj się z poziomami [hierarchii portfolio](../reference/fundamental-concepts/hosting-hierarchy.md) , aby wyrównać podstawowe warunki.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, wymuszanie i automatyzowanie hierarchii portfolio w celu kształtowania zasad firmowych w chmurze. | <li> Wszyscy użytkownicy mający strategię techniczną dotyczącą wdrażania chmury powinni znać hierarchię portfolio i poziomy używanej hierarchii. |

## <a name="step-5-establish-a-naming-and-tagging-standard-across-the-portfolio"></a>Krok 5. ustalenie standardu nazewnictwa i znakowania w portfolio

Wszystkie istniejące obciążenia i zasoby powinny być prawidłowo nazwane i oznaczone jako zgodne ze standardem nazewnictwa i znakiem. Te standardy powinny być udokumentowane i dostępne jako odniesienia dla wszystkich członków zespołu. Jeśli to możliwe, standardy powinny być również automatycznie wymuszane w celu zapewnienia minimalnych wymagań dotyczących tagowania.

**Dostarczane**

- Zanotuj lokalizację, stan i stronę konta dla skoroszytu nazewnictwa i Konwencji tagowania w [początkowym szablonie decyzji](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Utwórz [Standard nazewnictwa i znakowanie](../ready/azure-best-practices/naming-and-tagging.md).
- Wypełnij [skoroszyt nazewnictwa i Konwencji tagowania](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx) , aby śledzić decyzje.
- [Przejrzyj i zaktualizuj istniejące Tagi na platformie Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources).
- [Wymuszaj zasady tagowania na platformie Azure](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-policies).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, wymuszanie i automatyzowanie standardów nazewnictwa i tagowania, aby zapewnić spójność w portfolio. | <li> Wszyscy użytkownicy mający strategię techniczną dotyczącą wdrażania w chmurze powinni mieć przed wdrożeniem w chmurze wzorce nazewnictwa i znakowania. |

## <a name="step-6-create-a-resource-organization-design-to-implement-the-portfolio-hierarchy"></a>Krok 6. Tworzenie projektu organizacji zasobów w celu zaimplementowania hierarchii portfolio

Aby zapewnić spójne wyrównanie z decyzjami hierarchii portfolio, należy utworzyć projekt dla organizacji zasobów. Taki projekt umożliwia wyrównania narzędzi organizacyjnych od dostawcy chmury z hierarchią portfela wymaganą do obsługi planu wdrożenia chmury. Ten projekt przeprowadzi implementację, wyjaśniając, które zasoby można wdrożyć w określonych granicach w środowiskach chmurowych.

**Dostarczane**

- Mapuj produkty platformy Azure na wyrównany poziom hierarchii portfolio w [początkowym szablonie decyzji](https://raw.githubusercontent.com/Microsoft/CloudAdoptionFramework/master/references/initial-decisions-checklist.docx).

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Dowiedz [się, jak produkty platformy Azure obsługują hierarchię portfolio](../reference/fundamental-concepts/hierarchy-azure-tools.md).
- Przejrzyj istniejące subskrypcje, aby wyrównać wyrównanie do wybranej hierarchii portfolio.

Tworzenie strategii subskrypcji:

- Zacznij od [dwóch subskrypcji według projektu](../ready/azure-best-practices/initial-subscriptions.md). Dodaj podstawowe projekty subskrypcji, aby uwzględnić typowe potrzeby przedsiębiorstwa, takie jak usługi udostępnione lub subskrypcje piaskownicy.
- [Zarządzaj wieloma subskrypcjami](../ready/azure-best-practices/organize-subscriptions.md) , ponieważ do obsługi planu wdrażania chmury są wymagane dodatkowe subskrypcje.
- Ustanów [jasne granice na podstawie hierarchii portfolio](../reference/fundamental-concepts/hierarchy-azure-tools.md#organizing-the-hierarchy-in-azure).
- W razie potrzeby [Przenieś grupy zasobów i zasoby między subskrypcjami](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription) , aby przestrzegać strategii organizacji.

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. zarządzania chmurą jest odpowiedzialny za Definiowanie, implementowanie i Automatyzowanie projektu organizacji zasobów w ramach portfolio. | <li> Wszyscy użytkownicy mający strategię techniczną dotyczącą wdrażania chmury powinni znać projekt organizacji zasobów przed wdrożeniem w chmurze. |

## <a name="step-7-map-capabilities-teams-and-raci-to-fundamental-concepts"></a>Krok 7. mapowanie możliwości, zespołów i RACI na podstawowe koncepcje

Złożoność hierarchii portfolio pomoże w poinformowaniu o strukturach i metodologiach organizacyjnych w celu zaplanowania codziennych działań różnych zespołów.

**Dostarczane**

- Wypełnij przewodniki wprowadzenie do wyrównania organizacyjnego w oparciu o te koncepcje.

<!-- docsTest:ignore "Get started: Align your organization" -->

**Wskazówki dotyczące uzupełniania elementów dostarczanych:**

- Skorzystaj z wcześniejszych kroków jako przewodnika, aby oszacować [wskazówki dotyczące odpowiedzialności w hierarchii portfolio](../reference/fundamental-concepts/hosting-hierarchy.md#hierarchy-accountability-and-guidance). Określ, które możliwości muszą być dostarczane przez dedykowane organizacje lub zespoły wirtualne.
- Użyj [Rozpocznij: Wyrównaj swoją organizację](./org-alignment.md) , aby zastosować wskazówki dotyczące odpowiedzialności w hierarchii portfolio do Raci (odpowiedzialnych, do których można się skontaktować, które są świadome i poinformowane).

<!-- markdownlint-disable MD033 -->
<br>

| Zespół odpowiedzialny za | Osoby odpowiedzialne i wspierające |
| --- | --- |
| <li> Zespół ds. strategii chmury jest odpowiedzialny za wyrównywanie wirtualnych lub dedykowanych struktur organizacyjnych w celu zapewnienia sukcesu cyklu wdrożenia chmury. | <li> Wszyscy pracownicy korzystający z wdrożenia chmury powinni mieć zaznajomienie się z wyrównaniem osób i poziomów odpowiedzialności. |

## <a name="whats-next"></a>Co dalej

Kompiluj ten zestaw podstawowych koncepcji, korzystając z serii przewodników rozpoczynających pracę w tej części struktury wdrażania w chmurze.

> [!div class="nextstepaction"]
> [Zastosuj podstawowe koncepcje do innych przewodników rozpoczynających pracę](./index.md)
