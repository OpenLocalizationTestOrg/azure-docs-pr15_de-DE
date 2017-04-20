<properties
    pageTitle="Auswählen von Computer Learning Algorithmen | Microsoft Azure"
    description="Wie Erlernen von Azure-Computer Algorithmen für das überwachten und unbeaufsichtigte Learning in clustering, Klassifizierung oder Regressionsformel Versuche auswählen."
    services="machine-learning"
    documentationCenter=""
    authors="brohrer"
    manager="jhubbard"
    editor="cgronlun"
    tags=""/>
    
<tags
    ms.service="machine-learning"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="na"
    ms.workload="data-services"
    ms.date="08/09/2016"
    ms.author="brohrer;garye" />

# <a name="how-to-choose-algorithms-for-microsoft-azure-machine-learning"></a>Algorithmen für Microsoft Azure-Computer Learning auswählen

Die Antwort auf die Frage "Welcher Computertyp erlernen Algorithmus verwendet werden soll?" ist immer "Es hängt ab." Es hängt von der Größe, die Qualität und die Art der Daten. Es hängt davon ab, was Sie mit der Antwort machen möchten. Das hängt davon ab, wie die Math des Algorithmus in Anweisungen für den Computer übersetzt wurde, den Sie verwenden. Es hängt davon ab, und wie viel Zeit Sie haben. Auch die erfahrene Daten Wissenschaftler können nicht feststellen, welcher Algorithmus am besten ausgeführt wird, bevor Sie versuchen, diese.

## <a name="the-machine-learning-algorithm-cheat-sheet"></a>Der Computer Learning-Algorithmus Spickzettel:

Die **Microsoft Azure Computer erlernen Algorithmus Cheat Sheet** hilft Ihnen den rechten Computer erlernen Algorithmus für Vorhersagen Analytics-Lösungen aus der Bibliothek Microsoft Azure-Computer Erlernen der Algorithmen auszuwählen.
Dieser Artikel führt Sie durch die Verwendungsweise.

> [AZURE.NOTE] Zum Herunterladen der Spickzettel:, und erstellen mit diesem Artikel, wechseln Sie zum [Computer Algorithmus Spickzettel: für Microsoft Azure Computer erlernen Studio Lernen](machine-learning-algorithm-cheat-sheet.md).

Dieser Spickzettel: hat eine ganz bestimmte Zielgruppe im Hinterkopf: eine Wissenschaftler im Anfang Daten mit Learning Undergraduate auf Computer, die versuchen, Auswählen eines Algorithmus zu in Azure Computer erlernen Studio. Dies bedeutet, dass einige Generalizations und Oversimplifications macht, aber es wird Sie in einer sicheren Richtung zeigen. Dies bedeutet auch, dass es viele Algorithmen hier nicht aufgeführt gibt. Zunehmender Learning der Azure-Computer einen vollständigeren Satz der verfügbaren Methoden umfassen, fügen wir diese.

Diese Empfehlungen sind kompilierte Feedback und Tipps von viel Daten Wissenschaftler und Computer Learning gestellt. Wir nicht zustimmen, klicken Sie auf Alles, aber ich habe versucht, unsere Ansichten in eine ungefähre Übereinstimmung harmonisiert. Die meisten der Aussagen von darin beginnen, mit "kommt es.."

### <a name="how-to-use-the-cheat-sheet"></a>Gewusst wie: Verwenden der Spickzettel:

Lesen Sie die Pfad und den Algorithmus Beschriftungen im Diagramm als "für * &lt;Pfad Label&gt; * verwenden * &lt;Algorithmus&gt;*." Beispielsweise "verwenden *Geschwindigkeit* *zwei Klasse logistische Regressionsformel*." In einigen Fällen mehr als eine Verzweigung gelten.
Keines der Projekte wird manchmal passt perfekt sein. Sie sind Regel der Ziehpunkt Empfehlungen, damit die genaue wird nicht kümmern werden soll.
Mehrere Daten Wissenschaftler, die, denen ich mit genannten, die gesprochen, besteht die einzige sichere Möglichkeit, erhalten den besten Algorithmus in aller Folien versuchen.

