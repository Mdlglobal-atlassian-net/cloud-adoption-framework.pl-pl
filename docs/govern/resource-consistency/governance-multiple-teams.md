---
title: Projekt ładu na platformie Azure dla wielu zespołów
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Wskazówki dotyczące konfigurowania kontrolek ładu platformy Azure dla wielu zespołów, wielu obciążeń i wielu środowisk.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d6a21e852ff44a9036f2fbb9d0d0e60a0f4c930f
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223957"
---
# <a name="governance-design-for-multiple-teams"></a>Projekt nadzoru dla wielu zespołów

Celem tych wskazówek jest ułatwienie poznania procesu projektowania modelu zarządzania zasobami na platformie Azure w celu obsługi wielu zespołów, wielu obciążeń i wielu środowisk. Najpierw zapoznaj się z zestawem hipotetycznych wymagań ładu, a następnie przejdź do kilku przykładowych implementacji, które spełniają te wymagania.

Wymagania są następujące:

- Firma planuje przenieść nowe role w chmurze i obowiązki do zestawu użytkowników, a tym samym wymaga zarządzania tożsamościami dla wielu zespołów z różnymi potrzebami dostępu do zasobów na platformie Azure. Ten system zarządzania tożsamościami jest wymagany do przechowywania tożsamości następujących użytkowników:
  - Osoby w organizacji odpowiedzialne za własność **subskrypcji**.
  - Osoby w organizacji odpowiedzialne za **udostępnione zasoby infrastruktury** używane do łączenia sieci lokalnej z siecią wirtualną platformy Azure.
  - Dwie osoby w organizacji odpowiedzialne za zarządzanie **obciążeniem**.
- Obsługa wielu **środowisk**. Środowisko to logiczne grupowanie zasobów, takich jak maszyny wirtualne, sieci wirtualne i usługi routingu ruchu sieciowego. Te grupy zasobów mają podobne wymagania dotyczące zarządzania i zabezpieczeń i są zwykle używane do określonego celu, takiego jak testowanie lub produkcja. W tym przykładzie wymagania dotyczą czterech środowisk:
  - **Udostępnione środowisko infrastruktury** , które obejmuje zasoby współużytkowane przez obciążenia w innych środowiskach. Na przykład Sieć wirtualna z podsiecią bramy, która zapewnia łączność z lokalnymi.
  - **Środowisko produkcyjne** z najbardziej restrykcyjnymi zasadami zabezpieczeń. Może obejmować obciążenia wewnętrzne lub zewnętrzne.
  - **Środowisko produkcyjne** na potrzeby projektowania i testowania. To środowisko ma zabezpieczenia, zgodność i zasady dotyczące kosztów, które różnią się od tych w środowisku produkcyjnym. Na platformie Azure ma to formę subskrypcji Enterprise — tworzenie i testowanie.
  - **Środowisko piaskownicy** do weryfikacji koncepcji i celów edukacyjnych. To środowisko jest zwykle przypisywany dla pracowników uczestniczących w działaniach programistycznych i ma ścisłe procedury i funkcjonalne mechanizmy kontroli bezpieczeństwa, aby zapobiec wyładunku danych firmowych w tym miejscu. Na platformie Azure mają one formę subskrypcji programu Visual Studio. Te subskrypcje _nie_ powinny również być powiązane z Azure Active Directoryami przedsiębiorstwa.
- **Model uprawnień o** najniższych uprawnieniach, w którym użytkownicy domyślnie nie mają uprawnień. Model musi obsługiwać następujące elementy:
  - Pojedynczy zaufany użytkownik (konto usługi quasi) w zakresie subskrypcji z uprawnieniami do przypisywania praw dostępu do zasobów.
  - Każdy właściciel obciążenia domyślnie odmówił dostępu do zasobów. Prawa dostępu do zasobów są udzielane jawnie przez jednego zaufanego użytkownika w zakresie grupy zasobów.
  - Dostęp do zarządzania zasobami infrastruktury udostępnionej ograniczony do właścicieli infrastruktury udostępnionej.
  - Dostęp do zarządzania dla każdego obciążenia ograniczonego do właściciela obciążenia (w środowisku produkcyjnym) i zwiększenia poziomu kontroli w miarę rozwoju zwiększa się od dev do testowania do etapu produkcyjnego.
  - Przedsiębiorstwo nie chce, aby zarządzać rolami niezależnie w każdym z trzech głównych środowisk i w związku z tym wymagało użycia tylko [wbudowanych ról](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) dostępnych w kontroli dostępu opartej na ROLACH (RBAC) na platformie Azure. Jeśli w przedsiębiorstwie absolutnie wymagane są niestandardowe role RBAC, do synchronizowania ról niestandardowych w trzech środowiskach wymagane są dodatkowe procesy.
- Śledzenie kosztów według nazwy właściciela obciążenia, środowiska lub obu tych funkcji.

## <a name="identity-management"></a>Zarządzanie tożsamościami

Aby można było zaprojektować Zarządzanie tożsamościami dla modelu ładu, ważne jest, aby zrozumieć cztery główne obszary, które obejmują:

- **Administracyjnego** Procesy i narzędzia służące do tworzenia, edytowania i usuwania tożsamości użytkowników.
- **Ponowne** Weryfikowanie tożsamości użytkownika przez sprawdzenie poprawności poświadczeń, takich jak nazwa użytkownika i hasło.
- **Authorization:** Określanie zasobów, do których uwierzytelniony użytkownik może uzyskać dostęp lub jakie operacje mają uprawnienia do wykonywania.
- **Kontroli** Okresowe przeglądanie dzienników i innych informacji w celu odnalezienia problemów z zabezpieczeniami związanych z tożsamością użytkownika. Obejmuje to przeglądanie podejrzanych wzorców użycia, okresowe przeglądanie uprawnień użytkowników w celu sprawdzenia, czy są one dokładne, oraz innych funkcji.

