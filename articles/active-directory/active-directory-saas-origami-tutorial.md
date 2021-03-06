<properties
    pageTitle="Lernprogramm: Azure-Active Directory-Integration in Origami | Microsoft Azure"
    description="Informationen Sie zum einmaligen Anmeldens zwischen Azure Active Directory und Origami konfigurieren."
    services="active-directory"
    documentationCenter=""
    authors="jeevansd"
    manager="femila"
    editor=""/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/10/2016"
    ms.author="jeedes"/>


# <a name="tutorial-azure-active-directory-integration-with-origami"></a>Lernprogramm: Azure-Active Directory-Integration in Origami

In diesem Lernprogramm erfahren Sie, wie Origami mit Azure Active Directory (Azure AD) integriert werden soll.

Integrieren von Origami in Azure AD bietet Ihnen die folgenden Vorteile:

- Sie können in Azure AD steuern, wer auf Origami zugreifen kann
- Sie können Ihre Benutzer automatisch auf Origami (einmaliges Anmelden) mit ihren Konten Azure AD-angemeldete abrufen aktivieren.
- Sie können Ihre Konten an einem zentralen Ort – im klassischen Azure-Portal verwalten.

Wenn Sie weitere Details zu SaaS app-Integration in Azure AD-wissen möchten, finden Sie unter [Was ist Zugriff auf die Anwendung und einmaliges Anmelden mit Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Zum Konfigurieren von Azure AD-Integration mit Origami, benötigen Sie die folgenden Elemente:

- Ein Azure AD-Abonnement
- Origami einmalige Anmeldung aktiviert Abonnements


> [AZURE.NOTE] Wenn Sie um die Schritte in diesem Lernprogramm zu testen, empfehlen wir nicht mit einer Umgebung für die Herstellung.


Führen Sie zum Testen der Schritte in diesem Lernprogramm Tips:

- Sie sollten Ihre Umgebung Herstellung nicht verwenden, es sei denn, dies erforderlich ist.
- Wenn Sie eine Testversion Azure AD-Umgebung besitzen, können Sie eine einen Monat zum Testen [hier](https://azure.microsoft.com/pricing/free-trial/)erhalten.


## <a name="scenario-description"></a>Szenario Beschreibung
In diesem Lernprogramm testen Sie Azure AD-einmaliges Anmelden in einer testumgebung.

In diesem Lernprogramm beschriebenen Szenario besteht aus zwei Hauptfenster Bausteine:

1. Origami aus dem Katalog hinzufügen
2. Konfigurieren und Testen Azure AD einmaliges Anmelden


## <a name="adding-origami-from-the-gallery"></a>Origami aus dem Katalog hinzufügen
Zum Konfigurieren der Integration von Origami in Azure AD müssen Sie Origami zu Ihrer Liste der verwalteten SaaS apps aus dem Katalog hinzuzufügen.

**Um Origami aus dem Katalog hinzufügen möchten, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im **Azure klassischen Portal**auf der linken Navigationsbereich auf **Active Directory**.

    ![Active Directory][1]
2. Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3. Klicken Sie zum Öffnen der Anwendungsansicht in der Verzeichnisansicht im oberen Menü auf **Applications** .

    ![Applikationen][2]

4. Klicken Sie auf **Hinzufügen** , am unteren Rand der Seite.

    ![Applikationen][3]

5. Klicken Sie im Dialogfeld **Was möchten Sie tun** klicken Sie auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Applikationen][4]

6. Geben Sie in das Suchfeld **Origami**aus.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/tutorial_origami_01.png)
7. Im Ergebnisbereich **Origami**wählen Sie aus, und klicken Sie dann auf **abgeschlossen** , um die Anwendung hinzugefügt haben.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/tutorial_origami_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen Azure AD einmaliges Anmelden
In diesem Abschnitt Konfigurieren und Testen Azure AD-einmaliges Anmelden mit Origami basierend auf einen Testbenutzer "Britta Simon" bezeichnet.

Für einmaliges Anmelden entwickelt muss Azure AD kennen, kann der Benutzer Gegenstück Origami einem Benutzer in Azure AD. Kurzum, muss eine Link Beziehung zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in Origami eingerichtet werden.

Dieser Link Beziehung wird hergestellt, indem Sie den Wert des **Benutzernamens** in Azure AD als der Wert für den **Benutzernamen** in Origami zuweisen.

Zum Konfigurieren und Azure AD-einmaliges Anmelden mit Origami testen, müssen Sie die folgenden Bausteine durchführen:

1. **[Konfigurieren von Azure AD einmaligen Anmeldens](#configuring-azure-ad-single-sign-on)** - damit Ihre Benutzer dieses Feature verwenden können.
2. **[Erstellen einer Azure AD Benutzer testen](#creating-an-azure-ad-test-user)** : Azure AD-einmaliges Anmelden mit Britta Simon testen.
3. **[Erstellen einer Origami Benutzer testen](#creating-a-origami-test-user)** : ein Gegenstück von Britta Simon in Origami haben, die in der Azure AD-Darstellung Ihrer verknüpft ist.
4. **[Zuweisen von Azure AD Benutzer testen](#assigning-the-azure-ad-test-user)** : Britta Simon mit Azure AD-einmaliges Anmelden aktivieren.
5. **[Testen der einmaligen Anmeldens](#testing-single-sign-on)** - zur Überprüfung, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren von Azure AD einmaliges Anmelden

In diesem Abschnitt Azure AD-einmaliges Anmelden im klassischen Portal aktivieren und konfigurieren in Ihrer Anwendung Origami einmaliges Anmelden.


**Führen Sie die folgenden Schritte aus, um Azure AD-einmaliges Anmelden mit Origami konfigurieren:**

1. Im Portal klassischen auf der Seite **Origami** Integration Anwendung klicken Sie auf **Konfigurieren einmaligen Anmeldens** zum Öffnen des Dialogfelds **Konfigurieren einmaliges Anmelden** .
     
    ![Konfigurieren Sie einmaliges Anmelden][6] 

2. Klicken Sie auf der Seite **Wie möchten Sie Benutzer Origami auf bei** **Azure AD einmaliges Anmelden**wählen Sie aus, und klicken Sie dann auf **Weiter**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_03.png) 

3. Führen Sie auf der Seite Dialogfeld **App-Einstellungen konfigurieren** die folgenden Schritte aus:

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_04.png) 

    ein. Geben Sie in das Textfeld **Melden Sie sich auf URL** die URL Ihrer Benutzer melden Sie sich für den Zugriff auf Ihre Origami-Anwendung unter Verwendung des folgenden Musters untersuchten: **https://live.origamirisk.com/origami/account/login?account=\<Firmennamen\> **
    
    b. Klicken Sie auf **Weiter**
 
4. Klicken Sie auf der Seite **Konfigurieren einmaliges Anmelden bei Origami** führen Sie die folgenden Schritte aus:

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_05.png)

    ein. Klicken Sie auf **Zertifikat herunterladen**, und speichern Sie die Datei auf Ihrem Computer.

    b. Klicken Sie auf **Weiter**.



1. Melden Sie sich mit dem Konto Origami mit Administratorrechten an.

1. Klicken Sie oben im Menü auf **Administrator**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)
  

1. Führen Sie auf der Dialogseite einzelnen melden Sie sich auf einrichten die folgenden Schritte aus:

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/123.png)

    ein. Wählen Sie **Enable Single Sign On**aus.

    b. Im Portal Azure klassischen kopieren Sie die **URL der SAML-SSO**, und fügen Sie ihn in das Textfeld **Des Identitätsanbieter Anmeldung Seiten-URL** .

    c. Im Portal Azure klassischen kopieren Sie die **Einzelnen Zeichen, Dienst-URL**, und fügen Sie ihn in das Textfeld **Des Identitätsanbieter Sign-out Seiten-URL** .

    d. Klicken Sie auf **Durchsuchen** , um das Zertifikat hochladen, die, das Sie vom klassischen Azure-Portal heruntergeladen haben.

    e. Klicken Sie auf **Änderungen speichern**.


6. Im Portal klassischen wählen Sie die Bestätigung Konfiguration für einzelne Zeichen, und klicken Sie dann auf **Weiter**.
    
    ![Azure AD einmaliges Anmelden][10]

7. Klicken Sie auf der Seite **Bestätigung für einzelne anmelden** auf **abgeschlossen**.  
 
    ![Azure AD einmaliges Anmelden][11]


### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Benutzers mit Azure AD-testen
In diesem Abschnitt erstellen Sie einen Testbenutzer im klassischen Portal Britta Simon bezeichnet.


![Erstellen von Azure AD-Benutzer][20]

**Führen Sie die folgenden Schritte aus, um einen Testbenutzer in Azure AD zu erstellen:**

1. Klicken Sie im **Azure klassischen Portal**auf der linken Navigationsbereich auf **Active Directory**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_09.png) 

2. Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3. Wenn die Liste der Benutzer, klicken Sie im Menü oben anzeigen möchten, klicken Sie auf **Benutzer**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. Klicken Sie im Dialogfeld **Benutzer hinzufügen** um in der Symbolleiste auf der Unterseite öffnen, auf **Benutzer hinzufügen**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

5. Führen Sie auf der Seite **Teilen Sie uns zu diesem Benutzer** die folgenden Schritte aus:  ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_05.png) 

    ein. Wählen Sie als Typ des Benutzers neuen Benutzer in Ihrer Organisation ein.

    b. Geben Sie den Benutzernamen **Textfeld** **BrittaSimon**ein.

    c. Klicken Sie auf **Weiter**.

6.  Klicken Sie auf der Seite **Benutzerprofil** -Dialogfeld führen Sie die folgenden Schritte aus: ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_06.png) 

    ein. Geben Sie im Textfeld **Vorname** **Britta**aus.  

    b. In das letzte Textfeld **Name** , Typ, **Simon**.

    c. Geben Sie im Textfeld **Anzeigename** **Britta Simon**aus.

    d. Wählen Sie in der Liste **Rolle** **Benutzer**aus.

    e. Klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **erste temporäres Kennwort** auf **Erstellen**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_07.png) 

8. Klicken Sie auf der Seite **erste temporäres Kennwort** führen Sie die folgenden Schritte aus:

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-origami-tutorial/create_aaduser_08.png) 

    ein. Notieren Sie den Wert für das **Neue Kennwort ein**.

    b. Klicken Sie auf **abgeschlossen**.   



### <a name="creating-an-origami-test-user"></a>Erstellen eines Benutzers mit Origami testen

In diesem Abschnitt erstellen Sie einen Benutzer namens Britta Simon in Origami. 

1. Melden Sie sich mit dem Konto Origami mit Administratorrechten an.

2. Klicken Sie oben im Menü auf **Administrator**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. Klicken Sie auf **Benutzer**, klicken Sie im Dialogfeld **Benutzer und Sicherheit** .
    
    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. Klicken Sie auf **neuen Benutzer hinzufügen**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. Klicken Sie im Dialogfeld neuen Benutzer hinzufügen führen Sie die folgenden Schritte aus:

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    ein. Geben Sie in das Textfeld **Benutzername** Britta Simon Benutzer Namen in der klassischen Azure-Portal.

    b. Geben Sie im Textfeld **Kennwort** ein Passwotd ein.

    c. Geben Sie im Textfeld **Kennwort bestätigen** das Kennwort erneut ein.

    d. Geben Sie im Textfeld **Vorname** **Britta**aus.

    e. Geben Sie im Textfeld **Nachname** **Simon**aus.

    f. Klicken Sie auf **Speichern**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

1. Zuweisen von **Benutzerrollen** und **Client Access** für den Benutzer. 

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Test-Benutzers

In diesem Abschnitt aktivieren Sie Britta Simon Azure einmaliges Anmelden verwenden, indem Sie keinen Zugriff auf Origami erteilen.

![Zuweisen der Benutzer][200] 

**Um Origami Britta Simon zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im Portal klassischen zum Öffnen der Anwendungsansicht in der Verzeichnisansicht klicken Sie auf **Applikationen** im oberen Menü.

    ![Zuweisen der Benutzer][201] 

2. Wählen Sie in der Liste Applikationen **Origami**aus.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-origami-tutorial/tutorial_origami_50.png) 

3. Klicken Sie auf **Benutzer**, klicken Sie im Menü oben.

    ![Zuweisen der Benutzer][203]

4. Wählen Sie in der Liste Benutzer **Britta Simon**aus.

5. Klicken Sie unten auf der Symbolleiste auf **zuweisen**.

    ![Zuweisen der Benutzer][205]


### <a name="testing-single-sign-on"></a>Testen einmaliges Anmelden

In diesem Abschnitt Testen Sie Ihre Azure AD-einzelne anmelden Konfiguration mit der Access-Systemsteuerung.

Wenn Sie die Kachel Origami im Bereich Access klicken, Sie sollten automatisch an Ihrer Anwendung Origami angemeldete abrufen.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der zum Integrieren SaaS-Apps mit Azure-Active Directory-Lernprogramme](active-directory-saas-tutorial-list.md)
* [Was ist die Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-origami-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-origami-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-origami-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-origami-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-origami-tutorial/tutorial_general_205.png
