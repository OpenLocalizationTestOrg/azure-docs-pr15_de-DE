Ein Azure System zum Lastenausgleich ist ein System zum Lastenausgleich von Layer 4 (TCP, UDP). Das System zum Lastenausgleich bietet hohe Verfügbarkeit durch Verteilen von eingehenden Datenverkehr zwischen fehlerfrei Dienstinstanzen in der Cloud-Dienste oder virtuelle Computer in einem System zum Lastenausgleich. Azure System zum Lastenausgleich kann auch diese Dienste auf mehrere Ports, mehrere IP-Adressen oder beides darstellen.

Sie können ein System zum Lastenausgleich zu konfigurieren:

* Laden des Lastenausgleichs für eingehenden Internet-Datenverkehrs auf virtuellen Computern (VMs). Zusammenfassend ein System zum Lastenausgleich in diesem Szenario als ein [System zum Lastenausgleich Internetzugriff](../articles/load-balancer/load-balancer-internet-overview.md).
* Laden des Lastenausgleichs für Datenverkehr zwischen VMs in ein virtuelles Netzwerk (VNet), VMs in der Cloud-Dienste oder zwischen lokalen Computern und virtuellen Computern in einer standortübergreifenden virtuelles Netzwerk. Zusammenfassend ein System zum Lastenausgleich in diesem Szenario als eine [interne System zum Lastenausgleich (ILB)](../articles/load-balancer/load-balancer-internal-overview.md).
* Weiterleiten von externen Datenverkehr an eine bestimmte VM-Instanz.
