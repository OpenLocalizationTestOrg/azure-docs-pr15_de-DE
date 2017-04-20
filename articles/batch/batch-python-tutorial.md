<properties
    pageTitle="Lernprogramm - Erste Schritte mit dem Client Azure Stapel Python | Microsoft Azure"
    description="Erfahren Sie, die grundlegenden Konzepte von Azure Stapel und wie Sie den Dienst Stapel mit einem einfachen Szenario entwickeln"
    services="batch"
    documentationCenter="python"
    authors="mmacy"
    manager="timlt"
    editor=""/>

<tags
    ms.service="batch"
    ms.devlang="python"
    ms.topic="hero-article"
    ms.tgt_pltfrm="na"
    ms.workload="big-compute"
    ms.date="09/27/2016"
    ms.author="marsma"/>

# <a name="get-started-with-the-azure-batch-python-client"></a>Erste Schritte mit der Azure Stapel Python-client

> [AZURE.SELECTOR]
- [.NET](batch-dotnet-get-started.md)
- [Python](batch-python-tutorial.md)

Erlernen Sie die Grundlagen des [Blatts Azure] [ azure_batch] und den [Stapel Python] [ py_azure_sdk] Client wie eine kleine Stapel Anwendung in Python geschrieben erläutert. Betrachten wir wie zwei Stichproben Skripts verwenden den Stapel Dienst Verarbeitungszeit eine parallele Arbeitsbelastung auf Linux virtuellen Computern in der Cloud, und den Umgang mit [Azure-Speicher](./../storage/storage-introduction.md) für Datei Staging und abrufen. Sie erhalten einen allgemeinen Stapel Anwendungsworkflow erfahren Sie, erhalten einen Überblick über die wichtigsten Komponenten des Blatts Projekte, Vorgänge, Pools Basis und Knoten zu berechnen.

![Stapel Lösung Workflow (Basic)][11]<br/>

## <a name="prerequisites"></a>Erforderliche Komponenten

In diesem Artikel wird vorausgesetzt, dass Sie Kenntnisse von Python und Vertrautheit mit Linux verfügen. Außerdem wird davon ausgegangen, dass Sie die Konto Erstellung Anforderungen erfüllen, die für Azure und den Stapel und Speicher Services sind unter angegeben werden können.

### <a name="accounts"></a>Konten

