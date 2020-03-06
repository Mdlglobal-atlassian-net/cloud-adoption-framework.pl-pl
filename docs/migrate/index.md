---
title: Migracja do chmury
description: Migracja do chmury w podręczniku Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: 90a9c69b311f1d4687d2691af13c3b51a7b6f813
ms.sourcegitcommit: 26caeb6b7f4e14df30bf16727d0b1b3d63b9c0c2
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/05/2020
ms.locfileid: "78337803"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Migracja do chmury w podręczniku Cloud Adoption Framework

Każdy [plan wdrożenia chmury](../plan/index.md) w skali przedsiębiorstwa będzie zawierać obciążenia, które nie gwarantują znacznych inwestycji w przypadku tworzenia nowej logiki biznesowej. Te obciążenia można przenieść do chmury za pomocą różnorodnych podejść: metodą „lift and shift” czy „lift and optimize” albo przez modernizację. Każda z tych metod jest traktowana jako migracja. Poniższe ćwiczenia pomogą ustanowić iteracyjne procesy oceniania, migrowania, optymalizacji i zabezpieczania tych obciążeń oraz zarządzania nimi.

## <a name="getting-started"></a>Wprowadzenie

W celu przygotowania się na tę fazę cyklu życia wdrożenia chmury, sugerujemy pięć następujących ćwiczeń:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/prerequisites.md?tabs=Checklist">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Wstępne wymagania dotyczące migracji</h3>
Sprawdź, czy strefa docelowa została wdrożona i czy jest przygotowana do hostowania kilku pierwszych obciążeń, które zostaną zmigrowane na platformę Azure. Jeśli strategia wdrażania chmury i plan wdrożenia chmury nie zostały utworzone, sprawdź, czy prace nad nimi są w toku.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migrowanie pierwszego obciążenia</h3>
Podczas migracji pierwszego obciążenia skorzystaj ze wskazówek zawartych w Przewodniku po migracji na platformę Azure. Dzięki temu poznasz narzędzia i metody potrzebne do skalowania prac związanych z wdrożeniem.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Rozszerzone scenariusze migracji</h3>
Skorzystaj z listy kontrolnej dotyczącej zakresu rozszerzonego, aby zidentyfikować scenariusze, które wymagałyby modyfikacji przyszłego stanu architektury, procesów migracji, konfiguracji strefy docelowej lub decyzji dotyczących narzędzi migracji.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Najlepsze rozwiązania</h3>
Sprawdź wszystkie modyfikacje pod kątem sekcji najlepszych rozwiązań, aby zapewnić właściwą implementację rozszerzonego zakresu lub metod migracji specyficznych dla obciążenia/architektury.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/5.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Ulepszenia procesu</h3>
Migracja to działanie mocno obciążone procesami. Skalując nakład pracy związany z migracją, skorzystaj z sekcji zagadnień dotyczących migracji, aby ocenić i rozwinąć różne aspekty swoich procesów.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="iterative-migration-process"></a>Iteracyjny proces migracji

Zasadniczo migracja do chmury składa się z czterech prostych faz: ocena, migracja, optymalizacja, zabezpieczenia i zarządzanie. Ta sekcja podręcznika Cloud Adoption Framework uczy czytelników, jak zmaksymalizować zwrot z każdej fazy tego procesu i jak dostosować te fazy do swojego planu wdrożenia chmury. Poniższa ilustracja przedstawia fazy w podejściu iteracyjnym:

![Model migracji opisany w przewodniku Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

## <a name="create-a-balanced-cloud-portfolio"></a>Tworzenie zrównoważonego portfolio chmury

Każde zrównoważone portfolio technologiczne zawiera zróżnicowane zasoby w różnych stanach. Planowane jest wycofanie niektórych aplikacji i są one objęte minimalnym wsparciem. Inne aplikacje lub zasoby są obsługiwane w stanie konserwacji, ale funkcje tych rozwiązań są stabilne. W przypadku nowszych procesów biznesowych zmieniające się warunki rynkowe stymulują ciągłe ulepszenia lub modernizacje funkcji. Gdy powstają możliwości zapewnienia nowych źródeł przychodów, nowe aplikacje lub zasoby są wprowadzane do środowiska. Na każdym etapie cyklu życia zasobów wpływ inwestycji na przychody i zyski będzie ulegać zmianie. Wraz z kolejnymi etapami cyklu życia maleje prawdopodobieństwo, że nowa funkcja lub modernizacja umożliwi uzyskanie znaczne zwrotu z inwestycji.

Chmura zapewnia różne mechanizmy wdrażania, z których każdy cechuje się podobnym zakresem inwestycji i stopniem zwrotu. Tworzenie aplikacji natywnych dla chmury może znacznie zmniejszyć koszty operacyjne. Po wydaniu aplikacji natywnej dla chmury możliwe są szybsze iteracje programowania nowych funkcji. Modernizacja aplikacji może przynieść podobne korzyści przez wyeliminowanie starszych ograniczeń związanych z lokalnymi modelami programowania. Niestety, te dwa podejścia są pracochłonne i zależą od rozmiaru, umiejętności oraz doświadczenia zespołów programistycznych. Często praca nie jest zgodna z celami &mdash; osoby mające umiejętności i talent do modernizowania aplikacji wolą tworzyć nowe aplikacje. Na rynku, na którym brakuje pracowników, podczas projektów modernizacyjnych na dużą skalę mogą występować problemy związane z zadowoleniem pracowników i brakiem kwalifikacji. W zrównoważonym portfolio to podejście powinno być zarezerwowane dla aplikacji, które będą otrzymywać istotne ulepszenia funkcji, jeśli pozostaną w środowisku lokalnym.

## <a name="envision-an-end-state"></a>Przewidywanie stanu końcowego

Efektywny proces migracji wymaga określenia miejsca docelowego. Przed zrobieniem pierwszego kroku ustal przybliżoną wizję stanu końcowego. Ta grafika informacyjna przedstawia punkt początkowy składający się z istniejących aplikacji, danych i infrastruktury, które definiują majątek cyfrowy. Podczas procesu migracji każdy zasób jest przenoszony z zastosowaniem jednej z opcji po prawej stronie.

## <a name="migration-implementation"></a>Implementacja migracji

W tych artykułach omówiono dwa procesy, z których każdy ma podobny cel &mdash; zmigrowanie znaczącej części istniejących zasobów na platformę Azure. Jednak wyniki biznesowe i bieżący stan będą mieć istotny wpływ na procesy wymagane do osiągnięcia celu. Te subtelne odchylenia mogą być przyczyną dwóch znacząco odmiennych podejść dotyczących osiągnięcia podobnego stanu końcowego.

![Model migracji opisany w przewodniku Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

Aby zapewnić instrukcje dotyczące przyrostowego wykonania podczas przejścia do stanu końcowego, ten model dzieli migrację, skupiając się na dwóch obszarach.

**Przygotowanie do migracji:** Określ przybliżoną listę prac opartą głównie na bieżącym stanie i żądanych wynikach.

- **Wyniki biznesowe:** Kluczowe cele biznesowe tej migracji.
- **Szacowanie majątku cyfrowego:** Przybliżona szacunkowa liczba i stan obciążeń do migracji.
- **Role i obowiązki:** Jasna definicja struktury zespołu, podziału obowiązków i wymagań dotyczących dostępu.
- **Wymagania dotyczące zarządzania zmianami:** Tempo, procesy i dokumentacja wymagana do przeglądu i zatwierdzania zmian.

Te początkowe dane wejściowe kształtują listę prac związanych z migracją. Danymi wyjściowymi listy prac związanych z migracją jest lista aplikacji do zmigrowania do chmury. Ta kształtuje sposób realizacji procesu migracji do chmury. Wraz z upływem czasu będzie również powiększana o tworzenie dokumentacji niezbędnej do zarządzania zmianami.

**Proces migracji:** Każde działanie związane z migracją do chmury jest częścią jednego z następujących procesów w odniesieniu do listy prac związanych z migracją.

- **Ocena:** Oceń istniejący zasób i określ plan migracji tego zasobu.
- **Migracja:** Zreplikuj funkcję zasobu w chmurze.
- **Optymalizacja:** Zrównoważ wydajność, koszt, dostęp i możliwości operacyjne zasobu w chmurze.
- **Zabezpieczanie i zarządzanie:** Upewnij się, że zasób w chmurze jest gotowy do ciągłego działania.

Informacje zebrane podczas tworzenia listy prac związanych z migracją określają złożoność procesu migracji i wymagany nakład pracy z nim związany w ramach każdej iteracji i poszczególnych wydań funkcji.

## <a name="transition-to-the-end-state"></a>Przejście do stanu końcowego

Celem jest płynna i częściowo zautomatyzowana migracja do chmury. W procesie migracji są używane narzędzia zapewnione przez dostawcę chmury w celu szybkiej replikacji i przygotowania zasobów w chmurze. Po weryfikacji prosta zmiana sieci przekierowuje użytkowników do rozwiązania w chmurze. Dla wielu przypadków użycia technologia potrzebna do osiągnięcia tego celu jest w dużej mierze dostępna. Istnieją przykładowe przypadki, które pokazują tempo, w jakim można zreplikować 10 000 maszyn wirtualnych na platformie Azure.

Nadal wymagane jest przyrostowe podejście do migracji. W większości środowisk długą listę maszyn wirtualnych do migracji należy podzielić na mniejsze jednostki pracy, aby migracja zakończyła się powodzeniem. Istnieje wiele czynników, które ograniczają liczbę maszyn wirtualnych możliwych do zmigrowania w danym okresie. Szybkość sieciowego ruchu wychodzącego jest jednym z ograniczeń technicznych. Większość ograniczeń wynika z możliwości przedsiębiorstwa związanych z weryfikacją i dostosowaniem się do zmian.

Przyrostowe podejście do migracji w ramach przewodnika Cloud Adoption Framework pomaga utworzyć plan przyrostowy, który odzwierciedla i dokumentuje ograniczenia techniczne oraz kulturowe. Ten model ma na celu zwiększenie szybkości migracji przy jednoczesnej minimalizacji nakładu pracy działu IT i przedsiębiorstwa. Poniżej podano dwa przykłady wykonania migracji przyrostowej w oparciu o listę prac związanych z migracją.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./azure-migration-guide/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Przewodnik po migracji na platformę Azure</h3>
                        <p><b>Opisowe podsumowanie:</b> Ten klient wykonuje migrację mniej niż 1000 maszyn wirtualnych. Mniej niż dziesięć obsługiwanych aplikacji jest własnością właściciela aplikacji, który nie należy do organizacji IT. Pozostałe aplikacje, maszyny wirtualne i skojarzone dane są własnością członków zespołu ds. wdrażania chmury i są przez nich obsługiwane. Członkowie zespołu ds. wdrażania chmury mają dostęp administracyjny do środowisk produkcyjnych w istniejącym centrum danych.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./expanded-scope/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Przewodnik dotyczący złożonego scenariusza</h3>
                        <p><b>Opisowe podsumowanie:</b> Migracja tego klienta jest złożona na poziomie działalności, kultury i technologii. Ten przewodnik opisuje wiele problemów o konkretnej złożoności oraz sposoby ich rozwiązania.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

Te dwa procesy reprezentują dwa skrajne doświadczenia klientów, którzy zainwestowali w migrację do chmury. W większości firm stosowana jest kombinacja dwóch powyższych scenariuszy. Po zapoznaniu się z procesami użyj modelu migracji w ramach podręcznika Cloud Adoption Framework, aby rozpocząć rozmowę na temat migracji i zmodyfikować procesy bazowe w celu lepszego spełnienia Twoich potrzeb.

## <a name="next-steps"></a>Następne kroki

Wybierz jeden z następujących procesów:

> [!div class="nextstepaction"]
> [Przewodnik po migracji na platformę Azure](./azure-migration-guide/index.md)
>
> [Przewodnik o rozszerzonym zakresie](./expanded-scope/index.md)
