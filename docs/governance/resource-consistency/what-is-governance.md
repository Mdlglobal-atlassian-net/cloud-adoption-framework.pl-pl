---
title: Co to jest nadzór nad zasobami w chmurze?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wyjaśnienie zarządzania zasobami w chmurze na platformie Azure
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: a72213a1ad72ce2df14add3e36b276b58b75485e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70826344"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-resource-governance"></a>Co to jest nadzór nad zasobami w chmurze?

W [jaki sposób platforma Azure działa?](../../getting-started/what-is-azure.md), wiesz, że platforma Azure to zbiór serwerów i sprzętu sieciowego, na których działa zwirtualizowany sprzęt i oprogramowanie w imieniu użytkowników. System Azure umożliwia tworzenie, odczytywanie, aktualizowanie i usuwanie zasobów w organizacji, dzięki czemu można łatwo tworzyć, odczytywać, aktualizować i usuwać zasoby zgodnie z potrzebami.

Mimo że nieograniczone do zasobów może sprawiać, że deweloperzy są bardziej elastyczni, mogą również prowadzić do nieoczekiwanych kosztów. Na przykład zespół programistyczny może zostać zatwierdzony do wdrożenia zestawu zasobów do testowania, ale zapomina o ich usunięciu po zakończeniu testowania. Te zasoby będą nadal naliczane koszty nawet wtedy, gdy nie są już zatwierdzone lub wymagane.

Rozwiązaniem jest zarządzanie dostępem do zasobów. **Zarządzanie to** ciągły proces zarządzania, monitorowania i inspekcji użycia zasobów platformy Azure w celu spełnienia celów i wymagań organizacji.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94]

<!-- markdownlint-enable MD034 -->

Te wymagania są unikatowe dla każdej organizacji, więc podejście jednokrotne pasuje do ładu nie jest pomocne. Zamiast tego można zaprojektować model ładu przy użyciu dwóch podstawowych narzędzi ładu platformy Azure: **kontroli dostępu opartej na rolach (RBAC)** i **zasad dotyczących zasobów**.

RBAC definiuje role i role definiują operacje dozwolone dla każdego użytkownika przypisanego do tej roli. Na przykład rola **właściciela** zezwala na wszystkie operacje (tworzenie, odczytywanie, aktualizowanie i usuwanie) zasobu, podczas gdy rola **czytelnik** zezwala tylko na operacje odczytu. Role mogą być definiowane w szerokim zakresie i stosowane do wielu typów zasobów lub zdefiniowane bardziej wąskie i stosowane do zaledwie kilku typów zasobów.

Zasady zasobów definiują reguły tworzenia zasobów. Na przykład zasady zasobów mogą ograniczyć jednostkę SKU maszyny wirtualnej do określonego, zatwierdzonego rozmiaru. Inne zasady zasobów mogą wymusić zastosowanie znacznika dla przypisanego centrum kosztu, gdy zostanie wysłane żądanie utworzenia zasobu.

Podczas konfigurowania tych narzędzi ważne jest, aby zrównoważyć zarządzanie i elastyczność organizacyjną. Im bardziej restrykcyjne zasady zarządzania, tym mniej Agile deweloperzy i pracownicy IT. Restrykcyjne zasady zarządzania mogą wymagać dalszych czynności ręcznych, takich jak wymaganie od programisty wypełnienia formularza lub wysłania wiadomości e-mail do członka zespołu nadzoru w celu ręcznego utworzenia zasobu. Zespół nadzoru ma ograniczone zdolności produkcyjne i może stać się wąskim gardłem, dzięki czemu zespoły programistyczne czekają na nieproduktywne tworzenie zasobów lub niewykorzystane zasoby naliczają koszty przed ich usunięciem.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy rozumiesz koncepcję zarządzania zasobami w chmurze, Dowiedz się więcej na temat zarządzania dostępem do zasobów na platformie Azure.

> [!div class="nextstepaction"]
> [Informacje o dostępie do zasobów na platformie Azure](./azure-resource-access.md)
