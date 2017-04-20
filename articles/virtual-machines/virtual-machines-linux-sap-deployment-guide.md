<properties
   pageTitle="SAP NetWeaver auf Linux virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch | Microsoft Azure"
   description="SAP NetWeaver auf Linux virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch"
   services="virtual-machines-linux"
   documentationCenter=""
   authors="MSSedusch"
   manager="timlt"
   editor=""
   tags="azure-resource-manager"
   keywords=""/>
<tags
   ms.service="virtual-machines-linux"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="vm-linux"
   ms.workload="infrastructure-services"
   ms.date="08/18/2016"
   ms.author="sedusch"/>

# <a name="sap-netweaver-on-azure-virtual-machines-vms--deployment-guide"></a>SAP NetWeaver auf Azure-virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch

[767598]:https://service.sap.com/sap/support/notes/767598
[773830]:https://service.sap.com/sap/support/notes/773830
[826037]:https://service.sap.com/sap/support/notes/826037
[965908]:https://service.sap.com/sap/support/notes/965908
[1031096]:https://service.sap.com/sap/support/notes/1031096
[1139904]:https://service.sap.com/sap/support/notes/1139904
[1173395]:https://service.sap.com/sap/support/notes/1173395
[1245200]:https://service.sap.com/sap/support/notes/1245200
[1409604]:https://service.sap.com/sap/support/notes/1409604
[1558958]:https://service.sap.com/sap/support/notes/1558958
[1585981]:https://service.sap.com/sap/support/notes/1585981
[1588316]:https://service.sap.com/sap/support/notes/1588316
[1590719]:https://service.sap.com/sap/support/notes/1590719
[1597355]:https://service.sap.com/sap/support/notes/1597355
[1605680]:https://service.sap.com/sap/support/notes/1605680
[1619720]:https://service.sap.com/sap/support/notes/1619720
[1619726]:https://service.sap.com/sap/support/notes/1619726
[1619967]:https://service.sap.com/sap/support/notes/1619967
[1750510]:https://service.sap.com/sap/support/notes/1750510
[1752266]:https://service.sap.com/sap/support/notes/1752266
[1757924]:https://service.sap.com/sap/support/notes/1757924
[1757928]:https://service.sap.com/sap/support/notes/1757928
[1758182]:https://service.sap.com/sap/support/notes/1758182
[1758496]:https://service.sap.com/sap/support/notes/1758496
[1772688]:https://service.sap.com/sap/support/notes/1772688
[1814258]:https://service.sap.com/sap/support/notes/1814258
[1882376]:https://service.sap.com/sap/support/notes/1882376
[1909114]:https://service.sap.com/sap/support/notes/1909114
[1922555]:https://service.sap.com/sap/support/notes/1922555
[1928533]:https://service.sap.com/sap/support/notes/1928533
[1941500]:https://service.sap.com/sap/support/notes/1941500
[1956005]:https://service.sap.com/sap/support/notes/1956005
[1973241]:https://service.sap.com/sap/support/notes/1973241
[1984787]:https://service.sap.com/sap/support/notes/1984787
[1999351]:https://service.sap.com/sap/support/notes/1999351
[2002167]:https://service.sap.com/sap/support/notes/2002167
[2015553]:https://service.sap.com/sap/support/notes/2015553
[2039619]:https://service.sap.com/sap/support/notes/2039619
[2121797]:https://service.sap.com/sap/support/notes/2121797
[2134316]:https://service.sap.com/sap/support/notes/2134316
[2178632]:https://service.sap.com/sap/support/notes/2178632
[2191498]:https://service.sap.com/sap/support/notes/2191498
[2233094]:https://service.sap.com/sap/support/notes/2233094
[2243692]:https://service.sap.com/sap/support/notes/2243692

[azure-cli]:../xplat-cli-install.md
[azure-portal]:https://portal.azure.com
[azure-ps]:../powershell-install-configure.md
[azure-quickstart-templates-github]:https://github.com/Azure/azure-quickstart-templates
[azure-script-ps]:https://go.microsoft.com/fwlink/p/?LinkID=395017
[azure-subscription-service-limits]:../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../azure-subscription-service-limits.md#subscription

[Dbms-guide]:virtual-machines-linux-sap-dbms-guide.md (SAP NetWeaver auf Linux virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch DBMS) [Dbms-guide-2.1]:virtual-machines-linux-sap-dbms-guide.md#c7abf1f0-c927-4a7c-9c1d-c7b5b3b7212f (Zwischenspeichern für virtuellen Computern und virtuelle Festplatten) [Dbms-guide-2.2]:virtual-machines-linux-sap-dbms-guide.md#c8e566f9-21b7-4457-9f7f-126036971a91 (Software RAID) [Dbms-guide-2.3]:virtual-machines-linux-sap-dbms-guide.md#10b041ef-c177-498a-93ed-44b3441ab152 (Microsoft Azure-Speicher) [Dbms-guide-2]:virtual-machines-linux-sap-dbms-guide.md#65fa79d6-a85f-47ee-890b-22e794f51a64 (Struktur einer Bereitstellung RDBMS) [Dbms-guide-3]:virtual-machines-linux-sap-dbms-guide.md#871dfc27-e509-4222-9370-ab1de77021c3 (hohen Verfügbarkeit und Wiederherstellung mit Azure-virtuellen Computern) [dbms-guide-5.5.1]:virtual-machines-linux-sap-dbms-guide.md# 0fef0e79-d3fe-4ae2-85AF-73666a6f7268 (SQL Server 2012 SP1 CU4 und höher) [Dbms-guide-5.5.2]:virtual-machines-linux-sap-dbms-guide.md#f9071eff-9d72-4f47-9da4-1852d782087b (SQL Server 2012 SP1 CU3 und frühere Versionen) [Dbms-guide-5.6]:virtual-machines-linux-sap-dbms-guide.md#1b353e38-21b3-4310-aeb6-a77e7c8e81c8 (mit einer SQL Server-Bilder aus Microsoft Azure Marketplace) [Dbms-guide-5.8]:virtual-machines-linux-sap-dbms-guide.md#9053f720-6f3b-4483-904d-15dc54141e30 (allgemeiner SQL Server für SAP auf Azure Zusammenfassung) [Dbms-guide-5]:virtual-machines-linux-sap-dbms-guide.md#3264829e-075e-4d25-966e-a49dad878737 (Einzelheiten zu SQL Server-RDBMS) [Dbms-guide-8.4.1]:virtual-machines-linux-sap-dbms-guide.md#b48cfe3b-48e9-4f5b-a783-1d29155bd573 (Speicherkonfiguration) [dbms-guide-8.4.2]:virtual-machines-linux-sap-dbms-guide.md# 23c78d3b-ca5a-4e72-8a24-645d141a3f5d (Sichern und Wiederherstellen) [Dbms-guide-8.4.3]:virtual-machines-linux-sap-dbms-guide.md#77cd2fbb-307e-4cbf-a65f-745553f72d2c (Sicherung für sichern und Wiederherstellen der Leistung) [Dbms-guide-8.4.4]:virtual-machines-linux-sap-dbms-guide.md#f77c1436-9ad8-44fb-a331-8671342de818 (andere) [Dbms-guide-900-sap-cache-server-on-premises]:virtual-machines-linux-sap-dbms-guide.md#642f746c-e4d4-489d-bf63-73e80177a0a8

[dbms-guide-figure-100]:./media/virtual-machines-shared-sap-dbms-guide/100_storage_account_types.png
[dbms-guide-figure-200]:./media/virtual-machines-shared-sap-dbms-guide/200-ha-set-for-dbms-ha.png
[dbms-guide-figure-300]:./media/virtual-machines-shared-sap-dbms-guide/300-reference-config-iaas.png
[dbms-guide-figure-400]:./media/virtual-machines-shared-sap-dbms-guide/400-sql-2012-backup-to-blob-storage.png
[dbms-guide-figure-500]:./media/virtual-machines-shared-sap-dbms-guide/500-sql-2012-backup-to-blob-storage-different-containers.png
[dbms-guide-figure-600]:./media/virtual-machines-shared-sap-dbms-guide/600-iaas-maxdb.png
[dbms-guide-figure-700]:./media/virtual-machines-shared-sap-dbms-guide/700-livecach-prod.png
[dbms-guide-figure-800]:./media/virtual-machines-shared-sap-dbms-guide/800-azure-vm-sap-content-server.png
[dbms-guide-figure-900]:./media/virtual-machines-shared-sap-dbms-guide/900-sap-cache-server-on-premises.png

[Deployment-guide]:virtual-machines-linux-sap-deployment-guide.md (SAP NetWeaver auf Linux virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch) [Deployment-guide-2.2]:virtual-machines-linux-sap-deployment-guide.md#42ee2bdb-1efc-4ec7-ab31-fe4c22769b94 (SAP-Ressourcen) [Deployment-guide-3.1.2]:virtual-machines-linux-sap-deployment-guide.md#3688666f-281f-425b-a312-a77e7db2dfab (Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild) [deployment-guide-3.2]:virtual-machines-linux-sap-deployment-guide.md#db477013-9060-4602-9ad4-b0316f8bb281 (Szenario 1: Bereitstellen eines virtuellen Computers aus Azure Marketplace für SAP) [deployment-guide-3.3]:virtual-machines-linux-sap-deployment-guide.md#54a1fc6d-24fd-4feb-9c57-ac588a55dff2 (Szenario 2: Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild für SAP) [deployment-guide-3.4]:virtual-machines-linux-sap-deployment-guide.md#a9a60133-a763-4de8-8986-ac0fa33aa8c1 () Szenario 3: Verschieben eines virtuellen Computers aus lokalen Verwenden einer nicht GRG Azure-virtuellen mit SAP) [Deployment-guide-3]:virtual-machines-linux-sap-deployment-guide.md#b3253ee3-d63b-4d74-a49b-185e76c4088e (Bereitstellung Szenarien von virtuellen Computern für SAP auf Microsoft Azure) [Deployment-guide-4.1]:virtual-machines-linux-sap-deployment-guide.md#604bcec2-8b6e-48d2-a944-61b0f5dee2f7 (Bereitstellen von Azure PowerShell-Cmdlets) [Deployment-guide-4.2]:virtual-machines-linux-sap-deployment-guide.md#7ccf6c3e-97ae-4a7a-9c75-e82c37beb18e (herunterladen und importieren SAP relevanten PowerShell-Cmdlets) [Deployment-guide-4.3]:virtual-machines-linux-sap-deployment-guide.md#31d9ecd6-b136-4c73-b61e-da4a29bbc9cc (teilnehmen virtueller Computer in der lokalen Domäne - nur Windows) [Deployment-guide-4.4.2]:virtual-machines-linux-sap-deployment-guide.md#6889ff12-eaaf-4f3c-97e1-7c9edc7f7542 (Linux) [Bereitstellung Leitfaden 4,4]: Virtual-Machines-Linux-SAP-Deployment-Guide.MD#c7cbb0dc-52a4-49db-8e03-83e7edc2927d (herunterladen, installieren und Aktivieren von Azure-virtuellen Computer-Agent) [Deployment-guide-4.5.1]:virtual-machines-linux-sap-deployment-guide.md#987cf279-d713-4b4c-8143-6b11589bb9d4 (Azure PowerShell) [Deployment-guide-4.5.2]:virtual-machines-linux-sap-deployment-guide.md#408f3779-f422-4413-82f8-c57a23b4fc2f (Azure CLI) [Deployment-guide-4.5]:virtual-machines-linux-sap-deployment-guide.md#d98edcd3-f2a1-49f7-b26a-07448ceb60ca (Konfigurieren Azure erweiterte Überwachung Erweiterung für SAP) [Deployment-guide-5.1]:virtual-machines-linux-sap-deployment-guide.md#bb61ce92-8c5c-461f-8c53-39f5e5ed91f2 (Readiness überprüfen Azure erweiterte Überwachung für SAP) [Deployment-guide-5.2]:virtual-machines-linux-sap-deployment-guide.md#e2d592ff-b4ea-4a53-a91a-e5521edb6cd1 (integritätsprüfung für Azure Überwachung Infrastruktur Konfiguration) [Deployment-guide-5.3]:virtual-machines-linux-sap-deployment-guide.md#fe25a7da-4e4e-4388-8907-8abc2d33cfd8 (weiteren Azure Überwachung Infrastruktur für SAP Problembehandlung)

[deployment-guide-configure-monitoring-scenario-1]:virtual-machines-linux-sap-deployment-guide.md#ec323ac3-1de9-4c3a-b770-4ff701def65b (Configure Monitoring)
[deployment-guide-configure-proxy]:virtual-machines-linux-sap-deployment-guide.md#baccae00-6f79-4307-ade4-40292ce4e02d (Configure Proxy)
[deployment-guide-figure-100]:./media/virtual-machines-shared-sap-deployment-guide/100-deploy-vm-image.png
[deployment-guide-figure-1000]:./media/virtual-machines-shared-sap-deployment-guide/1000-service-properties.png
[deployment-guide-figure-11]:virtual-machines-linux-sap-deployment-guide.md#figure-11
[deployment-guide-figure-1100]:./media/virtual-machines-shared-sap-deployment-guide/1100-azperflib.png
[deployment-guide-figure-1200]:./media/virtual-machines-shared-sap-deployment-guide/1200-cmd-test-login.png
[deployment-guide-figure-1300]:./media/virtual-machines-shared-sap-deployment-guide/1300-cmd-test-executed.png
[deployment-guide-figure-14]:virtual-machines-linux-sap-deployment-guide.md#figure-14
[deployment-guide-figure-1400]:./media/virtual-machines-shared-sap-deployment-guide/1400-azperflib-error-servicenotstarted.png
[deployment-guide-figure-300]:./media/virtual-machines-shared-sap-deployment-guide/300-deploy-private-image.png
[deployment-guide-figure-400]:./media/virtual-machines-shared-sap-deployment-guide/400-deploy-using-disk.png
[deployment-guide-figure-5]:virtual-machines-linux-sap-deployment-guide.md#figure-5
[deployment-guide-figure-50]:./media/virtual-machines-shared-sap-deployment-guide/50-forced-tunneling-suse.png
[deployment-guide-figure-500]:./media/virtual-machines-shared-sap-deployment-guide/500-install-powershell.png
[deployment-guide-figure-6]:virtual-machines-linux-sap-deployment-guide.md#figure-6
[deployment-guide-figure-600]:./media/virtual-machines-shared-sap-deployment-guide/600-powershell-version.png
[deployment-guide-figure-7]:virtual-machines-linux-sap-deployment-guide.md#figure-7
[deployment-guide-figure-700]:./media/virtual-machines-shared-sap-deployment-guide/700-install-powershell-installed.png
[deployment-guide-figure-760]:./media/virtual-machines-shared-sap-deployment-guide/760-azure-cli-version.png
[deployment-guide-figure-900]:./media/virtual-machines-shared-sap-deployment-guide/900-cmd-update-executed.png
[deployment-guide-figure-azure-cli-installed]:virtual-machines-linux-sap-deployment-guide.md#402488e5-f9bb-4b29-8063-1c5f52a892d0
[deployment-guide-figure-azure-cli-version]:virtual-machines-linux-sap-deployment-guide.md#0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda
[deployment-guide-install-vm-agent-windows]:virtual-machines-linux-sap-deployment-guide.md#b2db5c9a-a076-42c6-9835-16945868e866
[deployment-guide-troubleshooting-chapter]:virtual-machines-linux-sap-deployment-guide.md#564adb4f-5c95-4041-9616-6635e83a810b (Checks and Troubleshooting for End-to-End Monitoring Setup for SAP on Azure)

