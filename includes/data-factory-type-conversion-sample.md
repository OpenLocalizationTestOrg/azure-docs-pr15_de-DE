### <a name="type-conversion-sample"></a>Typ Konvertierung Stichprobe
Im folgende Beispiel ist für das Kopieren von Daten von einem Blob in SQL Azure mit Konvertieren des Datentyps.

Nehmen Sie an das Blob-Dataset im CSV-Format ist und 3 Spalten enthält. Eine von ihnen ist eine Datetime-Spalte mit einem benutzerdefinierten Datetime-Format mit abgekürzten Französisch Namen für den Tag der Woche aus.

Definieren Sie das Dataset Blob-Quelle wie folgt zusammen mit Definitionen für die Spalten.

    {
        "name": "AzureBlobTypeSystemInput",
        "properties":
        {
             "structure": 
              [
                    { "name": "userid", "type": "Int64"},
                    { "name": "name", "type": "String"},
                    { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
              ],
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/myfolder",
                "fileName":"myfile.csv",
                "format":
                {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "external": true,
            "availability":
            {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }

Ausgehend von den SQL-Code würde zu .NET-Zuordnungstabelle über Sie die SQL Azure-Tabelle mit dem folgenden Schema definieren.

| Spaltenname | SQL-Datentyp |
| ----------- | -------- |
| Benutzer-ID | bigint |
| Namen | Text |
| LastLoginDate | "DateTime" |

Als Nächstes werden Sie wie folgt das SQL Azure-Dataset definieren. Hinweis: Sie müssen nicht mit Informationen zum Abschnitt "Struktur" angeben, da die Informationen im zugrunde liegenden Datenspeicher bereits angegeben ist.

    {
        "name": "AzureSQLOutput",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "MyTable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }

In diesem Fall werden Daten Factory automatisch den Typ ausführen, einschließlich Datetime-Feld mit den benutzerdefinierten Datetime Konvertierungen formatieren mithilfe von der Kultur Französisch-Französisch beim Verschieben von Daten aus Blob in SQL Azure.


