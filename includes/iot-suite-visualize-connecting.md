## <a name="view-device-telemetry-in-the-dashboard"></a>Ansicht Gerät Telemetrie in das dashboard

Das Dashboard in der remote-monitoring-Lösung können Sie die Telemetrie anzeigen, die Ihre Geräte an IoT Hub zu senden.

1. In Ihrem Browser remote monitoring Dashboard Lösung zurückzugeben Sie, klicken Sie im linken Bereich zum Navigieren zu der **Liste der Geräte**auf **Geräte** .

2. In der **Liste der Geräte**sollten Sie sehen, der Status des Geräts jetzt **ausgeführt**wird.

    ![][18]

3. Klicken Sie auf **Dashboard** -Dashboard zurückgegeben, wählen das Gerät im **Geräte-Ansicht** Dropdown-seine Telemetrie anzeigen. Die Telemetriedaten aus der beispielanwendung ist 50 Einheiten für die interne Temperatur, 55 Einheiten für externe Temperaturen und 50 Einheiten für Luftfeuchtigkeit. Beachten Sie, dass das Dashboard standardmäßig nur Temperatur und Feuchtigkeit Werte werden angezeigt.

    ![][img-telemetry]

## <a name="send-a-command-to-your-device"></a>Senden Sie einen Befehl auf Ihrem Gerät

Das Dashboard in der remote-monitoring-Lösung können Sie Befehle an Ihre Geräte über IoT Hub zu senden. Beispielsweise können Sie einen Befehl aus, um die interne Temperatur eines Geräts festlegen in der remote-Überwachung-Solution senden.

1. Klicken Sie in dem remote monitoring Lösung-Dashboard im linken Bereich der **Geräteliste**Navigieren auf **Geräten** .

2. Klicken Sie auf **Geräte-ID** für das Gerät in der **Liste Geräte**.

3. Klicken Sie in der Systemsteuerung **Gerätedetails** auf **Befehle**.

    ![][13]

4. Wählen Sie in der Dropdownliste **Befehl** **SetTemperature aus**, und geben Sie einen neuen Temperaturwert in **Temperatur** . Klicken Sie auf **Senden Befehl** , um den Befehl an das Gerät zu senden.

    ![][14]

    > [AZURE.NOTE] Die Befehlsverlaufs zeigt den Status des Befehls zuerst als **Ausstehend**. Wenn das Gerät den Befehl bestätigt, ändert sich der Status **Erfolg**.

5. Das Dashboard sicher, dass das Gerät jetzt als neuen Temperaturwert 75 sendet.

## <a name="next-steps"></a>Nächste Schritte

Im Artikel [Anpassen vorkonfiguriert Lösungen] [ lnk-customize] beschreibt einige Methoden können Sie in diesem Beispiel erweitern. Mögliche Extensions zählen realen-Sensoren und zusätzliche Befehle implementiert.

Weitere Informationen finden Sie Informationen zu den [Berechtigungen auf der Website azureiotsuite.com][lnk-permissions].

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
