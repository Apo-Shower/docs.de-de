---
title: Generieren und Kompilieren von dynamischem Quellcode
ms.date: 03/30/2017
helpviewer_keywords:
- Code Document Object Model
- System.CodeDom namespace
- language-independent source code modeling
- CodeDOM
- multiple languages supported by CodeDOM
- source code in multiple languages
- languages, multiple language support by CodeDOM
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
ms.openlocfilehash: 7379bac07de9b78369d3742fa3288f6fea6a573f
ms.sourcegitcommit: 8c99457955fc31785b36b3330c4ab6ce7984a7ba
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/29/2019
ms.locfileid: "75544983"
---
# <a name="compile-and-generate-dynamic-source-code"></a>Kompilieren und Generieren von dynamischem Quellcode

Das .NET Framework enthält einen Mechanismus, der „Code Document Object Model“ (CodeDOM) genannt wird, und mit dem Programmentwickler, die Quellcode ausgeben, Quellcode in mehreren Programmiersprachen zur Runtime generieren können und das alles auf Grundlage eines einzigen Modells, das den zu rendernden Code darstellt.  
  
Um den Quellcode darzustellen, werden CodeDOM-Elemente miteinander verknüpft, damit sie eine Datenstruktur bilden, die als CodeDOM-Diagramm bekannt ist, der die Struktur von Quellcode modelliert.  
  
Der <xref:System.CodeDom?displayProperty=fullName>-Namespace definiert Typen, die die logische Struktur des Quellcodes darstellen können, unabhängig von einer bestimmten Programmiersprache. Der <xref:System.CodeDom.Compiler?displayProperty=fullName>-Namespace definiert Typen zum Generieren von Quellcode von CodeDOM-Diagrammen und zum Verwalten der Quellcodekompilierung in unterstützten Sprachen. Compileranbieter oder Entwickler können die Reihe der unterstützten Sprachen erweitern.  
  
Sprachunabhängige Quellcodemodellierung kann von Wert sein, wenn ein Programm Quellcode für ein Programm-Modell in mehreren Sprachen oder für eine ungenaue Zielsprache generieren muss. Einige Designer nutzen z.B. CodeDOM als Sprachabstraktions-Schnittstelle, um Quellcode in der korrekten Programmiersprache zu erstellen, falls die CodeDOM-Unterstützung für die Sprache verfügbar ist.  
  
Das .NET Framework enthält Codegeneratoren und Codecompiler für <xref:Microsoft.CSharp.CSharpCodeProvider>, <xref:Microsoft.JScript.JScriptCodeProvider> und <xref:Microsoft.VisualBasic.VBCodeProvider>.  
  
## <a name="in-this-section"></a>In diesem Abschnitt

- [Verwenden von CodeDOM](using-the-codedom.md)

  Beschreibt häufige Verwendungen und stellt die Erstellung eines einfachen Objektdiagramms mithilfe von CodeDOM dar.  
  
- [Generieren von Quellcode und Kompilieren eines Programms aus einem CodeDOM-Diagramm](generating-and-compiling-source-code-from-a-codedom-graph.md)  

  Beschreibt, wie Quellcode generiert und der generierte Code mit einem externen Compiler mithilfe von im `System.CodeDom.Compiler`-Namespace definierten Klassen kompiliert wird.  
  
- [Vorgehensweise: Erstellen einer XML-Dokumentationsdatei mit CodeDOM](how-to-create-an-xml-documentation-file-using-codedom.md)  

  Beschreibt, wie CodeDOM zum Generieren von Code mit Kommentaren der XML-Dokumentation verwendet wird und wie der generierte Code kompiliert wird, damit die Ausgabe der XML-Dokumentation erstellt wird.  
  
- [Vorgehensweise: Erstellen einer Klasse mit CodeDOM](how-to-create-a-class-using-codedom.md)  

  Beschreibt, wie CodeDOM zum Generieren einer Klasse verwendet wird, die Felder, Eigenschaften, eine Methode, einen Konstruktor und einen Einstiegspunkt enthält.  
  
## <a name="reference"></a>Referenz  

- <xref:System.CodeDom>  

  Definiert Elemente, die Codeelemente in Programmiersprachen darstellen, die auf die Common Language Runtime abzielen.  
  
- <xref:System.CodeDom.Compiler>  

  Definiert Schnittstellen zum Generieren und Kompilieren von Code zur Runtime.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  

- [CodeDom Quick Reference](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100)) bietet Entwicklern eine schnelle Möglichkeit, die CodeDOM-Elemente zu finden, die Quell Code Elemente darstellen.
