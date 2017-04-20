<properties
   pageTitle="Verwenden Sie Hadoop Schwein mit SSH in einem Cluster HDInsight | Microsoft Azure"
   description="Hier erfahren Sie, wie eine Verbindung zu einem Hadoop Linux-basierten Cluster mit SSH, und klicken Sie dann mit dem Befehl Schwein Schwein Lateinisch Anweisungen interaktiv ausgeführt, oder als Stapelverarbeitungsauftrag her."
   services="hdinsight"
   documentationCenter=""
   authors="Blackmist"
   manager="jhubbard"
   editor="cgronlun"
    tags="azure-portal"/>

<tags
   ms.service="hdinsight"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="big-data"
   ms.date="10/11/2016"
   ms.author="larryfr"/>

#<a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a>Führen Sie Schwein Aufträge auf einem Linux-basierten Cluster mit dem Befehl Schwein (SSH)

[AZURE.INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

In diesem Dokument werden Sie durch den Prozess des Herstellens einer Verbindung zu einem Cluster Linux-basierten Azure HDInsight mithilfe von Secure Shell (SSH), klicken Sie dann mit dem Befehl Schwein Schwein Lateinisch Anweisungen interaktiv auszuführen oder als Stapelverarbeitungsauftrag geführt.

Die Programmiersprache Schwein Lateinisch können Sie Transformationen beschreiben, die mit den Eingabedaten für die gewünschte Ausgabe angewendet werden.

> [AZURE.NOTE] Wenn Sie bereits bei der Verwendung von Hadoop Linux-basierten Server vertraut sind, aber es neu in HDInsight sind, finden Sie unter [Linux-basierten HDInsight Tipps](hdinsight-hadoop-linux-information.md).

##<a id="prereq"></a>Erforderliche Komponenten

Um die Schritte in diesem Artikel ausführen zu können, benötigen Sie Folgendes.

* Ein Cluster Linux-basierten HDInsight (Hadoop auf HDInsight).

* SSH-Client. Linux, Unix und Mac OS sollte mit einem SSH-Client stammen. Windows-Benutzer müssen einen Client wie [kitten](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)heruntergeladen werden.

##<a id="ssh"></a>Kontaktaufnahme mit SSH

Verbinden Sie mit den vollqualifizierten Domänennamen (FQDN) des Clusters HDInsight mithilfe des Befehls SSH. Wird der FQDN dem Namen, klicken Sie dann den Cluster zugewiesen werden **. azurehdinsight.net**. Beispielsweise würde die folgenden zu einem Cluster mit dem Namen **Myhdinsight**herstellen.

    ssh admin@myhdinsight-ssh.azurehdinsight.net

**Wenn Sie einen Schlüssel des Zertifikats für die Authentifizierung SSH bereitgestellt** beim Erstellen den HDInsight-Cluster erstellt haben, müssen Sie den Speicherort des privaten Schlüssels auf Ihrem Clientsystem angeben.

    ssh admin@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Sofern Sie ein Kennwort für SSH Authentifizierung** beim Erstellen den HDInsight Cluster erstellt haben, müssen Sie das Kennwort bei einer entsprechenden Aufforderung angeben.

Weitere Informationen zur Verwendung von SSH mit HDInsight finden Sie unter [Use SSH mit Linux-basierten Hadoop auf HDInsight aus Linux, OS X und Unix](hdinsight-hadoop-linux-use-ssh-unix.md).

###<a name="putty-windows-based-clients"></a>Kitten (Windows-basierten Clients)

Windows bietet keine integrierten SSH-Client. Es wird empfohlen, mit **kitten**, die von [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)heruntergeladen werden kann.

Weitere Informationen zur Verwendung von kitten finden Sie unter [Use SSH mit Linux-basierten Hadoop auf HDInsight von Windows ](hdinsight-hadoop-linux-use-ssh-windows.md).

##<a id="pig"></a>Verwenden Sie den Befehl Schwein

2. Nachdem die Verbindung hergestellt ist, starten Sie die Schwein Befehlszeilenschnittstelle (CLI) mithilfe des folgenden Befehls.

        pig

    Nach einem Augenblick sollten Sie sehen einen `grunt>` Aufforderung.

3. Geben Sie die folgende Anweisung aus.

        LOGS = LOAD 'wasbs:///example/data/sample.log';

    Dieser Befehl lädt den Inhalt der Datei sample.log in Protokolle. Sie können den Inhalt der Datei mithilfe des folgenden anzeigen.

        DUMP LOGS;

4. Im nächsten Schritt Transformieren von Daten durch ein regulärer Ausdruck zum Extrahieren von nur der Protokollierungsstufe aus jeder Datensatz mithilfe der folgenden anwenden.

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Sie können **DUMP** verwenden, um die Daten nach der Transformation anzuzeigen. In diesem Fall verwenden `DUMP LEVELS;`.

5. Weiterhin Transformationen mithilfe der folgenden Anweisungen hinzu. Verwenden Sie `DUMP` um das Ergebnis der Transformation nach jedem Schritt anzuzeigen.

    <table>
    <tr>
    <th>Anweisung</th><th>Sinn und Zweck</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = Ebenen von LOGLEVEL FILTER ist nicht null.</td><td>Entfernt Zeilen, die einen null-Wert für die Protokollebene enthalten, und speichert die Ergebnisse in FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = Gruppe FILTEREDLEVELS durch LOGLEVEL;</td><td>Gruppiert die Zeilen durch die Protokollebene und speichert die Ergebnisse in GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENZEN Foreach = GROUPEDLEVELS generieren Gruppe als LOGLEVEL COUNT (FILTEREDLEVELS. LOGLEVEL) wie zählen;</td><td>Erstellt einen neuen Satz jedes eindeutige Protokoll enthaltenen Daten Ebene Wert und wie oft auftritt. Dies ist in FREQUENZEN gespeichert.</td>
    </tr>
    <tr>
    <td>Ergebnis = Reihenfolge FREQUENZEN durch COUNT Desc;</td><td>Ordnet die Protokollierungsgrade nach Anzahl (absteigend) und speichert in Ergebnis.</td>
    </tr>
    </table>

6. Sie können auch die Ergebnisse einer Transformation speichern, mithilfe der `STORE` Anweisung. Beispielsweise die folgenden speichert die `RESULT` in das Verzeichnis **/example/data/pigout** für den Speicher Standardcontainer für den Cluster.

        STORE RESULT into 'wasbs:///example/data/pigout';

    > [AZURE.NOTE] Die Daten werden im angegebenen Verzeichnis in Dateien mit dem Namen **Teil Nnnnn**gespeichert. Wenn das Verzeichnis bereits vorhanden ist, erhalten Sie einen Fehler.

7. Geben Sie die folgende Anweisung, um die schwierige Aufforderung zu beenden.

        QUIT;

###<a name="pig-latin-batch-files"></a>Batchdateien Schwein (Lateinisch)

Sie können auch den Befehl Schwein verwenden, Schwein Lateinisch in einer Datei enthaltenen ausführen.

3. Nach dem Beenden der schwierige Aufforderung, verwenden Sie den folgenden Befehl auf Pipe STDIN in eine Datei namens **pigbatch.pig**. Diese Datei wird in das Basisverzeichnis für das Konto erstellt werden, die Sie für die Sitzung SSH angemeldet sind.

        cat > ~/pigbatch.pig

4. Geben Sie oder fügen Sie die folgenden Zeilen, und klicken Sie dann verwenden Sie STRG + D nach Abschluss des.

        LOGS = LOAD 'wasbs:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

5. Verwenden Sie zum Ausführen der **pigbatch.pig** -Datei mithilfe des Befehls Schwein Folgendes.

        pig ~/pigbatch.pig

    Nachdem die Stapelverarbeitung abgeschlossen ist, sollte die folgende Ausgabe identisch wann Sie verwendet werden sollten angezeigt `DUMP RESULT;` in den vorherigen Schritten.

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

##<a id="summary"></a>Zusammenfassung

Wie Sie sehen können, kann der Befehl Schwein Sie interaktiv ausgeführt, MapReduce mithilfe Schwein Lateinisch sowie Tabellen gespeicherten anweisungenhttp://www.UtterAccess.com/Wiki/Index.PHP/Queries/SQL in einer Batchdatei ausführen.

##<a id="nextsteps"></a>Nächste Schritte

Allgemeine Informationen zu Schwein in HDInsight.

* [Verwenden Sie Schwein mit Hadoop auf HDInsight](hdinsight-use-pig.md)

Sie können Informationen auf andere Weise Hadoop auf HDInsight entwickelt.

* [Verwenden Sie die Struktur mit Hadoop auf HDInsight](hdinsight-use-hive.md)

* [Verwenden Sie MapReduce mit Hadoop auf HDInsight](hdinsight-use-mapreduce.md)
