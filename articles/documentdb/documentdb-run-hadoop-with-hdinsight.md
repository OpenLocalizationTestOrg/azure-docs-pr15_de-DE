<properties
    pageTitle="Führen Sie die DocumentDB und HDInsight mithilfe des Hadoop | Microsoft Azure"
    description="Erfahren Sie, wie ein, um eine einfache Struktur, MapReduce und Schwein mit DocumentDB und Azure HDInsight auszuführen."
    services="documentdb"
    authors="dennyglee"
    manager="jhubbard"
    editor="mimig"
    documentationCenter=""/>


<tags
    ms.service="documentdb"
    ms.workload="data-services"
    ms.tgt_pltfrm="na"
    ms.devlang="java"
    ms.topic="article"
    ms.date="09/20/2016"
    ms.author="denlee"/>

#<a name="DocumentDB-HDInsight"></a>Führen Sie einen Hadoop Auftrag mithilfe von DocumentDB und HDInsight

In diesem Lernprogramm erfahren Sie, Ausführen von [Apache Struktur][apache-hive], [Apache Schwein][apache-pig], und [Apache Hadoop] [ apache-hadoop] MapReduce Aufträge auf Azure HDInsight mit DocumentDBs Hadoop Verbinder. DocumentDB des Hadoop Verbinder ermöglicht DocumentDB als sowohl Quell-als auch Empfänger für Struktur, Schwein und MapReduce Aufträge fungieren. In diesem Lernprogramm verwendet DocumentDB als die Datenquelle und das Ziel für Hadoop Aufträge.

Am Ende dieses Lernprogramms, erhalten Sie die folgenden Fragen beantworten können:

- Wie lade ich Daten aus DocumentDB mithilfe einer Struktur, Schwein oder MapReduce Projekt?
- Wie speichere ich Daten in DocumentDB mithilfe einer Struktur, Schwein oder MapReduce Projekt?

Es empfiehlt sich, erste Schritte, durch das folgende Video, wir Ausführungsort durch eine Struktur Auftrag mithilfe von DocumentDB und HDInsight beobachten.

> [AZURE.VIDEO use-azure-documentdb-hadoop-connector-with-azure-hdinsight]

Klicken Sie dann zurück zu diesem Artikel, erhalten Sie die vollständigen Details wie Analytics Aufträge auf Ihre Daten DocumentDB ausgeführt werden kann.

> [AZURE.TIP] In diesem Lernprogramm wird davon ausgegangen, dass Sie die vorherige Erfahrung mit Apache Hadoop, Struktur und/oder Schwein haben. Wenn Sie Apache Hadoop, Struktur und Schwein nicht vertraut sind, wir empfehlen des Besuchs der [Apache Hadoop Dokumentation][apache-hadoop-doc]. In diesem Lernprogramm wird davon ausgegangen, dass Sie vorherige Erfahrung mit DocumentDB und verfügen über ein Konto DocumentDB. Wenn Sie noch neu bei DocumentDB sind, oder Sie verfügen nicht über ein Konto DocumentDB, aktivieren Sie sich unsere [Überfordert] [ getting-started] Seite.

Keine haben Zeit des Lernprogramms abgeschlossen, und nur die vollständige Beispiel PowerShell Skripts für Struktur, Schwein und MapReduce erhalten möchten? Kein Problem, erhalten sie [hier][documentdb-hdinsight-samples]. Der Download enthält auch die Hql Schwein und Java-Dateien für diese Beispiele.

## <a name="NewestVersion"></a>Neueste Version

<table border='1'>
    <tr><th>Hadoop-Connector-Version</th>
        <td>1.2.0</td></tr>
    <tr><th>Skript-Uri</th>
        <td>https://portalcontent.BLOB.Core.Windows.NET/scriptaction/documentdb-Hadoop-Installer-v04.ps1</td></tr>
    <tr><th>Änderungsdatum</th>
        <td>04/26/2016</td></tr>
    <tr><th>Unterstützte HDInsight Versionen</th>
        <td>3.1, 3,2</td></tr>
    <tr><th>Änderungsprotokoll</th>
        <td>Aktualisierte DocumentDB Java SDK zu 1.6.0</br>
            Hinzugefügte Unterstützung für partitionierte Websitesammlungen als Quelle und Empfänger</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Erforderliche Komponenten
