---
title: 'Gewusst wie: Zurückgeben eines LINQ-Abfrageergebnisses als bestimmter Typ'
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], specific type returned
- projection [LINQ in Visual Basic]
- anonymous types [Visual Basic]
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 621bb10a-e5d7-44fb-a025-317964b19d92
ms.openlocfilehash: 1084743b0c50d381375b76a3116ed7c9e6f9d769
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/22/2019
ms.locfileid: "74354203"
---
# <a name="how-to-return-a-linq-query-result-as-a-specific-type-visual-basic"></a>Gewusst wie: Zurückgeben eines LINQ-Abfrageergebnisses als ein bestimmter Typ (Visual Basic)
Language-Integrated Query (LINQ) vereinfacht den Zugriff auf Datenbankinformationen und das Ausführen von Abfragen. LINQ-Abfragen geben standardmäßig eine Liste von Objekten als anonymen Typ zurück. Sie können auch angeben, dass eine Abfrage eine Liste eines bestimmten Typs zurückgibt, indem Sie die `Select`-Klausel verwenden.  
  
 Im folgenden Beispiel wird gezeigt, wie eine neue Anwendung erstellt wird, die Abfragen für eine SQL Server Datenbank ausführt und die Ergebnisse als einen bestimmten benannten Typ projiziert. Weitere Informationen finden Sie unter [Anonyme Typen](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) und [SELECT-Klausel](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
 In den Beispielen in diesem Thema wird die Beispieldatenbank Northwind verwendet. Befindet sich diese Datenbank nicht auf Ihrem Entwicklungscomputer, können Sie diese aus dem Microsoft Download Center herunterladen. Anweisungen hierzu finden Sie unter [Herunterladen von Beispiel Datenbanken](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>So erstellen Sie eine Verbindung mit einer Datenbank  
  
1. Öffnen Sie in Visual Studio **Server-Explorer**/**Datenbank-Explorer** , indem Sie im Menü **Ansicht** auf **Server-Explorer** **/Datenbank-Explorer** klicken.  
  
2. Klicken Sie in **Server-Explorer** **Datenbank-Explorer**/mit der rechten Maustaste auf **Datenverbindungen** , und klicken Sie dann auf **Verbindung hinzufügen**.  
  
3. Geben Sie eine gültige Verbindung mit der Northwind-Beispieldatenbank an.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>So fügen Sie ein Projekt hinzu, das eine LINQ to SQL Datei enthält  
  
1. Zeigen Sie in Visual Studio im Menü **Datei** auf **Neu**, und klicken Sie auf **Projekt**. Wählen Sie Visual Basic **Windows Forms Anwendung** als Projekttyp aus.  
  
2. Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**. Wählen Sie die Element Vorlage **LINQ to SQL Klassen** aus.  
  
3. Nennen Sie die Datei `northwind.dbml`. Klicken Sie auf **Hinzufügen**. Der objektrelationaler Designer (O/R-Designer) wird für die Datei Northwind. dbml geöffnet.  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>So fügen Sie dem O/R-Designer abzufragende Tabellen hinzu  
  
1. Erweitern Sie in **Server-Explorer**/**Datenbank-Explorer**die Verbindung mit der Northwind-Datenbank. Erweitern Sie den Ordner **Tabellen** .  
  
     Wenn Sie den O/R-Designer geschlossen haben, können Sie ihn erneut öffnen, indem Sie auf die Datei Northwind. dbml, die Sie zuvor hinzugefügt haben, doppelklicken.  
  
2. Klicken Sie auf die Tabelle Customers, und ziehen Sie Sie in den linken Bereich des Designers.  
  
     Der Designer erstellt ein neues `Customer`-Objekt für das Projekt. Sie können ein Abfrageergebnis als `Customer` Typ oder als Typ projizieren, den Sie erstellen. In diesem Beispiel wird in einer späteren Prozedur ein neuer Typ erstellt und ein Abfrageergebnis als dieser Typ verwendet.  
  
3. Speichern Sie die Änderungen, und schließen Sie den Designer.  
  
4. Speichern Sie das Projekt.  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>So fügen Sie Code hinzu, um die Datenbank abzufragen und die Ergebnisse anzuzeigen  
  
1. Ziehen Sie aus der **Toolbox**ein <xref:System.Windows.Forms.DataGridView>-Steuerelement auf das standardmäßige Windows Form für Ihr Projekt, Form1.  
  
2. Doppelklicken Sie auf Form1, um die Form1-Klasse zu ändern.  
  
3. Fügen Sie nach der `End Class`-Anweisung der Form1-Klasse den folgenden Code hinzu, um einen `CustomerInfo`-Typ zum Speichern der Abfrageergebnisse für dieses Beispiel zu erstellen.  
  
     [!code-vb[VbLINQToSQLHowTos#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form8.vb#16)]  
  
4. Wenn Sie dem O/R-Designer Tabellen hinzugefügt haben, hat der Designer dem Projekt ein <xref:System.Data.Linq.DataContext> Objekt hinzugefügt. Dieses Objekt enthält den Code, den Sie für den Zugriff auf diese Tabellen benötigen, und für den Zugriff auf einzelne Objekte und Auflistungen für jede Tabelle. Das <xref:System.Data.Linq.DataContext>-Objekt für das Projekt wird basierend auf dem Namen der DBML-Datei benannt. Für dieses Projekt wird das <xref:System.Data.Linq.DataContext> Objekt `northwindDataContext`benannt.  
  
     Sie können eine Instanz des <xref:System.Data.Linq.DataContext> in Ihrem Code erstellen und die im O/R-Designer angegebenen Tabellen Abfragen.  
  
     Fügen Sie im `Load`-Ereignis der Form1-Klasse den folgenden Code hinzu, um die Tabellen abzufragen, die als Eigenschaften des Daten Kontexts verfügbar gemacht werden. Die `Select`-Klausel der Abfrage erstellt für jedes Element des Abfrage Ergebnisses einen neuen `CustomerInfo`-Typ anstelle eines anonymen Typs.  
  
     [!code-vb[VbLINQToSQLHowTos#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form8.vb#15)]  
  
5. Drücken Sie F5, um das Projekt auszuführen und die Ergebnisse anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch

- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [Abfragen](../../../../visual-basic/language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext-Methoden (O/R-Designer)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
