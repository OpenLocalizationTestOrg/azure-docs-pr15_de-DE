<properties
    pageTitle="Verwalten Sie Ihre erste API in Azure-API Management | Microsoft Azure"
    description="Informationen Sie zum Erstellen APIs, Vorgänge hinzufügen und erste Schritte mit API-Verwaltung."
    services="api-management"
    documentationCenter=""
    authors="steved0x"
    manager="erikre"
    editor=""/>

<tags
    ms.service="api-management"
    ms.workload="mobile"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="hero-article"
    ms.date="10/25/2016"
    ms.author="sdanie"/>

# <a name="manage-your-first-api-in-azure-api-management"></a>Der erste API in Azure-API Management verwalten

## <a name="overview"> </a>(Übersicht)

Dieser Anleitung erfahren Sie, wie schnell erste Schritte bei der Verwendung von Azure-API Management, und nehmen Sie Ihre ersten API Anruf.

## <a name="concepts"> </a>Was Azure-API Management ist?

Azure-API Management können Sie nehmen Sie alle Back-End- und auf deren Grundlage ein vollwertiges API-Programm starten.

Häufige Szenarien umfassen:

* **Sichern von mobilen Infrastruktur** durch Threadbegrenzung Zugriff mit API Tasten, verhindern von DOS-Angriffen mithilfe von begrenzungsebene, oder verwenden erweiterte Sicherheitsrichtlinien wie JWT token Überprüfung.
* Der **Aktivierung ISV Partner-Ökosysteme** durch schnelle Partner Onboarding durch die Entwicklerportal Geschenk und Erstellen einer API Fassade von internen Implementierungen entkoppeln, die nicht für Partner Ernährung ripe sind.
* **Eine interne API Programm ausführen** , indem Sie bietet einen zentralen Ort für die Organisation Kommunikation über die Verfügbarkeit und die neuesten Änderungen APIs, Threadbegrenzung Zugriff auf Grundlage der Organisationskonten, alle auf einem gesicherten Kanal zwischen dem API Gateway und der Back-End-basiert.


Das System besteht aus den folgenden Komponenten:

* Das **API-Gateway** ist den Endpunkt:
  * Akzeptiert API ruft und leitet diese an Ihre Downloadzeit.
  * Überprüft API Tasten, JWT Token, Zertifikate und anderer Anmeldeinformationen.
  * Erzwingt Verwendung von Kontingenten und bewerten Grenzwerte.
  * Wandelt Ihre API im laufenden Betrieb ohne Code Änderungen an.
  * Speichert die Back-End-Antworten in dem einrichten.
  * Rufen Sie Protokolle Metadaten Analytics Zwecken ein.

* Das **Publisher-Portal** ist die administrative Schnittstelle, in dem Sie Ihr Programm API einrichten. Verwendungszweck:
    * Definieren oder API Schema importieren.
    * Paket APIs in Produkte.
    * Richten Sie Richtlinien wie Kontingente oder Transformationen auf die APIs aus.
    * Rufen Sie Einblicke in Analytics ein.
    * Verwalten von Benutzern.

* Die **Entwicklerportal** dient als Hauptfenster Web Anwesenheitsinformationen für Entwickler, können sie hier:
    * Lesen API-Dokumentation.
    * Testen Sie eine API über die interaktive Konsole aus.
    * Erstellen eines Kontos, und abonnieren um API Tasten zu erhalten.
    * Klicken Sie auf eigene Verwendung Access-Analytics.


## <a name="create-service-instance"> </a>Erstellen Sie eine Instanz Management-API

>[AZURE.NOTE] Damit dieses Lernprogramm abgeschlossen, benötigen Sie ein Azure-Konto an. Wenn Sie kein Konto haben, können Sie ein kostenloses Konto nur wenigen Minuten erstellen. Weitere Informationen finden Sie unter [Azure kostenlose Testversion][].

Der erste Schritt beim Arbeiten mit API Management besteht im Erstellen einer Serviceinstanz. Melden Sie sich bei der [Klassischen Azure-Portal][] an, und klicken Sie auf **neu**, **App Dienste**, **API Management** **Erstellen**.

![Neue Instanz Management-API][api-management-create-instance-menu]

Geben Sie für die **URL**einen eindeutigen Unterdomäne Namen für die URL verwendet werden soll.

Wählen Sie das gewünschte **Abonnement** und die **Region** für Ihre Service-Instanz aus. Klicken Sie nachdem Sie Ihre Auswahl getroffen haben auf die Schaltfläche **Weiter** .

![Neue API-Verwaltungsdienst][api-management-create-instance-step1]

Geben Sie **Contoso Ltd.** für den **Namen der Organisation**und geben Sie Ihre e-Mail-Adresse im Feld **Administrator E-Mail** .

>[AZURE.NOTE] Diese e-Mail-Adresse ist für Benachrichtigungen aus der System-API verwendet. Weitere Informationen finden Sie unter [Konfigurieren von Benachrichtigungen und e-Mail-Vorlagen in Azure-API Management][].

![Neue API-Verwaltungsdienst][api-management-create-instance-step2]