[deploy-template-cli]:../resource-group-template-deploy.md#deploy-with-azure-cli-for-mac-linux-and-windows
[deploy-template-portal]:../resource-group-template-deploy.md#deploy-with-the-preview-portal
[deploy-template-powershell]:../resource-group-template-deploy.md#deploy-with-powershell

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:virtual-machines-linux-sap-get-started.md
[getting-started-dbms]:virtual-machines-linux-sap-get-started.md#1343ffe1-8021-4ce6-a08d-3a1553a4db82
[getting-started-deployment]:virtual-machines-linux-sap-get-started.md#6aadadd2-76b5-46d8-8713-e8d63630e955
[getting-started-planning]:virtual-machines-linux-sap-get-started.md#3da0389e-708b-4e82-b2a2-e92f132df89c

[getting-started-windows-classic]:virtual-machines-windows-classic-sap-get-started.md
[getting-started-windows-classic-dbms]:virtual-machines-windows-classic-sap-get-started.md#c5b77a14-f6b4-44e9-acab-4d28ff72a930
[getting-started-windows-classic-deployment]:virtual-machines-windows-classic-sap-get-started.md#f84ea6ce-bbb4-41f7-9965-34d31b0098ea
[getting-started-windows-classic-dr]:virtual-machines-windows-classic-sap-get-started.md#cff10b4a-01a5-4dc3-94b6-afb8e55757d3
[getting-started-windows-classic-ha-sios]:virtual-machines-windows-classic-sap-get-started.md#4bb7512c-0fa0-4227-9853-4004281b1037
[getting-started-windows-classic-planning]:virtual-machines-windows-classic-sap-get-started.md#f2a5e9d8-49e4-419e-9900-af783173481c

[ha-guide-classic]:http://go.microsoft.com/fwlink/?LinkId=613056

[install-extension-cli]:virtual-machines-linux-enable-aem.md

[Logo_Linux]:./media/virtual-machines-shared-sap-shared/Linux.png
[Logo_Windows]:./media/virtual-machines-shared-sap-shared/Windows.png

[msdn-set-azurermvmaemextension]:https://msdn.microsoft.com/library/azure/mt670598.aspx

[Planning-guide]:virtual-machines-linux-sap-planning-guide.md (SAP NetWeaver auf Linux virtuellen Computern (virtuellen Computern) – Planung und Implementierung Führungslinie) [Planning-guide-1.2]:virtual-machines-linux-sap-planning-guide.md#e55d1e22-c2c8-460b-9897-64622a34fdff (Ressourcen) [Planning-guide-11]:virtual-machines-linux-sap-planning-guide.md#7cf991a1-badd-40a9-944e-7baae842a058 (High Availability (HA) und Disaster Wiederherstellung (DR) für SAP NetWeaver auf Azure virtuellen Computern ausgeführt) [Planning-guide-11.4.1]:virtual-machines-linux-sap-planning-guide.md#5d9d36f9-9058-435d-8367-5ad05f00de77 (hohe Verfügbarkeit für SAP-Anwendungsserver) [Planning-guide-11.5]:virtual-machines-linux-sap-planning-guide.md#4e165b58-74ca-474f-a7f4-5e695a93204f (mithilfe von Autostart für SAP-Instanzen) [planning-guide-2.1]:virtual-machines-linux-sap-planning-guide.md# 1625df66-4cc6-4d60-9202-de8a0b77f803 (nur Cloud - virtuellen Computern Bereitstellungen in Azure ohne Abhängigkeiten Netzwerk Kunden lokal) [Planning-guide-2.2]:virtual-machines-linux-sap-planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10 (Cross lokale - Bereitstellung von einzelne oder mehrere SAP-virtuellen Computern in Azure mit dem lokalen Netzwerk vollständig integriert wird der Anforderung) [Planning-guide-3.1]:virtual-machines-linux-sap-planning-guide.md#be80d1b9-a463-4845-bd35-f4cebdb5424a (Azure Regionen) [Planning-guide-3.2.1]:virtual-machines-linux-sap-planning-guide.md#df49dc09-141b-4f34-a4a2-990913b30358 (Fehlerstrukturanalyse Domänen) [Planning-guide-3.2.2]:virtual-machines-linux-sap-planning-guide.md#fc1ac8b2-e54a-487c-8581-d3cc6625e560 (Domänen Upgrade) [Planning-guide-3.2.3]:virtual-machines-linux-sap-planning-guide.md#18810088- f9be - 4c 97-958a - 27996255c 665 (Azure Verfügbarkeit Sets) [Planning-guide-3.2]:virtual-machines-linux-sap-planning-guide.md#8d8ad4b8-6093-4b91-ac36-ea56d80dbf77 (das Microsoft Azure virtuellen Computern Konzept) [Planning-guide-3.3.2]:virtual-machines-linux-sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Speicher) [Planning-guide-5.1.1]:virtual-machines-linux-sap-planning-guide.md#4d175f1b-7353-4137-9d2f-817683c26e53 (Verschieben eines virtuellen Computers aus lokalen auf Azure mit einem Datenträger nicht GRG) [Planning-guide-5.1.2]:virtual-machines-linux-sap-planning-guide.md#e18f7839-c0e2-4385-b1e6-4538453a285c (Bereitstellen eines virtuellen Computers mit einem bestimmten Kunden-Image) [planning-guide-5.2.1]:virtual-machines-linux-sap-planning-guide.md#1b287330-944b-495d-9ea7-94b83aff73ef (Vorbereitung zum Verschieben eines virtuellen Computers aus lokalen in Azure einem Datenträger nicht GRG) [ Planning-Guide-5.2.2]:Virtual-Machines-Linux-SAP-Planning-Guide.MD#57f32b1c-0cba-4e57-ab6e-c39fe22b6ec3 (Vorbereitung für die Bereitstellung eines virtuellen Computers mit einem bestimmten Kunden-Image für SAP) [Planning-guide-5.2]:virtual-machines-linux-sap-planning-guide.md#6ffb9f41-a292-40bf-9e70-8204448559e7 (Vorbereiten virtueller Computer mit SAP für Azure) [Planning-guide-5.3.1]:virtual-machines-linux-sap-planning-guide.md#6e835de8-40b1-4b71-9f18-d45b20959b79 (Unterschied zwischen ein Azure Datenträger und Azure Abbildung) [Planning-guide-5.3.2]:virtual-machines-linux-sap-planning-guide.md#a43e40e6-1acc-4633-9816-8f095d5a7b6a (eine virtuelle Festplatte aus lokalen in Azure hochladen) [Planning-guide-5.4.2]:virtual-machines-linux-sap-planning-guide.md#9789b076-2011-4afa-b2fe-b07a8aba58a1 (Kopieren Datenträger zwischen Azure-Speicherkonten) [planning-guide-5.5.1]:virtual-machines-linux-sap-planning-guide.md# 4efec401-91e0-40c0-8e64-f2dceadff646 (virtueller Computer/virtuelle Festplatte Struktur für SAP-Bereitstellungen) [Planning-guide-5.5.3]:virtual-machines-linux-sap-planning-guide.md#17e0d543-7e8c-4160-a7da-dd7117a1ad9d (Einstellung Automatische Bereitstellung für angefügten Datenträger) [Planning-guide-7.1]:virtual-machines-linux-sap-planning-guide.md#3e9c3690-da67-421a-bc3f-12c520d99a30 (virtueller einzelne Computer mit SAP NetWeaver Demo-Schulung-Szenario) [Planning-guide-7]:virtual-machines-linux-sap-planning-guide.md#96a77628-a05e-475d-9df3-fb82217e8f14 (Bereitstellung von SAP-Instanzen von Cloud-Only Konzepte) [Planning-guide-9.1]:virtual-machines-linux-sap-planning-guide.md#6f0a47f3-a289-4090-a053-2521618a28c3 (Azure Überwachung Lösung für SAP) [Planning-guide-azure-premium-storage]:virtual-machines-linux-sap-planning-guide.md#ff5ad0f9-f7f4-4022-9102-af07aef3bc92 (Azure Premium Speicher)

[planning-guide-figure-100]:./media/virtual-machines-shared-sap-planning-guide/100-single-vm-in-azure.png
[planning-guide-figure-1300]:./media/virtual-machines-shared-sap-planning-guide/1300-ref-config-iaas-for-sap.png
[planning-guide-figure-1400]:./media/virtual-machines-shared-sap-planning-guide/1400-attach-detach-disks.png
[planning-guide-figure-1600]:./media/virtual-machines-shared-sap-planning-guide/1600-firewall-port-rule.png
[planning-guide-figure-1700]:./media/virtual-machines-shared-sap-planning-guide/1700-single-vm-demo.png
[planning-guide-figure-1900]:./media/virtual-machines-shared-sap-planning-guide/1900-vm-set-vnet.png
[planning-guide-figure-200]:./media/virtual-machines-shared-sap-planning-guide/200-multiple-vms-in-azure.png
[planning-guide-figure-2100]:./media/virtual-machines-shared-sap-planning-guide/2100-s2s.png
[planning-guide-figure-2200]:./media/virtual-machines-shared-sap-planning-guide/2200-network-printing.png
[planning-guide-figure-2300]:./media/virtual-machines-shared-sap-planning-guide/2300-sapgui-stms.png
[planning-guide-figure-2400]:./media/virtual-machines-shared-sap-planning-guide/2400-vm-extension-overview.png
[planning-guide-figure-2500]:./media/virtual-machines-shared-sap-planning-guide/2500-vm-extension-details.png
[planning-guide-figure-2600]:./media/virtual-machines-shared-sap-planning-guide/2600-sap-router-connection.png
[planning-guide-figure-2700]:./media/virtual-machines-shared-sap-planning-guide/2700-exposed-sap-portal.png
[planning-guide-figure-2800]:./media/virtual-machines-shared-sap-planning-guide/2800-endpoint-config.png
[planning-guide-figure-2900]:./media/virtual-machines-shared-sap-planning-guide/2900-azure-ha-sap-ha.png
[planning-guide-figure-300]:./media/virtual-machines-shared-sap-planning-guide/300-vpn-s2s.png
[planning-guide-figure-3000]:./media/virtual-machines-shared-sap-planning-guide/3000-sap-ha-on-azure.png
[planning-guide-figure-3200]:./media/virtual-machines-shared-sap-planning-guide/3200-sap-ha-with-sql.png
[planning-guide-figure-400]:./media/virtual-machines-shared-sap-planning-guide/400-vm-services.png
[planning-guide-figure-600]:./media/virtual-machines-shared-sap-planning-guide/600-s2s-details.png
[planning-guide-figure-700]:./media/virtual-machines-shared-sap-planning-guide/700-decision-tree-deploy-to-azure.png
[planning-guide-figure-800]:./media/virtual-machines-shared-sap-planning-guide/800-portal-vm-overview.png
[planning-guide-microsoft-azure-networking]:virtual-machines-linux-sap-planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd (Microsoft Azure Networking)
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:virtual-machines-linux-sap-planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f (Storage: Microsoft Azure Storage and Data Disks)