Bevor Sie den Anweisungen in diesem Lernprogramm folgen, stellen Sie sicher, dass Sie über Folgendes verfügen:

- Ein Konto DocumentDB, einer Datenbank und einer Websitesammlung mit Dokumenten in. Weitere Informationen finden Sie unter [Erste Schritte mit DocumentDB][getting-started]. Importieren von Beispieldaten in Ihr Konto DocumentDB mit den [DocumentDB importieren Tool][documentdb-import-data].
- Durchsatz. Liest und schreibt aus HDInsight in Richtung der vorgesehenen Anforderung Einheiten für Ihre Websitesammlungen gezählt werden sollen. Weitere Informationen finden Sie unter [Durchsatz bereitgestellt, die Anfrage Einheiten, und Datenbankvorgänge][documentdb-manage-throughput].
- Kapazität für eine weitere gespeicherte Prozedur innerhalb jeder ausgeben Websitesammlung. Gespeicherten Prozeduren werden für die Übertragung von resultierenden Dokumente verwendet. Weitere Informationen finden Sie unter [Websitesammlungen und bereitgestellte Durchsatz][documentdb-manage-document-storage].
- Kapazität für die resultierende Dokumente aus der Struktur, Schwein oder MapReduce Aufträge. Weitere Informationen finden Sie unter [Verwalten von DocumentDB Kapazität und Leistung][documentdb-manage-collections].
- [*Optional*] Kapazität für eine zusätzliche Auflistung. Weitere Informationen finden Sie unter [Speicherung von Dokumenten bereitgestellt und Aufwand Index][documentdb-manage-document-storage].

> [AZURE.WARNING] Um die Erstellung einer neuen Auflistung während einer der Einzelvorgänge zu vermeiden, können Sie entweder Ergebnisse zu Stdout drucken, speichern Sie die Ausgabe an Ihre WASB Container oder eine bereits vorhandene Sammlung angeben. Angeben einer vorhandenen Websitesammlungs an, neue Dokumente in der Auflistung erstellt werden und bereits vorhandenen Dokumente werden nur betroffen, wenn ein Konflikt *IDs*vorliegt. **Der Verbinder die vorhandenen Dokumente mit Id Konflikte automatisch überschrieben**. Sie können dieses Feature deaktivieren, indem Sie die Option Upsert auf "falsch" festlegen. Wenn Upsert falsch ist und ein Konflikt auftritt, tritt ein Fehler der Auftrag Hadoop; ein Id-Konflikt-Fehler ausgegeben.


## <a name="ProvisionHDInsight"></a>Schritt 1: Erstellen eines neuen HDInsight Clusters
In diesem Lernprogramm wird mit Skriptaktion aus dem Portal Azure HDInsight Cluster angepasst. In diesem Lernprogramm werden wir Azure-Portal verwenden, um Ihren Cluster HDInsight zu erstellen. Anweisungen zum Verwenden von PowerShell-Cmdlets oder HDInsight .NET SDK Auschecken [Anpassen HDInsight Cluster mithilfe der Aktion Skript] [ hdinsight-custom-provision] Artikel.

1. Melden Sie sich bei der [Azure-Portal][azure-portal].

2. Klicken Sie auf **+ neue** am oberen Rand der linken Navigationsbereich, Suchen nach **HDInsight** in der oberen Suchleiste auf das neue Blade.

3. **HDInsight** von **Microsoft** veröffentlicht wird am oberen Rand der Ergebnisse angezeigt. Klicken Sie darauf, und klicken Sie dann auf **Erstellen**.

