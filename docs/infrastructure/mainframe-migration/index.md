---
title: Omówienie migracji komputera mainframe
description: Migruj bazy danych, aplikacje i obciążenia komputerów mainframe na platformę Azure, aby uzyskać sprawdzoną, wysoce dostępną i skalowalną infrastrukturę bez wielu wad komputerów mainframe.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b38408033231a4ac1d8debe889117c2f5220c676
ms.sourcegitcommit: 72a280cd7aebc743a7d3634c051f7ae46e4fc9ae
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78223667"
---
<!-- cspell:ignore nanra njray dbspaces dbextents VSAM RACF LPARS ASSGN DLBL EXTENT LIBDEF EXEC IPLs -->

# <a name="mainframe-migration-overview"></a>Omówienie migracji komputera mainframe

Wiele firm i organizacji czerpie korzyści wynikające z przeniesienia niektórych lub wszystkich swoich obciążeń, aplikacji i baz danych do chmury. Platforma Azure udostępnia funkcje typu mainframe w skali chmury bez wielu wad związanych z komputerami mainframe.

Termin mainframe zazwyczaj odnosi się do dużego systemu komputerowego, ale większość wdrożonych obecnie systemów mainframe stanowią serwery IBM System Z lub systemy firmy IBM zgodne z innymi platformami sprzętowymi, na których działają systemy MVS, DOS, VSE, OS/390 lub z/OS. Systemy mainframe są nadal używane w wielu branżach do obsługi ważnych systemów informatycznych i są stosowane w bardzo specyficznych scenariuszach, takich jak duże, wysoce rozbudowane środowiska IT intensywnie korzystające z transakcji.

Migracja do chmury umożliwia firmom modernizację własnej infrastruktury. Dzięki usługom w chmurze możesz tworzyć aplikacje mainframe (wraz z ich wszystkimi zaletami), które będą dostępne jako obciążenie za każdym razem, gdy Twoja organizacja będzie tego potrzebować. Wiele obciążeń można przenieść na platformę Azure z uwzględnieniem tylko drobnych zmian kodu, takich jak aktualizacja nazw baz danych. Możliwe jest migrowanie bardziej złożonych obciążeń przy użyciu podejścia etapowego.

Większość firm z listy Fortune 500 korzysta już z platformy Azure na potrzeby obciążeń o kluczowym znaczeniu. Istotne podstawowe zachęty dostępne na platformie Azure motywują do przeprowadzenia wielu projektów migracji. Firmy zwykle najpierw przenoszą na platformę Azure obciążenia programistyczne i testowe, a następnie zasoby DevOps, pocztę e-mail i funkcje odzyskiwania po awarii jako usługi.

## <a name="intended-audience"></a>Docelowi odbiorcy

Jeśli rozważasz migrację lub dodanie usług w chmurze jako opcję dla Twojego środowiska IT, ten przewodnik jest przeznaczony dla Ciebie.

Te wskazówki ułatwiają organizacjom IT rozpoczęcie rozmowy na temat migracji. Możesz znać lepiej platformę Azure i infrastruktury oparte na chmurze niż komputery mainframe, więc ten przewodnik rozpoczyna się od przeglądu sposobu działania komputerów mainframe. Następnie opisywane są różne strategie służące do określenia, co należy zmigrować i w jaki sposób.

## <a name="mainframe-architecture"></a>Architektura komputera mainframe

W późnych latach 50. komputery mainframe zostały zaprojektowane jako serwery skalowalne w górę służące do uruchamiania dużej liczby transakcji online i przetwarzania wsadowego. Z tego powodu komputery mainframe mają oprogramowanie na potrzeby formularzy transakcji online (nazywanych też czasami zielonymi ekranami) i systemów we/wy o wysokiej wydajności służących do przetwarzania uruchomień wsadowych.

Komputery mainframe są znane ze swojej wysokiej niezawodności i dostępności oraz możliwości uruchamiania ogromnej liczby transakcji online i zadań wsadowych. Transakcja jest wynikiem operacji przetwarzania zainicjowanej przez pojedyncze żądanie, zwykle przez użytkownika z poziomu terminala. Transakcja może też pochodzić z wielu innych źródeł, w tym stron internetowych, zdalnych stacji roboczych i aplikacji z innych systemów informatycznych. Transakcja może być również automatycznie wyzwalana we wstępnie zdefiniowanym terminie, jak pokazano na poniższej ilustracji.

![Składniki typowej architektury komputera mainframe firmy IBM](../../_images/mainframe-migration/mainframe-architecture.png)

Typowa architektura komputera mainframe firmy IBM obejmuje następujące składniki:

- **Systemy frontonu:** Użytkownicy mogą inicjować transakcje z poziomu terminali, stron internetowych lub zdalnych stacji roboczych. Aplikacje mainframe często mają niestandardowe interfejsy użytkownika, które można zachować po migracji na platformę Azure. Emulatory terminali (nazywane również terminalami z zielonym ekranem) są nadal używane do uzyskiwania dostępu do aplikacji mainframe.

