<properties
   pageTitle="Verwenden Sie die Daten dem Store Java SDK zum Entwickeln von Applications | Microsoft Azure"
   description="Verwenden Sie zum Entwickeln von Applications Azure Daten dem Store Java SDK"
   services="data-lake-store"
   documentationCenter=""
   authors="nitinme"
   manager="jhubbard"
   editor="cgronlun"/>

<tags
   ms.service="data-lake-store"
   ms.devlang="na"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="na"
   ms.workload="big-data"
   ms.date="10/17/2016"
   ms.author="nitinme"/>

# <a name="get-started-with-azure-data-lake-store-using-java"></a>Erste Schritte mit Azure Lake Datenspeicher mit Java

> [AZURE.SELECTOR]
- [Portal](data-lake-store-get-started-portal.md)
- [PowerShell](data-lake-store-get-started-powershell.md)
- [.NET SDK](data-lake-store-get-started-net-sdk.md)
- [Java SDK](data-lake-store-get-started-java-sdk.md)
- [REST-API](data-lake-store-get-started-rest-api.md)
- [Azure CLI](data-lake-store-get-started-cli.md)
- [Node.js](data-lake-store-manage-use-nodejs.md)

Informationen Sie zum Verwenden von Azure Daten dem Store Java SDK Standardvorgänge ausführen, die beispielsweise als Erstellen von Ordnern, hoch- und Herunterladen von Datendateien usw.. Weitere Informationen zu den Daten Lake finden Sie unter [Azure dem Datenspeicher](data-lake-store-overview.md).

