<properties
    pageTitle="Eine einfache Experiments im Computer Learning Studio | Microsoft Azure"
    description="Diesem Computer Learning Lernprogramm führt Sie durch eine einfache Daten Science Experiments. Wir können den Preis für ein Auto mithilfe eines Regressionsformel Algorithmus Vorhersagen."
    keywords="Experimentieren Sie, linear Regressionsformel, Computer Learning Algorithmen, Computer Learning Lernprogramm, vorhersehbare Modellierung Techniken, Daten Science Experiments"
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
    ms.topic="hero-article"
    ms.date="07/14/2016"
    ms.author="garye"/>

# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Computer Learning-Lernprogramm: Erstellen Ihrer ersten Daten Science Experiments in Azure Computer erlernen Studio

Diese Computer Learning-Lernprogramm führt Sie durch eine einfache Daten Science Experiments. Wir erstellen ein linear Regressionsformel-Modell, das prognostiziert, stellen Sie der Preis für ein Auto wie basierend auf verschiedene Variablen und technischen Spezifikationen. Dazu verwenden wir Azure Computer Learning Studio zur Entwicklung und zum Durchlaufen einer einfaches vorhersehbare, dass Analytics experimentieren.

*Vorhersehbare Analytics* ist eine Art von Daten Science, die aktuelle Daten zum Vorhersagen von zukünftigen Ergebnisse verwendet. Für ein einfaches Beispiel des vorhersehbare Analytics, sehen Sie sich Daten Science für Anfänger video 4: [Antwort mit ein einfaches Modell vorhergesagt](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) (Common Language Runtime: 7:42).

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Wie hilft Computer Learning Studio?

Computer Learning Studio erleichtert es ein Versuch, mithilfe von Drag-and-Drop Modulen mit Vorhersage Modellierung Techniken vorprogrammierte einrichten. Um Ihre Experiments ausführen und Vorhersagen eine Antwort, verwenden Sie Computer Learning Studio *ein Modell zu erstellen*, *das Modell Zug*und *Score und das Modell testen*.

