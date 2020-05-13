---
title: Strategie migracji aplikacji mainframe
description: Poznaj strategie, takie jak rehostowanie, wycofywanie, ponowne kompilowanie lub zastępowanie aplikacji do migracji ze środowisk mainframe na platformę Azure.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a4b66a43cdf3524b23c109cdc5fa4e965c6e01f4
ms.sourcegitcommit: 60d8b863d431b5d7c005f2f14488620b6c4c49be
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83217663"
---
<!-- cSpell:ignore njray nanra Attunity Codit DRDA ISAM ISQL LPARS VSAM ODBC JDBC GDGs REXX TIP dbextents Raincode Tmax -->

# <a name="mainframe-application-migration"></a>Migracja aplikacji komputerów mainframe

W przypadku migrowania aplikacji ze środowisk mainframe na platformę Azure większość zespołów korzysta z podejścia typu Pragmatic: należy ponownie użyć wszędzie tam, gdzie to możliwe, a następnie rozpocząć wdrożenie etapowe, w przypadku których aplikacje są podpisywane lub zastępowane.

Migracja aplikacji zwykle obejmuje co najmniej jedną z następujących strategii:

- **Rehostowanie:** Możesz przenieść istniejący kod, programy i aplikacje z komputera mainframe, a następnie ponownie skompilować kod do uruchomienia w emulatorze mainframe hostowanym w wystąpieniu w chmurze. Takie podejście zwykle zaczyna się od przeniesienia aplikacji do emulatora opartego na chmurze, a następnie Migrowanie bazy danych do bazy danych opartej na chmurze. Niektóre Inżynieria i refaktoryzacji są wymagane wraz z konwertowaniem danych i plików.

    Alternatywnie można rehostować za pomocą tradycyjnego dostawcy hostingu. Jedną z głównych korzyści związanych z chmurą jest zarządzanie infrastrukturą. Możesz znaleźć dostawcę centrum danych, który będzie hostować Twoje obciążenia komputera mainframe. Ten model może kupić czas, zmniejszyć liczbę dostawców i zwiększyć koszty przejściowe.

- **Wycofywanie:** Wszystkie aplikacje, które nie są już potrzebne, powinny zostać wycofane przed migracją.

- **Kompiluj ponownie:** Niektóre organizacje decydują się na całkowite odpisanie programów przy użyciu nowoczesnych technik. Mając na względzie dodatkowy koszt i złożoność tego podejścia, nie jest to powszechnie zgodne z podejściem do podnoszenia i przesunięcia. Często po migracji tego typu warto rozpocząć zastępowanie modułów i kodu za pomocą aparatów transformacji kodu.

- **Zamień:** Takie podejście zastępuje funkcję mainframe z równoważnymi funkcjami w chmurze. Oprogramowanie jako usługa (SaaS) to jedna z opcji, która korzysta z rozwiązania utworzonego w ramach problemu dla przedsiębiorstw, takiego jak finanse, zasoby ludzkie, produkcja i planowanie zasobów przedsiębiorstwa. Ponadto dostępne są wiele aplikacji specyficznych dla branży, które rozwiązują problemy, które są używane do rozwiązywania niestandardowych rozwiązań typu mainframe.

Należy rozważyć rozpoczęcie od planowania obciążeń, które mają być początkowo migrowane, a następnie określić te wymagania dotyczące przenoszenie skojarzonych aplikacji, starszych baz kodu i baz danych.

## <a name="mainframe-emulation-in-azure"></a>Emulacja mainframe na platformie Azure

Usługi Azure Cloud Services mogą emulować tradycyjne środowiska mainframe, umożliwiając ponowne używanie istniejącego kodu i aplikacji mainframe. Typowe składniki serwera, które można emulować, to m.in. przetwarzanie transakcji online (OLTP), przetwarzanie wsadowe i systemy pozyskiwania danych.

### <a name="oltp-systems"></a>Systemy OLTP

Wiele komputerów mainframe ma systemy OLTP, które przetwarzają tysiące lub miliony aktualizacji dla dużej liczby użytkowników. Aplikacje te często korzystają z przetwarzania transakcji oraz oprogramowania obsługującego formularz ekranu, takie jak system kontroli informacji o klientach (CICS), systemy zarządzania informacjami (IMS) i procesor interfejsu terminalu (TIP).