4. Klicken Sie auf den neuen HDInsight Cluster erstellen Sie Blade, geben Sie Ihren **Clusternamen** ein, und wählen Sie das **Abonnement** Sie diese Ressource unter bereitstellen möchten.

    <table border='1'>
        <tr><td>Clustername</td><td>Name der Cluster.<br/>
   Most des DNS-Namens beginnen und enden mit einer alphanumerische Zeichen enthalten möglicherweise Striche.<br/>
   Das Feld muss eine Zeichenfolge zwischen 3 und 63 Zeichen lang sein.</td></tr>
        <tr><td>Namen des Abonnements.</td>
            <td>Wenn Sie mehrere Azure-Abonnement verfügen, wählen Sie das Abonnement, das Ihre HDInsight Cluster gehostet wird. </td></tr>
    </table>

5. Klicken Sie auf **Clustertyp auswählen** , und legen Sie die folgenden Eigenschaften auf die angegebenen Werte.

    <table border='1'>
        <tr><td>Clustertyp</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Cluster Ebene</td><td><strong>Standard</strong></td></tr>
        <tr><td>Betriebssystem</td><td><strong>Windows</strong></td></tr>
        <tr><td>Version</td><td>neueste version</td></tr>
    </table>

    Klicken Sie nun auf **auswählen**.

    ![Bereitstellen von Hadoop HDInsight initial Cluster-details][image-customprovision-page1]

6. Klicken Sie auf **Anmeldeinformationen** ein, legen Sie Ihren Benutzernamen und die Anmeldeinformationen für den remote-Zugriff. Wählen Sie Ihren **Cluster Login Benutzernamen** und Ihr **Kennwort Cluster**aus.

    Wenn Sie remote in Ihren Cluster möchten, wählen Sie *Ja* am unteren Rand der Blade, und geben Sie einen Benutzernamen und ein Kennwort.

7. Klicken Sie auf **Datenquelle** gewohnten Standort befinden für den Zugriff auf Daten festlegen. Wählen Sie die **Markierung Methode** und geben Sie ein bereits vorhandenen Speicherkonto oder erstellen Sie einen neuen.

8. Geben Sie in der gleichen Blade eines **Containers Standard** und einen **Speicherort**aus. Und klicken Sie auf **auswählen**.

    > [AZURE.NOTE] Wählen Sie eine Stelle in der Nähe der DocumentDB Konto Region für eine bessere Leistung

8. Klicken Sie auf **Preise** , um die Anzahl und Typ der Knoten auszuwählen. Sie können die standardmäßige Konfiguration beibehalten und die Anzahl der Worker Knoten höher skalieren.

9. Klicken Sie auf **optionale Konfiguration**, und klicken Sie dann auf **Skript-Aktionen** in das optionale Konfiguration Blade.

    Geben Sie die folgende Informationen zum Anpassen Ihrer HDInsight Clusters Skript-Aktionen.

    <table border='1'>
        <tr><th>Eigenschaft</th><th>Wert</th></tr>
        <tr><td>Namen</td>
            <td>Geben Sie einen Namen für die Skriptaktion ein.</td></tr>
        <tr><td>URI-Skript</td>
            <td>Geben Sie den URI an das Skript, das zum Anpassen des Clusters aufgerufen wird.</br></br>
   Geben Sie ein: </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
        <tr><td>Kopf</td>
            <td>Klicken Sie auf das Kontrollkästchen, um das PowerShell-Skript auf dem Kopf Knoten auszuführen.</br></br>
            <strong>Aktivieren Sie dieses Kontrollkästchen</strong>.</td></tr>
        <tr><td>Worker</td>
            <td>Klicken Sie auf das Kontrollkästchen, um das PowerShell-Skript auf dem Worker-Knoten auszuführen.</br></br>
            <strong>Aktivieren Sie dieses Kontrollkästchen</strong>.</td></tr>
        <tr><td>Zookeeper</td>
            <td>Klicken Sie auf das Kontrollkästchen, um das PowerShell-Skript auf die Zookeeper auszuführen.</br></br>
            <strong>Nicht erforderlich</strong>.
            </td></tr>
        <tr><td>Parameter</td>
            <td>Geben Sie den Parameter aus, wenn das Skript erforderlich.</br></br>
            <strong>Keine Parameter erforderlich</strong>.</td></tr>
    </table>

