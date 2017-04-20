<properties
    pageTitle="Melden Sie sich an eine klassische Azure VM | Microsoft Azure"
    description="Verwenden Sie das klassische Azure-Portal zur Anmeldung bei einem Windows-Computer mit dem klassischen Bereitstellungsmodell erstellt."
    services="virtual-machines-windows"
    documentationCenter=""
    authors="cynthn"
    manager="timlt"
    editor="tysonn"
    tags="azure-service-management"/>

<tags
    ms.service="virtual-machines-windows"
    ms.workload="infrastructure-services"
    ms.tgt_pltfrm="vm-windows"
    ms.devlang="na"
    ms.topic="article"
    ms.date="07/28/2016"
    ms.author="cynthn"/>


# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-classic-portal"></a>Melden Sie sich bei einem Windows-Computer mithilfe des Azure klassischen-Portals

Im klassischen Azure Portal verwenden Sie die Schaltfläche **Verbinden** zum Starten einer Remotedesktopsitzung, und melden Sie sich an einer Windows-VM.

Möchten Sie die Verbindung mit einer Linux VM? Informationen Sie [zum Anmelden bei einem virtuellen Computer unter Linux](virtual-machines-linux-mac-create-ssh-keys.md).

Hier erfahren Sie, wie [Führen Sie diese Schritte über neue Azure-Portal](virtual-machines-windows-connect-logon.md).

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-classic-include.md)] 

## <a name="video-walkthrough"></a>Video Exemplarische Vorgehensweise

Nachfolgend finden Sie eine video exemplarischen Vorgehensweise die Schritte in diesem Lernprogramm. Dazu gehört auch, Endpunkte und öffentliche und private Ports verwendet, um eine Verbindung mit einem Windows-VM in Azure.

[AZURE.VIDEO logging-on-to-vm-running-windows-server-on-azure]


## <a name="connect-to-the-virtual-machine"></a>Verbinden Sie mit dem virtuellen Computer

1. Melden Sie sich zum klassischen Azure-Portal.

2. Klicken Sie auf **virtuellen Computern**, und wählen Sie dann den virtuellen Computer aus.

3. Klicken Sie auf der Befehlsleiste am unteren Rand der Seite auf **Verbinden**.

    ![Melden Sie sich an dem virtuellen Computer](./media/virtual-machines-windows-classic-connect-logon/connectwindows.png)
    
> [AZURE.TIP] Wenn die Schaltfläche **Verbinden** nicht verfügbar ist, finden Sie unter die Tipps zur Problembehandlung am Ende dieses Artikels.

## <a name="log-on-to-the-virtual-machine"></a>Melden Sie sich an dem virtuellen Computer

[AZURE.INCLUDE [virtual-machines-log-on-win-server](../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Nächste Schritte

-   Wenn die Schaltfläche **Verbinden** inaktiv ist oder andere mit der Remotedesktopverbindung Probleme, versuchen Sie die Konfiguration. Klicken Sie aus dem Dashboard virtuellen Computer unter **Quick im Überblick**, auf **Remotekonfiguration zurückgesetzt**.
-   Versuchen Sie bei Problemen mit Ihrem Kennwort es. Das Dashboard virtuellen Computer unter **Quick im Überblick**, klicken Sie auf **Zurücksetzen des Kennworts**.

Wenn diese Tipps funktionieren nicht oder nicht sind, was Sie benötigen, finden Sie unter [Problembehandlung bei Remotedesktop Verbindungen auf einem Windows-basierten Azure Virtual Machine](virtual-machines-windows-troubleshoot-rdp-connection.md). Dieser Artikel führt Sie durch diagnostizieren und Beheben häufiger Probleme.


