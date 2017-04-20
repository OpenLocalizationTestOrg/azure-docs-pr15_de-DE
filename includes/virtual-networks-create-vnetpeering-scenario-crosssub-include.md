## <a name="peering-across-subscriptions"></a>Über Abonnements Peering

In diesem Szenario erstellen Sie eine peering zwischen zwei VNets zu anderen Abonnements gehören.

![Cross Subszenario](./media/virtual-networks-create-vnetpeering-scenario-crosssub-include/figure01.PNG)

VNet peering basiert auf Access rollenbasierte Steuerelement (RBAC) für die Autorisierung. Für Szenario Cross-Abonnements müssen Sie zuerst Benutzern ausreichenden Berechtigungen erteilen, von der Peeringverbindung erstellt wird:

> [AZURE.NOTE] Wenn derselbe Benutzer über beide Abonnements die Berechtigung verfügt, können Sie in Schritt 1 – 4 unten überspringen.