- **Warstwa aplikacji:** Komputery mainframe zazwyczaj zawierają system kontroli informacji o klientach (CICS, customer information control system), wiodący pakiet zarządzania transakcjami dla systemu mainframe IBM z/OS, który jest często używany wraz z systemem IBM Information Management System (IMS), czyli menedżerem transakcji opartym na komunikatach. Systemy wsadowe obsługują aktualizacje danych o wysokiej przepływności dla dużej liczby rekordów kont.

- **Kod:** Języki programowania używane przez komputery mainframe to COBOL, Pascal i PL/I oraz język naturalny. Język kontroli zadań (JCL) jest używany do pracy z systemem z/OS.

- **Warstwa bazy danych:** Wspólny system zarządzania relacyjnymi bazami danych (DBMS) dla systemu z/OS to IBM DD2. Służy on do zarządzania strukturami danych o nazwie *dbspaces*, które zawierają co najmniej jedną tabelę i są przypisane do pul magazynów fizycznych zestawów danych o nazwie *dbextents*. Dwa ważne składniki bazy danych to katalog, który identyfikuje lokalizacje danych w pulach magazynu, oraz dziennik zawierający zapis operacji wykonywanych w bazie danych. Obsługiwane są różne formaty danych plików prostych. System DB2 for z/OS zwykle korzysta z zestawów danych VSAM do przechowywania danych.

- **Warstwa zarządzania:** Komputery mainframe firmy IBM obejmują oprogramowanie do planowania, takie jak TWS-OPC, narzędzia do drukowania i wyprowadzania danych wyjściowych, takie jak CA-SAR i SPOOL, oraz system kontroli źródła dla kodu. Bezpieczna kontrola dostępu dla systemu z/OS jest obsługiwana za pomocą funkcji kontroli dostępu do zasobów (RACF, resource access control facility). Menedżer bazy danych zapewnia dostęp do danych w bazie danych i działa na własnej partycji w środowisku z/OS.

- **Partycje LPAR:** Partycje logiczne (LPAR) są używane do dzielenia zasobów obliczeniowych. Fizyczny komputer mainframe jest podzielony na wiele partycji LPAR.

- **System z/OS:** 64-bitowy system operacyjny, który jest najczęściej używany przez komputery mainframe firmy IBM.

Systemy firmy IBM używają monitora transakcji, takiego jak CICS, do śledzenia wszystkich aspektów transakcji biznesowych i zarządzania nimi. System CICS zarządza udostępnianiem zasobów, integralnością danych i priorytetyzacją wykonywania. Służy również do autoryzowania użytkowników, przydzielania zasobów i przekazywania żądań bazy danych z aplikacji do menedżera bazy danych, takiego jak IBM DB2.

W celu bardziej precyzyjnego dostrajania system CICS jest często używany wraz z programem IMS/TM (wcześniej nazywanym IMS/Data Communications lub IMS/DC). Program IMS zaprojektowano w celu zmniejszenia nadmiarowości danych dzięki utrzymywaniu pojedynczej kopii danych. Stanowi on uzupełnienie systemu CICS jako monitor transakcji przez utrzymywanie stanu w trakcie całego procesu i rejestrowanie funkcji biznesowych w magazynie danych.

## <a name="mainframe-operations"></a>Operacje komputera mainframe

Poniżej przedstawiono typowe operacje komputera mainframe:

- **Tryb online:** Obciążenia obejmują przetwarzanie transakcji, zarządzanie bazami danych i połączenia. Są one często implementowane przy użyciu łączników systemu IBM DB2, CICS i z/OS.

- **Zadania wsadowe:** Zadania są uruchamiane bez interakcji z użytkownikiem, zwykle zgodnie z ustalonym harmonogramem, na przykład rano każdego dnia tygodnia. Zadania wsadowe można uruchamiać w systemach opartych na systemie Windows lub Linux przy użyciu emulatora JCL, takiego jak serwer Micro Focus Enterprise Server lub oprogramowanie BMC Control-M.

- **Język kontroli zadań (JCL):** Określ zasoby, które są konieczne do przetwarzania zadań wsadowych. Język JCL przekazuje te informacje do systemu z/OS za pomocą zestawu instrukcji kontroli zadań. Podstawowy język JCL zawiera sześć typów instrukcji: JOB, ASSGN, DLBL, EXTENT, LIBDEF i EXEC. Zadanie może zawierać kilka instrukcji EXEC (kroków), a każdy krok może mieć kilka instrukcji LIBDEF, ASSGN, DLBL i EXTENT.

- **Proces początkowego ładowania programu (IPL):**  Oznacza ładowanie kopii systemu operacyjnego z dysku do rzeczywistego magazynu procesora i uruchamianie go. Procesy IPL są używane do przywracania działania po przestoju. Proces IPL przypomina rozruch systemu operacyjnego na maszynach wirtualnych z systemem Windows lub Linux.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Fakty i mity](./myths-and-facts.md)