[powershell-install-configure]:../powershell-install-configure.md
[resource-group-authoring-templates]:../resource-group-authoring-templates.md
[resource-group-overview]:../azure-resource-manager/resource-group-overview.md
[resource-groups-networking]:../virtual-network/resource-groups-networking.md
[sap-pam]:https://support.sap.com/pam (SAP Product Availability Matrix)
[sap-templates-2-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-2-tier-os-disk]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-disk%2Fazuredeploy.json
[sap-templates-2-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-2-tier-user-image%2Fazuredeploy.json
[sap-templates-3-tier-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image%2Fazuredeploy.json
[sap-templates-3-tier-user-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-user-image%2Fazuredeploy.json
[storage-azure-cli]:../storage/storage-azure-cli.md
[storage-azure-cli-copy-blobs]:../storage/storage-azure-cli.md#copy-blobs
[storage-introduction]:../storage/storage-introduction.md
[storage-powershell-guide-full-copy-vhd]:../storage/storage-powershell-guide-full.md#how-to-copy-blobs-from-one-storage-container-to-another
[storage-premium-storage-preview-portal]:../storage/storage-premium-storage.md
[storage-redundancy]:../storage/storage-redundancy.md
[storage-scalability-targets]:../storage/storage-scalability-targets.md
[storage-use-azcopy]:../storage/storage-use-azcopy.md
[template-201-vm-from-specialized-vhd]:https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd
[templates-101-simple-windows-vm]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-simple-windows-vm
[templates-101-vm-from-user-image]:https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image
[virtual-machines-linux-attach-disk-portal]:virtual-machines-linux-attach-disk-portal.md
[virtual-machines-azure-resource-manager-architecture]:../resource-manager-deployment-model.md
[virtual-machines-azurerm-versus-azuresm]:virtual-machines-linux-compare-deployment-models.md
[virtual-machines-windows-classic-configure-oracle-data-guard]:virtual-machines-windows-classic-configure-oracle-data-guard.md
[virtual-machines-linux-cli-deploy-templates]:virtual-machines-linux-cli-deploy-templates.md (Deploy and manage virtual machines by using Azure Resource Manager templates and the Azure CLI)
[virtual-machines-deploy-rmtemplates-powershell]:virtual-machines-windows-ps-manage.md (Manage virtual machines using Azure Resource Manager and PowerShell)
[virtual-machines-linux-agent-user-guide]:virtual-machines-linux-agent-user-guide.md
[virtual-machines-linux-agent-user-guide-command-line-options]:virtual-machines-linux-agent-user-guide.md#command-line-options
[virtual-machines-linux-capture-image]:virtual-machines-linux-capture-image.md
[virtual-machines-linux-capture-image-resource-manager]:virtual-machines-linux-capture-image.md
[virtual-machines-linux-capture-image-resource-manager-capture]:virtual-machines-linux-capture-image.md#capture-the-vm
[virtual-machines-linux-configure-raid]:virtual-machines-linux-configure-raid.md
[virtual-machines-linux-configure-lvm]:virtual-machines-linux-configure-lvm.md
[virtual-machines-linux-classic-create-upload-vhd-step-1]:virtual-machines-linux-classic-create-upload-vhd.md#step-1-prepare-the-image-to-be-uploaded
[virtual-machines-linux-create-upload-vhd-suse]:virtual-machines-linux-suse-create-upload-vhd.md
[virtual-machines-linux-redhat-create-upload-vhd]:virtual-machines-linux-redhat-create-upload-vhd.md
[virtual-machines-linux-how-to-attach-disk]:virtual-machines-linux-add-disk.md
[virtual-machines-linux-how-to-attach-disk-how-to-initialize-a-new-data-disk-in-linux]:virtual-machines-linux-add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk
[virtual-machines-linux-tutorial]:virtual-machines-linux-quick-create-cli.md
[virtual-machines-linux-update-agent]:virtual-machines-linux-update-agent.md
[virtual-machines-manage-availability]:virtual-machines-linux-manage-availability.md
[virtual-machines-ps-create-preconfigure-windows-resource-manager-vms]:virtual-machines-windows-ps-create.md
[virtual-machines-sizes]:virtual-machines-linux-sizes.md
[virtual-machines-windows-classic-ps-sql-alwayson-availability-groups]:virtual-machines-windows-classic-ps-sql-alwayson-availability-groups.md
[virtual-machines-windows-classic-ps-sql-int-listener]:virtual-machines-windows-classic-ps-sql-int-listener.md
[virtual-machines-sql-server-high-availability-and-disaster-recovery-solutions]:virtual-machines-windows-sql-high-availability-dr.md
[virtual-machines-sql-server-infrastructure-services]:virtual-machines-windows-sql-server-iaas-overview.md
[virtual-machines-sql-server-performance-best-practices]:virtual-machines-windows-sql-performance.md
[virtual-machines-upload-image-windows-resource-manager]:virtual-machines-windows-upload-image.md
[virtual-machines-windows-tutorial]:virtual-machines-windows-hero-tutorial.md
[virtual-machines-workload-template-sql-alwayson]:https://azure.microsoft.com/documentation/templates/sql-server-2014-alwayson-dsc/
[virtual-network-deploy-multinic-arm-cli]:../virtual-network/virtual-network-deploy-multinic-arm-cli.md
[virtual-network-deploy-multinic-arm-ps]:../virtual-network/virtual-network-deploy-multinic-arm-ps.md
[virtual-network-deploy-multinic-arm-template]:../virtual-network/virtual-network-deploy-multinic-arm-template.md
[virtual-networks-configure-vnet-to-vnet-connection]:../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md
[virtual-networks-create-vnet-arm-pportal]:../virtual-network/virtual-networks-create-vnet-arm-pportal.md
[virtual-networks-manage-dns-in-vnet]:../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md
[virtual-networks-multiple-nics]:../virtual-network/virtual-networks-multiple-nics.md
[virtual-networks-nsg]:../virtual-network/virtual-networks-nsg.md
[virtual-networks-reserved-private-ip]:../virtual-network/virtual-networks-static-private-ip-arm-ps.md
[virtual-networks-static-private-ip-arm-pportal]:../virtual-network/virtual-networks-static-private-ip-arm-pportal.md
[virtual-networks-udr-overview]:../virtual-network/virtual-networks-udr-overview.md
[vpn-gateway-about-vpn-devices]:../vpn-gateway/vpn-gateway-about-vpn-devices.md
[vpn-gateway-create-site-to-site-rm-powershell]:../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md
[vpn-gateway-cross-premises-options]:../vpn-gateway/vpn-gateway-plan-design.md
[vpn-gateway-site-to-site-create]:../vpn-gateway/vpn-gateway-site-to-site-create.md
[vpn-gateway-vpn-faq]:../vpn-gateway/vpn-gateway-vpn-faq.md
[xplat-cli]:../xplat-cli-install.md
[xplat-cli-azure-resource-manager]:../xplat-cli-azure-resource-manager.md

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]Klassische Bereitstellungsmodell.

Microsoft Azure ermöglicht Unternehmen, Datenverarbeitung und Speicher-Ressourcen in Formularlayouts ohne lange Aufträge Zyklen zu erwerben. Azure-virtuellen Computern ermöglicht Unternehmen Bereitstellen von Applications klassische, wie SAP NetWeaver Applications in Azure basierend und erweitern ihre Zuverlässigkeit und Verfügbarkeit ohne weitere Ressourcen zur Verfügung lokalen. Microsoft Azure unterstützt auch Cross lokale Konnektivität, womit Unternehmen aktiv Azure-virtuellen Computern in ihren lokalen Domänen, deren Wolken "Privat" und ihre SAP-System Querformat integrieren kann.

Diesem Whitepaper werden Schritt für Schritt beschrieben, wie eine Azure-virtuellen Computern für die Bereitstellung von Applications SAP NetWeaver Grundlage vorbereitet ist. Es wird davon ausgegangen, dass die Informationen in den [Planung und Implementierung Führungslinie] enthalten [Planungshandbuch] bekannt ist. Wenn dies nicht der Fall ist, sollte das jeweilige Dokument zuerst gelesen werden.

Das Papier ergänzen die SAP-Installationsdokumentation und SAP-Notizen, die die primären Ressourcen für Installationen und -Bereitstellungen mit SAP-Software auf bestimmten Plattformen darstellen.

[AZURE.INCLUDE [windows-warning](../../includes/virtual-machines-linux-sap-warning.md)]

## <a name="introduction"></a>Einführung
Eine große Anzahl von Unternehmen weltweit SAP NetWeaver-basierten Anwendungen – am häufigsten markante die SAP-Business Suite – verwenden, um ihrer Aufgabe kritische auszuführen Geschäftsprozesse. Des Systemzustands ist deshalb eine Anlage entscheidend, und die Möglichkeit, die Enterprise-Unterstützung bei einer Fehlfunktion, einschließlich Performance-Ereignissen wichtige erforderlich wird.
Microsoft Azure bietet übergeordnete Plattform Instrumentation an den Anforderungen Unterstützung aller wichtigen branchenanwendungen Tabellenbereich an. Dieses Handbuch stellt sicher, dass eine Microsoft Azure virtuellen Computern als Ziel für die Bereitstellung von SAP-Software so konfiguriert ist, dass Enterprise Support, unabhängig davon angeboten werden kann die Weise des virtuellen Computers erstellt wird, ihn aus dem Azure Marketplace geöffnet werden oder ein bestimmtes Bild mit Kunden verwenden.
In der folgenden, alle notwendigen Einrichtung werden die Schritte ausführlich beschrieben.

## <a name="prerequisites-and-resources"></a>Voraussetzungen und Ressourcen
### <a name="prerequisites"></a>Erforderliche Komponenten
Bevor Sie beginnen, stellen Sie sicher, dass die erforderlichen Komponenten, die die in der folgenden Kapitel beschrieben sind erfüllt sind.

#### <a name="local-personal-computer"></a>Lokale PC
Die Einrichtung einer Azure virtuellen Computern für die Bereitstellung von SAP-Software umfasst mehrere Schritte erforderlich ist. Zum Verwalten von Windows-virtuellen Computern oder Linux virtuellen Computern müssen Sie ein PowerShell-Skript und das Microsoft Azure-Portal zu verwenden. Für das ist eine lokale PC unter Windows 7 oder höher erforderlich. Wenn Sie nur möchten Verwalten von Linux virtuellen Computern und einen Linux-Computer für diese Aufgabe verwenden möchten, können Sie auch die Azure Befehlszeilenschnittstelle (Azure).

#### <a name="internet-connection"></a>Verbindung mit dem Internet
Zum Herunterladen und Ausführen der erforderliche Tools und Skripts, ist ein Internetzugang erforderlich. Darüber hinaus, benötigt der Microsoft Azure virtuellen Computern ausführen Azure erweiterte Überwachung Erweiterung Zugriff auf das Internet an. Bei diesem Azure-virtuellen Computer Teil einer Azure-virtuellen Netzwerk oder eine lokale Domäne handelt, stellen Sie sicher, dass die relevanten Proxyeinstellungen festgelegt sind, wie in Kapitel [Proxy konfigurieren] beschrieben[ deployment-guide-configure-proxy] in diesem Dokument.

#### <a name="microsoft-azure-subscription"></a>Microsoft Azure-Abonnement
Ein Azure-Konto bereits vorhanden ist, und entsprechende Anmeldeinformationen bekannt sind.

#### <a name="topology-consideration-and-networking"></a>Suchtopologie Aspekte und Netzwerke
Die Suchtopologie und der SAP-Bereitstellung in Azure-Architektur muss definiert werden. Architektur im Hinblick auf:

* Microsoft Azure-Speicher Konten verwendet werden
* Bereitstellen von SAP-System in virtuelles Netzwerk
* Bereitstellen von SAP-System in Ressourcengruppe
* Bereitstellen von SAP-System Azure Region
* SAP-Konfiguration (Ebene 2 oder Ebene 3)
* Virtueller Computer der Größe und Anzahl von zusätzlichen virtuellen Festplatten zu den VM(s) bereitgestellt werden soll
* SAP-Transport und Korrektur Systemkonfiguration

Azure-Speicherkonten oder Azure virtuelle Netzwerke sollte als solche erstellt und konfiguriert wurden bereits. So erstellen und konfigurieren sie fällt [Planung und Implementierung Leitfaden] [Planungshandbuch].

#### <a name="sap-sizing"></a>SAP-Ziehpunkt
* Die geplante SAP-Arbeitsbelastung festgelegt wurden, z. B. mithilfe der SAP-Quicksizer und die entsprechende SAPS Anzahl bekannt ist 
* Die erforderlichen CPU-Ressourcen und Speicherkapazität Auslastung des SAP-Systems sollte bekannt sein
* Die erforderlichen e/a-Vorgänge pro Sekunde sollte bekannt sein
* Die erforderliche Bandbreite in tatsächlichen Kommunikation zwischen verschiedenen virtuellen Computern in Azure ist bezeichnet.
* Die erforderliche Bandbreite zwischen der lokalen Bestand und die Azure bereitgestellt SAP Systeme ist bekannt.

#### <a name="resource-groups"></a>Ressourcengruppen
Ressourcengruppen sind ein neues Konzept, die alle Ressourcen enthalten, die den gleichen Lebenszyklus z. B. sie erstellt sind, und gleichzeitig gelöscht haben. Lesen Sie [diesen Artikel] [ resource-group-overview] für Weitere Informationen zu Ressourcengruppen. 

### <a name="42ee2bdb-1efc-4ec7-ab31-fe4c22769b94"></a>SAP-Ressourcen
Während der Konfigurationsarbeit sind die folgenden Ressourcen erforderlich:

* SAP-Hinweis [1928533]
    * die Liste der Azure-virtuellen Computern an Papiergrößen, die für die Bereitstellung von SAP-Software unterstützt werden 
    * wichtige Kapazitätsinformationen pro Größe Azure-virtuellen Computern
    * unterstützte SAP-Software und Kombination von OS und DB
* SAP-Hinweis [2015553] auflisten erforderliche Komponenten von SAP unterstützt werden müssen, wenn Sie SAP-Software in Microsoft Azure bereitstellen.
* SAP-Hinweis [1999351] , enthält weitere Informationen zur Problembehandlung für die erweiterte Azure Überwachung für SAP.
* SAP-Hinweis [2178632] , enthält detaillierte Informationen auf alle verfügbaren Überwachung Kriterien für SAP auf Microsoft Azure. 
* SAP-Hinweis [1409604] , die die erforderliche SAP-Host Agent-Version für Windows auf Microsoft Azure enthält, wenn Sie auf der neuen Azure Ressourcenmanager bereitstellen.
* SAP-Hinweis [2191498] , die die erforderliche SAP-Host Agent-Version für Linux auf Microsoft Azure enthält, wenn Sie auf der neuen Azure Ressourcenmanager bereitstellen.
* Informationen zur Lizenzierung für SAP auf Linux auf Azure mit SAP-Hinweis [2243692]
* SAP-Hinweis [1984787] , enthält allgemeine Informationen zu SUSE LINUX Enterprise Server 12
* Hinweis [2002167] , allgemeine Informationen Red Hat Enterprise Linux enthält SAP 7.x
* [SCN](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) , die alle enthält erforderlich SAP-Notizen für Linux
* SAP-bestimmte PowerShell-Cmdlets, die Teil des [Azure PowerShell] sind[azure-ps]
* SAP-bestimmte Azure CLI [Azure CLI] gehören[azure-cli]
* [Microsoft Azure-Portal][azure-portal]

[comment]: <> (MSSedusch erledigen hinzufügen Cloud Patchebene für SAP-Host Agent im SAP-Hinweis 1409604)
 
Die folgenden Handbücher behandeln als auch das Thema der SAP auf Microsoft Azure:

* [SAP NetWeaver auf Azure-virtuellen Computern (virtuellen Computern) – Planung und Implementierung Führungslinie] [Planungshandbuch]
* [SAP NetWeaver auf Azure-virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch (dieses Dokument)] [Bereitstellungshandbuch]
* [SAP NetWeaver auf Azure-virtuellen Computern (virtuellen Computern) – Bereitstellungshandbuch DBMS] [Dbms-Leitfadens]

## <a name="b3253ee3-d63b-4d74-a49b-185e76c4088e"></a>Szenarien für die Bereitstellung von virtuellen Computern für SAP auf Microsoft Azure
In diesem Kapitel erfahren Sie, die verschiedenen Arten von Bereitstellung und die einzelnen Schritte für jeden Bereitstellung.

### <a name="deployment-of-vms-for-sap"></a>Bereitstellung von virtuellen Computern für SAP
Microsoft Azure bietet mehrere Methoden zum Bereitstellen von virtuellen Computern und die zugehörigen Festplatten. Somit ist es sehr wichtig, die Unterschiede kennen, da Vorbereitungen von der virtuellen Maschinen hängt von der Möglichkeit der Bereitstellung abweichen. Im Allgemeinen sehen wir in den folgenden Szenarien:

#### <a name="deploying-a-vm-out-of-the-azure-marketplace"></a>Bereitstellen eines virtuellen Computers aus dem Azure Marketplace
Möchten Sie eine Microsoft oder 3rd Party bereitgestellten aus dem Azure Marketplace Bild Ihrer virtuellen Computer bereitstellen. Nachdem Sie Ihre virtuellen Computer auf Microsoft Azure bereitgestellt haben, führen Sie dieselben Richtlinien und Tools für die SAP-Software innerhalb der virtuellen Computer zu installieren, wie Sie in einer lokalen Umgebung tun würden. Für die Installation der Software SAP-innerhalb des Azure-virtuellen Computers, empfiehlt sich SAP und Microsoft zum Hochladen und Speichern der SAP-Installationsmedien Azure-virtuellen Festplatten oder zum Erstellen einer Azure-virtuellen Computer als 'Dateiserver' die enthält alle erforderlichen SAP-Installationsmedien arbeiten.

[comment]: <> (MSSedusch TODO warum wir empfehlen eine Dateimanagement z. B. Dateiserver oder virtuelle Festplatte sonst? Ist, die so anders aus lokalen?)

Weitere Informationen hierzu finden Sie unter Kapitel [Szenario 1: Bereitstellen eines virtuellen Computers aus Azure Marketplace für SAP] [Bereitstellung Leitfaden 3,2].

#### <a name="3688666f-281f-425b-a312-a77e7db2dfab"></a>Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild
Aufgrund von bestimmter Patch Anforderungen hinsichtlich des Workflowversion OS oder DBMS möglicherweise bereitgestellten Bilder aus dem Azure Marketplace nicht Ihren Anforderungen anpassen. Daher müssen Sie zum Erstellen eines virtuellen Computers verwenden eigener 'Privat' OS/DB Virtueller Computer Bilder die danach mehrmals bereitgestellt werden kann.
Die Schritte zum Erstellen eines Bildes als "Privat" unterscheiden sich zwischen einem Windows und ein Bild Linux.

___

> ![Windows][Logo_Windows] Windows
>
> Um ein Windows-Abbild vorbereiten, die zum Bereitstellen von mehreren virtuellen Computern verwendet werden kann, müssen die Windows-Einstellungen (wie Windows-SID und Hostname) auf dem lokalen virtuellen Computer abstrahiert/GRG sein. Dies kann mithilfe von Sysprep wie auf <https://technet.microsoft.com/library/cc721940.aspx>beschrieben.
>
> ![Linux][Logo_Linux] Linux
>
> Um ein Bild Linux vorzubereiten, die zum Bereitstellen von mehreren virtuellen Computern verwendet werden können, müssen einige Linux Einstellungen des lokalen virtuellen Computers abstrahiert/GRG sein. Dies kann mithilfe von Waagent-Entziehen von in [diesem Artikel] beschriebenen[ virtual-machines-linux-capture-image] oder in [diesem Artikel][virtual-machines-linux-agent-user-guide-command-line-options].

___

Sie können Ihre Datenbankinhalt einrichten, indem Sie entweder mit dem SAP Software bereitstellen Manager installieren eines neuen SAP-System, eine Sicherungskopie der Datenbank wiederherstellen, von einer virtuellen Festplatte, der mit dem virtuellen Computer angeschlossen ist oder Wiederherstellen einer Sicherungskopie der Datenbank direkt aus Azure-Speicher aus, wenn das DBMS unterstützt. (Siehe [DBMS Bereitstellung Guide][dbms-guide]). Wenn Sie bereits ein SAP-System in Ihrer lokalen virtuellen Computer (besonders für Systeme der Ebene 2) installiert haben, können Sie die SAP-System-Einstellungen anpassen, nach der Bereitstellung von den Azure-virtuellen Computer durch das System umbenennen Verfahren vom SAP-Software Provisioning-Manager (SAP-Hinweis [1619720]) unterstützt. Andernfalls können Sie die SAP-Software später nach der Bereitstellung von den Azure-virtuellen Computer installieren.

Weitere Informationen hierzu finden Sie unter Kapitel [Szenario 2: Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild für SAP] [Bereitstellung Leitfaden 3.3].

#### <a name="moving-a-vm-from-on-premises-to-microsoft-azure-with-a-non-generalized-disk"></a>Verschieben eines virtuellen Computers zu Microsoft Azure aus lokalen einem Datenträger nicht GRG
Sie möchten ein bestimmtes SAP-System von lokalen Microsoft Azure wechseln. Dies kann die virtuelle Festplatte, die das Betriebssystem, die SAP-Binärdateien und tatsächlichen DBMS Binärdateien enthält sowie die virtuellen Festplatten mit den Daten, und melden Sie sich Dateien des DBMS in Microsoft Azure hochladen erfolgen. In entgegengesetzt zu dem Szenario beschrieben in Kapitel [Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild] [Bereitstellung-Leitfaden-3.1.2] über Sie behalten Hostname, SAP-SID und SAP-Benutzerkonten auf dem Azure-virtuellen Computer, wie sie in der lokalen Umgebung konfiguriert wurden. Daher ist es nicht erforderlich, die das Betriebssystem verallgemeinern. Diesem Fall wendet hauptsächlich für Cross lokale Szenarien, wo ein Teil der SAP-Querformat lokalen und Webparts auf Microsoft Azure ausgeführt wird.

Weitere Informationen hierzu finden Sie unter Kapitel [Szenario 3: Verschieben eines virtuellen Computers aus lokalen mithilfe einer nicht GRG Azure-virtuellen mit SAP] [Bereitstellung Leitfaden 3.4].

### <a name="db477013-9060-4602-9ad4-b0316f8bb281"></a>Szenario 1: Bereitstellen eines virtuellen Computers, aus dem Azure Marketplace für SAP
Microsoft Azure bietet die Möglichkeit zum Bereitstellen einer virtuellen Computer-Instanz aus dem Azure Marketplace, seiner einige OS Standardbilder von Windows Server und anderen Linux-Versionen. Es ist es möglich, ein Bild bereitzustellen, die DBMS SKUs z.B. SqlServer umfasst. Einzelheiten mit diesen Bildern mit DBMS SKUs finden Sie in der [DBMS Bereitstellungshandbuch] [Dbms-Leitfadens]

SAP-Folge von Schritten Bereitstellen eines virtuellen Computers aus dem Azure Marketplace aussehen würde:

![Flussdiagramm des Bereitstellung für SAP-Systeme mithilfe eines Bilds virtuellen Computer aus Azure Marketplace][deployment-guide-figure-100]

Nach der Flussdiagramm ausgeführt werden müssen die folgenden Schritte aus:

#### <a name="create-virtual-machine-using-the-azure-portal"></a>Erstellen von virtuellen Computern, die über das Azure-Portal
Die einfachste Möglichkeit zum Erstellen eines neuen virtuellen Computers verwenden eines Bilds aus dem Azure Marketplace ist über das Azure-Portal. Navigieren Sie zu <https://portal.azure.com/#create>. Geben Sie die Art des Betriebssystems, die Sie in das Suchfeld ein, z. B. Windows, SLES oder RHEL bereitstellen, und wählen Sie die Version möchten. Vergewissern Sie sich, wählen Sie das Bereitstellungsmodell "Azure Ressourcenmanager", und klicken Sie auf erstellen.

Der Assistent führt Sie durch die erforderlichen Parameter zum Erstellen des virtuellen Computers sowie alle erforderlichen Ressourcen wie Netzwerk-Schnittstellen oder Speicherkonten. Einige dieser Parameter sind:

1. Grundlagen
    1. Name: Der Name der Ressource h. Name des virtuellen Computers
    1. Benutzername und Kennwort/SSH öffentlicher Schlüssel: Geben Sie den Benutzernamen und das Kennwort des Benutzers, die während der Bereitstellung erstellt wird. Für eine Linux virtuellen Computern, Sie können auch eingeben den öffentlichen SSH-Schlüssel, die Sie verwenden möchten, melden Sie den Computer mithilfe von SSH.
    1. Abonnements: Wählen Sie das Abonnement, das Sie verwenden, um den neuen virtuellen Computer bereitstellen möchten.
    1. Ressourcengruppe: Der Name der Ressourcengruppe. Sie können entweder den Namen einer neuen Gruppe für die Ressource oder eine Ressourcengruppe aus, die bereits einfügen
    1. Standort: Wählen Sie den Speicherort, in dem die neuen virtuellen Computern bereitgestellt werden sollen. Wenn Sie eine Verbindung mit Ihrem lokalen Netzwerk des virtuellen Computers möchten, stellen Sie sicher, um die Position des virtuellen Netzwerks auszuwählen, die Azure mit Ihrem lokalen Netzwerk verbunden. Weitere Informationen hierzu finden Sie unter [Microsoft Azure Networking] Kapitel[ planning-guide-microsoft-azure-networking] im [Planungshandbuch] [Planungshandbuch].
1. Größe: Lesen Sie bitte SAP-Hinweis [1928533] für eine Liste der unterstützten Typen von virtuellen Computer. Auch Stellen Sie sicher, dass die richtige Art zu aktivieren, wenn Sie Premium Speicher verwenden möchten. Nicht alle Typen von virtuellen Computer unterstützen Premium-Speicher. Finden Sie unter Kapitel [Speicher: Microsoft Azure-Speicher und Daten Datenträger] [ planning-guide-storage-microsoft-azure-storage-and-data-disks] und [Azure Premium Speicher] [Planung-Leitfaden-Azure-Premium-Speicher] in das [Planungshandbuch] [Planungshandbuch] Weitere Details.
1. Einstellungen
    1. Speicherkonto: Können Sie ein vorhandenes Speicherkonto aktivieren oder einen neuen erstellen. Lesen Sie Kapitel [Microsoft Azure Storage] [Dbms Leitfaden 2.3] des [DBMS Guide] [Dbms-Leitfadens] Weitere Details zu den verschiedenen Speichertypen an. Beachten Sie, dass nicht alle Typen von Speicherplatz für die Ausführung von SAP Anwendungen unterstützt werden.
    1. Virtuelles Netzwerk und Subnetz: Wählen Sie das virtuelle Netzwerk, die mit Ihrem lokalen Netzwerk verbunden ist, wenn Sie aus den virtuellen Computern in Ihr Intranet integriert werden soll.
    1. Öffentliche IP-Adresse: Wählen Sie die öffentliche IP-Adresse, die Sie verwenden, oder geben Sie den Parameter aus, um eine neue öffentliche IP-Adresse erstellen möchten. Eine öffentliche IP-Adresse können Sie Ihre virtuellen Computern über das Internet zugreifen. Vergewissern Sie sich außerdem eine Sicherheitsgruppe Netzwerk, um den Zugriff auf Ihre virtuellen Computern Filtern zu erstellen.
    1. Netzwerk-Sicherheitsgruppe: finden Sie unter [Was ist ein Netzwerk Sicherheit Gruppe (NSG)] [ virtual-networks-nsg] Weitere Details.
    1. Überwachung: Sie können die Einstellung Diagnose deaktivieren. Es wird werden automatisch aktiviert, wenn Sie die Befehle Azure erweiterte Überwachung aktivieren, wie in Kapitel [Überwachung konfigurieren]beschrieben ausführen[deployment-guide-configure-monitoring-scenario-1].
    1. Verfügbarkeit: Wählen Sie eine Sammlung Verfügbarkeit aus, oder geben Sie die Parameter zum Erstellen einer neuen Verfügbarkeit Menge. Weitere Informationen finden Sie unter Kapitel [Azure Verfügbarkeit Sätze] [planning-Leitfaden-3.2.3].
1. Zusammenfassung: Überprüfen Sie die Informationen auf der Seite "Zusammenfassung", und klicken Sie auf OK.

Nach dem Beenden Assistenten werden Ihres virtuellen Computers in der Ressourcengruppe bereitgestellt, die Sie ausgewählt haben.

#### <a name="create-virtual-machine-using-a-template"></a>Erstellen von virtuellen Computern mithilfe einer Vorlage
Sie können auch eine Bereitstellung mithilfe einer der SAP-Vorlagen im [Azure-Schnellstart-Vorlagen Github Repository]veröffentlicht erstellen[azure-quickstart-templates-github]. Oder Sie können mit dem [Azure-Portal]einen virtuellen Computer erstellen[virtual-machines-windows-tutorial], [PowerShell] [ virtual-machines-ps-create-preconfigure-windows-resource-manager-vms] oder [Azure CLI] [ virtual-machines-linux-tutorial] manuell.

* [Schicht 2-(nur eine virtuellen Computern) Konfigurationsvorlage] [ sap-templates-2-tier-marketplace-image] verwenden Sie diese Vorlage aus, wenn Sie ein Ebene 2-System, die mit nur einem virtuellen Computern erstellen möchten.
* [Schicht 3-(mehrere virtuelle Computer) Konfigurationsvorlage] [ sap-templates-3-tier-marketplace-image] verwenden Sie diese Vorlage aus, wenn Sie ein Schicht 3-System, die mit mehreren virtuellen Computern erstellen möchten.

Nachdem Sie eine der Vorlagen oben geöffnet, navigiert Azure-Portal in den Bereich Parameter bearbeiten. Geben Sie die folgenden Informationen ein:

* **SapSystemId**: SAP-System-ID
* **OsType**: Betriebssystem bereitstellen, z. B. Windows Server 2012 R2, SLES 12 oder RHEL 7.2 werden soll.
    * Die Liste enthält nur Versionen, die vom SAP auf Microsoft Azure unterstützt werden
* **SapSystemSize**: die Größe des SAP-System
    * Der Umfang der SAPS das neue System zu erhalten. Wenn Sie nicht sicher wie viele SAPS das System erforderlich sind sind, wenden Sie sich an Ihre SAP-Technologiepartner oder Systemintegrator
* **SystemAvailability**: (nur Ebene 3 Vorlage) System Verfügbarkeit 
    * Wählen Sie HA für eine Konfiguration, die für die Installation einer HA geeignet ist. Zwei Datenbankserver und zwei Server für die ASCS erstellt werden.
* StorageType: (nur Ebene 2 Vorlage) Typ Speicher, die verwendet werden soll 
    * Für Betriebssysteme vergrößern wird die Verwendung von Premium Speicher dringend empfohlen. Weitere Informationen zu den verschiedenen Speicher Datentypen finden Sie unter 
        * [Microsoft Azure-Speicher] [Dbms-Leitfaden-2.3], [Dbms-Leitfadens] [DBMS Handbuchs]
        * [Premium Speicher: Leistungsstarke Storage für Auslastung Azure-virtuellen Computern][storage-premium-storage-preview-portal]
        * [Einführung in Microsoft Azure-Speicher][storage-introduction]
* **AdminUsername** und **AdminPassword**: Benutzername und Kennwort
    * Ein neuer Benutzer wird erstellt, die zum Melden Sie sich mit dem Computer verwendet werden können.
* **NewOrExistingSubnet**: bestimmt, ob ein neues virtuelles Netzwerk und Subnetz erstellt werden soll, oder ein bestehendes Subnetz verwendet werden soll. Wenn Sie bereits über ein virtuelles Netzwerk, das mit Ihrem lokalen Netzwerk verbunden ist verfügen, wählen Sie die vorhandenen.
* **SubnetId**: die ID des im Subnetz, dem die virtuellen Computer sollen verbunden sein. Wählen Sie aus dem Subnetz des VPN oder Express-Routing virtuellen Netzwerks in Verbindung mit Ihrem lokalen Netzwerk des virtuellen Computers. Die ID in der Regel sieht /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

Nachdem Sie alle Parameter eingegeben haben, wählen Sie das Abonnement und die Ressourcengruppe aus, die Sie verwenden möchten. Sie können entweder wählen Sie eine vorhandene Ressourcengruppe oder einen neuen erstellen, indem Sie auswählen "+ neue" in dem Dropdownmenü. Wenn Sie eine neue Ressourcengruppe erstellen, müssen Sie auch den Bereich auszuwählen, in dem die Ressourcengruppe und des virtuellen Computers erstellt werden.

Überprüfen Sie die Vertragsbedingungen, akzeptieren Sie, und klicken Sie auf erstellen.

Bitte beachten Sie, dass der Azure-virtuellen Computer-Agent standardmäßig bereitgestellt wird, wenn Sie ein Bild aus dem Azure Marketplace verwenden.

#### <a name="configure-proxy-settings"></a>Konfigurieren von Proxyeinstellungen
Abhängig von Ihrer lokalen Netzwerkkonfiguration ist es möglicherweise erforderlich, um den Proxy auf Ihre virtuellen Computern konfigurieren, wenn sie mit Ihrem lokalen Netzwerk per VPN oder Express-Routing verbunden ist. Andernfalls des virtuellen Computers möglicherweise nicht zum Zugreifen auf das Internet und daher nicht die erforderlichen Erweiterungen herunterladen oder Überwachung Daten sammeln. Finden Sie in Kapitel [Proxy konfigurieren] [ deployment-guide-configure-proxy] dieses Dokuments.

#### <a name="join-domain-windows-only"></a>Teilnehmen an der Domäne (nur Windows)
In den Fall, dass die Bereitstellung in Azure, in der lokalen verbunden ist AD/DNS über Azure-Standorten oder Express-Routing (wird auch als Cross lokale in der [Planung und Implementierung Guide][planning-guide]), es wird davon ausgegangen, dass der virtuellen Computer eine lokale Domäne beitritt ist. Aspekte dieses Schritts sind in Kapitel [teilnehmen virtueller Computer in der lokalen Domäne (nur Windows)] [Bereitstellung Leitfaden 4.3] dieses Dokuments beschrieben.

#### <a name="ec323ac3-1de9-4c3a-b770-4ff701def65b"></a>Konfigurieren der Überwachung
Konfigurieren Sie die Azure erweiterte Überwachung Erweiterung für SAP beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung-Leitfaden-4.5] dieses Dokuments.

Überprüfen Sie die erforderlichen Komponenten für SAP-Überwachung für erforderlichen mindestens Versionen von SAP-Kernel und SAP-Host Agent in den Ressourcen aufgeführt, die in Kapitel [SAP-Ressourcen] [Bereitstellung Leitfaden 2.2] dieses Dokuments ein.

#### <a name="monitoring-check"></a>Kontrollkästchen für die Überwachung
Überprüfen Sie, ob die Überwachung funktioniert in Kapitel [überprüft und Problembehandlung bei End-to-End-Überwachung Setup für SAP auf Azure]beschriebenen[deployment-guide-troubleshooting-chapter].

#### <a name="post-deployment-steps"></a>Veröffentlichen Sie vor der Bereitstellung
Nach dem Erstellen des virtuellen Computer, sie bereitgestellt wird, und klicken Sie dann auf alle erforderlichen Softwarekomponenten in den virtuellen Computer installieren ist. Daher müssten diese Art von Bereitstellung Software installierten Knotenwert bereits in Microsoft Azure als Laufwerk, das angefügt werden kann oder andere virtuelle Computer verfügbar sein. Oder wir suchen in Cross lokale Szenarien darin die Verbindung zu der lokalen Anlagen (installieren Freigaben) einer angegebenen.

### <a name="54a1fc6d-24fd-4feb-9c57-ac588a55dff2"></a>Szenario 2: Bereitstellen eines virtuellen Computers durch ein benutzerdefiniertes Bild für SAP
Wie [Planung und Implementierung Leitfaden] [Planungshandbuch] bereits im detaillierten Schritte beschrieben ist es eine Möglichkeit zum Vorbereiten und erstellen ein benutzerdefiniertes Bild verwenden, um mehrere neue virtuelle Computer erstellen. Die Reihenfolge der Schritte im Flussdiagramm aussehen würde:
 
![Flussdiagramm des Bereitstellung für SAP-Systeme mithilfe eines Bilds virtueller Computer auf Privat Marketplace][deployment-guide-figure-300]

Nach der Flussdiagramm ausgeführt werden müssen die folgenden Schritte aus:

#### <a name="create-virtual-machine"></a>Erstellen von virtuellen Computern
Verwenden Sie zum Erstellen einer-Bereitstellung mit einer privaten OS Bild über das Portal Azure eine der SAP-Vorlagen auf dem [Azure-Schnellstart-Vorlagen Github Repository]veröffentlicht[azure-quickstart-templates-github].
Sie können einen virtuellen Computer mithilfe der [PowerShell] auch erstellen[ virtual-machines-upload-image-windows-resource-manager] manuell. 

* [Schicht 2-(nur eine virtuellen Computern) Konfigurationsvorlage] [ sap-templates-2-tier-user-image] verwenden Sie diese Vorlage aus, wenn Sie eine Ebene 2-System mit nur einen virtuellen Computern und ein eigenes Bild OS erstellen möchten.
* [Schicht 3-(mehrere virtuelle Computer) Konfigurationsvorlage] [ sap-templates-3-tier-user-image] verwenden Sie diese Vorlage aus, wenn Sie eine Ebene 3-System mit mehreren virtuellen Computern und ein eigenes Bild OS erstellen möchten.

Nachdem Sie eine der Vorlagen oben geöffnet, navigiert Azure-Portal in den Bereich Parameter bearbeiten. Geben Sie die folgenden Informationen ein:

* **SapSystemId**: SAP-System-ID
* **OsType**: Betriebssystemtyp bereitstellen, Windows oder Linux werden soll.
* **SapSystemSize**: die Größe des SAP-System
    * Der Umfang der SAPS das neue System zu erhalten. Wenn Sie nicht sicher wie viele SAPS das System erforderlich sind sind, wenden Sie sich an Ihre SAP-Technologiepartner oder Systemintegrator
* **SystemAvailability**: (nur Ebene 3 Vorlage) System Verfügbarkeit 
    * Wählen Sie HA für eine Konfiguration, die für die Installation einer HA geeignet ist. Zwei Datenbankserver und zwei Server für die ASCS erstellt werden.
* **StorageType**: (nur Ebene 2 Vorlage) Typ Speicher, die verwendet werden soll 
    * Für Betriebssysteme vergrößern wird die Verwendung von Premium Speicher dringend empfohlen. Weitere Informationen zu den verschiedenen Speicher Datentypen finden Sie unter 
        * [Microsoft Azure-Speicher] [Dbms-Leitfaden-2.3], [Dbms-Leitfadens] [DBMS Handbuchs]
        * [Premium Speicher: Leistungsstarke Storage für Auslastung Azure-virtuellen Computern][storage-premium-storage-preview-portal]
        * [Einführung in Microsoft Azure-Speicher][storage-introduction]
* **AdminUsername** und **AdminPassword**: Benutzername und Kennwort
    * Ein neuer Benutzer wird erstellt, die zum Melden Sie sich mit dem Computer verwendet werden können.
* **UserImageVhdUri**: URI der privaten OS Bild virtuellen Festplatte z. B. https://`<accountname`>.blob.core.windows.net/vhds/userimage.vhd
* **UserImageStorageAccount**: Name des Speicherkontos, in dem das private OS Bild z. B. gespeichert ist `<accountname`> im Beispiel oben genannten URI
* **NewOrExistingSubnet**: bestimmt, ob ein neues virtuelles Netzwerk und Subnetz erstellt werden soll, oder ein bestehendes Subnetz verwendet werden soll. Wenn Sie bereits über ein virtuelles Netzwerk, das mit Ihrem lokalen Netzwerk verbunden ist verfügen, wählen Sie die vorhandenen.
* **SubnetId**: die ID des im Subnetz, dem die virtuellen Computer sollen verbunden sein. Wählen Sie aus dem Subnetz des VPN oder Express-Routing virtuellen Netzwerks in Verbindung mit Ihrem lokalen Netzwerk des virtuellen Computers. Die ID in der Regel sieht /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

Nachdem Sie alle Parameter eingegeben haben, wählen Sie das Abonnement und die Ressourcengruppe aus, die Sie verwenden möchten. Sie können entweder wählen Sie eine vorhandene Ressourcengruppe oder einen neuen erstellen, indem Sie auswählen "+ neue" in dem Dropdownmenü. Wenn Sie eine neue Ressourcengruppe erstellen, müssen Sie auch den Bereich auszuwählen, in dem die Ressourcengruppe und des virtuellen Computers erstellt werden.

Überprüfen Sie die Vertragsbedingungen, akzeptieren Sie, und klicken Sie auf erstellen.

#### <a name="install-vm-agent-linux-only"></a>Installieren Sie virtueller Computer-Agent (nur Linux)
Der Linux-Agent muss im Bild Benutzer bereits installiert sein, wenn Sie die oben aufgeführten Vorlagen verwenden möchten. Andernfalls tritt ein Fehler die Bereitstellung. Herunterladen und Installieren des virtuellen Computer-Agents in das Bild des Benutzers, wie in Kapitel beschrieben [herunterladen, installieren und Aktivieren von Azure-virtuellen Computer-Agent] [Bereitstellung-Leitfaden-4,4] dieses Dokuments.
Wenn Sie die oben angegebenen Vorlagen nicht verwenden, können Sie auch des virtuellen Computer-Agents später installieren.

#### <a name="join-domain-windows-only"></a>Teilnehmen an der Domäne (nur Windows)
In den Fall, dass die Bereitstellung in Azure, in der lokalen verbunden ist AD/DNS über Azure-Standorten oder Express-Routing (wird auch als Cross lokale in der [Planung und Implementierung Guide][planning-guide]), es wird davon ausgegangen, dass der virtuellen Computer eine lokale Domäne beitritt ist. Aspekte dieses Schritts sind in Kapitel [teilnehmen virtueller Computer in der lokalen Domäne (nur Windows)] [Bereitstellung Leitfaden 4.3] dieses Dokuments beschrieben.

#### <a name="configure-proxy-settings"></a>Konfigurieren von Proxyeinstellungen
Abhängig von Ihrer lokalen Netzwerkkonfiguration ist es möglicherweise erforderlich, um den Proxy auf Ihre virtuellen Computern konfigurieren, wenn sie mit Ihrem lokalen Netzwerk per VPN oder Express-Routing verbunden ist. Andernfalls des virtuellen Computers möglicherweise nicht zum Zugreifen auf das Internet und daher nicht die erforderlichen Erweiterungen herunterladen oder Überwachung Daten sammeln. Finden Sie in Kapitel [Proxy konfigurieren] [ deployment-guide-configure-proxy] dieses Dokuments.

#### <a name="configure-monitoring"></a>Konfigurieren der Überwachung
Konfigurieren von Azure Überwachung Erweiterung für SAP beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung-Leitfaden-4.5] dieses Dokuments.
Überprüfen Sie die erforderlichen Komponenten für SAP-Überwachung für erforderlichen mindestens Versionen von SAP-Kernel und SAP-Host Agent in den Ressourcen aufgeführt, die in Kapitel [SAP-Ressourcen] [Bereitstellung Leitfaden 2.2] dieses Dokuments ein.

