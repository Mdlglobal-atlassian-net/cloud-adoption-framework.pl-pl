---
title: Projektowanie wielu zespołów na platformie Azure
description: Znajdź wskazówki dotyczące konfigurowania kontrolek ładu platformy Azure dla wielu zespołów, wielu obciążeń i wielu środowisk.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 84c1c1d8d6d483955e0b3928de7566f9ded4ffcb
ms.sourcegitcommit: 9a84c2dfa4c3859fd7d5b1e06bbb8549ff6967fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83756162"
---
<!-- cSpell:ignore netops -->

# <a name="governance-design-for-multiple-teams"></a>Projekt nadzoru dla wielu zespołów

Celem tych wskazówek jest ułatwienie poznania procesu projektowania modelu zarządzania zasobami na platformie Azure w celu obsługi wielu zespołów, wielu obciążeń i wielu środowisk. Najpierw zapoznaj się z zestawem hipotetycznych wymagań ładu, a następnie przejdź do kilku przykładowych implementacji, które spełniają te wymagania.

Wymagania są następujące:

- Firma planuje przenieść nowe role w chmurze i obowiązki do zestawu użytkowników, a tym samym wymaga zarządzania tożsamościami dla wielu zespołów z różnymi potrzebami dostępu do zasobów na platformie Azure. Ten system zarządzania tożsamościami jest wymagany do przechowywania tożsamości następujących użytkowników:
  - Osoby w organizacji odpowiedzialne za własność **subskrypcji**.
  - Osoby w organizacji odpowiedzialne za **udostępnione zasoby infrastruktury** używane do łączenia sieci lokalnej z siecią wirtualną na platformie Azure.
  - Dwie osoby w organizacji odpowiedzialne za zarządzanie **obciążeniem**.
- Obsługa wielu **środowisk**. Środowisko to logiczne grupowanie zasobów, takich jak maszyny wirtualne, sieci wirtualne i usługi routingu ruchu sieciowego. Te grupy zasobów mają podobne wymagania dotyczące zarządzania i zabezpieczeń i są zwykle używane do określonego celu, takiego jak testowanie lub produkcja. W tym przykładzie wymagania dotyczą czterech środowisk:
  - **Udostępnione środowisko infrastruktury** , które obejmuje zasoby współużytkowane przez obciążenia w innych środowiskach. Na przykład Sieć wirtualna z podsiecią bramy, która zapewnia łączność z lokalnymi.
  - **Środowisko produkcyjne** z najbardziej restrykcyjnymi zasadami zabezpieczeń. Może obejmować obciążenia wewnętrzne lub zewnętrzne.
  - **Środowisko nieprodukcyjne** na potrzeby projektowania i testowania. To środowisko ma zabezpieczenia, zgodność i zasady dotyczące kosztów, które różnią się od tych w środowisku produkcyjnym. Na platformie Azure ma to formę subskrypcji Enterprise — tworzenie i testowanie.
  - **Środowisko piaskownicy** do weryfikacji koncepcji i celów edukacyjnych. To środowisko jest zwykle przypisywany dla pracowników uczestniczących w działaniach programistycznych i ma ścisłe procedury i funkcjonalne mechanizmy kontroli bezpieczeństwa, aby zapobiec wyładunku danych firmowych w tym miejscu. Na platformie Azure mają one formę subskrypcji programu Visual Studio. Te subskrypcje _nie_ powinny również być powiązane z Azure Active Directoryami przedsiębiorstwa.
- **Model uprawnień o najniższych** uprawnieniach, w którym użytkownicy domyślnie nie mają uprawnień. Model musi obsługiwać następujące elementy:
  - Pojedynczy zaufany użytkownik objęty zakresem subskrypcji, traktowany jak konto usługi i przyznane uprawnienia do przypisywania praw dostępu do zasobów.
  - Każdy właściciel obciążenia domyślnie odmówił dostępu do zasobów. Prawa dostępu do zasobów są udzielane jawnie przez jednego zaufanego użytkownika w zakresie grupy zasobów.
  - Dostęp do zarządzania zasobami infrastruktury udostępnionej, ograniczone do właścicieli infrastruktury udostępnionej.
  - Dostęp do zarządzania dla każdego obciążenia ograniczonego do właściciela obciążenia w środowisku produkcyjnym, a zwiększenie poziomu kontroli jest realizowane przez różne środowiska wdrażania (projektowanie, testowanie, przygotowywanie i produkcja).
  - Przedsiębiorstwo nie chce, aby zarządzać rolami niezależnie w każdym z trzech głównych środowisk i w związku z tym wymagało użycia tylko [wbudowanych ról](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) dostępnych w kontroli dostępu opartej na ROLACH (RBAC) na platformie Azure. Jeśli w przedsiębiorstwie absolutnie wymagane są niestandardowe role RBAC, do synchronizowania ról niestandardowych w trzech środowiskach wymagane są dodatkowe procesy.
- Śledzenie kosztów według nazwy właściciela obciążenia, środowiska lub obu tych funkcji.

## <a name="identity-management"></a>Zarządzanie tożsamościami

Aby można było zaprojektować Zarządzanie tożsamościami dla modelu ładu, ważne jest, aby zrozumieć cztery główne obszary, które obejmują:

- **Administracja:** Procesy i narzędzia służące do tworzenia, edytowania i usuwania tożsamości użytkowników.
- **Uwierzytelnianie:** Weryfikowanie tożsamości użytkownika przez sprawdzenie poprawności poświadczeń, takich jak nazwa użytkownika i hasło.
- **Autoryzacja:** Określanie zasobów, do których uwierzytelniony użytkownik może uzyskać dostęp lub jakie operacje mają uprawnienia do wykonywania.
- **Inspekcja:** Okresowe przeglądanie dzienników i innych informacji w celu odnalezienia problemów z zabezpieczeniami związanych z tożsamością użytkownika. Obejmuje to przeglądanie podejrzanych wzorców użycia, okresowe przeglądanie uprawnień użytkowników w celu sprawdzenia, czy są one dokładne, oraz innych funkcji.

