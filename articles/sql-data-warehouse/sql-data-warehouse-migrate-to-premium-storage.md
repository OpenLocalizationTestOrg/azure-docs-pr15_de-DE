<properties
   pageTitle="Migrieren von Ihrer vorhandenen Azure SQL-Data Warehouse zu Premium Speicher | Microsoft Azure"
   description="Anweisungen für die Migration ein vorhandenes SQL Data Warehouse zu Premium-Speicher"
   services="sql-data-warehouse"
   documentationCenter="NA"
   authors="happynicolle"
   manager="barbkess"
   editor=""/>

<tags
   ms.service="sql-data-warehouse"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="data-services"
   ms.date="08/24/2016"
   ms.author="nicw;barbkess;sonyama"/>

# <a name="migration-to-premium-storage-details"></a>Migration Premium Speicher Details
SQL Data Warehouse eingeführt zuletzt [Premium-Speicher für höhere Leistung Vorhersagbarkeit][].  Wir können nun zum Migrieren von vorhandenen Daten Lager aktuell auf Standard-Speicher zu Premium-Speicher.  Lesen Sie weiter für Weitere Informationen darüber, wann und wie automatische Migration auftreten, und wie Self migrieren, wenn Sie es vorziehen, können Sie steuern, wann der Ausfall auftritt.

Wenn Sie mehr als ein Data Warehouse haben, verwenden Sie den [Zeitplan für die automatische Migration][] unten, um festzustellen, wann er ebenfalls migriert werden.

## <a name="determine-storage-type"></a>Ermitteln Sie Speicherplatz Typ
Wenn Sie eine DW vor den Datumsangaben unten erstellt haben, verwenden Sie derzeit Standard-Speicher.  Jedes Data Warehouse Standard Speichermenge, die automatische Migration unterliegt weist eine Mitteilung am oberen Rand der Data Warehouse Blade im [Azure-Portal][] an, die besagt "*ein späteres Upgrade auf Premium-Speicher wird einen Ausfall erforderlich.  Erfahren Sie mehr ->*. "

| **Region**          | **DW vor diesem Datum erstellt**   |
| :------------------ | :-------------------------------- |
| Australien OST      | Premium Speicher noch nicht verfügbar |
| Australien oder | 5 August 2016                    |
| Brasilien Süd        | 5 August 2016                    |
| Kanada Central      | 25 Mai 2016                      |
| Kanada OST         | 26 Mai 2016                      |
| USA – zentral          | 26 Mai 2016                      |
| China OST          | Premium Speicher noch nicht verfügbar |
| Nord-China         | Premium Speicher noch nicht verfügbar |
| Ostasien           | 25 Mai 2016                      |
| Ostasiatische US             | 26 Mai 2016                      |
| Ostasiatische US2            | 27 Mai 2016                      |
| Indien Central       | 27 Mai 2016                      |
| Indien Süd         | 26 Mai 2016                      |
| Indien "Westen"          | Premium Speicher noch nicht verfügbar |
| Japan OST          | 5 August 2016                    |
| Japan "Westen"          | Premium Speicher noch nicht verfügbar |
| Nord-zentralen US    | Premium Speicher noch nicht verfügbar |
| North Europa        | 5 August 2016                    |
| Süd zentralen US    | 27 Mai 2016                      |
| Oder Asien      | 24 Mai 2016                      |
| Westen Europa         | 25 Mai 2016                      |
| USA – zentral "Westen"     | 26 August 2016                   |
| Westen US             | 26 Mai 2016                      |
| Westen US2            | 26 August 2016                   |

## <a name="automatic-migration-details"></a>Details zur automatischen migration
Standardmäßig werden wir Ihre Datenbank für Sie während 6 Uhr und 6: 00 in die lokale Zeit des Bereichs während des [automatischen Migration Terminplan][] unter migrieren.  Ihre vorhandene Data Warehouse kann während der Migration nicht verwendet werden.  Wir davon ausgehen, dass es sich bei die Migration ungefähr eine Stunde pro TB Speicher pro Data Warehouse dauert.  Wir werden auch Stellen Sie sicher, dass Sie während eines Teils der automatischen Migration nicht belastet werden.

> [AZURE.NOTE] Verwenden Sie Ihre vorhandene Data Warehouse während der Migration ist nicht möglich.  Nach Abschluss die Migration werden Ihre Data Warehouse wieder online.

Die folgenden Details sind Schritte, dass Microsoft in Ihrem Auftrag zum Abschließen der Migrations sehr und sind keine Einbeziehung von Ihrer Seite erforderlich.  Stellen Sie in diesem Beispiel vor Ihrer vorhandenen DW auf Standard-Speicher aktuell ist mit der Bezeichnung "MyDW."

