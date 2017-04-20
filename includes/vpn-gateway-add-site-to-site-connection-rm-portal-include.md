1. Suchen Sie nach Schlüsselaufgaben virtuelle Netzwerk, und klicken Sie auf **Alle Einstellungen** , um das Blade **Einstellungen** zu öffnen.

2. Klicken Sie in den **Einstellungen** Blade auf **Verbindungen**, und klicken Sie dann auf **Hinzufügen** am oberen Rand der Blade um das Blade **Verbindung hinzufügen** zu öffnen.

    ![Erstellen von Website-zu-Standort-Verbindung](./media/vpn-gateway-add-site-to-site-connection-rm-portal-include/addconnection250.png)

3. In der Blade **Verbindung hinzufügen** , **Name** der Verbindung. 

4. Wählen Sie für **Verbindungstyp** **Site-to-site(IPSec)**ein.

5. Für **virtuellen Netzwerk-Gateway**ist der Wert fest, da Sie sich von diesem Gateway verbinden.

6. Klicken Sie für **Lokales Netzwerkgateway**auf **Auswählen eines Gateways für lokales Netzwerk** , und wählen Sie Lokales Netzwerkgateways, das Sie verwenden möchten. 

7. **Schlüssel freigegeben**muss hier der Wert der Wert entsprechen, den Sie für Ihr lokales VPN-Gerät verwenden. Wenn Ihr Gerät VPN auf Ihr lokales Netzwerk ein freigegebenes Schlüssels zur Verfügung steht, können Sie eine bilden und Eingabemethoden sie hier und auf dem lokalen Gerät. Wichtig ist, dass sie beide entsprechen.

8. Die restlichen Werte für **Abonnements**, **Ressourcengruppe**und den **Standort** sind fest.

9. Klicken Sie auf **OK** , um die Verbindung zu erstellen. *Verbindung erstellen* , die auf dem Bildschirm blinken sehen.

10. Wenn die Verbindung abgeschlossen ist, sehen Sie es in das Blade **Verbindungen** für Ihr Gateway angezeigt.

    ![Erstellen von Website-zu-Standort-Verbindung](./media/vpn-gateway-add-site-to-site-connection-rm-portal-include/connectionstatus450.png)

