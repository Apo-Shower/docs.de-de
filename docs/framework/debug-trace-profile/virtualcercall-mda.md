---
title: VirtualCERCall-MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- virtualCERCall MDA
- virtual CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
ms.openlocfilehash: 49ba4e7ca0b8ed2e433053130bc9ca2742c72ec9
ms.sourcegitcommit: 9c54866bcbdc49dbb981dd55be9bbd0443837aa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2020
ms.locfileid: "77217198"
---
# <a name="virtualcercall-mda"></a>VirtualCERCall-MDA
Der `virtualCERCall`-MDA (Assistent für verwaltetes Debuggen) wird als Warnung aktiviert und gibt an, dass eine Aufrufwebsite in einem Aufrufdiagramm eines eingeschränkten Ausführungsbereichs (CER) auf ein virtuelles Ziel verweist, also ein virtueller Aufruf an eine virtuelle, nicht finale Methode oder ein Aufruf, der eine Schnittstelle verwendet. Die Common Language Runtime (CLR) kann die Zielmethode dieser Aufrufe der Intermediate Language und der Metadatenanalyse nicht allein vorhersagen. Folglich kann die Aufrufstruktur nicht als Teil des CER-Diagramms vorbereitet und Threadabbrüche in dieser Unterstruktur nicht automatisch blockiert werden. Dieser MDA gibt eine Warnung für die Fälle aus, in denen ein CER erweitert werden muss. Dazu werden explizite Aufrufe der <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>-Methode verwendet, sobald die zusätzlichen Informationen, die zur Berechnung des Aufrufsziels erforderlich sind, zur Laufzeit bekannt sind.  
  
## <a name="symptoms"></a>Symptome  
 CERs, die nicht ausgeführt werden, wenn ein Thread abgebrochen oder eine Anwendungsdomäne entladen wird.  
  
## <a name="cause"></a>Ursache  
 Ein CER enthält einen Aufruf einer virtuellen Methode, die nicht automatisch vorbereitet werden kann.  
  
## <a name="resolution"></a>Lösung  
 Rufen Sie <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> für die virtuelle Methode auf.  
  
## <a name="effect-on-the-runtime"></a>Auswirkungen auf die Laufzeit  
 Dieser MDA hat keine Auswirkungen auf die CLR.  
  
## <a name="output"></a>Output  
  
```output
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## <a name="configuration"></a>Konfiguration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Beispiel  
  
```csharp
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## <a name="see-also"></a>Weitere Informationen

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [Diagnosing Errors with Managed Debugging Assistants (Fehlerdiagnose mit den Assistenten für verwaltetes Debugging)](diagnosing-errors-with-managed-debugging-assistants.md)
- [Interop Marshaling (Interop-Marshalling)](../interop/interop-marshaling.md)
