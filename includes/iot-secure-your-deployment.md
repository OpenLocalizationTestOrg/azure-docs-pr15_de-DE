# <a name="securing-your-iot-deployment"></a>Sichern Ihrer Bereitstellung IoT

Dieser Artikel enthält die nächste Detailebene für das Schützen der Azure IoT-basierte Internet der Dinge (IoT)-Infrastruktur. Es verknüpft mit Ebene Implementierungsdetails für das Konfigurieren und Bereitstellen von jeder Komponente. Darüber hinaus Vergleiche und Auswahlmöglichkeiten zwischen verschiedenen konkurrierenden Methoden.

Sichern der Bereitstellung des Azure IoT kann in die folgenden drei Bereiche unterteilt werden:

- **Gerätesicherheit**: das Gerät IoT schützen, während sie in der Natur bereitgestellt wird.
- **Verbindungssicherheit**: gewährleisten, dass alle zwischen dem IoT Gerät und IoT Hub übertragene Daten vertraulich und genehmigten ist.
- **Cloud-Sicherheit**: Bereitstellen eines Mediums zum Schutz von Daten während es durchläuft, und in der Cloud gespeichert ist.

![Drei Sicherheitsbereiche][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Bereitstellen von sicheren Gerät und Authentifizierung

Die Azure IoT Suite schützt IoT Geräte mit den folgenden beiden Methoden:

- Durch die Bereitstellung eines Schlüssels eindeutige Identität (Security Token) für jedes Gerät, die Kommunikation mit dem IoT Hub vom Gerät verwendet werden kann.

- Mithilfe einer auf dem Gerät [x. 509-Zertifikat] [ lnk-x509] und privaten Schlüssel als eine bedeutet, dass das Gerät an den IoT Hub authentifiziert. Diese Authentifizierungsmethode wird sichergestellt, dass der private Schlüssel auf dem Gerät nicht außerhalb des Geräts zu einem beliebigen Zeitpunkt bekannt ist eine höhere Sicherheit bereitstellen.

Die token Sicherheitsmethode enthält für jeden Anruf vom Gerät zu IoT Hub durch den symmetrischen Schlüssel für die einzelnen Aufrufe zuordnen, Authentifizierung. X. 509-basierte Authentifizierung ermöglicht die Authentifizierung von einem Gerät IoT auf der physischen Ebene als Teil der Herstellung der Verbindung TLS. Die Security-Token basierenden-Methode kann ohne das x. 509-Authentifizierung verwendet werden, die ein Muster weniger sicher ist. Die Wahl zwischen den beiden Methoden wird hauptsächlich von wie sicher Gerät Authentifizierung werden muss und Verfügbarkeit von sicherer Speicher auf dem Gerät (auf den privaten Schlüssel sicher speichern) vorgegeben.

## <a name="iot-hub-security-tokens"></a>Sicherheitstoken IoT Hub

IoT Hub verwendet Sicherheitstoken zum Authentifizieren von Geräten und Diensten, damit keine Tasten im Netzwerk gesendet. Darüber hinaus sind Sicherheitstoken Gültigkeitszeitraum und Bereich beschränkt. Automatisch generieren Azure IoT Hub SDKs Token, ohne eine spezielle Konfiguration erforderlich ist. Einige Szenarien erfordern jedoch den Benutzer generieren und Sicherheitstoken direkt verwenden. Dazu zählen die direkte Verwendung der Flächen MQTT, AMQP oder HTTP oder die Implementierung des Musters-Tokens-Dienst.

Weitere Informationen zur Struktur der das Sicherheitstoken und ihrer Verwendung finden Sie in den folgenden Artikeln:

-   [Security token Struktur][lnk-security-tokens]
-   [Verwenden von SAS Token als ein Gerät][lnk-sas-tokens]

Jeden IoT Hub hat eine [Registrierung des Geräts Identität] [ lnk-identity-registry] pro Gerät Ressourcen im Dienst, wie eine Warteschlange erstellen, Flugzeug Cloud-zu-Gerät-Nachrichten enthält, und den Zugriff auf das Gerät-Endpunkte verwendet werden kann. Die Identity-Registrierung IoT Hub bietet sichere Speicherung von Gerät Identitäten und Sicherheitsschlüssel für eine Lösung. Einzelpersonen oder Gruppen von Identitäten Geräte können eine Liste oder einer Sperrliste hinzugefügt werden vollständige Kontrolle über den Zugriff durch Geräte aktivieren. In den folgenden Artikeln finden Sie weitere Informationen zur Struktur der Registrierung des Geräts-Identität und unterstützten Vorgänge.

[IoT Hub unterstützt Protokolle wie MQTT, AMQP und HTTP-][lnk-protocols]. Jedes dieser Protokolle verwenden Sicherheitstoken vom Gerät IoT IoT Hub unterschiedlich:

- AMQP: SASL einfache und AMQP anspruchsbasierte Sicherheit ({policyName}@sas.root.{iothubName} im Fall von Hub-Level-Tokens. {Geräte-ID} im Fall eines WAN-Gerät-bezogenen Token).

- MQTT: Verbinden Paket verwendet {Geräte-ID} als {ClientId}, {IoThubhostname} / {Geräte-ID} in das Feld **Benutzername** und ein SAS-Token in das Feld **Kennwort** ein.

- HTTP: Gültiges Token im Authorization-Anforderungsheader ist.

IoT Hub Gerät Identität Registrierung kann zum Konfigurieren von Sicherheitsanmeldeinformationen pro Gerät und Zugriff auf Steuerelement verwendet werden. Jedoch, wenn eine Lösung IoT eine erhebliche Investition in ein [benutzerdefiniertes Gerät Identität Registrierung und/oder Authentifizierung Schema bereits][lnk-custom-auth], in eine vorhandene Infrastruktur mit IoT Hub durch Erstellen eines-token-Diensts integriert werden.

### <a name="x509-certificate-based-device-authentication"></a>X. 509-Zertifikat-basierten Geräteauthentifizierung

Die Verwendung eines [x. 509-Zertifikat gerätebasierte] [ lnk-use-x509] und die zugehörigen privaten und öffentlichen Schlüsselpaar ermöglicht zusätzliche Authentifizierung auf der physischen Ebene. Der private Schlüssel im Gerät sicher gespeichert und ist nicht sichtbar außerhalb des Geräts. Das x. 509-Zertifikat enthält Informationen über das Gerät, wie die Geräte-ID und andere Organisationseinheit Details. Eine Signatur des Zertifikats wird mit dem privaten Schlüssel generiert.

Allgemeine Gerät provisioning Ablauf:

- Ordnen Sie einen Bezeichner für ein physisches Gerät – Gerät Identität und/oder x. 509-Zertifikat auf das Gerät während manufacturing oder Inbetriebnahme Gerät.

- Erstellen Sie einen entsprechenden Eintrag Identität in IoT Hub – Gerät Identität und zugehörige Geräteinformationen in die Registrierung des Geräts IoT Hub an.

- X. 509-Fingerabdruck des Zertifikats sicher in IoT Hub Gerät Registrierung zu speichern.

### <a name="root-certificate-on-device"></a>Stammzertifikat auf Gerät

Beim Einrichten einer sicheren TLS-Verbindungs mit IoT Hub, authentifiziert das Gerät IoT IoT Hub mit einem Stammzertifikat, das Gerät SDK gehört. Für den Client C SDK befindet sich das Zertifikat unter dem Ordner "\\c\\Zertifikate" im Stammverzeichnis der Repo. Obwohl diese Stammzertifikate langer Lebensdauer sind, diese weiterhin möglicherweise ablaufen oder gesperrt werden. Wenn es keine Möglichkeit besteht der Aktualisierung des Zertifikats auf dem Gerät, das Gerät für die Verbindung anschließend IoT Hub (oder andere Cloud-Dienst) möglicherweise nicht. Müssen eine Möglichkeit zum Aktualisieren des Stammzertifikats, nachdem das IoT-Gerät bereitgestellt wird, wird dieses Risiko effektiv verringern.

## <a name="securing-the-connection"></a>Sichern die Verbindung

Internet-Verbindung zwischen dem IoT Gerät und IoT Hub ist mit dem Standard Transport Layer Security (TLS) gesichert. Azure IoT unterstützt [TLS 1.2][lnk-tls12], TLS 1.1 und TLS 1.0, in der angegebenen Reihenfolge. Unterstützung für TLS 1.0 wird nur für Abwärtskompatibilität bereitgestellt. Es empfiehlt sich, TLS 1.2 verwenden, da es die meisten Security enthält.

Azure IoT Suite unterstützt die folgenden Verschlüsselungsanbieter-Suites, in der angegebenen Reihenfolge.

| Chiffre-Suite | Länge |
|--------------|--------|
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (EQ. FS 7680 Bits RSA) | 256    |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (EQ. FS 3072 Bits RSA) | 128    |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 EQ (. FS 7680 Bits RSA)           | 256    |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (EQ. 3072 Bits RSA) FS           | 128    |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) | 256    |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9C MACHINE_CHECK_EXCEPTION) | 128    |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) | 256    |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) | 128    |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35)    | 256    |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f)    | 128    |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa)    | 112    |

