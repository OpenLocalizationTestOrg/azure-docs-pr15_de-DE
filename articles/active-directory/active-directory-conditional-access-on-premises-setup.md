<properties
    pageTitle="Einrichten von lokalen bedingten Zugriff mit Azure Active Directory-Gerät Registrierung | Microsoft Azure"
    description="Eine schrittweise Anleitung bedingte Zugriff auf lokale Applikationen mit Active Directory Federation Service (AD FS) in Windows Server 2012 R2 aktivieren."
    services="active-directory"
    documentationCenter=""
    authors="femila"
    manager="swadhwa"
    editor=""/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/27/2016"
    ms.author="femila"/>


# <a name="setting-up-on-premises-conditional-access-using-azure-active-directory-device-registration"></a>Einrichten von lokalen bedingten Zugriff mit Azure Active Directory-Gerät Registrierung

Besitzer Geräte Benutzer können persönlich bekannt Ihrer Organisation durch den Benutzer auffordern, Arbeit Ort Verknüpfung aktivierten Geräte mit dem Dienst Azure Active Directory-Gerät Registrierung gekennzeichnet werden. Es folgt eine schrittweise Anleitung zum bedingten Zugriff auf lokale Applikationen mit Active Directory Federation Service (AD FS) in Windows Server 2012 R2 zu aktivieren.

> [AZURE.NOTE]
> Office 365-Lizenz oder Azure AD Premium Lizenz ist bei Verwendung von Geräten in Azure Active Directory-Gerät Registrierung Dienst bedingte Richtlinien registriert erforderlich. Dies umfasst Richtlinien seitens Active Directory Federation Services (AD FS) auf lokale Ressourcen.

