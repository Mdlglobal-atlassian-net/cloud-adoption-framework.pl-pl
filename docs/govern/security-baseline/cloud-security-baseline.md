---
title: Informacje o linii bazowej zabezpieczeń chmury
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Dowiedz się więcej o linii bazowej zabezpieczeń w chmurze.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dfb7969d19017c003ef961c18e87b8cb110ccd4e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/16/2019
ms.locfileid: "71028872"
---
# <a name="understand-the-cloud-security-baseline"></a>Informacje o linii bazowej zabezpieczeń chmury

Ten artykuł wprowadzający znajduje się w ogólnym temacie planu bazowego zabezpieczeń w chmurze, który kompiluje [pięć dyscyplin nadzoru chmurowego](../governance-disciplines.md) w celu ustanowienia struktury zarządzania. Bardziej szczegółowe informacje o zabezpieczeniach w chmurze są dostępne w [ramach zaufanej chmury platformy Azure](https://azure.microsoft.com/overview/trusted-cloud). Podejścia do ulepszania organizacji Security stan można znaleźć w [katalogu usługi zabezpieczeń w chmurze](https://www.microsoft.com/security/information-protection)

> [!NOTE]
> Ten artykuł nie powinien zapewniać wystarczającego kontekstu, aby umożliwić czytelnikowi wdrożenie strategii zabezpieczeń. Jest to tylko ogólna świadomość.

## <a name="cloud-security"></a>Bezpieczeństwo chmury

Zabezpieczenia w chmurze to rozszerzenie tradycyjnych praktyk bezpieczeństwa informacji. Tradycyjne zabezpieczenia INFORMATYCZNe obejmują zasady i kontrole dotyczące zabezpieczeń komputera, zabezpieczeń sieci, ochrony danych, użycia informacji i tak dalej. Te same zasady i kontrolki są zbędne w chmurze. Podczas przekształceń w chmurze jest konieczne, aby CISO aktywnie angażować się i zrozumieć poziom chmury w celu zapewnienia, że starsze zasady IT są mapowane na odpowiednie poziomy kontroli w chmurze.

Co więcej, Każda strategia zabezpieczeń w chmurze powinna uwzględniać następujące tematy:

- **Klasyfikowanie danych.** Właściwa Klasyfikacja danych w celu zrozumienia wszelkich źródeł danych, które są prywatne, chronione lub wysoce poufne. Pomoże to zarządzać ryzykiem podczas planowania.
- **Planowanie scenariusza chmury hybrydowej.** Zrozumienie, jak starsze sieci lokalne będą łączyć się z chmurą, pomoże CISO identyfikować i korygować zagrożenia.
- **Zaplanuj ataki i błędy.** W ciągu pierwszych kilku miesięcy transformacji nastąpi błędy w miarę zdobywania zespołu. Zacznij od małych zagrożeń i wysoce ograniczonych wdrożeń, aby bezpiecznie się zapoznać.
- **Określanie priorytetów prywatności.** W całej transformacji cały zespół powinien mieć świadomość prywatności klientów i pracowników. Twoje dane są bezpieczne w chmurze, ale zespół powinien mieć świadomość i zachować ostrożność podczas pracy z danymi poufnymi.

## <a name="protecting-data-and-privacy"></a>Ochrona danych i prywatności

W przypadku organizacji w całym&mdash;świecie, niezależnie od tego, czy przedsiębiorstwa,&mdash;organizacje niedochodowe lub firmy w chmurze, stały się częścią ich trwającej strategii IT. Usługi Cloud Services zapewniają organizacjom o wszystkich rozmiarach dostęp do praktycznie nieograniczonego magazynu danych przy zwalnianiu ich z konieczności zakupu, obsługi i aktualizowania własnych sieci i systemów komputerowych. Dostawcy usług w chmurze firmy Microsoft i innych dostawców oferują infrastrukturę IT, platformę i oprogramowanie jako usługę (SaaS), dzięki czemu klienci mogą szybko skalować w górę lub w dół w miarę potrzeb i płacić tylko za moc obliczeniową i używane przez nich magazyn.

Jednak w miarę jak organizacje nadal korzystają z zalet usług w chmurze, takich jak zwiększone wybór, elastyczność i elastyczność przy jednoczesnym zwiększeniu wydajności i obniżeniu kosztów IT, muszą rozważyć, jak wprowadzenie usług w chmurze wpływa na ich prywatność, bezpieczeństwo i zgodność stan. Firma Microsoft pracowała nad nieskalowalnością, niezawodnością i zarządzaniem ofertami w chmurze, ale również w celu zapewnienia, że dane klientów są chronione i używane w przejrzysty sposób.

Zabezpieczenia to zasadniczy składnik silnych zabezpieczeń danych we wszystkich środowiskach przetwarzania online. Jednak zabezpieczenia same nie są wystarczające. Odbiorcy i gotowość do korzystania z określonego produktu do przetwarzania w chmurze również są zależne od ich możliwości zaufania do ochrony prywatności informacji oraz że ich dane będą używane tylko w sposób zgodny z oczekiwaniami klienta . Dowiedz się więcej o podejściu firmy Microsoft do [ochrony danych i prywatności w chmurze](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)

## <a name="risk-mitigation"></a>Ograniczanie ryzyka

Dwa największe ryzyka w dowolnym centrum danych można grupować w dwa źródła: Systemy przedawnienia i błąd ludzki. Ochrona przed tymi dwoma zagrożeniami jest minimalnym warunkiem definiującym strategię zabezpieczeń IT. Ta sama wartość dotyczy chmury. Poniżej przedstawiono kilka przykładów kontroli, które mogą być wprowadzane w celu korygowania ryzyka i wzmocnienia strategii zabezpieczeń w chmurze.

- **Starsze systemy:** Wiele składników w lokalnych rozwiązaniach centrów danych obejmuje oprogramowanie, sprzęt i procesy, które stanowią wstępne bieżące zagrożenia bezpieczeństwa. Jeśli to możliwe, należy skorygować, zamienić lub wycofać te systemy podczas transformacji w chmurze. Oczywiście nie zawsze jest to możliwe. Jeśli wszystkie starsze systemy pozostaną w środowisku produkcyjnym w ramach rozwiązania hybrydowego, ważne jest, aby te systemy zostały objęte spisem i zrozumiałe podczas wirtualnego projektu centrum danych. Dzięki temu zespół projektu może wyeliminować lub kontrolować dostęp do tych systemów z chmury.
- **Procesy i mechanizmy zabezpieczeń IT:** Zespoły projektowe w chmurze powinny być odświeżane w istniejących procesach zabezpieczeń IT i kontrolach, aby przekazywać je do chmury. W idealnym scenariuszu członek zespołu ds. zabezpieczeń IT będzie szkolony w cyberbezpieczeństwa i dedykowany jako członek zespołów projektowych i wykonawczych.
- **Monitorowanie i inspekcja:** Podczas projektowania procesów i narzędzi ładu upewnij się, że rozwiązania do monitorowania i inspekcji obejmują zagrożenia bezpieczeństwa lub naruszenia.

> [!NOTE]
> **Ujawnienie długów technicznych:** W tym temacie nie ma dalszych kroków do wykonania. Dodatkowe artykuły zostaną rozwinięcie w tym temacie w czasie. Bardziej szczegółowe informacje o zabezpieczeniach w chmurze są dostępne w [ramach zaufanej chmury platformy Azure](https://azure.microsoft.com/overview/trusted-cloud). Podejścia do ulepszania organizacji Security stan można znaleźć w [katalogu usługi zabezpieczeń w chmurze](https://www.microsoft.com/security/information-protection)