Geben Sie Computer Learning Studio: [https://studio.azureml.net](https://studio.azureml.net). Wenn Sie in Computer Learning Studio vor angemeldet haben, klicken Sie auf **hier anmelden**. Andernfalls klicken Sie auf **Sign Up** und zwischen kostenlosen und kostenpflichtigen Optionen auswählen.

Weitere allgemeine Informationen zu Computer Learning Studio finden Sie unter [Neuigkeiten Computer Learning Studio?](machine-learning-what-is-ml-studio.md)

## <a name="five-steps-to-create-an-experiment"></a>Fünf Schritte zum Erstellen einer Experiments

Auf diesem Computer Lernprogramm erlernen werden Sie fünf grundlegenden Schritte zum Erstellen eines Experiments im Computer erlernen Studio, um erstellen, Schulen und das Modell Punktzahl ausführen:

- Erstellen eines Modells
    - [Schritt 1: Get-Daten]
    - [Schritt 2: Vorverarbeitet Daten]
    - [Schritt 3: Definieren von features]
- Schulen Sie die einzelnen Details des Modells
    - [Schritt 4: Auswählen und Anwenden eines Algorithmus learning]
- Bewerten Sie und Testen Sie die einzelnen Details des Modells
    - [Schritt 5: Neue Autohändler Preise Vorhersagen]

[Schritt 1: Get-Daten]: #step-1-get-data
[Schritt 2: Vorverarbeitet Daten]: #step-2-preprocess-data
[Schritt 3: Definieren von features]: #step-3-define-features
[Schritt 4: Auswählen und Anwenden eines Algorithmus learning]: #step-4-choose-and-apply-a-learning-algorithm
[Schritt 5: Neue Autohändler Preise Vorhersagen]: #step-5-predict-new-automobile-prices


## <a name="step-1-get-data"></a>Schritt 1: Get-Daten

Es gibt eine Reihe von Beispiel-Datasets enthaltene Computer Learning Studio, die Sie auswählen können, und Importieren von Daten aus mehreren Quellen. In diesem Beispiel wird die enthalten Beispieldaten, **Auto Preisdaten (Rohstoffe)**verwendet.
Dieses Dataset enthält Einträge für eine Anzahl von einzelnen Automobilen, einschließlich Informationen wie Marke, Modell, technische Spezifikationen und Preis.

1. Starten eines neuen Experiments durch Klicken auf **+ neu** am unteren Fensterrand Computer Learning Studio, wählen Sie **EXPERIMENTIEREN**, und wählen Sie dann auf **Leere experimentieren**. Wählen Sie den Standardnamen Experiments am oberen Rand des Zeichenbereichs ab, und benennen Sie ihn in einen aussagekräftigeren Namen, beispielsweise **Auto Preis Vorhersage**.

2. Auf der linken Seite des Experiments ist Zeichenbereich eine Palette von Datasets und Module. Typ **Auto** in das Suchfeld im oberen Bereich des diese Palette Dataset suchen mit der Bezeichnung **Auto Preisdaten (Rohstoffe)**.

    ![Palette-Suche][screen1a]

3. Ziehen Sie das Dataset Experiments hinzugefügt.

    ![DataSet][screen1]

Um herauszufinden, wie diese Daten aussieht, klicken Sie auf der Ausgangs-Port am unteren Rand der Autohändler Dataset, und wählen Sie dann **visualisieren**.

![Modul Ausgangs-port][screen1c]

Die Variablen im Dataset als Spalten angezeigt werden, und jeder einzelnen Instanz des ein Auto als eine Zeile angezeigt. Die äußersten rechten Spalte (Spalte 26 und mit dem Titel "Preis") ist die Zielvariable, wir möchten vorhergesagt testen.

![DataSet Visualisierung][screen1b]

Schließen Sie das Visualisierungsfenster, indem Sie das "**X**" in der oberen rechten Ecke auf.

## <a name="step-2-preprocess-data"></a>Schritt 2: Vorverarbeitet Daten

Ein Dataset erfordert in der Regel einige vorverarbeitung, bevor es analysiert werden kann. Sie können die fehlenden Werte in den Spalten von verschiedenen Zeilen vorhanden bemerkt haben. Diese fehlenden Werte müssen bereinigt werden, damit das Modell ordnungsgemäß Daten analysieren kann. In diesem Fall werden wir Zeilen entfernen, die fehlende Werte aufweisen. Darüber hinaus hat die **normalisiert Verlusten** Spalte einen großen Bereich des fehlenden Werten, damit wir diese Spalte ganz aus dem Modell ausgeschlossen werden.

> [AZURE.TIP] Bereinigen die fehlenden Werte aus den Eingabedaten ist eine Voraussetzung für die meisten der Module verwenden.

Zuerst werden wir die Spalte **normalisiert Verlusten** entfernt, und wir werden entfernen Sie jede Zeile, die Daten fehlen.

1. **Wählen Sie Spalten** Geben Sie in das Suchfeld am oberen Rand der Palette Modul die [Spalten in Dataset auswählen] suchen[ select-columns] Modul, und ziehen Sie es des Experiments Leinen und Verbinden mit der Ausgangs-Port des Datasets auf **Auto Preisdaten (Rohstoffe)** . In diesem Modul kann wir auswählen, welche Datenspalten wir möchten ein- oder Ausschließen von im Objektmodell.

2. Wählen Sie die [Spalten auswählen in Dataset] [ select-columns] Modul, und klicken Sie im **Eigenschaftenbereich** auf **Spalte Datenauswahl zu starten** .

    - Klicken Sie auf der linken Seite auf **Regeln**
    - Klicken Sie unter **Beginnen mit**auf **alle Spalten**. Dies weist [Spalten auswählen in Dataset] [ select-columns] , bis alle Spalten (mit Ausnahme der wir ausschließen) zu übergeben.
    - Wählen Sie **ausschließen** und **Spaltennamen**Dropdown-Liste und klicken Sie dann in das Textfeld. Es wird eine Liste der Spalten angezeigt. SELECT **normalisiert Verlusten**, und es wird das Textfeld hinzugefügt werden.
    - Klicken Sie auf die Schaltfläche Häkchen (OK), um die Spaltenauswahl zu schließen.

    ![Spalten auswählen][screen3]

    Im Eigenschaftenbereich für **Spalten auswählen in Dataset** gibt an, dass es über alle Spalten aus dem Dataset außer **normalisiert Verlusten**übergeben wird.

    ![Wählen Sie Spalten in Dataset-Eigenschaften][screen4]

    > [AZURE.TIP] Sie können einen Kommentar in ein Modul durch Doppelklicken auf das Modul und dem Eingeben von Text hinzufügen. Dadurch können Sie auf einen Blick sehen in Ihrer Experiments tut das Modul. Doppelklicken Sie in diesem Fall auf die [Spalten in Dataset auswählen] [ select-columns] Modul, und geben Sie den Kommentar "ausschließen normalisiert Verlusten."

3. Ziehen Sie die [Clean fehlende Daten] [ clean-missing-data] Modul des Experiments Leinen und Verbinden mit den [Spalten in Dataset auswählen] [ select-columns] Modul. Wählen Sie im **Eigenschaftenbereich** unter **Reinigung Modus** zum Bereinigen der Daten durch Entfernen von Zeilen mit fehlenden Werten **gesamte Zeile zu entfernen** . Doppelklicken Sie auf das Modul, und geben Sie den Kommentar "Entfernen von fehlenden Wert Zeilen".

    ![Clean fehlende Dateneigenschaften][screen4a]

4. Ausführen des Experiments durch Klicken auf **Ausführen** unter Experiments Zeichenbereichs ab.

Wenn der Versuch beendet ist, haben alle Module ein grünes Häkchen, um anzugeben, dass sie erfolgreich fertig gestellt. Beachten Sie auch den Status **beendet ausgeführt** , in der oberen rechten Ecke.

![Ersten Versuch ausgeführt][screen5]

Wir den Versuch bisher getan haben nur die Daten zu bereinigen. Wenn Sie das bereinigte Dataset anzeigen möchten, klicken Sie auf der linken Ausgangs-Port der [Clean fehlende Daten] [ clean-missing-data] Modul ("bereinigt Dataset") und select **visualisieren**. Beachten Sie, dass die **normalisiert Verlusten** Spalte ist nicht mehr enthalten keine fehlenden Werte vorhanden sind.

Nun, die Daten clean ist, können wir können Sie angeben, welche Features wir im vorhersehbare Modell verwenden möchten.

## <a name="step-3-define-features"></a>Schritt 3: Definieren von features

Computers erlernen sind *Features* einzelnen messbare Eigenschaften des etwas, das Sie interessiert. In unserem Dataset jede Zeile eine Auto darstellt, und jeder Spalte ist ein Feature von, Auto.

Suchen nach einer gut erfordert Satz an Funktionen zum Erstellen eines Modells vorhersehbaren experimentieren und Kenntnisse über das Problem gelöst werden sollen. Einige Features sind besser für die Vorhersage des Ziels als andere. Einige Features haben auch, eine starke Korrelation mit anderen Features (z. B. Ort-mpg im Vergleich zu fahren mpg), sodass sie werden das Modell nicht viele neuen Informationen hinzugefügt werden und entfernt werden kann.

Erstellen Sie ein Modell, das eine Teilmenge der Features in unseren Dataset verwendet wird. Sie können zurückkehren und wählen Sie andere Features, des Experiments erneut ausführen und überprüfen, ob eine bessere Ergebnisse zu erhalten. Jedoch zum Starten, versuchen Sie die folgenden Features:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Ziehen Sie ein anderes [Wählen Sie Spalten in Dataset] [ select-columns] Modul des Experiments Leinen und Verbinden mit der linken Ausgangs-Port der [Clean fehlende Daten] [ clean-missing-data] Modul. Doppelklicken Sie auf das Modul, und geben Sie "Select Features für die Vorhersage".

2. Klicken Sie im **Eigenschaftenbereich** auf **Spalte Datenauswahl zu starten** .

3. Klicken Sie auf **Regeln**.

4. Klicken Sie unter **Beginnen mit** auf **keine Spalten**, und wählen Sie dann **einschließen** und **Spaltennamen** in der Filterzeile. Geben Sie die Liste der Spaltennamen. Dies weist das Modul nur Spalten passieren, die wir angeben.

    > [AZURE.TIP] Durch Ausführen des Experiments, haben wir sichergestellt, dass die Spaltendefinitionen für die Daten aus dem Dataset über die [Clean fehlende Daten] übergeben[ clean-missing-data] Modul. Dies bedeutet, dass andere Module beim Herstellen einer Verbindung auch Informationen aus der DataSet.

5. Klicken Sie auf die Häkchentaste (OK).

![Spalten auswählen][screen6]

Dies ergibt das Dataset, das in den Algorithmus Learning in den nächsten Schritten verwendet werden. Sie können später zurückzugeben und versuchen Sie es erneut mit einer anderen Auswahl der Features.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Schritt 4: Auswählen und Anwenden eines Algorithmus learning

Nun, dass die Daten bereit sind, besteht aus einem vorhersehbare-Modell erstellen Schulung und testen. Verwenden wir unsere Daten zu schulen die einzelnen Details des Modells und Testen Sie das Modell, um festzustellen, wie nahe Preise vorhergesagt werden kann. Für den Moment keine Gedanken Sie über Warum müssen Sie Schulen und ein Modell testen.

*Klassifizierung* und *Regressionsformel* werden zwei Arten des überwachten Computers Techniken erlernen. Klassifizierung prognostiziert eine Antwort von einem definierten Satz von Kategorien, wie eine Farbe (Rot, Blau oder Grün). Regressionsformel wird verwendet, um eine Zahl vorhergesagt werden.

Da wir Preis, schätzen, die eine Zahl ist möchten, verwenden wir ein Modell Regressionsformel. In diesem Beispiel werden wir eine einfache *lineare Regressionsformel* Modell Schulen und im nächsten Schritt werden wir es testen.

1. Wir verwenden Sie unsere Daten für Schulung und Testen von Teilen in separaten Schulung und legt testen. Wählen Sie aus, und ziehen Sie die [Aufgeteilten Daten] [ split] Modul des Experiments Leinen, und schließen Sie es an die Ausgabe des letzten [Spalten auswählen in Dataset] [ select-columns] Modul. **Anteil der Zeilen im ersten Ausgabe Dataset** auf 0,75 festgelegt. Auf diese Weise wir verwenden Sie 75 Prozent der Daten, um das Modell zu schulen und halten Sie wieder 25 Prozent für das Testen.

    > [AZURE.TIP] Durch den Parameter **Random Seed** ändern, können Sie verschiedene Stichproben für Schulung und Testen von produzieren. Dieser Parameter steuert das seeding von den Pseudo Zufallszahlen-Generator.

2. Ausführen des Experiments. Dadurch können die [Spalten in Dataset auswählen] [ select-columns] und [Aufgeteilten Daten] [ split] Module Spaltendefinition an den Modulen übergeben wir fügen anschließend hinzu.  

3. Um den Algorithmus Learning auszuwählen, erweitern Sie die Kategorie **Erlernen der Computer** in der Palette Modul am linken Rand des Zeichenbereichs ab, und dann **Modell zu initialisieren**. Dadurch wird mehrere Kategorien von Modulen, die zum Initialisieren der Computer Learning Algorithmen verwendet werden können.

    Wählen Sie für dieses Experiments die [Lineare Regressionsformel] [ linear-regression] Modul unter der **Regressionsformel** Kategorie (Sie können auch hier finden Sie das Modul durch Eingabe von "linear Regressionsformel" in das Suchfeld Palette), und ziehen Sie es an die Zeichenbereich Experiments.

4. Suchen und ziehen Sie das [Modell Zug] [ train-model] Modul Experiments hinzugefügt. Schließen Sie den linken input Port in die Ausgabe der die [Lineare Regressionsformel] [ linear-regression] Modul. Schließen Sie den rechten input Port Schulung Daten Ausgabe (linken Port) der [Aufgeteilten Daten] [ split] Modul.

5. Wählen Sie das [Modell Zug] [ train-model] Modul, klicken Sie im **Eigenschaftenbereich** auf **Spalte Datenauswahl zu starten** , und wählen Sie die Spalte **Price** . Dies ist der Wert, den unsere Modell vorhergesagt werden soll.

    ![Wählen Sie die Spalte "Price"][screen7]

6. Ausführen des Experiments.

Das Ergebnis ist ein geschult Regressionsformel-Modell, das verwendet werden kann, um neue Beispiele zum Vorhersagen zu bewerten.

![Anwenden des Computer Learning-Algorithmus][screen8]

## <a name="step-5-predict-new-automobile-prices"></a>Schritt 5: Neue Autohändler Preise Vorhersagen

Nun, da wir das Modell mit 75 Prozent unserer Daten geschulte haben, können wir es verwenden, um andere 25 Prozent der Daten an, wie gut finden Sie unter Punktzahl unsere Modell-Funktionen.

1. Suchen und ziehen Sie das [Modell Score] [ score-model] Modul des Experiments Leinen und schließen Sie den linken input Port in die Ausgabe des [Zug Modell] [ train-model] Modul. Schließen Sie den rechten input Port der Test Daten Ausgabe (rechts Port) der [Aufgeteilten Daten] [ split] Modul.  

    ![Faktor Modell Modul][screen8a]

2. Zum Ausführen des Experiments und zeigen Sie die Ausgabe aus dem [Score Modell] [ score-model] Modul, klicken Sie auf den Port für die Ausgabe, und wählen Sie dann **visualisieren**. Die Ausgabe zeigt die prognostizierten Werte für Preis und die bekannten Werte aus der Testdaten.  

3. Schließlich um die Qualität der Ergebnisse zu testen, wählen Sie Drag & Drop [Bewerten Modell] [ evaluate-model] Modul des Experiments Leinen, und schließen Sie den linken input Port an die Ausgabe des [Score Modell] [ score-model] Modul. (Es gibt zwei input Ports, da das [Modell ausgewertet werden soll] [ evaluate-model] Modul zum Vergleichen von zwei Modelle verwendet werden kann.)

4. Ausführen des Experiments.

Zum Anzeigen der Ausgabe aus dem [Auswerten Modell] [ evaluate-model] Modul, klicken Sie auf den Port für die Ausgabe, und wählen Sie dann **visualisieren**. Für unsere Modell werden die folgenden Statistiken angezeigt:

- **Mittlerer Absolute Fehler** (AUSGEGEBENE): den Mittelwert der absoluten Fehler (ein *Fehler* ist der Unterschied zwischen der prognostizierten Wert und der tatsächlichen Wert).
- **Stamm Mittelwert quadrierter Fehler** (RMSE): die Quadratwurzel von der Durchschnitt von Fehlern im Quadrat Vorhersagen auf das Test-Dataset vorgenommen.
- **Relative Absolute Fehler**: den Mittelwert der absoluten Fehler relativ zu der absoluten Unterschied zwischen Istwerte und den Mittelwert aller tatsächlichen Werte.
- **Relative quadrierter Fehler**: den Mittelwert der quadrierten Fehler relativ zu den quadrierten Unterschied zwischen den tatsächlichen Werten und den Mittelwert aller tatsächlichen Werte.
- **Koeffizient der Bestimmung**: auch bekannt als **R-Quadrat-Wert**, dies ist eine statistische Metrik, der angibt, wie gut ein Modell für die Daten passt.

Für jede des Fehlers ist Statistiken, kleinere besser. Ein kleinerer Wert gibt an, dass die Vorhersagen genauer den tatsächlichen Werten entsprechen. Für **Koeffizient der Bestimmung**, je näher der Wert ist auf einen (1.0), desto besseren Vorhersagen.

![Ergebnisse der Auswertung][screen9]

Der letzte Versuch sollte wie folgt aussehen:

![Computer Learning-Lernprogramm: Abschließen linear Regressionsformel Experiments, das Methoden für Vorhersagen Modellierung verwendet.][screen10]

## <a name="next-steps"></a>Nächste Schritte

Nun, dass Sie einen ersten Computer Learning Lernprogramm abgeschlossen haben und Ihre Experiments eingerichtet haben, können Sie durchlaufen, um zu versuchen, das Modell zu verbessern. Beispielsweise können Sie die Features ändern, die in Ihrer Vorhersage verwendet. Oder ändern Sie die Eigenschaften für die [Lineare Regressionsformel] [ linear-regression] Algorithmus oder einen anderen Algorithmus vollständig zu testen. Sie können selbst erlernen Algorithmen an Ihre Experiments gleichzeitig mehrere Computer hinzufügen und Vergleichen von zwei mithilfe des [Objektmodells ausgewertet werden soll] [ evaluate-model] Modul.

> [AZURE.TIP] Verwenden Sie die **SAVE AS** Schaltfläche unter Experiments Canvas, zum Kopieren von jeder Iteration Ihrer Experiments. Alle Iterationen eines Ihrer Experiments können Sie sehen, indem Sie auf **Ansicht ausführen Verlauf** unter des Zeichenbereichs ab. Finden Sie unter [Manage experimentieren Iterationen in Azure Computer Learning Studio] [ runhistory] für weitere Details.

[runhistory]: machine-learning-manage-experiment-iterations.md

Wenn Sie mit Ihrem Modell zufrieden sind, können Sie es als Webdienst zu verwendende Autohändler Preise Vorhersagen mit neuen Daten bereitstellen. Finden Sie unter [Bereitstellen eines Webdiensts Azure-Computer Learning] [ publish] für weitere Details.

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Vorhersehbare Modellierung Techniken zum Erstellen von mehr umfassend und detailliert eine exemplarische Vorgehensweise, Schulungen, bewerten und Bereitstellen eines Modells finden Sie unter [Entwickeln einer Vorhersage-Lösung mithilfe von Azure-Computer Learning][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[screen1]:./media/machine-learning-create-experiment/screen1.png
[screen1a]:./media/machine-learning-create-experiment/screen1a.png
[screen1b]:./media/machine-learning-create-experiment/screen1b.png
[screen1c]: ./media/machine-learning-create-experiment/screen1c.png
[screen2]:./media/machine-learning-create-experiment/screen2.png
[screen3]:./media/machine-learning-create-experiment/screen3.png
[screen4]:./media/machine-learning-create-experiment/screen4.png
[screen4a]:./media/machine-learning-create-experiment/screen4a.png
[screen5]:./media/machine-learning-create-experiment/screen5.png
[screen6]:./media/machine-learning-create-experiment/screen6.png
[screen7]:./media/machine-learning-create-experiment/screen7.png
[screen8]:./media/machine-learning-create-experiment/screen8.png
[screen8a]:./media/machine-learning-create-experiment/screen8a.png
[screen9]:./media/machine-learning-create-experiment/screen9.png
[screen10]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
