<properties
    pageTitle="Verwalten und Überwachen Ihrer Verbindern und API-Apps im App-Dienst | Microsoft Azure"
    description="Anzeigen der Leistung von Verbindern und API Apps in Logik Apps; Microservices Architektur"
    services="app-service\logic"
    documentationCenter=".net,nodejs,java"
    authors="MandiOhlinger"
    manager="anneta"
    editor="cgronlun"/>

<tags
    ms.service="logic-apps"
    ms.workload="integration"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/18/2016"
    ms.author="mandia"/>

# <a name="manage-and-monitor-your-built-in-api-apps-and-connectors"></a>Verwalten Sie und überwachen Sie Ihrer integrierten API Apps und Verbinder

>[AZURE.NOTE] Diese Version des Artikels gilt Logik apps 2014-12-01-Schema Vorschauversion aus.

Sie haben eine integrierte API App erstellt. Und was jetzt?

In Azure wird jeder API App einer separaten Website gehostet auf Azure. Daher können Sie leicht erkennen, wie viele Anfragen vorgenommen wurden, und sehen, wie viele Daten von der Verbinder verwendet wird. Sie können auch Ihre API App sichern, Benachrichtigungen erstellen, Folie Sicherheit aktivieren und Hinzufügen von Benutzern und Rollen.

In diesem Thema werden einige der anderen Optionen, um Ihre App API verwalten.

Wenn diese integrierten Features anzeigen möchten, öffnen Sie Ihre App API im [Azure-Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040)aus. Ist die API-App auf Ihrem Startboard, wählen Sie darauf, um die Eigenschaften zu öffnen. Sie können auch wählen Sie **Durchsuchen**, wählen Sie **API Apps**, und wählen Sie dann Ihre API App:

![][browse]

## <a name="see-the-properties-you-entered"></a>Finden Sie die Eigenschaften, die Sie eingegeben haben.

Wenn Sie die API App öffnen, gibt es verschiedene Funktionen und Aufgaben zur Verfügung:

![][settings]

Sie können:

- **Einstellungen** zeigt bestimmte Informationen über die API-App, einschließlich der Seite Abonnementdetails und listet die Benutzer, die auf Ihre app API zugreifen. Sie können auch vergrößern oder verkleinern die Anzahl der Instanzen der App-API mithilfe des Features "Skalierung"; zwischen anderen Features.
- Verwenden Sie die Schaltflächen **Starten** und **Beenden** , können Sie die App API steuern.
- Wenn die zugrunde liegenden Dateien verwendet werden, indem Sie Ihre App API Produktupdates vorgenommen werden, können Sie **Aktualisieren** , um die neuesten Versionen abrufen klicken. Wenn Sie ein Update oder ein von Microsoft veröffentlichte Sicherheitsupdate vorhanden ist, aktualisiert beispielsweise automatisch **Aktualisieren** auf Ihre App-API zum Einschließen dieses Fix.
- Wählen Sie Upgrade oder Downgrade anhand Ihrer Daten Verwendung der App API **Änderung ausführen möchten** . Dieses Feature können Sie auch die Verwendung Ihrer Daten finden Sie unter.
- Beim Erstellen eines Verbinders, das Tabellen, wie der SQL-Verbinder enthält, können Sie optional einen Tabellennamen zum Herstellen einer Verbindung mit eingeben. Ein Schema basierend auf der Tabelle wird automatisch erstellt und zur Verfügung, wenn Sie **Schemas herunterladen**klicken Sie auf. Dieses heruntergeladene Schema können dann um eine Transformation oder ein Schema zu erstellen.

## <a name="change-your-connector-or-api-configuration-values-you-entered"></a>Ändern der Verbinder oder API Konfigurationswerte, die Sie eingegeben haben.

Nachdem Sie konfiguriert oder den integrierten Verbinder erstellt haben, können Sie die Werte ändern, den, die Sie eingegeben haben. Angenommen, wenn Sie den SQL-Connector konfiguriert und der SQL Server-Namen oder Tabellennamen ändern möchten, können Sie dies in das Blade API App für den Verbinder ausführen.

