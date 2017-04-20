<properties 
    pageTitle="Stream Analytics: Drehen von Anmeldeinformationen für Eingaben und Ausgaben | Microsoft Azure" 
    description="Erfahren Sie, wie die Anmeldeinformationen für Stream Analytics Eingaben und Ausgaben zu aktualisieren."
    keywords="Anmeldeinformationen"
    services="stream-analytics" 
    documentationCenter="" 
    authors="jeffstokes72" 
    manager="jhubbard" 
    editor="cgronlun"/>

<tags 
    ms.service="stream-analytics" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="data-services" 
    ms.date="09/26/2016" 
    ms.author="jeffstok"/>

#<a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Drehen von Anmeldeinformationen für Eingaben und Ausgaben in Stream Analytics Aufträge

##<a name="abstract"></a>Abstrakte
Azure Stream Analytics gestattet keine heute die Anmeldeinformationen auf einer Ausgang ersetzen, während der Auftrag ausgeführt wird.

Zwar Azure Stream Analytics Fortsetzen eines Auftrags aus der letzten Ausgabe unterstützt, wollten wir den gesamten Prozess für die Verzögerung zwischen die Beendigung minimieren und Starten des Projekts und drehen die Anmeldeberechtigungen freigeben.

##<a name="part-1---prepare-the-new-set-of-credentials"></a>Teil 1: Vorbereiten den neuen Satz von Anmeldeinformationen:
In diesem Abschnitt gilt für die folgenden Eingaben/Ausgaben zur Verfügung:

* BLOB-Speicher
* Ereignis Hubs
* SQL-Datenbank
* Table Storage

Für andere Eingaben/Ausgaben fahren Sie mit Teil 2 fort.

###<a name="blob-storagetable-storage"></a>BLOB-Speicher/Tabellenspeicher
1.  Wechseln Sie zu der Erweiterung Speicher Azure Verwaltungsportal:  
![graphic1][graphic1]
2.  Suchen Sie die Speicherung von Ihrem Projekt verwendeten und darin wechseln:  
![graphic2][graphic2]
3.  Klicken Sie auf den Befehl Zugriffstasten verwalten:  
![graphic3][graphic3]
4.  Zwischen den Primärschlüssel Access und die sekundäre Zugriffstaste, **Wählen Sie das Schema nicht verwendet werden, indem Sie Ihre Arbeit**.
5.  Drücken Sie Regenerieren:  
![graphic4][graphic4]
6.  Kopieren des neu generierten Schlüssels an:  
![graphic5][graphic5]
7.  Fahren Sie mit Teil 2 fort.

###<a name="event-hubs"></a>Ereignis hubs
1.  Wechseln Sie zu der Erweiterung Dienstbus Azure Verwaltungsportal:  
![graphic6][graphic6]
2.  Suchen Sie den Dienst Bus Namespace verwendet, indem Sie Ihre Arbeit und darin wechseln:  
![graphic7][graphic7]
3.  Wenn Ihre Arbeit eine freigegebenen Zugriffsrichtlinie auf den Dienst Bus Namespace verwendet, springen Sie mit Schritt 6  
4.  Wechseln Sie zur Registerkarte Ereignis Hubs:  
![graphic8][graphic8]
5.  Suchen Sie nach dem Ereignis Hub verwendet, indem Sie Ihre Arbeit und darin wechseln:  
![graphic9][graphic9]
6.  Wechseln Sie zur Registerkarte konfigurieren:  
![graphic10][graphic10]
7.  Klicken Sie auf den Namen der Richtlinie Dropdown-Pfeil suchen Sie nach der freigegebenen Zugriffsrichtlinie durch Ihre Arbeit verwendet:  
![graphic11][graphic11]
8.  Zwischen den Primärschlüssel und die sekundäre Taste, **Wählen Sie das Schema nicht verwendet werden, indem Sie Ihre Arbeit**.  
9.  Drücken Sie Regenerieren:  
![graphic12][graphic12]
10. Kopieren Sie die Taste neu generierte an:  
![graphic13][graphic13]
11. Fahren Sie mit Teil 2 fort.  

###<a name="sql-database"></a>SQL-Datenbank

