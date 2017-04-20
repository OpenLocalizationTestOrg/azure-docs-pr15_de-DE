# <a name="internet-of-things-security-architecture"></a>Internet der Dinge-Sicherheitsarchitektur

Beim Entwerfen eines Systems ist es wichtig zu verstehen die potenziellen Bedrohungen für das System und entsprechende Verteidigung entsprechend, hinzufügen, wie das System entwickelt und ausgelegt ist. Es ist besonders wichtig, um vom Anfang des Produkts unter Einhaltung der Sicherheit zu entwerfen, da verstehen, wie ein Angreifer ein System manipulieren möglicherweise hilft, stellen Sie sicher, dass entsprechende Gegenmaßnahmen in vom Anfang sind. 

## <a name="security-starts-with-a-threat-model"></a>Sicherheit beginnt mit einem Bedrohungsmodell
 
Microsoft hat lange Bedrohungsmodellen für seine Produkte verwendet und hat das Unternehmen Bedrohungsanalyse öffentlich zugänglich gemacht. Die Erfahrung Unternehmen wird veranschaulicht, dass Modellierung hat unerwartete Vorteile neben die sofortige was Bedrohungen für die meisten sind über. Beispielsweise erstellt es auch eine öffnet eine offene Diskussion mit anderen Personen außerhalb der Entwicklungsteam zu neue Ideen und Verbesserung des Produkts führen kann.
  
Erstellen von Bedrohungsmodellen Ziel ist es zu verstehen, wie ein Angreifer möglicherweise ein System, und stellen Sie sicher, dass die entsprechende Gegenmaßnahmen vorhanden sind. Bedrohung Modellierung erzwungen, dass der Entwurf team Gegenmaßnahmen berücksichtigen, wie das System entwickelt wurde und nicht nach einem System bereitgestellt wird. Dies ist von grundlegender Bedeutung, da Sicherheitsmaßnahmen für eine Vielzahl von Geräten in das Feld also nicht realisierbare, ist fehleranfällig und verlassen Kunden gefährdet.

Viele Entwicklungsteams Aktionen erfassen die funktionalen Anforderungen für das System, die Kunden profitieren hervorragende Arbeit aus. Identifizieren, dass eine Person im System Missbrauch möglicherweise nicht offensichtlich Möglichkeiten ist jedoch schwieriger. Bedrohungsmodellen helfen zu verstehen, was ein Angreifer tun kann Entwicklungsteams und warum. Erstellen von Bedrohungsmodellen ist ein strukturierter Prozess, der erstellt einer Diskussion über die Sicherheit Designentscheidungen im System als auch in den Entwurf, die unterwegs, der Auswirkung auf die Sicherheit vorgenommen werden geändert. Während ein Bedrohungsmodell einfach ein Dokument ist, stellt diese Dokumentation auch eine ideale Möglichkeit, um sicherzustellen, dass die gleiche Knowledge Aufbewahrung von Lektionen Erkenntnisse und Hilfe neue team Einstieg schnell. Ergebnis des Erstellens von Bedrohungsmodellen werden schließlich können Sie andere Aspekte der Sicherheit, beispielsweise welche Sicherheit Zusagen berücksichtigen Sie für Ihre Kunden bereitstellen möchten. Diese Verpflichtung in Verbindung mit Bedrohungsmodellen werden informieren und Testen der Projektmappe Internet der Dinge (IoT) Laufwerk.
 

### <a name="when-to-threat-model"></a>Wann Modell Bedrohung

[Threat modeling](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) bietet den größten Wert, wenn es in der Entwurfsphase integriert ist. Wenn Sie entwerfen, können Sie die größte Flexibilität zu ändern, Bedrohungen zu beseitigen. Eliminierung Bedrohungen Design ist das gewünschte Ergebnis zu erreichen. Es ist wesentlich einfacher, als Gegenmaßnahmen hinzufügen, sie testen und gewährleisten, dass sie verbleiben aktuelle und außerdem eine solche Löschung ist nicht immer möglich. Es wird immer schwieriger, Bedrohungen zu beseitigen, wie ein Produkt entwickelten wird, und wiederum letztlich erfordern mehr Arbeit und sehr viel schwieriger vor-und Nachteile als bei der Entwicklung frühzeitig Bedrohungsanalyse.

### <a name="what-to-threat-model"></a>Was Bedrohungsmodell

Modell der Lösung als Ganzes thread, und konzentrieren Sie sich auch in den folgenden Bereichen:

- Die Sicherheits- und Datenschutzfeatures aufgeführt
- Die Features, deren Ausfälle Sicherheit relevant sind
- Die Features, die eine Vertrauensstellung Grenze touch 

### <a name="who-threat-models"></a>Verfahren, die zum Erstellen von Modellen

Erstellen von Bedrohungsmodellen ist ein Prozess wie jedes andere.  Es ist ratsam, Bedrohung Modell Dokuments wie alle anderen Komponenten der Lösung zu behandeln und zu überprüfen. Viele Entwicklungsteams Aktionen erfassen der funktionellen Anforderungen für das System, die Kunden profitieren hervorragende Arbeit aus. Identifizieren, dass eine Person im System Missbrauch möglicherweise nicht offensichtlich Möglichkeiten ist jedoch schwieriger. Bedrohungsmodellen helfen zu verstehen, was ein Angreifer tun kann Entwicklungsteams und warum.

### <a name="how-to-threat-model"></a>Wie Bedrohungsmodell

Erstellen von Bedrohungsmodellen besteht aus vier Schritten; die Schritte sind:

