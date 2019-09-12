---
title: Początkowe dopasowywanie organizacji
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Zawiera omówienie początkowego dopasowywania organizacji.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: governance
ms.openlocfilehash: a3e819cdd726e3df6edb4cbe0c20a7d652fde152
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70819168"
---
# <a name="initial-organization-alignment"></a>Początkowe dopasowywanie organizacji

**Cyfrowa transformacja** do przetwarzania w chmurze reprezentuje przejście od działania w środowisku lokalnym do działania w chmurze. Ta zmiana obejmuje nowe sposoby prowadzenia działalności — na przykład cyfrowa transformacja pozwala zastąpić wydatki inwestycyjne na oprogramowanie i sprzęt centrum danych wydatkami operacyjnymi na potrzeby użycia zasobów chmury. Zobaczmy, jak rozpocząć przy użyciu modelu [Microsoft Cloud Adoption Framework dla platformy Azure](../index.md).

## <a name="the-digital-transformation-process"></a>Proces cyfrowej transformacji

W celu pomyślnego wdrożenia chmury przedsiębiorstwo musi przygotować swoją organizację, osoby i procesy, aby były gotowe do tej cyfrowej transformacji. Struktura organizacyjna przedsiębiorstwa jest różna, dlatego nie ma żadnego podejścia, które pozwala przygotować w jednakowy sposób każdą z organizacji. Ten dokument zawiera opis kroków wysokiego poziomu, które przedsiębiorstwo może podjąć w celu przygotowania. Organizacja będzie musiała poświęcić czas na tworzenie szczegółowego planu realizacji każdego z wymienionych kroków.

Wysokiego poziomu proces transformacji cyfrowej jest następujący:

1. Tworzenie zespołu strategicznego ds. chmury. Ten zespół jest odpowiedzialny za prowadzenie transformacji cyfrowej. Na tym etapie ważne jest również utworzenie zespołu ds. ładu i zespołu ds. zabezpieczeń na potrzeby transformacji cyfrowej.
2. Członkowie zespołu strategicznego ds. chmury poznają nowe i zmienione technologie chmurowe.
3. Zespół strategiczny ds. chmury przygotowuje przedsiębiorstwo, tworząc przypadek biznesowy dla transformacji cyfrowej — wylicza wszystkie bieżące luki w strategii biznesowej i określa rozwiązania wysokiego poziomu w celu eliminacji tych luk.
4. Dopasowanie rozwiązań wysokiego poziomu do grup biznesowych. Identyfikacja osób biorących udział projekcie w każdej grupie biznesowej, które będą właścicielami projektu i implementacji poszczególnych rozwiązań.
5. Dostosowanie istniejących ról, umiejętności i procesów, aby uwzględnić role, umiejętności i procesy związane z chmurą.

<!--6. Develop processes for operating in the cloud to make solutions more robust in terms of availability, resiliency, and security.
1. Optimize solutions for performance, scalability, and cost efficiency.-->

## <a name="step-1-create-a-cloud-strategy-team"></a>Krok 1: Tworzenie zespołu strategicznego ds. chmury

Pierwszym krokiem cyfrowej transformacji przedsiębiorstwa jest zaangażowanie liderów biznesowych w całej organizacji w celu utworzenia zespołu strategicznego ds. chmury (CST, cloud strategy team). Ten zespół składa się z liderów biznesowych z działów finansów, infrastruktury IT i grup aplikacji. Zespoły te mogą pomóc w analizie chmury i fazie eksperymentowania.

Na przykład zespół strategiczny ds. chmury może być prowadzony przez dyrektora ds. technologii i składać się z członków zespołu architektury przedsiębiorstwa, finansów IT, starszych technologów z różnych grup aplikacji IT (kadry, finanse itd.) oraz liderów zespołów ds. infrastruktury, zabezpieczeń i sieci.

