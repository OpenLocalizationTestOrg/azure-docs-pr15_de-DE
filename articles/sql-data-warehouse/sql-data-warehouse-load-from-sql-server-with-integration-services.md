<properties
   pageTitle="Laden von Daten aus SQL Server in Azure SQL Data Warehouse (SSIS) | Microsoft Azure"
   description="Es wird gezeigt, wie ein Paket SQL Server Integration Services (SSIS) zum Verschieben von Daten aus einer Vielzahl von Datenquellen in SQL Data Warehouse zu erstellen."
   services="sql-data-warehouse"
   documentationCenter="NA"
   authors="lodipalm"
   manager="barbkess"
   editor=""/>

<tags
   ms.service="sql-data-warehouse"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-services"
   ms.date="08/08/2016"
   ms.author="lodipalm;sonyama;barbkess"/>

# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Laden von Daten aus SQL Server in Azure SQL Data Warehouse (SSIS)

> [AZURE.SELECTOR]
- [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
- [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
- [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)


Erstellen eines Pakets SQL Server Integration Services (SSIS), um Daten aus SQL Server in Azure SQL-Data Warehouse zu laden. Sie können optional umstrukturieren, Transformieren und bereinigen die Daten beim passieren Datenfluss SSIS umfasst.

In diesem Lernprogramm werden Sie folgende Aufgaben ausführen:

- Erstellen Sie ein neues Integration Services-Projekt in Visual Studio.
- Verbinden Sie mit Datenquellen, einschließlich SQL Server (als Quelle) und SQL Data Warehouse (als Ziel).
- Entwerfen eines SSIS-Pakets, das Daten aus der Quelle in das Ziel geladen.
- Führen Sie das SSIS-Paket, um die Daten zu laden.

In diesem Lernprogramm verwendet SQL Server als Datenquelle. SQL Server konnte lokal oder in einer Azure-virtuellen Computern ausgeführt werden.

## <a name="basic-concepts"></a>Grundlegende Konzepte

Das Paket ist die Arbeitseinheit in SSIS. Verwandte Pakete sind in Projekten gruppiert. Erstellen Sie Projekte und Entwurf-Paketen in Visual Studio mit SQL Server Data Tools an. Des Entwurfsprozesses ist eine visuelle Prozess in dem Sie ziehen und Ablegen Komponenten aus der Toolbox auf die Entwurfsoberfläche, verbinden diese und legen Sie ihre Eigenschaften an. Nachdem Sie Ihrem Paket abgeschlossen haben, können Sie optional auf SQL Server für umfassende Verwaltung, Überwachung und Sicherheit bereitstellen.

## <a name="options-for-loading-data-with-ssis"></a>Optionen für das Laden von Daten mit SSIS

SQL Server Integration Services (SSIS) ist eine flexible Reihe von Tools, die eine Vielzahl von Optionen zum Herstellen einer Verbindung mit und Laden von Daten in SQL Data Warehouse bereitstellt.

1. Verwenden einer ADO Netz Ziel mit SQL Data Warehouse verbinden. In diesem Lernprogramm verwendet eine ADO Netz Ziel, da es die geringste Anzahl Konfigurationsoptionen hat.
2. Verwenden Sie OLE DB-Ziel Verbindung zu SQL Data Warehouse. Diese Option möglicherweise etwas bessere Leistung als das Ziel des ADO Netz bereitstellen.
3. Verwenden Sie die Aufgabe Azure Blob hochladen, um die Daten in Azure BLOB-Speicher Phaseneigenschaften. Verwenden Sie dann der SSIS-Task SQL ausführen, um ein Polybase Skript zu starten, das die Daten in SQL Data Warehouse lädt. Diese Option bietet die optimale Leistung der hier aufgeführten drei Optionen. Um den Vorgang Azure Blob hochladen erhalten möchten, laden Sie das [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure][]aus. Weitere Informationen zum Polybase finden Sie unter [PolyBase][].

## <a name="before-you-start"></a>Bevor Sie beginnen

Um dieses Lernprogramm durchgehen, müssen Sie folgende Aktionen ausführen:

1. **SQL Server Integration Services (SSIS)**. SSIS ist eine Komponente von SQL Server und erfordert eine Testversion oder eine lizenzierte Version von SQL Server. Um eine Testversion von SQL Server 2016 Vorschau zu erhalten, finden Sie unter [SQL Server evaluieren möchten][].
2. **Visual Studio**. Wenn Sie die kostenlose Visual Studio 2015 Community Edition erhalten möchten, finden Sie unter [Visual Studio-Community][].
3. **SQL Server Data Tools für Visual Studio (SSDT)**. Wenn SQL Server Data Tools für Visual Studio 2015 erhalten möchten, finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)][].
4. **Beispieldaten**. In diesem Lernprogramm verwendet Beispieldaten, die als Quelldaten in SQL Server in der Datenbank AdventureWorks gespeicherten in SQL Data Warehouse geladen werden. Wenn die Datenbank AdventureWorks erhalten möchten, finden Sie unter [AdventureWorks 2014 Stichprobe Datenbanken][].
5. **A SQL Data Warehouse-Datenbank und Berechtigungen**. In diesem Lernprogramm stellt eine Verbindung mit einer Instanz von SQL Data Warehouse und Daten in diese lädt. Sie müssen Berechtigungen zum Erstellen einer Tabelle und zum Laden von Daten verfügen.
6. **Eine Firewall-Regel**. Sie müssen eine Firewall-Regel auf SQL Data Warehouse mit der IP-Adresse des lokalen Computers erstellen, bevor Sie Daten in SQL Data Warehouse hochladen können.

