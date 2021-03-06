---
title: Oracle-REF CURSORs
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 7cd29a6a20015c7ce4475b0211cb07f7ee78b530
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794875"
---
# <a name="oracle-ref-cursors"></a>Oracle-REF CURSORs
Der .NET Framework Datenanbieter für Oracle unterstützt den Oracle **ref Cursor** -Datentyp. Wenn Sie beim Arbeiten mit Oracle-REF CUSORS diesen Datenanbieter verwenden, müssen Sie das jeweilige Verhalten berücksichtigen.  
  
> [!NOTE]
> Das jeweilige Verhalten weicht von dem des Microsoft OLE DB-Anbieters für Oracle (MSDAORA) ab.  
  
- Aus Leistungsgründen bindet die Datenanbieter für Oracle die **ref Cursor** -Datentypen nicht automatisch wie MSDAORA, es sei denn, Sie geben Sie explizit an.  
  
- Der Datenanbieter unterstützt keine ODBC-Escapesequenzen, auch nicht das {resultset}-Escapezeichen für die Angabe von REF CURSOR-Parametern.  
  
- Zum Ausführen einer gespeicherten Prozedur, die Ref Cursors zurückgibt, müssen Sie die Parameter in <xref:System.Data.OracleClient.OracleParameterCollection> mit einem <xref:System.Data.OracleClient.OracleType> - **Cursor** und einem <xref:System.Data.OracleClient.OracleParameter.Direction%2A> -Wert von **Output**definieren. Mit diesem Datenanbieter können REF CURSORs nur als Ausgabeparameter gebunden werden. Das Binden von REF CURSORs als Eingabeparameter wird von diesem Datenanbieter nicht unterstützt.  
  
- Das Abrufen eines <xref:System.Data.OracleClient.OracleDataReader> aus dem Parameterwert wird nicht unterstützt. Nach dem Ausführen des Befehls weisen die Werte den Typ <xref:System.DBNull> auf.  
  
- Der einzige **CommandBehavior** -Enumerationswert, der mit Ref Cursors funktioniert (z. <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>b. beim Aufrufen von), ist **closeconnetction**; alle anderen werden ignoriert.  
  
- Die Reihenfolge der Ref Cursors in **OracleDataReader** hängt von der Reihenfolge der Parameter in der **OracleParameterCollection**ab. Die <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A>-Eigenschaft wird ignoriert.  
  
- Der Datentyp der PL/SQL- **Tabelle** wird nicht unterstützt. REF CURSORs sind im Vergleich effizienter. Wenn Sie einen **Tabellen** Datentyp verwenden müssen, verwenden Sie die OLE DB .NET-Datenanbieter mit MSDAORA.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [REF CURSOR-Beispiele](ref-cursor-examples.md)  
 Enthält drei Beispiele, in denen die Verwendung von REF CURSORs veranschaulicht wird.  
  
 [REF CURSOR-Parameter in OracleDataReader](ref-cursor-parameters-in-an-oracledatareader.md)  
 Veranschaulicht, wie eine gespeicherte PL/SQL-Prozedur ausgeführt wird, die einen REF CURSOR-Parameter zurückgibt und den Wert als **OracleDataReader**liest.  
  
 [Abrufen von Daten aus mehreren REF CURSORs mithilfe von OracleDataReader](retrieving-data-from-multiple-ref-cursors.md)  
 Veranschaulicht, wie eine gespeicherte PL/SQL-Prozedur ausgeführt wird, die zwei REF CURSOR-Parameter zurückgibt und die Werte mithilfe eines **OracleDataReader**liest.  
  
 [Auffüllen eines DataSets mit einem oder mehreren REF CURSORs](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Veranschaulicht das Ausführen einer gespeicherten PL/SQL-Prozedur, die zwei REF CURSOR-Parameter zurückgibt. Das <xref:System.Data.DataSet> wird mit den zurückgegebenen Zeilen aufgefüllt.  
  
## <a name="see-also"></a>Siehe auch

- [Oracle und ADO.NET](oracle-and-adonet.md)
- [Übersicht über ADO.NET](ado-net-overview.md)
