> [AZURE.SELECTOR]
- [Linux](../articles/iot-hub/iot-hub-linux-gateway-sdk-simulated-device.md)
- [Windows](../articles/iot-hub/iot-hub-windows-gateway-sdk-simulated-device.md)

In dieser exemplarischen Vorgehensweise der [simulierten Gerät Cloud hochladen Beispiel] veranschaulicht, wie die [Azure IoT Gateway SDK] [ lnk-sdk] Gerät-Cloud-Telemetrie IoT Hub von simulierten Geräten zu senden.

In dieser exemplarischen Vorgehensweise werden behandelt:

1. **Architektur**: wichtige Informationen zur Architektur von im Beispiel simuliert Gerät Cloud hochladen.

2. **Erstellen und Ausführen**: die erforderlichen Schritte zum Erstellen und Ausführen des Beispiels.

## <a name="architecture"></a>Architektur

Im Beispiel simulierten Gerät Cloud hochladen zeigt, wie zum Verwenden von SDK, um Telemetrie von simulierten Geräten mit einem Hub IoT sendet, ein Gateway zu erstellen. Die simulierten Geräten können nicht direkt mit IoT Hub, da verbinden:

- Die Geräte verwenden kein Kommunikationsprotokoll IoT Hub verständlich.
- Die Geräte sind nicht intelligent genug, um die Identität von IoT Hub zugewiesen merken.

Das Gateway löst diese Probleme für den simulierten Geräten wie folgt:

- Das Gateway versteht das verwendeten der simulierten Geräten, Protokoll Gerät-Cloud-Telemetrie ein Gerät empfängt, und leitet diese Nachrichten an IoT Hub mithilfe eines Protokolls vom Hub verstanden.
- Das Gateway speichert IoT Hub Identitäten für den simulierten Geräten und fungiert als Proxy, wenn die simulierten Geräten IoT Hub Nachrichten senden.

Das folgende Diagramm zeigt die Hauptkomponenten des Beispiels, einschließlich der Module Gateway:

![][1]


> [AZURE.NOTE] Nachrichten direkt an übergeben die Module nicht. Die Module Veröffentlichen von Nachrichten an eine interne Broker, der die Nachrichten an die anderen Module mit einem Abonnement-Mechanismus, wie im folgenden Diagramm dargestellt übermittelt. Weitere Informationen finden Sie unter [Erste Schritte mit der IoT Gateway SDK][lnk-gw-getstarted].

### <a name="protocol-ingestion-module"></a>Protokoll aufnehmen-Moduls

In diesem Modul ist der Ausgangspunkt für das Abrufen von Daten aus der Geräte, über das Gateway, und klicken Sie in der Cloud. Im Beispiel führt das Modul vier Aufgaben aus:

1.  Simulierten Temperaturdaten erstellt.
    
    Hinweis: Wenn Sie reale Geräte verwendet haben, würde das Modul Daten aus diesen Geräten gelesen.

2.  Es fügt die simulierten Temperaturdaten in den Inhalt einer Nachricht.

3.  Es fügt eine Eigenschaft mit einer gefälschten MAC-Adresse mit der Meldung, die die simulierten Temperaturdaten enthält.

4.  Es werden die Nachricht in der Kette mit dem nächsten Modul verfügbar gemacht.

> [AZURE.NOTE] Das Modul mit dem Namen **Erfassung Protokoll X** in der obigen Abbildung wird **simuliert Gerät** in den Quellcode aufgerufen.

### <a name="mac-lt-gt-iot-hub-id-module"></a>MAC &lt; - &gt; IoT Hub-ID-Modul

Dieses Modul scannt für Nachrichten, die eine Eigenschaft enthalten, die die MAC-Adresse, die durch das Protokoll aufnehmen Modul, des simulierten Ausgabegeräts hinzugefügt. Wenn das Modul eine solche Eigenschaft findet, die Nachricht eine andere Eigenschaft mit einem IoT Hub Geräteschlüssel hinzugefügt und anschließend wird die Nachricht in der Kette für das nächste Modul verfügbar. Dies ist wie im Beispiel IoT Hub Gerät Identitäten simulierten Geräten zuordnet. Der Entwickler richtet die Zuordnung zwischen MAC-Adressen und IoT Hub Identitäten manuell als Teil der Modulkonfiguration. 

> [AZURE.NOTE]  In diesem Beispiel verwendet eine MAC-Adresse als eine eindeutige Geräte-ID und es mit der Identität Gerät IoT Hub korreliert. Sie können jedoch Ihr eigenes Modul erstellen, das einen anderen eindeutigen Bezeichner verwendet. Beispielsweise müssen Sie möglicherweise Geräte mit eindeutige fortlaufende Zahlen oder Telemetriedaten, die hat einen eindeutigen Gerätenamen eingebettet, die Sie verwenden können, um die Identität des IoT Hub-Geräts zu bestimmen.

### <a name="iot-hub-communication-module"></a>IoT Hub Kommunikationsmodul

In diesem Modul Nachrichten mit einem IoT Hub Gerät Identität vom vorherigen Modul zugewiesen hat und sendet den Nachrichteninhalt an IoT Hub über HTTP. HTTP ist eines der drei Protokolle IoT Hub verständlich.

Zu öffnen eine Verbindung mit IoT-Hub für jedes simulierten Gerät, in diesem Modul wird eine einzelne HTTP-Verbindung vom Gateway an den Hub IoT geöffnet und multiplexes Verbindungen von allen simulierten Geräten über diese Verbindung. Auf diese Weise können ein Gateway so viele weitere Geräte verbinden, simulierten oder anderweitig, als wäre möglich, wenn sie für jedes Gerät eine eindeutige Verbindung geöffnet.

![][2]


<!-- Images -->
[1]: media/iot-hub-gateway-sdk-simulated-selector/image1.png
[2]: media/iot-hub-gateway-sdk-simulated-selector/image2.png

<!-- Links -->
[Beispiel für den simulierten Gerät Cloud hochladen]: https://github.com/Azure/azure-iot-gateway-sdk/blob/master/doc/sample_simulated_device_cloud_upload.md
[lnk-sdk]: https://github.com/Azure/azure-iot-gateway-sdk
[lnk-gw-getstarted]: ../articles/iot-hub/iot-hub-linux-gateway-sdk-get-started.md