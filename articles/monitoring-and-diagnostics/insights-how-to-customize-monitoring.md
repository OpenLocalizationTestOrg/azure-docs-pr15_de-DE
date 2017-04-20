<properties
    pageTitle="Übersicht über die Kriterien in Microsoft Azure | Microsoft Azure"
    description="Erfahren Sie, wie Überwachung Diagramme in Azure anpassen."
    authors="rboucher"
    manager="carolz"
    editor=""
    services="monitoring-and-diagnostics"
    documentationCenter="monitoring-and-diagnostics"/>

<tags
    ms.service="monitoring-and-diagnostics"
    ms.workload="na"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/08/2015"
    ms.author="robb"/>

# <a name="overview-of-metrics-in-microsoft-azure"></a>Übersicht über die Kriterien in Microsoft Azure

Alle Azure Dienste Nachverfolgen von wichtigen Kriterien, mit die Sie Status, Leistung, Verfügbarkeit und Verwendung Ihrer Dienste überwachen können. Sie können diese Kennzahlen Azure-Portal anzeigen, und können Sie auch die [REST-API](https://msdn.microsoft.com/library/azure/dn931930.aspx) oder [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) sämtlicher Kennzahlen programmgesteuert Zugriff auf.

Für einige Dienste müssen Sie möglicherweise Diagnose aktivieren, um alle Kennzahlen finden Sie unter. Für andere Personen, z. B. virtuellen Computern erhalten Sie eine grundlegende Reihe von Kennzahlen, aber muss so aktivieren Sie die vollständige festlegen häufig auftretenden Kennzahlen. Finden Sie weitere Informationen [für die Überwachung und Diagnose aktivieren](insights-how-to-use-diagnostics.md) aus.

## <a name="using-monitoring-charts"></a>Verwenden von Diagrammen Überwachung

Sie können keines der Metrik Diagramm Sie über eine beliebige Zeitraum Sie auswählen.

1. Im [Portal Azure](https://portal.azure.com/)klicken Sie auf **Durchsuchen**, und klicken Sie dann eine Ressource, die Sie für die Überwachung interessiert.

2. Im Abschnitt **Überwachung** enthält die wichtigsten Kennzahlen für jede Azure Ressource an. Angenommen, eine Web app hat **Anfragen und Fehler**, wobei als virtueller Computer **Prozentsatz der CPU** und **Datenträger lesen und Schreiben**müssten:  ![Überwachung Lens](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)

3. Indem Sie auf jedes Diagramm wird das **Metrik** Blade angezeigt werden. Klicken Sie auf das Blade, neben dem Diagramm finden eine Tabelle mit Sie Aggregationen von der Metrik (z. B. Mittelwert, Mindest- und Höchstwerte, für den Zeitraum fest, die, den Sie ausgewählt haben). Darunter befinden sich die Warnungsregeln für die Ressource.
    ![Metrische blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)

4. Um die Zeilen anzupassen, die angezeigt werden, klicken Sie auf die Schaltfläche **Bearbeiten** , klicken Sie auf das Diagramm oder den Befehl **Bearbeiten Diagramm** das metrischen Blade.

5. Klicken Sie auf das Blade Abfrage bearbeiten können Sie drei Aufgaben ausführen:
    - Ändern des Zeitraums
    - Wechseln die Darstellung zwischen Leiste und Linie
    - Wählen Sie aus verschiedenen Metics ![Abfrage bearbeiten](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)

6. Ändern des Zeitraums ist so einfach wie das Auswählen eines anderen Bereichs (z. B. **Vergangenen Stunde**) und klicken am unteren Rand der Blade **Speichern** . Sie können auch **benutzerdefinierte**auswählen, dem Sie einen bestimmten Zeitraum in den letzten 2 Wochen auswählen können. Beispielsweise können Sie die gesamte zwei Wochen oder, nur 1 Stunde von gestern anzeigen. Geben Sie in das Textfeld, geben Sie eine andere Stunde.
    ![Benutzerdefinierte Zeitraums](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)

7. Wählen Sie unterhalb des Zeitraums Kanal Sie eine beliebige Anzahl von Kennzahlen, um das Diagramm anzuzeigen.

8. Wenn Sie auf Speichern klicken, werden Ihre Änderungen für die jeweilige Ressource gespeichert werden. Beispielsweise wird Wenn Sie zwei virtuellen Computern haben und einem Diagramm auf eine Änderung, es keinen anderen Einfluss auf.

## <a name="creating-side-by-side-charts"></a>Erstellen von nebeneinander Diagrammen

Mit den leistungsstarken Anpassung im Portal können Sie beliebig viele Diagramme beliebig hinzufügen.

1. Klicken Sie im Menü am oberen Rand der Blade **...** auf **Kacheln hinzufügen**:  
    ![Fügen Sie das Menü](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Klicken Sie dann, Sie können auswählen wählen Sie ein Diagramm aus dem **Katalog** auf der rechten Seite des Bildschirms:  ![Katalog](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Wenn Sie die gewünschten die Metrik nicht angezeigt wird, können Sie jederzeit eine der voreingestellten Kennzahlen und **Bearbeiten von** hinzufügen das Diagramm, um die Metrik anzeigen, die Sie benötigen.

## <a name="monitoring-usage-quotas"></a>Überwachen der Verwendung von Kontingenten

Die meisten Kennzahlen sehen, Trends über einen Zeitraum, aber bestimmte Daten, wie die Verwendung von Kontingenten, sind Point-in-Time-Informationen mit einem Schwellenwert.

Sie können auch Verwendung von Kontingenten auf das Blade für Ressourcen anzeigen, die von Kontingenten haben:

![Verwendung](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Wie mit Kennzahlen können die [REST-API](https://msdn.microsoft.com/library/azure/dn931963.aspx) oder [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) Sie den vollständigen Satz der Verwendung von Kontingenten programmgesteuert Zugriff.

## <a name="next-steps"></a>Nächste Schritte

* [-Benachrichtigung erhalten](insights-receive-alert-notifications.md) , wenn eine Metrik einen Schwellenwert überschreitet.
* [Aktivieren die Überwachung und Diagnose](insights-how-to-use-diagnostics.md) zum Erfassen von detaillierter häufig auftretenden Kennzahlen auf Ihrem Dienst aus.
* [Anzahl der Instanzen automatisch skalieren](insights-how-to-scale.md) , um sicherzustellen, dass Ihr Dienst reagiert und verfügbar ist.
* [Monitor Application Leistung](../application-insights/app-insights-azure-web-apps.md) genau wie der Code in der Cloud ausführt, verstehen werden soll.
* Verwenden Sie [Anwendung Einsichten für JavaScript-apps und Webseiten](../application-insights/app-insights-web-track-usage.md) abzurufenden Client Analytics Informationen zu Browsern, die eine Webseite besuchen.
* [Verfügbarkeit von Monitor und Reaktionszeiten einer beliebigen Webseite](../application-insights/app-insights-monitor-web-app-availability.md) mit der Anwendung Einblicken, damit Sie heraus, ob Ihre Seite gefunden werden, ist nicht verfügbar.