Istnieje tylko jedna usługa zaufana przez platformę Azure dla tożsamości, która jest Azure Active Directory (Azure AD). Będziesz dodawać użytkowników do usługi Azure AD i korzystać z niej we wszystkich wymienionych powyżej funkcjach. Jednak przed rozpoczęciem konfigurowania usługi Azure AD ważne jest zapoznanie się z kontami uprzywilejowanymi, które są używane do zarządzania dostępem do tych usług.

Gdy Twoja organizacja zarejestrowano na potrzeby konta platformy Azure, przypisano co najmniej jednego **właściciela konta** platformy Azure. Ponadto zostanie utworzona dzierżawa usługi Azure AD, chyba że istniejąca dzierżawa jest już skojarzona z innymi usługami firmy Microsoft, takimi jak Office 365. Podczas tworzenia skojarzono **administratora globalnego** z pełnymi uprawnieniami w dzierżawie usługi Azure AD.

Tożsamości użytkowników zarówno dla właściciela konta platformy Azure, jak i administratora globalnego usługi Azure AD są przechowywane w wysoce zabezpieczonym systemie tożsamości, który jest zarządzany przez firmę Microsoft. Właściciel konta platformy Azure jest autoryzowany do tworzenia, aktualizowania i usuwania subskrypcji. Administrator globalny usługi Azure AD jest autoryzowany do wykonywania wielu działań w usłudze Azure AD, ale w przypadku tego przewodnika projektowego należy skoncentrować się na tworzeniu i usuwaniu tożsamości użytkownika.

> [!NOTE]
> Twoja organizacja może już mieć istniejącą dzierżawę usługi Azure AD, jeśli istnieje skojarzona z kontem licencję Office 365, Intune lub Dynamics.

Właściciel konta platformy Azure ma uprawnienia do tworzenia, aktualizowania i usuwania subskrypcji:

![Konto platformy Azure z menedżerem kont platformy Azure i administratorem](../../_images/govern/design/governance-3-0.png)
globalnym usługi Azure AD*rysunek 1 — konto platformy Azure z menedżerem kont i administratorem globalnym usługi Azure AD.*

**Administrator globalny** usługi Azure AD ma uprawnienia do tworzenia kont użytkowników:

![Konto platformy Azure z menedżerem kont platformy Azure i administratorem](../../_images/govern/design/governance-3-0a.png)
globalnym usługi Azure AD*rysunek 2 — Administrator globalny usługi Azure AD tworzy wymagane konta użytkowników w dzierżawie.*

Pierwsze dwa konta, **właściciel obciążenia APP1** i **właściciel obciążenia APP2** są skojarzone z osobą w organizacji odpowiedzialną za zarządzanie obciążeniem. Konto **operacji sieci** należy do osoby odpowiedzialnej za udostępnione zasoby infrastruktury. Na koniec konto **właściciela subskrypcji** jest powiązane z osobą odpowiedzialną za własność subskrypcji.

## <a name="resource-access-permissions-model-of-least-privilege"></a>Uprawnienia dostępu do zasobów — model najniższych uprawnień

Po utworzeniu systemu zarządzania tożsamościami i kontami użytkowników należy zdecydować, jak zastosować role kontroli dostępu opartej na rolach (RBAC) do poszczególnych kont w celu obsługi modelu uprawnień o najniższych uprawnieniach.

Istnieje również inne wymaganie, aby wszystkie zasoby skojarzone z poszczególnymi obciążeniami były od siebie odizolowane, dzięki czemu żaden właściciel obciążenia ma dostęp do innych obciążeń, które nie są właścicielami. Istnieje również wymóg implementacji tego modelu przy użyciu tylko wbudowanych ról dla kontroli dostępu opartej na rolach platformy Azure.

Każda rola RBAC jest stosowana w jednym z trzech zakresów na platformie Azure: **subskrypcja**, **Grupa zasobów**, a następnie pojedynczy **zasób**. Role są dziedziczone w niższych zakresach. Jeśli na przykład użytkownik ma przypisaną [rolę właściciela wbudowane](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) na poziomie subskrypcji, ta rola jest również przypisywana do tego użytkownika w grupie zasobów i na poziomie poszczególnych zasobów, chyba że zostanie zastąpiona.

W związku z tym, aby utworzyć model dostępu o najniższych uprawnieniach, należy podjąć decyzję o działaniach, które określony typ użytkownika może wykonać w każdym z tych trzech zakresów. Na przykład wymaganie właściciela obciążenia ma uprawnienia do zarządzania dostępem tylko do zasobów skojarzonych z ich obciążeniem i bez innych. Jeśli przypiszesz wbudowaną rolę właściciela w zakresie subskrypcji, każdy właściciel obciążenia będzie miał dostęp do wszystkich obciążeń.

Przyjrzyjmy się dwóm przykładowym modelom uprawnień do lepszego zrozumienia tego pojęcia. W pierwszym przykładzie model ufa tylko administratorowi usługi do tworzenia grup zasobów. W drugim przykładzie model przypisuje wbudowaną rolę właściciela do każdego właściciela obciążenia w zakresie subskrypcji.

W obu przykładach istnieje administrator usługi subskrypcji, który ma przypisaną rolę właściciela wbudowanego w zakresie subskrypcji. Odwołaj, że wbudowana rola właściciela przyznaje wszystkie uprawnienia, w tym zarządzanie dostępem do zasobów.
![Administrator usługi subskrypcji z rolą](../../_images/govern/design/governance-2-1.png)
właściciela*rysunek 3 — subskrypcja z administratorem usługi przypisaną rolę właściciela wbudowanego.*

