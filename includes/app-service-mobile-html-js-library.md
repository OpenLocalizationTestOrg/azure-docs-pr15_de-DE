##<a name="create-client"></a>Herstellen einer Clientverbindung

Erstellen Sie eine Client-Verbindung durch Erstellen einer `WindowsAzure.MobileServiceClient` Objekt.  Ersetzen Sie `appUrl` durch den URL zur Mobile-App.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

##<a name="table-reference"></a>Arbeiten mit Tabellen

In Access oder Aktualisieren von Daten erstellen Sie einen Bezug auf die Back-End-Tabelle. Ersetzen von `tableName` mit dem Namen der Tabelle

```
var table = client.getTable(tableName);
```

Nachdem Sie einen Tabellenverweis haben, können Sie arbeiten mit der Tabelle weiteren:

* [Abfrage eine Tabelle](#querying)
  * [Filtern von Daten](#table-filter)
  * [Seitennavigation durch die Daten](#table-paging)
  * [Sortieren von Daten](#sorting-data)
* [Einfügen von Daten](#inserting)
* [Ändern von Daten](#modifying)
* [Löschen von Daten](#deleting)

###<a name="querying"></a>So: einen Tabellenverweis Abfragen

Nachdem Sie einen Tabellenverweis haben, können Sie es zum Abfragen von Daten auf dem Server verwenden.  Abfragen, die in einer anderen Sprache "LINQ gefällt mir" vorgenommen wurden.
Wenn Sie alle Daten aus der Tabelle zurückgegeben werden soll, verwenden Sie Folgendes ein:

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

Die Funktion Erfolg wird mit den Ergebnissen aufgerufen.   Verwenden Sie nicht `for (var i in results)` in den Erfolg ausgeführt werden können, wie die Informationen durchlaufen wird, die in die Ergebnisse einbezogen wird beim anderen Abfrage Funktionen (wie `.includeTotalCount()`) verwendet werden.

Weitere Informationen zur Syntax Abfrage finden Sie in der [Abfrage Objekt Dokumentation].

####<a name="table-filter"></a>Filtern von Daten auf dem server

Sie können eine `where` Klausel auf die Tabelle verweisen:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Sie können auch eine Funktion verwenden, die das Objekt gefiltert.  In diesem Fall die `this` Variablen zugeordnet ist, mit dem aktuellen Objekt gefiltert wird.  Im folgenden werden funktional dem vorherigen Beispiel:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

####<a name="table-paging"></a>Blättern Sie durch die Daten

Nutzen Sie die Methoden take() und skip().  Angenommen, die Tabelle in der Zeile 100 Datensätze geteilt werden soll:

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

Den `.includeTotalCount()` Methode zum Hinzufügen eines Felds TotalCount auf das Objekt Ergebnisse verwendet wird.  Das Feld TotalCount wird mit der Gesamtzahl der Datensätze ausgefüllt, der zurückgegeben wird, wenn keine Seitennavigation verwendet wird.

Klicken Sie dann können die Variable Seiten und einige Schaltflächen auf der Benutzeroberfläche Sie eine Seitenliste bereitzustellen; Verwenden Sie loadPage(), um die neuen Datensätze für jede Seite zu laden.  Sie sollten implementieren irgendeine Zwischenspeichern Geschwindigkeit den Zugriff auf die Datensätze, die bereits geladen wurden.


####<a name="sorting-data"></a>So: zurückgeben Daten sortiert

Verwenden Sie die Abfragemethoden .orderBy() oder .orderByDescending():

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Weitere Informationen auf das Objekt Abfrage finden Sie in der [Abfrage Objekt Dokumentation].

###<a name="inserting"></a>So: Einfügen von Daten

Erstellen Sie ein JavaScript-Objekt mit dem entsprechenden Datums- und rufen Sie table.insert() asynchrones auf:

```
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

Auf dem erfolgreiche einfügen wird eingefügten Elements mit zusätzlichen Felder zurückgegeben, die für synchronisieren Vorgänge erforderlich sind.  Sie sollten Ihre eigenen Cache für diese Informationen für spätere Aktualisierungen aktualisieren.

Beachten Sie, dass der Server SDK Azure Mobile Apps Node.js dynamische Schema hinsichtlich der Entwicklung unterstützt.
Bei dynamischen Schema wird das Schema der Tabelle im laufenden Betrieb, so dass Sie das Hinzufügen von Spalten zur Tabelle einfach, indem Sie sie in einer Insert angeben oder Aktualisierungsvorgang aktualisiert.  Es empfiehlt sich, dass Sie dynamische Schema vor dem Verschieben Ihrer Anwendungs zu Herstellung deaktivieren.

###<a name="modifying"></a>So: Ändern von Daten

Mit der Methode .insert() vergleichbar, Sie erstellen Sie ein Objekt aktualisieren und rufen Sie .update().  Das Objekt aktualisieren muss die ID des Datensatzes zu aktualisierenden enthalten – dies abgerufen wird, wenn Sie den Eintrag lesen oder .insert() aufrufen.

```
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

###<a name="deleting"></a>So: Löschen von Daten

Rufen Sie die .del()-Methode, um einen Datensatz zu löschen.  Ein Verweis auf eine übergeben Sie die ID:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
