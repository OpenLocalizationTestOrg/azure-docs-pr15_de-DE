## <a name="service-chaining---transit-through-peered-vnet"></a>Verketten - Übertragung durch hervorragendem VNet Service

Obwohl die Verwendung von System leitet den Datenverkehr automatisch für die Bereitstellung erleichtert, gibt es Fälle, in denen das routing von Paketen über eine virtuelle Einheit steuern werden soll.
In diesem Szenario gibt es zwei VNets in einem Abonnement, HubVNet und VNet1 wie in der Abbildung unten beschrieben. Bereitstellen von Netzwerk virtuelle Appliance(NVA) in VNet HubVNet. Nach dem Herstellen peering zwischen HubVNet und VNet1 VNet, können Benutzer definiert Arbeitspläne einrichten und geben Sie den nächsten Abschnitt zum NVA in die HubVNet.

![NVA Übertragung](./media/virtual-networks-create-vnetpeering-scenario-transit-include/figure01.PNG)

> [AZURE.NOTE] Einfach zu verwendenden wird angenommen Sie, dass alle VNets hier im selben Abonnement sind. Aber funktioniert auch für Szenario Cross-Abonnement.

So aktivieren Sie während der Übertragung routing die wichtigste Eigenschaft ist der "Weitergeleitet Datenverkehr zulassen"-Parameter. Dadurch wird akzeptiert und Datenverkehr aus dem und in der NVA in die hervorragendem VNet zu senden.  
