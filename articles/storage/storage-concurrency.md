<properties
    pageTitle="Verwalten von Parallelität in Microsoft Azure-Speicher"
    description="Verwalten von Parallelität für die Dienste Blob, Warteschlange, Tabelle und Datei"
    services="storage"
    documentationCenter=""
    authors="jasonnewyork"
    manager="tadb"
    editor="tysonn"/>

<tags
    ms.service="storage"
    ms.workload="storage"
    ms.tgt_pltfrm="na"
    ms.devlang="dotnet"
    ms.topic="article"
    ms.date="10/18/2016"
    ms.author="jahogg"/>

# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Verwalten von Parallelität in Microsoft Azure-Speicher

## <a name="overview"></a>(Übersicht)

Moderne Internet-basierte Applikationen haben in der Regel mehrerer Benutzer anzeigen und Aktualisieren von Daten gleichzeitig. Setzt Entwickler genau überlegen wie eine vorhersehbare Erfahrung an die Endbenutzer besonders für Szenarien bereitgestellt, in dem mehrere Benutzer dieselben Daten aktualisieren können. Es gibt drei wichtigsten Daten Parallelität Strategien, die Entwickler in der Regel in Betracht ziehen, ein:  


1.  Vollständige Parallelität – lesen Sie eine Anwendung ausführen, die ein Update als Bestandteil der Aktualisierung überprüfen werden, wenn die Daten, da die Anwendung geändert haben letzten die Daten. Beispielsweise, wenn zwei Benutzer beim Anzeigen einer Wiki-Seite ein Update auf derselben Seite vornehmen muss dann die Wiki-Plattform sicherstellen, dass das zweite Update das erste Update – nicht überschrieben wird und beide Benutzer wissen, ob die Aktualisierung erfolgreich war. Diese Strategie wird am häufigsten in Webanwendungen verwendet.
2.  Eingeschränkte Parallelität – eine Anwendung suchen um eine Aktualisierung durchzuführen dauert eine Sperre für ein Objekt verhindern, dass andere Benutzer die Daten aktualisieren, bis die Sperre aufgehoben wird. Beispielsweise wird in einem Master/untergeordnete Daten Replikation Szenario, in dem nur das Master-Shape Updates ausführen, wird, das Master-Shape in der Regel halten eine exklusive Sperre für eine längere Zeit auf der Registerkarte Daten, um sicherzustellen, dass niemand aktualisiert werden können.
3.  Letzte jüngste Änderung gewinnt – ein Ansatz, der alle Aktualisierungsvorgänge, um den Vorgang fortzusetzen ohne überprüfen können, ob eine andere Anwendung die Daten zunächst seit der Anwendung wurde die Daten lesen. Diese Strategie (oder das Fehlen eines formalen Strategie) wird in der Regel verwendet, in dem Daten in einer Weise aufgeteilt werden, dass es ist keine Wahrscheinlichkeit, dass mehrere Benutzer dieselben Daten zugreifen können. Es kann auch hilfreich sein, in dem Datenstreams kurzlebige verarbeitet werden.  

Dieser Artikel enthält Übersicht über wie die Azure-Speicher Plattform Entwicklung durch erster Klasse Unterstützung für alle drei dieser Strategien Parallelität vereinfacht.  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure-Speicher vereinfacht die Cloudentwicklung von
Der Azure-Speicherdienst unterstützt alle drei Strategien, obwohl es ist besondere in der Lage ist, die umfassende Unterstützung für optimistischen und pessimistischen paralleler bereitstellen, weil es entwickelt wurde, auf eine signifikante Konsistenz Modell Zweifache der, die garantiert, wenn der Speicherdienst einer Daten einfügen Commit oder Aktualisierungsvorgang alle weiteren Zugriffe über die Daten des neuesten Updates angezeigt werden. Speicherplattformen mit einem tatsächlichen Konsistenz-Modell besitzen eine Verzögerung zwischen aus, wenn ein Schreibvorgang durchgeführt werden, von einem Benutzer, und wenn Sie die aktualisierten Daten durch andere Benutzer somit erschweren Entwicklung von Clientanwendungen müssen, um zu verhindern, dass Inkonsistenzen Auswirkung auf Anwender gesehen werden können.  

