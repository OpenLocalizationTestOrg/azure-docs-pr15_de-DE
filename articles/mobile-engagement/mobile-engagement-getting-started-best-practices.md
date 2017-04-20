<properties 
    pageTitle="Azure mobilen Engagement erste Schritte mit Best Practices"
    description="Erste Schritte-Leitfaden für Azure Mobile Engagement und bewährte Methoden für onboarding" 
    services="mobile-engagement" 
    documentationCenter="mobile" 
    authors="wesmc7777"
    manager="erikre"
    editor=""/>

<tags
    ms.service="mobile-engagement"
    ms.devlang="na"
    ms.topic="get-started-article"
    ms.tgt_pltfrm="mobile-multiple"
    ms.workload="mobile" 
    ms.date="10/04/2016"
    ms.author="wesmc;ricksal"/>

# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure mobilen Engagement - erste Schritte mit Best practices

## <a name="overview"></a>(Übersicht)

**Der mobile Bildschirm ist ein sehr unübersichtlich wirken Leerzeichen:** In 2013 gefunden einer Fallstudie an, dass das durchschnittliche Mobilgerät 27 Applikationen installiert hatten. Benutzer haben in der Regel 30 Stunden pro Monat auf ihre apps. Die meisten diesmal wurde aufgewendeten Connector für soziale Netzwerke und Spielen (ungefähr 20 Stunden). Durch 2014 hatten Android Market ungefähr 1,5 Millionen von Applications für Benutzer auswählen aus. Im Apple Store enthaltenen ungefähr 1,2 Millionen apps. Mobile-app verwenden ist immer noch erhöhen, da diese Entwickler konkurrieren wachsende Markt. 

Der Mittelwert mobile Benutzer installieren und deinstallieren-apps mit hoher Häufigkeit je nach Interessen ändern und in der app auftritt. Bei der Feststellung den Erfolg einer app wird sie wichtige Informationen nicht einfach nur wie viele Benutzer die app installieren. Es ist wichtig, wissen, wie gut ist Ihre app und die Verwendung Trend geändert hat. Die folgenden Fragen werden wichtig:

- Sind Ihre Benutzer Beginn an, um Ihre app irrelevante oder veralteten finden? 
- Wie viele Benutzer nicht mehr Ihre app überhaupt verwenden? 
- Werden in der app Einkäufe nach oben oder unten Trends?
- Werden Benutzer nicht bestanden Arbeit Zahlungen aufgrund von Problemen mit der app oder fehlende relevante ausführen? 
- Könnten Sie Ihre app nützliche und relevante behalten drücken Sie damit neue Inhalte für Ihre Benutzer? 
- Möchten Sie dieses frische Inhalt für alle Benutzer übereinstimmen oder dienten Benutzersegmente in Ihrer app auf der Grundlage? 
 
Antworten auf Fragen, die etwa wie folgt konnte helfen, die Nutzungsdauer und Umsatz aus der app zu erweitern. Er hilft Ihnen definieren und Ihre Benutzer Base beibehalten. 

Medien verbundenen apps sind in der Regel einige der höchsten Aufbewahrung zwischen Benutzer haben. Ein Grund hierfür ist, dass er ständig frischen Inhalte für Benutzer zur Verfügung. Frühe Anpassung der hilfreiche Pushbenachrichtigungen umgeleitet, auf ein Benutzersegment ist normalerweise auf die app Aufbewahrung eine hohe auswirken. 

Das Programm Azure Mobile Engagement soll helfen Ihnen die Nutzungsdauer und Beibehaltung der app erweitern, indem Sie eine Methode zum Sammeln und Analysieren detaillierte Informationen zur Verwendung der app bereitgestellt. Es hilft Ihnen Ihre Benutzer gemäß Verhalten Basis klassifizieren und markierten massensendungen zu ermitteln, für die Bereitstellung von Pushbenachrichtigungen und in der app-Nachrichten auf Benutzersegmente identifizierten erstellen. Key Performance Indicators (KPIS) messen, wie Ihre Benutzer bei anderen Aspekten der app aktiv sein sollen. Azure Mobile Engagement bietet Methoden, die Sie diese KPIs zu bestimmen müssen. Sie können die Rendite für Ihre Investition (Rendite) erhöhen, indem Sie die Infrastruktur, die Sie Engagement mobile-App zu erhöhen müssen. 

