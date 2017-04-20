<properties
   pageTitle="Wichtige Vault-Entwicklerhandbuch | Microsoft Azure"
   description="Azure-Taste Vault können Entwickler um kryptografische Schlüssel in der Microsoft Azure-Umgebung zu verwalten. "
   services="key-vault"
   documentationCenter=""
   authors="BrucePerlerMS"
   manager="mbaldwin"
   editor="bruceper" />
<tags
   ms.service="key-vault"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="identity"
   ms.date="10/03/2016"
   ms.author="bruceper" />

# <a name="azure-key-vault-developers-guide"></a>Azure wichtige Vault-Entwicklerhandbuch
Taste Vault verwenden, ist es möglich, sicheren Zugriff auf vertrauliche Informationen in Ihrer Anwendung so, dass:

- Schlüssel und geheime Schlüssel werden ohne den Code selbst schreiben geschützt werden und auf einfache Weise können diese von der Anwendung verwendet.
- Sie werden möglicherweise haben Ihre eigenen Kunden und ihre eigenen Schlüssel verwalten, damit Sie auf die Bereitstellung des Kern Softwarefunktionen konzentrieren können. Auf diese Weise werden die Anwendung nicht der Verantwortung oder potenzielle Haftung für Ihre Kunden Mandanten Schlüssel und geheime Schlüssel besitzen.
- Die Anwendung kann Schlüssel für die Anmeldung verwenden und Verschlüsselung noch hält das Key Management externe aus der Anwendung so, dass die Lösung für eine Anwendung geeignet ist, die geografisch verteilt ist.

