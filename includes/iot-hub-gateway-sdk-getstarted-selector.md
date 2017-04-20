> [AZURE.SELECTOR]
- [Linux](../articles/iot-hub/iot-hub-linux-gateway-sdk-get-started.md)
- [Windows](../articles/iot-hub/iot-hub-windows-gateway-sdk-get-started.md)

Dieser Artikel bietet eine detaillierte Vorgehensweise des [Beispielcode "Hello World"] [ lnk-helloworld-sample] Erläutern Sie die grundlegenden Komponenten des [Azure IoT Gateway SDK] [ lnk-gateway-sdk] Architektur. Das Beispiel verwendet die IoT Hub Gateway SDK eine einfache Gateway erstellen, der eine Meldung "Hello World" in eine Datei alle fünf Sekunden protokolliert.

In dieser exemplarischen Vorgehensweise werden behandelt:

- **Konzepte**: eine konzeptionelle Übersicht über die Komponenten, die alle Gateways Verfassen Sie, mit dem IoT Gateway SDK erstellen.  
- **Hello World-Beispielarchitektur**: Beschreibt die Konzepte wie zum Beispiel "Hello World" anwenden und wie die Komponenten zusammenarbeiten.
- **Gewusst wie: Erstellen Sie das Beispiel**: die erforderlichen Schritte zum Erstellen des Beispiels.
- **Gewusst wie: Ausführen des Beispiels**: die erforderlichen Schritte zum Ausführen des Beispiels. 
- **Finden Sie ein Ausgabebeispiel**: ein Beispiel für die Ausgabe zu erwarten, wenn Sie das Beispiel auszuführen.
- **Codeausschnitte**: eine Auflistung von Codeausschnitte, um anzuzeigen, wie im Beispiel "Hello World" Gateway wichtige Komponenten implementiert.

## <a name="azure-iot-gateway-sdk-concepts"></a>Azure IoT Gateway SDK-Konzepte

Bevor Sie im Beispielcode für untersuchen oder Erstellen eigener Feld Gateway mit dem IoT Gateway-SDK, sollten Sie die wichtigsten Konzepte verstehen, die die Architektur des SDK unterstützt.

### <a name="modules"></a>Module

Erstellen Sie ein Gateway mit dem Azure IoT Gateway SDK durch Erstellen und *Module*zusammenstellen. Module werden *Nachrichten* miteinander Datenaustausch verwenden. Ein Modul empfängt eine Nachricht, führt eine Aktion für diese, überträgt es optional in eine neue Nachricht und klicken Sie dann veröffentlicht wird für andere Module verarbeitet. Einige Module möglicherweise nur erzielt, neue Nachrichten und eingehende Nachrichten nie verarbeiten können. Eine Kette von Modulen erstellt eine Pipeline Datenverarbeitung mit jedes Modul ausführen eine Transformation auf die Daten zu einem Zeitpunkt in dieser Pipeline.

![Eine Kette von Modulen in Gateway erstellt, mit dem Azure IoT Gateway-SDK][1]
 
Das SDK enthält Folgendes:

- Vordefinierter Module, die common Gatewayfunktionen auszuführen.
- Die Schnittstellen können Entwickler benutzerdefinierte Module schreiben.
- Die Infrastruktur notwendig, bereitstellen und Ausführen eines Satzes von Modulen.

Das SDK bietet eine Abstraktionsebene, die Sie Gateways zur Ausführung in eine Vielzahl von Betriebssystemen und Plattformen erstellen kann.

![Azure IoT Gateway SDK Abstraktionsebene][2]

### <a name="messages"></a>Nachrichten

Zwar denken Module übergeben von Nachrichten miteinander in eine bequeme Möglichkeit zum Aufbau einer Gateway-Funktionen zu erfassen, ist es nicht ordnungsgemäß widerspiegeln was geschieht. Mithilfe einen Broker-Module miteinander kommunizieren, Veröffentlichen von Nachrichten in der Broker (Bus, Pubsub oder ein anderes messaging Muster), und lassen Sie dann den Broker Weiterleiten der Nachricht an die Module verbunden.

Ein Module verwendet die **Broker_Publish** -Funktion eine Meldung in der Broker veröffentlichen. Der Broker übermittelt Nachrichten an ein Modul durch den Aufruf einer Callback-Funktion. Eine Nachricht besteht aus einer Reihe von Schlüssel/Wert-Eigenschaften und den Inhalt als einen Block von Arbeitsspeicher übergeben.

![Die Rolle des der Broker im Azure IoT Gateway SDK][3]

### <a name="message-routing-and-filtering"></a>Routing von Nachrichten und Filtern

Es gibt zwei Methoden zum Weiterleiten von Nachrichten an den richtigen Modulen. Eine Reihe von Verknüpfungen kann an der Broker übergeben werden, damit der Broker der Quelle und Empfänger für jedes Modul weiß, oder das Modul auf die Eigenschaften des Message filtern. Ein Modul sollte eine Nachricht nur reagieren, wenn die Nachricht bestimmt ist. Die Links und Filtern von Nachrichten ist was effektiv eine Nachrichtenpipeline erstellt.

## <a name="hello-world-sample-architecture"></a>Hello World (Beispiel)

Das "Hello World" veranschaulicht die im vorherigen Abschnitt beschriebenen Konzepte. Das Beispiel "Hello World" implementiert ein Gateway, das eine Pipeline bestehend aus zwei Module verfügt:

-   Das Modul *"Hello World"* erstellt eine Nachricht alle fünf Sekunden und übergibt sie an das Modul für die Protokollierung.
-   Das Modul für die *Protokollierung* die empfangenen Nachrichten in eine Datei geschrieben.

![Architektur der mit dem Azure IoT Gateway SDK erstellte Hello World-Beispiel][4]

Wie im vorherigen Abschnitt beschrieben, wird das "Hello World"-Modul nicht Nachrichten direkt an das Modul Protokollierung alle fünf Sekunden übergeben. In diesem Fall veröffentlicht sie eine Nachricht der Broker alle fünf Sekunden.

Das Modul für die Protokollierung erhält eine Nachricht von der Broker und fungiert, den Inhalt der Nachricht in eine Datei geschrieben.

Das Modul für die Protokollierung werden nur Nachrichten aus der Broker genutzt, neue Nachrichten nie in der Broker veröffentlicht.

![Wie der Broker Nachrichten zwischen Modulen im Azure IoT Gateway SDK weiterleitet][5]

Die obige Abbildung zeigt die Architektur des Beispiels "Hello World" und die relativen Pfade zu den Quelldateien, die verschiedene Teile des Beispiels im [Repository]implementieren[lnk-gateway-sdk]. Verwenden Sie den Code auf eigene, oder verwenden Sie die Codeausschnitte unten als Leitfaden.

<!-- Images -->
[1]: media/iot-hub-gateway-sdk-getstarted-selector/modules.png
[2]: media/iot-hub-gateway-sdk-getstarted-selector/modules_2.png
[3]: media/iot-hub-gateway-sdk-getstarted-selector/messages_1.png
[4]: media/iot-hub-gateway-sdk-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-gateway-sdk-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/azure-iot-gateway-sdk/tree/master/samples/hello_world
[lnk-gateway-sdk]: https://github.com/Azure/azure-iot-gateway-sdk