Ważne jest również, aby utworzyć dwa inne zespoły wysokiego poziomu: zespół ds. ładu i zespół ds. zabezpieczeń. Zespoły te są odpowiedzialne za projektowanie, wdrażanie i bieżącą inspekcję zasad ładu i zabezpieczeń przedsiębiorstwa. Zespół ds. ładu potrzebuje członków, którzy pracowali nad ochroną zasobów, zarządzaniem kosztami, zasadami grup i pokrewnymi tematami. Zespół ds. zabezpieczeń potrzebuje członków, którzy biegle znają branżowe standardy zabezpieczeń, a także wymagania dotyczące zabezpieczeń przedsiębiorstwa.

![Zespół strategiczny ds. chmury z zespołami ds. ładu i zabezpieczeń](../_images/getting-started-overview-1.png)

Zespół ds. ładu jest odpowiedzialny za projektowanie i implementację modelu ładu przedsiębiorstwa w chmurze, a także wdrażanie i konserwowanie zasobów infrastruktury współdzielonej, które są częścią transformacji cyfrowej. Te zasoby obejmują zasoby sprzętowe, programowe i chmurowe niezbędne do połączenia sieci lokalnej z siecią wirtualną w chmurze.

Zespół ds. zabezpieczeń jest odpowiedzialny za projektowanie i implementowanie zasad zabezpieczeń przedsiębiorstwa w chmurze, przy ścisłej współpracy z zespołem ds. ładu. Zespół ds. zabezpieczeń jest właścicielem rozszerzenia granic zabezpieczeń w sieci lokalnej w celu uwzględnienia sieci wirtualnych w chmurze. Może to mieć formę posiadania i utrzymywania zapór ruchu przychodzącego i wychodzącego w sieci wirtualnej w chmurze, a także zapewniania, że narzędzia i zasady uniemożliwiają wdrożenie nieautoryzowanych zasobów.

## <a name="step-2-learn-whats-new-in-the-cloud"></a>Krok 2: Poznawanie nowości w chmurze

Następnym krokiem cyfrowej transformacji przedsiębiorstwa jest nauczenie się przez członków zespołu strategicznego ds. chmury, w jaki sposób technologia chmury zmieni biznesowy sposób działania przedsiębiorstwa. Jest to przygotowywanie i planowanie zmian biznesowych, personalnych i technologicznych. Ważne jest, aby członkowie zespołu strategicznego ds. chmury mogli zrozumieć, co jest nowego w chmurze i czym różni się ona od rozwiązań lokalnych.

![Zespół strategiczny ds. chmury oraz zespoły ds. ładu i zabezpieczeń poznają najlepsze rozwiązania dotyczące działalności w chmurze.](../_images/getting-started-overview-2.png)

Punktem początkowym do zrozumienia chmury jest nauczenie się [jak platforma Azure działa](../getting-started/what-is-azure.md) na wysokim poziomie. Następnie warto poznać podstawy [ładu na platformie Azure](../governance/resource-consistency/what-is-governance.md) w celu przygotowania się do [zarządzania dostępem do zasobów](../governance/resource-consistency/azure-resource-access.md).

Aby poznać zaawansowaną wiedzę, zespół ds. ładu powinien przejrzeć koncepcje i przewodniki projektowe w sekcji ładu zawartej w spisie treści. Sekcje infrastruktury i obciążeń są przydatne do poznawania typowych architektur i obciążeń w chmurze.

## <a name="step-3-identify-gaps-in-business-strategy"></a>Krok 3: Identyfikowanie luk w strategii biznesowej

Następnym krokiem zespołu strategicznego ds. chmury jest wyliczenie problemów biznesowych, które wymagają rozwiązania transformacji cyfrowej. Na przykład przedsiębiorstwo może korzystać z istniejącego lokalnego centrum danych z przestarzałym sprzętem, który wymaga wymiany. W innym przykładzie przedsiębiorstwo może doświadczać trudności z czasem wprowadzenia na rynek nowych funkcji i usług, a zatem nie nadążać za konkurencją. Te luki przedstawiają _cele_ cyfrowej transformacji przedsiębiorstwa.

Luki w strategii biznesowej mogą być klasyfikowane w następujących kategoriach:

