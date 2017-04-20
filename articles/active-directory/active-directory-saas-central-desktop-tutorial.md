<properties 
    pageTitle="Lernprogramm: Azure-Active Directory-Integration in zentralen Desktop | Microsoft Azure" 
    description="Erfahren Sie, wie mit zentralen Desktop mit Azure Active Directory einmaliges Anmelden, automatisierte Bereitstellung und mehr aktiviert!" 
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

#<a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Lernprogramm: Azure-Active Directory-Integration in zentralen Desktop

Ziel dieses Lernprogramms ist die Integration von Azure und zentralen Desktop angezeigt. Das in diesem Lernprogramm beschriebenen Szenario wird davon ausgegangen, dass Sie die folgenden Elemente bereits:

-   Ein gültiges Azure-Abonnement
-   Eine zentrale desktop einmaliges Anmelden aktiviert Abonnement / zentrale Desktop-Mandanten

In diesem Lernprogramm beschriebenen Szenario umfasst die folgenden Bausteine erforderlich:

1.  Aktivieren die Anwendungsintegration für zentrale Desktop
2.  Konfigurieren einmaliges Anmelden
3.  Konfigurieren der Benutzer bereitgestellt
4.  Zuweisen von Benutzern

![Szenario] (./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Szenario")
##<a name="enabling-the-application-integration-for-central-desktop"></a>Aktivieren die Anwendungsintegration für zentrale Desktop

Ziel dieses Abschnitts ist es, wie die Anwendung die Telefonintegration für zentrale Desktop gliedern.

###<a name="to-enable-the-application-integration-for-central-desktop-perform-the-following-steps"></a>Um die Anwendungsintegration für zentrale Desktop zu aktivieren, führen Sie die folgenden Schritte aus:

1.  Klicken Sie im Azure klassischen-Portal auf der linken Navigationsbereich auf **Active Directory**.

    ![Active Directory] (./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")

2.  Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3.  Klicken Sie zum Öffnen der Anwendungsansicht in der Verzeichnisansicht im oberen Menü auf **Applications** .

    ![Applikationen] (./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applikationen")

4.  Klicken Sie auf **Hinzufügen** , am unteren Rand der Seite.

    ![Anwendung hinzufügen] (./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Anwendung hinzufügen")

5.  Klicken Sie im Dialogfeld **Was möchten Sie tun** klicken Sie auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Hinzufügen einer Anwendung von gallerry] (./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Hinzufügen einer Anwendung von gallerry")

6.  Geben Sie im **Suchfeld** **Zentralen Desktop**aus.

    ![Katalog der Anwendung] (./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Katalog der Anwendung")

7.  Wählen Sie im Ergebnisbereich **Zentralen Desktop**, und klicken Sie dann auf **abgeschlossen** , um die Anwendung hinzugefügt haben.

    ![Zentrale Desktop] (./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Zentrale Desktop")
##<a name="configuring-single-sign-on"></a>Konfigurieren einmaliges Anmelden

Das Ziel der in diesem Abschnitt ist zu gliedernden wie Benutzer authentifizieren auf zentralen Desktop mit ihrem Konto in Azure Active Directory Federation je nach verwendetem SAML-Protokoll verwenden aktiviert.  
Als Teil dieses Verfahrens müssen Sie eine Base-64-codierte Zertifikat in Ihrem Mandanten zentralen Desktop hochladen.  
Wenn Sie nicht mit diesem Verfahren vertraut sind, finden Sie unter [Konvertieren ein binäres Zertifikat in eine Textdatei](http://youtu.be/PlgrzUZ-Y1o).



###<a name="to-configure-single-sign-on-perform-the-following-steps"></a>Führen Sie die folgenden Schritte aus, einmaliges Anmelden um zu konfigurieren:

1.  Im Azure klassischen-Portal auf der Seite **Zentrale Desktop** -Anwendung Integration klicken Sie auf **Konfigurieren einmaligen Anmeldens** um das Dialogfeld **Konfigurieren Single Sign On** öffnen.

    ![Konfigurieren einmaliges Anmelden] (./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Konfigurieren einmaliges Anmelden")

2.  Klicken Sie auf der Seite **Wie möchten Sie Benutzer bei der zentralen Desktop auf** **Microsoft Azure AD einmaliges Anmelden**wählen Sie aus, und klicken Sie dann auf **Weiter**.

    ![Konfigurieren einmaliges Anmelden] (./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Konfigurieren einmaliges Anmelden")

3.  Klicken Sie auf der Seite **App-URL konfigurieren** führen Sie die folgenden Schritte aus, und klicken Sie dann auf **Weiter**: 

    -   In das Textfeld **Zentralen Desktop melden Sie sich In URL** ein, geben Sie die URL der Ihrem Mandanten zentralen Desktop (z. B.: *http://contoso.centraldesktop.com*).
    -   Geben Sie Ihre zentrale Desktop AssertionConsumerService URL in das Textfeld zentralen Desktop Antwort-URL (z. B.: https://contoso.centraldesktop.com/saml2-assertion.php).

    >[AZURE.NOTE] Rufen Sie den Wert aus der zentralen desktop Metadaten (z. B.: *http://contoso.centraldesktop.com*).

    ![Konfigurieren der app-URL] (./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Konfigurieren der app-URL")

4.  Klicken Sie auf der Seite **Konfigurieren einmaliges Anmelden am zentralen Desktop** Wenn Ihr Zertifikat herunterladen möchten, klicken Sie auf **Zertifikat herunterladen**, und speichern Sie die Zertifikatdatei auf Ihrem Computer.

    ![Konfigurieren einmaliges Anmelden] (./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Konfigurieren einmaliges Anmelden")

5.  Melden Sie sich bei Ihrem **Zentralen Desktop** -Mandanten.

6.  Wechseln Sie zu **Einstellungen**, klicken Sie auf **Erweitert**, und klicken Sie dann auf **Single Sign On**.

    ![Setup – erweiterte] (./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup – erweiterte")

7.  Führen Sie auf der Seite **Einzelne melden Sie sich auf Einstellungen** die folgenden Schritte aus:

    ![Einmaliges Anmelden Einstellungen] (./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Einmaliges Anmelden Einstellungen")

    1.  Wählen Sie **Aktivieren SAML Version 2 für einmaliges Anmelden**.
    2.  Im Azure klassischen-Portal auf der Seite **Konfigurieren einmaliges Anmelden am zentralen Desktop** kopieren Sie den Wert des **Herausgebers URL** , und fügen Sie ihn in das Textfeld **SSO-URL** .
    3.  Im Azure klassischen-Portal auf der Seite **Konfigurieren einmaliges Anmelden am zentralen Desktop** kopieren Sie den Wert **Remote Anmelde-URL** , und fügen Sie ihn in das Textfeld **SSO Anmelde-URL** .
    4.  Im Azure klassischen-Portal auf der Seite **Konfigurieren einmaliges Anmelden am zentralen Desktop** kopieren Sie den Wert für die **Einzelnen Sign-Out Dienst-URL** , und klicken Sie dann in das Textfeld **SSO Abmeldung URL** einzufügen.

8.  Führen Sie im Abschnitt **Nachricht Signatur Überprüfungsmethode** die folgenden Schritte aus:

    ![Nachricht Signatur Überprüfungsmethode] (./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Nachricht Signatur Überprüfungsmethode")

    1.  Wählen Sie **Zertifikat**.
    2.  Wählen Sie in der Liste **SSO Zertifikat** **RSH SHA256**aus.
    3.  Erstellen Sie eine Textdatei aus dem heruntergeladenen Zertifikat, kopieren Sie den Inhalt der Textdatei, und fügen Sie ihn in das Feld **SSO Zertifikat** .  

        >[AZURE.TIP] Weitere Informationen hierzu finden Sie unter [So konvertieren ein binäres Zertifikat in eine Textdatei](http://youtu.be/PlgrzUZ-Y1o)

    4.  Wählen Sie die **Anzeige eines Links auf der Anmeldeseite SAMLv2**.

9.  Klicken Sie auf **Aktualisieren**.

10. Klicken Sie im Portal Azure klassischen wählen Sie die Konfiguration für einzelne Zeichen Bestätigung und dann auf **abgeschlossen** , um das Dialogfeld **Konfigurieren Single Sign On** schließen.

    ![Konfigurieren einmaliges Anmelden] (./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Konfigurieren einmaliges Anmelden")
##<a name="configuring-user-provisioning"></a>Konfigurieren der Benutzer bereitgestellt

Für AAD Benutzer anmelden können müssen diese mit der zentralen Desktop-Anwendung bereitgestellt werden. In diesem Abschnitt beschrieben, wie Sie die AAD Benutzerkonten in zentralen Desktop erstellen.

###<a name="to-provision-user-accounts-to-central-desktop"></a>Benutzerkonten auf zentralen Desktop bereitstellen zu können:

1.  Melden Sie sich bei Ihrem zentralen Desktop-Mandanten.

2.  Wechseln Sie zu **Personen \> internen Mitglieder**.

3.  Klicken Sie auf **interne Mitglieder hinzufügen**.

    ![Personen] (./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personen")

4.  Geben Sie in das Textfeld **E-Mail-Adresse der Mitglieder** ein Konto AAD Sie bereitstellen möchten, und klicken Sie dann auf **Weiter**.

    ![E-Mail-Adressen der Mitglieder] (./media/active-directory-saas-central-desktop-tutorial/IC781052.png "E-Mail-Adressen der Mitglieder")

5.  Klicken Sie auf **interne hinzufügen Mitglieder**.

    ![Interner Mitglied hinzufügen] (./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Interner Mitglied hinzufügen")

    >[AZURE.NOTE] Benutzer, die Sie hinzugefügt haben, eine e-Mail-Nachricht erhalten, die einen Link zur Bestätigung benötigten enthält klicken, um das Konto zu aktivieren.

>[AZURE.NOTE] Alle anderen zentralen Desktop Benutzer Konto Creation Tools können oder APIs bereitgestellt durch zentrale Desktop bereitstellen AAD Benutzerkonten

##<a name="assigning-users"></a>Zuweisen von Benutzern

Klicken Sie zum Testen der Konfigurations müssen Sie die Benutzer Azure AD-erteilen, dass Sie mit der Anwendung darauf zugreifen sollen, durch das Zuordnen zulassen möchten.

###<a name="to-assign-users-to-central-desktop-perform-the-following-steps"></a>Zuweisen von Benutzern zu zentralen Desktop führen Sie die folgenden Schritte aus:

1.  Erstellen Sie ein Testkonto im Portal Azure klassischen.

2.  Klicken Sie auf der Seite **Zentrale Desktop** -Anwendung Integration auf **Benutzer zuweisen**.

    ![Zuweisen von Benutzern] (./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Zuweisen von Benutzern")

3.  Wählen Sie Ihre Testbenutzer aus, klicken Sie auf **zuweisen**, und klicken Sie dann auf **Ja,** um Ihre Aufgabe zu bestätigen.

    ![Ja] (./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Ja")

Wenn Sie Ihre Einstellungen für einzelnen Zeichen testen möchten, öffnen Sie die Access-Systemsteuerung. Weitere Details über den Bereich Access finden Sie unter [Einführung in die Access-Systemsteuerung](active-directory-saas-access-panel-introduction.md).
