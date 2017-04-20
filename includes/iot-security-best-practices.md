# <a name="internet-of-things-security-best-practices"></a>Bewährte Methoden für die Sicherheit von Internet der Dinge

Zum Sichern einer Internet Dinge (IoT) erfordert-Infrastruktur eine Strategie für die strenge vorbeugender Sicherheit. Diese Strategie erfordert sichere Daten in der Cloud, Datenintegrität bei der Übertragung über das öffentliche Internet zu schützen und Bereitstellen von Geräten. Jede Ebene erstellt größerer Sicherheit-Sicherheit in der gesamten Infrastruktur.

## <a name="secure-an-iot-infrastructure"></a>Sichern einer IoT Infrastruktur

Diese vorbeugender Sicherheit Strategie kann entwickelt und mit aktiven Beteiligung der verschiedenen Spieler Zusammenhang mit der Fertigung, Entwicklung und Bereitstellung von IoT Geräte und Infrastruktur ausgeführt werden. Es folgt eine allgemeine Beschreibung der diese Player.  

- **IoT Hardware Hersteller/Integrator**: normalerweise der Hersteller von IoT Hardware wird bereitgestellt, Systemintegratoren Zusammenstellen der Hardware von verschiedenen Herstellern oder Lieferanten, die beim Bereitstellen von Hardware für eine Bereitstellung IoT hergestellt oder von anderen Lieferanten integriert sind.
- **Lösungsentwickler IoT**: die Entwicklung einer Lösung IoT erfolgt in der Regel durch eine Lösungsentwickler. Dieser Entwickler kann Teil eines internen Teams oder auf in diese Aktivität Systemintegrator (SI). Der Lösungsentwickler IoT kann verschiedene Komponenten der Lösung IoT von Grund auf zu entwickeln, integrieren verschiedene serienmäßig oder Open-Source-Komponenten oder vorkonfigurierte Lösungen mit geringfügige Anpassung einführen.
- **IoT Lösung Bereitsteller**: IoT nach einer Lösung entwickelt wird, muss in das Feld bereitgestellt werden. Dieser Schritt umfasst die Bereitstellung von Hardware, Verbund von Geräten und Bereitstellung von Lösungen in Hardwaregeräte oder der Cloud.
- **IoT Lösung Operator**: nach IoT Lösung bereitgestellt ist, er erfordert langfristige Operationen, Überwachung, Upgrades und Wartung. Dies kann durch ein internes Team erfolgen, die umfasst Informationen Technologiespezialisten, Hardware-Vorgänge und Wartung Teams und Domäne-Sicherheitsspezialisten, die das Verhalten der gesamten IoT Infrastruktur zu überwachen.

Die folgenden Abschnitten bewährte Methoden für diese Spieler zu entwickeln, bereitstellen und Verwenden von einer sicheren IoT-Infrastruktur.

## <a name="iot-hardware-manufacturerintegrator"></a>IoT Hardware Hersteller/integrator

Im folgenden werden die bewährten Methoden für IoT Hardwareherstellern und Hardware Systemintegratoren.

- **Bereich Hardware Mindestanforderungen**: Hardware-Design sollte die mindestens erforderlichen Features für Vorgang von der Hardware und nothing Weitere enthalten. Ein Beispiel ist USB-Anschlüsse nur bei Bedarf für den Vorgang des Geräts einschließen. Diese zusätzlichen Features öffnen Sie das Gerät für unerwünschte Angriffsmethoden, die vermieden werden sollten.
- **Stellen Sie Hardware Proof manipulieren**: Mechanismen zum Erkennen von physischen vor Manipulation, wie der Abdeckung Gerät öffnen oder Entfernen eines Teils des Geräts zu erstellen. Diese manipulieren Signale Teil des Datenstroms in der Cloud, die Operatoren dieser Ereignisse informiert hochgeladen werden kann.
- **Erstellen, um sichere Hardware**: Wenn Verbrauch ermöglicht, zum Erstellen von Sicherheitsfeatures wie sichere und verschlüsselte Speicher oder Funktionen basierend auf Modul TPM (Trusted Platform) zu starten. Diese Funktionen machen Geräte sicherer und Schützen der gesamte IoT-Infrastruktur.
- **Stellen Sie sicher Upgrades**: Firmwareupdates während der Lebensdauer des Geräts sind lässt. Erstellen von Geräten mit sicheren Pfade für Upgrades und kryptografischen Sicherstellung der Firmware-Versionen ansetzt, kann das Gerät während und nach dem Update sicher sein.

## <a name="iot-solution-developer"></a>IoT-Lösungsentwickler

Im folgenden sind die bewährten Methoden für IoT-Lösungsentwickler:

- **Gehen Sie folgendermaßen vor, sicherer Software Development-Methodik**: Entwicklung von sicherer Software erfordert Grund auf denken Sicherheit, seit Beginn des Projekts ganz nach dessen Implementierung, testen und bereitstellen. Die verfügbaren Optionen für Plattformen, Sprachen und Tools werden alle mit dieser Methodologie beeinflusst. Microsoft Security Development Lifecycle bietet eine schrittweise Erstellung sicheren Software.
- **Wählen Sie Open-Source-Software mit Vorsicht**: Open Source-Software ermöglicht die schnelle Entwicklung von Lösungen. Berücksichtigen Sie beim Auswählen von Open Source-Software die Aktivitätsebene der für die einzelnen Komponenten der Open-Source-Community. Eine aktive Community wird sichergestellt, dass Software unterstützt wird und Probleme ermittelt und behoben wurden. Alternativ eine ungewöhnliche und inaktive Open-Source-Software möglicherweise nicht unterstützt und Probleme wahrscheinlich nicht gefunden.
- **Integrieren mit Vorsicht**: viele Software Sicherheitslücken an die Grenze für Bibliotheken und APIs vorhanden sein. Funktionalität, die möglicherweise nicht für die aktuelle Bereitstellung erforderlich möglicherweise noch über einen API-Schicht verfügbar sein. Um allgemeine Sicherheit zu gewährleisten, überprüfen Sie alle Schnittstellen der Komponenten, die Sicherheitslücken integriert wird.      

