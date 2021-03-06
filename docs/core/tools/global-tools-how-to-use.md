---
title: 'Tutorial: Installieren und Verwenden eines globalen .NET Core-Tools'
description: Erfahren Sie, wie Sie ein .NET-Tool als globales Tool installieren und verwenden.
ms.date: 02/12/2020
ms.openlocfilehash: 9f8378e50fd2544eedbbaaeffb89d67800ec6880
ms.sourcegitcommit: 00aa62e2f469c2272a457b04e66b4cc3c97a800b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2020
ms.locfileid: "78156737"
---
# <a name="tutorial-install-and-use-a-net-core-global-tool-using-the-net-core-cli"></a>Tutorial: Erstellen und Verwenden eines globalen .NET Core-Tools mithilfe der .NET Core-CLI

**Dieser Artikel gilt für:** ✔️ .NET Core 2.1 SDK und neuere Versionen

In diesem Tutorial erfahren Sie, wie ein globales Tools installiert und verwendet wird. Sie verwenden ein Tool, das Sie im [ersten Tutorial dieser Reihe](global-tools-how-to-create.md) erstellen.

## <a name="prerequisites"></a>Voraussetzungen

* Absolvieren Sie das [erste Tutorial dieser Reihe](global-tools-how-to-create.md).

## <a name="use-the-tool-as-a-global-tool"></a>Verwenden des Tools als globales Tool

1. Installieren Sie das Tool aus dem Paket, indem Sie den Befehl [dotnet tool install](dotnet-tool-install.md) im Projektordner *microsoft.botsay* ausführen:

   ```dotnetcli
   dotnet tool install --global --add-source ./nupkg microsoft.botsay
   ```

   Der Parameter `--global` weist die .NET Core-CLI an, die Binärdateien des Tools an einem Standardspeicherort zu installieren, der automatisch zur Umgebungsvariablen PATH hinzugefügt wird.

   Der Parameter `--add-source` weist die .NET Core-CLI an, vorübergehend das Verzeichnis *./nupkg* als zusätzlichen Quellfeed für NuGet-Pakete zu verwenden. Sie haben Ihr Paket mit einem eindeutigen Namen versehen, um sicherzustellen, dass es nur im Verzeichnis *./nupkg* und nicht auf der Website Nuget.org gefunden wird.

   Die Ausgabe zeigt den zum Aufrufen des Tools verwendeten Befehl und die installierte Version:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Rufen Sie das Tool auf:

   ```console
   botsay hello from the bot
   ```

   > [!NOTE]
   > Wenn dieser Befehl fehlschlägt, müssen Sie möglicherweise ein neues Terminal öffnen, um PATH zu aktualisieren.

1. Entfernen Sie das Tool, indem Sie den Befehl [dotnet tool uninstall](dotnet-tool-uninstall.md) ausführen:

   ```dotnetcli
   dotnet tool uninstall -g microsoft.botsay
   ```

## <a name="use-the-tool-as-a-global-tool-installed-in-a-custom-location"></a>Verwenden des an einem benutzerdefinierten Speicherort installierten Tools als globales Tool

1. Installieren Sie das Toll aus dem Paket.

   Unter Windows:

   ```dotnetcli
   dotnet tool install --tool-path c:\dotnet-tools --add-source ./nupkg microsoft.botsay
   ```

   Unter Linux oder macOS:

   ```dotnetcli
   dotnet tool install --tool-path ~/bin --add-source ./nupkg microsoft.botsay
   ```

   Der Parameter `--tool-path` weist die .NET Core-CLI an, die Binärdateien des Tools am angegebenen Speicherort zu installieren. Wenn das Verzeichnis noch nicht vorhanden ist, wird es erstellt. Dieses Verzeichnis wird nicht automatisch zur Umgebungsvariablen PATH hinzugefügt.

   Die Ausgabe zeigt den zum Aufrufen des Tools verwendeten Befehl und die installierte Version:

   ```console
   You can invoke the tool using the following command: botsay
   Tool 'microsoft.botsay' (version '1.0.0') was successfully installed.
   ```

1. Rufen Sie das Tool auf:

   Unter Windows:

   ```console
   c:\dotnet-tools\botsay hello from the bot
   ```

   Unter Linux oder macOS:

   ```console
   ~/bin/botsay hello from the bot
   ```

1. Entfernen Sie das Tool, indem Sie den Befehl [dotnet tool uninstall](dotnet-tool-uninstall.md) ausführen:

   Unter Windows:

   ```dotnetcli
   dotnet tool uninstall --tool-path c:\dotnet-tools microsoft.botsay
   ```

   Unter Linux oder macOS:

   ```dotnetcli
   dotnet tool uninstall --tool-path ~/bin microsoft.botsay
   ```

## <a name="troubleshoot"></a>Problembehandlung

Falls im Verlauf des Tutorials eine Fehlermeldung angezeigt wird, finden Sie unter [Behandlung von Problemen bei der Nutzung von .NET Core-Tools](troubleshoot-usage-issues.md) weitere Informationen.

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie ein Tool als globales Tool installiert und verwendet. Um dasselbe Tool als lokales Tool zu installieren und zu verwenden, fahren Sie mit dem nächsten Tutorial fort.

> [!div class="nextstepaction"]
> [Installieren und Verwenden lokaler Tools](local-tools-how-to-use.md)
