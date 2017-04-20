<properties
   pageTitle="Abfrage Azure SQL-Data Warehouse (Sqlcmd) | Microsoft Azure"
   description="Verwenden von Abfragen Azure SQL-Data Warehouse mit der Befehlszeilenprogramms Sqlcmd."
   services="sql-data-warehouse"
   documentationCenter="NA"
   authors="sonyam"
   manager="barbkess"
   editor=""/>

<tags
   ms.service="sql-data-warehouse"
   ms.devlang="NA"
   ms.topic="get-started-article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-services"
   ms.date="09/06/2016"
   ms.author="barbkess;sonyama"/>

# <a name="query-azure-sql-data-warehouse-sqlcmd"></a>Abfrage Azure SQL Data Warehouse (Sqlcmd)

> [AZURE.SELECTOR]
- [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
- [Learning Azure-Computern](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
- [Visual Studio](sql-data-warehouse-query-visual-studio.md)
- [Sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 

Diese exemplarische Vorgehensweise verwendet das Befehlszeilendienstprogramm [Sqlcmd][] einer Azure SQL-Data Warehouse Abfragen an.  

## <a name="1-connect"></a>1. Verbinden von

Erste Schritte mit [Sqlcmd][], öffnen Sie die Befehlszeile, und geben Sie **Sqlcmd** gefolgt von der Verbindungszeichenfolge für die Data Warehouse SQL-Datenbank. Die Verbindungszeichenfolge erfordert die folgenden Parameter:

+ **Server (– S):** Server im Formular `<`Servername`>`. database.windows.net
+ **Datenbank (-d):** Name der Datenbank.
+ **Aktivieren Bezeichnern (-ich):** Bezeichner in Anführungszeichen müssen in Verbindung mit einer Instanz von SQL Data Warehouse aktiviert sein.

Wenn SQL Server-Authentifizierung verwenden möchten, müssen Sie die Benutzername und Kennwort Parameter hinzufügen:

+ **Benutzer (-U):** Server-Benutzer in das Formular `<`Benutzer`>`
+ **Kennwort (-P):** Kennwort des Benutzers.

Die Verbindungszeichenfolge könnte beispielsweise wie folgt aussehen:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Um Azure Active Directory-integrierte Authentifizierung verwenden, müssen Sie die Azure Active Directory-Parameter hinzufügen:

+ **Azure-Active Directory-Authentifizierung (-G):** Azure Active Directory für die Authentifizierung verwenden

Die Verbindungszeichenfolge könnte beispielsweise wie folgt aussehen:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [AZURE.NOTE] Sie müssen aktivieren [Azure-Active Directory-Authentifizierung](sql-data-warehouse-authentication.md) für die Authentifizierung mithilfe von Active Directory.

## <a name="2-query"></a>2. Abfrage

Nachdem die Verbindung können Sie alle unterstützten Transact-SQL-Anweisungen für die Instanz ausgeben.  In diesem Beispiel werden Abfragen im interaktiven Modus übermittelt.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Diesen nächsten Beispielen wird gezeigt, wie Sie Ihre Abfragen in Stapelverarbeitungsmodus mithilfe der F - Option oder Ihrer SQL zu Sqlcmd Rohrleitungsplan ausgeführt werden können.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie [Sqlcmd Dokumentation][Sqlcmd] für Weitere Informationen zu den Details zu den verfügbaren Optionen in Sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[Sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
