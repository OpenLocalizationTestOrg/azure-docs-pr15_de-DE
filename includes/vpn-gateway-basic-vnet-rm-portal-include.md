Zum Erstellen einer VNet im Bereitstellungsmodell Ressourcenmanager mithilfe des Azure-Portals führen Sie die folgenden Schritte aus. Die Screenshots dienen als Beispiele. Achten Sie darauf, dass Sie die Werte durch ein eigenes ersetzen. Weitere Informationen zum Arbeiten mit virtuelle Netzwerke finden Sie unter der [Virtuelle Network (Übersicht)](../articles/virtual-network/virtual-networks-overview.md).

1. Über einen Browser, navigieren Sie zu der [Azure-Portal](http://portal.azure.com) und, falls notwendig, melden Sie sich mit Ihrem Azure-Konto.

2. Klicken Sie auf **neu**. Geben Sie im Feld **Suchen die Marketplace** "Virtuellen Netzwerk" aus. Suchen Sie **Virtuelle Netzwerk** aus der zurückgegebenen Liste, und klicken Sie auf, um das **Virtuelle Netzwerk** Blade zu öffnen.

    ![Die Ressource Blade virtuellen Netzwerk suchen] (./media/vpn-gateway-basic-vnet-rm-portal-include/newvnetportal700.png "Suchen nach virtuellen Netzwerk Ressource blade")

3. Im unteren Bereich des Blades virtuelle Netzwerk aus der Liste **Wählen Sie ein Bereitstellungsmodell** **Ressourcenmanager**wählen Sie aus, und klicken Sie dann auf **Erstellen**.


    ![Wählen Sie aus Ressourcenmanager] (./media/vpn-gateway-basic-vnet-rm-portal-include/resourcemanager250.png "Wählen Sie aus Ressourcenmanager")

4. Konfigurieren Sie in der Blade **virtuelles Netzwerk erstellen** die VNet-Einstellungen aus. Wenn Sie in den Feldern ausfüllen, wird das rote Ausrufezeichen einem grünen Häkchen werden, wenn die Zeichen in das Feld eingegeben gültig sind.

    ![Feldüberprüfung] (./media/vpn-gateway-basic-vnet-rm-portal-include/checkmark300.png "Feldüberprüfung")

5. Ähnlich wie im folgenden Beispiel wird, sieht das Blade **virtuelles Netzwerk erstellen** aus. Möglicherweise gibt es Werte, die automatisch ausgefüllt werden. Wenn Ja, ersetzen Sie die Werte durch ein eigenes ein.

    ![Virtuelle Netzwerk-Blade erstellen] (./media/vpn-gateway-basic-vnet-rm-portal-include/createvnet300.png "Virtuelle Netzwerk-Blade erstellen")

6. **Name**: Geben Sie den Namen für das virtuelle Netzwerk.

7. **Adresse Abstand**: Geben Sie den Abstand Adresse. Wenn Sie mehrere Adresse Leerzeichen hinzugefügt haben, fügen Sie der ersten Adresse Leerzeichen hinzu. Sie können zusätzliche Adresse Leerzeichen nach dem Erstellen der VNet später hinzufügen.
 
8. **Subnetnamen**: Fügen Sie die Subnetnamen und Subnetzadressbereichs. Sie können zusätzliche Subnetze später hinzufügen, nachdem Sie die VNet erstellt.

10. **Abonnements**: Stellen Sie sicher, dass das Abonnement aufgeführt richtig ist. Sie können Abonnements mithilfe der Dropdown-Liste ändern.

11. **Ressourcengruppe**: Wählen Sie eine vorhandene Ressourcengruppe oder einen neuen erstellen, indem Sie einen Namen für die neue Ressourcengruppe eingeben. Wenn Sie eine neue Gruppe erstellen, benennen Sie die Ressourcengruppe entsprechend Ihren Werten für geplanten Konfiguration. Besuchen Sie für Weitere Informationen zu Ressourcengruppen [Azure Ressourcenmanager Übersicht](resource-group-overview.md#resource-groups)aus.

12. **Standort**: Wählen Sie den Speicherort für die VNet aus. Die Position bestimmt, wo die Ressourcen, die Sie für diese VNet bereitstellen gespeichert werden soll.

13. Wenn Sie in der Lage Ihre VNet einfach finden, auf dem Dashboard, und klicken Sie dann auf **Erstellen**möchten, wählen Sie **Pin zum Dashboard** .
    
    ![PIN zum dashboard] (./media/vpn-gateway-basic-vnet-rm-portal-include/pintodashboard150.png "PIN zum dashboard")

14. Nachdem Sie auf **Erstellen**, sehen Sie eine Kachel auf des Dashboards, die den Fortschritt Ihrer VNet widerspiegeln wird. Die Kachel ändert sich während der VNet erstellt wird.

    ![Erstellen von virtuelles Netzwerk-Kachel] (./media/vpn-gateway-basic-vnet-rm-portal-include/deploying150.png "Erstellen von virtuelles Netzwerk-Kachel")