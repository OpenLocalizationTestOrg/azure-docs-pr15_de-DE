<properties 
    pageTitle="Was sind Logik Apps aus?" 
    description="Erfahren Sie mehr über die App-Dienst Logik Apps" 
    authors="kevinlam1" 
    manager="dwrede" 
    editor="" 
    services="logic-apps" 
    documentationCenter=""/>

<tags
    ms.service="logic-apps"
    ms.workload="na"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="hero-article" 
    ms.date="10/12/2016"
    ms.author="klam"/>

# <a name="what-are-logic-apps"></a>Was sind Logik Apps aus?

Apps Logik Möglichkeit zur Vereinfachung und skalierbare Integration und Workflows in der Cloud zu implementieren. Es stellt einen visuellen Designer zum Modellieren und Ihren Prozess als eine Folge von Schritten bekannt als Workflow automatisieren.  Es gibt [viele Verbinder](../connectors/apis-list.md) in die Cloud und lokalen schnell über die Dienste und Protokolle integriert werden soll.  Eine app Logik zu einem Trigger (gefällt mir 'beim Hinzufügen ein Kontos zu Dynamics CRM') beginnt und nach Auslösen viele Kombinationen Aktionen, Konvertierungen und Bedingung Logik beginnen kann.

Vorteile der Verwendung von Apps Logik umfassen Folgendes:  

- Sparen Sie Zeit durch das Entwerfen komplexer Geschäftsprozessen mit einfach zu verstehen, Entwurfstools
- Nahtloses Implementierung von Mustern und Workflows, die andernfalls schwierig zu implementieren Code wäre
- Erste Schritte schnell auf Grundlage von Vorlagen
- Anpassen der Logik app mit APIs, Ihre eigenen benutzerdefinierten Code und Aktionen
- Herstellen einer Verbindung und synchronisieren Sie unterschiedliche Systeme über lokal und in der cloud
- Erstellen Sie vom BizTalk Server-API Management, Azure-Funktionen und Azure-Dienstbus mit erster Klasse Integration Unterstützung

Logik Apps ist eine vollständig verwaltete iPaaS (Integration Plattform als Dienst) da Entwickler keine Gedanken über das Erstellen von gehostet, Skalierbarkeit, Verfügbarkeit und Management zu machen.  Logik Apps werden automatisch nach oben skaliert Nachfrage zu.

![Datenfluss app-designer](./media/app-service-logic-what-are-logic-apps/LogicAppCapture2.png)

Wie erwähnt, mit Logik Apps, können Sie Geschäftsprozesse automatisieren. Es folgen einige Beispiele:  
 
* Verschieben von Dateien an einem FTP-Server in Azure-Speicher hochgeladen werden.
* Prozess und Routing Bestellungen über lokalen und cloud-Systeme
* Überwachen alle Tweets zu einem bestimmten Thema, die Absicht analysieren und Erstellen von Benachrichtigungen und Aufgaben für Elemente zuweisen benötigen.

Wie die folgenden Szenarien können alle von den visuellen Designer und ohne Schreiben von Code eine einzelne Zeile konfiguriert sein. Erste Schritte bei der [erstellen jetzt Ihre Logik app][create].  Nach dem schreiben - kann eine app Logik in mehreren Umgebungen und Regionen [schnell bereitgestellt und konfiguriert](app-service-logic-create-deploy-template.md) sein.

## <a name="why-logic-apps"></a>Warum Logik Apps?

Logik Apps bringt Geschwindigkeit und Skalierbarkeit in Enterprise-Integration Segment an.  Das Center für erleichterte Bedienung des Designers, Vielzahl von verfügbaren Trigger und Aktionen und leistungsstarke Verwaltungstools stellen zentrale Ihrer APIs einfacher denn je.  Wie Unternehmen in Richtung Digitalization verschieben möchten, können Logik Apps Sie älterer Versionen und überlegen Systeme miteinander zu verbinden.

Darüber hinaus mit Ihrem [Konto für Enterprise-Integration] [ biztalk] Sie können um Szenarien zur Integration mit mit einer [XML-messaging]enger skalieren[xml], [trading Partner Management][tpm], und vieles mehr.

- **Benutzerfreundliche Entwurfstools** - Logik Apps gestalteten End-to-End im Browser oder mit Visual Studio-Tools werden können. Mit einem Trigger – von einem einfachen Zeitplan zu starten, wenn ein Problem GitHub erstellt wird. Klicken Sie dann koordinieren Sie eine beliebige Anzahl von Aktionen mit den leistungsfähigen Katalog der Verbinder aus.

