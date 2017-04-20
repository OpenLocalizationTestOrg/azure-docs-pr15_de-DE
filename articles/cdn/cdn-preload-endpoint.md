<properties
    pageTitle="Vorab laden Posten für einen Endpunkt Azure CDN | Microsoft Azure"
    description="Erfahren Sie, wie zwischengespeicherte Inhalte auf einen Endpunkt CDN vorab zu laden."
    services="cdn"
    documentationCenter=""
    authors="camsoper"
    manager="erikre"
    editor=""/>

<tags
    ms.service="cdn"
    ms.workload="tbd"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="07/28/2016"
    ms.author="casoper"/>

# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Anlagen für einen Endpunkt Azure CDN im Voraus zu laden

[AZURE.INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Standardmäßig werden Anlagen zuerst zwischengespeichert, wie angefordert. Dies bedeutet, dass die erste Anforderung aus jeder Region kann länger dauern, da die Rand-Server keine werden der Inhalt Cache und muss dem Ausgangsserver die Anfrage weitergeleitet. Vor dem Laden von Inhalten vermieden werden diese ersten Treffer Wartezeit aus.

Zusätzlich zu einer besseren Customer Experience, kann die vorab geladen Cache Ihre Bestände jederzeit auch Netzwerkdatenverkehr auf dem Ausgangsserver reduzieren.

> [AZURE.NOTE] Vorab geladen Posten eignet sich für große Ereignisse oder Inhalte, die gleichzeitig auf eine große Anzahl von Benutzern, wie etwa einen neuen Film Version oder ein Update verfügbar ist.

In diesem Lernprogramm führt Sie durch die zwischengespeicherte Inhalte auf allen Azure CDN Kante Knoten vorab zu laden.

## <a name="walkthrough"></a>Exemplarische Vorgehensweise

1. Im [Portal Azure](https://portal.azure.com)navigieren Sie zu der CDN Profil mit den Endpunkt, die, den Sie vor dem laden möchten.  Das Profil Blade wird geöffnet.

2. Klicken Sie auf den Endpunkt in der Liste.  Das Endpunkt Blade wird geöffnet.

3. Klicken Sie aus dem CDN Endpunkt Blade auf die Schaltfläche Laden.

    ![CDN Endpunkt blade](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)

    Das Laden Blade wird geöffnet.

    ![CDN laden blade](./media/cdn-preload-endpoint/cdn-load-blade.png)

4. Geben Sie den vollständigen Pfad der einzelnen Ressourcen, die Sie laden möchten (z. B. `/pictures/kitten.png`) in das Textfeld **Pfad** ein.

    > [AZURE.TIP] Weitere **Pfad** Textfelder erscheinen, nach der Eingabe von Text, damit Sie eine Liste mit mehreren Anlagen erstellen können.  Sie können Anlagen aus der Liste löschen, indem Sie auf das Auslassungszeichen (...).
    >
    > Pfade muss eine relative URL, die den folgenden [regulären Ausdruck](https://msdn.microsoft.com/library/az24scfc.aspx)entspricht: `^(?:\/[a-zA-Z0-9-_.\u0020]+)+$`.  Jede Anlage müssen einen eigenen Pfad.  Es gibt keine Platzhalterzeichen Funktionalität für vorab laden Anlagen.

    ![Schaltfläche Laden](./media/cdn-preload-endpoint/cdn-load-paths.png)

5. Klicken Sie auf die Schaltfläche **Laden** .

    ![Schaltfläche Laden](./media/cdn-preload-endpoint/cdn-load-button.png)

> [AZURE.NOTE] Es ist eine Einschränkung der 10 laden Abfragen pro Minute pro CDN Profil ein.

## <a name="see-also"></a>Siehe auch
- [Löschen Sie einen Endpunkt Azure CDN](cdn-purge-endpoint.md)
- [Azure CDN REST-API-Referenz - bereinigen oder vorab laden von außen liegenden Tabellenblättern](https://msdn.microsoft.com/library/mt634451.aspx)
