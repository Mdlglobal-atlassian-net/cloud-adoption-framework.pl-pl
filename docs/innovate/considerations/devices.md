---
title: Korzystanie z urządzeń za pomocą funkcji odpisywania cyfrowo
description: Dowiedz się więcej na temat zaawansowanych metod zmniejszania wysiłku innowacji dzięki interakcji z klientami i środowiskiem otoczenia, a nie aplikacjami.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 2fd3bfb329131e2ec344131ba3e2cbf8bc189a8f
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83219737"
---
# <a name="ambient-experiences-interact-with-devices"></a>Środowiska otoczenia: korzystanie z urządzeń

W [kompilacji z empatię klienta](./build.md)omawiamy trzy testy prawdziwych innowacji: Rozwiąż potrzebę klienta, powracaj do klienta i Skaluj go na podstawie podstawy kohorty klientów. Każdy test hipotezy wymaga wysiłku i iteracji na podejście do wdrożenia. Ten artykuł zawiera szczegółowe informacje na temat niektórych zaawansowanych metod zmniejszania tego nakładu pracy przez _środowisko otoczenia_. W przypadku korzystania z urządzeń, a nie aplikacji, klient może być bardziej prawdopodobnie przełączany do rozwiązania.

## <a name="ambient-experiences"></a>Środowiska otoczenia

Środowisko otoczenia to środowisko cyfrowe, które odnosi się do bezpośredniego otoczenia. Rozwiązanie, które oferuje funkcje otoczenia, dąży do zaspokojenia klienta w razie potrzeby. Jeśli to możliwe, rozwiązanie spełnia wymagania klienta bez opuszczania przepływu działania, które go wywołało.

Żywotność w gospodarce cyfrowej jest całkowicie odwracania. Wszyscy jesteśmy bombarded z wiadomościami społecznościowymi, wiadomościami e-mail, sieciami Web, wizualizacją i werbalnymi, z których każdy jest ryzykiem odwracania. To ryzyko rośnie w każdej sekundzie, która upływa między punktem wymaganym przez klienta a momentem, gdy napotykają rozwiązanie. Niezliczone klienci są traconi w krótkim czasie. Aby wzrosnąć wdrożenie powtarzania, należy zmniejszyć liczbę rozpraszań, skracając czas na rozwiązanie (TTS).

## <a name="interact-with-devices"></a>Interakcja z urządzeniami

Standardowe środowisko sieci Web to najpopularniejsza technika tworzenia aplikacji używana do zaspokajania potrzeb klienta. W tym podejściu przyjęto założenie, że klient jest przed komputerem. Jeśli klient spójnie zaspokaja swój punkt potrzebny przed laptopem, Utwórz aplikację internetową. Ta aplikacja sieci Web zapewni środowisko otoczenia dla tego klienta w tym scenariuszu. Jednak wiemy, że ten scenariusz jest mniej i mniej prawdopodobnie w naszym bieżącym ERA.

![Środowiska otoczenia](../../_images/innovate/ambient-experiences.png)

Środowiska otoczenia zwykle wymagają więcej niż aplikacji sieci Web w ciągu następującej liczby dni. Dzięki [pomiarowi](./measure.md) i rozpoczęciu pracy [z klientem](./learn.md) zachowanie, które wyzwala potrzebę klienta, może być obserwowane, śledzone i używane do tworzenia większej otoczenia. Poniższa lista zawiera podsumowanie kilku metod integracji rozwiązań otoczenia z poszczególnymi informacjami o każdej z poniższych akapitów.

