<properties
    pageTitle="Verwenden Windows-10-Geräte in Ihrem Arbeitsplatz | Microsoft Azure"
    description="Stellt eine Momentaufnahme der Funktionen für Benutzer und IT, ein Vergleich der verschiedenen Arten ein Gerät nach der Bereitstellung und in einem Unternehmen mit Windows 10 verwendet werden kann."
    services="active-directory"
    documentationCenter=""
    authors="femila"
    manager="swadhwa"
    editor=""
    tags="azure-classic-portal"/>

<tags
    ms.service="active-directory"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/17/2016"
    ms.author="femila"/>

# <a name="using-windows-10-devices-in-your-workplace"></a>Verwenden Windows 10 Geräte in Ihrem Arbeitsplatz

Gilt für: Windows 10 PCs

Windows-10 bietet drei Modelle für Organisationen, die Benutzer auf Ressourcen der Art Arbeit in eine sichere und bequeme Möglichkeit zugreifen können.

- **Azure-Active Directory teilnehmen an.** (Azure AD Verknüpfung) nach Arbeitskräften, die Zugriff auf Ressourcen wie Office 365 hauptsächlich in der Cloud. Azure AD-Verknüpfung ist Self-service-Arbeit provisioning Erfahrung, das in Windows 10 neu ist.
- **Beitreten zu einer Domäne**und Organisationen, die Investitionen in lokalen apps und Ressourcen haben. Beitreten zu einer Domäne bietet eine verbesserte Oberfläche in Windows 10 Wenn mit Azure AD verbunden.
- **Neue BYOD einfacheres**für Benutzer, die ein Konto bei Arbeit oder Schule Windows und einfach Zugriff auf Ressourcen auf persönlichen Geräten hinzufügen möchten.

Die folgende Tabelle zeigt eine Momentaufnahme der Funktionen für Benutzer und IT-Administratoren, die ein Vergleich der verschiedenen Arten, die ein Gerät nach der Bereitstellung und in einem Unternehmen mit Windows 10 verwendet werden kann:

|                                                                                                                                                                 | Beitreten zu einer Domäne     | Azure AD-Verknüpfung | Persönliches Gerät |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|---------------|-----------------|
| Windows-Gerät anmelden bei geschäftlichen oder schulnotizbücher Konten.                                                                                                                      | Ja             | Ja           | Nein              |
| Benutzer einmaliges Anmelden (SSO) für Office 365 und Azure AD-apps. SSO ist die Möglichkeit, die nur einmal melden Sie sich bei Ressourcen der Organisation zugreifen. | Ja             | Ja           | Ja             |
| Benutzer SSO Kerberos-NTLM-apps.                                                                                                                                  | Ja             | Beschränkung       | Ja, über VPN         |
| Signifikante Autorisierung und bequeme-Anmeldung für geschäftlichen oder schulnotizbücher Konten mit Microsoft Passport und Windows Hallo.                                                                   | Ja             | Ja           | Ja             |
| Zugriff auf Enterprise-Windows Store zu einem geschäftlichen oder schulnotizbücher-Konto (kein Microsoft-Konto).                                                                                    | Ja             | Ja           | Ja             |
| Enterprise-kompatible roaming von benutzereinstellungen auf Geräten mit geschäftlichen oder schulnotizbücher Konten.                                                                                 | Ja             | Ja           | Ja             |
| Die Möglichkeit zum Einschränken des Zugriffs auf Geräte organisationsinterne apps, die mit organisationsinterne Geräterichtlinien kompatibel sind.                                                      | Ja             | Ja           | Ja             |
| Self-service-Bereitstellung von Geräten für "Arbeit überall" Benutzer                                                                                                | Nein              | Ja           | Ja             |
| Möglichkeit zum Verwalten von Geräten.                                                                                                                                       | Ja, über GP/SCCM | Ja           | Ja             |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Teilnehmen an der Verwendung im Besitz der Arbeit Geräte mit Azure AD-Verknüpfung und Domäne in Windows-10

Windows-10 bietet zwei Arten für Geräte im Besitz der Arbeit, um Ressourcen der Art Arbeit zuzugreifen:

- Azure AD-Verknüpfung
- Beitreten zu einer Domäne

 Beide können gültige Optionen je nach einer Organisation und sonstigen Erfordernissen sein. In einigen Fällen möglicherweise Organisationen nutzbringend UFI-beide Methoden der Bereitstellung.

## <a name="when-to-use-azure-active-directory-join"></a>Verwenden von Azure Active Directory teilnehmen

Azure AD-Verknüpfung steht eine neue Self-service Erfahrung in Windows 10 bereitgestellt.  Es ist Worker ausgelegt, die Ressourcen der Art Arbeit wie Office 365 hauptsächlich in der Cloud zugreifen. Es ist eine einfache Möglichkeit zum Konfigurieren von Computer, Tablets und für die Enterprise-Telefone. Geräte werden per Mobilgerät Verwaltung über konsistente Steuerelemente auf Windows-Plattformen verwaltet.