- **Verbinden APIs einfach** – sogar Komposition Aufgaben, die einfach zu beschreiben, sind, erschweren Code implementieren. Logik Apps erleichtert das verschiedenartige Systeme zu verbinden. Der marketing-Lösung in Ihrer lokalen Cloud verbinden möchten Abrechnung System? Möchten Sie über APIs und Systeme mit Unternehmendienstbus messaging zentrales? Logik apps sind die schnellste, besonders zuverlässigen Methode Lösungen für diese Probleme vorführen.

- **Erste Schritte auf Grundlage von Vorlagen schnell** - helfen Ihnen beim Einstieg haben wir einem [Katalog von Vorlagen] bereitgestellt[ templates] , bei denen Sie einige allgemeinen Lösungsmöglichkeiten rasch erstellen zu können. Aus Sie erweiterte B2B Lösungen zu einfache SaaS Konnektivität und sogar ein Paar, sind nur 'für Spaß': im Katalog ist die schnellste Möglichkeit zum Einstieg in die Potenz Logik Apps.

- **Erweiterbarkeit integrierten Add-in** - nicht finden Sie unter den Verbinder, die Sie benötigen? Logik Apps dient zum Arbeiten mit Ihrem eigenen APIs und Code. Sie können einfach eigene API app zum Verwenden eines benutzerdefinierten Verbinders, oder rufen Sie in einer [Azure-Funktion](https://functions.azure.com) zum Ausführen von Code bei Bedarf Codeausschnitte erstellen. 

- **Real Integration Pferdestärken (PS)** – einfach starten und wächst, wie Sie benötigen. Logik Apps kann einfach nutzen der BizTalk, die Lösung von Microsoft Branche führenden Integration Integration-Experten, die die erläuterten benötigten aktivieren. Erfahren Sie mehr über das [Enterprise Integration Pack](./app-service-logic-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Logik App Konzepte

Im folgenden werden einige der wichtigsten, die mit der Logik Apps umfassen. 

- **Workflow** - Apps Logik bietet grafisch zu modellieren Ihrer Geschäftsprozesse als eine Reihe von Schritten oder eines Workflows an.
- **Verwaltete Verbinder** - Ihrer apps Logik benötigen Zugriff auf Daten und Dienste. Verwaltete Verbinder werden speziell um Hilfe für das Herstellen einer Verbindung mit und Arbeiten mit Ihren Daten erstellt. Finden Sie in der Liste der Verbinder, die zurzeit in [verwaltete Verbinder]verfügbar[managedapis].
- **Trigger** - einige verwaltete Verbinder kann auch als Trigger fungieren. Ein Trigger startet eine neue Instanz eines Workflows basierend auf ein bestimmtes Ereignis, wie das Eintreffen einer e-Mail-Nachricht oder eine Änderung in Ihr Konto Azure-Speicher.
-  **Aktionen** - jeden Schritt nach der Trigger in einem Workflow eine Aktion aufgerufen wird. Jede Aktion wird in der Regel ein Vorgang auf Ihrem verwalteten Verbinder oder benutzerdefinierte API apps zugeordnet.
- **Enterprise-Integration Pack** - enthält Funktionen, die von BizTalk für komplexere Integrationsszenarios, Logik Apps aus. BizTalk ist Microsoft Branche führenden Integrationsplattform. Der Verbinder Enterprise Integration Pack können Sie auf einfache Weise Überprüfung, Transformation und weiteren Funktionen in Ihrer App Logik Workflows einbeziehen.

## <a name="getting-started"></a>Erste Schritte  

- Um mit Logik Apps anzufangen, führen Sie das [Erstellen einer App Logik] [ create] Lernprogramm.  
- [Allgemeine Beispiele anzeigen und Szenarien](app-service-logic-examples-and-scenarios.md)
- [Sie können Automatisieren von Geschäftsprozessen mit Logik Apps](http://channel9.msdn.com/Events/Build/2016/T694) 
- [Erfahren Sie, wie Ihre Systeme mit Logik Apps integriert werden soll.](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: app-service-logic-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: app-service-logic-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: app-service-logic-enterprise-integration-accounts.md
[xml]: app-service-logic-enterprise-integration-b2b.md
[templates]: app-service-logic-use-logic-app-templates.md