#### <a name="monitoring-check"></a>Kontrollkästchen für die Überwachung
Überprüfen Sie, ob die Überwachung funktioniert in Kapitel [überprüft und Problembehandlung bei End-to-End-Überwachung Setup für SAP auf Azure]beschriebenen[deployment-guide-troubleshooting-chapter].

### <a name="a9a60133-a763-4de8-8986-ac0fa33aa8c1"></a>Szenario 3: Verschieben eines virtuellen Computers aus lokalen mithilfe einer nicht GRG Azure-virtuellen mit SAP
Dieses Szenario wird die Groß-/Kleinschreibung von ein SAP-System einfach verschobene seine aktuelle Formular und Form aus lokalen in Azure adressieren. Bedeutet, dass keine Namen ändern möchten Windows oder Linux-Hostname und SAP-SID oder etwas stattfindet. In diesem Fall die virtuelle Festplatte nicht als Bild verwiesen wird, während der Bereitstellung aber direkt als der Datenträger OS verwendet wird. Im Hinblick auf die Bereitstellung unterscheidet sich in diesem Fall aus den ersten beiden Fällen dadurch, dass der virtuellen Computer-Agent automatisch während der Bereitstellung installiert werden kann. Daher der Azure-virtuellen Computer-Agent von Microsoft heruntergeladen werden muss und muss installiert und aktiviert innerhalb der virtuellen Computer manuell danach sein. Nachdem Sie diesen Vorgang erfolgreich verlaufen ist, können Sie weiterhin die SAP-Host Überwachung Azure-Erweiterung und seine Konfiguration einleiten. Überprüfen Sie in diesem Artikel, Details für die Funktion des Azure-virtuellen Computer Agents:

[comment]: <> (MSSedusch erledigen Update Windows verknüpfen unter) 

___

> ![Windows][Logo_Windows] Windows
>
> <http://Blogs.msdn.com/b/wats/Archive/2014/02/17/BGInfo-guest-Agent-Extension-for-Azure-VMs.aspx>
>
> ![Linux][Logo_Linux] Linux
>
> [Azure Linux Agent-Benutzerhandbuch][virtual-machines-linux-agent-user-guide]

___

Wie sieht der Workflow verschiedene Schritte aus:
 
![Flussdiagramm des Bereitstellung für einen Datenträger virtueller Computer mit SAP-Betriebssysteme][deployment-guide-figure-400]

Unter der Voraussetzung, dass der Datenträger ist bereits hochgeladen und Azure (Siehe [Planung und Implementierung Guide][planning-guide]), die folgenden Schritte definiert sein

#### <a name="create-virtual-machine"></a>Erstellen von virtuellen Computern
Verwenden Sie zum Erstellen einer-Bereitstellung mit einem privaten OS Datenträger über das Azure-Portal die SAP-Vorlage auf dem [Azure-Schnellstart-Vorlagen Github Repository]veröffentlicht[azure-quickstart-templates-github]. Sie können auch erstellen, einem virtuellen Computern mithilfe der [PowerShell oder Azure CLI manuell.

* [Konfigurationsvorlage für Ebene 2-(nur eine virtuellen Computern)][sap-templates-2-tier-os-disk]
    * Verwenden Sie diese Vorlage, wenn Sie ein Ebene 2-System, die mit nur einem virtuellen Computern erstellen möchten.

Nachdem Sie die oben genannte Vorlage geöffnet, navigiert Azure-Portal in den Bereich Parameter bearbeiten. Geben Sie die folgenden Informationen ein:

* **SapSystemId**: SAP-System-ID
* **OsType**: Betriebssystemtyp bereitstellen, Windows oder Linux werden soll.
* **SapSystemSize**: die Größe des SAP-System
    * Der Umfang der SAPS das neue System zu erhalten. Wenn Sie nicht sicher wie viele SAPS das System erforderlich sind sind, wenden Sie sich an Ihre SAP-Technologiepartner oder Systemintegrator
* **StorageType**: (nur Ebene 2 Vorlage) Typ Speicher, die verwendet werden soll 
    * Für Betriebssysteme vergrößern wird die Verwendung von Premium Speicher dringend empfohlen. Weitere Informationen zu den verschiedenen Speicher Datentypen finden Sie unter 
        * [Microsoft Azure-Speicher] [Dbms-Leitfaden-2.3], [Dbms-Leitfadens] [DBMS Handbuchs]
        * [Premium Speicher: Leistungsstarke Storage für Auslastung Azure-virtuellen Computern][storage-premium-storage-preview-portal]
        * [Einführung in Microsoft Azure-Speicher][storage-introduction]
* **OsDiskVhdUri**: URI des Betriebssystems als "Privat" Datenträger, z. B. https://`<accountname`>.blob.core.windows.net/vhds/osdisk.vhd
* **NewOrExistingSubnet**: bestimmt, ob ein neues virtuelles Netzwerk und Subnetz erstellt werden soll, oder ein bestehendes Subnetz verwendet werden soll. Wenn Sie bereits über ein virtuelles Netzwerk, das mit Ihrem lokalen Netzwerk verbunden ist verfügen, wählen Sie die vorhandenen.
* **SubnetId**: die ID des im Subnetz, dem die virtuellen Computer sollen verbunden sein. Wählen Sie aus dem Subnetz des VPN oder Express-Routing virtuellen Netzwerks in Verbindung mit Ihrem lokalen Netzwerk des virtuellen Computers. Die ID in der Regel sieht /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

Nachdem Sie alle Parameter eingegeben haben, wählen Sie das Abonnement und die Ressourcengruppe aus, die Sie verwenden möchten. Sie können entweder wählen Sie eine vorhandene Ressourcengruppe oder einen neuen erstellen, indem Sie auswählen "+ neue" in dem Dropdownmenü. Wenn Sie eine neue Ressourcengruppe erstellen, müssen Sie auch den Bereich auszuwählen, in dem die Ressourcengruppe und des virtuellen Computers erstellt werden.

Überprüfen Sie die Vertragsbedingungen, akzeptieren Sie, und klicken Sie auf erstellen.

#### <a name="install-vm-agent"></a>Installieren von virtuellen Computer-Agents
Der Linux-Agent muss bereits auf dem Datenträger OS installiert sein, wenn Sie die oben aufgeführten Vorlagen verwenden möchten. Andernfalls tritt ein Fehler die Bereitstellung. Herunterladen und Installieren des virtuellen Computer-Agents auf dem virtuellen Computer, wie in Kapitel beschrieben [herunterladen, installieren und Aktivieren von Azure-virtuellen Computer-Agent] [Bereitstellung-Leitfaden-4,4] dieses Dokuments.

Wenn Sie die oben angegebenen Vorlagen nicht verwenden, können Sie auch des virtuellen Computer-Agents später installieren.

#### <a name="join-domain-windows-only"></a>Teilnehmen an der Domäne (nur Windows)
In den Fall, dass die Bereitstellung in Azure, in der lokalen verbunden ist AD/DNS über Azure-Standorten oder Express-Routing (wird auch als Cross lokale in der [Planung und Implementierung Guide][planning-guide]), es wird davon ausgegangen, dass der virtuellen Computer eine lokale Domäne beitritt ist. Aspekte dieses Schritts sind in Kapitel [teilnehmen virtueller Computer in der lokalen Domäne (nur Windows)] [Bereitstellung Leitfaden 4.3] dieses Dokuments beschrieben.

#### <a name="configure-proxy-settings"></a>Konfigurieren von Proxyeinstellungen
Abhängig von Ihrer lokalen Netzwerkkonfiguration ist es möglicherweise erforderlich, um den Proxy auf Ihre virtuellen Computern konfigurieren, wenn sie mit Ihrem lokalen Netzwerk per VPN oder Express-Routing verbunden ist. Andernfalls des virtuellen Computers möglicherweise nicht zum Zugreifen auf das Internet und daher nicht die erforderlichen Erweiterungen herunterladen oder Überwachung Daten sammeln. Finden Sie in Kapitel [Proxy konfigurieren] [ deployment-guide-configure-proxy] dieses Dokuments.

#### <a name="configure-monitoring"></a>Konfigurieren der Überwachung
Konfigurieren von Azure erweiterte Überwachung Erweiterung für SAP beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung-Leitfaden-4.5] dieses Dokuments.

