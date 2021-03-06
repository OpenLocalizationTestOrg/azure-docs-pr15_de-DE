<properties 
    pageTitle="Lernprogramm: Azure-Active Directory-Integration in Mimecast-Verwaltungskonsole | Microsoft Azure" 
    description="Erfahren Sie, wie mit Mimecast-Verwaltungskonsole mit Azure Active Directory einmaliges Anmelden, automatisierte Bereitstellung und mehr aktiviert!" 
    services="active-directory" 
    authors="jeevansd"  
    documentationCenter="na" 
    manager="femila"/>
<tags 
    ms.service="active-directory" 
    ms.devlang="na" 
    ms.topic="article" 
    ms.tgt_pltfrm="na" 
    ms.workload="identity" 
    ms.date="09/29/2016" 
    ms.author="jeedes" />

#<a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Lernprogramm: Azure-Active Directory-Integration in Mimecast-Verwaltungskonsole
  
Das Ziel dieses Lernprogramms ist die Integration von Azure und Mimecast-Verwaltungskonsole anzeigen.  
Das in diesem Lernprogramm beschriebenen Szenario wird davon ausgegangen, dass Sie die folgenden Elemente bereits:

-   Ein gültiges Azure-Abonnement
-   Eine Mimecast-Verwaltungskonsole einmaliges Anmelden aktiviert Abonnement
  
Am Ende dieses Lernprogramms, werden die Azure AD-Benutzer, die Sie Mimecast-Verwaltungskonsole zugewiesen haben können einzelne melden Sie sich bei der Anwendung an der Verwaltungskonsole Mimecast Firmenwebsite (Service Provider initiiert signieren auf), oder verwenden die [Einführung in die Access-Systemsteuerung](active-directory-saas-access-panel-introduction.md).
  
In diesem Lernprogramm beschriebenen Szenario umfasst die folgenden Bausteine erforderlich:

1.  Aktivieren die Anwendungsintegration für Mimecast-Verwaltungskonsole
2.  Konfigurieren einmaliges Anmelden
3.  Konfigurieren der Benutzer bereitgestellt
4.  Zuweisen von Benutzern

![Szenario] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795008.png "Szenario")
##<a name="enabling-the-application-integration-for-mimecast-admin-console"></a>Aktivieren die Anwendungsintegration für Mimecast-Verwaltungskonsole
  
Das Ziel der in diesem Abschnitt ist zu gliedernden wie die Anwendungsintegration für Mimecast-Verwaltungskonsole aktiviert.

###<a name="to-enable-the-application-integration-for-mimecast-admin-console-perform-the-following-steps"></a>Führen Sie zum Aktivieren der Anwendungsintegration für Mimecast-Verwaltungskonsole die folgenden Schritte aus:

1.  Klicken Sie im Azure klassischen-Portal auf der linken Navigationsbereich auf **Active Directory**.

    ![Active Directory] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC700993.png "Active Directory")

2.  Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3.  Klicken Sie zum Öffnen der Anwendungsansicht in der Verzeichnisansicht im oberen Menü auf **Applications** .

    ![Applikationen] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC700994.png "Applikationen")

4.  Klicken Sie auf **Hinzufügen** , am unteren Rand der Seite.

    ![Anwendung hinzufügen] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC749321.png "Anwendung hinzufügen")

5.  Klicken Sie im Dialogfeld **Was möchten Sie tun** klicken Sie auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Hinzufügen einer Anwendung von gallerry] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC749322.png "Hinzufügen einer Anwendung von gallerry")

6.  Geben Sie im **Suchfeld** **Mimecast-Verwaltungskonsole**.

    ![Katalog der Anwendung] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795009.png "Katalog der Anwendung")

7.  Wählen Sie im Ergebnisbereich **Mimecast-Verwaltungskonsole**, und klicken Sie dann auf **abgeschlossen** , um die Anwendung hinzugefügt haben.

    ![Mimecast-Verwaltungskonsole] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795010.png "Mimecast-Verwaltungskonsole")
##<a name="configuring-single-sign-on"></a>Konfigurieren einmaliges Anmelden
  
