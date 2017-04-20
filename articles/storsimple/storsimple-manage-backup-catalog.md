<properties 
   pageTitle="Verwalten Ihrer StorSimple Sicherung Katalog | Microsoft Azure"
   description="Verwendung die StorSimple Manager Sicherungskatalog Seite in der Liste auswählen, und löschen zusätzliche Datensätze für einen Datenträger erläutert."
   services="storsimple"
   documentationCenter="NA"
   authors="SharS"
   manager="carmonm"
   editor="" />
<tags 
   ms.service="storsimple"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="TBD"
   ms.date="04/28/2016"
   ms.author="v-sharos" />

# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a>Verwenden Sie zum Verwalten Ihrer Sicherung Katalogs des StorSimple Manager-Diensts

## <a name="overview"></a>(Übersicht)

Die Seite StorSimple Manager **Sicherungskatalog** zeigt die Sicherung Datensätze, die erstellt werden, wenn Sie manuelle oder geplante Sicherungskopien geöffnet werden. Sie können mithilfe dieser Seite können die Liste alle Sicherungskopien für eine Sicherung Richtlinie oder einen Datenträger, aktivieren oder Löschen von Sicherungskopien, oder verwenden eine Sicherungskopie, wiederherstellen oder einen Datenträger klonen.

In diesem Lernprogramm wird erläutert, wie Liste auswählen, und löschen eine Sicherungskopie festlegen. Wechseln Sie zu [Stellen Sie Ihr Gerät aus einer Sicherung wieder her](storsimple-restore-from-backup-set.md), um weitere Informationen zum Wiederherstellen von Ihrem Geräts aus einer Sicherung. Informationen zu einem Volume klonen, wechseln Sie zu [Datenbeschriftungsreihe ein StorSimple Volume](storsimple-clone-volume.md).

