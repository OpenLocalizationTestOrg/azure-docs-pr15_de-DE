## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a>Vorbereiten von Azure Ressourcenmanager Anfragen authentifizieren

Sie müssen alle Vorgänge, die Sie für Ressourcen mit [Azure Ressourcenmanager] ausführen authentifizieren[ lnk-authenticate-arm] mit Azure Active Directory (AD). Die einfachste Möglichkeit hierzu ist PowerShell oder CLI Azure verwendet werden.

Sie sollten [Azure PowerShell 1.0] installieren[ lnk-powershell-install] oder höher, bevor Sie fortfahren.

Die folgenden Schritte zeigen, wie für eine Active Directory-Anwendung mithilfe von PowerShell Kennwortauthentifizierung eingerichtet. Sie können diese Befehle in einer standard-PowerShell-Sitzung ausführen.

1. Melden Sie sich bei Ihrer Azure-Abonnement mithilfe des folgenden Befehls:

    ```
    Login-AzureRmAccount
    ```

2. Notieren Sie Ihre **TenantId** und **SubscriptionId**. Diese werden später benötigt werden.

3. Erstellen Sie eine neue Azure Active Directory-Anwendung mit dem folgenden Befehl ein, der Platzhalter ersetzt:

    - **{Anzeigenamen}:** einen Anzeigenamen für die Anwendung wie **MySampleApp**
    - **{URL der Startseite}:** die URL der Startseite Ihrer App wie **http://mysampleapp/home**. Diese URL muss nicht auf einer echten Anwendung zeigen.
    - **{Anwendungskennung}:** Ein eindeutiger Bezeichner wie **http://mysampleapp**. Diese URL muss nicht auf einer echten Anwendung zeigen.
    - **{Kennwort}:** Ein Kennwort, das Sie zur Authentifizierung mit Ihrer app verwenden werden.

    ```
    New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
    ```
    
4. Notieren Sie die **ApplicationId** der Anwendung, die Sie erstellt haben. Sie können dies später benötigen.

5. Erstellen Sie einen neuen Dienst mit dem folgenden Befehl ein, und Ersetzen Sie **{MyApplicationId}** durch die **ApplicationId** aus dem vorherigen Schritt principal:

    ```
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
    
6. Richten Sie eine rollenzuweisung mit dem folgenden Befehl ein, und Ersetzen Sie **{MyApplicationId}** durch Ihre **ApplicationId**.

    ```
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```
    
Sie haben jetzt Erstellen der Azure AD-Anwendung, die Sie zum Authentifizieren aus einer benutzerdefinierten C#-Anwendung aktiviert wird. Weiter unten in diesem Lernprogramm benötigen Sie die folgenden Werte:

- TenantId
- SubscriptionId
- ApplicationId
- Kennwort

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: ../articles/powershell-install-configure.md
