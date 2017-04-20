> [AZURE.SELECTOR]
- [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
- [C#-](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)

## <a name="introduction"></a>Einführung in die

In die [Erste Schritte mit IoT Hub im Vergleich][lnk-twin-tutorial], gelernt Gerät-Metadaten zwischen Ihrer Lösung Back-End mit *Tags*, Bericht Gerät Bedingungen aus eine Gerät-app mit den *gemeldeten Eigenschaften*festgelegt und diese Informationen per Sprache SQL-ähnliche Abfragen.

In diesem Lernprogramm erfahren Sie, wie mit der das Ziel *gewünschten Eigenschaften* in Verbindung mit den *Eigenschaften gemeldet*, Remote apps Gerät konfigurieren. Genauer gesagt dieses Lernprogramm veranschaulicht, wie die zwei gemeldet und gewünschte Eigenschaften eine Konfiguration mit mehreren Schritte einer Gerät Anwendung Einstellung aktivieren, und geben Sie die Sichtbarkeit auf die Lösung Back-End den Status dieses Vorgangs auf allen Geräten.

Auf allgemeiner Ebene folgt dieses Lernprogramm den *gewünschten Zustand Muster* für Device-Management. Die grundlegende Vorstellung, dass dieses Muster ist die Lösung Back-End Geben Sie den gewünschten Zustand für den verwalteten Geräten, anstatt bestimmte Befehle senden. Dadurch wird das Gerät für die am besten erreichen den gewünschten Zustand (sehr wichtig in IoT Szenarien, in denen bestimmte Gerät Bedingungen die Möglichkeit beeinträchtigen, um bestimmte Befehle sofort auszuführen,) beim reporting ständig mit der Back-End, den aktuellen Status und mögliche Fehler. Das Muster gewünschten Zustand ist entscheidend für die Verwaltung großer Sätze von Geräten, wie sie die Back-End haben volle Transparenz des Status des Konfigurationsvorgangs auf allen Geräten ermöglicht.
Finden Sie weitere Informationen zu im Zusammenhang mit der Rolle des gewünschten Zustand Musters in Gerätemanagement in [Übersicht über die Azure IoT Hub Gerätemanagement][lnk-dm-overview].

> [AZURE.NOTE] In Szenarien, in dem Geräte in einem interaktiver Zeitraum (Aktivierung der Lüfter in einer app benutzergesteuerte) gesteuert werden, erwägen Sie [Cloud-Gerät - Methoden][lnk-methods].

In diesem Lernprogramm folgt die Anwendung Back-End-Änderungen die Telemetrie-Konfiguration von einem Zielgerät und als Ergebnis, das Gerät app mehreren Schritten, um die Aktualisierung einer Konfiguration (z. B. Software Modul neu gestartet werden muss), gelten die in diesem Lernprogramm mit einer einfachen Verzögerung simuliert).

Back-End speichert die Konfiguration in das Gerät und gewünschten Eigenschaften auf folgende Weise:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of the configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [AZURE.NOTE] Da Konfigurationen komplexe Objekte sein können, werden in der Regel eindeutigen Ids zugewiesen (Hashes oder [GUIDs][lnk-guid]) um ihre Vergleiche zu vereinfachen.

Die app Gerät meldet die aktuelle Konfiguration die gewünschte Eigenschaft **TelemetryConfig** in den Eigenschaften des gemeldeten Spiegelung:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Beachten Sie wie die gemeldeten **TelemetryConfig** einer zusätzlichen Eigenschaft **Status**, verwendet, um den Status des Konfigurationsvorgangs Update melden hat.

Wenn eine neue Konfiguration des gewünschte empfangen wird, meldet die Gerät app eine ausstehende Konfiguration durch Ändern der Informationen:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of the current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of the pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Klicken Sie dann zu einem späteren Zeitpunkt meldet die app Gerät den Erfolg der Fehler bei diesem Vorgang durch Aktualisieren die oben genannten-Eigenschaft.
Beachten Sie, wie die Back-End, jederzeit auf den Status des Konfigurationsvorgangs auf allen Geräten Abfragen kann.

In diesem Lernprogramm wird gezeigt, wie an:

- Erstellen Sie ein simulierten Gerät, erhält Konfiguration Updates vom Back-End und meldet mehrere Updates als *gemeldeten Eigenschaften* des Aktualisierungsvorgangs Konfiguration.
- Erstellen einer Back-End-app, die die gewünschte Konfiguration eines Geräts aktualisiert, und klicken Sie dann fragt den Konfigurationsprozess Update.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier