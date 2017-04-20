<properties
    pageTitle="Team von Daten Science in der Praxis: Verwenden von SQL Server | Microsoft Azure"
    description="Erweiterte Analytics Prozess und-Technologie in Aktion"  
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
    ms.author="fashah;bradsev"/>


# <a name="the-team-data-science-process-in-action-using-sql-server"></a>Team von Daten Science in der Praxis: Verwenden von SQL Server

In diesem Lernprogramm Sie exemplarischen Vorgehensweise erstellen und Bereitstellen von mithilfe von SQL Server und einer öffentlich zugänglichen Dataset-- [NYC Taxi Reisen](http://www.andresmh.com/nyctaxitrips/) Dataset ein Modell für den Computer lernen. Die Prozedur folgt einen Standarddaten Science-Workflow: Aufnahme und Durchsuchen der Daten, Engineer Features vereinfachen Learning, und klicken Sie dann erstellen und Bereitstellen von einem Modell.


## <a name="dataset"></a>NYC Taxi Reisen Datasetbeschreibung

Die NYC Taxi Reise Daten sind etwa 20GB komprimierter CSV-Dateien (~ 48GB dekomprimiert), mit den einzelnen Reisen 173 Millionen und die Flugpreise für jede Reise bezahlt. Jeder Reise Datensatz enthält die Pickup- und Ladengeschäft Ort und Uhrzeit, anonymes Hack (Treiber) Anzahl Lizenzen und Medallion (eindeutige Id des Taxi) an. Die Daten werden alle Reisen im Jahr 2013 behandelt und für jeden Monat in den folgenden zwei Datasets bereitgestellt werden:

1. Trip_data CSV enthält Reise Details wie etwa die Anzahl der Reisenden, Pickup- und Dropoff Punkt, Reise Dauer und Reise Länge. Es folgen einige Beispieldatensätze:

        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868

2. Die 'Trip_fare' enthält die CSV-Datei Details für jeden Reise wie Zahlungstyp, Fahrpreis Betrag, Zusatz und steuern, Tipps und Gebühren, bezahlt Fahrpreises und den Gesamtbetrag. Es folgen einige Beispieldatensätze:

        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Mit dem eindeutigen Schlüssel Reise beitreten\_Daten und Reise\_Fahrpreis besteht aus den Feldern: Medallion, Hack\_Lizenz und Pickup-\_Datetime.

## <a name="mltasks"></a>Beispiele für Vorhersage Aufgaben

Wir werden drei Vorhersage Probleme basierend auf Formulieren der *Tipp\_Betrag*, nämlich:

1. Binäre Klassifizierung: vorhergesagt, unabhängig davon, ob ein Tipp für eine Reise, d. h. bezahlt wurde eine *Tipp\_Betrag* , die größer ist als $0 eine positive Beispiel ist, während er sich eine *Tipp\_Betrag* $ 0 ist ein Beispiel für negative.

2. Multiclass Klassifizierung: vorhergesagt den Bereich der QuickInfo für die Reise bezahlt. Wir teilen der *Tipp\_Betrag* in fünf Fächer oder Klassen:

        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20

3. Regressionsformel Aufgabe: die Menge der QuickInfo für eine Reise bezahlt vorhergesagt.  


## <a name="setup"></a>Einrichten der Azure-Daten Science Umgebung für erweiterte analytics

Wie Sie sehen aus Anleitung zu [Ihrer Umgebung planen](machine-learning-data-science-plan-your-environment.md) können, gibt es mehrere Optionen NYC Taxi Reisen Datasets in Azure entwickelt:

- Arbeiten Sie mit den Daten in Azure Blobs dann Modell Kennenlernen der Azure-Computer
- Laden Sie die Daten in einer SQL Server-Datenbank und Modell Kennenlernen der Azure-Computer

In diesem Lernprogramm wird wir parallel Massenimport von Daten zu einer SQL Server, Durchsuchen von Daten, Feature veranschaulichen engineering und nach unten Sampling mithilfe von SQL Server Management Studio als auch IPython Notizbuch verwenden. [Beispielskripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) und [IPython Notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) sind in GitHub freigegeben. Ein Beispiel IPython Notizbuch zum Arbeiten mit den Daten in Azure Blobs steht auch am selben Speicherort.

So richten Ihre Umgebung Azure Daten Science

1. [Erstellen eines Speicherkontos](../storage/storage-create-storage-account.md)

2. [Erstellen einer Azure-Computer Learning-Arbeitsbereichs](machine-learning-create-workspace.md)

3. [Bereitstellung einer Daten Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), die als SQL Server sowie einen Notizbuch IPython Server dienen wird.

    > [AZURE.NOTE] Die Beispielskripts und IPython Notebooks werden zum virtuellen Computer Science Daten während des Installationsvorgangs heruntergeladen. Wenn das VM-Skript nach der Installation abgeschlossen ist, werden die Beispiele in Ihrer VM-Dokumentbibliothek:  
    > - Skripts zum Beispiel:`C:\Users\<user_name>\Documents\Data Science Scripts`  
    > - Beispiel IPython Notebooks:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
    > wobei `<user_name>` Ihrer VM Windows-Benutzername ist. Wir bezieht sich auf die Beispiel-Ordner als **Beispielskripts** und **Beispiel IPython Notebooks**.


Basierend auf die Größe des Datasets, Datenquellen-Speicherort und die ausgewählte(n) Azure-Umgebung, in diesem Szenario ähnelt [Szenario \#5: große Datasets in einem lokalen Dateien, SQL Server auf virtuellen Azure-Computer als Ziel](../machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Abrufen der Daten von öffentlichen Quelle

Wenn das Dataset [NYC Taxi Reisen](http://www.andresmh.com/nyctaxitrips/) aus ihrem öffentlichen Speicherort erhalten möchten, können Sie eine der in [Verschieben von Daten zu und von Azure BLOB-Speicher](machine-learning-data-science-move-azure-blob.md) beschriebenen Methoden zum Kopieren von Daten auf den neuen virtuellen Computer verwenden.

So kopieren Sie die Daten mit AzCopy:

1. Melden Sie sich an dem virtuellen Computer (VM)

2. Erstellen Sie ein neues Verzeichnis, in dem VM-Datenträger (Hinweis: Verwenden Sie nicht dem temporären Datenträger mit dem virtuellen Computer als einen Datenträger enthalten).

3. Führen Sie die folgende Azcopy-Befehlszeile, und Ersetzen Sie < Path_to_data_folder > durch Ihre Datenordner im (2) erstellt in einem Eingabeaufforderungsfenster aus:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

    Nach Abschluss der AzCopy ZIP insgesamt 24 CSV-Dateien (12 für Reise\_Daten und 12 für Reise\_Fahrpreis) sollte in den Datenordner sein.

4. Extrahieren Sie die heruntergeladenen Dateien. Notieren Sie den Ordner, in denen die nicht komprimierten Dateien befinden. In diesem Ordner werden als bezeichnet die < Pfad\_auf\_Daten\_Dateien\>.

## <a name="dbload"></a>Bulk Import von Daten in SQL Server-Datenbank

Mithilfe von _partitionierten Tabellen und Ansichten_, kann die Leistung des laden/übertragen großer Datenmengen mit einer SQL-Datenbank und nachfolgende Abfragen verbessert werden. In diesem Abschnitt führen wir die durch die Anweisungen in [Parallelen Bulk Data Import mithilfe von SQL Partitionstabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) zum Erstellen einer neuen Datenbank, und Laden Sie die Daten in partitionierten Tabellen parallel beschrieben.

1. Während Ihrer VM angemeldet haben, starten Sie **SQL Server Management Studio**.

2. Verbindung mit Windows-Authentifizierung.

    ![Verbinden SSMS][12]

3. Wenn Sie noch nicht den SQL Server-Authentifizierungsmodus geändert und einen neuen SQL-Benutzer erstellt haben, öffnen Sie die Skriptdatei, die mit dem Namen **Ändern\_auth.sql** im Ordner " **Beispielskripts** ". Ändern Sie den standardmäßigen Benutzernamen und das Kennwort ein. Klicken Sie auf **! Führen Sie** in der Symbolleiste, um das Skript auszuführen.

    ![Führen Sie Skript][13]

4. Stellen Sie sicher, und/oder ändern Sie die SQL Server Datenbank- und Protokolldateien Standardordner um sicherzustellen, die neu erstellten Datenbanken in einem Datenträger gespeichert werden. Das SQL Server VM Bild für Data Warehousing Lasten optimiert ist ist vorkonfiguriert Daten- und Protokolldateien Datenträger. Wenn Ihre VM einen Datenträger nicht enthalten und Sie neuen virtuellen Festplatten während des Installationsvorgangs VM hinzugefügt haben, ändern Sie den Standardordner wie folgt:

    - Mit der rechten Maustaste im linken Bereich der Name der SQL Server, und klicken Sie auf **Eigenschaften**.

        ![SQL Server-Eigenschaften][14]

    - Wählen Sie **Datenbank** aus der Liste **Wählen Sie eine Seite** nach links.

    - Stellen Sie sicher und/oder ändern Sie die **Standardspeicherorte für Datenbank** in den **Datenträger** Speicherorten Ihrer Wahl. Dies ist, in denen neue Datenbanken befinden, wenn mit den Standardeinstellungen für den Standort erstellt.

        ![Standardeinstellungen für SQL-Datenbank][15]  

5. So erstellen Sie eine neue Datenbank und eine Reihe von Dateigruppen zum partitionierten Tabellen halten, öffnen Sie das Beispielskript **Erstellen\_Db\_default.sql**. Das Skript erstellt eine neue Datenbank mit dem Namen **TaxiNYC** und 12 Dateigruppen in den Standardspeicherort der Daten. Jede Dateigruppe enthält einen Monat Reise\_Daten und Reise\_Ergebnisse so ausfallen Daten. Ändern Sie bei Bedarf den Datenbanknamen. Klicken Sie auf **! Führen Sie** zum Ausführen des Skripts.

6. Im nächsten Schritt erstellen Sie zwei Partitionstabellen, eine für die Reise\_Daten und eine andere für die Reise\_Fahrpreis. Öffnen Sie das Beispielskript **Erstellen\_partitionierten\_speichern**, dem wird:

    - Erstellen Sie eine Partitionsfunktion, um die Daten nach Monat teilen.
    - Erstellen Sie ein Partitionsschema, um jeden Monat Daten zu einer anderen Dateigruppe zuzuordnen.
    - Erstellen von zwei partitionierten Tabellen, die das Partitionsschema zugeordnet sind: **Nyctaxi\_Reise** enthält die Reise\_Daten und **Nyctaxi\_Fahrpreis** enthält die Reise\_Ergebnisse so ausfallen Daten.

    Klicken Sie auf **! Führen Sie** führen Sie das Skript und die partitionierten Tabellen erstellen.

7. In den Ordner **Beispielskripts** sind zwei PowerShell-Skriptbeispiele zur Verfügung gestellt, die veranschaulichen, dass die parallele Massen von Daten in SQL Server-Tabellen importiert.

    - **Bcp\_parallel\_generic.ps1** ist ein allgemeines Skript zum parallelen Bulk Import-Daten in eine Tabelle. Ändern Sie dieses Skript, um die Eingabe- und Ziel-Variablen festzulegen, wie in den Kommentarzeilen in das Skript angegeben.
    - **Bcp\_parallel\_nyctaxi.ps1** ist eine vorkonfigurierte Version des generischen Skripts und zum Laden der beiden Tabellen für die Daten NYC Taxi Reisen zu verwendet werden.  

8. Mit der rechten Maustaste die **Bcp\_parallel\_nyctaxi.ps1** script Name, und klicken Sie auf **Bearbeiten** , um es in PowerShell zu öffnen. Die vordefinierten Variablen überprüfen und ändern Sie Ihre ausgewählten Datenbanknamen, Eingabedaten Ordner, Log Zielordner und Pfade zu den Beispiel-Format-Dateien **nyctaxi_trip.xml** und **Nyctaxi\_fare.xml** (im Ordner **Beispielskripts** bereitgestellt).

    ![Massen Importieren von Daten][16]

    Sie können auch den Authentifizierungsmodus auswählen, Standard ist die Windows-Authentifizierung. Klicken Sie auf den grünen Pfeil in der Symbolleiste auf ausführen. Das Skript startet 24 Bulk Importvorgänge in parallel, 12 für jede partitionierte Tabelle. Sie können die Daten in Arbeit Importieren Öffnen den SQL Server-Standard-Datenordner wie oben überwachen.

9. PowerShell-Skript-Berichte der Start- und Endzeiten. Die Endzeit wird gemeldet, wenn alle vollständigen Imports Massen. Kontrollkästchen Log Zielordner um sicherzustellen, dass das gleichzeitige importiert wurden erfolgreich ist, d. h., keine Fehler im Protokoll Zielordner gemeldet.

10. Die Datenbank ist nun bereit für das Durchsuchen von Feature Engineering und anderer Vorgänge wie gewünscht. Da die Tabellen proaktiver partitioniert werden die **Pickup\_Datetime** Feld Abfragen die umfassen **Pickup\_Datetime** Bedingungen in der **WHERE** -Klausel werden das Partitionsschema Kommunikationsmittel.

11. Verwenden Sie in **SQL Server Management Studio**das bereitgestellten Beispielskript **Beispiel\_queries.sql**. Wenn keines der Beispielabfragen ausgeführt werden soll, markieren Sie die Abfragezeilen, und klicken Sie auf **! Führen Sie** in der Symbolleiste.

12. Die NYC Taxi Reisen Daten werden in zwei getrennten Tabellen geladen. Zur Verbesserung der Join-Operationen, wird empfohlen, die Tabellen zu indizieren. Das Beispielskript **Erstellen\_partitionierten\_index.sql** partitionierten Indizes auf zusammengesetzte Join-Schlüssels erstellt **Medallion, Hack\_Lizenz und Pickup-\_Datetime**.

## <a name="dbexplore"></a>Durchsuchen von Daten und Feature Engineering in SQLServer

In diesem Abschnitt werden wir Durchsuchen von Daten und Feature Generation führen Sie durch Ausführen von SQL-Abfragen direkt in der zuvor erstellten SQL Server-Datenbank von **SQL Server Management Studio** . Ein Beispielskript, mit dem Namen **Beispiel\_queries.sql** in den Ordner **Beispielskripts** bereitgestellt wird. Ändern Sie das Skript zum Ändern des Datenbanknamens aus, wenn vom Standardwert unterscheidet: **TaxiNYC**.

In dieser Übung wird Folgendes beschrieben:

- Verbinden Sie mit **SQL Server Management Studio** mit entweder Windows-Authentifizierung oder SQL-Authentifizierung und den SQL-Anmeldenamen und das Kennwort ein.
- Verwenden Sie die Verteilung der einige Felder in unterschiedlichen Zeitfenster Daten.
- Untersuchen Sie die Qualität der Daten der Länge und Breite Felder.
- Generieren von binären und multiclass Klassifizierung Bezeichnungen basierend auf der **Tipp\_Betrag**.
- Generieren von Features und Reise Abstände Compute/vergleichen.
- Verbinden Sie zwei Tabellen und Extrahieren einer Stichprobe, die zum Erstellen von Modellen verwendet wird.

Wenn Sie zur Einführung in Azure Computer fortfahren bereit sind, können Sie:  

1. Speichern Sie die endgültige SQL-Abfrage zum Extrahieren und die Beispieldaten und die Abfrage direkt in einem [Importierten Daten] kopieren und Einfügen[ import-data] Modul in Azure-Computer lernen, oder
2. Beibehalten der aufgenommenen und Engineering-Daten, die Sie für das Modell in eine neue Datenbanktabelle erstellen und Verwenden der neuen Tabelle in die [Daten importieren] möchten[ import-data] Modul in Azure-Computer lernen.

In diesem Abschnitt werden wir die letzte Abfrage zum Extrahieren und die Beispieldaten gespeichert. Die zweite Methode ist in den Abschnitt [Durchsuchen von Daten und Engineering Feature in IPython Notizbuch](#ipnb) veranschaulicht.

Für eine schnelle Überprüfung der Anzahl von Zeilen und Spalten in den Tabellen weiter oben Massenimport parallel aufgefüllt,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Untersuchung: Reise Verteilung von medallion

In diesem Beispiel identifiziert die Medallion (Taxi Zahlen) mit mehr als 100 Reisen innerhalb eines bestimmten Zeitraums. Die Abfrage würde der partitionierten Tabelle des Zugriffs profitieren, da es durch das Partitionsschema lagern ist **Pickup\_Datetime**. Abfragen des vollständigen Datasets machen auch mithilfe der partitionierten Tabelle und/oder Scan indizieren.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Untersuchung: Reise Verteilung von Medallion und hack_license

    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Beurteilung Daten: Überprüfen Sie, ob Datensätze mit falscher Längengrad und/oder Breitengrad

In diesem Beispiel wird untersucht werden, wenn keines der Felder Längengrad und/oder Breitengrad entweder einen ungültigen Wert enthalten (Radiant Grad sollte zwischen-90 und 90 sein), oder haben (0, 0) Koordinaten.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Untersuchung: Tipped im Vergleich zu nicht Geneigter Reisen Verteilung

In diesem Beispiel wird ermittelt die Anzahl der Reisen, die im Vergleich zu nicht in einem bestimmten Zeitraum Geneigter Geneigter wurden, Periode (oder in das vollständige Dataset, wenn mit dem gesamten Jahr). Diese Verteilung gilt für die Verteilung binary Bezeichnung später für die binäre Klassifizierung Modellierung verwendet werden sollen.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Untersuchung: Tipp Klasse-Bereich Verteilung

In diesem Beispiel wird berechnet die Verteilung der Tipp Bereiche in einem bestimmten Zeitraum an (oder in das vollständige Dataset, wenn mit dem gesamten Jahr). Dies ist die Verteilung der Beschriftung Klassen, die später für multiclass Klassifizierung Modellierung verwendet werden soll.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Untersuchung: Berechnen und Vergleichen von Reise Abstand

In diesem Beispiel konvertiert die Pickup- und Ladengeschäft Längengrad und Breitengrad, Geografie SQL verweist, berechnet den Reise Abstand SQL Geografie Punkt Differenz und der Ergebnisse für den Vergleich eine Stichprobe zurückgibt. Im Beispiel schränkt das Ergebnis auf gültige Koordinaten, die nur über die Qualität Assessment Datenabfrage zuvor behandelt.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Feature Engineering in SQL-Abfragen

Die Bezeichnung Generation und Geografie Konvertierung Untersuchung Abfragen können auch Etiketten-Features durch Entfernen des Webparts zählen generieren verwendet werden. Zusätzliche Features engineering SQL-Beispiele werden im Abschnitt [Durchsuchen von Daten und Engineering Feature in IPython Notizbuch](#ipnb) bereitgestellt. Es ist effizienter, das Feature Generation Abfragen ausführen, auf die vollständigen Dataset oder eine große Teilmenge unter Verwendung der SQL-Abfragen, die direkt auf die Instanz des SQL Server-Datenbank ausgeführt. Die Abfragen können in **SQL Server Management Studio**, IPython Notebook oder jeder Tool/Entwicklungsumgebung das die Datenbank, lokal oder Remote zugreifen können ausgeführt werden.

#### <a name="preparing-data-for-model-building"></a>Vorbereiten von Daten für das Modell zum Erstellen von

Die folgende Abfrage Joins die **Nyctaxi\_Reise** und **Nyctaxi\_Fahrpreis** Tabellen, generiert eine binäre Klassifizierung Bezeichnung **Geneigter**, ein Label mit mehreren Klasse Klassifizierung **Tipp\_Klasse**, und eine Stichprobe 1 % aus dem vollständigen verknüpften Dataset extrahiert. Mit dieser Abfrage kann kopiert dann direkt in der [Azure-Computer Learning Studio](https://studio.azureml.net) [Importieren von Daten] eingefügt werden[ import-data] -Modul für die Erfassung von direkten Daten aus der Instanz des SQL Server-Datenbank in Azure. Die Abfrage schließt Datensätze mit falsch (0, 0) Koordinaten.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Durchsuchen von Daten und Feature Engineering in IPython Notizbuch

In diesem Abschnitt werden wir Durchsuchen von Daten und Feature Generierung von Python und SQL-Abfragen für die zuvor erstellten SQL Server-Datenbank ausführen. Ein Beispiel IPython Notizbuch mit dem Namen **machine-Learning-data-science-process-sql-story.ipynb** wird im **Beispiel IPython Notizbücher** -Ordner bereitgestellt. Dieses Notizbuch ist auch auf [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)verfügbar.

Die empfohlene Reihenfolge beim Arbeiten mit großen Daten lautet wie folgt:

- In einige Beispiele für die Daten in einen Datenrahmen in-Memory-gelesen.
- Führen Sie einige Visualisierungen und mithilfe der gesammelten Daten kennen.
- Experimentieren Sie mit dem Feature Engineering mithilfe der gesammelten Daten.
- Verwenden Sie für größere Durchsuchen von Daten, Bearbeiten von Daten und Feature Engineering Python zum Ausstellen von SQL-Abfragen direkt mit der SQL Server-Datenbank in der Azure-VM.
- Entscheiden Sie die Größe der Stichprobe zum Erstellen der Azure-Computer Learning-Modell zu verwendenden.

Wenn Sie zur Einführung in Azure Computer fortfahren bereit sind, können Sie:  

1. Speichern Sie die endgültige SQL-Abfrage zum Extrahieren und die Beispieldaten und die Abfrage direkt in einem [Importierten Daten] kopieren und Einfügen[ import-data] Modul in Azure-Computer lernen. Diese Methode wird im Abschnitt [Zum Erstellen von Datenmodellen in Azure-Computer Learning](#mlmodel) veranschaulicht.    
2. Beibehalten der Stichprobe und Engineering Daten Sie verwenden für das Modell in eine neue Datenbanktabelle erstellen möchten, verwenden Sie das die neue Tabelle in die [Daten importieren] [ import-data] Modul.

Die folgenden sind einige Durchsuchen von Daten, Visualisierung von Daten und Feature engineering-Beispiele. Weitere Beispiele finden Sie unter Beispiel SQL IPython Notizbuch in den Ordner **Sample IPython Notebooks** .

#### <a name="initialize-database-credentials"></a>Initialisieren Sie Datenbankanmeldeinformationen

Initialisieren der Datenbankverbindungseinstellungen in den folgenden Variablen:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Create Database Connection

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Bericht Anzahl von Zeilen und Spalten in der Tabelle nyctaxi_trip

    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

- Gesamtanzahl der Zeilen = 173179759  
- Gesamtzahl der Spalten = 14

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a>Lesen in einer kleinen Datenbeispiel aus der SQL Server-Datenbank

    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Zeit zum Lesen, dass die Beispieltabelle 6.492000 Sekunden ist  
Die Anzahl der Zeilen und Spalten abgerufen = (84952, 21)

#### <a name="descriptive-statistics"></a>Beschreibende Statistik

Nun können mit die gesammelten Daten vertraut machen. Wir beginnen mit beschreibenden Statistiken für die Analyse der **Reise\_Abstand** (oder andere) Felder aus:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualisierung: Beispiel für Zeichnungsfläche

Als Nächstes stellen wir die Zeichnungsfläche Feld für den Reise Abstand zum Visualisieren der quantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Zeichnen Sie #1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualisierung: Verteilung Zeichnungsfläche Beispiel

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Zeichnen Sie #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualisierung: Häufig verwendete Hyperlinks und Zeile Flächen

In diesem Beispiel werden die Reise Entfernung in fünf Fächer bin und Visualisieren der binning Ergebnisse.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Wir können die oben genannten Bin Verteilung in einer Leiste zu zeichnen oder des Anschluss Zeichnungsfläche wie unten

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Zeichnen Sie #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![#4 zu zeichnen][4]

#### <a name="visualization-scatterplot-example"></a>Visualisierung: Scatterplot Beispiel

Wir zeigen, Punkt (XY) Zeichnungsfläche zwischen **Reise\_Zeit\_in\_Sekunden** und **Reise\_Abstand** zu sehen, ob alle Korrelation

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Zeichnen Sie #6][6]

In ähnlicher Weise können wir die Beziehung zwischen überprüfen **Rate\_Code** und **Reise\_Abstand**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Zeichnen Sie #8][8]

### <a name="sub-sampling-the-data-in-sql"></a>Untergeordnete Sampling die Daten in SQL Server

Bei der Vorbereitung für Datenmodell in [Azure Computer Learning Studio](https://studio.azureml.net)erstellen, Sie können Treffen einer Entscheidung bezüglich der **SQL-Abfrage direkt in das Modul importieren von Daten verwenden** oder beibehalten werden die Daten Engineering und Stichprobe in einer neuen Tabelle, die Sie in das [Importieren von Daten] verwenden können[ import-data] Modul mit einer einfachen * *Wählen* FROM < Ihrer\_neue\_Tabelle\_Name >**.

In diesem Abschnitt wird die aufgenommenen und Engineering-Daten zu speichern, um eine neue Tabelle erstellt. Ein Beispiel für eine direkte SQL-Abfrage für das Modell zum Erstellen von wird im Abschnitt [Durchsuchen von Daten und Engineering Feature in SQL Server](#dbexplore) bereitgestellt.

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a>Erstellen eine Stichprobe Tabelle und füllen Sie mit 1 % der verknüpften Tabellen. Drop Tabelle erste, sofern vorhanden.

In diesem Abschnitt wir Tabellen verknüpfen, **Nyctaxi\_Reise** und **Nyctaxi\_Fahrpreis**extrahieren eine Stichprobe 1 % und beibehalten die gesammelten Daten in eine neue Tabelle namens **Nyctaxi\_eine\_%**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Durchsuchen von Daten mithilfe von SQL-Abfragen in IPython Notizbuch

In diesem Abschnitt untersuchen wir Verteilung von Daten mithilfe der Stichprobe 1 % Daten dem dauerhaft in die neue Tabelle oben erstellte. Beachten Sie, dass ähnliche kennen die ursprünglichen Tabellen, optional **TABLESAMPLE** zur Begrenzung der Untersuchung Beispiel oder durch Beschränken der Ergebnisse auf einen bestimmten Zeitraum Periode mithilfe von ausgeführt werden können die **Pickup\_Datetime** Partitionen, wie im Abschnitt [Durchsuchen von Daten und Engineering Feature in SQL Server](#dbexplore) dargestellt.

#### <a name="exploration-daily-distribution-of-trips"></a>Untersuchung: Verteilung der täglichen der Reisen

    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Untersuchung: Reise Verteilung pro medallion

    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Verwenden von SQL-Abfragen in IPython Notizbuch Feature-Generierung

In diesem Abschnitt werden wir neue Etiketten generieren und Features, die direkt mit SQL-Abfragen, auf die Beispieltabelle 1 % wir im vorherigen Abschnitt erstellt.

#### <a name="label-generation-generate-class-labels"></a>Beschriftung Generation: Generieren Sie Klasse Etiketten

Im folgenden Beispiel generieren wir zwei Sätze von Bezeichnungen für Modellierung verwenden:

1. Binäre Klasse Etiketten **Geneigter** (Vorhersage Wenn eine Info erhält)
2. Multiclass Etiketten **Tipp\_Klasse** (Vorhersage der Tipp Bin oder dem Bereich)

        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''

        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()

        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''

        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Feature Engineering: Count Features für nach Kategorien sortierte Spalten

In diesem Beispiel wird transformiert ein kategorisierten Felds in ein numerisches Feld jeder Kategorie durch die Anzahl der Vorkommen in den Daten ersetzen.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Feature Engineering: Bin Features für numerische Spalten

In diesem Beispiel wird transformiert ein continuous numerisches Feld in vordefinierten Kategorie Bereiche, d. h., Transform numerisches Feld in einer kategorisierten dar.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Feature Engineering: Extrahieren Sie Speicherort Features aus Decimal Breitengrad/Längengrad

In diesem Beispiel bricht die dezimale Darstellung eines Felds Breitengrad und/oder Längengrad in mehrere Region Felder auf verschiedenen Granularitätsebenen als, Land, Stadt, Stadt, blockieren usw.. Beachten Sie, dass die neuen Geo-Felder den tatsächlichen Speicherorte nicht zugeordnet sind. Informationen zu Zuordnung Geocode Speicherorten finden Sie unter [Bing Maps REST-Dienste](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-the-final-form-of-the-featurized-table"></a>Überprüfen des endgültigen Formulars der Tabelle featurized

    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Wir sind jetzt bereit, um das Modell zum Erstellen von und Modell-Bereitstellung in [Azure-Computer Learning](https://studio.azureml.net)aufzurufen. Die Daten sind bereit für die Vorhersage Probleme weiter oben, nämlich identifiziert:

1. Binäre Klassifizierung: vorhergesagt unabhängig davon, ob ein Tipp für eine Reise bezahlt wurde.

2. Multiclass Klassifizierung: den Bereich der QuickInfo kostenpflichtige, entsprechend den zuvor definierten Klassen vorhergesagt.

3. Regressionsformel Aufgabe: die Menge der QuickInfo für eine Reise bezahlt vorhergesagt.  


## <a name="mlmodel"></a>Erstellen von Modellen in Azure-Computer lernen

Melden Sie sich, um die Modellierung Übung beginnen, in den Arbeitsbereich Learning der Azure-Computer an. Wenn Sie einen Computer erlernen Arbeitsbereich noch nicht erstellt haben, finden Sie unter [Erstellen eines Workspace Erlernen von Azure-Computer](machine-learning-create-workspace.md).

1. Azure-Computer Learning Einstieg finden Sie unter [Neuigkeiten Azure Computer Learning Studio?](machine-learning-what-is-ml-studio.md)

2. Melden Sie sich bei [Azure-Computer Studio Lernen](https://studio.azureml.net).

3. Die Homepage der Studio bietet eine Fülle von Informationen, Videos, Lernprogramme, Links auf die Module Referenz und andere Ressourcen. Weitere Informationen zu Azure-Computer Learning finden Sie in der [Azure Computer Lerncenter Dokumentation](https://azure.microsoft.com/documentation/services/machine-learning/).

Eine typische Schulung Experiments umfasst Folgendes:

1. Erstellen eines Experiments **+ neu** .
2. Abrufen der Daten zu lernen der Azure-Computer.
3. Vor dem verarbeiten, Transformieren und die Daten nach Bedarf ändern.
4. Generieren Sie Features, je nach Bedarf.
5. Teilen Sie die Daten in Datasets Training, Überprüfung, testen (oder haben Sie separate Datasets für jede).
6. Wählen Sie einen oder mehrere Computer Learning Algorithmen in Abhängigkeit von der Learning Problem zu lösen. Z. B. binäre Klassifizierung, multiclass Klassifizierung, Regressionsformel.
7. Schulen Sie ein oder mehrere Modelle mit dem Dataset Schulung.
8. Faktor Validierung Dataset mit der geschult Modelle.
9. Bewerten der Modelle, um die relevanten Metriken für das Problem Learning zu berechnen.
10. Einwandfrei optimieren Sie der Modelle aus, und wählen Sie das beste Modell zum Bereitstellen.

In dieser Übung haben wir bereits untersucht und Engineering-Daten in SQL Server und auf die Größe der Stichprobe in Azure-Computer lernen Aufnahme entschieden. So erstellen Sie eine oder mehrere der Vorhersagemodelle, die wir entschieden:

1. Abrufen der Daten zur Einführung in Azure-Computer unter Verwendung der [Daten importieren] [ import-data] Modul im Bereich **Daten ein- und Ausgabe** . Weitere Informationen finden Sie unter [Daten importieren] [ import-data] Referenzseite Modul.

    ![Azure-Computer Learning Importieren von Daten][17]

2. Wählen Sie **Azure SQL-Datenbank** als **Datenquelle** im **Eigenschaftenpanel** .

3. Geben Sie den DNS-Datenbanknamen im Feld **Datenbankservername** . Format:`tcp:<your_virtual_machine_DNS_name>,1433`

4. Geben Sie den **Datenbanknamen** in das entsprechende Feld ein.

5. Geben Sie die **SQL-Benutzername** in der **Server Aqccount Benutzername und das Kennwort in die **Server User Account Password **.

6. Aktivieren Sie Option **Alle Serverzertifikat akzeptieren** .

7. Im Bearbeitungsbereich Text **Datenbankabfrage** Beispiele einfügen die Abfrage, die extrahiert werden, die erforderlichen Felder (einschließlich keine berechneten Felder wie die Beschriftungen) database und nach-unten-Daten auf die gewünschte Stichprobengröße.

Ein Beispiel eines binären Klassifizierung Experiments Lesen von Daten direkt aus der SQL Server-Datenbank ist in der folgenden Abbildung. Ähnliche Versuche können für multiclass Klassifizierung und Regressionsformel Probleme erstellt werden.

![Azure-Computer Learning Zug][10]

> [AZURE.IMPORTANT] In den Modellierung Daten zur Verfügung gestellt Extraktion und sampling-Beispiele für die in den vorherigen Abschnitten, **Alle Etiketten für die drei Modellierung Übungen in der Abfrage enthalten sind**. Ein (erforderlich) wichtiger Schritt auf jedem der Modellierung Übungen ist die unnötigen Beschriftungen für die beiden anderen Probleme sowie alle anderen **zu Speicherverlusten Ziel** **ausgeschlossen** . Für z. B. binäre Klassifizierung Sie bei Verwendung der Bezeichnung **Geneigter** verwenden und ausschließen Felder **Tipp\_Klasse**, **Tipp\_Betrag**, und **insgesamt\_Betrag**. Da Letztere sind eine Ziel Speicherverluste, da beide Tipp implizieren bezahlt.
>
> Um unnötige Spalten ausschließen und/oder Speicherverluste abzielen, können die [Spalten in Dataset auswählen] [ select-columns] Modul oder die [Metadaten bearbeiten][edit-metadata]. Weitere Informationen finden Sie unter [Wählen Sie Spalten in Dataset] [ select-columns] und [Metadaten bearbeiten] [ edit-metadata] Seiten verweisen.

## <a name="mldeploy"></a>Bereitstellen von Modellen in Azure-Computer lernen

Wenn Ihr Modell bereit ist, können Sie auf einfache Weise als Webdienst direkt aus der Versuch, bereitstellen. Weitere Informationen zum Bereitstellen der Azure-Computer Learning-Webdienste finden Sie unter [Bereitstellen eines Webdiensts Learning der Azure-Computer](machine-learning-publish-a-machine-learning-web-service.md).

Um einen neuen Webdienst bereitstellen, müssen Sie:

1. Erstellen eines Bewertungsmuster Experiments.
2. Bereitstellen des Webdiensts.

Zum Erstellen eines bewertet Experiments mittels eines **beendet** Schulung Experiments, klicken Sie in der unteren Aktionsleiste auf **EXPERIMENTIEREN bewerten erstellen** .

![Bewerten von Azure][18]

Azure Computer Learning versucht, ein Bewertungsmuster Experiments basierend auf den Komponenten des Experiments Schulungen zu erstellen. Insbesondere wird es:

1. Speichern Sie das Modell geschulte und entfernen Sie das Modell Schulungsmodule.
2. Identifizieren Sie einen logischen **Eingangs-Port** , um die erwartete Eingabedaten Schema darstellen.
3. Identifizieren Sie einen logischen **Port Ausgabe** , um die erwartete Web Service Ausgabeschema darstellen.

Wenn Bewertungsmuster Experiments erstellt wird, überprüfen Sie es, und passen Sie nach Bedarf. Eine typische Anpassung ist mit der Bezeichnung Felder, schließt die Eingabe-Dataset und/oder Abfrage ersetzen, wie diese nicht verfügbar sind, wenn der Dienst aufgerufen wird. Es ist außerdem sollten Sie die Eingabe-Dataset und/oder Abfrage auf einige Datensätze zu verkleinern nur genug sind, um das input-Schema anzugeben. Für den Port Ausgabe wird für alle Felder und ausschließen nur die **Label bewertet** und **Wahrscheinlichkeiten bewertet** in der Ausgabe von [Spalten in Dataset auswählen] [ select-columns] Modul.

Ein Beispiel bewerten Experiments ist in der folgenden Abbildung. Wenn Sie mit der Bereitstellung beginnen, klicken Sie auf die Schaltfläche **Veröffentlichen-Webdienst** in der unteren Aktionsleiste.

![Azure-Computer Learning veröffentlichen][11]

In diesem Lernprogramm Exemplarische Vorgehensweise zusammenfassen, um haben Sie eine arbeitete mit einem großen öffentlichen Dataset ganz von Datenerfassung zum Modellieren von Schulungen und Bereitstellen eines Webdiensts Learning der Azure-Computer Science-Umgebung mit Azure-Daten erstellt.

### <a name="license-information"></a>Lizenzinformationen

Diese exemplarische Vorgehensweise und die zugehörigen Skripts und IPython Notebook(s) sind von Microsoft unter der Lizenz MIT freigegeben. Überprüfen Sie die Datei, in das Verzeichnis des Beispielcodes auf GitHub für weitere Details.

### <a name="references"></a>Verweise

• [Andrés Monroy NYC Taxi Reisen Downloadseite](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing des NYC Taxi Reise Daten von Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi und Limousine Kommission Research und Statistiken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)


[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