Istnieje tylko jedna usługa zaufana przez platformę Azure dla tożsamości, która jest Azure Active Directory (Azure AD). Będziesz dodawać użytkowników do usługi Azure AD i korzystać z niej we wszystkich wymienionych powyżej funkcjach. Przed rozpoczęciem konfigurowania usługi Azure AD ważne jest, aby zrozumieć konta uprzywilejowane, które są używane do zarządzania dostępem do tych usług.

Gdy Twoja organizacja zarejestrowano na potrzeby konta platformy Azure, przypisano co najmniej jednego **właściciela konta** platformy Azure. Ponadto zostanie utworzona **dzierżawa** usługi Azure AD, chyba że istniejąca dzierżawa jest już skojarzona z innymi usługami firmy Microsoft, takimi jak Office 365. Podczas tworzenia skojarzono **administratora globalnego** z pełnymi uprawnieniami w dzierżawie usługi Azure AD.

Tożsamości użytkowników zarówno dla właściciela konta platformy Azure, jak i administratora globalnego usługi Azure AD są przechowywane w wysoce zabezpieczonym systemie tożsamości, który jest zarządzany przez firmę Microsoft. Właściciel konta platformy Azure jest autoryzowany do tworzenia, aktualizowania i usuwania subskrypcji. Administrator globalny usługi Azure AD jest autoryzowany do wykonywania wielu działań w usłudze Azure AD, ale w przypadku tego przewodnika projektowego należy skoncentrować się na tworzeniu i usuwaniu tożsamości użytkownika.

> [!NOTE]
> Twoja organizacja może już mieć istniejącą dzierżawę usługi Azure AD, jeśli istnieje skojarzona z kontem licencję Office 365, Intune lub Dynamics 365.

Właściciel konta platformy Azure ma uprawnienia do tworzenia, aktualizowania i usuwania subskrypcji:

![Konto platformy Azure z właścicielem konta platformy Azure i administratorem globalnym usługi Azure AD ](../../_images/govern/design/governance-3-0.png)
 _rysunek 1: konto platformy Azure z właścicielem konta platformy Azure i administratorem globalnym usługi Azure AD._

**Administrator globalny** usługi Azure AD ma uprawnienia do tworzenia kont użytkowników:

![Konto platformy Azure z właścicielem konta platformy Azure i administratorem globalnym usługi Azure AD ](../../_images/govern/design/governance-3-0a.png)
 _rysunek 2: Administrator globalny usługi Azure AD tworzy wymagane konta użytkowników w dzierżawie._

Pierwsze dwa konta, **właściciel obciążenia APP1** i **właściciel obciążenia APP2**, są skojarzone z osobą w organizacji odpowiedzialną za zarządzanie obciążeniem. Konto **operacji sieci** należy do osoby odpowiedzialnej za udostępnione zasoby infrastruktury. Na koniec konto **właściciela subskrypcji** jest powiązane z osobą odpowiedzialną za własność subskrypcji.

## <a name="resource-access-permissions-model-of-least-privilege"></a>Uprawnienia dostępu do zasobów — model najniższych uprawnień

Po utworzeniu systemu zarządzania tożsamościami i kontami użytkowników należy zdecydować, jak zastosować role kontroli dostępu opartej na rolach (RBAC) do poszczególnych kont w celu obsługi modelu uprawnień o najniższych uprawnieniach.

Istnieje również inne wymaganie, aby wszystkie zasoby skojarzone z poszczególnymi obciążeniami były od siebie odizolowane, dzięki czemu żaden właściciel obciążenia ma dostęp do innych obciążeń, które nie są właścicielami. Istnieje również wymóg implementacji tego modelu przy użyciu tylko wbudowanych ról dla kontroli dostępu opartej na rolach platformy Azure.

Każda rola RBAC jest stosowana w jednym z trzech zakresów na platformie Azure: **subskrypcja**, **Grupa zasobów**, a następnie pojedynczy **zasób**. Role są dziedziczone w niższych zakresach. Jeśli na przykład użytkownik ma przypisaną [rolę właściciela wbudowane](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) na poziomie subskrypcji, ta rola jest również przypisywana do tego użytkownika w grupie zasobów i na poziomie poszczególnych zasobów, chyba że zostanie zastąpiona.

W związku z tym, aby utworzyć model dostępu o najniższych uprawnieniach, należy podjąć decyzję o działaniach, które określony typ użytkownika może wykonać w każdym z tych trzech zakresów. Na przykład wymaganie właściciela obciążenia ma uprawnienia do zarządzania dostępem tylko do zasobów skojarzonych z ich obciążeniem i bez innych. Jeśli przypiszesz wbudowaną rolę właściciela w zakresie subskrypcji, każdy właściciel obciążenia będzie miał dostęp do wszystkich obciążeń.

Przyjrzyjmy się dwóm przykładowym modelom uprawnień do lepszego zrozumienia tego pojęcia. W pierwszym przykładzie model ufa tylko administratorowi usługi do tworzenia grup zasobów. W drugim przykładzie model przypisuje wbudowaną rolę właściciela do każdego właściciela obciążenia w zakresie subskrypcji.

W obu przykładach istnieje administrator usługi subskrypcji, który ma przypisaną rolę właściciela wbudowanego w zakresie subskrypcji. Odwołaj, że wbudowana rola właściciela przyznaje wszystkie uprawnienia, w tym zarządzanie dostępem do zasobów.

![Administrator usługi subskrypcji z rolą właściciela ](../../_images/govern/design/governance-2-1.png)
 _rysunek 3: subskrypcja z administratorem usługi, która ma przypisaną rolę właściciela wbudowanego._

