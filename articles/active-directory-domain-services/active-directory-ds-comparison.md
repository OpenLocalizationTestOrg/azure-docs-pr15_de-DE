<properties
    pageTitle="Azure-Active Directory-Domänendiensten: Vergleichen Azure AD-Domänendienste – Selbsthilfe bei Domain Controller | Microsoft Azure"
    description="Vergleich von Azure Active Directory-Domänendiensten Controller – Selbsthilfe bei Domäne"
    services="active-directory-ds"
    documentationCenter=""
    authors="mahesh-unnikrishnan"
    manager="stevenpo"
    editor="curtand"/>

<tags
    ms.service="active-directory-ds"
    ms.workload="identity"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/01/2016"
    ms.author="maheshu"/>

# <a name="how-to-decide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Wie Sie entscheiden, ob Azure-Active Directory-Domänendienste ist die richtige für Ihre Anwendungsfall-
Azure-Active Directory-Domänendiensten können Sie Ihre Auslastung in Azure-Infrastrukturdiensten, ohne darum kümmern Verwalten Ihrer Identitätsinfrastruktur bereitstellen. Dieser verwaltete Dienst unterscheidet sich von Windows Server Active Directory typischerweise, die Sie bereitstellen und verwalten auf Ihrer eigenen. Der Dienst wurde für erleichterte Bereitstellung, automatisierte Gesundheit für die Überwachung und Behebung und eine einfache Identitätsinfrastruktur für die Cloud. Wir werden beständig Weiterentwicklung von den Dienst, um Unterstützung für allgemeine Szenarien für die Bereitstellung hinzuzufügen.