Um die Azure Mobile Engagement optimal zu nutzen, müssen Sie mit einem gut gestaltete Engagement Plan zu starten. Ihr Plan helfen Ihnen, die detaillierten Daten zu identifizieren, die Sie benötigen, kann der Benutzerbasis segmentieren. Dies kann auf Verhalten basieren und in der app auftritt. Damit für den Plan erfolgreich durchgeführt werden kann ist es eine bewährte Methode, um KPIS klar zu definieren, mit denen die Ziele der app gemessen werden. Mit löschen Performance Indicators definiert können Sie die notwendigen Logik einfach Einbetten in Ihre app fein detaillierte Daten sammeln der zum Analysieren und Auswerten der KPIs verwendet werden soll. Dieses Thema enthält einen Leitfaden für bewährte Methode zum Definieren von KPIs, die mit dem Plan Engagement soll verwendet werden. 


## <a name="step-1-define-your-kpis-to-fit-the-bet-model"></a>Schritt 1: Definieren der KPIs an das Modell SUCHERGEBNIS


Definieren von KPIs ordnungsgemäß kann die Durchführung einer Aufgabe schwierig sein. Apps für verschiedene Branchen entworfen haben eigene Besonderheiten und Zielsetzungen. Dies möglicherweise zur Folge, Ihren Ansatz verwechselt werden. Um dies zu vermeiden, Zielsetzungen und KPIs drei Kategorien klassifiziert werden sollte: **Business**, **Engagement**und **technischen**. Dies ist das wir **SUCHERGEBNIS Modell**anrufen.

Ein guter Plan haben im allgemeinen Ziele mit KPIs, die der Erfolge in den folgenden Kategorien des Modells SUCHERGEBNIS messen.


#### <a name="business-kpis"></a>Business KPIs

Business KPIs sollten die einfachste Teil zu erstellen. Sie definiert wahrscheinlich bereits diese in einer bestimmten Form, wenn Sie Ihre mobile-app geplant. Diese KPIs Hilfe im Allgemeinen Measure Umsatz und Rendite für Sie app an. Die folgende Liste enthält einige Beispiel Business KPIs, die Sie während der Definition Ihrer Performance Indicators Leitfaden helfen können:

- Medien Business KPIs
    - Anzahl von Werbung geklickt haben.
    - Anzahl der Seite Zugriffe pro Benutzer
    - Anzahl der aktuellen Abonnements
- Spiele Business KPIs
    - Anzahl der innerhalb der app Einkäufe
    - Durchschnittliche Umsatz pro Benutzer (ARPU)
    - Zeit für pro Sitzung
    - Tage wiedergegebenen und aktuellen Spiel Ebene
- E-Commerce Business KPIs
    - Tage-app verwendet
    - Durchschnittliche Umsatz pro Benutzer (ARPU)
    - Durchschnittliche Betrag im Einkaufswagen bei der Kaufabwicklung
    - Für die meisten Ansichten und Einkäufe Produktkategorie
- Bank und die Versicherungsnummer Business KPIs
    - Anzahl von Konten
    - Features aktiviert
    - Angebot Seiten, die besucht haben
    - Benachrichtigungen geklickt oder aktiviert      



#### <a name="engagement-kpis"></a>Engagement KPIs

Ein KPI Engagement ist einen Performance Indicator Projektdauer Benutzer messen. In diesem Bereich Trends herausfinden der Beibehaltung der app. Hier sind ein paar Beispiel Performance Indicators für diese Art von KPIS aus:

- Aktive Benutzer in der letzten 7 Tage
- Inaktive Benutzer zählen der letzten 7 Tage
- Anzahl der Benutzer, die nicht die app in 30 Tagen verwendet haben  

Einige offensichtlichen externen Faktoren möglicherweise Indikatoren in diesem Bereich beeinflussen. Beispielsweise könnten Sie ein mobiles Gerät mit einem Benutzer zu allen Zeiten sein. Dies möglicherweise oder möglicherweise nicht erfüllt. Eine app Spiele möglicherweise meist höhere Verwendung um Feiertage aufweisen, wenn ein Spieler Weitere während nicht bei der Arbeit oder Schule möglicherweise wiedergegeben wird.   

Gut definiert helfen KPIs in dieser Kategorie messen die Beziehung zwischen der app und Ihre Kunden Ihnen.



#### <a name="technical-kpis"></a>Technische KPIs

Performance Indicators in dieser Kategorie Ihnen helfen festzustellen, wenn Ihre app ordnungsgemäß verhält, hängend oder abstürzt. Diese Indikatoren können messen die Integrität der app und Ermitteln von Nutzbarkeit Probleme, die Benutzer mithilfe der app verhindern. Für diese Kategorie gesammelten Informationen kann auch Performance-Informationen enthalten, die für die marketing-Teams. Die Daten für die Problembehandlung nach möglicherweise auch IT und Teams zum Identifizieren von Fehlern unterstützt. 
 
Hier sind einige Beispiele für technische KPIs aus:

- Informationen zur nicht verarbeitete oder behandelt Ausnahme und ' Anzahl ' 
- Zeitstempel für letzten Absturz
- Letzte Schaltfläche geklickt oder letzten Seite besucht
- Arbeitsspeicherauslastung der app
- App-Frame-rate
- OS-Version, die app ausgeführt wird, klicken Sie auf
- App-version

Definieren Sie diese KPIs um Hilfe Measure app Leistung und mögliche Fehler pinpoint. Diese Indikatoren hilfreiche Informationen, die Zeit zu reduzieren, die Sie ein Update für Ihre Kunden verfügbar ist müssen. Sie können auch dienen definieren ein Benutzersegment, wer eine bestimmte Probleme aufgetreten ist. Die Benutzer Segmentierung können zum Erstellen von massensendungen zu ermitteln, um Benachrichtigungen betreffend verfügbaren Updates und mögliche Werbung helfen Kunden zufrieden wiederherstellen zu übermitteln. 


#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Playbook Übung 1: Erstellen des KPI-Dashboards

Wenn Sie Ihre marketing-Strategie zu definieren, sollten Ihre KPIs eine Ansicht für jede Ihrer Hauptziele darstellen. Sie sollten eindeutig definierte Datenpunkte sein, die Sie zum Erfassen von wichtigen Informationen zum Überwachen der app und das Verhalten des Endbenutzers zulassen.

Erstellen eines KPI-Dashboards die enthält die folgenden Informationen

1.  Was sind die KPIs für die app?
2.  Welche Datenpunkte wird ich für jeden KPI darstellen verwenden?
3.  Wo befindet sich diese Daten für meine Anwendung (d. h. Bildschirm Einstellungen, System...)?
4.  Können eine Sequenz Engagement für diesen KPI werden wiedergegeben?

Können Sie das Arbeitsblatt **KPI-Generator** in unseren [Medien Playbook Vorlage] [ Media Playbook link] Beispiele und Anleitungen.



## <a name="step-2-your-engagement-program"></a>Schritt 2: Ihr Engagement-Programm


Ein herausragender mobilen Engagement Programm sollte eine wichtige Komponente der app berücksichtigt werden. Dies sollte absolut großartige Willkommens Programm enthalten, das für einen Benutzer in den ersten Tagen der Verwendung von app ausgeführt wird. Dies ist normalerweise sehr positive Auswirkung auf Engagement und Beibehaltung der app. Studien haben gezeigt, dass die Mehrzahl der Benutzer nicht mehr verwenden eine app den ersten Tagen nach der Installation. Bemüht, entsprechen oder Kunden Erwartung steuernde Zinsen Frühester überschreiten, während der Benutzer weiterhin auf Ihre app konzentriert werden soll. Stellen Sie sicher, dass Sie den Schlüsselwert und die Vorteile der app an Ihre Kunden präsentieren. 


