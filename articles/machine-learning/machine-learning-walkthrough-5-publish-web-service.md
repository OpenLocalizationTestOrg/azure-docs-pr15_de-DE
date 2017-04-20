<properties
    pageTitle="Schritt 5: Bereitstellen des Computers Learning-Webdiensts | Microsoft Azure"
    description="Schritt 5 des der Entwicklungsphase eine vorhersehbare Lösung Exemplarische Vorgehensweise: Bereitstellen ein vorhersehbare Experiments in maschinellen Learning Studio als Webdienst."
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
    ms.date="10/05/2016"
    ms.author="garye"/>


# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a>Exemplarische Vorgehensweise Schritt 5: Bereitstellen des Azure Computer Learning-Webdiensts

Dies ist der fünfte Schritt der exemplarischen Vorgehensweise, [Entwickeln einer Lösung vorhersehbare Analytics in Azure-Computer lernen](machine-learning-walkthrough-develop-predictive-solution.md)


1.  [Erstellen Sie einen Computer Learning-Arbeitsbereich](machine-learning-walkthrough-1-create-ml-workspace.md)
2.  [Hochladen von vorhandenen Daten](machine-learning-walkthrough-2-upload-data.md)
3.  [Erstellen eines neuen Experiments](machine-learning-walkthrough-3-create-new-experiment.md)
4.  [Schulen und Auswerten der Modelle](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5.  **Stellen Sie den Web-Dienst**
6.  [Zugriff auf den Webdienst](machine-learning-walkthrough-6-access-web-service.md)

----------

Damit andere Personen können die Möglichkeit, das vorhersehbare Objektmodell verwenden, das wir in dieser exemplarischen Vorgehensweise entwickelt haben, stellen wir es als einen Webdienst auf Azure bereit.

Bisher haben wir Experimentieren mit unserem Modell Schulungen. Aber schlägt des bereitgestellten Diensts nicht mehr Erfassung - Vorhersagen durch Eingabe des Benutzers auf der Grundlage unserer Modells bewerten generiert wird. Damit wir Plänen vorbereitende Schritte dieser Experiments eines Experiments ***Schulung*** zum Konvertieren einer ***vorhersehbare*** experimentieren. 

Dies umfasst zwei Schritte:  

1. Konvertieren der *Schulung experimentieren* , die wir erstellt haben, in eine *vorhersehbare Experiments*
2. Bereitstellen des Experiments vorhersehbare als Webdienst

Aber wir zunächst ein wenig dieses Experiments zu optimieren. Derzeit haben wir zwei verschiedene Modelle den Versuch, aber wir nur ein Modell soll, wenn wir dies als Web Service bereitstellen.  

Nehmen wir an, dass wir entschieden haben, dass das Strukturmodell unterstützter besser Modell verwendet wurde. So führen Sie als Erstes ist die [Zwei-Klasse Unterstützung Vektor Computer] entfernen[ two-class-support-vector-machine] Modul und die Module, die für diese Schulung verwendet wurden. Sie möchten eine Kopie des Experiments zuerst zu erstellen, indem Sie auf **Speichern unter** am unteren Rand des Zeichenbereichs Experiments ab.

Wir müssen die folgenden Modulen zu löschen:  

- [Unterstützung für zwei-Klasse Vektor Computer][two-class-support-vector-machine]
- [Schulen Modell] [ train-model] und [Bewertung Modell] [ score-model] Module, das damit verbunden wurden,
- [Normalisieren von Daten] [ normalize-data] (beide)
- [Auswerten Modells][evaluate-model]

Wählen Sie das Modul, und drücken Sie die ENTF-Taste, oder das Modul Maustaste, und wählen Sie **Löschen**.

Nachdem wir dieses Modell mit der [Verstärkt-Entscheidungsstruktur beiden Klasse]bereitstellen sind[two-class-boosted-decision-tree].

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a>Konvertieren des Experiments Schulung in eine vorhersehbare Experiments

Konvertieren in eine vorhersehbare Experiments umfasst drei Schritte:

1. Speichern Sie das Modell geschulte haben, und Ersetzen Sie unsere Schulungsmodule
2. Kürzen des Experiments um Module zu entfernen, die nur für die Schulung benötigt wurden
3. Definieren Sie, in dem der Webdienst Eingabe akzeptiert und der, in dem die Ausgabe generiert wird

Zum Glück können alle drei Schritte ausgeführt werden, durch Klicken auf **Festlegen von Webdienst** am unteren Rand des Zeichenbereichs Experiments (Wählen Sie die Option **Vorhersage-Webdienst** ).

Wenn Sie **Festlegen von Webdienst**klicken, werden verschiedene Aktionen durchgeführt:

- Geschulte Modell wird in der Palette Modul am linken Rand des Zeichenbereichs Experiments als einzelnes Modul **Geschult Modell** gespeichert (Sie es unter **Geschult Modelle**finden).
- Module, die für die Schulung verwendet wurden, werden entfernt. Insbesondere:
  - [Zwei-Klasse unterstützter Entscheidungsstruktur][two-class-boosted-decision-tree]
  - [Zug-Modell][train-model]
  - [Aufteilen von Daten][split]
  - Das zweite [R-Skript ausführen] [ execute-r-script] Modul, die für Testdaten verwendet wurde
- Gespeicherte geschulte Modell wird wieder in Experiments hinzugefügt.
- **Web Service Eingabe-** und **Web Service** Module werden hinzugefügt.

> [AZURE.NOTE] Experiments wurde in zwei Teile im Rahmen der Registerkarten, die am oberen Rand des Zeichenbereichs Experiments hinzugefügt wurden gespeichert: der ursprünglichen Schulung Experiments ist auf der Registerkarte **Training experimentieren**und des neu erstellten vorhersehbare Experiments unter **prädiktive experimentieren**.

Wir müssen mit diesem bestimmten Versuch ein zusätzlicher Schritt erforderlich.
Wir zwei [R-Skript ausführen] hinzugefügt[ execute-r-script] Module, um eine Gewichtung-Funktion mit den Daten für die Schulung und Testen von bereitzustellen. Wir brauchen, die im letzten Modell tun.

Computer Learning Studio entfernt ein [R-Skript ausführen] [ execute-r-script] Modul beim Entfernen der [Teilung] [ split] Modul. Nun können wir jetzt der anderen entfernen und [Metadaten Editor] verbinden[ metadata-editor] direkt auf [Score Modell][score-model].    

Unsere Experiments sollte nun wie folgt aussehen:  

![Bewerten des geschult Modells][4]  

> [AZURE.NOTE] Sie vielleicht, warum es UCI Deutsch Kreditkartendaten Datasets in vorhersehbare Experiments links. Der Dienst geht, verwenden Sie die Daten des Benutzers, nicht im ursprünglichen Dataset, also Warum sollten Sie das ursprüngliche Dataset im Modell?
>
>Es gilt, dass der Dienst nicht die ursprünglichen Kreditkartendaten erforderlich ist. Aber das Schema für diese Daten, einschließlich Informationen wie wie viele Spalten vorhanden sind und welche Spalten sind numerisch. Diese Schemainformationen ist erforderlich, die Daten des Benutzers interpretiert werden. Wir lassen Sie diese Komponenten verbunden, sodass das Bewertungsmuster Modul das Dataset-Schema hat, wenn der Dienst ausgeführt wird. Die Daten wird nicht verwendet, nur das Schema.  

Ausführen des Experiments ein letzter Versuch (klicken Sie auf **Ausführen**.) Um sicherzustellen, dass die einzelnen Details des Modells weiterhin funktionsfähig ist, klicken Sie auf die Ausgabe des [Score Modell] [ score-model] Modul und select- **Ergebnisse anzeigen**. Sehen Sie, dass die ursprünglichen Daten angezeigt werden, zusammen mit der Credit Risikowert ("Etiketten bewertet") und den bewertet Wahrscheinlichkeitswert ("bewertet Wahrscheinlichkeiten".) 

## <a name="deploy-the-web-service"></a>Bereitstellen des Webdiensts

Sie können die Experiments als eine klassische Webdienst oder einen neuen Webdienst basierend auf Azure-Ressourcen-Manager bereitstellen.

### <a name="deploy-as-a-classic-web-service"></a>Als klassische Web Service bereitstellen ###

Um eine klassische Webdienst unsere Experiments abgeleiteten bereitzustellen, klicken Sie auf **Webdienst bereitstellen** unterhalb des Zeichenbereichs ab, und wählen Sie **Webdienst bereitstellen [Classic]**. Computer Learning Studio Experiments als Webdienst bereitgestellt und gelangen Sie dem Dashboard für diesen Webdienst. Von hier aus können Sie zurückgeben des Experiments (**Snapshot** oder **Anzeigen neuesten**) und führen Sie einen einfachen Test des Webdiensts (siehe **Testen des Webdiensts** unten). Es gibt auch hier Informationen zum Erstellen von Anwendungen, die den Webdienst (mehr dazu im nächsten Schritt dieser exemplarischen Vorgehensweise) zugreifen können.

![Web-Service-dashboard][6]

Sie können den Dienst durch Klicken auf die Registerkarte **Konfiguration** konfigurieren. Hier können Sie den Namen (es ist der Name des Experiments standardmäßig erteilt) ändern, und weisen Sie ihr eine Beschreibung. Sie können auch weitere benutzerfreundlichen Beschriftungen für die Eingabe- und Ausgabeparameter Spalten geben.  

![Konfigurieren Sie den Webdienst][5]  

### <a name="deploy-as-a-new-web-service"></a>Als neue Web Service bereitstellen

Klicken Sie zum Bereitstellen eines neuen Webdiensts unsere Experiments abgeleitet **Webdienst bereitstellen** unten den Zeichenbereich und den **Webdienst bereitstellen [New]**. Computer Learning Studio überträgt Sie an der Azure Computer Learning Services bereitstellen Experiments Webseite.

Geben Sie einen Namen für den Webdienst, und wählen Sie einen Plan pricing. Wenn Sie einen vorhandenen pricing Plan, dass diese ausgewählt werden kann haben, müssen andernfalls Sie einen neuen Preisplan für den Dienst erstellen. 

1.  Wählen Sie in der Dropdownliste **Preisplan** einen vorhandenen Plan, oder wählen Sie die Option **neuen Plan auswählen** .
2.  Geben Sie unter **Plan Name**einen Namen, der den Plan auf Ihrer Abrechnung identifiziert.
3.  Wählen Sie eine der **Monatlichen Planen von Ebenen**. Das Plan Ebenen wird standardmäßig die Pläne für Ihre Standardregion und den Webdienst wird für diese Region bereitgestellt.

Klicken Sie auf **Bereitstellen** und die Seite " **Schnellstart** " für Ihre Web Service zu öffnen.

Sie können den Dienst konfigurieren, indem Sie auf die Menüoption **Konfigurieren** . Hier können Sie den Namen (es ist der Name des Experiments standardmäßig erteilt) ändern, und weisen Sie ihr eine Beschreibung. 

Klicken Sie zum Testen der Web-Dienst auswählen auf die Menüoption **Testen** (siehe unten **den Webdienst testen** ). Informationen zum Erstellen von Anwendungen, die den Webdienst zugreifen können, klicken Sie auf die Menüoption **verbrauchen** (mehr dazu im nächsten Schritt dieser exemplarischen Vorgehensweise).

> [AZURE.TIP] Sie können den Webdienst aktualisieren, nachdem Sie sie bereitgestellt haben. Beispielsweise, wenn Sie das Modell ändern möchten, bearbeiten Sie des Experiments Schulung, Optimieren Sie die Parameter für ein, und klicken Sie auf **Web-Service bereitstellen**. Wählen Sie dann **Bereitstellen Webdienst [Classic]** oder **[New] Webdienst bereitstellen**. Wenn Sie Experiments erneut bereitstellen, wird den Webdienst jetzt mithilfe des aktualisierte Modell ersetzt.  

## <a name="test-the-web-service"></a>Testen Sie den Webdienst

### <a name="test-a-classic-web-service"></a>Testen Sie einen klassischen Webdienst

Sie können den Dienst in Computer Learning Studio oder im Azure Computer Learning Web Services-Portal testen. Im Azure Computer Learning Web Services-Portal Testen hat den Vorteil, dass Sie aktivieren 

**Testen Sie in Computer Learning Studio**

Klicken Sie auf der Seite **DASHBOARD** unter **Endpunkt Standard**auf der Schaltfläche **Testen** . Ein Dialogfeld wird pop-up und fordern Sie die Eingabedaten für den Dienst. Dies sind dieselben Spalten, die im ursprünglichen Deutsch Credit Risiko Dataset verwendet wurde.  

Geben Sie einen Satz von Daten, und klicken Sie dann auf **OK**. 

**Testen Sie im Azure Computer Learning Web Services-portal**

Klicken Sie auf **der Dashboardseite** auf den Link **Test** Vorschau unter **Standard-Endpunkt**. Die Testseite im Azure Computer Learning Web Services-Portal für den Webdienst-Endpunkt wird geöffnet und fordert Sie die Eingabedaten für den Dienst. Dies sind dieselben Spalten, die im ursprünglichen Deutsch Credit Risiko Dataset verwendet wurde.

Klicken Sie auf **Test Anforderung und Antwort**. 

In den Webdienst, die Daten über das **Web Service Eingabe** Modul an, über den [Metadaten-Editor] eingibt[ metadata-editor] Modul, und auf das [Modell Score] [ score-model] Modul, in dem er bewertet wird. Die Ergebnisse werden dann vom Webdienst über die **Web Service Ausgabe**ausgegeben.

**Testen eines neuen Webdiensts**

Klicken Sie im Azure-Computer Learning Web Services-Portal auf **Test** am oberen Seitenrand. **Die Testseite** wird geöffnet, und Sie können Eingabedaten für den Dienst. Input angezeigten Felder entsprechen den Spalten, die im ursprünglichen Deutsch Credit Risiko Dataset verwendet wurde. 

Geben Sie einen Satz von Daten, und klicken Sie dann auf **Test Anforderung und Antwort**.

Die Ergebnisse des Tests werden auf der rechten Seite der Seite in der Ausgabespalte angezeigt. 

Beim Testen der im Azure Computer Learning Web Services-Portal können Sie Beispieldaten, die Sie zum Testen des Anforderung und Antwort-Diensts verwenden können. Wenn Sie den Webdienst Computer Learning Studio erstellt haben, werden die Beispieldaten aus die Daten Ihrer, um das Modell zu schulen übernommen.

> [AZURE.TIP] Wir haben die Vorhersage Experiments konfiguriert, wie die gesamte erzeugt, aus dem [Modell Score] [ score-model] Modul zurückgegeben werden. Dazu gehören alle Eingabedaten plus der Credit Risikowert und die Wahrscheinlichkeit bewertet. Wenn Sie etwas andere - zurückgeben möchten beispielsweise nur der Kredit Risiko Wert - und klicken Sie dann ein [Projekt Spalten] eingefügt werden könnten[ project-columns] Modul zwischen [Score Modell] [ score-model] und der **Web-Service-Ausgabe** für Spalten angezeigt werden, wenn Sie nicht den Webdienst zurückgeben möchten. 

## <a name="manage-the-web-service"></a>Verwalten des Webdiensts

**Verwalten eines klassischen-Webdiensts**

Nachdem Sie den klassischen Webdienst bereitgestellt haben, können Sie es aus dem [Azure klassische Portal](https://manage.windowsazure.com)verwalten.

1. Melden Sie sich bei dem [Azure klassischen Portal](https://manage.windowsazure.com).
2. Klicken Sie im Bereich Dienste Microsoft Azure **Computer LEARNING**auf.
3. Klicken Sie auf den Arbeitsbereich.
4. Klicken Sie auf der Registerkarte **Webdienste** .
5. Klicken Sie auf den Webdienst, der erstellt wurde.
6. Klicken Sie auf den Endpunkt "Default".

Von hier aus Sie können Aktionen wie überwachen, wie der-Webdienst Aufgaben verwendet wird, und stellen Leistung sein durch ändern, wie viele gleichzeitige der Dienst ruft behandeln können.
Sie können auch den Webdienst in Azure Marketplace veröffentlichen.

Weitere Informationen finden Sie unter:

- [Erstellen von Endpunkten](machine-learning-create-endpoint.md)
- [Scaling-Webdienst](machine-learning-scaling-webservice.md)
- [Veröffentlichen von Azure Computer Learning-Webdienst in Azure Marketplace](machine-learning-publish-web-service-to-azure-marketplace.md)

**Verwalten von einem Webdienst im Azure Computer Learning Web Services-portal**

Nachdem Sie den Webdienst, Classic oder neu bereitgestellt haben, können Sie es aus dem [Azure-Computer Learning Web Services-Portal](https://servics.azureml.net)verwalten.

So überwachen Sie die Leistung des Webdienstes

1. Melden Sie sich der [Azure-Computer Learning Web Services-Portal](https://servics.azureml.net).
2. Klicken Sie auf **Webdienste**.
3. Klicken Sie auf den Webdienst.
4. Klicken Sie auf das **Dashboard**.

----------

**Weiter: [Zugriff auf den Webdienst](machine-learning-walkthrough-6-access-web-service.md)**

[1]: ./media/machine-learning-walkthrough-5-publish-web-service/publish1.png
[2]: ./media/machine-learning-walkthrough-5-publish-web-service/publish2.png
[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/