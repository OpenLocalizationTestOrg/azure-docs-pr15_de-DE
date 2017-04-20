<properties
 pageTitle="Entwicklertools Leitfaden - Gerät im Vergleich zu verstehen | Microsoft Azure"
 description="Azure IoT Hub Entwicklertools Leitfaden – verwenden Gerät im Vergleich Zustand und Konfiguration von Daten zwischen IoT Hub und Ihren Geräten für die Synchronisierung"
 services="iot-hub"
 documentationCenter=".net"
 authors="fsautomata"
 manager="timlt"
 editor=""/>

<tags
 ms.service="iot-hub"
 ms.devlang="multiple"
 ms.topic="article"
 ms.tgt_pltfrm="na"
 ms.workload="na"
 ms.date="09/30/2016" 
 ms.author="elioda"/>

# <a name="understand-device-twins---preview"></a>Gerät im Vergleich zu verstehen – Vorschau

## <a name="overview"></a>(Übersicht)

*Gerät im Vergleich* sind JSON-Dokumente, die Gerätestatusinformationen (Metadaten, Konfigurationen und Bedingungen) zu speichern. IoT Hub behält ein Gerät Ziel für jedes Gerät, das Herstellen einer Verbindung IoT-Hub an. In diesem Artikel wird beschrieben:

* die Struktur der Gerät Ziel: *Tags*, *gewünschten* und *Eigenschaften gemeldet*, und
* die Vorgänge, die auf dem Gerät im Vergleich Gerät apps und Back-End ausführen können.

> [AZURE.NOTE] Zu diesem Zeitpunkt für Gerät im Vergleich nur von Geräten, die Verbindung IoT Hub mit dem MQTT-Protokoll zugegriffen werden. Lizenzinformationen finden Sie die [MQTT unterstützen] [ lnk-devguide-mqtt] Artikel Anweisungen zum Konvertieren von vorhandenen Gerät app MQTT verwenden.

### <a name="when-to-use"></a>Verwenden von

Verwenden Sie Gerät im Vergleich zu:

* Speichern Sie in der Cloud, z. B. Bereitstellungsspeicherort von einem Computer Vending Gerät bestimmte Metadaten.
* Bericht mit aktuellen Zustandsinformationen wie verfügbaren Funktionen und Bedingungen aus der app Gerät, z. B. eine Verbindung über Mobiltelefon oder Wifi Gerät.
* Den Zustand des langer Workflows zwischen Gerät app und Back End, z. B. Back-End Angabe der neuen Firmwareversion zu installieren und das Gerät app reporting der verschiedenen Phasen Aktualisierungsvorgang zu synchronisieren.
* Abfragen von Ihrem Gerät Metadaten, Konfiguration oder Zustand.

[Nachrichten in der Cloud Gerät] verwenden[ lnk-d2c] Zeichenfolgen mit einem Zeitstempel versehen Ereignisse wie Zeitreihe Sensordaten oder Alarme. Verwenden der [Cloud-zu-Gerät Methoden] [ lnk-methods] für die interaktive Steuerung von Geräten, wie etwa einen einschalten.

## <a name="device-twins"></a>Gerät im Vergleich

Gerät im Vergleich Zusammenhang mit dem Gerät Informationen gespeichert, die:

- Gerät und Back enden können zum Synchronisieren von Gerät Bedingungen und Konfiguration verwenden.
- Die Anwendung Back-End können Sie Abfrage- und Ziel langer Vorgänge.

Des Lebenszyklus von einem Gerät und mit der entsprechenden [Gerät Identität]verknüpft ist[lnk-identity]. Im Vergleich werden implizit erstellt und gelöscht werden, wenn eine neue Gerät Identität erstellt oder IoT Hub gelöscht.

Ein Gerät Ziel ist ein JSON-Dokument, das umfasst:

* **Kategorien**. Ein JSON-Dokument Lese- und durch die Back-End. Kategorien werden nicht auf dem Gerät apps angezeigt.
* **Gewünschte Eigenschaften**. Verwendet in Verbindung mit gemeldeten Eigenschaften Gerätekonfiguration oder Bedingung. Gewünschte Eigenschaften können nur festgelegt werden durch die Anwendung wieder beenden und von der app Gerät gelesen werden können. Die app Gerät kann auch in Echtzeit der Änderungen auf die gewünschten Eigenschaften benachrichtigt.
* **Eigenschaften gemeldet**. Zusammen mit den gewünschten Eigenschaften verwendet Gerätekonfiguration oder Bedingung für die Synchronisierung. Gemeldete Eigenschaften kann nur von der app Gerät festgelegt werden und lesen und abgefragt, indem Sie die Anwendung Back-End.