Überprüfen Sie die erforderlichen Komponenten für SAP-Überwachung für erforderlich mindestens Versionen von SAP-Kernel und SAP-Host Agent in den Ressourcen in Kapitel [SAP-Ressourcen] [Bereitstellung Leitfaden 2.2] dieses Dokuments aufgelistet.

#### <a name="monitoring-check"></a>Kontrollkästchen für die Überwachung
Überprüfen Sie, ob die Überwachung funktioniert in Kapitel [überprüft und Problembehandlung bei End-to-End-Überwachung Setup für SAP auf Azure]beschriebenen[deployment-guide-troubleshooting-chapter].

### <a name="scenario-4-updating-the-monitoring-configuration-for-sap"></a>Szenario 4: Aktualisieren der Konfigurations der überwachen für SAP
Es gibt Fälle, in dem Sie müssen die Konfiguration die Überwachung aktualisieren möchten:

* Das gemeinsame MS/SAP-Team erweitert die Überwachungsfunktionen und entschieden Indikatoren mehr hinzufügen oder Löschen von einigen Indikatoren. 
* Microsoft führt eine neue Version der zugrunde liegenden Azure Infrastruktur Bereitstellung der überwachen Daten, und die Azure erweiterte Überwachung Erweiterung für SAP wird diese Änderungen zur Anpassung.
* Hinzufügen von weiteren virtuellen Festplatten bereitgestellt werden, um Ihre Azure-virtuellen Computer oder eine virtuelle Festplatte zu entfernen. In diesem Fall müssen Sie zum Aktualisieren der Auflistung Speicher verknüpfte Daten. Wenn Sie Ihre Konfiguration ändern, indem hinzufügen oder Löschen von Endpunkten oder einen virtuellen IP-Adressen zuweisen, wirkt sich dies nicht auf die Konfiguration die Überwachung aus.
* Sie ändern die Größe Ihrer Azure-virtuellen Computer z. B. a5 auf eine beliebige andere Größe der virtuellen Computer.
* Sie hinzufügen Ihre Azure-virtuellen Computer neue Netzwerkschnittstellen

Um die Konfiguration der Überwachung aktualisieren möchten, gehen Sie wie folgt aus:

* Aktualisieren Sie die Überwachung Infrastruktur anhand der Schritte in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] Erläuterung [Bereitstellung-Leitfaden-4.5] dieses Dokuments. Erneutes Ausführen des Skripts in diesem Kapitel beschriebenen erkennt, dass die Konfiguration Überwachung bereitgestellt wird und die notwendigen Änderungen vor, um die Konfiguration der Überwachung wird ausgeführt. 

___

> ![Windows][Logo_Windows] Windows
>
> Für die Aktualisierung von der Azure-virtuellen Computer-Agent ist kein Eingriff erforderlich. Virtueller Computer Agent automatisch aktualisiert, dass Sie sich selbst und erfordert einen Neustart virtueller Computer keine.
>
> ![Linux][Logo_Linux] Linux
>
> Führen Sie die Schritte in [diesem Artikel] [ virtual-machines-linux-update-agent] Sie den Azure Linux-Agent aktualisieren. 

___

## <a name="detailed-single-deployment-steps"></a>Detaillierte Schritte für einzelne Bereitstellung

### <a name="604bcec2-8b6e-48d2-a944-61b0f5dee2f7"></a>Bereitstellen von Azure PowerShell-cmdlets
* Wechseln Sie zu <https://azure.microsoft.com/downloads/>
* Klicken Sie im Abschnitt ist 'line Tools einen Abschnitt "Windows PowerShell" bezeichnet. Folgen Sie den Link "Installieren".
* Microsoft Download Manager wird Popup mit Posten, die mit .exe ein. Wählen Sie die Option 'Ausführen'.
* Ein Popupfenster wird im Zusammenhang fragt, ob Microsoft Web Platform Installer ausgeführt. Drücken Sie "Ja"
* Ein Bildschirm wie dieses angezeigt wird:
 
![Bildschirm Azure PowerShell-Cmdlets für die Installation][deployment-guide-figure-500]
<a name="figure-5"></a>

* Drücken Sie installieren und anzunehmen Sie den Endbenutzer-Lizenzvertrag.

Aktivieren Sie häufig an, ob die PowerShell-Cmdlets aktualisiert wurden. In der Regel werden Updates auf einem monatlichen Zeitraum. Die einfachste Möglichkeit hierfür ist die Installation Schritte wie zuvor beschrieben, auf der Installationsbildschirm in [diesem] [ deployment-guide-figure-5] Abbildung. In diesem Bildschirm wird das Datum der Freigabe der Cmdlets sowie die Anzahl der eigentlichen Release angezeigt. Sofern nicht anders in SAP-Notizen [1928533] oder [2015553]angegeben wird, empfiehlt es sich für die Arbeit mit der neuesten Version von Azure PowerShell-Cmdlets.

Die aktuelle installierte Version der Azure-Cmdlets auf dem Desktop oder ein Notebook kann mit dem Befehl PS geprüft werden soll:

```powershell
Import-Module Azure
(Get-Module Azure).Version
```

Das Ergebnis dargestellt werden soll, wie unten dargestellt, in [diesem] [ deployment-guide-figure-6] Abbildung.

![Ergebnis von Azure PS Cmdlet Version überprüfen][deployment-guide-figure-600]
<a name="figure-6"></a>

Ist die Azure-Cmdlet-Version installiert haben, klicken Sie auf dem Desktop oder ein Notebook der aktuellen Zeile, erste sieht der Bildschirm nach dem Starten von Microsoft Web Plattform Installer weicht im Vergleich zu den abgebildeten in [dieser] [ deployment-guide-figure-5] Abbildung.

Bitte beachten Sie den roten Kreis unten in der [Abbildung] [ deployment-guide-figure-7] unter.
 
![Installationsbildschirm für Azure-PowerShell-Cmdlets, die angibt, dass die neueste Version von Azure PS Cmdlets installiert sind][deployment-guide-figure-700]
<a name="figure-7"></a>

Wenn der Bildschirm als [über]sieht aus[deployment-guide-figure-7], gibt an, dass die neueste Version von Azure-Cmdlet ist bereits installiert, es ist nicht erforderlich, um die Installation fortzusetzen. In diesem Fall können Sie 'die Installation zu diesem Zeitpunkt beenden'.

### <a name="1ded9453-1330-442a-86ea-e0fd8ae8cab3"></a>Bereitstellen von Azure CLI
* Wechseln Sie zu <https://azure.microsoft.com/downloads/>
* Klicken Sie im Abschnitt ist 'line Tools einen Abschnitt "Azure line Interface" bezeichnet. Führen Sie den Link "installieren" für Ihr Betriebssystem aus.

Aktivieren Sie häufig an, ob die CLI Azure aktualisiert wurden. In der Regel werden Updates auf einem monatlichen Zeitraum. Die einfachste Möglichkeit hierfür ist die Installation oben beschriebenen Schritte.

Die aktuelle installierte Version des Azure CLI auf dem Desktop oder ein Notebook kann mit dem Befehl geprüft werden soll:

```
azure --version
```

Das Ergebnis dargestellt werden soll, wie unten dargestellt, in [diesem] [ deployment-guide-figure-azure-cli-version] Abbildung.

![Ergebnis von Azure CLI Version überprüfen][deployment-guide-figure-760]
<a name="0ad010e6-f9b5-4c21-9c09-bb2e5efb3fda"></a>

### <a name="31d9ecd6-b136-4c73-b61e-da4a29bbc9cc"></a>Teilnehmen an virtuellen Computer in der lokalen Domäne (nur Windows)
In Fällen, wo Sie SAP-virtuellen Computern eines Kreuzes lokale Szenarios bereitstellen, in dem lokalen AD und DNS-Einträge in Azure erweiterten, es wird davon ausgegangen, dass die virtuellen Computern in einer lokalen Domäne verknüpft sind. Die detaillierten Schritte Verknüpfen eines virtuellen Computers von einer lokalen Domäne und zusätzliche Software erforderlich sein, dass ein Mitglied einer lokalen Domäne Kunden abhängige ist. In der Regel ein virtuellen Computers zu einer lokalen Domäne beitritt bedeutet zusätzliche Software wie Schadsoftware Schutz Software oder verschiedenen Akteuren der Sicherungsdatei oder Überwachung Software installieren.

Darüber hinaus müssen Sie für Fälle sicherzustellen, in dem Internet Proxyeinstellungen erzwungenen beitreten zu einer Domäne, die lokale Windows System Account(S-1-5-18) auf dem Gast virtuellen Computer diese Einstellungen auch verfügt. Einfachste besteht darin, den Proxy mit Domäne Gruppenrichtlinien das Anwenden auf Systeme innerhalb der Domäne zu erzwingen.

### <a name="c7cbb0dc-52a4-49db-8e03-83e7edc2927d"></a>Herunterladen, installieren und Aktivieren von Azure-virtuellen Computer-Agents
Die folgenden Schritte sind erforderlich, wenn ein virtueller Computer für SAP aus einer OS Bilder bereitgestellt wird, der nicht z. B. nicht Syspreped für Windows GRG. Es ist nicht erforderlich sind, um die Installation des Agent für virtuellen Computern aus dem Azure Marketplace bereitgestellt. Diese Bilder enthalten bereits Azure-Agents aus.

#### <a name="b2db5c9a-a076-42c6-9835-16945868e866"></a>Windows

* Herunterladen des Agents Azure-virtuellen Computer an:
    * Herunterladen das Azure-virtuellen Computer-Agent Installer-Paket aus: <https://go.microsoft.com/fwlink/?LinkId=394789>
    * Lokal speichern Sie virtueller Computer Agent MSI-Paket auf dem Laptop oder einem server
* Installieren des Agents Azure-virtuellen Computer an:
    * Verbinden Sie mit dem bereitgestellten Azure virtuellen Computer mit dem Terminal Services (RDP)
    * Öffnen Sie ein Windows Explorer-Fenster des virtuellen Computers und ein Zielverzeichnis für die MSI-Datei des virtuellen Computer-Agents
    * Drag & drop Azure virtueller Computer Agent Installer MSI-Datei von Ihrem lokalen Laptop-Server in das Zielverzeichnis des virtuellen Computer-Agents auf dem virtuellen Computer
    * Durch Doppelklicken Sie auf die MSI-Datei auf dem virtuellen Computer
    * Für lokale Domänen virtueller Computer Mitglied, stellen Sie sicher, dass der tatsächliche Internet Proxyeinstellungen für das Windows Systemkonto (S-1-5-18) anwenden, auf dem virtuellen Computer als auch in Kapitel [Proxy konfigurieren]beschrieben[deployment-guide-configure-proxy]. Virtueller Computer-Agent wird in diesem Zusammenhang ausgeführt und Verbindung zu Azure hergestellt werden muss.