## <a name="securing-the-cloud"></a>Sichern von der cloud

Azure IoT Hub ermöglicht die Definition von [Zugriffsrichtlinien] [ lnk-protocols] für jeden Sicherheitsschlüssel. So gewähren Sie Zugriff auf die einzelnen IoT-Hub Endpunkte verwendet die folgende Gruppe von Berechtigungen. Berechtigungen einschränken des Zugriffs auf eine IoT Hub basierend auf Funktionen.

- **RegistryRead**. Gewährt Lesezugriff auf die Registrierung des Geräts Identität. Weitere Informationen finden Sie unter [Gerät Identität Registrierung][lnk-identity-registry].

- **RegistryReadWrite**. Gewährt Lese- und Schreibzugriff auf die Registrierung des Geräts Identität. Weitere Informationen finden Sie unter [Gerät Identität Registrierung][lnk-identity-registry].

- **ServiceConnect**. Erteilt den Zugriff auf die cloud-Dienst verbundenen Kommunikation und Überwachung von Endpunkten. Es erteilt beispielsweise die Berechtigung zum Back-End-Clouddiensten Gerät-Cloud-Nachrichten empfangen, Cloud-zu-Gerät Nachrichten senden, und die entsprechenden Übermittlung Empfangsbestätigungen abrufen.