**Verwenden Sie Azure AD teilnehmen an einem der folgenden Gründe**:

- Aktivieren der Self-service Bereitstellung von Geräten für Kollegen unterwegs werden soll.
- Werden Benutzer mit der Arbeit im Besitz mobilen Geräten wie Tablets und Telefone.
- Möchten Sie eine Reihe von Benutzern in Azure AD statt in Active Directory, beispielsweise saisonale Kollegen, Vertragsnehmer oder Kursteilnehmer verwalten.
- Verknüpfen von Funktionen Kollegen in remote-Standorten mit eingeschränkter lokalen Infrastruktur zur Verfügung stellen möchten.
- Sie verfügen nicht über einen lokalen Active Directory.

Einige Organisationen verwendet Azure AD teilnehmen an die primäre Methode zum Bereitstellen von Geräten im Besitz der Arbeit als besonders, wenn sie die meisten oder alle ihre Ressourcen in der Cloud migrieren. Hybrid Organisationen mit Active Directory und Azure AD-können auch auswählen, eine Methode oder ein anderes je nach dem Benutzer oder Abteilung bereitgestellt.

Höchstwerte für Schule und Hochschulen, möglicherweise beispielsweise Personal in Active Directory und die Schüler in Azure Active Directory verwalten. Einige Unternehmen sollten in Azure AD remote-Büros und Umsatz Abteilungen verwalten. Sowohl Azure AD Join-Domäne Join-Methoden können innerhalb einer Organisation Hybrid verwendet werden. Azure AD-Verknüpfung kann eine großartige Ergänzung zum Beitreten zu einer Domäne für die Bereitstellung von Geräten in einer Umgebung für die Arbeit sein.

**Über die Cloud, ist der am häufigsten gewöhnlichen Zugriff auf Enterprise-Ressourcen Ihrer Organisation möglicherweise genießen Weitere Vorteile ist**:

- Sie können die Abhängigkeiten von lokalen Identitätsinfrastruktur entfernen.
- Sie können Geräte Bereitstellungsmodell, vereinfachen, erste Weg Imaginglösungen, indem Sie Self-service-Konfiguration.
- Verwaltung mobiler Geräte können Sie Ihren sämtlichen Geräten auf verschiedenen Plattformen verwalten.

Weitere Informationen zur Azure AD teilnehmen finden Sie unter [Extending Cloud-Funktionen in Windows-10-Geräte über Azure Active Directory teilnehmen](active-directory-azureadjoin-overview.md).

## <a name="when-to-use-domain-join-or-keep-using-it"></a>Verwenden von Domäne teilnehmen (oder verwenden sie beibehalten)

Für den letzten 15 Jahren haben viele Organisationen beitreten zu einer Domäne Arbeit Geräte Verbindung verwendet. Sie können die Benutzer melden Sie sich bei ihren Geräten mit ihrer Active Directory-Arbeit oder Schule Konten. Beitreten zu einer Domäne kann auch IT zentral und vollständig diese Geräte verwalten. Organisationen verlassen sich normalerweise auf imaging Methoden zum Bereitstellen von Geräten und häufig System Center Konfigurations-Manager (SCCM) oder Gruppe Richtlinie (GP) verwenden, um diese zu verwalten.

**Ihr Unternehmen sollten nach jedem der folgenden Gründe verwenden Domäne Verknüpfung (oder beibehalten verwenden)**:

- Sie können Win32-apps auf folgenden Geräten, die NTLM/Kerberos verwenden bereitgestellt.
- Sie benötigen GP oder SCCM/DCM Geräte zu verwalten.
- Möchten Sie weiterhin Imaginglösungen zum Konfigurieren von Geräten für Ihre Mitarbeiter verwenden.

**Beitreten zu einer Domäne in Windows 10 bietet Ihnen außerdem die folgenden Vorteile beim mit Azure AD verbunden**:

- Signifikante Gerät gebundene Authentifizierung und bequeme-Anmeldung für geschäftlichen oder schulnotizbücher Konten mit Microsoft Passport und Windows Hallo.
- Zugriff auf die Enterprise-Windows Store für Geräte, die verwenden die Arbeit oder Schule Konten (kein Microsoft-Konto erforderlich).
- Enterprise-kompatible roaming der benutzereinstellungen zwischen den verschiedenen Geräten, die geschäftlichen oder schulnotizbücher Konten (kein Microsoft-Konto erforderlich) verwenden.
- Die Möglichkeit zum Einschränken des Zugriffs auf Geräte organisationsinterne apps, die mit organisationsinterne Geräterichtlinien kompatibel sind.