10. Erstellen einer neuen **Ressourcengruppe** oder verwenden Sie eine vorhandene Ressourcengruppe unter Ihrem Abonnement Azure.

11. Prüfen Sie jetzt **Pin zum Dashboard** , um ihre Bereitstellung nachverfolgen, und klicken Sie auf **Erstellen**!

## <a name="InstallCmdlets"></a>Schritt 2: Installieren und Konfigurieren von Azure PowerShell

1. Installieren der Azure PowerShell. Anweisungen finden Sie [hier][powershell-install-configure].

    > [AZURE.NOTE] Alternativ können Sie nur für Struktur Abfragen, die Struktur HDInsights online-Editor verwenden. Dazu melden Sie sich bei der [Azure-Portal][azure-portal], klicken Sie im linken Bereich zum Anzeigen einer Liste der Cluster HDInsight auf **HDInsight** . Klicken Sie auf die Cluster Struktur Abfragen ausgeführt werden soll, und klicken Sie dann auf **Abfrage-Verwaltungskonsole**.

2. Öffnen Sie die integrierten Skriptingtools Azure PowerShell-Umgebung
    - Klicken Sie auf einem Computer unter Windows 8 oder WindowsServer 2012 oder höher können Sie die integrierte Suche verwenden. Vom Startbildschirm Geben Sie **Powershell Ise** , und klicken Sie auf die **EINGABETASTE**.
    - Verwenden Sie das Startmenü auf einem Computer mit einer Version vor Windows 8 oder Windows Server 2012. Über das Startmenü **Eingabeaufforderungsfenster** Geben Sie im Suchfeld, und klicken Sie dann in der Ergebnisliste, klicken Sie auf **Eingabeaufforderung**. Geben Sie in der Befehlszeile **Powershell_ise** , und klicken Sie auf die **EINGABETASTE**.

3. Fügen Sie Ihrem Azure-Konto hinzu.
    1. Im Bereich Konsole **Hinzufügen-AzureAccount** Geben Sie ein, und klicken Sie auf die **EINGABETASTE**.
    2. Geben Sie die e-Mail-Adresse, die mit Ihrem Azure-Abonnement verknüpft ist, und klicken Sie auf **Weiter**.
    3. Geben Sie das Kennwort für Ihr Abonnement Azure ein.
    4. Klicken Sie auf **Anmelden**.