<!-- docsTest:ignore "resource group A" "resource groups A and B" "workload owner A" -->

1. W pierwszym przykładzie istnieje **właściciel obciążenia A** bez uprawnień do zakresu subskrypcji, &mdash; domyślnie nie ma uprawnień do zarządzania dostępem do zasobów. Ten użytkownik chce wdrożyć zasoby i zarządzać nimi w ramach obciążenia. Należy skontaktować się z **administratorem usługi** , aby zażądać utworzenia grupy zasobów.
    ![Właściciel obciążenia żąda utworzenia grupy zasobów A](../../_images/govern/design/governance-2-2.png)
2. **Administrator usługi** przegląda swoje żądanie i tworzy **grupę zasobów a**. W tym momencie **właściciel obciążenia** nadal nie ma uprawnień do wykonywania żadnych czynności.
    ![Administrator usługi tworzy grupę zasobów A](../../_images/govern/design/governance-2-3.png)
3. **Administrator usługi** dodaje **właściciela obciążenia a** do **grupy zasobów** a i przypisuje [wbudowaną rolę współautor](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Rola współautor przyznaje wszystkie uprawnienia do **grupy zasobów A,** z wyjątkiem zarządzania uprawnieniami dostępu.
    ![Administrator usługi dodaje właściciela obciążenia A do grupy zasobów A](../../_images/govern/design/governance-2-4.png)
4. Załóżmy, że **właściciel obciążenia a** ma wymóg dla pary członków zespołu do wyświetlania danych monitorowania procesora i ruchu sieciowego w ramach planowania pojemności dla obciążenia. Ponieważ **właściciel obciążenia A** ma przypisaną rolę współautor, nie ma uprawnień do dodawania użytkownika do **grupy zasobów A**. Muszą wysłać to żądanie do **administratora usługi**.
    ![Właściciele obciążenia żądają współautorów obciążeń do grupy zasobów](../../_images/govern/design/governance-2-5.png)
5. **Administrator usługi** przegląda żądanie i dodaje dwóch użytkowników **współautorów obciążenia** do **grupy zasobów a**. Żaden z tych dwóch użytkowników nie wymaga uprawnień do zarządzania zasobami, więc ma przypisaną [wbudowaną rolę czytnika](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor).
    ![Administrator usługi dodaje współautorów obciążeń do grupy zasobów A](../../_images/govern/design/governance-2-6.png)
6. Następnie **właściciel obciążenia B** wymaga również grupy zasobów, aby zawierała zasoby związane z obciążeniem. Podobnie jak w przypadku **właściciela obciążenia A**, **właściciel obciążenia B** początkowo nie ma uprawnień do wykonania akcji w zakresie subskrypcji, dlatego musi wysłać żądanie do **administratora usługi**.
    ![Właściciel obciążenia B żąda utworzenia grupy zasobów B](../../_images/govern/design/governance-2-7.png)
7. **Administrator usługi** przegląda żądanie i tworzy **grupę zasobów B**.  ![Administrator usługi tworzy grupę zasobów B](../../_images/govern/design/governance-2-8.png)
8. **Administrator usługi** dodaje następnie **właściciela obciążenia b** do **grupy zasobów b** i przypisuje wbudowaną rolę współautor.
    ![Administrator usługi dodaje właściciela obciążenia B do grupy zasobów B](../../_images/govern/design/governance-2-9.png)

W tym momencie każdy właściciel obciążenia jest izolowany w ich własnej grupie zasobów. Żaden z właścicieli obciążeń lub ich członkowie zespołu nie mają dostępu do zasobów w żadnej innej grupie zasobów.

![Subskrypcja z grupami zasobów A i B ](../../_images/govern/design/governance-2-10.png)
 _rysunek 4: subskrypcja z dwoma właścicielami obciążeń izolowanych z ich własną grupą zasobów._

Ten model jest modelem najniższych uprawnień, do którego &mdash; każdy użytkownik ma przypisane odpowiednie uprawnienia w prawidłowym zakresie zarządzania zasobami.

Należy wziąć pod uwagę, że każde zadanie w tym przykładzie zostało wykonane przez **administratora usługi**. Chociaż jest to prosty przykład i może nie być przyczyną problemu, ponieważ wystąpiły tylko dwa właściciele obciążeń, można łatwo wyobrazić typy problemów, które byłyby wynikiem dużej organizacji. Na przykład **administrator usługi** może stać się wąskim gardłem z dużą zaległością żądań, które powodują opóźnienia.

Przyjrzyjmy się drugiemu przykładowi, który zmniejsza liczbę zadań wykonywanych przez **administratora usługi**.

1. W tym modelu **właściciel obciążenia A** ma przypisaną wbudowaną rolę właściciela w zakresie subskrypcji, umożliwiając im utworzenie własnej grupy zasobów: **Grupa zasobów A**.  ![Administrator usługi dodaje właściciela obciążenia A do subskrypcji](../../_images/govern/design/governance-2-11.png)
2. Gdy **Grupa zasobów A** zostanie utworzona, **właściciel obciążenia a** jest domyślnie dodawany i dziedziczy wbudowaną rolę właściciela z zakresu subskrypcji.
    ![Właściciel obciążenia A tworzy grupę zasobów A](../../_images/govern/design/governance-2-12.png)
3. Wbudowana rola właściciela umożliwia **właścicielowi obciążenia** uprawnienie do zarządzania dostępem do grupy zasobów. **Właściciel obciążenia a** dodaje dwóch **współautorów obciążenia** i przypisuje wbudowaną rolę czytnika do każdego z nich.
    ![Właściciel obciążenia A dodaje współautorów obciążenia](../../_images/govern/design/governance-2-13.png)
4. **Administrator usługi** dodaje teraz **właściciela obciążenia B** do subskrypcji z wbudowaną rolą właściciela.
    ![Administrator usługi dodaje właściciela obciążenia B do subskrypcji](../../_images/govern/design/governance-2-14.png)
5. **Właściciel obciążenia b** tworzy **grupę zasobów b** i jest domyślnie dodawany. Następnie **właściciel obciążenia B** dziedziczy wbudowaną rolę właściciela z zakresu subskrypcji.
    ![Właściciel obciążenia B tworzy grupę zasobów B](../../_images/govern/design/governance-2-15.png)

Należy pamiętać, że w tym modelu **administrator usługi** wykonał mniejszą liczbę akcji niż w pierwszym przykładzie z powodu delegowania dostępu do zarządzania do każdego z poszczególnych właścicieli obciążeń.

![Subskrypcja z grupami zasobów A i B ](../../_images/govern/design/governance-2-16.png)
 _rysunek 5: subskrypcja z uprawnieniami administratora usługi i dwóch właścicieli obciążeń — wszystkie przypisane role właściciela wbudowanego._

Ponieważ **właściciel obciążenia a** i **właściciel obciążenia B** mają przypisaną rolę właściciela wbudowane w zakresie subskrypcji, każdy z nich dziedziczy rolę właściciela wbudowane dla każdej grupy zasobów. Oznacza to, że użytkownicy mają pełny dostęp do wszystkich zasobów, ale mogą również delegować dostęp do zarządzania do grup zasobów każdej z nich. Na przykład **właściciel obciążenia B** ma uprawnienia do dodawania dowolnego innego użytkownika do **grupy zasobów a** i może przypisywać do nich dowolną rolę, w tym wbudowaną rolę właściciela.

W przypadku porównania każdego przykładu z wymaganiami zobaczysz, że oba przykłady obsługują jednego zaufanego użytkownika w zakresie subskrypcji z uprawnieniem do przyznawania praw dostępu do zasobów dla dwóch właścicieli obciążeń. Każdy z dwóch właścicieli obciążeń nie miał domyślnie dostępu do zarządzania zasobami i wymaga, aby **administrator usługi** jawnie przypisał do nich uprawnienia. Tylko pierwszy przykład obsługuje wymaganie, aby zasoby skojarzone z poszczególnymi obciążeniami były od siebie odizolowane, dzięki czemu właściciel obciążenia nie ma dostępu do zasobów innych obciążeń.

## <a name="resource-management-model"></a>Model zarządzania zasobami

Teraz, Po zaprojektowaniu modelu uprawnień o najniższych uprawnieniach, przyjrzyjmy się, aby zapoznać się z niektórymi praktycznymi aplikacjami tych modeli ładu. Należy odwoływać się od wymagań, które muszą obsługiwać następujące trzy środowiska:

1. **Środowisko infrastruktury udostępnionej:** Grupa zasobów współużytkowana przez wszystkie obciążenia. Są to takie zasoby, jak bramy sieci, zapory i usługi zabezpieczeń.
2. **Środowisko produkcyjne:** Wiele grup zasobów reprezentujących wiele obciążeń produkcyjnych. Te zasoby są używane do hostowania artefaktów aplikacji prywatnych i publicznych. Te zasoby zwykle mają ścisłe modele zarządzania i zabezpieczeń, aby chronić zasoby, kod aplikacji i dane przed nieautoryzowanym dostępem.
3. **Środowisko przedprodukcyjne:** Wiele grup zasobów reprezentujących wiele obciążeń nieprodukcyjnych. Te zasoby są używane do programowania i testowania oraz mogą mieć bardziej swobodny model ładu, aby zapewnić lepszą elastyczność deweloperów. Zabezpieczenia w ramach tych grup powinny wzrosnąć, gdy proces tworzenia aplikacji jest zbliżony do środowiska produkcyjnego.

Dla każdego z tych trzech środowisk istnieje wymóg śledzenia danych kosztów według **właściciela obciążenia**, **środowiska**lub obu. Oznacza to, że chcesz poznać ciągły koszt **infrastruktury udostępnionej**, koszty związane z osobami zarówno w środowiskach **nieprodukcyjnych, jak i** **produkcyjnymi** , a na koniec łączny koszt **nieproduktywności** i środowiska **produkcyjnego** .

Wiesz już, że zasoby są objęte zakresem dwóch poziomów: **subskrypcji** i **grupy zasobów**. W związku z tym pierwsza decyzja polega na tym, jak organizować środowiska przez **subskrypcję**. Dostępne są tylko dwie możliwości: jedna subskrypcja lub wiele subskrypcji.

Przed zapoznaj się z przykładami każdego z tych modeli, przejdźmy do struktury zarządzania dla subskrypcji na platformie Azure.

Należy odwołać się od wymagań, które użytkownik ma w organizacji odpowiedzialnej za subskrypcje, a ten użytkownik jest właścicielem konta **właściciela subskrypcji** w dzierżawie usługi Azure AD. To konto nie ma uprawnień do tworzenia subskrypcji. Tylko **właściciel konta platformy Azure** ma uprawnienia do wykonania tej czynności:

![Właściciel konta platformy Azure tworzy subskrypcję ](../../_images/govern/design/governance-3-0b.png)
 _6: właściciel konta Azure tworzy subskrypcję._

Po utworzeniu subskrypcji **właściciel konta platformy Azure** może dodać konto **właściciela subskrypcji** do subskrypcji z rolą **właściciela** :

![Właściciel konta platformy Azure dodaje konto użytkownika właściciela subskrypcji do subskrypcji z rolą właściciela. ](../../_images/govern/design/governance-3-0c.png)
 _Rysunek 7. właściciel konta platformy Azure dodaje konto użytkownika **właściciela subskrypcji** do subskrypcji z rolą **właściciela** ._

Konto **właściciela subskrypcji** może teraz tworzyć **grupy zasobów** i delegować zarządzanie dostępem do zasobów.

Najpierw przyjrzyjmy się przykładowym modelowi zarządzania zasobami przy użyciu jednej subskrypcji. Pierwsza decyzja przedstawia sposób wyrównania grup zasobów do trzech środowisk. Dostępne są dwie opcje:

1. Wyrównaj każde środowisko do pojedynczej grupy zasobów. Wszystkie udostępnione zasoby infrastruktury są wdrażane w pojedynczej grupie zasobów **infrastruktury udostępnionej** . Wszystkie zasoby skojarzone z obciążeniami programistycznymi są wdrażane w pojedynczej grupie zasobów **deweloperskich** . Wszystkie zasoby skojarzone z obciążeniami produkcyjnymi są wdrażane w jednej **produkcyjnej** grupie zasobów dla środowiska **produkcyjnego** .
2. Utwórz osobne grupy zasobów dla każdego obciążenia, używając konwencji nazewnictwa i znaczników w celu dopasowania grup zasobów do każdego z tych trzech środowisk.

Zacznijmy od oceny pierwszej opcji. Będziesz używać modelu uprawnień, który został omówiony w poprzedniej sekcji, za pomocą jednego administratora usługi subskrypcji, który tworzy grupy zasobów i dodaje do nich użytkowników przy użyciu wbudowanej roli **współautor** lub **czytnika** .

<!-- docsTest:ignore managedBy -->
<!-- hub-vnet prod-vnet app1-dev-vnet app2-dev-vnet app1-prod-vnet app2-prod-vnet -->

1. Pierwsza wdrożona Grupa zasobów reprezentuje środowisko **infrastruktury udostępnionej** . Konto **właściciela subskrypcji** tworzy grupę zasobów dla udostępnionych zasobów infrastruktury o nazwie `netops-shared-rg` .
    ![Tworzenie grupy zasobów](../../_images/govern/design/governance-3-0d.png)
2. Konto **właściciela subskrypcji** dodaje do grupy zasobów konto **użytkownika operacji sieci** i przypisuje rolę **współautor** .
    ![Dodawanie użytkownika operacji sieciowych](../../_images/govern/design/governance-3-0e.png)
3. **Użytkownik operacji sieciowych** tworzy [bramę sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) i konfiguruje ją do łączenia się z lokalnym urządzeniem sieci VPN. **Użytkownik operacji sieciowych** stosuje także parę [tagów](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) do poszczególnych zasobów: `environment:shared` i `managedBy:netOps` . Gdy **administrator usługi subskrypcji** Eksportuje raport kosztów, koszty będą wyrównane do każdego z tych tagów. Pozwala to **administratorowi usługi subskrypcji** na przestawianie kosztów przy użyciu `environment` znacznika i `managedBy` znacznika. Zwróć uwagę na licznik **limity zasobów** w prawym górnym rogu rysunku. Każda subskrypcja platformy Azure ma [limity usług](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits)i aby pomóc zrozumieć efekt tych limitów, należy postępować zgodnie z limitem sieci wirtualnej dla każdej subskrypcji. Istnieje limit 1000 sieci wirtualnych na subskrypcję, a po wdrożeniu pierwszej sieci wirtualnej dostępne są teraz 999.
    ![Tworzenie bramy sieci VPN](../../_images/govern/design/governance-3-1.png)
4. Wdrożono dwie więcej grup zasobów. Pierwszy ma nazwę `prod-rg` . Ta grupa zasobów jest wyrównana ze środowiskiem produkcyjnym. Drugi ma nazwę `dev-rg` i jest wyrównany do środowiska deweloperskiego. Wszystkie zasoby skojarzone z obciążeniami produkcyjnymi są wdrażane w środowisku produkcyjnym, a wszystkie zasoby związane z obciążeniami programistycznymi są wdrażane w środowisku deweloperskim. W tym przykładzie wdrażane są tylko dwa obciążenia do każdego z tych dwóch środowisk, więc nie będą napotykane żadne limity usługi subskrypcji platformy Azure. Należy wziąć pod uwagę, że każda grupa zasobów ma limit 800 zasobów na grupę zasobów. Jeśli będziesz kontynuować dodawanie obciążeń do każdej grupy zasobów, ostatecznie osiągniesz ten limit.
    ![Tworzenie grup zasobów](../../_images/govern/design/governance-3-2.png)
5. Pierwszy **właściciel obciążenia** wysyła żądanie do **administratora usługi subskrypcji** i jest dodawany do każdej grupy zasobów środowiska projektowego i produkcyjnego z rolą **współautor** . Jak pokazano wcześniej, rola **współautor** zezwala użytkownikowi na wykonywanie dowolnej operacji poza przypisaniem roli innemu użytkownikowi. Pierwszy **właściciel obciążenia** może teraz tworzyć zasoby skojarzone z ich obciążeniem.
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-3.png)
6. Pierwszy **właściciel obciążenia** tworzy sieć wirtualną w każdej z dwóch grup zasobów z parą maszyn wirtualnych w każdym z nich. Pierwszy **właściciel obciążenia** stosuje `environment` `managedBy` Tagi i do wszystkich zasobów. Należy pamiętać, że licznik limit usług platformy Azure jest teraz równy 997 sieci wirtualnych.
    ![Tworzenie sieci wirtualnych](../../_images/govern/design/governance-3-4.png)
