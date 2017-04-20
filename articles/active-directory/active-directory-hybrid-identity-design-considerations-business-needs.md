<properties
    pageTitle="Azure Active Directory Hybrid Identität Entwurf Faktoren - bestimmen Identität Anforderungen | Microsoft Azure"
    description="Identifizieren des Unternehmens geschäftliche Anforderungen, die Sie definieren die Anforderungen für das Design der Hybrid Identität führen werden."
    documentationCenter=""
    services="active-directory"
    authors="billmath"
    manager="femila"
    editor=""/>

<tags
    ms.service="active-directory"
    ms.devlang="na"
    ms.topic="article"
    ms.tgt_pltfrm="na"
    ms.workload="identity" 
    ms.date="08/08/2016"
    ms.author="billmath"/>

# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Ermitteln der Identität Anforderungen für Ihre Identität Hybrid-Lösung
Der erste Schritt beim Entwerfen einer hybriden Identität Lösung ist die Anforderungen für die Unternehmensorganisation zu bestimmen, die diese Lösung genutzt werden wird.  Hybrid Identität als als Ergänzung (es unterstützt alle anderen Cloudlösungen durch die Bereitstellung der Authentifizierung) beginnt und wechselt um neue und interessante Funktionen bieten, die neuen Benutzer Auslastung entsperren.  Diese Auslastung oder Dienste, die Sie ergreifen für Ihre Benutzer möchten werden die Anforderungen für das Design der Hybrid Identität vorgegeben.  Diese Dienste und Auslastung müssen Hybrid Identität beide lokalen nutzen und in der Cloud.  

Sie müssen über diese wichtigsten Aspekte des Unternehmens zu verstehen, womit wechseln nun eine Vorbedingung und was das Unternehmen für die Zukunft plant. Wenn Sie die Sichtbarkeit der langfristig Strategie für den Entwurf von Hybrid Identität besitzen, sind Chancen, dass Ihre Lösung nicht skalierbare Anforderungen Unternehmen wächst und ändern.   T er in einem Diagramm zeigt ein Beispiel für eine Hybrid Identität Architektur und der Auslastung, die für Benutzer freigegeben werden, sind. Dies ist nur ein Beispiel für alle neuen mögliche Werte, die nicht gesperrt und mit einer Volltonfarbe Hybriden Identität Strategie übermittelt werden können. 
 