Es folgt ein Beispiel aus der [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) ein Versuch, die verschiedene Algorithmen gegen die gleichen Daten versucht und vergleicht die Ergebnisse: [Vergleichen mit mehreren Klasse Klassifizierern: Buchstabe Spracherkennung](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

>[AZURE.TIP] Herunterladen und Drucken eines Diagramms, das einen Überblick über die Funktionen des Computers Learning Studio bietet, finden Sie unter [Übersichtsdiagramm der Azure-Computer Learning Studio Funktionen](machine-learning-studio-overview-diagram.md).

## <a name="flavors-of-machine-learning"></a>Varianten des Computers learning

### <a name="supervised"></a>Überwacht

Überwachten Learning Algorithmen stellen Vorhersagen basierend auf eine Reihe von Beispielen. Beispielsweise können Aktienverlaufskurse auf Gefahr geraten zukünftige Preisen verwendet werden. Jedes Schulung zum Beispiel wird mit der Bezeichnung und der Wert von Interesse – in diesem Fall den Aktienkurs. Ein überwachten Learning-Algorithmus sucht nach Mustern in diesen Wert Beschriftungen. Sie können alle Informationen, die möglicherweise relevante – den Tag der Woche, die begrenzen, Finanzdaten des Unternehmens, den Typ der Branche, das Vorhandensein von Ereignissen störende Geopolicitical – und jeder Algorithmus für unterschiedliche Muster aussieht. Nachdem der Algorithmus das beste Muster gefunden hat kann, wird das Muster Vorhersagen für unbeschriftete Testdaten – morgen Preise.

Dies ist eine beliebte und nützliche Art von Learning Computer. Mit einer Ausnahme sind alle Module beim Erlernen der Azure-Computer überwacht erlernen Algorithmen. Es gibt mehrere bestimmte Arten von überwachten Learning, die in Azure Computer erlernen dargestellt werden: Klassifizierung Regressionsformel und Anomalie Erkennung.

* **Klassifizierung**. Wenn die Daten zu eine Kategorie Vorhersagen verwendet werden, steht überwachten Learning Klassifikation. Dies ist die Groß-/Kleinschreibung beim Zuweisen eines Bilds als ein Bild des "Cat" oder ein "Dog". Wenn nur zwei Auswahlmöglichkeiten vorhanden sind, wird dies **zwei-Klasse** oder **Binomialverteilung Klassifizierung**aufgerufen. Wenn als weitere Kategorien, sind bei der die ausgezeichnet NCAA März Madness Turnier Vorhersage, wird dieses Problem als **Multi-Klasse Klassifizierung**bezeichnet.

* **Regressionsformel**. Wenn ein Wert, wie mit vordefinierten Preise vorhergesagt werden wird, wird die überwachten Learning Regressionsformel aufgerufen.

* **Normalbetriebswerte**. Manchmal ist das Ziel von Datenpunkten zu identifizieren, die einfach ungewöhnliche sind. Betrug-Erkennung sind Verlusts beispielsweise keine Ausgaben ungewöhnlich Kreditkarte-Muster. Die möglichen Variationen sind also zahlreiche und die Schulung Beispiele so wenig, dass es nicht möglich, erfahren, welche Betrug sieht folgendermaßen aus. Der Ansatz, den Normalbetriebswerte akzeptiert besteht darin, einfach Hier erfahren, welche normale Aktivität aussieht (mit einem Verlauf-Betrug Transaktionen) und identifizieren alle Werte, die deutlich abweicht.

### <a name="unsupervised"></a>Unbeaufsichtigte

Unbeaufsichtigte lernen wurde von Datenpunkten keine Etiketten zugeordnet. Stattdessen wird das Ziel eines Algorithmus unbeaufsichtigte lernen, die Daten in irgendeiner Weise organisieren oder seine Struktur zu beschreiben. Dies kann bedeuten gruppieren zu Clustern oder suchen auf unterschiedliche Weise komplexe Daten betrachten, sodass sie einfacher oder übersichtlicher angezeigt wird.

### <a name="reinforcement-learning"></a>Ausbau learning

In Verstärkung erlernen Ruft den Algorithmus zum Auswählen einer Aktion als Antwort auf jedem Datenpunkt ab. Der Algorithmus Learning empfängt auch eine Belohnung Signal ein kurzes Zeitformat später, der angibt, wie gut die Entscheidung wurde.
Anhand dieser ändert der Algorithmus seine Strategie, um die höchsten Belohnung zu erzielen. Derzeit sind keine Verstärkung erlernen Algorithmus Module beim Erlernen der Azure-Computer. Ausbau Lernen ist häufig in Robotics, wobei der Satz von Sensorwerte zu einem bestimmten Zeitpunkt einen Datenpunkt und der Algorithmus muss den Robot nächste Aktion auswählen. Es ist außerdem, dass eine interne für das Internet der Dinge Applications angepasst wird.

## <a name="considerations-when-choosing-an-algorithm"></a>Aspekte bei der Auswahl eines Algorithmus

### <a name="accuracy"></a>Genauigkeit

Erste die genaueste Antwort möglich ist nicht immer erforderlich.
In einigen Fällen ist ein Näherungswert ausreichend, je nachdem, was Sie ihn verwenden möchten. Wenn dies der Fall ist, können Sie Ihre Verarbeitungszeit erheblich durch Verwenden von mehr ungefähren Methoden cut sein. Ein weiterer Vorteil von weitere ungefähren Methoden ist, dass sie in der vertrauten Regel [overfitting](https://youtu.be/DQWI1kvmwRg)zu vermeiden.

### <a name="training-time"></a>Schulung Zeit

Die Anzahl der Minuten oder Stunden, die erforderlich sind, um ein Modell zu schulen variiert viel zwischen Algorithmen. Schulung Zeit ist häufig eng mit Genauigkeit – eine der anderen in der Regel begleitet. Darüber hinaus sind einige Algorithmen vertrauliche auf die Anzahl der Datenpunkte als andere.
Beim Zeit beschränkt ist kann es insbesondere dann, wenn das DataSet groß ist die Wahl des Algorithmus, steuern.

### <a name="linearity"></a>Linearität

Stellen Sie viele Computer Learning Algorithmen Linearität verwenden. Linear Klassifizierung Algorithmen wird davon ausgegangen, dass Klassen von einer geraden Linie (oder dessen höhere dimensionale analoge) getrennt werden können. Dazu gehört logistische Regressionsformel und Vektor Computern (gemäß der Implementierung in Azure-Computer Learning) zu unterstützen.
Linear Regressionsformel Algorithmen wird vorausgesetzt, dass Datentrends einer geraden Linie folgt. Diese Annahmen nicht schlecht für einige Probleme sind, jedoch auf andere schalten sie Genauigkeit nach unten.

![Bounday nicht linear-Klasse][1]

***Nicht linear Klasse Grenze*** *-auf eine lineare Klassifizierung Algorithmus Genauigkeit ergibt*

![Daten mit einer nichtlinearen trend][2]

***Daten mit einer nichtlinearen trend*** *– mithilfe einer Regressionsformel linear-Methode erzeugt viel größere Fehler als erforderlich*

Trotz ihrer Gefahren werden lineare Algorithmen sehr häufig als erste Linie-Angriff. Sie sind normalerweise über einen Algorithmus einfach und schnell zu schulen.

### <a name="number-of-parameters"></a>Anzahl von Parametern

Parameter sind die Regler, die ein Wissenschaftler Daten Ruft ab, um beim Einrichten eines Algorithmus zu aktivieren. Zahlen, die Auswirkung auf das Verhalten des Algorithmus, wie die Fehlertoleranz oder Anzahl von Iterationen oder Optionen zwischen Varianten des Verhaltens des Algorithmus sind. Die Zeit und die Genauigkeit des Algorithmus können mitunter ganz einfach die richtigen Einstellungen abrufen vertrauliche sein. Algorithmen mit großen Anzahl Parameter erfordern in der Regel die meisten ausprobieren, erhalten eine gute Kombination aus.

Alternativ ist ein [Parameter ziehen](machine-learning-algorithm-parameters-optimize.md) Modul-Block in Azure-Computer lernen, die automatisch alle sind die Parameterkombinationen mit beliebigen Granularität versucht gewählte vorhanden. Obwohl dies eine hervorragende Möglichkeit zum sicherstellen, dass Sie den Parameter Speicherplatz erstreckt haben ist, erhöht der Zeitaufwand für ein Modell zu schulen wesentlich mit der Anzahl der Parameter.

Der Vorteil ist jedoch, dass viele Parameter in der Regel gibt an, dass ein Algorithmus größere Flexibilität. Sie können eine sehr gute Genauigkeit häufig erzielen. Vorausgesetzt, dass Sie die richtige Kombination von Einstellungen für die Parameter feststellen können.

### <a name="number-of-features"></a>Anzahl von features

Für bestimmte Datentypen, die Anzahl der Features sehr große möglicherweise im Vergleich zu der Anzahl von Datenpunkten. Dies ist häufig die Groß-/Kleinschreibung mit Genetik oder Textdaten. Große Anzahl von Features kann einige Learning-Algorithmen, Schulung unfeasibly lange Zeit tätigen Einbußen. Unterstützung Vektor Computern eignen sich besonders gut für diese Anfrage (siehe unten).

### <a name="special-cases"></a>Sonderfälle

Einige Algorithmen Learning von bestimmten Annahmen über die Struktur der Daten oder die gewünschten Ergebnisse. Wenn Sie einen, die Ihren Anforderungen entspricht finden können, vermitteln es nützliche Ergebnisse, genauere Vorhersagen oder schnelleres Schulung.

|**Algorithmus**|**Genauigkeit**|**Schulung Zeit**|**Linearität**|**Parameter**|**Notizen**|
|---|:---:|:---:|:---:|:---:|---|
|**Zwei-Klasse Klassifikation**| | | | | |
|[logistische Regressionsformel](https://msdn.microsoft.com/library/azure/dn905994.aspx)                    | |●|●|5| |
|[Entscheidung-Gesamtstruktur](https://msdn.microsoft.com/library/azure/dn906008.aspx)|●|○| |6| |
|[Entscheidung Dschungel](https://msdn.microsoft.com/library/azure/dn905976.aspx)|●|○| |6|Geringer Speicherbedarf|
|[unterstützter Entscheidungsstruktur](https://msdn.microsoft.com/library/azure/dn906025.aspx)|●|○| |6|Große Speicherbedarf|
|[neurales Netzwerk](https://msdn.microsoft.com/library/azure/dn905947.aspx)|●| | |9|[Weitere Anpassungen ist möglich](http://go.microsoft.com/fwlink/?LinkId=402867)|
|[Die durchschnittliche perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx)|○|○|●|4| |
|[Unterstützung Vektor Computer](https://msdn.microsoft.com/library/azure/dn905835.aspx)| |○|●|5|Gut für große Featuregruppen|
|[lokal umfassende Unterstützung Vektor Computer](https://msdn.microsoft.com/library/azure/dn913070.aspx)|○| | |8|Gut für große Featuregruppen|
|[Bayes Punkt-Computer](https://msdn.microsoft.com/library/azure/dn905930.aspx)| |○|●|3| |
|**Klassifizierung Multi-Klasse**| | | | | |
|[logistische Regressionsformel](https://msdn.microsoft.com/library/azure/dn905853.aspx)| |●|●|5| |
|[Entscheidung Gesamtstruktur](https://msdn.microsoft.com/library/azure/dn906015.aspx)|●|○| |6| |
|[Dschungel Entscheidung](https://msdn.microsoft.com/library/azure/dn905963.aspx)|●|○| |6|Geringer Speicherbedarf|
|[neurales Netzwerk](https://msdn.microsoft.com/library/azure/dn906030.aspx)|●| | |9|[Weitere Anpassungen ist möglich](http://go.microsoft.com/fwlink/?LinkId=402867)|
|[1 – V – alle](https://msdn.microsoft.com/library/azure/dn905887.aspx)|-|-|-|-|Finden Sie unter Eigenschaften der ausgewählten zwei-Klasse-Methode|
|**Regressionsformel**| | | | | |
|[Linear](https://msdn.microsoft.com/library/azure/dn905978.aspx)| |●|●|4| |
|[Linear Bayes'sche](https://msdn.microsoft.com/library/azure/dn906022.aspx)| |○|●|2| |
|[Entscheidung-Gesamtstruktur](https://msdn.microsoft.com/library/azure/dn905862.aspx)|●|○| |6| |
|[unterstützter Entscheidungsstruktur](https://msdn.microsoft.com/library/azure/dn905801.aspx)|●|○| |5|Große Speicherbedarf|
|[fast-Gesamtstruktur quantile](https://msdn.microsoft.com/library/azure/dn913093.aspx)|●|○| |9|Verteilung statt der Point Vorhersagen|
|[neurales Netzwerk](https://msdn.microsoft.com/library/azure/dn905924.aspx)|●| | |9|[Weitere Anpassungen ist möglich](http://go.microsoft.com/fwlink/?LinkId=402867)|
|[POISSON](https://msdn.microsoft.com/library/azure/dn905988.aspx)| | |●|5|Technisch gesehen Log-linear. Für die Vorhersage zählt|
|[Ordinal](https://msdn.microsoft.com/library/azure/dn906029.aspx)| | | |0|Für die Vorhersage Rang-Sortierung|
|**Normalbetriebswerte**| | | | | |
|[Unterstützung Vektor Computer](https://msdn.microsoft.com/library/azure/dn913103.aspx)|○|○| |2|Besonders gut für große Featuregruppen|
|[PCA-basierte Normalbetriebswerte](https://msdn.microsoft.com/library/azure/dn913102.aspx)| |○|●|3| |
|[K-Mittel](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/)| |○|●|4|Clustering-Algorithmus|


**Algorithmus-Eigenschaften:**

**●** - zeigt ausgezeichnete Genauigkeit, wie oft schnelle Schulung und die Verwendung von Linearität

**○** - zeigt eine gute Genauigkeit und Moderater Zeiten

## <a name="algorithm-notes"></a>Algorithmus Notizen

### <a name="linear-regression"></a>Linear Regressionsformel

Wie bereits erwähnt, passt [linear Regressionsformel](https://msdn.microsoft.com/library/azure/dn905978.aspx) eine Zeile (oder Ebene oder Hyperplane) an das DataSet. Es ist eine leistungsfähige, einfach und schnell, aber möglicherweise übermäßig vereinfachte für einige Probleme.
Aktivieren Sie dieses Kontrollkästchen für eine [lineare Regressionsformel Lernprogramm](machine-learning-linear-regression-in-azure.md).

![Daten und-Objekte mit einen trend][3]

***Daten und-Objekte mit einen trend***

### <a name="logistic-regression"></a>Logistische Regressionsformel

Obwohl es verwirrend "Regressionsformel" im Namen enthält, ist logistische Regressionsformel tatsächlich einem überzeugenden Werkzeug für [zwei-Klasse](https://msdn.microsoft.com/library/azure/dn905994.aspx) und [Multiclass](https://msdn.microsoft.com/library/azure/dn905853.aspx) Klassifikation. Es ist schnell und einfach. Die Tatsache, mit deren Hilfe ein des '-geformten Kurve anstelle einer geraden Linie erleichtert ideal für Daten in Gruppen unterteilen. Logistische Regressionsformel bietet lineare Klasse Grenzen stellen bei, Verwendung so sicher, dass eine lineare Annäherung ist, den Sie mit live können.

![Logistische Regressionsformel auf Daten mit nur einem Feature zwei-Klasse][4]

***Eine logistische Regressionsformel auf Daten mit nur einem Feature zwei-Klasse*** *-die Klasse Grenze ist der Punkt, an dem die logistische Kurve wie ungefähr beide Klassen wird*

### <a name="trees-forests-and-jungles"></a>Strukturen, Gesamtstrukturen und jungles

Entscheidung Gesamtstrukturen ([Regressionsformel](https://msdn.microsoft.com/library/azure/dn905862.aspx) [zwei-Klasse](https://msdn.microsoft.com/library/azure/dn906008.aspx)und [Multiclass](https://msdn.microsoft.com/library/azure/dn906015.aspx)) Entscheidung Jungles ([zwei-Klasse](https://msdn.microsoft.com/library/azure/dn905976.aspx) und [Multiclass](https://msdn.microsoft.com/library/azure/dn905963.aspx)) und unterstützter Entscheidungsstrukturen ([Regressionsformel](https://msdn.microsoft.com/library/azure/dn905801.aspx) und [zwei Klasse](https://msdn.microsoft.com/library/azure/dn906025.aspx)) alle Entscheidungsstrukturen für die eines grundlegenden Computers erlernen Konzept basieren auf. Es gibt viele Varianten von Entscheidungsstrukturen, allerdings dann dasselbe – das Feature Leerzeichen in Regionen mit dieser Bezeichnung zumeist unterteilen. Diese kann Bereiche konsistent Kategorie oder eines konstanten Wertes, je nachdem, ob Sie Klassifizierung oder Regressionsformel durchführen.

![Entscheidungsstruktur unterteilt Abstandweite feature][5]

***Eine Entscheidungsstruktur unterteilt Abstandweite Feature in Bereiche der ungefähr einheitliche Werte***

Da ein Feature Leerzeichen willkürlich kleine Bereiche unterteilt werden kann, es ist einfach, angenommen Inhaltsmengen haben einen Datenpunkt pro Region fein genug – ein extreme Beispiel Overfitting. Um dies zu vermeiden, eine große Gruppe von Strukturen werden erstellt besondere mathematische sorgfältig durchgeführt, dass die Strukturen nicht korreliert werden. Der Mittelwert der Gesamtstruktur"Entscheidung" ist eine Struktur, die Overfitting vermieden werden. Entscheidung Gesamtstrukturen können sehr viel Speicher. Entscheidung Jungles sind eine Variante, die weniger Speicherplatz auf eine etwas längere Zeit Schulung Kosten werden genutzt.

Unterstützter Entscheidungsstruktur vermeiden Overfitting durch beschränken, wie oft sie unterteilen können und wie einige Datenpunkte in jeder Region zulässig sind. Der Algorithmus erstellt eine Folge von Strukturen, von die jedes lernen kompensieren für den Fehler, um die Struktur vor nach links. Das Ergebnis ist eine sehr präzise Teilnehmern, die viel Speicher verwendet wird. Checken Sie die Beschreibung des vollständigen technischen [Friedmans ursprünglichen Papier](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Fast-Gesamtstruktur Quantile Regressionsformel](https://msdn.microsoft.com/library/azure/dn913093.aspx) ist eine Variante der Entscheidungsstrukturen für die Sonderfall, wo Sie nicht nur den normalen () Median der Daten in einem Bereich, sondern auch die Verteilung in Form von Quantiles wissen möchten.

### <a name="neural-networks-and-perceptrons"></a>Neurales Netzwerke und perceptrons

Neurales Netzwerke sind Brain-Design Algorithmen [Multiclass](https://msdn.microsoft.com/library/azure/dn906030.aspx), [zwei-Klasse](https://msdn.microsoft.com/library/azure/dn905947.aspx)und [Regressionsformel](https://msdn.microsoft.com/library/azure/dn905924.aspx) Probleme zu lernen. Es gibt eine unendliche Vielfalt an der neurales Netzwerke in Azure-Computer Learning des Formulars der gerichtete acyclische Diagramme sind jedoch. Die bedeutet, dass input Features vorwärts (niemals nach hinten) über eine Folge von Ebenen übergeben werden vor in Ausgaben aktiviert wird. In jeder Ebene sind Eingaben in verschiedenen Kombinationen gewichteten, summiert und an die nächste Ebene übergeben. Die Möglichkeit, anspruchsvolle Klasse Beschränkungen und Daten Trends scheinbar von magische Hier erfahren, erzeugt diese Kombination von einfacher Berechnungen. N-layered Netzwerke dieser Art führen Sie das Tiefe "Learning", das weniger Tech Center für Berichte und Sciencefiction Festbrennstoffen.

Diese hohe Leistung stammen nicht kostenlos, obwohl. Neurales Netzwerke können über einen längeren Zeitraum zu schulen, besonders für große Datenmengen mit vielen Features nutzen. Sie können zudem mehr Parameter als die meisten Algorithmen, was bedeutet, dass der Parameter ziehen die Schulung Zeit viel erweitert.
Und mögliche Werte für diese Overachievers, die [ihre eigenen Netzwerkstruktur](http://go.microsoft.com/fwlink/?LinkId=402867)angeben möchten, sind produktivsten.

<a name="boundaries-learned-by-neural-networks6"></a>![Grenzen von neurales Networks Erfahrungen][6]
---------------------------

***Die Grenzen von neurales Networks Erfahrungen können komplexe und übernommen wurden und überzählige sein.***

Die [zwei-Klasse durchschnittlich Perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) ist neurales Netzwerke Antwort auf starke Zunahme bei Zeiten. Es wird eine Netzwerkstruktur, die linear Grenzen bietet verwendet. Es ist fast primitiven der heutigen Standards, aber es wurde eine lange Geschichte robust arbeiten und klein genug, um schnell zu erlernen ist.

### <a name="svms"></a>SVMs

Unterstützung Vektor Computern (SVMs) Hier finden Sie die Grenze, die als breit einen Rand möglichst Klassen von trennt. Wenn zwei Klassen nicht eindeutig getrennt werden können, finden die Algorithmen die beste Grenze, den, die Sie können. Wie in Azure-Computer Learning geschrieben, wird die [zwei-Klasse SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) mit nur einer geraden Linie. (In SVM sprechen verwendet er einen linearen Kernel.) Da es linear weicht ernannt werden, ist es können ziemlich schnell ausgeführt. Feature-intensiver Daten, wie Text oder Genomische ist, in dem sie das beste. In diesen Fällen können SVMs Klassen schneller und mit weniger Overfitting als die meisten anderen Algorithmen zusätzlich zum Anfordern nur eines geringen Anteil Arbeitsspeicher zu trennen.

![Unterstützung Vektor Computer Klasse Grenze][7]

***Eine typische Unterstützung Vektor Computer Klasse Grenze maximiert den Trennen von zwei Klassen Rand***

Ein anderes Produkt von Microsoft Research, die [lokal Tiefe SVM zwei-Klasse](https://msdn.microsoft.com/library/azure/dn913070.aspx) ist eine nichtlinearen Variante von SVM, die meisten der Geschwindigkeit und Effizienz der lineare Version behält. Es eignet sich ideal für Fälle, in dem der lineare Ansatz präzise genug Antworten mitteilen nicht. Die Entwickler von gehalten, es fast Überwindung das Problem in einer Reihe von kleineren linear SVM Probleme. Lesen Sie die [vollständige Beschreibung](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) für die Details auf, wie sie dies zu erreichen abgerufen.

Mit der Erweiterung raffinierte der nonlinear SVMs, zeichnet der [1-Klasse SVM](https://msdn.microsoft.com/library/azure/dn913103.aspx) eine Grenze, die das gesamte Dataset eng erläutert. Dies ist nützlich für Normalbetriebswerte. Neue Datenpunkte, die weitaus außerhalb dieser Grenze liegen werden ungewöhnlich erwähnenswerte sein.

### <a name="bayesian-methods"></a>Bayes-Methoden

Bayes'sche Methoden sind sehr wünschenswert verfügbar: vermeiden Sie Overfitting. Dazu müssen sie einige Annahmen über die wahrscheinlich Verteilung der Antwort im voraus. Eine andere Nebenprodukt dieses Ansatzes ist, dass sie nur wenige Parameter besitzen. Azure-Computer-Learning hat beide Bayes-Algorithmen für das Klassifizierung ([zwei-Klasse Bayes Punkt-Computer](https://msdn.microsoft.com/library/azure/dn905930.aspx)) und Regressionsformel ([linear Regressionsformel Bayes'sche](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Beachten Sie, dass diese wird davon ausgegangen, dass die Daten Teilen oder mit einer geraden Linie angepasst werden können.

Auf einer zurückliegenden Notiz entwickelt wurden, Bayes Punkt Computern bei Microsoft Research. Sie verfügen über einige außergewöhnlich designter theoretischen Arbeit dahinter. Das Interesse Student wird auf den [ursprünglichen Artikel in JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) und eine [nützliche Blog von Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx)weitergeleitet.

### <a name="specialized-algorithms"></a>Spezielle Algorithmen

Wenn Sie ein bestimmtes Ziel haben möglicherweise Sie Glück. Innerhalb der Azure-Computer Learning-Auflistung stehen Algorithmen an, die in Rank Vorhersage ([ordinal Regressionsformel](https://msdn.microsoft.com/library/azure/dn906029.aspx)), Count Vorhersage ([Poisson Regressionsformel](https://msdn.microsoft.com/library/azure/dn905988.aspx)) und Normalbetriebswerte (eine basierend auf [Hauptkomponenten Analyse](https://msdn.microsoft.com/library/azure/dn913102.aspx) und eine auf Grundlage von s [Vektor Computer unterstützen](https://msdn.microsoft.com/library/azure/dn913103.aspx)) specialize.
Und ein einzige clustering-Algorithmus sowie ([K-Mittel](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/)) vorhanden ist.

![PCA-basierte Normalbetriebswerte][8]

***PCA-basierte Normalbetriebswerte*** *– der Großteil der Daten in eine stereotypischen Verteilung; Punkt abweichen erheblich aus, dass Verteilergruppen sind Verlusts fällt*

![DataSet gruppiert mit K-Mittel][9]

***Ein Dataset ist in 5-Cluster mit K Mitteln gruppiert.***

Es gibt auch eine Ensemble [One V alle multiclass Klassifizierung](https://msdn.microsoft.com/library/azure/dn905887.aspx), der das N-Klasse Klassifizierung Problem in N-1 zwei-Klasse Klassifizierung Probleme unterteilt. Die Genauigkeit, Schulung Zeit und Linearität Eigenschaften ergeben sich zwei-Klasse Klassifizierer verwendet.

![Zwei-Klasse Klassifizierern kombiniert, um eine Klassifizierung drei-Klasse bilden.][10]

***Ein Paar von zwei-Klasse Klassifizierern kombinieren, um eine drei-Klasse Klassifizierung bilden***

Erlernen von Azure Computer enthält auch den Zugriff auf eine leistungsstarke Computer Learning Framework unter dem Titel des [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
Angabe definiert Kategorisierung hier, da es Probleme bei der Klassifizierung und Regressionsformel informieren kann und kann sogar lernen Sie von teilweise unbeschriftete Daten. Sie können sie eine Anzahl von erlernen Algorithmen, Verlust Funktionen und Optimierungsalgorithmen verwenden konfigurieren. Es wurde von Grund auf neu entwickelt effiziente, parallel und sehr schnell sein. Er verarbeitet übertrieben hohen Featuregruppen mit minimalem Aufwand deutlich.
Gestartet und von Microsoft Research des eigenen John Langford geführt hat, ist Angabe einer Formel ein Eintrag in einem Feld Stock Car Algorithmen. Nicht jedes Problem passt Angabe, wenn Ihnen der Fall ist, es kann jedoch sein Wert an der Lernprozess an der Schnittstelle steigen. Es ist auch als [eigenständige open-Source-Code](https://github.com/JohnLangford/vowpal_wabbit) in mehreren Sprachen verfügbar.


<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