7. Żadna z sieci wirtualnych nie ma łączności z lokalnymi po utworzeniu. W tym typie architektury Każda sieć wirtualna musi być połączona z usługą **`hub-vnet`** w środowisku **infrastruktury udostępnionej** . Komunikacja równorzędna sieci wirtualnych tworzy połączenie między dwiema oddzielnymi sieciami wirtualnymi i zezwala na ruch sieciowy między nimi. Należy pamiętać, że Komunikacja równorzędna sieci wirtualnych nie jest z założenia przechodnie. Komunikacja równorzędna musi być określona w każdej z dwóch połączonych sieci wirtualnych, a w przypadku, gdy tylko jedna z sieci wirtualnych określa komunikację równorzędną, połączenie jest niekompletne. Aby zilustrować efekt tego, pierwszy **właściciel obciążenia** określa komunikację równorzędną między **`prod-vnet`** i **`hub-vnet`** . Zostanie utworzona pierwsza Komunikacja równorzędna, ale nie są przepływy ruchu, ponieważ uzupełniająca Komunikacja równorzędna z **`hub-vnet`** do **`prod-vnet`** nie została jeszcze określona. Pierwszy **właściciel obciążenia** kontaktuje się z użytkownikiem **operacji sieciowych** i żąda tego uzupełniającego połączenia komunikacji równorzędnej.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-5.png)
8. Użytkownik **operacji w sieci** przegląda żądanie, zatwierdza je, a następnie określa komunikację równorzędną w ustawieniach dla **`hub-vnet`** . Połączenie komunikacji równorzędnej zostało zakończone, a ruch sieciowy odbywa się między dwiema sieciami wirtualnymi.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-6.png)
9. Teraz drugi **właściciel obciążenia** wysyła żądanie do **administratora usługi subskrypcji** i jest dodawany do istniejących grup zasobów środowiska **produkcyjnego** i **programistycznego** z rolą **współautor** . Drugi **właściciel obciążenia** ma takie same uprawnienia dla wszystkich zasobów jak pierwszy **właściciel obciążenia** w każdej grupie zasobów.
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-7.png)
10. Drugi **właściciel obciążenia** tworzy podsieć w **`prod-vnet`** sieci wirtualnej, a następnie dodaje dwie maszyny wirtualne. Drugi **właściciel obciążenia** stosuje `environment` `managedBy` Tagi i do każdego zasobu.
    ![Tworzenie podsieci](../../_images/govern/design/governance-3-8.png)