## <a name="iot-solution-deployer"></a>IoT Lösung Bereitsteller

Es folgen bewährte Methoden für die IoT Lösung Benutzer geeignet Anrufschemen verfügen:

- **Bereitstellen von Hardware sicher**: IoT Bereitstellungen erfordern Hardware an unsicheren Speicherorten, z. B. in öffentlichen Bereichen oder unbeaufsichtigte Gebietsschemas bereitgestellt werden. In diesen Fällen stellen Sie sicher, dass Hardware Bereitstellung genehmigten ist die gestatteten Umfang. USB- oder andere Ports auf der Hardware zur Verfügung stehen, sicher, dass sie sichere abgedeckt werden. Viele Angriffsmethoden können diese als Einstiegspunkte verwenden.
- **Authentifizierungsschlüssel schützen**: während der Bereitstellung jedes Gerät benötigt Geräte-ID sowie die zugehörigen Authentifizierungsschlüssel von Cloud-Dienst generiert. Schützen Sie hierüber physisch auch nach der Bereitstellung. Eine beliebige Taste, kompromittierte kann von einem böswilligen Gerät verwendet werden, um als ein bestehendes Gerät ausgeben.

## <a name="iot-solution-operator"></a>IoT Lösung-operator

Im folgenden sind die bewährten Methoden für IoT Lösung Operatoren:

- **Aktualisieren Sie das System auf dem aktuellen Stand**: sicher, dass Gerätebetriebssystemen und alle Gerätetreiber auf die neuesten Version aktualisiert werden. Wenn Sie automatische Updates in Windows 10 (IoT oder anderen SKUs) aktivieren, bleibt Microsoft Stand, ein sicheres Betriebssystem für IoT Geräte bereitstellen. Nachhaltiger Schutz von anderen Betriebssystemen (wie Linux) wird auf dem aktuellen Stand hilft sicherzustellen, dass sie auch vor böswilligen Angriffen geschützt sind.
- **Schutz vor böswilligen Aktivität**: Wenn das Betriebssystem zulässt, installieren Sie die neuesten Viren und Malware-Funktionen auf jedem Gerät Operating System. Dadurch können die meisten externen Bedrohungen. Sie können die meisten modernen Betriebssysteme gegen Bedrohungen durch geeignete Maßnahmen schützen.
- **Häufig Audit**: Überwachung IoT Infrastruktur für Sicherheitsprobleme ist Schlüssel aus, wenn Sicherheit Vorfällen. Die meisten Betriebssysteme verfügen über integrierte Protokollierung, die häufig überprüft werden sollten, um sicherzustellen, dass keine Sicherheitslücken aufgetreten ist. Überwachungsinformationen kann gesendet werden als separate Telemetrie Stream an den Clouddienst, wo diese analysiert werden.
- **Physisch Schutz die IoT-Infrastruktur**: die schlechtesten Sicherheitsangriffen gegen IoT Infrastruktur werden gestartet Zugang zu den Geräten verwenden. Ein wichtiges-Methode wird zum Schutz vor böswilligen Verwendung der USB-Anschlüsse und anderen physischen Zugriff. Ein Schlüssel für Unternehmensdaten Verstöße, die aufgetreten sind möglicherweise ist der physischen Zugriff, wie beispielsweise USB-Anschluss verwenden protokollieren. In diesem Fall ermöglicht Windows 10 (IoT und anderen SKUs) eine detaillierte Protokollierung dieser Ereignisse.
- **Protect Cloud Anmeldeinformationen**: Cloud Authentifizierungsinformationen konfigurieren und den Betrieb einer IoT-bereitstellungs verwendet werden möglicherweise die einfachste Möglichkeit zugreifen und ein System IoT gefährden. Schützen der Anmeldeinformationen durch das Kennwort häufig ändern, und sehen davon ab, über diese Anmeldeinformationen bei öffentlichen Computern.

Die Funktionen der verschiedenen IoT Geräte variieren. Einige Geräte möglicherweise Computern common desktop Betriebssysteme, und einige Geräte möglicherweise sehr leicht Betriebssystemen ausgeführt werden. Best Practices für die Sicherheit beschrieben möglicherweise zuvor für diese Geräte in unterschiedlichem gelten. Wenn dieser Parameter sollte zusätzliche Sicherheit und Bereitstellung best Practices von den Herstellern dieser Geräte folgen.

Einige ältere und eingeschränkte Geräte möglicherweise nicht speziell für IoT Bereitstellung entworfen haben. Diese Geräte möglicherweise die Möglichkeit zum Verschlüsseln von Daten, mit dem Internet verbinden, oder geben Sie erweiterte Überwachung fehlen. In diesen Fällen kann ein Gateway modernen und sichere Feld Aggregieren von Daten aus älteren Geräte und für diese Geräte über das Internet verbinden erforderliche Sicherheit bieten. Feld Gateways bieten sichere Authentifizierung, Aushandlung von verschlüsselten Sitzungen, des Empfangs von Befehlen aus der Cloud und vielen weiteren Sicherheitsfeatures.
