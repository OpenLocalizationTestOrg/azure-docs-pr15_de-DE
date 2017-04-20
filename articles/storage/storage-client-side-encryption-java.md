<properties
    pageTitle="Clientseitige Verschlüsselung mit Java für Microsoft Azure-Speicher | Microsoft Azure"
    description="Der Azure-Speicher Client-Bibliothek für Java unterstützt clientseitige Verschlüsselung und Integration in Azure-Taste Tresor für maximale Sicherheit für Ihre Applikationen Azure-Speicher."
    services="storage"
    documentationCenter="java"
    authors="dineshmurthy"
    manager="jahogg"
    editor="tysonn"/>

<tags
    ms.service="storage"
    ms.workload="storage"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/18/2016"
    ms.author="dineshm"/>


# <a name="client-side-encryption-with-java-for-microsoft-azure-storage"></a>Clientseitige Verschlüsselung mit Java for Microsoft Azure-Speichers   

[AZURE.INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>(Übersicht)  

Der [Azure-Speicher-Client-Bibliothek für Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) unterstützt Verschlüsselung von Daten in Clientanwendungen vor dem Hochladen in Azure-Speicher und Entschlüsseln von Daten beim Herunterladen auf den Client. Die Bibliothek unterstützt Integration mit [Azure Schlüssel Tresor](https://azure.microsoft.com/services/key-vault/) auch für Speicher-Konto Key-Verwaltung.

## <a name="encryption-and-decryption-via-the-envelope-technique"></a>Verschlüsseln und Entschlüsseln über den Umschlag-Methode    
Führen Sie die Prozesse Verschlüsselung und Entschlüsseln die Umschlag Methode aus.  

### <a name="encryption-via-the-envelope-technique"></a>Verschlüsselung über den Umschlag-Methode  
Verschlüsselung über den Umschlag Methode funktioniert wie folgt:  

1.  Die Azure-Speicher-Client-Bibliothek generiert einen Schlüssel für Verschlüsselung von Inhalten (CEK), also eine one einmalig verwenden symmetrischen Schlüssel.  

2.  Mithilfe dieser CEK Benutzerdaten verschlüsselt.   

3.  Die CEK wird dann umschlossen () mit den wichtigsten Schlüssel verschlüsselt (KEK). Die KEK wird durch einen Key Identifier identifiziert und werden ein Paar für asymmetrische Key oder einen symmetrischen Schlüssel und kann lokal verwaltete oder möglich in Azure Key Depots gespeichert.  
Die Speicher-Client-Bibliothek selbst weist nie Zugriff auf KEK. Die Bibliothek Ruft den wichtigsten Umbruch Algorithmus, der Taste Tresor genannt ist. Benutzerdefinierte Anbieter für Key Umbruch/Entpacken verwenden, falls gewünscht, können Benutzer auswählen.  

4.  Die verschlüsselten Daten werden dann in der Azure-Speicherdienst hochgeladen werden. Der Umgebrochene Schlüssel sowie einige weitere Verschlüsselung Metadaten als Metadaten (auf ein Blob) gespeichert oder mit der verschlüsselten Daten (Warteschlangennachrichten und Tabelle Einheiten) interpoliert.

### <a name="decryption-via-the-envelope-technique"></a>Entschlüsseln über den Umschlag-Methode  
Entschlüsseln über den Umschlag Methode funktioniert wie folgt:  

1.  Die Client-Bibliothek wird davon ausgegangen, dass der Benutzer die wichtigsten Verschlüsselungsschlüssels (KEK) lokal oder in Azure Key Depots verwalten. Der Benutzer muss nicht den bestimmten Schlüssel kennen, der für die Verschlüsselung verwendet wurde. Stattdessen kann eine Key Auflösung der anderen Key Identifier in Tasten aufgelöst wird eingerichtet und verwendet.  

2.  Die Client-Bibliothek downloads die verschlüsselten Daten zusammen mit Verschlüsselung Material, die auf den Dienst gespeichert ist.  

3.  Umgebrochene Inhalt Verschlüsselungsschlüssels (CEK) ist, und klicken Sie dann mit der Taste Verschlüsselung allein stehenden (entschlüsselt) wichtiger (KEK). Hier wird erneut, die Client-Bibliothek nicht auf KEK zugreifen. Ruft Sie einfach das benutzerdefinierte oder Entpacken Algorithmus Schlüssel Tresor-Anbieter.  

4.  Der Inhalt Verschlüsselungsschlüssels (CEK) wird dann zum Entschlüsseln der verschlüsselten Benutzerdaten.

## <a name="encryption-mechanism"></a>Verfahren für Verschlüsselung  
Die Speicher-Client-Bibliothek wird [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) um Benutzerdaten verschlüsseln. Insbesondere [Verschlüsselung Block verketten (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) Modus mit AES. Jede service funktioniert etwas anders ausgeführt, damit wir ihnen hier besprechen wird.

### <a name="blobs"></a>BLOBs  
Die Client-Bibliothek unterstützt die Verschlüsselung nur gesamte Blobs aktuell. Insbesondere Verschlüsselung wird unterstützt, wenn der Benutzer die **Hochladen** verwenden* Methoden oder die * *OpenOutputStream** Methode. Für Downloads, beide abgeschlossen und Bereich Downloads unterstützt werden.  

Bei der Verschlüsselung die Clientbibliothek generiert eine zufällige Initialisierung Vektor (IV) von 16 Bytes, zusammen mit einer Taste zufällige Verschlüsselung von Inhalten (CEK) 32 Bytes und Umschlag Verschlüsselung BLOB-Daten mithilfe dieser Informationen ausführen. Der Umgebrochene CEK und einige zusätzliche Verschlüsselung Metadaten sind wie Metadaten zusammen mit der verschlüsselten Blob-Dienst BLOB-dann gespeichert.

>[AZURE.WARNING] Wenn Sie bearbeiten oder eigene Metadaten für das Blob hochladen, müssen Sie sicherstellen, dass diese Metadaten gewahrt wird. Wenn Sie neue Metadaten ohne diese Metadaten hochladen, der Umgebrochene CEK, IV und sonstige Metadaten verloren und der BLOB-Inhalt werden nie einer abrufbaren erneut.

Herunterladen eines verschlüsselten BLOBs umfasst den Inhalt des gesamten Blob mithilfe der */openInputStream *herunterladen**abrufen * Komfort Methoden. Der Umgebrochene CEK ausgepackt und zusammen mit der IV (in diesem Fall als Blob-Metadaten gespeichert) verwendet wird, um die entschlüsselten Daten an den Benutzer zurückzugeben.

Herunterladen eines beliebigen Textbereichs (**DownloadRange*** Methoden) im verschlüsselten Blob umfasst Einstellen des Bereichs von Benutzer bereitgestellt werden, um eine kleine zusätzliche Datenmenge abrufen, die den angeforderten Bereich erfolgreich entschlüsseln verwendet werden können.  

Alle Typen blob (Blobs blockieren, Blobs Seite und Anfügen Blobs) können verschlüsselt/entschlüsselt werden dieses Schema verwenden.

### <a name="queues"></a>Warteschlangen  
Da Warteschlangennachrichten von einem beliebigen Format werden können, definiert die Clientbibliothek ein benutzerdefiniertes Formats, das in den Nachrichtentext Initialization Vektor (IV) und die Verschlüsselung von verschlüsselten Inhalten-Taste (CEK) enthält.  

Bei der Verschlüsselung die Clientbibliothek generiert einen zufälligen IV von 16 Bytes sowie eine zufällige CEK 32 Bytes und führt Umschlag Verschlüsselung der Warteschlange Nachrichtentext mithilfe dieser Informationen aus. Der Umgebrochene CEK und einige zusätzliche Verschlüsselung Metadaten werden dann die Warteschlange verschlüsselte Nachricht hinzugefügt. Klicken Sie auf den Dienst wird diese geänderte Nachricht (siehe unten) gespeichert.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

Der Umgebrochene Schlüssel ist während entschlüsseln aus der Warteschlange Nachricht extrahiert und unverpacktem. Die IV ist auch aus der Warteschlange Nachricht extrahiert und zusammen mit dem allein stehenden Schlüssel verwendet werden, um die Daten der Warteschlange Nachricht entschlüsseln. Beachten Sie, dass die Verschlüsselung Metadaten small (unter 500 Byte) ist, sodass gedrückt, während sie das 64 KB Limit für eine Nachricht Warteschlange berücksichtigt, der Einfluss verwaltbare sein soll.

### <a name="tables"></a>Tabellen  
Die Client-Bibliothek unterstützt die Verschlüsselung der Elementeigenschaften für einfügen und Ersetzungsvorgänge.

>[AZURE.NOTE] Zusammenführen wird derzeit nicht unterstützt. Da eine Teilmenge der Eigenschaften möglicherweise zuvor mit einem anderen Schlüssel verschlüsselt sind, führt einfach die neuen Eigenschaften zusammenführen und aktualisieren die Metadaten Datenverlust. Zusammenführen von entweder erfordert zusätzliche Service-Anrufe, die bereits vorhandene Entität aus dem Dienst zu lesen, oder verwenden einen neuen Product Key pro Eigenschaft, beide über eignen sich nicht für die Leistung zu verbessern.

Tabelle Daten Verschlüsselung funktioniert wie folgt aus:  

1.  Benutzer geben Sie die Eigenschaften verschlüsselt werden.  

2.  Die Client-Bibliothek generiert eine zufällige Initialisierung Vektor (IV) von 16 Bytes zusammen mit einem zufällige Inhalt Schlüssel (CEK) 32 Bytes für jede Person, und führt Umschlag Verschlüsselung auf die einzelnen Eigenschaften verschlüsselt werden, indem Sie einen neuen IV pro Eigenschaft abgeleitet. Die verschlüsselte Eigenschaft wird als binäre Daten gespeichert werden.  

3.  Der Umgebrochene CEK und einige weitere Verschlüsselung Metadaten werden dann als zwei weitere reservierte Eigenschaften gespeichert. Die erste reservierte Eigenschaft (_ClientEncryptionMetadata1) ist eine Zeichenfolgeneigenschaft, die Informationen zu IV, Version und Umgebrochene Key enthält. Die zweite reservierte Eigenschaft (_ClientEncryptionMetadata2) ist ein binäre Eigenschaft, die Informationen zu den Eigenschaften enthält, die verschlüsselt sind. Die Informationen in dieser zweiten Eigenschaft (_ClientEncryptionMetadata2) ist selbst verschlüsselt.  

4.  Aufgrund von diese zusätzlichen reservierten Eigenschaften für die Verschlüsselung erforderlich ist können Benutzer jetzt nur 250 benutzerdefinierte Eigenschaften anstelle von 252 verfügen. Die Gesamtgröße der Entität muss kleiner als 1 MB.  

    Beachten Sie, dass nur die Zeichenfolgeneigenschaften verschlüsselt werden können. Wenn Sie andere Arten von Eigenschaften werden verschlüsselt werden, müssen sie in Zeichenfolgen konvertiert werden. Die verschlüsselten Zeichenfolgen werden vom Dienst als binäre Eigenschaften gespeichert, und sie wieder in Zeichenfolgen konvertiert werden, nach entschlüsseln.

    Für Tabellen, sowie die Verschlüsselungsrichtlinie müssen Benutzer die Eigenschaften verschlüsselt werden angeben. Dies kann entweder ein Attribut [verschlüsseln] (für POCO-Einheiten, die von TableEntity abgeleitet werden) oder einer Auflösung Verschlüsselung in angeben Anforderung Optionen erfolgen. Eine Verschlüsselung Auflösung ist eine Stellvertretung, die eine Partitionsschlüssel, Zeile-Taste und Eigenschaftsname verwendet und gibt einen Boolean zurück, der angibt, ob die Eigenschaft verschlüsselt werden soll. Bei der Verschlüsselung wird die Clientbibliothek diese Informationen verwendet, um zu entscheiden, ob eine Eigenschaft beim Schreiben zur Übertragung verschlüsselt werden soll. Die Stellvertretung sieht auch die Möglichkeit der Logik vor wie Eigenschaften verschlüsselt werden. (Beispielsweise ist X, dann verschlüsseln Eigenschaft A; andernfalls verschlüsseln Eigenschaften A und b) Beachten Sie, dass es nicht erforderlich sind, um diese Informationen beim Lesen oder Abfragen von Personen zu machen.

### <a name="batch-operations"></a>Stapel Vorgänge  
In Stapelvorgängen werden die gleichen KEK über alle Zeilen in dieser Reihe Vorgang verwendet werden, da die Clientbibliothek nur ein Optionsobjekt (und daher einer Richtlinie/KEK) ermöglicht pro Blatt Vorgang. Die Client-Bibliothek intern einen neuen zufällige IV und zufällige CEK pro Zeile in den Stapel generiert jedoch. Benutzer können auch andere Eigenschaften für jeden Vorgang im Stapel verschlüsseln dieses Verhalten in die Verschlüsselung Auflösung definieren auswählen.

### <a name="queries"></a>Abfragen  
Um Abfrage durchzuführen, müssen Sie einen Key Auflösung angeben, die alle Schlüssel im Resultset auflösen kann. Wenn eine Entität im Abfrageergebnis enthaltenen mit einem Anbieter aufgelöst werden kann, wird die Clientbibliothek ein Fehler ausgelöst. Für jede Abfrage, die Seite Projektionen Server ausführt, wird die Clientbibliothek die spezielle Verschlüsselung Metadateneigenschaften (_ClientEncryptionMetadata1 und _ClientEncryptionMetadata2) hinzufügen standardmäßig die ausgewählten Spalten.

## <a name="azure-key-vault"></a>Azure Key Tresor  
Azure-Taste Tresor hilft cryptographic Tasten schützen und Kennwörter von Cloudanwendungen und Dienste verwendet. Mithilfe von Azure Taste Tresor können Benutzer Tasten und vertraulichen Daten (z. B. Authentifizierung, Speicher Konto Tasten, Daten Verschlüsselung Tasten,. verschlüsseln. PFX-Dateien und Kennwörter) mithilfe von Tasten, die durch Hardware Security Module (HSMs) geschützt werden. Weitere Informationen finden Sie unter [Neuigkeiten Azure-Taste Tresor?](../key-vault/key-vault-whatis.md).

Die Speicher-Client-Bibliothek verwendet die Taste Tresor Core-Bibliothek, um ein gemeinsamer Rahmen über Azure bereitstellen, für die Verwaltung von Tasten. Benutzer erhalten auch den zusätzlichen Vorteil der Nutzung der Schlüssel Tresor Extensions-Bibliothek. Die Extensions-Bibliothek bietet nützliche Funktionalität, um einfache und nahtlose symmetrisch/RSA lokale und Key Cloud-Anbieter und mit Aggregation und Zwischenspeichern.

### <a name="interface-and-dependencies"></a>Benutzeroberfläche und Abhängigkeiten  
Es gibt drei Schlüssel Tresor-Paketen:  

- Azure-Keyvault-Core enthält die IKey und IKeyResolver. Es ist ein kleines Paket mit keine Abhängigkeiten. Die Speicher-Client-Bibliothek für Java, die sie als Abhängigkeit definiert.
- Azure-Keyvault enthält den Taste Tresor REST-Client.  
- Azure-Keyvault-Erweiterungen enthält Erweiterungscode, der Implementierung von cryptographic Algorithmen und eine RSAKey und eine SymmetricKey umfasst. Es hängt von den Core und KeyVault Namespace und stellt die Funktionalität zum Definieren einer aggregieren Auflösung (Wenn Sie möchten, dass Benutzer mehrere wichtige Anbieter verwenden) und eine Zwischenspeichern Key Auflösung. Zwar Speicher-Client-Bibliothek nicht direkt von diesem Paket, abhängt Wenn Benutzer Azure Taste Tresor verwenden, um ihre Schlüssel speichern oder verwenden Sie die Taste Tresor Erweiterungen zu nutzen den lokalen cloud cryptographic Provider möchten, benötigen sie dieses Paket.  

  Tresor Schlüssel ist für das wertvolle Master Tasten und Drosselung Grenzwerte pro Schlüssel Tresor dienen mit diesem berücksichtigen. Wenn Sie clientseitige Verschlüsselung mit Key Tresor durchführen zu können, ist das bevorzugte Modell symmetrische Master Schlüssel als vertrauliche Informationen in Key Tresor gespeichert und Cache lokal verwenden. Benutzer müssen die folgenden Schritte ausführen:  

1.  Erstellen Sie einen geheimen offline, und klicken Sie auf-Taste Tresor hochladen.  

2.  Verwenden Sie das Kennwort des Basis Bezeichner als Parameter, zum Beheben der aktuellen Version der Schlüssel für die Verschlüsselung und diese Informationen lokal zwischenspeichern. Verwenden Sie zum Zwischenspeichern von CachingKeyResolver; Benutzer sollten kein implementieren eigene Logik Zwischenspeichern.  

3.  Verwenden Sie die Auflösung Zwischenspeichern als Eingabe beim Erstellen der Verschlüsselungsrichtlinie.
Weitere Informationen zur Verwendung von Taste Tresor finden Sie in den Codebeispielen Verschlüsselung. <fix URL>  

## <a name="best-practices"></a>Bewährte Methoden  
Unterstützung für Verschlüsselung steht nur in der Bibliothek Speicher-Client für Java.

>[AZURE.IMPORTANT] Achten Sie auf diese wichtigen Punkte, wenn die clientseitige Verschlüsselung verwendet:
>  
>- Verwenden Sie beim Lesen aus oder Schreiben in einer verschlüsselten Blob gesamte Blob Upload Befehle und Bereich/ganze Blob Download Befehle. Vermeiden Sie das Schreiben in einer verschlüsselten Blob mit Protokoll Operationen wie blockieren setzen, Blockliste setzen, Schreiben von Seiten, Löschen von Seiten oder blockieren Anfügen; Andernfalls können Sie beschädigter verschlüsselte Blob und nicht gelesen werden.
>
>- Für Tabellen vorhanden ist eine ähnliche Einschränkung aus. Achten Sie darauf, dass keine verschlüsselte Eigenschaften aktualisieren, ohne die Verschlüsselung Metadaten zu aktualisieren.  
>
>- Wenn Sie auf die verschlüsselte Blob Metadaten festgelegt, überschreiben Sie möglicherweise die Verschlüsselung Zusammenhang Metadaten für Verschlüsselung erforderlich, da das Festlegen von Metadaten nicht erweiterbar ist. Dies gilt auch für Momentaufnahmen; Vermeiden Sie es, Metadaten beim Erstellen einer Momentaufnahme einer verschlüsselten Blob. Wenn Metadaten festgelegt werden muss, achten Sie darauf, zum Aufrufen der Methode **DownloadAttributes** zuerst, um die aktuellen Verschlüsselung Metadaten zu erhalten und zu vermeiden Sie gleichzeitige schreibt während Metadaten festgelegt wird.  
>
>- Aktivieren Sie die Kennzeichen **RequireEncryption** in der Standardoptionen für die Anfrage für Benutzer, die nur in Verbindung mit verschlüsselten Daten arbeiten soll. Weitere Informationen finden Sie unter.  

## <a name="client-api--interface"></a>Client-API / Schnittstelle  
Beim Erstellen eines Objekts EncryptionPolicy, können Benutzer nur einen Schlüssel (implementieren IKey), bieten nur eine Auflösung (implementieren IKeyResolver) oder beides. IKey ist die grundlegende Art des Schlüssels, die mit einer Key-ID gekennzeichnet wird und die Logik für die Funktion zum Umbrechen von/Entpacken bereitstellt. IKeyResolver dient zum Lösen eines Keys während der Entschlüsselungsprozess. Es definiert eine ResolveKey Methode, die einer angegebenen einen Key Identifier IKey zurückgibt. Dies bietet Benutzern die Möglichkeit, zwischen mehreren Tasten auszuwählen, die an mehreren Speicherorten verwaltet werden.

- Für die Verschlüsselung der Schlüssel wird immer verwendet, sowie das Fehlen eines Schlüssels führt zu einem Fehler Fehlern.  
- Zum Entschlüsseln:  
    - Die wichtige Auflösung wird aufgerufen, wenn den Schlüssel abgerufen angegeben. Die Auflösung angegeben, jedoch verfügt nicht über eine Zuordnung für den Key Bezeichner enthält, wird ein Fehler ausgelöst.  
    - Auflösung nicht angegeben, jedoch ein Schlüssel angegeben ist, wird der Schlüssel verwendet, dessen Kennung die erforderliche Schlüssel-ID stimmt. Wenn der Bezeichner nicht übereinstimmt, wird ein Fehler ausgelöst.  

      [Beispiele für Verschlüsselung](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>eine ausführlichere End-to-End-Szenario für Blobs, Queues und Tabellen, zusammen mit Key Tresor Integration zu veranschaulichen.

### <a name="requireencryption-mode"></a>RequireEncryption-Modus  
Benutzer können optional einen Modus des Vorgangs aktivieren, in dem alle Uploads und Downloads verschlüsselt werden müssen. In diesem Modus tritt Versuche, Daten, ohne dass eine Verschlüsselungsrichtlinie hochladen oder Herunterladen von Daten, die nicht auf den Dienst verschlüsselt sind auf dem Client. Die Kennzeichnung **RequireEncryption** des Objekts Optionen Anforderung steuert dieses Verhalten. Wenn die Anwendung alle Objekte in Azure-Speicher verschlüsselt wird, können Sie die Eigenschaft **RequireEncryption** auf die Anfrage Standardoptionen für den Dienst Client-Objekt festlegen.   

Verwenden Sie beispielsweise **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** Verschlüsselung für alle Blob-Vorgänge ausgeführt, bis das Clientobjekt erfordern.

### <a name="blob-service-encryption"></a>BLOB-Service-Verschlüsselung  
Erstellen Sie ein Objekt **BlobEncryptionPolicy** , und legen Sie sie in die Anfrage Optionen (pro-API oder eine Ebene Client mithilfe von **DefaultRequestOptions**). Allen weiteren Aufgaben werden von der Clientbibliothek intern behandelt werden.

    // Create the IKey used for encryption.
    RsaKey key = new RsaKey("private:key1" /* key identifier */);

    // Create the encryption policy to be used for upload and download.
    BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

    // Set the encryption policy on the request options.
    BlobRequestOptions options = new BlobRequestOptions();
    options.setEncryptionPolicy(policy);

    // Upload the encrypted contents to the blob.
    blob.upload(stream, size, null, options, null);

    // Download and decrypt the encrypted contents from the blob.
    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
    blob.download(outputStream, null, options, null);

### <a name="queue-service-encryption"></a>Die Verschlüsselung der service  
Erstellen Sie ein Objekt **QueueEncryptionPolicy** , und legen Sie sie in den Optionen Anforderung (pro-API oder eine Ebene Client mithilfe von **DefaultRequestOptions**). Allen weiteren Aufgaben werden von der Clientbibliothek intern behandelt werden.

    // Create the IKey used for encryption.
    RsaKey key = new RsaKey("private:key1" /* key identifier */);

    // Create the encryption policy to be used for upload and download.
    QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

    // Add message
    QueueRequestOptions options = new QueueRequestOptions();
    options.setEncryptionPolicy(policy);

    queue.addMessage(message, 0, 0, options, null);

    // Retrieve message
    CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);

### <a name="table-service-encryption"></a>Tabelle Service-Verschlüsselung  
Sie müssen zusätzlich zum Erstellen einer Verschlüsselungsrichtlinie und diese Anforderung Optionen festlegen, geben Sie eine **EncryptionResolver** in **TableRequestOptions**oder legen Sie das Attribut [verschlüsseln] auf der Entität Get und Set.

### <a name="using-the-resolver"></a>Verwenden die Auflösung  

    // Create the IKey used for encryption.
    RsaKey key = new RsaKey("private:key1" /* key identifier */);

    // Create the encryption policy to be used for upload and download.
    TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

    TableRequestOptions options = new TableRequestOptions()
    options.setEncryptionPolicy(policy);
    options.setEncryptionResolver(new EncryptionResolver() {
        public boolean encryptionResolver(String pk, String rk, String key) {
            if (key == "foo")
            {
                return true;
            }
            return false;
        }
    });

    // Insert Entity
    currentTable.execute(TableOperation.insert(ent), options, null);

    // Retrieve Entity
    // No need to specify an encryption resolver for retrieve
    TableRequestOptions retrieveOptions = new TableRequestOptions()
    retrieveOptions.setEncryptionPolicy(policy);

    TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
    TableResult result = currentTable.execute(operation, retrieveOptions, null);

### <a name="using-attributes"></a>Verwenden von Attributen  
Wie erwähnt, wenn die Entität TableEntity, implementiert, und klicken Sie dann die Eigenschaften Get und Set mit dem Attribut [verschlüsseln] anstelle der **EncryptionResolver**versehen werden können.

    private string encryptedProperty1;

    @Encrypt
    public String getEncryptedProperty1 () {
        return this.encryptedProperty1;
    }

    @Encrypt
    public void setEncryptedProperty1(final String encryptedProperty1) {
        this.encryptedProperty1 = encryptedProperty1;
    }

## <a name="encryption-and-performance"></a>Verschlüsselung und Leistung  
Beachten Sie, dass Ihre Daten ergibt zusätzliche Leistung Verwaltungsaufwand Speicher verschlüsseln werden soll. Inhalt Schlüssel und IV generiert werden muss, muss der Inhalt selbst verschlüsselt werden und zusätzliche Metadaten formatiert und hochgeladen werden müssen. Dieser Aufwand variieren je nach der Menge der verschlüsselten Daten. Es empfiehlt sich, dass Kunden immer deren Anwendung für Leistung bei der Entwicklung testen.

## <a name="next-steps"></a>Nächste Schritte  

- Herunterladen der [Azure-Speicher Clientbibliothek für Maven Java-Paket](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)  
- Herunterladen der [Azure-Speicher-Client-Bibliothek für Java-Quellcode GitHub](https://github.com/Azure/azure-storage-java)   
- Herunterladen der Azure-Taste Tresor Maven Bibliothek für Java Maven-Paketen:
    - [Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) -Paket
    - [Client](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) -Paket
- Besuchen Sie die [Azure Key Vaulting Dokumentation](../key-vault/key-vault-whatis.md)  