4. Das folgende Diagramm zeigt die wichtigen Teile der Deaktivierung des Azure PowerShell-Umgebung.

    ![Diagramm für Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Schritt 3: Führen Sie die Struktur des DocumentDB und HDInsight verwenden

> [AZURE.IMPORTANT] Verwenden der Einstellungen für die Konfiguration müssen alle Variablen < > erkennbar ausgefüllt werden.

1. Legen Sie die folgenden Variablen in Ihrem PowerShell-Skript-Fenster an.

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"

2. <p>Lassen Sie uns beginnen Sie mit die Abfragezeichenfolge bauen. Schreiben wir eine Struktur-Abfrage, die alle Dokumente System generiert werden (_ts) erfordert eindeutige Ids (_rid) aus einer Sammlung DocumentDB aber alle Dokumente hält, indem Sie die Minute und anschließend speichert die Ergebnisse in eine neue DocumentDB Websitesammlung zurück.</p>

    <p>Zunächst erstellen wir eine strukturtabelle Sammlung von DocumentDB. Fügen Sie den folgenden Codeausschnitt in der PowerShell-Skript Bereich <strong>nach</strong> der Codeausschnitt aus #1. Sicherstellen, dass Sie optionalen DocumentDB.query Parameter t Glätten unsere Dokumente, nur _ts aufnehmen und _rid.</p>

    > [AZURE.NOTE]**DocumentDB.inputCollections benennen wurde keinen Fehler.** Ja, können wir auf mehrere Websitesammlungen als Eingabe hinzufügen: </br>

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.


        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

3.  Als Nächstes erstellen wir eine strukturtabelle für die Ausgabesammlung. Die Ausgabe Dokumenteigenschaften werden den Monat, Tag, Stunde, Minute und die Gesamtzahl der vorkommen.

    > [AZURE.NOTE]**Noch erneut DocumentDB.outputCollections benennen wurde keinen Fehler.** Ja, können wir auf mehrere Websitesammlungen als Ausgabe hinzufügen: </br>
'*DocumentDB.outputCollections*'='*\<DocumentDB Ausgabe Websitesammlung Namen 1\>*,*\<DocumentDB Ausgabe Websitesammlung Name 2\>*' </br> Die Namen der Websitesammlung sind ohne Leerzeichen, verwenden nur ein einzelnes Komma getrennt. </br></br>
Dokumente werden verteilte Round-Robert über mehrere Websitesammlungen. Eine Reihe von Dokumenten in einer Websitesammlung gespeichert werden, und klicken Sie dann ein zweiter Stapel von Dokumenten in der nächsten Collection usw. gespeichert werden.

        # Create a Hive table for the output data to DocumentDB.
        $queryStringPart2 = "drop table DocumentDB_analytics; " +
                              "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                              "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                              "tblproperties ( " +
                                  "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                  "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                  "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                  "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "

4. Schließlich lassen Sie uns die Dokumente nach Monat, Tag, Stunde und Minute berechnen und fügen Sie die Ergebnisse wieder in die Ausgabe der strukturtabelle.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "

5. Fügen Sie den folgenden Codeausschnitt um eine Struktur Auftragsdefinition aus der vorherigen Abfrage zu erstellen.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    Sie können auch die - Datei wechseln zu eine Skriptdatei HiveQL auf HDFS angeben.

6. Fügen Sie den folgenden Codeausschnitt zum Speichern der Startzeit und den Auftrag Struktur hinzu.

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition

7. Fügen Sie die folgenden warten, bis die Struktur Auftrag abgeschlossen.

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600

8. Fügen Sie vor, um die Ausgabe der Standardansicht und die Start- und Endzeiten drucken.

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green

9. **Führen Sie** neuen Skripts! **Klicken Sie auf** die Schaltfläche grünen ausführen.

10. Überprüfen Sie die Ergebnisse an. Melden Sie sich bei der [Azure-Portal][azure-portal].
    1. Klicken Sie im linken Bereich auf <strong>Durchsuchen</strong> . </br>
    2. Klicken Sie auf <strong>Alles</strong> in der oberen rechten Rand des Bedienfelds durchsuchen. </br>
    3. Suchen nach, und klicken Sie auf <strong>Konten DocumentDB</strong>. </br>
    4. Suchen Sie als Nächstes Ihr <strong>Konto DocumentDB</strong>, und klicken Sie dann in Ihrer Abfrage Struktur angegebenen Ausgabe Auflistung <strong>DocumentDB Datenbank</strong> und Ihrer <strong>Websitesammlung DocumentDB</strong> zugeordnet.</br>
    5. Klicken Sie abschließend auf <strong>Document Explorer</strong> unter <strong>Entwicklertools</strong>.</br></p>

    Sie sehen die Ergebnisse der Abfrage Struktur.

    ![Struktur von Abfrageergebnissen][image-hive-query-results]

## <a name="RunPig"></a>Schritt 4: Ausführen ein Schwein Auftrags mithilfe von DocumentDB und HDInsight

> [AZURE.IMPORTANT] Verwenden der Einstellungen für die Konfiguration müssen alle Variablen < > erkennbar ausgefüllt werden.

1. Legen Sie die folgenden Variablen in der PowerShell-Skript-Bereich ein.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"

2. <p>Lassen Sie uns beginnen Sie mit die Abfragezeichenfolge bauen. Schreiben wir eine Schwein-Abfrage, die alle Dokumente System generiert werden (_ts) erfordert eindeutige Ids (_rid) aus einer Sammlung DocumentDB aber alle Dokumente hält, indem Sie die Minute und anschließend speichert die Ergebnisse in eine neue DocumentDB Websitesammlung zurück.</p>
    <p>Laden Sie Dokumente zuerst von DocumentDB in HDInsight. Fügen Sie den folgenden Codeausschnitt in der PowerShell-Skript Bereich <strong>nach</strong> der Codeausschnitt aus #1. Vergewissern Sie sich zum Hinzufügen einer Abfrage DocumentDB an den optional DocumentDB Abfrageparameter kürzen unsere Dokumente, nur _ts und _rid.</p>

    > [AZURE.NOTE]Ja, können wir auf mehrere Websitesammlungen als Eingabe hinzufügen: </br>
'*\<DocumentDB Eingabe Websitesammlung Namen 1\>*,*\<DocumentDB Eingabe Websitesammlung Name 2\>*'</br> Die Namen der Websitesammlung sind ohne Leerzeichen, verwenden nur ein einzelnes Komma getrennt. </b>

    Dokumente werden verteilte Round-Robert über mehrere Websitesammlungen. Eine Reihe von Dokumenten in einer Websitesammlung gespeichert werden, und klicken Sie dann ein zweiter Stapel von Dokumenten in der nächsten Collection usw. gespeichert werden.

        # Load data from DocumentDB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

3.  Als Nächstes berechnen wir die Dokumente nach Monat, Tag, Stunde, Minute und die Gesamtzahl der vorkommen.

        # GROUP BY minute and COUNT entries for each.
        $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                            "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                            "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "

4. Schließlich wir die Ergebnisse unserer neuen Ausgabe Auflistung speichern.

    > [AZURE.NOTE]Ja, können wir auf mehrere Websitesammlungen als Ausgabe hinzufügen: </br>
'\<DocumentDB Ausgabe Websitesammlung Namen 1\>,\<DocumentDB Ausgabe Websitesammlung Name 2\>'</br> Die Namen der Websitesammlung sind ohne Leerzeichen, verwenden nur ein einzelnes Komma getrennt.</br>
Dokumente werden verteilte Round-Robert über mehrere Sammlungen. Eine Reihe von Dokumenten in einer Websitesammlung gespeichert werden, und klicken Sie dann ein zweiter Stapel von Dokumenten in die nächste Collection usw. gespeichert werden.

        # Store output data to DocumentDB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "

5. Fügen Sie den folgenden Codeausschnitt um Schwein Auftragsdefinition aus der vorherigen Abfrage zu erstellen.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    Sie können auch die - Datei wechseln zu eine Skriptdatei Schwein auf HDFS angeben.

6. Fügen Sie den folgenden Codeausschnitt zum Speichern der Startzeit und den Auftrag Schwein hinzu.

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition

7. Fügen Sie den folgenden warten, für das Projekt Schwein ausführen.

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600

8. Fügen Sie vor, um die Ausgabe der Standardansicht und die Start- und Endzeiten drucken.

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green

9. **Führen Sie** neuen Skripts! **Klicken Sie auf** die Schaltfläche grünen ausführen.

10. Überprüfen Sie die Ergebnisse an. Melden Sie sich bei der [Azure-Portal][azure-portal].
    1. Klicken Sie im linken Bereich auf <strong>Durchsuchen</strong> . </br>
    2. Klicken Sie auf <strong>Alles</strong> in der oberen rechten Rand des Bedienfelds durchsuchen. </br>
    3. Suchen Sie, und klicken Sie auf <strong>DocumentDB-Konten</strong>. </br>
    4. Suchen Sie als Nächstes Ihr <strong>Konto DocumentDB</strong>, und klicken Sie dann in Ihrer Abfrage Schwein angegebenen Ausgabe Auflistung <strong>DocumentDB Datenbank</strong> und Ihrer <strong>Websitesammlung DocumentDB</strong> zugeordnet.</br>
    5. Klicken Sie abschließend auf <strong>Document Explorer</strong> unter <strong>Entwicklertools</strong>.</br></p>

    Die Ergebnisse der Abfrage Schwein wird angezeigt.

    ![Schwein Abfrageergebnisse][image-pig-query-results]

## <a name="RunMapReduce"></a>Schritt 5: Führen Sie die DocumentDB und HDInsight mithilfe des MapReduce

1. Legen Sie die folgenden Variablen in Ihrem PowerShell-Skript-Fenster an.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name

2. Wir werden einen MapReduce-Auftrag ausführen, der die Anzahl von Vorkommen für jedes Dokumenteigenschaft aus der Sammlung DocumentDB ermittelt. Fügen Sie dieses Skript Codeausschnitt **nach** Codeausschnitt oben.

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

    > [AZURE.NOTE] Im Lieferumfang von TallyProperties-v01.jar ist der benutzerdefinierten Installations des Verbinders Hadoop DocumentDB.

3. Fügen Sie den folgenden Befehl aus, und übermitteln Sie den Auftrag MapReduce hinzu.

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Über die Definition der MapReduce müssen Sie auch den HDInsight Cluster-Namen, die den Auftrag MapReduce und die Anmeldeinformationen ausgeführt werden soll. Der Start-AzureHDInsightJob ist eine asynchrone Anruf. Um die Fertigstellung des Projekts zu überprüfen, verwenden Sie das Cmdlet *AzureHDInsightJob warten* .

4. Fügen Sie den folgenden Befehl zum Überprüfen von Fehlern beim Ausführen des MapReduce Auftrags hinzu.

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green

5. **Führen Sie** neuen Skripts! **Klicken Sie auf** die Schaltfläche grünen ausführen.

6. Überprüfen Sie die Ergebnisse an. Melden Sie sich bei der [Azure-Portal][azure-portal].
    1. Klicken Sie im linken Bereich auf <strong>Durchsuchen</strong> .
    2. Klicken Sie auf <strong>Alles</strong> in der oberen rechten Rand des Bedienfelds durchsuchen.
    3. Suchen nach, und klicken Sie auf <strong>Konten DocumentDB</strong>.
    4. Suchen Sie als Nächstes Ihr <strong>Konto DocumentDB</strong>, und klicken Sie dann in Ihrem Auftrag MapReduce angegebenen Ausgabe Auflistung <strong>DocumentDB Datenbank</strong> und Ihrer <strong>Websitesammlung DocumentDB</strong> zugeordnet.
    5. Klicken Sie abschließend auf <strong>Document Explorer</strong> unter <strong>Entwicklertools</strong>.

    Sehen Sie die Ergebnisse Ihrer MapReduce Aufgaben an.

    ![MapReduce Abfrageergebnisse][image-mapreduce-query-results]

## <a name="NextSteps"></a>Nächste Schritte

Herzlichen Glückwunsch! Sie ist nur der ersten Struktur, Schwein und MapReduce Aufträge mit Azure DocumentDB und HDInsight.

Wir haben öffnen die Quelle ist unsere Hadoop Verbinder. Wenn Sie interessiert sind, können Sie auf [GitHub]mitwirken[documentdb-github].

Weitere Informationen finden Sie unter den folgenden Artikeln:

- [Entwickeln einer Java-Anwendungs mit Documentdb][documentdb-java-application]
- [Entwickeln Sie MapReduce Java-Programme für Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]
- [Erste Schritte mit Hadoop mit Struktur in HDInsight zum Analysieren von mobilen Telefonhörer verwenden][hdinsight-get-started]
- [Verwenden von MapReduce mit HDInsight][hdinsight-use-mapreduce]
- [Verwenden Sie die Struktur mit HDInsight][hdinsight-use-hive]
- [Schwein mit HDInsight verwenden][hdinsight-use-pig]
- [Anpassen von HDInsight Cluster mithilfe der Aktion Skript][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/documentdb-run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[documentdb-hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[documentdb-github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[documentdb-manage-collections]: documentdb-manage.md#Collections
[documentdb-manage-document-storage]: documentdb-manage.md#IndexOverhead
[documentdb-manage-throughput]: documentdb-manage.md#ProvThroughput
[documentdb-import-data]: documentdb-import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md#powershell
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/documentdb-run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/documentdb-run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/documentdb-run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/documentdb-run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: ../powershell-install-configure.md
