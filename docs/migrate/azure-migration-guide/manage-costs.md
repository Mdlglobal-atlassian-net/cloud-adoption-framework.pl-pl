---
title: Mechanizmy kontroli kosztów skoncentrowane na migracji
description: Dowiedz się, jak interpretować faktury oraz konfigurować budżety i płatności dotyczące zasobów platformy Azure przy użyciu podręcznika Cloud Adoption Framework dla platformy Azure.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 0ce3b5ee28983851e97c10360cf6707b4e3c17d1
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83214518"
---
<!-- cSpell:ignore bandersmsft -->

# <a name="migration-focused-cost-control-mechanisms"></a>Mechanizmy kontroli kosztów skoncentrowane na migracji

Chmura wprowadza kilka zmian w sposobie pracy, niezależnie od naszej roli w zespole technicznym. Koszty stanowią doskonały przykład tej zmiany. Dawniej tylko kadra kierownicza działu finansowego i informatycznego zajmowała się kosztami zasobów informatycznych (infrastruktury, aplikacji i danych). Chmura umożliwia każdemu członkowi działu informatycznego podejmowanie decyzji, które lepiej wspierają użytkownika końcowego, oraz działanie w oparciu o nie. Jednak takie możliwości wiążą się z odpowiedzialnością za świadome podejmowanie decyzji w zakresie kosztów.

W tym artykule przedstawiono narzędzia, które mogą ułatwić podejmowanie mądrych decyzji w zakresie kosztów przed migracją na platformę Azure, w jej trakcie oraz po niej.

W tym artykule mowa o następujących narzędziach:

> - Azure Migrate
> - Kalkulator cen platformy Azure
> - Kalkulator całkowitego kosztu posiadania platformy Azure
> - Azure Cost Management
> - Azure Advisor

Procesy opisane w tym artykule mogą wymagać współpracy z kierownikami działów informatycznych, z działem finansowym lub z właścicielami aplikacji biznesowych.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migration"></a>[Szacowanie kosztów maszyn wirtualnych przed migracją](#tab/EstimateVMCosts)

Przed migracją dowolnego zasobu (infrastruktury, aplikacji lub danych) istnieje możliwość oszacowania kosztów i dostosowania rozmiaru w oparciu o zaobserwowane kryteria wydajności dla tych zasobów. Szacowanie kosztów służy do dwóch celów: umożliwia kontrolę kosztów i zapewnia punkt kontrolny, aby zagwarantować, że bieżące budżety spełniają niezbędne wymagania w zakresie wydajności.

## <a name="cost-calculators"></a>Kalkulatory kosztów

W przypadku ręcznych obliczeń kosztów istnieją dwa przydatne kalkulatory, które umożliwiają szybkie oszacowanie kosztów w oparciu o architekturę obciążenia, które ma zostać zmigrowane.

