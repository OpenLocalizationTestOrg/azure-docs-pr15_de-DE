1. Klicken Sie im Portal aus **allen Ressourcen**auf **+ Hinzufügen**. Klicken Sie in das **Alles** Blade Suchfeld Geben Sie ein **Gateway für lokales Netzwerk**und dann auf zum Suchen. Dadurch wird eine Liste zurückgegeben. Klicken Sie auf **Lokales Netzwerkgateway** , um das Blade zu öffnen, und klicken Sie dann klicken Sie auf **Erstellen** , um das Blade **Erstellen lokales Netzwerkgateway** zu öffnen.

    ![Erstellen von lokalen Netzwerkgateway](./media/vpn-gateway-add-lng-rm-portal-include/addlng250.png)

2. Klicken Sie auf das **Erstellen lokales Netzwerk Gateway Blade**Geben Sie einen **Namen** für Ihr lokales Netzwerk Gateway-Objekt ein.
 
3. Geben Sie eine gültige öffentliche **IP-Adresse** für den VPN-Gerät oder virtuelle Netzwerk-Gateway, den Sie eine Verbindung herstellen möchten.<br>Wenn diese lokale Netzwerk einen lokalen Speicherort darstellt, ist dies die öffentliche IP-Adresse des Geräts VPN, die Sie in eine Verbindung herstellen möchten. Es kann nicht hinter NAT und Azure erreichbar sein soll.<br>Wenn diese lokale Netzwerk ein anderes VNet darstellt, geben Sie den öffentlichen IP-Adresse an, die mit dem Gateway virtuelles Netzwerk für die VNet zugewiesen wurde.<br>

4. **Adressbereichs** bezieht sich auf die Adressbereiche für das Netzwerk, das diesem lokale Netzwerk darstellt. Sie können mehrere Adressbereiche Abstand hinzufügen. Stellen Sie sicher, dass die Bereiche, die Sie hier angeben nicht mit anderen Netzwerken Zellbereiche die gewünschte überlappen Verbindung zu.
 
5. Für **Abonnements**stellen Sie sicher, dass das richtige Abonnement angezeigt wird.

6. Markieren Sie die Ressourcengruppe aus, der Sie verwenden möchten, für **Ressourcengruppe**. Sie können entweder eine neue Ressourcengruppe erstellen, oder wählen Sie eine, die bereits erstellt haben.

7. **Speicherort**wählen Sie einen Speicherort für dem in diesem Objekt erstellt wird. Soll am selben Speicherort auswählen, dem in Ihrem VNet befindet, aber es ist nicht dazu erforderlich.

8. Klicken Sie auf **Erstellen** , um das Gateway lokales Netzwerk zu erstellen.