- **DeviceConnect**. Erteilt den Zugriff auf Geräte-Kommunikationsendpunkte. Beispielsweise gewähren sie Berechtigungen zum Gerät-Cloud-Nachrichten senden und Empfangen von Nachrichten von Cloud-zu-Gerät. Diese Berechtigung wird von Geräten verwendet werden.

Es gibt zwei Methoden, um **DeviceConnect** Berechtigungen mit IoT Hub mit [Sicherheitstoken]zu erhalten[lnk-sas-tokens]: mit einem Gerät Identitätsschlüssel oder einer gemeinsamen Zugriff Richtlinienschlüssel. Darüber hinaus ist zu beachten, dass alle Funktionen von Geräten zugegriffen werden entwurfsbedingt auf Endpunkten mit Präfix verfügbar gemacht wird `/devices/{deviceId}`.

[Dienstkomponenten können nur Sicherheitstoken generieren] [ lnk-service-tokens] gemeinsam genutzter Zugriffsrichtlinien die entsprechenden Berechtigungen erteilen.

Azure IoT Hub und andere Dienste, die Teil der Lösung eventuell zulassen Verwaltung von Benutzern mithilfe von Azure Active Directory.

Von Azure IoT Hub aufgenommen Daten können von einer Vielzahl von Diensten wie etwa Azure Stream Analytics und Azure Blob-Speicher verwendet. Diese Dienste ermöglichen Management Access. Weitere Informationen zu diesen Diensten und verfügbaren Optionen aus:

- [Azure DocumentDB][lnk-docdb]: skalierbarer, vollständig indiziert Datenbankdienst für halbstrukturierte Daten, die Metadaten für die Geräte verwaltet Sie bereitstellen möchten, wie Attribute, Konfiguration und Sicherheitseigenschaften. DocumentDB bietet leistungsfähige mit hohem Durchsatz Verarbeitung, Schema unabhängig Indizieren von Daten und eine umfangreiche SQL-Abfrage-Oberfläche.

- [Azure Stream Analytics][lnk-asa]: in der Cloud, mit dem Sie schnell zu entwickeln und Bereitstellen einer Lösung kostengünstige Analytics, um in Echtzeit Einblicken anhand von Geräten, Sensoren, Infrastruktur und Applikationen aufdecken, Verarbeitung in Echtzeit Stream. Die Daten aus dieser vollständig verwalteter Dienst können auf keinem Datenträger zu skalieren und gleichzeitig weiterhin hohen Durchsatz, Latenz und Flexibilität.

- [Azure-App-Verwaltungsdienste][lnk-appservices]: eine Cloud-Plattform zum Erstellen von leistungsfähigen Web- und mobilen apps, die eine zu Daten an einer beliebigen Stelle Verbindung; in der Cloud oder lokalen. Erstellen von mobilen apps für iOS und Android Windows ansprechender. Integrieren Sie in Ihrer Software-as a Service (SaaS) und unternehmensanwendungen mit Out-of-Box-Konnektivität zu Dutzende von cloudbasierten Diensten und unternehmensanwendungen. Code in Ihrer bevorzugten Sprache und IDE (.NET, NodeJS, PHP, Python oder Java), Web-apps und APIs schneller zu erstellen.

- [Logik Apps][lnk-logicapps]: die Logik Apps-Feature von Azure App-Dienst unterstützt die Integration Ihrer IoT-Lösung für Ihre vorhandenen Line-of-Business-Systeme und Automatisierung Workflowprozesse. Logik Apps ermöglicht Entwicklern von einem Trigger starten und führen Sie dann eine Reihe von Schritten Entwurf Workflows – Regeln und Aktionen, die leistungsstarke Connectors verwenden, um Ihre Geschäftsprozesse zu integrieren. Logik Apps bietet Out-of-Box-Verbindung mit einer großen Ökosystems von SaaS, Cloud-basierten und lokale Applications.

- [Azure BLOB-Speicher][lnk-blob]: zuverlässige und ökonomische Cloud-Speicher für die Daten, die die Geräte in die Cloud zu senden.

## <a name="conclusion"></a>Abschluss

Dieser Artikel enthält die Übersicht über die Implementierung Ebene Details für das Entwerfen und Bereitstellen einer IoT-Infrastruktur mit Azure IoT. Schlüssel beim Sichern der gesamten IoT Infrastruktur muss jeder Komponente Sicherheit konfiguriert ist. Die entwurfsentscheidungen in Azure IoT verfügbar bieten einige Maß an Flexibilität und Auswahl. jede Auswahl haben jedoch Sicherheitsimplikationen. Es wird empfohlen, dass jede dieser Optionen über eine Bewertung Risiko/Kosten ausgewertet.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-as-a-device
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#using-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