- [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator) umożliwia szacowanie kosztów wybranych produktów platformy Azure.
- Czasami podjęcie decyzji wymaga porównania przyszłych kosztów chmury z bieżącymi kosztami lokalnymi. [Kalkulator całkowitego kosztu posiadania (TCO)](https://azure.microsoft.com/pricing/tco/calculator) takie porównanie umożliwia.

Te ręczne kalkulatory kosztów mogą być używane niezależnie do prognozowania potencjalnych wydatków i oszczędności. Mogą one być również używane razem z narzędziami do prognozowania kosztów usługi Azure Migrate w celu dostosowania oczekiwań związanych z kosztami w taki sposób, aby dopasować je do alternatywnych architektur lub ograniczeń wydajności.

## <a name="azure-migrate-calculations"></a>Obliczenia w usłudze Azure Migrate

**Wymagania wstępne:** W pozostałej części tej karty założono, że czytelnik wypełnił już usługę Azure Migrate przy użyciu kolekcji zasobów przeznaczonych do migracji (infrastrukturą, aplikacjami i danymi). Poprzedni artykuł na temat ocen zawiera instrukcje dotyczące zbierania danych początkowych. Po wypełnieniu danych wykonaj kolejne kroki, aby oszacować miesięczne koszty na podstawie zebranych danych.

Usługa Azure Migrate oblicza **szacunkowe koszty miesięczne** na podstawie danych przechwytywanych przez moduł zbierający i mapę usług. W poniższych krokach opisano ładowanie szacunkowych kosztów:

1. Przejdź do obszaru Ocena usługi Azure Migrate w portalu.
1. Na stronie **Omówienie** projektu wybierz pozycję **+Utwórz ocenę**.
1. Wybierz pozycję **Wyświetl wszystko**, aby sprawdzić właściwości oceny.
1. Utwórz grupę i określ jej nazwę.
1. Wybierz maszyny wirtualne, które chcesz dodać do grupy.
1. Wybierz pozycję **Utwórz ocenę**, aby utworzyć grupę i ocenę.
1. Po utworzeniu oceny możesz ją wyświetlić w obszarze Omówienie > Pulpit nawigacyjny.
1. W sekcji „Szczegóły oceny” w okienku nawigacji portalu wybierz pozycję **Szczegóły kosztów**.

Przedstawiony poniżej otrzymany wynik szacunkowy obejmuje miesięczne koszty obliczania i magazynu, które często stanowią największą część kosztów związanych z chmurą.

![Widok Szczegóły kosztów](./media/manage-costs/compute-storage-monthly-cost-estimate.png)

_Rysunek 1. Obraz przedstawiający widok Szczegóły kosztów oceny w usłudze Azure Migrate._

## <a name="additional-resources"></a>Zasoby dodatkowe

- [Konfiguracja i przegląd oceny w usłudze Azure Migrate](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- Aby zapoznać się z bardziej szczegółowym planem zarządzania kosztami dla większej liczby zasobów (infrastruktury, aplikacji i danych), zobacz temat dotyczący [modelu zarządzania w strukturze Cloud Adoption Framework](../../govern/guides/index.md). Przeczytaj zwłaszcza wskazówki dotyczące [dyscypliny w usłudze Cost Management](../../govern/cost-management/index.md) oraz [ulepszania usługi Cost Management w przewodniku dotyczącym ładu dla złożonych przedsiębiorstw](../../govern/guides/complex/cost-management-improvement.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migration"></a>[Szacowanie i optymalizowanie kosztów maszyn wirtualnych podczas migracji i po niej](#tab/EstimateOptimize)

Oszacowanie kosztów przed migracją ułatwia osiągnięcie celu związanego z oczekiwaniami w zakresie kosztów. Zapewnia również możliwość przeanalizowania wydajności i potrzeb związanych z kosztami poszczególnych zasobów do zmigrowania (infrastruktury, aplikacji i danych). Jest to jednak nadal tylko oszacowanie. Gdy zasób zostanie zmigrowany i obciążony, można przeprowadzić dokładniejsze obliczenia kosztów na podstawie rzeczywistego lub zsyntetyzowanego obciążenia.

## <a name="azure-advisor-cost-recommendations"></a>Zalecenia dotyczące kosztów w usłudze Azure Advisor

W ciągu 24 godzin od zmigrowania zasobów (infrastruktury, aplikacji i danych) na platformę Azure usługa Azure Advisor zaczyna monitorować wydajność poszczególnych zasobów, aby przekazać użytkownikowi opinię na temat danego zasobu. Jedna przekazana opinia dotyczy proporcji między kosztami oraz wykorzystaniem.

W poniższych krokach przedstawiono zalecenia dotyczące kosztów dla zasobów (infrastruktury, aplikacji i danych) w ramach bieżących subskrypcji:

1. Przejdź do obszaru **Azure Advisor** w portalu. W tym celu wybierz pozycję **Advisor** w lewym okienku nawigacji w witrynie Azure Portal. Jeśli pozycja Advisor w lewym okienku nie będzie widoczna, wybierz pozycję **Wszystkie usługi**. W okienku menu usługi w obszarze **Monitorowanie i zarządzanie** wybierz pozycję **Advisor**.
2. Na pulpicie nawigacyjnym usługi Advisor zostanie wyświetlone podsumowanie zaleceń dla wszystkich wybranych subskrypcji. Możesz wybrać subskrypcje, do których mają być wyświetlane zalecenia, przy użyciu listy rozwijanej filtru subskrypcji.
3. Aby wyświetlić zalecenia dotyczące kosztów, wybierz kartę Koszty.

## <a name="azure-cost-management"></a>Azure Cost Management

Usługa Azure Cost Management może zapewnić bardziej całościowe podsumowanie nawyków związanych z wydatkami, w tym szczegółowe podsumowanie kosztów i trendów związanych z wydatkami w czasie. W przypadku dużych lub złożonych migracji podsumowanie to może zawierać szczegółowe informacje potrzebne do podejmowania ogólnych decyzji w zakresie zarządzania dużymi kosztami.

Wymagania wstępne: W pozostałej części karty założono, że czytelnik zakończył konfigurację usługi Azure Cost Management podczas zapoznawania się z przewodnikiem dotyczącym konfiguracji platformy Azure. Aby uzyskać więcej informacji na temat konfigurowania usługi Azure Cost Management, zobacz [Zarządzanie kosztami i rozliczeniami dla zasobów platformy Azure](../../ready/azure-setup-guide/manage-costs.md) w przewodniku konfiguracji platformy Azure. Po wypełnieniu danych wykonaj kolejne kroki, aby oszacować miesięczne koszty na podstawie zebranych danych.

W poniższych krokach opisano ładowanie danych analizy kosztów w usłudze Azure Cost Management dla subskrypcji:

1. Przejdź do obszaru **Zarządzanie kosztami i rozliczenia** w portalu. Jeśli w lewym okienku pozycja Zarządzanie kosztami i rozliczenia nie jest widoczna, wybierz pozycję **Wszystkie usługi**. W okienku menu usługi w obszarze **Monitorowanie i zarządzanie** wybierz pozycję **Zarządzanie kosztami i rozliczenia**.
2. W obszarze Zarządzanie kosztami i rozliczenia wybierz pozycję **Zarządzanie kosztami** w lewym okienku nawigacji, aby rozpocząć analizowanie i optymalizowanie kosztów chmury.
3. W obszarze Zarządzanie kosztami wybierz pozycję **Analiza kosztów**.
    1. Użyj kapsułki **Zakres**, aby przełączyć na inny zakres w analizie kosztów.

Ta analiza umożliwi przegląd łącznego kosztu, budżetu (jeśli jest dostępny) i kosztów skumulowanych. Każde obliczenie może być wyświetlane według usługi, zasobu oraz w czasie. Co ważne, koszty mogą być analizowane według tagów. Prawidłowe nazewnictwo i tagowanie zasobów (infrastruktury, aplikacji i danych) stanowi punkt wyjścia dla wszystkich procesów zarządzania dźwiękiem i kosztami. Odpowiednie tagi umożliwiają lepsze zarządzanie kosztami i wyraźniejszy wpływ optymalizacji wydajności i kosztów.

## <a name="additional-resources"></a>Zasoby dodatkowe

- Aby zapoznać się z bardziej szczegółowym planem zarządzania kosztami dla większej liczby zasobów (infrastruktury, aplikacji i danych), zobacz temat dotyczący [modelu zarządzania w strukturze Cloud Adoption Framework](../../govern/guides/index.md). Przeczytaj zwłaszcza wskazówki dotyczące [dyscypliny w usłudze Cost Management](../../govern/cost-management/index.md) oraz [przyrostowego ulepszania usługi Cost Management w przewodniku dotyczącym ładu dla złożonych przedsiębiorstw](../../govern/guides/complex/cost-management-improvement.md).
- Aby uzyskać więcej informacji na temat usługi Azure Advisor, zobacz temat [Reducing service costs using Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) (Obniżanie kosztów usług przy użyciu Azure Advisor).
- Aby uzyskać więcej informacji na temat usługi Azure Cost Management, zobacz tematy [Understand and work with scopes](https://docs.microsoft.com/azure/cost-management/understand-work-scopes) (Zapoznanie się z zakresami i praca z nimi) oraz [Explore and analyze costs with Cost Analysis](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis) (Poznawanie i analizowanie kosztów za pomocą funkcji analizy kosztów — Szybki start).

# <a name="tips-and-tricks-to-optimize-costs"></a>[Porady i wskazówki dotyczące optymalizacji kosztów](#tab/TipsTricks)

Poza narzędziami wymienionymi w tym artykule istnieją pewne porady i wskazówki, które mogą pomóc szybko obniżyć koszty ogólne chmury. Poniżej przedstawiono kilka porad wysokiego poziomu, z którymi warto się zapoznać:

## <a name="avoid-unnecessary-spending"></a>Unikaj zbędnych wydatków

Większość zasobów (infrastruktura, aplikacje i dane) w istniejącym centrum danych można teoretycznie zmigrować do chmury. Nie oznacza to jednak, że należy to zrobić. Podczas oceniania poszczególnych obciążeń upewnij się, czy obciążenie powinno być migrowane. Artykuł dotyczący struktury Cloud Adoption Framework poświęcony [racjonalizacji przyrostowej](../../digital-estate/rationalize.md) może pomóc w ustaleniu, które zasoby powinny być migrowane.

## <a name="reduce-waste"></a>Ogranicz marnotrawstwo

Po wdrożeniu infrastruktury na platformie Azure ważne jest, aby upewnić się, że jest ona używana. Najprostszą metodą, aby natychmiast rozpocząć oszczędności jest przejrzenie zasobów i usunięcie wszystkich, które nie są używane.

## <a name="reduce-overprovisioning"></a>Ogranicz nadmierne udostępnianie

Nawet w przypadku najlepszych metod szacowania istnieje możliwość wystąpienia nadmiernego udostępniania zasobów (infrastruktury, aplikacji i danych) oraz ich niewystarczającego wykorzystania. Przegląd tych zasobów przy użyciu narzędzi z wcześniejszych dwóch kart pozwoli zidentyfikować potencjalne metody ograniczenia rozmiaru zasobów, aby lepiej dostosować wymagania wydajności i ograniczyć koszty.

## <a name="take-advantage-of-available-discounts"></a>Skorzystaj z dostępnych rabatów

Skontaktuj się z przedstawicielem swojego konta Microsoft, aby dowiedzieć się, jak skorzystać z bieżących opcji rabatu. Poniżej przedstawiono kilka przykładów rabatów często używanych do obniżenia kosztów.

## <a name="azure-reservations"></a>Rezerwacje platformy Azure

[Rezerwacje platformy Azure](https://docs.microsoft.com/azure/cost-management-billing/reservations/save-compute-costs-reservations) umożliwiają przedpłatę za pojemność obliczeniową maszyn wirtualnych lub usługi SQL Database za rok lub trzy lata. Przedpłaty umożliwiają uzyskanie rabatu na używane zasoby. Rezerwacje mogą znacząco obniżyć koszty obliczeniowe maszyny wirtualnej lub usługi SQL Database, do 72% względem płatności zgodnie z rzeczywistym użyciem w przypadku zobowiązania do zapłaty z góry za jeden rok lub trzy lata. Rezerwacje umożliwiają skorzystanie z rabatu na rozliczenia i nie mają wpływu na stan środowiska uruchomieniowego maszyn wirtualnych lub baz danych SQL.

## <a name="use-azure-hybrid-benefit"></a>Korzystaj z zalet użycia hybrydowego platformy Azure

Jeśli masz już licencje na system Windows Server lub program SQL Server w ramach wdrożeń lokalnych, możesz użyć programu [Korzyść użycia hybrydowego platformy Azure](https://azure.microsoft.com/pricing/hybrid-benefit) i oszczędzać na platformie Azure. W przypadku korzystania z systemu Windows Server każda licencja obejmuje koszt systemu operacyjnego (na maksymalnie dwóch maszynach wirtualnych), a Ty ponosisz tylko koszty według podstawowej stawki obliczeniowej. Możesz korzystać z istniejących licencji na program SQL Server, aby zaoszczędzić do 55% na opcjach usługi SQL Database opartych na rdzeniach wirtualnych. Opcje obejmują program SQL Server w usłudze Azure Virtual Machines i usługę SQL Server Integration Services.

## <a name="low-priority-vms-with-batch"></a>Maszyny wirtualne o niskim priorytecie z usługą Batch

W przypadku procesów w tle o niższym priorytecie usługa Batch oferuje możliwość zarządzania maszynami wirtualnymi usługi w tle oraz obniżenia kosztów. Jednak przed wybraniem tej opcji z rabatem ważne jest, by poznać wpływ na wydajność [maszyn wirtualnych o niskim priorytecie z usługą Batch](https://docs.microsoft.com/azure/batch/batch-low-pri-vms).

## <a name="additional-resources"></a>Zasoby dodatkowe

Aby zapoznać się z bardziej szczegółowym planem zarządzania kosztami dla większej liczby zasobów (infrastruktury, aplikacji i danych), zobacz temat dotyczący [modelu zarządzania w strukturze Cloud Adoption Framework](../../govern/guides/index.md). Przeczytaj zwłaszcza wskazówki dotyczące [dyscypliny w usłudze Cost Management](../../govern/cost-management/index.md) oraz [przyrostowych ulepszeń usługi Cost Management w przewodniku dotyczącym ładu dla złożonych przedsiębiorstw](../../govern/guides/complex/cost-management-improvement.md).
