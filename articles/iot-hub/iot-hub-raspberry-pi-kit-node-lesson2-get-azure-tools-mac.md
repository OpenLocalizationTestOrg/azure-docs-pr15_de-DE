<properties
 pageTitle="Abrufen von Azure-Tools (Mac OS 10.10) | Microsoft Azure"
 description="Installieren Sie auf dem Mac OS Python und Azure Line Interface (CLI Azure) ein."
 services="iot-hub"
 documentationCenter=""
 authors="shizn"
 manager="timlt"
 tags=""
 keywords=""/>

<tags
 ms.service="iot-hub"
 ms.devlang="multiple"
 ms.topic="article"
 ms.tgt_pltfrm="na"
 ms.workload="na"
 ms.date="10/21/2016"
 ms.author="xshi"/>

# <a name="21-get-azure-tools-macos-1010"></a>2.1 erste Azure-Tools (Mac OS 10.10)

> [AZURE.SELECTOR]
- [Windows 7 +](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
- [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
- [Mac OS 10.10.](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="211-what-you-will-do"></a>2.1.1 mögliche Aktionen werden

Installieren der Azure Line Interface (Azure CLI). Wenn Sie Probleme mit dem entsprechen, Zielwertsuche Lösungen in die [Seite zu behandeln](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="212-what-you-will-learn"></a>2.1.2 Gelernte wird

- So installieren Sie Azure CLI.
- So fügen Sie die IoT Untergruppen von Azure CLI.

## <a name="213-what-you-need"></a>2.1.3, benötigen Sie

- Einem Mac mit Verbindung zum Internet
- Ein aktives Azure-Abonnement. Wenn Sie kein Konto haben, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/) nur wenigen Minuten erstellen.

## <a name="214-install-python"></a>2.1.4 installieren Sie Python

Zwar Mac OS im Paket mit Python 2.7 geliefert wird, empfiehlt es sich Python bis Homebrew installieren. Finden Sie unter [Installieren von Python in Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Installieren Sie Python und Pip, indem Sie den folgenden Befehl ausführen:

```bash
brew install python
```

## <a name="215-install-the-azure-cli"></a>2.1.5 installieren Sie die Azure CLI

Die CLI Azure bietet eine für mehrere Plattformen Befehlszeilenoptionen für Azure, aktivieren Sie arbeiten direkt über Ihre Befehlszeile bereitstellen und Verwalten von Ressourcen. 

Gehen Sie folgendermaßen vor, um die neueste Azure CLI zu installieren:

1. Führen Sie die folgenden Befehle in einem Terminal-Fenster. Es kann Azure CLI installieren fünf Minuten dauern.

    ```bash
    pip install azure-cli-core==0.1.0b7 azure-cli-vm==0.1.0b7 azure-cli-storage==0.1.0b7 azure-cli-role==0.1.0b7 azure-cli-resource==0.1.0b7 azure-cli-profile==0.1.0b7 azure-cli-network==0.1.0b7 azure-cli-iot==0.1.0b7 azure-cli-feedback==0.1.0b7 azure-cli-configure==0.1.0b7 azure-cli-component==0.1.0b7 azure-cli==0.1.0b7
    ```

2. Überprüfen Sie die Installation, indem Sie den folgenden Befehl ausführen:

    ```bash
    az iot -h
    ```
  
Die folgende Ausgabe sollte angezeigt werden, wenn die Installation erfolgreich ist.

![BW Iot -h](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="215-summary"></a>2.1.5 Zusammenfassung

Sie haben Azure CLI installiert haben. Fahren Sie mit dem nächsten Abschnitt, um Ihre Identität Azure IoT Hub und Gerät, die Verwendung der CLI Azure erstellen.

## <a name="next-steps"></a>Nächste Schritte

[2.2 Erstellen Sie Ihrer IoT Hub und registrieren Sie der Brombeere Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)