Ten przykładowy model zarządzania zasobami umożliwia nam zarządzanie zasobami w trzech wymaganych środowiskach. Zasoby infrastruktury udostępnionej są chronione, ponieważ tylko jeden użytkownik w ramach subskrypcji ma uprawnienia dostępu do tych zasobów. Każdy właściciel obciążenia może korzystać z udostępnionych zasobów infrastruktury bez posiadania żadnych uprawnień do zasobów udostępnionych. Ten model zarządzania przestanie być przyczyną izolacji obciążeń, ponieważ zarówno **właściciele obciążeń** mogą uzyskać dostęp do zasobów każdego innego obciążenia.

Istnieje inny istotny problem z tym modelem, który może nie być od razu oczywisty. W tym przykładzie został **APP1 właściciel obciążenia** , który zażądał połączenia komunikacji równorzędnej sieci z usługą, **`hub-vnet`** Aby zapewnić łączność z siecią lokalną. Użytkownik **operacji sieciowych** ocenił to żądanie na podstawie zasobów wdrożonych w ramach tego obciążenia. Po dodaniu konta **właściciela subskrypcji** **app2go właściciela obciążenia** z rolą **współautor** ten użytkownik miał prawa dostępu do zarządzania wszystkimi zasobami w **`prod-rg`** grupie zasobów.

