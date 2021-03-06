---
title: -utf8output
ms.date: 07/20/2015
helpviewer_keywords:
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
ms.openlocfilehash: 5cdc60888cd872940afc1b03febd879bb6d87c2e
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/22/2019
ms.locfileid: "74350838"
---
# <a name="-utf8output-visual-basic"></a>-utf8output (Visual Basic)
Zeigt die Compilerausgabe mit UTF-8-Codierung an.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-utf8output[+ | -]  
```  
  
## <a name="arguments"></a>Argumente  
 `+` &#124; `-`  
 Optional. Der Standardwert für diese Option ist `-utf8output-`. Dies bedeutet, dass die Compilerausgabe keine UTF-8-Codierung verwendet. Die Angabe von `-utf8output` ist mit der Angabe von `-utf8output+` identisch.  
  
## <a name="remarks"></a>Hinweise  
 In einigen internationalen Konfigurationen kann die Compilerausgabe nicht ordnungsgemäß in der-Konsole angezeigt werden. Verwenden Sie in solchen Situationen `-utf8output`, und leiten Sie die Compilerausgabe in eine Datei um.  
  
> [!NOTE]
> Die `-utf8output`-Option ist in der Visual Studio-Entwicklungsumgebung nicht verfügbar. Sie ist nur verfügbar, wenn Sie über die Befehlszeile kompilieren.  
  
## <a name="example"></a>Beispiel  
 Der folgende Code kompiliert `In.vb` und weist den Compiler an, die Ausgabe mit UTF-8-Codierung anzuzeigen.  
  
```console  
vbc -utf8output in.vb  
```  
  
## <a name="see-also"></a>Siehe auch

- [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)
- [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
