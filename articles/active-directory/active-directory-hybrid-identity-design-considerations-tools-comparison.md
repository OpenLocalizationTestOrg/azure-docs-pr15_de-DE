<properties
    pageTitle="Hybrid Identität: Verzeichnisintegration tools Vergleich | Microsoft Azure"
    description="Dies ist Seite enthält eine umfassende Tabelle, die die verschiedenen Directory Integrationstools vergleicht, die für Verzeichnisintegration verwendet werden können."
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
    ms.topic="get-started-article"
    ms.date="08/08/2016"
    ms.author="billmath"/>

# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Hybriden Identität Verzeichnisintegration tools Vergleich

In den Jahren haben die Directory Integrationstools gewachsen entwickeltes und.  Dieses Dokument ist helfen bieten eine konsolidierte Ansicht dieser Tools und einen Vergleich der Features, die in den einzelnen verfügbar sind.

<!-- The hardcoded link is a workaround for campaign ids not working in acom links-->

>[AZURE.NOTE] Verbinden von Azure AD übernimmt die Komponenten und Funktionen, die zuvor als Dirsync und AAD synchronisieren freigegeben. Diese Tools werden nicht mehr einzeln freigegeben werden, und alle zukünftige Verbesserungen werden in Aktualisierungen Azure AD-verbinden, einbezogen, damit Sie immer wissen, wo Sie die aktuellste Funktionalität erhalten.
>
>DirSync und Azure-Active Directory-Synchronisierung werden nicht mehr unterstützt. Weitere Informationen finden Sie [hier](active-directory-aadconnect-dirsync-deprecated.md).


Verwenden Sie den folgenden Schlüssel für jede Tabelle ein.

● = Jetzt verfügbar  
Französisch = zukünftigen Versionen  
Seiten = Public Preview-Version  

## <a name="on-premises-to-cloud-synchronization"></a>Lokal in die Cloud Synchronisierung

| Feature  | Verbinden von Azure-Active Directory  | Azure-Active Directory-Synchronisierungsdienste (AAD synchronisieren) | Azure-Active Directory-Synchronisierungstool (DirSync)| Forefront Identität Manager 2010 R2 (FIM) |Microsoft-Identität-Manager 2016 (MIM)|
| :-------- |:--------:|:--------:|:--------:|:--------:|:--------:
| Herstellen einer Verbindung einzelnen mit lokalen Active Directory-Struktur | ● | ● | ● | ● |● |
| Verbinden mit mehreren lokalen Active Directory-Gesamtstrukturen |●  | ● |  | ● |● |
| Verbinden Sie mit mehreren lokalen Exchange-Organisationen | ● |  |  |  | |
| Verbinden Sie mit einzelnen lokalen LDAP-Verzeichnis | FRANZÖSISCH |  |  | ● |● |
| Verbinden Sie mit mehreren lokalen LDAP-Verzeichnisse durchsuchen |FRANZÖSISCH  |  |  | ● |● |
| Herstellen einer Verbindung mit lokalen Active Directory und lokalen LDAP-Verzeichnisse durchsuchen |FRANZÖSISCH  |  |  | ● |● |
| Verbinden Sie mit benutzerdefinierten Systeme (d. h. SQL, Oracle, MySQL usw.) | FRANZÖSISCH |  |  | ● |● |
| Synchronisieren von benutzerdefinierten Attributen (Directory Extensions) | ● |  |  |  |  |
|Verbinden Sie mit lokalen HR (d. h., SAP, Oracle e-Business, PeopleSoft)| FRANZÖSISCH |  |  | ● |● |
|Unterstützt FIM Synchronisierungsregeln und Connectors für die Bereitstellung auf lokale Systeme.|  |  |  | ● |● |

## <a name="cloud-to-on-premises-synchronization"></a>Cloud auf lokale Synchronisierung