## <a name="step-1-create-a-new-integration-services-project"></a>Schritt 1: Erstellen Sie ein neues Integration Services-Projekt

1. Starten Sie Visual Studio 2015.
2. Wählen Sie im Menü **Datei** **neu | Project**.
3. Navigieren Sie zu der **installiert | Vorlagen | Business Intelligence | Integrationsservices** Projekttypen.
4. Wählen Sie **Integration Services-Projekt**aus. Geben Sie Werte für die **Namen** und **einen Speicherort**aus, und wählen Sie dann auf **OK**.

Visual Studio wird geöffnet und erstellt ein neues Integration Services (SSIS) Projekt. Öffnet Visual Studio den Designer für die einzelnen neuen SSIS-Paket (Package.dtsx) im Projekt. Sie finden Sie im folgenden Bildschirm Bereiche:

- Klicken Sie auf der linken Seite der **Toolbox** der SSIS-Komponenten.
- In der Mitte der Entwurfsoberfläche, mit mehreren Registerkarten. Sie verwenden in der Regel mindestens die **Steuerung** und den **Datenfluss** Registerkarten.
- Klicken Sie auf der rechten Seite, die **Lösung Explorer** und die Bereiche **Eigenschaften** .

    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>Schritt 2: Erstellen von einfachen Datenfluss

1. Ziehen Sie eine Aufgabe mit Daten Datenfluss aus der Toolbox in die Mitte der Entwurfsoberfläche (auf der Registerkarte **Ablaufsteuerung** ) ein.

    ![][02]

2. Doppelklicken Sie auf die Daten Datenfluss Aufgabe wechseln Sie zur Registerkarte Datenfluss.
3. Ziehen Sie aus der Liste der anderen Quellen in der Toolbox einer Quelle ADO.NET auf die Entwurfsoberfläche. Mit der Quelle Netzwerkadapter weiterhin ausgewählt ist ändern Sie deren Namen mit **SQL Server-Datenquelle** im Bereich **Eigenschaften** an.
4. Ziehen Sie ein ADO.NET Ziel aus der Liste andere Ziele in der Toolbox auf die Entwurfsoberfläche unter der Quelle ADO.NET. Mit dem Ziel Netzwerkadapter weiterhin ausgewählt ist ändern Sie deren Namen in **SQL DW Ziel** im Bereich **Eigenschaften** ein.

    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>Schritt 3: Konfigurieren der Netzwerkadapter Quelle

1. Doppelklicken Sie auf die Quelle Netzwerkadapter, um den **ADO.NET Quelleditor**zu öffnen.

    ![][03]

2. Klicken Sie auf der Registerkarte **Verbindungs-Managers** des **ADO.NET Quelleditor**auf die Schaltfläche " **neu** " neben der Liste **ADO.NET Verbindungs-Managers** zum Öffnen des Dialogfelds **ADO.NET Verbindungs-Managers konfigurieren** und erstellen die Verbindungseinstellungen für die SQL Server-Datenbank aus, die in diesem Lernprogramm Daten geladen.

    ![][04]