![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Pushbenachrichtigungen sind die beste Methode frühen Projekten für Benutzer von mobilen Geräten. Jedoch sollte großartige sorgfältig werden beim Benutzer für Pushbenachrichtigungen segmentieren. Da, nachdem ein Benutzer ist mit der wie er erhält Spam oder irrelevante Benachrichtigungen, kann es schwerwiegende wirkt aufweisen. In wenigen Mausklicks kann ein Benutzer Ihrer Anwendung nie zurückzugebenden löschen. Der Benutzer sollten hochgradig personalisierten innerhalb der app-Wert statt generische Spam empfangen.

Nachdem Benutzer aktiv beschäftigt sind, kann das Programm Engagement andere Aspekte der app drive helfen.

Beispielsweise könnten Sie eine für eine Marketingkampagne einrichten, die Ihre aktive Benutzer so bewerten Sie Ihre app anfordert. Da diese Benutzersegment am aktivsten sind und die meisten Erfahrung mit Ihnen app, erwarten Sie, um die genauesten Bewertung zu verleihen. Nachdem Sie eine hohe app Bewertung haben, können sie von der organisch Herunterladen der app verringern sowie auf Ihrer neuen Verbesserung Anschaffungskosten voranzutreiben.



#### <a name="engagement-sequence"></a>Engagement Sequenz


Globale Engagement Programm enthält verschiedene Engagement folgen. Jede Sequenz soll mehrere Ziele erreicht haben.


###### <a name="life-push-sequence"></a>Nutzungsdauer Pushbenachrichtigungen Sequenz


Die Ziele für eine Nutzungsdauer Pushbenachrichtigungen Sequenz unterscheiden sich je nach den Lebenszyklus eines Auftrags für des Benutzers mit der app. Ein bestimmter Benutzer möglicherweise neue, inaktive oder sehr aktiv. Bei anderen Phasen eines Projekts Lebenszyklus möglicherweise Benutzer Ihre frisch Inhalte in Form von Tipps oder Links in der Dokumentation nutzen. 

Beispielsweise benötigen einen neuen Benutzer erste Orientierung in einer app-Hilfe oder ein neuer Benutzer Incentive ähnlich wie der folgende nutzbringend beim ersten sie die app starten...

*"Gerne integrierte stehen Ihnen! Denken Sie daran, anmelden, um Ihre 1st Monat kostenlos erhalten!"*


###### <a name="behavioral-push-sequence"></a>Sequenz Verhalten Pushbenachrichtigungen

Die Verhalten Pushbenachrichtigungen Sequenz soll basierend auf Benutzerverhalten für die app erfassten Verwendung zu vergrößern.  

Angenommen, nutzbringend ein sehr aktiver Benutzer einer Fantasy Football App mit der Pushbenachrichtigung von folgenden beschäftigt...

*"Johann Sie einen schwerwiegenden Football Lüfter sind! Melden Sie sich bei unseren NFL Abschnitt und gewonnen Sie kostenlosen Zugriff auf die SuperBowl!"*


###### <a name="alerting-push-sequence"></a>Warnung Abfolge von Pushbenachrichtigungen

Benutzer werden relevante Informationen ihren Interessen dienten schätzen. Eine Benachrichtigung Pushbenachrichtigungen Sequenz verbessert Engagement per Benachrichtigungen Interessen ausgehend, dass ein Benutzer klar worden ist. Dies kann explizit sein, wenn ein Benutzer eigene Interessen in der app auswählt. Es kann auch implizit basierend auf Daten, die bei der Interaktion mit dem Benutzer mit der app gesammelten bestimmt werden.

Beispielsweise möglicherweise der Benutzer, der eine app E-Commerce regelmäßig eine bestimmte Marke Kaffee kaufen, die Sie mit einer Business KPI festgehalten haben. Die folgende Benachrichtigung kann dieses Benutzers Engagement mit der app verbessern.
 
*"Hallo Wes, eine der Ihrer bevorzugten Marken Kaffee werden auf Verkauf 25 % Rabatt auf die erste Woche des September 2015. Vielen Dank, dass Sie als Kunden und wollten, stellen Sie sicher, dass Sie das wussten."*

###### <a name="rentention-push-sequence"></a>Rentention Pushbenachrichtigungen Sequenz

Diese Sequenz soll Benutzer verwenden eine sich wiederholende Pushbenachrichtigungen Benachrichtigung massensendungen zu ermitteln, um voranzutreiben reguläre Gewohnheit ansprechenden mit der app beibehalten. Damit können Sie app Aufbewahrung erhöhen, wenn der Anwender Interaktionen erhält. 

Der Benutzer einer verknüpften Sports-App möglicherweise beispielsweise die folgenden Pushbenachrichtigung wöchentlich auf Grundlage des Benutzers bevorzugten Teams erhalten:

*"Für die Chance, zu gewinnen 200 Punkt, go Stimme ab, ob die New York Hertha diese Woche gegen Hamburg Blau Jays deren Spiel gewonnen!"*


#### <a name="the-3w-approach"></a>Der Ansatz 3 w

Die verschiedenen Pushbenachrichtigungen folgen Mastering hilft Ihnen mit Endbenutzer populärer. Jedoch müssen Sie weiterhin das 3 w Verfahren zum Personalisieren Ihrer Benachrichtigungen verwenden. Der Ansatz 3 w sollte zu beheben, wer, wann und wie für jede Benachrichtigung. Wenn Sie diese drei Fragen klar erfüllen sollten Sie Benachrichtigungen für Engagement ordnungsgemäß konzentrieren.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)



###### <a name="who-the-user-segment-that-will-receive-messages"></a>Wer: Der Benutzer segmentieren, die Nachrichten erhalten

Drücken Benachrichtigungen für Ihre Benutzer muss einen sehr vertrauliche Kommunikationskanal berücksichtigt werden. Stellen Sie sicher, dass die Benachrichtigungen, die Sie senden auf ein Benutzersegment Ziel auch den Interessen der dieses Benutzersegment ausgelegte sind. Eine falsch weitergeleitete Benachrichtigung ist sehr wahrscheinlich eine negative Auswirkung eines Benutzers haben. Sie können dies zu Ihrer Anwendung deinstalliert führenden Spam erachten. 

Verwenden Sie eine Kombination von bestimmter Kriterien für technische und Verhalten, wenn Benutzer Segmenten zu definieren, die Benachrichtigungen erhalten werden. Ein einfaches Beispiel definieren ein Benutzersegment könnte ähnlich wie die folgende Anweisung aus:

