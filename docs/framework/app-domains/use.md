---
title: Verwenden von Anwendungsdomänen
ms.date: 03/30/2017
helpviewer_keywords:
- application domains, about
- common language runtime, application domains
- runtime, application domains
ms.assetid: c6d99815-e022-4d2c-9420-1d7ab5b9d504
ms.openlocfilehash: d6bbc2648608e9542158e0f281984174447633a4
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73119723"
---
# <a name="using-application-domains"></a>Verwenden von Anwendungsdomänen

Anwendungsdomänen stellen eine Isolationseinheit für die Common Language Runtime (CLR) bereit. Sie werden in einem Prozess erstellt und dort ausgeführt. Anwendungsdomänen werden normalerweise von einem Runtimehost erstellt. Dabei handelt es sich um eine Anwendung, die dafür verantwortlich ist, die Runtime in einen Prozess zu laden und Benutzercode innerhalb einer Anwendungsdomäne auszuführen. Der Runtimehost erstellt einen Prozess und eine Standardanwendungsdomäne und führt darin verwalteten Code aus. Runtimehosts sind z.B. ASP.NET, Microsoft Internet Explorer und Windows-Shell.  
  
Für die meisten Anwendungen müssen Sie nicht Ihre eigene Anwendungsdomäne erstellen. Der Runtimehost erstellt alle erforderlichen Anwendungsdomänen für Sie. Sie können aber zusätzliche Anwendungsdomänen erstellen und konfigurieren, wenn Ihre Anwendung Code isolieren oder DLLs verwenden und entladen muss.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  

[Vorgehensweise: Erstellen einer Anwendungsdomäne](how-to-create-an-application-domain.md)  
Erläutert, wie Sie eine Anwendungsdomäne programmgesteuert erstellen  
  
[Vorgehensweise: Entladen einer Anwendungsdomäne](how-to-unload-an-application-domain.md)  
Erläutert, wie Sie eine Anwendungsdomäne programmgesteuert entladen  
  
[Vorgehensweise: Konfigurieren einer Anwendungsdomäne](how-to-configure-an-application-domain.md)  
Führt Sie in die Konfiguration einer Anwendungsdomäne ein  
  
[Abrufen von Setupinformationen aus einer Anwendungsdomäne](retrieve-setup-information.md)  
Erläutert, wie Sie Setupinformationen aus einer Anwendungsdomäne abrufen können  
  
[Vorgehensweise: Laden von Assemblys in eine Anwendungsdomäne](how-to-load-assemblies-into-an-application-domain.md)  
Erläutert wie Sie eine Assembly in eine Anwendungsdomäne laden können  
  
[Vorgehensweise: Abrufen von Typ- und Memberinformationen aus einer Assembly](../reflection-and-codedom/get-type-member-information.md)  
Erläutert, wie Sie Informationen zu einer Assembly abrufen können  
  
[Erstellen von Schattenkopien von Assemblys](shadow-copy-assemblies.md)  
Erläutert, wie Sie Assemblys mit Schattenkopien aktualisieren können, während diese gerade verwendet werden, und wie Sie Schattenkopien konfigurieren können  
  
[Vorgehensweise: Empfangen von Ausnahmebenachrichtigungen (erste Chance)](how-to-receive-first-chance-exception-notifications.md)  
Erläutert, wie Sie eine Benachrichtigung bezüglich einer ausgelösten Ausnahme abrufen können, bevor die CLR mit dem Suchen nach Ausnahmehandlern beginnt.  
  
[Auflösen beim Laden von Assemblys](../../standard/assembly/resolve-loads.md)  
Führt Sie in das Verwenden des Ereignisses <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> ein, um fehlgeschlagene Assemblyladevorgänge aufzulösen.  
  
## <a name="reference"></a>Referenz  

<xref:System.AppDomain>  
Stellt eine Anwendungsdomäne dar Bietet Methoden zum Erstellen und Steuern von Anwendungsdomänen  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
[Assemblys in .NET](../../standard/assembly/index.md)  
Gibt einen Überblick über von Assemblys ausgeführte Funktionen  
  
[Programmieren mit Assemblys](../../standard/assembly/program.md)  
Beschreibt das Erstellen, Signieren und Festlegen von Attributen für Assemblys.  
  
[Ausgeben von dynamischen Methoden und Assemblys](../reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
Beschreibt das Erstellen dynamischer Assemblys.  
  
[Anwendungsdomänen](application-domains.md)  
Bietet eine konzeptionelle Übersicht über Anwendungsdomänen.  
  
[Übersicht über Reflektion](../reflection-and-codedom/reflection.md)  
Beschreibt, wie die **Reflektion**-Klasse verwendet wird, um Informationen zu einer Assembly abzurufen.
