<properties
    pageTitle="Geplante Wartung für Linux virtuellen Computern | Microsoft Azure"
    description="Verstehen Sie, welche Azure geplanten Wartung ist und wie sie Ihre Linux virtuellen Computern in Azure auswirkt"
    services="virtual-machines-linux"
    documentationCenter=""
    authors="drewm"
    manager="timlt"
    editor=""
    tags="azure-service-management,azure-resource-manager"/>

<tags
    ms.service="virtual-machines-linux"
    ms.workload="infrastructure-services"
    ms.tgt_pltfrm="vm-linux"
    ms.devlang="na"
    ms.topic="article"
    ms.date="04/26/2016"
    ms.author="drewm"/>

# <a name="planned-maintenance-for-linux-virtual-machines-in-azure"></a>Geplante Wartung für in Azure-virtuellen Computern Linux

Verstehen Sie, welche Azure geplanten Wartung ist und wie sie die Verfügbarkeit von Ihrem Linux virtuellen Computern beeinflussen kann. In diesem Artikel wird auch für [Windows-virtuellen Computern](virtual-machines-windows-planned-maintenance.md)verfügbar. 

Dieser Artikel bietet einen Hintergrund unter ', um den Prozess Azure geplanten Wartung. Wenn Sie Ihre virtuellen Computer neu gestartet Problembehandlung möchte, können Sie [diesen Blog lesen Beitrag mit detaillierten Informationen zu Anzeigen virtueller Computer Protokolle neu zu starten](https://azure.microsoft.com/blog/viewing-vm-reboot-logs/).

[AZURE.INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="why-azure-performs-planned-maintenance"></a>Warum Azure führt geplante Wartung

Microsoft Azure führt regelmäßig Updates des Globus zur Verbesserung der Zuverlässigkeit, Leistung und Sicherheit der Hostinfrastruktur, die virtuellen Computern zugrunde liegt. Viele dieser Updates werden ohne Einfluss zur Cloud Services, einschließlich Updates Arbeitsspeicher beibehalten oder virtuellen Computern ausgeführt werden.

Allerdings benötigen einige Updates einen Neustart Ihren virtuellen Computern die erforderlichen Updates für die Infrastruktur anwenden. Den virtuellen Computern sind fahren Sie während wir die Infrastruktur patch und dann die virtuellen Computer neu gestartet.

Bitte beachten Sie, dass es gibt zwei Arten von Wartung, die die Verfügbarkeit von Ihren virtuellen Computern auswirken können: geplanten und ungeplanten. Diese Seite beschreibt, wie Microsoft Azure geplanten Wartung ausführt. Weitere Informationen zu nicht geplante Wartung finden Sie unter [Arbeiten im Vergleich zu nicht geplante Wartung geplant](virtual-machines-linux-manage-availability.md).

[AZURE.INCLUDE [virtual-machines-common-planned-maintenance](../../includes/virtual-machines-common-planned-maintenance.md)]
