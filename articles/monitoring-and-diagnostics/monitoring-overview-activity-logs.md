<properties
    pageTitle="Übersicht über das Aktivitätsprotokoll Azure | Microsoft Azure"
    description="Erfahren Sie, was der Azure Aktivität Log ist und wie Sie diese Ereignisse innerhalb Ihres Abonnements Azure schwer verwenden können."
    authors="johnkemnetz"
    manager="rboucher"
    editor=""
    services="monitoring-and-diagnostics"
    documentationCenter="monitoring-and-diagnostics"/>

<tags
    ms.service="monitoring-and-diagnostics"
    ms.workload="na"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="10/25/2016"
    ms.author="johnkem"/>

# <a name="overview-of-the-azure-activity-log"></a>Übersicht über das Aktivitätsprotokoll Azure
Der **Azure Aktivität Log** ist ein Protokoll, der einen Einblick in die Vorgänge enthält, die in den Ressourcen im Rahmen Ihres Abonnements ausgeführt wurden. Der Aktivität Log wurde früher bekannt als "Überwachungsprotokolle" oder "Betriebsprotokolle", da es Steuerelement-Ebene Ereignisse für Ihre Abonnements Berichte. Mit der Log Aktivität Sie können festlegen, die "Was, wer, und wann ' für alle Vorgänge (sich, Beitrag, löschen), die für die Ressourcen in Ihrem Abonnement schreiben. Sie können auch den Status des Vorgangs und anderen relevanten Eigenschaften kennen. Das Aktivitätsprotokoll enthält nicht gelesen (GET) Vorgänge.

Das Protokoll Aktivität unterscheidet sich von [Diagnoseprotokollen](./monitoring-overview-of-diagnostic-logs.md), welche sind alle Protokolle, die von einer Ressource ausgegeben. Diese Protokolle bieten Daten über den Vorgang, der Ressource, die statt Operations für diese Ressource an.

Sie können die Ereignisse aus Ihrer Aktivitätsprotokoll mithilfe des Azure-Portals CLI, PowerShell-Cmdlets abrufen und Azure Monitor REST-API.

Anzeigen dieser- [video Einführung in das Protokoll Aktivität](https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz).  

## <a name="what-you-can-do-with-the-activity-log"></a>Mögliche Aktionen mit der Log Aktivität
Hier einige der Dinge, die Sie mit der Log Aktivität ausführen können:

- Abfragen Sie und zeigen Sie der **Azure-Portal an**.
- Fragen Sie über die REST-API, PowerShell-Cmdlet oder CLI ab.
- [Erstellen einer e-Mail- oder Webhook Benachrichtigung, die Deaktivieren eines Ereignisses Aktivität Log auslöst.](./insights-auditlog-to-webhook-email.md)
- [Speichern Sie es mit einem **Konto Speicher** für Archivierung oder manuellen Überprüfung](./monitoring-archive-activity-log.md). Sie können die Aufbewahrungszeit (in Tagen) Verwendung von **Profilen Log**angeben.
- Analysieren Sie es in PowerBI mit dem [**Inhalt Pack PowerBI**](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/).
- [Übertragen Sie darauf, um ein **Ereignis Hub** ](./monitoring-stream-activity-logs-event-hubs.md) für die Erfassung von einem Drittanbieter-Dienst oder benutzerdefinierten Analytics-Lösung, wie z. B. PowerBI darstellt.

## <a name="export-the-activity-log-with-log-profiles"></a>Exportieren der Aktivität Log mit Log Profilen
**Log-Profil** steuert, wie Ihre Aktivitäten Log exportiert wird. Verwenden eines Profils Log, können Sie konfigurieren:

- Stelle, an der die Aktivität Log (Speicher-Konto oder Ereignis Hubs) gesendet werden soll
- Welche Ereigniskategorien (schreiben, löschen, Aktion) gesendet werden soll
- Welche Bereiche (Speicherorte) exportiert werden sollen
- Wie lange die Aktivität Log in einem Speicher-Konto – ein Aufbewahrung von Null Tage beibehalten werden sollen, bedeutet, dass es sich bei Protokolle für immer gespeichert sind. Andernfalls kann der Wert eine beliebige Anzahl von Tagen zwischen 1 und 2.147.483.647 sein. Wenn Aufbewahrungsrichtlinien festgelegt sind, aber Speichern von Protokollen in einem Speicher-Konto (beispielsweise, wenn nur Ereignis Hubs oder OMS Optionen ausgewählt sind) deaktiviert ist, haben die Aufbewahrungsrichtlinien keine Auswirkung.