Einige Komponenten, die Bestandteil der Hybrid Identität Architektur sind![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Ermitteln Sie geschäftliche Anforderungen
Jedes Unternehmen müssen unterschiedliche Anforderungen, selbst wenn diese Unternehmen derselben Branche, real Unternehmen gehören, die Anforderungen variieren möglicherweise. Sie können weiterhin nutzen Sie best Practices aus der, aber schließlich des Unternehmens geschäftliche Anforderungen, die Sie definieren die Anforderungen für den Hybrid Identität Entwurf werden führen kann. 

Vergewissern Sie sich, wenn Sie Ihre geschäftliche Anforderungen identifizieren die folgenden Fragen beantworten:

- Ist Ihr Unternehmen IT Betrieb Kosten Ausschneiden suchen?
- Cloud-Anlagen (SaaS apps, Infrastructure) gesichert ist Ihr Unternehmen werden gefunden?
- Ist Ihr Unternehmen an Ihre IT modernisieren suchen?
  - Sind Ihre Benutzer mehr mobilen und anspruchsvolle IT zum Erstellen von Ausnahmen in Ihrer DMZ verschiedenen Typen von Datenverkehr an andere Ressourcen zugreifen dürfen?
  - Verfügt Ihr Unternehmen legacy apps, die erforderlich sind, diese moderne Benutzer veröffentlicht werden soll, aber sind nicht einfach neu schreiben?
  - Benötigt Ihr Unternehmen alle diese Aufgaben und zur gleichen Zeit unter Kontrolle bringen?
- Ist Ihr Unternehmen secure Benutzeridentität und Risiken reduzieren, indem Sie neue Tools, die das Fachwissen von Microsoft Azure Sicherheit Fachwissen lokal nutzen Onlineschalten suchen?
- Versucht Ihr Unternehmen, die gefürchteten "externen" Konten lokal zu entfernen, und verschieben Sie sie in der Cloud, in dem sie nicht mehr in Ihrer lokalen Umgebung ein inaktiv darstellen sind?

## <a name="analyze-on-premises-identity-infrastructure"></a>Lokale Identitätsinfrastruktur analysieren
Jetzt, da Sie eine Vorstellung zu Ihren Unternehmen geschäftliche Anforderungen haben, müssen Sie für Ihre lokalen Identitätsinfrastruktur ausgewertet werden soll. Diese Bewertung ist wichtig für Sie definieren die technischen Anforderungen Ihrer aktuellen Identität-Lösung in der Cloud Identität Managementsystem integriert werden soll. Vergewissern Sie sich die folgenden Fragen beantworten:

- Welche Authentifizierung und Autorisierung Lösung Ihres Unternehmens bedeutet lokal verwenden? 
- Verfügt Ihr Unternehmen derzeit lokalen Synchronisierungsdienste?
- Verwendet Ihr Unternehmen eine Drittanbieter-Identitätsanbieter (IdP)?

Sie müssen außerdem die Clouddienste bewusst sein, die möglicherweise Ihres Unternehmens. Es ist wichtig, Durchführung einer Bewertung, um die aktuelle Integration mit SaaS, IaaS oder PaaS Modelle in Ihrer Umgebung zu verstehen. Vergewissern Sie sich im Rahmen dieser Bewertung die folgenden Fragen beantworten:
- Verfügt Ihr Unternehmen eine Integration in einen Cloud-Dienstanbieter?
- Wenn Ja, werden auf welche Dienste verwendet?
- Gibt es zurzeit diese Integration in Herstellung oder ganz eines Pilotprojekts?


>[AZURE.NOTE]
Wenn Sie nicht genau alle Ihrer Apps Zuordnung und cloud Services, können Sie das Cloud App Discovery-Tool verwenden. Dieses Tool kann Ihre IT-Abteilung Einblick in Ihrer Organisation Business und Consumer Cloud apps bereitstellen. Die ist es einfacher denn je zu ermitteln Schatten IT in Ihrer Organisation, einschließlich Details zur von Verwendungsmustern und allen Benutzern Zugriff auf Ihre Cloud-Programme. Zugriff auf dieses Tool, wechseln Sie zu [https://appdiscovery.azure.com](https://appdiscovery.azure.com/)

## <a name="evaluate-identity-integration-requirements"></a>Auswerten Identität Integration Anforderungen
Als Nächstes müssen Sie die Identität Integration Anforderungen ausgewertet werden soll. Diese Bewertung ist wichtig, definieren die technischen Anforderungen für wie Benutzerauthentifizierung, Darstellung der Organisation Anwesenheitsinformationen in der Cloud, wie die Organisation Autorisierung zulassen wird und welche die Benutzerfunktionalität einnehmen soll. Vergewissern Sie sich die folgenden Fragen beantworten:

- Wird Ihre Organisation Föderation, standard-Authentifizierung oder beides werden verwendet?
- Es ist Föderation erforderlich?  Da die folgende:
 - Kerberos-basierte SSO
 - Ihr Unternehmen verfügt über eine lokale entwickelte (entweder internen oder 3rd Party), der SAML- oder -Funktionen, die ähnliche Föderation verwendet wird.
 - MFA mit einer Smartcard. RSA SecurID usw.
 - Client-Regeln zugreifen, die die folgenden Fragen beantworten:
     1. Kann ich alle externen Zugriff auf Office 365 basierend auf die IP-Adresse des Clients blockieren?
     1. Kann ich alle externen Zugriff auf Office 365, mit Ausnahme von Exchange ActiveSync blockieren?
     1. Ich kann alle externen Zugriff auf Office 365, eine Ausnahme bilden jedoch browserbasierte apps (OWA, SPO) blockieren
     1. Alle externen Zugriff auf Office 365 kann für Mitglieder vorgesehenen AD-Gruppen blockiert werden
- Sicherheit/Überwachung Bedenken
- Bereits vorhandene Investitionen in partnerverbundkontakte Authentifizierung
- Welchen Namen werden unserer Organisation wird für unsere Domäne in der Cloud verwendet?
- Verfügt die Organisation eine benutzerdefinierte Domäne?
    1. Ist die Domäne, öffentlichen und einfach über DNS überprüft?
    1. Wenn es nicht der Fall ist, klicken Sie dann haben Sie eine öffentlichen Domäne, die zum Registrieren einer alternativen UPN in AD verwendet werden können?
- Sind die Benutzer-IDs für Cloud Darstellung konsistent? 
- Verfügt die Organisation apps, die Integration mit Cloud Services erforderlich?
- Verfügt über die Organisation mehrere Domänen, sodass werden sie alle standard oder im Verbund Authentifizierung verwendet?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Auswerten von Applications, die in Ihrer Umgebung ausgeführt werden.
Jetzt, da Sie haben Sie eine Vorstellung zu Ihrem lokalen und cloud-Infrastruktur, müssen Sie die Anwendungen ausgewertet werden soll, die in dieser Umgebungen ausgeführt werden. Diese Bewertung ist wichtig, definieren die technischen Anforderungen diesen Anwendungen in der Cloud Identität Managementsystem integriert werden soll. Vergewissern Sie sich die folgenden Fragen beantworten:

- Wo werden unsere Applikationen live?
- Werden Benutzer lokale Applications zugreifen?  In der Cloud? Oder beides?
- Gibt es Pläne, nehmen die vorhandenen Auslastung und verschieben Sie sie in der Cloud?
- Gibt es Pläne, die neue Anwendungen entwickeln, die entweder lokal befinden oder in der Cloud, mit dem cloud Authentifizierung?

## <a name="evaluate-user-requirements"></a>Auswerten der Benutzer Anforderungen
Sie können auch für die Benutzer Anforderungen ausgewertet werden soll. Diese Bewertung ist wichtig, definieren die Schritte, die für auf Einführung und zur Unterstützung von Benutzern, wie er in der Cloud Übergabe benötigt werden. Vergewissern Sie sich die folgenden Fragen beantworten:

- Werden Benutzer Applikationen lokalen zugreifen?
- Werden Benutzer in der Cloud-Anwendung zugreifen?
- Wie üblich Benutzer melden Sie sich deren lokalen Umgebung?
- Wie werden Benutzer in der Cloud anmelden?

>[AZURE.NOTE]
Vergewissern Sie sich zum Erfassen von Notizen der einzelnen Antworten und die Gründe für die Antwort zu verstehen. [Ermitteln Reaktion Anforderungen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) wird über die verfügbaren Optionen und vor-und Nachteile gegenüber der beiden Optionen wechseln.  Durch Probleme beantwortet diese Fragen, die Sie auswählen, werden die beste Option ist für Ihr Unternehmen geeignet ist.

## <a name="next-steps"></a>Nächste Schritte
[Ermitteln Sie die Anforderungen für Directory-Synchronisierung](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Siehe auch
[Entwurf Aspekte (Übersicht)](active-directory-hybrid-identity-design-considerations-overview.md)
