## <a name="how-to-create-a-classic-vnet-in-the-azure-portal"></a>So erstellen Sie eine klassische VNet Azure-Portal

Führen Sie zum Erstellen einer klassischen VNet basierend auf dem oben genannten Szenario die folgenden Schritte aus.

1. Mithilfe eines Browsers und navigieren Sie zu http://portal.azure.com und, falls notwendig, melden Sie sich mit Ihrem Azure-Konto.
2. Klicken Sie auf **neu** > **Networking** > **virtuellen Netzwerk**, beachten Sie, dass in die Liste **Wählen Sie ein Modell zur Bereitstellung von** bereits zeigt **klassischen**, und klicken Sie dann auf **Erstellen**, wie in der folgenden Abbildung gezeigt.

    ![Erstellen von VNet Azure-Portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)

3. Geben Sie auf das Blade **virtuellen Netzwerk** den **Namen** der VNet, und klicken Sie dann auf **Adressbereichs**. Konfigurieren Sie Ihre Adresse Speicherplatz für den VNet und seine erste Subnetz und dann auf **OK**. Die folgende Abbildung zeigt die Einstellungen für den Zugriffsschutz CIDR in diesem Szenario.

    ![Adresse Leerzeichen blade](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)

4. Klicken Sie auf **Ressourcengruppe** und wählen Sie eine Ressourcengruppe aus der VNet zum Hinzufügen, oder klicken Sie auf **neue Ressourcengruppe erstellen** , um eine neue Ressourcengruppe der VNet hinzuzufügen. Die folgende Abbildung zeigt die Ressource gruppeneinstellungen für eine neue Ressourcengruppe **TestRG**bezeichnet. Besuchen Sie für Weitere Informationen zu Ressourcengruppen [Azure Ressourcenmanager Übersicht](../articles/virtual-network/resource-group-overview.md#resource-groups)aus.

    ![Ressource Gruppe Blade erstellen](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)

5. Ändern Sie bei Bedarf die Einstellungen für **Abonnement** und **einen Speicherort** für Ihre VNet. 

6. Wenn Sie nicht die VNet als Kachel in der **Startboard**finden Sie unter möchten, deaktivieren Sie **an Startboard anheften**. 

7. Klicken Sie auf **Erstellen** , und beachten Sie die Kachel mit dem Namen **Erstellen von virtuellen Netzwerk** , wie in der folgenden Abbildung gezeigt.

    ![Erstellen von VNet-Portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)

8. Warten Sie, bis die VNet erstellt werden soll, und wenn Sie die Kachel darunter angezeigt wird, klicken Sie auf, um weitere Subnetze hinzufügen.

    ![Erstellen Sie VNet-Portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)

9. Es sollte die **Konfiguration** für Ihr VNet angezeigt, wie unten dargestellt. 

    ![Erstellen Sie VNet-Portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)

10. Klicken Sie auf **Subnets** > **Hinzufügen**, geben Sie einen **Namen** , und geben Sie einen **Adressbereich (CIDR-Block)** für Ihr Subnetz, und klicken Sie dann auf **OK**. Die folgende Abbildung zeigt die Einstellungen für das aktuelle Szenario.

    ![Erstellen von VNet Azure-Portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)