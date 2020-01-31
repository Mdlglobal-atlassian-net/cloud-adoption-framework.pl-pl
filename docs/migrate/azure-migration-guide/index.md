---
title: Wprowadzenie do przewodnika migracji na platformę Azure
description: Dowiedz się, jak skutecznie wykonać migrację usług organizacji na platformę Azure, korzystając ze szczegółowych wskazówek.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 6f5592c93bb78b14a85e37ffa67ffea697a12345
ms.sourcegitcommit: 2362fb3154a91aa421224ffdb2cc632d982b129b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/28/2020
ms.locfileid: "76807040"
---
::: zone target="docs"

# <a name="azure-migration-guide-before-you-start"></a>Przewodnik po migracji na platformę Azure: Przed rozpoczęciem

::: zone-end

::: zone target="chromeless"

# <a name="before-you-start"></a>Przed rozpoczęciem

::: zone-end

Przed przeprowadzeniem migracji zasobów na platformę Azure musisz wybrać metodę migracji i funkcje, których będziesz używać do zabezpieczania środowiska i zarządzania nim. Ten przewodnik poprowadzi Cię przez ten proces podejmowania decyzji.

::: zone target="docs"

> [!TIP]
> Aby zapoznać się z tym przewodnikiem w środowisku interaktywnym, skorzystaj z witryny Azure Portal. Przejdź do [centrum przewodników Szybki start platformy Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) w witrynie Azure Portal, wybierz pozycję **Migrowanie swojego środowiska na platformę Azure**, a następnie postępuj zgodnie z instrukcjami krok po kroku.

::: zone-end

# <a name="overviewtaboverview"></a>[Omówienie](#tab/Overview)

W tym przewodniku przedstawiono podstawowe informacje na temat migrowania aplikacji i zasobów ze środowiska lokalnego na platformę Azure. Jest on przeznaczony dla zakresów migracji o minimalnej złożoności. Aby określić przydatność tego przewodnika dla Twojej migracji, zobacz kartę **Kiedy należy korzystać z tego przewodnika**.

Podczas migracji na platformę Azure można zmigrować aplikacje w niezmienionej postaci przy użyciu rozwiązań maszyn wirtualnych IaaS (nazywane jest to _ponownym hostowaniem_ lub migracją metodą _lift and shift_) albo skorzystać z możliwości użycia usług zarządzanych i innych natywnych funkcji chmury w celu zmodernizowania aplikacji. Zobacz kartę **Opcje migracji**, aby uzyskać więcej informacji na temat tych możliwości. Opracowując strategię migracji, warto rozważyć następujące zagadnienia:

- Czy migrowane aplikacje będą działać w chmurze?
- Jaka jest najlepsza strategia (w odniesieniu do technologii, narzędzi i migracji) dla mojej aplikacji? Zobacz [Przewodnik po decyzjach dotyczących narzędzi do migracji](../../decision-guides/migrate-decision-guide/index.md) dla modelu Microsoft Cloud Adoption Framework, aby uzyskać więcej informacji.
- Jak mogę skrócić czas przestoju podczas migracji?
- Jak mogę kontrolować koszty?
- Jak mogę śledzić koszty zasobów i odpowiednio je rozliczać?
- Jak mogę zapewnić zachowanie zgodności z wymaganiami i przepisami?
- Jak mogę spełnić wymagania prawne dotyczące niezależności danych obowiązujące w niektórych krajach?

Ten przewodnik pomaga odpowiedzieć na te pytania. Zawiera sugerowane zadania i funkcje, które należy wziąć pod uwagę podczas przygotowań do wdrożenia zasobów na platformie Azure, w tym:

> [!div class="checklist"]
>
> - **Konfigurowanie wymagań wstępnych.** Zaplanuj migrację i przygotuj się do niej.
> - **Ocena dopasowania pod względem technicznym.** Sprawdź gotowość techniczną i możliwości migracji.
> - **Zarządzanie kosztami i rozliczeniami.** Sprawdź koszty swoich zasobów.
> - **Migrowanie usług.** Wykonaj faktyczną migrację.
> - **Organizowanie zasobów.** Zablokuj zasoby o krytycznym znaczeniu dla swojego systemu i otaguj zasoby w celu ich śledzenia.
> - **Optymalizowanie i przekształcanie.** Skorzystaj z możliwości przejrzenia zasobów po migracji.
> - **Zabezpieczenia i zarządzanie.** Upewnij się, że Twoje środowisko jest bezpieczne i właściwie monitorowane.
> - **Uzyskiwanie pomocy.** Korzystaj z pomocy i obsługi technicznej podczas wykonywania czynności związanych z migracją lub po migracji.

::: zone target="docs"