Sie können die Dokumente Java SDK API für Azure Lake Datenspeicher bei [Azure Daten dem Store Java-API-Dokumente](https://azure.github.io/azure-data-lake-store-java/javadoc/)zugreifen.

## <a name="prerequisites"></a>Erforderliche Komponenten

* Java Development Kit (JDK 7 oder höher, wobei Java Version 1.7 oder höher)
* Azure Lake Datenspeicher-Konto. Folgen Sie den Anweisungen bei [den ersten Schritten mit Azure dem Datenspeicher mithilfe der Azure-Portal](data-lake-store-get-started-portal.md)an.
* [Maven](https://maven.apache.org/install.html). In diesem Lernprogramm verwendet Maven für erstellen und Project Abhängigkeiten an. Obwohl es zu erstellen, ohne ein System erstellen, wie Maven oder Gradle möglich ist, ist diese Systeme erstellen einfacher zu Abhängigkeiten verwalten.
* (Optional) Und IDE wie [IntelliJ IDEE](https://www.jetbrains.com/idea/download/) oder ["Ellipse"](https://www.eclipse.org/downloads/) oder eine ähnliche.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Wie authentifiziert ich mit Azure Active Directory?

In diesem Lernprogramm verwenden wir eine Azure AD-Anwendung Client geheim, um ein Azure Active Directory-Token (Dienst-Authentifizierung) abzurufen. Wir verwenden diese Token zum Erstellen eines Objekts Lake Datenspeicher Client, um Vorgänge Datei- und durchzuführen. Anweisungen zum Authentifizieren mit Azure Lake Datenspeicher mithilfe der Client geheim führen wir die folgenden allgemeinen Schritte aus:

1. Erstellen einer Azure AD-Web-Anwendung
2. Abrufen der Client-ID, Client geheim und token Endpunkt für die Azure AD-Webanwendung an.
3. Konfigurieren des Zugriffs für Azure AD-Web-Anwendung auf dem Lake Datenspeicher Datei/temporärer Ordner, den Sie zugreifen, die Java-Anwendung, die Sie erstellen möchten.

Anweisungen zum Ausführen der folgenden Schritte aus finden Sie unter [Erstellen einer Active Directory-Anwendung](data-lake-store-authenticate-using-active-directory.md#create-an-active-directory-application).

Azure-Active Directory bietet weitere Optionen auch auf ein Token abgerufen. Sie können aus einer Reihe von Authentifizierungsverfahren zu Ihrem Szenario entsprechend beispielsweise eine Anwendung in einem Browser, eine Anwendung verteilt als eine desktop-Anwendung oder eine Server-Anwendung, die lokal ausgeführt oder in einer Azure-virtuellen Computern ausführen auswählen. Sie können auch aus verschiedenen Arten von Anmeldeinformationen wie Kennwörter, Zertifikate, 2-Faktor-Authentifizierung auswählen. Darüber hinaus können mit Azure Active Directory Sie Ihrem lokalen Active Directory-Benutzer mit der Cloud zu synchronisieren. Weitere Informationen finden Sie unter [Authentifizierungsszenarien Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Erstellen einer Java-Anwendungs

Beispiele für der Code verfügbar [auf GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) führt Sie durch den Vorgang des Erstellens im Store Dateien Verketten von Dateien, beim Herunterladen einer Datei, und löschen Sie einige Dateien im Speicher. In diesem Abschnitt der Artikel helfen Ihnen durch die wichtigsten Teile des Codes.

1. Erstellen eines Projekts Maven [Mvn Urtyp](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) über die Befehlszeile verwenden oder mithilfe einer IDE an. Anweisungen zum Erstellen eines Java-Projekts IntelliJ verwenden, finden Sie [hier](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Anleitung zum Erstellen eines Projekts mit "Ellipse" finden Sie [hier](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 

2. Fügen Sie die folgenden Abhängigkeiten zur Datei **pom.xml** Maven ein. Hinzufügen von Text zwischen den folgenden Codeausschnitt der ** \</Version >** Tag und die ** \</project >** Kategorie:

        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.0.4-SNAPSHOT</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>

    Die erste Abhängigkeit besteht darin, die Daten dem Store SDK verwenden (`azure-datalake-store`) aus dem Repository Maven. Die zweite Abhängigkeit (`slf4j-nop`) um anzugeben, welche Protokollierung Framework für diese Anwendung verwendet wird. Die Daten dem Store SDK verwendet [slf4j](http://www.slf4j.org/) Protokollierung Fassade, in dem Sie aus einer Vielzahl von beliebte Protokollierung Framework, wie log4j, Java-Protokollierung, Logback usw., auswählen kann oder keine Protokollierung. In diesem Beispiel werden wir Protokollierung deaktiviert, daher verwenden wir die **slf4j-Nop** Bindung. Um weitere Protokollierungsoptionen in Ihre app verwenden zu können, finden Sie [hier](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-the-application-code"></a>Fügen Sie den Anwendungscode

Es gibt drei Hauptteilen an den Code ein.

1. Das Azure-Active Directory-Token abrufen

2. Verwenden Sie das Token Erstellen eines Sees Datenspeicher-Clients aus.

3. Verwenden Sie den Lake Datenspeicher-Client zum Ausführen von Vorgängen.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Schritt 1: Eine Azure Active Directory-Token abrufen.

Die Daten dem Store SDK bietet benutzerfreundliche Methoden, mit denen Sie erhalten die Sicherheitstoken zum Kommunizieren mit dem Konto Lake Datenspeicher erforderlich sind. Das SDK wird jedoch nicht verlangen, dass nur diese Methoden verwendet werden. Sie können eine andere Möglichkeit zum Abrufen von Token ebenfalls, wie Sie mithilfe der [Azure-Active Directory-SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java)oder Ihren eigenen benutzerdefinierten Code verwenden.

Um die Daten dem Store SDK verwenden, um die Token für die Active Directory-Webanwendung erhalten Sie zuvor erstellt haben, verwenden Sie die statischen Methoden in `AzureADAuthenticator` Class. Ersetzen Sie mit der tatsächlichen Werte für die Anwendung Azure Active Directory Web **Hier ausfüllen** .

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AzureADToken token = AzureADAuthenticator.getTokenUsingClientCreds(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Schritt 2: Erstellen Sie ein Objekt der Azure Lake Datenspeicher-Client (ADLStoreClient)

Erstellen ein Objekt [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) , müssen Sie angeben der Lake Datenspeicher Kontonamen und dem Azure Active Directory-Token, das Sie im letzten Schritt generiert. Beachten Sie, dass der Lake Datenspeicher Kontoname einen vollqualifizierten Domänennamen werden muss. Ersetzen Sie beispielsweise **Hier ausfüllen** mit ungefähr wie folgt **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, token);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a>Schritt 3: Verwenden der ADLStoreClient Datei- und Operationen

Im folgenden Code enthält Beispiel Codeausschnitte häufig verwendete Vorgänge an. Sie können die vollständigen [Daten dem Store Java SDK-API Dokumente](https://azure.github.io/azure-data-lake-store-java/javadoc/) des Objekts **ADLStoreClient** zu anderen Vorgängen finden Sie unter anzeigen.
 
Beachten Sie, dass Dateien lesen und in mithilfe von standard Java Streams geschrieben werden. Dies bedeutet, dass Sie eine der Java Streams auf die Lake Datenspeicher Streams profitieren von Standardfunktionen Java (z. B. Drucken Streams für formatierte Ausgabe oder eine der Komprimierung oder Verschlüsselung Streams zusätzliche Funktionen auf oben) layer können.

    // set file permission
    client.setPermission(filename, "744");

    // append to file
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a>Schritt 4: Erstellen Sie, und führen Sie die Anwendung

1. Zum Ausführen von innerhalb einer IDE suchen Sie, und drücken Sie die Schaltfläche **Ausführen** . Verwenden Sie zum Ausführen von Maven [Mitarbeiter: Mitarbeiter](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html)aus.

2. Erstellen von zu erzeugen, einem eigenständigen Glas, die Sie in Befehlszeile ausführen können JAR-Datei mit allen Abhängigkeiten enthalten, mit der [Maven Assembly-Plug-in](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Die pom.xml im [Beispiel-Quellcode auf Github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) enthält ein Beispiel dazu.


## <a name="next-steps"></a>Nächste Schritte

- [Schützen von Daten in Lake Datenspeicher](data-lake-store-secure-data.md)
- [Verwenden von Azure Daten Lake Analytics mit Lake Datenspeicher](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Verwenden von Azure HDInsight mit Lake Datenspeicher](data-lake-store-hdinsight-hadoop-use-portal.md)