Weitere Informationen zu den Szenarien bedingten Zugriff für lokale finden Sie unter [Arbeitsplatz auf jedes Gerät für SSO und nahtlose zweite Faktor Authentifizierung über Unternehmen Applikationen Verknüpfung](https://technet.microsoft.com/library/dn280945.aspx).

Diese Funktionen stehen für Kunden, die eine Azure Active Directory Premium-Lizenz erwerben.

<a name="supported-devices"></a>Unterstützte Geräte
-------------------------------------------------------------------------
* Windows 7-Domäne beitreten Geräte.
* Windows 8.1 persönlich und Domäne beigetreten Geräte.
* iOS 6 und höher, für den Safari-browser
* Android 4.0 oder höher, Samsung GS3 oder über Telefone, Samsung Note2 oder über Tablets.


<a name="scenario-prerequisites"></a>Szenario erforderliche Komponenten
------------------------------------------------------------------------
* Office 365-Abonnement oder Azure-Active Directory-Premium
* Ein Azure Active Directory-Mandanten
* Windows Server Active Directory (WindowsServer 2008 oder höher)
* Aktualisierte Schema in Windows Server 2012 R2
* Lizenz für Azure-Active Directory-Premium
* Windows Server 2012 R2 Federation Services konfiguriert für SSO zu Azure AD
* Windows Server 2012 R2 Web Anwendung Proxy Microsoft Azure-Active Directory verbinden (Azure AD verbinden). [Hier herunterladen Azure AD-verbinden](http://www.microsoft.com/en-us/download/details.aspx?id=47594).
* Überprüft Domäne.

<a name="known-issues-in-this-release"></a>Bekannte Probleme in dieser Version
-------------------------------------------------------------------------------
* Bedingte Gerät basierend-Richtlinien müssen Gerät Objekt schreiben-Back Active Directory aus Azure Active Directory. Es kann bis zu 3 Stunden Geräteobjekte geschrieben zurück in Active Directory werden dauern.
* iOS 7-Geräte fordert immer auf den Benutzer, während der Client Zertifikatauthentifizierung ein Zertifikat auszuwählen.
* Einige Versionen iOS8, bevor iOS 8.3 nicht funktionieren.

## <a name="scenario-assumptions"></a>Annahmen im Szenario
Dieses Szenario setzt voraus, dass Sie eine hybridumgebung aus einem Azure AD-Mandanten und einem lokalen Active Directory haben. Diese Mandanten mit Azure AD verbinden verbunden werden sollen und mit einer Domäne überprüft und AD FS für SSO. Die folgenden Checkliste hilft Ihnen die Konfiguration Ihrer Umgebung auf die oben beschriebenen Phase.

<a name="checklist-prerequisites-for-conditional-access-scenario"></a>Checkliste: Voraussetzung für bedingte Szenario:
--------------------------------------------------------------
Verbinden Sie Ihre Azure AD-Mandanten mit Ihrem lokalen Active Directory.

## <a name="configure-azure-active-directory-device-registration-service"></a>Konfigurieren von Azure-Active Directory-Gerät Registration Service
Verwenden Sie dieses Handbuch zum Bereitstellen und Konfigurieren von Azure Active Directory-Gerät Registrierung-Dienst für Ihre Organisation ein.

Mit diesem Leitfaden wird davon ausgegangen, dass Sie Windows Server Active Directory konfiguriert haben und auf Microsoft Azure Active Directory abonniert haben. Finden Sie unter Voraussetzungen für oben.

Führen Sie zum Bereitstellen von Azure Active Directory Gerät Registration Service mit Ihrem Azure Active Directory-Mandanten, die Aufgaben in der folgenden Prüfliste, in der Reihenfolge ein. Wenn ein Bezug Hyperlink führt zu einem Thema, diese Checkliste für zurückzukehren, nachdem Sie das Thema überprüfen, dass die verbleibenden Vorgänge in dieser Prüfliste fortgesetzt werden kann. Einige Vorgänge werden einen Szenario Überprüfungsschritt enthalten, der Ihnen helfen, zu bestätigen, dass der Schritt erfolgreich abgeschlossen wurde.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Teil 1: Aktivieren Azure-Active Directory-Gerät Registrierung

Führen Sie die Prüfliste zum Aktivieren und Konfigurieren der Azure Active Directory-Gerät Registrierung-Dienst unten aus.

| Aufgabe                                                                                                                                                                                                                                                                                                                                                                                             | Bezug                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Aktivieren Sie in Ihrem Mandanten Azure Active Directory für die Teilnahme am Arbeitsplatz Geräte zulassen Gerät Registrierung. Standardmäßig ist die kombinierte Authentifizierung für den Dienst nicht aktiviert. Mehrstufige Authentifizierung wird jedoch empfohlen, wenn Sie ein Gerät zu registrieren. Vor der Aktivierung der kombinierte Authentifizierung in ADRS, stellen Sie sicher, dass AD FS für eine kombinierte Authentifizierung konfiguriert ist. | [Azure-Active Directory-Gerät Registrierung aktivieren](active-directory-conditional-access-device-registration-overview.md)               |
| Geräte werden Ihre Azure Active Directory-Gerät Registrierung-Dienst ermitteln, indem Sie wonach bekannten DNS-Einträge zu können. Sie müssen Ihr Unternehmen DNS so konfigurieren, dass Geräte Ihrer Azure Active Directory-Gerät Registrierung-Dienst ermitteln können.                                                                                                                                                   | [Konfigurieren von Azure Active Directory-Gerät Registrierung Discovery.](active-directory-conditional-access-device-registration-overview.md) |

##<a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Teil 2: Bereitstellen und Konfigurieren von Windows Server 2012 R2 Active Directory Federation Services eine Beziehung Föderation mit Azure AD-einrichten

| Aufgabe                                                                                                                                                                                                                                                                                                                                                                                             | Bezug                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Bereitstellen von Active Directory-Domänendiensten Domäne mit den Windows Server 2012 R2 Schema Erweiterungen. Sie müssen nicht die Domänencontroller auf Windows Server 2012 R2 aktualisiert. Das Schema aktualisieren besteht die einzige Anforderung an. | [Aktualisieren Sie Ihrer Active Directory-Domäne Services Schema](#upgrade-your-active-directory-domain-services-schema)               |
| Geräte werden Ihre Azure Active Directory-Gerät Registrierung-Dienst ermitteln, indem Sie wonach bekannten DNS-Einträge zu können. Sie müssen Ihr Unternehmen DNS so konfigurieren, dass Geräte Ihrer Azure Active Directory-Gerät Registrierung-Dienst ermitteln können.                                                                                                                                                   | [Bereiten Sie Ihrer Active Directory-Support-Geräte vor](#prepare-your-active-directory-to-support-devices) |


##<a name="part-3-enable-device-writeback-in-azure-ad"></a>Teil 3: Aktivieren Gerät abgeschlossenen writebackvorgängen in Azure AD-

| Aufgabe                                                                                                                                                                                                                                                                                                                                                                                             | Bezug                                                       |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| Führen Sie die Aktivierung Gerät abgeschlossenen writebackvorgängen in Azure AD-Verbindung herstellen, Teil 2. Nach Abschluss des Vorgangs zurückgeben Sie dies in diesem Handbuch. | [Aktivieren der Gerät abgeschlossenen writebackvorgängen in Azure AD-Verbindung herstellen](#upgrade-your-active-directory-domain-services-schema)               |


##<a name="optional-part-4-enable-multi-factor-authentication"></a>[Optional] Teil 4: Aktivieren kombinierte Authentifizierung

Es wird dringend empfohlen, dass Sie eine der Optionen für mehrstufige Authentifizierung mehrere konfigurieren. Wenn Sie MFA anfordern möchten, finden Sie unter [auswählen die kombinierte Lösung für Sie](../multi-factor-authentication/multi-factor-authentication-get-started.md). Er enthält eine Beschreibung der einzelnen Lösung sowie Links zu helfen Ihnen die Konfiguration der Lösung Ihrer Wahl.

## <a name="part-5-verification"></a>Teil 5: Überprüfung

Die Bereitstellung ist abgeschlossen. Sie können nun einige Szenarien ausprobieren. Führen Sie die folgenden Links, um experimentieren Sie mit dem Dienst und mit den Features vertraut machen


| Aufgabe                                                                                                                                                                                                                         | Bezug                                                                       |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Teilnehmen an einigen Geräten zu Ihrem Arbeitsplatz mit Azure Active Directory-Gerät Registrierung. Sie können iOS, Windows und Android-Geräten teilnehmen.                                                                                         | [Teilnehmen an Geräte zu Ihrem Arbeitsplatz mit Azure Active Directory-Gerät Registrierung](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Sie können angezeigt und registrierte Geräte mithilfe der Administratorportal aktivieren/deaktivieren. In dieser Aufgabe werden Sie einige registrierte Geräte mithilfe der Administratorportal anzeigen.                                                        | [Azure-Active Directory-Gerät Registrierung (Übersicht)](active-directory-conditional-access-device-registration-overview.md)                             |
| Stellen Sie sicher, dass Geräteobjekte wieder aus Azure Active Directory auf Windows Server Active Directory geschrieben werden.                                                                                                                  | [Überprüfen Sie, ob registrierten Geräte geschrieben zurück in Active Directory](#verify-registered-devices-are-written-back-to-active-directory)                  |
| Jetzt, dass Benutzer aktivierten Geräte erfassen können, können Sie die Anwendung erstellen Richtlinien in AD FS, die nur registrierte Geräten ermöglichen. In dieser Aufgabe, die Sie erstellen Zugriff auf Access eine Regel für eine Anwendung und ein benutzerdefiniertes abgelehnte Nachricht | [Erstellen einer Anwendung Zugriffsrichtlinie und benutzerdefinierte Zugriff verweigert](#create-an-application-access-policy-and-custom-access-denied-message)            |



## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Integrieren von Azure-Active Directory mit lokalen Active Directory
Dies hilft Ihnen Ihre Azure AD-Mandanten mit Ihrem lokalen active Directory, mit Azure AD verbinden integrieren. Obwohl die Schritte in der klassischen Azure-Portal verfügbar sind, notieren Sie alle Inhalten Anweisungen in diesem Abschnitt aufgelisteten.

1.  Melden Sie sich mit einem Konto an, die ein globaler Administrator Azure AD ist im klassischen Azure-Portal an.
2.  Wählen Sie im linken Bereich aus **Active Directory**.
3.  Wählen Sie auf der Registerkarte **Verzeichnis** aus Ihrem Verzeichnis.
4.  Wählen Sie die Registerkarte **Verzeichnisintegration** aus.
5.  Führen Sie die Schritte 1 bis 3 Azure Active Directory mit Ihrem lokalen Verzeichnis integriert werden soll, unter Abschnitt **Bereitstellen und verwalten** .
  1.    Fügen Sie Domänen hinzu.
  2.    Installieren und Ausführen von Azure AD verbinden: Installieren Azure AD Verbinden mit den folgenden Anweisungen, [benutzerdefinierte Installation von Azure AD verbinden](./connect/active-directory-aadconnect-get-started-custom.md).
  3. Überprüfen und Verwalten von Verzeichnis synchronisieren. Anweisungen für einzelne Zeichen stehen in diesem Schritt.

  > [AZURE.NOTE]
  > Konfigurieren des Verbunds mit AD FS, entsprechend der Anleitung über verknüpft. Sie müssen nicht die Vorschau-Features konfigurieren.


## <a name="upgrade-your-active-directory-domain-services-schema"></a>Aktualisieren Sie Ihrer Active Directory-Domänendiensten schema

> [AZURE.NOTE]
> Aktualisieren Ihrer Active Directory-Schema kann nicht rückgängig gemacht werden. Es wird empfohlen, dass Sie zunächst diese in einer Umgebung für ausführen.

1. Melden Sie sich an Ihre Domänencontroller mit einem Konto an, die sowohl Organisations-Admin-Schema-Administrator über Berechtigungen verfügt.
2. Kopieren von **[Media] \support\adprep** Directory und Unterverzeichnisse auf einen der Controller Ihrer Active Directory-Domäne.
3. Dabei ist [Media] den Pfad zu der Windows Server 2012 R2 Installationsmedien.
4. Navigieren Sie zu dem Verzeichnis Adprep ein Eingabeaufforderungsfenster, und führen Sie: **adprep.exe/ForestPrep**. Führen Sie auf dem Bildschirm beschrieben vor, um das Schemaupgrade abgeschlossen.

## <a name="prepare-your-active-directory-to-support-devices"></a>Bereiten Sie Ihrer Active Directory zur Unterstützung von Geräten vor

>[AZURE.NOTE] Dies ist, die Sie ausführen müssen, um Ihre Active Directory-Struktur zur Unterstützung von Geräten vorbereiten einmalig. Sie müssen mit Administratorberechtigungen Enterprise angemeldet sein, und Ihre Active Directory-Struktur müssen das Schema Windows Server 2012 R2, um dieses Verfahren ausführen.


##<a name="prepare-your-active-directory-forest-to-support-devices"></a>Bereiten Sie Ihrer Active Directory-Struktur zur Unterstützung von Geräten vor

> [AZURE.NOTE]
>Dies ist, die Sie ausführen müssen, um Ihre Active Directory-Struktur zur Unterstützung von Geräten vorbereiten einmalig. Sie müssen mit Administratorberechtigungen Enterprise angemeldet sein, und Ihre Active Directory-Struktur müssen das Schema Windows Server 2012 R2, um dieses Verfahren ausführen.

### <a name="prepare-your-active-directory-forest"></a>Bereiten Sie Ihrer Active Directory-Struktur vor

1.  Öffnen Sie auf dem Server Föderation eine Windows PowerShell-Befehlsfenster und Typ: Initialisierung-ADDeviceRegistration
2.  Wenn Sie für **ServiceAccountName**aufgefordert werden, geben Sie den Namen des Dienstkontos, das Sie als Dienstkonto für AD FS ausgewählt haben. Wenn sie eine gMSA-Konto handelt, geben Sie das Konto im Format$ **Schreibweise Domäne\Benutzername an** . Verwenden Sie für ein Domänenkonto die Format- **Schreibweise Domäne\Benutzername an**.



### <a name="enable-device-authentication-in-ad-fs"></a>Aktivieren Sie die Geräteauthentifizierung in AD FS

1. Klicken Sie auf dem Server Föderation öffnen die AD FS-Verwaltungskonsole, und navigieren Sie zu dem **AD FS** > **Authentifizierungsrichtlinien**.
2. Wählen Sie **Bearbeiten globale primären Authentifizierung...** aus dem Bereich **Aktionen** .
3. Aktivieren Sie die **Geräteauthentifizierung aktivieren** , und wählen Sie dann auf**OK**.
4. Standardmäßig werden AD FS regelmäßig nicht verwendete Geräte aus Active Directory entfernt. Wenn Sie Azure Active Directory-Gerät Registrierung verwenden, damit Geräte in Azure verwaltet werden können, müssen Sie diese Aufgabe deaktivieren.


### <a name="disable-unused-device-cleanup"></a>Deaktivieren Sie nicht verwendete Gerät zum Aufräumen
1. Öffnen Sie auf dem Server Föderation eine Windows PowerShell-Befehlsfenster und Typ: Set-AdfsDeviceRegistration - MaximumInactiveDays 0

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Vorbereiten von Azure AD verbinden für Gerät abgeschlossenen writebackvorgängen

1.  Führen Sie Teil 1: Vorbereiten Azure AD verbinden.


## <a name="join-devices-to-your-workplace-using-azure-active-directory-device-registration"></a>Teilnehmen an Geräte zu Ihrem Arbeitsplatz mit Azure Active Directory-Gerät Registrierung

### <a name="join-an-ios-device-using-azure-active-directory-device-registration"></a>Teilnehmen an einem iOS-Gerät mit Azure Active Directory-Gerät Registrierung

Azure Active Directory-Gerät-Registrierung verwendet den Registrierungs-Prozess Over-the-Air Profil für iOS-Geräte. Dieser Prozess beginnt mit dem Herstellen einer Verbindung mit dem Profil Registrierungs-URL mit dem Webbrowser Safari Benutzer. Das URL-Format ist wie folgt aus:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

Wo `yourdomainname` ist der Domänenname, die Sie mit Azure Active Directory konfiguriert haben. Beispielsweise, wenn Sie Ihren Domänennamen "contoso.com" ist, wäre die URL:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Es gibt viele verschiedene Arten, kommunizieren diese URL für Ihre Benutzer aus. Es wird empfohlen, eine, veröffentlichen Sie diese URL in einer benutzerdefinierten Anwendungszugriff verweigert Nachricht in AD FS. Dies wird im Abschnitt anstehende behandelt: [Erstellen einer Anwendung Zugriffsrichtlinie und benutzerdefinierte Zugriff verweigert wird](#create-an-application-access-policy-and-custom-access-denied-message).

###<a name="join-a-windows-81-device-using-azure-active-directory-device-registration"></a>Teilnehmen an einer Azure Active Directory-Gerät Registration wird mit Windows 8.1-Gerät

1. Navigieren Sie auf Ihrem Gerät Windows 8.1 zu **PC Settings** > **Netzwerk** > **Arbeitsplatz**.
2. Geben Sie Ihren Benutzernamen im UPN-Format ein. Beispielsweise dan@contoso.com..
3. Wählen Sie **Verknüpfung**aus.
4. Wenn Sie dazu aufgefordert werden, Anmeldung mit Ihren Anmeldeinformationen. Das Gerät wird jetzt verknüpft.

###<a name="join-a-windows-7-device-using-azure-active-directory-device-registration"></a>Teilnehmen an einer Azure Active Directory-Gerät Registration wird mit Windows 7-Gerät
Wenn Sie Windows 7-Domäne registriert verknüpft, Geräte, die Sie das Gerät Registrierung Software-Paket bereitstellen müssen. Software-Paket heißt Arbeitsplatz teilnehmen für Windows 7 und auf der [Website Microsoft verbinden](https://connect.microsoft.com/site1164)zum Download verfügbar ist. Anleitung zum Verwenden des Pakets finden Sie unter [Konfigurieren automatische Gerät Registrierung für Windows 7-Domäne beigetreten Geräte](active-directory-conditional-access-automatic-device-registration-windows7.md).

### <a name="join-an-android-device-using-azure-active-directory-device-registration"></a>Teilnehmen an einem Android-Gerät mit Azure Active Directory-Gerät Registrierung

Der [Azure-Authentifizierung für Android-Thema](active-directory-conditional-access-azure-authenticator-app.md) enthält Anweisungen zum Azure Authentifizierung app auf Ihrem Android-Gerät installieren und Hinzufügen eines Kontos Arbeit an. Wenn Sie ein Konto Arbeit auf einem Android-Gerät erfolgreich erstellt wurde, wird das Gerät Arbeitsplatz, die die Organisation angehören.

## <a name="verify-registered-devices-are-written-back-to-active-directory"></a>Überprüfen Sie, ob registrierten Geräte geschrieben zurück in Active Directory
Sie können anzeigen, und stellen Sie sicher, dass Ihr Geräteobjekte wieder in Ihrer Active Directory geschrieben wurden LDP.exe oder ADSIEdit verwenden. Mit den Tools Active Directory-Administrator verfügbar sind.

Standardmäßig können Geräteobjekte, die geschrieben Back aus Azure Active Directory sind in der gleichen Domäne wie Ihre AD FS-Farm abgelegt werden.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Erstellen einer Anwendung Zugriffsrichtlinie und benutzerdefinierte Zugriff verweigert
Stellen Sie folgendes Szenario: Erstellen einer Relying Party Trust in AD FS-Anwendung, und Konfigurieren einer Emission Autorisierungsregel, die nur registrierte Geräte ermöglicht. Jetzt dürfen nur Geräte, die registriert sind die Anwendung zugreifen. Um für Ihre Benutzer für den Zugriff auf die Anwendung zu vereinfachen, konfigurieren Sie eine benutzerdefinierte ' Zugriff verweigert ' Nachricht, die Anweisungen zum Beitreten Geräts enthält. Die Benutzer verfügen nun über eine nahtlose Möglichkeit, aktivierten Geräte registrieren, um eine Anwendung zugreifen zu können.

Die folgenden Schritte werden gezeigt, wie dieses Szenario implementiert werden.

>[AZURE.NOTE]
In diesem Abschnitt wird davon ausgegangen, dass Sie bereits eine verlassen Partner vertrauen für eine Anwendung in AD FS konfiguriert haben.

1. Öffnen Sie das Tool AD FS MMC, und navigieren Sie zu AD FS > Vertrauen Beziehungen > verlassen vertrauen.
2. Suchen Sie nach der Anwendung, für die diese neue Access Regel angewendet werden soll. Mit der rechten Maustaste in der Anwendungs, und wählen Sie bearbeiten anfordern Regeln...
3. Wählen Sie die Registerkarte **Emission Autorisierungsregeln** , und wählen Sie dann auf **Regel hinzufügen**
4. Wählen Sie aus der Vorlage **anfordern Regel** Dropdown-Liste **Zulassen oder verweigern Benutzer basierend auf einer eingehenden Anspruch**aus. Wählen Sie **Weiter**aus.
5. Im Regelnamen anfordern: Feldtyp: **Zugriff von registrierten Geräten zulassen**
6. Die eingehende beanspruchen Typ: Dropdownliste, wählen Sie **Benutzer aus registriert ist**.
7. Der eingehende beanspruchen Wert: Feld, geben Sie ein: **Wahr**
8. Wählen Sie das Optionsfeld **für Benutzer mit diesem eingehenden Anspruch Zugriff zulassen** .
9. Wählen Sie **Ende** aus, und wählen Sie dann auf **Übernehmen**.
10. Entfernen Sie alle Regeln, die mehr als die Regel Berechtigungen sind, die Sie soeben erstellt haben. Beispielsweise Entfernen der Standard-Regel **Access für alle Benutzer zulassen** .

Die Anwendung wird jetzt konfiguriert zugreifen dürfen nur, wenn der Benutzer auf einem Gerät stammt, die sie registriert und am Arbeitsplatz hinzugefügt. Für erweiterte Richtlinien, finden Sie unter [Verwalten von Risiken mit mehrstufige Access Control](https://technet.microsoft.com/library/dn280949.aspx).

Als Nächstes konfigurieren Sie eine benutzerdefinierte Fehlermeldung für eine Anwendung. Die Fehlermeldung zulassen, dass Benutzer wissen, dass diese Verknüpfung müssen Geräts am Arbeitsplatz, bevor sie Zugriff auf die Anwendung dürfen. Sie können eine benutzerdefinierte Anwendung ' Zugriff verweigert ' Mitteilung mithilfe einer benutzerdefinierten HTML- und Windows PowerShell erstellen.

Öffnen Sie auf dem Server Föderation ein Windows PowerShell-Befehl-Fenster zu, und geben Sie den folgenden Befehl ein. Ersetzen Sie Teile des Befehls mit Elementen, die auf Ihrem System beziehen:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Sie müssen Ihr Gerät registrieren, bevor Sie diese Anwendung zugreifen können.

**Wenn Sie einem iOS-Gerät verwenden, wählen Sie diesen Link zu Ihrem Gerät teilnehmen**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Teilnehmen an diesem iOS-Gerät an Ihrem Arbeitsplatz.


**Wenn Sie ein Windows 8.1-Gerät verwenden**, können Sie Ihr Gerät verknüpfen, indem Sie auf **PC-Einstellungen ** >  **Netzwerk** > **Arbeitsplatz**.


Wobei "**verlassen Partei Trust Name**" den Namen des Objekts verlassen Partei Trust Applications in AD FS ist.
Dabei ist **IhreDomäne.com** den Namen der Domäne, den Sie mit Azure Active Directory konfiguriert haben. Beispielsweise "contoso.com".
Achten Sie darauf, dass alle Zeilenumbrüche (falls vorhanden) aus der HTML-Inhalt zu entfernen, die Sie an das Cmdlet " **Set-AdfsRelyingPartyWebContent** " übergeben.


Jetzt, wenn Benutzer eine Anwendung auf einem Gerät, die nicht mit dem Azure Active Directory Gerät Registrierung Service registriert ist zugreifen, empfängt eine Seite diese, die so Screenshot unten aussieht.

![Screeshot, der einen Fehler zurück, wenn Benutzer Geräts mit Azure AD registriert haben](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)

##<a name="related-articles"></a>Verwandte Artikel

- [Artikel Index für Anwendungsverwaltung in Azure-Active Directory](active-directory-apps-index.md)
