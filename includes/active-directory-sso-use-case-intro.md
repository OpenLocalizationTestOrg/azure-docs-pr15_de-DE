Organisationen sind weitere [Software als Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) Applikationen für Produktivität verwenden, da Cloud Technologie und Tools werden immer einfacher verfügbar. Die Anzahl der SaaS apps wächst, wird es schwierig, die Administratoren zum Verwalten von Konten und Zugriffsrechten, und für die Benutzer ihre anderen ein Kennwort. Folgende Programme einzeln verwalten zusätzliche Arbeit erstellt und weniger sicher ist.


- Mitarbeiter viele Kennwörter verfolgen müssen meist weniger sichere Methoden verwenden zu können, denken Sie daran entweder Kennwörter notieren oder verwenden die gleichen Kennwörter für vielen Konten.

- Beim Eintreffen eines neuen Mitarbeiters oder eine belässt, müssen alle ihre Konten einzeln nach der Bereitstellung oder heben nach der Bereitstellung sein.

- Darüber hinaus Mitarbeiter möglicherweise verwenden SaaS apps für ihre Arbeit ohne zu durchlaufen IT, d. h., erstellen sie ihre eigenen Konten Betriebssystemen, die die IT-Administratoren noch nicht genehmigt und für die Überwachung nicht zur Verfügung.  

Einmaliges Anmelden (SSO) stellt eine Lösung für alle diese Probleme. Es ist die einfachste Methode zum Verwalten von mehreren apps, und bieten Benutzern ein einheitliches anmelden arbeiten. Azure Active Directory (Azure AD) bietet eine robuste SSO-Lösung und viele verfügbare vorab integrierte Clientanwendungen, mit Lernprogramme für Administratoren, schnell eine neue app einrichten und Starten der Benutzer bereitgestellt hat.


## <a name="how-does-azure-active-directory-integrate-apps"></a>Wie lässt sich Azure Active Directory apps integrieren?  

Azure AD können Sie Ihre apps und bereitgestellte Konten integriert werden soll. Dies kann über zwei Vorgehensweisen erfolgen.

- Ist die app in der app-Katalog vorab integrierte, gelangen Sie über die Portal-apps einrichten und Konfigurieren der Einstellungen zum SSO zulassen. Für alle Gallery-app, Sie können erste Schritte mit folgen die einfachen schrittweisen Anweisungen in der app-Katalog und in der Azure-Portal einmaliges Anmelden aktivieren.

- Wenn die app nicht im Katalog ist, können Sie die meisten apps weiterhin in Azure AD als eine benutzerdefinierte app einrichten. Setzt ein wenig mehr Fachwissen zu konfigurieren. Sie können jede Anwendung, die SAML 2.0 als partnerverbundkontakte app unterstützt, oder einer Anwendung, die eine HTML-basierte Anmeldeseite als Kennwort SSO-app enthält hinzufügen.

In den Fall, in dem Benutzer ihre eigenen Konten für SaaS apps, die von verwaltet werden nicht erstellt haben, IT, das [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) -Tool bietet eine Lösung. Dieses Tool überwacht den Web-Verkehr zum Identifizieren, welche apps überall in der Organisation und die Anzahl der Personen, die mit jeder von ihnen genutzt werden. IT kann mithilfe dieser Informationen um zu erfahren Sie, welche apps Benutzer es vorziehen, und wählen Sie das in Azure AD für SSO integrieren.  

Wenn Sie eine app in Azure AD integrieren, kann der Benutzer definierte Anwendungsidentitäten zu ihren jeweiligen zugeordnet Azure AD-Identitäten.  