#### <a name="6889ff12-eaaf-4f3c-97e1-7c9edc7f7542"></a>Linux
Installieren Sie die virtuellen Computer-Agent für Linux mit dem folgenden Befehl

- **SLES**

```
sudo zypper install WALinuxAgent
```
- **RHEL**

```
sudo yum install WALinuxAgent
```

### <a name="baccae00-6f79-4307-ade4-40292ce4e02d"></a>Konfigurieren von Proxy
Die Schritte zum Konfigurieren des Proxys unterschiedlich Windows und Linux.

#### <a name="windows"></a>Windows
Diese Einstellungen müssen auch für das lokale Systemkonto Zugriff auf das Internet gültig sein. Wenn Ihre Proxyeinstellungen nicht durch Gruppenrichtlinien festgelegt werden, können Sie diese konfigurieren, für das lokale Systemkonto gehen Sie folgendermaßen vor, um ihn zu konfigurieren.

1.  Öffnen Sie gpedit.msc
1.  Navigieren Sie zur Konfiguration des Computers hat Administrative Vorlagen -> Windows-Komponenten -> Internet Explorer, und Aktivieren von "sind Proxy Einstellungen pro Computer (statt pro Benutzer)
1.  Öffnen Sie die Systemsteuerung, und navigieren Sie zu Netzwerk und Internet -> Internetoptionen
1.  Öffnen Sie die Registerkarte Verbindungen, und klicken Sie auf LAN-Einstellungen
1.  Deaktivieren von "Automatisch erkennen, Einstellungen"
1.  Aktivieren Sie "Einen Proxyserver für LAN verwenden", und geben Sie die Proxy-Host und den port

#### <a name="linux"></a>Linux
Konfigurieren Sie den richtigen Proxy in der Konfigurationsdatei des Microsoft Azure Gast-Agents, befindet sich am /etc/waagent.conf. Die folgenden Parameter müssen festgelegt werden:

```
HttpProxy.Host=<proxy host e.g. proxy.corp.local>
HttpProxy.Port=<port of the proxy host e.g. 80>
```

Nachdem Sie die Konfiguration mit geändert haben, starten Sie den agent

```
sudo service waagent restart
```

Die Proxyeinstellungen in /etc/waagent.conf gelten auch für die erforderlichen virtuellen Computer Extensions. Wenn Sie den Azure Repositorys verwenden möchten, stellen Sie sicher, dass der Datenverkehr an den folgenden Repositorys im lokalen Intranet nicht durchgelassen wird. Wenn Sie Benutzer definiert leitet Erzwungene Tunnel aktivieren, vergewissern Sie sich zum Hinzufügen einer Routing erstellt weitergeleitet, die Datenverkehr an den Repositorys direkt mit dem Internet und nicht über die Verbindung zwischen Standorten.

- **SLES** Sie müssen außerdem leitet für die IP-Adressen /etc/regionserverclnt.cfg hinzufügen. Ein Beispiel ist in den folgenden Screenshot dargestellt. 

- **RHEL** Sie müssen außerdem leitet für die IP-Adressen der Hosts der /etc/yum.repos.d/rhui-load-balancers hinzufügen. Ein Beispiel ist in den folgenden Screenshot dargestellt.

Weitere Details zu Benutzer definiert ist, finden Sie [in diesem Artikel][virtual-networks-udr-overview].

![Erzwungene Tunnel][deployment-guide-figure-50]

### <a name="d98edcd3-f2a1-49f7-b26a-07448ceb60ca"></a>Konfigurieren von Azure erweiterte Überwachung Erweiterung für SAP
Nachdem Sie der virtuellen Computer vorbereitet ist, wie in Kapitel [Bereitstellung Szenarien von virtuellen Computern für SAP auf Microsoft Azure] beschrieben [Bereitstellung-Leitfaden-3] der Azure-virtuellen Computer-Agent auf dem Computer installiert ist. Wichtige gemeldet werden Azure erweiterte Überwachung Bereitstellen der Erweiterung für SAP, die im Repository Azure Erweiterung in die globalen Rechenzentren von Microsoft Azure zur Verfügung steht. Weitere Informationen hierzu überprüfen Sie den [Planung und Implementierung Leitfaden] [planning-Leitfaden-9.1]. 

Sie können Azure PowerShell oder Azure CLI installieren und Konfigurieren der Azure erweiterte Überwachung Erweiterung für SAP. Lesen Sie Kapitel [Azure PowerShell] [Bereitstellung-Leitfaden-4.5.1], wenn Sie die Erweiterung auf einem Windows oder Linux VM mit einem Windows-Computer installieren möchten. Installieren die Erweiterung auf einer Linux VM mithilfe einer Linux finden Desktop Kapitel [Azure CLI] [Bereitstellung Leitfaden 4.5.2].

#### <a name="987cf279-d713-4b4c-8143-6b11589bb9d4"></a>Azure PowerShell für Linux und Windows-virtuellen Computern
Um den Vorgang der Installation der Azure erweiterte Überwachung Erweiterung für SAP ausführen zu können, führen Sie die folgenden Schritte aus:

* Stellen Sie sicher, dass Sie die neueste Version von Microsoft Azure PowerShell-Cmdlet installiert haben. Finden Sie unter Kapitel [Bereitstellen von Azure PowerShell-Cmdlets] [Bereitstellung-Leitfaden-4.1] dieses Dokuments.  
* Führen Sie das folgende PowerShell-Cmdlet ein. Führen Sie eine Liste der verfügbaren Umgebungen Cmdlet Get-AzureRmEnvironment aus. Wenn Sie eine öffentliche Azure verwenden möchten, ist Ihre Umgebung AzureCloud aus. Wählen Sie für Azure in China AzureChinaCloud ein.

```powershell
    $env = Get-AzureRmEnvironment -Name <name of the environment>
    Login-AzureRmAccount -Environment $env
    Set-AzureRmContext -SubscriptionName <subscription name>
    
    Set-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
```

Nachdem Sie Ihre Kontodaten und der Azure-virtuellen Computern bereitgestellt, wird das Skript die erforderlichen Erweiterungen bereitstellen und aktivieren die erforderlichen Features. Dies kann einige Minuten dauern.
Lesen Sie [diese MSDN-Artikel] [ msdn-set-azurermvmaemextension] Weitere Informationen zu den Set-AzureRmVMAEMExtension.
  
![Ergebnisbildschirm der erfolgreichen Ausführung der SAP-Cmdlet für bestimmte Azure festlegen – AzureRmVMAEMExtension][deployment-guide-figure-900]

Eine erfolgreiche Ausführung des Set-AzureRmVMAEMExtension werden alle die notwendigen Schritte zum Konfigurieren des Hosts Überwachung der Funktionen für SAP ausführen. 

Die Ausgabe, die das Skript übermitteln soll sieht wie folgt aus:

* Bestätigungsdialogfeld, die die Konfiguration die Überwachung für die Basis virtuelle Festplatte (mit dem OS) sowie alle zusätzlichen virtuellen Festplatten in den virtuellen Computer bereitgestellt wurde konfiguriert.
* Die beiden nächsten Nachrichten sind die Konfiguration von Speicher Kennzahlen für einen bestimmten Speicherkonto bestätigt. 
* Um eine Zeile der Ausgabe kann einen Status auf die tatsächliche Aktualisierung der Konfiguration der Überwachung erzielt werden.
* Ein anderes angezeigt wird bestätigt, dass die Konfiguration bereitgestellt oder aktualisiert wurde.
* Die letzte Zeile der Ausgabe ist die Möglichkeit haben, testen Sie die Konfiguration die Überwachung mit informativen.
* Um zu überprüfen, dass alle Schritte der Azure erweiterte Überwachung erfolgreich ausgeführt wurden und Azure-Infrastruktur die notwendigen Daten enthält, Fortsetzen das Kontrollkästchen Readiness Azure erweiterte Überwachung Erweiterung für SAP, wie beschrieben in Kapitel [Readiness überprüfen Azure erweiterte Überwachung für SAP] [Bereitstellung-Leitfaden-5.1] in diesem Dokument. 
* Wenn Sie weiterhin auf diese Weise, warten Sie 15 und 30 Minuten, bis die Azure-Diagnose die relevanten Daten gesammelt haben, wird aus.

#### <a name="408f3779-f422-4413-82f8-c57a23b4fc2f"></a>Azure CLI für Linux virtuellen Computern

Um den Vorgang der Installation der Azure erweiterte Überwachung Erweiterung für SAP mit Azure CLI ausführen zu können, führen Sie die folgenden Schritte aus:

1. Installieren von Azure CLI in [dieser] beschriebenen[ azure-cli] Artikel
1. Melden Sie sich mit Ihrem Azure-Konto

    ```
    azure login
    ```
1. Wechseln Sie zur Azure Ressourcenmanager Modus

    ```
    azure config mode arm
    ```
1. Azure erweiterte Überwachung aktivieren

    ```
    azure vm enable-aem <resource-group-name> <vm-name>
    ```  
1. Stellen Sie sicher, dass die Azure erweiterte Überwachung des virtuellen Computers Azure-Linux aktiv ist. Überprüfen Sie, ob die Datei /var/lib/AzureEnhancedMonitor/PerfCounters vorhanden ist. Wenn vorhanden ist, handelt es sich bei erfassten Anzeigeinformationen werden durch AEM mit:

    ```
    cat /var/lib/AzureEnhancedMonitor/PerfCounters
    ```
    Klicken Sie dann erhalten Sie, wie die Ausgabe:
    
    ```
    2;cpu;Current Hw Frequency;;0;2194.659;MHz;60;1444036656;saplnxmon;
    2;cpu;Max Hw Frequency;;0;2194.659;MHz;0;1444036656;saplnxmon;
    …
    …
    ```

## <a name="564adb4f-5c95-4041-9616-6635e83a810b"></a>Überprüft und Problembehandlung bei End-to-End-Überwachung Setup für SAP auf Azure
Nachdem Sie Ihre Azure-virtuellen Computer bereitgestellt und die relevanten Azure Überwachung Infrastruktur eingerichtet haben, überprüfen Sie, ob alle Komponenten der Azure erweiterte Überwachung gemischte so arbeiten. 

Das Kontrollkästchen Readiness für die Azure erweiterte Überwachung Erweiterung für SAP deshalb ausgeführt werden, wie in Kapitel [Readiness überprüfen Azure erweiterte Überwachung für SAP] beschrieben [Bereitstellung Leitfaden 5.1]. Wenn das Ergebnis dieser Prüfung positiv ist und Sie alle entsprechenden Leistungsindikatoren erhalten, wurde die Azure Überwachung erfolgreich eingerichtet. In diesem Fall fahren Sie mit der Installation von SAP-Host Agent wie in den SAP-Notizen aufgeführt, die in Kapitel [SAP-Ressourcen] [Bereitstellung Leitfaden 2.2] dieses Dokuments beschrieben. Wenn das Ergebnis der Prüfung Readiness fehlende Indikatoren zeigt an, fahren Sie die integritätsprüfung für die Überwachung Azure-Infrastruktur ausführen, wie in Kapitel [integritätsprüfung für Azure Überwachung Infrastruktur Konfiguration] beschrieben [Bereitstellung Leitfaden 5.2]. Aktivieren Sie im Fall ein Problem mit der Azure-Konfiguration für die Überwachung, Kapitel [Weitere Maßnahmen zur Problembehandlung für die Überwachung Azure-Infrastruktur für SAP] [Bereitstellung-Leitfaden-5.3] für weitere Hilfe zu behandeln.

### <a name="bb61ce92-8c5c-461f-8c53-39f5e5ed91f2"></a>Readiness Azure erweiterte Überwachung für SAP prüfen
Mit dieser Prüfung stellen Sie sicher, dass der Metrik der innerhalb Ihrer SAP-Anwendung angezeigt werden, die von der zugrunde liegenden Azure Überwachung Infrastruktur vollständig bereitgestellt werden. 

#### <a name="execute-the-readiness-check-on-a-windows-vm"></a>Führen Sie das Kontrollkästchen Readiness auf einen Windows-virtuellen
Um das Kontrollkästchen Readiness, melden Sie sich an den Azure virtuellen Computern (Admin-Konto ist nicht erforderlich) ausführen, und führen Sie die folgenden Schritte aus:

* Öffnen Sie ein Windows-Eingabeaufforderungsfenster, und wechseln Sie zum Installationsordner der Azure Überwachung Erweiterung für SAP-C:\Packages\Plugins\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\`<version`> \drop

Das Version-Webpart in den Pfad für die Überwachung Erweiterung oben bereitgestellten kann variieren. Wenn Sie mehrere Ordner der Überwachung Erweiterungsversion im Installationsordner angezeigt wird, überprüfen Sie die Konfiguration des Windows-Diensts 'AzureEnhancedMonitoring', und wechseln Sie zu dem Ordner, der als "Pfad zur ausführbare" angegeben.
 
![Eigenschaften des die Azure erweiterte Überwachung Erweiterung für SAP-Dienstes][deployment-guide-figure-1000]

* Führen Sie im Befehlsfenster ohne Parameter azperflib.exe ein.

> [AZURE.NOTE] Die azperflib.exe in einer Schleife ausgeführt wird und die zusammengestellten Indikatoren so aktualisiert, dass alle 60 Sekunden. Schließen Sie das Befehlsfenster die Schleife fertig sind,

Wenn die Azure erweiterte Überwachung Erweiterung nicht installiert ist oder der Dienst 'AzureEnhancedMonitoring' nicht ausgeführt wird, wurde die Erweiterung nicht ordnungsgemäß konfiguriert. Führen Sie in diesem Fall Kapitel [Weitere Maßnahmen zur Problembehandlung für die Überwachung Azure-Infrastruktur für SAP] [Bereitstellung-Leitfaden-5.3] ausführliche Anweisungen wie die Erweiterung erneut bereitgestellt.

##### <a name="check-the-output-of-azperflibexe"></a>Überprüfen Sie die Ausgabe der azperflib.exe
Die Ausgabe der azperflib.exe zeigt, dass alle Azure-Datenquellen für SAP aufgefüllt. Am Ende der Liste der zusammengestellten Indikatoren finden Sie eine Zusammenfassung und ein Dienststatus-Indikator, der den Status der Azure Überwachung festlegt. 
 
![Die Ausgabe der integritätsprüfung durch Ausführen der azperflib.exe gibt an, dass keine Probleme vorliegen][deployment-guide-figure-1100]
<a name="figure-11"></a>

Aktivieren Sie das Ergebnis zurückgegeben, die für die Ausgabe von den Gesamtbetrag der' Indikatoren', welche werden als leer und für die integritätsprüfung gemeldet wie oben in der Abbildung [oben]gezeigt[deployment-guide-figure-11].