1. W pierwszym przykładzie istnieje **właściciel obciążenia A** bez uprawnień w zakresie subskrypcji — domyślnie nie ma uprawnień do zarządzania dostępem do zasobów. Ten użytkownik chce wdrożyć zasoby i zarządzać nimi w ramach obciążenia. Należy skontaktować się z **administratorem usługi** , aby zażądać utworzenia grupy zasobów.
    ![Właściciel obciążenia żąda utworzenia grupy zasobów A](../../_images/govern/design/governance-2-2.png)
2. **Administrator usługi** przegląda swoje żądanie i tworzy **grupę zasobów a**. W tym momencie **właściciel obciążenia** nadal nie ma uprawnień do wykonywania żadnych czynności.
    ![Administrator usługi tworzy grupę zasobów A](../../_images/govern/design/governance-2-3.png)
3. **Administrator usługi** dodaje **właściciela obciążenia a** do **grupy zasobów** a i przypisuje wbudowaną [rolę współautor](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Rola współautor przyznaje wszystkie uprawnienia do **grupy zasobów A,** z wyjątkiem zarządzania uprawnieniami dostępu.
    ![Administrator usługi dodaje właściciela obciążenia a do grupy zasobów a](../../_images/govern/design/governance-2-4.png)
4. Załóżmy, że **właściciel obciążenia a** ma wymóg dla pary członków zespołu do wyświetlania danych monitorowania procesora i ruchu sieciowego w ramach planowania pojemności dla obciążenia. Ponieważ **właściciel obciążenia A** ma przypisaną rolę współautor, nie ma uprawnień do dodawania użytkownika do **grupy zasobów A**. Muszą wysłać to żądanie do **administratora usługi**.
    ![Właściciele obciążenia żądają współautorów obciążeń do grupy zasobów](../../_images/govern/design/governance-2-5.png)
5. **Administrator usługi** przegląda żądanie i dodaje dwóch użytkowników współautorów **obciążenia** do **grupy zasobów a**. Żaden z tych dwóch użytkowników nie wymaga uprawnień do zarządzania zasobami, więc ma przypisaną [wbudowaną rolę czytnika](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor).
    ![Administrator usługi dodaje współautorów obciążeń do grupy zasobów A](../../_images/govern/design/governance-2-6.png)
6. Następnie **właściciel obciążenia B** wymaga również grupy zasobów, aby zawierała zasoby związane z obciążeniem. Podobnie jak w przypadku **właściciela obciążenia A**, **właściciel obciążenia B** początkowo nie ma uprawnień do wykonania akcji w zakresie subskrypcji, dlatego musi wysłać żądanie do **administratora usługi**.
    ![Właściciel obciążenia B żąda utworzenia grupy zasobów B](../../_images/govern/design/governance-2-7.png)
7. **Administrator usługi** przegląda żądanie i tworzy **grupę zasobów B**.  ![Administrator usługi tworzy grupę zasobów B](../../_images/govern/design/governance-2-8.png)
8. **Administrator usługi** dodaje następnie **właściciela obciążenia b** do **grupy zasobów b** i przypisuje wbudowaną rolę współautor.
    ![Administrator usługi dodaje właściciela obciążenia B do grupy zasobów B](../../_images/govern/design/governance-2-9.png)

W tym momencie każdy właściciel obciążenia jest izolowany w ich własnej grupie zasobów. Żaden z właścicieli obciążeń lub ich członkowie zespołu nie mają dostępu do zasobów w żadnej innej grupie zasobów.

![subskrypcja z grupami zasobów a i](../../_images/govern/design/governance-2-10.png)
B*rysunek 4 — subskrypcja z dwoma właścicielami obciążeń izolowanych z ich własną grupą zasobów.*

Ten model jest modelem&mdash;najniższych uprawnień, do którego każdy użytkownik ma przypisane odpowiednie uprawnienia w prawidłowym zakresie zarządzania zasobami.

Należy jednak wziąć pod uwagę, że każde zadanie w tym przykładzie zostało wykonane przez **administratora usługi**. Chociaż jest to prosty przykład i może nie być przyczyną problemu, ponieważ wystąpiły tylko dwa właściciele obciążeń, można łatwo wyobrazić typy problemów, które byłyby wynikiem dużej organizacji. Na przykład **administrator usługi** może stać się wąskim gardłem z dużą zaległością żądań, które powodują opóźnienia.

Przyjrzyjmy się drugiemu przykładowi, który zmniejsza liczbę zadań wykonywanych przez **administratora usługi**.

1. W tym modelu **właściciel obciążenia A** ma przypisaną wbudowaną rolę właściciela w zakresie subskrypcji, umożliwiając im utworzenie własnej grupy zasobów: **Grupa zasobów A**.  ![Administrator usługi dodaje właściciela obciążenia A do subskrypcji](../../_images/govern/design/governance-2-11.png)
2. Gdy **Grupa zasobów A** zostanie utworzona, **właściciel obciążenia a** jest domyślnie dodawany i dziedziczy wbudowaną rolę właściciela z zakresu subskrypcji.
    ![Właściciel obciążenia A tworzy grupę zasobów A](../../_images/govern/design/governance-2-12.png)
3. Wbudowana rola właściciela umożliwia **właścicielowi obciążenia** uprawnienie do zarządzania dostępem do grupy zasobów. **Właściciel obciążenia a** dodaje dwóch **współautorów obciążenia** i przypisuje wbudowaną rolę czytnika do każdego z nich.
    ![Właściciel obciążenia A dodaje współautorów obciążenia](../../_images/govern/design/governance-2-13.png)
4. **Administrator usługi** dodaje teraz **właściciela obciążenia B** do subskrypcji z wbudowaną rolą właściciela.
    ![Administrator usługi dodaje właścicieli obciążeń B do subskrypcji](../../_images/govern/design/governance-2-14.png)
5. **Właściciel obciążenia b** tworzy **grupę zasobów b** i jest domyślnie dodawany. Następnie **właściciel obciążenia B** dziedziczy wbudowaną rolę właściciela z zakresu subskrypcji.
    ![Właściciel obciążenia B tworzy grupę zasobów B](../../_images/govern/design/governance-2-15.png)

Należy pamiętać, że w tym modelu **administrator usługi** wykonał mniejszą liczbę akcji niż w pierwszym przykładzie z powodu delegowania dostępu do zarządzania do każdego z poszczególnych właścicieli obciążeń.

![subskrypcja z grupami zasobów a i](../../_images/govern/design/governance-2-16.png)
B*rysunek 5 — subskrypcja z uprawnieniami administratora usługi i dwóch właścicieli obciążenia, która ma przypisaną wbudowaną rolę właściciela.*

Jednak ze względu na to, że zarówno **właściciel obciążenia a** , jak i **właściciel obciążenia B** przypisuje rolę właściciela wbudowanego w zakresie subskrypcji, każdy z nich dziedziczy rolę właściciela wbudowane dla każdej grupy zasobów. Oznacza to, że użytkownicy mają pełny dostęp do zasobów jednego innego, ale mogą również delegować dostęp do zarządzania do grup zasobów każdej z nich. Na przykład **właściciel obciążenia B** ma uprawnienia do dodawania dowolnego innego użytkownika do **grupy zasobów a** i może przypisywać do nich dowolną rolę, w tym wbudowaną rolę właściciela.

W przypadku porównania każdego przykładu z wymaganiami zobaczysz, że oba przykłady obsługują jednego zaufanego użytkownika w zakresie subskrypcji z uprawnieniem do przyznawania praw dostępu do zasobów dla dwóch właścicieli obciążeń. Każdy z dwóch właścicieli obciążeń nie miał domyślnie dostępu do zarządzania zasobami i wymaga, aby **administrator usługi** jawnie przypisał do nich uprawnienia. Jednak tylko pierwszy przykład obsługuje wymaganie, aby zasoby skojarzone z poszczególnymi obciążeniami były od siebie odizolowane, dzięki czemu właściciel obciążenia nie ma dostępu do zasobów innych obciążeń.

## <a name="resource-management-model"></a>Model zarządzania zasobami

Teraz, Po zaprojektowaniu modelu uprawnień o najniższych uprawnieniach, przyjrzyjmy się, aby zapoznać się z niektórymi praktycznymi aplikacjami tych modeli ładu. Należy odwoływać się od wymagań, które muszą obsługiwać następujące trzy środowiska:

1. **Infrastruktura udostępniona:** Grupa zasobów współużytkowana przez wszystkie obciążenia. Są to takie zasoby, jak bramy sieci, zapory i usługi zabezpieczeń.
2. **Narzędzi** Wiele grup zasobów reprezentujących wiele obciążeń produkcyjnych. Te zasoby są używane do obsługi prywatnych i publicznych artefaktów aplikacji. Te zasoby zwykle mają ścisłe modele zarządzania i zabezpieczeń, aby chronić zasoby, kod aplikacji i dane przed nieautoryzowanym dostępem.
3. **Nie produkcja:** Wiele grup zasobów reprezentujących wiele gotowych obciążeń nieprodukcyjnych. Te zasoby są używane na potrzeby tworzenia i testowania tych zasobów może mieć bardziej swobodny model ładu, aby zapewnić lepszą elastyczność deweloperów. Zabezpieczenia w tych grupach powinny zwiększyć się bliżej od "produkcji" procesu tworzenia aplikacji.

Dla każdego z tych trzech środowisk istnieje wymóg śledzenia danych kosztów według **właściciela obciążenia**, **środowiska**lub obu. Oznacza to, że chcesz poznać ciągły koszt **infrastruktury udostępnionej**, koszty związane z indywidualnymi środowiskami w środowiskach **nieprodukcyjnych** i **produkcyjnych** , a wreszcie łączny koszt **nieprodukcji** **i środowisko produkcyjne**.

Wiesz już, że zasoby są objęte zakresem dwóch poziomów: **subskrypcji** i **grupy zasobów**. W związku z tym pierwsza decyzja polega na tym, jakorganizować środowiska przez subskrypcję. Dostępne są tylko dwie możliwości: pojedyncza subskrypcja lub wiele subskrypcji.

Przed zapoznaj się z przykładami każdego z tych modeli, przejdźmy do struktury zarządzania dla subskrypcji na platformie Azure.

Należy odwołać się od wymagań, które użytkownik ma w organizacji odpowiedzialnej za subskrypcje, a ten użytkownik jest właścicielem konta **właściciela subskrypcji** w dzierżawie usługi Azure AD. Jednak to konto nie ma uprawnień do tworzenia subskrypcji. Tylko **właściciel konta platformy Azure** ma uprawnienia do wykonania tej czynności:

![Właściciel konta platformy Azure tworzy](../../_images/govern/design/governance-3-0b.png)
subskrypcję*6 — właściciel konta platformy Azure tworzy subskrypcję.*

Po utworzeniu subskrypcji **właściciel konta platformy Azure** może dodać konto **właściciela subskrypcji** do subskrypcji z rolą **właściciela** :

![Właściciel konta platformy Azure dodaje konto użytkownika właściciela subskrypcji do subskrypcji z rolą właściciela. Rysunek 7. *właściciel konta platformy Azure dodaje konto użytkownika **właściciela subskrypcji** do subskrypcji z rolą **właściciela** .* ](../../_images/govern/design/governance-3-0c.png)


**Właściciel subskrypcji** może teraz tworzyć **grupy zasobów** i delegować zarządzanie dostępem do zasobów.

Najpierw przyjrzyjmy się przykładowym modelowi zarządzania zasobami przy użyciu jednej subskrypcji. Pierwsza decyzja przedstawia sposób wyrównania grup zasobów do trzech środowisk. Dostępne są dwie opcje:

1. Wyrównaj każde środowisko do pojedynczej grupy zasobów. Wszystkie udostępnione zasoby infrastruktury są wdrażane w pojedynczej grupie zasobów **infrastruktury udostępnionej** . Wszystkie zasoby skojarzone z obciążeniami programistycznymi są wdrażane w pojedynczej grupie zasobów deweloperskich. Wszystkie zasoby skojarzone z obciążeniami produkcyjnymi są wdrażane w jednej produkcyjnej grupie zasobów dla środowiska **produkcyjnego** .
2. Utwórz osobne grupy zasobów dla każdego obciążenia, używając konwencji nazewnictwa i znaczników w celu dopasowania grup zasobów do każdego z tych trzech środowisk.

Zacznijmy od oceny pierwszej opcji. Będziesz używać modelu uprawnień, który został omówiony w poprzedniej sekcji, za pomocą jednego administratora usługi subskrypcji, który tworzy grupy zasobów i dodaje do nich użytkowników przy użyciu wbudowanej roli **współautor** lub **czytnika** .

1. Pierwsza wdrożona Grupa zasobów reprezentuje środowisko **infrastruktury udostępnionej** . **Właściciel subskrypcji** tworzy grupę zasobów dla udostępnionych zasobów infrastruktury o nazwie `netops-shared-rg`.
    ![Tworzenie grupy zasobów](../../_images/govern/design/governance-3-0d.png)
2. **Właściciel subskrypcji** dodaje do grupy zasobów konto **użytkownika operacji sieci** i przypisuje rolę **współautor** .
    ![Dodawanie użytkownika operacji sieciowych](../../_images/govern/design/governance-3-0e.png)
3. **Użytkownik operacji sieciowych** tworzy bramę [sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) i konfiguruje ją do łączenia się z lokalnym urządzeniem sieci VPN. Użytkownik **operacji sieciowych** stosuje także parę [tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) do poszczególnych zasobów: *Environment: Shared* i *zarządzane: netOps*. Gdy **administrator usługi subskrypcji** Eksportuje raport kosztów, koszty będą wyrównane do każdego z tych tagów. Pozwala to **administratorowi usługi subskrypcji** na przestawianie kosztów przy użyciu tagu *Environment* i znacznika *zarządzane* . Zwróć uwagę na licznik **limity zasobów** w prawym górnym rogu rysunku. Każda subskrypcja platformy Azure ma [limity usług](https://docs.microsoft.com/azure/azure-subscription-service-limits)i aby pomóc zrozumieć efekt tych limitów, należy postępować zgodnie z limitem sieci wirtualnej dla każdej subskrypcji. Istnieje limit 1000 sieci wirtualnych na subskrypcję, a po wdrożeniu pierwszej sieci wirtualnej dostępne są teraz 999.
    ![Tworzenie bramy sieci VPN](../../_images/govern/design/governance-3-1.png)
4. Wdrożono dwie więcej grup zasobów. Pierwszy ma nazwę `prod-rg`. Ta grupa zasobów jest wyrównana ze środowiskiem produkcyjnym. Drugi ma nazwę `dev-rg` i jest wyrównany do środowiska deweloperskiego. Wszystkie zasoby skojarzone z obciążeniami produkcyjnymi są wdrażane w środowisku produkcyjnym, a wszystkie zasoby związane z obciążeniami programistycznymi są wdrażane w środowisku deweloperskim. W tym przykładzie wdrażane są tylko dwa obciążenia do każdego z tych dwóch środowisk, więc nie będą napotykane żadne limity usługi subskrypcji platformy Azure. Należy jednak wziąć pod uwagę, że każda grupa zasobów ma limit 800 zasobów dla każdej grupy zasobów. W przypadku kontynuowania dodawania obciążeń do poszczególnych grup zasobów ostatecznie ten limit zostanie osiągnięty.
    ![Tworzenie grup zasobów](../../_images/govern/design/governance-3-2.png)
5. Pierwszy **właściciel obciążenia** wysyła żądanie do **administratora usługi subskrypcji** i jest dodawany do każdej grupy zasobów środowiska projektowego i produkcyjnego z rolą **współautor** . Jak pokazano wcześniej, rola **współautor** zezwala użytkownikowi na wykonywanie dowolnej operacji poza przypisaniem roli innemu użytkownikowi. Pierwszy **właściciel obciążenia** może teraz tworzyć zasoby skojarzone z ich obciążeniem.
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-3.png)
6. Pierwszy **właściciel obciążenia** tworzy sieć wirtualną w każdej z dwóch grup zasobów z parą maszyn wirtualnych w każdym z nich. Pierwszy **właściciel obciążenia** stosuje Tagi *Environment* i *zarządzane* do wszystkich zasobów. Należy pamiętać, że licznik limit usług platformy Azure jest teraz równy 997 sieci wirtualnych.
    ![Tworzenie sieci wirtualnych](../../_images/govern/design/governance-3-4.png)
7. Każda sieć wirtualna nie ma łączności z lokalnymi, gdy są tworzone. W tym typie architektury Każda sieć wirtualna musi być połączona z węzłem do sieci wirtualnej w środowisku **infrastruktury udostępnionej** . Komunikacja równorzędna sieci wirtualnych tworzy połączenie między dwiema oddzielnymi sieciami wirtualnymi i zezwala na ruch sieciowy między nimi. Należy pamiętać, że Komunikacja równorzędna sieci wirtualnych nie jest z założenia przechodnie. Komunikacja równorzędna musi być określona w każdej z dwóch połączonych sieci wirtualnych, a w przypadku, gdy tylko jedna z sieci wirtualnych określa komunikację równorzędną, połączenie jest niekompletne. Aby zilustrować efekt tego, pierwszy **właściciel obciążenia** określa komunikację równorzędną między siecią firmową i siecią **wirtualną**. Zostanie utworzona pierwsza Komunikacja równorzędna, ale nie ma żadnych przepływów ruchu, ponieważ uzupełniająca Komunikacja równorzędna z **koncentratora-Sieć wirtualna** do **produkcyjnego** nie została jeszcze określona. Pierwszy **właściciel obciążenia** kontaktuje się z użytkownikiem **operacji sieciowych** i żąda tego uzupełniającego połączenia komunikacji równorzędnej.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-5.png)
8. Użytkownik **operacji w sieci** przegląda żądanie, zatwierdza je, a następnie określa komunikację równorzędną w ustawieniach dla **koncentratora-Sieć wirtualna**. Połączenie komunikacji równorzędnej jest teraz kompletne i ruch sieciowy między dwiema sieciami wirtualnymi.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-6.png)
9. Teraz drugi **właściciel obciążenia** wysyła żądanie do **administratora usługi subskrypcji** i jest dodawany do istniejących grup zasobów środowiska produkcyjnego i **programistycznego** z rolą **współautor** . Drugi **właściciel obciążenia** ma takie same uprawnienia dla wszystkich zasobów jak pierwszy **właściciel obciążenia** w każdej grupie zasobów.
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-7.png)
10. Drugi **właściciel obciążenia** tworzy podsieć w sieci wirtualnej **produkcyjnej** , a następnie dodaje dwie maszyny wirtualne. Drugi **właściciel obciążenia** stosuje Tagi *Environment* i *zarządzane* do każdego zasobu.
    ![Tworzenie podsieci](../../_images/govern/design/governance-3-8.png)

