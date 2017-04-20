<properties
    pageTitle="Bereitstellen eines Webdiensts Computer Learning | Microsoft Azure"
    description="Informationen zum Konvertieren eines Experiments Schulung in eine vorhersehbare Experiments, für die Bereitstellung vorbereiten und dann als Azure-Computer Learning Web Service bereitstellen."
    services="machine-learning"
    documentationCenter=""
    authors="garyericson"
    manager="jhubbard"
    editor="cgronlun"/>

<tags
    ms.service="machine-learning"
    ms.workload="data-services"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/04/2016"
    ms.author="garye"/>

# <a name="deploy-an-azure-machine-learning-web-service"></a>Bereitstellen eines Webdiensts Learning der Azure-Computer

Azure-Computer-lernen können Sie erstellen, testen und Bereitstellen von vorhersehbare analytic Lösungen.

High-Level-von-aus Sicht von erfolgt dies in drei Schritten:

- **[Erstellen eines Experiments Training]** - Azure Computer Learning Studio ist eine gemeinsame Entwicklung visual-Umgebung, mit denen Sie Schulen und Testen Sie eine vorhersehbare Analytics Modell mit Daten, die Sie bereitstellen.
- **[Konvertieren sie eine vorhersehbare Experiments]** - einmal Modell wurde mit den vorhandenen Daten geschult und können Sie jetzt zum Bewerten der neuer Daten verwendet werden, Vorbereiten und Optimieren Sie Ihre Experiments für Vorhersagen.
- **Stellen sie als Webdienst** - Sie können Ihre vorhersehbare Experiments als [neue] oder [klassische] Azure Web Service bereitstellen. Benutzer können das Modell senden und Empfangen von Vorhersagen des Modells.

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Erstellen eines Experiments Schulung

Um ein Modell vorhersehbare Analytics Schulen, verwenden Sie Azure Computer erlernen Studio zum Erstellen eines Schulung Experiments, in dem Sie verschiedenen Modulen Schulungsdaten laden, Vorbereiten der Daten nach Bedarf, Computer Learning Algorithmen anwenden und die Ergebnisse auswerten enthalten. Sie können auf einem Versuch durchlaufen, und versuchen Sie es anderen Computer Learning Algorithmen zum Vergleichen und die Ergebnisse auswerten.

Der Vorgang des erstellen und Verwalten von Schulungen Versuche wird an anderer Stelle mehr sorgfältig behandelt. Weitere Informationen finden Sie in diesen Artikeln:

- [Erstellen eines einfachen Experiments in Azure Computer Learning Studio](machine-learning-create-experiment.md)
- [Entwickeln Sie eine vorhersehbare Lösung mit Azure-Computer Learning](machine-learning-walkthrough-develop-predictive-solution.md)
- [Importieren Sie die Schulung für Daten in Azure Computer Learning Studio](machine-learning-data-science-import-data.md)
- [Verwalten von Experiments Iterationen in Azure Computer Learning Studio](machine-learning-manage-experiment-iterations.md)

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a>Konvertieren des Experiments Schulung in eine vorhersehbare Experiments

Nachdem Sie das Modell gelernt haben, können Sie Ihre Experiments Schulung in eines vorhersehbare Experiments zum Bewerten der neuer Daten zu konvertieren.

Durch eine Umwandlung in eine vorhersehbare Experiments, erhalten Sie das Modell Ihres geschulte als Bewertungsmuster Webdienst bereitgestellt werden bieten. Benutzer des Webdiensts können Eingabedaten zum Modell senden, und Ihr Modell senden wieder die Vorhersageergebnisse. Wie Sie in eine vorhersehbare Experiments konvertieren, beachten Sie dass wie das Modell von anderen Benutzern verwendet werden soll.

Um Ihre Experiments Schulung in eine vorhersehbare Experiments zu konvertieren, klicken Sie auf am unteren Rand des Zeichenbereichs Experiments **Ausführen** , klicken Sie auf **Web-Service**wählen Sie und dann **Vorhersage-Webdienst**.

