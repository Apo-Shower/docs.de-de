---
title: Ereignisse freigegebener WithEvents-Variablen können nicht von freigegebenen Methoden behandelt werden.
ms.date: 07/20/2015
f1_keywords:
- bc30594
- vbc30594
helpviewer_keywords:
- BC30594
ms.assetid: 5b9fceb4-ab11-41bb-ad3b-6f1a9da8ae7e
ms.openlocfilehash: d6067c75835ecd14f1dd796c20ae3f29f456e541
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642929"
---
# <a name="events-of-shared-withevents-variables-cannot-be-handled-by-non-shared-methods"></a>Ereignisse freigegebener WithEvents-Variablen können nicht von freigegebenen Methoden behandelt werden.
Eine Variable mit dem `Shared` Modifizierer ist eine freigegebene Variable. Eine freigegebene Variable gibt genau einen Speicherort an. Eine Variable mit dem `WithEvents` Modifizierer bestätigt, dass der Typ, der die Variable angehört, den Satz von Ereignissen verarbeitet der Variablen ausgelöst. Ein Wert der Variablen zugewiesen ist, die Eigenschaft erstellt, wenn die `WithEvents` Deklaration hebt alle vorhandenen Ereignishandler und verknüpft den neuen Ereignishandler über die `Add` Methode.  
  
 **Fehler-ID:** BC30594  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
- Deklarieren Sie Ihre Ereignishandler `Shared`.  
  
## <a name="see-also"></a>Siehe auch

- [Shared](../../../visual-basic/language-reference/modifiers/shared.md)
- [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)