- Mit der September 2016 Schlüssel Vault, Ihre Anwendung können jetzt nutzen Sie Schlüssel Vault Zertifikate. Weitere Informationen finden Sie unter **zu Schlüsseln, Secrets und Zertifikaten** Artikel in der [REST-Referenz](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Weitere allgemeine Informationen zu Azure Schlüssel Vault finden Sie unter [Was ist Schlüssel Vault](key-vault-whatis.md).

## <a name="videos"></a>Videos
In diesem Video wird gezeigt, wie Ihre eigene wichtige Vault erstellen und Verwendungsweise der beispielanwendung "Hello Schlüssel Vault".

[AZURE.VIDEO azure-key-vault-developer-quick-start]

Links zu Ressourcen im Video erwähnten:
- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Azure Key Vault Beispielcode (engl.)](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

Hier erfahren, um können mehr führen Sie den [Schlüssel Vault Blog](http://aka.ms/kvblog) und im [Schlüssel Vault Forum](http://aka.ms/kvforum)teilnehmen.

## <a name="creating-and-managing-key-vaults"></a>Erstellen und Verwalten von wichtigen Depots

Bevor Sie mit Azure Schlüssel Vault im Code arbeiten, können Sie erstellen und verwalten Depots über REST, Ressourcen-Manager-Vorlagen, PowerShell oder CLI, wie in den folgenden Artikeln beschrieben:

- [Erstellen und Verwalten von wichtigen Depots mit REST](https://msdn.microsoft.com/library/azure/mt620024.aspx)
- [Erstellen und Verwalten von wichtigen Depots mit PowerShell](key-vault-get-started.md)
- [Erstellen und Verwalten von wichtigen Depots mit CLI](key-vault-manage-with-cli.md)
- [Erstellen Sie eine wichtige Vault und fügen Sie einen geheimen Schlüssel über eine Vorlage Azure Ressourcen-Manager](../resource-manager-template-keyvault.md)

>[AZURE.NOTE] Verwaltungsvorgänge für wichtige Depots werden über AAD authentifiziert und autorisiert über Schlüssel Vault des eigenen Richtlinien, pro Vault definiert.

## <a name="coding-with-key-vault"></a>Programmieren mit wichtigen Vault

Das Schlüssel Vault Managementsystem für Programmierer umfasst mehrere Schnittstellen mit REST bildet die Grundlage [Schlüssel Vault REST-API-Referenz](https://msdn.microsoft.com/library/azure/dn903609.aspx).

Sie können, unterliegen erfolgreiche Autorisierung Folgendes:

- Verwaltung von [Erstellen](https://msdn.microsoft.com/library/azure/dn903634.aspx), [Importieren](https://msdn.microsoft.com/library/azure/dn903626.aspx), [Aktualisieren](https://msdn.microsoft.com/library/azure/dn903616.aspx), [Löschen](https://msdn.microsoft.com/library/azure/dn903611.aspx) und anderer Vorgänge kryptografischer Schlüssel

- Verwalten von Secrets [erhalten möchten](https://msdn.microsoft.com/library/azure/dn903633.aspx), [Update](https://msdn.microsoft.com/library/azure/dn986818.aspx), [Löschen](https://msdn.microsoft.com/library/azure/dn903613.aspx) und anderer Vorgänge verwenden

- Verwenden Sie kryptografische Schlüssel mit [Vorzeichen](https://msdn.microsoft.com/library/azure/dn878096.aspx)/[Überprüfen](https://msdn.microsoft.com/library/azure/dn878082.aspx), [WrapKey](https://msdn.microsoft.com/library/azure/dn878066.aspx)/[UnwrapKey](https://msdn.microsoft.com/library/azure/dn878079.aspx) und [Verschlüsseln](https://msdn.microsoft.com/library/azure/dn878060.aspx)/[Entschlüsseln](https://msdn.microsoft.com/library/azure/dn878097.aspx) Vorgänge

Die folgenden SDKs sind für die Arbeit mit Schlüssel Vault verfügbar:

|[![.NET](./media/key-vault-developers-guide/msft.netlogo_purple.png)](https://msdn.microsoft.com/library/mt765854.aspx)|[![Node.js](./media/key-vault-developers-guide/nodejs.png)](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest)
|:--:|:--:|
|[.NET SDK-Dokumentation](https://msdn.microsoft.com/library/mt765854.aspx)|[Node.js SDK-Dokumentation](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest)|
|[.NET SDK-Paket auf Nuget](http://www.nuget.org/packages/Microsoft.Azure.KeyVault)|[Node.js SDK-Paket](https://www.npmjs.com/package/azure-keyvault)|

Weitere Informationen zur Version 2.x des .NET SDK finden Sie die [Anmerkungen zu dieser Version](key-vault-dotnet2api-release-notes.md).

## <a name="example-code"></a>Beispielcode
Vollständige Beispiele Schlüssel Vault mit einer Anwendung finden Sie unter:

- .NET beispielanwendung *HelloKeyVault* und ein Beispiel für Azure Web Service. [Azure-Taste Vault-Codebeispiele](http://www.microsoft.com/download/details.aspx?id=45343)
- Lernprogramm für Informationen zum Verwenden von Azure Schlüssel Vault aus einer Webanwendung in Azure. [Verwenden von Azure wichtige Vault from a Web Application](key-vault-use-from-web-application.md)

## <a name="how-tos"></a>Vorgehensweisen

Die folgenden Artikel und Szenarien bieten Aufgabe spezifische Leitfäden für die Arbeit mit Azure Schlüssel Vault:

- [Änderung wichtige Vault Mandanten-ID nach dem Verschieben von Abonnement](key-vault-subscription-move-fix.md) - beim Verschieben von Azure-Abonnement von Mandanten A, B-Mandanten, werden Ihre vorhandenen wichtige Depots nicht zugegriffen werden, indem die Prinzipale (Benutzer und-Anwendungen) im Mandanten b Fix verwenden dieses Handbuchs.
- [Den Zugriff auf Schlüssel Vault hinter der Firewall](key-vault-access-behind-firewall.md) - Zugriff auf einen Schlüssel vault Ihrer wichtigsten Vault Clients Anwendung muss mehrere Endpunkte für verschiedene Funktionen zugreifen können.

- [Zum Generieren und Transfer HSM-Protected-Schlüsseln für Azure Schlüssel Vault](key-vault-hsm-protected-keys.md) - dies helfen Ihnen beim Planen, generieren und anschließend eigene HSM-geschützten Schlüssel zur Verwendung mit Azure Schlüssel Vault übertragen.
- [Vorgehensweise zur sicheren Werte (beispielsweise Kennwörter) während der Bereitstellung](../resource-manager-keyvault-parameter.md) - Wenn Sie einen sicheren Wert (wie ein Kennwort) als Parameter übergeben, während der Bereitstellung müssen, können Sie diesen Wert als einen geheimen Schlüssel in einem Azure Schlüssel Vault und Verweis den Wert in anderen Ressourcen-Manager-Vorlagen speichern.
- [So verwenden Sie die Taste Vault für extensible Schlüsselverwaltungsdienst mit SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) - der SQL Server-Konnektor für Azure Schlüssel Vault können SQL Server und SQL in VM Nutzung den Azure-Taste Vault-Dienst als einen Anbieter Extensible Key Management (EKM), um den Verschlüsselungsschlüssel für Applikationen Link zu schützen. Transparente datenverschlüsselung Backup-Verschlüsselung und Spalte Verschlüsselung auf Anwendungsebene.
- [Gewusst wie: Bereitstellen von Zertifikaten auf VMs aus Schlüssel Vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - einer Cloud-Anwendung in einen virtuellen Computer auf Azure ausgeführt wird, benötigt ein Zertifikat. Wie erhalte Sie dieses Zertifikat in diesem virtuellen Computer heute?
- [Wie Sie Setup Key Vault mit Ende zum wichtige Drehung und Überwachung](key-vault-key-rotation-log-monitoring.md) - diese schrittweise Anleitung zum Einrichten der Rotation des und Überwachung mit Azure Schlüssel Vault.

Weitere aufgabenspezifische Anleitungen integrieren und Schlüssel Depots mit Azure verwenden finden Sie unter [Ryan Jones Azure Ressourcenmanager Vorlage Beispiele für Schlüssel Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

## <a name="integrated-with-key-vault"></a>Wichtige Vault integriert

Diese Artikel enthalten Informationen zum anderen Szenarien und Dienste, die von uns oder Schlüssel Vault integriert.

- [Verschlüsselung von Azure Festplatten](../security/azure-security-disk-encryption.md) nutzt der Branche standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) -Features von Windows und das Feature [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux Volumeverschlüsselung für das Betriebssystem und Festplatten mit den Daten bereitzustellen. Die Lösung integriert Azure Schlüssel Vault, mit denen Sie die Steuerung und Verwaltung der Verschlüsselungsschlüssel Datenträger und vertrauliche Informationen in Ihr Abonnement wichtige Vault und dabei sicherstellen, dass alle Daten in den virtuellen Computer Festplatten im Ruhezustand in Azure-Speicher verschlüsselt werden.


## <a name="supporting-libraries"></a>Unterstützung von Bibliotheken

- Bietet [Microsoft Azure Schlüssel Vault-Hauptbibliothek](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) `IKey` und `IKeyResolver` Schnittstellen zum Suchen von Bezeichnern Schlüssel und Ausführen von Vorgängen mit Schlüssel.

- [Microsoft Azure Schlüssel Vault Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) bietet erweiterte Funktionen für Azure Schlüssel Vault.

## <a name="other-key-vault-resources"></a>Andere Schlüssel Vault-Ressourcen
- [Wichtige Vault-Blog](http://aka.ms/kvblog)
- [Wichtige Vault-Forum](http://aka.ms/kvforum)
