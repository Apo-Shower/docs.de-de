---
title: 'Vorgehensweise: Speichern und Wiederverwenden von Abfragen'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a012bd79-1809-45e3-adea-0229532396cc
ms.openlocfilehash: c023f7610576c017c91fdb919322acdf9003767a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781638"
---
# <a name="how-to-store-and-reuse-queries"></a>Vorgehensweise: Speichern und Wiederverwenden von Abfragen
Wenn eine Anwendung häufig strukturell ähnliche Abfragen ausführt, können Sie häufig die Leistung steigern, indem Sie die Abfrage einmal kompilieren und dann mehrmals mit verschiedenen Parametern ausführen. So können beispielsweise mithilfe einer Anwendung alle Kunden in einer bestimmten Stadt abgerufen werden, wobei die Stadt zur Laufzeit vom Benutzer in einem Formular festgelegt wird. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]unterstützt die Verwendung von *kompilierten Abfragen* zu diesem Zweck.  
  
> [!NOTE]
> Dieses Nutzungsmuster stellt die gängigste Verwendung für kompilierte Abfragen dar. Andere Ansätze sind möglich. Kompilierte Abfragen können beispielsweise als statische Member einer partiellen Klasse gespeichert werden, die den vom Entwickler erzeugten Code ergänzt.  
  
## <a name="example"></a>Beispiel  
 In vielen Szenarien möchten Sie ggf. die Abfragen über Threadbegrenzungen hinweg wiederverwenden. In solchen Fällen ist die Speicherung kompilierter Abfragen in statischen Variablen besonders effektiv. Das folgende Codebeispiel basiert auf einer `Queries`-Klasse zum Speichern kompilierter Abfragen sowie auf einer Northwind-Klasse, die einen stark typisierten <xref:System.Data.Linq.DataContext> darstellt.  
  
 [!code-csharp[DLinqQuerying#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#6)]
 [!code-vb[DLinqQuerying#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#6)]  
  
 [!code-csharp[DLinqQuerying#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#7)]
 [!code-vb[DLinqQuerying#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#7)]  
  
## <a name="example"></a>Beispiel  
 Sie können derzeit keine Abfragen (in statischen Variablen) speichern, die einen *anonymen Typ*zurückgeben, da der Typ keinen Namen hat, der als generisches Argument bereitgestellt werden kann. Im folgenden Beispiel wird veranschaulicht, wie sich das Problem durch Erstellen eines Typs umgehen lässt, der das Ergebnis darstellen kann. Anschließend wird dieser Typ als generisches Argument verwendet.  
  
 [!code-csharp[DLinqQuerying#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#8)]
 [!code-vb[DLinqQuerying#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#8)]  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Data.Linq.CompiledQuery>
- [Abfragekonzepte](query-concepts.md)
- [Abfragen der Datenbank](querying-the-database.md)
