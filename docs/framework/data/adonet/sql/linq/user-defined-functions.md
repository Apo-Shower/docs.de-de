---
title: Benutzerdefinierte Funktionen
ms.date: 03/30/2017
ms.assetid: 3304c9b2-5c7a-4a95-9d45-4f260dcb606e
ms.openlocfilehash: 40697da4fe678668f8f7ecda86abebf40da7b973
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792306"
---
# <a name="user-defined-functions"></a>Benutzerdefinierte Funktionen
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] verwendet Methoden in Ihrem Objektmodell, die benutzerdefinierte Funktionen darstellen. Sie definieren die Methoden als Funktionen, indem Sie das <xref:System.Data.Linq.Mapping.FunctionAttribute>-Attribut und bei Bedarf auch das <xref:System.Data.Linq.Mapping.ParameterAttribute>-Attribut anwenden. Weitere Informationen finden Sie [unter LINQ to SQL-Objektmodell](the-linq-to-sql-object-model.md).  
  
 Zur Vermeidung einer <xref:System.InvalidOperationException> müssen benutzerdefinierte Funktionen in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in einer der folgenden Formen vorliegen:  
  
- Eine als Methodenaufruf eingebundene Funktion, die über die richtigen Zuordnungsattribute verfügt. Weitere Informationen finden Sie unter [Attribut basierte Zuordnung](attribute-based-mapping.md).  
  
- Eine spezifische statische SQL-Methode für [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
- Eine Funktion, die von einer .NET Framework Methode unterstützt wird.  
  
 Dieser Abschnitt erläutert das Bilden und Aufrufen dieser Methoden in Ihrer Anwendung, wenn Sie den Code selbst schreiben. Entwickler, die Visual Studio verwenden, verwenden normalerweise die objektrelationaler Designer, um benutzerdefinierte Funktionen zuzuordnen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Vorgehensweise: Verwenden von benutzerdefinierten Skalarwertfunktionen](how-to-use-scalar-valued-user-defined-functions.md)  
 Beschreibt, wie eine Funktion, die Skalarwerte zurückgibt, implementiert wird.  
  
 [Vorgehensweise: Verwenden von benutzerdefinierten Tabellenwert Funktionen](how-to-use-table-valued-user-defined-functions.md)  
 Beschreibt, wie eine Funktion, die Tabellenwerte zurückgibt, implementiert wird.  
  
 [Vorgehensweise: Inline Aufrufe von benutzerdefinierten Funktionen](how-to-call-user-defined-functions-inline.md)  
 Erläutert Inline-Funktionsaufrufe und die Ausführungsunterschiede, wenn der Aufruf inline erfolgt.