Weitere Informationen zur Azure AD teilnehmen finden Sie unter [Extending Cloud-Funktionen in Windows-10-Geräte über Azure Active Directory teilnehmen](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Aktivieren Sie die Teilnahme an der privat genutzte Geräte für die Arbeit oder Schule

Um BYOD im Unternehmen zu unterstützen, bietet Windows 10 dem Benutzer die Möglichkeit zum Hinzufügen eines Kontos geschäftlichen oder schulnotizbücher zu ihren Computer, Ihren Tablet oder Telefon. Nachdem der Benutzer ein Konto geschäftlichen oder schulnotizbücher hinzufügt, wird das Gerät mit Azure AD registriert und registriert optional in das Mobilgerät Management-System, das die Organisation konfiguriert hat. Verzeichnis wird diese Geräte im Vergleich zu 'beigetreten Azure AD' als 'Registriert' angezeigt. IT-Administraors können verschiedene Richtlinien, die auf Basis dieser Informationen, die eine hellere Fingereingabe auf Geräten als privat genutzte auf Geräten Arbeit im Besitz bereitstellen, falls gewünscht anwenden.

Benutzer können hinzufügen eine geschäftlichen oder Konto mit ihrem Gerät mit persönlichen sehr praktisch Schule. Können sie dies tun, wenn eine Anwendung Arbeit zum ersten Mal den Zugriff auf können, oder sie es manuell über das Menü Einstellungen. Dieses Konto wird SSO Ressourcen der Organisation zur Verfügung stellen.

Weitere Informationen zur Azure AD teilnehmen finden Sie unter [Verbinden Domänenverbund Geräten für 10 Windows Azure AD-auftritt](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Aktivieren Sie beitreten zu einer Domäne oder Azure AD-Verknüpfung

Alle oben beschriebenen Methoden (beitreten zu einer Domäne, Azure AD-Verknüpfung und Hinzufügen von Arbeit oder Schule Konto) Felder und Optionen der Benutzeroberfläche für Windows 10 haben. Alle erfordern jedoch IT-Administratoren die Funktionalität in der Infrastruktur aktivieren, bevor die Oberfläche eingesetzt werden kann.

## <a name="requirements-for-deploying-azure-ad-join"></a>Anforderungen für die Bereitstellung von Azure AD teilnehmen

Zum Bereitstellen von Azure AD teilnehmen für eine Reihe von Benutzern benötigen Sie Folgendes:

- Ein Azure AD-Abonnement.
- Ein Azure AD Premium-Abonnement, z. B. Mobilgerät Management automatische Registrierung, wenn Sie weitere Funktionen benötigen.
- Verwaltung mobiler Geräte – beispielsweise ein Microsoft Intune-Abonnement, mobilen Gerät-Verwaltung für Office 365 oder einem Partner Mobilgerät Management Anbieter, die mit Azure AD integriert werden soll. (Siehe den [Abschnitt häufig gestellte Fragen](#frequently-asked-questions) am Ende dieses Artikels Weitere Informationen).

Wenn Ihre Fertigungsanlagen Hybrid sind, empfehlen wir nachdrücklich, dass Sie Azure AD-verbinden, um die lokalen Verzeichnis zu Azure AD erweitern bereitstellen.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Anforderungen für die Verwendung von beitreten zu einer Domäne mit Azure AD

Beitreten zu einer Domäne weiterhin funktionsfähig, da es immer verfügt. Um die Vorteile von Azure AD-erhalten werden Sie die folgenden benötigen:

- Ein Azure AD-Abonnement.
- Bereitstellung von Azure AD Herstellen einer Verbindung mit lokalen Verzeichnis zu Azure AD zu erweitern.
- Einer Richtlinie, mit dem Domänenverbund Geräte auf Azure AD bedingte zugreifen kann.
- Eine Richtlinie, die Zugriff auf Geräte "Domäne" ermöglicht, wenn Sie zum Einschränken des Zugriffs für einige Geräte können möchten.
- System Center-Konfigurations-Manager Version 1509 für Technical Preview, Regeln für kompatible Geräte mit Anforderung der aktivieren. (Finden Sie in der TechNet-Dokumentation und Blogbeitrag).

Weitere Informationen zum Beitreten zu einer Domäne in Windows 10 finden Sie unter [Verbinden Domänenverbund Geräten für 10 Windows Azure AD-auftritt.](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Anforderungen für die Verwendung von BYOD und "Einem geschäftlichen oder schulnotizbücher-Konto hinzufügen"

So aktivieren Sie "bringen Ihre eigenen Gerät" (BYOD) mit geschäftlichen oder schulnotizbücher Konten, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement.
- Ein Azure AD Premium-Abonnement, wie z. B. mobilen Gerät Management automatische Registrierung, wenn Sie weitere Funktionen benötigen.

## <a name="requirements-for-using-microsoft-passport"></a>Anforderungen für die Verwendung von Microsoft Passport

Wenn Microsoft Passport aktivieren möchten, benötigen Sie Folgendes:

- Eine Infrastruktur öffentlicher Schlüssel (PKI) für die Unterstützung von Zertifikaten basierende Authentifizierung, die Microsoft Passport verwendet.
- Ein Intune-Abonnement für die Unterstützung von Zertifikaten basierende Authentifizierung, die Microsoft Passport für Azure AD teilnehmen an und geschäftlichen oder schulnotizbücher Konten verwendet.
- System Center-Konfigurations-Manager Version 1509 für Technical Preview (Siehe den TechNet-Dokumentation und Blogbeitrag) für die Unterstützung von Zertifikaten basierende Authentifizierung, die Microsoft Passport zur beitreten zu einer Domäne verwendet.
- Einer Richtlinie für die Aktivierung von Microsoft Passport in der Organisation.

Als Alternative bei der Verwendung einer Infrastruktur öffentlicher Schlüssel können Sie die Taste-basierten Microsoft Passport durch Ausführen der folgenden aktivieren:

- Bereitstellen von Windows Server 2016 "Herstellung Preview 1" DCs (keine Notwendigkeit der Domäne oder Gesamtstrukturfunktionsebenen; mehrere DCs für Redundanz-Server-Funktionen, die jeder Active Directory-Standort ausreichend wird).
- Legen Sie die Richtlinie Microsoft Passport in der Organisation zu aktivieren.

Weitere Informationen zu Microsoft Passport und Windows Hallo in Windows 10 finden Sie unter < link-to-MS-Passport-and-Windows-Hello-document >.

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Welche Partner Mobilgerät Management-Produkte mit Azure AD integrieren?

Die folgenden Lieferantenprodukte integrieren für unified Registrierung und bedingten Zugriff in 10 Windows Azure AD aus:

- AirWatch von VMware
- Citrix Xenmobile
- Lightspeed Mobile Manager
- Verwaltung von SOTI lokalen mobiler Geräte
- MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Was ist mit Arbeitsplatz in Windows 10 teilnehmen?
Arbeitsplatz Verknüpfung wurde in Windows 8.1 verwendet, um BYOD zu aktivieren. In Windows-10 wird BYOD über "Hinzufügen einer Arbeit oder Schule Konto" aktiviert, wie weiter oben in diesem Dokument erläutert. Organisationen, die die Verwaltung mobiler Geräte mit Azure AD integrieren nicht, können Benutzer das Gerät in Management manuell über die **Einstellungen**registrieren > **Konten** > **Arbeit zugreifen**.


### <a name="can-users-connect-their-microsoft-account-to-their-domain-account-in-windows-10"></a>Können die Benutzer ihre Microsoft-Konto an ihre Domäne in Windows 10 verbinden?
Nicht in Windows 10. In Windows 8.1 könnten Benutzer von Geräten Domänenverbund "ihrem Microsoft-Konto (z. B. Hotmail, Live, Outlook, Xbox usw.) an ihre Domäne auf bestimmte wie SSO Live-Diensten, die Verwendung von Windows Store und roaming von User Settings auf Geräten ermöglicht es verbinden". In Windows-10 weist das Microsoft-Konto "verbinden Funktionen" eingestellt wurden. Der Benutzer kann als weiteren Konten zum Aktivieren von SSO für Consumer-Dienste wie beispielsweise im Windows Store mindestens Microsoft-Konto hinzufügen. Dies geschieht in den **Einstellungen** > **Konten** > **Ihr Konto**.

Benutzer, die ein Upgrade von Windows 8.1 Domänenverbund Geräte und wer hatten ihrem Microsoft-Konto, verbunden, wird automatisch ihrer verbundene Microsoft-Konto hinzugefügt haben, in die Liste der weiteren Konten, die sie verwenden müssen.


## <a name="additional-information"></a>Weitere Informationen
* [Windows-10 für das Unternehmen: Methoden zur Verwendung von Geräten für die Arbeit](active-directory-azureadjoin-windows10-devices-overview.md)
* [Erweitern Sie die Cloud-Funktionen, die auf Windows-10-Geräte über Azure Active Directory teilnehmen](active-directory-azureadjoin-user-upgrade.md)
* [Informationen Sie zu Szenarios für die Verwendung für Azure AD teilnehmen](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Herstellen einer Verbindung Azure AD für Windows 10 Erfahrung mit Domänenverbund Geräte](active-directory-azureadjoin-devices-group-policy.md)
* [Einrichten von Azure AD teilnehmen](active-directory-azureadjoin-setup.md)