Gdy przenosisz aplikacje OLTP na platformę Azure, emulatory dla monitorów transakcji typu mainframe (TP) są dostępne do uruchamiania jako usługa (IaaS) przy użyciu maszyn wirtualnych na platformie Azure. Na serwerach sieci Web można również zaimplementować obsługę ekranu i funkcje formularza. Takie podejście może być połączone z interfejsami API bazy danych, takimi jak obiekty danych ActiveX (ADO), Open Database Connectivity (ODBC) i JDBC (Java Database Connectivity) na potrzeby dostępu do danych i transakcji.

### <a name="time-constrained-batch-updates"></a>Aktualizacje partii z ograniczeniami czasowymi

Wiele systemów mainframe wykonuje comiesięczne lub roczne aktualizacje milionów rekordów kont, takich jak te używane w bankowości, ubezpieczeniach i administracji publicznej. Komputery mainframe obsługują te typy obciążeń, oferując systemy obsługi danych o wysokiej przepływności. Komputery mainframe są zwykle szeregowe i są zależne od operacji wejścia/wyjścia na sekundę (IOPS) dostarczonych przez szkielet mainframe w celu uzyskania wydajności.

Środowiska wsadowe oparte na chmurze używają równoległych sieci obliczeniowych i o dużej szybkości na potrzeby wydajności. Jeśli potrzebujesz zoptymalizować wydajność usługi Batch, platforma Azure udostępnia różne opcje obliczeń, magazynowania i sieci.

### <a name="data-ingestion-systems"></a>Systemy pozyskiwania danych