![Konvertieren in Experiments bewerten](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Weitere Informationen zum Ausführen dieser Konvertierung finden Sie unter [Konvertieren ein Computers Learning Schulung Experiments auf eine vorhersehbare Experiments](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Die folgenden Schritte beschreiben ein vorhersehbare Experiments als neue Web Service bereitstellen. Sie können auch Experiments als Classic Web Service bereitstellen.

## <a name="deploy-the-predictive-experiment-as-a-new-web-service"></a>Bereitstellen des Experiments vorhersehbare als einen neuen Webdienst

Vorhersehbare Experiments vorbereitet wurden, können Sie es als Azure Web Service bereitstellen. Mithilfe des Webdiensts, Benutzer können Daten senden, das Modell und das Modell gibt seine Vorhersagen zurück.

Klicken Sie auf am unteren Rand des Zeichenbereichs Experiments **Ausführen** , für die Bereitstellung Ihrer vorhersehbare Experiments. Nachdem der Versuch beendet ist, klicken Sie auf **Webdienst bereitstellen** , und wählen Sie **Web Service bereitstellen [neu]**.  Die Bereitstellungsseite des Portals Computer Learning-Webdienst wird geöffnet.

### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Computer Learning-Webdienst Portal Experiments-Seite bereitstellen

Geben Sie auf der Seite bereitstellen Experiments einen Namen für den Webdienst.
Wählen Sie einen pricing Plan. Wenn Sie einen vorhandenen pricing Plan, dass diese ausgewählt werden kann haben, müssen andernfalls Sie einen neuen Preisplan für den Dienst erstellen.

1.  In den **Preisplan** Dropdown-Liste, wählen Sie einen vorhandenen Plan, oder wählen Sie die Option **neuen Plan auswählen** .
2.  Geben Sie unter **Plan Name**einen Namen ein, der den Plan auf Ihrer Abrechnung identifiziert.
3.  Wählen Sie eine der **Monatlichen Planen von Ebenen**. Plan Ebenen Standard die Pläne für Ihre Standardregion und den Webdienst wird für diese Region bereitgestellt.

Klicken Sie auf **Bereitstellen** und die Seite " **Schnellstart** " für Ihre Web Service zu öffnen.

Der Schnellstart Webdienstseite erhalten Sie Hinweise und Zugriff auf am häufigsten ausgeführten Aufgaben, die nach dem Erstellen eines Webdiensts ausgeführt wird. Hier können Sie ganz einfach die Testseite und die verbrauchen Seite zugreifen.

<!-- ![Deploy the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

### <a name="test-your-web-service"></a>Testen Sie den Webdienst

Um Ihre neuen Webdienst zu testen, klicken Sie unter Allgemeine Aufgaben auf **Webdienst testen** . Klicken Sie auf der Seite Testseite können Sie den Webdienst als eine Anforderung und Antwort-Dienst (Ressourceneinträge) oder einem Batch Execution-Dienst (BES) testen.

Die Ressourceneinträge Testseite zeigt die Eingaben, Ausgaben und globale Parameter, die Sie für die Experiments definiert haben. Um den Webdienst zu testen, können Sie manuell Geben Sie geeignete Werte für die Eingaben oder eine durch Kommas getrennten Werten (CSV) formatierten Datei mit den Werten Test angeben.

Geben Sie geeignete Werte für die Eingaben, und klicken Sie auf **Anforderung und Antwort testen**, um zu testen Ressourceneinträge, aus der Liste Ansichtsmodus verwenden. Die Vorhersageergebnisse anzeigen in der Ausgabespalte links.

![Stellen Sie den Webdienst](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

Klicken Sie zum Testen Ihrer BES **Batch**. Klicken Sie auf der Seite Batch Testseite auf Durchsuchen, klicken Sie unter Ihren Eingaben, und wählen Sie aus einer CSV-Datei, die entsprechende Beispielwerte enthält. Wenn Sie keiner CSV-Datei, und Ihre vorhersehbare Experiments mit Computer Learning Studio erstellt, können Sie das Dataset für die Vorhersage Experiments herunterladen und verwenden es.

Öffnen Sie das DataSet herunterladen Computer Learning Studio. Öffnen Sie Ihre vorhersehbare Experiments, und klicken Sie mit der rechten Maustaste auf die Eingabe für Ihre Experiments. Wählen Sie aus dem Kontextmenü **Dataset** , und wählen Sie dann **herunterladen**.

![Bereitstellen des Webdiensts](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Klicken Sie auf **Testen**. Zeigt der Status des Auftrags Batch Execution rechts unter **Test Batchaufträge**.

![Stellen Sie den Webdienst](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Auf der Seite **Konfiguration** können Sie die Beschreibung, Titel ändern, aktualisieren Sie den Speicher Konto Schlüssel und Beispieldaten für den Webdienst zu aktivieren.

![Konfigurieren Sie den Webdienst](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Nachdem Sie den Webdienst bereitgestellt haben, können Sie folgende Schritte ausführen:

- **Zugriff** über die Web-Service-API.
- **Verwalten** sie über Learning der Azure-Computer, Web Services-Portal oder das Azure klassischen Portal.
- **Update** bei Ihrem Modell ändert.

### <a name="access-the-web-service"></a>Zugriff auf den Webdienst

Nachdem Sie den Webdienst aus Computer Learning Studio bereitstellen, können Daten an den Dienst senden und Empfangen von Antworten programmgesteuert.

Die Seite **verbrauchen** enthält alle Informationen, die Sie benötigen, um den Webdienst zuzugreifen. Beispielsweise wird der API-Schlüssel bereitgestellt, um autorisierten Zugriff auf den Dienst zu ermöglichen.

Weitere Informationen zum Zugreifen auf einen Computer Learning-Webdienst finden Sie unter [wie einen bereitgestellten Azure-Computer Learning-Webdienst nutzt](machine-learning-consume-web-services.md).

### <a name="manage-your-new-web-service"></a>Verwalten Sie Ihrer neuen Webdienst

Sie können das klassische Webportal Services Computer Learning Web Services verwalten. Klicken Sie auf der [Hauptseite Portal](https://services.azureml-test.net/)auf **Webdienste**. Von der Webseite Services können Sie löschen oder kopieren ein Diensts. Um einen bestimmten Dienst zu überwachen, klicken Sie auf den Dienst, und klicken Sie dann auf **Dashboard**. Zum Überwachen von Batchaufträge mit dem Webdienst verknüpft ist, klicken Sie auf **Batch anfordern Protokoll**.

## <a name="deploy-the-predictive-experiment-as-a-classic-web-service"></a>Bereitstellen des Experiments vorhersehbare als Webdienst Classic

Vorhersehbare Experiments ausreichend vorbereitet wurden, können Sie es als Azure Web Service bereitstellen. Mithilfe des Webdiensts, Benutzer können Daten senden, das Modell und das Modell gibt seine Vorhersagen zurück.

Für die Bereitstellung Ihrer vorhersehbare Experiments klicken Sie auf **Ausführen** , am unteren Rand des Zeichenbereichs Experiments ab, und klicken Sie dann auf **Web-Service bereitstellen**. Der Webdienst eingerichtet ist, und Sie befinden sich im Web Service Dashboard.

![Stellen Sie den Webdienst](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

Sie können den Webdienst in der maschinellen Learning Web Services-Portal oder Computer Learning Studio testen.

Klicken Sie auf die Schaltfläche **Test** im Web Service Dashboard, zum Testen des Webdiensts Antwort anfordern. Ein Dialogfeld eingeblendet wird, für die Eingabedaten für den Dienst gefragt. Dies sind die Spalten von bewertet Experiments erwartet. Geben Sie einen Satz von Daten, und klicken Sie dann auf **OK**. Die Ergebnisse, die vom Webdienst generiert werden am unteren Rand des Dashboards angezeigt.

Sie können den Link, um Ihren Dienst im Azure Computer Learning Web Services-Portal testen, wie zuvor im Bereich neue Web Service dargestellt **Testen** Vorschau klicken.

Um den Batch Ausführung Dienst zu testen, klicken Sie auf Vorschau des Links **zu testen** . Klicken Sie auf der Seite Batch Testseite auf Durchsuchen, klicken Sie unter Ihren Eingaben, und wählen Sie aus einer CSV-Datei, die entsprechende Beispielwerte enthält. Wenn Sie keiner CSV-Datei, und Ihre vorhersehbare Experiments mit Computer Learning Studio erstellt, können Sie das Dataset für die Vorhersage Experiments herunterladen und verwenden es.

![Testen des Webdienstes](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Auf der Seite **Konfiguration** können Sie den Anzeigenamen des Diensts geändert und eine Beschreibung. Den Namen und die Beschreibung wird im [Azure klassischen Portal](http://manage.windowsazure.com/) , auf denen Sie Ihre Webdienste verwalten, angezeigt.

Sie können eine Beschreibung für Ihre Eingabedaten, Ausgabe von Daten und Webdienstparametern durch Eingabe einer Zeichenfolge für die einzelnen Spalten unter **INPUT-SCHEMA**, **AUSGABESCHEMA**und **WEBDIENSTPARAMETER**bereitstellen. Diese Beschreibungen werden in der Dokumentation Beispiel Code für den Webdienst verwendet.

Sie können die Protokollierung Diagnostizieren von Fehlern, die angezeigt werden, wenn Ihr Webdienst zugegriffen wird. Weitere Informationen finden Sie unter [Aktivieren der Protokollierung für Computer-Learning-Webdienste](machine-learning-web-services-logging.md).

![Konfigurieren Sie den Webdienst](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

Sie können auch die Endpunkte für den Webdienst im Azure Computer Learning Web Services-Portal vergleichbar mit dem Verfahren gezeigt zuvor im Bereich neue Web Service konfigurieren. Die Optionen unterscheiden sich, die Sie hinzufügen oder ändern Sie die Beschreibung der Dienste sowie die Protokollierung aktivieren und Enable-Beispieldaten für das Testen können.

### <a name="access-the-web-service"></a>Zugriff auf den Webdienst

Nachdem Sie den Webdienst aus Computer Learning Studio bereitstellen, können Daten an den Dienst senden und Empfangen von Antworten programmgesteuert.

Das Dashboard bietet alle Informationen, die Sie benötigen, um den Webdienst zuzugreifen. Beispielsweise der API-Schlüssel wird bereitgestellt, um den autorisierten Zugriff auf den Dienst zu ermöglichen, und API-Hilfeseiten für Hilfe bereitgestellt werden steigen Schreiben des Codes.

Weitere Informationen zum Zugreifen auf einen Computer Learning-Webdienst finden Sie unter [wie einen bereitgestellten Azure-Computer Learning-Webdienst nutzt](machine-learning-consume-web-services.md).

### <a name="manage-the-web-service"></a>Verwalten des Webdiensts

Es gibt verschiedene Aktionen, die bei der Durchführung ein Webdiensts überwachen. Sie können aktualisieren und löschen. Sie können auch zusätzliche Endpunkte für einen Webdienst Classic, zusätzlich zu den standardmäßigen Endpunkt hinzufügen, die bei der Bereitstellung erstellt wird.

Weitere Informationen finden Sie unter [Verwalten einer Azure-Computer Learning-Arbeitsbereich](machine-learning-manage-workspace.md) und [Verwalten eines Webdiensts mithilfe des Azure Computer Learning Web Services-Portals](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix the link and uncomment
For more information on how to manage Azure Machine Learning web service endpoints using the REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-the-web-service"></a>Aktualisieren Sie den Webdienst

Vornehmen von Änderungen an den Webdienst, wie das Aktualisieren des Modells mit zusätzlichen Daten, und es erneut, und überschreiben Sie den ursprünglichen Webdienst bereitstellen können.

Öffnen Sie zum Aktualisieren des Webdiensts des ursprünglichen vorhersehbare Experiments, den Sie zum Bereitstellen des Webdiensts, und stellen Sie eine bearbeitbare Kopie durch Klicken auf **SAVE AS**verwendet. Nehmen die Änderungen vor, und klicken Sie dann auf **Web-Service bereitstellen**.

Da Sie diese Experiments bevor Sie bereitgestellt haben, werden Sie gefragt, ob überschreiben (klassische Webdienst) oder (neuen Webdienst) die vorhandene Updatedienst werden soll. Beendet den vorhandenen Webdienst und das neue bereitgestellt durch Klicken auf **Ja** oder **Update** an ihrer Stelle Vorhersagen Experiments bereitgestellt wird.

> [AZURE.NOTE] Wenn Sie Konfiguration in der ursprünglichen Webdienst geändert, beispielsweise müssen eingeben einer neuen Anzeigenamen oder die Beschreibung, Sie diese Werte erneut eingeben.

Eine Option zum Aktualisieren des Webdiensts wird auf die einzelnen Details des Modells programmgesteuert neu trainieren. Weitere Informationen finden Sie unter [neu trainieren Computer Learning programmgesteuert modelliert](machine-learning-retrain-models-programmatically.md).


<!-- internal links -->
[Erstellen eines Experiments Schulung]: #create-a-training-experiment
[Um eine vorhersehbare besser zu konvertieren]: #convert-the-training-experiment-to-a-predictive-experiment
[Neu]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Classic]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
