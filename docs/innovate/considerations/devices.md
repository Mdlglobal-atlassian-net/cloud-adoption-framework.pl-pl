---
title: 'Innowacje w chmurze: Współpracuj z urządzeniami'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wprowadzenie do innowacji w chmurze — Współpracuj z urządzeniami
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: innovate
ms.openlocfilehash: 5a9ec9f38d89683482d7f98923aa0ef2ccf201b9
ms.sourcegitcommit: f3371811a36e12533ecbc3aa936e2a68e0cee25f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/21/2019
ms.locfileid: "72683218"
---
# <a name="ambient-experiences-interact-with-devices"></a>Środowiska otoczenia: korzystanie z urządzeń

Podczas [kompilowania przy użyciu empatię](./build.md)omówione zostały trzy testy prawdziwych innowacji: Rozwiąż potrzebę klienta, powracaj do klienta, skalując w oparciu o podstawę klienta kohorty. Każdy test hipotezy będzie wymagał nakładu pracy i iteracji na podejście do wdrożenia. W tym artykule przedstawiono szczegółowe informacje na temat niektórych zaawansowanych metod zmniejszania tego nakładu pracy przez **środowisko otoczenia**. W przypadku korzystania z urządzeń, a nie aplikacji, klient może być bardziej prawdopodobnie do rozwiązania w celu spełnienia ich potrzeby.

## <a name="ambient-experiences"></a>Środowiska otoczenia

Środowisko otoczenia to środowisko cyfrowe, które odnosi się do bezpośredniego otoczenia. Rozwiązanie, które oferuje funkcje otoczenia, dąży do zaspokojenia klienta w razie potrzeby. Gdy jest to możliwe, rozwiązanie spełnia wymagania klienta bez opuszczania naturalnego przepływu, w jakim się znajdują.

Żywotność w gospodarce cyfrowej jest całkowicie odwracania. Wszyscy jesteśmy bombarded z wiadomościami społecznościowymi, wiadomościami e-mail, sieciami Web, wizualizacją i werbalnymi, z których każdy jest ryzykiem odwracania. Ryzyko odwracania zwiększa się co sekundę między punktem klienta i interakcją z rozwiązaniem. Niezliczone klienci są Tracon w krótkim czasie. Aby wzrosnąć wdrożenie powtarzania, zmniejsz liczbę rozpraszań, skracając czas do rozwiązania (TTS).

## <a name="interacting-with-devices"></a>Korzystanie z urządzeń

Standardowe środowisko sieci Web to najpopularniejsza technika tworzenia aplikacji używana do zaspokajania potrzeb klienta. Założenie rozszerzania na to podejście polega na tym, że klient będzie przed komputerem. Jeśli klient spójnie zaspokaja swój punkt potrzebny przed laptopem, Utwórz aplikację internetową. Ta aplikacja sieci Web zapewni "środowisko otoczenia" dla tego klienta w tym scenariuszu. Jednak wiemy, że ten scenariusz jest coraz bardziej prawdopodobnie w nowoczesnej społeczeństwie.

![Środowiska otoczenia](../../_images/innovate/ambient-experiences.png)

Środowiska otoczenia, jak pokazano powyżej, zwykle wymagają więcej niż aplikacji sieci Web. Poprzez [pomiar](./measure.md) i [uczenie się z klientem](./learn.md) zachowanie, które prowadzi do wymaganego wyzwalacza klienta, może być zaobserwowane, śledzone i używane do tworzenia większej otoczenia środowiska. Poniżej przedstawiono podsumowanie kilku metod integracji rozwiązań otoczenia z poszczególnymi zadziałami, więcej szczegółowych informacji na temat każdego z poniższych akapitów.