1.  Microsoft benennt "MyDW", "MyDW_DO_NOT_USE_ [Timestamp]"
2.  Microsoft hält "MyDW_DO_NOT_USE_ [Timestamp]."  Während dieses Zeitraums wird eine Sicherungskopie übernommen.  Mehrere anhalten/Lebensläufe möglicherweise angezeigt werden, wenn wir Probleme dabei auftreten.
3.  Microsoft erstellt eine neue DW mit dem Namen "MyDW" Premium Speichermenge aus der Sicherung in Schritt 2 geöffnet.  "MyDW" wird erst nach Abschluss der Wiederherstellung angezeigt.
4.  Sobald die Wiederherstellung abgeschlossen ist, gibt "MyDW" auf die gleiche DWUs und angehalten oder aktiven Zustand, die zuvor der Migration.
5.  Nach Abschluss die Migration löscht Microsoft "MyDW_DO_NOT_USE_ [Timestamp]"
    
> [AZURE.NOTE] Diese Einstellungen werden nicht als Teil der Migration übertragen:
> 
>   -  Überwachung Ebene der Datenbank muss wieder aktiviert werden
>   -  Firewall-Regeln auf der Ebene der **Datenbank** haben, werden müssen.  Firewall-Regeln Ebene des **Servers** sind nicht betroffen werden.

### <a name="automatic-migration-schedule"></a>Automatische Migration Terminplan
Automatische Migration auftreten von 6 Uhr – 6 Uhr (lokale Zeit pro Region) während der folgenden einem Dienstausfall Terminplan.

| **Region**          | **Geschätzte Anfangstermin**     | **Geschätztes Enddatum**       |
| :------------------ | :--------------------------- | :--------------------------- |
| Australien OST      | Noch bestimmt nicht           | Noch bestimmt nicht           |
| Australien oder | 10 August 2016              | 24 August 2016              |
| Brasilien Süd        | 10 August 2016              | 24 August 2016              |
| Kanada Central      | 23 Juni 2016                | 1 Juli 2016                 |
| Kanada OST         | 23 Juni 2016                | 1 Juli 2016                 |
| USA – zentral          | 23 Juni 2016                | 4 Juli 2016                 |
| China OST          | Noch bestimmt nicht           | Noch bestimmt nicht           |
| Nord-China         | Noch bestimmt nicht           | Noch bestimmt nicht           |
| Ostasien           | 23 Juni 2016                | 1 Juli 2016                 |
| Ostasiatische US             | 23 Juni 2016                | 11 Juli 2016                |
| Ostasiatische US2            | 23 Juni 2016                | 8 Juli 2016                 |
| Indien Central       | 23 Juni 2016                | 1 Juli 2016                 |
| Indien Süd         | 23 Juni 2016                | 1 Juli 2016                 |
| Indien "Westen"          | Noch bestimmt nicht           | Noch bestimmt nicht           |
| Japan OST          | 10 August 2016              | 24 August 2016              |
| Japan "Westen"          | Noch bestimmt nicht           | Noch bestimmt nicht           |
| Nord-zentralen US    | Noch bestimmt nicht           | Noch bestimmt nicht           |
| North Europa        | 10 August 2016              | 31 August 2016              |
| Süd zentralen US    | 23 Juni 2016                | 2 Juli 2016                 |
| Oder Asien      | 23 Juni 2016                | 1 Juli 2016                 |
| Westen Europa         | 23 Juni 2016                | 8 Juli 2016                 |
| USA – zentral "Westen"     | 14 August 2016              | 31 August 2016              |
| Westen US             | 23 Juni 2016                | 7 Juli 2016                 |
| Westen US2            | 14 August 2016              | 31 August 2016              |

## <a name="self-migration-to-premium-storage"></a>Self-Migration zu Premium-Speicher
Wenn Sie möchten, können Sie steuern, wann Ihre Ausfallzeiten ausgeführt wird, können Sie die folgenden Schritte aus, ein vorhandenes Data Warehouse auf Standard-Speicher auf Premium Speicher migrieren.  Wenn Sie Self migrieren, muss Abschluss die Migration Self vor Beginn der automatische Migration in diesem Bereich der automatischen Migration einen Konflikt verursachen vermeiden (Siehe den [Zeitplan für die automatische Migration][]).

### <a name="self-migration-instructions"></a>Self-Migration Anweisungen
Wenn Sie Ihre Ausfallzeiten steuern möchten, können Sie Ihr Data Warehouse mithilfe von Sicherung und Wiederherstellung Self migrieren.  Ungefähr eine Stunde pro TB Speicherplatz pro DW ausführen, wird der Wiederherstellungsteil der Migration erwartet.  Wenn Sie denselben Namen nach Abschluss der Migration zu beibehalten möchten, führen Sie die Schritte für die [Schritte zum Umbenennen während der Migration][]. 