![Zusätzliche Katalog](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Die Seite **Sicherungskatalog** enthält, dass eine Abfrage, um die Sicherung einschränken Auswahl festgelegt. Sie können die Sicherung Datensätze filtern, die abgerufen werden, basierend auf den folgenden Parametern:

- **Gerät** – das Gerät, an dem die Sicherung erstellt wurde.

- **Zusätzliche Richtlinie oder Volumen** – die Sicherung Richtlinie oder Lautstärke mit diesen Sicherung Datensatz verknüpft ist.

- **Aus** – Datums- und Zeitbereich, wenn die Sicherungsdatei Menge erstellt wurde.

Die gefilterten zusätzliche Datensätze werden dann tabellarisch angeordnet basierend auf den folgenden Attributen:

- **Name** – den Namen der Sicherungsdatei Richtlinie oder Volumen zugeordnet Sicherung festlegen.

- **Größe** – die Größe des Sicherung festlegen.

- **Erstellt am** – Datum und Uhrzeit, wann die Sicherungskopien erstellt wurden. 

- **Typ** – Sicherung Datensätze können lokale Momentaufnahmen oder Momentaufnahmen cloud. Eine lokale Momentaufnahme ist eine Sicherungskopie der alle auf dem Gerät, lokal gespeicherte Lautstärke Daten an, während eine Momentaufnahme der Cloud auf die Sicherung von Volumendaten in der Cloud verweist. Lokale Momentaufnahmen bieten schnelleren Zugriff wohingegen Cloud Momentaufnahmen für Daten Stabilität ausgewählt sind.

- **Initiiert von** – die Sicherungen automatisch über einen Zeitplan oder manuell durch einen Benutzer initiiert werden können. Eine Sicherung Richtlinie können Sie Sicherungskopien planen. Alternativ können Sie die Option **Sicherung ausführen** , eine manuelle Sicherung ausführen.

## <a name="list-backup-sets-for-a-volume"></a>Liste Sicherung legt für einen Datenträger
 
Führen Sie die folgenden Schritte aus, um alle Sicherungskopien für einen Datenträger aufzulisten.

#### <a name="to-list-backup-sets"></a>Liste Sicherung Gruppen

1. Klicken Sie auf der Seite StorSimple Manager Dienst auf der Registerkarte **Sicherungskatalog** .

2. Filtern Sie die Auswahlmöglichkeiten wie folgt ein:

    1. Wählen Sie das entsprechende Gerät aus.

    2. Wählen Sie in der Dropdown-Liste ein Volume das entsprechende Sicherungskopien der anzeigen aus.

    3. Geben Sie den Zeitraum an.

    4. Klicken Sie auf das Symbol "Überprüfen" ![Kontrollkästchen-Symbol](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) zum Ausführen dieser Abfrage.
 
    In der Liste der Sätze Sicherung sollten die Sicherungskopien der ausgewählten Lautstärke zugeordnet angezeigt.

## <a name="select-a-backup-set"></a>Wählen Sie eine Sicherungskopie

Führen Sie die folgenden Schritte aus, um eine Sicherung einrichten für ein Volume oder eine Sicherungskopie Richtlinie auszuwählen.

#### <a name="to-select-a-backup-set"></a>Auswählen eine Sicherung Gruppe

1. Klicken Sie auf der Seite StorSimple Manager Dienst auf der Registerkarte **Sicherungskatalog** .

2. Filtern Sie die Auswahlmöglichkeiten wie folgt ein:

    1. Wählen Sie das entsprechende Gerät aus.

    2. Wählen Sie in der Dropdown-Liste die Richtlinie Volumen oder Sicherung für die Sicherung, die Sie auswählen möchten.

    3. Geben Sie den Zeitraum an.

    4. Klicken Sie auf das Symbol "Überprüfen" ![Kontrollkästchen-Symbol](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) zum Ausführen dieser Abfrage.

    Die Sicherungskopien zugeordnet das ausgewählte Volume oder zusätzliche Richtlinie sollte angezeigt werden, in der Liste der Sätze Sicherung.

3. Wählen Sie aus, und blenden Sie eine Sicherung festlegen. Die Optionen zum **Wiederherstellen** und **Löschen** , werden am unteren Rand der Seite angezeigt. Sie können eine der folgenden Aktionen in der Sicherungskopie durchführen, die Sie ausgewählt haben.

## <a name="delete-a-backup-set"></a>Löschen einer Sicherung Menge

Löschen Sie eine Sicherungskopie, wenn Sie nicht mehr mit verknüpften Daten beibehalten möchten. Führen Sie die folgenden Schritte aus, um eine Sicherung zu löschen.

#### <a name="to-delete-a-backup-set"></a>So löschen Sie eine Sicherungskopie festlegen

1. Klicken Sie auf der Seite StorSimple Manager-Dienst auf der **Registerkarte Sicherungskatalog**.

2. Filtern Sie die Auswahlmöglichkeiten wie folgt ein:

    1. Wählen Sie das entsprechende Gerät aus.

    2. Wählen Sie in der Dropdown-Liste die Richtlinie Volumen oder Sicherung für die Sicherung, die Sie auswählen möchten.

    3. Geben Sie den Zeitraum an.

    4. Klicken Sie auf das Symbol "Überprüfen" ![Kontrollkästchen-Symbol](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) zum Ausführen dieser Abfrage.

    Die Sicherungskopien zugeordnet das ausgewählte Volume oder zusätzliche Richtlinie sollte angezeigt werden, in der Liste der Sätze Sicherung.

3. Wählen Sie aus, und blenden Sie eine Sicherung festlegen. Die Optionen zum **Wiederherstellen** und **Löschen** , werden am unteren Rand der Seite angezeigt. Klicken Sie auf **Löschen**.

4. Sie werden benachrichtigt, wenn der Löschvorgang ist in den Fortschritt und wann sie erfolgreich abgeschlossen ist. Nachdem der Löschvorgang abgeschlossen ist, aktualisieren Sie die Abfrage auf dieser Seite. Die gelöschte Sicherung Menge wird in der Liste der Sätze Sicherung nicht mehr angezeigt.

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie, wie [den Sicherung Katalog zum Wiederherstellen von Ihrem Geräts aus einer Sicherung verwendet](storsimple-restore-from-backup-set.md).

- Erfahren Sie, wie Sie [den Dienst StorSimple Manager zum Verwalten von Ihrem Geräts StorSimple verwenden](storsimple-manager-service-administration.md).
