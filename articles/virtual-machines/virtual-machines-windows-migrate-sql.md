<properties
    pageTitle="Migrieren eine SQL Server-Datenbank in SQL Server auf einem virtuellen Computer | Microsoft Azure"
    description="Informationen Sie zum Migrieren einer lokalen Benutzerdatenbank zu SQL Server in einer Azure-virtueller Computer."
    services="virtual-machines-windows"
    documentationCenter=""
    authors="sabotta"
    manager="jhubbard"
    editor=""
    tags="azure-service-management" />
<tags
    ms.service="virtual-machines-windows"
    ms.workload="infrastructure-services"
    ms.tgt_pltfrm="vm-windows-sql-server"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/26/2016"
    ms.author="carlasab"/>


# <a name="migrate-a-sql-server-database-to-sql-server-in-an-azure-vm"></a>Migrieren einer SQL Server-Datenbank in SQL Server in einer VM Azure

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]Ressourcen-Manager-Modell.


Es gibt eine Reihe von Methoden für die Migration von einer lokalen SQL Server-Benutzer-Datenbank zu SQL Server in einer Azure VM. In diesem Artikel wird kurz erläutern verschiedenen Methoden, empfiehlt sich am besten für verschiedene Szenarien und ein [Lernprogramm](#azure-vm-deployment-wizard-tutorial) um Schritt für Schritt durch Verwendung der Assistent für das **Deployment einer SQL Server-Datenbank an eine Microsoft Azure Virtual Machine** einschließen. 

Die Methode mit dem **Bereitstellen einer SQL Server-Datenbank an eine Microsoft Azure Virtual Machine** -Assistenten im [Lernprogramm](#azure-vm-deployment-wizard-tutorial) beschrieben ist für nur dem klassischen Bereitstellungsmodell. 

## <a name="what-are-the-primary-migration-methods"></a>Was sind die primären Migrationsmethoden?

Die primäre Migrationsmethoden werden:

- Bereitstellen einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten verwenden
- Führen Sie lokale Sicherung Komprimierung und kopieren Sie die Sicherungsdatei manuell in der Azure-virtueller Computer
- Führen Sie eine Sicherung von der URL-URL und die Wiederherstellung in der Azure-virtueller Computer
- Trennen Sie und kopieren Sie die Daten und-Protokolldateien auf Azure BLOB-Speicher und klicken Sie dann auf SQL Server in Azure VM von URL anfügen
- Konvertieren von lokalen physischen Computer in Hyper-V VHD, Hochladen in Azure BLOB-Speicher und anschließendes bereitstellen wie VHD neue VM mit hochgeladen werden.
- Liefern Sie Festplatte mithilfe von Windows-Import/Export-Dienst
- Wenn Sie einer AlwaysOn-Bereitstellung: lokal, verwenden Sie den [Assistenten zum Hinzufügen eines Azure-Replikat](virtual-machines-windows-classic-sql-onprem-availability.md) beim Erstellen eines Replikats in Azure und klicken Sie dann auf Failover, die Benutzer auf der Azure-Datenbank-Instanz zeigt
- Verwenden Sie SQL Server- [Transaktionen Replikation](https://msdn.microsoft.com/library/ms151176.aspx) zum Konfigurieren von Azure SQL Server-Instanz als Abonnent und deaktivieren Sie dann auf Benutzer auf der Azure-Datenbank-Instanz zeigt-Replikation



## <a name="choosing-your-migration-method"></a>Auswählen der Migrationsmethode

Für eine optimale Leistung Übertragung ist die Migration der Datenbankdateien in der Azure-VM mithilfe einer komprimierten Sicherungsdatei in der Regel die beste Methode. Dies ist die Methode, die das [Bereitstellen einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten](#azure-vm-deployment-wizard-tutorial) verwendet. Dieser Assistent ist die empfohlene Methode für die Migration einer lokalen Benutzer Datenbank ausgeführt, die auf SQL Server 2005 oder höher, um SQL Server 2014 oder größer, wenn die Sicherungsdatei komprimierte Datenbank kleiner als 1 TB ist.

Verwenden Sie zum Minimieren der Ausfallzeit während des Migrationsprozesses Datenbank, entweder die Option AlwaysOn oder transaktionale Replikation.

Ist es nicht möglich, die oben beschriebenen Methoden verwenden, manuell migrieren Sie Ihrer Datenbank. Mit dieser Methode werden im Allgemeinen beginnen Sie mit einer gefolgt von einer Kopie der datenbanksicherung der Datenbank in Azure backup, und führen Sie dann eine Wiederherstellung der Datenbank. Sie können auch die Datenbankdateien selbst in Azure kopieren und klicken Sie dann anfügen. Es gibt mehrere Methoden mit denen dieser manuellen Prozess der zum Migrieren einer Datenbank in eine VM Azure ausgeführt werden können.

> [AZURE.NOTE] Wenn Sie auf SQL Server 2014 oder SQL Server 2016 aus älteren Versionen von SQL Server aktualisieren, sollten Sie erwägen, ob Änderungen erforderlich sind. Es wird empfohlen, dass Sie alle abhängig von der neuen Version von SQL Server als Teil Ihres Migrationsprojekts nicht unterstützte Features beheben. Weitere Informationen zu den unterstützten Editionen und Szenarien finden Sie unter [Aktualisieren auf SQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

In der folgenden Tabelle werden die einzelnen die primäre Migrationsmethoden aufgeführt und erläutert, wenn die Verwendung der einzelnen Methoden am besten geeignet ist.

| Methode  | Version der Quelldatenbank  |  Version der Zieldatenbank | Quelle Datenbank Sicherungsgröße Einschränkung  | Notizen  |
|---|---|---|---|---|
| [Bereitstellen einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten verwenden](#azure-vm-deployment-wizard-tutorial) | SQLServer 2005 oder höher | SQLServer 2014 oder höher | < 1 TB  | Schnellste und einfachste Methode, verwenden Sie nach Möglichkeit zum Migrieren zu einer neuen oder vorhandenen SQL Server-Instanz in einer Azure-virtueller Computer | 
| [Verwenden der Azure Replikat Assistent zum Hinzufügen von](virtual-machines-windows-classic-sql-onprem-availability.md) | SQLServer 2012 oder höher | SQLServer 2012 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Minimiert Ausfallzeiten Verwendung bei eine AlwaysOn lokale Bereitstellung. |
| [Verwenden Sie transaktionale SQL Server-Replikation](https://msdn.microsoft.com/library/ms151176.aspx) | SQLServer 2005 oder höher | SQLServer 2005 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Verwenden, wenn Sie benötigen, um Ausfallzeiten zu minimieren und keine AlwaysOn lokale Bereitstellung |
| [Führen Sie lokale Sicherung Komprimierung und manuell kopieren Sie die Sicherungsdatei in der Azure-virtuelle Computer](#backup-to-file-and-copy-to-vm-and-restore) | SQLServer 2005 oder höher | SQLServer 2005 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Verwenden Sie nur beim können nicht verwenden Sie den Assistenten, wie beispielsweise, wenn die Version der Datenbank kleiner als SQL Server 2012 SP1 CU2 ist oder die Sicherung Datenbankgröße ist größer als 1 TB (12,8 TB mit SQL Server 2016) |
| [Führen Sie eine Sicherung von der URL-URL und die Wiederherstellung in der Azure-virtueller Computer](#backup-to-url-and-restore) | SQL Server 2012 SP1 CU2 oder höher | SQL Server 2012 SP1 CU2 oder höher | < 12,8 TB für SQL Server 2016, andernfalls < 1 TB | In der Regel mit [der Sicherung auf URL](https://msdn.microsoft.com/library/dn435916.aspx) ist in Leistung und mit dem Assistenten entspricht und nicht so einfach |
| [Trennen und kopieren Sie die Daten und-Protokolldateien auf Azure BLOB-Speicher und klicken Sie dann über eine Verbindung mit SQL Server in Azure-virtueller Computer URL](#detach-and-copy-to-url-and-attach-from-url) | SQLServer 2005 oder höher | SQLServer 2014 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Verwenden Sie diese Methode, wenn Sie, [diese Dateien mithilfe des Diensts für Azure Blob-Speicher zu speichern planen](https://msdn.microsoft.com/library/dn385720.aspx) und an SQL Server anfügen, die in einer VM Azure, insbesondere mit sehr große Datenbanken |
| [Konvertieren der lokale Computer in Hyper-V VHDs Hochladen in Azure BLOB-Speicher und anschließendem Bereitstellen eines neuen virtuellen Computers mit hochgeladenen VHD](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) | SQLServer 2005 oder höher | SQLServer 2005 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Wird verwendet, wenn Datenbanken im Rahmen der Migration der Datenbank hängt von anderen Benutzerdatenbanken und/oder -Systemdatenbanken zusammen [bringt eine eigene SQL Server-Lizenz](../sql-database/sql-database-paas-vs-sql-server-iaas.md), beim Migrieren einer Datenbank, die Sie bei der Migration von System- und Benutzerinformationen auf einer älteren Version von SQL Server oder ausgeführt wird. |
| [Liefern Sie Festplatte mithilfe von Windows-Import/Export-Dienst](#ship-hard-drive) | SQLServer 2005 oder höher | SQLServer 2005 oder höher | [Azure VM Speichergrenzwert](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Verwenden der [Windows-Import/Export-Dienst](../storage/storage-import-export-service.md) beim manuellen Copy-Methode zu langsam, z. B. mit sehr große Datenbanken ist |

## <a name="azure-vm-deployment-wizard-tutorial"></a>Azure VM Bereitstellung Assistenten Lernprogramm

Verwenden Sie den **Bereitstellen einer SQL Server-Datenbank an eine Microsoft Azure Virtual Machine** -Assistenten in Microsoft SQL Server Management Studio zum Migrieren einer SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, SQL Server 2012, SQL Server 2014 oder SQL Server 2016 lokale Benutzer-Datenbank (bis zu 1 TB) an SQL Server 2014 oder SQL Server 2016 in einer Azure-virtueller Computer. Mithilfe dieses Assistenten zum Migrieren einer Benutzerdatenbank an eine vorhandene Azure-virtueller Computer oder an eine VM Azure mit SQL Server während des Migrationsvorgangs vom Assistenten erstellt. Beim Migrieren einer Datenbank auf eine neuere Version von SQL Server wird die Datenbank während des Aktivierungsvorgangs automatisch aktualisiert.

Die Methode ist für nur dem klassischen Bereitstellungsmodell. 

### <a name="get-latest-version-of-the-deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a>Neueste Version Bereitstellen einer SQL Server-Datenbank auf einem Microsoft Azure VM Assistenten abgerufen.

Verwenden Sie die neueste Version von Microsoft SQL Server Management Studio für SQL Server, um sicherzustellen, dass Sie die neueste Version des Assistenten zum **Bereitstellen einer SQL Server-Datenbank an eine Microsoft Azure Virtual Machine** verfügen. Die neueste Version des Assistenten beinhaltet die aktuellsten Updates Azure klassische-Portal und unterstützt die neuesten Azure VM Bilder in der Galerie (ältere Versionen des Assistenten funktioniert möglicherweise nicht). Rufen Sie die neueste Version der Microsoft SQL Server Management Studio für SQL Server, [Laden Sie sie herunter](http://go.microsoft.com/fwlink/?LinkId=616025) , und installieren es auf einem Clientcomputer mit Verbindung mit der Datenbank aus, Sie zu migrieren und mit dem Internet.

### <a name="configure-the-existing-azure-virtual-machine-and-sql-server-instance-if-applicable"></a>Konfigurieren Sie die vorhandenen Azure virtuellen Computer und SQL Server-Instanz (falls zutreffend)

Wenn Sie eine Migration zu einer vorhandenen Azure VM sind, sind die folgenden Konfigurationsschritte erforderlich:

- Konfigurieren Sie die VM Azure und SQL Server-Instanz, um die Konnektivität von einem anderen Computer zu aktivieren, indem Sie die Schritte zum [Verbinden mit der SQL Server-VM-Instanz SSMS auf einem anderen Computer](virtual-machines-windows-sql-connect.md). Nur die SQL Server 2014 und SQL Server 2016 Bilder im Katalog werden unterstützt, wenn Sie mit dem Assistenten migrieren.
- Konfigurieren Sie einen open Endpunkt für den Dienst SQL Server-Cloud-Adapter für die Microsoft Azure-Gateway mit privaten 11435-Port. Dieser Port wird als Teil des SQL Server 2014 oder SQL Server 2016 Bereitstellung auf einem Microsoft Azure VM erstellt. Der Cloud Adapter erstellt auch eine Windows-Firewall-Regel, um eingehenden TCP-Verbindungen unter Standardport 11435 zu ermöglichen. In diesem Endpunkt ermöglicht des Assistenten, um die Adapter Cloud-Dienst zum Kopieren der Sicherungsdateien aus der lokalen Instanz der Azure-VM verwenden. Weitere Informationen finden Sie unter [Cloud Adapter für SQL Server](https://msdn.microsoft.com/library/dn169301.aspx).

    ![Erstellen von Cloud-Adapter](./media/virtual-machines-windows-migrate-sql/cloud-adapter-endpoint.png)

### <a name="run-the-use-the-deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a>Führen Sie der Verwendung der Bereitstellung einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten

1. Öffnen Sie Microsoft SQL Server Management Studio für Microsoft SQL Server 2016 und Verbinden mit SQL Server-Instanz enthält die Benutzerdatenbank, die Sie für eine VM Azure migrieren.
2. Mit der rechten Maustaste in der Datenbank, die Sie migrieren, zeigen Sie auf Tasks, und klicken Sie dann auf in eine Microsoft Azure Virtual Machine bereitstellen.

    ![Start-Assistent](./media/virtual-machines-windows-migrate-sql/start-wizard.png)

3. Klicken Sie auf der Seite Einführung auf Weiter.
4. Verbinden Sie auf der Seite Einstellungen der Quelle mit SQL Server-Instanz mit der Datenbank, die Sie beabsichtigen, um eine VM Azure migrieren.
5. Geben Sie einen temporären Speicherort für die Sicherungsdateien. Wenn eine Verbindung zu einem Remoteserver herstellen, müssen Sie ein Netzlaufwerk angeben.

    ![Für Datenquellen](./media/virtual-machines-windows-migrate-sql/source-settings.png)

6. Klicken Sie auf Weiter.
7. Klicken Sie auf der Seite Microsoft Azure-Anmeldung auf anmelden und Azure-Konto anmelden.
8. Wählen Sie das Abonnement, das Sie verwenden möchten, verwenden Sie und klicken Sie auf Weiter.

    ![Azure-Anmeldung](./media/virtual-machines-windows-migrate-sql/azure-signin.png)

9. Sie können auf der Seite Einstellungen für die Bereitstellung einer neuen oder einen vorhandenen Cloud-Dienst angeben Name und der Name des virtuellen Computers:

 - Geben Sie einen neuen Namen von Cloud- und virtuellen Computer Namen erstellen einen neuen Cloud-Dienst mit eine neue Azure-virtueller Computer mit einem SQL Server 2014 oder SQL Server 2016 Gallery Image.

     - Wenn Sie einen neuen Namen für die Cloud-Dienst angeben, geben Sie das Speicherkonto, das Sie verwenden möchten.

     - Wenn Sie einen vorhandenen Cloud-Dienst Namen angeben, wird das Speicherkonto abgerufen und eingegeben werden.

 - Geben Sie einen vorhandenen Cloud-Dienst und neuen virtuellen Computernamen um eine neue Azure-virtueller Computer in einem vorhandenen Cloud-Dienst zu erstellen. Nur angegeben Sie ein SQL Server 2014 oder SQL Server 2016 Gallery Bild wird.
 - Geben Sie einen vorhandenen Cloud-Dienst-Name und der Name des virtuellen Computers zu einen vorhandenen Azure-virtueller Computer verwenden. Dabei muss es sich um ein Bild mithilfe von SQL Server 2014 oder SQL Server 2016 Bild erstellt.

        ![Deployment Settings](./media/virtual-machines-windows-migrate-sql/deployment-settings.png)

10. Klicken Sie auf Einstellungen
  - Wenn Sie einen vorhandenen Cloud-Dienst-Name und der Name des virtuellen Computers angegeben, werden Sie aufgefordert, den Benutzernamen und das Kennwort bereitzustellen.

        ![Azure-Computer-Einstellungen](./media/virtual-machines-windows-migrate-sql/azure-machine-settings.png)

    - Wenn Sie einen neuen Namen für den virtuellen Computer angegeben, werden Sie aufgefordert, wählen Sie ein Bild aus der Liste der Gallery-Bilder, und geben Sie die folgende Informationen:
      - Bild: Wählen Sie nur SQL Server 2014 oder SQL Server 2016
        - Benutzername
        - Neues Kennwort
        - Kennwort bestätigen
        - Speicherort
        - Briefumschlag Größe.
    - Darüber hinaus auf, um das selbst generierte Zertifikat für diese neue Microsoft Azure Virtual Machine zu akzeptieren, und klicken Sie dann auf OK.

    ![Azure neue Computer-Einstellungen](./media/virtual-machines-windows-migrate-sql/azure-new-machine-settings.png)

11. Geben Sie der Name der Zieldatenbank an, wenn der Name der Quelldatenbank unterscheidet. Wenn die Zieldatenbank bereits vorhanden ist, das System wird automatisch erhöht den Datenbanknamen, anstatt die vorhandene Datenbank überschreiben.
12. Klicken Sie auf Weiter, und klicken Sie dann auf Fertig stellen.

    ![Ergebnisse](./media/virtual-machines-windows-migrate-sql/results.png)

13. Klicken Sie nach Abschluss des Assistenten eine Verbindung mit dem virtuellen Computer, und stellen Sie sicher, dass Ihre Datenbank migriert wurde.
14. Wenn Sie einen neuen virtuellen Computer erstellt, konfigurieren Sie die Azure Virtual Machine und SQL Server-Instanz mithilfe der Schritte zum [Verbinden mit der VM für SQL Server-Instanz SSMS auf einem anderen Computer](virtual-machines-windows-sql-connect.md).

## <a name="backup-to-file-and-copy-to-vm-and-restore"></a>Sicherung auf Datei und Kopieren in die VM und Wiederherstellung

Verwenden Sie diese Methode, wenn Sie nicht das Bereitstellen einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten verwenden können entweder, da Sie zu einer Version von SQL Server vor SQL Server 2014 migrieren oder die Sicherungsdatei größer als 1 TB ist. Wenn Ihre Sicherungsdatei größer als 1 TB ist, müssen Sie es Stripe ändern, weil die maximale Größe eines Datenträgers VM 1 TB ist. Verwenden Sie die folgenden allgemeinen Schritte zum Migrieren einer Benutzerdatenbank, die die Verwendung dieser manuelle Methode:

1.  Führen Sie eine vollständige Sicherung in einen lokalen Ort.
2.  Erstellen oder Hochladen eines virtuellen Computers mit der Version von SQL Server erforderlich.
3.  Setup-Konnektivität basierend auf Ihren Anforderungen. Finden Sie [eine Verbindung mit einem SQL Server virtuellen Computer auf Azure (Ressourcen-Manager)](virtual-machines-windows-sql-connect.md).
4.  Kopieren Sie die Sicherungsdateien in Ihrer VM mit remote Desktop, Windows Explorer oder den Kopierbefehl von einer Befehlszeile aus.

## <a name="backup-to-url-and-restore"></a>Backup-to-URL und Wiederherstellung

Verwenden Sie die [backup-to-URL](https://msdn.microsoft.com/library/dn435916.aspx) -Methode, wenn Sie nicht, da die Sicherungsdatei größer als 1 TB ist und Sie from und to SQL Server 2016 migrieren Bereitstellen einer SQL Server-Datenbank, einem Microsoft Azure VM-Assistenten verwenden können. Für Datenbanken kleiner als 1 TB oder eine Version von SQL Server vor SQL Server 2016 wird die Verwendung des Assistenten empfohlen. Mit SQL Server 2016 sind Stripeset Sicherungssätze werden unterstützt, empfohlene für Leistung und zum Überschreiten der größenbeschränkungen für Nachrichten pro Blob erforderlich sind. Sehr große Datenbanken empfiehlt die Verwendung des [Windows-Import/Export-Dienst](../storage/storage-import-export-service.md) .

## <a name="detach-and-copy-to-url-and-attach-from-url"></a>Trennen und an die URL kopieren und Anfügen von URL

Verwenden Sie diese Methode, wenn Sie, [speichern diese Dateien mithilfe des Diensts für Azure Blob-Speicher planen](https://msdn.microsoft.com/library/dn385720.aspx) und SQL Server, die in einer VM Azure, insbesondere mit sehr große Datenbanken zuordnen. Verwenden Sie die folgenden allgemeinen Schritte zum Migrieren einer Benutzerdatenbank, die die Verwendung dieser manuelle Methode:

1.  Trennen Sie die Datenbankdateien aus der lokalen Datenbank-Instanz.
2.  Kopieren Sie die Datenbankdateien getrennten in Azure Blob-Speicher mit dem [Befehlszeilenprogramm AZCopy](../storage/storage-use-azcopy.md).
3.  Hinzufügen der Datenbankdateien aus dem Azure-URL auf die SQL Server-Instanz in der Azure-VM.

## <a name="convert-to-vm-and-upload-to-url-and-deploy-as-new-vm"></a>Konvertieren von VM und Hochladen in URL und als neue VM bereitstellen

Verwenden Sie diese Methode, um alle System- und Benutzerdatenbanken in einer lokalen SQL Server-Instanz auf Azure-virtueller Computer migrieren. Verwenden Sie die folgenden allgemeinen Schritte zum Migrieren einer gesamten SQL Server-Instanz mit dieser manuelle Methode:

1.  Konvertieren Sie physische oder virtuelle Computer in Hyper-V VHDs mithilfe von [Microsoft Virtual Machine Konverter](http://technet.microsoft.com/library/dn873998.aspx).
2.  Laden Sie VHD-Dateien in Azure-Speicher mit dem [Cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3.  Stellen Sie einen neuen virtuellen Computer mithilfe der hochgeladenen VHD bereit.

> [AZURE.NOTE] Um eine vollständige Anwendung zu migrieren, erwägen Sie [Azure Website Recovery](../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Liefern von Festplatte

Verwenden Sie die [Windows-Import/Export-Dienst-Methode](../storage/storage-import-export-service.md) in Azure Blob-Speicher in Situationen große Datenmengen Datei übertragen wobei Hochladen über das Netzwerk extrem aufwendige oder nicht möglich ist. Mit diesem Dienst senden Sie eine oder mehrere Festplatten mit dieser Daten einer Azure-Rechenzentrum, in dem die Daten zu Ihrem Speicherkonto hochgeladen werden soll.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Ausführen von SQL Server auf virtuellen Azure-Computern finden Sie unter [SQL Server auf virtuellen Azure-Computern Overview](virtual-machines-windows-sql-server-iaas-overview.md).

Anweisungen zum Erstellen einer Azure SQL Server Virtual Machine aus einer erfasste Bild finden Sie unter [Tipps und Tricks zum Klonen' SQL Azure-virtuelle Computer aus erfasste Bilder](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) im Blog CSS SQL Server-Entwickler.