3. Klicken Sie im Dialogfeld **Konfigurieren ADO.NET Verbindungs-Managers** klicken Sie auf die Schaltfläche " **neu** " zum Öffnen des Dialogfelds **Verbindungs-Managers** und erstellen eine Verbindung mit neuen Daten.

    ![][05]

4. Führen Sie die folgenden Elemente im Dialogfeld **Verbindungs-Manager** .

    1. Wählen Sie für **Anbieter**die SqlClient-Datenanbieter aus.
    2. Geben Sie für **Servername angezeigt**den SQL Server-Namen ein.
    3. Klicken Sie im Abschnitt **Melden Sie sich bei dem Server** wählen Sie aus, oder geben Sie Authentifizierungsinformationen.
    4. Wählen Sie im Abschnitt **mit Datenbank verbinden** der Beispieldatenbank AdventureWorks aus.
    5. Klicken Sie auf **Verbindung testen**.
    
        ![][06]
    
    6. Klicken Sie im Dialogfeld, das die Verbindung Testergebnisse Berichten, klicken Sie auf **OK** , um das Dialogfeld **Verbindungs-Managers** zurückzukehren.
    7. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurieren ADO.NET Verbindungs-Managers** zurückzukehren, klicken Sie im Dialogfeld **Verbindungs-Managers** .
 
5. Klicken Sie auf **OK** , um zum **ADO.NET Quelleditor**zurückzukehren, klicken Sie im Dialogfeld **Konfigurieren ADO.NET Verbindungs-Manager** .
6. Wählen Sie in der **ADO.NET Quelleditor**, in der Liste **Name der Tabelle oder die Ansicht** **Sales.SalesOrderDetail** Tabelle ein.

    ![][07]

7. Klicken Sie auf **Vorschau** , um die ersten 200 Zeilen mit Daten in der Quelltabelle im Dialogfeld **Vorschau der Abfrageergebnisse** angezeigt.

    ![][08]

8. Klicken Sie auf **Schließen** , um zu der **ADO.NET Quelleditor**zurückzukehren, klicken Sie im Dialogfeld **Vorschau der Abfrageergebnisse** .
9. Klicken Sie im **Quelleditor ADO.NET**auf **OK** , um die Konfiguration der Datenquelle abzuschließen.

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>Schritt 4: Die Quelle Netzwerkadapter Herstellen einer Verbindung mit dem Ziel Netzwerkadapter

1. Wählen Sie aus der Quelle Netzwerkadapter auf der Entwurfsoberfläche.
2. Wählen Sie den blauen Pfeil, der aus der Quelle Netzwerkadapter erweitert, und ziehen Sie es an die Ziel-Editor, bis sie an andockt.

    ![][10]

    In ein normales SSIS-Paket verwenden Sie eine Reihe von anderen Komponenten aus der SSIS-Toolbox zwischen der Quelle und das Ziel umstrukturieren, Transformieren und bereinigen Sie Ihre Daten beim passieren Datenfluss SSIS umfasst. Um dieses Beispiel möglichst einfach zu halten, wir die Quelle direkt an das Ziel eine Verbindung herstellen.

## <a name="step-5-configure-the-destination-adapter"></a>Schritt 5: Konfigurieren der Netzwerkadapter Ziel

1. Doppelklicken Sie auf den Netzwerkadapter Ziel, um die **Ziel-Editor für ADO.NET**zu öffnen.

    ![][11]

2. Klicken Sie auf der Registerkarte **Verbindungs-Managers** des **ADO.NET Ziel-Editor**auf die **neue** Schaltfläche neben der Liste **Verbindungs-Managers** zum Öffnen des Dialogfelds **ADO.NET Verbindungs-Managers konfigurieren** und Verbindungseinstellungen für die Azure SQL-Data Warehouse-Datenbank, in der in diesem Lernprogramm Laden der Daten, erstellen.
3. Klicken Sie im Dialogfeld **Konfigurieren ADO.NET Verbindungs-Managers** klicken Sie auf die Schaltfläche " **neu** " zum Öffnen des Dialogfelds **Verbindungs-Managers** und erstellen eine Verbindung mit neuen Daten.
4. Führen Sie die folgenden Elemente im Dialogfeld **Verbindungs-Manager** .
    1. Wählen Sie für **Anbieter**die SqlClient-Datenanbieter aus.
    2. Geben Sie unter **Servername**den Namen der SQL Data Warehouse.
    3. **Melden Sie sich an den Server** im Abschnitt wählen Sie **SQL Server-Authentifizierung verwenden** aus, und geben Sie Authentifizierungsinformationen.
    4. Wählen Sie im Abschnitt **mit Datenbank verbinden** aus einer vorhandenen SQL Data Warehouse-Datenbank.
    5. Klicken Sie auf **Verbindung testen**.
    6. Klicken Sie im Dialogfeld, das die Verbindung Testergebnisse Berichten, klicken Sie auf **OK** , um das Dialogfeld **Verbindungs-Managers** zurückzukehren.
    7. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurieren ADO.NET Verbindungs-Managers** zurückzukehren, klicken Sie im Dialogfeld **Verbindungs-Managers** .