Das Ziel der in diesem Abschnitt ist zu gliedernden wie Benutzer authentifizieren zu Mimecast-Verwaltungskonsole mit ihrem Konto in Azure Active Directory Federation je nach verwendetem SAML-Protokoll verwenden aktiviert.  
Als Teil dieses Verfahrens müssen Sie eine Datei Base-64-codierte Zertifikat zu erstellen.  
Wenn Sie nicht mit diesem Verfahren vertraut sind, finden Sie unter [Konvertieren ein binäres Zertifikat in eine Textdatei](http://youtu.be/PlgrzUZ-Y1o).

###<a name="to-configure-single-sign-on-perform-the-following-steps"></a>Führen Sie die folgenden Schritte aus, einmaliges Anmelden um zu konfigurieren:

1.  Klicken Sie auf **Konfigurieren einmaligen Anmeldens** zum Öffnen des Dialogfelds **Konfigurieren Single Sign On** , im Azure klassischen-Portal auf der Seite **Verwaltungskonsole Mimecast** Anwendung Integration.

    ![Konfigurieren Sie einmaliges Anmelden] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795011.png "Konfigurieren Sie einmaliges Anmelden")

2.  Klicken Sie auf der Seite **Wie möchten Sie Benutzer bei der Mimecast-Verwaltungskonsole auf** **Microsoft Azure AD einmaliges Anmelden**wählen Sie aus, und klicken Sie dann auf **Weiter**.

    ![Konfigurieren Sie einmaliges Anmelden] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795012.png "Konfigurieren Sie einmaliges Anmelden")

3.  Geben Sie auf der Seite **Konfigurieren der App-URL** in das Textfeld **Mimecast Administrator Console melden Sie sich auf URL** die URL, die Ihre Benutzer zum Melden Sie sich an Ihrer Anwendung Mimecast-Verwaltungskonsole auf (z. B.: "https://webmail-uk.mimecast.com" oder "https://webmail-us.mimecast.com"), und klicken Sie dann auf **Weiter**.

    >[AZURE.NOTE] Die Vorzeichen auf URL ist bestimmten Region.

    ![Konfigurieren der App-URL] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795013.png "Konfigurieren der App-URL")

4.  Klicken Sie auf der Seite **Konfigurieren einmaliges Anmelden bei Mimecast-Verwaltungskonsole** Wenn Ihr Zertifikat herunterladen möchten, klicken Sie auf **Zertifikat herunterladen**, und speichern Sie die Zertifikatdatei lokal auf Ihrem Computer.

    ![Konfigurieren Sie einmaliges Anmelden] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795014.png "Konfigurieren Sie einmaliges Anmelden")

5.  In einem anderen Webbrowserfenster melden Sie sich bei Ihrem Mimecast-Verwaltungskonsole als Administrator.

6.  Wechseln Sie zu **Services \> Anwendung**.

    ![Services] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC794998.png "Services")

7.  Klicken Sie auf **Profile Authentifizierung**.

    ![Authentifizierung Profile] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC794999.png "Authentifizierung Profile")

8.  Klicken Sie auf **Neues Authentifizierungsprofil**.

    ![Neue Authentifizierung Profile] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795000.png "Neue Authentifizierung Profile")

9.  Führen Sie im Abschnitt **Profile Authentifizierung** die folgenden Schritte aus:

    ![Authentifizierungsprofil] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795015.png "Authentifizierungsprofil")

    1.  Geben Sie im Textfeld **Beschreibung** einen Namen für die Konfiguration aus.
    2.  Wählen Sie **Erzwingen von SAML-Authentifizierung für Mimecast-Verwaltungskonsole**.
    3.  Wählen Sie als **Anbieter** **Azure Active Directory**.
    4.  Kopieren Sie auf der Seite **Konfigurieren einmaliges Anmelden bei Mimecast-Verwaltungskonsole** im Azure klassischen Portal den Wert für die **URL des Herausgebers** , und fügen Sie ihn in das Textfeld **URL des Herausgebers** .
    5.  Kopieren Sie den Wert **Remote Anmelde-URL** , und fügen Sie ihn in das Textfeld **Anmelde-URL** , im Azure klassischen-Portal auf der Seite **Konfigurieren einmaliges Anmelden bei Mimecast-Verwaltungskonsole** .
    6.  Kopieren Sie auf der Seite **Konfigurieren einmaliges Anmelden bei Mimecast-Verwaltungskonsole** im Azure klassischen Portal des Werts **Remote Anmelde-URL** , und fügen Sie ihn in das Textfeld **URL Abmelden** .  

        >[AZURE.NOTE]Die Anmelde-URL und dem Wert der Abmeldung URL sind für die Administrator-Konsole Mimecast identisch.

    7.  Erstellen Sie eine **Base-64-codierte** Datei aus Ihrem heruntergeladene Zertifikat.  

        >[AZURE.TIP]Weitere Informationen hierzu finden Sie unter [Konvertieren ein binäres Zertifikat in eine Textdatei](http://youtu.be/PlgrzUZ-Y1o).

    8.  Öffnen das Base-64-codierte Zertifikat in Editor entfernen die erste Zeile ("*--*") und die letzte Zeile ("*--*"), kopieren Sie den restlichen Inhalt davon in der Zwischenablage, und fügen Sie ihn in das Textfeld **Identität Anbieter Zertifikat (Metadaten)** .
    9.  Wählen Sie **Zulassen Single Sign in**.
    10. Klicken Sie auf **Speichern**.

10. Klicken Sie im Portal Azure klassischen wählen Sie die Konfiguration für einzelne Zeichen Bestätigung und dann auf **abgeschlossen** , um das Dialogfeld **Konfigurieren Single Sign On** schließen.

    ![Konfigurieren Sie einmaliges Anmelden] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795016.png "Konfigurieren Sie einmaliges Anmelden")