-API Management Service Instanzen stehen in drei Versionen: Developer, Standard und Premium. Standardmäßig werden neue Instanzen von API Management-Dienst in der Entwicklertools Ebene erstellt. Wählen Sie die Ebene Standard oder Premium, aktivieren Sie das Kontrollkästchen **Erweiterte Einstellungen** , und wählen Sie die gewünschte Ebene in der folgenden Abbildung.

>[AZURE.NOTE] Der Entwickler in ist für die Entwicklung, testen und Pilotprojekt API Programme Stelle, an der hoher Verfügbarkeit kein Belang ist. In der Standard- und Premium Stufen können Sie Ihre reservierte Einheit zählen ', damit weitere Datenverkehr verarbeiten skalieren. Die Standard- und Premium Ebenen bieten Ihrer API Verwaltungsdienst mit besonders Leistung und der Leistung. Sie können dieses Lernprogramms abgeschlossen haben, mithilfe einer beliebigen Ebene. Weitere Informationen zur Verwaltung API Ebenen finden Sie unter [Verwaltung API Preise][].

Klicken Sie auf das entsprechende Kontrollkästchen Ihrer Service-Instanz zu erstellen.

![Neue API-Verwaltungsdienst][api-management-instance-created]

Nachdem die Instanz des Diensts erstellt wurde, besteht der nächste Schritt zum Erstellen oder Importieren einer API.

## <a name="create-api"> </a>Eine API importieren

Eine API besteht aus einer Reihe von Vorgängen, die von einer Clientanwendung aufgerufen werden können. Proxy auf vorhandene Webdienste-API Vorgänge sind.

APIs erstellt werden können (und Vorgänge hinzugefügt werden können) manuell, oder Sie können importiert werden. In diesem Lernprogramm werden die API für eine Stichprobe Taschenrechner Webdienst von Microsoft bereitgestellt und auf Azure gehostet importiert.

>[AZURE.NOTE] Anleitung zum Erstellen einer API und manuellen Hinzufügen von Vorgängen finden Sie unter [Verfahren zum Erstellen von APIs](api-management-howto-create-apis.md) und [zum Hinzufügen von Vorgängen zu einer API](api-management-howto-add-operations.md).

APIs sind im Publisher-Portal konfiguriert das über die klassischen Azure-Portal zugegriffen werden kann. Um das Publisher-Portal erreicht haben, klicken Sie auf **Verwalten** im klassischen Azure-Portal für Ihre API Verwaltungsdienst.

![Publisher-portal][api-management-management-console]

Informationen zum Importieren den Taschenrechner API klicken Sie im Menü " **API Management** " auf der linken Seite auf **APIs** , und klicken Sie dann auf **API importieren**.

![Der-API-Importschaltfläche][api-management-import-api]

Führen Sie die folgenden Schritte aus, um den Rechner API zu konfigurieren:

1. Klicken Sie auf **Aus URL**, geben Sie **http://calcapi.cloudapp.net/calcapi.json** in das Textfeld **Spezifikation Dokument-URL** ein, und klicken Sie auf das Optionsfeld **Swagger** .
2. Geben Sie in das Textfeld **Web API URL-Suffix** **Calc** ein.
3. Klicken Sie im Feld **Produkte (optional)** ein, und wählen Sie **Starter**.
4. Klicken Sie auf **Speichern** , um die API importieren.

![Hinzufügen von neuen API][api-management-import-new-api]

