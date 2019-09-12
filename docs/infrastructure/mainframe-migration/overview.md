---
title: Omówienie migracji komputera mainframe
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migruj aplikacje ze środowisk mainframe na platformę Azure, sprawdzoną, wysoką dostępność i skalowalną infrastrukturę dla systemów, które są obecnie uruchamiane na komputerach mainframe.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ab3692702744e5cca174fcae55ea7b9d34e72998
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/06/2019
ms.locfileid: "70831050"
---
# <a name="mainframe-migration-overview"></a>Omówienie migracji komputera mainframe

W wielu firmach i organizacjach korzyści wynikające z przeniesienia niektórych lub wszystkich ich obciążeń, aplikacji i baz danych do chmury. Platforma Azure udostępnia funkcje podobne do typu mainframe w skali chmury bez wielu wad skojarzonych z systemami mainframe.

Termin mainframe zazwyczaj odnosi się do dużego systemu komputerowego, ale większość wdrożonych obecnie komputerów mainframe to IBM System Z lub systemy zgodne z plug-in IBM z systemem systemu MVS, DOS, VSE, OS/390 lub Z/OS. Systemy mainframe są nadal używane w wielu branżach do uruchamiania ważnych systemów informacyjnych i mają miejsce w wysoce konkretnych scenariuszach, takie jak duże, wysoce rozbudowane środowiska IT intensywnie korzystające z transakcji.

Migracja do chmury umożliwia firmom modernizację infrastruktury. Dzięki usługom w chmurze możesz tworzyć aplikacje typu mainframe i zapewniane przez nie wartości, dostępne jako obciążenie za każdym razem, gdy organizacja go potrzebuje. Wiele obciążeń można przenieść na platformę Azure z uwzględnieniem tylko drobnych zmian kodu, takich jak aktualizowanie nazw baz danych. Możliwe jest Migrowanie bardziej złożonych obciążeń przy użyciu podejścia etapowego.

Większość firm listy Fortune 500 korzysta już z platformy Azure na potrzeby obciążeń krytycznych. Ważne środki na platformie Azure przedstawiają wiele projektów migracji. Firmy zwykle przenoszą obciążenia programistyczne i testowe na platformę Azure, a następnie DevOps, wiadomości e-mail i odzyskiwania po awarii jako usługi.

## <a name="intended-audience"></a>Docelowi odbiorcy

Ten przewodnik jest przeznaczony dla Ciebie, Jeśli rozważasz migrację lub dodanie usług w chmurze jako opcji środowiska IT.

Te wskazówki ułatwiają organizacjom IT rozpoczęcie rozmowy z migracją. Użytkownik może być bardziej zaznajomiony z platformą Azure i infrastrukturami opartymi na chmurze niż w przypadku komputerów mainframe, więc ten przewodnik rozpoczyna się od przeglądu sposobu działania komputerów mainframe i kontynuuje pracę z różnymi strategiami dotyczącymi określania, co i jak przeprowadzić migrację.

## <a name="mainframe-architecture"></a>Architektura komputera mainframe

W przypadku późnych 1950s Komputery mainframe zostały zaprojektowane jako serwery skalowalne w celu uruchamiania dużych ilości transakcji online i przetwarzania wsadowego. Z tego powodu Komputery mainframe mają oprogramowanie do formularzy transakcji online (nazywanych też zielonymi ekranami) i wysokiej wydajności systemy we/wy służące do przetwarzania wsadowych uruchomień.

Komputery mainframe mają reputację o wysokiej niezawodności i dostępności i są znane do uruchamiania ogromnych transakcji online i zadań wsadowych. Transakcja jest wynikiem operacji przetwarzania zainicjowanego przez pojedyncze żądanie, zwykle od użytkownika w terminalu. Transakcje mogą również pochodzić z wielu innych źródeł, w tym stron sieci Web, zdalnych stacji roboczych i aplikacji z innych systemów informacyjnych. Transakcja może być również automatycznie wyzwalana we wstępnie zdefiniowanym czasie, jak pokazano na poniższej ilustracji.

![Składniki w typowej architekturze IBM mainframe](../../_images/mainframe-migration/zOS-architectural-layers.png)

Typowa architektura IBM mainframe obejmuje następujące typowe składniki:

- **Systemy frontonu:** Użytkownicy mogą inicjować transakcje z terminali, stron sieci Web lub zdalnych stacji roboczych. Aplikacje mainframe często mają niestandardowe interfejsy użytkownika, które można zachować po migracji na platformę Azure. Emulatory terminali są nadal używane do uzyskiwania dostępu do aplikacji typu mainframe i są również nazywane terminalami zielonego ekranu.