Ten przykładowy model zarządzania zasobami umożliwia nam zarządzanie zasobami w trzech wymaganych środowiskach. Zasoby infrastruktury udostępnionej są chronione, ponieważ w subskrypcji istnieje tylko jeden użytkownik z uprawnieniami do uzyskiwania dostępu do tych zasobów. Każdy właściciel obciążenia może korzystać z udostępnionych zasobów infrastruktury bez posiadania żadnych uprawnień do rzeczywistych zasobów udostępnionych. Jednak ten model zarządzania kończy się niepowodzeniem w przypadku izolacji obciążeń — każdy z dwóch **właścicieli obciążeń** może uzyskać dostęp do zasobów innego obciążenia.

Istnieje inny istotny problem z tym modelem, który może nie być od razu oczywisty. W tym przykładzie został app1y **właściciel obciążenia** , który zażądał połączenia komunikacji równorzędnej sieci z **koncentratorem-Sieć wirtualna** , aby zapewnić łączność z lokalnymi. Użytkownik **operacji sieciowych** ocenił to żądanie na podstawie zasobów wdrożonych w ramach tego obciążenia. Gdy **właściciel subskrypcji** dodał **właściciela obciążenia APP2** z rolą **współautor** , ten użytkownik miał prawa dostępu do zarządzania wszystkimi zasobami w grupie zasobów **prod-RG** .