- **[Środowisko mobilne](#mobile-experience)** : podobnie jak laptop, aplikacje mobilne są zwykle częścią otoczenia klientów. W niektórych scenariuszach może to zapewnić odpowiedni poziom interakcji, aby zapewnić otoczenie rozwiązania.
- **[Rzeczywistość mieszana](#mixed-reality):** Czasami otoczenie naturalne klienta należy zmienić, aby zapewnić interakcję. Powoduje to utworzenie bitu fałszywej rzeczywistości, w której klient może współtworzyć z rozwiązaniem i musi być spełniony. W takim przypadku rozwiązanie jest otaczające wartość false.
- **[Rzeczywistość zintegrowana](#integrated-reality):** Przechodzenie bliżej Ambience, zintegrowane rozwiązania o rzeczywistości koncentrują się na użyciu urządzenia, które istnieje w rzeczywistości klienta, aby zintegrować rozwiązanie z naturalnymi zachowaniami. Wirtualny asystent to doskonały przykład integracji rzeczywistości z otaczającym środowiskiem. Bardzo znana opcja polega na użyciu technologii Internet rzeczy (IoT) do integrowania urządzeń, które już istnieją w otoczeniu klienta.
- **[Zastosowana rzeczywistość](#adjusted-reality):** Jeśli którekolwiek z rozwiązań otoczenia powyżej używa analizy predykcyjnej w chmurze do definiowania i zapewnienia interakcji z klientem w naturalnym otoczeniu, rozwiązanie ma rzeczywistość o regulowanej rzeczywistości.

Zrozumienie potrzeb klientów i mierzenie wpływu klientów pomoże w ustaleniu, czy w celu zweryfikowania hipotez w celu pomyślnego zapoznania się z informacjami na temat interakcji z urządzeniem lub otoczenia. W przypadku każdego z tych punktów danych następujące sekcje ułatwią znalezienie najlepszego rozwiązania.

## <a name="mobile-experience"></a>Środowisko mobilne

Pierwszym etapem środowiska otoczenia jest przejście do komputera. Obecnie konsumenci i specjaliści biznesowi przechodzą płynnie między urządzeniami przenośnymi i komputerami. Każda z platform lub urządzeń używanych przez klienta tworzy nowe potencjalne środowisko dla klienta. Dodanie środowiska mobilnego, które rozszerza podstawowe rozwiązanie, jest najszybszym sposobem na poprawę integracji z bezpośrednim otoczeniem klienta. Chociaż urządzenie przenośne jest daleko od otoczenia, może okazać się bliżej punktu widzenia klienta.

Gdy klienci są często mobilni i zmieniają lokalizacje, może to być najbardziej odpowiednia postać środowiska otoczenia dla danego rozwiązania. Jednym ze wspólnych źródeł innowacji w stosunku do ostatniej dekady jest rozszerzenie istniejących rozwiązań w celu zintegrowania środowiska mobilnego.

Przykłady tego podejścia mogą być widoczne w usłudze Azure App Services. Podczas wczesnych iteracji [Funkcja aplikacji sieci web Azure App Service](/azure/app-service/overview) może służyć do testowania hipotezy. Ponieważ te rzeczy stają się bardziej złożone, [Funkcja aplikacji mobilnej platformy Azure App Services](/azure/app-service-mobile/) może rozłożyć aplikację sieci Web na wiele platform mobilnych.

## <a name="mixed-reality"></a>Rzeczywistość mieszana

Następnym poziomem dojrzałości dla środowiska otoczenia jest rozszerzanie lub replikacja otoczenia klienta za pomocą rozwiązań rzeczywistości mieszanej. W tym podejściu rozwiązanie przestało się bardziej otaczające przez utworzenie rozszerzenia rzeczywistość dla klienta do działania w ramach programu.

> [!IMPORTANT]
> Jeśli urządzenie rzeczywistości wirtualnej (VR) jest wymagane i *nie jest jeszcze częścią zachowań bezpośrednio otaczających lub naturalnych*, oznacza to, że rzeczywistości rozszerzone/wirtualne są bardziej alternatywnym doświadczeniem i mniejszą funkcjonalnością otoczenia.

Ta forma doświadczenia jest coraz większa dla pracowników zdalnych. Korzystanie z tych środowisk rośnie jeszcze szybciej w branżach, które wymagają współpracy z umiejętnościami specjalistycznymi, które nie są łatwo dostępne na rynku lokalnym. Typowym scenariuszem wymagającym rzeczywistości rozszerzonej w ramach naturalnego zachowania jest Scentralizowana obsługa wdrożenia złożonego produktu dla zdalnej siły zawodowej. W tych scenariuszach centralny zespół pomocy technicznej i pracownik zdalny mogą korzystać z zwiększonej rzeczywistości do rozwiązywania problemów lub instalowania produktu.

W przypadku scenariusza powyżej lub innych podobnych scenariuszy przykładem środowiska otoczenia jest użycie kotwic przestrzennych. Kotwice przestrzenne umożliwiają tworzenie środowisk o rzeczywistości mieszanej z obiektami, które utrzymują swoją lokalizację na różnych urządzeniach w miarę upływu czasu. Dzięki zakotwiczeniem przestrzennym określone zachowanie może być przechwytywane, rejestrowane i utrwalane, co zapewnia środowisko otoczenia, przy następnym uruchomieniu użytkownika w tym środowisku. [Kotwice przestrzenne platformy Azure](https://docs.microsoft.com/azure/spatial-anchors/overview) to usługa, która przenosi tę logikę do chmury, umożliwiając udostępnianie środowisk między urządzeniami, a nawet w różnych rozwiązaniach.

## <a name="integrated-reality"></a>Rzeczywistość zintegrowana

Oprócz rzeczywistości mobilnej lub nawet w rzeczywistości mieszanej jest używana funkcja rzeczywistości zintegrowanej. W tym podejściu celem jest całkowite usuwanie środowiska cyfrowego. Wszystko to jest urządzeniami z możliwościami obliczeniowymi i łącznością. Te urządzenia mogą służyć do zbierania danych z bezpośredniego otoczenia bez konieczności dotknięcia urządzenia telefonu, laptopa lub VR.

Ta forma doświadczenia jest idealnym rozwiązaniem, gdy pewna część urządzenia jest spójna w obrębie tego samego otoczenia, w którym występuje klient. Typowe scenariusze obejmują piętra fabryki, windy, a nawet samochodów. Te typy dużych urządzeń zawierają już moc obliczeniową. Możesz również użyć danych z urządzenia w celu wykrycia zachowań klienta i wysłania tych zachowań do chmury. Ten automatyczny przechwycenie danych dotyczących zachowania klienta znacznie zmniejsza potrzebę wprowadzenia danych przez klienta. Ponadto środowisko sieci Web, urządzenia przenośne lub VR może służyć jako pętla opinii umożliwiająca udostępnianie informacji uzyskanych na podstawie zintegrowanego rozwiązania rzeczywistość.

Przykładem zintegrowanej rzeczywistości na platformie Azure mogą być:

- [Rozwiązania platformy azure Internet rzeczy (IoT)](https://docs.microsoft.com/azure/iot-fundamentals)to zbiór usług na platformie Azure, które mogą pomóc w zarządzaniu urządzeniami i przepływie danych z tych urządzeń do chmury oraz z powrotem do użytkowników końcowych.
- [Azure Sphere](/azure-sphere), połączenie sprzętu i oprogramowania, Azure Sphere to bezpieczny sposób na umożliwienie istniejącemu urządzeniu bezpiecznego przesyłania danych między urządzeniem a rozwiązaniami Azure IoT.
- [Usługa Azure urządzenia Kinect Developers Kit](https://docs.microsoft.com/azure/Kinect-dk), czujniki AI z zaawansowaną obsługą komputerów i modelami mowy, które mogą zbierać dane wizualizacji i dźwięku z bezpośredniego otoczenia oraz dostarczać te wejścia do rozwiązania.

Wszystkie trzy mogą służyć do zbierania danych w naturalnym otoczeniu, w punkcie potrzeb klienta. W takim przypadku rozwiązanie może odpowiedzieć na te dane wejściowe, aby rozwiązać ten problem, czasami zanim klient nie wie, że wystąpiło wyzwalacz dla tego programu.

## <a name="adjusted-reality"></a>Rzeczywistość skorygowana

Najwyższą postać środowiska otoczenia jest korekta rzeczywistości, często nazywana analizą otoczenia. Rzeczywistość o regulowanej rzeczywistości to podejście do korzystania z informacji z rozwiązania, aby zmienić jego rzeczywistość, bez konieczności bezpośredniej współpracy z aplikacją. W tym podejściu aplikacja, która początkowo została skompilowana w celu udowodnienia hipotezy, może nie mieć już znaczenia. Zamiast tego urządzenia w środowisku ułatwią dane wejściowe i wyjściowe, aby zaspokoić potrzeby klientów.

Wirtualne Asystenci/inteligentne głośniki mogą zapewnić doskonały przykład o regulowanej rzeczywistości. Samo, inteligentny głośnik to przykład prostego zintegrowanej rzeczywistości. Dodawaj inteligentne światło i czujnik ruchu do rozwiązania inteligentnego głośnika i łatwo jest utworzyć podstawowe rozwiązanie z włączaniem świateł po wprowadzeniu pokoju.

Piętra fabryki na całym świecie zapewniają dodatkowe scenariusze o regulowanej rzeczywistości. Podczas wczesnych etapów zintegrowanej rzeczywistości czujniki na urządzeniach wykryły warunki, takie jak przegrzanie i zgłosiły potrzebę zmiany przez człowieka za pośrednictwem aplikacji. W przypadku niezmienionej rzeczywistości klient może nadal uczestniczyć w tym programie. Jednak pętla opinii jest ściśle. W pozostałej fabryce fabryki, jedno urządzenie będzie wykrywać nadgrzanie na żywotnym komputerze w obrębie linii montażowej. W innym miejscu, drugie urządzenie może nieco powolnić produkcję, aby umożliwić komputerowi chłodnie i wznowienie w czasie, gdy warunek został rozwiązany. W tym scenariuszu klient jest członkiem drugiej strony. Klient korzysta z aplikacji, aby ustawić reguły i zrozumieć, jak te reguły mają wpływ na produkcję, ale nie jest to wymagane części pętli opinii.

Usługi platformy Azure w poprzedniej sekcji, [rozwiązania azure Internet rzeczy (IoT)](https://docs.microsoft.com/azure/iot-fundamentals), [Azure Sphere](/azure-sphere)i [zestaw deweloperów urządzenia Kinect platformy Azure](https://docs.microsoft.com/azure/Kinect-dk) mogą być składnikami rozwiązania o regulowanej rzeczywistości. Oryginalna aplikacja i logika biznesowa będą stanowić pośrednika między danymi wejściowymi środowiska a zmianą, którą należy wykonać w środowisku fizycznym.

Innym przykładem o regulowanej rzeczywistości jest utworzenie dwucyfrowej sieci, która jest reprezentacją elektroniczną urządzenia fizycznego, prezentowaną przez komputery, urządzenia przenośne lub formaty o rzeczywistości mieszanej. W przeciwieństwie do mniej rozbudowanych modeli 3W, dwucyfrowe sznurki odzwierciedlają dane zbierane z rzeczywistego urządzenia w środowisku fizycznym. Pozwala to użytkownikowi na posługiwanie się reprezentacją cyfrową w sposób, który nie może być nigdy wykonywany w świecie rzeczywistym. W ten sposób urządzenia fizyczne dostosowują środowisko rzeczywistości mieszanej. Jednak rozwiązanie nadal zbiera dane z rozwiązania zintegrowanej rzeczywistości i korzysta z tego, aby kształtować rzeczywistość bieżącego otoczenia klienta.

Na platformie Azure Digital bliźniaczych reprezentacji są tworzone i dostępne za pomocą usługi o nazwie [Azure Digital bliźniaczych reprezentacji](https://docs.microsoft.com/azure/digital-twins/about-digital-twins).

## <a name="next-steps"></a>Następne kroki

Dzięki dokładniejszemu zrozumieniu interakcji z urządzeniami i otoczenia, który jest właściwy dla Twojego rozwiązania, możesz teraz zapoznać się z ostateczną dyscypliną innowacji, [przewidywaniam i wpływem](./predict.md).

> [!div class="nextstepaction"]
> [Przewidywanie i wpływ](./predict.md)