Komputery mainframe pobierają duże partie danych z usług detalicznych, finansowych, produkcyjnych i innych rozwiązań do przetworzenia. Na platformie Azure można używać prostych narzędzi wiersza polecenia, takich jak [AzCopy](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy) do kopiowania danych do i z lokalizacji magazynu. Można również użyć usługi [Azure Data Factory](https://docs.microsoft.com/azure/data-factory/introduction) , co pozwala na pozyskiwanie danych z różnych magazynów danych w celu tworzenia i planowania przepływów pracy opartych na danych.

Oprócz środowisk emulacji platforma Azure zapewnia usługi platformy jako usługa (PaaS) i usługi analityczne, które mogą ulepszyć istniejące środowiska mainframe.

## <a name="migrate-oltp-workloads-to-azure"></a>Migrowanie obciążeń OLTP na platformę Azure

Podejście do podnoszenia i przesunięcia to opcja bez kodu umożliwiająca szybkie Migrowanie istniejących aplikacji na platformę Azure. Każda aplikacja jest migrowana zgodnie z oczekiwaniami, która zapewnia korzyści z chmury bez ryzyka i kosztów związanych z wprowadzaniem zmian w kodzie. Użycie emulatora na potrzeby monitorów transakcji typu mainframe (TP) na platformie Azure obsługuje takie podejście.

Monitory TP są dostępne od różnych dostawców i uruchamiane na maszynach wirtualnych — opcja infrastruktura jako usługa (IaaS) na platformie Azure. Poniższe diagramy przed i po pokazują migrację aplikacji online obsługiwanej przez IBM DB2, system zarządzania relacyjnymi bazami danych (DBMS) na komputerze mainframe firmy IBM z/OS. W programie DB2 dla systemu z/OS są wykorzystywane pliki metody dostępu do magazynu wirtualnego (VSAM) w celu przechowywania danych i indeksowania metody dostępu sekwencyjnego (ISAM) dla plików prostych. Ta architektura używa również CICS do monitorowania transakcji.

!["Podnieś i Przenieś" Migracja środowiska mainframe na platformę Azure przy użyciu oprogramowania do emulacji](../../_images/mainframe-migration/mainframe-vs-azure.png)

Na platformie Azure środowiska emulacji są używane do uruchamiania Menedżera TP i zadań wsadowych korzystających z JCL. W warstwie danych DB2 jest zastępowany przez [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), chociaż Microsoft SQL Server, DB2 LUW lub Oracle Database może być również używany. Emulator obsługuje funkcję IMS, VSAM i SEQ. Narzędzia do zarządzania systemem komputera mainframe są zastępowane przez usługi platformy Azure i oprogramowanie od innych dostawców, które są uruchamiane na maszynach wirtualnych.

Funkcje obsługi ekranu i wpisów formularzy są powszechnie implementowane przy użyciu serwerów sieci Web, które można łączyć z interfejsami API bazy danych, takimi jak ADO, ODBC i JDBC na potrzeby dostępu do danych i transakcji. Dokładny wiersz składników usługi Azure IaaS do użycia zależy od preferowanego systemu operacyjnego. Przykład:

- Maszyny wirtualne oparte na systemie Windows: Internet Information Server (IIS) wraz z ASP.NET na potrzeby obsługi ekranu i logiki biznesowej. Użyj ADO.NET do uzyskiwania dostępu do danych i transakcji.

- Maszyny wirtualne oparte na systemie Linux: dostępne serwery aplikacji oparte na języku Java, takie jak Apache Tomcat na potrzeby obsługi ekranu i funkcjonalności biznesowej opartej na języku Java. Użyj JDBC do uzyskiwania dostępu do danych i transakcji.

## <a name="migrate-batch-workloads-to-azure"></a>Migrowanie obciążeń wsadowych do platformy Azure

Operacje wsadowe na platformie Azure różnią się od typowego środowiska wsadowego na mainframe. Zadania wsadowe komputera mainframe są zwykle szeregowe i są zależne od liczby operacji we/wy dostarczonej przez szkielet mainframe w celu uzyskania wydajności. Oparte na chmurze środowiska wsadowe wykorzystują równoległe i szybkie sieci do wydajności.

Aby zoptymalizować wydajność przetwarzania wsadowego przy użyciu platformy Azure, należy rozważyć opcje [obliczeń](https://docs.microsoft.com/azure/virtual-machines/windows/overview), [magazynu](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction), [sieci](https://azure.microsoft.com/blog/maximize-your-vm-s-performance-with-accelerated-networking-now-generally-available-for-both-windows-and-linux)i [monitorowania](https://docs.microsoft.com/azure/azure-monitor/overview) w następujący sposób.

### <a name="compute"></a>Wystąpienia obliczeniowe

Używanych

- Maszyny wirtualne o najwyższej szybkości zegara. Aplikacje mainframe są często typowymi procesorami, a komputery typu mainframe mają bardzo wysoką szybkość zegara.

- Maszyny wirtualne o dużej pojemności pamięci, aby umożliwić buforowanie obszarów roboczych danych i aplikacji.

- Maszyny wirtualne o wyższej gęstości procesorów wirtualnych vCPU, aby wykorzystać przetwarzanie wielowątkowe, jeśli aplikacja obsługuje wiele wątków.

- Przetwarzanie równoległe, jak platforma Azure umożliwia łatwe skalowanie do przetwarzania równoległego, zapewniając większą moc obliczeniową dla uruchomienia partii.

### <a name="storage"></a>Magazyn

Używanych

- [Dysk SSD Azure Premium](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage) lub [Azure Ultra SSD](https://docs.microsoft.com/azure/virtual-machines/windows/disks-ultra-ssd) dla maksymalnej liczby operacji we/wy na sekundę.

- Rozłożenie z wieloma dyskami dla większej liczby operacji we/wy na rozmiar magazynu.

- Partycjonowanie magazynu w celu rozłożenia operacji we/wy na wiele urządzeń magazynujących platformy Azure.

### <a name="networking"></a>Networking

- Używaj [przyspieszonej sieci platformy Azure](https://docs.microsoft.com/azure/virtual-network/create-vm-accelerated-networking-powershell) , aby zminimalizować opóźnienia.

### <a name="monitoring"></a>Monitorowanie

- Narzędzia do monitorowania, [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/overview), [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview)i dzienniki platformy Azure umożliwiają administratorom monitorowanie dowolnej wydajności przebiegów wsadowych i eliminowanie wąskich gardeł.

## <a name="migrate-development-environments"></a>Migruj środowiska deweloperskie

Rozproszone architektury chmury polegają na różnych zestawach narzędzi programistycznych, które zapewniają zalety nowoczesnych praktyk i języków programowania. Aby ułatwić to przejście, można użyć środowiska programistycznego z innymi narzędziami przeznaczonymi do emulowania środowisk IBM z/OS. Na poniższej liście przedstawiono opcje firmy Microsoft i innych dostawców:

| Składnik        | Opcje platformy Azure                                                                                                                                  |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| System z/OS             | Windows, Linux lub UNIX                                                                                                                      |
| CICS             | Usługi platformy Azure oferowane przez firmę Micro Focus, Oracle, GT Software (Fujitsu), TmaxSoft, Raincode i NTT, lub Przepisz przy użyciu Kubernetes |
| ISP              | Usługi platformy Azure oferowane przez firmę Micro Focus i Oracle                                                                                  |
| Asemblera        | Usługi platformy Azure z Raincode i TmaxSoft; lub COBOL, C lub Java lub mapowanie na funkcje systemu operacyjnego               |
| JCL              | JCL, PowerShell lub inne narzędzia do obsługi skryptów                                                                                                   |
| COBOL            | COBOL, C lub Java                                                                                                                            |
| Tocz          | Naturalne, COBOL, C lub Java                                                                                                                  |
| Pascal i PL/I | Pascal, PL/I, COBOL, C lub Java                                                                                                           |
| REXX i PL/I    | REXX, PowerShell lub inne narzędzia do obsługi skryptów                                                                                                  |

## <a name="migrate-databases-and-data"></a>Migrowanie baz danych i danych

Migracja aplikacji zwykle obejmuje rehostowanie warstwy danych. Możesz migrować SQL Server, Open Source i innych relacyjnych baz danych do w pełni zarządzanych rozwiązań na platformie Azure, takich jak [Azure SQL Database wystąpienie zarządzane](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), [usługa Azure Database Service for PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview), a także [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) z [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).

Na przykład można przeprowadzić migrację, jeśli używasz warstwy danych komputera mainframe:

- IBM DB2 lub baza danych IMS, Użyj usługi Azure SQL Database, SQL Server, DB2 LUW lub Oracle Database na platformie Azure.

- VSAM i inne pliki płaskie, używają plików prostych z indeksowaną metodą dostępu sekwencyjnego (ISAM) dla usługi Azure SQL, SQL Server, DB2 LUW lub Oracle.

- Grupy dat generacji (GDGs), Migrowanie do plików na platformie Azure, które używają konwencji nazewnictwa i rozszerzeń nazw plików, które zapewniają podobną funkcjonalność do GDGs.

Warstwa danych IBM zawiera kilka najważniejszych składników, które należy również migrować. Na przykład podczas migrowania bazy danych można również migrować kolekcję danych zawartych w pulach, z których każda zawiera klasy DB, które są zestawami danych VSAM z/OS. Migracja musi zawierać katalog, który identyfikuje lokalizacje danych w pulach magazynu. Ponadto w planie migracji należy wziąć pod uwagę dziennik bazy danych, który zawiera rekord operacji wykonywanych w bazie danych. Baza danych może mieć jeden, dwa (podwójny lub alternatywny) lub cztery (podwójne i alternatywne) dzienniki.

Migracja bazy danych obejmuje również następujące składniki:

- **Menedżer bazy danych:** Zapewnia dostęp do danych w bazie danych programu. Menedżer bazy danych działa we własnej partycji w środowisku z/OS.
- **Żądający aplikacji:** Akceptuje żądania z aplikacji przed przekazaniem ich do serwera aplikacji.
- **Karta zasobów online:** Zawiera składniki żądające aplikacji do użycia w transakcjach CICS.
- **Karta zasobów wsadowych:** Implementuje składniki żądającej aplikacji dla aplikacji wsadowych z/OS.
- **Interaktywny SQL (ISQL):** Działa jako aplikacja CICS i interfejs umożliwiający użytkownikom wprowadzanie instrukcji SQL lub poleceń operatora.
- **CICS:** Działa pod kontrolą CICS przy użyciu dostępnych zasobów i źródeł danych w CICS.
- **Aplikacja wsadowa:** Uruchamia logikę procesu bez interaktywnej komunikacji z użytkownikami, aby na przykład generować zbiorcze aktualizacje danych lub generować raporty z bazy danych.

## <a name="optimize-scale-and-throughput-for-azure"></a>Optymalizowanie skalowania i przepływności platformy Azure

Ogólnie mówiąc, Komputery mainframe można skalować w górę, podczas gdy chmura jest skalowana. Aby zoptymalizować skalę i przepływność aplikacji w stylu komputera mainframe działającego na platformie Azure, ważne jest, aby zrozumieć, jak Komputery mainframe mogą oddzielić i izolować aplikacje. Komputery mainframe z/OS używają funkcji o nazwie partycje logiczne (LPARS) do izolowania zasobów dla określonej aplikacji w jednym wystąpieniu i zarządzania nimi.

Na przykład, Komputery mainframe mogą używać jednej partycji logicznej (LPAR) dla regionu CICS ze skojarzonymi programami COBOL i osobnym LPAR dla bazy danych DB2. Dodatkowe LPARs są często używane do środowisk tworzenia, testowania i przemieszczania.

Na platformie Azure bardziej powszechne jest używanie oddzielnych maszyn wirtualnych do obsługi tego celu. Architektury platformy Azure zwykle wdrażają maszyny wirtualne dla warstwy aplikacji, oddzielny zestaw maszyn wirtualnych dla warstwy danych, inny zestaw do opracowania i tak dalej. Każdą warstwę przetwarzania można zoptymalizować przy użyciu najbardziej odpowiedniego typu maszyn wirtualnych i funkcji dla tego środowiska.

Ponadto każda warstwa może również zapewnić odpowiednie usługi odzyskiwania po awarii. Na przykład maszyny wirtualne z maszynami wirtualnymi i bazami danych mogą wymagać odzyskiwania gorącego lub ciepłego, podczas gdy maszyny wirtualne do tworzenia i testowania obsługują zimne odzyskiwanie.

Na poniższej ilustracji przedstawiono możliwe wdrożenie platformy Azure przy użyciu lokacji podstawowej i dodatkowej. W lokacji głównej maszyny wirtualne produkcyjne, przejściowe i testowe są wdrażane z wysoką dostępnością. Lokacja dodatkowa służy do tworzenia kopii zapasowych i odzyskiwania po awarii.

![Możliwe wdrożenie platformy Azure przy użyciu lokacji podstawowej i dodatkowej](../../_images/mainframe-migration/migration-backup-dr.png)

## <a name="perform-a-staged-mainframe-to-azure"></a>Wykonywanie przemieszczanego komputera mainframe na platformie Azure

Przenoszenie rozwiązań z komputera mainframe na platformę Azure może wymagać migracji _etapowej_ , w której niektóre aplikacje są przenoszone w pierwszej kolejności, a inne pozostają na komputerze mainframe tymczasowo lub trwale. Takie podejście zwykle wymaga systemów, które umożliwiają aplikacji i baz danych współdziałanie między mainframe i platformą Azure.

Typowym scenariuszem jest przeniesienie aplikacji na platformę Azure, zachowując dane używane przez aplikację na komputerze mainframe. Określone oprogramowanie służy do włączania dostępu do danych z komputera mainframe przez aplikacje na platformie Azure. Na szczęście wiele różnych rozwiązań zapewnia integrację między platformą Azure i istniejącymi środowiskami mainframe, obsługą scenariuszy hybrydowych oraz migracją w czasie. Partnerzy firmy Microsoft, niezależni dostawcy oprogramowania i Integratory systemów mogą pomóc Ci w podróży.

Jedną z opcji jest [Microsoft Host Integration Server](https://docs.microsoft.com/host-integration-server), rozwiązanie, które zapewnia rozproszoną architekturę relacyjnej bazy danych (DRDA) wymaganą dla aplikacji na platformie Azure, aby uzyskiwać dostęp do danych w programie DB2, które pozostają na komputerze mainframe. Inne opcje integracji komputerów typu mainframe z platformą Azure obejmują rozwiązania firmy IBM, Attunity, Codit, innych dostawców i opcje typu open source.

## <a name="partner-solutions"></a>Rozwiązania partnerskie

Jeśli rozważasz migrację komputerów mainframe, ekosystem partnerów jest dostępny do pomocy.

System Azure zapewnia sprawdzoną, wysoką dostępność i skalowalną infrastrukturę dla systemów, które są obecnie uruchamiane na komputerach mainframe. Niektóre obciążenia można migrować ze względu na łatwość. Inne obciążenia, które są zależne od starszego oprogramowania systemu, takie jak CICS i ISP, mogą być przenoszone przy użyciu rozwiązań partnerskich i migrowane na platformę Azure w miarę upływu czasu. Bez względu na to, co nastąpi, firma Microsoft i jej partnerzy są dostępni, aby pomóc zoptymalizować rozwiązanie dla platformy Azure przy zachowaniu funkcjonalności oprogramowania systemu mainframe.

## <a name="learn-more"></a>Dowiedz się więcej

Więcej informacji zawierają następujące zasoby:

- [Rozpoczynanie pracy z platformą Azure](https://docs.microsoft.com/azure)

- [Wdrażanie programu IBM DB2 pureScale na platformie Azure](https://azure.microsoft.com/resources/deploy-ibm-db2-purescale-on-azure)

- [Dokumentacja Host Integration Server](https://docs.microsoft.com/host-integration-server)