Diese Einstellungen können über die Option "Exportieren" in vorher Aktivität Log in das Portal konfiguriert werden. Sie können auch konfigurierten programmgesteuert [mithilfe der Azure Monitor REST-API](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell-Cmdlets oder CLI sein. Ein Abonnement kann nur ein Protokoll Profil haben.

### <a name="configure-log-profiles-using-the-azure-portal"></a>Konfigurieren von Log Profilen über das Azure-portal
Können Sie das Protokoll Aktivität an einen Hub Ereignis übertragen oder in einem Speicher-Konto mithilfe der Option "Exportieren" im Portal Azure speichern.

1. Navigieren Sie zu der **Aktivität Log** Blade über das Menü auf der linken Seite des Portals.

    ![Navigieren Sie zu Aktivität Log-Portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Klicken Sie auf die Schaltfläche " **Exportieren** " am oberen Rand der Blade.

    ![Schaltfläche "Exportieren" im portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Klicken Sie in das Blade, das angezeigt wird, können Sie Folgendes auswählen:  
    - Bereiche, für die Sie Ereignisse exportieren möchten
    - das Speicher-Konto, das Sie Ereignisse speichern möchten
    - die Anzahl der Tage, die diese Ereignisse im Speicher beibehalten werden soll. Eine Einstellung von 0 Tagen behält die Protokolle für immer aus.
    - der Dienst Bus Namespace in der Sie ein Ereignis Hub für diese Ereignisse streaming erstellt werden sollen.

    ![Exportieren von Aktivität Log blade](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Klicken Sie auf **Speichern** , um diese Einstellungen zu speichern. Die Einstellungen werden sofort zu Ihrem Abonnement übernommen.

### <a name="configure-log-profiles-using-the-azure-powershell-cmdlets"></a>Konfigurieren von Log Profilen mithilfe der Azure-PowerShell-Cmdlets
#### <a name="get-existing-log-profile"></a>Abrufen von vorhandenen Log-Profil
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Hinzufügen eines Profils log
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Eigenschaft         | Erforderlich | Beschreibung   |
|------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Namen             | Ja      | Der Name Ihres Profils Protokoll.                                 |
| StorageAccountId | Nein       | Ressourcen-ID des Kontos Speicher, dem die Aktivität Log gespeichert werden soll.                         |
| serviceBusRuleId | Nein       | Service Bus Regel-ID für den Namespace Dienstbus möchten Sie Ereignis Hubs in erstellt haben. Ist eine Zeichenfolge mit diesem Format: `{service bus resource ID}/authorizationrules/{key name}`. |
| Speicherorte        | Ja      | Durch Trennzeichen getrennte Liste der Gebiete, die für die Aktivität Log Ereignisse erfasst werden soll.              |
| RetentionInDays  | Ja      | Anzahl der Tage zwischen 1 und 2.147.483.647, welche Ereignisse beibehalten werden soll. Der Wert 0 (null) speichert die Protokolle endlos (für immer). |
| Kategorien       | Nein       | Durch Trennzeichen getrennte Liste der Ereigniskategorien, die erfasst werden. Mögliche Werte sind, schreiben, löschen und Aktion.                                 |

#### <a name="remove-a-log-profile"></a>Entfernen eines Profils log
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-the-azure-cross-platform-cli"></a>Konfigurieren von Log Profilen mithilfe der Azure-Plattform-CLI
#### <a name="get-existing-log-profile"></a>Abrufen von vorhandenen Log-Profil
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Die `name` Eigenschaft sollten auf den Namen Ihres Profils Protokoll.

#### <a name="add-a-log-profile"></a>Hinzufügen eines Profils log
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Eigenschaft         | Erforderlich | Beschreibung   |
|------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Namen             | Ja      | Der Name Ihres Profils Protokoll.                                 |
| storageId        | Nein       | Ressourcen-ID des Kontos Speicher, dem die Aktivität Log gespeichert werden soll.                         |
| serviceBusRuleId | Nein       | Service Bus Regel-ID für den Namespace Dienstbus möchten Sie Ereignis Hubs in erstellt haben. Ist eine Zeichenfolge mit diesem Format: `{service bus resource ID}/authorizationrules/{key name}`. |
| Speicherorte        | Ja      | Durch Trennzeichen getrennte Liste der Gebiete, die für die Aktivität Log Ereignisse erfasst werden soll.              |
| retentionInDays  | Ja      | Anzahl der Tage zwischen 1 und 2.147.483.647, welche Ereignisse beibehalten werden soll. Der Wert 0 (null) speichert die Protokolle endlos (für immer).     |
| Kategorien       | Nein       | Durch Trennzeichen getrennte Liste der Ereigniskategorien, die erfasst werden. Mögliche Werte sind, schreiben, löschen und Aktion.                                 |

#### <a name="remove-a-log-profile"></a>Entfernen eines Profils log
```
azure insights logprofile delete --name my_log_profile
```

## <a name="event-schema"></a>Ereignisschema
Jedes Ereignis in der Aktivität Log weist einen JSON-Blob ähnlich wie in diesem Beispiel:

```
{
  "value": [ {
    "authorization": {
      "action": "microsoft.support/supporttickets/write",
      "role": "Subscription Admin",
      "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
    },
    "caller": "admin@contoso.com",
    "channels": "Operation",
    "claims": {
      "aud": "https://management.core.windows.net/",
      "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
      "iat": "1421876371",
      "nbf": "1421876371",
      "exp": "1421880271",
      "ver": "1.0",
      "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
      "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
      "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
      "puid": "20030000801A118C",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
      "name": "John Smith",
      "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
      "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
      "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
      "appidacr": "2",
      "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
      "http://schemas.microsoft.com/claims/authnclassreference": "1"
    },
    "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
    "description": "",
    "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
    "eventName": {
      "value": "EndRequest",
      "localizedValue": "End request"
    },
    "eventSource": {
      "value": "Microsoft.Resources",
      "localizedValue": "Microsoft Resources"
    },
    "httpRequest": {
      "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
      "clientIpAddress": "192.168.35.115",
      "method": "PUT"
    },
    "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
    "level": "Informational",
    "resourceGroupName": "MSSupportGroup",
    "resourceProviderName": {
      "value": "microsoft.support",
      "localizedValue": "microsoft.support"
    },
    "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
    "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
    "operationName": {
      "value": "microsoft.support/supporttickets/write",
      "localizedValue": "microsoft.support/supporttickets/write"
    },
    "properties": {
      "statusCode": "Created"
    },
    "status": {
      "value": "Succeeded",
      "localizedValue": "Succeeded"
    },
    "subStatus": {
      "value": "Created",
      "localizedValue": "Created (HTTP Status Code: 201)"
    },
    "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
    "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
    "subscriptionId": "s1"
  } ],
"nextLink": "https://management.azure.com/########-####-####-####-############$skiptoken=######"
}
```

| Elementnamen         | Beschreibung             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Autorisierung        | BLOB RBAC Eigenschaften des Ereignisses. Normalerweise enthält die Eigenschaften "Aktion", "Rolle" und "Bereich" aus.|
| Anrufer               | E-Mail-Adresse des Benutzers, der den Vorgang, eine UPN-Anspruch oder SPN anfordern, die auf Grundlage der Verfügbarkeit ausgeführt hat.|
| Kanäle             | Die folgenden Werte: "Administrator", "Der Vorgang"|
| correlationId        | In der Regel eine GUID im Zeichenfolgenformat. Die gleiche Uber Aktion gehören Ereignisse, die eine CorrelationId freigeben.   |
| Beschreibung          | Beschreibung der statischen Text eines Ereignisses.                              |
| eventDataId          | Eindeutiger Bezeichner eines Ereignisses.    |
| Quelle          | Name des Azure Service oder Infrastruktur, die das Ereignis generiert hat.    |
| httpRequest          | BLOB, beschreibt die HTTP-Anforderung. In der Regel enthält "ClientRequestId", "ClientIpAddress" und "Methode" (HTTP-Methode. For example, setzen).                            |
| Ebene                | Ebene des Ereignisses. Die folgenden Werte: "Kritisch", "Zurück", "Warnung", "Information" und "Ausführlich"  |
| resourceGroupName    | Name der Ressourcengruppe für die betroffenen Ressource.               |
| resourceProviderName | Namen der Ressourcenanbieters für die betroffenen Ressource             |
| resourceUri          | Ressourcen-Id des betroffenen Ressource.                               |
| operationId          | Eine GUID Weitergabe an die Ereignisse aus, die einem Vorgang entsprechen.         |
| operationName        | Name des Vorgangs.  |
| Eigenschaften           | Festlegen von `<Key, Value>` Paare (d. h., ein Wörterbuch), beschreibt die Details des Ereignisses.                                |
| Status               | Eine Zeichenfolge, die den Status des Vorgangs. Einige allgemeine Werte sind: gestartet, In den Fortschritt, war erfolgreich, fehlgeschlagen, aktiv, gelöst.                                |
| untergeordnete Status            | Normalerweise der HTTP-Statuscode den entsprechenden Rest anrufen, kann jedoch auch andere Zeichenfolgen, die eine untergeordnete Status, wie diese allgemeine Werte beschreiben: OK (HTTP-Status Code: 200), erstellten (HTTP-Status Code: 201), zulässigen (HTTP-Status Code: 202), nicht Inhalt (HTTP-Status Code: 204), ungültige Anforderung (HTTP-Status Code: 400), nicht gefunden (HTTP-Status Code: 404), Konflikt (HTTP-Status Code : 409), interner Serverfehler (HTTP-Status Code: 500), Dienst nicht verfügbar (HTTP-Status Code: 503), Gateway-Timeout (HTTP-Status Code: 504). |
| eventTimestamp       | Zeitstempel, wenn das Ereignis vom Azure-Dienst Verarbeitung der Anforderung entspricht das Ereignis erstellt wurde.     |
| submissionTimestamp  | Zeitstempel, wenn das Ereignis für Abfragen verfügbar geworden ist.             |
| subscriptionId       | Azure-Abonnement-ID an.  |
| nextLink             | Fortsetzungstoken, den nächsten Satz von Ergebnissen abgerufen werden sollen, wenn er in mehreren Antworten aufgeteilt werden soll. In der Regel erforderlich, wenn mehr als 200 Datensätze vorhanden sind.     |

## <a name="next-steps"></a>Nächste Schritte
- [Erfahren Sie mehr über die Aktivität Log (vormals Überwachungsprotokolle)](../resource-group-audit.md)
- [Übertragen Sie das Aktivitätsprotokoll Azure zu Ereignis Hubs](./monitoring-stream-activity-logs-event-hubs.md)