- **Azure-Konto**: Wenn Sie bereits über ein Azure-Abonnement, [Erstellen Sie ein kostenloses Azure-Konto]besitzen[azure_free_account].
- **Stapel Konto**: Nachdem Sie ein Azure-Abonnement, [Erstellen Sie ein Stapel Azure-Konto](batch-account-create-portal.md)haben.
- **Speicher-Konto**: finden Sie unter [Erstellen eines Kontos Speicher](../storage/storage-create-storage-account.md#create-a-storage-account) in [zur Azure-Speicher-Konten](../storage/storage-create-storage-account.md).

### <a name="code-sample"></a>Beispiel für Code

Die zusammengehörenden Python- [Code Stichprobe] [ github_article_samples] eine viele Stapel Codebeispielen befindet sich in den [Azure-Stapel-Beispiele] [ github_samples] Repository auf GitHub. Können Sie alle Beispiele herunterladen, indem Sie auf **Datenbeschriftungsreihe oder Downloads > herunterladen ZIP-** auf der Startseite Repository, oder indem Sie auf der [Azure-Stapel-Beispiele-master.zip] [ github_samples_zip] direkten Downloadlink. Nachdem Sie den Inhalt der ZIP-Datei extrahiert haben, befinden sich die beiden Skripts in diesem Lernprogramm der `article_samples` Verzeichnis:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Python-Umgebung

Zum Beispiel- *python_tutorial_client.py* -Skript auf Ihrem lokalen Computer ausführen zu können, benötigen Sie eine **Python Interpreter** mit Version **2.7** oder **3,3 +**kompatibel. Das Skript wurde auf Linux und Windows getestet.

### <a name="cryptography-dependencies"></a>Abhängigkeiten Verschlüsselung

Sie müssen die Abhängigkeiten für die [Verschlüsselung] installieren[ crypto] Bibliothek erforderlich, indem Sie die `azure-batch` und `azure-storage` Python Pakete. Führen Sie einen der folgenden Vorgänge für Ihre Plattform geeignet, oder schlagen Sie in der [Verschlüsselung Installation] [ crypto_install] Details für Weitere Informationen:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`

* CentOS

    `yum update && yum install -y gcc openssl-dev libffi-devel python-devel`

* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`

* Windows

    `pip install cryptography`

>[AZURE.NOTE] Wenn für Python 3.3 + unter Linux installieren zu können, verwenden Sie die entsprechenden python3 für die Abhängigkeiten Python aus. Klicken Sie beispielsweise auf Ubuntu:`apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`

### <a name="azure-packages"></a>Azure-Paketen

Installieren Sie dann die **Azure Stapel** und **Azure-Speicher** Python Pakete. Sie führen Sie mit **Pip** und der *requirements.txt* finden Sie hier:

`/azure-batch-samples/Python/Batch/requirements.txt`

Problem folgen **Pip** Befehl aus, um die Pakete Stapel und Speicherplatz zu installieren:

`pip install -r requirements.txt`

Sie können den [Azure-Stapel] installieren[ pypi_batch] und [Azure-Speicher] [ pypi_storage] Python verpackt manuell:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [AZURE.TIP] Möglicherweise müssen Sie die Befehle mit Präfix `sudo` Wenn Sie ein Konto ohne Berechtigungen verwenden. Beispielsweise `sudo pip install -r requirements.txt`. Weitere Informationen zur Installation von Python-Paketen finden Sie unter [Installieren von Paketen] [ pypi_install] auf readthedocs.io.

## <a name="batch-python-tutorial-code-sample"></a>Beispiel für Stapel Python-Code des Lernprogramms

Im Beispiel zusammengehörenden Stapel Python besteht aus zwei Python Skripts und einige Datendateien.

- **python_tutorial_client.py**: interagiert mit den Diensten Stapel und Speicher eine parallele Arbeitsbelastung Datenverarbeitungsknoten (virtuelle Maschinen) ausführen. Das Skript *python_tutorial_client.py* , die auf Ihrem lokalen Computer ausgeführt wird.

- **python_tutorial_task.py**: das Skript, das ausgeführt wird, klicken Sie auf, berechnen Knoten in Azure die ist-Arbeit ausführen. In der Stichprobe analysiert *python_tutorial_task.py* den Text in einer Datei heruntergeladen aus Azure-Speicher (die Eingabe-Datei). Klicken Sie dann werden eine Textdatei (die Ausgabedatei), die eine Liste der obersten drei Wörter enthält, die die Eingabe Datei angezeigt. Nachdem sie die Ausgabedatei erstellt hat, uploads *python_tutorial_task.py* die Datei zu Azure-Speicher. Dadurch für herunterladen, um das Clientskript läuft auf Ihrem Computer zur Verfügung. Das Skript *python_tutorial_task.py* führt parallel auf mehreren berechnen-Knoten in der Stapel-Dienst.

- **./data/taskdata\*txt**: Diese drei Textdateien mitteilen, die für die Aufgaben, die auf den Knoten berechnen ausführen.

Das folgende Diagramm veranschaulicht die primäre Vorgänge, die von den Skripts Client und Vorgang ausgeführt werden. Dieser grundlegende Workflow ist normalerweise der viele berechnen Lösungen, die mit der Stapelverarbeitung erstellt wurden. Während sie jeder Stapel Dienst verfügbar Feature nicht zu veranschaulichen, umfasst nahezu jedem Stapel Szenario Teile dieser Workflow aus.

![Stapel Beispielworkflows][8]<br/>

[**Schritt 1.**](#step-1-create-storage-containers) Erstellen Sie **Container** in Azure BLOB-Speicher.<br/>
[**Schritt 2.**](#step-2-upload-task-script-and-data-files) Hochladen von Task-Skript und Eingabe-Dateien auf Container.<br/>
[**Schritt 3.**](#step-3-create-batch-pool) Erstellen Sie einen Stapel **Ressourcenpool**an.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Pool **StartTask** downloads das Skript Vorgang (python_tutorial_task.py) Knoten, wie er im Ressourcenpool teilnehmen an.<br/>
[**Schritt 4.**](#step-4-create-batch-job) Erstellen Sie eine **Position**ein.<br/>
[**Schritt 5 fort.**](#step-5-add-tasks-to-job) Hinzufügen von **Vorgängen** im Projekt.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Die Vorgänge werden auszuführenden auf Knoten geplant.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5 b.** Jede Aufgabe downloads seiner Eingabedaten aus Azure-Speicher, und klicken Sie dann mit der Ausführung beginnt.<br/>
[**Schritt 6 fort.**](#step-6-monitor-tasks) Überwachen von Aufgaben.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Wenn Vorgänge abgeschlossen sind, Hochladen diese ihre Ausgabedaten auf Azure-Speicher.<br/>
[**Schritt 7.**](#step-7-download-task-output) Laden Sie Vorgang Ausgabe von Speicher.

Wie erwähnt, nicht jeder Stapel Lösung führt die genauen Schritte aus, und enthalten möglicherweise veranschaulicht viele weitere, aber dieses Beispiel allgemeine Prozesse in einem Stapel Lösung gefunden.

## <a name="prepare-client-script"></a>Vorbereiten der Clientskript

Bevor Sie das Beispiel ausführen, fügen Sie Ihre Anmeldeinformationen ein Konto Stapel und Speicher hinzu *python_tutorial_client.py*. Wenn Sie dies noch nicht getan haben, öffnen Sie die Datei in Ihrem bevorzugten Editor, und aktualisieren Sie die folgenden Zeilen mit Ihren Anmeldeinformationen.

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
batch_account_name = "";
batch_account_key  = "";
batch_account_url  = "";

# Storage account credentials
storage_account_name = "";
storage_account_key  = "";
```

Ihre Anmeldeinformationen Stapel und Speicher in jedem Dienst Falz Konto finden Sie im [Portal Azure][azure_portal]:

![Stapelverarbeitung Anmeldeinformationen im Portal][9]
![Speicher Anmeldeinformationen im Portal][10]<br/>

In den folgenden Abschnitten analysieren wir die Schritte, die von den Skripts zum Verarbeiten von einer Arbeitsbelastung im Stapel-Dienst verwendet. Wir empfehlen Ihnen regelmäßig bezieht sich auf die Skripts in Editor, während der Arbeit zurecht durch die restlichen Artikel.

Wechseln Sie in die folgende Zeile in **python_tutorial_client.py** So starten Sie mit Schritt 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Schritt 1: Erstellen von Speichercontainer

![Erstellen von Containern in Azure-Speicher][1]
<br/>

Stapel enthält integrierten Unterstützung für die Interaktion mit Azure-Speicher. Container in Ihr Konto Speicher bietet die Dateien erforderlich, indem Sie die Aufgaben, die in Ihrem Konto Stapel ausgeführt werden. Die Container stellen auch einen Ort zum Speichern der Ausgabedaten, die die Aufgaben zu erstellen. Erstes bedeutet das Skript *python_tutorial_client.py* ist drei Container in [Azure BLOB-Speicher](../storage/storage-introduction.md#blob-storage)zu erstellen:

- **Anwendung**: dieser Container wird das Python-Skript ausführen, indem Sie die Aufgaben, *python_tutorial_task.py*speichern.
- **Eingabe**: Aufgaben werden aus dem *Eingabewerte* Container Verarbeitungszeit Datendateien herunterladen.
- **Ergebnis**: Wenn Vorgänge eingegebenen Datei Verarbeitung abgeschlossen haben, werden diese Hochladen der Ergebnisse an den Container *Ausgabe* .

Um ein Speicherkonto interagieren und Container erstellen, verwenden wir die [Azure-Speicher] [ pypi_storage] Paket zum Erstellen einer [BlockBlobService] [ py_blockblobservice] Objekt – "BLOB-Client". Wir erstellen Sie drei Container im über den Client BLOB-Speicher-Konto an.

```python
 # Create the blob client, for use in obtaining references to
 # blob storage containers and uploading files to containers.
 blob_client = azureblob.BlockBlobService(
     account_name=_STORAGE_ACCOUNT_NAME,
     account_key=_STORAGE_ACCOUNT_KEY)

 # Use the blob client to create the containers in Azure Storage if they
 # don't yet exist.
 app_container_name = 'application'
 input_container_name = 'input'
 output_container_name = 'output'
 blob_client.create_container(app_container_name, fail_on_exist=False)
 blob_client.create_container(input_container_name, fail_on_exist=False)
 blob_client.create_container(output_container_name, fail_on_exist=False)
```

Nachdem der Container erstellt wurden, kann die Anwendung nun die Dateien hochladen, die von Aufgaben verwendet werden.

> [AZURE.TIP] [So verwenden Sie Azure Blob-Speicher von Python](../storage/storage-python-how-to-use-blob-storage.md) bietet einen guten Überblick über das Arbeiten mit Azure-Speicher Container und Blobs. Sie sollten am oberen Rand der Liste lesen, wie Sie mit der Stapelverarbeitung zu arbeiten beginnen.

## <a name="step-2-upload-task-script-and-data-files"></a>Schritt 2: Hochladen Sie Vorgang Skripts und Datendateien

![Hochladen von Vorgang Anwendung und Eingabe (Daten) Dateien zu Containern][2]
<br/>

In der Datei hochladen Operation definiert *python_tutorial_client.py* zuerst Websitesammlungen **Anwendung** und **Eingabewerte** Datei Wege, wie sie auf dem lokalen Computer vorhanden sind. Und sie diese Dateien auf die Container hochgeladen wird, die Sie im vorherigen Schritt erstellt haben.

```python
 # Paths to the task script. This script will be executed by the tasks that
 # run on the compute nodes.
 application_file_paths = [os.path.realpath('python_tutorial_task.py')]

 # The collection of data files that are to be processed by the tasks.
 input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                     os.path.realpath('./data/taskdata2.txt'),
                     os.path.realpath('./data/taskdata3.txt')]

 # Upload the application script to Azure Storage. This is the script that
 # will process the data files, and is executed by each of the tasks on the
 # compute nodes.
 application_files = [
     upload_file_to_container(blob_client, app_container_name, file_path)
     for file_path in application_file_paths]

 # Upload the data files. This is the data that will be processed by each of
 # the tasks executed on the compute nodes in the pool.
 input_files = [
     upload_file_to_container(blob_client, input_container_name, file_path)
     for file_path in input_file_paths]
```

Verständnis der Liste, mit der `upload_file_to_container` Funktion für jede Datei in der Websitesammlungen und zwei [ResourceFile] heißt[ py_resource_file] Websitesammlungen ausgefüllt werden. Die `upload_file_to_container` Funktion steht unter:

```
def upload_file_to_container(block_blob_client, container_name, file_path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """
    blob_name = os.path.basename(file_path)

    print('Uploading file {} to container [{}]...'.format(file_path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles

Eine [ResourceFile] [ py_resource_file] bietet Aufgaben in Stapel mit der URL einer Datei in Azure-Speicher, die mit einem Knoten berechnen heruntergeladen wurde, bevor Sie diesen Vorgang ausgeführt wird. Die [ResourceFile][py_resource_file]. **Blob_source** -Eigenschaft gibt die vollständige URL der Datei an, wie sie in Azure-Speicher vorhanden sind. Die URL kann auch eine Signatur freigegebenen Access (SAS) enthalten, die sicheren Zugriff auf die Datei enthält. Die meisten Vorgangsarten in Stapel enthalten eine *ResourceFiles* -Eigenschaft, einschließlich:

- [CloudTask][py_task]
- [StartTask][py_starttask]
- [JobPreparationTask][py_jobpreptask]
- [JobReleaseTask][py_jobreltask]

In diesem Beispiel wird die Vorgangsarten JobPreparationTask oder JobReleaseTask nicht verwendet, aber Sie können Sie weitere Informationen über diese [Ausführen Vorbereitung und Fertigstellung Projektaufgaben Azure Blattnamen Knoten zu berechnen](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Freigegebene Access Signatur (SAS)

Freigegebene Access Signaturen sind Zeichenfolgen, die sicheren Zugriff auf Container und Blobs in Azure-Speicher bereitzustellen. Das Skript *python_tutorial_client.py* verwendet beide Blob und Container freigegeben Access Signaturen und veranschaulicht, wie diese Zeichenfolgen für den freigegebenen Zugriff Signatur aus der Speicherdienst zu erhalten.

- **BLOB freigegeben Access Signaturen**: des Pool StartTask verwendet BLOB-gemeinsamen Zugriff Signaturen aus, wenn es Datendateien für die Aufgabe Skripts und Eingabe von Speicher downloads (siehe [Schritt 3](#step-3-create-batch-pool) unten). Die `upload_file_to_container` -Funktion in *python_tutorial_client.py* enthält den Code, der einzelnen Blob des freigegebenen Access Signatur abruft. Bedeutet dies, indem Sie [BlockBlobService.make_blob_url] [ py_make_blob_url] im Speichermodul.

- **Container gemeinsamen Zugriff Signatur**: wie jeden Vorgang seine Arbeit auf dem Berechnungsknoten beendet, wird deren Ausgabedatei auf den Container *Ausgabe* in Azure-Speicher hochgeladen. Dazu verwendet *python_tutorial_task.py* eine Container freigegebenen Access-Signatur, die Schreibzugriff auf den Container bereitstellt. Die `get_container_sas_token` Funktion in *python_tutorial_client.py* erhält des Containers gemeinsamen Zugriff Signatur, die an die Aufgaben dann als Argument übergeben wird. Schritt 5 #, [Hinzufügen von Vorgängen zu einer Position](#step-5-add-tasks-to-job), wird die Verwendung des Containers SAS erläutert.

> [AZURE.TIP] Schauen Sie sich die auf freigegebenen Access Signaturen zweiteiligen Reihe [Teil 1: Grundlegendes zu SAS-Modell](../storage/storage-dotnet-shared-access-signature-part-1.md) und [Teil 2: Erstellen und Verwenden eines SAS mit dem Blob-Dienst](../storage/storage-dotnet-shared-access-signature-part-2.md), um mehr über den sicheren Zugriff auf Daten in Ihr Konto Speicher zu erfahren.

## <a name="step-3-create-batch-pool"></a>Schritt 3: Erstellen von Stapel Ressourcenpool

![Erstellen von einem Stapel Ressourcenpool][3]
<br/>

Einem Stapel **Ressourcenpool** ist eine Auflistung von Computeknoten (virtuelle Maschinen), auf denen Stapel Vorgänge des Projekts ausgeführt wird.

Nachdem der Vorgang Skripts und Datendateien mit dem Konto Speicher hochgeladen wird, beginnt *python_tutorial_client.py* seine Interaktion mit dem Dienst Stapel mithilfe des Moduls Stapel Python. Eine [BatchServiceClient] dazu[ py_batchserviceclient] wird erstellt:

```python
 # Create a Batch service client. We'll now be interacting with the Batch
 # service in addition to Storage.
 credentials = batchauth.SharedKeyCredentials(_BATCH_ACCOUNT_NAME,
                                              _BATCH_ACCOUNT_KEY)

 batch_client = batch.BatchServiceClient(
     credentials,
     base_url=_BATCH_ACCOUNT_URL)
```

Anschließend wird in den Stapel Konto mit einem Anruf, um ein Pool von Computeknoten erstellt `create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Wenn Sie einem Ressourcenpool erstellen, definieren Sie eine [PoolAddParameter] [ py_pooladdparam] , die verschiedene Eigenschaften für den Pool angibt:

- **ID** des dem Pool (*Id* - erforderlich)<p/>Wie bei den meisten Einheiten in Stapel, müssen Ihre neue Ressourcenpool eine eindeutige ID in Ihrem Konto Stapel. Der Code bezieht sich auf diesem Pool mit seiner-ID, und es ist, wie Sie den Pool im Azure- [Portal]identifizieren[azure_portal].

- **Anzahl der berechnen Knoten** (*Target_dedicated* - erforderlich)<p/>Diese Eigenschaft gibt an, wie viele virtuellen Computern im Pool bereitgestellt werden sollen. Es ist zu beachten, dass alle Stapel Konten ein **Kontingent** verfügen, die die Anzahl der **Kerne** (und daher berechnen Knoten) in einem Stapel Konto eingeschränkt. Sie können die standardmäßige Kontingente und Anweisungen zum [Vergrößern eine Vorgabe](batch-quota-limit.md#increase-a-quota) (beispielsweise die maximale Anzahl der Kerne in Ihr Konto Stapel) in [Kontingente und Grenzwerte für den Dienst Azure Stapel](batch-quota-limit.md)suchen. Wenn Sie feststellen, sich fragt, "Warum wird nicht Mein Ressourcenpool erreichen von mehreren X-Knoten?" die Ursache für dieses Core Kontingent sein.

- **Betriebssystem** für Knoten (*Virtual_machine_configuration* **oder** *Cloud_service_configuration* - erforderlich)<p/>In *python_tutorial_client.py*, erstellen wir einen Pool Linux Knoten mit einem [VirtualMachineConfiguration][py_vm_config]. Die `select_latest_verified_vm_image_with_node_agent_sku` in Funktion `common.helpers` vereinfacht das Arbeiten mit [Azure-virtuellen Computern Marketplace] [ vm_marketplace] Bilder. Weitere Informationen zur Verwendung von Marketplace Bilder finden Sie unter [Bereitstellen von Linux Knoten in Azure Stapel Pools zu berechnen](batch-linux-nodes.md) .

- **Größe des berechnen Knoten** (*Vm_size* - erforderlich)<p/>Da wir Linux Knoten für unsere [VirtualMachineConfiguration]angegeben haben[py_vm_config], wir geben Sie eine Größe virtueller Computer (`STANDARD_A1` in diesem Beispiel) von [Größen für virtuellen Computern in Azure](../virtual-machines/virtual-machines-linux-sizes.md). Erneut, finden Sie unter [Bereitstellen von Linux berechnen Knoten in Azure Stapel Pools](batch-linux-nodes.md) für Weitere Informationen.

- **Starten des Vorgangs** (*Start_task* - nicht erforderlich)<p/>Zusammen mit den über physischen Knoteneigenschaften, können Sie auch angeben einer [StartTask] [ py_starttask] für den Ressourcenpool (es ist nicht erforderlich). Die StartTask führt auf den einzelnen Knoten, wie der Knoten Pool Beitritt und jedes Mal ein Knoten neu gestartet wird. Die StartTask ist besonders hilfreich, bei der Vorbereitung Datenverarbeitungsknoten für die Ausführung von Aufgaben, wie etwa installieren die Programme, die Ihre Aufgaben ausgeführt werden.<p/>In diesem Beispiel-Anwendung übernimmt die StartTask Dateien, die sie downloads von Speicher (die angegeben sind, mithilfe der StartTasks **Resource_files** Eigenschaft) aus der StartTask *Directory arbeiten* auf das *freigegebene* Verzeichnis, die alle Vorgänge auf dem Knoten zugreifen können. Dadurch wird im Wesentlichen kopiert `python_tutorial_task.py` auf das freigegebene Verzeichnis auf den einzelnen Knoten wie der Knoten im Ressourcenpool beitritt, damit alle Aufgaben ausführen, die auf dem Knoten darauf zugreifen können.

Haben Sie bemerkt den Anruf an die `wrap_commands_in_shell` Helper (Funktion). Diese Funktion wird eine Auflistung von separate Befehle und erstellt eine einzige Befehlszeile für einen Vorgang Befehlszeileneigenschaft geeignet.

Auch wichtigste im obigen Codeausschnitt Änderung betrifft die Verwendung von zwei Umgebungsvariablen in der Eigenschaft **Befehlszeile** die StartTask: `AZ_BATCH_TASK_WORKING_DIR` und `AZ_BATCH_NODE_SHARED_DIR`. Jeder Computeknoten in einem Stapel Pool wird automatisch mit mehreren Umgebungsvariablen konfiguriert werden, die zum Stapel spezifisch sind. Jeder Prozess, der durch einen Vorgang ausgeführt wird hat Zugriff auf diese Umgebungsvariablen.

> [AZURE.TIP] Weitere Informationen zu der Umgebungsvariablen, auf Datenverarbeitungsknoten in einem Stapel Ressourcenpool sowie Informationen zum Vorgang Arbeitsverzeichnisse verfügbar sind, finden Sie unter **-Umgebung, die Einstellungen für Vorgänge** und **Dateien und Verzeichnissen** im [Stapel Azure-Features im Überblick](batch-api-basics.md).

## <a name="step-4-create-batch-job"></a>Schritt 4: Erstellen von Stapelverarbeitung

![Stapelverarbeitung erstellen][4]<br/>

Eine **Position** ist eine Sammlung von Vorgängen und einem Pool von Computeknoten zugeordnet ist. Die Aufgaben eines Projekts auf die zugeordneten Ressourcenpool berechnen Knoten ausgeführt werden.

Sie können ein Projekt nicht nur zum Organisieren und Nachverfolgen von Aufgaben in verknüpften Auslastung, sondern auch zur Erhebung von bestimmter Einschränkungen – wie etwa die maximale Laufzeit für das Projekt (und von Erweiterung, deren Aufgaben) und Priorität in Bezug auf die anderen Projekten in das Konto Stapel der beruflichen Position. In diesem Beispiel ist die Aufgabe jedoch nur mit dem Pool, der in Schritt 3 # erstellte verknüpft. Es sind keine zusätzlichen Eigenschaften konfiguriert.

Alle Stapelverarbeitungsaufträge stehen im Zusammenhang mit einem bestimmten Pool. Diese Zuordnung gibt an, welche Knoten Vorgänge des Projekts klicken Sie auf ausführen. Sie angeben der Ressourcenpool mithilfe der [PoolInformation] [ py_poolinfo] Eigenschaft, wie im folgenden Codeausschnitt dargestellt.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Nachdem Sie nun ein Auftrag erstellt wurde, werden Aufgaben für die Arbeitsschritte hinzugefügt.

## <a name="step-5-add-tasks-to-job"></a>Schritt 5: Hinzufügen von Aufgaben zum Projekt

![Hinzufügen von Aufgaben zum Projekt][5]<br/>
*(1) Vorgänge werden dem Projekt hinzugefügt, (2) die Vorgänge werden planmäßig auf Knoten ausführen und (3) die Aufgaben herunterladen, die zu verarbeitenden Datendateien*

Stapel **Aufgaben** sind die einzelnen Einheiten von Arbeit, die auf den Knoten berechnen ausführen. Eine Aufgabe verfügt über eine Befehlszeile und führt die Skripts oder ausführbare Dateien, die Sie in die Befehlszeile angeben.

Um die Arbeit tatsächlich ausführen zu können, müssen Aufgaben mit einem Projekt hinzugefügt werden. Jede [CloudTask] [ py_task] ist so konfiguriert, dass mit einer Befehlszeileneigenschaft und [ResourceFiles] [ py_resource_file] (wie mit dem Pool des StartTask), die die Aufgabe downloads auf den Knoten, bevor die Befehlszeile automatisch ausgeführt wird. In der Stichprobe verarbeitet jeden Vorgang nur eine Datei. Auf diese Weise enthält seiner ResourceFiles-Auflistung ein einzelnes Element.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [AZURE.IMPORTANT] Wenn sie Zugriff auf Umgebungsvariablen wie `$AZ_BATCH_NODE_SHARED_DIR` oder Ausführen der Anwendung nicht befindet sich der Knoten `PATH`, Befehl Aufgabenzeilen müssen die Verwaltungsshell aufrufen explizit, z. B. mit `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Diese Anforderung ist nicht erforderlich, wenn Ihre Aufgaben, eine Anwendung im des Knotens ausführen `PATH` und nicht auf eine beliebige Umgebungsvariablen verweisen.

Innerhalb der `for` Schleife im obigen Codeausschnitt, können Sie sehen, dass die Befehlszeile für den Vorgang mit fünf Befehlszeilenargumente erstellt wird, die an *python_tutorial_task.py*übergeben werden:

1. **Dateipfad**: Dies ist der lokale Pfad zu der Datei, wie sie auf dem Knoten vorhanden sind. Wenn die ResourceFile Objekt `upload_file_to_container` erstellt wurde in Schritt2 oben der Dateinamen für diese Eigenschaft verwendet wurde (die `file_path` Parameter im Konstruktor ResourceFile). Dies zeigt an, dass die Datei im selben Verzeichnis auf den Knoten als *python_tutorial_task.py*gefunden werden kann.

2. **NumWords**: die obersten *N* Wörter in der Ausgabedatei geschrieben werden sollen.

3. **StorageAccount**: der Name des Kontos Speicher, die im Container besitzt, der die Ausgabe der Aufgabe hochgeladen werden soll.

4. **Storagecontainer**: der Name des Containers Speicher, dem die Ausgabedateien hochgeladen werden soll.

5. **Sastoken**: die freigegebenen Access Signatur (SAS), die Schreibzugriff auf den Container **Ausgabe** in Azure-Speicher bereitstellt. Das Skript *python_tutorial_task.py* verwendet diese gemeinsamen Zugriff Signatur bei seinen BlockBlobService Verweis erstellt. Dies stellt Schreibzugriff auf den Container ohne eine Tastenkombination für das Speicherkonto.

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Schritt 6: Überwachen von Aufgaben

![Überwachen von Aufgaben][6]<br/>
*Das Skript (1) überwacht Aufgaben aus, um den Status der Fertigstellung und (2) die Aufgaben Ergebnisdaten auf Azure-Speicher hochladen*

Wenn Aufgaben mit einem Projekt hinzugefügt haben, werden sie automatisch in der Warteschlange und auf Datenverarbeitungsknoten im Pool zugeordnet den Auftrag für die Ausführung geplant. Je nach den Einstellungen, die Sie angeben, übernimmt Stapel alle Vorgang queuing, Planung, Wiederholung und anderen Vorgang Administration Aufgaben für Sie an.

Es gibt viele Vorgehensweisen für die Überwachung der Ausführung der Aufgabe ein. Die `wait_for_tasks_to_complete` -Funktion in *python_tutorial_client.py* bietet ein einfaches Beispiel für die Überwachung Aufgaben für einen bestimmten Zustand in diesem Fall die [abgeschlossen] [ py_taskstate] Zustand.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Schritt 7: Herunterladen Sie Vorgang Ausgabe

![Herunterladen der Aufgabe Ausgabe von Speicher][7]<br/>

Jetzt, da der Job abgeschlossen ist, kann die Ausgabe von Aufgaben aus Azure-Speicher heruntergeladen werden. Dies erfolgt mit einem Anruf, um `download_blobs_from_container` in *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [AZURE.NOTE] Den Anruf an die `download_blobs_from_container` in *python_tutorial_client.py* gibt an, dass die Dateien in Ihrem home-Verzeichnis heruntergeladen werden sollen. Diese Ausgabeort ändern können.

## <a name="step-8-delete-containers"></a>Schritt 8: Löschen Container

Da Sie Daten, die in Azure Storage gespeichert ist berechnet werden, ist es immer eine gute Idee, alle Blobs zu entfernen, die für Ihre Aufträge Stapel nicht mehr benötigt werden. In *python_tutorial_client.py*, geschieht dies mit drei Anrufe an [BlockBlobService.delete_container][py_delete_container]:

```
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a>Schritt 9: Löschen Sie den Auftrag und dem pool

Im letzten Schritt werden Sie aufgefordert, löschen Sie den Auftrag und dem Pool, die vom Skript *python_tutorial_client.py* erstellt wurden. Obwohl Sie für Projekte und Vorgänge selbst, Sie *sind* keine entrichten müssen Datenverarbeitungsknoten in Rechnung gestellt. Auf diese Weise wird empfohlen, dass Sie Knoten bei Bedarf nur zuweisen. Löschen nicht verwendeter Pools kann Teil Ihrer Verwaltungsvorgang sein.

Die BatchServiceClients [JobOperations] [ py_job] und [PoolOperations] [ py_pool] beide verfügen über eine entsprechende Löschvorgang Methoden, mit denen aufgerufen werden, wenn Sie den Löschvorgang zu bestätigen:

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [AZURE.IMPORTANT] Denken Sie daran, die Sie unterliegen für berechnen Ressourcen – löschen nicht verwendeter Pools Kosten minimieren beibehalten. Beachten Sie auch, dass ein Ressourcenpool alle Computeknoten in diesem Pool löschen, löschen und nach dem Löschen der Ressourcenpool alle Daten auf den Knoten können nicht wiederhergestellt werden können, die.

## <a name="run-the-sample-script"></a>Führen Sie das Beispielskript

Wenn Sie das Skript *python_tutorial_client.py* aus der zusammengehörenden [Code Stichprobe]ausführen[github_article_samples], die Ausgabe in der Konsole ähnelt dem folgenden. Es gibt eine Pause am `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` während des Pool Datenverarbeitungsknoten erstellt werden, wird gestartet, und die Befehle in den Ressourcenpool des Start-Aufgabe ausgeführt werden. Verwenden der [Azure-Portal] [ azure_portal] zum Überwachen der Ressourcenpool zu berechnen Knoten, Position und Aufgaben während und nach der Ausführung. Verwenden der [Azure-Portal] [ azure_portal] oder der [Microsoft Azure-Speicher-Explorer] [ storage_explorer] die Ressourcen Speicher (Container und Blobs) anzeigen möchten, die von der Anwendung erstellt werden.

>[AZURE.TIP] Führen Sie das Skript *python_tutorial_client.py* innerhalb der `azure-batch-samples/Python/Batch/article_samples` Directory. Verwendet einen relativen Pfad für die `common.helpers` Modul importieren, damit Sie sehen, möglicherweise `ImportError: No module named 'common'` , wenn Sie nicht ausführen, die das Skript aus diesem Datenverzeichnis.

Typische dauert Ausführung **etwa 5 bis 7 Minuten** , wenn Sie das Beispiel in die voreingestellte Konfiguration ausführen.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a>Nächste Schritte

*Python_tutorial_client.py* und *python_tutorial_task.py* so experimentieren Sie mit unterschiedlichen berechnen Szenarien ändern können. Beispielsweise versuchen Sie, eine Verzögerung Ausführung *python_tutorial_task.py* simulieren langer Vorgänge und überwachen sie im Portal hinzufügen. Versuchen Sie es weitere Aufgaben hinzufügen oder die Anzahl der berechnen Knoten anpassen. Hinzufügen von Logik zum Überprüfen und die Verwendung von einem vorhandenen Pool auf Geschwindigkeit Execution Zeit zulassen.

Nachdem Sie nun mit den grundlegenden Workflow einer Lösung Stapel vertraut sind, ist es Zeit, auf die zusätzliche Features des Diensts Stapel befasst.

- Überprüfen Sie den Artikel [Übersicht der Azure Stapel Features](batch-api-basics.md) Es empfiehlt sich, wenn Sie den Dienst neu ist.
- Starten Sie auf den anderen Stapel Entwicklung Artikeln in der **Entwicklung detaillierter** in den [Stapel learning Path][batch_learning_path].
- Auschecken einer anderen Implementierung Verarbeitung die Arbeitsbelastung "Top N Wörter" mit Blattnamen in der [TopNWords] [ github_topnwords] Stichprobe.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage

[pypi_install]: http://python-packaging-user-guide.readthedocs.io/en/latest/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Erstellen von Containern in Azure-Speicher"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Hochladen von Vorgang Anwendung und Eingabe (Daten) Dateien zu Containern"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Erstellen Sie Stapel Ressourcenpool"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Stapelverarbeitung erstellen"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Hinzufügen von Aufgaben zum Projekt"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Überwachen von Aufgaben"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Herunterladen der Aufgabe Ausgabe von Speicher"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Stapel Lösung Workflow (vollständige Diagramm)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Stapel Anmeldeinformationen-Portal"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Speicher Anmeldeinformationen-Portal"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Stapel Lösung Workflow (minimale Diagramm)"