![Diagram przedstawiający prawa dostępu do zarządzania](../../_images/govern/design/governance-3-10.png)

Oznacza to, że **właściciel obciążenia APP2** miał uprawnienia do wdrożenia własnej podsieci z maszynami wirtualnymi w sieci wirtualnej **produkcyjnej** . Domyślnie te maszyny wirtualne mają teraz dostęp do sieci lokalnej. Użytkownik **operacji sieciowych** nie wie o tych maszynach i nie zatwierdził ich łączności w środowisku lokalnym.

Następnie Przyjrzyjmy się pojedynczej subskrypcji z wieloma grupami zasobów dla różnych środowisk i obciążeń. Należy zauważyć, że w poprzednim przykładzie zasoby dla każdego środowiska były łatwe do zidentyfikowania, ponieważ znajdowały się w tej samej grupie zasobów. Teraz, gdy takie grupowanie nie jest już konieczne, należy polegać na konwencji nazewnictwa grup zasobów w celu zapewnienia tej funkcjonalności.

1. Zasoby **infrastruktury udostępnionej** nadal będą mieć oddzielną grupę zasobów w tym modelu, dzięki czemu pozostają takie same. Każde obciążenie wymaga dwóch grup zasobów — jeden dla każdego środowiska **projektowego** i **produkcyjnego** . W przypadku pierwszego obciążenia **właściciel subskrypcji** tworzy dwie grupy zasobów. Pierwszy z nich nosi nazwę **APP1-prod-RG** , a druga **— Nazwa APP1-dev-RG**. Jak wspomniano wcześniej, ta konwencja nazewnictwa identyfikuje zasoby jako skojarzone z pierwszym obciążeniem, **APP1**i środowiskiem **deweloperskim** lub **produkcyjnym** . Ponownie właściciel *subskrypcji* dodaje **właściciela obciążenia APP1** do grupy zasobów z rolą **współautor** .
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-12.png)
2. Podobnie jak w przypadku pierwszego przykładu **właściciel obciążenia APP1** wdraża sieć wirtualną o nazwie **APP1-prod-VNET** w środowisku **produkcyjnym** oraz inną nazwę **APP1-dev-VNET** w środowisku **deweloperskim** . Następnie **właściciel obciążenia APP1** wysyła żądanie do użytkownika **operacji sieciowych** w celu utworzenia połączenia komunikacji równorzędnej. Należy zauważyć, że **właściciel obciążenia APP1** dodaje te same Tagi co w pierwszym przykładzie, a licznik limit został zmniejszony do 997 sieci wirtualnych pozostałych w ramach subskrypcji.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-13.png)
3. **Właściciel subskrypcji** tworzy teraz dwie grupy zasobów dla **właściciela obciążenia APP2**. Zgodnie z tymi samymi konwencjami co w przypadku **właściciela obciążenia APP1**grupy zasobów mają nazwę **APP2-prod-RG** i **APP2-dev-RG**. **Właściciel subskrypcji** dodaje **właściciela obciążenia APP2** do każdej grupy zasobów z rolą **współautor** .
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-14.png)
4. *Właściciel obciążenia APP2* wdraża sieci wirtualne i maszyny wirtualne w grupach zasobów z tymi samymi konwencjami nazewnictwa. Dodawane są Tagi, a licznik limit został zmniejszony do 995 sieci wirtualnych pozostałych w ramach *subskrypcji*.
    ![Wdrażanie sieci wirtualnych i maszyn wirtualnych](../../_images/govern/design/governance-3-15.png)
5. *Właściciel obciążenia APP2* wysyła żądanie do użytkownika *operacji sieci* do elementu równorzędnego *APP2-prod-VNET* z koncentratorem. Użytkownik *operacji sieciowych* tworzy połączenie komunikacji równorzędnej.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-16.png)

Otrzymany model zarządzania jest podobny do pierwszego przykładu z kilkoma kluczowymi różnicami:

- Każdy z tych dwóch obciążeń jest izolowany przez obciążenie i środowisko.
- Ten model wymaga dwóch więcej sieci wirtualnych niż pierwszy przykładowy model. Chociaż nie jest to ważna różnica w przypadku tylko dwóch obciążeń, teoretyczny limit liczby obciążeń dla tego modelu wynosi 24.
- Zasoby nie są już pogrupowane w jednej grupie zasobów dla każdego środowiska. Grupowanie zasobów wymaga poznania konwencji nazewnictwa używanych dla każdego środowiska.
- Każda z połączeń równorzędnych sieci wirtualnych została sprawdzona i zatwierdzona przez użytkownika *operacji sieciowych* .

Teraz przyjrzyjmy się modelowi zarządzania zasobami przy użyciu wielu subskrypcji. W tym modelu porównujesz każde z trzech środowisk z oddzielną subskrypcją: subskrypcję **usług udostępnionych** , subskrypcję produkcyjną i na koniec subskrypcji **deweloperskiej** . Zagadnienia dotyczące tego modelu są podobne do modelu przy użyciu jednej subskrypcji w programie, aby określić sposób wyrównania grup zasobów do obciążeń. Określono już, że tworzenie grupy zasobów dla każdego obciążenia spełnia wymagania dotyczące izolacji obciążenia, więc w tym przykładzie nastąpi przeniesieniu do tego modelu.

