---
title: Funkcja zarządzania tożsamościami i kluczami w chmurze
description: Poznaj funkcje zarządzania tożsamościami i kluczami w chmurze.
author: JanetCThomas
ms.author: janet
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.topic: conceptual
ms.date: 05/15/2020
ms.openlocfilehash: bd98ff4e52faceea4c7dd48a2363efc5ebe87da2
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83755467"
---
# <a name="function-of-identity-and-key-management-in-the-cloud"></a>Funkcja zarządzania tożsamościami i kluczami w chmurze

Głównym celem zespołu ds. zabezpieczeń pracującego nad zarządzaniem tożsamości jest zapewnienie uwierzytelniania i autoryzacji ludzi, usług, urządzeń i aplikacji. Zarządzanie kluczami i certyfikatami zapewnia bezpieczną dystrybucję i dostęp do kluczowych materiałów do operacji kryptograficznych (które często obsługują podobne wyniki jako Zarządzanie tożsamościami).

## <a name="modernization"></a>Modernizacja

Tożsamość danych i modernizacja zarządzania kluczami są następujące:

- Dyscypliny zarządzania tożsamościami i certyfikatami są bliżej siebie, ponieważ zapewniają gwarancje związane z uwierzytelnianiem i autoryzacją w celu umożliwienia bezpiecznej komunikacji.
- Kontrolki tożsamości powstają jako podstawowy obwód zabezpieczeń dla aplikacji w chmurze
- Uwierzytelnianie oparte na kluczach dla usług w chmurze jest zastępowane zarządzaniem tożsamościami z powodu trudności z przechowywaniem i bezpiecznym dostępem do tych kluczy.
- Krytyczna ważność przeprowadzenia pozytywnych lekcji uzyskanych z lokalnych architektur tożsamości, takich jak pojedyncze tożsamości, logowanie jednokrotne (SSO) i natywna integracja aplikacji.
- Krytyczne znaczenie dla unikania częstych pomyłek w architekturze lokalnej, które często przenoszą ich złożoność, zapewniając trudność i trudności z pomocą techniczną. Należą do nich:
  - Grupy Sprawling i jednostki organizacyjne (OU).
  - Sprawling zbiór katalogów innych firm i systemów zarządzania tożsamościami.
  - Brak jasnej normalizacji i własności strategii tożsamości aplikacji.
- Ataki kradzieży poświadczeń pozostają w dużym wpływie i zagrożenie zagrożeniami.
- Konta usług i konta aplikacji pozostały największe wyzwanie, ale stają się łatwiejsze do rozwiązania. Zespoły tożsamości powinny aktywnie wykorzystywać możliwości chmury, które zaczynają rozwiązywać takie jak [tożsamości zarządzane usługi Azure AD](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview).

## <a name="team-composition-and-key-relationships"></a>Kompozycja zespołu i relacje między kluczami

Zespoły zarządzania tożsamościami i kluczami muszą tworzyć silne relacje z następującymi rolami:

- Architektura i operacje IT
- Architektura i operacje związane z zabezpieczeniami
- Zespoły programistyczne
- Zespoły ds. zabezpieczeń danych
- Zespoły ds. prywatności
- Zespoły prawne
- Zespoły zarządzania zgodnością/ryzykiem

## <a name="next-steps"></a>Następne kroki

Przegląd funkcji [zabezpieczeń infrastruktury i punktu końcowego](./cloud-security-infrastructure-endpoint.md)
