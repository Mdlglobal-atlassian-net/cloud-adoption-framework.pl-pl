---
title: Przewodnik po decyzjach związanych z szyfrowaniem
description: Zaimplementuj zasady szyfrowania, podstawową usługę migracji na platformę Azure, która zapewnia dodatkowe warstwy zabezpieczeń dla obciążeń i danych w chmurze.
author: rotycenh
ms.author: abuck
ms.date: 02/11/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 3eb722a170f508f749795fbfc91dc2ce58a1edb9
ms.sourcegitcommit: 7660521b631ea092fb805df9c9d28ad3024287ff
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83621207"
---
# <a name="encryption-decision-guide"></a>Przewodnik po decyzjach związanych z szyfrowaniem

Szyfrowanie danych chroni je przed nieautoryzowanym dostępem. Właściwie wdrożone zasady szyfrowania zapewniają dodatkowe warstwy zabezpieczeń obciążeń opartych na chmurze oraz chronią przed osobami atakującymi i innymi nieautoryzowanymi użytkownikami zarówno wewnątrz, jak i na zewnątrz organizacji i sieci.

Idź do: [Zarządzanie kluczami](#key-management) | [Szyfrowanie danych](#data-encryption) | [Dowiedz się więcej](#learn-more)

Strategia szyfrowania w chmurze skupia się na zasadach firmowych i potwierdzeniach zgodności. Szyfrowanie zasobów jest pożądane i wiele usług platformy Azure, takich jak Azure Storage i Azure SQL Database, domyślnie umożliwia szyfrowanie. Jednak szyfrowanie pociąga za sobą koszty — może zwiększyć opóźnienia i ogólne użycie zasobów.

W przypadku wymagających obciążeń istotne może być znalezienie właściwej równowagi między szyfrowaniem a wydajnością oraz określenie, jak szyfrowane są dane i ruch. Mechanizmy szyfrowania mogą różnić się pod względem kosztów i złożoności, a na decyzje dotyczące sposobu stosowania szyfrowania oraz sposobu przechowywania i zarządzania wpisami tajnymi i kluczami mogą mieć wpływ zarówno wymagania techniczne, jak i zasady.

Zasady firmowe i zgodność z innymi firmami to najważniejsze czynniki mające wpływ na planowanie strategii szyfrowania. Platforma Azure udostępnia wiele standardowych mechanizmów spełniających typowe wymagania dotyczące szyfrowania danych, zarówno magazynowanych, jak i przesyłanych. Jednak w przypadku zasad i wymagań dotyczących zgodności narzucających ściślejszą kontrolę, takich jak ustandaryzowane zarządzanie wpisami tajnymi i kluczami, używane szyfrowanie lub szyfrowanie specyficzne dla danych, należy opracować bardziej zaawansowaną strategię szyfrowania, aby sprostać tym wymaganiom.

## <a name="key-management"></a>Zarządzanie kluczami

Szyfrowanie danych w chmurze zależy od bezpieczeństwa magazynu, zarządzania i operacyjnego użycia kluczy szyfrowania. System zarządzania kluczami ma bardzo duże znaczenie dla zdolności organizacji do tworzenia i przechowywania kluczy kryptograficznych, a także ważnych haseł, parametrów połączeń i innych poufnych informacji IT oraz zarządzania nimi.

Nowoczesne systemy zarządzania kluczami, takie jak usługa Azure Key Vault, obsługują przechowywanie chronionych kluczy oprogramowania i zarządzanie nimi na potrzeby tworzenia i testowania aplikacji oraz chronione klucze sprzętowego modułu zabezpieczeń (HSM, hardware security module) w celu uzyskania maksymalnej ochrony obciążeń produkcyjnych lub danych poufnych.

Podczas planowania migracji do chmury poniższa tabela może ułatwić podjęcie decyzji o sposobie przechowywania kluczy szyfrowania, certyfikatów i wpisów tajnych, które mają krytyczne znaczenie dla tworzenia bezpiecznych i łatwych w zarządzaniu wdrożeń w chmurze, oraz zarządzania nimi:

| Pytanie | Natywne dla chmury | Używanie własnego klucza | Zatrzymywanie własnego klucza |
|--- |--------------|--------|-------------|
| Czy w organizacji brakuje scentralizowanego zarządzania kluczami i wpisami tajnymi?                                                                    | Yes          | Nie     | Nie          |
| Czy będzie potrzebne ograniczenie tworzenia kluczy i wpisów tajnych do urządzeń lokalnych, podczas gdy klucze te będą używane w chmurze? | Nie           | Yes    | Nie          |
| Czy organizacja ma wdrożone reguły lub zasady, które mogłyby uniemożliwić przechowywanie kluczy poza siedzibą firmy?                | Nie           | Nie     | Yes         |

### <a name="cloud-native"></a>Natywne dla chmury

W przypadku natywnego dla chmury zarządzania kluczami wszystkie klucze i wpisy tajne są generowane, zarządzane i przechowywane w magazynie opartym na chmurze, takim jak usługa Azure Key Vault. Takie podejście ułatwia wiele zadań IT związanych z zarządzaniem kluczami, takich jak tworzenie kopii zapasowej klucza, magazynowanie i odnawianie.

**Założenia dotyczące rozwiązań natywnych dla chmury:** Używanie natywnego dla chmury systemu zarządzania kluczami obejmuje następujące założenia:

- Masz zaufanie do rozwiązania zarządzania kluczami w chmurze pod względem tworzenia wpisów tajnych i kluczy w organizacji, zarządzania nimi i hostowania ich.
- Włączone są wszystkie lokalne aplikacje i usługi, które polegają na uzyskiwaniu dostępu do usług szyfrowania lub wpisów tajnych w celu uzyskania dostępu do systemu zarządzania kluczami w chmurze.

### <a name="bring-your-own-key"></a>Używanie własnego klucza

W przypadku podejścia polegającego na używaniu własnego klucza klucze są generowane na sprzęcie dedykowanego modułu HSM w środowisku lokalnym, a następnie bezpiecznie przenoszone do systemu zarządzania w chmurze, takiego jak usługa Azure Key Vault, do użytku z zasobami hostowanymi w chmurze.

**Założenia dotyczące używania własnego klucza:** Generowanie kluczy w środowisku lokalnym i ich używanie za pomocą systemu zarządzania kluczami w chmurze obejmuje następujące założenia:

- Masz zaufanie do podstawowych zabezpieczeń i infrastruktury kontroli dostępu platformy w chmurze pod względem hostingu i używania kluczy oraz wpisów tajnych.
- Aplikacje lub usługi hostowane w chmurze mogą uzyskiwać dostęp do kluczy i wpisów tajnych oraz używać ich w niezawodny i bezpieczny sposób.
- Przepisy prawa lub zasady organizacji wymagają tworzenia wpisów tajnych i kluczy organizacji oraz zarządzania nimi w środowisku lokalnym.

### <a name="on-premises-hold-your-own-key"></a>Środowisko lokalne (zatrzymywanie własnego klucza)

Niektóre scenariusze mogą obejmować zasady związane z przepisami lub powody techniczne, które uniemożliwiają przechowywanie kluczy w systemie zarządzania kluczami opartym na chmurze. W takich przypadkach należy generować klucze przy użyciu sprzętu lokalnego, przechowywać je i zarządzać nimi za pomocą lokalnego systemu zarządzania kluczami oraz udostępnić metodę umożliwiającą zasobom opartym na chmurze dostęp do tych kluczy dla celów szyfrowania. Należy pamiętać, że „zatrzymywanie własnego klucza” może nie być zgodne ze wszystkimi usługami Azure.

**Założenia dotyczące lokalnego zarządzania kluczami:** Używanie lokalnego systemu zarządzania kluczami obejmuje następujące założenia:

- Przepisy prawa lub zasady organizacji wymagają tworzenia wpisów tajnych i kluczy organizacji oraz zarządzania nimi i hostowania ich w środowisku lokalnym.
- Wszelkie aplikacje i usługi w chmurze, które polegają na uzyskiwaniu dostępu do usług szyfrowania lub wpisów tajnych mogą uzyskać dostęp do lokalnego systemu zarządzania kluczami.

## <a name="data-encryption"></a>Szyfrowanie danych

Istnieje kilka różnych stanów danych z różnymi potrzebami w zakresie szyfrowania, które należy wziąć pod uwagę podczas planowania zasad szyfrowania:

| Stan danych | Dane |
|-----|-----|
| Dane przesyłane | Ruch w sieci wewnętrznej, połączenia z Internetem, połączenia między centrami danych lub sieci wirtualne |
| Dane magazynowane    | Bazy danych, pliki, dyski wirtualne, magazyn PaaS |
| Dane w użyciu     | Dane załadowane do pamięci RAM lub do pamięci podręcznych procesorów CPU |

### <a name="data-in-transit"></a>Dane przesyłane

Dane przesyłane to dane przemieszczane między zasobami wewnętrznymi, centrami danych, sieciami zewnętrznymi lub za pośrednictwem Internetu.

Dane przesyłanych są zazwyczaj szyfrowane przez wymaganie protokołów SSL/TLS dla ruchu sieciowego. Zawsze szyfruj ruch między zasobami hostowanymi w chmurze a sieciami zewnętrznymi lub publicznym Internetem. Zasoby PaaS zazwyczaj domyślnie wymuszają szyfrowanie SSL/TLS. Zespoły ds. wdrażania chmury i właściciele obciążeń powinni rozważyć wymuszanie szyfrowania ruchu między zasobami IaaS hostowanymi wewnątrz sieci wirtualnych.

**Założenia dotyczące szyfrowania danych przesyłanych:** Wdrożenie właściwych zasad szyfrowania danych przesyłanych obejmuje następujące założenia:

- Wszystkie publicznie dostępne punkty końcowe w środowisku chmury będą się komunikować z publicznym Internetem przy użyciu protokołów SSL/TLS.
- Podczas łączenia sieci w chmurze z lokalną lub inną zewnętrzną siecią za pośrednictwem publicznego Internetu należy użyć zaszyfrowanych protokołów sieci VPN.
- Podczas łączenia sieci w chmurze z lokalną lub inną zewnętrzną siecią za pośrednictwem dedykowanego połączenia sieci WAN, takiego jak usługa ExpressRoute, należy użyć sieci VPN lub innego lokalnego urządzenia szyfrującego sparowanego z odpowiednią wirtualną siecią VPN lub urządzeniem szyfrującym wdrożonym w sieci w chmurze.
- Jeśli masz dane poufne, które nie powinny być uwzględniane w dziennikach ruchu lub innych raportach diagnostycznych widocznych dla pracowników działu IT, musisz zaszyfrować cały ruch między zasobami w sieci wirtualnej.

### <a name="data-at-rest"></a>Dane magazynowane

Dane magazynowane reprezentują wszystkie dane, które nie są aktywnie przenoszone lub przetwarzane, takie jak pliki, bazy danych, dyski maszyn wirtualnych, konta magazynu PaaS lub podobne zasoby. Szyfrowanie przechowywanych danych chroni urządzenia wirtualne i pliki przed nieautoryzowanym dostępem na drodze penetracji sieci z zewnątrz, przez nieautoryzowanych użytkowników wewnętrznych lub w wyniku przypadkowych wydań.

Zasoby magazynu i bazy danych PaaS zwykle domyślnie wymuszają szyfrowanie. Zasoby IaaS mogą być chronione przez szyfrowanie danych na poziomie dysku wirtualnego lub przez szyfrowanie całego konta magazynu hostującego usługi dysków wirtualnych. Wszystkie te zasoby mogą korzystać z kluczy zarządzanych przez firmę Microsoft lub kluczy zarządzanych przez klienta, przechowywanych w usłudze Azure Key Vault.

Szyfrowanie danych magazynowanych obejmuje również bardziej zaawansowane metody szyfrowania bazy danych, takie jak szyfrowanie na poziomie kolumny i wiersza, zapewniając o wiele ściślejszą kontrolę nad tym, które dokładnie dane są zabezpieczone.

To, które zasoby wymagają szyfrowania, powinny określać ogólne wymagania dotyczące zasad i zgodności, wrażliwość przechowywanych danych i wymagania dotyczące wydajności obciążeń.

### <a name="assumptions-about-encrypting-data-at-rest"></a>Założenia dotyczące szyfrowania danych magazynowanych

Szyfrowanie danych magazynowanych obejmuje następujące założenia:

- Przechowywane są dane, które nie są przeznaczone do użytku publicznego.
- Dla obciążeń akceptowany jest dodatkowy koszt w postaci opóźnienia wynikającego z szyfrowania dysku.

### <a name="data-in-use"></a>Dane w użyciu

Szyfrowanie danych w użyciu obejmuje zabezpieczanie danych w magazynie nietrwałym, takim jak pamięć RAM lub pamięć podręczna procesora CPU. Używanie technologii takich jak szyfrowanie całej pamięci i technologii enklaw takich jak Secure Guard Extensions (SGX) firmy Intel. Obejmuje to także techniki kryptograficzne, takie jak szyfrowanie homomorficzne, które może służyć do tworzenia bezpiecznych, zaufanych środowisk wykonywania.

**Założenia dotyczące szyfrowania danych w użyciu:** Szyfrowanie danych w użyciu obejmuje następujące założenia:

- Wymagane jest utrzymanie prawa własności do danych niezależnie od platformy chmury przez cały czas, nawet na poziomie pamięci RAM i procesora.

## <a name="learn-more"></a>Dowiedz się więcej

Aby uzyskać więcej informacji o szyfrowaniu i zarządzaniu kluczami na platformie Azure, zobacz:

- **[Omówienie szyfrowania na platformie Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview):** Szczegółowy opis sposobu, w jaki platforma Azure wykorzystuje szyfrowanie do zabezpieczenia zarówno danych magazynowanych, jak i przesyłanych.
- **[Usługa Azure Key Vault](https://docs.microsoft.com/azure/key-vault/general/overview):** Usługa Key Vault to podstawowy system zarządzania kluczami na platformie Azure, służący do przechowywania kluczy kryptograficznych, wpisów tajnych i certyfikatów oraz zarządzania nimi.
- **[Najlepsze rozwiązania z zakresu zabezpieczeń i szyfrowania danych platformy Azure](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices).** Omówienie najlepszych rozwiązań z zakresu zabezpieczeń i szyfrowania danych na platformie Azure.
- **[Poufne przetwarzanie na platformie Azure](https://azure.microsoft.com/solutions/confidential-compute):** Inicjatywa platformy Azure dotycząca poufnego przetwarzania zapewnia narzędzia i technologie do tworzenia zaufanych środowisk wykonywania lub innych mechanizmów szyfrowania do zabezpieczania używanych danych.

## <a name="next-steps"></a>Następne kroki

Szyfrowanie to tylko jeden z podstawowych składników infrastruktury wymagających podejmowania decyzji o architekturze w procesie wdrażania chmury. Aby poznać alternatywne wzorce lub modele używane podczas podejmowania decyzji projektowych dotyczących innych typów infrastruktury, zobacz [Omówienie przewodników dotyczących podejmowania decyzji](../index.md).

> [!div class="nextstepaction"]
> [Przewodniki podejmowania decyzji dotyczących architektury](../index.md)
