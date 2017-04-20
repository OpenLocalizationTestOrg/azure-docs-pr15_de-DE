<properties
    pageTitle="Generator-Dateitypen und Modell Qualität: Empfehlungen API | Microsoft Azure"
    description="Azure Computer Learning Empfehlungen – Schnellstarthandbuch"
    services="cognitive-services"
    documentationCenter=""
    authors="luiscabrer"
    manager="jhubbard"
    editor="cgronlun"/>

<tags
    ms.service="cognitive-services"
    ms.workload="data-services"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/20/2016"
    ms.author="luisca"/>

#  <a name="build-types-and-model-quality"></a>Dateitypen und Modell Qualität zu erstellen #

<a name="TypeofBuilds"></a>
## <a name="supported-build-types"></a>Generator unterstützte Dateitypen ##

Die Empfehlungen-API unterstützt derzeit zwei Arten von Build: *Empfehlungen* und *FBT*. Jede basiert auf unterschiedliche Algorithmen, und jedes unterschiedliche Vorteile hat. Dieses Dokument beschreibt die einzelnen Builds und Techniken für die Qualität der generiert Modelle vergleichen.

Wenn Sie nicht bereits getan haben, empfehlen wir, dass Sie der [Schnellstartübersicht](cognitive-services-recommendations-quick-start.md)abgeschlossen haben.

<a name="RecommendationBuild"></a>
### <a name="recommendation-build-type"></a>Empfehlungen-Generator-Datentyp ###

