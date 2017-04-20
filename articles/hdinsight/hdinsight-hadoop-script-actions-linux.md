<properties
    pageTitle="Skripts Aktion Entwicklung mit Linux-basierten HDInsight | Microsoft Azure"
    description="So HDInsight Linux-basierten Cluster mit Skriptaktion anpassen. Skript-Aktionen werden zur Azure HDInsight Cluster anpassen, und geben die Einstellungen der Cluster-Konfiguration oder zusätzliche Dienste, Tools oder andere Software auf dem Cluster installieren. "
    services="hdinsight"
    documentationCenter=""
    authors="Blackmist"
    manager="jhubbard"
    editor="cgronlun"/>

<tags
    ms.service="hdinsight"
    ms.workload="big-data"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/05/2016"
    ms.author="larryfr"/>

# <a name="script-action-development-with-hdinsight"></a>Skript Aktion Entwicklung mit HDInsight

Skript-Aktionen werden zur Azure HDInsight Cluster anpassen, und geben die Einstellungen für Cluster-Konfiguration oder zusätzliche Dienste, Tools oder andere Software auf dem Cluster installieren. Skript-Aktionen können während der Clustererstellung oder auf einem laufenden Cluster.

> [AZURE.NOTE] Die Informationen in diesem Dokument ist für Linux-basierte HDInsight Cluster spezifisch. Informationen zum Verwenden von Skript-Aktionen mit Windows-basierten Cluster finden Sie unter [Skript Aktion Entwicklung mit HDInsight (Windows)](hdinsight-hadoop-script-actions.md).

## <a name="what-are-script-actions"></a>Was sind die Skriptaktionen?

Skript-Aktionen werden Bash Skripts, die auf dem Clusterknoten Azure ausgeführt, Konfiguration ändern oder die Software zu installieren wird. Eine Skriptaktion wird als Stammordner ausgeführt und stellt Vollzugriff für die Cluster-Knoten.

Skript-Aktionen können mithilfe der folgenden Methoden angewendet werden:

| Verwenden Sie diese Option beim Anwenden eines Skripts... | Cluster-während der Erstellung... | Klicken Sie auf einen laufenden Cluster... |
| ----- |:-----:|:-----:|
| Azure-Portal | ✓ | ✓ |
| Azure PowerShell | ✓ | ✓ |
| Azure CLI | &nbsp; | ✓ |
| HDInsight .NET SDK | ✓ | ✓ |
| Azure Ressourcenmanager Vorlage | ✓ | &nbsp; |

