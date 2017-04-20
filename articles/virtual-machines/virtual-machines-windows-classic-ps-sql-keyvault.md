<properties
    pageTitle="Konfigurieren von Azure Key Tresor Integration für SQLServer auf virtuellen Computern Azure die (klassisch)"
    description="Erfahren Sie, wie die Konfiguration von SQL Server-Verschlüsselung mit Azure-Taste Tresor automatisieren. In diesem Thema wird erläutert, wie Azure-Taste Tresor Integration mit SQL Server zu verwenden, die zum Erstellen von virtuellen Computern im Bereitstellungsmodell klassischen."
    services="virtual-machines-windows"
    documentationCenter=""
    authors="rothja"
    manager="jhubbard"
    editor=""
    tags="azure-service-management"/>

<tags
    ms.service="virtual-machines-windows"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="vm-windows-sql-server"
    ms.workload="infrastructure-services"
    ms.date="09/26/2016"
    ms.author="jroth"/>

# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-vms-classic"></a>Konfigurieren von Azure Key Tresor Integration für SQLServer auf virtuellen Computern Azure die (klassisch)

> [AZURE.SELECTOR]
- [Ressourcenmanager](virtual-machines-windows-ps-sql-keyvault.md)
- [Klassische](virtual-machines-windows-classic-ps-sql-keyvault.md)

## <a name="overview"></a>(Übersicht)
Es gibt verschiedene SQL Server Verschlüsselungsfeatures wie [transparent-Verschlüsselung (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [Spalte Ebene Verschlüsselung (Gitternetz)](https://msdn.microsoft.com/library/ms173744.aspx)und [zusätzliche Verschlüsselung](https://msdn.microsoft.com/library/dn449489.aspx). Diese Formen von Verschlüsselung ist es erforderlich, verwalten und speichern die cryptographic Tasten, die Sie für die Verschlüsselung verwenden. Der Dienst Azure Schlüssel Tresor (AKV) Dient zur Verbesserung der Sicherheit und Verwaltung der folgenden Schlüssel an einem sicheren und hochgradig verfügbaren Speicherort. Der [SQL Server-Connector](http://www.microsoft.com/download/details.aspx?id=45344) ermöglicht SQL Server, um diese Schlüssel aus Azure-Taste Tresor verwenden.

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)]

Wenn Sie SQL Server mit dem lokalen Computer ausgeführt werden, sind [Schritte können zum Azure Schlüssel Tresor von Ihrem lokalen SQL Server-Computer zugreifen](https://msdn.microsoft.com/library/dn198405.aspx). Aber für SQL Server in Azure-virtuellen Computern, können Sie Zeit sparen, mit dem Feature *Azure Schlüssel Tresor Integration* . Mit wenigen Azure PowerShell-Cmdlets dieses Feature aktivieren können Sie die Konfiguration für einen SQL-VM zum Zugreifen auf Ihre Key Tresor notwendigen automatisieren.

Wenn dieses Feature aktiviert ist, es automatisch der SQL Server-Connector installiert, konfiguriert den EKM-Anbieter, um die Taste Tresor Azure zugreifen und erstellt die Anmeldeinformationen, damit Sie Ihre Tresor zugreifen können. Wenn Sie sich die Schritte in der Dokumentation oben erwähnten lokalen ansehen, können Sie sehen, dass dieses Feature die Schritte 2 und 3 Automatisierung. Lediglich, die Sie noch müssen manuell vornehmen möchten, besteht darin, die wichtigsten Tresor oder die Taste zu erstellen. Hier wird die gesamte Einrichtung von Ihrer SQL-VM automatisierte. Wenn dieses Feature dieses Setup abgeschlossen ist, können Sie T-SQL-Anweisungen zum Verschlüsseln der Datenbanken oder Sicherungen wie gewohnt beginnen ausführen.

[AZURE.INCLUDE [AKV Integration Prepare](../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a>Konfigurieren von AKV-Integration
Verwenden von PowerShell Azure-Taste Tresor Integration konfigurieren. Die folgenden Abschnitte enthalten eine Übersicht über die erforderlichen Parameter, und klicken Sie dann ein Beispiel PowerShell-Skript.

### <a name="install-the-sql-server-iaas-extension"></a>Installieren Sie die SQL Server IaaS-Erweiterung

[Installieren Sie die SQL Server IaaS Erweiterung](virtual-machines-windows-classic-sql-server-agent-extension.md)zuerst.

### <a name="understand-the-input-parameters"></a>Verstehen der Eingabeparameter
Der folgenden Tabelle sind die Parameter, die zum Ausführen des PowerShell-Skripts im nächsten Abschnitt erforderlich.

|Parameter|Beschreibung|Beispiel|
|---|---|---|
|**$akvURL**|**Die wichtigsten Tresor-URL**|"https://contosokeyvault.vault.azure.net/"|
|**$spName**|**Dienst Tilgungsanteile Namen**|"fde2b411 - 33d 5-4e11-af04eb07b669ccf2"|
|**$spSecret**|**Dienst Tilgungsanteile geheim**|"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM ="|
|**$credName**|**Anmeldeinformationen Namen**: AKV Integration erstellt einen Eintrag in SQL Server verschoben, sodass den virtuellen Computer auf die wichtigsten Tresor zugreifen. Wählen Sie einen Namen für diese Anmeldeinformationen ein.|"mycred1"|
|**$vmName**|**Name des virtuellen Computers**: den Namen einer zuvor erstellten SQL VM.|"Myvmname"|
|**$serviceName**|**Service Name**: Name der Cloud-Dienst, der mit der SQL-VM verknüpft ist.|"Mycloudservicename"|

### <a name="enable-akv-integration-with-powershell"></a>Aktivieren Sie die AKV Integration mit PowerShell
Das Cmdlet **AzureVMSqlServerKeyVaultCredentialConfig neu** erstellt ein Konfigurationsobjekt für die Integration von Azure-Taste Tresor. Die **Set-AzureVMSqlServerExtension** konfiguriert diese Integration mit dem Parameter **KeyVaultCredentialSettings** . Die folgenden Schritte zeigen, wie diese Befehle verwenden möchten.

1. Azure PowerShell zuerst konfigurieren Sie die Eingabeparameter mit Ihren Werten für bestimmten wie in den vorherigen Abschnitten dieses Themas beschrieben. Das folgende Skript ist ein Beispiel.

        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2.  Verwenden Sie dann das folgende Skript zu konfigurieren, und aktivieren Sie die Integration von AKV.

        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

Die SQL-IaaS-Agent-Erweiterung wird die SQL VM mit dieser neuen Konfiguration aktualisiert.

[AZURE.INCLUDE [AKV Integration Next Steps](../../includes/virtual-machines-sql-server-akv-next-steps.md)]