Entscheiden Sie, ob Azure Active Directory-Domänendiensten oder Drehen von und Verwalten Ihrer eigenen (http://www.Office.com/redir/xt103221361) in Azure AD-Infrastruktur:

- Finden Sie in der Liste der [Features von Azure Active Directory-Domänendiensten angeboten](active-directory-ds-features.md).

- Überprüfen Sie häufige [Bereitstellungsszenarien Azure Active Directory-Domänendiensten](active-directory-ds-scenarios.md).

- Schließlich [Azure Active Directory-Domänendiensten auf die Option http://www.Office.com/redir/xt103221361 AD vergleichen](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).


## <a name="compare-azure-ad-domain-services-to-diy-ad-domain-in-azure"></a>Vergleich von Azure Active Directory-Domänendiensten – Selbsthilfe bei AD-Domäne in Azure
Die folgende Tabelle hilft Ihnen bei der Entscheidung zwischen Azure-Active Directory-Domänendiensten verwenden und Verwalten Ihrer eigenen AD-Infrastruktur in Azure.

|**Feature**|**Azure-Active Directory-Domänendiensten**|**'Http://www.Office.com/redir/xt103221361' AD in Azure-virtuellen Computern**|
|---|:---:|:---:|
|[**Verwaltete Dienst**](active-directory-ds-comparison.md#managed-service)|**& #x 2713;**|**& #x 2715;**|
|[**Sichere Bereitstellungen**](active-directory-ds-comparison.md#secure-deployments)|**& #x 2713;**|Der Administrator muss die Bereitstellung gesichert.|
|[**DNS-server**](active-directory-ds-comparison.md#dns-server)|**& #x 2713;** (verwaltete Service)|**& #x 2713;**|
|[**Domänen- oder Enterprise Administratorrechte**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges)|**& #x 2715;**|**& #x 2713;**|
|[**Beitreten zu einer Domäne**](active-directory-ds-comparison.md#domain-join)|**& #x 2713;**|**& #x 2713;**|
|[**Domänenauthentifizierung NTLM und Kerberos verwenden**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos)|**& #x 2713;**|**& #x 2713;**|
|[**Benutzerdefinierte Organisationseinheitsstruktur**](active-directory-ds-comparison.md#custom-ou-structure)|**& #x 2713;**|**& #x 2713;**|
|[**Schema Erweiterungen**](active-directory-ds-comparison.md#schema-extensions)|**& #x 2715;**|**& #x 2713;**|
|[**Active Directory-Domäne/Struktur vertraut**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts)|**& #x 2715;**|**& #x 2713;**|
|[**LDAP lesen**](active-directory-ds-comparison.md#ldap-read)|**& #x 2713;**|**& #x 2713;**|
|[**Sicheres LDAP (LDAPS)**](active-directory-ds-comparison.md#secure-ldap)|**& #x 2713;**|**& #x 2713;**|
|[**LDAP-schreiben**](active-directory-ds-comparison.md#ldap-write)|**& #x 2715;**|**& #x 2713;**|
|[**Gruppenrichtlinien**](active-directory-ds-comparison.md#group-policy)|Einfache|Vollständige|
|[**Geo verteilt Bereitstellungen**](active-directory-ds-comparison.md#geo-dispersed-deployments)|**& #x 2715;**|**& #x 2713;**|


#### <a name="managed-service"></a>Verwaltete Dienst
Azure Active Directory-Domänendiensten Domänen werden von Microsoft verwaltet. Sie müssen keinen Patch, Updates, Überwachung, Sicherungskopien, und Sicherstellung der Verfügbarkeit Ihrer Domäne kümmern. Diese Verwaltungsaufgaben werden als Dienst von Microsoft Azure für verwalteten Domänen angeboten.

#### <a name="secure-deployments"></a>Sichere Bereitstellungen
Die verwaltete Domäne ist zuverlässig gemäß Microsoft Sicherheit bewährte Methoden für die AD-Bereitstellungen blockiert. Bewährten abgelenkt werden aus dem AD-Produktteam Jahrzehnten Erfahrung Technik und AD-Bereitstellungen unterstützen. Http://www.Office.com/redir/xt103221361 Bereitstellungen müssen bestimmte Bereitstellung zur unten/secure sperren die Bereitstellung Schritte.

#### <a name="dns-server"></a>DNS-server
Eine Azure-Active Directory-Domänendiensten verwaltete Domäne enthält verwalteten DNS-Dienste. Mitglieder der Gruppe 'AAD DC Administratoren' können DNS-Einträge in der verwalteten Domäne verwalten. Mitglieder dieser Gruppe erhalten vollständige DNS-Verwaltung zu Berechtigungen für die verwalteten Domäne. DNS-Verwaltung kann mithilfe der in der Packung Remote Server-Verwaltungstools (RSAT) enthalten 'DNS-Verwaltungskonsole' ausgeführt werden.

#### <a name="domain-or-enterprise-administrator-privileges"></a>Domänen- oder Unternehmensadministrator Berechtigungen
Diese erhöhten werden nicht in einer verwalteten AAD-DS-Domäne angeboten. Anwendungen, die diese erhöhten ausführen/installiert sein erfordern können nicht für verwaltete Domänen ausgeführt werden. Eine kleinere Teilmenge von Administratorrechten steht für Mitglieder der Gruppe delegierte Administration "AAD DC Administratoren" bezeichnet. Diese Rechte umfassen Berechtigungen zum Konfigurieren von DNS, Gruppenrichtlinien konfigurieren, Administratorrechte auf Computern Domänenverbund usw. zu erhalten.

#### <a name="domain-join"></a>Beitreten zu einer Domäne
Sie können virtuellen Computern teilnehmen, zu der verwalteten Domäne ähnlich wie Sie eine AD-Domäne Computern hinzufügen.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Domänenauthentifizierung NTLM und Kerberos verwenden
Mit Azure Active Directory-Domänendiensten können Sie Ihre Anmeldeinformationen ein corporate Authentifizierung mit verwalteten Domäne. Anmeldeinformationen mit Ihrer Azure AD-Mandanten synchron bleiben. Für synchronisierten Mandanten: Azure AD verbinden damit ist sichergestellt, dass Änderungen vorgenommen Anmeldeinformationen lokal in Azure Active Directory synchronisiert werden. Bei einer – Selbsthilfe bei Domäne einrichten müssen Sie möglicherweise mit einer lokalen Kontengesamtstruktur für Benutzer mit ihren Anmeldeinformationen corporate authentifizieren Vertrauensstellung zwischen Domänen einrichten. Möglicherweise müssen Sie alternativ Active Directory-Replikation einrichten, um sicherzustellen, dass Benutzerkennwörter mit Ihrer Domäne Azure Controller virtuelle Computer synchronisieren.

#### <a name="custom-ou-structure"></a>Benutzerdefinierte Organisationseinheitsstruktur
Mitglieder der Gruppe 'AAD DC Administratoren' können in der verwalteten Domäne benutzerdefinierten Organisationseinheit erstellen.

#### <a name="schema-extensions"></a>Schema Erweiterungen
Sie können nicht das base Schema eine Azure-Active Directory-Domänendiensten verwalteten Domäne erweitern. Daher können nicht Applikationen, die auf Erweiterungen AD-Schema (z. B. neuen Attributen unter User Object) basieren aufgehoben und zu AAD DS-Domänen verschoben.

#### <a name="ad-domain-or-forest-trusts"></a>AD-Domäne oder Gesamtstrukturvertrauensstellungen
Verwaltete Domänen können nicht konfiguriert werden, um (ein-/ausgehende) die Vertrauensstellung zu anderen Domänen einrichten. Daher verwenden nicht Szenarien wie Ressourcen Gesamtstruktur Bereitstellungen oder Fällen, wo Sie nicht zum Synchronisieren von Kennwörtern in Azure AD lieber, Azure Active Directory-Domänendiensten.

#### <a name="ldap-read"></a>LDAP-lesen
Die verwaltete Domäne unterstützt LDAP Auslastung lesen. Daher können Sie Applikationen bereitstellen, die gelesen LDAP-Abfragen, an der verwalteten Domäne ausführen.

#### <a name="secure-ldap"></a>Sicheres LDAP
Sie können Azure Active Directory-Domänendienste zur sicheren LDAP-Zugriff auf Ihre verwalteten Domäne, wozu auch über das Internet konfigurieren.

#### <a name="ldap-write"></a>LDAP-schreiben
Die verwaltete Domäne ist für Benutzerobjekte schreibgeschützt. Daher funktionieren Applikationen schreiben LDAP-Abfragen an die Attribute des Benutzerobjekts ausführen, die nicht in einer verwalteten Domäne. Benutzerkennwörter können darüber hinaus innerhalb der verwalteten Domäne geändert werden. Ein weiteres Beispiel wäre Änderung des Gruppenmitgliedschaft oder Gruppenattribute innerhalb der verwalteten Domäne, die nicht zulässig ist. Eine ändert sich jedoch Benutzerattributen oder Kennwörter mit in Azure AD (über PowerShell/Azure-Portal) oder lokalen AD die verwalteten AAD-DS-Domäne synchronisiert werden.

#### <a name="group-policy"></a>Gruppenrichtlinien
Klicken Sie auf die verwaltete AAD-DS-Domäne nicht anspruchsvolle Gruppenrichtlinie Konstrukte unterstützt. Sie können nicht beispielsweise erstellen und verschiedene Gruppenrichtlinienobjekte für jede benutzerdefinierte Organisationseinheit in der Domäne bereitstellen oder Filtern nach GP verwendet WMI verwenden. Es ist eine integrierte Gruppenrichtlinienobjekt jedes für den Container 'AADDC Computern' und 'AADDC Benutzer', die so konfigurieren Sie Gruppenrichtlinien angepasst werden können.

#### <a name="geo-dispersed-deployments"></a>Geo Ihres Bereitstellungen
Azure Active Directory-Domänendiensten verwaltete Domänen sind in einem einzigen virtuellen Netzwerk in Azure verfügbar. Für Szenarien, die Domänencontroller in mehreren Azure Regionen auf der ganzen Welt verfügbar sein müssen, Einrichten der Domänencontroller in Azure IaaS virtuellen Computern bessere Alternative möglicherweise.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>'Http://www.Office.com/redir/xt103221361' (DIY) AD-Bereitstellungsoptionen
Bereitstellung Fallstudien möglicherweise, wenn Sie einige der Funktionen, indem Sie eine Installation von Windows Server AD benötigen. Sollten Sie in diesen Fällen eine der folgenden http://www.Office.com/redir/xt103221361 (DIY) Optionen aus:

- **Eigenständigen Cloud Domäne:** Sie können festlegen, von einem eigenständigen 'Cloud Domäne' mit Azure-virtuellen Computern, die als Domäne-Controller konfiguriert wurden. Diese Infrastruktur lässt sich nicht mit Ihrem lokalen integrieren AD-Umgebung. Diese Option würde erfordern eine andere Gruppe von 'Cloud Anmeldeinformationen' Login/Verwalten von virtuellen Computern in der Cloud.

- **Ressourcen Gesamtstruktur Bereitstellung:** Sie können eine Domäne in Topologie, mithilfe einrichten Azure-virtuellen Computern als Domäne-Controller konfiguriert. Anschließend können Sie eine AD-Vertrauensstellung konfigurieren, mit Ihrem lokalen AD-Umgebung. Sie können Domäne Join-Computern (Azure virtuellen Computern) zu diesem Ressourcengesamtstruktur in der Cloud. Benutzerauthentifizierung geschieht über entweder eine VPN/ExpressRoute-Verbindung zu Ihrem lokalen Verzeichnis.

- **Erweitern Sie Ihre Domäne lokal in Azure:** Sie können ein Azure-virtuelles Netzwerk mit Ihrem lokalen Netzwerk über eine Verbindung VPN/ExpressRoute herstellen, damit Azure-virtuellen Computern können, um Ihrem lokalen verknüpft werden Active Directory. Eine andere Alternative ist zu Replikatdomänencontrollern Ihrer Domäne lokal in Azure als eines virtuellen Computers zu fördern. Sie können ihn dann einrichten, Replikation über ein VPN/ExpressRoute-Verbindung zu Ihrem lokalen Verzeichnis. In diesem Modus Bereitstellung erweitert Ihrer lokalen Domäne effektiv in Azure.

> [AZURE.NOTE] Sie können festlegen, dass es sich bei eine – Selbsthilfe bei Option für Ihre Bereitstellung verwenden – Anfragen besser geeignet ist. Erwägen Sie die [Freigabe von Feedback](active-directory-ds-contact-us.md) zu helfen Sie uns darüber, welche Features zur würden Sie Azure Active Directory-Domänendiensten zukünftig ausgewählt haben. Dieser Bewertung helfen Sie uns den Dienst Ihre Bedürfnisse und Fallstudien besser entsprechend weiterentwickelt.

Wir veröffentlicht haben [Richtlinien zum Bereitstellen von Windows Server Active Directory auf Azure virtuellen Computern](https://msdn.microsoft.com/library/azure/jj156090.aspx) – Selbsthilfe bei Installationen zu erleichtern.


## <a name="related-content"></a>Siehe auch
- [Features - Services Azure AD-Domäne](active-directory-ds-features.md)

- [Szenarien für die Bereitstellung - Azure Active Directory-Domänendiensten](active-directory-ds-scenarios.md)

- [Richtlinien für die Bereitstellung von Windows Server Active Directory auf Azure-virtuellen Computern](https://msdn.microsoft.com/library/azure/jj156090.aspx)