Aby dowiedzieć się więcej na temat organizowania i tworzenia struktury subskrypcji, zarządzania wdrożonymi zasobami i zapewniania zgodności z wymaganiami dotyczącymi zasad przedsiębiorstwa, zobacz temat [Ład na platformie Azure](https://docs.microsoft.com/azure/security/governance-in-azure).

::: zone-end

# <a name="when-to-use-this-guidetabwhentousethisguide"></a>[Kiedy należy korzystać z tego przewodnika](#tab/WhenToUseThisGuide)

Narzędzia omówione w tym przewodniku obsługują szeroką gamę scenariuszy migracji, jednak w tym przewodniku skupiono się na ograniczonym nakładzie pracy przy _minimalnej złożoności_. Aby określić, czy ten przewodnik migracji jest odpowiedni dla Twojego projektu, zastanów się, czy następujące warunki mają zastosowanie w Twoim przypadku:

- Wykonujesz migrację do homogenicznego środowiska.
- Do wykonania migracji wymagane jest dopasowanie tylko kilku jednostek biznesowych.
- Nie planujesz automatyzacji całej migracji.
- Migrujesz niewielką liczbę serwerów.
- Mapowanie zależności składników do zmigrowania można łatwo zdefiniować.
- Twoja branża ma minimalne wymagania prawne dotyczące tej migracji.

Jeśli którykolwiek z tych warunków _nie ma_ zastosowania w Twojej sytuacji, zamiast tego należy rozważyć skorzystanie z [przewodnika o rozszerzonym zakresie](../expanded-scope/index.md). Zalecamy również zgłoszenie się po pomoc do jednego z naszych zespołów Microsoft lub partnerów w przypadku wykonywania migracji wymagających przewodnika o rozszerzonym zakresie. Klienci, którzy kontaktują się z firmą Microsoft lub certyfikowanymi partnerami, odnoszą większy sukces w tych scenariuszach. Więcej informacji na temat uzyskiwania pomocy zawiera ten przewodnik.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Aby uzyskać więcej informacji, zobacz:

- [Przewodnik o rozszerzonym zakresie](../expanded-scope/index.md)

::: zone-end

# <a name="migration-optionstabmigrationoptions"></a>[Opcje migracji](#tab/MigrationOptions)

Migrację do chmury można przeprowadzić na kilka sposobów. Niektóre są lepiej dopasowane do różnych scenariuszy niż inne. Określając sposób migracji środowiska, należy wziąć pod uwagę następujące opcje podczas podejmowania decyzji dotyczącej strategii migracji:

- **Ponowne hostowanie:** Ponowne hostowanie, znane również jako metoda „lift and shift”, polega na przeniesieniu bieżącego stanu na platformę Azure przy minimalnych zmianach w ogólnej architekturze.
- **Refaktoryzacja:** Opcje typu platforma jako usługa (PaaS) mogą zmniejszyć koszty operacyjne powiązane z wieloma aplikacjami. Rozsądnym rozwiązaniem może być nieznaczna refaktoryzacja aplikacji w celu jej dostosowania do modelu PaaS. Dotyczy to również refaktoryzacji kodu w ramach procesu programowania w celu zapewnienia nowych możliwości biznesowych aplikacji.
- **Zmiana architektury:** Niektóre starzejące się aplikacje nie są zgodne z dostawcami usług w chmurze z względu na decyzje dotyczące architektury podjęte podczas tworzenia aplikacji. W takich przypadkach może być konieczna zmiana architektury aplikacji w ramach migracji.
- **Przebudowa:** W niektórych scenariuszach zmiany wymagane do zmigrowania aplikacji mogą być zbyt duże, aby móc uzasadnić dalsze inwestycje, i konieczna jest przebudowa rozwiązania.
- **Zastąpienie:** Rozwiązania są zwykle wdrażane przy użyciu najlepszych technologii i technik dostępnych w danym czasie. W niektórych przypadkach nowoczesne aplikacje typu „oprogramowanie jako usługa” (SaaS) mogą zapewniać wszystkie funkcje udostępniane przez aplikacją hostowaną. W tych scenariuszach można zaplanować zastąpienie obciążenia w przyszłości i z tego względu nie uwzględniać go w rozważaniach na temat migracji.

::: zone target="chromeless"

Te metody nie wykluczają się wzajemnie &mdash; na przykład mimo że podczas początkowej migracji mógł zostać zastosowany model **ponownego hostowania**, można wdrożyć **refaktoryzację** lub **zmianę architektury** jako część fazy optymalizacji po migracji. Omówiono to również w części **Optymalizowanie i przekształcanie** tego przewodnika.

::: zone-end

::: zone target="docs"

Te metody nie wykluczają się wzajemnie &mdash; na przykład mimo że podczas początkowej migracji mógł zostać zastosowany model **ponownego hostowania**, można wdrożyć **refaktoryzację** lub **zmianę architektury** jako część fazy optymalizacji po migracji. Omówiono to również w części [Optymalizowanie i przekształcanie](./optimize-and-transform.md) tego przewodnika.

::: zone-end

![Grafika informacyjna dotycząca opcji migracji](../../_images/migrate/migration-options.png)