"Alle Benutzer, die gestartet wird die eine mobile Anwendung für die erste Uhrzeit 3 Tage zurück, und die Anmeldeseite zweimal, ohne tatsächlich Abschließen einer Anmeldung besucht haben".
 
Diese Anweisung können Sie die Daten zu identifizieren, die Sie um Unterstützung für ein bestimmtes Szenario sammeln müssen würden.


###### <a name="what-the-message-that-you-will-send"></a>Was: Die Nachricht, die Sie senden

**Farbton**

Verwenden Sie in Ihrer Projekte einen Ton aus, die für geeignet ist Ihre für Ihre Benutzer segmentierter. Dies ist auf jeden Fall eine gute Möglichkeit zum Verbinden mit Ihrer Endbenutzer und Höherstufen eines Benutzers Zinsen in Ihrer app. 

**Umleitung**

Einer der Pushbenachrichtigung kann für mehr als die Anwendung öffnen verwendet werden. Wenn Sie die Benachrichtigung einen Kontext beispielsweise übertragenen Informationen oder eine Werbeaktion für Serverprodukte, diese Benachrichtigung bietet möglicherweise Tiefe Link direkt auf die richtigen Inhalte in der Anwendung. Um dies zu unterstützen, müssen Sie eine URL-Schema zu lassen Sie die Anwendung, die die Umleitung verwalten erstellen. Wenn Ihre Engagement folgen arbeiten, ist dies ein wichtiger Schritt, der nicht vergessen werden muss.

Umleitung kann auch für andere Systeme verwaltet werden. Mit einer URL-Aktion ist es beispielsweise möglich, Endbenutzer in vielen anderen Systemen, einschließlich der folgenden umgeleitet:

- Eine website
- Ein Postfach mit bereits Einrichten von e-Mail
- Ein SMS-Feld
- Ein DFÜ-Dienst
- Speichern Sie direkt mit der Anwendung zur Bewertung der Anwendungs. 

Auf diese Weise viele Verkaufschancen populärer Endbenutzer und Regeln für automatische zur Verbesserung der aufführungen erstellen.


**Format/Inhalt**

Verschiedene Typen und Pushbenachrichtigungen Benachrichtigung Formate:

1. **Ankündigungen** : ermöglicht es Ihnen, Werbung Nachrichten an Benutzer gesendet werden, bei anderen Minuten (außerhalb des in der app-app oder einem beliebigen Zeitpunkt).
2. **Umfragen** : Sie Informationen aus den Endbenutzer sammeln, indem sie Fragen aktiviert. Diese Antworten sind dann verfügbar, wenn Kriterien für den Endbenutzer Ziel erstellen.
3. **Legt Daten** : ermöglicht es Ihnen, eine binäre oder base64 Datendatei aktualisieren die app zu senden. Die Informationen in einer Pushbenachrichtigungen Daten enthalten sind, wird an Ihrer Anwendung an die Benutzer in Ihrer app personalisieren gesendet. Die Anwendung muss zur Unterstützung der Daten in einer Daten Pushbenachrichtigungen entworfen werden.
4. **Kacheln (nur für Windows Phone)** : ermöglichte von Microsoft Pushbenachrichtigungen Benachrichtigung Service (MPNS) verwenden Sie zum Senden einer systemeigenen Pushbenachrichtigungen Benachrichtigung mit XML-Daten (unterstützte seit SDK Version 0.9.0. Der endgültige Inhalt für Kacheln darf 32 KB nicht überschreiten.). Die Meldung, die direkt auf der Karte auf der Kachel angezeigt wird.
5. **WebView** : eine Webansicht ist ein Popupfenster mit Webinhalt. Diesem Popupfenster angezeigt wird, wenn der Endbenutzer auf der Pushbenachrichtigung geklickt hat. Eine Webansicht können Sie weitere Interaktion mit den Endbenutzer haben.
 
>[AZURE.NOTE] Stellen Sie sicher, dass Inhalte, die Sie als Pushbenachrichtigungen Senden der jeweiligen Plattform (iOS, Android, Windows) Richtlinien für die Entwicklung von apps und Senden von Pushbenachrichtigungen entspricht.

 


###### <a name="when-the-timing-of-your-campaign"></a>Wann: Die Anzeigedauer Ihrer für eine Marketingkampagne

Wann ist der beste Zeitpunkt zum Aktivieren einer Campaign Pushbenachrichtigungen auslösen? Sollten sie manuell oder automatisch? Sollte es wiederkehrt? Bestimmen der richtigen Zeitpunkt oder der Häufigkeit ist entscheidend für Benutzer mit optimales Ergebnis populärer. Für jede Sequenz Engagement und Szenario, müssen Sie angeben, wann kann ich die optimale Zeit für Pushbenachrichtigungen zu senden. Es folgen einige Beispiele möglich:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Wenn Sie viele Benachrichtigungen täglich senden möchten, müssen Sie die erforderlichen nachdenken, dass die Benutzer Ihre Kommunikation als Spam wahrnehmen können. 

