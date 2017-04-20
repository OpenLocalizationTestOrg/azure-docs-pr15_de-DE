<properties
    pageTitle="Azure Active Directory B2C: Page UI Anpassung Helper Tool | Microsoft Azure"
    description="Ein Helper-Tool verwendet, um die Seite Benutzeroberfläche Anpassungsfeature in Azure Active Directory B2C veranschaulichen."
    services="active-directory-b2c"
    documentationCenter=""
    authors="swkrish"
    manager="mbaldwin"
    editor="bryanla"/>

<tags
    ms.service="active-directory-b2c"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="07/22/2016"
    ms.author="swkrish"/>

# <a name="azure-active-directory-b2c-a-helper-tool-used-to-demonstrate-the-page-user-interface-ui-customization-feature"></a>Azure Active Directory B2C: Ein Helper-Tool verwendet, um die Seite Benutzer Benutzeroberflächen-Anpassungsfeature zu veranschaulichen

In diesem Artikel ist eine Ergänzung zum im [Hauptfenster Benutzeroberfläche Anpassung Artikel](active-directory-b2c-reference-ui-customization.md) in B2C Azure Active Directory (Azure AD). Die folgenden Schritte beschreiben, wie Übung Feature für die Anpassung der Benutzeroberfläche der Seite mit der Stichprobe HTML- und CSS-Inhalten, die wir zur Verfügung gestellt haben.

## <a name="get-an-azure-ad-b2c-tenant"></a>Abrufen von einem Mandanten Azure AD B2C

Bevor Sie nichts anpassen können, müssen Sie zu [einem B2C von Azure AD-Mandanten erhalten](active-directory-b2c-get-started.md) , wenn Sie eine bereits besitzen.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Erstellen einer Richtlinie Anmeldung oder Anmeldung

Der Beispieltext wir haben bereitgestellt werden kann, Customze zwei Seiten einer [Anmeldung oder Anmeldung Richtlinie](active-directory-b2c-reference-policies.md): der [einheitliche Anmeldeseite](active-directory-b2c-reference-ui-customization.md) und die [Seite Attribute selbst bestätigt](active-directory-b2c-reference-ui-customization.md). Wenn [die Richtlinie Anmelde oder Anmeldung erstellen](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), fügen Sie lokales Konto (e-Mail-Adresse), Facebook, Google und Microsoft als **Identitätsanbieter**hinzu. Hierbei handelt es sich um die einzige IDPs, die unsere Stichprobe HTML-Inhalt akzeptieren.  Sie können auch eine Teilmenge der folgenden IDPs hinzufügen, wenn Sie möchten.

## <a name="register-an-application"></a>Registrieren einer Anwendung

Um eine Anwendung zu [Registrieren](active-directory-b2c-app-registration.md) müssen in Ihrem Mandanten B2C, die mit die Richtlinie ausgeführt werden können. Nach dem Registrieren der Anwendungs, müssen Sie einige Optionen, mit denen Sie Ihre Anmelde Richtlinie tatsächlich ausführen:

- Erstellen Sie eine der Azure AD B2C Schnellstart Applications im Abschnitt "Erste Schritte" aufgeführt [Melden Sie sich nach oben, und melden Sie sich in Ihrer Anwendung Nutzer](active-directory-b2c-overview.md#getting-started).
- Mithilfe der vordefinierten [Azure AD B2C Umgebung](https://aadb2cplayground.azurewebsites.net) Anwendungs. Wenn Sie die Umgebung verwenden, müssen Sie eine Anwendung registrieren, in Ihrem B2C-Mandanten mit der **URI umleiten** `https://aadb2cplayground.azurewebsites.net/`.
- Verwenden Sie die Schaltfläche **Jetzt ausführen** auf die Richtlinie im [Azure-Portal](https://portal.azure.com/)an.

## <a name="customize-your-policy"></a>Passen Sie Ihrer Richtlinie an

Um das Aussehen und Verhalten Ihrer Richtlinie anpassen möchten, müssen Sie zuerst HTML- und CSS-Dateien mit den bestimmten Konventionen der Azure AD B2C erstellen. Sie können dann Ihre statischen Inhalt zu einer öffentlich zugänglichen Stelle hochladen, sodass Azure AD B2C darauf zugreifen können. Eigene dedizierte Webserver, Azure BLOB-Speicher, Azure Content Delivery Network oder einem anderen statischen Ressource-hosting Anbieter möglicherweise. Die einzigen Anforderungen sind, dass Ihre Inhalte über HTTPS steht und mithilfe von CORS zugegriffen werden kann. Nachdem Sie Ihre statischen Inhalt im Internet verfügbar gemacht haben, können Sie die Richtlinie, um zu diesem Speicherort zeigen und zu präsentieren, dass der Inhalt an Ihre Kunden bearbeiten. Im [Hauptfenster Benutzeroberfläche Anpassung Artikel](active-directory-b2c-reference-ui-customization.md) wird ausführlich beschrieben wie das Feature Azure AD B2C Anpassung funktioniert.

Im Sinne dieses Lernprogramms haben wir bereits einige Stichprobe Inhalte erstellt und gehostet wird es auf Azure BLOB-Speicher. Der Inhalt der Stichprobe ist eine sehr einfache Anpassung im Design unsere fiktives Unternehmen, "Absatzzahlen". Wenn Sie in Ihrer eigenen Richtlinie ausprobieren, gehen Sie folgendermaßen vor:

1. Melden Sie sich bei Ihrem Mandanten in [Azure-Portal](https://portal.azure.com/) , und navigieren Sie zu dem B2C Features Blade.
2. Klicken Sie auf **Anmeldung oder Anmeldung Richtlinien** , und klicken Sie dann auf die Richtlinie (beispielsweise "b2c\_1\_melden Sie sich\_von\_melden Sie sich\_in").
3. Klicken Sie auf **Seite Benutzeroberfläche Anpassung** , und klicken Sie dann **einheitliche Anmeldung oder Anmeldung Seite**.
4. Bringen Sie den Schalter **verwenden benutzerdefinierte Seite** auf **Ja**. Geben Sie im Feld **benutzerdefinierte Seite URI** `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Klicken Sie auf **OK**.
5. Klicken Sie auf **lokale Anmeldung Kontoseite**. Bringen Sie den Schalter **benutzerdefinierte Vorlage verwenden** , auf **Ja**. Geben Sie im Feld **benutzerdefinierte Seite URI** `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
5. Wiederholen Sie den gleichen Schritt für die **Anmeldeseite für soziale Netzwerke Konto**ein.
 Klicken Sie auf **OK** , zweimal, um die Benutzeroberfläche Anpassung Blades zu schließen.
6. Klicken Sie auf **Speichern**.

Nun können Sie die angepasste Richtlinie ausprobieren. Sie können Ihre eigene Anwendung der Azure AD B2C-Umgebung verwenden oder wenn soll, Sie können jedoch auch einfach auf den Befehl **Jetzt ausführen** , in der Richtlinie Blade. Wählen Sie im Dropdownmenü Ihrer Anwendung aus, und wählen Sie die entsprechende Umleitung URI. Klicken Sie auf die Schaltfläche **jetzt ausführen** . Eine neue Browserregisterkarte wird geöffnet und ausgeführt werden kann, bis der Benutzerfunktionalität eines anmelden für eine Anwendung durch den neuen Inhalt direkte!

## <a name="upload-the-sample-content-to-azure-blob-storage"></a>Hochladen des Stichprobe Inhalts zu Azure BLOB-Speicher

Ausführliche Azure BLOB-Speicher verwenden, um den Seiteninhalt Ihrer zu hosten, können Sie eigene Speicher-Konto erstellen und verwenden unsere B2C Helper-Tool zum Hochladen von Dateien.

### <a name="create-a-storage-account"></a>Erstellen Sie ein Speicherkonto

1. Melden Sie sich mit dem [Azure-Portal](https://portal.azure.com/)aus.
2. Klicken Sie auf **+ neue** > **Daten + Speicher** > **Speicher-Konto**. Sie benötigen ein Azure-Abonnement zum Erstellen eines Kontos Azure BLOB-Speicher. Sie können sich bei der [Website Azure](https://azure.microsoft.com/pricing/free-trial/)kostenlose Testversion anmelden.
3. Geben Sie einen **Namen** für das Speicherkonto (beispielsweise "Contoso"), und wählen Sie die entsprechende Auswahl für **Preise Ebene**, **Ressourcengruppe** und **Abonnement**aus. Stellen Sie sicher, dass Sie die **Pin zum Startboard** Option aktiviert haben. Klicken Sie auf **Erstellen**.
4. Kehren Sie zu der Startboard, und klicken Sie auf Speicherkonto, das Sie soeben erstellt haben.
5. Klicken Sie im Abschnitt " **Zusammenfassung** " auf **Container**, und klicken Sie dann auf **+ Hinzufügen**.
6. Geben Sie einen **Namen** für den Container (beispielsweise "b2c"), und wählen Sie **Blob** als den **Typ von Access**. Klicken Sie auf **OK**.
7. Container, den Sie erstellt haben, wird in der Liste auf das Blade **Blobs** angezeigt. Notieren Sie sich die URL des Containers; Angenommen, sie sollte folgendermaßen aussehen `https://contoso.blob.core.windows.net/b2c`. Schließen Sie das Blade **Blobs** .
8. Klicken Sie auf das Konto Blade Speicher klicken Sie auf die **Tasten** , und notieren Sie die Werte für die Felder **Speicher Kontonamen** und **Access-Primärschlüssel** .

1. Melden Sie sich mit dem [Azure-Portal](https://portal.azure.com/)aus.
2. Klicken Sie auf **+ neue** > **Daten + Speicher** > **Speicher-Konto**. Sie benötigen ein Azure-Abonnement zum Erstellen eines Kontos Azure BLOB-Speicher. Sie können sich bei der [Website Azure](https://azure.microsoft.com/pricing/free-trial/)kostenlose Testversion anmelden.
3. Wählen Sie **Blob-Speicher** unter **Art von Konto**aus, und lassen Sie die anderen Werte als Standard.  Bei Bedarf können Sie die Ressourcengruppe und Speicherort bearbeiten.  Klicken Sie auf **Erstellen**.
4. Kehren Sie zu der Startboard, und klicken Sie auf Speicherkonto, das Sie soeben erstellt haben.
5. Klicken Sie im Abschnitt **Zusammenfassung** auf **+ Container**.
6. Geben Sie einen **Namen** für den Container (beispielsweise "b2c"), und wählen Sie **Blob** als den **Typ von Access**. Klicken Sie auf **OK**.
7. Öffnen Sie die Container **Eigenschaften**, und notieren Sie die URL des Containers; Angenommen, sie sollte folgendermaßen aussehen `https://contoso.blob.core.windows.net/b2c`. Schließen Sie das Blade Container.
8. Klicken Sie auf das Konto Blade Speicher klicken Sie auf das **Symbol der Schlüssel** , und notieren Sie die Werte für die Felder **Speicher Kontonamen** und **Access-Primärschlüssel** .

> [AZURE.NOTE]
    **Access-Primärschlüssel** ist eine wichtige Sicherheitsanmeldeinformationen.

### <a name="download-the-helper-tool-and-sample-files"></a>Herunterladen der Hilfsdateien Dateitool und einer Stichprobe

Sie können die [Azure BLOB-Speicher Helper Werkzeug und Dateien als ZIP-Datei](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) herunterladen oder Klonen Sie es aus GitHub:

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Dieses Repository enthält eine `sample_templates\wingtip` Verzeichnis, das Beispiel HTML, CSS und Bilder enthält. Für diese Vorlagen auf Ihr eigenes Konto Azure BLOB-Speicher verweisen müssen Sie die HTML-Dateien zu bearbeiten. Open `unified.html` und `selfasserted.html` und Ersetzen Sie alle Instanzen von `https://localhost` durch die URL der eigenen Container, die Sie in den vorherigen Schritten notiert. Sie müssen den absoluten Pfad der HTML-Dateien verwenden, da in diesem Fall der HTML-Code Azure AD, unter der Domäne realisiert werden wird `https://login.microsoftonline.com`.

### <a name="upload-the-sample-files"></a>Hochladen der Beispieldateien

In der gleichen Repository Entzippen Sie ihn `B2CAzureStorageClient.zip` und Ausführen der `B2CAzureStorageClient.exe` innerhalb der Datei. Dieses Programm wird einfach hochladen aller Dateien im Verzeichnis, das Sie sich bei Ihrem Speicherkonto angeben und CORS Zugriff für diese Dateien aktivieren. Wenn Sie die oben aufgeführten Schritte ausgeführt haben, werden die HTML- und CSS-Dateien jetzt bei Ihrem Speicherkonto zeigen. Beachten Sie, dass der Name Ihres Kontos Speicher das Webpart, das vorausgeht `blob.core.windows.net`; beispielsweise `contoso`. Sie können überprüfen, ob der Inhalt ordnungsgemäß hochgeladen wurde, indem Sie versuchen, für den Zugriff auf `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` in einem Browser. Auch verwenden Sie [http://test-cors.org/](http://test-cors.org/) , um sicherzustellen, dass der Inhalt jetzt CORS aktiviert ist. (Suchen Sie nach "XHR Status: 200" im Ergebnis.)

### <a name="customize-your-policy-again"></a>Passen Sie die Richtlinie, erneut

Jetzt, da Sie den Inhalt der Stichprobe zu Ihrem Speicherkonto hochgeladen haben, müssen Sie die Anmelde Richtlinie aus, um darauf verweisen bearbeiten. Wiederholen Sie die Schritte aus dem Abschnitt ["Anpassen Ihrer Richtlinie"](#customize-your-policy) oben, diesmal URLs Ihrer eigenen Speicher-Konto verwenden. Beispielsweise den Speicherort der Ihre `unified.html` Datei wäre `<url-of-your-container>/wingtip/unified.html`.

Jetzt können Sie die Schaltfläche **Jetzt ausführen** oder Ihre eigene Anwendung die Richtlinie erneut auszuführenden verwenden. Das Ergebnis sollte fast genau gleich aussehen – Sie verwendet dieselbe HTML und CSS in beiden Fällen hören. Jedoch Ihre Richtlinien sind jetzt verweisen auf eine eigene Instanz der Azure BLOB-Speicher, und Sie sind kostenlos, bearbeiten und die Dateien wieder als Sie bitte hochladen. Weitere Informationen zum Anpassen der HTML und CSS finden Sie im [Hauptfenster Benutzeroberfläche Anpassung Artikel](active-directory-b2c-reference-ui-customization.md).