Sie können die Ergebniswerte wie folgt interpretieren:

| Azperflib.exe Ergebniswerte | Azure Readiness Status für die Überwachung |
| ------------------------------|----------------------------------- |
| **Indikatoren Summe: leeren** | Die folgenden 2 Azure-Speicher Indikatoren können leer sein: <ul><li>Speicher lesen lokal Wartezeit Server (ms)</li><li>Speicher lesen lokal Wartezeit E2E (ms)</li></ul>Alle anderen Indikatoren müssen Werte enthalten. |
| **Integritätsprüfung** | Nur angezeigt wird, ist der Rückgabetyp OK Status OK |

Wenn nicht beide Werte azperflib.exe zeigen an, dass alle eingetragenen Indikatoren richtig zurückgegeben werden, folgen Sie den Anweisungen für die integritätsprüfung für die Überwachung Infrastruktur Konfiguration von Azure beschriebenen in Kapitel [integritätsprüfung für Azure Überwachung Infrastruktur Konfiguration] [Bereitstellung-Leitfaden-5.2] unter.

#### <a name="execute-the-readiness-check-on-a-linux-vm"></a>Führen Sie das Kontrollkästchen Readiness auf einer Linux VM
Um das Kontrollkästchen Readiness ausführen zu können, Verbinden mit SSH zu der Azure-virtuellen Computern, und führen Sie folgende Schritte aus:

* Überprüfen Sie die Ausgabe der Azure erweiterte Überwachung Erweiterung
    * Weitere /var/lib/AzureEnhancedMonitor/PerfCounters
        * Erhalten Sie eine Liste der Datenquellen. Die Datei darf nicht leer sein.
    * Katze /var/lib/AzureEnhancedMonitor/PerfCounters | Grep zurück
        * Sollte zurückgeben, um eine Zeile, in dem der Fehler keine z. B. 3 ist; Config; Fehler beim; 0; 0; **keine**; 0; 1456416792; Tst-Servercs;
    * Weitere /var/lib/AzureEnhancedMonitor/LatestErrorRecord
        * Sollte leer sein oder sollte nicht vorhanden
* Wenn das erste Kontrollkästchen oben nicht erfolgreich war, führen Sie diese zusätzlichen Tests durch:
    * Stellen Sie sicher, dass die Waagent installiert und gestartet ist
        * Sudo ls-al/Var/lib/Waagent /
            * den Inhalt des Verzeichnisses Waagent sollte aufgelistet werden.
        * PS-Ax | Grep waagent
            * sollte einen Eintrag ähnlich wie anzeigen ' Python /usr/sbin/waagent-Daemon'
    * Stellen Sie sicher, dass die Erweiterung Linux Diagnostic installiert und gestartet ist
        * Sudo sh - C ' ls-al /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-*'
            * den Inhalt des Verzeichnisses Linux Diagnostic Erweiterung sollte aufgelistet werden.
        * PS-Ax | Grep-Diagnose
            * sollte einen Eintrag ähnlich wie anzeigen ' Python /var/lib/waagent/Microsoft.OSTCExtensions.LinuxDiagnostic-2.0.92/diagnostic.py-Daemon'
    * Stellen Sie sicher, dass die Azure erweiterte Überwachung Erweiterung installiert und gestartet ist
        * Sudo sh - C ' ls-al /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-*/'
            * den Inhalt des Verzeichnisses Azure erweiterte Überwachung Erweiterung sollte aufgelistet werden.
        * PS-Ax | Grep AzureEnhanced
            * sollte einen Eintrag ähnlich wie 'Python /var/lib/waagent/Microsoft.OSTCExtensions.AzureEnhancedMonitorForLinux-2.0.0.2/handler.py Daemon' anzeigen
* Installieren der SAP-Server-Agent, wie im SAP-Hinweis [1031096] beschrieben, und aktivieren Sie die Ausgabe saposcol
    * Ausführen von /usr/sap/hostctrl/exe/saposcol -d
    * Abbild Ccm ausführen
    * Überprüfen Sie, ob die Metrik "Virtualization_Configuration\Enhanced Überwachung Zugriff" wahr ist
* Wenn Sie bereits eine SAP NetWeaver ABAP Anwendungsserver installiert haben, öffnen Sie Transaktion ST06 und Kontrollkästchen, wenn die erweiterte Überwachung aktiviert ist.

Wenn keines der Prüfungen über Fail, führen Sie die Kapitel [Weitere Maßnahmen zur Problembehandlung für die Überwachung Azure-Infrastruktur für SAP] [Bereitstellung-Leitfaden-5.3] ausführliche Anweisungen wie die Erweiterung erneut bereitgestellt.

### <a name="e2d592ff-b4ea-4a53-a91a-e5521edb6cd1"></a>Integritätsprüfung für Azure Überwachung Infrastruktur Konfiguration
Wenn einige der Überwachung Daten werden nicht ordnungsgemäß zugestellt werden durch den Test in Kapitel [Readiness überprüfen Azure erweiterte Überwachung für SAP] beschriebenen [Bereitstellung Leitfaden 5.1] höher, führen Sie das Cmdlet Test-AzureRmVMAEMExtension zu testen, ob die aktuelle Konfiguration der Infrastruktur Azure für die Überwachung und die Überwachung Erweiterung für SAP korrekt ist.

Um festzustellen, ob die Konfiguration die Überwachung, führen Sie bitte die folgende Schritte aus:

* Stellen Sie sicher, dass Sie die neueste Version von Microsoft Azure PowerShell-Cmdlet installiert haben, wie unter Kapitel [Bereitstellen von Azure PowerShell-Cmdlets] [Bereitstellung-Leitfaden-4.1] dieses Dokuments.
* Führen Sie das folgende PowerShell-Cmdlet ein. Führen Sie eine Liste der verfügbaren Umgebungen Cmdlet Get-AzureRmEnvironment aus. Wenn Sie eine öffentliche Azure verwenden möchten, ist Ihre Umgebung AzureCloud aus. Wählen Sie für Azure in China AzureChinaCloud ein.

```powershell
$env = Get-AzureRmEnvironment -Name <name of the environment>
Login-AzureRmAccount -Environment $env
Set-AzureRmContext -SubscriptionName <subscription name>
Test-AzureRmVMAEMExtension -ResourceGroupName <resource group name> -VMName <virtual machine name>
```

* Nachdem Sie Ihre Kontodaten und der Azure-virtuellen Computern angegeben haben, wird das Skript die Konfiguration des virtuellen Computers testen ausgewählt haben.

 
![Festlegen des SAP-Cmdlets für bestimmte Azure Test-VMConfigForSAP_GUI][deployment-guide-figure-1200]

Nachdem Sie die Informationen zu Ihrem Konto und der Azure-virtuellen Computern eingegeben haben, wird das Skript die Konfiguration des virtuellen Computers testen ausgewählt haben.
 
![Die Ausgabe der erfolgreichen Test Azure Überwachung Infrastruktur für SAP][deployment-guide-figure-1300]

Stellen Sie sicher, dass jeder Kontrollkästchen mit OK gekennzeichnet ist. Wenn einige der Prüfungen nicht ok sind, führen Sie das Cmdlet Update beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung-Leitfaden-4.5] dieses Dokuments. Warten Sie ein anderes 15 Minuten, und die überprüfen in Kapitel [Readiness überprüfen Azure erweiterte Überwachung für SAP] beschriebenen [Bereitstellung Leitfaden 5.1] und [integritätsprüfung für Azure Überwachung Infrastruktur Konfiguration] [Bereitstellung-Leitfaden-5.2] erneut. Wenn die Prüfungen weiterhin ein Problem mit einigen oder allen Indikatoren angeben, fahren Sie mit Kapitel [Weitere Maßnahmen zur Problembehandlung für die Überwachung Azure-Infrastruktur für SAP] [Bereitstellung Guide 5.3].

### <a name="fe25a7da-4e4e-4388-8907-8abc2d33cfd8"></a>Weitere Maßnahmen zur Problembehandlung für die Überwachung Azure-Infrastruktur für SAP

#### <a name="windowslogowindows-azure-performance-counters-do-not-show-up-at-all"></a>![Windows][Logo_Windows] Azure-Datenquellen anzeigen gar nicht nach oben
Die Sammlung von Performance-Werte auf Azure erfolgt durch den Windows-Dienst 'AzureEnhancedMonitoring'. Wenn der Dienst nicht richtig installiert wurde oder sie nicht in Ihrer virtuellen Computer ausgeführt wird, kann gar keine Performance-Werte erfasst werden.

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a>Das Installationsverzeichnis der Erweiterung Azure erweiterte Überwachung ist leer. 

###### <a name="issue"></a>Problem
Das Installationsverzeichnis C:\Packages\Plugins\Microsoft.AzureCAT.AzureEnhancedMonitoring.AzureCATExtensionHandler\\`<version`> \drop leer ist.

###### <a name="solution"></a>Lösung
Die Erweiterung ist nicht installiert. Überprüfen Sie, ob es sich um ein Problem Proxy (wie vor beschrieben) ist. Möglicherweise müssen Sie den Computer neu starten und/oder führen Sie das Skript Skript festlegen-AzureRmVMAEMExtension erneut aus.

##### <a name="service-for-azure-enhanced-monitoring-does-not-exist"></a>Dienst für erweiterte Azure Überwachung ist nicht vorhanden 

###### <a name="issue"></a>Problem
Windows-Dienst 'AzureEnhancedMonitoring' ist nicht vorhanden. Azperflib.exe: Löst das Ergebnis azperlib.exe einen Fehler an, wie in der [folgenden Abbildung]gezeigt[deployment-guide-figure-14].
 
![Ausführung des azperflib.exe zeigt an, dass der Dienst der Azure erweiterte Überwachung Erweiterung für SAP nicht ausgeführt wird][deployment-guide-figure-1400]
<a name="figure-14"></a>

###### <a name="solution"></a>Lösung
Wenn der Dienst nicht vorhanden ist, wie in der [Abbildung oben][deployment-guide-figure-14], Azure Überwachung Erweiterung für SAP wurde nicht richtig installiert. Erneut bereitstellen, die Erweiterung entsprechend den zuvor beschriebenen Schritte für Ihre Bereitstellungsszenario in Kapitel [Bereitstellung Szenarien von virtuellen Computern für SAP auf Microsoft Azure] [Bereitstellung Leitfaden 3]. 

Nach der Bereitstellung der Erweiterung erneut zu überprüfen, ob die Azure Leistungsindikatoren nach 1 Stunde in den Azure-virtuellen Computer bereitgestellt werden.

##### <a name="service-for-azure-enhanced-monitoring-exists-but-fails-to-start"></a>Dienst für erweiterte Azure Überwachung vorhanden ist, aber nicht gestartet werden 

###### <a name="issue"></a>Problem
Windows-Dienst 'AzureEnhancedMonitoring' vorhanden und aktiviert ist, aber kann nicht gestartet werden. Überprüfen des Anwendung Ereignisprotokolls für Weitere Informationen.

###### <a name="solution"></a>Lösung
Fehlerhafte Konfiguration. Erneutes Aktivieren die Überwachung Erweiterung für den virtuellen Computer beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung Leitfaden 4.5].

#### <a name="windowslogowindows-some-azure-performance-counters-are-missing"></a>![Windows][Logo_Windows] Einige Azure-Datenquellen fehlen
Die Sammlung von Performance-Werte auf Azure erfolgt durch den Windows-Dienst 'AzureEnhancedMonitoring', die Daten aus verschiedenen Quellen abruft. Einige Konfigurationsdaten lokal erfasst werden, Performance-Werte werden aus Azure-Diagnose gelesen und Speicher Indikatoren aus der Protokollierung auf Abonnement Speichergrenze verwendet werden.

Behandlung von Problemen mit SAP-Notiz haben [1999351] nicht zum Führen des Skripts festlegen-AzureRmVMAEMExtension erneut. Möglicherweise müssen Sie für eine Stunde warten, da Speicher Analytics oder Diagnose Indikatoren möglicherweise nicht erstellt werden, sobald diese Funktionen aktiviert sind. Wenn das Problem weiterhin besteht, öffnen Sie eine Nachricht SAP-Kunden Unterstützung der Komponente BC-lokal-NT-AZR aus.

#### <a name="linuxlogolinux-azure-performance-counters-do-not-show-up-at-all"></a>![Linux][Logo_Linux] Azure-Datenquellen anzeigen gar nicht nach oben

Die Sammlung von Performance-Werte auf Azure erfolgt durch eine Daemon. Wenn der Daemon nicht ausgeführt wird, kann gar keine Performance-Werte erfasst werden.

##### <a name="the-installation-directory-of-the-azure-enhanced-monitoring-extension-is-empty"></a>Das Installationsverzeichnis der Erweiterung Azure erweiterte Überwachung ist leer. 

###### <a name="issue"></a>Problem
Das Verzeichnis/Var/Bibliothek/Waagent/enthält keine WindowSWF für die Erweiterung Azure erweiterte Überwachung.

###### <a name="solution"></a>Lösung
Die Erweiterung ist nicht installiert. Überprüfen Sie, ob es sich um ein Problem Proxy (wie vor beschrieben) ist. Möglicherweise müssen Sie den Computer neu starten und/oder führen Sie das Skript festlegen-AzureRmVMAEMExtension erneut aus.

#### <a name="linuxlogolinux-some-azure-performance-counters-are-missing"></a>![Linux][Logo_Linux] Einige Azure-Datenquellen fehlen

Die Sammlung von Performance-Werte auf Azure erfolgt Daemon, indem Sie die Daten aus verschiedenen Quellen abruft. Einige Konfigurationsdaten lokal erfasst werden, Performance-Werte werden aus Azure-Diagnose gelesen und Speicher Indikatoren aus der Protokollierung auf Abonnement Speichergrenze verwendet werden.

Eine vollständige und auf dem neuesten Stand Liste der bekannten Probleme finden Sie in SAP-Hinweis [1999351] , enthält weitere Informationen zur Problembehandlung für die erweiterte Azure Überwachung für SAP.

Behandlung von Problemen mit SAP-Hinweis [1999351] nicht unterstützen, führen Sie erneut das Skript festlegen – AzureRmVMAEMExtension beschriebenen in Kapitel [konfigurieren Azure erweiterte Überwachung Erweiterung für SAP] [Bereitstellung Leitfaden 4.5]. Möglicherweise müssen Sie für eine Stunde warten, da Speicher Analytics oder Diagnose Indikatoren möglicherweise nicht erstellt werden, sobald diese Funktionen aktiviert sind. Wenn das Problem weiterhin besteht, öffnen Sie eine Nachricht SAP-Kunden Support, klicken Sie auf die Komponente BC-lokal-NT-AZR für Windows oder BC-lokal-LNX-AZR für eine Linux virtuellen Computern aus.