- Modellieren der Anwendung
- Aufzählen von Bedrohungen
- Abwehren von Sicherheitsrisiken
- Überprüfen von Gegenmaßnahmen

#### <a name="the-process-steps"></a>Die Prozessschritte

Drei Faustregeln beim Erstellen von einem Bedrohungsmodell bedenken:

1. Erstellen Sie ein Diagramm aus Referenzarchitektur. 
2. Starten Sie zuerst der Breite. Verschaffen Sie sich einen Überblick, und verstehen Sie das System als Ganzes, vor dem tief Einstieg.  Dadurch wird sichergestellt, Sie im-Detail an den richtigen stellen.
3. Laufwerk des Prozesses, lassen Sie nicht zu den Prozess Sie Laufwerk. Wenn Sie ein Problem in der Phase der Modellierung suchen und sie untersuchen möchten, finden Sie es!  Nicht der Meinung, Sie müssen diese Schritte Servicekraft.  

#### <a name="threats"></a>Bedrohungen

Die vier Kernelemente ein Bedrohungsmodell sind:

- Prozesse (Web Services, Win32-Dienste * nix-Daemons usw.. Beachten Sie, dass einige komplexen Entitäten (z. B. Feld Gateways und Sensoren) abstrahiert werden können, wie ein Prozess, bei einem technischen Drilldown in den folgenden Bereichen nicht möglich ist.
- Daten gespeichert werden (überall, wo Daten, wie eine Konfigurationsdatei oder Datenbank gespeichert sind)
- Datenfluss (wobei Daten zwischen anderen Elementen in der Anwendung Verschiebungen)
- Externe Entitäten (alle Werte, die mit dem System interagiert, ist aber keine von der Anwendung gesteuert, Beispiele für Benutzer eingeschlossen werden sollen, und Satellitenassemblys Feeds)

Alle Elemente im Architekturdiagramm gelten verschiedene Bedrohungen; Wir verwenden das mnemonische Schrittweite. [Threat Modeling erneut, Schritt](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) mehr kennen die Schrittweite Elemente lesen.

Verschiedene Elemente des Anwendungsdiagramms gelten bestimmte Bedrohungen Schritt aus:

- Prozesse unterliegen Schrittweite
- Datenflüsse unterliegen TID
- Datenspeicher unterliegen TID und manchmal R, ein, wenn die Datenspeicher Protokolldateien sind.
- Externe Entitäten unterliegen SRD

## <a name="security-in-iot"></a>Sicherheit in IoT

Verbundene spezieller Geräte haben eine erhebliche Anzahl von potenziellen Interaktion Flächen oder Interaktionsmuster, die ein Framework zum Sichern von digitalen Zugriff auf diese Geräte bieten berücksichtigt werden müssen. Der Begriff "digital Access" wird hier verwendet, um alle Vorgänge unterscheiden, die durch direkte Gerät Interaktion ausgeführt werden, in denen Sicherheit in Access über die Steuerung des physischen Zugriffs angegeben. Platzieren das Gerät beispielsweise in einem Raum mit eine Sperre auf die Tür. Während der physische Zugriff verweigert werden kann, mithilfe von Software und Hardware können Maßnahmen ergriffen werden, um physische Access Zeilenabstand für System Interferenzen zu verhindern. 

Erfahren Sie die Interaktionsmuster, wird "Device Control" und "Gerätedaten" mit der gleichen Ebene Aufmerksamkeit betrachten wir. "Device Control" kann als Informationen klassifiziert werden, die ein Gerät Parteien mit dem Ziel ändern oder beeinflusst das Verhalten in Richtung des Zustands oder den Status ihrer Umgebung bereitgestellt wird. "Gerätedaten" können als Informationen klassifiziert werden, die ein Gerät an eine andere Partei über den Zustand und den beobachteten Zustand seiner Umgebung ausgibt.
   
Zur Optimierung der bewährten Sicherheitsmethoden empfiehlt es sich, dass eine typische IoT-Architektur in mehreren Komponente/Zonen als Teil der Bedrohungsmodell unterteilt werden. Diese Zonen werden vollständig in diesem Abschnitt beschrieben und umfassen:

-   -Gerät
-   Feld-Gateway
-   Cloud-Gateways, und
-   Dienste.

Zonen sind umfassende Möglichkeiten beim segmentieren Sie einer Lösung. Jede Zone ist häufig eigene Daten und Authentifizierung und Autorisierung erforderlich. Zonen können auch verwendet werden, um Schäden isoliert und die Auswirkungen der niedriger Vertrauenswürdigkeit Zonen auf einer höheren vertrauenswürdige Zonen einschränken.

Jede Zone ist durch eine Grenze vertrauen getrennt, als die punktierte rote Linie in der folgenden Abbildung gekennzeichnet ist. Es stellt einen Übergang von Data-Informationen von einer Quelle zu einem anderen. Während dieser Umstellung könnte Informationen oder Daten Spoofing, Tampering, Zurückweisung, Offenlegung von Informationen, Denial of Service und Erhöhung der geringsten Rechte (Schritt) sein.

![IoT Sicherheitszonen](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Die Komponenten, die innerhalb jeder Grenze dargestellt werden auch Schrittweite, aktivieren eine vollständige 360 unterzogen Bedrohungsanalyse Ansicht der Lösung. In den folgenden Abschnitten weiter auszuführen, auf den einzelnen Komponenten und bestimmte Sicherheitsaspekte und Lösungen, die in Place versetzt wird.

In den Abschnitten, der die befolgt werden Standardkomponenten in diesen Zonen in der Regel gefunden werden.

### <a name="the-device-zone"></a>Die Zone Gerät

Die Gerät-Umgebung ist die sofortige physischen Abstand zwischen dem Gerät, in der physischen Zugriff und/oder "Lokales Netzwerk" digitale Peer-zu-Peer-Zugriff auf das Gerät ist möglich. "Lokales Netzwerk" wird davon ausgegangen, dass ein Netzwerk sein, die unterschiedliche und von – isoliert ist jedoch potenziell überbrückt an – das öffentliche Internet und umfasst alle drahtlosen Sender im Nahbereich-Technologie, über die Peer-zu-Peer-Kommunikation von Geräten. Es ist *nicht* enthalten alle Netzwerk-Virtualisierungstechnologie erstellen den Eindruck eines lokalen Netzwerks und öffentlicher Operator Netzwerke, die erfordern alle zwei Geräte für die Kommunikation über öffentliches Netzwerk Speicherplatz, wären sie geben Sie eine Beziehung Peer-zu-Peer-Kommunikation wird auch nicht berücksichtigt.

### <a name="the-field-gateway-zone"></a>Das Feld Gateway-Zone

Feld Gateway ist eine Gerät-Appliance oder einige allgemeine Server Computersoftware, die als Kommunikation Aktivierung und möglicherweise als Steuerelement Gerätesystem- und Gerät Datenverarbeitung Hub fungiert. Die Feld Gateway Zone umfasst das Feld Gateway selbst und alle Geräte, die es angefügt sind. Wie der Name schon sagt, Feld Gateways äußeren dedizierten Datenverarbeitung Einrichtungen fungieren, sind meist Speicherort gebunden, physischen Intrusion potenziell unterliegen, und werden eingeschränkten betriebliche Redundanz. Alle zum bestätigen, dass ein Feld Gateway häufig eine Sache ist kann eine berühren und sabotage wissen, was ihre Funktion ist. 

Ein Feld Gateway unterscheidet sich von ein Router mere Datenverkehr, gab es eine aktive Rolle im Verwalten des Zugriffs und Informationsfluss, was bedeutet, dass es sich um eine Anwendung ist Entität und Netzwerk Verbindung oder Sitzung terminal behoben. Ein NAT-Gerät oder der Firewall, im Gegensatz dazu nicht geeignet ist, als Gateways dar, da sie keine explizite Verbindung oder Sitzung Anschlüsse, sondern vielmehr eine Route (oder Block) Verbindungen sind oder sie durchgeführte Sitzungen. Das Feld Gateway verfügt über zwei unterschiedliche Bereiche. Eine zeigt die Geräte, die es angefügt sind, innerhalb der Zone darstellt und der andere zeigt alle externe Parteien ist am Rand der Zone.   

### <a name="the-cloud-gateway-zone"></a>Die Cloud-Gateway-zone

Cloud-Gateway ist ein System, das über öffentliches Netzwerk Speicherplatz, in der Regel in einer Cloud-basierten Steuerelement und Daten Analysesystem, einen Verbund derartiger Systeme Remotekommunikation from und to Geräte oder Feld Gateways aus mehreren verschiedenen Websites ermöglicht. In einigen Fällen kann ein Cloud-Gateway sofort spezieller Geräte aus Anschlüsse wie Tablets oder Telefone erleichtern. Im Kontext hier erläuterten sollte "Cloud" auf einem dedizierten Datenverarbeitungssystem verweisen, die nicht am selben Standort wie der angeschlossene Geräte oder Gateways Feld gebunden ist. In einer Zone Cloud operative Maßnahmen gezielte Zugang zu verhindern, dass auch nicht notwendigerweise auf eine Infrastruktur "Öffentliche Cloud" verfügbar gemacht.  

Ein Cloud-Gateway kann in einem Netzwerk Virtualisierung Überlagerung das Cloud-Gateway und alle seine angeschlossene Geräte oder Feld Gateways aus anderen Netzwerkverkehr zu isolieren potenziell zugeordnet werden. Das Cloud-Gateway selbst ist weder ein Gerät-Verwaltungssystem noch eine Verarbeitung oder Speicher Facility für Gerätedaten. Diese Funktionen-Schnittstelle mit dem Cloud-Gateway. Die Cloud Gateway Zone umfasst das Cloud Gateway selbst sowie alle dar-Gateways und Geräte direkt oder indirekt als Anlage. Die Kante der Zone ist eine unterschiedliche Oberfläche, in dem alle externe Parteien über kommunizieren.

### <a name="the-services-zone"></a>Die Zone services

"Dienst" ist für diesen Kontext als alle Softwarekomponente oder Modul, das mit Geräten über ein Gateway - Feld oder in der Cloud für Datensammlung und-Analyse sowie für den Befehl und Steuerung gekoppelten ist definiert.  Dienste sind Vermittler. Sie ihre Identität in Richtung Gateways und andere Subsysteme fungieren, speichern und Analysieren von Daten, autonom Befehle zu Geräten basierend auf Daten Insights oder Zeitpläne und Informationen verfügbar machen und Steuern von Funktionen für Endbenutzer autorisierten an.

### <a name="information-devices-vs-special-purpose-devices"></a>Informationen-Geräten im Vergleich zu spezieller Geräte

PCs, Telefone und Tablets werden in erster Linie interaktive Informationen Geräte. Telefone und Tablets werden explizit auf die Maximierung Batterielebensdauer optimiert. Sie deaktivieren vorzugsweise teilweise beim interagieren nicht sofort mit einer Person, oder wenn nicht-Dienste wie Wiedergeben von Musik oder: leiten Besitzer an einem bestimmten Standort bereitstellen. Im Hinblick auf Systeme fungieren diese Informationen Technologie Geräte in erster Linie als Proxys bald Personen. Sie sind "Personen Aktuatoren" vorschlägt, Aktionen und "Personen Sensoren" Eingabe erfassen. 

Spezieller Geräte, unterscheiden sich von einfache Temperatursensoren für komplexe Factory Produktion Zeilen Tausende von Komponenten darin. Diese Geräte sind sehr viel in Zweck beschränkt und, auch wenn sie eine Benutzeroberfläche bereitstellen, sie sind größtenteils bezogen auf eine Schnittstelle mit oder in Anlagen in der physischen Welt integriert werden. Sie messen und Umwelt Umständen melden, Ventile aktivieren, Servos steuern, Alarmen auszugeben, Leuchten wechseln und viele andere Aufgaben ausführen. Auf diese Weise funktionieren, für die ein Gerät Informationen entweder zu Allgemein, zu teuer, zu groß oder zu spröde ist. Der konkrete Zweck schreibt sofort ihre technischen Entwurf als auch das verfügbare Budget für ihre Produktion und geplanten Lebensdauer Vorgang vor. Die Kombination dieser beiden wichtigsten Faktoren schränkt die verfügbaren betriebliche Energie Budget, physische Speicherbedarf und somit verfügbaren Speicher Compute und Sicherheitsfunktionen.  

Wenn etwas "wechselt falsche" mit automatisierten oder remote gesteuert Geräten, Fehlern beispielsweise physischen defekte oder Steuerelementlogik zum Zusammenstellen und Einhaltung Anmeldekennwort. Produktion lose gelöscht werden können, Gebäude looted oder brennen nach unten, und Personen möglicherweise verletzt oder sogar Die. Dies ist natürlich einer ganz anderen Klasse beschädigt sind als einer Person, einer gestohlenen Kreditkarte Grenzwert maximal ausnutzen. Das Sicherheitsniveau für Geräte, die Dinge verschieben sowie für Sensordaten, die schließlich Befehle, die Aspekte führt, die zu verschieben, führen muss größer als in einer beliebigen e-Commerce- oder eine bankszenarios sein. 


### <a name="device-control-and-device-data-interactions"></a>Gerät Steuerelement und damit zusammenhängende Interaktionen Gerät-Daten

Verbundene spezieller Geräte haben eine erhebliche Anzahl von potenziellen Interaktion Flächen oder Interaktionsmuster, die ein Framework zum Sichern von digitalen Zugriff auf diese Geräte bieten berücksichtigt werden müssen. Der Begriff "digital Access" wird hier verwendet, um alle Vorgänge unterscheiden, die durch direkte Gerät Interaktion ausgeführt werden, in denen Sicherheit in Access über die Steuerung des physischen Zugriffs angegeben. Platzieren das Gerät beispielsweise in einem Raum mit eine Sperre auf die Tür. Während der physische Zugriff verweigert werden kann, mithilfe von Software und Hardware können Maßnahmen ergriffen werden, um physische Access Zeilenabstand für System Interferenzen zu verhindern. 
 
Erfahren Sie die Interaktionsmuster, wird "Device Control" und "Gerätedaten" mit der gleichen Ebene Aufmerksamkeit beim Erstellen von Bedrohungsmodellen betrachten wir. "Device Control" kann als Informationen klassifiziert werden, die ein Gerät Parteien mit dem Ziel ändern oder beeinflusst das Verhalten in Richtung des Zustands oder den Status ihrer Umgebung bereitgestellt wird. "Gerätedaten" können als Informationen klassifiziert werden, die ein Gerät an eine andere Partei über den Zustand und den beobachteten Zustand seiner Umgebung ausgibt. 

## <a name="threat-modeling-the-azure-iot-reference-architecture"></a>Die Referenzarchitektur Azure IoT-Bedrohungsanalyse

Microsoft verwendet Framework obenstehenden auf Modellierung für Azure IoT Bedrohung Aktionen aus. Im Abschnitt unten verwenden wir daher das konkrete Beispiel für Azure IoT Referenzarchitektur zur Veranschaulichung wie Bedrohung für IoT Modellierung bedenken sollten und wie die identifizierten Bedrohungen behandeln. In unserem Fall identifiziert es vier Hauptbereichen Fokus:

-   Geräte und Datenquellen
-   Data-Transport
-   Gerät und Ereignisverarbeitung, und
-   Präsentation

![Für Azure IoT Bedrohungsanalyse](media/iot-security-architecture/iot-security-architecture-fig2.png) 

Die folgende Abbildung bietet eine vereinfachte Ansicht der IoT-Architektur von Microsoft mit einem Datenflussdiagramm-Modell, das von Microsoft Threat Modeling-Tool verwendet wird:

![Bedrohungsanalyse für Azure IoT mit MS Threat Modeling Tool](media/iot-security-architecture/iot-security-architecture-fig3.png)

Es ist wichtig zu beachten, dass die Architektur die Funktionen Gerät und Gateway trennt. Dies ermöglicht es dem Benutzer Gateway-Geräte verwenden können, die sicherer sind: sie sind mit dem Cloud-Gateway verwenden sichere Protokolle, die in der Regel erfordert mehr Verarbeitungsaufwand, dass eine systemeigene Gerät - wie ein Thermostat - eigenständig bereitstellen konnte kommunizieren kann. In der Zone Azure-Diensten wird davon ausgegangen, dass der Cloud Gateway vom Dienst Azure IoT Hub dargestellt ist.

### <a name="device-and-data-sourcesdata-transport"></a>Gerät und Data Sources-Daten transport

Dieser Abschnitt erläutert die oben beschriebene, über die Lens der Bedrohungsanalyse Architektur und bietet eine Übersicht über die wie wir reagieren sind einige der Sicherheitsmechanismen Probleme auf. Es wird auf die Kernelemente ein Bedrohungsmodell konzentrieren:

- Prozesse (die unter unsere Kontrolle und externe Elemente)
- Kommunikation (auch als Datenflüsse bezeichnet)
- Speicher (auch als Datenspeicher bezeichnet)

#### <a name="processes"></a>Prozesse

In jeder Kategorie in der Azure IoT-Architektur beschrieben, versuchen wir, eine Anzahl von unterschiedlichen Bedrohungen in den verschiedenen Stufen abwehren Data-Informationen in vorhanden ist: Prozess, Kommunikation und Speicher. Im folgenden geben wir eine Übersicht über die am häufigsten verwendeten Methoden für die Kategorie "Prozess", gefolgt von einem Überblick darüber, wie diese am besten behoben werden konnte: 

**Spoofing (S)**: ein Angreifer möglicherweise von einem Gerät, entweder auf Ebene der Software oder Hardware kryptografische Schlüsselmaterial extrahieren und anschließend wurde Zugriff auf das System mit einem anderen physischen oder virtuellen Gerät unter der Identität des Geräts das Schlüsselmaterial aus übernommen. Eine gute Illustration wird Remote-Steuerelemente können, die alle TV aktivieren und die beliebte pubertären Tools sind.

**Denial of Service (D)**: ein Gerät nicht funktioniert, oder die Kommunikation per Störung Funkfrequenzen oder Ausschneiden Kabel gerendert werden kann. Beispielsweise wird eine Kamera Überwachung, bei die seiner Power oder im Netzwerk Verbindung absichtlich Ausgesparte auftrat keine Daten, überhaupt angezeigt werden.

**Manipulation (T)**: ein Angreifer möglicherweise ganz oder teilweise ersetzen Sie die Software auf dem Gerät ausgeführt und damit die ersetzte Software der Echtheit des Geräts verwenden können, wenn das Schlüsselmaterial oder Funktionen für die kryptografischen gedrückt halten, wichtige Materialien für das Programm unerlaubten verfügbar waren. Beispielsweise kann ein Angreifer nutzen Sie extrahierten Schlüsselmaterial abzufangen und Daten aus dem Gerät im Kommunikationspfad unterdrücken, und Ersetzen Sie ihn durch "false" Daten, die mit dem gestohlenen Schlüsselmaterial authentifiziert wird.

**Offenlegung von Informationen (I)**: Wenn das Gerät manipulierten Software ausgeführt wird, kann dieser manipulierten Software potenziell Daten autorisiertem Speicherverluste. Beispielsweise kann ein Angreifer extrahierten Schlüsselmaterial um selbst in den Kommunikationspfad zwischen dem Gerät und ein Controller oder Feld Gateway oder Cloud Zugang zu Informationen einbeziehen einschleusen nutzen.

**Erhöhung der geringsten Rechte (E)**: ein Gerät, das bestimmte Funktion kann etwas anderes tun erzwungen werden. Beispielsweise kann ein Ventil, die so programmiert ist, öffnen Sie halb dazu veranlasst werden, um ganz zu öffnen.

| **Komponente** | **Bedrohung** | **Risikominderung**                                                                                                                                                | **Risiko**                                                                                                                                                                                                    | **Implementierung**                                                                                                                                                                                                                                                                                                                                     |
|---------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gerät        | S          | Das Gerät Identität zuweisen und das Gerät wird authentifiziert                                                                                                | Ersetzen Gerät oder einen Teil des Geräts mit einem anderen Gerät. Woher wissen wir, dass wir sprechen in das richtige Gerät?                                                                                           | Das Gerät, mit Transport Layer Security (TLS) oder IPSec-Authentifizierung. Infrastruktur sollten unterstützt mit vorinstallierten Schlüssel (PSK) auf diesen Geräten, die vollständige asymmetrische Kryptografie nicht verarbeiten kann. Nutzen von Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt)                             |
|               | TRID       | Übernehmen Sie nicht manipulierbares Mechanismen beispielsweise auf das Gerät, und es schwierig, unmöglich zum Extrahieren von Schlüsseln und anderen kryptografischen Material vom Gerät mit. | Das Risiko ist, wenn jemand das Gerät (physischen Störungen) Manipulation ist. Wie wir sind natürlich dieses Gerät nicht manipuliert.                                                                                 | Die effizienteste Minderung spielt eine vertrauenswürdige Plattform-Modul (TPM), mit dem Speichern von Schlüsseln in speziellen auf Chip Kreis aus der Schlüssel können nicht gelesen werden, jedoch können nur für kryptografische Vorgänge, die verwenden Sie die Taste jedoch nie offen legen den Schlüssel verwendet werden können. Arbeitsspeicher Verschlüsselung des Geräts. Verwalten von Schlüsseln für das Gerät. Signieren des Codes. |
|               | E          | Lassen Sie die Steuerung des Zugriffs des Geräts. Autorisierungsschema.                                                                                                    | Wenn das Gerät für die einzelnen Aktionen ausgeführt werden basierend auf Befehle aus einer externen Quelle oder sogar kompromittierten Sensoren ermöglicht es, den Angriff nicht anderweitig Operationen zugegriffen werden können. | Mit dem Authentifizierungsschema für das Gerät                                                                                                                                                                                                                                                                                                             |
| Feld Gateway | S          | Authentifizieren das Feld Gateway an Cloud-Gateway (Cert basiert, PSK, Forderung basiert,...)                                                                           | Wenn jemand Feld Gateway Spoofing kann, kann es sich selbst als ein Gerät präsentieren.                                                                                                                               | TLS RSA/PSK, IPSe, [RFC 4279](https://tools.ietf.org/html/rfc4279). Sämtliche Speicher- und Bescheinigung Fragen von Geräten im Allgemeinen – besten Fall ist verwenden TPM. 6LowPAN-Erweiterung für IPSec Wireless Sensor Netzwerke (WSN) unterstützen.                                                                                                              |
|               | TRID       | Schützen Sie das Feld Gateway gegen Manipulation (TPM?)                                                                                                            | Spoofingangriffe, die die Cloud Gateway denken verleiten ist es Feld Gateway kommunizieren kann Offenlegung von Informationen und Datenmanipulation führen                                                             | Arbeitsspeicher Verschlüsselung, TPM, Authentifizierung.                                                                                                                                                                                                                                                                                                              |
|               | E          | Access Control Mechanismus für das Feld Gateway                                                                                                                    |                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                        |

Es folgen einige Beispiele der Bedrohungen in dieser Kategorie:

Spoofing: Ein Angreifer möglicherweise extrahieren kryptografische Schlüsselmaterial aus einem Gerät entweder auf der Software oder Hardware, und anschließend Access das System mit einem anderen physischen oder virtuellen Gerät unter der Identität des Geräts das Schlüsselmaterial entnommen wurde.

**Denial-of-Service**: ein Gerät nicht funktioniert, oder die Kommunikation per Störung Funkfrequenzen oder Ausschneiden Kabel gerendert werden kann. Beispielsweise meldet eine Überwachung Kamera, bei die seiner Power oder im Netzwerk Verbindung absichtlich Ausgesparte auftrat-Daten in allen keine.

**Tampering**: ein Angreifer möglicherweise ganz oder teilweise ersetzen Sie die Software auf dem Gerät ausgeführt und damit die ersetzte Software der Echtheit des Geräts verwenden können, wenn das Schlüsselmaterial oder Funktionen für die kryptografischen gedrückt halten, wichtige Materialien für das Programm unerlaubten verfügbar waren.

**Tampering**: eine Überwachung Kamera, die ein Bild sichtbaren Spektrums, der eine leere Gang anzeigt konnte stützen sich ein Foto der eine solche Gang. Ein Smoke oder Feuer Sensor konnte jemand mit einer heller darunter gemeldet werden. In beiden Fällen das Gerät möglicherweise technisch voll vertrauenswürdig in Richtung des Systems, aber es wird ein Bericht mit manipulierten Informationen.

**Tampering**: Angreifer nutzen extrahierten Schlüsselmaterial abzufangen und Daten aus dem Gerät im Kommunikationspfad unterdrücken, und Ersetzen Sie ihn durch "false" Daten, die mit dem gestohlenen Schlüsselmaterial authentifiziert wird.

**Tampering**: ein Angreifer möglicherweise ganz oder teilweise ersetzen Sie die Software auf dem Gerät ausgeführt und damit die ersetzte Software der Echtheit des Geräts verwenden können, wenn das Schlüsselmaterial oder Funktionen für die kryptografischen gedrückt halten, wichtige Materialien für das Programm unerlaubten verfügbar waren.
   
**Offenlegung von Informationen**: Wenn das Gerät manipulierten Software ausgeführt wird, kann dieser manipulierten Software potenziell Daten autorisiertem Speicherverluste.

**Offenlegung von Informationen**: Angreifer nutzen extrahierten Schlüsselmaterial selbst in den Kommunikationspfad zwischen dem Gerät und ein Controller oder ein Feld Gateway oder Cloud-Gateway zum einbeziehen deaktiviert Informationen eingefügt.

**Denial-of-Service**: das Gerät kann werden ein- oder ausgeschaltet in einen Modus, in dem kein Kommunikation möglich (Dies ist beabsichtigt auf vielen gewerblichen Computer).

**Tampering**: das Gerät kann neu konfiguriert werden, um Benutzer in einem unbekannten an das Steuerelement System (außerhalb bekannte Kalibrierungsparameter) Zustand und somit bereitzustellen Daten, die möglicherweise falsch interpretiert werden können

**Erhöhung von Berechtigungen**: ein Gerät, das bestimmte Funktion kann etwas anderes tun erzwungen werden. Beispielsweise kann ein Ventil, die so programmiert ist, öffnen Sie halb dazu veranlasst werden, um ganz zu öffnen.

**Denial-of-Service**: das Gerät in einen Zustand, in dem die Kommunikation nicht kann, aktiviert werden kann.

**Tampering**: das Gerät kann neu konfiguriert werden, um Benutzer in einem unbekannten an das Steuerelement System (außerhalb bekannte Kalibrierungsparameter) Zustand und somit bereitzustellen Daten, die möglicherweise falsch interpretiert werden können.
 
**Spoofing/Tampering/Zurückweisung**: Wenn nicht gesichert (Dies ist selten die Groß-/Kleinschreibung mit Consumer Remote-Steuerelemente) ein Angreifer kann den Status eines Geräts anonym bearbeiten. Eine gute Illustration wird Remote-Steuerelemente können, die alle TV aktivieren und die beliebte pubertären Tools sind.

#### <a name="communication"></a>Kommunikation

Bedrohungen um Kommunikationspfad zwischen den Geräten, Geräte und Feld Gateways und Geräte und Cloud-Gateway. In der folgenden Tabelle weist einige Anleitungen um offene Sockets auf dem Gerät/VPN:

| **Komponente**               | **Bedrohung** | **Risikominderung**                                      | **Risiko**                                                                                                      | **Implementierung**                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gerät IoT Hub              | TID        | (D) TLS (PSK/RSA) zur Verschlüsselung des Datenverkehrs             | Abhören oder beeinträchtigen die Kommunikation zwischen dem Gerät und dem gateway                             | Sicherheit für die Protokollebene. Mit benutzerdefinierten Protokolle müssen Sie herausfinden, wie Sie diese schützen. In den meisten Fällen erfolgt die Kommunikation vom Gerät an den IoT Hub (Gerät initiiert die Verbindung).                                                                                                                                                                 |
| Gerät               | TID        | (D) TLS (PSK/RSA) zur Verschlüsselung des Datenverkehrs.            | Lesen von Daten zwischen Geräten übertragen. Die Daten manipulieren. Das Gerät mit neue Verbindungen überladen | Sicherheit für die Protokollebene (MQTT/AMQP/HTTP/CoAP. Mit benutzerdefinierten Protokolle müssen Sie herausfinden, wie Sie diese schützen. Der Risikominderung für die DoS Bedrohung ist peer-Geräte über ein Gateway Cloud oder ein Feld, und lassen sie nur fungieren als Clients an das Netzwerk. Die peering eine direkte Verbindung zwischen den Peers nach müssen vom Gateway vermittelte wurden möglicherweise |
| Externe Entität Gerät      | TID        | Der externe Entität, die das Gerät starken Paarung | Die Verbindung zu dem Gerät ausspähen. Die Kommunikation stören mit dem Gerät                     | Eine Kopplung sichere externe Entität, die das Gerät NFK/Bluetooth LE. Steuern der betrieblichen Systemsteuerung des Geräts (physisch)                                                                                                                                                                                                                                                  |
| Feld Gateway-Cloud-Gateway | TID        | TLS (PSK/RSA) zur Verschlüsselung des Datenverkehrs.               | Abhören oder beeinträchtigen die Kommunikation zwischen dem Gerät und dem gateway                             | Sicherheit für die Protokollebene (MQTT/AMQP/HTTP/CoAP). Mit benutzerdefinierten Protokolle müssen Sie herausfinden, wie Sie diese schützen.                                                                                                                                                                                                                                                       |
| Device-Cloud-Gateway        | TID        | TLS (PSK/RSA) zur Verschlüsselung des Datenverkehrs.               | Abhören oder beeinträchtigen die Kommunikation zwischen dem Gerät und dem gateway                             | Sicherheit für die Protokollebene (MQTT/AMQP/HTTP/CoAP). Mit benutzerdefinierten Protokolle müssen Sie herausfinden, wie Sie diese schützen.                                                                                                                                                                                                                                                       |

Es folgen einige Beispiele der Bedrohungen in dieser Kategorie:

**Denial of Service**: eingeschränkte Geräte sind im Allgemeinen unter DoS Bedrohung Wenn sie aktiv für eingehende Verbindungen oder unerwünschte Datagramme in einem Netzwerk, hören, weil ein Angreifer öffnen kann viele Verbindungen parallel und nicht service sie oder sie sehr langsam service oder das Gerät mit unerwünschten Datenverkehr übertragen werden kann. In beiden Fällen kann das Gerät effektiv möglicherweise nicht mehr im Netzwerk gerendert werden.

**Spoofing, Offenlegung von Informationen**: eingeschränkte Geräte und spezieller Geräte haben häufig eine für alle Sicherheitsfunktionen wie Kennwort oder PIN Schutz oder geschäftswichtige vollständig vertrauen im Netzwerk, d. h., sie werden Zugriff auf Informationen zu erteilen, wenn ein Gerät im gleichen Netzwerk, und das Netzwerk häufig nur von einem freigegebenen Schlüssel geschützt ist. Dies bedeutet, dass bei der gemeinsame geheimen Schlüssel Gerät oder Netzwerk offen gelegt werden, es möglich ist, das Gerät zu steuern oder beobachten Daten vom Gerät ausgegeben.  

**Spoofing**: ein Angreifer intercept oder teilweise überschreiben die Übertragung und Absender (Man in der Mitte) Spoofing kann

**Tampering**: ein Angreifer abfangen oder teilweise überschreiben die Übertragung und falsche Informationen senden kann 

**Offenlegung von Informationen:** ein Angreifer auf eine Übertragung belauschen und Abrufen von Informationen ohne Genehmigung möglicherweise **Denial-of-Service:** ein Angreifer möglicherweise das broadcast Signal jam und Verteilung von Informationen zu verweigern

#### <a name="storage"></a>Speicher

Jedes Gerät und Feld Gateway über eine Speicher (temporär für die Daten, os Bildspeicher queuing) verfügt.

| **Komponente**                            | **Bedrohung** | **Risikominderung**                       | **Risiko**                                                                                                                                                                                                                                                                                                                | **Implementierung**                                                                                                                                                     |
|------------------------------------------|------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Speicher des Geräts                           | TRID       | Speicher-Verschlüsselung, die Protokolle signieren | Lesen von Daten aus dem Speicher (PII Daten), mit der Telemetriedaten Manipulation. Manipulieren der in der Warteschlange oder die zwischengespeicherten Daten der Befehl-Steuerelement. Manipulieren der Konfiguration oder Firmware Updatepakete kann während zwischengespeichert oder lokal in der Warteschlange zu OS und/oder System Komponenten Gefährdung führen                                         | Verschlüsselung, Message Authentication Code (MAC) oder die digitale Signatur. Dabei möglich ist, starken Zugriffssteuerung über Zugriff auf Ressourcen (Lists, ACLs) oder Berechtigungen steuern. |
| Betriebssystem des Geräteabbild                          | TRID       |                                      | Manipulieren der OS / ersetzen die Betriebssystemkomponenten                                                                                                                                                                                                                                                                         | Nur-Lese-OS Partition signiert Betriebssystemabbild, Verschlüsselung                                                                                                                    |
| Feld Gateway-Speicher (queuing Daten) | TRID       | Speicher-Verschlüsselung, die Protokolle signieren | Lesen von Daten aus dem Speicher (PII-Daten) Telemetriedaten manipulieren, manipulieren in der Warteschlange oder die zwischengespeicherten Daten der Befehl-Steuerelement. Manipulieren der Konfiguration oder Firmware Updatepakete (für Geräte oder Feld Gateway bestimmt) kann zwar zwischengespeichert oder lokal in der Warteschlange zu OS und/oder System Komponenten Gefährdung führen | BitLocker                                                                                                                                                              |
| Feld Gateway Betriebssystemabbilds                   | TRID       |                                      | Manipulieren der OS / ersetzen die Betriebssystemkomponenten                                                                                                                                                                                                                                                                          | Nur-Lese-OS-Partition, signiert Betriebssystemabbild, Verschlüsselung                                                                                                                    |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Gerät und Ereignis Verarbeitung/Cloud Gateway zone

Ein Cloud-Gateway ist System, das über öffentliches Netzwerk Speicherplatz, in der Regel in einer Cloud-basierten Steuerelement und Daten Analysesystem, einen Verbund derartiger Systeme Remotekommunikation from und to Geräte oder Feld Gateways aus mehreren verschiedenen Websites ermöglicht. In einigen Fällen kann ein Cloud-Gateway sofort spezieller Geräte aus Anschlüsse wie Tablets oder Telefone erleichtern. Im Kontext hier erläuterten "Cloud" sollte auf einem dedizierten Datenverarbeitungssystem verweisen, die nicht am selben Standort wie der angeschlossene Geräte oder Gateways Feld gebunden ist, und dabei operative Maßnahmen zu verhindern, dass zielorientierten physischen Zugriff, aber nicht mit einem "Öffentliche Cloud"-Infrastruktur.  Ein Cloud-Gateway kann in einem Netzwerk Virtualisierung Überlagerung das Cloud-Gateway und alle seine angeschlossene Geräte oder Feld Gateways aus anderen Netzwerkverkehr zu isolieren potenziell zugeordnet werden. Das Cloud-Gateway selbst ist weder ein Gerät-Verwaltungssystem noch eine Verarbeitung oder Speicher Facility für Gerätedaten. Diese Funktionen-Schnittstelle mit dem Cloud-Gateway. Die Cloud Gateway Zone umfasst das Cloud Gateway selbst sowie alle dar-Gateways und Geräte direkt oder indirekt als Anlage.

Cloud-Gateway ist hauptsächlich benutzerdefinierten integrierten Software als Dienst verfügbar gemachten Endpunkte mit denen Feld Gateway und Geräten eine Verbindung mit. Sie müssen als solche unter Einhaltung der Sicherheit konzipiert. Führen Sie [SDL](http://www.microsoft.com/sdl) Prozess zum Entwerfen und Erstellen von diesem Dienst. 

#### <a name="services-zone"></a>Services-zone

Ein Steuerelement-System (oder Controller) ist eine softwarelösung, die mit einem Gerät oder ein Feld Gateway oder Cloud-Gateway zum Steuern von einem oder mehreren Geräten und/oder für sammeln und/oder speichern und Analysieren von Gerätedaten für die Präsentation oder nachfolgende Kontrolle Schnittstellen. Verwaltungssysteme sind die einzigen Entitäten im Rahmen dieser Diskussion, die unmittelbar Interaktion mit Personen erleichtern. Die Ausnahme sind intermediate physischen Kontroll-Oberflächen auf Geräten, wie ein Schalter, mit der eine Person benennen das Gerät abschalten oder andere Eigenschaften kann, und für die es keine funktionale Entsprechung, die Digital zugegriffen werden kann. 

Intermediate physischen Kontroll-Oberflächen sind, in dem jede Art von Steuern einer Logik schränkt die Funktion der physischen Steuerelement Oberfläche so, dass eine entsprechende Funktion Remote initiiert werden kann oder input Konflikte mit remote Input können vermieden werden – solche intermediated Steuerelement Flächen sind im Prinzip zugeordnet, mit einer lokalen Verwaltungssystem, die zugrunde liegenden dieselbe Funktionalität wie jedes andere Remotesteuerung System nutzt die parallel das Gerät zugeordnet werden kann. Obere Bedrohungen für die Cloud computing zur [Cloud Sicherheit Allianz (CSA)](https://cloudsecurityalliance.org/research/top-threats/) Seite nicht gelesen werden können.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

Finden Sie in den folgenden Artikeln Weitere Informationen:

- [SDL Bedrohung Modellierungstool](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
- [Microsoft Azure IoT Referenzarchitektur](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)
 
