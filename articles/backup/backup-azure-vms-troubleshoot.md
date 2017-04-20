<properties
    pageTitle="Behandeln von Problemen mit Azure-virtuellen Computern Sicherung | Microsoft Azure"
    description="Behandeln von Problemen mit sichern und Wiederherstellen von Azure-virtuellen Computern"
    services="backup"
    documentationCenter=""
    authors="trinadhk"
    manager="shreeshd"
    editor=""/>

<tags
    ms.service="backup"
    ms.workload="storage-backup-recovery"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="08/26/2016"
    ms.author="trinadhk;jimpark;"/>


# <a name="troubleshoot-azure-virtual-machine-backup"></a>Problembehebung bei der Sicherung von Azure-virtuellen Computern

> [AZURE.SELECTOR]
- [Wiederherstellung Services Tresor](backup-azure-vms-troubleshoot.md)
- [Zusätzliche Tresor](backup-azure-vms-troubleshoot-classic.md)

Sie können Fehler auftreten, während mit Azure Sicherung mit Informationen in der folgenden Tabelle aufgeführten beheben:

## <a name="backup"></a>Sicherung

| Sicherung | Fehlerdetails | Dieses Problem zu umgehen |
| -------- | -------- | -------|
|Sicherung|    Der Vorgang konnte nicht ausgeführt werden, wie virtueller Computer nicht mehr vorhanden sind. -Beenden Sie den Schutz von virtuellen Computern ohne zusätzliche Daten löschen. Weitere Details bei http://go.microsoft.com/fwlink/?LinkId=808124   |Dies geschieht, wenn der primäre virtueller Computer wird gelöscht, aber die Sicherung Richtlinie eines virtuellen Computers weiterhin auszuführenden Sicherung Suchen nach. Um diesen Fehler zu beheben: <ol><li> Erstellen Sie den virtuellen Computer mit demselben Namen und derselben Gruppe Ressourcenname [Name der Cloud-Dienst], neu.<br>(ODER)</li><li> Beenden Sie den Schutz von virtuellen Computern mit oder ohne zusätzliche Daten löschen. [Weitere details](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol>|
|Sicherung|Konnte nicht mit dem virtuellen Computer Agent Antrag auf Snapshot kommunizieren. -Stellen Sie sicher, dass die virtuellen Computer Zugriff auf das Internet ist. Aktualisieren Sie den virtuellen Computer-Agent darüber hinaus, wie die Leitfaden zur Problembehandlung bei http://go.microsoft.com/fwlink/?LinkId=800034 erwähnt |Dieser Fehler wird ausgelöst, wenn es ein Problem mit der Agent virtueller Computer liegt oder Netzwerkzugriff auf die Azure Infrastruktur in irgendeiner Weise blockiert. Erfahren Sie mehr über das Debuggen von virtuellen Computer snapshot-Probleme.<br> Wenn der Agent virtueller Computer nicht Probleme verursacht, starten Sie den virtuellen Computer neu. Manchmal kann ein falscher Zustand für virtuelle Computer Probleme verursachen und einen Neustart von den virtuellen Computer werden diese "schlechten Zustand" zurückgesetzt.|
|Sicherung|    Fehler bei Wiederherstellungsvorgangs Services-Erweiterung -Stellen Sie sicher, dass die neuesten virtuellen Computern Agents auf den virtuellen Computer vorhanden ist, und Agent-Dienst ausgeführt wird. Wiederholen Sie die Sicherung und schlägt fehl, wenden Sie sich an den Microsoft-Support.|   Dieser Fehler wird ausgelöst, wenn virtueller Computer Agent veraltet. Finden Sie im Abschnitt "Aktualisieren der virtuellen Computer Agent" unten, um den virtuellen Computer-Agent aktualisieren.|
|Sicherung |Virtuellen Computern vorhanden nicht. -Bitte stellen Sie sicher, dass die virtuellen Computern vorhanden ist, oder wählen Sie einen anderen virtuellen Computer aus. | Dies geschieht, wenn der primäre virtueller Computer wird gelöscht, aber die Sicherung Richtlinie eines virtuellen Computers weiterhin zu Sicherungskopie Suchen nach. Um diesen Fehler zu beheben: <ol><li> Erstellen Sie den virtuellen Computer mit demselben Namen und derselben Gruppe Ressourcenname [Name der Cloud-Dienst], neu.<br>(ODER)<br></li><li>Beenden Sie den Schutz von virtuellen Computern ohne zusätzliche Daten löschen. [Weitere details](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol>|
|Sicherung |Fehler bei der Ausführung des Befehls. -Ein anderer Vorgang gibt es zurzeit in Bearbeitung für diesen Artikel. Warten Sie, bis der vorherige Vorgang abgeschlossen ist, und wiederholen Sie dann |Eine vorhandene Sicherung oder Wiederherstellungsauftrag für den virtuellen Computer ausgeführt wird und ein neues Projekt kann nicht gestartet werden, während der vorhandene Auftrag ausgeführt wird.|
| Sicherung | Wiederholen Sie virtuelle Festplatten kopieren aus Sicherung Tresor Timeout - den Vorgang in wenigen Minuten. Wenn das Problem weiterhin besteht, wenden Sie sich an den Microsoft-Support. | Dies geschieht, wenn es ist zu viel Daten kopiert werden. Überprüfen Sie, ob Sie weniger als 16 Daten Datenträger verfügen. |
| Sicherung | Fehler bei der Sicherung mit interner Fehler: Führen Sie den Vorgang in wenigen Minuten erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Microsoft-Support | Sie können diesen Fehler 2 Gründen erhalten: <ol><li> Es ist ein vorübergehendes Problem beim Zugriff auf virtuellen Computer Speicher ein. Überprüfen Sie [Azure Status](https://azure.microsoft.com/en-us/status/) , um festzustellen, ob alle laufenden Problem im Zusammenhang mit berechnen/Speicher/Netzwerk in der Region ein. Bitte wird "Wiederholen" die Sicherung Beitrag Problem verringert. <li>Die ursprünglichen virtuellen wurde gelöscht und kann Sicherung kann nicht erstellt werden. Behalten Sie die Daten die Sicherung eines gelöschten virtuellen Computers, aber die Sicherung Fehler beenden, Aufheben des Blattschutzes des virtuellen Computer, und wählen Sie die Option, um die Daten aus. Hiermit wird die Sicherung planen und auch die periodische Fehlermeldungen abgebrochen. |
| Sicherung | Konnte nicht installiert werden die Azure Wiederherstellung Dienste ist Erweiterung für ausgewähltes Element - Agent virtueller Computer eine Vorbedingung für Azure Wiederherstellung Erweiterung aus. Installieren Sie den Agent Azure-virtuellen Computer, und starten Sie den erneut Registrierung | <ol> <li>Überprüfen Sie, ob der virtuellen Computer-Agent ordnungsgemäß installiert wurde. <li>Stellen Sie sicher, dass die Kennzeichnung auf virtuellen Computer Config richtig eingestellt ist.</ol> [Weitere Informationen finden Sie](#validating-vm-agent-installation) Informationen zu virtuellen Computer Agent-Installation, und wie Sie die Installation des virtuellen Computer-Agents überprüfen. |
| Sicherung | Erweiterung Fehler bei der Installation der Fehler "COM + konnte keine Verbindung mit dem Microsoft Distributed Transaktionskoordinator sprechen. | Dies bedeutet normalerweise, dass der Dienst COM + nicht ausgeführt wird. Hilfe zum Beheben dieses Problems wenden Sie sich an Microsoft Support. |
| Sicherung | Snapshot-Vorgang Fehler bei der Vorgang VSS "dieses Laufwerk durch BitLocker Drive Verschlüsselung gesperrt ist. Sie müssen dieses Laufwerk aus Control Panel entsperren. | BitLocker für alle Laufwerke des virtuellen Computers zu deaktivieren Sie, und prüfen Sie, ob das VSS Problem gelöst ist |
| Sicherung | Virtuellen Computern Probleme virtuellen Festplatten auf Premium Storage gespeichert sind für die Sicherung nicht unterstützt. | Keine |
| Sicherung | Azure-virtuellen Computern nicht gefunden. | Dies geschieht, wenn der primäre virtueller Computer wird gelöscht, aber die Sicherung Richtlinie eines virtuellen Computers weiterhin zu Sicherungskopie Suchen nach. Um diesen Fehler zu beheben: <ol><li>Erstellen Sie den virtuellen Computer mit demselben Namen und derselben Gruppe Ressourcenname [Name der Cloud-Dienst], neu. <br>(ODER) <li> Deaktivieren Sie den Schutz für diese virtuellen Computer, sodass die Sicherung Einzelvorgänge nicht erstellt werden </ol> |
| Sicherung | Virtuellen Computern-Agent ist nicht vorhanden ist, auf dem virtuellen Computer – installieren Sie das obligatorische Voraussetzung virtueller Computer-Agent, und starten Sie den erneut. | [Weitere Informationen finden Sie](#vm-agent) Informationen zu virtuellen Computer Agent-Installation, und wie Sie die Installation des virtuellen Computer-Agents überprüfen. |

## <a name="jobs"></a>Aufträge

| Vorgang | Fehlerdetails | Dieses Problem zu umgehen |
| -------- | -------- | -------|
| Auftrag abbrechen | Absage wird für diesen Auftrag nicht unterstützt: warten, bis der Auftrag abgeschlossen ist. | Keine |
| Auftrag abbrechen | Die Position ist nicht in einem Zustand abgebrochen werden: warten, bis der Auftrag abgeschlossen ist. <br>ODER<br> Der ausgewählte Auftrag ist nicht in einem Zustand abgebrochen werden: Warten Sie für das Projekt abgeschlossen.| Aller Wahrscheinlichkeit ist der Job fast abgeschlossen; Warten Sie, bis Auftragsabschluss |
| Auftrag abbrechen | Abbrechen des Auftrags kann nicht, da es nicht in den Fortschritt ist – Absage unterstützt nur für Projekte, die ausgeführt werden. Bitte Versuch Abbrechen auf in Bearbeitung befindlichen Position. | In diesem Fall aufgrund einer vorübergehendes Zustand. Warten Sie eine Minute, und wiederholen Sie den Vorgang abbrechen |
| Auftrag abbrechen | Nicht den Auftrag abbrechen - warten Sie, bis beendet wurde. | Keine |


## <a name="restore"></a>Stellen Sie wieder her
| Vorgang | Fehlerdetails | Dieses Problem zu umgehen |
| -------- | -------- | -------|
| Stellen Sie wieder her | Fehler bei der Wiederherstellung mit Cloud interner Fehler | <ol><li>Cloud-Dienst, dem Sie wiederherstellen möchten, ist mit DNS-Einstellungen konfiguriert. Sie können überprüfen <br>$deployment = "ServiceName" Get-AzureDeployment - ServiceName-Slot "Herstellung" Get-AzureDns - DnsSettings $deployment. DnsSettings<br>Ist Adresse, die so konfiguriert ist, bedeutet dies, dass die DNS-Einstellungen konfiguriert sind.<br> <li>Cloud-Dienst, in die Sie wiederherstellen möchten, die mit reservierte IP-Adressen konfiguriert ist und vorhandene virtuellen Computern in der Cloud-Dienst Zustand beendet werden.<br>Sie können ein Clouddienst IP reserviert hat, mithilfe der folgenden Powershell-Cmdlets prüfen:<br>$deployment = "Servicename" Get-AzureDeployment - ServiceName-Slot "Herstellung" $ Datenausführungsverhinderung. ReservedIPName <br><li>Sie versuchen, einen virtuellen Computer mit folgenden Inhalte Netzwerkkonfigurationen in in derselben Cloud-Service wiederherstellen. <br>-Virtuellen Computern unter Laden Lastenausgleich Konfiguration (interne und externe)<br>-Virtuellen Computern mit mehreren reservierte IP-Adressen<br>-Virtuellen Computern mit mehreren NICs<br>Wählen Sie einen neuen Clouddienst in der Benutzeroberfläche oder Näheres [Wiederherstellen Aspekte](./backup-azure-arm-restore-vms.md/#restoring-vms-with-special-network-configurations) für virtuelle Computer mit speziellen Netzwerkkonfiguration</ol> |
| Stellen Sie wieder her | Der ausgewählte DNS-Name wird bereits verwendet – Geben Sie an einen anderen DNS-Namen, und versuchen Sie es erneut. | Hier der DNS-Name bezieht sich auf den Namen der Cloud-Dienst (in der Regel, die mit. cloudapp.net). Dies muss eindeutig sein. Wenn dieser Fehler auftreten, müssen Sie einen anderen Namen des virtuellen Computers während der Wiederherstellung auswählen. <br><br> Beachten Sie, dass nur für Benutzer von der Azure-Portal dieser Fehler angezeigt wird. Die Wiederherstellung über PowerShell ist erfolgreich, da es nur die Datenträger stellt und nicht den virtuellen Computer erstellen. Der Fehler wird konfrontiert werden, wenn Sie der virtuellen Computer explizit von Ihnen erstellt wurde, nachdem Sie den Datenträger wiederherstellen, Vorgang. |
| Stellen Sie wieder her | Die angegebene virtuelle Netzwerkkonfiguration ist nicht korrekt – Geben Sie an einer anderen virtuellen Netzwerkkonfiguration, und versuchen Sie es erneut. | Keine |
| Stellen Sie wieder her | Angegebenen Cloud-Dienst ist eine reservierte IP-Adresse verwenden, die nicht mit der Konfiguration des virtuellen Computers wiederherzustellende entsprechen – Geben Sie einen anderen Cloud-Service, der nicht reservierte IP verwendet wird, oder wählen Sie aus einer anderen Wiederherstellung, zeigen Sie auf Wiederherstellen aus. | Keine |
| Stellen Sie wieder her | Cloud-Dienst Grenzwert für die Anzahl der Eingabewerte Endpunkte erreicht hat: durch Angeben von einem anderen Cloud-Dienst oder mithilfe eines vorhandenen Endpunkts, wiederholen Sie den Vorgang. | Keine |
| Stellen Sie wieder her | Zusätzliche Tresor und das Ziel Speicher sind in zwei verschiedenen Bereichen: sicherstellen, dass das in der Wiederherstellung angegebene Speicherkonto in der gleichen Azure Region als die Sicherung Tresor ist. | Keine |
| Stellen Sie wieder her | Speicher-Konto für angegebene bei der Wiederherstellung nicht unterstützt - Basic/Standard Speicherkonten mit lokal redundante oder Geo redundante Replikation Einstellungen werden unterstützt. Wählen Sie einen unterstützten Speicher-Konto | Keine |
| Stellen Sie wieder her | Speicher Kontotyp für Wiederherstellungsvorgangs angegeben ist nicht online – stellen Sie sicher, dass das in der Wiederherstellung angegebene Speicherkonto online ist | Dies kann aufgrund einer vorübergehenden Fehler in Azure-Speicher oder aufgrund von einem Ausfall vorkommen. Wählen Sie ein anderes Speicherkonto an. |
| Stellen Sie wieder her | Ressourcengruppe Kontingents erreicht wurde – einige Ressourcengruppen aus Azure-Portal löschen, oder wenden Sie sich an Azure Support, um die Grenzwerte zu vergrößern. | Keine |
| Stellen Sie wieder her | Ausgewählten Subnetz nicht vorhanden - wählen Sie ein Subnetz das vorhanden ist | Keine |


## <a name="policy"></a>Richtlinie
| Vorgang | Fehlerdetails | Dieses Problem zu umgehen |
| -------- | -------- | -------|
| Erstellen der Richtlinie | Fehler beim Erstellen der Richtlinie – reduzieren Sie die Aufbewahrung möglichen Richtlinienkonfiguration fortzusetzen. | Keine |


## <a name="vm-agent"></a>Virtueller Computer-Agents

### <a name="setting-up-the-vm-agent"></a>Einrichten des virtuellen Computer-Agents
In der Regel, die virtuellen Computer-Agent ist bereits in virtuellen Computern, die aus dem Katalog Azure erstellt werden. Virtuellen Computern, die von lokalen Rechenzentren migriert werden müssten allerdings nicht des virtuellen Computer-Agents installiert. Für diese virtuelle Computer muss der Agent virtueller Computer explizit installiert werden. Weitere Informationen zum [Installieren des virtuellen Computer-Agents eines vorhandenen virtuellen Computers](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Für Windows-virtuellen Computern:

- Herunterladen Sie und installieren Sie die [MSI-Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sie benötigen Administratorrechte, um die Installation durchzuführen.
- [Die Eigenschaft virtueller Computer zu aktualisieren](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) , um anzugeben, dass der Agent installiert ist.

Für Linux virtuelle Computer:

- Installieren Sie neueste [Linux Agent](https://github.com/Azure/WALinuxAgent) von Github.
- [Die Eigenschaft virtueller Computer zu aktualisieren](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) , um anzugeben, dass der Agent installiert ist.


### <a name="updating-the-vm-agent"></a>Aktualisieren des virtuellen Computer-Agents
Für Windows-virtuellen Computern:

- Aktualisieren der virtuellen Computer-Agent ist so einfach wie die [virtuellen Computer Agent Binärdateien](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)erneut zu installieren. Jedoch müssen Sie sicherstellen, dass keine zusätzliche Operation ausgeführt wird, während des virtuellen Computer-Agents aktualisiert wird.

Für Linux virtuelle Computer:

- Folgen Sie den Anweisungen auf [Linux virtueller Computer-Agent aktualisieren](../virtual-machines/virtual-machines-linux-update-agent.md).


### <a name="validating-vm-agent-installation"></a>Virtueller Computer Agent Installation wird überprüft.
So aktivieren Sie die virtuellen Computer Agent-Version auf Windows-virtuellen Computern:

1. Melden Sie sich bei der Azure-virtuellen Computern, und navigieren Sie zu dem Ordner *C:\WindowsAzure\Packages*. Suchen Sie die Datei WaAppAgent.exe vorhanden.
2. Mit der rechten Maustaste in der Datei, wechseln Sie zu **Eigenschaften**, und wählen Sie dann auf die Registerkarte **Details** . Das Feld Produktversion sollten 2.6.1198.718 oder höher

## <a name="troubleshoot-vm-snapshot-issues"></a>Behandlung von Problemen beim virtuellen Computer-Snapshot
Virtueller Computer Sicherung beruht auf Ausgabe Momentaufnahme Befehls an zugrunde liegenden Speicher. Ohne Zugriff auf Speicher oder Verzögerung in die Ausführung der Aufgabe Momentaufnahme kann keine Sicherung durchführen. Die folgenden verursachen Snapshot-Vorgang Fehler.

1. Netzwerkzugriff auf Speicher ist gesperrt NSG verwenden<br>
   Erfahren Sie mehr erfahren Sie, wie Sie entweder mithilfe der IP-Adressen mit dem Speicher oder über Proxyserver [Netzwerkzugriff aktivieren](backup-azure-vms-prepare.md#2-network-connectivity) .
2.  Virtueller Computer mit Sql Server-Sicherung konfiguriert können Momentaufnahme Vorgang Verzögerung führen. <br>
    Sichern Sie standardmäßig virtueller Computer Probleme VSS vollständige Sicherung auf Windows-virtuellen Computern aus. Klicken Sie auf virtuellen Computern, die Sql Server ausgeführt werden und SQLServer-Sicherung konfiguriert ist, kann dies Verzögerung in Momentaufnahme Ausführung führen. Legen Sie folgenden Registrierungsschlüssel, wenn Sie zusätzliche Fehler aufgrund Momentaufnahme auftrat.

    ```
    [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
    "USEVSSCOPYBACKUP"="TRUE"
    ```
3.  Virtueller Computer Status gemeldet falsch auf, da virtueller Computer war(en) in RDP ist.  <br>
    Wenn Sie den virtuellen Computern in RDP beenden, überprüfen Sie im Portal zurück, ob virtueller Computer Status ordnungsgemäß wiedergegeben wird. Wenn dies nicht der Fall, beenden Sie den virtuellen Computer im Portal 'War(en)'-Option in Dashboard virtuellen Computer verwenden.
4.  Wenn die gleiche mehr als vier virtuellen Computers freigeben-Dienst Cloud, konfigurieren Sie mehrere zusätzliche Richtlinien zum Phaseneigenschaften der Sicherung Zeiten also nicht mehr als vier virtuellen Computer Sicherungskopien zur gleichen Zeit gestartet werden. Versuchen Sie, die Sicherung starten-Zeiten eine Stunde zwischen Richtlinien auseinander verteilt. 
5.  Virtueller Computer wird bei hoher CPU/Arbeitsspeicher ausgeführt.<br>
    Wenn bei hoher CPU-Auslastung des virtuellen Computers ausgeführt wird usage(>90%) oder Arbeitsspeicher, Momentaufnahme Vorgang ist in der Warteschlange, verzögert und wird später überschritten wird. Führen Sie bei Bedarf die Sicherung in diesen Fällen.

<br>

## <a name="networking"></a>Netzwerke
Wie alle Erweiterungen Sicherung Erweiterung benötigen Zugriff auf das öffentliche Internet entwickelt. Keinen Zugriff auf das öffentliche Internet kann selbst auf vielfältige Weise darstellen:

- Die Erweiterung Installation kann fehl.
- Die Sicherung (wie Datenträger Snapshot) fehlschlagen können
- Anzeigen des Status des Vorgangs Sicherung ein Fehler auftreten können

Hat die Notwendigkeit der öffentlichen Internetadressen beheben formuliert wurde [hier](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). Sie müssen zum Überprüfen der DNS-Konfiguration für die VNET, und stellen Sie sicher, dass die Azure-URIs aufgelöst werden können.

Nachdem Sie die Auflösung ordnungsgemäß vorgenommen wird, muss Zugriff auf die Azure IP-Adressen auch bereitgestellt werden. Zum Aufheben der Blockierung Zugang zur Azure-Infrastruktur, führen Sie einen der folgenden Schritte aus:

1. Weißen Azure Datencenter IP-Bereiche.
    - Abrufen der Liste der [Azure Datacenter IP-Adressen](https://www.microsoft.com/download/details.aspx?id=41653) in der weißen Liste enthalten sein.
    - Aufheben der Blockierung mithilfe des Cmdlets [New-NetRoute](https://technet.microsoft.com/library/hh826148.aspx) IP-Adressen. Führen Sie dieses Cmdlet in den Azure-virtuellen Computer, in einem erhöhten PowerShell-Fenster (als Administrator ausführen) aus.
    - Hinzufügen von Regeln auf das NSG (Wenn Sie eine Organisation vorhanden ist) zum Zulassen des Zugriffs auf die IP-Adressen.
2. Erstellen eines Pfads für HTTP-Datenverkehr
    - Wenn Sie haben einige Einschränkung Network Speicherort (beispielsweise ein Netzwerk Sicherheit Gruppe) ein HTTP-Proxyserver den Datenverkehr weiterleiten bereitstellen. Schritte zum Bereitstellen von eines HTTP-Proxy-Servers finden Sie [hier](backup-azure-vms-prepare.md#2-network-connectivity).
    - Hinzufügen von Regeln auf das NSG (Wenn Sie eine Organisation vorhanden ist) zum Zugreifen auf das INTERNET aus dem HTTP-Proxy dürfen.

>[AZURE.NOTE] DHCP muss innerhalb der Gast für IaaS virtueller Computer Sicherung entwickelt aktiviert sein.  Wenn Sie eine statische private IP-Adresse benötigen, sollten Sie es über die Plattform konfigurieren. Die Option innerhalb des virtuellen Computers sollte links aktiviert sein.
Weitere Informationen zum [Festlegen einer statischen internen privaten IP](../virtual-network/virtual-networks-reserved-private-ip.md)anzeigen