Azure Mobile Engagement bietet zwei Methoden, wie Sie Ihre Kommunikation wird als Spam angesehen zu vermeiden. Verwenden Sie detailliert Segmentierung zuerst, um sicherzustellen, dass Sie nicht die gleiche Zielgruppe. Darüber hinaus bietet Azure Mobile Engagement ein Kontingentfeature "". Dieses Feature kann Benachrichtigungen für eine für eine Marketingkampagne gesendet werden. Beispielsweise wird ein Kontingent 5 pro Woche Einstellung sicherstellen, dass einen Benutzer als Teil der für eine Marketingkampagne Benutzersegment nicht mehr als 5 Benachrichtigungen für diese Woche empfangen werden, enthalten.





#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Playbook Übung 2: Erstellen des Engagement-Programms

Einige Zeit Zusammenfassen von Ihren Zielen und die massensendungen zu ermitteln, der für die Wiedergabe mit bestimmten folgen erwartet definieren. Stellen Sie sicher, dass Sie den 3 w Ansatz, die Benachrichtigungen in Ihre anwenden. 

Verwenden Sie das **Programm Engagement** Arbeitsblatt in die [Medien Playbook Vorlage] [ Media Playbook link] Beispiele und Anleitungen.


## <a name="step-3-app-integration"></a>Schritt 3: App-Integration


#### <a name="create-a-tag-plan"></a>Erstellen Sie einen Plan für die Kategorie

Um Azure Mobile Engagement in Ihre app integrieren müssen Sie einen Plan für die Kategorie zu erstellen. Der Kategorie-Plan ist der Grundsteine des Projekts. Die Beziehung zwischen marketing Spezifikationen, den Workflow der Anwendung, und die in der app KPIs messen erfassten Daten werden real Kategorie definiert. Er gibt an, welche Analytics im Portal angezeigt werden kann. Außerdem können Sie die Benutzersegmente definieren und die markierten Pushbenachrichtigungen zu Ihrer Endbenutzer populärer zu senden. Einmal müssen Sie den Tag Plan definiert, hinzufügen, dass der Code es in Ihre app integrieren einfache mit dem Azure Mobile Engagement SDK ist.

Ein Plan für die Kategorie sollte nicht alles in einer Anwendung kategorisieren. Sie sollten nur Kategorie Daten enthalten, die Bestandteil Ihrer Strategie mobilen Engagement ist. Dies wird wahrscheinlich zwischen Clientanwendungen verschiedener sein. Die [Vorlage für Medien Playbook] [ Media Playbook link] vorausgesetzt, indem Azure Mobile Engagement hilft einen Tag Plan mit einer bestimmten Methode erstellen. Verwenden Sie das Arbeitsblatt **Kategorie Plan** als ein Leitfaden zum Erstellen Ihres Plans Kategorie ein.

Wenn Sie einen Abschnitt Kategorie auf dem Arbeitsblatt zu definieren, müssen Sie spezieller an. Dies ist sehr wichtig, um Verwirrung zu vermeiden. Details jedes erwartet Szenario, in dem jede Kategorie gesendet wird. Zählen der Name der Aktivität, in dem jede Kategorie eingebettet ist. Dies sollten alle im **Informative** Teil des Arbeitsblatts aufgenommen werden. Das Kategorie Plan Arbeitsblatt sollten Hauptfenster Bezug zur Überprüfung testen. 

Im Abschnitt **zum Sammeln von Daten** sollte Ihr Entwicklungsteam finden Sie die Typen, Namen, Werte und zusätzliche Informationen Schlüssel/Wert-Paare, die erforderlich für jede Kategorie, die in der Anwendung eingebettet werden.

Es empfiehlt sich, überprüfen den Tag Plan mit allen Teams mit dem Projekt verbundenen. Nehmen Sie die notwendigen Korrekturen und bestätigen Sie, dass alles für Marketing und Entwicklung Teams klar ist.

Das Arbeitsblatt **Leistungsumfang** kann steuern helfen, die allen beteiligten Personen im Projekt verwendet werden.


#### <a name="data-types"></a>Datentypen

Dies sind gängige Typen von Datensupport von Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Geräte und Benutzer

Azure Mobile Engagement identifiziert Benutzer durch einen eindeutigen Bezeichner für jedes Gerät generieren. Dieser Bezeichner heißt das Gerätebezeichner (oder die Geräte-ID). Es wird in einer Weise generiert, dass alle Programme auf dem gleichen Gerät die gleichen Geräte-ID freigeben.

