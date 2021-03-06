---
title: Lokaler Kanal
ms.date: 03/30/2017
ms.assetid: fa1917a4-f701-4e82-a439-14a16282c7cc
ms.openlocfilehash: 6bc1fac22f6eed3c9acb6b86f7611cbfb4e1d371
ms.sourcegitcommit: 5fb5b6520b06d7f5e6131ec2ad854da302a28f2e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/03/2019
ms.locfileid: "74714885"
---
# <a name="local-channel"></a>Lokaler Kanal
Der lokale Channel ist ein Windows Communication Foundation (WCF)-Transport Kanal, der für die Kommunikation innerhalb derselben Anwendungsdomäne verwendet wird. Dies ist nützlich bei Szenarien, in denen der Client und der Dienst in der gleichen Anwendungsdomäne ausgeführt werden und der Mehraufwand eines normalen WCF-Kanalstapels (Serialisierung und Deserialisierung von Meldungen) vermieden werden muss.  
  
## <a name="demonstrates"></a>Veranschaulicht  
 Lokaler Kanal  
  
## <a name="discussion"></a>Diskussion  
 Das Beispiel umfasst zwei Projektdateien.  
  
- **Localchannel**: die programmatische Darstellung des lokalen Kanals innerhalb der aktuellen Anwendungsdomäne. In diesem Projekt fügt die sendende Komponente die Nachricht einer Warteschlange im Arbeitsspeicher hinzu. Die empfangende Komponente ruft die Nachricht aus der Warteschlange ab, um sie zu empfangen.  
  
- **Clientandservice**: dieses Projekt hostet einen Dienst in einer Konsolenanwendung und führt dann einen Client aus, um den Dienst innerhalb derselben Anwendungsdomäne aufzurufen.  
  
 Aufgrund des Entwurfs des lokalen Kanals werden Kanalstapel und Serialisierungsvorgang ausgelassen, um die Geschwindigkeit zu erhöhen. Der lokale Transportkanal wird mit einer Warteschlange implementiert, mit der Dienstaufrufe vom Client zum Dienst transportiert und der Wert zum Client zurückgesendet wird. Im Beispiel werden die Objekte kopiert, statt Parameter und Rückgabewerte zu serialisieren.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1. Erstellen Sie die Projektmappe LocalChannel, und führen Sie sie aus.  
  
2. Der Diensthost wird gestartet, und der Client ruft den Dienst mithilfe des lokalen Kanals auf. Ein Konsolenfenster mit den Ergebnissen des Dienstaufrufs wird angezeigt.  
  
> [!IMPORTANT]
> Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Wenn dieses Verzeichnis nicht vorhanden ist, wechseln Sie zu [Windows Communication Foundation (WCF) und Windows Workflow Foundation (WF)-Beispiele für .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) , um alle Windows Communication Foundation (WCF) und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] Beispiele herunterzuladen. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\LocalChannel`