1. W tym modelu istnieją trzy *subskrypcje*: *udostępniona infrastruktura*, *produkcja*i *programowanie*. Każda z tych trzech subskrypcji wymaga *właściciela subskrypcji*, a w prostym przykładzie użyjesz tego samego konta użytkownika dla wszystkich trzech. Zasoby *infrastruktury udostępnionej* są zarządzane podobnie jak dwa pierwsze przykłady, a pierwsze obciążenie jest skojarzone z *APP1 RG* w środowisku produkcyjnym i grupą zasobów o tej samej nazwie podczas *opracowywania* środowisko. *Właściciel obciążenia APP1* jest dodawany do każdej grupy zasobów z rolą *współautor* .
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-17.png)
2. Podobnie jak w przypadku wcześniejszych przykładów, *właściciel obciążenia APP1* tworzy zasoby i żąda połączenia komunikacji równorzędnej z siecią wirtualną *infrastruktury udostępnionej* . *Właściciel obciążenia APP1* dodaje tylko tag *zarządzane* , ponieważ nie jest już potrzebny tag *Environment* . Oznacza to, że zasoby dla każdego środowiska są teraz pogrupowane w tej samej *subskrypcji* , a znacznik *środowiska* jest nadmiarowy. Licznik limit jest zmniejszany do 999 sieci wirtualnych.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-18.png)
3. Na koniec *właściciel subskrypcji* powtarza proces dla drugiego obciążenia, dodając grupy zasobów za pomocą *właściciela obciążenia APP2* w roli * współautor. Wartość licznika limit dla każdej subskrypcji środowiska jest zmniejszana do 998 sieci wirtualnych.

Ten model zarządzania ma zalety w drugim przykładzie powyżej. Jednak kluczową różnicą jest to, że limity są mniejsze od problemu ze względu na fakt, że są rozłożone na dwie *subskrypcje*. Wadą jest to, że dane o kosztach śledzone przez Tagi muszą być agregowanewe wszystkich trzech subskrypcjach.

W związku z tym można wybrać jeden z tych dwóch przykładów modeli zarządzania zasobami w zależności od priorytetu wymagań. Jeśli przewidujesz, że Twoja organizacja nie osiągnie limitów usługi dla jednej subskrypcji, możesz użyć pojedynczej subskrypcji z wieloma grupami zasobów. Z drugiej strony, jeśli organizacja przewiduje wiele obciążeń, może być lepszym rozwiązaniem wielu subskrypcji dla każdego środowiska.

## <a name="implementing-the-resource-management-model"></a>Implementowanie modelu zarządzania zasobami

Zapoznaj się z kilkoma różnymi modelami, które ułatwiają dostęp do zasobów platformy Azure. Teraz wykonaj kroki niezbędne do zaimplementowania modelu zarządzania zasobami z jedną subskrypcją dla każdej z **udostępnionych środowisk infrastruktury**, **produkcji**i **programowania** , korzystając z przewodnika projektowania. Dla wszystkich trzech środowisk będziesz mieć jednego **właściciela subskrypcji** . Każde obciążenie zostanie odizolowane w **grupie zasobów** z dodaniem **właściciela obciążenia** z rolą **współautor** .