![Diagram przedstawiający prawa dostępu do zarządzania](../../_images/govern/design/governance-3-10.png)

Oznacza to, że **właściciel obciążenia APP2** miał uprawnienia do wdrożenia własnej podsieci z maszynami wirtualnymi w **`prod-vnet`** sieci wirtualnej. Domyślnie te maszyny wirtualne mają dostęp do sieci lokalnej. Użytkownik **operacji sieciowych** nie wie o tych maszynach i nie zatwierdził ich łączności w środowisku lokalnym.

Następnie Przyjrzyjmy się pojedynczej subskrypcji z wieloma grupami zasobów dla różnych środowisk i obciążeń. Należy zauważyć, że w poprzednim przykładzie zasoby dla każdego środowiska były łatwe do zidentyfikowania, ponieważ znajdowały się w tej samej grupie zasobów. Teraz, gdy takie grupowanie nie jest już konieczne, należy polegać na konwencji nazewnictwa grup zasobów w celu zapewnienia tej funkcjonalności.

1. Zasoby **infrastruktury udostępnionej** nadal będą mieć oddzielną grupę zasobów w tym modelu, dzięki czemu pozostają takie same. Każde obciążenie wymaga dwóch grup zasobów — jeden dla każdego środowiska **projektowego** i **produkcyjnego** . W przypadku pierwszego obciążenia konto **właściciela subskrypcji** tworzy dwie grupy zasobów. Pierwszy z nich nosi nazwę **APP1-prod-RG** , a druga **— Nazwa APP1-dev-RG**. Jak wspomniano wcześniej, ta konwencja nazewnictwa identyfikuje zasoby jako skojarzone z pierwszym obciążeniem, **APP1**i środowiskiem **deweloperskim** lub **produkcyjnym** . Ponownie konto **właściciela subskrypcji** dodaje **właściciela obciążenia APP1** do grupy zasobów z rolą **współautor** .
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-12.png)
2. Podobnie jak w przypadku pierwszego przykładu **właściciel obciążenia APP1** wdraża sieć wirtualną o nazwie **APP1-prod-VNET** w środowisku **produkcyjnym** oraz inną nazwę **APP1-dev-VNET** w środowisku **deweloperskim** . Następnie **właściciel obciążenia APP1** wysyła żądanie do użytkownika **operacji sieciowych** w celu utworzenia połączenia komunikacji równorzędnej. Należy zauważyć, że **właściciel obciążenia APP1** dodaje te same Tagi co w pierwszym przykładzie, a licznik limit został zmniejszony do 997 sieci wirtualnych pozostałych w ramach subskrypcji.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-13.png)
3. Konto **właściciela subskrypcji** tworzy teraz dwie grupy zasobów dla **właściciela obciążenia APP2**. Zgodnie z tymi samymi konwencjami co w przypadku **właściciela obciążenia APP1**grupy zasobów mają nazwę **APP2-prod-RG** i **APP2-dev-RG**. Konto **właściciela subskrypcji** dodaje **właściciela obciążenia APP2** do każdej grupy zasobów z rolą **współautor** .
    ![Dodawanie współautorów](../../_images/govern/design/governance-3-14.png)
