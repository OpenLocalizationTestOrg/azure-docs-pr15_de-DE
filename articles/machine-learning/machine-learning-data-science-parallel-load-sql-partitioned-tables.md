<properties 
    pageTitle="Massenimport von Daten mithilfe von SQL-Partitionstabellen parallel | Microsoft Azure" 
    description="Parallele Massenimport von Daten mithilfe von SQL-Partitionstabellen" 
    services="machine-learning" 
    documentationCenter="" 
    authors="bradsev"
    manager="jhubbard" 
    editor="cgronlun" />

<tags 
    ms.service="machine-learning" 
    ms.workload="data-services" 
    ms.tgt_pltfrm="na" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.date="09/19/2016" 
    ms.author="bradsev" /> 

# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Parallele Massenimport von Daten mithilfe von SQL-Partitionstabellen

In diesem Dokument wird beschrieben, wie zum partitionierte Tabellen für fast parallel Bulk Import von Daten in einer SQL Server-Datenbank zu erstellen. Für große laden/Datenübertragung mit einer SQL­Datenbank kann Importieren von Daten in die SQL-Datenbank und den nachfolgenden Abfragen verbessert werden mithilfe von _partitionierten Tabellen und Ansichten_. 


## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Erstellen Sie eine neue Datenbank und eine Reihe von Dateigruppen

- [Erstellen einer neuen Datenbank](https://technet.microsoft.com/library/ms176061.aspx) (falls er nicht vorhanden ist)
- Fügen Sie Datenbankdateigruppen der Datenbank die annehmen partitionierten physischen Dateien hinzu

  Hinweis: Dies ist möglich mit [Datenbank erstellen](https://technet.microsoft.com/library/ms176061.aspx) , wenn neue oder [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) , wenn die Datenbank bereits vorhanden ist.

- Hinzufügen einer oder mehrerer Dateien (nach Bedarf) in jeder Datenbankdateigruppe

 > [AZURE.NOTE] Geben Sie die Ziel-Dateigruppe die Daten für diese Partition enthält und den Speicherort der Dateigruppendaten physische Datenbank Dateinamen.
 
Das folgende Beispiel erstellt eine neue Datenbank mit drei Dateigruppen als die primäre und melden Sie sich mit einer physischen Datei in den einzelnen Gruppen. Die Datenbankdateien werden in den Standardordner für SQL Server-Daten erstellt, wie in der SQL Server-Instanz konfiguriert. Weitere Informationen zu den Standardspeicherort finden Sie unter [Dateispeicherorte für Standardinstanzen und benannte Instanzen von SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);
    
    EXECUTE ('
        CREATE DATABASE <database_name>
        ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
        FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
        FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
        FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
        LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')
    
## <a name="create-a-partitioned-table"></a>Erstellen Sie eine partitionierte Tabelle

Erstellen Sie gemäß dem Datenschema, die im vorherigen Schritt erstellten Datenbankdateigruppen zugeordnet partitionierte Tabellen. Wenn Daten Bulk zum partitionierten Tabellen importiert werden, werden Datensätze wie unten beschrieben auf die Dateigruppen gemäß einem Partitionsschema verteilt.

**Um eine Partitionstabelle zu erstellen, müssen Sie:**

- [Erstellen einer Partitionsfunktion](https://msdn.microsoft.com/library/ms187802.aspx) die definiert den Bereich der Werte/Grenzen, die in jeder einzelnen Partitionstabelle, z. B. eingeschlossen werden, um Partitionen nach Monat zu begrenzen (einige\_Datetime\_Feld) im Jahr 2013:

        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )

- [Erstellen einer Partitionsschema](https://msdn.microsoft.com/library/ms179854.aspx) der jeweiligen Bereich Partition in der Partitionsfunktion eine physische Dateigruppe, z. B. zugeordnet ist:

        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )

  Tipp: Führen Sie die folgende Abfrage aus, um die Bereiche wirksam in jede Partition entsprechend der Funktion-Schema zu überprüfen:

        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>

- [Erstellen der partitionierten Tabelle](https://msdn.microsoft.com/library/ms174979.aspx) (s) nach Ihrer Datenschema und geben Sie das Partition Schema und Einschränkung Feld verwendet, um die Tabelle, z. B. partitionieren:

        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Weitere Informationen finden Sie unter [Erstellen von partitionierten Tabellen und Indizes](https://msdn.microsoft.com/library/ms188730.aspx).


## <a name="bulk-import-the-data-for-each-individual-partition-table"></a>Massen importieren Sie die Daten für jede einzelne Partitionstabelle

- Sie können BCP, BULK INSERT oder anderen Methoden wie [SQL Server-Assistenten für die Migration](http://sqlazuremw.codeplex.com/)verwenden. Im Beispiel wird die BCP-Methode verwendet.

- [Ändern Sie die Datenbank](https://msdn.microsoft.com/library/bb522682.aspx) , zum Ändern der Protokollierung von Transaktionen Schema in BULK_LOGGED minimieren Aufwand für die Protokollierung, z. B.:

        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED

- Zum Laden von Daten zu beschleunigen, starten Sie die Import Mengenoperationen parallel. Tipps auf Verwaltungsebene Bulk Import großer Datenmengen in SQL Server-Datenbanken finden Sie unter [1 TB in weniger als 1 Stunde geladen werden](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Das folgende PowerShell-Skript ist ein Beispiel für Paralleles Laden von Daten mithilfe von BCP.

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0
    
    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>
       
    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"
   
    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir
      
    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }
    
    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }
    
    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }
    
    Get-Job
    
    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a>Erstellen von Indizes zur Optimierung von Verknüpfungen und Leistung von Abfragen

- Wenn Sie für die Modellierung Daten aus mehreren Tabellen extrahieren soll, erstellen Sie Indizes für die Verknüpfung Schlüssel zur Verbesserung der Leistung teilnehmen.

- [Erstellen von Indizes](https://technet.microsoft.com/library/ms188783.aspx) (gruppierten oder nicht gruppierten) Zielgruppenadressierung derselben Dateigruppe für jede Partition, z. B. für:

        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
oder,

        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)

 > [AZURE.NOTE] Sie können auswählen, die Indizes vor Massenimport von Daten zu erstellen. Laden der Daten wird vor dem Bulk Import indexerstellung verlangsamen.


## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Erweiterte Analytics Prozess und die Technologie im Beispiel für eine Aktion

Ein Beispiel für die End-to-End-Exemplarische Vorgehensweise mithilfe des Cortana Analytics-Prozesses mit einem öffentlichen Dataset, finden Sie unter [Cortana Analytics Prozess in der Praxis: Verwenden von SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
 