| Kategoria | Opis |
| --- | --- |
| Zarządzanie kosztami | Reprezentuje lukę w sposobie opłacania technologii przez przedsiębiorstwo. |
| Ład | Reprezentuje lukę w procesach używanych przez przedsiębiorstwo do ochrony zasobów przed nieprawidłowym użyciem, które może spowodować przekroczenie kosztów, problemy z zabezpieczeniami lub problemy ze zgodnością. |
| Zgodność | Reprezentuje lukę w sposobie, w jaki przedsiębiorstwo przestrzega własnych wewnętrznych procesów i zasad, a także zewnętrznych przepisów, regulacji i standardów. |
| Bezpieczeństwo | Reprezentuje lukę w sposobie, w jaki przedsiębiorstwo chroni swoją technologię i zasoby danych przed zagrożeniami zewnętrznymi. |
| Ład dotyczący danych | Reprezentuje lukę w sposobie, w jaki przedsiębiorstwo zarządza swoimi danymi, a w szczególności danymi klientów. Na przykład Ogólne rozporządzenie o ochronie danych (RODO) w Unii Europejskiej ma rygorystyczne wymagania w zakresie ochrony danych klienta, które mogą wymagać nowego sprzętu i oprogramowania. |

Gdy przedsiębiorstwo zaklasyfikuje wszystkie luki w zakresie strategii biznesowej do tych kategorii, następnym krokiem jest określenie rozwiązania wysokiego poziomu dla każdego problemu.

W poniższej tabeli przedstawiono kilka przykładów:

|Luka w strategii biznesowej|Kategoria &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|Rozwiązanie &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|-----|-----|-----|
| Usługi aktualnie hostowane w środowisku lokalnym doświadczają problemów z dostępnością, odpornością i skalowalnością w czasie szczytowego zapotrzebowania, czyli około 10 procent użycia. Serwery w lokalnym centrum danych są przestarzałe. Dział IT przedsiębiorstwa zaleca zakup nowego sprzętu lokalnego dla centrum danych z specyfikacjami do obsługi szczytowego zapotrzebowania.| Zarządzanie kosztami | Przeprowadź migrację istniejących, problematycznych obciążeń lokalnych do skalowalnych zasobów w chmurze i płać wyłącznie za użycie. |
| Zewnętrzne przepisy i regulacje dotyczące zarządzania danymi wymagają od przedsiębiorstwa przestrzegania zestawu standardowych sposobów kontroli, które wymagają szyfrowania danych magazynowanych, a zatem nowego sprzętu i oprogramowania. | Ład dotyczący danych | Przenieś dane do szyfrowanej usługi magazynowej Azure dla danych magazynowanych. |
| W usługach hostowanych w lokalnym centrum danych wystąpiły rozproszone ataki odmowy usługi (DDoS) dotyczące usług publicznych. Ataki są trudne do wyeliminowania, a skuteczne zaradzenie im wymaga nowego sprzętu, oprogramowania i personelu ds. zabezpieczeń. | Bezpieczeństwo | Przeprowadź migrację usług na platformę Azure i skorzystaj z ochrony przed atakami DDoS platformy Azure.|

Po wyliczeniu wszystkich luk w strategii biznesowej i ustaleniu rozwiązań wysokiego poziomu należy określić priorytety listy. Na liście można określić priorytety, dopasowując luki w zakresie strategii biznesowej do krótkoterminowych i długoterminowych celów przedsiębiorstwa w każdej kategorii. Na przykład, jeśli przedsiębiorstwo ma krótkoterminowy cel zmniejszenia wydatków w ciągu następnych dwóch kwartałów obrachunkowych, można określić priorytet luki biznesowej w kategorii *zarządzanie kosztami* na podstawie przewidywanych oszczędności kosztów skojarzonych z każdą z luk.

Dane wyjściowe tego procesu to lista rankingowa rozwiązań wysokiego poziomu, które są dopasowane do kategorii biznesowych.

## <a name="step-4-align-high-level-solutions-with-business-groups-to-design-solutions"></a>Krok 4: Dopasowanie rozwiązań wysokiego poziomu do grup biznesowych w celu projektowania rozwiązań