>[AZURE.NOTE] **Verwaltung von API** unterstützt derzeit Version 1.2 und 2.0 Swagger Dokument für den Import. Sicherstellen, dass, obwohl [Swagger 2.0-Spezifikation](http://swagger.io/specification) , deklariert `host`, `basePath`, und `schemes` Eigenschaften optional sind, **müssen** Swagger 2.0 Dokument enthalten diese Eigenschaften; Andernfalls wird wird nicht es importiert. 

Sobald die API importiert sind, wird die Zusammenfassungsseite für die API im Portal Publisher angezeigt.

![Zusammenfassung der API][api-management-imported-api-summary]

Im Abschnitt API weist mehrere Registerkarten an. Die Registerkarte **Zusammenfassung** zeigt grundlegende Metrik und Informationen über die API. Die Registerkarte [Einstellungen](api-management-howto-create-apis.md#configure-api-settings) wird zum Anzeigen und bearbeiten die Konfiguration für eine API verwendet. Zum Verwalten der im-API Vorgänge, wird die Registerkarte [Vorgänge](api-management-howto-add-operations.md) verwendet. Die Registerkarte **Sicherheit** kann Gateway-Authentifizierung für die Back-End-Server mit Standardauthentifizierung oder [gemeinsamen Zertifikatauthentifizierung](api-management-howto-mutual-certificates.md)konfigurieren und so konfigurieren Sie die [Autorisierung des Benutzers mithilfe OAuth 2.0](api-management-howto-oauth2.md)verwendet werden.  Die Registerkarte **Probleme** wird zum Anzeigen von der Entwickler, die Ihre APIs gemeldeten Probleme. So konfigurieren Sie die Produkte, die diese API enthalten, wird die Registerkarte **Produkte** verwendet.

Standardmäßig wird jede Instanz-API Management mit zwei Stichproben Produkten geliefert:

-   **Starter**
-   **Unbegrenzte**

In diesem Lernprogramm wurde der grundlegenden Rechner-API beim Import der API mit dem Produkt Starter hinzugefügt.

Um eine API anrufen, müssen Entwickler zunächst ein Produkt abonnieren, die sie darauf zugreifen können. Entwickler können Produkte in die Entwicklerportal abonnieren oder Administratoren können Entwickler zu Products im Portal Publisher abonnieren. Sie können ein Administrator sind, da die Instanz-API Management in den vorherigen Schritten in der Lernprogramm erstellt werden, sodass Sie bereits standardmäßig jedes Produkt abonniert haben.

## <a name="call-operation"> </a>Rufen Sie die Entwicklerportal ein Vorgangs

Vorgänge können direkt aus der Entwicklerportal, bietet eine bequeme Möglichkeit zum Anzeigen und testen die Vorgänge einer API aufgerufen werden. Rufen Sie in diesem Lernprogramm Schritt der grundlegenden Taschenrechner API **Hinzufügen zwei ganzen** Vorgang. Klicken Sie auf **Entwicklerportal** aus dem Menü am oberen rechten Ecke des Publisher-Portals.

![Entwicklerportal][api-management-developer-portal-menu]

Klicken Sie im oberen Menü auf **APIs** , und klicken Sie dann auf **Grundlegende Taschenrechner** , um die verfügbaren Vorgänge anzuzeigen.

![Entwicklerportal][api-management-developer-portal-calc-api]

Beachten Sie die Beschreibungen der Stichprobe und Parameter, die importiert wurden, zusammen mit dem API und JOIN-Operationen, beibringen für die Entwickler, die diesen Vorgang verwendet wird. Diese Art von Beschreibung können auch hinzugefügt werden, wenn Vorgänge manuell hinzugefügt werden.

Klicken Sie zum Aufrufen des Vorgangs **zwei Zahlen hinzufügen** , **Probieren Sie es**aus.

![Versuch es][api-management-developer-portal-calc-api-console]

Sie können einige Werte für die Parameter eingeben oder übernehmen Sie die Standardeinstellungen, und klicken Sie dann auf **Senden**.

![HTTP abrufen][api-management-invoke-get]

Nachdem ein Vorgang aufgerufen wird, zeigt Entwicklerportal den **Status der Antwort**, der **Antwort-Header**und **Inhalt der Antwort**an.

![Antwort][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Analytics anzeigen

Um Analytics für grundlegende Rechner anzuzeigen, wechseln Sie zurück zu Publisher-Portal durch Auswahl **Verwalten** im Menü am oberen rechten Ecke der Entwicklerportal.

![Verwalten][api-management-manage-menu]

Die Standardansicht für das Publisher-Portal ist **Dashboards**, die einen Überblick über Ihre API Management-Instanz bereitstellt.

![Dashboard][api-management-dashboard]

Richten Sie den Mauszeiger über dem Diagramm für **Grundlegende Taschenrechner** , die bestimmten Kriterien für die Verwendung der API für einen bestimmten Zeitraum angezeigt.

>[AZURE.NOTE] Wenn Sie alle Zeilen auf dem Diagramm angezeigt werden, wechseln Sie zurück zu den Entwicklerportal und einige Anrufe in das API, warten Sie einige Minuten, und kehren Sie danach zu dem Dashboard.

Klicken Sie auf **Details anzeigen** , wenn die Zusammenfassungsseite für die-API, einschließlich einer größeren Version der angezeigten Metrik anzuzeigen.

![Analytics][api-management-mouse-over]

![Zusammenfassung][api-management-api-summary-metrics]

Ausführliche Metrik und Reports klicken Sie auf **Analytics** aus dem Menü **API Management** auf der linken Seite.

![(Übersicht)][api-management-analytics-overview]

Im Abschnitt **Analytics** weist die folgenden vier Registerkarten:

-   **Auf einen Blick** bietet Kriterien für insgesamt Verwendung und Gesundheit, als auch die besten Entwickler, Top-Produkte, Top-APIs und verwendete Vorgänge.
-   **Verwendung** stellt einen detaillierten Einblick in API Anrufe und Bandbreite, einschließlich einer geografischen Darstellung.
-   Statuscodes zum **Systemzustand** Schwerpunkt cache Erfolg Sätzen, Reaktionszeiten und API und Reaktionszeiten service.
-   **Aktivität** bietet Berichte, die einen Drilldown auf die bestimmte Aktivität nach Entwicklertools, Produkt, API und Vorgang an.

## <a name="next-steps"> </a>Nächste Schritte

- Erfahren Sie, wie [Schützen Ihrer API mit Zins Grenzwerte](api-management-howto-product-with-rules.md).

[Azure kostenlose Testversion]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Konfigurieren von Benachrichtigungen und e-Mail-Vorlagen in Azure-API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[Projektmanagement-API Preise]: http://azure.microsoft.com/pricing/details/api-management/

[Azure klassischen-Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
