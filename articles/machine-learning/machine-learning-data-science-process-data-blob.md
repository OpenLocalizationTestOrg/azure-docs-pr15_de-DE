<properties 
    pageTitle="Verarbeiten von Azure Blob-Daten mit erweiterten Analytics | Microsoft Azure" 
    description="Verarbeitung von Daten in Azure BLOB-Speicher." 
    services="machine-learning,storage" 
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
    ms.author="fashah;garye;bradsev" /> 

#<a name="heading"></a>Verarbeiten von Azure Blob-Daten mit erweiterten analytics

In diesem Dokument werden Kennenlernen Daten und Funktionen in Azure BLOB-Speicher gespeicherten Daten, Generieren von behandelt. 

## <a name="load-the-data-into-a-pandas-data-frame"></a>Laden Sie die Daten in einen Pandas Datenrahmen
Um untersuchen und zu einem Dataset ändern, müssen sie aus der Quelle Blob in einer lokalen Datei heruntergeladen werden die anschließend in einem Pandas Daten Frame geladen werden kann. Hier sind die auszuführenden Schritte für dieses Verfahren aus:

1. Download die Daten von Azure BLOB-mit dem folgenden Beispiel Python-Code mit BLOB-Dienst. Ersetzen Sie im folgenden Code wird die Variable durch Ihre spezifischen Werte: 

        from azure.storage.blob import BlobService
        import tables
        
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>

        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))


2. Lesen der Daten in einem Pandas Daten-Frame aus der heruntergeladenen Datei.

        #LOCALFILE is the file path 
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Sie sind jetzt bereit zum Durchsuchen der Daten und zum Generieren von Features auf dieses Dataset.


##<a name="blob-dataexploration"></a>Durchsuchen von Daten

Hier sind einige Beispiele für die Möglichkeiten zum Untersuchen von Daten mithilfe von Pandas verwenden:

1. Überprüfen Sie die Anzahl der Zeilen und Spalten. 

        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape

2. Untersuchen Sie die ersten oder letzten Zeilen im Dataset wie folgt:

        dataframe_blobdata.head(10)
        
        dataframe_blobdata.tail(10)

3. Überprüfen Sie die Datentypen, die jeder Spalte importiert wurde, wie die Verwendung des folgende Beispielcode
    
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype

4. Überprüfen Sie die grundlegenden Statistiken für die Spalten in das DataSet wie folgt
 
        dataframe_blobdata.describe()
    
5. Sehen Sie sich die Anzahl der Einträge für jeden Wert von Column wie folgt

        dataframe_blobdata['<column_name>'].value_counts()

6. Zählen Sie im Vergleich zu die tatsächliche Anzahl der Einträge in jeder Spalte der folgende Beispielcode mit fehlende Werten

        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
     
7.  Wenn Sie Werte für eine bestimmte Spalte fehlen in den Daten verfügen, können Sie sie wie folgt ablegen:

        dataframe_blobdata_noNA = dataframe_blobdata.dropna()
        dataframe_blobdata_noNA.shape

    Eine andere Möglichkeit, ersetzen Sie die fehlende Werten wird mit der Mode-Funktion:
    
        dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        

8. Erstellen einer Variablen Anzahl der Fächer verwenden, um die Verteilung einer Variablen zu zeichnen Histogramm Zeichnungsfläche 
    
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
        
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
    
9. Sehen Sie sich können Sie die Korrelation zwischen Variablen über eine Scatterplot oder mithilfe der integrierten Korrelations-Funktion

        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
        
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()
    
    
##<a name="blob-featuregen"></a>Feature-Generierung
    
Wir können Features mit Python wie folgt erstellen:

###<a name="blob-countfeature"></a>Symbol Wert basiert Feature-Generierung

Nach Kategorien sortierte Features können wie folgt erstellt:

1. Untersuchen Sie die Verteilung der nach Kategorien sortierte Spalte:
    
        dataframe_blobdata['<categorical_column>'].value_counts()

2. Generieren Sie Symbol-Werte für die einzelnen Werte in den Spalten

        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')

3. Teilnehmen an der Spalte mit der ursprünglichen Datenrahmen 
 
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)

4. Entfernen Sie die ursprüngliche Variable selbst:

        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)
    
###<a name="blob-binningfeature"></a>Schachten Feature Generation von

Zum Generieren von binned Features, gehen wir wie folgt:

1. Hinzufügen einer Sequenz von Spalten an, um eine numerische Spalte bin
 
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
        
2. Konvertieren einer Sequenz von Variablen vom Datentyp boolean Schachten von

        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
    
3. Schließlich teilnehmen Sie die simulierte Variablen wieder auf den ursprünglichen Daten frame

        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool) 


##<a name="sql-featuregen"></a>Zurückschreiben von Daten in Azure Blob und Verarbeiten von in Azure-Computer lernen

Nachdem Sie die Daten untersucht haben und Sie können die benötigten Features erstellt, die Daten hochladen (aufgenommen oder Featurized) für eine Azure BLOB- und nutzen Sie es in Azure Computer Lernen mit den folgenden Schritten: beachten, dass zusätzliche Features in Azure Computer Learning Studio sowie erstellt werden können. 
1. Schreiben von Daten Rahmens in lokale Datei

        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Laden Sie die Daten in Azure Blob wie folgt:

        from azure.storage.blob import BlobService
        import tables

        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>

        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
        
        try:
       
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
        
        except:         
            print ("Something went wrong with uploading blob:"+BLOBNAME)

3. Nachdem die Daten aus dem Blob mithilfe der Azure-Computer Learning [Daten importieren] gelesen werden können[ import-data] Modul wie in dem folgenden Bildschirm dargestellt:
 
![Leser blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
 