Darüber hinaus enthält der Stammebene der Gerät und die schreibgeschützten Eigenschaften aus den entsprechenden Identität, wie in der [Registrierung des Geräts Identität]enthaltenen[lnk-identity].

![][img-twin]

Hier ist ein Beispiel für ein Gerät und JSON-Dokument ein:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Im Stammobjekt, werden die Systemeigenschaften und Container für Objekte `tags` und beide `reported` und `desired properties`. Die `properties` Container enthält einige Elemente schreibgeschützt (`$metadata`, `$etag`, und `$version`), die in den [Metadaten und] Hilfethemas beschrieben sind[ lnk-twin-metadata] und [vollständige Parallelität] [ lnk-concurrency] Abschnitte.

### <a name="reported-property-example"></a>Gemeldete Eigenschaft (Beispiel)

Im obigen Beispiel enthält das Gerät und eine `batteryLevel` Eigenschaft, die von der app Gerät gemeldet wird. Diese Eigenschaft ermöglicht es, Abfragen und werden für Geräte basierend auf der letzten gemeldeten Batteriestand. Ein weiteres Beispiel müssten das Gerät app-Funktionen für Berichte Gerät oder Verbindungsoptionen.

Beachten Sie die Eigenschaften wie gemeldete Szenarien, in dem die Back-End in den letzten bekannten Wert einer Eigenschaft interessiert ist, zu vereinfachen. [Gerät-Cloud - Nachrichten] verwenden[ lnk-d2c] Wenn die Back-End Gerät werden in Form eines mit einem Zeitstempel versehen Ereignisse wie Zeit Serie folgen verarbeiten.

### <a name="desired-configuration-example"></a>Beispiel für die gewünschte Konfiguration

Im Beispiel oben im `telemetryConfig` gewünschte und gemeldete Eigenschaften werden von der wieder beenden und Gerät app zum Synchronisieren von der telemetrieprotokoll-Konfigurations für dieses Gerät verwendet. Zum Beispiel:

1. Die app-Back-End legt die gewünschte Eigenschaft mit dem Wert der gewünschten Konfiguration. So sieht der Teil des Dokuments mit der gewünschten Eigenschaft aus:

        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
        
2. Die app Gerät wird die Änderung sofort, wenn angeschlossen, oder bei der ersten Verbindung wiederherstellen benachrichtigt. Die app Gerät dann meldet aktualisierte Konfiguration (oder ein Fehler Bedingung mithilfe der `status` Eigenschaft). So sieht der Teil gemeldeten Eigenschaften aus:

        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...

3. Die app-Back-End beibehalten kann die Ergebnisse des Vorgangs Konfiguration auf vielen Geräten, indem Sie [Abfragen] nachverfolgen[ lnk-query] im Vergleich.

> [AZURE.NOTE] Die oben aufgeführten Codeausschnitte finden Sie Beispiele, optimiert die Lesbarkeit zu verbessern, der eine Möglichkeit zur Konfiguration des Geräts und deren Status codiert werden sollen. IoT Hub nicht vorgangseinschränkung für ein bestimmtes Schema für die gewünschten und gemeldeten Eigenschaften in das Gerät im Vergleich.

In vielen Fällen werden im Vergleich zum Synchronisieren von zeitintensive Vorgänge wie Firmwareupdates verwendet. [Verwenden Sie die gewünschte Eigenschaften zum Konfigurieren von Geräten] finden Sie unter[ lnk-twin-properties] für Weitere Informationen zum Verwenden von Eigenschaften zum Synchronisieren und lange nachverfolgen Ausführen von Vorgängen auf Geräten.

## <a name="back-end-operations"></a>Back-End-Vorgängen

Die Back-End arbeitet auf das Ziel, verwenden die folgenden atomare Vorgänge, die über HTTP zur Verfügung gestellt:

1. **Ziel nach Id abrufen**. Dieser Vorgang gibt der Inhalt des das Ziel des Dokuments, einschließlich der Kategorien und des gewünschten, gemeldet und Systemeigenschaften.
2. **Teilweise und aktualisieren**. Dieser Vorgang ermöglicht die Back-End teilweise das Ziel des Tags oder gewünschten Eigenschaften aktualisieren. Die teilweise Aktualisierung wird als JSON-Dokument ausgedrückt, die addiert oder eine beliebige Eigenschaft erwähnt aktualisiert werden. Legen Sie die Eigenschaften auf `null` werden entfernt. Beispielsweise die folgenden erstellt eine neue gewünschte Eigenschaft mit dem Wert `{"newProperty": "newValue"}`, überschreibt den vorhandenen Wert `existingProperty` mit `"otherNewValue"`, und entfernt werden können vollständig `otherOldProperty`. Keine Änderungen erfolgen zu anderen vorhandenen gewünschten Eigenschaften oder Kategorien:

        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }

3. **Ersetzen Sie die gewünschte Eigenschaften**. Dieser Vorgang ermöglicht die Back-End vollständig überschreiben alle vorhandene gewünschte Eigenschaften und Ersetzen durch ein neues JSON-Dokument für `properties/desired`.
4. **Ersetzen von Tags**. Dieser Vorgang ermöglicht analog zum gewünschte Eigenschaften zu ersetzen, Back-End vollständig überschreiben alle vorhandenen Tags und Ersetzen durch ein neues JSON-Dokument für `tags`.

Alle Vorgänge der oben genannten unterstützen [vollständige Parallelität] [ lnk-concurrency] und die **ServiceConnect** Berechtigung erfordern, in dem [Sicherheit] definierten[ lnk-security] Artikel.

Back-End kann zusätzlich zu diesen Vorgängen, die im Vergleich mit einer [Abfragesprache]SQL-ähnliche Abfragen[lnk-query], und führen Sie Vorgänge auf großen Datensätzen im Vergleich mit [Aufträge][lnk-jobs].

## <a name="device-operations"></a>Gerätevorgänge

Die app Gerät arbeitet auf das Ziel mithilfe der folgenden atomare Vorgänge:

1. **Zwei abzurufen**. Dieser Vorgang gibt den Inhalt der das Ziel des Dokuments (einschließlich Tags und gewünscht, gemeldet und Systemeigenschaften) für das aktuell verbundene Gerät.
2. **Teilweise Update Eigenschaften gemeldet**. Dieser Vorgang ermöglicht das teilweise Aktualisieren der gemeldeten Eigenschaften des aktuell verbundenen Geräts an. Diese verwendet das gleiche JSON-Update-Format als Back-End gegenüberliegende teilweise Aktualisierung der gewünschten Eigenschaften.
3. **Berücksichtigen gewünschten Eigenschaften**. Aktualisierungen an die gewünschten Eigenschaften benachrichtigt werden, sobald sie auftreten, kann das aktuell verbundene Gerät auswählen. Das Gerät empfängt derselben Form des aktualisieren (teilweise oder vollständig Austausch) ausgeführt, indem Sie die Back-End.

Alle Vorgänge der oben die **DeviceConnect** Berechtigung erfordern, in dem [Sicherheit] definierten[ lnk-security] Artikel.

Das [Azure IoT Gerät SDKs] [ lnk-sdks] verwenden Sie die oben aufgeführten Vorgänge aus vielen Sprachen und Plattformen erleichtern. Weitere Informationen zu den Details IoT-Hub einfaches für die gewünschten Eigenschaften Synchronisierung finden Sie im [Gerät erneut eine Verbindung herzustellen Fluss][lnk-reconnection].

> [AZURE.NOTE] Aktuell sind Gerät im Vergleich nur Geräten, die Verbindung IoT Hub mit dem MQTT-Protokoll zugegriffen werden.

## <a name="reference-topics"></a>Verweis Themen:

Die folgenden Verweis Themen bieten weitere Informationen zum Steuern des Zugriffs auf Ihre IoT Hub.

## <a name="tags-and-properties-format"></a>Formatieren von Tags und Eigenschaften

Kategorien, die gewünschten und gemeldete Eigenschaften werden JSON-Objekte mit den folgenden Einschränkungen:

* Alle Tasten in JSON-Objekte sind die Groß-/Kleinschreibung beachtet 128 Zeichen Unicode-Zeichenfolgen. Zulässige Zeichen ausschließen Unicode-Steuerzeichen (Segmente C0 und C1), und `'.'`, `' '`, und `'$'`.
* Alle Werte in JSON-Objekt die folgenden Typen von JSON sein können: Boolesch, Zahl, Zeichenfolge, Objekt. Arrays sind nicht zulässig.

## <a name="twin-size"></a>Zwei Größe

IoT Hub erzwingt eine Einschränkung 8KB Größe, auf die Werte `tags`, `properties/desired`, und `properties/reported`, schreibgeschützte Elemente ausschließen.
Berechnet die Größe durch zählen alle Zeichen, die ohne UNICODE steuern Zeichen (Segmente C0 und C1) und Leerzeichen `' '` Wenn es außerhalb Zeichenfolgenkonstante angezeigt wird.
IoT Hub werden alle Vorgänge Fehler ablehnen, die diese Dokumente über die Beschränkung vergrößern möchten.

## <a name="twin-metadata"></a>Und Metadaten

IoT Hub behält den Zeitstempel der letzten Aktualisierung für jedes JSON-Objekt in der gewünschten und gemeldete Eigenschaften an. Die Zeitstempel in UTC sind und im gewünschten Format [ISO8601] codierte `YYYY-MM-DDTHH:MM:SS.mmmZ`.
Zum Beispiel:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Auf jeder Ebene (nicht nur die Blätter der JSON-Struktur) bleibt diese Informationen zur Aufbewahrung von Updates, die Tasten Objekt zu entfernen.