5. Klicken Sie auf **OK** , um die **Ziel-Editor für ADO.NET**zurückzukehren, klicken Sie im Dialogfeld **Konfigurieren ADO.NET Verbindungs-Manager** .
6. Klicken Sie in der **Ziel-Editor für ADO.NET**neben der Liste **Verwenden einer Tabelle oder Ansicht** So öffnen Sie im Dialogfeld **Tabelle erstellen** , um eine neue Zieltabelle mit einer Spalte zu erstellen, die die Quelltabelle entspricht auf **neu** .

    ![][12a]

7. Führen Sie die folgenden Elemente im Dialogfeld **Tabelle erstellen** .

    1. Ändern Sie den Namen der Zieltabelle **SalesOrderDetail**.
    2. Entfernen Sie die **Rowguid** -Spalte. Der Datentyp **Uniqueidentifier** wird nicht in SQL Data Warehouse unterstützt.
    3. Ändern Sie den Datentyp der Spalte **"LineTotal"** in **Geld**ein. Der **decimal** -Datentyp ist nicht in SQL Data Warehouse unterstützt. Informationen zu unterstützten Datentypen finden Sie unter [CREATE TABLE (Azure SQL-Data Warehouse, Parallel Data Warehouse)][].
    
        ![][12b]
    
    4. Klicken Sie auf **OK** , um die Tabelle erstellen, und kehren Sie zu der **Ziel-Editor für ADO.NET**zurück.

8. Wählen Sie in der **Ziel-Editor für ADO.NET** **Zuordnungen** Registerkarte sehen, wie die Spalten in der Quelle auf Spalten in das Ziel zugeordnet werden.

    ![][13]

9. Klicken Sie auf **OK** , um die Konfiguration der Datenquelle abzuschließen.

## <a name="step-6-run-the-package-to-load-the-data"></a>Schritt 6: Führen Sie das Paket aus, um die Daten zu laden.

Führen Sie das Paket aus, indem Sie auf die Schaltfläche **Start** , klicken Sie auf der Symbolleiste oder, indem Sie eine der Optionen im Menü **Debuggen** **Ausführen** auswählen.

Wie das Paket beginnt, wird Gelb dreht Räder an, dass Aktivität als auch die Anzahl der Zeilen, die bisher verarbeitet.

![][14]

Wenn das Paket ausgeführt wurde, wird grüne Häkchen an, dass Erfolg als auch die Gesamtzahl der Zeilen mit Daten aus der Quelle an das Ziel geladen.

![][15]

Herzlichen Glückwunsch! Sie haben SQL Server Integration Services erfolgreich verwendet, um Daten in Azure SQL-Data Warehouse zu laden.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu den SSIS-Datenfluss. Beginnen Sie hier: [Datenfluss][].
- Erfahren Sie, wie Debuggen und Problembehandlung bei der Pakete rechts in der Design-Umgebung. Beginnen Sie hier: [Tools für die Entwicklung Paket zur Problembehandlung][].
- Erfahren Sie, wie Sie Ihre SSIS-Projekte und Pakete Integration Services-Server oder einen anderen Speicherort bereitstellen. Beginnen Sie hier: [Bereitstellung von Projekten und Pakete][].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[Leitfaden für PolyBase]: https://msdn.microsoft.com/library/mt143171.aspx
[Herunterladen von SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[Erstellen Sie die Tabelle (SQL Azure Datawarehouse, Parallel Datawarehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Datenfluss]: https://msdn.microsoft.com/library/ms140080.aspx
[Problembehandlungstools für die Entwicklung von Paket]: https://msdn.microsoft.com/library/ms137625.aspx
[Bereitstellung von Projekten und Pakete]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services-Feature Pack für Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[Testen der SQL Server]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio-Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Stichprobe Datenbanken]: https://msftdbprodsamples.codeplex.com/releases/view/125550
