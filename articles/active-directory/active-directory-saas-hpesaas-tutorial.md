<properties
    pageTitle="Lernprogramm: Azure-Active Directory-Integration in HPE SaaS | Microsoft Azure"
    description="Informationen Sie zum einmaligen Anmeldens zwischen Azure Active Directory und HPE SaaS konfigurieren."
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
    ms.date="08/16/2016"
    ms.author="jeedes"/>


# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a>Lernprogramm: Azure-Active Directory-Integration in HPE SaaS

Ziel dieses Lernprogramms ist zu veranschaulichen HPE SaaS mit Azure Active Directory (Azure AD) integriert werden soll.  
Integrieren von HPE SaaS in Azure AD bietet Ihnen die folgenden Vorteile:

- Sie können in Azure AD steuern, wer auf HPE SaaS zugreifen kann
- Sie können Ihre Benutzer automatisch auf HPE SaaS (einmaliges Anmelden) angemeldete Abrufen mit ihren Azure AD-Konten aktivieren.
- Sie können Ihre Konten an einem zentralen Ort – im klassischen Azure-Portal verwalten.


Wenn Sie weitere Details zu SaaS app-Integration in Azure AD-wissen möchten, finden Sie unter [Was ist Zugriff auf die Anwendung und einmaliges Anmelden mit Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Um Azure AD-Integration mit HPE SaaS konfigurieren zu können, benötigen Sie die folgenden Elemente:

- Ein Azure AD-Abonnement
- HPE SaaS einmalige Anmeldung aktiviert Abonnements


> [AZURE.NOTE] Wenn Sie um die Schritte in diesem Lernprogramm zu testen, empfehlen wir nicht mit einer Umgebung für die Herstellung.


Führen Sie zum Testen der Schritte in diesem Lernprogramm Tips:

- Sie sollten Ihre Umgebung Herstellung nicht verwenden, es sei denn, dies erforderlich ist.
- Wenn Sie eine Testversion Azure AD-Umgebung besitzen, können Sie eine einen Monat zum Testen [hier](https://azure.microsoft.com/pricing/free-trial/)erhalten.


## <a name="scenario-description"></a>Szenario Beschreibung
Ziel dieses Lernprogramms ist, sodass Sie in einer Umgebung für Azure AD-einmaligen Anmeldens testen können.  
In diesem Lernprogramm beschriebenen Szenario besteht aus zwei Hauptfenster Bausteine:

1. HPE SaaS aus dem Katalog hinzufügen
2. Konfigurieren und Testen Azure AD einmaliges Anmelden


## <a name="adding-hpe-saas-from-the-gallery"></a>HPE SaaS aus dem Katalog hinzufügen
Zum Konfigurieren der Integration von HPE SaaS in Azure AD müssen Sie HPE SaaS zu Ihrer Liste der verwalteten SaaS apps aus dem Katalog hinzuzufügen.

**Um HPE SaaS aus dem Katalog hinzufügen möchten, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im **Azure klassischen Portal**auf der linken Navigationsbereich auf **Active Directory**. 

    ![Active Directory][1]

2. Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3. Klicken Sie zum Öffnen der Anwendungsansicht in der Verzeichnisansicht im oberen Menü auf **Applications** .

    ![Applikationen][2]

4. Klicken Sie auf **Hinzufügen** , am unteren Rand der Seite.

    ![Applikationen][3]

5. Klicken Sie im Dialogfeld **Was möchten Sie tun** klicken Sie auf **eine Anwendung aus dem Katalog hinzufügen**.

    ![Applikationen][4]

6. Geben Sie in das Suchfeld **HPE SaaS**aus.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_01.png)

7. Wählen Sie im Ergebnisbereich **HPE SaaS aus**, und klicken Sie dann auf **abgeschlossen** , um die Anwendung hinzugefügt haben.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen Azure AD einmaliges Anmelden
Das Ziel der in diesem Abschnitt ist erläutert, wie Sie konfigurieren und Testen der Azure AD-einmaliges Anmelden mit HPE SaaS basierend auf einen Testbenutzer "Britta Simon" bezeichnet.

Für einmaliges Anmelden entwickelt muss Azure AD wissen, was der Benutzer Gegenstück HPE SaaS an einen Benutzer in Azure AD ist. Kurzum, muss eine Link Beziehung zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in HPE SaaS eingerichtet werden.  
Dieser Link Beziehung wird hergestellt, indem Sie den Wert des **Benutzernamens** in Azure AD als der Wert für den **Benutzernamen** in HPE SaaS zuweisen.

Zum Konfigurieren und Azure AD-einmaliges Anmelden mit HPE SaaS testen, müssen Sie die folgenden Bausteine durchführen:

1. **[Konfigurieren von Azure AD einmaligen Anmeldens](#configuring-azure-ad-single-single-sign-on)** - damit Ihre Benutzer dieses Feature verwenden können.
2. **[Erstellen einer Azure AD Benutzer testen](#creating-an-azure-ad-test-user)** : Azure AD-einmaliges Anmelden mit Britta Simon testen.
4. **[Erstellen einer HPE SaaS Benutzer testen](#creating-a-hpesaas-test-user)** : ein Gegenstück von Britta Simon in HPE SaaS haben, die in der Azure AD-Darstellung Ihrer verknüpft ist.
5. **[Zuweisen von Azure AD Benutzer testen](#assigning-the-azure-ad-test-user)** : Britta Simon mit Azure AD-einmaliges Anmelden aktivieren.
5. **[Testen der einmaligen Anmeldens](#testing-single-sign-on)** - zur Überprüfung, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren von Azure AD einmaliges Anmelden

Das Ziel der in diesem Abschnitt ist Azure AD-einmaliges Anmelden im klassischen Azure-Portal aktivieren und konfigurieren einmaliges Anmelden in Ihrer Anwendung HPE SaaS.



**Führen Sie die folgenden Schritte aus, um Azure AD-einmaliges Anmelden mit HPE SaaS konfigurieren:**

1. Im Azure klassischen-Portal auf der Seite **HPE SaaS** Integration Anwendung klicken Sie auf **Konfigurieren einmaligen Anmeldens** zum Öffnen des Dialogfelds **Konfigurieren einmaliges Anmelden** .

    ![Konfigurieren Sie einmaliges Anmelden][6] 

2. Klicken Sie auf der Seite **Wie möchten Sie Benutzer HPE SaaS auf bei** **Azure AD einmaliges Anmelden**wählen Sie aus, und klicken Sie dann auf **Weiter**.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_03.png) 

3. Klicken Sie auf der Dialogseite **App-Einstellungen konfigurieren** , gehen Sie folgendermaßen vor:.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_04.png) 


    ein. Geben Sie in das Textfeld **Melden Sie sich auf URL** die URL, die von den Benutzern die Anmeldung an Ihrer Anwendung HPE SaaS verwendet: **"https://login.saas.hpe.com/msg"**. Kunden können auch diese Anwendung bestimmte URL ändern.

    b. Klicken Sie auf **Weiter**.


4. Führen Sie auf der Seite **Konfigurieren einmaliges Anmelden bei HPE SaaS** die folgenden Schritte aus:

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_05.png) 

    ein. Klicken Sie auf **Herunterladen von Metadaten**aus, und speichern Sie die Datei auf Ihrem Computer.

    b. Klicken Sie auf **Weiter**.


5. Um für die Anwendung konfigurierten SSO zu gelangen, wenden Sie sich an Ihr Supportteam HPE SaaS und per e-Mail senden Sie die heruntergeladene Metadaten-Datei anfügen. Damit sie für die Integration von SSO konfiguriert werden können.


6. Im Portal Azure klassischen wählen Sie die Konfiguration für einzelne Zeichen Bestätigung, und klicken Sie dann auf **Weiter**.

    ![Azure AD einmaliges Anmelden][10]

7. Klicken Sie auf der Seite **Bestätigung für einzelne anmelden** auf **abgeschlossen**.  

    ![Azure AD einmaliges Anmelden][11]



### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Benutzers mit Azure AD-testen
Das Ziel der in diesem Abschnitt besteht im Erstellen eines Testbenutzers aufgerufen Britta Simon im klassischen Azure-Portal.  

![Erstellen von Azure AD-Benutzer][20]

**Führen Sie die folgenden Schritte aus, um einen Testbenutzer in Azure AD zu erstellen:**

1. Klicken Sie im **Azure klassischen Portal**auf der linken Navigationsbereich auf **Active Directory**.

![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_09.png) 

2. Wählen Sie aus der Liste **Verzeichnis** Verzeichnis für das Sie Verzeichnisintegration aktivieren möchten.

3. Wenn die Liste der Benutzer, klicken Sie im Menü oben anzeigen möchten, klicken Sie auf **Benutzer**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. Klicken Sie im Dialogfeld **Benutzer hinzufügen** um in der Symbolleiste auf der Unterseite öffnen, auf **Benutzer hinzufügen**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

5. Führen Sie auf der Seite **Teilen Sie uns zu diesem Benutzer** die folgenden Schritte aus:

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_05.png) 

    ein. Wählen Sie als Typ des Benutzers neuen Benutzer in Ihrer Organisation ein.

    b. Geben Sie den Benutzernamen **Textfeld** **BrittaSimon**ein.

    c. Klicken Sie auf **Weiter**.

6.  Klicken Sie auf der Seite **Benutzerprofil** Dialogfeld führen Sie die folgenden Schritte aus:

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_06.png) 

    ein. Geben Sie im Textfeld **Vorname** **Britta**aus.  

    b. In das letzte Textfeld **Name** , Typ, **Simon**.

    c. Geben Sie im Textfeld **Anzeigename** **Britta Simon**aus.

    d. Wählen Sie in der Liste **Rolle** **Benutzer**aus.

    e. Klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **erste temporäres Kennwort** auf **Erstellen**.

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_07.png) 