Zusätzlich zur Auswahl einer geeigneten Parallelität Strategie sollten Entwickler auch achten wie eine Speicherplattform Änderungen – besonders Änderungen auf dasselbe Objekt über Transaktionen isoliert. Der Azure-Speicherdienst verwendet Snapshot-Isolation um gelesen Vorgänge gleichzeitig mit Schreibvorgänge innerhalb einer Einzelpartition auftritt zu erlauben. Im Gegensatz zu anderen Isolationsebenen garantiert Snapshot-Isolation an, dass alle liest eine einheitliche Momentaufnahme der Daten finden Sie auch während Updates auftreten – im Wesentlichen durch die letzten Zugesicherter Werte, während eine Aktualisierung zurückgeben Transaktion verarbeitet wird.  

## <a name="managing-concurrency-in-blob-storage"></a>Verwalten von Parallelität im BLOB-Speicher
Sie können optional entweder optimistischen und pessimistischen Parallelitätsmodellen zum Verwalten des Zugriffs auf Blobs und Container im Blob-Dienst verwenden. Wenn Sie eine Strategie letzten schreibt Wins nicht explizit angeben ist der Standardwert.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Vollständige Parallelität für Blobs und Container  

Der Speicherdienst weist einen Bezeichner für jedes Objekt gespeichert. Jedes Mal, wenn ein Aktualisierungsvorgang für ein Objekt ausgeführt wird, wird dieser Bezeichner aktualisiert. Der Bezeichner wird als Teil einer HTTP-GET-Antwort mit der ETag (Entitätstag) Kopfzeile, die innerhalb der HTTP-Protokoll definiert wird an den Client zurückgegeben. Ein Benutzers solches Objekt ein Update ausführen kann in der ursprünglichen ETag zusammen mit einer bedingten Kopfzeile senden, um sicherzustellen, dass eine Aktualisierung nur stattfindet, wenn eine bestimmte Bedingung erfüllt ist – in diesem Fall die Bedingung ist mit einer "If-Match" Kopfzeile einzugeben der Speicherdienst, um sicherzustellen, dass der Wert von der in der Anforderung Update angegebene ETag identisch, die in der Speicherdienst gespeichert ist.  

Die Gliederung dieses Prozesses sieht wie folgt aus:  

1.  Abrufen eines BLOBs aus der Speicherdienst, die Antwort beinhaltet einen ETag-Header HTTP-Wert, der die aktuelle Version des Objekts in der Speicherdienst festlegt.
2.  Wenn Sie das Blob aktualisieren, fügen Sie den ETag-Wert, den Sie in Schritt 1 in der Kopfzeile der **If-Match** bedingte der Anfrage erhalten, die Sie zum Dienst senden.
3.  Der Dienst vergleicht den ETag-Wert in der Besprechungsanfrage mit den aktuellen ETag-Wert des Blob.
4.  Ist der aktuelle Wert der ETag des Blob eine andere Version als das ETag in das **If-Match** bedingte Kopf-oder Fußzeile die Anforderung, gibt der Dienst eine 412 Fehler an den Client zurück. Dies zeigt an an den Kunden, dass es sich bei einem anderen Prozess verwendet das Blob aktualisiert haben, da der Client Abrufen wieder.
5.  Ist der aktuelle Wert der ETag des Blob dieselbe Version wie das ETag in den **If-Match** bedingten Kopf-oder Fußzeile die Anforderung, wird der Dienst die angeforderten durchführt und aktualisiert den aktuellen ETag-Wert, der das Blob, um anzuzeigen, dass er eine neue Version erstellt hat.  

Folgende C#-Codeausschnitt (mit der Client-Speicher Bibliothek 4.2.0 müssen) zeigt ein einfaches Beispiel für das Erstellen einer **If-Match AccessCondition** anhand des Werts ETag, die aus der Eigenschaften eines Blob zugegriffen werden kann, die zuvor entweder abgerufen oder eingefügt wurde. Anschließend wird das Objekt **AccessCondition** Wenn sie das Blob aktualisieren: das Objekt **AccessCondition** der Anforderung den **If-Match** -Header hinzugefügt. Wenn Sie einem anderen Prozess verwendet das Blob aktualisiert haben, gibt der Blob-Dienst eine Meldung zum Verbindungsstatus HTTP 412 (Vorbedingung konnte nicht). Sie können das vollständige Beispiel hier herunterladen: [Verwalten von Parallelität mit Azure-Speicher](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

    // Retrieve the ETag from the newly created blob
    // Etag is already populated as UploadText should cause a PUT Blob call
    // to storage blob service which returns the etag in response.
    string orignalETag = blockBlob.Properties.ETag;

    // This code simulates an update by a third party.
    string helloText = "Blob updated by a third party.";

    // No etag, provided so orignal blob is overwritten (thus generating a new etag)
    blockBlob.UploadText(helloText);
    Console.WriteLine("Blob updated. Updated ETag = {0}",
    blockBlob.Properties.ETag);

    // Now try to update the blob using the orignal ETag provided when the blob was created
    try
    {
        Console.WriteLine("Trying to update blob using orignal etag to generate if-match access condition");
        blockBlob.UploadText(helloText,accessCondition:
        AccessCondition.GenerateIfMatchCondition(orignalETag));
    }
    catch (StorageException ex)
    {
        if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        {
            Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
            // TODO: client can decide on how it wants to handle the 3rd party updated content.
        }
        else
            throw;
    }  

