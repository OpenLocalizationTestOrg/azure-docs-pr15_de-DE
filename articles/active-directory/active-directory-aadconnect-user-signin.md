<properties
    pageTitle="Azure AD verbinden: Benutzer anmelden | Microsoft Azure"
    description="Azure AD verbinden Benutzer anmelden für benutzerdefinierte Einstellungen."
    services="active-directory"
    documentationCenter=""
    authors="billmath"
    manager="femila"
    editor="curtand"/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/16/2016"
    ms.author="billmath"/>



# <a name="azure-ad-connect-user-sign-on-options"></a>Azure AD verbinden Benutzer melden Sie sich auf Optionen

Azure AD verbinden kann Ihre Benutzer bei der Cloud, und klicken Sie auf lokale Ressourcen mit denselben Kennwörtern auf. In diesem Artikel werden die wichtigsten Punkte für jede Identitätsmodell einfacher auswählen die Identität, dass Sie für Ihre Anmelden bei Azure AD verwenden möchten.

Wenn Sie bereits mit Azure AD-Identitätsmodell vertraut und Weitere Informationen zu einer bestimmten Methode möchten, nur klicken Sie unten auf den entsprechenden Thema.

* [Kennwort synchronisieren](#password-synchronization)
* [Partnerverbundkontakte SSO (mit ADFS)](#federation-using-a-new-or-existing-ad-fs-in-windows-server-2012-r2-farm)


## <a name="choosing-a-user-sign-in-method"></a>Auswählen einer Benutzer anmelden Methode
Für die meisten Organisationen, die nur Benutzer aktivieren möchten, die sich bei Office 365 anmelden, wird SaaS-Anwendungen und andere Azure AD-Grundlage Ressourcen, die standardmäßige Kennwort Synchronisierungsoption empfohlen werden.
Einige Organisationen haben jedoch besondere Gründe für die Verwendung von partnerverbundkontakte bei der Anmeldung die Option wie AD FS.  Hierzu gehören:

- Ihre Organisation bereits hat AD FS oder eine 3rd party Föderation Anbieter bereitgestellt
- Ihre Sicherheitsrichtlinie untersagt synchronisieren Kennworthashes in der cloud
- Benötigen Sie, dass Benutzer nahtlose SSO erzielen Sie (ohne zusätzliche Kennwort auffordert) Autos Domäne Cloudressourcen zugreifen auf das Unternehmensnetzwerk verknüpft werden.
- Sie benötigen einige Funktionen, die bestimmten AD FS wird
    - Lokale kombinierte Authentifizierung mithilfe einer Drittanbieter-Anbieter oder Smart-Karten (Weitere Informationen zu Drittanbietern MFA-Anbieter für AD FS in Windows Server 2012 R2)
    - Active Directory-Integration-Funktionen, wie etwa weiche Konto sperren oder AD Kennwort und Arbeit Stunden Richtlinie
    - Bedingte Zugriff auf beide lokalen und cloud Ressourcen mithilfe der Registrierung Gerät, Azure AD-Verknüpfung oder Intune MDM Richtlinien

### <a name="password-synchronization"></a>Synchronisierung von Kennwörtern
Mit der Synchronisierung von Kennwörtern werden Hashes Benutzerkennwörter zu Azure AD aus Ihrem lokalen Active Directory synchronisiert.  Wenn Kennwörter lokal zurücksetzen oder geändert werden, werden die neuen Kennwörter sofort zu Azure AD synchronisiert, damit Ihre Benutzer dasselbe Kennwort immer für Cloudressourcen verwenden, und können wie lokal.  Die Kennwörter werden nie gesendet Azure AD noch in Azure AD als Klartext gespeichert.
Synchronisierung von Kennwörtern kann zusammen mit Kennwort schreiben-Back self aktivieren Dienstkennwort in Azure AD Zurücksetzen verwendet werden.

<center>![Cloud](./media/active-directory-aadconnect-user-signin/passwordhash.png)</center>

[Weitere Informationen zu Synchronisierung von Kennwörtern](active-directory-aadconnectsync-implement-password-synchronization.md)


### <a name="federation-using-a-new-or-existing-ad-fs-in-windows-server-2012-r2-farm"></a>Föderation mit einer neuen oder vorhandenen AD FS in Windows Server 2012 R2 farm
Mit partnerverbundkontakte melden Sie sich auf können die Benutzer in Azure AD-basierten Services mit ihrer lokalen Kennwörter und, klicken Sie auf das Unternehmensnetzwerk, melden Sie sich auf ohne ihre Kennwörter erneut eingeben zu müssen.  Die Option Föderation mit AD FS können Sie ein neues bereitstellen oder einer vorhandenen AD FS in Windows Server 2012 R2 Farm angeben.  Wenn Sie eine vorhandene Serverfarm angeben, wird Azure AD verbinden die Vertrauensstellung zwischen der Farm und Azure AD-so konfigurieren, dass die Benutzer anmelden können, klicken Sie auf.

<center>![Cloud](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="to-deploy-federation-with-ad-fs-in-windows-server-2012-r2-you-will-need-the-following"></a>Um einen Partnerverbund mit ADFS in Windows Server 2012 R2 bereitstellen, benötigen Sie Folgendes

Wenn Sie eine neue Farm bereitstellen:

- Ein Windows Server 2012 R2-Server für die Föderation.
- Ein Windows Server 2012 R2-Server für die Web-Proxy-Anwendung.
- eine PFX-Datei mit einem SSL-Zertifikat für Ihren vorgesehenen Föderation Dienstnamen, wie z. B. fs.contoso.com.

Wenn Sie eine neue Farm bereitstellen oder verwenden eine vorhandene Farm:

- Lokale Administratorrechte auf Ihren Servern Föderation.
- Lokale Administratorrechte auf eine beliebige Arbeitsgruppe (ohne Beitritt zu Domäne) Server, auf dem Sie die Rolle des Web-Anwendungsproxy bereitstellen möchten.
- Der Computer, auf dem Sie den Assistenten ausführen, müssen Verbindung zu einem beliebigen anderen Computern hergestellt auf dem AD FS oder Web Anwendungsproxy über Windows Remote Management installiert werden soll.

[Konfigurieren von SSO mit AD FS](./aad-connect/active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) 

#### <a name="sign-on-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Melden Sie sich auf eine frühere Version von AD FS verwendet oder eine Lösung eines Drittanbieters

Wenn Sie mit einer früheren Version von AD FS (z. B. AD FS 2.0) oder einer Drittanbieter-Anbieter Föderation bereits Cloud anmelden konfiguriert haben, können Sie entscheiden Benutzer anmelden Konfiguration über Azure AD verbinden überspringen.  Dies ermöglicht Ihnen die letzte Synchronisierung und andere Funktionen des Azure AD verbinden gleichzeitiger Verwendung Ihrer vorhandene Lösung für melden Sie sich auf abrufen.

[Azure Active Directory Federation Drittanbieter-Kompatibilitätsliste](./active-directory-aadconnect-federation-compatibility.md)

## <a name="user-sign-in-and-user-principal-name-upn"></a>Benutzer anmelden und Benutzerprinzipalnamen (UPN)

### <a name="understanding-user-principal-name"></a>Grundlegendes zu Benutzerprinzipalnamen

In Active Directory ist das standardmäßige UPN-Suffix der DNS-Name der Domäne, in dem Benutzerkonto erstellt. Dies ist in den meisten Fällen den Domänennamen registriert ist, wie die Enterprise-Domäne im Internet. Sie können jedoch weitere Benutzerprinzipalnamen-Suffixe mit Active Directory-Domänen und-Vertrauensstellungen hinzufügen.

Der UPN des Benutzers ist Format username@domai. Angenommen, für ein lokales active Directory contoso.com Benutzer Johann haben Benutzerprinzipalnamen john@contoso.com. Der UPN des Benutzers basiert auf RFC 822. Obwohl Benutzerprinzipalnamen und e-Mail-das gleiche Format freigeben, wird der Wert der UPN für einen Benutzer möglicherweise oder möglicherweise nicht gleich der e-Mail-Adresse des Benutzers.

### <a name="user-principal-name-in-azure-ad"></a>Benutzerprinzipalnamen in Azure AD-

Azure AD verbinden-Assistent wird verwenden Sie das Attribut UserPrincipalName oder lassen Sie das Attribut (in die benutzerdefinierte Installation) angeben, um aus lokalen als den Benutzerprinzipalnamen in Azure AD verwendet werden. Dies ist der Wert, der für die Anmeldung bei Azure AD verwendet werden. Wenn der Wert der Benutzer Benutzerprinzipalnamen-Attribut eine Domäne überprüft in Azure AD keinem, klicken Sie dann Azure AD wird durch Ersetzen eines Standardwerts. onmicrosoft.com-Wert.

Jedes Verzeichnis in Azure Active Directory im Lieferumfang von integrierten Domänennamen in das Formular contoso.onmicrosoft.com, mit dem Sie erste Schritte mit Azure oder anderen Microsoft-Diensten. Sie können verbessern und Anmeldeverhalten Verwendung von benutzerdefinierten Domänen zu vereinfachen. Informationen zu benutzerdefinierten Domäne lesen Namen in Azure AD- und so überprüfen Sie eine Domäne, Sie [Hinzufügen Ihrer benutzerdefinierten Domänennamen zu Azure Active Directory](active-directory-add-domain.md#add-your-custom-domain-name-to-azure-active-directory)

## <a name="azure-ad-sign-in-configuration"></a>Azure AD-Anmeldung-Konfiguration

### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Azure AD-in Konfiguration mit Azure AD-verbinden
Azure AD Anmeldeverhalten ist abhängig davon, ob Azure AD entsprechen das UPN-Suffix eines Benutzers Nachschlagen in eine benutzerdefinierte Domänen im Verzeichnis Azure AD-überprüft synchronisiert werden kann. Azure AD verbinden bietet Hilfe beim Konfigurieren Azure AD-Anmeldung Einstellungen so, dass Benutzer Anmeldeverhalten in der Cloud ähnlich wie einen lokalen befindet. Azure AD verbinden Listet die Benutzerprinzipalnamen-Suffixe für die Domänen definiert und versucht, die sie mit einer benutzerdefinierten Domäne in Azure AD entsprechen und hilft Ihnen, mit der entsprechenden Aktion, die ausgeführt werden muss.
Azure AD-Anmeldeseite, die UPN Suffixe definiert für lokalen Active Directory-Listen und zeigt den entsprechenden Status für jedes Suffix an. Die Statuswerte kann eine von der unter:

| Bundesstaat | Beschreibung | Aktion erforderlich |
|:----|:----|:----|
|Überprüft| Verbinden von Azure AD gefundenen in Azure Active Directory eine entsprechende Domäne überprüft werden. Alle Benutzer für diese Domäne können Anmeldung ihre Anmeldeinformationen lokal verwenden| Es ist keine Maßnahme erforderlich. |
|Nicht überprüft| Azure AD Verbinden gefunden eine übereinstimmende benutzerdefinierte Domäne in Azure AD, aber es ist nicht überprüft. Benutzerprinzipalnamen-Suffix für die Benutzer dieser Domäne wird geändert werden auf Standard. onmicrosoft.com Suffix nach synchronisieren, wenn die Domäne nicht überprüft wurde. | Überprüfen Sie die benutzerdefinierte Domäne in Azure AD aus. [Weitere Informationen](./active-directory-add-domain.md#verify-the-domain-name-with-azure-ad) |  
|Nicht hinzugefügt.| Eine benutzerdefinierte Domäne mit dem UPN Suffix entsprechende Azure AD Verbinden nicht gefunden. Benutzerprinzipalnamen-Suffix für Benutzer in dieser Domäne wird geändert werden auf Standard. "onmicrosoft.com", wenn die Domäne nicht hinzugefügt wird und Verifeid in Azure.| Hinzufügen und Überprüfen einer benutzerdefinierten Domänennamens, die mit dem UPN Suffix [Weitere](./active-directory-add-domain.md) entspricht|

Azure AD-Anmeldeseite Listet die Benutzerprinzipalnamen Suffix(s) für lokalen Active Directory und den entsprechenden benutzerdefinierten Domäne in Azure AD mit den aktuellen Überprüfungsstatus definiert. In die benutzerdefinierte Installation können Sie jetzt das Attribut für Benutzerprinzipalnamen auf der Seite **Azure AD-anmelden** auswählen.

![Azure AD-Anmeldeseite](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Sie können auf die Aktualisierungsschaltfläche, den aktuellen Status der benutzerdefinierten Domänen aus Azure AD erneut abzurufen klicken.

###<a name="selecting-attribute-for-user-principal-name-in-azure-ad"></a>Attribut für Benutzerprinzipalnamen Azure AD auswählen

UserPrincipalName - Attribut UserPrincipalName ist das Attribut Benutzer verwendet werden, wenn er Azure AD anmelden und Office 365. Die Domänen verwendet, auch bekannt als das Benutzerprinzipalnamen-Suffix, sollten in Azure AD, damit die Benutzer synchronisiert werden überprüft werden. Es wird dringend empfohlen, den standardmäßigen Attribut UserPrincipalName beibehalten. Wenn dieses Attribut nicht geroutet ist und kann nicht bestätigt werden, ist es möglich, wählen Sie ein anderes Attribut aus, beispielsweise e-Mail, wie das Attribut, halten die Anmelde-ID Dies wird als alternative ID bezeichnet. Alternativer Wert muss den standardmäßigen RFC822 folgen. Mit Kennwort für einmaliges Anmelden (SSO) und Föderation SSO als die Lösung Anmeldung kann eine alternative Kennung verwendet werden.

>[AZURE.NOTE] Verwenden eine alternative Kennung ist nicht mit allen Office 365-Auslastung kompatibel. Weitere Informationen finden Sie unter [Konfigurieren von alternativen Anmelde-ID](https://technet.microsoft.com/library/dn659436.aspx).

#### <a name="different-custom-domain-states-and-effect-on-azure-sign-in-experience"></a>Andere benutzerdefinierte Domäne Zuständen und wirkt sich auf Azure Anmeldeverhalten
Es ist wichtig, die Beziehung zwischen den Status der benutzerdefinierten Domäne in Ihrem Verzeichnis Azure AD- und UPN-Suffixe definiert lokalen. Lassen Sie uns aufzurufen Sie, die anderen möglichen Azure-in Erfahrung beim Einrichten Sycnhronization Azure AD-Verbindung über AirPort verwenden.

Die folgenden Informationen ein, lassen Sie uns davon aus, dass wir mit dem UPN Suffix "contoso.com" betreffenden sind die im lokalen Verzeichnis als Teil des UPN, beispielsweise verwendet wird user@contoso.com.

###### <a name="express-settings--password-synchronization"></a>Express-Einstellungen / Synchronisierung von Kennwörtern
| Bundesstaat         | Auswirkung auf Benutzerfunktionalität Azure anmelden |
|:-------------:|:----------------------------------------|
| Nicht hinzugefügt. | In diesem Fall wurde keine benutzerdefinierte Domäne für contoso.com in Azure AD-Verzeichnis hinzugefügt. Benutzer, die lokale mit Suffix UPN besitzen @contoso.com, werden nicht mit ihrem lokalen Benutzerprinzipalnamen Azure anmelden können. Sie müssen stattdessen einen neuen UPN gesendetes Azure AD durch Hinzufügen des Suffixes für Standard-Azure AD-Verzeichnis zu verwenden. Wenn die Benutzer Azure AD-Verzeichnis azurecontoso.onmicrosoft.com klicken Sie dann auf den lokalen Benutzer synchronisiert werden beispielsweise user@contoso.com erhält eine UPN deruser@azurecontoso.onmicrosoft.com|
| Nicht überprüft | In diesem Fall müssen wir eine benutzerdefinierte Domäne contoso.com in Azure AD-Verzeichnis hinzugefügt, jedoch noch nicht überprüft wird. Wenn Sie im voraus mit Synchronisierung Benutzer ohne Überprüfung der Domäne zugreifen, werden dann Benutzer zugewiesen einen neuen UPN von Azure Active Directory, so wie es im Szenario 'Nicht hinzugefügten' gemacht haben.|
| Überprüft | In diesem Fall müssen wir eine benutzerdefinierte Domäne contoso.com bereits hinzugefügt und in Azure AD für das UPN-Suffix überprüft. Die Benutzer können ihren lokalen Benutzerprinzipalnamen, z. B. mit user@contoso.com, in Azure anmelden, nachdem sie auf Azure Active Directory synchronisiert werden|

###### <a name="ad-fs-federation"></a>AD FS-Verbund
Sie können eine Föderation mit Standard können nicht erstellt. "onmicrosoft.com"-Domäne in Azure AD- oder eine nicht überprüft benutzerdefinierten Domäne in Azure AD. Wenn Sie im Assistenten Azure AD verbinden ausgeführt werden, wenn Sie eine nicht überprüfte Domäne erstellen auswählen fordert eine Föderation mit dann Azure AD verbinden Sie mit der erforderlichen Einträge erstellt werden, wo der DNS-Einträge für die Domäne gehostet wird. Weitere Informationen finden Sie [hier](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Wenn Sie Benutzer anmelden Option als "Föderation mit AD FS" ausgewählt haben, müssen Sie eine benutzerdefinierte Domäne weiterhin bei der Erstellung einer Föderation in Azure AD verfügen. Für diese Diskussion bedeutet dies, dass wir eine benutzerdefinierte Domäne contoso.com in Azure AD-Verzeichnis hinzugefügt haben, sollten an.

| Bundesstaat         | Auswirkung auf Benutzerfunktionalität Azure anmelden |
|:-------------:|:----------------------------------------|
| Nicht hinzugefügt. | In diesem Fall Azure AD Verbinden nicht übereinstimmende benutzerdefinierte Domäne für die UPN Suffix contoso.com in Azure AD-Verzeichnis gefunden. Sie müssen eine benutzerdefinierte Domäne contoso.com hinzufügen, wenn Sie Benutzern die Anmeldung mit AD FS mit ihrem lokalen Benutzerprinzipalnamen wie benötigen user@contoso.com.|
| Nicht überprüft | In diesem Fall fordert Azure AD verbinden Sie mit entsprechenden Details auf, wie Sie Ihre Domäne zu einem späteren Zeitpunkt überprüfen können|
| Überprüft | In diesem Fall anstehen mit der Konfiguration ohne weitere Aktion zu gelangen|  

## <a name="changing-user-sign-in-method"></a>Ändern der Benutzer anmelden Methode

Sie können die Benutzer anmelden Methode aus Föderation in Kennwort synchronisieren mit den verfügbaren Aufgaben in Azure AD Verbinden nach der erstmaligen Konfiguration von Azure AD Verbinden mit dem Assistenten ändern. Den Azure AD verbinden-Assistenten erneut ausführen, und es wird eine Liste der Aufgaben, die Sie ausführen können angezeigt werden. Wählen Sie in der Liste der Vorgänge **ändern Benutzer anmelden** . 

![Ändern der Benutzer anmelden"](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Klicken Sie auf der nächsten Seite werden Sie aufgefordert, die Anmeldeinformationen für Azure AD bereitstellen.

![Verbinden mit Azure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Wählen Sie auf der Seite **Benutzer anmelden** **Synchronisierung von Kennwörtern**aus. Hiermit wird Verzeichnis aus, zu einer verwalteten Partnersuche geändert.

![Herstellen einer Verbindung Azure AD mit](./media/active-directory-aadconnect-user-signin/changeusersignin3.png)

>[AZURE.NOTE] Wenn Sie nur eine temporäre wechseln zu Synchronisierung von Kennwörtern erstellen möchten, aktivieren Sie dann die **Benutzerkonten nicht konvertieren**. Nicht auf die Option Auschecken führt zum Konvertieren eines einzelnen Benutzers verbunden, und es kann einige Stunden dauern.
  
## <a name="next-steps"></a>Nächste Schritte
Erfahren Sie mehr über die [Integration von Ihrem lokalen Identitäten mit Azure Active Directory](active-directory-aadconnect.md).

Erfahren Sie mehr über [Azure AD verbinden: Entwerfen Konzepte](active-directory-aadconnect-design-concepts.md)