Schritte umfassen:

1. Der Verbinder oder API App zu öffnen. Wenn Sie dies tun, wird das Blade API App geöffnet.
2. Klicken Sie in **Essentials**auf den Link unter der Eigenschaft Host. Der Hyperlink wird wie *Slackconnector* oder *microsoftsqlconnector123*benannt:

    ![][apiapphost]

3. Wählen Sie in das Blade API App Host **Einstellungen**aus. Markieren Sie in das Blade Einstellungen **Application Settings**. Die Konfigurationswerte sind unter **App-Einstellungen**aufgelistet:

    ![][hostsettings]

4. Klicken Sie auf die Einstellung, die Sie ändern möchten, geben Sie den neuen Wert, und **Speichern Sie** Ihre Änderungen.


## <a name="install-the-hybrid-connection-manager---optional"></a>Installieren der Hybrid Verbindungs-Manager - Optional

![][hcsetup]

Der Hybrid-Verbindungs-Managers gibt Ihnen die Möglichkeit, eine Verbindung mit einem lokalen System, wie SQL Server oder SAP. Diese Hybrid-Konnektivität verwendet Azure-Dienstbus Verbindung herzustellen und die Sicherheit zwischen Azure Ressourcen und lokale Ressourcen steuern.

[Mithilfe der Hybrid-Verbindungs-Managers in Azure App-Dienst](app-service-logic-hybrid-connection-manager.md)finden Sie unter.

> [AZURE.NOTE] Hybrid-Verbindungs-Managers ist erforderlich, nur, wenn Sie sich hinter der Firewall mit einer lokalen Ressource verbunden sind. Wenn Sie nicht zu einem lokalen System herstellen, möglicherweise nicht in der Verbinder Blade Hybrid Verbindungs-Managers aufgeführt.

## <a name="monitor-the-performance"></a>Überwachen der Leistung
Performance-Werte sind integrierte Features und enthalten mit jeder API-App, die Sie erstellen. Diese Kennzahlen gelten nur für Ihre API App in Azure gehostet wird. Beispiel für Kriterien:

![][monitoring]

Sie können:

- Markieren Sie **Anfragen und Fehler** unterschiedliche Performance-Werte einschließlich häufig bekannte HTTP-Fehlercodes wie 200, 400 oder 500 HTTP Statuscodes hinzuzufügen. Sie können auch finden Sie unter Reaktionszeiten, sehen, wie viele Anfragen bei der App API vorgenommen werden, und finden Sie unter wie viele Daten zum Einsatz und wie viele Daten abgeschaltet. Basierend auf den Performance-Werte, können Sie erstellen e-Mail-Benachrichtigungen eine Metrik einen Schwellenwert Ihrer Wahl übersteigt.
- **Verwendung**, können Sie sehen wie viel **CPU** von der App API verwendet wird, überprüfen Sie die aktuelle **Einsatzkontingent** in MB und Ihrer Verwendung von maximale Daten basieren auf Ihre Kosten Kategorie anzeigen. **Geschätzt aufwenden** helfen Ihnen die potenziellen Kosten des Ausführens der App API zu bestimmen.
- Wählen Sie **Prozesse** Process Explorer öffnen. Der Web-Instanzen und deren Eigenschaften, einschließlich Thread zählen und Speicherkapazität Verwendung zeigt.

Mit diesen Tools, können Sie feststellen, ob das Planen der App-Service sollte skaliert nach oben oder nach unten, basierend auf den Bedürfnissen Ihres Unternehmens skaliert werden. Diese Features sind integrierte Portal mit keine weiteren Tools erforderlich.

## <a name="control-the-security"></a>Steuern der Sicherheits

Apps-API verwenden, rollenbasierte Sicherheit. Diese Rollen gelten für die gesamte Azure zur Verfügung steht, einschließlich API Apps und anderen Ressourcen Azure. Die Rollen beinhalten:

Rolle | Beschreibung
--- | ---
Besitzer | Vollzugriff auf die Verwaltungsoption und anderen Benutzern oder Gruppen Zugriff gewähren.
Mitwirkenden | Haben Sie Vollzugriff auf die Verwaltungsoption. Kann nicht für andere Benutzer oder Gruppen den Zugriff gewähren.
Reader | Kann alle Ressourcen mit Ausnahme von vertraulichen Daten anzeigen
Access-Administrator für Benutzer | Anzeigen aller Ressourcen, die Rollen erstellen/verwalten und erstellen/verwalten Tickets unterstützen.

Finden Sie unter [rollenbasierte Access-Steuerelement im Microsoft Azure-Portal](../active-directory/role-based-access-control-configure.md).

Sie können ganz einfach Hinzufügen von Benutzern und bestimmte Rollen in Ihrer App API zuordnen. Im Portal werden Benutzer, die Zugriff und Rolle haben:

![][access]  

- Wählen Sie **Benutzer** zum Hinzufügen eines Benutzers und Zuweisen einer Rolle Entfernen eines Benutzers aus.
- Wählen Sie die **Rollen** an alle Benutzer in einer bestimmten Rolle, finden Sie unter Hinzufügen eines Benutzers zu einer Rolle aus, und Entfernen eines Benutzers aus einer Rolle.


## <a name="more-good-stuff"></a>Weitere gute von Inhalten
- Wählen Sie **-API-Definition** , um die automatisch erstellte Swagger Datei für Ihre bestimmte API-app zu öffnen.
- Wählen Sie die **Abhängigkeiten** , um die von der App API benötigten Dateien anzuzeigen. Wenn Sie den SAP-Connector verwenden, installieren Sie einige zusätzlichen Dateien auf den lokalen Hybrid-Verbindungs-Manager. Diese Abhängigkeiten werden in Ihrem app-Blade API angezeigt.

>[AZURE.IMPORTANT] Wenn Sie Ihre API app-Eigenschaften zu öffnen, und sehen Sie unter **Essentials**nach, gibt es **Host** und dem **Gateway** Links, die neue Blades zu öffnen:
>
> ![][host]
>
>Diese Eigenschaften sind speziell für die Website, die auf der App API gehostet wird. Bei Verwendung eines integrierten API App oder den Verbinder wird die meisten dieser Eigenschaften nicht wirklich anwenden, und es wird empfohlen, dass Sie diese Eigenschaften nicht aktualisieren. Wenn Sie eigene API-App in Visual Studio erstellt haben und es zu Ihrem Abonnement Azure bereitgestellt werden, können Sie die Blades Host und dem Gateway verwenden. <br/><br/>


>[AZURE.NOTE] Wechseln Sie zu mit Logik Apps für ein Azure-Konto anmelden, bevor Sie zu [Versuchen Logik App](https://tryappservice.azure.com/?appservice=logic). Sie können eine kurzlebige Starter Logik app erstellen. Keine Zusagen, und keine Kreditkarten erforderlich.

## <a name="read-more"></a>Weitere Informationen

[Überwachen Sie Ihrer Apps Logik](app-service-logic-monitor-your-logic-apps.md)<br/>
[Verbinder und API Apps-Liste in der App-Dienst](app-service-logic-connectors-list.md)<br/>
[Rollenbasierte Access-Steuerelements im Microsoft Azure-Portal](../active-directory/role-based-access-control-configure.md)<br/>
[Verwenden die Hybrid-Verbindungs-Managers in Azure App-Verwaltungsdienst](app-service-logic-hybrid-connection-manager.md)


<!--Image references-->
[browse]: ./media/app-service-logic-monitor-your-connectors/browse.png
[settings]: ./media/app-service-logic-monitor-your-connectors/settings.png
[hcsetup]: ./media/app-service-logic-monitor-your-connectors/hcsetup.png
[monitoring]: ./media/app-service-logic-monitor-your-connectors/monitoring.png
[access]: ./media/app-service-logic-monitor-your-connectors/access.png
[host]: ./media/app-service-logic-monitor-your-connectors/host.png
[hostsettings]: ./media/app-service-logic-monitor-your-connectors/hostsettings.png
[apiapphost]: ./media/app-service-logic-monitor-your-connectors/apiapphost.png