Der Speicherdienst enthält auch Unterstützung für zusätzliche bedingten Header wie **If-geändert-seit**, **Wenn-unverändert-seit** und **If-keine-Match** sowie deren Kombinationen. Weitere Informationen finden Sie auf der MSDN- [Bedingte Kopfzeilen für BLOB-Dienstvorgänge angeben](http://msdn.microsoft.com/library/azure/dd179371.aspx) .  

In der folgenden Tabelle sind die Container Vorgänge, die bedingte Kopfzeilen wie z. B. **If-Match** in die Anfrage annehmen, und einen ETag-Wert in der Antwort zurückgeben, zusammengefasst.  

| Vorgang                | Gibt Container ETag-Wert | Bedingte Kopfzeilen akzeptiert |
|:-------------------------|:-----------------------------|:----------------------------|
| Container erstellen         | Ja                          | Nein                          |
| Containereigenschaften abrufen | Ja                          | Nein                          |
| Abrufen von Metadaten für Container   | Ja                          | Nein                          |
| Container-Metadaten   | Ja                          | Ja                         |
| Abrufen von Container ACL        | Ja                          | Nein                          |
| Festlegen der Container ACL        | Ja                          | Ja (*)                     |
| Container löschen         | Nein                           | Ja                         |
| Verleasen Container          | Ja                          | Ja                         |
| Liste Blobs               | Nein                           | Nein                          |

(*) Die vom SetContainerACL definierten Berechtigungen zwischengespeichert werden und Updates für folgende Berechtigungen 30 Sekunden dauern verteilen während den, die Zeitraum Updates nicht zum konsistent sein unbedingt.  

In der folgenden Tabelle enthält eine Übersicht über die Blob-Vorgänge, die bedingte Überschriften z. B. **If-Match** in die Anfrage annehmen, und in der Antwort einen ETag-Wert zurückgeben.

| Vorgang           | Gibt ETag-Wert | Bedingte Kopfzeilen akzeptiert           |
|:--------------------|:-------------------|:--------------------------------------|
| Setzen Sie Blob            | Ja                | Ja                                   |
| Abrufen von Blob            | Ja                | Ja                                   |
| Abrufen von Blob-Eigenschaften | Ja                | Ja                                   |
| Festlegen von Blob-Eigenschaften | Ja                | Ja                                   |
| Abrufen von Blob-Metadaten   | Ja                | Ja                                   |
| Blob-Metadaten   | Ja                | Ja                                   |
| Verleasen Blob (*)      | Ja                | Ja                                   |
| Blob Snapshot       | Ja                | Ja                                   |
| Kopieren von Blob           | Ja                | Ja (für Quell- und Zielfelder Blob) |
| Kopieren Blob Abbrechen     | Nein                 | Nein                                    |
| Blob löschen         | Nein                 | Ja                                   |
| Setzen Sie blockieren           | Nein                 | Nein                                    |
| Setzen Sie Blockliste      | Ja                | Ja                                   |
| Abrufen von Blockliste      | Ja                | Nein                                    |
| Seite setzen            | Ja                | Ja                                   |
| Erste Seite Bereiche     | Ja                | Ja                                   |


(*) Verleasen Blob ändert sich nicht auf das ETag auf ein Blob aus.  

### <a name="pessimistic-concurrency-for-blobs"></a>Eingeschränkte Parallelität für blobs
Einen Blob Exklusivmodus sperren möchten, können Sie eine [verleasen](http://msdn.microsoft.com/library/azure/ee691972.aspx) daran erwerben. Wenn Sie eine verleasen erwerben, Sie angeben, wie lange Sie die verleasen benötigen: Dies kann für zwischen 15 bis 60 Sekunden oder unbegrenzte die zu einer exklusiven Sperre Beträge. Sie können Erneuern einer begrenzten verleasen, um ihn zu erweitern, und können Sie alle verleasen freigeben, wenn Sie damit fertig sind. Der Blob-Dienst wieder automatisch begrenzten Leases aufgehoben sie ablaufen.  

Leases aktivieren anderen Synchronisierung Strategien unterstützt werden müssen, einschließlich exklusiven Schreibbereich / gelesen, ausschließlich Schreiben freigegeben / exklusives lesen und Schreiben freigegeben / exklusiv zu lesen. Wobei einer verleasen vorhanden ist erzwingt der Speicherdienst exklusiv schreibt (setzen, festlegen und Löschvorgängen) jedoch Ausschließlichkeit für Vorgänge gelesen Sicherstellung den Entwickler, um sicherzustellen, dass alle Clientanwendungen jeweils eine verleasen-ID und die nur einen einzigen Client verwenden erfordert eine gültige verleasen ID. hat. Lesen Sie Vorgänge, die nicht in freigegebenen liest eine verleasen ID-Ergebnis enthalten.  

Im folgende C#-Codeausschnitt zeigt ein Beispiel für beim Abrufen eines ausschließlich verleasen für 30 Sekunden auf ein Blob, aktualisieren den Inhalt des Blob und anschließend wieder die verleasen. Ist es bereits eine gültige verleasen auf das Blob bei dem Versuch, eine neue verleasen erfassen, gibt der Blob-Dienst ein "HTTP (409) Konflikt" Status Ergebnis. Der folgenden Codeausschnitt verwendet Objekt **AccessCondition** , um die verleasen-Informationen einschließen, wenn sie zum Aktualisieren des BLOBs in der Speicherdienst anfordert.  Sie können das vollständige Beispiel hier herunterladen: [Verwalten von Parallelität mit Azure-Speicher](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

    // Acquire lease for 15 seconds
    string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
    Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

    // Update blob using lease. This operation will succeed
    const string helloText = "Blob updated";
    var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
    blockBlob.UploadText(helloText, accessCondition: accessCondition);
    Console.WriteLine("Blob updated using an exclusive lease");

    //Simulate third party update to blob without lease
    try
    {
        // Below operation will fail as no valid lease provided
        Console.WriteLine("Trying to update blob without valid lease");
        blockBlob.UploadText("Update without lease, will fail");
    }
    catch (StorageException ex)
    {
        if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
            Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
        else
            throw;
    }  

Wenn Sie einen Schreibvorgang für eine geleaste Blob versuchen, ohne die ID verleasen übergeben, schlägt die Anforderung mit einem 412 Fehler fehl. Beachten Sie, dass wenn die verleasen läuft ab, bevor Sie die Methode **UploadText** aufrufen, aber Sie weiterhin die verleasen ID übergeben, die Anforderung auch mit einem Fehler **412** fehlschlägt. Weitere Informationen zur Verwaltung von verleasen Ablauf Zeiten und verleasen Ids finden Sie unter der [Verleasen Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) REST-Dokumentation.  

Die folgenden Blob-Vorgänge können Leases eingeschränkte Parallelität verwalten:  


-   Setzen Sie Blob
-   Abrufen von Blob
-   Abrufen von Blob-Eigenschaften
-   Festlegen von Blob-Eigenschaften
-   Abrufen von Blob-Metadaten
-   Blob-Metadaten
-   Blob löschen
-   Setzen Sie blockieren
-   Setzen Blockliste
-   Abrufen von Blockliste
-   Seite setzen
-   Erste Seite Bereiche
-   Snapshot Blob - verleasen ID optional, wenn eine verleasen vorhanden ist
-   Kopieren von Blob - erforderlich verleasen-ID aus, wenn eine verleasen auf das Ziel Blob vorhanden ist
-   Abbruch kopieren Blob - ID verleasen erforderlich, wenn eine unbegrenzte verleasen auf das Ziel Blob vorhanden ist
-   Verleasen Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Eingeschränkte Parallelität für Container
Leases auf Container aktivieren die gleichen Synchronisierung Strategien wie auf Blobs unterstützt werden müssen (exklusiv Schreiben / Lesen, ausschließlich Schreiben freigegeben / exklusives lesen und Schreiben freigegeben / exklusiv lesen) jedoch im Gegensatz zu Blobs der Speicherdienst nur Ausschließlichkeit auf Löschvorgänge erzwingt. Zum Löschen eines Containers mit einer aktiven verleasen muss ein Client die aktive verleasen-ID, mit der Anforderung löschen beinhalten. Klicken Sie auf eine geleaste Container alle anderen Container Vorgänge erfolgreich ausgeführt werden kann, ohne, wozu auch die Personalnummer verleasen Vorgänge in diesem Fall sind sie freigegeben. Ist Exklusivität des aktualisieren (sich oder Satz) oder gelesen Vorgänge erforderlich sollte dann Entwickler sicherzustellen, dass alle Clients nur jeweils einen Client eine gültige verleasen ID. weist eine verleasen-ID und die verwenden  

Die folgenden Container Vorgänge können Leases eingeschränkte Parallelität verwalten:  

-   Container löschen
-   Containereigenschaften abrufen
-   Abrufen von Metadaten für Container
-   Container-Metadaten
-   Abrufen von Container ACL
-   Festlegen der Container ACL
-   Verleasen Container  

Weitere Informationen finden Sie unter:  

- [Angeben von bedingten Kopfzeilen für Blob-Dienstvorgänge](http://msdn.microsoft.com/library/azure/dd179371.aspx)
- [Verleasen Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
- [Verleasen Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-the-table-service"></a>Verwalten von Parallelität im Dienst Tabelle
Der Tabelle-Dienst verwendet optimistische, dass Parallelität als Standardverhalten überprüft, wenn Sie mit Personen, die im Gegensatz zu den Blob-Dienst arbeiten, wo Sie explizit wählen müssen, um vollständige Parallelität überprüft werden soll. Ein weiterer Unterschied zwischen den Tabellen und Blob-Diensten ist, dass Sie nur die Parallelitätsverhalten Einheiten verwalten können, während mit dem Blob-Dienst Sie der gleichzeitigen sowohl Containern und Blobs verwalten können.  

Vollständige Parallelität verwendet, und prüfen, ob es sich bei einem anderen Prozess verwendet eine Entität geändert, nachdem Sie sie von der Tabelle Speicherdienst abgerufen, können Sie den ETag-Wert, den Sie erhalten, wenn der Dienst Tabelle eine Entität zurückgibt. Die Gliederung dieses Prozesses sieht wie folgt aus:  

1.  Eine Entität aus der Tabelle Speicherdienst abgerufen werden, die Antwort enthält einen ETag-Wert, der den aktuellen Bezeichner enthält, die diese Person in der Speicherdienst zugeordnet werden.
2.  Wenn Sie die Entität aktualisieren, einschließen des ETag-Werts, den Sie in Schritt 1 im Kopf der Anfrage obligatorisch **If-Match** zu erhalten, die Sie an den Dienst senden.
3.  Der Dienst vergleicht den ETag-Wert in der Besprechungsanfrage mit dem aktuellen ETag-Wert der Entität.
4.  Wenn der aktuelle ETag-Wert der Entität das ETag in das obligatorische **If-Match** -Header in der Anforderung unterscheidet, gibt der Dienst einer 412 Fehler an den Client zurück. Dies zeigt an an den Kunden, dass es sich bei einem anderen Prozess verwendet die Entität aktualisiert haben, da der Client Abrufen wieder.
5.  Wenn der aktuelle ETag-Wert der Entität dem das ETag im obligatorisch **If-Match** -Header in der Anforderung entspricht oder der **If-Match** -Header enthält das Platzhalterzeichen (*), wird der Dienst die angeforderten durchführt und den aktuellen ETag-Wert der Entität, um anzuzeigen, dass er aktualisiert wurde aktualisiert.  

Beachten Sie, dass im Gegensatz zu den Blob-Dienst, der Tabelle Dienst der Client einen **If-Match** -Header in Aktualisierungsabfragen aufnehmen möchten erfordert. Es ist jedoch möglich, die eine normale erzwingen aktualisieren (letzter Autor Wins Strategie) und der Parallelität umgehen, wenn der Client dem Platzhalterzeichen (*) in der Anforderung die Kopfzeile **If-Match** festlegt.  

Der folgende C#-Codeausschnitt zeigt eine Kundenentität, die entweder zuvor erstellt wurde, oder die e-Mail-Adresse aktualisiert haben, die abgerufen. Die ursprüngliche einfügen oder Abrufen von Vorgang Stores ETag-Wert in das Kundenobjekt und da die Stichprobe die gleichen Objektinstanz verwendet, wenn sie die Ersetzenvorgang ausgeführt wird, sendet automatisch den ETag-Wert wieder in der Tabelle Service, aktivieren den Dienst auf Parallelität geprüft. Wenn Sie einem anderen Prozess verwendet die Entität in Tabellenspeicher aktualisiert haben, gibt der Dienst eine Meldung zum Verbindungsstatus HTTP 412 (Vorbedingung konnte nicht).  Sie können das vollständige Beispiel hier herunterladen: [Verwalten von Parallelität mit Azure-Speicher](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

    try
    {
        customer.Email = "updatedEmail@contoso.org";
        TableOperation replaceCustomer = TableOperation.Replace(customer);
        customerTable.Execute(replaceCustomer);
        Console.WriteLine("Replace operation succeeded.");
    }
    catch (StorageException ex)
    {
        if (ex.RequestInformation.HttpStatusCode == 412)
            Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
        else
            throw;
    }  

Um die Überprüfung auf Parallelität explizit deaktivieren zu können, sollten Sie die Eigenschaft **ETag** das Objekt **Mitarbeiter** festlegen "*", bevor Sie die Ersetzenvorgang ausführen.  

    customer.ETag = "*";  

Die folgende Tabelle fasst zusammen, wie die Tabelle Entität Vorgänge ETag-Werte verwendet:

| Vorgang                | Gibt ETag-Wert | Erfordert If-Match Anfrage-header |
|:-------------------------|:-------------------|:---------------------------------|
| Abfrage-Elemente           | Ja                | Nein                               |
| Einfügen von Entität            | Ja                | Nein                               |
| Entität aktualisieren            | Ja                | Ja                              |
| Zusammenführen von Entität             | Ja                | Ja                              |
| Element löschen            | Nein                 | Ja                              |
| Einfügen oder ersetzen Entität | Ja                | Nein                               |
| Einfügen oder Entität zusammenführen   | Ja                | Nein                               |

Notiz, die das **Einfügen oder juristische ersetzen** und **Einfügen oder juristische Zusammenführen** hingegen ** keine Prüfungen Parallelität ausgeführt werden, da diese ETag-Wert nicht in der Tabelle Service senden.  

Im Allgemeinen sollten Entwickler, die mit Tabellen auf vollständige Parallelität verlassen, bei der Entwicklung von Applications skalierbare. Wenn pessimistische Sperren benötigt wird, können ein Ansatz Entwickler dauern, wenn Sie den Zugriff auf Tabellen besteht darin, weisen Sie einen festgelegten Blob für jede Tabelle, und versuchen, eine verleasen auf das Blob zu dauern, bevor Sie auf die Tabelle in Betrieb. Dieser Ansatz ist erforderlich, die Anwendung, um sicherzustellen, dass alle Daten Access Pfade die verleasen, indem Sie auf die Tabelle zu erhalten. Beachten Sie auch, dass die minimale verleasen Zeit ist 15 Sekunden sorgfältige für Skalierbarkeit einzugeben.  

Weitere Informationen finden Sie unter:  

- [Vorgänge für Personen](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-the-queue-service"></a>Verwalten von Parallelität in der Warteschlangendienst
Ein Szenario welche Gleichzeitigkeit von Bedeutung im Dienst einfügen in die Warteschlange ist ist, in dem mehrere Clients Nachrichten aus einer Warteschlange abrufen. Wenn eine Nachricht aus der Warteschlange abgerufen wird, enthält die Antwort an die Nachricht und eine Bestätigung pop-Wert, der erforderlich ist, um die Nachricht zu löschen. Die Nachricht wird nicht automatisch aus der Warteschlange gelöscht, aber nachdem es abgerufen wurde, es ist nicht für andere Clients sichtbar für den Zeitraum, der durch den Parameter Visibilitytimeout angegeben. Löschen die Nachricht aus, nachdem verarbeitet wurde und vor der Zeit, die durch die TimeNextVisible angegebenen der Antwort, das berechnete Element auf der Grundlage des Werts des Parameters Visibilitytimeout wird der Client, der die Nachricht empfängt erwartet. Der Wert von Visibilitytimeout ist Zeit addiert, die Nachricht abgerufen wird, um den Wert von TimeNextVisible zu ermitteln.  

Der Warteschlangendienst hat keine Unterstützung für entweder optimistischen und pessimistischen Parallelität und dies Grund-Clients, die Verarbeitung von Nachrichten aus einer Warteschlange abgerufen werden sollten sicherstellen, dass Nachrichten in Idempotent Weise verarbeitet werden. Eine Strategie der letzte Autor Wins ist für Update-Operationen wie SetQueueServiceProperties, SetQueueMetaData, SetQueueACL und UpdateMessage verwendet.  

Weitere Informationen finden Sie unter:  

- [Warteschlange Dienst REST-API](http://msdn.microsoft.com/library/azure/dd179363.aspx)
- [Abrufen von Nachrichten](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-the-file-service"></a>Verwalten von Parallelität in der Dateidienst
Der Dateidienst kann mit zwei verschiedenen Protokoll Endpunkten – SMB und REST zugegriffen werden. Der REST-Dienst hat keinen Support für optimistische Sperren oder pessimistische Sperren, und alle Updates werden die letzte Autor Wins Strategie befolgen. SMB-Clients, die Dateifreigaben bereitstellen können Datei System Sperren Verfahren zum Verwalten des Zugriffs auf freigegebene Dateien – einschließlich der Berechtigung zum Ausführen der vollständigen Sperren nutzen. Wenn ein SMB-Client eine Datei geöffnet wird, gibt Sie den Zugriff auf Dateien und die Freigabe Modus. Festlegen einer Datei Zugriffsoption "Schreiben" oder "/ Lese" zusammen mit einem Dateifreigabe-Modus von "Keine" führt die Datei von einem SMB-Client geschützt ist, bis die Datei geschlossen wird. Der REST-Dienst gibt Statuscode 409 (Konflikt) mit dem Fehlercode SharingViolation zurück, bei der restlichen Vorgangs an einer Datei ist, wo ein SMB-Client die Datei gesperrt hat.  

Wenn eine Datei zum Löschen von SMB-Client geöffnet wird, kennzeichnet die Datei als ausstehend löschen, bis alle anderen SMB-Client öffnen Kontrollpunkten an dieser Datei geschlossen sind. Während eine Datei als ausstehende löschen markiert ist, werden alle übrigen Vorgang auf dieser Datei Statuscode 409 (Konflikt) mit dem Fehlercode SMBDeletePending zurück. Statuscode 404 (nicht gefunden) wird nicht zurückgegeben, da es für den SMB-Client So entfernen Sie die Kennzeichnung ausstehende Löschung, indem Sie die Datei schließen möglich ist. Kurzum, Statuscode 404 (nicht gefunden) nur erwartet wird, wenn die Datei wurde entfernt. Beachten Sie, dass während einer SMB ausstehen und löschen eine Datei wird, es nicht in der Listendateien Ergebnisse berücksichtigt werden. Beachten Sie auch, dass der REST Datei löschen und die restlichen löschen Directory Vorgänge automatisch engagieren, und nicht ausstehen und löschen führen.  

Weitere Informationen finden Sie unter:  

- [Verwalten von Datei sperrt](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Zusammenfassung und nächste Schritte
Der Microsoft Azure-Speicherdienst wurde entwickelt, um die Anforderungen komplexe online-Anwendung ohne erzwungene Entwicklern das manipulieren oder überdenken Key Entwurf Annahmen wie Parallelität und Daten Konsistenz, die sie mittlerweile für gewährt wird.  

Für die vollständige Beispiel-Anwendung, auf die verwiesen wird in diesem Blog:  

- [Verwalten von Parallelität mit Azure-Speicher - Beispiel-Anwendung](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Für Weitere Informationen zu Azure-Speicher finden Sie unter:  

- [Homepage von Microsoft Azure-Speicher](https://azure.microsoft.com/services/storage/)
- [Einführung in Azure-Speicher](storage-introduction.md)
- Erste Schritte für [Blob](storage-dotnet-how-to-use-blobs.md), [Tabelle](storage-dotnet-how-to-use-tables.md), [Warteschlangen](storage-dotnet-how-to-use-queues.md)und [Dateien](storage-dotnet-how-to-use-files.md) Speicher
- Speicherarchitektur – [Azure-Speicher: eine hoch verfügbare Cloud-Speicherdienst mit signifikante Konsistenz](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)