Teraz, gdy cele transformacji cyfrowej zostały wyliczone, określono ich priorytety i zaproponowano rozwiązania wysokiego poziomu, następnym krokiem zespołu strategicznego ds. chmury jest dostosowanie poszczególnych rozwiązań wysokiego poziomu do zespołów projektowych i implementujących w każdej z grup biznesowych.

Zespoły przyjmują listy z priorytetami i opracowują poszczególne rozwiązania wysokiego poziomu, aby zaprojektować każde z rozwiązań. Proces projektowania obejmuje określenie nowej infrastruktury i nowych obciążeń. Mogą być również wprowadzane zmiany dotyczące ról osób i wykonywanych przez nie procesów. Na tym etapie ważne jest także, aby zespoły ds. ładu i zabezpieczeń przejrzały każdy projekt wykonany przez każdy z zespołów projektowych. Każdy projekt musi podlegać zasadom i procedurom zdefiniowanym przez zespoły ds. ładu i zabezpieczeń, a te zespoły muszą być uwzględnione w ostatecznym zatwierdzaniu każdego projektu.

![Zespół strategiczny ds. chmury dostarcza rozwiązania wysokiego poziomu zespołom projektowym i implementującym.](../_images/getting-started-overview-3.png)

Projektowanie poszczególnych rozwiązań nie jest prostym zadaniem. W miarę tworzenia projektów należy je rozpatrywać w kontekście innych projektów rozwiązań pochodzących od innych zespołów. Jeśli na przykład kilka z projektów powoduje migrację istniejących lokalnych aplikacji i usług do chmury, bardziej wydajne może być zgrupowanie ich razem i zaprojektowanie ogólnej strategii migracji. W innym przykładzie może nie być możliwe migrowanie niektórych istniejących lokalnych aplikacji i usług, a rozwiązaniem może być zastąpienie ich przez usługi zaprogramowane na nowo lub dostarczone przez inne firmy. W takim przypadku może być wydajniejsze ich zgrupowanie i sprawdzenie, czy nie nakładają się, aby wyznaczyć, czy można zastosować usługę innej firmy do większej liczby rozwiązań.

Po ukończeniu projektowania rozwiązania zespół przechodzi do fazy implementacji poszczególnych projektów. Faza implementacji każdego projektu rozwiązania może odbywać się przy użyciu standardowych procesów zarządzania projektami.

## <a name="step-5-adapt-existing-roles-skills-and-process-for-the-cloud"></a>Krok 5. Dostosowanie istniejących ról, umiejętności i procesów do chmury

W każdej fazie historii branży IT najbardziej znaczące zmiany branżowe często oznaczają zmiany dotyczące ról pracowników. Podczas przejścia od komputerów mainframe do modelu klient/serwer, rola operatora komputera w dużym stopniu zanikła i została zastąpiona przez rolę administratora systemu. Kiedy nadeszła era wirtualizacji, zmalało zapotrzebowanie na osoby indywidualne pracujące na fizycznych serwerach i zostało zastąpione zapotrzebowaniem na specjalistów ds. wirtualizacji. Podobnie, przy przejściu instytucji do przetwarzania w chmurze, role prawdopodobnie znowu się zmienią. Na przykład specjaliści centrum danych mogą zostać zastąpieni analitykami finansowymi chmury. Nawet w przypadkach, gdy tytuły zawodów IT nie ulegają zmianie, codzienne role robocze znacznie się zmieniły.

Pracownicy działu IT mogą niepokoić się o swoje role i stanowiska, dowiadując się, że do obsługi rozwiązań w chmurze jest wymagany inny zestaw umiejętności. Jednak elastyczni pracownicy, którzy eksplorują i poznają nowe technologie chmury, nie muszą się obawiać. Mogą oni dążyć do wdrażania usług w chmurze i pomagać organizacji zrozumieć i przyjąć powiązane zmiany.

### <a name="capturing-concerns"></a>Wychwytywanie problemów

Podczas transformacji cyfrowej każdy zespół powinien od razu wychwycić ewentualne problemy pracowników. Podczas wychwytywania problemów należy zidentyfikować następujące elementy:

- **Typ problemu.** Na przykład pracownicy mogą być oporni na zmiany obowiązków zawodowych, które towarzyszą transformacji cyfrowej.
- **Wpływ problemu, jeśli nie zostanie rozwiązany.** Na przykład odporność na transformację cyfrową może spowodować, że pracownicy będą wolno realizować niezbędne zmiany.
- **Obszar przystosowany do rozwiązania problemu.** Na przykład, jeśli pracownicy w dziale IT są niechętnie nastawieni do zdobywania nowych umiejętności, najlepiej przystosowanym do rozwiązania tego problemu obszarem będą osoby biorące udział w projekcie IT. Zidentyfikowanie obszaru może być oczywiste w przypadku niektórych problemów. W takich przypadkach może być konieczna eskalacja do kierownictwa wykonawczego.

### <a name="identify-gaps"></a>Identyfikacja luk

Innym aspektem pracy w przypadku problemów z transformacją cyfrową przedsiębiorstwa jest zidentyfikowanie **luk**. Luką są rola, umiejętność lub proces wymagane dla transformacji cyfrowej, które nie istnieją obecnie w przedsiębiorstwie.

Zacznij od wyliczenia nowych obowiązków, które towarzyszą transformacji cyfrowej, z naciskiem na nowe obowiązki i bieżące obowiązki do wycofania. Określ obszar dopasowany do poszczególnych odpowiedzialności. W przypadku nowych obowiązków należy wyznaczyć, jak ściśle są dopasowane do obszaru. Niektóre obowiązki mogą obejmować kilka obszarów, co stanowi możliwość lepszego dopasowania, które należy wychwycić jako problem. W przypadku, gdy żaden obszar nie zostanie rozpoznany jako odpowiedzialny, należy wychwycić to jako lukę.

Następnie zidentyfikuj umiejętności niezbędne do obsługi odpowiedzialności. Ustal, czy przedsiębiorstwo ma istniejące zasoby z tymi umiejętnościami. Jeśli żadne istniejące zasoby nie są dostępne, wyznacz niezbędne programy szkoleniowe lub talenty do pozyskania. Określ przedział czasu, w którym trzeba obsłużyć daną odpowiedzialność, aby zachować właściwy przebieg transformacji cyfrowej.

Na koniec zidentyfikuj role, które będą realizować te umiejętności. Niektórzy z istniejących pracowników obejmą części roli, a w innych przypadkach może być konieczna zupełnie nowa rola.

### <a name="partner-across-teams"></a>Partnerstwo zespołów

Umiejętności niezbędne do wypełnienia luk w transformacji cyfrowej organizacji zwykle nie będą ograniczone do pojedynczej roli ani nawet pojedynczego działu. Umiejętności będą mieć relacje i zależności, które mogą obejmować pojedynczą rolę lub wiele ról, a role te mogą istnieć w kilku działach. Na przykład właściciel obciążenia może wymagać, aby ktoś w roli IT ustanowił podstawowe zasoby, takie jak subskrypcje i grupy zasobów.

Te zależności reprezentują nowe procesy implementowane przez organizację w celu zarządzania przepływem pracy między rolami. W powyższym przykładzie kilka różnych typów procesów może obsługiwać relację między właścicielem obciążenia a rolą IT. Na przykład można utworzyć narzędzie przepływu pracy w celu zarządzania procesem lub można użyć prostego szablonu wiadomości e-mail.

Śledź te zależności i dostrzegaj procesy, które będą je obsługiwać, oraz zauważ, czy te procesy już istnieją. W przypadku procesów wymagających narzędzi upewnij się, że plan wdrażania dowolnych narzędzi jest dopasowany do ogólnego harmonogramu transformacji cyfrowej.

## <a name="next-steps"></a>Następne kroki

Transformacja cyfrowa jest procesem iteracyjnym, a z każdą iteracją zespoły stają się bardziej wydajne.

> [!div class="nextstepaction"]
> [Sposób działania platformy Azure](../getting-started/what-is-azure.md)