Weitere Informationen zur Verwendung dieser Methode Skriptaktionen anwenden, finden Sie unter [Anpassen HDInsight Cluster mit Skript-Aktionen](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Bewährte Methoden für die Skriptentwicklung

Wenn Sie ein benutzerdefiniertes Skript für einen Cluster HDInsight entwickeln, gibt es verschiedene empfohlene Vorgehensweisen beachten müssen:

- [Ziel der Hadoop-version](#bPS1)
- [Adressieren Sie die Version des Betriebssystems](#bps10)
- [Bereitstellen von unveränderliche Links zu Skriptressourcen](#bPS2)
- [Verwenden Sie vordefinierte kompilierte Ressourcen](#bPS4)
- [Sicherstellen Sie, dass das Anpassung Cluster Skript Idempotent ist](#bPS3)
- [Sicherstellen einer hohen Verfügbarkeit der Clusterarchitektur](#bPS5)
- [Konfigurieren Sie die benutzerdefinierten Komponenten um Azure Blob-Speicher zu verwenden.](#bPS6)
- [Informationen zu STDOUT und STDERR schreiben](#bPS7)
- [Speichern von Dateien als ASCII mit LF Zeilenenden](#bps8)
- [Verwenden Sie "Wiederholen" Logik zum Wiederherstellen von vorübergehende Fehler](#bps9)

> [AZURE.IMPORTANT] Skript-Aktionen müssen innerhalb von 60 Minuten durchzuführen, oder sie erklärt werden. Während der Bereitstellung von Knoten das Skript gleichzeitig mit anderen Installation und Konfiguration Prozesse ausgeführt. Induzierten Risikos für Ressourcen wie etwa CPU-Zeit oder Netzwerk Bandbreite kann das Skript zum länger dauern, als in Ihrer Entwicklungsumgebung bedeutet verursachen.

### <a name="bPS1"></a>Ziel der Hadoop-version

Unterschiedliche Versionen von HDInsight müssen unterschiedliche Versionen von installierten Hadoop Dienste und Komponenten. Wenn Ihr Skript eine bestimmte Version von einem Dienst oder einer Komponente erwartet, sollten Sie das Skript nur mit der Version von HDInsight verwenden, die die erforderlichen Komponenten enthält. Informationen auf Komponentenversionen enthaltenen HDInsight finden Sie unter Verwendung des Dokuments [HDInsight Komponente Versioning](hdinsight-component-versioning.md) .

###<a name="bps10"></a>Adressieren Sie die Version des Betriebssystems

HDInsight Linux-basierten basiert auf der Verteilung Ubuntu Linux. Unterschiedliche Versionen von HDInsight basieren auf unterschiedlichen Versionen von Ubuntu, der Effekt möglicherweise Ihr Skript Verhalten. Beispielsweise HDInsight 3,4 und frühere Versionen basieren auf Ubuntu-Versionen, die Upstart verwenden. Version 3.5 basiert auf Ubuntu 16.04, Systemd verwendet. Systemd und Upstart aufsetzen auf unterschiedliche Befehle, damit Ihr Skript für die Arbeit mit beide geschrieben werden sollen.

Ein weiterer wichtiger Unterschied zwischen HDInsight 3 Absatz 4 und 3.5 heißt `JAVA_HOME` jetzt Java 8 verweist.

Sie können mit die Version des Betriebssystems überprüfen `lsb_release`. Die folgenden Codeausschnitte aus dem Farbton installieren Skript veranschaulicht, wie um festzustellen, ob das Skript auf Ubuntu 14 oder 16 ausgeführt wird:

    OS_VERSION=$(lsb_release -sr)
    if [[ $OS_VERSION == 14* ]]; then
        echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
        HUE_TARFILE=hue-binaries-14-04.tgz
    elif [[ $OS_VERSION == 16* ]]; then
        echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
        HUE_TARFILE=hue-binaries-16-04.tgz
    fi
    ...
    if [[ $OS_VERSION == 16* ]]; then
        echo "Using systemd configuration"
        systemctl daemon-reload
        systemctl stop webwasb.service    
        systemctl start webwasb.service
    else
        echo "Using upstart configuration"
        initctl reload-configuration
        stop webwasb
        start webwasb
    fi
    ...
    if [[ $OS_VERSION == 14* ]]; then
        export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
    elif [[ $OS_VERSION == 16* ]]; then
        export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    fi

Sie können das vollständige Skript suchen, das diese Codeausschnitte am https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh enthält.

Die Version von Ubuntu, die von HDInsight verwendet wird, finden Sie im Dokument [HDInsight Komponentenversion](hdinsight-component-versioning.md) .

Die Unterschiede zwischen Systemd und Upstart finden Sie unter [Systemd für Upstart Benutzer](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Bereitstellen von unveränderliche Links zu Ressourcen für Skripts

Stellen Sie sicher, dass die Skripts und vom Skript verwendeten Ressourcen zur Verfügung, während der gesamten Dauer der Cluster bleiben und die Versionen dieser Dateien für die Dauer unverändert bleiben. Diese Ressourcen sind erforderlich, wenn neue Knoten zum Cluster hinzugefügt werden, während der Skalierung Vorgänge.

Die bewährte Methode ist zum Herunterladen und archivieren alles in einem Konto Azure-Speicher für Ihr Abonnement.

> [AZURE.IMPORTANT] Das verwendete Speicherkonto muss im Speicher Standardkonto für Cluster oder einen öffentlichen, schreibgeschützten Container auf einem beliebigen anderen Speicherkonto.

Beispielsweise werden von Microsoft bereitgestellten Beispiele in der [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) Speicher-Konto gespeichert, die einen öffentlichen schreibgeschützten Container durch das Team HDInsight verwaltet wird.

### <a name="bPS4"></a>Verwenden Sie vordefinierte kompilierte Ressourcen

Klicken Sie zum Verringern der Zeit dauert führen Sie das Skript, Vorgänge, die Ressourcen aus dem Quellcode kompilieren zu vermeiden. Stattdessen vorab kompilieren Sie die Ressourcen aus, und speichern Sie die binäre Version in Azure Blob-Speicher, sodass sie schnell zu Cluster aus dem Skript heruntergeladen werden kann.

### <a name="bPS3"></a>Sicherstellen Sie, dass das Anpassung Cluster Skript Idempotent ist

Skripts Idempotent in der sinnvoll sein, die mehrmals ausgeführt, ist das Skript haben entworfen werden müssen, es sollte sicherstellen, dass der Cluster jedes Mal, wenn er ausgeführt wird, auf den gleichen Zustand zurückgegeben wird.

Wenn Sie ein benutzerdefiniertes Skript Anwendung am /usr/local/bin auf Installationen beispielsweise seinem ersten Ausführen und dann bei jeder nachfolgenden Ausführung sollte das Skript überprüfen Sie, ob die Anwendung bereits an der Position /usr/local/bin vorhanden ist, bevor Sie fortfahren mit einer anderen im Skript Schritte.

### <a name="bPS5"></a>Sicherstellen einer hohen Verfügbarkeit der Clusterarchitektur

Linux-basierten HDInsight Cluster bietet zwei am Knoten, die innerhalb der Cluster aktiv sind und Skript sind Aktionen, die für beide Knoten ausgeführt wurde. Wenn die Komponenten, die Sie installieren nur ein am Knoten erwarten, müssen Sie ein Skript entwerfen, die nur die Komponente auf eine der beiden am Knoten im Cluster installiert wird.

> [AZURE.IMPORTANT] Standarddienste als Teil des HDInsight installiert wurden dazu ausgelegt über zwischen den beiden am Knoten fehlschlägt, je nach Bedarf, jedoch dieses Feature nicht auf benutzerdefinierte durch Skript Ctions installierten Komponenten erweitert wird. Wenn Sie über eine Skriptaktion hochgradig verfügbar sein installierten Komponenten benötigen, müssen Sie Ihre eigenen Failovermechanismus implementieren, die die beiden verfügbaren am Knoten verwendet.

### <a name="bPS6"></a>Konfigurieren Sie die benutzerdefinierten Komponenten um Azure Blob-Speicher zu verwenden.

Komponenten, die Sie auf dem Cluster installieren möglicherweise eine Standardkonfiguration, die Speicherung Hadoop Distributed Datei System (HDFS) verwendet. HDInsight verwendet Azure BLOB-Speicher (WASB) als Standardspeicher. Dadurch wird eine HDFS kompatibel Dateisystem, die Daten erhalten bleibt, auch wenn der Cluster gelöscht wird. Konfigurieren Sie Komponenten, die Sie installieren, um WASB anstelle von HDFS verwenden.

Beispielsweise kopiert vor die Giraph examples.jar Datei aus dem lokalen Dateisystem in WASB:

    hadoop fs -copyFromLocal /usr/hdp/current/giraph/giraph-examples.jar /example/jars/

### <a name="bPS7"></a>Informationen zu STDOUT und STDERR schreiben

Informationen zu STDOUT und STDERR während der Ausführung von Skript geschrieben angemeldet ist, und kann mithilfe das Ambari Web-Benutzeroberfläche angezeigt werden.

> [AZURE.NOTE] Ambari stehen nur zur Verfügung, wenn der Cluster erfolgreich erstellt wird. Wenn Sie eine Skriptaktion während der Clustererstellung verwenden und nicht erstellt werden kann, finden Sie unter Problembehandlung Abschnitt [Anpassen HDInsight Cluster mithilfe der Skriptaktion](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) andere Methoden für den Zugriff auf die protokollierten Informationen.

Die meisten Dienstprogramme und Installationspakete schreibt bereits zu STDOUT und STDERR Informationen jedoch möglicherweise zusätzliche Protokollierung hinzufügen möchten. Senden des Textes STDOUT verwenden `echo`. Zum Beispiel:

        echo "Getting ready to install Foo"

Standardmäßig `echo` wird die Zeichenfolge an STDOUT zu senden. Wenn es in STDERR umgeleitet werden sollen, hinzufügen `>&2` vor dem `echo`. Zum Beispiel:

        >&2 echo "An error occurred installing Foo"

Dies leitet an STDOUT (1, die standardmäßigen daher hier nicht aufgeführt ist,) gesendet werden, auf STDERR (2). Weitere Informationen zu e/a-Umleitung finden Sie unter [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Weitere Informationen zum Anzeigen von Skript-Aktionen protokollierten Informationen finden Sie unter [Anpassen HDInsight Cluster mithilfe der Skriptaktion](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

###<a name="bps8"></a>Speichern von Dateien als ASCII mit LF Zeilenenden

Bash Skripts sollten mit Linien durch LF abgeschlossen als ASCII-Format gespeichert werden. Wenn Dateien als UTF-8, z. B. eine Byte Order Mark am Anfang der Datei oder mit Linie Ende von CRLF, das für Windows-Editoren gemeinsam benutzt wird gespeichert sind, wird das Skript mit ähnlich wie der folgende Fehler nicht funktionieren:

    $'\r': command not found
    line 1: #!/usr/bin/env: No such file or directory

###<a name="bps9"></a>Verwenden Sie "Wiederholen" Logik zum Wiederherstellen von vorübergehende Fehler

Beim Herunterladen von Dateien, und Installieren von Paketen mit apt Get oder andere Aktionen, die Daten über das Internet übertragen möglicherweise die Aktion aufgrund einer vorübergehenden Netzwerke Fehler fehl. Beispielsweise kann die remote Ressource, mit dem Sie kommunizieren, gerade einem über zu einer Sicherung Knoten sein.

Wenn Ihr Skript robuste an vorübergehende Fehler vornehmen möchten, können Sie "Wiederholen" Logik implementieren. So sieht ein Beispiel für eine Funktion, die alle darauf übergebenen Befehl ausführen und (wenn der Befehl fehlschlägt,) bis zu drei Mal zu wiederholen. Es werden zwei Sekunden zwischen den einzelnen "Wiederholen" warten.

    #retry
    MAXATTEMPTS=3

    retry() {
        local -r CMD="$@"
        local -i ATTMEPTNUM=1
        local -i RETRYINTERVAL=2

        until $CMD
        do
            if (( ATTMEPTNUM == MAXATTEMPTS ))
            then
                    echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                    return 1
            else
                    echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                    sleep $(( RETRYINTERVAL ))
                    ATTMEPTNUM=$ATTMEPTNUM+1
            fi
        done
    }

Nachfolgend werden Beispiele für die Verwendung dieses (Funktion).

    retry ls -ltr foo

    retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh

## <a name="helpermethods"></a>Helper Methoden für benutzerdefinierte Skripts

Skript Aktion Helper Methoden sind Dienstprogramme, die Sie beim Erstellen von benutzerdefinierten Skripts verwenden können. Diese sind in [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh)definiert und enthalten sein können, in Ihren Skripts mithilfe der folgenden:

    # Import the helper method module.
    wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh

Dadurch wird die folgenden Hilfen in Ihrem Skript zur Verwendung verfügbar:

| Helper Verwendung | Beschreibung |
| ------------ | ----------- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` | Eine Datei aus der Quelle URL auf den Pfad für die angegebene Datei heruntergeladen wird. Standardmäßig wird eine vorhandene Datei nicht überschrieben. |
| `untar_file TARFILE DESTDIR` | Extrahiert eine Tar-Datei (mit `-xf`,) in das Zielverzeichnis. |
| `test_is_headnode` | Wenn auf einem Cluster am Knoten gibt 1; ausgeführt wurde andernfalls 0. |
| `test_is_datanode` | Wenn der aktuelle Knoten ein Datenknoten (Worker) ist, gibt 1 zurück. andernfalls 0. |
| `test_is_first_datanode` | Wenn der aktuelle Knoten der erste (Worker) Datenknoten (mit dem Namen workernode0) ist, gibt 1 zurück. andernfalls 0. |
| `get_headnodes` | Gibt den vollqualifizierten Domänennamen des der Headnodes im Cluster an. Namen sind durch Kommas getrennt. Fehler wird eine leere Zeichenfolge zurückgegeben. |
| `get_primary_headnode` | Ruft den vollqualifizierten Domänennamen des die primäre Headnode ab. Fehler wird eine leere Zeichenfolge zurückgegeben. |
| `get_secondary_headnode` | Ruft den vollqualifizierten Domänennamen des der sekundäre Headnode ab. Fehler wird eine leere Zeichenfolge zurückgegeben. |
| `get_primary_headnode_number` | Ruft des numerischen Suffixes die primäre Headnode ab. Fehler wird eine leere Zeichenfolge zurückgegeben. |
| `get_secondary_headnode_number` | Ruft des numerischen Suffixes die sekundäre Headnode ab. Fehler wird eine leere Zeichenfolge zurückgegeben. |

## <a name="commonusage"></a>Gemeinsame Verwendungsmuster

Dieser Abschnitt enthält Anleitungen auf einige der gemeinsamen Verwendungsmuster, die Sie bei Auftreten schreiben ein eigenes benutzerdefinierte Skript implementieren.

### <a name="passing-parameters-to-a-script"></a>Übergeben von Parametern an ein Skript

In einigen Fällen möglicherweise Ihr Skript Parameter erforderlich. Abrufen von Informationen aus der Ambari REST-API möglicherweise Sie beispielsweise die Administratorkennworts für den Cluster benötigen.

Parameter an das Skript übergeben werden als _Parameter mit Feldern fester Breite_bezeichnet und sind zugewiesen `$1` für den ersten Parameter, `$2` für das zweite und damit einmaliges Anmelden. `$0`enthält den Namen des eigentlichen Skripts.

Werte als Parameter an das Skript übergeben sollten einfache Anführungszeichen (') eingeschlossen werden, damit der übergebene Wert als Literal behandelt wird und besondere Behandlung darin enthaltenen Zeichen wie angegeben ist nicht '!'.

### <a name="setting-environment-variables"></a>Einrichten der Umgebungsvariablen

Festlegen einer Umgebungsvariable ausgeführt wird wie folgt:

    VARIABLENAME=value

Dabei ist VARIABLENNAME den Namen der Variablen an. Verwenden Sie für den Zugriff auf die Variable innerhalb der folgenden `$VARIABLENAME`. Wenn Sie einen Wert durch einen mit Feldern fester Breite Parameter als Umgebungsvariable-, die mit dem Namen Kennwort bereitgestellten zuweisen, möchten Sie beispielsweise Folgendes verwenden:

    PASSWORD=$1

Nachfolgende Zugriff auf die Informationen könnten dann verwenden `$PASSWORD`.

Umgebungsvariablen innerhalb des Skripts festlegen, die nur innerhalb des Gültigkeitsbereichs des Skripts vorhanden sein. In einigen Fällen müssen Sie möglicherweise breit Systemumgebungsvariablen hinzufügen, die beibehalten wird, nachdem Sie das Skript abgeschlossen ist. Dies ist in der Regel, damit Benutzer eine Verbindung herstellen mit dem Cluster über SSH bei Ihrem Skript installierten Komponenten verwenden können. Dies erreichen Sie durch das Hinzufügen der Umgebungsvariablen zu `/etc/environment`. Beispielsweise im folgenden Beispiel wird __HADOOP\_ü\_Verzeichnis__:

    echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a>Zugriff auf Speicherorte benutzerdefinierte Skripts gespeichert sind

Skripts verwendet, um einen Cluster anpassen müssen entweder in dem Speicher Standardkonto für den Cluster oder auf ein anderes Speicherkonto, in einer öffentlichen schreibgeschützten Container sein. Wenn Ihr Skript an anderen Ressourcen greift auf diese auch in einer öffentlich zugänglichen sein müssen (mindestens öffentlichen schreibgeschützt). Beispielsweise möglicherweise möchten Sie eine Datei nicht herunterladen bei der Verwendung von Cluster `download_file`.

Speichern der Datei in einem barrierefreien Azure-Speicher-Konto vom Cluster (z. B. des Standardkontos Speicher), wird raschen Zugriff angeben, wie diese Speicher innerhalb des Netzwerks Azure ist.

### <a name="checking-the-operating-system-version"></a>Aktivieren die Version des Betriebssystems

Unterschiedliche Versionen von HDInsight basieren auf bestimmten Versionen von Ubuntu. Möglicherweise gibt es Unterschiede zwischen OS-Versionen, die Sie für Ihr Skript Einchecken müssen. Beispielsweise müssen Sie eine binäre installieren, die mit der Version von Ubuntu verknüpft ist.

Verwenden Sie zum Überprüfen der Version des Betriebssystems `lsb_release`. Zum Beispiel veranschaulicht die folgenden Bezug auf eine andere Tar-Datei, je nach der Version des Betriebssystems:

    OS_VERSION=$(lsb_release -sr)
    if [[ $OS_VERSION == 14* ]]; then
        echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
        HUE_TARFILE=hue-binaries-14-04.tgz
    elif [[ $OS_VERSION == 16* ]]; then
        echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
        HUE_TARFILE=hue-binaries-16-04.tgz
    fi

## <a name="deployScript"></a>Checkliste für die Bereitstellung von einer Skriptaktion

Hier sind die Schritte, die wir erstellen, wenn Sie diese Skripts bereitstellen vorbereiten:

- Setzen Sie die Dateien, die die benutzerdefinierte Skripts an einem Ort enthalten, die während der Bereitstellung von dem Clusterknoten zugegriffen werden kann. Dies kann einen der standardmäßigen oder weiteren Speicherplatz Konten zum Zeitpunkt der Clusterbereitstellung oder einem beliebigen anderen öffentlich zugänglichen Speichercontainer angegeben sein.

- Hinzufügen von Prüfungen in Skripts, um sicherzustellen, dass er impotently, ausführen, so, dass das Skript mehrmals auf demselben Knoten ausgeführt werden kann.

- Verwenden Sie eine temporäre Datei Verzeichnis/tmp so behalten Sie die heruntergeladenen Dateien verwendet werden, indem Sie die Skripts und dann bereinigen sie nach Skripts ausgeführt haben.

- Den Fall, dass OS Ebene Einstellungen oder Hadoop Service Konfigurationsdateien geändert wurden, sollten Sie HDInsight-Dienste neu zu starten, damit sie von einer beliebigen OS Ebene Einstellungen, beispielsweise die Umgebungsvariablen in den Skripts festlegen auswählen können.

## <a name="runScriptAction"></a>Ausführen eine Skriptaktion

Skript-Aktionen können Sie HDInsight Cluster mithilfe des Azure-Portals Azure PowerShell Azure Ressource Manager (Cloud) Vorlagen oder HDInsight .NET SDK anpassen. Anweisungen erfahren Sie, [wie Skriptaktion verwenden](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Skriptbeispiele für benutzerdefinierte

Microsoft stellt Stichproben Skripts zum Installieren von Komponenten in einem HDInsight Cluster. Skripts und deren Verwendung Anweisungen stehen unter den folgenden Links:

- [Installieren und Verwenden von Farbton auf HDInsight Cluster](hdinsight-hadoop-hue-linux.md)
- [Installieren und Verwenden von R auf HDInsight Hadoop Cluster](hdinsight-hadoop-r-scripts-linux.md)
- [Installieren und Verwenden von Solr auf HDInsight Zuordnungseinheiten](hdinsight-hadoop-solr-install-linux.md)
- [Installieren und Verwenden von Giraph auf HDInsight Cluster](hdinsight-hadoop-giraph-install-linux.md)  

> [AZURE.NOTE] Die Dokumente, die über verknüpft sind HDInsight Linux-basierten Cluster. Eine Skripts, die mit Windows-basierten HDInsight arbeiten, finden Sie unter [Skript Aktion Entwicklung mit HDInsight (Windows)](hdinsight-hadoop-script-actions.md) oder verwenden Sie die verfügbaren Links am oberen Rand jeder Artikel.

##<a name="troubleshooting"></a>Behandlung von Problemen

Im folgenden werden Fehler auftreten können, wenn Sie Skripts verwenden, die Sie entwickelt haben:

__Error__: `$'\r': command not found`. Manchmal gefolgt von `syntax error: unexpected end of file`.

_Ursache_: Dieser Fehler wird ausgelöst, wenn die Zeilen in einem Skript mit CRLF beenden. UNIX-Systemen erwarten nur LF als das Ende der Zeile an.

Dieses Problem tritt in den meisten Fällen Wenn auf einem Windows-Umgebung, die das Skript verfasst wird ungeändert CRLF einer Linie enden für viele Text-Editoren unter Windows.

_Lösung_: Wenn sie eine Option im Texteditor ist, wählen Sie Unix-Format oder LF für das Ende der Zeile. Sie können auch die folgenden Befehle auf einem Unix-System verwenden, das CRLF in einer LF zu ändern:

> [AZURE.NOTE] Die folgenden Befehle sind annähernd, darin, dass sie die Zeilenenden CRLF auf LF ändern müssen. Wählen Sie eine basierend auf den Dienstprogrammen auf Ihrem System verfügbar.

| Befehl | Notizen |
| ------- | ----- |
| `unix2dos -b INFILE` | Die Originaldatei gesichert werden mit einem. BAK-Erweiterung |
| `tr -d '\r' < INFILE > OUTFILE` | OUTFILE wird eine Version mit nur LF Ende enthalten. |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Dadurch wird die Datei ändern, direkt ohne Erstellen einer neuen Datei |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` | OUTFILE wird eine Version mit nur LF Ende enthalten.

__Error__: `line 1: #!/usr/bin/env: No such file or directory`.

_Ursache_: Dieser Fehler tritt auf, wenn das Skript als UTF-8 mit einer Byte Order Mark (BOM) gespeichert wurde.

_Lösung_: Speichern Sie die Datei entweder als ASCII- oder UTF-8, ohne eine Stücklisten. Sie können auch mit dem folgenden Befehl auf einem Linux oder Unix-System zum Erstellen einer neuen Datei, ohne die Stücklisten verwenden:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Ersetzen Sie für die oben aufgeführten Befehl __INFILE__ mit der Datei, die die Stücklisten enthält. __OUTFILE__ sollten einen neuen Dateinamen ein, der das Skript ohne die Stücklisten enthalten sollen.

## <a name="seeAlso"></a>Nächste Schritte

* Erfahren Sie, wie [Anpassen HDInsight Cluster mithilfe der Skriptaktion](hdinsight-hadoop-customize-cluster-linux.md)

* Verwenden der [HDInsight .NET SDK-Referenz](https://msdn.microsoft.com/library/mt271028.aspx) , um weitere Informationen zum Erstellen von .NET Applications, die HDInsight verwalten

* Verwenden Sie die [REST-API HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) , wie Sie die restlichen Management Aktionen auf HDInsight Cluster verwenden können.