4. Konto **właściciela obciążenia APP2** wdraża sieci wirtualne i maszyny wirtualne w grupach zasobów z tymi samymi konwencjami nazewnictwa. Dodawane są Tagi, a licznik limit został zmniejszony do 995 sieci wirtualnych pozostałych w ramach subskrypcji.
    ![Wdrażanie sieci wirtualnych i maszyn wirtualnych](../../_images/govern/design/governance-3-15.png)
5. Konto **właściciela obciążenia APP2** wysyła żądanie do **użytkownika operacji sieciowych** w celu komunikacji równorzędnej z usługą **APP2-prod-VNET** z **`hub-vnet`** . Użytkownik **operacji sieciowych** tworzy połączenie komunikacji równorzędnej.
    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-16.png)

Otrzymany model zarządzania jest podobny do pierwszego przykładu z kilkoma kluczowymi różnicami:

- Każdy z tych dwóch obciążeń jest izolowany przez obciążenie i środowisko.
- Ten model wymaga dwóch więcej sieci wirtualnych niż pierwszy przykładowy model. Chociaż nie jest to ważna różnica w przypadku tylko dwóch obciążeń, teoretyczny limit liczby obciążeń dla tego modelu wynosi 24.
- Zasoby nie są już pogrupowane w jednej grupie zasobów dla każdego środowiska. Grupowanie zasobów wymaga poznania konwencji nazewnictwa używanych dla każdego środowiska.
- Każda z połączeń równorzędnych sieci wirtualnych została sprawdzona i zatwierdzona przez **użytkownika operacji sieciowych**.

Teraz przyjrzyjmy się modelowi zarządzania zasobami przy użyciu wielu subskrypcji. W tym modelu porównujesz każde z trzech środowisk z oddzielną subskrypcją: subskrypcję **usług udostępnionych** , subskrypcję **produkcyjną** i na koniec subskrypcji **deweloperskiej** . Zagadnienia dotyczące tego modelu są podobne do modelu przy użyciu jednej subskrypcji w programie, aby określić sposób wyrównania grup zasobów do obciążeń. Określono już, że tworzenie grupy zasobów dla każdego obciążenia spełnia wymagania dotyczące izolacji obciążenia, więc w tym przykładzie nastąpi przeniesieniu do tego modelu.

1. W tym modelu istnieją trzy subskrypcje: **udostępniona infrastruktura**, **produkcja**i **programowanie**. Każda z tych trzech subskrypcji wymaga właściciela subskrypcji, a w prostym przykładzie użyjesz tego samego konta użytkownika dla wszystkich trzech. Zasoby **infrastruktury udostępnionej** są zarządzane podobnie jak dwa pierwsze przykłady, a pierwsze obciążenie jest skojarzone z grupą zasobów **APP1-RG** w środowisku **produkcyjnym** i grupą zasobów o tej samej nazwie w środowisku **deweloperskim** . Konto **właściciela obciążenia APP1** jest dodawane do każdej grupy zasobów z rolą *współautor**.

    ![Dodawanie współautorów](../../_images/govern/design/governance-3-17.png)

2. Podobnie jak w przypadku wcześniejszych przykładów, **właściciel obciążenia APP1** tworzy zasoby i żąda połączenia komunikacji równorzędnej z siecią wirtualną **infrastruktury udostępnionej** . Konto **właściciela obciążenia APP1** dodaje tylko tag, `managedBy` ponieważ nie jest już potrzebny `environment` tag. Oznacza to, że zasoby dla każdego środowiska są teraz pogrupowane w tej samej **subskrypcji** , a `environment` tag jest nadmiarowy. Licznik limit jest zmniejszany do 999 sieci wirtualnych.

    ![Tworzenie połączenia komunikacji równorzędnej](../../_images/govern/design/governance-3-18.png)

3. Na koniec konto **właściciela subskrypcji** powtarza proces dla drugiego obciążenia, dodając grupy zasobów z **właścicielem obciążenia APP2** w roli **współautor** . Wartość licznika limit dla każdej subskrypcji środowiska jest zmniejszana do 998 sieci wirtualnych.

Ten model zarządzania ma zalety w drugim przykładzie powyżej. Kluczową różnicą jest to, że limity są mniejsze od problemu ze względu na fakt, że są rozłożone na dwie subskrypcje. Wadą jest to, że dane o kosztach śledzone przez Tagi muszą być agregowane we wszystkich trzech subskrypcjach.

W związku z tym można wybrać jeden z tych dwóch przykładów modeli zarządzania zasobami w zależności od priorytetu wymagań. Jeśli przewidujesz, że Twoja organizacja nie osiągnie limitów usługi dla jednej subskrypcji, możesz użyć pojedynczej subskrypcji z wieloma grupami zasobów. Z drugiej strony, jeśli organizacja przewiduje wiele obciążeń, może być lepszym rozwiązaniem wielu subskrypcji dla każdego środowiska.

## <a name="implement-the-resource-management-model"></a>Implementowanie modelu zarządzania zasobami

