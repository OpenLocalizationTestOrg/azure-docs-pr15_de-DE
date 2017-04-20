<properties 
   pageTitle="Verbinden Sie per Remotezugriff auf Ihr Gerät StorSimple | Microsoft Azure"
   description="Wird erläutert, wie Sie Ihr Gerät für remote-Verwaltung konfigurieren und Herstellen einer Verbindung mit der Windows PowerShell für StorSimple über HTTP oder HTTPS."
   services="storsimple"
   documentationCenter=""
   authors="alkohli"
   manager="carmonm"
   editor="" />
<tags 
   ms.service="storsimple"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="06/21/2016"
   ms.author="alkohli" />

# <a name="connect-remotely-to-your-storsimple-device"></a>Verbinden Sie per Remotezugriff auf Ihr Gerät StorSimple

## <a name="overview"></a>(Übersicht)

Windows PowerShell Remote können Sie eine Verbindung mit Ihrem Gerät StorSimple. Wenn Sie auf diese Weise verbinden, werden Sie kein Menü angezeigt. (Sie ein Menü nur angezeigt, wenn Sie die serielle Konsole auf dem Gerät verwenden, um eine Verbindung herstellen.) Mit Windows PowerShell Remote verbinden Sie mit einer bestimmten Runspace aus. Sie können auch die Anzeigesprache angeben. 

Weitere Informationen zur Verwendung von Windows PowerShell Remote auf Ihrem Gerät zu verwalten, wechseln Sie zum [Verwenden von Windows PowerShell für StorSimple auf Ihrem Gerät StorSimple verwalten](storsimple-windows-powershell-administration.md).

In diesem Lernprogramm wird erläutert, wie Sie Ihr Gerät für remote-Verwaltung konfigurieren und dann Herstellen einer Verbindung mit Windows PowerShell für StorSimple. HTTP oder HTTPS können Sie über Windows PowerShell Remote eine Verbindung herzustellen. Jedoch, wenn Sie der Herstellen einer Verbindung mit Windows PowerShell für StorSimple Entscheidung sind, beachten Sie Folgendes: 

- Herstellen einer Verbindung mit der seriellen Gerät-Konsole direkt sichere ist, aber ist nicht mit der seriellen Konsole über Netzwerk Schalter verbinden. Seien Sie auf das Sicherheitsrisiko, beim Herstellen einer Verbindung zur Gerät serielle Konsole über Netzwerk Schalter. 

- Herstellen einer Verbindung durch eine HTTP-Sitzung bieten möglicherweise mehr Sicherheit als über die serielle Konsole über das Netzwerk verbinden. Auch wenn dies nicht die sicherste Methode ist, ist es auf vertrauenswürdige Netzwerke zulässig. 

- Herstellen einer Verbindung durch eine HTTPS-Sitzung mit ein selbst signiertes Zertifikat ist die sicherste und die empfohlene Option.

Sie können per Remotezugriff auf die Windows PowerShell-Schnittstelle verbinden. Remotezugriff auf Ihrem Gerät StorSimple über die Benutzeroberfläche von Windows PowerShell ist jedoch nicht standardmäßig aktiviert. Sie müssen zuerst aktivieren, remote-Verwaltung auf dem Gerät, und klicken Sie dann auf dem Client, mit dem Ihr Gerät zugreifen.

In diesem Artikel beschriebenen Schritte wurden für eine Host-System unter Windows Server 2012 R2 ausgeführt.

## <a name="connect-through-http"></a>Über HTTP verbunden

Herstellen einer Verbindung mit Windows PowerShell für StorSimple über eine HTTP-Sitzung bietet mehr Sicherheit als über die serielle Konsole Ihres Geräts StorSimple verbinden. Auch wenn dies nicht die sicherste Methode ist, ist es auf vertrauenswürdige Netzwerke zulässig.

Entweder im klassischen Azure-Portal oder die serielle Konsole können Sie remote-Verwaltung konfigurieren. Wählen Sie aus den folgenden Verfahren aus:

- [Verwenden der Azure klassischen Portal remote-Management über HTTP aktivieren](#use-the-azure-classic-portal-to-enable-remote-management-over-http)

- [Verwenden der seriellen Konsole remote-Management über HTTP aktivieren](#use-the-serial-console-to-enable-remote-management-over-http)

Nachdem Sie remote-Verwaltung aktiviert haben, gehen Sie folgendermaßen vor, So bereiten Sie eine Verbindung, die den Client.

- [Vorbereiten des Clients für remote-Verbindung](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a>Verwenden der Azure klassischen Portal remote-Management über HTTP aktivieren 

Führen Sie die folgenden Schritte im klassischen Azure-Portal remote-Management über HTTP aktivieren.

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a>Aktivieren des remote-Verwaltung über die klassischen Azure-portal

1. Zugriff auf **Geräte** > **Konfigurieren** für Ihr Gerät.

2. Führen Sie einen Bildlauf nach unten bis zum Abschnitt **Remote-Verwaltung** .

3. **Aktivieren des Remote-Verwaltung** auf **Ja**festgelegt.

4. Sie können nun auswählen, um eine Verbindung über HTTP. (Die Standardeinstellung ist Verbindung über HTTPS). Stellen Sie sicher, dass HTTP aktiviert ist.

    >[AZURE.NOTE] Herstellen einer Verbindung über HTTP kann nur in vertrauenswürdigen Netzwerken verwendet werden.

6. Klicken Sie auf **Speichern** , am unteren Rand der Seite.

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a>Verwenden der seriellen Konsole remote-Management über HTTP aktivieren

Führen Sie die folgenden Schritte aus, auf das Gerät serielle Konsole remote-Verwaltung aktivieren.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Aktivieren des remote-Verwaltung über das Gerät serielle Konsole

1. Wählen Sie im Menü seriellen Konsole Option 1 aus. Weitere Informationen zur Verwendung der seriellen Konsole auf dem Gerät wechseln Sie zum [Verbinden mit Windows PowerShell für StorSimple über serielle Konsole Gerät](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-device-serial-console).

2. Dazu aufgefordert werden Geben Sie Folgendes ein:`Enable-HcsRemoteManagement –AllowHttp`

3. Sie werden zu Problemen Sicherheit von über HTTP, um eine Verbindung mit dem Gerät benachrichtigt. Wenn Sie dazu aufgefordert werden, bestätigen Sie **J**ein.

4. Vergewissern Sie sich, dass HTTP, indem Sie eingeben aktiviert ist:`Get-HcsSystem`

5. Vergewissern Sie sich, dass das Feld **RemoteManagementMode** **HttpsAndHttpEnabled**zeigt. Die folgende Abbildung zeigt diese Einstellungen in kitten.

     ![Seriell HTTPS oder HTTP aktiviert](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a>Vorbereiten des Clients für remote-Verbindung

Führen Sie die folgenden Schritte aus, auf dem Client remote-Verwaltung zu aktivieren.

#### <a name="to-prepare-the-client-for-remote-connection"></a>So bereiten Sie remote-Verbindung den client

1. Starten einer Sitzung für Windows PowerShell als Administrator an.

2. Geben Sie den folgenden Befehl aus, um die IP-Adresse des Geräts StorSimple des Clients vertrauenswürdige Hosts Liste hinzuzufügen: 

     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`

     Ersetzen Sie <*Device_ip*> durch die IP-Adresse Ihres Geräts; Zum Beispiel: 

     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`

3. Geben Sie den folgenden Befehl aus, um das Gerät Anmeldeinformationen in einer Variablen zu speichern: 

     *$cred = Get-Anmeldeinformationen*

4. Klicken Sie im Dialogfeld, das angezeigt wird:

    1. Geben Sie den Benutzernamen in diesem Format ein: *Device_ip\SSAdmin*.
    2. Geben Sie das Gerät Administrator Kennwort ein, das bei das Gerät mit den Setup-Assistenten konfiguriert wurde eingestellt. Das standardmäßige Kennwort lautet *Kennwort1*.

7. Starten Sie Windows PowerShell-Sitzung auf dem Gerät durch diesen Befehl eingeben:

     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`

     >[AZURE.NOTE] So erstellen Sie eine Windows PowerShell-Sitzung für die Verwendung mit StorSimple virtuelle Gerät Anfügen der `–Port` Parameter, und geben Sie den öffentlichen Port, die Sie für StorSimple virtuelle Einheit in Remote konfiguriert.

     An diesem Punkt sollten Sie eine aktive remote Windows PowerShell-Sitzung auf das Gerät verfügen.

    ![PowerShell Remote über HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Herstellen der Verbindung über HTTPS

Herstellen einer Verbindung mit Windows PowerShell für StorSimple über eine HTTPS-Sitzung ist die sicherste und empfohlene Methode Remote Verbindung mit Ihrem Gerät Microsoft Azure StorSimple. Die folgenden Verfahren erläutert die serielle Konsole und Client-Computer so einrichten, dass Sie HTTPS für StorSimple eine Verbindung zu Windows PowerShell verwenden können.

Entweder im klassischen Azure-Portal oder die serielle Konsole können Sie remote-Verwaltung konfigurieren. Wählen Sie aus den folgenden Verfahren aus:

- [Verwenden der Azure klassischen Portal remote-Management über HTTPS aktivieren](#use-the-azure-classic-portal-to-enable-remote-management-over-https)

- [Verwenden der seriellen Konsole remote-Management über HTTPS aktivieren](#use-the-serial-console-to-enable-remote-management-over-https)

Nachdem Sie remote-Verwaltung aktiviert haben, gehen Sie folgendermaßen vor, Vorbereiten des Hosts remote-Verwaltung und Verbinden mit dem Gerät über remote-Host.

- [Vorbereiten des Hosts für den remote-Verwaltung](#prepare-the-host-for-remote-management)

- [Verbinden Sie mit dem Gerät über remote-host](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a>Verwenden der Azure klassischen Portal remote-Management über HTTPS aktivieren

Führen Sie die folgenden Schritte im klassischen Azure-Portal remote-Management über HTTPS aktivieren.

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a>So aktivieren Sie remote-Management über HTTPS vom klassischen Azure-portal

1. Zugriff auf **Geräte** > **Konfigurieren** für Ihr Gerät.

2. Führen Sie einen Bildlauf nach unten bis zum Abschnitt **Remote-Verwaltung** .

3. **Aktivieren des Remote-Verwaltung** auf **Ja**festgelegt.

4. Sie können nun auswählen, um eine Verbindung mit HTTPS. (Die Standardeinstellung ist Verbindung über HTTPS). Vergewissern Sie sich, dass HTTPS ausgewählt sind. 

5. Klicken Sie auf **Remote-Verwaltungszertifikat herunterladen**. Geben Sie einen Speicherort aus, um diese Datei zu speichern. Sie müssen dieses Zertifikat auf dem Computer Client oder Host installieren, das Sie für die Verbindung mit dem Gerät verwendet wird.

6. Klicken Sie auf **Speichern** , am unteren Rand der Seite.

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a>Verwenden der seriellen Konsole remote-Management über HTTPS aktivieren

Führen Sie die folgenden Schritte auf das Gerät seriellen Konsole remote-Verwaltung zu ermöglichen.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Aktivieren des remote-Verwaltung über das Gerät serielle Konsole

1. Wählen Sie im Menü seriellen Konsole Option 1 aus. Weitere Informationen zur Verwendung der seriellen Konsole auf dem Gerät wechseln Sie zum [Verbinden mit Windows PowerShell für StorSimple über serielle Konsole Gerät](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-device-serial-console).

2. Dazu aufgefordert werden Geben Sie Folgendes ein: 

     `Enable-HcsRemoteManagement`

    Dies sollte HTTPS auf Ihrem Gerät aktivieren.

3. Vergewissern Sie sich, dass HTTPS durch Eingeben der aktiviert wurde: 

     `Get-HcsSystem`

    Vergewissern Sie sich, dass das Feld **RemoteManagementMode** **HttpsEnabled**zeigt. Die folgende Abbildung zeigt diese Einstellungen in kitten.

     ![Serielle HTTPS aktiviert](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)

4. Aus der Ausgabe von `Get-HcsSystem`, kopieren Sie die fortlaufende Zahl des Geräts und zur späteren Verwendung zu speichern.

    >[AZURE.NOTE] Die fortlaufende Zahl ist der Name CN im Zertifikat zugeordnet.

5. Fordern Sie ein Zertifikat remote-Verwaltung, indem Sie eingeben: 
 
     `Get-HcsRemoteManagementCert`

    Ein Zertifikat ähnlich wie der folgende wird angezeigt.

    ![Remote-Verwaltungszertifikat abrufen](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)

5. Kopieren Sie die Informationen in das Zertifikat aus **---beginnen Zertifikat---** **---** enden Zertifikat (...) in einem Text-Editor wie Editor, und speichern Sie diese als CER-Datei. (Kopieren Sie diese Datei auf Ihren remote Host beim Vorbereiten des Hosts.)

    >[AZURE.NOTE] Um ein neues Zertifikat generieren, verwenden Sie die `Set-HcsRemoteManagementCert` Cmdlet.

### <a name="prepare-the-host-for-remote-management"></a>Vorbereiten des Hosts für den remote-Verwaltung

Um den Host-Computer eine Verbindung vorzubereiten, der eine HTTPS-Sitzung verwendet wird, führen Sie die folgenden Schritte aus:

- [Importieren Sie die CER-Datei in den Stammspeicher des Clients oder remote-Host](#to-import-the-certificate-on-the-remote-host).

- [Fügen Sie die Gerät fortlaufende Nummern zu der Datei Hosts auf remote-Host](#to-add-device-serial-numbers-to-the-remote-host).

Jeder der folgenden Verfahren wird nachstehend beschrieben.

#### <a name="to-import-the-certificate-on-the-remote-host"></a>So importieren Sie das Zertifikat auf remote-host

1. Mit der rechten Maustaste in der CER-Datei, und wählen Sie aus, **Installieren Sie ein Zertifikat**. Dadurch wird die Zertifikat Import-Assistent gestartet.

    ![Zertifikat-Import-Assistent 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)

2. **Speicherort**wählen Sie **Lokaler Computer**aus, und klicken Sie dann auf **Weiter**.

3. Wählen Sie **Alle Zertifikate in folgendem Speicher**aus, und klicken Sie dann auf **Durchsuchen**. Navigieren Sie zum Stammordner des remote-Host Store, und klicken Sie dann auf **Weiter**.

    ![Zertifikat-Import-Assistent 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)

4. Klicken Sie auf **Fertig stellen**. Eine Nachricht, die besagt, dass der Import erfolgreich war angezeigt.

    ![Zertifikat-Import-Assistent 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a>Hinzufügen von Gerät fortlaufenden Zahlen zum remote-host

1. Starten Sie den Editor als Administrator, und öffnen Sie die Datei Hosts am \Windows\System32\Drivers\etc.

2. Fügen Sie die folgenden drei Einträge zu Ihrer Hostsdatei: **Daten 0 IP-Adresse**, **Controller 0 feste IP-Adresse**und **Controller 1 feste IP-Adresse**.

3. Geben Sie das Gerät fortlaufende Zahl, das Sie zuvor gespeichert haben. Ordnen Sie dies die IP-Adresse, wie in der folgenden Abbildung gezeigt. Anfügen von Controller 0 und 1 Controller **Controller0** und **Controller1** am Ende die fortlaufende Zahl (CN Name).

    ![Hinzufügen von CN Name zur Hostsdatei](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)

4. Speichern der Hostsdatei.

### <a name="connect-to-the-device-from-the-remote-host"></a>Verbinden Sie mit dem Gerät über remote-host

Verwenden von Windows PowerShell und SSL eine SSAdmin Sitzung auf Ihrem Gerät aus einem remote-Host oder Client eingeben. Die Sitzung SSAdmin ordnet die Option 1 im Menü [serielle Konsole](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-device-serial-console) von Ihrem Gerät.

Führen Sie das folgende Verfahren auf dem Computer, von dem Sie die Windows PowerShell-Verbindung vornehmen möchten.

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a>Eine Sitzung SSAdmin auf dem Gerät eingeben, mithilfe von Windows PowerShell und SSL

1. Starten einer Sitzung für Windows PowerShell als Administrator an.

2. Hinzufügen von IP-Adresse des Geräts an den Kunden vertrauenswürdigen Hosts durch eingeben:

     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`

    Wo finde ich <*Device_ip*> die IP-Adresse Ihres Geräts; Zum Beispiel: 

     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`

3. Erstellen Sie einen neuen Eintrag, indem Sie eingeben: 

     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`

    Wo finde ich <*IP-Adresse des Ziels Gerät*> die IP-Adresse der Daten 0 für Ihr Gerät; beispielsweise **10.126.173.90** wie in der vorherigen Abbildung der Hosts-Datei dargestellt. Geben Sie auch das Administratorkennwort für Ihr Gerät aus.

4. Erstellen Sie eine Sitzung, indem Sie eingeben:

     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`

    Müssen Sie für den Parameter - ComputerName in das Cmdlet die <*fortlaufende Zahl des Ziels Gerät*> aus. Diese Seriennummer wurde die IP-Adresse der Daten in der Datei Hosts auf remote-Host 0 zugeordnet. beispielsweise **SHX0991003G44MT** wie in der folgenden Abbildung gezeigt.

5. Type: 

     `Enter-PSSession $session`

6. Sie müssen ein paar Minuten warten, und dann werden Sie mit Ihrem Gerät über HTTPS verbunden sein, über SSL. Eine Meldung wird angezeigt, die angibt, dass Sie mit Ihrem Gerät verbunden sind.

    ![PowerShell Remote mit HTTPS und SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zum [Verwenden von Windows PowerShell zum Verwalten von Ihrem Geräts StorSimple](storsimple-windows-powershell-administration.md).

- Weitere Informationen zum [Verwenden des Diensts StorSimple Manager zum Verwalten von Ihrem Geräts StorSimple](storsimple-manager-service-administration.md).