##<a name="configuring-user-provisioning"></a>Konfigurieren der Benutzer bereitgestellt
  
Um Azure AD-Benutzern zur Anmeldung bei Mimecast-Verwaltungskonsole zu ermöglichen, müssen er in Mimecast Administrator Console bereitgestellt werden.  
Wenn Mimecast-Verwaltungskonsole ist die Bereitstellung eine manuelle Aufgabe.
  
Sie müssen eine Domäne zu registrieren, bevor Sie Benutzer erstellen können.

###<a name="to-configure-user-provisioning-perform-the-following-steps"></a>Führen Sie zum Konfigurieren der Benutzer bereitgestellt, die folgenden Schritte aus:

1.  Melden Sie sich als Administrator auf Ihre **Mimecast-Verwaltungskonsole** an.

2.  Wechseln Sie zu **Verzeichnisse \> internen**.

    ![Verzeichnisse durchsuchen] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795003.png "Verzeichnisse durchsuchen")

3.  Klicken Sie auf **neue Domäne registrieren**.

    ![Registrieren Sie neue Domäne] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795004.png "Registrieren Sie neue Domäne")

4.  Nachdem Sie die neue Domäne erstellt wurde, klicken Sie auf **Neue Adresse**.

    ![Neue Adresse] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795005.png "Neue Adresse")

5.  Führen Sie im Dialogfeld neue Adresse die folgenden Schritte aus:

    ![Speichern] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795006.png "Speichern")

    1.  Geben Sie die **E-Mail-Adresse**, **Globale Name**, **Kennwort** und **Kennwort bestätigen** Attribute eines gültigen AAD-Kontos ein, die Sie in die verknüpfte Textfelder bereitstellen möchten.
    2.  Klicken Sie auf **Speichern**.

>[AZURE.NOTE]Sie können andere Mimecast-Verwaltungskonsole Benutzer Konto Creation Tools oder APIs Mimecast-Verwaltungskonsole zum Bereitstellen von AAD Benutzerkonten aus.

##<a name="assigning-users"></a>Zuweisen von Benutzern
  
Klicken Sie zum Testen der Konfigurations müssen Sie die Benutzer Azure AD-erteilen, dass Sie mit der Anwendung darauf zugreifen sollen, durch das Zuordnen zulassen möchten.

###<a name="to-assign-users-to-mimecast-admin-console-perform-the-following-steps"></a>Zuweisen von Benutzern zu Mimecast Admin-Konsole führen Sie die folgenden Schritte aus:

1.  Erstellen Sie ein Testkonto im Azure klassischen Portal.

2.  Klicken Sie auf der Seite **Verwaltungskonsole Mimecast **Anwendung Integration auf **Benutzer zuweisen**.

    ![Zuweisen von Benutzern] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC795017.png "Zuweisen von Benutzern")

3.  Wählen Sie Ihre Testbenutzer aus, klicken Sie auf **zuweisen**, und klicken Sie dann auf **Ja,** um Ihre Aufgabe zu bestätigen.

    ![Ja] (./media/active-directory-saas-mimecast-admin-console-tutorial/IC767830.png "Ja")
  
Wenn Sie Ihre Einstellungen für einzelnen Zeichen testen möchten, öffnen Sie die Access-Systemsteuerung. Weitere Details über den Bereich Access finden Sie unter [Einführung in die Access-Systemsteuerung](active-directory-saas-access-panel-introduction.md).