<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="policy-statements"></a>Instrukcje zasad

Poniższe instrukcje zasad określają wymagania wymagane do skorygowania określonych zagrożeń. Te zasady definiują wymagania funkcjonalne dla programu ładu MVP. Każda z nich zostanie przedstawiona w implementacji programu ładu MVP.

Cost Management:

- Do celów śledzenia wszystkie zasoby muszą być przypisane do właściciela aplikacji w ramach jednej z podstawowych funkcji roboczych.
- W przypadku wystąpienia problemów dotyczących kosztów dodatkowe wymagania dotyczące ładu zostaną nawiązane z zespołem finansowym.

Linia bazowa zabezpieczeń:

- Każdy zasób wdrożony w chmurze musi mieć zatwierdzoną klasyfikację danych.
- Żadne zasoby identyfikowane na poziomie chronionym nie mogą zostać wdrożone w chmurze, dopóki nie zostaną zatwierdzone i zaimplementowane odpowiednie wymagania dotyczące zabezpieczeń i zarządzania.
- Do momentu zweryfikowania i zarządzania minimalnymi wymaganiami dotyczącymi zabezpieczeń sieci środowiska chmury są widoczne jako strefa zdemilitaryzowana i powinny spełniać podobne wymagania dotyczące połączenia z innymi centrami danych lub sieciami wewnętrznymi.

Spójność zasobów:

- Ze względu na to, że na tym etapie nie wdrożono żadnych obciążeń o krytycznym znaczeniu, nie ma warunków podlegających umowie SLA, wydajności ani BCDR.
- W przypadku wdrożenia obciążeń o kluczowym znaczeniu należy nawiązać dodatkowe wymagania dotyczące ładu przy użyciu operacji IT.

Linia bazowa tożsamości:

- Wszystkie zasoby wdrożone w chmurze powinny być kontrolowane przy użyciu tożsamości i ról zatwierdzonych przez bieżące zasady zarządzania.
- Wszystkie grupy w lokalnej infrastrukturze Active Directory, które mają podwyższony poziom uprawnień, powinny być mapowane do zatwierdzonej roli RBAC.

Przyspieszenie wdrożenia:

- Wszystkie zasoby muszą być pogrupowane i otagowane zgodnie ze zdefiniowanymi strategiami grupowania i tagowania.
- Wszystkie zasoby muszą używać zatwierdzonego modelu wdrażania.
- Po ustanowieniu ładu dla dostawcy usług w chmurze wszystkie narzędzia do wdrażania muszą być zgodne z narzędziami zdefiniowanymi przez zespół nadzoru.

## <a name="processes"></a>Procesy

Nie przydzielono budżetu do ciągłego monitorowania i wymuszania tych zasad ładu. Z tego względu zespół nadzoru chmurowego posiada pewne metody ad hoc do monitorowania przestrzegania instrukcji zasad.

- **Oświat** Zespół ds. zarządzania chmurą to czas inwestowania w chmurę wdrożenia chmury w przewodnikach ładu, które obsługują te zasady.
- **Przeglądy wdrożenia:** Przed wdrożeniem dowolnego elementu zawartości zespół ds. zarządzania chmurą przegląda Przewodnik dotyczący ładu z zespołami wdrażania chmury.