>[AZURE.NOTE] Hinweis: Sie müssen die Verbindung zum Dienst SQL-Datenbank. Wir werden wie folgt mithilfe der Verwaltungsoption auf Azure Verwaltungsportal anzeigen, aber Sie auch einige clientseitige Tool wie SQL Server Management Studio ebenfalls verwenden.

1.  Wechseln Sie zu der SQL-Datenbanken Erweiterung Azure Verwaltungsportal:  
![graphic14][graphic14]
2.  Suchen Sie nach der SQL-Datenbank verwendet werden, indem Sie Ihr Projekt, und **Klicken Sie auf dem Server auf** Link in derselben Zeile:  
![graphic15][graphic15]
3.  Klicken Sie auf den Befehl verwalten:  
![graphic16][graphic16]
4.  Typ Datenbank Master:  
![graphic17][graphic17]
5.  Geben Sie Ihren Benutzernamen, Ihr Kennwort ein, und klicken Sie auf Anmelden:  
![graphic18][graphic18]
6.  Klicken Sie auf neue Abfrage:  
![graphic19][graphic19]
7.  Geben Sie die folgende Abfrage ersetzen < Login_name > mit Ihrem Benutzernamen und Ersetzen von <enterStrongPasswordHere> mit dem neuen Kennwort:  
`CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8.  Klicken Sie auf ausführen:  
![graphic20][graphic20]
9.  Kehren Sie zu Schritt 2 und dieses Mal auf die Datenbank:  
![graphic21][graphic21]
10. Klicken Sie auf den Befehl verwalten:  
![graphic22][graphic22]
11. Geben Sie Ihren Benutzernamen, Ihr Kennwort ein, und klicken Sie auf Anmeldung:  
![graphic23][graphic23]
12. Klicken Sie auf neue Abfrage:  
![graphic24][graphic24]
13. Geben Sie in der folgenden Abfrage ersetzen < Benutzername > mit einem Namen, um diese Anmeldung im Zusammenhang mit dieser Datenbank zu identifizieren (Sie können den gleichen Wert, den Sie für < Login_name >, beispielsweise gegeben hat bereitstellen) werden soll, und ersetzen < Login_name > mit Ihren neuen Benutzernamen ein:  
`CREATE USER <user_name> FROM LOGIN <login_name>`
14. Klicken Sie auf ausführen:  
![graphic25][graphic25]
15. Geben Ihre neuen Benutzer jetzt, mit den gleichen Rollen und Berechtigungen, die Ihre ursprüngliche Benutzer hatte.
16. Fahren Sie mit Teil 2 fort.

##<a name="part-2-stopping-the-stream-analytics-job"></a>Teil 2: Der Stream-Analytics-Auftrag gestoppt wird.
1.  Wechseln Sie zu der Erweiterung Stream Analytics Azure Verwaltungsportal:  
![graphic26][graphic26]
2.  Suchen Sie nach der Position und darin navigieren:  
![graphic27][graphic27]
3.  Wechseln Sie zu der Registerkarte Eingaben oder die Ausgaben basierend auf, ob Sie die Anmeldeinformationen auf eine Eingabe oder auf eine Ausgabe drehen sind.  
![graphic28][graphic28]
4.  Klicken Sie auf den Befehl zum Beenden und bestätigen Sie, dass der Auftrag beendet wurde:  
![graphic29][graphic29] warten, bis das Projekt zu beenden.
5.  Suchen Sie die ein-/Ausgabe, die Sie Anmeldeinformationen auf Drehen und darin navigieren möchten:  
![graphic30][graphic30]
6.  Fahren Sie mit Teil 3.

##<a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a>Teil 3: Bearbeiten die Anmeldeinformationen für das Stream Analytics-Projekt

###<a name="blob-storagetable-storage"></a>BLOB-Speicher/Tabellenspeicher
1.  Suchen Sie das Feld Kontoschlüssel Speicher, und fügen Sie den neu generierten Key ein:  
![graphic31][graphic31]
2.  Klicken Sie auf den Befehl speichern, und bestätigen Sie Ihre Änderungen zu speichern:  
![graphic32][graphic32]
3.  Ein Verbindungstest wird beim Speichern der Änderungen automatisch gestartet wird, vergewissern Sie sich abgelaufen ist.
4.  Fahren Sie mit Teil 4 fort.

###<a name="event-hubs"></a>Ereignis hubs
1.  Suchen nach dem Feld Ereignis Hub Richtlinie-Taste, und fügen Sie den neu generierten Key ein:  
![graphic33][graphic33]
2.  Klicken Sie auf den Befehl speichern, und bestätigen Sie Ihre Änderungen zu speichern:  
![graphic34][graphic34]
3.  Ein Verbindungstest beginnt automatisch beim Speichern der Änderungen, stellen Sie sicher, dass es erfolgreich bestanden hat.
4.  Fahren Sie mit Teil 4 fort.

###<a name="power-bi"></a>Power BI
1.  Klicken Sie auf die Autorisierung erneuern:  
* ![graphic35][graphic35]
* Die folgende Bestätigung wird angezeigt:  
* ![graphic36][graphic36]
2.  Klicken Sie auf den Befehl speichern, und bestätigen Sie Ihre Änderungen zu speichern:  
![graphic37][graphic37]
3.  Ein Verbindungstest wird automatisch gestartet, wenn Sie die Änderungen zu speichern, stellen Sie sicher, dass es war erfolgreich.
4.  Fahren Sie mit Teil 4 fort.

###<a name="sql-database"></a>SQL-Datenbank
1.  Suchen Sie die Felder Benutzername und Kennwort, und fügen sie den neu erstellten Satz Anmeldeinformationen:  
![graphic38][graphic38]
2.  Klicken Sie auf den Befehl speichern, und bestätigen Sie Ihre Änderungen zu speichern:  
![graphic39][graphic39]
3.  Ein Verbindungstest beginnt automatisch beim Speichern der Änderungen, stellen Sie sicher, dass es erfolgreich bestanden hat.  
4.  Fahren Sie mit Teil 4 fort.

##<a name="part-4-starting-your-job-from-last-stopped-time"></a>Teil 4: Starten des letzten beendet Verwendung
1.  Navigieren Sie nicht die ein-/Ausgabe an:  
![graphic40][graphic40]
2.  Klicken Sie auf den Befehl starten:  
![graphic41][graphic41]
3.  Wählen Sie aus dem letzten beendet, und klicken Sie auf OK:  
 ![graphic42][graphic42]
4.  Fahren Sie mit Teil 5.  

##<a name="part-5-removing-the-old-set-of-credentials"></a>Teil 5: Entfernen den alten Satz von Anmeldeinformationen
In diesem Abschnitt gilt für die folgenden Eingaben/Ausgaben zur Verfügung:
* BLOB-Speicher
* Ereignis Hubs
* SQL-Datenbank
* Table Storage

###<a name="blob-storagetable-storage"></a>BLOB-Speicher/Tabellenspeicher
Wiederholen Sie für die Tastenkombination, die zuvor von Ihrem Auftrag verwendet wurde, die jetzt nicht verwendete Zugriffstaste erneuern Teil 1 ein.

###<a name="event-hubs"></a>Ereignis hubs
Wiederholen Sie die Teil 1 für die Taste, die zuvor von Ihrem Auftrag verwendet wurde, den jetzt nicht verwendeten Schlüssel erneuern.

###<a name="sql-database"></a>SQL-Datenbank
1.  Kehren Sie zum Abfragefenster aus Teil 1 Schritt 7, und geben Sie die folgende Abfrage ersetzen < Previous_login_name > mit den Benutzernamen, die zuvor von Ihrem Auftrag verwendet wurde:  
`DROP LOGIN <previous_login_name>`  
2.  Klicken Sie auf ausführen:  
    ![graphic43][graphic43]  

Sie sollten die folgende Bestätigung erhalten: 

    Command(s) completed successfully.

## <a name="get-help"></a>Hilfe erhalten
Weitere Unterstützung benötigen versuchen Sie es unsere [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Nächste Schritte

- [Einführung in Azure Stream Analytics](stream-analytics-introduction.md)
- [Erste Schritte mit Azure Stream Analytics](stream-analytics-get-started.md)
- [Skalieren Sie Azure Stream Analytics Aufträge](stream-analytics-scale-jobs.md)
- [Azure Stream Analytics Query Language Bezug](https://msdn.microsoft.com/library/azure/dn834998.aspx)
- [Azure Stream Analytics Management REST-API-Referenz](https://msdn.microsoft.com/library/azure/dn835031.aspx)


[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png
 