> [!NOTE]
> Przeczytaj [Opis dostępu do zasobów na platformie Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles) , aby dowiedzieć się więcej na temat relacji między kontami i subskrypcjami platformy Azure.

Wykonaj następujące kroki:

1. Utwórz [konto platformy Azure](https://docs.microsoft.com/azure/active-directory/sign-up-organization) , jeśli organizacja jeszcze go nie ma. Osoba, która zarejestruje się na konto platformy Azure, zostaje administratorem konta platformy Azure, a lider organizacji musi wybrać osobę, która ma założyć tę rolę. Osoba ta będzie odpowiedzialna za:
    - Tworzenie subskrypcji.
    - Tworzenie i administrowanie dzierżawami [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) , które przechowują tożsamość użytkownika dla tych subskrypcji.
2. Zespół liderów w organizacji decyduje, które osoby są odpowiedzialne za:
    - Zarządzanie tożsamościami użytkowników; [dzierżawa usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) jest tworzona domyślnie podczas tworzenia konta platformy Azure w organizacji, a administrator konta jest domyślnie dodawany jako [administrator globalny usługi Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) . Organizacja może wybrać innego użytkownika do zarządzania tożsamościami użytkowników, [przypisując do tego użytkownika rolę administratora globalnego usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-users-assign-role-azure-portal).
    - Subskrypcje, co oznacza, że Ci użytkownicy:
        - Zarządzaj kosztami związanymi z użyciem zasobów w tej subskrypcji.
        - Zaimplementuj i Zachowaj najmniejszy model uprawnień na potrzeby dostępu do zasobów.
        - Śledź limity usług.
    - Udostępnione usługi infrastruktury (Jeśli organizacja zdecyduje się korzystać z tego modelu), co oznacza, że ten użytkownik jest odpowiedzialny za:
        - Łączność lokalna z siecią platformy Azure.
        - Własność łączności sieciowej na platformie Azure za pośrednictwem komunikacji równorzędnej sieci wirtualnej.
    - Właściciele obciążeń.
3. Administrator globalny usługi Azure AD [tworzy nowe konta użytkowników](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) dla:
    - Osoba, która będzie **właścicielem subskrypcji** dla każdej subskrypcji skojarzonej z każdym środowiskiem. Należy pamiętać, że jest to konieczne tylko wtedy, gdy **administrator usługi** subskrypcji nie będzie miał zadań związanych z zarządzaniem dostępem do zasobów dla każdej subskrypcji/środowiska.
    - Osoba, która będzie **użytkownikiem operacji sieciowych**.
    - Osoby, które są **właścicielami obciążeń**.
4. Administrator konta platformy Azure tworzy następujące trzy subskrypcje przy użyciu [portalu konta platformy Azure](https://account.azure.com):
    - Subskrypcja środowiska **infrastruktury udostępnionej** .
    - Subskrypcja środowiska produkcyjnego .
    - Subskrypcja środowiska deweloperskiego .
5. Administrator konta platformy Azure [dodaje właściciela usługi subskrypcji do każdej subskrypcji](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#assign-a-user-as-an-administrator-of-a-subscription).
6. Utwórz proces zatwierdzania dla **właścicieli obciążeń** , aby zażądać tworzenia grup zasobów. Proces zatwierdzania można zaimplementować na wiele sposobów, na przykład za pośrednictwem poczty e-mail, lub za pomocą narzędzia do zarządzania procesem, takiego jak [przepływy pracy programu SharePoint](https://support.office.com/article/introduction-to-sharepoint-workflow-07982276-54e8-4e17-8699-5056eff4d9e3). Proces zatwierdzania może wykonać następujące czynności:
    - **Właściciel obciążenia** przygotowuje zestawienie materiałów dla wymaganych zasobów platformy Azure w środowisku **programistycznym** , środowisku **produkcyjnym** lub w obu systemach i przesyła je do **właściciela subskrypcji**.
    - **Właściciel subskrypcji** przegląda zestawienie materiałów i sprawdza poprawność żądanych zasobów, aby upewnić się, że żądane zasoby są odpowiednie do ich planowanego użycia — na przykład, sprawdzając, czy żądane [rozmiary maszyn wirtualnych](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) są niepoprawne.
    - Jeśli żądanie nie zostanie zatwierdzone, **właściciel obciążenia** zostanie powiadomiony. Jeśli żądanie zostanie zatwierdzone, **właściciel subskrypcji** [tworzy żądaną grupę zasobów](https://docs.microsoft.com/azure/azure-resource-manager/manage-resource-groups-portal#create-resource-groups) zgodnie z konwencjami nazewnictwa [](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)organizacji, [dodaje **właściciela obciążenia** ](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment) z [rolą **współautor** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) i wysyła powiadomienie do **właściciela obciążenia** , który utworzył grupę zasobów.
7. Utwórz proces zatwierdzania dla właścicieli obciążeń, aby zażądać połączenia komunikacji równorzędnej sieci wirtualnej od właściciela udostępnionej infrastruktury. Tak jak w poprzednim kroku, ten proces zatwierdzania można zaimplementować za pomocą poczty e-mail lub narzędzia do zarządzania procesami.

Po wdrożeniu modelu ładu można wdrożyć udostępnione usługi infrastruktury.

## <a name="related-resources"></a>Powiązane zasoby

[Wbudowane role dla zasobów platformy Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się więcej o wdrażaniu infrastruktury podstawowej](../../infrastructure/virtual-machines/basic-workload.md)