###### <a name="sessions-and-activities"></a>Sitzungen und Aktivitäten

Eine Sitzung ist eine Instanz der app, die von einem Benutzer ausgeführt wird. Die Sitzung umfasst ab dem Zeitpunkt der Benutzer die app gestartet wird, bis es nicht mehr.

Eine Aktivität ist eine logische Gruppierung einer Reihe von Aktionen, die während einer Sitzung für die app kann möglicherweise. Es ist in der Regel einen bestimmten Bildschirm in der app, aber es kann sein, dass nichts durch die Logik der Anwendung definiert. Zumindest sollten Sie jede Bildschirm oder Aktivität für Ihre app kategorisieren. Dies ermöglicht Ihnen, den Benutzer-Pfad zu verstehen.


###### <a name="events"></a>Ereignisse

Ereignisse werden verwendet, um die Interaktion mit dem Benutzer mit der app zu melden. Sie können die Sofortsuche Aktionen, wie die gemeinsame Nutzung von Inhalten oder Starten eines Videos sein. Kategorisieren von Ereignissen stellt Ihnen Daten Websitesammlungen zur Verfügung, die zeigen, wie Benutzer die app interagieren. 

###### <a name="jobs"></a>Aufträge

Aufträge werden verwendet, um die Aktionen zu Berichten, die eine Dauer aufweisen. Einige Beispiele möchten:

- Ausführung von API-Abfragen
- Zeitpunkt der Anzeige von anzeigen
- Hintergrund Aufgaben Dauer 
- Language Pack für-Prozess Dauer
- Anzeigen eines Videos


###### <a name="errors"></a>Fehler

Fehler werden verwendet, um die Probleme, die von der app erkannt zu informieren. Beispielsweise falsche Benutzeraktionen oder Fehler beim Aufrufen eines API.

###### <a name="application-information"></a>Informationen zur Anwendung

Anwendungsinformationen (App-Info) Dient zum Kategorisieren von Daten im Zusammenhang mit eines Benutzers Erfahrung mit einer Anwendung. Es wird durch die Interaktion mit der Anwendung eines Benutzers ausgelöst. 

Bei einem Schlüssel angegebenen app-Informationen werden von nachverfolgt Azure Mobile Engagement nur dem letzten Wert (keine History). App-Informationen werden den Status Ihrer app oder die Endbenutzer. Beispielsweise den Status Log in oder der Gruppe eines Benutzers bevorzugten Produkt.

###### <a name="crash-data"></a>Von Absturzdaten

Stürzt ab automatisch von gesammelten Daten werden die Mobile Engagement SDK Berichte Anwendungsfehler nicht von der Anwendung behandelt. Beispiel: Ausnahmefehler, die eintritt.


###### <a name="extra-data"></a>Zusätzliche Daten

Mit den Parametern können Ereignisse, Fehler, Aktivitäten und Projekte erweitert werden. Dies ist eine zusätzliche Informationen, die ein Entwickler als bestimmte Daten aus der Anwendung vorsehen. Dies ist wichtig für abgestimmte Segmentierung definieren. 

Beispielsweise können der Wert eines Tags "Artikel" Sie zum Segment Endbenutzer basierend auf, die den jeweiligen Gegenstand angezeigt. Die möglicherweise jedoch nicht ausreichend sein. Möglicherweise ist es besser, wenn die gleiche "Artikel" Kategorie auch zusätzliche-Informationen, wie etwa "News_category" in einer Aktivität enthalten. Dies würde Dynamisches Festlegen von bevorzugten Kategorien für den Benutzer hilfreich sein. 

Zusätzliche Informationen wird als Schlüssel/Wert-Paar gemeldet. Im Beispiel für diese Anwendung Medien wäre zusätzliche Informationen für "News_category" den Wert für die Kategorie. Beispielsweise "Sports", "Wirtschaft" oder "Politik".





#### <a name="tag-and-sdk-integration"></a>Kategorie und SDK-integration 

Führen Sie Schritt-für-Schritt-Anweisungen für die Azure Mobile Engagement SDK in Ihre app zu integrieren der [Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) -Dokumentation auf Azure-Website ein. Wählen Sie Ihre Zielplattform über die Links am oberen Rand der Seite aus.

Es empfiehlt sich beim Erstellen von Projekten für zwei apps auf Azure Mobile Engagement erstellt. Eine für die Entwicklung und Test Staging und anderen für die Herstellung Staging. Ihr IT-Team kann dann von Test Staging zu Herstellung heraufstufen, wenn das Testen der Benutzerakzeptanz erfolgreich ist.



#### <a name="user-acceptance-testing-uat"></a>Benutzerakzeptanz testen (UAT)