8. Klicken Sie auf der Seite **erste temporäres Kennwort** führen Sie die folgenden Schritte aus:

    ![Erstellen eines Benutzers mit Azure AD-testen](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_08.png) 

    ein. Notieren Sie den Wert für das **Neue Kennwort ein**.

    b. Klicken Sie auf **abgeschlossen**.   




### <a name="creating-a-hpe-saas-test-user"></a>Erstellen eines Testbenutzers HPE SaaS

Das Ziel der in diesem Abschnitt ist zum Erstellen eines Benutzers Britta Simon in HPE SaaS bezeichnet. Arbeiten Sie mit HPE SaaS Supportteam Benutzer im HPE SaaS Konto hinzufügen. 


> [AZURE.NOTE]Wenn Sie einen Benutzer manuell erstellen müssen, müssen Sie wenden Sie sich an das Supportteam HPE SaaS.


### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Test-Benutzers

Das Ziel der in diesem Abschnitt ist für die Aktivierung der Britta Simon Azure einmaliges Anmelden verwenden, indem Sie keinen Zugriff auf HPE SaaS erteilen.

![Zuweisen der Benutzer][200] 

**Um HPE SaaS Britta Simon zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im Portal Azure klassischen zum Öffnen der Anwendungsansicht in der Verzeichnisansicht klicken Sie auf **Applikationen** im oberen Menü.

    ![Zuweisen der Benutzer][201] 

2. Wählen Sie in der Liste Applikationen **HPE SaaS**aus.

    ![Konfigurieren Sie einmaliges Anmelden](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_50.png) 

1. Klicken Sie auf **Benutzer**, klicken Sie im Menü oben.

    ![Zuweisen der Benutzer][203] 

1. Wählen Sie in der Liste Benutzer **Britta Simon**aus.

2. Klicken Sie unten auf der Symbolleiste auf **zuweisen**.

    ![Zuweisen der Benutzer][205]



### <a name="testing-single-sign-on"></a>Testen einmaliges Anmelden

Das Ziel der in diesem Abschnitt ist zum Azure AD-einzelne anmelden Überprüfen der Konfiguration mithilfe des Bedienfelds Access.  
Wenn Sie die Kachel HPE SaaS im Bereich Access klicken, Sie sollten automatisch an Ihrer Anwendung HPE SaaS angemeldete abrufen.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der zum Integrieren SaaS-Apps mit Azure-Active Directory-Lernprogramme](active-directory-saas-tutorial-list.md)
* [Was ist die Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_205.png