Der Typ der Empfehlungen-Generator verwendet Matrix Factorization um Empfehlungen zu ermöglichen. Es [latente Feature](https://en.wikipedia.org/wiki/Latent_variable) Vektoren basierend auf Ihre Transaktionen beschreiben Sie jedes Element generiert und anschließend diese latenten Vektoren verwendet, um Elemente zu vergleichen, die ähnliche sind.

Wenn Sie basierte auf Verkäufen in Ihrem Geschäft Modell Schulen und ein Telefon Lumia 650 als Eingabe für das Modell angeben, wird das Modell eine Reihe von Elemente zurück, die von Personen erworben werden, für die wahrscheinlich ein Telefon Lumia 650 kaufen werden in der Regel. Die Elemente möglicherweise nicht Komplement. In diesem Beispiel ist es möglich, dass das Modell andere Telefone zurückgeben, da die Personen, die die Lumia 650 wie andere Telefone zufrieden sind möglicherweise.

Die Empfehlungen-Generator weist zwei Funktionen, die sie attraktiver vornehmen:

* *Unterstützt die Empfehlungen-Generator *kalt Element* Platzierung **

Elemente, die keine wesentlichen Verwendung haben, werden kalt Elemente bezeichnet. Wenn Sie eine Lieferung von einem Telefon, die, denen Sie vor dem nie verkauft haben erhalten, kann nicht das System beispielsweise Empfehlungen für dieses Produkt auf Transaktionen alleine abgeleitet. Dies bedeutet, dass das System von Informationen über das Produkt selbst lernen soll.

Wenn Sie Platzierung kalt Element verwenden möchten, müssen Sie Informationen der Features für jede Ihrer Elemente im Katalog bereitzustellen. Folgendes wird (Notiz Schlüssel = Wert-Format für die Features) die ersten Zeilen des Katalogs aussehen können.

>6CX-00001, einbinden Pro2, Oberflächen-, geben Sie = Hardware, Speicher = 128 GB Arbeitsspeicher = 4G, Hersteller = Microsoft

>73H-00013, Aktivierung Xbox 360, Spiele,, Typ = Software, Language = Englisch, Bewertung = Reifen

>WAH-0F05, Minecraft Xbox 360, Spiele,, * Typ = Software, Language = Spanisch, Bewertung Jugend =

Sie müssen auch die folgenden Buildparameter festlegen:

| Parameter erstellen         | Notizen
|------------------     |-----------
|*useFeaturesInModel*     | Legen Sie auf **true**.  Zeigt an, ob das Modell Empfehlungen verbessern Funktionen verwendet werden können.
|*allowColdItemPlacement*   | Legen Sie auf **true**. Zeigt an, ob die Empfehlungen kalt Elemente auch über Features Ähnlichkeit Pushbenachrichtigungen sollte.
| *modelingFeatureList*   | Durch Trennzeichen getrennte Liste der Featurenamen empfohlen verbessern die eigene Empfehlungen verwendet werden. Beispielsweise "Sprache, Speicher" für das vorherige Beispiel.

**Der Build Empfehlungen unterstützt Benutzer Empfehlungen**

Ein Empfehlungen-Generator unterstützt [Benutzer Empfehlungen](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/56f30d77eda5650db055a3dd). Dies bedeutet, dass es individuelle Empfehlungen für Benutzer auf Grundlage ihrer Transaktion Verläufe bereitgestellt werden. Für Benutzer Empfehlungen stellt Sie die Benutzer-ID oder des letzten Verlaufs von Transaktionen für diesen Benutzer bereit.

Eine klassisches Beispiel, in denen Sie Benutzer Empfehlungen anwenden sollten bei der Anmeldung auf der Seite Willkommen ist. Es können Sie Inhalt heraufstufen, die für den Benutzer bestimmte gilt.

Möglicherweise möchten Sie auch einen Empfehlungen erstellen Typ anwenden, wenn der Benutzer gerade Auschecken. An diesem Punkt, stehen Ihnen die Liste der Elemente, die der Benutzer kaufen, und können Sie Empfehlungen basierend auf der aktuellen Markt Korb bereitstellen.

#### <a name="recommendations-build-parameters"></a>Empfehlungen erstellen Parameter

| Namen  |   Beschreibung |    Geben Sie ein, <br>  Gültige Werte <br> (Standardwert)
|-------|-------------------|------------------
| *NumberOfModelIterations* |   Die Anzahl der Iterationen, die das Modell führt, wird durch die Gesamtzeit berechnen und die Genauigkeit Modell wiedergegeben. Je höher der Wert, desto genauer das Modell, aber die Zeit berechnen dauert länger.  |   Ganze Zahl, <br>  10 bis 50 <br>(40)
| *NumberOfModelDimensions* |   Die Anzahl der Dimensionen bezieht sich auf die Anzahl der Features, die das Modell versucht, zu den Daten zu suchen. Erhöhen der Anzahl von Dimensionen ermöglicht besser Feinabstimmung der Ergebnisse in kleinere Cluster. Allerdings werden zu viele Dimensionen Modell verhindern Korrelationen zwischen Elementen suchen. |  Ganze Zahl, <br> 10 bis 40 <br>(20) |
| *ItemCutOffLowerBound* |  Definiert die Mindestanzahl der Verwendung Punkte, die ein Element befinden soll, damit er als Teil des Modells gilt. |        Ganze Zahl, <br> 2 oder mehr <br> (2) |
| *ItemCutOffUpperBound* |  Definiert die maximale Anzahl der Verwendung Punkte, die ein Element befinden soll, damit er als Teil des Modells gilt. |  Ganze Zahl, <br>2 oder mehr<br> (2147483647) |
|*UserCutOffLowerBound* |   Definiert die minimale Anzahl von Transaktionen, die ein Benutzer muss durchgeführt haben, Teil des Modells berücksichtigt werden müssen. | Ganze Zahl, <br> 2 oder mehr <br> (2)
| *UserCutOffUpperBound* |  Definiert die maximale Anzahl von Transaktionen, die ein Benutzer muss durchgeführt haben, Teil des Modells berücksichtigt werden müssen. | Ganze Zahl, <br>2 oder mehr <br> (2147483647)|
| *UseFeaturesInModel* |    Zeigt an, ob Features zum Optimieren des Modells Empfehlungen verwendet werden können. |     Boolesch<br> Standard: WAHR
|*ModelingFeatureList* |    Durch Trennzeichen getrennte Liste der Featurenamen empfohlen verbessern die eigene Empfehlungen verwendet werden. Das hängt von den Features, die wichtig sind. |    Eine Zeichenfolge, bis zu 512 Zeichen
| *AllowColdItemPlacement* |    Zeigt an, ob die Empfehlungen kalt Elemente auch über Features Ähnlichkeit Pushbenachrichtigungen sollte. | Boolesch <br> Standard: falsch
| *EnableFeatureCorrelation*    | Zeigt an, ob in Logik Funktionen verwendet werden können. | Boolesch <br> Standard: falsch
| *ReasoningFeatureList* |  Durch Trennzeichen getrennte Liste der Featurenamen für Schlussfolgerungen Sätze, z. B. Empfehlungen erläuterungen verwendet werden soll. Das hängt von den Features, die für Kunden wichtig sind. | Eine Zeichenfolge, bis zu 512 Zeichen
| *EnableU2I* | Aktivieren von individuellen Empfehlungen, auch als Benutzer, um das Element (U2I) Empfehlungen bezeichnet. | Boolesch <br>Standard: WAHR
|*EnableModelingInsights* | Definiert, ob offline Auswertung zusammenbringen Modellierung Einsichten (d. h., Genauigkeit und Vielfalt Kennzahlen) ausgeführt werden soll. Wenn true wird eine Teilmenge der Daten nicht für Schulung, da es zum Testen des Modells reserviert werden benötigen verwendet werden soll. Weitere Informationen zum [Testen der offline](#OfflineEvaluation). | Boolesch <br> Standard: falsch
| *SplitterStrategy* | Wenn modeling Einsichten aktivieren auf *true*festgelegt ist, ist dies an, wie Daten Testzwecken geteilt werden soll.  | Zeichenfolge, die *RandomSplitter* oder *LastEventSplitter* <br>Standard: RandomSplitter


<a name="FBTBuild"></a>
### <a name="fbt-build-type"></a>FBT erstellen Typ ###

Die häufig gekauft nicht trennen (FBT) erstellen wird eine Analyse, die zählt, wie oft, die zwei oder drei unterschiedliche Produkte zur gemeinsamen zusammen auftreten. Es wird die Datensätze basierend auf einer Ähnlichkeit-Funktion (**gemeinsame Vorkommen**, **Jaccard**, **heben Sie**) sortiert.

Stellen Sie sich **Jaccard** , und **heben Sie** als Möglichkeiten, die gemeinsame Vorkommen standardisiert werden soll.  Dies bedeutet, dass die Elemente zurückgegeben werden nur dann, wenn sie wo zusammen mit dem Element Startwert gekauft.

In diesem Beispiel Lumia 650 Telefon wird Telefon X zurückgegeben werden nur, wenn Sie in der gleichen Sitzung als Lumia 650 Telefon Telefon X erworben haben. Da dies wahrscheinlich nicht sein kann, erwarten wir Elemente Ergänzung zu den Lumia 650 zurückgegeben werden soll; beispielsweise ein IRM-Schutz Bildschirm oder einer Power Netzwerkadapter für die 650 Lumia.

Zwei Elemente beachtet derzeit in der gleichen Sitzung erworben werden, wenn sie in einer Transaktion mit den gleichen Benutzer-ID und den Zeitstempel auftreten.

FBT Builds unterstützen keine kalt Elemente, da per Definition erwarten zwei Elemente in derselben Transaktion erworben werden. Während FBT Builds Sätze von Elementen (Dreiergruppen) zurückgeben können, unterstützen sie keine individuelle Empfehlungen, da sie annehmen, dass ein einzelnes Startwert Element als Eingabe.


#### <a name="fbt-build-parameters"></a>FBT erstellen Parameter

| Namen  |   Beschreibung |       Geben Sie ein,  <br> Gültige Werte <br> (Standardwert)
|-------|---------------|-----------------------
| *FbtSupportThreshold* | Wie vorsichtig ist das Modell. Die Anzahl der gemeinsamen Vorkommen von Elementen für die Modellierung berücksichtigt werden. |  Ganze Zahl, <br> 3-50 <br> (6)
| *FbtMaxItemSetSize* | Umschließt die Anzahl der Elemente in einer Gruppe von häufig verwendeten an.| Ganze Zahl  <br> 2-3 <br> (2)
| *FbtMinimalScore* | Minimale Punktzahl, die ein häufig verwendeten Satz sein soll, in die zurückgegebenen Ergebnisse aufgenommen werden sollen. Je höher, desto besser. | Double <br> 0 und höher <br> (0)
| *FbtSimilarityFunction* | Definiert die Ähnlichkeit Funktion vom Build verwendet werden. **Heben Sie** Serendipity bevorzugt, **gemeinsame Vorkommen** bevorzugt Vorhersagbarkeit und **Jaccard** ist eine Kompromisse zwischen den beiden. | Zeichenfolge,  <br>  <i>Cooccurrence, heben Sie, jaccard</i><br> Standard: <i>jaccard</i>

<a name="SelectBuild"></a>
## <a name="build-evaluation-and-selection"></a>Bewertung und Auswahl zu erstellen ##

In diesem Handbuch möglicherweise Ihnen helfen festzustellen, ob Sie eine Empfehlungen erstellen oder eine FBT erstellen verwenden, aber es eine endgültige Antwort in Fällen bietet, wo Sie sie verwenden eines konnte, nicht. Darüber hinaus auch, wenn Sie wissen, dass Sie eine FBT erstellen verwenden möchten, möchten Sie weiterhin **Jaccard** oder **heben Sie** , wie die Ähnlichkeit Funktion auswählen.

Auswählen zwischen zwei unterschiedliche Versionen am besten testen sie in der Praxis (Bewertung online) und eine Konvertierung Abschlag (Disagio) unterschiedlichen Versionen nachverfolgen. Die Konvertierung Rate konnte basierend auf Empfehlungen Klicks gemessen werden, die tatsächliche Anzahl von Empfehlungen angezeigt oder sogar auf die tatsächliche Beträge Einkäufe, wenn die anderen Empfehlungen angezeigt wurden. Sie können Ihre Konvertierung Zins Metrik anhand Ihrer Business Ziel auswählen.

In einigen Fällen können Sie das Modell offline zu evaluieren, bevor Sie ihn in der Herstellung einfügen möchten. Während der Auswertung offline kein Ersatz für die Bewertung online ist, kann es als Metrik dienen.

<a name="OfflineEvaluation"></a>
## <a name="offline-evaluation"></a>Offline-Bewertung  ##

Das Ziel einer Auswertung offline ist Vorhersagen Genauigkeit (die Anzahl der Benutzer, die eine empfohlene Elemente zu kaufen) und der Vielfalt von Empfehlungen (die Anzahl der Elemente, die vorgeschlagen werden).
Als Teil der Genauigkeit und Vielfalt Kennzahlen Auswertung, das System sucht nach einer Stichprobe von Benutzern und teilt die Transaktionen für diese Benutzer in zwei Gruppen: Schulung Dataset und das Test-Dataset.

> [AZURE.NOTE]Wenn Sie offline Kennzahlen verwenden möchten, müssen Sie werden in den Verwendungsdaten verfügen.
> Zeitdaten ist richtig zwischen Schulung und Testen Datasets Verwendung Teilen erforderlich.

> Darüber hinaus kann offline Bewertung nicht Ergebnissen für kleine Verwendung Dateien führen. Für die Bewertung sorgfältige, sein sollten mindestens 1.000 Verwendung Punkte im Dataset testen.

<a name="Precision"></a>
### <a name="precision-at-k"></a>Genauigkeit bei-k ###
In der folgenden Tabelle stellt die Ausgabe der Genauigkeit bei k offline Auswertung dar.

| K | 1 | 2 | 3 |   4 |     5
|---|---|---|---|---|---|
|Prozentsatz |   13,75 | 18.04   | 21 |  24.31 | 26.61
|Benutzer in testen |    10.000 |    10.000 |    10.000 |    10.000 |    10.000
|Benutzer betrachtet | 10.000 |    10.000 |    10.000 |    10.000 |    10.000
|Benutzer, die nicht berücksichtigt. | 0 | 0 | 0 | 0 | 0

#### <a name="k"></a>K
In der obigen Tabelle darstellt *k* die Anzahl von Empfehlungen an den Kunden dargestellt. Die Tabelle lautet wie folgt: "Wenn während des Testzeitraums nur eine Empfehlungen für den Kunden angezeigt wurde, die Benutzer nur 13,75 würde erworben haben die Empfehlungen." Diese Anweisung basiert auf der Annahme, dass das Modell mit Daten erwerben gelernt wurde. Eine weitere Möglichkeit, dies zu sagen ist, dass die Genauigkeit bei 1 13,75 liegt.

Beachten Sie, wie an den Kunden Weitere Elemente angezeigt werden, die Wahrscheinlichkeit für den Kunden erwerben einer empfohlene Element nach oben wechselt. Für das vorherige experimentieren verdoppelt die Wahrscheinlichkeit fast auf 26.61 %, wenn 5 Elemente vorgeschlagen werden.

#### <a name="percentage"></a>Prozentsatz
Der Prozentsatz der Benutzer, die mit mindestens einem *k* empfohlenen interagiert wird angezeigt. Der Prozentwert wird durch Dividieren der Anzahl der Benutzer, die mindestens ein Empfehlungen ein interaktives durch die Gesamtzahl der Benutzer betrachtet berechnet. Benutzer betrachtet Weitere Informationen finden Sie unter.

#### <a name="users-in-test"></a>Benutzer in testen
Daten in dieser Zeile stellt die Gesamtanzahl der Benutzer im Dataset testen.

#### <a name="users-considered"></a>Benutzer betrachtet
Ein Benutzer gilt nur dann, wenn das System mindestens empfohlen *k* Elemente basierend auf dem Modell mit Schulung Dataset generiert.

#### <a name="users-not-considered"></a>Benutzer, die nicht berücksichtigt.
Daten in dieser Zeile steht für alle Benutzer, die nicht berücksichtigt. Benutzer, die nicht mindestens erhalten haben *k* Elemente empfohlen.

Benutzer, die nicht als = Benutzer in Test – Benutzer betrachtet

<a name="Diversity"></a>
### <a name="diversity"></a>Vielfalt ###
Kennzahlen Vielfalt messen den Typ der Elemente empfohlen. In der folgenden Tabelle stellt die Ausgabe der Vielfalt offline Auswertung dar.

|Quantil Periode |    0-90|  90-99| 99-100
|------------------|--------|-------|---------
|Prozentsatz        | 34.258 | 55.127| 10.615


Gesamte Elemente empfohlen: 100,000

Eindeutige Elemente empfohlen: 954

#### <a name="percentile-buckets"></a>Quantil buckets
Jede Zelle Quantil wird durch eine Spanne (Mindest- und Höchstwerte, den Bereich zwischen 0 und 100) dargestellt. Die Elemente in der Nähe 100 beliebteste Elemente, und die Elemente in der Nähe 0 sind mindestens beliebte. Z. B. ist der Prozentwert für die Zelle 99-100 %-Quantil 10.6, bedeutet, dass 10.6 Prozent empfohlenen nur die oberen davon Beliebteste Elemente zurückgegeben. Das Quantil Periode Minimalwert (einschließlich) ist, und der maximale Wert ist ausschließlich, eine Ausnahme bilden jedoch 100.
#### <a name="unique-items-recommended"></a>Eindeutige Elemente empfohlen
Eindeutige Elemente empfohlen Metrik zeigt die Anzahl der unterschiedlichen Elemente, die für die Auswertung zurückgegeben wurden.
#### <a name="total-items-recommended"></a>Empfohlene Elemente (gesamt)
Die Gesamtzahl der Artikel empfohlen Metrisch die Anzahl von Elementen empfohlen angezeigt. Möglicherweise einige Duplikate ein.

<a name="ImplementingEvaluation"></a>
### <a name="offline-evaluation-metrics"></a>Offline Auswertung Kennzahlen ###
Die Genauigkeit und Vielfalt offline Metrik sein hilfreich bei der Auswahl von welchem Build zu verwenden. Erstellen Sie zur Erstellungszeit als Teil der jeweiligen FBT oder Empfehlungen Parameter ein:

-   Legen Sie den *EnableModelingInsights* -Generator-Parameter auf **true**.
-   Aktivieren Sie gegebenenfalls den *SplitterStrategy* (entweder *RandomSplitter* oder *LastEventSplitter*).
*RandomSplitter* teilt die Verwendungsdaten im Zug und Testen legt basierend auf der angegebenen *RandomSplitterParameters* Test % und zufällige Werte Startwert.
*LastEventSplitter* teilt die Verwendungsdaten im Zug und Sätze basierend auf der letzten Transaktion für jeden Benutzer zu testen.

Dadurch wird einen Build ausgelöst, der nur eine Teilmenge der Daten für Schulung und die restlichen Daten zur verwendet um Auswertung Kennzahlen zu berechnen.  Nach Abschluss der erstellen, müssen die Ausgabe der Auswertung, erhalten Sie aufrufen, der [Get-Generator Kennzahlen-API](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0/operations/577eaa75eda565095421666f)und den entsprechenden *ModelId* sowie *BuildId*übergeben.

 Im folgenden sehen die JSON-Ausgabe für die Bewertung der Stichprobe.


    {
     "Result": {
     "precisionItemRecommend": null,
     "precisionUserRecommend": {
      "precisionMetrics": [
        {
          "k": 1,
          "percentage": 13.75,
          "usersInTest": 10000,
          "usersConsidered": 10000,
          "usersNotConsidered": 0
        },
        {
          "k": 2,
          "percentage": 18.04,
          "usersInTest": 10000,
          "usersConsidered": 10000,
          "usersNotConsidered": 0
        },
        {
          "k": 3,
          "percentage": 21.0,
          "usersInTest": 10000,
          "usersConsidered": 10000,
          "usersNotConsidered": 0
        },
        {
          "k": 4,
          "percentage": 24.31,
          "usersInTest": 10000,
          "usersConsidered": 10000,
          "usersNotConsidered": 0
        },
        {
          "k": 5,
          "percentage": 26.61,
          "usersInTest": 10000,
          "usersConsidered": 10000,
          "usersNotConsidered": 0
        }
      ],
      "error": null
    },
    "diversityItemRecommend": null,
    "diversityUserRecommend": {
      "percentileBuckets": [
        {
          "min": 0,
          "max": 90,
          "percentage": 34.258
        },
        {
          "min": 90,
          "max": 99,
          "percentage": 55.127
        },
        {
          "min": 99,
          "max": 100,
          "percentage": 10.615
        }
      ],
      "totalItemsRecommended": 100000,
      "uniqueItemsRecommended": 954,
      "uniqueItemsInTrainSet": null,
      "error": null
      }
     },
    "Id": 1,
    "Exception": null,
    "Status": 5,
    "IsCanceled": false,
    "IsCompleted": true,
    "CreationOptions": 0,
    "AsyncState": null,
    "IsFaulted": false
    }