Testen der Benutzerakzeptanz (UAT) umfasst, und stellen Sie sicher, dass alles ordnungsgemäß funktioniert. Zahlungen Arbeit abgeschlossen werden können und alle erforderliche Daten, die auf Grundlage Ihres Plans Kategorie sammeln:
 
- Kategorisieren von Informationen sollten an Ort gemäß dokumentierten AZME Konzepte
- Alle erforderlichen Informationen werden gesammelt (einschließlich zusätzliche Informationen Wert App Info-Wert)
- Nomenklatur entspricht nach Kategorie planen Liquiditätskonten
- Es gibt keine doppelten Tags gesendet werden

Erwägen Sie alle Arten von Verhalten im Infobereich, die Sie in Ihrer app eingebettet haben

- Abmelden bei der app und in der app legt Ankündigungen, Umfragen, Daten ab.
- Text/Web-Ansichten
- Badge aktualisieren, Kategorien



#### <a name="setup"></a>Setup

Einrichten von Azure Mobile Engagement ist sehr einfach. Gesamte Dokumentation im Zusammenhang mit der Benutzeroberfläche steht auf der Website Azure Mobile Engagement, [wie Sie in der Benutzeroberfläche Navigieren](mobile-engagement-user-interface-home.md).

Es wird empfohlen, dass Sie starten, indem Sie die richtigen Rollen und Mitglied von Rollen für die Benutzer Ihres Projekts einrichten. Auf diese Weise können Sie die richtige Zugriff auf die Plattform für alle Benutzer verwalten. Ihre Rollen können umfassen:

- Administratoren
- Entwickler
- ' Anzeigende Benutzer ' 

Danach:
- Registrieren Sie sich Ihre Geräte-ID auf Ihrer eigenen Gerät testen.
- Wechseln Sie zu den Einstellungen Ihres Kontos, und richten Sie die gewünschte Zeitzone Diagramme und Benachrichtigung Übermittlungszeitpunkt für Ihre Zeitzone festgelegt haben.
- Wechseln Sie zu den Einstellungen der Anwendung, und registrieren Sie "App-Informationen" Ziel Endbenutzer ist benötigten.

Überprüfen Sie weitere Informationen zum Ausführen Ihrer ersten Pushbenachrichtigungen Benachrichtigung für eine Marketingkampagne [verwenden und Verwalten von Push-Vorgänge für Ihre Endbenutzer erreichen Schritte](mobile-engagement-how-tos.md)aus.



## <a name="conclusion"></a>Abschluss


Engagement Programme sind iterative und sollten Sie kontinuierlich verbessern an, wie Sie ausprobieren, was für Ihre app am besten geeignet. 

Zunächst, bei der Entwicklung von Erfahrung mit Engagement Strategien nicht versuchen, eine Strategie für die gesamte globale Engagement zu erstellen. Machen Sie einen Schritt-für-Schritt-Ansatz Identifizieren Ihrer KPIs und wie sie genutzt. Engagement Strategie wird für jedes app eindeutig sein.

Nachdem Sie einige Erfahrung entwickelt haben sollten Sie Folgendes für Ihre Programme Engagement hinzufügen:

- Verlauf: Erfassen von Benutzern und Sie wahrscheinlich Datensammlung Datenquellen definieren. Azure mobilen Engagement kann mit Datensammlung Datenquellen verknüpft werden. Sie können Sie aufführungen jeder Quelle zu überwachen. Diese Informationen werden zu Ihrer Investition Acquisition maximieren interessant sein. 

- A / B testen: Dies ist ein wesentlicher Teil des Engagement-Programm. Jede app verfügt über eine eigene Besonderheiten. Mit A / B testen, können Sie Ihr Programm Engagement verbessern.

- Geo-Standort: Dies ist eine große Chance für Marken. Dank dieses Features können Sie am richtigen Ort und Zeit erreicht haben. Es empfiehlt sich, dass Sie genügend Endbenutzer Verhaltensdaten gesammelt haben, bevor Sie beginnen mit geografischen Position Überprüfung.

- Pushbenachrichtigungen Daten: Daten Pushbenachrichtigungen ist eine unsichtbare Pushbenachrichtigungen. Daten Pushbenachrichtigungen ermöglicht das Anpassen Ihrer Anwendungs basierend auf Endbenutzerverhalten. Angenommen, wenn ein Benutzersegment häufig technischen Produkte berät, kann der app-Besitzer einer Pushbenachrichtigungen Daten senden, ihre Homepage mit technischen Inhalten personalisieren wird.



## <a name="next-steps"></a>Nächste Schritte

- [Erstellen eines Kontos Azure Mobile Engagement](mobile-engagement-create.md).
- Besuchen Sie [definieren strategische Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) Weitere Informationen zum Definieren von strategische Mobile Engagement aus.



  

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
