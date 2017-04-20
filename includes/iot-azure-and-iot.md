
# <a name="azure-and-internet-of-things"></a>Azure und das Internet der Dinge

Willkommen bei Microsoft Azure und dem Internet Dinge (IoT). In diesem Artikel wird ein IoT Lösungsarchitektur, die die gemeinsamen Merkmale einer Lösung IoT beschreibt, die Sie mithilfe von Azure Services bereitstellen können. IoT Lösungen erfordern bidirektionale Kommunikation zwischen Nummerierung möglicherweise in die Millionen und eine Lösung Back-End-Geräten zu schützen. Beispielsweise kann eine Lösung Back-End automatisierte, vorhersehbare Analytics Einblicken anhand von Ihr Gerät-Cloud-Ereignisstream aufgedeckt verwenden.

Azure IoT Hub ist ein Key Baustein aus, wenn Sie diese mithilfe von Azure Services IoT Lösungsarchitektur implementieren. IoT Suite bietet vollständige, End-to-End-Implementierungen dieser Architektur für bestimmte IoT-Szenarien. Zum Beispiel: 

- Die *remote-Überwachung* -Lösung können Sie Überwachen des Status von Geräten wie Verkaufsautomaten. 
- Die *Vorhersage Wartung* -Lösung können Sie die Wartung Anforderungen von Geräten wie Pumpen in remote entsprechend Stationen vorherzusehen und unvorhergesehenen Ausfallzeiten zu vermeiden.

## <a name="iot-solution-architecture"></a>IoT Lösungsarchitektur

Das folgende Diagramm zeigt eine typische IoT Lösungsarchitektur. Das Diagramm umfasst nicht die Namen der keine bestimmte Azure Services, jedoch werden die wichtigsten Elemente in einer generischen IoT Lösungsarchitektur. In dieser Architektur Datenerfassung IoT Geräte, die sie an einer Cloud-Gateway zu senden. Das Gateway Cloud macht die Daten verfügbar für Verarbeitung durch andere Back-End-Dienste aus, in dem Daten an andere Line-of-Business Applications oder human Operatoren durch ein Dashboard oder ein anderes Gerät Präsentation übermittelt werden.

![IoT Lösungsarchitektur][img-solution-architecture]

> [AZURE.NOTE] Eine ausführliche Erläuterung der IoT-Architektur finden Sie in der [Microsoft Azure IoT Referenzarchitektur][lnk-refarch].

### <a name="device-connectivity"></a>Device-Konnektivität

In dieser Lösungsarchitektur IoT senden Geräte Telemetrie, wie etwa Sensorwerte von einer pumping Station, an einen Endpunkt Cloud gespeichert und verarbeitet. In einem Szenario mit Vorhersage Wartung möglicherweise Back-End den Datenstrom Sensor verwenden, um zu bestimmen, wann eine bestimmte Pumpe Wartung erfordert. Geräte können auch empfangen und darauf antworten Cloud-Gerät-Befehlen durch Lesen von Nachrichten aus einer Cloud Endpunkt. Beispielsweise kann im Szenario mit Vorhersage Wartung Lösung Back-End Befehle senden an andere Pumpen in die pumping Station beginnen erneutes Abläufe, unmittelbar bevor Wartung, um sicherzustellen, dass der Wartung Engineer gestartet werden kann, wenn er eingeht begonnen wird.

Eines der größten Herausforderungen facing IoT Projekte ist wie sicher und zuverlässig Geräte mit der Lösung Back-End verbunden. IoT Geräte haben unterschiedliche Eigenschaften im Vergleich zu anderen Clients wie Browser und mobile apps. IoT Geräte:

- Sind häufig eingebettete Systeme mit kein human Operator.
- Kann an Remotestandorten bereitgestellt werden, auf dem physischen Zugriff teuer ist.
- Kann nur über die Lösung Back-End erreichbar sein. Es gibt keine andere Möglichkeit zur Interaktion mit dem Gerät.
- Möglicherweise Power und Verarbeitungsressourcen begrenzt.
- Möglicherweise zeitweilig, langsamen oder teuren Netzwerkkonnektivität.
- Möglicherweise müssen Sie proprietäre, benutzerdefinierte oder Branchen-Anwendungsprotokolle verwenden.
- Kann mit einer großen Anzahl häufig verwendete Hardware und Software Plattformen erstellt werden.

Neben den oben genannten Anforderungen muss jede IoT Lösung auch Skalierung, Sicherheit und Zuverlässigkeit übermitteln. Der daraus resultierenden Benutzersatz Connectivity Anforderungen ist schwierig und zeitaufwändig von herkömmlichen Technologien wie Web-Containern und messaging Broker implementiert werden. Azure IoT Hub und den Geräte-SDKs IoT einfacher Lösungen implementieren, die diese Anforderungen erfüllen.

Ein Gerät direkt mit einer Cloud-Gateway-Endpunkt kommunizieren kann, oder wenn das Gerät keine der Communications-Protokolle, die das Cloud-Gateway unterstützt verwenden kann, können Sie über eine anspruchsvollere Gateway verbinden. Das [Azure IoT Protokollgateway] [ lnk-protocol-gateway] kann Protokoll Übersetzung ausführen, wenn Geräte Protokolle nicht verwenden können, die IoT Hub unterstützt.

### <a name="data-processing-and-analytics"></a>Datenverarbeitung und-Analyse

In der Cloud ist eine Lösung wieder beenden IoT Großteil der Datenverarbeitung, wie filtern und sammeln Telemetrie und Weiterleitung an andere Dienste. Beenden die IoT Lösung zurück:

- Empfängt Telemetrie in der Skalierung von Ihrer Geräte und bestimmt, wie diese Daten verarbeiten und speichern. 
- Können Sie Befehle aus der Cloud an bestimmtes Gerät zu senden.
- Registrierung Gerätefunktionen, mit denen Sie Geräte bereitgestellt werden soll und welche Geräte zulässig sind, Verbindung mit Ihrer Infrastruktur-Steuerelement enthält.
- Können Sie überwacht den Status Ihrer Geräte und deren Aktivitäten zu überwachen.

Im Szenario mit Vorhersage Wartung speichert Lösung Back-End zurückliegenden Telemetriedaten an. Diese Daten können die Back-End verwenden, um Muster zu identifizieren, die angeben, dass Wartung auf einer bestimmten Pumpe fällig ist.

IoT Solutions können automatische Feedback Schleifen enthalten. Beispielsweise kann ein Modul Analytics in der Back-End aus Telemetrie identifizieren, die Temperatur des ein bestimmtes Gerät über den normalen Betrieb Ebenen ist. Die Lösung senden Sie einen Befehl auf dem Gerät korrigierend anweist.

### <a name="presentation-and-business-connectivity"></a>Präsentation und Business connectivity

Die Präsentation und Business Connectivity Ebene ermöglicht Endbenutzern die IoT-Lösung und den Geräten interagieren. Er ermöglicht Benutzern das Anzeigen und Analysieren von ihren Geräten erfassten Daten. Diese Ansichten können Form von Dashboards oder BI-Berichten, die beide Verlaufsdaten anzeigen können oder nahezu in Echtzeit-Daten nutzen. Beispielsweise kann ein Operator auf dem Status des bestimmten entsprechend Station überprüfen und finden Sie unter Warnungen vom System ausgelöst. Auf dieser Schicht erfolgt kann auch die Integration von IoT Lösung Back-End mit vorhandenen Line-of-Business Applications anzupassenden in Geschäftsprozessen des Unternehmens oder Workflows. Beispielsweise kann die Vorhersage Wartung Lösung mit einem scheduling System integrieren, die Onlinedokumentation für eine Engineer, um eine pumping Station zu besuchen, wenn die Lösung eine Pumpe müssen Wartung identifiziert.

![IoT Lösung dashboard][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