| Feature  | Verbinden von Azure-Active Directory  | Synchronisierungsdienste Azure-Active Directory | Azure-Active Directory-Synchronisierungstool (DirSync) | Forefront Identität Manager 2010 R2 (FIM) |Microsoft-Identität-Manager 2016 (MIM)|
| :-------- |:--------:|:--------:|:--------:|:--------:|:--------:
| Abgeschlossenen Writebackvorgängen von Geräten | ● |  | ● |  ||
| Attribut abgeschlossenen writebackvorgängen (für Exchange-hybridbereitstellung) | ● | ● | ● | ● |● |
| Abgeschlossenen Writebackvorgängen von Objekten für Benutzer und Gruppen |  ●|  | |  ||
| Abgeschlossenen Writebackvorgängen Kennwörter (über das Zurücksetzen von Kennwörtern Self-service (SSPR) und das Kennwort ändern) |  ● | ● |  |  ||



## <a name="authentication-feature-support"></a>Unterstützung von Features Authentifizierung

| Feature  | Verbinden von Azure-Active Directory | Synchronisierungsdienste Azure-Active Directory | Azure-Active Directory-Synchronisierungstool (DirSync) | Forefront Identität Manager 2010 R2 (FIM) |Microsoft-Identität-Manager 2016 (MIM)|
| :-------- |:--------:|:--------:|:--------:|:--------:|:--------:
| Synchronisieren von Kennwort für einzelne lokalen Active Directory-Struktur | ● | ● | ● |  ||
| Synchronisieren von Kennwort für mehrere lokalen Active Directory-Gesamtstrukturen |  ●| ● |  |  ||
| Einmaliges Anmelden mit Föderation | ● | ● | ● | ● |● |
| Abgeschlossenen Writebackvorgängen Kennwörter (von SSPR und das Kennwort ändern) |●  | ● |  |  ||



## <a name="set-up-and-installation"></a>Einrichtung und Installation

| Feature  | Verbinden von Azure-Active Directory  | Synchronisierungsdienste Azure-Active Directory | Azure-Active Directory-Synchronisierungstool (DirSync) | Microsoft-Identität-Manager 2016 (MIM) |
| :-------- |:--------:|:--------:|:--------:|:--------:
| Unterstützung der Installation auf einem Domain Controller | ● | ● | ● |  |
| Unterstützung der Installation SQL Express verwenden | ● | ● | ● |  |
| Einfache Aktualisierung von DirSync |● |  |  |  |
| Lokalisierung von Administrator UX in Windows Server-Sprachen | ● | ● | ● |  |
|Lokalisierung von Endbenutzer UX Sprachen für Windows Server| |  |  |● |
| Unterstützung für WindowsServer 2008 und Windows Server 2008 R2 | ● für synchronisieren, nicht für die Föderation| ● | ●  | ● |
| Unterstützung für WindowsServer 2012 und Windows Server 2012 R2 | ● | ● | ● | ● |

## <a name="filtering-and-configuration"></a>Filtern und Konfiguration

Feature  | Verbinden von Azure-Active Directory | Synchronisierungsdienste Azure-Active Directory | Azure-Active Directory-Synchronisierungstool (DirSync) | Forefront Identität Manager 2010 R2 (FIM)| Microsoft-Identität-Manager 2016 (MIM)
:-------- |:--------:|:--------:|:--------:|:--------:|:--------:|
Klicken Sie auf Domänen und organisationsinterne Einheiten filtern | ● | ● | ● | ●  | ●
Klicken Sie auf Objekte Attributwerte filtern | ● | ● | ● | ●| ●
Zulassen Sie, dass minimalen Satz von Attributen werden (MinSync) synchronisiert | ● | ● |  ||
Zulassen von anderen Dienstvorlagen für Attribut Zahlungen angewendet werden |●  | ● |  ||
Zulassen Sie Entfernen von Attributen aus parallelen aus Active Directory auf Azure AD | ● | ● |  |  |
Zulassen der erweiterten Anpassung Attribut Zahlungen | ● | ● |  | ●  | ●

## <a name="next-steps"></a>Nächste Schritte
Erfahren Sie mehr über die [Integration von Ihrem lokalen Identitäten mit Azure Active Directory](active-directory-aadconnect.md).