- ** [Środowisko mobilne](#mobile-experience):** Podobnie jak w przypadku laptopów aplikacje mobilne są powszechnie używane w środowiskach klientów. W niektórych sytuacjach może to zapewnić odpowiedni poziom interakcji, aby zapewnić otoczenie rozwiązania.
- ** [Rzeczywistość mieszana](#mixed-reality):** Czasami należy zmienić typowy otoczenie klienta, aby zapewnić interakcję. Ten czynnik tworzy coś w przypadku wartości false, w której klient współdziała z rozwiązaniem i ma zapotrzebną wartość. W takim przypadku rozwiązanie jest otaczające wartość false.
- ** [Rzeczywistość zintegrowana](#integrated-reality):** Przechodzenie bliżej Ambience, zintegrowane rozwiązania o rzeczywistości koncentrują się na korzystaniu z urządzenia, które istnieje w rzeczywistości klienta, aby zintegrować rozwiązanie z naturalnymi zachowaniami. Wirtualny asystent to doskonały przykład integracji rzeczywistości z otaczającym środowiskiem. Mniej znana opcja dotyczy technologii Internet rzeczy (IoT), które integrują urządzenia, które już istnieją w otoczeniu klienta.
- ** [Zastosowana rzeczywistość](#adjusted-reality):** Gdy dowolne z tych rozwiązań w otoczeniu korzysta z analizy predykcyjnej w chmurze do definiowania i zapewniania interakcji z klientem w naturalnym otoczeniu, rozwiązanie ma już wartość rzeczywistość.

Zrozumienie potrzeb klientów i mierzenie wpływu klientów obie pomocne w ustaleniu, czy interakcja urządzenia lub środowisko otoczenia są niezbędne do zweryfikowania hipotez. W przypadku każdego z tych punktów danych następujące sekcje ułatwią znalezienie najlepszego rozwiązania.

## <a name="mobile-experience"></a>Środowisko mobilne

W pierwszym etapie środowiska otoczenia użytkownik przechodzi poza komputer. Obecnie konsumenci i specjaliści biznesowi przechodzą płynnie między urządzeniami przenośnymi i komputerami. Każda z platform lub urządzeń używanych przez klienta tworzy nowe potencjalne środowisko. Dodanie środowiska mobilnego, które rozszerza podstawowe rozwiązanie, jest najszybszym sposobem na poprawę integracji z bezpośrednim otoczeniem klienta. Chociaż urządzenie przenośne jest daleko od otoczenia, może być bliżej punktu widzenia klienta.

Gdy klienci są często urządzeniami mobilnymi i zmianami, które mogą reprezentować najbardziej odpowiednią formę środowiska otoczenia dla danego rozwiązania. W ciągu ostatniej dekady innowacje były często wyzwalane przez integrację istniejących rozwiązań z doświadczeniem mobilnym.

Azure App Service jest doskonałym przykładem tego podejścia. Podczas wczesnych iteracji [Funkcja aplikacji sieci web Azure App Service](https://docs.microsoft.com/azure/app-service/overview) może służyć do testowania hipotezy. Ponieważ te rzeczy stają się bardziej skomplikowane, [Funkcja aplikacji mobilnej Azure App Service](https://docs.microsoft.com/azure/app-service-mobile) może rozciągnąć aplikację sieci Web na wiele platform mobilnych.

## <a name="mixed-reality"></a>Rzeczywistość mieszana

Rozwiązania rzeczywistości mieszanej reprezentują następny poziom dojrzałości dla środowisk otoczenia. To podejście rozszerza lub replikuje otoczenie danego klienta. tworzy rozszerzenie rzeczywistość dla klienta do działania w ramach programu.

> [!IMPORTANT]
> Jeśli urządzenie rzeczywistości wirtualnej (VR) jest wymagane i *nie jest jeszcze częścią bezpośrednio otaczających lub naturalnych zachowań klienta*, zwiększone lub wirtualne rzeczywistość jest bardziej alternatywnym doświadczeniem i mniejszą funkcjonalnością otoczenia.

Środowiska o rzeczywistości mieszanej są coraz częściej spotykane wśród zdalnych pracowników. Ich użycie rośnie jeszcze szybciej w branżach, które wymagają współpracy lub specjalistycznych umiejętności, które nie są łatwo dostępne na rynku lokalnym. Sytuacje wymagające scentralizowanej obsługi dla złożonego produktu dla zdalnej siły robocizny są szczególnie niedrogie dla rzeczywistości rozszerzonej. W tych scenariuszach centralny zespół pomocy technicznej i pracownicy zdalni mogą korzystać z zwiększonej rzeczywistości, aby korzystać z produktu, rozwiązywać problemy i instalować go.

Rozważmy na przykład przypadek zakotwiczenia przestrzennego. Kotwice przestrzenne umożliwiają tworzenie środowisk o rzeczywistości mieszanej z obiektami, które utrzymują swoje lokalizacje na różnych urządzeniach w miarę upływu czasu. Dzięki zakotwiczeniem przestrzennym można przechwytywać, rejestrować i utrwalać konkretne zachowanie, a tym samym zapewnić środowisko otoczenia podczas następnego działania użytkownika w tym środowisku. [Kotwice przestrzenne platformy Azure](https://docs.microsoft.com/azure/spatial-anchors/overview) to usługa, która przenosi tę logikę do chmury, umożliwiając udostępnianie środowisk między urządzeniami, a nawet w różnych rozwiązaniach.

## <a name="integrated-reality"></a>Rzeczywistość zintegrowana

Poza rzeczywistością mobilną lub nawet z rzeczywistości mieszanej jest w rzeczywistości zintegrowane. Celem zintegrowanej rzeczywistości jest całkowite usuwanie środowiska cyfrowego. Wszystko to jest urządzeniami z możliwościami obliczeniowymi i łącznością. Te urządzenia mogą służyć do zbierania danych z bezpośredniego otoczenia bez konieczności dotknięcia urządzenia telefonu, laptopa lub VR.

To środowisko jest idealne, gdy pewna postać urządzenia jest spójna w obrębie tego samego otoczenia, w którym występuje klient. Typowe scenariusze obejmują piętra fabryki, windy i nawet samochód. Te typy dużych urządzeń zawierają już moc obliczeniową. Możesz również użyć danych z urządzenia w celu wykrycia zachowań klienta i wysłania tych zachowań do chmury. Ten automatyczny przechwycenie danych dotyczących zachowania klienta znacznie zmniejsza potrzebę wprowadzenia danych przez klienta. Ponadto środowisko sieci Web, urządzenia przenośne lub VR może działać jako pętla opinii umożliwiająca udostępnianie informacji uzyskanych na podstawie zintegrowanego rozwiązania rzeczywistość.

Przykładem zintegrowanej rzeczywistości na platformie Azure mogą być:

- [Rozwiązania azure Internet rzeczy (IoT)](https://docs.microsoft.com/azure/iot-fundamentals)to zbiór usług na platformie Azure, które mogą pomóc w zarządzaniu urządzeniami i przepływie danych z tych urządzeń do chmury oraz z powrotem do użytkowników końcowych.
- [Azure Sphere](https://docs.microsoft.com/azure-sphere), połączenie sprzętu i oprogramowania. Azure Sphere to bezpieczny sposób na umożliwienie istniejącemu urządzeniu bezpiecznego przesyłania danych między urządzeniem a rozwiązaniami Azure IoT.
- [Usługa Azure urządzenia Kinect Developers Kit](https://docs.microsoft.com/azure/Kinect-dk), czujniki AI z zaawansowaną obsługą komputerów i modelami mowy. Czujniki te umożliwiają zbieranie danych wizualnych i dźwiękowych z bezpośredniego otoczenia i podawanie tych wejść do rozwiązania.

Możesz użyć wszystkich trzech z tych narzędzi do zbierania danych z otoczenia naturalnego i w punktach potrzeb klienta. W takim przypadku rozwiązanie może odpowiedzieć na te dane wejściowe, aby rozwiązać ten problem, czasami zanim klient nie wie, że wystąpiło wyzwalacz dla tego programu.

## <a name="adjusted-reality"></a>Rzeczywistość dostosowana

Najwyższą postać środowiska otoczenia jest korekta rzeczywistości, często nazywana _analizą otoczenia_. Dostosowana rzeczywistość to podejście do użycia informacji z rozwiązania, aby zmienić rzeczywistość klienta bez konieczności bezpośredniej współpracy z aplikacją. W tym podejściu aplikacja, która początkowo została skompilowana w celu udowodnienia hipotezy, może już nie mieć znaczenia. Zamiast tego urządzenia w środowisku pomagają w modulacji danych wejściowych i wyjściowych, aby zaspokoić potrzeby klientów.

Wirtualne Asystenci i inteligentne głośniki oferują doskonałe przykłady o regulowanej rzeczywistości. Samo, inteligentny głośnik to przykład prostego zintegrowanej rzeczywistości. Należy jednak dodać inteligentnego światła i czujnika ruchu do rozwiązania do obsługi głośników inteligentnych i łatwo utworzyć podstawowe rozwiązanie, które włącza lampy po wprowadzeniu pokoju.

Piętra fabryki na całym świecie zapewniają dodatkowe przykłady o regulowanej rzeczywistości. W przypadku wczesnych etapów zintegrowanej rzeczywistości czujniki na urządzeniach wykryły warunki, takie jak nadgrzanie, a następnie powiadamiają ludzi za pomocą aplikacji. W przypadku skorygowanej rzeczywistości klient może nadal uczestniczyć, ale pętla opinii jest ściśle. W pozostałej fabryce fabryki, jedno urządzenie może wykrywać nadgrzanie na żywotnym komputerze w miejscu i w linii montażowej. Drugie urządzenie znacznie spowalnia produkcję w innym miejscu, aby umożliwić jej chłodnie, a następnie wznowienie pełnego tempa po rozwiązaniu problemu. W takiej sytuacji klient jest uczestnikiem drugiej strony. Klient korzysta z aplikacji, aby ustawić reguły i zrozumieć, jak te reguły mają wpływ na produkcję, ale nie są one konieczne w przypadku pętli opinii.

W przypadku usług platformy Azure opisanych w ramach [rozwiązań usługi azure Internet rzeczy (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](https://docs.microsoft.com/azure-sphere)i [zestawu deweloperów urządzenia Kinect platformy Azure](https://docs.microsoft.com/azure/Kinect-dk) mogą być składniki rozwiązania o regulowanej rzeczywistości. Oryginalna aplikacja i logika biznesowa będą następnie stanowić pośrednika między danymi wejściowymi środowiska a zmianą, która powinna zostać wprowadzona w środowisku fizycznym.

Cyfrowy dwuosiowy to kolejny przykład o regulowanej rzeczywistości. Termin ten odnosi się do cyfrowej reprezentacji urządzenia fizycznego, prezentowanego za pomocą formatów komputera, mobilnego lub mieszanego. W przeciwieństwie do mniej rozbudowanych modeli 3W, dwucyfrowe sznurki odzwierciedlają dane zbierane z rzeczywistego urządzenia w środowisku fizycznym. To rozwiązanie umożliwia użytkownikowi posługiwanie się reprezentacją cyfrową w sposób, który nie może być nigdy wykonywany w świecie rzeczywistym. W tym podejściu urządzenia fizyczne dostosowują środowisko rzeczywistości mieszanej. Jednak rozwiązanie nadal zbiera dane z rozwiązania zintegrowanej rzeczywistości i używa tych danych do kształtowania rzeczywistości bieżącego otoczenia klienta.

Na platformie Azure Digital bliźniaczych reprezentacji są tworzone i dostępne za pomocą usługi o nazwie [Azure Digital bliźniaczych reprezentacji](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Następne kroki

Teraz, gdy masz jeszcze lepszy wgląd w interakcje urządzeń i środowisko otoczenia, które jest odpowiednie dla Twojego rozwiązania, możesz zapoznać się z ostateczną dyscypliną innowacji, [przewidywaniam i wpływem](./predict.md).

> [!div class="nextstepaction"]
> [Przewidywanie i wpływ](./predict.md)