## <a name="optimistic-concurrency"></a>Vollständige Parallelität

Kategorien, unterstützt alle gewünschte und gemeldete Eigenschaften vollständigen Parallelität.
Tags haben ein Etag, gemäß [RFC7232], die den Tag JSON-Darstellung darstellt. Dies können in bedingte Update-Vorgänge vom Back-End Sie Konsistenz sicherzustellen.

Gewünschte und gemeldete Eigenschaften nicht besitzen Etags, aber eine `$version` Wert, der garantiert inkrementell ist. Analog kann zu einem Etag, die Version von der Aktualisierung Partei z. B. (ein Gerät app für eine Eigenschaft gemeldeten) oder die Back-End für eine gewünschte Eigenschaft verwendet werden Konsistenz Aktualisierungen erzwingen.

Versionen sind auch hilfreich, wenn ein beachten Agent (beispielsweise der Gerät-app verwendet und die gewünschten Eigenschaften) Races zwischen das Ergebnis einer Operation abrufen und eine Benachrichtigung über Updates abstimmen hat. Im Abschnitt [Gerät erneut eine Verbindung herzustellen Fluss] [ lnk-reconnection] enthält weitere Informationen.

## <a name="device-reconnection-flow"></a>Gerät erneut eine Verbindung herzustellen Fluss

IoT Hub behält die gewünschten Eigenschaften aktualisieren Benachrichtigungen für getrennte Geräte nicht. Es folgt, dass ein Gerät, das Herstellen einer Verbindung ist im Dokument vollständige gewünschten Eigenschaften sowie Ihr Abonnement für Benachrichtigungen Update abrufen muss. Angegebenen Races zwischen Update Benachrichtigungen und vollständigen Abruf die Möglichkeit, muss der folgende Fluss sichergestellt werden:

1. Gerät app eine Verbindung mit einem IoT-Hub.
2. Gerät app abonniert Update Benachrichtigungen für die gewünschten Eigenschaften aus.
3. Gerät app Ruft das vollständige Dokument für die gewünschten Eigenschaften.

Die app Gerät kann alle Benachrichtigungen mit ignorieren `$version` kleiner oder gleich als die Version des Dokuments vollständige abgerufenen. Dies ist möglich, da IoT Hub ist sichergestellt, dass die Versionen immer erhöht.

> [AZURE.NOTE] Diese Logik ist bereits in der [Azure IoT Gerät SDKs]implementiert[lnk-sdks]. Diese Beschreibung ist sinnvoll, nur, wenn die Gerät app keine der Azure IoT Gerät SDKs verwenden und die Benutzeroberfläche MQTT muss direkt programmieren.

## <a name="additional-reference-material"></a>Weiteres Referenzmaterial

Andere Verweis in der Developer Guide Themen:

- [IoT Hub Endpunkte] [ lnk-endpoints] beschrieben, die verschiedene Endpunkte, die jeder IoT Hub für Laufzeit und Management Vorgänge macht.
- [Beschränkung und Kontingente] [ lnk-quotas] beschreibt die Kontingente, die beziehen sich auf den Dienst IoT Hub und das Drosselung Verhalten zu erwarten, wenn Sie den Dienst verwenden.
- [IoT Hub Geräte und Dienste SDKs] [ lnk-sdks] Listet die verschiedenen Sprache SDKs Sie eine zu verwenden, wenn Sie das Gerät und der Dienst Clientanwendungen, die Interaktion mit einem IoT Hub entwickeln.
- [Abfragesprache für im Vergleich, Methoden und Aufträge] [ lnk-query] die Abfragesprache Sie Informationen über IoT Hub Ihr Gerät im Vergleich, Methoden und Aufträge abgerufen können werden.
- [Support IoT Hub MQTT] [ lnk-devguide-mqtt] bietet weitere Informationen zur Unterstützung von IoT Hub für die MQTT-Protokoll.

## <a name="next-steps"></a>Nächste Schritte

Jetzt haben Sie gelernt, zu dem Gerät im Vergleich, Sie in den folgenden Themen der Developer Guide interessieren könnten:

- [Auf einem Gerät eine direkte Methode aufrufen][lnk-methods]
- [Planen von Projekten auf mehreren Geräten][lnk-jobs]

Wenn Sie einige der in diesem Artikel beschriebenen Konzepte ausprobieren möchten, möglicherweise in den folgenden IoT Hub Lernprogrammen interessiert sein:

- [So verwenden Sie das Gerät Ziel][lnk-twin-tutorial]
- [So verwenden Sie zwei Eigenschaften][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png