> [AZURE.SELECTOR]
- [C in Windows](../articles/iot-suite/iot-suite-connecting-devices.md)
- [C unter Linux](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
- [C in mbed](../articles/iot-suite/iot-suite-connecting-devices-mbed.md)
- [Node.js](../articles/iot-suite/iot-suite-connecting-devices-node.md)

## <a name="scenario-overview"></a>Übersicht über das Szenario

In diesem Szenario erstellen Sie ein Gerät, das auf die Remote überwachen [vorkonfigurierte Lösung]die folgenden Telemetrie sendet[lnk-what-are-preconfig-solutions]:

- Externe Temperaturen
- Interne Temperatur
- Luftfeuchtigkeit

Zur Vereinfachung Beispielwerte durch den Code auf dem Gerät wird, aber wir empfehlen Sie das Beispiel zu erweitern, indem eine Verbindung echte Sensoren an Ihr Gerät senden echten Telemetrie.

Um dieses Lernprogramm durchzuführen, benötigen Sie ein aktives Azure-Konto. Wenn Sie nicht über ein Konto verfügen, können Sie ein kostenlose Testversion Konto in ein paar Minuten erstellen. Weitere Informationen hierzu finden Sie unter [Kostenlose Testversion von Azure][lnk-free-trial].

## <a name="before-you-start"></a>Bevor Sie beginnen

Bevor Sie für Ihr Gerät keinen Code schreiben, müssen Sie Ihre remote monitoring vorkonfigurierte Lösung bereitstellen und dann ein neues benutzerdefiniertes Gerät in dieser Lösung bereitstellen.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Stellen Sie Ihre remote monitoring vorkonfigurierte Lösung bereit

Das Gerät Sie in diesem Lernprogramm erstellen sendet Daten an eine Instanz der [Remoteüberwachung] [ lnk-remote-monitoring] vorkonfiguriert Lösung. Wenn Sie bereits im Azure-Konto die remote monitoring vorkonfigurierte Lösung bereitgestellt hatte keine, führen Sie die folgenden Schritte aus:

1. Klicken Sie auf der Seite <https://www.azureiotsuite.com/> auf **+** zum Erstellen einer neuen Lösung.

2. Klicken Sie auf **auswählen** , in der Systemsteuerung **Remoteüberwachung** Ihrer neue Lösung erstellen.

3. Geben Sie auf der Seite **Erstellen Remote monitoring Lösung** einen **Lösungsname** Ihrer Wahl, wählen Sie die **Region** , die Sie bereitstellen möchten, und wählen Sie aus der Azure-Abonnement verwenden möchten. Klicken Sie dann auf **Projektmappe erstellen**.

4. Warten Sie, bis der Bereitstellungsprozess abgeschlossen ist.

> [AZURE.WARNING] Die vorkonfigurierten Lösungen verwenden abzurechnende Azure-Diensten. Achten Sie darauf, dass Ihr Abonnement die vorkonfigurierte Lösung entfernen, wenn Sie damit alle unnötigen Gebühren zu vermeiden fertig sind. Sie können eine vorkonfigurierte Lösung vollständig aus Ihrem Abonnement entfernen, finden Sie auf der Seite <https://www.azureiotsuite.com/> .

Wenn der Bereitstellungsprozess für die remote-Überwachung Lösung abgeschlossen ist, klicken Sie auf **Starten** , um die Lösung Dashboard im Browser zu öffnen.

![][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a>Ihr Gerät in der remote-Überwachung-Solution bereitstellen

> [AZURE.NOTE] Wenn Sie ein Gerät in Ihrer Lösung bereits bereitgestellt haben, können Sie diesen Schritt überspringen. Sie müssen die Anmeldeinformationen Gerät kennen, wenn Sie die Client-Anwendung erstellen.

Für ein Gerät für die Verbindung zu der vorkonfigurierten Lösung muss es sich IoT Hub mit gültige Anmeldeinformationen identifizieren. Sie können die Anmeldeinformationen Gerät aus dem Dashboard Lösung abrufen. Sie haben die Anmeldeinformationen Gerät in der Clientanwendung weiter unten in diesem Lernprogramm einschließen. 

Um ein neues Gerät für Ihre Lösung mit remote monitoring hinzuzufügen, führen Sie die folgenden Schritte im Dashboard Lösung:

1.  Klicken Sie in der linken unteren Ecke des Dashboards auf **einem Gerät hinzufügen**.

    ![][1]

2.  Klicken Sie im Bereich **Benutzerdefinierte Gerät** klicken Sie auf **Hinzufügen**.

    ![][2]

3.  Wählen Sie **Ich möchte meinen eigenen Geräte-ID zu definieren**, geben Sie eine Geräte-ID wie **Mydevice**klicken Sie auf **ID überprüfen** , stellen Sie sicher, dass dieser Name bereits verwendeten nicht ist, und klicken Sie dann auf **Erstellen** , um das Gerät bereitstellen.

    ![][3]

5. Notieren Sie die Anmeldeinformationen Gerät (Geräte-ID, IoT Hub Hostname und Geräteschlüssel), die Clientanwendung benötigt diese Verbindung mit der remote-Überwachung-Solution. Klicken Sie dann auf **Fertig**.

    ![][4]

6. Stellen Sie sicher, dass Ihr Gerät im Geräte-Abschnitt wird angezeigt. Gerätestatus steht **noch aus** , bis das Gerät eine Verbindung mit der remote-Überwachung-Solution herstellt.

    ![][5]

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png
[5]: ./media/iot-suite-selector-connecting/suite5.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/