1.  [Anhalten][] der DW nimmt eine automatische Sicherung
2.  [Wiederherstellen][] von der letzten snapshot
3.  Löschen Sie Ihre vorhandene DW Standard Speichermenge an. **Wenn Sie diesen Schritt nicht tun, werden Sie für beide DWs Rechnung gestellt.**

> [AZURE.NOTE] Diese Einstellungen werden nicht als Teil der Migration übertragen:
> 
>   -  Überwachung Ebene der Datenbank muss wieder aktiviert werden
>   -  Firewall-Regeln auf der Ebene der **Datenbank** haben, werden müssen.  Firewall-Regeln auf der Ebene **Server** sind nicht betroffen werden.

#### <a name="optional-steps-to-rename-during-migration"></a>Optional: Schritte zum Umbenennen während der migration 
Zwei Datenbanken auf dem gleichen logischen Server aufweisen nicht den gleichen Namen. SQL Data Warehouse unterstützt jetzt die Möglichkeit, eine DW umbenennen.

Stellen Sie in diesem Beispiel vor Ihrer vorhandenen DW auf Standard-Speicher aktuell ist mit der Bezeichnung "MyDW."

1.  Umbenennen von "MyDW" mit dem Befehl ALTER DATABASE, dass zufrieden sind folgt auf bestimmte "MyDW_BeforeMigration."  Dieser Befehl bricht alle vorhandene Transaktionen und in der master-Datenbank erfolgreich vorgenommen werden.
```
ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
```
2.  [Pause][] "MyDW_BeforeMigration" nimmt eine automatische Sicherung
3.  [Wiederherstellen][] von der letzten snapshot eine neue Datenbank mit dem Namen, die Sie verwendet haben (ex: "MyDW")
4.  Löschen Sie "MyDW_BeforeMigration" ein.  **Wenn Sie diesen Schritt nicht tun, werden Sie für beide DWs Rechnung gestellt.**

> [AZURE.NOTE] Diese Einstellungen werden nicht als Teil der Migration übertragen:
> 
>   -  Überwachung Ebene der Datenbank muss wieder aktiviert werden
>   -  Firewall-Regeln auf der Ebene der **Datenbank** haben, werden müssen.  Firewall-Regeln auf der Ebene **Server** sind nicht betroffen werden.

## <a name="next-steps"></a>Nächste Schritte
Klicken Sie mit der Änderung Premium Speicher haben wir auch die Anzahl der Blob-Datenbankdateien in die zugrunde liegende Architektur des Data Warehouse erhöht.  Um die Leistungsvorteile von diese Änderung maximieren, empfehlen wir, dass Sie Ihre mithilfe des folgenden Skripts gruppierte Columnstore Indizes neu zu erstellen.  Das folgende Skript funktioniert, wenn Sie einige der vorhandenen Daten zu den zusätzlichen Blobs erzwingen.  Wenn Sie keine Maßnahmen ergreifen, werden die Daten über einen Zeitraum natürlich verteilen, während Sie weitere Daten in der Data Warehouse-Tabellen zu laden.

**Erforderlichen Komponenten:**

1.  Datawarehouse sollte mit 1.000 DWUs oder höher ausgeführt werden (siehe [Skalieren berechnen Power][])
2.  Ausführen des Skripts Benutzer sollten in die [Rolle des Mediumrc][] oder höher
    1.  Wenn einen Benutzer diese Rolle hinzufügen möchten, führen Sie Folgendes aus: 
        1.  ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create Table to control Index Rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select 
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from 
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go
 
--------------------------------------------------------------------------------
-- Step 2: Execute Index Rebuilds.  If script fails, the below can be rerun to restart where last left off
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Cleanup Table Created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Wenn Sie Probleme mit Ihrem Data Warehouse, [Erstellen Sie ein Ticket Support][] und Bezug "Migration zu Premium Speicher" als eine mögliche Ursache auftreten.

<!--Image references-->

<!--Article references-->
[Automatische Migration Terminplan]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[Erstellen einer Support-ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md/#pause-compute
[Stellen Sie wieder her]: sql-data-warehouse-restore-database-portal.md
[Schritte zum Umbenennen während der migration]: #optional-steps-to-rename-during-migration
[Maßstab berechnen power]: sql-data-warehouse-manage-compute-portal/#scale-compute-power
[Mediumrc Rolle]: sql-data-warehouse-develop-concurrency/#workload-management

<!--MSDN references-->


<!--Other Web references-->
[Premium-Speicher für höhere Leistung Vorhersagbarkeit]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure-Portal]: https://portal.azure.com
