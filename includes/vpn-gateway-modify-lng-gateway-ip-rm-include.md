Um die Gateway-IP-Adresse zu ändern, verwenden Sie den `New-AzureRmVirtualNetworkGatewayConnection` Cmdlet. Solange Sie den Namen des Gateways lokales Netzwerk genau wie den vorhandenen Namen beibehalten, werden die Einstellungen überschrieben. Zu diesem Zeitpunkt unterstützt das Cmdlet "Set" nicht die Gateway IP-Adresse ändern.

### <a name="gwipnoconnection"></a>So ändern Sie die Gateway IP-Adresse – keine Gateway-Verbindung

Um die Gateway IP-Adresse für Ihr lokales Netzwerk-Gateway zu aktualisieren, die noch nicht über eine Verbindung verfügen, verwenden Sie im folgenden Beispiel wird ein. Sie können auch die Adresspräfixe gleichzeitig aktualisieren. Die Einstellungen angegebenen überschreibt die vorhandenen Einstellungen. Achten Sie darauf, dass Sie den vorhandenen Namen Ihres Gateways lokales Netzwerk verwenden. Wenn dies nicht der Fall, werden ein neues Gateway für lokales Netzwerk erstellen Sie nicht überschrieben wird der vorhandenen vergleichen.

Verwenden Sie im folgenden Beispiel, das die Werte für Ihren eigenen ersetzen.

    New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
    -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
    -GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName


### <a name="gwipwithconnection"></a>So ändern Sie die Gateway IP-Adresse – vorhandene Gateway-Verbindung

Wenn bereits eine Gateway-Verbindung besteht, müssen Sie zuerst die Verbindung zu entfernen. Klicken Sie dann können Sie die Gateway-IP-Adresse ändern und eine neue Verbindung erstellen. Langweilig für Ihre VPN-Verbindung führt.


>[AZURE.IMPORTANT] Löschen Sie nicht das Option VPN Gateway aus. Wenn Sie dies tun, müssen Sie durch die Schritte zum neu erstellen sowie umkonfigurieren von Ihrem lokalen Router mit IP-Adresse, die mit dem neu erstellten Gateway zugewiesen werden: zurückzukehren.
 

1. Die Verbindung zu entfernen. Suchen Sie den Namen der Verbindung mithilfe der `Get-AzureRmVirtualNetworkGatewayConnection` Cmdlet.

        Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
        -ResourceGroupName MyRGName

2. Ändern Sie den Wert GatewayIpAddress ein. Sie können auch Ihre Adresspräfixe zu diesem Zeitpunkt bei Bedarf ändern. Beachten Sie, dass dadurch die vorhandenen Einstellungen für lokales Netzwerk Gateway überschrieben werden. Verwenden Sie den vorhandenen Namen Ihr lokales Netzwerk-Gateway beim ändern, damit die Einstellungen überschrieben werden. Wenn dies nicht der Fall, werden ein neues lokales Netzwerk-Gateway, erstellen Sie nicht ändern der vorhandenen vergleichen.

        New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
        -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
        -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName

3. Die Verbindung zu erstellen. In diesem Beispiel werden wir einen Verbindungstyp IPsec konfigurieren. Wenn Sie die Verbindung neu erstellen, verwenden Sie angegebenen Verbindungstyp für die Konfiguration. Finden Sie zusätzliche Verbindungstypen der [PowerShell-Cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) Seite.  Sie können zum Abrufen des Namens VirtualNetworkGateway Ausführen der `Get-AzureRmVirtualNetworkGateway` Cmdlet.

    Festlegen der Variablen:

        $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
        $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName

    Die Verbindung zu erstellen:
    
        New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
        -Location "West US" `
        -VirtualNetworkGateway1 $vnetgw `
        -LocalNetworkGateway2 $local `
        -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'