- **Warstwa aplikacji:** Komputery mainframe zazwyczaj zawierają system kontroli informacji o klientach (CICS), wiodący pakiet zarządzania transakcjami dla systemu mainframe firmy IBM z/OS, który jest często używany w przypadku usługi IBM Information Management System (IMS). Systemy wsadowe obsługują aktualizacje danych o wysokiej przepływności dla dużych ilości rekordów kont.

- **Kodu** Języki programowania używane przez Komputery mainframe to COBOL, Pascal, PL/I i naturalne. Język kontroli zadań (JCL) jest używany do pracy z systemem z/OS.

- **Warstwa bazy danych:** Wspólny system zarządzania relacyjnymi bazami danych (DBMS) dla systemu z/OS to IBM DD2. Zarządza on strukturami danych o nazwie *Spaces* , które zawierają jedną lub więcej tabel i są przypisane do pul magazynów fizycznych zestawów danych o nazwie *dbzasięg*. Dwa ważne składniki bazy danych to katalog, który identyfikuje lokalizacje danych w pulach magazynu, oraz dziennik zawierający rekord operacji wykonywanych w bazie danych. Obsługiwane są różne formaty danych o płaskim pliku. W programie DB2 dla systemu z/OS są zwykle stosowane zestawy danych metody dostępu do magazynu wirtualnego (VSAM).

- **Warstwa zarządzania:** Komputery mainframe firmy IBM obejmują oprogramowanie do planowania, takie jak TWS-OPC, narzędzia do drukowania i wyprowadzania danych wyjściowych, takie jak CA-SAR i BUFOROWANIE, oraz system kontroli źródła dla kodu. Zabezpieczanie kontroli dostępu dla systemu z/OS jest obsługiwane przez funkcję kontroli dostępu do zasobów (RACF). Menedżer bazy danych zapewnia dostęp do danych w bazie danych i działa we własnej partycji w środowisku z/OS.

- **LPAR:** Partycje logiczne lub LPARs są używane do dzielenia zasobów obliczeniowych. Fizyczny mainframe jest podzielony na wiele LPARs.

- **system operacyjny z/OS:** 64-bitowy system operacyjny, który jest najczęściej używany przez Komputery mainframe firmy IBM.

Systemy firmy IBM używają monitora transakcji, takiego jak CICS, do śledzenia wszystkich aspektów transakcji biznesowej i zarządzania nimi. CICS zarządza udostępnieniem zasobów, integralności danych i priorytetyzacji wykonania. CICS autoryzuje użytkowników, przydziela zasoby i przekazuje żądania bazy danych przez aplikację do Menedżera bazy danych, takiego jak IBM DB2.

Aby precyzyjniej dostrajać, CICS jest często używany z usługą IMS/TM (dawniej w przypadku komunikacji z wieloma usługami (ISP/Data Communications, ISP/DC). IMS zaprojektowano w celu zmniejszenia nadmiarowości danych przez utrzymywanie pojedynczej kopii danych. Uzupełnia CICS jako monitor transakcji przez utrzymywanie stanu przez proces i rejestrowanie funkcji firmy w magazynie danych.

## <a name="mainframe-operations"></a>Operacje komputera mainframe

Poniżej przedstawiono typowe operacje komputera mainframe:

- **Sieci** Obciążenia obejmują przetwarzanie transakcji, zarządzanie bazami danych i połączenia. Są one często implementowane przy użyciu łączników IBM DB2, CICS i z/OS.

- **Sekwencja** Zadania są uruchamiane bez interakcji z użytkownikiem — zwykle w regularnych harmonogramach, takich jak każdy dzień tygodnia rano. Zadania usługi Batch można uruchamiać w systemach opartych na systemie Windows lub Linux przy użyciu emulatora JCL, takiego jak serwer Enterprise Server lub BMC Control-M.

- **Język kontroli zadań (JCL):** Określ zasoby, które są konieczne do przetwarzania zadań wsadowych. JCL przekazuje te informacje do systemu z/OS za pomocą zestawu instrukcji kontroli zadań. Podstawowa JCL zawiera sześć typów instrukcji: JOB, ASSGN, DLBL, zakres, LIBDEF i EXEC. Zadanie może zawierać kilka instrukcji EXEC (kroki), a każdy krok może mieć kilka instrukcji LIBDEF, ASSGN, DLBL i zakres.

- **Początkowe ładowanie programu (IPL):**  Odnosi się do ładowania kopii systemu operacyjnego z dysku do rzeczywistego magazynu procesora i uruchamiania go. IPLs są używane do odzyskiwania po przestoju. IPL przypomina rozruch systemu operacyjnego na maszynach wirtualnych z systemem Windows lub Linux.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Mitów i fakty](myths-and-facts.md)