Zapoznaj się z kilkoma różnymi modelami, które ułatwiają dostęp do zasobów platformy Azure. Teraz wykonaj kroki niezbędne do zaimplementowania modelu zarządzania zasobami z jedną subskrypcją dla każdej z **udostępnionych środowisk infrastruktury**, **produkcji**i **programowania** , korzystając z przewodnika projektowania. Dla wszystkich trzech środowisk będziesz mieć jedno konto **właściciela subskrypcji** . Każde obciążenie zostanie odizolowane w **grupie zasobów** z dodaniem **właściciela obciążenia** z rolą **współautor** .

> [!NOTE]
> Przeczytaj [Opis dostępu do zasobów na platformie Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles) , aby dowiedzieć się więcej na temat relacji między kontami i subskrypcjami platformy Azure.

Wykonaj następujące kroki:

1. Utwórz [konto platformy Azure](https://docs.microsoft.com/azure/active-directory/sign-up-organization) , jeśli organizacja jeszcze go nie ma. Osoba, która zarejestruje się na konto platformy Azure, zostaje administratorem konta platformy Azure, a lider organizacji musi wybrać osobę, która ma założyć tę rolę. Osoba ta będzie odpowiedzialna za:
    - Tworzenie subskrypcji.
    - Tworzenie i administrowanie dzierżawami [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) , które przechowują tożsamość użytkownika dla tych subskrypcji.
2. Zespół liderów w organizacji decyduje, kto jest odpowiedzialny za:
    - Zarządzanie tożsamościami użytkowników; [dzierżawa usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) jest tworzona domyślnie podczas tworzenia konta platformy Azure w organizacji, a administrator konta jest domyślnie dodawany jako [administrator globalny usługi Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) . Organizacja może wybrać innego użytkownika do zarządzania tożsamościami użytkowników, [przypisując do tego użytkownika rolę administratora globalnego usługi Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-assign-role-azure-portal).
    - Subskrypcje, co oznacza, że Ci użytkownicy:
        - Zarządzaj kosztami związanymi z użyciem zasobów w tej subskrypcji.
        - Zaimplementuj i Zachowaj najmniejszy model uprawnień na potrzeby dostępu do zasobów.
        - Śledź limity usług.
    - Udostępnione usługi infrastruktury (Jeśli organizacja zdecyduje się korzystać z tego modelu), co oznacza, że ten użytkownik jest odpowiedzialny za:
        - Łączność lokalna z siecią platformy Azure.
        - Własność łączności sieciowej na platformie Azure za pośrednictwem komunikacji równorzędnej sieci wirtualnej.
    - Właściciele obciążeń.
3. Administrator globalny usługi Azure AD [tworzy nowe konta użytkowników](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) dla:
    - Osoba, która będzie właścicielem subskrypcji dla każdej subskrypcji skojarzonej z każdym środowiskiem. Należy pamiętać, że jest to konieczne tylko wtedy, gdy **administrator usługi** subskrypcji nie będzie miał zadań związanych z zarządzaniem dostępem do zasobów dla każdej subskrypcji/środowiska.
    - Osoba, która będzie **użytkownikiem operacji sieciowych**.
    - Osoby, które są **właścicielami obciążeń**.
4. Administrator konta platformy Azure tworzy następujące trzy subskrypcje przy użyciu [portalu konta platformy Azure](https://account.azure.com/subscriptions):
    - Subskrypcja środowiska **infrastruktury udostępnionej** .
    - Subskrypcja środowiska **produkcyjnego** .
    - Subskrypcja środowiska **deweloperskiego** .
5. Administrator konta platformy Azure [dodaje właściciela usługi subskrypcji do każdej subskrypcji](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#to-assign-a-user-as-an-administrator).
6. Utwórz proces zatwierdzania dla **właścicieli obciążeń** , aby zażądać tworzenia grup zasobów. Proces zatwierdzania można zaimplementować na wiele sposobów, na przykład za pośrednictwem poczty e-mail, lub za pomocą narzędzia do zarządzania procesem, takiego jak [przepływy pracy programu SharePoint](https://support.office.com/article/introduction-to-sharepoint-workflow-07982276-54e8-4e17-8699-5056eff4d9e3). Proces zatwierdzania może wykonać następujące czynności:
    - **Właściciel obciążenia** przygotowuje zestawienie materiałów dla wymaganych zasobów platformy Azure w środowisku **programistycznym** , środowisku **produkcyjnym** lub w obu systemach i przesyła je do **właściciela subskrypcji**.
    - **Właściciel subskrypcji** przegląda zestawienie materiałów i weryfikuje żądane zasoby, aby upewnić się, że żądane zasoby są odpowiednie do ich planowanego użycia — na przykład, sprawdzając, czy żądane [rozmiary maszyn wirtualnych](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) są poprawne.
    - Jeśli żądanie nie zostanie zatwierdzone, **właściciel obciążenia** zostanie powiadomiony. Jeśli żądanie zostanie zatwierdzone, **właściciel subskrypcji** [tworzy żądaną grupę zasobów](https://docs.microsoft.com/azure/azure-resource-manager/manage-resource-groups-portal#create-resource-groups) zgodnie z [konwencjami nazewnictwa](../../ready/azure-best-practices/naming-and-tagging.md)organizacji, [dodaje **właściciela obciążenia** ](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment) z [rolą **współautor** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) i wysyła powiadomienie do **właściciela obciążenia** , który utworzył grupę zasobów.
7. Utwórz proces zatwierdzania dla właścicieli obciążeń, aby zażądać połączenia komunikacji równorzędnej sieci wirtualnej od właściciela udostępnionej infrastruktury. Tak jak w poprzednim kroku, ten proces zatwierdzania można zaimplementować za pomocą poczty e-mail lub narzędzia do zarządzania procesami.

Po wdrożeniu modelu ładu można wdrożyć udostępnione usługi infrastruktury.

## <a name="related-resources"></a>Powiązane zasoby

[Wbudowane role dla zasobów platformy Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Dowiedz się więcej o wdrażaniu infrastruktury podstawowej](../../infrastructure/virtual-machines/basic-workload.md)
